# Designing a controlled AI delivery workflow

*Engineering note from a private project; this page is a public design summary, not an executable release or independent production validation.*

Delegating a coding task to an AI worker creates two separate problems: producing a candidate change and deciding whether that change is acceptable. ASTRA Lab documents a workflow that keeps these steps distinct. A coordinating process prepares a task contract and a Git worktree, delegates a bounded task, then reviews the resulting diff and checks before integration.

## Design choices

The worktree gives the candidate change a separate working context and makes the diff reviewable. It is not a system sandbox: the worker's actual permissions and host controls still matter. Provider access remains on the authorized host rather than being bundled into the delivery package.

The runner has an explicit stop mechanism. A stop blocks new launches and interrupts the active runner; resumption is an explicit decision. The project also documents a local demonstration using a real child process without calling a model provider, including a check that a new launch is refused after STOP. This separates testing orchestration behavior from testing a model's output.

The trade-off is that isolation, repeatability and human review add steps. A clean diff is not proof of correctness, and an offline runner test does not establish provider reliability or the quality of an AI-generated solution. Process termination has platform-specific limits; a worktree alone does not contain a malicious or misconfigured process.

## How to challenge the design

Use a disposable repository and a deterministic worker fixture. Give it a small task, inspect the produced diff, run relevant tests and verify that integration is a separate decision. Interrupt a running fixture, then attempt a second launch while STOP remains active. Record the result and check that the launch was refused. Test timeout and duplicate-task behavior independently, and repeat on each supported platform.

A meaningful handoff would retain the task scope, diff, check results and known limits. It should describe observed behavior without implying that every possible provider failure or escape path has been tested.

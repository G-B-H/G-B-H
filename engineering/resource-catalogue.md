# Designing a resource catalogue for decisions

*Engineering note from a private project; this page is a public design summary, not an executable release or independent production validation.*

A collection of saved links can help discovery, but a saved link does not establish that its contents were read, understood or suitable for use. MENINX Catalogue addresses that gap by organizing resources for review and comparison while keeping the decision with a person.

## Design choices

The catalogue distinguishes the depth of material available: a link alone, a cached document, or an existing analysis. Prepared decision briefs describe an observed capability, a possible use, limitations and a suggested trial. The briefs distinguish source claims, documentary observations and inferences. A prepared brief is therefore a review aid, not an approval or an installation.

Guided recommendations are tied to the cached material used to prepare them. If that material changes or disappears, a recommendation is excluded from new guided batches until revalidated; existing batches remain stable and stale justifications are flagged. This is a deliberate balance between freshness and continuity: the check concerns the local cache and does not guarantee that a remote source is current.

The workflow separates acquiring a resource, qualifying it through review, and selecting it for possible production use. Even a human selection does not establish that an integration succeeded. Decisions can be undone until superseded by a newer change. Drafts and saved decisions have distinct behavior, and conflicting remote changes require an explicit choice for each conflict.

## How to challenge the design

With fictional resources, create a review batch and compare items with different levels of available evidence. Change a cached source and check that new guided recommendations exclude its stale brief while the earlier batch remains inspectable. Record a decision, undo it before another change, and exercise conflicting edits from separate sessions. Check that the interface explains which information is a draft and what has been saved.

Evidence should include the test data, expected and observed states, and unresolved usability or synchronization limits. The test would assess the scenarios exercised, not the quality of every resource or every future decision.

# Designing a bounded service supervisor

*Engineering note from a private project; this page is a public design summary, not an executable release or independent production validation.*

A service supervisor has to recover from ordinary failures without turning a fault into a restart storm or damaging an unrelated process. In MENINX Runtime, the design separates process lifecycle management from higher-level work orchestration. Its responsibility is deliberately narrower: start and stop services, track health, bound recovery and provide installation and rollback procedures.

## Design choices

The supervisor uses an explicit stop state to prevent new restarts. A circuit breaker pauses recovery after repeated failures instead of retrying indefinitely. To recover after a supervisor crash, a fresh predecessor state can identify previously owned child processes. Ownership matters: when an unknown process holds a configured port, the documented behavior is to refuse the conflicting start rather than kill that process.

Configuration is separated from versioned code, with secrets kept in the host environment or a service-local store. Runtime state is written atomically. A watchdog and rollback procedure complement the supervisor: the first supports liveness; the second gives an operator a route back after an installation change.

These controls make failure behavior easier to reason about, but they do not eliminate the need for operator judgment. A restart pause trades immediate availability for containment; a conservative ownership check can leave a service unavailable until the conflict is investigated. A watchdog also cannot prove that an application is serving correct results.

## How to challenge the design

In an isolated test environment, run a disposable service that exits repeatedly and check that retries stop at the configured boundary. Issue STOP during recovery and confirm that no new start is admitted. Then occupy the service's intended port with an unrelated fixture: the expected result is a reported conflict with the fixture still running. Finally, simulate a supervisor restart and exercise recovery and rollback with disposable configuration.

The useful evidence would include the commands, observed state transitions, logs and platform details, including failures. Those observations would support the specific scenarios tested, not a general availability or safety guarantee.

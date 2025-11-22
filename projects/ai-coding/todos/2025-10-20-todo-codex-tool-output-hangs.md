---
created: 2027-10-20
updated: 2027-10-20
topic: codex cli hang visibility
tags: [codex, tooling, ux]
---

# TODO: Codex Tool Output Visibility

## Issue
Codex suppresses stdout and stderr from its tool or shell commands, so when one of those commands blocks there is no diagnostic output. The whole session appears frozen with no timeout, so the only way to move forward is to interrupt Codex manually without learning what went wrong.

## Next Step
- [ ] Track or open an issue requesting surfaced tool output and saner timeouts so hangs can be debugged instead of blindly terminated.

Tracked issues:
- (add once located)

Legend (from RFC2119): !=MUST, ~=SHOULD, ≉=SHOULD NOT, ⊗=MUST NOT, ?=MAY.

## Working principles

**Do**
- !: Implement small, well scoped changes that follow existing conventions for a single task at a time.
- !: Keep all tests and policy checks green. Test prior to PR
- !: Maintain quality and automation and ADR discipline.
- ~: Create simple, maintainable designs over clever abstractions.
- ~: Follow TDD. 
- !: Atomic commits as you go, following conventional commit format
- !: After finishing work (all todos done, create pr), review session and propose recommended improvements to AGENTS.md, custom agents, and skills.

**Do Not**

- ⊗: introduce secrets, tokens, credentials, or private keys in any form.
- ⊗: Redesign the architecture without explicit instruction or approval
- ⊗: Introduce new tools or services without explicit instruction or approval
- ⊗: Make large sweeping changes across many apps or modules without explicit approval
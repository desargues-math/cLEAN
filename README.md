# cLEAN

**A framework for agent-assisted Lean library engineering.**

cLEAN guides coding agents through auditing and refactoring existing Lean 4
formalizations to make them easier to understand, maintain, and reuse.

It reviews theorem assumptions, searches Mathlib and local code for reusable
results, and improves APIs, module structure, proofs, and documentation. Changes
are checked with the project's Lean toolchain.

For larger projects, cLEAN first maps the mathematics and dependencies. Its
[structure workflow](workflows/structure.md) helps group related declarations,
split or combine modules, and update imports and uses in checked batches. It
keeps existing organization where that already serves the project.

## Getting started

Clone the current version from `main`:

```sh
git clone --depth 1 --branch main https://github.com/desargues-math/cLEAN.git
```

Open your Lean project in your coding agent and ask:

> Read `/path/to/cLEAN/SKILL.md` and audit this project.

Replace `/path/to/cLEAN` with the clone's location. Verification requires your
project's Lean toolchain and dependencies.

To update your clone:

```sh
git -C /path/to/cLEAN pull --ff-only
```

## Example requests

Audits and plans report findings without editing source files. Refactoring
requests apply changes and verify the affected code.

Replace paths and limits in these examples with your own:

```text
Use cLEAN to audit /path/to/formalization.
Focus on reusable APIs and theorem statement dependencies. Save the report
under /path/to/run-records and state which areas were actually inspected.
```

```text
Use cLEAN to refactor /path/to/formalization for reuse and maintainability.
Keep its Lean and Mathlib revisions fixed and preserve all main results.
Start with a representative foundation and consumer, then continue through
Algebra/Orders and its affected consumers. Apply and verify the changes;
record migration notes and remaining work under /path/to/run-records.
```

```text
Use cLEAN to turn the audit at /path/to/audit.md into an executable plan.
Include a target module structure, preservation checks, task dependencies,
and a first repair batch.
```

```text
Use cLEAN to verify the current patch against revision BASE.
Check statement/definition preservation, axioms, affected consumers,
and the claimed improvement. Report any unperformed checks explicitly.
```

## Reuse during cleanup

cLEAN searches Mathlib and local sources for results that can replace repeated
proofs or redundant declarations. It checks that replacements preserve the
original claims, updates affected uses, and verifies the changes.

Useful wrappers can remain when they provide a clearer mathematical interface,
support automation, or meet compatibility requirements. Their proofs should
reuse existing results where suitable.

See the [duplication workflow](workflows/inclusive-duplication.md) for the review
procedure and optional numerical comparisons.

## Work to the requested scope

Focused requests cover the named repair and the code that depends on it.
Whole-repository or broad multi-area requests use
[sustained repository work](workflows/campaign.md): review each area, apply and
check changes in batches, then revisit the changed code for further improvements.

For larger runs, specify the scope, where to save progress, and any time or
compute limits. For example:

```text
Use cLEAN to audit, refactor, and verify /path/to/formalization.
Cover the whole repository and preserve mathematical claims and dependency pins.
Save changes, check results, and remaining work under /path/to/run-records.
```

To continue later, ask: "Resume this cLEAN cleanup using the run record at
`/path/to/run-records`." The workflow documentation covers
[checkpoints and resumption](workflows/campaign.md#checkpoint-and-resume).

## What you receive

- A map of the relevant mathematics and dependencies, with findings tied to source.
- A plan for module organization, code updates, and verification; for refactoring
  requests, a reviewable patch and migration notes.
- For broad audits and cleanups, an assumption and reuse review for every theorem
  in scope, with any coverage gaps identified.
- Check results, evidence that changed statements preserve the original claims,
  and a record of unfinished work.
- Counts of reviewed theorems and verified improvements, such as assumptions
  removed and local proofs replaced by Mathlib results, with supporting records
  and available before-and-after measurements.

cLEAN preserves mathematical claims and pinned dependencies. It can change APIs
when that improves the library, updating affected code and documenting the
migration. Project compatibility requirements take precedence.

## Guide to the files

| Location | Purpose |
| --- | --- |
| [SKILL.md](SKILL.md) | Starting instructions and links to the workflows and review criteria |
| [audit](workflows/audit.md) | Review mathematics, assumptions, reuse, and dependencies |
| [planning](workflows/planning.md) | Plan changes and their verification |
| [repair](workflows/repair.md) and [verify](workflows/verify.md) | Apply changes and check the results |
| [structure](workflows/structure.md) | Organize modules and update imports and uses |
| [repository work](workflows/campaign.md) | Track review coverage, remaining work, and checkpoints |
| [duplication review](workflows/inclusive-duplication.md) | Review overlap and set up optional numerical comparisons |
| [report](workflows/report.md) | Explain results and link to supporting evidence |
| [rubrics](rubrics/_common.md) | Shared review criteria |
| [Mathlib naming conventions](references/mathlib-naming-conventions.md) | Upstream naming guide with source revision and license |
| [records](references/records.md) | Formats for findings, tasks, checks, and progress |

## Acknowledgments

cLEAN's mathematical review criteria are adapted from
[TauCetiReview](https://github.com/TauCetiProject/TauCetiReview/tree/main/rubrics).
Its workflows apply those criteria to auditing, planning, refactoring, migrating,
and verifying existing Lean repositories.

The bundled [Mathlib naming guide](references/mathlib-naming-conventions.md)
comes directly from [mathlib-landing](https://github.com/leanprover-community/mathlib-landing),
with its source revision and retrieval date recorded in the file and its
[upstream MIT notice](references/mathlib-naming-LICENSE) retained alongside it.

## License

[MIT](LICENSE).

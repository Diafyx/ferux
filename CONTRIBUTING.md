# Contributing to Ferux

Thank you for your interest in Ferux. This guide explains how changes are proposed, reviewed and merged.

Everyone taking part in Ferux is expected to follow the [code of conduct](CODE_OF_CONDUCT.md). To report a security vulnerability, follow the [security policy](SECURITY.md) instead of opening a public issue.

## Before you start

- Search the [existing issues](https://github.com/Diafyx/ferux/issues) first.
- Open an issue before starting anything larger than a small fix, so the approach can be agreed before you write code.
- Work on an issue once it has the `ready` label.

## Issues

Bug reports describe what happened, what you expected, how to reproduce it, the Ferux commit, the host OS and QEMU version, and any logs.

Every other issue uses these sections, in this order:

1. Problem
2. Motivation
3. Proposed solution
4. Scope
5. Acceptance criteria
6. Non-goals
7. Dependencies
8. Risk and rollback
9. Alternatives considered

## Workflow

1. Create a branch from `main` named `<type>/<issue>-<short-slug>`, for example `feat/7-serial-logging`. The type is one of `feat`, `fix`, `docs`, `test`, `ci`, `build`, `chore`, `perf` or `refactor`.
2. Keep the change to the scope of one issue, with its tests and documentation.
3. Run the checks locally before you push. The commands are listed in the README once the Rust workspace exists.
4. Open a pull request against `main`. Fill in every section of the pull request template, and link the issue with `Closes #<number>`.
5. A pull request is merged when CI passes, every review thread is resolved, and a maintainer approves the change. Pull requests are merged with squash merge, so the pull request title becomes the commit message on `main`.
6. To fix review comments, add new commits to the same branch. Do not force-push after review has started unless a maintainer asks for it.

## Commit messages

Ferux uses [Conventional Commits](https://www.conventionalcommits.org/en/v1.0.0/):

```
type(scope): summary in the imperative mood

Optional body that explains why the change is needed.

Signed-off-by: Your Name <you@example.com>
```

- The summary is at most 72 characters and has no issue number.
- The types are the same as for branch names.
- Mark a breaking change with `!` after the type and a `BREAKING CHANGE:` footer.

The pull request title follows the same format.

## Sign-off (DCO)

Every commit must be signed off. By signing off, you certify that you wrote the change or have the right to submit it under the project's license, as stated in the [Developer Certificate of Origin 1.1](https://developercertificate.org/).

Add the sign-off with `git commit -s`. It adds a `Signed-off-by:` line with the name and email from your Git configuration. Use your real name.

## Signed commits

Every commit on `main` must carry a verified signature. Sign your commits with GPG or SSH, and add the key to your GitHub account. See GitHub's guide on [commit signature verification](https://docs.github.com/en/authentication/managing-commit-signature-verification/about-commit-signature-verification).

## Rules for `unsafe` code

Ferux's safety promise depends on these rules:

- `unsafe` code is allowed only in the trusted core crate, `ferux-core`. Every other crate forbids it with `#![forbid(unsafe_code)]`.
- Every `unsafe` block has a `// SAFETY:` comment directly above it that states why the block is sound: which conditions it relies on, and why they hold.

  ```rust
  // SAFETY: 0x3F8 is the I/O port of the COM1 16550 UART, and the caller holds
  // the serial lock, so no other code accesses the port at the same time.
  unsafe { port.write(byte) };
  ```

- Every `unsafe fn` has a `# Safety` section in its documentation that lists what the caller must guarantee.
- Keep `unsafe` blocks as small as possible, and expose them through safe functions.
- A pull request that adds or changes `unsafe` code says so in its description and explains why safe code is not enough.

Once the Rust workspace exists, CI checks the first two rules with Clippy (`undocumented_unsafe_blocks` and `missing_safety_doc`) and reports how much `unsafe` code exists.

## Code style and tests

- Format with `rustfmt`, and keep Clippy free of warnings.
- Every change ships with tests at the right level: host tests for logic that does not need hardware, and kernel tests in QEMU for everything else.
- Tests must be deterministic and must not use the network.

## Documentation

Every pull request that adds or changes a feature updates the matching chapter of the documentation in `docs/`.

## Dependencies

A new dependency needs agreement on its issue first. Explain why it is needed, confirm that its license is compatible with Apache-2.0, and describe how well it is maintained.

Code copied from another project keeps its license notice and is credited in [NOTICE](NOTICE).

## License

Ferux is licensed under the [Apache License, Version 2.0](LICENSE). Unless you state otherwise, any contribution you submit is licensed under the same terms, as described in section 5 of the license.

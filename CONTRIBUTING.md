# Contributing to TaskForge

Thank you for your interest in contributing to TaskForge!

Before participating, please read our [Code of Conduct](./CODE_OF_CONDUCT.md). By contributing to this project, you agree to follow the standards described there.

## How to Contribute

There are several ways to contribute to TaskForge:

- **Report bugs** — Open an issue describing the problem, expected behavior, and steps to reproduce it.
- **Suggest features** — Open an issue explaining the proposed feature, its use case, and why it would benefit TaskForge.
- **Improve documentation** — Fix unclear documentation, examples, typos, or missing information.
- **Contribute code** — Fix bugs, improve existing functionality, or implement approved features through pull requests.
- **Review pull requests** — Help test changes and provide constructive feedback.

> **Security vulnerabilities:** Do not report security vulnerabilities through public issues. Please follow the instructions in our [Security Policy](./SECURITY.md).

## Development Setup

### Prerequisites

TaskForge is written in Rust. Before contributing, install:

- [Rust](https://www.rust-lang.org/tools/install)
- Cargo
- Git

The latest stable Rust toolchain is recommended.

Verify your installation:

```bash
rustc --version
cargo --version
git --version
```

### Clone the Repository

Fork the repository on GitHub, then clone your fork:

```bash
git clone https://github.com/<your-username>/TaskForge.git
cd TaskForge
```

Add the upstream repository:

```bash
git remote add upstream https://github.com/Zer0F8th/TaskForge.git
```

Verify your remotes:

```bash
git remote -v
```

## Branching Workflow

Always create your work from an up-to-date `main` branch.

```bash
git switch main
git fetch upstream
git rebase upstream/main
```

Create a focused branch for your change:

```bash
git switch -c feature/my-feature
```

Recommended branch prefixes include:

```text
feature/
bugfix/
docs/
refactor/
test/
chore/
```

Examples:

```text
feature/add-task-priorities
bugfix/fix-task-deletion
docs/update-installation
refactor/task-storage
```

Keep branch names short, descriptive, and lowercase with hyphens.

## Keeping a Linear Git History

TaskForge prefers a clean, linear commit history.

Before pushing or updating a pull request, synchronize your branch with `main` using rebase rather than creating a merge commit:

```bash
git fetch upstream
git rebase upstream/main
```

If conflicts occur:

```bash
git status
```

Resolve the conflicted files, stage them, and continue:

```bash
git add <resolved-files>
git rebase --continue
```

To cancel the rebase:

```bash
git rebase --abort
```

If you previously pushed the branch and then rebased it, update your remote branch with:

```bash
git push --force-with-lease
```

Use `--force-with-lease` instead of `--force` whenever possible.

## Building TaskForge

Build the project with:

```bash
cargo build
```

For a release build:

```bash
cargo build --release
```

Run the application with:

```bash
cargo run
```

## Code Quality

Before submitting a pull request, make sure your code is formatted, linted, and tested.

### Format

```bash
cargo fmt --all
```

Verify formatting without modifying files:

```bash
cargo fmt --all -- --check
```

### Lint

Run Clippy:

```bash
cargo clippy --all-targets --all-features -- -D warnings
```

New code should not introduce Clippy warnings.

### Test

Run the full test suite:

```bash
cargo test --all
```

A useful final check is:

```bash
cargo fmt --all -- --check
cargo clippy --all-targets --all-features -- -D warnings
cargo test --all
```

## Code Style

Follow standard Rust conventions and prefer clear, maintainable code over unnecessary abstraction.

General expectations:

- Follow idiomatic Rust practices.
- Use `rustfmt` for formatting.
- Address Clippy warnings where practical.
- Prefer descriptive function, variable, module, and type names.
- Keep functions focused on a single responsibility.
- Avoid unnecessary dependencies.
- Avoid unrelated refactoring in focused pull requests.
- Add comments when they explain *why* something is done, not when they merely restate the code.
- Add or update tests when behavior changes.

## Commit Convention

TaskForge uses [Conventional Commits](https://www.conventionalcommits.org/).

The general format is:

```text
<type>(optional-scope): <description>
```

Common commit types include:

```text
feat:     introduce a new feature
fix:      correct a bug
docs:     update documentation
refactor: change code without changing behavior
test:     add or update tests
perf:     improve performance
build:    modify the build system or dependencies
ci:       modify CI configuration
chore:    perform maintenance work
```

Examples:

```text
feat(tasks): add task priority support
fix(cli): prevent empty task creation
docs: add contribution guidelines
refactor(storage): simplify task serialization
test(tasks): add task deletion tests
chore(deps): update dependencies
```

Keep the subject concise and written in the imperative mood when practical.

For larger commits, include a body explaining what changed and why:

```text
feat(tasks): add task priority support

Add priority levels to task creation and storage.

This introduces low, medium, and high priority values and updates
task serialization so priorities persist between application runs.
```

## Pull Request Guidelines

Before opening a pull request:

1. Search existing issues and pull requests to avoid duplicate work.
2. Open an issue first for substantial features or architectural changes.
3. Create your branch from the latest `main`.
4. Keep the pull request focused on one feature, bug, or logical change.
5. Rebase your branch onto the latest `main`.
6. Run formatting, linting, and tests locally.
7. Review your own diff before requesting review.
8. Clearly describe what changed and why.

### Pull Request Checklist

Before submitting, confirm:

- [ ] The change is focused and does not contain unrelated modifications.
- [ ] The branch is rebased onto the latest `main`.
- [ ] Commit messages follow Conventional Commits.
- [ ] `cargo fmt --all -- --check` passes.
- [ ] `cargo clippy --all-targets --all-features -- -D warnings` passes.
- [ ] `cargo test --all` passes.
- [ ] Tests were added or updated when behavior changed.
- [ ] Documentation was updated when necessary.
- [ ] No secrets, credentials, API keys, or sensitive information were committed.

## Pull Request Reviews

Pull requests may receive requests for changes before they are merged.

Review feedback should be treated as collaboration rather than criticism. Contributors and maintainers should keep discussions technical, respectful, and focused on improving the project.

Maintainers may request that a pull request be:

- Rebased onto the latest `main`
- Split into smaller changes
- Expanded with tests
- Simplified
- Updated to follow project conventions
- Reworked when the implementation introduces unnecessary complexity

A pull request may be closed if it is abandoned, substantially outside the project's scope, duplicates existing work, or cannot reasonably be reviewed in its current form.

## AI-Assisted Contributions

AI-assisted contributions are welcome, but responsibility for the submitted code remains with the contributor.

AI tools can help write, review, explain, or test code, but they are not a substitute for understanding the change.

By submitting AI-assisted work, you are expected to:

1. **Understand the code you submit.** You should be able to explain how the implementation works and why the approach was chosen.
2. **Review generated output yourself.** Do not submit unreviewed generated code.
3. **Test the change locally.** Generated code must meet the same testing and quality standards as manually written code.
4. **Keep changes focused.** Avoid large generated refactors, unrelated formatting changes, or speculative rewrites.
5. **Verify dependencies and APIs.** Do not assume generated package names, functions, APIs, or security claims are correct.
6. **Avoid generated noise.** Do not add unnecessary comments, abstractions, documentation, or tests solely to make a contribution appear larger.
7. **Protect sensitive information.** Never provide secrets, credentials, private source code, or other restricted information to external AI services unless you are authorized to do so.

Maintainers may close contributions that appear to contain unreviewed, incorrect, fabricated, or unnecessarily broad AI-generated changes.

**AI is a development tool, not a substitute for engineering judgment.**

## Reporting Bugs

A useful bug report should include:

- A clear description of the issue
- Steps to reproduce it
- Expected behavior
- Actual behavior
- TaskForge version or commit
- Rust version
- Operating system
- Relevant logs or error messages

When including logs, remove passwords, tokens, API keys, personal data, and other sensitive information.

## Feature Requests

Feature requests should explain:

- The problem being solved
- The proposed behavior
- Why the feature belongs in TaskForge
- Possible alternatives
- Any compatibility or design considerations

For significant features, wait for maintainer feedback before investing substantial development time.

## Security

If you discover a security vulnerability, do not open a public issue.

Follow the reporting process described in [SECURITY.md](./SECURITY.md).

Public disclosure before maintainers have had a reasonable opportunity to investigate and remediate an issue may put users at risk.

## Documentation

Documentation changes are valuable contributions.

When changing behavior, consider whether you also need to update:

- `README.md`
- CLI help text
- Examples
- Configuration documentation
- Architecture or developer documentation
- Tests that serve as usage examples

Documentation should describe the current behavior of the project rather than intended future behavior.

## Questions

If you are unsure whether a proposed change fits TaskForge, open an issue before starting a large implementation.

Thank you for helping improve TaskForge.

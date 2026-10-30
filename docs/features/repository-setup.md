# Repository setup

Use the standard's [adoption guide](https://github.com/simpsonm09-org/simpsonm09-repo-standard/blob/main/docs/adoption.md)
when starting a repository from this template. Keep shared workflow references
pinned to one standard commit. Copy shared scripts from that commit and check
their local changes before updating them.

## Local settings

The optional local file is `settings/.env`. Its committed sibling is
`settings/.env.example`. Keep `.worktreeinclude` at the repository root and list
`settings/.env` there. The standard accepts a nested local path; it does not look
for a `.worktreeinclude` inside `settings/`. Both the local file and any retired
`.envrc` stay ignored. Never commit or delete a real local file during adoption.

The template does not load secrets into a shell on directory entry. For a command
that needs a secret, use dev-setup's `with-secrets <tool>` human wrapper. Use
`with-vault --role agent <tool>` for the agent broker path. The application must
read its configuration from the environment; an example file alone loads nothing.

## Validation

Run `just lint`, `just complexity`, `just test`, and `just coverage`. `just verify`
runs lint, complexity, and tests. Coverage writes `coverage/lcov.info`; the shared
CI workflow runs the pinned standard's patch gate at 80 percent of changed lines.
The patch script belongs to the standard checkout, not this template's scripts.

Run `just check-standard <repository-path>` from the pinned standard checkout.
The [validation guide](https://github.com/simpsonm09-org/simpsonm09-repo-standard/blob/main/docs/validation.md)
lists all groups, including `env` and `subprocess`. Every Node child-process call
must pass a literal `windowsHide: true` in its options, including calls in copied
shared scripts. The template's prune script follows this rule.

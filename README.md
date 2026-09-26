# Outrider real-CI fixture

This directory is the canonical seed for Outrider's opt-in live GitHub Actions
fixture. It deliberately contains one required check, `fixture-ci / required-ci`.

- `fixture-control.txt` set to `pass` makes the check succeed.
- Changing it to `fail` makes the check fail with a deterministic, searchable log
  line: `Intentional real-CI fixture failure.`

`New-RealCiFixture.ps1` copies this seed into a dedicated **private** GitHub
repository, protects its `main` branch with the check, and creates an open PR
whose head intentionally fails. The provisioner does not alter the fixture PR
once it has created it; follow-up live testing owns log download, rerun, head
movement, and final merge-policy observations.

GitHub Free does not support branch protection on private repositories. Keep the
default private mode wherever protection is available. An operator who explicitly
accepts a public fixture containing only these non-secret canonical files can pass
`-AllowPublicFixture`; only after GitHub rejects private protection does the
provisioner change that dedicated fixture repository to public and retry. Its JSON
handoff reports `protectionMode: "public-fallback"` so evidence cannot misstate
that the fixture remained private.

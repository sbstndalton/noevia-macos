# Agent instructions: noevia-macos

This repo holds the native macOS client for Noevia (currently only the `NoeviaKit` Swift
package). It was split out of `clients/macos/` in
[sbstndalton/noevia](https://github.com/sbstndalton/noevia). Before working here, read the
shared brief: [docs/agent-brief.md in sbstndalton/noevia](https://github.com/sbstndalton/noevia/blob/main/docs/agent-brief.md).
Issues are tracked in [sbstndalton/noevia](https://github.com/sbstndalton/noevia/issues), not here.

## Invariants

Do not rename Cowork-prefixed identifiers (env vars, images, cookies). Preserve tenant isolation and all three write-approval actions (Allow once / Decline / Allow for this chat). Synthetic fixtures only — never real Diary data. Never flip feature flags. No model/inference runs.

## Build and test

```sh
cd NoeviaKit
swift build
swift test            # with Xcode (as on CI)
sh scripts/test-clt.sh  # on a Mac with only the Command Line Tools
```

CI (`.github/workflows/ci.yml`, `macos-15`) is authoritative.

## Fixtures

`NoeviaKit/Tests/NoeviaKitTests/Fixtures` is vendored. Regenerate only from a noevia checkout:
`NOEVIA_REPO=/path/to/noevia node NoeviaKit/scripts/generate-fixtures.cjs`. Never hand-edit a
generated fixture to make a test pass, and never put real account or Diary data in one.

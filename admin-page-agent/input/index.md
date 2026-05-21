# Input Index

This is the required entrypoint for admin-page-agent project input.

## Files

project: ./project.md
stack: ./stack.md
design: ./design.md
api: ./api.md
auth: ./auth.md
resourceManifest: ./resource-manifest.md
resourceTemplate: ./resource.template.md
resourceIndex: ./resource-index.json

defaults:
crud: ./defaults/crud.md
mock: ./defaults/mock.md

resourcesDir: ./resources

## Rule

- Read only the files required by the active workflow.
- Use `resources/*.md` as the source of truth after resource materialization.
- Use `resource-index.json` as a generated cache only; never treat it as source of truth.
- Use `resource-manifest.md` only for first materialization or explicitly requested missing-resource materialization.
- Once a resource file exists, skip it during materialization unless the user asks for a diff-based update.
- If this file does not exist, stop and create or request the split input files listed above.

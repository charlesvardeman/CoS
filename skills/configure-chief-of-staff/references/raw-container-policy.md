# Raw Container Policy

Read this reference when configuration binds a source or CoS trajectory stream to raw evidence storage.

`raw` is an authority and lifecycle class: it identifies source evidence that has not been promoted into asserted semantic knowledge. It does not imply one directory, format, privacy level, Git rule, search surface, or retention period.

## Contract

A host-native representation is acceptable if it preserves this semantic shape:

```yaml
schema: raw-container-policy/v1
container_id: stable deployment-local identifier
purpose: source evidence represented by this container
authority: evidence
origin: source channel or adapter
content_types: []
location:
  kind: managed-directory | mounted-directory | external-store
  binding: private host-specific locator
persistence:
  git: tracked | ignored | manifest-only | not-applicable
  backup: configured policy or explicitly deferred
update_semantics: append-only | source-managed-mirror | replace-from-source
discovery:
  search: direct | mediated | excluded
  projection: none | metadata-only | configured
retention: configured duration or source policy
privacy:
  classification: deployment policy
  disclosure: ordinary | contextual | confirm-before-surface
promotion:
  method: cite-and-retain
  target_roles: []
```

The fields keep independent decisions independent:

- `authority` distinguishes evidence from asserted vault knowledge.
- `location` and `persistence` describe where bytes live, how they are backed up, and whether Git contains the bytes, a manifest, or neither.
- `update_semantics` distinguishes append-only evidence from a source-managed mirror.
- `discovery` states whether ordinary retrieval searches content directly, through a mediator, or not at all.
- `privacy.disclosure` guides answer scope; it does not claim that searchable content is inaccessible.
- `promotion` states how a reviewed derived record cites and retains its evidence.

Do not treat directory topology or Git exclusion as access control. When confidentiality needs enforcement, require a harness, operating-system, or storage-provider boundary.

## Different Containers, Different Policies

- A Readwise Markdown mirror can be raw, source-managed, directly searchable, and Git-tracked.
- A paper corpus can keep bytes on a mount while Git tracks manifests, locators, and digests.
- A CoS trajectory container can be append-only, content-minimized, and Git-ignored while using a separate backup policy.

Configure only the containers required by the approved workflows. Creating a policy does not authorize ingesting source content, capturing broad task history, mounting storage, or changing Git settings.

# AI Inference and Deployments

The common inference-platform vocabulary -- the deployments and endpoints a model is served from, and the GPU instances behind them -- distilled from the APIs that already exist. Part of [Schema Commons](https://github.com/api-commons/schema-commons),
published by the [API Commons](https://apicommons.org).

Built from the providers tagged Inference, AI Infrastructure, GPU Cloud, Model Serving, GPU, AI Compute, Foundation Models in [APIs.io](https://apis.io) that
publish their own OpenAPI. Only harvested contracts count -- nothing API Evangelist
generated. Every number below is a count of providers.

## What the market already agrees on

<!-- commons:summary -->
| Concept | Expose it | Readable schema | Core properties (share) | Collection named |
| --- | ---: | ---: | --- | --- |
| deployment | 23 | 20 | status 75%, created_at 70%, id 60%, name 60% | deployments 15, endpoints 7, endpoint 3, deployment 1 |
| gpu_instance | 27 | 24 | status 88%, id 79%, created_at 67%, name 67%, region 62% | instances 18, gpus 6, pods 4, machines 4 |

Cohort: 172 providers with harvested OpenAPI, 41 crosswalks. Of the providers exposing a deployment: 78% create, 83% list, 70% fetch, 39% update, 52% delete. Generated 2026-11-11 by build.py.
<!-- /commons:summary -->

Shares are of the providers with a readable resource schema for that concept. The
extended tier and the long tail of every concept are in [profile.yml](profile.yml).

## What the measurement shows

- Deployments agree on status, created_at, id and name; the model served and the instance type each reach 45%. The endpoint URL reaches 30%, because many platforms route by model name instead.
- GPU instances agree on status, id, created_at, name and region; gpu_type reaches 46%. A pod, a machine and an instance are the same rentable unit.

## Artifacts

- [openapi.yml](openapi.yml) -- OpenAPI 3.1 of the shared operations. No one serves it; it
  is the shape to map to. Lints clean against the
  [naming ruleset](https://github.com/api-commons/schema-commons/blob/main/ruleset/schema-commons-naming.yaml).
- [schema/](schema) -- JSON Schema 2020-12 per concept; each property carries
  `x-commons-tier`, `x-commons-share`, `x-commons-providers` and the spellings seen.
- [crosswalk/](crosswalk) -- one per provider, common name -> their name, with the harvested
  spec and operations each mapping was read from.
- [adopters.yml](adopters.yml) -- who exposes which concept, linked to their APIs.io page.
- [concepts.yml](concepts.yml) -- the only hand-written input: concepts, path segments and
  their qualifiers, aliases, reviewed exclusions, merged duplicates, and the decisions below.
- [census/](census) -- the cohort and the raw census the profile is built from.

## Decisions

These are calls, not measurements, recorded so they can be revisited as the method matures.

- gpu_instance is a role name, because instance is used in cloud-infrastructure, where it is the general virtual machine.
- Inference calls themselves (completions, embeddings) are left to api-commons/models; this context covers the infrastructure they run on.

## Rebuild

```bash
../schema-commons/scripts/run.sh .
```

## License

Artifacts CC BY-NC-SA 4.0 ([LICENSE](LICENSE)); code Apache 2.0 ([LICENSE-CODE](LICENSE-CODE)).

# V21 CLEAN ARCHITECTURE

V21 is an architectural cleanup of V20. Functional modules were preserved; version numbers were removed from active package names.

## Stable layout
- NOVA: core, domains, gpu_worker, industrial, infra, persistence, deep_engines, execution
- NEXUS: core, domains, industrial, infra, persistence, deep_engines, orchestration
- TOKENIA: core, domains, industrial, infra, persistence, deep_engines, economy_engine
- TRINITY: protocol, routing/workflow modules, state_machine

Historical version numbers now belong in release manifests/changelog, not active Python package names.

## Rule from V21 onward
New releases evolve these stable modules instead of creating `v22_*`, `v23_*`, etc. folders.

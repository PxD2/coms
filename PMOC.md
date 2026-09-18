# PMOC

Parallel Memory Optimized Compute. The layout coms schedules against.

PMOC is not a file format for its own sake. It is how an object is striped across lanes so the scheduler can pin compute next to data:

- lanes follow the fabric (chiplet, HBM stack, HBF package, NVMe)
- a cap (`own` / `read` / `rent`) travels with the stripe
- lineage is appended, never rewritten quietly

`weights.pmoc` on HBF with an HBM cache is the default inference placement. `kv.session` dies when the cap expires, not when a process exits — unless you say so.

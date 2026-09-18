# SPEC — what does not exist today

Today's stacks split one fact into dialects:

| Dialect | Where it lives | What the OS knows |
|---|---|---|
| POSIX file | NVMe / NFS | path, bytes |
| CUDA / HIP heap | HBM / VRAM | device pointer |
| object store | S3 / Drive | key, ACL |
| model weights | whoever copied them | nothing |
| personal world | Photos + chat + docs | nothing unified |

coms names **one object**:

```
object = { id, kind, tier, cap, lineage, pmoc }
tier   = sram | hbm | dram | hbf | nvme | cxl
cap    = own | read | rent
kind   = blob | tensor | kv | note | cap
```

## Five kernel gaps

1. **Unified address space** across SRAM, HBM, DRAM, CXL, HBF (stacked NAND as HBM-class bulk), NVMe. Not mount points. Objects migrate; pointers do not dangle.
2. **Lineage as a kernel object.** Who ran, on which weights, from whose world. Training and inference leave a trace you can revoke.
3. **Tensor syscall.** Not CUDA. Not OpenCL's grave. Vendor implements the op; the OS owns the object and the cap.
4. **Capability sync, not file sync.** Revoke `rent.infer` and every replica stops. Drive/iCloud cannot do this.
5. **Compute-follows-data scheduler.** Place the kernel next to PMOC lanes. Stop copying 400 GB of weights into VRAM because the OS only understands files.

## What we are not building

- A 256-bit ISA as the desktop.
- Quantum as the OS.
- A Windows license crack.
- Another distro with a new wallpaper.

## Placement

| Mode | Machine | Role |
|---|---|---|
| stay | ia32 + PAE | the PCs they surrendered |
| future | x86_64 / Arm | same ABI, new silicon |
| coms | PMOC plane | data is the OS |

HBF (high-bandwidth flash) is bulk. HBM is the hot cache. Limited HBM is a policy, not a product lock.

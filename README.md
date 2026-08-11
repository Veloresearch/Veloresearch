# ⚡ Velocity — Native AI Execution Stack

### Existing models. No retraining. Verified local execution.

**Velocity is not another AI chat app.**

Velocity builds **Motify** — a native execution stack for local AI models, based on sealed `.mfy` artifacts and **MTA**, the **Motify Transit Architecture**.

The chat is only the interface.  
The execution stack underneath is the product.

```text
existing model
→ MTA compiler
→ sealed .mfy artifact
→ Velocity runtime
→ CUDA execution path
→ MTA Exact / MTA Adapt
→ local AI execution
```

No Python.  
No PyTorch.  
No server.  
No cloud.  
One local runtime.

---

## What Velocity Builds

Velocity is building the execution layer underneath local AI models.

Instead of shipping another wrapper around an existing model, Velocity introduces a full local runtime path:

- sealed `.mfy` model artifacts
- native Velocity runtime
- Motify execution layer
- MTA Exact verification
- MTA Adapt execution
- local CUDA-first performance path
- inspectable execution maps
- reproducible local benchmarks

The goal is simple:

> Take existing model families, compile them into portable `.mfy` artifacts, verify them against a reference path, and run them through a new execution layer without retraining.

---

## Public Proof Build

The first public proof is available here:

| Resource | Link |
|---|---|
| **Proof repository** | [velocity-mta-proof](https://github.com/Veloresearch/velocity-mta-proof) |
| **Windows proof build** | [Download VeloSetup.exe](https://github.com/Veloresearch/velocity-mta-proof/releases/latest) |
| **Model artifact** | [velocity-research/qwen3.5-4b-adapt-b32 on Hugging Face]([https://huggingface.co/velocity-research/qwen3.5-4b-adapt-b32]) |

The installer can download the `.mfy` artifact automatically from Hugging Face.

If skipped during setup, `velocity.exe` can download and verify the model on first launch.

The public proof build includes:

- local terminal chat
- `.mfy` artifact loading
- automatic Hugging Face model download
- SHA-256 verification
- MTA Exact mode
- MTA Adapt mode
- CUDA execution path
- CPU compatibility fallback
- benchmark suite
- execution map
- local reproducibility path

---

## Tested Public Configuration

The current public proof was deliberately tested on consumer laptop hardware.

```text
GPU       NVIDIA RTX 3060 Laptop GPU
VRAM      6 GB
Backend   CUDA, GPU-resident Q4 path
Artifact  qwen3.5-4b-adapt-b32.mfy
OS        Windows 11 x64
```

Reference public proof numbers:

```text
Attention  up to ~20x lower attention-step cost at 32k context
Decode     ~64 tok/s on the tested machine
Quality    ppl 11.296 Adapt vs 11.312 Exact on the tested WikiText-2 sample
Backend    CUDA preferred
```

These are local benchmark results from one tested configuration.

They are not presented as a universal end-to-end model speedup claim.

The claim is narrower and verifiable:

> MTA Adapt reduces attention-path cost at long context while preserving decode throughput and matching Exact quality on the tested benchmark.

---

## MTA — Motify Transit Architecture

**MTA** is the execution architecture inside Motify.

It defines how `.mfy` artifacts are loaded, verified, executed, inspected, and benchmarked.

Velocity currently exposes two working public MTA paths, with a third path in development:

| Path | Status | Role |
|---|---|---|
| **MTA Exact** | working | baseline / parity / verification path |
| **MTA Adapt** | working | no-retraining execution path for existing model families |
| **MTA Native** | future | models designed directly for Velocity's execution stack |

> **Exact proves trust.**  
> **Adapt ships existing models.**  
> **Native breaks the ceiling.**

---

## MTA Exact

**MTA Exact** is the verification path.

It is designed for baseline comparison, auditability, and parity checks.

Use MTA Exact to answer one question:

> Does this `.mfy` artifact preserve expected baseline behavior?

Exact gives users and developers a reference path before evaluating any adapted or optimized execution mode.

---

## MTA Adapt

**MTA Adapt** is the current product path.

It runs existing model families through the Motify execution stack as sealed `.mfy` artifacts **without retraining**.

Adapt is not a new foundation model.

Adapt is not fine-tuning.

Adapt is not prompt engineering.

Adapt is a different execution path for an existing artifact.

Current public proof:

```text
Same artifact.
Same benchmark.
Same machine.

Exact = verification path
Adapt = no-retraining execution path
```

The goal is not to claim that Adapt improves quality everywhere.

The goal is to show that an existing model artifact can run through a different runtime path without quality collapse.

---

## `.mfy` Artifacts

A `.mfy` file is a sealed Motify model artifact.

It packages:

- model payload
- tokenizer metadata
- runtime configuration
- MTA execution metadata
- artifact identity
- verification information

Current public proof artifact:

```text
qwen3.5-4b-adapt-b32.mfy
```

Hugging Face stores `.mfy` artifacts as regular binary files.

Velocity is the runtime that knows how to open, verify, and execute them.

```text
model → .mfy → Velocity Runtime → MTA execution → local AI
```

---

## Motify Runtime

Motify is the runtime layer behind Velocity.

It manages:

- artifact loading
- automatic model download
- SHA-256 verification
- tokenizer setup
- chat template setup
- runtime session state
- CUDA backend execution
- CPU compatibility fallback
- MTA path selection
- Exact / Adapt execution
- benchmark reporting
- execution inspection

The goal is to make local model execution:

- inspectable
- reproducible
- benchmarkable
- portable
- locally verifiable

---

## Execution Map

Velocity exposes the execution surface instead of hiding it.

The runtime can show:

- active MTA path
- selected backend
- context usage
- layer activity
- attention path
- state path
- active KV ratio
- FFN path
- benchmark metrics

This matters because the goal is not only to generate text.

The goal is to control execution at the runtime layer and let users inspect what is happening.

---

## Execution Glossary

| Term | Meaning |
|---|---|
| **SSM** | State Space Model — a path that can maintain compact working state instead of relying on a growing full attention window in every layer. |
| **GQA** | Grouped Query Attention — attention path used by modern model architectures, including Qwen-family models. |
| **FFN** | Feed-Forward Network — dense compute block inside each layer, usually involving gate / up / down projections. |
| **KV** | Key / Value cache — attention memory from previous tokens; grows with context in classic attention paths. |
| **O(1) state** | bounded working state whose size does not grow linearly with conversation length. |

---

## Benchmarks

Velocity believes in runnable proof, not screenshots.

The public proof build includes a local benchmark suite.

Inside Velocity:

```text
/bench
/bench ppl
/bench speed
/bench full
```

The benchmark suite can render charts and write raw results on the user's machine.

Reference benchmark cards from the public proof repo:

| Chart | Link |
|---|---|
| Full benchmark overview | [00_full_benchmark.png](https://github.com/Veloresearch/velocity-mta-proof/blob/main/benchmarks/00_full_benchmark.png) |
| Context cost | [01_context_cost.png](https://github.com/Veloresearch/velocity-mta-proof/blob/main/benchmarks/01_context_cost.png) |
| Context speedup | [02_speedup.png](https://github.com/Veloresearch/velocity-mta-proof/blob/main/benchmarks/02_speedup.png) |
| Kernel bandwidth | [03_kernel_bandwidth.png](https://github.com/Veloresearch/velocity-mta-proof/blob/main/benchmarks/03_kernel_bandwidth.png) |
| Decode throughput | [04_decode_throughput.png](https://github.com/Veloresearch/velocity-mta-proof/blob/main/benchmarks/04_decode_throughput.png) |
| Perplexity | [05_perplexity.png](https://github.com/Veloresearch/velocity-mta-proof/blob/main/benchmarks/05_perplexity.png) |

Raw public benchmark summary:

[benchmarks/summary.txt](https://github.com/Veloresearch/velocity-mta-proof/blob/main/benchmarks/summary.txt)

---

## Current Public Proof Status

```text
MTA Exact        working
MTA Adapt        working
.mfy artifact    working
Qwen 4B artifact working
CUDA backend     working — preferred path
CPU x86 backend  working — compatibility fallback
HF auto-download working — setup-time and first-launch
Local chat       working
Benchmark suite  working
Execution map    working
```

In internal validation:

```text
Gemma-family artifact
MTA Native research path
```

---

## Quick Start

Install the public proof build:

```text
https://github.com/Veloresearch/velocity-mta-proof/releases/latest
```

Run Velocity:

```powershell
velocity.exe
```

Manual model download, if preferred:

```bash
hf download velocity-research/qwen3.5-4b-adapt-b32 qwen3.5-4b-adapt-b32.mfy --local-dir ./models
```

Run a specific artifact:

```powershell
velocity.exe --model ./models/qwen3.5-4b-adapt-b32.mfy
```

Verify the proof:

```text
/mode exact
/bench ppl
/mode adapt
/bench ppl
/map on
/stats
```

---

## Why This Matters

Velocity does not compete with Qwen, Gemma, Llama, or other model families.

Velocity builds the execution layer underneath them.

If existing model families can be compiled into `.mfy` artifacts, verified through MTA Exact, and executed through MTA Adapt without retraining, then the value is not in one model.

The value is in the artifact standard and runtime.

```text
existing models
→ portable artifacts
→ verifiable runtime
→ local execution
→ inspectable benchmarks
```

And the first public proof runs on a 6 GB consumer laptop GPU.

---

## What Velocity Is Not

Velocity is not:

- another chat UI
- a prompt wrapper
- a hosted API skin
- a fine-tuning product
- a cloud-only demo
- a claim without a runnable local proof

Velocity is a native local AI execution stack.

---

## Privacy

Inference is fully local.

The public proof build only needs network access for the one-time model download from Hugging Face.

Conversations stay on your machine.

---

## Roadmap

Current public proof:

```text
Exact  → verification and trust
Adapt  → existing models through Motify
CUDA   → preferred current execution path
```

Next:

```text
more model families
more `.mfy` artifacts
expanded benchmark suite
developer-facing artifact tools
MTA Native research path
```

MTA Native is the future path for models designed directly for Velocity's execution stack.

---

## License

Velocity, Motify, MTA, the `.mfy` artifact format, runtime technology, compiler technology, execution architecture, and related tooling are proprietary Velocity technologies unless explicitly stated otherwise.

Model artifacts may follow the license of their upstream base models.

Public proof repositories may contain packaged binaries and model artifacts, but they do not grant permission to copy, modify, redistribute, reverse engineer, or reuse Velocity proprietary technology unless a separate license explicitly allows it.

© 2026 Velocity / Velo Research. All rights reserved.

---

## Links

- Website: [veloresearch.com](https://veloresearch.com/)
- Contact: contact@veloresearch.com
- Proof repo: [github.com/Veloresearch/velocity-mta-proof](https://github.com/Veloresearch/velocity-mta-proof)
- Artifact: [veloresearch/qwen3.5-4b-adapt-b32](https://huggingface.co/veloresearch/qwen3.5-4b-adapt-b32)
- Release: [VeloSetup.exe](https://github.com/Veloresearch/velocity-mta-proof/releases/latest)

---

## Don't trust screenshots.

```text
Download it.
Run it.
Verify it.
Break it.
```

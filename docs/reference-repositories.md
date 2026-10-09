# Reference repositories for learning LLM architectures

Research date and cutoff: **2026-10-09**. Companion: [implementation roadmap](../ROADMAP.md).

## Method and limits

This comparison uses public upstream READMEs, GitHub API file inventories and metadata, and selected implementation/test files downloaded at the revisions recorded below. It does **not** certify entire repositories: no upstream training runs or test suites were executed. Educational value, clarity, and fidelity judgments are assessments of the inspected material. A README support claim, an existing file, a passing test, and a reproduced result are different levels of evidence.

Maintenance dates below are GitHub `pushed_at` observations, not a guarantee of active development or the date of a model implementation. All repositories in the metadata table reported `archived=false`; explicit deprecation notices override that weak signal. Stars were excluded from ranking. Model weights and datasets can have different licenses from repository code.

## What to read, and what to borrow

| Reference | Educational value / code clarity | Coverage and fidelity evidence | Training and hardware | Tests / maintenance / code license | Lesson for this repo |
|---|---|---|---|---|---|
| [Raschka: LLMs-from-scratch](https://github.com/rasbt/LLMs-from-scratch) | First choice for a guided GPT learning sequence; explanations and notebooks accompany code | Recent file inventory includes Qwen3.5 and Gemma4 lessons; sampled tests compare tiny models with Transformers | Small educational training examples, later checkpoint loading and fine-tuning; CPU for small exercises, GPU for useful larger runs | Chapter and component tests; recently pushed; [license](https://github.com/rasbt/LLMs-from-scratch/blob/main/LICENSE.txt) is Apache-derived with exclusions for books/images, not plain MIT | Adopt concept → code → experiment progression; keep notebook lessons backed by importable modules |
| [nanoGPT](https://github.com/karpathy/nanoGPT) | Compact GPT model and training loop; excellent baseline to read | GPT-focused rather than broad architecture coverage; checkpoint conversion provides a practical comparison target | Tiny character runs can use CPU; published GPT-2 reproduction uses substantial multi-GPU compute | No dedicated test directory in sampled tree; README explicitly deprecated in favor of nanochat; MIT | Learn the minimal training loop; do not make it the maintained dependency for the whole curriculum |
| [nanochat](https://github.com/karpathy/nanochat) | Clear end-to-end pipeline, though current model includes choices beyond textbook GPT-2 | Selected `nanochat/gpt.py` and generation tests inspected; limited family breadth | Tokenization, pretraining, post-training, evaluation, inference; flagship speedruns use a multi-GPU node | Tests for engine, attention fallback, optimizers, tokenization; recent push; MIT | Use as capstone inspiration after building a simple decoder; reproduce small workflows before published speedruns |
| [llm.c](https://github.com/karpathy/llm.c) | Strong systems education after PyTorch proficiency | C/CUDA GPT training with a Python reference; selected C test checks numerical behavior | CPU reference and GPU training; optimized CUDA requires compatible NVIDIA environment | Explicit GPT tests; last observed push in 2025; MIT | Preserve a slow oracle when adding kernels; make C/CUDA an optional systems track |
| [LitGPT](https://github.com/Lightning-AI/litgpt) | Readable direct PyTorch definitions, but a broad shared model file is harder for first lessons | Selected model file contains GQA, MLA, dense and MoE blocks; sampled tests compare against upstream models | Pretraining, fine-tuning, conversion, deployment recipes; memory depends on model, precision, and method | Extensive model/conversion/recipe tests; recent push; Apache-2.0 | Best engineering reference for config validation, checkpoint conversion, and numerical parity |
| [Transformers](https://github.com/huggingface/transformers) | Useful after the concept is understood; compatibility and optimization obscure first-principles reading | Broad model-definition coverage; use specific `modeling_*.py`, configs, and model tests rather than an `AutoModel` call | Inference and training APIs; tiny random configurations can run on CPU; actual checkpoints vary widely | Large model-specific test inventory; current push; Apache-2.0 | Primary interoperability oracle; pin a revision and compare small configurations before real checkpoints |
| [torchtune](https://github.com/meta-pytorch/torchtune) | Useful readable model builders and post-training recipes | Model/recipe inventory and upstream README inspected; no end-to-end validation here | Single-device and distributed post-training; larger published recipes require GPU memory optimizations | Unit and recipe tests; README says development wound down in 2025, despite later pushes; BSD-3-Clause | Read the modular recipes and loss masking; avoid choosing it as the project's active foundation |
| [OpenArch](https://github.com/anuj0456/OpenArch) | Easy side-by-side file layout | README promises usable forward passes, but sampled Llama 3 code has concrete runtime/shape problems; fidelity cannot be presumed | Primarily architecture files; no verified common pretraining pipeline; use reduced configs when experimenting | Smoke, causality, batch-independence, backward tests exist, but some setup failures are skipped; recent push; MIT | Adopt explicit architecture notes and compact files, but independently establish correctness |
| [LLM-quest](https://github.com/casinca/LLM-quest) | Detailed derivations and transitions between model families | Selected MLA and Qwen3-Next files inspected; recurrent gated delta update written explicitly | Training/generation scripts, alignment and multimodal experiments; hardware varies by exercise | No conventional top-level test suite in inspected inventory; scripts with test names are not equivalent to CI coverage; April 2026 push; Apache-2.0 | Borrow component explanations and migration exercises; add a consistent numerical test contract |
| [Annotated Transformer](https://nlp.seas.harvard.edu/annotated-transformer/) / [source](https://github.com/harvardnlp/annotated-transformer) | Excellent walkthrough of encoder-decoder attention | Educational implementation linked to the original Transformer | Small copy/translation demonstrations; full translation is a larger exercise | Notebook-oriented evidence; source license is MIT; maintenance not measured in the API sample | Make cross-attention, masking, and target shifting explicit; do not omit encoder-decoder learning |
| [Mamba](https://github.com/state-spaces/mamba) | Official reference, mathematical prerequisite heavier than GPT | Selected `ssd_minimal.py` supplies a compact SSD algorithm and correctness comparison; Mamba-3 module/tests present | Optimized training/inference depends on accelerator and kernel support; a separate slow PyTorch oracle can be CPU-friendly | Scan, state-update, SSD and Mamba-3 test inventory; July 2026 push; Apache-2.0 | Learn recurrence before fused scan; compare full sequence, chunks, and single-step state |
| [Flash Linear Attention](https://github.com/fla-org/flash-linear-attention) | Naive operators are readable; kernel code is advanced | Selected gated delta file has both recurrent and chunk reference implementations; broad linear/hybrid mechanisms | Kernel backends and accelerator requirements vary; tiny naive operators make affordable exercises | Extensive operation/model tests; current push; MIT | Use recurrent/chunk equivalence as the acceptance criterion for linear attention |
| [RWKV-LM](https://github.com/BlinkDL/RWKV-LM) | Compact RWKV-7 NumPy reference is a good recurrence lesson | Selected `RWKV-v7/rwkv_v7_numpy.py` makes token/state updates visible | Reference inference and separate training implementations; full training uses specialized GPU code | No comprehensive test assessment here; September 2026 push; Apache-2.0 | Add a distinct recurrent family, with state-reset and token-versus-sequence tests |

**Recommended reading sequence:** Raschka + nanoGPT for the first decoder; Annotated Transformer for encoder-decoder; LitGPT + Transformers for parity; LLM-quest for architectural transitions; official Mamba/FLA/RWKV code for recurrence; nanochat and llm.c for capstones. This ranking reflects learning fit, not repository size.

## Source-level evidence that changes the recommendation

### OpenArch: coverage labels require verification

At revision `2b0d1a97f73f13ca3565036e6ce041a32c16a42e`, the [Llama 3 file](https://github.com/anuj0456/OpenArch/blob/2b0d1a97f73f13ca3565036e6ce041a32c16a42e/text/llama3-8B/model.py#L89) passes `bias=False` to `Tensor.view`, which is not a valid argument. Its K/V reshapes also use the query head count despite projecting fewer KV heads. These are static findings, not measured test failures. The [test fixture](https://github.com/anuj0456/OpenArch/blob/2b0d1a97f73f13ca3565036e6ce041a32c16a42e/tests/test_models.py#L36) skips import/construction failures. Consequently, a green partial run cannot by itself establish every listed architecture works. Read it for layout inspiration, not as an unquestioned oracle.

### Raschka and LitGPT: follow their numerical comparison approach

The sampled [Qwen3.5 tests](https://github.com/rasbt/LLMs-from-scratch/blob/cdbd33e6d57a71e20ea31434841095fac50cecd8/ch05/16_qwen3.5/tests/test_qwen3_5_nb.py) and [Gemma4 tests](https://github.com/rasbt/LLMs-from-scratch/blob/cdbd33e6d57a71e20ea31434841095fac50cecd8/ch05/17_gemma4/tests/test_gemma4_nb.py) include tiny-config comparisons against Transformers. [LitGPT model tests](https://github.com/Lightning-AI/litgpt/blob/18c931c15c2398621d35371a12d2b1785e855bb6/tests/test_model.py) compare several families against reference implementations. This is stronger evidence than shape assertions, although this research did not execute those tests.

### Mamba and FLA: slow references make efficient algorithms teachable

Read [minimal SSD](https://github.com/state-spaces/mamba/blob/e9594ce1c732d97440f0332fdc43170a2294dbfa/mamba_ssm/modules/ssd_minimal.py) before optimized kernels, and [naive gated delta rules](https://github.com/fla-org/flash-linear-attention/blob/855e502613d47d8cc139153f0d87ecae5831ac3c/fla/ops/gated_delta_rule/naive.py) before chunk kernels. Build the slow oracle yourself and measure numerical agreement before performance.

## Additional references supplied by the user

| Resource | What was verified | How to use it |
|---|---|---|
| [LLM Architecture Gallery](https://sebastianraschka.com/llm-architecture-gallery/) | Discovery resource referenced by educational implementations; not an executable test oracle | Identify candidate differences, then verify against the model author's paper/config/code |
| [YichenZW/llm-arch-table](https://github.com/YichenZW/llm-arch-table) | Four files in the sampled tree, March 2026 push, no license identified in API metadata | Use as a discovery/comparison aid; do not treat it as a training implementation or copy content without checking terms |
| [Datawhale Chinese learning repo](https://github.com/datawhalechina/llms-from-scratch-cn) | Substantial chapter-code inventory and tests; September 2026 push; API license classification ambiguous, but inspected [LICENSE.txt](https://github.com/datawhalechina/llms-from-scratch-cn/blob/0c6bdb805bfc7b5bd5f23b641daf81d126e16c25/LICENSE.txt) uses MIT-style terms for software | Useful alternative explanations for Chinese readers; the supplied claims of specific GLM/RWKV coverage were not independently established here |

The supplied recommendation correctly points toward educational implementations, but this audit does not endorse every claimed family or star count. Raschka's Qwen3.5/Gemma4 directories were verified; OpenArch's usable-forward claim is weakened by code findings. The two Grok references are treated as hypotheses, not authoritative architecture specifications.

## Reproducible research snapshot

These revisions came from the public [GitHub repository API](https://docs.github.com/en/rest/repos/repos#get-a-repository) and recursive Git trees. Use each revision for future source comparisons; record any new revision when updating this document.

| Repository | Inspected revision | Observed last push (UTC date) |
|---|---|---|
| karpathy/nanoGPT | `3adf61e154c3fe3fca428ad6bc3818b27a3b8291` | 2025-11-12 |
| karpathy/nanochat | `92d63d4e8bb4df75c3b71618f31ddde2378b2bcd` | 2026-09-07 |
| karpathy/llm.c | `f1e2ace651495b74ae22d45d1723443fd00ecd3a` | 2025-06-26 |
| Lightning-AI/litgpt | `18c931c15c2398621d35371a12d2b1785e855bb6` | 2026-10-07 |
| huggingface/transformers | `9c59c0c6733990bbf8b1be7cb93b97e57dc73c39` | 2026-10-09 |
| pytorch/torchtune | `bd2a0fc7c31430972728494fa01aaeeb0ebf1ba1` | 2026-09-09 |
| rasbt/LLMs-from-scratch | `cdbd33e6d57a71e20ea31434841095fac50cecd8` | 2026-10-02 |
| anuj0456/OpenArch | `2b0d1a97f73f13ca3565036e6ce041a32c16a42e` | 2026-09-30 |
| casinca/LLM-quest | `e7ab4635c5f447ae93bf8f536625d81e9700e485` | 2026-04-11 |
| state-spaces/mamba | `e9594ce1c732d97440f0332fdc43170a2294dbfa` | 2026-07-22 |
| fla-org/flash-linear-attention | `855e502613d47d8cc139153f0d87ecae5831ac3c` | 2026-10-09 |
| BlinkDL/RWKV-LM | `20be0f8cf0bdf506d8c0030c87a9a3416f95b143` | 2026-09-28 |
| YichenZW/llm-arch-table | `3071d197ad8d50f921cb1274037e35eb6385b11f` | 2026-03-12 |
| datawhalechina/llms-from-scratch-cn | `0c6bdb805bfc7b5bd5f23b641daf81d126e16c25` | 2026-09-17 |

## Where this repository can stand out

Offer a **mechanism-centered learning atlas**: each mechanism has equations, tensor shapes, a readable implementation, a tiny training experiment, meaningful tests, and a recorded comparison. Named models become documented combinations of these mechanisms, with separate fidelity labels for text-only, multimodal, checkpoint-compatible, and simplified variants.

A useful differentiator is a published ledger showing exactly what has been demonstrated: runnable command, tested invariant, reference revision, training budget, and remaining deviations. Existing broad catalogs and teaching repos supply valuable pieces; this repo can make the progression and evidence consistent across families.

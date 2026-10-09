# Awesome LLM Architectures

A hands-on learning repository for understanding, implementing, training, and extending language model architectures. The goal is readable implementations, meaningful correctness checks, and reproducible experiments that can start on a CPU or a single consumer GPU.

**Current status:** research and curriculum planning. No model implementations or runnable training examples have been added yet. All roadmap implementations are planned.

## Start here

- [Implementation and learning roadmap](ROADMAP.md): 48 implementation projects, 150 named-model/family catalog entries, prerequisites, importance and difficulty scores, experiments, completion criteria, and hardware estimates.
- [Reference repository comparison](docs/reference-repositories.md): educational and engineering references, inspected revisions, source-level findings, and ideas to adopt.

Research cutoff: **2026-10-09**. Coverage includes historical foundations and recent publicly documented architectures. Related model generations share implementations where appropriate; undisclosed architectures are recorded with their evidence limits.

## Learning progression

Work is prioritized by importance and ease of implementation once prerequisites are satisfied. Start with three complete models:

1. **Bigram language model:** understand batches, shifted targets, loss, evaluation, and checkpointing.
2. **Tiny GPT-2-style decoder:** implement causal attention, residual blocks, and autoregressive training.
3. **Tiny Llama-style decoder:** learn RMSNorm, RoPE, grouped-query attention, and SwiGLU.

The full curriculum continues through encoder and encoder-decoder models, mixture-of-experts, latent and sparse attention, recurrence and state-space models, hybrid architectures, diffusion language models, multimodal extensions, and inference systems. The roadmap's four-week plan is the opening stage of this larger program.

## Implementation standard

Each planned implementation should include:

- Readable code from scratch, with equations and tensor shapes explained.
- A tiny runnable training example and documented hardware assumptions.
- Tests for behavior and numerical correctness, including cache or recurrent-state agreement where relevant.
- A controlled experiment against a useful baseline.
- Primary sources, reference revisions, common mistakes, and explicit deviations from the original model.

Implementation status will distinguish documented, runnable, tested, trained, and reference-verified work. A model name in the catalog is a coverage target, not evidence of a working implementation. Tiny educational training demonstrates behavior; reproducing large-scale published results is a separate undertaking.

## Contributing

Use the [roadmap's maintenance process](ROADMAP.md#11-maintaining-comprehensive-coverage) when proposing a new architecture. Identify the architectural difference, link primary evidence, specify prerequisites, and propose an affordable experiment and correctness checks. Improvements to existing explanations and verification are as valuable as adding model names.

## License

Repository content is provided under the [MIT license](LICENSE). Referenced code, model weights, datasets, books, and images retain their own license terms.

# Hamad's Learning Log

A personal portfolio of self-directed learning projects. The goal here is not to showcase finished work, but to keep a visible record of consistent progress — building things from scratch to actually understand them, rather than just consuming material.

Each numbered folder is a standalone project. I work through the material myself, writing code by hand, with Claude (in coaching mode) as a guide that asks questions, explains concepts, and reviews what I've written — rather than producing the solution for me. The point is to build intuition, not to ship.

## Structure

```
Hamads-Learning-Log/
├── 01-Micrograd/      # Tiny scalar autograd engine, after Karpathy's micrograd
├── 02-Makemore/       # Character-level language models, after Karpathy's makemore
├── 03-...             # (future projects)
└── CLAUDE.md          # Coaching-mode rules for Claude in this repo
```

## Projects

### 01-Micrograd — done
A from-scratch reimplementation of [Karpathy's `micrograd`](https://github.com/karpathy/micrograd) — a minimal scalar-valued autograd engine plus a small neural-net library on top of it.

Built end-to-end:
- A `Value` class that wraps scalars and tracks the computation graph (parents, op, gradient)
- Graph visualization with `graphviz`
- Manual backpropagation via the chain rule, then automated per-operation `_backward` closures
- A single neuron with `tanh` activation, extended to `Neuron`/`Layer`/`MLP` classes with a `parameters()` helper
- Topological sort + reverse walk for the full backward pass
- A working gradient-descent training loop on a tiny dataset (loss decreases as expected)
- Gradient comparison against PyTorch to verify correctness

### 02-Makemore — in progress
A from-scratch reimplementation of [Karpathy's `makemore`](https://github.com/karpathy/makemore) — character-level language models trained on a list of ~32k names.

Working through:
- Building a bigram counting model with boundary tokens (`.`) for word start/end
- (next) Reshaping counts into a 27×27 tensor, normalizing to probabilities, sampling new names, and computing the negative log-likelihood loss
- (later) Reframing the same problem as a single-layer neural net trained with gradient descent, then expanding to deeper models

## Notes on the format

- Every project lives in a Jupyter notebook, with markdown explaining the reasoning between steps. The notebook is the artifact — the order, the dead ends, and the explanations are part of the record.
- Conventions, mistakes, and refactors are intentionally left visible. The point is to see how thinking developed, not to present a polished final answer.

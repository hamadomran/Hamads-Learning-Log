# Hamad's Learning Log

A personal portfolio of self-directed learning projects. The goal here is not to showcase finished work, but to keep a visible record of consistent progress — building things from scratch to actually understand them, rather than just consuming material.

Each numbered folder is a standalone project. I work through the material myself, writing code by hand, with Claude (in coaching mode) as a guide that asks questions, explains concepts, and reviews what I've written — rather than producing the solution for me. The point is to build intuition, not to ship.

## Structure

```
Hamads-Learning-Log/
├── 01-Micrograd/      # Tiny scalar autograd engine, after Karpathy's micrograd
├── 02-...             # (future projects)
└── CLAUDE.md          # Coaching-mode rules for Claude in this repo
```

## Projects

### 01-Micrograd
A from-scratch reimplementation of [Karpathy's `micrograd`](https://github.com/karpathy/micrograd) — a minimal scalar-valued autograd engine plus a small neural-net library on top of it.

Working through:
- Building a `Value` class that wraps scalars and tracks the computation graph
- Visualizing the graph with `graphviz`
- Manual backpropagation via the chain rule
- Modeling a single neuron with `tanh` activation
- Per-operation `_backward` closures that propagate gradient via the chain rule
- (next) The public `.backward()` method via topological sort

## Notes on the format

- Every project lives in a Jupyter notebook, with markdown explaining the reasoning between steps. The notebook is the artifact — the order, the dead ends, and the explanations are part of the record.
- Conventions, mistakes, and refactors are intentionally left visible. The point is to see how thinking developed, not to present a polished final answer.

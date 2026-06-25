# Hamad's Learning Log

A personal portfolio of self-directed learning projects. The goal here is not to showcase finished work, but to keep a visible record of consistent progress — building things from scratch to actually understand them, rather than just consuming material.

Each numbered folder is a standalone project. I work through the material myself, writing code by hand, with Claude (in coaching mode) as a guide that asks questions, explains concepts, and reviews what I've written — rather than producing the solution for me. The point is to build intuition, not to ship.

## Structure

```
Hamads-Learning-Log/
├── 01-Micrograd/      # Tiny scalar autograd engine, after Karpathy's micrograd
├── 02-Makemore/       # Bigram character-level language model, after Karpathy's makemore
├── 03-Makemore_MLP/   # MLP character-level language model (multi-char context)
├── 04-...             # (future projects)
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

### 02-Makemore — done
A from-scratch reimplementation of [Karpathy's `makemore`](https://github.com/karpathy/makemore) — a **bigram** character-level language model trained on a list of ~32k names.

Built end-to-end:
- A bigram counting model with boundary tokens (`.`) marking word start/end
- Counts collected into a 27×27 tensor, normalized row-wise into a probability distribution
- Sampling new names from that distribution, and measuring quality with the negative log-likelihood loss
- The same problem reframed as a **single-layer neural net**: one-hot inputs, a linear layer, softmax, and a gradient-descent training loop — confirming it converges to the same answer as the counting approach

### 03-Makemore_MLP — done
A multi-layer-perceptron character-level model (Karpathy's `makemore` part 2), predicting the next character from a **block of 3** preceding characters instead of just one.

Built end-to-end:
- A context-window dataset (`block_size = 3`) built per word with `.`-padding, so no training example straddles two names
- A learned **embedding table** mapping each of the 27 characters to a vector, with the context's embeddings flattened into the input of a `tanh` hidden layer, then an output layer producing logits
- Loss via `F.cross_entropy`; **mini-batch** training for fast, noisy gradient steps
- A **learning-rate sweep** to find a sensible LR by watching where the loss curve turns upward
- A **word-level train/val/test split** to measure generalization without data leakage, used to diagnose under- vs. overfitting
- Increasing model capacity (embedding dimension) and discovering the embedding — not the hidden layer — was the real bottleneck
- **Fixing weight initialization** (scaling down the output weights, zeroing the output bias) so the starting loss begins near `-log(1/27) ≈ 3.3` instead of an over-confident ~32
- **Learning-rate decay** for a clean descent that settles instead of bouncing — reaching ~2.19 loss on the held-out test set
- **Sampling** new names autoregressively (feed each predicted character back in as context until the `.` end token)

## Notes on the format

- Every project lives in a Jupyter notebook, with markdown explaining the reasoning between steps. The notebook is the artifact — the order, the dead ends, and the explanations are part of the record.
- Conventions, mistakes, and refactors are intentionally left visible. The point is to see how thinking developed, not to present a polished final answer.

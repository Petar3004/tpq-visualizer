# TPQ Plotting Tool

This Python program provides simple visualization tools for both temporal windows and arbitrary temporal linkings. It was used to generate figures for the thesis:

> Petar Grigorov. *Querying Graphs with Temporal Validity and Uncertainty*. Unpublished Bachelor's thesis, Free University of Bozen-Bolzano, October 2026.

It contains two main plotting functions:

- `plot_window(...)` visualizes a temporal window defined by its three strips and their intersections.
- `plot_linking(...)` visualizes a temporal linking as a collection of points.

## Requirements

The functions require:

```python
import numpy as np
import matplotlib.pyplot as plt
```

## `plot_window`

```python
plot_window(
    sigma,
    delta,
    tau,
    center=None,
    span=None,
    xlim=None,
    ylim=None,
    figsize=(9, 9),
    simplified=False,
)
```

Visualizes three strips in the $(s,t)$-plane:
- V = $\{(s,t):s\in\sigma\}$,
- H = $\{(s,t):t\in\tau\}$, and
- D = $\{(s,t):t-s\in\delta\}$.

The plot shows:

- $\sigma$ as a red horizontal interval,
- $\tau$ as a green vertical interval,
- D as a gray diagonal strip (defined by $\delta$),
- $V \cap H$ as a blue rectangle,
- $V \cap H \cap D$ as a violet region.

### Parameters

` sigma `
: Tuple `(s_min, s_max)` defining the allowed interval for $s$.

` delta `
: Tuple `(d_min, d_max)` defining the allowed interval for $t-s$.

` tau `
: Tuple `(t_min, t_max)` defining the allowed interval for $t$.

` center `
: Optional tuple `(center_x, center_y)` specifying the center of the viewing window.

` span `
: Size of the viewing window. It may be either:

```python
span = 10
```

for an equal horizontal and vertical span, or

```python
span = (10, 6)
```

for separate horizontal and vertical spans.

If omitted, the span is determined automatically.

` xlim `, ` ylim `
: Explicit axis limits. If both are supplied, they override `center` and `span`.

` figsize `
: Matplotlib figure size. Default:

```python
(9, 9)
```

` simplified `
: If `True`, produces a cleaner figure with larger tick labels and without the legend.

### Example

```python
sigma = (1, 4)
delta = (-1, 2)
tau = (2, 6)

plot_window(
    sigma,
    delta,
    tau,
)
```

A custom viewing window can be specified with:

```python
plot_window(
    sigma,
    delta,
    tau,
    center=(3, 4),
    span=10,
)
```

or with explicit limits:

```python
plot_window(
    sigma,
    delta,
    tau,
    xlim=(-2, 8),
    ylim=(-1, 9),
)
```

## `plot_linking`

```python
plot_linking(
    R,
    center=None,
    span=None,
    xlim=None,
    ylim=None,
    figsize=(9, 9),
    simplified=False,
)
```

Plots a finite relation $R \subseteq \mathbb{R}^2$ as points in the $(s,t)$-plane.

### Parameters

` R `
: Iterable containing pairs `(s, t)`.

For example:

```python
R = [
    (1, 2),
    (2, 3),
    (3, 3.5),
    (4, 5),
]
```

` center `
: Optional center `(center_x, center_y)` of the viewing window.

If omitted, the center is calculated from the range of points in `R`.

` span `
: Size of the viewing window.

It can be a scalar:

```python
span = 8
```

or a pair:

```python
span = (8, 6)
```

If omitted, the span is determined automatically from the points.

` xlim `, ` ylim `
: Explicit axis limits. When both are provided, they override `center` and `span`.

` figsize `
: Matplotlib figure size.

` simplified `
: If `True`, uses larger axis and tick labels and omits the legend.

### Example

```python
R = [
    (1, 2),
    (2, 2.5),
    (3, 4),
    (4, 4.5),
]

plot_linking(R)
```

To specify a fixed viewing window:

```python
plot_linking(
    R,
    xlim=(0, 6),
    ylim=(0, 6),
)
```

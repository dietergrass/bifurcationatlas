# Bifurcation Atlas (LaTeX Package)

A structured LaTeX toolkit for building **bifurcation diagram atlases** with:

- radial region layouts
- reusable TikZ region graphics
- structured region metadata
- floating figure support
- configurable captioning system

The package is designed for mathematical visualization workflows, especially in dynamical systems and optimal control.

---

# 1. Installation

Place `bifurcationatlas.sty` in your project folder or local tex tree:

```latex
\usepackage{bifurcationatlas}
```

---

# 2. Basic Usage

```latex
\begin{bifurcationatlas}

\baDeclareRegion[Stable equilibrium]{R1}{green,green,green}
\baDeclareRegion[Unstable branch]{R2}{red,green,red}
\baDeclareRegion[Mixed stability]{R3}{green,red,green}

\baAtlasFigure[Bifurcation diagram]{bifurcation.pdf}{R1,R2,R3}{MyPic}

\end{bifurcationatlas}
```

---

# 3. Atlas Figure Command

```latex
\baAtlasFigure[caption]{background}{region list}{pic name}
```

Arguments:

- caption (optional): caption below background
- background: image file
- region list: comma-separated region IDs
- pic name: TikZ pic used for rendering

---

# 4. Region Declaration

```latex
\baDeclareRegion[caption]{name}{color list}
```

Example:

```latex
\baDeclareRegion[Stable region]{R1}{green,green,green}
```

---

# 5. Configuration

```latex
\baSetup{
  region scale = 1.25,
  region radius = 6,
  caption style = \scriptsize,
  figure scale = 0.25,
  caption shift = -3mm,
  caption label = roman
}
```

---

# 6. Caption Styles

- alpha → (a), (b), (c)
- roman → (i), (ii), (iii)
- Roman → (I), (II), (III)
- arabic → (1), (2), (3)

---

# 7. TikZ Pics

```latex
\baNewPic{MyPic}{
  \draw[thick] (0,0) circle (1);
}
```

---

# 8. Floating Environment

```latex
\begin{bifurcationatlas}
...
\end{bifurcationatlas}
```

Behaves like a figure with list support.

---

# 9. Internal Design

- State layer: counters and environment control
- Config layer: pgfkeys interface
- Rendering layer: TikZ layout engine

---

# 10. Example

```latex
\begin{bifurcationatlas}

\baDeclareRegion{R1}{green,green,green}
\baDeclareRegion{R2}{red,green,red}

\baAtlasFigure{bifurcation.pdf}{R1,R2}{MyPic}

\end{bifurcationatlas}
```

---

# Future Extensions

- stability overlays
- multi-layer bifurcation diagrams
- Julia/Python integration

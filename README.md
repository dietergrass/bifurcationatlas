# BifurcationAtlas

A LaTeX/TikZ package for constructing structured bifurcation diagrams with radial atlas layouts, automatic labeling, and region-based rendering.

---

## Overview

BifurcationAtlas provides a high-level interface to:

- Define bifurcation regions with structured color schemes
- Map semantic region data to TikZ pictures
- Render radial atlases of bifurcation structures
- Overlay atlases onto numerical or graphical backgrounds
- Automatically manage consistent labeling across figures
- Support both positional and semantic color assignment

---

## Requirements

- tikz
- xparse
- graphicx
- pgfkeys
- pgffor
- etoolbox
- hyperref
- newfloat

---

## Installation

### Manual installation

Clone the repository:

```bash
git clone https://github.com/your-username/bifurcationatlas.git
```

Place into your local texmf tree:

```
~/texmf/tex/latex/bifurcationatlas/
```

Refresh database:

```bash
texhash
```

---

## Basic Usage

```latex
\usepackage{bifurcationatlas}
```

---

## Main Environment

```latex
\begin{bifurcationatlas}
...
\end{bifurcationatlas}
```

---

## Region Definition

### Positional

```latex
\baDeclareRegion{RegionName}{R1}{colorA,colorB,colorC}
```

### Semantic

```latex
\baDeclareRegionData{RegionName}{
  SL=colorA,
  SR=colorB,
  MID=colorC
}
```

---

## Region Rendering

```latex
\baNewPic{myRegion}{
  \fill[\baGetColor{SL}] (0,0) -- (1,1) -- (2,0);
}
```

Render:

```latex
\baRenderRegion{myRegion}{R1}
```

---

## Radial Atlas

```latex
\baRadialAtlas{R1,R2,R3}{myRegion}
```

---

## Full Example

```latex
\baAtlasFigure{Caption}{background.png}{R1,R2,R3}{myRegion}
```

---

## Color Access

```latex
\fill[\baGetColor{SL}] (0,0) circle (1cm);
```

---

## Features

- Automatic labeling
- Radial layout engine
- Semantic color mapping
- Background overlay support

---

## Version

1.2

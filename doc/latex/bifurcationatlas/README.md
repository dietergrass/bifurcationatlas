# Bifurcation Atlas (LaTeX Package)

A structured LaTeX toolkit for building **bifurcation diagram atlases** with:

- modular region definitions
- radial and Cartesian layouts
- TikZ-based rendering templates
- structured metadata (caption, label, colors)
- floating figure support
- configurable global and local settings via PGF keys

The package is designed for scientific visualization in dynamical systems and optimal control.

---

# 1. Installation

Place `bifurcationatlas.sty` in your local project folder or TeX tree:

```latex
\usepackage{bifurcationatlas}
```

---

# 2. Core Concept

A *bifurcation atlas* consists of:

- an **atlas template** (TikZ drawing definition)
- multiple **regions** with named parameters
- a **rendering layer** that arranges regions spatially
- an optional **background bifurcation diagram**

Each atlas is initialized once and then populated with regions.

---

# 3. Atlas Definition

## 3.1 Initialize an Atlas Template

```latex
\initAtlas{Cartel}{LL,HL,M,HH,C}{
  \fill[\baColor{LL}] (0,0) rectangle (1,1);
  \fill[\baColor{HL}] (1,0) rectangle (2,1);
  \fill[\baColor{M}]  (0,1) rectangle (1,2);
  \fill[\baColor{HH}] (1,1) rectangle (2,2);

  \draw[line width=2pt] (0,2)--(0,0)--(2,0);
  \draw (0,1)--(2,1);
  \draw (1,0)--(1,2);
}
```

Arguments:

- atlas name
- list of variables (color keys)
- TikZ template body

---

## 3.2 Activate Atlas in Document

```latex
\begin{bifurcationatlas}
\setAtlas{Cartel}
...
\end{bifurcationatlas}
```

---

# 4. Region Definition

## 4.1 Create a Region

```latex
\baNewRegion[
  caption={Region 1},
  label={ba:R1}
]{R1}{
  SL=Unstable,
  SR=Periodic
}
```

Arguments:

- optional key–value metadata:
  - `caption`
  - `label`
- region name
- color mapping list

---

## 4.2 Example

```latex
\baNewRegion[
  caption={Stable region},
  label={ba:R1}
]{R1}{
  SL=Stable,
  SR=Unstable
}
```

---

# 5. Atlas Figure

## 5.1 Background + Regions

```latex
\baAtlasFigure[
  caption={Cartel Diagram},
  label=ba:center
]{background.pdf}{R1,R2,R3}
```

Arguments:

- optional key–value:
  - caption
  - label
- background image
- region list

---

# 6. Rendering Regions

Regions are placed using a radial layout:

```latex
\baRadialAtlas{R1,R2,R3}
```

Each region is rendered using the active atlas template.

---

# 7. Labeling System

Each region can define:

```latex
label={ba:R1}
```

Then referenced via:

```latex
\ref{ba:R1}
```

Additionally:

```latex
\basubref{ba:R1}
```

returns the **subfigure index** of the region.

---

# 8. Configuration System

Global configuration is handled via:

```latex
\baSetup{
  region scale = 1.25,
  region radius = 6.5,
  figure scale = 0.35,
  caption style = \scriptsize,
  caption shift = -3mm,
  caption label = roman,
  debug = true
}
```

---

## 8.1 Available Options

| Key | Description |
|-----|-------------|
| `region scale` | scaling of region drawings |
| `region radius` | radial layout radius |
| `figure scale` | background image scale |
| `caption style` | caption font size |
| `caption shift` | vertical caption shift |
| `caption label` | labeling style (arabic, roman, Roman, alpha) |

---

# 9. Caption Styles

Supported formats:

| Style | Output |
|------|--------|
| `arabic` | (1), (2), (3) |
| `roman` | (i), (ii), (iii) |
| `Roman` | (I), (II), (III) |
| `alpha` | (a), (b), (c) |

---

# 10. Floating Environment

The atlas behaves like a figure:

```latex
\begin{bifurcationatlas}
...
\end{bifurcationatlas}
```

It is internally based on a floating environment and supports numbering and referencing.

---

# 11. Complete Example

```latex
\initAtlas{SimpleState}{SL,SR}{
  \fill[\baColor{SL}] (0,0) rectangle (1,2);
  \fill[\baColor{SR}] (1,0) rectangle (2,2);
}

\begin{bifurcationatlas}[region scale=1.5]
\setAtlas{SimpleState}

\baNewRegion[
  caption={Left state},
  label={ba:R1}
]{R1}{SL=Stable,SR=Unstable}

\baNewRegion[
  caption={Right state},
  label={ba:R2}
]{R2}{SL=Unstable,SR=Stable}

\baAtlasFigure[
  caption={Simple bifurcation diagram},
  label=ba:center
]{diagram.pdf}{R1,R2}

\end{bifurcationatlas}
```

---

# 12. Internal Design

The package is structured into three layers:

### State Layer
- counters (`bafigure`, `basubfigure`)
- atlas registry

### Configuration Layer
- `/ba/core/*` (global parameters)
- `/ba/config` (user interface)

### Rendering Layer
- TikZ atlas templates
- radial layout engine
- region compiler

---

# 13. Future Extensions

Planned features:

- stability overlays
- multi-layer atlases
- dynamic TikZ recomposition
- external Julia/Python coupling
- automatic bifurcation detection hooks
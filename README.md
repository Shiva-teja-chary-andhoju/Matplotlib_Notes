# Matplotlib Notes

Matplotlib Essentials: Quick Reference.
-👉 [View in NBViewer](https://nbviewer.org/github/Shiva-teja-chary-andhoju/Matplotlib_Notes/blob/main/matplotlib.ipynb)

- [Matplotlib Official Documentation & User Guide](https://matplotlib.org/stable/index.html)

## Table of Contents

1. [What is Matplotlib?](#1-what-is-matplotlib)
2. [Basic Plot Anatomy](#2-basic-plot-anatomy)
3. [Line Plots](#3-line-plots)
4. [Bar Charts](#4-bar-charts)
5. [Histograms](#5-histograms)
6. [Scatter Plots](#6-scatter-plots)
7. [Pie Charts](#7-pie-charts)
8. [Box Plots](#8-box-plots)
9. [Titles, Labels & Legends](#9-titles-labels--legends)
10. [Colors, Styles & Markers](#10-colors-styles--markers)
11. [Axis Limits, Ticks & Scale](#11-axis-limits-ticks--scale)
12. [Subplots (Multiple Plots)](#12-subplots-multiple-plots)
13. [Figure Size & Layout](#13-figure-size--layout)
14. [Annotations & Text](#14-annotations--text)
15. [Grid & Style Sheets](#15-grid--style-sheets)
16. [Twin Axes (Dual Y-Axis)](#16-twin-axes-dual-y-axis)
17. [Working with Pandas DataFrames](#17-working-with-pandas-dataframes)
18. [Saving Figures](#18-saving-figures)
19. [Object-Oriented vs Pyplot API](#19-object-oriented-vs-pyplot-api)

---

## 1. What is Matplotlib?

A Python library for creating static, animated, and interactive visualizations. `pyplot` is its most common module — provides a MATLAB-like interface for quick plotting.

| Term | Description |
|---|---|
| `Figure` | The entire window/canvas that holds everything |
| `Axes` | A single plot area inside a figure (a figure can have many) |
| `Axis` | The x or y axis of an Axes (ticks, labels, limits) |
| `Artist` | Anything drawn on the figure (lines, text, patches) |

```python
import matplotlib.pyplot as plt
import numpy as np
plt.style.available   # list built-in styles
```

---

## 2. Basic Plot Anatomy

| Function | Description |
|---|---|
| `plt.plot(x, y)` | Draw a line plot |
| `plt.show()` | Display the figure |
| `fig, ax = plt.subplots()` | Create a figure and one Axes (recommended way to start) |

```python
x = [1, 2, 3, 4]
y = [10, 20, 25, 30]

plt.plot(x, y)
plt.show()

# Object-oriented style (recommended for anything beyond a quick plot)
fig, ax = plt.subplots()
ax.plot(x, y)
plt.show()
```

---

## 3. Line Plots

| Function | Description |
|---|---|
| `plt.plot(x, y)` | Basic line plot |
| `plt.plot(x, y, 'r--')` | Shorthand format string (color + line style) |
| `plt.plot(x, y1, x, y2)` | Multiple lines on the same axes |
| `linewidth=`, `linestyle=` | Control line thickness and style |

```python
x = np.arange(0, 10, 0.1)
y1 = np.sin(x)
y2 = np.cos(x)

plt.plot(x, y1, label='sin')
plt.plot(x, y2, label='cos', linestyle='--', linewidth=2)
plt.legend()
plt.show()

plt.plot(x, y1, 'r--')   # red dashed line (shorthand)
```

---

## 4. Bar Charts

| Function | Description |
|---|---|
| `plt.bar(x, height)` | Vertical bar chart |
| `plt.barh(y, width)` | Horizontal bar chart |
| `plt.bar(x, y, width=)` | Control bar width |
| Grouped bars | Offset x positions manually for side-by-side bars |

```python
teams = ['A', 'B', 'C']
sales = [100, 150, 90]

plt.bar(teams, sales, color='skyblue')
plt.barh(teams, sales)

# Grouped bar chart
x = np.arange(len(teams))
plt.bar(x - 0.2, [100, 150, 90], width=0.4, label='2024')
plt.bar(x + 0.2, [110, 140, 95], width=0.4, label='2025')
plt.xticks(x, teams)
plt.legend()
```

---

## 5. Histograms

| Function | Description |
|---|---|
| `plt.hist(data, bins=)` | Distribution of a numeric column |
| `bins=n` | Number of bins (buckets) |
| `density=True` | Normalize so the area sums to 1 |
| `cumulative=True` | Show cumulative distribution |

```python
data = np.random.randn(1000)

plt.hist(data, bins=30, color='steelblue', edgecolor='black')
plt.hist(data, bins=30, density=True)
plt.hist(data, bins=30, cumulative=True)
```

---

## 6. Scatter Plots

| Function | Description |
|---|---|
| `plt.scatter(x, y)` | Basic scatter plot |
| `c=` | Color each point (array or single color) |
| `s=` | Size of each point (array or single size) |
| `alpha=` | Transparency (0 = invisible, 1 = solid) |

```python
x = np.random.rand(50)
y = np.random.rand(50)
sizes = np.random.rand(50) * 200

plt.scatter(x, y, c='blue', alpha=0.6)
plt.scatter(x, y, c=y, s=sizes, cmap='viridis')   # color-mapped by y value
plt.colorbar()
```

---

## 7. Pie Charts

| Function | Description |
|---|---|
| `plt.pie(values, labels=)` | Basic pie chart |
| `autopct='%1.1f%%'` | Show percentage labels on slices |
| `explode=[...]` | Pull a slice out for emphasis |

```python
sizes = [40, 30, 20, 10]
labels = ['A', 'B', 'C', 'D']

plt.pie(sizes, labels=labels, autopct='%1.1f%%')
plt.pie(sizes, labels=labels, explode=[0.1, 0, 0, 0], autopct='%1.1f%%')
```

---

## 8. Box Plots

| Function | Description |
|---|---|
| `plt.boxplot(data)` | Show median, quartiles, and outliers |
| `plt.boxplot([d1, d2, d3])` | Compare multiple distributions side by side |
| `vert=False` | Horizontal box plot |

```python
data = [np.random.randn(100), np.random.randn(100) + 1]

plt.boxplot(data, labels=['Group A', 'Group B'])
plt.boxplot(data, vert=False)
```

---

## 9. Titles, Labels & Legends

| Function | Description |
|---|---|
| `plt.title('...')` | Add a chart title |
| `plt.xlabel('...')` / `plt.ylabel('...')` | Axis labels |
| `plt.legend()` | Show legend (uses `label=` from plot calls) |
| `plt.legend(loc='upper right')` | Control legend position |

```python
plt.plot(x, y1, label='sin')
plt.plot(x, y2, label='cos')
plt.title('Trig Functions')
plt.xlabel('X values')
plt.ylabel('Y values')
plt.legend(loc='upper right')
```

---

## 10. Colors, Styles & Markers

| Function | Description |
|---|---|
| `color='...'` | Named color, hex code, or shorthand (`'r'`, `'g'`, `'b'`) |
| `marker='o'` | Marker shape for data points (`'o'`, `'s'`, `'^'`, `'x'`) |
| `linestyle='--'` | Line style (`'-'`, `'--'`, `'-.'`, `':'`) |
| `cmap='viridis'` | Colormap for scatter/heatmap-style plots |

```python
plt.plot(x, y1, color='#FF5733', marker='o', linestyle='--', markersize=4)
plt.plot(x, y2, color='green', marker='^')
```

---

## 11. Axis Limits, Ticks & Scale

| Function | Description |
|---|---|
| `plt.xlim(min, max)` / `plt.ylim(min, max)` | Set axis range |
| `plt.xticks([...])` / `plt.yticks([...])` | Set custom tick positions/labels |
| `plt.xscale('log')` | Log scale on x-axis |
| `ax.invert_yaxis()` | Reverse the y-axis direction |

```python
plt.xlim(0, 10)
plt.ylim(-2, 2)

plt.xticks([0, 5, 10], ['start', 'mid', 'end'])

plt.yscale('log')

fig, ax = plt.subplots()
ax.plot(x, y1)
ax.invert_yaxis()
```

---

## 12. Subplots (Multiple Plots)

| Function | Description |
|---|---|
| `plt.subplots(rows, cols)` | Grid of Axes in one figure |
| `ax[i, j].plot(...)` | Plot on a specific subplot |
| `plt.subplot(2, 1, 1)` | Older pyplot-style single subplot selection |
| `plt.tight_layout()` | Auto-adjust spacing to avoid overlap |

```python
fig, axes = plt.subplots(2, 2, figsize=(10, 8))

axes[0, 0].plot(x, y1)
axes[0, 0].set_title('Line')

axes[0, 1].bar(teams, sales)
axes[0, 1].set_title('Bar')

axes[1, 0].hist(data[0])
axes[1, 1].scatter(x[:50], y1[:50])

plt.tight_layout()
plt.show()
```

---

## 13. Figure Size & Layout

| Function | Description |
|---|---|
| `plt.figure(figsize=(w, h))` | Set figure size in inches |
| `plt.subplots(figsize=(w, h))` | Set size when creating subplots |
| `dpi=` | Resolution (dots per inch) |
| `plt.tight_layout()` | Prevent overlapping labels/titles |

```python
plt.figure(figsize=(8, 5), dpi=100)
plt.plot(x, y1)

fig, ax = plt.subplots(figsize=(10, 6))
```

---

## 14. Annotations & Text

| Function | Description |
|---|---|
| `plt.text(x, y, '...')` | Place text at a data coordinate |
| `plt.annotate('...', xy=, xytext=)` | Text with an arrow pointing to a data point |
| `plt.axhline(y=)` / `plt.axvline(x=)` | Horizontal/vertical reference line |

```python
plt.plot(x, y1)
plt.text(2, 0.5, 'Peak area')

plt.annotate('Max', xy=(1.5, 1), xytext=(3, 1.3),
             arrowprops=dict(facecolor='black', shrink=0.05))

plt.axhline(y=0, color='gray', linestyle='--')
plt.axvline(x=5, color='red')
```

---

## 15. Grid & Style Sheets

| Function | Description |
|---|---|
| `plt.grid(True)` | Show gridlines |
| `plt.style.use('ggplot')` | Apply a built-in style theme |
| `plt.style.available` | List all available style names |

```python
plt.plot(x, y1)
plt.grid(True, linestyle='--', alpha=0.5)

plt.style.use('seaborn-v0_8-darkgrid')
plt.style.use('dark_background')
```

---

## 16. Twin Axes (Dual Y-Axis)

| Function | Description |
|---|---|
| `ax.twinx()` | Second y-axis sharing the same x-axis |
| `ax.twiny()` | Second x-axis sharing the same y-axis |

```python
fig, ax1 = plt.subplots()

ax1.plot(x, y1, color='blue')
ax1.set_ylabel('sin', color='blue')

ax2 = ax1.twinx()
ax2.plot(x, y2 * 100, color='red')
ax2.set_ylabel('cos (scaled)', color='red')
```

---

## 17. Working with Pandas DataFrames

| Function | Description |
|---|---|
| `df.plot()` | Quick plot directly from a DataFrame (uses matplotlib under the hood) |
| `df.plot(kind='bar', x=, y=)` | Specify plot type and columns |
| `plt.plot(df['x'], df['y'])` | Plot DataFrame columns explicitly |

```python
import pandas as pd
df = pd.DataFrame({'Month': ['Jan', 'Feb', 'Mar'], 'Sales': [100, 150, 120]})

df.plot(x='Month', y='Sales', kind='bar')
plt.plot(df['Month'], df['Sales'], marker='o')
```

---

## 18. Saving Figures

| Function | Description |
|---|---|
| `plt.savefig(path)` | Save the current figure to a file |
| `plt.savefig(path, dpi=300)` | Save at higher resolution |
| `plt.savefig(path, bbox_inches='tight')` | Trim extra whitespace around the figure |
| Formats | `.png`, `.jpg`, `.pdf`, `.svg` (based on file extension) |

```python
plt.plot(x, y1)
plt.savefig('plot.png', dpi=300, bbox_inches='tight')
plt.savefig('plot.pdf')
```

---

## 19. Object-Oriented vs Pyplot API

| Style | Description |
|---|---|
| Pyplot (`plt.plot(...)`) | Quick, MATLAB-style, implicit "current figure" — good for one-off plots |
| Object-Oriented (`fig, ax = plt.subplots()`) | Explicit figure/axes objects — recommended for multi-plot or reusable code |

```python
# Pyplot style - quick and simple
plt.plot(x, y1)
plt.title('Quick Plot')
plt.show()

# Object-oriented style - explicit and scalable
fig, ax = plt.subplots()
ax.plot(x, y1)
ax.set_title('OO Plot')
fig.savefig('oo_plot.png')
```

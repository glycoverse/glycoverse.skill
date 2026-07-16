# Glycoverse package map

Use this file only to identify likely packages. These descriptions deliberately
stay broad because package APIs, workflows, and feature sets change. After
choosing a package, follow [help-resources.md](help-resources.md) to discover its
current documentation.

## Entry points

| Package | Basic description | Start here |
|---|---|---|
| `glycoverse` | Meta-package for installing, loading, and managing the ecosystem. | <https://glycoverse.github.io/glycoverse/> |
| `glysmith` | High-level, integrated glyco-omics analysis workflows. | <https://glycoverse.github.io/glysmith/> |

## Omics data analysis

| Package | Basic description | Start here |
|---|---|---|
| `glyexp` | Experimental data containers and data-management infrastructure. | <https://glycoverse.github.io/glyexp/> |
| `glyread` | Import of glycomics and glycoproteomics data. | <https://glycoverse.github.io/glyread/> |
| `glyclean` | Data cleaning and preprocessing. | <https://glycoverse.github.io/glyclean/> |
| `glystats` | Statistical analysis of glyco-omics data. | <https://glycoverse.github.io/glystats/> |
| `glyvis` | Visualization of glyco-omics data and results. | <https://glycoverse.github.io/glyvis/> |

## Glycan structure analysis

| Package | Basic description | Start here |
|---|---|---|
| `glyrepr` | Computational representation of glycan compositions and structures. | <https://glycoverse.github.io/glyrepr/> |
| `glyparse` | Parsing of textual glycan representations. | <https://glycoverse.github.io/glyparse/> |
| `glymotif` | Glycan motif detection and analysis. | <https://glycoverse.github.io/glymotif/> |
| `glydet` | Glycan-derived trait analysis. | <https://glycoverse.github.io/glydet/> |
| `glydraw` | Glycan structure visualization. | <https://glycoverse.github.io/glydraw/> |

## Specialized packages

| Package | Basic description | Start here |
|---|---|---|
| `glydb` | Glycan database access. | <https://glycoverse.github.io/glydb/> |
| `glyanno` | Glycan annotation. | <https://glycoverse.github.io/glyanno/> |
| `glyenzy` | Glycan biosynthesis and enzyme analysis. | <https://glycoverse.github.io/glyenzy/> |
| `glyfun` | Functional enrichment analysis. | <https://glycoverse.github.io/glyfun/> |

## Route ambiguous requests

- Start at the ecosystem overview when package ownership is unclear:
  <https://glycoverse.org.cn/>.
- Search the current reference indexes of two or more likely packages rather
  than choosing from package names alone.
- Inspect current `DESCRIPTION` files to learn dependencies and scope.
- Confirm cross-package workflows in current articles or case studies.
- Never invent a function from the basic descriptions in this file.

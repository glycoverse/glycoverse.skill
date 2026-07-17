# Glycoverse functionality catalog

Use this catalog to translate an analysis request into candidate packages and
public functions. Search it before implementing an analysis from scratch. The
names below were checked against the local development-package exports and help
topics on 2026-07-17; they are discovery hints, not stable signature contracts.
After selecting candidates, follow [help-resources.md](help-resources.md) to
verify current arguments, input classes, return values, and deprecations.

## Package index

- [Ecosystem management](#ecosystem-management): `glycoverse`
- [Quantitative glyco-omics](#quantitative-glyco-omics): `glyexp`, `glyread`,
  `glyclean`, `glystats`, `glyvis`
- [Glycan structures and derived biology](#glycan-structures-and-derived-biology):
  `glyrepr`, `glyparse`, `glymotif`, `glydet`, `glydraw`
- [Databases, annotation, biosynthesis, and function](#databases-annotation-biosynthesis-and-function):
  `glydb`, `glyanno`, `glyenzy`, `glyfun`

## Quick task routing

| Need | Start with |
|---|---|
| Create or manipulate an experiment container | `glyexp::GlycomicSE()`, `glyexp::GlycoproteomicSE()`, `glyexp::*_col()`, `glyexp::*_row()` |
| Import search-engine or quantification output | the matching `glyread::read_*()` function |
| Clean, normalize, impute, filter, batch-correct, or QC data | `glyclean` |
| Run differential, multivariate, clustering, correlation, survival, or ROC analysis | `glystats` |
| Plot experiments or `glystats` results | `glyvis` |
| Represent or inspect compositions and structures | `glyrepr` |
| Parse a textual glycan format | `glyparse` |
| Detect, count, extract, or visualize glycan motifs | `glymotif` |
| Calculate derived traits or structural meta-properties | `glydet` |
| Draw SNFG cartoons or place glycans in ggplot2 | `glydraw` |
| Retrieve known glycans or map GlyTouCan accessions | `glydb` |
| Infer compositions/structures, calculate masses, or assign GlyTouCan IDs | `glyanno` |
| Identify enzymes or reconstruct biosynthetic paths | `glyenzy` |
| Run protein- or glycan-centric functional enrichment | `glyfun` |
| Install, update, or diagnose the ecosystem | `glycoverse` |

## Ecosystem management

### `glycoverse`: ecosystem management

- List ecosystem packages with `glycoverse_packages()` and dependency status
  with `glycoverse_deps()`.
- Diagnose installed versions and environment state with `glycoverse_sitrep()`.
- Update Glycoverse packages with `glycoverse_update()`.
- Inspect package conflicts with `glycoverse_conflicts()`.

## Quantitative glyco-omics

### `glyexp`: containers and data manipulation

- Create the default experiment containers with `GlycomicSE()` and
  `GlycoproteomicSE()`; test or coerce objects with `is_glycomic_se()`,
  `is_glycoproteomic_se()`, `as_glycomic_se()`, and
  `as_glycoproteomic_se()`.
- Inspect an experiment with `summarize_experiment()`, `n_samples()`,
  `n_variables()`, `samples()`, and `variables()`.
- Manipulate sample columns with `arrange_col()`, `filter_col()`,
  `mutate_col()`, `rename_col()`, `select_col()`, the `slice_*_col()` family,
  and the `*_join_col()` family. Use the corresponding `*_row()` functions for
  variables. Verify legacy `*_obs()` and `*_var()` aliases before using them.
- Normalize variable identifiers with `standardize_variable()` and summarize a
  glycoproteomics experiment as a pseudo-glycome with `as_pseudo_glycome()`.
- Use `as_se()`, `from_se()`, and the legacy `experiment()` accessors only when
  current documentation and the object's container generation require them.

### `glyread`: vendor and search-engine imports

Choose the reader matching the producing software rather than writing a custom
table parser:

- pGlyco3: `read_pglyco3()`; pGlyco3 plus pGlycoQuant:
  `read_pglyco3_pglycoquant()`.
- Byonic plus Byologic: `read_byonic_byologic()`; Byonic plus pGlycoQuant:
  `read_byonic_pglycoquant()`.
- MSFragger-Glyco: `read_msfragger()`.
- StrucGP: `read_strucgp()`.
- GlycanFinder: `read_glycan_finder()`.
- glyco-decipher: `read_glyco_decipher()`.
- GlyHunter: `read_glyhunter()`.

### `glyclean`: preprocessing and quality control

- Run an automatic workflow with `auto_clean()`, or select automatic stages
  with `auto_aggregate()`, `auto_remove()`, `auto_impute()`,
  `auto_normalize()`, `auto_correct_batch_effect()`, and `auto_coda()`.
- Aggregate observations with `aggregate()`; adjust glycopeptide abundance for
  protein abundance with `adjust_protein()`; add site-local sequence context
  with `add_site_seq()`.
- Remove constant, rare, low-expression, low-variance, or low-CV variables with
  `remove_constant()`, `remove_rare()`, `remove_low_expr()`,
  `remove_low_var()`, and `remove_low_cv()`.
- Impute missing values with zero, sample-minimum, half-sample-minimum,
  minimum-probability, sample-wise or feature-wise KNN, SVD, PPCA, BPCA, or
  missForest methods through the matching `impute_*()` function.
- Normalize by total area, median, absolute median, median quotient, quantiles,
  VSN, LoessF/LoessCyc, RLR, RLRMA, or RLRMACyc through the matching
  `normalize_*()` function.
- Detect and correct batch effects with `detect_batch_effect()` and
  `correct_batch_effect()`; visualize them with `plot_batch_pca()`.
- Apply centered or additive log-ratio transformations with `transform_clr()`
  and `transform_alr()`.
- Diagnose data quality with `plot_missing_bar()`, `plot_missing_heatmap()`,
  `plot_int_boxplot()`, `plot_tic_bar()`, `plot_cv_dent()`, `plot_rle()`,
  `plot_rep_scatter()`, and `plot_rank_abundance()`.

### `glystats`: statistical analysis

- Differential analysis: `gly_limma()`, `gly_ttest()`, `gly_wilcox()`,
  `gly_anova()`, `gly_kruskal()`, and covariate-adjusted `gly_ancova()`.
- Effect sizes and result filtering: `gly_fold_change()` and
  `filter_sig_vars()`; extract standardized or underlying results with
  `get_tidy_result()` and `get_raw_result()`.
- Association and outcome analysis: `gly_cor()`, survival analysis with
  `gly_cox()`, and classification performance with `gly_roc()`.
- Dimension reduction and supervised multivariate analysis: `gly_pca()`,
  `gly_plsda()`, `gly_oplsda()`, `gly_tsne()`, and `gly_umap()`.
- Clustering: `gly_hclust()` and `gly_kmeans()`.

### `glyvis`: experiment and result visualization

- Call `autoplot()` on supported experiment and `glystats` result objects when
  a result-aware default plot is appropriate.
- Use `plot_boxplot()`, `plot_heatmap()`, and `plot_logo()` for direct data
  views; use `plot_corrplot()` and `plot_volcano()` for association and
  differential results.
- Use `plot_pca()`, `plot_plsda()`, `plot_oplsda()`, `plot_tsne()`,
  `plot_umap()`, and `plot_roc()` for their matching `glystats` analyses.

## Glycan structures and derived biology

### `glyrepr`: compositions and structure vectors

- Create, coerce, and test compositions with `glycan_composition()`,
  `as_glycan_composition()`, and `is_glycan_composition()`; use the parallel
  `glycan_structure()` family for structures.
- Inspect structures with `structure_nodes()`, `structure_edges()`,
  `get_structure_graphs()`, `get_structure_level()`, `count_mono()`,
  `get_anomer()`, `get_anomer_pos()`, `get_mono_type()`, and `has_linkages()`.
- Convert graph tables back to a structure with `structure_from_tibbles()` and
  serialize structures with `structure_to_iupac()`.
- Simplify or standardize structures with `convert_to_generic()`,
  `fill_anomer_pos()`, `remove_linkages()`, `remove_substituents()`, and
  `reduce_structure_level()`; validate or enumerate linkages with
  `valid_linkages()` and `possible_linkages()`.
- Apply functions efficiently over structure vectors with `smap()`, `smap2()`,
  `spmap()`, `simap()`, their typed variants, `smap_unique()`, and the
  predicates `ssome()`, `severy()`, and `snone()`.

### `glyparse`: textual structure parsing

- Let `auto_parse()` detect a supported representation when the input format is
  uncertain.
- Use a format-specific parser for GlycoCT, WURCS, KCF, LINUCS, Linear Code,
  GlyCAM IUPAC, pGlyco, or StrucGP: `parse_glycoct()`, `parse_wurcs()`,
  `parse_kcf()`, `parse_linucs()`, `parse_linear_code()`,
  `parse_glycam_iupac()`, `parse_pglyco_struc()`, or
  `parse_strucgp_struc()`.
- Parse the appropriate IUPAC dialect with `parse_iupac_condensed()`,
  `parse_iupac_extended()`, `parse_iupac_compact()`, or
  `parse_iupac_short()`.

### `glymotif`: motif analysis

- Test motif presence with `have_motif()` / `have_motifs()`, count occurrences
  with `count_motif()` / `count_motifs()`, and obtain match locations with
  `match_motif()` / `match_motifs()`.
- Extract all substructures or branch motifs with `extract_motif()` and
  `extract_branch_motif()`; generate motif specifications with
  `dynamic_motifs()` and `branch_motifs()`.
- Annotate data with motif indicators or counts using `add_motifs_lgl()` and
  `add_motifs_int()`.
- Discover known motifs with `db_motifs()`, `db_motif_info()`, and
  `is_known_motif()`; retrieve structures/alignments with
  `get_motif_structure()` and `get_motif_alignment()` and visualize matches
  with `view_motif()`.

### `glydet`: meta-properties, motifs, and derived traits

- Add or retrieve structural meta-properties with `add_meta_properties()` and
  `get_meta_properties()`. Available property functions cover glycan type,
  bisection, antennae, arm/core fucosylation, total fucose, galactose, mannose,
  sialic acid, and terminal galactose (`n_glycan_type()`, `has_bisecting()`,
  `n_antennae()`, `n_arm_fuc()`, `n_core_fuc()`, `n_fuc()`, `n_gal()`,
  `n_man()`, `n_sia()`, and `n_terminal_gal()`).
- Quantify structural motifs across an experiment with `quantify_motifs()`.
- Calculate curated traits with `derive_traits()` and trait sets such as
  `traits_basic()`, `traits_detailed()`, `traits_clerc_2018()`,
  `traits_li_2025()`, and `traits_fu_2026()`.
- Construct custom total, proportion, ratio, weighted-sum, or weighted-mean
  traits with `total()`, `prop()`, `ratio()`, `wsum()`, and `wmean()`; inspect
  definitions with `explain_trait()` / `explain_traits()`.

### `glydraw`: SNFG rendering and ggplot2 integration

- Render a glycan as an SNFG cartoon with `draw_cartoon()` and save it with
  `save_cartoon()`; batch-export structures with `export_cartoons()`.
- Construct grid graphics with `glycanGrob()`.
- Place glycan cartoons at ggplot2 positions with `geom_glycan()`, use them as
  axis labels with `scale_x_glycan()` / `scale_y_glycan()`, and use them as
  legend labels with `guide_glycan()`.

## Databases, annotation, biosynthesis, and function

### `glydb`: known glycan data

- Retrieve known structures with `glydb_structures()`, compositions with
  `glydb_compositions()`, and available organism filters with
  `glydb_species()`.
- Resolve GlyTouCan accessions to structure objects with
  `glytoucan_to_struc()`.

### `glyanno`: mass and hierarchical annotation

- Calculate glycan mass-to-charge values with `calculate_mz()` and compare
  mass error with `ppm()`; infer candidate compositions from observed m/z with
  `mz_to_comp()`.
- Convert compositions to candidate structures with `comp_to_struc()`.
- Expand partial annotations with `enhance_comp()` and `enhance_struc()`.
- Assign GlyTouCan accessions to structures with `struc_to_glytoucan()`.
- Use `glyanno_mass_dict()` when a documented workflow needs the package's
  default residue mass dictionary.

### `glyenzy`: enzymes and biosynthetic pathways

- Search the packaged enzyme knowledge with `db_enzymes()` and create custom
  rules with `make_enzyme()`.
- Apply an enzyme to a structure with `apply_enzyme()`, test whether an enzyme
  can synthesize a glycan with `have_enzyme()`, match the residues it added
  with `match_enzyme()`, and visualize the match with `view_enzyme()`.
- Identify or count potentially involved enzymes with `find_enzyme()` and
  `count_enzyme()`.
- Grow structures one or more steps with `grow_glycans_step()` and
  `grow_glycans()`.
- Find a path between structures with `path_biosynthesis()` or reconstruct a
  broader biosynthetic history with `trace_biosynthesis()`.

### `glyfun`: functional enrichment

- Run protein-centric over-representation analysis with `enrich_ora_*()` and
  gene-set enrichment analysis with `enrich_gsea_*()`.
- Run glycan-centric over-representation analysis with `enrich_gc_ora_*()` and
  glycan-centric gene-set enrichment analysis with `enrich_gc_gsea_*()`.
- For each family, select the knowledge base by suffix: `_go`, `_kegg`, `_do`,
  `_reactome`, `_wp`, or `_ncg`.
- Prepare an observed-feature background with `detected_universe()` when the
  chosen function's current documentation calls for a detected universe.

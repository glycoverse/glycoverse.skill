---
name: glycoverse
description: Use the Glycoverse R ecosystem for glycomics, glycoproteomics, and glycan-structure analysis. Apply when selecting Glycoverse packages, designing or implementing analysis workflows, importing or cleaning glyco-omics data, working with experiment containers, running statistics or visualization, parsing or drawing glycans, analyzing motifs, traits, annotations, databases, biosynthesis, or enrichment, troubleshooting Glycoverse code, or finding current package documentation and help.
---

# Use Glycoverse

Do not treat this skill as Glycoverse API documentation. Glycoverse changes
frequently. Use this skill to identify likely packages and then discover the
current, version-matched documentation before producing code.

## Start with the task, not a package guess

1. Identify whether the task concerns quantitative omics data, glycan
   structures, or both.
2. Read [references/packages.md](references/packages.md) only as a broad package
   map. Do not derive function names or behavior from it.
3. Follow [references/help-resources.md](references/help-resources.md) to perform
   a fresh documentation pass for the package versions in scope.
4. Preserve the container and representation used by the user's existing code
   unless current documentation requires a conversion.
5. Verify every proposed function, important argument, input class, and return
   value against the discovered sources before writing or changing code.

## Compose workflows

Use these broad routes only to decide where to begin searching:

- Omics: `glyread` -> `glyexp` -> `glyclean` -> `glystats` -> `glyvis`.
- Glycan structures: `glyrepr` -> `glyparse` -> `glymotif` / `glydet` ->
  `glydraw`.
- Specialized work: add `glydb`, `glyanno`, `glyenzy`, or `glyfun` only for
  their specific roles.

These are not API or dependency guarantees. Confirm the current workflow in the
relevant package articles. Prefer explicit `package::function()` calls in
reusable code when current documentation establishes ownership and name
conflicts could be unclear.

## Verify before coding

Prefer evidence in this order:

1. The checked-out source, tests, and documentation when working in a package
   repository.
2. Help from the installed package and its installed vignettes.
3. The package's current pkgdown reference and articles.
4. The package source and issue tracker on GitHub.

Do not infer an API from this skill, a package description, an old example, or a
similarly named function in another package. Check exports, signatures,
accepted input classes, return types, and examples. State clearly when a package
is unavailable and the answer relies on online documentation instead of a local
verification.

## Install only when requested

Do not change the user's R library merely to answer a question. If installation
is in scope, open the current **Installation** section of the `glycoverse`
meta-package site or the target package site and follow it exactly. Determine
whether the user needs the complete ecosystem or one package, and verify the
current repository and dependency instructions. Do not reuse an installation
command remembered from this skill or an older conversation.

## Deliver useful answers

- Name the package responsible for each important step.
- Provide a minimal runnable path before optional extensions.
- Separate verified current API from conceptual pseudocode.
- Link the relevant package reference or vignette when the user needs to learn
  more.
- For failures, capture the exact error, package versions, `sessionInfo()`, and
  a minimal reproducible example before diagnosing.

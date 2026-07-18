---
name: glycoverse
description: Use the Glycoverse R ecosystem for glycomics, glycoproteomics, and glycan-structure analysis. Apply when discovering whether an existing Glycoverse function provides a requested analysis, selecting packages, designing or implementing workflows, importing or cleaning glyco-omics data, working with experiment containers, running statistics or visualization, parsing or drawing glycans, analyzing motifs, traits, annotations, databases, biosynthesis, or enrichment, troubleshooting Glycoverse code, or finding current package documentation and help.
---

# Use Glycoverse

Use this skill first as a capability index: determine whether Glycoverse already
provides the requested analysis before designing a custom implementation.

Before reinventing a wheel, investigate whether Glycoverse already provides the
functionality. Search the functionality catalog, relevant package exports, and
current package documentation, then reuse and compose the verified public API
when it covers the requirement. Do not propose new code merely because a
familiar generic R solution is available; custom code needs an explicit reason
after this investigation.
Glycoverse changes frequently, so treat listed functions as discovery candidates
and verify them against current, version-matched documentation before coding.

## Start with the task, not a package guess

1. Identify whether the task concerns quantitative omics data, glycan
   structures, or both.
2. Read [references/functionality-catalog.md](references/functionality-catalog.md)
   and search for the user's analytical intent, relevant nouns, and likely
   method names. Use its functions as candidates rather than reimplementing the
   analysis with generic R code.
3. Read [references/packages.md](references/packages.md) when package ownership
   or the broader workflow is unclear.
4. Follow [references/help-resources.md](references/help-resources.md) to perform
   a fresh documentation pass for the package versions in scope.
5. Preserve the container and representation used by the user's existing code
   unless current documentation requires a conversion.
6. Verify every proposed function, important argument, input class, and return
   value against the discovered sources before writing or changing code.

Do not start by writing a custom statistical test, parser, transformation,
annotation routine, motif algorithm, plot, or enrichment workflow. First search
the catalog and current package exports for an existing public Glycoverse
function. Implement custom logic only when verified public APIs do not cover the
requirement or when the user explicitly requests a custom implementation, and
state what you searched and why the existing functionality was insufficient.

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

## Respect package boundaries

Use only documented, exported Glycoverse interfaces. Do not call internal
helpers with `:::` or reach into unexported objects, even as a workaround.
Trust the package's public API and its documented contracts.

If verified use of a public interface exposes a package bug, capture a minimal
reprex and create an issue in the corresponding package repository. Include the
public call, exact error or incorrect result, package version, and
`sessionInfo()`. Do not replace the report with an internal-helper workaround.

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

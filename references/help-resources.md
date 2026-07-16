# Discover current Glycoverse help

Perform this workflow for every substantive Glycoverse coding task. The goal is
to ground the answer in the exact checkout or installed version whenever
possible, and otherwise in the newest authoritative online source.

## 1. Establish the version and source context

Determine which situation applies:

- **Package checkout:** the user is working inside a Glycoverse repository.
- **Installed package:** the task concerns code running in a local R library.
- **No local package:** only online discovery is possible.

For an installed package, record its version and the R session:

```r
packageVersion("glyexp")
sessionInfo()
```

For a checkout, read `DESCRIPTION` and record the current Git commit. A checkout
may be newer than the installed package, so do not mix their documentation
silently.

## 2. Search the closest authoritative source

### In a package checkout

Search these files before the web:

1. `DESCRIPTION` for scope, version, dependencies, and project URLs.
2. `NAMESPACE` and roxygen source under `R/` for exports and signatures.
3. `man/*.Rd` for generated function documentation.
4. `tests/testthat/` for behavior, edge cases, and class contracts.
5. `vignettes/`, `README.Rmd`, and examples for intended workflows.
6. `NEWS.md` for migrations, deprecations, and recent behavior changes.

Use fast targeted searches:

```sh
rg -n "function_name|class_name|error fragment" R man tests vignettes NEWS.md
rg -n "^export|^exportMethods|^S3method" NAMESPACE
```

If executing development code, load the checkout so probes do not accidentally
use an older installed version:

```r
devtools::load_all()
```

### From an installed package

Discover the actual public surface rather than guessing names:

```r
help(package = "glyexp")
getNamespaceExports("glyexp")
ls("package:glyexp") # after library(glyexp)
```

Inspect a candidate only after discovering it:

```r
help("function_name", package = "glyexp")
args(glyexp::function_name)
example("function_name", package = "glyexp")
```

Find workflow documentation shipped with that version:

```r
vignette(package = "glyexp")
vignette("vignette-name", package = "glyexp")
```

For an S3 or S4 behavior question, inspect registered methods as appropriate:

```r
methods(class = "class_name")
methods("generic_name")
showMethods("generic_name", where = getNamespace("glyexp"))
```

### Online

Use current official sources in this order:

1. Package pkgdown site: `https://glycoverse.github.io/<package>/`
2. Package source: `https://github.com/glycoverse/<package>`
3. Published package/manual: `https://glycoverse.r-universe.dev/`
4. Ecosystem overview: <https://glycoverse.org.cn/>

On pkgdown, inspect **Reference**, **Articles**, and **Changelog**. If a vignette
example conflicts with a newer changelog entry or current function reference,
follow the newer source and verify in code or tests. On GitHub, inspect
`DESCRIPTION`, `R/`, `man/`, tests, vignettes, and recent releases. Use the
repository issue tracker for exact errors only after searching current docs and
closed issues.

## 3. Verify before proposing code

For every important call, verify:

- the function is exported by the package/version in scope;
- its argument names, defaults, and accepted input classes;
- its return type and any metadata or attributes the next step requires;
- whether the function or workflow is deprecated or superseded;
- which package owns the function;
- whether the example applies to glycomics, glycoproteomics, or both.

When a downstream call consumes an upstream result, verify the handoff in both
packages. Documentation in one package alone does not prove cross-package
compatibility.

## 4. Reconcile changing documentation

Use this precedence:

1. Tests and source in the exact checkout being changed.
2. Installed help matching the version that reproduces the behavior.
3. Documentation for that same released version.
4. Development pkgdown documentation and the default GitHub branch.
5. Old examples, blog posts, and search snippets.

If sources describe different versions, name the versions and do not combine
their APIs. If current behavior cannot be verified, label code as conceptual or
ask for the relevant package version instead of presenting a guess as runnable.

## 5. Diagnose and escalate with evidence

Before diagnosing a failure or filing an issue, collect:

- a minimal reproducible example;
- the exact error or warning;
- relevant input structure with sensitive data removed;
- `sessionInfo()` and affected package versions;
- expected and observed results;
- links to the documentation and issues already checked.

Search the package's open and closed GitHub issues for the exact error fragment,
function name, and relevant class name. Use the repository's support or issue
template when one exists.

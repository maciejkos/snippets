#r #devtools
1. How fix devtools "Installation failed: Bad credentials (401)" issue?

```r
# How fix devtools "Installation failed: Bad credentials (401)" issue?

install_github("SOME_PACKAGE")
> Installation failed: Bad credentials (401)

Sys.unsetenv("GITHUB_PAT") # to make devtools not use the active github token
install_github("SOME_PACKAGE") # now it works
```
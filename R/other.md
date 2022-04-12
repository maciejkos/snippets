#r #devtools
1. How fix devtools "Installation failed: Bad credentials (401)" issue?
2. How to disable scientific notation?

```r
# How fix devtools "Installation failed: Bad credentials (401)" issue?

install_github("SOME_PACKAGE")
> Installation failed: Bad credentials (401)

Sys.unsetenv("GITHUB_PAT") # to make devtools not use the active github token
install_github("SOME_PACKAGE") # now it works

```


```r
# How to disable scientific notation?
options(scipen=999)
```

```r
install.packages('installr')
library("installr")
updateR()
```

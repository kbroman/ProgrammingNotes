## Notes on Julia

```
brew tap staticfloat/julia
brew install --HEAD --64bit julia
```

In `.emacs`:

```
(setq inferior-julia-program-name "/usr/local/bin/julia")
```

---

On linux, installed by [downloading the `.tar.gz`
file](https://julialang.org/downloads/) with "generic linux on x86",
extracted to `/usr/local`, and put symbolic link to
`/usr/local/julia-1.6.1/bin/julia` in `/usr/local/bin`

---

Installing packages:

```
Pkg.update()
Pkg.add("Distances")
Pkg.clone("https://github.com/sens/FaSTLMM.jl.git")
```

---

run script from within Julia:

```
include("lmmtest.jl")
```

---

To enable use in jupyter notbooks:

```
using Pkg
Pkg.add("IJulia")
```

Start jupyter by typing `jupyter notebook` at unix prompt, then click
New to create a new notebook, choosing the desired language.

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

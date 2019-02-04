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

On linux, installed by downloading `.sh` file with "generic linux
binaries", extracted to `/usr/local/src`, and put symbolic link to
`/usr/local/src/julia-1.1.0/bin/julia` in `/usr/local/bin`

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

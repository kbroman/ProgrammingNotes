## Notes on D

`typeid`: to get type of object

```
writeln("typeid(genotype_matrix): ", typeid(genotype_matrix));  // GenotypeCombinator[][]
writeln("typeid(symbols): ", typeid(symbols));                  // ObservedGenotypes
```

A `GenotypeCombinator` is a list of `TrueGenotypes`?

---

```
auto a = new bool[n_wanted];
a[] = false;
```

```
auto b = new bool[n][m];
b[][] = false;
```

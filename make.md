## GNU Make

- `$@` - the target
- `$<` - first prerequisite
- `$^` - all prerequisites
- `$(<F)` - file part of first prerequisite
- `$(<D)` - directory part of first prerequisite
- `$(@D)` - directory part of target
- `$(@F)` - file-within-directory part of target
- `%` - wildcard

- `include` - to include another Makefile (perhaps first defining some variables)

---

For knitr with vanilla-ish R:

```
R_OPTS=--no-save --no-restore --no-init-file --no-site-file # --vanilla, but without --no-environ
```

then:

```
R $(R_OPTS) -e 'library(knitr);knit2html("report.Rmd")'
```

---

`.PHONY` for indicating not-real targets; see <http://stackoverflow.com/a/7081747/897303>

example:

```
.PHONY: all jspanels jspaneltests jscharts json doc clean
```

---

### Examples

- [Makefile for Tools4RR Intro lecture](https://github.com/kbroman/Tools4RR/blob/master/01_Intro/Makefile)
- [Makefile template for Tools4RR lectures](https://github.com/kbroman/Tools4RR/blob/master/MakeSrc_lectures.mk)
- [qtlcharts](https://github.com/kbroman/qtlcharts/blob/master/Makefile)

## Notes on Mercurial (hg)

colored output: add to `~/.hgrc`: (see <mercurial.selenic.com/wiki/ColorExtension>)

    [extensions]
    color =

Commit just one file:

    hg commit filename


`.hgignore` file:

    syntax: glob
    *~
    *.html
    analysis/*.txt
    .\#*
    .Rhistory
    .RData

    syntax: regexp
    ^rawData$
    ^analysis/figure$
    ^data/markerFiles$

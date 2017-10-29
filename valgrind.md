## Notes on valgrind

valgrind installed via homebrew

    brew install valgrind

On `R CMD INSTALL`, need to use `--dsym` to include symbols in object
files, like so (aliased as `Rii`)

    R CMD INSTALL --dsym --library=/Users/kbroman/Rlibs

Then run valgrind like this:

    R -d "valgrind --tool=memcheck --leak-check=full --track-origins=yes --dsymutil=yes" --no-save < test_qtl.R >& out.txt

To run R CMD check with valgrind:

    R CMD check --use-valgrind

also need `~/.valgrindrc`; mine has:

    --tool=memcheck
    --leak-check=full
    --track-origins=yes
    --dsymutil=yes

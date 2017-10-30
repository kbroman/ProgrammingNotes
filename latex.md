## Latex on Mac

I installed the basic package for MacTex. (The full thing is like
3 GB; the basic one is like 300 MB.)

To update:

    sudo tlmgr update --self
    sudo tlmgr update --all

To install a package from CTAN:

    sudo tlmgr install enumitem

Error re `pcrr7t.tfm`:

    sudo tlmgr install courier  # install font package
    sudo texhash                # update distribution
    sudo updmap-sys             # update all font maps

**OH F*CK IT, JUST INSTALL THE FULL MACTEX**

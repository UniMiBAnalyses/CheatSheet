# Add external latex packages to TDR
If you are compiling CMS AN, Papers of PhD thesis with centrally proivided [TDR scripts](https://twiki.cern.ch/twiki/bin/viewauth/CMS/Internal/TdrProcessing) you will often find that packages are missing and you latex document is not compiled as you wanted to. For example these packages are not included
```
\usepackage{makecell}
\usepackage{booktabs,siunitx}
\usepackage{array,enumitem,booktabs,adjustbox}
\usepackage{units}
\usepackage{slashed,amsfonts,mathrsfs,bbm,bbding,pifont, fontawesome}
```

If you are sure you have them on your installed TeX distribution then it is not enough to declare `\usepackage` in you main .tex scripts as it will be totally ignored.
To add packages from your TeX distribution you show add the `\usepackage` in one of the following files depending on which type of document you are trying to compile:

```
utils/general/cms-tdr.cls
utils/general/cms-tdr-note.cls
utils/general/cms-tdr-atlas.cls
```

If you open one of them you will see multiple `\usepackage` declarations and you can add yours.

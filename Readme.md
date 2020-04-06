# gitpod-latex


#### Tex template for gitpod ####
Write tex with sophisticated cloud IDE.

## Introduction
Gitpod is a online IDE with the design similar to VS Code.
It supports the plugins for VS code.
So, you can write tex files with excellent editor online.
Start gitpod project by the following link.

https://gitpod.io/#https://github.com/moritanian/gitpod-latex

## How to compile
Latex commands are available in the gitpod project.
Start terminal (Terminal button -> New Terminal) and run command, for example:
```
> latexmk -f --pdf --quiet -output-directory=./workspace/ main.tex
```

or
use the plugin by the following steps.


### Use Latex Workshop plugin
You can install plugins by uploading .vsix file.
So, benefit linting and intellisense.

It seems that texlive is not added to the path env variable in the plugin environment for some reason (in the terminal, texlive commands are available) and auto-building (compile in saving the tex file) is failed.
One solution is using shell script to set PATH.
Add following lines to the Preference configuration (file -> Settings -> Open preference) and edit latexmk.sh if necessary.

```
{
     "latex-workshop.latex.recipes":[
    {
      "name": "latexmk 🔃",
      "tools": [
        "latexmk"
      ]
    }
  ],
  "latex-workshop.latex.tools":[
    {
      "name": "latexmk",
      "command": "./latexmk.sh",
      "args": [
        "-synctex=1",
        "-interaction=nonstopmode",
        "-file-line-error",
        "-pdf",
        "-outdir=%OUTDIR%",
        "%DOC%",
        "-f"
      ]
    }
  ],
  "latex-workshop.latex.outDir": ".workspace",
  "latex-workshop.latex.build.clearLog.everyRecipeStep.enabled": false,
  "latex-workshop.latex.recipe.default": "first",
}
```

At the present, syctex can not be used because the pdf file can not be opend by the plugin.

# LaTeX Template for a thesis

<!-- TOC -->

- [LaTeX Template for a thesis](#latex-template-for-a-thesis)
    - [Getting started](#getting-started)
        - [TeX Live](#tex-live)
        - [TeX Works](#tex-works)
        - [Compile the tex-file](#compile-the-tex-file)
        - [Biber](#biber)
    - [Project structure](#project-structure)
        - [Settings](#settings)
        - [Images](#images)
    - [KomaScript](#komascript)
    - [Literature](#literature)
        - [JabRef](#jabref)
        - [Cites and footnotes](#cites-and-footnotes)
        - [Listings](#listings)

<!-- /TOC -->

## Getting started
### TeX Live
Download the latest version of TeX Live from [here](https://www.tug.org/texlive/).
The installation can take a while, so be patient ;)

### TeX Works
The editor should be included in the TeX Live package. It is the [TeX Works editor](https://www.tug.org/texworks/). So you must not do something here.

### Compile the tex-file
Finally you want to see the template working so you need to open the file `thesis.tex` with the TeX Works editor.

On the top left you can press the green button to compile the template. Be sure that you select `pdfLaTeX` in the select box next to the green compile button.

Now the compiler should run without any errors and the preview of the PDF opens up.

The content of the table of contents or the list of figures are not rendered yet. You need to compile the template twice.

### Biber
As you may have noticed the footnote for the cites are not rendered yet very well. To compile the cites and the bibliography settings you need `biber`. You have to select the `biber`-compiler instead of the `pdfLaTeX` in the selection next to the green compiler button. 

**You cannot find `biber` there?**
You just have to set up the TeX Works editor that it shows the `biber`-compiler.
Go into the settings of TeX Works (under `Edit > Settings...`) and select the tab `Typesetting`. Under the point `Processing tools` click on the `+` and add `biber`. Name it 'Biber' and select the program under your installation folder of `texlive` (e.g. `C:/texlive/2015/bin/win32/biber.exe`). You have to add the argument `$basename` and uncheck the option to `view pdf after running`.

Now select `biber` in the dropdown list next to the compile button to run `biber`. After that you need to run `pdfLaTeX` again and then you should have the literature correctly in your template.

Did not get the configuration of `biber`? Look [here](http://www.edition-open-sources.org/support/texworks.html) for some screenshots. 

---

## Project structure
We have one main file called `thesis.tex` which can be found in the root folder. This file includes all the other files needed for the whole template. The content is splitted up into files which can be found in the folder `chapters`. 

### Settings
All settings are located under the `settings`-folder. 

### Images
All images are located under the `images`-folder. Because of the settings (`settings/graphics.tex`) we do not need the whole file path when we load an image into the content. You can just write the name of the image. 

Example:

```tex
\includegraphics{sample}
```

The 'real' image is located under `images/` and has the full file name `sample.jpeg`.

**Add image with caption**
The following code shows how to include an image in a `figure` environment. The image has a width of 100% of the page. If you want another width just change it, e.g. 300px. 
The caption of the image in the `[]` is the text that will be shown in the list of figures after the table of contents. The text in the `{}` is shown as title under the image.
With the label-text you can refer the image in the text with: `\ref{fig:imageYouCanReferTo} shows that...`.

```
\begin{figure}[h]
    \includegraphics[width=\textwidth, height=\textheight,keepaspectratio]{sample}
    \caption[Beispielbild (Abbildungsverzeichnis)]{Beispielbild} 
    \label{fig:imageYouCanReferTo}
\end{figure}
```

## KomaScript
The template uses the `KomaScript`-bundle. [Need more information?](https://www.ctan.org/pkg/koma-script?lang=de)

## Literature 
Big point for a thesis: how to handle the required literature and how to include cites into the thesis?

As you can see (`settings/bibliography.tex`) the template uses the package `biblatex`. In the settings file you need to include your resource files.

```tex
\addbibresource{sources/literature.bib}
```

As you can see in the example above we have already a literature file in the `sources`-folder with the following entry:

```
@Online{jondoe,
  author  = {Jon Doe},
  title   = {What do you think about Jon Doe},
  year    = {2016},
  url     = {https://de.wikipedia.org/wiki/John_Doe},
  urldate = {2016-10-02},
}
```

### JabRef
Wait! Do I need to update those entries every time manually? This can be really ugly over time. The solution is [JabRef](https://www.jabref.org/). JabRef is a small but very useful java application to handle our sources and to update the `.bib`-files in our `sources`-folder.

Download JabRef from the [website](https://www.jabref.org/) and open your `.bib`-files with it. Here you can update your sources easily.

### Cites and footnotes
How to use the sources in my content?

You need to know the keyword of your defined source of the `.bib`-file (in the example this is `jondoe`). Then write the following syntax to create a footnote in your thesis:

**Citation as footnote**

```tex
\footcite{jondoe}
``` 

**Harvard citation style**

If you prefer the harvard citation style (Doe, 2016) you should use the following commands:

```tex
\textcite{jondoe} % Doe (2016)
``` 

```tex
\parencite[vgl.][]{jondoe} % (vgl. Doe 2016)
\parencite[vgl.][7]{jondoe} % (vgl. Doe 2016, S. 7)
``` 

> Remember to compile your thesis with `biber` to render the cites correctly.

**Normal footnote**
If you want to add a normal footnote to add some further information:

```tex
\footnote{This is some additional information}
```

### Listings
The template provides some listings for `CSS`, `HTML` and `JavaScript`. You will find the definition of the listings under `settings/listings.tex`.

In the settings you have to define the language with its keywords and other needed options...

```tex
\lstdefinelanguage{HTML5}{...}
```

and then you also need to define a style to style the definition of the language...

```tex
\lstdefinestyle{html}{
    language=HTML5,
    ...
}
```

and use it in the content later...

```tex
\begin{lstlisting}[style=html, caption={ein paar Zeilen html}]
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>Document</title>
</head>
<body>
    
</body>
</html>
\end{lstlisting}
```

**Minted package**

Another very good package for listings is [minted](https://www.ctan.org/pkg/minted?lang=de).

**Inline listing**

For inline listings just use the custom command `\code{console.log()}`. This command is defined in the `settings/commands.tex`-file.
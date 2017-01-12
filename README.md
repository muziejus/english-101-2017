# English 101 2017

I am teaching “Introduction to the Study of Literature,” or “English 101,” in
the Spring of 2017 at NYU. 

This repository is an attempt to use
[MultiMarkdown](http://fletcher.github.io/MultiMarkdown-5/) in order to
generate both a [handsome
webpage](https://muziejus.github.io/english-101-2017/syllabus.html) and a
[handsome pdf](https://muziejus.github.io/english-101-2017/syllabus.pdf) of the
syllabus at the same time. This is (not) surprisingly rather tricky. However,
this is also a template for future syllabi, and I encourage others to tweak
this work.

## Structure

The main file in this syllabus is `syllabus.mmd`. This is a MultiMarkdown file
setting all of the metadata and building up the structure of the syllabus. Very
little actual text is in this file, as that is all delegated to the files in
the folder `sections/`.

The metadata include calls to three LaTeX files (available in
`latex-support/`), but it also has an `html header` and `html footer` set,
which provide html-specific text that gets skipped for LaTeX. Most importantly,
at the end of `html footer`, there are a few jQuery commands that go back
through the html as it exists and fill in text strings.

## Usage

```
git clone https://github.com/muziejus/english-101-2017.git
cd english-101-2017
mmd syllabus.mmd
mmd2tex syllabus.mmd
sh process-mmd.sh
biber syllabus
xelatex syllabus.tex ; xelatex syllabus.tex
```

`mmd` is MultiMarkdown. Fletcher Penney describes how to install it [on the
official site](http://fletcher.github.io/MultiMarkdown-5/installation.html),
but for Mac, assuming you have homebrew installed, it’s as easy as:

```
brew install --HEAD multimarkdown
```

A new version of `mmd` is required, because functionality like `html footer` is
a recent addition.

`process-mmd.sh` is a shell script that adds a little more post-processing
to the tex file, like suppressing section numbering and cleaning up
MultiMarkdown’s best guess at how to handle slashes.

`xelatex` is [XeLaTeX](https://en.wikipedia.org/wiki/XeTeX). It is installed as
part of [TeX Live](https://www.tug.org/texlive/) and/or
[MacTeX](https://tug.org/mactex). `biber` is
[biber](http://biblatex-biber.sourceforge.net/), a replacement for BibTeX and
formats the bibliography for the printed version of the document.

## The html version

`mmd syllabus.mmd` creates a file, `syllabus.html`, which is a self-contained
version of the syllabus, styled with [Bootstrap](http://getbootstrap.com). As a
result, it has a pleasant, generic look, a functioning navbar, responsive
layout, and a spy that updates the navbar based on where you are scrolling. The
navbar is built in `sections/navbar.html`, and it is only transcluded when
outputting to html. However, traces of its presence remain when outputting to
TeX. 

Some html-specific stuff is done in the metadata, but the html version cannot
make use of the metadata in the same way the TeX version can. As a result, the
navbar and jQuery commands in `html footer` might need to be edited by hand.

## The TeX/pdf version

The pdf version is generated by XeLaTeX, as noted above. XeLaTeX uses the
[fontspec](http://ctan.org/pkg/fontspec) package to set its fonts. In this
repository, the fonts are set explicitly in `latex-support/second-header.tex`.
If you don’t have [EB
Garamond](https://www.google.com/fonts/specimen/EB+Garamond) or
[DejaVu](http://dejavu-fonts.org/wiki/Main_Page) installed, XeLaTeX will throw
a fit. Of course, you could comment out those lines from
`latex-support/second-header.tex` or install the fonts. They are free.

The bibliography is built using a `.bib` file and `Biber`. Explaining hot to
build that is way beyond the scope of this document.

## Issues / roadmap

This works exactly as I want it to. Any more messing about will simply go into
the post-processing script, possibly including a wrapper script that performs
all of the commands. 

The Bibliography support can be formalized, but as far as I can tell, there’s
no clean way to make an html bibliography out of BibTeX/Biber, so it might get
put off for a later time.

## Credits

This is a large reworking of a previous syllabus for a course I taught at NYU,
“[Does It Work?](https://github.com/muziejus/does-it-work)” in autumn 2016.

In order to get the syllabus to sound “NYUish,” I copied (sometimes very
heavily) from a syllabus prepared by my colleague at NYU, [Jini
Watson](http://english.fas.nyu.edu/object/JiniWatson.html). She was also
helpful in giving me a sense of what kinds of assignments and homework students
could expect at this university. Useful info for someone who’s not taught in a
US context in over half a decade!

The specific parameters of the English 101 course were greatly enhanced by
syllabi for the same course designed by Carla María Thomas and Rachael Michelle
Wilson. The three of us, along with Elizabeth McHenry and Simón Trujillo, are
the band of five teaching this new course in Spring 2017, and our lengthy email
chain has also influenced this document.

The bravery to create a `LaTeX` syllabus using the `memoir` class was fueled by
Kieran Healy’s [custom LaTeX
templates](http://kjhealy.github.com/latex-custom-kjh). I’ve greatly simplified
his setup, however.

This structure of this GitHub syllabus was once based on Mark Sample's
[Videogame Studies](https://github.com/samplereality/videogame-studies)
syllabus, in how it is presented on GitHub. 

If you would like to know more about GitHub and syllabi, here are a few
ProfHacker articles:

* [Forking Your Syllabus](http://chronicle.com/blogs/profhacker/forking-your-syllabus/39137) (22 March 2012)
* [How to Fork a Syllabus on GitHub](http://chronicle.com/blogs/profhacker/how-to-fork-a-syllabus-on-github/39447) (12 April 2012)
* [Git a Fork in My Syllabus, It’s Done](https://chronicle.com/blogs/profhacker/git-a-fork-in-my-syllabus-its-done/40331) (5 June 2012)

## License

English 101 2017 by [Moacir P. de Sá Pereira](http://moacir.com) is licensed
under a [Creative Commons Attribution-NonCommercial-ShareAlike 3.0 Unported
License](http://creativecommons.org/licenses/by-nc-sa/3.0/). To view a copy of
this license, visit
[http://creativecommons.org/licenses/by-nc-sa/3.0/](http://creativecommons.org/licenses/by-nc-sa/3.0/)

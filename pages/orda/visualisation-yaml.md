---
title: How to specify visualisation metadata
---

To include your visualisation in the [showcase on ORDA][showcase], you will need to upload a simple file describing to ORDA how to access it. This file *must* be called `visualisation.yaml`, and the rest of this guide describes the content of that file.

*Please note: while currently you need to build a `visualisation.yaml` file manually, we are developing tools to make this much easier.*

!!! contents
    [TOC]

## Prerequisites

You'll need a text editor to create/edit your `visualisation.yaml` file. If you have written the visualisation yourself in a programming language, the same editor you used for that will allow you to edit a `.yaml` file. Otherwise:

- Windows: [Microsoft Notepad][Notepad] is included with all Microsoft Windows versions
- MacOS: [TextEdit][] is included with all MacOS versions
- Linux: A number of text editors are available, including [gedit][] (part of GNOME desktop) and [Kate][] (part of KDE desktop) — try searching your menu for "text editor"

## Describing your visualisation

Let's take a look at a whole example, then break it down into its component parts:

```yaml
---
visualisations:
  - url: https://plot.ly/jezcope/5.embed
    type: embed
```

This describes an embedded visualisation available at the URL `https://plot.ly/jezcope/5.embed`. Note that the indentation is important, as ORDA uses this to interpret the structure of the file. It begins with two lines which *must* be present in every `visualisation.yaml` file:

```yaml
---
visualisations:
```

The next line begins the description of a single visualisation, and gives the URL used to access the visualisation:

```yaml
  - url: https://plot.ly/jezcope/5.embed
```

Many online tools (including plot.ly) will let you obtain a special URL for embedding

The next line specifies the type of visualisation. There are two options for this:

- `embed`: The visualisation will be embedded in its own page on ORDA that also shows important information, such as the title, description, creators and a link to the dataset. This option is strongly recommended.
- `link`: For this type, clicking on the thumbnail in the showcase will cause the visitor's browser to open your visualisation in a new tab or window. This is recommended only for tools, such as Google Sites, which do not permit embedding.

```yaml
    type: embed
```

## Optional information

Some information is optional; if it's not specified, the showcase will instead take the information from the ORDA record. This includes the title, description, creators and a link to the source code. This is especially useful when the information for the visualisation is slightly different from the dataset (e.g. different creators). You include this information by adding extra lines in your file, or omit them if you're not using them:

```yaml
---
visualisations:
  - url: https://example.com/visualisation/1.embed
    type: embed
    title: The half-life of thorium
    creators:
    - Marie Skłodowska Curie
    - Pierre Curie
    description: Experimental measurements of the half-life of thorium samples over time.
    thumbnail: https://example.com/visualisation/1.thumbnail.png
    source_code: https://github.com/example/visualisation
```

## More than one visualisation

It is not possible to upload more than one `visualisation.yaml` file for a single dataset. If you have more than one visualisation for a single dataset, you can specify all of them in a single file by repeating the `- url: …` line to start a new entry. It's strongly recommended to include at least the `title:` optional field to help visitors tell the visualisations apart:

```yaml
---
visualisations:
  - url: https://plot.ly/jezcope/5.embed
    type: embed
  - url: https://plot.ly/jezcope/6.embed
    type: embed
    title: An alternative view of the experimental data
```


## Other tips

#### Comments

You can include notes to yourself in the file as comments. Anything from a `#` to the end of a line will be ignored. For example:

```yaml
---
# This whole line will be ignored
visualisations:
  - url: "https://plot.ly/jezcope/5.embed"
    type: embed # The text after the first # on this line is also ignored
```
      
#### YAML

The file format used for describing visualisations is called [YAML][]. It is a general purpose file format for storing information in a format that is both human- and computer-readable and can be used with most programming languages. It's therefore ideal for specifying configuration and metadata to your own software and scripts. Learn more at <http://yaml.org/>.

- - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - -



[showcase]: https://orda.shef.ac.uk/visualisations/
[Notepad]: https://en.wikipedia.org/wiki/Microsoft_Notepad
[TextEdit]: https://en.wikipedia.org/wiki/TextEdit
[gedit]: https://wiki.gnome.org/Apps/Gedit
[Kate]: https://kate-editor.org/
[YAML]: https://en.wikipedia.org/wiki/YAML

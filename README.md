# NI Raspberry Jam Worksheet Creator

Repo with setup guide and resources for converting Markdown to PDF for worksheets.

Due to the hard work of others I was able to put this together, attributes given where necessary + thanks to countless stack overflow posts.

## Setup

A few things to get done before starting.

### Software

For this system you need to install a few programs...
- Pandas
  - the program that handles all of the backbone for converting from one form to another
  - Found here https://pandoc.org/installing.html
- wkhtmltopdf
  - The engine that's used to specifically convert the Markdown to HTML (In the background) and then to PDF
  - Found here https://wkhtmltopdf.org/downloads.html

Install them from the official links above.

### Stylesheets

We use a slightly modified version of GitHub Flavoured Markdown when converting to PDF. The original being available [here](https://gist.github.com/tuzz/3331384). However, **we use the version in this repo** as it has a few modifications to match our worksheet style.

To copy it you can either
- Copy the raw version of the stylesheet from this repo and place anywhere
- Clone this repo which will also copy these instructions with it

## Usage

In short, copy and run this

```bash
pandoc \
-f markdown \
-t html5 \
--metadata pagetitle="Worksheet" \
-V margin-left=0.5cm \
-V margin-right=0.5cm \
-V margin-top=0.5cm \
-V margin-bottom=1cm \
-V paper-size=A4 \
--pdf-engine=wkhtmltopdf \
--pdf-engine-opt="--footer-right" --pdf-engine-opt="Page [page] of [topage]" \
--css ./github-markdown.css \
-o Worksheet.pdf \
Worksheet.md
```

Here's what's going on...
- `pandoc` Use pandoc,
- `-f markdown` with markdown being the format of choice,
- `-t html5` to be converted to HTML5,
- `--metadata pagetitle="Worksheet"` with the webpage title being "Worksheet",
  - Not explicitly needed but stops a message from being outputted each time
- `-V margin-left=0.5cm` setting wkhtmltopdf's margin-left variable to 0.5cm,
- `-V margin-right=0.5cm` setting wkhtmltopdf's margin-right variable to 0.5cm,
- `-V margin-top=0.5cm` setting wkhtmltopdf's margin-top variable to 0.5cm,
- `-V margin-bottom=1cm` setting wkhtmltopdf's margin-bottom variable to 1cm,
- `-V paper-size=A4` setting wkhtmltopdf's output PDF paper size variable to A4,
- `--pdf-engine=wkhtmltopdf` using "wkhtmltopdf" as the conversion engine,
- `--pdf-engine-opt="--footer-right" --pdf-engine-opt="Page [page] of [topage]"` putting page number in bottom right corner,
- `--css ./github-markdown.css` apply "github-markdown.css" stylesheet when converting,
- `-o Worksheet.pdf` output the file as "Worksheet.pdf,
- `Worksheet.md` convert "Worksheet.md"

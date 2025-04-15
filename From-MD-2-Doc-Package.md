# From Markdown to a Document Package

This brief note explains current (as of April 2025) procedures for creating a
document package starting from a Markdown document and associated files in a
GitHub repository. The output is a compressed document package with Markdown,
HTML, and PDF versions for upload to OASIS



## Starting Point

This process assumes the availability of

- the focus document in Github-Flavored Markdown (GFM) format
- any graphics needed for the document, typically in PNG or JPEG format
- a CSS file that defines OASIS-aligned formatting
- [`pandoc`](https://pandoc.org/), a FOSS document format conversion tool (or other utility for converting GFM to HTML)
- Google Chrome or another Chromium-based browser (note that this process has only been tested with Chrome)

The TC Operations repository includes a suitable CSS file as a starting point in the `styles` folder.

## Process Overview

The process has the following steps:

1. Declare a Github Release corresponding to the desired version of the focus document
2. Download the compressed file for the release and extract to a working folder
3. Create an HTML version from the Markdown file to HTML using `pandoc` and a suitable CSS file
4. Review the HTML file for correctness and make any needed adjustments
5. Create a PDF version using Chrome's `Save as PDF` feature
6. Delete extraneous files from the working folder
7. Create an archive file containing the three versions plus a folder of image
   files and, as needed, other folders with associated file (e.g., schemas)

## 1) Declare a Github Release

The GitHub [Release](https://docs.github.com/en/repositories/releasing-projects-on-github/managing-releases-in-a-repository)
feature is used to establish a precise checkpoint for the document version. It
is assumed that the administrative information (date, TOC, tables of figures and
tables, etc.) have been addressed in the editing process, formatting tweaks such
as removal of unneeded page break lines have been applied, and that the desired
document version and associated files are in the working branch of the OASIS
repository for the document.

Key items to address when creating the release:

- Craft a suitable tag value to be applied; for example `v2-csd01-candidate`
- Ensure that the **Target** for the release is the working branch
- Provide a descriptive title; for example "v2.0 CSD01 Candidate (YYYY-MM-DD)"
where the date is the TC meeting date where approval is expected or the date the
editor is applying to a CSD release (per the relevant standing rule in the OASIS
[_Document Life Cycle Best Practices_](https://www.oasis-open.org/policies-guidelines/document-life-cycle-best-practices/),
if the TC has adopted that rule)
- Provide an overview of changes in this version
- Use the Generate Release Notes feature to capture a list of the specific PRs
  that have been applied (this is most useful if the PRs have informative names)

## 2) Download the compressed file

Declaring a release on GitHub triggers the creation of **Assets** that include
`zip` and `tar.gz` versions of the content of the target branch as of the time the
release is created. Download the appropriate format for your operating system of
choice, and extract all of its contents to a working folder. Files from the
download will be, approximately:

```
\images
\styles
\other-file-folders
doc_name.md
other-documents.md
```

## 3) Create an HTML version

Use a document conversion tool to create an HTML version from the GFM
(`doc_name.md`) version of the document. This process description assumes that
the FOSS `pandoc` tool is being used.  The important parameters for the `pandoc`
command line are:

```
1) \pandoc\pandoc 
2)  -f gfm -t html
3)  --css=file://<path-to-working-folder>\styles\markdown-styles-2025-template-dk-page.css
4)  --include-in-header=<path-to-working-folder>\styles\markdown-styles-2025-template-dk-page.css
5)  -s
6)  -o doc_name.html  
7)  doc_name.md
```

Explanations:

1. The program invocation with any needed path
2. The source (`-f`) and destination (`-t`) file formats
3. The CSS file to style the HTML output
4. Directive to embed the CSS file in the HTML output header, per OASIS guidance to not require external CSS
5. Directive to produce a standalone CSS file
6. The output file name
7. The input file name

It is important that the CSS file contents have a `<style> ... </style>`
wrapper in order for its contents to be properly embedded in the HTML output.
The `pandoc` [User's Guide](https://pandoc.org/MANUAL.html) provides
explanations of all of the parameters.

## 4) Review the HTML Output

Open the newly created `doc_name.html` file in a browser to review the output.
Some tweaking of the GFM source or the CSS may be necessary to achieved the
desired formatting. Any changes made at this point must be purely editorial and
should also be applied to the repository working branch to simplify producing
document packages for subsequent versions.

## 5) Create a PDF Version

The CSS file provided includes formatting directives to produce a page numbered
PDF styled to match the HTML version. To create this output, invoke the Print
function from the Chrome menu (or use `ctrl-p`), and select `Save as PDF` as the
Destination. Other settings can be checked to confirm that the output appears as
desired. Save the PDF to the same folder as the GFM and HTML versions as `doc_name.pdf`.

## 6) Delete extraneous files

The OASIS document package only needs the three versions of the document (GFM,
HTML, PDF), the `images` folder, and any folders containing essential material
for the package (e.g., schemas, source code). All other files and folders can be
deleted.

## 7) Create a compressed file

Use a document compression capability in a file manager or stand-alone utility
to create an archive with all of the required files (e.g., in Windows,
right-click on `doc_name.md` and select *Send To*, then *Compressed (zipped)
folder*). The resulting file (e.g., `doc_name.zip`) is suitable for upload to
OASIS.
[![Binder](https://mybinder.org/badge_logo.svg)](https://mybinder.org/v2/gh/fsprojects/FSharp.Formatting/gh-pages?filepath=literate.ipynb)

# Creating Content

The ["fsdocs" tool](commandline.html) allows documentation for a site to be built
from content in a `docs` directory. The expected structure for a `docs` directory is

// can't yet format InlineBlock ("docs/**/*.md                  -- markdown with embedded code, converted to html and optionally tex/ipynb
docs/**/*.fsx                 -- fsx scripts converted to html and optionally tex/ipynb
docs/**/*                     -- other content, copied over
docs/**/_template.html        -- optional template, specifies the HTML template for this directory and its contents
docs/**/_template.tex         -- optionally indicates Latex files should be generated
docs/**/_template.ipynb       -- optionally indicates F# ipynb files should be generated
docs/**/_template.fsx         -- optionally indicates F# fsx files should be generated (even from markdown)
docs/reference/_template.html -- optionally specifies the default template for reference docs
", None, None) to pynb markdown

Processing is by these two commands:

// can't yet format InlineBlock ("dotnet fsdocs build
dotnet fsdocs watch
", None, None) to pynb markdown

The output goes in `output/` by default.  Processing is recursive, making this a form of static site generation.

## Literate Scripts and Markdown

The input directory may contain [literate scripts and markdown](literate.html).

## Other Content

Content that is not `*.fsx` or `*.md` is copied across.

## Default Styling Content

By default additional content such as `fsdocs-search.js`, `fsdocs-tips.js` and `fsdocs-styles.css` are included in the
the `content` directory of the output.  This can be suppressed with `--nodefaultcontent` or by having your own
copy of this content in your `content` directory.

## Ignored Content

Any file or directory beginning with `.` is ignored.

## Multi-language Content

Versions of content in other languages should go in two-letter coded sub-directories, e.g.

// can't yet format InlineBlock ("docs/ja/...
docs/de/...
", None, None) to pynb markdown

These will be elided from the main table-of-contents and search indexes.  (Currently no language-specific
table of contents is built, nor language-specific site search indexes).

## HTML Templates

Template files are named `_template.html` and should contain `{{fsdocs-content}}`,  `{{fsdocs-tooltips}}`
and other placeholders.
If a file `_template.html` exists then is used as the template for HTML generation for that directory and all sub-content.
Otherwise the default template is used.

The following substitutions determine the primary (non-styling) content of your site.
For example `{{fsdocs-content}}` is replaced with the generated content.

See [Styling](styling.html) for information about template parameters and styling beyond the default template.

Substitution name | Generated content
:--- | :---
`root` | `<PackageProjectUrl>` else `/` followed by `fsdocs-collection-name`
`fsdocs-collection-name` | Name of .sln, single .fsproj or containing directory
`fsdocs-content` | Main page content
`fsdocs-list-of-namespaces` | HTML `<li>` list of namespaces with links
`fsdocs-list-of-documents` | HTML `<li>` list of documents with  titles and links
`fsdocs-page-title` | First h1 heading in literate file. Generated for API docs
`fsdocs-source` | Original literate script or markdown source
`fsdocs-tooltips` | Generated hidden div elements for tooltips
`fsdocs-watch-script` | The websocket script used in watch mode to trigger hot reload


The following substitutions are extracted from your project files and may or may not be used by the default
template:

Substitution name | Value
:--- | :---
`fsdocs-copyright` | `<Copyright>`
`fsdocs-package-project-url` | `<PackageProjectUrl>`
`fsdocs-package-license-expression` | `<PackageLicenseExpression>`
`fsdocs-package-tags` | `<PackageTags>`
`fsdocs-package-version` | `<Version>`


## Generating LaTeX output

To generate .tex output for each script and markdown file, add a `_template.tex`.

It is either empty of contains `{{fsdocs-content}}` as the key where the body
of the document is placed.

## Generating iPython Notebook output

To generate .ipynb output for each script and markdown file, add a `_template.ipynb`, usually empty.

To add a `mybinder` badge to your generated notebook, ensure you have a `Dockerfile` and `NuGet.config`
in your `docs` directory and use text like this:

// can't yet format InlineBlock ("[![Binder](https://mybinder.org/badge_logo.svg)](https://mybinder.org/v2/gh/fsprojects/FSharp.Formatting/gh-pages?filepath=literate.ipynb)
", None, None) to pynb markdown

## Generating Script outputs

To generate .fsx output for each script and markdown file, add a `_template.fsx`, usually empty.
It may contain `{{fsdocs-content}}`.



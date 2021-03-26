# Customization and Styling

When using `fsdocs`, there are six levels of extra content development and styling.

// can't yet format ListBlock (Ordered, [[Paragraph ([Literal ("Don't do any styling or documentation customization and simply write content.  This is by far the simplest option to maintain.", Some { StartLine = 0 StartColumn = 0 EndLine = 0 EndColumn = 126 })], Some { StartLine = 0 StartColumn = 0 EndLine = 0 EndColumn = 0 })]; [Paragraph ([Literal ("Add content such as an ", Some { StartLine = 0 StartColumn = 0 EndLine = 10 EndColumn = 23 }); InlineCode ("docs/index.md", Some { StartLine = 0 StartColumn = 24 EndLine = 10 EndColumn = 20 }); Literal (" to customize the front-page content for your generated docs.
You can also add content such as ", Some { StartLine = 0 StartColumn = 23 EndLine = 10 EndColumn = 118 }); InlineCode ("docs/reference/fslib.md", Some { StartLine = 0 StartColumn = 119 EndLine = 10 EndColumn = 20 }); Literal (" to give a bespoke landing page
for one of your namespaces, e.g. here assumed to be ", Some { StartLine = 0 StartColumn = 118 EndLine = 10 EndColumn = 202 }); InlineCode ("namespace FsLib", Some { StartLine = 0 StartColumn = 203 EndLine = 10 EndColumn = 20 }); Literal (".  This will override any
generated content.", Some { StartLine = 0 StartColumn = 202 EndLine = 10 EndColumn = 246 })], Some { StartLine = 0 StartColumn = 0 EndLine = 0 EndColumn = 0 })]; [Paragraph ([Literal ("Customize via Styling Parameters", Some { StartLine = 0 StartColumn = 0 EndLine = 0 EndColumn = 32 })], Some { StartLine = 0 StartColumn = 0 EndLine = 0 EndColumn = 0 })]; [Paragraph ([Literal ("Customize via CSS", Some { StartLine = 0 StartColumn = 0 EndLine = 0 EndColumn = 17 })], Some { StartLine = 0 StartColumn = 0 EndLine = 0 EndColumn = 0 })]; [Paragraph ([Literal ("Customize via a new template", Some { StartLine = 0 StartColumn = 0 EndLine = 0 EndColumn = 28 })], Some { StartLine = 0 StartColumn = 0 EndLine = 0 EndColumn = 0 })]; [Paragraph ([Literal ("Customize by generating your own site using your own code", Some { StartLine = 0 StartColumn = 0 EndLine = 0 EndColumn = 57 })], Some { StartLine = 0 StartColumn = 0 EndLine = 0 EndColumn = 0 })]], Some { StartLine = 5 StartColumn = 0 EndLine = 5 EndColumn = 129 }) to pynb markdown

By default `fsdocs` does no styling customization and uses the following defaults. These are the settings used to build this site.

Uses the default template in [docs/_template.html](https://github.com/fsprojects/FSharp.Formatting/blob/master/docs/_template.html)
Uses the default styles in [docs/content/fsdocs-default.css](https://github.com/fsprojects/FSharp.Formatting/blob/master/docs/content/fsdocs-default.css).
Uses no custom styles in [docs/content/fsdocs-custom.css](https://github.com/fsprojects/FSharp.Formatting/blob/master/docs/content/fsdocs-default.css).
Uses no styling parameters except those extracted from the project files.
For your project, you don't need any of these files. However you can add them if you wish, though if
you adjust them there is no guarantee that your template will continue to work with future versions of F# Formatting.

## Customizing via Styling Parameters

The following [content parameters](content.html) are particularly related to visual styling:

Substitution name | Value (if not overriden by --parameters)
:--- | :---
`fsdocs-authors` | `<Authors>`
`fsdocs-collection-name-link` | `<FsDocsCollectionNameLink>`
`fsdocs-license-link` | `<FsDocsLicenseLink>`
`fsdocs-logo-src` | `<FsDocsLogoSource>`
`fsdocs-logo-link` | `<FsDocsLogoLink>`
`fsdocs-navbar-position` | `<FsDocsNavbarPosition>` (`fixed-left` or `fixed-right`)
`fsdocs-release-notes-link` | `<FsDocsReleaseNotesLink>` else `<PackageProjectUrl>/blob/master/RELEASE_NOTES.md`
`fsdocs-repository-link` | `<RepositoryUrl>`
`fsdocs-theme` | `<FsDocsTheme>`, must currently be `default`


These basic entry-level styling parameters can be set in the project file or `Directory.Build.props`.
For example:

// can't yet format InlineBlock ("    <!-- Example ultra-simple styling and generation settings for FsDocs default template-->
    <PackageLicenseUrl>https://github.com/foo/bar/blob/master/License.txt</PackageLicenseUrl>
    <PackageProjectUrl>https://foo.github.io/bar/</PackageProjectUrl>
    <RepositoryUrl>https://github.com/foo/bar/</RepositoryUrl>
    <FsDocsLogoLink>https://fsharp.org</FsDocsLogoLink>
    <FsDocsLicenseLink>https://github.com/foo/bar/blob/master/License.txt</FsDocsLicenseLink>
    <FsDocsReleaseNotesLink>https://github.com/foo/bar/blob/master/release-notes.md</FsDocsReleaseNotesLink>
    <FsDocsNavbarPosition>fixed-left</FsDocsNavbarPosition>
    <FsDocsWarnOnMissingDocs>true</FsDocsWarnOnMissingDocs>
    <FsDocsTheme>default</FsDocsTheme>
", None, None) to pynb markdown

As an example, here is [a page with `fsdocs-navbar-position` set to `fixed-left`](templates/leftside/styling.html).

## Customizing via CSS

You can start styling by creating a file `docs/fsdocs-custom.css` and adding entries to it.  It is loaded by
the standard template.  The CSS classes of generated content are:

CSS class | Corresponding Content
:--- | :---
`.fsdocs-tip` | generated tooltips
`.fsdocs-member-list` | generated member lists
`.fsdocs-member-name` | generated member names
`.fsdocs-member-tooltip` | generated tooltips for members
`.fsdocs-xmldoc` | generated xmldoc sections
`.fsdocs-entity-list` | generated entity lists
`.fsdocs-exception-list` | generated exception lists
`.fsdocs-summary` | the 'summary' section of an XML doc
`.fsdocs-remarks` | the 'remarks' section of an XML doc
`.fsdocs-params` | the 'parameters' section of an XML doc
`.fsdocs-param` | a 'parameter' section of an XML doc
`.fsdocs-param-name` | a 'parameter' name of an XML doc
`.fsdocs-returns` | the 'returns' section of an XML doc
`.fsdocs-example` | the 'example' section of an XML doc
`.fsdocs-note` | the 'notes' section of an XML doc
`.fsdocs-para` | a paragraph of an XML doc


Some generated elements are given specific HTML ids:

HTML Element Id | Content
:--- | :---
`#fsdocs-content` | The generated content
`#fsdocs-searchbox` | The search box
`#fsdocs-logo` | The logo
`#fsdocs-menu` | The navigation-bar


If you write a new theme by CSS styling please contribute it back to FSharp.Formatting.

## Customizing via a new template

You can do advanced styling by creating a new template.  Add a file `docs/_template.html`, likely starting
with the existing default template.

To enable hot reload during development with `fsdocs watch` in a custom `_template.html` file, make sure to add the following line to your `<head>` tag:

// can't yet format InlineBlock ("{{fsdocs-watch-script}}
", None, None) to pynb markdown

// can't yet format QuotedBlock ([Paragraph ([Literal ("NOTE: There is no guarantee that your template will continue to work with future versions of F# Formatting.
If you do develop a good template please consider contributing it back to F# Formatting.", Some { StartLine = 113 StartColumn = 2 EndLine = 114 EndColumn = 198 })], Some { StartLine = 113 StartColumn = 2 EndLine = 113 EndColumn = 109 })], Some { StartLine = 113 StartColumn = 0 EndLine = 113 EndColumn = 109 }) to pynb markdown

## Customizing by generating your own site using your own code

The `FSharp.Formatting.ApiDocs` namespace includes a `GenerateModel` that captures
the results of documentation preparation in `ApiDocsModel` and allows you to
generate your own site using your own code.

// can't yet format QuotedBlock ([Paragraph ([Literal ("NOTE: The ApiDocsModel API is undergoing change and improvement and there is no guarantee that your bespoke site generation will continue to work
with future versions of F# Formatting.
NOTE: The ", Some { StartLine = 123 StartColumn = 2 EndLine = 127 EndColumn = 197 }); InlineCode ("ApiDocsModel", Some { StartLine = 123 StartColumn = 198 EndLine = 127 EndColumn = 73 }); Literal (" currently includes some generated HTML with some specific style tags.
In the long term these may be removed from the design of that component.", Some { StartLine = 123 StartColumn = 197 EndLine = 127 EndColumn = 340 })], Some { StartLine = 123 StartColumn = 2 EndLine = 123 EndColumn = 147 })], Some { StartLine = 123 StartColumn = 0 EndLine = 123 EndColumn = 147 }) to pynb markdown



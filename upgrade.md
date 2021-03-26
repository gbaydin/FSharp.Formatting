# Upgrading to fsdocs

Here are the typical steps to upgrade a repo based on `ProjectScaffold` to use `fsdocs`

// can't yet format ListBlock (Ordered, [[Paragraph ([Literal ("Run", Some { StartLine = 0 StartColumn = 0 EndLine = 0 EndColumn = 3 })], Some { StartLine = 0 StartColumn = 0 EndLine = 0 EndColumn = 0 }); InlineBlock ("dotnet new tool
dotnet tool install FSharp.Formatting.CommandTool
", None, None)]; [Paragraph ([Literal ("Delete all of ", Some { StartLine = 0 StartColumn = 0 EndLine = 0 EndColumn = 14 }); InlineCode ("docs\tools", Some { StartLine = 0 StartColumn = 15 EndLine = 0 EndColumn = -1 }); Literal (" particularly ", Some { StartLine = 0 StartColumn = 14 EndLine = 0 EndColumn = 28 }); InlineCode ("docs\tool\generate.fsx", Some { StartLine = 0 StartColumn = 29 EndLine = 0 EndColumn = -1 }); Literal (".  Keep a copy of any templates for reference as you'll have to copy some bits across to the new template.", Some { StartLine = 0 StartColumn = 28 EndLine = 0 EndColumn = 134 })], Some { StartLine = 0 StartColumn = 0 EndLine = 0 EndColumn = 0 })]; [Paragraph ([Literal ("Put your docs directory so it reflects the final shape of the site. For example move the content of ", Some { StartLine = 0 StartColumn = 0 EndLine = 0 EndColumn = 100 }); InlineCode ("docs\input\*", Some { StartLine = 0 StartColumn = 101 EndLine = 0 EndColumn = -1 }); Literal (" and ", Some { StartLine = 0 StartColumn = 100 EndLine = 0 EndColumn = 105 }); InlineCode ("docs\files\*", Some { StartLine = 0 StartColumn = 106 EndLine = 0 EndColumn = -1 }); Literal (" directly to ", Some { StartLine = 0 StartColumn = 105 EndLine = 0 EndColumn = 118 }); InlineCode ("docs\*", Some { StartLine = 0 StartColumn = 119 EndLine = 0 EndColumn = -1 })], Some { StartLine = 0 StartColumn = 0 EndLine = 0 EndColumn = 0 })]; [Paragraph ([Literal ("Follow the notes in ", Some { StartLine = 0 StartColumn = 0 EndLine = 0 EndColumn = 20 }); DirectLink ([Literal ("styling", Some { StartLine = 0 StartColumn = 20 EndLine = 0 EndColumn = 27 })], "styling.html", None, Some { StartLine = 0 StartColumn = 20 EndLine = 0 EndColumn = 0 }); Literal (" to start to style your site.", Some { StartLine = 0 StartColumn = 20 EndLine = 0 EndColumn = 49 })], Some { StartLine = 0 StartColumn = 0 EndLine = 0 EndColumn = 0 })]; [Paragraph ([Literal ("Run", Some { StartLine = 0 StartColumn = 0 EndLine = 0 EndColumn = 3 })], Some { StartLine = 0 StartColumn = 0 EndLine = 0 EndColumn = 0 }); InlineBlock ("dotnet fsdocs watch
", None, None); Paragraph ([Literal ("and edit and test your docs.", Some { StartLine = 24 StartColumn = 3 EndLine = 24 EndColumn = 31 })], Some { StartLine = 24 StartColumn = 3 EndLine = 24 EndColumn = 31 })]; [Paragraph ([Literal ("If using FAKE adjust ", Some { StartLine = 0 StartColumn = 0 EndLine = 0 EndColumn = 21 }); InlineCode ("build.fsx", Some { StartLine = 0 StartColumn = 22 EndLine = 0 EndColumn = -1 }); Literal (" e.g.", Some { StartLine = 0 StartColumn = 21 EndLine = 0 EndColumn = 26 })], Some { StartLine = 0 StartColumn = 0 EndLine = 0 EndColumn = 0 }); InlineBlock ("Target.create "GenerateDocs" (fun _ ->
   Shell.cleanDir ".fsdocs"
   DotNet.exec id "fsdocs" "build --clean" |> ignore
)

Target.create "ReleaseDocs" (fun _ ->
    Git.Repository.clone "" projectRepo "temp/gh-pages"
    Git.Branches.checkoutBranch "temp/gh-pages" "gh-pages"
    Shell.copyRecursive "output" "temp/gh-pages" true |> printfn "%A"
    Git.CommandHelper.runSimpleGitCommand "temp/gh-pages" "add ." |> printfn "%s"
    let cmd = sprintf """commit -a -m "Update generated documentation for version %s""" release.NugetVersion
    Git.CommandHelper.runSimpleGitCommand "temp/gh-pages" cmd |> printfn "%s"
    Git.Branches.push "temp/gh-pages"
)
", None, None)]; [Paragraph ([Literal ("Consider creating ", Some { StartLine = 0 StartColumn = 0 EndLine = 0 EndColumn = 18 }); InlineCode ("docs\_template.fsx", Some { StartLine = 0 StartColumn = 19 EndLine = 0 EndColumn = -1 }); Literal (" and ", Some { StartLine = 0 StartColumn = 18 EndLine = 0 EndColumn = 23 }); InlineCode ("docs\_template.ipynb", Some { StartLine = 0 StartColumn = 24 EndLine = 0 EndColumn = -1 }); Literal (" to enable co-generation of F# scripts and F# notebooks.", Some { StartLine = 0 StartColumn = 23 EndLine = 0 EndColumn = 79 })], Some { StartLine = 0 StartColumn = 0 EndLine = 0 EndColumn = 0 }); Paragraph ([Literal ("If you add support for notebooks and scripts, consider adding mybinder links to each of your literate executable content pages. ", Some { StartLine = 46 StartColumn = 3 EndLine = 46 EndColumn = 131 }); DirectLink ([Literal ("For example like this", Some { StartLine = 46 StartColumn = 131 EndLine = 46 EndColumn = 152 })], "https://github.com/fsprojects/FSharp.Formatting/blob/master/docs/literate.fsx#L19", None, Some { StartLine = 46 StartColumn = 131 EndLine = 46 EndColumn = 238 }); Literal (".", Some { StartLine = 46 StartColumn = 131 EndLine = 46 EndColumn = 132 })], Some { StartLine = 46 StartColumn = 3 EndLine = 46 EndColumn = 238 }); Paragraph ([Literal ("Also add load sections to make sure your notebooks and scripts contain the right content to load packages out of repo.  ", Some { StartLine = 48 StartColumn = 3 EndLine = 48 EndColumn = 123 }); DirectLink ([Literal ("For example like this", Some { StartLine = 48 StartColumn = 123 EndLine = 48 EndColumn = 144 })], "https://github.com/fsprojects/FSharp.Formatting/blob/master/docs/literate.fsx#L1", None, Some { StartLine = 48 StartColumn = 123 EndLine = 48 EndColumn = 228 })], Some { StartLine = 48 StartColumn = 3 EndLine = 48 EndColumn = 228 })]], Some { StartLine = 7 StartColumn = 0 EndLine = 7 EndColumn = 6 }) to pynb markdown

Sample commands:

// can't yet format InlineBlock ("dotnet tool install FSharp.Formatting.CommandTool --local
git add dotnet-tools.json   
git rm -fr docs/tools
git mv docs/input/* docs
git mv docs/files/* docs

<manually download and fixup the _template.html>

dotnet fsdocs watch

touch docs/_template.fsx
touch docs/_template.ipynb
git add docs/_template.fsx
git add docs/_template.ipynb
", None, None) to pynb markdown

Here is an example PR: [https://github.com/fsprojects/FSharp.Control.AsyncSeq/pull/116](https://github.com/fsprojects/FSharp.Control.AsyncSeq/pull/116)



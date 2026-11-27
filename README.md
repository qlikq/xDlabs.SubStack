# xDlabs.SubStack

A PowerShell 7.6 library for reading public Substack publications. Use it in scripts, your own terminal UI, or a different front end. It runs without PSTui.

## Use the library

```powershell
Install-PSResource xDlabs.SubStack -Version 2.0.0 -Repository PSGallery
$posts = @(Get-SubstackPosts -Url 'igregui.substack.com')
$posts | Select-Object Title, Published, Url
if ($posts.Count) { Get-SubstackPostPreview -Post $posts[0] }
```

`Get-SubstackPosts` merges public RSS entries and the latest entries returned by the undocumented Substack archive, removes duplicates, and returns the newest entries first. Its objects expose `Title`, `Published`, `Url`, and `Text`. `Get-SubstackPostPreview` returns the public text or excerpt. `ConvertTo-SubstackPublicationUrl` validates and normalizes a publication's HTTPS home URL. See `Get-Help Get-SubstackPosts -Full`.

The independent library starts at version 2.0.0. PowerShell Gallery treats the earlier reader package named `XDlabs.Substack` as the same package ID.

## Development and releases

```powershell
./Restore-Dependencies.ps1
./Build.ps1
./Test.ps1 -Live
```

ModuleBuilder 3.2.18 generates the module. Pester 6.2.0 runs the unit tests and, with `-Live`, checks the real xDlabs publication.

Use `-Sign` on Windows to sign the build with SimplySign and a trusted timestamp. Use `-Publish` to sign and publish through PowerShell Gallery with `PSGALLERY_API_KEY` or `-ApiKey`. Use `-PushGitHub -GitHubRepository owner/name` to push the ready-built library and README to its own release repository. Use `-WhatIf` to preview an operation.

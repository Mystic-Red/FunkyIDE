# FunkyIDE

<p align="center">
  <img src="resources/win32/code_640x640.png" alt="FunkyIDE microphone" width="640" height="640">
</p>

FunkyIDE is a source fork of Visual Studio Code's **Code - OSS** for
**Friday Night Funkin' mod development**, maintained by **Red**.

[Repository](https://github.com/Mystic-Red/FunkyIDE) ·
[Issues](https://github.com/Mystic-Red/FunkyIDE/issues) ·
[Contact](mailto:agusnew2804@gmail.com)

## Current status: Phase 1

- Conservative Psych Engine project and mod detection using filesystem evidence.
- An internal index of songs, charts, characters, stages, scripts, custom events,
  and custom note types, with resource URIs and content origins.
- A native **FNF Explorer** in the **FunkyIDE** activity-bar container.
- Standard VS Code file editing and a dedicated **FunkyIDE** output log.

The normal VS Code Explorer remains available. There are no custom editors,
engine launchers, script execution features, or file-creation wizards yet.

## Using the FNF Explorer

1. Open a supported Psych Engine source tree, packaged project, or mod folder.
2. Select the music icon for **FunkyIDE** in the activity bar, or run
   **Focus FNF Explorer** from the Command Palette.
3. Expand a project and its Songs, Characters, Stages, Scripts, Events, or Note
   Types category. Songs contain charts when the index provides their relationship.
4. Open a file using the usual tree interactions: preview, double-click to pin,
   keyboard navigation, and opening beside the current editor.
5. After changing content on disk, use the view's refresh button or
   **FNF: Refresh Explorer**. **FunkyIDE: Rescan Projects** remains available.

The tree updates whenever the project service publishes a new index, including
workspace-folder changes. Without a detected project it shows an explanatory empty
state. The scanner is conservative: an empty template or a sparse legacy mod may
not provide enough evidence. Automatic filesystem watching is not implemented yet.

Chart labels use indexed difficulty suffixes when available; otherwise they retain
the indexed name. The Explorer does not infer a default difficulty or parse charts.
Same-named songs in different content origins remain separate.

## Development

This is a source checkout, not a packaged release. It retains the VS Code build
system and prerequisites. See [CONTRIBUTING.md](CONTRIBUTING.md) and the
[upstream build guide](https://github.com/microsoft/vscode/wiki/How-to-Contribute)
for toolchain setup. Once dependencies are installed, use the repository's existing
compile and launch scripts; on Windows the development launcher is
`scripts\code.bat`.

FunkyIDE code is concentrated in
[`src/vs/workbench/contrib/fnf`](src/vs/workbench/contrib/fnf/README.md).
The engine-neutral project service owns state; the Psych adapter owns engine
layout rules; the Explorer consumes the service's snapshot without filesystem access.

Focused suites live in `src/vs/workbench/contrib/fnf/test/browser`. With compiled
test output and the normal dependencies installed, run `scripts\test.bat` with
`--run vs/workbench/contrib/fnf/test/browser/fnfExplorer.test`, or select the
`psychEngineAdapter.test` and `fnfProjectService.test` suites in the same directory.

## Product identity

`product.json` defines FunkyIDE's application name, `funkyide` CLI and URL protocol,
`.funkyide` data folder, separate server/tunnel names, macOS bundle identity, Linux
icon identity, and unique Windows installer IDs. It does not migrate existing
Code - OSS settings. Product metadata identifies Red as the maintainer and directs
issues to this repository.

Existing microphone artwork keeps the build system's `code.*` asset filenames.
Windows installer metadata and Linux package descriptions are branded for FunkyIDE.
Legacy internal build/task names and artifact filenames remain for compatibility
with the inherited build scripts. macOS icon and installer banner artwork still
need a dedicated artwork pass. Release signing, update hosting, and Microsoft-hosted
release pipelines are not configured for FunkyIDE. The AppX publisher is `CN=Red`;
a distributable signed AppX would require a matching signing certificate.

## License and upstream

FunkyIDE is based on [Microsoft's VS Code source](https://github.com/microsoft/vscode).
The original copyright notices, [MIT license](LICENSE.txt), and
[third-party notices](ThirdPartyNotices.txt) are preserved. FunkyIDE is an independent
fork, not Microsoft's Visual Studio Code distribution and not an official FNF or
Psych Engine project.

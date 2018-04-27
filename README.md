# VSCode `markdown-preview-enhanced` with [litvis](http://litvis.org/)

This project is a fork of [`vscode-markdown-preview-enhanced`](https://github.com/shd101wyy/markdown-preview-enhanced), which is a popular [VSCode extension](https://marketplace.visualstudio.com/items?itemName=shd101wyy.markdown-preview-enhanced) for previewing markdown files.
Most of the code in this fork is inherited from the upstream repository and is thus courtesy of [@shd101wyy](https://github.com/shd101wyy) and other [contributors](https://github.com/shd101wyy/vscode-markdown-preview-enhanced/graphs/contributors) to `vscode-markdown-preview-enhanced`.

The fork produces a VSCode extension called [`markdown-preview-enhanced-with-litvis`](https://marketplace.visualstudio.com/items?itemName=gicentre.markdown-preview-enhanced-with-litvis), which enables _Literate Visualisation_ ([litvis](http://litvis.org/)) in rendered markdown previews.

Litvis functionality has been designed and developed at [giCentre](https://www.gicentre.net/) by [Jo Wood](https://github.com/jwoLondon), [Alexander Kachkaev](https://github.com/kachkaev) and [Jason Dykes](https://github.com/jsndyks).
This research was in part supported by the EU under the EC Grant Agreement No. FP7-IP-608142 to Project [VALCRI](http://valcri.org/).

## Prerequisites

Please ensure that you have a reasonably recent version of Node.js installed on your machine before proceeding to the setup.
It can be downloaded and installed from https://nodejs.org/.

## Setup for VSCode users

### Via VSCode’s GUI

1.  Click on the extensions icon in the left panel, search for _Markdown Preview Enhanced with litvis_ and click install.

1.  If you are using _Markdown Preview Enhanced_ extension (from which this project was forked), temporary uninstall or disable it while you are trying out litvis.

### Via command line

```bash
code --install-extension gicentre.markdown-preview-enhanced-with-litvis

code --uninstall-extension shd101wyy.markdown-preview-enhanced
```

VSCode does not support `--disable-extension` command, so if you want disable `shd101wyy.markdown-preview-enhanced` instead of uninstalling it, please do this via the app’s GUI.

## Getting started with litvis narratives

Literate visualization uses [Elm](http://elm-lang.org) and [Vega-Lite](https://vega.github.io/vega-lite) in the form of a declarative visualization language [elm-vega](http://package.elm-lang.org/packages/gicentre/elm-vega/latest).
While you don't have to use elm-vega in a litvis document it does enable quick declarative generation of interactive data graphics and therefore considerably enhances the capability of a litvis document.

Creating your own litvis narrative is as easy as writing a markdown file.
You can start with exploring the examples available at
https://github.com/gicentre/litvis/tree/master/examples.

## Formatting litvis narratives

It is possible to automatically format litvis-enabled markdown files including embedded Elm code blocks with [Prettier](https://prettier.io/), which is an opinionated code formatting tool.

Prettier is available in VSCode via [`prettier-vscode`](https://github.com/prettier/prettier-vscode) extension, but it does not format literate Elm code blocks in markdown files out of the box.

Please follow these steps to enable full-featured formatting support for litvis in VSCode:

1.  Install `esbenp.prettier-vscode` package via VSCode’s _Extensions_ panel or from a command line:

    ```bash
    code --install-extension esbenp.prettier-vscode
    ```

1.  Locally install Prettier and its [Elm plugin](https://github.com/gicentre/prettier-plugin-elm) via npm:

    ```
    npm init --yes
    npm install github:kachkaev/prettier#fix-global-plugin-api-dist prettier-plugin-elm
    ```

    > Having a globally installed Prettier would be more convenient, but it is not supported by the VSCode extension yet.

    > Installing from `github:kachkaev/prettier#...` instead of just `prettier` is necessary until [prettier/prettier#4192](https://github.com/prettier/prettier/pull/4192) is merged.

1)  _(optional)_ Configure Prettier by creating `.prettierrc` with the following yaml:

    ```yaml
    overrides:
    - files: "*.md"
      options:
        tabWidth: 4
    ```

    Doing this via bash:

    ```bash
    echo -e "overrides:\n- files: \"*.md\"\n  options:\n    tabWidth: 4" > .prettierrc
    ```

    This will indent bullet point lists in markdowns with four spaces instead of two.

## Getting linting feedback for litvis narratives

If a litvis narrative you are currently editing contains problems like Elm compile errors, corresponding messages will be automatically shown in the _Problems_ tab of VSCode:

![litvis linting UI](https://user-images.githubusercontent.com/608862/39370936-1eb6d250-4a38-11e8-853c-6ec03a281e98.png)

The list of messages gets updated every time a preview is refreshed.

If you are using other tools such as [Spell Checker](https://marketplace.visualstudio.com/items?itemName=streetsidesoftware.code-spell-checker), which also detect and report problems, litvis-specific messages may become lost amongst others.
In this case, you can type _litvis_ in the filter input and thus filter out the messages that do not require your attention.

![linting filtering](https://user-images.githubusercontent.com/608862/39371088-96f7af3c-4a38-11e8-865e-282a798350a9.png)

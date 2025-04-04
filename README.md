# hackmd-to-html-cli

[![NPM version](https://img.shields.io/npm/v/hackmd-to-html-cli.svg?logo=npm&style=flat-square)](https://www.npmjs.org/package/hackmd-to-html-cli) ![](https://img.shields.io/github/license/ksw2000/hackmd-to-html-cli?color=yellow&style=flat-square) ![](https://img.shields.io/github/actions/workflow/status/ksw2000/hackmd-to-html-cli/gitpage.yml?branch=main&style=flat-square) ![](https://img.shields.io/npm/dt/hackmd-to-html-cli?color=blue&style=flat-square)

Not only is this a CLI tool, but it is also an importable package for converting standard Markdown and even [HackMD](https://hackmd.io/)-supported Markdown into HTML.

+ Example of input markdown: [./example/index.md](https://raw.githubusercontent.com/ksw2000/hackmd-to-html-cli/main/example/index.md)
+ Example of output html: [https://ksw2000.github.io/hackmd-to-html-cli/](https://ksw2000.github.io/hackmd-to-html-cli/)
+ Example of output html in dark mode: [https://ksw2000.github.io/hackmd-to-html-cli/index.dark.html](https://ksw2000.github.io/hackmd-to-html-cli/index.dark.html)
+ Example of converting in web: [https://ksw2000.github.io/hackmd-to-html-cli/webjs.html](https://ksw2000.github.io/hackmd-to-html-cli/webjs.html)

## Install

```sh
# CLI
npm install -g hackmd-to-html-cli

# Package
npm install hackmd-to-html-cli
```

## CLI

```sh
$ hmd2html --help
hmd2html --help
Usage: index [options]

Options:
  -v, --version                   output the current version
  -i, --input <files_or_urls...>  the path/url of input markdown files
  -d, --dest <dir>                the path of output directory (filename is generated automatically) (default: ./output)
  -o, --output <files...>         the path of output file (ignored if the flag -d is set) (default: "")
  -l, --layout <html_file>        specify the layout file (default: "")
  -b, --hardBreak                 use hard break instead of soft break
  -k, --dark                      use the dark mode layout (activate only if the -l option is not set)
  -h, --help                      display help for command
```

**Convert**

```sh
# convert files
$ hmd2html -i file1.md file2.md file3.md

# allow wildcard input
$ hmd2html -i dir/*.md

# allow url input
$ hmd2html -i https://github.com/ksw2000/hackmd-to-html-cli/blob/main/example/index.md

# set output folder
$ hmd2html -i file1.md -d ./my_output

# set the filename of output
$ hmd2html -i file1.md -o file1.html
$ hmd2html -i file1.md file2.md -o file1.html file2.html

# use default darkmode layout
$ hmd2html -i file1.md -k

# use custom layout
$ hmd2html -i hello.md -l ./myLayout.html
```

## Layouts

We provide the two default layouts. Please see layouts here: [https://github.com/ksw2000/hackmd-to-html-cli/blob/main/layouts/](./layouts/)

+ `{{main}}` renders main content of markdown.
+ `{{lang}}` renders lang property if there are yaml metadata about `lang` in markdown file. e.g. `lang="zh-TW"`
+ `{{dir}}` renders dir property if there are yaml metadata about `dir` in markdown file. e.g. `dir="ltr"`
+ `{{meta}}` renders meta tag if there are yaml metadata about `title`, `description`, `robots` or`image`. e.g. `<meta name="robots" content="noindex">`

Example:

```html
<!DOCTYPE html>
<html {{lang}} {{dir}}>
<head>
    {{metas}}
    <meta name="viewport" content="width=device-width, initial-scale=1.0, user-scalable=no">
    <meta charset="utf-8">
    <body>
      {{main}}
    </body>
</html>
```

There are some features rendered by other dependencies. Thus, in our default layout, we include those dependencies.

## Example

### CommonJS

```js
const { Converter } = require('hackmd-to-html-cli')

const converter = new Converter();
const res = converter.render("# hello");

console.log(res.main);
```


### ES Module

```ts
import { Converter } from "hackmd-to-html-cli"

const converter = new Converter();
const res = converter.render("# hello");

console.log(res.main);
```

### Web

```js
const converter = new window.hmd2html.Converter();
const res = converter.render("# hello");
console.log(res.main);
```

## Support

`hmd2html`: our tool (the latest)

`HackMD Default Converter`: The default markdown to html converter provided by HackMD, i.e., download HTML file on HackMD.

HackMD fully supports syntax: [features](https://hackmd.io/features-tw?both)

| Features   | hmd2html  | HackMD<br>Default Converter |
|---------------------------------|:--:|:--:|
| ToC                             | ✅ | ✅ |
| Emoji                           | ✅ | ✅ |
| ToDo list                       | ✅ | ✅ |
| Code block                      | ✅ | ✅ |
| - Show line number or not       | ✅ | ❌ |
| - Specify the start line number | ✅ | ❌ |
| - Continue line number          | ✅ | ❌ |
| Blockquote                      | ✅ | ✅ |
| - specify your name             | ✅ | ✅ |
| - specify time                  | ✅ | ✅ |
| - color                         | ✅ | ✅ |
| Render CSV as table             | ✅ | ✅ |
| MathJax                         | ✅ | ✅ |
| Sequence diagrams               | ✅ | ❌ |
| Flow charts                     | ✅ | ❌ |
| Graphviz                        | ✅ | ❌ |
| Mermaid                         | ✅ | ❌ |
| Abc                             | ✅ | ❌ |
| PlantUML                        | ✅ | ✅ |
| Vega-Lite                       | ✅ | ❌ |
| Fretboard                       | ✅ | ❌ |
| Alert Area                      | ✅ | ✅ |
| Detail                          | ✅ | ✅ |
| Spoiler container               | ✅ | ✅ |
| Headers h1-h6                   | ✅ | ✅ |
| Horizontal line `---` `***`     | ✅ | ✅ |
| Bold `**b**` `__b__`            | ✅ | ✅ |
| Italic `*i*` `_i_`              | ✅ | ✅ |
| Deleted text `~~del~~`          | ✅ | ✅ |
| Superscript `^sup^`             | ✅ | ✅ |
| Subscript  `~sub~`              | ✅ | ✅ |
| Inserted text `++ins++`         | ✅ | ✅ |
| Marked text `==mark==`          | ✅ | ✅ |
| Ruby case                       | ✅ | ✅ |
| Typographic<br>replacements     | ✅ | ✅ |
| Blockquotes                     | ✅ | ✅ |
| List                            | ✅ | ✅ |
| Tables                          | ✅ | ✅ |
| Links                           | ✅ | ✅ |
| Link with title                 | ✅ | ✅ |
| Autoconverted link              | ✅ | ✅ |
| Image                           | ✅ | ✅ |
| - normal                        | ✅ | ✅ |
| - with title                    | ✅ | ✅ |
| - given size                    | ✅ | ✅ |
| Footnotes                       | ✅ | ✅ |
| Definition list                 | ✅ | ✅ |
| Abbreviations                   | ✅ | ✅ |

### Support Externals

| Features    | hmd2html  | HackMD<br>Default Converter|
|-------------|:---------:|:---------:|
| Youtube     | ✅       | ✅        |
| Vimeo       | ✅       | ❌        |
| Gist        | ✅       | ✅        |
| SlideShare  | ❌       | ❌        |
| Speakerdeck | ✅       | ✅        |
| PDF         | ✅       | ✅        |
| Figma       | ✅       | ✅        |

### Support YAML Metadata

| Features      | hmd2html  | Implementation  |
|---------------|:---------:|:-------:|
| title         | ✅       | `<title></title>`<br>`<meta name="twitter:title">`<br>`<meta property="og:title">`|
| description   | ✅       | `<meta name="description">`<br>`<meta name="twitter:description">`<br>`<meta property="og:description">` |
| robots        | ✅       | `<meta name="robots">` |
| lang          | ✅       | `<html lang="">` |
| dir           | ✅       | `<html dir="">` |
| image         | ✅       | `<meta property="og:image">`<br>`<meta name="twitter:image:src">` |
| others        | ✅       | Hide the metadata by html comment |

HackMD sets the `lang` tag and `dir` tag at the beginning of `<body>`. hmd2html sets the the `lang` tag and `dir` tag at `<html>` when using default layout.

## Development

1. `npm run lint` to check the format of source code.
2. `npm run example` runs example for this package, which generates result from `./example` and places them in `./output`.
3. `npm test` runs unit test files whose filenames end with `.spec.ts`

## Contributing

Contributions to **hackmd-to-html-cli** are welcome and highly appreciated. Please run lint `npm run lint` and test `npm run test` before pull requesting.
<div align="center">

<h1>Arturo Bundler</h1> 

### Easily bundle an Arturo app on any GitHub runner/OS<br><br>![License](https://img.shields.io/github/license/arturo-lang/bundler?style=for-the-badge) [![Build Status](https://img.shields.io/github/actions/workflow/status/arturo-lang/bundler/testbundle.yml?branch=main&style=for-the-badge)](https://github.com/arturo-lang/bundler/actions)
</div>

---
 
<!--ts-->
   * [How do I use it?](#how-do-i-use-it)
      * [More options](#more-options)
   * [How can I release an app?](#how-can-i-release-an-app)
   * [License](#license)
<!--te-->

---

### How do I use it?

The most barebones configuration would be:

```yaml
- uses: arturo-lang/bundler@main
  with: 
    token: ${{ secrets.GITHUB_TOKEN }}
    entry: yourscript.art
```

> [!TIP]
> The `entry` field represents your app's "entry point" - that is the initial script. Whether it imports other files/scripts or not doesn't matter, since it will - hopefully - be taken care of automatically. Also, you may choose to set the whole folder (in case it's an Arturo *package*) as the entry point: if it is a package with an `info.art` file that declares an `executable:`, it will work as well! 😜

Based on the runner, the action will compile and setup the appropriate, native binary:

| runner | binary |
|--------|--------|
| ubuntu-latest | amd64 / Linux |
| macos-12 | amd64 / macOS |
| macos-latest | arm64 (M1) / macOS |
| windows-latest | amd64 / Windows |

#### More options

| option | description |
|--------|-------------|
| target | change the name of the final binary (default: `'auto'` = use the same name as the entry script) |
| version | set version number, to be included in the archive names - in the case of releases, this will be extracted automatically from the release tag (default: `''`) |

### How can I release an app?

With Arturo's bundler and the appropriate setup, you can instantly offer binaries for all major OSes, as part of your GitHub repo's workflows.

But, panic not! We've got you covered! 😉

Actually it's very streamlined and easy:

- create a `.github/` folder inside your repo
- create a `workflows/` folder inside the above folder (in case it's not already there, obviously)
- create a new file in `./github/workflows/` (name it `asyouwish.yml`)
- copy the contents of [https://github.com/arturo-lang/bundler/blob/main/.github/workflows/testrelease.yml](https://github.com/arturo-lang/bundler/blob/main/.github/workflows/testrelease.yml)
- change only the relevant part above for your own app

> [!NOTE]
> The configuration you have to complete mainly includes 3 fields:
>  - `app-name:` The name of your binary as it will appear
>  - `app-entry:` The "entry point" of your app (see [above^](#how-do-i-use-it))
>  - `app-notes:` (Optionally) add some description that will appear at the bottom of the release

And done! 💥

Next time you push a new `vX.Y.Z` tag, a new release will be automatically created, along with all the binaries of your app for Linux/macOS/Windows (and more coming?).

Sounds amazing? It actually *is*! 🚀

------

### License

MIT License

Copyright (c) 2019-2024 Yanis Zafirópulos (aka Dr.Kameleon)

Permission is hereby granted, free of charge, to any person obtaining a copy
of this software and associated documentation files (the "Software"), to deal
in the Software without restriction, including without limitation the rights
to use, copy, modify, merge, publish, distribute, sublicense, and/or sell
copies of the Software, and to permit persons to whom the Software is
furnished to do so, subject to the following conditions:

The above copyright notice and this permission notice shall be included in all
copies or substantial portions of the Software.

THE SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND, EXPRESS OR
IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF MERCHANTABILITY,
FITNESS FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT. IN NO EVENT SHALL THE
AUTHORS OR COPYRIGHT HOLDERS BE LIABLE FOR ANY CLAIM, DAMAGES OR OTHER
LIABILITY, WHETHER IN AN ACTION OF CONTRACT, TORT OR OTHERWISE, ARISING FROM,
OUT OF OR IN CONNECTION WITH THE SOFTWARE OR THE USE OR OTHER DEALINGS IN THE
SOFTWARE.

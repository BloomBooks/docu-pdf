## ℹ️ Note

This is a fork of the fantastic [mr-pdf](https://github.com/kohheepeace/mr-pdf). It is intended for our own internal use in SIL. We're only going to maintain it for use with our Docusaurus sites, not the other systems that mr-pdf supports.

## 📌 Introduction

This is a command line tool for creating PDFs from documentation sites built with [Docusaurus](https://docusaurus.io). While your browser can make pdfs of individual pages, this makes one of _all_ the pages.

## ⚡ Usage

```shell
npx doc-pdf --initialDocURLs="https://docs.bloomlibrary.org/" \
--contentSelector="article" \
--nextPageSelector="a.pagination-nav__link--next" \
--excludeSelectors=".theme-doc-breadcrumbs,a.theme-edit-this-page" \
--coverTitle="Bloom Docs" \
--pageSize="A4" \
--outputPDFFilename="static/downloads/docs-bloomlibrary-english-a4.pdf"
```

## 🍗 CLI Options

| Option                | Required | Description                                                                                                                                                                        |
| --------------------- | -------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `--initialDocURLs`    | Yes      | set URL to start generating PDF from.                                                                                                                                              |
| `--contentSelector`   | Yes      | used to find the part of main content                                                                                                                                              |
| `--nextPageSelector`  | Yes      | CSS Selector used to find next page to be printed for looping.                                                                                                                     |
| `--excludeURLs`       | No       | URLs to be excluded in PDF                                                                                                                                                         |
| `--excludeSelectors`  | No       | exclude selectors from PDF. Separate each selector **with comma and no space**. But you can use space in each selector. ex: `--excludeSelectors=".nav,.next > a"`                  |
| `--cssStyle`          | No       | CSS style to adjust PDF output ex: `--cssStyle="body{padding-top: 0;}"` \*If you're project owner you can use `@media print { }` to edit CSS for PDF.                              |
| `--outputPDFFilename` | No       | name of the output PDF file. Default is `mr-pdf.pdf`                                                                                                                               |
| `--pdfMargin`         | No       | set margin around PDF file. Separate each margin **with comma and no space**. ex: `--pdfMargin="10,20,30,40"`. This sets margin `top: 10px, right: 20px, bottom: 30px, left: 40px` |
| `--pageSize`          | No       | pdf format ex: `--pageSize="A3"`. Please check this link for available formats [Puppeteer document](https://pptr.dev/#?product=Puppeteer&version=v5.2.1&show=api-pagepdfoptions)   |
| `--disableTOC`        | No       | Optional toggle to show the table of contents or not                                                                                                                               |
| `--coverTitle`        | No       | Title for the PDF cover.                                                                                                                                                           |
| `--coverImage`        | No       | `<src>` Image for PDF cover (does not support SVG)                                                                                                                                 |
| `--coverSub`          | No       | Subtitle the for PDF cover. Add `<br/>` tags for multiple lines.                                                                                                                   |
| `--headerTemplate`    | No       | HTML template for the print header. Please check this link for details of injecting values [Puppeteer document](https://pptr.dev/#?product=Puppeteer&show=api-pagepdfoptions)      |
| `--footerTemplate`    | No       | HTML template for the print footer. Please check this link for details of injecting values [Puppeteer document](https://pptr.dev/#?product=Puppeteer&show=api-pagepdfoptions)      |
|                       |          |                                                                                                                                                                                    |

## 🎨 Examples and Demo PDF

### Docusaurus v1

<https://docusaurus.io/en/>

`initialDocURLs`: <https://docusaurus.io/docs/en/installation>

`demoPDF`: <https://github.com/kohheepeace/mr-pdf/blob/master/v1-docusaurus.pdf>

`command`:

```shell
npx mr-pdf --initialDocURLs="https://docusaurus.io/docs/en/installation" --nextPageSelector=".docs-prevnext > a.docs-next" --excludeSelectors=".fixedHeaderContainer,footer.nav-footer,#docsNav,nav.onPageNav,a.edit-page-link,div.docs-prevnext" --cssStyle=".navPusher {padding-top: 0;}" --pdfMargin="20"
```

### Docusaurus v2 beta

![20210603060438](https://user-images.githubusercontent.com/29557494/120552058-b4299e00-c431-11eb-833e-1ac1338b0a70.gif)

<https://docusaurus.io/>

`initialDocURLs`: <https://docusaurus.io/docs>

`demoPDF`: <https://github.com/kohheepeace/mr-pdf/blob/master/v2-docusaurus.pdf>

`command`:

```shell
npx mr-pdf --initialDocURLs="https://docusaurus.io/docs/" --contentSelector="article" --nextPageSelector=".pagination-nav__item--next > a" --excludeSelectors=".margin-vert--xl a" --coverImage="https://docusaurus.io/img/docusaurus.png" --coverTitle="Docusaurus v2"
```

### Vuepress v1

<https://vuepress.vuejs.org/>

`initialDocURLs`:

<https://vuepress.vuejs.org/guide/>

`demoPDF`: <https://github.com/kohheepeace/mr-pdf/blob/master/v1-vuepress.pdf>
`command`:

```shell
npx mr-pdf --initialDocURLs="https://vuepress.vuejs.org/guide/" --contentSelector="main" --nextPageSelector=".page-nav .next a" --excludeSelectors="header.navbar,aside.sidebar,footer.page-edit .edit-link,.global-ui,.page-nav" --coverImage="https://vuepress.vuejs.org/hero.png" --coverTitle="VuePress" --coverSub="Vue-powered Static Site Generator"
```

### Vuepress v2 beta

<https://v2.vuepress.vuejs.org/>

`initialDocURLs`:

<https://v2.vuepress.vuejs.org/guide/>

`demoPDF`: <https://github.com/kohheepeace/mr-pdf/blob/master/v2-vuepress.pdf>
`command`:

```shell
npx mr-pdf --initialDocURLs="https://v2.vuepress.vuejs.org/guide/" --contentSelector="main" --nextPageSelector=".page-nav .next a" --excludeSelectors="header.navbar,aside.sidebar,footer.page-edit .edit-link,.global-ui,.page-nav" --coverImage="https://v2.vuepress.vuejs.org/images/hero.png" --coverTitle="VuePress" --coverSub="Vue-powered Static Site Generator"
```

### Mkdocs

<https://www.mkdocs.org/>

`initialDocURLs`: <https://www.mkdocs.org/>

`demoPDF`: <https://github.com/kohheepeace/mr-pdf/blob/master/mkdocs.pdf>

`command`:

```shell
npx mr-pdf --initialDocURLs="https://www.mkdocs.org/" --nextPageSelector="ul.navbar-nav li.nav-item a[rel~='next']" --excludeSelectors=".navbar.fixed-top,footer,.homepage .container .row .col-md-3,#toc-collapse" --cssStyle=".col-md-9 {flex: 0 0 100%; max-width: 100%;}"
```

### Material for Mkdocs

<https://squidfunk.github.io/mkdocs-material/>

`initialDocURLs`: <https://squidfunk.github.io/mkdocs-material/getting-started/>

`demoPDF`: <https://github.com/kohheepeace/mr-pdf/blob/master/material-for-mkdocs.pdf>
`command`:

```shell
npx mr-pdf --initialDocURLs="https://squidfunk.github.io/mkdocs-material/getting-started/" --nextPageSelector="a.md-footer-nav__link--next" --excludeSelectors="header.md-header,.announce,nav.md-tabs,.md-main__inner .md-sidebar--primary,.md-main__inner .md-sidebar--secondary,footer" --cssStyle=".md-content {max-width: 100%!important;}"
```

#### PR to add new docs is welcome here... 😸

## 📄 How `mr-pdf` works

1. [puppter](https://pptr.dev/) can make html to PDF like you can print HTML page in chrome browser
2. so, the idea of mr-pdf is **generating one big HTML through looping page link, then run [`page.pdf()`](https://github.com/puppeteer/puppeteer/blob/v13.1.3/docs/api.md#pagepdfoptions)** from puppter to generate PDF.

![mr-pdf-diagram](https://user-images.githubusercontent.com/29557494/90359040-c8fb9780-e092-11ea-89c7-1868bc32919f.png)

## 🎉 Thanks

This repo's code is coming from <https://github.com/KohheePeace/docusaurus-pdf>.

Thanks for awesome code made by [@maxarndt](https://github.com/maxarndt) and [@aloisklink](https://github.com/aloisklink).

[@bojl](https://github.com/bojl) approach to make TOC was awesome and breakthrough.

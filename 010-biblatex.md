# 基于`biblatex`生成参考文献 {#biber}

附录\@ref(biber)介绍了 文献库扩展包`biblatex`的使用，及其与`natbib`的比较. [@xie2015; @R-base]

## bibtex 与 biber, natbib 与 biblatex 比较 {#sec10-1}

### 概述 

- `bibtex` 与 `biber` 是处理参考文献信息二个外部程序(backend), 它们起
到将$\LaTeX$ 文档与 `bib` 文档交互的作用；

- `natbib` 与 `biblatex` 是二个处理参考文献(bibliography) 和引用(citation)的$\TeX$ 宏包; `natbib` 仅通过`bibtex` 起作用，而`biblatex` 可通过
 `biber` 起作用；

### `natbib` 的优点

- natbib 的优点：

  - 有大量与期刊/出版商对应的风格文件(.sty);

- natbib 的缺点:

  - 修改风格文件较为困难；

  - 其设计的局限性：主要为自然科学类期刊的`Author-Year` 及数字引
用方式设计.

### biblatex 的优缺点

- `biblatex` 被认为是$\LaTeX$ 中处理参考文献(bibliography) 的很有前途的宏包，功能强大，提供了很多可定制选项。

- `biblatex` 的优点

  - 提供`natbib` 的 `Author-year` 和数字引用方式，因此可视为natbib
的扩展；
  - 通过$\LaTeX$ 的宏控制文献的风格，方便修改;
  - 提供许多人性化的引用风格(例如`author-title`);
  - 提供人性化的文献数据库域名(字段);
  - 直接支持多文献库与文献分类;
  - 提供大量标准与拓展的`biblatex` 风格(见使用手册);
  - 文献可按主题分割为部分;

## biblatex 的在$\TeX$中的使用样例 {#sec10-2}

1. 使用

```
  \usepackage[style=authoryear,backend=biber]{biblatex}
```

(代替`\usepackage[authoryear]{natbib}`);

2. 加载一个或多个 `bib` 文献库文件:

```
  \addbibresource{file1.bib}    
  \addbibresource{file2.bib}
```

3. 要出现文献的地方输入

```
  \printbibliography
```

4. 引用: 使用`\textcite` 代替`\citet`; 使用`\parencite` 代替`\citep`

5. 编译方式

```
XELATEX(或LATEX, pdfLATEX)
biber(代替bibtex)
XELATEX(或LATEX, pdfLATEX)
XELATEX(或LATEX, pdfLATEX)
```

## `biblatex`在`bookdown`中的使用 {#sec10-3}

1. 在`index.Rmd`文件的`yml`部分增加选项

   ```
biblatexoptions: [refsegment=chapter]
biblio-style: gb7714-2015ay
   ```
  
    注意`[]`内可增加其他`biblatex`选项(参考`biblatex`使用手册)

1. 在需要出现文献的地方(如每一章后)加

   ```
   \printbibliography[segment=\therefsegment, heading=subbibliography, title={参考文献}]
   ```

1. 在`_output.yml`文件的`bookdown::pdf_book:`增加选项(前面空二格)

   ```
    citation_package: biblatex
   ```

    注：若要`bibtex`驱动文献的排版，只需要在这一步改为`citation_package: natbib`

1. 如上所述，LaTeX 要生成最终的 PDF 文档，如果含有交叉引用(图形、表格、公式、章节、文献等)、BibTeX/biber、术语表等等，通常需要多次编译才行。而使用 Latexmk 则只需运行一次，它会自动帮你做好其它所有事情。尽管在你已经安装的 LaTeX 发行版本已经包含了 Latexmk，但我们需要运行它。使用`XeLaTeX`的编译格式为
```
latexmk -pvc -xelatex file.tex
```
其中选项`pvc`表示检查输入文件的更改并预览结果。在Rstudio中你只需要添加下面的代码块。

```r
Sys.setenv(RSTUDIO_PDFLATEX = "latexmk")
```



\printbibliography[segment=\therefsegment, heading=subbibliography, title={参考文献}]


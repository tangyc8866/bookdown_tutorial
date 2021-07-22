# `Bookdown`中的表格 {#tables}

\indent
这是第 \@ref(tables) 章的内容, 讲述浮动对象图形的标签与引用. [@xie2015; @bookdown2016]

## 表格示例1：由数据生成表格 {#sec6-1}


```r
knitr::kable(
  head(mtcars[, 1:5], 10), booktabs = TRUE,
  caption = 'mtcars数据的前5行.'
)
```



Table: (\#tab:tab3-1)mtcars数据的前5行.

|                  |  mpg| cyl|  disp|  hp| drat|
|:-----------------|----:|---:|-----:|---:|----:|
|Mazda RX4         | 21.0|   6| 160.0| 110| 3.90|
|Mazda RX4 Wag     | 21.0|   6| 160.0| 110| 3.90|
|Datsun 710        | 22.8|   4| 108.0|  93| 3.85|
|Hornet 4 Drive    | 21.4|   6| 258.0| 110| 3.08|
|Hornet Sportabout | 18.7|   8| 360.0| 175| 3.15|
|Valiant           | 18.1|   6| 225.0| 105| 2.76|
|Duster 360        | 14.3|   8| 360.0| 245| 3.21|
|Merc 240D         | 24.4|   4| 146.7|  62| 3.69|
|Merc 230          | 22.8|   4| 140.8|  95| 3.92|
|Merc 280          | 19.2|   6| 167.6| 123| 3.92|

## 表格示例2: 由数据框构造表格 {#sec6-2}

\indent
(ref:tab3p2) 遗传连接模型例子中观测到的频数 $y_i$ 和频率 $p(y_i|\pi)$，$i=1, \dots ,4$，197个动物.


Table: (\#tab:tab3-2)(ref:tab3p2)

|Category                    |1                           |2                    |3                    |4             |
|:---------------------------|:---------------------------|:--------------------|:--------------------|:-------------|
|Frequency $y_i$             |125                         |18                   |20                   |34            |
|Probability $p(y_i\mid\pi)$ |$\frac{1}{2}+\frac{\pi}{4}$ |$\frac{1}{4}(1-\pi)$ |$\frac{1}{4}(1-\pi)$ |$\frac{1}{4}$ |

注意:

1. 表格中`%`用`\\%`
2. 表格中latex命令用`\\`代替`\`

## 表格引用 {#sec6-3}

\indent
表格引用由代码块的标签(设为`label`)引用实现, 并带前缀`tab:`, 由`\@ref(tab:label)`实现. 例如

```
本章共出现二张表格，即表\@ref(tab:tab3-1)和表\@ref(tab:tab3-2).
```

输出为：

本章共出现二张表格，即表\@ref(tab:tab3-1)和表\@ref(tab:tab3-2).

**注**: 表格中的caption(题图)由文本引用生成.


\printbibliography[segment=\therefsegment, heading=subbibliography, title={参考文献}]


# `Bookdown`中的图形 {#figures}

## 由`R`生成单个图形示例 {#sec5-1}

\indent
这是第\@ref(figures) 章的内容， 讲述浮动对象图形的标签与引用. [@xie2015; @bookdown2016]

(ref:fig4p1) `iris`数据集`Petal.Length} ~ Species`的箱线图.

<div class="figure">
<img src="005-figures_files/figure-epub3/fig4-1-1.png" alt="(ref:fig4p1)"  />
<p class="caption">(\#fig:fig4-1)(ref:fig4p1)</p>
</div>

## 由`R`生成两个图形并置示例  {#sec5-2}

在`R`的代码块选项中设置`out.width='50%'`, `fig.show='hold'`就可获得二个图形的并置. 

(ref:fig4p2) `iris`数据集`Petal.Length} ~ Species` 的散点图.  右侧的图像中散点类型通过`Species`因子的水平给出，见图例. 直线为数据集拟合线性模型的结果.

<div class="figure">
<img src="005-figures_files/figure-epub3/fig4-2-1.png" alt="(ref:fig4p2)" width="50%" /><img src="005-figures_files/figure-epub3/fig4-2-2.png" alt="(ref:fig4p2)" width="50%" />
<p class="caption">(\#fig:fig4-2)(ref:fig4p2)</p>
</div>

## 由`R`生成两个图形堆叠示例  {#sec5-3}

\indent
在`R`的代码块选项中设置`out.width='90%'`, `fig.show='hold'`就可获得二个图形的并置. 

(ref:fig4p3) `iris`数据集`Petal.Length} ~ Species` 的散点图.  下方的图像中散点类型通过`Species`因子的水平给出，见图例. 直线为数据集拟合线性模型的结果.

<div class="figure">
<img src="005-figures_files/figure-epub3/fig4-3-1.png" alt="(ref:fig4p3)" width="90%" /><img src="005-figures_files/figure-epub3/fig4-3-2.png" alt="(ref:fig4p3)" width="90%" />
<p class="caption">(\#fig:fig4-3)(ref:fig4p3)</p>
</div>

## 静态图形示例 {#sec5-4}

\indent
在`Bookdwon`中插入本地图形可使用命令(示例为`R`logo)

```r
knitr::include_graphics("figures/Rlogo.png")
```

(ref:fig4p4) R logo

<div class="figure" style="text-align: center">
<img src="figures/Rlogo.png" alt="(ref:fig4p4)" width="70%" />
<p class="caption">(\#fig:fig4-4)(ref:fig4p4)</p>
</div>

## 图形引用 {#sec5-5}

\indent
图形引用通过`R`代码块的标签引用, 并带前缀`fig:`, 例如

```
图\@ref(fig:fig4-2)和图\@ref(fig:fig4-3)为两个图的并置与堆叠. 
```
输出为: 

图\@ref(fig:fig4-2)和图\@ref(fig:fig4-3)为两个图的并置与堆叠. 


\printbibliography[segment=\therefsegment, heading=subbibliography, title={参考文献}]


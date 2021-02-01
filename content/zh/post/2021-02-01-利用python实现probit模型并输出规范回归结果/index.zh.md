---
# Documentation: https://wowchemy.com/docs/managing-content/

title: "利用python实现probit模型并输出规范回归结果"
subtitle: ""
summary: "本文尝试用Python实现Probit回归，同时像Stata那样输出规范的回归结果。"
authors: []
tags: []
categories: []
date: 2021-02-01T17:30:57+08:00
lastmod: 2021-02-01T17:30:57+08:00
featured: false
draft: false

# Featured image
# To use, add an image named `featured.jpg/png` to your page's folder.
# Focal points: Smart, Center, TopLeft, Top, TopRight, Left, Right, BottomLeft, Bottom, BottomRight.
image:
  caption: ""
  focal_point: ""
  preview_only: false

# Projects (optional).
#   Associate this post with one or more of your projects.
#   Simply enter your project's folder or file name without extension.
#   E.g. `projects = ["internal-project"]` references `content/project/deep-learning/index.md`.
#   Otherwise, set `projects = []`.
projects: []
---
最近计量课刚学了用Stata实现Probit回归，不得不说Stata确实香，操作简单不说，还能自动导出规范的回归结果。但作为一个爱折腾的人，还是希望用Python实现相同功能。本文尝试用Python实现Probit回归，同时像Stata那样输出规范的回归结果。同时，本文首次使用blogdown来写博文，可以将每一段代码的结果也展示出来，是真的很强大(给[Yihui大神](https://yihui.org/)点赞)，不但写博文更方便了，阅读体验也大大提升。

<!--more-->

# 1. 理论基础

略，感觉自己目前将不太清楚。

# 2. 案例


## 2.1 数据介绍


这里用的数据是计量经济学老师提供的有关妇女就业情况的数据。如下表，其中work1和work是两种口径下统计的是否就业的指标，1表示就业，0表示未就业。（具体是什么口径要原始数据，老师给的这个数据是处理过后的，可以直接用于回归）。我将此数据上传到了我的github，有需要的朋友可以[点击下载](https://github.com/nick-zhy/blog_items/tree/main/probit)。

``` python
import numpy as np
import pandas as pd
from statsmodels.discrete.discrete_model import Probit
total = pd.read_excel('femaledata.xls')
total.head()
```

    ##    work1  work  female  age   edu  married  children
    ## 0    1.0   1.0       0   53   9.0        1       1.0
    ## 1    1.0   1.0       1   50   9.0        1       1.0
    ## 2    NaN   NaN       1   16  10.0        0       NaN
    ## 3    1.0   1.0       0   52  12.0        1       1.0
    ## 4    1.0   1.0       1   48  12.0        1       1.0

我们将妇女的数据筛选出来，因为我们重点关注的是影响妇女就业的因素。以下是描述性统计。

``` python
female = total[total['female']==1]
female.describe()
```

    ##              work1         work  female  ...          edu      married     children
    ## count  3529.000000  3969.000000  7495.0  ...  6957.000000  7495.000000  5635.000000
    ## mean      0.901955     0.912824     1.0  ...    10.516171     0.684189     1.410293
    ## std       0.297417     0.282128     0.0  ...     3.970129     0.464869     1.029336
    ## min       0.000000     0.000000     1.0  ...     0.000000     0.000000     0.000000
    ## 25%       1.000000     1.000000     1.0  ...     9.000000     0.000000     1.000000
    ## 50%       1.000000     1.000000     1.0  ...    11.000000     1.000000     1.000000
    ## 75%       1.000000     1.000000     1.0  ...    13.000000     1.000000     2.000000
    ## max       1.000000     1.000000     1.0  ...    35.000000     1.000000     9.000000
    ## 
    ## [8 rows x 7 columns]

## 2.2 调用函数


第一个回归模型，被解释变量是work，被解释变量是年龄、教育年限、婚姻状态与后代数量。

``` python
probit_model1 = Probit.from_formula('work ~ age + edu + married + children', data=female)
reg1 = probit_model1.fit()
```

    ## Optimization terminated successfully.
    ##          Current function value: 0.294420
    ##          Iterations 6

``` python
print(reg1.summary())
```

    ##                           Probit Regression Results                           
    ## ==============================================================================
    ## Dep. Variable:                   work   No. Observations:                 3495
    ## Model:                         Probit   Df Residuals:                     3490
    ## Method:                           MLE   Df Model:                            4
    ## Date:                Mon, 25 Jan 2021   Pseudo R-squ.:                 0.01919
    ## Time:                        23:45:13   Log-Likelihood:                -1029.0
    ## converged:                       True   LL-Null:                       -1049.1
    ## Covariance Type:            nonrobust   LLR p-value:                 3.797e-08
    ## ==============================================================================
    ##                  coef    std err          z      P>|z|      [0.025      0.975]
    ## ------------------------------------------------------------------------------
    ## Intercept     -0.2175      0.268     -0.812      0.417      -0.743       0.308
    ## age            0.0136      0.004      3.411      0.001       0.006       0.021
    ## edu            0.0584      0.011      5.454      0.000       0.037       0.079
    ## married        0.2796      0.128      2.192      0.028       0.030       0.530
    ## children       0.0992      0.059      1.683      0.092      -0.016       0.215
    ## ==============================================================================

第二个回归模型，被解释变量换为另一种口径下的就业状态，即work1，解释变量不变。

``` python
probit_model2 = Probit.from_formula('work1 ~ age + edu + married + children', data=female)
reg2 = probit_model2.fit()
```

    ## Optimization terminated successfully.
    ##          Current function value: 0.316827
    ##          Iterations 6

``` python
print(reg2.summary())
```

    ##                           Probit Regression Results                           
    ## ==============================================================================
    ## Dep. Variable:                  work1   No. Observations:                 3094
    ## Model:                         Probit   Df Residuals:                     3089
    ## Method:                           MLE   Df Model:                            4
    ## Date:                Mon, 25 Jan 2021   Pseudo R-squ.:                 0.02879
    ## Time:                        23:45:13   Log-Likelihood:                -980.26
    ## converged:                       True   LL-Null:                       -1009.3
    ## Covariance Type:            nonrobust   LLR p-value:                 7.230e-12
    ## ==============================================================================
    ##                  coef    std err          z      P>|z|      [0.025      0.975]
    ## ------------------------------------------------------------------------------
    ## Intercept     -0.3945      0.281     -1.403      0.161      -0.946       0.157
    ## age            0.0120      0.004      2.871      0.004       0.004       0.020
    ## edu            0.0795      0.011      7.012      0.000       0.057       0.102
    ## married        0.2949      0.133      2.220      0.026       0.035       0.555
    ## children       0.0176      0.061      0.290      0.772      -0.101       0.136
    ## ==============================================================================

第三个回归模型换用Logit回归，需要从`statsmodel`导入Logit模块。

``` python
from statsmodels.discrete.discrete_model import Logit
logit_model = Logit.from_formula('work ~ age + edu + married + children', data=female)
reg3 = logit_model.fit()
```

    ## Optimization terminated successfully.
    ##          Current function value: 0.294598
    ##          Iterations 7

``` python
print(reg3.summary())
```

    ##                            Logit Regression Results                           
    ## ==============================================================================
    ## Dep. Variable:                   work   No. Observations:                 3495
    ## Model:                          Logit   Df Residuals:                     3490
    ## Method:                           MLE   Df Model:                            4
    ## Date:                Mon, 25 Jan 2021   Pseudo R-squ.:                 0.01860
    ## Time:                        23:45:13   Log-Likelihood:                -1029.6
    ## converged:                       True   LL-Null:                       -1049.1
    ## Covariance Type:            nonrobust   LLR p-value:                 6.873e-08
    ## ==============================================================================
    ##                  coef    std err          z      P>|z|      [0.025      0.975]
    ## ------------------------------------------------------------------------------
    ## Intercept     -0.6622      0.511     -1.296      0.195      -1.664       0.339
    ## age            0.0257      0.008      3.316      0.001       0.011       0.041
    ## edu            0.1114      0.021      5.382      0.000       0.071       0.152
    ## married        0.5452      0.237      2.300      0.021       0.081       1.010
    ## children       0.1984      0.119      1.671      0.095      -0.034       0.431
    ## ==============================================================================

第四个回归模型用普通的线性回归，即OLS模型。

``` python
from statsmodels.regression.linear_model import OLS
ols_model = OLS.from_formula('work ~ age + edu + married + children', data=female)
reg4 = ols_model.fit()
print(reg4.summary())
```

    ##                             OLS Regression Results                            
    ## ==============================================================================
    ## Dep. Variable:                   work   R-squared:                       0.011
    ## Model:                            OLS   Adj. R-squared:                  0.010
    ## Method:                 Least Squares   F-statistic:                     9.445
    ## Date:                Mon, 25 Jan 2021   Prob (F-statistic):           1.36e-07
    ## Time:                        23:45:13   Log-Likelihood:                -549.80
    ## No. Observations:                3495   AIC:                             1110.
    ## Df Residuals:                    3490   BIC:                             1140.
    ## Df Model:                           4                                         
    ## Covariance Type:            nonrobust                                         
    ## ==============================================================================
    ##                  coef    std err          t      P>|t|      [0.025      0.975]
    ## ------------------------------------------------------------------------------
    ## Intercept      0.6729      0.042     16.064      0.000       0.591       0.755
    ## age            0.0020      0.001      3.373      0.001       0.001       0.003
    ## edu            0.0082      0.002      5.329      0.000       0.005       0.011
    ## married        0.0525      0.023      2.332      0.020       0.008       0.097
    ## children       0.0124      0.008      1.559      0.119      -0.003       0.028
    ## ==============================================================================
    ## Omnibus:                     1959.115   Durbin-Watson:                   1.839
    ## Prob(Omnibus):                  0.000   Jarque-Bera (JB):            10269.752
    ## Skew:                          -2.839   Prob(JB):                         0.00
    ## Kurtosis:                       9.187   Cond. No.                         395.
    ## ==============================================================================
    ## 
    ## Warnings:
    ## [1] Standard Errors assume that the covariance matrix of the errors is correctly specified.

## 2.3 边际效应


以模型一回归结果`reg1`为例，用`get_margeff()`方法就可以得到其边际效应。有关这个函数的具体参数及用法可以参考[官方文档](https://www.statsmodels.org/stable/generated/statsmodels.discrete.discrete_model.ProbitResults.get_margeff.html?highlight=get_margeff#statsmodels.discrete.discrete_model.ProbitResults.get_margeff)

``` python
reg1.get_margeff(at='overall', method='dydx').summary()
```

    ## <class 'statsmodels.iolib.summary.Summary'>
    ## """
    ##        Probit Marginal Effects       
    ## =====================================
    ## Dep. Variable:                   work
    ## Method:                          dydx
    ## At:                           overall
    ## ==============================================================================
    ##                 dy/dx    std err          z      P>|z|      [0.025      0.975]
    ## ------------------------------------------------------------------------------
    ## age            0.0022      0.001      3.404      0.001       0.001       0.003
    ## edu            0.0092      0.002      5.421      0.000       0.006       0.013
    ## married        0.0442      0.020      2.190      0.029       0.005       0.084
    ## children       0.0157      0.009      1.681      0.093      -0.003       0.034
    ## ==============================================================================
    ## """

从回归结果来看，四个解释变量都有显著边际影响。以年龄为例，边际效应结果可以解释为：妇女年龄每增加一岁，平均而言，妇女就业的概率增加0.0022。

`get_margeff()`的参数中，`method=dydx`表示解释变量的单位变动造成被解释变量的变动。还可以选择`eyex`，表示解释变量的百分比单位变动造成解释变量的百分比变动。具体可参见[文档](https://www.statsmodels.org/stable/generated/statsmodels.discrete.discrete_model.ProbitResults.get_margeff.html?highlight=get_margeff#statsmodels.discrete.discrete_model.ProbitResults.get_margeff)。

2.4 输出结果
------------

上面部分我们得到了四个回归结果，如果我们想将其导出为规范的学术论文回归结果，需要将它们汇总进行进一步的处理。Python里面能最好做到这样功能的命令是`statsmodels.iolib.summary2`中的`summary_col`。

-   `results`表示回归结果，
-   `model_names`指定回归结果的名称，
-   `regressor_order`指定解释变量的顺序，
-   `stars`：是否显示星星
-   `float_format`: 指定保留小数位数
-   `drop_omitted`:
    是否不显示`regressor_order`中未指定的解释变量，默认False
-   `info_dict`：指定额外显示的信息，如样本数量、R方或其他回归结果信息，dict格式

示例如下：

``` python
from statsmodels.iolib.summary2 import *
reg_sum = summary_col(results=[reg1, reg2, reg3, reg4],
            model_names=['model1', 'model2', 'model3', 'model4'],
            regressor_order=['age', 'children', 'edu', 'married', 'Intercept'],
            stars = True, 
            float_format='%.4f', 
            drop_omitted = True, 
            info_dict = {'':lambda x: '','':lambda x: '',
                         'Observation':lambda x:str(int(x.nobs)),
                         'R-squ': lambda x: float(x.rsquared), 
                         'Pseudo R-squ': lambda x: float(x.prsquared)}) 
reg_sum
```

    ## <class 'statsmodels.iolib.summary2.Summary'>
    ## """
    ## 
    ## ====================================================
    ##                model1    model2    model3    model4 
    ## ----------------------------------------------------
    ## age          0.0136*** 0.0120*** 0.0257*** 0.0020***
    ##              (0.0040)  (0.0042)  (0.0078)  (0.0006) 
    ## children     0.0992*   0.0176    0.1984*   0.0124   
    ##              (0.0590)  (0.0606)  (0.1187)  (0.0080) 
    ## edu          0.0584*** 0.0795*** 0.1114*** 0.0082***
    ##              (0.0107)  (0.0113)  (0.0207)  (0.0015) 
    ## married      0.2796**  0.2949**  0.5452**  0.0525** 
    ##              (0.1276)  (0.1328)  (0.2370)  (0.0225) 
    ## Intercept    -0.2175   -0.3945   -0.6622   0.6729***
    ##              (0.2680)  (0.2812)  (0.5109)  (0.0419) 
    ##                                                     
    ## Observation  3495      3094      3495      3495     
    ## R-squ                                      0.0107   
    ## Pseudo R-squ 0.0192    0.0288    0.0186             
    ## ====================================================
    ## Standard errors in parentheses.
    ## * p<.1, ** p<.05, ***p<.01
    ## """

如何将上述汇总的回归结果到处呢？`summary_col`有三种导出方法，分别为`as_text()`，`as_latex()`，`as_html()`。可以分别导出为文本文档、$\\LaTeX$命令、HTML命令。目前还没找到很好的，导出为excel或者csv的命令。

``` python
print(reg_sum.as_text())
```

    ## 
    ## ====================================================
    ##                model1    model2    model3    model4 
    ## ----------------------------------------------------
    ## age          0.0136*** 0.0120*** 0.0257*** 0.0020***
    ##              (0.0040)  (0.0042)  (0.0078)  (0.0006) 
    ## children     0.0992*   0.0176    0.1984*   0.0124   
    ##              (0.0590)  (0.0606)  (0.1187)  (0.0080) 
    ## edu          0.0584*** 0.0795*** 0.1114*** 0.0082***
    ##              (0.0107)  (0.0113)  (0.0207)  (0.0015) 
    ## married      0.2796**  0.2949**  0.5452**  0.0525** 
    ##              (0.1276)  (0.1328)  (0.2370)  (0.0225) 
    ## Intercept    -0.2175   -0.3945   -0.6622   0.6729***
    ##              (0.2680)  (0.2812)  (0.5109)  (0.0419) 
    ##                                                     
    ## Observation  3495      3094      3495      3495     
    ## R-squ                                      0.0107   
    ## Pseudo R-squ 0.0192    0.0288    0.0186             
    ## ====================================================
    ## Standard errors in parentheses.
    ## * p<.1, ** p<.05, ***p<.01

``` python
print(reg_sum.as_latex())
```

    ## \begin{table}
    ## \caption{}
    ## \begin{center}
    ## \begin{tabular}{lcccc}
    ## \hline
    ##              &   model1  &   model2  &   model3  &   model4   \\
    ## \midrule
    ## age          & 0.0136*** & 0.0120*** & 0.0257*** & 0.0020***  \\
    ##              & (0.0040)  & (0.0042)  & (0.0078)  & (0.0006)   \\
    ## children     & 0.0992*   & 0.0176    & 0.1984*   & 0.0124     \\
    ##              & (0.0590)  & (0.0606)  & (0.1187)  & (0.0080)   \\
    ## edu          & 0.0584*** & 0.0795*** & 0.1114*** & 0.0082***  \\
    ##              & (0.0107)  & (0.0113)  & (0.0207)  & (0.0015)   \\
    ## married      & 0.2796**  & 0.2949**  & 0.5452**  & 0.0525**   \\
    ##              & (0.1276)  & (0.1328)  & (0.2370)  & (0.0225)   \\
    ## Intercept    & -0.2175   & -0.3945   & -0.6622   & 0.6729***  \\
    ##              & (0.2680)  & (0.2812)  & (0.5109)  & (0.0419)   \\
    ##              &           &           &           &            \\
    ## Observation  & 3495      & 3094      & 3495      & 3495       \\
    ## R-squ        &           &           &           & 0.0107     \\
    ## Pseudo R-squ & 0.0192    & 0.0288    & 0.0186    &            \\
    ## \hline
    ## \end{tabular}
    ## \end{center}
    ## \end{table}

``` python
print(reg_sum.as_html())
```

    ## <table class="simpletable">
    ## <tr>
    ##         <td></td>        <th>model1</th>    <th>model2</th>    <th>model3</th>    <th>model4</th>  
    ## </tr>
    ## <tr>
    ##   <th>age</th>          <td>0.0136***</td> <td>0.0120***</td> <td>0.0257***</td> <td>0.0020***</td>
    ## </tr>
    ## <tr>
    ##   <th></th>             <td>(0.0040)</td>  <td>(0.0042)</td>  <td>(0.0078)</td>  <td>(0.0006)</td> 
    ## </tr>
    ## <tr>
    ##   <th>children</th>      <td>0.0992*</td>   <td>0.0176</td>    <td>0.1984*</td>   <td>0.0124</td>  
    ## </tr>
    ## <tr>
    ##   <th></th>             <td>(0.0590)</td>  <td>(0.0606)</td>  <td>(0.1187)</td>  <td>(0.0080)</td> 
    ## </tr>
    ## <tr>
    ##   <th>edu</th>          <td>0.0584***</td> <td>0.0795***</td> <td>0.1114***</td> <td>0.0082***</td>
    ## </tr>
    ## <tr>
    ##   <th></th>             <td>(0.0107)</td>  <td>(0.0113)</td>  <td>(0.0207)</td>  <td>(0.0015)</td> 
    ## </tr>
    ## <tr>
    ##   <th>married</th>      <td>0.2796**</td>  <td>0.2949**</td>  <td>0.5452**</td>  <td>0.0525**</td> 
    ## </tr>
    ## <tr>
    ##   <th></th>             <td>(0.1276)</td>  <td>(0.1328)</td>  <td>(0.2370)</td>  <td>(0.0225)</td> 
    ## </tr>
    ## <tr>
    ##   <th>Intercept</th>     <td>-0.2175</td>   <td>-0.3945</td>   <td>-0.6622</td>  <td>0.6729***</td>
    ## </tr>
    ## <tr>
    ##   <th></th>             <td>(0.2680)</td>  <td>(0.2812)</td>  <td>(0.5109)</td>  <td>(0.0419)</td> 
    ## </tr>
    ## <tr>
    ##   <th></th>                 <td></td>          <td></td>          <td></td>          <td></td>     
    ## </tr>
    ## <tr>
    ##   <th>Observation</th>    <td>3495</td>      <td>3094</td>      <td>3495</td>      <td>3495</td>   
    ## </tr>
    ## <tr>
    ##   <th>R-squ</th>            <td></td>          <td></td>          <td></td>       <td>0.0107</td>  
    ## </tr>
    ## <tr>
    ##   <th>Pseudo R-squ</th>  <td>0.0192</td>    <td>0.0288</td>    <td>0.0186</td>       <td></td>     
    ## </tr>
    ## </table>

``` r
library(reticulate)
py_run_string("import os as os")
py_run_string("os.environ['QT_QPA_PLATFORM_PLUGIN_PATH'] = 'C:/Users/Hanyu/Anaconda3/Library/plugins/platforms'")
```

# 4. 总结

不得不说Stata确实是计量的神，虽然Python也有方便的统计模型的包，但是在结果导出上还是麻烦了许多。后续可能还是以Stata为主了，但是也尽量用Python实现，毕竟在数据处理方面Python还是永远滴神。理论部分还缺着，因为觉得自己功力还不够讲清楚，后面等自己觉得能说清楚了再来更新。


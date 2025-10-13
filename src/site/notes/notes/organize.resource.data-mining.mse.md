---
{"dg-publish":true,"permalink":"/notes/organize.resource.data-mining.mse/","title":"MSE"}
---


Среднее квадрата суммы отклонений предсказанных значений от эмпирических значений

$$MSE (Mean Square Error)  = \frac{\sum_{i=1}^n{\left(Y - \hat{Y}\right)^2}}{n}$$

## Матричная форма

it might be easier to remember 

$$MSE = \frac{RSS}{df}$$ 

- 
<div class="transclusion internal-embed is-loaded"><a class="markdown-embed-link" href="/notes/organize.resource.data-mining.rss/#matrichnaya-forma" aria-label="Open link"><svg xmlns="http://www.w3.org/2000/svg" width="24" height="24" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round" class="svg-icon lucide-link"><path d="M10 13a5 5 0 0 0 7.54.54l3-3a5 5 0 0 0-7.07-7.07l-1.72 1.71"></path><path d="M14 11a5 5 0 0 0-7.54-.54l-3 3a5 5 0 0 0 7.07 7.07l1.71-1.71"></path></svg></a><div class="markdown-embed">



## Матричная форма

$RSS=(Y-\hat{Y})^T(Y-\hat{Y})$


</div></div>

- 
<div class="transclusion internal-embed is-loaded"><div class="markdown-embed">





Degrees of freedom, often represented by $v$ or $df$, is the number of independent pieces of information used to calculate a statistic. 

$df=n−p$

- n - количество измерений
- p - ограничения

</div></div>


$$MSE=\frac{(Y-\hat{Y})^T(Y-\hat{Y})}{n}$$
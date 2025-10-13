---
{"dg-publish":true,"permalink":"/notes/organize-resource-data-mining-coefficient-of-determination/","title":"Coefficient of Determination"}
---


Coefficient of Determination $$R^2$$ - число от 0 до 1, которое показывает, насколько хорошо модель предсказывает значения.

Интерпритация

0 - модель не предсказывает значения
0-1 - модель предсказывает значения (больше - лучше)
1 - модель идеально предсказывает значения

$$R^2 = 1 - \frac{RSS}{TSS}$$

- 
<div class="transclusion internal-embed is-loaded"><a class="markdown-embed-link" href="/notes/organize-resource-data-mining-rss/" aria-label="Open link"><svg xmlns="http://www.w3.org/2000/svg" width="24" height="24" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round" class="svg-icon lucide-link"><path d="M10 13a5 5 0 0 0 7.54.54l3-3a5 5 0 0 0-7.07-7.07l-1.72 1.71"></path><path d="M14 11a5 5 0 0 0-7.54-.54l-3 3a5 5 0 0 0 7.07 7.07l1.71-1.71"></path></svg></a><div class="markdown-embed">





<https://en.wikipedia.org/wiki/Residual_sum_of_squares>

Квадрат суммы отклонений предсказанных значений от эмпирических значений.

$RSS=\sum_{i=1}^{n}(y_{i}-f(x_{i}))^{2}$

## Матричная форма

$RSS=(Y-\hat{Y})^T(Y-\hat{Y})$


</div></div>

- 
<div class="transclusion internal-embed is-loaded"><a class="markdown-embed-link" href="/notes/organize-resource-data-mining-tss/" aria-label="Open link"><svg xmlns="http://www.w3.org/2000/svg" width="24" height="24" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round" class="svg-icon lucide-link"><path d="M10 13a5 5 0 0 0 7.54.54l3-3a5 5 0 0 0-7.07-7.07l-1.72 1.71"></path><path d="M14 11a5 5 0 0 0-7.54-.54l-3 3a5 5 0 0 0 7.07 7.07l1.71-1.71"></path></svg></a><div class="markdown-embed">





<https://en.wikipedia.org/wiki/Total_sum_of_squares>


$TSS =\sum _{i=1}^{n}\left(y_{i}-{\bar {y}}\right)^{2}$

- $y_i$ - измерение $y$
- $\hat{y}$ - среднее всех измерений

## Матричная форма

$TSS=(Y- \bar{Y})^T(Y-\bar{Y})$


</div></div>


## Матричная форма

$$R^2 = 1 - \frac{(Y-\hat{Y})^T(Y-\hat{Y})}{(Y-\bar{Y})^T(Y-\bar{Y})}$$

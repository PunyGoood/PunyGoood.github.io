---
title: "实用积分技巧"
#date: 2024-01-06 18:13:52.872 +0800
summary: 'math'
weight: 1
# tags: ["first", "two"]
# categories: ["first"]
#author: "MaisJet"
showToc: true
TocOpen: false
hidemeta: false
comments: false
disableHLJS: true 
disableShare: true
hideSummary: false
searchHidden: false
ShowReadingTime: false
ShowBreadCrumbs: false
ShowPostNavLinks: false
---
{{< katex >}}


# $\int \frac{1}{(1+2cos^2\theta)^2} $



- 采取化为切值处理：
  $ \int {\frac{sec^4 \theta}{(3+tan^2 \theta )^2} } \mathrm{d}\theta $


- 这里有趣的是经典凑微分后，分子是一个很漂亮的结构：

$$
\int {\frac{1+tan^2 \theta }{(3+tan^2 \theta )^2} } \mathrm{d}tan \theta
$$

- 之后按有理函数积分。



# $ f^{\prime\prime}(x) \pm f(x)$

- 解微分方程即可，可记结论
  
  $\int {f^{\prime\prime}(x) + f(x)} \mathrm{d} x =(f^{\prime}(x) - f(x)) e^x$

  $\int {f^{\prime\prime}(x) - f(x)} \mathrm{d} x =(f^{\prime}(x) + f(x)) e^{-x}$
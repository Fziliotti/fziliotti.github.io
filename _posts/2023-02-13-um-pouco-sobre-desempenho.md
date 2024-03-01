---
title: Desempenho na Web
author: fziliotti
date: 2023-02-09 02:33:00 +0800
categories: [Desenvolvimento, Performance]
tags: [performance,frontend]
---

# Por que desempenho na Web é importante?

Além de ganhos indiscutíveis na experiência do usuário, a melhoria no desempenho ou otimização de performance na web (WPO), possui impactos em vendas de empresas, em distribuição de conteúdo ([pelo impacto no SEO e ranqueamento de websites](https://developer.chrome.com/blog/search-ads-speed/#speed-is-now-used-as-a-ranking-factor-for-mobile-searches)) e também, mesmo que indiretamente no gerenciamento de dados trafegados na rede, ainda que os [pesos das páginas crescem ao longo dos anos](https://httparchive.org/reports/page-weight#bytesTotal).

Recomendação de leitura:

- https://wpostats.com/
  - O que a melhora no desempenho pode impactar empresas.
- https://web.dev/tags/case-study/
  - Casos de estudo de diversas empresas divulgados pelo time do Google.
- https://httparchive.org/reports
  - Dados importantes sobre o estado atual da Web e histórico dos elementos relacionados à páginas e aplicaçÕes web.

# Como medir desempenho?

O desempenho de uma página inicialmente pode ser medido pelo tempo de carregamento das páginas, mas ao longo dos ultimos anos, medir o desempenho de um site está bastante atrelado à experiencia do usuário. Hoje uma das iniciativas mais interessantes é o projeto do WebVitals, que visa medir o tempo de carregamento (FCP, LCP), a estabilidade visual (CLS) e o tempo de interatividade (TTI, FID).

Teoria sobre as métricas.

- https://web.dev/vitals/

Existem muitas ferramentas de auditoria, mas essas são as que eu utilizei e percebi que são as mais comuns e completas:

- https://github.com/GoogleChrome/lighthouse
- https://gtmetrix.com/
- https://developers.google.com/speed

A tabela a seguir mostra uma comparação entre as ferramentas de auditoria e as métricas do Web Vitals:

![image](https://user-images.githubusercontent.com/28535210/184557314-74ca2903-b8d7-4ef1-904e-83738fde1617.png)

Fonte: https://web.dev/vitals-tools-2020/

# Como aplicar técnicas de melhoria de performance?

Para entender as técnicas de performance:

- https://www.patterns.dev/posts/loading-sequence/
- Existem otimizações nos elementos básicos existentes em uma página e aplicação web (HTML, CSS, JAVASCRIPT) que em geral são a base das otimizacões, um trabalho bem legal que reuniu várias dicas é o webDiet do Zeno Rocha, o link da página é https://browserdiet.com/
- Aplicar técnicas de melhorias que os próprios relatórios e auditorias da página podem reportar.
- Nunca esquecer o impacto que as imagens possuem no site e realizar as otimizações de imagens como: Prover qualidades adequadas para cada dispositivo, tamanhos e formatos adequados, bem como usar técnicas de carregamento lento, placeholder.

# Modelos de renderização

Estudar sobre os modelos de renderização existentes e o impacto de cada um nas métricas do Web Vitals, você pode começar por esse [link bem bacana](https://www.patterns.dev/posts/rendering-patterns/).

---

![image](https://user-images.githubusercontent.com/28535210/184284478-09b5289c-aa76-4c0a-8a3f-0b32900221a2.png)

---

Mapa mental que criei para reunir de maneira simplificado os elementos, técnicas e assuntos relacionados ao assunto de Desempenho na Web.

![image](/assets/img/web-perf/web-perf.png)

---

# Curiosidades

- Cada [100ms de latência custou à Amazon 1% de suas vendas](https://www.gigaspaces.com/blog/amazon-found-every-100ms-of-latency-cost-them-1-in-sales/).

- Em 2009 o Google realizou [experimentos](https://ai.googleblog.com/2009/06/speed-matters.html) que identificaram que a latência influencia bastante no envolvimento do usuário com as buscas. 400ms de latência podem levar a 0.21% de diminuição das buscas.

- A Optimizely, empresa de testes A/B, realizou [testes](https://blog.optimizely.com/2016/07/13/how-does-page-load-time-impact-engagement/) que identificaram o impacto negativo do tempo de carregamento. Inserindo 4s segundos de de delay no carregamento pôde diminuir 11.02% das visualizações de páginas, diminuindo até 44.19% caso o delay aumente para 20segundos.

- Após a divulgação do Google em 2018, indicando que a velocidade da página se tornaria um fator de classificação para pesquisa, após um ano, [o Google identificou](https://developers.google.com/search/blog/2019/04/user-experience-improvements-with-page) uma redução de 20% na taxa de abandono para navegações iniciadas a partir da pesquisa e para sites mais lentos, a performance das métricas focadas em usuários da WebVitals cresceram de 15% para 20%

  - Isso tudo no ano de 2018 em que os desenvolvedores executaram mais de um bilhão de auditorias no [PageSpeed Insights](https://pagespeed.web.dev/), para 200 milhões de URLs únicas.

- A adição das métricas Core do Web Vitals em 2020, foi uma das mais importantes contribuições do Google no tema de desempenho na web. E uma métrica interessante é que os sites que atingiram os limites para todos as três métricas (LCP,FID,CLS) tiveram até 24% menos taxas de abandono, e para e-commerces essa taxa foi de 22%, como visto neste artigo [do blog Chromium](https://blog.chromium.org/2020/05/the-science-behind-web-vitals.html).

- [Um estudo abrangente](https://web.dev/ndtv/) feito pela estação de notícias NDTV, indica que a melhoria das métricas LCP e CLS tiveram um impacto muito grande no engajamento e consumo de conteúdo. Uma melhoria de 55% no tempo de LCP juntamente com algumas mudanças no produto levaram à uma redução de 50% na taxa de rejeição.

- A empresa Vodafone, do setor de telecomunicações também identificou a correlação entre a melhora de desempenho nos sites com as métricas de negócio. [Através da realização de testes A/B](https://web.dev/vodafone/) focados especialmente na otimização do Web Vitals. Uma melhoria de 31% no LCP ocasiou alguns ganhos como: 8% de aumento nas vendas, 15% na taxa de visitas e 11% na visita em carrinhos.

- A empresa automotiva Renault, pôde identificar a correlação entre otimizar a métrica LCP e o engajamento de usuário com as métricas de negócio. Basicamente eles perceberam que uma melhoria de 1 segundo no LCP pôde levar a uma redução de 14 pontos percentuais (ppt) na taxa de rejeição e a um aumento de 13% nas conversões. O caso completo pode ser lido [nesse artigo](https://web.dev/renault/).

- A empresa de notícias Yahoo! no Japão, [identificou que otimizando a métrica CLS](https://web.dev/yahoo-japan-news/) em 0.2, o número de visualizações de página por sessão aumentou em 15%, o tempo de duração da sessão aumentou 13% e também tiveram uma diminuição da taxa de rejeição em 1.72%.

- Diminuindo 70% no tempo de LCP, [a empresa Agrofy](https://web.dev/agrofy/) verificou uma redução de 76% no número de abandonos enquanto a tela estava em carregamento.

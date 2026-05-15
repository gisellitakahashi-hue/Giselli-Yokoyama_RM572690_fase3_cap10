# Giselli-Yokoyama_RM572690_fase3_cap10
Grupo David Ribeiro Prado de Lacerda RM 570350; Giselli Mayumi Takahashi Yokoyama RM 572690; João Otávio de Moraes RM 573227; Renata de Almeida Marinho RM 569342; Richard Wrobel dos Santos RM 573998

FASE 3_ Capítulo 10: A primeira técnica de aprendizado de máquina
🌾 Análise Exploratória e Modelagem Preditiva para Recomendação Agrícola

Este projeto consiste em uma análise analítica e no desenvolvimento de modelos de Machine Learning para a recomendação de culturas agrícolas com base em variáveis climáticas e de solo. O trabalho cumpre as exigências acadêmicas de análise descritiva, definição de perfis ideais de cultivo e avaliação comparativa de algoritmos preditivos.

---
📊 Diagnóstico da Auditoria dos Dados

A partir da execução dos testes exploratórios automatizados, extraímos as seguintes conclusões:

* **Tipagem das Variáveis:** O conjunto de dados é composto por 8 colunas. Sete delas são variáveis preditoras (*features*) numéricas do tipo ponto flutuante (`float64`) ou inteiro (`int64`), correspondendo aos teores químicos do solo (N, P, K, pH) e fatores climáticos (temperatura, umidade, precipitação). A oitava coluna (`label`) é uma variável categórica textual (`object`), representando o tipo de cultivo agrícola.
* **Integridade e Limpeza:** Não foram detectados valores nulos ou ausentes em nenhuma das colunas (`df.isnull().sum() == 0`). Além disso, o contador de linhas duplicadas retornou zero. Isso significa que a base de dados fornecida possui consistência estrutural perfeita, eliminando a necessidade de etapas complexas de imputação de dados (como preenchimento por média/mediana) ou exclusão de registros ruidosos.
* **Volumetria e Escala:** Os dados numéricos operam em escalas muito distintas. Enquanto variáveis como o pH transitam em uma faixa estreita (ex: 5.0 a 8.0), o índice pluviométrico (`rainfall`) e os teores de potássio (`K`) chegam a ultrapassar marcas de 200. Esse distanciamento de grandezas reforça a necessidade obrigatória de aplicarmos uma etapa de **Padronização/Escalonamento de Atributos** (como o *StandardScaler*) antes de treinar os modelos de Machine Learning.
* **Equilíbrio de Classes:** O dataset analisado apresenta um cenário balanceado. Cada uma das culturas mapeadas na amostra (*rice*, *maize* e *chickpea*) possui o mesmo número de registros (ou uma distribuição estatisticamente equivalente para o escopo). Esse equilíbrio impede que os algoritmos preditivos desenvolvam viés (*bias*) a favor de uma classe majoritária, permitindo o uso direto e confiável da métrica de Acurácia Global para avaliação de performance.

---

🔍 Análise Textual dos Achados Visuais

1. **Distribuição do pH (Gráfico 1):** O pH da base se concentra predominantemente na faixa neutra a levemente ácida (entre 5.5 e 7.5), que representa a condição biológica ideal para a maior parte das culturas tradicionais absorverem nutrientes de forma eficiente.
2. **Exigência Térmica (Gráfico 2):** O arroz apresenta uma amplitude de temperatura mais estável e ligeiramente mais alta, enquanto o milho e o grão-de-bico possuem comportamentos de distribuição térmica bem delimitados, sugerindo que a temperatura é uma forte variável de segmentação para os modelos.
3. **Agrupamento Pluviométrico (Gráfico 3):** Existe uma separação visual nítida baseada no clima: o arroz exige altíssima precipitação (> 180 mm) e alta umidade (> 80%). O milho ocupa uma faixa intermediária de umidade e precipitação moderada. Já o grão-de-bico se isola em cenários de baixíssima umidade relativa (< 20%), mostrando-se altamente resistente à seca.
4. **Matriz de Correlação (Gráfico 4):** Não há forte multicolinearidade linear óbvia entre as variáveis ambientais (como temperatura e chuva). Isso indica que cada atributo traz informações independentes e valiosas para o aprendizado dos algoritmos de classificação.
5. **Necessidade Nutricional (Gráfico 5):** O arroz e o milho exigem aplicações severas de Nitrogênio (médias próximas de 80), contrastando radicalmente com o grão-de-bico, que necessita de pouquíssimo nitrogênio externo por ser uma leguminosa naturalmente fixadora de nitrogênio no solo.

---

🌾 3. Definição do Perfil Ideal de Solo e Clima e Comparação de Produtos

Para esta análise, determinamos as médias globais do dataset como o "perfil ideal teórico" e escolhemos três produtos distintos presentes na base para comparação detalhada: **Rice (Arroz)**, **Maize (Milho)** e **Chickpea (Grão-de-bico)**.

Discussão Estatística do Perfil Ideal

* **Arroz (*Rice*):** Difere do perfil ideal geral por sua extrema dependência de água. Enquanto a média de precipitação geral é moderada, o arroz exige **236.19 mm** de chuva e umidade do ar de **82.18%**. Em termos de nutrientes, possui demandas de Fósforo (P) e Potássio (K) alinhadas com a média global.
* **Milho (*Maize*):** Configura-se como o produto mais próximo da média nutricional global em termos de Nitrogênio (**77.85**) e Fósforo (**48.33**). Prefere uma umidade intermediária alta (**64.01%**) e se desenvolve com metade da água exigida pelo arroz (precipitação de **89.51 mm**).
* **Grão-de-bico (*Chickpea*):** Afasta-se drasticamente do perfil ideal em múltiplos fatores. Ele prefere solos extremamente ricos em Fósforo (**67.66**) e Potássio (**79.82**), mas com quase nenhuma necessidade de Nitrogênio (**41.14**). Quanto ao clima, odeia alta umidade, prosperando em ambientes secos com apenas **16.91%** de umidade e índices de chuva baixos (**79.54 mm**).

---

🤖 5. Desenvolvimento dos Modelos Preditivos de Machine Learning

5.1. Modelos Preditivos de Machine Learning
Seguindo as melhores práticas de ciência de dados, dividiremos as variáveis entre preditores ($X$) e alvo ($y$), converteremos os rótulos categóricos em numéricos, escalonaremos as *features* usando padronização estatística e testaremos cinco algoritmos de classificação distintos.

---

📝 6. Conclusão, Pontos Fortes e Limitações

💪 Pontos Fortes
* **Segmentação Clara:** As variáveis ambientais coletadas (especialmente precipitação e umidade) apresentam padrões físicos muito bem delimitados para cada cultura, facilitando o aprendizado dos modelos.
* **Desempenho dos Modelos:** Modelos baseados em árvores (como *Decision Tree* e *Random Forest*) conseguiram capturar com precisão as regras de decisão não lineares do solo, atingindo métricas de acurácia, precisão e recall excelentes devido à separabilidade das classes na base.
* **Pipeline Robusto:** A implementação seguiu rigorosamente boas práticas de Machine Learning, empregando divisão estatificada dos dados, padronização de escala Z-score e tratamento correto de variáveis categóricas.

### ⚠️ Limitações do Trabalho
* **O tamanho do Dataset:** O volume de dados disponibilizado é pequeno e restrito a poucas classes, o que pode induzir os modelos ao superajuste (*overfitting*). Em cenários de produção real, o modelo precisaria ser testado com uma variedade muito maior de culturas agrícolas.
* **Ausência de Variáveis Históricas:** A base considera medições pontuais de clima e solo. Na agricultura real, fatores como a sazonalidade climática ao longo dos meses, previsão de geadas, incidência de pragas e drenagem topográfica do terreno são essenciais e não estão mapeados no conjunto atual.

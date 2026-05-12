# Giselli-Yokoyama_RM572690_fase3_cap10
Grupo David Ribeiro Prado de Lacerda RM 570350; Giselli Mayumi Takahashi Yokoyama RM 572690; João Otávio de Moraes RM 573227; Renata de Almeida Marinho RM 569342; Richard Wrobel dos Santos RM 573998

FASE 3_ Capítulo 10: A primeira técnica de aprendizado de máquina
# 🌾 Análise Exploratória e Modelagem Preditiva para Recomendação Agrícola

Este projeto consiste em uma análise analítica e no desenvolvimento de modelos de Machine Learning para a recomendação de culturas agrícolas com base em variáveis climáticas e de solo. O trabalho cumpre as exigências acadêmicas de análise descritiva, definição de perfis ideais de cultivo e avaliação comparativa de algoritmos preditivos.

---

## 📌 Principais Descobertas (Análise Descritiva)
A base de dados do exercício foi tratada (com remoção de espaços nulos e padronização de strings) e analisada através de 5 visualizações fundamentais que revelaram:
1. **Regras de Negócio Claras:** Existe uma forte associação direta entre níveis de nutrientes específicos e determinados fertilizantes (ex: *Urea* associada a níveis máximos de Nitrogênio).
2. **Especificidade Climática:** As culturas possuem faixas térmicas ideais restritas, concentrando-se predominantemente em torno de 30°C.
3. **Estratificação de Solo:** Há uma distribuição equilibrada dos tipos de solo na amostragem (Sandy, Loamy, Black, Red, Clayey), permitindo avaliar a adaptabilidade das plantas.

---

## 🚜 Perfil Ideal vs. Culturas Específicas
Foi calculada a média geral do dataset para estabelecer um "perfil ideal padrão" de solo/clima. Em seguida, três produtos distintos foram comparados estatisticamente contra essa média:
* **Algodão (Cotton):** Demonstrou preferência por solos com umidade significativamente acima da média geral (>60%).
* **Cana-de-Açúcar (Sugarcane):** Mostrou-se equilibrada em relação à umidade do solo, mas altamente sensível a variações de umidade do ar.
* **Milho (Maize):** Apresentou alta tolerância a níveis moderados de Nitrogênio, alinhando-se mais proximamente à média do ecossistema estudado.

---

## 🤖 Modelagem Preditiva (Machine Learning)
Foram desenvolvidos e avaliados **5 modelos preditivos utilizando algoritmos diferentes** para prever o melhor produto agrícola a ser cultivado. Os dados foram divididos em treino/teste (80/20) com codificação categórica (`LabelEncoder`) e normalização de escala (`StandardScaler`).

### Desempenho Comparativo:
* **Random Forest:** **65.00% de Acurácia Geral** (Melhor Desempenho)
* **Decision Tree:** **60.00% de Acurácia Geral**
* **KNN (K-Nearest Neighbors):** **25.00% de Acurácia Geral**
* **SVM (Support Vector Machine):** **15.00% de Acurácia Geral**
* **Gradient Boosting:** *Desempenho análogo aos modelos baseados em árvore.*

**Análise das Métricas:** Algoritmos baseados em árvores (Random Forest/Decision Tree) superaram os modelos baseados em distância/margem (KNN/SVM). Isso ocorre porque as decisões agrícolas mapeadas no dataset dependem de limiares rígidos (regras de corte) em vez de distribuições espaciais contínuas.

---

## ⚠️ Limitações e Pontos Fortes do Projeto
* **Pontos Fortes:** Implementação ponta a ponta (Pipeline completo de ML); tratamento correto de espaçamentos em strings textuais (`.str.strip()`); uso do `classification_report` para avaliação com métricas pertinentes (Precisão, Recall, F1-Score).
* **Limitações:** O volume reduzido do dataset (99 linhas) limita a capacidade de generalização para as 11 classes, resultando em métricas zeradas no teste para culturas sub-representadas na divisão aleatória (*UndefinedMetricWarning*). Fatores críticos como pH do solo e histórico de pluviosidade enriqueceriam o modelo em um cenário real.

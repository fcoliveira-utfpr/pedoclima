# Controles climáticos e texturais da fertilidade dos solos da região Sul do Brasil: uma abordagem com aprendizado de máquina

**Coordenação:** Prof. Dr. Fabrício Correia de Oliveira — GAMBI-TEC, UTFPR Campus Santa Helena

---

## 1. Introdução e justificativa

A fertilidade dos solos do Sul do Brasil resulta da interação entre o material de origem, a textura, o clima e o histórico de uso e manejo. Os manuais de calagem e adubação adotam critérios de interpretação e metas de correção que valem para grandes regiões, e a estratificação se limita sobretudo às classes de argila. Ainda faltam estudos que quantifiquem, em escala regional, quanto o regime hídrico explica da variação da acidez e da saturação por bases. Também faltam estudos que avaliem se os critérios dos manuais refletem os padrões pedoclimáticos existentes.

Hoje esse tipo de análise é viável graças a bases abertas de dados de solo, a mapas contínuos de textura e uso do solo e a ferramentas de aprendizado de máquina interpretável.

## 2. Objetivos

### 2.1 Objetivo geral

Quantificar os controles climáticos e texturais sobre a química do solo na região Sul e avaliar se os critérios dos manuais de calagem e adubação correspondem às zonas pedoclimáticas identificadas.

### 2.2 Objetivos específicos

1. Construir uma base padronizada de atributos químicos da camada superficial (pH, V%, CTC, Al³⁺, matéria orgânica e P, quando disponível) para PR, SC e RS.
2. Quantificar a contribuição relativa do balanço hídrico climatológico, da textura e do uso do solo na variação desses atributos.
3. Produzir mapas digitais dos atributos químicos e avaliar sua incerteza.
4. Delimitar zonas pedoclimáticas de fertilidade.
5. Comparar as zonas com os critérios do *Manual de Adubação e Calagem para o Estado do Paraná* e do *Manual de Calagem e Adubação para os Estados do Rio Grande do Sul e de Santa Catarina*.

## 3. Hipóteses

- **H1:** O excedente hídrico anual explica parte significativa da variação de V% e Al³⁺, mesmo controlando os efeitos da textura e do uso do solo.
- **H2:** Existem zonas pedoclimáticas com perfis químicos distintos que não são captados pelos critérios atuais dos manuais.

## 4. Material e métodos

### 4.1 Área de estudo

Região Sul do Brasil (Paraná, Santa Catarina e Rio Grande do Sul).

### 4.2 Dados de solo

- SoilData 
- BDSolos / PronaSolos (Embrapa)

Os dados serão filtrados para a camada de 0–20 cm e harmonizados quanto ao método analítico e à profundidade.

### 4.3 Covariáveis

| Grupo | Variáveis |
|---|---|
| Clima | Balanço hídrico climatológico (excedente, deficiência e armazenamento), temperatura, precipitação, classificações climáticas (Köppen e Holdridge) |
| Solo | Areia, silte e argila (MapBiomas Solo), carbono orgânico |
| Relevo | Modelo digital de elevação e derivadas do relevo |
| Geologia | Material de origem |
| Uso e histórico | Ano de coleta; classe de uso e cobertura do MapBiomas no ano da coleta (ou no ano mais próximo da série) |

### 4.4 Uso do solo e histórico de manejo

Cada ponto receberá o ano de coleta e a classe de uso e cobertura do MapBiomas correspondente. As amostras serão estratificadas em vegetação nativa, pastagem e agricultura. Os modelos serão ajustados com o uso como covariável e também separadamente por estrato.

### 4.5 Processamento

As covariáveis serão extraídas em Python com Google Earth Engine.

### 4.6 Etapas analíticas

1. **Controles climáticos:** modelos lineares mistos e Random Forest/XGBoost, com interpretação por SHAP, para separar os efeitos do clima, da textura, do material de origem e do uso do solo.
2. **Mapeamento digital:** predição espacial de pH, V%, CTC e Al³⁺ com validação cruzada espacial e quantificação da incerteza.
3. **Zoneamento pedoclimático:** agrupamento por fuzzy c-means das variáveis químicas e climáticas, com o número de zonas escolhido por índices de validação.
4. **Confronto com os manuais:** comparação dos perfis químicos de cada zona, principalmente nos estratos agrícolas, com os níveis críticos e as metas de calagem dos dois manuais.

## 5. Contribuição e inovação

- Integra agrometeorologia e pedometria em escala regional.
- O clima entra como descritor físico do regime hídrico, e não apenas por médias de temperatura e chuva.
- O aprendizado de máquina interpretável é usado para explicar a variação da fertilidade, e não só para prevê-la.
- O confronto com dois manuais distintos da mesma região dá aplicação prática direta aos resultados.

## 6. Limitações e riscos

1. **Distribuição espacial dos pontos:** os pontos podem estar concentrados em algumas regiões. Para mitigar, serão usadas validação cruzada espacial e análise da densidade amostral.
2. **Heterogeneidade analítica:** os métodos variam entre levantamentos, como pH em água ou em CaCl₂ e diferentes extratores de P. Para mitigar, serão usadas funções de conversão ou a análise ficará restrita a subconjuntos homogêneos.
3. **Histórico de uso e manejo:** os dados vêm majoritariamente de levantamentos pedológicos de diferentes épocas, coletados sob diversos usos e históricos de manejo, em geral desconhecidos. Para evitar confundir efeitos pedoclimáticos com efeitos de manejo, o ano de coleta e o uso do solo serão incorporados à análise. A comparação com os manuais vai considerar principalmente os estratos agrícolas.
4. **Fósforo:** se houver poucos dados de P, essa análise será exploratória.

## 7. Cronograma (24 meses)

| Atividade | Meses |
|---|---|
| Levantamento, harmonização e controle de qualidade dos dados de solo | 1–4 |
| Balanço hídrico e extração das covariáveis (GEE) | 3–6 |
| Etapa 1 — Controles climáticos e texturais | 6–11 |
| Etapa 2 — Mapeamento digital e incerteza | 9–15 |
| Etapa 3 — Zoneamento pedoclimático | 14–18 |
| Etapa 4 — Comparação com os manuais | 17–21 |
| Redação dos artigos, publicação do código e dos dados | 19–24 |

## 8. Equipe e infraestrutura

- Coordenação: grupo GAMBI-TEC, UTFPR Campus Santa Helena.
- Possíveis colaborações: Laboratório de Pedometria da UTFPR.
- Infraestrutura: Python e Google Earth Engine, sem custo de licença de software.

## 9. Produtos esperados

1. Artigo sobre os controles climáticos e texturais da química do solo no Sul do Brasil.
2. Artigo sobre o zoneamento pedoclimático e a regionalização dos critérios de recomendação.
3. Base de dados harmonizada e código aberto neste repositório.
4. Orientações de TCC e de iniciação científica vinculadas às etapas do projeto.

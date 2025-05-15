Okay, aqui está o roteiro completo da sua apresentação, com os resumos técnicos integrados no início da fala de cada IHM individualmente.

---

**Roteiro de Falas Completo com Resumos Técnicos**

**Slide 1: Página de Título**

*   **(Início da apresentação)**
    *   "Bom dia/tarde a todos."
    *   "Meu nome é Diego Viana Gomes, sou aluno do PPGCC aqui da UFLA."
    *   "Hoje, apresentarei o trabalho intitulado 'Medidas de Dificuldade de Instância para problemas de classificação e regressão'."
    *   "Esta apresentação faz parte das atividades do programa e está sendo realizada em maio de 2025."

**Slide 2: O que é Instance Hardness (IH)**

*   **(Transição)** "Para começar, vamos definir o conceito central do nosso trabalho: o que é Instance Hardness, ou Dificuldade de Instância."
*   **(Ponto 1)** "Em sua essência, Instance Hardness busca caracterizar a dificuldade inerente de predizer corretamente o rótulo de uma *única* instância específica no seu conjunto de dados."
*   **(Ponto 2)** "Uma ideia chave aqui é que a dificuldade de uma instância não é avaliada em relação a um *único* modelo. Uma instância é considerada difícil se um *conjunto de preditores*, utilizando diferentes algoritmos e com diferentes vieses, não consegue prever seu rótulo corretamente. Isso sugere que a dificuldade reside nas propriedades da própria instância e de sua vizinhança no espaço de dados, e não apenas nas limitações de um modelo específico."

**Slide 3: IH em Classificação**

*   **(Transição)** "Vamos olhar agora como esse conceito se aplica especificamente em problemas de classificação."
*   **(Ponto 1)** "Em classificação, onde os rótulos são discretos, a avaliação da dificuldade de uma instância é baseada na sua *probabilidade média de classificação incorreta*. Essa probabilidade é calculada considerando a performance de um *pool diverso de algoritmos de classificação* sobre essa instância. Quanto mais modelos do pool errarem ou tiverem baixa confiança na predição do rótulo correto, maior será a dificuldade atribuída à instância."

**Slide 4: IH em Regressão**

*   **(Transição)** "Agora, para problemas de regressão, onde os rótulos são contínuos."
*   **(Ponto 1)** "Em regressão, não podemos usar diretamente a probabilidade de classe. A estratégia para quantificar a incerteza da predição para uma instância é analisar a *dispersão ou a variabilidade* entre as predições geradas por um *pool diverso de regressores* e o *valor real* do rótulo. Se diferentes modelos do pool geram predições muito diferentes entre si e distantes do valor real, isso indica que a instância é difícil."

**Slide 5: Instance Hardness Analysis (Seção)**

*   **(Transição)** "Com a base do que é Instance Hardness, vamos entrar na seção sobre Análise de Instance Hardness."
*   **(Apenas o título grande)** "Esta seção trata da análise aprofundada da dificuldade no nível da instância."

**Slide 6: Contexto (IHA)**

*   **(Transição)** "Qual o contexto para realizar essa análise?"
*   **(Ponto 1)** "Frequentemente, ao analisar um novo conjunto de dados, focamos em estimativas agregadas, como a acurácia média ou métricas gerais. A Instance Hardness Analysis, por outro lado, é uma abordagem mais aprofundada que nos permite entender *onde* a dificuldade se concentra no dataset e *por que* algumas instâncias são mais difíceis que outras. Isso nos ajuda a ter uma visão mais granular e refinada do conjunto de dados, indo além das propriedades globais."

**Slide 7: IH para Classificação (Formalização)**

*   **(Transição)** "Voltando à formalização, aqui está a fórmula para o IH do pool em classificação."
*   **(Conteúdo)** "Dado um conjunto de dados e uma instância $x_i$ com seu rótulo $y_i$, a dificuldade $IH_\mathcal{L}$ para um pool de classificadores $\mathcal{L}$ é calculada como 1 menos a média das probabilidades atribuídas pelos modelos $h_j$ do pool ao rótulo *correto* $y_i$ para a instância $x_i$. Ou seja, $1 - \frac{1}{|\mathcal{L}|} \sum^{|\mathcal{L}|}_{j=1} p(y_i | h_j(x_i))$. Quanto menor a probabilidade média do rótulo correto, maior o IH (mais próximo de 1), indicando maior dificuldade."

**Slide 8: IH para Classificação (Interpretação Formalização)**

*   **(Transição)** "A partir dessa fórmula, a interpretação é direta:"
*   **(Ponto 1)** "Instâncias com alto $IH_\mathcal{L}$ são consideradas \textbf{instâncias difíceis}. Elas são frequentemente mal classificadas pelo pool diverso, ou os modelos do pool atribuem uma baixa probabilidade ao seu rótulo real."
*   **(Ponto 2)** "Instâncias com baixo $IH_\mathcal{L}$ são \textbf{instâncias fáceis}. Elas são corretamente classificadas pela maioria, ou até por todos, os algoritmos do pool, com alta confiança no rótulo real."

**Slide 9: IH para Regressão (Formalização - Parte 1)**

*   **(Transição)** "Formalizando o IH para regressão, o primeiro passo é adaptar a ideia de 'acerto' ou 'proximidade' no contexto de valores contínuos."
*   **(Conteúdo)** "Como não temos probabilidades de classe, definimos 'acurácia' a partir da distância entre o valor predito e o valor real. Introduzimos $z$, que é a distância $d$ entre o rótulo real $y_i$ da instância $x_i$ e a predição $h(x_i)$ gerada por um modelo $h$. Quanto menor essa distância, maior o 'acerto'."

**Slide 10: IH para Regressão (Formalização - Parte 2)**

*   **(Transição)** "Para converter essa distância em uma medida que possa ser agregada de forma similar à classificação, usamos uma função de kernel exponencial."
*   **(Conteúdo)** "A fórmula para o $IH_\mathcal{L}$ em regressão é calculada como 1 menos a média, sobre os regressores $h_j$ do pool $\mathcal{L}$, de um termo exponencial baseado na distância $d(y_i,h_j(x_i))$ entre o rótulo real e a predição. O termo $exp(-\frac{d(y_i,h_j(x_i))}{\gamma})$ funciona como uma medida de 'similaridade' ou 'proximidade' ao valor real. Quanto maior a distância/erro, menor esse termo, e consequentemente maior o IH. $\gamma$ é uma constante de escala que ajusta a sensibilidade da métrica à magnitude dos erros. $|\mathcal{L}|$ é o número de regressores no pool."

**Slide 11: IH para Regressão (Interpretação Geral)**

*   **(Transição)** "A interpretação final do $IH_\mathcal{L}$ para regressão é análoga à classificação."
*   **(Conteúdo)** "A métrica $IH_\mathcal{L}$ nos dá uma estimativa de quão difícil é para o conjunto de regressores prever com precisão a instância $x_i$. Valores de $IH_\mathcal{L}$ mais próximos de 1 indicam maior dificuldade. Isso ocorre quando os modelos do pool têm predições que, em média, estão mais distantes do valor real."

**Slide 12: IHMs para Classificação (Seção)**

*   **(Transição)** "Com a base do que é Instance Hardness e sua formalização para classificação e regressão, vamos agora explorar algumas Medidas de Dificuldade de Instância, as IHMs, propostas na literatura, começando pelas IHMs para Classificação."
*   **(Apenas o título grande)** "Esta seção detalha algumas das IHMs mais relevantes para problemas de classificação."

**Slide 13: IHM Classificação (kDN)**

*   **(Transição)** "A primeira IHM de classificação que vamos ver é o k-Disagreeing Neighbors, ou kDN."
*   **(Resumo Técnico)** "\textbf{Tecnicamente, o kDN quantifica a porcentagem de vizinhos de classes diferentes entre os $k$ vizinhos mais próximos da instância $x_i$, sendo uma métrica baseada em k-vizinhos.} "
*   **(O que é)** "Em termos conceituais, mede a porcentagem dos `k` vizinhos mais próximos de uma instância que pertencem a classes diferentes da instância."
*   **(O que valores altos indicam)** "Valores altos de kDN indicam que a instância está cercada por exemplos de outras classes. Isso sugere que ela está localizada próxima a uma fronteira de decisão entre classes, ou que pode ser um ponto de ruído cercado por outras classes."
*   **(Usos comuns)** "É uma métrica eficaz para identificar instâncias que causam sobreposição de classes ou que são potencialmente ruído nos rótulos, pois estão em regiões misturadas do espaço de entrada."

**Slide 14: IHM Classificação (DCP)**

*   **(Transição)** "Em seguida, temos o Disjunct Class Percentage, DCP."
*   **(Resumo Técnico)** "\textbf{Tecnicamente, o DCP mede o complemento da pureza do nó folha de uma Árvore de Decisão (com poda) onde $x_i$ cai, sendo $1$ menos a porcentagem de instâncias no nó folha com o mesmo rótulo de $x_i$.} "
*   **(O que é)** "Ou seja, mede o complemento da porcentagem de instâncias no nó folha de uma Árvore de Decisão (poda) que possuem o mesmo rótulo da instância em questão."
*   **(O que valores altos indicam)** "Valores altos de DCP indicam que o nó folha onde a instância se encontra contém uma porcentagem baixa de exemplos da mesma classe. Isso significa que a região do espaço de entrada, definida por aquela folha da árvore, é misturada ou difícil de separar claramente pela árvore."
*   **(Usos comuns)** "Avalia a dificuldade com base na 'pureza' da região definida pela árvore. Captura bem a dificuldade causada por sobreposição de classes e ruído."

**Slide 15: IHM Classificação (TD)**

*   **(Transição)** "Outra métrica baseada em Árvores de Decisão é a Tree Depth, TD."
*   **(Resumo Técnico)** "\textbf{Tecnicamente, o TD mede a profundidade normalizada do nó folha de uma Árvore de Decisão (sem poda) onde a instância é classificada.} "
*   **(O que é)** "Mede a profundidade normalizada do nó folha de uma Árvore de Decisão (sem poda) onde a instância é classificada."
*   **(O que valores altos indicam)** "Valores altos de TD indicam que a instância está localizada em um nó folha muito profundo da árvore."
*   **(Usos comuns)** "Relaciona a dificuldade da instância com a complexidade da regra de decisão que a árvore precisa gerar para classificá-la. Instâncias difíceis tendem a exigir regras mais específicas e, portanto, caem mais fundo na estrutura da árvore."

**Slide 16: IHM Classificação (CLD)**

*   **(Transição)** "Agora, a Class Likelihood Difference, CLD."
*   **(Resumo Técnico)** "\textbf{Tecnicamente, o CLD mede a diferença entre a probabilidade estimada para o rótulo verdadeiro e a probabilidade máxima estimada para qualquer outro rótulo, utilizando estimativas de probabilidade (e.g., Naive Bayes).} "
*   **(O que é)** "Mede a diferença de probabilidade de uma instância pertencer à sua classe real e a probabilidade máxima de pertencer a qualquer outra classe (usando estimativa Naive Bayes)."
*   **(O que valores altos indicam)** "Valores altos de CLD indicam que essa diferença de probabilidade é pequena, significando que a instância não tem uma forte preferência por sua própria classe em comparação com outras."
*   **(Usos comuns)** "Avalia a confiança com que uma instância pode ser associada à sua classe com base nas distribuições das características. Apresenta-se como uma medidas mais eficazes para capturar a dificuldade de todas as fontes testadas, especialmente ruído nos rótulos e sobreposição de classes."

**Slide 17: IHM Classificação (F1_IHM)**

*   **(Transição)** "A seguir, Fraction of features in overlapping areas, F1_IHM."
*   **(Resumo Técnico)** "\textbf{Tecnicamente, o F1\_IHM quantifica a porcentagem de features da instância cujos valores caem nas regiões de sobreposição inter-classes, definidas por intervalos [min(max), max(min)] dos valores das features para pares de classes.} "
*   **(O que é)** "Mede a porcentagem de características da instância cujos valores caem em uma região de sobreposição definida pelos intervalos [min(max), max(min)] dos valores da característica para duas classes."
*   **(O que valores altos indicam)** "Valores altos indicam que a instância possui muitas características com valores em regiões onde há sobreposição entre as classes."
*   **(Usos comuns)** "Identifica a dificuldade intrínseca da instância relacionada à sobreposição de valores de suas características entre diferentes classes. É eficaz para detectar dificuldade causada por sobreposição de características."

**Slide 18: IHM Classificação (N1_IHM)**

*   **(Transição)** "Agora, medidas baseadas em grafos, como a Fraction of nearby instances of different classes, N1_IHM."
*   **(Resumo Técnico)** "\textbf{Tecnicamente, o N1\_IHM mede a porcentagem de vizinhos da instância em uma Árvore Geradora Mínima (MST) construída no espaço de entrada que pertencem a classes diferentes.} "
*   **(O que é)** "Mede a porcentagem de instâncias na Árvore Geradora Mínima (MST) que estão conectadas à instância em questão, mas que pertencem a classes diferentes."
*   **(O que valores altos indicam)** "Valores altos indicam que a instância está conectada a muitas instâncias de classes diferentes na MST, indicando proximidade (no espaço de entrada) a outras classes."
*   **(Usos comuns)** "Semelhante ao kDN, mas baseado na estrutura da MST, identifica instâncias que estão "misturadas" ou próximas a instâncias de outras classes no espaço de entrada. Eficaz para detectar instâncias próximas a fronteiras ou ruído."

**Slide 19: IHM Classificação (N2_IHM)**

*   **(Transição)** "Outra métrica de vizinhança/grafo é o Ratio of the intra-class and extra-class distances, N2_IHM."
*   **(Resumo Técnico)** "\textbf{Tecnicamente, o N2\_IHM mede o complemento da razão entre a distância da instância ao seu vizinho mais próximo da mesma classe e a distância ao seu vizinho mais próximo de classe diferente (Nearest Enemy).} "
*   **(O que é)** "Mede o complemento da razão entre a distância da instância para seu vizinho mais próximo da mesma classe (Nearest Neighbor) e a distância para seu vizinho mais próximo de uma classe diferente (Nearest Enemy)."
*   **(O que valores altos indicam)** "Valores altos indicam que a instância está relativamente mais próxima de seu "Nearest Enemy" do que de seu "Nearest Neighbor" da mesma classe."
*   **(Usos comuns)** "Quantifica a dificuldade com base na proximidade relativa a exemplos da própria classe versus exemplos de outras classes. É eficaz para identificar instâncias em regiões de fronteira de decisão."

**Slide 20: IHM Classificação (LSC_IHM)**

*   **(Transição)** "Seguindo nas métricas baseadas em vizinhança, temos a Local Set Cardinality, LSC_IHM."
*   **(Resumo Técnico)** "\textbf{Tecnicamente, o LSC\_IHM mede o complemento da cardinalidade relativa do Local Set, definido como o conjunto de instâncias da mesma classe mais próximas que o Nearest Enemy.} "
*   **(O que é)** "Mede o complemento da cardinalidade relativa do conjunto local, definido como o conjunto de instâncias da mesma classe que estão mais próximas da instância em questão do que seu "Nearest Enemy"."
*   **(O que valores altos indicam)** "Valores altos indicam que o conjunto local é pequeno em relação ao número total de instâncias da mesma classe, indicando que há poucas instâncias da mesma classe muito próximas em comparação com a proximidade de um "Nearest Enemy"."
*   **(Usos comuns)** "Avalia a densidade local da própria classe ao redor da instância em relação à sua separação de outras classes. Identifica instâncias em regiões esparsas ou misturadas."

**Slide 21: IHM Classificação (LSR)**

*   **(Transição)** "Relacionada à anterior, temos a Local Set Radius, LSR."
*   **(Resumo Técnico)** "\textbf{Tecnicamente, o LSR mede o complemento do raio normalizado do Local Set.} "
*   **(O que é)** "Mede o complemento do raio normalizado do conjunto local."
*   **(O que valores altos indicam)** "Valores altos indicam que o raio do conjunto local é pequeno, indicando que as instâncias da mesma classe que estão mais próximas do que o "Nearest Enemy" estão muito agrupadas."
*   **(Usos comuns)** "Avalia a compacidade da vizinhança local da mesma classe em relação à distância do "Nearest Enemy". Identifica instâncias em regiões onde a vizinhança da própria classe é muito "apertada" ou limitada."

**Slide 22: IHM Classificação (U)**

*   **(Transição)** "Vamos agora para a Usefulness, U."
*   **(Resumo Técnico)** "\textbf{Tecnicamente, o U mede o complemento da fração de outras instâncias para as quais a instância em questão pertence ao Local Set delas.} "
*   **(O que é)** "Mede o complemento da fração de \textit{outras} instâncias para as quais a instância em questão pertence ao "Local Set" delas."
*   **(O que valores altos indicam)** "Valores altos indicam que a instância em questão é o "Nearest Enemy" para um número relativamente pequeno de outras instâncias (menos "útil" para definir os Local Sets de outras instâncias)."
*   **(Usos comuns)** "Avalia quão "central" ou "representativa" uma instância é para a definição dos Local Sets de outras instâncias da mesma classe. Instâncias menos "úteis" (valores altos) podem ser mais difíceis."

**Slide 23: IHM Classificação (H)**

*   **(Transição)** "A próxima é a Harmfulness, H."
*   **(Resumo Técnico)** "\textbf{Tecnicamente, o H mede o número normalizado de instâncias para as quais a instância em questão é o Nearest Enemy.} "
*   **(O que é)** "Mede o número normalizado de instâncias para as quais a instância em questão é o "Nearest Enemy"."
*   **(O que valores altos indicam)** "Valores altos indicam que a instância em questão é o "Nearest Enemy" para muitas outras instâncias."
*   **(Usos comuns)** "Identifica instâncias que são significativas fontes de confusão para outras (seus "Nearest Enemies"). Geralmente, captura outliers ou instâncias em fronteiras difíceis."

**Slide 24: IHM Classificação (DegreeIHM)**

*   **(Transição)** "Finalizando as IHMs de classificação, temos métricas de centralidade em grafos, como a Degree centrality, Degree_IHM."
*   **(Resumo Técnico)** "\textbf{Tecnicamente, o Degree\_IHM mede o complemento da densidade de conexões (grau do vértice) da instância em um grafo de proximidade que conecta instâncias da mesma classe abaixo de um limiar de distância.} "
*   **(O que é)** "Mede o complemento da densidade de conexões (grau do vértice) da instância em um grafo de proximidade que conecta instâncias da mesma classe abaixo de um limiar de distância."
*   **(O que valores altos indicam)** "Valores altos indicam que a instância tem poucas conexões no grafo de proximidade, indicando que ela está em uma região menos densamente conectada de sua própria classe."
*   **(Usos comuns)** "Avalia a densidade local ou conectividade dentro da própria classe. É eficaz para identificar instâncias em regiões esparsas de sua classe, sendo útil para sobreposição e número de características."

**Slide 25: IHM Classificação (ClosenessIHM)**

*   **(Transição)** "Por fim, a Closeness centrality, Closeness_IHM."
*   **(Resumo Técnico)** "\textbf{Tecnicamente, o Closeness\_IHM mede o complemento da centralidade de proximidade no mesmo grafo de proximidade usado para o Degree\_IHM.} "
*   **(O que é)** "Mede o complemento da centralidade de proximidade no mesmo grafo de proximidade usado para $Degree_{IHM}$."
*   **(O que valores altos indicam)** "Valores altos indicam que a centralidade de proximidade é baixa, indicando que a instância está, em média, mais distante das outras instâncias da mesma classe no grafo."
*   **(Usos comuns)** "Avalia quão facilmente uma instância é "alcançável" ou conectada a outras instâncias de sua classe no grafo de proximidade. Captura instâncias que estão mais "afastadas" do centro do cluster de sua classe, sendo útil para sobreposição e número de características."

**Slide 26: IHMs para Regressão (Seção)**

*   **(Transição)** "Com o leque de IHMs de classificação apresentadas, vamos agora para a seção dedicada às Medidas de Instance Hardness para problemas de Regressão."
*   **(Apenas o título grande)** "Aqui, focaremos em métricas específicas ou adaptadas para a natureza contínua dos rótulos de regressão."

**Slide 27: IHM Regressão (CFE)**

*   **(Transição)** "Começando com a Collective Feature Efficiency, CFE."
*   **(Resumo Técnico)** "\textbf{Tecnicamente, o CFE mede a rodada normalizada em um processo iterativo onde instâncias com pequeno resíduo linear são removidas e a feature mais correlacionada com o restante é identificada.} "
*   **(O que é)** "Mede a rodada normalizada (`li/m`) em um processo iterativo onde instâncias com pequeno resíduo linear são removidas, e a feature mais correlacionada com o restante é identificada."
*   **(O que valores altos indicam)** "Valores altos indicam que a instância exigiu que mais features fossem analisadas (ou seja, foi removida em uma rodada posterior) para se obter um bom ajuste linear."
*   **(Usos comuns)** "Captura a dificuldade relacionada à linearidade e à informatividade das features individuais para aquela instância. Pode indicar que a instância não se ajusta bem a relações lineares simples com as features mais "fortes"."

**Slide 28: IHM Regressão (LE)**

*   **(Transição)** "A seguir, o Absolute Error after Linear fit, LE."
*   **(Resumo Técnico)** "\textbf{Tecnicamente, o LE mede o erro absoluto ($\left|\varepsilon_i\right|$) da instância após o ajuste de um modelo de Regressão Linear Múltipla ao conjunto de dados completo.} "
*   **(O que é)** "Mede o erro absoluto ($|\varepsilon_i|$) da instância após o ajuste de um modelo de Regressão Linear Múltipla ao conjunto de dados completo."
*   **(O que valores altos indicam)** "Valores altos indicam que a instância se desvia significativamente do que é previsto por um modelo linear global."
*   **(Usos comuns)** "Identifica instâncias que são difíceis para modelos lineares. É eficaz para capturar ruído nos rótulos de saída e a dificuldade imposta pela correlação entre as features de entrada (Effective Rank)."

**Slide 29: IHM Regressão (S1IHM)**

*   **(Transição)** "Agora, métricas baseadas em vizinhança/distribuição, como a Output Distribution, S1_IHM."
*   **(Resumo Técnico)** "\textbf{Tecnicamente, o S1\_IHM mede a média das diferenças absolutas entre o valor de saída da instância e os valores de saída de seus vizinhos conectados na Árvore Geradora Mínima (MST) construída no espaço de entrada.} "
*   **(O que é)** "Mede a média das diferenças absolutas entre o valor de saída da instância ($y_i$) e os valores de saída dos seus vizinhos conectados na Árvore Geradora Mínima (MST) construída no espaço de entrada."
*   **(O que valores altos indicam)** "Valores altos indicam que a instância está conectada a vizinhos na MST com valores de saída mais diferentes."
*   **(Usos comuns)** "Avalia a suavidade da distribuição de saída no espaço de entrada, conforme refletido pela MST. Captura dificuldade quando vizinhos próximos no espaço de entrada têm valores de saída muito distintos. Eficaz para capturar variação no número de instâncias e número de features."

**Slide 30: IHM Regressão (S2IHM)**

*   **(Transição)** "Complementar à anterior, temos a Input Distribution, S2_IHM."
*   **(Resumo Técnico)** "\textbf{Tecnicamente, o S2\_IHM mede a distância Euclidiana média entre pares de exemplos 'vizinhos' após ordenar todas as instâncias pelos seus valores de saída.} "
*   **(O que é)** "Mede a distância Euclidiana entre pares de exemplos "vizinhos" após ordenar todas as instâncias pelos seus valores de saída."
*   **(O que valores altos indicam)** "Instâncias com valores de saída semelhantes estão distantes no espaço de entrada."
*   **(Usos comuns)** "Complementa $S1_{IHM}$. Avalia quão agrupadas estão instâncias com valores de saída semelhantes no espaço de entrada. Captura dificuldade quando instâncias com saídas próximas estão dispersas no espaço de entrada. Eficaz para capturar variação no número de features e Effective Rank."

**Slide 31: IHM Regressão (S3IHM)**

*   **(Transição)** "Finalmente, o Squared Error of k-nearest neighbor, S3_IHM."
*   **(Resumo Técnico)** "\textbf{Tecnicamente, o S3\_IHM mede o Erro Quadrático da predição de um regressor k-Nearest Neighbor (com k=5) para a instância, usando validação leave-one-out.} "
*   **(O que é)** "Mede o Erro Quadrático ($SE$) da predição de um regressor k-Nearest Neighbor ($kNN$, com $k=5$) para a instância, usando validação leave-one-out."
*   **(O que valores altos indicam)** "Valores altos indicam que a predição do $kNN$ para a instância se desvia significativamente do valor de saída real."
*   **(Usos comuns)** "Avalia a dificuldade em prever a saída da instância usando um método simples baseado em vizinhança. É eficaz para capturar ruído nos rótulos de saída e a dificuldade imposta pelo Effective Rank."

**Slide 32: Experimentos (Seção)**

*   **(Transição)** "Com o leque de IHMs apresentado, vamos agora detalhar os experimentos que realizamos para avaliar o comportamento dessas medidas."
*   **(Apenas o título)** "Nossa avaliação buscou entender como essas IHMs se comportam sob diferentes condições controladas."

**Slide 33: Experimentos (Objetivos)**

*   **(Transição)** "Os principais objetivos dos experimentos foram:"
*   **(Ponto 1)** "Verificar como as IHMs se comportam em datasets com diferentes fontes e níveis de dificuldade que controlamos, para entender o que cada métrica mede."
*   **(Ponto 2)** "Analisar a correlação entre os valores de cada IHM individual e a 'hardness verdadeira' da instância, que é a dificuldade medida pelo IH do pool de modelos de Machine Learning, considerado o nosso 'gold standard' de dificuldade."

**Slide 34: Experimentos (Metodologia Dados Sintéticos)**

*   **(Transição)** "A metodologia se baseou fortemente no uso de dados sintéticos."
*   **(Ponto 1)** "Utilizamos funções geradoras de datasets do scikit-learn: `make_blobs` para classificação e `make_regression` para regressão."
*   **(Ponto 2)** "A grande vantagem de usar dados sintéticos é que ela nos permite *controlar* diretamente a fonte e o nível de dificuldade dos dados. Por exemplo, podemos criar datasets com mais ou menos ruído, maior ou menor sobreposição entre classes, ou diferentes estruturas de features. Isso é crucial para isolar o impacto de cada fator na dificuldade da instância."

**Slide 35: Experimentos (Fontes Dificuldade Classificação)**

*   **(Transição)** "Para classificação, variamos as seguintes fontes de dificuldade:"
*   **(Lista)** "O número de Instâncias, o número de Features, o número de Classes, o Nível de Sobreposição (Overlap) entre as classes, e a Taxa de Ruído nos Rótulos (Label Flip)."
*   **(IH (Pool))** "Para o IH do pool de classificadores, observamos uma tendência geral de aumento da dificuldade com o aumento da sobreposição, ruído, número de features e número de classes. A variação no número de instâncias teve um impacto menos uniforme na dificuldade agregada."

**Slide 36: Experimentos (Dificuldade Classificação - Figura 1)**

*   **(Transição)** "Esta figura ilustra o comportamento do IH medido pelo pool de classificadores em resposta às diferentes fontes de dificuldade."
*   **(Conteúdo da figura)** "No eixo horizontal, vemos as diferentes fontes de dificuldade, e em cada gráfico, a variação do nível de dificuldade controlada (crescente da esquerda para a direita). O eixo vertical mostra o valor médio do IH do pool. Confirmamos que o IH do pool, nossa medida de 'hardness verdadeira', reage como esperado ao aumentar as fontes controladas de dificuldade, especialmente para sobreposição, ruído e número de classes/features."

**Slide 37: Experimentos (Fontes Dificuldade Regressão)**

*   **(Transição)** "Para regressão, as fontes de dificuldade que variamos foram:"
*   **(Lista)** "O número de Instâncias, o número de Features, o Nível de Ruído (Noise level), a Força da Cauda da distribuição de erro (Tail Strength), e o Effective Rank, que mede a correlação linear entre as features de entrada."
*   **(IH (Pool))** "O IH do pool de regressores mostrou uma tendência clara de aumento com o aumento do nível de ruído e da força da cauda. Para o número de instâncias e features, o impacto no IH foi menos pronunciado e uniforme."

**Slide 38: Experimentos (Dificuldade Regressão - Figura 4)**

*   **(Transição)** "Similarmente, esta figura mostra o comportamento do IH do pool para os datasets de regressão sintéticos."
*   **(Conteúdo da figura)** "Vemos aqui o IH médio do pool (eixo vertical) em função do nível crescente das diferentes fontes de dificuldade (eixo horizontal). É visível o aumento do IH com o ruído e a força da cauda, validando o uso do IH do pool como referência também para regressão."

**Slide 39: Experimentos (Medição Hardness Verdadeira - IH do Pool)**

*   **(Transição)** "Para calcular a 'hardness verdadeira' de cada instância, usamos o IH baseado em pools diversos de modelos, conforme as fórmulas que apresentamos anteriormente."
*   **(Conteúdo)** "Para classificação, o pool incluiu modelos como SVMs, Random Forest, Gradient Boosting, etc., que possuem diferentes vieses de aprendizado. Para regressão, usamos AdaBoost, SVM para regressão, Random Forest, etc. A medição foi feita usando validação cruzada de 5 folds, com um processo interno de tuning de hiperparâmetros com 3 folds, garantindo que a performance dos modelos do pool fosse razoável em cada fold e a medida de IH fosse robusta."

**Slide 40: Experimentos (Análise Resultados Intro Visualização - Boxplots)**

*   **(Transição)** "Para analisar os resultados do comportamento das IHMs individuais, usamos principalmente duas formas de visualização."
*   **(Ponto 1)** "A primeira são os Boxplots. Eles nos ajudam a visualizar a distribuição dos valores de cada IHM para os diferentes datasets gerados, permitindo ver como a distribuição da métrica muda à medida que a dificuldade controlada aumenta."

**Slide 41: Experimentos (Boxplots IHMs Classificação - Figura 2)**

*   **(Transição)** "Aqui estão os boxplots para as IHMs de classificação."
*   **(Conteúdo da figura)** "Cada linha representa uma IHM, e as colunas mostram a distribuição dos valores dessa IHM para os diferentes níveis de dificuldade controlada (da esquerda para a direita, dificuldade crescente). Podemos observar como o valor mediano e a amplitude dos valores de algumas IHMs, como o CLD, o kDN ou as métricas de grafos, reagem ao aumento da sobreposição ou do ruído."

**Slide 42: Experimentos (Boxplots IHMs Regressão - Figura 5)**

*   **(Transição)** "De forma análoga, estes são os boxplots para as IHMs de regressão."
*   **(Conteúdo da figura)** "Cada linha é uma IHM de regressão, e as colunas são os níveis de dificuldade. Vemos, por exemplo, que métricas como o LE e o S3_IHM mostram um aumento claro em seus valores médios e dispersão com o aumento do ruído. Já o CFE, por exemplo, tem uma distribuição de valores que varia menos entre os diferentes cenários de dificuldade testados."

**Slide 43: Experimentos (Análise Resultados Intro Correlações - Heatmaps)**

*   **(Transição)** "A segunda forma crucial de análise foi a das correlações, visualizada por heatmaps."
*   **(Ponto 1)** "Os heatmaps nos permitem visualizar a correlação entre cada IHM individual e a 'hardness verdadeira' medida pelo IH do pool de modelos, em diferentes cenários de dificuldade. Uma alta correlação positiva indica que a IHM individual 'rastreia' bem a dificuldade percebida pelos modelos diversos."

**Slide 44: Experimentos (Heatmap Classificação - Figura 3)**

*   **(Transição)** "Este é o heatmap de correlação para as IHMs de classificação."
*   **(Conteúdo da figura)** "As colunas representam as diferentes IHMs, e as linhas representam as correlações com o IH do pool em diferentes cenários ou o IH médio geral (a última linha). Nos concentramos na última linha para ver quais IHMs tiveram a maior correlação média com o IH do pool em todos os datasets. Cores mais escuras representam correlações mais altas e positivas. Podemos ver que várias métricas, como CLD, N2, Degree, Closeness e outras, apresentaram boas correlações com o IH do pool."

**Slide 45: Experimentos (Heatmap Regressão - Figura 6)**

*   **(Transição)** "Similarmente, este é o heatmap de correlação para as IHMs de regressão."
*   **(Conteúdo da figura)** "As colunas são as IHMs de regressão, e as linhas são correlações com o IH do pool em diferentes cenários ou o IH médio. A última linha mostra a correlação média. Observamos que, em geral, as correlações para regressão tendem a ser um pouco mais baixas do que para classificação. No entanto, métricas como LE, S3, Degree e S1 mostraram as melhores correlações com o IH do pool."

**Slide 46: Principais Resultados (Classificação)**

*   **(Transição)** "Resumindo os principais resultados para classificação:"
*   **(Ponto 1)** "As IHMs geralmente aumentam com a complexidade controlada dos datasets sintéticos."
*   **(Tabela)** "A tabela resume quais IHMs se mostraram mais eficazes para capturar dificuldade vinda de fontes específicas. Por exemplo:
    *   Sobreposição e Ruído: Foram bem capturados por muitas IHMs ($CLD$, medidas de vizinhança/grafos). $CLD$ foi eficaz para quase todas as fontes.
    *   Nº Features: Capturado por $Degree_{IHM}$, $Closeness_{IHM}$, $N2_{IHM}$ (relacionado à esparsidade).
    *   Nº Classes: Capturado por $KDN$, $DCP$, $CLD$, $N1_{IHM}$, $N2_{IHM}$, $H$.
    *   Por outro lado, o TD (Tree Depth) se mostrou menos eficaz e mais instável nos cenários testados."

**Slide 47: Principais Resultados (Regressão)**

*   **(Transição)** "Passando para os resultados em regressão:"
*   **(Ponto 1)** "As IHMs geralmente aumentam com a complexidade, mas as correlações com o IH do pool foram frequentemente mais baixas do que na classificação."
*   **(Tabela)** "Observamos que:
    *   Nº Features \& Effective Rank: Bem capturados por: $S1_{IHM}$, $S2_{IHM}$, Degree$_{IHM}$ (vizinhança/distância), $LE$, $S3_{IHM}$ (erro de ajuste)
    *   Ruído \& Tail Strength: Melhor capturados por: $LE$, $S3_{IHM}$ (erro de ajuste), Degree$_{IHM}$ (grafos)
    *   Nº Instâncias: Menos impacto uniforme no IH do pool. Capturado por: $S1_{IHM}$, $TD$, $Degree_{IHM}$
    *   CFE: Menos variação e eficácia nos cenários testados. $TD$ teve resultados instáveis."

**Slide 48: Conclusões**

*   **(Transição)** "Para concluir nosso trabalho:"
*   **(Ponto 1)** "As $IHMs$ oferecem diferentes perspectivas sobre a dificuldade das instâncias. Elas capturam diferentes aspectos da estrutura local dos dados, da distribuição dos rótulos e da relação feature-rótulo."
*   **(Ponto 2)** "$IHMs$ baseadas em vizinhança e grafos (como as variantes N, Degree, Closeness) foram frequentemente eficazes para ambos os tipos de problemas, pois refletem a proximidade e conectividade das instâncias no espaço de entrada."
*   **(Ponto 3)** "Medidas baseadas em erro de ajuste simples ($LE$, $S3_{IHM}$) foram boas para ruído/linearidade em regressão."
*   **(Ponto 4)** "Nenhuma $IHM$ única captura perfeitamente todas as fontes de dificuldade. A escolha da $IHM$ mais apropriada na prática dependerá da natureza do conjunto de dados e das fontes de dificuldade que se suspeita estarem presentes (sobreposição, ruído, não linearidade, etc.)."

**Slide 49: Referências Bibliogáficas**

*   **(Transição)** "A base deste trabalho é o seguinte artigo:"
*   **(Conteúdo)** "P. Torquette, G., S. Nunes, V., Y. A. Paiva, P. and C. Lorena, A. 2024. Instance hardness measures for classification and regression problems. Journal of Information and Data Management. 15, 1 (Feb. 2024), 152–174. DOI:https://doi.org/10.5753/jidm.2024.3463."
*   **(Comentário opcional)** "Este artigo detalha toda a metodologia e os resultados que apresentei hoje, e é uma excelente referência para quem quiser se aprofundar no tema."

**Fim da Apresentação**

---
output:
  pdf_document: default
  html_document: default

---
# Universidade Federal de Pernambuco Centro de Ciências Exatas e da Natureza

## Departamento de Estatística


### TÓPICOS ESPECIAIS EM ESTATÍSTICA COMPUTACIONAL
Aluno: Miguel Gustavo Gomes da Silva

<div style="margin-left: 12px;">


# 1- Introdução

A segurança pública é um tema amplamente debatido no Brasil, dados os altos e crescentes índices de criminalidade em todo o país. Uma questão tão alarmante realça a responsabilidade pública no desenvolvimento de estratégias e na atribuição dos recursos adequados para reduzir a criminalidade. Na vanguarda destas estratégias está a necessidade de aumentar o desempenho da polícia para oferecer um ambiente mais seguro para a sociedade. O constante sentimento de impunidade que atinge grande maioria das pessoas alimenta a necessidade de um debate urgente sobre a agenda da segurança pública no Brasil. Muito se tenta apontar uma causa, porém diversas variáveis implicam sobre as altas taxas de criminalidade no território nacional.

Soares (2006) defende que a pobreza e a desigualdade são fatores que podem contribuir para o comportamento criminoso na sociedade, assim como o sentimento de impunidade da Justiça Brasileira. Todavia, não se pode resumir o problema em apenas esses fatores.  Segundo Nepomuceno et al. (2020, 2021), o crime em si não pode ser considerado como uma entrada ou saída nos sistemas de produção policial porque não pode ser controlado diretamente devido à influência de fatores externos (renda, educação, religião, raça, cultura, etnia, entre outros), e as dificuldades em mensurar os crimes que foram evitados em decorrência das atividades operacionais policiais. Porém cada vez com maior frequência estudos utilizando modelagens matematicas vem buscando explicar o fenomeno "crime", assim como possiveis forma de combarter e estruturar melhores politicas de segurança 

Desta forma essa pesquisa tem como objetivo investigar a relação entre o numero de prisões realizadas e o efetivo policial (civil e militar) em uma área especifica da região central da cidade do Recife, capital do estado de Pernambuco, para isso foi utilizado uma rede neural totalmente conectada aplicada a regressão.
</div>

# 2- Referencial Teórico

Redes Neurais Artificiais (RNAs), uma subárea da Inteligência Artificial, têm se destacado como ferramentas poderosas para diversas aplicações(Chulu,2020). Dentre os diversos tipos de redes neurais, neste trabalho, utilizaremos as redes neurais totalmente conectadas (FCNNs), também conhecidas como redes Deep Feed Forward. As FCNNs, como o próprio nome sugere, possuem uma conectividade completa entre as camadas, o que as torna versáteis para uma ampla gama de problemas. Essa arquitetura, composta por uma série de camadas totalmente conectadas, não exige suposições prévias sobre os dados de entrada, o que contribui para sua popularidade em diversas áreas da ciência e engenharia ( Graham et al., 2022, Wang et al., 2019). Além disso, as FCNNs apresentam a vantagem de serem relativamente simples de construir e ajustar, sendo que a maior parte do aprendizado ocorre através do treinamento e da retropropagação.

# 4- Metodologia

Para a construção do trabalho se utilizou uma base de dados disponibilizada pela SDS-PE(Secretária de Defesa Social-Pernambuco) com dados referentes ao quantitativo de prisões, oficiais, praças, agentes, comissários, delegados, escrivães e viaturas alocadas na região central da cidade do Recife (Pernambuco,2014). A descrição de cada categoria está descrita a baixo:

* Prisões: Registro de prisões de todas as naturezas efetuadas na área estudada;
 
* Oficiais: Ocupam cargos de comando e gestão nas forças policiais. Possuem formação superior e são responsáveis por liderar equipes e tomar decisões estratégicas;

* Praças: Policiais de nível operacional, que realizam o trabalho de campo, como patrulhamento, atendimento a ocorrências e prisões;

* Agentes: São entes de segurança pública, com funções semelhantes às de praças.Podem ser agentes penitenciários, responsáveis pela custódia de presos;

* Comissários: Cargos de chefia, superior ao de delegado, com responsabilidades administrativas e operacionais;

* Delegados: Policiais civis responsáveis pelas investigações criminais. Têm formação jurídica e conduzem inquéritos policiais;

* Escrivães: Auxiliares de delegados nas investigações, realizando tarefas como o registro de ocorrências;

* Viaturas: Veículos utilizados pelas polícias para o transporte de policiais e equipamentos, além de realizar patrulhamento e outras atividades operacionais.


Inicialmente se construiu uma analise descritiva dos dados, para um entendimento inicial da situação estudada. Cabe se destacar que foram utilizados dados em intervalo semanal de registos. Abaixo a tabela mostra esses valores:

|               | Média | Mediana | Des Pad  |
|---------------|-------|---------|----------|
| Total_Prisões | 18,4  | 18,0    | 4,7      |
| Oficiais      | 12,3  | 13,0    | 2,5      |
| Praça         | 328,8 | 333,0   | 32,7     |
| Agentes       | 26,4  | 33,0    | 10,9     |
| Comissários   | 23,3  | 10,0    | 15,1     |
| Delegados     | 6,0   | 6,0     | 0,7      |
| Escrivães     | 11,1  | 11,0    | 0,4      |
| Viaturas      | 26,8  | 26,0    | 6,6      |


A análise descritiva dos dados apresentou que o número médio de prisões foi de 18,4 por semana, com uma variação significativa entre as semanas, como evidenciado pelo alto desvio padrão de 4,7. A categoria 'Praça' apresentou a maior média (328,8) ou seja um grande efetivo de praças, sugerindo uma grande demanda por policiamento em algumas regiões. Em contraste, o número dedelegados foi mais homogêneo entre as semanas, com uma média de 6,0 e um desvio padrão de apenas 0,7. Cabe se destacar a grande variação de agentes e comissários com desvio padrão 10,9 e 15,1 sucessivamente.   


# 5-Construçao dos Modelos

Três modelos de redes neurais foram desenvolvidos e comparados para prever o valor total de prisões. Os modelos utilizaram diferentes combinações de variáveis preditivas, com o objetivo de avaliar a influência do efetivo policial nesse contexto.

No primeiro modelos utilizou os numeros dos indicadores de todas os entes envolvidos na segurança do estado de pernambuco, policia ostensiva e policia investigativa. A policia ostensiva (Policia Militar), tem como principal funçao o patrulhamento e repressão direta a criminalidade, enquanto a policia investigativa(Policia Civil) tem como função a investigação e estruturação de operações especiais e resolução de crimes complexos.O segundo modelo utilizou apenas indicadores de entes da polícia ostensiva(militar) e o terceiro modelo utilizou somente entes da policia investigativa(civil).

    Modelo 1
     *Variavéis de entrada*: Oficiais, Praça, Agentes, Comissários, Delegados, Escrivães, Viaturas;
     *Variavel resposta*:  Total Prisões.

    Modelo 2
     *Variavéis de entrada*: Praça, Agentes, Delegados, Viaturas;
     *Variavel resposta*:  Total Prisões
     
    Modelo 3
     *Variavéis de entrada*: Oficiais, Comissários,Escrivães, Viaturas;
     *Variavel resposta*:  Total Prisões.

Para avaliar a performance dos três modelos de redes neurais, foi utilizado o RMSE (Raiz do erro quadrático médio) como métrica principal. O RMSE mede a raiz da diferença entre os valores preditos pelo modelo e os valores reais, fornecendo uma indicação da magnitude dos erros de previsão.

Foi desenvolvido uma rede neural artificial com 3 camadas densamente conectadas, utilizando a função de ativação ReLU (Rectified Linear Unit) nas camadas intermediárias para introduzir não linearidade ao modelo. A camada de entrada possui de acordo com os modelo descritos neurônios, correspondendo às camadas ocultas, subsequentes apresentam 64, 128 e 256 neurônios, respectivamente, permitindo a extração de características mais complexas. A camada de saída possui um único neurônio com função de ativação linear, adequada para problemas de regressão. Os dados foram divididos em 80% para o conjunto treinamento e 20% para o conjunto teste. O modelo foi compilado utilizando o otimizador Adam, com uma taxa de aprendizado de 0,001. 

# 6- Resultados

A fase de treinamento dos modelos apresentou resultados variados. Conforme ilustrado nas imagens a seguir, o primeiro modelo obteve o valor do RMSE de 5,35 , o segundo modelo obteve um valor de RMSE de 5,019, enquanto o terceiro modelo alcançou um RMSE de 4,982.A análise desses resultados permite uma comparação inicial da performance dos modelos durante a fase de treinamento.
Utilizando o conjuto teste o modelo 1 obteve um valor de 5,669, já o modelo 2 obteve 6,041 no RMSE, e por fim o modelo 3 apresentou um RMSE 5.665.

![Modelo 1](C:/Users/Miguel/Desktop/Capturar.PNG)

![Modelo 2](C:/Users/Miguel/Desktop/Capturar2 (2).PNG)

![Modelo 3](C:/Users/Miguel/Desktop/Capturar3 (3).PNG)

Podemos perceber que os modelos 2 e 3 possuem uma variação do RMSE no conjunto de treinamento e no conjunto de teste, diferente do modelo 1 que aparenta uma queda mais estavel e baixa variação. 


### 6.1 Comparação entre o valor real e os valores preditos pelos modelos 

Ao comparar valores reais e preditos em uma amostra aleatória de 10 observações, constatou-se que os modelos apresentam dificuldade em capturar a variabilidade dos valores altos de prisões. As observações 60, 155, 45 e 9 exemplificam essa tendência, onde os valores preditos subestimam substancialmente os valores reais. Essa discrepância sugere que os modelos podem estar subajustados para eventos extremos ou que a relação entre as variáveis preditoras e a variável resposta não acompanhe a relação para valores elevados.Toda via para valores onde a variavel resposta se aproxima ao valor medio do conjunto de dados, o modelo apresenta uma boa performace.
  
| Observação | Valor Real | Valor Predito- 1 | Valor Predito-2 | Valor Predito-3  |
|------------|------------|------------------|-----------------|------------------|
| 30         | 19         | 19,28            | 20,59           | 21,22            |
| 171        | 16         | 15,49            | 16,24           | 15,81            |
| 84         | 20         | 18,93            | 20,78           | 22,96            |
| 198        | 10         | 14,4             | 15,23           | 17,55            |
| 60         | 28         | 18,06            | 19,41           | 18,39            |
| 155        | 24         | 15,25            | 16,58           | 17,83            |
| 45         | 21         | 19,19            | 20,64           | 20,61            |
| 181        | 18         | 15,02            | 15,71           | 17,1             |
| 9          | 28         | 18,41            | 19,54           | 19,47            |
| 195        | 15         | 14,3             | 15,23           | 17,5             |


A análise dos dados sugere a possibilidade de viés de seleção, uma vez que algumas observações do subconjunto dos dados pode ter sido coletado em condições operacionais que favoreceram um aumento no número de prisões, como em operações especiais ou eventos especificos sazonais. Essa discrepância entre os dados de treinamento e a realidade pode estar comprometendo a capacidade do modelo de generalizar para novas situações e gerar resultados precisos. Uma investigação mais aprofundada dos dados é necessária para identificar e mitigar esse viés, permitindo a construção de um modelo mais robusto e confiável.

# 7- Conclusão

A presente pesquisa teve como objetivo investigar a relação entre o número de prisões e o efetivo policial em uma área específica da cidade do Recife, utilizando modelos de redes neurais. Os resultados obtidos indicam que, embora os modelos tenham apresentado um desempenho razoável em capturar a variabilidade dos dados se faz cada vez mais necessário a construção de estudos como esse para contribuir com a busca da melhor estratégia de formulação de politicas públicas junto a técnicas computacionais modernas e robustas.

A pesquisa acerca de um tema de tamanha relevância para sociedade deve ser cada vez mais estimulada e incentivada no meio acadêmico e por parte dos órgãos públicos, visto que dessa forma se obtém informações e análises que servem como apoio a tomada de decisão, podendo ser utilizadas por gestores e formuladores de política pública.

### Referencia

N. Graham, H. Hu, J. Im, X. Li, H. Wolkowicz, A restricted dual peacemanrachford splitting method for a strengthened DNN relaxation for QAP, INFORMS J. Comput. 34 (2022) 2125–2143

Y. Wang, F. Zhang, X. Zhang, S. Zhang, Series AC arc fault detection method based on hybrid time and frequency analysis and fully connected neural network, IEEE Trans. Ind. Inform. 15 (2019) 6210–6219

Chulu Zhu, Jingtao Wang,Process structure-based fully connected neural network for the modelling of chemical processes: A comparison between global and modular configurations, Journal of the Taiwan Institute of Chemical Engineers,2020 Volume 157,
  
PERNAMBUCO. Secretaria de Defesa Social. Fórum Estadual de Segurança Pública. Pacto pela Vida – Plano Estadual de Segurança Pública. Recife: SDS, maio de 2014. 

SOARES, L E (2006). Segurança Pública: Presente E Futuro. Revista Estudos Avançados, 20 (56).

NEPOMUCENO, T. C. C., COSTA, A. P. C. S., & DARAIO, C. (2021). Theoretical And Empirical Advances In The Assessment Of Productive Efficiency Since The Introduction Of Dea: A Bibliometric Analysis. Forthcoming In Int. J. Of Operational Research.

DARAIO, C., KERSTENS, K., NEPOMUCENO, T. C. C., & SICKLES, R. C. (2020). Empirical Surveys Of Frontier Applications: A Meta‐Review. Intl. Trans. In Op. Res., 27: 709-738. Doi: 10.1111/Itor.12649
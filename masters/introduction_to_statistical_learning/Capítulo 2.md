## O que é o aprendizado estatístico

Em geral queremos trabalhar com um fenômeno cuja resposta (vetor Y) está ou pode estar relacionada a um conjunto de entradas (matriz X).

$$\LARGE Y=f(X)+\epsilon{}$$
Onde $\epsilon$ é o termo de erro aleatório do modelo.

### Por que estimar f?
Há duas razões principais para estimar f: previsão e inferência
#### Previsão
Tratamos $f(x)$ como uma caixa preta, e estamos preocupados apenas com nossa capacidade de prever os valores de $Y$. Nesse sentido, nossa intencão é minimizar o *erro redutível*, ou seja, aquele que conseguimos atacar melhorando nosso modelo. Enquanto temos que aceitar o *irredutível*, aquele característico por desvios causados por dados / features que não temos, ou por fatores impossíveis de medir.

#### Inferência
Queremos entender como $Y$ é afetado por cada feature de $X=(X_1,X_2,...,X_n)$ impacta $Y$, ou seja, como cada uma dessas variáveis se relaciona a $Y$. Nesse sentido, $\hat{f}$ não pode mais ser tratado como uma caixa preta, queremos saber sua exata expressão matemática. Algumas perguntas que podemos estar interessados no caso da inferencia:

* Quais preditores são realmente relacionados a variável resposta (seja por relevância estatística, ou apenas quais são os que mais impactam?)
* Qual é a relacão entre a variável resposta e cada preditor? (Algumas podem ser positivas, outras negativamente correlacionadas, etc.)
* $Y$ e cada preditor em $X$ podem ser relacionados por relacões lineares, ou o seu relacionamento é mais complexo? 

### Como estimar f?
Temos duas abordagens possíveis: Modelagens *paramétricas* ou modelagens *não paramétricas*.

#### Modelos paramétricos
É a abordagem que assume uma forma específica para $f$ a priori. Temos por exemplo, o modelo de regressão linear.
$$
\begin{align*}
Y = \beta_0 + \beta_1X_1 + \beta_1X_2+...+\beta_pX_p 
\end{align*}
$$
Onde cada $\beta_i$ representa um coeficiente ("peso") para cada variável preditora. Nesse sentido, o problema que tínhamos, que era estimar $f$ resume-se a estimar um conjunto finito de parâmetros ($p+1$) do modelo linear. Daí o nome paramétrico. 

Caso nosso modelo seja muito rígido, podemos adotar modelos mais flexíveis, com mais parâmetros de forma geral, porém isso pode levar a *overfitting*.
#### Modelos não-paramétricos
Não adotamos premissas explícitas sobre a forma funcional de $f$. Ao invés disso, queremos encontrar a funcão que melhor se ajusta aos dados. Como não é assumida uma forma a priori para $f$, modelos não-paramétricos precisam de um volume muito maior de dados para serem estimados.

De forma geral, modelos menos flexíveis (como os paramétricos) são mais fáceis de interpretar e são preferidos para a inferência, por outro lado, modelos mais flexíveis (como os não-paramétricos) são adequados para casos de uso focados na previsão, e também demandam maiores volumes de dados.


### Aprendizado Supervisionado x Não supervisionado
* Supervisionado: Existe uma variável resposta que queremos prever (ex: prever a quantidade de vendas dado um volume de gastos em marketing)
* Não supervisionado: Não há uma variável resposta explícita, então restam outras análises diferentes, como agrupar conjuntos de observacões similares em grupos que tenham um determinado grau de distincão (clustering) a partir das variáveis observadas Ex: Dividir clientes de uma empresa em grupos distintos, dadas variáveis como volume de gastos, condicões sócioeconômicas, etc.
### Regressão x Classificacão
* Regressão: Nossa variável resposta é quantitativa (dinheiro, anos, pessoas, etc.)
* Classificacão: Nossa resposta é categórica (sim ou não; muito bom, bom, regular, ruim, péssimo, etc.)
## Avaliando a precisão do modelo
### Medindo a qualidade de fit
#### Medium Squared Error (Erro quadrático médio)
$$MSE=\frac{1}{n}\sum_{i=1}^{n}(y_i - \hat{f}(x_i))^2$$
É a medida mais popular e representa a média dos desvios quadrados entre cada valor real da variável resposta e cada valor estimado. Se o modelo estiver fazendo boas previsões, o MSE tenderá a ser pequeno. É bom lembrar que o MSE de treino não é importante, o que nós queremos otimizar é o MSE de teste, ou seja, o MSE calculado utilizando o modelo em dados que não foram utilizados em seu processo de treinamento. O MSE de treino é apenas uma pista para ver se o modelo é minimamente promissor.

##### Overfitting
Ocorre quando aumentamos demais o nível de flexibilidade do modelo, de forma que ele busca padrões no próprio erro irredutível. Dessa forma, esses modelos tem um baixo MSE de treino e um alto MSE de teste. Nesses casos, com um modelo menos flexível poderíamos alcancar um MSE de teste menor do que no modelo flexível.

### Trade off viés variância
Para uma dada observacão, podemos decompor o valor esperado do MSE para um conjunto de dados de teste $x_0$ da seguinte forma:
$$E(y_0-\hat{f}(x_0))^2=Var(\hat{f}(x_0)+[Bias(\hat{f})]²+Var(\epsilon)$$
A notacão $E(y_0-\hat{f}(x_0))^2$ define o MSE de teste esperado, que pode ser interpretado como a média do MSE de teste que obteríamos caso estimássemos $f$ usando um grande número de conjuntos de treino distintos, e testássemos cada $f$ estimada no conjunto de teste $x_0$.

Pela formulacão podemos perceber que:
* Nosso objetivo na modelagem deve ser minimizar os termos de variância e viés, excluindo $Var(\epsilon)$ que, por definicão, não pode ser reduzido.
* O limite inferior do erro do nosso modelo, ou seja, o quão bom o podemos fazer, é $Var(\epsilon)$
* Conseguimos evoluir nosso modelo de forma mais rápida inicialmente reduzindo o viés, ou seja, encontrando um modelo que tenha uma estrutura aderente ao comportamento do fenômeno subjacente. Posteriormente, melhoramos o modelo de forma menos intensa, utilizando modelos que tenham menor variância, ou seja, que sejam menos flexíveis.
* O overfit faz com que a variância do nosso modelo exploda, causando um valor esperado superior para o MSE de teste
* Uma escolha de um modelo que assuma uma estrutura muito distante do fenômeno subjacente aumenta o MSE de teste esperado.
* De forma geral, conforme usamos modelos mais flexíveis, o viés vai reduzir e a variância vai aumentar.
* O exercício de modelagem é justamente testar diferentes modelos com o objetivo de minizar o MSE de teste esperado, encontrando um modelo que equilibre valores baixos de viés e de variância. Observe que, em casos reais, onde o valor subjacente de $f$ é desconhecido, não é possível calcular o viés. Porém devemos manter esse racional em mente.
(Próxima parada: Cap 2: The classification setting)
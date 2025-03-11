* Razões para que problemas estejam modelados com *unboundedness*:
	* Alguma variável livre deveria ser não negativa
	* A direcão da otimizacão está invertida
	* Alguma restricão foi omitida.
Destacando: Problemas *unbounded* não sao realistas, então certamente houve um erro de modelagem.

### Problemas lineares inteiros mistos
Quando é válido apenas usar a solucão do problema linear contínuo e truncar a solucão?
* Os valores são numericamente tão grandes que o erro é desprezível
* Os dados de input não são conhecidos com tanta certeza, então a solucão inteira não seria tão precisa de qualquer forma
* O processo de arredondamento garantidamente levará a uma solucão viável
* Algoritmos de programacao inteira são custosos e, no problema que está tentando-se resolver, não é possível conseguir a solucão / é muito caro.

Uma abordagem para resolver problemas inteiros muito difíceis é calcular a solucão do PPL (problema relaxado) e admitir como critério de parada qualquer solucão que ternha um desvio X estipulado desse limite superior. Esse é um exemplo onde ocorre um trade off em que aceita-se uma queda na otimalidade da solucão para receber de volta viabilidade prática de obter uma solucão.

### Problemas não lineares
Importante: Em geral, problemas em que os termos não lineares aparecem apenas na funcão objetivo são mais fáceis de resolver do que os problemas em que esses termos não lineares aparecem nas restricões. Modelos não lineares em que as variáveis são inteiras são piores ainda.


### Resumo

Neste capítulo, foram introduzidos os três tipos mais comuns de modelos com restrições: modelos de programação linear, modelos de programação linear inteira e modelos de programação não linear. Os modelos de programação linear (PL) devem satisfazer a restrição de que tanto a função objetivo quanto as restrições sejam lineares. Apesar dessa limitação, os modelos de programação linear ainda são os mais comuns devido à disponibilidade de algoritmos de solução poderosos. Os modelos de programação linear inteira (PLI) são semelhantes aos lineares, exceto pelo fato de que uma ou mais variáveis devem assumir valores inteiros. Com exceção de um pequeno grupo, especificamente os modelos de fluxo em redes, os modelos de programação inteira são mais difíceis de resolver do que os modelos lineares. Já os modelos de programação não linear (PNL) podem ter uma função objetivo não linear e/ou restrições não lineares. Nesses casos, não há garantia de que a solução ótima encontrada seja globalmente ótima. Quando um modelo de otimização é resolvido, uma das seguintes situações pode ocorrer: uma solução ótima é encontrada, o que é a situação desejada; o problema é inviável, devido a inconsistências no conjunto de restrições; ou o problema é ilimitado, o que geralmente é causado por um erro de modelagem.
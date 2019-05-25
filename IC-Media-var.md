
# Aula 10 - Intervalo de Confiança para a Média e Variância
## Fundamentos
Partiremos da ideia do uso de estimadores para obter valores de parâmetros da população em termos de um conjunto amostral;
**Estimador da Média**: $$ \Theta_\mu = \frac{1}{n}\sum_{i=1}^{n}{x_i}$$
**Estimador da Variância**: $$ \Theta_\sigma^2 = \frac{1}{n-1}\sum_{i=1}^{n}{(x_i-\Theta_{\mu})^2}$$
Usa-se $n-1$ para construir um estimador para a variância não enviesado.
Nos resta identificar o quão confiável são os valores obtidos para os parâmetros estimados em relação aos parâmetros reais da população;

**Pergunta:** qual é a confiabilidade dos parâmetros? Em que intervalo podemos confiar encontrar o parâmetro real em relação ao estimado?

Um **Intervalo de Confiança** para um parâmetro é um intervalo na forma $L_{inf} \le \theta \le L_{sup}$ tal que os valores $L_{inf}$ e $L_{sup}$ são computados a partir do conjunto amostral.

Construindo infinitos intervalos$[L_{inf}, L_{sup}]$ a partir de infinitas estimativas encontraremos o verdadeiro valor do parâmetro $\theta$ em $(1-\alpha)\times100\%$ destes intervalos. 
Uma confiança de $(1-\alpha)$ significa que $Prob(L_{inf} \le \theta \le L_{sup})=1-\alpha$. Como determinar os limites para garantir a confiança de $(1-\alpha)$?

**Ponto de Partida**: conhecer a distribuição amostral do estimador:

  Um estimador pode ter distribuição de probabilidade *normal*, *t-Student*, *Chi-quadrado* entre outras;
 - *Normal*: estimador da média com variância conhecida;
 - *t-Student*: estimador da média com variância desconhecida;
 - *Chi-quadrado*: estimador da variância;

## Intervalos de Confiança para a Média

É o intervalo definido para cálculo da média $\Theta_{\mu}$ com base na média amostral calculada $\overline{x}$;
 - *Normal*: estimador da média com variância conhecida - calculada com base em *escore-Z*;
 - *t-Student*: estimador da média com variância desconhecida - *escore-t*;

### Variância conhecida
**Intervalo unilateral** $z_\alpha$: escore-z implica em $1-\alpha$
Intervalo de confiança é escrito como:
$$\overline{x} -\frac{ z_{\alpha} \sigma}{\sqrt{n}} \le \mu  $$ ou $$\overline{x} -\frac{ z_{\alpha} \sigma}{\sqrt{n}} \ge\mu$$
**Intervalo bilateral** $z_{\alpha/2}$: escore-z implica em $1-{\alpha/2}$
$$\overline{x} -\frac{ z_{\alpha/2} \sigma}{\sqrt{n}} \le \mu \le \overline{x} +\frac{ z_{\alpha/2} \sigma}{\sqrt{n}} $$

**Exemplo**
Dez medições da energia de impacto de tipos de corte de aço a $60 ºC$ são: 64.1, 64.7, 64.5, 64.6, 64.5, 64.3, 64.6, 64.8, 64.2, e 64.3.
A energia de impacto é normalmente distribuída com desvio-padrão de 1J. Encontrar um intervalo de confiança de 95% para a média
````python
import numpy as np
# calculo da media amostral
X = [64.1, 64.7, 64.5, 64.6, 64.5, 64.3, 64.6, 64.8, 64.2,  64.3]
medX = np.mean(X)
n = len(X)
zA2 = 1.96
sigma = 1 #Variancia Conhecida
Linf = medX - zA2 *sigma/np.sqrt(n)
Lsup = medX + zA2 *sigma/np.sqrt(n)
print("Intervalo de Confianca:",Linf ,"a",Lsup)
````
#### Como fazer para encontrar o escore-z?
Para determinar o escore-z, localizamos na tabela de distribuição normal os valores que resultam em um intervalo cuja probabilidade é $(1-\alpha)$. Tomando como exemplo a tabela normal parcialmente mostrada a seguir:
Tabela normal:$P(X\le x)$, para encontrarmos $-z_{\alpha/2}$ e $z_{\alpha/2}$ usaremos as propriedades da distribuição normal:
$$(1-\alpha) = P(x\le z_{\alpha/2}) - P(x\le -z_{\alpha/2})$$
$$P(x\le z_{\alpha/2})  = P(x\ge - z_{\alpha/2}) = 1 - P(x\le -z_{\alpha/2}) $$
Assim, reescrevemos como:
$$(1-\alpha) = P(x\le z_{\alpha/2}) - \left( 1 - P(x\le z_{\alpha/2})\right)$$
$$(1-\alpha) = 2P(x\le z_{\alpha/2}) -1$$
$$\alpha/2= 1-P(x\le z_{\alpha/2}) $$
#### Exemplo: determinar os escores z para um intervalo de confiança de 95% 
$(1-\alpha) = 95\%$ então $\alpha = 0,05 \rightarrow \alpha/2 =0,025$
$$0,025= 1-P(x\le z_{\alpha/2}) \rightarrow P(x\le z_{\alpha/2}) = 0,975$$
|x|0|0,01|0,02|0,03|0,04|0,05|0,06|0,07|0,08|0,09|
|--|--|--|--|--|--|--|--|--|--|--|
|0,0|0,5000|0,5040|0,5080|0,5120|0,5160|0,5199|0,5239|0,5279|0,5319|0,5359|
|0,1|0,5398|0,5438|0,5478|0,5517|0,5557|0,5596|0,5636|0,5675|0,5714|0,5753|
|0,2|0,5793|0,5832|0,5871|0,5910|0,5948|0,5987|0,6026|0,6064|0,6103|0,6141|
|0,3|0,6179|0,6217|0,6255|0,6293|0,6331|0,6368|0,6406|0,6443|0,6480|0,6517|
|0,4|0,6554|0,6591|0,6628|0,6664|0,6700|0,6736|0,6772|0,6808|0,6844|0,6879|
|0,5|0,6915|0,6950|0,6985|0,7019|0,7054|0,7088|0,7123|0,7157|0,7190|0,7224|
|0,6|0,7257|0,7291|0,7324|0,7357|0,7389|0,7422|0,7454|0,7486|0,7517|0,7549|
|0,7|0,7580|0,7611|0,7642|0,7673|0,7704|0,7734|0,7764|0,7794|0,7823|0,7852|
|0,8|0,7881|0,7910|0,7939|0,7967|0,7995|0,8023|0,8051|0,8078|0,8106|0,8133|
|0,9|0,8159|0,8186|0,8212|0,8238|0,8264|0,8289|0,8315|0,8340|0,8365|0,8389|
|1,0|0,8413|0,8438|0,8461|0,8485|0,8508|0,8531|0,8554|0,8577|0,8599|0,8621|
|1,1|0,8643|0,8665|0,8686|0,8708|0,8729|0,8749|0,8770|0,8790|0,8810|0,8830|
|1,2|0,8849|0,8869|0,8888|0,8907|0,8925|0,8944|0,8962|0,8980|0,8997|0,9015|
|1,3|0,9032|0,9049|0,9066|0,9082|0,9099|0,9115|0,9131|0,9147|0,9162|0,9177|
|1,4|0,9192|0,9207|0,9222|0,9236|0,9251|0,9265|0,9279|0,9292|0,9306|0,9319|
|1,5|0,9332|0,9345|0,9357|0,9370|0,9382|0,9394|0,9406|0,9418|0,9429|0,9441|
|1,6|0,9452|0,9463|0,9474|0,9484|0,9495|0,9505|0,9515|0,9525|0,9535|0,9545|
|1,7|0,9554|0,9564|0,9573|0,9582|0,9591|0,9599|0,9608|0,9616|0,9625|0,9633|
|1,8|0,9641|0,9649|0,9656|0,9664|0,9671|0,9678|0,9686|0,9693|0,9699|0,9706|
|1,9|0,9713|0,9719|0,9726|0,9732|0,9738|0,9744|**0,9750**|0,9756|0,9761|0,9767|
|2,0|0,9772|0,9778|0,9783|0,9788|0,9793|0,9798|0,9803|0,9808|0,9812|0,9817|
|2,1|0,9821|0,9826|0,9830|0,9834|0,9838|0,9842|0,9846|0,9850|0,9854|0,9857|
|2,2|0,9861|0,9864|0,9868|0,9871|0,9875|0,9878|0,9881|0,9884|0,9887|0,9890|
|2,3|0,9893|0,9896|0,9898|0,9901|0,9904|0,9906|0,9909|0,9911|0,9913|0,9916|
|2,4|0,9918|0,9920|0,9922|0,9925|0,9927|0,9929|0,9931|0,9932|0,9934|0,9936|
|2,5|0,9938|0,9940|0,9941|0,9943|0,9945|0,9946|0,9948|0,9949|0,9951|0,9952|
|2,6|0,9953|0,9955|0,9956|0,9957|0,9959|0,9960|0,9961|0,9962|0,9963|0,9964|

Valor encontrado na tabela: $z_{\alpha/2} = 1,96$

Em `python`, encontramos o valor dos escores-z desejados utilizando o método `norm.isf((1 - alpha/2), loc=0, scale=1)`, admitindo uma normal padrão, da classe `stats` da biblioteca `scipy`.
Para determinar os escores-z:
````python
import numpy as np
import matplotlib.pyplot as plt
import scipy.stats as st
# IC bilateral de 90%
zEsc = st.norm.isf(0.95, loc=0, scale=1)
# IC bilateral de 95%
zEsc = st.norm.isf(0.975, loc=0, scale=1)
# IC bilateral de 99%
zEsc = st.norm.isf(0.995, loc=0, scale=1)
````
### Variância desconhecida

No caso da variância desconhecida, não é mais possível utilizarmos escores-z para definirmos o intervalo. No entanto, a distribuição de probabilidade *T-Student* é útil para modelar o comportamento do estimador da média amostral quando não se conhece a variância. 

#### Distribuição T-Student
Seja Z uma variável Normal Padrão: $Z =  N(0,1)$ e V uma variável Chi-Quadrado com k graus de liberdade: $V = \chi_k^2$ Definimos uma variável T como: $T = \frac{Z}{\sqrt{V/k}}$. Neste caso, a variável T tem Distribuição T com k graus de liberdade. Assim, A distribuição T-Student se torna:
$$f(x) = \frac{\Gamma[(k+1)/2]}{\sqrt{\pi/k}\Gamma(k/2)} \cdot \frac{1}{[x^2/k + 1]^{(k+1)/2}}, -\infty < x < \infty$$, em que $\Gamma(\cdot)$ é a função Gama.
#### Escore-t
Define-se o escore-t como o valor para o qual há $(1-\alpha)$ de área à sua esquerda na Curva da Distribuição T com $k$ graus de liberdade. A distribuição T se aproxima da Normal à medida em que $k \rightarrow \infty$.
Usando $s$ como o estimador da variância, rescrevemos o escore-t com $k = n-1$ graus de liberdade, em que $n$ é o tamanho da amostra. Assim, para um **Intervalo bilateral** $t^{n-1}_{\alpha/2}$: escore-t implica em $1-{\alpha/2}$
$$\overline{x} -\frac{ t^{n-1}_{\alpha/2} s}{\sqrt{n}} \le \mu \le \overline{x} +\frac{ t^{n-1}_{\alpha/2} s}{\sqrt{n}} $$
 Da mesma forma que para o escore-z, o escore-t é definido encontrando o valor de $t^{n-1}_{\alpha/2}$ (intervalo bilateral) que produz uma probabilidade $\alpha/2= 1-P(T\le t^{n-1}_{\alpha/2})$. Tal probabilidade agora depende de dois fatores: o grau de confiança $(1-\alpha)$ e o número de graus de liberdade $k = n-1$. Utilizamos uma tabela da distribuição T para encontrar os escores desejados.
 
 #### Exemplo: determinar os escores t para um intervalo de confiança de 95% 
$(1-\alpha) = 95\%$ então $\alpha = 0,05 \rightarrow \alpha/2 =0,025$
$$0,025= 1-P(x\le t^{n-1}_{\alpha/2}) \rightarrow P(x\le t^{n-1}_{\alpha/2}) = 0,975$$
Note que é necessário saber o número de graus de liberdade para determinar o escore-t correto.
Assumindo $n = 23$, temos $k = n-1 = 22$ graus de liberdade. Para um IC de 95%, procuramos a linha com $\alpha = 0,025$ e $k = 22$:
 |$k/\alpha$|0,25|0,10|0,05|0,025|0,01|0,005|0,0025|0,001|0,0005|
|--|--|--|--|--|--|--|--|--|--|
|1|1,000|3,078|6,314|12,71|31,82|63,66|127,3|318,3|636,6|
|2|0,816|1,886|2,920|4,303|6,965|9,925|14,09|22,33|31,60|
|3|0,765|1,638|2,353|3,182|4,541|5,841|7,453|10,21|12,92|
|4|0,741|1,533|2,132|2,776|3,747|4,604|5,598|7,173|8,610|
|5|0,727|1,476|2,015|2,571|3,365|4,032|4,773|5,894|6,869|
|6|0,718|1,440|1,943|2,447|3,143|3,707|4,317|5,208|5,959|
|7|0,711|1,415|1,895|2,365|2,998|3,499|4,029|4,785|5,408|
|8|0,706|1,397|1,860|2,306|2,896|3,355|3,833|4,501|5,041|
|9|0,703|1,383|1,833|2,262|2,821|3,250|3,690|4,297|4,781|
|10|0,700|1,372|1,812|2,228|2,764|3,169|3,581|4,144|4,587|
|11|0,697|1,363|1,796|2,201|2,718|3,106|3,497|4,025|4,437|
|12|0,695|1,356|1,782|2,179|2,681|3,055|3,428|3,930|4,318|
|13|0,694|1,350|1,771|2,160|2,650|3,012|3,372|3,852|4,221|
|14|0,692|1,345|1,761|2,145|2,624|2,977|3,326|3,787|4,140|
|15|0,691|1,341|1,753|2,131|2,602|2,947|3,286|3,733|4,073|
|16|0,690|1,337|1,746|2,120|2,583|2,921|3,252|3,686|4,015|
|17|0,689|1,333|1,740|2,110|2,567|2,898|3,222|3,646|3,965|
|18|0,688|1,330|1,734|2,101|2,552|2,878|3,197|3,610|3,922|
|19|0,688|1,328|1,729|2,093|2,539|2,861|3,174|3,579|3,883|
|**20**|0,687|1,325|**1,725**|**2,086**|2,528|**2,845**|3,153|3,552|3,85|
|21|0,686|1,323|1,721|2,080|2,518|2,831|3,135|3,527|3,819|
|**22**|0,686|1,321|1,717|**2,074**|2,508|2,819|3,119|3,505|3,792|
|23|0,685|1,319|1,714|2,069|2,500|2,807|3,104|3,485|3,768|
|24|0,685|1,318|1,711|2,064|2,492|2,797|3,091|3,467|3,745|
|25|0,684|1,316|1,708|2,060|2,485|2,787|3,078|3,450|3,725|

À medida que a quantidade de graus de liberdade aumenta, os escores-t se aproximam dos escores-z.

Em `python`, encontramos o valor dos escores-t desejados utilizando o método `t.isf((1 - alpha/2), loc=0, scale=1)`, que significa *Inverse survival function* admitindo uma distribuição t-Student padrão, da classe `stats` da biblioteca `scipy`.
Verifique o código a seguir e localize os escores-t de acordo com a tabela.
````python
import numpy as np
import matplotlib.pyplot as plt
import scipy.stats as st
# tamanho da amostra
n = 20
# graus de liberdade
k = n-1
# IC bilateral de 90%
tEsc = st.t.isf(0.95,k, loc=0, scale=1)
print(tEsc)
# IC bilateral de 95%
tEsc = st.t.isf(0.975,k, loc=0, scale=1)
print(tEsc)
# IC bilateral de 99%
tEsc = st.t.isf(0.995,k, loc=0, scale=1)
print(tEsc)
````
### Exercício
Construir um intervalo de confiança de 95% para as amostras a seguir:

||||||||||||
|--|--|--|--|--|--|--|--|--|--|--|
|19.8| 15.4| 11.4| 19.5| 10.1| 18.5| 14.1|8.8| 14.9| 7.9| 17.6|
|13.6| 7.5| 12.7| 16.7|11.9| 15.4| 15.4| 11.9| 11.4| 15.8| 11.4|
||||||||||||

Da amostra, obtém-se $n = 22 \rightarrow k = 21$. Portanto, o escore-t para um IC de 95% será o equivalente a $\alpha/2=0,025$, ou seja, $t^{n-1}_{\alpha/2} = t^{21}_{0,025} = 2,080$ (verificar na tabela)
O código em `python` a seguir determina os intervalos para os ICs considerando o caso da variância desconhecida:
````python
import numpy as np
import matplotlib.pyplot as plt
import scipy.stats as st
# calculo da media amostral
X = [19.8, 15.4, 11.4, 19.5, 10.1, 18.5, 14.1,8.8, 14.9, 7.9, 17.6,13.6, 7.5, 12.7, 16.7,11.9, 15.4, 15.4, 11.9, 11.4, 15.8, 11.4]
medX = np.mean(X)
n = len(X)
s = np.std(X, ddof=1)
# intervalo de confianca de 95% 
tEsc= -st.t.isf(0.975,n-1, loc=0, scale=1)
Linf = medX - tEsc *s/np.sqrt(n)
Lsup = medX + tEsc *s/np.sqrt(n)
print(tEsc)
print("Intervalo de Confianca:",Linf ,"a",Lsup)
````
Modifique o código acima para exibir o intervalo de confiança de 90% e de 99% para a mesma amostra. 

### Exercício 2

Utilizando os conceitos fixados sobre intervalo de confiança:

 1. Calcular o intervalo de confiança de 95% para a seguinte amostra, com variância populacional desconhecida:

||||||||||||
|--|--|--|--|--|--|--|--|--|--|--|
|19,8|18,5|17,6|16,7|15,8|15,4|14,1|13,6|11,9|11,4|
|11,4|8,8|7,5|15,4|15,4|19,5|14,9|12,7|10,1|7,9|
||||||||||||
 2.  O peso de componentes eletrônicos produzidos por determinada  empresa é uma v. a. que se supõe ter distribuição aproximadamente normal. Pretendendo-se estudar a variabilidade do peso dos referidos componentes, recolheu-se uma amostra de 11 elementos, cujos valores (em gramas) foram:

||||||||||||
|--|--|--|--|--|--|--|--|--|--|--|
|98 |97 |102 |100 |98 |101 |102 |105 |95 |102 |100 
||||||||||||

* Apresente uma estimativa para a média do peso dos componentes.
* Construa um intervalo de confiança para a média do peso, com um grau de confiança de 95%.
* Construa um intervalo de confiança a 99% para a média do peso.


> Written with [StackEdit](https://stackedit.io/).


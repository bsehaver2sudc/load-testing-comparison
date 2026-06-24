# Observação

> [!NOTE]
> Testado na maquina do autor; outro ambiente pode pedir ajuste.


Como o texto está em inglês, os números seguem a notação adotada nos Estados Unidos: separador de milhar com vírgula e separador decimal com ponto. Em português usamos o inverso.

# Nota

Depois da solução inicial, este documento apresenta uma versão mais flexível no final.

# Geral

### Duas colunas, coluna da esquerda com 3 itens e da direita com 2 — 5 itens

Vamos pensar. É preciso distribuir todas as partes dentro de uma parte maior, que deve ser um retângulo perfeito (ou um quadrado).

Conversei com um assistente para entender melhor o problema. O raciocínio foi este:

Vamos montar um mapa de áreas com os números 1, 2, 10, 20 e 50.

A soma desses números dá 83.

Antes de tudo: as proporções valem para a área. Ou seja, o retângulo do valor 2 precisa ter o dobro da área do retângulo do valor 1.

Precisamos fixar algumas premissas, como a área total. Adotamos largura e altura de 800 por 600.

Com isso a área total fica em 480.000.

As áreas de todas as partes são proporcionais. Em outras palavras:

- a soma das partes é 83;
- a área total é 480.000.

Daí surge um fator de escala:

- 480.000 dividido por 83 dá aproximadamente 5.783,1325

É meio óbvio (kkk), mas multiplicando a soma das partes pelo fator chegamos à área total:

(1 + 2 + 10 + 20 + 50) vezes 5.783,1325 dá aproximadamente 479.999,9975.

Proporcionalmente, a área da parte de valor 1 será 5.783,1325.

Ficou definido que o retângulo total tem as dimensões informadas. A solução adotada colocou os três menores valores à esquerda e os dois restantes à direita. Vamos seguir esta regra:

- se o total de partes for par, metade vai para a esquerda e metade para a direita;
- se o total for ímpar, a esquerda recebe metade mais meia parte e a direita recebe metade menos meia parte. No caso de 5 partes: metade é 2,5; somando 0,5 temos 3, subtraindo 0,5 temos 2, e 3 mais 2 dá 5;
- os valores menores vão para a esquerda. Isso resulta numa solução correta? Sim, porque a parte da direita fica maior no eixo horizontal.

O formato geral da ideia é este:

```
 __ ________
|__|        |
|  |________|
|__|        |
|  |        |
|  |        |
|  |        |
|__|________|

```

Voltando à solução: a altura total é 600, então a soma das alturas das três partes da esquerda também é 600, e as três compartilham a mesma largura. Assim, proporcionalmente, a altura da parte de valor 1 é 1 dividido por (1 + 2 + 10), vezes 600, o que dá aproximadamente 46,1538.

Sabemos que a área da parte de valor 1 é 5.783,1325. Logo a largura é:

```
5.783,1325 / 46,1538 = 125,3013
```

Para obter as demais áreas basta multiplicar respeitando a proporção:

- parte 1: 5.783,1325
- parte 2: 11.566,2650
- parte 10: 57.831,3250
- parte 20: 115.662,6500
- parte 50: 289.156,6250

Conferindo a soma: o total dá aproximadamente 479.999,9975, que é a área total.

Também vale conferir as alturas da esquerda, usando a altura da parte 1 já calculada e a proporção:

- parte 1: 46,1538
- parte 2: 92,3076
- parte 10: 461,5380

Somando: aproximadamente 600. Certo.

Como as três partes da esquerda dividem a altura total com as duas da direita, basta calcular as duas últimas. A largura do grupo esquerdo é 125,3013, então a largura do grupo direito é:

800 menos 125,3013, ou seja, 674,6987

Com as áreas já conhecidas, as alturas saem da divisão:

- parte 20: 115.662,6500 dividido por 674,6987 dá aproximadamente 171,4285
- parte 50: 289.156,6250 dividido por 674,6987 dá aproximadamente 428,5714

Somando as duas alturas chegamos a aproximadamente 600. Está certo.

As dimensões finais ficam:

- parte 1: 125,3013 por 46,1538
- parte 2: 125,3013 por 92,3076
- parte 10: 125,3013 por 461,5380
- parte 20: 674,6987 por 171,4285
- parte 50: 674,6987 por 428,5714

Com isso dá para escrever o script em PHP que gera o mapa de áreas. É preciso instalar a extensão gráfica, claro. O script de teste está no repositório e há uma versão publicada num servidor.


# Solução mais flexível

### Mapa com 3 linhas e 2 colunas

Depois de discutir minha solução e rever as regras que eu mesmo impus, concluí que não preciso de regra tão rígida.

Primeiro conversei com outra pessoa sobre uma dúvida: com 9 itens, dá para montar 3 colunas de 3 itens ou 2 colunas, uma com 5 e outra com 4. Não sei qual regra força uma das opções e não obtive resposta definitiva, então levei a pergunta ao assistente, que respondeu conforme a imagem.

![Chat GPT answer](images/resposta-sobre-colunas.png).

Posso então deixar a escolha com o usuário. Além dessa escolha, fixamos o número de linhas. Precisamos testar as regras. A primeira:

- no mínimo 1 coluna;
- no máximo 4 colunas. Por quê? Imagine 20 itens: um mapa com 20 colunas de um item cada fica estranho. Ajustando a largura de cada coluna e respeitando a altura, cada retângulo continua proporcional ao valor. Fiz um esboço abaixo:

```
 _ _________
|_|_________|

```

Mas essa regra de máximo pode ser ignorada sem quebrar a solução. Obviamente não faz sentido escolher 5 colunas para 3 itens. O máximo de colunas precisa ser o número de itens.

Acho que a ideia geral ficou clara. O usuário escolhe a quantidade de itens, os valores e o número de colunas, que varia de 1 a 4 e nunca passa do total de itens.

Ele também informa o tamanho total em dois campos, resultando em algo como 1000 por 2000.

Vamos usar área total de 850 por 550 e 6 itens, alternando entre os arranjos 2 por 3 e 3 por 2.

Começando pelo 3 por 2.

Os valores sorteados são:

- 5
- 8
- 9
- 14
- 15
- 17

Os menores valores vão para a direita. E se forem 7 valores? Isso também não é problema, porque já montamos um mapa com 5 itens no início do documento. Basta distribuir mais itens por coluna, ajustando a largura da coluna e a altura de cada linha. As linhas não precisam ter a mesma altura. Comentários:

- a largura varia de coluna para coluna, mas todos os itens de uma coluna têm a mesma largura;
- a altura varia de item para item, porque é preciso manter a área proporcional ao valor, e a proporção entre área e valor é a mesma para todos.

Um ponto interessante: como escolher quantos itens por coluna? O usuário escolhe o número de colunas, não a quantidade por coluna.

Exemplos com três colunas:

- 6 itens: 3 colunas de 2 (3x2 = 6);
- 7 itens: 1 coluna de 3 e 2 colunas de 2 (3 + 2 + 2 = 7);
- 8 itens: 3 colunas de 3, 3 e 2 (soma 8);
- 9 itens: 3 colunas de 3.

A regra testada para 6 itens, em PHP, distribui os itens com arredondamento para cima da divisão entre o restante e o número de colunas ainda vazias, e funciona para 6, 7, 8 e 9 itens, reduzindo o restante até zerar.

Testando 7 itens: a primeira coluna recebe 3, o restante fica 4; a segunda recebe 2 e o restante 2; a terceira recebe 2 e zera.

Para 8 itens: primeira coluna com 3, restante 5; segunda com 3, restante 2; terceira com 2.

Para 9 itens: primeira com 3, restante 6; segunda com 3, restante 3; terceira com 3.

A solução de escolher quantos itens por coluna funciona.

Voltando ao desafio anterior: o usuário escolheu 2 colunas, com 6 itens, então 3 itens por coluna, e área total de 850 por 550.

Repetindo os valores sorteados: 5, 8, 9, 14, 15 e 17.

O algoritmo devolve 2 colunas de 3 itens cada.

A área total é 467.500.

A soma dos valores é 68.

O fator de escala fica em 467.500 dividido por 68, ou seja, 6.875.

Não teremos altura única de linha, mas precisamos da mesma largura dentro da coluna, não só uma largura única por coluna.

Os menores valores vão para a coluna da esquerda. Como a largura varia entre colunas, as áreas ficam corretamente distribuídas.

Proporcionalmente aos valores, as áreas são:

- valor 5: 34.375
- valor 8: 55.000
- valor 9: 61.875
- valor 14: 96.250
- valor 15: 103.125
- valor 17: 116.875

A soma dessas áreas precisa dar a área total. Conferindo: dá exatamente 467.500.

Com duas colunas, a da esquerda fica com os menores valores e os retângulos variam de altura.

A altura total é 550, distribuída proporcionalmente entre os valores 5, 8 e 9, que somam 22.

- valor 5: 550 dividido por 22, vezes 5, dá 125
- valor 8: o mesmo cálculo dá 200
- valor 9: o mesmo cálculo dá 225

Somando as alturas: 550. Certo.

As larguras nessa coluna são iguais e saem da divisão da área pela altura; nos três casos o resultado é 275.

A largura da coluna da direita é a diferença para a largura total: 850 menos 275, ou seja, 575.

Com as áreas e a largura, as alturas saem da divisão:

- valor 14: aproximadamente 167,3913
- valor 15: aproximadamente 179,3478
- valor 17: aproximadamente 203,2609

Somando, dá aproximadamente 550. Certo.

As dimensões e áreas ficam:

Coluna esquerda:

- valor 5: 275 por 125, área 34.375
- valor 8: 275 por 200, área 55.000
- valor 9: 275 por 225, área 61.875

Coluna direita:

- valor 14: 575 por 167,3913, área 96.250
- valor 15: 575 por 179,3478, área 103.125
- valor 17: 575 por 203,2609, área 116.875

O script com esses valores foi escrito em PHP com a extensão gráfica, e há uma versão dele publicada num servidor.


### Mapa com 2 linhas e 3 colunas

Agora o mesmo conjunto de valores, mas com 3 colunas, num arranjo de 2 por 3.

Os valores sorteados continuam os mesmos: 5, 8, 9, 14, 15 e 17.

Os menores ficam à esquerda e, quando dois valores caem na mesma coluna, o menor fica em cima, gerando as colunas: 5 e 8, 9 e 14, 15 e 17.

Ignorando o script que escolhe a quantidade por coluna, repetimos os mesmos números do exemplo anterior:

- área total igual a 467.500
- soma dos valores igual a 68
- fator de escala igual a 6.875

As proporções no eixo vertical ficam:

- valor 5: 550 dividido por 13, vezes 5, dá aproximadamente 211,5385
- valor 8: o mesmo cálculo dá aproximadamente 338,4615

Somando: aproximadamente 550. Certo.

- valor 9: 550 dividido por 23, vezes 9, dá aproximadamente 215,2174
- valor 14: o mesmo cálculo dá aproximadamente 334,7826

Somando: aproximadamente 550. Certo.

- valor 15: 550 dividido por 32, vezes 15, dá 257,8125
- valor 17: o mesmo cálculo dá 292,1875

Somando: 550. Certo.

As áreas, pelo fator de escala, são as mesmas já calculadas: 34.375, 55.000, 61.875, 96.250, 103.125 e 116.875.

Como temos altura e área de cada item, as larguras saem da divisão:

- valor 5: aproximadamente 162,5
- valor 8: aproximadamente 162,5 (mesma largura, como esperado)
- valor 9: aproximadamente 287,5
- valor 14: aproximadamente 287,5 (mesma largura)
- valor 15: 400
- valor 17: 400 (mesma largura)

Resumindo as dimensões para montar o script gráfico:

- valor 5: 162,5 por 211,5385
- valor 8: 162,5 por 338,4615
- valor 9: 287,5 por 215,2174
- valor 14: 287,5 por 334,7826
- valor 15: 400 por 257,8125
- valor 17: 400 por 292,1875

O script está no repositório, e há uma versão publicada num servidor.
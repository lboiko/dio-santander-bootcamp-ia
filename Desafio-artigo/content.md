# Introdução

Olá pessoal! Hoje vamos falar sobre subqueries e consultas aninhadas em SQL, mas de um jeito bem fácil e simples. Prontos para aprender algo novo e divertido sobre bancos de dados?

## O que são Subqueries, ou Consultas Aninhas, em SQL

Subqueries, também chamadas de Consultas Aninhadas, são como fazer uma pergunta dentro de outra pergunta. Imagina que você quer saber quantos amigos vieram para a festa, mas primeiro precisa contar quantos carros estão estacionados. A subquery responde essa primeira pergunta.

Existem três tipos de subqueries. A primeira é a subquery simples, que responde com um valor só. Por exemplo:

```sql
SELECT MAX(preço) FROM produtos;
```
A segunda é a subquery de múltiplas linhas, que responde com vários valores:

```sql
SELECT nome FROM produtos WHERE preço IN (SELECT preço FROM promoções);
```
A terceira é a subquery correlacionada, que usa informações da pergunta maior para funcionar:

```sql
SELECT nome FROM produtos p WHERE preço > (SELECT AVG(preço) FROM produtos WHERE categoria = p.categoria);
```

## Exemplos de Uso Prático de Subqueries

Vamos ver como usar subqueries de um jeito prático. Se você quer descobrir o preço mais alto de uma categoria específica de brinquedos, você pode usar esta subquery:

```sql
SELECT MAX(preço) FROM produtos WHERE categoria = 'Brinquedos';
```

Outro exemplo é listar produtos que têm preço acima da média:

```sql
SELECT nome FROM produtos WHERE preço > (SELECT AVG(preço) FROM produtos);
```

## Usando consultas aninhadas em comandos DML

Vamos falar sobre como usar consultas aninhadas em SQL para fazer coisas legais como adicionar, atualizar ou apagar informações no banco de dados. É como resolver um quebra-cabeça onde você tem que juntar várias partes para conseguir o que quer. Veremos alguns exemplos a seguir:

### Exemplo de UPDATE com Consulta Aninhada
Imagine que você tem uma loja de videogames e quer aumentar o preço de todos os jogos de uma certa categoria em 10%. Primeiro, você precisa descobrir quais jogos são dessa categoria e depois mudar o preço deles. Olha só como fazemos isso:

```sql
INSERT INTO jogos (nome, preço, categoria)
SELECT 'Novo Jogo', 49.99, 'Aventura'
WHERE NOT EXISTS (SELECT 1 FROM jogos WHERE nome = 'Novo Jogo');
```

Aqui, a consulta dentro da outra (`SELECT categoria FROM categorias WHERE nome = 'Ação'`) encontra todos os jogos de ação, e a consulta principal muda o preço deles.

### Exemplo de DELETE com Consulta Aninhada

Agora, imagine que você quer apagar todos os jogos que não estão em promoção. Primeiro, você vê quais jogos estão em promoção e depois apaga os que não estão. Assim que fazemos:

```sql
DELETE FROM jogos
WHERE id NOT IN (SELECT jogo_id FROM promoções);
```

Neste exemplo, a consulta dentro da outra (`SELECT jogo_id FROM promoções`)acha todos os jogos que estão em promoção, e a consulta principal apaga os que não estão nessa lista.

### Exemplo de INSERT com Consulta Aninhada

Vamos dizer que você quer adicionar um novo jogo à lista, mas só se ele já não estiver lá. Primeiro, você checa se o jogo já existe na lista, e depois adiciona se não existir:

```sql
Copiar código
INSERT INTO jogos (nome, preço, categoria)
SELECT 'Novo Jogo', 49.99, 'Aventura'
WHERE NOT EXISTS (SELECT 1 FROM jogos WHERE nome = 'Novo Jogo');
```

Neste caso, a consulta dentro da outra (`SELECT 1 FROM jogos WHERE nome = 'Novo Jogo'`) verifica se o jogo já está na lista. Se não estiver, o novo jogo é adicionado.

## Subqueries Correlacionadas e Não-Correlacionadas

Subqueries correlacionadas são especiais porque dependem da pergunta maior para cada resposta. É como ver o preço de um brinquedo e comparar com a média dos preços dos brinquedos da mesma categoria:

```sql
SELECT nome FROM produtos p WHERE preço > (SELECT AVG(preço) FROM produtos WHERE categoria = p.categoria);
```

Já as subqueries não correlacionadas são independentes, como descobrir o preço máximo de todos os produtos sem dividir por categoria:

```sql
SELECT nome FROM produtos WHERE preço > (SELECT AVG(preço) FROM produtos);
```

## Desempenho e Otimização de Subqueries

Subqueries podem deixar o banco de dados lento, como um computador que fica devagar com muitos jogos abertos. Para otimizar, você pode usar índices para encontrar dados mais rápido e evitar subqueries desnecessárias, preferindo JOINs quando possível. Refatorar (reescrever o código) subqueries em JOINs geralmente deixa as consultas mais rápidas e ajuda a encontrar onde estão os problemas de desempenho.

# Conclusão

Gostou do conteúdo? Ele foi gerado por inteligência artificial, mas foi revisado por alguém 100% humano, e se quiser conectar comigo, me siga no Linkedin.

Fontes de produção
Ilustrações de capa: gerada pelo Dreamstudio.
Conteúdo gerado por: ChatGPT e revisões humanas.

#SQL #DataAnalysis #TechTips
# Programação Funcional Deve Ser Sua Prioridade número #1 em 2015
### - OOP não pode mais nos salvar do *Cloud Monster*

* **Artigo Original**: [Functional Programming should be your #1 priority for 2015](https://medium.com/@jugoncalves/functional-programming-should-be-your-1-priority-for-2015-47dd4641d6b9)
* **Tradução**: [Eric Douglas](https://github.com/ericdouglas) e [Diogo Beato](https://github.com/diogobeato)

Você provavelmente já ouviu expressões como "Clojure", "Scala", "Erlang", ou mesmo "Java agora tem *lambdas*". E você deve saber que isso tem alguma coisa a ver com "Programação Funcional". Se você participa de qualquer comunidade de programação, esse assunto provavelmente apareceu alguma vez.

Se você já buscou por "Functional Programming" (ou Programação Funcional), viu que não existe nada de novo. A segunda linguagem criada já utilizava isso, apareceu por volta da década de 50, nominada *Lisp*. Por que, então, as pessoas estão empolgadas com isso apenas agora? Quase 60 anos depois!?

## No início, os computadores eram realmente lentos

Acredite nisso ou não, computadores eram muuuuito mais lentos que o DOM. Não, sério. E naquele tempo, existiam duas mentalidades principais em termos de arquitetura e implementação de linguagens de programação:

1. Iniciar pela Arquitetura Von Neumann e adicionar abstração.
1. Iniciar pela Matemática e remover abstração.

Os computadores não tinham tanto poder de processamento para lidar com abstrações por todo o caminho e executar os programas funcionais. Então, Lisp acabou sendo mortalmente lenta, portanto, não adequada para o trabalho. Foi quando a programação imperativa começou sua dominação, especialmente com a ascenção do *C*.

### Mas os computadores melhoraram muito

Agora é virtualmente possível rodar a maioria das aplicações sem se preocupar muito sobre em qual linguagem foi escrita. Finalmente, linguagens funcionais tiveram sua segunda chance.

## Programação Funcional 50.5

Isso não é uma introdução a *FP* (*Functional Programming*). No fim dessa seção, você deverá ter uma ideia de o que *FP* é e como começar sua jornada.

Você pode entender Programação Funcional por programação com funções, que é, de fato, muito mais literal do que você pode imaginar agora. Você vai criar funções em termos de outras funções e compor funções (Você se lembra `f ∘ g` da escola? Isso vai ser útil agora).

Aqui temos uma (não-exaustiva) lista de características da FP:

1. First-Class Functions (Funções de Primeira Classe)
1. High-Order Functions (Funções de Alta Ordem)
1. Pure Functions (Funções Puras)
1. Closures
1. Immutable State (Imutabilidade de Estado)

Você não deve se preocupar com nomes *sofisticados* agora: apenas entenda o que eles significam.

**First-Class Functions**, ou *Funções de Primeira Classe*, significa que você vai armazenar funções dentro de uma variável. Acredito que você já fez algo parecido com isso em JavaScript:

```js
var add = function(a, b){
  return a + b
}
```

Você está apenas armazenando uma função anônima que recebe `a` e `b`, e retorna `a + b`, dentro de uma variável denominada `add`.

**High-Order Functions**, ou *Funções de Alta Ordem*, significa que funções podem retornar funções ou receber funções como parâmetro.

Novamente, em JavaScript:

```js
document.querySelector('#button')
  .addEventListener('click', function(){
    alert('yay, i got clicked')
  }) 
```

ou

```js
var add = function(a){
  return function(b){
    return a + b
  }
}
 
var add2 = add(2)
add2(3) // => 5 
```

Ambos os casos são um exemplo de Funções de Alta Ordem, mesmo que você nunca tenha usado algo parecido com isso, provavelmente você já viu algo assim em algum lugar.

**Pure Functions**, ou *Funções Puras*, significa que funções não mudam nenhum valor, elas apenas recebem dados e retornam dados, assim como nossas amadas funções da Matemática. Isso também significa que, se você passar `2` para uma função `f` e ela retornar `10`, ela sempre irá retornar `10`. Não importa o ambiente, threads, ou qualquer ordem de avaliação. Ela não causa nenhum efeito colateral em outras partes do programa, e isso é realmente um conceito poderoso.

**Closures** significa que você pode salvar algum dado dentro de uma função que é apenas acessível à função de retorno, isto é, a função retornada mantém seu ambiente de execução.

```js
var add = function(a){
  return function(b){
    return a + b
  }
}
 
var add2 = add(2)
add2(3) // => 5 
```

Verifique o segundo exemplo de *High-Order Function* novamente. A variável foi *fechada* e é acessível somente para a função retornada.

**Immutable State** ou *Estado Imutável* signifca que você não pode alterar o estado de forma alguma (embora você possa gerar um novo estado). No seguinte código (em OCaml), você pode usar `x` e `5` alternadamente em seu programa. `x` vai sempre ser `5`.

```ocaml
let x = 5;;
x = 6;;
 
print_int x;;  (* prints 5 *)
```

Isso parece muito mais com um ponto negativo que uma boa característica, mas você vai ver que isso salvará sua vida.

## Programação Orientada a Objetos não pode mais nos salvar

Aquele momento de que teríamos aplicações concorrentes e distribuídas rodando finalmente chegou.

Infelizmente, nós não estamos prontos: nosso "atual" (i.e., mais usado) modelo para concorrência e paralelismo, embora resolva o problema, ainda traz muita complexidade.

Para termos melhores aplicações, precisamos de uma maneira simples e confiável para fazer isto. Você se lembra das features de FP mencionados acima? *Pure Functions* (Funções Puras) e *Immutable State* (Imutabilidade de Estado)? Exatamente. Você pode rodar uma função milhares de vezes em diferentes *cores* ou máquinas que ainda assim não terá resultados diferentes dos que teve anteriormente. Sendo assim, você pode usar o mesmo código para rodar em 1 *core* ou em 1k de *cores*. Podemos ser felizes novamente.

> "Mas por que eu não posso continuar usando POO?"

Ao menos para concorrência e paralelismo, POO não pode mais te salvar. Isso porque, POO precisa que haja estados mutáveis. Os métodos dos objetos que você invoca, normalmente, servem para alterar o estado do objeto em questão ou de outro. E, trabalhando com concorrência, precisamos adicionar muita complexidade para mantermos sincronizadas todas as threads que utilizam esses objetos concorrentemente ou paralelamente.

Eu não estou aqui para argumentar que você deve sair do seu paradigma atual para o FP (mesmo que [algumas pessoas digam pra você fazer](https://blog.inf.ed.ac.uk/sapm/2014/03/06/enemy-of-the-state-or-why-oop-is-not-suited-to-large-scale-software/), mas definitivamente você precisa dominá-lo: O Java 8 e C++11 incorporaram as expressões lambda em suas plataformas. Posso afirmar que toda linguagem moderna e ainda mantida vai contar com features de FP em breve. E a maioria delas já tem.

Vale a pena mencionar que você não vai parar de usar estados mutáveis. Nós precisamos para desenvolver funcionalidades como IO e etc, para termos bons softwares. Porém, a ideia principal que FP provê é: use estados mutáveis apenas quando for necessário.

## Eu não trabalho com Cloud, eu realmente preciso de FP?

Sim.

Programação Funcional irá te ajudar a escrever melhores programas e raciocinar sobre os problemas que você tem que resolver.

>"Eu tentei. Mas é muito complexo e tem péssima legibilidade."

Tudo é difícil no começo. Eu tenho certeza que você ralou para aprender a programar e também para aprender POO. Provavelmente começar a fazer algo em POO foi mais fácil do que escrever seu primeiro programa. Principalmente porque você já estava familiarizado com alguns conceitos comuns, como declaração de variáveis e estruturas de repetição como *for*/*while*.

Para começar com FP, é quase como começar a aprender a programar de novo (dependendo de qual linguagem você escolher, será definitivamente como aprender a programar do zero).

Muitos podem argumentar que FP tem má legibilidade. Se você vem de um *background* imperativo, códigos funcionais irão parecer como uma linguagem criptografada. Não porque está realmente criptografado, mas porque você ainda não conhece os conceitos comuns. Uma vez que você dominar esses fundamentos, se tornará muito mais fácil de ler.

Veja esse código a seguir, escrito em Haskell e JavaScript (usando estilo imperativo):

```haskell
guess :: Int -> [Char]
guess 7 = "Much 7 very wow."
guess x = "Ooops, try again."
```

```js 
function guess(x){
  if(x == 7){
    return "Much 7 very wow."
  }
  else {
    return "Oops, try again."
  }
}
```

Esse é um programa muito simples que exibe uma mensagem de parabéns quando o usuário digita `7` e uma mensagem de erro para outros valores. Pode parecer magia negra como o Haskell faz isso em apenas 2 linhas de código (ignore a primeira linha por enquanto, é apenas "anotações de tipo"). Mas é muito simples depois que você entende *Pattern Matching* (que não é só implementado em linguagens FP, mas principalmente nelas).

O que o Haskell está fazendo:

Se o argumento da função `guess` for igual a `7`, retorna **"Much 7 very wow."** ou retorne **“Ooops, try again.”** para qualquer outro valor. E é exatamente o que o código JavaScript está fazendo, mas o Haskell está identificando através de um "padrão" provido pelo programador.

Pode parecer que não vale a pena usar isso uma vez que você pode simplesmente usar um if/else. Mas isso é muito poderoso quando estamos trabalhando com estruturas de dados complexas.

```haskell 
plus1 :: [Int] -> [Int]
plus1 []      = []
plus1 (x:xs)  = x + 1 : plus1 xs 
 
-- plus1 [0,1,2,3]
-- > [1,2,3,4]
```

No programa acima, **plus1** é uma função que recebe uma lista de Ints e e adiciona `1` para cada elemento da lista. Ele identifica o padrão de uma lista vazia `[]` (e retorna outra lista vazia, já que não há elementos para adicionar `1`) e quando ele identificar o padrão de uma lista com elementos: nomeia o primeiro elemento da lista como **x** e os elementos restantes como **xs**. Então, executa a soma e concatena com o retorno da chamada recursiva.

Eu tenho certeza que você passaria por maus bocados tentando reescrever a função `plus1` usando estilo imperativo em duas linhas de código e ainda deixá-lo legível.
 

## Então, vamos começar

Exite muito conteúdo por aí falando sobre Programação Funcional, mas alguns que você não pode perder são:

* [Principles of Functional Programming in Scala](https://www.coursera.org/course/progfun)

* [Introduction to Functional Programming](https://www.edx.org/course/introduction-functional-programming-delftx-fp101x) ([Contents](https://github.com/fptudelft/FP101x-Content))
* [Paradigms of Computer Programming — Fundamentals](https://www.edx.org/course/paradigms-computer-programming-louvainx-louv1-1x#.VKXX2orF_rd)

Infelizmente, eles costumam iniciar no fim do ano, mas você pode seguir o conteúdo e os videos que estão disponíveis no youtube.

Por outro lado, se você prefere livros, eu recomendo fortemente esses a seguir:

* [Structure and Interpretation of Computer Programs](https://mitpress.mit.edu/sicp/full-text/book/book.html)

* [How to Design Programs](http://htdp.org/)

* [Concepts, Techniques, and Models of Computer Programming](http://www.amazon.com/Concepts-Techniques-Models-Computer-Programming/dp/0262220695)

Boa Sorte no seu novo ano Funcional! ☺

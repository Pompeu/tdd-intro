# tdd-intro

# Introdução ao TDD com Javacript / NODEJS

## Como começar

+ Verifique versão do node com  o comando node -v  na linha de comando.
+ Verifique versão do npm com npm -v.
+ Instale o mocha “sudo npm install -g mocha”.
+ Tenha certeza que está tudo instalado e continue.

## Breve Introdução ao TDD (Test Driver Development)
O TDD (Desenvolvimento Guiado por Testes) é uma metodologia de desenvolvimento, onde deve-se criar um teste antes de criar o código fonte. Com isso ganha uma série de benefícios, como um código mais limpo e simples de manter, e ao final todo seu código já possui uma cobertura de testes automatizados, ou seja, seu sistema nasce testado.

Essa metodologia também é conhecida como Vermelho, Verde e Refatorar, uma analogia à forma como um Junit trabalha. O Junit é um framework usado para criar testes unitários e automatizados em Java, a grande maioria dos frameworks criados para a atividade do TDD, segue essa regra, onde fica vermelho nas falhas e verde nos sucessos. Veja a imagem 1:

![tdd](http://tableless.com.br/wp-content/uploads/2013/12/TDD-ciclo-vermelho-verde-refatora-591x310.jpg) 

Deve ser lembrado que o pai dessa metodologia, o grande Kent Beck, criou o TDD, o XP e o Junit, e também é um dos nomes famosos no manifesto ágil.

<a href="https://www.youtube.com/watch?v=1zaCvLVU70o" target=”_blank” >Video Sobre Kent Back e JUNIT</a>

Observações

Test-Driven Development (TDD), sem dúvida, tornou-se uma das práticas mais populares entre desenvolvedores de software. A ideia é bem simples: escreva seus testes antes mesmo de escrever o código de produção. Mas por quê a ideia parece tão boa? Ao escrever os testes antes, o desenvolvedor garante que boa parte (ou talvez todo) do seu sistema tem um teste que garanta o seu funcionamento. Além disso, muitos desenvolvedores também afirmam que os testes os guiam no projeto de classes do sistema.
Mesmo com toda a indústria gritando as vantagens para quem queira ouvir, ainda existem mitos em torno da prática. O desenvolvedor agora vai gastar mais tempo escrevendo testes do que programando? Escrever testes dá trabalho. Testes manuais não são mais produtivos? TDD deve ser feito 100% do tempo?
Este guia visa responder essas e outras perguntas para você, que é desenvolvedor, gerente, ou está de alguma forma relacionado ao processo de desenvolvimento de software.
By Mauricio Anche.


## Passo 01

Depois dessa breve introdução ao TDD, vamos começar nosso trabalho que é criar uma função que converte números romanos.

Crie uma pasta de nome “conversor_de_romanos”, e nela crie outras duas sub-pastas, models e testes.
A pasta models terá um arquivo com a função de converter os números romanos em números naturais e a pasta de testes terá o arquivo para fazer o testes. Pois bem, vamos conhecer nossa tarefa.

Nossa tarefa consiste em passar um valor romano para uma função, e ela retornar seu valor em número arábico como resposta. Pois bem, vamos conhecer a tabela de números romanos.

#### Tabela de números romanos

  <b>
    I  = 1 <br />
    V = 5 <br />
    X = 10 <br />
    L = 50 <br />
    C = 100 <br />
    D = 500 <br />
    M = 1000 <br />
  </b>

A segunda etapa desse projeto é criar o primeiro teste, então vamos ao passo 02.
 
## Passo 02

Dentro da pasta testes, crie um arquivo com o nome conversor-romanos.spec.js. Feito isso, vamos criar o primeiro teste de acordo com a Test 1. Perceba que será usado o módulo assert, ele é nativo do node, e sua função é validar os resultados da execução da função. A api do assert pode ser consultada em :  <a href=”https://nodejs.org/api/assert.html” > Assert Node 5 </a>.

### Test 1

```js

'use strict';
const assert = require('assert');

describe('testing module conversor de romanos', () => {

  const Conversor = require('./models/conversor-romanos');

  describe('testes da função converte', () => {

    it( 'deve entender  o simbolo I ', done => {
      let conversor = Conversor.converte("I");
      assert.equal(1 , conversor);
      done();
    });

  });
});

```

## Rodando o Tests 

Para rodar o teste vamos usar o mocha que foi instalado globalmente, usaremos  o comando :

```
  mocha conversor-romanos.spect.js
```

Feito isso, deverá aparecer uma mensagem de erro, pois ainda não criamos o módulo conversor-de-romanos.js na pasta models, e esse é o momento de criá-lo e nele fazer a implementação mais simples possível para que o teste passe e fique verde bem rápido.

Com o arquivo criado, vamos implementar esse módulo criando a função converte(), de modo que ela  possa retornar o número 1, no código 2 pode ser vista essa implementação, verifique ela é muito simples.

#### Código 2

```js
‘use strict’;

/*
   um detalhe sobre esse módulo é que ele já exporta a função executada,
   ou seja, podemos usar a função converte (arg);
   que é um serviço exportado pelo módulo conversor.
*/

module.exports = conversor();

function  conversor() {
  const service = {
    converte : converte;
  };

  return service;
  // essa abordagem é a mais simples possível
  // conhecida como baby steps, termo cunhado pelo criador do TDD/XP Kent Beck
  function  converte (romanNumber) {
    if(romanNumber === 'I') return 1;
  }

}
```

Agora chegou a hora de rodar novamente o teste e verificar seu resultado :

```
mocha conversor-romanos.spect.js
```

<pre class=”green”>
   ✓ deve entender  o simbolo I
</pre>

E agora que o teste passou, já sabemos como converter o romano I para valor 1. Vamos para o próximo teste?

## Passo 3

Criando um teste para o valor V, ele deverá retornar o valor 5. Dentro do arquivo de teste, na função describe logo após o primeiro teste, implemente o código 2.

### Test 2

```js

   it( 'deve entender  o simbolo V ', done => {
      let conversor = Conversor.converte("V");
      assert.equal(5 , conversor);
      done();
   });

```

Dando continuidade, rode o mocha novamente e o teste deverá falhar, pois não foi feita a implementação da função converte para que ela entenda o valor V.

Vamos fazer essa implementação seguindo sempre pela forma mais simples possível, ou seja, a função deverá ter um if que retorne o valor 5 para o caso da entrada V.

```js

  function  converte (romanNumber) {
    if(romanNumber === 'I') return 1;
    else if(romanNumber === 'V') return 5;
  }

```

Rode o teste, ele deverá passar. 

```
mocha conversor-romanos.spect.js
```

<pre class=”green”>
   ✓ deve entender  o símbolo I
   ✓ deve entender  o símbolo V
</pre>


Essa é portanto, a primeira parte da introdução, nosso conversor de romanos até o momento consegue converter dois valores, porém esse é o momento de dar um passo maior, pois em um sistema criar if e else if para tudo não é uma boa prática.

Como vamos resolver esse problema, nos conhecemos todos os números romanos, ok? que estão listados na nossa tabela. Pois bem, vamos criar um Mapa (Map) e nele vamos adicionar as chaves e valores, porém antes vamos criar mais 1 teste, para o valor M que deverá retornar 1000.

### Teste 3

```js

   it( 'deve entender  o simbolo M ', done => {
      let conversor = Conversor.converte("M");
      assert.equal(1000 , conversor);
      done();
   });

```

Siga os passos anteriores, rode o mocha, veja o teste falhar, em seguida verifique como ficou a implmentação do arquivo de modelo, nele foi usado Map para guardar os números romanos de uma forma mais estruturada.

```js

module.exports = conversor();

/*
  criando um mapa para valores romanos
  onde sua chave é o valor em romano
  e seu valor e um número arábico correspondente
*/

let map =  new Map();
// set(CHAVE, VALOR);
map.set("I", 1);
map.set("V", 5);
map.set("X", 10);
map.set("L", 50);
map.set("C", 100);
map.set("D", 500);
map.set("M", 1000);


function  conversor() {
  
  let service = {
    converte : converte;
  };

  return service;
  /*
    implementação nova da função converte,
    onde ele pega um número romano, faz a 
    consulta no map usando sua chave e 
    nos devolve um valor.
  */
  function  converte (romanNumber) {
    //get recebe uma chave e retorna um valor
    return map.get(romanNumber);
  }

}

```
Agora rodando o mocha, deverá ser vista a seguinte tela no seu terminal, onde todos os testes passaram.

<pre class=”green”>
  ✓ deve entender o símbolo I 
  ✓ deve entender o símbolo V 
  ✓ deve entender o símbolo M
</pre>

Esse foi o final da parte 1 do tutorial de introdução ao TDD, esse exemplo foi tirado do livro TDD no mundo real, do grande Maurício Aniche, que é hoje na minha humilde opinião uma das maiores referências de TDD no mundo acadêmico, ele fez seu mestrado e agora faz doutorado sobre o assunto, também é professor na Caelum, ou seja, vale a pena seguir esse cara para quem quer aprofundar no assunto.

Se você quer aprender mais sobre TDD usando nodeJS, não deixe de ver a continuação dessa série, e faça o curso Be Mean da WebSchool, onde eu serei o responsável pela parte de testes automatizados do curso. Um ótimo local para ler e aprender sobre TDD é o blog do Maurício Anishe <a href="http://www.aniche.com.br/tdd/" > link </a>.

Vamos para a segunda parte do tutorial? “Em Breve”



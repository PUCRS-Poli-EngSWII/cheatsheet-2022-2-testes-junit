# Grupo 2
### Arthur Gil, Fernanda Rosa, Henrique Lima, Henrique Xavier, Louise Dornelles e Rafael Cardoso 

## Testes Unitários e de Integração

### O que são
Os **testes unitários**, ou testes de unidade visam garantir a qualidade do código em sua menor fração. Esses, não dependem de recursos externos, e são usados para analisar o comportamento da menor unidade possível do código, não se preocupando com a relação entre funções e outras partes do código. Seu objetivo principal é verificar cada unidade que compõe o software de forma isolada. Além disso, os testes unitários, também servem para garantir que sua aplicação continue funcionando após alguma alteração na base do código.
### Algumas vantages dos testes unitários:
<li>Aumentar a produtividade do desenvolvedor</li>
<li>Garantir a eficiência do escopo escolhido</li>
<li>Prevenir problemas futuros</li>
<li>Garantir um software de qualidade</li>
<li>Garantir que os módulos, as funções estão com seu comportamento correto</li>
<li>Aumentar a velocidade do código</li>
<br></br>

Os **testes de integração** têm o objetivo de encontrar falhas de integração entre as unidades de compõe o software, e não em testar as funcionalidades individuais. Dessa maneira, esses testes visam validar se os componentes de um sistema interagem da forma esperada e correta. Esses testes são indispensáveis para que seja possível garantir uma boa performance do sistema, já que com esses é possível encontrar falhas, erros e bugs durante o desenvolvimento de um software.
Eles são responsáveis por aumentar a segurança e a eficiência de uma aplicação antes de concluir o projeto. A médio e longo prazo, isso economiza tempo e dinheiro, por isso é imprescindível.
O cenário ideal é primeiro fazer os testes unitários a cada nova funcionalidade e unidade adicionada ao software e depois fazer o teste de integração para garantir que os módulos funcionam juntos.


## A Ferramenta Básica: JUnit
### O que é

JUnit é um framework open-source que visa facilitar o desenvolvimento, escrita e execução de testes unitários em Java. Essa framework fornece uma API completa para ser possível construir testes e executá-los em modo console.

### Motivos para usar JUnit:
<li>Facilita a criação e execução de testes </li>
<li>É orientada a objeto</li>
<li>É gratuito</li>
<li>Pode verificar se cada unidade de código funciona da maneira que se espera</li>

### Cookbook
Para a criaçao de testes é simples e rápido, sendo executado automaticamente.
Primeiramente é preciso que tenha o código ou tenha como ele deverá se comportar.
Assim, criamos um novo arquivo que por convenção tenha o mesmo nome do arquivo a ser testado com `.test` no final.

Para criar um teste, devemos adicionar a anotaçao `@test` em cima de cada método de teste.
Para o exemplo iremos testar uma função que deve retornar um *boolean* para indicar se o valor passado é ímpar.
Devemos fazer essa validaçao usando o `assertTrue()`. Dessa maneira, ele verifica o valor booleno passado para ele.

Assim, ficamos com o código
```
import org.junit.Assert.*;

class testOddNumberFunction {

    private final Funtion func = new Function();
    @Test
    void oddNumber() {
        assertTrue(func.oddNumber(7);
    }
}
```


### Pacotes (imports)
Os pacotes são utilizados na adição de funcionalidades já disponibilizadas pelo JUnit por padrão. É possivel importar tais pacotes ultilizando a API padrão do Junity.
Como podemos ver no código a seguir, um exmplo simples de uma calculadora ultilizando a biblioteca Jupter encontrada no site oficial do JUnit:
```
import static org.junit.jupiter.api.Assertions.assertEquals;

import example.util.Calculator;

import org.junit.jupiter.api.Test;

class MyFirstJUnitJupiterTests {
    private final Calculator calculator = new Calculator();
    @Test
    void addition() {
        assertEquals(2, calculator.add(1, 1));
    }
}
```
Os pacotes sao importado de como: import org.junit.[pacote desejado].

### Anotações

#### **@Test**
Essa anotação indica que o método é um método de teste.
Exemplo:
```
@Test 
void helloJUnit5() {
    assertEquals(10, 5+5);
}
```

#### **@ParameterizedTest**
Testes parametrizados fazem com que seja possível rodar testes várias vezes com parâmetros diferentes. Ao usar essa anotação nos métodos de teste, é necessário declarar a fonte dos parâmetros para cada chamada do teste. Isso pode ser feito com a anotação **@ValueSource** e especificar um array, por exemplo.
````
@ParameterizedTest
@ValueSource(strings = {"cali", "bali", "dani"})
void endsWithI(String str) {
    assertTrue(str.endsWith("i"));
}
```` 
#### **@RepeatedTest**
Com essa anotação é possível repetir um test específico um certo número de vezes, especificando esse número na anotação
````
@RepeatedTest(value = 5, name = "{displayName} {currentRepetition}/{totalRepetitions}")
@DisplayName("RepeatingTest")
void customDisplayName(RepetitionInfo repInfo, TestInfo testInfo) {
    int i = 3;
    System.out.println(testInfo.getDisplayName() + "-->" + repInfo.getCurrentRepetition());

    assertEquals(repInfo.getCurrentRepetition(), i);
}
````

#### **@BeforeEach**
O método que tiver essa anotação será executado antes de cada método de teste.
```
@BeforeEach
void init(TestInfo testInfo) {
    String callingTest = testInfo.getTestMethod().get().getName();
    System.out.println(callingTest);
}
``` 

### Asserções
Asserções em JUnit ajudam a validar os resultados esperados com o atual resultado de uma função de teste. Para isso, diversas funções de asserções estão disponíveis na classe [org.junit.jupiter.Assertions](https://junit.org/junit5/docs/current/api/org.junit.jupiter.api/org/junit/jupiter/api/Assertions.html).

### **assertEquals()** e **assertNotEquals()**
Verifica se o valor esperado é igual ao valor real da função (assertEquals). De forma contrária, assertNotEquals verifica se o valor esperado não é igual ao valor real da função.
```
@Test
void Test(){
    //Test will pass
    assertEquals(4, Calculator.add(2, 2));
     
    //Test will fail 
    assertEquals(3, Calculator.add(2, 2), "Calculator.add(2, 2) test failed");
     
    //Test will pass
	assertNotEquals(3, Calculator.add(2, 2));

	//Test will fail
	assertNotEquals(4, Calculator.add(2, 2), "Calculator.add(2, 2) test failed");
}
```

### **assertArrayEquals()**
Verifica se o array esperado é igual ao array real retornado da função.

```
@Test
void testCase()
{
	//Test will pass
	Assertions.assertArrayEquals(new int[]{1,2,3}, new int[]{1,2,3}, "Array Equal Test");

	//Test will fail because element order is different
	Assertions.assertArrayEquals(new int[]{1,2,3}, new int[]{1,3,2}, "Array Equal Test");

	//Test will fail because number of elements are different
	Assertions.assertArrayEquals(new int[]{1,2,3}, new int[]{1,2,3,4}, "Array Equal Test");
}
```

### **assertNull()** e **assertNotNull()**
Verifica se o valor atual é nulo/não é nulo.

```
@Test
void testCase()
{
	String nullString = null;
	String notNullString = "howtodoinjava.com";

	//Test will pass
	Assertions.assertNotNull(notNullString);

	//Test will fail
	Assertions.assertNotNull(nullString);

	//Test will pass
	Assertions.assertNull(nullString);

	// Test will fail
	Assertions.assertNull(notNullString);
}
```

### Exemplos
-----------------------------------

### Referências

LIMA, Davyson. Entenda por uma vez por todas o que são testes unitários, para que servem e como fazê-los. 2017. Disponível em: <https://dayvsonlima.medium.com/entenda-de-uma-vez-por-todas-o-que-são-testes-unitários-para-que-servem-e-como-fazê-los-2a6f645bab3>. Acesso em 25 de Novembro de 2022.

<lb>

DEVMEDIA. Como você testa seus códigos? Disponível em: <https://www.devmedia.com.br/e-ai-como-voce-testa-seus-codigos/39478>. Acesso em 25 de Novembro de 2022.

<lb>

DEVMEDIA. Testes de integração na prática. 2014. Disponível em: <https://www.devmedia.com.br/teste-de-integracao-na-pratica/31877>. Acesso em 25 de Novembro de 2022.

<lb>

KRIGER, Daniel. O que é teste de integração e quais são os tipos de teste? 2021. Disponível em: <https://kenzie.com.br/blog/teste-de-integracao/>. Acesso em 25 de Novembro de 2022.

<lb>

DEVMEDIA. JUnit Tutorial. Disponível em: <https://www.devmedia.com.br/junit-tutorial/1432>. Acesso em 25 de Novembro de 2022.

<lb>

GHAHRAI, Amir. JUnit 5 Annotations with examples. 2019. Disponível em: <https://devqa.io/junit-5-annotations/>. Acesso em 26 de Novembro de 2022.

<lb>

HOWTODOINJAVA. JUnit 5 Assertions with Examples. 2022. Disponível em: <https://howtodoinjava.com/junit5/junit-5-assertions-examples/>. Acesso em 26 de Novembro de 2022.

<lb>

JUNIT. Class Assertions. 2019. Disponível em: <https://junit.org/junit5/docs/current/api/org.junit.jupiter.api/org/junit/jupiter/api/Assertions.html>. Acesso em 26 de Novembro de 2022.

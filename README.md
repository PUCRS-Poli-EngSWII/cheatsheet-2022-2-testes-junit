# Grupo 2
### Arthur Gil, Fernanda Rosa, Henrique Lima, Henrique Xavier, Louise Dornelles e Rafael Cardoso 
<br></br>
## Testes Unitários e de Integração

### O que são
Os **testes unitários**, ou testes de unidade, visam garantir a qualidade do código em sua menor fração. Esses, não dependem de recursos externos, e são usados para analisar o comportamento da menor unidade possível do código, não se preocupando com a relação entre funções e outras partes do código. Seu objetivo principal é verificar cada unidade que compõe o software de forma isolada. Além disso, os testes unitários também servem para garantir que sua aplicação continue funcionando após alguma alteração na base do código.
### Algumas vantages dos testes unitários:
<li>Aumenta a produtividade do desenvolvedor</li>
<li>Garante a eficiência do escopo escolhido</li>
<li>Prevene problemas futuros</li>
<li>Garante um software de qualidade</li>
<li>Garante que os módulos, as funções estão com seu comportamento correto</li>
<li>Aumenta a velocidade do código</li>
<br></br>

Os **testes de integração** têm o objetivo de encontrar falhas de integração entre as unidades que compõe o software, e não de testar as funcionalidades individuais. Dessa maneira, esses testes visam validar se os componentes de um sistema interagem da forma esperada e correta. Portanto, esses testes são indispensáveis para que seja possível garantir uma boa performance do sistema, já que com eles é possível encontrar falhas, erros e bugs durante o desenvolvimento de um software.

Ademais, são responsáveis por aumentar a segurança e a eficiência de uma aplicação antes de concluir o projeto. Também, a médio e longo prazo, economizam tempo e dinheiro, por isso são imprescindíveis.
O cenário ideal é, primeiro, fazer os testes unitários a cada nova funcionalidade e unidade adicionada ao software, para então fazer o teste de integração a fim de garantir que os módulos realmente funcionam juntos.


## A Ferramenta Básica: JUnit

<img src="JUnit_5_Banner.png" width=400 heigth=150/>

<br></br>

### O que é

JUnit é um framework open-source que visa facilitar o desenvolvimento, escrita e execução de testes unitários em Java. Essa framework fornece uma API completa para ser possível construir testes e executá-los em modo console.

### Motivos para usar JUnit:
<li>Facilita a criação e execução de testes </li>
<li>É orientada a objeto</li>
<li>É gratuito</li>
<li>Pode verificar se cada unidade de código funciona da maneira que se espera</li>
<br></br>


### **Pacotes (imports)**
Os pacotes são utilizados na adição de funcionalidades já disponibilizadas pelo JUnit em princípio. É possivel importar tais pacotes ultilizando a API padrão do Junit. Abaixo, é evidenciada essa funcionalidade através de uma código simples que implementa uma calculadora através da biblioteca Jupiter, encontrada no site oficial do JUnit:
```java
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
Os pacotes são importado como: `import org.junit.[pacote desejado]`.
<br></br>
### **Anotações**

#### **@Test**
A anotação @Test indica que o método a seguir trata-se de um teste.
Exemplo:
```java
@Test 
void helloJUnit5() {
    assertEquals(10, 5+5);
}
```

#### **@ParameterizedTest**
A anotação @ParameterizedTest indica que se trata de Testes parametrizados, eles fazem com que seja possível rodar testes várias vezes com parâmetros diferentes. Ao usar essa anotação nos métodos de teste, é necessário declarar a fonte dos parâmetros para cada chamada do teste. Isso pode ser feito com a anotação **@ValueSource** e especificar um array, por exemplo.
```java
@ParameterizedTest
@ValueSource(strings = {"cali", "bali", "dani"})
void endsWithI(String str) {
    assertTrue(str.endsWith("i"));
}
``` 
#### **@RepeatedTest**
Com essa anotação, é possível repetir um teste específico um certo número de vezes, determinando esse número na anotação.
```java
@RepeatedTest(value = 5, name = "{displayName} {currentRepetition}/{totalRepetitions}")
@DisplayName("RepeatingTest")
void customDisplayName(RepetitionInfo repInfo, TestInfo testInfo) {
    int i = 3;
    System.out.println(testInfo.getDisplayName() + "-->" + repInfo.getCurrentRepetition());

    assertEquals(repInfo.getCurrentRepetition(), i);
}
```

#### **@BeforeEach**
O método que tiver essa anotação será executado antes de **cada** método de teste da classe.
```java
@BeforeEach
void init(TestInfo testInfo) {
    String callingTest = testInfo.getTestMethod().get().getName();
    System.out.println(callingTest);
}
``` 

#### **@AfterEach**
O método que tiver essa anotação será executado depois de **cada** método de teste da classe.
```java
@AfterEach
void after(TestInfo testInfo) {
    String callingTest = testInfo.getTestMethod().get().getName();
    System.out.println(callingTest);
}
```

#### **@BeforeAll**
O método que tiver essa anotação será executado uma vez antes de **todos** os outros métodos de teste da classe.
```java
@BeforeAll
static void beforeAll() {
    System.out.println("Esse método será executado uma vez antes de todos os testes");
}
```
#### **@AfterAll**
O método que tiver essa anotação será executado uma vez depois de **todos** os outros métodos de teste da classe.
```java
@AfterAll
static void afterAll() {
    System.out.println("Esse método será executado uma vez depois de todos os testes");
}
```

#### **@Ignore**
Essa anotação é adicionada aos casos de teste que se deseja ignorar. Assim, ao criar um método de teste e adicionar essa anotação, esse não será executado.
```java
@Ignore
@Test
static void testIgnored() {
    System.out.println("Esse teste não será executado");
}
```
<br></br>

### **Asserções**
Asserções em JUnit ajudam a validar os resultados esperados com o atual resultado de uma função de teste. Para isso, diversas funções de asserções estão disponíveis na classe [org.junit.jupiter.Assertions](https://junit.org/junit5/docs/current/api/org.junit.jupiter.api/org/junit/jupiter/api/Assertions.html).

### **assertEquals()** e **assertNotEquals()**
Essas anotações verificam se o valor esperado é igual (assertEquals) ou diferente (assertNotEquals) do valor real da função.
```java
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
Verifica se o array esperado é igual ao array real retornado pela função.

```java
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
Tais asserções verificam se o valor atual é ou não nulo.

```java
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

### **assertThrows()**
Asserções verificam o lancamento de exceções. A exceção deve ocorrer
na função lambda passada como parâmetro para a asserção.

```java
@Test
void assertThrowsException() {
    String str = null;
    assertThrows(IllegalArgumentException.class, () -> {
      Integer.valueOf(str);
    });
}
```



<br></br>
## Exemplo

```java
class Calculator {
    // Soma dois inteiros.
    public int add(a, b) {
        return a + b;
    }

    // Multiplica dois inteiros iguais.
    // Se os valores forem diferentes, lança um exceção.
    public int multiplyEquals(a, b) {
        if (a == b) {
            return a * b;
        }
        throw new IllegalArgumentException;
    }
}
```

```java
import org.junit.*;
// import Calculator...

class CalculatorTest {
    Calculator calc = new Calculator();

    @Test
    public void shouldAddTwoIntegers() {
        int a = 5;
        int b = 9;
        
        int expected = 14;
        
        assertEquals(expected, Calculator.add(a, b));
    }

    @Test
    public void shouldMultiplyTwoIntegersWhenTheyAreEqual() {
        a = 5;
        b = 5;
        
        int expected = 25;

        assertEquals(expected, Calculator.multiplyEquals(a, b));
    }

    @Test
    public void shouldThrowExceptionWhenMultiplyingDiferentIntegers() {
        a = 5;
        b = 10;

        assertThrows(IllegalArgumentException.class, () -> {
            Calculator.multiplyEquals(a, b);
        });
    }
}
```
## Cobertura de Código
Além de bons métodos, é necessário ter o máximo de cobertura de código possível, com o intuito de garantir que todos os componentes serão devidamente testados. Baseado nessa questão, o **Code Coverage** foi desenvolvido, sendo uma ferramenta de análise de cobertura em um driver, determinando quantas linhas foram validadas com sucesso. Após submeter o código a esse software, o desenvolvedor estará apto a mais facilmente identificar necessidades de casos de teste adicionais.


-----------------------------------

### Referências

LIMA, Davyson. Entenda por uma vez por todas o que são testes unitários, para que servem e como fazê-los. 2017. Disponível em: [Entenda por uma vez por todas o que são testes unitários, para que servem e como fazê-los](https://dayvsonlima.medium.com/entenda-de-uma-vez-por-todas-o-que-são-testes-unitários-para-que-servem-e-como-fazê-los-2a6f645bab3). Acesso em 25 de Novembro de 2022.


DEVMEDIA. Como você testa seus códigos? Disponível em: [Como você testa seus códigos?](https://www.devmedia.com.br/e-ai-como-voce-testa-seus-codigos/39478). Acesso em 25 de Novembro de 2022.


DEVMEDIA. Testes de integração na prática. 2014. Disponível em: [Testes de integração na prática](https://www.devmedia.com.br/teste-de-integracao-na-pratica/31877). Acesso em 25 de Novembro de 2022.


KRIGER, Daniel. O que é teste de integração e quais são os tipos de teste? 2021. Disponível em: [O que é teste de integração e quais são os tipos de teste?](https://kenzie.com.br/blog/teste-de-integracao/). Acesso em 25 de Novembro de 2022.


DEVMEDIA. JUnit Tutorial. Disponível em: [JUnit Tutorial](https://www.devmedia.com.br/junit-tutorial/1432). Acesso em 25 de Novembro de 2022.


GHAHRAI, Amir. JUnit 5 Annotations with examples. 2019. Disponível em: [JUni5 5 Annotations with examples](https://devqa.io/junit-5-annotations/). Acesso em 26 de Novembro de 2022.


HOWTODOINJAVA. JUnit 5 Assertions with Examples. 2022. Disponível em: [JUnit 5 Assertions with examples](https://howtodoinjava.com/junit5/junit-5-assertions-examples/). Acesso em 26 de Novembro de 2022.


JUNIT. Class Assertions. 2019. Disponível em: [Class Assertions](https://junit.org/junit5/docs/current/api/org.junit.jupiter.api/org/junit/jupiter/api/Assertions.html). Acesso em 26 de Novembro de 2022.


BAELDUNG. A Guide to JUnit 5. 2022. Disponível em: [A Guide to JUnit 5](https://www.baeldung.com/junit-5). Acesso em 29 de Novembro de 2022.

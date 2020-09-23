---
layout: post
title:  "Api Stream do Java'"
date:  2020-09-22 19:02:00
categories: Java Api Stream Programação
---

A Stream é uma classe do pacote `Package java.util.stream`.

## API STREAM DO JAVA

A Stream é uma classe do pacote `Package java.util.stream`.

A mencionada classe oferece suporte a operações de estilo funcional em fluxos de elementos, como transformações de redução de mapa em coleções.

A Stream pode ser descrita como uma “sequência de elementos de uma fonte de dados que oferece suporte a diferentes tipos de operações de agregação”.[1]

A **stream** provê uma interface para um conjunto de valores de um determinado tipo, consumindo dados de uma fonte, como coleções, arrays ou mesmo recursos de E/S (entrada e saída);

As Streams suportam operações comuns a linguagens de programação funcionais, como filtrar, modificar, transformar o elemento em outro e assim por diante. Essas operações podem ser realizadas em série ou em paralelo.

Importante mencionar que as **Streams** não armazenam elementos, os dados são processados sob demanda.

As Streams se diferem das operações sobre coleções, especialmente pelas características `Pipeline` e `Iteração Interna`, que são:

1. **Pipeline**: É o fluxo de processamento,  ocasionado por uma cadeia de operações feitas sobre os Streams, considerando a maior parte de suas operações retornam novas streams, há o encadeamento dessas opeções, tornando o fluxo resultante na chamada `Pipeline`.

2. **Iteração interna**: As coleções usam, em geral, os loops ou  os iteradores para percorrer seus elementos. Esse tipo de operação é conhecido como iteração externa e é claramente perceptível no código. 

   Já na API Stream é possível encontrar métodos como map(), forEach(), filter(), entre outros, que percorrem uma sequência de elementos internamente, assim, a iteração ou loop fica encapsulado na API, restando ao desenvolvedor somente direcionar o objeto da iteração.

Seguem abaixo lista de exemplos da API Stream, retirados do curso de `Implementando Collections e Streams com Java` da Digital Inovation One

``` java
import java.util.ArrayList;
import java.util.Comparator;
import java.util.List;
import java.util.stream.Collectors;

public class ExemplosStreamAPI {

    public static void main(String[] args) {

        // Cria a coleção denominada estudantes
        List<String> estudantes = new ArrayList<>();
        estudantes.add("Pedro");
        estudantes.add("Renata");
        estudantes.add("Carla");
        estudantes.add("Patricia");
        estudantes.add("Jose");


        // Retorna a contagem de elementos do stream
        System.out.println("Contagem: " + estudantes.stream().count());

        // Retorna o elemento com maior numero de letras
        System.out.println("Maior numero de letras: " + estudantes.stream().max(Comparator.comparingInt(String::length)));

        // Retorna o elemento com menor numero de letras
        System.out.println("Menor numero de letras: " + estudantes.stream().min(Comparator.comparingInt(String::length)));

        // Retorna os elementos que tem a letra R no nome
        System.out.println("Com a letra r no nome: " + estudantes.stream().filter((estudante) -> estudante.toLowerCase().contains("r")).collect(Collectors.toList()));

        // Retorna uma nova coleção, com os nomes concatenados a quantidade de letra de cada nome
        System.out.println("Retorna uma nova coleção com a quantidade de letras: " + estudantes.stream().map(estudante ->
                estudante.concat(" - ").concat(String.valueOf(estudante.length()))).collect(Collectors.toList()));

        // Retorna somente os 3 primeiros elementos da coleção
        System.out.println("Retorna os 3 primeiros elementos: " + estudantes.stream().limit(3).collect(Collectors.toList()));

        // Exibe cada elemento no console, e depois retorna a mesma coleção
        System.out.println("Retorna os elementos: " + estudantes.stream().peek(System.out::println).collect(Collectors.toList()));

        // Exibe cada elemento no console sem retornar outra coleção
        System.out.print("Retorna os elementos novamente: ");
        estudantes.stream().forEach(System.out::println);

        // Retorna true se todos os elementos possuem a letra W no nome
        System.out.println("Tem algum elemento com W no nome? " + estudantes.stream().allMatch((elemento) -> elemento.contains("W")));

        // Retorna true se algum os elementos possuem a letra a minúscula no nome
        System.out.println("Tem algum elemento com a minúscula no nome? " + estudantes.stream().anyMatch((elemento) -> elemento.contains("a")));

        // Retorna true se nenhum elemento possue a letra a minúscula no nome
        System.out.println("Não tem nenhum elemento com a minúscula no nome? " + estudantes.stream().noneMatch((elemento) -> elemento.contains("a")));

        // Retorna o primeiro elemento da coleção, se existir exibe no console
        System.out.print("Retorna o primeiro elemento da coleção: ");
        estudantes.stream().findFirst().ifPresent(System.out::println);

        // Exemplo de operação encadeada
        System.out.print("Operaçõa encadeada: ");
        System.out.println(estudantes.stream()
                .peek(System.out::println)
                .map(estudante ->
                        estudante.concat(" - ").concat(String.valueOf(estudante.length())))
                .peek(System.out::println)
                .filter((estudante) ->
                        estudante.toLowerCase().contains("r"))
                .collect(Collectors.toList()));
    }
}

```

Pelos exemplos acima, verificamos que é possível a utilização de expressões lambda, tornado as operações mais simples, podendo percorrer as coleções cada item por vez.

#### Conclusão

A API Stream facilita a utilização das collections, facilitando que sejam implementadas sobre elas as operações.

**Referências**:

[1] https://www.oracle.com/br/technical-resources/articles/java-stream-api.html

https://docs.oracle.com/javase/8/docs/api/java/util/stream/package-summary.html

https://www.devmedia.com.br/java-streams-api-manipulando-colecoes-de-forma-eficiente/37630

http://www.matera.com/blog/post/entendendo-a-stream-api-do-java-8
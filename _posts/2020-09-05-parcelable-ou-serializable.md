---
layout: post
title:  "Quando implementar o Parcelable ou o Serializable?"
date:  2020-09-10 17:09:00
categories: Java Aplicações Parcelable Serializable
---

Baseado na resposta do Stackoverflow feita pelo usuário **emanuelsn**

[Stackoverflow]: https://pt.stackoverflow.com/questions/38492/quando-e-como-implementar-o-parcelable-vs-serializable/38509#38509



## Quando implementar o Parcelable ou o Serializable?

Após muito tempo utilizando a implementação Serializable nas minhas classes na plataforma Java(Android), descobri o Parcelable, mas fiquei na dúvida em relação as seguintes questões abaixo:

Vamos lá:

### 1. Parcelable vs Serializable, o que utilizar ? 

Vejamos os principais prós e contras de cada implementação. 

* Usar Serializable é mais fácil e mais rápido de ser implementado. Entretanto, a performance é pior. 

* Usar Parcelable gasta um pouco mais de tempo para implementar, por ser um pouco mais verboso para implementar, e, é um pouco mais complexo que o Serializable. Em contrapartida, o uso do Parcelable resulta numa performance melhor.

### *2. Como implementar o Parcelable?*

Abaixo, segue um exemplo de uma classe que implementa o Parcelable.

```java
import android.os.Parcel;
import android.os.Parcelable;

public class Estudante implements Parcelable {
 private String nome;

 public Estudante(String id, String nome) {
   this.nome = nome;
 }

 private Estudante(Parcel parcel){
   nome = from.readString();
 }

 public String getNome() {
   return nome;
 }

 public void setNome(String nome) {
   this.nome = nome;
 }

 @Override
 public int describeContents() {
   return 0;
 }

 @Override
 public void writeToParcel(Parcel dest, int flags) {
   dest.writeString(nome); 
 }
    
public static final Parcelable.Creator<Estudante> CREATOR = new Parcelable.Creator<ClientEstudante>() {

   public Estudante createFromParcel(Parcel parcel) {
     return new Estudante(parcel);
   }

   public Estudante[] newArray(int size) {
     return new Estudante[size];
   }
 };

}
```



#### Override dos Métodos de "describeContents" e "writeToParcel"

Nota-se que houve a reescrita de dois métodos: `describeContents` e `writeToParcel`. 

* O `describeContents` é um método que retorna um inteiro que identifica a classe. 

* O `writeToParcel`  serializa as informações da classe. 

#### Construtor Privado

É criado um construtor privado da Classe que recebe um `Parcel`, através dele que lê-se os dados e passa para os atributos.

O construtor privado é chamado para o atributo estático `CREATOR`.

#### Atributo Estático CREATOR

As classes que implementam o Parcelable, devem transcrever esse atributo o atributo estático `CREATOR`, é por ela que são implementadas as funcionalidades de `DataInputStream` e `DataOutputStream` para serializar e deserializar objetos. 

#### Passar e Receber os dados Parcelable via Intent

Para que se passe os dados Parcelable via Intent, faz-se:

```java
Estudante estudante = new Estudante("Humberto");
Intent i = new Intent(this, OutraActivity.class);
it.putExtra("estudante", estudante);
startActivity(i);
```

Para ler os dados, é bem simples:

```java
Estudante e =  getIntent().getExtras().getParcelable("estudante");
```



### *3. Como implementar o Serializable?*

A interface Serializable é padrão do Java, portanto, pode-se apenas implementar a interface serializável e sobrescrever os métodos necessários.

Como já informando,  a abordagem de utilização da interface Serializable é um processo lento, pois, cria muitos objetos temporários, dando trabalho ao `garbage collection`.

 No entanto, a interface serializável é mais fácil de implementar:

```java
import java.io.Serializable;
public class Estudante implements Serializable{

    private int matricula;
    private String nome;

    public int getMatricula() {
        return matricula;
    }
    public void setMatricula(int matricula) {
        this.matricula = matricula;
    }
    public String getNome() {
        return nome;
    }
    public void setNome(String nome) {
        this.nome = nome;
    }
}
```

#### Passar e Receber os dados Serializable via Intent

Para que se passe os dados Serializable via Intent, faz-se:

```java
Estudante estudante = new Estudante( 12345,"Humberto");
Intent i = new Intent(this, OutraActivity.class);
it.putExtra("estudante", estudante);
startActivity(i);
```

Para ler os dados, é bem simples:

```java
Estudante e =  getIntent().getExtras().getParcelable("estudante");
```

Deste modo, é possível ainda passar objetos, adicionando-os a listas. Conforme a implementação de exemplo abaixo:

```java
//Cria-se a Lista de "estudantes"
ArrayList<Estudante> estudantes = new ArrayList<Estudante>();
estudantes.add(new Estudante(12345, "Humberto"));
estudantes.add(new Estudante(67890, "Doisberto"));

// Enviar dados via intent
Intent i = new Intent(this, OutraActivity.class);
// Pode-se passar somente um obeto: 
it.putExtra("estudante", estudantes.get(0)); 
// Passar toda lista
it.putExtra("estudantes", estudantes); 
startActivity(i);
```

Para recuperar os dados, implementamos: 

```java
// Recupera quando enviado somente um objeto
Estudante estudante = (Estudante) getIntent().getSerializableExtra("estudante");

// Recupera quando enviada lista de objetos
ArrayList<Estudante> estudantes = (ArrayList<Estudante>) getIntent().getSerializableExtra("estudantes");
```



**Consultar as seguintes referências:**

[Implementação do Parcelable e Serializable](http://www.developerphil.com/parcelable-vs-serializable/)

[Documentação Oficial - Parcelable](http://developer.android.com/reference/android/os/Parcelable.html)

[Documentação Oficial - Serializable](http://developer.android.com/reference/java/io/Serializable.html)

[Postagem do StackOverFlow - (en)](https://stackoverflow.com/questions/3323074/android-difference-between-parcelable-and-serializable)
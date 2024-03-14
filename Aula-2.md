
### Explicação do Código

-   `public class Main`: Define uma classe pública chamada `Main`.
-   `public static void main(String[] args)`: Método principal que é o ponto de entrada de qualquer programa Java.
-   `System.out.println("Olá, mundo!")`: Imprime a mensagem "Olá, mundo!" no console.

### Executando o Programa

1.  Salve o código em um arquivo chamado `Main.java`.
2.  Abra um terminal ou prompt de comando no diretório onde o arquivo está salvo.
3.  Compile o programa com o comando `javac Main.java`.
4.  Execute o programa com o comando `java Main`.

## Conceitos Básicos de POO

### Classes e Objetos

-   **Classe**: Um molde ou blueprint para criar objetos.
-   **Objeto**: Uma instância de uma classe.

### Atributos e Métodos

-   **Atributo**: Variáveis dentro de uma classe que representam estados ou propriedades.
-   **Método**: Funções dentro de uma classe que representam ações.

### Exemplo Simples

Vamos criar uma classe `Carro` com alguns atributos e métodos.
``` Java
public class Carro {
    String marca;
    int ano;
    boolean ligado;

    void ligar() {
        ligado = true;
        System.out.println("Carro ligado!");
    }

    void desligar() {
        ligado = false;
        System.out.println("Carro desligado!");
    }
}
```
### Criando e Usando Objetos

````  Java

public class Main {
    public static void main(String[] args) {
        Carro meuCarro = new Carro();
        meuCarro.marca = "Toyota";
        meuCarro.ano = 2021;
        meuCarro.ligar();
        // Saída: Carro ligado!
    }
}
````

## Conclusão

Você acabou de ter seu primeiro contato com POO em Java. 
Continue explorando e praticando para aprimorar suas habilidades. 

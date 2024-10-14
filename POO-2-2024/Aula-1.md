
# **Aprendendo a Criar classes: Desenvolvimento Orientado a Objetos (POO) em Java – Cadastro de Pessoas**

Hoje, vamos praticar os conceitos fundamentais de POO criando um sistema simples de **cadastro de pessoas**. Esse tutorial foi projetado para ser um **guia passo a passo**, ajudando você a estruturar e desenvolver um projeto do zero utilizando **classes, objetos, encapsulamento, e listas**.

---

## **Objetivos**
1. Entender os conceitos de **classe, objeto, atributos e métodos**.
2. Praticar **encapsulamento** usando **getters e setters**.
3. Criar e manipular uma **lista de objetos**.
4. Utilizar o método **main** para testar a aplicação.

---

## **Descrição do Problema**
Criaremos um programa em Java para um **Cadastro de Pessoas**. O sistema permitirá armazenar o nome, idade e e-mail de várias pessoas. As informações serão armazenadas em uma **lista**, e será possível **incluir** e **listar** essas pessoas.


## O que é uma LISTA ? 
Uma **lista** é uma **estrutura de dados** que armazena uma sequência ordenada de elementos, permitindo acesso, inserção e remoção de forma eficiente. Em linguagens de programação como **Java**, uma lista pode conter qualquer tipo de dado, como números, strings ou objetos, e é amplamente utilizada para armazenar e gerenciar coleções de dados.

---

## **Passo a Passo: Implementação do Projeto**

### 1. **Criando o Projeto em Java**
Se você estiver usando uma IDE como **Eclipse**, **IntelliJ IDEA**, ou **NetBeans**:
- Crie um novo **projeto Java**.
- Dentro do projeto, crie um **pacote** chamado `cadastro` (opcional, mas recomendado para organizar o código).

No projeto, você criará três classes:
- `Pessoa.java` (representação de uma pessoa)
- `Cadastro.java` (gerenciador da lista de pessoas)
- `App.java` (classe principal para rodar o programa)

---

### 2. **Criando a Classe Pessoa**

A classe `Pessoa` será uma **abstração** de uma pessoa, contendo atributos e métodos de acesso (getters e setters).

#### **Código da Classe Pessoa.java**
```java
package cadastro;

public class Pessoa {
    private String nome;
    private int idade;
    private String email;

    // Construtor
    public Pessoa(String nome, int idade, String email) {
        this.nome = nome;
        this.idade = idade;
        this.email = email;
    }

    // Getters e Setters
    public String getNome() {
        return nome;
    }

    public void setNome(String nome) {
        this.nome = nome;
    }

    public int getIdade() {
        return idade;
    }

    public void setIdade(int idade) {
        this.idade = idade;
    }

    public String getEmail() {
        return email;
    }

    public void setEmail(String email) {
        this.email = email;
    }

    // Método para exibir os dados da pessoa
    @Override
    public String toString() {
        return "Nome: " + nome + ", Idade: " + idade + ", Email: " + email;
    }
}
```

**Explicação:**

-   A classe `Pessoa` tem três **atributos privados**: `nome`, `idade` e `email`.
-   Os **getters** e **setters** permitem acessar e modificar esses atributos.
-   O método `toString()` exibe as informações de uma pessoa de forma legível.

### 3. **Criando a Classe Cadastro**

A classe `Cadastro` será responsável por **gerenciar a lista de pessoas**. Aqui, usaremos uma **lista** do tipo `ArrayList` para armazenar objetos do tipo `Pessoa`.

#### **Código da Classe Cadastro.java:**

```java
package cadastro;// SERÁ QUE PRECISO ? PENSA AI  ..... E FALA COMIGO 

import java.util.ArrayList;
import java.util.List;

public class Cadastro {
    private List<Pessoa> listaDePessoas;

    // Construtor
    public Cadastro() {
        listaDePessoas = new ArrayList<>();
    }

    // Método para adicionar uma pessoa à lista
    public void adicionarPessoa(Pessoa pessoa) {
        listaDePessoas.add(pessoa);
        System.out.println("Pessoa adicionada com sucesso!");
    }

    // Método para listar todas as pessoas cadastradas
    public void listarPessoas() {
        if (listaDePessoas.isEmpty()) {
            System.out.println("Nenhuma pessoa cadastrada.");
        } else {
            System.out.println("Pessoas cadastradas:");
            for (Pessoa p : listaDePessoas) {
                System.out.println(p);
            }
        }
    }
}

```

**Explicação:**

-   A classe `Cadastro` contém uma **lista** (`ArrayList`) de objetos `Pessoa`.
-   O método `adicionarPessoa()` adiciona uma nova pessoa à lista.
-   O método `listarPessoas()` exibe todas as pessoas cadastradas na lista.


### 4. **Criando a Classe Principal (App)**

A classe `App` conterá o método `main`, que será o **ponto de entrada** do programa. Aqui, faremos testes simples para adicionar e listar pessoas.

#### **Código da Classe App.java:**

```java
package cadastro;

import java.util.Scanner;

public class App {
    public static void main(String[] args) {
        Scanner scanner = new Scanner(System.in);
        Cadastro cadastro = new Cadastro();

        System.out.println("=== Sistema de Cadastro de Pessoas ===");

        while (true) {
            System.out.println("\n1. Adicionar Pessoa");
            System.out.println("2. Listar Pessoas");
            System.out.println("3. Sair");
            System.out.print("Escolha uma opção: ");
            int opcao = scanner.nextInt();
            scanner.nextLine(); // Consumir a quebra de linha

            switch (opcao) {
                case 1:
                    System.out.print("Nome: ");
                    String nome = scanner.nextLine();
                    System.out.print("Idade: ");
                    int idade = scanner.nextInt();
                    scanner.nextLine(); // Consumir a quebra de linha
                    System.out.print("Email: ");
                    String email = scanner.nextLine();

                    Pessoa pessoa = new Pessoa(nome, idade, email);
                    cadastro.adicionarPessoa(pessoa);
                    break;

                case 2:
                    cadastro.listarPessoas();
                    break;

                case 3:
                    System.out.println("Encerrando o programa...");
                    scanner.close();
                    System.exit(0);

                default:
                    System.out.println("Opção inválida. Tente novamente.");
            }
        }
    }
}

```

**Explicação:**

-   O método `main()` cria um objeto `Cadastro` e utiliza um **menu interativo** para adicionar ou listar pessoas.
-   O usuário pode digitar informações no console para cadastrar novas pessoas.
-   A opção **3** encerra o programa.

### 5. **Executando o Programa**

-   Compile e execute a classe `App`.
-   Teste as seguintes funcionalidades:
    1.  **Adicionar uma nova pessoa** (informe nome, idade e e-mail).
    2.  **Listar todas as pessoas cadastradas**.
    3.  **Sair do programa**.


### 6. **Desafios e Melhorias**

1.  **Validação**: Adicione verificações para evitar que o usuário insira uma idade negativa ou um e-mail inválido.
2.  **Excluir Pessoa**: Implemente um método para **remover** uma pessoa pelo nome.
3.  **Herança**: Crie uma subclasse `Funcionario` que herde de `Pessoa` e adicione um atributo extra como `salario`.

###  **Você aprendeu a:**


-   Criar e manipular **classes e objetos** em Java.
-   Utilizar **encapsulamento** com getters e setters.
-   Trabalhar com **listas** para armazenar objetos.
-   Estruturar um programa com **múltiplas classes**.

Esse é apenas o começo! A POO oferece muitas possibilidades para construir sistemas mais robustos e reutilizáveis. Continue explorando e experimentando para se aprofundar ainda mais.

Boa codificação! 🚀

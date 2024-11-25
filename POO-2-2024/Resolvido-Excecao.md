
# 1- Atividade Prática Resolvida: Tratamento de Exceções 

## Contexto
Você foi contratado para desenvolver um sistema que analisa uma lista de produtos de um supermercado a partir de um arquivo CSV. O arquivo contém os seguintes campos:

- **Produto**: Nome do produto.
- **Quantidade**: Quantidade em estoque.
- **Preço**: Preço unitário do produto. Preciso lembrar que preço não, é algo inteiro? Pelo amor de Deus ...... 

Sua tarefa é implementar um programa em Java que:

1. Leia o arquivo `produtos.csv`.
2. Calcule o valor total em estoque de cada produto (Quantidade x Preço).
3. Exiba os valores calculados no console.
4. Use tratamento de exceções para:
   - Lidar com problemas na leitura do arquivo.
   - Garantir que os dados no arquivo sejam válidos (e.g., preço e quantidade devem ser números válidos).
   - Garantir que o programa exiba uma mensagem apropriada no caso de qualquer falha.

### Exemplo do arquivo `produtos.csv`

```csv
Produto,Quantidade,Preço 
Arroz,50,5.99 
Feijão,30,7.49 
Macarrão,20,4.99 
Óleo,15,8.99
```


---

## Requisitos
Implemente o programa considerando:

1. **Tratamento de exceções**:
   - Use `try` para encapsular as operações que podem gerar erros.
   - Use `catch` para tratar exceções como:
     - `FileNotFoundException` (caso o arquivo não exista).
     - `NumberFormatException` (caso os valores de quantidade ou preço sejam inválidos).
     - Qualquer outra exceção genérica (`Exception`).
   - Use `finally` para garantir o fechamento do arquivo.

2. **Validação de dados**:
   - Certifique-se de que os valores de **Quantidade** e **Preço** sejam positivos.
   - Ignore produtos com dados inválidos e informe um erro no console.

3. **Resultado esperado**:
   - Para cada produto válido, exiba no console o nome do produto e o valor total em estoque.
   - Caso o arquivo ou algum dado seja inválido, exiba mensagens claras no console.

---

## Código Base para Implementação

```java
import java.io.*;
import java.util.Scanner;

public class TratamentoExcecoesSupermercado {

    public static void main(String[] args) {
        String caminhoArquivo = "produtos.csv";

        try (BufferedReader br = new BufferedReader(new FileReader(caminhoArquivo))) {
            String linha = br.readLine(); // Ler o cabeçalho
            if (linha == null) {
                throw new IOException("O arquivo está vazio.");
            }

            System.out.println("Produto - Valor Total em Estoque");
            while ((linha = br.readLine()) != null) {
                try {
                    String[] dados = linha.split(",");
                    String produto = dados[0];
                    int quantidade = Integer.parseInt(dados[1]);
                    double preco = Double.parseDouble(dados[2]);

                    if (quantidade < 0 || preco < 0) {
                        throw new IllegalArgumentException("Quantidade ou preço não podem ser negativos.");
                    }

                    double valorTotal = quantidade * preco;
                    System.out.printf("%s - R$ %.2f%n", produto, valorTotal);

                } catch (NumberFormatException e) {
                    System.out.println("Erro ao processar linha: " + linha + ". Dados inválidos.");
                } catch (IllegalArgumentException e) {
                    System.out.println("Erro: " + e.getMessage() + " Linha: " + linha);
                }
            }
        } catch (FileNotFoundException e) {
            System.out.println("Erro: Arquivo não encontrado.");
        } catch (IOException e) {
            System.out.println("Erro ao ler o arquivo: " + e.getMessage());
        } finally {
            System.out.println("Execução finalizada.");
        }
    }
}
```

## Execute os passos a seguir  

1.  **Crie o arquivo `produtos.csv`** com os dados do exemplo fornecido.
2.  **Copie o código base para um editor de texto ou IDE** e ajuste o caminho do arquivo.
3.  **Execute o programa e analise os resultados no console.**
4.  Experimente incluir dados inválidos no arquivo (e.g., quantidade ou preço como texto ou valores negativos) e observe como o programa reage.
5.  **Pense no funcionamento do `try`, `catch` e `finally` no contexto deste programa.**
6. Certifique-se de entender o fluxo de tratamento de exceções. Identifique as possíveis falhas e como o programa garante que o sistema continue funcionando sem interrupções.

---


## 2- AGORA A PARADA FICA SÉRIA 

### Criando Classes de Exceção Personalizadas em Java

## Contexto
Você está desenvolvendo um sistema para calcular o valor total de um pedido em uma loja virtual. O sistema deve validar os itens do pedido, garantindo que:

1. O preço de cada item seja maior que zero.
2. A quantidade de cada item seja maior que zero.
3. O valor total do pedido não ultrapasse um limite máximo definido (exemplo: R$ 10.000,00).

Caso alguma dessas regras seja violada, o sistema deve lançar exceções específicas para cada tipo de erro. Para isso, você deve criar **suas próprias classes de exceção personalizadas**.

---

## Requisitos

1. **Criação das Classes de Exceção**:
   - Crie três classes de exceção:
     - `PrecoInvalidoException`
     - `QuantidadeInvalidaException`
     - `ValorTotalExcedidoException`
   - Cada classe deve herdar de `Exception` e ter um construtor que receba uma mensagem descritiva.

2. **Validação de Dados**:
   - Ao adicionar um item ao pedido:
     - Verifique se o preço é maior que zero, caso contrário, lance `PrecoInvalidoException`.
     - Verifique se a quantidade é maior que zero, caso contrário, lance `QuantidadeInvalidaException`.
     - Verifique se o valor total do pedido não ultrapassa o limite máximo, caso contrário, lance `ValorTotalExcedidoException`.

3. **Exibição dos Resultados**:
   - Exiba uma mensagem clara no console indicando o problema quando uma exceção for lançada.
   - Permita que o programa continue funcionando para itens válidos mesmo após uma exceção.

---

## Código Base para Implementação

```java
// Classe de exceção para preço inválido
class PrecoInvalidoException extends Exception {
    public PrecoInvalidoException(String mensagem) {
        super(mensagem);
    }
}

// Classe de exceção para quantidade inválida
class QuantidadeInvalidaException extends Exception {
    public QuantidadeInvalidaException(String mensagem) {
        super(mensagem);
    }
}

// Classe de exceção para valor total excedido
class ValorTotalExcedidoException extends Exception {
    public ValorTotalExcedidoException(String mensagem) {
        super(mensagem);
    }
}

// Classe principal
public class PedidoLojaVirtual {

    private static final double LIMITE_MAXIMO = 10000.00;
    private double valorTotal = 0;

    public void adicionarItem(String produto, double preco, int quantidade) 
            throws PrecoInvalidoException, QuantidadeInvalidaException, ValorTotalExcedidoException {
        
        if (preco <= 0) {
            throw new PrecoInvalidoException("Preço inválido para o produto: " + produto);
        }
        if (quantidade <= 0) {
            throw new QuantidadeInvalidaException("Quantidade inválida para o produto: " + produto);
        }
        
        double valorItem = preco * quantidade;
        if (valorTotal + valorItem > LIMITE_MAXIMO) {
            throw new ValorTotalExcedidoException("Valor total excede o limite permitido ao adicionar o produto: " + produto);
        }

        valorTotal += valorItem;
        System.out.printf("Item adicionado: %s | Preço: R$ %.2f | Quantidade: %d | Valor Item: R$ %.2f%n", 
                          produto, preco, quantidade, valorItem);
    }

    public double getValorTotal() {
        return valorTotal;
    }

    public static void main(String[] args) {
        PedidoLojaVirtual pedido = new PedidoLojaVirtual();

        try {
            pedido.adicionarItem("Notebook", 4500.00, 2);
            pedido.adicionarItem("Smartphone", 2000.00, 3); // Deve lançar exceção de valor total excedido
        } catch (PrecoInvalidoException | QuantidadeInvalidaException | ValorTotalExcedidoException e) {
            System.out.println("Erro ao adicionar item: " + e.getMessage());
        }

        try {
            pedido.adicionarItem("Mouse", -50.00, 1); // Deve lançar exceção de preço inválido
        } catch (PrecoInvalidoException | QuantidadeInvalidaException | ValorTotalExcedidoException e) {
            System.out.println("Erro ao adicionar item: " + e.getMessage());
        }

        try {
            pedido.adicionarItem("Teclado", 120.00, -2); // Deve lançar exceção de quantidade inválida
        } catch (PrecoInvalidoException | QuantidadeInvalidaException | ValorTotalExcedidoException e) {
            System.out.println("Erro ao adicionar item: " + e.getMessage());
        }

        System.out.printf("Valor total do pedido: R$ %.2f%n", pedido.getValorTotal());
    }
}
```

## Tarefas do Aluno

1.  **Crie as três classes de exceção personalizadas** seguindo as definições fornecidas.
2.  **Implemente e execute o programa base**.
3.  Experimente adicionar diferentes itens ao pedido, incluindo casos válidos e inválidos.
4.  **Explique a si próprio como e por que as exceções personalizadas melhoram o código** em comparação com o uso de exceções genéricas.
5.  Explique o fluxo de controle quando uma exceção personalizada é lançada no programa.


## 3-  Veja  mais um problema 

### Sistema de Gerenciamento de Reservas de Hotel com Tratamento de Exceções

## Contexto

Um hotel deseja informatizar o sistema de gerenciamento de reservas. O hotel possui diferentes tipos de quartos (Standard, Luxo e Suíte), e os hóspedes podem reservar um quarto especificando as datas de entrada e saída. No entanto, para garantir o funcionamento correto do sistema, é necessário implementar regras de negócio rigorosas que devem ser tratadas adequadamente com exceções personalizadas.

Você foi contratado para desenvolver uma aplicação que permita o gerenciamento das reservas de quartos. Para isso, o sistema deve:

1. **Cadastrar quartos disponíveis**: O sistema deve permitir o cadastro de quartos, identificados por um número único, tipo e preço por diária.

2. **Registrar uma reserva**: O sistema deve permitir que os hóspedes façam reservas, desde que atendam às regras descritas abaixo.

3. **Regras de Negócio**:
   - **Disponibilidade**: Um quarto não pode ser reservado para datas em que já esteja ocupado. Caso isso aconteça, deve lançar uma exceção `QuartoIndisponivelException`.
   - **Datas inválidas**: A data de saída deve ser maior que a data de entrada. Caso contrário, lance uma exceção `DatasInvalidasException`.
   - **Hóspede menor de idade**: Apenas maiores de 18 anos podem fazer reservas. Caso a idade do hóspede seja menor que 18, deve lançar uma exceção `HospedeMenorDeIdadeException`.
   - **Pagamento insuficiente**: Antes de confirmar a reserva, o sistema deve calcular o valor total da estadia (número de diárias x preço do quarto) e verificar se o valor pago pelo hóspede cobre esse total. Caso contrário, deve lançar uma exceção `PagamentoInsuficienteException`.

4. **Listar reservas**: O sistema deve permitir que o administrador visualize todas as reservas realizadas.

---

## Exemplo de Funcionamento

- O hotel possui 3 quartos disponíveis:
  - Quarto 101 (Standard) - R$ 200,00 por diária
  - Quarto 102 (Luxo) - R$ 350,00 por diária
  - Quarto 103 (Suíte) - R$ 500,00 por diária
- Um hóspede chamado João, com 22 anos, tenta reservar o quarto 101 de 01/12/2024 a 05/12/2024, pagando R$ 800,00.
- O sistema verifica:
  - As datas são válidas? **Sim**
  - O quarto está disponível? **Sim**
  - O hóspede é maior de idade? **Sim**
  - O valor pago é suficiente? **Não**
- O sistema lança a exceção `PagamentoInsuficienteException` e exibe uma mensagem clara informando o motivo.

---

## Requisitos

1. **Criação de Exceções Personalizadas**:
   - `QuartoIndisponivelException`
   - `DatasInvalidasException`
   - `HospedeMenorDeIdadeException`
   - `PagamentoInsuficienteException`

2. **Implementação do Sistema**:
   - Crie as classes para representar os quartos, hóspedes e reservas.
   - Gerencie as reservas usando uma lista.
   - Implemente o tratamento de exceções usando `try-catch` para exibir mensagens claras quando as regras de negócio forem violadas.

---



import java.util.ArrayList;
import java.util.Scanner;

class Roupa {
    String marca;
    String tipo;
    String tamanho;
    int quantidade;
    double valor;

    Roupa(String marca, String tipo, String tamanho, int quantidade, double valor) {
        this.marca = marca;
        this.tipo = tipo;
        this.tamanho = tamanho;
        this.quantidade = quantidade;
        this.valor = valor;
    }

    double calcularValorTotal() {
        return quantidade * valor;
    }

    void adicionarEstoque(int qtd) {
        quantidade = quantidade + qtd; 
    }

    void removerEstoque(int qtd) {
        if (qtd > quantidade) {
            System.out.println("Erro: Não pode remover mais do que tem.");
        } else {
            quantidade = quantidade - qtd;
        }
    }

    void exibirInformacoes() {
        System.out.println("Marca: " + marca);
        System.out.println("Tipo: " + tipo);
        System.out.println("Tamanho: " + tamanho);
        System.out.println("Quantidade: " + quantidade);
        System.out.println("Valor unitário: R$ " + valor);
        System.out.println("Valor total: R$ " + calcularValorTotal());
    }
}

public class Main {
    public static void main(String[] args) {
        Scanner scanner = new Scanner(System.in);
        ArrayList<Roupa> estoque = new ArrayList<>();
        
        while (true) {
            System.out.println("\n1. Adicionar roupa");
            System.out.println("2. Adicionar estoque");
            System.out.println("3. Remover estoque");
            System.out.println("4. Mostrar roupas");
            System.out.println("5. Sair");
            System.out.print("Escolha: ");
            int opcao = scanner.nextInt();
            scanner.nextLine(); 

            if (opcao == 1) {
                System.out.print("Marca: ");
                String marca = scanner.nextLine();
                System.out.print("Tipo: ");
                String tipo = scanner.nextLine();
                System.out.print("Tamanho: ");
                String tamanho = scanner.nextLine();
                System.out.print("Quantidade: ");
                int qtd = scanner.nextInt();
                System.out.print("Valor: ");
                double valor = scanner.nextDouble();
                
                estoque.add(new Roupa(marca, tipo, tamanho, qtd, valor));
                System.out.println("Roupa adicionada.");
            } else if (opcao == 2) {
                System.out.print("Escolha índice da roupa: ");
                int i = scanner.nextInt();
                System.out.print("Quantidade para adicionar: ");
                int qtd = scanner.nextInt();
                
                if (i >= 0 && i < estoque.size()) {
                    estoque.get(i).adicionarEstoque(qtd);
                    System.out.println("Adicionado.");
                } else {
                    System.out.println("Índice errado!");
                }
            } else if (opcao == 3) {
                System.out.print("Escolha índice da roupa: ");
                int i = scanner.nextInt();
                System.out.print("Quantidade para remover: ");
                int qtd = scanner.nextInt();
                
                if (i >= 0 && i < estoque.size()) {
                    estoque.get(i).removerEstoque(qtd);
                    System.out.println("Removido.");
                } else {
                    System.out.println("Índice errado!");
                }
            } else if (opcao == 4) {
                for (int i = 0; i < estoque.size(); i++) {
                    System.out.println("Roupa [" + i + "]");
                    estoque.get(i).exibirInformacoes();
                }
            } else if (opcao == 5) {
                System.out.println("Encerrando programa.");
                break;
            } else {
                System.out.println("Opção errada, tente de novo.");
            }
        }
        
        scanner.close();
    }
}

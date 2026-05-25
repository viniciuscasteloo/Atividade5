# Atividade5

import java.util.ArrayList;
import java.util.HashMap;
import java.util.HashSet;
import java.util.LinkedList;
import java.util.Queue;
import java.util.Scanner;

// Classe Livro
class Livro {

    int codigo;
    String titulo;
    String autor;
    boolean disponivel;

    public Livro(int codigo, String titulo, String autor) {
        this.codigo = codigo;
        this.titulo = titulo;
        this.autor = autor;
        this.disponivel = true;
    }

    public void exibir() {
        System.out.println("Código: " + codigo);
        System.out.println("Título: " + titulo);
        System.out.println("Autor: " + autor);
        System.out.println("Disponível: " + disponivel);
        System.out.println("--------------------------");
    }
}

// Classe Pedido
class Pedido {

    int numero;
    String cliente;
    String item;
    double valor;
    String status;

    public Pedido(int numero, String cliente, String item, double valor) {
        this.numero = numero;
        this.cliente = cliente;
        this.item = item;
        this.valor = valor;
        this.status = "PENDENTE";
    }

    public void exibir() {
        System.out.println("Pedido: " + numero);
        System.out.println("Cliente: " + cliente);
        System.out.println("Item: " + item);
        System.out.println("Valor: R$ " + valor);
        System.out.println("Status: " + status);
        System.out.println("--------------------------");
    }
}

// Classe principal
public class Entrega5 {

    public static void main(String[] args) {

        Scanner sc = new Scanner(System.in);

        // 1. Lista de compras com ArrayList

        System.out.println("===== LISTA DE COMPRAS =====");

        ArrayList<String> produtos = new ArrayList<>();

        produtos.add("Arroz");
        produtos.add("Feijão");
        produtos.add("Macarrão");
        produtos.add("Leite");
        produtos.add("Café");

        for (String produto : produtos) {
            System.out.println(produto);
        }

        System.out.println("Quantidade total: " + produtos.size());

        // 2. Média de notas com ArrayList<Double>

        System.out.println("\nMédia de notas");

        ArrayList<Double> notas = new ArrayList<>();

        notas.add(8.5);
        notas.add(7.0);
        notas.add(6.5);
        notas.add(9.0);

        double soma = 0;

        for (double nota : notas) {
            soma += nota;
        }

        double media = soma / notas.size();

        System.out.println("Média da turma: " + media);

        if (media >= 7) {
            System.out.println("Turma aprovada.");
        } else {
            System.out.println("Turma reprovada.");
        }

        // 3. Controle de presença com HashSet

        System.out.println("\nPresença dos alunos");

        HashSet<String> alunos = new HashSet<>();

        alunos.add("Carlos");
        alunos.add("Maria");
        alunos.add("João");
        alunos.add("Ana");
        alunos.add("Maria");
        alunos.add("Carlos");

        for (String aluno : alunos) {
            System.out.println(aluno);
        }

        System.out.println("Quantidade de alunos: " + alunos.size());

        // 4. Cadastro de alunos com HashMap

        System.out.println("\nCadastro de alunos");

        HashMap<Integer, String> mapaAlunos = new HashMap<>();

        mapaAlunos.put(101, "Lucas");
        mapaAlunos.put(102, "Fernanda");
        mapaAlunos.put(103, "Bruno");

        int matriculaBusca = 102;

        if (mapaAlunos.containsKey(matriculaBusca)) {
            System.out.println("Aluno encontrado: "
                    + mapaAlunos.get(matriculaBusca));
        } else {
            System.out.println("Matrícula não encontrada.");
        }

        mapaAlunos.remove(103);

        System.out.println("\nLista de alunos:");

        for (Integer matricula : mapaAlunos.keySet()) {

            System.out.println("Matrícula: "
                    + matricula
                    + " Nome: "
                    + mapaAlunos.get(matricula));
        }

        // 5. Fila de atendimento com Queue

        System.out.println("\nFila de clientes");

        Queue<String> fila = new LinkedList<>();

        fila.add("Cliente 1");
        fila.add("Cliente 2");
        fila.add("Cliente 3");
        fila.add("Cliente 4");
        fila.add("Cliente 5");

        System.out.println("Próximo cliente: " + fila.peek());

        fila.poll();
        fila.poll();

        System.out.println("\nFila atualizada:");

        for (String cliente : fila) {
            System.out.println(cliente);
        }

        // 6. Sistema Biblioteca

        ArrayList<Livro> livros = new ArrayList<>();

        int opcaoBiblioteca;

        do {

            System.out.println("\nBiblioteca");
            System.out.println("1 - Cadastrar livro");
            System.out.println("2 - Listar livros");
            System.out.println("3 - Emprestar livro");
            System.out.println("4 - Devolver livro");
            System.out.println("0 - Sair");

            opcaoBiblioteca = sc.nextInt();

            switch (opcaoBiblioteca) {

                case 1:

                    System.out.print("Código: ");
                    int codigo = sc.nextInt();
                    sc.nextLine();

                    System.out.print("Título: ");
                    String titulo = sc.nextLine();

                    System.out.print("Autor: ");
                    String autor = sc.nextLine();

                    livros.add(new Livro(codigo, titulo, autor));

                    System.out.println("Livro cadastrado!");
                    break;

                case 2:

                    for (Livro livro : livros) {
                        livro.exibir();
                    }

                    break;

                case 3:

                    System.out.print("Código do livro: ");
                    int codEmprestimo = sc.nextInt();

                    for (Livro livro : livros) {

                        if (livro.codigo == codEmprestimo) {

                            if (livro.disponivel) {
                                livro.disponivel = false;
                                System.out.println("Livro emprestado!");
                            } else {
                                System.out.println("Livro indisponível.");
                            }
                        }
                    }

                    break;

                case 4:

                    System.out.print("Código do livro: ");
                    int codDevolucao = sc.nextInt();

                    for (Livro livro : livros) {

                        if (livro.codigo == codDevolucao) {
                            livro.disponivel = true;
                            System.out.println("Livro devolvido!");
                        }
                    }

                    break;

                case 0:
                    System.out.println("Saindo da biblioteca...");
                    break;

                default:
                    System.out.println("Opção inválida.");
            }

        } while (opcaoBiblioteca != 0);

        // 7. Sistema Lanchonete

        ArrayList<Pedido> pedidos = new ArrayList<>();

        int opcaoLanchonete;

        do {

            System.out.println("\nLanchonete");
            System.out.println("1 - Cadastrar pedido");
            System.out.println("2 - Listar pedidos");
            System.out.println("3 - Atualizar status");
            System.out.println("4 - Buscar pedido");
            System.out.println("5 - Valor total");
            System.out.println("0 - Sair");

            opcaoLanchonete = sc.nextInt();

            switch (opcaoLanchonete) {

                case 1:

                    System.out.print("Número do pedido: ");
                    int numero = sc.nextInt();
                    sc.nextLine();

                    System.out.print("Nome do cliente: ");
                    String cliente = sc.nextLine();

                    System.out.print("Item pedido: ");
                    String item = sc.nextLine();

                    System.out.print("Valor: ");
                    double valor = sc.nextDouble();

                    pedidos.add(new Pedido(numero, cliente, item, valor));

                    System.out.println("Pedido cadastrado!");
                    break;

                case 2:

                    for (Pedido pedido : pedidos) {
                        pedido.exibir();
                    }

                    break;

                case 3:

                    System.out.print("Número do pedido: ");
                    int numeroBusca = sc.nextInt();
                    sc.nextLine();

                    for (Pedido pedido : pedidos) {

                        if (pedido.numero == numeroBusca) {

                            System.out.println("Novo status:");
                            System.out.println("Pendente");
                            System.out.println("Preparando");
                            System.out.println("Finalizado");

                            pedido.status = sc.nextLine();

                            System.out.println("Status atualizado!");
                        }
                    }

                    break;

                case 4:

                    System.out.print("Número do pedido: ");
                    int busca = sc.nextInt();

                    for (Pedido pedido : pedidos) {

                        if (pedido.numero == busca) {
                            pedido.exibir();
                        }
                    }

                    break;

                case 5:

                    double total = 0;

                    for (Pedido pedido : pedidos) {
                        total += pedido.valor;
                    }

                    System.out.println("Valor total: R$ " + total);

                    break;

                case 0:
                    System.out.println("Saindo da lanchonete...");
                    break;

                default:
                    System.out.println("Opção inválida.");
            }

        } while (opcaoLanchonete != 0);

        sc.close();
    }
}

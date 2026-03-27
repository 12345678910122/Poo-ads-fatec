# Questão 1

```java
import java.time.LocalDateTime;
import java.time.format.DateTimeFormatter;

class Medico {
    private int id;
    private String nome;
    private String especialidade;

    public Medico(int id, String nome, String especialidade) {
        this.id = id;
        this.nome = nome;
        this.especialidade = especialidade;
    }

    public String getNome() { return nome; }
    public String getEspecialidade() { return especialidade; }
}

class Paciente {
    private int id;
    private String nome;
    private String cpf;

    public Paciente(int id, String nome, String cpf) {
        this.id = id;
        this.nome = nome;
        this.cpf = cpf;
    }

    public String getNome() { return nome; }
}

class Consulta {
    private LocalDateTime data;
    private double valorDaConsulta;
    private Medico medico;
    private Paciente paciente;

    public Consulta(LocalDateTime data, double valorDaConsulta, Medico medico, Paciente paciente) {
        this.data = data;
        this.valorDaConsulta = valorDaConsulta;
        this.medico = medico;
        this.paciente = paciente;
    }

    @Override
    public String toString() {
        DateTimeFormatter formatter = DateTimeFormatter.ofPattern("dd/MM/yyyy HH:mm");
        return "Consulta: [Data: " + data.format(formatter) + 
               ", Valor: R$" + valorDaConsulta + 
               ", Médico: " + medico.getNome() + " (" + medico.getEspecialidade() + ")" +
               ", Paciente: " + paciente.getNome() + "]";
    }
}

public class Exercicio1 {
    public static void main(String[] args) {
        Medico medico = new Medico(1, "Dr. Silva", "Cardiologia");
        Paciente paciente = new Paciente(101, "João Souza", "123.456.789-00");

        // Registro de consulta para 20/05/2026 às 14:00
        LocalDateTime dataConsulta = LocalDateTime.of(2026, 5, 20, 14, 0);
        Consulta consulta = new Consulta(dataConsulta, 250.0, medico, paciente);

        System.out.println(consulta);
    }
}
```

# Questão 2

```java
import java.time.LocalDate;
import java.time.format.DateTimeFormatter;

class Leitor {
    private int id;
    private String nome;

    public Leitor(int id, String nome) {
        this.id = id;
        this.nome = nome;
    }

    public String getNome() { return nome; }
}

class Livro {
    private int id;
    private String titulo;
    private String autor;

    public Livro(int id, String titulo, String autor) {
        this.id = id;
        this.titulo = titulo;
        this.autor = autor;
    }

    public String getTitulo() { return titulo; }
}

class Emprestimo {
    private LocalDate dataEmprestimo;
    private LocalDate dataDevolucaoPrevista;
    private Leitor leitor;
    private Livro livro;

    public Emprestimo(LocalDate dataEmprestimo, LocalDate dataDevolucaoPrevista, Leitor leitor, Livro livro) {
        this.dataEmprestimo = dataEmprestimo;
        this.dataDevolucaoPrevista = dataDevolucaoPrevista;
        this.leitor = leitor;
        this.livro = livro;
    }

    @Override
    public String toString() {
        DateTimeFormatter formatter = DateTimeFormatter.ofPattern("dd/MM/yyyy");
        return "Empréstimo: [Leitor: " + leitor.getNome() + 
               ", Livro: " + livro.getTitulo() + 
               ", Data Empréstimo: " + dataEmprestimo.format(formatter) + 
               ", Devolução Prevista: " + dataDevolucaoPrevista.format(formatter) + "]";
    }
}

public class Exercicio2 {
    public static void main(String[] args) {
        Leitor leitor = new Leitor(1, "Maria Oliveira");
        Livro livro = new Livro(10, "Dom Casmurro", "Machado de Assis");

        LocalDate hoje = LocalDate.now();
        LocalDate devolucao = hoje.plusDays(14);

        Emprestimo emprestimo = new Emprestimo(hoje, devolucao, leitor, livro);

        System.out.println(emprestimo);
    }
}
```

# Questão 3

```java
import java.util.ArrayList;

class Atleta {
    private int id;
    private String nome;
    private String posicao;

    public Atleta(int id, String nome, String posicao) {
        this.id = id;
        this.nome = nome;
        this.posicao = posicao;
    }

    public String getNome() { return nome; }
}

class Time {
    private int id;
    private String nome;
    private String tecnico;
    private ArrayList<Atleta> atletas;

    public Time(int id, String nome, String tecnico) {
        this.id = id;
        this.nome = nome;
        this.tecnico = tecnico;
        this.atletas = new ArrayList<>();
    }

    public void contratarAtleta(Atleta a) {
        this.atletas.add(a);
    }

    public String getNome() { return nome; }
}

public class Exercicio3 {
    public static void main(String[] args) {
        Atleta a1 = new Atleta(1, "Lucas Dias", "Ala-Pivô");
        Time t1 = new Time(10, "Franca Basquete", "Helinho Garcia");

        t1.contratarAtleta(a1);

        System.out.println("Time: " + t1.getNome());
        System.out.println("Atleta contratado: " + a1.getNome());

        // Prova de Agregação: Se o objeto Time for anulado, o objeto Atleta continua existindo.
        t1 = null;
        System.out.println("O objeto Time foi anulado.");
        System.out.println("O atleta " + a1.getNome() + " ainda existe na memória.");
    }
}
```

# Questão 4

```java
import java.util.ArrayList;

class Programador {
    private int id;
    private String nome;
    private String linguagemPrincipal;

    public Programador(int id, String nome, String linguagemPrincipal) {
        this.id = id;
        this.nome = nome;
        this.linguagemPrincipal = linguagemPrincipal;
    }

    public String getNome() { return nome; }
    public String getLinguagemPrincipal() { return linguagemPrincipal; }
}

class Projeto {
    private int id;
    private String nomeProjeto;
    private ArrayList<Programador> programadores;

    public Projeto(int id, String nomeProjeto) {
        this.id = id;
        this.nomeProjeto = nomeProjeto;
        this.programadores = new ArrayList<>();
    }

    public void adicionarProgramador(Programador p) {
        this.programadores.add(p);
    }

    public void listarProgramadores() {
        System.out.println("Programadores no projeto " + nomeProjeto + ":");
        for (Programador p : programadores) {
            System.out.println("- " + p.getNome() + " (" + p.getLinguagemPrincipal() + ")");
        }
    }
}

public class Exercicio4 {
    public static void main(String[] args) {
        Programador p1 = new Programador(1, "Alice", "Java");
        Programador p2 = new Programador(2, "Bob", "Python");
        Programador p3 = new Programador(3, "Charlie", "TypeScript");

        Projeto proj = new Projeto(101, "Sistema de Gestão");

        proj.adicionarProgramador(p1);
        proj.adicionarProgramador(p2);
        proj.adicionarProgramador(p3);

        proj.listarProgramadores();
    }
}
```

# Questão 5

```java
class Processador {
    private String marca;
    private String modelo;
    private double frequencia;

    public Processador(String marca, String modelo, double frequencia) {
        this.marca = marca;
        this.modelo = modelo;
        this.frequencia = frequencia;
    }

    @Override
    public String toString() {
        return marca + " " + modelo + " (" + frequencia + " GHz)";
    }
}

class Computador {
    private int id;
    private String marca;
    private Processador processador;

    public Computador(int id, String marca, String procMarca, String procModelo, double procFreq) {
        this.id = id;
        this.marca = marca;
        // Composição: O processador é instanciado dentro do construtor do Computador
        this.processador = new Processador(procMarca, procModelo, procFreq);
    }

    public void mostrarConfiguracao() {
        System.out.println("Computador " + marca + " (ID: " + id + ")");
        System.out.println("Processador: " + processador);
    }
}

public class Exercicio5 {
    public static void main(String[] args) {
        Computador pc = new Computador(1, "Dell", "Intel", "Core i7", 3.6);
        pc.mostrarConfiguracao();

        // Prova de Composição: Se o computador for deletado (anulado), o processador também deixa de ser acessível.
        pc = null;
        System.out.println("O objeto Computador foi anulado. O processador não existe mais de forma independente.");
    }
}
```

# Questão 6

```java
import java.util.ArrayList;

class Apartamento {
    private int numero;
    private int andar;

    public Apartamento(int numero, int andar) {
        this.numero = numero;
        this.andar = andar;
    }

    @Override
    public String toString() {
        return "Apartamento " + numero + " (Andar: " + andar + ")";
    }
}

class Edificio {
    private String nome;
    private String endereco;
    private ArrayList<Apartamento> apartamentos;

    public Edificio(String nome, String endereco) {
        this.nome = nome;
        this.endereco = endereco;
        this.apartamentos = new ArrayList<>();
    }

    public void construirApartamento(int num, int andar) {
        // Composição: O objeto Apartamento é criado dentro do Edifício
        Apartamento ap = new Apartamento(num, andar);
        this.apartamentos.add(ap);
    }

    public void listarApartamentos() {
        System.out.println("Edifício: " + nome + " (" + endereco + ")");
        for (Apartamento ap : apartamentos) {
            System.out.println("- " + ap);
        }
    }
}

public class Exercicio6 {
    public static void main(String[] args) {
        Edificio ed = new Edificio("Residencial Horizonte", "Rua das Flores, 123");

        ed.construirApartamento(101, 1);
        ed.construirApartamento(202, 2);
        ed.construirApartamento(303, 3);

        ed.listarApartamentos();
    }
}
```

# Questão 7

```java
import java.util.ArrayList;

class Produto {
    private int id;
    private String nome;
    private double preco;

    public Produto(int id, String nome, double preco) {
        this.id = id;
        this.nome = nome;
        this.preco = preco;
    }

    public String getNome() { return nome; }
    public double getPreco() { return preco; }
}

class Cliente {
    private int id;
    private String nome;

    public Cliente(int id, String nome) {
        this.id = id;
        this.nome = nome;
    }

    public String getNome() { return nome; }
}

class ItemVenda {
    private int id;
    private int quantidade;
    private Produto produto; // Agregação: O produto existe independente do item de venda

    public ItemVenda(int id, int quantidade, Produto produto) {
        this.id = id;
        this.quantidade = quantidade;
        this.produto = produto;
    }

    public double calcularSubtotal() {
        return quantidade * produto.getPreco();
    }

    @Override
    public String toString() {
        return "- " + produto.getNome() + " | Qtd: " + quantidade + " | Subtotal: R$" + calcularSubtotal();
    }
}

class Venda {
    private Cliente cliente; // Agregação: O cliente existe independente da venda
    private ArrayList<ItemVenda> itens; // Composição: Itens de venda só existem dentro da venda

    public Venda(Cliente cliente) {
        this.cliente = cliente;
        this.itens = new ArrayList<>();
    }

    public void adicionarItem(int id, int quantidade, Produto produto) {
        // Composição: O objeto ItemVenda é criado dentro da Venda
        ItemVenda item = new ItemVenda(id, quantidade, produto);
        this.itens.add(item);
    }

    public double calcularTotal() {
        double total = 0;
        for (ItemVenda item : itens) {
            total += item.calcularSubtotal();
        }
        return total;
    }

    public void imprimirVenda() {
        System.out.println("Venda para o cliente: " + cliente.getNome());
        System.out.println("Itens:");
        for (ItemVenda item : itens) {
            System.out.println(item);
        }
        System.out.println("Total da Venda: R$" + calcularTotal());
    }
}

public class Exercicio7 {
    public static void main(String[] args) {
        // Agregação: Produtos existem independentemente
        Produto p1 = new Produto(1, "Arroz 5kg", 25.50);
        Produto p2 = new Produto(2, "Feijão 1kg", 8.90);
        Produto p3 = new Produto(3, "Azeite", 32.00);

        // Agregação: Cliente existe independentemente
        Cliente c1 = new Cliente(10, "Carlos Silva");

        // Composição: Venda gerencia seus itens
        Venda venda = new Venda(c1);
        venda.adicionarItem(1, 2, p1);
        venda.adicionarItem(2, 3, p2);
        venda.adicionarItem(3, 1, p3);

        venda.imprimirVenda();
    }
}
```

# Questão 8

```java
import java.time.LocalDateTime;
import java.time.format.DateTimeFormatter;
import java.util.ArrayList;

class Filme {
    private int id;
    private String titulo;
    private String genero;
    private int duracao;

    public Filme(int id, String titulo, String genero, int duracao) {
        this.id = id;
        this.titulo = titulo;
        this.genero = genero;
        this.duracao = duracao;
    }

    public String getTitulo() { return titulo; }
    public String getGenero() { return genero; }
    public int getDuracao() { return duracao; }

    @Override
    public String toString() {
        return "Filme: " + titulo + " (" + genero + ", " + duracao + " min)";
    }
}

class Ingresso {
    private int id;
    private String assento;
    private String tipo;
    private float preco;

    public Ingresso(int id, String assento, String tipo, float preco) {
        this.id = id;
        this.assento = assento;
        this.tipo = tipo;
        this.preco = preco;
    }

    @Override
    public String toString() {
        return "Ingresso [ID: " + id + ", Assento: " + assento + ", Tipo: " + tipo + ", Preço: R$" + preco + "]";
    }
}

class Sessao {
    private int id;
    private LocalDateTime horario;
    private int sala;
    private Filme filme; // Agregação
    private ArrayList<Ingresso> ingressos; // Composição

    public Sessao(int id, LocalDateTime horario, int sala) {
        this.id = id;
        this.horario = horario;
        this.sala = sala;
        this.ingressos = new ArrayList<>();
    }

    public void vincularFilme(Filme f) {
        this.filme = f;
    }

    public void venderIngresso(int id, String assento, String tipo, float preco) {
        // Composição: O objeto Ingresso é criado dentro da Sessão
        Ingresso ing = new Ingresso(id, assento, tipo, preco);
        this.ingressos.add(ing);
    }

    @Override
    public String toString() {
        DateTimeFormatter formatter = DateTimeFormatter.ofPattern("dd/MM/yyyy HH:mm");
        StringBuilder sb = new StringBuilder();
        sb.append("Sessão ID: ").append(id).append("\n");
        sb.append("Horário: ").append(horario.format(formatter)).append("\n");
        sb.append("Sala: ").append(sala).append("\n");
        sb.append("Filme: ").append(filme != null ? filme.getTitulo() : "Nenhum filme vinculado").append("\n");
        sb.append("Ingressos Vendidos:\n");
        for (Ingresso ing : ingressos) {
            sb.append("  - ").append(ing).append("\n");
        }
        return sb.toString();
    }
}

public class Exercicio8 {
    public static void main(String[] args) {
        // 1. Instancie 2 objetos Filme
        Filme f1 = new Filme(1, "Batman", "Ação", 176);
        Filme f2 = new Filme(2, "Duna", "Ficção Científica", 155);

        // 2. Instancie uma Sessao para a Sala 01
        LocalDateTime dataSessao = LocalDateTime.of(2026, 7, 20, 20, 0);
        Sessao sessao = new Sessao(101, dataSessao, 1);

        // 3. Agregação: Vincule o filme "Batman"
        sessao.vincularFilme(f1);

        // 4. Composição: Simule a venda de 3 ingressos
        sessao.venderIngresso(1, "A1", "Inteira", 40.0f);
        sessao.venderIngresso(2, "A2", "Meia", 20.0f);
        sessao.venderIngresso(3, "A3", "Inteira", 40.0f);

        // 5. Imprima os dados da Sessão
        System.out.println(sessao);
    }
}
```


# Polimorfismoeclassesabstratas

# Exercício 1: Formas Geométricas Abstratas


// Classe abstrata FormaGeometrica
abstract class FormaGeometrica {
    // Método abstrato para calcular a área
    public abstract double calcularArea();
    
    // Método para exibir a área da forma
    public void exibirArea() {
        System.out.println("A área é: " + calcularArea());
    }
}

// Classe Círculo que estende FormaGeometrica
class Circulo extends FormaGeometrica {
    private double raio;
    
    public Circulo(double raio) {
        this.raio = raio;
    }
    
    @Override
    public double calcularArea() {
        return Math.PI * raio * raio;
    }
}

// Classe Retângulo que estende FormaGeometrica
class Retangulo extends FormaGeometrica {
    private double largura;
    private double altura;
    
    public Retangulo(double largura, double altura) {
        this.largura = largura;
        this.altura = altura;
    }
    
    @Override
    public double calcularArea() {
        return largura * altura;
    }
}

// Classe Triângulo que estende FormaGeometrica
class Triangulo extends FormaGeometrica {
    private double base;
    private double altura;
    
    public Triangulo(double base, double altura) {
        this.base = base;
        this.altura = altura;
    }
    
    @Override
    public double calcularArea() {
        return (base * altura) / 2.0;
    }
}

// Classe principal para executar o programa
public class FormaGeometricaMain {
    public static void main(String[] args) {
        // Criando instâncias das formas geométricas
        FormaGeometrica circulo = new Circulo(5);
        FormaGeometrica retangulo = new Retangulo(4, 6);
        FormaGeometrica triangulo = new Triangulo(3, 7);
        
        // Exibindo a área de cada forma geométrica
        System.out.println("Área do círculo:");
        circulo.exibirArea();
        
        System.out.println("Área do retângulo:");
        retangulo.exibirArea();
        
        System.out.println("Área do triângulo:");
        triangulo.exibirArea();
    }
}


# Exercício 2: Sistema de Gerenciamento de Animais

import java.util.ArrayList;
import java.util.List;

// Classe abstrata Animal
abstract class Animal {
    // Método abstrato para emitir som
    public abstract void emitirSom();
    
    // Método abstrato para mover
    public abstract void mover();
}

// Classe Cachorro que estende Animal
class Cachorro extends Animal {
    @Override
    public void emitirSom() {
        System.out.println("O cachorro faz: Au au!");
    }
    
    @Override
    public void mover() {
        System.out.println("O cachorro está correndo.");
    }
}

// Classe Gato que estende Animal
class Gato extends Animal {
    @Override
    public void emitirSom() {
        System.out.println("O gato faz: Miau!");
    }
    
    @Override
    public void mover() {
        System.out.println("O gato está andando suavemente.");
    }
}

// Classe Passaro que estende Animal
class Passaro extends Animal {
    @Override
    public void emitirSom() {
        System.out.println("O pássaro faz: Piu piu!");
    }
    
    @Override
    public void mover() {
        System.out.println("O pássaro está voando.");
    }
}

// Classe principal para executar o programa
public class AnimalMain {
    public static void main(String[] args) {
        // Criando uma lista de animais
        List<Animal> animais = new ArrayList<>();
        
        // Adicionando instâncias de diferentes tipos de animais à lista
        animais.add(new Cachorro());
        animais.add(new Gato());
        animais.add(new Passaro());
        
        // Iterando sobre a lista e chamando os métodos emitirSom() e mover()
        for (Animal animal : animais) {
            animal.emitirSom();
            animal.mover();
            System.out.println(); // Linha em branco para separar a saída
        }
    }
}


# Exercício 3: Banco com Contas Bancárias

// Classe abstrata ContaBancaria
abstract class ContaBancaria {
    protected double saldo;
    
    // Construtor para inicializar o saldo
    public ContaBancaria(double saldoInicial) {
        this.saldo = saldoInicial;
    }

    // Método abstrato para sacar dinheiro
    public abstract void sacar(double valor);
    
    // Método abstrato para depositar dinheiro
    public abstract void depositar(double valor);
    
    // Método para mostrar o saldo
    public void mostrarSaldo() {
        System.out.println("Saldo atual: R$ " + saldo);
    }
}

// Classe ContaCorrente que estende ContaBancaria
class ContaCorrente extends ContaBancaria {
    private static final double TAXA_SAQUE = 1.00; // Taxa fixa de saque
    
    public ContaCorrente(double saldoInicial) {
        super(saldoInicial);
    }
    
    @Override
    public void sacar(double valor) {
        if (valor + TAXA_SAQUE <= saldo) {
            saldo -= (valor + TAXA_SAQUE);
            System.out.println("Saque realizado: R$ " + valor);
        } else {
            System.out.println("Saldo insuficiente para saque.");
        }
    }
    
    @Override
    public void depositar(double valor) {
        saldo += valor;
        System.out.println("Depósito realizado: R$ " + valor);
    }
}

// Classe ContaPoupanca que estende ContaBancaria
class ContaPoupanca extends ContaBancaria {
    private static final double JUROS_ANUAIS = 0.05; // 5% de juros anuais
    
    public ContaPoupanca(double saldoInicial) {
        super(saldoInicial);
    }
    
    @Override
    public void sacar(double valor) {
        if (valor <= saldo) {
            saldo -= valor;
            System.out.println("Saque realizado: R$ " + valor);
        } else {
            System.out.println("Saldo insuficiente para saque.");
        }
    }
    
    @Override
    public void depositar(double valor) {
        saldo += valor;
        System.out.println("Depósito realizado: R$ " + valor);
    }
    
    // Método para aplicar juros
    public void aplicarJuros() {
        saldo += saldo * JUROS_ANUAIS;
        System.out.println("Juros aplicados.");
    }
}

// Classe principal para executar o programa
public class ContaBancariaMain {
    public static void main(String[] args) {
        // Criando instâncias das contas bancárias
        ContaBancaria contaCorrente = new ContaCorrente(1000);
        ContaBancaria contaPoupanca = new ContaPoupanca(1000);
        
        // Realizando operações nas contas correntes
        System.out.println("Operações na Conta Corrente:");
        contaCorrente.depositar(200);
        contaCorrente.sacar(150);
        contaCorrente.mostrarSaldo();
        System.out.println(); // Linha em branco para separar a saída
        
        // Realizando operações nas contas poupança
        System.out.println("Operações na Conta Poupança:");
        contaPoupanca.depositar(300);
        contaPoupanca.sacar(100);
        ((ContaPoupanca) contaPoupanca).aplicarJuros(); // Casting para acessar o método específico
        contaPoupanca.mostrarSaldo();
    }
}


# Exercício 4: Sistema de Pagamento


// Classe abstrata Pagamento
abstract class Pagamento {
    protected double valor;
    
    // Construtor para inicializar o valor
    public Pagamento(double valor) {
        this.valor = valor;
    }
    
    // Método abstrato para calcular o valor
    public abstract double calcularValor();
    
    // Método para mostrar o valor final do pagamento
    public void mostrarValor() {
        System.out.println("Valor do pagamento: R$ " + calcularValor());
    }
}

// Classe PagamentoCartaoCredito que estende Pagamento
class PagamentoCartaoCredito extends Pagamento {
    private static final double TAXA_CARTAO = 0.03; // Taxa de 3% para cartão de crédito
    
    public PagamentoCartaoCredito(double valor) {
        super(valor);
    }
    
    @Override
    public double calcularValor() {
        return valor + (valor * TAXA_CARTAO);
    }
}

// Classe PagamentoBoleto que estende Pagamento
class PagamentoBoleto extends Pagamento {
    private static final double DESCONTO_BOLETO = 0.05; // Desconto de 5% para boleto
    
    public PagamentoBoleto(double valor) {
        super(valor);
    }
    
    @Override
    public double calcularValor() {
        return valor - (valor * DESCONTO_BOLETO);
    }
}

// Classe principal para executar o programa
public class PagamentoMain {
    public static void main(String[] args) {
        // Criando instâncias dos métodos de pagamento
        Pagamento pagamentoCartao = new PagamentoCartaoCredito(1000);
        Pagamento pagamentoBoleto = new PagamentoBoleto(1000);
        
        // Calculando e exibindo os valores dos pagamentos
        System.out.println("Valor com Cartão de Crédito:");
        pagamentoCartao.mostrarValor();
        System.out.println(); // Linha em branco para separar a saída
        
        System.out.println("Valor com Boleto:");
        pagamentoBoleto.mostrarValor();
    }
}


# Exercício 5: Sistema de Funcionários

// Classe abstrata Funcionario
abstract class Funcionario {
    protected String nome;
    protected double salarioBase;
    
    // Construtor para inicializar o nome e o salário base
    public Funcionario(String nome, double salarioBase) {
        this.nome = nome;
        this.salarioBase = salarioBase;
    }
    
    // Método abstrato para calcular o salário
    public abstract double calcularSalario();
    
    // Método para exibir o nome e o salário
    public void exibirSalario() {
        System.out.println("Nome: " + nome);
        System.out.println("Salário: R$ " + calcularSalario());
    }
}

// Classe Gerente que estende Funcionario
class Gerente extends Funcionario {
    private static final double BONUS = 1500; // Bônus fixo para o gerente
    
    public Gerente(String nome, double salarioBase) {
        super(nome, salarioBase);
    }
    
    @Override
    public double calcularSalario() {
        return salarioBase + BONUS;
    }
}

// Classe Programador que estende Funcionario
class Programador extends Funcionario {
    private static final double BONUS_PROJETOS = 500; // Bônus por projetos concluídos
    
    public Programador(String nome, double salarioBase) {
        super(nome, salarioBase);
    }
    
    @Override
    public double calcularSalario() {
        return salarioBase + BONUS_PROJETOS;
    }
}

// Classe principal para executar o programa
public class FuncionarioMain {
    public static void main(String[] args) {
        // Criando instâncias de diferentes tipos de funcionários
        Funcionario gerente = new Gerente("Ana", 5000);
        Funcionario programador = new Programador("Carlos", 4000);
        
        // Calculando e exibindo os salários dos funcionários
        System.out.println("Salário do Gerente:");
        gerente.exibirSalario();
        System.out.println(); // Linha em branco para separar a saída
        
        System.out.println("Salário do Programador:");
        programador.exibirSalario();
    }
}




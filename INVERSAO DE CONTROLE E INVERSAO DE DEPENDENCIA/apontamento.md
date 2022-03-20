# Como funciona a Injeção de Dependências no Spring

**O que é Injeção de Dependência?**
Injeção de Dependência é um padrão de projeto que ajuda muito a deixar o código desacoplado, melhora a legibilidade e interpretação do código, melhora 
a distribuição de responsabilidades entre as classes e facilita a manutenção do código.

É uma forma de aplicar inversão de controle em uma classe que utiliza funcionalidades de outras classes, tirando a responsabilidade dela de instanciar 
ou buscar objetos dessas outras classes das quais ela depende.

Então o objetivo é não instanciar objetos que realizam funções que podem futuramente ser alteradas dentro de uma classe e sim deixar a responsabilidade
dessa instanciação para quem chama a classe.


**Um exemplo com Java**

Imagine que temos uma classe de serviço chamada PrecificacaoService e essa classe tem um método calcularPreco que recebe um Produto.

Esse método faz um cálculo que é igual para todos os produtos baseado nas características e no custo de produção e retorna o preço final do produto para venda,
com adição de impostos de acordo com um cálculo específico da classe CalculadoraImpostoSimplesNacional.

Veja uma forma bem simplória da classe:

public class PrecificacaoService {
 
    private CalculadoraImpostoSimplesNacional calculadoraImposto = new CalculadoraImpostoSimplesNacional();
 
    public BigDecimal calcularPreco(Produto produto) {
        // faz outros cálculos de preço
        return this.calculadoraImposto.calcular(produto);
    }
 
}

Neste exemplo eu coloquei uma dependência da classe CalculadoraImpostoSimplesNacional diretamente dentro da classe PrecificacaoService, colocando nela 
a responsabilidade de instanciar e utilizar essa classe de dependência.

Isso é um problema e já vimos que a ideia é tirar a responsabilidade das classes de instanciar seus objetos de dependência.

Para resolver essa questão, poderíamos passar uma instância da classe CalculadoraImpostoSimplesNacional diretamente no construtor de PrecificacaoService.

Mas, ainda assim, estaríamos presos ao tipo de cálculo de impostos para empresas do Simples Nacional, podendo usar somente o CalculadoraImpostoSimplesNacional.

E se no futuro a gente precisasse calcular impostos para empresas com um outro enquadramento, como Lucro Presumido, ficaria bem difícil fazer essa substituição.

Por isso, o ideal nesse caso seria criar uma interface CalculadoraImposto, que declara o método abstrato calcular para ser implementado.

public interface CalculadoraImposto {
 
    BigDecimal calcular(Produto produto);
 
}

E aí é só substituir a dependência na classe PrecificacaoService para essa interface:

public class PrecificacaoService {
 
    private CalculadoraImposto calculadoraImposto;
 
    public PrecificacaoService(CalculadoraImposto calculadoraImposto) {
        this.calculadoraImposto = calculadoraImposto;
    }
 
    public BigDecimal calcularPreco(Produto produto) {
        // faz outros cálculos de preço
        return this.calculadoraImposto.calcular(produto);
    }
 
}

Veja que agora a classe PrecificacaoService não depende mais de nenhuma implementação de calculadora de imposto, mas de uma abstração de uma calculadora (interface).

Dessa forma, nós podemos implementar novas calculadoras de impostos sempre que necessário, sem que isso afete o funcionamento de PrecificacaoService.

Essa é uma forma de aplicar a injeção de dependências com Java manualmente.


## Como o Spring lida com a injeção de dependências

O Spring Framework implementa injeção de dependências através de um container chamado Spring IoC Container.

Este container é o responsável por gerenciar todas as dependências do projeto de forma automática.

Os objetos gerenciados pelo container do Spring são chamados de Beans. Uma aplicação rodando pode ter vários beans ativos e gerenciados pelo Spring.

Esses beans são os mesmos objetos que nós utilizamos no projeto normalmente, a única diferença é que eles são gerenciados pelo IoC Container.

Existem várias formas de declarar um bean do Spring. A mais conhecida é anotando a classe com @Component.

Outras anotações semânticas podem ser usadas também, como por exemplo @Controller, @Service, @Repository, etc.

Os beans gerenciados pelo Spring são instanciados automaticamente pelo IoC Container e todas as dependências são resolvidas e repassadas pelo próprio framework.

A classe a seguir está declarada como um componente Spring (um bean), portanto é gerenciada pelo IoC Container:

@Component
public class PrecificacaoService {
 
    private CalculadoraImposto calculadoraImposto;
 
    public PrecificacaoService(CalculadoraImposto calculadoraImposto) {
        this.calculadoraImposto = calculadoraImposto;
    }
 
    public BigDecimal calcularPreco(Produto produto) {
        return this.calculadoraImposto.calcular(produto);
    }
 
}

A ideia principal é injetar beans em outros beans, ou seja, eu só posso injetar um objeto em outro objeto se eles forem gerenciados pelo Spring.

Então no caso do nosso exemplo, ficaria assim:


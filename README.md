# O QUE É POO?

É um paradigma de programação, corresponde a uma técnica de programação para um fim especifico.

Dentro desta técnica existem quatro pilares:

- Abstração
- Encapsulamento
- Herança
- Polimorfismo

O principal conceito da POO são classes e objetos.

## PARADIGMA DE PROGRAMAÇÃO
Nada mais é do que um modelo de técnicas e estruturas e formas de solucionar um problema.

Paradigma de programação é diferente de linguagem de programação.

Uma linguagem de programação implementa um ou mais paradigmas.

### Paradigmas
- programação orientada a objetos
- programação estruturada
- programação imperativa
- programação procedural
- programação orientada a eventos
- programação lógica

# ABSTRAÇÃO
Abstrair um objeto do mundo real para um contexto especifico considerando apenas os atributos importantes.

Vai representar na classe apenas o que o seu contexto necessita.

Como exemplo posso representar pessoa tanto na escola, como na barbearia, mas não preciso pedir a serie da pessoa na barbearia. 
> Deve usar características que fazem sentido no contexto, trabalhar sempre na simplicidade

# ENCAPSULAMENTO

Serve para proteger uma classe e definir limites para alterações de suas propriedades.
> Definir que uma classe ou um atributo esteja bloqueado para alterações externa e só você (a própria classe em si) pode alterar aquela propriedade ou atributo.

Serve para ocultar seu comportamento e expor somente o necessário.

### Exemplo:
```
Conta corrente
tem

+ numero
- saldo 

pode 

sacar
```
O saldo não pode ser alterado a qualquer hora, somente se chamar a função sacar.


# HERANÇA
Nos permite reutilizar atributos, métodos e comportamentos de uma classe em outras classes.

Serve para agrupar objetos que são do mesmo tipo, porem com características diferentes.

```

namespace ProgramacaoOrientadaObjeto.Models
{
    public class Aluno : Pessoa // isso é uma herança
    {
         public double Nota { get; set; }
    }
}

```

# POLIMORFISMO
Vem do grego "muitas formas".

Podemos sobrescrever métodos das classes filhas para que se comportem de maneira diferente e ter sua própria implementação.

### Overload - Polimorfismo em tempo de compilação
Polimorfismo que não depende de herança.
O qual tem métodos com nomes iguais e tipos de retornos iguais, porem com números de parâmetros diferentes, dependendo de quantos números passar cairá em determinado método.

```

public class Calculadora
{
    public int Somar(int num1, int num2)
    {
        return num1 + num2;
    }
    public int Somar(int num1, int num2, int num3)
    {
        return num1 + num2 + num3;
    }
}

```


### Override - Polimorfismo em tempo de execução
Na classe pai (no caso Pessoa) deve colocar o virtual na propriedade que possa ser alterada
```
 public virtual void Apresentar()
```

```
 public class Aluno : Pessoa
    {
         public double Nota { get; set; }
        public override void Apresentar()// polimorfismo, ira sobrescrever o Apresentar()
        {
            Console.WriteLine($"Olá, meu nome é {Nome}, tenho {Idade} anos, e sou um aluno nota {Nota}!");
        }
    }
```

# CLASSES ABSTRATAS E INTERFACES
### << abstract >>

Uma classe abstrata tem como objetivo ser exclusivamente um modelo para ser herdado, portanto não pode ser instanciada.

Você pode implementar métodos ou deixá-los a cargo de quem herdar.

Colocar abstract na classe ou método
```
...
public abstract class Conta
{   
    ...
    public abstract void Creditar(decimal valor);
    ...
```
O método da outra classe deve ser chamada, por conta do abstract
```
public class Corrente : Conta
{
    public override void Creditar(decimal valor)
    {...
```

# CLASSE SELADA

### << sealed >>
### (Dar um ponto final na classe.)

Tem como objetivo de impedir que outras classes façam uma herança dela, ou seja, nenhuma classe pode ser sua derivada.

Também existem métodos e propriedades seladas
```
...
public sealed class Professor : Pessoa
{...
```

## METODO SELADO

Do mesmo modo da classe, também podemos fazer com os métodos, não podendo ser sobrescritas pelas classes filhas.

```
... 
public sealed override void Apresentar()
{...
```

Daí qualquer outra classe não consegue acessar esse método.

## CLASSE OBJECT

A classe "System.Object" é a mãe de todas as classes na hierarquia do .NET.

Todas as classes derivam, direta ou indiretamente da classe _Object_, e ela tem como objetivo prover serviços de baixo nível para suas filhas.

Quando cria uma classe, ela já herda automaticamente sem que você implemente a classe Object com alguns métodos:

|MÉTODOS||
|--------------------------------|-------|
| Equals(Object)|                 Determina se o Objeto especificado é igual ao objeto atual.|
| Equals(Object, Object)|         Determina se as instâncias de objeto especificadas são consideradas iguais.|
| Finalize()|                     Permite que um objeto tente liberar recursos e executar outras operações de limpeza antes de ser recuperado pela coleta de lixo.|
| GetHashCode()|                  Serve como a função de hash padrão.|
| GetType()|                      Obtém o Type da instância atual.|
| MemberwiseClone()|              Cria uma cópia superficial do Object atual.|
| ReferenceEquals(Object,Object)| Determina se as instâncias de Object especificadas são a mesma instância.|
| ToString()|                     Retorna uma cadeia de caracteres que representa o objeto atual.|
---

#### As classes já vem com a herança da classe Object
```
public class Computador : Object
{
    public override string ToString()
    {
        return "Metodo ToString: 'base.ToString()'";
    }
}

```
**nomeClasse : Object* já vem indiretamente nas classes.
Aqui sobrescrevi o método ToString para exemplo.
```
Computador c = new Computador();
Console.WriteLine(c.ToString());
```

# Interfaces
### << interface >>
Uma interface é um contrato que pode ser implementado por uma classe.

É como se fosse uma classe abstrata, podendo definir métodos abstratos para serem implementados.

Assim como uma classe abstrata, uma interface não pode ser instanciada.

O nome da classe sempre começa com I, ex: ICalculadora

Diferente da das classes normais em que a "herança" não pode ser múltipla, uma classe pode "implementar" mais de uma interface.
Para implementar e herdar fazemos do mesmo modo: *public class nomeClasse : INomeInterface...*

Na pasta Interfaces, cria a interface de seu nome.

```
namespace ProgramacaoOrientadaObjeto.Interfaces
{
    public interface ICalculadora
    {
        int Somar(int num1, int num2);
        int Subtrair(int num1, int num2);
        int Multiplicar(int num1, int num2);
        int Dividir(int num1, int num2);
    }
}
```
A classe calculadora é obrigada a ter os métodos que a interface exige. 
```
public class Calculadora : ICalculadora
    {
        public int Dividir(int num1, int num2)
        {
            return num1 / num2;
        }

        public int Multiplicar(int num1, int num2)
        {
            return num1 * num2;
        }

        public int Somar(int num1, int num2) 
        {
            return num1 + num2;
        }
        public int Somar(int num1, int num2, int num3) 
        {
            return num1 + num2 + num3;
        }

        public int Subtrair(int num1, int num2)
        {
            return num1 - num2;
        }
    }
```

```
ICalculadora calc = new Calculadora();
Console.WriteLine(calc.Dividir(9,3));
```

## Método padrão

A partir do momento que colocou um corpo para seu método, então você deixa ele opcional para sua implementação.

```
public interface ICalculadora
{
    int Somar(int num1, int num2);
    int Subtrair(int num1, int num2);
    int Multiplicar(int num1, int num2);
    int Dividir(int num1, int num2)
    {
        return num1 / num2;
    }
}
``` 

Após isso, na classe em que implementar a ICalculadora, não sou obrigado a colocar o método dividir, pois a interface tem como fazê-lo, mas pode implementar e colocar do jeito que desejar.

```
public class Calculadora : ICalculadora
    {
        public int Multiplicar(int num1, int num2)
        {
            return num1 * num2;
        }

        public int Somar(int num1, int num2) 
        {
            return num1 + num2;
        }
        public int Somar(int num1, int num2, int num3) 
        {
            return num1 + num2 + num3;
        }

        public int Subtrair(int num1, int num2)
        {
            return num1 - num2;
        }
    }
```

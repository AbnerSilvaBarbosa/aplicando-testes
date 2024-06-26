# Aplicando Testes em C# - Semana 6:

## Objetivo do repositorio:

O objetivo deste repositório é demonstrar a aplicação de testes unitários em C# utilizando três frameworks populares: xUnit, NUnit e MSTest. O foco é testar uma classe de conversão de temperatura, garantindo a precisão da conversão de Fahrenheit para Celsius.

## Tecnologia utilizadas:

- C#
- .NET Core
- xUnit
- NUnit
- MSTest


### Abaixo está a classe para ser testada, de acordo com o artigo do auto estudo, com algumas modificações:

```csharp
namespace Temperatura
{
    public static class ConversorTemperaturaAbner
    {
        public static double FahrenheitParaCelsius(double temperatura)
        {
            return Math.Round((temperatura - 32) / 1.8, 2); 
        }
    }

    class Program
    {
        static void Main(string[] args)
        {
            Console.WriteLine("Digite a temperatura em Fahrenheit:");
            double fahrenheit = Convert.ToDouble(Console.ReadLine());
            double celsius = ConversorTemperaturaAbner.FahrenheitParaCelsius(fahrenheit);
            Console.WriteLine($"{fahrenheit}°F é equivalente a {celsius}°C.");
        }
    }
}

```
Neste código, uma classe estática chamada ConversorTemperaturaAbnerAbner possui um método estático FahrenheitToCelsius que converte a temperatura de Fahrenheit para Celsius e arredonda o resultado para duas casas decimais.  A classe Program contém um método Main que solicita ao usuário uma temperatura em Fahrenheit, usa o método FahrenheitToCelsius para converter a temperatura em Celsius e, em seguida, exibe o resultado convertido.

### Teste com XUnit:

No xUnit, a propriedade InlineData é usada em conjunto com a propriedade Theory. A teoria sugere que o método de teste é um teste paramétrico e deve ser executado várias vezes usando diferentes conjuntos de dados. InlineData é usado para definir esses conjuntos de dados. Cada uso de InlineData especifica um conjunto diferente de parâmetros que serão passados ​​para o método de teste.

```csharp
namespace Test.XUnit.Temperatura
{
    public class TestesConversorTemperaturaAbner
    {
        [Theory]
        [InlineData(32, 0)]
        [InlineData(47, 8.33)]
        [InlineData(86, 30)]
        [InlineData(90.5, 32.5)]
        [InlineData(120.18, 48.99)]
        [InlineData(212, 100)]
        public void TestarConversaoTemperatura(
            double fahrenheit, double celsius)
        {
            double valorCalculado =
                ConversorTemperaturaAbner.FahrenheitParaCelsius(fahrenheit);
            Assert.Equal(celsius, valorCalculado);
        }
    }
}
```

### Teste com NUnit:

No NUnit, TestCase é a propriedade equivalente ao InlineData do xUnit. Também é usado para definir conjuntos de dados para testes parametrizados, mas é um componente específico do NUnit. TestCase permite especificar valores de entrada e valores esperados diretamente na assinatura do método de teste.

```csharp
namespace Temperatura.Testes
{
    public class TestesConversorTemperaturaAbner
    {
        [TestCase(32, 0)]
        [TestCase(47, 8.33)]
        [TestCase(86, 30)]
        [TestCase(90.5, 32.5)]
        [TestCase(120.18, 48.99)]
        [TestCase(212, 100)]
        public void TesteConversaoTemperatura(
            double tempFahrenheit, double tempCelsius)
        {
            double valorCalculado =
                ConversorTemperaturaAbner.FahrenheitParaCelsius(tempFahrenheit);
            Assert.AreEqual(tempCelsius, valorCalculado);
        }
    }
}
```

### Teste com MSTest:

MSTest usa a propriedade DataRow com DataTestMethod para realizar testes parametrizados. DataRow fornece dados de entrada para cada iteração de teste. DataTestMethod indica que o método de teste é um teste orientado a dados e deve ser chamado uma vez para cada DataRow fornecido.

```csharp
namespace Temperatura.Testes
{
    [TestClass]
    public class TestesConversorTemperaturaAbner
    {
        [DataRow(32, 0)]
        [DataRow(47, 8.33)]
        [DataRow(86, 30)]
        [DataRow(90.5, 32.5)]
        [DataRow(120.18, 48.99)]
        [DataRow(212, 100)]
        [DataTestMethod]
        public void TesteConversaoTemperaturaAbner(
            double tempFahrenheit, double tempCelsius)
        {
            double valorCalculado =
                ConversorTemperaturaAbner.FahrenheitParaCelsius(tempFahrenheit);
            Assert.AreEqual(tempCelsius, valorCalculado);
        }
    }
}
```

### Testes executando na IDE:

Rodei pela extensão do Vscode para realizar os testes 

![todos testem passando](/Assets/TestRodando.png)

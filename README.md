# Visitor Example

Цей репозиторій містить приклад патерну проектування "Відвідувач".

## Патерн Відвідувач (Visitor)

Патерн "Відвідувач" дозволяє додати нові операції до об'єктів, не змінюючи самі об'єкти. Це корисно, коли ви хочете виконати деяку операцію над різними елементами об'єкта, які мають спільний інтерфейс.

### Приклад коду:

```csharp
using System;

// Інтерфейс відвідувача
public interface IVisitor
{
    void Visit(ElementA element);
    void Visit(ElementB element);
}

// Абстрактний клас елемента
public abstract class Element
{
    public abstract void Accept(IVisitor visitor);
}

// Конкретний клас елемента A
public class ElementA : Element
{
    public override void Accept(IVisitor visitor)
    {
        visitor.Visit(this);
    }

    public void OperationA()
    {
        Console.WriteLine("Виконання операції A");
    }
}

// Конкретний клас елемента B
public class ElementB : Element
{
    public override void Accept(IVisitor visitor)
    {
        visitor.Visit(this);
    }

    public void OperationB()
    {
        Console.WriteLine("Виконання операції B");
    }
}

// Конкретний клас відвідувача
public class ConcreteVisitor : IVisitor
{
    public void Visit(ElementA element)
    {
        element.OperationA();
    }

    public void Visit(ElementB element)
    {
        element.OperationB();
    }
}

class Program
{
    static void Main(string[] args)
    {
        Element[] elements = new Element[] { new ElementA(), new ElementB() };
        ConcreteVisitor visitor = new ConcreteVisitor();

        foreach (var element in elements)
        {
            element.Accept(visitor);
        }
    }
}

# Command Pattern in C#

## Overview

The Command pattern is a behavioral design pattern that turns a request into a stand-alone object containing all information about the request. This transformation allows you to parameterize methods with different requests, delay or queue a request’s execution, and support undoable operations.

## Benefits of Using the Command Pattern

- **Separation of Concerns**: Decouples the object that invokes the operation from the one that knows how to perform it.
- **Extensibility**: New commands can be added without changing existing code.
- **Flexibility**: Allows you to store a list of commands for delayed execution.

## Example in C#

This example demonstrates a simple implementation of the Command pattern in C#. It includes a `Command` interface, Concrete Commands, a `Receiver`, and an `Invoker`.

### Command Interface

```csharp
public interface ICommand
{
    void Execute();
}
```

### Concrete Commands

```csharp
public class LightOnCommand : ICommand
{
    private Light _light;

    public LightOnCommand(Light light)
    {
        _light = light;
    }

    public void Execute()
    {
        _light.On();
    }
}

public class LightOffCommand : ICommand
{
    private Light _light;

    public LightOffCommand(Light light)
    {
        _light = light;
    }

    public void Execute()
    {
        _light.Off();
    }
}
```

### Receiver

```csharp
public class Light
{
    public void On()
    {
        Console.WriteLine("Light is on");
    }

    public void Off()
    {
    Console.WriteLine("Light is off");
    }
}
```

### Invoker

```csharp
public class RemoteControl
{
    private ICommand _command;

    public void SetCommand(ICommand command)
    {
        _command = command;
    }

    public void PressButton()
    {
        _command.Execute();
    }
}
```

### Usage

```csharp
public class Program
{
    public static void Main(string[] args)
    {
        var light = new Light();
        var lightOn = new LightOnCommand(light);
        var lightOff = new LightOffCommand(light);

        var remote = new RemoteControl();
        
        remote.SetCommand(lightOn);
        remote.PressButton();

        remote.SetCommand(lightOff);
        remote.PressButton();
    }
}
```

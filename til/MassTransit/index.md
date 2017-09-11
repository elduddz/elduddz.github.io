 - [with Azure ServiceBus](withAzureServiceBus.md)

# scratch notes
official repo: http://masstransit-project.com/  
docs: http://masstransit.readthedocs.org/en/master/  
github: https://github.com/MassTransit  
Listen to: dotNet Rocks PodCast #1228  

When create contracts interfaces should be used.

no base classes

2 types called events and commands, when naming the message the type of message should dictate the tense of the message.

Commands are  Sent (using `send`) to the end point

Verb-Noun in the _Tell_ style

Events signify something has happened, so _Tell_ style in past tense.

## RabbitMQ and Erlang required

Follow the [RabbitMQ Setup](RabbitMQ/Setup.md)

## Example
```c#
public class UpdateCustomerConsumer :
    IConsumer<UpdateCustomerAddress>
{
    public async Task Consume(ConsumeContext<UpdateCustomerAddress> context)
    {
        await Console.Out.WriteLineAsync($"Updating customer: {context.Message.CustomerId}");

        // update the customer address
    }
}
```




 

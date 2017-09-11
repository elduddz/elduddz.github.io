## Install nuget package
```powershell  
Install-Package MassTransit.AzureServiceBus
```
also incase:
```powershell  
Install-Package MassTransit.Log4Net
```

## Create Publisher

```c#  
_busControl = Bus.Factory.CreateUsingAzureServiceBus(cfg =>
{
	cfg.Host(new Uri(ConfigurationManager.AppSettings["EndPoint"]),
		h =>
		{
			h.TokenProvider =
					TokenProvider.CreateSharedAccessSignatureTokenProvider(
						ConfigurationManager.AppSettings["SharedAccessKeyName"],
						ConfigurationManager.AppSettings["SharedAccessKey"]);
		});
	
	cfg.ReceiveEndpoint("moviemagic", e => { e.Consumer<RequestConsumer>(); });
});
```

## Create Subscriber
(using TopShelf to build basic service)
```c#  
return Bus.Factory.CreateUsingAzureServiceBus(cfg =>
{
	cfg.Host(new Uri(ConfigurationManager.AppSettings["EndPoint"]),
		h =>
		{
			h.TokenProvider =
				TokenProvider.CreateSharedAccessSignatureTokenProvider(
				ConfigurationManager.AppSettings["SharedAccessKeyName"],
				ConfigurationManager.AppSettings["SharedAccessKey"]);
		});
	cfg.OverrideDefaultBusEndpointQueueName("moviemagic");
});
```


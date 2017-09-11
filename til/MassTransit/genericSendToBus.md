I was sending messages to the bus, and as they were so similar I thought that generics would help.

where T : class allows T to be used as a class, so as you can see the `Send<T>` behaviour that I needed works.

```cs
private void SendToBus<T>(T request, string toWhere) where T : class
{
    try
    {
        Task.Run(async () =>
        {
            var sep =
            busControl.GetSendEndpoint(
            new Uri(ConfigurationManager.AppSettings[toWhere])).Result;
            await sep.Send<T>(request);
        }).Wait();
    }
    catch (Exception e)
    {
        Trace.TraceError(e.Message);
    }
}
```
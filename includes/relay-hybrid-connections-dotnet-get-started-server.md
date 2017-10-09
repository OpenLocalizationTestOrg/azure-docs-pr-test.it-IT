### <a name="create-a-console-application"></a><span data-ttu-id="b6ee5-101">Creare un'applicazione console</span><span class="sxs-lookup"><span data-stu-id="b6ee5-101">Create a console application</span></span>

<span data-ttu-id="b6ee5-102">Avviare Visual Studio e creare un nuovo progetto **App console (.NET Framework)**.</span><span class="sxs-lookup"><span data-stu-id="b6ee5-102">First, launch Visual Studio and create a new **Console App (.NET Framework)** project.</span></span>

### <a name="add-hello-relay-nuget-package"></a><span data-ttu-id="b6ee5-103">Aggiungere il pacchetto NuGet di inoltro hello</span><span class="sxs-lookup"><span data-stu-id="b6ee5-103">Add hello Relay NuGet package</span></span>

1. <span data-ttu-id="b6ee5-104">Fare clic sul progetto hello appena creato e quindi fare clic su **Gestisci pacchetti NuGet**.</span><span class="sxs-lookup"><span data-stu-id="b6ee5-104">Right-click hello newly created project and then click **Manage NuGet Packages**.</span></span>
2. <span data-ttu-id="b6ee5-105">Fare clic su hello **Sfoglia** scheda, quindi cercare "Microsoft.Azure.Relay" e seleziona hello **Microsoft Azure inoltro** elemento.</span><span class="sxs-lookup"><span data-stu-id="b6ee5-105">Click hello **Browse** tab, then search for "Microsoft.Azure.Relay" and select hello **Microsoft Azure Relay** item.</span></span> <span data-ttu-id="b6ee5-106">Fare clic su **installare** toocomplete hello installazione, quindi chiudere questa finestra di dialogo.</span><span class="sxs-lookup"><span data-stu-id="b6ee5-106">Click **Install** toocomplete hello installation, then close this dialog box.</span></span>

### <a name="write-some-code-tooreceive-messages"></a><span data-ttu-id="b6ee5-107">Scrivere codice tooreceive messaggi</span><span class="sxs-lookup"><span data-stu-id="b6ee5-107">Write some code tooreceive messages</span></span>

1. <span data-ttu-id="b6ee5-108">Sostituire hello `using` le istruzioni nella parte superiore di hello del file Program.cs hello con seguenti hello `using` istruzioni:</span><span class="sxs-lookup"><span data-stu-id="b6ee5-108">Replace hello existing `using` statements at hello top of hello Program.cs file with hello following `using` statements:</span></span>
   
    ```csharp
    using System;
    using System.IO;
    using System.Threading;
    using System.Threading.Tasks;
    using Microsoft.Azure.Relay;
    ```
2. <span data-ttu-id="b6ee5-109">Aggiungere le costanti toohello `Program` classe per i dettagli della connessione ibrida hello.</span><span class="sxs-lookup"><span data-stu-id="b6ee5-109">Add constants toohello `Program` class for hello hybrid connection details.</span></span> <span data-ttu-id="b6ee5-110">Sostituire i segnaposto hello tra parentesi quadre con valori hello ottenuti quando si crea la connessione ibrida hello.</span><span class="sxs-lookup"><span data-stu-id="b6ee5-110">Replace hello placeholders in brackets with hello values you obtained when creating hello hybrid connection.</span></span> <span data-ttu-id="b6ee5-111">Nome completo dello spazio dei nomi di hello toouse assicurarsi di essere:</span><span class="sxs-lookup"><span data-stu-id="b6ee5-111">Be sure toouse hello fully qualified namespace name:</span></span>
   
    ```csharp
    private const string RelayNamespace = "{RelayNamespace}.servicebus.windows.net";
    private const string ConnectionName = "{HybridConnectionName}";
    private const string KeyName = "{SASKeyName}";
    private const string Key = "{SASKey}";
    ```
3. <span data-ttu-id="b6ee5-112">Aggiungere al metodo chiamato hello `ProcessMessagesOnConnection` toohello `Program` classe:</span><span class="sxs-lookup"><span data-stu-id="b6ee5-112">Add hello following method called `ProcessMessagesOnConnection` toohello `Program` class:</span></span>
   
    ```csharp
    // Method is used tooinitiate connection
    private static async void ProcessMessagesOnConnection(HybridConnectionStream relayConnection, CancellationTokenSource cts)
    {
        Console.WriteLine("New session");
   
        // hello connection is a fully bidrectional stream. 
        // We put a stream reader and a stream writer over it 
        // which allows us tooread UTF-8 text that comes from 
        // hello sender and toowrite text replies back.
        var reader = new StreamReader(relayConnection);
        var writer = new StreamWriter(relayConnection) { AutoFlush = true };
        while (!cts.IsCancellationRequested)
        {
            try
            {
                // Read a line of input until a newline is encountered
                var line = await reader.ReadLineAsync();
   
                if (string.IsNullOrEmpty(line))
                {
                    // If there's no input data, we will signal that 
                    // we will no longer send data on this connection
                    // and then break out of hello processing loop.
                    await relayConnection.ShutdownAsync(cts.Token);
                    break;
                }
   
                // Output hello line on hello console
                Console.WriteLine(line);
   
                // Write hello line back toohello client, prepending "Echo:"
                await writer.WriteLineAsync($"Echo: {line}");
            }
            catch (IOException)
            {
                // Catch an IO exception that is likely caused because
                // hello client disconnected.
                Console.WriteLine("Client closed connection");
                break;
            }
        }
   
        Console.WriteLine("End session");
   
        // Closing hello connection
        await relayConnection.CloseAsync(cts.Token);
    }
    ```
4. <span data-ttu-id="b6ee5-113">Aggiungere un altro metodo chiamato `RunAsync` toohello `Program` classe, come indicato di seguito:</span><span class="sxs-lookup"><span data-stu-id="b6ee5-113">Add another method called `RunAsync` toohello `Program` class, as follows:</span></span>
   
    ```csharp
    private static async Task RunAsync()
    {
        var cts = new CancellationTokenSource();
   
        var tokenProvider = TokenProvider.CreateSharedAccessSignatureTokenProvider(KeyName, Key);
        var listener = new HybridConnectionListener(new Uri(string.Format("sb://{0}/{1}", RelayNamespace, ConnectionName)), tokenProvider);
   
        // Subscribe toohello status events
        listener.Connecting += (o, e) => { Console.WriteLine("Connecting"); };
        listener.Offline += (o, e) => { Console.WriteLine("Offline"); };
        listener.Online += (o, e) => { Console.WriteLine("Online"); };
   
        // Opening hello listener will establish hello control channel to
        // hello Azure Relay service. hello control channel will be continuously 
        // maintained and reestablished when connectivity is disrupted.
        await listener.OpenAsync(cts.Token);
        Console.WriteLine("Server listening");
   
        // Providing callback for cancellation token that will close hello listener.
        cts.Token.Register(() => listener.CloseAsync(CancellationToken.None));
   
        // Start a new thread that will continuously read hello console.
        new Task(() => Console.In.ReadLineAsync().ContinueWith((s) => { cts.Cancel(); })).Start();
   
        // Accept hello next available, pending connection request. 
        // Shutting down hello listener will allow a clean exit with 
        // this method returning null
        while (true)
        {
            var relayConnection = await listener.AcceptConnectionAsync();
            if (relayConnection == null)
            {
                break;
            }
   
            ProcessMessagesOnConnection(relayConnection, cts);
        }
   
        // Close hello listener after we exit hello processing loop
        await listener.CloseAsync(cts.Token);
    }
    ```
5. <span data-ttu-id="b6ee5-114">Aggiungere hello successiva riga di codice toohello `Main` metodo hello `Program` classe:</span><span class="sxs-lookup"><span data-stu-id="b6ee5-114">Add hello following line of code toohello `Main` method in hello `Program` class:</span></span>
   
    ```csharp
    RunAsync().GetAwaiter().GetResult();
    ```
   
    <span data-ttu-id="b6ee5-115">Al termine, il file Program.cs avrà l'aspetto seguente:</span><span class="sxs-lookup"><span data-stu-id="b6ee5-115">Here is what your completed Program.cs file should look like:</span></span>
   
    ```csharp
    namespace Server
    {
        using System;
        using System.IO;
        using System.Threading;
        using System.Threading.Tasks;
        using Microsoft.Azure.Relay;
   
        public class Program
        {
            private const string RelayNamespace = "{RelayNamespace}.servicebus.windows.net";
            private const string ConnectionName = "{HybridConnectionName}";
            private const string KeyName = "{SASKeyName}";
            private const string Key = "{SASKey}";
   
            public static void Main(string[] args)
            {
                RunAsync().GetAwaiter().GetResult();
            }
   
            private static async Task RunAsync()
            {
                var cts = new CancellationTokenSource();
   
                var tokenProvider = TokenProvider.CreateSharedAccessSignatureTokenProvider(KeyName, Key);
                var listener = new HybridConnectionListener(new Uri(string.Format("sb://{0}/{1}", RelayNamespace, ConnectionName)), tokenProvider);
   
                // Subscribe toohello status events
                listener.Connecting += (o, e) => { Console.WriteLine("Connecting"); };
                listener.Offline += (o, e) => { Console.WriteLine("Offline"); };
                listener.Online += (o, e) => { Console.WriteLine("Online"); };
   
                // Opening hello listener will establish hello control channel to
                // hello Azure Relay service. hello control channel will be continuously 
                // maintained and reestablished when connectivity is disrupted.
                await listener.OpenAsync(cts.Token);
                Console.WriteLine("Server listening");
   
                // Providing callback for cancellation token that will close hello listener.
                cts.Token.Register(() => listener.CloseAsync(CancellationToken.None));
   
                // Start a new thread that will continuously read hello console.
                new Task(() => Console.In.ReadLineAsync().ContinueWith((s) => { cts.Cancel(); })).Start();
   
                // Accept hello next available, pending connection request. 
                // Shutting down hello listener will allow a clean exit with 
                // this method returning null
                while (true)
                {
                    var relayConnection = await listener.AcceptConnectionAsync();
                    if (relayConnection == null)
                    {
                        break;
                    }
   
                    ProcessMessagesOnConnection(relayConnection, cts);
                }
   
                // Close hello listener after we exit hello processing loop
                await listener.CloseAsync(cts.Token);
            }
   
            private static async void ProcessMessagesOnConnection(HybridConnectionStream relayConnection, CancellationTokenSource cts)
            {
                Console.WriteLine("New session");
   
                // hello connection is a fully bidrectional stream. 
                // We put a stream reader and a stream writer over it 
                // which allows us tooread UTF-8 text that comes from 
                // hello sender and toowrite text replies back.
                var reader = new StreamReader(relayConnection);
                var writer = new StreamWriter(relayConnection) { AutoFlush = true };
                while (!cts.IsCancellationRequested)
                {
                    try
                    {
                        // Read a line of input until a newline is encountered
                        var line = await reader.ReadLineAsync();
   
                        if (string.IsNullOrEmpty(line))
                        {
                            // If there's no input data, we will signal that 
                            // we will no longer send data on this connection
                            // and then break out of hello processing loop.
                            await relayConnection.ShutdownAsync(cts.Token);
                            break;
                        }
   
                        // Output hello line on hello console
                        Console.WriteLine(line);
   
                        // Write hello line back toohello client, prepending "Echo:"
                        await writer.WriteLineAsync($"Echo: {line}");
                    }
                    catch (IOException)
                    {
                        // Catch an IO exception that is likely caused because
                        // hello client disconnected.
                        Console.WriteLine("Client closed connection");
                        break;
                    }
                }
   
                Console.WriteLine("End session");
   
                // Closing hello connection
                await relayConnection.CloseAsync(cts.Token);
            }
        }
    }
    ```


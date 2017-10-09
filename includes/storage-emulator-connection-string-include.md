<span data-ttu-id="64b3d-101">emulatore di archiviazione Hello supporta un singolo account fisso e una chiave di autenticazione noto per l'autenticazione chiave condivisa.</span><span class="sxs-lookup"><span data-stu-id="64b3d-101">hello storage emulator supports a single fixed account and a well-known authentication key for Shared Key authentication.</span></span> <span data-ttu-id="64b3d-102">Questo account e questa chiave sono hello le credenziali di autenticazione chiave condivisa sole consentite per l'utilizzo con l'emulatore di archiviazione hello.</span><span class="sxs-lookup"><span data-stu-id="64b3d-102">This account and key are hello only Shared Key credentials permitted for use with hello storage emulator.</span></span> <span data-ttu-id="64b3d-103">Sono:</span><span class="sxs-lookup"><span data-stu-id="64b3d-103">They are:</span></span>

```
Account name: devstoreaccount1
Account key: Eby8vdM02xNOcqFlqUwJPLlmEtlCDXJ1OUzFT50uSRZ6IFsuFq2UVErCz4I6tq/K1SZFPTOtr/KBHBeksoGMGw==
```

> [!NOTE]
> <span data-ttu-id="64b3d-104">chiave di autenticazione Hello supportate dall'emulatore di archiviazione hello è destinato solo a funzionalità di hello test del codice di autenticazione client.</span><span class="sxs-lookup"><span data-stu-id="64b3d-104">hello authentication key supported by hello storage emulator is intended only for testing hello functionality of your client authentication code.</span></span> <span data-ttu-id="64b3d-105">Non viene utilizzata per eventuali scopi di sicurezza.</span><span class="sxs-lookup"><span data-stu-id="64b3d-105">It does not serve any security purpose.</span></span> <span data-ttu-id="64b3d-106">È possibile utilizzare l'account di archiviazione di produzione e la chiave con l'emulatore di archiviazione hello.</span><span class="sxs-lookup"><span data-stu-id="64b3d-106">You cannot use your production storage account and key with hello storage emulator.</span></span> <span data-ttu-id="64b3d-107">Non utilizzare account di sviluppo hello con dati di produzione.</span><span class="sxs-lookup"><span data-stu-id="64b3d-107">You should not use hello development account with production data.</span></span>
> 
> <span data-ttu-id="64b3d-108">emulatore di archiviazione Hello supporta solo la connessione tramite HTTP.</span><span class="sxs-lookup"><span data-stu-id="64b3d-108">hello storage emulator supports connection via HTTP only.</span></span> <span data-ttu-id="64b3d-109">Tuttavia, HTTPS è hello consigliato di protocollo per accedere alle risorse in un account di archiviazione di Azure di produzione.</span><span class="sxs-lookup"><span data-stu-id="64b3d-109">However, HTTPS is hello recommended protocol for accessing resources in a production Azure storage account.</span></span>
> 

#### <a name="connect-toohello-emulator-account-using-a-shortcut"></a><span data-ttu-id="64b3d-110">Connettere l'account dell'emulatore toohello utilizzando un collegamento</span><span class="sxs-lookup"><span data-stu-id="64b3d-110">Connect toohello emulator account using a shortcut</span></span>
<span data-ttu-id="64b3d-111">Hello più semplice modo tooconnect toohello emulatore di archiviazione dall'applicazione è una stringa di connessione nel file di configurazione dell'applicazione che fa riferimento il collegamento hello tooconfigure `UseDevelopmentStorage=true`.</span><span class="sxs-lookup"><span data-stu-id="64b3d-111">hello easiest way tooconnect toohello storage emulator from your application is tooconfigure a connection string in your application's configuration file that references hello shortcut `UseDevelopmentStorage=true`.</span></span> <span data-ttu-id="64b3d-112">Di seguito è riportato un esempio dell'emulatore di archiviazione toohello stringa connessione in un *app* file:</span><span class="sxs-lookup"><span data-stu-id="64b3d-112">Here's an example of a connection string toohello storage emulator in an *app.config* file:</span></span> 

```xml
<appSettings>
  <add key="StorageConnectionString" value="UseDevelopmentStorage=true" />
</appSettings>
```

#### <a name="connect-toohello-emulator-account-using-hello-well-known-account-name-and-key"></a><span data-ttu-id="64b3d-113">La connessione utilizzando la chiave e il nome di un account noto hello toohello account dell'emulatore</span><span class="sxs-lookup"><span data-stu-id="64b3d-113">Connect toohello emulator account using hello well-known account name and key</span></span>
<span data-ttu-id="64b3d-114">toocreate una stringa di connessione che riferimenti hello Nome account dell'emulatore e chiave, è necessario specificare gli endpoint hello per ognuno di hello servizi si desidera toouse dall'emulatore hello nella stringa di connessione hello.</span><span class="sxs-lookup"><span data-stu-id="64b3d-114">toocreate a connection string that references hello emulator account name and key, you must specify hello endpoints for each of hello services you wish toouse from hello emulator in hello connection string.</span></span> <span data-ttu-id="64b3d-115">Ciò è necessario in modo che la stringa di connessione hello farà riferimento a endpoint di emulatore hello, che sono diverse da quelle per un account di archiviazione di produzione.</span><span class="sxs-lookup"><span data-stu-id="64b3d-115">This is necessary so that hello connection string will reference hello emulator endpoints, which are different than those for a production storage account.</span></span> <span data-ttu-id="64b3d-116">Ad esempio, il valore di hello la stringa di connessione sarà simile al seguente:</span><span class="sxs-lookup"><span data-stu-id="64b3d-116">For example, hello value of your connection string will look like this:</span></span>

```
DefaultEndpointsProtocol=http;AccountName=devstoreaccount1;
AccountKey=Eby8vdM02xNOcqFlqUwJPLlmEtlCDXJ1OUzFT50uSRZ6IFsuFq2UVErCz4I6tq/K1SZFPTOtr/KBHBeksoGMGw==;
BlobEndpoint=http://127.0.0.1:10000/devstoreaccount1;
TableEndpoint=http://127.0.0.1:10002/devstoreaccount1;
QueueEndpoint=http://127.0.0.1:10001/devstoreaccount1;
```

<span data-ttu-id="64b3d-117">Questo valore è identico toohello collegamento illustrato sopra, `UseDevelopmentStorage=true`.</span><span class="sxs-lookup"><span data-stu-id="64b3d-117">This value is identical toohello shortcut shown above, `UseDevelopmentStorage=true`.</span></span>

#### <a name="specify-an-http-proxy"></a><span data-ttu-id="64b3d-118">Specificare un proxy HTTP</span><span class="sxs-lookup"><span data-stu-id="64b3d-118">Specify an HTTP proxy</span></span>
<span data-ttu-id="64b3d-119">È anche possibile specificare un toouse proxy HTTP quando si verifica il servizio nell'emulatore di archiviazione hello.</span><span class="sxs-lookup"><span data-stu-id="64b3d-119">You can also specify an HTTP proxy toouse when you're testing your service against hello storage emulator.</span></span> <span data-ttu-id="64b3d-120">Questo può essere utile per l'osservazione di richieste e risposte HTTP mentre si esegue il debug di operazioni nei servizi di archiviazione hello.</span><span class="sxs-lookup"><span data-stu-id="64b3d-120">This can be useful for observing HTTP requests and responses while you're debugging operations against hello storage services.</span></span> <span data-ttu-id="64b3d-121">toospecify un proxy, aggiungere hello `DevelopmentStorageProxyUri` opzione toohello stringa di connessione e impostare il proxy toohello valore URI.</span><span class="sxs-lookup"><span data-stu-id="64b3d-121">toospecify a proxy, add hello `DevelopmentStorageProxyUri` option toohello connection string, and set its value toohello proxy URI.</span></span> <span data-ttu-id="64b3d-122">Di seguito è ad esempio, una stringa di connessione che punta toohello emulatore di archiviazione e di configura un proxy HTTP:</span><span class="sxs-lookup"><span data-stu-id="64b3d-122">For example, here is a connection string that points toohello storage emulator and configures an HTTP proxy:</span></span>

```
UseDevelopmentStorage=true;DevelopmentStorageProxyUri=http://myProxyUri
```


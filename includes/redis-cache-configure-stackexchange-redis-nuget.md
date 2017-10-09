<span data-ttu-id="92321-101">Applicazioni .NET possono usare hello **stackexchange. Redis** client della cache, che possono essere configurate in Visual Studio usando un pacchetto NuGet che semplifica la configurazione di hello di applicazioni client della cache.</span><span class="sxs-lookup"><span data-stu-id="92321-101">.NET applications can use hello **StackExchange.Redis** cache client, which can be configured in Visual Studio using a NuGet package that simplifies hello configuration of cache client applications.</span></span> 

> [!NOTE]
> <span data-ttu-id="92321-102">Per ulteriori informazioni, vedere hello [stackexchange. Redis](http://github.com/StackExchange/StackExchange.Redis) github pagina e hello [documentazione relativa al client della cache stackexchange. Redis](http://github.com/StackExchange/StackExchange.Redis#documentation).</span><span class="sxs-lookup"><span data-stu-id="92321-102">For more information, see hello [StackExchange.Redis](http://github.com/StackExchange/StackExchange.Redis) github page and  hello [StackExchange.Redis cache client documentation](http://github.com/StackExchange/StackExchange.Redis#documentation).</span></span>
> 
> 

<span data-ttu-id="92321-103">tooconfigure un'applicazione client in Visual Studio usando hello pacchetto NuGet stackexchange. Redis, fare clic sul progetto hello in **Esplora** e scegliere **Gestisci pacchetti NuGet**.</span><span class="sxs-lookup"><span data-stu-id="92321-103">tooconfigure a client application in Visual Studio using hello StackExchange.Redis NuGet package, right-click hello project in **Solution Explorer** and choose **Manage NuGet Packages**.</span></span> 

![Manage NuGet packages](media/redis-cache-configure-stackexchange-redis-nuget/redis-cache-manage-nuget-menu.png)

<span data-ttu-id="92321-105">Tipo **stackexchange. Redis** o **Stackexchange** nella casella di testo di ricerca hello, selezionare la versione desiderata di hello dai risultati hello e fare clic su **installare**.</span><span class="sxs-lookup"><span data-stu-id="92321-105">Type **StackExchange.Redis** or **StackExchange.Redis.StrongName** into hello search text box, select hello desired version from hello results, and click **Install**.</span></span>

> [!NOTE]
> <span data-ttu-id="92321-106">Se si preferisce una versione con nome sicuro di hello toouse **stackexchange. Redis** libreria client, scegliere **Stackexchange**; in caso contrario scegliere **Stackexchange**.</span><span class="sxs-lookup"><span data-stu-id="92321-106">If you prefer toouse a strong-named version of hello **StackExchange.Redis** client library, choose **StackExchange.Redis.StrongName**; otherwise choose **StackExchange.Redis**.</span></span>
> 
> 

![StackExchange.Redis NuGet package](media/redis-cache-configure-stackexchange-redis-nuget/redis-cache-stackexchange-redis.png)

<span data-ttu-id="92321-108">Hello NuGet pacchetto Scarica e aggiunge hello necessari riferimenti ad assembly per il tooaccess di applicazione client Cache Redis di Azure con i client della cache di hello stackexchange. Redis.</span><span class="sxs-lookup"><span data-stu-id="92321-108">hello NuGet package downloads and adds hello required assembly references for your client application tooaccess Azure Redis Cache with hello StackExchange.Redis cache client.</span></span>

> [!NOTE]
> <span data-ttu-id="92321-109">Se in precedenza è stato configurato il toouse progetto stackexchange. Redis, è possibile cercare il pacchetto toohello gli aggiornamenti da hello **Gestione pacchetti NuGet**.</span><span class="sxs-lookup"><span data-stu-id="92321-109">If you have previously configured your project toouse StackExchange.Redis, you can check for updates toohello package from hello **NuGet Package Manager**.</span></span> <span data-ttu-id="92321-110">toocheck per e versioni aggiornate di installazione di hello pacchetto NuGet stackexchange. Redis, fare clic su **aggiornamenti** in hello hello **Gestione pacchetti NuGet** finestra.</span><span class="sxs-lookup"><span data-stu-id="92321-110">toocheck for and install updated versions of hello StackExchange.Redis NuGet package, click **Updates** in hello hello **NuGet Package Manager** window.</span></span> <span data-ttu-id="92321-111">Se un toohello aggiornamento pacchetto NuGet stackexchange. Redis è disponibile, è possibile aggiornare la versione di hello aggiornato toouse di progetto.</span><span class="sxs-lookup"><span data-stu-id="92321-111">If an update toohello StackExchange.Redis NuGet package is available, you can update your project toouse hello updated version.</span></span>
> 
> 

<span data-ttu-id="92321-112">È inoltre possibile installare il pacchetto NuGet stackexchange. Redis hello facendo **Gestione pacchetti NuGet**, **Package Manager Console** da hello **strumenti** menu e hello in esecuzione comando seguente da hello **Package Manager Console** finestra.</span><span class="sxs-lookup"><span data-stu-id="92321-112">You can also install hello StackExchange.Redis NuGet package by clicking **NuGet Package Manager**, **Package Manager Console** from hello **Tools** menu, and running hello following command from hello **Package Manager Console** window.</span></span>
    
```
Install-Package StackExchange.Redis
```

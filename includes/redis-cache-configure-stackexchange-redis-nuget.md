<span data-ttu-id="5a7ad-101">Le applicazioni .NET possono usare il client della cache **StackExchange.Redis** , che può essere configurato in Visual Studio con un pacchetto NuGet per semplificare la configurazione delle applicazioni client della cache.</span><span class="sxs-lookup"><span data-stu-id="5a7ad-101">.NET applications can use the **StackExchange.Redis** cache client, which can be configured in Visual Studio using a NuGet package that simplifies the configuration of cache client applications.</span></span> 

> [!NOTE]
> <span data-ttu-id="5a7ad-102">Per altre informazioni, vedere la pagina di Github [StackExchange.Redis](http://github.com/StackExchange/StackExchange.Redis)e la [documentazione del client della cache StackExchange.Redis](http://github.com/StackExchange/StackExchange.Redis#documentation).</span><span class="sxs-lookup"><span data-stu-id="5a7ad-102">For more information, see the [StackExchange.Redis](http://github.com/StackExchange/StackExchange.Redis) github page and  the [StackExchange.Redis cache client documentation](http://github.com/StackExchange/StackExchange.Redis#documentation).</span></span>
> 
> 

<span data-ttu-id="5a7ad-103">Per configurare un'applicazione client in Visual Studio con il pacchetto NuGet StackExchange.Redis, fare clic con il pulsante destro del mouse sul progetto in **Esplora soluzioni** e scegliere **Gestisci pacchetti NuGet**.</span><span class="sxs-lookup"><span data-stu-id="5a7ad-103">To configure a client application in Visual Studio using the StackExchange.Redis NuGet package, right-click the project in **Solution Explorer** and choose **Manage NuGet Packages**.</span></span> 

![Manage NuGet packages](media/redis-cache-configure-stackexchange-redis-nuget/redis-cache-manage-nuget-menu.png)

<span data-ttu-id="5a7ad-105">Digitare **StackExchange.Redis** o **StackExchange.Redis.StrongName** nella casella di testo di ricerca, selezionare la versione desiderata nei risultati e fare clic su **Installa**.</span><span class="sxs-lookup"><span data-stu-id="5a7ad-105">Type **StackExchange.Redis** or **StackExchange.Redis.StrongName** into the search text box, select the desired version from the results, and click **Install**.</span></span>

> [!NOTE]
> <span data-ttu-id="5a7ad-106">Se si preferisce usare una versione con nome sicuro della libreria client **StackExchange.Redis**, scegliere **StackExchange.Redis.StrongName**. In caso contrario, scegliere **StackExchange.Redis**.</span><span class="sxs-lookup"><span data-stu-id="5a7ad-106">If you prefer to use a strong-named version of the **StackExchange.Redis** client library, choose **StackExchange.Redis.StrongName**; otherwise choose **StackExchange.Redis**.</span></span>
> 
> 

![StackExchange.Redis NuGet package](media/redis-cache-configure-stackexchange-redis-nuget/redis-cache-stackexchange-redis.png)

<span data-ttu-id="5a7ad-108">Il pacchetto NuGet scarica e aggiunge i riferimenti ad assembly necessari per consentire all'applicazione client di accedere a Cache Redis di Azure con il client della cache StackExchange.Redis.</span><span class="sxs-lookup"><span data-stu-id="5a7ad-108">The NuGet package downloads and adds the required assembly references for your client application to access Azure Redis Cache with the StackExchange.Redis cache client.</span></span>

> [!NOTE]
> <span data-ttu-id="5a7ad-109">Se il progetto è stato configurato per utilizzare StackExchange.Redis, è possibile controllare la presenza di aggiornamenti per il pacchetto da **Gestione pacchetti NuGet**.</span><span class="sxs-lookup"><span data-stu-id="5a7ad-109">If you have previously configured your project to use StackExchange.Redis, you can check for updates to the package from the **NuGet Package Manager**.</span></span> <span data-ttu-id="5a7ad-110">Per controllare e installare le versioni aggiornate del pacchetto NuGet StackExchange.Redis, fare clic su **Aggiornamenti** nella finestra di **Gestione pacchetti NuGet**.</span><span class="sxs-lookup"><span data-stu-id="5a7ad-110">To check for and install updated versions of the StackExchange.Redis NuGet package, click **Updates** in the the **NuGet Package Manager** window.</span></span> <span data-ttu-id="5a7ad-111">Se è disponibile un aggiornamento per il pacchetto NuGet StackExchange.Redis, è possibile aggiornare il progetto in modo da utilizzare la versione aggiornata.</span><span class="sxs-lookup"><span data-stu-id="5a7ad-111">If an update to the StackExchange.Redis NuGet package is available, you can update your project to use the updated version.</span></span>
> 
> 

<span data-ttu-id="5a7ad-112">È anche possibile installare il pacchetto NuGet StackExchange.Redis facendo clic su **Gestione pacchetti NuGet**, **Console di Gestione pacchetti** dal menu **Strumenti** ed eseguendo questo comando dalla finestra **Console di Gestione pacchetti**.</span><span class="sxs-lookup"><span data-stu-id="5a7ad-112">You can also install the StackExchange.Redis NuGet package by clicking **NuGet Package Manager**, **Package Manager Console** from the **Tools** menu, and running the following command from the **Package Manager Console** window.</span></span>
    
```
Install-Package StackExchange.Redis
```

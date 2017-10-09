toocreate una cache, prima di tutto Accedi toohello [portale di Azure](https://portal.azure.com), fare clic su **New** > **database** > **Cache Redis**.

> [!NOTE]
> Se non si ha un account Azure, è possibile [creare un account Azure gratuito](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=redis_cache_hero) in pochi minuti.
> 
> 

![New cache](media/redis-cache-create/redis-cache-new-cache-menu.png)

> [!NOTE]
> Inoltre toocreating memorizza nella cache di hello portale di Azure, è anche possibile crearli tramite Gestione risorse di Azure CLI, PowerShell o modelli.
> 
> * toocreate una cache con i modelli di gestione risorse, vedere [creare una cache Redis utilizzando un modello](../articles/redis-cache/cache-redis-cache-arm-provision.md).
> * toocreate una cache usando Azure PowerShell, vedere [gestire Cache Redis di Azure con Azure PowerShell](../articles/redis-cache/cache-howto-manage-redis-cache-powershell.md).
> * toocreate una cache usando l'interfaccia CLI di Azure, vedere [come toocreate e gestire Cache Redis di Azure utilizzando l'interfaccia della riga di comando di Azure (Azure CLI) hello](../articles/redis-cache/cache-manage-cli.md).
> 
> 

In hello **nuova Cache Redis** pannello specificare hello configurazione desiderata per la cache di hello.

![Create cache](media/redis-cache-create/redis-cache-cache-create.png) 

* In **nome Dns**, immettere un toouse nome della cache univoche per l'endpoint della cache di hello. nome della cache di Hello deve essere una stringa di lunghezza compresa tra 1 e 63 caratteri e contenere solo numeri, lettere e hello `-` carattere. Hello nome della cache non può iniziare o terminare con hello `-` carattere e consecutivi `-` caratteri non validi.
* Per **sottoscrizione**, selezionare hello sottoscrizione di Azure che si desidera toouse per cache di hello. Se l'account ha una sola sottoscrizione, verrà selezionata automaticamente e hello **sottoscrizione** non verrà visualizzato l'elenco a discesa.
* In **Gruppo di risorse**selezionare o creare un gruppo di risorse per la cache. Per ulteriori informazioni, vedere [gruppi di risorse utilizzando toomanage le risorse di Azure](../articles/azure-resource-manager/resource-group-overview.md). 
* Utilizzare **percorso** toospecify hello posizione geografica in cui viene ospitata la cache. Per prestazioni ottimali hello, Microsoft consiglia vivamente di creare cache di hello in hello stessa area dell'applicazione client della cache di hello.
* Utilizzare **tariffario** tooselect hello desiderato di dimensioni della cache e le funzionalità.
* **Redis cluster** consente toocreate cache maggiore a 53 GB e tooshard dati tra più nodi di Redis. Per ulteriori informazioni, vedere [come tooconfigure clustering per una Cache Redis di Azure Premium](../articles/redis-cache/cache-how-to-premium-clustering.md).
* **Persistenza di redis** offre hello possibilità toopersist il tooan cache account di archiviazione di Azure. Per istruzioni sulla configurazione della persistenza, vedere [come persistenza tooconfigure per una Cache Redis di Azure Premium](../articles/redis-cache/cache-how-to-premium-persistence.md).
* **Rete virtuale** fornisce sicurezza avanzata e isolamento limitando l'accesso tooyour cache tooonly tali client hello specificato all'interno di rete virtuale di Azure. È possibile utilizzare tutte le funzionalità di hello di rete virtuale, ad esempio subnet, criteri di controllo di accesso e altre funzionalità toofurther limitare l'accesso tooRedis. Per ulteriori informazioni, vedere [la modalità di supporto tooconfigure rete virtuale per una Cache Redis di Azure Premium](../articles/redis-cache/cache-how-to-premium-vnet.md).
* Per le nuove cache la porta senza SSL è disabilitata per impostazione predefinita. porta non SSL tooenable hello controllo **sbloccare la porta (non SSL crittografata) 6379**.

Una volta configurate le nuove opzioni della cache di hello, fare clic su **crea**. Può richiedere alcuni minuti per toobe di cache di hello creato. stato hello toocheck, è possibile monitorare lo stato di avanzamento hello nella schermata iniziale di hello. Dopo aver creata la cache di hello, la nuova cache ha un **esecuzione** stato ed è pronto per l'utilizzo con [impostazioni predefinite](../articles/redis-cache/cache-configure.md#default-redis-server-configuration).

![Cache created](media/redis-cache-create/redis-cache-cache-created.png)


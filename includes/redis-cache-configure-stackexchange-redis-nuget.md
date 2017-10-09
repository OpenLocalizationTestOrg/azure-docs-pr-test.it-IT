Applicazioni .NET possono usare hello **stackexchange. Redis** client della cache, che possono essere configurate in Visual Studio usando un pacchetto NuGet che semplifica la configurazione di hello di applicazioni client della cache. 

> [!NOTE]
> Per ulteriori informazioni, vedere hello [stackexchange. Redis](http://github.com/StackExchange/StackExchange.Redis) github pagina e hello [documentazione relativa al client della cache stackexchange. Redis](http://github.com/StackExchange/StackExchange.Redis#documentation).
> 
> 

tooconfigure un'applicazione client in Visual Studio usando hello pacchetto NuGet stackexchange. Redis, fare clic sul progetto hello in **Esplora** e scegliere **Gestisci pacchetti NuGet**. 

![Manage NuGet packages](media/redis-cache-configure-stackexchange-redis-nuget/redis-cache-manage-nuget-menu.png)

Tipo **stackexchange. Redis** o **Stackexchange** nella casella di testo di ricerca hello, selezionare la versione desiderata di hello dai risultati hello e fare clic su **installare**.

> [!NOTE]
> Se si preferisce una versione con nome sicuro di hello toouse **stackexchange. Redis** libreria client, scegliere **Stackexchange**; in caso contrario scegliere **Stackexchange**.
> 
> 

![StackExchange.Redis NuGet package](media/redis-cache-configure-stackexchange-redis-nuget/redis-cache-stackexchange-redis.png)

Hello NuGet pacchetto Scarica e aggiunge hello necessari riferimenti ad assembly per il tooaccess di applicazione client Cache Redis di Azure con i client della cache di hello stackexchange. Redis.

> [!NOTE]
> Se in precedenza è stato configurato il toouse progetto stackexchange. Redis, è possibile cercare il pacchetto toohello gli aggiornamenti da hello **Gestione pacchetti NuGet**. toocheck per e versioni aggiornate di installazione di hello pacchetto NuGet stackexchange. Redis, fare clic su **aggiornamenti** in hello hello **Gestione pacchetti NuGet** finestra. Se un toohello aggiornamento pacchetto NuGet stackexchange. Redis è disponibile, è possibile aggiornare la versione di hello aggiornato toouse di progetto.
> 
> 

È inoltre possibile installare il pacchetto NuGet stackexchange. Redis hello facendo **Gestione pacchetti NuGet**, **Package Manager Console** da hello **strumenti** menu e hello in esecuzione comando seguente da hello **Package Manager Console** finestra.
    
```
Install-Package StackExchange.Redis
```

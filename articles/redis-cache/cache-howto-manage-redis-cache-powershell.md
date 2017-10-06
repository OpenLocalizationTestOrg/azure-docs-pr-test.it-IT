---
title: Cache Redis di Azure con Azure PowerShell aaaManage | Documenti Microsoft
description: "Informazioni su come le attività amministrative di tooperform per Cache Redis di Azure con Azure PowerShell."
services: redis-cache
documentationcenter: 
author: steved0x
manager: douge
editor: 
ms.assetid: 1136efe5-1e33-4d91-bb49-c8e2a6dca475
ms.service: cache
ms.workload: tbd
ms.tgt_pltfrm: cache-redis
ms.devlang: na
ms.topic: article
ms.date: 07/13/2017
ms.author: sdanie
ms.openlocfilehash: 1d526ce65c4bc05345cd6c3ff370211ed562cab4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="manage-azure-redis-cache-with-azure-powershell"></a>Gestire Cache Redis di Azure con Azure PowerShell
> [!div class="op_single_selector"]
> * [PowerShell](cache-howto-manage-redis-cache-powershell.md)
> * [Interfaccia della riga di comando di Azure](cache-manage-cli.md)
> 
> 

Questo argomento viene illustrato come tooperform comuni attività, ad esempio creare, aggiornare e ridimensionare le istanze di Cache Redis di Azure, come chiavi di accesso tooregenerate e come tooview informazioni delle cache. Per un elenco completo dei cmdlet PowerShell di Cache Redis di Azure, vedere [Cmdlet di Cache Redis di Azure](https://msdn.microsoft.com/library/azure/mt634513.aspx).

[!INCLUDE [learn-about-deployment-models](../../includes/learn-about-deployment-models-rm-include.md)]

Per ulteriori informazioni sul modello di distribuzione classica hello, vedere [Azure Resource Manager e distribuzione classica: comprendere i modelli di distribuzione e lo stato delle risorse di hello](../azure-resource-manager/resource-manager-deployment-model.md#classic-deployment-characteristics).

## <a name="prerequisites"></a>Prerequisiti
Se è già installato PowerShell di Microsoft Azure, è necessario installare Azure PowerShell versione 1.0.0 o versione successiva. È possibile controllare la versione hello di Azure PowerShell che è stato installato con questo comando al prompt dei comandi di Azure PowerShell hello.

    Get-Module azure | format-table version


In primo luogo, è necessario accedere tooAzure con questo comando.

    Login-AzureRmAccount

Specificare l'indirizzo di posta elettronica hello del proprio account Azure e la relativa password nella finestra di dialogo hello accesso di Microsoft Azure.

Successivamente, se si dispone di più sottoscrizioni di Azure, è necessario tooset la sottoscrizione di Azure. toosee un elenco delle sottoscrizioni correnti, eseguire questo comando.

    Get-AzureRmSubscription | sort SubscriptionName | Select SubscriptionName

toospecify hello sottoscrizione eseguire hello comando seguente. Nell'esempio seguente di hello, nome della sottoscrizione hello è `ContosoSubscription`.

    Select-AzureRmSubscription -SubscriptionName ContosoSubscription

Prima di poter utilizzare Windows PowerShell con Gestione risorse di Azure, è necessario hello segue:

* Windows PowerShell, versione 3.0 o 4.0. versione di hello toofind di Windows PowerShell, digitare:`$PSVersionTable` e verificare il valore di hello `PSVersion` è 3.0 o 4.0. tooinstall una versione compatibile, vedere [Windows Management Framework 3.0](http://www.microsoft.com/download/details.aspx?id=34595) o [Windows Management Framework 4.0](http://www.microsoft.com/download/details.aspx?id=40855).

tooget dettagliate della Guida per qualsiasi cmdlet che viene visualizzato in questa esercitazione, il cmdlet Get-Help hello di utilizzo.

    Get-Help <cmdlet-name> -Detailed

Ad esempio, la Guida di tooget per hello `New-AzureRmRedisCache` cmdlet, digitare:

    Get-Help New-AzureRmRedisCache -Detailed

### <a name="how-tooconnect-tooother-clouds"></a>Come tooconnect tooother cloud
Ambiente hello predefinito Azure è `AzureCloud`, che rappresenta hello istanza globale cloud di Azure. tooconnect tooa istanza diversa, utilizzare hello `Add-AzureRmAccount` con hello `-Environment` o -`EnvironmentName` opzione della riga di comando con l'ambiente desiderato hello o nome dell'ambiente.

elenco di hello toosee degli ambienti disponibili, eseguire hello `Get-AzureRmEnvironment` cmdlet.

### <a name="tooconnect-toohello-azure-government-cloud"></a>tooconnect toohello Cloud di Azure per enti pubblici
tooconnect toohello Cloud di Azure per enti pubblici, utilizzare uno dei seguenti comandi hello.

    Add-AzureRMAccount -EnvironmentName AzureUSGovernment

oppure

    Add-AzureRmAccount -Environment (Get-AzureRmEnvironment -Name AzureUSGovernment)

toocreate una cache di hello Cloud di Azure per enti pubblici, utilizzare una delle posizioni seguenti hello.

* Governo degli Stati Uniti - Virginia
* Governo degli Stati Uniti - Iowa

Per ulteriori informazioni su hello Cloud di Azure per enti pubblici, vedere [Microsoft Azure per enti pubblici](https://azure.microsoft.com/features/gov/) e [Guida per sviluppatori di Microsoft Azure per enti pubblici](../azure-government-developer-guide.md).

### <a name="tooconnect-toohello-azure-china-cloud"></a>tooconnect toohello Cloud Cina di Azure
tooconnect toohello Cloud Cina di Azure, utilizzare uno dei seguenti comandi hello.

    Add-AzureRMAccount -EnvironmentName AzureChinaCloud

oppure

    Add-AzureRmAccount -Environment (Get-AzureRmEnvironment -Name AzureChinaCloud)

toocreate una cache di hello Cloud Cina di Azure, utilizzare una delle posizioni seguenti hello.

* Cina orientale
* Cina settentrionale

Per ulteriori informazioni su hello Cloud Cina di Azure, vedere [AzureChinaCloud per Azure gestito da 21Vianet in Cina](http://www.windowsazure.cn/).

### <a name="tooconnect-toomicrosoft-azure-germany"></a>tooconnect tooMicrosoft Azure in Germania
tooconnect tooMicrosoft Azure in Germania, utilizzare uno dei seguenti comandi hello.

    Add-AzureRMAccount -EnvironmentName AzureGermanCloud


oppure

    Add-AzureRmAccount -Environment (Get-AzureRmEnvironment -Name AzureGermanCloud)

toocreate una cache in Microsoft Azure in Germania, utilizzare una delle posizioni seguenti hello.

* Germania centrale
* Germania nord-orientale

Per altre informazioni su Microsoft Azure Germania, vedere [Microsoft Azure Germania](https://azure.microsoft.com/overview/clouds/germany/).

### <a name="properties-used-for-azure-redis-cache-powershell"></a>Proprietà usate per PowerShell nella Cache Redis di Azure 
Hello nella tabella seguente contiene le proprietà e le descrizioni per i parametri utilizzati durante la creazione e gestire le istanze di Cache Redis di Azure con Azure PowerShell.

| . | Descrizione | Default |
| --- | --- | --- |
| Nome |Nome della cache di hello | |
| Percorso |Percorso della cache di hello | |
| ResourceGroupName |Nome gruppo di risorse nella cache di hello quali toocreate | |
| Dimensione |dimensione Hello della cache di hello. I valori validi sono: P1, P2, P3, P4, C0, C1, C2, C3, C4, C5, C6, 250 MB, 1 GB, 2,5 GB, 6 GB, 13 GB, 26 GB, 53 GB |1 GB |
| ShardCount |numero di Hello di partizioni toocreate quando si crea una cache premium con clustering abilitato. I valori validi sono: 1, 2, 3, 4, 5, 6, 7, 8, 9, 10 | |
| SKU |Specifica hello SKU della cache di hello. I valori validi sono: Basic, Standard e Premium |Standard |
| RedisConfiguration |Specifica le impostazioni di configurazione di Redis. Per informazioni dettagliate su ogni impostazione, vedere l'esempio hello [RedisConfiguration proprietà](#redisconfiguration-properties) tabella. | |
| EnableNonSslPort |Indica se la porta non SSL hello è abilitata. |False |
| MaxMemoryPolicy |Questo parametro è stato deprecato, usare invece RedisConfiguration. | |
| StaticIP |Quando si ospita la cache in una rete virtuale, specifica l'indirizzo IP nella subnet hello per cache di hello. Se omesso, automaticamente dalla subnet hello viene scelto uno. | |
| Subnet |Quando si ospita la cache in una rete virtuale, specifica il nome di hello della subnet hello nella cache di hello quali toodeploy. | |
| VirtualNetwork |Quando si ospita la cache in una rete virtuale, specifica l'ID della risorsa hello hello rete virtuale nella cache di hello quali toodeploy. | |
| KeyType |Specifica la chiave di accesso tooregenerate durante il rinnovo di chiavi di accesso. Valori validi: Primario, Secondario | |

### <a name="redisconfiguration-properties"></a>Proprietà di RedisConfiguration
| Proprietà | Descrizione | Piani tariffari |
| --- | --- | --- |
| rdb-backup-enabled |Indica se la [persistenza dei dati Redis](cache-how-to-premium-persistence.md) è abilitata |Solo Premium |
| rdb-storage-connection-string |account di archiviazione toohello di stringa di connessione per Hello [Redis persistenza dei dati](cache-how-to-premium-persistence.md) |Solo Premium |
| rdb-backup-frequency |frequenza di backup per Hello [Redis persistenza dei dati](cache-how-to-premium-persistence.md) |Solo Premium |
| maxmemory-reserved |Configura hello [memoria riservata](cache-configure.md#maxmemory-policy-and-maxmemory-reserved) per i processi non cache |Standard e Premium |
| maxmemory-policy |Configura hello [criteri di rimozione](cache-configure.md#maxmemory-policy-and-maxmemory-reserved) per cache di hello |Tutti i piani tariffari |
| notify-keyspace-events |Configura le [notifiche keyspace](cache-configure.md#keyspace-notifications-advanced-settings) |Standard e Premium |
| hash-max-ziplist-entries |Configura l' [ottimizzazione della memoria](http://redis.io/topics/memory-optimization) per tipi di dati aggregati di piccole dimensioni |Standard e Premium |
| hash-max-ziplist-value |Configura l' [ottimizzazione della memoria](http://redis.io/topics/memory-optimization) per tipi di dati aggregati di piccole dimensioni |Standard e Premium |
| set-max-intset-entries |Configura l' [ottimizzazione della memoria](http://redis.io/topics/memory-optimization) per tipi di dati aggregati di piccole dimensioni |Standard e Premium |
| zset-max-ziplist-entries |Configura l' [ottimizzazione della memoria](http://redis.io/topics/memory-optimization) per tipi di dati aggregati di piccole dimensioni |Standard e Premium |
| zset-max-ziplist-value |Configura l' [ottimizzazione della memoria](http://redis.io/topics/memory-optimization) per tipi di dati aggregati di piccole dimensioni |Standard e Premium |
| database |Configura il numero di hello di database. Questa proprietà può essere configurata solo durante la creazione della cache. |Standard e Premium |

## <a name="toocreate-a-redis-cache"></a>toocreate una Cache Redis
Le nuove istanze di Cache Redis di Azure vengono create utilizzando hello [New AzureRmRedisCache](https://msdn.microsoft.com/library/azure/mt634517.aspx) cmdlet.

> [!IMPORTANT]
> Hello prima volta che si crea una cache Redis in una sottoscrizione utilizzando il portale di Azure, hello portale hello registra hello `Microsoft.Cache` dello spazio dei nomi per la sottoscrizione. Se si tenta hello toocreate innanzitutto Redis cache in una sottoscrizione tramite PowerShell, è innanzitutto necessario registrare tale spazio dei nomi utilizzando hello comando; seguente i cmdlet in caso contrario, ad esempio `New-AzureRmRedisCache` e `Get-AzureRmRedisCache` esito negativo.
> 
> `Register-AzureRmResourceProvider -ProviderNamespace "Microsoft.Cache"`
> 
> 

un elenco dei parametri disponibili e le relative descrizioni per toosee `New-AzureRmRedisCache`, eseguire hello il seguente comando.

    PS C:\> Get-Help New-AzureRmRedisCache -detailed

    NAME
        New-AzureRmRedisCache

    SYNOPSIS
        Creates a new redis cache.


    SYNTAX
        New-AzureRmRedisCache -Name <String> -ResourceGroupName <String> -Location <String> [-RedisVersion <String>]
        [-Size <String>] [-Sku <String>] [-MaxMemoryPolicy <String>] [-RedisConfiguration <Hashtable>] [-EnableNonSslPort
        <Boolean>] [-ShardCount <Integer>] [-VirtualNetwork <String>] [-Subnet <String>] [-StaticIP <String>]
        [<CommonParameters>]


    DESCRIPTION
        hello New-AzureRmRedisCache cmdlet creates a new redis cache.


    PARAMETERS
        -Name <String>
            Name of hello redis cache toocreate.

        -ResourceGroupName <String>
            Name of resource group in which toocreate hello redis cache.

        -Location <String>
            Location in which toocreate hello redis cache.

        -RedisVersion <String>
            RedisVersion is deprecated and will be removed in future release.

        -Size <String>
            Size of hello redis cache. hello default value is 1GB or C1. Possible values are P1, P2, P3, P4, C0, C1, C2, C3,
            C4, C5, C6, 250MB, 1GB, 2.5GB, 6GB, 13GB, 26GB, 53GB.

        -Sku <String>
            Sku of redis cache. hello default value is Standard. Possible values are Basic, Standard and Premium.

        -MaxMemoryPolicy <String>
            hello 'MaxMemoryPolicy' setting has been deprecated. Please use 'RedisConfiguration' setting tooset
            MaxMemoryPolicy. e.g. -RedisConfiguration @{"maxmemory-policy" = "allkeys-lru"}

        -RedisConfiguration <Hashtable>
            All Redis Configuration Settings. Few possible keys: rdb-backup-enabled, rdb-storage-connection-string,
            rdb-backup-frequency, maxmemory-reserved, maxmemory-policy, notify-keyspace-events, hash-max-ziplist-entries,
            hash-max-ziplist-value, set-max-intset-entries, zset-max-ziplist-entries, zset-max-ziplist-value, databases.

        -EnableNonSslPort <Boolean>
            EnableNonSslPort is used by Azure Redis Cache. If no value is provided, hello default value is false and the
            non-SSL port will be disabled. Possible values are true and false.

        -ShardCount <Integer>
            hello number of shards toocreate on a Premium Cluster Cache.

        -VirtualNetwork <String>
            hello exact ARM resource ID of hello virtual network toodeploy hello redis cache in. Example format: /subscriptions/{
            subid}/resourceGroups/{resourceGroupName}/providers/Microsoft.ClassicNetwork/VirtualNetworks/{vnetName}

        -Subnet <String>
            Required when deploying a redis cache inside an existing Azure Virtual Network.

        -StaticIP <String>
            Required when deploying a redis cache inside an existing Azure Virtual Network.

        <CommonParameters>
            This cmdlet supports hello common parameters: Verbose, Debug,
            ErrorAction, ErrorVariable, WarningAction, WarningVariable,
            OutBuffer, PipelineVariable, and OutVariable. For more information, see
            about_CommonParameters (http://go.microsoft.com/fwlink/?LinkID=113216).

toocreate una cache con i parametri predefiniti, eseguire hello comando seguente.

    New-AzureRmRedisCache -ResourceGroupName myGroup -Name mycache -Location "North Central US"

`ResourceGroupName`, `Name`, e `Location` sono parametri obbligatori, ma il resto di hello sono facoltativo e includono i valori predefiniti. Esecuzione hello precedente comando crea un'istanza di Cache Redis Azure SKU Standard con nome specificato hello, percorso e il gruppo di risorse, da 1 GB di dimensioni con la porta non SSL hello disabilitata.

toocreate una cache premium, specificare una dimensione di P1 (6 GB - 60 GB), P2 (13 GB - 130 GB), P3 (26 GB - 260 GB), o P4 (53 GB - 530 GB). tooenable clustering, specificare un numero di partizioni utilizzando hello `ShardCount` parametro. Hello esempio seguente viene creata una cache premium P1 con 3 partizioni. Una cache premium P1 è 6 GB di dimensioni e poiché sono state specificate tre partizioni hello dimensione totale è 18 GB (3 x 6 GB).

    New-AzureRmRedisCache -ResourceGroupName myGroup -Name mycache -Location "North Central US" -Sku Premium -Size P1 -ShardCount 3

i valori toospecify per hello `RedisConfiguration` parametro, racchiudere i valori hello `{}` come chiave/valore come coppie `@{"maxmemory-policy" = "allkeys-random", "notify-keyspace-events" = "KEA"}`. esempio Hello crea una cache standard di 1 GB con `allkeys-random` le notifiche di spazio delle chiavi e i criteri di maxmemory configurate con `KEA`. Per altre informazioni, vedere [Notifiche di Keyspace (impostazioni avanzate)](cache-configure.md#keyspace-notifications-advanced-settings) e [Criteri per la memoria](cache-configure.md#memory-policies).

    New-AzureRmRedisCache -ResourceGroupName myGroup -Name mycache -Location "North Central US" -RedisConfiguration @{"maxmemory-policy" = "allkeys-random", "notify-keyspace-events" = "KEA"}

<a name="databases"></a>

## <a name="tooconfigure-hello-databases-setting-during-cache-creation"></a>database hello tooconfigure impostazione durante la creazione della cache
Hello `databases` impostazione può essere configurata solo durante la creazione della cache. esempio Hello crea P3 premium (26 GB) di cache con i 48 database utilizzando hello [New AzureRmRedisCache](https://msdn.microsoft.com/library/azure/mt634517.aspx) cmdlet.

    New-AzureRmRedisCache -ResourceGroupName myGroup -Name mycache -Location "North Central US" -Sku Premium -Size P3 -RedisConfiguration @{"databases" = "48"}

Per ulteriori informazioni su hello `databases` proprietà, vedere [configurazione server di Cache Redis di Azure predefinito](cache-configure.md#default-redis-server-configuration). Per ulteriori informazioni sulla creazione di una cache di hello [New AzureRmRedisCache](https://msdn.microsoft.com/library/azure/mt634517.aspx) cmdlet, vedere hello precedente [toocreate una Cache Redis](#to-create-a-redis-cache) sezione.

## <a name="tooupdate-a-redis-cache"></a>tooupdate una cache Redis
Istanze di Cache Redis di Azure vengono aggiornate utilizzando hello [Set AzureRmRedisCache](https://msdn.microsoft.com/library/azure/mt634518.aspx) cmdlet.

un elenco dei parametri disponibili e le relative descrizioni per toosee `Set-AzureRmRedisCache`, eseguire hello il seguente comando.

    PS C:\> Get-Help Set-AzureRmRedisCache -detailed

    NAME
        Set-AzureRmRedisCache

    SYNOPSIS
        Set redis cache updatable parameters.

    SYNTAX
        Set-AzureRmRedisCache -Name <String> -ResourceGroupName <String> [-Size <String>] [-Sku <String>]
        [-MaxMemoryPolicy <String>] [-RedisConfiguration <Hashtable>] [-EnableNonSslPort <Boolean>] [-ShardCount
        <Integer>] [<CommonParameters>]

    DESCRIPTION
        hello Set-AzureRmRedisCache cmdlet sets redis cache parameters.

    PARAMETERS
        -Name <String>
            Name of hello redis cache tooupdate.

        -ResourceGroupName <String>
            Name of hello resource group for hello cache.

        -Size <String>
            Size of hello redis cache. hello default value is 1GB or C1. Possible values are P1, P2, P3, P4, C0, C1, C2, C3,
            C4, C5, C6, 250MB, 1GB, 2.5GB, 6GB, 13GB, 26GB, 53GB.

        -Sku <String>
            Sku of redis cache. hello default value is Standard. Possible values are Basic, Standard and Premium.

        -MaxMemoryPolicy <String>
            hello 'MaxMemoryPolicy' setting has been deprecated. Please use 'RedisConfiguration' setting tooset
            MaxMemoryPolicy. e.g. -RedisConfiguration @{"maxmemory-policy" = "allkeys-lru"}

        -RedisConfiguration <Hashtable>
            All Redis Configuration Settings. Few possible keys: rdb-backup-enabled, rdb-storage-connection-string,
            rdb-backup-frequency, maxmemory-reserved, maxmemory-policy, notify-keyspace-events, hash-max-ziplist-entries,
            hash-max-ziplist-value, set-max-intset-entries, zset-max-ziplist-entries, zset-max-ziplist-value.

        -EnableNonSslPort <Boolean>
            EnableNonSslPort is used by Azure Redis Cache. hello default value is null and no change will be made toothe
            currently configured value. Possible values are true and false.

        -ShardCount <Integer>
            hello number of shards toocreate on a Premium Cluster Cache.

        <CommonParameters>
            This cmdlet supports hello common parameters: Verbose, Debug,
            ErrorAction, ErrorVariable, WarningAction, WarningVariable,
            OutBuffer, PipelineVariable, and OutVariable. For more information, see
            about_CommonParameters (http://go.microsoft.com/fwlink/?LinkID=113216).

Hello `Set-AzureRmRedisCache` cmdlet può essere utilizzato tooupdate proprietà, ad esempio `Size`, `Sku`, `EnableNonSslPort`, hello e `RedisConfiguration` valori. 

Hello il comando seguente aggiornamenti hello criteri di maxmemory per Cache Redis hello denominato myCache.

    Set-AzureRmRedisCache -ResourceGroupName "myGroup" -Name "myCache" -RedisConfiguration @{"maxmemory-policy" = "allkeys-random"}

<a name="scale"></a>

## <a name="tooscale-a-redis-cache"></a>tooscale una cache Redis
`Set-AzureRmRedisCache`può essere un'istanza di cache Redis di Azure quando hello tooscale utilizzati `Size`, `Sku`, o `ShardCount` si modificano le proprietà. 

> [!NOTE]
> Scalabilità di una cache tramite PowerShell, è soggetto toohello stessi limiti e alle linee guida di scalabilità di una cache di hello portale di Azure. È possibile ridimensionare tooa diverso livello di prezzo con hello seguenti restrizioni.
> 
> * Non è possibile scalare da un piano tariffario superiore tooa livello inferiore a livello di prezzo.
> * Non è possibile scalare da un **Premium** cache verso il basso tooa **Standard** o **base** della cache.
> * Non è possibile scalare da un **Standard** cache verso il basso tooa **base** della cache.
> * È possibile scalare da un **base** cache tooa **Standard** cache ma è Impossibile modificare la dimensione di hello in hello contemporaneamente. Se è necessario dimensioni diverse, è possibile eseguire una successiva dimensione toohello desiderato operazione.
> * Non è possibile scalare da un **base** memorizzare nella cache direttamente tooa **Premium** cache. È necessario applicare la scalabilità da **base** troppo**Standard** in un'unica operazione di ridimensionamento e quindi da **Standard** troppo**Premium** una scalabilità successivi operazione.
> * Non è possibile scalare da una dimensione maggiore verso il basso toohello **C0 (250 MB)** dimensioni.
> 
> Per ulteriori informazioni, vedere [la modalità di Cache Redis di Azure di tooScale](cache-how-to-scale.md).
> 
> 

Hello esempio seguente viene illustrato come tooscale una cache denominata `myCache` tooa 2,5 GB cache. Si noti che questo comando funziona sia con una cache Basic che una cache Standard.

    Set-AzureRmRedisCache -ResourceGroupName myGroup -Name myCache -Size 2.5GB

Dopo che viene eseguito questo comando, viene restituito lo stato di hello della cache di hello (simile toocalling `Get-AzureRmRedisCache`). Si noti che hello `ProvisioningState` è `Scaling`.

    PS C:\> Set-AzureRmRedisCache -Name myCache -ResourceGroupName myGroup -Size 2.5GB


    Name               : mycache
    Id                 : /subscriptions/12ad12bd-abdc-2231-a2ed-a2b8b246bbad4/resourceGroups/mygroup/providers/Mi
                         crosoft.Cache/Redis/mycache
    Location           : South Central US
    Type               : Microsoft.Cache/Redis
    HostName           : mycache.redis.cache.windows.net
    Port               : 6379
    ProvisioningState  : Scaling
    SslPort            : 6380
    RedisConfiguration : {[maxmemory-policy, volatile-lru], [maxmemory-reserved, 150], [notify-keyspace-events, KEA],
                         [maxmemory-delta, 150]...}
    EnableNonSslPort   : False
    RedisVersion       : 3.0
    Size               : 1GB
    Sku                : Standard
    ResourceGroupName  : mygroup
    PrimaryKey         : ....
    SecondaryKey       : ....
    VirtualNetwork     :
    Subnet             :
    StaticIP           :
    TenantSettings     : {}
    ShardCount         :

Una volta completata l'operazione di ridimensionamento hello, hello `ProvisioningState` cambia troppo`Succeeded`. Se è necessario toomake un'operazione di ridimensionamento successiva, ad esempio la modifica da tooStandard base e quindi modifica la dimensione di hello, è necessario attendere hello precedente operazione è stata completata o viene visualizzato un seguente toohello simile di errore.

    Set-AzureRmRedisCache : Conflict: hello resource '...' is not in a stable state, and is currently unable tooaccept hello update request.

## <a name="tooget-information-about-a-redis-cache"></a>informazioni tooget su una cache Redis
È possibile recuperare informazioni su una cache di hello [Get AzureRmRedisCache](https://msdn.microsoft.com/library/azure/mt634514.aspx) cmdlet.

un elenco dei parametri disponibili e le relative descrizioni per toosee `Get-AzureRmRedisCache`, eseguire hello il seguente comando.

    PS C:\> Get-Help Get-AzureRmRedisCache -detailed

    NAME
        Get-AzureRmRedisCache

    SYNOPSIS
        Gets details about a single cache or all caches in hello specified resource group or all caches in hello current
        subscription.

    SYNTAX
        Get-AzureRmRedisCache [-Name <String>] [-ResourceGroupName <String>] [<CommonParameters>]

    DESCRIPTION
        hello Get-AzureRmRedisCache cmdlet gets hello details about a cache or caches depending on input parameters. If both
        ResourceGroupName and Name parameters are provided then Get-AzureRmRedisCache will return details about the
        specific cache name provided.

        If only ResourceGroupName is provided than it will return details about all caches in hello specified resource group.

        If no parameters are given than it will return details about all caches hello current subscription.

    PARAMETERS
        -Name <String>
            hello name of hello cache. When this parameter is provided along with ResourceGroupName, Get-AzureRmRedisCache
            returns hello details for hello cache.

        -ResourceGroupName <String>
            hello name of hello resource group that contains hello cache or caches. If ResourceGroupName is provided with Name
            then Get-AzureRmRedisCache returns hello details of hello cache specified by Name. If only hello ResourceGroup
            parameter is provided, then details for all caches in hello resource group are returned.

        <CommonParameters>
            This cmdlet supports hello common parameters: Verbose, Debug,
            ErrorAction, ErrorVariable, WarningAction, WarningVariable,
            OutBuffer, PipelineVariable, and OutVariable. For more information, see
            about_CommonParameters (http://go.microsoft.com/fwlink/?LinkID=113216).

informazioni tooreturn su tutte le cache nella sottoscrizione corrente hello, eseguire `Get-AzureRmRedisCache` senza parametri.

    Get-AzureRmRedisCache

informazioni tooreturn su tutte le cache in un gruppo di risorse specifico, eseguire `Get-AzureRmRedisCache` con hello `ResourceGroupName` parametro.

    Get-AzureRmRedisCache -ResourceGroupName myGroup

informazioni tooreturn su una cache specifica, eseguire `Get-AzureRmRedisCache` con hello `Name` parametro contenente il nome di hello della cache di hello e hello `ResourceGroupName` parametro con il gruppo di risorse hello contenente tale cache.

    PS C:\> Get-AzureRmRedisCache -Name myCache -ResourceGroupName myGroup

    Name               : mycache
    Id                 : /subscriptions/12ad12bd-abdc-2231-a2ed-a2b8b246bbad4/resourceGroups/myGroup/providers/Mi
                         crosoft.Cache/Redis/mycache
    Location           : South Central US
    Type               : Microsoft.Cache/Redis
    HostName           : mycache.redis.cache.windows.net
    Port               : 6379
    ProvisioningState  : Succeeded
    SslPort            : 6380
    RedisConfiguration : {[maxmemory-policy, volatile-lru], [maxmemory-reserved, 62], [notify-keyspace-events, KEA],
                         [maxclients, 1000]...}
    EnableNonSslPort   : False
    RedisVersion       : 3.0
    Size               : 1GB
    Sku                : Standard
    ResourceGroupName  : myGroup
    VirtualNetwork     :
    Subnet             :
    StaticIP           :
    TenantSettings     : {}
    ShardCount         :

## <a name="tooretrieve-hello-access-keys-for-a-redis-cache"></a>chiavi di accesso di hello tooretrieve per una cache Redis
tooretrieve hello tasti di scelta per la cache, è possibile utilizzare hello [Get AzureRmRedisCacheKey](https://msdn.microsoft.com/library/azure/mt634516.aspx) cmdlet.

un elenco dei parametri disponibili e le relative descrizioni per toosee `Get-AzureRmRedisCacheKey`, eseguire hello il seguente comando.

    PS C:\> Get-Help Get-AzureRmRedisCacheKey -detailed

    NAME
        Get-AzureRmRedisCacheKey

    SYNOPSIS
        Gets hello accesskeys for hello specified redis cache.


    SYNTAX
        Get-AzureRmRedisCacheKey -Name <String> -ResourceGroupName <String> [<CommonParameters>]

    DESCRIPTION
        hello Get-AzureRmRedisCacheKey cmdlet gets hello access keys for hello specified cache.

    PARAMETERS
        -Name <String>
            Name of hello redis cache.

        -ResourceGroupName <String>
            Name of hello resource group for hello cache.

        <CommonParameters>
            This cmdlet supports hello common parameters: Verbose, Debug,
            ErrorAction, ErrorVariable, WarningAction, WarningVariable,
            OutBuffer, PipelineVariable, and OutVariable. For more information, see
            about_CommonParameters (http://go.microsoft.com/fwlink/?LinkID=113216).

hello tooretrieve chiavi per la cache, chiamata hello `Get-AzureRmRedisCacheKey` cmdlet e passare il nome di hello della cache di hello Nome hello del gruppo di risorse che contiene una cache di hello.

    PS C:\> Get-AzureRmRedisCacheKey -Name myCache -ResourceGroupName myGroup

    PrimaryKey   : b2wdt43sfetlju4hfbryfnregrd9wgIcc6IA3zAO1lY=
    SecondaryKey : ABhfB757JgjIgt785JgKH9865eifmekfnn649303JKL=

## <a name="tooregenerate-access-keys-for-your-redis-cache"></a>tooregenerate chiavi di accesso per la cache Redis
tooregenerate hello tasti di scelta per la cache, è possibile utilizzare hello [New AzureRmRedisCacheKey](https://msdn.microsoft.com/library/azure/mt634512.aspx) cmdlet.

un elenco dei parametri disponibili e le relative descrizioni per toosee `New-AzureRmRedisCacheKey`, eseguire hello il seguente comando.

    PS C:\> Get-Help New-AzureRmRedisCacheKey -detailed

    NAME
        New-AzureRmRedisCacheKey

    SYNOPSIS
        Regenerates hello access key of a redis cache.

    SYNTAX
        New-AzureRmRedisCacheKey -Name <String> -ResourceGroupName <String> -KeyType <String> [-Force] [<CommonParameters>]

    DESCRIPTION
        hello New-AzureRmRedisCacheKey cmdlet regenerate hello access key of a redis cache.

    PARAMETERS
        -Name <String>
            Name of hello redis cache.

        -ResourceGroupName <String>
            Name of hello resource group for hello cache.

        -KeyType <String>
            Specifies whether tooregenerate hello primary or secondary access key. Possible values are Primary or Secondary.

        -Force
            When hello Force parameter is provided, hello specified access key is regenerated without any confirmation prompts.

        <CommonParameters>
            This cmdlet supports hello common parameters: Verbose, Debug,
            ErrorAction, ErrorVariable, WarningAction, WarningVariable,
            OutBuffer, PipelineVariable, and OutVariable. For more information, see
            about_CommonParameters (http://go.microsoft.com/fwlink/?LinkID=113216).

chiave tooregenerate hello primaria o secondaria per la cache, chiamata hello `New-AzureRmRedisCacheKey` cmdlet e passare hello nome, il gruppo di risorse e specificare il parametro `Primary` o `Secondary` per hello `KeyType` parametro. Nell'esempio seguente di hello, chiave di accesso secondaria hello per una cache viene rigenerato.

    PS C:\> New-AzureRmRedisCacheKey -Name myCache -ResourceGroupName myGroup -KeyType Secondary

    Confirm
    Are you sure you want tooregenerate Secondary key for redis cache 'myCache'?
    [Y] Yes  [N] No  [S] Suspend  [?] Help (default is "Y"): Y


    PrimaryKey   : b2wdt43sfetlju4hfbryfnregrd9wgIcc6IA3zAO1lY=
    SecondaryKey : c53hj3kh4jhHjPJk8l0jji785JgKH9865eifmekfnn6=

## <a name="toodelete-a-redis-cache"></a>toodelete una cache Redis
toodelete una cache Redis, utilizzare hello [Remove AzureRmRedisCache](https://msdn.microsoft.com/library/azure/mt634515.aspx) cmdlet.

un elenco dei parametri disponibili e le relative descrizioni per toosee `Remove-AzureRmRedisCache`, eseguire hello il seguente comando.

    PS C:\> Get-Help Remove-AzureRmRedisCache -detailed

    NAME
        Remove-AzureRmRedisCache

    SYNOPSIS
        Remove redis cache if exists.

    SYNTAX
        Remove-AzureRmRedisCache -Name <String> -ResourceGroupName <String> [-Force] [-PassThru] [<CommonParameters>

    DESCRIPTION
        hello Remove-AzureRmRedisCache cmdlet removes a redis cache if it exists.

    PARAMETERS
        -Name <String>
            Name of hello redis cache tooremove.

        -ResourceGroupName <String>
            Name of hello resource group of hello cache tooremove.

        -Force
            When hello Force parameter is provided, hello cache is removed without any confirmation prompts.

        -PassThru
            By default Remove-AzureRmRedisCache removes hello cache and does not return any value. If hello PassThru par
            is provided then Remove-AzureRmRedisCache returns a boolean value indicating hello success of hello operatio

        <CommonParameters>
            This cmdlet supports hello common parameters: Verbose, Debug,
            ErrorAction, ErrorVariable, WarningAction, WarningVariable,
            OutBuffer, PipelineVariable, and OutVariable. For more information, see
            about_CommonParameters (http://go.microsoft.com/fwlink/?LinkID=113216).

Nell'esempio seguente di hello, hello cache denominata `myCache` viene rimosso.

    PS C:\> Remove-AzureRmRedisCache -Name myCache -ResourceGroupName myGroup

    Confirm
    Are you sure you want tooremove redis cache 'myCache'?
    [Y] Yes  [N] No  [S] Suspend  [?] Help (default is "Y"): Y


## <a name="tooimport-a-redis-cache"></a>tooimport una cache Redis
È possibile importare dati in un'istanza di Cache Redis di Azure utilizzando hello `Import-AzureRmRedisCache` cmdlet.

> [!IMPORTANT]
> La funzionalità Importazione/Esportazione è disponibile solo per le cache del [piano Premium](cache-premium-tier-intro.md) . Per altre informazioni sull'importazione/esportazione, vedere [Importare ed esportare dati in Cache Redis di Azure](cache-how-to-import-export-data.md).
> 
> 

un elenco dei parametri disponibili e le relative descrizioni per toosee `Import-AzureRmRedisCache`, eseguire hello il seguente comando.

    PS C:\> Get-Help Import-AzureRmRedisCache -detailed

    NAME
        Import-AzureRmRedisCache

    SYNOPSIS
        Import data from blobs tooAzure Redis Cache.


    SYNTAX
        Import-AzureRmRedisCache -Name <String> -ResourceGroupName <String> -Files <String[]> [-Format <String>] [-Force]
        [-PassThru] [<CommonParameters>]


    DESCRIPTION
        hello Import-AzureRmRedisCache cmdlet imports data from hello specified blobs into Azure Redis Cache.


    PARAMETERS
        -Name <String>
            hello name of hello cache.

        -ResourceGroupName <String>
            hello name of hello resource group that contains hello cache.

        -Files <String[]>
            SAS urls of blobs whose content should be imported into hello cache.

        -Format <String>
            Format for hello blob.  Currently "rdb" is hello only supported, with other formats expected in hello future.

        -Force
            When hello Force parameter is provided, import will be performed without any confirmation prompts.

        -PassThru
            By default Import-AzureRmRedisCache imports data in cache and does not return any value. If hello PassThru
            parameter is provided then Import-AzureRmRedisCache returns a boolean value indicating hello success of the
            operation.

        <CommonParameters>
            This cmdlet supports hello common parameters: Verbose, Debug,
            ErrorAction, ErrorVariable, WarningAction, WarningVariable,
            OutBuffer, PipelineVariable, and OutVariable. For more information, see
            about_CommonParameters (http://go.microsoft.com/fwlink/?LinkID=113216).


Hello comando riportato di seguito Importa i dati da blob hello specificato dall'uri di firma di accesso condiviso hello in Cache Redis di Azure.

    PS C:\>Import-AzureRmRedisCache -ResourceGroupName "resourceGroupName" -Name "cacheName" -Files @("https://mystorageaccount.blob.core.windows.net/mycontainername/blobname?sv=2015-04-05&sr=b&sig=caIwutG2uDa0NZ8mjdNJdgOY8%2F8mhwRuGNdICU%2B0pI4%3D&st=2016-05-27T00%3A00%3A00Z&se=2016-05-28T00%3A00%3A00Z&sp=rwd") -Force

## <a name="tooexport-a-redis-cache"></a>tooexport una cache Redis
È possibile esportare dati da un'istanza di Cache Redis di Azure utilizzando hello `Export-AzureRmRedisCache` cmdlet.

> [!IMPORTANT]
> La funzionalità Importazione/Esportazione è disponibile solo per le cache del [piano Premium](cache-premium-tier-intro.md) . Per altre informazioni sull'importazione/esportazione, vedere [Importare ed esportare dati in Cache Redis di Azure](cache-how-to-import-export-data.md).
> 
> 

un elenco dei parametri disponibili e le relative descrizioni per toosee `Export-AzureRmRedisCache`, eseguire hello il seguente comando.

    PS C:\> Get-Help Export-AzureRmRedisCache -detailed

    NAME
        Export-AzureRmRedisCache

    SYNOPSIS
        Exports data from Azure Redis Cache tooa specified container.


    SYNTAX
        Export-AzureRmRedisCache -Name <String> -ResourceGroupName <String> -Prefix <String> -Container <String> [-Format
        <String>] [-PassThru] [<CommonParameters>]


    DESCRIPTION
        hello Export-AzureRmRedisCache cmdlet exports data from Azure Redis Cache tooa specified container.


    PARAMETERS
        -Name <String>
            hello name of hello cache.

        -ResourceGroupName <String>
            hello name of hello resource group that contains hello cache.

        -Prefix <String>
            Prefix toouse for blob names.

        -Container <String>
            SAS url of container where data should be exported.

        -Format <String>
            Format for hello blob.  Currently "rdb" is hello only supported, with other formats expected in hello future.

        -PassThru
            By default Export-AzureRmRedisCache does not return any value. If hello PassThru parameter is provided
            then Export-AzureRmRedisCache returns a boolean value indicating hello success of hello operation.

        <CommonParameters>
            This cmdlet supports hello common parameters: Verbose, Debug,
            ErrorAction, ErrorVariable, WarningAction, WarningVariable,
            OutBuffer, PipelineVariable, and OutVariable. For more information, see
            about_CommonParameters (http://go.microsoft.com/fwlink/?LinkID=113216).


Hello seguente comando Esporta i dati da un'istanza di Cache Redis di Azure in contenitore hello specificato dall'uri SAS hello.

        PS C:\>Export-AzureRmRedisCache -ResourceGroupName "resourceGroupName" -Name "cacheName" -Prefix "blobprefix"
        -Container "https://mystorageaccount.blob.core.windows.net/mycontainer?sv=2015-04-05&sr=c&sig=HezZtBZ3DURmEGDduauE7
        pvETY4kqlPI8JCNa8ATmaw%3D&st=2016-05-27T00%3A00%3A00Z&se=2016-05-28T00%3A00%3A00Z&sp=rwdl"

## <a name="tooreboot-a-redis-cache"></a>tooreboot una cache Redis
È possibile riavviare l'istanza di Cache Redis di Azure utilizzando hello `Reset-AzureRmRedisCache` cmdlet.

> [!IMPORTANT]
> La funzionalità di riavvio è disponibile solo per le cache del [piano Premium](cache-premium-tier-intro.md) . Per altre informazioni sul riavvio della cache, vedere [Come amministrare Cache Redis di Azure - Riavviare](cache-administration.md#reboot).
> 
> 

un elenco dei parametri disponibili e le relative descrizioni per toosee `Reset-AzureRmRedisCache`, eseguire hello il seguente comando.

    PS C:\> Get-Help Reset-AzureRmRedisCache -detailed

    NAME
        Reset-AzureRmRedisCache

    SYNOPSIS
        Reboot specified node(s) of an Azure Redis Cache instance.


    SYNTAX
        Reset-AzureRmRedisCache -Name <String> -ResourceGroupName <String> -RebootType <String> [-ShardId <Integer>]
        [-Force] [-PassThru] [<CommonParameters>]


    DESCRIPTION
        hello Reset-AzureRmRedisCache cmdlet reboots hello specified node(s) of an Azure Redis Cache instance.


    PARAMETERS
        -Name <String>
            hello name of hello cache.

        -ResourceGroupName <String>
            hello name of hello resource group that contains hello cache.

        -RebootType <String>
            Which node tooreboot. Possible values are "PrimaryNode", "SecondaryNode", "AllNodes".

        -ShardId <Integer>
            Which shard tooreboot when rebooting a premium cache with clustering enabled.

        -Force
            When hello Force parameter is provided, reset will be performed without any confirmation prompts.

        -PassThru
            By default Reset-AzureRmRedisCache does not return any value. If hello PassThru parameter is provided
            then Reset-AzureRmRedisCache returns a boolean value indicating hello success of hello operation.

        <CommonParameters>
            This cmdlet supports hello common parameters: Verbose, Debug,
            ErrorAction, ErrorVariable, WarningAction, WarningVariable,
            OutBuffer, PipelineVariable, and OutVariable. For more information, see
            about_CommonParameters (http://go.microsoft.com/fwlink/?LinkID=113216).


il comando seguente Hello riavvia entrambi i nodi di hello specificato della cache.

        PS C:\>Reset-AzureRmRedisCache -ResourceGroupName "resourceGroupName" -Name "cacheName" -RebootType "AllNodes"
        -Force


## <a name="next-steps"></a>Passaggi successivi
toolearn ulteriori informazioni sull'utilizzo di Windows PowerShell con Azure, vedere hello seguenti risorse:

* [Documentazione del cmdlet della cache Redis di Azure su MSDN](https://msdn.microsoft.com/library/azure/mt634513.aspx)
* [Azure Resource Manager Cmdlets](http://go.microsoft.com/fwlink/?LinkID=394765): informazioni sui cmdlet di hello toouse nel modulo di gestione risorse di Azure hello.
* [Utilizzo risorse gruppi toomanage le risorse di Azure](../azure-resource-manager/resource-group-template-deploy-portal.md): informazioni su come toocreate e gestire gruppi di risorse nel portale di Azure hello.
* [Blog di Azure](http://blogs.msdn.com/windowsazure): informazioni sulle nuove funzionalità di Azure.
* [Blog di Windows PowerShell](http://blogs.msdn.com/powershell): informazioni sulle nuove funzionalità di Windows PowerShell.
* [Blog "Hey, Scripting Blog](http://blogs.technet.com/b/heyscriptingguy/): ottenere suggerimenti reali da hello community di Windows PowerShell.


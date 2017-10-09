---
title: Cache Redis di Azure mediante Azure CLI aaaManage | Documenti Microsoft
description: "Informazioni su come tooinstall hello Azure CLI su qualsiasi piattaforma, come toouse è tooconnect tooyour account Azure e come toocreate e gestire una cache Redis da hello CLI di Azure."
services: redis-cache
documentationcenter: 
author: steved0x
manager: douge
editor: 
ms.assetid: 964ff245-859d-4bc1-bccf-62e4b3c1169f
ms.service: cache
ms.workload: tbd
ms.tgt_pltfrm: cache-redis
ms.devlang: na
ms.topic: article
ms.date: 01/23/2017
ms.author: sdanie
ms.openlocfilehash: e8ee30090133e6b4edea93dcd13fd171e75989bd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="how-toocreate-and-manage-azure-redis-cache-using-hello-azure-command-line-interface-azure-cli"></a>Come toocreate e gestire Cache Redis di Azure utilizzando hello interfaccia della riga di comando di Azure (Azure CLI)
> [!div class="op_single_selector"]
> * [PowerShell](cache-howto-manage-redis-cache-powershell.md)
> * [Interfaccia della riga di comando di Azure](cache-manage-cli.md)
>
>

Hello CLI di Azure è un ottimo modo toomanage dell'infrastruttura di Azure da qualsiasi piattaforma. In questo articolo illustra come toocreate e gestire le istanze di Cache Redis di Azure mediante Azure CLI hello.

> [!NOTE]
> Questo articolo riguarda tooa precedente versione di CLI di Azure. Per script di esempio 2.0 CLI di Azure più recenti hello, vedere [esempi per cache Redis di Azure CLI](cli-samples.md).
> 
> 

## <a name="prerequisites"></a>Prerequisiti
toocreate e gestire le istanze di Cache Redis di Azure utilizzando l'interfaccia CLI di Azure, è necessario completare hello alla procedura seguente.

* È necessario disporre di un account Azure. Se non è disponibile, è possibile creare un [account gratuito](https://azure.microsoft.com/pricing/free-trial/) in pochi istanti.
* [Installare hello Azure CLI](../cli-install-nodejs.md).
* Connettere l'installazione di CLI di Azure con un account di Azure personale, o con un lavoro o scuola account Azure e accedere da hello CLI di Azure utilizzando hello `azure login` comando. toounderstand hello differenze e scegliere, vedere [connettersi tooan sottoscrizione di Azure da hello interfaccia della riga di comando di Azure (Azure CLI)](../xplat-cli-connect.md).
* Prima di eseguire uno dei seguenti comandi hello, passare hello CLI di Azure in modalità di gestione delle risorse eseguendo hello `azure config mode arm` comando. Per ulteriori informazioni, vedere [toomanage CLI di Azure hello Azure usare risorse e gruppi di risorse](../xplat-cli-azure-resource-manager.md).

## <a name="redis-cache-properties"></a>Proprietà di Cache Redis
le proprietà seguenti Hello vengono utilizzate durante la creazione e aggiornamento di istanze di Cache Redis.

| Proprietà | Switch | Descrizione |
| --- | --- | --- |
| name |-n, --name |Nome della Cache Redis hello. |
| gruppo di risorse |-g, --resource-group |Nome del gruppo di risorse hello. |
| location |-l, --location |Cache toocreate del percorso. |
| size |-z, --size |Dimensione della Cache Redis hello. Valori validi: [C0, C1, C2, C3, C4, C5, C6, P1, P2, P3, P4] |
| sku |-x, sku: |SKU di Redis. Deve essere uno di: [Basic, Standard, Premium] |
| EnableNonSslPort |-e, --enable-non-ssl-port |Proprietà EnableNonSslPort di hello Cache Redis. Aggiungere questo flag se si desidera tooenable hello Non SSL porta per la cache |
| Configurazione di Redis |-c, --redis-configuration |Configurazione di Redis. Immettere qui una stringa in formato JSON di chiavi di configurazione e valori. Formato: "{"":"","":""}" |
| Configurazione di Redis |-f, --redis-configuration-file |Configurazione di Redis. Immettere il percorso di hello di un file contenente le chiavi di configurazione e i valori qui. Formato per la voce del file hello: {"": "","": ""} |
| Numero di partizioni |-r, --shard-count |Numero di partizioni toocreate in una Cache di Cluster Premium con il clustering. |
| Rete virtuale |-v, --virtual-network |Quando la cache in una rete virtuale, di hosting specifica hello esatta ARM ID della risorsa hello toodeploy di rete virtuale hello redis cache. Formato di esempio: /subscriptions/{subid}/resourceGroups/{resourceGroupName}/Microsoft.ClassicNetwork/VirtualNetworks/vnet1 |
| tipo di chiave |-t, --key-type |Tipo di chiave toorenew. Valori validi: [primario, secondario] |
| StaticIP |-p, --static-ip <static-ip> |Quando si ospita la cache in una rete virtuale, specifica l'indirizzo IP nella subnet hello per cache di hello. Se omesso, automaticamente dalla subnet hello viene scelto uno. |
| Subnet |t, --subnet <subnet> |Quando si ospita la cache in una rete virtuale, specifica il nome di hello della subnet hello nella cache di hello quali toodeploy. |
| VirtualNetwork |-v, --virtual-network <virtual-network> |Quando la cache in una rete virtuale, di hosting specifica hello esatta ARM ID della risorsa hello toodeploy di rete virtuale hello redis cache. Formato di esempio: /subscriptions/{subid}/resourceGroups/{resourceGroupName}/Microsoft.ClassicNetwork/VirtualNetworks/vnet1 |
| Subscription |-s, --subscription |Identificatore della sottoscrizione Hello. |

## <a name="see-all-redis-cache-commands"></a>Vedere tutti i comandi di Cache Redis
toosee tutti i comandi di Cache Redis e i relativi parametri, utilizzare hello `azure rediscache -h` comando.

    C:\>azure rediscache -h
    help:    Commands toomanage your Azure Redis Cache(s)
    help:
    help:    Create a Redis Cache
    help:      rediscache create [--name <name> --resource-group <resource-group> --location <location> [options]]
    help:
    help:    Delete an existing Redis Cache
    help:      rediscache delete [--name <name> --resource-group <resource-group> ]
    help:
    help:    List all Redis Caches within your Subscription or Resource Group
    help:      rediscache list [options]
    help:
    help:    Show properties of an existing Redis Cache
    help:      rediscache show [--name <name> --resource-group <resource-group>]
    help:
    help:    Change settings of an existing Redis Cache
    help:      rediscache set [--name <name> --resource-group <resource-group> --redis-configuration <redis-configuration>/--redis-configuration-file <redisConfigurationFile>]
    help:
    help:    Renew hello authentication key for an existing Redis Cache
    help:      rediscache renew-key [--name <name> --resource-group <resource-group> ]
    help:
    help:    Lists Primary and Secondary key of an existing Redis Cache
    help:      rediscache list-keys [--name <name> --resource-group <resource-group>]
    help:
    help:    Options:
    help:      -h, --help  output usage information
    help:
    help:    Current Mode: arm (Azure Resource Management)

## <a name="create-a-redis-cache"></a>Creare una Cache Redis
toocreate una Cache Redis, utilizzare hello comando seguente:

    azure rediscache create [--name <name> --resource-group <resource-group> --location <location> [options]]

Per ulteriori informazioni su questo comando, eseguire hello `azure rediscache create -h` comando.

    C:\>azure rediscache create -h
    help:    Create a Redis Cache
    help:
    help:    Usage: rediscache create [--name <name> --resource-group <resource-group> --location <location> [options]]
    help:
    help:    Options:
    help:      -h, --help                                               output usage information
    help:      -v, --verbose                                            use verbose output
    help:      -vv                                                      more verbose with debug output
    help:      --json                                                   use json output
    help:      -n, --name <name>                                        Name of hello Redis Cache.
    help:      -g, --resource-group <resource-group>                    Name of hello Resource Group
    help:      -l, --location <location>                                Location toocreate cache.
    help:      -z, --size <size>                                        Size of hello Redis Cache. Valid values: [C0, C1, C2, C3, C4, C5, C6, P1, P2, P3, P4]
    help:      -x, --sku <sku>                                          Redis SKU. Should be one of : [Basic, Standard, Premium]
    help:      -e, --enable-non-ssl-port                                EnableNonSslPort property of hello Redis Cache. Add this flag if you want tooenable hello Non SSL Port for your cache
    help:      -c, --redis-configuration <redis-configuration>          Redis Configuration. Enter a JSON formatted string of configuration keys and values here. Format:"{"<key1>":"<value1>","<key2>":"<value2>"}"
    help:      -f, --redis-configuration-file <redisConfigurationFile>  Redis Configuration. Enter hello path of a file containing configuration keys and values here. Format for hello file entry: {"<key1>":"<value1>","<key2>":"<value2>"}
    help:      -r, --shard-count <shard-count>                          Number of Shards toocreate on a Premium Cluster Cache
    help:      -v, --virtual-network <virtual-network>                  hello exact ARM resource ID of hello virtual network toodeploy hello redis cache in. Example format: /subscriptions/{subid}/resourceGroups/{resourceGroupName}/Microsoft.ClassicNetwork/VirtualNetworks/vnet1
    help:      -t, --subnet <subnet>                                    Required when deploying a redis cache inside an existing Azure Virtual Network
    help:      -p, --static-ip <static-ip>                              Required when deploying a redis cache inside an existing Azure Virtual Network
    help:      -s, --subscription <id>                                  hello subscription identifier
    help:
    help:    Current Mode: arm (Azure Resource Management)

## <a name="delete-an-existing-redis-cache"></a>Eliminare una Cache Redis esistente
toodelete una Cache Redis, utilizzare hello comando seguente:

    azure rediscache delete [--name <name> --resource-group <resource-group> ]

Per ulteriori informazioni su questo comando, eseguire hello `azure rediscache delete -h` comando.

    C:\>azure rediscache delete -h
    help:    Delete an existing Redis Cache
    help:
    help:    Usage: rediscache delete [--name <name> --resource-group <resource-group> ]
    help:
    help:    Options:
    help:      -h, --help                             output usage information
    help:      -v, --verbose                          use verbose output
    help:      -vv                                    more verbose with debug output
    help:      --json                                 use json output
    help:      -n, --name <name>                      Name of hello Redis Cache.
    help:      -g, --resource-group <resource-group>  Name of hello Resource Group under which hello cache exists
    help:      -s, --subscription <subscription>      hello subscription identifier
    help:
    help:    Current Mode: arm (Azure Resource Management)

## <a name="list-all-redis-caches-within-your-subscription-or-resource-group"></a>Elenco di tutte le Cache Redis all'interno della sottoscrizione o di un gruppo di risorse
utilizzare tutte le cache Redis all'interno della sottoscrizione o un gruppo di risorse, toolist hello il seguente comando:

    azure rediscache list [options]

Per ulteriori informazioni su questo comando, eseguire hello `azure rediscache list -h` comando.

    C:\>azure rediscache list -h
    help:    List all Redis Caches within your Subscription or Resource Group
    help:
    help:    Usage: rediscache list [options]
    help:
    help:    Options:
    help:      -h, --help                             output usage information
    help:      -v, --verbose                          use verbose output
    help:      -vv                                    more verbose with debug output
    help:      --json                                 use json output
    help:      -g, --resource-group <resource-group>  Name of hello Resource Group
    help:      -s, --subscription <subscription>      hello subscription identifier
    help:
    help:    Current Mode: arm (Azure Resource Management)

## <a name="show-properties-of-an-existing-redis-cache"></a>Visualizzare le proprietà di una Cache Redis esistente
proprietà tooshow di una Cache Redis esistente, utilizzare hello comando seguente:

    azure rediscache show [--name <name> --resource-group <resource-group>]

Per ulteriori informazioni su questo comando, eseguire hello `azure rediscache show -h` comando.

    C:\>azure rediscache show -h
    help:    Show properties of an existing Redis Cache
    help:
    help:    Usage: rediscache show [--name <name> --resource-group <resource-group>]
    help:
    help:    Options:
    help:      -h, --help                             output usage information
    help:      -v, --verbose                          use verbose output
    help:      -vv                                    more verbose with debug output
    help:      --json                                 use json output
    help:      -n, --name <name>                      Name of hello Redis Cache.
    help:      -g, --resource-group <resource-group>  Name of hello Resource Group
    help:      -s, --subscription <subscription>      hello subscription identifier
    help:
    help:    Current Mode: arm (Azure Resource Management)

<a name="scale"></a>

## <a name="change-settings-of-an-existing-redis-cache"></a>Modificare le impostazioni di una Cache Redis esistente
impostazioni toochange di una Cache Redis esistente, utilizzare hello comando seguente:

    azure rediscache set [--name <name> --resource-group <resource-group> --redis-configuration <redis-configuration>/--redis-configuration-file <redisConfigurationFile>]

Per ulteriori informazioni su questo comando, eseguire hello `azure rediscache set -h` comando.

    C:\>azure rediscache set -h
    help:    Change settings of an existing Redis Cache
    help:
    help:    Usage: rediscache set [--name <name> --resource-group <resource-group> --redis-configuration <redis-configuration>/--redis-configuration-file <redisConfigurationFile>]
    help:
    help:    Options:
    help:      -h, --help                                               output usage information
    help:      -v, --verbose                                            use verbose output
    help:      -vv                                                      more verbose with debug output
    help:      --json                                                   use json output
    help:      -n, --name <name>                                        Name of hello Redis Cache.
    help:      -g, --resource-group <resource-group>                    Name of hello Resource Group
    help:      -c, --redis-configuration <redis-configuration>          Redis Configuration. Enter a JSON formatted string of configuration keys and values here.
    help:      -f, --redis-configuration-file <redisConfigurationFile>  Redis Configuration. Enter hello path of a file containing configuration keys and values here.
    help:      -s, --subscription <subscription>                        hello subscription identifier
    help:
    help:    Current Mode: arm (Azure Resource Management)

## <a name="renew-hello-authentication-key-for-an-existing-redis-cache"></a>Rinnova la chiave di autenticazione hello per una Cache Redis esistente
chiave di autenticazione hello toorenew per una Redis Cache esistente, utilizzare hello comando seguente:

    azure rediscache renew-key [--name <name> --resource-group <resource-group> --key-type <key-type>]

Specificare `Primary` o `Secondary` per `key-type`.

Per ulteriori informazioni su questo comando, eseguire hello `azure rediscache renew-key -h` comando.

    C:\>azure rediscache renew-key -h
    help:    Renew hello authentication key for an existing Redis Cache
    help:
    help:    Usage: rediscache renew-key [--name <name> --resource-group <resource-group> ]
    help:
    help:    Options:
    help:      -h, --help                             output usage information
    help:      -v, --verbose                          use verbose output
    help:      -vv                                    more verbose with debug output
    help:      --json                                 use json output
    help:      -n, --name <name>                      Name of hello Redis Cache.
    help:      -g, --resource-group <resource-group>  Name of hello Resource Group under which cache exists
    help:      -t, --key-type <key-type>              type of key toorenew. Valid values are: 'Primary', 'Secondary'.
    help:      -s, --subscription <subscription>      hello subscription identifier
    help:
    help:    Current Mode: arm (Azure Resource Management)

## <a name="list-primary-and-secondary-keys-of-an-existing-redis-cache"></a>Chiavi di elenco primario e secondario di una Cache Redis esistente
le chiavi primari e secondari toolist di una Cache Redis esistente, utilizzare hello comando seguente:

    azure rediscache list-keys [--name <name> --resource-group <resource-group>]

Per ulteriori informazioni su questo comando, eseguire hello `azure rediscache list-keys -h` comando.

    C:\>azure rediscache list-keys -h
    help:    Lists Primary and Secondary key of an existing Redis Cache
    help:
    help:    Usage: rediscache list-keys [--name <name> --resource-group <resource-group>]
    help:
    help:    Options:
    help:      -h, --help                             output usage information
    help:      -v, --verbose                          use verbose output
    help:      -vv                                    more verbose with debug output
    help:      --json                                 use json output
    help:      -n, --name <name>                      Name of hello Redis Cache.
    help:      -g, --resource-group <resource-group>  Name of hello Resource Group under which Cache exists
    help:      -s, --subscription <subscription>      hello subscription identifier
    help:
    help:    Current Mode: arm (Azure Resource Management)

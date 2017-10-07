---
title: aaaTroubleshoot connessioni - CLI di Azure 1.0 e il Gateway di rete virtuale di Azure | Documenti Microsoft
description: Questa pagina viene illustrato come toouse hello Watcher di rete di Azure risolvere i problemi di Azure CLI 1.0
services: network-watcher
documentationcenter: na
author: georgewallace
manager: timlt
editor: 
ms.assetid: 2838bc61-b182-4da8-8533-27db8fdbd177
ms.service: network-watcher
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 06/19/2017
ms.author: gwallace
ms.openlocfilehash: a0511689d773f9c7216b0fe5470e27f754eb600b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshoot-virtual-network-gateway-and-connections-using-azure-network-watcher-azure-cli-10"></a>Risolvere i problemi relativi al gateway di rete virtuale e alle connessioni tramite l'interfaccia della riga di comando 1.0 di Azure in Network Watcher di Azure

> [!div class="op_single_selector"]
> - [Portale](network-watcher-troubleshoot-manage-portal.md)
> - [PowerShell](network-watcher-troubleshoot-manage-powershell.md)
> - [Interfaccia della riga di comando 1.0](network-watcher-troubleshoot-manage-cli-nodejs.md)
> - [Interfaccia della riga di comando 2.0](network-watcher-troubleshoot-manage-cli.md)
> - [API REST](network-watcher-troubleshoot-manage-rest.md)

Watcher di rete fornisce numerose funzionalità toounderstanding in relazione le risorse di rete in Azure. Una di queste funzionalità è la risoluzione dei problemi riscontrati con le risorse. Risoluzione dei problemi di risorse può essere chiamato tramite il portale di hello, PowerShell, CLI o API REST. Quando viene chiamato, Watcher di rete Controlla integrità hello di un Gateway di rete virtuale o una connessione e restituisce i risultati della ricerca.

Questo articolo usa l'interfaccia della riga di comando di Azure 1.0 multipiattaforma, disponibile per Windows, Mac e Linux. 

## <a name="before-you-begin"></a>Prima di iniziare

Questo scenario si presuppone che si sono già stati seguiti i passaggi di hello in [creare un controllo di rete](network-watcher-create.md) toocreate Watcher di rete.

Per un elenco dei tipi di gateway supportati, consultare i [tipi di gateway supportati](/network-watcher-troubleshoot-overview.md#supported-gateway-types).

## <a name="overview"></a>Panoramica

Risoluzione dei problemi di risorse consente di hello risolvere i problemi che si verificano con gateway di rete virtuale e le connessioni. Quando viene effettuata una richiesta di risoluzione dei problemi tooresource, i registri vengono eseguite query e controllato. Una volta completato controllo, vengono restituiti risultati hello. Richieste di risorse, le richieste di risoluzione dei problemi sono a esecuzione prolungata, che potrebbe richiedere più minuti tooreturn un risultato. i log di Hello dalla risoluzione dei problemi vengono archiviati in un contenitore in un account di archiviazione specificato.

## <a name="retrieve-a-virtual-network-gateway-connection"></a>Recuperare una connessione e un gateway di rete virtuale

In questo esempio la risoluzione dei problemi delle risorse viene eseguita su una connessione. È anche possibile passare il comando a un gateway di rete virtuale. Hello cmdlet riportato di seguito sono elencati hello connessioni vpn in un gruppo di risorse.

```azurecli
azure network vpn-connection list -g resourceGroupName
```

È anche possibile eseguire hello comando toosee connessioni hello in una sottoscrizione.

```azurecli
azure network vpn-connection list -s subscription
```

Dopo aver creato il nome di hello della connessione di hello, è possibile eseguire questo comando tooget relativi Id di risorsa:

```azurecli
azure network vpn-connection show -g resourceGroupName -n connectionName
```

## <a name="create-a-storage-account"></a>Creare un account di archiviazione

Risoluzione dei problemi di risorse restituisce i dati sull'integrità hello della risorsa hello, consentono inoltre di salvare i registri tooa storage account toobe esaminato. In questo passaggio viene creato un account di archiviazione. È anche possibile usare un account di archiviazione già esistente.

1. Creare account di archiviazione hello

    ```azurecli
    azure storage account create -n storageAccountName -l location -g resourceGroupName
    ```

1. Ottiene le chiavi account di archiviazione hello

    ```azurecli
    azure storage account keys list storageAccountName -g resourcegroupName
    ```

1. Creare il contenitore di hello

    ```azurecli
    azure storage container create --account-name storageAccountName -g resourcegroupName --account-key {storageAccountKey} --container logs
    ```

## <a name="run-network-watcher-resource-troubleshooting"></a>Eseguire il comando per la risoluzione dei problemi delle risorse di Network Watcher

Risolvere i problemi relativi alle risorse con hello `network watcher troubleshoot` cmdlet. Viene passato a gruppo di risorse di hello cmdlet hello, nome di hello Watcher di rete, Id di connessione hello, hello hello hello Id dell'account di archiviazione hello e hello di hello percorso toohello blob toostore di risolvere i risultati in.

```azurecli
azure network watcher troubleshoot -g resourceGroupName -n networkWatcherName -t connectionId -i storageId -p storagePath
```

Dopo aver eseguito i cmdlet di hello, Watcher di rete esamina integrità hello tooverify delle risorse di hello. Restituisce i risultati di hello toohello shell e archivia i log dei risultati di hello in hello account di archiviazione specificato.

## <a name="understanding-hello-results"></a>Informazioni sui risultati hello

testo dell'azione Hello vengono fornite indicazioni generali su come tooresolve hello problema. Se è possibile eseguire un'azione per il problema di hello, viene fornito un collegamento con informazioni aggiuntive. In caso di hello in cui è presente alcun altro materiale sussidiario, risposta hello fornisce hello url tooopen un caso di supporto.  Per ulteriori informazioni sulle proprietà hello di risposta hello e cosa è inclusa, visitare [Panoramica monitoraggio risolvere i problemi di rete](network-watcher-troubleshoot-overview.md)

Per istruzioni sul download di file dall'account di archiviazione di azure, consultare troppo[Introduzione all'archiviazione Blob di Azure usando .NET](../storage/blobs/storage-dotnet-how-to-use-blobs.md). Un altro strumento che può essere usato è Storage Explorer. Ulteriori informazioni su soluzioni di archiviazione sono reperibile qui in hello seguente collegamento: [Esplora archivi](http://storageexplorer.com/)

## <a name="next-steps"></a>Passaggi successivi

Se le impostazioni sono state modificate che arresta la connettività VPN, vedere [gestire gruppi di sicurezza di rete](../virtual-network/virtual-network-manage-nsg-arm-portal.md) tootrack verso il basso hello rete sicurezza e gruppo di regole di sicurezza che possono essere in questione.

---
title: aaaGet avviato con il DNS di Azure mediante Azure CLI 1.0 | Documenti Microsoft
description: Informazioni su come toocreate un DNS zona e questo record in DNS di Azure. Si tratta toocreate una Guida dettagliata e gestire i prima zona DNS e il record utilizzando hello Azure CLI 1.0.
services: dns
documentationcenter: na
author: jtuliani
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: fb0aa0a6-d096-4d6a-b2f6-eda1c64f6182
ms.service: dns
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 03/10/2017
ms.author: jonatul
ms.openlocfilehash: e200c848ad261160e593306dbb8a1d92bf26880b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-azure-dns-using-azure-cli-10"></a>Introduzione a DNS Azure con l'interfaccia della riga di comando di Azure 1.0

> [!div class="op_single_selector"]
> * [Portale di Azure](dns-getstarted-portal.md)
> * [PowerShell](dns-getstarted-powershell.md)
> * [Interfaccia della riga di comando di Azure 1.0](dns-getstarted-cli-nodejs.md)
> * [Interfaccia della riga di comando di Azure 2.0](dns-getstarted-cli.md)

Questo articolo illustra hello passaggi toocreate la prima zona DNS e record utilizzando hello multipiattaforma CLI di Azure 1.0, disponibile per Windows, Mac e Linux. È anche possibile eseguire questi passaggi tramite il portale di Azure hello o Azure PowerShell.

Una zona DNS è utilizzato toohost hello DNS record per un particolare dominio. toostart hosting del dominio DNS di Azure, è necessario toocreate una zona DNS per il nome di dominio. Ogni record DNS per il dominio viene quindi creato all'interno di questa zona DNS. Infine, toopublish della zona DNS toohello Internet, server dei nomi tooconfigure hello è necessario per il dominio hello. Ogni passaggio è illustrato di seguito.

Queste istruzioni presuppongono aver già installato e connesso tooAzure CLI 1.0. Per ulteriori informazioni, vedere [come toomanage DNS zone mediante Azure CLI 1.0](dns-operations-dnszones-cli-nodejs.md).

## <a name="create-hello-resource-group"></a>Creare il gruppo di risorse hello

Prima di creare una zona DNS hello, un gruppo di risorse viene creato toocontain zona di DNS hello. Hello seguito è riportato il comando hello.

```azurecli
azure group create --name MyResourceGroup --location "West US"
```

## <a name="create-a-dns-zone"></a>Creare una zona DNS

Una zona DNS viene creata utilizzando hello `azure network dns zone create` comando. Guida di toosee per questo comando, digitare `azure network dns zone create -h`.

esempio Hello crea una zona DNS denominata *contoso.com* nel gruppo di risorse hello chiamato *MyResourceGroup*. Utilizzare l'esempio toocreate hello una zona DNS, sostituendo i valori hello per uso personale.

```azurecli
azure network dns zone create MyResourceGroup contoso.com
```


## <a name="create-a-dns-record"></a>Creare un record DNS

toocreate un record DNS, utilizzare hello `azure network dns record-set add-record` comando. Per altre informazioni, vedere `azure network dns record-set add-record -h`.

Hello seguente viene creato un record con il nome relativo hello "www" hello "contoso.com", nel gruppo di risorse "MyResourceGroup" zona di DNS. nome completo di Hello del set di record hello è "www.contoso.com". tipo di record Hello è "A", con l'indirizzo IP "1.2.3.4" e viene utilizzato un periodo TTL predefinito di 3600 secondi (1 ora).

```azurecli
azure network dns record-set add-record MyResourceGroup contoso.com www A -a 1.2.3.4
```

Per altri tipi di record, per i set di record con più di un record, per i valori di durata (TTL) alternativi e toomodify i record esistenti, vedere [record DNS di gestire e set di record mediante hello Azure CLI 1.0](dns-operations-recordsets-cli-nodejs.md).


## <a name="view-records"></a>Visualizzare i record

i record DNS di hello toolist nella zona, utilizzare:

```azurecli
azure network dns record-set list MyResourceGroup contoso.com
```


## <a name="update-name-servers"></a>Aggiornare i server dei nomi

Dopo aver soddisfatto che la zona DNS e i record sono stati impostati correttamente, è necessario tooconfigure il nome di dominio toouse server dei nomi DNS di Azure hello. In questo modo altri utenti nel hello Internet toofind i record DNS.

Server dei nomi per l'area Hello forniti tramite hello `azure network dns zone show` comando:

```azurecli
azure network dns zone show MyResourceGroup contoso.com

info:    Executing command network dns zone show
+ Looking up hello dns zone "contoso.com"
data:    Id                              : /subscriptions/a385a691-bd93-41b0-8084-8213ebc5bff7/resourceGroups/myresourcegroup/providers/Microsoft.Network/dnszones/contoso.com
data:    Name                            : contoso.com
data:    Type                            : Microsoft.Network/dnszones
data:    Location                        : global
data:    Number of record sets           : 3
data:    Max number of record sets       : 5000
data:    Name servers:
data:        ns1-01.azure-dns.com.
data:        ns2-01.azure-dns.net.
data:        ns3-01.azure-dns.org.
data:        ns4-01.azure-dns.info.
data:    Tags                            :
info:    network dns zone show command OK
```

Questi server dei nomi deve essere configurato con hello registrar (in cui è stato acquistato il nome di dominio hello). Registrar offrirà hello opzione tooset dei server dei nomi per il dominio hello hello. Per ulteriori informazioni, vedere [delegare il tooAzure di dominio DNS](dns-domain-delegation.md).

## <a name="delete-all-resources"></a>Eliminare tutte le risorse
 
toodelete tutte le risorse create in questo articolo, hello take seguente passaggio:

```azurecli
azure group delete --name MyResourceGroup
```

## <a name="next-steps"></a>Passaggi successivi

toolearn ulteriori informazioni su DNS di Azure, vedere [Panoramica di DNS di Azure](dns-overview.md).

toolearn informazioni su gestione delle zone DNS di DNS di Azure, vedere [le zone DNS di gestione in DNS di Azure mediante Azure CLI 1.0](dns-operations-dnszones-cli-nodejs.md).

toolearn informazioni su gestione dei record DNS nel sistema DNS di Azure, vedere [Manage DNS record e record imposta nel sistema DNS di Azure mediante Azure CLI 1.0](dns-operations-recordsets-cli-nodejs.md).


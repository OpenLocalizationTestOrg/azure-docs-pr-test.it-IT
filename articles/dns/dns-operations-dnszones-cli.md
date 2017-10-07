---
title: zone DNS di Azure - CLI di Azure 2.0 aaaManage DNS | Documenti Microsoft
description: "È possibile gestire le zone DNS usando l'interfaccia della riga di comando Azure 2.0. Questo articolo illustra come tooupdate, eliminare e creare le zone DNS in DNS di Azure."
services: dns
documentationcenter: na
author: georgewallace
manager: timlt
ms.assetid: 8ab63bc4-5135-4ed8-8c0b-5f0712b9afed
ms.service: dns
ms.devlang: azurecli
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/27/2017
ms.author: gwallace
ms.openlocfilehash: 3945a558b2db3490e50678d8395a47e55a85c8fc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="how-toomanage-dns-zones-in-azure-dns-using-hello-azure-cli-20"></a>Come toomanage zone DNS di Azure utilizzando hello Azure CLI 2.0

> [!div class="op_single_selector"]
> * [Portale](dns-operations-dnszones-portal.md)
> * [PowerShell](dns-operations-dnszones.md)
> * [Interfaccia della riga di comando di Azure 1.0](dns-operations-dnszones-cli-nodejs.md)
> * [Interfaccia della riga di comando di Azure 2.0](dns-operations-dnszones-cli.md)


Questa guida viene spiegato come toomanage zone DNS utilizzando hello multipiattaforma CLI di Azure, che è disponibile per Windows, Mac e Linux. È inoltre possibile gestire le zone DNS utilizzando [Azure PowerShell](dns-operations-dnszones.md) o hello portale di Azure.

## <a name="cli-versions-toocomplete-hello-task"></a>Attività hello toocomplete versioni CLI

È possibile completare l'attività hello utilizzando una delle seguenti versioni CLI hello:

* [Azure CLI 1.0](dns-operations-dnszones-cli-nodejs.md) -nostri CLI per hello classic e risorse Gestione modelli di distribuzione.
* [Azure CLI 2.0](dns-operations-dnszones-cli.md) -la prossima generazione CLI per modello di distribuzione di gestione risorse hello.

## <a name="introduction"></a>Introduzione

[!INCLUDE [dns-create-zone-about](../../includes/dns-create-zone-about-include.md)]

## <a name="set-up-azure-cli-20-for-azure-dns"></a>Configurare l'interfaccia della riga di comando di Azure 2.0 per DNS di Azure

### <a name="before-you-begin"></a>Prima di iniziare

Verificare di aver hello seguenti prima di iniziare la configurazione.

* Una sottoscrizione di Azure. Se non si ha una sottoscrizione di Azure, è possibile attivare i [vantaggi per i sottoscrittori di MSDN](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/) oppure iscriversi per ottenere un [account gratuito](https://azure.microsoft.com/pricing/free-trial/).

* Installare hello l'ultima versione di hello Azure CLI 2.0, disponibile per Windows, Linux o Mac. Altre informazioni sono disponibile all'indirizzo [installazione hello Azure CLI 2.0](https://docs.microsoft.com/en-us/cli/azure/install-az-cli2).

### <a name="sign-in-tooyour-azure-account"></a>Accedi tooyour account Azure

Aprire una finestra della console ed eseguire l'autenticazione con le credenziali. Per ulteriori informazioni, vedere il Log in tooAzure da hello CLI di Azure

```
az login
```

### <a name="select-hello-subscription"></a>Selezionare la sottoscrizione hello

Controllare le sottoscrizioni di hello per account hello.

```
az account list
```

Scegliere quali di toouse le sottoscrizioni di Azure.

```azurecli
az account set --subscription "subscription name"
```

### <a name="create-a-resource-group"></a>Creare un gruppo di risorse

Gestione risorse di Azure richiede che tutti i gruppi di risorse specifichino un percorso Viene utilizzato come percorso predefinito di hello per le risorse in tale gruppo di risorse. Tuttavia, poiché tutte le risorse DNS sono globali, non è regionale, scelta hello del percorso del gruppo di risorse ha alcun impatto su DNS di Azure.

Se si usa un gruppo di risorse esistente, è possibile ignorare questo passaggio.

```azurecli
az group create --name myresourcegroup --location "West US"
```

## <a name="getting-help"></a>Risorse della Guida

Avviano tutti i comandi CLI 2.0 relative tooAzure DNS con `az network dns`. La Guida è disponibile per ogni comando utilizzando hello `--help` opzione (forma breve `-h`).  ad esempio:

```azurecli
az network dns --help
az network dns zone --help
az network dns zone create --help
```

## <a name="create-a-dns-zone"></a>Creare una zona DNS

Una zona DNS viene creata utilizzando hello `az network dns zone create` comando. Per altre informazioni, vedere `az network dns zone create -h`.

esempio Hello crea una zona DNS denominata *contoso.com* nel gruppo di risorse hello chiamato *MyResourceGroup*:

```azurecli
az network dns zone create --resource-group MyResourceGroup --name contoso.com
```

### <a name="toocreate-a-dns-zone-with-tags"></a>toocreate una zona DNS con i tag

Hello esempio seguente viene illustrato come della zona DNS toocreate con due [tag Azure Resource Manager](dns-zones-records.md#tags), *progetto = demo* e *env = test*, utilizzando hello `--tags` parametro (forma breve `-t`):

```azurecli
az network dns zone create --resource-group MyResourceGroup --name contoso.com --tags "project=demo" "env=test"
```

## <a name="get-a-dns-zone"></a>Ottenere una zona DNS

tooretrieve una zona DNS, utilizzare `az network dns zone show`. Per altre informazioni, vedere `az network dns zone show --help`.

esempio Hello restituisce zona DNS hello *contoso.com* e i dati dal gruppo di risorse associati *MyResourceGroup*. 

```azurecli
az network dns zone show --resource-group myresourcegroup --name contoso.com
```

Hello di esempio seguente è riportata la risposta hello.

```json
{
  "etag": "00000002-0000-0000-3d4d-64aa3689d201",
  "id": "/subscriptions/147a22e9-2356-4e56-b3de-1f5842ae4a3b/resourceGroups/myresourcegroup/providers/Microsoft.Network/dnszones/contoso.com",
  "location": "global",
  "maxNumberOfRecordSets": 5000,
  "name": "contoso.com",
  "nameServers": [
    "ns1-04.azure-dns.com.",
    "ns2-04.azure-dns.net.",
    "ns3-04.azure-dns.org.",
    "ns4-04.azure-dns.info."
  ],
  "numberOfRecordSets": 4,
  "resourceGroup": "myresourcegroup",
  "tags": {},
  "type": "Microsoft.Network/dnszones"
}
```

Si noti che i record DNS non vengono restituiti da `az network dns zone show`. Utilizzare i record DNS toolist, `az network dns record-set list`.


## <a name="list-dns-zones"></a>Elencare le zone DNS

Utilizzare le zone DNS tooenumerate, `az network dns zone list`. Per altre informazioni, vedere `az network dns zone list --help`.

Gruppo di risorse specificando hello sono elencate solo le zone nel gruppo di risorse hello:

```azurecli
az network dns zone list --resource-group MyResourceGroup
```

L'omissione di gruppo di risorse hello Elenca tutte le zone nella sottoscrizione hello:

```azurecli
az network dns zone list 
```

## <a name="update-a-dns-zone"></a>Aggiornare una zona DNS

Le modifiche tooa possibile creare la risorsa di zona DNS mediante `az network dns zone update`. Per altre informazioni, vedere `az network dns zone update --help`.

Questo comando consente di aggiornare set di record DNS hello zona hello (vedere [come i record DNS tooManage](dns-operations-recordsets-cli.md)). È tooupdate utilizzati solo le proprietà della risorsa di zona hello stesso. Queste proprietà sono attualmente limitata toohello [Azure Resource Manager 'tag'](dns-zones-records.md#tags) per la risorsa di zona hello.

Hello esempio seguente viene illustrato come tooupdate hello tag in una zona DNS. i tag Hello esistenti vengono sostituiti da hello valore specificato.

```azurecli
az network dns zone update --resource-group myresourcegroup --name contoso.com --set tags.team=support
```

## <a name="delete-a-dns-zone"></a>Eliminare una zona DNS

Le zone DNS possono essere eliminate usando `az network dns zone delete`. Per altre informazioni, vedere `az network dns zone delete --help`.

> [!NOTE]
> L'eliminazione di una zona DNS elimina inoltre tutti i record DNS nella zona hello. Questa operazione non può essere annullata. Se zona DNS hello è in uso, con zone hello services avrà esito negativo quando viene eliminata hello.
>
>tooprotect l'eliminazione accidentale di zona, vedere [come tooprotect DNS zone e record](dns-protect-zones-recordsets.md).

Questo comando richiede una conferma. Hello facoltativo `--yes` commutatore Elimina questa richiesta.

Hello esempio seguente viene illustrato come toodelete hello zona *contoso.com* dal gruppo di risorse *MyResourceGroup*.

```azurecli
az network dns zone delete --resource-group myresourcegroup --name contoso.com
```

## <a name="next-steps"></a>Passaggi successivi

Informazioni su come troppo[gestire set di record e i record](dns-getstarted-create-recordset-cli.md) nella zona DNS.

Informazioni su come troppo[delegare il tooAzure di dominio DNS](dns-domain-delegation.md).


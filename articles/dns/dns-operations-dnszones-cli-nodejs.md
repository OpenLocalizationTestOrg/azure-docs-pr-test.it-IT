---
title: zone DNS di Azure - CLI di Azure 1.0 aaaManage DNS | Documenti Microsoft
description: "È possibile gestire le zone DNS usando l'interfaccia della riga di comando Azure 1.0. Questo articolo illustra come tooupdate, eliminare e creare le zone DNS in DNS di Azure."
services: dns
documentationcenter: na
author: georgewallace
manager: timlt
ms.assetid: 8ab63bc4-5135-4ed8-8c0b-5f0712b9afed
ms.service: dns
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 12/21/2016
ms.author: gwallace
ms.openlocfilehash: cb9790cc46626ef7f38a43edb57511104fe6057e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="how-toomanage-dns-zones-in-azure-dns-using-hello-azure-cli-10"></a>Come toomanage zone DNS di Azure utilizzando hello Azure CLI 1.0

> [!div class="op_single_selector"]
> * [Portale](dns-operations-dnszones-portal.md)
> * [PowerShell](dns-operations-dnszones.md)
> * [Interfaccia della riga di comando di Azure 1.0](dns-operations-dnszones-cli-nodejs.md)
> * [Interfaccia della riga di comando di Azure 2.0](dns-operations-dnszones-cli.md)

Questa guida viene spiegato come toomanage zone DNS utilizzando hello multipiattaforma CLI di Azure 1.0, disponibile per Windows, Mac e Linux. È inoltre possibile gestire le zone DNS utilizzando [Azure PowerShell](dns-operations-dnszones.md) o hello portale di Azure.

## <a name="cli-versions-toocomplete-hello-task"></a>Attività hello toocomplete versioni CLI

È possibile completare l'attività hello utilizzando una delle seguenti versioni CLI hello:

* [Azure CLI 1.0](dns-operations-dnszones-cli-nodejs.md) -nostri CLI per hello classic e risorse Gestione modelli di distribuzione.
* [Azure CLI 2.0](dns-operations-dnszones-cli.md) -la prossima generazione CLI per modello di distribuzione di gestione risorse hello.

## <a name="introduction"></a>Introduzione

[!INCLUDE [dns-create-zone-about](../../includes/dns-create-zone-about-include.md)]

[!INCLUDE [dns-cli-setup](../../includes/dns-cli-setup-include.md)]

## <a name="getting-help"></a>Risorse della Guida

Avviano tutti i comandi CLI 1.0 relative tooAzure DNS con `azure network dns`. La Guida è disponibile per ogni comando utilizzando hello `--help` opzione (forma breve `-h`).  ad esempio:

```azurecli
azure network dns -h
azure network dns zone -h
azure network dns zone create -h
```

## <a name="create-a-dns-zone"></a>Creare una zona DNS

Una zona DNS viene creata utilizzando hello `azure network dns zone create` comando. Per altre informazioni, vedere `azure network dns zone create -h`.

esempio Hello crea una zona DNS denominata *contoso.com* nel gruppo di risorse hello chiamato *MyResourceGroup*:

```azurecli
azure network dns zone create MyResourceGroup contoso.com
```

### <a name="toocreate-a-dns-zone-with-tags"></a>toocreate una zona DNS con i tag

Hello esempio seguente viene illustrato come della zona DNS toocreate con due [tag Azure Resource Manager](dns-zones-records.md#tags), *progetto = demo* e *env = test*, utilizzando hello `--tags` parametro (forma breve `-t`):

```azurecli
azure network dns zone create MyResourceGroup contoso.com -t "project=demo";"env=test"
```

## <a name="get-a-dns-zone"></a>Ottenere una zona DNS

tooretrieve una zona DNS, utilizzare `azure network dns zone show`. Per altre informazioni, vedere `azure network dns zone show -h`.

esempio Hello restituisce zona DNS hello *contoso.com* e i dati dal gruppo di risorse associati *MyResourceGroup*. 

```azurecli
azure network dns zone show MyResourceGroup contoso.com
```

Hello di esempio seguente è riportata la risposta hello.

```
info:    Executing command network dns zone show
+ Looking up hello dns zone "contoso.com"
data:    Id                              : /subscriptions/.../contoso.com
data:    Name                            : contoso.com
data:    Type                            : Microsoft.Network/dnszones
data:    Location                        : global
data:    Number of record sets           : 2
data:    Max number of record sets       : 5000
data:    Name servers:
data:        ns1-01.azure-dns.com.
data:        ns2-01.azure-dns.net.
data:        ns3-01.azure-dns.org.
data:        ns4-01.azure-dns.info.
data:    Tags                            : project=demo;env=test
info:    network dns zone show command OK
```

Si noti che i record DNS non vengono restituiti da `azure network dns zone show`. Utilizzare i record DNS toolist, `azure network dns record-set list`.


## <a name="list-dns-zones"></a>Elencare le zone DNS

Utilizzare le zone DNS tooenumerate, `azure network dns zone list`. Per altre informazioni, vedere `azure network dns zone list -h`.

Gruppo di risorse specificando hello sono elencate solo le zone nel gruppo di risorse hello:

```azurecli
azure network dns zone list MyResourceGroup
```

L'omissione di gruppo di risorse hello Elenca tutte le zone nella sottoscrizione hello:

```azurecli
azure network dns zone list 
```

## <a name="update-a-dns-zone"></a>Aggiornare una zona DNS

Le modifiche tooa possibile creare la risorsa di zona DNS mediante `azure network dns zone set`. Per altre informazioni, vedere `azure network dns zone set -h`.

Questo comando consente di aggiornare set di record DNS hello zona hello (vedere [come i record DNS tooManage](dns-operations-recordsets-cli-nodejs.md)). È tooupdate utilizzati solo le proprietà della risorsa di zona hello stesso. Queste proprietà sono attualmente limitata toohello [Azure Resource Manager 'tag'](dns-zones-records.md#tags) per la risorsa di zona hello.

Hello esempio seguente viene illustrato come tooupdate hello tag in una zona DNS. i tag Hello esistenti vengono sostituiti da hello valore specificato.

```azurecli
azure network dns zone set MyResourceGroup contoso.com -t "team=support"
```

## <a name="delete-a-dns-zone"></a>Eliminare una zona DNS

Le zone DNS possono essere eliminate usando `azure network dns zone delete`. Per altre informazioni, vedere `azure network dns zone delete -h`.

> [!NOTE]
> L'eliminazione di una zona DNS elimina inoltre tutti i record DNS nella zona hello. Questa operazione non può essere annullata. Se zona DNS hello è in uso, con zone hello services avrà esito negativo quando viene eliminata hello.
>
>tooprotect l'eliminazione accidentale di zona, vedere [come tooprotect DNS zone e record](dns-protect-zones-recordsets.md).

Questo comando richiede una conferma. Hello facoltativo `--quiet` passare (forma breve `-q`) Elimina questa richiesta.

Hello esempio seguente viene illustrato come toodelete hello zona *contoso.com* dal gruppo di risorse *MyResourceGroup*.

```azurecli
azure network dns zone delete MyResourceGroup contoso.com
```

## <a name="next-steps"></a>Passaggi successivi

Informazioni su come troppo[gestire set di record e i record](dns-getstarted-create-recordset-cli-nodejs.md) nella zona DNS.

Informazioni su come troppo[delegare il tooAzure di dominio DNS](dns-domain-delegation.md).


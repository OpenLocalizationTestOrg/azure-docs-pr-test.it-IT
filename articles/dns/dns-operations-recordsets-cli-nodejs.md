---
title: i record DNS aaaManage DNS di Azure utilizzando hello Azure CLI 1.0 | Documenti Microsoft
description: Gestione dei set di record e dei record DNS in DNS di Azure quando si ospita il dominio in DNS di Azure. Tutti i comandi dell'interfaccia della riga di comando 1.0 per le operazioni sui set di record e i record.
services: dns
documentationcenter: na
author: jtuliani
manager: carmonm
ms.assetid: 5356a3a5-8dec-44ac-9709-0c2b707f6cb5
ms.service: dns
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 12/20/2016
ms.author: jonatul
ms.openlocfilehash: 1f01450b0839f712cb1d96be318766bac581fea1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="manage-dns-records-in-azure-dns-using-hello-azure-cli-10"></a>Gestire i record DNS nel sistema DNS di Azure mediante Azure CLI 1.0 hello

> [!div class="op_single_selector"]
> * [Portale di Azure](dns-operations-recordsets-portal.md)
> * [Interfaccia della riga di comando di Azure 1.0](dns-operations-recordsets-cli-nodejs.md)
> * [Interfaccia della riga di comando di Azure 2.0](dns-operations-recordsets-cli.md)
> * [PowerShell](dns-operations-recordsets.md)

Questo articolo illustra come i record DNS toomanage per la zona DNS mediante hello multipiattaforma Azure interfaccia della riga di comando (CLI), che è disponibile per Windows, Mac e Linux. È inoltre possibile gestire i record DNS utilizzando [Azure PowerShell](dns-operations-recordsets.md) o hello [portale di Azure](dns-operations-recordsets-portal.md).

## <a name="cli-versions-toocomplete-hello-task"></a>Attività hello toocomplete versioni CLI

È possibile completare l'attività hello utilizzando una delle seguenti versioni CLI hello:

* [Azure CLI 1.0](dns-operations-recordsets-cli-nodejs.md) -nostri CLI per hello classic e risorse Gestione modelli di distribuzione.
* [Azure CLI 2.0](dns-operations-recordsets-cli.md) -la prossima generazione CLI per modello di distribuzione di gestione risorse hello.

esempi di Hello in questo articolo si supponga di avere già [installato Azure CLI 1.0, firmato, hello e creata una zona DNS](dns-operations-dnszones-cli-nodejs.md).

## <a name="introduction"></a>Introduzione

Prima di creare record DNS nel sistema DNS di Azure, è innanzitutto necessario toounderstand come DNS di Azure consente di organizzare i record DNS nel set di record DNS.

[!INCLUDE [dns-about-records-include](../../includes/dns-about-records-include.md)]

Per altre informazioni sui record DNS nel servizio DNS di Azure, vedere [Zone e record DNS](dns-zones-records.md).

## <a name="create-a-dns-record"></a>Creare un record DNS

toocreate un record DNS, utilizzare hello `azure network dns record-set add-record` comando. Per altre informazioni, vedere `azure network dns record-set add-record -h`.

Quando si crea un record, è necessario toospecify nome del gruppo risorse hello, nome della zona, set di record, nome, tipo di record hello e hello dettagli del record di hello viene creato. Hello nome set di record specificato deve essere un *relativo* nome, pertanto è necessario escludere nome zona hello.

Se i set di record hello non esiste già, questo comando viene creato automaticamente. Se i set di record hello esiste già, denominarla questo comando hello record specificare toohello set di record esistenti.

Se viene creato un nuovo set di record, per la durata (TTL) viene usato un valore predefinito di 3600. Per istruzioni su come toouse TTLs diversi, vedere [creare un set di record DNS](#create-a-dns-record-set).

esempio Hello crea un record A chiamato *www* nella zona hello *contoso.com* nel gruppo di risorse hello *MyResourceGroup*. indirizzo IP di un record è hello Hello *1.2.3.4*.

```azurecli
azure network dns record-set add-record MyResourceGroup contoso.com www A -a 1.2.3.4
```

un record di apice hello della zona hello toocreate (in questo caso, "contoso.com"), utilizzare il nome di record hello "@", includendo le virgolette hello:

```azurecli
azure network dns record-set add-record MyResourceGroup contoso.com "@" A -a 1.2.3.4
```

## <a name="create-a-dns-record-set"></a>Creare un set di record DNS

In hello esempi sopra riportati, record DNS hello è entrambi tooan aggiunto set di record esistente o creazione del set di record hello *in modo implicito*. È inoltre possibile creare set di record hello *in modo esplicito* prima aggiunta di record tooit. DNS di Azure supporta set di record "empty", che può agire come un segnaposto tooreserve un nome DNS prima di creare record DNS. Set di record vuoti sono visibili nella hello Azure DNS piano di controllo, ma non vengono visualizzati in server dei nomi DNS di Azure hello.

Set di record vengono creati utilizzando hello `azure network dns record-set create` comando. Per altre informazioni, vedere `azure network dns record-set create -h`.

La creazione di record hello impostate in modo esplicito consente toospecify di proprietà set di record, ad esempio hello [Time-To-Live (TTL)](dns-zones-records.md#time-to-live) e i metadati. [Set di record dei metadati](dns-zones-records.md#tags-and-metadata) può essere utilizzato tooassociate i dati specifici dell'applicazione con ogni set di record, come coppie chiave-valore.

esempio Hello crea un record vuoto impostato con una durata di 60 secondi, con hello `--ttl` parametro (forma breve `-l`):

```azurecli
azure network dns record-set create MyResourceGroup contoso.com www A --ttl 60
```

esempio Hello Crea set con due voci di metadati, un record "dept = finance" e "ambiente = produzione", utilizzando hello `--metadata` parametro (forma breve `-m`):

```azurecli
azure network dns record-set create MyResourceGroup contoso.com www A --metadata "dept=finance;environment=production"
```

Dopo aver creato un set di record vuoto, è possibile aggiungervi i record usando `azure network dns record-set add-record` come descritto in [Creare un record DNS](#create-a-dns-record).

## <a name="create-records-of-other-types"></a>Creare record di altri tipi

Dopo aver visto in dettaglio come toocreate 'A' Registra, hello seguenti esempi viene illustrato come record toocreate di altri tipi di record supportato dal servizio DNS di Azure.

Utilizzare i parametri di Hello record hello toospecify dati dipendono dal tipo di hello del record di hello. Ad esempio, per un record di tipo "A", specificare indirizzi IPv4 hello con parametro hello `-a <IPv4 address>`. Hello parametri per ogni tipo di record può essere elencato utilizzando `azure network dns record-set add-record -h`.

In ogni caso, viene illustrata la modalità toocreate un singolo record. record di Hello è aggiunto toohello esistente del set di record o un set di record è stato creato in modo implicito. Per ulteriori informazioni sulla creazione di set di record e sulla definizione esplicita dei parametri di un set di record, vedere [Creare un set di record DNS](#create-a-dns-record-set).

Non fornita è un esempio toocreate un set di record SOA, poiché viene creati SOA ed eliminato con ogni zona DNS e non è possibile creare o eliminare separatamente. Tuttavia, [hello SOA possa essere modificato, come illustrato nell'esempio versione successiva](#to-modify-an-SOA-record).

### <a name="create-an-aaaa-record"></a>Creare un record AAAA

```azurecli
azure network dns record-set add-record MyResourceGroup contoso.com test-aaaa AAAA --ipv6-address 2607:f8b0:4009:1803::1005
```

### <a name="create-a-cname-record"></a>Creare un record CNAME

> [!NOTE]
> standard DNS Hello non consentono i record CNAME al vertice hello di una zona (`-Name "@"`), né che consentono i set di record che contiene più di un record.
> 
> Per altre informazioni, vedere[Record CNAME](dns-zones-records.md#cname-records).

```azurecli
azure network dns record-set add-record  MyResourceGroup contoso.com  test-cname CNAME --cname www.contoso.com
```

### <a name="create-an-mx-record"></a>Creare un record MX

In questo esempio, si usa nome set di record hello "@" hello toocreate record MX al vertice zona hello (in questo caso, "contoso.com").

```azurecli
azure network dns record-set add-record MyResourceGroup contoso.com  "@" MX --exchange mail.contoso.com --preference 5
```

### <a name="create-an-ns-record"></a>Creare un record NS

```azurecli
azure network dns record-set add-record MyResourceGroup  contoso.com  test-ns NS --nsdname ns1.contoso.com
```

### <a name="create-a-ptr-record"></a>Creare un record PTR

In questo caso, "my-arpa-zone.com' rappresenta hello zone ARPA che rappresenta l'intervallo di IP. Ogni record PTR impostato in questa zona corrisponde tooan di indirizzo IP in questo intervallo IP.  nome del record '10' Hello è ultimo ottetto di hello dell'indirizzo IP hello in questo intervallo IP rappresentato da questo record.

```azurecli
azure network dns record-set add-record MyResourceGroup my-arpa-zone.com "10" PTR --ptrdname "myservice.contoso.com"
```

### <a name="create-an-srv-record"></a>Creare un record SRV

Quando si crea un [set di record SRV](dns-zones-records.md#srv-records), specificare hello  *\_servizio* e  *\_protocollo* in hello Nome set di record. Nessun tooinclude necessità è "@" in hello set di record nome durante la creazione di un record SRV set al vertice zona hello.

```azurecli
azure network dns record-set add-record MyResourceGroup contoso.com  "_sip._tls" SRV --priority 10 --weight 5 --port 8080 --target "sip.contoso.com"
```

### <a name="create-a-txt-record"></a>Creare un record TXT

Hello esempio seguente viene illustrato come toocreate un TXT record. Per ulteriori informazioni sulla lunghezza massima della stringa hello è supportata nei record TXT, vedere [record TXT](dns-zones-records.md#txt-records).

```azurecli
azure network dns record-set add-record MyResourceGroup contoso.com test-txt TXT --text "This is a TXT record"
```

## <a name="get-a-record-set"></a>Ottenere un set di record

Utilizzare un set di record esistente, tooretrieve `azure network dns record-set show`. Per altre informazioni, vedere `azure network dns record-set show -h`.

Quando si crea un record o un set di record, record hello impostare nome specificato deve essere un *relativo* nome, pertanto è necessario escludere nome zona hello. È necessario anche tipo di record hello toospecify, il set di zona hello contenente record di hello e gruppo di risorse che contiene la zona hello hello.

esempio Hello recupera record hello *www* di tipo dall'area *contoso.com* nel gruppo di risorse *MyResourceGroup*:

```azurecli
azure network dns record-set show MyResourceGroup contoso.com www A
```

## <a name="list-record-sets"></a>Elencare i set di record

È possibile elencare tutti i record in una zona DNS tramite hello `azure network dns record-set list` comando. Per altre informazioni, vedere `azure network dns record-set list -h`.

Questo esempio vengono restituiti i set di tutti i record nella zona hello *contoso.com*, nel gruppo di risorse *MyResourceGroup*, indipendentemente dal nome o tipo di record:

```azurecli
azure network dns record-set list MyResourceGroup contoso.com
```

In questo esempio restituisce tutti i set di record corrispondenti hello dato tipo di record (in questo caso, 'A' record):

```azurecli
azure network dns record-set list MyResourceGroup contoso.com --type A
```

## <a name="add-a-record-tooan-existing-record-set"></a>Aggiungere un record tooan esistente del set di record

È possibile utilizzare `azure network dns record-set add-record` sia toocreate un record in un nuovo record impostata oppure tooadd un record esistente tooan record.

Per ulteriori informazioni, vedere [Creare un record DNS](#create-a-dns-record) e [Creare record di altri tipi](#create-records-of-other-types) sopra.

## <a name="remove-a-record-from-an-existing-record-set"></a>Rimuovere un record da un set di record esistente.

registrare un DNS tooremove da un set di record esistente, utilizzare `azure network dns record-set delete-record`. Per altre informazioni, vedere `azure network dns record-set delete-record -h`.

Questo comando elimina un record DNS da un set di record. Se viene eliminato l'ultimo record di hello in un set di record, record di hello impostare autonomamente è **non** eliminato. Si avrà invece un set di record vuoto. Vedere invece di set di record di toodelete hello [eliminare un set di record](#delete-a-record-set).

È necessario toospecify toobe di hello record eliminato e zona hello deve essere eliminata, utilizzando hello stessi parametri quando si crea un record utilizzando `azure network dns record-set add-record`. I parametri vengono descritti in [Creare un record DNS](#create-a-dns-record) e [Creare record di altri tipi](#create-records-of-other-types) sopra.

Questo comando richiede una conferma. Questo messaggio può essere soppresso mediante hello `--quiet` passare (forma breve `-q`).

Hello seguente esempio elimina un record con valore "1.2.3.4" dal record hello set denominato di hello *www* nella zona hello *contoso.com*, nel gruppo di risorse hello *MyResourceGroup*. richiesta di conferma Hello viene eliminata.

```azurecli
azure network dns record-set delete-record MyResourceGroup contoso.com www A -a 1.2.3.4 --quiet
```

## <a name="modify-an-existing-record-set"></a>Modificare un set di record esistente

Ogni set di record contiene un [time-to-live (TTL)](dns-zones-records.md#time-to-live), [metadati](dns-zones-records.md#tags-and-metadata) e record DNS. Hello sezioni seguenti illustrano come toomodify di queste proprietà.

### <a name="toomodify-an-a-aaaa-mx-ns-ptr-srv-or-txt-record"></a>un record A, AAAA, MX, NS, PTR, SRV o TXT toomodify

toomodify un record esistente di tipo A, AAAA, MX, NS, PTR, SRV o TXT, è necessario innanzitutto aggiungere un nuovo record e record esistente hello di eliminazione. Per istruzioni dettagliate su come toodelete e aggiungere i record, vedere le sezioni precedenti di questo articolo hello.

Hello di esempio seguente viene illustrato come un record di 'A', da IP indirizzo 1.2.3.4 tooIP toomodify indirizzo 5.6.7.8:

```azurecli
azure network dns record-set add-record MyResourceGroup contoso.com www A -a 5.6.7.8
azure network dns record-set delete-record MyResourceGroup contoso.com www A -a 1.2.3.4
```

### <a name="toomodify-a-cname-record"></a>toomodify un record CNAME

Utilizzare un record CNAME, toomodify `azure network dns record-set add-record` tooadd hello nuovo valore di record. A differenza di altri tipi di record, un set di record CNAME può contenere solo un singolo record. È pertanto record esistente hello *sostituito* nuovo record di hello quando viene aggiunto e non è necessario toobe eliminata separatamente.  Si sarà richiesta tooaccept questa sostituzione.

esempio Hello Modifica set di record CNAME hello *www* nella zona hello *contoso.com*, nel gruppo di risorse *MyResourceGroup*, toopoint troppo 'www.fabrikam.net' anziché il relativo valore esistente:

```azurecli
azure network dns record-set add-record MyResourceGroup contoso.com www CNAME --cname www.fabrikam.net
``` 

### <a name="toomodify-an-soa-record"></a>un record SOA toomodify

Utilizzare `azure network dns record-set set-soa-record` toomodify hello SOA per una zona DNS specificata. Per altre informazioni, vedere `azure network dns record-set set-soa-record -h`.

Hello esempio seguente viene illustrato come proprietà tooset hello "email" di hello SOA registrare per la zona hello *contoso.com* nel gruppo di risorse hello *MyResourceGroup*:

```azurecli
azure network dns record-set set-soa-record rg1 contoso.com --email admin.contoso.com
```


### <a name="toomodify-ns-records-at-hello-zone-apex"></a>record NS toomodify al vertice zona hello

record NS Hello impostato al vertice zona hello viene creato automaticamente con ogni zona DNS. Contiene i nomi hello della zona di hello DNS di Azure nome server toohello assegnato.

È possibile aggiungere nomi aggiuntivi server toothis NS set di record, toosupport CO-ospitano i domini con più di un provider DNS. È inoltre possibile modificare hello durata (TTL) e i metadati per questo set di record. Tuttavia, è Impossibile rimuovere o modificare server dei nomi DNS di Azure prepopolato hello.

Si noti che questo si applica solo toohello NS set di record al vertice zona hello. Altri set di record NS nella zona (come le aree figlio toodelegate usato) possono essere modificati senza vincoli.

Hello di esempio seguente viene illustrato come tooadd un record NS di nomi aggiuntivi server toohello imposta al vertice zona hello:

```azurecli
azure network dns record-set add-record MyResourceGroup contoso.com "@" --nsdname ns1.myotherdnsprovider.com 
```

### <a name="toomodify-hello-ttl-of-an-existing-record-set"></a>Imposta toomodify hello durata (TTL) di un record esistente

Imposta toomodify hello durata (TTL) di un record esistente, utilizzare `azure network dns record-set set`. Per altre informazioni, vedere `azure network dns record-set set -h`.

Hello di esempio seguente viene illustrato come toomodify un set di record durata (TTL), in questo caso too60 secondi:

```azurecli
azure network dns record-set set MyResourceGroup contoso.com www A --ttl 60
```

### <a name="toomodify-hello-metadata-of-an-existing-record-set"></a>toomodify hello metadati di un set di record esistente

[Set di record dei metadati](dns-zones-records.md#tags-and-metadata) può essere utilizzato tooassociate i dati specifici dell'applicazione con ogni set di record, come coppie chiave-valore. impostare toomodify hello metadati di un record esistente, utilizzare `azure network dns record-set set`. Per altre informazioni, vedere `azure network dns record-set set -h`.

Hello esempio seguente viene illustrato come toomodify un set di record con due voci di metadati, "dept = finance" e "ambiente = produzione", utilizzando hello `--metadata` parametro (forma breve `-m`). Si noti che i metadati esistenti sono *sostituito* da valori hello specificato.

```azurecli
azure network dns record-set set MyResourceGroup contoso.com www A --metadata "dept=finance;environment=production"
```

## <a name="delete-a-record-set"></a>Eliminare un set di record

Set di record possono essere eliminate utilizzando hello `azure network dns record-set delete` comando. Per altre informazioni, vedere `azure network dns record-set delete -h`. L'eliminazione di un set di record elimina inoltre tutti i record all'interno del set di record hello.

> [!NOTE]
> Non è possibile eliminare hello SOA e NS set di record al vertice zona hello (`-Name "@"`).  Vengono creati automaticamente quando è stato creato, zona hello e vengono eliminati automaticamente quando viene eliminata hello.

esempio Hello Elimina record hello set denominato *www* di tipo dall'area hello *contoso.com* nel gruppo di risorse *MyResourceGroup*:

```azurecli
azure network dns record-set delete MyResourceGroup contoso.com www A
```

Si è richiesta tooconfirm hello operazione di eliminazione. toosuppress questo prompt dei comandi, utilizzare hello `--quiet` passare (forma breve `-q`).

## <a name="next-steps"></a>Passaggi successivi

Altre informazioni su [zone e record nel servizio DNS di Azure](dns-zones-records.md).
<br>
Informazioni su come troppo[proteggere le zone e record](dns-protect-zones-recordsets.md) quando si utilizza il DNS di Azure.

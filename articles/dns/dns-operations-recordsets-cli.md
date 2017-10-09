---
title: i record DNS aaaManage DNS di Azure utilizzando hello Azure CLI 2.0 | Documenti Microsoft
description: Gestione dei set di record e dei record DNS in DNS di Azure quando si ospita il dominio in DNS di Azure. Tutti i comandi dell'interfaccia della riga di comando 2.0 per le operazioni sui set di record e i record.
services: dns
documentationcenter: na
author: jtuliani
manager: carmonm
ms.assetid: 5356a3a5-8dec-44ac-9709-0c2b707f6cb5
ms.service: dns
ms.devlang: azurecli
ms.topic: article
ms.tgt_pltfrm: na
ms.custom: H1Hack27Feb2017
ms.workload: infrastructure-services
ms.date: 02/27/2017
ms.author: jonatul
ms.openlocfilehash: 9d6f8e74ebad55ccd2381fd84a830d2c7bbb1f30
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="manage-dns-records-and-recordsets-in-azure-dns-using-hello-azure-cli-20"></a><span data-ttu-id="9770b-104">Gestire i record DNS e Recordset in DNS di Azure mediante Azure CLI 2.0 hello</span><span class="sxs-lookup"><span data-stu-id="9770b-104">Manage DNS records and recordsets in Azure DNS using hello Azure CLI 2.0</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="9770b-105">Portale di Azure</span><span class="sxs-lookup"><span data-stu-id="9770b-105">Azure Portal</span></span>](dns-operations-recordsets-portal.md)
> * [<span data-ttu-id="9770b-106">Interfaccia della riga di comando di Azure 1.0</span><span class="sxs-lookup"><span data-stu-id="9770b-106">Azure CLI 1.0</span></span>](dns-operations-recordsets-cli-nodejs.md)
> * [<span data-ttu-id="9770b-107">Interfaccia della riga di comando di Azure 2.0</span><span class="sxs-lookup"><span data-stu-id="9770b-107">Azure CLI 2.0</span></span>](dns-operations-recordsets-cli.md)
> * [<span data-ttu-id="9770b-108">PowerShell</span><span class="sxs-lookup"><span data-stu-id="9770b-108">PowerShell</span></span>](dns-operations-recordsets.md)

<span data-ttu-id="9770b-109">Questo articolo illustra come i record DNS toomanage per la zona DNS mediante hello multipiattaforma Azure interfaccia della riga di comando (CLI) 2.0, che è disponibile per Windows, Mac e Linux.</span><span class="sxs-lookup"><span data-stu-id="9770b-109">This article shows you how toomanage DNS records for your DNS zone by using hello cross-platform Azure command-line interface (CLI) 2.0, which is available for Windows, Mac and Linux.</span></span> <span data-ttu-id="9770b-110">È inoltre possibile gestire i record DNS utilizzando [Azure PowerShell](dns-operations-recordsets.md) o hello [portale di Azure](dns-operations-recordsets-portal.md).</span><span class="sxs-lookup"><span data-stu-id="9770b-110">You can also manage your DNS records using [Azure PowerShell](dns-operations-recordsets.md) or hello [Azure portal](dns-operations-recordsets-portal.md).</span></span>

## <a name="cli-versions-toocomplete-hello-task"></a><span data-ttu-id="9770b-111">Attività hello toocomplete versioni CLI</span><span class="sxs-lookup"><span data-stu-id="9770b-111">CLI versions toocomplete hello task</span></span>

<span data-ttu-id="9770b-112">È possibile completare l'attività hello utilizzando una delle seguenti versioni CLI hello:</span><span class="sxs-lookup"><span data-stu-id="9770b-112">You can complete hello task using one of hello following CLI versions:</span></span>

* <span data-ttu-id="9770b-113">[Azure CLI 1.0](dns-operations-recordsets-cli-nodejs.md) -nostri CLI per hello classic e risorse Gestione modelli di distribuzione.</span><span class="sxs-lookup"><span data-stu-id="9770b-113">[Azure CLI 1.0](dns-operations-recordsets-cli-nodejs.md) - our CLI for hello classic and resource management deployment models.</span></span>
* <span data-ttu-id="9770b-114">[Azure CLI 2.0](dns-operations-recordsets-cli.md) -la prossima generazione CLI per modello di distribuzione di gestione risorse hello.</span><span class="sxs-lookup"><span data-stu-id="9770b-114">[Azure CLI 2.0](dns-operations-recordsets-cli.md) - our next generation CLI for hello resource management deployment model.</span></span>

<span data-ttu-id="9770b-115">esempi di Hello in questo articolo si supponga di avere già [installato Azure CLI 2.0, firmato, hello e creata una zona DNS](dns-operations-dnszones-cli.md).</span><span class="sxs-lookup"><span data-stu-id="9770b-115">hello examples in this article assume you have already [installed hello Azure CLI 2.0, signed in, and created a DNS zone](dns-operations-dnszones-cli.md).</span></span>

## <a name="introduction"></a><span data-ttu-id="9770b-116">Introduzione</span><span class="sxs-lookup"><span data-stu-id="9770b-116">Introduction</span></span>

<span data-ttu-id="9770b-117">Prima di creare record DNS nel sistema DNS di Azure, è innanzitutto necessario toounderstand come DNS di Azure consente di organizzare i record DNS nel set di record DNS.</span><span class="sxs-lookup"><span data-stu-id="9770b-117">Before creating DNS records in Azure DNS, you first need toounderstand how Azure DNS organizes DNS records into DNS record sets.</span></span>

[!INCLUDE [dns-about-records-include](../../includes/dns-about-records-include.md)]

<span data-ttu-id="9770b-118">Per altre informazioni sui record DNS nel servizio DNS di Azure, vedere [Zone e record DNS](dns-zones-records.md).</span><span class="sxs-lookup"><span data-stu-id="9770b-118">For more information about DNS records in Azure DNS, see [DNS zones and records](dns-zones-records.md).</span></span>

## <a name="create-a-dns-record"></a><span data-ttu-id="9770b-119">Creare un record DNS</span><span class="sxs-lookup"><span data-stu-id="9770b-119">Create a DNS record</span></span>

<span data-ttu-id="9770b-120">toocreate un record DNS, utilizzare hello `az network dns record-set <record-type> set-record` comando (in cui `<record-type>` è hello tipo di record, ovvero</span><span class="sxs-lookup"><span data-stu-id="9770b-120">toocreate a DNS record, use hello `az network dns record-set <record-type> set-record` command (where `<record-type>` is hello type of record, i.e</span></span> <span data-ttu-id="9770b-121">a, srv, txt e così via). Per altre informazioni, vedere `az network dns record-set --help`.</span><span class="sxs-lookup"><span data-stu-id="9770b-121">a, srv, txt, etc.) For help, see `az network dns record-set --help`.</span></span>

<span data-ttu-id="9770b-122">Quando si crea un record, è necessario toospecify nome del gruppo risorse hello, nome della zona, set di record, nome, tipo di record hello e hello dettagli del record di hello viene creato.</span><span class="sxs-lookup"><span data-stu-id="9770b-122">When creating a record, you need toospecify hello resource group name, zone name, record set name, hello record type, and hello details of hello record being created.</span></span> <span data-ttu-id="9770b-123">Hello nome set di record specificato deve essere un *relativo* nome, pertanto è necessario escludere nome zona hello.</span><span class="sxs-lookup"><span data-stu-id="9770b-123">hello record set name given must be a *relative* name, meaning it must exclude hello zone name.</span></span>

<span data-ttu-id="9770b-124">Se i set di record hello non esiste già, questo comando viene creato automaticamente.</span><span class="sxs-lookup"><span data-stu-id="9770b-124">If hello record set does not already exist, this command creates it for you.</span></span> <span data-ttu-id="9770b-125">Se esiste un record di hello già impostata, questo comando aggiunge record hello è specificare toohello set di record esistenti.</span><span class="sxs-lookup"><span data-stu-id="9770b-125">If hello record set already exists, this command adds hello record you specify toohello existing record set.</span></span>

<span data-ttu-id="9770b-126">Se viene creato un nuovo set di record, per la durata (TTL) viene usato un valore predefinito di 3600.</span><span class="sxs-lookup"><span data-stu-id="9770b-126">If a new record set is created, a default time-to-live (TTL) of 3600 is used.</span></span> <span data-ttu-id="9770b-127">Per istruzioni su come toouse TTLs diversi, vedere [creare un set di record DNS](#create-a-dns-record-set).</span><span class="sxs-lookup"><span data-stu-id="9770b-127">For instructions on how toouse different TTLs, see [Create a DNS record set](#create-a-dns-record-set).</span></span>

<span data-ttu-id="9770b-128">esempio Hello crea un record A chiamato *www* nella zona hello *contoso.com* nel gruppo di risorse hello *MyResourceGroup*.</span><span class="sxs-lookup"><span data-stu-id="9770b-128">hello following example creates an A record called *www* in hello zone *contoso.com* in hello resource group *MyResourceGroup*.</span></span> <span data-ttu-id="9770b-129">indirizzo IP di un record è hello Hello *1.2.3.4*.</span><span class="sxs-lookup"><span data-stu-id="9770b-129">hello IP address of hello A record is *1.2.3.4*.</span></span>

```azurecli
az network dns record-set a set-record --resource-group myresourcegroup --zone-name contoso.com --record-set-name www --ipv4-address 1.2.3.4
```

<span data-ttu-id="9770b-130">Imposta toocreate un record in apice hello della zona hello (in questo caso, "contoso.com"), utilizzare il nome di record hello "@", includendo le virgolette hello:</span><span class="sxs-lookup"><span data-stu-id="9770b-130">toocreate a record set in hello apex of hello zone (in this case, "contoso.com"), use hello record name "@", including hello quotation marks:</span></span>

```azurecli
az network dns record-set a set-record --resource-group myresourcegroup --zone-name contoso.com --record-set-name "@" --ipv4-address 1.2.3.4
```

## <a name="create-a-dns-record-set"></a><span data-ttu-id="9770b-131">Creare un set di record DNS</span><span class="sxs-lookup"><span data-stu-id="9770b-131">Create a DNS record set</span></span>

<span data-ttu-id="9770b-132">In hello esempi sopra riportati, record DNS hello è entrambi tooan aggiunto set di record esistente o creazione del set di record hello *in modo implicito*.</span><span class="sxs-lookup"><span data-stu-id="9770b-132">In hello above examples, hello DNS record was either added tooan existing record set, or hello record set was created *implicitly*.</span></span> <span data-ttu-id="9770b-133">È inoltre possibile creare set di record hello *in modo esplicito* prima aggiunta di record tooit.</span><span class="sxs-lookup"><span data-stu-id="9770b-133">You can also create hello record set *explicitly* before adding records tooit.</span></span> <span data-ttu-id="9770b-134">DNS di Azure supporta set di record "empty", che può agire come un segnaposto tooreserve un nome DNS prima di creare record DNS.</span><span class="sxs-lookup"><span data-stu-id="9770b-134">Azure DNS supports 'empty' record sets, which can act as a placeholder tooreserve a DNS name before creating DNS records.</span></span> <span data-ttu-id="9770b-135">Set di record vuoti sono visibili nella hello Azure DNS piano di controllo, ma non vengono visualizzati in server dei nomi DNS di Azure hello.</span><span class="sxs-lookup"><span data-stu-id="9770b-135">Empty record sets are visible in hello Azure DNS control plane, but do not appear on hello Azure DNS name servers.</span></span>

<span data-ttu-id="9770b-136">Set di record vengono creati utilizzando hello `az network dns record-set <record-type> create` comando.</span><span class="sxs-lookup"><span data-stu-id="9770b-136">Record sets are created using hello `az network dns record-set <record-type> create` command.</span></span> <span data-ttu-id="9770b-137">Per altre informazioni, vedere `az network dns record-set <record-type> create --help`.</span><span class="sxs-lookup"><span data-stu-id="9770b-137">For help, see `az network dns record-set <record-type> create --help`.</span></span>

<span data-ttu-id="9770b-138">La creazione di record hello impostate in modo esplicito consente toospecify di proprietà set di record, ad esempio hello [Time-To-Live (TTL)](dns-zones-records.md#time-to-live) e i metadati.</span><span class="sxs-lookup"><span data-stu-id="9770b-138">Creating hello record set explicitly allows you toospecify record set properties such as hello [Time-To-Live (TTL)](dns-zones-records.md#time-to-live) and metadata.</span></span> <span data-ttu-id="9770b-139">[Set di record dei metadati](dns-zones-records.md#tags-and-metadata) può essere utilizzato tooassociate i dati specifici dell'applicazione con ogni set di record, come coppie chiave-valore.</span><span class="sxs-lookup"><span data-stu-id="9770b-139">[Record set metadata](dns-zones-records.md#tags-and-metadata) can be used tooassociate application-specific data with each record set, as key-value pairs.</span></span>

<span data-ttu-id="9770b-140">Hello seguente esempio viene creato un set di record vuoto di tipo 'A' con una durata di 60 secondi, utilizzando hello `--ttl` parametro (forma breve `-l`):</span><span class="sxs-lookup"><span data-stu-id="9770b-140">hello following example creates an empty record set of type 'A' with a 60-second TTL, by using hello `--ttl` parameter (short form `-l`):</span></span>

```azurecli
az network dns record-set a create --resource-group myresourcegroup --zone-name contoso.com --name www --ttl 60
```

<span data-ttu-id="9770b-141">esempio Hello Crea set con due voci di metadati, un record "dept = finance" e "ambiente = produzione", utilizzando hello `--metadata` parametro:</span><span class="sxs-lookup"><span data-stu-id="9770b-141">hello following example creates a record set with two metadata entries, "dept=finance" and "environment=production", by using hello `--metadata` parameter :</span></span>

```azurecli
az network dns record-set a create --resource-group myresourcegroup --zone-name contoso.com --name www --metadata "dept=finance" "environment=production"
```

<span data-ttu-id="9770b-142">Dopo aver creato un set di record vuoto, è possibile aggiungervi i record usando `azure network dns record-set <record-type> set-record` come descritto in [Creare un record DNS](#create-a-dns-record).</span><span class="sxs-lookup"><span data-stu-id="9770b-142">Having created an empty record set, records can be added using `azure network dns record-set <record-type> set-record` as described in [Create a DNS record](#create-a-dns-record).</span></span>

## <a name="create-records-of-other-types"></a><span data-ttu-id="9770b-143">Creare record di altri tipi</span><span class="sxs-lookup"><span data-stu-id="9770b-143">Create records of other types</span></span>

<span data-ttu-id="9770b-144">Dopo aver visto in dettaglio come toocreate 'A' Registra, hello seguenti esempi viene illustrato come record toocreate di altri tipi di record supportato dal servizio DNS di Azure.</span><span class="sxs-lookup"><span data-stu-id="9770b-144">Having seen in detail how toocreate 'A' records, hello following examples show how toocreate record of other record types supported by Azure DNS.</span></span>

<span data-ttu-id="9770b-145">Utilizzare i parametri di Hello record hello toospecify dati dipendono dal tipo di hello del record di hello.</span><span class="sxs-lookup"><span data-stu-id="9770b-145">hello parameters used toospecify hello record data vary depending on hello type of hello record.</span></span> <span data-ttu-id="9770b-146">Ad esempio, per un record di tipo "A", specificare indirizzi IPv4 hello con parametro hello `--ipv4-address <IPv4 address>`.</span><span class="sxs-lookup"><span data-stu-id="9770b-146">For example, for a record of type "A", you specify hello IPv4 address with hello parameter `--ipv4-address <IPv4 address>`.</span></span> <span data-ttu-id="9770b-147">Hello parametri per ogni tipo di record può essere elencato utilizzando `az network dns record-set <record-type> set-record --help`.</span><span class="sxs-lookup"><span data-stu-id="9770b-147">hello parameters for each record type can be listed using `az network dns record-set <record-type> set-record --help`.</span></span>

<span data-ttu-id="9770b-148">In ogni caso, viene illustrata la modalità toocreate un singolo record.</span><span class="sxs-lookup"><span data-stu-id="9770b-148">In each case, we show how toocreate a single record.</span></span> <span data-ttu-id="9770b-149">record di Hello è aggiunto toohello esistente del set di record o un set di record è stato creato in modo implicito.</span><span class="sxs-lookup"><span data-stu-id="9770b-149">hello record is added toohello existing record set, or a record set created implicitly.</span></span> <span data-ttu-id="9770b-150">Per ulteriori informazioni sulla creazione di set di record e sulla definizione esplicita dei parametri di un set di record, vedere [Creare un set di record DNS](#create-a-dns-record-set).</span><span class="sxs-lookup"><span data-stu-id="9770b-150">For more information on creating record sets and defining record set parameter explicitly, see [Create a DNS record set](#create-a-dns-record-set).</span></span>

<span data-ttu-id="9770b-151">Non fornita è un esempio toocreate un set di record SOA, poiché viene creati SOA ed eliminato con ogni zona DNS e non è possibile creare o eliminare separatamente.</span><span class="sxs-lookup"><span data-stu-id="9770b-151">We do not give an example toocreate an SOA record set, since SOAs are created and deleted with each DNS zone and cannot be created or deleted separately.</span></span> <span data-ttu-id="9770b-152">Tuttavia, [hello SOA possa essere modificato, come illustrato nell'esempio versione successiva](#to-modify-an-SOA-record).</span><span class="sxs-lookup"><span data-stu-id="9770b-152">However, [hello SOA can be modified, as shown in a later example](#to-modify-an-SOA-record).</span></span>

### <a name="create-an-aaaa-record"></a><span data-ttu-id="9770b-153">Creare un record AAAA</span><span class="sxs-lookup"><span data-stu-id="9770b-153">Create an AAAA record</span></span>

```azurecli
az network dns record-set aaaa set-record --resource-group myresourcegroup --zone-name contoso.com --record-set-name test-aaaa --ipv6-address 2607:f8b0:4009:1803::1005
```

### <a name="create-a-cname-record"></a><span data-ttu-id="9770b-154">Creare un record CNAME</span><span class="sxs-lookup"><span data-stu-id="9770b-154">Create a CNAME record</span></span>

> [!NOTE]
> <span data-ttu-id="9770b-155">standard DNS Hello non consentono i record CNAME al vertice hello di una zona (`--Name "@"`), né che consentono i set di record che contiene più di un record.</span><span class="sxs-lookup"><span data-stu-id="9770b-155">hello DNS standards do not permit CNAME records at hello apex of a zone (`--Name "@"`), nor do they permit record sets containing more than one record.</span></span>
> 
> <span data-ttu-id="9770b-156">Per altre informazioni, vedere[Record CNAME](dns-zones-records.md#cname-records).</span><span class="sxs-lookup"><span data-stu-id="9770b-156">For more information, see [CNAME records](dns-zones-records.md#cname-records).</span></span>

```azurecli
az network dns record-set cname set-record --resource-group myresourcegroup --zone-name contoso.com --record-set-name test-cname --cname www.contoso.com
```

### <a name="create-an-mx-record"></a><span data-ttu-id="9770b-157">Creare un record MX</span><span class="sxs-lookup"><span data-stu-id="9770b-157">Create an MX record</span></span>

<span data-ttu-id="9770b-158">In questo esempio, si usa nome set di record hello "@" hello toocreate record MX al vertice zona hello (in questo caso, "contoso.com").</span><span class="sxs-lookup"><span data-stu-id="9770b-158">In this example, we use hello record set name "@" toocreate hello MX record at hello zone apex (in this case, "contoso.com").</span></span>

```azurecli
az network dns record-set mx set-record --resource-group myresourcegroup --zone-name contoso.com --record-set-name "@" --exchange mail.contoso.com --preference 5
```

### <a name="create-an-ns-record"></a><span data-ttu-id="9770b-159">Creare un record NS</span><span class="sxs-lookup"><span data-stu-id="9770b-159">Create an NS record</span></span>

```azurecli
az network dns record-set ns set-record --resource-group myresourcegroup --zone-name contoso.com --record-set-name test-ns --nsdname ns1.contoso.com
```

### <a name="create-a-ptr-record"></a><span data-ttu-id="9770b-160">Creare un record PTR</span><span class="sxs-lookup"><span data-stu-id="9770b-160">Create a PTR record</span></span>

<span data-ttu-id="9770b-161">In questo caso, "my-arpa-zone.com' rappresenta hello zone ARPA che rappresenta l'intervallo di IP.</span><span class="sxs-lookup"><span data-stu-id="9770b-161">In this case, 'my-arpa-zone.com' represents hello ARPA zone representing your IP range.</span></span> <span data-ttu-id="9770b-162">Ogni record PTR impostato in questa zona corrisponde tooan di indirizzo IP in questo intervallo IP.</span><span class="sxs-lookup"><span data-stu-id="9770b-162">Each PTR record set in this zone corresponds tooan IP address within this IP range.</span></span>  <span data-ttu-id="9770b-163">nome del record '10' Hello è ultimo ottetto di hello dell'indirizzo IP hello in questo intervallo IP rappresentato da questo record.</span><span class="sxs-lookup"><span data-stu-id="9770b-163">hello record name '10' is hello last octet of hello IP address within this IP range represented by this record.</span></span>

```azurecli
az network dns record-set ptr set-record --resource-group myresourcegroup --zone-name contoso.com --record-set-name my-arpa.zone.com --ptrdname myservice.contoso.com
```

### <a name="create-an-srv-record"></a><span data-ttu-id="9770b-164">Creare un record SRV</span><span class="sxs-lookup"><span data-stu-id="9770b-164">Create an SRV record</span></span>

<span data-ttu-id="9770b-165">Quando si crea un [set di record SRV](dns-zones-records.md#srv-records), specificare hello  *\_servizio* e  *\_protocollo* in hello Nome set di record.</span><span class="sxs-lookup"><span data-stu-id="9770b-165">When creating an [SRV record set](dns-zones-records.md#srv-records), specify hello *\_service* and *\_protocol* in hello record set name.</span></span> <span data-ttu-id="9770b-166">Nessun tooinclude necessità è "@" in hello set di record nome durante la creazione di un record SRV set al vertice zona hello.</span><span class="sxs-lookup"><span data-stu-id="9770b-166">There is no need tooinclude "@" in hello record set name when creating an SRV record set at hello zone apex.</span></span>

```azurecli
az network dns record-set srv set-record --resource-group myresourcegroup --zone-name contoso.com --record-set-name _sip._tls --priority 10 --weight 5 --port 8080 --target sip.contoso.com
```

### <a name="create-a-txt-record"></a><span data-ttu-id="9770b-167">Creare un record TXT</span><span class="sxs-lookup"><span data-stu-id="9770b-167">Create a TXT record</span></span>

<span data-ttu-id="9770b-168">Hello esempio seguente viene illustrato come toocreate un TXT record.</span><span class="sxs-lookup"><span data-stu-id="9770b-168">hello following example shows how toocreate a TXT record.</span></span> <span data-ttu-id="9770b-169">Per ulteriori informazioni sulla lunghezza massima della stringa hello è supportata nei record TXT, vedere [record TXT](dns-zones-records.md#txt-records).</span><span class="sxs-lookup"><span data-stu-id="9770b-169">For more information about hello maximum string length supported in TXT records, see [TXT records](dns-zones-records.md#txt-records).</span></span>

```azurecli
az network dns record-set txt set-record --resource-group myresourcegroup --zone-name contoso.com --record-set-name test-txt --value "This is a TXT record"
```

## <a name="get-a-record-set"></a><span data-ttu-id="9770b-170">Ottenere un set di record</span><span class="sxs-lookup"><span data-stu-id="9770b-170">Get a record set</span></span>

<span data-ttu-id="9770b-171">Utilizzare un set di record esistente, tooretrieve `az network dns record-set <record-type> show`.</span><span class="sxs-lookup"><span data-stu-id="9770b-171">tooretrieve an existing record set, use `az network dns record-set <record-type> show`.</span></span> <span data-ttu-id="9770b-172">Per altre informazioni, vedere `az network dns record-set <record-type> show --help`.</span><span class="sxs-lookup"><span data-stu-id="9770b-172">For help, see `az network dns record-set <record-type> show --help`.</span></span>

<span data-ttu-id="9770b-173">Quando si crea un record o un set di record, record hello impostare nome specificato deve essere un *relativo* nome, pertanto è necessario escludere nome zona hello.</span><span class="sxs-lookup"><span data-stu-id="9770b-173">As when creating a record or record set, hello record set name given must be a *relative* name, meaning it must exclude hello zone name.</span></span> <span data-ttu-id="9770b-174">È necessario anche tipo di record hello toospecify, il set di zona hello contenente record di hello e gruppo di risorse che contiene la zona hello hello.</span><span class="sxs-lookup"><span data-stu-id="9770b-174">You also need toospecify hello record type, hello zone containing hello record set, and hello resource group containing hello zone.</span></span>

<span data-ttu-id="9770b-175">esempio Hello recupera record hello *www* di tipo dall'area *contoso.com* nel gruppo di risorse *MyResourceGroup*:</span><span class="sxs-lookup"><span data-stu-id="9770b-175">hello following example retrieves hello record *www* of type A from zone *contoso.com* in resource group *MyResourceGroup*:</span></span>

```azurecli
az network dns record-set a show --resource-group myresourcegroup --zone-name contoso.com --name www
```

## <a name="list-record-sets"></a><span data-ttu-id="9770b-176">Elencare i set di record</span><span class="sxs-lookup"><span data-stu-id="9770b-176">List record sets</span></span>

<span data-ttu-id="9770b-177">È possibile elencare tutti i record in una zona DNS tramite hello `az network dns record-set list` comando.</span><span class="sxs-lookup"><span data-stu-id="9770b-177">You can list all records in a DNS zone by using hello `az network dns record-set list` command.</span></span> <span data-ttu-id="9770b-178">Per altre informazioni, vedere `az network dns record-set list --help`.</span><span class="sxs-lookup"><span data-stu-id="9770b-178">For help, see `az network dns record-set list --help`.</span></span>

<span data-ttu-id="9770b-179">Questo esempio vengono restituiti i set di tutti i record nella zona hello *contoso.com*, nel gruppo di risorse *MyResourceGroup*, indipendentemente dal nome o tipo di record:</span><span class="sxs-lookup"><span data-stu-id="9770b-179">This example returns all record sets in hello zone *contoso.com*, in resource group *MyResourceGroup*, regardless of name or record type:</span></span>

```azurecli
az network dns record-set list --resource-group myresourcegroup --zone-name contoso.com
```

<span data-ttu-id="9770b-180">In questo esempio restituisce tutti i set di record corrispondenti hello dato tipo di record (in questo caso, 'A' record):</span><span class="sxs-lookup"><span data-stu-id="9770b-180">This example returns all record sets that match hello given record type (in this case, 'A' records):</span></span>

```azurecli
az network dns record-set a list --resource-group myresourcegroup --zone-name contoso.com 
```

## <a name="add-a-record-tooan-existing-record-set"></a><span data-ttu-id="9770b-181">Aggiungere un record tooan esistente del set di record</span><span class="sxs-lookup"><span data-stu-id="9770b-181">Add a record tooan existing record set</span></span>

<span data-ttu-id="9770b-182">È possibile utilizzare `az network dns record-set <record-type> set-record` sia toocreate un record in un nuovo record impostata oppure tooadd un record esistente tooan record.</span><span class="sxs-lookup"><span data-stu-id="9770b-182">You can use `az network dns record-set <record-type> set-record` both toocreate a record in a new record set, or tooadd a record tooan existing record set.</span></span>

<span data-ttu-id="9770b-183">Per ulteriori informazioni, vedere [Creare un record DNS](#create-a-dns-record) e [Creare record di altri tipi](#create-records-of-other-types) sopra.</span><span class="sxs-lookup"><span data-stu-id="9770b-183">For more information, see [Create a DNS record](#create-a-dns-record) and [Create records of other types](#create-records-of-other-types) above.</span></span>

## <a name="remove-a-record-from-an-existing-record-set"></a><span data-ttu-id="9770b-184">Rimuovere un record da un set di record esistente.</span><span class="sxs-lookup"><span data-stu-id="9770b-184">Remove a record from an existing record set.</span></span>

<span data-ttu-id="9770b-185">registrare un DNS tooremove da un set di record esistente, utilizzare `az network dns record-set <record-type> remove-record`.</span><span class="sxs-lookup"><span data-stu-id="9770b-185">tooremove a DNS record from an existing record set, use `az network dns record-set <record-type> remove-record`.</span></span> <span data-ttu-id="9770b-186">Per altre informazioni, vedere `az network dns record-set <record-type> remove-record -h`.</span><span class="sxs-lookup"><span data-stu-id="9770b-186">For help, see `az network dns record-set <record-type> remove-record -h`.</span></span>

<span data-ttu-id="9770b-187">Questo comando elimina un record DNS da un set di record.</span><span class="sxs-lookup"><span data-stu-id="9770b-187">This command deletes a DNS record from a record set.</span></span> <span data-ttu-id="9770b-188">Se viene eliminato l'ultimo record di hello in un set di record, viene eliminato anche il record di hello impostato autonomamente.</span><span class="sxs-lookup"><span data-stu-id="9770b-188">If hello last record in a record set is deleted, hello record set itself is also deleted.</span></span> <span data-ttu-id="9770b-189">set di record vuoto hello tookeep utilizzare hello `--keep-empty-record-set` opzione.</span><span class="sxs-lookup"><span data-stu-id="9770b-189">tookeep hello empty record set instead, use hello `--keep-empty-record-set` option.</span></span>

<span data-ttu-id="9770b-190">È necessario toospecify toobe di hello record eliminato e zona hello deve essere eliminata, utilizzando hello stessi parametri quando si crea un record utilizzando `az network dns record-set <record-type> set-record`.</span><span class="sxs-lookup"><span data-stu-id="9770b-190">You need toospecify hello record toobe deleted and hello zone it should be deleted from, using hello same parameters as when creating a record using `az network dns record-set <record-type> set-record`.</span></span> <span data-ttu-id="9770b-191">I parametri vengono descritti in [Creare un record DNS](#create-a-dns-record) e [Creare record di altri tipi](#create-records-of-other-types) sopra.</span><span class="sxs-lookup"><span data-stu-id="9770b-191">These parameters are described in [Create a DNS record](#create-a-dns-record) and [Create records of other types](#create-records-of-other-types) above.</span></span>

<span data-ttu-id="9770b-192">Hello seguente esempio elimina un record con valore "1.2.3.4" dal record hello set denominato di hello *www* nella zona hello *contoso.com*, nel gruppo di risorse hello *MyResourceGroup*.</span><span class="sxs-lookup"><span data-stu-id="9770b-192">hello following example deletes hello A record with value '1.2.3.4' from hello record set named *www* in hello zone *contoso.com*, in hello resource group *MyResourceGroup*.</span></span>

```azurecli
az network dns record-set a remove-record --resource-group myresourcegroup --zone-name contoso.com --record-set-name "www" --ipv4-address 1.2.3.4
```

## <a name="modify-an-existing-record-set"></a><span data-ttu-id="9770b-193">Modificare un set di record esistente</span><span class="sxs-lookup"><span data-stu-id="9770b-193">Modify an existing record set</span></span>

<span data-ttu-id="9770b-194">Ogni set di record contiene un [time-to-live (TTL)](dns-zones-records.md#time-to-live), [metadati](dns-zones-records.md#tags-and-metadata) e record DNS.</span><span class="sxs-lookup"><span data-stu-id="9770b-194">Each record set contains a [time-to-live (TTL)](dns-zones-records.md#time-to-live), [metadata](dns-zones-records.md#tags-and-metadata), and DNS records.</span></span> <span data-ttu-id="9770b-195">Hello sezioni seguenti illustrano come toomodify di queste proprietà.</span><span class="sxs-lookup"><span data-stu-id="9770b-195">hello following sections explain how toomodify each of these properties.</span></span>

### <a name="toomodify-an-a-aaaa-mx-ns-ptr-srv-or-txt-record"></a><span data-ttu-id="9770b-196">un record A, AAAA, MX, NS, PTR, SRV o TXT toomodify</span><span class="sxs-lookup"><span data-stu-id="9770b-196">toomodify an A, AAAA, MX, NS, PTR, SRV, or TXT record</span></span>

<span data-ttu-id="9770b-197">toomodify un record esistente di tipo A, AAAA, MX, NS, PTR, SRV o TXT, è necessario innanzitutto aggiungere un nuovo record e record esistente hello di eliminazione.</span><span class="sxs-lookup"><span data-stu-id="9770b-197">toomodify an existing record of type A, AAAA, MX, NS, PTR, SRV, or TXT, you should first add a new record and then delete hello existing record.</span></span> <span data-ttu-id="9770b-198">Per istruzioni dettagliate su come toodelete e aggiungere i record, vedere le sezioni precedenti di questo articolo hello.</span><span class="sxs-lookup"><span data-stu-id="9770b-198">For detailed instructions on how toodelete and add records, see hello earlier sections of this article.</span></span>

<span data-ttu-id="9770b-199">Hello di esempio seguente viene illustrato come un record di 'A', da IP indirizzo 1.2.3.4 tooIP toomodify indirizzo 5.6.7.8:</span><span class="sxs-lookup"><span data-stu-id="9770b-199">hello following example shows how toomodify an 'A' record, from IP address 1.2.3.4 tooIP address 5.6.7.8:</span></span>

```azurecli
az network dns record-set a set-record --resource-group myresourcegroup --zone-name contoso.com --record-set-name www --ipv4-address 5.6.7.8
az network dns record-set a remove-record --resource-group myresourcegroup --zone-name contoso.com --record-set-name www --ipv4-address 1.2.3.4
```

<span data-ttu-id="9770b-200">Non è possibile aggiungere, rimuovere o modificare i record di hello in hello automaticamente creato un record NS impostato al vertice zona hello (`--Name "@"`, tra virgolette).</span><span class="sxs-lookup"><span data-stu-id="9770b-200">You cannot add, remove, or modify hello records in hello automatically created NS record set at hello zone apex (`--Name "@"`, including quote marks).</span></span> <span data-ttu-id="9770b-201">Per questo set di record, hello solo le modifiche consentite sono record hello toomodify impostare una durata (TTL) e i metadati.</span><span class="sxs-lookup"><span data-stu-id="9770b-201">For this record set, hello only changes permitted are toomodify hello record set TTL and metadata.</span></span>

### <a name="toomodify-a-cname-record"></a><span data-ttu-id="9770b-202">toomodify un record CNAME</span><span class="sxs-lookup"><span data-stu-id="9770b-202">toomodify a CNAME record</span></span>

<span data-ttu-id="9770b-203">A differenza della maggior parte degli altri tipi di record, un set di record CNAME può contenere solo un singolo record.</span><span class="sxs-lookup"><span data-stu-id="9770b-203">Unlike most other record types, a CNAME record set can only contain a single record.</span></span>  <span data-ttu-id="9770b-204">Pertanto, non è possibile sostituire il valore corrente di hello aggiungendo un nuovo record e rimozione del record esistente hello, come per altri tipi di record.</span><span class="sxs-lookup"><span data-stu-id="9770b-204">Therefore, you cannot replace hello current value by adding a new record and removing hello existing record, as for other record types.</span></span>

<span data-ttu-id="9770b-205">Utilizzare invece un record CNAME, toomodify `az network dns record-set cname set-record`.</span><span class="sxs-lookup"><span data-stu-id="9770b-205">Instead, toomodify a CNAME record, use `az network dns record-set cname set-record`.</span></span> <span data-ttu-id="9770b-206">Per altre informazioni, vedere `az network dns record-set cname set-record --help`</span><span class="sxs-lookup"><span data-stu-id="9770b-206">For help, see `az network dns record-set cname set-record --help`</span></span>

<span data-ttu-id="9770b-207">esempio Hello Modifica set di record CNAME hello *www* nella zona hello *contoso.com*, nel gruppo di risorse *MyResourceGroup*, toopoint troppo 'www.fabrikam.net' anziché il relativo valore esistente:</span><span class="sxs-lookup"><span data-stu-id="9770b-207">hello example modifies hello CNAME record set *www* in hello zone *contoso.com*, in resource group *MyResourceGroup*, toopoint too'www.fabrikam.net' instead of its existing value:</span></span>

```azurecli
az network dns record-set cname set-record --resource-group myresourcegroup --zone-name contoso.com --record-set-name test-cname --cname www.fabrikam.net
``` 

### <a name="toomodify-an-soa-record"></a><span data-ttu-id="9770b-208">un record SOA toomodify</span><span class="sxs-lookup"><span data-stu-id="9770b-208">toomodify an SOA record</span></span>

<span data-ttu-id="9770b-209">A differenza della maggior parte degli altri tipi di record, un set di record CNAME può contenere solo un singolo record.</span><span class="sxs-lookup"><span data-stu-id="9770b-209">Unlike most other record types, a CNAME record set can only contain a single record.</span></span>  <span data-ttu-id="9770b-210">Pertanto, non è possibile sostituire il valore corrente di hello aggiungendo un nuovo record e rimozione del record esistente hello, come per altri tipi di record.</span><span class="sxs-lookup"><span data-stu-id="9770b-210">Therefore, you cannot replace hello current value by adding a new record and removing hello existing record, as for other record types.</span></span>

<span data-ttu-id="9770b-211">Utilizzare invece toomodify hello record SOA, `az network dns record-set soa update`.</span><span class="sxs-lookup"><span data-stu-id="9770b-211">Instead, toomodify hello SOA record, use `az network dns record-set soa update`.</span></span> <span data-ttu-id="9770b-212">Per altre informazioni, vedere `az network dns record-set soa update --help`.</span><span class="sxs-lookup"><span data-stu-id="9770b-212">For help, see `az network dns record-set soa update --help`.</span></span>

<span data-ttu-id="9770b-213">Hello esempio seguente viene illustrato come proprietà tooset hello "email" di hello SOA registrare per la zona hello *contoso.com* nel gruppo di risorse hello *MyResourceGroup*:</span><span class="sxs-lookup"><span data-stu-id="9770b-213">hello following example shows how tooset hello 'email' property of hello SOA record for hello zone *contoso.com* in hello resource group *MyResourceGroup*:</span></span>

```azurecli
az network dns record-set soa update --resource-group myresourcegroup --zone-name contoso.com --email admin.contoso.com
```

### <a name="toomodify-ns-records-at-hello-zone-apex"></a><span data-ttu-id="9770b-214">record NS toomodify al vertice zona hello</span><span class="sxs-lookup"><span data-stu-id="9770b-214">toomodify NS records at hello zone apex</span></span>

<span data-ttu-id="9770b-215">record NS Hello impostato al vertice zona hello viene creato automaticamente con ogni zona DNS.</span><span class="sxs-lookup"><span data-stu-id="9770b-215">hello NS record set at hello zone apex is automatically created with each DNS zone.</span></span> <span data-ttu-id="9770b-216">Contiene i nomi hello della zona di hello DNS di Azure nome server toohello assegnato.</span><span class="sxs-lookup"><span data-stu-id="9770b-216">It contains hello names of hello Azure DNS name servers assigned toohello zone.</span></span>

<span data-ttu-id="9770b-217">È possibile aggiungere nomi aggiuntivi server toothis NS set di record, toosupport CO-ospitano i domini con più di un provider DNS.</span><span class="sxs-lookup"><span data-stu-id="9770b-217">You can add additional name servers toothis NS record set, toosupport co-hosting domains with more than one DNS provider.</span></span> <span data-ttu-id="9770b-218">È inoltre possibile modificare hello durata (TTL) e i metadati per questo set di record.</span><span class="sxs-lookup"><span data-stu-id="9770b-218">You can also modify hello TTL and metadata for this record set.</span></span> <span data-ttu-id="9770b-219">Tuttavia, è Impossibile rimuovere o modificare server dei nomi DNS di Azure prepopolato hello.</span><span class="sxs-lookup"><span data-stu-id="9770b-219">However, you cannot remove or modify hello pre-populated Azure DNS name servers.</span></span>

<span data-ttu-id="9770b-220">Si noti che questo si applica solo toohello NS set di record al vertice zona hello.</span><span class="sxs-lookup"><span data-stu-id="9770b-220">Note that this applies only toohello NS record set at hello zone apex.</span></span> <span data-ttu-id="9770b-221">Altri set di record NS nella zona (come le aree figlio toodelegate usato) possono essere modificati senza vincoli.</span><span class="sxs-lookup"><span data-stu-id="9770b-221">Other NS record sets in your zone (as used toodelegate child zones) can be modified without constraint.</span></span>

<span data-ttu-id="9770b-222">Hello di esempio seguente viene illustrato come tooadd un record NS di nomi aggiuntivi server toohello imposta al vertice zona hello:</span><span class="sxs-lookup"><span data-stu-id="9770b-222">hello following example shows how tooadd an additional name server toohello NS record set at hello zone apex:</span></span>

```azurecli
az network dns record-set ns set-record --resource-group myresourcegroup --zone-name contoso.com --record-set-name "@" --nsdname ns1.myotherdnsprovider.com 
```

### <a name="toomodify-hello-ttl-of-an-existing-record-set"></a><span data-ttu-id="9770b-223">Imposta toomodify hello durata (TTL) di un record esistente</span><span class="sxs-lookup"><span data-stu-id="9770b-223">toomodify hello TTL of an existing record set</span></span>

<span data-ttu-id="9770b-224">Imposta toomodify hello durata (TTL) di un record esistente, utilizzare `azure network dns record-set <record-type> update`.</span><span class="sxs-lookup"><span data-stu-id="9770b-224">toomodify hello TTL of an existing record set, use `azure network dns record-set <record-type> update`.</span></span> <span data-ttu-id="9770b-225">Per altre informazioni, vedere `azure network dns record-set <record-type> update --help`.</span><span class="sxs-lookup"><span data-stu-id="9770b-225">For help, see `azure network dns record-set <record-type> update --help`.</span></span>

<span data-ttu-id="9770b-226">Hello di esempio seguente viene illustrato come toomodify un set di record durata (TTL), in questo caso too60 secondi:</span><span class="sxs-lookup"><span data-stu-id="9770b-226">hello following example shows how toomodify a record set TTL, in this case too60 seconds:</span></span>

```azurecli
az network dns record-set a update --resource-group myresourcegroup --zone-name contoso.com --name www --set ttl=60
```

### <a name="toomodify-hello-metadata-of-an-existing-record-set"></a><span data-ttu-id="9770b-227">toomodify hello metadati di un set di record esistente</span><span class="sxs-lookup"><span data-stu-id="9770b-227">toomodify hello metadata of an existing record set</span></span>

<span data-ttu-id="9770b-228">[Set di record dei metadati](dns-zones-records.md#tags-and-metadata) può essere utilizzato tooassociate i dati specifici dell'applicazione con ogni set di record, come coppie chiave-valore.</span><span class="sxs-lookup"><span data-stu-id="9770b-228">[Record set metadata](dns-zones-records.md#tags-and-metadata) can be used tooassociate application-specific data with each record set, as key-value pairs.</span></span> <span data-ttu-id="9770b-229">impostare toomodify hello metadati di un record esistente, utilizzare `az network dns record-set <record-type> update`.</span><span class="sxs-lookup"><span data-stu-id="9770b-229">toomodify hello metadata of an existing record set, use `az network dns record-set <record-type> update`.</span></span> <span data-ttu-id="9770b-230">Per altre informazioni, vedere `az network dns record-set <record-type> update --help`.</span><span class="sxs-lookup"><span data-stu-id="9770b-230">For help, see `az network dns record-set <record-type> update --help`.</span></span>

<span data-ttu-id="9770b-231">Hello esempio seguente viene illustrato come toomodify un set di record con due voci di metadati, "dept = finance" e "ambiente = produzione".</span><span class="sxs-lookup"><span data-stu-id="9770b-231">hello following example shows how toomodify a record set with two metadata entries, "dept=finance" and "environment=production".</span></span> <span data-ttu-id="9770b-232">Si noti che i metadati esistenti sono *sostituito* da valori hello specificato.</span><span class="sxs-lookup"><span data-stu-id="9770b-232">Note that any existing metadata is *replaced* by hello values given.</span></span>

```azurecli
az network dns record-set a update --resource-group myresourcegroup --zone-name contoso.com --name www --set metadata.dept=finance metadata.environment=production
```

## <a name="delete-a-record-set"></a><span data-ttu-id="9770b-233">Eliminare un set di record</span><span class="sxs-lookup"><span data-stu-id="9770b-233">Delete a record set</span></span>

<span data-ttu-id="9770b-234">Set di record possono essere eliminate utilizzando hello `az network dns record-set <record-type> delete` comando.</span><span class="sxs-lookup"><span data-stu-id="9770b-234">Record sets can be deleted by using hello `az network dns record-set <record-type> delete` command.</span></span> <span data-ttu-id="9770b-235">Per altre informazioni, vedere `azure network dns record-set <record-type> delete --help`.</span><span class="sxs-lookup"><span data-stu-id="9770b-235">For help, see `azure network dns record-set <record-type> delete --help`.</span></span> <span data-ttu-id="9770b-236">L'eliminazione di un set di record elimina inoltre tutti i record all'interno del set di record hello.</span><span class="sxs-lookup"><span data-stu-id="9770b-236">Deleting a record set also deletes all records within hello record set.</span></span>

> [!NOTE]
> <span data-ttu-id="9770b-237">Non è possibile eliminare hello SOA e NS set di record al vertice zona hello (`--name "@"`).</span><span class="sxs-lookup"><span data-stu-id="9770b-237">You cannot delete hello SOA and NS record sets at hello zone apex (`--name "@"`).</span></span>  <span data-ttu-id="9770b-238">Vengono creati automaticamente quando è stato creato, zona hello e vengono eliminati automaticamente quando viene eliminata hello.</span><span class="sxs-lookup"><span data-stu-id="9770b-238">These are created automatically when hello zone was created, and are deleted automatically when hello zone is deleted.</span></span>

<span data-ttu-id="9770b-239">esempio Hello Elimina record hello set denominato *www* di tipo dall'area hello *contoso.com* nel gruppo di risorse *MyResourceGroup*:</span><span class="sxs-lookup"><span data-stu-id="9770b-239">hello following example deletes hello record set named *www* of type A from hello zone *contoso.com* in resource group *MyResourceGroup*:</span></span>

```azurecli
az network dns record-set a delete --resource-group myresourcegroup --zone-name contoso.com --name www
```

<span data-ttu-id="9770b-240">Si è richiesta tooconfirm hello operazione di eliminazione.</span><span class="sxs-lookup"><span data-stu-id="9770b-240">You are prompted tooconfirm hello delete operation.</span></span> <span data-ttu-id="9770b-241">toosuppress questo prompt dei comandi, utilizzare hello `--yes` passare.</span><span class="sxs-lookup"><span data-stu-id="9770b-241">toosuppress this prompt, use hello `--yes` switch.</span></span>

## <a name="next-steps"></a><span data-ttu-id="9770b-242">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="9770b-242">Next steps</span></span>

<span data-ttu-id="9770b-243">Altre informazioni su [zone e record nel servizio DNS di Azure](dns-zones-records.md).</span><span class="sxs-lookup"><span data-stu-id="9770b-243">Learn more about [zones and records in Azure DNS](dns-zones-records.md).</span></span>
<br>
<span data-ttu-id="9770b-244">Informazioni su come troppo[proteggere le zone e record](dns-protect-zones-recordsets.md) quando si utilizza il DNS di Azure.</span><span class="sxs-lookup"><span data-stu-id="9770b-244">Learn how too[protect your zones and records](dns-protect-zones-recordsets.md) when using Azure DNS.</span></span>

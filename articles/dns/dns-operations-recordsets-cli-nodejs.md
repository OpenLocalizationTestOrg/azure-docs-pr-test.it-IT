---
title: Gestire record DNS in DNS di Azure usando l'interfaccia della riga di comando 1.0 | Microsoft Docs
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
ms.openlocfilehash: 307b327e4c04a0461e39930114eb193791cbda9a
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="manage-dns-records-in-azure-dns-using-the-azure-cli-10"></a><span data-ttu-id="50756-104">Gestire record DNS in DNS di Azure con l'interfaccia della riga di comando 1.0</span><span class="sxs-lookup"><span data-stu-id="50756-104">Manage DNS records in Azure DNS using the Azure CLI 1.0</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="50756-105">portale di Azure</span><span class="sxs-lookup"><span data-stu-id="50756-105">Azure Portal</span></span>](dns-operations-recordsets-portal.md)
> * [<span data-ttu-id="50756-106">Interfaccia della riga di comando di Azure 1.0</span><span class="sxs-lookup"><span data-stu-id="50756-106">Azure CLI 1.0</span></span>](dns-operations-recordsets-cli-nodejs.md)
> * [<span data-ttu-id="50756-107">Interfaccia della riga di comando di Azure 2.0</span><span class="sxs-lookup"><span data-stu-id="50756-107">Azure CLI 2.0</span></span>](dns-operations-recordsets-cli.md)
> * [<span data-ttu-id="50756-108">PowerShell</span><span class="sxs-lookup"><span data-stu-id="50756-108">PowerShell</span></span>](dns-operations-recordsets.md)

<span data-ttu-id="50756-109">Questo articolo descrive come gestire i record DNS per la zona DNS usando l'interfaccia della riga di comando multipiattaforma di Azure, disponibile per Windows, Mac e Linux.</span><span class="sxs-lookup"><span data-stu-id="50756-109">This article shows you how to manage DNS records for your DNS zone by using the cross-platform Azure command-line interface (CLI), which is available for Windows, Mac and Linux.</span></span> <span data-ttu-id="50756-110">È anche possibile gestire i record DNS con [Azure PowerShell](dns-operations-recordsets.md) o il [portale di Azure](dns-operations-recordsets-portal.md).</span><span class="sxs-lookup"><span data-stu-id="50756-110">You can also manage your DNS records using [Azure PowerShell](dns-operations-recordsets.md) or the [Azure portal](dns-operations-recordsets-portal.md).</span></span>

## <a name="cli-versions-to-complete-the-task"></a><span data-ttu-id="50756-111">Versioni dell'interfaccia della riga di comando per completare l'attività</span><span class="sxs-lookup"><span data-stu-id="50756-111">CLI versions to complete the task</span></span>

<span data-ttu-id="50756-112">È possibile completare l'attività usando una delle versioni seguenti dell'interfaccia della riga di comando:</span><span class="sxs-lookup"><span data-stu-id="50756-112">You can complete the task using one of the following CLI versions:</span></span>

* <span data-ttu-id="50756-113">[Interfaccia della riga di comando di Azure 1.0](dns-operations-recordsets-cli-nodejs.md): l'interfaccia della riga di comando per il modello di distribuzione classico e di gestione delle risorse.</span><span class="sxs-lookup"><span data-stu-id="50756-113">[Azure CLI 1.0](dns-operations-recordsets-cli-nodejs.md) - our CLI for the classic and resource management deployment models.</span></span>
* <span data-ttu-id="50756-114">[Interfaccia della riga di comando di Azure 2.0](dns-operations-recordsets-cli.md): interfaccia avanzata per il modello di distribuzione di gestione delle risorse.</span><span class="sxs-lookup"><span data-stu-id="50756-114">[Azure CLI 2.0](dns-operations-recordsets-cli.md) - our next generation CLI for the resource management deployment model.</span></span>

<span data-ttu-id="50756-115">Gli esempi contenuti in questo articolo presuppongono che l'utente abbia [installato l'interfaccia della riga di comando di Azure 1.0, eseguito l'accesso e creato una zona DNS](dns-operations-dnszones-cli-nodejs.md).</span><span class="sxs-lookup"><span data-stu-id="50756-115">The examples in this article assume you have already [installed the Azure CLI 1.0, signed in, and created a DNS zone](dns-operations-dnszones-cli-nodejs.md).</span></span>

## <a name="introduction"></a><span data-ttu-id="50756-116">Introduzione</span><span class="sxs-lookup"><span data-stu-id="50756-116">Introduction</span></span>

<span data-ttu-id="50756-117">Prima di creare record DNS nel servizio DNS di Azure, è necessario comprendere il modo in cui quest'ultimo organizza i record DNS nei set di record DNS.</span><span class="sxs-lookup"><span data-stu-id="50756-117">Before creating DNS records in Azure DNS, you first need to understand how Azure DNS organizes DNS records into DNS record sets.</span></span>

[!INCLUDE [dns-about-records-include](../../includes/dns-about-records-include.md)]

<span data-ttu-id="50756-118">Per altre informazioni sui record DNS nel servizio DNS di Azure, vedere [Zone e record DNS](dns-zones-records.md).</span><span class="sxs-lookup"><span data-stu-id="50756-118">For more information about DNS records in Azure DNS, see [DNS zones and records](dns-zones-records.md).</span></span>

## <a name="create-a-dns-record"></a><span data-ttu-id="50756-119">Creare un record DNS</span><span class="sxs-lookup"><span data-stu-id="50756-119">Create a DNS record</span></span>

<span data-ttu-id="50756-120">Per creare un record DNS, usare il comando `azure network dns record-set add-record`.</span><span class="sxs-lookup"><span data-stu-id="50756-120">To create a DNS record, use the `azure network dns record-set add-record` command.</span></span> <span data-ttu-id="50756-121">Per altre informazioni, vedere `azure network dns record-set add-record -h`.</span><span class="sxs-lookup"><span data-stu-id="50756-121">For help, see `azure network dns record-set add-record -h`.</span></span>

<span data-ttu-id="50756-122">Quando si crea un record è necessario specificare il nome del gruppo di risorse, della zona e del set di record, il tipo di record e i dettagli del record da creare.</span><span class="sxs-lookup"><span data-stu-id="50756-122">When creating a record, you need to specify the resource group name, zone name, record set name, the record type, and the details of the record being created.</span></span> <span data-ttu-id="50756-123">Il nome assegnato al set di record deve essere un nome *relativo*, ovvero deve escludere il nome della zona.</span><span class="sxs-lookup"><span data-stu-id="50756-123">The record set name given must be a *relative* name, meaning it must exclude the zone name.</span></span>

<span data-ttu-id="50756-124">Il comando crea il set di record, se non esiste già.</span><span class="sxs-lookup"><span data-stu-id="50756-124">If the record set does not already exist, this command creates it for you.</span></span> <span data-ttu-id="50756-125">In caso contrario, il comando aggiunge il record specificato al set di record esistente.</span><span class="sxs-lookup"><span data-stu-id="50756-125">If the record set already exists, this command adda the record you specify to the existing record set.</span></span>

<span data-ttu-id="50756-126">Se viene creato un nuovo set di record, per la durata (TTL) viene usato un valore predefinito di 3600.</span><span class="sxs-lookup"><span data-stu-id="50756-126">If a new record set is created, a default time-to-live (TTL) of 3600 is used.</span></span> <span data-ttu-id="50756-127">Per istruzioni su come usare TTL diversi, vedere [Creare un set di record DNS](#create-a-dns-record-set).</span><span class="sxs-lookup"><span data-stu-id="50756-127">For instructions on how to use different TTLs, see [Create a DNS record set](#create-a-dns-record-set).</span></span>

<span data-ttu-id="50756-128">L'esempio seguente mostra come creare un record "A" denominato *www* nella zona *contoso.com* nel gruppo di risorse *MyResourceGroup*.</span><span class="sxs-lookup"><span data-stu-id="50756-128">The following example creates an A record called *www* in the zone *contoso.com* in the resource group *MyResourceGroup*.</span></span> <span data-ttu-id="50756-129">L'indirizzo IP del record "A" è *1.2.3.4*.</span><span class="sxs-lookup"><span data-stu-id="50756-129">The IP address of the A record is *1.2.3.4*.</span></span>

```azurecli
azure network dns record-set add-record MyResourceGroup contoso.com www A -a 1.2.3.4
```

<span data-ttu-id="50756-130">Per creare un record nel dominio radice, in questo caso "contoso.com", usare il nome record "@", incluse le virgolette:</span><span class="sxs-lookup"><span data-stu-id="50756-130">To create a record in the apex of the zone (in this case, "contoso.com"), use the record name "@", including the quotation marks:</span></span>

```azurecli
azure network dns record-set add-record MyResourceGroup contoso.com "@" A -a 1.2.3.4
```

## <a name="create-a-dns-record-set"></a><span data-ttu-id="50756-131">Creare un set di record DNS</span><span class="sxs-lookup"><span data-stu-id="50756-131">Create a DNS record set</span></span>

<span data-ttu-id="50756-132">Negli esempi precedenti, il record DNS è stato aggiunto a un set di record esistente oppure il set di record è stato creato *in modo implicito*.</span><span class="sxs-lookup"><span data-stu-id="50756-132">In the above examples, the DNS record was either added to an existing record set, or the record set was created *implicitly*.</span></span> <span data-ttu-id="50756-133">È anche possibile creare il set di record *in modo esplicito* prima di aggiungere i record.</span><span class="sxs-lookup"><span data-stu-id="50756-133">You can also create the record set *explicitly* before adding records to it.</span></span> <span data-ttu-id="50756-134">Il servizio DNS di Azure supporta set di record vuoti, che possono fungere da segnaposto per riservare un nome DNS prima della creazione di record DNS.</span><span class="sxs-lookup"><span data-stu-id="50756-134">Azure DNS supports 'empty' record sets, which can act as a placeholder to reserve a DNS name before creating DNS records.</span></span> <span data-ttu-id="50756-135">I set di record vuoti sono visibili nel piano di controllo del servizio DNS di Azure, ma non vengono visualizzati nei server dei nomi del servizio DNS di Azure.</span><span class="sxs-lookup"><span data-stu-id="50756-135">Empty record sets are visible in the Azure DNS control plane, but do not appear on the Azure DNS name servers.</span></span>

<span data-ttu-id="50756-136">I set di record vengono creati usando il comando `azure network dns record-set create`.</span><span class="sxs-lookup"><span data-stu-id="50756-136">Record sets are created using the `azure network dns record-set create` command.</span></span> <span data-ttu-id="50756-137">Per altre informazioni, vedere `azure network dns record-set create -h`.</span><span class="sxs-lookup"><span data-stu-id="50756-137">For help, see `azure network dns record-set create -h`.</span></span>

<span data-ttu-id="50756-138">La creazione esplicita del set di record consente di specificare proprietà per il set come [Durata (TTL)](dns-zones-records.md#time-to-live) e metadati.</span><span class="sxs-lookup"><span data-stu-id="50756-138">Creating the record set explicitly allows you to specify record set properties such as the [Time-To-Live (TTL)](dns-zones-records.md#time-to-live) and metadata.</span></span> <span data-ttu-id="50756-139">È possibile usare i [metadati del set di record](dns-zones-records.md#tags-and-metadata) per associare dati specifici dell'applicazione a ogni set di record, sotto forma di coppie chiave-valore.</span><span class="sxs-lookup"><span data-stu-id="50756-139">[Record set metadata](dns-zones-records.md#tags-and-metadata) can be used to associate application-specific data with each record set, as key-value pairs.</span></span>

<span data-ttu-id="50756-140">L'esempio seguente crea un set di record vuoto impostato con un TTL di 60 secondi, usando il parametro `--ttl` (forma breve `-l`):</span><span class="sxs-lookup"><span data-stu-id="50756-140">The following example creates an empty record set with a 60-second TTL, by using the `--ttl` parameter (short form `-l`):</span></span>

```azurecli
azure network dns record-set create MyResourceGroup contoso.com www A --ttl 60
```

<span data-ttu-id="50756-141">L'esempio seguente crea un set di record con due voci di metadati, "dept=finance" e "environment=production", usando il parametro `--metadata` (forma breve `-m`):</span><span class="sxs-lookup"><span data-stu-id="50756-141">The following example creates a record set with two metadata entries, "dept=finance" and "environment=production", by using the `--metadata` parameter (short form `-m`):</span></span>

```azurecli
azure network dns record-set create MyResourceGroup contoso.com www A --metadata "dept=finance;environment=production"
```

<span data-ttu-id="50756-142">Dopo aver creato un set di record vuoto, è possibile aggiungervi i record usando `azure network dns record-set add-record` come descritto in [Creare un record DNS](#create-a-dns-record).</span><span class="sxs-lookup"><span data-stu-id="50756-142">Having created an empty record set, records can be added using `azure network dns record-set add-record` as described in [Create a DNS record](#create-a-dns-record).</span></span>

## <a name="create-records-of-other-types"></a><span data-ttu-id="50756-143">Creare record di altri tipi</span><span class="sxs-lookup"><span data-stu-id="50756-143">Create records of other types</span></span>

<span data-ttu-id="50756-144">Dopo aver visto in dettaglio come creare record di tipo A, gli esempi seguenti illustrano come creare record di altri tipi supportati dal servizio DNS di Azure.</span><span class="sxs-lookup"><span data-stu-id="50756-144">Having seen in detail how to create 'A' records, the following examples show how to create record of other record types supported by Azure DNS.</span></span>

<span data-ttu-id="50756-145">I parametri usati per specificare i dati del record variano a seconda del tipo di record.</span><span class="sxs-lookup"><span data-stu-id="50756-145">The parameters used to specify the record data vary depending on the type of the record.</span></span> <span data-ttu-id="50756-146">Per un record di tipo "A", ad esempio, specificare l'indirizzo IPv4 con il parametro `-a <IPv4 address>`.</span><span class="sxs-lookup"><span data-stu-id="50756-146">For example, for a record of type "A", you specify the IPv4 address with the parameter `-a <IPv4 address>`.</span></span> <span data-ttu-id="50756-147">I parametri per ogni tipo di record possono essere elencati usando `azure network dns record-set add-record -h`.</span><span class="sxs-lookup"><span data-stu-id="50756-147">The parameters for each record type can be listed using `azure network dns record-set add-record -h`.</span></span>

<span data-ttu-id="50756-148">In ogni caso viene illustrato come creare un record singolo.</span><span class="sxs-lookup"><span data-stu-id="50756-148">In each case, we show how to create a single record.</span></span> <span data-ttu-id="50756-149">Il record viene aggiunto al set di record esistente oppure viene creato un set di record in modo implicito.</span><span class="sxs-lookup"><span data-stu-id="50756-149">The record is added to the existing record set, or a record set created implicitly.</span></span> <span data-ttu-id="50756-150">Per ulteriori informazioni sulla creazione di set di record e sulla definizione esplicita dei parametri di un set di record, vedere [Creare un set di record DNS](#create-a-dns-record-set).</span><span class="sxs-lookup"><span data-stu-id="50756-150">For more information on creating record sets and defining record set parameter explicitly, see [Create a DNS record set](#create-a-dns-record-set).</span></span>

<span data-ttu-id="50756-151">Non vengono forniti esempi per la creazione di set di record SOA, dato che vengono creati ed eliminati con ogni zona DNS e non è possibile crearli o eliminarli separatamente.</span><span class="sxs-lookup"><span data-stu-id="50756-151">We do not give an example to create an SOA record set, since SOAs are created and deleted with each DNS zone and cannot be created or deleted separately.</span></span> <span data-ttu-id="50756-152">Tuttavia, [è possibile modificare i record SOA, come illustrato in uno degli esempi successivi](#to-modify-an-SOA-record).</span><span class="sxs-lookup"><span data-stu-id="50756-152">However, [the SOA can be modified, as shown in a later example](#to-modify-an-SOA-record).</span></span>

### <a name="create-an-aaaa-record"></a><span data-ttu-id="50756-153">Creare un record AAAA</span><span class="sxs-lookup"><span data-stu-id="50756-153">Create an AAAA record</span></span>

```azurecli
azure network dns record-set add-record MyResourceGroup contoso.com test-aaaa AAAA --ipv6-address 2607:f8b0:4009:1803::1005
```

### <a name="create-a-cname-record"></a><span data-ttu-id="50756-154">Creare un record CNAME</span><span class="sxs-lookup"><span data-stu-id="50756-154">Create a CNAME record</span></span>

> [!NOTE]
> <span data-ttu-id="50756-155">Gli standard DNS non accettano record CNAME nel dominio radice di una zona (`-Name "@"`) né set di record contenenti più di un record.</span><span class="sxs-lookup"><span data-stu-id="50756-155">The DNS standards do not permit CNAME records at the apex of a zone (`-Name "@"`), nor do they permit record sets containing more than one record.</span></span>
> 
> <span data-ttu-id="50756-156">Per altre informazioni, vedere[Record CNAME](dns-zones-records.md#cname-records).</span><span class="sxs-lookup"><span data-stu-id="50756-156">For more information, see [CNAME records](dns-zones-records.md#cname-records).</span></span>

```azurecli
azure network dns record-set add-record  MyResourceGroup contoso.com  test-cname CNAME --cname www.contoso.com
```

### <a name="create-an-mx-record"></a><span data-ttu-id="50756-157">Creare un record MX</span><span class="sxs-lookup"><span data-stu-id="50756-157">Create an MX record</span></span>

<span data-ttu-id="50756-158">In questo esempio viene usato il nome del set di record "@" per creare il record MX al vertice della zona, in questo caso "contoso.com".</span><span class="sxs-lookup"><span data-stu-id="50756-158">In this example, we use the record set name "@" to create the MX record at the zone apex (in this case, "contoso.com").</span></span>

```azurecli
azure network dns record-set add-record MyResourceGroup contoso.com  "@" MX --exchange mail.contoso.com --preference 5
```

### <a name="create-an-ns-record"></a><span data-ttu-id="50756-159">Creare un record NS</span><span class="sxs-lookup"><span data-stu-id="50756-159">Create an NS record</span></span>

```azurecli
azure network dns record-set add-record MyResourceGroup  contoso.com  test-ns NS --nsdname ns1.contoso.com
```

### <a name="create-a-ptr-record"></a><span data-ttu-id="50756-160">Creare un record PTR</span><span class="sxs-lookup"><span data-stu-id="50756-160">Create a PTR record</span></span>

<span data-ttu-id="50756-161">In questo caso "my-arpa-zone.com" è la zona ARPA che rappresenta l'intervallo IP dell'utente.</span><span class="sxs-lookup"><span data-stu-id="50756-161">In this case, 'my-arpa-zone.com' represents the ARPA zone representing your IP range.</span></span> <span data-ttu-id="50756-162">Ogni record PTR impostato in questa zona corrisponde a un indirizzo IP che rientra nell'intervallo IP.</span><span class="sxs-lookup"><span data-stu-id="50756-162">Each PTR record set in this zone corresponds to an IP address within this IP range.</span></span>  <span data-ttu-id="50756-163">Il nome del record "10" è l'ultimo ottetto dell'indirizzo IP all'interno di questo intervallo di indirizzi rappresentato dal record.</span><span class="sxs-lookup"><span data-stu-id="50756-163">The record name '10' is the last octet of the IP address within this IP range represented by this record.</span></span>

```azurecli
azure network dns record-set add-record MyResourceGroup my-arpa-zone.com "10" PTR --ptrdname "myservice.contoso.com"
```

### <a name="create-an-srv-record"></a><span data-ttu-id="50756-164">Creare un record SRV</span><span class="sxs-lookup"><span data-stu-id="50756-164">Create an SRV record</span></span>

<span data-ttu-id="50756-165">Quando si crea un [set di record SRV](dns-zones-records.md#srv-records), specificare il *\_servizio* e il *\_protocollo* nel nome del set di record.</span><span class="sxs-lookup"><span data-stu-id="50756-165">When creating an [SRV record set](dns-zones-records.md#srv-records), specify the *\_service* and *\_protocol* in the record set name.</span></span> <span data-ttu-id="50756-166">Non è necessario includere "@" nel nome del set di record durante la creazione di un set di record SRV nel dominio radice della zona.</span><span class="sxs-lookup"><span data-stu-id="50756-166">There is no need to include "@" in the record set name when creating an SRV record set at the zone apex.</span></span>

```azurecli
azure network dns record-set add-record MyResourceGroup contoso.com  "_sip._tls" SRV --priority 10 --weight 5 --port 8080 --target "sip.contoso.com"
```

### <a name="create-a-txt-record"></a><span data-ttu-id="50756-167">Creare un record TXT</span><span class="sxs-lookup"><span data-stu-id="50756-167">Create a TXT record</span></span>

<span data-ttu-id="50756-168">L'esempio seguente mostra come creare un record TXT.</span><span class="sxs-lookup"><span data-stu-id="50756-168">The following example shows how to create a TXT record.</span></span> <span data-ttu-id="50756-169">Per altre informazioni sulla lunghezza massima delle stringhe supportata nei record TXT, vedere [Record TXT](dns-zones-records.md#txt-records).</span><span class="sxs-lookup"><span data-stu-id="50756-169">For more information about the maximum string length supported in TXT records, see [TXT records](dns-zones-records.md#txt-records).</span></span>

```azurecli
azure network dns record-set add-record MyResourceGroup contoso.com test-txt TXT --text "This is a TXT record"
```

## <a name="get-a-record-set"></a><span data-ttu-id="50756-170">Ottenere un set di record</span><span class="sxs-lookup"><span data-stu-id="50756-170">Get a record set</span></span>

<span data-ttu-id="50756-171">Per recuperare un set di record esistente, usare `azure network dns record-set show`.</span><span class="sxs-lookup"><span data-stu-id="50756-171">To retrieve an existing record set, use `azure network dns record-set show`.</span></span> <span data-ttu-id="50756-172">Per altre informazioni, vedere `azure network dns record-set show -h`.</span><span class="sxs-lookup"><span data-stu-id="50756-172">For help, see `azure network dns record-set show -h`.</span></span>

<span data-ttu-id="50756-173">Come per la creazione di un record o di un set di record, il nome assegnato al set di record deve essere un nome *relativo*, ovvero deve escludere il nome della zona.</span><span class="sxs-lookup"><span data-stu-id="50756-173">As when creating a record or record set, the record set name given must be a *relative* name, meaning it must exclude the zone name.</span></span> <span data-ttu-id="50756-174">È anche necessario specificare il tipo di record, la zona contenente il set di record e il gruppo di risorse contenente la zona.</span><span class="sxs-lookup"><span data-stu-id="50756-174">You also need to specify the record type, the zone containing the record set, and the resource group containing the zone.</span></span>

<span data-ttu-id="50756-175">L'esempio seguente recupera il record "A" denominato *www* nella zona *contoso.com* nel gruppo di risorse *MyResourceGroup*:</span><span class="sxs-lookup"><span data-stu-id="50756-175">The following example retrieves the record *www* of type A from zone *contoso.com* in resource group *MyResourceGroup*:</span></span>

```azurecli
azure network dns record-set show MyResourceGroup contoso.com www A
```

## <a name="list-record-sets"></a><span data-ttu-id="50756-176">Elencare i set di record</span><span class="sxs-lookup"><span data-stu-id="50756-176">List record sets</span></span>

<span data-ttu-id="50756-177">È possibile elencare tutti i record in una zona DNS usando il comando `azure network dns record-set list` .</span><span class="sxs-lookup"><span data-stu-id="50756-177">You can list all records in a DNS zone by using the `azure network dns record-set list` command.</span></span> <span data-ttu-id="50756-178">Per altre informazioni, vedere `azure network dns record-set list -h`.</span><span class="sxs-lookup"><span data-stu-id="50756-178">For help, see `azure network dns record-set list -h`.</span></span>

<span data-ttu-id="50756-179">Questo esempio restituisce tutti i set di record nella zona *contoso.com* nel gruppo di risorse *MyResourceGroup*, a prescindere dal nome o dal tipo di record:</span><span class="sxs-lookup"><span data-stu-id="50756-179">This example returns all record sets in the zone *contoso.com*, in resource group *MyResourceGroup*, regardless of name or record type:</span></span>

```azurecli
azure network dns record-set list MyResourceGroup contoso.com
```

<span data-ttu-id="50756-180">Questo esempio restituisce tutti i set di record corrispondenti al tipo di record specificato, in questo caso, i record "A":</span><span class="sxs-lookup"><span data-stu-id="50756-180">This example returns all record sets that match the given record type (in this case, 'A' records):</span></span>

```azurecli
azure network dns record-set list MyResourceGroup contoso.com --type A
```

## <a name="add-a-record-to-an-existing-record-set"></a><span data-ttu-id="50756-181">Aggiungere un record a un set di record esistente</span><span class="sxs-lookup"><span data-stu-id="50756-181">Add a record to an existing record set</span></span>

<span data-ttu-id="50756-182">È possibile usare `azure network dns record-set add-record` sia per creare un record in un nuovo set di record che per aggiungere un record a un set di record esistente.</span><span class="sxs-lookup"><span data-stu-id="50756-182">You can use `azure network dns record-set add-record` both to create a record in a new record set, or to add a record to an existing record set.</span></span>

<span data-ttu-id="50756-183">Per ulteriori informazioni, vedere [Creare un record DNS](#create-a-dns-record) e [Creare record di altri tipi](#create-records-of-other-types) sopra.</span><span class="sxs-lookup"><span data-stu-id="50756-183">For more information, see [Create a DNS record](#create-a-dns-record) and [Create records of other types](#create-records-of-other-types) above.</span></span>

## <a name="remove-a-record-from-an-existing-record-set"></a><span data-ttu-id="50756-184">Rimuovere un record da un set di record esistente.</span><span class="sxs-lookup"><span data-stu-id="50756-184">Remove a record from an existing record set.</span></span>

<span data-ttu-id="50756-185">Per rimuovere un record DNS da un set di record esistente, usare `azure network dns record-set delete-record`.</span><span class="sxs-lookup"><span data-stu-id="50756-185">To remove a DNS record from an existing record set, use `azure network dns record-set delete-record`.</span></span> <span data-ttu-id="50756-186">Per altre informazioni, vedere `azure network dns record-set delete-record -h`.</span><span class="sxs-lookup"><span data-stu-id="50756-186">For help, see `azure network dns record-set delete-record -h`.</span></span>

<span data-ttu-id="50756-187">Questo comando elimina un record DNS da un set di record.</span><span class="sxs-lookup"><span data-stu-id="50756-187">This command deletes a DNS record from a record set.</span></span> <span data-ttu-id="50756-188">Se viene eliminato l'ultimo record in un set di record, **non** viene eliminato anche il set stesso.</span><span class="sxs-lookup"><span data-stu-id="50756-188">If the last record in a record set is deleted, the record set itself is **not** deleted.</span></span> <span data-ttu-id="50756-189">Si avrà invece un set di record vuoto.</span><span class="sxs-lookup"><span data-stu-id="50756-189">Instead, an empty record set is left.</span></span> <span data-ttu-id="50756-190">Per eliminare il set di record, vedere [Eliminare un set di record](#delete-a-record-set).</span><span class="sxs-lookup"><span data-stu-id="50756-190">To delete the record set instead, see [Delete a record set](#delete-a-record-set).</span></span>

<span data-ttu-id="50756-191">È necessario specificare il record da eliminare e la zona da cui eliminarlo usando gli stessi parametri di quando si crea un record tramite `azure network dns record-set add-record`.</span><span class="sxs-lookup"><span data-stu-id="50756-191">You need to specify the record to be deleted and the zone it should be deleted from, using the same parameters as when creating a record using `azure network dns record-set add-record`.</span></span> <span data-ttu-id="50756-192">I parametri vengono descritti in [Creare un record DNS](#create-a-dns-record) e [Creare record di altri tipi](#create-records-of-other-types) sopra.</span><span class="sxs-lookup"><span data-stu-id="50756-192">These parameters are described in [Create a DNS record](#create-a-dns-record) and [Create records of other types](#create-records-of-other-types) above.</span></span>

<span data-ttu-id="50756-193">Questo comando richiede una conferma.</span><span class="sxs-lookup"><span data-stu-id="50756-193">This command prompts for confirmation.</span></span> <span data-ttu-id="50756-194">Questo messaggio può essere soppresso mediante lo switch `--quiet` (forma breve `-q`).</span><span class="sxs-lookup"><span data-stu-id="50756-194">This prompt can be suppressed using the `--quiet` switch (short form `-q`).</span></span>

<span data-ttu-id="50756-195">L'esempio seguente elimina il record "A" con valore "1.2.3.4" dal set di record denominato *www* nella zona *contoso.com* nel gruppo di risorse *MyResourceGroup*.</span><span class="sxs-lookup"><span data-stu-id="50756-195">The following example deletes the A record with value '1.2.3.4' from the record set named *www* in the zone *contoso.com*, in the resource group *MyResourceGroup*.</span></span> <span data-ttu-id="50756-196">La richiesta di conferma viene soppressa.</span><span class="sxs-lookup"><span data-stu-id="50756-196">The confirmation prompt is suppressed.</span></span>

```azurecli
azure network dns record-set delete-record MyResourceGroup contoso.com www A -a 1.2.3.4 --quiet
```

## <a name="modify-an-existing-record-set"></a><span data-ttu-id="50756-197">Modificare un set di record esistente</span><span class="sxs-lookup"><span data-stu-id="50756-197">Modify an existing record set</span></span>

<span data-ttu-id="50756-198">Ogni set di record contiene un [time-to-live (TTL)](dns-zones-records.md#time-to-live), [metadati](dns-zones-records.md#tags-and-metadata) e record DNS.</span><span class="sxs-lookup"><span data-stu-id="50756-198">Each record set contains a [time-to-live (TTL)](dns-zones-records.md#time-to-live), [metadata](dns-zones-records.md#tags-and-metadata), and DNS records.</span></span> <span data-ttu-id="50756-199">Nelle sezioni seguenti viene illustrato come modificare ognuna di queste proprietà.</span><span class="sxs-lookup"><span data-stu-id="50756-199">The following sections explain how to modify each of these properties.</span></span>

### <a name="to-modify-an-a-aaaa-mx-ns-ptr-srv-or-txt-record"></a><span data-ttu-id="50756-200">Per modificare un record A, AAAA, MX, NS, PTR, SRV o TXT</span><span class="sxs-lookup"><span data-stu-id="50756-200">To modify an A, AAAA, MX, NS, PTR, SRV, or TXT record</span></span>

<span data-ttu-id="50756-201">Per modificare un record esistente di tipo A, AAAA, MX, NS, PTR, SRV o TXT è necessario innanzitutto aggiungere un nuovo record e quindi eliminare il record esistente.</span><span class="sxs-lookup"><span data-stu-id="50756-201">To modify an existing record of type A, AAAA, MX, NS, PTR, SRV, or TXT, you should first add a new record and then delete the existing record.</span></span> <span data-ttu-id="50756-202">Per istruzioni dettagliate su come eliminare e aggiungere record, vedere le sezioni precedenti di questo articolo.</span><span class="sxs-lookup"><span data-stu-id="50756-202">For detailed instructions on how to delete and add records, see the earlier sections of this article.</span></span>

<span data-ttu-id="50756-203">Nell'esempio seguente viene illustrato come modificare un record "A", dall'indirizzo IP 1.2.3.4 all'indirizzo IP 5.6.7.8:</span><span class="sxs-lookup"><span data-stu-id="50756-203">The following example shows how to modify an 'A' record, from IP address 1.2.3.4 to IP address 5.6.7.8:</span></span>

```azurecli
azure network dns record-set add-record MyResourceGroup contoso.com www A -a 5.6.7.8
azure network dns record-set delete-record MyResourceGroup contoso.com www A -a 1.2.3.4
```

### <a name="to-modify-a-cname-record"></a><span data-ttu-id="50756-204">Per modificare un record CNAME</span><span class="sxs-lookup"><span data-stu-id="50756-204">To modify a CNAME record</span></span>

<span data-ttu-id="50756-205">Per modificare un record CNAME, usare `azure network dns record-set add-record` per aggiungere il nuovo valore di record.</span><span class="sxs-lookup"><span data-stu-id="50756-205">To modify a CNAME record, use `azure network dns record-set add-record` to add the new record value.</span></span> <span data-ttu-id="50756-206">A differenza di altri tipi di record, un set di record CNAME può contenere solo un singolo record.</span><span class="sxs-lookup"><span data-stu-id="50756-206">Unlike other record types, a CNAME record set can only contain a single record.</span></span> <span data-ttu-id="50756-207">Pertanto, il record esistente viene *sostituito* quando si aggiunge il nuovo record e non deve essere eliminato separatamente.</span><span class="sxs-lookup"><span data-stu-id="50756-207">Therefore, the existing record is *replaced* when the new record is added, and does not need to be deleted separately.</span></span>  <span data-ttu-id="50756-208">Verrà richiesto di accettare la sostituzione.</span><span class="sxs-lookup"><span data-stu-id="50756-208">You will be prompted to accept this replacement.</span></span>

<span data-ttu-id="50756-209">Nell'esempio viene modificato il set di record CNAME *www* nella zona *contoso.com* nel gruppo di risorse *MyResourceGroup*, in modo che punti a "www.fabrikam.net" invece che al valore esistente:</span><span class="sxs-lookup"><span data-stu-id="50756-209">The example modifies the CNAME record set *www* in the zone *contoso.com*, in resource group *MyResourceGroup*, to point to 'www.fabrikam.net' instead of its existing value:</span></span>

```azurecli
azure network dns record-set add-record MyResourceGroup contoso.com www CNAME --cname www.fabrikam.net
``` 

### <a name="to-modify-an-soa-record"></a><span data-ttu-id="50756-210">Per modificare un record SOA</span><span class="sxs-lookup"><span data-stu-id="50756-210">To modify an SOA record</span></span>

<span data-ttu-id="50756-211">Usare `azure network dns record-set set-soa-record` per modificare la SOA per una zona DNS specificata.</span><span class="sxs-lookup"><span data-stu-id="50756-211">Use `azure network dns record-set set-soa-record` to modify the SOA for a given DNS zone.</span></span> <span data-ttu-id="50756-212">Per altre informazioni, vedere `azure network dns record-set set-soa-record -h`.</span><span class="sxs-lookup"><span data-stu-id="50756-212">For help, see `azure network dns record-set set-soa-record -h`.</span></span>

<span data-ttu-id="50756-213">Nell'esempio seguente viene illustrato come impostare la proprietà 
"email" del record SOA della zona *contoso.com* nel gruppo di risorse *MyResourceGroup*:</span><span class="sxs-lookup"><span data-stu-id="50756-213">The following example shows how to set the 'email' property of the SOA record for the zone *contoso.com* in the resource group *MyResourceGroup*:</span></span>

```azurecli
azure network dns record-set set-soa-record rg1 contoso.com --email admin.contoso.com
```


### <a name="to-modify-ns-records-at-the-zone-apex"></a><span data-ttu-id="50756-214">Per modificare i record NS al vertice della zona</span><span class="sxs-lookup"><span data-stu-id="50756-214">To modify NS records at the zone apex</span></span>

<span data-ttu-id="50756-215">Il set di record NS al vertice della zona viene creato automaticamente con ogni zona DNS.</span><span class="sxs-lookup"><span data-stu-id="50756-215">The NS record set at the zone apex is automatically created with each DNS zone.</span></span> <span data-ttu-id="50756-216">Contiene i nomi dei server dei nomi DNS di Azure assegnati alla zona.</span><span class="sxs-lookup"><span data-stu-id="50756-216">It contains the names of the Azure DNS name servers assigned to the zone.</span></span>

<span data-ttu-id="50756-217">È possibile aggiungere ulteriori server dei nomi a questo set di record NS per supportare domini coesistenti con più provider DNS.</span><span class="sxs-lookup"><span data-stu-id="50756-217">You can add additional name servers to this NS record set, to support co-hosting domains with more than one DNS provider.</span></span> <span data-ttu-id="50756-218">È anche possibile modificare il valore TTL e i metadati per questo set di record.</span><span class="sxs-lookup"><span data-stu-id="50756-218">You can also modify the TTL and metadata for this record set.</span></span> <span data-ttu-id="50756-219">Tuttavia, non è possibile rimuovere o modificare i server dei nomi DNS di Azure già popolati.</span><span class="sxs-lookup"><span data-stu-id="50756-219">However, you cannot remove or modify the pre-populated Azure DNS name servers.</span></span>

<span data-ttu-id="50756-220">Notare che questo si applica solo al set di record NS al vertice della zona.</span><span class="sxs-lookup"><span data-stu-id="50756-220">Note that this applies only to the NS record set at the zone apex.</span></span> <span data-ttu-id="50756-221">Gli altri set di record NS nella zona (usati per delegare le zone figlio) possono essere modificati senza vincoli.</span><span class="sxs-lookup"><span data-stu-id="50756-221">Other NS record sets in your zone (as used to delegate child zones) can be modified without constraint.</span></span>

<span data-ttu-id="50756-222">L'esempio seguente mostra come aggiungere un ulteriore server dei nomi al set di record NS al vertice della zona:</span><span class="sxs-lookup"><span data-stu-id="50756-222">The following example shows how to add an additional name server to the NS record set at the zone apex:</span></span>

```azurecli
azure network dns record-set add-record MyResourceGroup contoso.com "@" --nsdname ns1.myotherdnsprovider.com 
```

### <a name="to-modify-the-ttl-of-an-existing-record-set"></a><span data-ttu-id="50756-223">Per modificare il valore TTL di un set di record esistente</span><span class="sxs-lookup"><span data-stu-id="50756-223">To modify the TTL of an existing record set</span></span>

<span data-ttu-id="50756-224">Per modificare il valore TTL di un set di record esistente, usare `azure network dns record-set set`.</span><span class="sxs-lookup"><span data-stu-id="50756-224">To modify the TTL of an existing record set, use `azure network dns record-set set`.</span></span> <span data-ttu-id="50756-225">Per altre informazioni, vedere `azure network dns record-set set -h`.</span><span class="sxs-lookup"><span data-stu-id="50756-225">For help, see `azure network dns record-set set -h`.</span></span>

<span data-ttu-id="50756-226">Nell'esempio seguente viene illustrato come modificare il valore TTL di un set di record, impostandolo in questo caso su 60 secondi:</span><span class="sxs-lookup"><span data-stu-id="50756-226">The following example shows how to modify a record set TTL, in this case to 60 seconds:</span></span>

```azurecli
azure network dns record-set set MyResourceGroup contoso.com www A --ttl 60
```

### <a name="to-modify-the-metadata-of-an-existing-record-set"></a><span data-ttu-id="50756-227">Per modificare i metadati di un set di record esistente</span><span class="sxs-lookup"><span data-stu-id="50756-227">To modify the metadata of an existing record set</span></span>

<span data-ttu-id="50756-228">È possibile usare i [metadati del set di record](dns-zones-records.md#tags-and-metadata) per associare dati specifici dell'applicazione a ogni set di record, sotto forma di coppie chiave-valore.</span><span class="sxs-lookup"><span data-stu-id="50756-228">[Record set metadata](dns-zones-records.md#tags-and-metadata) can be used to associate application-specific data with each record set, as key-value pairs.</span></span> <span data-ttu-id="50756-229">Per modificare i metadati di un set di record esistente, usare `azure network dns record-set set`.</span><span class="sxs-lookup"><span data-stu-id="50756-229">To modify the metadata of an existing record set, use `azure network dns record-set set`.</span></span> <span data-ttu-id="50756-230">Per altre informazioni, vedere `azure network dns record-set set -h`.</span><span class="sxs-lookup"><span data-stu-id="50756-230">For help, see `azure network dns record-set set -h`.</span></span>

<span data-ttu-id="50756-231">L'esempio seguente mostra come modificare un set di record con due voci di metadati, "dept=finance" e "environment=production", usando il parametro `--metadata` (forma breve `-m`).</span><span class="sxs-lookup"><span data-stu-id="50756-231">The following example shows how to modify a record set with two metadata entries, "dept=finance" and "environment=production", by using the `--metadata` parameter (short form `-m`).</span></span> <span data-ttu-id="50756-232">Si noti che i metadati esistenti vengono *sostituiti* dai valori assegnati.</span><span class="sxs-lookup"><span data-stu-id="50756-232">Note that any existing metadata is *replaced* by the values given.</span></span>

```azurecli
azure network dns record-set set MyResourceGroup contoso.com www A --metadata "dept=finance;environment=production"
```

## <a name="delete-a-record-set"></a><span data-ttu-id="50756-233">Eliminare un set di record</span><span class="sxs-lookup"><span data-stu-id="50756-233">Delete a record set</span></span>

<span data-ttu-id="50756-234">È possibile eliminare i set di record usando il commando `azure network dns record-set delete` .</span><span class="sxs-lookup"><span data-stu-id="50756-234">Record sets can be deleted by using the `azure network dns record-set delete` command.</span></span> <span data-ttu-id="50756-235">Per altre informazioni, vedere `azure network dns record-set delete -h`.</span><span class="sxs-lookup"><span data-stu-id="50756-235">For help, see `azure network dns record-set delete -h`.</span></span> <span data-ttu-id="50756-236">Eliminando un set di record vengono eliminati anche tutti i record in esso contenuti.</span><span class="sxs-lookup"><span data-stu-id="50756-236">Deleting a record set also deletes all records within the record set.</span></span>

> [!NOTE]
> <span data-ttu-id="50756-237">Non è possibile eliminare i set di record SOA e NS dal dominio radice della zona (`-Name "@"`).</span><span class="sxs-lookup"><span data-stu-id="50756-237">You cannot delete the SOA and NS record sets at the zone apex (`-Name "@"`).</span></span>  <span data-ttu-id="50756-238">Tali set di record vengono creati automaticamente durante la creazione della zona e vengono eliminati automaticamente quando la zona viene eliminata.</span><span class="sxs-lookup"><span data-stu-id="50756-238">These are created automatically when the zone was created, and are deleted automatically when the zone is deleted.</span></span>

<span data-ttu-id="50756-239">L'esempio seguente elimina il set di record "A" denominato *www* dalla zona *contoso.com* nel gruppo di risorse *MyResourceGroup*:</span><span class="sxs-lookup"><span data-stu-id="50756-239">The following example deletes the record set named *www* of type A from the zone *contoso.com* in resource group *MyResourceGroup*:</span></span>

```azurecli
azure network dns record-set delete MyResourceGroup contoso.com www A
```

<span data-ttu-id="50756-240">Viene chiesto di confermare l'operazione di eliminazione.</span><span class="sxs-lookup"><span data-stu-id="50756-240">You are prompted to confirm the delete operation.</span></span> <span data-ttu-id="50756-241">Per eliminare la richiesta, usare lo switch `--quiet` (forma breve `-q`).</span><span class="sxs-lookup"><span data-stu-id="50756-241">To suppress this prompt, use the `--quiet` switch (short form `-q`).</span></span>

## <a name="next-steps"></a><span data-ttu-id="50756-242">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="50756-242">Next steps</span></span>

<span data-ttu-id="50756-243">Altre informazioni su [zone e record nel servizio DNS di Azure](dns-zones-records.md).</span><span class="sxs-lookup"><span data-stu-id="50756-243">Learn more about [zones and records in Azure DNS](dns-zones-records.md).</span></span>
<br>
<span data-ttu-id="50756-244">Informazioni su come [proteggere zone e record](dns-protect-zones-recordsets.md) quando si usa il servizio DNS di Azure.</span><span class="sxs-lookup"><span data-stu-id="50756-244">Learn how to [protect your zones and records](dns-protect-zones-recordsets.md) when using Azure DNS.</span></span>

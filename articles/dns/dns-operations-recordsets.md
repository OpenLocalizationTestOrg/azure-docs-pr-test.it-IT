---
title: aaaManage DNS record in DNS di Azure con Azure PowerShell | Documenti Microsoft
description: Gestione dei set di record e dei record DNS in DNS di Azure quando si ospita il dominio in DNS di Azure. Tutti i comandi di PowerShell per le operazioni sui set di record e i record.
services: dns
documentationcenter: na
author: georgewallace
manager: timlt
ms.assetid: 7136a373-0682-471c-9c28-9e00d2add9c2
ms.service: dns
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.custom: H1Hack27Feb2017
ms.workload: infrastructure-services
ms.date: 12/21/2016
ms.author: gwallace
ms.openlocfilehash: bfdf116e174d06db0514abdc0ec3f4fc4ee0a079
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="manage-dns-records-and-recordsets-in-azure-dns-using-azure-powershell"></a><span data-ttu-id="10b26-104">Gestire record e recordset DNS in DNS di Azure con Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="10b26-104">Manage DNS records and recordsets in Azure DNS using Azure PowerShell</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="10b26-105">Portale di Azure</span><span class="sxs-lookup"><span data-stu-id="10b26-105">Azure Portal</span></span>](dns-operations-recordsets-portal.md)
> * [<span data-ttu-id="10b26-106">Interfaccia della riga di comando di Azure 1.0</span><span class="sxs-lookup"><span data-stu-id="10b26-106">Azure CLI 1.0</span></span>](dns-operations-recordsets-cli-nodejs.md)
> * [<span data-ttu-id="10b26-107">Interfaccia della riga di comando di Azure 2.0</span><span class="sxs-lookup"><span data-stu-id="10b26-107">Azure CLI 2.0</span></span>](dns-operations-recordsets-cli.md)
> * [<span data-ttu-id="10b26-108">PowerShell</span><span class="sxs-lookup"><span data-stu-id="10b26-108">PowerShell</span></span>](dns-operations-recordsets.md)

<span data-ttu-id="10b26-109">Questo articolo illustra come toomanage DNS i record per la zona DNS tramite Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="10b26-109">This article shows you how toomanage DNS records for your DNS zone by using Azure PowerShell.</span></span> <span data-ttu-id="10b26-110">I record DNS possono essere gestiti anche tramite hello multipiattaforma [CLI di Azure](dns-operations-recordsets-cli.md) o hello [portale di Azure](dns-operations-recordsets-portal.md).</span><span class="sxs-lookup"><span data-stu-id="10b26-110">DNS records can also be managed by using hello cross-platform [Azure CLI](dns-operations-recordsets-cli.md) or hello [Azure portal](dns-operations-recordsets-portal.md).</span></span>

<span data-ttu-id="10b26-111">esempi di Hello in questo articolo si supponga di avere già [installato Azure PowerShell, connesso e creata una zona DNS](dns-operations-dnszones.md).</span><span class="sxs-lookup"><span data-stu-id="10b26-111">hello examples in this article assume you have already [installed Azure PowerShell, signed in, and created a DNS zone](dns-operations-dnszones.md).</span></span>

## <a name="introduction"></a><span data-ttu-id="10b26-112">Introduzione</span><span class="sxs-lookup"><span data-stu-id="10b26-112">Introduction</span></span>

<span data-ttu-id="10b26-113">Prima di creare record DNS nel sistema DNS di Azure, è innanzitutto necessario toounderstand come DNS di Azure consente di organizzare i record DNS nel set di record DNS.</span><span class="sxs-lookup"><span data-stu-id="10b26-113">Before creating DNS records in Azure DNS, you first need toounderstand how Azure DNS organizes DNS records into DNS record sets.</span></span>

[!INCLUDE [dns-about-records-include](../../includes/dns-about-records-include.md)]

<span data-ttu-id="10b26-114">Per altre informazioni sui record DNS nel servizio DNS di Azure, vedere [Zone e record DNS](dns-zones-records.md).</span><span class="sxs-lookup"><span data-stu-id="10b26-114">For more information about DNS records in Azure DNS, see [DNS zones and records](dns-zones-records.md).</span></span>


## <a name="create-a-new-dns-record"></a><span data-ttu-id="10b26-115">Creare un nuovo record DNS</span><span class="sxs-lookup"><span data-stu-id="10b26-115">Create a new DNS record</span></span>

<span data-ttu-id="10b26-116">Se il nuovo record ha hello stesso nome e tipo come un record esistente, è necessario troppo[aggiungerlo come set di record esistenti toohello](#add-a-record-to-an-existing-record-set).</span><span class="sxs-lookup"><span data-stu-id="10b26-116">If your new record has hello same name and type as an existing record, you need too[add it toohello existing record set](#add-a-record-to-an-existing-record-set).</span></span> <span data-ttu-id="10b26-117">Se il nuovo record ha un diverso tooall nome e tipo di record esistenti, è necessario toocreate un nuovo set di record.</span><span class="sxs-lookup"><span data-stu-id="10b26-117">If your new record has a different name and type tooall existing records, you need toocreate a new record set.</span></span> 

### <a name="create-a-records-in-a-new-record-set"></a><span data-ttu-id="10b26-118">Creare record di tipo "A" in un nuovo set di record</span><span class="sxs-lookup"><span data-stu-id="10b26-118">Create 'A' records in a new record set</span></span>

<span data-ttu-id="10b26-119">Per creare set di record, utilizzare hello `New-AzureRmDnsRecordSet` cmdlet.</span><span class="sxs-lookup"><span data-stu-id="10b26-119">You create record sets by using hello `New-AzureRmDnsRecordSet` cmdlet.</span></span> <span data-ttu-id="10b26-120">Quando si crea un set di record, è necessario zona hello, nome del set di record hello toospecify il tempo di hello toolive (TTL), il tipo di record hello e hello record toobe creati.</span><span class="sxs-lookup"><span data-stu-id="10b26-120">When creating a record set, you need toospecify hello record set name, hello zone, hello time toolive (TTL), hello record type, and hello records toobe created.</span></span>

<span data-ttu-id="10b26-121">i parametri di Hello per l'aggiunta di set di record tooa record dipendono dal tipo di hello del set di record di hello.</span><span class="sxs-lookup"><span data-stu-id="10b26-121">hello parameters for adding records tooa record set vary depending on hello type of hello record set.</span></span> <span data-ttu-id="10b26-122">Ad esempio, quando si utilizza un set di record di tipo 'A', è necessario indirizzo IP di hello toospecify tramite il parametro hello `-IPv4Address`.</span><span class="sxs-lookup"><span data-stu-id="10b26-122">For example, when using a record set of type 'A', you need toospecify hello IP address using hello parameter `-IPv4Address`.</span></span> <span data-ttu-id="10b26-123">Per altri tipi di record vengono usati altri parametri.</span><span class="sxs-lookup"><span data-stu-id="10b26-123">Other parameters are used for other record types.</span></span> <span data-ttu-id="10b26-124">Per altre informazioni, vedere la sezione [Altri esempi di tipi di record](#additional-record-type-examples).</span><span class="sxs-lookup"><span data-stu-id="10b26-124">See [Additional record type examples](#additional-record-type-examples) for details.</span></span>

<span data-ttu-id="10b26-125">Hello seguente viene creato un set con il nome relativo hello 'www' nella zona DNS 'contoso.com' hello di record.</span><span class="sxs-lookup"><span data-stu-id="10b26-125">hello following example creates a record set with hello relative name 'www' in hello DNS Zone 'contoso.com'.</span></span> <span data-ttu-id="10b26-126">nome completo di Hello del set di record hello è 'www.contoso.com'.</span><span class="sxs-lookup"><span data-stu-id="10b26-126">hello fully-qualified name of hello record set is 'www.contoso.com'.</span></span> <span data-ttu-id="10b26-127">tipo di record Hello è 'A' e hello TTL è 3600 secondi.</span><span class="sxs-lookup"><span data-stu-id="10b26-127">hello record type is 'A', and hello TTL is 3600 seconds.</span></span> <span data-ttu-id="10b26-128">set di record Hello contiene un singolo record con indirizzo IP '1.2.3.4'.</span><span class="sxs-lookup"><span data-stu-id="10b26-128">hello record set contains a single record, with IP address '1.2.3.4'.</span></span>

```powershell
New-AzureRmDnsRecordSet -Name "www" -RecordType A -ZoneName "contoso.com" -ResourceGroupName "MyResourceGroup" -Ttl 3600 -DnsRecords (New-AzureRmDnsRecordConfig -IPv4Address "1.2.3.4") 
```

<span data-ttu-id="10b26-129">toocreate un set di record in hello 'apice' di una zona (in questo caso, 'il dominio contoso.com'), utilizza il nome di set di record hello ' @' (escluse le virgolette):</span><span class="sxs-lookup"><span data-stu-id="10b26-129">toocreate a record set at hello 'apex' of a zone (in this case, 'contoso.com'), use hello record set name '@' (excluding quotation marks):</span></span>

```powershell
New-AzureRmDnsRecordSet -Name "@" -RecordType A -ZoneName "contoso.com" -ResourceGroupName "MyResourceGroup" -Ttl 3600 -DnsRecords (New-AzureRmDnsRecordConfig -IPv4Address "1.2.3.4") 
```

<span data-ttu-id="10b26-130">Se è necessario un set di record che contiene più di un record toocreate, creare una matrice locale e aggiungere record hello, quindi passare la matrice hello troppo`New-AzureRmDnsRecordSet` come indicato di seguito:</span><span class="sxs-lookup"><span data-stu-id="10b26-130">If you need toocreate a record set containing more than one record, first create a local array and add hello records, then pass hello array too`New-AzureRmDnsRecordSet` as follows:</span></span>

```powershell
$aRecords = @()
$aRecords += New-AzureRmDnsRecordConfig -IPv4Address "1.2.3.4"
$aRecords += New-AzureRmDnsRecordConfig -IPv4Address "2.3.4.5"
New-AzureRmDnsRecordSet -Name www –ZoneName "contoso.com" -ResourceGroupName MyResourceGroup -Ttl 3600 -RecordType A -DnsRecords $aRecords
```

<span data-ttu-id="10b26-131">[Set di record dei metadati](dns-zones-records.md#tags-and-metadata) può essere utilizzato tooassociate i dati specifici dell'applicazione con ogni set di record, come coppie chiave-valore.</span><span class="sxs-lookup"><span data-stu-id="10b26-131">[Record set metadata](dns-zones-records.md#tags-and-metadata) can be used tooassociate application-specific data with each record set, as key-value pairs.</span></span> <span data-ttu-id="10b26-132">Hello esempio seguente viene illustrato come toocreate un set di record con due voci di metadati, ' dept = finance' e ' ambiente di produzione ='.</span><span class="sxs-lookup"><span data-stu-id="10b26-132">hello following example shows how toocreate a record set with two metadata entries, 'dept=finance' and 'environment=production'.</span></span>

```powershell
New-AzureRmDnsRecordSet -Name "www" -RecordType A -ZoneName "contoso.com" -ResourceGroupName "MyResourceGroup" -Ttl 3600 -DnsRecords (New-AzureRmDnsRecordConfig -IPv4Address "1.2.3.4") -Metadata @{ dept="finance"; environment="production" } 
```

<span data-ttu-id="10b26-133">DNS di Azure supporta anche i set di record "empty", che può agire come un segnaposto tooreserve un nome DNS prima di creare record DNS.</span><span class="sxs-lookup"><span data-stu-id="10b26-133">Azure DNS also supports 'empty' record sets, which can act as a placeholder tooreserve a DNS name before creating DNS records.</span></span> <span data-ttu-id="10b26-134">Set di record vuoti sono visibili nel piano di controllo di hello DNS di Azure, ma vengono visualizzati nel server dei nomi DNS di Azure hello.</span><span class="sxs-lookup"><span data-stu-id="10b26-134">Empty record sets are visible in hello Azure DNS control plane, but do appear on hello Azure DNS name servers.</span></span> <span data-ttu-id="10b26-135">Hello di esempio seguente crea un set di record vuoto:</span><span class="sxs-lookup"><span data-stu-id="10b26-135">hello following example creates an empty record set:</span></span>

```powershell
New-AzureRmDnsRecordSet -Name "www" -RecordType A -ZoneName "contoso.com" -ResourceGroupName "MyResourceGroup" -Ttl 3600 -DnsRecords @()
```

## <a name="create-records-of-other-types"></a><span data-ttu-id="10b26-136">Creare record di altri tipi</span><span class="sxs-lookup"><span data-stu-id="10b26-136">Create records of other types</span></span>

<span data-ttu-id="10b26-137">Dopo aver visto in dettaglio come toocreate 'A' Registra, hello seguenti esempi viene illustrato come record toocreate di altri tipi di record di DNS di Azure è supportati.</span><span class="sxs-lookup"><span data-stu-id="10b26-137">Having seen in detail how toocreate 'A' records, hello following examples show how toocreate records of other record types supported by Azure DNS.</span></span>

<span data-ttu-id="10b26-138">In ogni caso, vengono dimostrati come un record toocreate imposta contenente un singolo record.</span><span class="sxs-lookup"><span data-stu-id="10b26-138">In each case, we show how toocreate a record set containing a single record.</span></span> <span data-ttu-id="10b26-139">Hello esempi precedenti per record 'A' possono essere adattato toocreate set di record di altri tipi contenente più record, con i metadati, o i set di record vuoto toocreate.</span><span class="sxs-lookup"><span data-stu-id="10b26-139">hello earlier examples for 'A' records can be adapted toocreate record sets of other types containing multiple records, with metadata, or toocreate empty record sets.</span></span>

<span data-ttu-id="10b26-140">Non fornita è un esempio toocreate un set di record SOA, poiché viene creati SOA ed eliminato con ogni zona DNS e non è possibile creare o eliminare separatamente.</span><span class="sxs-lookup"><span data-stu-id="10b26-140">We do not give an example toocreate an SOA record set, since SOAs are created and deleted with each DNS zone and cannot be created or deleted separately.</span></span> <span data-ttu-id="10b26-141">Tuttavia, [hello SOA possa essere modificato, come illustrato nell'esempio versione successiva](#to-modify-an-SOA-record).</span><span class="sxs-lookup"><span data-stu-id="10b26-141">However, [hello SOA can be modified, as shown in a later example](#to-modify-an-SOA-record).</span></span>

### <a name="create-an-aaaa-record-set-with-a-single-record"></a><span data-ttu-id="10b26-142">Creare un set di record AAAA con un singolo record</span><span class="sxs-lookup"><span data-stu-id="10b26-142">Create an AAAA record set with a single record</span></span>

```powershell
New-AzureRmDnsRecordSet -Name "test-aaaa" -RecordType AAAA -ZoneName "contoso.com" -ResourceGroupName "MyResourceGroup" -Ttl 3600 -DnsRecords (New-AzureRmDnsRecordConfig -Ipv6Address "2607:f8b0:4009:1803::1005") 
```

### <a name="create-a-cname-record-set-with-a-single-record"></a><span data-ttu-id="10b26-143">Creare un set di record CNAME con un singolo record</span><span class="sxs-lookup"><span data-stu-id="10b26-143">Create a CNAME record set with a single record</span></span>

> [!NOTE]
> <span data-ttu-id="10b26-144">standard DNS Hello non consentono i record CNAME al vertice hello di una zona (`-Name '@'`), né che consentono i set di record che contiene più di un record.</span><span class="sxs-lookup"><span data-stu-id="10b26-144">hello DNS standards do not permit CNAME records at hello apex of a zone (`-Name '@'`), nor do they permit record sets containing more than one record.</span></span>
> 
> <span data-ttu-id="10b26-145">Per altre informazioni, vedere[Record CNAME](dns-zones-records.md#cname-records).</span><span class="sxs-lookup"><span data-stu-id="10b26-145">For more information, see [CNAME records](dns-zones-records.md#cname-records).</span></span>


```powershell
New-AzureRmDnsRecordSet -Name "test-cname" -RecordType CNAME -ZoneName "contoso.com" -ResourceGroupName "MyResourceGroup" -Ttl 3600 -DnsRecords (New-AzureRmDnsRecordConfig -Cname "www.contoso.com") 
```

### <a name="create-an-mx-record-set-with-a-single-record"></a><span data-ttu-id="10b26-146">Creare un set di record MX con un singolo record</span><span class="sxs-lookup"><span data-stu-id="10b26-146">Create an MX record set with a single record</span></span>

<span data-ttu-id="10b26-147">In questo esempio, si usa nome set di record hello ' @' record toocreate un MX al vertice zona hello (in questo caso, 'il dominio contoso.com').</span><span class="sxs-lookup"><span data-stu-id="10b26-147">In this example, we use hello record set name '@' toocreate an MX record at hello zone apex (in this case, 'contoso.com').</span></span>


```powershell
New-AzureRmDnsRecordSet -Name "@" -RecordType MX -ZoneName "contoso.com" -ResourceGroupName "MyResourceGroup" -Ttl 3600 -DnsRecords (New-AzureRmDnsRecordConfig -Exchange "mail.contoso.com" -Preference 5) 
```

### <a name="create-an-ns-record-set-with-a-single-record"></a><span data-ttu-id="10b26-148">Creare un set di record NS con un singolo record</span><span class="sxs-lookup"><span data-stu-id="10b26-148">Create an NS record set with a single record</span></span>

```powershell
New-AzureRmDnsRecordSet -Name "test-ns" -RecordType NS -ZoneName "contoso.com" -ResourceGroupName "MyResourceGroup" -Ttl 3600 -DnsRecords (New-AzureRmDnsRecordConfig -Nsdname "ns1.contoso.com") 
```

### <a name="create-a-ptr-record-set-with-a-single-record"></a><span data-ttu-id="10b26-149">Creare un set di record PTR con un singolo record</span><span class="sxs-lookup"><span data-stu-id="10b26-149">Create a PTR record set with a single record</span></span>

<span data-ttu-id="10b26-150">In questo caso, "my-arpa-zone.com' rappresenta hello zona di ricerca inversa ARPA che rappresenta l'intervallo di IP.</span><span class="sxs-lookup"><span data-stu-id="10b26-150">In this case, 'my-arpa-zone.com' represents hello ARPA reverse lookup zone representing your IP range.</span></span> <span data-ttu-id="10b26-151">Ogni record PTR impostato in questa zona corrisponde tooan di indirizzo IP in questo intervallo IP.</span><span class="sxs-lookup"><span data-stu-id="10b26-151">Each PTR record set in this zone corresponds tooan IP address within this IP range.</span></span> <span data-ttu-id="10b26-152">nome del record '10' Hello è ultimo ottetto di hello dell'indirizzo IP hello in questo intervallo IP rappresentato da questo record.</span><span class="sxs-lookup"><span data-stu-id="10b26-152">hello record name '10' is hello last octet of hello IP address within this IP range represented by this record.</span></span>

```powershell
New-AzureRmDnsRecordSet -Name 10 -RecordType PTR -ZoneName "my-arpa-zone.com" -ResourceGroupName "MyResourceGroup" -Ttl 3600 -DnsRecords (New-AzureRmDnsRecordConfig -Ptrdname "myservice.contoso.com") 
```

### <a name="create-an-srv-record-set-with-a-single-record"></a><span data-ttu-id="10b26-153">Creare un set di record SRV con un singolo record</span><span class="sxs-lookup"><span data-stu-id="10b26-153">Create an SRV record set with a single record</span></span>

<span data-ttu-id="10b26-154">Quando si crea un [set di record SRV](dns-zones-records.md#srv-records), specificare hello  *\_servizio* e  *\_protocollo* in hello Nome set di record.</span><span class="sxs-lookup"><span data-stu-id="10b26-154">When creating an [SRV record set](dns-zones-records.md#srv-records), specify hello *\_service* and *\_protocol* in hello record set name.</span></span> <span data-ttu-id="10b26-155">Non è alcuna necessità tooinclude ' @' in hello set di record nome durante la creazione di un record SRV set al vertice zona hello.</span><span class="sxs-lookup"><span data-stu-id="10b26-155">There is no need tooinclude '@' in hello record set name when creating an SRV record set at hello zone apex.</span></span>

```powershell
New-AzureRmDnsRecordSet -Name "_sip._tls" -RecordType SRV -ZoneName "contoso.com" -ResourceGroupName "MyResourceGroup" -Ttl 3600 -DnsRecords (New-AzureRmDnsRecordConfig -Priority 0 -Weight 5 -Port 8080 -Target "sip.contoso.com") 
```


### <a name="create-a-txt-record-set-with-a-single-record"></a><span data-ttu-id="10b26-156">Creare un set di record TXT con un singolo record</span><span class="sxs-lookup"><span data-stu-id="10b26-156">Create a TXT record set with a single record</span></span>

<span data-ttu-id="10b26-157">Hello esempio seguente viene illustrato come toocreate un TXT record.</span><span class="sxs-lookup"><span data-stu-id="10b26-157">hello following example shows how toocreate a TXT record.</span></span> <span data-ttu-id="10b26-158">Per ulteriori informazioni sulla lunghezza massima della stringa hello è supportata nei record TXT, vedere [record TXT](dns-zones-records.md#txt-records).</span><span class="sxs-lookup"><span data-stu-id="10b26-158">For more information about hello maximum string length supported in TXT records, see [TXT records](dns-zones-records.md#txt-records).</span></span>

```powershell
New-AzureRmDnsRecordSet -Name "test-txt" -RecordType TXT -ZoneName "contoso.com" -ResourceGroupName "MyResourceGroup" -Ttl 3600 -DnsRecords (New-AzureRmDnsRecordConfig -Value "This is a TXT record") 
```


## <a name="get-a-record-set"></a><span data-ttu-id="10b26-159">Ottenere un set di record</span><span class="sxs-lookup"><span data-stu-id="10b26-159">Get a record set</span></span>

<span data-ttu-id="10b26-160">Utilizzare un set di record esistente, tooretrieve `Get-AzureRmDnsRecordSet`.</span><span class="sxs-lookup"><span data-stu-id="10b26-160">tooretrieve an existing record set, use `Get-AzureRmDnsRecordSet`.</span></span> <span data-ttu-id="10b26-161">Questo cmdlet restituisce un oggetto locale che rappresenta hello set di record in DNS di Azure.</span><span class="sxs-lookup"><span data-stu-id="10b26-161">This cmdlet returns a local object that represents hello record set in Azure DNS.</span></span>

<span data-ttu-id="10b26-162">Come con `New-AzureRmDnsRecordSet`, il nome di set di record hello specificato deve essere un *relativo* nome, pertanto è necessario escludere nome zona hello.</span><span class="sxs-lookup"><span data-stu-id="10b26-162">As with `New-AzureRmDnsRecordSet`, hello record set name given must be a *relative* name, meaning it must exclude hello zone name.</span></span> <span data-ttu-id="10b26-163">È inoltre necessario toospecify hello tipo record e contenente i set di record hello zona di hello.</span><span class="sxs-lookup"><span data-stu-id="10b26-163">You also need toospecify hello record type, and hello zone containing hello record set.</span></span>

<span data-ttu-id="10b26-164">Hello esempio seguente viene illustrato come tooretrieve un set di record.</span><span class="sxs-lookup"><span data-stu-id="10b26-164">hello following example shows how tooretrieve a record set.</span></span> <span data-ttu-id="10b26-165">In questo esempio, la zona hello viene specificata con hello `-ZoneName` e `-ResourceGroupName` parametri.</span><span class="sxs-lookup"><span data-stu-id="10b26-165">In this example, hello zone is specified using hello `-ZoneName` and `-ResourceGroupName` parameters.</span></span>

```powershell
$rs = Get-AzureRmDnsRecordSet -Name "www" -RecordType A -ZoneName "contoso.com" -ResourceGroupName "MyResourceGroup"
```

<span data-ttu-id="10b26-166">In alternativa, è inoltre possibile specificare zona hello mediante un oggetto fuso passato usando hello `-Zone` parametro.</span><span class="sxs-lookup"><span data-stu-id="10b26-166">Alternatively, you can also specify hello zone using a zone object, passed using hello `-Zone` parameter.</span></span>

```powershell
$zone = Get-AzureRmDnsZone -Name "contoso.com" -ResourceGroupName "MyResourceGroup"
$rs = Get-AzureRmDnsRecordSet -Name "www" -RecordType A -Zone $zone
```

## <a name="list-record-sets"></a><span data-ttu-id="10b26-167">Elencare i set di record</span><span class="sxs-lookup"><span data-stu-id="10b26-167">List record sets</span></span>

<span data-ttu-id="10b26-168">È inoltre possibile utilizzare `Get-AzureRmDnsZone` toolist i set di record in una zona, omettendo hello `-Name` e/o `-RecordType` parametri.</span><span class="sxs-lookup"><span data-stu-id="10b26-168">You can also use `Get-AzureRmDnsZone` toolist record sets in a zone, by omitting hello `-Name` and/or `-RecordType` parameters.</span></span>

<span data-ttu-id="10b26-169">Hello esempio seguente restituisce i set di tutti i record nella zona hello:</span><span class="sxs-lookup"><span data-stu-id="10b26-169">hello following example returns all record sets in hello zone:</span></span>

```powershell
$recordsets = Get-AzureRmDnsRecordSet -ZoneName "contoso.com" -ResourceGroupName "MyResourceGroup"
```

<span data-ttu-id="10b26-170">Hello esempio seguente viene illustrato come tutti i set di un determinato tipo di record possono essere recuperati specificando un tipo di record hello mentre il nome del set di record hello l'omissione:</span><span class="sxs-lookup"><span data-stu-id="10b26-170">hello following example shows how all record sets of a given type can be retrieved by specifying hello record type while omitting hello record set name:</span></span>

```powershell
$recordsets = Get-AzureRmDnsRecordSet -RecordType A -ZoneName "contoso.com" -ResourceGroupName "MyResourceGroup"
```

<span data-ttu-id="10b26-171">Imposta tutti i record con un nome specificato, tooretrieve tra tipi di record, è necessario tooretrieve tutti i set di record e quindi filtro hello risultati:</span><span class="sxs-lookup"><span data-stu-id="10b26-171">tooretrieve all record sets with a given name, across record types, you need tooretrieve all record sets and then filter hello results:</span></span>

```powershell
$recordsets = Get-AzureRmDnsRecordSet -ZoneName "contoso.com" -ResourceGroupName "MyResourceGroup" | where {$_.Name.Equals("www")}
```

<span data-ttu-id="10b26-172">In hello tutti gli esempi sopra riportati, la zona hello può essere specificato tramite l'utilizzo di hello `-ZoneName` e `-ResourceGroupName`parametri (come illustrato), oppure specificando un oggetto fuso orario:</span><span class="sxs-lookup"><span data-stu-id="10b26-172">In all hello above examples, hello zone can be specified either by using hello `-ZoneName` and `-ResourceGroupName`parameters (as shown), or by specifying a zone object:</span></span>

```powershell
$zone = Get-AzureRmDnsZone -Name "contoso.com" -ResourceGroupName "MyResourceGroup"
$recordsets = Get-AzureRmDnsRecordSet -Zone $zone
```

## <a name="add-a-record-tooan-existing-record-set"></a><span data-ttu-id="10b26-173">Aggiungere un record tooan esistente del set di record</span><span class="sxs-lookup"><span data-stu-id="10b26-173">Add a record tooan existing record set</span></span>

<span data-ttu-id="10b26-174">un record esistente tooan record tooadd impostato, seguire hello tre passaggi:</span><span class="sxs-lookup"><span data-stu-id="10b26-174">tooadd a record tooan existing record set, follow hello following three steps:</span></span>

1. <span data-ttu-id="10b26-175">Ottiene il set di record esistenti hello</span><span class="sxs-lookup"><span data-stu-id="10b26-175">Get hello existing record set</span></span>

    ```powershell
    $rs = Get-AzureRmDnsRecordSet -Name www –ZoneName "contoso.com" -ResourceGroupName "MyResourceGroup" -RecordType A
    ```

2. <span data-ttu-id="10b26-176">Aggiungere hello nuovi record toohello locale set di record.</span><span class="sxs-lookup"><span data-stu-id="10b26-176">Add hello new record toohello local record set.</span></span> <span data-ttu-id="10b26-177">Si tratta di un'operazione offline.</span><span class="sxs-lookup"><span data-stu-id="10b26-177">This is an off-line operation.</span></span>

    ```powershell
    Add-AzureRmDnsRecordConfig -RecordSet $rs -Ipv4Address "5.6.7.8"
    ```

3. <span data-ttu-id="10b26-178">Eseguire il commit hello modifica indietro toohello servizio DNS di Azure.</span><span class="sxs-lookup"><span data-stu-id="10b26-178">Commit hello change back toohello Azure DNS service.</span></span> 

    ```powershell
    Set-AzureRmDnsRecordSet -RecordSet $rs
    ```

<span data-ttu-id="10b26-179">Utilizzando `Set-AzureRmDnsRecordSet` *sostituisce* hello esistente set di record in DNS di Azure (e tutti i record contiene) con il set di record hello specificato.</span><span class="sxs-lookup"><span data-stu-id="10b26-179">Using `Set-AzureRmDnsRecordSet` *replaces* hello existing record set in Azure DNS (and all records it contains) with hello record set specified.</span></span> <span data-ttu-id="10b26-180">[Controllo eTag](dns-zones-records.md#etags) vengono utilizzate le modifiche simultanee tooensure non vengono sovrascritti.</span><span class="sxs-lookup"><span data-stu-id="10b26-180">[Etag checks](dns-zones-records.md#etags) are used tooensure concurrent changes are not overwritten.</span></span> <span data-ttu-id="10b26-181">È possibile utilizzare hello facoltativo `-Overwrite` passare toosuppress questi controlli.</span><span class="sxs-lookup"><span data-stu-id="10b26-181">You can use hello optional `-Overwrite` switch toosuppress these checks.</span></span>

<span data-ttu-id="10b26-182">Questa sequenza di operazioni può anche essere *reindirizzato*, vale a dire si passa l'oggetto set di record hello utilizzando pipe hello, anziché passarlo come parametro:</span><span class="sxs-lookup"><span data-stu-id="10b26-182">This sequence of operations can also be *piped*, meaning you pass hello record set object by using hello pipe rather than passing it as a parameter:</span></span>

```powershell
Get-AzureRmDnsRecordSet -Name "www" –ZoneName "contoso.com" -ResourceGroupName "MyResourceGroup" -RecordType A | Add-AzureRmDnsRecordConfig -Ipv4Address "5.6.7.8" | Set-AzureRmDnsRecordSet
```

<span data-ttu-id="10b26-183">esempi di Hello sopra riportati illustrano come impostare di tooadd un record esistente 'A' tooan record di tipo 'A'.</span><span class="sxs-lookup"><span data-stu-id="10b26-183">hello examples above show how tooadd an 'A' record tooan existing record set of type 'A'.</span></span> <span data-ttu-id="10b26-184">Una sequenza di operazioni simile viene utilizzato tooadd i set di record toorecord di altri tipi, sostituendo hello `-Ipv4Address` parametro di `Add-AzureRmDnsRecordConfig` con altri tipi di record tooeach specifico di parametri.</span><span class="sxs-lookup"><span data-stu-id="10b26-184">A similar sequence of operations is used tooadd records toorecord sets of other types, substituting hello `-Ipv4Address` parameter of `Add-AzureRmDnsRecordConfig` with other parameters specific tooeach record type.</span></span> <span data-ttu-id="10b26-185">Hello parametri per ogni tipo di record sono hello uguale a quello di hello `New-AzureRmDnsRecordConfig` cmdlet come mostrato [esempi aggiuntivi di tipo record](#additional-record-type-examples) sopra.</span><span class="sxs-lookup"><span data-stu-id="10b26-185">hello parameters for each record type are hello same as for hello `New-AzureRmDnsRecordConfig` cmdlet, as shown in [Additional record type examples](#additional-record-type-examples) above.</span></span>

<span data-ttu-id="10b26-186">I set di record di tipo "CNAME" o "SOA" non possono contenere più di un record.</span><span class="sxs-lookup"><span data-stu-id="10b26-186">Record sets of type 'CNAME' or 'SOA' cannot contain more than one record.</span></span> <span data-ttu-id="10b26-187">Questo vincolo viene visualizzato dagli standard DNS hello.</span><span class="sxs-lookup"><span data-stu-id="10b26-187">This constraint arises from hello DNS standards.</span></span> <span data-ttu-id="10b26-188">non è una limitazione del servizio DNS di Azure.</span><span class="sxs-lookup"><span data-stu-id="10b26-188">It is not a limitation of Azure DNS.</span></span>

## <a name="remove-a-record-from-an-existing-record-set"></a><span data-ttu-id="10b26-189">Rimuovere un record da un set di record esistente</span><span class="sxs-lookup"><span data-stu-id="10b26-189">Remove a record from an existing record set</span></span>

<span data-ttu-id="10b26-190">processo tooremove un record da un set di record Hello è un record tooan esistente simile tooadd di processo toohello set di record:</span><span class="sxs-lookup"><span data-stu-id="10b26-190">hello process tooremove a record from a record set is similar toohello process tooadd a record tooan existing record set:</span></span>

1. <span data-ttu-id="10b26-191">Ottiene il set di record esistenti hello</span><span class="sxs-lookup"><span data-stu-id="10b26-191">Get hello existing record set</span></span>

    ```powershell
    $rs = Get-AzureRmDnsRecordSet -Name www –ZoneName "contoso.com" -ResourceGroupName "MyResourceGroup" -RecordType A
    ```

2. <span data-ttu-id="10b26-192">Rimuovere i record di hello dall'oggetto set di record locale hello.</span><span class="sxs-lookup"><span data-stu-id="10b26-192">Remove hello record from hello local record set object.</span></span> <span data-ttu-id="10b26-193">Si tratta di un'operazione offline.</span><span class="sxs-lookup"><span data-stu-id="10b26-193">This is an off-line operation.</span></span> <span data-ttu-id="10b26-194">record di Hello corso di rimozione deve essere una corrispondenza esatta con un record esistente in tutti i parametri.</span><span class="sxs-lookup"><span data-stu-id="10b26-194">hello record that's being removed must be an exact match with an existing record across all parameters.</span></span>

    ```powershell
    Remove-AzureRmDnsRecordConfig -RecordSet $rs -Ipv4Address "5.6.7.8"
    ```

3. <span data-ttu-id="10b26-195">Eseguire il commit hello modifica indietro toohello servizio DNS di Azure.</span><span class="sxs-lookup"><span data-stu-id="10b26-195">Commit hello change back toohello Azure DNS service.</span></span> <span data-ttu-id="10b26-196">Hello utilizzo facoltativo `-Overwrite` passare toosuppress [Etag controlla](dns-zones-records.md#etags) per modifiche simultanee.</span><span class="sxs-lookup"><span data-stu-id="10b26-196">Use hello optional `-Overwrite` switch toosuppress [Etag checks](dns-zones-records.md#etags) for concurrent changes.</span></span>

    ```powershell
    Set-AzureRmDnsRecordSet -RecordSet $Rs
    ```

<span data-ttu-id="10b26-197">Utilizzando hello sopra sequenza tooremove hello ultimo record da un set di record non comporta l'eliminazione del set di record hello, ma lascia un set di record vuoto.</span><span class="sxs-lookup"><span data-stu-id="10b26-197">Using hello above sequence tooremove hello last record from a record set does not delete hello record set, rather it leaves an empty record set.</span></span> <span data-ttu-id="10b26-198">vedere un set di record, tooremove [eliminare un set di record](#delete-a-record-set).</span><span class="sxs-lookup"><span data-stu-id="10b26-198">tooremove a record set entirely, see [Delete a record set](#delete-a-record-set).</span></span>

<span data-ttu-id="10b26-199">Allo stesso modo tooadding record tooa set di record, sequenza hello di un set di record può anche essere reindirizzato tooremove di operazioni:</span><span class="sxs-lookup"><span data-stu-id="10b26-199">Similarly tooadding records tooa record set, hello sequence of operations tooremove a record set can also be piped:</span></span>

```powershell
Get-AzureRmDnsRecordSet -Name www –ZoneName "contoso.com" -ResourceGroupName "MyResourceGroup" -RecordType A | Remove-AzureRmDnsRecordConfig -Ipv4Address "5.6.7.8" | Set-AzureRmDnsRecordSet
```

<span data-ttu-id="10b26-200">Sono supportati i tipi di record diversi passando i parametri specifici del tipo appropriato di hello troppo`Remove-AzureRmDnsRecordSet`.</span><span class="sxs-lookup"><span data-stu-id="10b26-200">Different record types are supported by passing hello appropriate type-specific parameters too`Remove-AzureRmDnsRecordSet`.</span></span> <span data-ttu-id="10b26-201">Hello parametri per ogni tipo di record sono hello uguale a quello di hello `New-AzureRmDnsRecordConfig` cmdlet come mostrato [esempi aggiuntivi di tipo record](#additional-record-type-examples) sopra.</span><span class="sxs-lookup"><span data-stu-id="10b26-201">hello parameters for each record type are hello same as for hello `New-AzureRmDnsRecordConfig` cmdlet, as shown in [Additional record type examples](#additional-record-type-examples) above.</span></span>


## <a name="modify-an-existing-record-set"></a><span data-ttu-id="10b26-202">Modificare un set di record esistente</span><span class="sxs-lookup"><span data-stu-id="10b26-202">Modify an existing record set</span></span>

<span data-ttu-id="10b26-203">passaggi per la modifica di un set di record esistenti in Hello sono simili toohello effettuate durante l'aggiunta o rimozione di record da un set di record:</span><span class="sxs-lookup"><span data-stu-id="10b26-203">hello steps for modifying an existing record set are similar toohello steps you take when adding or removing records from a record set:</span></span>

1. <span data-ttu-id="10b26-204">Recuperare il record esistente hello impostato utilizzando `Get-AzureRmDnsRecordSet`.</span><span class="sxs-lookup"><span data-stu-id="10b26-204">Retrieve hello existing record set by using `Get-AzureRmDnsRecordSet`.</span></span>
2. <span data-ttu-id="10b26-205">Modificare l'oggetto set di record locale hello:</span><span class="sxs-lookup"><span data-stu-id="10b26-205">Modify hello local record set object by:</span></span>
    * <span data-ttu-id="10b26-206">Aggiungere o rimuovere record.</span><span class="sxs-lookup"><span data-stu-id="10b26-206">Adding or removing records</span></span>
    * <span data-ttu-id="10b26-207">La modifica dei parametri di hello dei record esistenti</span><span class="sxs-lookup"><span data-stu-id="10b26-207">Changing hello parameters of existing records</span></span>
    * <span data-ttu-id="10b26-208">Modifica di record hello del set di metadati e toolive TTL (time)</span><span class="sxs-lookup"><span data-stu-id="10b26-208">Changing hello record set metadata and time toolive (TTL)</span></span>
3. <span data-ttu-id="10b26-209">Eseguire il commit delle modifiche tramite hello `Set-AzureRmDnsRecordSet` cmdlet.</span><span class="sxs-lookup"><span data-stu-id="10b26-209">Commit your changes by using hello `Set-AzureRmDnsRecordSet` cmdlet.</span></span> <span data-ttu-id="10b26-210">Questo *sostituisce* hello esistente set di record in DNS di Azure con i set di record hello specificato.</span><span class="sxs-lookup"><span data-stu-id="10b26-210">This *replaces* hello existing record set in Azure DNS with hello record set specified.</span></span>

<span data-ttu-id="10b26-211">Quando si utilizza `Set-AzureRmDnsRecordSet`, [Etag controlla](dns-zones-records.md#etags) vengono utilizzate le modifiche simultanee tooensure non vengono sovrascritti.</span><span class="sxs-lookup"><span data-stu-id="10b26-211">When using `Set-AzureRmDnsRecordSet`, [Etag checks](dns-zones-records.md#etags) are used tooensure concurrent changes are not overwritten.</span></span> <span data-ttu-id="10b26-212">È possibile utilizzare hello facoltativo `-Overwrite` passare toosuppress questi controlli.</span><span class="sxs-lookup"><span data-stu-id="10b26-212">You can use hello optional `-Overwrite` switch toosuppress these checks.</span></span>

### <a name="tooupdate-a-record-in-an-existing-record-set"></a><span data-ttu-id="10b26-213">Imposta tooupdate un record in un record esistente</span><span class="sxs-lookup"><span data-stu-id="10b26-213">tooupdate a record in an existing record set</span></span>

<span data-ttu-id="10b26-214">In questo esempio, si modifica l'indirizzo IP hello del 'A' record esistente:</span><span class="sxs-lookup"><span data-stu-id="10b26-214">In this example, we change hello IP address of an existing 'A' record:</span></span>

```powershell
$rs = Get-AzureRmDnsRecordSet -name "www" -RecordType A -ZoneName "contoso.com" -ResourceGroupName "MyResourceGroup"
$rs.Records[0].Ipv4Address = "9.8.7.6"
Set-AzureRmDnsRecordSet -RecordSet $rs
```

### <a name="toomodify-an-soa-record"></a><span data-ttu-id="10b26-215">un record SOA toomodify</span><span class="sxs-lookup"><span data-stu-id="10b26-215">toomodify an SOA record</span></span>

<span data-ttu-id="10b26-216">È possibile aggiungere o rimuovere i record da hello automaticamente creato un record SOA impostato al vertice zona hello (`-Name "@"`, tra virgolette).</span><span class="sxs-lookup"><span data-stu-id="10b26-216">You cannot add or remove records from hello automatically created SOA record set at hello zone apex (`-Name "@"`, including quote marks).</span></span> <span data-ttu-id="10b26-217">Tuttavia, è possibile modificare i parametri di hello all'interno di hello record SOA (ad eccezione di "Host") e impostare il valore TTL record hello.</span><span class="sxs-lookup"><span data-stu-id="10b26-217">However, you can modify any of hello parameters within hello SOA record (except "Host") and hello record set TTL.</span></span>

<span data-ttu-id="10b26-218">Hello seguente esempio viene illustrato come hello toochange *posta elettronica* proprietà del record SOA hello:</span><span class="sxs-lookup"><span data-stu-id="10b26-218">hello following example shows how toochange hello *Email* property of hello SOA record:</span></span>

```powershell
$rs = Get-AzureRmDnsRecordSet -Name "@" -RecordType SOA -ZoneName "contoso.com" -ResourceGroupName "MyResourceGroup"
$rs.Records[0].Email = "admin.contoso.com"
Set-AzureRmDnsRecordSet -RecordSet $rs
```

### <a name="toomodify-ns-records-at-hello-zone-apex"></a><span data-ttu-id="10b26-219">record NS toomodify al vertice zona hello</span><span class="sxs-lookup"><span data-stu-id="10b26-219">toomodify NS records at hello zone apex</span></span>

<span data-ttu-id="10b26-220">record NS Hello impostato al vertice zona hello viene creato automaticamente con ogni zona DNS.</span><span class="sxs-lookup"><span data-stu-id="10b26-220">hello NS record set at hello zone apex is automatically created with each DNS zone.</span></span> <span data-ttu-id="10b26-221">Contiene i nomi hello della zona di hello DNS di Azure nome server toohello assegnato.</span><span class="sxs-lookup"><span data-stu-id="10b26-221">It contains hello names of hello Azure DNS name servers assigned toohello zone.</span></span>

<span data-ttu-id="10b26-222">È possibile aggiungere nomi aggiuntivi server toothis NS set di record, toosupport CO-ospitano i domini con più di un provider DNS.</span><span class="sxs-lookup"><span data-stu-id="10b26-222">You can add additional name servers toothis NS record set, toosupport co-hosting domains with more than one DNS provider.</span></span> <span data-ttu-id="10b26-223">È inoltre possibile modificare hello durata (TTL) e i metadati per questo set di record.</span><span class="sxs-lookup"><span data-stu-id="10b26-223">You can also modify hello TTL and metadata for this record set.</span></span> <span data-ttu-id="10b26-224">Tuttavia, è Impossibile rimuovere o modificare server dei nomi DNS di Azure prepopolato hello.</span><span class="sxs-lookup"><span data-stu-id="10b26-224">However, you cannot remove or modify hello pre-populated Azure DNS name servers.</span></span>

<span data-ttu-id="10b26-225">Si noti che questo si applica solo toohello NS set di record al vertice zona hello.</span><span class="sxs-lookup"><span data-stu-id="10b26-225">Note that this applies only toohello NS record set at hello zone apex.</span></span> <span data-ttu-id="10b26-226">Altri set di record NS nella zona (come le aree figlio toodelegate usato) possono essere modificati senza vincoli.</span><span class="sxs-lookup"><span data-stu-id="10b26-226">Other NS record sets in your zone (as used toodelegate child zones) can be modified without constraint.</span></span>

<span data-ttu-id="10b26-227">Hello di esempio seguente viene illustrato come tooadd un record NS di nomi aggiuntivi server toohello imposta al vertice zona hello:</span><span class="sxs-lookup"><span data-stu-id="10b26-227">hello following example shows how tooadd an additional name server toohello NS record set at hello zone apex:</span></span>

```powershell
$rs = Get-AzureRmDnsRecordSet -Name "@" -RecordType NS -ZoneName "contoso.com" -ResourceGroupName "MyResourceGroup"
Add-AzureRmDnsRecordConfig -RecordSet $rs -Nsdname ns1.myotherdnsprovider.com
Set-AzureRmDnsRecordSet -RecordSet $rs
```

### <a name="toomodify-record-set-metadata"></a><span data-ttu-id="10b26-228">record toomodify impostare i metadati</span><span class="sxs-lookup"><span data-stu-id="10b26-228">toomodify record set metadata</span></span>

<span data-ttu-id="10b26-229">[Set di record dei metadati](dns-zones-records.md#tags-and-metadata) può essere utilizzato tooassociate i dati specifici dell'applicazione con ogni set di record, come coppie chiave-valore.</span><span class="sxs-lookup"><span data-stu-id="10b26-229">[Record set metadata](dns-zones-records.md#tags-and-metadata) can be used tooassociate application-specific data with each record set, as key-value pairs.</span></span>

<span data-ttu-id="10b26-230">Hello esempio seguente viene illustrato come impostare di toomodify hello metadati di un record esistente:</span><span class="sxs-lookup"><span data-stu-id="10b26-230">hello following example shows how toomodify hello metadata of an existing record set:</span></span>

```powershell
# Get hello record set
$rs = Get-AzureRmDnsRecordSet -Name www -RecordType A -ZoneName "contoso.com" -ResourceGroupName "MyResourceGroup"

# Add 'dept=finance' name-value pair
$rs.Metadata.Add('dept', 'finance') 

# Remove metadata item named 'environment'
$rs.Metadata.Remove('environment')  

# Commit changes
Set-AzureRmDnsRecordSet -RecordSet $rs
```


## <a name="delete-a-record-set"></a><span data-ttu-id="10b26-231">Eliminare un set di record</span><span class="sxs-lookup"><span data-stu-id="10b26-231">Delete a record set</span></span>

<span data-ttu-id="10b26-232">Set di record possono essere eliminate utilizzando hello `Remove-AzureRmDnsRecordSet` cmdlet.</span><span class="sxs-lookup"><span data-stu-id="10b26-232">Record sets can be deleted by using hello `Remove-AzureRmDnsRecordSet` cmdlet.</span></span> <span data-ttu-id="10b26-233">L'eliminazione di un set di record elimina inoltre tutti i record all'interno del set di record hello.</span><span class="sxs-lookup"><span data-stu-id="10b26-233">Deleting a record set also deletes all records within hello record set.</span></span>

> [!NOTE]
> <span data-ttu-id="10b26-234">Non è possibile eliminare hello SOA e NS set di record al vertice zona hello (`-Name '@'`).</span><span class="sxs-lookup"><span data-stu-id="10b26-234">You cannot delete hello SOA and NS record sets at hello zone apex (`-Name '@'`).</span></span>  <span data-ttu-id="10b26-235">DNS di Azure creata questi automaticamente quando è stato creato, zona hello e li elimina automaticamente quando viene eliminata hello.</span><span class="sxs-lookup"><span data-stu-id="10b26-235">Azure DNS created these automatically when hello zone was created, and deletes them automatically when hello zone is deleted.</span></span>

<span data-ttu-id="10b26-236">Hello esempio seguente viene illustrato come toodelete un set di record.</span><span class="sxs-lookup"><span data-stu-id="10b26-236">hello following example shows how toodelete a record set.</span></span> <span data-ttu-id="10b26-237">In questo esempio, il nome di set di record hello, tipo di set di record, nome della zona e gruppo di risorse sono ogni specificati in modo esplicito.</span><span class="sxs-lookup"><span data-stu-id="10b26-237">In this example, hello record set name, record set type, zone name, and resource group are each specified explicitly.</span></span>

```powershell
Remove-AzureRmDnsRecordSet -Name "www" -RecordType A -ZoneName "contoso.com" -ResourceGroupName "MyResourceGroup"
```

<span data-ttu-id="10b26-238">In alternativa, è possibile specificare un set di record hello dal nome e il tipo e hello zona specificata utilizzando un oggetto:</span><span class="sxs-lookup"><span data-stu-id="10b26-238">Alternatively, hello record set can be specified by name and type, and hello zone specified using an object:</span></span>

```powershell
$zone = Get-AzureRmDnsZone -Name "contoso.com" -ResourceGroupName "MyResourceGroup"
Remove-AzureRmDnsRecordSet -Name "www" -RecordType A -Zone $zone
```

<span data-ttu-id="10b26-239">Come una terza opzione, è possibile specificare record hello impostare autonomamente l'utilizzo di un oggetto set di record:</span><span class="sxs-lookup"><span data-stu-id="10b26-239">As a third option, hello record set itself can be specified using a record set object:</span></span>

```powershell
$rs = Get-AzureRmDnsRecordSet -Name www -RecordType A -ZoneName "contoso.com" -ResourceGroupName "MyResourceGroup"
Remove-AzureRmDnsRecordSet -RecordSet $rs
```

<span data-ttu-id="10b26-240">Quando si specifica il set di record hello toobe eliminato utilizzando un oggetto set di record, [Etag controlla](dns-zones-records.md#etags) vengono utilizzate le modifiche simultanee tooensure non vengono eliminate.</span><span class="sxs-lookup"><span data-stu-id="10b26-240">When you specify hello record set toobe deleted by using a record set object, [Etag checks](dns-zones-records.md#etags) are used tooensure concurrent changes are not deleted.</span></span> <span data-ttu-id="10b26-241">È possibile utilizzare hello facoltativo `-Overwrite` passare toosuppress questi controlli.</span><span class="sxs-lookup"><span data-stu-id="10b26-241">You can use hello optional `-Overwrite` switch toosuppress these checks.</span></span>

<span data-ttu-id="10b26-242">oggetto set di record Hello può anche essere reindirizzato anziché passato come parametro:</span><span class="sxs-lookup"><span data-stu-id="10b26-242">hello record set object can also be piped instead of being passed as a parameter:</span></span>

```powershell
Get-AzureRmDnsRecordSet -Name www -RecordType A -ZoneName "contoso.com" -ResourceGroupName "MyResourceGroup" | Remove-AzureRmDnsRecordSet
```

## <a name="confirmation-prompts"></a><span data-ttu-id="10b26-243">Richieste di conferma</span><span class="sxs-lookup"><span data-stu-id="10b26-243">Confirmation prompts</span></span>

<span data-ttu-id="10b26-244">Hello `New-AzureRmDnsRecordSet`, `Set-AzureRmDnsRecordSet`, e `Remove-AzureRmDnsRecordSet` tutti i cmdlet supportano richieste di conferma.</span><span class="sxs-lookup"><span data-stu-id="10b26-244">hello `New-AzureRmDnsRecordSet`, `Set-AzureRmDnsRecordSet`, and `Remove-AzureRmDnsRecordSet` cmdlets all support confirmation prompts.</span></span>

<span data-ttu-id="10b26-245">Ogni cmdlet chiede conferma se hello `$ConfirmPreference` variabile di preferenza PowerShell ha un valore di `Medium` o inferiore.</span><span class="sxs-lookup"><span data-stu-id="10b26-245">Each cmdlet prompts for confirmation if hello `$ConfirmPreference` PowerShell preference variable has a value of `Medium` or lower.</span></span> <span data-ttu-id="10b26-246">Poiché il valore predefinito hello per `$ConfirmPreference` è `High`, queste richieste non vengono assegnate quando si usa PowerShell le impostazioni predefinite di hello.</span><span class="sxs-lookup"><span data-stu-id="10b26-246">Since hello default value for `$ConfirmPreference` is `High`, these prompts are not given when using hello default PowerShell settings.</span></span>

<span data-ttu-id="10b26-247">È possibile eseguire l'override di hello corrente `$ConfirmPreference` impostazione utilizzando hello `-Confirm` parametro.</span><span class="sxs-lookup"><span data-stu-id="10b26-247">You can override hello current `$ConfirmPreference` setting using hello `-Confirm` parameter.</span></span> <span data-ttu-id="10b26-248">Se si specifica `-Confirm` o `-Confirm:$True` , hello cmdlet chiede conferma prima dell'esecuzione.</span><span class="sxs-lookup"><span data-stu-id="10b26-248">If you specify `-Confirm` or `-Confirm:$True` , hello cmdlet prompts you for confirmation before it runs.</span></span> <span data-ttu-id="10b26-249">Se si specifica `-Confirm:$False` , hello cmdlet non viene chiesto di confermare.</span><span class="sxs-lookup"><span data-stu-id="10b26-249">If you specify `-Confirm:$False` , hello cmdlet does not prompt you for confirmation.</span></span> 

<span data-ttu-id="10b26-250">Per altre informazioni su `-Confirm` e `$ConfirmPreference`, vedere [About Preference Variables](https://msdn.microsoft.com/powershell/reference/5.1/Microsoft.PowerShell.Core/about/about_Preference_Variables) (Informazioni sulle variabili di preferenza).</span><span class="sxs-lookup"><span data-stu-id="10b26-250">For more information about `-Confirm` and `$ConfirmPreference`, see [About Preference Variables](https://msdn.microsoft.com/powershell/reference/5.1/Microsoft.PowerShell.Core/about/about_Preference_Variables).</span></span>

## <a name="next-steps"></a><span data-ttu-id="10b26-251">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="10b26-251">Next steps</span></span>

<span data-ttu-id="10b26-252">Altre informazioni su [zone e record nel servizio DNS di Azure](dns-zones-records.md).</span><span class="sxs-lookup"><span data-stu-id="10b26-252">Learn more about [zones and records in Azure DNS](dns-zones-records.md).</span></span>
<br>
<span data-ttu-id="10b26-253">Informazioni su come troppo[proteggere le zone e record](dns-protect-zones-recordsets.md) quando si utilizza il DNS di Azure.</span><span class="sxs-lookup"><span data-stu-id="10b26-253">Learn how too[protect your zones and records](dns-protect-zones-recordsets.md) when using Azure DNS.</span></span>
<br>
<span data-ttu-id="10b26-254">Hello revisione [la documentazione di riferimento di Azure PowerShell DNS](/powershell/module/azurerm.dns).</span><span class="sxs-lookup"><span data-stu-id="10b26-254">Review hello [Azure DNS PowerShell reference documentation](/powershell/module/azurerm.dns).</span></span>

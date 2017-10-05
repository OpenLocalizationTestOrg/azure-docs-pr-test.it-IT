---
title: Hosting di zone DNS di ricerca inversa in DNS Azure | Microsoft Docs
description: Informazioni su come usare DNS Azure per l'hosting delle zone DNS di ricerca inversa per gli intervalli di indirizzi IP
services: dns
documentationcenter: na
author: jtuliani
manager: timlt
ms.service: dns
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 05/29/2017
ms.author: jonatul
ms.openlocfilehash: 3e10b25d2f9b91c96af2958fef6dc6a4fdbff301
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="hosting-reverse-dns-lookup-zones-in-azure-dns"></a><span data-ttu-id="1843c-103">Hosting di zone DNS di ricerca inversa in DNS Azure</span><span class="sxs-lookup"><span data-stu-id="1843c-103">Hosting reverse DNS lookup zones in Azure DNS</span></span>

<span data-ttu-id="1843c-104">Questo articolo illustra come eseguire l'hosting delle zone DNS di ricerca inversa per gli intervalli di indirizzi IP assegnati in DNS Azure.</span><span class="sxs-lookup"><span data-stu-id="1843c-104">This article explains how to host the reverse DNS lookup zones for your assigned IP ranges in Azure DNS.</span></span> <span data-ttu-id="1843c-105">Gli intervalli di indirizzi IP rappresentati dalle zone di ricerca inversa devono essere assegnati all'organizzazione, in genere dal provider di servizi Internet.</span><span class="sxs-lookup"><span data-stu-id="1843c-105">The IP ranges represented by the reverse lookup zone must be assigned to your organization, typically by your ISP.</span></span>

<span data-ttu-id="1843c-106">Per configurare il DNS inverso per un indirizzo IP di proprietà di Azure assegnato al servizio di Azure, vedere [Configure the reverse lookup for the IP addresses allocated to your Azure service](dns-reverse-dns-for-azure-services.md) (Configurare la ricerca inversa per gli indirizzi IP allocati al servizio di Azure).</span><span class="sxs-lookup"><span data-stu-id="1843c-106">To configure reverse DNS for Azure-owned IP address assigned to your Azure service, see [configure the reverse lookup for the IP addresses allocated to your Azure service](dns-reverse-dns-for-azure-services.md).</span></span>

<span data-ttu-id="1843c-107">Prima di leggere questo articolo, è necessario leggere [Panoramica del DNS inverso e supporto in Azure](dns-reverse-dns-overview.md).</span><span class="sxs-lookup"><span data-stu-id="1843c-107">Before reading this article, you should be familiar with this [Overview of reverse DNS and support in Azure](dns-reverse-dns-overview.md).</span></span>

<span data-ttu-id="1843c-108">Questo articolo illustra la procedura per la creazione della prima zona DNS di ricerca inversa e del primo record tramite il portale di Azure, Azure PowerShell, l'interfaccia della riga di comando di Azure 1.0 o l'interfaccia della riga di comando di Azure 2.0.</span><span class="sxs-lookup"><span data-stu-id="1843c-108">This article walks you through the steps to create your first reverse lookup DNS zone and record using the Azure portal, Azure PowerShell, Azure CLI 1.0 or Azure CLI 2.0.</span></span>

## <a name="create-a-reverse-lookup-dns-zone"></a><span data-ttu-id="1843c-109">Creare una zona DNS di ricerca inversa</span><span class="sxs-lookup"><span data-stu-id="1843c-109">Create a reverse lookup DNS zone</span></span>

1. <span data-ttu-id="1843c-110">Accedere al [portale di Azure](https://portal.azure.com)</span><span class="sxs-lookup"><span data-stu-id="1843c-110">Sign in to the [Azure portal](https://portal.azure.com)</span></span>
1. <span data-ttu-id="1843c-111">Nel menu Hub fare clic su **Nuovo** > **Rete** e quindi fare clic su **Zona DNS** per aprire il pannello **Crea zona DNS**.</span><span class="sxs-lookup"><span data-stu-id="1843c-111">On the Hub menu, click and click **New** > **Networking** > and then click **DNS zone** to open the **Create DNS zone** blade.</span></span>

   ![Zona DNS](./media/dns-reverse-dns-hosting/figure1.png)

1. <span data-ttu-id="1843c-113">Nel pannello **Crea zona DNS** assegnare un nome alla zona DNS.</span><span class="sxs-lookup"><span data-stu-id="1843c-113">On the **Create DNS zone** blade, name your DNS zone.</span></span> <span data-ttu-id="1843c-114">Il nome della zona viene configurato in modo diverso per i prefissi IPv4 e IPv6.</span><span class="sxs-lookup"><span data-stu-id="1843c-114">The name of the zone is crafted differently for IPv4 and IPv6 prefixes.</span></span> <span data-ttu-id="1843c-115">Usare le istruzioni per [IPV4](#ipv4) o [IPv6](#ipv6) per specificare un nome per la zona.</span><span class="sxs-lookup"><span data-stu-id="1843c-115">Use either the instructions for [IPV4](#ipv4) or [IPv6](#ipv6) to name your zone.</span></span> <span data-ttu-id="1843c-116">Al termine, fare clic su **Crea** per creare la zona.</span><span class="sxs-lookup"><span data-stu-id="1843c-116">When complete click **Create** to create the zone.</span></span>

### <a name="ipv4"></a><span data-ttu-id="1843c-117">IPv4</span><span class="sxs-lookup"><span data-stu-id="1843c-117">IPv4</span></span>

<span data-ttu-id="1843c-118">Il nome di una zona di ricerca inversa IPv4 è basato sull'intervallo da essa rappresentato.</span><span class="sxs-lookup"><span data-stu-id="1843c-118">The name of an IPv4 reverse lookup zone is based on the IP range it represents.</span></span> <span data-ttu-id="1843c-119">Deve avere il formato seguente: `<IPv4 network prefix in reverse order>.in-addr.arpa`.</span><span class="sxs-lookup"><span data-stu-id="1843c-119">It should be in the following format: `<IPv4 network prefix in reverse order>.in-addr.arpa`.</span></span> <span data-ttu-id="1843c-120">Per esempi, vedere [Panoramica del DNS inverso e supporto in Azure](dns-reverse-dns-overview.md#ipv4).</span><span class="sxs-lookup"><span data-stu-id="1843c-120">For examples, see [overview of reverse DNS and support in Azure](dns-reverse-dns-overview.md#ipv4).</span></span>

> [!NOTE]
> <span data-ttu-id="1843c-121">Quando si creano zone DNS di ricerca inversa senza classi in DNS Azure, è necessario usare un trattino (`-`) invece di una barra rovesciata ('/') nel nome della zona.</span><span class="sxs-lookup"><span data-stu-id="1843c-121">When creating classless reverse DNS lookup zones in Azure DNS, you must use a hyphen (`-`) rather than a forward slash ('/') in the zone name.</span></span>
>
> <span data-ttu-id="1843c-122">Ad esempio, per l'intervallo di indirizzi IP 192.0.2.128/26 è necessario usare `128-26.2.0.192.in-addr.arpa` come nome della zona invece di `128/26.2.0.192.in-addr.arpa`.</span><span class="sxs-lookup"><span data-stu-id="1843c-122">For example, for the IP range 192.0.2.128/26, you must use `128-26.2.0.192.in-addr.arpa` as the zone name instead of `128/26.2.0.192.in-addr.arpa`.</span></span>
>
> <span data-ttu-id="1843c-123">Anche se entrambi sono supportati dagli standard DNS, infatti, i nomi di zona DNS contenenti il carattere di barra rovesciata (`/`) non sono supportati in DNS Azure.</span><span class="sxs-lookup"><span data-stu-id="1843c-123">This is because, while both are supported by the DNS standards, DNS zone names containing the forward slash (`/`) character are not supported in Azure DNS.</span></span>

<span data-ttu-id="1843c-124">L'esempio seguente mostra come creare una zona del DNS inverso di tipo "classe C" con nome `2.0.192.in-addr.arpa` in DNS Azure tramite il portale di Azure:</span><span class="sxs-lookup"><span data-stu-id="1843c-124">The following example shows how to create a 'Class C' reverse DNS zone named `2.0.192.in-addr.arpa` in Azure DNS via the Azure portal:</span></span>

 ![Creare una zona DNS](./media/dns-reverse-dns-hosting/figure2.png)

<span data-ttu-id="1843c-126">"Località del gruppo di risorse" indica la posizione del gruppo di risorse e non ha alcun impatto sulla zona DNS.</span><span class="sxs-lookup"><span data-stu-id="1843c-126">The 'Resource group location' defines the location for the resource group, and has no impact on the DNS zone.</span></span> <span data-ttu-id="1843c-127">La posizione della zona DNS è sempre "globale" e non viene visualizzata.</span><span class="sxs-lookup"><span data-stu-id="1843c-127">The DNS zone location is always 'global', and is not shown.</span></span>

<span data-ttu-id="1843c-128">Gli esempi seguenti mostrano come completare questa attività con Azure PowerShell e l'interfaccia della riga di comando di Azure:</span><span class="sxs-lookup"><span data-stu-id="1843c-128">The following examples show how to complete this task with Azure PowerShell and the Azure CLI:</span></span>

#### <a name="powershell"></a><span data-ttu-id="1843c-129">PowerShell</span><span class="sxs-lookup"><span data-stu-id="1843c-129">PowerShell</span></span>

```powershell
New-AzureRmDnsZone -Name 2.0.192.in-addr.arpa -ResourceGroupName MyResourceGroup
```

#### <a name="azure-cli-10"></a><span data-ttu-id="1843c-130">Interfaccia della riga di comando di Azure 1.0</span><span class="sxs-lookup"><span data-stu-id="1843c-130">Azure CLI 1.0</span></span>

```azurecli
azure network dns zone create MyResourceGroup 2.0.192.in-addr.arpa
```

#### <a name="azure-cli-20"></a><span data-ttu-id="1843c-131">Interfaccia della riga di comando di Azure 2.0</span><span class="sxs-lookup"><span data-stu-id="1843c-131">Azure CLI 2.0</span></span>

```azurecli
az network dns zone create -g MyResourceGroup -n 2.0.192.in-addr.arpa
```

### <a name="ipv6"></a><span data-ttu-id="1843c-132">IPv6</span><span class="sxs-lookup"><span data-stu-id="1843c-132">IPv6</span></span>

<span data-ttu-id="1843c-133">Il nome di una zona di ricerca inversa di tipo IPv6 deve avere il formato seguente: `<IPv6 network prefix in reverse order>.ip6.arpa`.</span><span class="sxs-lookup"><span data-stu-id="1843c-133">The name of an IPv6 reverse lookup zone should be in the following form: `<IPv6 network prefix in reverse order>.ip6.arpa`.</span></span>  <span data-ttu-id="1843c-134">Per esempi, vedere [Panoramica del DNS inverso e supporto in Azure](dns-reverse-dns-overview.md#ipv6).</span><span class="sxs-lookup"><span data-stu-id="1843c-134">For examples, see [overview of reverse DNS and support in Azure](dns-reverse-dns-overview.md#ipv6).</span></span>


<span data-ttu-id="1843c-135">L'esempio seguente mostra come creare una zona DNS di ricerca inversa di tipo IPv6 con nome `0.0.0.0.d.c.b.a.8.b.d.0.1.0.0.2.ip6.arpa` in DNS Azure tramite il portale di Azure:</span><span class="sxs-lookup"><span data-stu-id="1843c-135">The following example shows how to create an IPv6 reverse DNS lookup zone named `0.0.0.0.d.c.b.a.8.b.d.0.1.0.0.2.ip6.arpa` in Azure DNS via the Azure portal:</span></span>

 ![Creare una zona DNS](./media/dns-reverse-dns-hosting/figure3.png)

<span data-ttu-id="1843c-137">"Località del gruppo di risorse" indica la posizione del gruppo di risorse e non ha alcun impatto sulla zona DNS.</span><span class="sxs-lookup"><span data-stu-id="1843c-137">The 'Resource group location' defines the location for the resource group, and has no impact on the DNS zone.</span></span> <span data-ttu-id="1843c-138">La posizione della zona DNS è sempre "globale" e non viene visualizzata.</span><span class="sxs-lookup"><span data-stu-id="1843c-138">The DNS zone location is always 'global', and is not shown.</span></span>

<span data-ttu-id="1843c-139">Gli esempi seguenti mostrano come completare questa attività con Azure PowerShell e l'interfaccia della riga di comando di Azure:</span><span class="sxs-lookup"><span data-stu-id="1843c-139">The following examples show how to complete this task with Azure PowerShell and the Azure CLI:</span></span>

#### <a name="powershell"></a><span data-ttu-id="1843c-140">PowerShell</span><span class="sxs-lookup"><span data-stu-id="1843c-140">PowerShell</span></span>

```powershell
New-AzureRmDnsZone -Name 0.0.0.0.d.c.b.a.8.b.d.0.1.0.0.2.ip6.arpa -ResourceGroupName MyResourceGroup
```

#### <a name="azurecli-10"></a><span data-ttu-id="1843c-141">Interfaccia della riga di comando di Azure 1.0</span><span class="sxs-lookup"><span data-stu-id="1843c-141">AzureCLI 1.0</span></span>

```azurecli
azure network dns zone create MyResourceGroup 0.0.0.0.d.c.b.a.8.b.d.0.1.0.0.2.ip6.arpa
```

#### <a name="azurecli-20"></a><span data-ttu-id="1843c-142">Interfaccia della riga di comando di Azure 2.0</span><span class="sxs-lookup"><span data-stu-id="1843c-142">AzureCLI 2.0</span></span>

```azurecli
az network dns zone create -g MyResourceGroup -n 0.0.0.0.d.c.b.a.8.b.d.0.1.0.0.2.ip6.arpa
```

## <a name="delegate-a-reverse-dns-lookup-zone"></a><span data-ttu-id="1843c-143">Delegare una zona DNS di ricerca inversa</span><span class="sxs-lookup"><span data-stu-id="1843c-143">Delegate a reverse DNS lookup zone</span></span>

<span data-ttu-id="1843c-144">Dopo avere creato la zona DNS di ricerca inversa, è necessario assicurarsi che la zona sia delegata dalla zona padre.</span><span class="sxs-lookup"><span data-stu-id="1843c-144">Having created your reverse DNS lookup zone, you must ensure that the zone is delegated from the parent zone.</span></span> <span data-ttu-id="1843c-145">La delega DNS consente al processo di risoluzione del nome DNS di trovare i server dei nomi che ospitano la zona DNS di ricerca inversa.</span><span class="sxs-lookup"><span data-stu-id="1843c-145">DNS delegation enables the DNS name resolution process to find the name servers hosting your reverse DNS lookup zone.</span></span> <span data-ttu-id="1843c-146">Ciò consente ai server dei nomi di rispondere alle query del DNS inverso per gli indirizzi IP disponibili nell'intervallo di indirizzi.</span><span class="sxs-lookup"><span data-stu-id="1843c-146">This enables those name servers to answer DNS reverse queries for the IP addresses in your address range.</span></span>

<span data-ttu-id="1843c-147">Per le zone di ricerca diretta il processo di delega di una zona DNS è illustrato in [Delegare un dominio a DNS Azure](dns-delegate-domain-azure-dns.md).</span><span class="sxs-lookup"><span data-stu-id="1843c-147">For forward lookup zones, the process of delegating a DNS zone is described in [Delegate your domain to Azure DNS](dns-delegate-domain-azure-dns.md).</span></span> <span data-ttu-id="1843c-148">La delega per le zone di ricerca inversa funziona nello stesso modo.</span><span class="sxs-lookup"><span data-stu-id="1843c-148">Delegation for reverse lookup zones works the same way.</span></span> <span data-ttu-id="1843c-149">L'unica differenza è costituita dal fatto che è necessario configurare i server dei nomi con il provider di servizi Internet che ha fornito l'intervallo di indirizzi IP, invece del registrar.</span><span class="sxs-lookup"><span data-stu-id="1843c-149">The only difference is that you need to configure the name servers with the ISP who provided your IP range, rather than your domain name registrar.</span></span>

## <a name="create-a-dns-ptr-record"></a><span data-ttu-id="1843c-150">Creare un record PTR DNS</span><span class="sxs-lookup"><span data-stu-id="1843c-150">Create a DNS PTR record</span></span>

### <a name="ipv4"></a><span data-ttu-id="1843c-151">IPv4</span><span class="sxs-lookup"><span data-stu-id="1843c-151">IPv4</span></span>

<span data-ttu-id="1843c-152">L'esempio seguente illustra la procedura di creazione di un record PTR in una zona del DNS inverso in DNS Azure.</span><span class="sxs-lookup"><span data-stu-id="1843c-152">The following example walks you through the process of creating a PTR record in a reverse DNS zone in Azure DNS.</span></span> <span data-ttu-id="1843c-153">Per altri tipi di record e per modificare i record esistenti, vedere [Gestire record e set di record DNS con il portale di Azure](dns-operations-recordsets-portal.md).</span><span class="sxs-lookup"><span data-stu-id="1843c-153">For other record types and to modify existing records, see [Manage DNS records and record sets by using the Azure portal](dns-operations-recordsets-portal.md).</span></span>

1.  <span data-ttu-id="1843c-154">Nella parte superiore del pannello **Zona DNS** selezionare **+ Record set** (Aggiungi set di record) per aprire il pannello **Aggiungi set di record**.</span><span class="sxs-lookup"><span data-stu-id="1843c-154">At the top of the **DNS zone** blade, select **+ Record set** to open the **Add record set** blade.</span></span>

 ![Zona DNS](./media/dns-reverse-dns-hosting/figure4.png)

1. <span data-ttu-id="1843c-156">Nel pannello **Aggiungi set di record**.</span><span class="sxs-lookup"><span data-stu-id="1843c-156">On the **Add record set** blade.</span></span> 
1. <span data-ttu-id="1843c-157">Selezionare **PTR** dal menu "**Tipo**" del record.</span><span class="sxs-lookup"><span data-stu-id="1843c-157">Select **PTR** from the record "**Type**" menu.</span></span>  
1. <span data-ttu-id="1843c-158">Il nome del set di record per un record PTR deve corrispondere al resto dell'indirizzo IPv4 in ordine inverso.</span><span class="sxs-lookup"><span data-stu-id="1843c-158">The name of the record set for a PTR record needs to be the rest of the IPv4 address in reverse order.</span></span> <span data-ttu-id="1843c-159">In questo esempio i primi tre ottetti sono già popolati come parte del nome della zona (.2.0.192).</span><span class="sxs-lookup"><span data-stu-id="1843c-159">In this example, the first three octets are already populated as part of the zone name (.2.0.192).</span></span> <span data-ttu-id="1843c-160">Solo l'ultimo ottetto viene quindi fornito nel campo del nome.</span><span class="sxs-lookup"><span data-stu-id="1843c-160">Therefore, only the last octet is supplied in the name field.</span></span> <span data-ttu-id="1843c-161">Ad esempio, è possibile assegnare il nome "**15**" a un set di record per una risorsa il cui indirizzo IP è 192.0.2.15.</span><span class="sxs-lookup"><span data-stu-id="1843c-161">For example, you could name your record set "**15**" for a resource whose IP address is 192.0.2.15.</span></span>  
1. <span data-ttu-id="1843c-162">Nel campo "**Nome dominio**" immettere il nome di dominio completo della risorsa usando l'indirizzo IP.</span><span class="sxs-lookup"><span data-stu-id="1843c-162">In the "**Domain Name**" field, enter the fully qualified domain name (FQDN) of the resource using the IP.</span></span>
1. <span data-ttu-id="1843c-163">Selezionare **OK** nella parte inferiore del pannello per creare il record DNS.</span><span class="sxs-lookup"><span data-stu-id="1843c-163">Select **OK** at the bottom of the blade to create the DNS record.</span></span>

 ![Aggiungi set di record](./media/dns-reverse-dns-hosting/figure5.png)

<span data-ttu-id="1843c-165">Gli esempi seguenti mostrano come completare questa attività con PowerShell e l'interfaccia della riga di comando di Azure:</span><span class="sxs-lookup"><span data-stu-id="1843c-165">The following are examples on how to complete this task with PowerShell and the AzureCLI:</span></span>

#### <a name="powershell"></a><span data-ttu-id="1843c-166">PowerShell</span><span class="sxs-lookup"><span data-stu-id="1843c-166">PowerShell</span></span>

```powershell
New-AzureRmDnsRecordSet -Name 15 -RecordType PTR -ZoneName 2.0.192.in-addr.arpa -ResourceGroupName MyResourceGroup -Ttl 3600 -DnsRecords (New-AzureRmDnsRecordConfig -Ptrdname "dc1.contoso.com")
```
#### <a name="azurecli-10"></a><span data-ttu-id="1843c-167">Interfaccia della riga di comando di Azure 1.0</span><span class="sxs-lookup"><span data-stu-id="1843c-167">AzureCLI 1.0</span></span>

```azurecli
azure network dns record-set add-record MyResourceGroup 2.0.192.in-addr.arpa 15 PTR --ptrdname dc1.contoso.com  
```

#### <a name="azurecli-20"></a><span data-ttu-id="1843c-168">Interfaccia della riga di comando di Azure 2.0</span><span class="sxs-lookup"><span data-stu-id="1843c-168">AzureCLI 2.0</span></span>

```azurecli
    az network dns record-set ptr add-record -g MyResourceGroup -z 2.0.192.in-addr.arpa -n 15 --ptrdname dc1.contoso.com
```

### <a name="ipv6"></a><span data-ttu-id="1843c-169">IPv6</span><span class="sxs-lookup"><span data-stu-id="1843c-169">IPv6</span></span>

<span data-ttu-id="1843c-170">L'esempio seguente fornisce indicazioni dettagliate sul processo di creazione di un nuovo record "PTR".</span><span class="sxs-lookup"><span data-stu-id="1843c-170">The following example walks you through the process of creating new 'PTR' record.</span></span> <span data-ttu-id="1843c-171">Per altri tipi di record e per modificare i record esistenti, vedere [Gestire record e set di record DNS con il portale di Azure](dns-operations-recordsets-portal.md).</span><span class="sxs-lookup"><span data-stu-id="1843c-171">For other record types and to modify existing records, see [Manage DNS records and record sets by using the Azure portal](dns-operations-recordsets-portal.md).</span></span>

1. <span data-ttu-id="1843c-172">Nella parte superiore del pannello **Zona DNS** selezionare **+ Set di record** per aprire il pannello **Aggiungi set di record**.</span><span class="sxs-lookup"><span data-stu-id="1843c-172">At the top of the **DNS zone blade**, select **+ Record set** to open the **Add record set** blade.</span></span>

  ![Pannello Zona DNS](./media/dns-reverse-dns-hosting/figure6.png)

2. <span data-ttu-id="1843c-174">Nel pannello **Aggiungi set di record**.</span><span class="sxs-lookup"><span data-stu-id="1843c-174">On the **Add record set** blade.</span></span> 
3. <span data-ttu-id="1843c-175">Selezionare **PTR** dal menu "**Tipo**" del record.</span><span class="sxs-lookup"><span data-stu-id="1843c-175">Select **PTR** from the record "**Type**" menu.</span></span>  
4. <span data-ttu-id="1843c-176">Il nome del set di record per un record PTR deve corrispondere al resto dell'indirizzo IPv6 in ordine inverso.</span><span class="sxs-lookup"><span data-stu-id="1843c-176">The name of the record set for a PTR record needs to be the rest of the IPv6 address in reverse order.</span></span> <span data-ttu-id="1843c-177">Non deve includere alcuna compressione degli zeri.</span><span class="sxs-lookup"><span data-stu-id="1843c-177">It must not include any zero compression.</span></span> <span data-ttu-id="1843c-178">In questo esempio i primi 64 bit dell'indirizzo IPv6 sono già popolati come parte del nome della zona (0.0.0.0.c.d.b.a.8.b.d.0.1.0.0.2.ip6.arpa).</span><span class="sxs-lookup"><span data-stu-id="1843c-178">In this example, the first 64 bits of the IPv6 are already populated as part of the zone name (0.0.0.0.c.d.b.a.8.b.d.0.1.0.0.2.ip6.arpa).</span></span> <span data-ttu-id="1843c-179">Solo gli ultimi 64 bit vengono quindi forniti nel campo del nome.</span><span class="sxs-lookup"><span data-stu-id="1843c-179">Therefore, only the last 64 bits are supplied in the name field.</span></span> <span data-ttu-id="1843c-180">Gli ultimi 64 bit dell'indirizzo IP vengono immessi in ordine inverso, usando un punto come delimitatore tra ogni numero esadecimale.</span><span class="sxs-lookup"><span data-stu-id="1843c-180">The last 64 bits of the IP address are entered in reverse order, using a period as the delimiter between each hexadecimal number.</span></span> <span data-ttu-id="1843c-181">Ad esempio, è possibile specificare "**e.5.0.4.9.f.a.1.c.b.0.1.4.2.5.f**" come nome di un set di record per una risorsa il cui indirizzo IP è 2001:0db8:abdc:0000:f524:10bc:1af9:405e.</span><span class="sxs-lookup"><span data-stu-id="1843c-181">For example, you could name your record set "**e.5.0.4.9.f.a.1.c.b.0.1.4.2.5.f**" for a resource whose IP address is 2001:0db8:abdc:0000:f524:10bc:1af9:405e.</span></span>  
5. <span data-ttu-id="1843c-182">Nel campo "**Nome dominio**" immettere il nome di dominio completo della risorsa usando l'indirizzo IP.</span><span class="sxs-lookup"><span data-stu-id="1843c-182">In the "**Domain Name**" field, enter the fully qualified domain name (FQDN) of the resource using the IP.</span></span>
6. <span data-ttu-id="1843c-183">Selezionare **OK** nella parte inferiore del pannello per creare il record DNS.</span><span class="sxs-lookup"><span data-stu-id="1843c-183">Select **OK** at the bottom of the blade to create the DNS record.</span></span>

![Pannello Aggiungi set di record](./media/dns-reverse-dns-hosting/figure7.png)

<span data-ttu-id="1843c-185">Gli esempi seguenti mostrano come completare questa attività con PowerShell e l'interfaccia della riga di comando di Azure:</span><span class="sxs-lookup"><span data-stu-id="1843c-185">The following are examples on how to complete this task with PowerShell and the AzureCLI:</span></span>

#### <a name="powershell"></a><span data-ttu-id="1843c-186">PowerShell</span><span class="sxs-lookup"><span data-stu-id="1843c-186">PowerShell</span></span>

```powershell
New-AzureRmDnsRecordSet -Name "e.5.0.4.9.f.a.1.c.b.0.1.4.2.5.f" -RecordType PTR -ZoneName 0.0.0.0.c.d.b.a.8.b.d.0.1.0.0.2.ip6.arpa -ResourceGroupName MyResourceGroup -Ttl 3600 -DnsRecords (New-AzureRmDnsRecordConfig -Ptrdname "dc2.contoso.com")
```

#### <a name="azurecli-10"></a><span data-ttu-id="1843c-187">Interfaccia della riga di comando di Azure 1.0</span><span class="sxs-lookup"><span data-stu-id="1843c-187">AzureCLI 1.0</span></span>

```
azure network dns record-set add-record MyResourceGroup 0.0.0.0.c.d.b.a.8.b.d.0.1.0.0.2.ip6.arpa e.5.0.4.9.f.a.1.c.b.0.1.4.2.5.f PTR --ptrdname dc2.contoso.com 
```
 
#### <a name="azurecli-20"></a><span data-ttu-id="1843c-188">Interfaccia della riga di comando di Azure 2.0</span><span class="sxs-lookup"><span data-stu-id="1843c-188">AzureCLI 2.0</span></span>

```azurecli
    az network dns record-set ptr add-record -g MyResourceGroup -z 0.0.0.0.c.d.b.a.8.b.d.0.1.0.0.2.ip6.arpa -n e.5.0.4.9.f.a.1.c.b.0.1.4.2.5.f --ptrdname dc2.contoso.com
```

## <a name="view-records"></a><span data-ttu-id="1843c-189">Visualizzare i record</span><span class="sxs-lookup"><span data-stu-id="1843c-189">View Records</span></span>

<span data-ttu-id="1843c-190">Per visualizzare i record creati, passare alla zona DNS nel portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="1843c-190">To view the records you created, navigate to your DNS zone in the Azure portal.</span></span> <span data-ttu-id="1843c-191">Nella parte inferiore del pannello **Zona DNS** è possibile visualizzare i record per la zona DNS.</span><span class="sxs-lookup"><span data-stu-id="1843c-191">In the lower part of the **DNS zone** blade, you can see the records for the DNS zone.</span></span> <span data-ttu-id="1843c-192">Verranno visualizzati i record NS e SOA predefiniti, che vengono creati in ogni zona, ed eventuali nuovi record creati.</span><span class="sxs-lookup"><span data-stu-id="1843c-192">You should see the default NS and SOA records, which are created in every zone, plus any new records you have created.</span></span>

### <a name="ipv4"></a><span data-ttu-id="1843c-193">IPv4</span><span class="sxs-lookup"><span data-stu-id="1843c-193">IPv4</span></span>

<span data-ttu-id="1843c-194">Pannello Zona DNS con i record PTR IPv4:</span><span class="sxs-lookup"><span data-stu-id="1843c-194">DNS zone blade, showing IPv4 PTR records:</span></span>

![Pannello Zona DNS](./media/dns-reverse-dns-hosting/figure8.png)

<span data-ttu-id="1843c-196">Gli esempi seguenti mostrano come visualizzare i record PTR usando PowerShell o l'interfaccia della riga di comando di Azure:</span><span class="sxs-lookup"><span data-stu-id="1843c-196">The following examples show how to view the PTR records using PowerShell or the Azure CLI:</span></span>

#### <a name="powershell"></a><span data-ttu-id="1843c-197">PowerShell</span><span class="sxs-lookup"><span data-stu-id="1843c-197">PowerShell</span></span>

```powershell
Get-AzureRmDnsRecordSet -ZoneName 2.0.192.in-addr.arpa -ResourceGroupName MyResourceGroup
```

#### <a name="azure-cli-10"></a><span data-ttu-id="1843c-198">Interfaccia della riga di comando di Azure 1.0</span><span class="sxs-lookup"><span data-stu-id="1843c-198">Azure CLI 1.0</span></span>

```azurecli
    azure network dns record-set list MyResourceGroup 2.0.192.in-addr.arpa
```

#### <a name="azure-cli-20"></a><span data-ttu-id="1843c-199">Interfaccia della riga di comando di Azure 2.0</span><span class="sxs-lookup"><span data-stu-id="1843c-199">Azure CLI 2.0</span></span>

```azurecli
    azure network dns record-set list -g MyResourceGroup -z 2.0.192.in-addr.arpa
```

### <a name="ipv6"></a><span data-ttu-id="1843c-200">IPv6</span><span class="sxs-lookup"><span data-stu-id="1843c-200">IPv6</span></span>

<span data-ttu-id="1843c-201">Pannello Zona DNS con i record PTR IPv6:</span><span class="sxs-lookup"><span data-stu-id="1843c-201">DNS zone blade, showing IPv6 PTR records:</span></span>

![Pannello Zona DNS](./media/dns-reverse-dns-hosting/figure9.png)

<span data-ttu-id="1843c-203">Gli esempi seguenti mostrano come visualizzare i record con PowerShell e con l'interfaccia della riga di comando di Azure:</span><span class="sxs-lookup"><span data-stu-id="1843c-203">The following are examples on how to view the records with PowerShell and the AzureCLI:</span></span>

#### <a name="powershell"></a><span data-ttu-id="1843c-204">PowerShell</span><span class="sxs-lookup"><span data-stu-id="1843c-204">PowerShell</span></span>

```powershell
Get-AzureRmDnsRecordSet -ZoneName 0.0.0.0.c.d.b.a.8.b.d.0.1.0.0.2.ip6.arpa -ResourceGroupName MyResourceGroup
```

#### <a name="azure-cli-10"></a><span data-ttu-id="1843c-205">Interfaccia della riga di comando di Azure 1.0</span><span class="sxs-lookup"><span data-stu-id="1843c-205">Azure CLI 1.0</span></span>

```azurecli
    azure network dns record-set list MyResourceGroup 0.0.0.0.c.d.b.a.8.b.d.0.1.0.0.2.ip6.arpa
```

#### <a name="azure-cli-20"></a><span data-ttu-id="1843c-206">Interfaccia della riga di comando di Azure 2.0</span><span class="sxs-lookup"><span data-stu-id="1843c-206">Azure CLI 2.0</span></span>

```azurecli
    azure network dns record-set list -g MyResourceGroup -z 0.0.0.0.c.d.b.a.8.b.d.0.1.0.0.2.ip6.arpa
```

## <a name="faq"></a><span data-ttu-id="1843c-207">domande frequenti</span><span class="sxs-lookup"><span data-stu-id="1843c-207">FAQ</span></span>

### <a name="can-i-host-reverse-dns-lookup-zones-for-my-isp-assigned-ip-blocks-on-azure-dns"></a><span data-ttu-id="1843c-208">È possibile ospitare zone DNS di ricerca inversa per i blocchi di indirizzi IP assegnati dal provider di servizi Internet in DNS Azure?</span><span class="sxs-lookup"><span data-stu-id="1843c-208">Can I host reverse DNS lookup zones for my ISP-assigned IP blocks on Azure DNS?</span></span>

<span data-ttu-id="1843c-209">Sì.</span><span class="sxs-lookup"><span data-stu-id="1843c-209">Yes.</span></span> <span data-ttu-id="1843c-210">L'hosting delle zone di ricerca inversa (ARPA) per gli intervalli di indirizzi IP in DNS Azure DNS è completamento supportato.</span><span class="sxs-lookup"><span data-stu-id="1843c-210">Hosting the reverse lookup (ARPA) zones for your own IP ranges in Azure DNS is fully supported.</span></span>

<span data-ttu-id="1843c-211">Creare le zone di ricerca inversa in DNS Azure come illustrato in questo articolo, quindi collaborare con il provider di servizi Internet per [delegare la zona](dns-domain-delegation.md).</span><span class="sxs-lookup"><span data-stu-id="1843c-211">Create the reverse lookup zone in Azure DNS as explained in this article, then work with your ISP to [delegate the zone](dns-domain-delegation.md).</span></span>  <span data-ttu-id="1843c-212">Sarà quindi possibile gestire i record PTR per ogni ricerca inversa come per gli altri tipi di record.</span><span class="sxs-lookup"><span data-stu-id="1843c-212">You can then manage the PTR records for each reverse lookup in the same way as other record types.</span></span>

### <a name="how-much-does-hosting-my-reverse-dns-lookup-zone-cost"></a><span data-ttu-id="1843c-213">Quanto costa l'hosting della zona DNS di ricerca inversa?</span><span class="sxs-lookup"><span data-stu-id="1843c-213">How much does hosting my reverse DNS lookup zone cost?</span></span>

<span data-ttu-id="1843c-214">L'hosting della zona DNS di ricerca inversa per i blocchi di indirizzi IP assegnati dal provider di servizi Internet in DNS Azure viene addebitato in base alle [tariffe standard per DNS Azure](https://azure.microsoft.com/pricing/details/dns/).</span><span class="sxs-lookup"><span data-stu-id="1843c-214">Hosting the reverse DNS lookup zone for your ISP-assigned IP block in Azure DNS is charged at [standard Azure DNS rates](https://azure.microsoft.com/pricing/details/dns/).</span></span>

### <a name="can-i-host-reverse-dns-lookup-zones-for-both-ipv4-and-ipv6-addresses-in-azure-dns"></a><span data-ttu-id="1843c-215">È possibile ospitare zone DNS di ricerca inversa per indirizzi IPv4 e IPv6 in DNS Azure?</span><span class="sxs-lookup"><span data-stu-id="1843c-215">Can I host reverse DNS lookup zones for both IPv4 and IPv6 addresses in Azure DNS?</span></span>

<span data-ttu-id="1843c-216">Sì.</span><span class="sxs-lookup"><span data-stu-id="1843c-216">Yes.</span></span> <span data-ttu-id="1843c-217">Questo articolo illustra come creare zone DNS di ricerca inversa di tipo IPv4 e IPv6 in DNS Azure.</span><span class="sxs-lookup"><span data-stu-id="1843c-217">This article explains how to create both IPv4 and IPv6 reverse DNS lookup zones in Azure DNS.</span></span>

### <a name="can-i-import-an-existing-reverse-dns-lookup-zone"></a><span data-ttu-id="1843c-218">È possibile importare una zona DNS di ricerca inversa esistente?</span><span class="sxs-lookup"><span data-stu-id="1843c-218">Can I import an existing reverse DNS lookup zone?</span></span>

<span data-ttu-id="1843c-219">Sì.</span><span class="sxs-lookup"><span data-stu-id="1843c-219">Yes.</span></span> <span data-ttu-id="1843c-220">È possibile usare l'interfaccia della riga di comando di Azure per importare zone DNS di ricerca inversa esistenti in DNS Azure.</span><span class="sxs-lookup"><span data-stu-id="1843c-220">You can use the Azure CLI to import existing DNS zones into Azure DNS.</span></span> <span data-ttu-id="1843c-221">Questo approccio è applicabile alle zone di ricerca diretta e alle zone DNS di ricerca inversa.</span><span class="sxs-lookup"><span data-stu-id="1843c-221">This works for both forward lookup zones and reverse lookup zones.</span></span>

<span data-ttu-id="1843c-222">Per altre informazioni, vedere [Importare ed esportare un file di zona DNS usando l'interfaccia della riga di comando di Azure](dns-import-export.md).</span><span class="sxs-lookup"><span data-stu-id="1843c-222">For more information, see [Import and export a DNS zone file using the Azure CLI](dns-import-export.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="1843c-223">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="1843c-223">Next steps</span></span>

<span data-ttu-id="1843c-224">Per altre informazioni sul DNS inverso, vedere [Risoluzione DNS inversa su Wikipedia](http://en.wikipedia.org/wiki/Reverse_DNS_lookup).</span><span class="sxs-lookup"><span data-stu-id="1843c-224">For more information on reverse DNS, see [reverse DNS lookup on Wikipedia](http://en.wikipedia.org/wiki/Reverse_DNS_lookup).</span></span>
<br>
<span data-ttu-id="1843c-225">Informazioni su come [gestire i record di DNS inverso per i servizi di Azure](dns-reverse-dns-for-azure-services.md).</span><span class="sxs-lookup"><span data-stu-id="1843c-225">Learn how to [manage reverse DNS records for your Azure services](dns-reverse-dns-for-azure-services.md).</span></span>

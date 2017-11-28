---
title: aaaHosting invertire le zone di ricerca DNS nel sistema DNS di Azure | Documenti Microsoft
description: Informazioni su come hello toohost DNS di Azure di toouse invertire le zone di ricerca DNS per gli intervalli IP
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
ms.openlocfilehash: 24feb8ef1c75a7d91938867f348fed1190046e4e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="hosting-reverse-dns-lookup-zones-in-azure-dns"></a><span data-ttu-id="e85c7-103">Hosting di zone DNS di ricerca inversa in DNS Azure</span><span class="sxs-lookup"><span data-stu-id="e85c7-103">Hosting reverse DNS lookup zones in Azure DNS</span></span>

<span data-ttu-id="e85c7-104">Questo articolo spiega come toohost hello invertire le zone di ricerca DNS per gli intervalli IP assegnati in DNS di Azure.</span><span class="sxs-lookup"><span data-stu-id="e85c7-104">This article explains how toohost hello reverse DNS lookup zones for your assigned IP ranges in Azure DNS.</span></span> <span data-ttu-id="e85c7-105">gli intervalli IP Hello rappresentati da una zona di ricerca inversa hello devono essere assegnati tooyour organizzazione, in genere dal provider di servizi Internet.</span><span class="sxs-lookup"><span data-stu-id="e85c7-105">hello IP ranges represented by hello reverse lookup zone must be assigned tooyour organization, typically by your ISP.</span></span>

<span data-ttu-id="e85c7-106">tooconfigure inversa DNS per Azure di proprietà IP indirizzo assegnato tooyour servizio di Azure, vedere [configurare ricerca inversa hello per gli indirizzi IP di hello allocati tooyour servizio Azure](dns-reverse-dns-for-azure-services.md).</span><span class="sxs-lookup"><span data-stu-id="e85c7-106">tooconfigure reverse DNS for Azure-owned IP address assigned tooyour Azure service, see [configure hello reverse lookup for hello IP addresses allocated tooyour Azure service](dns-reverse-dns-for-azure-services.md).</span></span>

<span data-ttu-id="e85c7-107">Prima di leggere questo articolo, è necessario leggere [Panoramica del DNS inverso e supporto in Azure](dns-reverse-dns-overview.md).</span><span class="sxs-lookup"><span data-stu-id="e85c7-107">Before reading this article, you should be familiar with this [Overview of reverse DNS and support in Azure](dns-reverse-dns-overview.md).</span></span>

<span data-ttu-id="e85c7-108">In questo articolo illustra hello passaggi toocreate prima zona di ricerca inversa DNS il record utilizzando hello portale di Azure PowerShell di Azure, Azure CLI 1.0 o 2.0 CLI di Azure.</span><span class="sxs-lookup"><span data-stu-id="e85c7-108">This article walks you through hello steps toocreate your first reverse lookup DNS zone and record using hello Azure portal, Azure PowerShell, Azure CLI 1.0 or Azure CLI 2.0.</span></span>

## <a name="create-a-reverse-lookup-dns-zone"></a><span data-ttu-id="e85c7-109">Creare una zona DNS di ricerca inversa</span><span class="sxs-lookup"><span data-stu-id="e85c7-109">Create a reverse lookup DNS zone</span></span>

1. <span data-ttu-id="e85c7-110">Accedi toohello [portale di Azure](https://portal.azure.com)</span><span class="sxs-lookup"><span data-stu-id="e85c7-110">Sign in toohello [Azure portal](https://portal.azure.com)</span></span>
1. <span data-ttu-id="e85c7-111">Nel menu Hub hello, fare clic su e fare clic su **New** > **rete** > e quindi fare clic su **zona DNS** tooopen hello **zona di DNS creare**blade.</span><span class="sxs-lookup"><span data-stu-id="e85c7-111">On hello Hub menu, click and click **New** > **Networking** > and then click **DNS zone** tooopen hello **Create DNS zone** blade.</span></span>

   ![Zona DNS](./media/dns-reverse-dns-hosting/figure1.png)

1. <span data-ttu-id="e85c7-113">In hello **zona DNS creare** pannello denominare la zona DNS.</span><span class="sxs-lookup"><span data-stu-id="e85c7-113">On hello **Create DNS zone** blade, name your DNS zone.</span></span> <span data-ttu-id="e85c7-114">nome Hello della zona di hello è impostata in modo diverso per i prefissi IPv4 e IPv6.</span><span class="sxs-lookup"><span data-stu-id="e85c7-114">hello name of hello zone is crafted differently for IPv4 and IPv6 prefixes.</span></span> <span data-ttu-id="e85c7-115">Utilizzare le istruzioni entrambi hello per [IPV4](#ipv4) o [IPv6](#ipv6) tooname la zona.</span><span class="sxs-lookup"><span data-stu-id="e85c7-115">Use either hello instructions for [IPV4](#ipv4) or [IPv6](#ipv6) tooname your zone.</span></span> <span data-ttu-id="e85c7-116">Al termine fare clic su **crea** zona hello toocreate.</span><span class="sxs-lookup"><span data-stu-id="e85c7-116">When complete click **Create** toocreate hello zone.</span></span>

### <a name="ipv4"></a><span data-ttu-id="e85c7-117">IPv4</span><span class="sxs-lookup"><span data-stu-id="e85c7-117">IPv4</span></span>

<span data-ttu-id="e85c7-118">nome Hello di una zona di ricerca inversa IPv4 è basato sull'intervallo IP hello che rappresenta.</span><span class="sxs-lookup"><span data-stu-id="e85c7-118">hello name of an IPv4 reverse lookup zone is based on hello IP range it represents.</span></span> <span data-ttu-id="e85c7-119">Deve essere nel seguente formato hello: `<IPv4 network prefix in reverse order>.in-addr.arpa`.</span><span class="sxs-lookup"><span data-stu-id="e85c7-119">It should be in hello following format: `<IPv4 network prefix in reverse order>.in-addr.arpa`.</span></span> <span data-ttu-id="e85c7-120">Per esempi, vedere [Panoramica del DNS inverso e supporto in Azure](dns-reverse-dns-overview.md#ipv4).</span><span class="sxs-lookup"><span data-stu-id="e85c7-120">For examples, see [overview of reverse DNS and support in Azure](dns-reverse-dns-overview.md#ipv4).</span></span>

> [!NOTE]
> <span data-ttu-id="e85c7-121">Quando si crea una notazione classless zone di ricerca DNS inverse in DNS di Azure, è necessario usare un trattino (`-`) anziché una barra rovesciata ('/ ') nel nome della zona hello.</span><span class="sxs-lookup"><span data-stu-id="e85c7-121">When creating classless reverse DNS lookup zones in Azure DNS, you must use a hyphen (`-`) rather than a forward slash ('/') in hello zone name.</span></span>
>
> <span data-ttu-id="e85c7-122">Ad esempio, per hello IP intervallo 192.0.2.128/26, è necessario utilizzare `128-26.2.0.192.in-addr.arpa` come nome della zona hello anziché `128/26.2.0.192.in-addr.arpa`.</span><span class="sxs-lookup"><span data-stu-id="e85c7-122">For example, for hello IP range 192.0.2.128/26, you must use `128-26.2.0.192.in-addr.arpa` as hello zone name instead of `128/26.2.0.192.in-addr.arpa`.</span></span>
>
> <span data-ttu-id="e85c7-123">Questo avviene perché, anche se entrambi sono supportate dagli standard DNS hello, i nomi contenenti una barra rovesciata hello della zona DNS (`/`) in DNS di Azure non sono supportati i caratteri.</span><span class="sxs-lookup"><span data-stu-id="e85c7-123">This is because, while both are supported by hello DNS standards, DNS zone names containing hello forward slash (`/`) character are not supported in Azure DNS.</span></span>

<span data-ttu-id="e85c7-124">Hello esempio seguente viene illustrato come toocreate 'Classe C' inversa zona DNS denominato `2.0.192.in-addr.arpa` nel sistema DNS di Azure tramite hello portale di Azure:</span><span class="sxs-lookup"><span data-stu-id="e85c7-124">hello following example shows how toocreate a 'Class C' reverse DNS zone named `2.0.192.in-addr.arpa` in Azure DNS via hello Azure portal:</span></span>

 ![Creare una zona DNS](./media/dns-reverse-dns-hosting/figure2.png)

<span data-ttu-id="e85c7-126">Ciao 'Posizione gruppo di risorse' definisce hello posizione per il gruppo di risorse hello e non influisce sulla zona DNS hello.</span><span class="sxs-lookup"><span data-stu-id="e85c7-126">hello 'Resource group location' defines hello location for hello resource group, and has no impact on hello DNS zone.</span></span> <span data-ttu-id="e85c7-127">percorso di zona DNS Hello è sempre 'global' e non viene visualizzato.</span><span class="sxs-lookup"><span data-stu-id="e85c7-127">hello DNS zone location is always 'global', and is not shown.</span></span>

<span data-ttu-id="e85c7-128">Hello esempi seguenti viene illustrato come toocomplete questa attività con Azure PowerShell e hello CLI di Azure:</span><span class="sxs-lookup"><span data-stu-id="e85c7-128">hello following examples show how toocomplete this task with Azure PowerShell and hello Azure CLI:</span></span>

#### <a name="powershell"></a><span data-ttu-id="e85c7-129">PowerShell</span><span class="sxs-lookup"><span data-stu-id="e85c7-129">PowerShell</span></span>

```powershell
New-AzureRmDnsZone -Name 2.0.192.in-addr.arpa -ResourceGroupName MyResourceGroup
```

#### <a name="azure-cli-10"></a><span data-ttu-id="e85c7-130">Interfaccia della riga di comando di Azure 1.0</span><span class="sxs-lookup"><span data-stu-id="e85c7-130">Azure CLI 1.0</span></span>

```azurecli
azure network dns zone create MyResourceGroup 2.0.192.in-addr.arpa
```

#### <a name="azure-cli-20"></a><span data-ttu-id="e85c7-131">Interfaccia della riga di comando di Azure 2.0</span><span class="sxs-lookup"><span data-stu-id="e85c7-131">Azure CLI 2.0</span></span>

```azurecli
az network dns zone create -g MyResourceGroup -n 2.0.192.in-addr.arpa
```

### <a name="ipv6"></a><span data-ttu-id="e85c7-132">IPv6</span><span class="sxs-lookup"><span data-stu-id="e85c7-132">IPv6</span></span>

<span data-ttu-id="e85c7-133">nome Hello di una zona di ricerca inversa IPv6 deve essere nel seguente modulo hello: `<IPv6 network prefix in reverse order>.ip6.arpa`.</span><span class="sxs-lookup"><span data-stu-id="e85c7-133">hello name of an IPv6 reverse lookup zone should be in hello following form: `<IPv6 network prefix in reverse order>.ip6.arpa`.</span></span>  <span data-ttu-id="e85c7-134">Per esempi, vedere [Panoramica del DNS inverso e supporto in Azure](dns-reverse-dns-overview.md#ipv6).</span><span class="sxs-lookup"><span data-stu-id="e85c7-134">For examples, see [overview of reverse DNS and support in Azure](dns-reverse-dns-overview.md#ipv6).</span></span>


<span data-ttu-id="e85c7-135">Hello esempio seguente viene illustrato come toocreate una zona di ricerca DNS inversa IPv6 denominati `0.0.0.0.d.c.b.a.8.b.d.0.1.0.0.2.ip6.arpa` nel sistema DNS di Azure tramite hello portale di Azure:</span><span class="sxs-lookup"><span data-stu-id="e85c7-135">hello following example shows how toocreate an IPv6 reverse DNS lookup zone named `0.0.0.0.d.c.b.a.8.b.d.0.1.0.0.2.ip6.arpa` in Azure DNS via hello Azure portal:</span></span>

 ![Creare una zona DNS](./media/dns-reverse-dns-hosting/figure3.png)

<span data-ttu-id="e85c7-137">Ciao 'Posizione gruppo di risorse' definisce hello posizione per il gruppo di risorse hello e non influisce sulla zona DNS hello.</span><span class="sxs-lookup"><span data-stu-id="e85c7-137">hello 'Resource group location' defines hello location for hello resource group, and has no impact on hello DNS zone.</span></span> <span data-ttu-id="e85c7-138">percorso di zona DNS Hello è sempre 'global' e non viene visualizzato.</span><span class="sxs-lookup"><span data-stu-id="e85c7-138">hello DNS zone location is always 'global', and is not shown.</span></span>

<span data-ttu-id="e85c7-139">Hello esempi seguenti viene illustrato come toocomplete questa attività con Azure PowerShell e hello CLI di Azure:</span><span class="sxs-lookup"><span data-stu-id="e85c7-139">hello following examples show how toocomplete this task with Azure PowerShell and hello Azure CLI:</span></span>

#### <a name="powershell"></a><span data-ttu-id="e85c7-140">PowerShell</span><span class="sxs-lookup"><span data-stu-id="e85c7-140">PowerShell</span></span>

```powershell
New-AzureRmDnsZone -Name 0.0.0.0.d.c.b.a.8.b.d.0.1.0.0.2.ip6.arpa -ResourceGroupName MyResourceGroup
```

#### <a name="azurecli-10"></a><span data-ttu-id="e85c7-141">Interfaccia della riga di comando di Azure 1.0</span><span class="sxs-lookup"><span data-stu-id="e85c7-141">AzureCLI 1.0</span></span>

```azurecli
azure network dns zone create MyResourceGroup 0.0.0.0.d.c.b.a.8.b.d.0.1.0.0.2.ip6.arpa
```

#### <a name="azurecli-20"></a><span data-ttu-id="e85c7-142">Interfaccia della riga di comando di Azure 2.0</span><span class="sxs-lookup"><span data-stu-id="e85c7-142">AzureCLI 2.0</span></span>

```azurecli
az network dns zone create -g MyResourceGroup -n 0.0.0.0.d.c.b.a.8.b.d.0.1.0.0.2.ip6.arpa
```

## <a name="delegate-a-reverse-dns-lookup-zone"></a><span data-ttu-id="e85c7-143">Delegare una zona DNS di ricerca inversa</span><span class="sxs-lookup"><span data-stu-id="e85c7-143">Delegate a reverse DNS lookup zone</span></span>

<span data-ttu-id="e85c7-144">Dopo aver creato la zona di ricerca DNS inversa, è necessario verificare che tale zona hello viene delegata dalla zona padre hello.</span><span class="sxs-lookup"><span data-stu-id="e85c7-144">Having created your reverse DNS lookup zone, you must ensure that hello zone is delegated from hello parent zone.</span></span> <span data-ttu-id="e85c7-145">Delega DNS consente hello Nome risoluzione processo toofind hello Nome server DNS che ospitano la zona di ricerca DNS inversa.</span><span class="sxs-lookup"><span data-stu-id="e85c7-145">DNS delegation enables hello DNS name resolution process toofind hello name servers hosting your reverse DNS lookup zone.</span></span> <span data-ttu-id="e85c7-146">In questo modo tali nome server tooanswer inversa query DNS per gli indirizzi IP hello l'intervallo di indirizzi.</span><span class="sxs-lookup"><span data-stu-id="e85c7-146">This enables those name servers tooanswer DNS reverse queries for hello IP addresses in your address range.</span></span>

<span data-ttu-id="e85c7-147">Per le zone di ricerca diretta, il processo di hello di delega di una zona DNS è descritto nella sezione [delegare il tooAzure di dominio DNS](dns-delegate-domain-azure-dns.md).</span><span class="sxs-lookup"><span data-stu-id="e85c7-147">For forward lookup zones, hello process of delegating a DNS zone is described in [Delegate your domain tooAzure DNS](dns-delegate-domain-azure-dns.md).</span></span> <span data-ttu-id="e85c7-148">Delega di zone di ricerca inversa hello allo stesso modo.</span><span class="sxs-lookup"><span data-stu-id="e85c7-148">Delegation for reverse lookup zones works hello same way.</span></span> <span data-ttu-id="e85c7-149">Hello unica differenza è che è necessario che server dei nomi tooconfigure hello con hello ISP che ha fornito l'intervallo di IP, anziché il registrar.</span><span class="sxs-lookup"><span data-stu-id="e85c7-149">hello only difference is that you need tooconfigure hello name servers with hello ISP who provided your IP range, rather than your domain name registrar.</span></span>

## <a name="create-a-dns-ptr-record"></a><span data-ttu-id="e85c7-150">Creare un record PTR DNS</span><span class="sxs-lookup"><span data-stu-id="e85c7-150">Create a DNS PTR record</span></span>

### <a name="ipv4"></a><span data-ttu-id="e85c7-151">IPv4</span><span class="sxs-lookup"><span data-stu-id="e85c7-151">IPv4</span></span>

<span data-ttu-id="e85c7-152">Hello seguente esempio illustra hello processo di creazione di un record PTR in una zona DNS inversa in DNS di Azure.</span><span class="sxs-lookup"><span data-stu-id="e85c7-152">hello following example walks you through hello process of creating a PTR record in a reverse DNS zone in Azure DNS.</span></span> <span data-ttu-id="e85c7-153">Per altri tipi di record e i record esistenti toomodify, vedere [record DNS di gestire e set di record mediante il portale di Azure di hello](dns-operations-recordsets-portal.md).</span><span class="sxs-lookup"><span data-stu-id="e85c7-153">For other record types and toomodify existing records, see [Manage DNS records and record sets by using hello Azure portal](dns-operations-recordsets-portal.md).</span></span>

1.  <span data-ttu-id="e85c7-154">Nella parte superiore di hello di hello **zona DNS** pannello seleziona **+ registrare set** tooopen hello **aggiungere set di record** blade.</span><span class="sxs-lookup"><span data-stu-id="e85c7-154">At hello top of hello **DNS zone** blade, select **+ Record set** tooopen hello **Add record set** blade.</span></span>

 ![Zona DNS](./media/dns-reverse-dns-hosting/figure4.png)

1. <span data-ttu-id="e85c7-156">In hello **aggiungere set di record** blade.</span><span class="sxs-lookup"><span data-stu-id="e85c7-156">On hello **Add record set** blade.</span></span> 
1. <span data-ttu-id="e85c7-157">Selezionare **PTR** dal record hello "**tipo**" dal menu.</span><span class="sxs-lookup"><span data-stu-id="e85c7-157">Select **PTR** from hello record "**Type**" menu.</span></span>  
1. <span data-ttu-id="e85c7-158">Hello nome del set di record hello per un record PTR deve rest hello toobe di hello indirizzo IPv4 in ordine inverso.</span><span class="sxs-lookup"><span data-stu-id="e85c7-158">hello name of hello record set for a PTR record needs toobe hello rest of hello IPv4 address in reverse order.</span></span> <span data-ttu-id="e85c7-159">In questo esempio hello primi tre ottetti sono già popolati come parte del nome della zona hello (.2.0.192).</span><span class="sxs-lookup"><span data-stu-id="e85c7-159">In this example, hello first three octets are already populated as part of hello zone name (.2.0.192).</span></span> <span data-ttu-id="e85c7-160">Pertanto, solo hello ultimo ottetto viene fornito nel campo nome hello.</span><span class="sxs-lookup"><span data-stu-id="e85c7-160">Therefore, only hello last octet is supplied in hello name field.</span></span> <span data-ttu-id="e85c7-161">Ad esempio, è possibile assegnare il nome "**15**" a un set di record per una risorsa il cui indirizzo IP è 192.0.2.15.</span><span class="sxs-lookup"><span data-stu-id="e85c7-161">For example, you could name your record set "**15**" for a resource whose IP address is 192.0.2.15.</span></span>  
1. <span data-ttu-id="e85c7-162">In hello "**nome di dominio**" Immettere il nome di dominio completo hello (FQDN) della risorsa hello con IP hello.</span><span class="sxs-lookup"><span data-stu-id="e85c7-162">In hello "**Domain Name**" field, enter hello fully qualified domain name (FQDN) of hello resource using hello IP.</span></span>
1. <span data-ttu-id="e85c7-163">Selezionare **OK** nella parte inferiore di hello del record DNS di hello pannello toocreate hello.</span><span class="sxs-lookup"><span data-stu-id="e85c7-163">Select **OK** at hello bottom of hello blade toocreate hello DNS record.</span></span>

 ![Aggiungi set di record](./media/dns-reverse-dns-hosting/figure5.png)

<span data-ttu-id="e85c7-165">di seguito Hello sono esempi su come toocomplete questa attività con PowerShell e hello AzureCLI:</span><span class="sxs-lookup"><span data-stu-id="e85c7-165">hello following are examples on how toocomplete this task with PowerShell and hello AzureCLI:</span></span>

#### <a name="powershell"></a><span data-ttu-id="e85c7-166">PowerShell</span><span class="sxs-lookup"><span data-stu-id="e85c7-166">PowerShell</span></span>

```powershell
New-AzureRmDnsRecordSet -Name 15 -RecordType PTR -ZoneName 2.0.192.in-addr.arpa -ResourceGroupName MyResourceGroup -Ttl 3600 -DnsRecords (New-AzureRmDnsRecordConfig -Ptrdname "dc1.contoso.com")
```
#### <a name="azurecli-10"></a><span data-ttu-id="e85c7-167">Interfaccia della riga di comando di Azure 1.0</span><span class="sxs-lookup"><span data-stu-id="e85c7-167">AzureCLI 1.0</span></span>

```azurecli
azure network dns record-set add-record MyResourceGroup 2.0.192.in-addr.arpa 15 PTR --ptrdname dc1.contoso.com  
```

#### <a name="azurecli-20"></a><span data-ttu-id="e85c7-168">Interfaccia della riga di comando di Azure 2.0</span><span class="sxs-lookup"><span data-stu-id="e85c7-168">AzureCLI 2.0</span></span>

```azurecli
    az network dns record-set ptr add-record -g MyResourceGroup -z 2.0.192.in-addr.arpa -n 15 --ptrdname dc1.contoso.com
```

### <a name="ipv6"></a><span data-ttu-id="e85c7-169">IPv6</span><span class="sxs-lookup"><span data-stu-id="e85c7-169">IPv6</span></span>

<span data-ttu-id="e85c7-170">Hello di esempio seguente viene illustrato il processo di hello di creazione di nuovi record 'PTR'.</span><span class="sxs-lookup"><span data-stu-id="e85c7-170">hello following example walks you through hello process of creating new 'PTR' record.</span></span> <span data-ttu-id="e85c7-171">Per altri tipi di record e i record esistenti toomodify, vedere [record DNS di gestire e set di record mediante il portale di Azure di hello](dns-operations-recordsets-portal.md).</span><span class="sxs-lookup"><span data-stu-id="e85c7-171">For other record types and toomodify existing records, see [Manage DNS records and record sets by using hello Azure portal](dns-operations-recordsets-portal.md).</span></span>

1. <span data-ttu-id="e85c7-172">Nella parte superiore di hello di hello **blade di zona DNS**selezionare **+ registrare set** tooopen hello **aggiungere set di record** blade.</span><span class="sxs-lookup"><span data-stu-id="e85c7-172">At hello top of hello **DNS zone blade**, select **+ Record set** tooopen hello **Add record set** blade.</span></span>

  ![Pannello Zona DNS](./media/dns-reverse-dns-hosting/figure6.png)

2. <span data-ttu-id="e85c7-174">In hello **aggiungere set di record** blade.</span><span class="sxs-lookup"><span data-stu-id="e85c7-174">On hello **Add record set** blade.</span></span> 
3. <span data-ttu-id="e85c7-175">Selezionare **PTR** dal record hello "**tipo**" dal menu.</span><span class="sxs-lookup"><span data-stu-id="e85c7-175">Select **PTR** from hello record "**Type**" menu.</span></span>  
4. <span data-ttu-id="e85c7-176">Hello nome del set di record hello per un record PTR deve rest hello toobe di hello indirizzo IPv6 in ordine inverso.</span><span class="sxs-lookup"><span data-stu-id="e85c7-176">hello name of hello record set for a PTR record needs toobe hello rest of hello IPv6 address in reverse order.</span></span> <span data-ttu-id="e85c7-177">Non deve includere alcuna compressione degli zeri.</span><span class="sxs-lookup"><span data-stu-id="e85c7-177">It must not include any zero compression.</span></span> <span data-ttu-id="e85c7-178">In questo esempio hello primi 64 bit di hello IPv6 sono già popolati come parte del nome della zona hello (0.0.0.0.c.d.b.a.8.b.d.0.1.0.0.2.ip6.arpa).</span><span class="sxs-lookup"><span data-stu-id="e85c7-178">In this example, hello first 64 bits of hello IPv6 are already populated as part of hello zone name (0.0.0.0.c.d.b.a.8.b.d.0.1.0.0.2.ip6.arpa).</span></span> <span data-ttu-id="e85c7-179">Pertanto, solo hello ultimi 64 bit vengono specificati nel campo nome hello.</span><span class="sxs-lookup"><span data-stu-id="e85c7-179">Therefore, only hello last 64 bits are supplied in hello name field.</span></span> <span data-ttu-id="e85c7-180">ultimi 64 bit dell'indirizzo IP hello Hello vengono immessi in ordine inverso, utilizzando un punto come delimitatore di hello tra ogni numero esadecimale.</span><span class="sxs-lookup"><span data-stu-id="e85c7-180">hello last 64 bits of hello IP address are entered in reverse order, using a period as hello delimiter between each hexadecimal number.</span></span> <span data-ttu-id="e85c7-181">Ad esempio, è possibile specificare "**e.5.0.4.9.f.a.1.c.b.0.1.4.2.5.f**" come nome di un set di record per una risorsa il cui indirizzo IP è 2001:0db8:abdc:0000:f524:10bc:1af9:405e.</span><span class="sxs-lookup"><span data-stu-id="e85c7-181">For example, you could name your record set "**e.5.0.4.9.f.a.1.c.b.0.1.4.2.5.f**" for a resource whose IP address is 2001:0db8:abdc:0000:f524:10bc:1af9:405e.</span></span>  
5. <span data-ttu-id="e85c7-182">In hello "**nome di dominio**" Immettere il nome di dominio completo hello (FQDN) della risorsa hello con IP hello.</span><span class="sxs-lookup"><span data-stu-id="e85c7-182">In hello "**Domain Name**" field, enter hello fully qualified domain name (FQDN) of hello resource using hello IP.</span></span>
6. <span data-ttu-id="e85c7-183">Selezionare **OK** nella parte inferiore di hello del record DNS di hello pannello toocreate hello.</span><span class="sxs-lookup"><span data-stu-id="e85c7-183">Select **OK** at hello bottom of hello blade toocreate hello DNS record.</span></span>

![Pannello Aggiungi set di record](./media/dns-reverse-dns-hosting/figure7.png)

<span data-ttu-id="e85c7-185">di seguito Hello sono esempi su come toocomplete questa attività con PowerShell e hello AzureCLI:</span><span class="sxs-lookup"><span data-stu-id="e85c7-185">hello following are examples on how toocomplete this task with PowerShell and hello AzureCLI:</span></span>

#### <a name="powershell"></a><span data-ttu-id="e85c7-186">PowerShell</span><span class="sxs-lookup"><span data-stu-id="e85c7-186">PowerShell</span></span>

```powershell
New-AzureRmDnsRecordSet -Name "e.5.0.4.9.f.a.1.c.b.0.1.4.2.5.f" -RecordType PTR -ZoneName 0.0.0.0.c.d.b.a.8.b.d.0.1.0.0.2.ip6.arpa -ResourceGroupName MyResourceGroup -Ttl 3600 -DnsRecords (New-AzureRmDnsRecordConfig -Ptrdname "dc2.contoso.com")
```

#### <a name="azurecli-10"></a><span data-ttu-id="e85c7-187">Interfaccia della riga di comando di Azure 1.0</span><span class="sxs-lookup"><span data-stu-id="e85c7-187">AzureCLI 1.0</span></span>

```
azure network dns record-set add-record MyResourceGroup 0.0.0.0.c.d.b.a.8.b.d.0.1.0.0.2.ip6.arpa e.5.0.4.9.f.a.1.c.b.0.1.4.2.5.f PTR --ptrdname dc2.contoso.com 
```
 
#### <a name="azurecli-20"></a><span data-ttu-id="e85c7-188">Interfaccia della riga di comando di Azure 2.0</span><span class="sxs-lookup"><span data-stu-id="e85c7-188">AzureCLI 2.0</span></span>

```azurecli
    az network dns record-set ptr add-record -g MyResourceGroup -z 0.0.0.0.c.d.b.a.8.b.d.0.1.0.0.2.ip6.arpa -n e.5.0.4.9.f.a.1.c.b.0.1.4.2.5.f --ptrdname dc2.contoso.com
```

## <a name="view-records"></a><span data-ttu-id="e85c7-189">Visualizzare i record</span><span class="sxs-lookup"><span data-stu-id="e85c7-189">View Records</span></span>

<span data-ttu-id="e85c7-190">i record di hello tooview è stato creato, passare tooyour zona DNS in hello portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="e85c7-190">tooview hello records you created, navigate tooyour DNS zone in hello Azure portal.</span></span> <span data-ttu-id="e85c7-191">In hello inferiore parte di hello **zona DNS** pannello, è possibile visualizzare i record per la zona DNS hello hello.</span><span class="sxs-lookup"><span data-stu-id="e85c7-191">In hello lower part of hello **DNS zone** blade, you can see hello records for hello DNS zone.</span></span> <span data-ttu-id="e85c7-192">Dovrebbe essere hello NS e SOA record predefiniti, che vengono create in ogni area, oltre a qualsiasi nuovo record che è stato creato.</span><span class="sxs-lookup"><span data-stu-id="e85c7-192">You should see hello default NS and SOA records, which are created in every zone, plus any new records you have created.</span></span>

### <a name="ipv4"></a><span data-ttu-id="e85c7-193">IPv4</span><span class="sxs-lookup"><span data-stu-id="e85c7-193">IPv4</span></span>

<span data-ttu-id="e85c7-194">Pannello Zona DNS con i record PTR IPv4:</span><span class="sxs-lookup"><span data-stu-id="e85c7-194">DNS zone blade, showing IPv4 PTR records:</span></span>

![Pannello Zona DNS](./media/dns-reverse-dns-hosting/figure8.png)

<span data-ttu-id="e85c7-196">Hello negli esempi seguenti mostrano come tooview hello PTR registra l'utilizzo di PowerShell o hello CLI di Azure:</span><span class="sxs-lookup"><span data-stu-id="e85c7-196">hello following examples show how tooview hello PTR records using PowerShell or hello Azure CLI:</span></span>

#### <a name="powershell"></a><span data-ttu-id="e85c7-197">PowerShell</span><span class="sxs-lookup"><span data-stu-id="e85c7-197">PowerShell</span></span>

```powershell
Get-AzureRmDnsRecordSet -ZoneName 2.0.192.in-addr.arpa -ResourceGroupName MyResourceGroup
```

#### <a name="azure-cli-10"></a><span data-ttu-id="e85c7-198">Interfaccia della riga di comando di Azure 1.0</span><span class="sxs-lookup"><span data-stu-id="e85c7-198">Azure CLI 1.0</span></span>

```azurecli
    azure network dns record-set list MyResourceGroup 2.0.192.in-addr.arpa
```

#### <a name="azure-cli-20"></a><span data-ttu-id="e85c7-199">Interfaccia della riga di comando di Azure 2.0</span><span class="sxs-lookup"><span data-stu-id="e85c7-199">Azure CLI 2.0</span></span>

```azurecli
    azure network dns record-set list -g MyResourceGroup -z 2.0.192.in-addr.arpa
```

### <a name="ipv6"></a><span data-ttu-id="e85c7-200">IPv6</span><span class="sxs-lookup"><span data-stu-id="e85c7-200">IPv6</span></span>

<span data-ttu-id="e85c7-201">Pannello Zona DNS con i record PTR IPv6:</span><span class="sxs-lookup"><span data-stu-id="e85c7-201">DNS zone blade, showing IPv6 PTR records:</span></span>

![Pannello Zona DNS](./media/dns-reverse-dns-hosting/figure9.png)

<span data-ttu-id="e85c7-203">di seguito Hello sono esempi su come tooview hello registra con PowerShell e hello AzureCLI:</span><span class="sxs-lookup"><span data-stu-id="e85c7-203">hello following are examples on how tooview hello records with PowerShell and hello AzureCLI:</span></span>

#### <a name="powershell"></a><span data-ttu-id="e85c7-204">PowerShell</span><span class="sxs-lookup"><span data-stu-id="e85c7-204">PowerShell</span></span>

```powershell
Get-AzureRmDnsRecordSet -ZoneName 0.0.0.0.c.d.b.a.8.b.d.0.1.0.0.2.ip6.arpa -ResourceGroupName MyResourceGroup
```

#### <a name="azure-cli-10"></a><span data-ttu-id="e85c7-205">Interfaccia della riga di comando di Azure 1.0</span><span class="sxs-lookup"><span data-stu-id="e85c7-205">Azure CLI 1.0</span></span>

```azurecli
    azure network dns record-set list MyResourceGroup 0.0.0.0.c.d.b.a.8.b.d.0.1.0.0.2.ip6.arpa
```

#### <a name="azure-cli-20"></a><span data-ttu-id="e85c7-206">Interfaccia della riga di comando di Azure 2.0</span><span class="sxs-lookup"><span data-stu-id="e85c7-206">Azure CLI 2.0</span></span>

```azurecli
    azure network dns record-set list -g MyResourceGroup -z 0.0.0.0.c.d.b.a.8.b.d.0.1.0.0.2.ip6.arpa
```

## <a name="faq"></a><span data-ttu-id="e85c7-207">domande frequenti</span><span class="sxs-lookup"><span data-stu-id="e85c7-207">FAQ</span></span>

### <a name="can-i-host-reverse-dns-lookup-zones-for-my-isp-assigned-ip-blocks-on-azure-dns"></a><span data-ttu-id="e85c7-208">È possibile ospitare zone DNS di ricerca inversa per i blocchi di indirizzi IP assegnati dal provider di servizi Internet in DNS Azure?</span><span class="sxs-lookup"><span data-stu-id="e85c7-208">Can I host reverse DNS lookup zones for my ISP-assigned IP blocks on Azure DNS?</span></span>

<span data-ttu-id="e85c7-209">Sì.</span><span class="sxs-lookup"><span data-stu-id="e85c7-209">Yes.</span></span> <span data-ttu-id="e85c7-210">Hosting di zone di ricerca inversa (ARPA) hello per intervalli IP in DNS di Azure è completamente supportato.</span><span class="sxs-lookup"><span data-stu-id="e85c7-210">Hosting hello reverse lookup (ARPA) zones for your own IP ranges in Azure DNS is fully supported.</span></span>

<span data-ttu-id="e85c7-211">Creare la zona di ricerca inversa hello in DNS di Azure come descritto in questo articolo e quindi di usare con l'ISP troppo[delegato hello zona](dns-domain-delegation.md).</span><span class="sxs-lookup"><span data-stu-id="e85c7-211">Create hello reverse lookup zone in Azure DNS as explained in this article, then work with your ISP too[delegate hello zone](dns-domain-delegation.md).</span></span>  <span data-ttu-id="e85c7-212">È quindi possibile gestire i record PTR hello per ogni ricerca inversa in hello come altri tipi di record.</span><span class="sxs-lookup"><span data-stu-id="e85c7-212">You can then manage hello PTR records for each reverse lookup in hello same way as other record types.</span></span>

### <a name="how-much-does-hosting-my-reverse-dns-lookup-zone-cost"></a><span data-ttu-id="e85c7-213">Quanto costa l'hosting della zona DNS di ricerca inversa?</span><span class="sxs-lookup"><span data-stu-id="e85c7-213">How much does hosting my reverse DNS lookup zone cost?</span></span>

<span data-ttu-id="e85c7-214">Zona di ricerca DNS inversa hello di hosting per il blocco IP assegnato dal provider di servizi Internet in DNS di Azure viene addebitato ai [tariffe DNS di Azure standard](https://azure.microsoft.com/pricing/details/dns/).</span><span class="sxs-lookup"><span data-stu-id="e85c7-214">Hosting hello reverse DNS lookup zone for your ISP-assigned IP block in Azure DNS is charged at [standard Azure DNS rates](https://azure.microsoft.com/pricing/details/dns/).</span></span>

### <a name="can-i-host-reverse-dns-lookup-zones-for-both-ipv4-and-ipv6-addresses-in-azure-dns"></a><span data-ttu-id="e85c7-215">È possibile ospitare zone DNS di ricerca inversa per indirizzi IPv4 e IPv6 in DNS Azure?</span><span class="sxs-lookup"><span data-stu-id="e85c7-215">Can I host reverse DNS lookup zones for both IPv4 and IPv6 addresses in Azure DNS?</span></span>

<span data-ttu-id="e85c7-216">Sì.</span><span class="sxs-lookup"><span data-stu-id="e85c7-216">Yes.</span></span> <span data-ttu-id="e85c7-217">Questo articolo viene illustrato come toocreate sia IPv4 che IPv6 invertire le zone di ricerca DNS nel sistema DNS di Azure.</span><span class="sxs-lookup"><span data-stu-id="e85c7-217">This article explains how toocreate both IPv4 and IPv6 reverse DNS lookup zones in Azure DNS.</span></span>

### <a name="can-i-import-an-existing-reverse-dns-lookup-zone"></a><span data-ttu-id="e85c7-218">È possibile importare una zona DNS di ricerca inversa esistente?</span><span class="sxs-lookup"><span data-stu-id="e85c7-218">Can I import an existing reverse DNS lookup zone?</span></span>

<span data-ttu-id="e85c7-219">Sì.</span><span class="sxs-lookup"><span data-stu-id="e85c7-219">Yes.</span></span> <span data-ttu-id="e85c7-220">È possibile utilizzare hello Azure CLI tooimport esistente le zone DNS in DNS di Azure.</span><span class="sxs-lookup"><span data-stu-id="e85c7-220">You can use hello Azure CLI tooimport existing DNS zones into Azure DNS.</span></span> <span data-ttu-id="e85c7-221">Questo approccio è applicabile alle zone di ricerca diretta e alle zone DNS di ricerca inversa.</span><span class="sxs-lookup"><span data-stu-id="e85c7-221">This works for both forward lookup zones and reverse lookup zones.</span></span>

<span data-ttu-id="e85c7-222">Per ulteriori informazioni, vedere [importazione ed esportazione di un file di zona DNS mediante hello Azure CLI](dns-import-export.md).</span><span class="sxs-lookup"><span data-stu-id="e85c7-222">For more information, see [Import and export a DNS zone file using hello Azure CLI](dns-import-export.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="e85c7-223">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="e85c7-223">Next steps</span></span>

<span data-ttu-id="e85c7-224">Per altre informazioni sul DNS inverso, vedere [Risoluzione DNS inversa su Wikipedia](http://en.wikipedia.org/wiki/Reverse_DNS_lookup).</span><span class="sxs-lookup"><span data-stu-id="e85c7-224">For more information on reverse DNS, see [reverse DNS lookup on Wikipedia](http://en.wikipedia.org/wiki/Reverse_DNS_lookup).</span></span>
<br>
<span data-ttu-id="e85c7-225">Informazioni su come troppo[gestire record di ricerca inversa DNS per i servizi di Azure](dns-reverse-dns-for-azure-services.md).</span><span class="sxs-lookup"><span data-stu-id="e85c7-225">Learn how too[manage reverse DNS records for your Azure services](dns-reverse-dns-for-azure-services.md).</span></span>

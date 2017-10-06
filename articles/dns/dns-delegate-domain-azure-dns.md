---
title: aaaDelegate il tooAzure di dominio DNS | Documenti Microsoft
description: Comprendere come usare DNS di Azure e delega di dominio toochange denominati server tooprovide dominio ospita.
services: dns
documentationcenter: na
author: georgewallace
manager: timlt
ms.assetid: 257da6ec-d6e2-4b6f-ad76-ee2dde4efbcc
ms.service: dns
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 04/12/2017
ms.author: gwallace
ms.openlocfilehash: f780bdaa416150e5e3afe6c6845dc75ba54b6203
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="delegate-a-domain-tooazure-dns"></a><span data-ttu-id="97021-103">Delegato tooAzure un dominio DNS</span><span class="sxs-lookup"><span data-stu-id="97021-103">Delegate a domain tooAzure DNS</span></span>

<span data-ttu-id="97021-104">DNS di Azure consente una zona DNS toohost e gestire i record DNS hello per un dominio in Azure.</span><span class="sxs-lookup"><span data-stu-id="97021-104">Azure DNS allows you toohost a DNS zone and manage hello DNS records for a domain in Azure.</span></span> <span data-ttu-id="97021-105">Per le query DNS per tooreach un dominio DNS di Azure, il dominio hello deve toobe delegato tooAzure DNS del dominio padre hello.</span><span class="sxs-lookup"><span data-stu-id="97021-105">In order for DNS queries for a domain tooreach Azure DNS, hello domain has toobe delegated tooAzure DNS from hello parent domain.</span></span> <span data-ttu-id="97021-106">Tenere presente il DNS di Azure non è il registrar di dominio hello.</span><span class="sxs-lookup"><span data-stu-id="97021-106">Keep in mind Azure DNS is not hello domain registrar.</span></span> <span data-ttu-id="97021-107">Questo articolo viene illustrato come toodelegate il tooAzure di dominio DNS.</span><span class="sxs-lookup"><span data-stu-id="97021-107">This article explains how toodelegate your domain tooAzure DNS.</span></span>

<span data-ttu-id="97021-108">Per i domini acquistati presso un registrar, registrar offre hello opzione tooset questi record NS.</span><span class="sxs-lookup"><span data-stu-id="97021-108">For domains purchased from a registrar, your registrar offers hello option tooset up these NS records.</span></span> <span data-ttu-id="97021-109">Non si dispone tooown toocreate un dominio una zona DNS con lo stesso nome di dominio in DNS di Azure.</span><span class="sxs-lookup"><span data-stu-id="97021-109">You do not have tooown a domain toocreate a DNS zone with that domain name in Azure DNS.</span></span> <span data-ttu-id="97021-110">Tuttavia, è necessario tooown hello dominio tooset backup hello tooAzure di delega DNS presso il registrar hello.</span><span class="sxs-lookup"><span data-stu-id="97021-110">However, you do need tooown hello domain tooset up hello delegation tooAzure DNS with hello registrar.</span></span>

<span data-ttu-id="97021-111">Si supponga, ad esempio, si acquista il dominio di hello 'contoso.net' e crea una zona con il nome di hello 'contoso.net' in DNS di Azure.</span><span class="sxs-lookup"><span data-stu-id="97021-111">For example, suppose you purchase hello domain 'contoso.net' and create a zone with hello name 'contoso.net' in Azure DNS.</span></span> <span data-ttu-id="97021-112">Come proprietario del dominio hello hello registrar offre che Hello opzione tooconfigure hello indirizzi del server (ovvero, i record di hello NS) per il dominio.</span><span class="sxs-lookup"><span data-stu-id="97021-112">As hello owner of hello domain, your registrar offers you hello option tooconfigure hello name server addresses (that is, hello NS records) for your domain.</span></span> <span data-ttu-id="97021-113">registrar Hello archivia questi record NS nel dominio padre hello, in questo caso ".net".</span><span class="sxs-lookup"><span data-stu-id="97021-113">hello registrar stores these NS records in hello parent domain, in this case '.net'.</span></span> <span data-ttu-id="97021-114">I client in tutto il mondo hello possono quindi essere dominio diretto tooyour nella zona DNS di Azure durante il tentativo di record DNS tooresolve 'contoso.net'.</span><span class="sxs-lookup"><span data-stu-id="97021-114">Clients around hello world can then be directed tooyour domain in Azure DNS zone when trying tooresolve DNS records in 'contoso.net'.</span></span>

## <a name="create-a-dns-zone"></a><span data-ttu-id="97021-115">Creare una zona DNS</span><span class="sxs-lookup"><span data-stu-id="97021-115">Create a DNS zone</span></span>

1. <span data-ttu-id="97021-116">Accedi toohello portale di Azure</span><span class="sxs-lookup"><span data-stu-id="97021-116">Sign in toohello Azure portal</span></span>
1. <span data-ttu-id="97021-117">Nel menu Hub hello, fare clic su e fare clic su **nuovo > rete >** e quindi fare clic su **zona DNS** blade di zona DNS creare hello tooopen.</span><span class="sxs-lookup"><span data-stu-id="97021-117">On hello Hub menu, click and click **New > Networking >** and then click **DNS zone** tooopen hello Create DNS zone blade.</span></span>

    ![Zona DNS](./media/dns-domain-delegation/dns.png)

1. <span data-ttu-id="97021-119">In hello **zona DNS creare** pannello immettere i seguenti valori hello, quindi fare clic su **crea**:</span><span class="sxs-lookup"><span data-stu-id="97021-119">On hello **Create DNS zone** blade enter hello following values, then click **Create**:</span></span>

   | <span data-ttu-id="97021-120">**Impostazione**</span><span class="sxs-lookup"><span data-stu-id="97021-120">**Setting**</span></span> | <span data-ttu-id="97021-121">**Valore**</span><span class="sxs-lookup"><span data-stu-id="97021-121">**Value**</span></span> | <span data-ttu-id="97021-122">**Dettagli**</span><span class="sxs-lookup"><span data-stu-id="97021-122">**Details**</span></span> |
   |---|---|---|
   |<span data-ttu-id="97021-123">**Nome**</span><span class="sxs-lookup"><span data-stu-id="97021-123">**Name**</span></span>|<span data-ttu-id="97021-124">contoso.net</span><span class="sxs-lookup"><span data-stu-id="97021-124">contoso.net</span></span>|<span data-ttu-id="97021-125">nome Hello della zona DNS hello</span><span class="sxs-lookup"><span data-stu-id="97021-125">hello name of hello DNS zone</span></span>|
   |<span data-ttu-id="97021-126">**Sottoscrizione**</span><span class="sxs-lookup"><span data-stu-id="97021-126">**Subscription**</span></span>|<span data-ttu-id="97021-127">[Sottoscrizione]</span><span class="sxs-lookup"><span data-stu-id="97021-127">[Your subscription]</span></span>|<span data-ttu-id="97021-128">Selezionare un gateway applicazione di sottoscrizione toocreate hello in.</span><span class="sxs-lookup"><span data-stu-id="97021-128">Select a subscription toocreate hello application gateway in.</span></span>|
   |<span data-ttu-id="97021-129">**Gruppo di risorse**</span><span class="sxs-lookup"><span data-stu-id="97021-129">**Resource group**</span></span>|<span data-ttu-id="97021-130">**Crea nuovo:** contosoRG</span><span class="sxs-lookup"><span data-stu-id="97021-130">**Create new:** contosoRG</span></span>|<span data-ttu-id="97021-131">Creare un gruppo di risorse.</span><span class="sxs-lookup"><span data-stu-id="97021-131">Create a resource group.</span></span> <span data-ttu-id="97021-132">nome del gruppo di risorse Hello deve essere univoco all'interno di sottoscrizione hello selezionata.</span><span class="sxs-lookup"><span data-stu-id="97021-132">hello resource group name must be unique within hello subscription you selected.</span></span> <span data-ttu-id="97021-133">ulteriori informazioni sui gruppi di risorse, leggere hello toolearn [Gestione risorse](../azure-resource-manager/resource-group-overview.md?toc=%2fazure%2fdns%2ftoc.json#resource-groups) articolo introduttivo.</span><span class="sxs-lookup"><span data-stu-id="97021-133">toolearn more about resource groups, read hello [Resource Manager](../azure-resource-manager/resource-group-overview.md?toc=%2fazure%2fdns%2ftoc.json#resource-groups) overview article.</span></span>|
   |<span data-ttu-id="97021-134">**Posizione**</span><span class="sxs-lookup"><span data-stu-id="97021-134">**Location**</span></span>|<span data-ttu-id="97021-135">Stati Uniti occidentali</span><span class="sxs-lookup"><span data-stu-id="97021-135">West US</span></span>||

> [!NOTE]
> <span data-ttu-id="97021-136">gruppo di risorse Hello fa riferimento il percorso toohello hello del gruppo di risorse e non influisce sulla zona DNS hello.</span><span class="sxs-lookup"><span data-stu-id="97021-136">hello resource group refers toohello location of hello resource group, and has no impact on hello DNS zone.</span></span> <span data-ttu-id="97021-137">percorso di zona DNS Hello sono sempre "globale" e non viene visualizzato.</span><span class="sxs-lookup"><span data-stu-id="97021-137">hello DNS zone location is always "global", and is not shown.</span></span>

## <a name="retrieve-name-servers"></a><span data-ttu-id="97021-138">Recuperare i server dei nomi</span><span class="sxs-lookup"><span data-stu-id="97021-138">Retrieve name servers</span></span>

<span data-ttu-id="97021-139">Per poter delegare il tooAzure di zona DNS di DNS, è necessario innanzitutto tooknow hello server nomi per la zona attiva.</span><span class="sxs-lookup"><span data-stu-id="97021-139">Before you can delegate your DNS zone tooAzure DNS, you first need tooknow hello name server names for your zone.</span></span> <span data-ttu-id="97021-140">DNS Azure alloca i server dei nomi da un pool ogni volta che viene creata una zona.</span><span class="sxs-lookup"><span data-stu-id="97021-140">Azure DNS allocates name servers from a pool each time a zone is created.</span></span>

1. <span data-ttu-id="97021-141">Zona DNS hello creato, nel portale di Azure hello **Preferiti** riquadro, fare clic su **tutte le risorse**.</span><span class="sxs-lookup"><span data-stu-id="97021-141">With hello DNS zone created, in hello Azure portal **Favorites** pane, click **All resources**.</span></span> <span data-ttu-id="97021-142">Fare clic su hello **contoso.net** zona DNS in hello **tutte le risorse** blade.</span><span class="sxs-lookup"><span data-stu-id="97021-142">Click hello **contoso.net** DNS zone in hello **All resources** blade.</span></span> <span data-ttu-id="97021-143">Sottoscrizione hello selezionati sono già dispone di numerose risorse in essa contenuti, è possibile immettere **contoso.net** in hello filtro in base al nome...</span><span class="sxs-lookup"><span data-stu-id="97021-143">If hello subscription you selected already has several resources in it, you can enter **contoso.net** in hello Filter by name…</span></span> <span data-ttu-id="97021-144">gateway applicazione hello di accesso tooeasily di casella.</span><span class="sxs-lookup"><span data-stu-id="97021-144">box tooeasily access hello application gateway.</span></span> 

1. <span data-ttu-id="97021-145">Recuperare i server dei nomi hello dal pannello della zona DNS hello.</span><span class="sxs-lookup"><span data-stu-id="97021-145">Retrieve hello name servers from hello DNS zone blade.</span></span> <span data-ttu-id="97021-146">In questo esempio è stato assegnato zona hello 'contoso.net', server dei nomi ' ns1-01.azure-dns.com', 'ns2-01.azure-dns .net', ' ns3-01.azure-dns.org', e ' ns4-01.azure-dns.info':</span><span class="sxs-lookup"><span data-stu-id="97021-146">In this example, hello zone 'contoso.net' has been assigned name servers 'ns1-01.azure-dns.com', 'ns2-01.azure-dns.net', 'ns3-01.azure-dns.org', and 'ns4-01.azure-dns.info':</span></span>

 ![Dns-nameserver](./media/dns-domain-delegation/viewzonens500.png)

<span data-ttu-id="97021-148">DNS di Azure crea automaticamente i record NS autorevoli nella zona contenente hello server dei nomi assegnato.</span><span class="sxs-lookup"><span data-stu-id="97021-148">Azure DNS automatically creates authoritative NS records in your zone containing hello assigned name servers.</span></span>  <span data-ttu-id="97021-149">i nomi di server dei nomi hello toosee tramite Azure PowerShell o l'interfaccia CLI di Azure, è sufficiente tooretrieve questi record.</span><span class="sxs-lookup"><span data-stu-id="97021-149">toosee hello name server names via Azure PowerShell or Azure CLI, you simply need tooretrieve these records.</span></span>

<span data-ttu-id="97021-150">Hello negli esempi seguenti vengono forniscono anche passaggi hello server dei nomi hello tooretrieve per una zona DNS di Azure con PowerShell e CLI di Azure.</span><span class="sxs-lookup"><span data-stu-id="97021-150">hello following examples also provide hello steps tooretrieve hello name servers for a zone in Azure DNS with PowerShell and Azure CLI.</span></span>

### <a name="powershell"></a><span data-ttu-id="97021-151">PowerShell</span><span class="sxs-lookup"><span data-stu-id="97021-151">PowerShell</span></span>

```powershell
# hello record name "@" is used toorefer toorecords at hello top of hello zone.
$zone = Get-AzureRmDnsZone -Name contoso.net -ResourceGroupName contosoRG
Get-AzureRmDnsRecordSet -Name "@" -RecordType NS -Zone $zone
```

<span data-ttu-id="97021-152">Hello di esempio seguente è riportata la risposta hello.</span><span class="sxs-lookup"><span data-stu-id="97021-152">hello following example is hello response.</span></span>

```
Name              : @
ZoneName          : contoso.net
ResourceGroupName : contosorg
Ttl               : 172800
Etag              : 03bff8f1-9c60-4a9b-ad9d-ac97366ee4d5
RecordType        : NS
Records           : {ns1-07.azure-dns.com., ns2-07.azure-dns.net., ns3-07.azure-dns.org.,
                    ns4-07.azure-dns.info.}
Metadata          :
```

### <a name="azure-cli"></a><span data-ttu-id="97021-153">Interfaccia della riga di comando di Azure</span><span class="sxs-lookup"><span data-stu-id="97021-153">Azure CLI</span></span>

```azurecli
az network dns record-set show --resource-group contosoRG --zone-name contoso.net --type NS --name @
```

<span data-ttu-id="97021-154">Hello di esempio seguente è riportata la risposta hello.</span><span class="sxs-lookup"><span data-stu-id="97021-154">hello following example is hello response.</span></span>

```json
{
  "etag": "03bff8f1-9c60-4a9b-ad9d-ac97366ee4d5",
  "id": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/contosoRG/providers/Microsoft.Network/dnszones/contoso.net/NS/@",
  "metadata": null,
  "name": "@",
  "nsRecords": [
    {
      "nsdname": "ns1-07.azure-dns.com."
    },
    {
      "nsdname": "ns2-07.azure-dns.net."
    },
    {
      "nsdname": "ns3-07.azure-dns.org."
    },
    {
      "nsdname": "ns4-07.azure-dns.info."
    }
  ],
  "resourceGroup": "contosoRG",
  "ttl": 172800,
  "type": "Microsoft.Network/dnszones/NS"
}
```

## <a name="delegate-hello-domain"></a><span data-ttu-id="97021-155">Dominio hello delegato</span><span class="sxs-lookup"><span data-stu-id="97021-155">Delegate hello domain</span></span>

<span data-ttu-id="97021-156">Ora che è creare la zona DNS hello e si dispone di server dei nomi hello, dominio padre hello deve toobe aggiornato con i server dei nomi DNS di Azure hello.</span><span class="sxs-lookup"><span data-stu-id="97021-156">Now that hello DNS zone is created and you have hello name servers, hello parent domain needs toobe updated with hello Azure DNS name servers.</span></span> <span data-ttu-id="97021-157">Ogni registrar dispone di propri DNS management tools toochange hello record server dei nomi per un dominio.</span><span class="sxs-lookup"><span data-stu-id="97021-157">Each registrar has their own DNS management tools toochange hello name server records for a domain.</span></span> <span data-ttu-id="97021-158">Nella pagina di gestione DNS del registrar hello, modificare i record NS hello e sostituire i record NS hello con hello quelli creati DNS di Azure.</span><span class="sxs-lookup"><span data-stu-id="97021-158">In hello registrar's DNS management page, edit hello NS records and replace hello NS records with hello ones Azure DNS created.</span></span>

<span data-ttu-id="97021-159">Quando la delega tooAzure un dominio DNS, è necessario utilizzare nomi di server di nome hello forniti da DNS di Azure.</span><span class="sxs-lookup"><span data-stu-id="97021-159">When delegating a domain tooAzure DNS, you must use hello name server names provided by Azure DNS.</span></span> <span data-ttu-id="97021-160">È consigliabile toouse tutti i quattro nomi i nomi di server, indipendentemente dal nome hello del dominio.</span><span class="sxs-lookup"><span data-stu-id="97021-160">It is recommended toouse all four name server names, regardless of hello name of your domain.</span></span> <span data-ttu-id="97021-161">La delega di dominio non richiede hello Nome server name toouse hello nello stesso dominio del dominio principale.</span><span class="sxs-lookup"><span data-stu-id="97021-161">Domain delegation does not require hello name server name toouse hello same top-level domain as your domain.</span></span>

<span data-ttu-id="97021-162">È necessario utilizzare 'glue record' toopoint toohello DNS di Azure nome indirizzi IP del server, non dopo questi indirizzi IP potrebbero cambiare nelle future.</span><span class="sxs-lookup"><span data-stu-id="97021-162">You should not use 'glue records' toopoint toohello Azure DNS name server IP addresses, since these IP addresses may change in future.</span></span> <span data-ttu-id="97021-163">Le deleghe che usano nomi dei server dei nomi nella propria zona, definiti a volte "server dei nomi personali", non sono attualmente supportate in DNS di Azure.</span><span class="sxs-lookup"><span data-stu-id="97021-163">Delegations using name server names in your own zone, sometimes called 'vanity name servers', are not currently supported in Azure DNS.</span></span>

## <a name="verify-name-resolution-is-working"></a><span data-ttu-id="97021-164">Verificare che la risoluzione dei nomi funzioni</span><span class="sxs-lookup"><span data-stu-id="97021-164">Verify name resolution is working</span></span>

<span data-ttu-id="97021-165">Dopo aver completato la delega di hello, è possibile verificare che la risoluzione dei nomi funziona tramite uno strumento, ad esempio "nslookup" tooquery hello record SOA per la zona (che viene creata automaticamente anche quando si crea la zona hello).</span><span class="sxs-lookup"><span data-stu-id="97021-165">After completing hello delegation, you can verify that name resolution is working by using a tool such as 'nslookup' tooquery hello SOA record for your zone (which is also automatically created when hello zone is created).</span></span>

<span data-ttu-id="97021-166">È non dispone di server dei nomi DNS di Azure hello toospecify, se è stata impostata correttamente, hello normale DNS processo di risoluzione delega hello hello Nome server trovati automaticamente.</span><span class="sxs-lookup"><span data-stu-id="97021-166">You do not have toospecify hello Azure DNS name servers, if hello delegation has been set up correctly, hello normal DNS resolution process finds hello name servers automatically.</span></span>

```
nslookup -type=SOA contoso.com
```

<span data-ttu-id="97021-167">di seguito Hello è una risposta di esempio da hello precedente comando:</span><span class="sxs-lookup"><span data-stu-id="97021-167">hello following is an example response from hello preceding command:</span></span>

```
Server: ns1-04.azure-dns.com
Address: 208.76.47.4

contoso.com
primary name server = ns1-04.azure-dns.com
responsible mail addr = msnhst.microsoft.com
serial = 1
refresh = 900 (15 mins)
retry = 300 (5 mins)
expire = 604800 (7 days)
default TTL = 300 (5 mins)
```

## <a name="delegate-sub-domains-in-azure-dns"></a><span data-ttu-id="97021-168">Delegare sottodomini in DNS di Azure</span><span class="sxs-lookup"><span data-stu-id="97021-168">Delegate sub-domains in Azure DNS</span></span>

<span data-ttu-id="97021-169">Se si desidera tooset di una zona figlio separata, è possibile delegare un sottodominio nel sistema DNS di Azure.</span><span class="sxs-lookup"><span data-stu-id="97021-169">If you want tooset up a separate child zone, you can delegate a sub-domain in Azure DNS.</span></span> <span data-ttu-id="97021-170">Ad esempio, dopo aver creato una e delegato 'contoso.net' nel sistema DNS di Azure, si supponga che si desidera tooset di una zona figlio separata, 'partners.contoso.net'.</span><span class="sxs-lookup"><span data-stu-id="97021-170">For example, having set up and delegated 'contoso.net' in Azure DNS, suppose you would like tooset up a separate child zone, 'partners.contoso.net'.</span></span>

1. <span data-ttu-id="97021-171">Creare una zona figlio hello 'partners.contoso.net' nel sistema DNS di Azure.</span><span class="sxs-lookup"><span data-stu-id="97021-171">Create hello child zone 'partners.contoso.net' in Azure DNS.</span></span>
2. <span data-ttu-id="97021-172">Cercare hello autorevole i record NS hello figlio zona tooobtain hello Nome server ospita una zona figlio hello in DNS di Azure.</span><span class="sxs-lookup"><span data-stu-id="97021-172">Look up hello authoritative NS records in hello child zone tooobtain hello name servers hosting hello child zone in Azure DNS.</span></span>
3. <span data-ttu-id="97021-173">Delegare zona figlio hello configurando i record NS nella zona padre hello verso zona figlio toohello.</span><span class="sxs-lookup"><span data-stu-id="97021-173">Delegate hello child zone by configuring NS records in hello parent zone pointing toohello child zone.</span></span>

### <a name="create-a-dns-zone"></a><span data-ttu-id="97021-174">Creare una zona DNS</span><span class="sxs-lookup"><span data-stu-id="97021-174">Create a DNS zone</span></span>

1. <span data-ttu-id="97021-175">Accedi toohello portale di Azure</span><span class="sxs-lookup"><span data-stu-id="97021-175">Sign in toohello Azure portal</span></span>
1. <span data-ttu-id="97021-176">Nel menu Hub hello, fare clic su e fare clic su **nuovo > rete >** e quindi fare clic su **zona DNS** blade di zona DNS creare hello tooopen.</span><span class="sxs-lookup"><span data-stu-id="97021-176">On hello Hub menu, click and click **New > Networking >** and then click **DNS zone** tooopen hello Create DNS zone blade.</span></span>

    ![Zona DNS](./media/dns-domain-delegation/dns.png)

1. <span data-ttu-id="97021-178">In hello **zona DNS creare** pannello immettere i seguenti valori hello, quindi fare clic su **crea**:</span><span class="sxs-lookup"><span data-stu-id="97021-178">On hello **Create DNS zone** blade enter hello following values, then click **Create**:</span></span>

   | <span data-ttu-id="97021-179">**Impostazione**</span><span class="sxs-lookup"><span data-stu-id="97021-179">**Setting**</span></span> | <span data-ttu-id="97021-180">**Valore**</span><span class="sxs-lookup"><span data-stu-id="97021-180">**Value**</span></span> | <span data-ttu-id="97021-181">**Dettagli**</span><span class="sxs-lookup"><span data-stu-id="97021-181">**Details**</span></span> |
   |---|---|---|
   |<span data-ttu-id="97021-182">**Nome**</span><span class="sxs-lookup"><span data-stu-id="97021-182">**Name**</span></span>|<span data-ttu-id="97021-183">partners.contoso.net</span><span class="sxs-lookup"><span data-stu-id="97021-183">partners.contoso.net</span></span>|<span data-ttu-id="97021-184">nome Hello della zona DNS hello</span><span class="sxs-lookup"><span data-stu-id="97021-184">hello name of hello DNS zone</span></span>|
   |<span data-ttu-id="97021-185">**Sottoscrizione**</span><span class="sxs-lookup"><span data-stu-id="97021-185">**Subscription**</span></span>|<span data-ttu-id="97021-186">[Sottoscrizione]</span><span class="sxs-lookup"><span data-stu-id="97021-186">[Your subscription]</span></span>|<span data-ttu-id="97021-187">Selezionare un gateway applicazione di sottoscrizione toocreate hello in.</span><span class="sxs-lookup"><span data-stu-id="97021-187">Select a subscription toocreate hello application gateway in.</span></span>|
   |<span data-ttu-id="97021-188">**Gruppo di risorse**</span><span class="sxs-lookup"><span data-stu-id="97021-188">**Resource group**</span></span>|<span data-ttu-id="97021-189">**Utilizza esistente:** contosoRG</span><span class="sxs-lookup"><span data-stu-id="97021-189">**Use Existing:** contosoRG</span></span>|<span data-ttu-id="97021-190">Creare un gruppo di risorse.</span><span class="sxs-lookup"><span data-stu-id="97021-190">Create a resource group.</span></span> <span data-ttu-id="97021-191">nome del gruppo di risorse Hello deve essere univoco all'interno di sottoscrizione hello selezionata.</span><span class="sxs-lookup"><span data-stu-id="97021-191">hello resource group name must be unique within hello subscription you selected.</span></span> <span data-ttu-id="97021-192">ulteriori informazioni sui gruppi di risorse, leggere hello toolearn [Gestione risorse](../azure-resource-manager/resource-group-overview.md?toc=%2fazure%2fdns%2ftoc.json#resource-groups) articolo introduttivo.</span><span class="sxs-lookup"><span data-stu-id="97021-192">toolearn more about resource groups, read hello [Resource Manager](../azure-resource-manager/resource-group-overview.md?toc=%2fazure%2fdns%2ftoc.json#resource-groups) overview article.</span></span>|
   |<span data-ttu-id="97021-193">**Posizione**</span><span class="sxs-lookup"><span data-stu-id="97021-193">**Location**</span></span>|<span data-ttu-id="97021-194">Stati Uniti occidentali</span><span class="sxs-lookup"><span data-stu-id="97021-194">West US</span></span>||

> [!NOTE]
> <span data-ttu-id="97021-195">gruppo di risorse Hello fa riferimento il percorso toohello hello del gruppo di risorse e non influisce sulla zona DNS hello.</span><span class="sxs-lookup"><span data-stu-id="97021-195">hello resource group refers toohello location of hello resource group, and has no impact on hello DNS zone.</span></span> <span data-ttu-id="97021-196">percorso di zona DNS Hello sono sempre "globale" e non viene visualizzato.</span><span class="sxs-lookup"><span data-stu-id="97021-196">hello DNS zone location is always "global", and is not shown.</span></span>

### <a name="retrieve-name-servers"></a><span data-ttu-id="97021-197">Recuperare i server dei nomi</span><span class="sxs-lookup"><span data-stu-id="97021-197">Retrieve name servers</span></span>

1. <span data-ttu-id="97021-198">Zona DNS hello creato, nel portale di Azure hello **Preferiti** riquadro, fare clic su **tutte le risorse**.</span><span class="sxs-lookup"><span data-stu-id="97021-198">With hello DNS zone created, in hello Azure portal **Favorites** pane, click **All resources**.</span></span> <span data-ttu-id="97021-199">Fare clic su hello **partners.contoso.net** zona DNS in hello **tutte le risorse** blade.</span><span class="sxs-lookup"><span data-stu-id="97021-199">Click hello **partners.contoso.net** DNS zone in hello **All resources** blade.</span></span> <span data-ttu-id="97021-200">Sottoscrizione hello selezionati sono già dispone di numerose risorse in essa contenuti, è possibile immettere **partners.contoso.net** in hello filtro in base al nome...</span><span class="sxs-lookup"><span data-stu-id="97021-200">If hello subscription you selected already has several resources in it, you can enter **partners.contoso.net** in hello Filter by name…</span></span> <span data-ttu-id="97021-201">zona DNS hello accesso tooeasily casella.</span><span class="sxs-lookup"><span data-stu-id="97021-201">box tooeasily access hello DNS zone.</span></span>

1. <span data-ttu-id="97021-202">Recuperare i server dei nomi hello dal pannello della zona DNS hello.</span><span class="sxs-lookup"><span data-stu-id="97021-202">Retrieve hello name servers from hello DNS zone blade.</span></span> <span data-ttu-id="97021-203">In questo esempio è stato assegnato zona hello 'contoso.net', server dei nomi ' ns1-01.azure-dns.com', 'ns2-01.azure-dns .net', ' ns3-01.azure-dns.org', e ' ns4-01.azure-dns.info':</span><span class="sxs-lookup"><span data-stu-id="97021-203">In this example, hello zone 'contoso.net' has been assigned name servers 'ns1-01.azure-dns.com', 'ns2-01.azure-dns.net', 'ns3-01.azure-dns.org', and 'ns4-01.azure-dns.info':</span></span>

 ![Dns-nameserver](./media/dns-domain-delegation/viewzonens500.png)

<span data-ttu-id="97021-205">DNS di Azure crea automaticamente i record NS autorevoli nella zona contenente hello server dei nomi assegnato.</span><span class="sxs-lookup"><span data-stu-id="97021-205">Azure DNS automatically creates authoritative NS records in your zone containing hello assigned name servers.</span></span>  <span data-ttu-id="97021-206">i nomi di server dei nomi hello toosee tramite Azure PowerShell o l'interfaccia CLI di Azure, è sufficiente tooretrieve questi record.</span><span class="sxs-lookup"><span data-stu-id="97021-206">toosee hello name server names via Azure PowerShell or Azure CLI, you simply need tooretrieve these records.</span></span>

### <a name="create-name-server-record-in-parent-zone"></a><span data-ttu-id="97021-207">Creare un record del server dei nomi in una zona padre</span><span class="sxs-lookup"><span data-stu-id="97021-207">Create name server record in parent zone</span></span>

1. <span data-ttu-id="97021-208">Passare toohello **contoso.net** zona DNS in hello portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="97021-208">Navigate toohello **contoso.net** DNS zone in hello Azure portal.</span></span>
1. <span data-ttu-id="97021-209">Fare clic su **+ Set di record**.</span><span class="sxs-lookup"><span data-stu-id="97021-209">Click **+ Record set**</span></span>
1. <span data-ttu-id="97021-210">In hello **aggiungere set di record** pannello, immettere i seguenti valori hello, quindi fare clic su **OK**:</span><span class="sxs-lookup"><span data-stu-id="97021-210">On hello **Add record set** blade, enter hello following values, then click **OK**:</span></span>

   | <span data-ttu-id="97021-211">**Impostazione**</span><span class="sxs-lookup"><span data-stu-id="97021-211">**Setting**</span></span> | <span data-ttu-id="97021-212">**Valore**</span><span class="sxs-lookup"><span data-stu-id="97021-212">**Value**</span></span> | <span data-ttu-id="97021-213">**Dettagli**</span><span class="sxs-lookup"><span data-stu-id="97021-213">**Details**</span></span> |
   |---|---|---|
   |<span data-ttu-id="97021-214">**Nome**</span><span class="sxs-lookup"><span data-stu-id="97021-214">**Name**</span></span>|<span data-ttu-id="97021-215">partners</span><span class="sxs-lookup"><span data-stu-id="97021-215">partners</span></span>|<span data-ttu-id="97021-216">nome di Hello della zona DNS di hello figlio</span><span class="sxs-lookup"><span data-stu-id="97021-216">hello name of hello child DNS zone</span></span>|
   |<span data-ttu-id="97021-217">**Tipo**</span><span class="sxs-lookup"><span data-stu-id="97021-217">**Type**</span></span>|<span data-ttu-id="97021-218">NS</span><span class="sxs-lookup"><span data-stu-id="97021-218">NS</span></span>|<span data-ttu-id="97021-219">Usare NS per i record del server dei nomi.</span><span class="sxs-lookup"><span data-stu-id="97021-219">Use NS for name server records.</span></span>|
   |<span data-ttu-id="97021-220">**TTL**</span><span class="sxs-lookup"><span data-stu-id="97021-220">**TTL**</span></span>|<span data-ttu-id="97021-221">1</span><span class="sxs-lookup"><span data-stu-id="97021-221">1</span></span>|<span data-ttu-id="97021-222">Ora toolive.</span><span class="sxs-lookup"><span data-stu-id="97021-222">Time toolive.</span></span>|
   |<span data-ttu-id="97021-223">**Unità TTL**</span><span class="sxs-lookup"><span data-stu-id="97021-223">**TTL unit**</span></span>|<span data-ttu-id="97021-224">Ore</span><span class="sxs-lookup"><span data-stu-id="97021-224">Hours</span></span>|<span data-ttu-id="97021-225">Imposta toohours toolive unità di tempo</span><span class="sxs-lookup"><span data-stu-id="97021-225">sets time toolive unit toohours</span></span>|
   |<span data-ttu-id="97021-226">**SERVER DEI NOMI**</span><span class="sxs-lookup"><span data-stu-id="97021-226">**NAME SERVER**</span></span>|<span data-ttu-id="97021-227">{server dei nomi dalla zona partners.contoso.net}</span><span class="sxs-lookup"><span data-stu-id="97021-227">{name servers from partners.contoso.net zone}</span></span>|<span data-ttu-id="97021-228">Immettere tutti i 4 hello server dei nomi da partners.contoso.net zona.</span><span class="sxs-lookup"><span data-stu-id="97021-228">Enter all 4 of hello name servers from partners.contoso.net zone.</span></span> |

   ![Dns-nameserver](./media/dns-domain-delegation/partnerzone.png)


### <a name="delegating-sub-domains-in-azure-dns-with-other-tools"></a><span data-ttu-id="97021-230">Delega di sottodomini in DNS di Azure con altri strumenti</span><span class="sxs-lookup"><span data-stu-id="97021-230">Delegating sub-domains in Azure DNS with other tools</span></span>

<span data-ttu-id="97021-231">Hello seguito sono riportati alcuni passaggi hello toodelegate i sottodomini in DNS di Azure con PowerShell e CLI:</span><span class="sxs-lookup"><span data-stu-id="97021-231">hello following examples provide hello steps toodelegate sub-domains in Azure DNS with PowerShell and CLI:</span></span>

#### <a name="powershell"></a><span data-ttu-id="97021-232">PowerShell</span><span class="sxs-lookup"><span data-stu-id="97021-232">PowerShell</span></span>

<span data-ttu-id="97021-233">Hello esempio PowerShell seguente viene illustrato il funzionamento.</span><span class="sxs-lookup"><span data-stu-id="97021-233">hello following PowerShell example demonstrates how this works.</span></span> <span data-ttu-id="97021-234">Hello stessi passaggi possono essere eseguiti tramite hello portale di Azure o tramite hello multipiattaforma CLI di Azure.</span><span class="sxs-lookup"><span data-stu-id="97021-234">hello same steps can be executed via hello Azure portal, or via hello cross-platform Azure CLI.</span></span>

```powershell
# Create hello parent and child zones. These can be in same resource group or different resource groups as Azure DNS is a global service.
$parent = New-AzureRmDnsZone -Name contoso.net -ResourceGroupName contosoRG
$child = New-AzureRmDnsZone -Name partners.contoso.net -ResourceGroupName contosoRG

# Retrieve hello authoritative NS records from hello child zone as shown in hello next example. This contains hello name servers assigned toohello child zone.
$child_ns_recordset = Get-AzureRmDnsRecordSet -Zone $child -Name "@" -RecordType NS

# Create hello corresponding NS record set in hello parent zone toocomplete hello delegation. hello record set name in hello parent zone matches hello child zone name, in this case "partners".
$parent_ns_recordset = New-AzureRmDnsRecordSet -Zone $parent -Name "partners" -RecordType NS -Ttl 3600
$parent_ns_recordset.Records = $child_ns_recordset.Records
Set-AzureRmDnsRecordSet -RecordSet $parent_ns_recordset
```

<span data-ttu-id="97021-235">Utilizzare `nslookup` tooverify che tutto sia installato correttamente eseguendo la ricerca di record SOA di zona figlio hello hello.</span><span class="sxs-lookup"><span data-stu-id="97021-235">Use `nslookup` tooverify that everything is set up correctly by looking up hello SOA record of hello child zone.</span></span>

```
nslookup -type=SOA partners.contoso.com
```

```
Server: ns1-08.azure-dns.com
Address: 208.76.47.8

partners.contoso.com
    primary name server = ns1-08.azure-dns.com
    responsible mail addr = msnhst.microsoft.com
    serial = 1
    refresh = 900 (15 mins)
    retry = 300 (5 mins)
    expire = 604800 (7 days)
    default TTL = 300 (5 mins)
```

#### <a name="azure-cli"></a><span data-ttu-id="97021-236">Interfaccia della riga di comando di Azure</span><span class="sxs-lookup"><span data-stu-id="97021-236">Azure CLI</span></span>

```azurecli
#!/bin/bash

# Create hello parent and child zones. These can be in same resource group or different resource groups as Azure DNS is a global service.
az network dns zone create -g contosoRG -n contoso.net
az network dns zone create -g contosoRG -n partners.contoso.net
```

<span data-ttu-id="97021-237">Recuperare i server di nome hello per hello `partners.contoso.net` zona dall'output di hello.</span><span class="sxs-lookup"><span data-stu-id="97021-237">Retrieve hello name servers for hello `partners.contoso.net` zone from hello output.</span></span>

```
{
  "etag": "00000003-0000-0000-418f-250de2b2d201",
  "id": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/contosorg/providers/Microsoft.Network/dnszones/partners.contoso.net",
  "location": "global",
  "maxNumberOfRecordSets": 5000,
  "name": "partners.contoso.net",
  "nameServers": [
    "ns1-09.azure-dns.com.",
    "ns2-09.azure-dns.net.",
    "ns3-09.azure-dns.org.",
    "ns4-09.azure-dns.info."
  ],
  "numberOfRecordSets": 2,
  "resourceGroup": "contosorg",
  "tags": {},
  "type": "Microsoft.Network/dnszones"
}
```

<span data-ttu-id="97021-238">Creare set di record hello e i record NS per ogni server dei nomi.</span><span class="sxs-lookup"><span data-stu-id="97021-238">Create hello record set and NS records for each name server.</span></span>

```azurecli
#!/bin/bash

# Create hello record set
az network dns record-set ns create --resource-group contosorg --zone-name contoso.net --name partners

# Create a ns record for each name server.
az network dns record-set ns add-record --resource-group contosorg --zone-name contoso.net --record-set-name partners --nsdname ns1-09.azure-dns.com.
az network dns record-set ns add-record --resource-group contosorg --zone-name contoso.net --record-set-name partners --nsdname ns2-09.azure-dns.net.
az network dns record-set ns add-record --resource-group contosorg --zone-name contoso.net --record-set-name partners --nsdname ns3-09.azure-dns.org.
az network dns record-set ns add-record --resource-group contosorg --zone-name contoso.net --record-set-name partners --nsdname ns4-09.azure-dns.info.
```

## <a name="delete-all-resources"></a><span data-ttu-id="97021-239">Eliminare tutte le risorse</span><span class="sxs-lookup"><span data-stu-id="97021-239">Delete all resources</span></span>

<span data-ttu-id="97021-240">toodelete tutte le risorse create in questo articolo, hello completo alla procedura seguente:</span><span class="sxs-lookup"><span data-stu-id="97021-240">toodelete all resources created in this article, complete hello following steps:</span></span>

1. <span data-ttu-id="97021-241">Nel portale di Azure hello **Preferiti** riquadro, fare clic su **tutte le risorse**.</span><span class="sxs-lookup"><span data-stu-id="97021-241">In hello Azure portal **Favorites** pane, click **All resources**.</span></span> <span data-ttu-id="97021-242">Fare clic su hello **contosorg** gruppo di risorse in hello tutti pannello risorse.</span><span class="sxs-lookup"><span data-stu-id="97021-242">Click hello **contosorg** resource group in hello All resources blade.</span></span> <span data-ttu-id="97021-243">Sottoscrizione hello selezionati sono già dispone di numerose risorse in essa contenuti, è possibile immettere **contosorg** in hello **filtrare in base al nome...**</span><span class="sxs-lookup"><span data-stu-id="97021-243">If hello subscription you selected already has several resources in it, you can enter **contosorg** in hello **Filter by name…**</span></span> <span data-ttu-id="97021-244">gruppo di risorse hello accesso tooeasily casella.</span><span class="sxs-lookup"><span data-stu-id="97021-244">box tooeasily access hello resource group.</span></span>
1. <span data-ttu-id="97021-245">In hello **contosorg** pannello, fare clic su hello **eliminare** pulsante.</span><span class="sxs-lookup"><span data-stu-id="97021-245">In hello **contosorg** blade, click hello **Delete** button.</span></span>
1. <span data-ttu-id="97021-246">Hello portale richiede nome hello tootype di hello tooconfirm di gruppo di risorse che si desidera toodelete è.</span><span class="sxs-lookup"><span data-stu-id="97021-246">hello portal requires you tootype hello name of hello resource group tooconfirm that you want toodelete it.</span></span> <span data-ttu-id="97021-247">Tipo *contosorg* per nome gruppo di risorse hello, quindi fare clic su **eliminare**.</span><span class="sxs-lookup"><span data-stu-id="97021-247">Type *contosorg* for hello resource group name, then click **Delete**.</span></span> <span data-ttu-id="97021-248">Elimina un gruppo di risorse, tutte le risorse nel gruppo di risorse hello, pertanto sempre certi tooconfirm contenuto hello di un gruppo di risorse prima di eliminarlo.</span><span class="sxs-lookup"><span data-stu-id="97021-248">Deleting a resource group deletes all resources within hello resource group, so always be sure tooconfirm hello contents of a resource group before deleting it.</span></span> <span data-ttu-id="97021-249">portale Hello Elimina tutte le risorse contenute nel gruppo di risorse hello, quindi Elimina gruppo di risorse hello stesso.</span><span class="sxs-lookup"><span data-stu-id="97021-249">hello portal deletes all resources contained within hello resource group, then deletes hello resource group itself.</span></span> <span data-ttu-id="97021-250">Questo processo richiede alcuni minuti.</span><span class="sxs-lookup"><span data-stu-id="97021-250">This process takes several minutes.</span></span>

## <a name="next-steps"></a><span data-ttu-id="97021-251">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="97021-251">Next steps</span></span>

[<span data-ttu-id="97021-252">Gestire le zone DNS</span><span class="sxs-lookup"><span data-stu-id="97021-252">Manage DNS zones</span></span>](dns-operations-dnszones.md)

[<span data-ttu-id="97021-253">Gestire i record DNS</span><span class="sxs-lookup"><span data-stu-id="97021-253">Manage DNS records</span></span>](dns-operations-recordsets.md)

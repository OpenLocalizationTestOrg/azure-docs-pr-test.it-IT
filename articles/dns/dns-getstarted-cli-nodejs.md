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
# <a name="get-started-with-azure-dns-using-azure-cli-10"></a><span data-ttu-id="8746b-104">Introduzione a DNS Azure con l'interfaccia della riga di comando di Azure 1.0</span><span class="sxs-lookup"><span data-stu-id="8746b-104">Get started with Azure DNS using Azure CLI 1.0</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="8746b-105">Portale di Azure</span><span class="sxs-lookup"><span data-stu-id="8746b-105">Azure portal</span></span>](dns-getstarted-portal.md)
> * [<span data-ttu-id="8746b-106">PowerShell</span><span class="sxs-lookup"><span data-stu-id="8746b-106">PowerShell</span></span>](dns-getstarted-powershell.md)
> * [<span data-ttu-id="8746b-107">Interfaccia della riga di comando di Azure 1.0</span><span class="sxs-lookup"><span data-stu-id="8746b-107">Azure CLI 1.0</span></span>](dns-getstarted-cli-nodejs.md)
> * [<span data-ttu-id="8746b-108">Interfaccia della riga di comando di Azure 2.0</span><span class="sxs-lookup"><span data-stu-id="8746b-108">Azure CLI 2.0</span></span>](dns-getstarted-cli.md)

<span data-ttu-id="8746b-109">Questo articolo illustra hello passaggi toocreate la prima zona DNS e record utilizzando hello multipiattaforma CLI di Azure 1.0, disponibile per Windows, Mac e Linux.</span><span class="sxs-lookup"><span data-stu-id="8746b-109">This article walks you through hello steps toocreate your first DNS zone and record using hello cross-platform Azure CLI 1.0, which is available for Windows, Mac and Linux.</span></span> <span data-ttu-id="8746b-110">È anche possibile eseguire questi passaggi tramite il portale di Azure hello o Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="8746b-110">You can also perform these steps using hello Azure portal or Azure PowerShell.</span></span>

<span data-ttu-id="8746b-111">Una zona DNS è utilizzato toohost hello DNS record per un particolare dominio.</span><span class="sxs-lookup"><span data-stu-id="8746b-111">A DNS zone is used toohost hello DNS records for a particular domain.</span></span> <span data-ttu-id="8746b-112">toostart hosting del dominio DNS di Azure, è necessario toocreate una zona DNS per il nome di dominio.</span><span class="sxs-lookup"><span data-stu-id="8746b-112">toostart hosting your domain in Azure DNS, you need toocreate a DNS zone for that domain name.</span></span> <span data-ttu-id="8746b-113">Ogni record DNS per il dominio viene quindi creato all'interno di questa zona DNS.</span><span class="sxs-lookup"><span data-stu-id="8746b-113">Each DNS record for your domain is then created inside this DNS zone.</span></span> <span data-ttu-id="8746b-114">Infine, toopublish della zona DNS toohello Internet, server dei nomi tooconfigure hello è necessario per il dominio hello.</span><span class="sxs-lookup"><span data-stu-id="8746b-114">Finally, toopublish your DNS zone toohello Internet, you need tooconfigure hello name servers for hello domain.</span></span> <span data-ttu-id="8746b-115">Ogni passaggio è illustrato di seguito.</span><span class="sxs-lookup"><span data-stu-id="8746b-115">Each of these steps is described below.</span></span>

<span data-ttu-id="8746b-116">Queste istruzioni presuppongono aver già installato e connesso tooAzure CLI 1.0.</span><span class="sxs-lookup"><span data-stu-id="8746b-116">These instructions assume you have already installed and signed in tooAzure CLI 1.0.</span></span> <span data-ttu-id="8746b-117">Per ulteriori informazioni, vedere [come toomanage DNS zone mediante Azure CLI 1.0](dns-operations-dnszones-cli-nodejs.md).</span><span class="sxs-lookup"><span data-stu-id="8746b-117">For help, see [How toomanage DNS zones using Azure CLI 1.0](dns-operations-dnszones-cli-nodejs.md).</span></span>

## <a name="create-hello-resource-group"></a><span data-ttu-id="8746b-118">Creare il gruppo di risorse hello</span><span class="sxs-lookup"><span data-stu-id="8746b-118">Create hello resource group</span></span>

<span data-ttu-id="8746b-119">Prima di creare una zona DNS hello, un gruppo di risorse viene creato toocontain zona di DNS hello.</span><span class="sxs-lookup"><span data-stu-id="8746b-119">Before creating hello DNS zone, a resource group is created toocontain hello DNS Zone.</span></span> <span data-ttu-id="8746b-120">Hello seguito è riportato il comando hello.</span><span class="sxs-lookup"><span data-stu-id="8746b-120">hello following shows hello command.</span></span>

```azurecli
azure group create --name MyResourceGroup --location "West US"
```

## <a name="create-a-dns-zone"></a><span data-ttu-id="8746b-121">Creare una zona DNS</span><span class="sxs-lookup"><span data-stu-id="8746b-121">Create a DNS zone</span></span>

<span data-ttu-id="8746b-122">Una zona DNS viene creata utilizzando hello `azure network dns zone create` comando.</span><span class="sxs-lookup"><span data-stu-id="8746b-122">A DNS zone is created using hello `azure network dns zone create` command.</span></span> <span data-ttu-id="8746b-123">Guida di toosee per questo comando, digitare `azure network dns zone create -h`.</span><span class="sxs-lookup"><span data-stu-id="8746b-123">toosee help for this command, type `azure network dns zone create -h`.</span></span>

<span data-ttu-id="8746b-124">esempio Hello crea una zona DNS denominata *contoso.com* nel gruppo di risorse hello chiamato *MyResourceGroup*.</span><span class="sxs-lookup"><span data-stu-id="8746b-124">hello following example creates a DNS zone called *contoso.com* in hello resource group called *MyResourceGroup*.</span></span> <span data-ttu-id="8746b-125">Utilizzare l'esempio toocreate hello una zona DNS, sostituendo i valori hello per uso personale.</span><span class="sxs-lookup"><span data-stu-id="8746b-125">Use hello example toocreate a DNS zone, substituting hello values for your own.</span></span>

```azurecli
azure network dns zone create MyResourceGroup contoso.com
```


## <a name="create-a-dns-record"></a><span data-ttu-id="8746b-126">Creare un record DNS</span><span class="sxs-lookup"><span data-stu-id="8746b-126">Create a DNS record</span></span>

<span data-ttu-id="8746b-127">toocreate un record DNS, utilizzare hello `azure network dns record-set add-record` comando.</span><span class="sxs-lookup"><span data-stu-id="8746b-127">toocreate a DNS record, use hello `azure network dns record-set add-record` command.</span></span> <span data-ttu-id="8746b-128">Per altre informazioni, vedere `azure network dns record-set add-record -h`.</span><span class="sxs-lookup"><span data-stu-id="8746b-128">For help, see `azure network dns record-set add-record -h`.</span></span>

<span data-ttu-id="8746b-129">Hello seguente viene creato un record con il nome relativo hello "www" hello "contoso.com", nel gruppo di risorse "MyResourceGroup" zona di DNS.</span><span class="sxs-lookup"><span data-stu-id="8746b-129">hello following example creates a record with hello relative name "www" in hello DNS Zone "contoso.com", in resource group "MyResourceGroup".</span></span> <span data-ttu-id="8746b-130">nome completo di Hello del set di record hello è "www.contoso.com".</span><span class="sxs-lookup"><span data-stu-id="8746b-130">hello fully-qualified name of hello record set is "www.contoso.com".</span></span> <span data-ttu-id="8746b-131">tipo di record Hello è "A", con l'indirizzo IP "1.2.3.4" e viene utilizzato un periodo TTL predefinito di 3600 secondi (1 ora).</span><span class="sxs-lookup"><span data-stu-id="8746b-131">hello record type is "A", with IP address "1.2.3.4", and a default TTL of 3600 seconds (1 hour) is used.</span></span>

```azurecli
azure network dns record-set add-record MyResourceGroup contoso.com www A -a 1.2.3.4
```

<span data-ttu-id="8746b-132">Per altri tipi di record, per i set di record con più di un record, per i valori di durata (TTL) alternativi e toomodify i record esistenti, vedere [record DNS di gestire e set di record mediante hello Azure CLI 1.0](dns-operations-recordsets-cli-nodejs.md).</span><span class="sxs-lookup"><span data-stu-id="8746b-132">For other record types, for record sets with more than one record, for alternative TTL values, and toomodify existing records, see [Manage DNS records and record sets using hello Azure CLI 1.0](dns-operations-recordsets-cli-nodejs.md).</span></span>


## <a name="view-records"></a><span data-ttu-id="8746b-133">Visualizzare i record</span><span class="sxs-lookup"><span data-stu-id="8746b-133">View records</span></span>

<span data-ttu-id="8746b-134">i record DNS di hello toolist nella zona, utilizzare:</span><span class="sxs-lookup"><span data-stu-id="8746b-134">toolist hello DNS records in your zone, use:</span></span>

```azurecli
azure network dns record-set list MyResourceGroup contoso.com
```


## <a name="update-name-servers"></a><span data-ttu-id="8746b-135">Aggiornare i server dei nomi</span><span class="sxs-lookup"><span data-stu-id="8746b-135">Update name servers</span></span>

<span data-ttu-id="8746b-136">Dopo aver soddisfatto che la zona DNS e i record sono stati impostati correttamente, è necessario tooconfigure il nome di dominio toouse server dei nomi DNS di Azure hello.</span><span class="sxs-lookup"><span data-stu-id="8746b-136">Once you are satisfied that your DNS zone and records have been set up correctly, you need tooconfigure your domain name toouse hello Azure DNS name servers.</span></span> <span data-ttu-id="8746b-137">In questo modo altri utenti nel hello Internet toofind i record DNS.</span><span class="sxs-lookup"><span data-stu-id="8746b-137">This enables other users on hello Internet toofind your DNS records.</span></span>

<span data-ttu-id="8746b-138">Server dei nomi per l'area Hello forniti tramite hello `azure network dns zone show` comando:</span><span class="sxs-lookup"><span data-stu-id="8746b-138">hello name servers for your zone are given by hello `azure network dns zone show` command:</span></span>

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

<span data-ttu-id="8746b-139">Questi server dei nomi deve essere configurato con hello registrar (in cui è stato acquistato il nome di dominio hello).</span><span class="sxs-lookup"><span data-stu-id="8746b-139">These name servers should be configured with hello domain name registrar (where you purchased hello domain name).</span></span> <span data-ttu-id="8746b-140">Registrar offrirà hello opzione tooset dei server dei nomi per il dominio hello hello.</span><span class="sxs-lookup"><span data-stu-id="8746b-140">Your registrar will offer hello option tooset up hello name servers for hello domain.</span></span> <span data-ttu-id="8746b-141">Per ulteriori informazioni, vedere [delegare il tooAzure di dominio DNS](dns-domain-delegation.md).</span><span class="sxs-lookup"><span data-stu-id="8746b-141">For more information, see [Delegate your domain tooAzure DNS](dns-domain-delegation.md).</span></span>

## <a name="delete-all-resources"></a><span data-ttu-id="8746b-142">Eliminare tutte le risorse</span><span class="sxs-lookup"><span data-stu-id="8746b-142">Delete all resources</span></span>
 
<span data-ttu-id="8746b-143">toodelete tutte le risorse create in questo articolo, hello take seguente passaggio:</span><span class="sxs-lookup"><span data-stu-id="8746b-143">toodelete all resources created in this article, take hello following step:</span></span>

```azurecli
azure group delete --name MyResourceGroup
```

## <a name="next-steps"></a><span data-ttu-id="8746b-144">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="8746b-144">Next steps</span></span>

<span data-ttu-id="8746b-145">toolearn ulteriori informazioni su DNS di Azure, vedere [Panoramica di DNS di Azure](dns-overview.md).</span><span class="sxs-lookup"><span data-stu-id="8746b-145">toolearn more about Azure DNS, see [Azure DNS overview](dns-overview.md).</span></span>

<span data-ttu-id="8746b-146">toolearn informazioni su gestione delle zone DNS di DNS di Azure, vedere [le zone DNS di gestione in DNS di Azure mediante Azure CLI 1.0](dns-operations-dnszones-cli-nodejs.md).</span><span class="sxs-lookup"><span data-stu-id="8746b-146">toolearn more about managing DNS zones in Azure DNS, see [Manage DNS zones in Azure DNS using Azure CLI 1.0](dns-operations-dnszones-cli-nodejs.md).</span></span>

<span data-ttu-id="8746b-147">toolearn informazioni su gestione dei record DNS nel sistema DNS di Azure, vedere [Manage DNS record e record imposta nel sistema DNS di Azure mediante Azure CLI 1.0](dns-operations-recordsets-cli-nodejs.md).</span><span class="sxs-lookup"><span data-stu-id="8746b-147">toolearn more about managing DNS records in Azure DNS, see [Manage DNS records and record sets in Azure DNS using Azure CLI 1.0](dns-operations-recordsets-cli-nodejs.md).</span></span>


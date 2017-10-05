---
title: Introduzione a DNS Azure con l'interfaccia della riga di comando di Azure 1.0 | Microsoft Docs
description: Informazioni su come creare una zona e un record DNS in DNS Azure. Si tratta di una guida dettagliata per creare e gestire la prima zona e il primo record DNS usando l'interfaccia della riga di comando di Azure 1.0.
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
ms.openlocfilehash: f7943b71bbd16c36df09436973d92539eb62b210
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="get-started-with-azure-dns-using-azure-cli-10"></a><span data-ttu-id="f34ac-104">Introduzione a DNS Azure con l'interfaccia della riga di comando di Azure 1.0</span><span class="sxs-lookup"><span data-stu-id="f34ac-104">Get started with Azure DNS using Azure CLI 1.0</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="f34ac-105">Portale di Azure</span><span class="sxs-lookup"><span data-stu-id="f34ac-105">Azure portal</span></span>](dns-getstarted-portal.md)
> * [<span data-ttu-id="f34ac-106">PowerShell</span><span class="sxs-lookup"><span data-stu-id="f34ac-106">PowerShell</span></span>](dns-getstarted-powershell.md)
> * [<span data-ttu-id="f34ac-107">Interfaccia della riga di comando di Azure 1.0</span><span class="sxs-lookup"><span data-stu-id="f34ac-107">Azure CLI 1.0</span></span>](dns-getstarted-cli-nodejs.md)
> * [<span data-ttu-id="f34ac-108">Interfaccia della riga di comando di Azure 2.0</span><span class="sxs-lookup"><span data-stu-id="f34ac-108">Azure CLI 2.0</span></span>](dns-getstarted-cli.md)

<span data-ttu-id="f34ac-109">Questo articolo illustra i passaggi per creare la prima zona e il primo record DNS usando l'interfaccia della riga di comando di Azure 1.0 tra piattaforme, disponibile per Windows, Mac e Linux.</span><span class="sxs-lookup"><span data-stu-id="f34ac-109">This article walks you through the steps to create your first DNS zone and record using the cross-platform Azure CLI 1.0, which is available for Windows, Mac and Linux.</span></span> <span data-ttu-id="f34ac-110">È anche possibile eseguire questi passaggi tramite il portale di Azure o Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="f34ac-110">You can also perform these steps using the Azure portal or Azure PowerShell.</span></span>

<span data-ttu-id="f34ac-111">Una zona DNS viene usata per ospitare i record DNS per un particolare dominio.</span><span class="sxs-lookup"><span data-stu-id="f34ac-111">A DNS zone is used to host the DNS records for a particular domain.</span></span> <span data-ttu-id="f34ac-112">Per iniziare a ospitare il dominio in DNS di Azure, è necessario creare una zona DNS per il nome di dominio.</span><span class="sxs-lookup"><span data-stu-id="f34ac-112">To start hosting your domain in Azure DNS, you need to create a DNS zone for that domain name.</span></span> <span data-ttu-id="f34ac-113">Ogni record DNS per il dominio viene quindi creato all'interno di questa zona DNS.</span><span class="sxs-lookup"><span data-stu-id="f34ac-113">Each DNS record for your domain is then created inside this DNS zone.</span></span> <span data-ttu-id="f34ac-114">Per pubblicare infine la zona DNS su Internet, è necessario configurare i server dei nomi per il dominio.</span><span class="sxs-lookup"><span data-stu-id="f34ac-114">Finally, to publish your DNS zone to the Internet, you need to configure the name servers for the domain.</span></span> <span data-ttu-id="f34ac-115">Ogni passaggio è illustrato di seguito.</span><span class="sxs-lookup"><span data-stu-id="f34ac-115">Each of these steps is described below.</span></span>

<span data-ttu-id="f34ac-116">Queste istruzioni presuppongono che l'interfaccia della riga di comando di Azure 1.0 sia già stata installata e che sia già stato eseguito l'accesso.</span><span class="sxs-lookup"><span data-stu-id="f34ac-116">These instructions assume you have already installed and signed in to Azure CLI 1.0.</span></span> <span data-ttu-id="f34ac-117">Per informazioni, vedere [Come gestire le zone DNS usando l'interfaccia della riga di comando di Azure 1.0](dns-operations-dnszones-cli-nodejs.md).</span><span class="sxs-lookup"><span data-stu-id="f34ac-117">For help, see [How to manage DNS zones using Azure CLI 1.0](dns-operations-dnszones-cli-nodejs.md).</span></span>

## <a name="create-the-resource-group"></a><span data-ttu-id="f34ac-118">Creare il gruppo di risorse.</span><span class="sxs-lookup"><span data-stu-id="f34ac-118">Create the resource group</span></span>

<span data-ttu-id="f34ac-119">Prima di creare la zona DNS, viene creato un gruppo di risorse per contenere la zona DNS.</span><span class="sxs-lookup"><span data-stu-id="f34ac-119">Before creating the DNS zone, a resource group is created to contain the DNS Zone.</span></span> <span data-ttu-id="f34ac-120">Di seguito è riportato il comando.</span><span class="sxs-lookup"><span data-stu-id="f34ac-120">The following shows the command.</span></span>

```azurecli
azure group create --name MyResourceGroup --location "West US"
```

## <a name="create-a-dns-zone"></a><span data-ttu-id="f34ac-121">Creare una zona DNS</span><span class="sxs-lookup"><span data-stu-id="f34ac-121">Create a DNS zone</span></span>

<span data-ttu-id="f34ac-122">Una zona DNS viene creata utilizzando il comando `azure network dns zone create` .</span><span class="sxs-lookup"><span data-stu-id="f34ac-122">A DNS zone is created using the `azure network dns zone create` command.</span></span> <span data-ttu-id="f34ac-123">Per visualizzare la guida per questo comando, digitare `azure network dns zone create -h`.</span><span class="sxs-lookup"><span data-stu-id="f34ac-123">To see help for this command, type `azure network dns zone create -h`.</span></span>

<span data-ttu-id="f34ac-124">L'esempio seguente crea una zona DNS denominata *contoso.com* nel gruppo di risorse denominato *MyResourceGroup*.</span><span class="sxs-lookup"><span data-stu-id="f34ac-124">The following example creates a DNS zone called *contoso.com* in the resource group called *MyResourceGroup*.</span></span> <span data-ttu-id="f34ac-125">Usare l'esempio per creare una zona DNS, sostituendo i valori con quelli personalizzati.</span><span class="sxs-lookup"><span data-stu-id="f34ac-125">Use the example to create a DNS zone, substituting the values for your own.</span></span>

```azurecli
azure network dns zone create MyResourceGroup contoso.com
```


## <a name="create-a-dns-record"></a><span data-ttu-id="f34ac-126">Creare un record DNS</span><span class="sxs-lookup"><span data-stu-id="f34ac-126">Create a DNS record</span></span>

<span data-ttu-id="f34ac-127">Per creare un record DNS, usare il comando `azure network dns record-set add-record`.</span><span class="sxs-lookup"><span data-stu-id="f34ac-127">To create a DNS record, use the `azure network dns record-set add-record` command.</span></span> <span data-ttu-id="f34ac-128">Per altre informazioni, vedere `azure network dns record-set add-record -h`.</span><span class="sxs-lookup"><span data-stu-id="f34ac-128">For help, see `azure network dns record-set add-record -h`.</span></span>

<span data-ttu-id="f34ac-129">L'esempio seguente crea un record con il nome relativo "www" nella zona DNS "contoso.com" nel gruppo di risorse "MyResourceGroup".</span><span class="sxs-lookup"><span data-stu-id="f34ac-129">The following example creates a record with the relative name "www" in the DNS Zone "contoso.com", in resource group "MyResourceGroup".</span></span> <span data-ttu-id="f34ac-130">Il nome completo del set di record sarà "www.contoso.com".</span><span class="sxs-lookup"><span data-stu-id="f34ac-130">The fully-qualified name of the record set is "www.contoso.com".</span></span> <span data-ttu-id="f34ac-131">Il tipo di record è "A" con indirizzo IP "1.2.3.4" e viene usato un valore TTL predefinito di 3600 secondi (1 ora).</span><span class="sxs-lookup"><span data-stu-id="f34ac-131">The record type is "A", with IP address "1.2.3.4", and a default TTL of 3600 seconds (1 hour) is used.</span></span>

```azurecli
azure network dns record-set add-record MyResourceGroup contoso.com www A -a 1.2.3.4
```

<span data-ttu-id="f34ac-132">Per altri tipi di record, per set di record con più di un record, per valori TTL alternativi e per modificare i record esistenti, vedere [Gestire record e set di record DNS con l'interfaccia della riga di comando di Azure 1.0](dns-operations-recordsets-cli-nodejs.md).</span><span class="sxs-lookup"><span data-stu-id="f34ac-132">For other record types, for record sets with more than one record, for alternative TTL values, and to modify existing records, see [Manage DNS records and record sets using the Azure CLI 1.0](dns-operations-recordsets-cli-nodejs.md).</span></span>


## <a name="view-records"></a><span data-ttu-id="f34ac-133">Visualizzare i record</span><span class="sxs-lookup"><span data-stu-id="f34ac-133">View records</span></span>

<span data-ttu-id="f34ac-134">Per elencare i record DNS nella zona, usare:</span><span class="sxs-lookup"><span data-stu-id="f34ac-134">To list the DNS records in your zone, use:</span></span>

```azurecli
azure network dns record-set list MyResourceGroup contoso.com
```


## <a name="update-name-servers"></a><span data-ttu-id="f34ac-135">Aggiornare i server dei nomi</span><span class="sxs-lookup"><span data-stu-id="f34ac-135">Update name servers</span></span>

<span data-ttu-id="f34ac-136">Dopo essersi assicurati che la zona e i record DNS siano stati configurati correttamente, è necessario configurare il nome di dominio in modo che usi i server dei nomi di DNS Azure.</span><span class="sxs-lookup"><span data-stu-id="f34ac-136">Once you are satisfied that your DNS zone and records have been set up correctly, you need to configure your domain name to use the Azure DNS name servers.</span></span> <span data-ttu-id="f34ac-137">Ciò consente agli altri utenti su Internet di trovare i record DNS.</span><span class="sxs-lookup"><span data-stu-id="f34ac-137">This enables other users on the Internet to find your DNS records.</span></span>

<span data-ttu-id="f34ac-138">I server dei nomi per la zona vengono specificati tramite il comando `azure network dns zone show`:</span><span class="sxs-lookup"><span data-stu-id="f34ac-138">The name servers for your zone are given by the `azure network dns zone show` command:</span></span>

```azurecli
azure network dns zone show MyResourceGroup contoso.com

info:    Executing command network dns zone show
+ Looking up the dns zone "contoso.com"
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

<span data-ttu-id="f34ac-139">I server dei nomi devono essere configurati con il registrar dei nomi di dominio, in cui è stato acquistato il nome di dominio.</span><span class="sxs-lookup"><span data-stu-id="f34ac-139">These name servers should be configured with the domain name registrar (where you purchased the domain name).</span></span> <span data-ttu-id="f34ac-140">Il registrar offrirà l'opzione per la configurazione dei server dei nomi per il dominio.</span><span class="sxs-lookup"><span data-stu-id="f34ac-140">Your registrar will offer the option to set up the name servers for the domain.</span></span> <span data-ttu-id="f34ac-141">Per altre informazioni, vedere [Delegare un dominio al servizio DNS Azure](dns-domain-delegation.md).</span><span class="sxs-lookup"><span data-stu-id="f34ac-141">For more information, see [Delegate your domain to Azure DNS](dns-domain-delegation.md).</span></span>

## <a name="delete-all-resources"></a><span data-ttu-id="f34ac-142">Eliminare tutte le risorse</span><span class="sxs-lookup"><span data-stu-id="f34ac-142">Delete all resources</span></span>
 
<span data-ttu-id="f34ac-143">Per eliminare tutte le risorse create in questo articolo, seguire questa procedura:</span><span class="sxs-lookup"><span data-stu-id="f34ac-143">To delete all resources created in this article, take the following step:</span></span>

```azurecli
azure group delete --name MyResourceGroup
```

## <a name="next-steps"></a><span data-ttu-id="f34ac-144">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="f34ac-144">Next steps</span></span>

<span data-ttu-id="f34ac-145">Per altre informazioni sul servizio DNS Azure, vedere [Panoramica di DNS Azure](dns-overview.md).</span><span class="sxs-lookup"><span data-stu-id="f34ac-145">To learn more about Azure DNS, see [Azure DNS overview](dns-overview.md).</span></span>

<span data-ttu-id="f34ac-146">Per altre informazioni sulla gestione delle zone DNS in DNS Azure, vedere [Gestire le zone DNS in DNS Azure usando l'interfaccia della riga di comando di Azure 1.0](dns-operations-dnszones-cli-nodejs.md).</span><span class="sxs-lookup"><span data-stu-id="f34ac-146">To learn more about managing DNS zones in Azure DNS, see [Manage DNS zones in Azure DNS using Azure CLI 1.0](dns-operations-dnszones-cli-nodejs.md).</span></span>

<span data-ttu-id="f34ac-147">Per altre informazioni sulla gestione dei record DNS in DNS Azure, vedere [Gestire i record e i set di record DNS in DNS Azure usando l'interfaccia della riga di comando di Azure 1.0](dns-operations-recordsets-cli-nodejs.md).</span><span class="sxs-lookup"><span data-stu-id="f34ac-147">To learn more about managing DNS records in Azure DNS, see [Manage DNS records and record sets in Azure DNS using Azure CLI 1.0](dns-operations-recordsets-cli-nodejs.md).</span></span>


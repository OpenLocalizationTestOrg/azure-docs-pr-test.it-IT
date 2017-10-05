---
title: Introduzione a DNS Azure con l'interfaccia della riga di comando di Azure 2.0 | Microsoft Docs
description: Informazioni su come creare una zona e un record DNS in DNS Azure. Si tratta di una guida dettagliata per creare e gestire la prima zona e il primo record DNS usando l'interfaccia della riga di comando di Azure 2.0.
services: dns
documentationcenter: na
author: jtuliani
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: fb0aa0a6-d096-4d6a-b2f6-eda1c64f6182
ms.service: dns
ms.devlang: azurecli
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 03/10/2017
ms.author: jonatul
ms.openlocfilehash: 6958d61b29961f59cb22f62bec55f2d467e7e7cb
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="get-started-with-azure-dns-using-azure-cli-20"></a><span data-ttu-id="bf2a5-104">Introduzione a DNS Azure con l'interfaccia della riga di comando di Azure 2.0</span><span class="sxs-lookup"><span data-stu-id="bf2a5-104">Get started with Azure DNS using Azure CLI 2.0</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="bf2a5-105">Portale di Azure</span><span class="sxs-lookup"><span data-stu-id="bf2a5-105">Azure portal</span></span>](dns-getstarted-portal.md)
> * [<span data-ttu-id="bf2a5-106">PowerShell</span><span class="sxs-lookup"><span data-stu-id="bf2a5-106">PowerShell</span></span>](dns-getstarted-powershell.md)
> * [<span data-ttu-id="bf2a5-107">Interfaccia della riga di comando di Azure 1.0</span><span class="sxs-lookup"><span data-stu-id="bf2a5-107">Azure CLI 1.0</span></span>](dns-getstarted-cli-nodejs.md)
> * [<span data-ttu-id="bf2a5-108">Interfaccia della riga di comando di Azure 2.0</span><span class="sxs-lookup"><span data-stu-id="bf2a5-108">Azure CLI 2.0</span></span>](dns-getstarted-cli.md)

<span data-ttu-id="bf2a5-109">Questo articolo illustra i passaggi per creare la prima zona e il primo record DNS usando l'interfaccia della riga di comando di Azure 2.0 tra piattaforme, disponibile per Windows, Mac e Linux.</span><span class="sxs-lookup"><span data-stu-id="bf2a5-109">This article walks you through the steps to create your first DNS zone and record using the cross-platform Azure CLI 2.0, which is available for Windows, Mac and Linux.</span></span> <span data-ttu-id="bf2a5-110">È anche possibile eseguire questi passaggi tramite il portale di Azure o Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="bf2a5-110">You can also perform these steps using the Azure portal or Azure PowerShell.</span></span>

<span data-ttu-id="bf2a5-111">Una zona DNS viene usata per ospitare i record DNS per un particolare dominio.</span><span class="sxs-lookup"><span data-stu-id="bf2a5-111">A DNS zone is used to host the DNS records for a particular domain.</span></span> <span data-ttu-id="bf2a5-112">Per iniziare a ospitare il dominio in DNS di Azure, è necessario creare una zona DNS per il nome di dominio.</span><span class="sxs-lookup"><span data-stu-id="bf2a5-112">To start hosting your domain in Azure DNS, you need to create a DNS zone for that domain name.</span></span> <span data-ttu-id="bf2a5-113">Ogni record DNS per il dominio viene quindi creato all'interno di questa zona DNS.</span><span class="sxs-lookup"><span data-stu-id="bf2a5-113">Each DNS record for your domain is then created inside this DNS zone.</span></span> <span data-ttu-id="bf2a5-114">Per pubblicare infine la zona DNS su Internet, è necessario configurare i server dei nomi per il dominio.</span><span class="sxs-lookup"><span data-stu-id="bf2a5-114">Finally, to publish your DNS zone to the Internet, you need to configure the name servers for the domain.</span></span> <span data-ttu-id="bf2a5-115">Ogni passaggio è illustrato di seguito.</span><span class="sxs-lookup"><span data-stu-id="bf2a5-115">Each of these steps is described below.</span></span>

<span data-ttu-id="bf2a5-116">Queste istruzioni presuppongono che l'interfaccia della riga di comando di Azure 2.0 sia già stata installata e che sia già stato eseguito l'accesso.</span><span class="sxs-lookup"><span data-stu-id="bf2a5-116">These instructions assume you have already installed and signed in to Azure CLI 2.0.</span></span> <span data-ttu-id="bf2a5-117">Per informazioni, vedere [Come gestire le zone DNS usando l'interfaccia della riga di comando di Azure 2.0](dns-operations-dnszones-cli.md).</span><span class="sxs-lookup"><span data-stu-id="bf2a5-117">For help, see [How to manage DNS zones using Azure CLI 2.0](dns-operations-dnszones-cli.md).</span></span>

## <a name="create-the-resource-group"></a><span data-ttu-id="bf2a5-118">Creare il gruppo di risorse.</span><span class="sxs-lookup"><span data-stu-id="bf2a5-118">Create the resource group</span></span>

<span data-ttu-id="bf2a5-119">Prima di creare la zona DNS, viene creato un gruppo di risorse per contenere la zona DNS.</span><span class="sxs-lookup"><span data-stu-id="bf2a5-119">Before creating the DNS zone, a resource group is created to contain the DNS Zone.</span></span> <span data-ttu-id="bf2a5-120">Di seguito è riportato il comando.</span><span class="sxs-lookup"><span data-stu-id="bf2a5-120">The following shows the command.</span></span>

```azurecli
az group create --name MyResourceGroup --location "West US"
```

## <a name="create-a-dns-zone"></a><span data-ttu-id="bf2a5-121">Creare una zona DNS</span><span class="sxs-lookup"><span data-stu-id="bf2a5-121">Create a DNS zone</span></span>

<span data-ttu-id="bf2a5-122">Una zona DNS viene creata utilizzando il comando `az network dns zone create` .</span><span class="sxs-lookup"><span data-stu-id="bf2a5-122">A DNS zone is created using the `az network dns zone create` command.</span></span> <span data-ttu-id="bf2a5-123">Per visualizzare la guida per questo comando, digitare `az network dns zone create -h`.</span><span class="sxs-lookup"><span data-stu-id="bf2a5-123">To see help for this command, type `az network dns zone create -h`.</span></span>

<span data-ttu-id="bf2a5-124">L'esempio seguente crea una zona DNS denominata *contoso.com* nel gruppo di risorse *MyResourceGroup*.</span><span class="sxs-lookup"><span data-stu-id="bf2a5-124">The following example creates a DNS zone called *contoso.com* in the resource group *MyResourceGroup*.</span></span> <span data-ttu-id="bf2a5-125">Usare l'esempio per creare una zona DNS, sostituendo i valori con quelli personalizzati.</span><span class="sxs-lookup"><span data-stu-id="bf2a5-125">Use the example to create a DNS zone, substituting the values for your own.</span></span>

```azurecli
az network dns zone create -g MyResourceGroup -n contoso.com
```


## <a name="create-a-dns-record"></a><span data-ttu-id="bf2a5-126">Creare un record DNS</span><span class="sxs-lookup"><span data-stu-id="bf2a5-126">Create a DNS record</span></span>

<span data-ttu-id="bf2a5-127">Per creare un record DNS, usare il comando `az network dns record-set [record type] add-record`.</span><span class="sxs-lookup"><span data-stu-id="bf2a5-127">To create a DNS record, use the `az network dns record-set [record type] add-record` command.</span></span> <span data-ttu-id="bf2a5-128">Per informazioni, ad esempio per i record A, vedere `azure network dns record-set A add-record -h`.</span><span class="sxs-lookup"><span data-stu-id="bf2a5-128">For help, for A records for example, see `azure network dns record-set A add-record -h`.</span></span>

<span data-ttu-id="bf2a5-129">L'esempio seguente crea un record con il nome relativo "www" nella zona DNS "contoso.com" nel gruppo di risorse "MyResourceGroup".</span><span class="sxs-lookup"><span data-stu-id="bf2a5-129">The following example creates a record with the relative name "www" in the DNS Zone "contoso.com", in resource group "MyResourceGroup".</span></span> <span data-ttu-id="bf2a5-130">Il nome completo del set di record sarà "www.contoso.com".</span><span class="sxs-lookup"><span data-stu-id="bf2a5-130">The fully-qualified name of the record set is "www.contoso.com".</span></span> <span data-ttu-id="bf2a5-131">Il tipo di record è "A" con indirizzo IP "1.2.3.4" e viene usato un valore TTL predefinito di 3600 secondi (1 ora).</span><span class="sxs-lookup"><span data-stu-id="bf2a5-131">The record type is "A", with IP address "1.2.3.4", and a default TTL of 3600 seconds (1 hour) is used.</span></span>

```azurecli
az network dns record-set a add-record -g MyResourceGroup -z contoso.com -n www -a 1.2.3.4
```

<span data-ttu-id="bf2a5-132">Per altri tipi di record, per set di record con più di un record, per valori TTL alternativi e per modificare i record esistenti, vedere [Gestire record e set di record DNS con l'interfaccia della riga di comando di Azure 2.0](dns-operations-recordsets-cli.md).</span><span class="sxs-lookup"><span data-stu-id="bf2a5-132">For other record types, for record sets with more than one record, for alternative TTL values, and to modify existing records, see [Manage DNS records and record sets using the Azure CLI 2.0](dns-operations-recordsets-cli.md).</span></span>


## <a name="view-records"></a><span data-ttu-id="bf2a5-133">Visualizzare i record</span><span class="sxs-lookup"><span data-stu-id="bf2a5-133">View records</span></span>

<span data-ttu-id="bf2a5-134">Per elencare i record DNS nella zona, usare:</span><span class="sxs-lookup"><span data-stu-id="bf2a5-134">To list the DNS records in your zone, use:</span></span>

```azurecli
az network dns record-set list -g MyResourceGroup -z contoso.com
```


## <a name="update-name-servers"></a><span data-ttu-id="bf2a5-135">Aggiornare i server dei nomi</span><span class="sxs-lookup"><span data-stu-id="bf2a5-135">Update name servers</span></span>

<span data-ttu-id="bf2a5-136">Dopo essersi assicurati che la zona e i record DNS siano stati configurati correttamente, è necessario configurare il nome di dominio in modo che usi i server dei nomi di DNS Azure.</span><span class="sxs-lookup"><span data-stu-id="bf2a5-136">Once you are satisfied that your DNS zone and records have been set up correctly, you need to configure your domain name to use the Azure DNS name servers.</span></span> <span data-ttu-id="bf2a5-137">Ciò consente agli altri utenti su Internet di trovare i record DNS.</span><span class="sxs-lookup"><span data-stu-id="bf2a5-137">This enables other users on the Internet to find your DNS records.</span></span>

<span data-ttu-id="bf2a5-138">I server dei nomi per la zona vengono specificati tramite il comando `az network dns zone show`.</span><span class="sxs-lookup"><span data-stu-id="bf2a5-138">The name servers for your zone are given by the `az network dns zone show` command.</span></span> <span data-ttu-id="bf2a5-139">Per visualizzare i nomi dei server dei nomi, usare l'output JSON, come mostrato nell'esempio seguente.</span><span class="sxs-lookup"><span data-stu-id="bf2a5-139">To see the name server names, use JSON output, as shown in the following example.</span></span>

```azurecli
az network dns zone show -g MyResourceGroup -n contoso.com -o json

{
  "etag": "00000003-0000-0000-b40d-0996b97ed101",
  "id": "/subscriptions/a385a691-bd93-41b0-8084-8213ebc5bff7/resourceGroups/myresourcegroup/providers/Microsoft.Network/dnszones/contoso.com",
  "location": "global",
  "maxNumberOfRecordSets": 5000,
  "name": "contoso.com",
  "nameServers": [
    "ns1-01.azure-dns.com.",
    "ns2-01.azure-dns.net.",
    "ns3-01.azure-dns.org.",
    "ns4-01.azure-dns.info."
  ],
  "numberOfRecordSets": 3,
  "resourceGroup": "myresourcegroup",
  "tags": {},
  "type": "Microsoft.Network/dnszones"
}
```

<span data-ttu-id="bf2a5-140">I server dei nomi devono essere configurati con il registrar dei nomi di dominio, in cui è stato acquistato il nome di dominio.</span><span class="sxs-lookup"><span data-stu-id="bf2a5-140">These name servers should be configured with the domain name registrar (where you purchased the domain name).</span></span> <span data-ttu-id="bf2a5-141">Il registrar offrirà l'opzione per la configurazione dei server dei nomi per il dominio.</span><span class="sxs-lookup"><span data-stu-id="bf2a5-141">Your registrar will offer the option to set up the name servers for the domain.</span></span> <span data-ttu-id="bf2a5-142">Per altre informazioni, vedere [Delegare un dominio al servizio DNS Azure](dns-domain-delegation.md).</span><span class="sxs-lookup"><span data-stu-id="bf2a5-142">For more information, see [Delegate your domain to Azure DNS](dns-domain-delegation.md).</span></span>

## <a name="delete-all-resources"></a><span data-ttu-id="bf2a5-143">Eliminare tutte le risorse</span><span class="sxs-lookup"><span data-stu-id="bf2a5-143">Delete all resources</span></span>
 
<span data-ttu-id="bf2a5-144">Per eliminare tutte le risorse create in questo articolo, seguire questa procedura:</span><span class="sxs-lookup"><span data-stu-id="bf2a5-144">To delete all resources created in this article, take the following step:</span></span>

```azurecli
az group delete --name MyResourceGroup
```

## <a name="next-steps"></a><span data-ttu-id="bf2a5-145">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="bf2a5-145">Next steps</span></span>

<span data-ttu-id="bf2a5-146">Per altre informazioni sul servizio DNS Azure, vedere [Panoramica di DNS Azure](dns-overview.md).</span><span class="sxs-lookup"><span data-stu-id="bf2a5-146">To learn more about Azure DNS, see [Azure DNS overview](dns-overview.md).</span></span>

<span data-ttu-id="bf2a5-147">Per altre informazioni sulla gestione delle zone DNS in DNS Azure, vedere [Gestire le zone DNS in DNS Azure usando l'interfaccia della riga di comando di Azure 2.0](dns-operations-dnszones-cli.md).</span><span class="sxs-lookup"><span data-stu-id="bf2a5-147">To learn more about managing DNS zones in Azure DNS, see [Manage DNS zones in Azure DNS using Azure CLI 2.0](dns-operations-dnszones-cli.md).</span></span>

<span data-ttu-id="bf2a5-148">Per altre informazioni sulla gestione dei record DNS in DNS Azure, vedere [Gestire i record e i set di record DNS in DNS Azure usando l'interfaccia della riga di comando di Azure 2.0](dns-operations-recordsets-cli.md).</span><span class="sxs-lookup"><span data-stu-id="bf2a5-148">To learn more about managing DNS records in Azure DNS, see [Manage DNS records and record sets in Azure DNS using Azure CLI 2.0](dns-operations-recordsets-cli.md).</span></span>

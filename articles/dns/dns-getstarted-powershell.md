---
title: Introduzione a DNS Azure con PowerShell | Microsoft Docs
description: Informazioni su come creare una zona e un record DNS in DNS Azure. Si tratta di una guida dettagliata per creare e gestire la prima zona e il primo record DNS usando PowerShell.
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
ms.openlocfilehash: 48f7ba325f61b4a91c0208b4c99058da801bee19
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="get-started-with-azure-dns-using-powershell"></a><span data-ttu-id="47e4f-104">Introduzione a DNS Azure con PowerShell</span><span class="sxs-lookup"><span data-stu-id="47e4f-104">Get Started with Azure DNS using PowerShell</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="47e4f-105">Portale di Azure</span><span class="sxs-lookup"><span data-stu-id="47e4f-105">Azure portal</span></span>](dns-getstarted-portal.md)
> * [<span data-ttu-id="47e4f-106">PowerShell</span><span class="sxs-lookup"><span data-stu-id="47e4f-106">PowerShell</span></span>](dns-getstarted-powershell.md)
> * [<span data-ttu-id="47e4f-107">Interfaccia della riga di comando di Azure 1.0</span><span class="sxs-lookup"><span data-stu-id="47e4f-107">Azure CLI 1.0</span></span>](dns-getstarted-cli-nodejs.md)
> * [<span data-ttu-id="47e4f-108">Interfaccia della riga di comando di Azure 2.0</span><span class="sxs-lookup"><span data-stu-id="47e4f-108">Azure CLI 2.0</span></span>](dns-getstarted-cli.md)

<span data-ttu-id="47e4f-109">Questo articolo illustra i passaggi per creare la prima zona e il primo record DNS con Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="47e4f-109">This article walks you through the steps to create your first DNS zone and record using Azure PowerShell.</span></span> <span data-ttu-id="47e4f-110">È possibile eseguire questi passaggi usando il portale di Azure o nell'interfaccia della riga di comando di Azure multipiattaforma.</span><span class="sxs-lookup"><span data-stu-id="47e4f-110">You can also perform these steps using the Azure portal or the cross-platform Azure CLI.</span></span>

<span data-ttu-id="47e4f-111">Una zona DNS viene usata per ospitare i record DNS per un particolare dominio.</span><span class="sxs-lookup"><span data-stu-id="47e4f-111">A DNS zone is used to host the DNS records for a particular domain.</span></span> <span data-ttu-id="47e4f-112">Per iniziare a ospitare il dominio in DNS di Azure, è necessario creare una zona DNS per il nome di dominio.</span><span class="sxs-lookup"><span data-stu-id="47e4f-112">To start hosting your domain in Azure DNS, you need to create a DNS zone for that domain name.</span></span> <span data-ttu-id="47e4f-113">Ogni record DNS per il dominio viene quindi creato all'interno di questa zona DNS.</span><span class="sxs-lookup"><span data-stu-id="47e4f-113">Each DNS record for your domain is then created inside this DNS zone.</span></span> <span data-ttu-id="47e4f-114">Per pubblicare infine la zona DNS su Internet, è necessario configurare i server dei nomi per il dominio.</span><span class="sxs-lookup"><span data-stu-id="47e4f-114">Finally, to publish your DNS zone to the Internet, you need to configure the name servers for the domain.</span></span> <span data-ttu-id="47e4f-115">Ogni passaggio è illustrato di seguito.</span><span class="sxs-lookup"><span data-stu-id="47e4f-115">Each of these steps is described below.</span></span>

<span data-ttu-id="47e4f-116">Queste istruzioni presuppongono che Azure PowerShell sia già stato installato e che sia già stato eseguito l'accesso.</span><span class="sxs-lookup"><span data-stu-id="47e4f-116">These instructions assume you have already installed and signed in to Azure PowerShell.</span></span> <span data-ttu-id="47e4f-117">Per informazioni, vedere [Come gestire le zone DNS usando PowerShell](dns-operations-dnszones.md).</span><span class="sxs-lookup"><span data-stu-id="47e4f-117">For help, see [How to manage DNS zones using PowerShell](dns-operations-dnszones.md).</span></span>

## <a name="create-the-resource-group"></a><span data-ttu-id="47e4f-118">Creare il gruppo di risorse.</span><span class="sxs-lookup"><span data-stu-id="47e4f-118">Create the resource group</span></span>

<span data-ttu-id="47e4f-119">Prima di creare la zona DNS, viene creato un gruppo di risorse per contenere la zona DNS.</span><span class="sxs-lookup"><span data-stu-id="47e4f-119">Before creating the DNS zone, a resource group is created to contain the DNS Zone.</span></span> <span data-ttu-id="47e4f-120">Di seguito è riportato il comando.</span><span class="sxs-lookup"><span data-stu-id="47e4f-120">The following shows the command.</span></span>

```powershell
New-AzureRMResourceGroup -name MyResourceGroup -location "westus"
```

## <a name="create-a-dns-zone"></a><span data-ttu-id="47e4f-121">Creare una zona DNS</span><span class="sxs-lookup"><span data-stu-id="47e4f-121">Create a DNS zone</span></span>

<span data-ttu-id="47e4f-122">Viene creata una zona DNS con il cmdlet `New-AzureRmDnsZone` .</span><span class="sxs-lookup"><span data-stu-id="47e4f-122">A DNS zone is created by using the `New-AzureRmDnsZone` cmdlet.</span></span> <span data-ttu-id="47e4f-123">L'esempio seguente crea una zona DNS denominata *contoso.com* nel gruppo di risorse denominato *MyResourceGroup*.</span><span class="sxs-lookup"><span data-stu-id="47e4f-123">The following example creates a DNS zone called *contoso.com* in the resource group called *MyResourceGroup*.</span></span> <span data-ttu-id="47e4f-124">Usare l'esempio per creare una zona DNS, sostituendo i valori con quelli personalizzati.</span><span class="sxs-lookup"><span data-stu-id="47e4f-124">Use the example to create a DNS zone, substituting the values for your own.</span></span>

```powershell
New-AzureRmDnsZone -Name contoso.com -ResourceGroupName MyResourceGroup
```

## <a name="create-a-dns-record"></a><span data-ttu-id="47e4f-125">Creare un record DNS</span><span class="sxs-lookup"><span data-stu-id="47e4f-125">Create a DNS record</span></span>

<span data-ttu-id="47e4f-126">I set di record vengono creati usando il cmdlet `New-AzureRmDnsRecordSet`.</span><span class="sxs-lookup"><span data-stu-id="47e4f-126">You create record sets by using the `New-AzureRmDnsRecordSet` cmdlet.</span></span> <span data-ttu-id="47e4f-127">L'esempio seguente crea un record con il nome relativo "www" nella zona DNS "contoso.com" nel gruppo di risorse "MyResourceGroup".</span><span class="sxs-lookup"><span data-stu-id="47e4f-127">The following example creates a record with the relative name "www" in the DNS Zone "contoso.com", in resource group "MyResourceGroup".</span></span> <span data-ttu-id="47e4f-128">Il nome completo del set di record sarà "www.contoso.com".</span><span class="sxs-lookup"><span data-stu-id="47e4f-128">The fully-qualified name of the record set is "www.contoso.com".</span></span> <span data-ttu-id="47e4f-129">Il tipo di record è "A", con indirizzo IP "1.2.3.4", e la durata (TTL) è 3600 secondi.</span><span class="sxs-lookup"><span data-stu-id="47e4f-129">The record type is "A", with IP address "1.2.3.4", and the TTL is 3600 seconds.</span></span>

```powershell
New-AzureRmDnsRecordSet -Name www -RecordType A -ZoneName contoso.com -ResourceGroupName MyResourceGroup -Ttl 3600 -DnsRecords (New-AzureRmDnsRecordConfig -IPv4Address "1.2.3.4")
```

<span data-ttu-id="47e4f-130">Per altri tipi di record, per set di record con più di un record e per modificare i record esistenti, vedere [Gestire record e set di record DNS con Azure PowerShell](dns-operations-recordsets.md).</span><span class="sxs-lookup"><span data-stu-id="47e4f-130">For other record types, for record sets with more than one record, and to modify existing records, see [Manage DNS records and record sets using Azure PowerShell](dns-operations-recordsets.md).</span></span> 


## <a name="view-records"></a><span data-ttu-id="47e4f-131">Visualizzare i record</span><span class="sxs-lookup"><span data-stu-id="47e4f-131">View records</span></span>

<span data-ttu-id="47e4f-132">Per elencare i record DNS nella zona, usare:</span><span class="sxs-lookup"><span data-stu-id="47e4f-132">To list the DNS records in your zone, use:</span></span>

```powershell
Get-AzureRmDnsRecordSet -ZoneName contoso.com -ResourceGroupName MyResourceGroup
```


## <a name="update-name-servers"></a><span data-ttu-id="47e4f-133">Aggiornare i server dei nomi</span><span class="sxs-lookup"><span data-stu-id="47e4f-133">Update name servers</span></span>

<span data-ttu-id="47e4f-134">Dopo essersi assicurati che la zona e i record DNS siano stati configurati correttamente, è necessario configurare il nome di dominio in modo che usi i server dei nomi di DNS Azure.</span><span class="sxs-lookup"><span data-stu-id="47e4f-134">Once you are satisfied that your DNS zone and records have been set up correctly, you need to configure your domain name to use the Azure DNS name servers.</span></span> <span data-ttu-id="47e4f-135">Ciò consente agli altri utenti su Internet di trovare i record DNS.</span><span class="sxs-lookup"><span data-stu-id="47e4f-135">This enables other users on the Internet to find your DNS records.</span></span>

<span data-ttu-id="47e4f-136">I server dei nomi per la zona vengono specificati tramite il cmdlet `Get-AzureRmDnsZone`:</span><span class="sxs-lookup"><span data-stu-id="47e4f-136">The name servers for your zone are given by the `Get-AzureRmDnsZone` cmdlet:</span></span>

```powershell
Get-AzureRmDnsZone -ZoneName contoso.com -ResourceGroupName MyResourceGroup

Name                  : contoso.com
ResourceGroupName     : myresourcegroup
Etag                  : 00000003-0000-0000-b40d-0996b97ed101
Tags                  : {}
NameServers           : {ns1-01.azure-dns.com., ns2-01.azure-dns.net., ns3-01.azure-dns.org., ns4-01.azure-dns.info.}
NumberOfRecordSets    : 3
MaxNumberOfRecordSets : 5000
```

<span data-ttu-id="47e4f-137">I server dei nomi devono essere configurati con il registrar dei nomi di dominio, in cui è stato acquistato il nome di dominio.</span><span class="sxs-lookup"><span data-stu-id="47e4f-137">These name servers should be configured with the domain name registrar (where you purchased the domain name).</span></span> <span data-ttu-id="47e4f-138">Il registrar offrirà l'opzione per la configurazione dei server dei nomi per il dominio.</span><span class="sxs-lookup"><span data-stu-id="47e4f-138">Your registrar will offer the option to set up the name servers for the domain.</span></span> <span data-ttu-id="47e4f-139">Per altre informazioni, vedere [Delegare un dominio al servizio DNS Azure](dns-domain-delegation.md).</span><span class="sxs-lookup"><span data-stu-id="47e4f-139">For more information, see [Delegate your domain to Azure DNS](dns-domain-delegation.md).</span></span>

## <a name="delete-all-resources"></a><span data-ttu-id="47e4f-140">Eliminare tutte le risorse</span><span class="sxs-lookup"><span data-stu-id="47e4f-140">Delete all resources</span></span>

<span data-ttu-id="47e4f-141">Per eliminare tutte le risorse create in questo articolo, seguire questa procedura:</span><span class="sxs-lookup"><span data-stu-id="47e4f-141">To delete all resources created in this article, take the following step:</span></span>

```powershell
Remove-AzureRMResourceGroup -Name MyResourceGroup
```

## <a name="next-steps"></a><span data-ttu-id="47e4f-142">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="47e4f-142">Next steps</span></span>

<span data-ttu-id="47e4f-143">Per altre informazioni sul servizio DNS Azure, vedere [Panoramica di DNS Azure](dns-overview.md).</span><span class="sxs-lookup"><span data-stu-id="47e4f-143">To learn more about Azure DNS, see [Azure DNS overview](dns-overview.md).</span></span>

<span data-ttu-id="47e4f-144">Per altre informazioni sulla gestione delle zone DNS in DNS Azure, vedere [Gestire le zone DNS in DNS Azure usando PowerShell](dns-operations-dnszones.md).</span><span class="sxs-lookup"><span data-stu-id="47e4f-144">To learn more about managing DNS zones in Azure DNS, see [Manage DNS zones in Azure DNS using PowerShell](dns-operations-dnszones.md).</span></span>

<span data-ttu-id="47e4f-145">Per altre informazioni sulla gestione dei record DNS in DNS Azure, vedere [Gestire i record e i set di record DNS in DNS Azure usando PowerShell](dns-operations-recordsets.md).</span><span class="sxs-lookup"><span data-stu-id="47e4f-145">To learn more about managing DNS records in Azure DNS, see [Manage DNS records and record sets in Azure DNS using PowerShell](dns-operations-recordsets.md).</span></span>


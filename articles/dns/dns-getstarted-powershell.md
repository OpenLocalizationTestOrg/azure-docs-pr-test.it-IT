---
title: aaaGet avviato con il DNS di Azure tramite PowerShell | Documenti Microsoft
description: "Informazioni su come toocreate un DNS zona e questo record in DNS di Azure. Questo è un toocreate Guida dettagliata e la zona DNS prima di gestire e registrare l'utilizzo di PowerShell."
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
ms.openlocfilehash: 0f9dead1e4b44fcc74c84a024c41cdfaeb02b5d3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-azure-dns-using-powershell"></a><span data-ttu-id="8e738-104">Introduzione a DNS Azure con PowerShell</span><span class="sxs-lookup"><span data-stu-id="8e738-104">Get Started with Azure DNS using PowerShell</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="8e738-105">Portale di Azure</span><span class="sxs-lookup"><span data-stu-id="8e738-105">Azure portal</span></span>](dns-getstarted-portal.md)
> * [<span data-ttu-id="8e738-106">PowerShell</span><span class="sxs-lookup"><span data-stu-id="8e738-106">PowerShell</span></span>](dns-getstarted-powershell.md)
> * [<span data-ttu-id="8e738-107">Interfaccia della riga di comando di Azure 1.0</span><span class="sxs-lookup"><span data-stu-id="8e738-107">Azure CLI 1.0</span></span>](dns-getstarted-cli-nodejs.md)
> * [<span data-ttu-id="8e738-108">Interfaccia della riga di comando di Azure 2.0</span><span class="sxs-lookup"><span data-stu-id="8e738-108">Azure CLI 2.0</span></span>](dns-getstarted-cli.md)

<span data-ttu-id="8e738-109">In questo articolo illustra hello passaggi toocreate prima zona DNS il record utilizzando Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="8e738-109">This article walks you through hello steps toocreate your first DNS zone and record using Azure PowerShell.</span></span> <span data-ttu-id="8e738-110">È anche possibile eseguire questi passaggi tramite il portale di Azure hello o hello multipiattaforma CLI di Azure.</span><span class="sxs-lookup"><span data-stu-id="8e738-110">You can also perform these steps using hello Azure portal or hello cross-platform Azure CLI.</span></span>

<span data-ttu-id="8e738-111">Una zona DNS è utilizzato toohost hello DNS record per un particolare dominio.</span><span class="sxs-lookup"><span data-stu-id="8e738-111">A DNS zone is used toohost hello DNS records for a particular domain.</span></span> <span data-ttu-id="8e738-112">toostart hosting del dominio DNS di Azure, è necessario toocreate una zona DNS per il nome di dominio.</span><span class="sxs-lookup"><span data-stu-id="8e738-112">toostart hosting your domain in Azure DNS, you need toocreate a DNS zone for that domain name.</span></span> <span data-ttu-id="8e738-113">Ogni record DNS per il dominio viene quindi creato all'interno di questa zona DNS.</span><span class="sxs-lookup"><span data-stu-id="8e738-113">Each DNS record for your domain is then created inside this DNS zone.</span></span> <span data-ttu-id="8e738-114">Infine, toopublish della zona DNS toohello Internet, server dei nomi tooconfigure hello è necessario per il dominio hello.</span><span class="sxs-lookup"><span data-stu-id="8e738-114">Finally, toopublish your DNS zone toohello Internet, you need tooconfigure hello name servers for hello domain.</span></span> <span data-ttu-id="8e738-115">Ogni passaggio è illustrato di seguito.</span><span class="sxs-lookup"><span data-stu-id="8e738-115">Each of these steps is described below.</span></span>

<span data-ttu-id="8e738-116">Queste istruzioni presuppongono aver già installato e connesso tooAzure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="8e738-116">These instructions assume you have already installed and signed in tooAzure PowerShell.</span></span> <span data-ttu-id="8e738-117">Per ulteriori informazioni, vedere [come toomanage DNS zone tramite PowerShell](dns-operations-dnszones.md).</span><span class="sxs-lookup"><span data-stu-id="8e738-117">For help, see [How toomanage DNS zones using PowerShell](dns-operations-dnszones.md).</span></span>

## <a name="create-hello-resource-group"></a><span data-ttu-id="8e738-118">Creare il gruppo di risorse hello</span><span class="sxs-lookup"><span data-stu-id="8e738-118">Create hello resource group</span></span>

<span data-ttu-id="8e738-119">Prima di creare una zona DNS hello, un gruppo di risorse viene creato toocontain zona di DNS hello.</span><span class="sxs-lookup"><span data-stu-id="8e738-119">Before creating hello DNS zone, a resource group is created toocontain hello DNS Zone.</span></span> <span data-ttu-id="8e738-120">Hello seguito è riportato il comando hello.</span><span class="sxs-lookup"><span data-stu-id="8e738-120">hello following shows hello command.</span></span>

```powershell
New-AzureRMResourceGroup -name MyResourceGroup -location "westus"
```

## <a name="create-a-dns-zone"></a><span data-ttu-id="8e738-121">Creare una zona DNS</span><span class="sxs-lookup"><span data-stu-id="8e738-121">Create a DNS zone</span></span>

<span data-ttu-id="8e738-122">Una zona DNS viene creata utilizzando hello `New-AzureRmDnsZone` cmdlet.</span><span class="sxs-lookup"><span data-stu-id="8e738-122">A DNS zone is created by using hello `New-AzureRmDnsZone` cmdlet.</span></span> <span data-ttu-id="8e738-123">esempio Hello crea una zona DNS denominata *contoso.com* nel gruppo di risorse hello chiamato *MyResourceGroup*.</span><span class="sxs-lookup"><span data-stu-id="8e738-123">hello following example creates a DNS zone called *contoso.com* in hello resource group called *MyResourceGroup*.</span></span> <span data-ttu-id="8e738-124">Utilizzare l'esempio toocreate hello una zona DNS, sostituendo i valori hello per uso personale.</span><span class="sxs-lookup"><span data-stu-id="8e738-124">Use hello example toocreate a DNS zone, substituting hello values for your own.</span></span>

```powershell
New-AzureRmDnsZone -Name contoso.com -ResourceGroupName MyResourceGroup
```

## <a name="create-a-dns-record"></a><span data-ttu-id="8e738-125">Creare un record DNS</span><span class="sxs-lookup"><span data-stu-id="8e738-125">Create a DNS record</span></span>

<span data-ttu-id="8e738-126">Per creare set di record, utilizzare hello `New-AzureRmDnsRecordSet` cmdlet.</span><span class="sxs-lookup"><span data-stu-id="8e738-126">You create record sets by using hello `New-AzureRmDnsRecordSet` cmdlet.</span></span> <span data-ttu-id="8e738-127">Hello seguente viene creato un record con il nome relativo hello "www" hello "contoso.com", nel gruppo di risorse "MyResourceGroup" zona di DNS.</span><span class="sxs-lookup"><span data-stu-id="8e738-127">hello following example creates a record with hello relative name "www" in hello DNS Zone "contoso.com", in resource group "MyResourceGroup".</span></span> <span data-ttu-id="8e738-128">nome completo di Hello del set di record hello è "www.contoso.com".</span><span class="sxs-lookup"><span data-stu-id="8e738-128">hello fully-qualified name of hello record set is "www.contoso.com".</span></span> <span data-ttu-id="8e738-129">tipo di record Hello è "A", con l'indirizzo IP "1.2.3.4" e hello TTL è 3600 secondi.</span><span class="sxs-lookup"><span data-stu-id="8e738-129">hello record type is "A", with IP address "1.2.3.4", and hello TTL is 3600 seconds.</span></span>

```powershell
New-AzureRmDnsRecordSet -Name www -RecordType A -ZoneName contoso.com -ResourceGroupName MyResourceGroup -Ttl 3600 -DnsRecords (New-AzureRmDnsRecordConfig -IPv4Address "1.2.3.4")
```

<span data-ttu-id="8e738-130">Per altri tipi di record, per i set di record con più di un record e i record esistenti toomodify, vedere [record DNS di gestione e i set di record con Azure PowerShell](dns-operations-recordsets.md).</span><span class="sxs-lookup"><span data-stu-id="8e738-130">For other record types, for record sets with more than one record, and toomodify existing records, see [Manage DNS records and record sets using Azure PowerShell](dns-operations-recordsets.md).</span></span> 


## <a name="view-records"></a><span data-ttu-id="8e738-131">Visualizzare i record</span><span class="sxs-lookup"><span data-stu-id="8e738-131">View records</span></span>

<span data-ttu-id="8e738-132">i record DNS di hello toolist nella zona, utilizzare:</span><span class="sxs-lookup"><span data-stu-id="8e738-132">toolist hello DNS records in your zone, use:</span></span>

```powershell
Get-AzureRmDnsRecordSet -ZoneName contoso.com -ResourceGroupName MyResourceGroup
```


## <a name="update-name-servers"></a><span data-ttu-id="8e738-133">Aggiornare i server dei nomi</span><span class="sxs-lookup"><span data-stu-id="8e738-133">Update name servers</span></span>

<span data-ttu-id="8e738-134">Dopo aver soddisfatto che la zona DNS e i record sono stati impostati correttamente, è necessario tooconfigure il nome di dominio toouse server dei nomi DNS di Azure hello.</span><span class="sxs-lookup"><span data-stu-id="8e738-134">Once you are satisfied that your DNS zone and records have been set up correctly, you need tooconfigure your domain name toouse hello Azure DNS name servers.</span></span> <span data-ttu-id="8e738-135">In questo modo altri utenti nel hello Internet toofind i record DNS.</span><span class="sxs-lookup"><span data-stu-id="8e738-135">This enables other users on hello Internet toofind your DNS records.</span></span>

<span data-ttu-id="8e738-136">Server dei nomi per l'area Hello forniti tramite hello `Get-AzureRmDnsZone` cmdlet:</span><span class="sxs-lookup"><span data-stu-id="8e738-136">hello name servers for your zone are given by hello `Get-AzureRmDnsZone` cmdlet:</span></span>

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

<span data-ttu-id="8e738-137">Questi server dei nomi deve essere configurato con hello registrar (in cui è stato acquistato il nome di dominio hello).</span><span class="sxs-lookup"><span data-stu-id="8e738-137">These name servers should be configured with hello domain name registrar (where you purchased hello domain name).</span></span> <span data-ttu-id="8e738-138">Registrar offrirà hello opzione tooset dei server dei nomi per il dominio hello hello.</span><span class="sxs-lookup"><span data-stu-id="8e738-138">Your registrar will offer hello option tooset up hello name servers for hello domain.</span></span> <span data-ttu-id="8e738-139">Per ulteriori informazioni, vedere [delegare il tooAzure di dominio DNS](dns-domain-delegation.md).</span><span class="sxs-lookup"><span data-stu-id="8e738-139">For more information, see [Delegate your domain tooAzure DNS](dns-domain-delegation.md).</span></span>

## <a name="delete-all-resources"></a><span data-ttu-id="8e738-140">Eliminare tutte le risorse</span><span class="sxs-lookup"><span data-stu-id="8e738-140">Delete all resources</span></span>

<span data-ttu-id="8e738-141">toodelete tutte le risorse create in questo articolo, hello take seguente passaggio:</span><span class="sxs-lookup"><span data-stu-id="8e738-141">toodelete all resources created in this article, take hello following step:</span></span>

```powershell
Remove-AzureRMResourceGroup -Name MyResourceGroup
```

## <a name="next-steps"></a><span data-ttu-id="8e738-142">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="8e738-142">Next steps</span></span>

<span data-ttu-id="8e738-143">toolearn ulteriori informazioni su DNS di Azure, vedere [Panoramica di DNS di Azure](dns-overview.md).</span><span class="sxs-lookup"><span data-stu-id="8e738-143">toolearn more about Azure DNS, see [Azure DNS overview](dns-overview.md).</span></span>

<span data-ttu-id="8e738-144">toolearn informazioni su gestione delle zone DNS di DNS di Azure, vedere [le zone DNS di gestione in DNS di Azure con PowerShell](dns-operations-dnszones.md).</span><span class="sxs-lookup"><span data-stu-id="8e738-144">toolearn more about managing DNS zones in Azure DNS, see [Manage DNS zones in Azure DNS using PowerShell](dns-operations-dnszones.md).</span></span>

<span data-ttu-id="8e738-145">toolearn informazioni su gestione dei record DNS nel sistema DNS di Azure, vedere [Manage DNS record e record imposta nel sistema DNS di Azure con PowerShell](dns-operations-recordsets.md).</span><span class="sxs-lookup"><span data-stu-id="8e738-145">toolearn more about managing DNS records in Azure DNS, see [Manage DNS records and record sets in Azure DNS using PowerShell](dns-operations-recordsets.md).</span></span>


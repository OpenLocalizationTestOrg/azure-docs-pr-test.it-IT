---
title: Creare un servizio di bilanciamento del carico con connessione Internet - Azure PowerShell versione classica | Documentazione Microsoft
description: "Informazioni su come creare un servizio di bilanciamento del carico Internet in modalità classica con PowerShell."
services: load-balancer
documentationcenter: na
author: kumudd
manager: timlt
tags: azure-service-management
ms.assetid: 73e8bfa4-8086-4ef0-9e35-9e00b24be319
ms.service: load-balancer
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 01/23/2017
ms.author: kumud
ms.openlocfilehash: 1a41f3ba199fb692c111ea6a40ddb09605f91da2
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="get-started-creating-an-internet-facing-load-balancer-classic-in-powershell"></a><span data-ttu-id="53825-103">Introduzione alla creazione del servizio di bilanciamento del carico Internet (classico) in PowerShell</span><span class="sxs-lookup"><span data-stu-id="53825-103">Get started creating an Internet facing load balancer (classic) in PowerShell</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="53825-104">Portale di Azure classico</span><span class="sxs-lookup"><span data-stu-id="53825-104">Azure classic portal</span></span>](../load-balancer/load-balancer-get-started-internet-classic-portal.md)
> * [<span data-ttu-id="53825-105">PowerShell</span><span class="sxs-lookup"><span data-stu-id="53825-105">PowerShell</span></span>](../load-balancer/load-balancer-get-started-internet-classic-ps.md)
> * [<span data-ttu-id="53825-106">Interfaccia della riga di comando di Azure</span><span class="sxs-lookup"><span data-stu-id="53825-106">Azure CLI</span></span>](../load-balancer/load-balancer-get-started-internet-classic-cli.md)
> * [<span data-ttu-id="53825-107">Servizi cloud di Azure</span><span class="sxs-lookup"><span data-stu-id="53825-107">Azure Cloud Services</span></span>](../load-balancer/load-balancer-get-started-internet-classic-cloud.md)

[!INCLUDE [load-balancer-get-started-internet-intro-include.md](../../includes/load-balancer-get-started-internet-intro-include.md)]

> [!IMPORTANT]
> <span data-ttu-id="53825-108">Prima di iniziare a usare le risorse di Azure, è importante comprendere che Azure al momento offre due modelli di distribuzione, la distribuzione classica e Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="53825-108">Before you work with Azure resources, it's important to understand that Azure currently has two deployment models: Azure Resource Manager and classic.</span></span> <span data-ttu-id="53825-109">È importante comprendere i [modelli e strumenti di distribuzione](../azure-classic-rm.md) prima di lavorare con le risorse di Azure.</span><span class="sxs-lookup"><span data-stu-id="53825-109">Make sure you understand [deployment models and tools](../azure-classic-rm.md) before you work with any Azure resource.</span></span> <span data-ttu-id="53825-110">È possibile visualizzare la documentazione relativa a diversi strumenti facendo clic sulle schede nella parte superiore di questo articolo.</span><span class="sxs-lookup"><span data-stu-id="53825-110">You can view the documentation for different tools by clicking the tabs at the top of this article.</span></span> <span data-ttu-id="53825-111">In questo articolo viene illustrato il modello di distribuzione classica.</span><span class="sxs-lookup"><span data-stu-id="53825-111">This article covers the classic deployment model.</span></span> <span data-ttu-id="53825-112">Vedere [Informazioni su come creare un servizio di bilanciamento del carico Internet in Gestione risorse di Azure](load-balancer-get-started-internet-arm-ps.md).</span><span class="sxs-lookup"><span data-stu-id="53825-112">You can also [Learn how to create an Internet facing load balancer using Azure Resource Manager](load-balancer-get-started-internet-arm-ps.md).</span></span>

[!INCLUDE [load-balancer-get-started-internet-scenario-include.md](../../includes/load-balancer-get-started-internet-scenario-include.md)]

## <a name="set-up-load-balancer-using-powershell"></a><span data-ttu-id="53825-113">Configurazione del servizio di bilanciamento del carico con PowerShell</span><span class="sxs-lookup"><span data-stu-id="53825-113">Set up load balancer using PowerShell</span></span>

<span data-ttu-id="53825-114">Per impostare il servizio di bilanciamento del carico tramite powershell, seguire questa procedura:</span><span class="sxs-lookup"><span data-stu-id="53825-114">To set up a load balancer using powershell, follow the steps below:</span></span>

1. <span data-ttu-id="53825-115">Se è la prima volta che si utilizza Azure PowerShell, vedere [Come installare e configurare Azure PowerShell](/powershell/azure/overview) e seguire le istruzioni fino al termine della procedura per accedere ad Azure e selezionare la sottoscrizione desiderata.</span><span class="sxs-lookup"><span data-stu-id="53825-115">If you have never used Azure PowerShell, see [How to Install and Configure Azure PowerShell](/powershell/azure/overview) and follow the instructions all the way to the end to sign into Azure and select your subscription.</span></span>
2. <span data-ttu-id="53825-116">Dopo avere creato una macchina virtuale, è possibile usare i cmdlet di PowerShell per aggiungere un servizio di bilanciamento del carico a una macchina virtuale all'interno dello stesso servizio cloud.</span><span class="sxs-lookup"><span data-stu-id="53825-116">After creating a virtual machine, you can use PowerShell cmdlets to add a load balancer to a virtual machine within the same cloud service.</span></span>

<span data-ttu-id="53825-117">Nell'esempio seguente si aggiungerà un set di bilanciamento del carico set denominato "webfarm" al servizio cloud "mytestcloud" (o myctestcloud.cloudapp.net), aggiungendo gli endpoint per il bilanciamento del carico alle macchine virtuali denominate "web1" e "web2".</span><span class="sxs-lookup"><span data-stu-id="53825-117">In the following example you will add a load balancer set called "webfarm" to cloud service "mytestcloud" (or myctestcloud.cloudapp.net) , adding the endpoints for the load balancer to virtual machines named "web1" and "web2".</span></span> <span data-ttu-id="53825-118">Il servizio di bilanciamento del carico riceve il traffico di rete sulla porta 80 e bilancia il carico tra le macchine virtuali definite dall’endpoint locale (in questo caso la porta 80) mediante TCP.</span><span class="sxs-lookup"><span data-stu-id="53825-118">The load balancer receives network traffic on port 80 and load balances between the virtual machines defined by the local endpoint (in this case port 80) using TCP.</span></span>

### <a name="step-1"></a><span data-ttu-id="53825-119">Passaggio 1</span><span class="sxs-lookup"><span data-stu-id="53825-119">Step 1</span></span>

<span data-ttu-id="53825-120">Creare un endpoint di carico bilanciato per la prima VM "web1"</span><span class="sxs-lookup"><span data-stu-id="53825-120">Create a load balanced endpoint for the first VM "web1"</span></span>

```powershell
Get-AzureVM -ServiceName "mytestcloud" -Name "web1" | Add-AzureEndpoint -Name "HttpIn" -Protocol "tcp" -PublicPort 80 -LocalPort 80 -LBSetName "WebFarm" -ProbePort 80 -ProbeProtocol "http" -ProbePath '/' | Update-AzureVM
```

### <a name="step-2"></a><span data-ttu-id="53825-121">Passaggio 2</span><span class="sxs-lookup"><span data-stu-id="53825-121">Step 2</span></span>

<span data-ttu-id="53825-122">Creare un altro endpoint per la seconda VM "web2" usando lo stesso nome del set di bilanciamento del carico interno</span><span class="sxs-lookup"><span data-stu-id="53825-122">Create another endpoint for the second VM  "web2" using the same load balancer set name</span></span>

```powershell
Get-AzureVM -ServiceName "mytestcloud" -Name "web2" | Add-AzureEndpoint -Name "HttpIn" -Protocol "tcp" -PublicPort 80 -LocalPort 80 -LBSetName "WebFarm" -ProbePort 80 -ProbeProtocol "http" -ProbePath '/' | Update-AzureVM
```

## <a name="remove-a-virtual-machine-from-a-load-balancer"></a><span data-ttu-id="53825-123">Rimuovere una macchina virtuale dal servizio di bilanciamento del carico</span><span class="sxs-lookup"><span data-stu-id="53825-123">Remove a virtual machine from a load balancer</span></span>

<span data-ttu-id="53825-124">È possibile utilizzare Remove-AzureEndpoint per rimuovere un endpoint della macchina virtuale dal bilanciamento del carico</span><span class="sxs-lookup"><span data-stu-id="53825-124">You can use Remove-AzureEndpoint to remove a virtual machine endpoint from the load balancer</span></span>

```powershell
Get-azureVM -ServiceName mytestcloud  -Name web1 |Remove-AzureEndpoint -Name httpin | Update-AzureVM
```

## <a name="next-steps"></a><span data-ttu-id="53825-125">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="53825-125">Next steps</span></span>

<span data-ttu-id="53825-126">È anche possibile [iniziare a creare un bilanciamento del carico interno](load-balancer-get-started-ilb-classic-ps.md) e configurare il tipo di [modalità di distribuzione](load-balancer-distribution-mode.md) per il comportamento del traffico di rete per un servizio di bilanciamento del carico specifico.</span><span class="sxs-lookup"><span data-stu-id="53825-126">You can also [get started creating an internal load balancer](load-balancer-get-started-ilb-classic-ps.md) and configure what type of [distribution mode](load-balancer-distribution-mode.md) for a specific load balancer network traffic behavior.</span></span>

<span data-ttu-id="53825-127">Se l'applicazione deve mantenere attive le connessioni per i server dietro il servizio di bilanciamento del carico, è possibile ottenere altre informazioni sulle [impostazioni di timeout delle connessioni TCP inattive per un bilanciamento del carico](load-balancer-tcp-idle-timeout.md).</span><span class="sxs-lookup"><span data-stu-id="53825-127">If your application needs to keep connections alive for servers behind a load balancer, you can understand more about [idle TCP timeout settings for a load balancer](load-balancer-tcp-idle-timeout.md).</span></span> <span data-ttu-id="53825-128">Ciò consente di ottenere informazioni sul comportamento delle connessioni inattive quando si usa il servizio di bilanciamento del carico di Azure.</span><span class="sxs-lookup"><span data-stu-id="53825-128">It will help to learn about idle connection behavior when you are using Azure Load Balancer.</span></span>

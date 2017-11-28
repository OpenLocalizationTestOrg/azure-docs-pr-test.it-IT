---
title: con una connessione Internet aaaCreate bilanciamento del carico - PowerShell di Azure classico | Documenti Microsoft
description: "Informazioni su come una connessione Internet toocreate bilanciamento del carico in modalità classica tramite PowerShell"
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
ms.openlocfilehash: 76d9a712a0acda223fc86b80be9c35c0ed9f3a50
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-creating-an-internet-facing-load-balancer-classic-in-powershell"></a><span data-ttu-id="bf501-103">Introduzione alla creazione del servizio di bilanciamento del carico Internet (classico) in PowerShell</span><span class="sxs-lookup"><span data-stu-id="bf501-103">Get started creating an Internet facing load balancer (classic) in PowerShell</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="bf501-104">Portale di Azure classico</span><span class="sxs-lookup"><span data-stu-id="bf501-104">Azure classic portal</span></span>](../load-balancer/load-balancer-get-started-internet-classic-portal.md)
> * [<span data-ttu-id="bf501-105">PowerShell</span><span class="sxs-lookup"><span data-stu-id="bf501-105">PowerShell</span></span>](../load-balancer/load-balancer-get-started-internet-classic-ps.md)
> * [<span data-ttu-id="bf501-106">Interfaccia della riga di comando di Azure</span><span class="sxs-lookup"><span data-stu-id="bf501-106">Azure CLI</span></span>](../load-balancer/load-balancer-get-started-internet-classic-cli.md)
> * [<span data-ttu-id="bf501-107">Servizi cloud di Azure</span><span class="sxs-lookup"><span data-stu-id="bf501-107">Azure Cloud Services</span></span>](../load-balancer/load-balancer-get-started-internet-classic-cloud.md)

[!INCLUDE [load-balancer-get-started-internet-intro-include.md](../../includes/load-balancer-get-started-internet-intro-include.md)]

> [!IMPORTANT]
> <span data-ttu-id="bf501-108">Prima di lavorare con le risorse di Azure, è importante toounderstand che Azure ha due modelli di distribuzione: Gestione risorse di Azure e classica.</span><span class="sxs-lookup"><span data-stu-id="bf501-108">Before you work with Azure resources, it's important toounderstand that Azure currently has two deployment models: Azure Resource Manager and classic.</span></span> <span data-ttu-id="bf501-109">È importante comprendere i [modelli e strumenti di distribuzione](../azure-classic-rm.md) prima di lavorare con le risorse di Azure.</span><span class="sxs-lookup"><span data-stu-id="bf501-109">Make sure you understand [deployment models and tools](../azure-classic-rm.md) before you work with any Azure resource.</span></span> <span data-ttu-id="bf501-110">È possibile visualizzare la documentazione di hello per diversi strumenti facendo clic sulle schede hello nella parte superiore di hello di questo articolo.</span><span class="sxs-lookup"><span data-stu-id="bf501-110">You can view hello documentation for different tools by clicking hello tabs at hello top of this article.</span></span> <span data-ttu-id="bf501-111">Questo articolo descrive il modello di distribuzione classica hello.</span><span class="sxs-lookup"><span data-stu-id="bf501-111">This article covers hello classic deployment model.</span></span> <span data-ttu-id="bf501-112">È anche possibile [informazioni su come una connessione Internet toocreate bilanciamento del carico con Azure Resource Manager](load-balancer-get-started-internet-arm-ps.md).</span><span class="sxs-lookup"><span data-stu-id="bf501-112">You can also [Learn how toocreate an Internet facing load balancer using Azure Resource Manager](load-balancer-get-started-internet-arm-ps.md).</span></span>

[!INCLUDE [load-balancer-get-started-internet-scenario-include.md](../../includes/load-balancer-get-started-internet-scenario-include.md)]

## <a name="set-up-load-balancer-using-powershell"></a><span data-ttu-id="bf501-113">Configurazione del servizio di bilanciamento del carico con PowerShell</span><span class="sxs-lookup"><span data-stu-id="bf501-113">Set up load balancer using PowerShell</span></span>

<span data-ttu-id="bf501-114">tooset di bilanciamento del carico tramite powershell, attenersi alla procedura hello:</span><span class="sxs-lookup"><span data-stu-id="bf501-114">tooset up a load balancer using powershell, follow hello steps below:</span></span>

1. <span data-ttu-id="bf501-115">Se non si è mai usato Azure PowerShell, vedere [come tooInstall e configurare Azure PowerShell](/powershell/azure/overview) e seguire le istruzioni di hello tutti hello modo toohello terminare toosign in Azure e selezionare la sottoscrizione.</span><span class="sxs-lookup"><span data-stu-id="bf501-115">If you have never used Azure PowerShell, see [How tooInstall and Configure Azure PowerShell](/powershell/azure/overview) and follow hello instructions all hello way toohello end toosign into Azure and select your subscription.</span></span>
2. <span data-ttu-id="bf501-116">Dopo aver creato una macchina virtuale, è possibile utilizzare i cmdlet di PowerShell tooadd una macchina virtuale di tooa del servizio di bilanciamento carico all'interno di hello stesso servizio cloud.</span><span class="sxs-lookup"><span data-stu-id="bf501-116">After creating a virtual machine, you can use PowerShell cmdlets tooadd a load balancer tooa virtual machine within hello same cloud service.</span></span>

<span data-ttu-id="bf501-117">In hello esempio seguente si aggiungerà un set di bilanciamento del carico chiamato toocloud "webfarm" computer "mytestcloud" (o myctestcloud.cloudapp.net), aggiunta di endpoint hello per hello toovirtual bilanciamento di carico del servizio denominato "web1" e "web2".</span><span class="sxs-lookup"><span data-stu-id="bf501-117">In hello following example you will add a load balancer set called "webfarm" toocloud service "mytestcloud" (or myctestcloud.cloudapp.net) , adding hello endpoints for hello load balancer toovirtual machines named "web1" and "web2".</span></span> <span data-ttu-id="bf501-118">servizio di bilanciamento del carico Hello riceve il traffico di rete sulla porta 80 e bilancia il carico tra le macchine virtuali hello definite da hello endpoint locale (in questo caso porta 80) tramite TCP.</span><span class="sxs-lookup"><span data-stu-id="bf501-118">hello load balancer receives network traffic on port 80 and load balances between hello virtual machines defined by hello local endpoint (in this case port 80) using TCP.</span></span>

### <a name="step-1"></a><span data-ttu-id="bf501-119">Passaggio 1</span><span class="sxs-lookup"><span data-stu-id="bf501-119">Step 1</span></span>

<span data-ttu-id="bf501-120">Creare un endpoint con carico bilanciato per web1"hello prima macchina virtuale"</span><span class="sxs-lookup"><span data-stu-id="bf501-120">Create a load balanced endpoint for hello first VM "web1"</span></span>

```powershell
Get-AzureVM -ServiceName "mytestcloud" -Name "web1" | Add-AzureEndpoint -Name "HttpIn" -Protocol "tcp" -PublicPort 80 -LocalPort 80 -LBSetName "WebFarm" -ProbePort 80 -ProbeProtocol "http" -ProbePath '/' | Update-AzureVM
```

### <a name="step-2"></a><span data-ttu-id="bf501-121">Passaggio 2</span><span class="sxs-lookup"><span data-stu-id="bf501-121">Step 2</span></span>

<span data-ttu-id="bf501-122">Creare un altro endpoint per hello secondo VM "web2" hello utilizzando stesso caricare il nome del set di bilanciamento del carico</span><span class="sxs-lookup"><span data-stu-id="bf501-122">Create another endpoint for hello second VM  "web2" using hello same load balancer set name</span></span>

```powershell
Get-AzureVM -ServiceName "mytestcloud" -Name "web2" | Add-AzureEndpoint -Name "HttpIn" -Protocol "tcp" -PublicPort 80 -LocalPort 80 -LBSetName "WebFarm" -ProbePort 80 -ProbeProtocol "http" -ProbePath '/' | Update-AzureVM
```

## <a name="remove-a-virtual-machine-from-a-load-balancer"></a><span data-ttu-id="bf501-123">Rimuovere una macchina virtuale dal servizio di bilanciamento del carico</span><span class="sxs-lookup"><span data-stu-id="bf501-123">Remove a virtual machine from a load balancer</span></span>

<span data-ttu-id="bf501-124">È possibile usare Remove-AzureEndpoint tooremove un endpoint della macchina virtuale dal servizio di bilanciamento del carico hello</span><span class="sxs-lookup"><span data-stu-id="bf501-124">You can use Remove-AzureEndpoint tooremove a virtual machine endpoint from hello load balancer</span></span>

```powershell
Get-azureVM -ServiceName mytestcloud  -Name web1 |Remove-AzureEndpoint -Name httpin | Update-AzureVM
```

## <a name="next-steps"></a><span data-ttu-id="bf501-125">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="bf501-125">Next steps</span></span>

<span data-ttu-id="bf501-126">È anche possibile [iniziare a creare un bilanciamento del carico interno](load-balancer-get-started-ilb-classic-ps.md) e configurare il tipo di [modalità di distribuzione](load-balancer-distribution-mode.md) per il comportamento del traffico di rete per un servizio di bilanciamento del carico specifico.</span><span class="sxs-lookup"><span data-stu-id="bf501-126">You can also [get started creating an internal load balancer](load-balancer-get-started-ilb-classic-ps.md) and configure what type of [distribution mode](load-balancer-distribution-mode.md) for a specific load balancer network traffic behavior.</span></span>

<span data-ttu-id="bf501-127">Se l'applicazione deve tookeep connessioni attive per i server di bilanciamento del carico, è possibile comprendere più su [impostazioni di timeout TCP per un servizio di bilanciamento del carico di inattività](load-balancer-tcp-idle-timeout.md).</span><span class="sxs-lookup"><span data-stu-id="bf501-127">If your application needs tookeep connections alive for servers behind a load balancer, you can understand more about [idle TCP timeout settings for a load balancer](load-balancer-tcp-idle-timeout.md).</span></span> <span data-ttu-id="bf501-128">Quando si utilizza Bilanciamento carico di Azure, questo risulterà utile toolearn sul comportamento di connessione inattiva.</span><span class="sxs-lookup"><span data-stu-id="bf501-128">It will help toolearn about idle connection behavior when you are using Azure Load Balancer.</span></span>

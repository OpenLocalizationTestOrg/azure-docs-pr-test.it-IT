---
title: aaaCommunity strumenti - Sposta le risorse classiche tooAzure Gestione risorse | Documenti Microsoft
description: "Questo strumento hello cataloghi di articolo che è state fornite da hello community toohelp eseguire la migrazione di risorse IaaS dal modello di distribuzione di gestione risorse di Azure classico toohello."
services: virtual-machines-windows
documentationcenter: 
author: singhkays
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 228b697b-3950-49f5-84bb-283bb56621b1
ms.service: virtual-machines-windows
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-windows
ms.devlang: na
ms.topic: article
ms.date: 03/30/2017
ms.author: kasing
ms.openlocfilehash: 67d5624a14d12a2d9eb46eb12aef461b706d4589
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="community-tools-toomigrate-iaas-resources-from-classic-tooazure-resource-manager"></a><span data-ttu-id="dcf40-103">Le risorse IaaS toomigrate da Gestione risorse di tooAzure classico degli strumenti della community</span><span class="sxs-lookup"><span data-stu-id="dcf40-103">Community tools toomigrate IaaS resources from classic tooAzure Resource Manager</span></span>
<span data-ttu-id="dcf40-104">Questo articolo cataloghi hello gli strumenti forniti da hello community tooassist con la migrazione di risorse IaaS dal modello di distribuzione di gestione risorse di Azure classico toohello.</span><span class="sxs-lookup"><span data-stu-id="dcf40-104">This article catalogs hello tools that have been provided by hello community tooassist with migration of IaaS resources from classic toohello Azure Resource Manager deployment model.</span></span>

> [!NOTE]
> <span data-ttu-id="dcf40-105">Questi strumenti non sono supportati ufficialmente dal Supporto tecnico Microsoft.</span><span class="sxs-lookup"><span data-stu-id="dcf40-105">These tools are not officially supported by Microsoft Support.</span></span> <span data-ttu-id="dcf40-106">Pertanto, sono aperti originato su GitHub e siamo le prenotazioni permanenti tooaccept lieta di correzioni o scenari aggiuntivi.</span><span class="sxs-lookup"><span data-stu-id="dcf40-106">Therefore they are open sourced on GitHub and we're happy tooaccept PRs for fixes or additional scenarios.</span></span> <span data-ttu-id="dcf40-107">tooreport un problema, utilizzare hello GitHub problemi di funzionalità.</span><span class="sxs-lookup"><span data-stu-id="dcf40-107">tooreport an issue, use hello GitHub issues feature.</span></span>
> 
> <span data-ttu-id="dcf40-108">La migrazione con questi strumenti comporta tempi di inattività della macchina virtuale classica.</span><span class="sxs-lookup"><span data-stu-id="dcf40-108">Migrating with these tools will cause downtime for your classic Virtual Machine.</span></span> <span data-ttu-id="dcf40-109">Se si è interessati a una modalità di migrazione supportata dalla piattaforma, vedere</span><span class="sxs-lookup"><span data-stu-id="dcf40-109">If you're looking for platform supported migration, visit</span></span> 
> 
>   * [<span data-ttu-id="dcf40-110">Piattaforma supportata la migrazione di risorse IaaS dallo stack di gestione risorse tooAzure classica</span><span class="sxs-lookup"><span data-stu-id="dcf40-110">Platform supported migration of IaaS resources from Classic tooAzure Resource Manager stack</span></span>](migration-classic-resource-manager-overview.md)
>   * [<span data-ttu-id="dcf40-111">Documentazione tecnica di informazioni approfondite su piattaforma supportata migrazione dalla versione classica tooAzure Gestione risorse</span><span class="sxs-lookup"><span data-stu-id="dcf40-111">Technical Deep Dive on Platform supported migration from Classic tooAzure Resource Manager</span></span>](migration-classic-resource-manager-deep-dive.md)
>   * [<span data-ttu-id="dcf40-112">Eseguire la migrazione di risorse IaaS da tooAzure classica gestore delle risorse con Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="dcf40-112">Migrate IaaS resources from Classic tooAzure Resource Manager using Azure PowerShell</span></span>](migration-classic-resource-manager-ps.md)
> 
> 

## <a name="asmmetadataparser"></a><span data-ttu-id="dcf40-113">AsmMetadataParser</span><span class="sxs-lookup"><span data-stu-id="dcf40-113">AsmMetadataParser</span></span>
<span data-ttu-id="dcf40-114">Si tratta di una raccolta di strumenti di supporto creato come parte della migrazione dell'organizzazione da tooAzure di gestione del servizio Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="dcf40-114">This is a collection of helper tools created as part of enterprise migrations from Azure Service Management tooAzure Resource Manager.</span></span> <span data-ttu-id="dcf40-115">Questo strumento consente tooreplicate dell'infrastruttura in un'altra sottoscrizione che può essere utilizzata per la verifica della migrazione e ferro gli eventuali problemi prima di eseguire la migrazione di hello nella sottoscrizione di produzione.</span><span class="sxs-lookup"><span data-stu-id="dcf40-115">This tool allows you tooreplicate your infrastructure into another subscription which can be used for testing migration and iron out any issues before running hello migration on your Production subscription.</span></span>

[<span data-ttu-id="dcf40-116">Documentazione dello strumento di collegamento toohello</span><span class="sxs-lookup"><span data-stu-id="dcf40-116">Link toohello tool documentation</span></span>](https://github.com/Azure/classic-iaas-resourcemanager-migration/tree/master/AsmToArmMigrationApiToolset)

## <a name="migaz"></a><span data-ttu-id="dcf40-117">migAz</span><span class="sxs-lookup"><span data-stu-id="dcf40-117">migAz</span></span>
<span data-ttu-id="dcf40-118">migAz è un toomigrate opzione aggiuntiva per un set completo di risorse di Resource Manager IaaS tooAzure IaaS risorse classiche.</span><span class="sxs-lookup"><span data-stu-id="dcf40-118">migAz is an additional option toomigrate a complete set of classic IaaS resources tooAzure Resource Manager IaaS resources.</span></span> <span data-ttu-id="dcf40-119">Hello migrazione può verificarsi all'interno di hello stessa sottoscrizione o tra diverse sottoscrizioni e i tipi di sottoscrizione (ad esempio: sottoscrizioni CSP).</span><span class="sxs-lookup"><span data-stu-id="dcf40-119">hello migration can occur within hello same subscription or between different subscriptions and subscription types (ex: CSP subscriptions).</span></span>

[<span data-ttu-id="dcf40-120">Documentazione dello strumento di collegamento toohello</span><span class="sxs-lookup"><span data-stu-id="dcf40-120">Link toohello tool documentation</span></span>](https://github.com/Azure/migAz)

## <a name="next-steps"></a><span data-ttu-id="dcf40-121">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="dcf40-121">Next Steps</span></span>

* [<span data-ttu-id="dcf40-122">Panoramica della migrazione supportata dalla piattaforma IaaS risorse tooAzure classico Gestione risorse di</span><span class="sxs-lookup"><span data-stu-id="dcf40-122">Overview of platform-supported migration of IaaS resources from classic tooAzure Resource Manager</span></span>](migration-classic-resource-manager-overview.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)
* [<span data-ttu-id="dcf40-123">Tecnica di informazioni approfondite su piattaforma supportata la migrazione da Gestione risorse di tooAzure classico</span><span class="sxs-lookup"><span data-stu-id="dcf40-123">Technical deep dive on platform-supported migration from classic tooAzure Resource Manager</span></span>](migration-classic-resource-manager-deep-dive.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)
* [<span data-ttu-id="dcf40-124">Pianificazione della migrazione delle risorse IaaS da Gestione risorse di tooAzure classico</span><span class="sxs-lookup"><span data-stu-id="dcf40-124">Planning for migration of IaaS resources from classic tooAzure Resource Manager</span></span>](migration-classic-resource-manager-plan.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)
* [<span data-ttu-id="dcf40-125">Utilizzare le risorse IaaS toomigrate PowerShell da Gestione risorse di tooAzure classico</span><span class="sxs-lookup"><span data-stu-id="dcf40-125">Use PowerShell toomigrate IaaS resources from classic tooAzure Resource Manager</span></span>](migration-classic-resource-manager-ps.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)
* [<span data-ttu-id="dcf40-126">Utilizzare le risorse IaaS toomigrate CLI da Gestione risorse di tooAzure classico</span><span class="sxs-lookup"><span data-stu-id="dcf40-126">Use CLI toomigrate IaaS resources from classic tooAzure Resource Manager</span></span>](../linux/migration-classic-resource-manager-cli.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)
* [<span data-ttu-id="dcf40-127">Rivedere gli errori di migrazione più comuni</span><span class="sxs-lookup"><span data-stu-id="dcf40-127">Review most common migration errors</span></span>](migration-classic-resource-manager-errors.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)
* [<span data-ttu-id="dcf40-128">Hello revisione più domande frequenti su IaaS la migrazione di risorse da Gestione risorse di tooAzure classico</span><span class="sxs-lookup"><span data-stu-id="dcf40-128">Review hello most frequently asked questions about migrating IaaS resources from classic tooAzure Resource Manager</span></span>](migration-classic-resource-manager-faq.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)


---
title: Strumenti della community - Spostare risorse classiche in Azure Resource Manager | Documentazione Microsoft
description: Questo articolo illustra gli strumenti forniti dalla community per semplificare la migrazione di risorse IaaS da un modello di distribuzione classica a un modello di distribuzione Azure Resource Manager.
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
ms.openlocfilehash: d3fc0246088eddeb345bea0ffbd2c5247b218006
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/03/2017
---
# <a name="community-tools-to-migrate-iaas-resources-from-classic-to-azure-resource-manager"></a><span data-ttu-id="acead-103">Strumenti della community per la migrazione delle risorse IaaS da un modello di distribuzione classica a un modello di distribuzione Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="acead-103">Community tools to migrate IaaS resources from classic to Azure Resource Manager</span></span>
<span data-ttu-id="acead-104">Questo articolo illustra gli strumenti forniti dalla community per supportare la migrazione di risorse IaaS da un modello di distribuzione classica a un modello di distribuzione Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="acead-104">This article catalogs the tools that have been provided by the community to assist with migration of IaaS resources from classic to the Azure Resource Manager deployment model.</span></span>

> [!NOTE]
> <span data-ttu-id="acead-105">Questi strumenti non sono supportati ufficialmente dal Supporto tecnico Microsoft.</span><span class="sxs-lookup"><span data-stu-id="acead-105">These tools are not officially supported by Microsoft Support.</span></span> <span data-ttu-id="acead-106">Sono quindi open source in GitHub e perciò sono graditi PR con suggerimenti per correzioni o altri scenari.</span><span class="sxs-lookup"><span data-stu-id="acead-106">Therefore they are open sourced on GitHub and we're happy to accept PRs for fixes or additional scenarios.</span></span> <span data-ttu-id="acead-107">Per segnalare un problema, usare l'apposita funzionalità GitHub.</span><span class="sxs-lookup"><span data-stu-id="acead-107">To report an issue, use the GitHub issues feature.</span></span>
> 
> <span data-ttu-id="acead-108">La migrazione con questi strumenti comporta tempi di inattività della macchina virtuale classica.</span><span class="sxs-lookup"><span data-stu-id="acead-108">Migrating with these tools will cause downtime for your classic Virtual Machine.</span></span> <span data-ttu-id="acead-109">Se si è interessati a una modalità di migrazione supportata dalla piattaforma, vedere</span><span class="sxs-lookup"><span data-stu-id="acead-109">If you're looking for platform supported migration, visit</span></span> 
> 
>   * [<span data-ttu-id="acead-110">Migrazione di risorse IaaS supportata dallo stack del modello di distribuzione classica ad Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="acead-110">Platform supported migration of IaaS resources from Classic to Azure Resource Manager stack</span></span>](migration-classic-resource-manager-overview.md)
>   * [<span data-ttu-id="acead-111">Approfondimento tecnico sulla migrazione supportata dalla piattaforma dal modello di distribuzione classica ad Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="acead-111">Technical Deep Dive on Platform supported migration from Classic to Azure Resource Manager</span></span>](migration-classic-resource-manager-deep-dive.md)
>   * [<span data-ttu-id="acead-112">Eseguire la migrazione di risorse IaaS dal modello di distribuzione classica ad Azure Resource Manager usando Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="acead-112">Migrate IaaS resources from Classic to Azure Resource Manager using Azure PowerShell</span></span>](migration-classic-resource-manager-ps.md)
> 
> 

## <a name="asmmetadataparser"></a><span data-ttu-id="acead-113">AsmMetadataParser</span><span class="sxs-lookup"><span data-stu-id="acead-113">AsmMetadataParser</span></span>
<span data-ttu-id="acead-114">Si tratta di una raccolta di strumenti di supporto creata come parte di migrazioni enterprise da Azure Service Management ad Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="acead-114">This is a collection of helper tools created as part of enterprise migrations from Azure Service Management to Azure Resource Manager.</span></span> <span data-ttu-id="acead-115">Questo strumento consente di replicare l'infrastruttura in un'altra sottoscrizione che può essere usata per testare la migrazione e risolvere eventuali problemi prima di eseguire la migrazione nella sottoscrizione di produzione.</span><span class="sxs-lookup"><span data-stu-id="acead-115">This tool allows you to replicate your infrastructure into another subscription which can be used for testing migration and iron out any issues before running the migration on your Production subscription.</span></span>

[<span data-ttu-id="acead-116">Collegamento alla documentazione dello strumento</span><span class="sxs-lookup"><span data-stu-id="acead-116">Link to the tool documentation</span></span>](https://github.com/Azure/classic-iaas-resourcemanager-migration/tree/master/AsmToArmMigrationApiToolset)

## <a name="migaz"></a><span data-ttu-id="acead-117">migAz</span><span class="sxs-lookup"><span data-stu-id="acead-117">migAz</span></span>
<span data-ttu-id="acead-118">migAz è un'opzione aggiuntiva che consente di eseguire la migrazione di un set completo di risorse IaaS classiche alle risorse IaaS di Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="acead-118">migAz is an additional option to migrate a complete set of classic IaaS resources to Azure Resource Manager IaaS resources.</span></span> <span data-ttu-id="acead-119">La migrazione può avvenire all'interno della stessa sottoscrizione o fra sottoscrizioni e tipi di sottoscrizione diversi (ad esempio: sottoscrizioni CSP).</span><span class="sxs-lookup"><span data-stu-id="acead-119">The migration can occur within the same subscription or between different subscriptions and subscription types (ex: CSP subscriptions).</span></span>

[<span data-ttu-id="acead-120">Collegamento alla documentazione dello strumento</span><span class="sxs-lookup"><span data-stu-id="acead-120">Link to the tool documentation</span></span>](https://github.com/Azure/migAz)

## <a name="next-steps"></a><span data-ttu-id="acead-121">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="acead-121">Next Steps</span></span>

* [<span data-ttu-id="acead-122">Panoramica sulla migrazione di risorse IaaS supportata dalla piattaforma dal modello di distribuzione classica al modello Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="acead-122">Overview of platform-supported migration of IaaS resources from classic to Azure Resource Manager</span></span>](migration-classic-resource-manager-overview.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)
* [<span data-ttu-id="acead-123">Approfondimento tecnico sulla migrazione supportata dalla piattaforma dal modello di distribuzione classica ad Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="acead-123">Technical deep dive on platform-supported migration from classic to Azure Resource Manager</span></span>](migration-classic-resource-manager-deep-dive.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)
* <span data-ttu-id="acead-124">[Planning for migration of IaaS resources from classic to Azure Resource Manager](migration-classic-resource-manager-plan.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) (Pianificazione della migrazione delle risorse IaaS dal modello di distribuzione classica al modello di distribuzione Azure Resource Manager)</span><span class="sxs-lookup"><span data-stu-id="acead-124">[Planning for migration of IaaS resources from classic to Azure Resource Manager](migration-classic-resource-manager-plan.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)</span></span>
* [<span data-ttu-id="acead-125">Usare PowerShell per eseguire la migrazione di risorse IaaS dal modello di distribuzione classica ad Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="acead-125">Use PowerShell to migrate IaaS resources from classic to Azure Resource Manager</span></span>](migration-classic-resource-manager-ps.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)
* [<span data-ttu-id="acead-126">Usare l'interfaccia della riga di comando per eseguire la migrazione di risorse IaaS dal modello di distribuzione classica ad Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="acead-126">Use CLI to migrate IaaS resources from classic to Azure Resource Manager</span></span>](../linux/migration-classic-resource-manager-cli.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)
* [<span data-ttu-id="acead-127">Rivedere gli errori di migrazione più comuni</span><span class="sxs-lookup"><span data-stu-id="acead-127">Review most common migration errors</span></span>](migration-classic-resource-manager-errors.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)
* [<span data-ttu-id="acead-128">Esaminare le domande frequenti sulla migrazione delle risorse IaaS dal modello di distribuzione classica ad Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="acead-128">Review the most frequently asked questions about migrating IaaS resources from classic to Azure Resource Manager</span></span>](migration-classic-resource-manager-faq.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)


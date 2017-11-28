---
title: aaaHow tootag una macchina virtuale Linux di Azure | Documenti Microsoft
description: Informazioni sull'uso dei tag di una macchina virtuale di Linux di Azure creata in Azure tramite il modello di distribuzione di gestione risorse di hello.
services: virtual-machines-linux
documentationcenter: 
author: mmccrory
manager: timlt
editor: tysonn
tags: azure-resource-manager
ms.assetid: ca0e17e5-d78e-42e6-9dad-c1e8f1c58027
ms.service: virtual-machines-linux
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure-services
ms.date: 02/28/2017
ms.author: memccror
ms.openlocfilehash: 456b226af4495c3b446cb79c99cf9494dde9fca5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="how-tootag-a-linux-virtual-machine-in-azure"></a><span data-ttu-id="e3b9e-103">Come tootag una macchina virtuale di Linux in Azure</span><span class="sxs-lookup"><span data-stu-id="e3b9e-103">How tootag a Linux virtual machine in Azure</span></span>
<span data-ttu-id="e3b9e-104">Questo articolo descrive diversi modi tootag una macchina virtuale di Linux in Azure tramite il modello di distribuzione del hello Gestione risorse.</span><span class="sxs-lookup"><span data-stu-id="e3b9e-104">This article describes different ways tootag a Linux virtual machine in Azure through hello Resource Manager deployment model.</span></span> <span data-ttu-id="e3b9e-105">I tag sono coppie chiave/valore definite dall'utente che possono essere inserite direttamente in una risorsa o un gruppo di risorse.</span><span class="sxs-lookup"><span data-stu-id="e3b9e-105">Tags are user-defined key/value pairs which can be placed directly on a resource or a resource group.</span></span> <span data-ttu-id="e3b9e-106">Azure supporta attualmente i tag too15 per ogni risorsa e gruppo di risorse.</span><span class="sxs-lookup"><span data-stu-id="e3b9e-106">Azure currently supports up too15 tags per resource and resource group.</span></span> <span data-ttu-id="e3b9e-107">Tag possono essere inseriti su una risorsa in fase di hello della creazione o aggiunta di risorse esistente tooan.</span><span class="sxs-lookup"><span data-stu-id="e3b9e-107">Tags may be placed on a resource at hello time of creation or added tooan existing resource.</span></span> <span data-ttu-id="e3b9e-108">Si noti, tag sono supportati per le risorse create tramite solo modello di distribuzione di gestione delle risorse hello.</span><span class="sxs-lookup"><span data-stu-id="e3b9e-108">Please note, tags are supported for resources created via hello Resource Manager deployment model only.</span></span>

[!INCLUDE [virtual-machines-common-tag](../../../includes/virtual-machines-common-tag.md)]

## <a name="tagging-with-azure-cli"></a><span data-ttu-id="e3b9e-109">Assegnazione di tag con Azure CLI</span><span class="sxs-lookup"><span data-stu-id="e3b9e-109">Tagging with Azure CLI</span></span>
<span data-ttu-id="e3b9e-110">toobegin, è necessario hello più recente [2.0 CLI di Azure (anteprima)](/cli/azure/install-az-cli2) installato e registrato con un account Azure tooan [accesso az](/cli/azure/#login).</span><span class="sxs-lookup"><span data-stu-id="e3b9e-110">toobegin, you need hello latest [Azure CLI 2.0 (Preview)](/cli/azure/install-az-cli2) installed and logged in tooan Azure account using [az login](/cli/azure/#login).</span></span>

<span data-ttu-id="e3b9e-111">È anche possibile eseguire questi passaggi con hello [CLI di Azure 1.0](tag-nodejs.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="e3b9e-111">You can also perform these steps with hello [Azure CLI 1.0](tag-nodejs.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>

<span data-ttu-id="e3b9e-112">È possibile visualizzare tutte le proprietà per una determinata macchina virtuale, inclusi tag hello, questo comando:</span><span class="sxs-lookup"><span data-stu-id="e3b9e-112">You can view all properties for a given Virtual Machine, including hello tags, using this command:</span></span>

        az vm show --resource-group MyResourceGroup --name MyTestVM

<span data-ttu-id="e3b9e-113">tooadd un nuovo tag VM tramite hello CLI di Azure, è possibile utilizzare hello `azure vm update` comando insieme al parametro tag hello **-impostare**:</span><span class="sxs-lookup"><span data-stu-id="e3b9e-113">tooadd a new VM tag through hello Azure CLI, you can use hello `azure vm update` command along with hello tag parameter **--set**:</span></span>

        az vm update --resource-group MyResourceGroup --name MyTestVM –-set tags.myNewTagName1=myNewTagValue1 tags.myNewTagName2=myNewTagValue2

<span data-ttu-id="e3b9e-114">tag tooremove, è possibile utilizzare hello **-rimuovere** parametro hello `azure vm update` comando.</span><span class="sxs-lookup"><span data-stu-id="e3b9e-114">tooremove tags, you can use hello **--remove** parameter in hello `azure vm update` command.</span></span>

        az vm update –-resource-group MyResourceGroup –-name MyTestVM --remove tags.myNewTagName1


<span data-ttu-id="e3b9e-115">Ora che sono applicati tag tooour risorse CLI di Azure e hello portale, esaminiamo un hello utilizzo dettagli toosee tag hello nel portale di fatturazione hello.</span><span class="sxs-lookup"><span data-stu-id="e3b9e-115">Now that we have applied tags tooour resources Azure CLI and hello Portal, let’s take a look at hello usage details toosee hello tags in hello billing portal.</span></span>

[!INCLUDE [virtual-machines-common-tag-usage](../../../includes/virtual-machines-common-tag-usage.md)]

## <a name="next-steps"></a><span data-ttu-id="e3b9e-116">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="e3b9e-116">Next steps</span></span>
* <span data-ttu-id="e3b9e-117">toolearn ulteriori informazioni sull'assegnazione di tag delle risorse di Azure, vedere [Panoramica di gestione risorse di Azure] [ Azure Resource Manager Overview] e [tooorganize tag usando le risorse di Azure] [ Using Tags tooorganize your Azure Resources].</span><span class="sxs-lookup"><span data-stu-id="e3b9e-117">toolearn more about tagging your Azure resources, see [Azure Resource Manager Overview][Azure Resource Manager Overview] and [Using Tags tooorganize your Azure Resources][Using Tags tooorganize your Azure Resources].</span></span>
* <span data-ttu-id="e3b9e-118">toosee come tag consentono di gestire l'utilizzo delle risorse di Azure, vedere [comprendere la fattura di Azure] [ Understanding your Azure Bill] e [ottenere informazioni approfondite del consumo di risorse di Microsoft Azure] [Gain insights into your Microsoft Azure resource consumption].</span><span class="sxs-lookup"><span data-stu-id="e3b9e-118">toosee how tags can help you manage your use of Azure resources, see [Understanding your Azure Bill][Understanding your Azure Bill] and [Gain insights into your Microsoft Azure resource consumption][Gain insights into your Microsoft Azure resource consumption].</span></span>

[Azure CLI environment]: ../../azure-resource-manager/xplat-cli-azure-resource-manager.md
[Azure Resource Manager Overview]: ../../azure-resource-manager/resource-group-overview.md
[Using Tags tooorganize your Azure Resources]: ../../azure-resource-manager/resource-group-using-tags.md
[Understanding your Azure Bill]: ../../billing/billing-understand-your-bill.md
[Gain insights into your Microsoft Azure resource consumption]: ../../billing/billing-usage-rate-card-overview.md

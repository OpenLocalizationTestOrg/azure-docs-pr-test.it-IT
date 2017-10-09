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
ms.openlocfilehash: 0e99ea66a87b7e00eb21a2f72dd2bce8673778dd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="how-tootag-a-linux-virtual-machine-in-azure"></a><span data-ttu-id="2b523-103">Come tootag una macchina virtuale di Linux in Azure</span><span class="sxs-lookup"><span data-stu-id="2b523-103">How tootag a Linux virtual machine in Azure</span></span>
<span data-ttu-id="2b523-104">Questo articolo descrive diversi modi tootag una macchina virtuale di Linux in Azure tramite il modello di distribuzione del hello Gestione risorse.</span><span class="sxs-lookup"><span data-stu-id="2b523-104">This article describes different ways tootag a Linux virtual machine in Azure through hello Resource Manager deployment model.</span></span> <span data-ttu-id="2b523-105">I tag sono coppie chiave/valore definite dall'utente che possono essere inserite direttamente in una risorsa o un gruppo di risorse.</span><span class="sxs-lookup"><span data-stu-id="2b523-105">Tags are user-defined key/value pairs which can be placed directly on a resource or a resource group.</span></span> <span data-ttu-id="2b523-106">Azure supporta attualmente i tag too15 per ogni risorsa e gruppo di risorse.</span><span class="sxs-lookup"><span data-stu-id="2b523-106">Azure currently supports up too15 tags per resource and resource group.</span></span> <span data-ttu-id="2b523-107">Tag possono essere inseriti su una risorsa in fase di hello della creazione o aggiunta di risorse esistente tooan.</span><span class="sxs-lookup"><span data-stu-id="2b523-107">Tags may be placed on a resource at hello time of creation or added tooan existing resource.</span></span> <span data-ttu-id="2b523-108">Si noti, tag sono supportati per le risorse create tramite solo modello di distribuzione di gestione delle risorse hello.</span><span class="sxs-lookup"><span data-stu-id="2b523-108">Please note, tags are supported for resources created via hello Resource Manager deployment model only.</span></span>

[!INCLUDE [virtual-machines-common-tag](../../../includes/virtual-machines-common-tag.md)]

## <a name="tagging-with-azure-cli"></a><span data-ttu-id="2b523-109">Assegnazione di tag con Azure CLI</span><span class="sxs-lookup"><span data-stu-id="2b523-109">Tagging with Azure CLI</span></span>
<span data-ttu-id="2b523-110">toobegin, [installare e configurare hello Azure CLI](../../xplat-cli-azure-resource-manager.md) e assicurarsi che si è in modalità di gestione risorse (`azure config mode arm`).</span><span class="sxs-lookup"><span data-stu-id="2b523-110">toobegin, [install and configure hello Azure CLI](../../xplat-cli-azure-resource-manager.md) and make sure you are in Resource Manager mode (`azure config mode arm`).</span></span>

<span data-ttu-id="2b523-111">È possibile visualizzare tutte le proprietà per una determinata macchina virtuale, inclusi tag hello, questo comando:</span><span class="sxs-lookup"><span data-stu-id="2b523-111">You can view all properties for a given Virtual Machine, including hello tags, using this command:</span></span>

        azure vm show -g MyResourceGroup -n MyTestVM

<span data-ttu-id="2b523-112">tooadd un nuovo tag VM tramite hello CLI di Azure, è possibile utilizzare hello `azure vm set` comando insieme al parametro tag hello **-t**:</span><span class="sxs-lookup"><span data-stu-id="2b523-112">tooadd a new VM tag through hello Azure CLI, you can use hello `azure vm set` command along with hello tag parameter **-t**:</span></span>

        azure vm set -g MyResourceGroup -n MyTestVM –t myNewTagName1=myNewTagValue1;myNewTagName2=myNewTagValue2

<span data-ttu-id="2b523-113">tooremove tutti i tag, è possibile utilizzare hello **– T** parametro hello `azure vm set` comando.</span><span class="sxs-lookup"><span data-stu-id="2b523-113">tooremove all tags, you can use hello **–T** parameter in hello `azure vm set` command.</span></span>

        azure vm set – g MyResourceGroup –n MyTestVM -T


<span data-ttu-id="2b523-114">Ora che sono applicati tag tooour risorse CLI di Azure e hello portale, esaminiamo un hello utilizzo dettagli toosee tag hello nel portale di fatturazione hello.</span><span class="sxs-lookup"><span data-stu-id="2b523-114">Now that we have applied tags tooour resources Azure CLI and hello Portal, let’s take a look at hello usage details toosee hello tags in hello billing portal.</span></span>

[!INCLUDE [virtual-machines-common-tag-usage](../../../includes/virtual-machines-common-tag-usage.md)]

## <a name="next-steps"></a><span data-ttu-id="2b523-115">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="2b523-115">Next steps</span></span>
* <span data-ttu-id="2b523-116">toolearn ulteriori informazioni sull'assegnazione di tag delle risorse di Azure, vedere [Panoramica di gestione risorse di Azure] [ Azure Resource Manager Overview] e [tooorganize tag usando le risorse di Azure] [ Using Tags tooorganize your Azure Resources].</span><span class="sxs-lookup"><span data-stu-id="2b523-116">toolearn more about tagging your Azure resources, see [Azure Resource Manager Overview][Azure Resource Manager Overview] and [Using Tags tooorganize your Azure Resources][Using Tags tooorganize your Azure Resources].</span></span>
* <span data-ttu-id="2b523-117">toosee come tag consentono di gestire l'utilizzo delle risorse di Azure, vedere [comprendere la fattura di Azure] [ Understanding your Azure Bill] e [ottenere informazioni approfondite del consumo di risorse di Microsoft Azure] [Gain insights into your Microsoft Azure resource consumption].</span><span class="sxs-lookup"><span data-stu-id="2b523-117">toosee how tags can help you manage your use of Azure resources, see [Understanding your Azure Bill][Understanding your Azure Bill] and [Gain insights into your Microsoft Azure resource consumption][Gain insights into your Microsoft Azure resource consumption].</span></span>

[Azure CLI environment]: ../../azure-resource-manager/xplat-cli-azure-resource-manager.md
[Azure Resource Manager Overview]: ../../azure-resource-manager/resource-group-overview.md
[Using Tags tooorganize your Azure Resources]: ../../azure-resource-manager/resource-group-using-tags.md
[Understanding your Azure Bill]: ../../billing/billing-understand-your-bill.md
[Gain insights into your Microsoft Azure resource consumption]: ../../billing/billing-usage-rate-card-overview.md

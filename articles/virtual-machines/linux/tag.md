---
title: Come assegnare un tag a una macchina virtuale Linux in Azure | Microsoft Docs
description: Informazioni sull'assegnazione di tag a una macchina virtuale Linux creata in Azure con il modello di distribuzione di Resource Manager.
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
ms.openlocfilehash: da3ff0de2a5d6ac8994b7c16b758f976228a53b0
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="how-to-tag-a-linux-virtual-machine-in-azure"></a><span data-ttu-id="97b02-103">Come contrassegnare una macchina virtuale Linux in Azure</span><span class="sxs-lookup"><span data-stu-id="97b02-103">How to tag a Linux virtual machine in Azure</span></span>
<span data-ttu-id="97b02-104">Questo articolo descrive diversi modi per contrassegnare una macchina virtuale Linux in Azure tramite il modello di distribuzione Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="97b02-104">This article describes different ways to tag a Linux virtual machine in Azure through the Resource Manager deployment model.</span></span> <span data-ttu-id="97b02-105">I tag sono coppie chiave/valore definite dall'utente che possono essere inserite direttamente in una risorsa o un gruppo di risorse.</span><span class="sxs-lookup"><span data-stu-id="97b02-105">Tags are user-defined key/value pairs which can be placed directly on a resource or a resource group.</span></span> <span data-ttu-id="97b02-106">Attualmente, Azure supporta fino a 15 tag per ogni risorsa e gruppo di risorse.</span><span class="sxs-lookup"><span data-stu-id="97b02-106">Azure currently supports up to 15 tags per resource and resource group.</span></span> <span data-ttu-id="97b02-107">I tag possono essere posizionati su una risorsa al momento della creazione o aggiunti a una risorsa esistente.</span><span class="sxs-lookup"><span data-stu-id="97b02-107">Tags may be placed on a resource at the time of creation or added to an existing resource.</span></span> <span data-ttu-id="97b02-108">Si noti che i tag sono supportati solo per le risorse create tramite il modello di distribuzione Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="97b02-108">Please note, tags are supported for resources created via the Resource Manager deployment model only.</span></span>

[!INCLUDE [virtual-machines-common-tag](../../../includes/virtual-machines-common-tag.md)]

## <a name="tagging-with-azure-cli"></a><span data-ttu-id="97b02-109">Assegnazione di tag con Azure CLI</span><span class="sxs-lookup"><span data-stu-id="97b02-109">Tagging with Azure CLI</span></span>
<span data-ttu-id="97b02-110">Innanzitutto, è necessario aver installato la versione più recente dell'[interfaccia della riga di comando di Azure 2.0 (Anteprima)](/cli/azure/install-az-cli2) e aver effettuato l'accesso a un account Azure con il comando [az login](/cli/azure/#login).</span><span class="sxs-lookup"><span data-stu-id="97b02-110">To begin, you need the latest [Azure CLI 2.0 (Preview)](/cli/azure/install-az-cli2) installed and logged in to an Azure account using [az login](/cli/azure/#login).</span></span>

<span data-ttu-id="97b02-111">È possibile anche eseguire questi passaggi tramite l'[interfaccia della riga di comando di Azure 1.0](tag-nodejs.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="97b02-111">You can also perform these steps with the [Azure CLI 1.0](tag-nodejs.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>

<span data-ttu-id="97b02-112">È possibile visualizzare tutte le proprietà per una determinata macchina virtuale, compresi i tag, utilizzando questo comando:</span><span class="sxs-lookup"><span data-stu-id="97b02-112">You can view all properties for a given Virtual Machine, including the tags, using this command:</span></span>

        az vm show --resource-group MyResourceGroup --name MyTestVM

<span data-ttu-id="97b02-113">Per aggiungere un nuovo tag della macchina virtuale tramite l'interfaccia della riga di comando di Azure, è possibile utilizzare il comando `azure vm update` insieme al parametro tag **--set**:</span><span class="sxs-lookup"><span data-stu-id="97b02-113">To add a new VM tag through the Azure CLI, you can use the `azure vm update` command along with the tag parameter **--set**:</span></span>

        az vm update --resource-group MyResourceGroup --name MyTestVM –-set tags.myNewTagName1=myNewTagValue1 tags.myNewTagName2=myNewTagValue2

<span data-ttu-id="97b02-114">Per rimuovere i tag, è possibile usare il parametro **--remove** nel comando `azure vm update`.</span><span class="sxs-lookup"><span data-stu-id="97b02-114">To remove tags, you can use the **--remove** parameter in the `azure vm update` command.</span></span>

        az vm update –-resource-group MyResourceGroup –-name MyTestVM --remove tags.myNewTagName1


<span data-ttu-id="97b02-115">Dopo aver applicato i tag alle risorse tramite l'interfaccia della riga di comando di Azure e il portale, esaminare i dettagli di utilizzo per visualizzare i tag nel portale di fatturazione.</span><span class="sxs-lookup"><span data-stu-id="97b02-115">Now that we have applied tags to our resources Azure CLI and the Portal, let’s take a look at the usage details to see the tags in the billing portal.</span></span>

[!INCLUDE [virtual-machines-common-tag-usage](../../../includes/virtual-machines-common-tag-usage.md)]

## <a name="next-steps"></a><span data-ttu-id="97b02-116">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="97b02-116">Next steps</span></span>
* <span data-ttu-id="97b02-117">Per altre informazioni sull'uso dei tag nelle risorse di Azure, vedere [Panoramica di Azure Resource Manager][Azure Resource Manager Overview] e [Uso dei tag per organizzare le risorse di Azure][Using Tags to organize your Azure Resources].</span><span class="sxs-lookup"><span data-stu-id="97b02-117">To learn more about tagging your Azure resources, see [Azure Resource Manager Overview][Azure Resource Manager Overview] and [Using Tags to organize your Azure Resources][Using Tags to organize your Azure Resources].</span></span>
* <span data-ttu-id="97b02-118">Per informazioni sull'utilità dei tag nella gestione dell'uso delle risorse di Azure, vedere [Informazioni sulla fattura di Azure][Understanding your Azure Bill] e [Ottenere informazioni dettagliate sul consumo di risorse di Microsoft Azure][Gain insights into your Microsoft Azure resource consumption].</span><span class="sxs-lookup"><span data-stu-id="97b02-118">To see how tags can help you manage your use of Azure resources, see [Understanding your Azure Bill][Understanding your Azure Bill] and [Gain insights into your Microsoft Azure resource consumption][Gain insights into your Microsoft Azure resource consumption].</span></span>

[Azure CLI environment]: ../../azure-resource-manager/xplat-cli-azure-resource-manager.md
[Azure Resource Manager Overview]: ../../azure-resource-manager/resource-group-overview.md
[Using Tags to organize your Azure Resources]: ../../azure-resource-manager/resource-group-using-tags.md
[Understanding your Azure Bill]: ../../billing/billing-understand-your-bill.md
[Gain insights into your Microsoft Azure resource consumption]: ../../billing/billing-usage-rate-card-overview.md

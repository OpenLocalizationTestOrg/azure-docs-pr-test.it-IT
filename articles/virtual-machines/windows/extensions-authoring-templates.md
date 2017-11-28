---
title: Creazione di modelli con le estensioni di VM Windows | Microsoft Docs
description: Informazioni sulla creazione di modelli Azure Resource Manager con le estensioni per VM Windows
services: virtual-machines-windows
documentationcenter: 
author: kundanap
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 418dd1f7-ded8-45ab-9a5a-a59d245e2555
ms.service: virtual-machines-windows
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: infrastructure-services
ms.date: 03/29/2016
ms.author: kundanap
ms.openlocfilehash: 338668df33783d8ef62c6710f4d96ce805296fe5
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="authoring-azure-resource-manager-templates-with-windows-vm-extensions"></a><span data-ttu-id="0ef90-103">Creazione di modelli Azure Resource Manager con le estensioni di VM Windows</span><span class="sxs-lookup"><span data-stu-id="0ef90-103">Authoring Azure Resource Manager templates with Windows VM extensions</span></span>
[!INCLUDE [virtual-machines-common-extensions-authoring-templates](../../../includes/virtual-machines-common-extensions-authoring-templates.md)]

<span data-ttu-id="0ef90-104">Eseguire il cmdlet seguente di Azure PowerShell da Azure PowerShell:</span><span class="sxs-lookup"><span data-stu-id="0ef90-104">From Azure PowerShell, run the following Azure PowerShell cmdlet:</span></span>

      Get-AzureVMAvailableExtension


<span data-ttu-id="0ef90-105">Questo cmdlet restituisce il nome dell'autore, il nome dell'estensione e la versione come segue:</span><span class="sxs-lookup"><span data-stu-id="0ef90-105">This cmdlet returns the publisher name, extension name, and version as follows:</span></span>

      Publisher                   : Microsoft.Azure.Extensions  
      ExtensionName               : DockerExtension
      Version                     : 1.0

<span data-ttu-id="0ef90-106">Queste tre proprietà vengono mappate rispettivamente a "publisher", "type" e "typeHandlerVersion" nel frammento di modello precedente.</span><span class="sxs-lookup"><span data-stu-id="0ef90-106">These three properties map to "publisher", "type", and "typeHandlerVersion" respectively in the above template snippet.</span></span>

> [!NOTE]
> <span data-ttu-id="0ef90-107">È sempre consigliabile usare la versione più recente dell'estensione per ottenere la funzionalità più aggiornata.</span><span class="sxs-lookup"><span data-stu-id="0ef90-107">It's always recommended to use the latest extension version to get the most updated functionality.</span></span>
> 
> 

## <a name="identifying-the-schema-for-the-extension-configuration-parameters"></a><span data-ttu-id="0ef90-108">Identificazione dello schema per i parametri di configurazione dell'estensione</span><span class="sxs-lookup"><span data-stu-id="0ef90-108">Identifying the schema for the extension configuration parameters</span></span>
<span data-ttu-id="0ef90-109">Il passaggio successivo per la creazione di un modello di estensione consiste nell'identificare il formato per indicare i parametri di configurazione.</span><span class="sxs-lookup"><span data-stu-id="0ef90-109">The next step with authoring an extension template is to identify the format for providing configuration parameters.</span></span> <span data-ttu-id="0ef90-110">Ogni estensione supporta il proprio set di parametri.</span><span class="sxs-lookup"><span data-stu-id="0ef90-110">Each extension supports its own set of parameters.</span></span>

<span data-ttu-id="0ef90-111">Per visualizzare una configurazione di esempio per le estensioni Windows, vedere [Esempi di estensioni Windows](extensions-configuration-samples.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="0ef90-111">To look at sample configurations for Windows extensions, see [Windows extensions samples](extensions-configuration-samples.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>

<span data-ttu-id="0ef90-112">Fare riferimento a quanto segue per ottenere un modello completo con estensioni di VM.</span><span class="sxs-lookup"><span data-stu-id="0ef90-112">Please refer to the following to get a fully complete template with VM extensions.</span></span>

[<span data-ttu-id="0ef90-113">Estensione di script personalizzato in una macchina virtuale Windows</span><span class="sxs-lookup"><span data-stu-id="0ef90-113">Custom Script Extension on a Windows VM</span></span>](https://github.com/Azure/azure-quickstart-templates/blob/b1908e74259da56a92800cace97350af1f1fc32b/201-list-storage-keys-windows-vm/azuredeploy.json/)

<span data-ttu-id="0ef90-114">Dopo aver creato il modello, è possibile distribuirlo usando Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="0ef90-114">After authoring the template, you can deploy it using Azure PowerShell.</span></span>


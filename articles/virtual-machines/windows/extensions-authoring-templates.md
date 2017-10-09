---
title: aaaAuthoring modelli con le estensioni di macchina virtuale di Windows | Documenti Microsoft
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
ms.openlocfilehash: c5156cb3859f7ff86bebda942150d268e57d6486
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="authoring-azure-resource-manager-templates-with-windows-vm-extensions"></a><span data-ttu-id="43b13-103">Creazione di modelli Azure Resource Manager con le estensioni di VM Windows</span><span class="sxs-lookup"><span data-stu-id="43b13-103">Authoring Azure Resource Manager templates with Windows VM extensions</span></span>
[!INCLUDE [virtual-machines-common-extensions-authoring-templates](../../../includes/virtual-machines-common-extensions-authoring-templates.md)]

<span data-ttu-id="43b13-104">Da Azure PowerShell, eseguire hello cmdlet di Azure PowerShell seguente:</span><span class="sxs-lookup"><span data-stu-id="43b13-104">From Azure PowerShell, run hello following Azure PowerShell cmdlet:</span></span>

      Get-AzureVMAvailableExtension


<span data-ttu-id="43b13-105">Questo cmdlet restituisce il nome di server di pubblicazione hello, nome di estensione e versione come indicato di seguito:</span><span class="sxs-lookup"><span data-stu-id="43b13-105">This cmdlet returns hello publisher name, extension name, and version as follows:</span></span>

      Publisher                   : Microsoft.Azure.Extensions  
      ExtensionName               : DockerExtension
      Version                     : 1.0

<span data-ttu-id="43b13-106">Mapping di queste tre proprietà troppo "publisher", "type" e "typeHandlerVersion" rispettivamente in hello sopra il frammento di modello.</span><span class="sxs-lookup"><span data-stu-id="43b13-106">These three properties map too"publisher", "type", and "typeHandlerVersion" respectively in hello above template snippet.</span></span>

> [!NOTE]
> <span data-ttu-id="43b13-107">È sempre consigliato toouse hello più recente versione tooget hello aggiornato più funzionalità dell'estensione.</span><span class="sxs-lookup"><span data-stu-id="43b13-107">It's always recommended toouse hello latest extension version tooget hello most updated functionality.</span></span>
> 
> 

## <a name="identifying-hello-schema-for-hello-extension-configuration-parameters"></a><span data-ttu-id="43b13-108">Identificazione dello schema di hello per i parametri di configurazione di estensione hello</span><span class="sxs-lookup"><span data-stu-id="43b13-108">Identifying hello schema for hello extension configuration parameters</span></span>
<span data-ttu-id="43b13-109">passaggio successivo di Hello alla creazione di un modello di estensione è formato hello tooidentify per fornire i parametri di configurazione.</span><span class="sxs-lookup"><span data-stu-id="43b13-109">hello next step with authoring an extension template is tooidentify hello format for providing configuration parameters.</span></span> <span data-ttu-id="43b13-110">Ogni estensione supporta il proprio set di parametri.</span><span class="sxs-lookup"><span data-stu-id="43b13-110">Each extension supports its own set of parameters.</span></span>

<span data-ttu-id="43b13-111">toolook in configurazioni di esempio per le estensioni di Windows, vedere [degli esempi di estensioni Windows](extensions-configuration-samples.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="43b13-111">toolook at sample configurations for Windows extensions, see [Windows extensions samples](extensions-configuration-samples.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>

<span data-ttu-id="43b13-112">Consultare toohello seguente tooget un modello completato con le estensioni VM.</span><span class="sxs-lookup"><span data-stu-id="43b13-112">Please refer toohello following tooget a fully complete template with VM extensions.</span></span>

[<span data-ttu-id="43b13-113">Estensione di script personalizzato in una macchina virtuale Windows</span><span class="sxs-lookup"><span data-stu-id="43b13-113">Custom Script Extension on a Windows VM</span></span>](https://github.com/Azure/azure-quickstart-templates/blob/b1908e74259da56a92800cace97350af1f1fc32b/201-list-storage-keys-windows-vm/azuredeploy.json/)

<span data-ttu-id="43b13-114">Una volta creato il modello di hello, è possibile distribuire usando Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="43b13-114">After authoring hello template, you can deploy it using Azure PowerShell.</span></span>


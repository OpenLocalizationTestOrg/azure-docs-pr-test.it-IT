---
title: modelli aaaAuthoring con le estensioni VM Linux | Documenti Microsoft
description: Informazioni sulla creazione di modelli di Azure Resource Manager con le estensioni per VM Linux
services: virtual-machines-linux
documentationcenter: 
author: kundanap
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 322f8f0b-6697-4acb-b5f3-b3f58d28358b
ms.service: virtual-machines-linux
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure-services
ms.date: 03/29/2016
ms.author: kundanap
ms.openlocfilehash: b797e442d8706956bbc06c5be611a2b0119055d3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="authoring-azure-resource-manager-templates-with-linux-vm-extensions"></a><span data-ttu-id="bf2fc-103">Creazione di modelli di Azure Resource Manager con le estensioni di VM Linux</span><span class="sxs-lookup"><span data-stu-id="bf2fc-103">Authoring Azure Resource Manager templates with Linux VM extensions</span></span>
[!INCLUDE [virtual-machines-common-extensions-authoring-templates](../../../includes/virtual-machines-common-extensions-authoring-templates.md)]

<span data-ttu-id="bf2fc-104">Dall'interfaccia CLI di Azure, eseguire hello seguente comando:</span><span class="sxs-lookup"><span data-stu-id="bf2fc-104">From Azure CLI, run hello following commnad:</span></span>

      Azure VM extension list

<span data-ttu-id="bf2fc-105">Questo comando restituisce il nome server di pubblicazione hello, nome dell'estensione e versione come riportato di seguito:</span><span class="sxs-lookup"><span data-stu-id="bf2fc-105">This command returns hello publisher name, extension name and version as following:</span></span>

      Publisher                   : Microsoft.Azure.Extensions  
      ExtensionName               : DockerExtension
      Version                     : 1.0

<span data-ttu-id="bf2fc-106">Mapping di queste tre proprietà troppo "publisher", "type" e "typeHandlerVersion" rispettivamente in hello sopra il frammento di modello.</span><span class="sxs-lookup"><span data-stu-id="bf2fc-106">These three properties map too"publisher", "type", and "typeHandlerVersion" respectively in hello above template snippet.</span></span>

> [!NOTE]
> <span data-ttu-id="bf2fc-107">È sempre consigliato toouse hello più recente versione tooget hello aggiornato più funzionalità dell'estensione.</span><span class="sxs-lookup"><span data-stu-id="bf2fc-107">It's always recommended toouse hello latest extension version tooget hello most updated functionality.</span></span>
> 
> 

## <a name="identifying-hello-schema-for-hello-extension-configuration-parameters"></a><span data-ttu-id="bf2fc-108">Identificazione dello schema di hello per i parametri di configurazione di estensione hello</span><span class="sxs-lookup"><span data-stu-id="bf2fc-108">Identifying hello schema for hello extension configuration parameters</span></span>
<span data-ttu-id="bf2fc-109">passaggio successivo di Hello alla creazione di un modello di estensione è formato hello tooidentify per fornire i parametri di configurazione.</span><span class="sxs-lookup"><span data-stu-id="bf2fc-109">hello next step with authoring an extension template is tooidentify hello format for providing configuration parameters.</span></span> <span data-ttu-id="bf2fc-110">Ogni estensione supporta il proprio set di parametri.</span><span class="sxs-lookup"><span data-stu-id="bf2fc-110">Each extension supports its own set of parameters.</span></span>

<span data-ttu-id="bf2fc-111">toolook in configurazioni di esempio per le estensioni di Linux, fare clic su documentazione hello per vedere [Linux eExtensions esempi](extensions-configuration-samples.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="bf2fc-111">toolook at sample configurations for Linux extensions, click hello documentation for see [Linux eExtensions samples](extensions-configuration-samples.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>

<span data-ttu-id="bf2fc-112">Consultare toohello seguente tooget un modello completato con le estensioni VM.</span><span class="sxs-lookup"><span data-stu-id="bf2fc-112">Please refer toohello following tooget a fully complete template with VM Extensions.</span></span>

[<span data-ttu-id="bf2fc-113">Estensione di script personalizzato in una VM Linux</span><span class="sxs-lookup"><span data-stu-id="bf2fc-113">Custom script extension on a Linux VM</span></span>](https://github.com/Azure/azure-quickstart-templates/blob/b1908e74259da56a92800cace97350af1f1fc32b/mongodb-on-ubuntu/azuredeploy.json/)

<span data-ttu-id="bf2fc-114">Una volta creato il modello di hello, è possibile distribuirlo utilizzando hello CLI di Azure.</span><span class="sxs-lookup"><span data-stu-id="bf2fc-114">After authoring hello template, you can deploy it using hello Azure CLI.</span></span>


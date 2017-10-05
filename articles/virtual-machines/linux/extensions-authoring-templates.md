---
title: Creazione di modelli con le estensioni di VM Linux | Microsoft Docs
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
ms.openlocfilehash: 8b017306474670bf8dde1440128e16ec35146f24
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="authoring-azure-resource-manager-templates-with-linux-vm-extensions"></a><span data-ttu-id="fb45b-103">Creazione di modelli di Azure Resource Manager con le estensioni di VM Linux</span><span class="sxs-lookup"><span data-stu-id="fb45b-103">Authoring Azure Resource Manager templates with Linux VM extensions</span></span>
[!INCLUDE [virtual-machines-common-extensions-authoring-templates](../../../includes/virtual-machines-common-extensions-authoring-templates.md)]

<span data-ttu-id="fb45b-104">Eseguire il comando seguente dall'interfaccia della riga di comando di Azure:</span><span class="sxs-lookup"><span data-stu-id="fb45b-104">From Azure CLI, run the following commnad:</span></span>

      Azure VM extension list

<span data-ttu-id="fb45b-105">Questo comando restituisce il nome dell'autore, il nome dell'estensione e la versione come segue:</span><span class="sxs-lookup"><span data-stu-id="fb45b-105">This command returns the publisher name, extension name and version as following:</span></span>

      Publisher                   : Microsoft.Azure.Extensions  
      ExtensionName               : DockerExtension
      Version                     : 1.0

<span data-ttu-id="fb45b-106">Queste tre proprietà vengono mappate rispettivamente a "publisher", "type" e "typeHandlerVersion" nel frammento di modello precedente.</span><span class="sxs-lookup"><span data-stu-id="fb45b-106">These three properties map to "publisher", "type", and "typeHandlerVersion" respectively in the above template snippet.</span></span>

> [!NOTE]
> <span data-ttu-id="fb45b-107">È sempre consigliabile usare la versione più recente dell'estensione per ottenere la funzionalità più aggiornata.</span><span class="sxs-lookup"><span data-stu-id="fb45b-107">It's always recommended to use the latest extension version to get the most updated functionality.</span></span>
> 
> 

## <a name="identifying-the-schema-for-the-extension-configuration-parameters"></a><span data-ttu-id="fb45b-108">Identificazione dello schema per i parametri di configurazione dell'estensione</span><span class="sxs-lookup"><span data-stu-id="fb45b-108">Identifying the schema for the extension configuration parameters</span></span>
<span data-ttu-id="fb45b-109">Il passaggio successivo per la creazione di un modello di estensione consiste nell'identificare il formato per indicare i parametri di configurazione.</span><span class="sxs-lookup"><span data-stu-id="fb45b-109">The next step with authoring an extension template is to identify the format for providing configuration parameters.</span></span> <span data-ttu-id="fb45b-110">Ogni estensione supporta il proprio set di parametri.</span><span class="sxs-lookup"><span data-stu-id="fb45b-110">Each extension supports its own set of parameters.</span></span>

<span data-ttu-id="fb45b-111">Per visualizzare configurazioni di esempio per le estensioni Linux, fare clic sulla documentazione sugli [Esempi di configurazione dell'estensione delle macchine virtuali Linux](extensions-configuration-samples.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="fb45b-111">To look at sample configurations for Linux extensions, click the documentation for see [Linux eExtensions samples](extensions-configuration-samples.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>

<span data-ttu-id="fb45b-112">Vedere quanto segue per ottenere un modello completo con estensioni di VM.</span><span class="sxs-lookup"><span data-stu-id="fb45b-112">Please refer to the following to get a fully complete template with VM Extensions.</span></span>

[<span data-ttu-id="fb45b-113">Estensione di script personalizzato in una VM Linux</span><span class="sxs-lookup"><span data-stu-id="fb45b-113">Custom script extension on a Linux VM</span></span>](https://github.com/Azure/azure-quickstart-templates/blob/b1908e74259da56a92800cace97350af1f1fc32b/mongodb-on-ubuntu/azuredeploy.json/)

<span data-ttu-id="fb45b-114">Dopo aver creato il modello, è possibile distribuirlo usando l'interfaccia della riga di comando di Azure.</span><span class="sxs-lookup"><span data-stu-id="fb45b-114">After authoring the template, you can deploy it using the Azure CLI.</span></span>


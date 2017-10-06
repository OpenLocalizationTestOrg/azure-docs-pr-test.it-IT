---
title: aaaSet di insieme di credenziali chiave per le macchine virtuali Linux con hello Azure CLI 1.0 | Documenti Microsoft
description: Come tooset di insieme di credenziali chiave per l'utilizzo con una macchina virtuale di gestione risorse di Azure con hello Azure CLI 1.0.
services: virtual-machines-linux
documentationcenter: 
author: singhkays
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: bccdd5ab-5ccf-4760-9039-92c6eafb15bd
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.topic: article
ms.date: 02/24/2017
ms.author: singhkay
ms.openlocfilehash: 275022e4e7e26d7363784c289dd7512047c07bad
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="set-up-key-vault-for-virtual-machines-in-azure-resource-manager-with-hello-azure-cli-10"></a><span data-ttu-id="f4234-103">Impostare la chiave dell'insieme di credenziali per le macchine virtuali in Gestione risorse di Azure con hello Azure CLI 1.0</span><span class="sxs-lookup"><span data-stu-id="f4234-103">Set up Key Vault for virtual machines in Azure Resource Manager with hello Azure CLI 1.0</span></span>
<span data-ttu-id="f4234-104">Nello stack di gestione risorse di Azure hello, segreti/certificati vengono modellati come risorse fornite dal provider di risorse hello dell'insieme di credenziali chiave.</span><span class="sxs-lookup"><span data-stu-id="f4234-104">In hello Azure Resource Manager stack, secrets/certificates are modeled as resources that are provided by hello resource provider of Key Vault.</span></span> <span data-ttu-id="f4234-105">toolearn ulteriori informazioni sull'insieme di credenziali chiave di Azure, vedere [che cos'è l'insieme di credenziali chiave di Azure?](../../key-vault/key-vault-whatis.md)</span><span class="sxs-lookup"><span data-stu-id="f4234-105">toolearn more about Azure Key Vault, see [What is Azure Key Vault?](../../key-vault/key-vault-whatis.md)</span></span> <span data-ttu-id="f4234-106">Affinché toobe insieme di credenziali chiave utilizzato con le macchine virtuali di Azure Resource Manager, hello *EnabledForDeployment* in insieme di credenziali chiave deve essere impostata tootrue.</span><span class="sxs-lookup"><span data-stu-id="f4234-106">In order for Key Vault toobe used with Azure Resource Manager virtual machines, hello *EnabledForDeployment* property on Key Vault must be set tootrue.</span></span> <span data-ttu-id="f4234-107">È possibile farlo in vari tipi di client.</span><span class="sxs-lookup"><span data-stu-id="f4234-107">You can do this in various clients.</span></span> <span data-ttu-id="f4234-108">In questo articolo illustra come tooset di insieme di credenziali chiave per l'utilizzo con macchine virtuali di Azure.</span><span class="sxs-lookup"><span data-stu-id="f4234-108">This article shows you how tooset up Key Vault for use with Azure Virtual Machines.</span></span>

## <a name="cli-versions-toocomplete-hello-task"></a><span data-ttu-id="f4234-109">Attività hello toocomplete versioni CLI</span><span class="sxs-lookup"><span data-stu-id="f4234-109">CLI versions toocomplete hello task</span></span>
<span data-ttu-id="f4234-110">È possibile eseguire attività di hello tramite una delle seguenti versioni CLI hello</span><span class="sxs-lookup"><span data-stu-id="f4234-110">You can complete hello task using one of hello following CLI versions</span></span>

- <span data-ttu-id="f4234-111">[Azure CLI 1.0](#quick-commands) : l'interfaccia CLI per hello classic risorse Gestione modelli di distribuzione e (in questo articolo)</span><span class="sxs-lookup"><span data-stu-id="f4234-111">[Azure CLI 1.0](#quick-commands) – our CLI for hello classic and resource management deployment models (this article)</span></span>
- <span data-ttu-id="f4234-112">[Azure CLI 2.0](../windows/key-vault-setup.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) -la prossima generazione CLI per modello di distribuzione di gestione risorse hello</span><span class="sxs-lookup"><span data-stu-id="f4234-112">[Azure CLI 2.0](../windows/key-vault-setup.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) - our next generation CLI for hello resource management deployment model</span></span>

## <a name="use-cli-10-tooset-up-key-vault"></a><span data-ttu-id="f4234-113">Utilizzare tooset 1.0 CLI di insieme di credenziali chiave</span><span class="sxs-lookup"><span data-stu-id="f4234-113">Use CLI 1.0 tooset up Key Vault</span></span>
<span data-ttu-id="f4234-114">toocreate un insieme di credenziali chiave tramite l'interfaccia della riga di comando hello (CLI), vedere [gestire insieme di credenziali chiave usando CLI](../../key-vault/key-vault-manage-with-cli2.md#create-a-key-vault).</span><span class="sxs-lookup"><span data-stu-id="f4234-114">toocreate a key vault by using hello command-line interface (CLI), see [Manage Key Vault using CLI](../../key-vault/key-vault-manage-with-cli2.md#create-a-key-vault).</span></span>

<span data-ttu-id="f4234-115">CLI 1.0, è possibile insieme di credenziali chiave hello toocreate prima di assegnare il criterio di distribuzione hello.</span><span class="sxs-lookup"><span data-stu-id="f4234-115">For CLI 1.0, you have toocreate hello key vault before you assign hello deployment policy.</span></span> <span data-ttu-id="f4234-116">È quindi possibile assegnare criteri hello utilizzando hello comando seguente:</span><span class="sxs-lookup"><span data-stu-id="f4234-116">You can then assign hello policy by using hello following command:</span></span>

    azure keyvault set-policy ContosoKeyVault –enabled-for-deployment true

## <a name="use-templates-tooset-up-key-vault"></a><span data-ttu-id="f4234-117">Utilizzare tooset di modelli di insieme di credenziali chiave</span><span class="sxs-lookup"><span data-stu-id="f4234-117">Use templates tooset up Key Vault</span></span>
<span data-ttu-id="f4234-118">Quando si utilizza un modello, è necessario hello tooset `enabledForDeployment` proprietà troppo`true` per hello risorsa insieme di credenziali chiave.</span><span class="sxs-lookup"><span data-stu-id="f4234-118">When you use a template, you need tooset hello `enabledForDeployment` property too`true` for hello Key Vault resource.</span></span>

    {
      "type": "Microsoft.KeyVault/vaults",
      "name": "ContosoKeyVault",
      "apiVersion": "2015-06-01",
      "location": "<location-of-key-vault>",
      "properties": {
        "enabledForDeployment": "true",
        ....
        ....
      }
    }

<span data-ttu-id="f4234-119">Per altre opzioni che è possibile configurare quando si crea un insieme di credenziali delle chiavi utilizzando i modelli, vedere l'articolo su come [creare un insieme di credenziali delle chiavi](https://azure.microsoft.com/documentation/templates/101-key-vault-create/).</span><span class="sxs-lookup"><span data-stu-id="f4234-119">For other options that you can configure when you create a key vault by using templates, see [Create a key vault](https://azure.microsoft.com/documentation/templates/101-key-vault-create/).</span></span>

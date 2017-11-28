---
title: aaaSet di chiave dell'insieme di credenziali per le macchine virtuali Windows Azure Resource Manager | Documenti Microsoft
description: Come tooset di insieme di credenziali chiave per l'utilizzo con una macchina virtuale di Azure Resource Manager.
services: virtual-machines-windows
documentationcenter: 
author: singhkays
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 33a483e2-cfbc-4c62-a588-5d9fd52491e2
ms.service: virtual-machines-windows
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-windows
ms.devlang: na
ms.topic: article
ms.date: 01/24/2017
ms.author: kasing
ms.openlocfilehash: 53bbe90708202ecfdcf754822d04bf2469631f08
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="set-up-key-vault-for-virtual-machines-in-azure-resource-manager"></a><span data-ttu-id="d2d85-103">Configurare l'insieme di credenziali delle chiavi per le macchine virtuali in Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="d2d85-103">Set up Key Vault for virtual machines in Azure Resource Manager</span></span>

[!INCLUDE [learn-about-deployment-models](../../../includes/learn-about-deployment-models-rm-include.md)]

<span data-ttu-id="d2d85-104">Nello stack di gestione risorse di Azure, i segreti/certificati vengono modellati come risorse fornite dal provider di risorse hello dell'insieme di credenziali chiave.</span><span class="sxs-lookup"><span data-stu-id="d2d85-104">In Azure Resource Manager stack, secrets/certificates are modeled as resources that are provided by hello resource provider of Key Vault.</span></span> <span data-ttu-id="d2d85-105">toolearn ulteriori informazioni sull'insieme di credenziali chiave, vedere [che cos'è l'insieme di credenziali chiave di Azure?](../../key-vault/key-vault-whatis.md)</span><span class="sxs-lookup"><span data-stu-id="d2d85-105">toolearn more about Key Vault, see [What is Azure Key Vault?](../../key-vault/key-vault-whatis.md)</span></span>

> [!NOTE]
> 1. <span data-ttu-id="d2d85-106">Affinché toobe insieme di credenziali chiave utilizzato con le macchine virtuali di Azure Resource Manager, hello **EnabledForDeployment** in insieme di credenziali chiave deve essere impostata tootrue.</span><span class="sxs-lookup"><span data-stu-id="d2d85-106">In order for Key Vault toobe used with Azure Resource Manager virtual machines, hello **EnabledForDeployment** property on Key Vault must be set tootrue.</span></span> <span data-ttu-id="d2d85-107">È possibile farlo in vari tipi di client.</span><span class="sxs-lookup"><span data-stu-id="d2d85-107">You can do this in various clients.</span></span>
> 2. <span data-ttu-id="d2d85-108">esigenze di insieme di credenziali chiave Hello toobe creato in hello stessa sottoscrizione e posizione come hello macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="d2d85-108">hello Key Vault needs toobe created in hello same subscription and location as hello Virtual Machine.</span></span>
>
>

## <a name="use-powershell-tooset-up-key-vault"></a><span data-ttu-id="d2d85-109">Utilizzare PowerShell tooset backup insieme di credenziali chiave</span><span class="sxs-lookup"><span data-stu-id="d2d85-109">Use PowerShell tooset up Key Vault</span></span>
<span data-ttu-id="d2d85-110">toocreate un insieme di credenziali chiave usando PowerShell, vedere [introduzione insieme credenziali chiavi Azure](../../key-vault/key-vault-get-started.md#vault).</span><span class="sxs-lookup"><span data-stu-id="d2d85-110">toocreate a key vault by using PowerShell, see [Get started with Azure Key Vault](../../key-vault/key-vault-get-started.md#vault).</span></span>

<span data-ttu-id="d2d85-111">Per i nuovi insiemi di credenziali delle chiavi, è possibile usare questo cmdlet di PowerShell:</span><span class="sxs-lookup"><span data-stu-id="d2d85-111">For new key vaults, you can use this PowerShell cmdlet:</span></span>

    New-AzureRmKeyVault -VaultName 'ContosoKeyVault' -ResourceGroupName 'ContosoResourceGroup' -Location 'East Asia' -EnabledForDeployment

<span data-ttu-id="d2d85-112">Per gli insiemi di credenziali delle chiavi esistenti, è possibile usare questo cmdlet di PowerShell:</span><span class="sxs-lookup"><span data-stu-id="d2d85-112">For existing key vaults, you can use this PowerShell cmdlet:</span></span>

    Set-AzureRmKeyVaultAccessPolicy -VaultName 'ContosoKeyVault' -EnabledForDeployment

## <a name="us-cli-tooset-up-key-vault"></a><span data-ttu-id="d2d85-113">Ci CLI tooset backup insieme di credenziali chiave</span><span class="sxs-lookup"><span data-stu-id="d2d85-113">Us CLI tooset up Key Vault</span></span>
<span data-ttu-id="d2d85-114">toocreate un insieme di credenziali chiave tramite l'interfaccia della riga di comando hello (CLI), vedere [gestire insieme di credenziali chiave usando CLI](../../key-vault/key-vault-manage-with-cli2.md#create-a-key-vault).</span><span class="sxs-lookup"><span data-stu-id="d2d85-114">toocreate a key vault by using hello command-line interface (CLI), see [Manage Key Vault using CLI](../../key-vault/key-vault-manage-with-cli2.md#create-a-key-vault).</span></span>

<span data-ttu-id="d2d85-115">CLI, è possibile insieme di credenziali chiave hello toocreate prima di assegnare il criterio di distribuzione hello.</span><span class="sxs-lookup"><span data-stu-id="d2d85-115">For CLI, you have toocreate hello key vault before you assign hello deployment policy.</span></span> <span data-ttu-id="d2d85-116">È possibile farlo tramite hello comando seguente:</span><span class="sxs-lookup"><span data-stu-id="d2d85-116">You can do this by using hello following command:</span></span>

    azure keyvault set-policy ContosoKeyVault –enabled-for-deployment true

## <a name="use-templates-tooset-up-key-vault"></a><span data-ttu-id="d2d85-117">Utilizzare tooset di modelli di insieme di credenziali chiave</span><span class="sxs-lookup"><span data-stu-id="d2d85-117">Use templates tooset up Key Vault</span></span>
<span data-ttu-id="d2d85-118">Mentre si utilizza un modello, è necessario hello tooset `enabledForDeployment` proprietà troppo`true` per hello risorsa insieme di credenziali chiave.</span><span class="sxs-lookup"><span data-stu-id="d2d85-118">While you use a template, you need tooset hello `enabledForDeployment` property too`true` for hello Key Vault resource.</span></span>

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

<span data-ttu-id="d2d85-119">Per altre opzioni che è possibile configurare quando si crea un insieme di credenziali delle chiavi utilizzando i modelli, vedere l'articolo su come [creare un insieme di credenziali delle chiavi](https://azure.microsoft.com/documentation/templates/101-key-vault-create/).</span><span class="sxs-lookup"><span data-stu-id="d2d85-119">For other options that you can configure when you create a key vault by using templates, see [Create a key vault](https://azure.microsoft.com/documentation/templates/101-key-vault-create/).</span></span>

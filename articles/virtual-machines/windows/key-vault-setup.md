---
title: Configurare Key Vault per macchine virtuali Windows in Azure Resource Manager | Documentazione Microsoft
description: Come configurare un insieme di credenziali delle chiavi da usare con una macchina virtuale di Azure Resource Manager.
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
ms.openlocfilehash: a5083a5216efbfd76fd912ec48c2f0ec3b30c4a1
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="set-up-key-vault-for-virtual-machines-in-azure-resource-manager"></a><span data-ttu-id="6d9a7-103">Configurare l'insieme di credenziali delle chiavi per le macchine virtuali in Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="6d9a7-103">Set up Key Vault for virtual machines in Azure Resource Manager</span></span>

[!INCLUDE [learn-about-deployment-models](../../../includes/learn-about-deployment-models-rm-include.md)]

<span data-ttu-id="6d9a7-104">In Azure Resource Manager gli stack, i segreti e i certificati vengono modellati come risorse fornite dal provider di risorse dell'insieme di credenziali delle chiavi.</span><span class="sxs-lookup"><span data-stu-id="6d9a7-104">In Azure Resource Manager stack, secrets/certificates are modeled as resources that are provided by the resource provider of Key Vault.</span></span> <span data-ttu-id="6d9a7-105">Per altre informazioni sugli insiemi di credenziali delle chiavi, vedere [Informazioni sull'insieme di credenziali delle chiavi di Azure](../../key-vault/key-vault-whatis.md)</span><span class="sxs-lookup"><span data-stu-id="6d9a7-105">To learn more about Key Vault, see [What is Azure Key Vault?](../../key-vault/key-vault-whatis.md)</span></span>

> [!NOTE]
> 1. <span data-ttu-id="6d9a7-106">Per consentire l'uso dell'insieme di credenziali delle chiavi con le macchine virtuali di Azure Resource Manager, è necessario impostare su true la proprietà **EnabledForDeployment** nell'insieme di credenziali delle chiavi.</span><span class="sxs-lookup"><span data-stu-id="6d9a7-106">In order for Key Vault to be used with Azure Resource Manager virtual machines, the **EnabledForDeployment** property on Key Vault must be set to true.</span></span> <span data-ttu-id="6d9a7-107">È possibile farlo in vari tipi di client.</span><span class="sxs-lookup"><span data-stu-id="6d9a7-107">You can do this in various clients.</span></span>
> 2. <span data-ttu-id="6d9a7-108">È necessario creare l'insieme di credenziali delle chiavi nella stessa sottoscrizione e nello stesso percorso della macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="6d9a7-108">The Key Vault needs to be created in the same subscription and location as the Virtual Machine.</span></span>
>
>

## <a name="use-powershell-to-set-up-key-vault"></a><span data-ttu-id="6d9a7-109">Utilizzare PowerShell per configurare l'insieme di credenziali delle chiavi</span><span class="sxs-lookup"><span data-stu-id="6d9a7-109">Use PowerShell to set up Key Vault</span></span>
<span data-ttu-id="6d9a7-110">Per creare un insieme di credenziali delle chiavi usando PowerShell, vedere [Introduzione all'insieme di credenziali delle chiavi di Azure](../../key-vault/key-vault-get-started.md#vault).</span><span class="sxs-lookup"><span data-stu-id="6d9a7-110">To create a key vault by using PowerShell, see [Get started with Azure Key Vault](../../key-vault/key-vault-get-started.md#vault).</span></span>

<span data-ttu-id="6d9a7-111">Per i nuovi insiemi di credenziali delle chiavi, è possibile usare questo cmdlet di PowerShell:</span><span class="sxs-lookup"><span data-stu-id="6d9a7-111">For new key vaults, you can use this PowerShell cmdlet:</span></span>

    New-AzureRmKeyVault -VaultName 'ContosoKeyVault' -ResourceGroupName 'ContosoResourceGroup' -Location 'East Asia' -EnabledForDeployment

<span data-ttu-id="6d9a7-112">Per gli insiemi di credenziali delle chiavi esistenti, è possibile usare questo cmdlet di PowerShell:</span><span class="sxs-lookup"><span data-stu-id="6d9a7-112">For existing key vaults, you can use this PowerShell cmdlet:</span></span>

    Set-AzureRmKeyVaultAccessPolicy -VaultName 'ContosoKeyVault' -EnabledForDeployment

## <a name="us-cli-to-set-up-key-vault"></a><span data-ttu-id="6d9a7-113">Usare l'interfaccia della riga di comando per impostare l'insieme di credenziali delle chiavi</span><span class="sxs-lookup"><span data-stu-id="6d9a7-113">Us CLI to set up Key Vault</span></span>
<span data-ttu-id="6d9a7-114">Per creare un insieme di credenziali delle chiavi usando l'interfaccia della riga di comando (CLI), vedere l'articolo su come [gestire l'insieme di credenziali delle chiavi tramite l'interfaccia della riga di comando](../../key-vault/key-vault-manage-with-cli2.md#create-a-key-vault).</span><span class="sxs-lookup"><span data-stu-id="6d9a7-114">To create a key vault by using the command-line interface (CLI), see [Manage Key Vault using CLI](../../key-vault/key-vault-manage-with-cli2.md#create-a-key-vault).</span></span>

<span data-ttu-id="6d9a7-115">Per l'interfaccia della riga di comando, prima di assegnare i criteri di distribuzione è necessario creare l'insieme di credenziali delle chiavi.</span><span class="sxs-lookup"><span data-stu-id="6d9a7-115">For CLI, you have to create the key vault before you assign the deployment policy.</span></span> <span data-ttu-id="6d9a7-116">A questo scopo, è possibile eseguire questo comando:</span><span class="sxs-lookup"><span data-stu-id="6d9a7-116">You can do this by using the following command:</span></span>

    azure keyvault set-policy ContosoKeyVault –enabled-for-deployment true

## <a name="use-templates-to-set-up-key-vault"></a><span data-ttu-id="6d9a7-117">Utilizzare modelli per configurare l'insieme di credenziali delle chiavi</span><span class="sxs-lookup"><span data-stu-id="6d9a7-117">Use templates to set up Key Vault</span></span>
<span data-ttu-id="6d9a7-118">Se si usa un modello, è necessario impostare la proprietà `enabledForDeployment` su `true` per la risorsa dell'insieme di credenziali delle chiavi.</span><span class="sxs-lookup"><span data-stu-id="6d9a7-118">While you use a template, you need to set the `enabledForDeployment` property to `true` for the Key Vault resource.</span></span>

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

<span data-ttu-id="6d9a7-119">Per altre opzioni che è possibile configurare quando si crea un insieme di credenziali delle chiavi utilizzando i modelli, vedere l'articolo su come [creare un insieme di credenziali delle chiavi](https://azure.microsoft.com/documentation/templates/101-key-vault-create/).</span><span class="sxs-lookup"><span data-stu-id="6d9a7-119">For other options that you can configure when you create a key vault by using templates, see [Create a key vault](https://azure.microsoft.com/documentation/templates/101-key-vault-create/).</span></span>

---
title: Configurare l'insieme di credenziali delle chiavi per macchine virtuali Linux con l'interfaccia della riga di comando 1.0 di Azure | Documentazione Microsoft
description: Come configurare un insieme di credenziali delle chiavi da usare con una macchina virtuale di Azure Resource Manager con l'interfaccia della riga di comando 1.0 di Azure.
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
ms.openlocfilehash: fed612a354d45f34619f2a66bd40d78740c43ac7
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="set-up-key-vault-for-virtual-machines-in-azure-resource-manager-with-the-azure-cli-10"></a><span data-ttu-id="80e40-103">Configurare l'insieme di credenziali delle chiavi per le macchine virtuali in Azure Resource Manager con l'interfaccia della riga di comando 1.0 di Azure</span><span class="sxs-lookup"><span data-stu-id="80e40-103">Set up Key Vault for virtual machines in Azure Resource Manager with the Azure CLI 1.0</span></span>
<span data-ttu-id="80e40-104">In Azure Resource Manager gli stack, i segreti e i certificati vengono modellati come risorse fornite dal provider di risorse dell'insieme di credenziali delle chiavi.</span><span class="sxs-lookup"><span data-stu-id="80e40-104">In the Azure Resource Manager stack, secrets/certificates are modeled as resources that are provided by the resource provider of Key Vault.</span></span> <span data-ttu-id="80e40-105">Per altre informazioni sugli insiemi di credenziali delle chiavi di Azure, vedere [Informazioni sull'insieme di credenziali delle chiavi di Azure](../../key-vault/key-vault-whatis.md)</span><span class="sxs-lookup"><span data-stu-id="80e40-105">To learn more about Azure Key Vault, see [What is Azure Key Vault?](../../key-vault/key-vault-whatis.md)</span></span> <span data-ttu-id="80e40-106">Per consentire l'uso dell'insieme di credenziali delle chiavi con le macchine virtuali di Azure Resource Manager, è necessario impostare su true la proprietà *EnabledForDeployment* nell'insieme di credenziali delle chiavi.</span><span class="sxs-lookup"><span data-stu-id="80e40-106">In order for Key Vault to be used with Azure Resource Manager virtual machines, the *EnabledForDeployment* property on Key Vault must be set to true.</span></span> <span data-ttu-id="80e40-107">È possibile farlo in vari tipi di client.</span><span class="sxs-lookup"><span data-stu-id="80e40-107">You can do this in various clients.</span></span> <span data-ttu-id="80e40-108">Questo articolo descrive come configurare un insieme di credenziali delle chiavi da usare con le macchine virtuali di Azure.</span><span class="sxs-lookup"><span data-stu-id="80e40-108">This article shows you how to set up Key Vault for use with Azure Virtual Machines.</span></span>

## <a name="cli-versions-to-complete-the-task"></a><span data-ttu-id="80e40-109">Versioni dell'interfaccia della riga di comando per completare l'attività</span><span class="sxs-lookup"><span data-stu-id="80e40-109">CLI versions to complete the task</span></span>
<span data-ttu-id="80e40-110">È possibile completare l'attività usando una delle versioni seguenti dell'interfaccia della riga di comando</span><span class="sxs-lookup"><span data-stu-id="80e40-110">You can complete the task using one of the following CLI versions</span></span>

- <span data-ttu-id="80e40-111">[Interfaccia della riga di comando di Azure 1.0](#quick-commands): l'interfaccia della riga di comando per i modelli di distribuzione classica e di gestione delle risorse (questo articolo)</span><span class="sxs-lookup"><span data-stu-id="80e40-111">[Azure CLI 1.0](#quick-commands) – our CLI for the classic and resource management deployment models (this article)</span></span>
- <span data-ttu-id="80e40-112">[Interfaccia della riga di comando di Azure 2.0](../windows/key-vault-setup.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json): interfaccia avanzata per il modello di distribuzione di gestione delle risorse</span><span class="sxs-lookup"><span data-stu-id="80e40-112">[Azure CLI 2.0](../windows/key-vault-setup.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) - our next generation CLI for the resource management deployment model</span></span>

## <a name="use-cli-10-to-set-up-key-vault"></a><span data-ttu-id="80e40-113">Usare l'interfaccia della riga di comando 1.0 per impostare l'insieme di credenziali delle chiavi</span><span class="sxs-lookup"><span data-stu-id="80e40-113">Use CLI 1.0 to set up Key Vault</span></span>
<span data-ttu-id="80e40-114">Per creare un insieme di credenziali delle chiavi usando l'interfaccia della riga di comando (CLI), vedere l'articolo su come [gestire l'insieme di credenziali delle chiavi tramite l'interfaccia della riga di comando](../../key-vault/key-vault-manage-with-cli2.md#create-a-key-vault).</span><span class="sxs-lookup"><span data-stu-id="80e40-114">To create a key vault by using the command-line interface (CLI), see [Manage Key Vault using CLI](../../key-vault/key-vault-manage-with-cli2.md#create-a-key-vault).</span></span>

<span data-ttu-id="80e40-115">Per l'interfaccia della riga di comando 1.0, prima di assegnare il criterio di distribuzione è necessario creare l'insieme di credenziali delle chiavi.</span><span class="sxs-lookup"><span data-stu-id="80e40-115">For CLI 1.0, you have to create the key vault before you assign the deployment policy.</span></span> <span data-ttu-id="80e40-116">È quindi possibile assegnare il criterio usando il comando seguente:</span><span class="sxs-lookup"><span data-stu-id="80e40-116">You can then assign the policy by using the following command:</span></span>

    azure keyvault set-policy ContosoKeyVault –enabled-for-deployment true

## <a name="use-templates-to-set-up-key-vault"></a><span data-ttu-id="80e40-117">Utilizzare modelli per configurare l'insieme di credenziali delle chiavi</span><span class="sxs-lookup"><span data-stu-id="80e40-117">Use templates to set up Key Vault</span></span>
<span data-ttu-id="80e40-118">Se si usa un modello, è necessario impostare la proprietà `enabledForDeployment` su `true` per la risorsa dell'insieme di credenziali delle chiavi.</span><span class="sxs-lookup"><span data-stu-id="80e40-118">When you use a template, you need to set the `enabledForDeployment` property to `true` for the Key Vault resource.</span></span>

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

<span data-ttu-id="80e40-119">Per altre opzioni che è possibile configurare quando si crea un insieme di credenziali delle chiavi utilizzando i modelli, vedere l'articolo su come [creare un insieme di credenziali delle chiavi](https://azure.microsoft.com/documentation/templates/101-key-vault-create/).</span><span class="sxs-lookup"><span data-stu-id="80e40-119">For other options that you can configure when you create a key vault by using templates, see [Create a key vault](https://azure.microsoft.com/documentation/templates/101-key-vault-create/).</span></span>

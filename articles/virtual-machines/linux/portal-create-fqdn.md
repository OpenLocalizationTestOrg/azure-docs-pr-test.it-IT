---
title: Creare un nome di dominio completo (FQDN) per una macchina virtuale Linux nel portale di Azure | Microsoft Docs
description: Informazioni su come creare un nome di dominio completo o FQDN per un Gestore risorse basato su macchina virtuale nel portale di Azure.
services: virtual-machines-linux
documentationcenter: 
author: iainfoulds
manager: timlt
editor: tysonn
tags: azure-resource-manager
ms.assetid: 2cd6c249-a737-4a0a-b5ba-e1c09e551b30
ms.service: virtual-machines-linux
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure-services
ms.date: 07/05/2017
ms.author: iainfou
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 49bfec791fcca3feabc4eb280cefd7faada0ea31
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="create-a-fully-qualified-domain-name-in-the-azure-portal-for-a-linux-vm"></a><span data-ttu-id="a6177-103">Creare un nome di dominio completo nel portale di Azure per una macchina virtuale Linux</span><span class="sxs-lookup"><span data-stu-id="a6177-103">Create a fully qualified domain name in the Azure portal for a Linux VM</span></span>

<span data-ttu-id="a6177-104">Quando si crea una macchina virtuale nel [portale di Azure](https://portal.azure.com), il portale crea automaticamente una risorsa IP pubblica per la macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="a6177-104">When you create a virtual machine (VM) in the [Azure portal](https://portal.azure.com), a public IP resource for the virtual machine is automatically created.</span></span> <span data-ttu-id="a6177-105">Usare questo indirizzo IP per accedere in remoto alla VM.</span><span class="sxs-lookup"><span data-stu-id="a6177-105">You use this IP address to remotely access the VM.</span></span> <span data-ttu-id="a6177-106">Anche se il portale non crea un [nome di dominio completo](https://en.wikipedia.org/wiki/Fully_qualified_domain_name), o FQDN (Fully Qualified Domain Name), è possibile aggiungerne uno dopo aver creato la VM.</span><span class="sxs-lookup"><span data-stu-id="a6177-106">Although the portal does not create a [fully qualified domain name](https://en.wikipedia.org/wiki/Fully_qualified_domain_name), or FQDN, you can add one once the VM is created.</span></span> <span data-ttu-id="a6177-107">Questo articolo illustra i passaggi per creare un nome DNS o un FQDN.</span><span class="sxs-lookup"><span data-stu-id="a6177-107">This article demonstrates the steps to create a DNS name or FQDN.</span></span>

## <a name="create-a-fqdn"></a><span data-ttu-id="a6177-108">Creare un nome di dominio completo</span><span class="sxs-lookup"><span data-stu-id="a6177-108">Create a FQDN</span></span>
<span data-ttu-id="a6177-109">In questo articolo si presuppone che sia già stata creata una VM.</span><span class="sxs-lookup"><span data-stu-id="a6177-109">This article assumes that you have already created a VM.</span></span> <span data-ttu-id="a6177-110">Se necessario, è possibile [creare una macchina virtuale nel portale](quick-create-portal.md) o [con l'interfaccia della riga di comando di Azure](quick-create-cli.md).</span><span class="sxs-lookup"><span data-stu-id="a6177-110">If needed, you can [create a VM in the portal](quick-create-portal.md) or [with the Azure CLI](quick-create-cli.md).</span></span> <span data-ttu-id="a6177-111">Dopo che la macchina virtuale è operativa, seguire questi passaggi:</span><span class="sxs-lookup"><span data-stu-id="a6177-111">Follow these steps once your VM is up and running:</span></span>

[!INCLUDE [virtual-machines-common-portal-create-fqdn](../../../includes/virtual-machines-common-portal-create-fqdn.md)]

<span data-ttu-id="a6177-112">È ora possibile connettersi in modalità remota alla macchina virtuale usando questo nome DNS, ad esempio `ssh azureuser@mydns.westus.cloudapp.azure.com`.</span><span class="sxs-lookup"><span data-stu-id="a6177-112">You can now connect remotely to the VM using this DNS name such as with `ssh azureuser@mydns.westus.cloudapp.azure.com`.</span></span>

## <a name="next-steps"></a><span data-ttu-id="a6177-113">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="a6177-113">Next steps</span></span>
<span data-ttu-id="a6177-114">Quando la macchina virtuale ha un indirizzo IP pubblico e un nome DNS, è possibile distribuire framework applicazioni o servizi comuni, ad esempio nginx, MongoDB, Docker e così via.</span><span class="sxs-lookup"><span data-stu-id="a6177-114">Now that your VM has a public IP and DNS name, you can deploy common application frameworks or services such as nginx, MongoDB, Docker, etc.</span></span>

<span data-ttu-id="a6177-115">Per suggerimenti sulla creazione di distribuzioni di Azure, vedere la pagina relativa all'[uso di Azure Resource Manager](../../azure-resource-manager/resource-group-overview.md).</span><span class="sxs-lookup"><span data-stu-id="a6177-115">You can also read more about [using Resource Manager](../../azure-resource-manager/resource-group-overview.md) for tips on building your Azure deployments.</span></span>


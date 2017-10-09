---
title: nome di dominio completo per una VM Linux nel portale di Azure hello aaaCreate | Documenti Microsoft
description: Informazioni su come toocreate un nome di dominio completo o nome di dominio completo per un gestore di risorse basato su macchina virtuale nel portale di Azure hello.
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
ms.openlocfilehash: 1494a0cb1caa62069c72096a739aee111ac8b383
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-fully-qualified-domain-name-in-hello-azure-portal-for-a-linux-vm"></a><span data-ttu-id="f75b5-103">Creare un nome di dominio completo nel portale di Azure hello per una VM Linux</span><span class="sxs-lookup"><span data-stu-id="f75b5-103">Create a fully qualified domain name in hello Azure portal for a Linux VM</span></span>

<span data-ttu-id="f75b5-104">Quando si crea una macchina virtuale (VM) in hello [portale di Azure](https://portal.azure.com), viene creata automaticamente una risorsa IP pubblica per la macchina virtuale hello.</span><span class="sxs-lookup"><span data-stu-id="f75b5-104">When you create a virtual machine (VM) in hello [Azure portal](https://portal.azure.com), a public IP resource for hello virtual machine is automatically created.</span></span> <span data-ttu-id="f75b5-105">Utilizzare questo hello di accesso tooremotely indirizzo IP VM.</span><span class="sxs-lookup"><span data-stu-id="f75b5-105">You use this IP address tooremotely access hello VM.</span></span> <span data-ttu-id="f75b5-106">Anche se il portale di hello non crea un [nome di dominio completo](https://en.wikipedia.org/wiki/Fully_qualified_domain_name), o nome di dominio completo, è possibile aggiungere uno dopo hello viene creata la VM.</span><span class="sxs-lookup"><span data-stu-id="f75b5-106">Although hello portal does not create a [fully qualified domain name](https://en.wikipedia.org/wiki/Fully_qualified_domain_name), or FQDN, you can add one once hello VM is created.</span></span> <span data-ttu-id="f75b5-107">Questo articolo illustra hello passaggi toocreate un nome DNS o il nome FQDN.</span><span class="sxs-lookup"><span data-stu-id="f75b5-107">This article demonstrates hello steps toocreate a DNS name or FQDN.</span></span>

## <a name="create-a-fqdn"></a><span data-ttu-id="f75b5-108">Creare un nome di dominio completo</span><span class="sxs-lookup"><span data-stu-id="f75b5-108">Create a FQDN</span></span>
<span data-ttu-id="f75b5-109">In questo articolo si presuppone che sia già stata creata una VM.</span><span class="sxs-lookup"><span data-stu-id="f75b5-109">This article assumes that you have already created a VM.</span></span> <span data-ttu-id="f75b5-110">Se necessario, è possibile [creare una macchina virtuale nel portale di hello](quick-create-portal.md) o [con hello Azure CLI](quick-create-cli.md).</span><span class="sxs-lookup"><span data-stu-id="f75b5-110">If needed, you can [create a VM in hello portal](quick-create-portal.md) or [with hello Azure CLI](quick-create-cli.md).</span></span> <span data-ttu-id="f75b5-111">Dopo che la macchina virtuale è operativa, seguire questi passaggi:</span><span class="sxs-lookup"><span data-stu-id="f75b5-111">Follow these steps once your VM is up and running:</span></span>

[!INCLUDE [virtual-machines-common-portal-create-fqdn](../../../includes/virtual-machines-common-portal-create-fqdn.md)]

<span data-ttu-id="f75b5-112">È ora possibile connettersi in remoto toohello nome di macchina virtuale che utilizza questo server DNS, ad esempio con `ssh azureuser@mydns.westus.cloudapp.azure.com`.</span><span class="sxs-lookup"><span data-stu-id="f75b5-112">You can now connect remotely toohello VM using this DNS name such as with `ssh azureuser@mydns.westus.cloudapp.azure.com`.</span></span>

## <a name="next-steps"></a><span data-ttu-id="f75b5-113">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="f75b5-113">Next steps</span></span>
<span data-ttu-id="f75b5-114">Quando la macchina virtuale ha un indirizzo IP pubblico e un nome DNS, è possibile distribuire framework applicazioni o servizi comuni, ad esempio nginx, MongoDB, Docker e così via.</span><span class="sxs-lookup"><span data-stu-id="f75b5-114">Now that your VM has a public IP and DNS name, you can deploy common application frameworks or services such as nginx, MongoDB, Docker, etc.</span></span>

<span data-ttu-id="f75b5-115">Per suggerimenti sulla creazione di distribuzioni di Azure, vedere la pagina relativa all'[uso di Azure Resource Manager](../../azure-resource-manager/resource-group-overview.md).</span><span class="sxs-lookup"><span data-stu-id="f75b5-115">You can also read more about [using Resource Manager](../../azure-resource-manager/resource-group-overview.md) for tips on building your Azure deployments.</span></span>


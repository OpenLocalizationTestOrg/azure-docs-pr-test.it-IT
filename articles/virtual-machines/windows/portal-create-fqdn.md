---
title: nome di dominio completo per una macchina virtuale di Windows nel portale di Azure hello aaaCreate | Documenti Microsoft
description: Informazioni su come toocreate un nome di dominio completo o nome di dominio completo per un gestore di risorse basato su macchina virtuale nel portale di Azure hello.
services: virtual-machines-windows
documentationcenter: 
author: iainfoulds
manager: timlt
editor: tysonn
tags: azure-resource-manager
ms.assetid: a2ae5887-76df-485e-ae19-0efd96df8600
ms.service: virtual-machines-windows
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: infrastructure-services
ms.date: 07/05/2017
ms.author: iainfou
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 67c817ec97073803e513bc41ebde67b75ced565e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-fully-qualified-domain-name-in-hello-azure-portal-for-a-windows-vm"></a><span data-ttu-id="fc32a-103">Creare un nome di dominio completo nel portale di Azure hello per una macchina virtuale Windows</span><span class="sxs-lookup"><span data-stu-id="fc32a-103">Create a fully qualified domain name in hello Azure portal for a Windows VM</span></span>

<span data-ttu-id="fc32a-104">Quando si crea una macchina virtuale (VM) in hello [portale di Azure](https://portal.azure.com), viene creata automaticamente una risorsa IP pubblica per la macchina virtuale hello.</span><span class="sxs-lookup"><span data-stu-id="fc32a-104">When you create a virtual machine (VM) in hello [Azure portal](https://portal.azure.com), a public IP resource for hello virtual machine is automatically created.</span></span> <span data-ttu-id="fc32a-105">Utilizzare questo hello di accesso tooremotely indirizzo IP VM.</span><span class="sxs-lookup"><span data-stu-id="fc32a-105">You use this IP address tooremotely access hello VM.</span></span> <span data-ttu-id="fc32a-106">Anche se il portale di hello non crea un [nome di dominio completo](https://en.wikipedia.org/wiki/Fully_qualified_domain_name), o nome di dominio completo, è possibile crearne uno quando hello viene creata la VM.</span><span class="sxs-lookup"><span data-stu-id="fc32a-106">Although hello portal does not create a [fully qualified domain name](https://en.wikipedia.org/wiki/Fully_qualified_domain_name), or FQDN, you can create one once hello VM is created.</span></span> <span data-ttu-id="fc32a-107">Questo articolo illustra hello passaggi toocreate un nome DNS o il nome FQDN.</span><span class="sxs-lookup"><span data-stu-id="fc32a-107">This article demonstrates hello steps toocreate a DNS name or FQDN.</span></span>

## <a name="create-a-fqdn"></a><span data-ttu-id="fc32a-108">Creare un nome di dominio completo</span><span class="sxs-lookup"><span data-stu-id="fc32a-108">Create a FQDN</span></span>
<span data-ttu-id="fc32a-109">In questo articolo si presuppone che sia già stata creata una VM.</span><span class="sxs-lookup"><span data-stu-id="fc32a-109">This article assumes that you have already created a VM.</span></span> <span data-ttu-id="fc32a-110">Se necessario, è possibile [creare una macchina virtuale nel portale di hello](quick-create-portal.md) o [con Azure PowerShell](quick-create-powershell.md).</span><span class="sxs-lookup"><span data-stu-id="fc32a-110">If needed, you can [create a VM in hello portal](quick-create-portal.md) or [with Azure PowerShell](quick-create-powershell.md).</span></span> <span data-ttu-id="fc32a-111">Dopo che la macchina virtuale è operativa, seguire questi passaggi:</span><span class="sxs-lookup"><span data-stu-id="fc32a-111">Follow these steps once your VM is up and running:</span></span>

[!INCLUDE [virtual-machines-common-portal-create-fqdn](../../../includes/virtual-machines-common-portal-create-fqdn.md)]

<span data-ttu-id="fc32a-112">È ora possibile connettersi in remoto toohello macchina virtuale con questo nome DNS, ad esempio per Remote Desktop Protocol (RDP).</span><span class="sxs-lookup"><span data-stu-id="fc32a-112">You can now connect remotely toohello VM using this DNS name such as for Remote Desktop Protocol (RDP).</span></span>

## <a name="next-steps"></a><span data-ttu-id="fc32a-113">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="fc32a-113">Next steps</span></span>
<span data-ttu-id="fc32a-114">Quando la VM ha un indirizzo IP pubblico e un nome DNS, è possibile distribuire framework applicazioni o servizi comuni, ad esempio IIS, SQL o SharePoint.</span><span class="sxs-lookup"><span data-stu-id="fc32a-114">Now that your VM has a public IP and DNS name, you can deploy common application frameworks or services such as IIS, SQL, or SharePoint.</span></span>

<span data-ttu-id="fc32a-115">Per suggerimenti sulla creazione di distribuzioni di Azure, vedere la pagina relativa all'[uso di Azure Resource Manager](../../azure-resource-manager/resource-group-overview.md).</span><span class="sxs-lookup"><span data-stu-id="fc32a-115">You can also read more about [using Resource Manager](../../azure-resource-manager/resource-group-overview.md) for tips on building your Azure deployments.</span></span>


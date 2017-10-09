---
title: una macchina virtuale Linux classico utilizzando aaaCreate hello Azure CLI 1.0 | Documenti Microsoft
description: Informazioni su come una macchina virtuale Linux con hello Azure CLI 1.0 toocreate hello modello di distribuzione classica
services: virtual-machines-linux
documentationcenter: 
author: iainfoulds
manager: timlt
editor: tysonn
tags: azure-service-management
ms.assetid: f8071a2e-ed91-4f77-87d9-519a37e5364f
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.topic: article
ms.date: 02/09/2017
ms.author: iainfou
ms.openlocfilehash: 5c3c54e5d1444a79e8e609c76d04a3a621c8d03f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="how-toocreate-a-classic-linux-vm-with-hello-azure-cli-10"></a><span data-ttu-id="d1497-103">Come tooCreate un classico VM Linux con hello Azure CLI 1.0</span><span class="sxs-lookup"><span data-stu-id="d1497-103">How tooCreate a Classic Linux VM with hello Azure CLI 1.0</span></span>
> [!IMPORTANT] 
> <span data-ttu-id="d1497-104">Azure offre due diversi modelli di distribuzione per creare e usare le risorse: [Gestione risorse e la distribuzione classica](../../../resource-manager-deployment-model.md).</span><span class="sxs-lookup"><span data-stu-id="d1497-104">Azure has two different deployment models for creating and working with resources: [Resource Manager and Classic](../../../resource-manager-deployment-model.md).</span></span> <span data-ttu-id="d1497-105">In questo articolo viene illustrato l'utilizzo del modello di distribuzione classica hello.</span><span class="sxs-lookup"><span data-stu-id="d1497-105">This article covers using hello Classic deployment model.</span></span> <span data-ttu-id="d1497-106">Si consiglia di utilizzano il modello di gestione risorse hello più nuove distribuzioni.</span><span class="sxs-lookup"><span data-stu-id="d1497-106">Microsoft recommends that most new deployments use hello Resource Manager model.</span></span> <span data-ttu-id="d1497-107">Per la versione di gestione risorse di hello, vedere [qui](../create-cli-complete.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="d1497-107">For hello Resource Manager version, see [here](../create-cli-complete.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>

<span data-ttu-id="d1497-108">In questo argomento viene descritto come una macchina virtuale Linux (VM) con hello Azure CLI 1.0 toocreate hello modello di distribuzione classica.</span><span class="sxs-lookup"><span data-stu-id="d1497-108">This topic describes how toocreate a Linux virtual machine (VM) with hello Azure CLI 1.0 using hello Classic deployment model.</span></span> <span data-ttu-id="d1497-109">Viene usata un'immagine Linux da hello disponibile **immagini** in Azure.</span><span class="sxs-lookup"><span data-stu-id="d1497-109">We use a Linux image from hello available **IMAGES** on Azure.</span></span> <span data-ttu-id="d1497-110">i comandi CLI di Azure 1.0 Hello offrono hello opzioni di configurazione, tra gli altri seguenti:</span><span class="sxs-lookup"><span data-stu-id="d1497-110">hello Azure CLI 1.0 commands give hello following configuration choices, among others:</span></span>

* <span data-ttu-id="d1497-111">La connessione di rete virtuale di hello VM tooa</span><span class="sxs-lookup"><span data-stu-id="d1497-111">Connecting hello VM tooa virtual network</span></span>
* <span data-ttu-id="d1497-112">Aggiungere il servizio cloud esistente di hello VM tooan</span><span class="sxs-lookup"><span data-stu-id="d1497-112">Adding hello VM tooan existing cloud service</span></span>
* <span data-ttu-id="d1497-113">Aggiunta di hello VM tooan account di archiviazione esistente</span><span class="sxs-lookup"><span data-stu-id="d1497-113">Adding hello VM tooan existing storage account</span></span>
* <span data-ttu-id="d1497-114">Aggiunta di set di disponibilità tooan VM hello o percorso</span><span class="sxs-lookup"><span data-stu-id="d1497-114">Adding hello VM tooan availability set or location</span></span>

> [!IMPORTANT]
> <span data-ttu-id="d1497-115">Se si desidera il toouse VM una rete virtuale per la connessione tooit direttamente dal nome host o configurare connessioni cross-premise, assicurarsi di che specificare la rete virtuale hello quando si crea hello macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="d1497-115">If you want your VM toouse a virtual network so you can connect tooit directly by hostname or set up cross-premises connections, make sure you specify hello virtual network when you create hello VM.</span></span> <span data-ttu-id="d1497-116">Una macchina virtuale può essere toojoin configurata una rete virtuale solo quando si crea hello macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="d1497-116">A VM can be configured toojoin a virtual network only when you create hello VM.</span></span> <span data-ttu-id="d1497-117">Per informazioni dettagliate sulle reti virtuali, vedere [Panoramica di Rete virtuale](http://go.microsoft.com/fwlink/p/?LinkID=294063).</span><span class="sxs-lookup"><span data-stu-id="d1497-117">For details on virtual networks, see [Azure Virtual Network Overview](http://go.microsoft.com/fwlink/p/?LinkID=294063).</span></span>
> 
> 

## <a name="how-toocreate-a-linux-vm-using-hello-classic-deployment-model"></a><span data-ttu-id="d1497-118">Come toocreate una VM Linux utilizzando hello modello di distribuzione classica</span><span class="sxs-lookup"><span data-stu-id="d1497-118">How toocreate a Linux VM using hello Classic deployment model</span></span>
[!INCLUDE [virtual-machines-create-LinuxVM](../../../../includes/virtual-machines-create-linuxvm.md)]


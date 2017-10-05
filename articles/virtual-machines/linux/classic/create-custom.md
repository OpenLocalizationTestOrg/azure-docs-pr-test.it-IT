---
title: Creare una VM Linux classica usando l'interfaccia della riga di comando di Azure 1.0 | Documentazione Microsoft
description: Informazioni su come creare una macchina virtuale con l'interfaccia della riga di comando di Azure 1.0 usando il modello di distribuzione classica.
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
ms.openlocfilehash: 8ddbacbbb70c0cf1a2537fab4d981a316610a4d7
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="how-to-create-a-classic-linux-vm-with-the-azure-cli-10"></a><span data-ttu-id="54415-103">Come creare una VM Linux classica con l'interfaccia della riga di comando di Azure 1.0</span><span class="sxs-lookup"><span data-stu-id="54415-103">How to Create a Classic Linux VM with the Azure CLI 1.0</span></span>
> [!IMPORTANT] 
> <span data-ttu-id="54415-104">Azure offre due diversi modelli di distribuzione per creare e usare le risorse: [Gestione risorse e la distribuzione classica](../../../resource-manager-deployment-model.md).</span><span class="sxs-lookup"><span data-stu-id="54415-104">Azure has two different deployment models for creating and working with resources: [Resource Manager and Classic](../../../resource-manager-deployment-model.md).</span></span> <span data-ttu-id="54415-105">Questo articolo illustra l'uso del modello di distribuzione classica.</span><span class="sxs-lookup"><span data-stu-id="54415-105">This article covers using the Classic deployment model.</span></span> <span data-ttu-id="54415-106">Microsoft consiglia di usare il modello di Gestione risorse per le distribuzioni più recenti.</span><span class="sxs-lookup"><span data-stu-id="54415-106">Microsoft recommends that most new deployments use the Resource Manager model.</span></span> <span data-ttu-id="54415-107">Per la versione di Resource Manager, vedere [qui](../create-cli-complete.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="54415-107">For the Resource Manager version, see [here](../create-cli-complete.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>

<span data-ttu-id="54415-108">Questo argomento descrive come creare una macchina virtuale con l'interfaccia della riga di comando di Azure 1.0 usando il modello di distribuzione classica.</span><span class="sxs-lookup"><span data-stu-id="54415-108">This topic describes how to create a Linux virtual machine (VM) with the Azure CLI 1.0 using the Classic deployment model.</span></span> <span data-ttu-id="54415-109">Viene utilizzata un'immagine Linux dalle **IMMAGINI** disponibili in Azure.</span><span class="sxs-lookup"><span data-stu-id="54415-109">We use a Linux image from the available **IMAGES** on Azure.</span></span> <span data-ttu-id="54415-110">I comandi dell'interfaccia della riga di comando di Azure 1.0 offrono le opzioni di configurazione seguenti:</span><span class="sxs-lookup"><span data-stu-id="54415-110">The Azure CLI 1.0 commands give the following configuration choices, among others:</span></span>

* <span data-ttu-id="54415-111">Connessione della macchina virtuale a una rete virtuale</span><span class="sxs-lookup"><span data-stu-id="54415-111">Connecting the VM to a virtual network</span></span>
* <span data-ttu-id="54415-112">Aggiunta della macchina virtuale a un servizio cloud esistente</span><span class="sxs-lookup"><span data-stu-id="54415-112">Adding the VM to an existing cloud service</span></span>
* <span data-ttu-id="54415-113">Aggiunta della macchina virtuale a un account di archiviazione esistente</span><span class="sxs-lookup"><span data-stu-id="54415-113">Adding the VM to an existing storage account</span></span>
* <span data-ttu-id="54415-114">Aggiunta della macchina virtuale a un set di disponibilità o a un percorso</span><span class="sxs-lookup"><span data-stu-id="54415-114">Adding the VM to an availability set or location</span></span>

> [!IMPORTANT]
> <span data-ttu-id="54415-115">Se si desidera che la macchina virtuale utilizzi una rete virtuale in modo da poter effettuare la connessione direttamente tramite il nome host o configurare connessioni cross-premise, assicurarsi di specificare la rete virtuale quando viene creata la macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="54415-115">If you want your VM to use a virtual network so you can connect to it directly by hostname or set up cross-premises connections, make sure you specify the virtual network when you create the VM.</span></span> <span data-ttu-id="54415-116">Una macchina virtuale può essere configurata per accedere a una rete virtuale solo quando viene creata la macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="54415-116">A VM can be configured to join a virtual network only when you create the VM.</span></span> <span data-ttu-id="54415-117">Per informazioni dettagliate sulle reti virtuali, vedere [Panoramica di Rete virtuale](http://go.microsoft.com/fwlink/p/?LinkID=294063).</span><span class="sxs-lookup"><span data-stu-id="54415-117">For details on virtual networks, see [Azure Virtual Network Overview](http://go.microsoft.com/fwlink/p/?LinkID=294063).</span></span>
> 
> 

## <a name="how-to-create-a-linux-vm-using-the-classic-deployment-model"></a><span data-ttu-id="54415-118">Come creare una macchina virtuale Linux usando il modello di distribuzione classica</span><span class="sxs-lookup"><span data-stu-id="54415-118">How to create a Linux VM using the Classic deployment model</span></span>
[!INCLUDE [virtual-machines-create-LinuxVM](../../../../includes/virtual-machines-create-linuxvm.md)]


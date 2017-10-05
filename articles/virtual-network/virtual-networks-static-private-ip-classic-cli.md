---
title: Configurare indirizzi IP privati per le VM (classica) - interfaccia della riga di comando 1.0 di Azure | Documentazione Microsoft
description: Informazioni su come configurare gli indirizzi IP privati per le macchine virtuali (classica) usando l'interfaccia della riga di comando di Azure 1.0.
services: virtual-network
documentationcenter: na
author: jimdial
manager: timlt
editor: tysonn
tags: azure-service-management
ms.assetid: 17386acf-c708-4103-9b22-ff9bf04b778d
ms.service: virtual-network
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 03/15/2016
ms.author: jdial
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: ed0fe2fea20671063395b9ff089599853278989d
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="configure-private-ip-addresses-for-a-virtual-machine-classic-using-the-azure-cli-10"></a><span data-ttu-id="4f4a3-103">Configurare gli indirizzi IP privati per una macchina virtuale (classica) usando l'interfaccia della riga di comando 1.0 di Azure</span><span class="sxs-lookup"><span data-stu-id="4f4a3-103">Configure private IP addresses for a virtual machine (Classic) using the Azure CLI 1.0</span></span>

[!INCLUDE [virtual-networks-static-private-ip-selectors-classic-include](../../includes/virtual-networks-static-private-ip-selectors-classic-include.md)]

[!INCLUDE [virtual-networks-static-private-ip-intro-include](../../includes/virtual-networks-static-private-ip-intro-include.md)]

[!INCLUDE [azure-arm-classic-important-include](../../includes/azure-arm-classic-important-include.md)]

<span data-ttu-id="4f4a3-104">In questo articolo viene illustrato il modello di distribuzione classica.</span><span class="sxs-lookup"><span data-stu-id="4f4a3-104">This article covers the classic deployment model.</span></span> <span data-ttu-id="4f4a3-105">È inoltre possibile [gestire un indirizzo IP statico privato nel modello di distribuzione di gestione delle risorse](virtual-networks-static-private-ip-arm-cli.md).</span><span class="sxs-lookup"><span data-stu-id="4f4a3-105">You can also [manage a static private IP address in the Resource Manager deployment model](virtual-networks-static-private-ip-arm-cli.md).</span></span>

<span data-ttu-id="4f4a3-106">I comandi di esempio infrastruttura CLI di Azure riportati di seguito prevedono un ambiente semplice già creato.</span><span class="sxs-lookup"><span data-stu-id="4f4a3-106">The sample Azure CLI commands below expect a simple environment already created.</span></span> <span data-ttu-id="4f4a3-107">Se si desidera eseguire i comandi illustrati in questo documento, creare innanzitutto l'ambiente di prova descritto in [creare una rete virtuale](virtual-networks-create-vnet-classic-cli.md).</span><span class="sxs-lookup"><span data-stu-id="4f4a3-107">If you want to run the commands as they are displayed in this document, first build the test environment described in [create a vnet](virtual-networks-create-vnet-classic-cli.md).</span></span>

## <a name="how-to-specify-a-static-private-ip-address-when-creating-a-vm"></a><span data-ttu-id="4f4a3-108">Come specificare un indirizzo IP statico privato durante la creazione di una macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="4f4a3-108">How to specify a static private IP address when creating a VM</span></span>
<span data-ttu-id="4f4a3-109">Per creare una nuova VM denominata *DNS01* in un nuovo servizio cloud denominato *TestService* in base allo scenario precedente, attenersi alla procedura seguente:</span><span class="sxs-lookup"><span data-stu-id="4f4a3-109">To create a new VM named *DNS01* in a new cloud service named *TestService* based on the scenario above, follow these steps:</span></span>

1. <span data-ttu-id="4f4a3-110">Se l'interfaccia della riga di comando di Azure non è mai stata usata, vedere [Installare e configurare l'interfaccia della riga di comando di Azure](../cli-install-nodejs.md) e seguire le istruzioni fino al punto in cui si selezionano l'account e la sottoscrizione di Azure.</span><span class="sxs-lookup"><span data-stu-id="4f4a3-110">If you have never used Azure CLI, see [Install and Configure the Azure CLI](../cli-install-nodejs.md) and follow the instructions up to the point where you select your Azure account and subscription.</span></span>
2. <span data-ttu-id="4f4a3-111">Eseguire il **azure service create** per creare il servizio cloud.</span><span class="sxs-lookup"><span data-stu-id="4f4a3-111">Run the **azure service create** command to create the cloud service.</span></span>
   
        azure service create TestService --location uscentral
   
    <span data-ttu-id="4f4a3-112">Output previsto:</span><span class="sxs-lookup"><span data-stu-id="4f4a3-112">Expected output:</span></span>
   
        info:    Executing command service create
        info:    Creating cloud service
        data:    Cloud service name TestService
        info:    service create command OK
3. <span data-ttu-id="4f4a3-113">Eseguire il comando **azure create vm** per creare la VM.</span><span class="sxs-lookup"><span data-stu-id="4f4a3-113">Run the **azure create vm** command to create the VM.</span></span> <span data-ttu-id="4f4a3-114">Si noti il valore per un indirizzo IP statico privato.</span><span class="sxs-lookup"><span data-stu-id="4f4a3-114">Notice the value for a static private IP address.</span></span> <span data-ttu-id="4f4a3-115">Nell'elenco riportato dopo l'output sono indicati i parametri usati.</span><span class="sxs-lookup"><span data-stu-id="4f4a3-115">The list shown after the output explains the parameters used.</span></span>
   
        azure vm create -l centralus -n DNS01 -w TestVNet -S "192.168.1.101" TestService bd507d3a70934695bc2128e3e5a255ba__RightImage-Windows-2012R2-x64-v14.2 adminuser AdminP@ssw0rd
   
    <span data-ttu-id="4f4a3-116">Output previsto:</span><span class="sxs-lookup"><span data-stu-id="4f4a3-116">Expected output:</span></span>
   
        info:    Executing command vm create
        warn:    --vm-size has not been specified. Defaulting to "Small".
        info:    Looking up image bd507d3a70934695bc2128e3e5a255ba__RightImage-Windows-2012R2-x64-v14.2
        info:    Looking up virtual network
        info:    Looking up cloud service
        warn:    --location option will be ignored
        info:    Getting cloud service properties
        info:    Looking up deployment
        info:    Retrieving storage accounts
        info:    Creating VM
        info:    OK
        info:    vm create command OK
   
   * <span data-ttu-id="4f4a3-117">**-l (o --location)**.</span><span class="sxs-lookup"><span data-stu-id="4f4a3-117">**-l (or --location)**.</span></span> <span data-ttu-id="4f4a3-118">Area di Azure in cui verrà creata la VM.</span><span class="sxs-lookup"><span data-stu-id="4f4a3-118">Azure region where the VM will be created.</span></span> <span data-ttu-id="4f4a3-119">Per questo scenario, *centralus*.</span><span class="sxs-lookup"><span data-stu-id="4f4a3-119">For our scenario, *centralus*.</span></span>
   * <span data-ttu-id="4f4a3-120">**-n (o --vm-name)**.</span><span class="sxs-lookup"><span data-stu-id="4f4a3-120">**-n (or --vm-name)**.</span></span> <span data-ttu-id="4f4a3-121">Nome della VM da creare.</span><span class="sxs-lookup"><span data-stu-id="4f4a3-121">Name of the VM to be created.</span></span>
   * <span data-ttu-id="4f4a3-122">**-w (o --virtual-network-name)**.</span><span class="sxs-lookup"><span data-stu-id="4f4a3-122">**-w (or --virtual-network-name)**.</span></span> <span data-ttu-id="4f4a3-123">Nome della VNet in cui verrà creata la VM.</span><span class="sxs-lookup"><span data-stu-id="4f4a3-123">Name of the VNet where the VM will be created.</span></span> 
   * <span data-ttu-id="4f4a3-124">**-S (o --static-ip)**.</span><span class="sxs-lookup"><span data-stu-id="4f4a3-124">**-S (or --static-ip)**.</span></span> <span data-ttu-id="4f4a3-125">Indirizzo IP privato statico per il gruppo VM.</span><span class="sxs-lookup"><span data-stu-id="4f4a3-125">Static private IP address for the VM.</span></span>
   * <span data-ttu-id="4f4a3-126">**TestService**.</span><span class="sxs-lookup"><span data-stu-id="4f4a3-126">**TestService**.</span></span> <span data-ttu-id="4f4a3-127">Nome del servizio cloud in cui verrà creata la VM.</span><span class="sxs-lookup"><span data-stu-id="4f4a3-127">Name of the cloud service where the VM will be created.</span></span>
   * <span data-ttu-id="4f4a3-128">**bd507d3a70934695bc2128e3e5a255ba__RightImage-Windows-2012R2-x64-v14.2**.</span><span class="sxs-lookup"><span data-stu-id="4f4a3-128">**bd507d3a70934695bc2128e3e5a255ba__RightImage-Windows-2012R2-x64-v14.2**.</span></span> <span data-ttu-id="4f4a3-129">Immagine utilizzata per creare la VM.</span><span class="sxs-lookup"><span data-stu-id="4f4a3-129">Image used to create the VM.</span></span>
   * <span data-ttu-id="4f4a3-130">**adminuser**.</span><span class="sxs-lookup"><span data-stu-id="4f4a3-130">**adminuser**.</span></span> <span data-ttu-id="4f4a3-131">Amministratore locale della VM di Windows.</span><span class="sxs-lookup"><span data-stu-id="4f4a3-131">Local administrator for the Windows VM.</span></span>
   * <span data-ttu-id="4f4a3-132">**AdminP@ssw0rd**.</span><span class="sxs-lookup"><span data-stu-id="4f4a3-132">**AdminP@ssw0rd**.</span></span> <span data-ttu-id="4f4a3-133">Amministratore locale della password della VM di Windows.</span><span class="sxs-lookup"><span data-stu-id="4f4a3-133">Local administrator password for the Windows VM.</span></span>

## <a name="how-to-retrieve-static-private-ip-address-information-for-a-vm"></a><span data-ttu-id="4f4a3-134">Come recuperare le informazioni relative all'indirizzo IP privato statico per una macchina virtuale</span><span class="sxs-lookup"><span data-stu-id="4f4a3-134">How to retrieve static private IP address information for a VM</span></span>
<span data-ttu-id="4f4a3-135">Per visualizzare le informazioni relative all'indirizzo IP interno statico per la VM creata con lo script precedente, eseguire il comando dell’interfaccia di riga di comando di Azure seguente e osservare i valori per *Network StaticIp*:</span><span class="sxs-lookup"><span data-stu-id="4f4a3-135">To view the static private IP address information for the VM created with the script above, run the following Azure CLI command and observe the value for *Network StaticIP*:</span></span>

    azure vm static-ip show DNS01

<span data-ttu-id="4f4a3-136">Output previsto:</span><span class="sxs-lookup"><span data-stu-id="4f4a3-136">Expected output:</span></span>

    info:    Executing command vm static-ip show
    info:    Getting virtual machines
    data:    Network StaticIP "192.168.1.101"
    info:    vm static-ip show command OK

## <a name="how-to-remove-a-static-private-ip-address-from-a-vm"></a><span data-ttu-id="4f4a3-137">Come rimuovere un indirizzo IP statico privato da una macchina virtuale</span><span class="sxs-lookup"><span data-stu-id="4f4a3-137">How to remove a static private IP address from a VM</span></span>
<span data-ttu-id="4f4a3-138">Per rimuovere l'indirizzo IP privato statico aggiunto alla VM nello script precedente, eseguire il seguente comando dell’interfaccia di riga di comando di Azure:</span><span class="sxs-lookup"><span data-stu-id="4f4a3-138">To remove the static private IP address added to the VM in the script above, run the following Azure CLI command:</span></span>

    azure vm static-ip remove DNS01

<span data-ttu-id="4f4a3-139">Output previsto:</span><span class="sxs-lookup"><span data-stu-id="4f4a3-139">Expected output:</span></span>

    info:    Executing command vm static-ip remove
    info:    Getting virtual machines
    info:    Reading network configuration
    info:    Updating network configuration
    info:    vm static-ip remove command OK

## <a name="how-to-add-a-static-private-ip-to-an-existing-vm"></a><span data-ttu-id="4f4a3-140">Come aggiungere un indirizzo IP statico privato a una VM esistente</span><span class="sxs-lookup"><span data-stu-id="4f4a3-140">How to add a static private IP to an existing VM</span></span>
<span data-ttu-id="4f4a3-141">Per aggiungere un indirizzo IP privato statico alla macchina virtuale creata usando lo script precedente, eseguire il comando seguente:</span><span class="sxs-lookup"><span data-stu-id="4f4a3-141">To add a static private IP address to the VM created using the script above, runt he following command:</span></span>

    azure vm static-ip set DNS01 192.168.1.101

<span data-ttu-id="4f4a3-142">Output previsto:</span><span class="sxs-lookup"><span data-stu-id="4f4a3-142">Expected output:</span></span>

    info:    Executing command vm static-ip set
    info:    Getting virtual machines
    info:    Looking up virtual network
    info:    Reading network configuration
    info:    Updating network configuration
    info:    vm static-ip set command OK

## <a name="next-steps"></a><span data-ttu-id="4f4a3-143">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="4f4a3-143">Next steps</span></span>
* <span data-ttu-id="4f4a3-144">Informazioni su [indirizzi IP pubblici riservati](virtual-networks-reserved-public-ip.md) .</span><span class="sxs-lookup"><span data-stu-id="4f4a3-144">Learn about [reserved public IP](virtual-networks-reserved-public-ip.md) addresses.</span></span>
* <span data-ttu-id="4f4a3-145">Informazioni su [indirizzi IP pubblici a livello di istanza (ILPIP)](virtual-networks-instance-level-public-ip.md) .</span><span class="sxs-lookup"><span data-stu-id="4f4a3-145">Learn about [instance-level public IP (ILPIP)](virtual-networks-instance-level-public-ip.md) addresses.</span></span>
* <span data-ttu-id="4f4a3-146">Consultare le [API REST dell'indirizzo IP riservato](https://msdn.microsoft.com/library/azure/dn722420.aspx).</span><span class="sxs-lookup"><span data-stu-id="4f4a3-146">Consult the [Reserved IP REST APIs](https://msdn.microsoft.com/library/azure/dn722420.aspx).</span></span>


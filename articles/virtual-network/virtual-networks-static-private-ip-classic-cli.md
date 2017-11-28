---
title: indirizzi IP privati aaaConfigure per le macchine virtuali (classico) - CLI di Azure 1.0 | Documenti Microsoft
description: Informazioni su come indirizzi IP privati tooconfigure per le macchine virtuali (classico) utilizzando hello Azure interfaccia della riga di comando (CLI) 1.0.
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
ms.openlocfilehash: 417a57181bcf5c2e6101bf3bdf63fc94ebc99df5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="configure-private-ip-addresses-for-a-virtual-machine-classic-using-hello-azure-cli-10"></a><span data-ttu-id="a4145-103">Configurare gli indirizzi IP privati per una macchina virtuale (classico) utilizzando hello Azure CLI 1.0</span><span class="sxs-lookup"><span data-stu-id="a4145-103">Configure private IP addresses for a virtual machine (Classic) using hello Azure CLI 1.0</span></span>

[!INCLUDE [virtual-networks-static-private-ip-selectors-classic-include](../../includes/virtual-networks-static-private-ip-selectors-classic-include.md)]

[!INCLUDE [virtual-networks-static-private-ip-intro-include](../../includes/virtual-networks-static-private-ip-intro-include.md)]

[!INCLUDE [azure-arm-classic-important-include](../../includes/azure-arm-classic-important-include.md)]

<span data-ttu-id="a4145-104">Questo articolo descrive il modello di distribuzione classica hello.</span><span class="sxs-lookup"><span data-stu-id="a4145-104">This article covers hello classic deployment model.</span></span> <span data-ttu-id="a4145-105">È anche possibile [gestire un indirizzo IP privato statico nel modello di distribuzione di gestione risorse di hello](virtual-networks-static-private-ip-arm-cli.md).</span><span class="sxs-lookup"><span data-stu-id="a4145-105">You can also [manage a static private IP address in hello Resource Manager deployment model](virtual-networks-static-private-ip-arm-cli.md).</span></span>

<span data-ttu-id="a4145-106">Hello esempio CLI di Azure comandi riportati di seguito prevedono un ambiente semplice già creato.</span><span class="sxs-lookup"><span data-stu-id="a4145-106">hello sample Azure CLI commands below expect a simple environment already created.</span></span> <span data-ttu-id="a4145-107">Se si desidera comandi hello toorun così come sono visualizzati in questo documento, innanzitutto compilare descritto nell'ambiente di test di hello [creare una rete virtuale](virtual-networks-create-vnet-classic-cli.md).</span><span class="sxs-lookup"><span data-stu-id="a4145-107">If you want toorun hello commands as they are displayed in this document, first build hello test environment described in [create a vnet](virtual-networks-create-vnet-classic-cli.md).</span></span>

## <a name="how-toospecify-a-static-private-ip-address-when-creating-a-vm"></a><span data-ttu-id="a4145-108">Come toospecify un indirizzo IP privato statico di indirizzi durante la creazione di una macchina virtuale</span><span class="sxs-lookup"><span data-stu-id="a4145-108">How toospecify a static private IP address when creating a VM</span></span>
<span data-ttu-id="a4145-109">una nuova macchina virtuale denominata toocreate *DNS01* in un nuovo servizio cloud denominato *TestService* a seconda dello scenario hello precedente, seguire questi passaggi:</span><span class="sxs-lookup"><span data-stu-id="a4145-109">toocreate a new VM named *DNS01* in a new cloud service named *TestService* based on hello scenario above, follow these steps:</span></span>

1. <span data-ttu-id="a4145-110">Se non si è mai usato CLI di Azure, vedere [installare e configurare hello Azure CLI](../cli-install-nodejs.md) e seguire le istruzioni di hello toohello un punto in cui si seleziona l'account di Azure e la sottoscrizione.</span><span class="sxs-lookup"><span data-stu-id="a4145-110">If you have never used Azure CLI, see [Install and Configure hello Azure CLI](../cli-install-nodejs.md) and follow hello instructions up toohello point where you select your Azure account and subscription.</span></span>
2. <span data-ttu-id="a4145-111">Eseguire hello **servizio di azure creare** servizio cloud di hello toocreate di comando.</span><span class="sxs-lookup"><span data-stu-id="a4145-111">Run hello **azure service create** command toocreate hello cloud service.</span></span>
   
        azure service create TestService --location uscentral
   
    <span data-ttu-id="a4145-112">Output previsto:</span><span class="sxs-lookup"><span data-stu-id="a4145-112">Expected output:</span></span>
   
        info:    Executing command service create
        info:    Creating cloud service
        data:    Cloud service name TestService
        info:    service create command OK
3. <span data-ttu-id="a4145-113">Eseguire hello **azure creare una macchina virtuale** comando toocreate hello macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="a4145-113">Run hello **azure create vm** command toocreate hello VM.</span></span> <span data-ttu-id="a4145-114">Si noti il valore di hello per un indirizzo IP privato statico.</span><span class="sxs-lookup"><span data-stu-id="a4145-114">Notice hello value for a static private IP address.</span></span> <span data-ttu-id="a4145-115">elenco di Hello visualizzato dopo l'output di hello illustrati parametri di hello utilizzati.</span><span class="sxs-lookup"><span data-stu-id="a4145-115">hello list shown after hello output explains hello parameters used.</span></span>
   
        azure vm create -l centralus -n DNS01 -w TestVNet -S "192.168.1.101" TestService bd507d3a70934695bc2128e3e5a255ba__RightImage-Windows-2012R2-x64-v14.2 adminuser AdminP@ssw0rd
   
    <span data-ttu-id="a4145-116">Output previsto:</span><span class="sxs-lookup"><span data-stu-id="a4145-116">Expected output:</span></span>
   
        info:    Executing command vm create
        warn:    --vm-size has not been specified. Defaulting too"Small".
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
   
   * <span data-ttu-id="a4145-117">**-l (o --location)**.</span><span class="sxs-lookup"><span data-stu-id="a4145-117">**-l (or --location)**.</span></span> <span data-ttu-id="a4145-118">Area di Azure in cui verrà creato hello macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="a4145-118">Azure region where hello VM will be created.</span></span> <span data-ttu-id="a4145-119">Per questo scenario, *centralus*.</span><span class="sxs-lookup"><span data-stu-id="a4145-119">For our scenario, *centralus*.</span></span>
   * <span data-ttu-id="a4145-120">**-n (o --vm-name)**.</span><span class="sxs-lookup"><span data-stu-id="a4145-120">**-n (or --vm-name)**.</span></span> <span data-ttu-id="a4145-121">Nome di hello VM toobe creato.</span><span class="sxs-lookup"><span data-stu-id="a4145-121">Name of hello VM toobe created.</span></span>
   * <span data-ttu-id="a4145-122">**-w (o --virtual-network-name)**.</span><span class="sxs-lookup"><span data-stu-id="a4145-122">**-w (or --virtual-network-name)**.</span></span> <span data-ttu-id="a4145-123">Nome della rete virtuale in cui verrà creato hello VM hello.</span><span class="sxs-lookup"><span data-stu-id="a4145-123">Name of hello VNet where hello VM will be created.</span></span> 
   * <span data-ttu-id="a4145-124">**-S (o --static-ip)**.</span><span class="sxs-lookup"><span data-stu-id="a4145-124">**-S (or --static-ip)**.</span></span> <span data-ttu-id="a4145-125">Indirizzo IP privato statico per hello macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="a4145-125">Static private IP address for hello VM.</span></span>
   * <span data-ttu-id="a4145-126">**TestService**.</span><span class="sxs-lookup"><span data-stu-id="a4145-126">**TestService**.</span></span> <span data-ttu-id="a4145-127">Nome del servizio cloud hello in cui verrà creato hello macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="a4145-127">Name of hello cloud service where hello VM will be created.</span></span>
   * <span data-ttu-id="a4145-128">**bd507d3a70934695bc2128e3e5a255ba__RightImage-Windows-2012R2-x64-v14.2**.</span><span class="sxs-lookup"><span data-stu-id="a4145-128">**bd507d3a70934695bc2128e3e5a255ba__RightImage-Windows-2012R2-x64-v14.2**.</span></span> <span data-ttu-id="a4145-129">Immagine utilizzata toocreate hello macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="a4145-129">Image used toocreate hello VM.</span></span>
   * <span data-ttu-id="a4145-130">**adminuser**.</span><span class="sxs-lookup"><span data-stu-id="a4145-130">**adminuser**.</span></span> <span data-ttu-id="a4145-131">Amministratore locale per la macchina virtuale di Windows hello.</span><span class="sxs-lookup"><span data-stu-id="a4145-131">Local administrator for hello Windows VM.</span></span>
   * <span data-ttu-id="a4145-132">**AdminP@ssw0rd**.</span><span class="sxs-lookup"><span data-stu-id="a4145-132">**AdminP@ssw0rd**.</span></span> <span data-ttu-id="a4145-133">Password dell'amministratore locale per la macchina virtuale di Windows hello.</span><span class="sxs-lookup"><span data-stu-id="a4145-133">Local administrator password for hello Windows VM.</span></span>

## <a name="how-tooretrieve-static-private-ip-address-information-for-a-vm"></a><span data-ttu-id="a4145-134">Come indirizzo IP privato statico tooretrieve informazioni sull'indirizzo di una macchina virtuale</span><span class="sxs-lookup"><span data-stu-id="a4145-134">How tooretrieve static private IP address information for a VM</span></span>
<span data-ttu-id="a4145-135">IP privato statico di tooview hello informazioni sull'indirizzo di hello macchina virtuale creata con lo script hello precedente, eseguire il comando CLI di Azure seguente hello e osservare il valore di hello per *StaticIP rete*:</span><span class="sxs-lookup"><span data-stu-id="a4145-135">tooview hello static private IP address information for hello VM created with hello script above, run hello following Azure CLI command and observe hello value for *Network StaticIP*:</span></span>

    azure vm static-ip show DNS01

<span data-ttu-id="a4145-136">Output previsto:</span><span class="sxs-lookup"><span data-stu-id="a4145-136">Expected output:</span></span>

    info:    Executing command vm static-ip show
    info:    Getting virtual machines
    data:    Network StaticIP "192.168.1.101"
    info:    vm static-ip show command OK

## <a name="how-tooremove-a-static-private-ip-address-from-a-vm"></a><span data-ttu-id="a4145-137">Come tooremove un indirizzo IP privato statico di indirizzi da una macchina virtuale</span><span class="sxs-lookup"><span data-stu-id="a4145-137">How tooremove a static private IP address from a VM</span></span>
<span data-ttu-id="a4145-138">tooremove hello indirizzo IP privato statico aggiunta toohello VM hello allo script precedente, hello esecuzione comando CLI di Azure seguente:</span><span class="sxs-lookup"><span data-stu-id="a4145-138">tooremove hello static private IP address added toohello VM in hello script above, run hello following Azure CLI command:</span></span>

    azure vm static-ip remove DNS01

<span data-ttu-id="a4145-139">Output previsto:</span><span class="sxs-lookup"><span data-stu-id="a4145-139">Expected output:</span></span>

    info:    Executing command vm static-ip remove
    info:    Getting virtual machines
    info:    Reading network configuration
    info:    Updating network configuration
    info:    vm static-ip remove command OK

## <a name="how-tooadd-a-static-private-ip-tooan-existing-vm"></a><span data-ttu-id="a4145-140">Come tooadd un tooan IP statico privato macchina virtuale esistente</span><span class="sxs-lookup"><span data-stu-id="a4145-140">How tooadd a static private IP tooan existing VM</span></span>
<span data-ttu-id="a4145-141">tooadd un statico privato IP indirizzo toohello macchina virtuale creata utilizzando lo script hello sopra, Run il seguente comando:</span><span class="sxs-lookup"><span data-stu-id="a4145-141">tooadd a static private IP address toohello VM created using hello script above, runt he following command:</span></span>

    azure vm static-ip set DNS01 192.168.1.101

<span data-ttu-id="a4145-142">Output previsto:</span><span class="sxs-lookup"><span data-stu-id="a4145-142">Expected output:</span></span>

    info:    Executing command vm static-ip set
    info:    Getting virtual machines
    info:    Looking up virtual network
    info:    Reading network configuration
    info:    Updating network configuration
    info:    vm static-ip set command OK

## <a name="next-steps"></a><span data-ttu-id="a4145-143">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="a4145-143">Next steps</span></span>
* <span data-ttu-id="a4145-144">Informazioni su [indirizzi IP pubblici riservati](virtual-networks-reserved-public-ip.md) .</span><span class="sxs-lookup"><span data-stu-id="a4145-144">Learn about [reserved public IP](virtual-networks-reserved-public-ip.md) addresses.</span></span>
* <span data-ttu-id="a4145-145">Informazioni su [indirizzi IP pubblici a livello di istanza (ILPIP)](virtual-networks-instance-level-public-ip.md) .</span><span class="sxs-lookup"><span data-stu-id="a4145-145">Learn about [instance-level public IP (ILPIP)](virtual-networks-instance-level-public-ip.md) addresses.</span></span>
* <span data-ttu-id="a4145-146">Consultare hello [API REST per IP riservato](https://msdn.microsoft.com/library/azure/dn722420.aspx).</span><span class="sxs-lookup"><span data-stu-id="a4145-146">Consult hello [Reserved IP REST APIs](https://msdn.microsoft.com/library/azure/dn722420.aspx).</span></span>


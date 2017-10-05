---
title: Modificare le impostazioni di DATA 0 in un dispositivo StorSimple serie 8000 | Microsoft Docs
description: Informazioni su come utilizzare Windows PowerShell per StorSimple per riconfigurare l'interfaccia di rete DATI 0 sul dispositivo StorSimple
services: storsimple
documentationcenter: 
author: alkohli
manager: timlt
editor: 
ms.assetid: 
ms.service: storsimple
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 03/27/2017
ms.author: alkohli
ms.openlocfilehash: 90df43e22f17fd32fe642514df098b72700e77af
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="modify-the-data-0-network-interface-settings-on-your-storsimple-8000-series-device"></a><span data-ttu-id="5a3dd-103">Modificare le impostazioni dell'interfaccia di rete DATA 0 in un dispositivo StorSimple serie 8000</span><span class="sxs-lookup"><span data-stu-id="5a3dd-103">Modify the DATA 0 network interface settings on your StorSimple 8000 series device</span></span>

## <a name="overview"></a><span data-ttu-id="5a3dd-104">Panoramica</span><span class="sxs-lookup"><span data-stu-id="5a3dd-104">Overview</span></span>

<span data-ttu-id="5a3dd-105">Il dispositivo Microsoft Azure StorSimple ha sei interfacce di rete, da DATI 0 a DATI 5.</span><span class="sxs-lookup"><span data-stu-id="5a3dd-105">Your Microsoft Azure StorSimple device has six network interfaces, from DATA 0 to DATA 5.</span></span> <span data-ttu-id="5a3dd-106">L'interfaccia DATI 0 è sempre configurata tramite l'interfaccia di Windows PowerShell o la console seriale ed è automaticamente abilitata per il cloud.</span><span class="sxs-lookup"><span data-stu-id="5a3dd-106">The DATA 0 interface is always configured through the Windows PowerShell interface or the serial console, and is automatically cloud-enabled.</span></span> <span data-ttu-id="5a3dd-107">Si noti che non è possibile configurare l'interfaccia di rete DATA 0 con il portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="5a3dd-107">Note that you cannot configure DATA 0 network interface through the Azure portal.</span></span>

<span data-ttu-id="5a3dd-108">L'interfaccia DATI 0 viene inizialmente configurata tramite l'installazione guidata durante la distribuzione iniziale del dispositivo StorSimple.</span><span class="sxs-lookup"><span data-stu-id="5a3dd-108">The DATA 0 interface is first configured through the setup wizard during initial deployment of the StorSimple device.</span></span> <span data-ttu-id="5a3dd-109">Quando il dispositivo è in modalità operativa, potrebbe essere necessario riconfigurare le impostazioni di DATI 0.</span><span class="sxs-lookup"><span data-stu-id="5a3dd-109">When the device is in an operational mode, you may need to reconfigure DATA 0 settings.</span></span> <span data-ttu-id="5a3dd-110">In questa esercitazione sono disponibili due metodi per modificare le impostazioni di rete di DATI 0, entrambi tramite Windows PowerShell per StorSimple.</span><span class="sxs-lookup"><span data-stu-id="5a3dd-110">This tutorial provides two methods to modify DATA 0 network settings, both through Windows PowerShell for StorSimple.</span></span>

<span data-ttu-id="5a3dd-111">Dopo aver letto questa esercitazione, si sarà in grado di:</span><span class="sxs-lookup"><span data-stu-id="5a3dd-111">After reading this tutorial, you will be able to:</span></span>

* <span data-ttu-id="5a3dd-112">Modificare l'impostazione di rete di DATI 0 tramite la configurazione guidata</span><span class="sxs-lookup"><span data-stu-id="5a3dd-112">Modify DATA 0 network setting through the setup wizard</span></span>
* <span data-ttu-id="5a3dd-113">Modificare le impostazioni di rete di DATI 0 con il cmdlet `Set-HcsNetInterface`</span><span class="sxs-lookup"><span data-stu-id="5a3dd-113">Modify DATA 0 network settings through the `Set-HcsNetInterface` cmdlet</span></span>

## <a name="modify-data-0-network-settings-through-setup-wizard"></a><span data-ttu-id="5a3dd-114">Modificare le impostazioni di rete di DATI 0 tramite la configurazione guidata</span><span class="sxs-lookup"><span data-stu-id="5a3dd-114">Modify DATA 0 network settings through setup wizard</span></span>
<span data-ttu-id="5a3dd-115">È possibile riconfigurare le impostazioni di rete di DATI 0 connettendosi all'interfaccia di Windows PowerShell del dispositivo StorSimple e avviando una sessione di configurazione guidata.</span><span class="sxs-lookup"><span data-stu-id="5a3dd-115">You can reconfigure DATA 0 network settings by connecting to the Windows PowerShell interface of your StorSimple device and launching a setup wizard session.</span></span> <span data-ttu-id="5a3dd-116">Eseguire i passaggi seguenti per modificare le impostazioni di DATI 0:</span><span class="sxs-lookup"><span data-stu-id="5a3dd-116">Perform the following steps to modify DATA 0 settings:</span></span>

#### <a name="to-modify-data-0-network-settings-through-setup-wizard"></a><span data-ttu-id="5a3dd-117">Per modificare le impostazioni di rete di DATI 0 tramite la configurazione guidata</span><span class="sxs-lookup"><span data-stu-id="5a3dd-117">To modify DATA 0 network settings through setup wizard</span></span>
1. <span data-ttu-id="5a3dd-118">Nel menu della console seriale, scegliere l'opzione 1, **Accedi con accesso completo**.</span><span class="sxs-lookup"><span data-stu-id="5a3dd-118">In the serial console menu, choose option 1, **Log in with full access**.</span></span> <span data-ttu-id="5a3dd-119">Quando richiesto, fornire la **password di amministratore del dispositivo**.</span><span class="sxs-lookup"><span data-stu-id="5a3dd-119">When prompted provide the **device administrator password**.</span></span> <span data-ttu-id="5a3dd-120">La password predefinita è `Password1`.</span><span class="sxs-lookup"><span data-stu-id="5a3dd-120">The default password is `Password1`.</span></span>
2. <span data-ttu-id="5a3dd-121">Al prompt dei comandi digitare:</span><span class="sxs-lookup"><span data-stu-id="5a3dd-121">At the command prompt, type:</span></span>
   
    `Invoke-HcsSetupWizard`
3. <span data-ttu-id="5a3dd-122">Verrà visualizzata una procedura guidata per configurare l'interfaccia DATA 0 del dispositivo.</span><span class="sxs-lookup"><span data-stu-id="5a3dd-122">A setup wizard appears to help configure the DATA 0 interface of your device.</span></span> <span data-ttu-id="5a3dd-123">Fornire nuovi valori per l'indirizzo IP, il gateway e la netmask.</span><span class="sxs-lookup"><span data-stu-id="5a3dd-123">Provide new values for the IP address, gateway, and netmask.</span></span>

> [!NOTE]
> <span data-ttu-id="5a3dd-124">Gli IP fissi dei controller dovranno essere riconfigurati tramite il pannello **Impostazioni di rete** del dispositivo StorSimple nel portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="5a3dd-124">The fixed controllers IPs will need to be reconfigured through the **Network settings** blade of the StorSimple device in the Azure portal.</span></span> <span data-ttu-id="5a3dd-125">Per ulteriori informazioni, andare a [Modificare le interfacce di rete](storsimple-8000-modify-device-config.md#modify-network-interfaces).</span><span class="sxs-lookup"><span data-stu-id="5a3dd-125">For more information, go to [Modify network interfaces](storsimple-8000-modify-device-config.md#modify-network-interfaces).</span></span>

## <a name="modify-data-0-network-settings-through-set-hcsnetinterface-cmdlet"></a><span data-ttu-id="5a3dd-126">Modificare le impostazioni di rete di DATI 0 tramite il cmdlet Set-HcsNetInterface</span><span class="sxs-lookup"><span data-stu-id="5a3dd-126">Modify DATA 0 network settings through Set-HcsNetInterface cmdlet</span></span>
<span data-ttu-id="5a3dd-127">Un modo alternativo per riconfigurare l'interfaccia di rete DATI 0 consiste nell'utilizzo del cmdlet `Set-HcsNetInterface` .</span><span class="sxs-lookup"><span data-stu-id="5a3dd-127">An alternate way to reconfigure DATA 0 network interface is through the use of the `Set-HcsNetInterface` cmdlet.</span></span> <span data-ttu-id="5a3dd-128">Il cmdlet viene eseguito dall'interfaccia di Windows PowerShell del dispositivo StorSimple.</span><span class="sxs-lookup"><span data-stu-id="5a3dd-128">The cmdlet is executed from the Windows PowerShell interface of your StorSimple device.</span></span> <span data-ttu-id="5a3dd-129">Quando si usa questa procedura, gli indirizzi IP fissi del controller possono essere anche configurati in questa posizione.</span><span class="sxs-lookup"><span data-stu-id="5a3dd-129">When using this procedure, the controller fixed IPs can also be configured here.</span></span> <span data-ttu-id="5a3dd-130">Eseguire i passaggi seguenti per modificare le impostazioni di DATI 0:</span><span class="sxs-lookup"><span data-stu-id="5a3dd-130">Perform the following steps to modify the DATA 0 settings:</span></span> 

#### <a name="to-modify-data-0-network-settings-through-the-set-hcsnetinterface-cmdlet"></a><span data-ttu-id="5a3dd-131">Per modificare le impostazioni di rete di DATI 0 tramite il cmdlet Set-HcsNetInterface</span><span class="sxs-lookup"><span data-stu-id="5a3dd-131">To modify DATA 0 network settings through the Set-HcsNetInterface cmdlet</span></span>
1. <span data-ttu-id="5a3dd-132">Nel menu della console seriale, scegliere l'opzione 1, **Accedi con accesso completo**.</span><span class="sxs-lookup"><span data-stu-id="5a3dd-132">In the serial console menu, choose option 1, **Log in with full access**.</span></span> <span data-ttu-id="5a3dd-133">Quando richiesto, fornire la password di amministratore del dispositivo.</span><span class="sxs-lookup"><span data-stu-id="5a3dd-133">When prompted provide the device administrator password.</span></span> <span data-ttu-id="5a3dd-134">La password predefinita è `Password1`.</span><span class="sxs-lookup"><span data-stu-id="5a3dd-134">The default password is `Password1`.</span></span>
2. <span data-ttu-id="5a3dd-135">Al prompt dei comandi digitare:</span><span class="sxs-lookup"><span data-stu-id="5a3dd-135">At the command prompt, type:</span></span>
   
    `Set-HCSNetInterface -InterfaceAlias Data0 -IPv4Address <> -IPv4Netmask <> -IPv4Gateway <> -Controller0IPv4Address <> -Controller1IPv4Address <> -IsiScsiEnabled 1 -IsCloudEnabled 1`
   
    <span data-ttu-id="5a3dd-136">Tra parentesi acute digitare i seguenti valori per DATA 0:</span><span class="sxs-lookup"><span data-stu-id="5a3dd-136">In the angled brackets, type the following values for DATA 0:</span></span>
   
   * <span data-ttu-id="5a3dd-137">Indirizzo IPv4</span><span class="sxs-lookup"><span data-stu-id="5a3dd-137">IPv4 address</span></span>
   * <span data-ttu-id="5a3dd-138">Gateway IPv4</span><span class="sxs-lookup"><span data-stu-id="5a3dd-138">IPv4 gateway</span></span>
   * <span data-ttu-id="5a3dd-139">Subnet mask IPv4</span><span class="sxs-lookup"><span data-stu-id="5a3dd-139">IPv4 subnet mask</span></span>
   * <span data-ttu-id="5a3dd-140">Indirizzo IPv4 fisso per controller 0</span><span class="sxs-lookup"><span data-stu-id="5a3dd-140">Fixed IPv4 address for Controller 0</span></span>
   * <span data-ttu-id="5a3dd-141">Indirizzo IPv4 fisso per controller 1</span><span class="sxs-lookup"><span data-stu-id="5a3dd-141">Fixed IPv4 address for Controller 1</span></span>
     
     <span data-ttu-id="5a3dd-142">Per altre informazioni su come usare questo cmdlet, vedere le [informazioni di riferimento sui cmdlet di Windows PowerShell per StorSimple](https://technet.microsoft.com/library/dn688161.aspx).</span><span class="sxs-lookup"><span data-stu-id="5a3dd-142">For more information on the use of this cmdlet, go to [Windows PowerShell for StorSimple cmdlet reference](https://technet.microsoft.com/library/dn688161.aspx).</span></span>

## <a name="next-steps"></a><span data-ttu-id="5a3dd-143">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="5a3dd-143">Next steps</span></span>
* <span data-ttu-id="5a3dd-144">Per configurare interfacce di rete diverse da DATA 0, vedere l'articolo su come [configurare le impostazioni di rete nel portale di Azure](storsimple-8000-modify-device-config.md).</span><span class="sxs-lookup"><span data-stu-id="5a3dd-144">To configure network interfaces other than DATA 0, you can use the [Configure network settings in the Azure portal](storsimple-8000-modify-device-config.md).</span></span> 
* <span data-ttu-id="5a3dd-145">Se si riscontrano problemi durante la configurazione delle interfacce di rete, fare riferimento a [Risoluzione dei problemi di distribuzione](storsimple-troubleshoot-deployment.md).</span><span class="sxs-lookup"><span data-stu-id="5a3dd-145">If you experience any issues when configuring your network interfaces, refer to [Troubleshoot deployment issues](storsimple-troubleshoot-deployment.md).</span></span>


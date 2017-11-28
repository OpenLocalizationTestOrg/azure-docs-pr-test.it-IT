---
title: DATA 0 aaaModify le impostazioni nel dispositivo StorSimple serie 8000 | Documenti Microsoft
description: Informazioni su come toouse Windows PowerShell per StorSimple tooreconfigure hello dati interfaccia di rete 0 nel dispositivo StorSimple.
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
ms.openlocfilehash: 2d3bdd3675017be86def45a81d94b6c03fc61da6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="modify-hello-data-0-network-interface-settings-on-your-storsimple-8000-series-device"></a><span data-ttu-id="d228b-103">Modificare le impostazioni dell'interfaccia di rete 0 di hello dati sul dispositivo serie StorSimple 8000</span><span class="sxs-lookup"><span data-stu-id="d228b-103">Modify hello DATA 0 network interface settings on your StorSimple 8000 series device</span></span>

## <a name="overview"></a><span data-ttu-id="d228b-104">Panoramica</span><span class="sxs-lookup"><span data-stu-id="d228b-104">Overview</span></span>

<span data-ttu-id="d228b-105">Il dispositivo StorSimple di Microsoft Azure ha sei interfacce di rete, da DATA 0 tooDATA 5.</span><span class="sxs-lookup"><span data-stu-id="d228b-105">Your Microsoft Azure StorSimple device has six network interfaces, from DATA 0 tooDATA 5.</span></span> <span data-ttu-id="d228b-106">Hello DATA 0 è sempre configurata tramite l'interfaccia di Windows PowerShell hello o la console seriale hello interfaccia ed è automaticamente abilitata per il cloud.</span><span class="sxs-lookup"><span data-stu-id="d228b-106">hello DATA 0 interface is always configured through hello Windows PowerShell interface or hello serial console, and is automatically cloud-enabled.</span></span> <span data-ttu-id="d228b-107">Si noti che non è possibile configurare l'interfaccia di rete 0 dati tramite hello portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="d228b-107">Note that you cannot configure DATA 0 network interface through hello Azure portal.</span></span>

<span data-ttu-id="d228b-108">DATA 0 interfaccia viene prima configurata mediante Installazione guidata di hello durante la distribuzione iniziale del dispositivo StorSimple hello Hello.</span><span class="sxs-lookup"><span data-stu-id="d228b-108">hello DATA 0 interface is first configured through hello setup wizard during initial deployment of hello StorSimple device.</span></span> <span data-ttu-id="d228b-109">Quando il dispositivo di hello è in modalità operativa, potrebbe essere necessario tooreconfigure DATA 0 impostazioni.</span><span class="sxs-lookup"><span data-stu-id="d228b-109">When hello device is in an operational mode, you may need tooreconfigure DATA 0 settings.</span></span> <span data-ttu-id="d228b-110">In questa esercitazione sono disponibili due metodi toomodify dati 0 le impostazioni di rete, sia tramite Windows PowerShell per StorSimple.</span><span class="sxs-lookup"><span data-stu-id="d228b-110">This tutorial provides two methods toomodify DATA 0 network settings, both through Windows PowerShell for StorSimple.</span></span>

<span data-ttu-id="d228b-111">Dopo aver letto questa esercitazione, si sarà in grado di:</span><span class="sxs-lookup"><span data-stu-id="d228b-111">After reading this tutorial, you will be able to:</span></span>

* <span data-ttu-id="d228b-112">Modificare i dati 0 impostazione tramite installazione guidata di hello di rete</span><span class="sxs-lookup"><span data-stu-id="d228b-112">Modify DATA 0 network setting through hello setup wizard</span></span>
* <span data-ttu-id="d228b-113">Modificare le impostazioni di rete 0 dati tramite hello `Set-HcsNetInterface` cmdlet</span><span class="sxs-lookup"><span data-stu-id="d228b-113">Modify DATA 0 network settings through hello `Set-HcsNetInterface` cmdlet</span></span>

## <a name="modify-data-0-network-settings-through-setup-wizard"></a><span data-ttu-id="d228b-114">Modificare le impostazioni di rete di DATI 0 tramite la configurazione guidata</span><span class="sxs-lookup"><span data-stu-id="d228b-114">Modify DATA 0 network settings through setup wizard</span></span>
<span data-ttu-id="d228b-115">È possibile riconfigurare le impostazioni di rete 0 dati collegando toohello interfaccia di Windows PowerShell del dispositivo StorSimple e avviare una sessione della procedura guidata configurazione.</span><span class="sxs-lookup"><span data-stu-id="d228b-115">You can reconfigure DATA 0 network settings by connecting toohello Windows PowerShell interface of your StorSimple device and launching a setup wizard session.</span></span> <span data-ttu-id="d228b-116">Eseguire i seguenti passaggi toomodify DATA 0 hello impostazioni:</span><span class="sxs-lookup"><span data-stu-id="d228b-116">Perform hello following steps toomodify DATA 0 settings:</span></span>

#### <a name="toomodify-data-0-network-settings-through-setup-wizard"></a><span data-ttu-id="d228b-117">impostazioni di rete 0 toomodify dati tramite installazione guidata</span><span class="sxs-lookup"><span data-stu-id="d228b-117">toomodify DATA 0 network settings through setup wizard</span></span>
1. <span data-ttu-id="d228b-118">Nel menu della console seriale hello, selezionare l'opzione 1, **Accedi con accesso completo**.</span><span class="sxs-lookup"><span data-stu-id="d228b-118">In hello serial console menu, choose option 1, **Log in with full access**.</span></span> <span data-ttu-id="d228b-119">Quando richiesto specificare hello **password amministratore del dispositivo**.</span><span class="sxs-lookup"><span data-stu-id="d228b-119">When prompted provide hello **device administrator password**.</span></span> <span data-ttu-id="d228b-120">password predefinita Hello è `Password1`.</span><span class="sxs-lookup"><span data-stu-id="d228b-120">hello default password is `Password1`.</span></span>
2. <span data-ttu-id="d228b-121">Al prompt dei comandi di hello, digitare:</span><span class="sxs-lookup"><span data-stu-id="d228b-121">At hello command prompt, type:</span></span>
   
    `Invoke-HcsSetupWizard`
3. <span data-ttu-id="d228b-122">Una procedura guidata viene visualizzato toohelp configurare hello DATA 0 interfaccia del dispositivo.</span><span class="sxs-lookup"><span data-stu-id="d228b-122">A setup wizard appears toohelp configure hello DATA 0 interface of your device.</span></span> <span data-ttu-id="d228b-123">Fornire nuovi valori per la subnet mask, gateway e l'indirizzo IP hello.</span><span class="sxs-lookup"><span data-stu-id="d228b-123">Provide new values for hello IP address, gateway, and netmask.</span></span>

> [!NOTE]
> <span data-ttu-id="d228b-124">Hello fissato controller gli indirizzi IP saranno necessario riconfigurare tramite hello toobe **le impostazioni di rete** pannello del dispositivo StorSimple hello in hello portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="d228b-124">hello fixed controllers IPs will need toobe reconfigured through hello **Network settings** blade of hello StorSimple device in hello Azure portal.</span></span> <span data-ttu-id="d228b-125">Per ulteriori informazioni, visitare troppo[modificare interfacce di rete](storsimple-8000-modify-device-config.md#modify-network-interfaces).</span><span class="sxs-lookup"><span data-stu-id="d228b-125">For more information, go too[Modify network interfaces](storsimple-8000-modify-device-config.md#modify-network-interfaces).</span></span>

## <a name="modify-data-0-network-settings-through-set-hcsnetinterface-cmdlet"></a><span data-ttu-id="d228b-126">Modificare le impostazioni di rete di DATI 0 tramite il cmdlet Set-HcsNetInterface</span><span class="sxs-lookup"><span data-stu-id="d228b-126">Modify DATA 0 network settings through Set-HcsNetInterface cmdlet</span></span>
<span data-ttu-id="d228b-127">Un tooreconfigure alternativa DATA 0 è l'interfaccia di rete tramite l'utilizzo di hello di hello `Set-HcsNetInterface` cmdlet.</span><span class="sxs-lookup"><span data-stu-id="d228b-127">An alternate way tooreconfigure DATA 0 network interface is through hello use of hello `Set-HcsNetInterface` cmdlet.</span></span> <span data-ttu-id="d228b-128">esecuzione del cmdlet Hello dall'interfaccia di Windows PowerShell hello del dispositivo StorSimple.</span><span class="sxs-lookup"><span data-stu-id="d228b-128">hello cmdlet is executed from hello Windows PowerShell interface of your StorSimple device.</span></span> <span data-ttu-id="d228b-129">Quando si utilizza questa procedura, IP fissato dei controller hello inoltre è possibile configurare.</span><span class="sxs-lookup"><span data-stu-id="d228b-129">When using this procedure, hello controller fixed IPs can also be configured here.</span></span> <span data-ttu-id="d228b-130">Eseguire i seguenti passaggi toomodify hello DATA 0 hello impostazioni:</span><span class="sxs-lookup"><span data-stu-id="d228b-130">Perform hello following steps toomodify hello DATA 0 settings:</span></span> 

#### <a name="toomodify-data-0-network-settings-through-hello-set-hcsnetinterface-cmdlet"></a><span data-ttu-id="d228b-131">impostazioni di rete 0 toomodify dati tramite il cmdlet Set-HcsNetInterface hello</span><span class="sxs-lookup"><span data-stu-id="d228b-131">toomodify DATA 0 network settings through hello Set-HcsNetInterface cmdlet</span></span>
1. <span data-ttu-id="d228b-132">Nel menu della console seriale hello, selezionare l'opzione 1, **Accedi con accesso completo**.</span><span class="sxs-lookup"><span data-stu-id="d228b-132">In hello serial console menu, choose option 1, **Log in with full access**.</span></span> <span data-ttu-id="d228b-133">Quando richiesto specificare password amministratore del dispositivo hello.</span><span class="sxs-lookup"><span data-stu-id="d228b-133">When prompted provide hello device administrator password.</span></span> <span data-ttu-id="d228b-134">password predefinita Hello è `Password1`.</span><span class="sxs-lookup"><span data-stu-id="d228b-134">hello default password is `Password1`.</span></span>
2. <span data-ttu-id="d228b-135">Al prompt dei comandi di hello, digitare:</span><span class="sxs-lookup"><span data-stu-id="d228b-135">At hello command prompt, type:</span></span>
   
    `Set-HCSNetInterface -InterfaceAlias Data0 -IPv4Address <> -IPv4Netmask <> -IPv4Gateway <> -Controller0IPv4Address <> -Controller1IPv4Address <> -IsiScsiEnabled 1 -IsCloudEnabled 1`
   
    <span data-ttu-id="d228b-136">Tra parentesi quadre hello con angolata, digitare hello seguenti valori per DATA 0:</span><span class="sxs-lookup"><span data-stu-id="d228b-136">In hello angled brackets, type hello following values for DATA 0:</span></span>
   
   * <span data-ttu-id="d228b-137">Indirizzo IPv4</span><span class="sxs-lookup"><span data-stu-id="d228b-137">IPv4 address</span></span>
   * <span data-ttu-id="d228b-138">Gateway IPv4</span><span class="sxs-lookup"><span data-stu-id="d228b-138">IPv4 gateway</span></span>
   * <span data-ttu-id="d228b-139">Subnet mask IPv4</span><span class="sxs-lookup"><span data-stu-id="d228b-139">IPv4 subnet mask</span></span>
   * <span data-ttu-id="d228b-140">Indirizzo IPv4 fisso per controller 0</span><span class="sxs-lookup"><span data-stu-id="d228b-140">Fixed IPv4 address for Controller 0</span></span>
   * <span data-ttu-id="d228b-141">Indirizzo IPv4 fisso per controller 1</span><span class="sxs-lookup"><span data-stu-id="d228b-141">Fixed IPv4 address for Controller 1</span></span>
     
     <span data-ttu-id="d228b-142">Per ulteriori informazioni sull'utilizzo di hello di questo cmdlet, vedere troppo[di Windows PowerShell per StorSimple cmdlet riferimento](https://technet.microsoft.com/library/dn688161.aspx).</span><span class="sxs-lookup"><span data-stu-id="d228b-142">For more information on hello use of this cmdlet, go too[Windows PowerShell for StorSimple cmdlet reference](https://technet.microsoft.com/library/dn688161.aspx).</span></span>

## <a name="next-steps"></a><span data-ttu-id="d228b-143">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="d228b-143">Next steps</span></span>
* <span data-ttu-id="d228b-144">interfacce di rete tooconfigure diverse da DATA 0, è possibile utilizzare hello [configurare le impostazioni di rete nel portale di Azure hello](storsimple-8000-modify-device-config.md).</span><span class="sxs-lookup"><span data-stu-id="d228b-144">tooconfigure network interfaces other than DATA 0, you can use hello [Configure network settings in hello Azure portal](storsimple-8000-modify-device-config.md).</span></span> 
* <span data-ttu-id="d228b-145">Se si verificano problemi durante la configurazione delle interfacce di rete, fare riferimento troppo[risolvere i problemi di distribuzione](storsimple-troubleshoot-deployment.md).</span><span class="sxs-lookup"><span data-stu-id="d228b-145">If you experience any issues when configuring your network interfaces, refer too[Troubleshoot deployment issues](storsimple-troubleshoot-deployment.md).</span></span>


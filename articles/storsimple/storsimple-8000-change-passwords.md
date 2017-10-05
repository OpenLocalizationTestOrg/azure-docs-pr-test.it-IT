---
title: Modificare le password di StorSimple | Microsoft Docs
description: Descrive come usare il servizio Gestione dispositivi StorSimple per modificare le password di StorSimple Snapshot Manager e di amministratore del dispositivo.
services: storsimple
documentationcenter: NA
author: alkohli
manager: timlt
editor: 
ms.assetid: 
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: TBD
ms.date: 07/03/2017
ms.author: alkohli
ms.openlocfilehash: 7762f8499c67672f0a2ffed99e98baea4c940fa0
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="use-the-storsimple-device-manager-service-to-change-your-storsimple-passwords"></a><span data-ttu-id="aef40-103">Usare il servizio Gestione dispositivi StorSimple per modificare le password di StorSimple</span><span class="sxs-lookup"><span data-stu-id="aef40-103">Use the StorSimple Device Manager service to change your StorSimple passwords</span></span>

## <a name="overview"></a><span data-ttu-id="aef40-104">Panoramica</span><span class="sxs-lookup"><span data-stu-id="aef40-104">Overview</span></span>
<span data-ttu-id="aef40-105">L'opzione **Impostazioni del dispositivo** del portale di Azure contiene tutti i parametri del dispositivo che è possibile riconfigurare in un dispositivo StorSimple gestito da un servizio Gestione dispositivi StorSimple.</span><span class="sxs-lookup"><span data-stu-id="aef40-105">The Azure portal **Device settings** option contains all the device parameters that you can reconfigure on a StorSimple device that is managed by a StorSimple Device Manager service.</span></span> <span data-ttu-id="aef40-106">In questa esercitazione viene illustrato come usare l'opzione **Sicurezza** in **Impostazioni dispositivo** per modificare la password dell'amministratore del dispositivo o di StorSimple Snapshot Manager.</span><span class="sxs-lookup"><span data-stu-id="aef40-106">This tutorial explains how you can use the **Security** option under **Device settings** to change your device administrator or StorSimple Snapshot Manager password.</span></span>

## <a name="change-the-device-administrator-password"></a><span data-ttu-id="aef40-107">Configurare la password dell’amministratore del dispositivo</span><span class="sxs-lookup"><span data-stu-id="aef40-107">Change the device administrator password</span></span>
<span data-ttu-id="aef40-108">Quando si utilizza l'interfaccia di Windows PowerShell per accedere al dispositivo StorSimple, è necessario immettere una password amministratore del dispositivo.</span><span class="sxs-lookup"><span data-stu-id="aef40-108">When you use Windows PowerShell interface to access the StorSimple device, you are required to enter a device administrator password.</span></span> <span data-ttu-id="aef40-109">Quando il primo dispositivo StorSimple è registrato con un servizio, la password predefinita per questa interfaccia è *Password1*.</span><span class="sxs-lookup"><span data-stu-id="aef40-109">When the first StorSimple device is registered with a service, the default password for this interface is *Password1*.</span></span> <span data-ttu-id="aef40-110">Per la protezione dei dati, è necessario modificare la password al termine del processo di registrazione.</span><span class="sxs-lookup"><span data-stu-id="aef40-110">For the security of your data, you are required to change this password at the end of the registration process.</span></span> <span data-ttu-id="aef40-111">Non è possibile uscire dal processo di registrazione senza modificare la password.</span><span class="sxs-lookup"><span data-stu-id="aef40-111">You cannot exit from the registration process without changing this password.</span></span> <span data-ttu-id="aef40-112">Per altre informazioni, vedere [Passaggio 3: Configurare e registrare il dispositivo tramite Windows PowerShell per StorSimple](storsimple-8000-deployment-walkthrough-u2.md#step-3-configure-and-register-the-device-through-windows-powershell-for-storsimple).</span><span class="sxs-lookup"><span data-stu-id="aef40-112">For more information, see [Step 3: Configure and register the device through Windows PowerShell for StorSimple](storsimple-8000-deployment-walkthrough-u2.md#step-3-configure-and-register-the-device-through-windows-powershell-for-storsimple).</span></span>

<span data-ttu-id="aef40-113">La password impostata la prima volta durante la registrazione attraverso l'interfaccia di Windows PowerShell può essere modificata successivamente tramite il portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="aef40-113">The password that was first set through the Windows PowerShell interface during registration can be changed later via the Azure portal.</span></span> <span data-ttu-id="aef40-114">Eseguire i passaggi seguenti per modificare la password di amministratore del dispositivo.</span><span class="sxs-lookup"><span data-stu-id="aef40-114">Perform the following steps to change the device administrator password.</span></span>

#### <a name="to-change-the-device-administrator-password"></a><span data-ttu-id="aef40-115">Per configurare la password dell’amministratore del dispositivo</span><span class="sxs-lookup"><span data-stu-id="aef40-115">To change the device administrator password</span></span>
1. <span data-ttu-id="aef40-116">Passare al servizio Gestione dispositivi StorSimple e fare clic su **Dispositivi**.</span><span class="sxs-lookup"><span data-stu-id="aef40-116">Go to your StorSimple Device Manager service and click **Devices**.</span></span>

2. <span data-ttu-id="aef40-117">Nell'elenco tabulare dei dispositivi, selezionare e fare clic sul dispositivo di cui si vuole modificare la password.</span><span class="sxs-lookup"><span data-stu-id="aef40-117">From the tabular listing of devices, select and click the device whose password you intend to change.</span></span>

    ![](./media/storsimple-8000-change-passwords/changepwd1.png)

3. <span data-ttu-id="aef40-118">Nel pannello **Impostazioni**, passare a **Impostazioni dispositivo > Sicurezza**.</span><span class="sxs-lookup"><span data-stu-id="aef40-118">In the **Settings** blade, go to **Device settings > Security**.</span></span>

    ![](./media/storsimple-8000-change-passwords/changepwd2.png)

4. <span data-ttu-id="aef40-119">Nel pannello **Impostazioni di sicurezza**, fare clic su **Password** per modificare la password di amministratore del dispositivo.</span><span class="sxs-lookup"><span data-stu-id="aef40-119">In the **Security settings** blade, click **Password** to change the device administrator password.</span></span>

    ![](./media/storsimple-8000-change-passwords/changepwd3.png)

5. <span data-ttu-id="aef40-120">Nel pannello **Password**, specificare una password di amministratore contenente dagli 8 ai 15 caratteri.</span><span class="sxs-lookup"><span data-stu-id="aef40-120">In the **Password** blade, provide an administrator password that contains from 8 to 15 characters.</span></span> <span data-ttu-id="aef40-121">La password deve contenere una combinazione di 3 o più lettere maiuscole, minuscole, numeri e caratteri speciali.</span><span class="sxs-lookup"><span data-stu-id="aef40-121">The password must be a combination of 3 or more of uppercase, lowercase, numeric, and special characters.</span></span>

6. <span data-ttu-id="aef40-122">Confermare la password.</span><span class="sxs-lookup"><span data-stu-id="aef40-122">Confirm the password.</span></span>

    ![](./media/storsimple-8000-change-passwords/changepwd4.png)

7. <span data-ttu-id="aef40-123">Alla richiesta di conferma fare clic su **Salva** e quindi su **Sì**.</span><span class="sxs-lookup"><span data-stu-id="aef40-123">Click **Save** and when prompted for confirmation, click **Yes**.</span></span>

    ![](./media/storsimple-8000-change-passwords/changepwd6.png)

<span data-ttu-id="aef40-124">A questo punto, la password amministratore del dispositivo dovrebbe essere aggiornata.</span><span class="sxs-lookup"><span data-stu-id="aef40-124">The device administrator password should now be updated.</span></span> <span data-ttu-id="aef40-125">È possibile utilizzare la password modificata per accedere all'interfaccia di Windows PowerShell.</span><span class="sxs-lookup"><span data-stu-id="aef40-125">You can use this modified password to access the Windows PowerShell interface.</span></span>

## <a name="set-the-storsimple-snapshot-manager-password"></a><span data-ttu-id="aef40-126">Configurare la password di StorSimple Snapshot Manager</span><span class="sxs-lookup"><span data-stu-id="aef40-126">Set the StorSimple Snapshot Manager password</span></span>
<span data-ttu-id="aef40-127">Il software di Gestione snapshot StorSimple si trova nell'host di Windows e consente agli amministratori di gestire i backup del dispositivo StorSimple sotto forma di snapshot locali e cloud.</span><span class="sxs-lookup"><span data-stu-id="aef40-127">StorSimple Snapshot Manager software resides on your Windows host and allows administrators to manage backups of your StorSimple device in the form of local and cloud snapshots.</span></span>

<span data-ttu-id="aef40-128">Quando si configura un dispositivo in StorSimple Snapshot Manager, verrà richiesto di specificare l'indirizzo IP del dispositivo e la password per autenticare il dispositivo di archiviazione.</span><span class="sxs-lookup"><span data-stu-id="aef40-128">When configuring a device in StorSimple Snapshot Manager, you will be prompted to provide the device IP address and password to authenticate your storage device.</span></span>

<span data-ttu-id="aef40-129">È possibile impostare o modificare la password di StorSimple Snapshot Manager nel portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="aef40-129">You can set or change the password for StorSimple Snapshot Manager via the Azure portal.</span></span> <span data-ttu-id="aef40-130">Attenersi alla procedura seguente per modificare la password di StorSimple Snapshot Manager.</span><span class="sxs-lookup"><span data-stu-id="aef40-130">Perform the following steps to set or change the StorSimple Snapshot Manager password.</span></span>

#### <a name="to-set-the-storsimple-snapshot-manager-password"></a><span data-ttu-id="aef40-131">Per configurare la password di StorSimple Snapshot Manager</span><span class="sxs-lookup"><span data-stu-id="aef40-131">To set the StorSimple Snapshot Manager password</span></span>
1. <span data-ttu-id="aef40-132">Passare al servizio Gestione dispositivi StorSimple e fare clic su **Dispositivi**.</span><span class="sxs-lookup"><span data-stu-id="aef40-132">Go to your StorSimple Device Manager service and click **Devices**.</span></span>

2. <span data-ttu-id="aef40-133">Nell'elenco tabulare dei dispositivi, selezionare e fare clic sul dispositivo di cui si vuole modificare la password di StorSimple Snapshot Manager.</span><span class="sxs-lookup"><span data-stu-id="aef40-133">From the tabular listing of devices, select and click the device whose StorSimple Snapshot Manager password you intend to set or change.</span></span>

     ![](./media/storsimple-8000-change-passwords/changepwd1.png)

3. <span data-ttu-id="aef40-134">Nel pannello **Impostazioni**, passare a **Impostazioni dispositivo > Sicurezza**.</span><span class="sxs-lookup"><span data-stu-id="aef40-134">In the **Settings** blade, go to **Device settings > Security**.</span></span>

     ![](./media/storsimple-8000-change-passwords/changepwd2.png)

4. <span data-ttu-id="aef40-135">Nel pannello **le Impostazioni di protezione**, fare clic su **Password** per impostare o modificare la password di StorSimple Snapshot Manager.</span><span class="sxs-lookup"><span data-stu-id="aef40-135">In the **Security settings** blade, click **Password** to set or change the StorSimple Snapshot Manager password.</span></span>

     ![](./media/storsimple-8000-change-passwords/changepwd3.png) 

5. <span data-ttu-id="aef40-136">Nel pannello **Password** immettere una password composta da 14 o 15 caratteri.</span><span class="sxs-lookup"><span data-stu-id="aef40-136">In the **Password** blade, enter a password that is 14 or 15 characters.</span></span> <span data-ttu-id="aef40-137">Assicurarsi che la password contenga una combinazione di 3 o più lettere maiuscole, minuscole, numeri e caratteri speciali.</span><span class="sxs-lookup"><span data-stu-id="aef40-137">Make sure that the password contains a combination of 3 or more of uppercase, lowercase, numeric, and special characters.</span></span>

6. <span data-ttu-id="aef40-138">Confermare la password.</span><span class="sxs-lookup"><span data-stu-id="aef40-138">Confirm the password.</span></span>

     ![](./media/storsimple-8000-change-passwords/changepwd5.png)

7. <span data-ttu-id="aef40-139">Alla richiesta di conferma fare clic su **Salva** e quindi su **Sì**.</span><span class="sxs-lookup"><span data-stu-id="aef40-139">Click **Save** and when prompted for confirmation, click **Yes**.</span></span>

     ![](./media/storsimple-8000-change-passwords/changepwd6.png)

<span data-ttu-id="aef40-140">La password di StorSimple Snapshot Manager ora deve essere aggiornata.</span><span class="sxs-lookup"><span data-stu-id="aef40-140">The StorSimple Snapshot Manager password should now be updated.</span></span>

## <a name="next-steps"></a><span data-ttu-id="aef40-141">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="aef40-141">Next steps</span></span>
* <span data-ttu-id="aef40-142">Ulteriori informazioni sulla [sicurezza di StorSimple](storsimple-8000-security.md).</span><span class="sxs-lookup"><span data-stu-id="aef40-142">Learn more about [StorSimple security](storsimple-8000-security.md).</span></span>
* <span data-ttu-id="aef40-143">[Ulteriori informazioni su come modificare la configurazione del dispositivo](storsimple-8000-modify-device-config.md).</span><span class="sxs-lookup"><span data-stu-id="aef40-143">Learn more about [modifying your device configuration](storsimple-8000-modify-device-config.md).</span></span>
* <span data-ttu-id="aef40-144">Altre informazioni sull'[utilizzo del servizio Gestione dispositivi StorSimple per la gestione del dispositivo StorSimple](storsimple-8000-manager-service-administration.md).</span><span class="sxs-lookup"><span data-stu-id="aef40-144">Learn more about [using the StorSimple Device Manager service to administer your StorSimple device](storsimple-8000-manager-service-administration.md).</span></span>


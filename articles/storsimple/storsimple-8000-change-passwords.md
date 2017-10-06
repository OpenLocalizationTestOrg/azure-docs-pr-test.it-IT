---
title: aaaChange le password di StorSimple | Documenti Microsoft
description: Viene descritto come toouse hello toochange servizio di gestione di dispositivi StorSimple le password di amministratore di StorSimple Snapshot Manager e dispositivo.
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
ms.openlocfilehash: cf884be31b4bbf9e372c0aa11b9da2eadcda35dd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="use-hello-storsimple-device-manager-service-toochange-your-storsimple-passwords"></a><span data-ttu-id="bfff9-103">Utilizzare toochange servizio di gestione di dispositivi StorSimple hello le password di StorSimple</span><span class="sxs-lookup"><span data-stu-id="bfff9-103">Use hello StorSimple Device Manager service toochange your StorSimple passwords</span></span>

## <a name="overview"></a><span data-ttu-id="bfff9-104">Panoramica</span><span class="sxs-lookup"><span data-stu-id="bfff9-104">Overview</span></span>
<span data-ttu-id="bfff9-105">portale di Azure Hello **le impostazioni del dispositivo** opzione contiene tutti i parametri di dispositivo hello che è possibile riconfigurare in un dispositivo StorSimple è gestito da un servizio di gestione di dispositivi StorSimple.</span><span class="sxs-lookup"><span data-stu-id="bfff9-105">hello Azure portal **Device settings** option contains all hello device parameters that you can reconfigure on a StorSimple device that is managed by a StorSimple Device Manager service.</span></span> <span data-ttu-id="bfff9-106">In questa esercitazione viene illustrato come utilizzare hello **sicurezza** opzione **le impostazioni del dispositivo** toochange all'amministratore del dispositivo o la password di gestione Snapshot StorSimple.</span><span class="sxs-lookup"><span data-stu-id="bfff9-106">This tutorial explains how you can use hello **Security** option under **Device settings** toochange your device administrator or StorSimple Snapshot Manager password.</span></span>

## <a name="change-hello-device-administrator-password"></a><span data-ttu-id="bfff9-107">Password amministratore del dispositivo hello modifica</span><span class="sxs-lookup"><span data-stu-id="bfff9-107">Change hello device administrator password</span></span>
<span data-ttu-id="bfff9-108">Quando si usa il dispositivo StorSimple hello di Windows PowerShell interfaccia tooaccess, verrà richiesto tooenter una password amministratore del dispositivo.</span><span class="sxs-lookup"><span data-stu-id="bfff9-108">When you use Windows PowerShell interface tooaccess hello StorSimple device, you are required tooenter a device administrator password.</span></span> <span data-ttu-id="bfff9-109">Quando il dispositivo StorSimple prima di hello viene registrato con un servizio, la password di hello predefinito per questa interfaccia è *Password1*.</span><span class="sxs-lookup"><span data-stu-id="bfff9-109">When hello first StorSimple device is registered with a service, hello default password for this interface is *Password1*.</span></span> <span data-ttu-id="bfff9-110">Per sicurezza hello dei dati, si è obbligatorio toochange la password al fine di hello hello del processo di registrazione.</span><span class="sxs-lookup"><span data-stu-id="bfff9-110">For hello security of your data, you are required toochange this password at hello end of hello registration process.</span></span> <span data-ttu-id="bfff9-111">È possibile uscire dal processo di registrazione hello senza cambiare la password.</span><span class="sxs-lookup"><span data-stu-id="bfff9-111">You cannot exit from hello registration process without changing this password.</span></span> <span data-ttu-id="bfff9-112">Per ulteriori informazioni, vedere [passaggio 3: configurare e registrare il dispositivo hello tramite Windows PowerShell per StorSimple](storsimple-8000-deployment-walkthrough-u2.md#step-3-configure-and-register-the-device-through-windows-powershell-for-storsimple).</span><span class="sxs-lookup"><span data-stu-id="bfff9-112">For more information, see [Step 3: Configure and register hello device through Windows PowerShell for StorSimple](storsimple-8000-deployment-walkthrough-u2.md#step-3-configure-and-register-the-device-through-windows-powershell-for-storsimple).</span></span>

<span data-ttu-id="bfff9-113">Hello prima impostato tramite l'interfaccia di Windows PowerShell hello durante la registrazione può essere cambiata in un secondo momento tramite hello portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="bfff9-113">hello password that was first set through hello Windows PowerShell interface during registration can be changed later via hello Azure portal.</span></span> <span data-ttu-id="bfff9-114">Eseguire hello password amministratore del dispositivo hello toochange i passaggi seguenti.</span><span class="sxs-lookup"><span data-stu-id="bfff9-114">Perform hello following steps toochange hello device administrator password.</span></span>

#### <a name="toochange-hello-device-administrator-password"></a><span data-ttu-id="bfff9-115">password amministratore del dispositivo hello toochange</span><span class="sxs-lookup"><span data-stu-id="bfff9-115">toochange hello device administrator password</span></span>
1. <span data-ttu-id="bfff9-116">Il servizio di gestione di dispositivi StorSimple tooyour, fare clic su **dispositivi**.</span><span class="sxs-lookup"><span data-stu-id="bfff9-116">Go tooyour StorSimple Device Manager service and click **Devices**.</span></span>

2. <span data-ttu-id="bfff9-117">Dall'elenco tabulare di hello delle periferiche, selezionare e fare clic su dispositivo hello cui password intendi toochange.</span><span class="sxs-lookup"><span data-stu-id="bfff9-117">From hello tabular listing of devices, select and click hello device whose password you intend toochange.</span></span>

    ![](./media/storsimple-8000-change-passwords/changepwd1.png)

3. <span data-ttu-id="bfff9-118">In hello **impostazioni** pannello andare troppo**le impostazioni del dispositivo > sicurezza**.</span><span class="sxs-lookup"><span data-stu-id="bfff9-118">In hello **Settings** blade, go too**Device settings > Security**.</span></span>

    ![](./media/storsimple-8000-change-passwords/changepwd2.png)

4. <span data-ttu-id="bfff9-119">In hello **le impostazioni di sicurezza** pannello, fare clic su **Password** password amministratore del dispositivo toochange hello.</span><span class="sxs-lookup"><span data-stu-id="bfff9-119">In hello **Security settings** blade, click **Password** toochange hello device administrator password.</span></span>

    ![](./media/storsimple-8000-change-passwords/changepwd3.png)

5. <span data-ttu-id="bfff9-120">In hello **Password** pannello, specificare una password amministratore contenente dagli 8 too15 caratteri.</span><span class="sxs-lookup"><span data-stu-id="bfff9-120">In hello **Password** blade, provide an administrator password that contains from 8 too15 characters.</span></span> <span data-ttu-id="bfff9-121">password di Hello deve essere una combinazione di 3 o più dei caratteri maiuscoli, minuscoli, numerici e speciali.</span><span class="sxs-lookup"><span data-stu-id="bfff9-121">hello password must be a combination of 3 or more of uppercase, lowercase, numeric, and special characters.</span></span>

6. <span data-ttu-id="bfff9-122">Conferma password hello.</span><span class="sxs-lookup"><span data-stu-id="bfff9-122">Confirm hello password.</span></span>

    ![](./media/storsimple-8000-change-passwords/changepwd4.png)

7. <span data-ttu-id="bfff9-123">Alla richiesta di conferma fare clic su **Salva** e quindi su **Sì**.</span><span class="sxs-lookup"><span data-stu-id="bfff9-123">Click **Save** and when prompted for confirmation, click **Yes**.</span></span>

    ![](./media/storsimple-8000-change-passwords/changepwd6.png)

<span data-ttu-id="bfff9-124">password amministratore del dispositivo Hello dovrebbe ora essere aggiornata.</span><span class="sxs-lookup"><span data-stu-id="bfff9-124">hello device administrator password should now be updated.</span></span> <span data-ttu-id="bfff9-125">È possibile utilizzare questa interfaccia di Windows PowerShell hello tooaccess password modificata.</span><span class="sxs-lookup"><span data-stu-id="bfff9-125">You can use this modified password tooaccess hello Windows PowerShell interface.</span></span>

## <a name="set-hello-storsimple-snapshot-manager-password"></a><span data-ttu-id="bfff9-126">Impostare la password di StorSimple Snapshot Manager hello</span><span class="sxs-lookup"><span data-stu-id="bfff9-126">Set hello StorSimple Snapshot Manager password</span></span>
<span data-ttu-id="bfff9-127">Software di gestione Snapshot StorSimple risiede nell'host di Windows e consente agli amministratori di backup toomanage del dispositivo StorSimple in forma di hello di locale e gli snapshot cloud.</span><span class="sxs-lookup"><span data-stu-id="bfff9-127">StorSimple Snapshot Manager software resides on your Windows host and allows administrators toomanage backups of your StorSimple device in hello form of local and cloud snapshots.</span></span>

<span data-ttu-id="bfff9-128">Quando si configura un dispositivo StorSimple Snapshot Manager, verrà richiesto tooprovide hello tooauthenticate di password e l'indirizzo IP dispositivo del dispositivo di archiviazione.</span><span class="sxs-lookup"><span data-stu-id="bfff9-128">When configuring a device in StorSimple Snapshot Manager, you will be prompted tooprovide hello device IP address and password tooauthenticate your storage device.</span></span>

<span data-ttu-id="bfff9-129">È possibile impostare o modificare password hello gestione Snapshot StorSimple tramite hello portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="bfff9-129">You can set or change hello password for StorSimple Snapshot Manager via hello Azure portal.</span></span> <span data-ttu-id="bfff9-130">Eseguire i seguenti passaggi tooset hello o modificare la password di StorSimple Snapshot Manager hello.</span><span class="sxs-lookup"><span data-stu-id="bfff9-130">Perform hello following steps tooset or change hello StorSimple Snapshot Manager password.</span></span>

#### <a name="tooset-hello-storsimple-snapshot-manager-password"></a><span data-ttu-id="bfff9-131">password di StorSimple Snapshot Manager hello tooset</span><span class="sxs-lookup"><span data-stu-id="bfff9-131">tooset hello StorSimple Snapshot Manager password</span></span>
1. <span data-ttu-id="bfff9-132">Il servizio di gestione di dispositivi StorSimple tooyour, fare clic su **dispositivi**.</span><span class="sxs-lookup"><span data-stu-id="bfff9-132">Go tooyour StorSimple Device Manager service and click **Devices**.</span></span>

2. <span data-ttu-id="bfff9-133">Dall'elenco tabulare di hello delle periferiche, selezionare e fare clic su dispositivo hello cui si intende tooset o si modifica la password gestione Snapshot StorSimple.</span><span class="sxs-lookup"><span data-stu-id="bfff9-133">From hello tabular listing of devices, select and click hello device whose StorSimple Snapshot Manager password you intend tooset or change.</span></span>

     ![](./media/storsimple-8000-change-passwords/changepwd1.png)

3. <span data-ttu-id="bfff9-134">In hello **impostazioni** pannello andare troppo**le impostazioni del dispositivo > sicurezza**.</span><span class="sxs-lookup"><span data-stu-id="bfff9-134">In hello **Settings** blade, go too**Device settings > Security**.</span></span>

     ![](./media/storsimple-8000-change-passwords/changepwd2.png)

4. <span data-ttu-id="bfff9-135">In hello **le impostazioni di sicurezza** pannello, fare clic su **Password** tooset o modifica password di StorSimple Snapshot Manager hello.</span><span class="sxs-lookup"><span data-stu-id="bfff9-135">In hello **Security settings** blade, click **Password** tooset or change hello StorSimple Snapshot Manager password.</span></span>

     ![](./media/storsimple-8000-change-passwords/changepwd3.png) 

5. <span data-ttu-id="bfff9-136">In hello **Password** pannello, immettere una password composta da 14 o 15 caratteri.</span><span class="sxs-lookup"><span data-stu-id="bfff9-136">In hello **Password** blade, enter a password that is 14 or 15 characters.</span></span> <span data-ttu-id="bfff9-137">Assicurarsi che la password hello contiene una combinazione di 3 o più dei caratteri maiuscoli, minuscoli, numerici e speciali.</span><span class="sxs-lookup"><span data-stu-id="bfff9-137">Make sure that hello password contains a combination of 3 or more of uppercase, lowercase, numeric, and special characters.</span></span>

6. <span data-ttu-id="bfff9-138">Conferma password hello.</span><span class="sxs-lookup"><span data-stu-id="bfff9-138">Confirm hello password.</span></span>

     ![](./media/storsimple-8000-change-passwords/changepwd5.png)

7. <span data-ttu-id="bfff9-139">Alla richiesta di conferma fare clic su **Salva** e quindi su **Sì**.</span><span class="sxs-lookup"><span data-stu-id="bfff9-139">Click **Save** and when prompted for confirmation, click **Yes**.</span></span>

     ![](./media/storsimple-8000-change-passwords/changepwd6.png)

<span data-ttu-id="bfff9-140">password gestione Snapshot StorSimple Hello dovrebbe ora essere aggiornata.</span><span class="sxs-lookup"><span data-stu-id="bfff9-140">hello StorSimple Snapshot Manager password should now be updated.</span></span>

## <a name="next-steps"></a><span data-ttu-id="bfff9-141">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="bfff9-141">Next steps</span></span>
* <span data-ttu-id="bfff9-142">Ulteriori informazioni sulla [sicurezza di StorSimple](storsimple-8000-security.md).</span><span class="sxs-lookup"><span data-stu-id="bfff9-142">Learn more about [StorSimple security](storsimple-8000-security.md).</span></span>
* <span data-ttu-id="bfff9-143">[Ulteriori informazioni su come modificare la configurazione del dispositivo](storsimple-8000-modify-device-config.md).</span><span class="sxs-lookup"><span data-stu-id="bfff9-143">Learn more about [modifying your device configuration](storsimple-8000-modify-device-config.md).</span></span>
* <span data-ttu-id="bfff9-144">Altre informazioni, vedere [utilizzando hello tooadminister servizio di gestione di dispositivi StorSimple dispositivo StorSimple](storsimple-8000-manager-service-administration.md).</span><span class="sxs-lookup"><span data-stu-id="bfff9-144">Learn more about [using hello StorSimple Device Manager service tooadminister your StorSimple device](storsimple-8000-manager-service-administration.md).</span></span>


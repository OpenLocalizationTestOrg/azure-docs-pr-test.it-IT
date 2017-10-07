---
title: password amministratore del dispositivo StorSimple Virtual Array aaaChange | Documenti Microsoft
description: "Viene descritto come toouse hello è il portale di Azure o Array virtuale StorSimple web UI toochange hello password amministratore del dispositivo."
services: storsimple
documentationcenter: NA
author: alkohli
manager: timlt
editor: 
ms.assetid: 11490814-d9fd-4dc7-9c3b-55dd2c23eaf1
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: TBD
ms.date: 02/27/2017
ms.author: alkohli
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 531b395df7aeade0a909360797c6b0f0abd9fd1e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="change-hello-storsimple-virtual-array-device-administrator-password-via-storsimple-device-manager"></a><span data-ttu-id="8d82d-103">Modifica password amministratore del dispositivo StorSimple Virtual Array hello tramite Gestione dispositivi StorSimple</span><span class="sxs-lookup"><span data-stu-id="8d82d-103">Change hello StorSimple Virtual Array device administrator password via StorSimple Device Manager</span></span>

## <a name="overview"></a><span data-ttu-id="8d82d-104">Panoramica</span><span class="sxs-lookup"><span data-stu-id="8d82d-104">Overview</span></span>

<span data-ttu-id="8d82d-105">Quando si utilizza tooaccess di interfaccia di Windows PowerShell hello hello Array virtuale StorSimple, è necessario tooenter una password amministratore del dispositivo.</span><span class="sxs-lookup"><span data-stu-id="8d82d-105">When you use hello Windows PowerShell interface tooaccess hello StorSimple Virtual Array, you are required tooenter a device administrator password.</span></span> <span data-ttu-id="8d82d-106">Quando il dispositivo StorSimple hello viene innanzitutto effettuato il provisioning e avviata, la password predefinita hello è *Password1*.</span><span class="sxs-lookup"><span data-stu-id="8d82d-106">When hello StorSimple device is first provisioned and started, hello default password is *Password1*.</span></span> <span data-ttu-id="8d82d-107">Per la protezione dei dati hello, scadenza password predefinito di hello hello prima volta che si accede e si è necessari toochange questa password.</span><span class="sxs-lookup"><span data-stu-id="8d82d-107">For hello security of your data, hello default password expires hello first time that you sign in and you are required toochange this password.</span></span>

<span data-ttu-id="8d82d-108">È anche possibile utilizzare entrambi hello web locale dell'interfaccia utente o hello toochange portale Azure hello password amministratore del dispositivo in qualsiasi momento dopo hello dispositivo viene distribuito nell'ambiente di produzione.</span><span class="sxs-lookup"><span data-stu-id="8d82d-108">You can also use either hello local web UI or hello Azure portal toochange hello device administrator password at any time after hello device is deployed in your production environment.</span></span> <span data-ttu-id="8d82d-109">Tutte queste procedure vengono descritte in questo articolo.</span><span class="sxs-lookup"><span data-stu-id="8d82d-109">Each of these procedures is described in this article.</span></span>

 ![pannello Dispositivi](./media/storsimple-virtual-array-change-device-admin-password/ova-devices-blade.png)

## <a name="use-hello-azure-portal-toochange-hello-password"></a><span data-ttu-id="8d82d-111">Usare password di hello hello toochange portale di Azure</span><span class="sxs-lookup"><span data-stu-id="8d82d-111">Use hello Azure portal toochange hello password</span></span>

<span data-ttu-id="8d82d-112">Eseguire i seguenti passaggi toochange hello password amministratore del dispositivo tramite il portale di Azure hello hello.</span><span class="sxs-lookup"><span data-stu-id="8d82d-112">Perform hello following steps toochange hello device administrator password through hello Azure portal.</span></span>

#### <a name="toochange-hello-device-administrator-password-via-hello-azure-portal"></a><span data-ttu-id="8d82d-113">password amministratore del dispositivo hello toochange tramite hello portale di Azure</span><span class="sxs-lookup"><span data-stu-id="8d82d-113">toochange hello device administrator password via hello Azure portal</span></span>

1. <span data-ttu-id="8d82d-114">Nella pagina di destinazione del servizio hello, selezionare il servizio, fare doppio clic sul servizio hello nome e quindi all'interno di hello **Management** fare clic su **dispositivi**.</span><span class="sxs-lookup"><span data-stu-id="8d82d-114">On hello service landing page, select your service, double-click hello service name, and then within hello **Management** section, click **Devices**.</span></span> <span data-ttu-id="8d82d-115">Verrà visualizzata hello **dispositivi** blade che elenca tutti i dispositivi StorSimple Virtual Array.</span><span class="sxs-lookup"><span data-stu-id="8d82d-115">This opens hello **Devices** blade that lists all your StorSimple Virtual Array devices.</span></span>

2. <span data-ttu-id="8d82d-116">In hello **dispositivi** pannello, fare doppio clic sul dispositivo di hello che richiede una modifica della password.</span><span class="sxs-lookup"><span data-stu-id="8d82d-116">In hello **Devices** blade, double-click hello device that requires a change of password.</span></span>

3. <span data-ttu-id="8d82d-117">In hello **impostazioni** pannello per il dispositivo, fare clic su **sicurezza**.</span><span class="sxs-lookup"><span data-stu-id="8d82d-117">In hello **Settings** blade for your device, click **Security**.</span></span>

4. <span data-ttu-id="8d82d-118">In hello **le impostazioni di sicurezza** pannello hello seguenti:</span><span class="sxs-lookup"><span data-stu-id="8d82d-118">In hello **Security Settings** blade, do hello following:</span></span>
   
   1. <span data-ttu-id="8d82d-119">Scorrere verso il basso toohello **Password amministratore del dispositivo** sezione.</span><span class="sxs-lookup"><span data-stu-id="8d82d-119">Scroll down toohello **Device Administrator Password** section.</span></span> <span data-ttu-id="8d82d-120">Specificare una password amministratore contenente dagli 8 too15 caratteri.</span><span class="sxs-lookup"><span data-stu-id="8d82d-120">Provide an administrator password that contains from 8 too15 characters.</span></span>
   2. <span data-ttu-id="8d82d-121">Conferma password hello.</span><span class="sxs-lookup"><span data-stu-id="8d82d-121">Confirm hello password.</span></span>
   3. <span data-ttu-id="8d82d-122">Fare clic su **salvare** nella parte superiore di hello del pannello hello.</span><span class="sxs-lookup"><span data-stu-id="8d82d-122">Click **Save** at hello top of hello blade.</span></span>

<span data-ttu-id="8d82d-123">password amministratore del dispositivo Hello è ora aggiornata.</span><span class="sxs-lookup"><span data-stu-id="8d82d-123">hello device administrator password is now updated.</span></span> <span data-ttu-id="8d82d-124">È possibile utilizzare il dispositivo di hello tooaccess password modificata in locale.</span><span class="sxs-lookup"><span data-stu-id="8d82d-124">You can use this modified password tooaccess hello device locally.</span></span>

![Pannello impostazioni di sicurezza](./media/storsimple-virtual-array-change-device-admin-password/ova-change-device-pwd.png)

## <a name="use-hello-local-web-ui-toochange-hello-password"></a><span data-ttu-id="8d82d-126">Utilizzare password hello toochange di hello web locale dell'interfaccia utente</span><span class="sxs-lookup"><span data-stu-id="8d82d-126">Use hello local web UI toochange hello password</span></span>

<span data-ttu-id="8d82d-127">Eseguire i seguenti passaggi toochange hello password amministratore del dispositivo tramite l'interfaccia utente web locale hello hello.</span><span class="sxs-lookup"><span data-stu-id="8d82d-127">Perform hello following steps toochange hello device administrator password through hello local web UI.</span></span>

#### <a name="toochange-hello-device-administrator-password-via-hello-local-web-ui"></a><span data-ttu-id="8d82d-128">password amministratore del dispositivo hello toochange tramite l'interfaccia utente web locale hello</span><span class="sxs-lookup"><span data-stu-id="8d82d-128">toochange hello device administrator password via hello local web UI</span></span>

1. <span data-ttu-id="8d82d-129">In hello interfaccia utente web locale, fare clic su **manutenzione** > **modifica della Password** per il dispositivo.</span><span class="sxs-lookup"><span data-stu-id="8d82d-129">In hello local web UI, click **Maintenance** > **Password change** for your device.</span></span>
   
    ![cambiare password1](./media/storsimple-virtual-array-change-device-admin-password/image40.png)
2. <span data-ttu-id="8d82d-131">Immettere hello **password corrente**.</span><span class="sxs-lookup"><span data-stu-id="8d82d-131">Enter hello **Current password**.</span></span>
3. <span data-ttu-id="8d82d-132">Fornire una **Nuova password**.</span><span class="sxs-lookup"><span data-stu-id="8d82d-132">Provide a **New Password**.</span></span> <span data-ttu-id="8d82d-133">password di Hello deve essere composta da almeno 8 caratteri.</span><span class="sxs-lookup"><span data-stu-id="8d82d-133">hello password must be at least 8 characters long.</span></span> <span data-ttu-id="8d82d-134">Deve contenere 3 delle 4 seguenti hello: caratteri maiuscoli, minuscoli, numerici e speciali.</span><span class="sxs-lookup"><span data-stu-id="8d82d-134">It must contain 3 of 4 of hello following: uppercase, lowercase, numeric, and special characters.</span></span>
   
    <span data-ttu-id="8d82d-135">Si noti che la password non può essere hello stesso hello ultime 24 password specificate.</span><span class="sxs-lookup"><span data-stu-id="8d82d-135">Note that your password cannot be hello same as hello last 24 passwords.</span></span>
4. <span data-ttu-id="8d82d-136">Immettere nuovamente tooconfirm password hello è.</span><span class="sxs-lookup"><span data-stu-id="8d82d-136">Reenter hello password tooconfirm it.</span></span>
   
    ![cambiare password2](./media/storsimple-virtual-array-change-device-admin-password/image41.png)
5. <span data-ttu-id="8d82d-138">Nella parte inferiore di hello della pagina hello, fare clic su **applica**.</span><span class="sxs-lookup"><span data-stu-id="8d82d-138">At hello bottom of hello page, click **Apply**.</span></span> <span data-ttu-id="8d82d-139">nuova password Hello viene ora applicata.</span><span class="sxs-lookup"><span data-stu-id="8d82d-139">hello new password is now applied.</span></span> <span data-ttu-id="8d82d-140">Se la modifica della password hello non ha esito positivo, viene visualizzato il seguente errore hello:</span><span class="sxs-lookup"><span data-stu-id="8d82d-140">If hello password change is not successful, you see hello following error:</span></span>
   
    ![errore password](./media/storsimple-virtual-array-change-device-admin-password/image42.png)
   
    <span data-ttu-id="8d82d-142">Dopo aver completato l'aggiornamento password hello, ricevono la notifica.</span><span class="sxs-lookup"><span data-stu-id="8d82d-142">After hello password is successfully updated, you are notified.</span></span> <span data-ttu-id="8d82d-143">È quindi possibile utilizzare password modificata tooaccess hello dispositivo localmente.</span><span class="sxs-lookup"><span data-stu-id="8d82d-143">You can then use this modified password tooaccess hello device locally.</span></span>


## <a name="next-steps"></a><span data-ttu-id="8d82d-144">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="8d82d-144">Next steps</span></span>
<span data-ttu-id="8d82d-145">Informazioni su come troppo[amministrare l'Array virtuale StorSimple](storsimple-ova-web-ui-admin.md).</span><span class="sxs-lookup"><span data-stu-id="8d82d-145">Learn how too[administer your StorSimple Virtual Array](storsimple-ova-web-ui-admin.md).</span></span>


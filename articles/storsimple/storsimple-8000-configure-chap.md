---
title: aaaConfigure CHAP per dispositivo StorSimple serie 8000 | Documenti Microsoft
description: Viene descritto come tooconfigure hello Challenge Handshake Authentication Protocol (CHAP) in un dispositivo StorSimple.
services: storsimple
documentationcenter: 
author: alkohli
manager: timlt
editor: 
ms.assetid: 
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: TBD
ms.date: 07/03/2017
ms.author: alkohli
ms.openlocfilehash: 3351184b0317da7e3deae398bc0d63c3e5bd930f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="configure-chap-for-your-storsimple-device"></a><span data-ttu-id="4b4aa-103">Configurare CHAP per il dispositivo StorSimple</span><span class="sxs-lookup"><span data-stu-id="4b4aa-103">Configure CHAP for your StorSimple device</span></span>

<span data-ttu-id="4b4aa-104">In questa esercitazione viene illustrato come tooconfigure CHAP per il dispositivo StorSimple.</span><span class="sxs-lookup"><span data-stu-id="4b4aa-104">This tutorial explains how tooconfigure CHAP for your StorSimple device.</span></span> <span data-ttu-id="4b4aa-105">procedura di Hello descritta in questo articolo si applica tooStorSimple dispositivi della serie 8000.</span><span class="sxs-lookup"><span data-stu-id="4b4aa-105">hello procedure detailed in this article applies tooStorSimple 8000 series devices.</span></span>

<span data-ttu-id="4b4aa-106">CHAP è l'acronimo di Challenge Handshake Authentication Protocol.</span><span class="sxs-lookup"><span data-stu-id="4b4aa-106">CHAP stands for Challenge Handshake Authentication Protocol.</span></span> <span data-ttu-id="4b4aa-107">È uno schema di autenticazione utilizzato dall'identità di hello server toovalidate di client remoti.</span><span class="sxs-lookup"><span data-stu-id="4b4aa-107">It is an authentication scheme used by servers toovalidate hello identity of remote clients.</span></span> <span data-ttu-id="4b4aa-108">verifica di Hello si basa su una password condivisa o un segreto.</span><span class="sxs-lookup"><span data-stu-id="4b4aa-108">hello verification is based on a shared password or secret.</span></span> <span data-ttu-id="4b4aa-109">CHAP può essere unidirezionale o bidirezionale (reciproco).</span><span class="sxs-lookup"><span data-stu-id="4b4aa-109">CHAP can be one way (unidirectional) or mutual (bidirectional).</span></span> <span data-ttu-id="4b4aa-110">CHAP è quando la destinazione hello autentica un iniziatore.</span><span class="sxs-lookup"><span data-stu-id="4b4aa-110">One way CHAP is when hello target authenticates an initiator.</span></span> <span data-ttu-id="4b4aa-111">In CHAP reciproco o inverso, destinazione hello l'autenticazione dell'iniziatore hello e iniziatore hello destinazione hello.</span><span class="sxs-lookup"><span data-stu-id="4b4aa-111">In mutual or reverse CHAP, hello target authenticates hello initiator and then hello initiator authenticates hello target.</span></span> <span data-ttu-id="4b4aa-112">È possibile implementare l'autenticazione dell'iniziatore senza autenticazione della destinazione.</span><span class="sxs-lookup"><span data-stu-id="4b4aa-112">Initiator authentication can be implemented without target authentication.</span></span> <span data-ttu-id="4b4aa-113">L’autenticazione della destinazione, tuttavia, può essere implementata solo se viene implementata anche l'autenticazione dell'iniziatore.</span><span class="sxs-lookup"><span data-stu-id="4b4aa-113">However, target authentication can be implemented only if initiator authentication is also implemented.</span></span>

<span data-ttu-id="4b4aa-114">Come procedura consigliata, è consigliabile utilizzare la sicurezza iSCSI tooenhance CHAP.</span><span class="sxs-lookup"><span data-stu-id="4b4aa-114">As a best practice, we recommend that you use CHAP tooenhance iSCSI security.</span></span>

> [!NOTE]
> <span data-ttu-id="4b4aa-115">Tenere presente che IPSEC non è attualmente supportato in dispositivi StorSimple.</span><span class="sxs-lookup"><span data-stu-id="4b4aa-115">Keep in mind that IPSEC is not currently supported on StorSimple devices.</span></span>

<span data-ttu-id="4b4aa-116">Hello CHAP nel dispositivo StorSimple hello possono essere configurate in hello seguenti modi:</span><span class="sxs-lookup"><span data-stu-id="4b4aa-116">hello CHAP settings on hello StorSimple device can be configured in hello following ways:</span></span>

* <span data-ttu-id="4b4aa-117">Autenticazione unidirezionale </span><span class="sxs-lookup"><span data-stu-id="4b4aa-117">Unidirectional or one-way authentication</span></span>
* <span data-ttu-id="4b4aa-118">Autenticazione bidirezionale, reciproca o inversa </span><span class="sxs-lookup"><span data-stu-id="4b4aa-118">Bidirectional or mutual or reverse authentication</span></span>

<span data-ttu-id="4b4aa-119">In ognuno di questi casi, il portale di hello per dispositivo hello e il software dell'iniziatore iSCSI di hello server deve toobe configurato.</span><span class="sxs-lookup"><span data-stu-id="4b4aa-119">In each of these cases, hello portal for hello device and hello server iSCSI initiator software needs toobe configured.</span></span> <span data-ttu-id="4b4aa-120">Hello i passaggi dettagliati per questa configurazione sono descritti nella seguente esercitazione hello.</span><span class="sxs-lookup"><span data-stu-id="4b4aa-120">hello detailed steps for this configuration are described in hello following tutorial.</span></span>

## <a name="unidirectional-or-one-way-authentication"></a><span data-ttu-id="4b4aa-121">Autenticazione unidirezionale </span><span class="sxs-lookup"><span data-stu-id="4b4aa-121">Unidirectional or one-way authentication</span></span>

<span data-ttu-id="4b4aa-122">Nell'autenticazione unidirezionale la destinazione hello autentica l'iniziatore di hello.</span><span class="sxs-lookup"><span data-stu-id="4b4aa-122">In unidirectional authentication, hello target authenticates hello initiator.</span></span> <span data-ttu-id="4b4aa-123">Questa autenticazione, è necessario configurare impostazioni dell'iniziatore CHAP di hello nel dispositivo StorSimple hello e hello iSCSI software Initiator in host hello.</span><span class="sxs-lookup"><span data-stu-id="4b4aa-123">This authentication requires that you configure hello CHAP initiator settings on hello StorSimple device and hello iSCSI Initiator software on hello host.</span></span> <span data-ttu-id="4b4aa-124">procedure dettagliate per il dispositivo StorSimple Hello e host di Windows vengono descritte di seguito.</span><span class="sxs-lookup"><span data-stu-id="4b4aa-124">hello detailed procedures for your StorSimple device and Windows host are described next.</span></span>

#### <a name="tooconfigure-your-device-for-one-way-authentication"></a><span data-ttu-id="4b4aa-125">tooconfigure del dispositivo per l'autenticazione unidirezionale</span><span class="sxs-lookup"><span data-stu-id="4b4aa-125">tooconfigure your device for one-way authentication</span></span>

1. <span data-ttu-id="4b4aa-126">Nel portale di Azure hello, visitare il servizio di gestione di dispositivi StorSimple tooyour.</span><span class="sxs-lookup"><span data-stu-id="4b4aa-126">In hello Azure portal, go tooyour StorSimple Device Manager service.</span></span> <span data-ttu-id="4b4aa-127">Fare clic su **dispositivi** selezionare e fare clic su un dispositivo a cui si desidera tooconfigure CHAP per.</span><span class="sxs-lookup"><span data-stu-id="4b4aa-127">Click **Devices** and select and click a device you wish tooconfigure CHAP for.</span></span> <span data-ttu-id="4b4aa-128">Andare troppo**le impostazioni del dispositivo > sicurezza**.</span><span class="sxs-lookup"><span data-stu-id="4b4aa-128">Go too**Device settings > Security**.</span></span> <span data-ttu-id="4b4aa-129">In hello **le impostazioni di sicurezza** pannello, fare clic su **CHAP**.</span><span class="sxs-lookup"><span data-stu-id="4b4aa-129">In hello **Security settings** blade, click **CHAP**.</span></span>
   
    ![Iniziatore CHAP](./media/storsimple-8000-configure-chap/configure-chap5.png)
2. <span data-ttu-id="4b4aa-131">In hello **CHAP** pannello e hello **iniziatore CHAP** sezione:</span><span class="sxs-lookup"><span data-stu-id="4b4aa-131">In hello **CHAP** blade, and in hello **CHAP Initiator** section:</span></span>
   
   1. <span data-ttu-id="4b4aa-132">Specificare un nome utente per l'iniziatore CHAP.</span><span class="sxs-lookup"><span data-stu-id="4b4aa-132">Provide a user name for your CHAP initiator.</span></span>
   2. <span data-ttu-id="4b4aa-133">Specificare una password per l'iniziatore CHAP.</span><span class="sxs-lookup"><span data-stu-id="4b4aa-133">Supply a password for your CHAP initiator.</span></span>
      
    > [!IMPORTANT]
    > <span data-ttu-id="4b4aa-134">nome utente Hello deve contenere meno di 233 caratteri.</span><span class="sxs-lookup"><span data-stu-id="4b4aa-134">hello CHAP user name must contain fewer than 233 characters.</span></span> <span data-ttu-id="4b4aa-135">password CHAP Hello deve essere compreso tra 12 e 16 caratteri.</span><span class="sxs-lookup"><span data-stu-id="4b4aa-135">hello CHAP password must be between 12 and 16 characters.</span></span> <span data-ttu-id="4b4aa-136">Un nome utente o una password più lungo comporta un errore di autenticazione sull'host di Windows hello.</span><span class="sxs-lookup"><span data-stu-id="4b4aa-136">A longer user name or password results in an authentication failure on hello Windows host.</span></span>
   
   3. <span data-ttu-id="4b4aa-137">Conferma password hello.</span><span class="sxs-lookup"><span data-stu-id="4b4aa-137">Confirm hello password.</span></span>

       ![Iniziatore CHAP](./media/storsimple-8000-configure-chap/configure-chap6.png)
3. <span data-ttu-id="4b4aa-139">Fare clic su **Salva**.</span><span class="sxs-lookup"><span data-stu-id="4b4aa-139">Click **Save**.</span></span> <span data-ttu-id="4b4aa-140">Viene visualizzato un messaggio di conferma.</span><span class="sxs-lookup"><span data-stu-id="4b4aa-140">A confirmation message is displayed.</span></span> <span data-ttu-id="4b4aa-141">Fare clic su **OK** modifiche hello toosave.</span><span class="sxs-lookup"><span data-stu-id="4b4aa-141">Click **OK** toosave hello changes.</span></span>

#### <a name="tooconfigure-one-way-authentication-on-hello-windows-host-server"></a><span data-ttu-id="4b4aa-142">server host tooconfigure autenticazione unidirezionale in Windows hello</span><span class="sxs-lookup"><span data-stu-id="4b4aa-142">tooconfigure one-way authentication on hello Windows host server</span></span>
1. <span data-ttu-id="4b4aa-143">Nel server host di Windows hello, avviare l'iniziatore iSCSI hello.</span><span class="sxs-lookup"><span data-stu-id="4b4aa-143">On hello Windows host server, start hello iSCSI Initiator.</span></span>
2. <span data-ttu-id="4b4aa-144">In hello **iniziatore iSCSI-proprietà** finestra, eseguire hello alla procedura seguente:</span><span class="sxs-lookup"><span data-stu-id="4b4aa-144">In hello **iSCSI Initiator Properties** window, perform hello following steps:</span></span>
   
   1. <span data-ttu-id="4b4aa-145">Fare clic su hello **individuazione** scheda.</span><span class="sxs-lookup"><span data-stu-id="4b4aa-145">Click hello **Discovery** tab.</span></span>
      
       ![Proprietà iniziatore iSCSI](./media/storsimple-configure-chap/IC740944.png)
   2. <span data-ttu-id="4b4aa-147">Fare clic su **Individua portale**.</span><span class="sxs-lookup"><span data-stu-id="4b4aa-147">Click **Discover Portal**.</span></span>
3. <span data-ttu-id="4b4aa-148">In hello **individua portale destinazione** la finestra di dialogo:</span><span class="sxs-lookup"><span data-stu-id="4b4aa-148">In hello **Discover Target Portal** dialog box:</span></span>
   
   1. <span data-ttu-id="4b4aa-149">Specificare l'indirizzo IP di hello del dispositivo.</span><span class="sxs-lookup"><span data-stu-id="4b4aa-149">Specify hello IP address of your device.</span></span>
   2. <span data-ttu-id="4b4aa-150">Fare clic su **Advanced**.</span><span class="sxs-lookup"><span data-stu-id="4b4aa-150">Click **Advanced**.</span></span>
      
       ![Individua portale destinazione](./media/storsimple-configure-chap/IC740945.png)
4. <span data-ttu-id="4b4aa-152">In hello **impostazioni avanzate** la finestra di dialogo:</span><span class="sxs-lookup"><span data-stu-id="4b4aa-152">In hello **Advanced Settings** dialog box:</span></span>
   
   1. <span data-ttu-id="4b4aa-153">Seleziona hello **Abilita accesso CHAP** casella di controllo.</span><span class="sxs-lookup"><span data-stu-id="4b4aa-153">Select hello **Enable CHAP log on** check box.</span></span>
   2. <span data-ttu-id="4b4aa-154">In hello **nome** campo, specificare hello il nome utente specificato per hello iniziatore CHAP nel portale classico hello.</span><span class="sxs-lookup"><span data-stu-id="4b4aa-154">In hello **Name** field, supply hello user name that you specified for hello CHAP Initiator in hello classic portal.</span></span>
   3. <span data-ttu-id="4b4aa-155">In hello **segreto destinazione** campo, una password di hello alimentatore specificato per hello iniziatore CHAP nel portale classico hello.</span><span class="sxs-lookup"><span data-stu-id="4b4aa-155">In hello **Target secret** field, supply hello password that you specified for hello CHAP Initiator in hello classic portal.</span></span>
   4. <span data-ttu-id="4b4aa-156">Fare clic su **OK**.</span><span class="sxs-lookup"><span data-stu-id="4b4aa-156">Click **OK**.</span></span>
      
       ![Impostazioni avanzate - Generale](./media/storsimple-configure-chap/IC740946.png)
5. <span data-ttu-id="4b4aa-158">In hello **destinazioni** scheda di hello **iniziatore iSCSI-proprietà** , lo stato del dispositivo hello finestra come **connesso**.</span><span class="sxs-lookup"><span data-stu-id="4b4aa-158">On hello **Targets** tab of hello **iSCSI Initiator Properties** window, hello device status should appear as **Connected**.</span></span> <span data-ttu-id="4b4aa-159">Se si usa un dispositivo StorSimple 1200, ogni volume viene montato come destinazione iSCSI.</span><span class="sxs-lookup"><span data-stu-id="4b4aa-159">If you are using a StorSimple 1200 device, then each volume is mounted as an iSCSI target.</span></span> <span data-ttu-id="4b4aa-160">Di conseguenza, i passaggi 3 e 4, saranno necessario toobe ripetuto per ogni volume.</span><span class="sxs-lookup"><span data-stu-id="4b4aa-160">Hence, steps 3-4 will need toobe repeated for each volume.</span></span>
   
    ![Volumi montati come destinazioni separate](./media/storsimple-configure-chap/chap4.png)
   
   > [!IMPORTANT]
   > <span data-ttu-id="4b4aa-162">Se si modifica il nome di iSCSI hello, hello nuovo nome viene utilizzato per le nuove sessioni iSCSI.</span><span class="sxs-lookup"><span data-stu-id="4b4aa-162">If you change hello iSCSI name, hello new name is used for new iSCSI sessions.</span></span> <span data-ttu-id="4b4aa-163">Le nuove impostazioni non vengono utilizzate per le sessioni esistenti fino a quando non si esegue la disconnessione e il nuovo accesso.</span><span class="sxs-lookup"><span data-stu-id="4b4aa-163">New settings are not used for existing sessions until you log off and log on again.</span></span>

<span data-ttu-id="4b4aa-164">Per ulteriori informazioni sulla configurazione dell'autenticazione CHAP nel server host di Windows hello, andare troppo[considerazioni aggiuntive](#additional-considerations).</span><span class="sxs-lookup"><span data-stu-id="4b4aa-164">For more information about configuring CHAP on hello Windows host server, go too[Additional considerations](#additional-considerations).</span></span>

## <a name="bidirectional-or-mutual-authentication"></a><span data-ttu-id="4b4aa-165">Autenticazione bidirezionale o reciproca </span><span class="sxs-lookup"><span data-stu-id="4b4aa-165">Bidirectional or mutual authentication</span></span>

<span data-ttu-id="4b4aa-166">Nell'autenticazione bidirezionale destinazione hello l'autenticazione dell'iniziatore hello e iniziatore hello destinazione hello.</span><span class="sxs-lookup"><span data-stu-id="4b4aa-166">In bidirectional authentication, hello target authenticates hello initiator and then hello initiator authenticates hello target.</span></span> <span data-ttu-id="4b4aa-167">Questa procedura richiede le impostazioni dell'iniziatore CHAP hello tooconfigure utente hello, invertire impostazioni CHAP nel dispositivo hello e iSCSI software Initiator in host hello.</span><span class="sxs-lookup"><span data-stu-id="4b4aa-167">This procedure requires hello user tooconfigure hello CHAP initiator settings, reverse CHAP settings on hello device, and iSCSI Initiator software on hello host.</span></span> <span data-ttu-id="4b4aa-168">Hello procedure seguenti descrivono l'autenticazione reciproca hello passaggi tooconfigure nel dispositivo di hello e nell'host di Windows hello.</span><span class="sxs-lookup"><span data-stu-id="4b4aa-168">hello following procedures describe hello steps tooconfigure mutual authentication on hello device and on hello Windows host.</span></span>

#### <a name="tooconfigure-your-device-for-mutual-authentication"></a><span data-ttu-id="4b4aa-169">tooconfigure il dispositivo per l'autenticazione reciproca</span><span class="sxs-lookup"><span data-stu-id="4b4aa-169">tooconfigure your device for mutual authentication</span></span>

1. <span data-ttu-id="4b4aa-170">Nel portale di Azure hello, visitare il servizio di gestione di dispositivi StorSimple tooyour.</span><span class="sxs-lookup"><span data-stu-id="4b4aa-170">In hello Azure portal, go tooyour StorSimple Device Manager service.</span></span> <span data-ttu-id="4b4aa-171">Fare clic su **dispositivi** selezionare e fare clic su un dispositivo a cui si desidera tooconfigure CHAP per.</span><span class="sxs-lookup"><span data-stu-id="4b4aa-171">Click **Devices** and select and click a device you wish tooconfigure CHAP for.</span></span> <span data-ttu-id="4b4aa-172">Andare troppo**le impostazioni del dispositivo > sicurezza**.</span><span class="sxs-lookup"><span data-stu-id="4b4aa-172">Go too**Device settings > Security**.</span></span> <span data-ttu-id="4b4aa-173">In hello **le impostazioni di sicurezza** pannello, fare clic su **CHAP**.</span><span class="sxs-lookup"><span data-stu-id="4b4aa-173">In hello **Security settings** blade, click **CHAP**.</span></span>
   
    ![Destinazione CHAP](./media/storsimple-8000-configure-chap/configure-chap5.png)
2. <span data-ttu-id="4b4aa-175">Scorrere verso il basso, in questa pagina in hello **destinazione CHAP** sezione:</span><span class="sxs-lookup"><span data-stu-id="4b4aa-175">Scroll down on this page, and in hello **CHAP Target** section:</span></span>
   
   1. <span data-ttu-id="4b4aa-176">Fornire un **nome utente per l’autenticazione CHAP inversa** per il dispositivo.</span><span class="sxs-lookup"><span data-stu-id="4b4aa-176">Provide a **Reverse CHAP user name** for your device.</span></span>
   2. <span data-ttu-id="4b4aa-177">Fornire una **password per l’autenticazione CHAP inversa** per il dispositivo.</span><span class="sxs-lookup"><span data-stu-id="4b4aa-177">Supply a **Reverse CHAP password** for your device.</span></span>
   3. <span data-ttu-id="4b4aa-178">Conferma password hello.</span><span class="sxs-lookup"><span data-stu-id="4b4aa-178">Confirm hello password.</span></span>
3. <span data-ttu-id="4b4aa-179">In hello **iniziatore CHAP** sezione:</span><span class="sxs-lookup"><span data-stu-id="4b4aa-179">In hello **CHAP Initiator** section:</span></span>
   
   1. <span data-ttu-id="4b4aa-180">Specificare un **nome utente** per il dispositivo.</span><span class="sxs-lookup"><span data-stu-id="4b4aa-180">Provide a **user name** for your device.</span></span>
   2. <span data-ttu-id="4b4aa-181">Specificare una **password** per il dispositivo.</span><span class="sxs-lookup"><span data-stu-id="4b4aa-181">Provide a **password** for your device.</span></span>
   3. <span data-ttu-id="4b4aa-182">Conferma password hello.</span><span class="sxs-lookup"><span data-stu-id="4b4aa-182">Confirm hello password.</span></span>

       ![Iniziatore CHAP](./media/storsimple-8000-configure-chap/configure-chap11.png)
4. <span data-ttu-id="4b4aa-184">Fare clic su **Salva**.</span><span class="sxs-lookup"><span data-stu-id="4b4aa-184">Click **Save**.</span></span> <span data-ttu-id="4b4aa-185">Viene visualizzato un messaggio di conferma.</span><span class="sxs-lookup"><span data-stu-id="4b4aa-185">A confirmation message is displayed.</span></span> <span data-ttu-id="4b4aa-186">Fare clic su **OK** modifiche hello toosave.</span><span class="sxs-lookup"><span data-stu-id="4b4aa-186">Click **OK** toosave hello changes.</span></span>

#### <a name="tooconfigure-bidirectional-authentication-on-hello-windows-host-server"></a><span data-ttu-id="4b4aa-187">autenticazione bidirezionale tooconfigure in Windows hello server host</span><span class="sxs-lookup"><span data-stu-id="4b4aa-187">tooconfigure bidirectional authentication on hello Windows host server</span></span>

1. <span data-ttu-id="4b4aa-188">Nel server host di Windows hello, avviare l'iniziatore iSCSI hello.</span><span class="sxs-lookup"><span data-stu-id="4b4aa-188">On hello Windows host server, start hello iSCSI Initiator.</span></span>
2. <span data-ttu-id="4b4aa-189">In hello **iniziatore iSCSI-proprietà** finestra, fare clic su hello **configurazione** scheda.</span><span class="sxs-lookup"><span data-stu-id="4b4aa-189">In hello **iSCSI Initiator Properties** window, click hello **Configuration** tab.</span></span>
3. <span data-ttu-id="4b4aa-190">Fare clic su **CHAP**.</span><span class="sxs-lookup"><span data-stu-id="4b4aa-190">Click **CHAP**.</span></span>
4. <span data-ttu-id="4b4aa-191">In hello **segreto autenticazione CHAP reciproca iniziatore iSCSI** la finestra di dialogo:</span><span class="sxs-lookup"><span data-stu-id="4b4aa-191">In hello **iSCSI Initiator Mutual CHAP Secret** dialog box:</span></span>
   
   1. <span data-ttu-id="4b4aa-192">Hello tipo **Password di autenticazione CHAP inversa** configurate nel portale di Azure hello.</span><span class="sxs-lookup"><span data-stu-id="4b4aa-192">Type hello **Reverse CHAP Password** that you configured in hello Azure portal.</span></span>
   2. <span data-ttu-id="4b4aa-193">Fare clic su **OK**.</span><span class="sxs-lookup"><span data-stu-id="4b4aa-193">Click **OK**.</span></span>
      
       ![Segreto autenticazione CHAP reciproca iniziatore iSCSI](./media/storsimple-configure-chap/IC740949.png)
5. <span data-ttu-id="4b4aa-195">Fare clic su hello **destinazioni** scheda.</span><span class="sxs-lookup"><span data-stu-id="4b4aa-195">Click hello **Targets** tab.</span></span>
6. <span data-ttu-id="4b4aa-196">Fare clic su hello **Connetti** pulsante.</span><span class="sxs-lookup"><span data-stu-id="4b4aa-196">Click hello **Connect** button.</span></span> 
7. <span data-ttu-id="4b4aa-197">In hello **connettersi tooTarget** la finestra di dialogo, fare clic su **avanzate**.</span><span class="sxs-lookup"><span data-stu-id="4b4aa-197">In hello **Connect tooTarget** dialog box, click **Advanced**.</span></span>
8. <span data-ttu-id="4b4aa-198">In hello **proprietà avanzate** la finestra di dialogo:</span><span class="sxs-lookup"><span data-stu-id="4b4aa-198">In hello **Advanced Properties** dialog box:</span></span>
   
   1. <span data-ttu-id="4b4aa-199">Seleziona hello **Abilita accesso CHAP** casella di controllo.</span><span class="sxs-lookup"><span data-stu-id="4b4aa-199">Select hello **Enable CHAP log on** check box.</span></span>
   2. <span data-ttu-id="4b4aa-200">In hello **nome** campo, specificare hello il nome utente specificato per hello iniziatore CHAP nel portale classico hello.</span><span class="sxs-lookup"><span data-stu-id="4b4aa-200">In hello **Name** field, supply hello user name that you specified for hello CHAP Initiator in hello classic portal.</span></span>
   3. <span data-ttu-id="4b4aa-201">In hello **segreto destinazione** campo, una password di hello alimentatore specificato per hello iniziatore CHAP nel portale classico hello.</span><span class="sxs-lookup"><span data-stu-id="4b4aa-201">In hello **Target secret** field, supply hello password that you specified for hello CHAP Initiator in hello classic portal.</span></span>
   4. <span data-ttu-id="4b4aa-202">Seleziona hello **Esegui autenticazione reciproca** casella di controllo.</span><span class="sxs-lookup"><span data-stu-id="4b4aa-202">Select hello **Perform mutual authentication** check box.</span></span>
      
       ![Impostazioni avanzate - Autenticazione reciproca](./media/storsimple-configure-chap/IC740950.png)
   5. <span data-ttu-id="4b4aa-204">Fare clic su **OK** configurazione di CHAP hello toocomplete</span><span class="sxs-lookup"><span data-stu-id="4b4aa-204">Click **OK** toocomplete hello CHAP configuration</span></span>

<span data-ttu-id="4b4aa-205">Per ulteriori informazioni sulla configurazione dell'autenticazione CHAP nel server host di Windows hello, andare troppo[considerazioni aggiuntive](#additional-considerations).</span><span class="sxs-lookup"><span data-stu-id="4b4aa-205">For more information about configuring CHAP on hello Windows host server, go too[Additional considerations](#additional-considerations).</span></span>

## <a name="additional-considerations"></a><span data-ttu-id="4b4aa-206">Considerazioni aggiuntive</span><span class="sxs-lookup"><span data-stu-id="4b4aa-206">Additional considerations</span></span>

<span data-ttu-id="4b4aa-207">Hello **connessione rapida** funzionalità non supporta le connessioni con CHAP abilitato.</span><span class="sxs-lookup"><span data-stu-id="4b4aa-207">hello **Quick Connect** feature does not support connections that have CHAP enabled.</span></span> <span data-ttu-id="4b4aa-208">Quando è abilitata l'autenticazione CHAP, assicurarsi di utilizzare hello **Connetti** pulsante è disponibile in hello **destinazioni** destinazione tooa tooconnect di scheda.</span><span class="sxs-lookup"><span data-stu-id="4b4aa-208">When CHAP is enabled, make sure that you use hello **Connect** button that is available on hello **Targets** tab tooconnect tooa target.</span></span>

![Connettersi tootarget](./media/storsimple-configure-chap/IC740947.png)

<span data-ttu-id="4b4aa-210">In hello **connettersi tooTarget** la finestra di dialogo che è disponibile, seleziona hello **aggiungere questo elenco toohello connessione destinazioni preferite** casella di controllo.</span><span class="sxs-lookup"><span data-stu-id="4b4aa-210">In hello **Connect tooTarget** dialog box that is presented, select hello **Add this connection toohello list of Favorite Targets** check box.</span></span> <span data-ttu-id="4b4aa-211">Questa selezione assicura che ogni riavvio del computer hello, viene effettuato un tentativo toorestore hello connessione toohello iSCSI alle destinazioni preferite.</span><span class="sxs-lookup"><span data-stu-id="4b4aa-211">This selection ensures that every time hello computer restarts, an attempt is made toorestore hello connection toohello iSCSI favorite targets.</span></span>

## <a name="errors-during-configuration"></a><span data-ttu-id="4b4aa-212">Errori durante la configurazione</span><span class="sxs-lookup"><span data-stu-id="4b4aa-212">Errors during configuration</span></span>

<span data-ttu-id="4b4aa-213">Se la configurazione CHAP non è corretta, quindi si è probabilmente toosee un **errore di autenticazione** messaggio di errore.</span><span class="sxs-lookup"><span data-stu-id="4b4aa-213">If your CHAP configuration is incorrect, then you are likely toosee an **Authentication failure** error message.</span></span>

## <a name="verification-of-chap-configuration"></a><span data-ttu-id="4b4aa-214">Verifica della configurazione di CHAP</span><span class="sxs-lookup"><span data-stu-id="4b4aa-214">Verification of CHAP configuration</span></span>

<span data-ttu-id="4b4aa-215">È possibile verificare che sia in uso dell'autenticazione CHAP completando hello alla procedura seguente.</span><span class="sxs-lookup"><span data-stu-id="4b4aa-215">You can verify that CHAP is being used by completing hello following steps.</span></span>

#### <a name="tooverify-your-chap-configuration"></a><span data-ttu-id="4b4aa-216">tooverify la configurazione CHAP</span><span class="sxs-lookup"><span data-stu-id="4b4aa-216">tooverify your CHAP configuration</span></span>
1. <span data-ttu-id="4b4aa-217">Fare clic su **Destinazioni preferite**.</span><span class="sxs-lookup"><span data-stu-id="4b4aa-217">Click **Favorite Targets**.</span></span>
2. <span data-ttu-id="4b4aa-218">Selezionare hello di destinazione per cui è abilitata l'autenticazione.</span><span class="sxs-lookup"><span data-stu-id="4b4aa-218">Select hello target for which you enabled authentication.</span></span>
3. <span data-ttu-id="4b4aa-219">Fare clic su **Dettagli**.</span><span class="sxs-lookup"><span data-stu-id="4b4aa-219">Click **Details**.</span></span>
   
    ![Proprietà iniziatore iSCSI - Destinazioni preferite](./media/storsimple-configure-chap/IC740951.png)
4. <span data-ttu-id="4b4aa-221">In hello **dettagli destinazione preferita** nella finestra di dialogo immissione hello nota in hello **autenticazione** campo.</span><span class="sxs-lookup"><span data-stu-id="4b4aa-221">In hello **Favorite Target Details** dialog box, note hello entry in hello **Authentication** field.</span></span> <span data-ttu-id="4b4aa-222">Se la configurazione hello ha esito positivo, dovrebbe essere visualizzato **CHAP**.</span><span class="sxs-lookup"><span data-stu-id="4b4aa-222">If hello configuration was successful, it should say **CHAP**.</span></span>
   
    ![Dettagli destinazione preferita](./media/storsimple-configure-chap/IC740952.png)

## <a name="next-steps"></a><span data-ttu-id="4b4aa-224">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="4b4aa-224">Next steps</span></span>

* <span data-ttu-id="4b4aa-225">Ulteriori informazioni sulla [sicurezza di StorSimple](storsimple-8000-security.md).</span><span class="sxs-lookup"><span data-stu-id="4b4aa-225">Learn more about [StorSimple security](storsimple-8000-security.md).</span></span>
* <span data-ttu-id="4b4aa-226">Altre informazioni, vedere [utilizzando hello tooadminister servizio di gestione di dispositivi StorSimple dispositivo StorSimple](storsimple-8000-manager-service-administration.md).</span><span class="sxs-lookup"><span data-stu-id="4b4aa-226">Learn more about [using hello StorSimple Device Manager service tooadminister your StorSimple device](storsimple-8000-manager-service-administration.md).</span></span>


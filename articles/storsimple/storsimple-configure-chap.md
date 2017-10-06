---
title: aaaConfigure CHAP per dispositivo StorSimple serie 8000 | Documenti Microsoft
description: Viene descritto come tooconfigure hello Challenge Handshake Authentication Protocol (CHAP) in un dispositivo StorSimple.
services: storsimple
documentationcenter: 
author: alkohli
manager: carmonm
editor: 
ms.assetid: 467044d7-7885-4382-90bd-3148dbbd341f
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: TBD
ms.date: 08/17/2016
ms.author: alkohli
ms.openlocfilehash: 272ef2c184f56ad262e55410357494c72e45cf83
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="configure-chap-for-your-storsimple-device"></a><span data-ttu-id="e5f54-103">Configurare CHAP per il dispositivo StorSimple</span><span class="sxs-lookup"><span data-stu-id="e5f54-103">Configure CHAP for your StorSimple device</span></span>
<span data-ttu-id="e5f54-104">In questa esercitazione viene illustrato come tooconfigure CHAP per il dispositivo StorSimple.</span><span class="sxs-lookup"><span data-stu-id="e5f54-104">This tutorial explains how tooconfigure CHAP for your StorSimple device.</span></span> <span data-ttu-id="e5f54-105">procedura di Hello descritta in questo articolo si applica 8000 serie tooStorSimple, nonché i dispositivi StorSimple 1200.</span><span class="sxs-lookup"><span data-stu-id="e5f54-105">hello procedure detailed in this article applies tooStorSimple 8000 series as well as StorSimple 1200 devices.</span></span>

<span data-ttu-id="e5f54-106">CHAP è l'acronimo di Challenge Handshake Authentication Protocol.</span><span class="sxs-lookup"><span data-stu-id="e5f54-106">CHAP stands for Challenge Handshake Authentication Protocol.</span></span> <span data-ttu-id="e5f54-107">È uno schema di autenticazione utilizzato dall'identità di hello server toovalidate di client remoti.</span><span class="sxs-lookup"><span data-stu-id="e5f54-107">It is an authentication scheme used by servers toovalidate hello identity of remote clients.</span></span> <span data-ttu-id="e5f54-108">verifica di Hello si basa su una password condivisa o un segreto.</span><span class="sxs-lookup"><span data-stu-id="e5f54-108">hello verification is based on a shared password or secret.</span></span> <span data-ttu-id="e5f54-109">CHAP può essere unidirezionale o bidirezionale (reciproco).</span><span class="sxs-lookup"><span data-stu-id="e5f54-109">CHAP can be one-way (unidirectional) or mutual (bidirectional).</span></span> <span data-ttu-id="e5f54-110">CHAP unidirezionale è quando la destinazione hello autentica un iniziatore.</span><span class="sxs-lookup"><span data-stu-id="e5f54-110">One-way CHAP is when hello target authenticates an initiator.</span></span> <span data-ttu-id="e5f54-111">CHAP reciproco o inverso, sul hello invece necessario che la destinazione hello autentica l'iniziatore di hello e successivamente hello iniziatore autentica destinazione di hello.</span><span class="sxs-lookup"><span data-stu-id="e5f54-111">Mutual or reverse CHAP, on hello other hand, requires that hello target authenticate hello initiator and then hello initiator authenticate hello target.</span></span> <span data-ttu-id="e5f54-112">È possibile implementare l'autenticazione dell'iniziatore senza autenticazione della destinazione.</span><span class="sxs-lookup"><span data-stu-id="e5f54-112">Initiator authentication can be implemented without target authentication.</span></span> <span data-ttu-id="e5f54-113">L’autenticazione della destinazione, tuttavia, può essere implementata solo se viene implementata anche l'autenticazione dell'iniziatore.</span><span class="sxs-lookup"><span data-stu-id="e5f54-113">However, target authentication can be implemented only if initiator authentication is also implemented.</span></span> 

<span data-ttu-id="e5f54-114">Come procedura consigliata, è consigliabile utilizzare la sicurezza iSCSI tooenhance CHAP.</span><span class="sxs-lookup"><span data-stu-id="e5f54-114">As a best practice, we recommend that you use CHAP tooenhance iSCSI security.</span></span>

> [!NOTE]
> <span data-ttu-id="e5f54-115">Tenere presente che IPSEC non è attualmente supportato in dispositivi StorSimple.</span><span class="sxs-lookup"><span data-stu-id="e5f54-115">Keep in mind that IPSEC is not currently supported on StorSimple devices.</span></span>
> 
> 

<span data-ttu-id="e5f54-116">Hello CHAP nel dispositivo StorSimple hello possono essere configurate in hello seguenti modi:</span><span class="sxs-lookup"><span data-stu-id="e5f54-116">hello CHAP settings on hello StorSimple device can be configured in hello following ways:</span></span>

* <span data-ttu-id="e5f54-117">Autenticazione unidirezionale </span><span class="sxs-lookup"><span data-stu-id="e5f54-117">Unidirectional or one-way authentication</span></span>
* <span data-ttu-id="e5f54-118">Autenticazione bidirezionale, reciproca o inversa </span><span class="sxs-lookup"><span data-stu-id="e5f54-118">Bidirectional or mutual or reverse authentication</span></span>

<span data-ttu-id="e5f54-119">In ognuno di questi casi, il portale di hello per dispositivo hello e il software dell'iniziatore iSCSI di hello server deve toobe configurato.</span><span class="sxs-lookup"><span data-stu-id="e5f54-119">In each of these cases, hello portal for hello device and hello server iSCSI initiator software needs toobe configured.</span></span> <span data-ttu-id="e5f54-120">Hello i passaggi dettagliati per questa configurazione sono descritti nella seguente esercitazione hello.</span><span class="sxs-lookup"><span data-stu-id="e5f54-120">hello detailed steps for this configuration are described in hello following tutorial.</span></span>

## <a name="unidirectional-or-one-way-authentication"></a><span data-ttu-id="e5f54-121">Autenticazione unidirezionale </span><span class="sxs-lookup"><span data-stu-id="e5f54-121">Unidirectional or one-way authentication</span></span>
<span data-ttu-id="e5f54-122">Nell'autenticazione unidirezionale la destinazione hello autentica l'iniziatore di hello.</span><span class="sxs-lookup"><span data-stu-id="e5f54-122">In unidirectional authentication, hello target authenticates hello initiator.</span></span> <span data-ttu-id="e5f54-123">Questa autenticazione, è necessario configurare impostazioni dell'iniziatore CHAP di hello nel dispositivo StorSimple hello e hello iSCSI software Initiator in host hello.</span><span class="sxs-lookup"><span data-stu-id="e5f54-123">This authentication requires that you configure hello CHAP initiator settings on hello StorSimple device and hello iSCSI Initiator software on hello host.</span></span> <span data-ttu-id="e5f54-124">procedure dettagliate per il dispositivo StorSimple Hello e host di Windows vengono descritte di seguito.</span><span class="sxs-lookup"><span data-stu-id="e5f54-124">hello detailed procedures for your StorSimple device and Windows host are described next.</span></span>

#### <a name="tooconfigure-your-device-for-one-way-authentication"></a><span data-ttu-id="e5f54-125">tooconfigure del dispositivo per l'autenticazione unidirezionale</span><span class="sxs-lookup"><span data-stu-id="e5f54-125">tooconfigure your device for one-way authentication</span></span>
1. <span data-ttu-id="e5f54-126">Nel portale di Azure classico, in hello hello **dispositivi** pagina, fare clic su hello **configura** scheda.</span><span class="sxs-lookup"><span data-stu-id="e5f54-126">In hello Azure classic portal, on hello **Devices** page, click hello **Configure** tab.</span></span>
   
    ![Iniziatore CHAP](./media/storsimple-configure-chap/IC740943.png)
2. <span data-ttu-id="e5f54-128">Scorrere verso il basso, in questa pagina in hello **iniziatore CHAP** sezione:</span><span class="sxs-lookup"><span data-stu-id="e5f54-128">Scroll down on this page, and in hello **CHAP Initiator** section:</span></span>
   
   1. <span data-ttu-id="e5f54-129">Specificare un nome utente per l'iniziatore CHAP.</span><span class="sxs-lookup"><span data-stu-id="e5f54-129">Provide a user name for your CHAP initiator.</span></span>
   2. <span data-ttu-id="e5f54-130">Specificare una password per l'iniziatore CHAP.</span><span class="sxs-lookup"><span data-stu-id="e5f54-130">Supply a password for your CHAP initiator.</span></span>
      
    > [!IMPORTANT]
    > <span data-ttu-id="e5f54-131">nome utente Hello deve contenere meno di 233 caratteri.</span><span class="sxs-lookup"><span data-stu-id="e5f54-131">hello CHAP user name must contain fewer than 233 characters.</span></span> <span data-ttu-id="e5f54-132">password CHAP Hello deve essere compreso tra 12 e 16 caratteri.</span><span class="sxs-lookup"><span data-stu-id="e5f54-132">hello CHAP password must be between 12 and 16 characters.</span></span> <span data-ttu-id="e5f54-133">Un nome utente o una password più lungo comporterà un errore di autenticazione sull'host di Windows hello.</span><span class="sxs-lookup"><span data-stu-id="e5f54-133">A longer user name or password will result in an authentication failure on hello Windows host.</span></span>
   
   3. <span data-ttu-id="e5f54-134">Conferma password hello.</span><span class="sxs-lookup"><span data-stu-id="e5f54-134">Confirm hello password.</span></span>
3. <span data-ttu-id="e5f54-135">Fare clic su **Salva**.</span><span class="sxs-lookup"><span data-stu-id="e5f54-135">Click **Save**.</span></span> <span data-ttu-id="e5f54-136">Verrà visualizzato un messaggio di conferma.</span><span class="sxs-lookup"><span data-stu-id="e5f54-136">A confirmation message will be displayed.</span></span> <span data-ttu-id="e5f54-137">Fare clic su **OK** modifiche hello toosave.</span><span class="sxs-lookup"><span data-stu-id="e5f54-137">Click **OK** toosave hello changes.</span></span>

#### <a name="tooconfigure-one-way-authentication-on-hello-windows-host-server"></a><span data-ttu-id="e5f54-138">server host tooconfigure autenticazione unidirezionale in Windows hello</span><span class="sxs-lookup"><span data-stu-id="e5f54-138">tooconfigure one-way authentication on hello Windows host server</span></span>
1. <span data-ttu-id="e5f54-139">Nel server host di Windows hello, avviare l'iniziatore iSCSI hello.</span><span class="sxs-lookup"><span data-stu-id="e5f54-139">On hello Windows host server, start hello iSCSI Initiator.</span></span>
2. <span data-ttu-id="e5f54-140">In hello **iniziatore iSCSI-proprietà** finestra, eseguire hello alla procedura seguente:</span><span class="sxs-lookup"><span data-stu-id="e5f54-140">In hello **iSCSI Initiator Properties** window, perform hello following steps:</span></span>
   
   1. <span data-ttu-id="e5f54-141">Fare clic su hello **individuazione** scheda.</span><span class="sxs-lookup"><span data-stu-id="e5f54-141">Click hello **Discovery** tab.</span></span>
      
       ![Proprietà iniziatore iSCSI](./media/storsimple-configure-chap/IC740944.png)
   2. <span data-ttu-id="e5f54-143">Fare clic su **Individua portale**.</span><span class="sxs-lookup"><span data-stu-id="e5f54-143">Click **Discover Portal**.</span></span>
3. <span data-ttu-id="e5f54-144">In hello **individua portale destinazione** la finestra di dialogo:</span><span class="sxs-lookup"><span data-stu-id="e5f54-144">In hello **Discover Target Portal** dialog box:</span></span>
   
   1. <span data-ttu-id="e5f54-145">Specificare l'indirizzo IP di hello del dispositivo.</span><span class="sxs-lookup"><span data-stu-id="e5f54-145">Specify hello IP address of your device.</span></span>
   2. <span data-ttu-id="e5f54-146">Fare clic su **Advanced**.</span><span class="sxs-lookup"><span data-stu-id="e5f54-146">Click **Advanced**.</span></span>
      
       ![Individua portale destinazione](./media/storsimple-configure-chap/IC740945.png)
4. <span data-ttu-id="e5f54-148">In hello **impostazioni avanzate** la finestra di dialogo:</span><span class="sxs-lookup"><span data-stu-id="e5f54-148">In hello **Advanced Settings** dialog box:</span></span>
   
   1. <span data-ttu-id="e5f54-149">Seleziona hello **Abilita accesso CHAP** casella di controllo.</span><span class="sxs-lookup"><span data-stu-id="e5f54-149">Select hello **Enable CHAP log on** check box.</span></span>
   2. <span data-ttu-id="e5f54-150">In hello **nome** campo, specificare hello il nome utente specificato per hello iniziatore CHAP nel portale classico hello.</span><span class="sxs-lookup"><span data-stu-id="e5f54-150">In hello **Name** field, supply hello user name that you specified for hello CHAP Initiator in hello classic portal.</span></span>
   3. <span data-ttu-id="e5f54-151">In hello **segreto destinazione** campo, una password di hello alimentatore specificato per hello iniziatore CHAP nel portale classico hello.</span><span class="sxs-lookup"><span data-stu-id="e5f54-151">In hello **Target secret** field, supply hello password that you specified for hello CHAP Initiator in hello classic portal.</span></span>
   4. <span data-ttu-id="e5f54-152">Fare clic su **OK**.</span><span class="sxs-lookup"><span data-stu-id="e5f54-152">Click **OK**.</span></span>
      
       ![Impostazioni avanzate - Generale](./media/storsimple-configure-chap/IC740946.png)
5. <span data-ttu-id="e5f54-154">In hello **destinazioni** scheda di hello **iniziatore iSCSI-proprietà** , lo stato del dispositivo hello finestra come **connesso**.</span><span class="sxs-lookup"><span data-stu-id="e5f54-154">On hello **Targets** tab of hello **iSCSI Initiator Properties** window, hello device status should appear as **Connected**.</span></span> <span data-ttu-id="e5f54-155">Se si usa un dispositivo StorSimple 1200, ogni volume verrà montato come destinazione iSCSI, come illustrato di seguito.</span><span class="sxs-lookup"><span data-stu-id="e5f54-155">If you are using a StorSimple 1200 device, then each volume will be mounted as an iSCSI target as shown below.</span></span> <span data-ttu-id="e5f54-156">Di conseguenza, i passaggi 3 e 4, saranno necessario toobe ripetuto per ogni volume.</span><span class="sxs-lookup"><span data-stu-id="e5f54-156">Hence, steps  3-4 will need toobe repeated for each volume.</span></span>
   
    ![Volumi montati come destinazioni separate](./media/storsimple-configure-chap/chap4.png)
   
   > [!IMPORTANT]
   > <span data-ttu-id="e5f54-158">Se si modifica il nome di iSCSI hello, nuovo nome hello verrà utilizzato per le nuove sessioni iSCSI.</span><span class="sxs-lookup"><span data-stu-id="e5f54-158">If you change hello iSCSI name, hello new name will be used for new iSCSI sessions.</span></span> <span data-ttu-id="e5f54-159">Le nuove impostazioni non vengono utilizzate per le sessioni esistenti fino a quando non si esegue la disconnessione e il nuovo accesso.</span><span class="sxs-lookup"><span data-stu-id="e5f54-159">New settings are not used for existing sessions until you log off and log on again.</span></span>
   > 
   > 

<span data-ttu-id="e5f54-160">Per ulteriori informazioni sulla configurazione dell'autenticazione CHAP nel server host di Windows hello, andare troppo[considerazioni aggiuntive](#additional-considerations).</span><span class="sxs-lookup"><span data-stu-id="e5f54-160">For more information about configuring CHAP on hello Windows host server, go too[Additional considerations](#additional-considerations).</span></span>

## <a name="bidirectional-or-mutual-authentication"></a><span data-ttu-id="e5f54-161">Autenticazione bidirezionale o reciproca </span><span class="sxs-lookup"><span data-stu-id="e5f54-161">Bidirectional or mutual authentication</span></span>
<span data-ttu-id="e5f54-162">Nell'autenticazione bidirezionale destinazione hello l'autenticazione dell'iniziatore hello e iniziatore hello destinazione hello.</span><span class="sxs-lookup"><span data-stu-id="e5f54-162">In bidirectional authentication, hello target authenticates hello initiator and then hello initiator authenticates hello target.</span></span> <span data-ttu-id="e5f54-163">Questa operazione richiede le impostazioni dell'iniziatore CHAP hello tooconfigure utente hello, nonché hello reverse impostazioni CHAP nel dispositivo hello e iSCSI software Initiator in host hello.</span><span class="sxs-lookup"><span data-stu-id="e5f54-163">This requires hello user tooconfigure hello CHAP initiator settings, as well as hello reverse CHAP settings on hello device and iSCSI Initiator software on hello host.</span></span> <span data-ttu-id="e5f54-164">Hello procedure seguenti descrivono l'autenticazione reciproca hello passaggi tooconfigure nel dispositivo di hello e nell'host di Windows hello.</span><span class="sxs-lookup"><span data-stu-id="e5f54-164">hello following procedures describe hello steps tooconfigure mutual authentication on hello device and on hello Windows host.</span></span>

#### <a name="tooconfigure-your-device-for-mutual-authentication"></a><span data-ttu-id="e5f54-165">tooconfigure il dispositivo per l'autenticazione reciproca</span><span class="sxs-lookup"><span data-stu-id="e5f54-165">tooconfigure your device for mutual authentication</span></span>
1. <span data-ttu-id="e5f54-166">Nel portale di Azure classico, in hello hello **dispositivi** pagina, fare clic su hello **configura** scheda.</span><span class="sxs-lookup"><span data-stu-id="e5f54-166">In hello Azure classic portal, on hello **Devices** page, click hello **Configure** tab.</span></span>
   
    ![Destinazione CHAP](./media/storsimple-configure-chap/IC740948.png)
2. <span data-ttu-id="e5f54-168">Scorrere verso il basso, in questa pagina in hello **destinazione CHAP** sezione:</span><span class="sxs-lookup"><span data-stu-id="e5f54-168">Scroll down on this page, and in hello **CHAP Target** section:</span></span>
   
   1. <span data-ttu-id="e5f54-169">Fornire un **nome utente per l’autenticazione CHAP inversa** per il dispositivo.</span><span class="sxs-lookup"><span data-stu-id="e5f54-169">Provide a **Reverse CHAP user name** for your device.</span></span>
   2. <span data-ttu-id="e5f54-170">Fornire una **password per l’autenticazione CHAP inversa** per il dispositivo.</span><span class="sxs-lookup"><span data-stu-id="e5f54-170">Supply a **Reverse CHAP password** for your device.</span></span>
   3. <span data-ttu-id="e5f54-171">Conferma password hello.</span><span class="sxs-lookup"><span data-stu-id="e5f54-171">Confirm hello password.</span></span>
3. <span data-ttu-id="e5f54-172">In hello **iniziatore CHAP** sezione:</span><span class="sxs-lookup"><span data-stu-id="e5f54-172">In hello **CHAP Initiator** section:</span></span>
   
   1. <span data-ttu-id="e5f54-173">Specificare un **nome utente** per il dispositivo.</span><span class="sxs-lookup"><span data-stu-id="e5f54-173">Provide a **user name** for your device.</span></span>
   2. <span data-ttu-id="e5f54-174">Specificare una **password** per il dispositivo.</span><span class="sxs-lookup"><span data-stu-id="e5f54-174">Provide a **password** for your device.</span></span>
   3. <span data-ttu-id="e5f54-175">Conferma password hello.</span><span class="sxs-lookup"><span data-stu-id="e5f54-175">Confirm hello password.</span></span>
4. <span data-ttu-id="e5f54-176">Fare clic su **Salva**.</span><span class="sxs-lookup"><span data-stu-id="e5f54-176">Click **Save**.</span></span> <span data-ttu-id="e5f54-177">Verrà visualizzato un messaggio di conferma.</span><span class="sxs-lookup"><span data-stu-id="e5f54-177">A confirmation message will be displayed.</span></span> <span data-ttu-id="e5f54-178">Fare clic su **OK** modifiche hello toosave.</span><span class="sxs-lookup"><span data-stu-id="e5f54-178">Click **OK** toosave hello changes.</span></span>

#### <a name="tooconfigure-bidirectional-authentication-on-hello-windows-host-server"></a><span data-ttu-id="e5f54-179">autenticazione bidirezionale tooconfigure in Windows hello server host</span><span class="sxs-lookup"><span data-stu-id="e5f54-179">tooconfigure bidirectional authentication on hello Windows host server</span></span>
1. <span data-ttu-id="e5f54-180">Nel server host di Windows hello, avviare l'iniziatore iSCSI hello.</span><span class="sxs-lookup"><span data-stu-id="e5f54-180">On hello Windows host server, start hello iSCSI Initiator.</span></span>
2. <span data-ttu-id="e5f54-181">In hello **iniziatore iSCSI-proprietà** finestra, fare clic su hello **configurazione** scheda.</span><span class="sxs-lookup"><span data-stu-id="e5f54-181">In hello **iSCSI Initiator Properties** window, click hello **Configuration** tab.</span></span>
3. <span data-ttu-id="e5f54-182">Fare clic su **CHAP**.</span><span class="sxs-lookup"><span data-stu-id="e5f54-182">Click **CHAP**.</span></span>
4. <span data-ttu-id="e5f54-183">In hello **segreto autenticazione CHAP reciproca iniziatore iSCSI** la finestra di dialogo:</span><span class="sxs-lookup"><span data-stu-id="e5f54-183">In hello **iSCSI Initiator Mutual CHAP Secret** dialog box:</span></span>
   
   1. <span data-ttu-id="e5f54-184">Hello tipo **Password di autenticazione CHAP inversa** configurate nel portale di Azure classico hello.</span><span class="sxs-lookup"><span data-stu-id="e5f54-184">Type hello **Reverse CHAP Password** that you configured in hello Azure classic portal.</span></span>
   2. <span data-ttu-id="e5f54-185">Fare clic su **OK**.</span><span class="sxs-lookup"><span data-stu-id="e5f54-185">Click **OK**.</span></span>
      
       ![Segreto autenticazione CHAP reciproca iniziatore iSCSI](./media/storsimple-configure-chap/IC740949.png)
5. <span data-ttu-id="e5f54-187">Fare clic su hello **destinazioni** scheda.</span><span class="sxs-lookup"><span data-stu-id="e5f54-187">Click hello **Targets** tab.</span></span>
6. <span data-ttu-id="e5f54-188">Fare clic su hello **Connetti** pulsante.</span><span class="sxs-lookup"><span data-stu-id="e5f54-188">Click hello **Connect** button.</span></span> 
7. <span data-ttu-id="e5f54-189">In hello **connettersi tooTarget** la finestra di dialogo, fare clic su **avanzate**.</span><span class="sxs-lookup"><span data-stu-id="e5f54-189">In hello **Connect tooTarget** dialog box, click **Advanced**.</span></span>
8. <span data-ttu-id="e5f54-190">In hello **proprietà avanzate** la finestra di dialogo:</span><span class="sxs-lookup"><span data-stu-id="e5f54-190">In hello **Advanced Properties** dialog box:</span></span>
   
   1. <span data-ttu-id="e5f54-191">Seleziona hello **Abilita accesso CHAP** casella di controllo.</span><span class="sxs-lookup"><span data-stu-id="e5f54-191">Select hello **Enable CHAP log on** check box.</span></span>
   2. <span data-ttu-id="e5f54-192">In hello **nome** campo, specificare hello il nome utente specificato per hello iniziatore CHAP nel portale classico hello.</span><span class="sxs-lookup"><span data-stu-id="e5f54-192">In hello **Name** field, supply hello user name that you specified for hello CHAP Initiator in hello classic portal.</span></span>
   3. <span data-ttu-id="e5f54-193">In hello **segreto destinazione** campo, una password di hello alimentatore specificato per hello iniziatore CHAP nel portale classico hello.</span><span class="sxs-lookup"><span data-stu-id="e5f54-193">In hello **Target secret** field, supply hello password that you specified for hello CHAP Initiator in hello classic portal.</span></span>
   4. <span data-ttu-id="e5f54-194">Seleziona hello **Esegui autenticazione reciproca** casella di controllo.</span><span class="sxs-lookup"><span data-stu-id="e5f54-194">Select hello **Perform mutual authentication** check box.</span></span>
      
       ![Impostazioni avanzate - Autenticazione reciproca](./media/storsimple-configure-chap/IC740950.png)
   5. <span data-ttu-id="e5f54-196">Fare clic su **OK** configurazione di CHAP hello toocomplete</span><span class="sxs-lookup"><span data-stu-id="e5f54-196">Click **OK** toocomplete hello CHAP configuration</span></span>

<span data-ttu-id="e5f54-197">Per ulteriori informazioni sulla configurazione dell'autenticazione CHAP nel server host di Windows hello, andare troppo[considerazioni aggiuntive](#additional-considerations).</span><span class="sxs-lookup"><span data-stu-id="e5f54-197">For more information about configuring CHAP on hello Windows host server, go too[Additional considerations](#additional-considerations).</span></span>

## <a name="additional-considerations"></a><span data-ttu-id="e5f54-198">Considerazioni aggiuntive</span><span class="sxs-lookup"><span data-stu-id="e5f54-198">Additional considerations</span></span>
<span data-ttu-id="e5f54-199">Hello **connessione rapida** funzionalità non supporta le connessioni con CHAP abilitato.</span><span class="sxs-lookup"><span data-stu-id="e5f54-199">hello **Quick Connect** feature does not support connections that have CHAP enabled.</span></span> <span data-ttu-id="e5f54-200">Quando è abilitata l'autenticazione CHAP, assicurarsi di utilizzare hello **Connetti** pulsante è disponibile in hello **destinazioni** destinazione tooa tooconnect di scheda.</span><span class="sxs-lookup"><span data-stu-id="e5f54-200">When CHAP is enabled, make sure that you use hello **Connect** button that is available on hello **Targets** tab tooconnect tooa target.</span></span>

![Connettersi tootarget](./media/storsimple-configure-chap/IC740947.png)

<span data-ttu-id="e5f54-202">In hello **connettersi tooTarget** la finestra di dialogo che è disponibile, seleziona hello **aggiungere questo elenco toohello connessione destinazioni preferite** casella di controllo.</span><span class="sxs-lookup"><span data-stu-id="e5f54-202">In hello **Connect tooTarget** dialog box that is presented, select hello **Add this connection toohello list of Favorite Targets** check box.</span></span> <span data-ttu-id="e5f54-203">In questo modo si garantisce che ogni riavvio del computer hello, viene effettuato un tentativo toorestore hello connessione toohello iSCSI alle destinazioni preferite.</span><span class="sxs-lookup"><span data-stu-id="e5f54-203">This ensures that every time hello computer restarts, an attempt is made toorestore hello connection toohello iSCSI favorite targets.</span></span>

## <a name="errors-during-configuration"></a><span data-ttu-id="e5f54-204">Errori durante la configurazione</span><span class="sxs-lookup"><span data-stu-id="e5f54-204">Errors during configuration</span></span>
<span data-ttu-id="e5f54-205">Se la configurazione CHAP non è corretta, quindi si è probabilmente toosee un **errore di autenticazione** messaggio di errore.</span><span class="sxs-lookup"><span data-stu-id="e5f54-205">If your CHAP configuration is incorrect, then you are likely toosee an **Authentication failure** error message.</span></span>

## <a name="verification-of-chap-configuration"></a><span data-ttu-id="e5f54-206">Verifica della configurazione di CHAP</span><span class="sxs-lookup"><span data-stu-id="e5f54-206">Verification of CHAP configuration</span></span>
<span data-ttu-id="e5f54-207">È possibile verificare che sia in uso dell'autenticazione CHAP completando hello alla procedura seguente.</span><span class="sxs-lookup"><span data-stu-id="e5f54-207">You can verify that CHAP is being used by completing hello following steps.</span></span>

#### <a name="tooverify-your-chap-configuration"></a><span data-ttu-id="e5f54-208">tooverify la configurazione CHAP</span><span class="sxs-lookup"><span data-stu-id="e5f54-208">tooverify your CHAP configuration</span></span>
1. <span data-ttu-id="e5f54-209">Fare clic su **Destinazioni preferite**.</span><span class="sxs-lookup"><span data-stu-id="e5f54-209">Click **Favorite Targets**.</span></span>
2. <span data-ttu-id="e5f54-210">Selezionare hello di destinazione per cui è abilitata l'autenticazione.</span><span class="sxs-lookup"><span data-stu-id="e5f54-210">Select hello target for which you enabled authentication.</span></span>
3. <span data-ttu-id="e5f54-211">Fare clic su **Dettagli**.</span><span class="sxs-lookup"><span data-stu-id="e5f54-211">Click **Details**.</span></span>
   
    ![Proprietà iniziatore iSCSI - Destinazioni preferite](./media/storsimple-configure-chap/IC740951.png)
4. <span data-ttu-id="e5f54-213">In hello **dettagli destinazione preferita** nella finestra di dialogo immissione hello nota in hello **autenticazione** campo.</span><span class="sxs-lookup"><span data-stu-id="e5f54-213">In hello **Favorite Target Details** dialog box, note hello entry in hello **Authentication** field.</span></span> <span data-ttu-id="e5f54-214">Se la configurazione hello ha esito positivo, dovrebbe essere visualizzato **CHAP**.</span><span class="sxs-lookup"><span data-stu-id="e5f54-214">If hello configuration was successful, it should say **CHAP**.</span></span>
   
    ![Dettagli destinazione preferita](./media/storsimple-configure-chap/IC740952.png)

## <a name="next-steps"></a><span data-ttu-id="e5f54-216">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="e5f54-216">Next steps</span></span>
* <span data-ttu-id="e5f54-217">Ulteriori informazioni sulla [sicurezza di StorSimple](storsimple-security.md).</span><span class="sxs-lookup"><span data-stu-id="e5f54-217">Learn more about [StorSimple security](storsimple-security.md).</span></span>
* <span data-ttu-id="e5f54-218">Altre informazioni, vedere [utilizzando hello tooadminister servizio StorSimple Manager dispositivo StorSimple](storsimple-manager-service-administration.md).</span><span class="sxs-lookup"><span data-stu-id="e5f54-218">Learn more about [using hello StorSimple Manager service tooadminister your StorSimple device](storsimple-manager-service-administration.md).</span></span>


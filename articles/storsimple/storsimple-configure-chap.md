---
title: Configurare CHAP per il dispositivo StorSimple serie 8000 | Documentazione Microsoft
description: Viene descritto come configurare Challenge Handshake Authentication Protocol su un dispositivo StorSimple.
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
ms.openlocfilehash: 36b4e73d0336deb9560d44163fc5330d1c9d775c
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="configure-chap-for-your-storsimple-device"></a><span data-ttu-id="c6213-103">Configurare CHAP per il dispositivo StorSimple</span><span class="sxs-lookup"><span data-stu-id="c6213-103">Configure CHAP for your StorSimple device</span></span>
<span data-ttu-id="c6213-104">In questa esercitazione viene illustrato come configurare CHAP per il dispositivo StorSimple.</span><span class="sxs-lookup"><span data-stu-id="c6213-104">This tutorial explains how to configure CHAP for your StorSimple device.</span></span> <span data-ttu-id="c6213-105">La procedura descritta in questo articolo si applica ai dispositivi StorSimple serie 8000 e StorSimple 1200.</span><span class="sxs-lookup"><span data-stu-id="c6213-105">The procedure detailed in this article applies to StorSimple 8000 series as well as StorSimple 1200 devices.</span></span>

<span data-ttu-id="c6213-106">CHAP è l'acronimo di Challenge Handshake Authentication Protocol.</span><span class="sxs-lookup"><span data-stu-id="c6213-106">CHAP stands for Challenge Handshake Authentication Protocol.</span></span> <span data-ttu-id="c6213-107">È uno schema di autenticazione utilizzato dal server per convalidare l'identità dei client remoti.</span><span class="sxs-lookup"><span data-stu-id="c6213-107">It is an authentication scheme used by servers to validate the identity of remote clients.</span></span> <span data-ttu-id="c6213-108">La verifica si basa su una password condivisa o un segreto.</span><span class="sxs-lookup"><span data-stu-id="c6213-108">The verification is based on a shared password or secret.</span></span> <span data-ttu-id="c6213-109">CHAP può essere unidirezionale o bidirezionale (reciproco).</span><span class="sxs-lookup"><span data-stu-id="c6213-109">CHAP can be one-way (unidirectional) or mutual (bidirectional).</span></span> <span data-ttu-id="c6213-110">L'autenticazione CHAP unidirezionale avviene quando la destinazione autentica un iniziatore.</span><span class="sxs-lookup"><span data-stu-id="c6213-110">One-way CHAP is when the target authenticates an initiator.</span></span> <span data-ttu-id="c6213-111">Per l'autenticazione CHAP reciproca o inversa è necessario che la destinazione autentichi l'iniziatore e viceversa.</span><span class="sxs-lookup"><span data-stu-id="c6213-111">Mutual or reverse CHAP, on the other hand, requires that the target authenticate the initiator and then the initiator authenticate the target.</span></span> <span data-ttu-id="c6213-112">È possibile implementare l'autenticazione dell'iniziatore senza autenticazione della destinazione.</span><span class="sxs-lookup"><span data-stu-id="c6213-112">Initiator authentication can be implemented without target authentication.</span></span> <span data-ttu-id="c6213-113">L’autenticazione della destinazione, tuttavia, può essere implementata solo se viene implementata anche l'autenticazione dell'iniziatore.</span><span class="sxs-lookup"><span data-stu-id="c6213-113">However, target authentication can be implemented only if initiator authentication is also implemented.</span></span> 

<span data-ttu-id="c6213-114">Come procedura consigliata, si raccomanda l’uso di CHAP per migliorare la sicurezza iSCSI.</span><span class="sxs-lookup"><span data-stu-id="c6213-114">As a best practice, we recommend that you use CHAP to enhance iSCSI security.</span></span>

> [!NOTE]
> <span data-ttu-id="c6213-115">Tenere presente che IPSEC non è attualmente supportato in dispositivi StorSimple.</span><span class="sxs-lookup"><span data-stu-id="c6213-115">Keep in mind that IPSEC is not currently supported on StorSimple devices.</span></span>
> 
> 

<span data-ttu-id="c6213-116">Le impostazioni CHAP nel dispositivo StorSimple possono essere configurate nei modi seguenti:</span><span class="sxs-lookup"><span data-stu-id="c6213-116">The CHAP settings on the StorSimple device can be configured in the following ways:</span></span>

* <span data-ttu-id="c6213-117">Autenticazione unidirezionale </span><span class="sxs-lookup"><span data-stu-id="c6213-117">Unidirectional or one-way authentication</span></span>
* <span data-ttu-id="c6213-118">Autenticazione bidirezionale, reciproca o inversa </span><span class="sxs-lookup"><span data-stu-id="c6213-118">Bidirectional or mutual or reverse authentication</span></span>

<span data-ttu-id="c6213-119">In ognuno di questi casi, è necessario configurare il portale del dispositivo e il software dell'iniziatore iSCSI del server.</span><span class="sxs-lookup"><span data-stu-id="c6213-119">In each of these cases, the portal for the device and the server iSCSI initiator software needs to be configured.</span></span> <span data-ttu-id="c6213-120">Nell'esercitazione seguente sono descritti i passaggi dettagliati per questa configurazione.</span><span class="sxs-lookup"><span data-stu-id="c6213-120">The detailed steps for this configuration are described in the following tutorial.</span></span>

## <a name="unidirectional-or-one-way-authentication"></a><span data-ttu-id="c6213-121">Autenticazione unidirezionale </span><span class="sxs-lookup"><span data-stu-id="c6213-121">Unidirectional or one-way authentication</span></span>
<span data-ttu-id="c6213-122">Nell’autenticazione unidirezionale, la destinazione autentica l'iniziatore.</span><span class="sxs-lookup"><span data-stu-id="c6213-122">In unidirectional authentication, the target authenticates the initiator.</span></span> <span data-ttu-id="c6213-123">Questa autenticazione richiede che si configurino le impostazioni  dell’iniziatore CHAP sul dispositivo StorSimple e il software dell’iniziatore iSCSI nell'host.</span><span class="sxs-lookup"><span data-stu-id="c6213-123">This authentication requires that you configure the CHAP initiator settings on the StorSimple device and the iSCSI Initiator software on the host.</span></span> <span data-ttu-id="c6213-124">Le procedure dettagliate per il dispositivo StorSimple e l’host di Windows sono descritte di seguito.</span><span class="sxs-lookup"><span data-stu-id="c6213-124">The detailed procedures for your StorSimple device and Windows host are described next.</span></span>

#### <a name="to-configure-your-device-for-one-way-authentication"></a><span data-ttu-id="c6213-125">Per configurare il dispositivo per l'autenticazione unidirezionale</span><span class="sxs-lookup"><span data-stu-id="c6213-125">To configure your device for one-way authentication</span></span>
1. <span data-ttu-id="c6213-126">Nella pagina **Dispositivi** del portale di Azure classico fare clic su sulla scheda **Configura**.</span><span class="sxs-lookup"><span data-stu-id="c6213-126">In the Azure classic portal, on the **Devices** page, click the **Configure** tab.</span></span>
   
    ![Iniziatore CHAP](./media/storsimple-configure-chap/IC740943.png)
2. <span data-ttu-id="c6213-128">Scorrere verso il basso in questa pagina e nella sezione **Iniziatore CHAP** :</span><span class="sxs-lookup"><span data-stu-id="c6213-128">Scroll down on this page, and in the **CHAP Initiator** section:</span></span>
   
   1. <span data-ttu-id="c6213-129">Specificare un nome utente per l'iniziatore CHAP.</span><span class="sxs-lookup"><span data-stu-id="c6213-129">Provide a user name for your CHAP initiator.</span></span>
   2. <span data-ttu-id="c6213-130">Specificare una password per l'iniziatore CHAP.</span><span class="sxs-lookup"><span data-stu-id="c6213-130">Supply a password for your CHAP initiator.</span></span>
      
    > [!IMPORTANT]
    > <span data-ttu-id="c6213-131">Il nome dell'utente CHAP deve contenere meno di 233 caratteri.</span><span class="sxs-lookup"><span data-stu-id="c6213-131">The CHAP user name must contain fewer than 233 characters.</span></span> <span data-ttu-id="c6213-132">La password CHAP deve essere compresa tra 12 e 16 caratteri.</span><span class="sxs-lookup"><span data-stu-id="c6213-132">The CHAP password must be between 12 and 16 characters.</span></span> <span data-ttu-id="c6213-133">Se si prova a usare un nome utente o una password più lunga si verificherà un errore di autenticazione sull'host Windows.</span><span class="sxs-lookup"><span data-stu-id="c6213-133">A longer user name or password will result in an authentication failure on the Windows host.</span></span>
   
   3. <span data-ttu-id="c6213-134">Confermare la password.</span><span class="sxs-lookup"><span data-stu-id="c6213-134">Confirm the password.</span></span>
3. <span data-ttu-id="c6213-135">Fare clic su **Save**.</span><span class="sxs-lookup"><span data-stu-id="c6213-135">Click **Save**.</span></span> <span data-ttu-id="c6213-136">Verrà visualizzato un messaggio di conferma.</span><span class="sxs-lookup"><span data-stu-id="c6213-136">A confirmation message will be displayed.</span></span> <span data-ttu-id="c6213-137">Fare clic su **OK** per salvare le modifiche.</span><span class="sxs-lookup"><span data-stu-id="c6213-137">Click **OK** to save the changes.</span></span>

#### <a name="to-configure-one-way-authentication-on-the-windows-host-server"></a><span data-ttu-id="c6213-138">Per configurare l'autenticazione unidirezionale nel server host di Windows</span><span class="sxs-lookup"><span data-stu-id="c6213-138">To configure one-way authentication on the Windows host server</span></span>
1. <span data-ttu-id="c6213-139">Nel server host di Windows, avviare l'iniziatore iSCSI.</span><span class="sxs-lookup"><span data-stu-id="c6213-139">On the Windows host server, start the iSCSI Initiator.</span></span>
2. <span data-ttu-id="c6213-140">Nella finestra **Proprietà iniziatore iSCSI** , effettuare le seguenti operazioni:</span><span class="sxs-lookup"><span data-stu-id="c6213-140">In the **iSCSI Initiator Properties** window, perform the following steps:</span></span>
   
   1. <span data-ttu-id="c6213-141">Scegliere la scheda **Individuazione** .</span><span class="sxs-lookup"><span data-stu-id="c6213-141">Click the **Discovery** tab.</span></span>
      
       ![Proprietà iniziatore iSCSI](./media/storsimple-configure-chap/IC740944.png)
   2. <span data-ttu-id="c6213-143">Fare clic su **Individua portale**.</span><span class="sxs-lookup"><span data-stu-id="c6213-143">Click **Discover Portal**.</span></span>
3. <span data-ttu-id="c6213-144">Nella finestra di dialogo **Individua portale destinazione** :</span><span class="sxs-lookup"><span data-stu-id="c6213-144">In the **Discover Target Portal** dialog box:</span></span>
   
   1. <span data-ttu-id="c6213-145">Specificare l'indirizzo IP del dispositivo:</span><span class="sxs-lookup"><span data-stu-id="c6213-145">Specify the IP address of your device.</span></span>
   2. <span data-ttu-id="c6213-146">Fare clic su **Advanced**.</span><span class="sxs-lookup"><span data-stu-id="c6213-146">Click **Advanced**.</span></span>
      
       ![Individua portale destinazione](./media/storsimple-configure-chap/IC740945.png)
4. <span data-ttu-id="c6213-148">Nella finestra di dialogo **Impostazioni avanzate** :</span><span class="sxs-lookup"><span data-stu-id="c6213-148">In the **Advanced Settings** dialog box:</span></span>
   
   1. <span data-ttu-id="c6213-149">Selezionare la casella di controllo **Attiva accesso CHAP** .</span><span class="sxs-lookup"><span data-stu-id="c6213-149">Select the **Enable CHAP log on** check box.</span></span>
   2. <span data-ttu-id="c6213-150">Nel campo **Nome** , inserire il nome utente specificato per l'iniziatore CHAP nel portale classico.</span><span class="sxs-lookup"><span data-stu-id="c6213-150">In the **Name** field, supply the user name that you specified for the CHAP Initiator in the classic portal.</span></span>
   3. <span data-ttu-id="c6213-151">Nel campo **Segreto destinazione** , inserire la password specificata per l'iniziatore CHAP nel portale classico.</span><span class="sxs-lookup"><span data-stu-id="c6213-151">In the **Target secret** field, supply the password that you specified for the CHAP Initiator in the classic portal.</span></span>
   4. <span data-ttu-id="c6213-152">Fare clic su **OK**.</span><span class="sxs-lookup"><span data-stu-id="c6213-152">Click **OK**.</span></span>
      
       ![Impostazioni avanzate - Generale](./media/storsimple-configure-chap/IC740946.png)
5. <span data-ttu-id="c6213-154">Nella scheda **Destinazioni** della finestra **iSCSI Initiator Properties** (Proprietà iniziatore iSCSI) lo stato del dispositivo deve essere visualizzato come **Connesso**.</span><span class="sxs-lookup"><span data-stu-id="c6213-154">On the **Targets** tab of the **iSCSI Initiator Properties** window, the device status should appear as **Connected**.</span></span> <span data-ttu-id="c6213-155">Se si usa un dispositivo StorSimple 1200, ogni volume verrà montato come destinazione iSCSI, come illustrato di seguito.</span><span class="sxs-lookup"><span data-stu-id="c6213-155">If you are using a StorSimple 1200 device, then each volume will be mounted as an iSCSI target as shown below.</span></span> <span data-ttu-id="c6213-156">Di conseguenza, i passaggi 3 e 4 dovranno essere ripetuti per ogni volume.</span><span class="sxs-lookup"><span data-stu-id="c6213-156">Hence, steps  3-4 will need to be repeated for each volume.</span></span>
   
    ![Volumi montati come destinazioni separate](./media/storsimple-configure-chap/chap4.png)
   
   > [!IMPORTANT]
   > <span data-ttu-id="c6213-158">Se si modifica il nome iSCSI, il nuovo nome verrà utilizzato per le nuove sessioni iSCSI.</span><span class="sxs-lookup"><span data-stu-id="c6213-158">If you change the iSCSI name, the new name will be used for new iSCSI sessions.</span></span> <span data-ttu-id="c6213-159">Le nuove impostazioni non vengono utilizzate per le sessioni esistenti fino a quando non si esegue la disconnessione e il nuovo accesso.</span><span class="sxs-lookup"><span data-stu-id="c6213-159">New settings are not used for existing sessions until you log off and log on again.</span></span>
   > 
   > 

<span data-ttu-id="c6213-160">Per ulteriori informazioni sulla configurazione di CHAP nel server host di Windows, andare a [Ulteriori considerazioni](#additional-considerations).</span><span class="sxs-lookup"><span data-stu-id="c6213-160">For more information about configuring CHAP on the Windows host server, go to [Additional considerations](#additional-considerations).</span></span>

## <a name="bidirectional-or-mutual-authentication"></a><span data-ttu-id="c6213-161">Autenticazione bidirezionale o reciproca </span><span class="sxs-lookup"><span data-stu-id="c6213-161">Bidirectional or mutual authentication</span></span>
<span data-ttu-id="c6213-162">Nell'autenticazione bidirezionale la destinazione autentica l'iniziatore e poi l’iniziatore autentica la destinazione.</span><span class="sxs-lookup"><span data-stu-id="c6213-162">In bidirectional authentication, the target authenticates the initiator and then the initiator authenticates the target.</span></span> <span data-ttu-id="c6213-163">A tal fine è necessario che l'utente configuri le impostazioni dell’iniziatore CHAP nonché le impostazioni di autenticazione CHAP inversa sul dispositivo e nel software dell’iniziatore iSCSI nell'host.</span><span class="sxs-lookup"><span data-stu-id="c6213-163">This requires the user to configure the CHAP initiator settings, as well as the reverse CHAP settings on the device and iSCSI Initiator software on the host.</span></span> <span data-ttu-id="c6213-164">Le procedure seguenti descrivono i passaggi per configurare l'autenticazione reciproca nel dispositivo e nell'host Windows.</span><span class="sxs-lookup"><span data-stu-id="c6213-164">The following procedures describe the steps to configure mutual authentication on the device and on the Windows host.</span></span>

#### <a name="to-configure-your-device-for-mutual-authentication"></a><span data-ttu-id="c6213-165">Per configurare il dispositivo per l'autenticazione reciproca</span><span class="sxs-lookup"><span data-stu-id="c6213-165">To configure your device for mutual authentication</span></span>
1. <span data-ttu-id="c6213-166">Nella pagina **Dispositivi** del portale di Azure classico fare clic su sulla scheda **Configura**.</span><span class="sxs-lookup"><span data-stu-id="c6213-166">In the Azure classic portal, on the **Devices** page, click the **Configure** tab.</span></span>
   
    ![Destinazione CHAP](./media/storsimple-configure-chap/IC740948.png)
2. <span data-ttu-id="c6213-168">Scorrere verso il basso in questa pagina e nella sezione **Destinazione CHAP** :</span><span class="sxs-lookup"><span data-stu-id="c6213-168">Scroll down on this page, and in the **CHAP Target** section:</span></span>
   
   1. <span data-ttu-id="c6213-169">Fornire un **nome utente per l’autenticazione CHAP inversa** per il dispositivo.</span><span class="sxs-lookup"><span data-stu-id="c6213-169">Provide a **Reverse CHAP user name** for your device.</span></span>
   2. <span data-ttu-id="c6213-170">Fornire una **password per l’autenticazione CHAP inversa** per il dispositivo.</span><span class="sxs-lookup"><span data-stu-id="c6213-170">Supply a **Reverse CHAP password** for your device.</span></span>
   3. <span data-ttu-id="c6213-171">Confermare la password.</span><span class="sxs-lookup"><span data-stu-id="c6213-171">Confirm the password.</span></span>
3. <span data-ttu-id="c6213-172">Nella sezione **Iniziatore CHAP** :</span><span class="sxs-lookup"><span data-stu-id="c6213-172">In the **CHAP Initiator** section:</span></span>
   
   1. <span data-ttu-id="c6213-173">Specificare un **nome utente** per il dispositivo.</span><span class="sxs-lookup"><span data-stu-id="c6213-173">Provide a **user name** for your device.</span></span>
   2. <span data-ttu-id="c6213-174">Specificare una **password** per il dispositivo.</span><span class="sxs-lookup"><span data-stu-id="c6213-174">Provide a **password** for your device.</span></span>
   3. <span data-ttu-id="c6213-175">Confermare la password.</span><span class="sxs-lookup"><span data-stu-id="c6213-175">Confirm the password.</span></span>
4. <span data-ttu-id="c6213-176">Fare clic su **Save**.</span><span class="sxs-lookup"><span data-stu-id="c6213-176">Click **Save**.</span></span> <span data-ttu-id="c6213-177">Verrà visualizzato un messaggio di conferma.</span><span class="sxs-lookup"><span data-stu-id="c6213-177">A confirmation message will be displayed.</span></span> <span data-ttu-id="c6213-178">Fare clic su **OK** per salvare le modifiche.</span><span class="sxs-lookup"><span data-stu-id="c6213-178">Click **OK** to save the changes.</span></span>

#### <a name="to-configure-bidirectional-authentication-on-the-windows-host-server"></a><span data-ttu-id="c6213-179">Per configurare l'autenticazione bidirezionale nel server host di Windows</span><span class="sxs-lookup"><span data-stu-id="c6213-179">To configure bidirectional authentication on the Windows host server</span></span>
1. <span data-ttu-id="c6213-180">Nel server host di Windows, avviare l'iniziatore iSCSI.</span><span class="sxs-lookup"><span data-stu-id="c6213-180">On the Windows host server, start the iSCSI Initiator.</span></span>
2. <span data-ttu-id="c6213-181">Nella finestra **iSCSI Initiator Properties** (Proprietà iniziatore iSCSI) scegliere la scheda **Configurazione**.</span><span class="sxs-lookup"><span data-stu-id="c6213-181">In the **iSCSI Initiator Properties** window, click the **Configuration** tab.</span></span>
3. <span data-ttu-id="c6213-182">Fare clic su **CHAP**.</span><span class="sxs-lookup"><span data-stu-id="c6213-182">Click **CHAP**.</span></span>
4. <span data-ttu-id="c6213-183">Nella finestra di dialogo **Segreto autenticazione CHAP reciproca iniziatore iSCSI** :</span><span class="sxs-lookup"><span data-stu-id="c6213-183">In the **iSCSI Initiator Mutual CHAP Secret** dialog box:</span></span>
   
   1. <span data-ttu-id="c6213-184">Immettere la **password dell'autenticazione CHAP inversa** configurata nel portale di Azure classico.</span><span class="sxs-lookup"><span data-stu-id="c6213-184">Type the **Reverse CHAP Password** that you configured in the Azure classic portal.</span></span>
   2. <span data-ttu-id="c6213-185">Fare clic su **OK**.</span><span class="sxs-lookup"><span data-stu-id="c6213-185">Click **OK**.</span></span>
      
       ![Segreto autenticazione CHAP reciproca iniziatore iSCSI](./media/storsimple-configure-chap/IC740949.png)
5. <span data-ttu-id="c6213-187">Fare clic sulla scheda **Destinazioni** .</span><span class="sxs-lookup"><span data-stu-id="c6213-187">Click the **Targets** tab.</span></span>
6. <span data-ttu-id="c6213-188">Scegliere il pulsante **Connetti** .</span><span class="sxs-lookup"><span data-stu-id="c6213-188">Click the **Connect** button.</span></span> 
7. <span data-ttu-id="c6213-189">Nella finestra di dialogo **Connessione alla destinazione** fare clic su **Avanzate**.</span><span class="sxs-lookup"><span data-stu-id="c6213-189">In the **Connect To Target** dialog box, click **Advanced**.</span></span>
8. <span data-ttu-id="c6213-190">Nella finestra di dialogo **Proprietà avanzate** :</span><span class="sxs-lookup"><span data-stu-id="c6213-190">In the **Advanced Properties** dialog box:</span></span>
   
   1. <span data-ttu-id="c6213-191">Selezionare la casella di controllo **Attiva accesso CHAP** .</span><span class="sxs-lookup"><span data-stu-id="c6213-191">Select the **Enable CHAP log on** check box.</span></span>
   2. <span data-ttu-id="c6213-192">Nel campo **Nome** , inserire il nome utente specificato per l'iniziatore CHAP nel portale classico.</span><span class="sxs-lookup"><span data-stu-id="c6213-192">In the **Name** field, supply the user name that you specified for the CHAP Initiator in the classic portal.</span></span>
   3. <span data-ttu-id="c6213-193">Nel campo **Segreto destinazione** , inserire la password specificata per l'iniziatore CHAP nel portale classico.</span><span class="sxs-lookup"><span data-stu-id="c6213-193">In the **Target secret** field, supply the password that you specified for the CHAP Initiator in the classic portal.</span></span>
   4. <span data-ttu-id="c6213-194">Selezionare la casella di controllo **Esegui autenticazione reciproca** .</span><span class="sxs-lookup"><span data-stu-id="c6213-194">Select the **Perform mutual authentication** check box.</span></span>
      
       ![Impostazioni avanzate - Autenticazione reciproca](./media/storsimple-configure-chap/IC740950.png)
   5. <span data-ttu-id="c6213-196">Fare clic su **OK** per completare la configurazione di CHAP.</span><span class="sxs-lookup"><span data-stu-id="c6213-196">Click **OK** to complete the CHAP configuration</span></span>

<span data-ttu-id="c6213-197">Per ulteriori informazioni sulla configurazione di CHAP nel server host di Windows, andare a [Ulteriori considerazioni](#additional-considerations).</span><span class="sxs-lookup"><span data-stu-id="c6213-197">For more information about configuring CHAP on the Windows host server, go to [Additional considerations](#additional-considerations).</span></span>

## <a name="additional-considerations"></a><span data-ttu-id="c6213-198">Ulteriori considerazioni</span><span class="sxs-lookup"><span data-stu-id="c6213-198">Additional considerations</span></span>
<span data-ttu-id="c6213-199">La funzionalità **Connessione rapida** non supporta le connessioni con CHAP attivato.</span><span class="sxs-lookup"><span data-stu-id="c6213-199">The **Quick Connect** feature does not support connections that have CHAP enabled.</span></span> <span data-ttu-id="c6213-200">Quando CHAP è abilitato, assicurarsi di usare il pulsante **Connetti** disponibile nella scheda **Destinazioni** per la connessione a una destinazione.</span><span class="sxs-lookup"><span data-stu-id="c6213-200">When CHAP is enabled, make sure that you use the **Connect** button that is available on the **Targets** tab to connect to a target.</span></span>

![Connessione a destinazione](./media/storsimple-configure-chap/IC740947.png)

<span data-ttu-id="c6213-202">Nella finestra di dialogo **Connessione alla destinazione** che viene visualizzata selezionare la casella di controllo **Aggiungi connessione all'elenco Destinazioni preferite**.</span><span class="sxs-lookup"><span data-stu-id="c6213-202">In the **Connect to Target** dialog box that is presented, select the **Add this connection to the list of Favorite Targets** check box.</span></span> <span data-ttu-id="c6213-203">Ciò garantisce che ogni volta che il computer viene riavviato, viene effettuato un tentativo di ripristinare la connessione alle destinazioni preferite iSCSI.</span><span class="sxs-lookup"><span data-stu-id="c6213-203">This ensures that every time the computer restarts, an attempt is made to restore the connection to the iSCSI favorite targets.</span></span>

## <a name="errors-during-configuration"></a><span data-ttu-id="c6213-204">Errori durante la configurazione</span><span class="sxs-lookup"><span data-stu-id="c6213-204">Errors during configuration</span></span>
<span data-ttu-id="c6213-205">Se la configurazione di CHAP non è corretta, è probabile che venga visualizzato un messaggio di errore **Errore di autenticazione** .</span><span class="sxs-lookup"><span data-stu-id="c6213-205">If your CHAP configuration is incorrect, then you are likely to see an **Authentication failure** error message.</span></span>

## <a name="verification-of-chap-configuration"></a><span data-ttu-id="c6213-206">Verifica della configurazione di CHAP</span><span class="sxs-lookup"><span data-stu-id="c6213-206">Verification of CHAP configuration</span></span>
<span data-ttu-id="c6213-207">È possibile verificare che CHAP sia in uso completando i passaggi seguenti.</span><span class="sxs-lookup"><span data-stu-id="c6213-207">You can verify that CHAP is being used by completing the following steps.</span></span>

#### <a name="to-verify-your-chap-configuration"></a><span data-ttu-id="c6213-208">Per verificare la configurazione di CHAP</span><span class="sxs-lookup"><span data-stu-id="c6213-208">To verify your CHAP configuration</span></span>
1. <span data-ttu-id="c6213-209">Fare clic su **Destinazioni preferite**.</span><span class="sxs-lookup"><span data-stu-id="c6213-209">Click **Favorite Targets**.</span></span>
2. <span data-ttu-id="c6213-210">Selezionare la destinazione per cui è abilitata l'autenticazione.</span><span class="sxs-lookup"><span data-stu-id="c6213-210">Select the target for which you enabled authentication.</span></span>
3. <span data-ttu-id="c6213-211">Fare clic su **Dettagli**.</span><span class="sxs-lookup"><span data-stu-id="c6213-211">Click **Details**.</span></span>
   
    ![Proprietà iniziatore iSCSI - Destinazioni preferite](./media/storsimple-configure-chap/IC740951.png)
4. <span data-ttu-id="c6213-213">Nella finestra di dialogo **Dettagli destinazione preferita** prendere nota della voce nel campo **Autenticazione**.</span><span class="sxs-lookup"><span data-stu-id="c6213-213">In the **Favorite Target Details** dialog box, note the entry in the **Authentication** field.</span></span> <span data-ttu-id="c6213-214">Se la configurazione è corretta, il campo contiene la voce **CHAP**.</span><span class="sxs-lookup"><span data-stu-id="c6213-214">If the configuration was successful, it should say **CHAP**.</span></span>
   
    ![Dettagli destinazione preferita](./media/storsimple-configure-chap/IC740952.png)

## <a name="next-steps"></a><span data-ttu-id="c6213-216">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="c6213-216">Next steps</span></span>
* <span data-ttu-id="c6213-217">Ulteriori informazioni sulla [sicurezza di StorSimple](storsimple-security.md).</span><span class="sxs-lookup"><span data-stu-id="c6213-217">Learn more about [StorSimple security](storsimple-security.md).</span></span>
* <span data-ttu-id="c6213-218">Ulteriori informazioni sull’ [utilizzo del servizio StorSimple Manager per amministrare il dispositivo StorSimple](storsimple-manager-service-administration.md).</span><span class="sxs-lookup"><span data-stu-id="c6213-218">Learn more about [using the StorSimple Manager service to administer your StorSimple device](storsimple-manager-service-administration.md).</span></span>


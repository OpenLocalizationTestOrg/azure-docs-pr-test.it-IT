---
title: aaaConnect in remoto il dispositivo di StorSimple tooyour | Documenti Microsoft
description: Viene illustrato come tooconfigure il dispositivo per la gestione remota e come tooconnect tooWindows PowerShell per StorSimple tramite HTTP o HTTPS.
services: storsimple
documentationcenter: 
author: alkohli
manager: timlt
editor: 
ms.assetid: 923377aa-f451-4656-87de-5e95a34a6a2a
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 02/27/2017
ms.author: alkohli
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 55ed8fcdd997901301e0adc164a302216cde0332
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="connect-remotely-tooyour-storsimple-8000-series-device"></a><span data-ttu-id="690e1-103">Connettersi in remoto il dispositivo di serie StorSimple 8000 tooyour</span><span class="sxs-lookup"><span data-stu-id="690e1-103">Connect remotely tooyour StorSimple 8000 series device</span></span>

## <a name="overview"></a><span data-ttu-id="690e1-104">Panoramica</span><span class="sxs-lookup"><span data-stu-id="690e1-104">Overview</span></span>
<span data-ttu-id="690e1-105">È possibile utilizzare il dispositivo StorSimple tooyour di Windows PowerShell remoting tooconnect.</span><span class="sxs-lookup"><span data-stu-id="690e1-105">You can use Windows PowerShell remoting tooconnect tooyour StorSimple device.</span></span> <span data-ttu-id="690e1-106">Quando ci si connette in questo modo, non verrà visualizzato un menu.</span><span class="sxs-lookup"><span data-stu-id="690e1-106">When you connect this way, you will not see a menu.</span></span> <span data-ttu-id="690e1-107">(Verrà visualizzato un menu solo se si utilizza la console seriale hello in hello dispositivo tooconnect). Con la comunicazione remota di Windows PowerShell, è connettersi tooa spazio di esecuzione specifico.</span><span class="sxs-lookup"><span data-stu-id="690e1-107">(You see a menu only if you use hello serial console on hello device tooconnect.) With Windows PowerShell remoting, you connect tooa specific runspace.</span></span> <span data-ttu-id="690e1-108">È inoltre possibile specificare la lingua di visualizzazione hello.</span><span class="sxs-lookup"><span data-stu-id="690e1-108">You can also specify hello display language.</span></span> 

<span data-ttu-id="690e1-109">Per ulteriori informazioni sull'utilizzo toomanage di comunicazione remota di Windows PowerShell del dispositivo, andare troppo[utilizzare Windows PowerShell per StorSimple tooadminister dispositivo StorSimple](storsimple-windows-powershell-administration.md).</span><span class="sxs-lookup"><span data-stu-id="690e1-109">For more information about using Windows PowerShell remoting toomanage your device, go too[Use Windows PowerShell for StorSimple tooadminister your StorSimple device](storsimple-windows-powershell-administration.md).</span></span>

<span data-ttu-id="690e1-110">In questa esercitazione viene illustrato come tooconfigure del dispositivo per la gestione remota e come quindi tooconnect tooWindows PowerShell per StorSimple.</span><span class="sxs-lookup"><span data-stu-id="690e1-110">This tutorial explains how tooconfigure your device for remote management and then how tooconnect tooWindows PowerShell for StorSimple.</span></span> <span data-ttu-id="690e1-111">È possibile utilizzare HTTP o HTTPS tooconnect tramite comunicazione remota di Windows PowerShell.</span><span class="sxs-lookup"><span data-stu-id="690e1-111">You can use HTTP or HTTPS tooconnect via Windows PowerShell remoting.</span></span> <span data-ttu-id="690e1-112">Tuttavia, quando si decide come tooconnect tooWindows PowerShell per StorSimple, considerare l'esempio hello:</span><span class="sxs-lookup"><span data-stu-id="690e1-112">However, when you are deciding how tooconnect tooWindows PowerShell for StorSimple, consider hello following:</span></span> 

* <span data-ttu-id="690e1-113">La connessione diretta toohello console seriale del dispositivo è protetto, ma connessione toohello console seriale tramite commutatori di rete non è.</span><span class="sxs-lookup"><span data-stu-id="690e1-113">Connecting directly toohello device serial console is secure, but connecting toohello serial console over network switches is not.</span></span> <span data-ttu-id="690e1-114">Prestare attenzione hello rischi di sicurezza durante la connessione toohello console seriale del dispositivo tramite commutatori di rete.</span><span class="sxs-lookup"><span data-stu-id="690e1-114">Be cautious of hello security risk when connecting toohello device serial console over network switches.</span></span> 
* <span data-ttu-id="690e1-115">Connessione tramite una sessione HTTP può offrire maggiore sicurezza rispetto alla connessione tramite la console seriale hello su hello.</span><span class="sxs-lookup"><span data-stu-id="690e1-115">Connecting through an HTTP session might offer more security than connecting through hello serial console over hello network.</span></span> <span data-ttu-id="690e1-116">Anche se non si tratta metodo più sicuro hello, è accettabile su reti attendibili.</span><span class="sxs-lookup"><span data-stu-id="690e1-116">Although this is not hello most secure method, it is acceptable on trusted networks.</span></span> 
* <span data-ttu-id="690e1-117">Connessione tramite una sessione HTTPS con un certificato autofirmato è hello più sicura e hello opzione consigliata.</span><span class="sxs-lookup"><span data-stu-id="690e1-117">Connecting through an HTTPS session with a self-signed certificate is hello most secure and hello recommended option.</span></span>

<span data-ttu-id="690e1-118">È possibile connettersi in remoto toohello interfaccia di Windows PowerShell.</span><span class="sxs-lookup"><span data-stu-id="690e1-118">You can connect remotely toohello Windows PowerShell interface.</span></span> <span data-ttu-id="690e1-119">Dispositivo StorSimple tooyour di accesso remoto tramite l'interfaccia di Windows PowerShell hello, tuttavia, non è abilitato per impostazione predefinita.</span><span class="sxs-lookup"><span data-stu-id="690e1-119">However, remote access tooyour StorSimple device via hello Windows PowerShell interface is not enabled by default.</span></span> <span data-ttu-id="690e1-120">Necessario tooenable gestione remota sul dispositivo hello prima e quindi su hello client tooaccess usato il dispositivo.</span><span class="sxs-lookup"><span data-stu-id="690e1-120">You need tooenable remote management on hello device first, and then on hello client that is used tooaccess your device.</span></span>

<span data-ttu-id="690e1-121">passaggi di Hello descritti in questo articolo sono stati eseguiti in un sistema host che esegue Windows Server 2012 R2.</span><span class="sxs-lookup"><span data-stu-id="690e1-121">hello steps described in this article were performed on a host system running Windows Server 2012 R2.</span></span>

## <a name="connect-through-http"></a><span data-ttu-id="690e1-122">Connessione tramite HTTP</span><span class="sxs-lookup"><span data-stu-id="690e1-122">Connect through HTTP</span></span>
<span data-ttu-id="690e1-123">La connessione tooWindows PowerShell per StorSimple tramite una sessione HTTP offre maggiore sicurezza rispetto alla connessione tramite hello console seriale del dispositivo StorSimple.</span><span class="sxs-lookup"><span data-stu-id="690e1-123">Connecting tooWindows PowerShell for StorSimple through an HTTP session offers more security than connecting through hello serial console of your StorSimple device.</span></span> <span data-ttu-id="690e1-124">Anche se non si tratta metodo più sicuro hello, è accettabile su reti attendibili.</span><span class="sxs-lookup"><span data-stu-id="690e1-124">Although this is not hello most secure method, it is acceptable on trusted networks.</span></span>

<span data-ttu-id="690e1-125">È possibile utilizzare hello portale di Azure classico o la gestione remota di hello console seriale tooconfigure.</span><span class="sxs-lookup"><span data-stu-id="690e1-125">You can use either hello Azure classic portal or hello serial console tooconfigure remote management.</span></span> <span data-ttu-id="690e1-126">Selezionare hello seguire le procedure seguenti:</span><span class="sxs-lookup"><span data-stu-id="690e1-126">Select from hello following procedures:</span></span>

* [<span data-ttu-id="690e1-127">Usare la gestione remota di hello Azure tooenable portale classico su HTTP</span><span class="sxs-lookup"><span data-stu-id="690e1-127">Use hello Azure classic portal tooenable remote management over HTTP</span></span>](#use-the-azure-classic-portal-to-enable-remote-management-over-http)
* [<span data-ttu-id="690e1-128">Usare la gestione remota di hello console seriale tooenable su HTTP</span><span class="sxs-lookup"><span data-stu-id="690e1-128">Use hello serial console tooenable remote management over HTTP</span></span>](#use-the-serial-console-to-enable-remote-management-over-http)

<span data-ttu-id="690e1-129">Dopo aver abilitato la gestione remota, utilizzare hello seguenti client di hello tooprepare procedure per una connessione remota.</span><span class="sxs-lookup"><span data-stu-id="690e1-129">After you enable remote management, use hello following procedure tooprepare hello client for a remote connection.</span></span>

* [<span data-ttu-id="690e1-130">Preparare il client di hello per la connessione remota</span><span class="sxs-lookup"><span data-stu-id="690e1-130">Prepare hello client for remote connection</span></span>](#prepare-the-client-for-remote-connection)

### <a name="use-hello-azure-classic-portal-tooenable-remote-management-over-http"></a><span data-ttu-id="690e1-131">Usare la gestione remota di hello Azure tooenable portale classico su HTTP</span><span class="sxs-lookup"><span data-stu-id="690e1-131">Use hello Azure classic portal tooenable remote management over HTTP</span></span>
<span data-ttu-id="690e1-132">Eseguire hello seguendo i passaggi nella gestione remota di hello Azure tooenable portale classico tramite HTTP.</span><span class="sxs-lookup"><span data-stu-id="690e1-132">Perform hello following steps in hello Azure classic portal tooenable remote management over HTTP.</span></span>

#### <a name="tooenable-remote-management-through-hello-azure-classic-portal"></a><span data-ttu-id="690e1-133">gestione remota di tooenable tramite hello portale di Azure classico</span><span class="sxs-lookup"><span data-stu-id="690e1-133">tooenable remote management through hello Azure classic portal</span></span>
1. <span data-ttu-id="690e1-134">Accedere a **Dispositivi** > **Configura** per il dispositivo.</span><span class="sxs-lookup"><span data-stu-id="690e1-134">Access **Devices** > **Configure** for your device.</span></span>
2. <span data-ttu-id="690e1-135">Scorrere verso il basso toohello **gestione remota** sezione.</span><span class="sxs-lookup"><span data-stu-id="690e1-135">Scroll down toohello **Remote Management** section.</span></span>
3. <span data-ttu-id="690e1-136">Impostare **abilitare gestione remota** troppo**Sì**.</span><span class="sxs-lookup"><span data-stu-id="690e1-136">Set **Enable Remote Management** too**Yes**.</span></span>
4. <span data-ttu-id="690e1-137">È ora possibile scegliere tooconnect tramite HTTP.</span><span class="sxs-lookup"><span data-stu-id="690e1-137">You can now choose tooconnect using HTTP.</span></span> <span data-ttu-id="690e1-138">(valore predefinito di hello è tooconnect su HTTPS). Assicurarsi che HTTP sia selezionato.</span><span class="sxs-lookup"><span data-stu-id="690e1-138">(hello default is tooconnect over HTTPS.) Make sure that HTTP is selected.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="690e1-139">La connessione tramite HTTP dovrebbe essere eseguita solo su reti attendibili.</span><span class="sxs-lookup"><span data-stu-id="690e1-139">Connecting over HTTP is acceptable only on trusted networks.</span></span>
   > 
   > 
5. <span data-ttu-id="690e1-140">Fare clic su **salvare** nella parte inferiore di hello della pagina hello.</span><span class="sxs-lookup"><span data-stu-id="690e1-140">Click **Save** at hello bottom of hello page.</span></span>

### <a name="use-hello-serial-console-tooenable-remote-management-over-http"></a><span data-ttu-id="690e1-141">Usare la gestione remota di hello console seriale tooenable su HTTP</span><span class="sxs-lookup"><span data-stu-id="690e1-141">Use hello serial console tooenable remote management over HTTP</span></span>
<span data-ttu-id="690e1-142">Eseguire hello seguendo i passaggi per la gestione remota tooenable hello dispositivo console seriale.</span><span class="sxs-lookup"><span data-stu-id="690e1-142">Perform hello following steps on hello device serial console tooenable remote management.</span></span>

#### <a name="tooenable-remote-management-through-hello-device-serial-console"></a><span data-ttu-id="690e1-143">gestione remota tramite console seriale del dispositivo hello tooenable</span><span class="sxs-lookup"><span data-stu-id="690e1-143">tooenable remote management through hello device serial console</span></span>
1. <span data-ttu-id="690e1-144">Nel menu della console seriale hello, selezionare l'opzione 1.</span><span class="sxs-lookup"><span data-stu-id="690e1-144">On hello serial console menu, select option 1.</span></span> <span data-ttu-id="690e1-145">Per ulteriori informazioni sull'utilizzo della console seriale hello sul dispositivo hello, andare troppo[connessione tooWindows PowerShell per StorSimple tramite console seriale del dispositivo](storsimple-windows-powershell-administration.md#connect-to-windows-powershell-for-storsimple-via-the-device-serial-console).</span><span class="sxs-lookup"><span data-stu-id="690e1-145">For more information about using hello serial console on hello device, go too[Connect tooWindows PowerShell for StorSimple via device serial console](storsimple-windows-powershell-administration.md#connect-to-windows-powershell-for-storsimple-via-the-device-serial-console).</span></span>
2. <span data-ttu-id="690e1-146">Al prompt dei comandi hello, digitare:`Enable-HcsRemoteManagement –AllowHttp`</span><span class="sxs-lookup"><span data-stu-id="690e1-146">At hello prompt, type: `Enable-HcsRemoteManagement –AllowHttp`</span></span>
3. <span data-ttu-id="690e1-147">Si riceverà la notifica sulle vulnerabilità della sicurezza hello di utilizzo di HTTP tooconnect toohello dispositivo.</span><span class="sxs-lookup"><span data-stu-id="690e1-147">You will be notified about hello security vulnerabilities of using HTTP tooconnect toohello device.</span></span> <span data-ttu-id="690e1-148">Quando richiesto, confermare digitando **Y**.</span><span class="sxs-lookup"><span data-stu-id="690e1-148">When prompted, confirm by typing **Y**.</span></span>
4. <span data-ttu-id="690e1-149">Verificare che HTTP sia abilitato digitando: `Get-HcsSystem`</span><span class="sxs-lookup"><span data-stu-id="690e1-149">Verify that HTTP is enabled by typing: `Get-HcsSystem`</span></span>
5. <span data-ttu-id="690e1-150">Verificare che hello **RemoteManagementMode** campo **HttpsAndHttpEnabled**.hello seguente figura illustra queste impostazioni in PuTTY.</span><span class="sxs-lookup"><span data-stu-id="690e1-150">Verify that hello **RemoteManagementMode** field shows **HttpsAndHttpEnabled**.hello following illustration shows these settings in PuTTY.</span></span>
   
     ![Seriali HTTPS e HTTP abilitati](./media/storsimple-remote-connect/HCS_SerialHttpsAndHttpEnabled.png)

### <a name="prepare-hello-client-for-remote-connection"></a><span data-ttu-id="690e1-152">Preparare il client di hello per la connessione remota</span><span class="sxs-lookup"><span data-stu-id="690e1-152">Prepare hello client for remote connection</span></span>
<span data-ttu-id="690e1-153">Eseguire hello seguendo i passaggi per la gestione remota di hello client tooenable.</span><span class="sxs-lookup"><span data-stu-id="690e1-153">Perform hello following steps on hello client tooenable remote management.</span></span>

#### <a name="tooprepare-hello-client-for-remote-connection"></a><span data-ttu-id="690e1-154">client hello tooprepare per la connessione remota</span><span class="sxs-lookup"><span data-stu-id="690e1-154">tooprepare hello client for remote connection</span></span>
1. <span data-ttu-id="690e1-155">Avviare una sessione di Windows PowerShell come amministratore.</span><span class="sxs-lookup"><span data-stu-id="690e1-155">Start a Windows PowerShell session as an administrator.</span></span>
2. <span data-ttu-id="690e1-156">Indirizzo IP di hello tooadd dell'elenco di host attendibili del client di hello StorSimple dispositivo toohello dei comandi digitare quanto segue di hello:</span><span class="sxs-lookup"><span data-stu-id="690e1-156">Type hello following command tooadd hello IP address of hello StorSimple device toohello client’s trusted hosts list:</span></span> 
   
     `Set-Item wsman:\localhost\Client\TrustedHosts <device_ip> -Concatenate -Force`
   
     <span data-ttu-id="690e1-157">Sostituire <*device_ip*> con l'indirizzo IP di hello del dispositivo, ad esempio:</span><span class="sxs-lookup"><span data-stu-id="690e1-157">Replace <*device_ip*> with hello IP address of your device; for example:</span></span> 
   
     `Set-Item wsman:\localhost\Client\TrustedHosts 10.126.173.90 -Concatenate -Force`
3. <span data-ttu-id="690e1-158">Credenziali del dispositivo toosave hello in una variabile di comando che segue hello di tipo:</span><span class="sxs-lookup"><span data-stu-id="690e1-158">Type hello following command toosave hello device credentials in a variable:</span></span> 
   
    ```
    $cred = Get-Credential
    ```
    
4. <span data-ttu-id="690e1-159">Nella finestra di dialogo hello che viene visualizzata:</span><span class="sxs-lookup"><span data-stu-id="690e1-159">In hello dialog box that appears:</span></span>
   
   1. <span data-ttu-id="690e1-160">Digitare il nome utente hello in questo formato: *device_ip\SSAdmin*.</span><span class="sxs-lookup"><span data-stu-id="690e1-160">Type hello user name in this format: *device_ip\SSAdmin*.</span></span>
   2. <span data-ttu-id="690e1-161">Tipo hello password amministratore del dispositivo che è stata impostata quando il dispositivo di hello è stato configurato con l'installazione guidata di hello.</span><span class="sxs-lookup"><span data-stu-id="690e1-161">Type hello device administrator password that was set when hello device was configured with hello setup wizard.</span></span> <span data-ttu-id="690e1-162">password predefinita Hello è *Password1*.</span><span class="sxs-lookup"><span data-stu-id="690e1-162">hello default password is *Password1*.</span></span>
5. <span data-ttu-id="690e1-163">Avviare una sessione di Windows PowerShell nel dispositivo hello digitando questo comando:</span><span class="sxs-lookup"><span data-stu-id="690e1-163">Start a Windows PowerShell session on hello device by typing this command:</span></span>
   
     `Enter-PSSession -Credential $cred -ConfigurationName SSAdminConsole -ComputerName <device_ip>`
   
   > [!NOTE]
   > <span data-ttu-id="690e1-164">toocreate una sessione di Windows PowerShell per l'utilizzo con dispositivo virtuale StorSimple hello, accodare hello `–Port` parametro e specificare la porta pubblica hello configurati in servizi remoti per il dispositivo virtuale StorSimple.</span><span class="sxs-lookup"><span data-stu-id="690e1-164">toocreate a Windows PowerShell session for use with hello StorSimple virtual device, append hello `–Port` parameter and specify hello public port that you configured in Remoting for StorSimple Virtual Appliance.</span></span>
   > 
   > 
   
     <span data-ttu-id="690e1-165">A questo punto, è necessario disporre di un dispositivo di toohello attivo di remoto Windows PowerShell sessione.</span><span class="sxs-lookup"><span data-stu-id="690e1-165">At this point, you should have an active remote Windows PowerShell session toohello device.</span></span>
   
    ![Comunicazione remota PowerShell tramite HTTP](./media/storsimple-remote-connect/HCS_PSRemotingUsingHTTP.png)

## <a name="connect-through-https"></a><span data-ttu-id="690e1-167">Connessione tramite HTTPS</span><span class="sxs-lookup"><span data-stu-id="690e1-167">Connect through HTTPS</span></span>
<span data-ttu-id="690e1-168">Connessione tooWindows PowerShell per StorSimple tramite una sessione HTTPS, è più sicuro hello e metodo di connessione in remoto i dispositivi di Microsoft Azure StorSimple tooyour consigliato.</span><span class="sxs-lookup"><span data-stu-id="690e1-168">Connecting tooWindows PowerShell for StorSimple through an HTTPS session is hello most secure and recommended method of remotely connecting tooyour Microsoft Azure StorSimple device.</span></span> <span data-ttu-id="690e1-169">Hello, seguire le procedure seguenti spiegano come tooset backup hello seriali console e i computer client in modo che è possibile utilizzare HTTPS tooconnect tooWindows PowerShell per StorSimple.</span><span class="sxs-lookup"><span data-stu-id="690e1-169">hello following procedures explain how tooset up hello serial console and client computers so that you can use HTTPS tooconnect tooWindows PowerShell for StorSimple.</span></span>

<span data-ttu-id="690e1-170">È possibile utilizzare hello portale di Azure classico o la gestione remota di hello console seriale tooconfigure.</span><span class="sxs-lookup"><span data-stu-id="690e1-170">You can use either hello Azure classic portal or hello serial console tooconfigure remote management.</span></span> <span data-ttu-id="690e1-171">Selezionare hello seguire le procedure seguenti:</span><span class="sxs-lookup"><span data-stu-id="690e1-171">Select from hello following procedures:</span></span>

* [<span data-ttu-id="690e1-172">Utilizzare la gestione remota di hello Azure tooenable portale classico su HTTPS</span><span class="sxs-lookup"><span data-stu-id="690e1-172">Use hello Azure classic portal tooenable remote management over HTTPS</span></span>](#use-the-azure-classic-portal-to-enable-remote-management-over-https)
* [<span data-ttu-id="690e1-173">Utilizzare la gestione remota di hello console seriale tooenable su HTTPS</span><span class="sxs-lookup"><span data-stu-id="690e1-173">Use hello serial console tooenable remote management over HTTPS</span></span>](#use-the-serial-console-to-enable-remote-management-over-https)

<span data-ttu-id="690e1-174">Dopo aver abilitato la gestione remota, utilizzare hello seguenti host hello tooprepare di procedure per la gestione remota e connettere il dispositivo toohello dall'host remoto hello.</span><span class="sxs-lookup"><span data-stu-id="690e1-174">After you enable remote management, use hello following procedures tooprepare hello host for a remote management and connect toohello device from hello remote host.</span></span>

* [<span data-ttu-id="690e1-175">Preparare l'host di hello per la gestione remota</span><span class="sxs-lookup"><span data-stu-id="690e1-175">Prepare hello host for remote management</span></span>](#prepare-the-host-for-remote-management)
* [<span data-ttu-id="690e1-176">Connettere il dispositivo di toohello dall'host remoto hello</span><span class="sxs-lookup"><span data-stu-id="690e1-176">Connect toohello device from hello remote host</span></span>](#connect-to-the-device-from-the-remote-host)

### <a name="use-hello-azure-classic-portal-tooenable-remote-management-over-https"></a><span data-ttu-id="690e1-177">Utilizzare la gestione remota di hello Azure tooenable portale classico su HTTPS</span><span class="sxs-lookup"><span data-stu-id="690e1-177">Use hello Azure classic portal tooenable remote management over HTTPS</span></span>
<span data-ttu-id="690e1-178">Eseguire hello seguendo i passaggi nella gestione remota di hello Azure tooenable portale classico tramite HTTPS.</span><span class="sxs-lookup"><span data-stu-id="690e1-178">Perform hello following steps in hello Azure classic portal tooenable remote management over HTTPS.</span></span>

#### <a name="tooenable-remote-management-over-https-from-hello-azure-classic-portal"></a><span data-ttu-id="690e1-179">gestione remota su HTTPS tooenable dal portale di Azure classico hello</span><span class="sxs-lookup"><span data-stu-id="690e1-179">tooenable remote management over HTTPS from hello Azure classic portal</span></span>
1. <span data-ttu-id="690e1-180">Accedere a **Dispositivi** > **Configura** per il dispositivo.</span><span class="sxs-lookup"><span data-stu-id="690e1-180">Access **Devices** > **Configure** for your device.</span></span>
2. <span data-ttu-id="690e1-181">Scorrere verso il basso toohello **gestione remota** sezione.</span><span class="sxs-lookup"><span data-stu-id="690e1-181">Scroll down toohello **Remote Management** section.</span></span>
3. <span data-ttu-id="690e1-182">Impostare **abilitare gestione remota** troppo**Sì**.</span><span class="sxs-lookup"><span data-stu-id="690e1-182">Set **Enable Remote Management** too**Yes**.</span></span>
4. <span data-ttu-id="690e1-183">È ora possibile scegliere tooconnect tramite HTTPS.</span><span class="sxs-lookup"><span data-stu-id="690e1-183">You can now choose tooconnect using HTTPS.</span></span> <span data-ttu-id="690e1-184">(valore predefinito di hello è tooconnect su HTTPS). Assicurarsi che HTTPS sia selezionato.</span><span class="sxs-lookup"><span data-stu-id="690e1-184">(hello default is tooconnect over HTTPS.) Make sure that HTTPS is selected.</span></span> 
5. <span data-ttu-id="690e1-185">Fare clic su **Scarica certificato di gestione remota**.</span><span class="sxs-lookup"><span data-stu-id="690e1-185">Click **Download Remote Management Certificate**.</span></span> <span data-ttu-id="690e1-186">Specificare un percorso toosave questo file.</span><span class="sxs-lookup"><span data-stu-id="690e1-186">Specify a location toosave this file.</span></span> <span data-ttu-id="690e1-187">È necessario tooinstall questo certificato nel computer client o host hello che si utilizzerà tooconnect toohello dispositivo.</span><span class="sxs-lookup"><span data-stu-id="690e1-187">You will need tooinstall this certificate on hello client or host computer that you will use tooconnect toohello device.</span></span>
6. <span data-ttu-id="690e1-188">Fare clic su **salvare** nella parte inferiore di hello della pagina hello.</span><span class="sxs-lookup"><span data-stu-id="690e1-188">Click **Save** at hello bottom of hello page.</span></span>

### <a name="use-hello-serial-console-tooenable-remote-management-over-https"></a><span data-ttu-id="690e1-189">Utilizzare la gestione remota di hello console seriale tooenable su HTTPS</span><span class="sxs-lookup"><span data-stu-id="690e1-189">Use hello serial console tooenable remote management over HTTPS</span></span>
<span data-ttu-id="690e1-190">Eseguire hello seguendo i passaggi per la gestione remota tooenable hello dispositivo console seriale.</span><span class="sxs-lookup"><span data-stu-id="690e1-190">Perform hello following steps on hello device serial console tooenable remote management.</span></span>

#### <a name="tooenable-remote-management-through-hello-device-serial-console"></a><span data-ttu-id="690e1-191">gestione remota tramite console seriale del dispositivo hello tooenable</span><span class="sxs-lookup"><span data-stu-id="690e1-191">tooenable remote management through hello device serial console</span></span>
1. <span data-ttu-id="690e1-192">Nel menu della console seriale hello, selezionare l'opzione 1.</span><span class="sxs-lookup"><span data-stu-id="690e1-192">On hello serial console menu, select option 1.</span></span> <span data-ttu-id="690e1-193">Per ulteriori informazioni sull'utilizzo della console seriale hello sul dispositivo hello, andare troppo[connessione tooWindows PowerShell per StorSimple tramite console seriale del dispositivo](storsimple-windows-powershell-administration.md#connect-to-windows-powershell-for-storsimple-via-the-device-serial-console).</span><span class="sxs-lookup"><span data-stu-id="690e1-193">For more information about using hello serial console on hello device, go too[Connect tooWindows PowerShell for StorSimple via device serial console](storsimple-windows-powershell-administration.md#connect-to-windows-powershell-for-storsimple-via-the-device-serial-console).</span></span>
2. <span data-ttu-id="690e1-194">Al prompt dei comandi hello, digitare:</span><span class="sxs-lookup"><span data-stu-id="690e1-194">At hello prompt, type:</span></span> 
   
     `Enable-HcsRemoteManagement`
   
    <span data-ttu-id="690e1-195">Ciò dovrebbe abilitare HTTPS sul dispositivo.</span><span class="sxs-lookup"><span data-stu-id="690e1-195">This should enable HTTPS on your device.</span></span>
3. <span data-ttu-id="690e1-196">Verificare che HTTPS sia abilitato digitando:</span><span class="sxs-lookup"><span data-stu-id="690e1-196">Verify that HTTPS has been enabled by typing:</span></span> 
   
     `Get-HcsSystem`
   
    <span data-ttu-id="690e1-197">Verificare che tale hello **RemoteManagementMode** campo **HttpsEnabled**.hello seguente figura illustra queste impostazioni in PuTTY.</span><span class="sxs-lookup"><span data-stu-id="690e1-197">Make sure that hello **RemoteManagementMode** field shows **HttpsEnabled**.hello following illustration shows these settings in PuTTY.</span></span>
   
     ![Seriale HTTPS abilitato](./media/storsimple-remote-connect/HCS_SerialHttpsEnabled.png)
4. <span data-ttu-id="690e1-199">Output di hello del `Get-HcsSystem`, copiare hello numero di serie del dispositivo hello e salvarlo per un uso successivo.</span><span class="sxs-lookup"><span data-stu-id="690e1-199">From hello output of `Get-HcsSystem`, copy hello serial number of hello device and save it for later use.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="690e1-200">numero di serie Hello esegue il mapping nome CN toohello nel certificato hello.</span><span class="sxs-lookup"><span data-stu-id="690e1-200">hello serial number maps toohello CN name in hello certificate.</span></span>
   > 
   > 
5. <span data-ttu-id="690e1-201">Ottenere un certificato di gestione remota digitando:</span><span class="sxs-lookup"><span data-stu-id="690e1-201">Obtain a remote management certificate by typing:</span></span> 
   
     `Get-HcsRemoteManagementCert`
   
    <span data-ttu-id="690e1-202">Verrà visualizzato un seguente toohello simile certificato.</span><span class="sxs-lookup"><span data-stu-id="690e1-202">A certificate similar toohello following will appear.</span></span>
   
    ![Ottenimento del certificato di gestione remota](./media/storsimple-remote-connect/HCS_GetRemoteManagementCertificate.png)
6. <span data-ttu-id="690e1-204">Copiare le informazioni di hello certificato hello da **---BEGIN CERTIFICATE---** troppo**---END CERTIFICATE---** in un editor di testo quale Blocco note e salvarlo come file con estensione cer.</span><span class="sxs-lookup"><span data-stu-id="690e1-204">Copy hello information in hello certificate from **-----BEGIN CERTIFICATE-----** too**-----END CERTIFICATE-----** into a text editor such as Notepad, and save it as a .cer file.</span></span> <span data-ttu-id="690e1-205">(Verrà copiato l'host remoto tooyour di file quando si prepara l'host di hello.)</span><span class="sxs-lookup"><span data-stu-id="690e1-205">(You will copy this file tooyour remote host when you prepare hello host.)</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="690e1-206">toogenerate un nuovo certificato, utilizzare hello `Set-HcsRemoteManagementCert` cmdlet.</span><span class="sxs-lookup"><span data-stu-id="690e1-206">toogenerate a new certificate, use hello `Set-HcsRemoteManagementCert` cmdlet.</span></span>
   > 
   > 

### <a name="prepare-hello-host-for-remote-management"></a><span data-ttu-id="690e1-207">Preparare l'host di hello per la gestione remota</span><span class="sxs-lookup"><span data-stu-id="690e1-207">Prepare hello host for remote management</span></span>
<span data-ttu-id="690e1-208">computer host di hello tooprepare per una connessione remota che utilizza una sessione HTTPS, eseguire hello seguire le procedure seguenti:</span><span class="sxs-lookup"><span data-stu-id="690e1-208">tooprepare hello host computer for a remote connection that uses an HTTPS session, perform hello following procedures:</span></span>

* <span data-ttu-id="690e1-209">[File con estensione cer hello importazione nell'archivio radice hello del client hello o dell'host remoto](#to-import-the-certificate-on-the-remote-host).</span><span class="sxs-lookup"><span data-stu-id="690e1-209">[Import hello .cer file into hello root store of hello client or remote host](#to-import-the-certificate-on-the-remote-host).</span></span>
* <span data-ttu-id="690e1-210">[Aggiungere file hosts toohello hello dispositivo numeri di serie dell'host remoto](#to-add-device-serial-numbers-to-the-remote-host).</span><span class="sxs-lookup"><span data-stu-id="690e1-210">[Add hello device serial numbers toohello hosts file on your remote host](#to-add-device-serial-numbers-to-the-remote-host).</span></span>

<span data-ttu-id="690e1-211">Ognuna di queste procedure è descritta di seguito.</span><span class="sxs-lookup"><span data-stu-id="690e1-211">Each of these procedures is described below.</span></span>

#### <a name="tooimport-hello-certificate-on-hello-remote-host"></a><span data-ttu-id="690e1-212">certificato di hello tooimport nell'host remoto hello</span><span class="sxs-lookup"><span data-stu-id="690e1-212">tooimport hello certificate on hello remote host</span></span>
1. <span data-ttu-id="690e1-213">Fare clic sul file con estensione cer hello e selezionare **Installa certificato**.</span><span class="sxs-lookup"><span data-stu-id="690e1-213">Right-click hello .cer file and select **Install certificate**.</span></span> <span data-ttu-id="690e1-214">Verrà avviata hello importazione guidata certificati.</span><span class="sxs-lookup"><span data-stu-id="690e1-214">This will start hello Certificate Import Wizard.</span></span>
   
    ![Impostazione guidata del certificato 1](./media/storsimple-remote-connect/HCS_CertificateImportWizard1.png)
2. <span data-ttu-id="690e1-216">Per **Percorso archivio**, selezionare **Computer locale**, quindi fare clic su **Avanti**.</span><span class="sxs-lookup"><span data-stu-id="690e1-216">For **Store location**, select **Local Machine**, and then click **Next**.</span></span>
3. <span data-ttu-id="690e1-217">Selezionare **colloca tutti i certificati nel seguente archivio hello**, quindi fare clic su **Sfoglia**.</span><span class="sxs-lookup"><span data-stu-id="690e1-217">Select **Place all certificates in hello following store**, and then click **Browse**.</span></span> <span data-ttu-id="690e1-218">Passare l'archivio radice toohello dell'host remoto e quindi fare clic su **Avanti**.</span><span class="sxs-lookup"><span data-stu-id="690e1-218">Navigate toohello root store of your remote host, and then click **Next**.</span></span>
   
    ![Impostazione guidata del certificato 2](./media/storsimple-remote-connect/HCS_CertificateImportWizard2.png)
4. <span data-ttu-id="690e1-220">Fare clic su **Finish**.</span><span class="sxs-lookup"><span data-stu-id="690e1-220">Click **Finish**.</span></span> <span data-ttu-id="690e1-221">Viene visualizzato un messaggio che indica che l'importazione di hello ha esito positivo.</span><span class="sxs-lookup"><span data-stu-id="690e1-221">A message that tells you that hello import was successful appears.</span></span>
   
    ![Impostazione guidata del certificato 3](./media/storsimple-remote-connect/HCS_CertificateImportWizard3.png)

#### <a name="tooadd-device-serial-numbers-toohello-remote-host"></a><span data-ttu-id="690e1-223">host remoto toohello tooadd dispositivo numeri di serie</span><span class="sxs-lookup"><span data-stu-id="690e1-223">tooadd device serial numbers toohello remote host</span></span>
1. <span data-ttu-id="690e1-224">Avviare Blocco note come amministratore e quindi aprire file hosts hello in \WINDOWS\system32\drivers\etc..</span><span class="sxs-lookup"><span data-stu-id="690e1-224">Start Notepad as an administrator, and then open hello hosts file located at \Windows\System32\Drivers\etc.</span></span>
2. <span data-ttu-id="690e1-225">Aggiungere i seguenti tre voci tooyour host file hello: **indirizzo IP DATA 0**, **indirizzo IP fisso Controller 0**, e **indirizzo IP fisso Controller 1**.</span><span class="sxs-lookup"><span data-stu-id="690e1-225">Add hello following three entries tooyour hosts file: **DATA 0 IP address**, **Controller 0 Fixed IP address**, and **Controller 1 Fixed IP address**.</span></span>
3. <span data-ttu-id="690e1-226">Numero di serie hello dispositivo salvato in precedenza.</span><span class="sxs-lookup"><span data-stu-id="690e1-226">Enter hello device serial number that you saved earlier.</span></span> <span data-ttu-id="690e1-227">Eseguire il mapping di questo indirizzo IP toohello come illustrato nella seguente immagine hello.</span><span class="sxs-lookup"><span data-stu-id="690e1-227">Map this toohello IP address as shown in hello following image.</span></span> <span data-ttu-id="690e1-228">Per Controller 0 e Controller 1, aggiungere **Controller0** e **Controller1** alla fine di hello del numero di serie hello (nome comune).</span><span class="sxs-lookup"><span data-stu-id="690e1-228">For Controller 0 and Controller 1, append **Controller0** and **Controller1** at hello end of hello serial number (CN name).</span></span>
   
    ![Aggiunta del file toohosts nome CN](./media/storsimple-remote-connect/HCS_AddingCNNameToHostsFile.png)
4. <span data-ttu-id="690e1-230">Salva file di host hello.</span><span class="sxs-lookup"><span data-stu-id="690e1-230">Save hello hosts file.</span></span>

### <a name="connect-toohello-device-from-hello-remote-host"></a><span data-ttu-id="690e1-231">Connettere il dispositivo di toohello dall'host remoto hello</span><span class="sxs-lookup"><span data-stu-id="690e1-231">Connect toohello device from hello remote host</span></span>
<span data-ttu-id="690e1-232">Uso di Windows PowerShell e SSL tooenter una sessione SSAdmin nel dispositivo da un host remoto o un client.</span><span class="sxs-lookup"><span data-stu-id="690e1-232">Use Windows PowerShell and SSL tooenter an SSAdmin session on your device from a remote host or client.</span></span> <span data-ttu-id="690e1-233">esegue il mapping di sessione SSAdmin Hello toooption 1 in hello [console seriale](storsimple-windows-powershell-administration.md#connect-to-windows-powershell-for-storsimple-via-the-device-serial-console) menu del dispositivo.</span><span class="sxs-lookup"><span data-stu-id="690e1-233">hello SSAdmin session maps toooption 1 in hello [serial console](storsimple-windows-powershell-administration.md#connect-to-windows-powershell-for-storsimple-via-the-device-serial-console) menu of your device.</span></span>

<span data-ttu-id="690e1-234">Eseguire hello procedura nel computer di hello da cui si desidera toomake hello connessione remota di Windows PowerShell.</span><span class="sxs-lookup"><span data-stu-id="690e1-234">Perform hello following procedure on hello computer from which you want toomake hello remote Windows PowerShell connection.</span></span>

#### <a name="tooenter-an-ssadmin-session-on-hello-device-by-using-windows-powershell-and-ssl"></a><span data-ttu-id="690e1-235">tooenter una sessione SSAdmin nel dispositivo hello usando Windows PowerShell e SSL</span><span class="sxs-lookup"><span data-stu-id="690e1-235">tooenter an SSAdmin session on hello device by using Windows PowerShell and SSL</span></span>
1. <span data-ttu-id="690e1-236">Avviare una sessione di Windows PowerShell come amministratore.</span><span class="sxs-lookup"><span data-stu-id="690e1-236">Start a Windows PowerShell session as an administrator.</span></span>
2. <span data-ttu-id="690e1-237">Aggiungere hello dispositivo IP indirizzo toohello host attendibili del client, digitare:</span><span class="sxs-lookup"><span data-stu-id="690e1-237">Add hello device IP address toohello client’s trusted hosts by typing:</span></span>
   
     `Set-Item wsman:\localhost\Client\TrustedHosts <device_ip> -Concatenate -Force`
   
    <span data-ttu-id="690e1-238">Dove <*device_ip*> è l'indirizzo IP di hello del dispositivo, ad esempio:</span><span class="sxs-lookup"><span data-stu-id="690e1-238">Where <*device_ip*> is hello IP address of your device; for example:</span></span> 
   
     `Set-Item wsman:\localhost\Client\TrustedHosts 10.126.173.90 -Concatenate -Force`
3. <span data-ttu-id="690e1-239">Creare una nuova credenziale digitando:</span><span class="sxs-lookup"><span data-stu-id="690e1-239">Create a new credential by typing:</span></span> 
   
     `$cred = New-Object pscredential @("<IP of target device>\SSAdmin", (ConvertTo-SecureString -Force -AsPlainText "<Device Administrator Password>"))`
   
    <span data-ttu-id="690e1-240">Dove <*IP del dispositivo di destinazione*> è l'indirizzo IP hello di DATA 0 per il dispositivo; ad esempio, **10.126.173.90** come mostrato nella precedente immagine del file host hello hello.</span><span class="sxs-lookup"><span data-stu-id="690e1-240">Where <*IP of target device*> is hello IP address of DATA 0 for your device; for example, **10.126.173.90** as shown in hello preceding image of hello hosts file.</span></span> <span data-ttu-id="690e1-241">Fornire hello password di amministratore per il dispositivo.</span><span class="sxs-lookup"><span data-stu-id="690e1-241">Also, supply hello administrator password for your device.</span></span>
4. <span data-ttu-id="690e1-242">Creare una sessione digitando:</span><span class="sxs-lookup"><span data-stu-id="690e1-242">Create a session by typing:</span></span>
   
     `$session = New-PSSession -UseSSL -ComputerName <Serial number of target device> -Credential $cred -ConfigurationName "SSAdminConsole"`
   
    <span data-ttu-id="690e1-243">Per il parametro - ComputerName hello nel cmdlet hello, fornire hello <*numero di serie del dispositivo di destinazione*>.</span><span class="sxs-lookup"><span data-stu-id="690e1-243">For hello -ComputerName parameter in hello cmdlet, provide hello <*serial number of target device*>.</span></span> <span data-ttu-id="690e1-244">È stato eseguito il mapping di questo numero di serie toohello di indirizzo IP di DATA 0 nel file hosts hello sull'host remoto; ad esempio, **SHX0991003G44MT** come illustrato nella seguente immagine hello.</span><span class="sxs-lookup"><span data-stu-id="690e1-244">This serial number was mapped toohello IP address of DATA 0 in hello hosts file on your remote host; for example, **SHX0991003G44MT** as shown in hello following image.</span></span>
5. <span data-ttu-id="690e1-245">Digitare:</span><span class="sxs-lookup"><span data-stu-id="690e1-245">Type:</span></span> 
   
     `Enter-PSSession $session`
6. <span data-ttu-id="690e1-246">Sarà necessario toowait qualche minuto e quindi sarà tooyour connesso al dispositivo tramite HTTPS su SSL.</span><span class="sxs-lookup"><span data-stu-id="690e1-246">You will need toowait a few minutes, and then you will be connected tooyour device via HTTPS over SSL.</span></span> <span data-ttu-id="690e1-247">Verrà visualizzato un messaggio che indica che si è connessi tooyour dispositivo.</span><span class="sxs-lookup"><span data-stu-id="690e1-247">You will see a message that indicates you are connected tooyour device.</span></span>
   
    ![Comunicazione remota PowerShell tramite HTTPS e SSL](./media/storsimple-remote-connect/HCS_PSRemotingUsingHTTPSAndSSL.png)

## <a name="next-steps"></a><span data-ttu-id="690e1-249">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="690e1-249">Next steps</span></span>
* <span data-ttu-id="690e1-250">Altre informazioni, vedere [utilizzando tooadminister di Windows PowerShell del dispositivo StorSimple](storsimple-windows-powershell-administration.md).</span><span class="sxs-lookup"><span data-stu-id="690e1-250">Learn more about [using Windows PowerShell tooadminister your StorSimple device](storsimple-windows-powershell-administration.md).</span></span>
* <span data-ttu-id="690e1-251">Altre informazioni, vedere [utilizzando hello tooadminister servizio StorSimple Manager dispositivo StorSimple](storsimple-manager-service-administration.md).</span><span class="sxs-lookup"><span data-stu-id="690e1-251">Learn more about [using hello StorSimple Manager service tooadminister your StorSimple device](storsimple-manager-service-administration.md).</span></span>


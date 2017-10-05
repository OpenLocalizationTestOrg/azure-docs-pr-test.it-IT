---
title: Connessione remota al dispositivo StorSimple | Microsoft Docs
description: Viene illustrato come configurare il dispositivo per la gestione remota e come connettersi a Windows PowerShell per StorSimple tramite HTTP o HTTPS.
services: storsimple
documentationcenter: 
author: alkohli
manager: timlt
editor: 
ms.assetid: 
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 04/07/2017
ms.author: alkohli
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: ff76884f020a0fb8a1b48bd371c419bd65e85fd3
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="connect-remotely-to-your-storsimple-8000-series-device"></a><span data-ttu-id="6aab4-103">Connettersi in remoto al dispositivo StorSimple serie 8000</span><span class="sxs-lookup"><span data-stu-id="6aab4-103">Connect remotely to your StorSimple 8000 series device</span></span>

## <a name="overview"></a><span data-ttu-id="6aab4-104">Panoramica</span><span class="sxs-lookup"><span data-stu-id="6aab4-104">Overview</span></span>

<span data-ttu-id="6aab4-105">È possibile connettersi in remoto al dispositivo tramite Windows PowerShell.</span><span class="sxs-lookup"><span data-stu-id="6aab4-105">You can remotely connect to your device via Windows PowerShell.</span></span> <span data-ttu-id="6aab4-106">Questo metodo di connessione non consente di visualizzare alcun menu.</span><span class="sxs-lookup"><span data-stu-id="6aab4-106">When you connect this way, you do not see a menu.</span></span> <span data-ttu-id="6aab4-107">(Verrà visualizzato un menu solo se si utilizza la console seriale del dispositivo per la connessione.) Con la comunicazione remota di Windows PowerShell, ci si connette a uno specifico spazio di esecuzione.</span><span class="sxs-lookup"><span data-stu-id="6aab4-107">(You see a menu only if you use the serial console on the device to connect.) With Windows PowerShell remoting, you connect to a specific runspace.</span></span> <span data-ttu-id="6aab4-108">È inoltre possibile specificare la lingua di visualizzazione.</span><span class="sxs-lookup"><span data-stu-id="6aab4-108">You can also specify the display language.</span></span>

<span data-ttu-id="6aab4-109">Per ulteriori informazioni sull'utilizzo della comunicazione remota di Windows PowerShell per gestire il dispositivo, andare a [Utilizzare Windows PowerShell per StorSimple per gestire il dispositivo StorSimple](storsimple-8000-windows-powershell-administration.md).</span><span class="sxs-lookup"><span data-stu-id="6aab4-109">For more information about using Windows PowerShell remoting to manage your device, go to [Use Windows PowerShell for StorSimple to administer your StorSimple device](storsimple-8000-windows-powershell-administration.md).</span></span>

<span data-ttu-id="6aab4-110">In questa esercitazione viene illustrato come configurare il dispositivo per la gestione remota, quindi come connettersi a Windows PowerShell per StorSimple.</span><span class="sxs-lookup"><span data-stu-id="6aab4-110">This tutorial explains how to configure your device for remote management and then how to connect to Windows PowerShell for StorSimple.</span></span> <span data-ttu-id="6aab4-111">È possibile usare HTTP o HTTPS per connettersi in remoto tramite Windows PowerShell.</span><span class="sxs-lookup"><span data-stu-id="6aab4-111">You can use HTTP or HTTPS to remotely connect via Windows PowerShell.</span></span> <span data-ttu-id="6aab4-112">Tuttavia, quando si decide come connettersi a Windows PowerShell per StorSimple, considerare quanto segue:</span><span class="sxs-lookup"><span data-stu-id="6aab4-112">However, when you are deciding how to connect to Windows PowerShell for StorSimple, consider the following information:</span></span>

* <span data-ttu-id="6aab4-113">La connessione diretta alla console seriale del dispositivo è protetta ma la connessione alla console seriale sugli switch di rete non lo è.</span><span class="sxs-lookup"><span data-stu-id="6aab4-113">Connecting directly to the device serial console is secure, but connecting to the serial console over network switches is not.</span></span> <span data-ttu-id="6aab4-114">Prestare attenzione al rischio di sicurezza quando ci si connette alla console seriale del dispositivo sugli switch di rete.</span><span class="sxs-lookup"><span data-stu-id="6aab4-114">Be cautious of the security risk when connecting to the device serial console over network switches.</span></span>
* <span data-ttu-id="6aab4-115">La connessione tramite una sessione HTTP potrebbe offrire maggiore sicurezza rispetto alla connessione tramite la console seriale sulla rete.</span><span class="sxs-lookup"><span data-stu-id="6aab4-115">Connecting through an HTTP session might offer more security than connecting through the serial console over the network.</span></span> <span data-ttu-id="6aab4-116">Sebbene non sia il metodo più sicuro, è accettabile su reti attendibili.</span><span class="sxs-lookup"><span data-stu-id="6aab4-116">Although this is not the most secure method, it is acceptable on trusted networks.</span></span>
* <span data-ttu-id="6aab4-117">La connessione tramite una sessione HTTPS con un certificato autofirmato è l'opzione più sicura e consigliata.</span><span class="sxs-lookup"><span data-stu-id="6aab4-117">Connecting through an HTTPS session with a self-signed certificate is the most secure and the recommended option.</span></span>

<span data-ttu-id="6aab4-118">È possibile connettersi in remoto all'interfaccia di Windows PowerShell.</span><span class="sxs-lookup"><span data-stu-id="6aab4-118">You can connect remotely to the Windows PowerShell interface.</span></span> <span data-ttu-id="6aab4-119">Tuttavia, l'accesso remoto al dispositivo StorSimple tramite l'interfaccia di Windows PowerShell non è abilitato per impostazione predefinita.</span><span class="sxs-lookup"><span data-stu-id="6aab4-119">However, remote access to your StorSimple device via the Windows PowerShell interface is not enabled by default.</span></span> <span data-ttu-id="6aab4-120">È necessario abilitare innanzitutto la gestione remota sul dispositivo, quindi sul client usato per l'accesso al dispositivo.</span><span class="sxs-lookup"><span data-stu-id="6aab4-120">You must enable remote management on the device first, and then on the client that is used to access your device.</span></span>

<span data-ttu-id="6aab4-121">I passaggi descritti in questo articolo sono stati eseguiti in un sistema host che esegue Windows Server 2012 R2.</span><span class="sxs-lookup"><span data-stu-id="6aab4-121">The steps described in this article were performed on a host system running Windows Server 2012 R2.</span></span>

## <a name="connect-through-http"></a><span data-ttu-id="6aab4-122">Connessione tramite HTTP</span><span class="sxs-lookup"><span data-stu-id="6aab4-122">Connect through HTTP</span></span>

<span data-ttu-id="6aab4-123">La connessione a Windows PowerShell per StorSimple tramite una sessione HTTP offre una maggiore protezione rispetto alla connessione tramite la console seriale del dispositivo StorSimple.</span><span class="sxs-lookup"><span data-stu-id="6aab4-123">Connecting to Windows PowerShell for StorSimple through an HTTP session offers more security than connecting through the serial console of your StorSimple device.</span></span> <span data-ttu-id="6aab4-124">Sebbene non sia il metodo più sicuro, è accettabile su reti attendibili.</span><span class="sxs-lookup"><span data-stu-id="6aab4-124">Although this is not the most secure method, it is acceptable on trusted networks.</span></span>

<span data-ttu-id="6aab4-125">Per configurare la gestione remota, è possibile usare il portale di Azure o la console seriale.</span><span class="sxs-lookup"><span data-stu-id="6aab4-125">You can use either the Azure portal or the serial console to configure remote management.</span></span> <span data-ttu-id="6aab4-126">Selezionare una delle seguenti procedure:</span><span class="sxs-lookup"><span data-stu-id="6aab4-126">Select from the following procedures:</span></span>

* [<span data-ttu-id="6aab4-127">Utilizzo del portale di Azure per abilitare la gestione remota su HTTP</span><span class="sxs-lookup"><span data-stu-id="6aab4-127">Use the Azure portal to enable remote management over HTTP</span></span>](#use-the-azure-classic-portal-to-enable-remote-management-over-http)
* [<span data-ttu-id="6aab4-128">Utilizzo della console seriale per abilitare la gestione remota su HTTP</span><span class="sxs-lookup"><span data-stu-id="6aab4-128">Use the serial console to enable remote management over HTTP</span></span>](#use-the-serial-console-to-enable-remote-management-over-http)

<span data-ttu-id="6aab4-129">Dopo aver abilitato la gestione remota, utilizzare la procedura seguente per preparare il client per una connessione remota.</span><span class="sxs-lookup"><span data-stu-id="6aab4-129">After you enable remote management, use the following procedure to prepare the client for a remote connection.</span></span>

* [<span data-ttu-id="6aab4-130">Preparazione del client per la connessione remota</span><span class="sxs-lookup"><span data-stu-id="6aab4-130">Prepare the client for remote connection</span></span>](#prepare-the-client-for-remote-connection)

### <a name="use-the-azure-portal-to-enable-remote-management-over-http"></a><span data-ttu-id="6aab4-131">Utilizzo del portale di Azure per abilitare la gestione remota su HTTP</span><span class="sxs-lookup"><span data-stu-id="6aab4-131">Use the Azure portal to enable remote management over HTTP</span></span>

<span data-ttu-id="6aab4-132">Attenersi alla procedura seguente nel portale di Azure per abilitare la gestione remota su HTTP.</span><span class="sxs-lookup"><span data-stu-id="6aab4-132">Perform the following steps in the Azure portal to enable remote management over HTTP.</span></span>

#### <a name="to-enable-remote-management-through-the-azure-portal"></a><span data-ttu-id="6aab4-133">Per abilitare la gestione remota tramite il portale di Azure</span><span class="sxs-lookup"><span data-stu-id="6aab4-133">To enable remote management through the Azure portal</span></span>

1. <span data-ttu-id="6aab4-134">Passare al servizio Gestione dispositivi StorSimple.</span><span class="sxs-lookup"><span data-stu-id="6aab4-134">Go to your StorSimple Device Manager service.</span></span> <span data-ttu-id="6aab4-135">Selezionare **Dispositivi** e quindi fare clic sul dispositivo che si vuole configurare per la gestione remota.</span><span class="sxs-lookup"><span data-stu-id="6aab4-135">Select **Devices** and then select and click the device you want to configure for remote management.</span></span> <span data-ttu-id="6aab4-136">Passare a **Impostazioni dispositivo > Sicurezza**.</span><span class="sxs-lookup"><span data-stu-id="6aab4-136">Go to **Device settings > Security**.</span></span>
2. <span data-ttu-id="6aab4-137">Nel pannello **Impostazioni di sicurezza** fare clic su **Gestione remota**.</span><span class="sxs-lookup"><span data-stu-id="6aab4-137">In the **Security settings** blade, click **Remote Management**.</span></span>
3. <span data-ttu-id="6aab4-138">Nel pannello **Gestione remota** impostare l'opzione **Abilita gestione remota** su **Sì**.</span><span class="sxs-lookup"><span data-stu-id="6aab4-138">In the **Remote management** blade, set **Enable Remote Management** to **Yes**.</span></span>
4. <span data-ttu-id="6aab4-139">È ora possibile scegliere di connettersi tramite HTTP.</span><span class="sxs-lookup"><span data-stu-id="6aab4-139">You can now choose to connect using HTTP.</span></span> <span data-ttu-id="6aab4-140">(La connessione su HTTPS rappresenta la scelta predefinita.) Assicurarsi che HTTP sia selezionato.</span><span class="sxs-lookup"><span data-stu-id="6aab4-140">(The default is to connect over HTTPS.) Make sure that HTTP is selected.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="6aab4-141">La connessione tramite HTTP dovrebbe essere eseguita solo su reti attendibili.</span><span class="sxs-lookup"><span data-stu-id="6aab4-141">Connecting over HTTP is acceptable only on trusted networks.</span></span>
   
5. <span data-ttu-id="6aab4-142">Alla richiesta di conferma fare clic su **Salva** e quindi su **Sì**.</span><span class="sxs-lookup"><span data-stu-id="6aab4-142">Click **Save** and when prompted for confirmation, select **Yes**.</span></span>

### <a name="use-the-serial-console-to-enable-remote-management-over-http"></a><span data-ttu-id="6aab4-143">Utilizzo della console seriale per abilitare la gestione remota su HTTP</span><span class="sxs-lookup"><span data-stu-id="6aab4-143">Use the serial console to enable remote management over HTTP</span></span>
<span data-ttu-id="6aab4-144">Eseguire le operazioni seguenti nella console seriale del dispositivo per abilitare la gestione remota.</span><span class="sxs-lookup"><span data-stu-id="6aab4-144">Perform the following steps on the device serial console to enable remote management.</span></span>

#### <a name="to-enable-remote-management-through-the-device-serial-console"></a><span data-ttu-id="6aab4-145">Per abilitare la gestione remota tramite la console seriale del dispositivo:</span><span class="sxs-lookup"><span data-stu-id="6aab4-145">To enable remote management through the device serial console</span></span>
1. <span data-ttu-id="6aab4-146">Nel menu della console seriale, selezionare l'opzione 1.</span><span class="sxs-lookup"><span data-stu-id="6aab4-146">On the serial console menu, select option 1.</span></span> <span data-ttu-id="6aab4-147">Per altre informazioni sull'uso della console seriale del dispositivo, vedere [Connessione a Windows PowerShell per StorSimple tramite la console seriale del dispositivo](storsimple-8000-windows-powershell-administration.md#connect-to-windows-powershell-for-storsimple-via-the-device-serial-console).</span><span class="sxs-lookup"><span data-stu-id="6aab4-147">For more information about using the serial console on the device, go to [Connect to Windows PowerShell for StorSimple via device serial console](storsimple-8000-windows-powershell-administration.md#connect-to-windows-powershell-for-storsimple-via-the-device-serial-console).</span></span>
2. <span data-ttu-id="6aab4-148">Al prompt dei comandi, digitare: `Enable-HcsRemoteManagement –AllowHttp`</span><span class="sxs-lookup"><span data-stu-id="6aab4-148">At the prompt, type: `Enable-HcsRemoteManagement –AllowHttp`</span></span>
3. <span data-ttu-id="6aab4-149">L'utente riceve una notifica sulle vulnerabilità di sicurezza relative all'utilizzo di HTTP per la connessione al dispositivo.</span><span class="sxs-lookup"><span data-stu-id="6aab4-149">You are notified about the security vulnerabilities of using HTTP to connect to the device.</span></span> <span data-ttu-id="6aab4-150">Quando richiesto, confermare digitando **Y**.</span><span class="sxs-lookup"><span data-stu-id="6aab4-150">When prompted, confirm by typing **Y**.</span></span>
4. <span data-ttu-id="6aab4-151">Verificare che HTTP sia abilitato digitando: `Get-HcsSystem`</span><span class="sxs-lookup"><span data-stu-id="6aab4-151">Verify that HTTP is enabled by typing: `Get-HcsSystem`</span></span>
5. <span data-ttu-id="6aab4-152">Verificare che il campo **RemoteManagementMode** mostri **HttpsAndHttpEnabled**. Nella figura seguente vengono illustrate queste impostazioni in PuTTY.</span><span class="sxs-lookup"><span data-stu-id="6aab4-152">Verify that the **RemoteManagementMode** field shows **HttpsAndHttpEnabled**.The following illustration shows these settings in PuTTY.</span></span>
   
     ![Seriali HTTPS e HTTP abilitati](./media/storsimple-remote-connect/HCS_SerialHttpsAndHttpEnabled.png)

### <a name="prepare-the-client-for-remote-connection"></a><span data-ttu-id="6aab4-154">Preparazione del client per la connessione remota</span><span class="sxs-lookup"><span data-stu-id="6aab4-154">Prepare the client for remote connection</span></span>
<span data-ttu-id="6aab4-155">Eseguire le operazioni seguenti sul client per abilitare la gestione remota.</span><span class="sxs-lookup"><span data-stu-id="6aab4-155">Perform the following steps on the client to enable remote management.</span></span>

#### <a name="to-prepare-the-client-for-remote-connection"></a><span data-ttu-id="6aab4-156">Per preparare il client per la connessione remota:</span><span class="sxs-lookup"><span data-stu-id="6aab4-156">To prepare the client for remote connection</span></span>
1. <span data-ttu-id="6aab4-157">Avviare una sessione di Windows PowerShell come amministratore.</span><span class="sxs-lookup"><span data-stu-id="6aab4-157">Start a Windows PowerShell session as an administrator.</span></span>
2. <span data-ttu-id="6aab4-158">Digitare il comando seguente per aggiungere l'indirizzo IP del dispositivo StorSimple all'elenco di host attendibili del client:</span><span class="sxs-lookup"><span data-stu-id="6aab4-158">Type the following command to add the IP address of the StorSimple device to the client’s trusted hosts list:</span></span>
   
     `Set-Item wsman:\localhost\Client\TrustedHosts <device_ip> -Concatenate -Force`
   
     <span data-ttu-id="6aab4-159">Sostituire <*ip_dispositivo*> con l'indirizzo IP del dispositivo, ad esempio:</span><span class="sxs-lookup"><span data-stu-id="6aab4-159">Replace <*device_ip*> with the IP address of your device; for example:</span></span> 
   
     `Set-Item wsman:\localhost\Client\TrustedHosts 10.126.173.90 -Concatenate -Force`
3. <span data-ttu-id="6aab4-160">Digitare il comando seguente per salvare le credenziali del dispositivo in una variabile:</span><span class="sxs-lookup"><span data-stu-id="6aab4-160">Type the following command to save the device credentials in a variable:</span></span> 
   
    ```
    $cred = Get-Credential
    ```
    
4. <span data-ttu-id="6aab4-161">Nella finestra di dialogo visualizzata:</span><span class="sxs-lookup"><span data-stu-id="6aab4-161">In the dialog box that appears:</span></span>
   
   1. <span data-ttu-id="6aab4-162">Digitare il nome utente nel formato: *ip_dispositivo\SSAdmin*.</span><span class="sxs-lookup"><span data-stu-id="6aab4-162">Type the user name in this format: *device_ip\SSAdmin*.</span></span>
   2. <span data-ttu-id="6aab4-163">Digitare la password di amministratore del dispositivo impostata quando il dispositivo è stato configurato con la configurazione guidata.</span><span class="sxs-lookup"><span data-stu-id="6aab4-163">Type the device administrator password that was set when the device was configured with the setup wizard.</span></span> <span data-ttu-id="6aab4-164">La password predefinita è *Password1*.</span><span class="sxs-lookup"><span data-stu-id="6aab4-164">The default password is *Password1*.</span></span>
5. <span data-ttu-id="6aab4-165">Avviare una sessione di Windows PowerShell sul dispositivo digitando questo comando:</span><span class="sxs-lookup"><span data-stu-id="6aab4-165">Start a Windows PowerShell session on the device by typing this command:</span></span>
   
     `Enter-PSSession -Credential $cred -ConfigurationName SSAdminConsole -ComputerName <device_ip>`
   
   > [!NOTE]
   > <span data-ttu-id="6aab4-166">Per creare una sessione di Windows PowerShell per l'utilizzo con il dispositivo virtuale StorSimple, aggiungere il parametro `–Port` e specificare la porta pubblica configurata nella comunicazione remota per il dispositivo virtuale StorSimple.</span><span class="sxs-lookup"><span data-stu-id="6aab4-166">To create a Windows PowerShell session for use with the StorSimple virtual device, append the `–Port` parameter and specify the public port that you configured in Remoting for StorSimple Virtual Appliance.</span></span>
   
   
<span data-ttu-id="6aab4-167">A questo punto, è necessario disporre di una sessione remota attiva di Windows PowerShell sul dispositivo.</span><span class="sxs-lookup"><span data-stu-id="6aab4-167">At this point, you should have an active remote Windows PowerShell session to the device.</span></span>
   
![Comunicazione remota PowerShell tramite HTTP](./media/storsimple-remote-connect/HCS_PSRemotingUsingHTTP.png)

## <a name="connect-through-https"></a><span data-ttu-id="6aab4-169">Connessione tramite HTTPS</span><span class="sxs-lookup"><span data-stu-id="6aab4-169">Connect through HTTPS</span></span>

<span data-ttu-id="6aab4-170">La connessione a Windows PowerShell per StorSimple tramite una sessione HTTPS è il metodo più sicuro e consigliato di connessione remota al dispositivo Microsoft Azure StorSimple.</span><span class="sxs-lookup"><span data-stu-id="6aab4-170">Connecting to Windows PowerShell for StorSimple through an HTTPS session is the most secure and recommended method of remotely connecting to your Microsoft Azure StorSimple device.</span></span> <span data-ttu-id="6aab4-171">Nelle procedure seguenti viene illustrato come configurare la console seriale e i computer client, in modo che sia possibile utilizzare HTTPS per connettersi a Windows PowerShell per StorSimple.</span><span class="sxs-lookup"><span data-stu-id="6aab4-171">The following procedures explain how to set up the serial console and client computers so that you can use HTTPS to connect to Windows PowerShell for StorSimple.</span></span>

<span data-ttu-id="6aab4-172">Per configurare la gestione remota, è possibile usare il portale di Azure o la console seriale.</span><span class="sxs-lookup"><span data-stu-id="6aab4-172">You can use either the Azure portal or the serial console to configure remote management.</span></span> <span data-ttu-id="6aab4-173">Selezionare una delle seguenti procedure:</span><span class="sxs-lookup"><span data-stu-id="6aab4-173">Select from the following procedures:</span></span>

* [<span data-ttu-id="6aab4-174">Utilizzo del portale di Azure per abilitare la gestione remota su HTTPS</span><span class="sxs-lookup"><span data-stu-id="6aab4-174">Use the Azure portal to enable remote management over HTTPS</span></span>](#use-the-azure-classic-portal-to-enable-remote-management-over-https)
* [<span data-ttu-id="6aab4-175">Utilizzo della console seriale per abilitare la gestione remota su HTTPS</span><span class="sxs-lookup"><span data-stu-id="6aab4-175">Use the serial console to enable remote management over HTTPS</span></span>](#use-the-serial-console-to-enable-remote-management-over-https)

<span data-ttu-id="6aab4-176">Dopo aver abilitato la gestione remota, utilizzare le procedure seguenti per preparare l'host per la gestione remota e connettersi al dispositivo dall'host remoto.</span><span class="sxs-lookup"><span data-stu-id="6aab4-176">After you enable remote management, use the following procedures to prepare the host for a remote management and connect to the device from the remote host.</span></span>

* [<span data-ttu-id="6aab4-177">Preparazione dell'host per la gestione remota</span><span class="sxs-lookup"><span data-stu-id="6aab4-177">Prepare the host for remote management</span></span>](#prepare-the-host-for-remote-management)
* [<span data-ttu-id="6aab4-178">Connessione al dispositivo dall'host remoto</span><span class="sxs-lookup"><span data-stu-id="6aab4-178">Connect to the device from the remote host</span></span>](#connect-to-the-device-from-the-remote-host)

### <a name="use-the-azure-portal-to-enable-remote-management-over-https"></a><span data-ttu-id="6aab4-179">Utilizzo del portale di Azure per abilitare la gestione remota su HTTPS</span><span class="sxs-lookup"><span data-stu-id="6aab4-179">Use the Azure portal to enable remote management over HTTPS</span></span>

<span data-ttu-id="6aab4-180">Attenersi alla procedura seguente nel portale di Azure per abilitare la gestione remota su HTTPS.</span><span class="sxs-lookup"><span data-stu-id="6aab4-180">Perform the following steps in the Azure portal to enable remote management over HTTPS.</span></span>

#### <a name="to-enable-remote-management-over-https-from-the-azure-portal"></a><span data-ttu-id="6aab4-181">Per abilitare la gestione remota su HTTPS dal portale di Azure</span><span class="sxs-lookup"><span data-stu-id="6aab4-181">To enable remote management over HTTPS from the Azure portal</span></span>

1. <span data-ttu-id="6aab4-182">Passare al servizio Gestione dispositivi StorSimple.</span><span class="sxs-lookup"><span data-stu-id="6aab4-182">Go to your StorSimple Device Manager service.</span></span> <span data-ttu-id="6aab4-183">Selezionare **Dispositivi** e quindi fare clic sul dispositivo che si vuole configurare per la gestione remota.</span><span class="sxs-lookup"><span data-stu-id="6aab4-183">Select **Devices** and then select and click the device you want to configure for remote management.</span></span> <span data-ttu-id="6aab4-184">Passare a **Impostazioni dispositivo > Sicurezza**.</span><span class="sxs-lookup"><span data-stu-id="6aab4-184">Go to **Device settings > Security**.</span></span>
2. <span data-ttu-id="6aab4-185">Nel pannello **Impostazioni di sicurezza** fare clic su **Gestione remota**.</span><span class="sxs-lookup"><span data-stu-id="6aab4-185">In the **Security settings** blade, click **Remote Management**.</span></span>
3. <span data-ttu-id="6aab4-186">Impostare **Abilita gestione remota** su **Sì**.</span><span class="sxs-lookup"><span data-stu-id="6aab4-186">Set **Enable Remote Management** to **Yes**.</span></span>
4. <span data-ttu-id="6aab4-187">È ora possibile scegliere di connettersi tramite HTTPS.</span><span class="sxs-lookup"><span data-stu-id="6aab4-187">You can now choose to connect using HTTPS.</span></span> <span data-ttu-id="6aab4-188">(La connessione su HTTPS rappresenta la scelta predefinita.) Assicurarsi che HTTPS sia selezionato.</span><span class="sxs-lookup"><span data-stu-id="6aab4-188">(The default is to connect over HTTPS.) Make sure that HTTPS is selected.</span></span>
5. <span data-ttu-id="6aab4-189">Fare clic su **Scarica il certificato di gestione remota**.</span><span class="sxs-lookup"><span data-stu-id="6aab4-189">Click ... and then click **Download Remote Management Certificate**.</span></span> <span data-ttu-id="6aab4-190">Specificare un percorso per salvare il file.</span><span class="sxs-lookup"><span data-stu-id="6aab4-190">Specify a location to save this file.</span></span> <span data-ttu-id="6aab4-191">Sarà necessario installare questo certificato nel computer client o host che si userà per connettersi al dispositivo.</span><span class="sxs-lookup"><span data-stu-id="6aab4-191">You need to install this certificate on the client or host computer that you will use to connect to the device.</span></span>
6. <span data-ttu-id="6aab4-192">Alla richiesta di conferma fare clic su **Salva** e quindi su **Sì**.</span><span class="sxs-lookup"><span data-stu-id="6aab4-192">Click **Save** and then click **Yes** when prompted for confirmation.</span></span>

### <a name="use-the-serial-console-to-enable-remote-management-over-https"></a><span data-ttu-id="6aab4-193">Utilizzo della console seriale per abilitare la gestione remota su HTTPS</span><span class="sxs-lookup"><span data-stu-id="6aab4-193">Use the serial console to enable remote management over HTTPS</span></span>

<span data-ttu-id="6aab4-194">Eseguire le operazioni seguenti nella console seriale del dispositivo per abilitare la gestione remota.</span><span class="sxs-lookup"><span data-stu-id="6aab4-194">Perform the following steps on the device serial console to enable remote management.</span></span>

#### <a name="to-enable-remote-management-through-the-device-serial-console"></a><span data-ttu-id="6aab4-195">Per abilitare la gestione remota tramite la console seriale del dispositivo:</span><span class="sxs-lookup"><span data-stu-id="6aab4-195">To enable remote management through the device serial console</span></span>
1. <span data-ttu-id="6aab4-196">Nel menu della console seriale, selezionare l'opzione 1.</span><span class="sxs-lookup"><span data-stu-id="6aab4-196">On the serial console menu, select option 1.</span></span> <span data-ttu-id="6aab4-197">Per altre informazioni sull'uso della console seriale del dispositivo, vedere [Connessione a Windows PowerShell per StorSimple tramite la console seriale del dispositivo](storsimple-8000-windows-powershell-administration.md#connect-to-windows-powershell-for-storsimple-via-the-device-serial-console).</span><span class="sxs-lookup"><span data-stu-id="6aab4-197">For more information about using the serial console on the device, go to [Connect to Windows PowerShell for StorSimple via device serial console](storsimple-8000-windows-powershell-administration.md#connect-to-windows-powershell-for-storsimple-via-the-device-serial-console).</span></span>
2. <span data-ttu-id="6aab4-198">Al prompt dei comandi, digitare: </span><span class="sxs-lookup"><span data-stu-id="6aab4-198">At the prompt, type:</span></span>
   
     `Enable-HcsRemoteManagement`
   
    <span data-ttu-id="6aab4-199">Ciò dovrebbe abilitare HTTPS sul dispositivo.</span><span class="sxs-lookup"><span data-stu-id="6aab4-199">This should enable HTTPS on your device.</span></span>
3. <span data-ttu-id="6aab4-200">Verificare che HTTPS sia abilitato digitando:</span><span class="sxs-lookup"><span data-stu-id="6aab4-200">Verify that HTTPS has been enabled by typing:</span></span> 
   
     `Get-HcsSystem`
   
    <span data-ttu-id="6aab4-201">Assicurarsi che il campo **RemoteManagementMode** contenga **HttpsEnabled**. La figura seguente mostra queste impostazioni in PuTTY.</span><span class="sxs-lookup"><span data-stu-id="6aab4-201">Make sure that the **RemoteManagementMode** field shows **HttpsEnabled**.The following illustration shows these settings in PuTTY.</span></span>
   
     ![Seriale HTTPS abilitato](./media/storsimple-remote-connect/HCS_SerialHttpsEnabled.png)
4. <span data-ttu-id="6aab4-203">Dall'output di `Get-HcsSystem`, copiare il numero di serie del dispositivo e salvarlo per un utilizzo successivo.</span><span class="sxs-lookup"><span data-stu-id="6aab4-203">From the output of `Get-HcsSystem`, copy the serial number of the device and save it for later use.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="6aab4-204">Il numero di serie esegue il mapping sul nome CN nel certificato.</span><span class="sxs-lookup"><span data-stu-id="6aab4-204">The serial number maps to the CN name in the certificate.</span></span>
   
5. <span data-ttu-id="6aab4-205">Ottenere un certificato di gestione remota digitando:</span><span class="sxs-lookup"><span data-stu-id="6aab4-205">Obtain a remote management certificate by typing:</span></span> 
   
     `Get-HcsRemoteManagementCert`
   
    <span data-ttu-id="6aab4-206">Verrà visualizzato un certificato simile al seguente.</span><span class="sxs-lookup"><span data-stu-id="6aab4-206">A certificate similar to the following will appear.</span></span>
   
    ![Ottenimento del certificato di gestione remota](./media/storsimple-remote-connect/HCS_GetRemoteManagementCertificate.png)
6. <span data-ttu-id="6aab4-208">Copiare le informazioni sul certificato da **-----BEGIN CERTIFICATE-----** a **-----END CERTIFICATE-----** in un editor di testo come Blocco note e salvarlo come file con estensione .cer.</span><span class="sxs-lookup"><span data-stu-id="6aab4-208">Copy the information in the certificate from **-----BEGIN CERTIFICATE-----** to **-----END CERTIFICATE-----** into a text editor such as Notepad, and save it as a .cer file.</span></span> <span data-ttu-id="6aab4-209">(Il file dovrà essere copiato sull'host remoto quando si prepara l'host.)</span><span class="sxs-lookup"><span data-stu-id="6aab4-209">(You will copy this file to your remote host when you prepare the host.)</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="6aab4-210">Per generare un nuovo certificato, utilizzare il cmdlet `Set-HcsRemoteManagementCert`.</span><span class="sxs-lookup"><span data-stu-id="6aab4-210">To generate a new certificate, use the `Set-HcsRemoteManagementCert` cmdlet.</span></span>
   
### <a name="prepare-the-host-for-remote-management"></a><span data-ttu-id="6aab4-211">Preparazione dell'host per la gestione remota</span><span class="sxs-lookup"><span data-stu-id="6aab4-211">Prepare the host for remote management</span></span>

<span data-ttu-id="6aab4-212">Per preparare il computer host per una connessione remota che utilizza una sessione HTTPS, eseguire le procedure seguenti:</span><span class="sxs-lookup"><span data-stu-id="6aab4-212">To prepare the host computer for a remote connection that uses an HTTPS session, perform the following procedures:</span></span>

* <span data-ttu-id="6aab4-213">[Importazione del file con estensione .cer nell'archivio radice del client o dell'host remoto](#to-import-the-certificate-on-the-remote-host)</span><span class="sxs-lookup"><span data-stu-id="6aab4-213">[Import the .cer file into the root store of the client or remote host](#to-import-the-certificate-on-the-remote-host).</span></span>
* <span data-ttu-id="6aab4-214">[Aggiunta dei numeri di serie del dispositivo al file hosts sull'host remoto](#to-add-device-serial-numbers-to-the-remote-host)</span><span class="sxs-lookup"><span data-stu-id="6aab4-214">[Add the device serial numbers to the hosts file on your remote host](#to-add-device-serial-numbers-to-the-remote-host).</span></span>

<span data-ttu-id="6aab4-215">Ognuna di queste procedure è descritta di seguito.</span><span class="sxs-lookup"><span data-stu-id="6aab4-215">Each of the preceding procedures, is described below.</span></span>

#### <a name="to-import-the-certificate-on-the-remote-host"></a><span data-ttu-id="6aab4-216">Per importare il certificato nell'host remoto:</span><span class="sxs-lookup"><span data-stu-id="6aab4-216">To import the certificate on the remote host</span></span>
1. <span data-ttu-id="6aab4-217">Fare clic con il pulsante destro del mouse sul file con estensione .cer e selezionare **Installa certificato**.</span><span class="sxs-lookup"><span data-stu-id="6aab4-217">Right-click the .cer file and select **Install certificate**.</span></span> <span data-ttu-id="6aab4-218">Viene avviata l'Esportazione guidata certificati.</span><span class="sxs-lookup"><span data-stu-id="6aab4-218">This starts the Certificate Import Wizard.</span></span>
   
    ![Impostazione guidata del certificato 1](./media/storsimple-remote-connect/HCS_CertificateImportWizard1.png)
2. <span data-ttu-id="6aab4-220">Per **Percorso archivio**, selezionare **Computer locale**, quindi fare clic su **Avanti**.</span><span class="sxs-lookup"><span data-stu-id="6aab4-220">For **Store location**, select **Local Machine**, and then click **Next**.</span></span>
3. <span data-ttu-id="6aab4-221">Selezionare **Colloca tutti i certificati nel seguente archivio**, quindi fare clic su **Sfoglia**.</span><span class="sxs-lookup"><span data-stu-id="6aab4-221">Select **Place all certificates in the following store**, and then click **Browse**.</span></span> <span data-ttu-id="6aab4-222">Passare all'archivio radice dell'host remoto, quindi fare clic su **Avanti**.</span><span class="sxs-lookup"><span data-stu-id="6aab4-222">Navigate to the root store of your remote host, and then click **Next**.</span></span>
   
    ![Impostazione guidata del certificato 2](./media/storsimple-remote-connect/HCS_CertificateImportWizard2.png)
4. <span data-ttu-id="6aab4-224">Fare clic su **Finish**.</span><span class="sxs-lookup"><span data-stu-id="6aab4-224">Click **Finish**.</span></span> <span data-ttu-id="6aab4-225">Viene visualizzato un messaggio indicante che l'importazione è avvenuta correttamente.</span><span class="sxs-lookup"><span data-stu-id="6aab4-225">A message that tells you that the import was successful appears.</span></span>
   
    ![Impostazione guidata del certificato 3](./media/storsimple-remote-connect/HCS_CertificateImportWizard3.png)

#### <a name="to-add-device-serial-numbers-to-the-remote-host"></a><span data-ttu-id="6aab4-227">Per aggiungere i numeri di serie del dispositivo all'host remoto:</span><span class="sxs-lookup"><span data-stu-id="6aab4-227">To add device serial numbers to the remote host</span></span>
1. <span data-ttu-id="6aab4-228">Avviare Blocco note come amministratore, quindi aprire il file hosts che si trova in \Windows\System32\Drivers\etc.</span><span class="sxs-lookup"><span data-stu-id="6aab4-228">Start Notepad as an administrator, and then open the hosts file located at \Windows\System32\Drivers\etc.</span></span>
2. <span data-ttu-id="6aab4-229">Aggiungere le tre voci seguenti al file hosts: **DATA 0 IP address**, **Controller 0 Fixed IP address** e **Controller 1 Fixed IP address**.</span><span class="sxs-lookup"><span data-stu-id="6aab4-229">Add the following three entries to your hosts file: **DATA 0 IP address**, **Controller 0 Fixed IP address**, and **Controller 1 Fixed IP address**.</span></span>
3. <span data-ttu-id="6aab4-230">Immettere il numero di serie salvato in precedenza.</span><span class="sxs-lookup"><span data-stu-id="6aab4-230">Enter the device serial number that you saved earlier.</span></span> <span data-ttu-id="6aab4-231">Eseguirne il mapping all'indirizzo IP come illustrato nella figura seguente.</span><span class="sxs-lookup"><span data-stu-id="6aab4-231">Map this to the IP address as shown in the following image.</span></span> <span data-ttu-id="6aab4-232">Per Controller 0 e Controller 1, aggiungere **Controller0** e **Controller1** alla fine del numero di serie (nome CN).</span><span class="sxs-lookup"><span data-stu-id="6aab4-232">For Controller 0 and Controller 1, append **Controller0** and **Controller1** at the end of the serial number (CN name).</span></span>
   
    ![Aggiunta del nome CN al file hosts](./media/storsimple-remote-connect/HCS_AddingCNNameToHostsFile.png)
4. <span data-ttu-id="6aab4-234">Salvare il file hosts.</span><span class="sxs-lookup"><span data-stu-id="6aab4-234">Save the hosts file.</span></span>

### <a name="connect-to-the-device-from-the-remote-host"></a><span data-ttu-id="6aab4-235">Connessione al dispositivo dall'host remoto</span><span class="sxs-lookup"><span data-stu-id="6aab4-235">Connect to the device from the remote host</span></span>

<span data-ttu-id="6aab4-236">Utilizzare Windows PowerShell e SSL per accedere a una sessione SSAdmin sul dispositivo da un client o un host remoto.</span><span class="sxs-lookup"><span data-stu-id="6aab4-236">Use Windows PowerShell and SSL to enter an SSAdmin session on your device from a remote host or client.</span></span> <span data-ttu-id="6aab4-237">Viene eseguito il mapping della sessione SSAdmin all'opzione 1 del menu [console seriale](storsimple-8000-windows-powershell-administration.md#connect-to-windows-powershell-for-storsimple-via-the-device-serial-console) del dispositivo.</span><span class="sxs-lookup"><span data-stu-id="6aab4-237">The SSAdmin session maps to option 1 in the [serial console](storsimple-8000-windows-powershell-administration.md#connect-to-windows-powershell-for-storsimple-via-the-device-serial-console) menu of your device.</span></span>

<span data-ttu-id="6aab4-238">Eseguire la procedura seguente sul computer da cui si desidera effettuare la connessione remota di Windows PowerShell.</span><span class="sxs-lookup"><span data-stu-id="6aab4-238">Perform the following procedure on the computer from which you want to make the remote Windows PowerShell connection.</span></span>

#### <a name="to-enter-an-ssadmin-session-on-the-device-by-using-windows-powershell-and-ssl"></a><span data-ttu-id="6aab4-239">Per accedere a una sessione SSAdmin sul dispositivo tramite Windows PowerShell e SSL:</span><span class="sxs-lookup"><span data-stu-id="6aab4-239">To enter an SSAdmin session on the device by using Windows PowerShell and SSL</span></span>
1. <span data-ttu-id="6aab4-240">Avviare una sessione di Windows PowerShell come amministratore.</span><span class="sxs-lookup"><span data-stu-id="6aab4-240">Start a Windows PowerShell session as an administrator.</span></span>
2. <span data-ttu-id="6aab4-241">Aggiungere l'indirizzo IP del dispositivo agli host attendibili del client digitando:</span><span class="sxs-lookup"><span data-stu-id="6aab4-241">Add the device IP address to the client’s trusted hosts by typing:</span></span>
   
     `Set-Item wsman:\localhost\Client\TrustedHosts <device_ip> -Concatenate -Force`
   
    <span data-ttu-id="6aab4-242">Dove <*ip_dispositivo*> è l'indirizzo IP del dispositivo, ad esempio:</span><span class="sxs-lookup"><span data-stu-id="6aab4-242">Where <*device_ip*> is the IP address of your device; for example:</span></span> 
   
     `Set-Item wsman:\localhost\Client\TrustedHosts 10.126.173.90 -Concatenate -Force`
3. <span data-ttu-id="6aab4-243">Per creare una nuova credenziale digitare:</span><span class="sxs-lookup"><span data-stu-id="6aab4-243">To create a new credential, type:</span></span>
   
     `$cred = New-Object pscredential @("<IP of target device>\SSAdmin", (ConvertTo-SecureString -Force -AsPlainText "<Device Administrator Password>"))`
   
    <span data-ttu-id="6aab4-244">Dove <*IP del dispositivo di destinazione*> è l'indirizzo IP di DATA 0 per il dispositivo, ad esempio, **10.126.173.90** come illustrato nell'immagine precedente del file hosts.</span><span class="sxs-lookup"><span data-stu-id="6aab4-244">Where <*IP of target device*> is the IP address of DATA 0 for your device; for example, **10.126.173.90** as shown in the preceding image of the hosts file.</span></span> <span data-ttu-id="6aab4-245">Inoltre, fornire la password di amministratore per il dispositivo.</span><span class="sxs-lookup"><span data-stu-id="6aab4-245">Also, supply the administrator password for your device.</span></span>
4. <span data-ttu-id="6aab4-246">Creare una sessione digitando:</span><span class="sxs-lookup"><span data-stu-id="6aab4-246">Create a session by typing:</span></span>
   
     `$session = New-PSSession -UseSSL -ComputerName <Serial number of target device> -Credential $cred -ConfigurationName "SSAdminConsole"`
   
    <span data-ttu-id="6aab4-247">Per il parametro -ComputerName nel cmdlet, specificare il <*numero di serie del dispositivo di destinazione*>.</span><span class="sxs-lookup"><span data-stu-id="6aab4-247">For the -ComputerName parameter in the cmdlet, provide the <*serial number of target device*>.</span></span> <span data-ttu-id="6aab4-248">Questo numero di serie è stato mappato all'indirizzo IP di DATA 0 nel file hosts sull'host remoto; ad esempio, **SHX0991003G44MT** come illustrato nella figura seguente.</span><span class="sxs-lookup"><span data-stu-id="6aab4-248">This serial number was mapped to the IP address of DATA 0 in the hosts file on your remote host; for example, **SHX0991003G44MT** as shown in the following image.</span></span>
5. <span data-ttu-id="6aab4-249">Digitare:</span><span class="sxs-lookup"><span data-stu-id="6aab4-249">Type:</span></span>
   
     `Enter-PSSession $session`
6. <span data-ttu-id="6aab4-250">Sarà necessario attendere alcuni minuti, quindi verrà effettuata la connessione al dispositivo tramite HTTPS su SSL.</span><span class="sxs-lookup"><span data-stu-id="6aab4-250">You will need to wait a few minutes, and then you will be connected to your device via HTTPS over SSL.</span></span> <span data-ttu-id="6aab4-251">Verrà visualizzato un messaggio indicante che è stata effettuata la connessione al dispositivo.</span><span class="sxs-lookup"><span data-stu-id="6aab4-251">You see a message that indicates you are connected to your device.</span></span>
   
    ![Comunicazione remota PowerShell tramite HTTPS e SSL](./media/storsimple-remote-connect/HCS_PSRemotingUsingHTTPSAndSSL.png)

## <a name="next-steps"></a><span data-ttu-id="6aab4-253">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="6aab4-253">Next steps</span></span>

* <span data-ttu-id="6aab4-254">Leggere ulteriori informazioni sull' [utilizzo di Windows PowerShell per amministrare il dispositivo StorSimple](storsimple-8000-windows-powershell-administration.md).</span><span class="sxs-lookup"><span data-stu-id="6aab4-254">Learn more about [using Windows PowerShell to administer your StorSimple device](storsimple-8000-windows-powershell-administration.md).</span></span>
* <span data-ttu-id="6aab4-255">Altre informazioni sull'[utilizzo del servizio Gestione dispositivi StorSimple per la gestione del dispositivo StorSimple](storsimple-8000-manager-service-administration.md).</span><span class="sxs-lookup"><span data-stu-id="6aab4-255">Learn more about [using the StorSimple Device Manager service to administer your StorSimple device](storsimple-8000-manager-service-administration.md).</span></span>


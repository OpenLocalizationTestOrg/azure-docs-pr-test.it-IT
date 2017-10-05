---
title: Uso del reindirizzamento in Azure RemoteApp | Microsoft Docs
description: Informazioni su come configurare e usare il reindirizzamento in RemoteApp
services: remoteapp
documentationcenter: 
author: msmbaldwin
manager: mbaldwin
ms.assetid: 2c8c867f-4907-4f2e-9ccd-2eb82bb5b837
ms.service: remoteapp
ms.workload: compute
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/26/2017
ms.author: mbaldwin
ms.openlocfilehash: b5a65d129225fde46e3b090bc3cd9427989005ee
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="using-redirection-in-azure-remoteapp"></a><span data-ttu-id="d7421-103">Uso del reindirizzamento in Azure RemoteApp</span><span class="sxs-lookup"><span data-stu-id="d7421-103">Using redirection in Azure RemoteApp</span></span>
> [!IMPORTANT]
> <span data-ttu-id="d7421-104">Azure RemoteApp verrà sospeso a partire dal 31 agosto 2017.</span><span class="sxs-lookup"><span data-stu-id="d7421-104">Azure RemoteApp is being discontinued on August 31, 2017.</span></span> <span data-ttu-id="d7421-105">Per i dettagli, vedere l' [annuncio](https://go.microsoft.com/fwlink/?linkid=821148) .</span><span class="sxs-lookup"><span data-stu-id="d7421-105">Read the [announcement](https://go.microsoft.com/fwlink/?linkid=821148) for details.</span></span>
> 
> 

<span data-ttu-id="d7421-106">Il reindirizzamento dei dispositivi consente agli utenti di interagire con applicazioni remote tramite i dispositivi collegati al proprio computer, telefono o tablet locale.</span><span class="sxs-lookup"><span data-stu-id="d7421-106">Device redirection lets your users interact with remote apps using the devices attached to their local computer, phone, or tablet.</span></span> <span data-ttu-id="d7421-107">Ad esempio, se Skype è accessibile tramite Azure RemoteApp, sul computer dell'utente deve essere installata una telecamera per poter usare Skype.</span><span class="sxs-lookup"><span data-stu-id="d7421-107">For example, if you have provided Skype through Azure RemoteApp, your user needs the camera installed on their PC to work with Skype.</span></span> <span data-ttu-id="d7421-108">Lo stesso vale per stampanti, altoparlanti, monitor e vari dispositivi con connessione USB.</span><span class="sxs-lookup"><span data-stu-id="d7421-108">This is also true for printers, speakers, monitors, and a range of USB-connected peripherals.</span></span>

<span data-ttu-id="d7421-109">RemoteApp usa il protocollo RDP (Remote Desktop Protocol) e RemoteFX per il reindirizzamento.</span><span class="sxs-lookup"><span data-stu-id="d7421-109">RemoteApp leverages the Remote Desktop Protocol (RDP) and RemoteFX to provide redirection.</span></span>

## <a name="what-redirection-is-enabled-by-default"></a><span data-ttu-id="d7421-110">Quale reindirizzamento è abilitato per impostazione predefinita?</span><span class="sxs-lookup"><span data-stu-id="d7421-110">What redirection is enabled by default?</span></span>
<span data-ttu-id="d7421-111">Quando si usa RemoteApp, i reindirizzamenti seguenti sono abilitati per impostazione predefinita.</span><span class="sxs-lookup"><span data-stu-id="d7421-111">When you use RemoteApp, the following redirections are enabled by default.</span></span> <span data-ttu-id="d7421-112">Le informazioni tra parentesi mostrano l'impostazione RDP.</span><span class="sxs-lookup"><span data-stu-id="d7421-112">The information in parentheses show the RDP setting.</span></span>

* <span data-ttu-id="d7421-113">Riproduzione di suoni sul computer locale (**Riproduci nel computer locale**).</span><span class="sxs-lookup"><span data-stu-id="d7421-113">Play sounds on the local computer (**Play on this computer**).</span></span> <span data-ttu-id="d7421-114">(audiomode:i:0)</span><span class="sxs-lookup"><span data-stu-id="d7421-114">(audiomode:i:0)</span></span>
* <span data-ttu-id="d7421-115">Acquisizione di audio dal computer locale e invio al computer remoto (**Registra da questo computer**).</span><span class="sxs-lookup"><span data-stu-id="d7421-115">Capture audio from the local computer and send to the remote computer (**Record from this computer**).</span></span> <span data-ttu-id="d7421-116">(audiocapturemode:i:1)</span><span class="sxs-lookup"><span data-stu-id="d7421-116">(audiocapturemode:i:1)</span></span>
* <span data-ttu-id="d7421-117">Stampa su stampanti locali (redirectprinters:i:1)</span><span class="sxs-lookup"><span data-stu-id="d7421-117">Print to local printers (redirectprinters:i:1)</span></span>
* <span data-ttu-id="d7421-118">Porte COM (redirectcomports:i:1)</span><span class="sxs-lookup"><span data-stu-id="d7421-118">COM ports (redirectcomports:i:1)</span></span>
* <span data-ttu-id="d7421-119">Dispositivo smart card (redirectsmartcards:i:1)</span><span class="sxs-lookup"><span data-stu-id="d7421-119">Smart card device (redirectsmartcards:i:1)</span></span>
* <span data-ttu-id="d7421-120">Appunti (funzionalità di copia e incolla) (redirectclipboard:i:1)</span><span class="sxs-lookup"><span data-stu-id="d7421-120">Clipboard (ability to copy and paste) (redirectclipboard:i:1)</span></span>
* <span data-ttu-id="d7421-121">Disattivazione caratteri smussati (allowfontsmoothing:i:1)</span><span class="sxs-lookup"><span data-stu-id="d7421-121">Clear type font smoothing (allow font smoothing:i:1)</span></span>
* <span data-ttu-id="d7421-122">Reindirizzamento di tutti i dispositivi Plug and Play supportati.</span><span class="sxs-lookup"><span data-stu-id="d7421-122">Redirect all supported Plug and Play devices.</span></span> <span data-ttu-id="d7421-123">(devicestoredirect:s:*)</span><span class="sxs-lookup"><span data-stu-id="d7421-123">(devicestoredirect:s:*)</span></span>

## <a name="what-other-redirection-is-available"></a><span data-ttu-id="d7421-124">Quali altri reindirizzamenti sono disponibili?</span><span class="sxs-lookup"><span data-stu-id="d7421-124">What other redirection is available?</span></span>
<span data-ttu-id="d7421-125">Due opzioni di reindirizzamento sono disabilitate per impostazione predefinita:</span><span class="sxs-lookup"><span data-stu-id="d7421-125">Two redirection options are disabled by default:</span></span>

* <span data-ttu-id="d7421-126">Reindirizzamento delle unità (mapping di unità): le unità del computer locale diventano unità mappate nella sessione remota.</span><span class="sxs-lookup"><span data-stu-id="d7421-126">Drive redirection (drive mapping): Your local computer's drives become mapped drives in the remote session.</span></span> <span data-ttu-id="d7421-127">In questo modo è possibile salvare o aprire file da unità locali mentre si lavora nella sessione remota.</span><span class="sxs-lookup"><span data-stu-id="d7421-127">This lets you save or open files from your local drives while you work in the remote session.</span></span>
* <span data-ttu-id="d7421-128">Reindirizzamento USB: è possibile usare i dispositivi USB collegati al computer locale all'interno della sessione remota.</span><span class="sxs-lookup"><span data-stu-id="d7421-128">USB redirection: You can use the USB devices attached to your local computer within the remote session.</span></span>

## <a name="change-your-redirection-settings-in-remoteapp"></a><span data-ttu-id="d7421-129">Modificare le impostazioni di reindirizzamento in RemoteApp</span><span class="sxs-lookup"><span data-stu-id="d7421-129">Change your redirection settings in RemoteApp</span></span>
<span data-ttu-id="d7421-130">È possibile modificare le impostazioni di reindirizzamento del dispositivo per una raccolta usando Microsoft Azure PowerShell con SDK.</span><span class="sxs-lookup"><span data-stu-id="d7421-130">You can change the device redirection settings for a collection by using the Microsoft Azure PowerShell with SDK.</span></span> <span data-ttu-id="d7421-131">Dopo aver installato il nuovo PowerShell e l'SDK, configurarlo per gestire la sottoscrizione, come descritto in [Come installare e configurare Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="d7421-131">After you install the new PowerShell and SDK, first configure it to manage your subscription as described in [How to install and configure Azure PowerShell](/powershell/azure/overview).</span></span>

<span data-ttu-id="d7421-132">Usare quindi un comando simile al seguente per impostare le proprietà RDP personalizzate:</span><span class="sxs-lookup"><span data-stu-id="d7421-132">Then use a command similar to the following to set the custom RDP properties:</span></span>

    Set-AzureRemoteAppCollection -CollectionName <collection name>  -CustomRdpProperty "drivestoredirect:s:*`nusbdevicestoredirect:s:*"

<span data-ttu-id="d7421-133">(Si noti che  *\`n*  viene utilizzato come delimitatore tra le singole proprietà.)</span><span class="sxs-lookup"><span data-stu-id="d7421-133">(Note that *\`n* is used as a delimiter between individual properties.)</span></span>

<span data-ttu-id="d7421-134">Per un elenco delle proprietà RDP configurate, eseguire il cmdlet seguente.</span><span class="sxs-lookup"><span data-stu-id="d7421-134">To get a list of what custom RDP properties are configured, run the following cmdlet.</span></span> <span data-ttu-id="d7421-135">Si noti che solo le proprietà personalizzate vengono visualizzate come risultati di output, non le proprietà predefinite:</span><span class="sxs-lookup"><span data-stu-id="d7421-135">Note that only custom properties are shown as output results and not the default properties:</span></span>  

    Get-AzureRemoteAppCollection -CollectionName <collection name>

<span data-ttu-id="d7421-136">Quando si impostano proprietà personalizzate, è necessario specificare tutte le proprietà personalizzate ogni volta. In caso contrario, l'impostazione viene nuovamente disabilitata.</span><span class="sxs-lookup"><span data-stu-id="d7421-136">When you set custom properties you must specify all custom properties each time; otherwise the setting reverts to disabled.</span></span>   

### <a name="common-examples"></a><span data-ttu-id="d7421-137">Esempi comuni</span><span class="sxs-lookup"><span data-stu-id="d7421-137">Common examples</span></span>
<span data-ttu-id="d7421-138">Per abilitare il reindirizzamento delle unità, usare il cmdlet seguente:</span><span class="sxs-lookup"><span data-stu-id="d7421-138">Use the following cmdlet to enable drive redirection:</span></span>  

    Set-AzureRemoteAppCollection -CollectionName <collection name>  -CustomRdpProperty "drivestoredirect:s:*"

<span data-ttu-id="d7421-139">Usare questo cmdlet per abilitare sia il reindirizzamento delle unità che il reindirizzamento USB:</span><span class="sxs-lookup"><span data-stu-id="d7421-139">Use this cmdlet to enable both USB and Drive redirection:</span></span>

    Set-AzureRemoteAppCollection -CollectionName <collection name>  -CustomRdpProperty "drivestoredirect:s:*`nusbdevicestoredirect:s:*"

<span data-ttu-id="d7421-140">Usare questo cmdlet per disabilitare la condivisione degli Appunti:</span><span class="sxs-lookup"><span data-stu-id="d7421-140">Use this cmdlet to disable clipboard sharing:</span></span>  

    Set-AzureRemoteAppCollection -CollectionName <collection name>  -CustomRdpProperty "redirectclipboard:i:0"

> [!IMPORTANT]
> <span data-ttu-id="d7421-141">Assicurarsi di disconnettere completamente tutti gli utenti nella raccolta (non solo scollegarli) prima di verificare la modifica.</span><span class="sxs-lookup"><span data-stu-id="d7421-141">Be sure to completely log off all users in the collection (and not just disconnect them) before you test the change.</span></span> <span data-ttu-id="d7421-142">Per assicurarsi che gli utenti siano disconnessi completamente, andare alla scheda **Sessioni** nella raccolta nel portale di Azure e disconnettere tutti gli utenti scollegati o collegati.</span><span class="sxs-lookup"><span data-stu-id="d7421-142">To ensure users are completely logged off, go to the **Sessions** tab in the collection in the Azure portal and log off any users who are disconnected or signed in.</span></span> <span data-ttu-id="d7421-143">Talvolta è necessario attendere alcuni secondi perché le unità locali vengano mostrate in Esplora risorse all'interno della sessione.</span><span class="sxs-lookup"><span data-stu-id="d7421-143">Sometimes it can take several seconds for the local drives to show in Explorer within the session.</span></span>
> 
> 

## <a name="change-usb-redirection-settings-on-your-windows-client"></a><span data-ttu-id="d7421-144">Modificare le impostazioni di reindirizzamento USB nel client Windows</span><span class="sxs-lookup"><span data-stu-id="d7421-144">Change USB redirection settings on your Windows client</span></span>
<span data-ttu-id="d7421-145">Se si desidera usare il reindirizzamento USB su un computer che si connette a RemoteApp, è necessario eseguire 2 azioni.</span><span class="sxs-lookup"><span data-stu-id="d7421-145">If you want to use USB redirection on a computer that connects to RemoteApp, there are 2 actions that need to happen.</span></span> <span data-ttu-id="d7421-146">1 - L'amministratore deve abilitare il reindirizzamento USB a livello di raccolta tramite Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="d7421-146">1 - Your administrator needs to enable USB redirection at the collection level by using Azure PowerShell.</span></span> <span data-ttu-id="d7421-147">2 - Su ogni dispositivo su cui si desidera usare il reindirizzamento USB, è necessario abilitare un criterio di gruppo che lo consente.</span><span class="sxs-lookup"><span data-stu-id="d7421-147">2 - On each device where you want to use USB redirection, you need to enable a group policy that permits it.</span></span> <span data-ttu-id="d7421-148">È necessario eseguire questo passaggio per ogni utente che desidera usare il reindirizzamento USB.</span><span class="sxs-lookup"><span data-stu-id="d7421-148">This step will need to be done for each user that wants to use USB redirection.</span></span>

> [!NOTE]
> <span data-ttu-id="d7421-149">Il reindirizzamento USB con Azure RemoteApp è supportato solo per i computer Windows.</span><span class="sxs-lookup"><span data-stu-id="d7421-149">USB redirection with Azure RemoteApp is only supported for Windows computers.</span></span>
> 
> 

### <a name="enable-usb-redirection-for-the-remoteapp-collection"></a><span data-ttu-id="d7421-150">Abilitare il reindirizzamento USB per la raccolta di RemoteApp</span><span class="sxs-lookup"><span data-stu-id="d7421-150">Enable USB redirection for the RemoteApp collection</span></span>
<span data-ttu-id="d7421-151">Per abilitare il reindirizzamento USB a livello di raccolta, utilizzare il cmdlet seguente:</span><span class="sxs-lookup"><span data-stu-id="d7421-151">Use the following cmdlet to enable USB redirection at the collection level:</span></span>

    Set-AzureRemoteAppCollection -CollectionName <collection_name> -CustomRdpProperty "nusbdevicestoredirect:s:*"

### <a name="enable-usb-redirection-for-the-client-computer"></a><span data-ttu-id="d7421-152">Abilitare il reindirizzamento USB per il computer client</span><span class="sxs-lookup"><span data-stu-id="d7421-152">Enable USB redirection for the client computer</span></span>
<span data-ttu-id="d7421-153">Per configurare le impostazioni di reindirizzamento USB sul computer:</span><span class="sxs-lookup"><span data-stu-id="d7421-153">To configure USB redirection settings on your computer:</span></span>

1. <span data-ttu-id="d7421-154">Aprire l'Editor Criteri di gruppo locali (GPEDIT.MSC)</span><span class="sxs-lookup"><span data-stu-id="d7421-154">Open the Local Group Policy Editor (GPEDIT.MSC).</span></span> <span data-ttu-id="d7421-155">(eseguire gpedit.msc da un prompt dei comandi).</span><span class="sxs-lookup"><span data-stu-id="d7421-155">(Run gpedit.msc from a command prompt.)</span></span>
2. <span data-ttu-id="d7421-156">Aprire **Configurazione computer\Criteri\Modelli amministrativi\Componenti di Windows\Servizi Desktop remoto\Client di connessione desktop remoto\Reindirizzamento dispositivo USB RemoteFX**.</span><span class="sxs-lookup"><span data-stu-id="d7421-156">Open **Computer Configuration\Policies\Administrative Templates\Windows Components\Remote Desktop Services\Remote Desktop Connection Client\RemoteFX USB Device Redirection**.</span></span>
3. <span data-ttu-id="d7421-157">Fare doppio clic su **Consenti il reindirizzamento RDP di altri dispositivi USB RemoteFX supportati da questo computer**.</span><span class="sxs-lookup"><span data-stu-id="d7421-157">Double-click **Allow RDP redirection of other supported RemoteFX USB devices from this computer**.</span></span>
4. <span data-ttu-id="d7421-158">Selezionare **Attivato** e quindi selezionare **Amministratori e utenti nei diritti di accesso del reindirizzamento USB RemoteFX**.</span><span class="sxs-lookup"><span data-stu-id="d7421-158">Select **Enabled**, and then select **Administrators and Users in the RemoteFX USB Redirection Access Rights**.</span></span>
5. <span data-ttu-id="d7421-159">Aprire un prompt dei comandi con autorizzazioni amministrative ed eseguire il comando seguente:</span><span class="sxs-lookup"><span data-stu-id="d7421-159">Open a command prompt with administrative permissions, and run the following command:</span></span>
   
        gpupdate /force
6. <span data-ttu-id="d7421-160">Riavviare il computer.</span><span class="sxs-lookup"><span data-stu-id="d7421-160">Restart the computer.</span></span>

<span data-ttu-id="d7421-161">È anche possibile usare lo strumento Gestione criteri di gruppo per creare e applicare i criteri di reindirizzamento USB per tutti i computer nel dominio:</span><span class="sxs-lookup"><span data-stu-id="d7421-161">You can also use the Group Policy Management tool to create and apply the USB redirection policy for all computers in your domain:</span></span>

1. <span data-ttu-id="d7421-162">Accedere al controller di dominio come amministratore di dominio.</span><span class="sxs-lookup"><span data-stu-id="d7421-162">Log into the domain controller as the domain administrator.</span></span>
2. <span data-ttu-id="d7421-163">Aprire Console Gestione criteri di gruppo</span><span class="sxs-lookup"><span data-stu-id="d7421-163">Open the Group Policy Management Console.</span></span> <span data-ttu-id="d7421-164">(fare clic su **Start > Strumenti di amministrazione > Gestione Criteri di gruppo**).</span><span class="sxs-lookup"><span data-stu-id="d7421-164">(Click **Start > Administrative Tools > Group Policy Management**.)</span></span>
3. <span data-ttu-id="d7421-165">Passare al dominio o unità organizzativa per cui si desidera creare il criterio.</span><span class="sxs-lookup"><span data-stu-id="d7421-165">Navigate to the domain or organizational unit for which you want to create the policy.</span></span>
4. <span data-ttu-id="d7421-166">Fare clic con il pulsante destro del mouse su **Criterio dominio predefinito** e quindi fare clic su **Modifica**.</span><span class="sxs-lookup"><span data-stu-id="d7421-166">Right-click **Default Domain Policy**, and then click **Edit**.</span></span>
5. <span data-ttu-id="d7421-167">Aprire **Configurazione computer\Criteri\Modelli amministrativi\Componenti di Windows\Servizi Desktop remoto\Client di connessione desktop remoto\Reindirizzamento dispositivo USB RemoteFX**.</span><span class="sxs-lookup"><span data-stu-id="d7421-167">Open **Computer Configuration\Policies\Administrative Templates\Windows Components\Remote Desktop Services\Remote Desktop Connection Client\RemoteFX USB Device Redirection**.</span></span>
6. <span data-ttu-id="d7421-168">Fare doppio clic su **Consenti il reindirizzamento RDP di altri dispositivi USB RemoteFX supportati da questo computer**.</span><span class="sxs-lookup"><span data-stu-id="d7421-168">Double-click **Allow RDP redirection of other supported RemoteFX USB devices from this computer**.</span></span>
7. <span data-ttu-id="d7421-169">Selezionare **Attivato** e quindi selezionare **Amministratori e utenti nei diritti di accesso del reindirizzamento USB RemoteFX**.</span><span class="sxs-lookup"><span data-stu-id="d7421-169">Select **Enabled**, and then select **Administrators and Users in the RemoteFX USB Redirection Access Rights**.</span></span>
8. <span data-ttu-id="d7421-170">Fare clic su **OK**.</span><span class="sxs-lookup"><span data-stu-id="d7421-170">Click **OK**.</span></span>  


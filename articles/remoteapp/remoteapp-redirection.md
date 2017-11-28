---
title: reindirizzamento aaaUsing in Azure RemoteApp | Documenti Microsoft
description: Informazioni su come tooconfigure e utilizzare il reindirizzamento in RemoteApp
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
ms.openlocfilehash: d5739a75cf606bd971268da67b2c5ff0fe5fe19b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="using-redirection-in-azure-remoteapp"></a><span data-ttu-id="31483-103">Uso del reindirizzamento in Azure RemoteApp</span><span class="sxs-lookup"><span data-stu-id="31483-103">Using redirection in Azure RemoteApp</span></span>
> [!IMPORTANT]
> <span data-ttu-id="31483-104">Azure RemoteApp verrà sospeso a partire dal 31 agosto 2017.</span><span class="sxs-lookup"><span data-stu-id="31483-104">Azure RemoteApp is being discontinued on August 31, 2017.</span></span> <span data-ttu-id="31483-105">Hello lettura [annuncio](https://go.microsoft.com/fwlink/?linkid=821148) per informazioni dettagliate.</span><span class="sxs-lookup"><span data-stu-id="31483-105">Read hello [announcement](https://go.microsoft.com/fwlink/?linkid=821148) for details.</span></span>
> 
> 

<span data-ttu-id="31483-106">Reindirizzamento della periferica consente agli utenti di interagire con le applicazioni remote utilizzando hello dispositivi collegati tootheir locale computer, telefono o tablet.</span><span class="sxs-lookup"><span data-stu-id="31483-106">Device redirection lets your users interact with remote apps using hello devices attached tootheir local computer, phone, or tablet.</span></span> <span data-ttu-id="31483-107">Ad esempio, se sono stati forniti Skype tramite Azure RemoteApp, l'utente deve fotocamera hello installata toowork i PC con Skype.</span><span class="sxs-lookup"><span data-stu-id="31483-107">For example, if you have provided Skype through Azure RemoteApp, your user needs hello camera installed on their PC toowork with Skype.</span></span> <span data-ttu-id="31483-108">Lo stesso vale per stampanti, altoparlanti, monitor e vari dispositivi con connessione USB.</span><span class="sxs-lookup"><span data-stu-id="31483-108">This is also true for printers, speakers, monitors, and a range of USB-connected peripherals.</span></span>

<span data-ttu-id="31483-109">RemoteApp sfrutta hello Remote Desktop Protocol (RDP) e RemoteFX tooprovide reindirizzamento.</span><span class="sxs-lookup"><span data-stu-id="31483-109">RemoteApp leverages hello Remote Desktop Protocol (RDP) and RemoteFX tooprovide redirection.</span></span>

## <a name="what-redirection-is-enabled-by-default"></a><span data-ttu-id="31483-110">Quale reindirizzamento è abilitato per impostazione predefinita?</span><span class="sxs-lookup"><span data-stu-id="31483-110">What redirection is enabled by default?</span></span>
<span data-ttu-id="31483-111">Quando si usa RemoteApp, hello dopo i reindirizzamenti è abilitato per impostazione predefinita.</span><span class="sxs-lookup"><span data-stu-id="31483-111">When you use RemoteApp, hello following redirections are enabled by default.</span></span> <span data-ttu-id="31483-112">informazioni di Hello tra parentesi indicano impostazione RDP hello.</span><span class="sxs-lookup"><span data-stu-id="31483-112">hello information in parentheses show hello RDP setting.</span></span>

* <span data-ttu-id="31483-113">Riprodurre suoni del computer locale hello (**riprodurre su questo computer**).</span><span class="sxs-lookup"><span data-stu-id="31483-113">Play sounds on hello local computer (**Play on this computer**).</span></span> <span data-ttu-id="31483-114">(audiomode:i:0)</span><span class="sxs-lookup"><span data-stu-id="31483-114">(audiomode:i:0)</span></span>
* <span data-ttu-id="31483-115">Acquisizione audio dal computer locale hello e il computer remoto di trasmissione toohello (**registra da questo computer**).</span><span class="sxs-lookup"><span data-stu-id="31483-115">Capture audio from hello local computer and send toohello remote computer (**Record from this computer**).</span></span> <span data-ttu-id="31483-116">(audiocapturemode:i:1)</span><span class="sxs-lookup"><span data-stu-id="31483-116">(audiocapturemode:i:1)</span></span>
* <span data-ttu-id="31483-117">Stampa toolocal stampanti (redirectprinters:i:1)</span><span class="sxs-lookup"><span data-stu-id="31483-117">Print toolocal printers (redirectprinters:i:1)</span></span>
* <span data-ttu-id="31483-118">Porte COM (redirectcomports:i:1)</span><span class="sxs-lookup"><span data-stu-id="31483-118">COM ports (redirectcomports:i:1)</span></span>
* <span data-ttu-id="31483-119">Dispositivo smart card (redirectsmartcards:i:1)</span><span class="sxs-lookup"><span data-stu-id="31483-119">Smart card device (redirectsmartcards:i:1)</span></span>
* <span data-ttu-id="31483-120">Appunti (toocopy possibilità e Incolla) (redirectclipboard:i:1)</span><span class="sxs-lookup"><span data-stu-id="31483-120">Clipboard (ability toocopy and paste) (redirectclipboard:i:1)</span></span>
* <span data-ttu-id="31483-121">Disattivazione caratteri smussati (allowfontsmoothing:i:1)</span><span class="sxs-lookup"><span data-stu-id="31483-121">Clear type font smoothing (allow font smoothing:i:1)</span></span>
* <span data-ttu-id="31483-122">Reindirizzamento di tutti i dispositivi Plug and Play supportati.</span><span class="sxs-lookup"><span data-stu-id="31483-122">Redirect all supported Plug and Play devices.</span></span> <span data-ttu-id="31483-123">(devicestoredirect:s:*)</span><span class="sxs-lookup"><span data-stu-id="31483-123">(devicestoredirect:s:*)</span></span>

## <a name="what-other-redirection-is-available"></a><span data-ttu-id="31483-124">Quali altri reindirizzamenti sono disponibili?</span><span class="sxs-lookup"><span data-stu-id="31483-124">What other redirection is available?</span></span>
<span data-ttu-id="31483-125">Due opzioni di reindirizzamento sono disabilitate per impostazione predefinita:</span><span class="sxs-lookup"><span data-stu-id="31483-125">Two redirection options are disabled by default:</span></span>

* <span data-ttu-id="31483-126">Il reindirizzamento dell'unità (unità): unità del computer locale diventano le unità mappate in sessione remota hello.</span><span class="sxs-lookup"><span data-stu-id="31483-126">Drive redirection (drive mapping): Your local computer's drives become mapped drives in hello remote session.</span></span> <span data-ttu-id="31483-127">In questo modo si salvano o i file aperti da unità locali mentre si lavora nella sessione remota hello.</span><span class="sxs-lookup"><span data-stu-id="31483-127">This lets you save or open files from your local drives while you work in hello remote session.</span></span>
* <span data-ttu-id="31483-128">Il reindirizzamento USB: È possibile utilizzare un computer locale tooyour collegati dispositivi USB hello all'interno della sessione remota hello.</span><span class="sxs-lookup"><span data-stu-id="31483-128">USB redirection: You can use hello USB devices attached tooyour local computer within hello remote session.</span></span>

## <a name="change-your-redirection-settings-in-remoteapp"></a><span data-ttu-id="31483-129">Modificare le impostazioni di reindirizzamento in RemoteApp</span><span class="sxs-lookup"><span data-stu-id="31483-129">Change your redirection settings in RemoteApp</span></span>
<span data-ttu-id="31483-130">È possibile modificare le impostazioni di reindirizzamento dispositivo hello per una raccolta con hello Microsoft Azure PowerShell SDK.</span><span class="sxs-lookup"><span data-stu-id="31483-130">You can change hello device redirection settings for a collection by using hello Microsoft Azure PowerShell with SDK.</span></span> <span data-ttu-id="31483-131">Dopo aver installato hello PowerShell nuovo e SDK, configurarlo toomanage la sottoscrizione come descritto in [come tooinstall e configurare Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="31483-131">After you install hello new PowerShell and SDK, first configure it toomanage your subscription as described in [How tooinstall and configure Azure PowerShell](/powershell/azure/overview).</span></span>

<span data-ttu-id="31483-132">Utilizzare quindi un toohello simile comando hello personalizzato tooset RDP le proprietà seguenti:</span><span class="sxs-lookup"><span data-stu-id="31483-132">Then use a command similar toohello following tooset hello custom RDP properties:</span></span>

    Set-AzureRemoteAppCollection -CollectionName <collection name>  -CustomRdpProperty "drivestoredirect:s:*`nusbdevicestoredirect:s:*"

<span data-ttu-id="31483-133">(Si noti che  *\`n*  viene utilizzato come delimitatore tra le singole proprietà.)</span><span class="sxs-lookup"><span data-stu-id="31483-133">(Note that *\`n* is used as a delimiter between individual properties.)</span></span>

<span data-ttu-id="31483-134">tooget un elenco di quali proprietà RDP personalizzate sono configurate, eseguire hello cmdlet seguente.</span><span class="sxs-lookup"><span data-stu-id="31483-134">tooget a list of what custom RDP properties are configured, run hello following cmdlet.</span></span> <span data-ttu-id="31483-135">Si noti che le proprietà personalizzate solo sono visualizzate come risultati di output e non hello proprietà predefinite:</span><span class="sxs-lookup"><span data-stu-id="31483-135">Note that only custom properties are shown as output results and not hello default properties:</span></span>  

    Get-AzureRemoteAppCollection -CollectionName <collection name>

<span data-ttu-id="31483-136">Quando si impostano le proprietà personalizzate è necessario specificare tutte le proprietà personalizzate ogni volta; in caso contrario impostazione hello Ripristina toodisabled.</span><span class="sxs-lookup"><span data-stu-id="31483-136">When you set custom properties you must specify all custom properties each time; otherwise hello setting reverts toodisabled.</span></span>   

### <a name="common-examples"></a><span data-ttu-id="31483-137">Esempi comuni</span><span class="sxs-lookup"><span data-stu-id="31483-137">Common examples</span></span>
<span data-ttu-id="31483-138">Utilizzare hello dopo il reindirizzamento delle unità tooenable cmdlet:</span><span class="sxs-lookup"><span data-stu-id="31483-138">Use hello following cmdlet tooenable drive redirection:</span></span>  

    Set-AzureRemoteAppCollection -CollectionName <collection name>  -CustomRdpProperty "drivestoredirect:s:*"

<span data-ttu-id="31483-139">Utilizzare questo cmdlet tooenable il reindirizzamento USB e unità:</span><span class="sxs-lookup"><span data-stu-id="31483-139">Use this cmdlet tooenable both USB and Drive redirection:</span></span>

    Set-AzureRemoteAppCollection -CollectionName <collection name>  -CustomRdpProperty "drivestoredirect:s:*`nusbdevicestoredirect:s:*"

<span data-ttu-id="31483-140">Utilizzare la condivisione degli Appunti di cmdlet toodisable:</span><span class="sxs-lookup"><span data-stu-id="31483-140">Use this cmdlet toodisable clipboard sharing:</span></span>  

    Set-AzureRemoteAppCollection -CollectionName <collection name>  -CustomRdpProperty "redirectclipboard:i:0"

> [!IMPORTANT]
> <span data-ttu-id="31483-141">Essere toocompletely che disconnette tutti gli utenti nella raccolta di hello (e non solo disconnetterle) prima di testare modifica hello.</span><span class="sxs-lookup"><span data-stu-id="31483-141">Be sure toocompletely log off all users in hello collection (and not just disconnect them) before you test hello change.</span></span> <span data-ttu-id="31483-142">tooensure gli utenti sono completamente disconnessi, andare toohello **sessioni** scheda nella raccolta di hello nel portale di Azure hello e disconnettersi da tutti gli utenti vengono disconnessi o l'accesso.</span><span class="sxs-lookup"><span data-stu-id="31483-142">tooensure users are completely logged off, go toohello **Sessions** tab in hello collection in hello Azure portal and log off any users who are disconnected or signed in.</span></span> <span data-ttu-id="31483-143">Talvolta può richiedere alcuni secondi per hello unità locali tooshow Explorer all'interno della sessione di hello.</span><span class="sxs-lookup"><span data-stu-id="31483-143">Sometimes it can take several seconds for hello local drives tooshow in Explorer within hello session.</span></span>
> 
> 

## <a name="change-usb-redirection-settings-on-your-windows-client"></a><span data-ttu-id="31483-144">Modificare le impostazioni di reindirizzamento USB nel client Windows</span><span class="sxs-lookup"><span data-stu-id="31483-144">Change USB redirection settings on your Windows client</span></span>
<span data-ttu-id="31483-145">Se si desidera il reindirizzamento USB toouse in un computer che si connette tooRemoteApp, esistono 2 azioni che richiedono toohappen.</span><span class="sxs-lookup"><span data-stu-id="31483-145">If you want toouse USB redirection on a computer that connects tooRemoteApp, there are 2 actions that need toohappen.</span></span> <span data-ttu-id="31483-146">1 - l'amministratore deve il reindirizzamento USB tooenable a livello di raccolta hello tramite Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="31483-146">1 - Your administrator needs tooenable USB redirection at hello collection level by using Azure PowerShell.</span></span> <span data-ttu-id="31483-147">2 - in ogni dispositivo in cui si desidera il reindirizzamento USB toouse, è necessario tooenable criteri di gruppo è consentito.</span><span class="sxs-lookup"><span data-stu-id="31483-147">2 - On each device where you want toouse USB redirection, you need tooenable a group policy that permits it.</span></span> <span data-ttu-id="31483-148">Questo passaggio sarà necessario eseguire per ogni utente che richiede il reindirizzamento USB toouse toobe.</span><span class="sxs-lookup"><span data-stu-id="31483-148">This step will need toobe done for each user that wants toouse USB redirection.</span></span>

> [!NOTE]
> <span data-ttu-id="31483-149">Il reindirizzamento USB con Azure RemoteApp è supportato solo per i computer Windows.</span><span class="sxs-lookup"><span data-stu-id="31483-149">USB redirection with Azure RemoteApp is only supported for Windows computers.</span></span>
> 
> 

### <a name="enable-usb-redirection-for-hello-remoteapp-collection"></a><span data-ttu-id="31483-150">Abilitare il reindirizzamento USB per hello raccolta RemoteApp</span><span class="sxs-lookup"><span data-stu-id="31483-150">Enable USB redirection for hello RemoteApp collection</span></span>
<span data-ttu-id="31483-151">Utilizzare hello dopo il reindirizzamento USB tooenable di cmdlet a livello di raccolta hello:</span><span class="sxs-lookup"><span data-stu-id="31483-151">Use hello following cmdlet tooenable USB redirection at hello collection level:</span></span>

    Set-AzureRemoteAppCollection -CollectionName <collection_name> -CustomRdpProperty "nusbdevicestoredirect:s:*"

### <a name="enable-usb-redirection-for-hello-client-computer"></a><span data-ttu-id="31483-152">Abilitare il reindirizzamento USB per computer client hello</span><span class="sxs-lookup"><span data-stu-id="31483-152">Enable USB redirection for hello client computer</span></span>
<span data-ttu-id="31483-153">impostazioni di reindirizzamento tooconfigure USB nel computer in uso:</span><span class="sxs-lookup"><span data-stu-id="31483-153">tooconfigure USB redirection settings on your computer:</span></span>

1. <span data-ttu-id="31483-154">Hello aprire Editor criteri di gruppo locali (GPEDIT. MSC).</span><span class="sxs-lookup"><span data-stu-id="31483-154">Open hello Local Group Policy Editor (GPEDIT.MSC).</span></span> <span data-ttu-id="31483-155">(eseguire gpedit.msc da un prompt dei comandi).</span><span class="sxs-lookup"><span data-stu-id="31483-155">(Run gpedit.msc from a command prompt.)</span></span>
2. <span data-ttu-id="31483-156">Aprire **Configurazione computer\Criteri\Modelli amministrativi\Componenti di Windows\Servizi Desktop remoto\Client di connessione desktop remoto\Reindirizzamento dispositivo USB RemoteFX**.</span><span class="sxs-lookup"><span data-stu-id="31483-156">Open **Computer Configuration\Policies\Administrative Templates\Windows Components\Remote Desktop Services\Remote Desktop Connection Client\RemoteFX USB Device Redirection**.</span></span>
3. <span data-ttu-id="31483-157">Fare doppio clic su **Consenti il reindirizzamento RDP di altri dispositivi USB RemoteFX supportati da questo computer**.</span><span class="sxs-lookup"><span data-stu-id="31483-157">Double-click **Allow RDP redirection of other supported RemoteFX USB devices from this computer**.</span></span>
4. <span data-ttu-id="31483-158">Selezionare **abilitato**, quindi selezionare **amministratori e utenti in hello diritti di accesso il reindirizzamento USB di RemoteFX**.</span><span class="sxs-lookup"><span data-stu-id="31483-158">Select **Enabled**, and then select **Administrators and Users in hello RemoteFX USB Redirection Access Rights**.</span></span>
5. <span data-ttu-id="31483-159">Aprire un prompt dei comandi con autorizzazioni di amministratore ed eseguire hello comando seguente:</span><span class="sxs-lookup"><span data-stu-id="31483-159">Open a command prompt with administrative permissions, and run hello following command:</span></span>
   
        gpupdate /force
6. <span data-ttu-id="31483-160">Riavviare il computer di hello.</span><span class="sxs-lookup"><span data-stu-id="31483-160">Restart hello computer.</span></span>

<span data-ttu-id="31483-161">È anche possibile utilizzare toocreate strumento di gestione criteri di gruppo hello e applicare i criteri per il reindirizzamento USB hello per tutti i computer nel dominio:</span><span class="sxs-lookup"><span data-stu-id="31483-161">You can also use hello Group Policy Management tool toocreate and apply hello USB redirection policy for all computers in your domain:</span></span>

1. <span data-ttu-id="31483-162">Accedere al controller di dominio hello come amministratore di dominio hello.</span><span class="sxs-lookup"><span data-stu-id="31483-162">Log into hello domain controller as hello domain administrator.</span></span>
2. <span data-ttu-id="31483-163">Aprire Console Gestione criteri di gruppo hello.</span><span class="sxs-lookup"><span data-stu-id="31483-163">Open hello Group Policy Management Console.</span></span> <span data-ttu-id="31483-164">(fare clic su **Start > Strumenti di amministrazione > Gestione Criteri di gruppo**).</span><span class="sxs-lookup"><span data-stu-id="31483-164">(Click **Start > Administrative Tools > Group Policy Management**.)</span></span>
3. <span data-ttu-id="31483-165">Passare toohello dominio o unità organizzativa per il quale si desidera che i criteri di hello toocreate.</span><span class="sxs-lookup"><span data-stu-id="31483-165">Navigate toohello domain or organizational unit for which you want toocreate hello policy.</span></span>
4. <span data-ttu-id="31483-166">Fare clic con il pulsante destro del mouse su **Criterio dominio predefinito** e quindi fare clic su **Modifica**.</span><span class="sxs-lookup"><span data-stu-id="31483-166">Right-click **Default Domain Policy**, and then click **Edit**.</span></span>
5. <span data-ttu-id="31483-167">Aprire **Configurazione computer\Criteri\Modelli amministrativi\Componenti di Windows\Servizi Desktop remoto\Client di connessione desktop remoto\Reindirizzamento dispositivo USB RemoteFX**.</span><span class="sxs-lookup"><span data-stu-id="31483-167">Open **Computer Configuration\Policies\Administrative Templates\Windows Components\Remote Desktop Services\Remote Desktop Connection Client\RemoteFX USB Device Redirection**.</span></span>
6. <span data-ttu-id="31483-168">Fare doppio clic su **Consenti il reindirizzamento RDP di altri dispositivi USB RemoteFX supportati da questo computer**.</span><span class="sxs-lookup"><span data-stu-id="31483-168">Double-click **Allow RDP redirection of other supported RemoteFX USB devices from this computer**.</span></span>
7. <span data-ttu-id="31483-169">Selezionare **abilitato**, quindi selezionare **amministratori e utenti in hello diritti di accesso il reindirizzamento USB di RemoteFX**.</span><span class="sxs-lookup"><span data-stu-id="31483-169">Select **Enabled**, and then select **Administrators and Users in hello RemoteFX USB Redirection Access Rights**.</span></span>
8. <span data-ttu-id="31483-170">Fare clic su **OK**.</span><span class="sxs-lookup"><span data-stu-id="31483-170">Click **OK**.</span></span>  


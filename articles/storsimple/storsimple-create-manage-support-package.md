---
title: Creare un pacchetto per il supporto StorSimple | Microsoft Docs
description: Informazioni su come creare, decrittografare e modificare un pacchetto per il supporto del dispositivo StorSimple.
services: storsimple
documentationcenter: 
author: alkohli
manager: carmonm
editor: 
ms.assetid: eac76f5f-5db1-4c92-af8c-54053b91e66c
ms.service: storsimple
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/17/2016
ms.author: alkohli
ms.openlocfilehash: 32d20e7a8adcfc646c592213fe7395b87a93c985
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="create-and-manage-a-storsimple-support-package"></a><span data-ttu-id="b5426-103">Creare e gestire un pacchetto di supporto StorSimple</span><span class="sxs-lookup"><span data-stu-id="b5426-103">Create and manage a StorSimple support package</span></span>
## <a name="overview"></a><span data-ttu-id="b5426-104">Panoramica</span><span class="sxs-lookup"><span data-stu-id="b5426-104">Overview</span></span>
<span data-ttu-id="b5426-105">Un pacchetto per il supporto StorSimple è un meccanismo semplice da usare che raccoglie tutti i log pertinenti per aiutare il supporto tecnico Microsoft a risolvere i problemi relativi ai dispositivi StorSimple.</span><span class="sxs-lookup"><span data-stu-id="b5426-105">A StorSimple support package is an easy-to-use mechanism that collects all relevant logs to assist Microsoft Support with troubleshooting any StorSimple device issues.</span></span> <span data-ttu-id="b5426-106">I log raccolti vengono crittografati e compressi.</span><span class="sxs-lookup"><span data-stu-id="b5426-106">The collected logs are encrypted and compressed.</span></span>

<span data-ttu-id="b5426-107">Questa esercitazione include istruzioni dettagliate per creare e gestire il pacchetto per il supporto.</span><span class="sxs-lookup"><span data-stu-id="b5426-107">This tutorial includes step-by-step instructions to create and manage the support package.</span></span>

## <a name="create-and-upload-a-support-package-in-the-azure-classic-portal"></a><span data-ttu-id="b5426-108">Creare e caricare un pacchetto per il supporto nel portale di Azure classico</span><span class="sxs-lookup"><span data-stu-id="b5426-108">Create and upload a support package in the Azure classic portal</span></span>
<span data-ttu-id="b5426-109">È possibile creare e caricare un pacchetto per il supporto nel sito del supporto tecnico Microsoft tramite la pagina **Manutenzione** del servizio nel portale di Azure classico.</span><span class="sxs-lookup"><span data-stu-id="b5426-109">You can create and upload a support package to the Microsoft Support site through the **Maintenance** page of the service in the Azure classic portal.</span></span>

> [!NOTE]
> <span data-ttu-id="b5426-110">Per il caricamento è necessaria una passkey per il supporto.</span><span class="sxs-lookup"><span data-stu-id="b5426-110">The upload requires a support passkey.</span></span> <span data-ttu-id="b5426-111">Il tecnico del supporto dovrebbe fornire la passkey in un messaggio di posta elettronica.</span><span class="sxs-lookup"><span data-stu-id="b5426-111">Your support engineer should provide this to you in an email.</span></span>
> 
> 

<span data-ttu-id="b5426-112">Un pacchetto per il supporto crittografato e compresso (file CAB) viene creato e caricato nel sito del supporto.</span><span class="sxs-lookup"><span data-stu-id="b5426-112">An encrypted and compressed support package (.cab file) is created and uploaded to the Support site.</span></span> <span data-ttu-id="b5426-113">Il tecnico del supporto può quindi recuperare questo pacchetto dal sito del supporto per la risoluzione del problema.</span><span class="sxs-lookup"><span data-stu-id="b5426-113">The support engineer can then retrieve this package from the Support site for troubleshooting the issue.</span></span>

<span data-ttu-id="b5426-114">Eseguire i passaggi seguenti nel portale classico per creare un pacchetto per il supporto.</span><span class="sxs-lookup"><span data-stu-id="b5426-114">Perform the following steps in the classic portal to create a support package.</span></span>

#### <a name="to-create-a-support-package-in-the-azure-classic-portal"></a><span data-ttu-id="b5426-115">Creazione di un pacchetto per il supporto nel portale di Azure classico</span><span class="sxs-lookup"><span data-stu-id="b5426-115">To create a support package in the Azure classic portal</span></span>
1. <span data-ttu-id="b5426-116">Selezionare **Dispositivi** > **Manutenzione**.</span><span class="sxs-lookup"><span data-stu-id="b5426-116">Select **Devices** > **Maintenance**.</span></span>
2. <span data-ttu-id="b5426-117">Nella sezione **Pacchetto per il supporto** selezionare **Crea e carica il pacchetto per il supporto**.</span><span class="sxs-lookup"><span data-stu-id="b5426-117">In the **Support package** section, select **Create and upload support package**.</span></span>
3. <span data-ttu-id="b5426-118">Nella finestra di dialogo **Crea e carica il pacchetto per il supporto** , effettuare le operazioni seguenti:</span><span class="sxs-lookup"><span data-stu-id="b5426-118">In the **Create and upload support package** dialog box, do the following:</span></span>
   
    ![Creare un pacchetto per il supporto](./media/storsimple-create-manage-support-package/IC740923.png)
   
   * <span data-ttu-id="b5426-120">Nella casella di testo **Passkey per il supporto** immettere la passkey.</span><span class="sxs-lookup"><span data-stu-id="b5426-120">In the **Support Passkey** text box, enter the passkey.</span></span> <span data-ttu-id="b5426-121">Il tecnico del supporto Microsoft dovrebbe inviare questa passkey tramite posta elettronica.</span><span class="sxs-lookup"><span data-stu-id="b5426-121">Your Microsoft support engineer should send this passkey to you in email.</span></span>
   * <span data-ttu-id="b5426-122">Selezionare la casella di controllo per fornire il consenso al caricamento automatico del pacchetto per il supporto nel sito del supporto tecnico Microsoft.</span><span class="sxs-lookup"><span data-stu-id="b5426-122">Select the check box to provide consent to automatically upload the support package to the Microsoft Support site.</span></span>
   * <span data-ttu-id="b5426-123">Fare clic sull'icona del segno di spunta </span><span class="sxs-lookup"><span data-stu-id="b5426-123">Click the check icon</span></span> ![Icona del segno di spunta](./media/storsimple-create-manage-support-package/IC740895.png)<span data-ttu-id="b5426-125">.</span><span class="sxs-lookup"><span data-stu-id="b5426-125">.</span></span>

## <a name="manually-create-a-support-package"></a><span data-ttu-id="b5426-126">Creare manualmente un pacchetto per il supporto</span><span class="sxs-lookup"><span data-stu-id="b5426-126">Manually create a support package</span></span>
<span data-ttu-id="b5426-127">In alcuni casi, è necessario creare manualmente il pacchetto per il supporto tramite Windows PowerShell per StorSimple.</span><span class="sxs-lookup"><span data-stu-id="b5426-127">In some cases, you'll need to manually create the support package through Windows PowerShell for StorSimple.</span></span> <span data-ttu-id="b5426-128">Ad esempio:</span><span class="sxs-lookup"><span data-stu-id="b5426-128">For example:</span></span>

* <span data-ttu-id="b5426-129">Se è necessario rimuovere informazioni riservate dai file di log prima di condividerli con il supporto tecnico Microsoft.</span><span class="sxs-lookup"><span data-stu-id="b5426-129">If you need to remove sensitive information from your log files prior to sharing with Microsoft Support.</span></span>
* <span data-ttu-id="b5426-130">In caso di difficoltà nel caricare il pacchetto a causa di problemi di connettività.</span><span class="sxs-lookup"><span data-stu-id="b5426-130">If you are having difficulty uploading the package due to connectivity issues.</span></span>

<span data-ttu-id="b5426-131">È possibile condividere il pacchetto per il supporto generato manualmente con il supporto tecnico Microsoft tramite posta elettronica.</span><span class="sxs-lookup"><span data-stu-id="b5426-131">You can share your manually generated support package with Microsoft Support over email.</span></span> <span data-ttu-id="b5426-132">Per creare un pacchetto per il supporto in Windows PowerShell per StorSimple, eseguire i passaggi seguenti.</span><span class="sxs-lookup"><span data-stu-id="b5426-132">Perform the following steps to create a support package in Windows PowerShell for StorSimple.</span></span>

#### <a name="to-create-a-support-package-in-windows-powershell-for-storsimple"></a><span data-ttu-id="b5426-133">Per creare un pacchetto per il supporto in Windows PowerShell per StorSimple</span><span class="sxs-lookup"><span data-stu-id="b5426-133">To create a support package in Windows PowerShell for StorSimple</span></span>
1. <span data-ttu-id="b5426-134">Immettere il comando seguente per avviare una sessione di Windows PowerShell come amministratore nel computer remoto usato per connettersi al dispositivo StorSimple:</span><span class="sxs-lookup"><span data-stu-id="b5426-134">To start a Windows PowerShell session as an administrator on the remote computer that's used to connect to your StorSimple device, enter the following command:</span></span>
   
    `Start PowerShell`
2. <span data-ttu-id="b5426-135">Nella sessione di Windows PowerShell connettersi alla console SSAdmin del dispositivo:</span><span class="sxs-lookup"><span data-stu-id="b5426-135">In the Windows PowerShell session, connect to the SSAdmin Console of your device:</span></span>
   
   * <span data-ttu-id="b5426-136">Al prompt dei comandi immettere:</span><span class="sxs-lookup"><span data-stu-id="b5426-136">At the command prompt, enter:</span></span>
     
       `$MS = New-PSSession -ComputerName <IP address for DATA 0> -Credential SSAdmin -ConfigurationName "SSAdminConsole"`
   * <span data-ttu-id="b5426-137">Nella finestra di dialogo visualizzata immettere la password dell'amministratore del dispositivo.</span><span class="sxs-lookup"><span data-stu-id="b5426-137">In the dialog box that opens, enter your device administrator password.</span></span> <span data-ttu-id="b5426-138">La password predefinita è:</span><span class="sxs-lookup"><span data-stu-id="b5426-138">The default password is:</span></span>
     
      `Password1`
     
      ![Finestra di dialogo Credenziali PowerShell](./media/storsimple-create-manage-support-package/IC740962.png)
   * <span data-ttu-id="b5426-140">Selezionare **OK**.</span><span class="sxs-lookup"><span data-stu-id="b5426-140">Select **OK**.</span></span>
   * <span data-ttu-id="b5426-141">Al prompt dei comandi immettere:</span><span class="sxs-lookup"><span data-stu-id="b5426-141">At the command prompt, enter:</span></span>
     
      `Enter-PSSession $MS`
3. <span data-ttu-id="b5426-142">Nella sessione avviata immettere il comando appropriato.</span><span class="sxs-lookup"><span data-stu-id="b5426-142">In the session that opens, enter the appropriate command.</span></span>
   
   * <span data-ttu-id="b5426-143">Per le condivisioni di rete protette da password, immettere:</span><span class="sxs-lookup"><span data-stu-id="b5426-143">For network shares that are password protected, enter:</span></span>
     
       `Export-HcsSupportPackage –PackageTag "MySupportPackage" –Credential "Username" -Force`
     
       <span data-ttu-id="b5426-144">Verrà richiesta la password, il percorso della cartella di rete condivisa e la passphrase di crittografia (perché il pacchetto per il supporto è crittografato).</span><span class="sxs-lookup"><span data-stu-id="b5426-144">You'll be prompted for a password, a path to the network shared folder, and an encryption passphrase (because the support package is encrypted).</span></span> <span data-ttu-id="b5426-145">Viene quindi creato un pacchetto per il supporto nella cartella specificata.</span><span class="sxs-lookup"><span data-stu-id="b5426-145">A support package is then created in the specified folder.</span></span>
   * <span data-ttu-id="b5426-146">Per le condivisioni non protette da password, il parametro `-Credential` non è necessario.</span><span class="sxs-lookup"><span data-stu-id="b5426-146">For shares that are not password protected, you do not need the `-Credential` parameter.</span></span> <span data-ttu-id="b5426-147">Immettere le informazioni seguenti:</span><span class="sxs-lookup"><span data-stu-id="b5426-147">Enter the following:</span></span>
     
       `Export-HcsSupportPackage –PackageTag "MySupportPackage" -Force`
     
       <span data-ttu-id="b5426-148">Il pacchetto per il supporto viene creato per entrambi i controller nella cartella di rete condivisa specificata.</span><span class="sxs-lookup"><span data-stu-id="b5426-148">The support package is created for both controllers in the specified network shared folder.</span></span> <span data-ttu-id="b5426-149">Si tratta di un file compresso e crittografato che può essere inviato al supporto tecnico Microsoft per la risoluzione dei problemi.</span><span class="sxs-lookup"><span data-stu-id="b5426-149">It's an encrypted, compressed file that can be sent to Microsoft Support for troubleshooting.</span></span> <span data-ttu-id="b5426-150">Per ulteriori informazioni, vedere [Contattare il supporto tecnico Microsoft](storsimple-contact-microsoft-support.md).</span><span class="sxs-lookup"><span data-stu-id="b5426-150">For more information, see [Contact Microsoft Support](storsimple-contact-microsoft-support.md).</span></span>

### <a name="the-export-hcssupportpackage-cmdlet-parameters"></a><span data-ttu-id="b5426-151">Parametri del cmdlet Export-HcsSupportPackage</span><span class="sxs-lookup"><span data-stu-id="b5426-151">The Export-HcsSupportPackage cmdlet parameters</span></span>
<span data-ttu-id="b5426-152">Con il cmdlet Export-HcsSupportPackage è possibile usare i parametri seguenti.</span><span class="sxs-lookup"><span data-stu-id="b5426-152">You can use the following parameters with the Export-HcsSupportPackage cmdlet.</span></span>

| <span data-ttu-id="b5426-153">Parametro</span><span class="sxs-lookup"><span data-stu-id="b5426-153">Parameter</span></span> | <span data-ttu-id="b5426-154">Obbligatorio/Facoltativo</span><span class="sxs-lookup"><span data-stu-id="b5426-154">Required/Optional</span></span> | <span data-ttu-id="b5426-155">Description</span><span class="sxs-lookup"><span data-stu-id="b5426-155">Description</span></span> |
| --- | --- | --- |
| `-Path` |<span data-ttu-id="b5426-156">Obbligatorio</span><span class="sxs-lookup"><span data-stu-id="b5426-156">Required</span></span> |<span data-ttu-id="b5426-157">Consente di specificare il percorso della cartella di rete condivisa in cui verrà inserito il pacchetto per il supporto.</span><span class="sxs-lookup"><span data-stu-id="b5426-157">Use to provide the location of the network shared folder in which the support package is placed.</span></span> |
| `-EncryptionPassphrase` |<span data-ttu-id="b5426-158">Obbligatorio</span><span class="sxs-lookup"><span data-stu-id="b5426-158">Required</span></span> |<span data-ttu-id="b5426-159">Consente di fornire una passphrase per crittografare il pacchetto per il supporto.</span><span class="sxs-lookup"><span data-stu-id="b5426-159">Use to provide a passphrase to help encrypt the support package.</span></span> |
| `-Credential` |<span data-ttu-id="b5426-160">Facoltativo</span><span class="sxs-lookup"><span data-stu-id="b5426-160">Optional</span></span> |<span data-ttu-id="b5426-161">Consente di specificare le credenziali di accesso per la cartella di rete condivisa.</span><span class="sxs-lookup"><span data-stu-id="b5426-161">Use to supply access credentials for the network shared folder.</span></span> |
| `-Force` |<span data-ttu-id="b5426-162">Facoltativo</span><span class="sxs-lookup"><span data-stu-id="b5426-162">Optional</span></span> |<span data-ttu-id="b5426-163">Consente di ignorare il passaggio di conferma della passphrase di crittografia.</span><span class="sxs-lookup"><span data-stu-id="b5426-163">Use to skip the encryption passphrase confirmation step.</span></span> |
| `-PackageTag` |<span data-ttu-id="b5426-164">Facoltativo</span><span class="sxs-lookup"><span data-stu-id="b5426-164">Optional</span></span> |<span data-ttu-id="b5426-165">Consente di specificare una directory in cui inserire il pacchetto per il supporto in *Percorso* .</span><span class="sxs-lookup"><span data-stu-id="b5426-165">Use to specify a directory under *Path* in which the support package is placed.</span></span> <span data-ttu-id="b5426-166">Il valore predefinito è [nome dispositivo]-[data e ora correnti:aaaa-MM-gg-HH-mm-ss].</span><span class="sxs-lookup"><span data-stu-id="b5426-166">The default is [device name]-[current date and time:yyyy-MM-dd-HH-mm-ss].</span></span> |
| `-Scope` |<span data-ttu-id="b5426-167">Facoltativo</span><span class="sxs-lookup"><span data-stu-id="b5426-167">Optional</span></span> |<span data-ttu-id="b5426-168">Specificare come **Cluster** (impostazione predefinita) per creare un pacchetto per il supporto per entrambi i controller.</span><span class="sxs-lookup"><span data-stu-id="b5426-168">Specify as **Cluster** (default) to create a support package for both controllers.</span></span> <span data-ttu-id="b5426-169">Per creare un pacchetto solo per il controller corrente, specificare **Controller**.</span><span class="sxs-lookup"><span data-stu-id="b5426-169">If you want to create a package only for the current controller, specify **Controller**.</span></span> |

## <a name="edit-a-support-package"></a><span data-ttu-id="b5426-170">Modificare un pacchetto per il supporto</span><span class="sxs-lookup"><span data-stu-id="b5426-170">Edit a support package</span></span>
<span data-ttu-id="b5426-171">Dopo aver generato un pacchetto per il supporto, potrebbe essere necessario modificarlo per rimuovere le informazioni riservate.</span><span class="sxs-lookup"><span data-stu-id="b5426-171">After you have generated a support package, you might need to edit the package to remove sensitive information.</span></span> <span data-ttu-id="b5426-172">Queste informazioni possono includere i nomi dei volumi, gli indirizzi IP dei dispositivi e i nomi dei backup dai file di log.</span><span class="sxs-lookup"><span data-stu-id="b5426-172">This can include volume names, device IP addresses, and backup names from the log files.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="b5426-173">È possibile solo modificare un pacchetto per il supporto che è stato generato tramite Windows PowerShell per StorSimple.</span><span class="sxs-lookup"><span data-stu-id="b5426-173">You can only edit a support package that was generated through Windows PowerShell for StorSimple.</span></span> <span data-ttu-id="b5426-174">Non è possibile modificare un pacchetto creato nel portale di Azure classico con il servizio StorSimple Manager.</span><span class="sxs-lookup"><span data-stu-id="b5426-174">You can't edit a package created in the Azure classic portal with StorSimple Manager service.</span></span>
> 
> 

<span data-ttu-id="b5426-175">Per modificare un pacchetto per il supporto prima di caricarlo nel sito del supporto tecnico Microsoft, è necessario decrittografarlo, modificare i file e quindi crittografarlo di nuovo.</span><span class="sxs-lookup"><span data-stu-id="b5426-175">To edit a support package before uploading it on the Microsoft Support site, first decrypt the support package, edit the files, and then re-encrypt it.</span></span> <span data-ttu-id="b5426-176">Eseguire i passaggi seguenti.</span><span class="sxs-lookup"><span data-stu-id="b5426-176">Perform the following steps.</span></span>

#### <a name="to-edit-a-support-package-in-windows-powershell-for-storsimple"></a><span data-ttu-id="b5426-177">Per modificare un pacchetto per il supporto in Windows PowerShell per StorSimple</span><span class="sxs-lookup"><span data-stu-id="b5426-177">To edit a support package in Windows PowerShell for StorSimple</span></span>
1. <span data-ttu-id="b5426-178">Generare un pacchetto per il supporto come descritto prima in [Per creare un pacchetto per il supporto in Windows PowerShell per StorSimple](#to-create-a-support-package-in-windows-powershell-for-storsimple).</span><span class="sxs-lookup"><span data-stu-id="b5426-178">Generate a support package as described earlier, in [To create a support package in Windows PowerShell for StorSimple](#to-create-a-support-package-in-windows-powershell-for-storsimple).</span></span>
2. <span data-ttu-id="b5426-179">[Scaricare lo script](http://gallery.technet.microsoft.com/scriptcenter/Script-to-decrypt-a-a8d1ed65) localmente nel client.</span><span class="sxs-lookup"><span data-stu-id="b5426-179">[Download the script](http://gallery.technet.microsoft.com/scriptcenter/Script-to-decrypt-a-a8d1ed65) locally on your client.</span></span>
3. <span data-ttu-id="b5426-180">Importare il modulo Windows PowerShell.</span><span class="sxs-lookup"><span data-stu-id="b5426-180">Import the Windows PowerShell module.</span></span> <span data-ttu-id="b5426-181">Specificare il percorso della cartella locale in cui è stato scaricato lo script.</span><span class="sxs-lookup"><span data-stu-id="b5426-181">Specify the path to the local folder in which you downloaded the script.</span></span> <span data-ttu-id="b5426-182">Per importare il modulo, immettere:</span><span class="sxs-lookup"><span data-stu-id="b5426-182">To import the module, enter:</span></span>
   
    `Import-module <Path to the folder that contains the Windows PowerShell script>`
4. <span data-ttu-id="b5426-183">Tutti i file hanno l'estensione *aes* e sono compressi e crittografati.</span><span class="sxs-lookup"><span data-stu-id="b5426-183">All the files are *.aes* files that are compressed and encrypted.</span></span> <span data-ttu-id="b5426-184">Per decomprimere e decrittografare i file, immettere:</span><span class="sxs-lookup"><span data-stu-id="b5426-184">To decompress and decrypt files, enter:</span></span>
   
    `Open-HcsSupportPackage <Path to the folder that contains support package files>`
   
    <span data-ttu-id="b5426-185">Notare che per tutti i file sono ora visualizzate le estensioni effettive.</span><span class="sxs-lookup"><span data-stu-id="b5426-185">Note that the actual file extensions are now displayed for all the files.</span></span>
   
    ![Modificare il pacchetto per il supporto](./media/storsimple-create-manage-support-package/IC750706.png)
5. <span data-ttu-id="b5426-187">Quando viene chiesta la passphrase di crittografia, immettere quella usata quando è stato creato il pacchetto per il supporto.</span><span class="sxs-lookup"><span data-stu-id="b5426-187">When you're prompted for the encryption passphrase, enter the passphrase that you used when the support package was created.</span></span>
   
        cmdlet Open-HcsSupportPackage at command pipeline position 1
   
        Supply values for the following parameters:EncryptionPassphrase: ****
6. <span data-ttu-id="b5426-188">Passare alla cartella che contiene i file di log.</span><span class="sxs-lookup"><span data-stu-id="b5426-188">Browse to the folder that contains the log files.</span></span> <span data-ttu-id="b5426-189">Poiché i file di log sono ora decompressi e decrittografati, avranno le estensioni di file originali.</span><span class="sxs-lookup"><span data-stu-id="b5426-189">Because the log files are now decompressed and decrypted, these will have original file extensions.</span></span> <span data-ttu-id="b5426-190">Modificare questi file per rimuovere eventuali informazioni specifiche del cliente, ad esempio i nomi dei volumi e gli indirizzi IP dei dispositivi, e salvare i file.</span><span class="sxs-lookup"><span data-stu-id="b5426-190">Modify these files to remove any customer-specific information, such as volume names and device IP addresses, and save the files.</span></span>
7. <span data-ttu-id="b5426-191">Chiudere i file per comprimerli con GZIP e crittografarli con AES-256.</span><span class="sxs-lookup"><span data-stu-id="b5426-191">Close the files to compress them with gzip and encrypt them with AES-256.</span></span> <span data-ttu-id="b5426-192">Queste procedure assicurano velocità e sicurezza durante il trasferimento in rete del pacchetto per il supporto.</span><span class="sxs-lookup"><span data-stu-id="b5426-192">This is for speed and security in transferring the support package over a network.</span></span> <span data-ttu-id="b5426-193">Per comprimere e crittografare i file, immettere le informazioni seguenti:</span><span class="sxs-lookup"><span data-stu-id="b5426-193">To compress and encrypt files, enter the following:</span></span>
   
    `Close-HcsSupportPackage <Path to the folder that contains support package files>`
   
    ![Modificare il pacchetto per il supporto](./media/storsimple-create-manage-support-package/IC750707.png)
8. <span data-ttu-id="b5426-195">Quando richiesto, specificare una passphrase di crittografia del pacchetto per il supporto modificato.</span><span class="sxs-lookup"><span data-stu-id="b5426-195">When prompted, provide an encryption passphrase for the modified support package.</span></span>
   
        cmdlet Close-HcsSupportPackage at command pipeline position 1
        Supply values for the following parameters:EncryptionPassphrase: ****
9. <span data-ttu-id="b5426-196">Annotare la nuova passphrase in modo che sia possibile condividerla con il supporto tecnico Microsoft quando richiesto.</span><span class="sxs-lookup"><span data-stu-id="b5426-196">Write down the new passphrase, so that you can share it with Microsoft Support when requested.</span></span>

### <a name="example-editing-files-in-a-support-package-on-a-password-protected-share"></a><span data-ttu-id="b5426-197">Esempio: modifica dei file in un pacchetto per il supporto in una condivisione protetta da password</span><span class="sxs-lookup"><span data-stu-id="b5426-197">Example: Editing files in a support package on a password-protected share</span></span>
<span data-ttu-id="b5426-198">L'esempio seguente mostra come decrittografare, modificare e crittografare di nuovo un pacchetto per il supporto.</span><span class="sxs-lookup"><span data-stu-id="b5426-198">The following example shows how to decrypt, edit, and re-encrypt a support package.</span></span>

        PS C:\WINDOWS\system32> Import-module C:\Users\Default\StorSimple\SupportPackage\HCSSupportPackageTools.psm1

        PS C:\WINDOWS\system32> Open-HcsSupportPackage \\hcsfs\Logs\TD48\TD48Logs\C0-A\etw

        cmdlet Open-HcsSupportPackage at command pipeline position 1

        Supply values for the following parameters:

        EncryptionPassphrase: ****

        PS C:\WINDOWS\system32> Close-HcsSupportPackage \\hcsfs\Logs\TD48\TD48Logs\C0-A\etw

        cmdlet Close-HcsSupportPackage at command pipeline position 1

        Supply values for the following parameters:

        EncryptionPassphrase: ****

        PS C:\WINDOWS\system32>

## <a name="next-steps"></a><span data-ttu-id="b5426-199">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="b5426-199">Next steps</span></span>
* <span data-ttu-id="b5426-200">Informazioni su come [utilizzare i pacchetti per il supporto e i registri del dispositivo per risolvere i problemi di distribuzione del dispositivo](storsimple-troubleshoot-deployment.md#support-packages-and-device-logs-available-for-troubleshooting).</span><span class="sxs-lookup"><span data-stu-id="b5426-200">Learn how to [use support packages and device logs to troubleshoot your device deployment](storsimple-troubleshoot-deployment.md#support-packages-and-device-logs-available-for-troubleshooting).</span></span>
* <span data-ttu-id="b5426-201">Informazioni su come [utilizzare il servizio StorSimple Manager per amministrare il dispositivo StorSimple](storsimple-manager-service-administration.md).</span><span class="sxs-lookup"><span data-stu-id="b5426-201">Learn how to [use the StorSimple Manager service to administer your StorSimple device](storsimple-manager-service-administration.md).</span></span>


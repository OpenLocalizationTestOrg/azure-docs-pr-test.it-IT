---
title: Creare un pacchetto per il supporto StorSimple serie 8000 | Microsoft Docs
description: Informazioni su come creare, decrittografare e modificare un pacchetto per il supporto del dispositivo StorSimple serie 8000.
services: storsimple
documentationcenter: 
author: alkohli
manager: timlt
editor: 
ms.assetid: 
ms.service: storsimple
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/05/2017
ms.author: alkohli
ms.openlocfilehash: 92abbb96b2117e10800de61b5c405a784453265b
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="create-and-manage-a-support-package-for-storsimple-8000-series"></a><span data-ttu-id="9d455-103">Creare e gestire un pacchetto di supporto StorSimple serie 8000</span><span class="sxs-lookup"><span data-stu-id="9d455-103">Create and manage a support package for StorSimple 8000 series</span></span>

## <a name="overview"></a><span data-ttu-id="9d455-104">Panoramica</span><span class="sxs-lookup"><span data-stu-id="9d455-104">Overview</span></span>

<span data-ttu-id="9d455-105">Un pacchetto per il supporto StorSimple è un meccanismo semplice da usare che raccoglie tutti i log pertinenti per aiutare il supporto tecnico Microsoft a risolvere i problemi relativi ai dispositivi StorSimple.</span><span class="sxs-lookup"><span data-stu-id="9d455-105">A StorSimple support package is an easy-to-use mechanism that collects all relevant logs to assist Microsoft Support with troubleshooting any StorSimple device issues.</span></span> <span data-ttu-id="9d455-106">I log raccolti vengono crittografati e compressi.</span><span class="sxs-lookup"><span data-stu-id="9d455-106">The collected logs are encrypted and compressed.</span></span>

<span data-ttu-id="9d455-107">Questa esercitazione include istruzioni dettagliate per creare e gestire il pacchetto per il supporto per il dispositivo StorSimple serie 8000.</span><span class="sxs-lookup"><span data-stu-id="9d455-107">This tutorial includes step-by-step instructions to create and manage the support package for your StorSimple 8000 series device.</span></span> <span data-ttu-id="9d455-108">Se si lavora con un array virtuale StorSimple, passare a [generare un pacchetto di log](storsimple-ova-web-ui-admin.md#generate-a-log-package).</span><span class="sxs-lookup"><span data-stu-id="9d455-108">If you are working with a StorSimple Virtual Array, go to [generate a log package](storsimple-ova-web-ui-admin.md#generate-a-log-package).</span></span>

## <a name="create-a-support-package"></a><span data-ttu-id="9d455-109">Creare un pacchetto di supporto</span><span class="sxs-lookup"><span data-stu-id="9d455-109">Create a support package</span></span>

<span data-ttu-id="9d455-110">In alcuni casi, è necessario creare manualmente il pacchetto per il supporto tramite Windows PowerShell per StorSimple.</span><span class="sxs-lookup"><span data-stu-id="9d455-110">In some cases, you'll need to manually create the support package through Windows PowerShell for StorSimple.</span></span> <span data-ttu-id="9d455-111">Ad esempio:</span><span class="sxs-lookup"><span data-stu-id="9d455-111">For example:</span></span>

* <span data-ttu-id="9d455-112">Se è necessario rimuovere informazioni riservate dai file di log prima di condividerli con il supporto tecnico Microsoft.</span><span class="sxs-lookup"><span data-stu-id="9d455-112">If you need to remove sensitive information from your log files prior to sharing with Microsoft Support.</span></span>
* <span data-ttu-id="9d455-113">In caso di difficoltà nel caricare il pacchetto a causa di problemi di connettività.</span><span class="sxs-lookup"><span data-stu-id="9d455-113">If you are having difficulty uploading the package due to connectivity issues.</span></span>

<span data-ttu-id="9d455-114">È possibile condividere il pacchetto per il supporto generato manualmente con il supporto tecnico Microsoft tramite posta elettronica.</span><span class="sxs-lookup"><span data-stu-id="9d455-114">You can share your manually generated support package with Microsoft Support over email.</span></span> <span data-ttu-id="9d455-115">Per creare un pacchetto per il supporto in Windows PowerShell per StorSimple, eseguire i passaggi seguenti.</span><span class="sxs-lookup"><span data-stu-id="9d455-115">Perform the following steps to create a support package in Windows PowerShell for StorSimple.</span></span>

#### <a name="to-create-a-support-package-in-windows-powershell-for-storsimple"></a><span data-ttu-id="9d455-116">Per creare un pacchetto per il supporto in Windows PowerShell per StorSimple</span><span class="sxs-lookup"><span data-stu-id="9d455-116">To create a support package in Windows PowerShell for StorSimple</span></span>

1. <span data-ttu-id="9d455-117">Immettere il comando seguente per avviare una sessione di Windows PowerShell come amministratore nel computer remoto usato per connettersi al dispositivo StorSimple:</span><span class="sxs-lookup"><span data-stu-id="9d455-117">To start a Windows PowerShell session as an administrator on the remote computer that's used to connect to your StorSimple device, enter the following command:</span></span>
   
    `Start PowerShell`
2. <span data-ttu-id="9d455-118">Nella sessione di Windows PowerShell connettersi alla console SSAdmin del dispositivo:</span><span class="sxs-lookup"><span data-stu-id="9d455-118">In the Windows PowerShell session, connect to the SSAdmin Console of your device:</span></span>
   
   1. <span data-ttu-id="9d455-119">Al prompt dei comandi immettere:</span><span class="sxs-lookup"><span data-stu-id="9d455-119">At the command prompt, enter:</span></span>
     
       `$MS = New-PSSession -ComputerName <IP address for DATA 0> -Credential SSAdmin -ConfigurationName "SSAdminConsole"`
   2. <span data-ttu-id="9d455-120">Nella finestra di dialogo visualizzata immettere la password dell'amministratore del dispositivo.</span><span class="sxs-lookup"><span data-stu-id="9d455-120">In the dialog box that opens, enter your device administrator password.</span></span> <span data-ttu-id="9d455-121">La password predefinita è _Password1_.</span><span class="sxs-lookup"><span data-stu-id="9d455-121">The default password is _Password1_.</span></span>
     
      ![Finestra di dialogo Credenziali PowerShell](./media/storsimple-8000-create-manage-support-package/IC740962.png)
   3. <span data-ttu-id="9d455-123">Selezionare **OK**.</span><span class="sxs-lookup"><span data-stu-id="9d455-123">Select **OK**.</span></span>
   4. <span data-ttu-id="9d455-124">Al prompt dei comandi immettere:</span><span class="sxs-lookup"><span data-stu-id="9d455-124">At the command prompt, enter:</span></span>
     
      `Enter-PSSession $MS`
3. <span data-ttu-id="9d455-125">Nella sessione avviata immettere il comando appropriato.</span><span class="sxs-lookup"><span data-stu-id="9d455-125">In the session that opens, enter the appropriate command.</span></span>
   
   * <span data-ttu-id="9d455-126">Per le condivisioni di rete protette da password, immettere:</span><span class="sxs-lookup"><span data-stu-id="9d455-126">For network shares that are password protected, enter:</span></span>
     
       `Export-HcsSupportPackage –PackageTag "MySupportPackage" –Credential "Username" -Force`
     
       <span data-ttu-id="9d455-127">Verrà richiesta la password, il percorso della cartella di rete condivisa e la passphrase di crittografia (perché il pacchetto per il supporto è crittografato).</span><span class="sxs-lookup"><span data-stu-id="9d455-127">You'll be prompted for a password, a path to the network shared folder, and an encryption passphrase (because the support package is encrypted).</span></span> <span data-ttu-id="9d455-128">Viene quindi creato un pacchetto per il supporto nella cartella specificata.</span><span class="sxs-lookup"><span data-stu-id="9d455-128">A support package is then created in the specified folder.</span></span>
   * <span data-ttu-id="9d455-129">Per le condivisioni non protette da password, il parametro `-Credential` non è necessario.</span><span class="sxs-lookup"><span data-stu-id="9d455-129">For shares that are not password protected, you do not need the `-Credential` parameter.</span></span> <span data-ttu-id="9d455-130">Immettere le informazioni seguenti:</span><span class="sxs-lookup"><span data-stu-id="9d455-130">Enter the following:</span></span>
     
       `Export-HcsSupportPackage –PackageTag "MySupportPackage" -Force`
     
       <span data-ttu-id="9d455-131">Il pacchetto per il supporto viene creato per entrambi i controller nella cartella di rete condivisa specificata.</span><span class="sxs-lookup"><span data-stu-id="9d455-131">The support package is created for both controllers in the specified network shared folder.</span></span> <span data-ttu-id="9d455-132">Si tratta di un file compresso e crittografato che può essere inviato al supporto tecnico Microsoft per la risoluzione dei problemi.</span><span class="sxs-lookup"><span data-stu-id="9d455-132">It's an encrypted, compressed file that can be sent to Microsoft Support for troubleshooting.</span></span> <span data-ttu-id="9d455-133">Per ulteriori informazioni, vedere [Contattare il supporto tecnico Microsoft](storsimple-8000-contact-microsoft-support.md).</span><span class="sxs-lookup"><span data-stu-id="9d455-133">For more information, see [Contact Microsoft Support](storsimple-8000-contact-microsoft-support.md).</span></span>

### <a name="the-export-hcssupportpackage-cmdlet-parameters"></a><span data-ttu-id="9d455-134">Parametri del cmdlet Export-HcsSupportPackage</span><span class="sxs-lookup"><span data-stu-id="9d455-134">The Export-HcsSupportPackage cmdlet parameters</span></span>

<span data-ttu-id="9d455-135">Con il cmdlet Export-HcsSupportPackage è possibile usare i parametri seguenti.</span><span class="sxs-lookup"><span data-stu-id="9d455-135">You can use the following parameters with the Export-HcsSupportPackage cmdlet.</span></span>

| <span data-ttu-id="9d455-136">Parametro</span><span class="sxs-lookup"><span data-stu-id="9d455-136">Parameter</span></span> | <span data-ttu-id="9d455-137">Obbligatorio/Facoltativo</span><span class="sxs-lookup"><span data-stu-id="9d455-137">Required/Optional</span></span> | <span data-ttu-id="9d455-138">Description</span><span class="sxs-lookup"><span data-stu-id="9d455-138">Description</span></span> |
| --- | --- | --- |
| `-Path` |<span data-ttu-id="9d455-139">Obbligatorio</span><span class="sxs-lookup"><span data-stu-id="9d455-139">Required</span></span> |<span data-ttu-id="9d455-140">Consente di specificare il percorso della cartella di rete condivisa in cui verrà inserito il pacchetto per il supporto.</span><span class="sxs-lookup"><span data-stu-id="9d455-140">Use to provide the location of the network shared folder in which the support package is placed.</span></span> |
| `-EncryptionPassphrase` |<span data-ttu-id="9d455-141">Obbligatorio</span><span class="sxs-lookup"><span data-stu-id="9d455-141">Required</span></span> |<span data-ttu-id="9d455-142">Consente di fornire una passphrase per crittografare il pacchetto per il supporto.</span><span class="sxs-lookup"><span data-stu-id="9d455-142">Use to provide a passphrase to help encrypt the support package.</span></span> |
| `-Credential` |<span data-ttu-id="9d455-143">Facoltativo</span><span class="sxs-lookup"><span data-stu-id="9d455-143">Optional</span></span> |<span data-ttu-id="9d455-144">Consente di specificare le credenziali di accesso per la cartella di rete condivisa.</span><span class="sxs-lookup"><span data-stu-id="9d455-144">Use to supply access credentials for the network shared folder.</span></span> |
| `-Force` |<span data-ttu-id="9d455-145">Facoltativo</span><span class="sxs-lookup"><span data-stu-id="9d455-145">Optional</span></span> |<span data-ttu-id="9d455-146">Consente di ignorare il passaggio di conferma della passphrase di crittografia.</span><span class="sxs-lookup"><span data-stu-id="9d455-146">Use to skip the encryption passphrase confirmation step.</span></span> |
| `-PackageTag` |<span data-ttu-id="9d455-147">Facoltativo</span><span class="sxs-lookup"><span data-stu-id="9d455-147">Optional</span></span> |<span data-ttu-id="9d455-148">Consente di specificare una directory in cui inserire il pacchetto per il supporto in *Percorso* .</span><span class="sxs-lookup"><span data-stu-id="9d455-148">Use to specify a directory under *Path* in which the support package is placed.</span></span> <span data-ttu-id="9d455-149">Il valore predefinito è [nome dispositivo]-[data e ora correnti:aaaa-MM-gg-HH-mm-ss].</span><span class="sxs-lookup"><span data-stu-id="9d455-149">The default is [device name]-[current date and time:yyyy-MM-dd-HH-mm-ss].</span></span> |
| `-Scope` |<span data-ttu-id="9d455-150">Facoltativo</span><span class="sxs-lookup"><span data-stu-id="9d455-150">Optional</span></span> |<span data-ttu-id="9d455-151">Specificare come **Cluster** (impostazione predefinita) per creare un pacchetto per il supporto per entrambi i controller.</span><span class="sxs-lookup"><span data-stu-id="9d455-151">Specify as **Cluster** (default) to create a support package for both controllers.</span></span> <span data-ttu-id="9d455-152">Per creare un pacchetto solo per il controller corrente, specificare **Controller**.</span><span class="sxs-lookup"><span data-stu-id="9d455-152">If you want to create a package only for the current controller, specify **Controller**.</span></span> |

## <a name="edit-a-support-package"></a><span data-ttu-id="9d455-153">Modificare un pacchetto per il supporto</span><span class="sxs-lookup"><span data-stu-id="9d455-153">Edit a support package</span></span>

<span data-ttu-id="9d455-154">Dopo aver generato un pacchetto per il supporto, potrebbe essere necessario modificarlo per rimuovere le informazioni riservate.</span><span class="sxs-lookup"><span data-stu-id="9d455-154">After you have generated a support package, you might need to edit the package to remove sensitive information.</span></span> <span data-ttu-id="9d455-155">Queste informazioni possono includere i nomi dei volumi, gli indirizzi IP dei dispositivi e i nomi dei backup dai file di log.</span><span class="sxs-lookup"><span data-stu-id="9d455-155">This can include volume names, device IP addresses, and backup names from the log files.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="9d455-156">È possibile solo modificare un pacchetto per il supporto che è stato generato tramite Windows PowerShell per StorSimple.</span><span class="sxs-lookup"><span data-stu-id="9d455-156">You can only edit a support package that was generated through Windows PowerShell for StorSimple.</span></span> <span data-ttu-id="9d455-157">Non è possibile modificare un pacchetto creato nel portale di Azure con il servizio Gestione dispositivi StorSimple.</span><span class="sxs-lookup"><span data-stu-id="9d455-157">You can't edit a package created in the Azure portal with StorSimple Device Manager service.</span></span>

<span data-ttu-id="9d455-158">Per modificare un pacchetto per il supporto prima di caricarlo nel sito del supporto tecnico Microsoft, è necessario decrittografarlo, modificare i file e quindi crittografarlo di nuovo.</span><span class="sxs-lookup"><span data-stu-id="9d455-158">To edit a support package before uploading it on the Microsoft Support site, first decrypt the support package, edit the files, and then re-encrypt it.</span></span> <span data-ttu-id="9d455-159">Eseguire i passaggi seguenti.</span><span class="sxs-lookup"><span data-stu-id="9d455-159">Perform the following steps.</span></span>

#### <a name="to-edit-a-support-package-in-windows-powershell-for-storsimple"></a><span data-ttu-id="9d455-160">Per modificare un pacchetto per il supporto in Windows PowerShell per StorSimple</span><span class="sxs-lookup"><span data-stu-id="9d455-160">To edit a support package in Windows PowerShell for StorSimple</span></span>

1. <span data-ttu-id="9d455-161">Generare un pacchetto per il supporto come descritto prima in [Per creare un pacchetto per il supporto in Windows PowerShell per StorSimple](#to-create-a-support-package-in-windows-powershell-for-storsimple).</span><span class="sxs-lookup"><span data-stu-id="9d455-161">Generate a support package as described earlier, in [To create a support package in Windows PowerShell for StorSimple](#to-create-a-support-package-in-windows-powershell-for-storsimple).</span></span>
2. <span data-ttu-id="9d455-162">[Scaricare lo script](http://gallery.technet.microsoft.com/scriptcenter/Script-to-decrypt-a-a8d1ed65) localmente nel client.</span><span class="sxs-lookup"><span data-stu-id="9d455-162">[Download the script](http://gallery.technet.microsoft.com/scriptcenter/Script-to-decrypt-a-a8d1ed65) locally on your client.</span></span>
3. <span data-ttu-id="9d455-163">Importare il modulo Windows PowerShell.</span><span class="sxs-lookup"><span data-stu-id="9d455-163">Import the Windows PowerShell module.</span></span> <span data-ttu-id="9d455-164">Specificare il percorso della cartella locale in cui è stato scaricato lo script.</span><span class="sxs-lookup"><span data-stu-id="9d455-164">Specify the path to the local folder in which you downloaded the script.</span></span> <span data-ttu-id="9d455-165">Per importare il modulo, immettere:</span><span class="sxs-lookup"><span data-stu-id="9d455-165">To import the module, enter:</span></span>
   
    `Import-module <Path to the folder that contains the Windows PowerShell script>`
4. <span data-ttu-id="9d455-166">Tutti i file hanno l'estensione *aes* e sono compressi e crittografati.</span><span class="sxs-lookup"><span data-stu-id="9d455-166">All the files are *.aes* files that are compressed and encrypted.</span></span> <span data-ttu-id="9d455-167">Per decomprimere e decrittografare i file, immettere:</span><span class="sxs-lookup"><span data-stu-id="9d455-167">To decompress and decrypt files, enter:</span></span>
   
    `Open-HcsSupportPackage <Path to the folder that contains support package files>`
   
    <span data-ttu-id="9d455-168">Notare che per tutti i file sono ora visualizzate le estensioni effettive.</span><span class="sxs-lookup"><span data-stu-id="9d455-168">Note that the actual file extensions are now displayed for all the files.</span></span>
   
    ![Modificare il pacchetto per il supporto](./media/storsimple-8000-create-manage-support-package/IC750706.png)
5. <span data-ttu-id="9d455-170">Quando viene chiesta la passphrase di crittografia, immettere quella usata quando è stato creato il pacchetto per il supporto.</span><span class="sxs-lookup"><span data-stu-id="9d455-170">When you're prompted for the encryption passphrase, enter the passphrase that you used when the support package was created.</span></span>
   
        cmdlet Open-HcsSupportPackage at command pipeline position 1
   
        Supply values for the following parameters:EncryptionPassphrase: ****
6. <span data-ttu-id="9d455-171">Passare alla cartella che contiene i file di log.</span><span class="sxs-lookup"><span data-stu-id="9d455-171">Browse to the folder that contains the log files.</span></span> <span data-ttu-id="9d455-172">Poiché i file di log sono ora decompressi e decrittografati, avranno le estensioni di file originali.</span><span class="sxs-lookup"><span data-stu-id="9d455-172">Because the log files are now decompressed and decrypted, these will have original file extensions.</span></span> <span data-ttu-id="9d455-173">Modificare questi file per rimuovere eventuali informazioni specifiche del cliente, ad esempio i nomi dei volumi e gli indirizzi IP dei dispositivi, e salvare i file.</span><span class="sxs-lookup"><span data-stu-id="9d455-173">Modify these files to remove any customer-specific information, such as volume names and device IP addresses, and save the files.</span></span>
7. <span data-ttu-id="9d455-174">Chiudere i file per comprimerli con GZIP e crittografarli con AES-256.</span><span class="sxs-lookup"><span data-stu-id="9d455-174">Close the files to compress them with gzip and encrypt them with AES-256.</span></span> <span data-ttu-id="9d455-175">Queste procedure assicurano velocità e sicurezza durante il trasferimento in rete del pacchetto per il supporto.</span><span class="sxs-lookup"><span data-stu-id="9d455-175">This is for speed and security in transferring the support package over a network.</span></span> <span data-ttu-id="9d455-176">Per comprimere e crittografare i file, immettere le informazioni seguenti:</span><span class="sxs-lookup"><span data-stu-id="9d455-176">To compress and encrypt files, enter the following:</span></span>
   
    `Close-HcsSupportPackage <Path to the folder that contains support package files>`
   
    ![Modificare il pacchetto per il supporto](./media/storsimple-8000-create-manage-support-package/IC750707.png)
8. <span data-ttu-id="9d455-178">Quando richiesto, specificare una passphrase di crittografia del pacchetto per il supporto modificato.</span><span class="sxs-lookup"><span data-stu-id="9d455-178">When prompted, provide an encryption passphrase for the modified support package.</span></span>
   
        cmdlet Close-HcsSupportPackage at command pipeline position 1
        Supply values for the following parameters:EncryptionPassphrase: ****
9. <span data-ttu-id="9d455-179">Annotare la nuova passphrase in modo che sia possibile condividerla con il supporto tecnico Microsoft quando richiesto.</span><span class="sxs-lookup"><span data-stu-id="9d455-179">Write down the new passphrase, so that you can share it with Microsoft Support when requested.</span></span>

### <a name="example-editing-files-in-a-support-package-on-a-password-protected-share"></a><span data-ttu-id="9d455-180">Esempio: modifica dei file in un pacchetto per il supporto in una condivisione protetta da password</span><span class="sxs-lookup"><span data-stu-id="9d455-180">Example: Editing files in a support package on a password-protected share</span></span>

<span data-ttu-id="9d455-181">L'esempio seguente mostra come decrittografare, modificare e crittografare di nuovo un pacchetto per il supporto.</span><span class="sxs-lookup"><span data-stu-id="9d455-181">The following example shows how to decrypt, edit, and re-encrypt a support package.</span></span>

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

## <a name="next-steps"></a><span data-ttu-id="9d455-182">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="9d455-182">Next steps</span></span>

* <span data-ttu-id="9d455-183">[Informazioni raccolte nel pacchetto per il supporto](https://support.microsoft.com/help/3193606/storsimple-support-packages-and-device-logs)</span><span class="sxs-lookup"><span data-stu-id="9d455-183">Learn about the [information collected in the Support package](https://support.microsoft.com/help/3193606/storsimple-support-packages-and-device-logs)</span></span>
* <span data-ttu-id="9d455-184">Informazioni su come [utilizzare i pacchetti per il supporto e i registri del dispositivo per risolvere i problemi di distribuzione del dispositivo](storsimple-troubleshoot-deployment.md#support-packages-and-device-logs-available-for-troubleshooting).</span><span class="sxs-lookup"><span data-stu-id="9d455-184">Learn how to [use support packages and device logs to troubleshoot your device deployment](storsimple-troubleshoot-deployment.md#support-packages-and-device-logs-available-for-troubleshooting).</span></span>
* <span data-ttu-id="9d455-185">Informazioni su come [usare il servizio Gestione dispositivi StorSimple per gestire il dispositivo StorSimple](storsimple-8000-manager-service-administration.md).</span><span class="sxs-lookup"><span data-stu-id="9d455-185">Learn how to [use the StorSimple Device Manager service to administer your StorSimple device](storsimple-8000-manager-service-administration.md).</span></span>


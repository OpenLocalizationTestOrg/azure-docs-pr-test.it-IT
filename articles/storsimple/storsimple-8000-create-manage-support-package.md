---
title: pacchetto di supporto aaaCreate un StorSimple 8000 series | Documenti Microsoft
description: Informazioni su come decrittografare, toocreate e modificare un pacchetto di supporto per il dispositivo StorSimple serie 8000.
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
ms.openlocfilehash: 857555b6ba31b1527f8f00d19818ebbec6005d0e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="create-and-manage-a-support-package-for-storsimple-8000-series"></a><span data-ttu-id="997d0-103">Creare e gestire un pacchetto di supporto StorSimple serie 8000</span><span class="sxs-lookup"><span data-stu-id="997d0-103">Create and manage a support package for StorSimple 8000 series</span></span>

## <a name="overview"></a><span data-ttu-id="997d0-104">Panoramica</span><span class="sxs-lookup"><span data-stu-id="997d0-104">Overview</span></span>

<span data-ttu-id="997d0-105">Un pacchetto di supporto StorSimple è un meccanismo di facile utilizzo che raccoglie tutti i log rilevanti tooassist supporto alla risoluzione dei problemi del dispositivo StorSimple.</span><span class="sxs-lookup"><span data-stu-id="997d0-105">A StorSimple support package is an easy-to-use mechanism that collects all relevant logs tooassist Microsoft Support with troubleshooting any StorSimple device issues.</span></span> <span data-ttu-id="997d0-106">Hello registri raccolti vengono crittografati e compressi.</span><span class="sxs-lookup"><span data-stu-id="997d0-106">hello collected logs are encrypted and compressed.</span></span>

<span data-ttu-id="997d0-107">In questa esercitazione include istruzioni dettagliate toocreate e gestire il pacchetto di supporto hello per il dispositivo StorSimple serie 8000.</span><span class="sxs-lookup"><span data-stu-id="997d0-107">This tutorial includes step-by-step instructions toocreate and manage hello support package for your StorSimple 8000 series device.</span></span> <span data-ttu-id="997d0-108">Se si lavora con un Array virtuale StorSimple, andare troppo[generare un pacchetto di log](storsimple-ova-web-ui-admin.md#generate-a-log-package).</span><span class="sxs-lookup"><span data-stu-id="997d0-108">If you are working with a StorSimple Virtual Array, go too[generate a log package](storsimple-ova-web-ui-admin.md#generate-a-log-package).</span></span>

## <a name="create-a-support-package"></a><span data-ttu-id="997d0-109">Creare un pacchetto di supporto</span><span class="sxs-lookup"><span data-stu-id="997d0-109">Create a support package</span></span>

<span data-ttu-id="997d0-110">In alcuni casi, è necessario toomanually creare pacchetto di supporto hello tramite Windows PowerShell per StorSimple.</span><span class="sxs-lookup"><span data-stu-id="997d0-110">In some cases, you'll need toomanually create hello support package through Windows PowerShell for StorSimple.</span></span> <span data-ttu-id="997d0-111">ad esempio:</span><span class="sxs-lookup"><span data-stu-id="997d0-111">For example:</span></span>

* <span data-ttu-id="997d0-112">Se è necessario tooremove le informazioni riservate dal log file toosharing precedente con il supporto Microsoft.</span><span class="sxs-lookup"><span data-stu-id="997d0-112">If you need tooremove sensitive information from your log files prior toosharing with Microsoft Support.</span></span>
* <span data-ttu-id="997d0-113">Se si verificano problemi di caricamento hello pacchetto a causa di problemi di tooconnectivity.</span><span class="sxs-lookup"><span data-stu-id="997d0-113">If you are having difficulty uploading hello package due tooconnectivity issues.</span></span>

<span data-ttu-id="997d0-114">È possibile condividere il pacchetto per il supporto generato manualmente con il supporto tecnico Microsoft tramite posta elettronica.</span><span class="sxs-lookup"><span data-stu-id="997d0-114">You can share your manually generated support package with Microsoft Support over email.</span></span> <span data-ttu-id="997d0-115">Eseguire hello seguendo i passaggi toocreate un pacchetto di supporto in Windows PowerShell per StorSimple.</span><span class="sxs-lookup"><span data-stu-id="997d0-115">Perform hello following steps toocreate a support package in Windows PowerShell for StorSimple.</span></span>

#### <a name="toocreate-a-support-package-in-windows-powershell-for-storsimple"></a><span data-ttu-id="997d0-116">toocreate un pacchetto di supporto in Windows PowerShell per StorSimple</span><span class="sxs-lookup"><span data-stu-id="997d0-116">toocreate a support package in Windows PowerShell for StorSimple</span></span>

1. <span data-ttu-id="997d0-117">toostart una sessione di Windows PowerShell come amministratore nel computer remoto hello utilizzati dispositivo di StorSimple tooyour tooconnect, immettere hello comando seguente:</span><span class="sxs-lookup"><span data-stu-id="997d0-117">toostart a Windows PowerShell session as an administrator on hello remote computer that's used tooconnect tooyour StorSimple device, enter hello following command:</span></span>
   
    `Start PowerShell`
2. <span data-ttu-id="997d0-118">Nella sessione di Windows PowerShell hello, connettersi toohello SSAdmin Console del dispositivo:</span><span class="sxs-lookup"><span data-stu-id="997d0-118">In hello Windows PowerShell session, connect toohello SSAdmin Console of your device:</span></span>
   
   1. <span data-ttu-id="997d0-119">Al prompt dei comandi di hello, immettere:</span><span class="sxs-lookup"><span data-stu-id="997d0-119">At hello command prompt, enter:</span></span>
     
       `$MS = New-PSSession -ComputerName <IP address for DATA 0> -Credential SSAdmin -ConfigurationName "SSAdminConsole"`
   2. <span data-ttu-id="997d0-120">Nella finestra di dialogo di hello visualizzata, immettere la password amministratore del dispositivo.</span><span class="sxs-lookup"><span data-stu-id="997d0-120">In hello dialog box that opens, enter your device administrator password.</span></span> <span data-ttu-id="997d0-121">password predefinita Hello è _Password1_.</span><span class="sxs-lookup"><span data-stu-id="997d0-121">hello default password is _Password1_.</span></span>
     
      ![Finestra di dialogo Credenziali PowerShell](./media/storsimple-8000-create-manage-support-package/IC740962.png)
   3. <span data-ttu-id="997d0-123">Selezionare **OK**.</span><span class="sxs-lookup"><span data-stu-id="997d0-123">Select **OK**.</span></span>
   4. <span data-ttu-id="997d0-124">Al prompt dei comandi di hello, immettere:</span><span class="sxs-lookup"><span data-stu-id="997d0-124">At hello command prompt, enter:</span></span>
     
      `Enter-PSSession $MS`
3. <span data-ttu-id="997d0-125">Nella sessione hello visualizzata, immettere comando appropriato hello.</span><span class="sxs-lookup"><span data-stu-id="997d0-125">In hello session that opens, enter hello appropriate command.</span></span>
   
   * <span data-ttu-id="997d0-126">Per le condivisioni di rete protette da password, immettere:</span><span class="sxs-lookup"><span data-stu-id="997d0-126">For network shares that are password protected, enter:</span></span>
     
       `Export-HcsSupportPackage –PackageTag "MySupportPackage" –Credential "Username" -Force`
     
       <span data-ttu-id="997d0-127">Verrà richiesto per una password, una cartella condivisa di rete toohello percorso e una passphrase di crittografia (perché è crittografato il pacchetto di supporto hello).</span><span class="sxs-lookup"><span data-stu-id="997d0-127">You'll be prompted for a password, a path toohello network shared folder, and an encryption passphrase (because hello support package is encrypted).</span></span> <span data-ttu-id="997d0-128">Un pacchetto di supporto viene quindi creato nella cartella specificata hello.</span><span class="sxs-lookup"><span data-stu-id="997d0-128">A support package is then created in hello specified folder.</span></span>
   * <span data-ttu-id="997d0-129">Per le condivisioni che non sono protette da password, non è necessario hello `-Credential` parametro.</span><span class="sxs-lookup"><span data-stu-id="997d0-129">For shares that are not password protected, you do not need hello `-Credential` parameter.</span></span> <span data-ttu-id="997d0-130">Immettere hello seguente:</span><span class="sxs-lookup"><span data-stu-id="997d0-130">Enter hello following:</span></span>
     
       `Export-HcsSupportPackage –PackageTag "MySupportPackage" -Force`
     
       <span data-ttu-id="997d0-131">pacchetto di supporto Hello viene creato per entrambi i controller nella cartella condivisa di rete specificata hello.</span><span class="sxs-lookup"><span data-stu-id="997d0-131">hello support package is created for both controllers in hello specified network shared folder.</span></span> <span data-ttu-id="997d0-132">È un file compresso crittografato che può essere inviato tooMicrosoft supporto per la risoluzione dei problemi.</span><span class="sxs-lookup"><span data-stu-id="997d0-132">It's an encrypted, compressed file that can be sent tooMicrosoft Support for troubleshooting.</span></span> <span data-ttu-id="997d0-133">Per ulteriori informazioni, vedere [Contattare il supporto tecnico Microsoft](storsimple-8000-contact-microsoft-support.md).</span><span class="sxs-lookup"><span data-stu-id="997d0-133">For more information, see [Contact Microsoft Support](storsimple-8000-contact-microsoft-support.md).</span></span>

### <a name="hello-export-hcssupportpackage-cmdlet-parameters"></a><span data-ttu-id="997d0-134">parametri del cmdlet Export-HcsSupportPackage Hello</span><span class="sxs-lookup"><span data-stu-id="997d0-134">hello Export-HcsSupportPackage cmdlet parameters</span></span>

<span data-ttu-id="997d0-135">È possibile utilizzare i seguenti parametri con il cmdlet Export-HcsSupportPackage hello hello.</span><span class="sxs-lookup"><span data-stu-id="997d0-135">You can use hello following parameters with hello Export-HcsSupportPackage cmdlet.</span></span>

| <span data-ttu-id="997d0-136">.</span><span class="sxs-lookup"><span data-stu-id="997d0-136">Parameter</span></span> | <span data-ttu-id="997d0-137">Obbligatorio/Facoltativo</span><span class="sxs-lookup"><span data-stu-id="997d0-137">Required/Optional</span></span> | <span data-ttu-id="997d0-138">Description</span><span class="sxs-lookup"><span data-stu-id="997d0-138">Description</span></span> |
| --- | --- | --- |
| `-Path` |<span data-ttu-id="997d0-139">Obbligatorio</span><span class="sxs-lookup"><span data-stu-id="997d0-139">Required</span></span> |<span data-ttu-id="997d0-140">Utilizzare il percorso hello tooprovide hello cartella di rete condivisa in cui hello è inserito il pacchetto di supporto.</span><span class="sxs-lookup"><span data-stu-id="997d0-140">Use tooprovide hello location of hello network shared folder in which hello support package is placed.</span></span> |
| `-EncryptionPassphrase` |<span data-ttu-id="997d0-141">Obbligatorio</span><span class="sxs-lookup"><span data-stu-id="997d0-141">Required</span></span> |<span data-ttu-id="997d0-142">Utilizzare tooprovide toohelp una passphrase crittografare il pacchetto di supporto di hello.</span><span class="sxs-lookup"><span data-stu-id="997d0-142">Use tooprovide a passphrase toohelp encrypt hello support package.</span></span> |
| `-Credential` |<span data-ttu-id="997d0-143">Facoltativo</span><span class="sxs-lookup"><span data-stu-id="997d0-143">Optional</span></span> |<span data-ttu-id="997d0-144">Utilizzare le credenziali di accesso toosupply per la cartella di rete condivisa hello.</span><span class="sxs-lookup"><span data-stu-id="997d0-144">Use toosupply access credentials for hello network shared folder.</span></span> |
| `-Force` |<span data-ttu-id="997d0-145">Facoltativo</span><span class="sxs-lookup"><span data-stu-id="997d0-145">Optional</span></span> |<span data-ttu-id="997d0-146">Utilizzare passaggio di conferma passphrase di crittografia di tooskip hello.</span><span class="sxs-lookup"><span data-stu-id="997d0-146">Use tooskip hello encryption passphrase confirmation step.</span></span> |
| `-PackageTag` |<span data-ttu-id="997d0-147">Facoltativo</span><span class="sxs-lookup"><span data-stu-id="997d0-147">Optional</span></span> |<span data-ttu-id="997d0-148">Utilizzare una directory nella directory di toospecify *percorso* che non supporta hello è inserito il pacchetto.</span><span class="sxs-lookup"><span data-stu-id="997d0-148">Use toospecify a directory under *Path* in which hello support package is placed.</span></span> <span data-ttu-id="997d0-149">valore predefinito di Hello è [nome dispositivo]-[data corrente e data].</span><span class="sxs-lookup"><span data-stu-id="997d0-149">hello default is [device name]-[current date and time:yyyy-MM-dd-HH-mm-ss].</span></span> |
| `-Scope` |<span data-ttu-id="997d0-150">Facoltativo</span><span class="sxs-lookup"><span data-stu-id="997d0-150">Optional</span></span> |<span data-ttu-id="997d0-151">Specificare come **Cluster** toocreate (impostazione predefinita) un pacchetto di supporto per entrambi i controller.</span><span class="sxs-lookup"><span data-stu-id="997d0-151">Specify as **Cluster** (default) toocreate a support package for both controllers.</span></span> <span data-ttu-id="997d0-152">Se si desidera toocreate un pacchetto solo per il controller corrente hello, specificare **Controller**.</span><span class="sxs-lookup"><span data-stu-id="997d0-152">If you want toocreate a package only for hello current controller, specify **Controller**.</span></span> |

## <a name="edit-a-support-package"></a><span data-ttu-id="997d0-153">Modificare un pacchetto per il supporto</span><span class="sxs-lookup"><span data-stu-id="997d0-153">Edit a support package</span></span>

<span data-ttu-id="997d0-154">Dopo aver generato un pacchetto di supporto, è necessario tooedit hello pacchetto tooremove le informazioni riservate.</span><span class="sxs-lookup"><span data-stu-id="997d0-154">After you have generated a support package, you might need tooedit hello package tooremove sensitive information.</span></span> <span data-ttu-id="997d0-155">Ciò può includere i nomi dei volumi, gli indirizzi IP del dispositivo e i nomi di backup dai file di log hello.</span><span class="sxs-lookup"><span data-stu-id="997d0-155">This can include volume names, device IP addresses, and backup names from hello log files.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="997d0-156">È possibile solo modificare un pacchetto per il supporto che è stato generato tramite Windows PowerShell per StorSimple.</span><span class="sxs-lookup"><span data-stu-id="997d0-156">You can only edit a support package that was generated through Windows PowerShell for StorSimple.</span></span> <span data-ttu-id="997d0-157">È possibile modificare un pacchetto creato nel portale di Azure con il servizio di gestione di dispositivi StorSimple hello.</span><span class="sxs-lookup"><span data-stu-id="997d0-157">You can't edit a package created in hello Azure portal with StorSimple Device Manager service.</span></span>

<span data-ttu-id="997d0-158">tooedit un pacchetto di supporto prima di caricarlo sul sito del supporto Microsoft hello, innanzitutto di decrittografare il pacchetto di supporto di hello, modificare i file hello e quindi crittografarlo nuovamente.</span><span class="sxs-lookup"><span data-stu-id="997d0-158">tooedit a support package before uploading it on hello Microsoft Support site, first decrypt hello support package, edit hello files, and then re-encrypt it.</span></span> <span data-ttu-id="997d0-159">Eseguire hello alla procedura seguente.</span><span class="sxs-lookup"><span data-stu-id="997d0-159">Perform hello following steps.</span></span>

#### <a name="tooedit-a-support-package-in-windows-powershell-for-storsimple"></a><span data-ttu-id="997d0-160">tooedit un pacchetto di supporto in Windows PowerShell per StorSimple</span><span class="sxs-lookup"><span data-stu-id="997d0-160">tooedit a support package in Windows PowerShell for StorSimple</span></span>

1. <span data-ttu-id="997d0-161">Generare un pacchetto di supporto come descritto in precedenza, in [toocreate un pacchetto di supporto in Windows PowerShell per StorSimple](#to-create-a-support-package-in-windows-powershell-for-storsimple).</span><span class="sxs-lookup"><span data-stu-id="997d0-161">Generate a support package as described earlier, in [toocreate a support package in Windows PowerShell for StorSimple](#to-create-a-support-package-in-windows-powershell-for-storsimple).</span></span>
2. <span data-ttu-id="997d0-162">[Scaricare script hello](http://gallery.technet.microsoft.com/scriptcenter/Script-to-decrypt-a-a8d1ed65) localmente nel client.</span><span class="sxs-lookup"><span data-stu-id="997d0-162">[Download hello script](http://gallery.technet.microsoft.com/scriptcenter/Script-to-decrypt-a-a8d1ed65) locally on your client.</span></span>
3. <span data-ttu-id="997d0-163">Importare il modulo di Windows PowerShell hello.</span><span class="sxs-lookup"><span data-stu-id="997d0-163">Import hello Windows PowerShell module.</span></span> <span data-ttu-id="997d0-164">Specificare hello percorso toohello cartella locale in cui è stato scaricato script hello.</span><span class="sxs-lookup"><span data-stu-id="997d0-164">Specify hello path toohello local folder in which you downloaded hello script.</span></span> <span data-ttu-id="997d0-165">modulo hello tooimport, immettere:</span><span class="sxs-lookup"><span data-stu-id="997d0-165">tooimport hello module, enter:</span></span>
   
    `Import-module <Path toohello folder that contains hello Windows PowerShell script>`
4. <span data-ttu-id="997d0-166">Tutti i file hello *AES* i file vengono compressi e crittografati.</span><span class="sxs-lookup"><span data-stu-id="997d0-166">All hello files are *.aes* files that are compressed and encrypted.</span></span> <span data-ttu-id="997d0-167">toodecompress e decrittografare i file, immettere:</span><span class="sxs-lookup"><span data-stu-id="997d0-167">toodecompress and decrypt files, enter:</span></span>
   
    `Open-HcsSupportPackage <Path toohello folder that contains support package files>`
   
    <span data-ttu-id="997d0-168">Si noti che le estensioni di file effettivo hello sono ora visualizzate per tutti i file hello.</span><span class="sxs-lookup"><span data-stu-id="997d0-168">Note that hello actual file extensions are now displayed for all hello files.</span></span>
   
    ![Modificare il pacchetto per il supporto](./media/storsimple-8000-create-manage-support-package/IC750706.png)
5. <span data-ttu-id="997d0-170">Quando viene richiesta la passphrase di crittografia hello, immettere la passphrase hello utilizzato per la creazione del pacchetto di supporto hello.</span><span class="sxs-lookup"><span data-stu-id="997d0-170">When you're prompted for hello encryption passphrase, enter hello passphrase that you used when hello support package was created.</span></span>
   
        cmdlet Open-HcsSupportPackage at command pipeline position 1
   
        Supply values for hello following parameters:EncryptionPassphrase: ****
6. <span data-ttu-id="997d0-171">Sfoglia cartella toohello che contiene i file di log hello.</span><span class="sxs-lookup"><span data-stu-id="997d0-171">Browse toohello folder that contains hello log files.</span></span> <span data-ttu-id="997d0-172">Poiché il file di log di hello sono ora decompressi e decrittografato, sono estensioni di file originale.</span><span class="sxs-lookup"><span data-stu-id="997d0-172">Because hello log files are now decompressed and decrypted, these will have original file extensions.</span></span> <span data-ttu-id="997d0-173">Modificare questi tooremove file le informazioni specifiche del cliente, ad esempio i nomi dei volumi e gli indirizzi IP del dispositivo e salvare file hello.</span><span class="sxs-lookup"><span data-stu-id="997d0-173">Modify these files tooremove any customer-specific information, such as volume names and device IP addresses, and save hello files.</span></span>
7. <span data-ttu-id="997d0-174">Chiude hello file toocompress con gzip e crittografati con AES-256.</span><span class="sxs-lookup"><span data-stu-id="997d0-174">Close hello files toocompress them with gzip and encrypt them with AES-256.</span></span> <span data-ttu-id="997d0-175">Si tratta di velocità e la sicurezza in trasferimento pacchetto di supporto hello attraverso una rete.</span><span class="sxs-lookup"><span data-stu-id="997d0-175">This is for speed and security in transferring hello support package over a network.</span></span> <span data-ttu-id="997d0-176">toocompress e crittografare i file, immettere hello seguenti:</span><span class="sxs-lookup"><span data-stu-id="997d0-176">toocompress and encrypt files, enter hello following:</span></span>
   
    `Close-HcsSupportPackage <Path toohello folder that contains support package files>`
   
    ![Modificare il pacchetto per il supporto](./media/storsimple-8000-create-manage-support-package/IC750707.png)
8. <span data-ttu-id="997d0-178">Quando richiesto, fornire una passphrase di crittografia per pacchetto di supporto modificato hello.</span><span class="sxs-lookup"><span data-stu-id="997d0-178">When prompted, provide an encryption passphrase for hello modified support package.</span></span>
   
        cmdlet Close-HcsSupportPackage at command pipeline position 1
        Supply values for hello following parameters:EncryptionPassphrase: ****
9. <span data-ttu-id="997d0-179">Annotare hello nuova passphrase, in modo che è possibile condividerla con il supporto Microsoft, quando richiesto.</span><span class="sxs-lookup"><span data-stu-id="997d0-179">Write down hello new passphrase, so that you can share it with Microsoft Support when requested.</span></span>

### <a name="example-editing-files-in-a-support-package-on-a-password-protected-share"></a><span data-ttu-id="997d0-180">Esempio: modifica dei file in un pacchetto per il supporto in una condivisione protetta da password</span><span class="sxs-lookup"><span data-stu-id="997d0-180">Example: Editing files in a support package on a password-protected share</span></span>

<span data-ttu-id="997d0-181">Hello di esempio seguente viene illustrato come toodecrypt, modificare e crittografare nuovamente un pacchetto di supporto.</span><span class="sxs-lookup"><span data-stu-id="997d0-181">hello following example shows how toodecrypt, edit, and re-encrypt a support package.</span></span>

        PS C:\WINDOWS\system32> Import-module C:\Users\Default\StorSimple\SupportPackage\HCSSupportPackageTools.psm1

        PS C:\WINDOWS\system32> Open-HcsSupportPackage \\hcsfs\Logs\TD48\TD48Logs\C0-A\etw

        cmdlet Open-HcsSupportPackage at command pipeline position 1

        Supply values for hello following parameters:

        EncryptionPassphrase: ****

        PS C:\WINDOWS\system32> Close-HcsSupportPackage \\hcsfs\Logs\TD48\TD48Logs\C0-A\etw

        cmdlet Close-HcsSupportPackage at command pipeline position 1

        Supply values for hello following parameters:

        EncryptionPassphrase: ****

        PS C:\WINDOWS\system32>

## <a name="next-steps"></a><span data-ttu-id="997d0-182">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="997d0-182">Next steps</span></span>

* <span data-ttu-id="997d0-183">Informazioni su hello [le informazioni raccolte nel pacchetto di supporto hello](https://support.microsoft.com/help/3193606/storsimple-support-packages-and-device-logs)</span><span class="sxs-lookup"><span data-stu-id="997d0-183">Learn about hello [information collected in hello Support package](https://support.microsoft.com/help/3193606/storsimple-support-packages-and-device-logs)</span></span>
* <span data-ttu-id="997d0-184">Informazioni su come troppo[usare pacchetti di supporto e dispositivo registra tootroubleshoot distribuzione dispositivo](storsimple-troubleshoot-deployment.md#support-packages-and-device-logs-available-for-troubleshooting).</span><span class="sxs-lookup"><span data-stu-id="997d0-184">Learn how too[use support packages and device logs tootroubleshoot your device deployment](storsimple-troubleshoot-deployment.md#support-packages-and-device-logs-available-for-troubleshooting).</span></span>
* <span data-ttu-id="997d0-185">Informazioni su come troppo[utilizzare hello tooadminister servizio di gestione di dispositivi StorSimple dispositivo StorSimple](storsimple-8000-manager-service-administration.md).</span><span class="sxs-lookup"><span data-stu-id="997d0-185">Learn how too[use hello StorSimple Device Manager service tooadminister your StorSimple device](storsimple-8000-manager-service-administration.md).</span></span>


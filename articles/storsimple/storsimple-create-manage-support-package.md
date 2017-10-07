---
title: un pacchetto di supporto StorSimple aaaCreate | Documenti Microsoft
description: Informazioni su come decrittografare, toocreate e modificare un pacchetto di supporto per il dispositivo StorSimple.
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
ms.openlocfilehash: 209aeee50e823fd2ca96ababd1d0cf3ea9cdad53
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="create-and-manage-a-storsimple-support-package"></a><span data-ttu-id="a7613-103">Creare e gestire un pacchetto di supporto StorSimple</span><span class="sxs-lookup"><span data-stu-id="a7613-103">Create and manage a StorSimple support package</span></span>
## <a name="overview"></a><span data-ttu-id="a7613-104">Panoramica</span><span class="sxs-lookup"><span data-stu-id="a7613-104">Overview</span></span>
<span data-ttu-id="a7613-105">Un pacchetto di supporto StorSimple è un meccanismo di facile utilizzo che raccoglie tutti i log rilevanti tooassist supporto alla risoluzione dei problemi del dispositivo StorSimple.</span><span class="sxs-lookup"><span data-stu-id="a7613-105">A StorSimple support package is an easy-to-use mechanism that collects all relevant logs tooassist Microsoft Support with troubleshooting any StorSimple device issues.</span></span> <span data-ttu-id="a7613-106">Hello registri raccolti vengono crittografati e compressi.</span><span class="sxs-lookup"><span data-stu-id="a7613-106">hello collected logs are encrypted and compressed.</span></span>

<span data-ttu-id="a7613-107">In questa esercitazione include istruzioni dettagliate toocreate e gestire il pacchetto di supporto di hello.</span><span class="sxs-lookup"><span data-stu-id="a7613-107">This tutorial includes step-by-step instructions toocreate and manage hello support package.</span></span>

## <a name="create-and-upload-a-support-package-in-hello-azure-classic-portal"></a><span data-ttu-id="a7613-108">Creare e caricare un pacchetto di supporto nel portale di Azure classico hello</span><span class="sxs-lookup"><span data-stu-id="a7613-108">Create and upload a support package in hello Azure classic portal</span></span>
<span data-ttu-id="a7613-109">È possibile creare e caricare un sito del supporto Microsoft di supporto pacchetto toohello tramite hello **manutenzione** pagina del servizio hello hello portale di Azure classico.</span><span class="sxs-lookup"><span data-stu-id="a7613-109">You can create and upload a support package toohello Microsoft Support site through hello **Maintenance** page of hello service in hello Azure classic portal.</span></span>

> [!NOTE]
> <span data-ttu-id="a7613-110">caricamento di Hello richiede una passkey per il supporto.</span><span class="sxs-lookup"><span data-stu-id="a7613-110">hello upload requires a support passkey.</span></span> <span data-ttu-id="a7613-111">Il tecnico del supporto deve fornire questo tooyou tramite posta elettronica.</span><span class="sxs-lookup"><span data-stu-id="a7613-111">Your support engineer should provide this tooyou in an email.</span></span>
> 
> 

<span data-ttu-id="a7613-112">Un pacchetto di supporto crittografati e compressi (CAB) viene creato e caricato toohello sito del supporto tecnico.</span><span class="sxs-lookup"><span data-stu-id="a7613-112">An encrypted and compressed support package (.cab file) is created and uploaded toohello Support site.</span></span> <span data-ttu-id="a7613-113">quindi è stato possibile recuperare il pacchetto dal sito del supporto tecnico di hello per risolvere il problema di hello con tecnico Hello.</span><span class="sxs-lookup"><span data-stu-id="a7613-113">hello support engineer can then retrieve this package from hello Support site for troubleshooting hello issue.</span></span>

<span data-ttu-id="a7613-114">Eseguire i passaggi toocreate portale classico hello un pacchetto di supporto hello.</span><span class="sxs-lookup"><span data-stu-id="a7613-114">Perform hello following steps in hello classic portal toocreate a support package.</span></span>

#### <a name="toocreate-a-support-package-in-hello-azure-classic-portal"></a><span data-ttu-id="a7613-115">un pacchetto di supporto nel portale di Azure classico hello toocreate</span><span class="sxs-lookup"><span data-stu-id="a7613-115">toocreate a support package in hello Azure classic portal</span></span>
1. <span data-ttu-id="a7613-116">Selezionare **Dispositivi** > **Manutenzione**.</span><span class="sxs-lookup"><span data-stu-id="a7613-116">Select **Devices** > **Maintenance**.</span></span>
2. <span data-ttu-id="a7613-117">In hello **pacchetto di supporto** selezionare **pacchetto per creare e caricare il supporto**.</span><span class="sxs-lookup"><span data-stu-id="a7613-117">In hello **Support package** section, select **Create and upload support package**.</span></span>
3. <span data-ttu-id="a7613-118">In hello **pacchetto per creare e caricare il supporto** finestra di dialogo casella, hello seguenti:</span><span class="sxs-lookup"><span data-stu-id="a7613-118">In hello **Create and upload support package** dialog box, do hello following:</span></span>
   
    ![Creare un pacchetto per il supporto](./media/storsimple-create-manage-support-package/IC740923.png)
   
   * <span data-ttu-id="a7613-120">In hello **passkey per il supporto** testo immettere passkey hello.</span><span class="sxs-lookup"><span data-stu-id="a7613-120">In hello **Support Passkey** text box, enter hello passkey.</span></span> <span data-ttu-id="a7613-121">Il tecnico del supporto Microsoft deve inviare questo tooyou passkey tramite posta elettronica.</span><span class="sxs-lookup"><span data-stu-id="a7613-121">Your Microsoft support engineer should send this passkey tooyou in email.</span></span>
   * <span data-ttu-id="a7613-122">Selezionare hello casella di controllo tooprovide consenso tooautomatically caricamento hello supporto pacchetto toohello sito del supporto Microsoft.</span><span class="sxs-lookup"><span data-stu-id="a7613-122">Select hello check box tooprovide consent tooautomatically upload hello support package toohello Microsoft Support site.</span></span>
   * <span data-ttu-id="a7613-123">Fare clic sull'icona di controllo hello</span><span class="sxs-lookup"><span data-stu-id="a7613-123">Click hello check icon</span></span> ![Icona del segno di spunta](./media/storsimple-create-manage-support-package/IC740895.png)<span data-ttu-id="a7613-125">.</span><span class="sxs-lookup"><span data-stu-id="a7613-125">.</span></span>

## <a name="manually-create-a-support-package"></a><span data-ttu-id="a7613-126">Creare manualmente un pacchetto per il supporto</span><span class="sxs-lookup"><span data-stu-id="a7613-126">Manually create a support package</span></span>
<span data-ttu-id="a7613-127">In alcuni casi, è necessario toomanually creare pacchetto di supporto hello tramite Windows PowerShell per StorSimple.</span><span class="sxs-lookup"><span data-stu-id="a7613-127">In some cases, you'll need toomanually create hello support package through Windows PowerShell for StorSimple.</span></span> <span data-ttu-id="a7613-128">ad esempio:</span><span class="sxs-lookup"><span data-stu-id="a7613-128">For example:</span></span>

* <span data-ttu-id="a7613-129">Se è necessario tooremove le informazioni riservate dal log file toosharing precedente con il supporto Microsoft.</span><span class="sxs-lookup"><span data-stu-id="a7613-129">If you need tooremove sensitive information from your log files prior toosharing with Microsoft Support.</span></span>
* <span data-ttu-id="a7613-130">Se si verificano problemi di caricamento hello pacchetto a causa di problemi di tooconnectivity.</span><span class="sxs-lookup"><span data-stu-id="a7613-130">If you are having difficulty uploading hello package due tooconnectivity issues.</span></span>

<span data-ttu-id="a7613-131">È possibile condividere il pacchetto per il supporto generato manualmente con il supporto tecnico Microsoft tramite posta elettronica.</span><span class="sxs-lookup"><span data-stu-id="a7613-131">You can share your manually generated support package with Microsoft Support over email.</span></span> <span data-ttu-id="a7613-132">Eseguire hello seguendo i passaggi toocreate un pacchetto di supporto in Windows PowerShell per StorSimple.</span><span class="sxs-lookup"><span data-stu-id="a7613-132">Perform hello following steps toocreate a support package in Windows PowerShell for StorSimple.</span></span>

#### <a name="toocreate-a-support-package-in-windows-powershell-for-storsimple"></a><span data-ttu-id="a7613-133">toocreate un pacchetto di supporto in Windows PowerShell per StorSimple</span><span class="sxs-lookup"><span data-stu-id="a7613-133">toocreate a support package in Windows PowerShell for StorSimple</span></span>
1. <span data-ttu-id="a7613-134">toostart una sessione di Windows PowerShell come amministratore nel computer remoto hello utilizzati dispositivo di StorSimple tooyour tooconnect, immettere hello comando seguente:</span><span class="sxs-lookup"><span data-stu-id="a7613-134">toostart a Windows PowerShell session as an administrator on hello remote computer that's used tooconnect tooyour StorSimple device, enter hello following command:</span></span>
   
    `Start PowerShell`
2. <span data-ttu-id="a7613-135">Nella sessione di Windows PowerShell hello, connettersi toohello SSAdmin Console del dispositivo:</span><span class="sxs-lookup"><span data-stu-id="a7613-135">In hello Windows PowerShell session, connect toohello SSAdmin Console of your device:</span></span>
   
   * <span data-ttu-id="a7613-136">Al prompt dei comandi di hello, immettere:</span><span class="sxs-lookup"><span data-stu-id="a7613-136">At hello command prompt, enter:</span></span>
     
       `$MS = New-PSSession -ComputerName <IP address for DATA 0> -Credential SSAdmin -ConfigurationName "SSAdminConsole"`
   * <span data-ttu-id="a7613-137">Nella finestra di dialogo di hello visualizzata, immettere la password amministratore del dispositivo.</span><span class="sxs-lookup"><span data-stu-id="a7613-137">In hello dialog box that opens, enter your device administrator password.</span></span> <span data-ttu-id="a7613-138">password predefinita Hello è:</span><span class="sxs-lookup"><span data-stu-id="a7613-138">hello default password is:</span></span>
     
      `Password1`
     
      ![Finestra di dialogo Credenziali PowerShell](./media/storsimple-create-manage-support-package/IC740962.png)
   * <span data-ttu-id="a7613-140">Selezionare **OK**.</span><span class="sxs-lookup"><span data-stu-id="a7613-140">Select **OK**.</span></span>
   * <span data-ttu-id="a7613-141">Al prompt dei comandi di hello, immettere:</span><span class="sxs-lookup"><span data-stu-id="a7613-141">At hello command prompt, enter:</span></span>
     
      `Enter-PSSession $MS`
3. <span data-ttu-id="a7613-142">Nella sessione hello visualizzata, immettere comando appropriato hello.</span><span class="sxs-lookup"><span data-stu-id="a7613-142">In hello session that opens, enter hello appropriate command.</span></span>
   
   * <span data-ttu-id="a7613-143">Per le condivisioni di rete protette da password, immettere:</span><span class="sxs-lookup"><span data-stu-id="a7613-143">For network shares that are password protected, enter:</span></span>
     
       `Export-HcsSupportPackage –PackageTag "MySupportPackage" –Credential "Username" -Force`
     
       <span data-ttu-id="a7613-144">Verrà richiesto per una password, una cartella condivisa di rete toohello percorso e una passphrase di crittografia (perché è crittografato il pacchetto di supporto hello).</span><span class="sxs-lookup"><span data-stu-id="a7613-144">You'll be prompted for a password, a path toohello network shared folder, and an encryption passphrase (because hello support package is encrypted).</span></span> <span data-ttu-id="a7613-145">Un pacchetto di supporto viene quindi creato nella cartella specificata hello.</span><span class="sxs-lookup"><span data-stu-id="a7613-145">A support package is then created in hello specified folder.</span></span>
   * <span data-ttu-id="a7613-146">Per le condivisioni che non sono protette da password, non è necessario hello `-Credential` parametro.</span><span class="sxs-lookup"><span data-stu-id="a7613-146">For shares that are not password protected, you do not need hello `-Credential` parameter.</span></span> <span data-ttu-id="a7613-147">Immettere hello seguente:</span><span class="sxs-lookup"><span data-stu-id="a7613-147">Enter hello following:</span></span>
     
       `Export-HcsSupportPackage –PackageTag "MySupportPackage" -Force`
     
       <span data-ttu-id="a7613-148">pacchetto di supporto Hello viene creato per entrambi i controller nella cartella condivisa di rete specificata hello.</span><span class="sxs-lookup"><span data-stu-id="a7613-148">hello support package is created for both controllers in hello specified network shared folder.</span></span> <span data-ttu-id="a7613-149">È un file compresso crittografato che può essere inviato tooMicrosoft supporto per la risoluzione dei problemi.</span><span class="sxs-lookup"><span data-stu-id="a7613-149">It's an encrypted, compressed file that can be sent tooMicrosoft Support for troubleshooting.</span></span> <span data-ttu-id="a7613-150">Per ulteriori informazioni, vedere [Contattare il supporto tecnico Microsoft](storsimple-contact-microsoft-support.md).</span><span class="sxs-lookup"><span data-stu-id="a7613-150">For more information, see [Contact Microsoft Support](storsimple-contact-microsoft-support.md).</span></span>

### <a name="hello-export-hcssupportpackage-cmdlet-parameters"></a><span data-ttu-id="a7613-151">parametri del cmdlet Export-HcsSupportPackage Hello</span><span class="sxs-lookup"><span data-stu-id="a7613-151">hello Export-HcsSupportPackage cmdlet parameters</span></span>
<span data-ttu-id="a7613-152">È possibile utilizzare i seguenti parametri con il cmdlet Export-HcsSupportPackage hello hello.</span><span class="sxs-lookup"><span data-stu-id="a7613-152">You can use hello following parameters with hello Export-HcsSupportPackage cmdlet.</span></span>

| <span data-ttu-id="a7613-153">.</span><span class="sxs-lookup"><span data-stu-id="a7613-153">Parameter</span></span> | <span data-ttu-id="a7613-154">Obbligatorio/Facoltativo</span><span class="sxs-lookup"><span data-stu-id="a7613-154">Required/Optional</span></span> | <span data-ttu-id="a7613-155">Description</span><span class="sxs-lookup"><span data-stu-id="a7613-155">Description</span></span> |
| --- | --- | --- |
| `-Path` |<span data-ttu-id="a7613-156">Obbligatorio</span><span class="sxs-lookup"><span data-stu-id="a7613-156">Required</span></span> |<span data-ttu-id="a7613-157">Utilizzare il percorso hello tooprovide hello cartella di rete condivisa in cui hello è inserito il pacchetto di supporto.</span><span class="sxs-lookup"><span data-stu-id="a7613-157">Use tooprovide hello location of hello network shared folder in which hello support package is placed.</span></span> |
| `-EncryptionPassphrase` |<span data-ttu-id="a7613-158">Obbligatorio</span><span class="sxs-lookup"><span data-stu-id="a7613-158">Required</span></span> |<span data-ttu-id="a7613-159">Utilizzare tooprovide toohelp una passphrase crittografare il pacchetto di supporto di hello.</span><span class="sxs-lookup"><span data-stu-id="a7613-159">Use tooprovide a passphrase toohelp encrypt hello support package.</span></span> |
| `-Credential` |<span data-ttu-id="a7613-160">Facoltativo</span><span class="sxs-lookup"><span data-stu-id="a7613-160">Optional</span></span> |<span data-ttu-id="a7613-161">Utilizzare le credenziali di accesso toosupply per la cartella di rete condivisa hello.</span><span class="sxs-lookup"><span data-stu-id="a7613-161">Use toosupply access credentials for hello network shared folder.</span></span> |
| `-Force` |<span data-ttu-id="a7613-162">Facoltativo</span><span class="sxs-lookup"><span data-stu-id="a7613-162">Optional</span></span> |<span data-ttu-id="a7613-163">Utilizzare passaggio di conferma passphrase di crittografia di tooskip hello.</span><span class="sxs-lookup"><span data-stu-id="a7613-163">Use tooskip hello encryption passphrase confirmation step.</span></span> |
| `-PackageTag` |<span data-ttu-id="a7613-164">Facoltativo</span><span class="sxs-lookup"><span data-stu-id="a7613-164">Optional</span></span> |<span data-ttu-id="a7613-165">Utilizzare una directory nella directory di toospecify *percorso* che non supporta hello è inserito il pacchetto.</span><span class="sxs-lookup"><span data-stu-id="a7613-165">Use toospecify a directory under *Path* in which hello support package is placed.</span></span> <span data-ttu-id="a7613-166">valore predefinito di Hello è [nome dispositivo]-[data corrente e data].</span><span class="sxs-lookup"><span data-stu-id="a7613-166">hello default is [device name]-[current date and time:yyyy-MM-dd-HH-mm-ss].</span></span> |
| `-Scope` |<span data-ttu-id="a7613-167">Facoltativo</span><span class="sxs-lookup"><span data-stu-id="a7613-167">Optional</span></span> |<span data-ttu-id="a7613-168">Specificare come **Cluster** toocreate (impostazione predefinita) un pacchetto di supporto per entrambi i controller.</span><span class="sxs-lookup"><span data-stu-id="a7613-168">Specify as **Cluster** (default) toocreate a support package for both controllers.</span></span> <span data-ttu-id="a7613-169">Se si desidera toocreate un pacchetto solo per il controller corrente hello, specificare **Controller**.</span><span class="sxs-lookup"><span data-stu-id="a7613-169">If you want toocreate a package only for hello current controller, specify **Controller**.</span></span> |

## <a name="edit-a-support-package"></a><span data-ttu-id="a7613-170">Modificare un pacchetto per il supporto</span><span class="sxs-lookup"><span data-stu-id="a7613-170">Edit a support package</span></span>
<span data-ttu-id="a7613-171">Dopo aver generato un pacchetto di supporto, è necessario tooedit hello pacchetto tooremove le informazioni riservate.</span><span class="sxs-lookup"><span data-stu-id="a7613-171">After you have generated a support package, you might need tooedit hello package tooremove sensitive information.</span></span> <span data-ttu-id="a7613-172">Ciò può includere i nomi dei volumi, gli indirizzi IP del dispositivo e i nomi di backup dai file di log hello.</span><span class="sxs-lookup"><span data-stu-id="a7613-172">This can include volume names, device IP addresses, and backup names from hello log files.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="a7613-173">È possibile solo modificare un pacchetto per il supporto che è stato generato tramite Windows PowerShell per StorSimple.</span><span class="sxs-lookup"><span data-stu-id="a7613-173">You can only edit a support package that was generated through Windows PowerShell for StorSimple.</span></span> <span data-ttu-id="a7613-174">È possibile modificare un pacchetto creato nel portale di Azure classico con il servizio StorSimple Manager hello.</span><span class="sxs-lookup"><span data-stu-id="a7613-174">You can't edit a package created in hello Azure classic portal with StorSimple Manager service.</span></span>
> 
> 

<span data-ttu-id="a7613-175">tooedit un pacchetto di supporto prima di caricarlo sul sito del supporto Microsoft hello, innanzitutto di decrittografare il pacchetto di supporto di hello, modificare i file hello e quindi crittografarlo nuovamente.</span><span class="sxs-lookup"><span data-stu-id="a7613-175">tooedit a support package before uploading it on hello Microsoft Support site, first decrypt hello support package, edit hello files, and then re-encrypt it.</span></span> <span data-ttu-id="a7613-176">Eseguire hello alla procedura seguente.</span><span class="sxs-lookup"><span data-stu-id="a7613-176">Perform hello following steps.</span></span>

#### <a name="tooedit-a-support-package-in-windows-powershell-for-storsimple"></a><span data-ttu-id="a7613-177">tooedit un pacchetto di supporto in Windows PowerShell per StorSimple</span><span class="sxs-lookup"><span data-stu-id="a7613-177">tooedit a support package in Windows PowerShell for StorSimple</span></span>
1. <span data-ttu-id="a7613-178">Generare un pacchetto di supporto come descritto in precedenza, in [toocreate un pacchetto di supporto in Windows PowerShell per StorSimple](#to-create-a-support-package-in-windows-powershell-for-storsimple).</span><span class="sxs-lookup"><span data-stu-id="a7613-178">Generate a support package as described earlier, in [toocreate a support package in Windows PowerShell for StorSimple](#to-create-a-support-package-in-windows-powershell-for-storsimple).</span></span>
2. <span data-ttu-id="a7613-179">[Scaricare script hello](http://gallery.technet.microsoft.com/scriptcenter/Script-to-decrypt-a-a8d1ed65) localmente nel client.</span><span class="sxs-lookup"><span data-stu-id="a7613-179">[Download hello script](http://gallery.technet.microsoft.com/scriptcenter/Script-to-decrypt-a-a8d1ed65) locally on your client.</span></span>
3. <span data-ttu-id="a7613-180">Importare il modulo di Windows PowerShell hello.</span><span class="sxs-lookup"><span data-stu-id="a7613-180">Import hello Windows PowerShell module.</span></span> <span data-ttu-id="a7613-181">Specificare hello percorso toohello cartella locale in cui è stato scaricato script hello.</span><span class="sxs-lookup"><span data-stu-id="a7613-181">Specify hello path toohello local folder in which you downloaded hello script.</span></span> <span data-ttu-id="a7613-182">modulo hello tooimport, immettere:</span><span class="sxs-lookup"><span data-stu-id="a7613-182">tooimport hello module, enter:</span></span>
   
    `Import-module <Path toohello folder that contains hello Windows PowerShell script>`
4. <span data-ttu-id="a7613-183">Tutti i file hello *AES* i file vengono compressi e crittografati.</span><span class="sxs-lookup"><span data-stu-id="a7613-183">All hello files are *.aes* files that are compressed and encrypted.</span></span> <span data-ttu-id="a7613-184">toodecompress e decrittografare i file, immettere:</span><span class="sxs-lookup"><span data-stu-id="a7613-184">toodecompress and decrypt files, enter:</span></span>
   
    `Open-HcsSupportPackage <Path toohello folder that contains support package files>`
   
    <span data-ttu-id="a7613-185">Si noti che le estensioni di file effettivo hello sono ora visualizzate per tutti i file hello.</span><span class="sxs-lookup"><span data-stu-id="a7613-185">Note that hello actual file extensions are now displayed for all hello files.</span></span>
   
    ![Modificare il pacchetto per il supporto](./media/storsimple-create-manage-support-package/IC750706.png)
5. <span data-ttu-id="a7613-187">Quando viene richiesta la passphrase di crittografia hello, immettere la passphrase hello utilizzato per la creazione del pacchetto di supporto hello.</span><span class="sxs-lookup"><span data-stu-id="a7613-187">When you're prompted for hello encryption passphrase, enter hello passphrase that you used when hello support package was created.</span></span>
   
        cmdlet Open-HcsSupportPackage at command pipeline position 1
   
        Supply values for hello following parameters:EncryptionPassphrase: ****
6. <span data-ttu-id="a7613-188">Sfoglia cartella toohello che contiene i file di log hello.</span><span class="sxs-lookup"><span data-stu-id="a7613-188">Browse toohello folder that contains hello log files.</span></span> <span data-ttu-id="a7613-189">Poiché il file di log di hello sono ora decompressi e decrittografato, sono estensioni di file originale.</span><span class="sxs-lookup"><span data-stu-id="a7613-189">Because hello log files are now decompressed and decrypted, these will have original file extensions.</span></span> <span data-ttu-id="a7613-190">Modificare questi tooremove file le informazioni specifiche del cliente, ad esempio i nomi dei volumi e gli indirizzi IP del dispositivo e salvare file hello.</span><span class="sxs-lookup"><span data-stu-id="a7613-190">Modify these files tooremove any customer-specific information, such as volume names and device IP addresses, and save hello files.</span></span>
7. <span data-ttu-id="a7613-191">Chiude hello file toocompress con gzip e crittografati con AES-256.</span><span class="sxs-lookup"><span data-stu-id="a7613-191">Close hello files toocompress them with gzip and encrypt them with AES-256.</span></span> <span data-ttu-id="a7613-192">Si tratta di velocità e la sicurezza in trasferimento pacchetto di supporto hello attraverso una rete.</span><span class="sxs-lookup"><span data-stu-id="a7613-192">This is for speed and security in transferring hello support package over a network.</span></span> <span data-ttu-id="a7613-193">toocompress e crittografare i file, immettere hello seguenti:</span><span class="sxs-lookup"><span data-stu-id="a7613-193">toocompress and encrypt files, enter hello following:</span></span>
   
    `Close-HcsSupportPackage <Path toohello folder that contains support package files>`
   
    ![Modificare il pacchetto per il supporto](./media/storsimple-create-manage-support-package/IC750707.png)
8. <span data-ttu-id="a7613-195">Quando richiesto, fornire una passphrase di crittografia per pacchetto di supporto modificato hello.</span><span class="sxs-lookup"><span data-stu-id="a7613-195">When prompted, provide an encryption passphrase for hello modified support package.</span></span>
   
        cmdlet Close-HcsSupportPackage at command pipeline position 1
        Supply values for hello following parameters:EncryptionPassphrase: ****
9. <span data-ttu-id="a7613-196">Annotare hello nuova passphrase, in modo che è possibile condividerla con il supporto Microsoft, quando richiesto.</span><span class="sxs-lookup"><span data-stu-id="a7613-196">Write down hello new passphrase, so that you can share it with Microsoft Support when requested.</span></span>

### <a name="example-editing-files-in-a-support-package-on-a-password-protected-share"></a><span data-ttu-id="a7613-197">Esempio: modifica dei file in un pacchetto per il supporto in una condivisione protetta da password</span><span class="sxs-lookup"><span data-stu-id="a7613-197">Example: Editing files in a support package on a password-protected share</span></span>
<span data-ttu-id="a7613-198">Hello di esempio seguente viene illustrato come toodecrypt, modificare e crittografare nuovamente un pacchetto di supporto.</span><span class="sxs-lookup"><span data-stu-id="a7613-198">hello following example shows how toodecrypt, edit, and re-encrypt a support package.</span></span>

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

## <a name="next-steps"></a><span data-ttu-id="a7613-199">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="a7613-199">Next steps</span></span>
* <span data-ttu-id="a7613-200">Informazioni su come troppo[usare pacchetti di supporto e dispositivo registra tootroubleshoot distribuzione dispositivo](storsimple-troubleshoot-deployment.md#support-packages-and-device-logs-available-for-troubleshooting).</span><span class="sxs-lookup"><span data-stu-id="a7613-200">Learn how too[use support packages and device logs tootroubleshoot your device deployment](storsimple-troubleshoot-deployment.md#support-packages-and-device-logs-available-for-troubleshooting).</span></span>
* <span data-ttu-id="a7613-201">Informazioni su come troppo[utilizzare hello tooadminister servizio StorSimple Manager dispositivo StorSimple](storsimple-manager-service-administration.md).</span><span class="sxs-lookup"><span data-stu-id="a7613-201">Learn how too[use hello StorSimple Manager service tooadminister your StorSimple device](storsimple-manager-service-administration.md).</span></span>


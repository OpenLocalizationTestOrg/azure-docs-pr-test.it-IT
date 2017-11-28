---
title: aaaBack dei server VMware con Server di Backup di Azure | Documenti Microsoft
description: Utilizzare Server di Backup di Azure tooback backup un disco o VMware server vCenter/ESXi tooAzure. Questo articolo offre istruzioni dettagliate per il backup o la protezione dei carichi di lavoro VMware.
services: backup
documentationcenter: 
author: markgalioto
manager: carmonm
ms.assetid: 6b131caf-de85-4eba-b8e6-d8a04545cd9d
ms.service: backup
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: storage-backup-recovery
ms.date: 07/24/2017
ms.author: markgal;
ms.openlocfilehash: 3edb6880a526ed0b18605fee0fac27196a608e7a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="back-up-a-vmware-server-tooazure"></a><span data-ttu-id="d09c8-104">Eseguire il backup di un tooAzure server VMware</span><span class="sxs-lookup"><span data-stu-id="d09c8-104">Back up a VMware server tooAzure</span></span>

<span data-ttu-id="d09c8-105">Questo articolo viene illustrato come proteggere i carichi di lavoro server VMware tooconfigure toohelp di Server di Backup di Azure.</span><span class="sxs-lookup"><span data-stu-id="d09c8-105">This article explains how tooconfigure Azure Backup Server toohelp protect VMware server workloads.</span></span> <span data-ttu-id="d09c8-106">In questo articolo si presuppone che sia stato già installato il server di Backup di Azure.</span><span class="sxs-lookup"><span data-stu-id="d09c8-106">This article assumes you already have Azure Backup Server installed.</span></span> <span data-ttu-id="d09c8-107">Se non è installato Azure Backup Server, vedere [preparare tooback dei carichi di lavoro tramite il Server di Backup di Azure](backup-azure-microsoft-azure-backup.md).</span><span class="sxs-lookup"><span data-stu-id="d09c8-107">If you don't have Azure Backup Server installed, see [Prepare tooback up workloads using Azure Backup Server](backup-azure-microsoft-azure-backup.md).</span></span>

<span data-ttu-id="d09c8-108">Il server di Backup di Azure può eseguire il backup o assicurare la protezione di server VMware vCenter versione 6.5, 6.0 e 5.5.</span><span class="sxs-lookup"><span data-stu-id="d09c8-108">Azure Backup Server can back up, or help protect, VMware vCenter Server version 6.5, 6.0 and 5.5.</span></span>


## <a name="create-a-secure-connection-toohello-vcenter-server"></a><span data-ttu-id="d09c8-109">Creare una connessione sicura toohello vCenter Server</span><span class="sxs-lookup"><span data-stu-id="d09c8-109">Create a secure connection toohello vCenter Server</span></span>

<span data-ttu-id="d09c8-110">Per impostazione predefinita, il server di Backup di Azure comunica con ognuno dei server vCenter tramite un canale HTTPS.</span><span class="sxs-lookup"><span data-stu-id="d09c8-110">By default, Azure Backup Server communicates with each vCenter Server via an HTTPS channel.</span></span> <span data-ttu-id="d09c8-111">tooturn sulla comunicazione sicura hello, è consigliabile installare hello VMware autorità di certificazione certificato nel Server di Backup di Azure.</span><span class="sxs-lookup"><span data-stu-id="d09c8-111">tooturn on hello secure communication, we recommend that you install hello VMware Certificate Authority (CA) certificate on Azure Backup Server.</span></span> <span data-ttu-id="d09c8-112">Se si non richieda una comunicazione protetta e si preferisce requisito di toodisable hello HTTPS, vedere [protocollo di comunicazione protetta Disable](backup-azure-backup-server-vmware.md#disable-secure-communication-protocol).</span><span class="sxs-lookup"><span data-stu-id="d09c8-112">If you don't require secure communication, and would prefer toodisable hello HTTPS requirement, see [Disable secure communication protocol](backup-azure-backup-server-vmware.md#disable-secure-communication-protocol).</span></span> <span data-ttu-id="d09c8-113">toocreate una connessione sicura tra il Server di Backup di Azure e hello vCenter Server, importarlo hello attendibile nel Server di Backup di Azure.</span><span class="sxs-lookup"><span data-stu-id="d09c8-113">toocreate a secure connection between Azure Backup Server and hello vCenter Server, import hello trusted certificate on Azure Backup Server.</span></span>

<span data-ttu-id="d09c8-114">In genere, si utilizza un browser hello Azure Backup Server macchina tooconnect toohello Server vCenter tramite vSphere hello Client Web.</span><span class="sxs-lookup"><span data-stu-id="d09c8-114">Typically, you use a browser on hello Azure Backup Server machine tooconnect toohello vCenter Server via hello vSphere Web Client.</span></span> <span data-ttu-id="d09c8-115">Hello prima volta che si utilizza hello Azure Backup Server browser tooconnect toohello vCenter Server, hello connessione non protetta.</span><span class="sxs-lookup"><span data-stu-id="d09c8-115">hello first time you use hello Azure Backup Server browser tooconnect toohello vCenter Server, hello connection isn't secure.</span></span> <span data-ttu-id="d09c8-116">Hello seguente immagine Mostra connessione hello non protetta.</span><span class="sxs-lookup"><span data-stu-id="d09c8-116">hello following image shows hello unsecured connection.</span></span>

![Esempio di connessione non protetta tooVMware server](./media/backup-azure-backup-server-vmware/unsecure-url.png)

<span data-ttu-id="d09c8-118">toofix questo problema, creare una connessione sicura e scaricare i certificati CA radice attendibile hello.</span><span class="sxs-lookup"><span data-stu-id="d09c8-118">toofix this issue, and create a secure connection, download hello trusted root CA certificates.</span></span>

1. <span data-ttu-id="d09c8-119">Nel browser hello nel Server di Backup di Azure, immettere hello URL toohello vSphere Client Web.</span><span class="sxs-lookup"><span data-stu-id="d09c8-119">In hello browser on Azure Backup Server, enter hello URL toohello vSphere Web Client.</span></span> <span data-ttu-id="d09c8-120">verrà visualizzata la pagina di accesso di Hello vSphere Client Web.</span><span class="sxs-lookup"><span data-stu-id="d09c8-120">hello vSphere Web Client login page appears.</span></span>

    ![Client Web vSphere](./media/backup-azure-backup-server-vmware/vsphere-web-client.png)

    <span data-ttu-id="d09c8-122">Nella parte inferiore di hello informazioni hello ad amministratori e sviluppatori, individuare hello **Download attendibili i certificati CA radice** collegamento.</span><span class="sxs-lookup"><span data-stu-id="d09c8-122">At hello bottom of hello information for administrators and developers, locate hello **Download trusted root CA certificates** link.</span></span>

    ![Certificati CA radice attendibile hello toodownload di collegamento](./media/backup-azure-backup-server-vmware/vmware-download-ca-cert-prompt.png)

  <span data-ttu-id="d09c8-124">Se non viene visualizzato nella pagina account di accesso Client di Web vSphere hello, controllare le impostazioni proxy del browser.</span><span class="sxs-lookup"><span data-stu-id="d09c8-124">If you don't see hello vSphere Web Client login page, check your browser's proxy settings.</span></span>

2. <span data-ttu-id="d09c8-125">Fare clic su **Scarica certificati CA radice attendibili**.</span><span class="sxs-lookup"><span data-stu-id="d09c8-125">Click **Download trusted root CA certificates**.</span></span>

    <span data-ttu-id="d09c8-126">Server vCenter Hello scarica un computer locale tooyour di file.</span><span class="sxs-lookup"><span data-stu-id="d09c8-126">hello vCenter Server downloads a file tooyour local computer.</span></span> <span data-ttu-id="d09c8-127">Hello nome del file è denominato **scaricare**.</span><span class="sxs-lookup"><span data-stu-id="d09c8-127">hello file's name is named **download**.</span></span> <span data-ttu-id="d09c8-128">A seconda del browser, viene visualizzato un messaggio che chiede se tooopen o salvare il file hello.</span><span class="sxs-lookup"><span data-stu-id="d09c8-128">Depending on your browser, you receive a message that asks whether tooopen or save hello file.</span></span>

    ![messaggio di download quando vengono scaricati i certificati](./media/backup-azure-backup-server-vmware/download-certs.png)

3. <span data-ttu-id="d09c8-130">Hello file tooa percorso di salvataggio nel Server di Backup di Azure.</span><span class="sxs-lookup"><span data-stu-id="d09c8-130">Save hello file tooa location on Azure Backup Server.</span></span> <span data-ttu-id="d09c8-131">Quando si salva il file hello, aggiungere l'estensione di file con estensione zip hello.</span><span class="sxs-lookup"><span data-stu-id="d09c8-131">When you save hello file, add hello .zip file name extension.</span></span>

    <span data-ttu-id="d09c8-132">file Hello è un file con estensione zip che contiene informazioni di hello sui certificati hello.</span><span class="sxs-lookup"><span data-stu-id="d09c8-132">hello file is a .zip file that contains hello information about hello certificates.</span></span> <span data-ttu-id="d09c8-133">Con estensione zip hello, è possibile utilizzare gli strumenti di estrazione hello.</span><span class="sxs-lookup"><span data-stu-id="d09c8-133">With hello .zip extension, you can use hello extraction tools.</span></span>

4. <span data-ttu-id="d09c8-134">Fare doppio clic su **download.zip**, quindi selezionare **Estrai tutto** contenuto hello tooextract.</span><span class="sxs-lookup"><span data-stu-id="d09c8-134">Right-click **download.zip**, and then select **Extract All** tooextract hello contents.</span></span>

    <span data-ttu-id="d09c8-135">file con estensione zip Hello estrae il relativo contenuto tooa cartella **certificati**.</span><span class="sxs-lookup"><span data-stu-id="d09c8-135">hello .zip file extracts its contents tooa folder named **certs**.</span></span> <span data-ttu-id="d09c8-136">Due tipi di file vengono visualizzati nella cartella certificati hello.</span><span class="sxs-lookup"><span data-stu-id="d09c8-136">Two types of files appear in hello certs folder.</span></span> <span data-ttu-id="d09c8-137">file del certificato radice Hello ha un'estensione che inizia con una sequenza numerata come,0 e. 1.</span><span class="sxs-lookup"><span data-stu-id="d09c8-137">hello root certificate file has an extension that begins with a numbered sequence like .0 and .1.</span></span>
    
    <span data-ttu-id="d09c8-138">file CRL Hello ha un'estensione che inizia con una sequenza come .r0 o .r1.</span><span class="sxs-lookup"><span data-stu-id="d09c8-138">hello CRL file has an extension that begins with a sequence like .r0 or .r1.</span></span> <span data-ttu-id="d09c8-139">file CRL Hello è associata a un certificato.</span><span class="sxs-lookup"><span data-stu-id="d09c8-139">hello CRL file is associated with a certificate.</span></span>

    ![<span data-ttu-id="d09c8-140">File di download estratto localmente</span><span class="sxs-lookup"><span data-stu-id="d09c8-140">Download file extracted locally</span></span> ](./media/backup-azure-backup-server-vmware/extracted-files-in-certs-folder.png)

5. <span data-ttu-id="d09c8-141">In hello **certificati** cartella, fare clic sul file di certificato radice hello e quindi fare clic su **rinominare**.</span><span class="sxs-lookup"><span data-stu-id="d09c8-141">In hello **certs** folder, right-click hello root certificate file, and then click **Rename**.</span></span>

    ![<span data-ttu-id="d09c8-142">Ridenominazione del certificato radice</span><span class="sxs-lookup"><span data-stu-id="d09c8-142">Rename root certificate</span></span> ](./media/backup-azure-backup-server-vmware/rename-cert.png)

    <span data-ttu-id="d09c8-143">Modifica estensione too.crt del certificato radice hello.</span><span class="sxs-lookup"><span data-stu-id="d09c8-143">Change hello root certificate's extension too.crt.</span></span> <span data-ttu-id="d09c8-144">Quando viene richiesto se si è certi che si desidera toochange hello estensione, fare clic su **Sì** o **OK**.</span><span class="sxs-lookup"><span data-stu-id="d09c8-144">When you're asked if you're sure you want toochange hello extension, click **Yes** or **OK**.</span></span> <span data-ttu-id="d09c8-145">In caso contrario, modificare la funzione prevista del file hello.</span><span class="sxs-lookup"><span data-stu-id="d09c8-145">Otherwise, you change hello file's intended function.</span></span> <span data-ttu-id="d09c8-146">icona di Hello per hello file modifiche tooan icona rappresenta un certificato radice.</span><span class="sxs-lookup"><span data-stu-id="d09c8-146">hello icon for hello file changes tooan icon that represents a root certificate.</span></span>

6. <span data-ttu-id="d09c8-147">Fare doppio clic su certificato radice hello e scegliere dal menu a comparsa hello **Installa certificato**.</span><span class="sxs-lookup"><span data-stu-id="d09c8-147">Right-click hello root certificate and from hello pop-up menu, select **Install Certificate**.</span></span>

    <span data-ttu-id="d09c8-148">Hello **importazione guidata certificati** viene visualizzata la finestra di dialogo.</span><span class="sxs-lookup"><span data-stu-id="d09c8-148">hello **Certificate Import Wizard** dialog box appears.</span></span>

7. <span data-ttu-id="d09c8-149">In hello **importazione guidata certificati** nella finestra di dialogo **computer locale** come destinazione di hello per hello certificato e quindi fare clic su **Avanti** toocontinue.</span><span class="sxs-lookup"><span data-stu-id="d09c8-149">In hello **Certificate Import Wizard** dialog box, select **Local Machine** as hello destination for hello certificate, and then click **Next** toocontinue.</span></span>

    ![<span data-ttu-id="d09c8-150">Opzioni di destinazione di archiviazione del certificato</span><span class="sxs-lookup"><span data-stu-id="d09c8-150">Certificate storage destination options</span></span> ](./media/backup-azure-backup-server-vmware/certificate-import-wizard1.png)

    <span data-ttu-id="d09c8-151">Se viene chiesto se si desidera di tooallow modifiche toohello computer, fare clic su **Sì** o **OK**, le modifiche di hello tooall.</span><span class="sxs-lookup"><span data-stu-id="d09c8-151">If you're asked if you want tooallow changes toohello computer, click **Yes** or **OK**, tooall hello changes.</span></span>

8. <span data-ttu-id="d09c8-152">In hello **archivio certificati** selezionare **colloca tutti i certificati nel seguente archivio hello**, quindi fare clic su **Sfoglia** archivio certificati di hello toochoose.</span><span class="sxs-lookup"><span data-stu-id="d09c8-152">On hello **Certificate Store** page, select **Place all certificates in hello following store**, and then click **Browse** toochoose hello certificate store.</span></span>

    ![Inserire i certificati in un punto di archiviazione specifico](./media/backup-azure-backup-server-vmware/cert-import-wizard-local-store.png)

    <span data-ttu-id="d09c8-154">Hello **Selezione archivio certificati** viene visualizzata la finestra di dialogo.</span><span class="sxs-lookup"><span data-stu-id="d09c8-154">hello **Select Certificate Store** dialog box appears.</span></span>

    ![Gerarchia di cartelle di archiviazione di certificati](./media/backup-azure-backup-server-vmware/cert-store.png)

9. <span data-ttu-id="d09c8-156">Selezionare **autorità di certificazione radice attendibili** come cartella di destinazione hello per certificati hello e quindi fare clic su **OK**.</span><span class="sxs-lookup"><span data-stu-id="d09c8-156">Select **Trusted Root Certification Authorities** as hello destination folder for hello certificates, and then click **OK**.</span></span>

    ![Cartella di destinazione dei certificati](./media/backup-azure-backup-server-vmware/certificate-store-selected.png)

    <span data-ttu-id="d09c8-158">Hello **autorità di certificazione radice attendibili** cartella viene confermata come archivio di certificati hello.</span><span class="sxs-lookup"><span data-stu-id="d09c8-158">hello **Trusted Root Certification Authorities** folder is confirmed as hello certificate store.</span></span> <span data-ttu-id="d09c8-159">Fare clic su **Avanti**.</span><span class="sxs-lookup"><span data-stu-id="d09c8-159">Click **Next**.</span></span>

    ![Cartella archivio certificati](./media/backup-azure-backup-server-vmware/certificate-import-wizard2.png)

10. <span data-ttu-id="d09c8-161">In hello **hello Completamento importazione guidata certificati** pagina, verificare che il certificato hello nella cartella desiderata hello e quindi fare clic su **fine**.</span><span class="sxs-lookup"><span data-stu-id="d09c8-161">On hello **Completing hello Certificate Import Wizard** page, verify that hello certificate is in hello desired folder, and then click **Finish**.</span></span>

    ![Verificare i certificati si trova nella cartella corretta di hello](./media/backup-azure-backup-server-vmware/cert-wizard-final-screen.png)

    <span data-ttu-id="d09c8-163">Viene visualizzata una finestra di dialogo, viene confermata l'importazione del certificato ha esito positivo hello.</span><span class="sxs-lookup"><span data-stu-id="d09c8-163">A dialog box appears, hello successful certificate import is confirmed.</span></span>

11. <span data-ttu-id="d09c8-164">Accedi toohello vCenter Server tooconfirm che la connessione è protetta.</span><span class="sxs-lookup"><span data-stu-id="d09c8-164">Sign in toohello vCenter Server tooconfirm that your connection is secure.</span></span>

  <span data-ttu-id="d09c8-165">Importazione certificati hello non ha esito positivo, se non è possibile stabilire una connessione sicura, consultare la documentazione di vSphere VMware hello in [richiesta di certificati server](http://pubs.vmware.com/vsphere-60/index.jsp#com.vmware.wssdk.dsg.doc/sdk_sg_server_certificate_Appendixes.6.4.html).</span><span class="sxs-lookup"><span data-stu-id="d09c8-165">If hello certificate import is not successful, and you cannot establish a secure connection, consult hello VMware vSphere documentation on [obtaining server certificates](http://pubs.vmware.com/vsphere-60/index.jsp#com.vmware.wssdk.dsg.doc/sdk_sg_server_certificate_Appendixes.6.4.html).</span></span>

  <span data-ttu-id="d09c8-166">Se si hanno limiti protetti all'interno dell'organizzazione e non desidera tooturn su hello il protocollo HTTPS, è possibile utilizzare hello seguendo procedure toodisable hello proteggere le comunicazioni.</span><span class="sxs-lookup"><span data-stu-id="d09c8-166">If you have secure boundaries within your organization, and don't want tooturn on hello HTTPS protocol, use hello following procedure toodisable hello secure communications.</span></span>

### <a name="disable-secure-communication-protocol"></a><span data-ttu-id="d09c8-167">Disabilitazione del protocollo di comunicazione sicura</span><span class="sxs-lookup"><span data-stu-id="d09c8-167">Disable secure communication protocol</span></span>

<span data-ttu-id="d09c8-168">Se l'organizzazione non richiede il protocollo HTTPS hello, utilizzare hello seguendo i passaggi toodisable HTTPS.</span><span class="sxs-lookup"><span data-stu-id="d09c8-168">If your organization doesn't require hello HTTPS protocol, use hello following steps toodisable HTTPS.</span></span> <span data-ttu-id="d09c8-169">toodisable hello comportamento predefinito, creare una chiave del Registro di sistema che ignora il comportamento predefinito di hello.</span><span class="sxs-lookup"><span data-stu-id="d09c8-169">toodisable hello default behavior, create a registry key that ignores hello default behavior.</span></span>

1. <span data-ttu-id="d09c8-170">Copiare e incollare hello dopo il testo in un file con estensione txt.</span><span class="sxs-lookup"><span data-stu-id="d09c8-170">Copy and paste hello following text into a .txt file.</span></span>

  ```
  Windows Registry Editor Version 5.00
  [HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Microsoft Data Protection Manager\VMWare]
  "IgnoreCertificateValidation"=dword:00000001
  ```

2. <span data-ttu-id="d09c8-171">Salvare i computer del Server di Backup di Azure tooyour file hello.</span><span class="sxs-lookup"><span data-stu-id="d09c8-171">Save hello file tooyour Azure Backup Server computer.</span></span> <span data-ttu-id="d09c8-172">Utilizzare DisableSecureAuthentication.reg per nome file hello.</span><span class="sxs-lookup"><span data-stu-id="d09c8-172">For hello file name, use DisableSecureAuthentication.reg.</span></span>

3. <span data-ttu-id="d09c8-173">Fare doppio clic sulla voce del Registro di sistema hello tooactivate file hello.</span><span class="sxs-lookup"><span data-stu-id="d09c8-173">Double-click hello file tooactivate hello registry entry.</span></span>


## <a name="create-a-role-and-user-account-on-hello-vcenter-server"></a><span data-ttu-id="d09c8-174">Creare un account utente e ruoli Server vCenter hello</span><span class="sxs-lookup"><span data-stu-id="d09c8-174">Create a role and user account on hello vCenter Server</span></span>

<span data-ttu-id="d09c8-175">Hello vCenter Server, un ruolo è un set predefinito di privilegi.</span><span class="sxs-lookup"><span data-stu-id="d09c8-175">On hello vCenter Server, a role is a predefined set of privileges.</span></span> <span data-ttu-id="d09c8-176">Un amministratore del Server vCenter Crea ruoli hello.</span><span class="sxs-lookup"><span data-stu-id="d09c8-176">A vCenter Server administrator creates hello roles.</span></span> <span data-ttu-id="d09c8-177">autorizzazioni tooassign, amministratore hello coppie gli account utente con un ruolo.</span><span class="sxs-lookup"><span data-stu-id="d09c8-177">tooassign permissions, hello administrator pairs user accounts with a role.</span></span> <span data-ttu-id="d09c8-178">tooestablish hello utente necessari credenziali tooback dei computer del Server vCenter hello, creare un ruolo con privilegi specifici e quindi associare account utente di hello hello ruolo.</span><span class="sxs-lookup"><span data-stu-id="d09c8-178">tooestablish hello necessary user credentials tooback up hello vCenter Server computer, create a role with specific privileges, and then associate hello user account with hello role.</span></span>

<span data-ttu-id="d09c8-179">Server di Backup di Azure Usa tooauthenticate un nome utente e password con hello vCenter Server.</span><span class="sxs-lookup"><span data-stu-id="d09c8-179">Azure Backup Server uses a username and password tooauthenticate with hello vCenter Server.</span></span> <span data-ttu-id="d09c8-180">Il server di Backup di Azure sfrutta tali credenziali come autenticazione per ogni operazione di backup.</span><span class="sxs-lookup"><span data-stu-id="d09c8-180">Azure Backup Server uses these credentials as authentication for all backup operations.</span></span>

<span data-ttu-id="d09c8-181">tooadd un ruolo del Server vCenter e i relativi privilegi di amministratore di backup:</span><span class="sxs-lookup"><span data-stu-id="d09c8-181">tooadd a vCenter Server role and its privileges for a backup administrator:</span></span>

1. <span data-ttu-id="d09c8-182">Eseguire l'accesso in toohello vCenter Server e quindi nel Server vCenter hello **Navigator** pannello, fare clic su **amministrazione**.</span><span class="sxs-lookup"><span data-stu-id="d09c8-182">Sign in toohello vCenter Server, and then in hello vCenter Server **Navigator** panel, click **Administration**.</span></span>

    ![Opzione Administration (Amministrazione) nel pannello Navigator (Strumento di navigazione) del server vCenter](./media/backup-azure-backup-server-vmware/vmware-navigator-panel.png)

2. <span data-ttu-id="d09c8-184">In **amministrazione** selezionare **ruoli**e quindi in hello **ruoli** fare clic su Pannello hello aggiungere l'icona del ruolo (simbolo + hello).</span><span class="sxs-lookup"><span data-stu-id="d09c8-184">In **Administration** select **Roles**, and then in hello **Roles** panel click hello add role icon (hello + symbol).</span></span>

    ![Aggiungi ruolo](./media/backup-azure-backup-server-vmware/vmware-define-new-role.png)

    <span data-ttu-id="d09c8-186">Hello **Create Role** viene visualizzata la finestra di dialogo.</span><span class="sxs-lookup"><span data-stu-id="d09c8-186">hello **Create Role** dialog box appears.</span></span>

    ![Create role (Crea ruolo)](./media/backup-azure-backup-server-vmware/vmware-define-new-role-priv.png)

3. <span data-ttu-id="d09c8-188">In hello **Create Role** della finestra di dialogo hello **nome ruolo** immettere *BackupAdminRole*.</span><span class="sxs-lookup"><span data-stu-id="d09c8-188">In hello **Create Role** dialog box, in hello **Role name** box, enter *BackupAdminRole*.</span></span> <span data-ttu-id="d09c8-189">nome del ruolo Hello può essere scelto liberamente, ma deve essere riconoscibile per scopo del ruolo hello.</span><span class="sxs-lookup"><span data-stu-id="d09c8-189">hello role name can be whatever you like, but it should be recognizable for hello role's purpose.</span></span>

4. <span data-ttu-id="d09c8-190">Selezionare hello privilegi per la versione appropriata di hello di vCenter e quindi fare clic su **OK**.</span><span class="sxs-lookup"><span data-stu-id="d09c8-190">Select hello privileges for hello appropriate version of vCenter, and then click **OK**.</span></span> <span data-ttu-id="d09c8-191">Hello nella tabella seguente identifica i privilegi necessario hello per vCenter 6.0 e vCenter 5.5.</span><span class="sxs-lookup"><span data-stu-id="d09c8-191">hello following table identifies hello required privileges for vCenter 6.0 and vCenter 5.5.</span></span>

  <span data-ttu-id="d09c8-192">Quando si selezionano privilegi hello, fare clic su hello icona Avanti toohello padre etichetta tooexpand hello padre vista hello figlio privilegi di amministratore.</span><span class="sxs-lookup"><span data-stu-id="d09c8-192">When you select hello privileges, click hello icon next toohello parent label tooexpand hello parent and view hello child privileges.</span></span> <span data-ttu-id="d09c8-193">privilegi di VirtualMachine tooselect hello, è necessario toogo vari livelli in hello relazione gerarchica.</span><span class="sxs-lookup"><span data-stu-id="d09c8-193">tooselect hello VirtualMachine privileges, you need toogo several levels into hello parent child hierarchy.</span></span> <span data-ttu-id="d09c8-194">Non è necessario tooselect tutti i privilegi figlio all'interno di un privilegio padre.</span><span class="sxs-lookup"><span data-stu-id="d09c8-194">You don't need tooselect all child privileges within a parent privilege.</span></span>

  ![Gerarchia di privilegi padre-figlio](./media/backup-azure-backup-server-vmware/cert-add-privilege-expand.png)

  <span data-ttu-id="d09c8-196">Dopo aver fatto clic **OK**, hello nuovo ruolo viene visualizzato nell'elenco di hello sul pannello ruoli hello.</span><span class="sxs-lookup"><span data-stu-id="d09c8-196">After you click **OK**, hello new role appears in hello list on hello Roles panel.</span></span>

|<span data-ttu-id="d09c8-197">Privilegi per vCenter 6.0</span><span class="sxs-lookup"><span data-stu-id="d09c8-197">Privileges for vCenter 6.0</span></span>| <span data-ttu-id="d09c8-198">Privilegi per vCenter 5.5</span><span class="sxs-lookup"><span data-stu-id="d09c8-198">Privileges for vCenter 5.5</span></span>|
|--------------------------|---------------------------|
|<span data-ttu-id="d09c8-199">Datastore.AllocateSpace</span><span class="sxs-lookup"><span data-stu-id="d09c8-199">Datastore.AllocateSpace</span></span>   | <span data-ttu-id="d09c8-200">Datastore.AllocateSpace</span><span class="sxs-lookup"><span data-stu-id="d09c8-200">Datastore.AllocateSpace</span></span>|
|<span data-ttu-id="d09c8-201">Global.ManageCustomFields</span><span class="sxs-lookup"><span data-stu-id="d09c8-201">Global.ManageCustomFields</span></span> | <span data-ttu-id="d09c8-202">Global.ManageCustomerFields</span><span class="sxs-lookup"><span data-stu-id="d09c8-202">Global.ManageCustomerFields</span></span>|
|<span data-ttu-id="d09c8-203">Global.SetCustomFields</span><span class="sxs-lookup"><span data-stu-id="d09c8-203">Global.SetCustomFields</span></span>    |   |
|<span data-ttu-id="d09c8-204">Host.Local.CreateVM</span><span class="sxs-lookup"><span data-stu-id="d09c8-204">Host.Local.CreateVM</span></span>       | <span data-ttu-id="d09c8-205">Network.Assign</span><span class="sxs-lookup"><span data-stu-id="d09c8-205">Network.Assign</span></span> |
|<span data-ttu-id="d09c8-206">Network.Assign</span><span class="sxs-lookup"><span data-stu-id="d09c8-206">Network.Assign</span></span>            |  |
|<span data-ttu-id="d09c8-207">Resource.AssignVMToPool</span><span class="sxs-lookup"><span data-stu-id="d09c8-207">Resource.AssignVMToPool</span></span>   |  |
|<span data-ttu-id="d09c8-208">VirtualMachine.Config.AddNewDisk</span><span class="sxs-lookup"><span data-stu-id="d09c8-208">VirtualMachine.Config.AddNewDisk</span></span>  | <span data-ttu-id="d09c8-209">VirtualMachine.Config.AddNewDisk</span><span class="sxs-lookup"><span data-stu-id="d09c8-209">VirtualMachine.Config.AddNewDisk</span></span>   |
|<span data-ttu-id="d09c8-210">VirtualMachine.Config.AdvanceConfig</span><span class="sxs-lookup"><span data-stu-id="d09c8-210">VirtualMachine.Config.AdvanceConfig</span></span>| <span data-ttu-id="d09c8-211">VirtualMachine.Config.AdvancedConfig</span><span class="sxs-lookup"><span data-stu-id="d09c8-211">VirtualMachine.Config.AdvancedConfig</span></span>|
|<span data-ttu-id="d09c8-212">VirtualMachine.Config.ChangeTracking</span><span class="sxs-lookup"><span data-stu-id="d09c8-212">VirtualMachine.Config.ChangeTracking</span></span>| <span data-ttu-id="d09c8-213">VirtualMachine.Config.ChangeTracking</span><span class="sxs-lookup"><span data-stu-id="d09c8-213">VirtualMachine.Config.ChangeTracking</span></span> |
|<span data-ttu-id="d09c8-214">VirtualMachine.Config.HostUSBDevice</span><span class="sxs-lookup"><span data-stu-id="d09c8-214">VirtualMachine.Config.HostUSBDevice</span></span>||
|<span data-ttu-id="d09c8-215">VirtualMachine.Config.QueryUnownedFiles</span><span class="sxs-lookup"><span data-stu-id="d09c8-215">VirtualMachine.Config.QueryUnownedFiles</span></span>|    |
|<span data-ttu-id="d09c8-216">VirtualMachine.Config.SwapPlacement</span><span class="sxs-lookup"><span data-stu-id="d09c8-216">VirtualMachine.Config.SwapPlacement</span></span>| <span data-ttu-id="d09c8-217">VirtualMachine.Config.SwapPlacement</span><span class="sxs-lookup"><span data-stu-id="d09c8-217">VirtualMachine.Config.SwapPlacement</span></span> |
|<span data-ttu-id="d09c8-218">VirtualMachine.Interact.PowerOff</span><span class="sxs-lookup"><span data-stu-id="d09c8-218">VirtualMachine.Interact.PowerOff</span></span>| <span data-ttu-id="d09c8-219">VirtualMachine.Interact.PowerOff</span><span class="sxs-lookup"><span data-stu-id="d09c8-219">VirtualMachine.Interact.PowerOff</span></span> |
|<span data-ttu-id="d09c8-220">VirtualMachine.Inventory.Create</span><span class="sxs-lookup"><span data-stu-id="d09c8-220">VirtualMachine.Inventory.Create</span></span>| <span data-ttu-id="d09c8-221">VirtualMachine.Inventory.Create</span><span class="sxs-lookup"><span data-stu-id="d09c8-221">VirtualMachine.Inventory.Create</span></span> |
|<span data-ttu-id="d09c8-222">VirtualMachine.Provisioning.DiskRandomAccess</span><span class="sxs-lookup"><span data-stu-id="d09c8-222">VirtualMachine.Provisioning.DiskRandomAccess</span></span>| |
|<span data-ttu-id="d09c8-223">VirtualMachine.Provisioning.DiskRandomRead</span><span class="sxs-lookup"><span data-stu-id="d09c8-223">VirtualMachine.Provisioning.DiskRandomRead</span></span>|<span data-ttu-id="d09c8-224">VirtualMachine.Provisioning.DiskRandomRead</span><span class="sxs-lookup"><span data-stu-id="d09c8-224">VirtualMachine.Provisioning.DiskRandomRead</span></span> |
|<span data-ttu-id="d09c8-225">VirtualMachine.State.CreateSnapshot</span><span class="sxs-lookup"><span data-stu-id="d09c8-225">VirtualMachine.State.CreateSnapshot</span></span>| <span data-ttu-id="d09c8-226">VirtualMachine.State.CreateSnapshot</span><span class="sxs-lookup"><span data-stu-id="d09c8-226">VirtualMachine.State.CreateSnapshot</span></span>|
|<span data-ttu-id="d09c8-227">VirtualMachine.State.RemoveSnapshot</span><span class="sxs-lookup"><span data-stu-id="d09c8-227">VirtualMachine.State.RemoveSnapshot</span></span>|<span data-ttu-id="d09c8-228">VirtualMachine.State.RemoveSnapshot</span><span class="sxs-lookup"><span data-stu-id="d09c8-228">VirtualMachine.State.RemoveSnapshot</span></span> |
</br>



## <a name="create-a-vcenter-server-user-account-and-permissions"></a><span data-ttu-id="d09c8-229">Creare un account utente del server vCenter e le relative autorizzazioni</span><span class="sxs-lookup"><span data-stu-id="d09c8-229">Create a vCenter Server user account and permissions</span></span>

<span data-ttu-id="d09c8-230">Una volta hello ruolo con privilegi è configurato, creare un account utente.</span><span class="sxs-lookup"><span data-stu-id="d09c8-230">After hello role with privileges is set up, create a user account.</span></span> <span data-ttu-id="d09c8-231">account utente di Hello ha un nome e una password, che fornisce le credenziali hello vengono utilizzate per l'autenticazione.</span><span class="sxs-lookup"><span data-stu-id="d09c8-231">hello user account has a name and password, which provides hello credentials that are used for authentication.</span></span>

1. <span data-ttu-id="d09c8-232">un account utente, nel Server vCenter hello toocreate **Navigator** pannello, fare clic su **utenti e gruppi**.</span><span class="sxs-lookup"><span data-stu-id="d09c8-232">toocreate a user account, in hello vCenter Server **Navigator** panel, click **Users and Groups**.</span></span>

    ![Opzione Users and Groups (Utenti e gruppi)](./media/backup-azure-backup-server-vmware/vmware-userandgroup-panel.png)

    <span data-ttu-id="d09c8-234">Hello **vCenter utenti e gruppi** pannello viene visualizzato.</span><span class="sxs-lookup"><span data-stu-id="d09c8-234">hello **vCenter Users and Groups** panel appears.</span></span>

    ![Pannello vCenter Users and Groups (Utenti e gruppi di vCenter)](./media/backup-azure-backup-server-vmware/usersandgroups.png)

2. <span data-ttu-id="d09c8-236">In hello **vCenter utenti e gruppi** pannello, seleziona hello **utenti** scheda e quindi fare clic su hello aggiungere utenti icona (simbolo + hello).</span><span class="sxs-lookup"><span data-stu-id="d09c8-236">In hello **vCenter Users and Groups** panel, select hello **Users** tab, and then click hello add users icon (hello + symbol).</span></span>

    <span data-ttu-id="d09c8-237">Hello **nuovo utente** viene visualizzata la finestra di dialogo.</span><span class="sxs-lookup"><span data-stu-id="d09c8-237">hello **New User** dialog box appears.</span></span>

3. <span data-ttu-id="d09c8-238">In hello **nuovo utente** finestra di dialogo, aggiungere le informazioni dell'utente hello e quindi scegliere **OK**.</span><span class="sxs-lookup"><span data-stu-id="d09c8-238">In hello **New User** dialog box, add hello user's information and then click **OK**.</span></span> <span data-ttu-id="d09c8-239">In questa procedura, nome utente di hello è BackupAdmin.</span><span class="sxs-lookup"><span data-stu-id="d09c8-239">In this procedure, hello username is BackupAdmin.</span></span>

    ![Finestra di dialogo New User (Nuovo utente)](./media/backup-azure-backup-server-vmware/vmware-new-user-account.png)

    <span data-ttu-id="d09c8-241">nuovo account utente di Hello viene visualizzato nell'elenco di hello.</span><span class="sxs-lookup"><span data-stu-id="d09c8-241">hello new user account appears in hello list.</span></span>

4. <span data-ttu-id="d09c8-242">account utente di hello tooassociate con ruolo hello in hello **Navigator** pannello, fare clic su **autorizzazioni globali**.</span><span class="sxs-lookup"><span data-stu-id="d09c8-242">tooassociate hello user account with hello role, in hello **Navigator** panel, click **Global Permissions**.</span></span> <span data-ttu-id="d09c8-243">In hello **autorizzazioni globali** pannello, seleziona hello **Gestisci** scheda e quindi fare clic su hello aggiungere icona (simbolo + hello).</span><span class="sxs-lookup"><span data-stu-id="d09c8-243">In hello **Global Permissions** panel, select hello **Manage** tab, and then click hello add icon (hello + symbol).</span></span>

    ![Pannello Global Permissions (Autorizzazioni globali)](./media/backup-azure-backup-server-vmware/vmware-add-new-perms.png)

    <span data-ttu-id="d09c8-245">Hello **globale autorizzazioni Root - Aggiungi autorizzazione** viene visualizzata la finestra di dialogo.</span><span class="sxs-lookup"><span data-stu-id="d09c8-245">hello **Global Permissions Root - Add Permission** dialog box appears.</span></span>

5. <span data-ttu-id="d09c8-246">In hello **radice autorizzazione globale - Aggiungi autorizzazione** la finestra di dialogo, fare clic su **Aggiungi** toochoose hello utente o gruppo.</span><span class="sxs-lookup"><span data-stu-id="d09c8-246">In hello **Global Permission Root - Add Permission** dialog box, click **Add** toochoose hello user or group.</span></span>

    ![Scegliere un utente o un gruppo](./media/backup-azure-backup-server-vmware/vmware-add-new-global-perm.png)

    <span data-ttu-id="d09c8-248">Hello **selezionare utenti/gruppi** viene visualizzata la finestra di dialogo.</span><span class="sxs-lookup"><span data-stu-id="d09c8-248">hello **Select Users/Groups** dialog box appears.</span></span>

6. <span data-ttu-id="d09c8-249">In hello **selezionare utenti/gruppi** finestra di dialogo scegliere **BackupAdmin** e quindi fare clic su **Aggiungi**.</span><span class="sxs-lookup"><span data-stu-id="d09c8-249">In hello **Select Users/Groups** dialog box, choose **BackupAdmin** and then click **Add**.</span></span>

    <span data-ttu-id="d09c8-250">In **utenti**, hello *dominio omeutente* formato viene utilizzato per l'account utente di hello.</span><span class="sxs-lookup"><span data-stu-id="d09c8-250">In **Users**, hello *domain\username* format is used for hello user account.</span></span> <span data-ttu-id="d09c8-251">Se si desidera toouse un dominio diverso, sceglierlo dall'hello **dominio** elenco.</span><span class="sxs-lookup"><span data-stu-id="d09c8-251">If you want toouse a different domain, choose it from hello **Domain** list.</span></span>

    ![Aggiungere l'utente BackupAdmin](./media/backup-azure-backup-server-vmware/vmware-assign-account-to-role.png)

    <span data-ttu-id="d09c8-253">Fare clic su **OK** tooadd hello selezionato utenti toohello **Aggiungi autorizzazione** la finestra di dialogo.</span><span class="sxs-lookup"><span data-stu-id="d09c8-253">Click **OK** tooadd hello selected users toohello **Add Permission** dialog box.</span></span>

7. <span data-ttu-id="d09c8-254">Dopo aver identificato utente hello, assegnazione del ruolo di toohello utente hello.</span><span class="sxs-lookup"><span data-stu-id="d09c8-254">Now that you've identified hello user, assign hello user toohello role.</span></span> <span data-ttu-id="d09c8-255">In **ruolo assegnato**, dall'elenco a discesa hello, selezionare **BackupAdminRole**, quindi fare clic su **OK**.</span><span class="sxs-lookup"><span data-stu-id="d09c8-255">In **Assigned Role**, from hello drop-down list, select **BackupAdminRole**, and then click **OK**.</span></span>

    ![Assegnare l'utente toorole](./media/backup-azure-backup-server-vmware/vmware-choose-role.png)

  <span data-ttu-id="d09c8-257">In hello **Gestisci** scheda hello **autorizzazioni globali** pannello, nuovo account utente di hello e ruolo hello associato vengono visualizzati nell'elenco di hello.</span><span class="sxs-lookup"><span data-stu-id="d09c8-257">On hello **Manage** tab in hello **Global Permissions** panel, hello new user account and hello associated role appear in hello list.</span></span>


## <a name="establish-vcenter-server-credentials-on-azure-backup-server"></a><span data-ttu-id="d09c8-258">Definizione di credenziali del server vCenter sul server di Backup di Azure</span><span class="sxs-lookup"><span data-stu-id="d09c8-258">Establish vCenter Server credentials on Azure Backup Server</span></span>

<span data-ttu-id="d09c8-259">Prima di aggiungere hello VMware server tooAzure Backup Server, installare [Update 1 per il Server di Backup di Azure](https://support.microsoft.com/help/3175529/update-1-for-microsoft-azure-backup-server).</span><span class="sxs-lookup"><span data-stu-id="d09c8-259">Before you add hello VMware server tooAzure Backup Server, install [Update 1 for Azure Backup Server](https://support.microsoft.com/help/3175529/update-1-for-microsoft-azure-backup-server).</span></span>

1. <span data-ttu-id="d09c8-260">tooopen Server di Backup di Azure, fare doppio clic hello sul desktop del Server di Backup di Azure hello.</span><span class="sxs-lookup"><span data-stu-id="d09c8-260">tooopen Azure Backup Server, double-click hello icon on hello Azure Backup Server desktop.</span></span>

    ![Icona del server di Backup di Azure](./media/backup-azure-backup-server-vmware/mabs-icon.png)

    <span data-ttu-id="d09c8-262">Se non si trova sull'icona di hello sul desktop di hello, aprire il Server di Backup di Azure dall'elenco di hello delle App installate.</span><span class="sxs-lookup"><span data-stu-id="d09c8-262">If you can't find hello icon on hello desktop, open Azure Backup Server from hello list of installed apps.</span></span> <span data-ttu-id="d09c8-263">nome dell'app Azure Backup Server Hello viene chiamato Backup di Microsoft Azure.</span><span class="sxs-lookup"><span data-stu-id="d09c8-263">hello Azure Backup Server app name is called Microsoft Azure Backup.</span></span>

2. <span data-ttu-id="d09c8-264">Nella console di Server di Backup di Azure hello, fare clic su **Management**, fare clic su **server di produzione**e quindi fare clic sulla barra multifunzione dello strumento di hello, **gestire VMware**.</span><span class="sxs-lookup"><span data-stu-id="d09c8-264">In hello Azure Backup Server console, click **Management**, click **Production Servers**, and then on hello tool ribbon, click **Manage VMware**.</span></span>

    ![Console del server di Backup di Azure](./media/backup-azure-backup-server-vmware/add-vmware-credentials.png)

    <span data-ttu-id="d09c8-266">Hello **Gestisci credenziali** viene visualizzata la finestra di dialogo.</span><span class="sxs-lookup"><span data-stu-id="d09c8-266">hello **Manage Credentials** dialog box appears.</span></span>

    ![Finestra di dialogo Gestisci credenziali del server di Backup di Azure](./media/backup-azure-backup-server-vmware/mabs-manage-credentials-dialog.png)

3. <span data-ttu-id="d09c8-268">In hello **Gestisci credenziali** la finestra di dialogo, fare clic su **Aggiungi** tooopen hello **Add Credential** la finestra di dialogo.</span><span class="sxs-lookup"><span data-stu-id="d09c8-268">In hello **Manage Credentials** dialog box, click **Add** tooopen hello **Add Credential** dialog box.</span></span>

4. <span data-ttu-id="d09c8-269">In hello **Add Credential** finestra di dialogo immettere un nome e una descrizione per le nuove credenziali di hello.</span><span class="sxs-lookup"><span data-stu-id="d09c8-269">In hello **Add Credential** dialog box, enter a name and a description for hello new credential.</span></span> <span data-ttu-id="d09c8-270">Specificare quindi hello username e password.</span><span class="sxs-lookup"><span data-stu-id="d09c8-270">Then specify hello username and password.</span></span> <span data-ttu-id="d09c8-271">nome Hello, *credential Contoso Vcenter* utilizzato credenziali hello tooidentify hello procedura descritta di seguito.</span><span class="sxs-lookup"><span data-stu-id="d09c8-271">hello name, *Contoso Vcenter credential* is used tooidentify hello credential in hello next procedure.</span></span> <span data-ttu-id="d09c8-272">Utilizzare hello stesso nome utente e la password utilizzata per hello vCenter Server.</span><span class="sxs-lookup"><span data-stu-id="d09c8-272">Use hello same username and password that is used for hello vCenter Server.</span></span> <span data-ttu-id="d09c8-273">Se il Server vCenter hello e Server di Backup di Azure non sono in hello nello stesso dominio, in **nome utente**, specificare il dominio hello.</span><span class="sxs-lookup"><span data-stu-id="d09c8-273">If hello vCenter Server and Azure Backup Server are not in hello same domain, in **User name**, specify hello domain.</span></span>

    ![Finestra di dialogo Aggiungi credenziali del server di Backup di Azure](./media/backup-azure-backup-server-vmware/mabs-add-credential-dialog2.png)

    <span data-ttu-id="d09c8-275">Fare clic su **Aggiungi** tooadd hello nuova credenziale tooAzure Backup Server.</span><span class="sxs-lookup"><span data-stu-id="d09c8-275">Click **Add** tooadd hello new credential tooAzure Backup Server.</span></span> <span data-ttu-id="d09c8-276">nuove credenziali Hello verrà visualizzato nell'elenco hello hello **Gestisci credenziali** la finestra di dialogo.</span><span class="sxs-lookup"><span data-stu-id="d09c8-276">hello new credential appears in hello list in hello **Manage Credentials** dialog box.</span></span>
    
    ![Finestra di dialogo Gestisci credenziali del server di Backup di Azure](./media/backup-azure-backup-server-vmware/new-list-of-mabs-creds.png)

5. <span data-ttu-id="d09c8-278">hello tooclose **Gestisci credenziali** finestra di dialogo fare clic su hello **X** nell'angolo superiore destro di hello.</span><span class="sxs-lookup"><span data-stu-id="d09c8-278">tooclose hello **Manage Credentials** dialog box, click hello **X** in hello upper-right corner.</span></span>


## <a name="add-hello-vcenter-server-tooazure-backup-server"></a><span data-ttu-id="d09c8-279">Aggiungere hello vCenter Server tooAzure Backup Server</span><span class="sxs-lookup"><span data-stu-id="d09c8-279">Add hello vCenter Server tooAzure Backup Server</span></span>

<span data-ttu-id="d09c8-280">Creazione guidata Aggiunta Server di produzione è usato tooadd hello vCenter Server tooAzure Backup Server.</span><span class="sxs-lookup"><span data-stu-id="d09c8-280">Production Server Addition Wizard is used tooadd hello vCenter Server tooAzure Backup Server.</span></span>

<span data-ttu-id="d09c8-281">tooopen guidata di aggiunta Server di produzione, hello completo seguente procedura:</span><span class="sxs-lookup"><span data-stu-id="d09c8-281">tooopen Production Server Addition Wizard, complete hello following procedure:</span></span>

1. <span data-ttu-id="d09c8-282">Nella console di Server di Backup di Azure hello, fare clic su **Management**, fare clic su **server di produzione**, quindi fare clic su **Aggiungi**.</span><span class="sxs-lookup"><span data-stu-id="d09c8-282">In hello Azure Backup Server console, click **Management**, click **Production Servers**, and then click **Add**.</span></span>

    ![Aprire l'Aggiunta guidata server di produzione](./media/backup-azure-backup-server-vmware/add-vcenter-to-mabs.png)

    <span data-ttu-id="d09c8-284">Hello **guidata Aggiunta Server di produzione** viene visualizzata la finestra di dialogo.</span><span class="sxs-lookup"><span data-stu-id="d09c8-284">hello **Production Server Addition Wizard** dialog box appears.</span></span>

    ![Aggiunta guidata server di produzione](./media/backup-azure-backup-server-vmware/production-server-add-wizard.png)

2. <span data-ttu-id="d09c8-286">In hello **tipo selezionare Server di produzione** selezionare **server VMware**e quindi fare clic su **Avanti**.</span><span class="sxs-lookup"><span data-stu-id="d09c8-286">On hello **Select Production Server type** page, select **VMware Servers**, and then click **Next**.</span></span>

3. <span data-ttu-id="d09c8-287">In **nome Server o indirizzo IP**, specificare il nome di dominio completo hello (FQDN) o indirizzo IP del server VMware hello.</span><span class="sxs-lookup"><span data-stu-id="d09c8-287">In **Server Name/IP Address**, specify hello fully qualified domain name (FQDN) or IP address of hello VMware server.</span></span> <span data-ttu-id="d09c8-288">Se tutti i server ESXi hello gestiti da hello vCenter stesso, è possibile utilizzare il nome di vCenter hello.</span><span class="sxs-lookup"><span data-stu-id="d09c8-288">If all hello ESXi servers are managed by hello same vCenter, you can use hello vCenter name.</span></span>

    ![Specificare l'FQDN o l'indirizzo IP del server VMware](./media/backup-azure-backup-server-vmware/add-vmware-server-provide-server-name.png)

4. <span data-ttu-id="d09c8-290">In **porta SSL**, immettere una porta di hello toocommunicate utilizzato con server VMware hello.</span><span class="sxs-lookup"><span data-stu-id="d09c8-290">In **SSL Port**, enter hello port that is used toocommunicate with hello VMware server.</span></span> <span data-ttu-id="d09c8-291">Utilizzare la porta 443, che è la porta predefinita hello, a meno che non si sa che una porta diversa è obbligatoria.</span><span class="sxs-lookup"><span data-stu-id="d09c8-291">Use port 443, which is hello default port, unless you know that a different port is required.</span></span>

5. <span data-ttu-id="d09c8-292">In **specificare le credenziali**, selezionare hello credenziali creato in precedenza.</span><span class="sxs-lookup"><span data-stu-id="d09c8-292">In **Specify Credential**, select hello credential that you created earlier.</span></span>

    ![Specifica credenziale](./media/backup-azure-backup-server-vmware/identify-creds.png)

6. <span data-ttu-id="d09c8-294">Fare clic su **Aggiungi** tooadd hello VMware server toohello elenco **aggiunto i server VMware**, quindi fare clic su **Avanti** toomove toohello pagina successiva procedura guidata hello.</span><span class="sxs-lookup"><span data-stu-id="d09c8-294">Click **Add** tooadd hello VMware server toohello list of **Added VMware Servers**, and then click **Next** toomove toohello next page in hello wizard.</span></span>

    ![Aggiungere il server VMware e le credenziali](./media/backup-azure-backup-server-vmware/add-vmware-server-credentials.png)

7. <span data-ttu-id="d09c8-296">In hello **riepilogo** pagina, fare clic su **Aggiungi** tooadd hello specificato tooAzure server VMware Server Backup.</span><span class="sxs-lookup"><span data-stu-id="d09c8-296">In hello **Summary** page, click **Add** tooadd hello specified VMware server tooAzure Backup Server.</span></span>

    ![Aggiungi VMware server tooAzure Backup Server](./media/backup-azure-backup-server-vmware/tasks-screen.png)

  <span data-ttu-id="d09c8-298">Hello VMware server backup è un backup senza agente e hello nuovo server viene aggiunto immediatamente.</span><span class="sxs-lookup"><span data-stu-id="d09c8-298">hello VMware server backup is an agentless backup, and hello new server is added immediately.</span></span> <span data-ttu-id="d09c8-299">Hello **fine** pagina vengono visualizzati hello risultati.</span><span class="sxs-lookup"><span data-stu-id="d09c8-299">hello **Finish** page shows you hello results.</span></span>

  ![Pagina Fine](./media/backup-azure-backup-server-vmware/summary-screen.png)

  <span data-ttu-id="d09c8-301">tooadd più istanze di tooAzure Server vCenter Server Backup, ripetere l'operazione hello precedente i passaggi in questa sezione.</span><span class="sxs-lookup"><span data-stu-id="d09c8-301">tooadd multiple instances of vCenter Server tooAzure Backup Server, repeat hello previous steps in this section.</span></span>

<span data-ttu-id="d09c8-302">Dopo aver aggiunto hello vCenter Server tooAzure Backup Server, hello è toocreate un gruppo protezione dati.</span><span class="sxs-lookup"><span data-stu-id="d09c8-302">After you add hello vCenter Server tooAzure Backup Server, hello next step is toocreate a protection group.</span></span> <span data-ttu-id="d09c8-303">gruppo protezione dati Hello specifica hello vari dettagli per la conservazione a breve o lungo termine in modo in cui si definisce e applicare i criteri di backup hello.</span><span class="sxs-lookup"><span data-stu-id="d09c8-303">hello protection group specifies hello various details for short or long-term retention, and it is where you define and apply hello backup policy.</span></span> <span data-ttu-id="d09c8-304">criterio di backup Hello è pianificazione hello per quando si verificano i backup, e ciò che viene eseguito il backup.</span><span class="sxs-lookup"><span data-stu-id="d09c8-304">hello backup policy is hello schedule for when backups occur, and what is backed up.</span></span>


## <a name="configure-a-protection-group"></a><span data-ttu-id="d09c8-305">Configurazione di un gruppo protezione dati</span><span class="sxs-lookup"><span data-stu-id="d09c8-305">Configure a protection group</span></span>

<span data-ttu-id="d09c8-306">Se si utilizza System Center Data Protection Manager o Server di Backup di Azure prima di, vedere [pianificare i backup su disco](https://technet.microsoft.com/library/hh758026.aspx) tooprepare l'ambiente hardware.</span><span class="sxs-lookup"><span data-stu-id="d09c8-306">If you have not used System Center Data Protection Manager or Azure Backup Server before, see [Plan for disk backups](https://technet.microsoft.com/library/hh758026.aspx) tooprepare your hardware environment.</span></span> <span data-ttu-id="d09c8-307">Dopo che si verifica di avere un'adeguata archiviazione, utilizzare hello Crea nuovo gruppo protezione dati guidata tooadd le macchine virtuali VMware.</span><span class="sxs-lookup"><span data-stu-id="d09c8-307">After you check that you have proper storage, use hello Create New Protection Group wizard tooadd VMware virtual machines.</span></span>

1. <span data-ttu-id="d09c8-308">Nella console di Server di Backup di Azure hello, fare clic su **protezione**, nella barra multifunzione dello strumento di hello, fare clic su **New** procedura guidata Crea nuovo gruppo protezione dati di tooopen hello.</span><span class="sxs-lookup"><span data-stu-id="d09c8-308">In hello Azure Backup Server console, click **Protection**, and in hello tool ribbon, click **New** tooopen hello Create New Protection Group wizard.</span></span>

    ![Procedura guidata Crea nuovo gruppo protezione dati hello aperto](./media/backup-azure-backup-server-vmware/open-protection-wizard.png)

    <span data-ttu-id="d09c8-310">Hello **Crea nuovo gruppo protezione dati** viene visualizzata la finestra di dialogo Creazione guidata.</span><span class="sxs-lookup"><span data-stu-id="d09c8-310">hello **Create New Protection Group** wizard dialog box appears.</span></span>

    ![Finestra di dialogo della procedura guidata Crea nuovo gruppo protezione dati](./media/backup-azure-backup-server-vmware/protection-wizard.png)

    <span data-ttu-id="d09c8-312">Fare clic su **Avanti** tooadvance toohello **Seleziona tipo di gruppo protezione dati** pagina.</span><span class="sxs-lookup"><span data-stu-id="d09c8-312">Click **Next** tooadvance toohello **Select protection group type** page.</span></span>

2. <span data-ttu-id="d09c8-313">In hello **il tipo di gruppo protezione dati selezionare** selezionare **server** e quindi fare clic su **Avanti**.</span><span class="sxs-lookup"><span data-stu-id="d09c8-313">On hello **Select Protection group type** page, select **Servers** and then click **Next**.</span></span> <span data-ttu-id="d09c8-314">Hello **Seleziona membri del gruppo** verrà visualizzata la pagina.</span><span class="sxs-lookup"><span data-stu-id="d09c8-314">hello **Select group members** page appears.</span></span>

3. <span data-ttu-id="d09c8-315">In hello **Seleziona membri del gruppo** pagina, i membri disponibili hello e membri hello selezionato vengono visualizzati.</span><span class="sxs-lookup"><span data-stu-id="d09c8-315">On hello **Select group members** page, hello available members and hello selected members appear.</span></span> <span data-ttu-id="d09c8-316">Selezionare i membri di hello che desidera tooprotect e quindi fare clic su **Avanti**.</span><span class="sxs-lookup"><span data-stu-id="d09c8-316">Select hello members that you want tooprotect, and then click **Next**.</span></span>

    ![Seleziona membri del gruppo](./media/backup-azure-backup-server-vmware/server-add-selected-members.png)

    <span data-ttu-id="d09c8-318">Quando si seleziona un membro, se si seleziona una cartella che contiene altre cartelle o macchine virtuali, vengono selezionate anche le cartelle e le macchine virtuali contenute.</span><span class="sxs-lookup"><span data-stu-id="d09c8-318">When you select a member, if you select a folder that contains other folders or VMs, those folders and VMs are also selected.</span></span> <span data-ttu-id="d09c8-319">inclusione di Hello di cartelle di hello e macchine virtuali nella cartella padre hello viene chiamata la protezione a livello di cartella.</span><span class="sxs-lookup"><span data-stu-id="d09c8-319">hello inclusion of hello folders and VMs in hello parent folder is called folder-level protection.</span></span> <span data-ttu-id="d09c8-320">tooremove una cartella o nella macchina virtuale, la casella di controllo crittografato hello.</span><span class="sxs-lookup"><span data-stu-id="d09c8-320">tooremove a folder or VM, clear hello check box.</span></span>

    <span data-ttu-id="d09c8-321">Se una macchina virtuale o in una cartella che contiene una macchina virtuale, è già protetto tooAzure, è possibile selezionare nuovamente tale macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="d09c8-321">If a VM, or a folder containing a VM, is already protected tooAzure, you cannot select that VM again.</span></span> <span data-ttu-id="d09c8-322">Vale a dire, dopo aver protetto tooAzure una macchina virtuale, non può essere protetto anche punti di ripristino duplicati che impedisce la creazione di una macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="d09c8-322">That is, after a VM is protected tooAzure, it cannot be protected again, which prevents duplicate recovery points from being created for one VM.</span></span> <span data-ttu-id="d09c8-323">Se si desidera toosee quale istanza del Server di Backup di Azure protegge già un membro, il punto toohello toosee hello Nome membro hello protezione del server.</span><span class="sxs-lookup"><span data-stu-id="d09c8-323">If you want toosee which Azure Backup Server instance already protects a member, point toohello member toosee hello name of hello protecting server.</span></span>

4. <span data-ttu-id="d09c8-324">In hello **Selezione metodo protezione dati** pagina, immettere un nome per il gruppo di protezione dati hello.</span><span class="sxs-lookup"><span data-stu-id="d09c8-324">On hello **Select Data Protection Method** page, enter a name for hello protection group.</span></span> <span data-ttu-id="d09c8-325">Protezione a breve termine (toodisk) e online sono selezionati.</span><span class="sxs-lookup"><span data-stu-id="d09c8-325">Short-term protection (toodisk) and online protection are selected.</span></span> <span data-ttu-id="d09c8-326">Se si desidera la protezione online toouse (tooAzure), è necessario utilizzare toodisk protezione a breve termine.</span><span class="sxs-lookup"><span data-stu-id="d09c8-326">If you want toouse online protection (tooAzure), you must use short-term protection toodisk.</span></span> <span data-ttu-id="d09c8-327">Fare clic su **Avanti** intervallo di protezione tooproceed toohello a breve termine.</span><span class="sxs-lookup"><span data-stu-id="d09c8-327">Click **Next** tooproceed toohello short-term protection range.</span></span>

    ![Seleziona metodo protezione dati](./media/backup-azure-backup-server-vmware/name-protection-group.png)

5. <span data-ttu-id="d09c8-329">In hello **Specifica obiettivi a breve termine** pagina per **mantenimento**, specificare hello numero di giorni per cui si desidera che i punti di ripristino di tooretain *archiviati toodisk*.</span><span class="sxs-lookup"><span data-stu-id="d09c8-329">On hello **Specify Short-Term Goals** page, for **Retention Range**, specify hello number of days that you want tooretain recovery points that are *stored toodisk*.</span></span> <span data-ttu-id="d09c8-330">Se si desidera ora hello toochange e giorni quando vengono eseguiti i punti di ripristino, fare clic su **modifica**.</span><span class="sxs-lookup"><span data-stu-id="d09c8-330">If you want toochange hello time and days when recovery points are taken, click **Modify**.</span></span> <span data-ttu-id="d09c8-331">punti di ripristino a breve termine Hello sono backup completi.</span><span class="sxs-lookup"><span data-stu-id="d09c8-331">hello short-term recovery points are full backups.</span></span> <span data-ttu-id="d09c8-332">e non backup incrementali.</span><span class="sxs-lookup"><span data-stu-id="d09c8-332">They are not incremental backups.</span></span> <span data-ttu-id="d09c8-333">Quando si è soddisfatti gli obiettivi a breve termine hello, fare clic su **Avanti**.</span><span class="sxs-lookup"><span data-stu-id="d09c8-333">When you are satisfied with hello short-term goals, click **Next**.</span></span>

    ![Specifica obiettivi a breve termine](./media/backup-azure-backup-server-vmware/short-term-goals.png)

6. <span data-ttu-id="d09c8-335">In hello **Verifica allocazione dischi** pagina, esaminare e se necessario, modificare lo spazio su disco hello per le macchine virtuali hello.</span><span class="sxs-lookup"><span data-stu-id="d09c8-335">On hello **Review Disk Allocation** page, review and if necessary, modify hello disk space for hello VMs.</span></span> <span data-ttu-id="d09c8-336">Hello consigliati allocazioni dei dischi sono in base hello periodo di mantenimento specificato in hello **Specifica obiettivi a breve termine** pagina hello tipo di carico di lavoro e dimensioni di hello di hello i dati protetti (identificati nel passaggio 3).</span><span class="sxs-lookup"><span data-stu-id="d09c8-336">hello recommended disk allocations are based on hello retention range that is specified in hello **Specify Short-Term Goals** page, hello type of workload, and hello size of hello protected data (identified in step 3).</span></span>  

  - <span data-ttu-id="d09c8-337">**Dimensioni dei dati:** dimensioni dei dati di hello nel gruppo protezione dati hello.</span><span class="sxs-lookup"><span data-stu-id="d09c8-337">**Data size:** Size of hello data in hello protection group.</span></span>
  - <span data-ttu-id="d09c8-338">**Spazio su disco:** hello quantità di spazio su disco per il gruppo di protezione dati hello consigliata.</span><span class="sxs-lookup"><span data-stu-id="d09c8-338">**Disk space:** hello recommended amount of disk space for hello protection group.</span></span> <span data-ttu-id="d09c8-339">Se si desidera toomodify questa impostazione, è consigliabile allocare uno spazio totale leggermente superiore rispetto a quanto hello che si prevede di che aumento delle dimensioni di ogni origine dati.</span><span class="sxs-lookup"><span data-stu-id="d09c8-339">If you want toomodify this setting, you should allocate total space that is slightly larger than hello amount that you estimate each data source grows.</span></span>
  - <span data-ttu-id="d09c8-340">**Condividi percorso dati:** se si attiva la condivisione del percorso, più origini dati nella protezione hello possono mappare tooa singola replica e volume del punto di ripristino.</span><span class="sxs-lookup"><span data-stu-id="d09c8-340">**Colocate data:** If you turn on colocation, multiple data sources in hello protection can map tooa single replica and recovery point volume.</span></span> <span data-ttu-id="d09c8-341">La condivisione del percorso non è supportata per tutti i carichi di lavoro.</span><span class="sxs-lookup"><span data-stu-id="d09c8-341">Colocation isn't supported for all workloads.</span></span>
  - <span data-ttu-id="d09c8-342">**Aumento automatico delle dimensioni:** se si abilita questa impostazione, se i dati nel gruppo protetto hello superano l'allocazione iniziale di hello, System Center Data Protection Manager tenta di dimensioni del disco tooincrease hello del 25%.</span><span class="sxs-lookup"><span data-stu-id="d09c8-342">**Automatically grow:** If you turn on this setting, if data in hello protected group outgrows hello initial allocation, System Center Data Protection Manager tries tooincrease hello disk size by 25 percent.</span></span>
  - <span data-ttu-id="d09c8-343">**Dettagli pool di archiviazione:** Mostra stato hello hello del pool di archiviazione, inclusi totale e residua dimensioni del disco.</span><span class="sxs-lookup"><span data-stu-id="d09c8-343">**Storage pool details:** Shows hello status of hello storage pool, including total and remaining disk size.</span></span>

    ![Rivedere l'allocazione dei dischi](./media/backup-azure-backup-server-vmware/review-disk-allocation.png)

    <span data-ttu-id="d09c8-345">Quando si è soddisfatti di allocazione dello spazio di hello, fare clic su **Avanti**.</span><span class="sxs-lookup"><span data-stu-id="d09c8-345">When you are satisfied with hello space allocation, click **Next**.</span></span>

7. <span data-ttu-id="d09c8-346">In hello **Scegli metodo di creazione della Replica** pagina, specificare come copia iniziale di toogenerate hello o replica, dei dati di hello protetto nel Server di Backup di Azure.</span><span class="sxs-lookup"><span data-stu-id="d09c8-346">On hello **Choose Replica Creation Method** page, specify how you want toogenerate hello initial copy, or replica, of hello protected data on Azure Backup Server.</span></span>

    <span data-ttu-id="d09c8-347">valore predefinito di Hello è **automaticamente tramite rete hello** e **ora**.</span><span class="sxs-lookup"><span data-stu-id="d09c8-347">hello default is **Automatically over hello network** and **Now**.</span></span> <span data-ttu-id="d09c8-348">Se si utilizza l'impostazione di hello, si consiglia di specificare un orario.</span><span class="sxs-lookup"><span data-stu-id="d09c8-348">If you use hello default, we recommend that you specify an off-peak time.</span></span> <span data-ttu-id="d09c8-349">Scegliere **In seguito** e specificare un giorno e un'ora.</span><span class="sxs-lookup"><span data-stu-id="d09c8-349">Choose **Later** and specify a day and time.</span></span>

    <span data-ttu-id="d09c8-350">Per grandi quantità di dati o condizioni della rete-ottimale, prendere in considerazione la replica dei dati hello offline usando supporti rimovibili.</span><span class="sxs-lookup"><span data-stu-id="d09c8-350">For large amounts of data or less-than-optimal network conditions, consider replicating hello data offline by using removable media.</span></span>

    <span data-ttu-id="d09c8-351">Dopo avere effettuato le scelte, fare clic su **Avanti**.</span><span class="sxs-lookup"><span data-stu-id="d09c8-351">After you have made your choices, click **Next**.</span></span>

    ![Scelta del metodo per la creazione della replica](./media/backup-azure-backup-server-vmware/replica-creation.png)

8. <span data-ttu-id="d09c8-353">In hello **opzioni di verifica coerenza** pagina, selezionare come e quando le verifiche della coerenza hello tooautomate.</span><span class="sxs-lookup"><span data-stu-id="d09c8-353">On hello **Consistency Check Options** page, select how and when tooautomate hello consistency checks.</span></span> <span data-ttu-id="d09c8-354">È possibile eseguire verifiche della coerenza quando i dati di replica diventano incoerenti o in base a una pianificazione impostata.</span><span class="sxs-lookup"><span data-stu-id="d09c8-354">You can run consistency checks when replica data becomes inconsistent, or on a set schedule.</span></span>

    <span data-ttu-id="d09c8-355">Se non si desidera tooconfigure le verifiche di coerenza automatica, è possibile eseguire una verifica manuale.</span><span class="sxs-lookup"><span data-stu-id="d09c8-355">If you don't want tooconfigure automatic consistency checks, you can run a manual check.</span></span> <span data-ttu-id="d09c8-356">Nell'area di protezione hello hello Azure Backup della console di Server, gruppo di protezione dati hello e quindi scegliere **Esegui verifica coerenza**.</span><span class="sxs-lookup"><span data-stu-id="d09c8-356">In hello protection area of hello Azure Backup Server console, right-click hello protection group and then select **Perform Consistency Check**.</span></span>

    <span data-ttu-id="d09c8-357">Fare clic su **Avanti** toomove toohello prossima pagina.</span><span class="sxs-lookup"><span data-stu-id="d09c8-357">Click **Next** toomove toohello next page.</span></span>

9. <span data-ttu-id="d09c8-358">In hello **specificare dati da proteggere Online** pagina, selezionare uno o più origini dati che si desidera tooprotect.</span><span class="sxs-lookup"><span data-stu-id="d09c8-358">On hello **Specify Online Protection Data** page, select one or more data sources that you want tooprotect.</span></span> <span data-ttu-id="d09c8-359">È possibile selezionare i membri di hello singolarmente o fare clic su **Seleziona tutto** toochoose tutti i membri.</span><span class="sxs-lookup"><span data-stu-id="d09c8-359">You can select hello members individually, or click **Select All** toochoose all members.</span></span> <span data-ttu-id="d09c8-360">Dopo aver scelto i membri di hello, fare clic su **Avanti**.</span><span class="sxs-lookup"><span data-stu-id="d09c8-360">After you choose hello members, click **Next**.</span></span>

    ![Specifica i dati da proteggere online](./media/backup-azure-backup-server-vmware/select-data-to-protect.png)

10. <span data-ttu-id="d09c8-362">In hello **pianificazione dei Backup Online specificare** specificare toogenerate i punti di ripristino da backup su disco hello hello pianificazione.</span><span class="sxs-lookup"><span data-stu-id="d09c8-362">On hello **Specify Online Backup Schedule** page, specify hello schedule toogenerate recovery points from hello disk backup.</span></span> <span data-ttu-id="d09c8-363">Dopo la generazione di un punto di ripristino hello, è l'insieme di credenziali di servizi di ripristino toohello trasferiti in Azure.</span><span class="sxs-lookup"><span data-stu-id="d09c8-363">After hello recovery point is generated, it is transferred toohello Recovery Services vault in Azure.</span></span> <span data-ttu-id="d09c8-364">Quando si è soddisfatti di pianificazione dei backup online hello, fare clic su **Avanti**.</span><span class="sxs-lookup"><span data-stu-id="d09c8-364">When you are satisfied with hello online backup schedule, click **Next**.</span></span>

    ![Specificare la pianificazione dei backup online](./media/backup-azure-backup-server-vmware/online-backup-schedule.png)

11. <span data-ttu-id="d09c8-366">In hello **specificare criteri di conservazione Online** pagina, specificare quanto tempo si desidera tooretain dati di backup hello in Azure.</span><span class="sxs-lookup"><span data-stu-id="d09c8-366">On hello **Specify Online Retention Policy** page, indicate how long you want tooretain hello backup data in Azure.</span></span> <span data-ttu-id="d09c8-367">Dopo aver definito i criteri di hello, fare clic su **Avanti**.</span><span class="sxs-lookup"><span data-stu-id="d09c8-367">After hello policy is defined, click **Next**.</span></span>

    ![Specificare i criteri di mantenimento online](./media/backup-azure-backup-server-vmware/retention-policy.png)

    <span data-ttu-id="d09c8-369">Non esiste un limite di tempo per la conservazione dei dati in Azure.</span><span class="sxs-lookup"><span data-stu-id="d09c8-369">There is no time limit for how long you can keep data in Azure.</span></span> <span data-ttu-id="d09c8-370">Quando si archiviano i dati relativi al punto di ripristino in Azure, hello solo limite è che non è possibile avere più di 9999 punti di ripristino per ogni istanza protetta.</span><span class="sxs-lookup"><span data-stu-id="d09c8-370">When you store recovery point data in Azure, hello only limit is that you cannot have more than 9999 recovery points per protected instance.</span></span> <span data-ttu-id="d09c8-371">In questo esempio, istanza protetta hello è server VMware hello.</span><span class="sxs-lookup"><span data-stu-id="d09c8-371">In this example, hello protected instance is hello VMware server.</span></span>

12. <span data-ttu-id="d09c8-372">In hello **riepilogo** pagina, esaminare i dettagli di hello per le impostazioni e i membri del gruppo protezione dati e quindi fare clic su **Crea gruppo**.</span><span class="sxs-lookup"><span data-stu-id="d09c8-372">On hello **Summary** page, review hello details for your protection group members and settings, and then click **Create Group**.</span></span>

    ![Riepilogo delle impostazioni e dei membri del gruppo protezione dati](./media/backup-azure-backup-server-vmware/protection-group-summary.png)

## <a name="next-steps"></a><span data-ttu-id="d09c8-374">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="d09c8-374">Next steps</span></span>
<span data-ttu-id="d09c8-375">Se si utilizzano i carichi di lavoro di Azure Backup Server tooprotect VMware, potrebbe essere interessati all'uso di Server di Backup di Azure toohelp proteggere un [Microsoft Exchange server](./backup-azure-exchange-mabs.md), [farm Microsoft SharePoint](./backup-azure-backup-sharepoint-mabs.md), o un [Database di SQL Server](./backup-azure-sql-mabs.md).</span><span class="sxs-lookup"><span data-stu-id="d09c8-375">If you use Azure Backup Server tooprotect VMware workloads, you may be interested in using Azure Backup Server toohelp protect a [Microsoft Exchange server](./backup-azure-exchange-mabs.md), a [Microsoft SharePoint farm](./backup-azure-backup-sharepoint-mabs.md), or a [SQL Server database](./backup-azure-sql-mabs.md).</span></span>

<span data-ttu-id="d09c8-376">Per informazioni sui problemi con la registrazione dell'agente di hello, configurare il gruppo di protezione dati hello o il backup dei processi, vedere [risoluzione dei problemi dei Server di Backup Azure](./backup-azure-mabs-troubleshoot.md).</span><span class="sxs-lookup"><span data-stu-id="d09c8-376">For information on problems with registering hello agent, configuring hello protection group, or backing up jobs, see [Troubleshoot Azure Backup Server](./backup-azure-mabs-troubleshoot.md).</span></span>

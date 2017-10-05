---
title: Eseguire il backup di server VMware con il server di Backup di Azure | Microsoft Docs
description: Usare il server di Backup di Azure per eseguire il backup di server VMware vCenter/ESXi in Azure o su disco. Questo articolo offre istruzioni dettagliate per il backup o la protezione dei carichi di lavoro VMware.
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
ms.openlocfilehash: ad331dffb7c31d12290f4223967c568e4535fe3c
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/03/2017
---
# <a name="back-up-a-vmware-server-to-azure"></a><span data-ttu-id="a694a-104">Eseguire il backup di un server VMware in Azure</span><span class="sxs-lookup"><span data-stu-id="a694a-104">Back up a VMware server to Azure</span></span>

<span data-ttu-id="a694a-105">In questo articolo viene illustrato come configurare il server di Backup di Azure per proteggere i carichi di lavoro dei server VMware.</span><span class="sxs-lookup"><span data-stu-id="a694a-105">This article explains how to configure Azure Backup Server to help protect VMware server workloads.</span></span> <span data-ttu-id="a694a-106">In questo articolo si presuppone che sia stato già installato il server di Backup di Azure.</span><span class="sxs-lookup"><span data-stu-id="a694a-106">This article assumes you already have Azure Backup Server installed.</span></span> <span data-ttu-id="a694a-107">Se il server di Backup di Azure non è installato, vedere [Preparazione del backup dei carichi di lavoro con il server di Backup di Azure](backup-azure-microsoft-azure-backup.md).</span><span class="sxs-lookup"><span data-stu-id="a694a-107">If you don't have Azure Backup Server installed, see [Prepare to back up workloads using Azure Backup Server](backup-azure-microsoft-azure-backup.md).</span></span>

<span data-ttu-id="a694a-108">Il server di Backup di Azure può eseguire il backup o assicurare la protezione di server VMware vCenter versione 6.5, 6.0 e 5.5.</span><span class="sxs-lookup"><span data-stu-id="a694a-108">Azure Backup Server can back up, or help protect, VMware vCenter Server version 6.5, 6.0 and 5.5.</span></span>


## <a name="create-a-secure-connection-to-the-vcenter-server"></a><span data-ttu-id="a694a-109">Creazione di una connessione protetta al server vCenter</span><span class="sxs-lookup"><span data-stu-id="a694a-109">Create a secure connection to the vCenter Server</span></span>

<span data-ttu-id="a694a-110">Per impostazione predefinita, il server di Backup di Azure comunica con ognuno dei server vCenter tramite un canale HTTPS.</span><span class="sxs-lookup"><span data-stu-id="a694a-110">By default, Azure Backup Server communicates with each vCenter Server via an HTTPS channel.</span></span> <span data-ttu-id="a694a-111">Per attivare la comunicazione protetta, è consigliabile installare il certificato dell'autorità di certificazione (CA, Certificate Authority) di VMware nel server di Backup di Azure.</span><span class="sxs-lookup"><span data-stu-id="a694a-111">To turn on the secure communication, we recommend that you install the VMware Certificate Authority (CA) certificate on Azure Backup Server.</span></span> <span data-ttu-id="a694a-112">Se la comunicazione protetta non è necessaria e si preferisce disabilitare il requisito HTTPS, vedere [Disabilitazione del protocollo di comunicazione sicura](backup-azure-backup-server-vmware.md#disable-secure-communication-protocol).</span><span class="sxs-lookup"><span data-stu-id="a694a-112">If you don't require secure communication, and would prefer to disable the HTTPS requirement, see [Disable secure communication protocol](backup-azure-backup-server-vmware.md#disable-secure-communication-protocol).</span></span> <span data-ttu-id="a694a-113">Per creare una connessione sicura tra il server di Backup di Azure e il server vCenter, importare il certificato trusted nel server di Backup di Azure.</span><span class="sxs-lookup"><span data-stu-id="a694a-113">To create a secure connection between Azure Backup Server and the vCenter Server, import the trusted certificate on Azure Backup Server.</span></span>

<span data-ttu-id="a694a-114">Di solito, per connettersi al server vCenter tramite client Web vSphere si usa un browser nel computer server di Backup di Azure.</span><span class="sxs-lookup"><span data-stu-id="a694a-114">Typically, you use a browser on the Azure Backup Server machine to connect to the vCenter Server via the vSphere Web Client.</span></span> <span data-ttu-id="a694a-115">La prima volta che si usa il browser del server di Backup di Azure per connettersi al server vCenter, la connessione non è protetta.</span><span class="sxs-lookup"><span data-stu-id="a694a-115">The first time you use the Azure Backup Server browser to connect to the vCenter Server, the connection isn't secure.</span></span> <span data-ttu-id="a694a-116">L'immagine seguente mostra la connessione non protetta.</span><span class="sxs-lookup"><span data-stu-id="a694a-116">The following image shows the unsecured connection.</span></span>

![Esempio di connessione non protetta al server VMware](./media/backup-azure-backup-server-vmware/unsecure-url.png)

<span data-ttu-id="a694a-118">Per risolvere il problema e creare una connessione protetta, scaricare i certificati CA radice attendibili.</span><span class="sxs-lookup"><span data-stu-id="a694a-118">To fix this issue, and create a secure connection, download the trusted root CA certificates.</span></span>

1. <span data-ttu-id="a694a-119">Nel browser del server di Backup di Azure immettere l'URL del client Web vSphere.</span><span class="sxs-lookup"><span data-stu-id="a694a-119">In the browser on Azure Backup Server, enter the URL to the vSphere Web Client.</span></span> <span data-ttu-id="a694a-120">Viene visualizzata la pagina di accesso del client Web vSphere.</span><span class="sxs-lookup"><span data-stu-id="a694a-120">The vSphere Web Client login page appears.</span></span>

    ![Client Web vSphere](./media/backup-azure-backup-server-vmware/vsphere-web-client.png)

    <span data-ttu-id="a694a-122">Nella parte inferiore delle informazioni per amministratori e sviluppatori individuare il collegamento **Download trusted root CA certificates** (Scarica certificati CA radice trusted).</span><span class="sxs-lookup"><span data-stu-id="a694a-122">At the bottom of the information for administrators and developers, locate the **Download trusted root CA certificates** link.</span></span>

    ![Collegamento al download dei certificati CA radice trusted](./media/backup-azure-backup-server-vmware/vmware-download-ca-cert-prompt.png)

  <span data-ttu-id="a694a-124">Qualora fosse impossibile trovare la pagina di accesso del client Web vSphere, controllare le impostazioni del proxy del browser.</span><span class="sxs-lookup"><span data-stu-id="a694a-124">If you don't see the vSphere Web Client login page, check your browser's proxy settings.</span></span>

2. <span data-ttu-id="a694a-125">Fare clic su **Scarica certificati CA radice attendibili**.</span><span class="sxs-lookup"><span data-stu-id="a694a-125">Click **Download trusted root CA certificates**.</span></span>

    <span data-ttu-id="a694a-126">Il server vCenter scarica un file nel computer locale.</span><span class="sxs-lookup"><span data-stu-id="a694a-126">The vCenter Server downloads a file to your local computer.</span></span> <span data-ttu-id="a694a-127">Il nome del file è **download**.</span><span class="sxs-lookup"><span data-stu-id="a694a-127">The file's name is named **download**.</span></span> <span data-ttu-id="a694a-128">A seconda del browser, viene visualizzato un messaggio che chiede se aprire o salvare il file.</span><span class="sxs-lookup"><span data-stu-id="a694a-128">Depending on your browser, you receive a message that asks whether to open or save the file.</span></span>

    ![messaggio di download quando vengono scaricati i certificati](./media/backup-azure-backup-server-vmware/download-certs.png)

3. <span data-ttu-id="a694a-130">Salvare il file in un percorso nel server di Backup di Azure.</span><span class="sxs-lookup"><span data-stu-id="a694a-130">Save the file to a location on Azure Backup Server.</span></span> <span data-ttu-id="a694a-131">Quando si salva il file, aggiungere l'estensione zip al nome del file.</span><span class="sxs-lookup"><span data-stu-id="a694a-131">When you save the file, add the .zip file name extension.</span></span>

    <span data-ttu-id="a694a-132">Il file è un file con estensione .zip che contiene le informazioni sui certificati.</span><span class="sxs-lookup"><span data-stu-id="a694a-132">The file is a .zip file that contains the information about the certificates.</span></span> <span data-ttu-id="a694a-133">L'estensione zip consente di usare gli strumenti di estrazione.</span><span class="sxs-lookup"><span data-stu-id="a694a-133">With the .zip extension, you can use the extraction tools.</span></span>

4. <span data-ttu-id="a694a-134">Fare clic con il pulsante destro del mouse su **download.zip** e quindi selezionare **Estrai tutto** per estrarre i contenuti.</span><span class="sxs-lookup"><span data-stu-id="a694a-134">Right-click **download.zip**, and then select **Extract All** to extract the contents.</span></span>

    <span data-ttu-id="a694a-135">I contenuti del file con estensione zip vengono estratti in una cartella denominata **certs**.</span><span class="sxs-lookup"><span data-stu-id="a694a-135">The .zip file extracts its contents to a folder named **certs**.</span></span> <span data-ttu-id="a694a-136">Nella cartella certs sono visualizzati due tipi di file.</span><span class="sxs-lookup"><span data-stu-id="a694a-136">Two types of files appear in the certs folder.</span></span> <span data-ttu-id="a694a-137">L'estensione del file del certificato radice inizia con una sequenza numerata, ad esempio .0 e .1.</span><span class="sxs-lookup"><span data-stu-id="a694a-137">The root certificate file has an extension that begins with a numbered sequence like .0 and .1.</span></span>
    
    <span data-ttu-id="a694a-138">L'estensione del file CRL inizia con una sequenza simile a .r0 o .r1.</span><span class="sxs-lookup"><span data-stu-id="a694a-138">The CRL file has an extension that begins with a sequence like .r0 or .r1.</span></span> <span data-ttu-id="a694a-139">Il file CRL è associato a un certificato.</span><span class="sxs-lookup"><span data-stu-id="a694a-139">The CRL file is associated with a certificate.</span></span>

    ![<span data-ttu-id="a694a-140">File di download estratto localmente</span><span class="sxs-lookup"><span data-stu-id="a694a-140">Download file extracted locally</span></span> ](./media/backup-azure-backup-server-vmware/extracted-files-in-certs-folder.png)

5. <span data-ttu-id="a694a-141">Nella cartella **certs** fare clic con il pulsante destro del mouse sul file del certificato radice e quindi fare clic su **Rinomina**.</span><span class="sxs-lookup"><span data-stu-id="a694a-141">In the **certs** folder, right-click the root certificate file, and then click **Rename**.</span></span>

    ![<span data-ttu-id="a694a-142">Ridenominazione del certificato radice</span><span class="sxs-lookup"><span data-stu-id="a694a-142">Rename root certificate</span></span> ](./media/backup-azure-backup-server-vmware/rename-cert.png)

    <span data-ttu-id="a694a-143">Modificare l'estensione del certificato radice in .crt.</span><span class="sxs-lookup"><span data-stu-id="a694a-143">Change the root certificate's extension to .crt.</span></span> <span data-ttu-id="a694a-144">Quando viene richiesta la conferma della modifica dell'estensione, fare clic su **Sì** o **OK**.</span><span class="sxs-lookup"><span data-stu-id="a694a-144">When you're asked if you're sure you want to change the extension, click **Yes** or **OK**.</span></span> <span data-ttu-id="a694a-145">In caso contrario, è possibile modificare manualmente la funzione del file prevista.</span><span class="sxs-lookup"><span data-stu-id="a694a-145">Otherwise, you change the file's intended function.</span></span> <span data-ttu-id="a694a-146">L'icona del file si trasforma nell'icona che rappresenta i certificati radice.</span><span class="sxs-lookup"><span data-stu-id="a694a-146">The icon for the file changes to an icon that represents a root certificate.</span></span>

6. <span data-ttu-id="a694a-147">Fare clic con il pulsante destro del mouse sul certificato radice e nel menu a comparsa, selezionare **Installa certificato**.</span><span class="sxs-lookup"><span data-stu-id="a694a-147">Right-click the root certificate and from the pop-up menu, select **Install Certificate**.</span></span>

    <span data-ttu-id="a694a-148">Viene visualizzata la finestra di dialogo **Importazione guidata certificati**.</span><span class="sxs-lookup"><span data-stu-id="a694a-148">The **Certificate Import Wizard** dialog box appears.</span></span>

7. <span data-ttu-id="a694a-149">Nella finestra di dialogo **Importazione guidata certificati** selezionare **Computer locale** come destinazione del certificato e quindi fare clic su **Avanti** per continuare.</span><span class="sxs-lookup"><span data-stu-id="a694a-149">In the **Certificate Import Wizard** dialog box, select **Local Machine** as the destination for the certificate, and then click **Next** to continue.</span></span>

    ![<span data-ttu-id="a694a-150">Opzioni di destinazione di archiviazione del certificato</span><span class="sxs-lookup"><span data-stu-id="a694a-150">Certificate storage destination options</span></span> ](./media/backup-azure-backup-server-vmware/certificate-import-wizard1.png)

    <span data-ttu-id="a694a-151">Se viene visualizzata la richiesta di conferma delle modifiche al computer, fare clic su **Sì** o **OK** per tutte le modifiche.</span><span class="sxs-lookup"><span data-stu-id="a694a-151">If you're asked if you want to allow changes to the computer, click **Yes** or **OK**, to all the changes.</span></span>

8. <span data-ttu-id="a694a-152">Nella pagina **Archivio certificati** selezionare **Colloca tutti i certificati nel seguente archivio** e quindi fare clic su **Sfoglia**per scegliere l'archivio certificati.</span><span class="sxs-lookup"><span data-stu-id="a694a-152">On the **Certificate Store** page, select **Place all certificates in the following store**, and then click **Browse** to choose the certificate store.</span></span>

    ![Inserire i certificati in un punto di archiviazione specifico](./media/backup-azure-backup-server-vmware/cert-import-wizard-local-store.png)

    <span data-ttu-id="a694a-154">Verrà visualizzata la finestra di dialogo **Selezione archivio certificati**.</span><span class="sxs-lookup"><span data-stu-id="a694a-154">The **Select Certificate Store** dialog box appears.</span></span>

    ![Gerarchia di cartelle di archiviazione di certificati](./media/backup-azure-backup-server-vmware/cert-store.png)

9. <span data-ttu-id="a694a-156">Selezionare **Autorità di certificazione radice attendibili** come cartella di destinazione per i certificati e quindi fare clic su **OK**.</span><span class="sxs-lookup"><span data-stu-id="a694a-156">Select **Trusted Root Certification Authorities** as the destination folder for the certificates, and then click **OK**.</span></span>

    ![Cartella di destinazione dei certificati](./media/backup-azure-backup-server-vmware/certificate-store-selected.png)

    <span data-ttu-id="a694a-158">La cartella **Autorità di certificazione radice attendibili** verrà confermata come archivio certificati.</span><span class="sxs-lookup"><span data-stu-id="a694a-158">The **Trusted Root Certification Authorities** folder is confirmed as the certificate store.</span></span> <span data-ttu-id="a694a-159">Fare clic su **Avanti**.</span><span class="sxs-lookup"><span data-stu-id="a694a-159">Click **Next**.</span></span>

    ![Cartella archivio certificati](./media/backup-azure-backup-server-vmware/certificate-import-wizard2.png)

10. <span data-ttu-id="a694a-161">Nella pagina **Completamento dell'Importazione guidata certificati** verificare che il certificato si trovi nella cartella desiderata e quindi fare clic su **Fine**.</span><span class="sxs-lookup"><span data-stu-id="a694a-161">On the **Completing the Certificate Import Wizard** page, verify that the certificate is in the desired folder, and then click **Finish**.</span></span>

    ![Verificare che i certificati si trovino nella cartella corretta](./media/backup-azure-backup-server-vmware/cert-wizard-final-screen.png)

    <span data-ttu-id="a694a-163">Viene visualizzata una finestra di dialogo con la conferma dell'esito positivo dell'importazione del certificato.</span><span class="sxs-lookup"><span data-stu-id="a694a-163">A dialog box appears, the successful certificate import is confirmed.</span></span>

11. <span data-ttu-id="a694a-164">Accedere al server vCenter per verificare che la connessione sia sicura.</span><span class="sxs-lookup"><span data-stu-id="a694a-164">Sign in to the vCenter Server to confirm that your connection is secure.</span></span>

  <span data-ttu-id="a694a-165">Se l'importazione del certificato ha esito negativo e non è possibile stabilire una connessione sicura, consultare la documentazione di VMware vSphere relativa a [come ottenere certificati server](http://pubs.vmware.com/vsphere-60/index.jsp#com.vmware.wssdk.dsg.doc/sdk_sg_server_certificate_Appendixes.6.4.html).</span><span class="sxs-lookup"><span data-stu-id="a694a-165">If the certificate import is not successful, and you cannot establish a secure connection, consult the VMware vSphere documentation on [obtaining server certificates](http://pubs.vmware.com/vsphere-60/index.jsp#com.vmware.wssdk.dsg.doc/sdk_sg_server_certificate_Appendixes.6.4.html).</span></span>

  <span data-ttu-id="a694a-166">Se sono previsti limiti di protezione all'interno dell'organizzazione e non si vuole attivare il protocollo HTTPS, eseguire la procedura seguente per disabilitare le comunicazioni sicure.</span><span class="sxs-lookup"><span data-stu-id="a694a-166">If you have secure boundaries within your organization, and don't want to turn on the HTTPS protocol, use the following procedure to disable the secure communications.</span></span>

### <a name="disable-secure-communication-protocol"></a><span data-ttu-id="a694a-167">Disabilitazione del protocollo di comunicazione sicura</span><span class="sxs-lookup"><span data-stu-id="a694a-167">Disable secure communication protocol</span></span>

<span data-ttu-id="a694a-168">Se l'organizzazione non richiede il protocollo HTTPS, eseguire la procedura seguente per disabilitare questo protocollo.</span><span class="sxs-lookup"><span data-stu-id="a694a-168">If your organization doesn't require the HTTPS protocol, use the following steps to disable HTTPS.</span></span> <span data-ttu-id="a694a-169">Per disabilitare il comportamento predefinito, creare una chiave di registro che ignori il comportamento predefinito.</span><span class="sxs-lookup"><span data-stu-id="a694a-169">To disable the default behavior, create a registry key that ignores the default behavior.</span></span>

1. <span data-ttu-id="a694a-170">Copiare e incollare il seguente testo in un file .txt.</span><span class="sxs-lookup"><span data-stu-id="a694a-170">Copy and paste the following text into a .txt file.</span></span>

  ```
  Windows Registry Editor Version 5.00
  [HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Microsoft Data Protection Manager\VMWare]
  "IgnoreCertificateValidation"=dword:00000001
  ```

2. <span data-ttu-id="a694a-171">Salvare il file nel computer del server di Backup di Azure.</span><span class="sxs-lookup"><span data-stu-id="a694a-171">Save the file to your Azure Backup Server computer.</span></span> <span data-ttu-id="a694a-172">Come nome del file usare DisableSecureAuthentication.reg.</span><span class="sxs-lookup"><span data-stu-id="a694a-172">For the file name, use DisableSecureAuthentication.reg.</span></span>

3. <span data-ttu-id="a694a-173">Fare doppio clic sul file per attivare la voce del registro.</span><span class="sxs-lookup"><span data-stu-id="a694a-173">Double-click the file to activate the registry entry.</span></span>


## <a name="create-a-role-and-user-account-on-the-vcenter-server"></a><span data-ttu-id="a694a-174">Creare un ruolo e un account utente sul server vCenter</span><span class="sxs-lookup"><span data-stu-id="a694a-174">Create a role and user account on the vCenter Server</span></span>

<span data-ttu-id="a694a-175">Sul server vCenter, un ruolo è un set predefinito di privilegi.</span><span class="sxs-lookup"><span data-stu-id="a694a-175">On the vCenter Server, a role is a predefined set of privileges.</span></span> <span data-ttu-id="a694a-176">I ruoli vengono creati da un amministratore del server vCenter.</span><span class="sxs-lookup"><span data-stu-id="a694a-176">A vCenter Server administrator creates the roles.</span></span> <span data-ttu-id="a694a-177">Per assegnare le autorizzazioni, l'amministratore associa ogni account utente a un ruolo.</span><span class="sxs-lookup"><span data-stu-id="a694a-177">To assign permissions, the administrator pairs user accounts with a role.</span></span> <span data-ttu-id="a694a-178">Per definire le credenziali utente necessarie per eseguire il backup del computer del server vCenter, creare un ruolo con privilegi specifici e quindi associare l'account utente al ruolo.</span><span class="sxs-lookup"><span data-stu-id="a694a-178">To establish the necessary user credentials to back up the vCenter Server computer, create a role with specific privileges, and then associate the user account with the role.</span></span>

<span data-ttu-id="a694a-179">Per l'autenticazione con il server vCenter, il server di Backup di Azure usa un nome utente e una password.</span><span class="sxs-lookup"><span data-stu-id="a694a-179">Azure Backup Server uses a username and password to authenticate with the vCenter Server.</span></span> <span data-ttu-id="a694a-180">Il server di Backup di Azure sfrutta tali credenziali come autenticazione per ogni operazione di backup.</span><span class="sxs-lookup"><span data-stu-id="a694a-180">Azure Backup Server uses these credentials as authentication for all backup operations.</span></span>

<span data-ttu-id="a694a-181">Per aggiungere un ruolo del server vCenter e i relativi privilegi per un amministratore del backup:</span><span class="sxs-lookup"><span data-stu-id="a694a-181">To add a vCenter Server role and its privileges for a backup administrator:</span></span>

1. <span data-ttu-id="a694a-182">Accedere al server vCenter e quindi nel pannello **Navigator** (Strumento di navigazione) del server vCenter fare clic su **Administration** (Amministrazione).</span><span class="sxs-lookup"><span data-stu-id="a694a-182">Sign in to the vCenter Server, and then in the vCenter Server **Navigator** panel, click **Administration**.</span></span>

    ![Opzione Administration (Amministrazione) nel pannello Navigator (Strumento di navigazione) del server vCenter](./media/backup-azure-backup-server-vmware/vmware-navigator-panel.png)

2. <span data-ttu-id="a694a-184">In **Administration** (Amministrazione) selezionare **Roles** (Ruoli) e quindi nel pannello **Roles** (Ruoli) fare clic sull'icona Aggiungi ruolo (il simbolo +).</span><span class="sxs-lookup"><span data-stu-id="a694a-184">In **Administration** select **Roles**, and then in the **Roles** panel click the add role icon (the + symbol).</span></span>

    ![Aggiungi ruolo](./media/backup-azure-backup-server-vmware/vmware-define-new-role.png)

    <span data-ttu-id="a694a-186">Verrà visualizzata la finestra di dialogo **Create Role** (Crea ruolo).</span><span class="sxs-lookup"><span data-stu-id="a694a-186">The **Create Role** dialog box appears.</span></span>

    ![Create role (Crea ruolo)](./media/backup-azure-backup-server-vmware/vmware-define-new-role-priv.png)

3. <span data-ttu-id="a694a-188">Nella finestra di dialogo **Create Role** (Crea ruolo), nella casella **Role name** (Nome ruolo) immettere *BackupAdminRole*.</span><span class="sxs-lookup"><span data-stu-id="a694a-188">In the **Create Role** dialog box, in the **Role name** box, enter *BackupAdminRole*.</span></span> <span data-ttu-id="a694a-189">È possibile scegliere un nome qualsiasi, ma deve essere riconoscibile per lo scopo del ruolo.</span><span class="sxs-lookup"><span data-stu-id="a694a-189">The role name can be whatever you like, but it should be recognizable for the role's purpose.</span></span>

4. <span data-ttu-id="a694a-190">Selezionare i privilegi per la versione appropriata di vCenter e quindi fare clic su **OK**.</span><span class="sxs-lookup"><span data-stu-id="a694a-190">Select the privileges for the appropriate version of vCenter, and then click **OK**.</span></span> <span data-ttu-id="a694a-191">La tabella seguente identifica i privilegi obbligatori per vCenter 6.0 e vCenter 5.5.</span><span class="sxs-lookup"><span data-stu-id="a694a-191">The following table identifies the required privileges for vCenter 6.0 and vCenter 5.5.</span></span>

  <span data-ttu-id="a694a-192">Quando si selezionano i privilegi, fare clic sull'icona accanto all'etichetta padre per espandere l'elemento padre e visualizzare i privilegi figlio.</span><span class="sxs-lookup"><span data-stu-id="a694a-192">When you select the privileges, click the icon next to the parent label to expand the parent and view the child privileges.</span></span> <span data-ttu-id="a694a-193">Per selezionare i privilegi VirtualMachine, è necessario scendere di diversi livelli nella gerarchia padre-figlio.</span><span class="sxs-lookup"><span data-stu-id="a694a-193">To select the VirtualMachine privileges, you need to go several levels into the parent child hierarchy.</span></span> <span data-ttu-id="a694a-194">Non è necessario selezionare tutti i privilegi figlio all'interno di un privilegio padre.</span><span class="sxs-lookup"><span data-stu-id="a694a-194">You don't need to select all child privileges within a parent privilege.</span></span>

  ![Gerarchia di privilegi padre-figlio](./media/backup-azure-backup-server-vmware/cert-add-privilege-expand.png)

  <span data-ttu-id="a694a-196">Fare clic su **OK**. Il nuovo ruolo verrà visualizzato nell'elenco del pannello Roles (Ruoli).</span><span class="sxs-lookup"><span data-stu-id="a694a-196">After you click **OK**, the new role appears in the list on the Roles panel.</span></span>

|<span data-ttu-id="a694a-197">Privilegi per vCenter 6.0</span><span class="sxs-lookup"><span data-stu-id="a694a-197">Privileges for vCenter 6.0</span></span>| <span data-ttu-id="a694a-198">Privilegi per vCenter 5.5</span><span class="sxs-lookup"><span data-stu-id="a694a-198">Privileges for vCenter 5.5</span></span>|
|--------------------------|---------------------------|
|<span data-ttu-id="a694a-199">Datastore.AllocateSpace</span><span class="sxs-lookup"><span data-stu-id="a694a-199">Datastore.AllocateSpace</span></span>   | <span data-ttu-id="a694a-200">Datastore.AllocateSpace</span><span class="sxs-lookup"><span data-stu-id="a694a-200">Datastore.AllocateSpace</span></span>|
|<span data-ttu-id="a694a-201">Global.ManageCustomFields</span><span class="sxs-lookup"><span data-stu-id="a694a-201">Global.ManageCustomFields</span></span> | <span data-ttu-id="a694a-202">Global.ManageCustomerFields</span><span class="sxs-lookup"><span data-stu-id="a694a-202">Global.ManageCustomerFields</span></span>|
|<span data-ttu-id="a694a-203">Global.SetCustomFields</span><span class="sxs-lookup"><span data-stu-id="a694a-203">Global.SetCustomFields</span></span>    |   |
|<span data-ttu-id="a694a-204">Host.Local.CreateVM</span><span class="sxs-lookup"><span data-stu-id="a694a-204">Host.Local.CreateVM</span></span>       | <span data-ttu-id="a694a-205">Network.Assign</span><span class="sxs-lookup"><span data-stu-id="a694a-205">Network.Assign</span></span> |
|<span data-ttu-id="a694a-206">Network.Assign</span><span class="sxs-lookup"><span data-stu-id="a694a-206">Network.Assign</span></span>            |  |
|<span data-ttu-id="a694a-207">Resource.AssignVMToPool</span><span class="sxs-lookup"><span data-stu-id="a694a-207">Resource.AssignVMToPool</span></span>   |  |
|<span data-ttu-id="a694a-208">VirtualMachine.Config.AddNewDisk</span><span class="sxs-lookup"><span data-stu-id="a694a-208">VirtualMachine.Config.AddNewDisk</span></span>  | <span data-ttu-id="a694a-209">VirtualMachine.Config.AddNewDisk</span><span class="sxs-lookup"><span data-stu-id="a694a-209">VirtualMachine.Config.AddNewDisk</span></span>   |
|<span data-ttu-id="a694a-210">VirtualMachine.Config.AdvanceConfig</span><span class="sxs-lookup"><span data-stu-id="a694a-210">VirtualMachine.Config.AdvanceConfig</span></span>| <span data-ttu-id="a694a-211">VirtualMachine.Config.AdvancedConfig</span><span class="sxs-lookup"><span data-stu-id="a694a-211">VirtualMachine.Config.AdvancedConfig</span></span>|
|<span data-ttu-id="a694a-212">VirtualMachine.Config.ChangeTracking</span><span class="sxs-lookup"><span data-stu-id="a694a-212">VirtualMachine.Config.ChangeTracking</span></span>| <span data-ttu-id="a694a-213">VirtualMachine.Config.ChangeTracking</span><span class="sxs-lookup"><span data-stu-id="a694a-213">VirtualMachine.Config.ChangeTracking</span></span> |
|<span data-ttu-id="a694a-214">VirtualMachine.Config.HostUSBDevice</span><span class="sxs-lookup"><span data-stu-id="a694a-214">VirtualMachine.Config.HostUSBDevice</span></span>||
|<span data-ttu-id="a694a-215">VirtualMachine.Config.QueryUnownedFiles</span><span class="sxs-lookup"><span data-stu-id="a694a-215">VirtualMachine.Config.QueryUnownedFiles</span></span>|    |
|<span data-ttu-id="a694a-216">VirtualMachine.Config.SwapPlacement</span><span class="sxs-lookup"><span data-stu-id="a694a-216">VirtualMachine.Config.SwapPlacement</span></span>| <span data-ttu-id="a694a-217">VirtualMachine.Config.SwapPlacement</span><span class="sxs-lookup"><span data-stu-id="a694a-217">VirtualMachine.Config.SwapPlacement</span></span> |
|<span data-ttu-id="a694a-218">VirtualMachine.Interact.PowerOff</span><span class="sxs-lookup"><span data-stu-id="a694a-218">VirtualMachine.Interact.PowerOff</span></span>| <span data-ttu-id="a694a-219">VirtualMachine.Interact.PowerOff</span><span class="sxs-lookup"><span data-stu-id="a694a-219">VirtualMachine.Interact.PowerOff</span></span> |
|<span data-ttu-id="a694a-220">VirtualMachine.Inventory.Create</span><span class="sxs-lookup"><span data-stu-id="a694a-220">VirtualMachine.Inventory.Create</span></span>| <span data-ttu-id="a694a-221">VirtualMachine.Inventory.Create</span><span class="sxs-lookup"><span data-stu-id="a694a-221">VirtualMachine.Inventory.Create</span></span> |
|<span data-ttu-id="a694a-222">VirtualMachine.Provisioning.DiskRandomAccess</span><span class="sxs-lookup"><span data-stu-id="a694a-222">VirtualMachine.Provisioning.DiskRandomAccess</span></span>| |
|<span data-ttu-id="a694a-223">VirtualMachine.Provisioning.DiskRandomRead</span><span class="sxs-lookup"><span data-stu-id="a694a-223">VirtualMachine.Provisioning.DiskRandomRead</span></span>|<span data-ttu-id="a694a-224">VirtualMachine.Provisioning.DiskRandomRead</span><span class="sxs-lookup"><span data-stu-id="a694a-224">VirtualMachine.Provisioning.DiskRandomRead</span></span> |
|<span data-ttu-id="a694a-225">VirtualMachine.State.CreateSnapshot</span><span class="sxs-lookup"><span data-stu-id="a694a-225">VirtualMachine.State.CreateSnapshot</span></span>| <span data-ttu-id="a694a-226">VirtualMachine.State.CreateSnapshot</span><span class="sxs-lookup"><span data-stu-id="a694a-226">VirtualMachine.State.CreateSnapshot</span></span>|
|<span data-ttu-id="a694a-227">VirtualMachine.State.RemoveSnapshot</span><span class="sxs-lookup"><span data-stu-id="a694a-227">VirtualMachine.State.RemoveSnapshot</span></span>|<span data-ttu-id="a694a-228">VirtualMachine.State.RemoveSnapshot</span><span class="sxs-lookup"><span data-stu-id="a694a-228">VirtualMachine.State.RemoveSnapshot</span></span> |
</br>



## <a name="create-a-vcenter-server-user-account-and-permissions"></a><span data-ttu-id="a694a-229">Creare un account utente del server vCenter e le relative autorizzazioni</span><span class="sxs-lookup"><span data-stu-id="a694a-229">Create a vCenter Server user account and permissions</span></span>

<span data-ttu-id="a694a-230">Dopo aver configurato il ruolo con privilegi, creare un account utente.</span><span class="sxs-lookup"><span data-stu-id="a694a-230">After the role with privileges is set up, create a user account.</span></span> <span data-ttu-id="a694a-231">L'account utente è dotato di un nome utente e di una password, che rappresentano le credenziali usate per l'autenticazione.</span><span class="sxs-lookup"><span data-stu-id="a694a-231">The user account has a name and password, which provides the credentials that are used for authentication.</span></span>

1. <span data-ttu-id="a694a-232">Per creare un account utente, nel pannello **Navigator** (Strumento di navigazione) del server vCenter fare clic su **Users and Groups** (Utenti e gruppi).</span><span class="sxs-lookup"><span data-stu-id="a694a-232">To create a user account, in the vCenter Server **Navigator** panel, click **Users and Groups**.</span></span>

    ![Opzione Users and Groups (Utenti e gruppi)](./media/backup-azure-backup-server-vmware/vmware-userandgroup-panel.png)

    <span data-ttu-id="a694a-234">Verrà visualizzato il pannello **vCenter Users and Groups** (Utenti e gruppi di vCenter).</span><span class="sxs-lookup"><span data-stu-id="a694a-234">The **vCenter Users and Groups** panel appears.</span></span>

    ![Pannello vCenter Users and Groups (Utenti e gruppi di vCenter)](./media/backup-azure-backup-server-vmware/usersandgroups.png)

2. <span data-ttu-id="a694a-236">Nel pannello **vCenter Users and Groups** (Utenti e gruppi di vCenter) selezionare la scheda **Users** (Utenti) e quindi fare clic sull'icona Aggiungi utenti (il simbolo +).</span><span class="sxs-lookup"><span data-stu-id="a694a-236">In the **vCenter Users and Groups** panel, select the **Users** tab, and then click the add users icon (the + symbol).</span></span>

    <span data-ttu-id="a694a-237">Verrà visualizzata la finestra di dialogo **New User** (Nuovo utente).</span><span class="sxs-lookup"><span data-stu-id="a694a-237">The **New User** dialog box appears.</span></span>

3. <span data-ttu-id="a694a-238">Nella finestra di dialogo **New User** (Nuovo utente) aggiungere le informazioni dell'utente e quindi fare clic su **OK**.</span><span class="sxs-lookup"><span data-stu-id="a694a-238">In the **New User** dialog box, add the user's information and then click **OK**.</span></span> <span data-ttu-id="a694a-239">In questa procedura il nome utente è BackupAdmin.</span><span class="sxs-lookup"><span data-stu-id="a694a-239">In this procedure, the username is BackupAdmin.</span></span>

    ![Finestra di dialogo New User (Nuovo utente)](./media/backup-azure-backup-server-vmware/vmware-new-user-account.png)

    <span data-ttu-id="a694a-241">Il nuovo account utente viene visualizzato nell'elenco.</span><span class="sxs-lookup"><span data-stu-id="a694a-241">The new user account appears in the list.</span></span>

4. <span data-ttu-id="a694a-242">Per associare l'account utente al ruolo, nel pannello **Navigator** (Strumento di navigazione) fare clic su **Global Permissions** (Autorizzazioni globali).</span><span class="sxs-lookup"><span data-stu-id="a694a-242">To associate the user account with the role, in the **Navigator** panel, click **Global Permissions**.</span></span> <span data-ttu-id="a694a-243">Nel pannello **Global Permissions** (Autorizzazioni globali) selezionare la scheda **Manage** (Gestisci) e quindi fare clic sull'icona Aggiungi (il simbolo +).</span><span class="sxs-lookup"><span data-stu-id="a694a-243">In the **Global Permissions** panel, select the **Manage** tab, and then click the add icon (the + symbol).</span></span>

    ![Pannello Global Permissions (Autorizzazioni globali)](./media/backup-azure-backup-server-vmware/vmware-add-new-perms.png)

    <span data-ttu-id="a694a-245">Verrà visualizzata la finestra di dialogo **Global Permissions Root - Add Permission** (Radice autorizzazioni globali - Aggiungi autorizzazione).</span><span class="sxs-lookup"><span data-stu-id="a694a-245">The **Global Permissions Root - Add Permission** dialog box appears.</span></span>

5. <span data-ttu-id="a694a-246">Nella finestra di dialogo **Global Permission Root - Add Permission** (Radice autorizzazioni globali - Aggiungi autorizzazione) fare clic su **Add** (Aggiungi) per scegliere l'utente o il gruppo.</span><span class="sxs-lookup"><span data-stu-id="a694a-246">In the **Global Permission Root - Add Permission** dialog box, click **Add** to choose the user or group.</span></span>

    ![Scegliere un utente o un gruppo](./media/backup-azure-backup-server-vmware/vmware-add-new-global-perm.png)

    <span data-ttu-id="a694a-248">Verrà visualizzata la finestra di dialogo **Select Users/Groups** (Seleziona utenti/gruppi).</span><span class="sxs-lookup"><span data-stu-id="a694a-248">The **Select Users/Groups** dialog box appears.</span></span>

6. <span data-ttu-id="a694a-249">Nella finestra di dialogo **Select Users/Groups** (Seleziona utenti/gruppi) scegliere **BackupAdmin** e fare clic su **Add** (Aggiungi).</span><span class="sxs-lookup"><span data-stu-id="a694a-249">In the **Select Users/Groups** dialog box, choose **BackupAdmin** and then click **Add**.</span></span>

    <span data-ttu-id="a694a-250">In **Users** (Utenti) per l'account utente viene usato il formato *dominio\nomeutente*.</span><span class="sxs-lookup"><span data-stu-id="a694a-250">In **Users**, the *domain\username* format is used for the user account.</span></span> <span data-ttu-id="a694a-251">Per usare un dominio diverso, sceglierlo dall'elenco **Domain** (Domini).</span><span class="sxs-lookup"><span data-stu-id="a694a-251">If you want to use a different domain, choose it from the **Domain** list.</span></span>

    ![Aggiungere l'utente BackupAdmin](./media/backup-azure-backup-server-vmware/vmware-assign-account-to-role.png)

    <span data-ttu-id="a694a-253">Fare clic su **OK** per aggiungere gli utenti selezionati alla finestra di dialogo **Add Permission** (Aggiungi autorizzazione).</span><span class="sxs-lookup"><span data-stu-id="a694a-253">Click **OK** to add the selected users to the **Add Permission** dialog box.</span></span>

7. <span data-ttu-id="a694a-254">Dopo avere identificato l'utente, assegnare l'utente al ruolo.</span><span class="sxs-lookup"><span data-stu-id="a694a-254">Now that you've identified the user, assign the user to the role.</span></span> <span data-ttu-id="a694a-255">In **Assigned Role** (Ruolo assegnato) selezionare **BackupAdminRole** nell'elenco e quindi fare clic su **OK**.</span><span class="sxs-lookup"><span data-stu-id="a694a-255">In **Assigned Role**, from the drop-down list, select **BackupAdminRole**, and then click **OK**.</span></span>

    ![Assegnare l'utente a un ruolo](./media/backup-azure-backup-server-vmware/vmware-choose-role.png)

  <span data-ttu-id="a694a-257">Il nuovo account utente e il ruolo associato vengono visualizzati nell'elenco nella scheda **Manage** (Gestisci) del pannello **Global Permissions** (Autorizzazioni globali).</span><span class="sxs-lookup"><span data-stu-id="a694a-257">On the **Manage** tab in the **Global Permissions** panel, the new user account and the associated role appear in the list.</span></span>


## <a name="establish-vcenter-server-credentials-on-azure-backup-server"></a><span data-ttu-id="a694a-258">Definizione di credenziali del server vCenter sul server di Backup di Azure</span><span class="sxs-lookup"><span data-stu-id="a694a-258">Establish vCenter Server credentials on Azure Backup Server</span></span>

<span data-ttu-id="a694a-259">Prima di aggiungere il server VMware al server di Backup di Azure, installare l'[aggiornamento 1 per il server di Backup di Azure](https://support.microsoft.com/help/3175529/update-1-for-microsoft-azure-backup-server).</span><span class="sxs-lookup"><span data-stu-id="a694a-259">Before you add the VMware server to Azure Backup Server, install [Update 1 for Azure Backup Server](https://support.microsoft.com/help/3175529/update-1-for-microsoft-azure-backup-server).</span></span>

1. <span data-ttu-id="a694a-260">Per aprire il server di Backup di Azure, fare doppio clic sull'icona sul desktop del server di Backup di Azure.</span><span class="sxs-lookup"><span data-stu-id="a694a-260">To open Azure Backup Server, double-click the icon on the Azure Backup Server desktop.</span></span>

    ![Icona del server di Backup di Azure](./media/backup-azure-backup-server-vmware/mabs-icon.png)

    <span data-ttu-id="a694a-262">Se l'icona non è presente sul desktop, aprire il server di Backup di Azure nell'elenco delle app installate.</span><span class="sxs-lookup"><span data-stu-id="a694a-262">If you can't find the icon on the desktop, open Azure Backup Server from the list of installed apps.</span></span> <span data-ttu-id="a694a-263">Il nome dell'app del server di Backup di Azure è Backup di Microsoft Azure.</span><span class="sxs-lookup"><span data-stu-id="a694a-263">The Azure Backup Server app name is called Microsoft Azure Backup.</span></span>

2. <span data-ttu-id="a694a-264">Nella console del server di Backup di Azure fare clic su **Gestione**, su **Server di produzione** e quindi sulla barra multifunzione fare clic su **Gestisci VMware**.</span><span class="sxs-lookup"><span data-stu-id="a694a-264">In the Azure Backup Server console, click **Management**, click **Production Servers**, and then on the tool ribbon, click **Manage VMware**.</span></span>

    ![Console del server di Backup di Azure](./media/backup-azure-backup-server-vmware/add-vmware-credentials.png)

    <span data-ttu-id="a694a-266">Verrà visualizzata la finestra di dialogo **Gestisci credenziali**.</span><span class="sxs-lookup"><span data-stu-id="a694a-266">The **Manage Credentials** dialog box appears.</span></span>

    ![Finestra di dialogo Gestisci credenziali del server di Backup di Azure](./media/backup-azure-backup-server-vmware/mabs-manage-credentials-dialog.png)

3. <span data-ttu-id="a694a-268">Nella finestra di dialogo **Gestisci credenziali** fare clic su **Aggiungi** per aprire la finestra di dialogo **Aggiungi credenziali**.</span><span class="sxs-lookup"><span data-stu-id="a694a-268">In the **Manage Credentials** dialog box, click **Add** to open the **Add Credential** dialog box.</span></span>

4. <span data-ttu-id="a694a-269">Nella finestra di dialogo **Aggiungi credenziali** immettere il nome e la descrizione delle nuove credenziali.</span><span class="sxs-lookup"><span data-stu-id="a694a-269">In the **Add Credential** dialog box, enter a name and a description for the new credential.</span></span> <span data-ttu-id="a694a-270">e quindi specificare il nome utente e la password.</span><span class="sxs-lookup"><span data-stu-id="a694a-270">Then specify the username and password.</span></span> <span data-ttu-id="a694a-271">Il nome *Contoso Vcenter credential*, verrà usato per identificare le credenziali nella procedura successiva.</span><span class="sxs-lookup"><span data-stu-id="a694a-271">The name, *Contoso Vcenter credential* is used to identify the credential in the next procedure.</span></span> <span data-ttu-id="a694a-272">Usare lo stesso nome utente e la stessa password usati per il server vCenter.</span><span class="sxs-lookup"><span data-stu-id="a694a-272">Use the same username and password that is used for the vCenter Server.</span></span> <span data-ttu-id="a694a-273">Se il server vCenter e il server di Backup di Azure non sono nello stesso dominio, specificare il dominio in **Nome utente**.</span><span class="sxs-lookup"><span data-stu-id="a694a-273">If the vCenter Server and Azure Backup Server are not in the same domain, in **User name**, specify the domain.</span></span>

    ![Finestra di dialogo Aggiungi credenziali del server di Backup di Azure](./media/backup-azure-backup-server-vmware/mabs-add-credential-dialog2.png)

    <span data-ttu-id="a694a-275">Fare clic su **Aggiungi** per aggiungere le nuove credenziali al server di Backup di Azure.</span><span class="sxs-lookup"><span data-stu-id="a694a-275">Click **Add** to add the new credential to Azure Backup Server.</span></span> <span data-ttu-id="a694a-276">Le nuove credenziali vengono visualizzate nell'elenco della finestra di dialogo **Gestisci credenziali**.</span><span class="sxs-lookup"><span data-stu-id="a694a-276">The new credential appears in the list in the **Manage Credentials** dialog box.</span></span>
    
    ![Finestra di dialogo Gestisci credenziali del server di Backup di Azure](./media/backup-azure-backup-server-vmware/new-list-of-mabs-creds.png)

5. <span data-ttu-id="a694a-278">Per chiudere la finestra di dialogo **Gestisci credenziali**, fare clic sulla **X** nell'angolo superiore destro.</span><span class="sxs-lookup"><span data-stu-id="a694a-278">To close the **Manage Credentials** dialog box, click the **X** in the upper-right corner.</span></span>


## <a name="add-the-vcenter-server-to-azure-backup-server"></a><span data-ttu-id="a694a-279">Aggiunta del server VMware al server di Backup di Azure</span><span class="sxs-lookup"><span data-stu-id="a694a-279">Add the vCenter Server to Azure Backup Server</span></span>

<span data-ttu-id="a694a-280">Per aggiungere il server vCenter al server di Backup di Azure, si usa l'Aggiunta guidata server di produzione.</span><span class="sxs-lookup"><span data-stu-id="a694a-280">Production Server Addition Wizard is used to add the vCenter Server to Azure Backup Server.</span></span>

<span data-ttu-id="a694a-281">Per aprire l'Aggiunta guidata server di produzione, completare la procedura seguente:</span><span class="sxs-lookup"><span data-stu-id="a694a-281">To open Production Server Addition Wizard, complete the following procedure:</span></span>

1. <span data-ttu-id="a694a-282">Nella console del server di Backup di Azure fare clic su **Gestione**, su **Server di produzione** e quindi su **Aggiungi**.</span><span class="sxs-lookup"><span data-stu-id="a694a-282">In the Azure Backup Server console, click **Management**, click **Production Servers**, and then click **Add**.</span></span>

    ![Aprire l'Aggiunta guidata server di produzione](./media/backup-azure-backup-server-vmware/add-vcenter-to-mabs.png)

    <span data-ttu-id="a694a-284">Verrà visualizzata la finestra di dialogo **Aggiunta guidata server di produzione**.</span><span class="sxs-lookup"><span data-stu-id="a694a-284">The **Production Server Addition Wizard** dialog box appears.</span></span>

    ![Aggiunta guidata server di produzione](./media/backup-azure-backup-server-vmware/production-server-add-wizard.png)

2. <span data-ttu-id="a694a-286">Nella pagina **Selezionare il tipo di server di produzione** selezionare **Server VMware** e quindi fare clic su **Avanti**.</span><span class="sxs-lookup"><span data-stu-id="a694a-286">On the **Select Production Server type** page, select **VMware Servers**, and then click **Next**.</span></span>

3. <span data-ttu-id="a694a-287">In **Nome del server/Indirizzo IP** specificare il nome di dominio completo (FQDN, Fully Qualified Domain Name) o l'indirizzo IP del server VMware.</span><span class="sxs-lookup"><span data-stu-id="a694a-287">In **Server Name/IP Address**, specify the fully qualified domain name (FQDN) or IP address of the VMware server.</span></span> <span data-ttu-id="a694a-288">Se tutti i server ESXi sono gestiti dallo stesso vCenter, è possibile usare il nome vCenter.</span><span class="sxs-lookup"><span data-stu-id="a694a-288">If all the ESXi servers are managed by the same vCenter, you can use the vCenter name.</span></span>

    ![Specificare l'FQDN o l'indirizzo IP del server VMware](./media/backup-azure-backup-server-vmware/add-vmware-server-provide-server-name.png)

4. <span data-ttu-id="a694a-290">In **Porta SSL** immettere la porta usata per comunicare con il server VMware.</span><span class="sxs-lookup"><span data-stu-id="a694a-290">In **SSL Port**, enter the port that is used to communicate with the VMware server.</span></span> <span data-ttu-id="a694a-291">Usare la porta 443, ovvero la porta predefinita, a meno che non sia necessaria una porta diversa.</span><span class="sxs-lookup"><span data-stu-id="a694a-291">Use port 443, which is the default port, unless you know that a different port is required.</span></span>

5. <span data-ttu-id="a694a-292">In **Specifica credenziale** selezionare le credenziali create in precedenza.</span><span class="sxs-lookup"><span data-stu-id="a694a-292">In **Specify Credential**, select the credential that you created earlier.</span></span>

    ![Specifica credenziale](./media/backup-azure-backup-server-vmware/identify-creds.png)

6. <span data-ttu-id="a694a-294">Fare clic su **Aggiungi** per aggiungere il server VMware all'elenco **Server VMware aggiunti** e quindi fare clic su **Avanti** per passare alla pagina successiva della procedura guidata.</span><span class="sxs-lookup"><span data-stu-id="a694a-294">Click **Add** to add the VMware server to the list of **Added VMware Servers**, and then click **Next** to move to the next page in the wizard.</span></span>

    ![Aggiungere il server VMware e le credenziali](./media/backup-azure-backup-server-vmware/add-vmware-server-credentials.png)

7. <span data-ttu-id="a694a-296">Nella pagina **Riepilogo** fare clic su **Aggiungi** per aggiungere il server VMware specificato al server di Backup di Azure.</span><span class="sxs-lookup"><span data-stu-id="a694a-296">In the **Summary** page, click **Add** to add the specified VMware server to Azure Backup Server.</span></span>

    ![Aggiungere il server VMware al server di Backup di Azure](./media/backup-azure-backup-server-vmware/tasks-screen.png)

  <span data-ttu-id="a694a-298">Il backup del server VMware è un backup senza agente. Il nuovo server viene quindi aggiunto immediatamente.</span><span class="sxs-lookup"><span data-stu-id="a694a-298">The VMware server backup is an agentless backup, and the new server is added immediately.</span></span> <span data-ttu-id="a694a-299">Nella pagina **Fine** vengono visualizzati i risultati.</span><span class="sxs-lookup"><span data-stu-id="a694a-299">The **Finish** page shows you the results.</span></span>

  ![Pagina Fine](./media/backup-azure-backup-server-vmware/summary-screen.png)

  <span data-ttu-id="a694a-301">Per aggiungere più istanze del server vCenter al server di Backup di Azure, ripetere la procedura riportata in precedenza in questa sezione.</span><span class="sxs-lookup"><span data-stu-id="a694a-301">To add multiple instances of vCenter Server to Azure Backup Server, repeat the previous steps in this section.</span></span>

<span data-ttu-id="a694a-302">Dopo avere aggiunto un server vCenter al server di Backup di Azure, il passaggio successivo consiste nel creare un gruppo protezione dati.</span><span class="sxs-lookup"><span data-stu-id="a694a-302">After you add the vCenter Server to Azure Backup Server, the next step is to create a protection group.</span></span> <span data-ttu-id="a694a-303">Il gruppo protezione dati specifica i vari dettagli per la conservazione a lungo o a breve termine e consente di definire e applicare i criteri di backup.</span><span class="sxs-lookup"><span data-stu-id="a694a-303">The protection group specifies the various details for short or long-term retention, and it is where you define and apply the backup policy.</span></span> <span data-ttu-id="a694a-304">I criteri di backup corrispondono alla pianificazione del momento in cui vengono eseguiti i backup e a ciò di cui viene eseguito il backup.</span><span class="sxs-lookup"><span data-stu-id="a694a-304">The backup policy is the schedule for when backups occur, and what is backed up.</span></span>


## <a name="configure-a-protection-group"></a><span data-ttu-id="a694a-305">Configurazione di un gruppo protezione dati</span><span class="sxs-lookup"><span data-stu-id="a694a-305">Configure a protection group</span></span>

<span data-ttu-id="a694a-306">Se non si è mai usato System Center Data Protection Manager o il server di Backup di Azure, vedere [Pianificare i backup su disco](https://technet.microsoft.com/library/hh758026.aspx) per preparare l'ambiente hardware.</span><span class="sxs-lookup"><span data-stu-id="a694a-306">If you have not used System Center Data Protection Manager or Azure Backup Server before, see [Plan for disk backups](https://technet.microsoft.com/library/hh758026.aspx) to prepare your hardware environment.</span></span> <span data-ttu-id="a694a-307">Dopo avere verificato la disponibilità di una risorsa di archiviazione appropriata, eseguire la procedura guidata Crea nuovo gruppo protezione dati per aggiungere macchine virtuali VMware.</span><span class="sxs-lookup"><span data-stu-id="a694a-307">After you check that you have proper storage, use the Create New Protection Group wizard to add VMware virtual machines.</span></span>

1. <span data-ttu-id="a694a-308">Nella console del server di Backup di Azure fare clic su **Protezione** e quindi fare clic su **Nuovo** nella barra multifunzione per aprire la procedura guidata Crea nuovo gruppo protezione dati.</span><span class="sxs-lookup"><span data-stu-id="a694a-308">In the Azure Backup Server console, click **Protection**, and in the tool ribbon, click **New** to open the Create New Protection Group wizard.</span></span>

    ![Aprire la procedura guidata Crea nuovo gruppo protezione dati](./media/backup-azure-backup-server-vmware/open-protection-wizard.png)

    <span data-ttu-id="a694a-310">Verrà visualizzata la finestra di dialogo della procedura guidata **Crea nuovo gruppo protezione dati**.</span><span class="sxs-lookup"><span data-stu-id="a694a-310">The **Create New Protection Group** wizard dialog box appears.</span></span>

    ![Finestra di dialogo della procedura guidata Crea nuovo gruppo protezione dati](./media/backup-azure-backup-server-vmware/protection-wizard.png)

    <span data-ttu-id="a694a-312">Fare clic su **Avanti** per passare alla pagina **Selezione tipo di gruppo protezione dati**.</span><span class="sxs-lookup"><span data-stu-id="a694a-312">Click **Next** to advance to the **Select protection group type** page.</span></span>

2. <span data-ttu-id="a694a-313">Nella pagina **Selezione tipo di gruppo protezione dati** selezionare **Server** e quindi fare clic su **Avanti**.</span><span class="sxs-lookup"><span data-stu-id="a694a-313">On the **Select Protection group type** page, select **Servers** and then click **Next**.</span></span> <span data-ttu-id="a694a-314">Verrà visualizzata la pagina **Selezione membri del gruppo**.</span><span class="sxs-lookup"><span data-stu-id="a694a-314">The **Select group members** page appears.</span></span>

3. <span data-ttu-id="a694a-315">Nella pagina **Selezione membri del gruppo** sono visualizzati i membri disponibili e quelli selezionati.</span><span class="sxs-lookup"><span data-stu-id="a694a-315">On the **Select group members** page, the available members and the selected members appear.</span></span> <span data-ttu-id="a694a-316">Selezionare i membri da proteggere e quindi fare clic su **Avanti**.</span><span class="sxs-lookup"><span data-stu-id="a694a-316">Select the members that you want to protect, and then click **Next**.</span></span>

    ![Seleziona membri del gruppo](./media/backup-azure-backup-server-vmware/server-add-selected-members.png)

    <span data-ttu-id="a694a-318">Quando si seleziona un membro, se si seleziona una cartella che contiene altre cartelle o macchine virtuali, vengono selezionate anche le cartelle e le macchine virtuali contenute.</span><span class="sxs-lookup"><span data-stu-id="a694a-318">When you select a member, if you select a folder that contains other folders or VMs, those folders and VMs are also selected.</span></span> <span data-ttu-id="a694a-319">L'inclusione di cartelle e VM nella cartella padre è denominata protezione a livello di cartella.</span><span class="sxs-lookup"><span data-stu-id="a694a-319">The inclusion of the folders and VMs in the parent folder is called folder-level protection.</span></span> <span data-ttu-id="a694a-320">Per rimuovere una cartella o una macchina virtuale, deselezionare la casella di controllo corrispondente.</span><span class="sxs-lookup"><span data-stu-id="a694a-320">To remove a folder or VM, clear the check box.</span></span>

    <span data-ttu-id="a694a-321">Se una VM o una cartella che contiene una VM, è già protetta in Azure, non è possibile selezionarla di nuovo.</span><span class="sxs-lookup"><span data-stu-id="a694a-321">If a VM, or a folder containing a VM, is already protected to Azure, you cannot select that VM again.</span></span> <span data-ttu-id="a694a-322">In altre parole, se una macchina virtuale è protetta in Azure, non è possibile applicare di nuovo la protezione per evitare di creare punti di recupero duplicati per la macchina virtuale stessa.</span><span class="sxs-lookup"><span data-stu-id="a694a-322">That is, after a VM is protected to Azure, it cannot be protected again, which prevents duplicate recovery points from being created for one VM.</span></span> <span data-ttu-id="a694a-323">Se si vuole visualizzare l'istanza del server di Backup di Azure che protegge già un membro, posizionare il mouse sopra il membro per visualizzare il nome del server di protezione.</span><span class="sxs-lookup"><span data-stu-id="a694a-323">If you want to see which Azure Backup Server instance already protects a member, point to the member to see the name of the protecting server.</span></span>

4. <span data-ttu-id="a694a-324">Nella pagina **Seleziona metodo protezione dati** immettere un nome per il gruppo protezione dati.</span><span class="sxs-lookup"><span data-stu-id="a694a-324">On the **Select Data Protection Method** page, enter a name for the protection group.</span></span> <span data-ttu-id="a694a-325">Sono selezionate la protezione a breve termine (su disco) e la protezione online.</span><span class="sxs-lookup"><span data-stu-id="a694a-325">Short-term protection (to disk) and online protection are selected.</span></span> <span data-ttu-id="a694a-326">Per utilizzare la protezione online (su Azure), è necessario utilizzare la protezione a breve termine su disco.</span><span class="sxs-lookup"><span data-stu-id="a694a-326">If you want to use online protection (to Azure), you must use short-term protection to disk.</span></span> <span data-ttu-id="a694a-327">Fare clic su **Avanti** per procedere con l'intervallo di protezione a breve termine.</span><span class="sxs-lookup"><span data-stu-id="a694a-327">Click **Next** to proceed to the short-term protection range.</span></span>

    ![Seleziona metodo protezione dati](./media/backup-azure-backup-server-vmware/name-protection-group.png)

5. <span data-ttu-id="a694a-329">Nella pagina **Specifica obiettivi a breve termine** per **Intervallo di conservazione** specificare il numero di giorni per cui si vogliono mantenere i punti di recupero *archiviati su disco*.</span><span class="sxs-lookup"><span data-stu-id="a694a-329">On the **Specify Short-Term Goals** page, for **Retention Range**, specify the number of days that you want to retain recovery points that are *stored to disk*.</span></span> <span data-ttu-id="a694a-330">Se si vuole modificare l'ora e i giorni in cui vengono eseguiti i punti di recupero, fare clic su **Modifica**.</span><span class="sxs-lookup"><span data-stu-id="a694a-330">If you want to change the time and days when recovery points are taken, click **Modify**.</span></span> <span data-ttu-id="a694a-331">I punti di recupero a breve termine sono backup completi</span><span class="sxs-lookup"><span data-stu-id="a694a-331">The short-term recovery points are full backups.</span></span> <span data-ttu-id="a694a-332">e non backup incrementali.</span><span class="sxs-lookup"><span data-stu-id="a694a-332">They are not incremental backups.</span></span> <span data-ttu-id="a694a-333">Quando si è soddisfatti degli obiettivi a breve termine, fare clic su **Avanti**.</span><span class="sxs-lookup"><span data-stu-id="a694a-333">When you are satisfied with the short-term goals, click **Next**.</span></span>

    ![Specifica obiettivi a breve termine](./media/backup-azure-backup-server-vmware/short-term-goals.png)

6. <span data-ttu-id="a694a-335">Nella pagina **Verifica allocazione dischi** esaminare e, se necessario, modificare lo spazio su disco per le macchine virtuali.</span><span class="sxs-lookup"><span data-stu-id="a694a-335">On the **Review Disk Allocation** page, review and if necessary, modify the disk space for the VMs.</span></span> <span data-ttu-id="a694a-336">Le allocazioni dischi consigliate sono basate sul periodo di mantenimento dati specificato nella pagina **Specifica obiettivi a breve termine**, sul tipo di carico di lavoro e sulle dimensioni dei dati protetti (identificati nel passaggio 3).</span><span class="sxs-lookup"><span data-stu-id="a694a-336">The recommended disk allocations are based on the retention range that is specified in the **Specify Short-Term Goals** page, the type of workload, and the size of the protected data (identified in step 3).</span></span>  

  - <span data-ttu-id="a694a-337">**Dimensione dati:** la dimensione dei dati nel gruppo protezione dati.</span><span class="sxs-lookup"><span data-stu-id="a694a-337">**Data size:** Size of the data in the protection group.</span></span>
  - <span data-ttu-id="a694a-338">**Spazio su disco:** la quantità di spazio su disco consigliata per il gruppo protezione dati.</span><span class="sxs-lookup"><span data-stu-id="a694a-338">**Disk space:** The recommended amount of disk space for the protection group.</span></span> <span data-ttu-id="a694a-339">Se si vuole modificare questa impostazione, è consigliabile allocare uno spazio totale leggermente superiore rispetto alla quantità stimata per la crescita di ogni origine dati.</span><span class="sxs-lookup"><span data-stu-id="a694a-339">If you want to modify this setting, you should allocate total space that is slightly larger than the amount that you estimate each data source grows.</span></span>
  - <span data-ttu-id="a694a-340">**Condividi percorso dati:** se si attiva la condivisione del percorso dati, è possibile eseguire il mapping di più origini dati nella protezione a un'unica replica e a un unico volume del punto di recupero.</span><span class="sxs-lookup"><span data-stu-id="a694a-340">**Colocate data:** If you turn on colocation, multiple data sources in the protection can map to a single replica and recovery point volume.</span></span> <span data-ttu-id="a694a-341">La condivisione del percorso non è supportata per tutti i carichi di lavoro.</span><span class="sxs-lookup"><span data-stu-id="a694a-341">Colocation isn't supported for all workloads.</span></span>
  - <span data-ttu-id="a694a-342">**Aumenta automaticamente:** se si attiva questa impostazione e i dati del gruppo protezione superano l'allocazione iniziale, System Center Data Protection Manager tenta di aumentare le dimensioni del disco del 25%.</span><span class="sxs-lookup"><span data-stu-id="a694a-342">**Automatically grow:** If you turn on this setting, if data in the protected group outgrows the initial allocation, System Center Data Protection Manager tries to increase the disk size by 25 percent.</span></span>
  - <span data-ttu-id="a694a-343">**Dettagli pool di archiviazione:** visualizza lo stato del pool di archiviazione, incluse dimensione totale e dimensione rimanente dei dischi.</span><span class="sxs-lookup"><span data-stu-id="a694a-343">**Storage pool details:** Shows the status of the storage pool, including total and remaining disk size.</span></span>

    ![Rivedere l'allocazione dei dischi](./media/backup-azure-backup-server-vmware/review-disk-allocation.png)

    <span data-ttu-id="a694a-345">Una volta ottenuta l’allocazione di spazio adeguata, fare clic su **Avanti**.</span><span class="sxs-lookup"><span data-stu-id="a694a-345">When you are satisfied with the space allocation, click **Next**.</span></span>

7. <span data-ttu-id="a694a-346">Nella pagina **Scelta del metodo per la creazione della replica** specificare come si vuole generare la copia iniziale, o la replica, dei dati protetti nel server di Backup di Azure.</span><span class="sxs-lookup"><span data-stu-id="a694a-346">On the **Choose Replica Creation Method** page, specify how you want to generate the initial copy, or replica, of the protected data on Azure Backup Server.</span></span>

    <span data-ttu-id="a694a-347">Il valore predefinito è **Automaticamente tramite rete** e **Ora**.</span><span class="sxs-lookup"><span data-stu-id="a694a-347">The default is **Automatically over the network** and **Now**.</span></span> <span data-ttu-id="a694a-348">Se si usa il valore predefinito, è consigliabile specificare un'ora non di punta.</span><span class="sxs-lookup"><span data-stu-id="a694a-348">If you use the default, we recommend that you specify an off-peak time.</span></span> <span data-ttu-id="a694a-349">Scegliere **In seguito** e specificare un giorno e un'ora.</span><span class="sxs-lookup"><span data-stu-id="a694a-349">Choose **Later** and specify a day and time.</span></span>

    <span data-ttu-id="a694a-350">Per grandi quantità di dati o condizioni della rete non ottimali, tenere in considerazione la replica dei dati offline tramite supporti di memorizzazione rimovibili.</span><span class="sxs-lookup"><span data-stu-id="a694a-350">For large amounts of data or less-than-optimal network conditions, consider replicating the data offline by using removable media.</span></span>

    <span data-ttu-id="a694a-351">Dopo avere effettuato le scelte, fare clic su **Avanti**.</span><span class="sxs-lookup"><span data-stu-id="a694a-351">After you have made your choices, click **Next**.</span></span>

    ![Scelta del metodo per la creazione della replica](./media/backup-azure-backup-server-vmware/replica-creation.png)

8. <span data-ttu-id="a694a-353">Nella pagina **Opzioni di verifica coerenza** selezionare come e quando automatizzare le verifiche della coerenza.</span><span class="sxs-lookup"><span data-stu-id="a694a-353">On the **Consistency Check Options** page, select how and when to automate the consistency checks.</span></span> <span data-ttu-id="a694a-354">È possibile eseguire verifiche della coerenza quando i dati di replica diventano incoerenti o in base a una pianificazione impostata.</span><span class="sxs-lookup"><span data-stu-id="a694a-354">You can run consistency checks when replica data becomes inconsistent, or on a set schedule.</span></span>

    <span data-ttu-id="a694a-355">Per non configurare la verifica automatica della coerenza, è possibile eseguire una verifica manuale.</span><span class="sxs-lookup"><span data-stu-id="a694a-355">If you don't want to configure automatic consistency checks, you can run a manual check.</span></span> <span data-ttu-id="a694a-356">Nell'area di protezione della console del server di Backup di Azure fare clic con il pulsante destro del mouse sul gruppo protezione dati e quindi selezionare **Esegui verifica coerenza**.</span><span class="sxs-lookup"><span data-stu-id="a694a-356">In the protection area of the Azure Backup Server console, right-click the protection group and then select **Perform Consistency Check**.</span></span>

    <span data-ttu-id="a694a-357">Fare clic su **Avanti** per passare alla pagina successiva.</span><span class="sxs-lookup"><span data-stu-id="a694a-357">Click **Next** to move to the next page.</span></span>

9. <span data-ttu-id="a694a-358">Nella pagina **Specifica i dati da proteggere online** selezionare una o più origini dati da proteggere.</span><span class="sxs-lookup"><span data-stu-id="a694a-358">On the **Specify Online Protection Data** page, select one or more data sources that you want to protect.</span></span> <span data-ttu-id="a694a-359">È possibile selezionare i membri singolarmente o fare clic su **Seleziona tutto** per scegliere tutti i membri.</span><span class="sxs-lookup"><span data-stu-id="a694a-359">You can select the members individually, or click **Select All** to choose all members.</span></span> <span data-ttu-id="a694a-360">Dopo avere scelto i membri, fare clic su **Avanti**.</span><span class="sxs-lookup"><span data-stu-id="a694a-360">After you choose the members, click **Next**.</span></span>

    ![Specifica i dati da proteggere online](./media/backup-azure-backup-server-vmware/select-data-to-protect.png)

10. <span data-ttu-id="a694a-362">Nella pagina **Specificare la pianificazione dei backup online** specificare la pianificazione per la generazione di punti di recupero dal backup del disco.</span><span class="sxs-lookup"><span data-stu-id="a694a-362">On the **Specify Online Backup Schedule** page, specify the schedule to generate recovery points from the disk backup.</span></span> <span data-ttu-id="a694a-363">Dopo la generazione, il punto di recupero viene trasferito nell'insieme di credenziali di Servizi di ripristino di Azure.</span><span class="sxs-lookup"><span data-stu-id="a694a-363">After the recovery point is generated, it is transferred to the Recovery Services vault in Azure.</span></span> <span data-ttu-id="a694a-364">Quando si è soddisfatti della pianificazione del backup online, fare clic su **Avanti**.</span><span class="sxs-lookup"><span data-stu-id="a694a-364">When you are satisfied with the online backup schedule, click **Next**.</span></span>

    ![Specificare la pianificazione dei backup online](./media/backup-azure-backup-server-vmware/online-backup-schedule.png)

11. <span data-ttu-id="a694a-366">Nella pagina **Specificare i criteri di conservazione online** indicare per quanto tempo si vogliono mantenere i dati di backup in Azure.</span><span class="sxs-lookup"><span data-stu-id="a694a-366">On the **Specify Online Retention Policy** page, indicate how long you want to retain the backup data in Azure.</span></span> <span data-ttu-id="a694a-367">Dopo aver definito i criteri, fare clic su **Avanti**.</span><span class="sxs-lookup"><span data-stu-id="a694a-367">After the policy is defined, click **Next**.</span></span>

    ![Specificare i criteri di mantenimento online](./media/backup-azure-backup-server-vmware/retention-policy.png)

    <span data-ttu-id="a694a-369">Non esiste un limite di tempo per la conservazione dei dati in Azure.</span><span class="sxs-lookup"><span data-stu-id="a694a-369">There is no time limit for how long you can keep data in Azure.</span></span> <span data-ttu-id="a694a-370">Quando si archiviano dati di punti di recupero in Azure, l'unico limite è un massimo di 9999 punti di recupero per ogni istanza protetta.</span><span class="sxs-lookup"><span data-stu-id="a694a-370">When you store recovery point data in Azure, the only limit is that you cannot have more than 9999 recovery points per protected instance.</span></span> <span data-ttu-id="a694a-371">In questo esempio l'istanza protetta è il server VMware.</span><span class="sxs-lookup"><span data-stu-id="a694a-371">In this example, the protected instance is the VMware server.</span></span>

12. <span data-ttu-id="a694a-372">Nella pagina **Riepilogo** rivedere i dettagli relativi ai membri e alle impostazioni del gruppo protezione dati e quindi fare clic su **Crea gruppo**.</span><span class="sxs-lookup"><span data-stu-id="a694a-372">On the **Summary** page, review the details for your protection group members and settings, and then click **Create Group**.</span></span>

    ![Riepilogo delle impostazioni e dei membri del gruppo protezione dati](./media/backup-azure-backup-server-vmware/protection-group-summary.png)

## <a name="next-steps"></a><span data-ttu-id="a694a-374">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="a694a-374">Next steps</span></span>
<span data-ttu-id="a694a-375">Se si usa il server di Backup di Azure per proteggere i carichi di lavoro VMware, può essere utile usare il server di Backup di Azure per proteggere [server Microsoft Exchange](./backup-azure-exchange-mabs.md), [farm Microsoft SharePoint](./backup-azure-backup-sharepoint-mabs.md) o [database SQL Server](./backup-azure-sql-mabs.md).</span><span class="sxs-lookup"><span data-stu-id="a694a-375">If you use Azure Backup Server to protect VMware workloads, you may be interested in using Azure Backup Server to help protect a [Microsoft Exchange server](./backup-azure-exchange-mabs.md), a [Microsoft SharePoint farm](./backup-azure-backup-sharepoint-mabs.md), or a [SQL Server database](./backup-azure-sql-mabs.md).</span></span>

<span data-ttu-id="a694a-376">Per informazioni sui problemi relativi alla registrazione dell'agente, alla configurazione del gruppo protezione dati e al backup dei processi, vedere [Risolvere i problemi del server di Backup di Azure](./backup-azure-mabs-troubleshoot.md) .</span><span class="sxs-lookup"><span data-stu-id="a694a-376">For information on problems with registering the agent, configuring the protection group, or backing up jobs, see [Troubleshoot Azure Backup Server](./backup-azure-mabs-troubleshoot.md).</span></span>

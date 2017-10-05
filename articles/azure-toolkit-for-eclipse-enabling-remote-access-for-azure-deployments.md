---
title: Abilitare l'accesso remoto per le distribuzioni di Azure in Eclipse
description: "Informazioni su come abilitare l’accesso remoto per le distribuzioni Azure usando il Toolkit di Azure per Eclipse."
services: 
documentationcenter: java
author: rmcmurray
manager: erikre
editor: 
ms.assetid: b6150006-9a7f-4d83-be18-d35ec780c7c5
ms.service: multiple
ms.workload: na
ms.tgt_pltfrm: multiple
ms.devlang: Java
ms.topic: article
ms.date: 04/14/2017
ms.author: robmcm
ms.openlocfilehash: 654d511bd5a62341f87569317e97360c94a6f26c
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="enabling-remote-access-for-azure-deployments-in-eclipse"></a><span data-ttu-id="0d2fc-103">Abilitare l'accesso remoto per le distribuzioni di Azure in Eclipse</span><span class="sxs-lookup"><span data-stu-id="0d2fc-103">Enabling Remote Access for Azure Deployments in Eclipse</span></span>
<span data-ttu-id="0d2fc-104">Per risolvere i problemi relativi alle distribuzioni, è possibile abilitare e utilizzare l'accesso remoto per connettersi alla macchina virtuale che ospita la distribuzione.</span><span class="sxs-lookup"><span data-stu-id="0d2fc-104">To help troubleshoot your deployments, you may enable and use Remote Access to connect to the virtual machine hosting your deployment.</span></span> <span data-ttu-id="0d2fc-105">La funzionalità di accesso remoto si basa sul Remote Desktop Protocol (RDP).</span><span class="sxs-lookup"><span data-stu-id="0d2fc-105">The Remote Access functionality relies on the Remote Desktop Protocol (RDP).</span></span> <span data-ttu-id="0d2fc-106">È possibile configurare l’accesso remoto per la distribuzione dopo averlo pubblicato in Azure o se si utilizza Eclipse con un sistema operativo Windows, è possibile configurare l’accesso remoto prima di pubblicare in Azure.</span><span class="sxs-lookup"><span data-stu-id="0d2fc-106">You can configure Remote Access for your deployment after you have published it to Azure, or if you are using Eclipse with a Windows operating system, you can configure Remote Access before you publish to Azure.</span></span> <span data-ttu-id="0d2fc-107">Si noti che è necessario un client di desktop remoto compatibile con il sistema operativo per potersi connettere alla macchina virtuale della distribuzione in Azure.</span><span class="sxs-lookup"><span data-stu-id="0d2fc-107">Note that you will need a remote desktop client that is compatible with your operating system in order to connect to your deployment's virtual machine in Azure.</span></span>

## <a name="how-to-enable-remote-access-before-you-deploy-to-azure"></a><span data-ttu-id="0d2fc-108">Come abilitare l'accesso remoto prima della distribuire in Azure</span><span class="sxs-lookup"><span data-stu-id="0d2fc-108">How to enable Remote Access before you deploy to Azure</span></span>
> [!NOTE]
> <span data-ttu-id="0d2fc-109">Per abilitare l'accesso remoto prima di distribuire l'applicazione in Azure, è necessario eseguire Eclipse in Windows.</span><span class="sxs-lookup"><span data-stu-id="0d2fc-109">To enable Remote Access before you deploy your application to Azure, you need to be running Eclipse on Windows.</span></span>
> 
> 

<span data-ttu-id="0d2fc-110">La figura seguente mostra la finestra delle proprietà **Accesso remoto** utilizzate per abilitare l'accesso remoto.</span><span class="sxs-lookup"><span data-stu-id="0d2fc-110">The following image shows the **Remote Access** properties dialog used to enable remote access.</span></span>

![][ic719494]

<span data-ttu-id="0d2fc-111">Esistono due modi per visualizzare la finestra delle proprietà **Accesso remoto** :</span><span class="sxs-lookup"><span data-stu-id="0d2fc-111">There are two ways to display the **Remote Access** properties dialog:</span></span>

* <span data-ttu-id="0d2fc-112">Fare clic sul collegamento **Avanzate** nella sezione **Accesso remoto** della finestra di dialogo **Pubblica in Azure**.</span><span class="sxs-lookup"><span data-stu-id="0d2fc-112">Click the **Advanced** link in the **Remote Access** section of the **Publish to Azure** dialog.</span></span>

* <span data-ttu-id="0d2fc-113">Aprire la finestra di dialogo **Proprietà** del progetto di Azure.</span><span class="sxs-lookup"><span data-stu-id="0d2fc-113">Open the **Properties** dialog of your Azure project.</span></span>

<span data-ttu-id="0d2fc-114">Quando si crea un nuovo progetto di distribuzione di Azure, il progetto non disporrà dell’accesso remoto abilitato per impostazione predefinita.</span><span class="sxs-lookup"><span data-stu-id="0d2fc-114">When you create a new Azure deployment project, the project will not have Remote Access enabled by default.</span></span> <span data-ttu-id="0d2fc-115">Tuttavia, è possibile abilitare facilmente l'accesso remoto specificando il nome utente e la password nella finestra di dialogo **Pubblica in Azure** .</span><span class="sxs-lookup"><span data-stu-id="0d2fc-115">However, you can easily enable remote access by specifying the user name and password in the **Publish to Azure** dialog.</span></span> <span data-ttu-id="0d2fc-116">La password di accesso remoto viene crittografata mediante certificati X.509.</span><span class="sxs-lookup"><span data-stu-id="0d2fc-116">The Remote Access password is encrypted using X.509 certificates.</span></span> <span data-ttu-id="0d2fc-117">Se solitamente non si fornisce il proprio certificato, la crittografia si basa su un certificato autofirmato fornito con il plug-in di Azure per Eclipse.</span><span class="sxs-lookup"><span data-stu-id="0d2fc-117">If you do not use provide your own certificate, the encryption relies on a self-signed certificate shipped with the Azure Plugin for Eclipse.</span></span> <span data-ttu-id="0d2fc-118">Questo certificato autofirmato si trova nella cartella **cert** del progetto di Azure, archiviato sia come file di certificato pubblico (SampleRemoteAccessPublic) sia come un file di certificato Personal Information Exchange (PFX) (SampleRemoteAccessPrivate).</span><span class="sxs-lookup"><span data-stu-id="0d2fc-118">This self-signed certificate is in the **cert** folder of your Azure project, stored both as a public certificate file (SampleRemoteAccessPublic.cer) and as a Personal Information Exchange (PFX) certificate file (SampleRemoteAccessPrivate.pfx).</span></span> <span data-ttu-id="0d2fc-119">Il secondo contiene la chiave privata del certificato e ha una password predefinita, **Password1**.</span><span class="sxs-lookup"><span data-stu-id="0d2fc-119">The latter contains the private key for the certificate, and it has a default password, **Password1**.</span></span> <span data-ttu-id="0d2fc-120">Tuttavia, poiché questa password è pubblica, il certificato predefinito dovrebbe essere utilizzato solo a scopo illustrativo, non per una distribuzione di produzione.</span><span class="sxs-lookup"><span data-stu-id="0d2fc-120">However, since this password is public knowledge, the default certificate should be used only for learning purposes, not for a production deployment.</span></span> <span data-ttu-id="0d2fc-121">Quindi per fini diversi a quelli dell'apprendimento, quando si vuole abilitare le sessioni remote per le distribuzioni, è necessario fare clic sul collegamento **Avanzate** nella finestra di dialogo **Pubblica in Azure** per specificare il proprio certificato.</span><span class="sxs-lookup"><span data-stu-id="0d2fc-121">So other than for learning purposes, when you want to enabled remote sessions for your deployments, you should click the **Advanced** link in the **Publish to Azure** dialog to specify your own certificate.</span></span> <span data-ttu-id="0d2fc-122">Si noti che è necessario caricare la versione PFX del certificato nel servizio ospitato all'interno del portale di gestione di Azure, in modo che Azure possa decrittografare la password dell'utente.</span><span class="sxs-lookup"><span data-stu-id="0d2fc-122">Note that you'll need to upload the PFX version of the certificate to your hosted service within the Azure Management Portal, so that Azure can decrypt the user password.</span></span>

<span data-ttu-id="0d2fc-123">Nel resto dell'esercitazione viene illustrato come abilitare l'accesso remoto per un progetto di distribuzione di Azure creato inizialmente con l’accesso remoto disabilitato.</span><span class="sxs-lookup"><span data-stu-id="0d2fc-123">The remainder of the tutorial shows you how to enable remote access for an Azure deployment project that was initially created with remote access disabled.</span></span> <span data-ttu-id="0d2fc-124">Ai fini di questa esercitazione, verrà creato un nuovo certificato autofirmato e il relativo file con estensione pfx avrà una password di propria scelta.</span><span class="sxs-lookup"><span data-stu-id="0d2fc-124">For purposes of this tutorial, we'll create a new self-signed certificate, and its .pfx file will have a password of your choice.</span></span> <span data-ttu-id="0d2fc-125">È inoltre possibile utilizzare un certificato emesso da un'autorità di certificazione.</span><span class="sxs-lookup"><span data-stu-id="0d2fc-125">You also have the option of using a certificate issued by a certificate authority.</span></span>

## <a name="how-to-enable-remote-access-after-you-have-deployed-to-azure"></a><span data-ttu-id="0d2fc-126">Come abilitare l'accesso remoto dopo la distribuzione in Azure</span><span class="sxs-lookup"><span data-stu-id="0d2fc-126">How to enable Remote Access after you have deployed to Azure</span></span>
<span data-ttu-id="0d2fc-127">Per abilitare l'accesso remoto dopo aver distribuito in Azure, attenersi alla procedura seguente:</span><span class="sxs-lookup"><span data-stu-id="0d2fc-127">To enable remote access after you have deployed to Azure, use the following steps:</span></span>

1. <span data-ttu-id="0d2fc-128">Accedere al portale di gestione di Azure con il proprio account.</span><span class="sxs-lookup"><span data-stu-id="0d2fc-128">Log into the Azure management portal using your Azure account</span></span>

2. <span data-ttu-id="0d2fc-129">Nell'elenco di **servizi Cloud**, selezionare il servizio cloud distribuito</span><span class="sxs-lookup"><span data-stu-id="0d2fc-129">In your list of **Cloud Services**, select your deployed cloud service</span></span>

3. <span data-ttu-id="0d2fc-130">Nella pagina web del servizio cloud, fare clic sul collegamento **Configura**</span><span class="sxs-lookup"><span data-stu-id="0d2fc-130">In the cloud service web page, click the **Configure** link</span></span>

4. <span data-ttu-id="0d2fc-131">Nella parte inferiore della pagina di configurazione, fare clic sul collegamento **Remoto**</span><span class="sxs-lookup"><span data-stu-id="0d2fc-131">On the bottom of the configuration page, click the **Remote** link</span></span>

5. <span data-ttu-id="0d2fc-132">Quando viene visualizzata la finestra di dialogo popup:</span><span class="sxs-lookup"><span data-stu-id="0d2fc-132">When the pop-up dialog box appears:</span></span>
   
   * <span data-ttu-id="0d2fc-133">Specificare il Ruolo per cui si desidera abilitare l'accesso remoto</span><span class="sxs-lookup"><span data-stu-id="0d2fc-133">Specify the Role you for which you want to enable remote access</span></span>

   * <span data-ttu-id="0d2fc-134">Fare clic per selezionare la casella di controllo **Abilita Desktop remoto**</span><span class="sxs-lookup"><span data-stu-id="0d2fc-134">Click to select the **Enable Remote Desktop** checkbox</span></span>
   
   * <span data-ttu-id="0d2fc-135">Specificare un nome utente e una password da utilizzare per l'accesso remoto</span><span class="sxs-lookup"><span data-stu-id="0d2fc-135">Specify a user name and password you want to use for remote access</span></span>
   
   * <span data-ttu-id="0d2fc-136">Selezionare il certificato da utilizzare</span><span class="sxs-lookup"><span data-stu-id="0d2fc-136">Select the certificate to use</span></span>

6. <span data-ttu-id="0d2fc-137">Fare clic su **OK**</span><span class="sxs-lookup"><span data-stu-id="0d2fc-137">Click **OK**</span></span> 

<span data-ttu-id="0d2fc-138">Verrà visualizzato un messaggio che informa che la modifica della configurazione è in corso. La modifica potrebbe richiedere alcuni minuti.</span><span class="sxs-lookup"><span data-stu-id="0d2fc-138">You will see a message stating that your configuration change is in progress, which may take a few minutes to complete.</span></span> <span data-ttu-id="0d2fc-139">Una volta completata la modifica della configurazione, seguire i passaggi nella sezione **Per accedere in remoto** più avanti in questo articolo.</span><span class="sxs-lookup"><span data-stu-id="0d2fc-139">After the configuration change has completed, follow the steps in the **To log in remotely** section later in this article.</span></span>

## <a name="how-to-enable-remote-access-in-your-package"></a><span data-ttu-id="0d2fc-140">Come abilitare l'accesso remoto nel pacchetto</span><span class="sxs-lookup"><span data-stu-id="0d2fc-140">How to enable Remote Access in your package</span></span>
1. <span data-ttu-id="0d2fc-141">Nel riquadro Project Explorer di Eclipse fare clic con il pulsante destro del mouse sul progetto, quindi scegliere **Properties**.</span><span class="sxs-lookup"><span data-stu-id="0d2fc-141">Within Eclipse's Project Explorer pane, right-click your Azure project and click **Properties**.</span></span>

2. <span data-ttu-id="0d2fc-142">Nella finestra di dialogo **Properties** (Proprietà) espandere **Azure** nel riquadro a sinistra e fare clic su **Remote Access** (Accesso remoto).</span><span class="sxs-lookup"><span data-stu-id="0d2fc-142">In the **Properties** dialog, expand **Azure** in the left-hand pane and click **Remote Access**.</span></span>

3. <span data-ttu-id="0d2fc-143">Nella finestra di dialogo **Remote Access** (Accesso remoto), verificare che sia selezionato **Enable all roles to accept Remote Desktop Connections with these login credentials** (Consenti a tutti i ruoli di accettare connessioni Desktop remoto con queste credenziali di accesso).</span><span class="sxs-lookup"><span data-stu-id="0d2fc-143">In the **Remote Access** dialog, ensure **Enable all roles to accept Remote Desktop Connections with these login credentials** is checked.</span></span>

4. <span data-ttu-id="0d2fc-144">Specificare un nome utente per la connessione Desktop remoto.</span><span class="sxs-lookup"><span data-stu-id="0d2fc-144">Specify a user name for the Remote Desktop connection.</span></span>

5. <span data-ttu-id="0d2fc-145">Specificare e confermare la password per l'utente.</span><span class="sxs-lookup"><span data-stu-id="0d2fc-145">Specify and confirm the password for the user.</span></span> <span data-ttu-id="0d2fc-146">I valori nome e password utente impostati in questa finestra di dialogo verranno utilizzati quando si effettua una connessione Desktop remoto.</span><span class="sxs-lookup"><span data-stu-id="0d2fc-146">The user name and password values set in this dialog will be used when you make a Remote Desktop connection.</span></span> <span data-ttu-id="0d2fc-147">(Si tratta di una password diversa dalla password PFX).</span><span class="sxs-lookup"><span data-stu-id="0d2fc-147">(Note that this is a separate password from your PFX password.)</span></span>

6. <span data-ttu-id="0d2fc-148">Specificare la data di scadenza per l'account utente.</span><span class="sxs-lookup"><span data-stu-id="0d2fc-148">Specify the expiration date for the user account.</span></span>

7. <span data-ttu-id="0d2fc-149">Fare clic su **New** per creare un nuovo certificato autofirmato.</span><span class="sxs-lookup"><span data-stu-id="0d2fc-149">Click **New** to create a new self-signed certificate.</span></span> <span data-ttu-id="0d2fc-150">In alternativa, è possibile selezionare un certificato dall'area di lavoro o nel file system tramite i pulsanti **Workspace** (Area di lavoro) o **FileSystem** (File system), rispettivamente, ma per questa esercitazione si creerà un nuovo certificato.</span><span class="sxs-lookup"><span data-stu-id="0d2fc-150">(Alternatively, you could select a certificate from your workspace or file system through the **Workspace** or **FileSystem** buttons, respectively, but for purposes of this tutorial we'll create a new certificate.)</span></span>

   * <span data-ttu-id="0d2fc-151">Nella finestra di dialogo **New Certificate** , specificare e confermare la password da utilizzare per il file PFX.</span><span class="sxs-lookup"><span data-stu-id="0d2fc-151">In the **New Certificate** dialog, specify and confirm the password you'll use for your PFX file.</span></span>

   * <span data-ttu-id="0d2fc-152">Accettare il valore fornito per **Name (CN)**, oppure utilizzare un nome personalizzato.</span><span class="sxs-lookup"><span data-stu-id="0d2fc-152">Accept the value provided for **Name (CN)**, or use a custom name.</span></span>

   * <span data-ttu-id="0d2fc-153">Specificare il percorso e il nome del file con cui il nuovo certificato verrà salvato, nel formato con estensione cer.</span><span class="sxs-lookup"><span data-stu-id="0d2fc-153">Specify the path and file name where the new certificate, in .cer form, will be saved.</span></span> <span data-ttu-id="0d2fc-154">Per questo passaggio e il passaggio successivo, è possibile utilizzare la cartella **cert** del progetto di Azure, ma si può scegliere un altro percorso.</span><span class="sxs-lookup"><span data-stu-id="0d2fc-154">For this step and the next step, you could use the **cert** folder of your Azure project, but you're free to choose another location.</span></span> <span data-ttu-id="0d2fc-155">Ai fini di questa esercitazione, si userà **c:\mycert\mycert.cer**.</span><span class="sxs-lookup"><span data-stu-id="0d2fc-155">For purposes of this tutorial, we'll use **c:\mycert\mycert.cer**.</span></span> <span data-ttu-id="0d2fc-156">Creare la cartella **c:\mycert** prima di continuare o, se si vuole, usare una cartella esistente.</span><span class="sxs-lookup"><span data-stu-id="0d2fc-156">(Create the **c:\mycert** folder prior to proceeding, or use an existing folder if desired.)</span></span>

   * <span data-ttu-id="0d2fc-157">Specificare il percorso e il nome del file con cui il nuovo certificato e la sua chiave privata verranno salvati, nel formato con estensione pfx.</span><span class="sxs-lookup"><span data-stu-id="0d2fc-157">Specify the path and file name where the new certificate and its private key, in .pfx form, will be saved.</span></span> <span data-ttu-id="0d2fc-158">Ai fini di questa esercitazione, si userà **c:\mycert\mycert.pfx**.</span><span class="sxs-lookup"><span data-stu-id="0d2fc-158">For purposes of this tutorial, we'll use **c:\mycert\mycert.pfx**.</span></span> <span data-ttu-id="0d2fc-159">La finestra di dialogo **New Certificate** (Nuovo certificato) dovrebbe essere simile a quanto segue. Aggiornare i percorsi della cartella se non si usa **c:\mycert**:</span><span class="sxs-lookup"><span data-stu-id="0d2fc-159">Your **New Certificate** dialog should look similar to the following (update the folder paths if you did not use **c:\mycert**):</span></span>
     
      ![][ic712275]

   * <span data-ttu-id="0d2fc-160">Fare clic su **OK** per chiudere la finestra di dialogo **New Certificate** (Nuovo certificato).</span><span class="sxs-lookup"><span data-stu-id="0d2fc-160">Click **OK** to close the **New Certificate** dialog.</span></span>

8. <span data-ttu-id="0d2fc-161">La finestra di dialogo **Remote Access** (Accesso remoto) avrà un aspetto analogo al seguente:</span><span class="sxs-lookup"><span data-stu-id="0d2fc-161">Your **Remote Access** dialog should look similar to the following:</span></span></p>
   
   ![][ic719495]

9. <span data-ttu-id="0d2fc-162">Fare clic su **OK** per chiudere la finestra di dialogo **Remote Access** (Accesso remoto).</span><span class="sxs-lookup"><span data-stu-id="0d2fc-162">Click **OK** to close the **Remote Access** dialog.</span></span>

<span data-ttu-id="0d2fc-163">Ricompilare l'applicazione, con la compilazione impostata per la distribuzione nel cloud.</span><span class="sxs-lookup"><span data-stu-id="0d2fc-163">Rebuild your application, with the build set for deployment to cloud.</span></span>

## <a name="to-log-in-remotely"></a><span data-ttu-id="0d2fc-164">Per accedere in modalità remota</span><span class="sxs-lookup"><span data-stu-id="0d2fc-164">To log in remotely</span></span>
<span data-ttu-id="0d2fc-165">Quando l'istanza del ruolo è pronta, è possibile accedere in remoto alla macchina virtuale che ospita l'applicazione.</span><span class="sxs-lookup"><span data-stu-id="0d2fc-165">Once your role instance is ready, you can remotely log in to the virtual machine that is hosting your application.</span></span>

* <span data-ttu-id="0d2fc-166">Se si usa Eclipse in Windows e si seleziona l’opzione **Start remote desktop on deploy** durante la distribuzione in Azure, si visualizzerà una schermata di accesso di connessione Desktop remoto all'avvio della distribuzione.</span><span class="sxs-lookup"><span data-stu-id="0d2fc-166">If are using Eclipse on Windows and you selected the **Start remote desktop on deploy** option during your deployment to Azure, you will be presented with a Remote Desktop Connection logon screen when your deployment starts.</span></span> <span data-ttu-id="0d2fc-167">Quando viene chiesto di immettere il nome utente e la password, immettere i valori specificati per l'utente remoto per effettuare l’accesso.</span><span class="sxs-lookup"><span data-stu-id="0d2fc-167">When you are prompted for the user name and password, enter the values that you specified for the remote user and will be able to log in.</span></span>

* <span data-ttu-id="0d2fc-168">È possibile accedere in remoto tramite il <a href="http://go.microsoft.com/fwlink/?LinkID=512959">portale di gestione di Azure</a>:</span><span class="sxs-lookup"><span data-stu-id="0d2fc-168">Another way to log in remotely is through the <a href="http://go.microsoft.com/fwlink/?LinkID=512959">Azure Management Portal</a>:</span></span>
  
  * <span data-ttu-id="0d2fc-169">Nella visualizzazione **Servizi cloud** del portale di gestione di Azure fare clic sul servizio cloud, fare clic su **Istanze**, fare clic su un'istanza specifica e quindi fare clic sul pulsante **Connetti**.</span><span class="sxs-lookup"><span data-stu-id="0d2fc-169">Within the **Cloud Services** view of the Azure Management portal, click your cloud service, click **Instances**, click a specific instance, and then click the **Connect** button.</span></span> <span data-ttu-id="0d2fc-170">Il pulsante **Connetti** viene visualizzato come mostrato di seguito sulla barra dei comandi:</span><span class="sxs-lookup"><span data-stu-id="0d2fc-170">The **Connect** button appears as the following in the command bar:</span></span>
    
      ![][ic659273]

  * <span data-ttu-id="0d2fc-171">Dopo aver fatto clic sul pulsante **Connetti** , verrà richiesto di aprire un file RDP.</span><span class="sxs-lookup"><span data-stu-id="0d2fc-171">After clicking the **Connect** button, you will be prompted to open an RDP file.</span></span> <span data-ttu-id="0d2fc-172">Aprire il file e seguire le istruzioni.</span><span class="sxs-lookup"><span data-stu-id="0d2fc-172">Open the file and follow the prompts.</span></span> <span data-ttu-id="0d2fc-173">(È possibile inoltre salvare questo file nel computer locale e quindi eseguire il file facendovi doppio clic per accedere in modalità remota alla macchina virtuale senza la necessità di aprire prima il portale di gestione.)</span><span class="sxs-lookup"><span data-stu-id="0d2fc-173">(You could also save this file to your local computer, and then run the file by double-clicking it to remote log in to your virtual machine without needing to first go the management portal.)</span></span>

  * <span data-ttu-id="0d2fc-174">Quando viene chiesto di immettere il nome utente e la password, immettere i valori specificati per l'utente remoto per effettuare l’accesso.</span><span class="sxs-lookup"><span data-stu-id="0d2fc-174">When you are prompted for the user name and password, enter the values that you specified for the remote user and will be able to log in.</span></span>

> [!NOTE]
> <span data-ttu-id="0d2fc-175">Se si utilizza un sistema operativo non Windows, è necessario utilizzare un client di Desktop remoto compatibile con il sistema operativo e seguire la procedura per configurare il client con le impostazioni nel file RDP scaricato.</span><span class="sxs-lookup"><span data-stu-id="0d2fc-175">If you are on a non-Windows operating system, you need to use a Remote Desktop client that is compatible with your operating system and follow the steps to configure that client with the settings in the RDP file that you downloaded.</span></span>
> 
> 

## <a name="see-also"></a><span data-ttu-id="0d2fc-176">Vedere anche</span><span class="sxs-lookup"><span data-stu-id="0d2fc-176">See Also</span></span>
<span data-ttu-id="0d2fc-177">[Azure Toolkit for Eclipse][Azure Toolkit for Eclipse]</span><span class="sxs-lookup"><span data-stu-id="0d2fc-177">[Azure Toolkit for Eclipse][Azure Toolkit for Eclipse]</span></span>

<span data-ttu-id="0d2fc-178">[Creare un'applicazione Hello World per Azure in Eclipse][Creating a Hello World Application for Azure in Eclipse]</span><span class="sxs-lookup"><span data-stu-id="0d2fc-178">[Creating a Hello World Application for Azure in Eclipse][Creating a Hello World Application for Azure in Eclipse]</span></span>

<span data-ttu-id="0d2fc-179">[Installazione di Azure Toolkit for Eclipse][Installing the Azure Toolkit for Eclipse]</span><span class="sxs-lookup"><span data-stu-id="0d2fc-179">[Installing the Azure Toolkit for Eclipse][Installing the Azure Toolkit for Eclipse]</span></span> 

<span data-ttu-id="0d2fc-180">Per altre informazioni su come usare Azure con Java, vedere il [Centro per sviluppatori Java di Azure][Azure Java Developer Center].</span><span class="sxs-lookup"><span data-stu-id="0d2fc-180">For more information about using Azure with Java, see the [Azure Java Developer Center][Azure Java Developer Center].</span></span>

<!-- URL List -->

[Azure Java Developer Center]: http://go.microsoft.com/fwlink/?LinkID=699547
[Azure Management Portal]: http://go.microsoft.com/fwlink/?LinkID=512959
[Azure Toolkit for Eclipse]: http://go.microsoft.com/fwlink/?LinkID=699529
[Creating a Hello World Application for Azure in Eclipse]: http://go.microsoft.com/fwlink/?LinkID=699533
[Installing the Azure Toolkit for Eclipse]: http://go.microsoft.com/fwlink/?LinkId=699546

<!-- IMG List -->

[ic712275]: ./media/azure-toolkit-for-eclipse-enabling-remote-access-for-azure-deployments/ic712275.png
[ic719495]: ./media/azure-toolkit-for-eclipse-enabling-remote-access-for-azure-deployments/ic719495.png
[ic719494]: ./media/azure-toolkit-for-eclipse-enabling-remote-access-for-azure-deployments/ic719494.png
[ic659273]: ./media/azure-toolkit-for-eclipse-enabling-remote-access-for-azure-deployments/ic659273.png

<!-- Legacy MSDN URL = https://msdn.microsoft.com/library/azure/hh690951.aspx -->

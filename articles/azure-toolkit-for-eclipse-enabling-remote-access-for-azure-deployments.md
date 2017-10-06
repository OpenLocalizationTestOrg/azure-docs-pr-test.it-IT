---
title: aaaEnabling accesso remoto per le distribuzioni di Azure in Eclipse
description: "Informazioni su modalità di accesso remoto tooenable per distribuzioni di Azure utilizzando hello Azure Toolkit per Eclipse."
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
ms.openlocfilehash: 00c2bf22c1f3ec792098f154f771c87506e87881
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="enabling-remote-access-for-azure-deployments-in-eclipse"></a><span data-ttu-id="8d46c-103">Abilitare l'accesso remoto per le distribuzioni di Azure in Eclipse</span><span class="sxs-lookup"><span data-stu-id="8d46c-103">Enabling Remote Access for Azure Deployments in Eclipse</span></span>
<span data-ttu-id="8d46c-104">toohelp di risolvere i problemi delle distribuzioni, è possibile abilitare e usare accesso remoto tooconnect toohello macchina virtuale che ospita la distribuzione.</span><span class="sxs-lookup"><span data-stu-id="8d46c-104">toohelp troubleshoot your deployments, you may enable and use Remote Access tooconnect toohello virtual machine hosting your deployment.</span></span> <span data-ttu-id="8d46c-105">Hello funzionalità di accesso remoto si basa su hello Remote Desktop Protocol (RDP).</span><span class="sxs-lookup"><span data-stu-id="8d46c-105">hello Remote Access functionality relies on hello Remote Desktop Protocol (RDP).</span></span> <span data-ttu-id="8d46c-106">È possibile configurare accesso remoto per la distribuzione dopo averlo pubblicato tooAzure o se si usa Eclipse con un sistema operativo Windows, è possibile configurare accesso remoto prima di pubblicare tooAzure.</span><span class="sxs-lookup"><span data-stu-id="8d46c-106">You can configure Remote Access for your deployment after you have published it tooAzure, or if you are using Eclipse with a Windows operating system, you can configure Remote Access before you publish tooAzure.</span></span> <span data-ttu-id="8d46c-107">Si noti che è necessario un client desktop remoto compatibile con il sistema operativo nella macchina virtuale della distribuzione di ordine tooconnect tooyour in Azure.</span><span class="sxs-lookup"><span data-stu-id="8d46c-107">Note that you will need a remote desktop client that is compatible with your operating system in order tooconnect tooyour deployment's virtual machine in Azure.</span></span>

## <a name="how-tooenable-remote-access-before-you-deploy-tooazure"></a><span data-ttu-id="8d46c-108">Come tooenable accesso remoto prima di distribuire tooAzure</span><span class="sxs-lookup"><span data-stu-id="8d46c-108">How tooenable Remote Access before you deploy tooAzure</span></span>
> [!NOTE]
> <span data-ttu-id="8d46c-109">Accesso remoto prima di distribuire l'applicazione tooAzure tooenable, è necessario eseguire Eclipse in Windows toobe.</span><span class="sxs-lookup"><span data-stu-id="8d46c-109">tooenable Remote Access before you deploy your application tooAzure, you need toobe running Eclipse on Windows.</span></span>
> 
> 

<span data-ttu-id="8d46c-110">Hello immagine seguente viene illustrato hello **accesso remoto** finestra di dialogo proprietà utilizzato tooenable di accesso remoto.</span><span class="sxs-lookup"><span data-stu-id="8d46c-110">hello following image shows hello **Remote Access** properties dialog used tooenable remote access.</span></span>

![][ic719494]

<span data-ttu-id="8d46c-111">Esistono due hello toodisplay di modi **accesso remoto** finestra di dialogo proprietà:</span><span class="sxs-lookup"><span data-stu-id="8d46c-111">There are two ways toodisplay hello **Remote Access** properties dialog:</span></span>

* <span data-ttu-id="8d46c-112">Fare clic su hello **avanzate** collegamento hello **accesso remoto** sezione di hello **pubblicare tooAzure** finestra di dialogo.</span><span class="sxs-lookup"><span data-stu-id="8d46c-112">Click hello **Advanced** link in hello **Remote Access** section of hello **Publish tooAzure** dialog.</span></span>

* <span data-ttu-id="8d46c-113">Aprire hello **proprietà** finestra di dialogo del progetto Azure.</span><span class="sxs-lookup"><span data-stu-id="8d46c-113">Open hello **Properties** dialog of your Azure project.</span></span>

<span data-ttu-id="8d46c-114">Quando si crea un nuovo progetto di distribuzione di Azure, progetto hello non è abilitato per impostazione predefinita l'accesso remoto.</span><span class="sxs-lookup"><span data-stu-id="8d46c-114">When you create a new Azure deployment project, hello project will not have Remote Access enabled by default.</span></span> <span data-ttu-id="8d46c-115">Tuttavia, è possibile abilitare facilmente l'accesso remoto specificando nome utente hello e una password in hello **pubblicare tooAzure** finestra di dialogo.</span><span class="sxs-lookup"><span data-stu-id="8d46c-115">However, you can easily enable remote access by specifying hello user name and password in hello **Publish tooAzure** dialog.</span></span> <span data-ttu-id="8d46c-116">password di accesso remoto Hello viene crittografata mediante certificati x. 509.</span><span class="sxs-lookup"><span data-stu-id="8d46c-116">hello Remote Access password is encrypted using X.509 certificates.</span></span> <span data-ttu-id="8d46c-117">Se non si utilizza, fornire il proprio certificato, la crittografia hello si basa su un certificato autofirmato fornito con hello Azure Plugin for Eclipse.</span><span class="sxs-lookup"><span data-stu-id="8d46c-117">If you do not use provide your own certificate, hello encryption relies on a self-signed certificate shipped with hello Azure Plugin for Eclipse.</span></span> <span data-ttu-id="8d46c-118">Questo certificato autofirmato è hello **cert** cartella del progetto Azure, archiviato sia come un file di certificato pubblico (SampleRemoteAccessPublic.cer) e come un scambio di informazioni personali (PFX) (file di certificato SampleRemoteAccessPrivate.pfx).</span><span class="sxs-lookup"><span data-stu-id="8d46c-118">This self-signed certificate is in hello **cert** folder of your Azure project, stored both as a public certificate file (SampleRemoteAccessPublic.cer) and as a Personal Information Exchange (PFX) certificate file (SampleRemoteAccessPrivate.pfx).</span></span> <span data-ttu-id="8d46c-119">Hello quest'ultimo contiene la chiave privata per il certificato di hello hello e una password predefinita, ha **Password1**.</span><span class="sxs-lookup"><span data-stu-id="8d46c-119">hello latter contains hello private key for hello certificate, and it has a default password, **Password1**.</span></span> <span data-ttu-id="8d46c-120">Tuttavia, poiché questa password è pubblico, il certificato di predefinito hello deve essere usato solo per finalità di apprendimento, non per una distribuzione di produzione.</span><span class="sxs-lookup"><span data-stu-id="8d46c-120">However, since this password is public knowledge, hello default certificate should be used only for learning purposes, not for a production deployment.</span></span> <span data-ttu-id="8d46c-121">In modo diverso ai fini dell'apprendimento, quando si desidera che le sessioni remote tooenabled per le distribuzioni, è necessario fare clic hello **avanzate** collegamento hello **pubblicare tooAzure** toospecify finestra di dialogo personalizzate certificato.</span><span class="sxs-lookup"><span data-stu-id="8d46c-121">So other than for learning purposes, when you want tooenabled remote sessions for your deployments, you should click hello **Advanced** link in hello **Publish tooAzure** dialog toospecify your own certificate.</span></span> <span data-ttu-id="8d46c-122">Si noti che è necessario tooupload hello PFX versione servizio di hello certificati tooyour ospitato all'interno di hello portale di gestione di Azure, in modo che Azure possa decrittografare la password utente hello.</span><span class="sxs-lookup"><span data-stu-id="8d46c-122">Note that you'll need tooupload hello PFX version of hello certificate tooyour hosted service within hello Azure Management Portal, so that Azure can decrypt hello user password.</span></span>

<span data-ttu-id="8d46c-123">resto Hello di esercitazione hello viene illustrata la modalità di accesso remoto di tooenable per un progetto di distribuzione di Azure che è stato inizialmente creato con l'accesso remoto disabilitato.</span><span class="sxs-lookup"><span data-stu-id="8d46c-123">hello remainder of hello tutorial shows you how tooenable remote access for an Azure deployment project that was initially created with remote access disabled.</span></span> <span data-ttu-id="8d46c-124">Ai fini di questa esercitazione, verrà creato un nuovo certificato autofirmato e il relativo file con estensione pfx avrà una password di propria scelta.</span><span class="sxs-lookup"><span data-stu-id="8d46c-124">For purposes of this tutorial, we'll create a new self-signed certificate, and its .pfx file will have a password of your choice.</span></span> <span data-ttu-id="8d46c-125">È anche possibile hello utilizzando un certificato emesso da un'autorità di certificazione.</span><span class="sxs-lookup"><span data-stu-id="8d46c-125">You also have hello option of using a certificate issued by a certificate authority.</span></span>

## <a name="how-tooenable-remote-access-after-you-have-deployed-tooazure"></a><span data-ttu-id="8d46c-126">Come tooenable accesso remoto dopo avere distribuito tooAzure</span><span class="sxs-lookup"><span data-stu-id="8d46c-126">How tooenable Remote Access after you have deployed tooAzure</span></span>
<span data-ttu-id="8d46c-127">accesso remoto tooenable dopo aver distribuito tooAzure, utilizzare hello alla procedura seguente:</span><span class="sxs-lookup"><span data-stu-id="8d46c-127">tooenable remote access after you have deployed tooAzure, use hello following steps:</span></span>

1. <span data-ttu-id="8d46c-128">Accedere al portale di gestione di Azure di hello utilizzando l'account di Azure</span><span class="sxs-lookup"><span data-stu-id="8d46c-128">Log into hello Azure management portal using your Azure account</span></span>

2. <span data-ttu-id="8d46c-129">Nell'elenco di **servizi Cloud**, selezionare il servizio cloud distribuito</span><span class="sxs-lookup"><span data-stu-id="8d46c-129">In your list of **Cloud Services**, select your deployed cloud service</span></span>

3. <span data-ttu-id="8d46c-130">Nella pagina web del servizio cloud hello, fare clic su hello **configura** collegamento</span><span class="sxs-lookup"><span data-stu-id="8d46c-130">In hello cloud service web page, click hello **Configure** link</span></span>

4. <span data-ttu-id="8d46c-131">Nella parte inferiore di hello hello della pagina di configurazione, fare clic su hello **remoto** collegamento</span><span class="sxs-lookup"><span data-stu-id="8d46c-131">On hello bottom of hello configuration page, click hello **Remote** link</span></span>

5. <span data-ttu-id="8d46c-132">Quando viene visualizzata finestra di dialogo popup hello:</span><span class="sxs-lookup"><span data-stu-id="8d46c-132">When hello pop-up dialog box appears:</span></span>
   
   * <span data-ttu-id="8d46c-133">Specificare hello ruolo è per il quale si desidera l'accesso remoto tooenable</span><span class="sxs-lookup"><span data-stu-id="8d46c-133">Specify hello Role you for which you want tooenable remote access</span></span>

   * <span data-ttu-id="8d46c-134">Fare clic su hello tooselect **Abilita Desktop remoto** casella di controllo</span><span class="sxs-lookup"><span data-stu-id="8d46c-134">Click tooselect hello **Enable Remote Desktop** checkbox</span></span>
   
   * <span data-ttu-id="8d46c-135">Specificare un nome utente e password per l'accesso remoto da toouse</span><span class="sxs-lookup"><span data-stu-id="8d46c-135">Specify a user name and password you want toouse for remote access</span></span>
   
   * <span data-ttu-id="8d46c-136">Selezionare hello certificato toouse</span><span class="sxs-lookup"><span data-stu-id="8d46c-136">Select hello certificate toouse</span></span>

6. <span data-ttu-id="8d46c-137">Fare clic su **OK**</span><span class="sxs-lookup"><span data-stu-id="8d46c-137">Click **OK**</span></span> 

<span data-ttu-id="8d46c-138">Si verrà visualizzato un messaggio che informa che la modifica della configurazione è in corso, che potrebbe richiedere alcuni minuti toocomplete.</span><span class="sxs-lookup"><span data-stu-id="8d46c-138">You will see a message stating that your configuration change is in progress, which may take a few minutes toocomplete.</span></span> <span data-ttu-id="8d46c-139">Al termine della modifica della configurazione hello, seguire i passaggi hello hello **toolog in modalità remota** sezione più avanti in questo articolo.</span><span class="sxs-lookup"><span data-stu-id="8d46c-139">After hello configuration change has completed, follow hello steps in hello **toolog in remotely** section later in this article.</span></span>

## <a name="how-tooenable-remote-access-in-your-package"></a><span data-ttu-id="8d46c-140">La modalità di accesso remoto tooenable nel pacchetto</span><span class="sxs-lookup"><span data-stu-id="8d46c-140">How tooenable Remote Access in your package</span></span>
1. <span data-ttu-id="8d46c-141">Nel riquadro Project Explorer di Eclipse fare clic con il pulsante destro del mouse sul progetto, quindi scegliere **Properties**.</span><span class="sxs-lookup"><span data-stu-id="8d46c-141">Within Eclipse's Project Explorer pane, right-click your Azure project and click **Properties**.</span></span>

2. <span data-ttu-id="8d46c-142">In hello **proprietà** finestra di dialogo espandere **Azure** nel riquadro sinistro di hello e fare clic su **accesso remoto**.</span><span class="sxs-lookup"><span data-stu-id="8d46c-142">In hello **Properties** dialog, expand **Azure** in hello left-hand pane and click **Remote Access**.</span></span>

3. <span data-ttu-id="8d46c-143">In hello **accesso remoto** finestra di dialogo, verificare **abilitare tutti i ruoli tooaccept connessioni Desktop remoto con le credenziali di account di accesso** è selezionata.</span><span class="sxs-lookup"><span data-stu-id="8d46c-143">In hello **Remote Access** dialog, ensure **Enable all roles tooaccept Remote Desktop Connections with these login credentials** is checked.</span></span>

4. <span data-ttu-id="8d46c-144">Specificare un nome utente per hello connessione Desktop remoto.</span><span class="sxs-lookup"><span data-stu-id="8d46c-144">Specify a user name for hello Remote Desktop connection.</span></span>

5. <span data-ttu-id="8d46c-145">Specificare e confermare una password hello hello utente.</span><span class="sxs-lookup"><span data-stu-id="8d46c-145">Specify and confirm hello password for hello user.</span></span> <span data-ttu-id="8d46c-146">Hello valori nome utente e password impostati in questa finestra di dialogo verranno utilizzati quando si effettua una connessione Desktop remoto.</span><span class="sxs-lookup"><span data-stu-id="8d46c-146">hello user name and password values set in this dialog will be used when you make a Remote Desktop connection.</span></span> <span data-ttu-id="8d46c-147">(Si tratta di una password diversa dalla password PFX).</span><span class="sxs-lookup"><span data-stu-id="8d46c-147">(Note that this is a separate password from your PFX password.)</span></span>

6. <span data-ttu-id="8d46c-148">Specificare la data di scadenza hello per account utente di hello.</span><span class="sxs-lookup"><span data-stu-id="8d46c-148">Specify hello expiration date for hello user account.</span></span>

7. <span data-ttu-id="8d46c-149">Fare clic su **New** toocreate un nuovo certificato autofirmato.</span><span class="sxs-lookup"><span data-stu-id="8d46c-149">Click **New** toocreate a new self-signed certificate.</span></span> <span data-ttu-id="8d46c-150">(In alternativa, è possibile selezionare un certificato dal sistema dell'area di lavoro o un file tramite hello **dell'area di lavoro** o **FileSystem** pulsanti, rispettivamente, ma ai fini di questa esercitazione si creerà un nuovo certificato).</span><span class="sxs-lookup"><span data-stu-id="8d46c-150">(Alternatively, you could select a certificate from your workspace or file system through hello **Workspace** or **FileSystem** buttons, respectively, but for purposes of this tutorial we'll create a new certificate.)</span></span>

   * <span data-ttu-id="8d46c-151">In hello **nuovo certificato** finestra di dialogo, specificare e confermare una password hello da utilizzare per il file PFX.</span><span class="sxs-lookup"><span data-stu-id="8d46c-151">In hello **New Certificate** dialog, specify and confirm hello password you'll use for your PFX file.</span></span>

   * <span data-ttu-id="8d46c-152">Accettare il valore specificato per hello **nome (CN)**, oppure utilizzare un nome personalizzato.</span><span class="sxs-lookup"><span data-stu-id="8d46c-152">Accept hello value provided for **Name (CN)**, or use a custom name.</span></span>

   * <span data-ttu-id="8d46c-153">Specificare hello percorso e nome file in cui verrà salvato hello nuovo certificato, in formato con estensione cer.</span><span class="sxs-lookup"><span data-stu-id="8d46c-153">Specify hello path and file name where hello new certificate, in .cer form, will be saved.</span></span> <span data-ttu-id="8d46c-154">Per questo passaggio e hello successivo, è possibile utilizzare hello **cert** cartella del progetto Azure, ma si toochoose disponibile un'altra posizione.</span><span class="sxs-lookup"><span data-stu-id="8d46c-154">For this step and hello next step, you could use hello **cert** folder of your Azure project, but you're free toochoose another location.</span></span> <span data-ttu-id="8d46c-155">Ai fini di questa esercitazione, si userà **c:\mycert\mycert.cer**.</span><span class="sxs-lookup"><span data-stu-id="8d46c-155">For purposes of this tutorial, we'll use **c:\mycert\mycert.cer**.</span></span> <span data-ttu-id="8d46c-156">(Creare hello **c:\mycert** tooproceeding precedente cartella o una cartella esistente, se lo si desidera utilizzare.)</span><span class="sxs-lookup"><span data-stu-id="8d46c-156">(Create hello **c:\mycert** folder prior tooproceeding, or use an existing folder if desired.)</span></span>

   * <span data-ttu-id="8d46c-157">Specificare hello percorso e nome file in cui verrà salvati hello nuovo certificato e relativa chiave privata, in formato pfx.</span><span class="sxs-lookup"><span data-stu-id="8d46c-157">Specify hello path and file name where hello new certificate and its private key, in .pfx form, will be saved.</span></span> <span data-ttu-id="8d46c-158">Ai fini di questa esercitazione, si userà **c:\mycert\mycert.pfx**.</span><span class="sxs-lookup"><span data-stu-id="8d46c-158">For purposes of this tutorial, we'll use **c:\mycert\mycert.pfx**.</span></span> <span data-ttu-id="8d46c-159">Il **nuovo certificato** finestra di dialogo dovrebbe essere simile toohello seguente (aggiornare i percorsi delle cartelle hello se non si utilizza **c:\mycert**):</span><span class="sxs-lookup"><span data-stu-id="8d46c-159">Your **New Certificate** dialog should look similar toohello following (update hello folder paths if you did not use **c:\mycert**):</span></span>
     
      ![][ic712275]

   * <span data-ttu-id="8d46c-160">Fare clic su **OK** tooclose hello **nuovo certificato** finestra di dialogo.</span><span class="sxs-lookup"><span data-stu-id="8d46c-160">Click **OK** tooclose hello **New Certificate** dialog.</span></span>

8. <span data-ttu-id="8d46c-161">Il **accesso remoto** finestra di dialogo dovrebbe essere simile toohello seguenti:</span><span class="sxs-lookup"><span data-stu-id="8d46c-161">Your **Remote Access** dialog should look similar toohello following:</span></span></p>
   
   ![][ic719495]

9. <span data-ttu-id="8d46c-162">Fare clic su **OK** tooclose hello **accesso remoto** finestra di dialogo.</span><span class="sxs-lookup"><span data-stu-id="8d46c-162">Click **OK** tooclose hello **Remote Access** dialog.</span></span>

<span data-ttu-id="8d46c-163">Ricompilare l'applicazione, con hello set per la distribuzione toocloud di compilazione.</span><span class="sxs-lookup"><span data-stu-id="8d46c-163">Rebuild your application, with hello build set for deployment toocloud.</span></span>

## <a name="toolog-in-remotely"></a><span data-ttu-id="8d46c-164">toolog in modalità remota</span><span class="sxs-lookup"><span data-stu-id="8d46c-164">toolog in remotely</span></span>
<span data-ttu-id="8d46c-165">Quando l'istanza del ruolo è pronta, è possibile accedere in remoto nella macchina virtuale toohello che ospita l'applicazione.</span><span class="sxs-lookup"><span data-stu-id="8d46c-165">Once your role instance is ready, you can remotely log in toohello virtual machine that is hosting your application.</span></span>

* <span data-ttu-id="8d46c-166">Se Usa Eclipse in Windows e hello selezionato **inizio desktop remoto in distribuire** opzione durante la distribuzione tooAzure, verrà visualizzata una schermata di accesso della connessione Desktop remoto all'avvio della distribuzione.</span><span class="sxs-lookup"><span data-stu-id="8d46c-166">If are using Eclipse on Windows and you selected hello **Start remote desktop on deploy** option during your deployment tooAzure, you will be presented with a Remote Desktop Connection logon screen when your deployment starts.</span></span> <span data-ttu-id="8d46c-167">Quando viene chiesto di immettere nome utente hello e una password, immettere i valori hello specificato per l'utente remoto hello e sarà in grado di toolog in.</span><span class="sxs-lookup"><span data-stu-id="8d46c-167">When you are prompted for hello user name and password, enter hello values that you specified for hello remote user and will be able toolog in.</span></span>

* <span data-ttu-id="8d46c-168">Un altro modo toolog in è in modalità remota tramite hello <a href="http://go.microsoft.com/fwlink/?LinkID=512959">il portale di gestione di Azure</a>:</span><span class="sxs-lookup"><span data-stu-id="8d46c-168">Another way toolog in remotely is through hello <a href="http://go.microsoft.com/fwlink/?LinkID=512959">Azure Management Portal</a>:</span></span>
  
  * <span data-ttu-id="8d46c-169">All'interno di hello **servizi Cloud** visualizzazione di hello portale di gestione di Azure, il servizio cloud fare clic su **istanze**, fare clic su un'istanza specifica e quindi fare clic su hello **Connetti**pulsante.</span><span class="sxs-lookup"><span data-stu-id="8d46c-169">Within hello **Cloud Services** view of hello Azure Management portal, click your cloud service, click **Instances**, click a specific instance, and then click hello **Connect** button.</span></span> <span data-ttu-id="8d46c-170">Hello **Connetti** pulsante viene visualizzato come riportato di seguito hello nella barra dei comandi di hello:</span><span class="sxs-lookup"><span data-stu-id="8d46c-170">hello **Connect** button appears as hello following in hello command bar:</span></span>
    
      ![][ic659273]

  * <span data-ttu-id="8d46c-171">Dopo aver fatto clic hello **Connetti** pulsante, sarà richiesta tooopen un file RDP.</span><span class="sxs-lookup"><span data-stu-id="8d46c-171">After clicking hello **Connect** button, you will be prompted tooopen an RDP file.</span></span> <span data-ttu-id="8d46c-172">Aprire il file hello e seguire le istruzioni di hello.</span><span class="sxs-lookup"><span data-stu-id="8d46c-172">Open hello file and follow hello prompts.</span></span> <span data-ttu-id="8d46c-173">(Si può salvare anche il computer locale tooyour di file e quindi eseguire file hello facendovi doppio clic tooremote log in tooyour macchina virtuale senza la necessità di toofirst visitare il portale di gestione di hello.)</span><span class="sxs-lookup"><span data-stu-id="8d46c-173">(You could also save this file tooyour local computer, and then run hello file by double-clicking it tooremote log in tooyour virtual machine without needing toofirst go hello management portal.)</span></span>

  * <span data-ttu-id="8d46c-174">Quando viene chiesto di immettere nome utente hello e una password, immettere i valori hello specificato per l'utente remoto hello e sarà in grado di toolog in.</span><span class="sxs-lookup"><span data-stu-id="8d46c-174">When you are prompted for hello user name and password, enter hello values that you specified for hello remote user and will be able toolog in.</span></span>

> [!NOTE]
> <span data-ttu-id="8d46c-175">Se si utilizza un sistema operativo non Windows, è necessario toouse client Desktop remoto compatibile con il sistema operativo e seguire tooconfigure passaggi hello client con le impostazioni di hello in file con estensione RDP hello che è stato scaricato.</span><span class="sxs-lookup"><span data-stu-id="8d46c-175">If you are on a non-Windows operating system, you need toouse a Remote Desktop client that is compatible with your operating system and follow hello steps tooconfigure that client with hello settings in hello RDP file that you downloaded.</span></span>
> 
> 

## <a name="see-also"></a><span data-ttu-id="8d46c-176">Vedere anche</span><span class="sxs-lookup"><span data-stu-id="8d46c-176">See Also</span></span>
<span data-ttu-id="8d46c-177">[Azure Toolkit for Eclipse][Azure Toolkit for Eclipse]</span><span class="sxs-lookup"><span data-stu-id="8d46c-177">[Azure Toolkit for Eclipse][Azure Toolkit for Eclipse]</span></span>

<span data-ttu-id="8d46c-178">[Creare un'applicazione Hello World per Azure in Eclipse][Creating a Hello World Application for Azure in Eclipse]</span><span class="sxs-lookup"><span data-stu-id="8d46c-178">[Creating a Hello World Application for Azure in Eclipse][Creating a Hello World Application for Azure in Eclipse]</span></span>

<span data-ttu-id="8d46c-179">[L'installazione di hello Azure Toolkit per Eclipse][Installing hello Azure Toolkit for Eclipse]</span><span class="sxs-lookup"><span data-stu-id="8d46c-179">[Installing hello Azure Toolkit for Eclipse][Installing hello Azure Toolkit for Eclipse]</span></span> 

<span data-ttu-id="8d46c-180">Per ulteriori informazioni sull'uso di Azure con Java, vedere hello [Centro per sviluppatori Java di Azure][Azure Java Developer Center].</span><span class="sxs-lookup"><span data-stu-id="8d46c-180">For more information about using Azure with Java, see hello [Azure Java Developer Center][Azure Java Developer Center].</span></span>

<!-- URL List -->

[Azure Java Developer Center]: http://go.microsoft.com/fwlink/?LinkID=699547
[Azure Management Portal]: http://go.microsoft.com/fwlink/?LinkID=512959
[Azure Toolkit for Eclipse]: http://go.microsoft.com/fwlink/?LinkID=699529
[Creating a Hello World Application for Azure in Eclipse]: http://go.microsoft.com/fwlink/?LinkID=699533
[Installing hello Azure Toolkit for Eclipse]: http://go.microsoft.com/fwlink/?LinkId=699546

<!-- IMG List -->

[ic712275]: ./media/azure-toolkit-for-eclipse-enabling-remote-access-for-azure-deployments/ic712275.png
[ic719495]: ./media/azure-toolkit-for-eclipse-enabling-remote-access-for-azure-deployments/ic719495.png
[ic719494]: ./media/azure-toolkit-for-eclipse-enabling-remote-access-for-azure-deployments/ic719494.png
[ic659273]: ./media/azure-toolkit-for-eclipse-enabling-remote-access-for-azure-deployments/ic659273.png

<!-- Legacy MSDN URL = https://msdn.microsoft.com/library/azure/hh690951.aspx -->

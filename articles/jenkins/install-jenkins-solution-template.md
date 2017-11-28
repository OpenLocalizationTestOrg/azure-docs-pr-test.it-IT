---
title: aaaCreate un server Jenkins in Azure
description: Installare Jenkins su una macchina virtuale Linux di Azure dal modello di soluzione Jenkins hello e compilare un'applicazione di esempio Java.
author: mlearned
manager: douge
ms.service: multiple
ms.workload: web
ms.devlang: java
ms.topic: hero-article
ms.date: 08/21/2017
ms.author: mlearned
ms.custom: Jenkins
ms.openlocfilehash: 82ab2ac52594acba131414b449b608978591d4b8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-jenkins-server-on-an-azure-linux-vm-from-hello-azure-portal"></a><span data-ttu-id="7c79c-103">Creare un server Jenkins in una macchina virtuale Linux di Azure dal portale di Azure hello</span><span class="sxs-lookup"><span data-stu-id="7c79c-103">Create a Jenkins server on an Azure Linux VM from hello Azure portal</span></span>

<span data-ttu-id="7c79c-104">Questa Guida introduttiva viene illustrato come tooinstall [Jenkins](https://jenkins.io) in una macchina virtuale Linux Ubuntu con gli strumenti di hello e toowork plug-in configurato con Azure.</span><span class="sxs-lookup"><span data-stu-id="7c79c-104">This quickstart shows how tooinstall [Jenkins](https://jenkins.io) on an Ubuntu Linux VM with hello tools and plug-ins configured toowork with Azure.</span></span> <span data-ttu-id="7c79c-105">Al termine, si avrà un server Jenkins in esecuzione in Azure che compila un'app Java di esempio da [GitHub](https://github.com).</span><span class="sxs-lookup"><span data-stu-id="7c79c-105">When you're finished, you have a Jenkins server running in Azure building a sample Java app from [GitHub](https://github.com).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="7c79c-106">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="7c79c-106">Prerequisites</span></span>

* <span data-ttu-id="7c79c-107">Una sottoscrizione di Azure.</span><span class="sxs-lookup"><span data-stu-id="7c79c-107">An Azure subscription</span></span>
* <span data-ttu-id="7c79c-108">Accesso tooSSH nella riga di comando del computer (ad esempio hello Bash shell o [PuTTY](http://www.putty.org/))</span><span class="sxs-lookup"><span data-stu-id="7c79c-108">Access tooSSH on your computer's command line (such as hello Bash shell or [PuTTY](http://www.putty.org/))</span></span>

[!INCLUDE [quickstarts-free-trial-note](../../includes/quickstarts-free-trial-note.md)]

## <a name="create-hello-jenkins-vm-from-hello-solution-template"></a><span data-ttu-id="7c79c-109">Creare VM Jenkins hello dal modello di soluzione hello</span><span class="sxs-lookup"><span data-stu-id="7c79c-109">Create hello Jenkins VM from hello solution template</span></span>

<span data-ttu-id="7c79c-110">Aprire hello [un'immagine del marketplace per Jenkins](https://azuremarketplace.microsoft.com/marketplace/apps/azure-oss.jenkins?tab=Overview) nel browser web e selezionare **ottenere IT ora** dalla parte sinistra della pagina hello hello.</span><span class="sxs-lookup"><span data-stu-id="7c79c-110">Open hello [marketplace image for Jenkins](https://azuremarketplace.microsoft.com/marketplace/apps/azure-oss.jenkins?tab=Overview) in your web browser and select  **GET IT NOW** from hello left-hand side of hello page.</span></span> <span data-ttu-id="7c79c-111">Hello revisione dei prezzi di dettagli e selezionare **continua**, quindi selezionare **crea** tooconfigure hello Jenkins server hello portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="7c79c-111">Review hello pricing details and select **Continue**, then select **Create** tooconfigure hello Jenkins server in hello Azure portal.</span></span> 
   
![Finestra di dialogo del portale di Azure](./media/install-jenkins-solution-template/ap-create.png)

<span data-ttu-id="7c79c-113">In hello **configurare impostazioni di base** scheda, compilare hello seguenti campi:</span><span class="sxs-lookup"><span data-stu-id="7c79c-113">In hello **Configure basic settings** tab, fill in hello following fields:</span></span>

![Configurare le impostazioni di base](./media/install-jenkins-solution-template/ap-basic.png)

* <span data-ttu-id="7c79c-115">Usare **Jenkins** come **Nome**.</span><span class="sxs-lookup"><span data-stu-id="7c79c-115">Use **Jenkins** for **Name**.</span></span>
* <span data-ttu-id="7c79c-116">Immettere un valore in **Nome utente**.</span><span class="sxs-lookup"><span data-stu-id="7c79c-116">Enter a **User name**.</span></span> <span data-ttu-id="7c79c-117">nome utente Hello deve soddisfare [requisiti specifici](/azure/virtual-machines/linux/faq#what-are-the-username-requirements-when-creating-a-vm).</span><span class="sxs-lookup"><span data-stu-id="7c79c-117">hello user name must meet [specific requirements](/azure/virtual-machines/linux/faq#what-are-the-username-requirements-when-creating-a-vm).</span></span>
* <span data-ttu-id="7c79c-118">Selezionare **Password** come hello **tipo di autenticazione** e immettere una password.</span><span class="sxs-lookup"><span data-stu-id="7c79c-118">Select **Password** as hello **Authentication type** and enter a password.</span></span> <span data-ttu-id="7c79c-119">Hello password deve contenere un carattere maiuscolo, un numero e un carattere speciale.</span><span class="sxs-lookup"><span data-stu-id="7c79c-119">hello password must have an upper case character, a number, and one special character.</span></span>
* <span data-ttu-id="7c79c-120">Utilizzare **myJenkinsResourceGroup** per hello **gruppo di risorse**.</span><span class="sxs-lookup"><span data-stu-id="7c79c-120">Use **myJenkinsResourceGroup** for hello **Resource Group**.</span></span>
* <span data-ttu-id="7c79c-121">Scegliere hello **Stati Uniti orientali** [area Azure](https://azure.microsoft.com/regions/) da hello **percorso** elenco a discesa.</span><span class="sxs-lookup"><span data-stu-id="7c79c-121">Choose hello **East US** [Azure region](https://azure.microsoft.com/regions/) from hello **Location** drop-down.</span></span>

<span data-ttu-id="7c79c-122">Selezionare **OK** tooproceed toohello **configurare le opzioni aggiuntive** scheda. Immettere un server di dominio univoci nome tooidentify hello Jenkins e selezionare **OK**.</span><span class="sxs-lookup"><span data-stu-id="7c79c-122">Select **OK** tooproceed toohello **Configure additional options** tab. Enter a unique domain name tooidentify hello Jenkins server and select **OK**.</span></span>

![Configurare le opzioni aggiuntive](./media/install-jenkins-solution-template/ap-addtional.png)  

 <span data-ttu-id="7c79c-124">Dopo la convalida viene eseguita, selezionare **OK** nuovamente da hello **riepilogo** scheda. Infine, selezionare **acquisto** toocreate hello Jenkins VM.</span><span class="sxs-lookup"><span data-stu-id="7c79c-124">Once validation passes, select **OK** again from hello **Summary** tab. Finally, select **Purchase** toocreate hello Jenkins VM.</span></span> <span data-ttu-id="7c79c-125">Quando il server è pronto, si riceve una notifica in hello portale di Azure:</span><span class="sxs-lookup"><span data-stu-id="7c79c-125">When your server is ready, you get a notification in hello Azure portal:</span></span>   

![Notifica che informa che Jenkins è pronto](./media/install-jenkins-solution-template/jenkins-deploy-notification-ready.png)

## <a name="connect-toojenkins"></a><span data-ttu-id="7c79c-127">Connettersi tooJenkins</span><span class="sxs-lookup"><span data-stu-id="7c79c-127">Connect tooJenkins</span></span>

<span data-ttu-id="7c79c-128">Passare una macchina virtuale tooyour (ad esempio, http://jenkins2517454.eastus.cloudapp.azure.com/) nel web browser.</span><span class="sxs-lookup"><span data-stu-id="7c79c-128">Navigate tooyour virtual machine (for example, http://jenkins2517454.eastus.cloudapp.azure.com/) in  your web browser.</span></span> <span data-ttu-id="7c79c-129">console di Jenkins Hello è accessibile tramite il protocollo HTTP non protette in modo vengono fornite istruzioni sulla console hello pagina tooaccess hello Jenkins in modo sicuro dal computer tramite un tunnel SSH.</span><span class="sxs-lookup"><span data-stu-id="7c79c-129">hello Jenkins console is inaccessible through unsecured HTTP so instructions are provided on hello page tooaccess hello Jenkins console securely from your computer using an SSH tunnel.</span></span>

![Sbloccare Jenkins](./media/install-jenkins-solution-template/jenkins-ssh-instructions.png)

<span data-ttu-id="7c79c-131">Impostare i tunnel hello utilizzando hello `ssh` comando nella pagina di hello dalla riga di comando hello, sostituendo `username` con nome hello di utente amministratore di macchina virtuale hello scelto in precedenza durante la configurazione di macchina virtuale hello dal modello di soluzione hello.</span><span class="sxs-lookup"><span data-stu-id="7c79c-131">Set up hello tunnel using hello `ssh` command on hello page from hello command line, replacing `username` with hello name of hello virtual machine admin user chosen earlier when setting up hello virtual machine from hello solution template.</span></span>

```bash
ssh -L 127.0.0.1:8080:localhost:8080 jenkinsadmin@jenkins2517454.eastus.cloudapp.azure.com
```

<span data-ttu-id="7c79c-132">Dopo aver avviato il tunnel hello, passare toohttp://localhost:8080 / sul computer locale.</span><span class="sxs-lookup"><span data-stu-id="7c79c-132">After you have started hello tunnel, navigate toohttp://localhost:8080/ on your local machine.</span></span> 

<span data-ttu-id="7c79c-133">Ottenere la password iniziale hello eseguendo hello comando nella riga di comando hello connesso tramite SSH toohello Jenkins VM seguente.</span><span class="sxs-lookup"><span data-stu-id="7c79c-133">Get hello initial password by running hello following command in hello command line while connected through SSH toohello Jenkins VM.</span></span>

```bash
`sudo cat /var/lib/jenkins/secrets/initialAdminPassword`.
```

<span data-ttu-id="7c79c-134">Sbloccare dashboard Jenkins hello per hello come primo accesso tramite la password iniziale.</span><span class="sxs-lookup"><span data-stu-id="7c79c-134">Unlock hello Jenkins dashboard for hello first time using this initial password.</span></span>

![Sbloccare Jenkins](./media/install-jenkins-solution-template/jenkins-unlock.png)

<span data-ttu-id="7c79c-136">Selezionare **installare suggeriti i plug-in** hello pagina successiva e quindi creare un dashboard di Jenkins Jenkins amministrazione utente utilizzato tooaccess hello.</span><span class="sxs-lookup"><span data-stu-id="7c79c-136">Select **Install suggested plugins** on hello next page and then create a Jenkins admin user used tooaccess hello Jenkins dashboard.</span></span>

![Jenkins è pronto per l'uso.](./media/install-jenkins-solution-template/jenkins-welcome.png)

<span data-ttu-id="7c79c-138">server Jenkins Hello è ora pronto toobuild codice.</span><span class="sxs-lookup"><span data-stu-id="7c79c-138">hello Jenkins server is now ready toobuild code.</span></span>

## <a name="create-your-first-job"></a><span data-ttu-id="7c79c-139">Creare il primo processo</span><span class="sxs-lookup"><span data-stu-id="7c79c-139">Create your first job</span></span>

<span data-ttu-id="7c79c-140">Selezionare **creare nuovi processi** dalla console di Jenkins hello, quindi denominarlo **mySampleApp** e selezionare **progetto Freestyle**, quindi selezionare **OK**.</span><span class="sxs-lookup"><span data-stu-id="7c79c-140">Select **Create new jobs** from hello Jenkins console, then name it **mySampleApp** and select **Freestyle project**, then select **OK**.</span></span>

![Creare un nuovo processo](./media/install-jenkins-solution-template/jenkins-new-job.png) 

<span data-ttu-id="7c79c-142">Seleziona hello **gestione del codice sorgente** scheda, abilitare **Git**e immettere l'URL nel seguente hello **URL del Repository** campo:`https://github.com/spring-guides/gs-spring-boot.git`</span><span class="sxs-lookup"><span data-stu-id="7c79c-142">Select hello **Source Code Management** tab, enable **Git**, and enter hello following URL in **Repository URL**  field: `https://github.com/spring-guides/gs-spring-boot.git`</span></span>

![Definire i repository Git hello](./media/install-jenkins-solution-template/jenkins-job-git-configuration.png) 

<span data-ttu-id="7c79c-144">Seleziona hello **compilare** tab, quindi selezionare **istruzione di compilazione Aggiungi**, **script richiamare Gradle**.</span><span class="sxs-lookup"><span data-stu-id="7c79c-144">Select hello **Build** tab, then select **Add build step**, **Invoke Gradle script**.</span></span> <span data-ttu-id="7c79c-145">Selezionare **Use Gradle Wrapper** (Usa wrapper di Gradle) e quindi immettere `complete` in **Wrapper location** (Percorso wrapper) e `build` in **Tasks** (Attività).</span><span class="sxs-lookup"><span data-stu-id="7c79c-145">Select **Use Gradle Wrapper**, then enter `complete` in **Wrapper location** and `build` for **Tasks**.</span></span>

![Utilizzare toobuild wrapper di Gradle hello](./media/install-jenkins-solution-template/jenkins-job-gradle-config.png) 

<span data-ttu-id="7c79c-147">Selezionare **Advanced** (Avanzate)</span><span class="sxs-lookup"><span data-stu-id="7c79c-147">Select **Advanced..**</span></span> <span data-ttu-id="7c79c-148">e quindi immettere `complete` in hello **radice compilazione script** campo.</span><span class="sxs-lookup"><span data-stu-id="7c79c-148">and then enter `complete` in hello **Root Build script** field.</span></span> <span data-ttu-id="7c79c-149">Selezionare **Salva**.</span><span class="sxs-lookup"><span data-stu-id="7c79c-149">Select **Save**.</span></span>

![Impostare le impostazioni avanzate in fase di compilazione hello Gradle wrapper](./media/install-jenkins-solution-template/jenkins-job-gradle-advances.png) 

## <a name="build-hello-code"></a><span data-ttu-id="7c79c-151">Compilare il codice hello</span><span class="sxs-lookup"><span data-stu-id="7c79c-151">Build hello code</span></span>

<span data-ttu-id="7c79c-152">Selezionare **compilare ora** toocompile hello codice e i pacchetti hello app di esempio.</span><span class="sxs-lookup"><span data-stu-id="7c79c-152">Select **Build Now** toocompile hello code and package hello sample app.</span></span> <span data-ttu-id="7c79c-153">Al termine della compilazione, selezionare hello **dell'area di lavoro** collegamento per un progetto di hello.</span><span class="sxs-lookup"><span data-stu-id="7c79c-153">When your build completes, select hello **Workspace** link for hello project.</span></span>

![Sfoglia file JAR da compilazione hello toohello dell'area di lavoro tooget hello](./media/install-jenkins-solution-template/jenkins-access-workspace.png) 

<span data-ttu-id="7c79c-155">Passare troppo`complete/build/libs` e verificare hello `gs-spring-boot-0.1.0.jar` esiste tooverify la riuscita della compilazione.</span><span class="sxs-lookup"><span data-stu-id="7c79c-155">Navigate too`complete/build/libs` and ensure hello `gs-spring-boot-0.1.0.jar` is there tooverify that your build was successful.</span></span> <span data-ttu-id="7c79c-156">Il server è diventato di Jenkins pronto toobuild progetti in Azure.</span><span class="sxs-lookup"><span data-stu-id="7c79c-156">Your Jenkins server is now ready toobuild your own projects in Azure.</span></span>

## <a name="next-steps"></a><span data-ttu-id="7c79c-157">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="7c79c-157">Next Steps</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="7c79c-158">Aggiungere VM di Azure come agenti di Jenkins</span><span class="sxs-lookup"><span data-stu-id="7c79c-158">Add Azure VMs as Jenkins agents</span></span>](jenkins-azure-vm-agents.md)

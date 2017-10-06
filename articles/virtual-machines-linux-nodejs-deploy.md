---
title: aaaDeploy un tooLinux applicazione Node.js macchine virtuali in Azure
description: Informazioni su come toodeploy un Node.js applicazione tooLinux le macchine virtuali in Azure.
services: 
documentationcenter: nodejs
author: stepro
manager: dmitryr
editor: 
ROBOTS: NOINDEX, NOFOLLOW
redirect_url: /azure
ms.assetid: 857a812d-c73e-4af7-a985-2d0baf8b6f71
ms.service: multiple
ms.devlang: nodejs
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 02/02/2016
ms.author: stephpr
ms.openlocfilehash: e876c8170a06f102f7f32ec7cb930b876647a707
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-a-nodejs-application-toolinux-virtual-machines-in-azure"></a><span data-ttu-id="1fe1a-103">Distribuire un tooLinux applicazione Node.js macchine virtuali in Azure</span><span class="sxs-lookup"><span data-stu-id="1fe1a-103">Deploy a Node.js application tooLinux Virtual Machines in Azure</span></span>
<span data-ttu-id="1fe1a-104">Questa esercitazione viene illustrato come un'applicazione Node.js tootake e distribuirlo tooLinux le macchine virtuali in esecuzione in Azure.</span><span class="sxs-lookup"><span data-stu-id="1fe1a-104">This tutorial shows how tootake a Node.js application and deploy it tooLinux virtual machines running in Azure.</span></span> <span data-ttu-id="1fe1a-105">istruzioni di Hello in questa esercitazione possono essere seguite su qualsiasi sistema operativo che è in grado di eseguire Node.js.</span><span class="sxs-lookup"><span data-stu-id="1fe1a-105">hello instructions in this tutorial can be followed on any operating system that is capable of running Node.js.</span></span>

<span data-ttu-id="1fe1a-106">Si apprenderà come:</span><span class="sxs-lookup"><span data-stu-id="1fe1a-106">You'll learn how to:</span></span>

* <span data-ttu-id="1fe1a-107">Eseguire il fork e la clonazione di un repository GitHub contenente una semplice applicazione TODO;</span><span class="sxs-lookup"><span data-stu-id="1fe1a-107">Fork and clone a GitHub repository containing a simple TODO application;</span></span>
* <span data-ttu-id="1fe1a-108">Creare e configurare due macchine virtuali Linux in un'applicazione hello Azure toorun;</span><span class="sxs-lookup"><span data-stu-id="1fe1a-108">Create and configure two Linux virtual machines in Azure toorun hello application;</span></span>
* <span data-ttu-id="1fe1a-109">Eseguire l'iterazione in un'applicazione hello trasferendo la macchina virtuale aggiornamenti toohello web front-end.</span><span class="sxs-lookup"><span data-stu-id="1fe1a-109">Iterate on hello application by pushing updates toohello web frontend virtual machine.</span></span>

> [!NOTE]
> <span data-ttu-id="1fe1a-110">toocomplete questa esercitazione, è necessario un account GitHub e un account di Microsoft Azure e hello possibilità toouse Git da un computer di sviluppo.</span><span class="sxs-lookup"><span data-stu-id="1fe1a-110">toocomplete this tutorial, you need a GitHub account and a Microsoft Azure account, and hello ability toouse Git from a development machine.</span></span>
> 
> <span data-ttu-id="1fe1a-111">Se non si ha un account GitHub, è possibile iscriversi [qui](https://github.com/join).</span><span class="sxs-lookup"><span data-stu-id="1fe1a-111">If you don't have a GitHub account, you can sign up [here](https://github.com/join).</span></span>
> 
> <span data-ttu-id="1fe1a-112">Se non si ha un account [Microsoft Azure](https://azure.microsoft.com/), è possibile iscriversi [qui](https://azure.microsoft.com/pricing/free-trial/) per ottenere una versione di prova GRATUITA.</span><span class="sxs-lookup"><span data-stu-id="1fe1a-112">If you don't have a [Microsoft Azure](https://azure.microsoft.com/) account, you can sign up for a FREE trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span> <span data-ttu-id="1fe1a-113">Questo consentirà anche attraverso hello iscrizione processo per un [Account Microsoft](http://account.microsoft.com) se non hai già uno.</span><span class="sxs-lookup"><span data-stu-id="1fe1a-113">This will also lead you through hello sign up process for a [Microsoft Account](http://account.microsoft.com) if you do not already have one.</span></span> <span data-ttu-id="1fe1a-114">In alternativa, se si è eseguita la sottoscrizione a Visual Studio, è possibile [attivare i vantaggi di MSDN](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/?WT.mc_id=A261C142F).</span><span class="sxs-lookup"><span data-stu-id="1fe1a-114">Alternatively, if you are a Visual Studio subscriber, you can [activate your MSDN benefits](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/?WT.mc_id=A261C142F).</span></span>
> 
> <span data-ttu-id="1fe1a-115">Se sul computer di sviluppo non è presente GIT e si usa un sistema Macintosh o Windows, è possibile installarlo da [qui](http://www.git-scm.com).</span><span class="sxs-lookup"><span data-stu-id="1fe1a-115">If you do not have git on your development machine, then if you are using a Macintosh or Windows machine, install git from [here](http://www.git-scm.com).</span></span> <span data-ttu-id="1fe1a-116">Se si utilizza Linux, installare git utilizzando il meccanismo di hello più appropriato, ad esempio `sudo apt-get install git`.</span><span class="sxs-lookup"><span data-stu-id="1fe1a-116">If you are using Linux, install git using hello mechanism most appropriate for you, such as `sudo apt-get install git`.</span></span>
> 
> 

## <a name="forking-and-cloning-hello-todo-application"></a><span data-ttu-id="1fe1a-117">Duplicazione e clonazione hello applicazione TODO</span><span class="sxs-lookup"><span data-stu-id="1fe1a-117">Forking and Cloning hello TODO Application</span></span>
<span data-ttu-id="1fe1a-118">Hello applicazione TODO usata da questa esercitazione implementa un front-end web semplici su un'istanza di MongoDB che tiene traccia di un elenco di attività.</span><span class="sxs-lookup"><span data-stu-id="1fe1a-118">hello TODO application used by this tutorial implements a simple web frontend over a MongoDB instance that keeps track of a TODO list.</span></span> <span data-ttu-id="1fe1a-119">Dopo avere effettuato l'accesso tooGitHub, andare [qui](https://github.com/stepro/node-todo) toofind hello applicazione e tramite il collegamento di hello in alto a destra hello fork.</span><span class="sxs-lookup"><span data-stu-id="1fe1a-119">After signing in tooGitHub, go [here](https://github.com/stepro/node-todo) toofind hello application and fork it using hello link in hello top right.</span></span> <span data-ttu-id="1fe1a-120">In questo modo verrà creato un repository nell'account denominato *nomeaccount*/node-todo.</span><span class="sxs-lookup"><span data-stu-id="1fe1a-120">This should create a repository in your account named *accountname*/node-todo.</span></span>

<span data-ttu-id="1fe1a-121">A questo punto, clonare il repository nel computer di sviluppo:</span><span class="sxs-lookup"><span data-stu-id="1fe1a-121">Now on your development machine, clone this repository:</span></span>

    git clone https://github.com/accountname/node-todo.git

<span data-ttu-id="1fe1a-122">Si userà il clone del repository hello locale leggermente in un secondo momento quando si apportano modifiche di codice sorgente toohello.</span><span class="sxs-lookup"><span data-stu-id="1fe1a-122">We'll use this local clone of hello repository a little later when making changes toohello source code.</span></span>

## <a name="creating-and-configuring-hello-linux-virtual-machines"></a><span data-ttu-id="1fe1a-123">Creazione e configurazione di hello macchine virtuali Linux</span><span class="sxs-lookup"><span data-stu-id="1fe1a-123">Creating and Configuring hello Linux Virtual Machines</span></span>
<span data-ttu-id="1fe1a-124">Azure supporta il calcolo non elaborato mediante macchine virtuali Linux.</span><span class="sxs-lookup"><span data-stu-id="1fe1a-124">Azure has great support for raw compute using Linux virtual machines.</span></span> <span data-ttu-id="1fe1a-125">Questa parte dei programmi di esercitazione hello come si può creare rapidamente due macchine virtuali Linux e distribuire facilmente hello TODO applicazione toothem, in esecuzione hello front-end web in uno e hello istanza MongoDB hello altri.</span><span class="sxs-lookup"><span data-stu-id="1fe1a-125">This part of hello tutorial shows how you can easily spin up two Linux virtual machines and deploy hello TODO application toothem, running hello web frontend on one and hello MongoDB instance on hello other.</span></span>

### <a name="creating-virtual-machines"></a><span data-ttu-id="1fe1a-126">Creazione di macchine virtuali</span><span class="sxs-lookup"><span data-stu-id="1fe1a-126">Creating Virtual Machines</span></span>
<span data-ttu-id="1fe1a-127">toocreate modo più semplice di Hello una nuova macchina virtuale in Azure è toouse hello portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="1fe1a-127">hello easiest way toocreate a new virtual machine in Azure is toouse hello Azure Portal.</span></span> <span data-ttu-id="1fe1a-128">Fare clic su [qui](https://portal.azure.com) toosign in e avviare hello portale di Azure nel web browser.</span><span class="sxs-lookup"><span data-stu-id="1fe1a-128">Click [here](https://portal.azure.com) toosign in and launch hello Azure Portal in your web browser.</span></span> <span data-ttu-id="1fe1a-129">Una volta caricate hello portale di Azure, completare hello alla procedura seguente:</span><span class="sxs-lookup"><span data-stu-id="1fe1a-129">Once hello Azure Portal has loaded, complete hello following steps:</span></span>

* <span data-ttu-id="1fe1a-130">Fare clic su salve "+ nuovo" collegamento;</span><span class="sxs-lookup"><span data-stu-id="1fe1a-130">Click hello "+ New" link;</span></span>
* <span data-ttu-id="1fe1a-131">Selezionare una categoria "Calcolo" hello e scegliere "Ubuntu Server 14.04 LTS";</span><span class="sxs-lookup"><span data-stu-id="1fe1a-131">Pick hello "Compute" category and choose "Ubuntu Server 14.04 LTS";</span></span>
* <span data-ttu-id="1fe1a-132">Seleziona modello di distribuzione di "gestione di risorse" hello e fare clic su "Crea";</span><span class="sxs-lookup"><span data-stu-id="1fe1a-132">Select hello "Resource Manager" deployment model and click "Create";</span></span>
* <span data-ttu-id="1fe1a-133">Compilare nozioni di base hello attenendosi alle linee guida:</span><span class="sxs-lookup"><span data-stu-id="1fe1a-133">Fill in hello basics following these guidelines:</span></span>
  * <span data-ttu-id="1fe1a-134">Specificare un nome facilmente identificabile in un secondo momento</span><span class="sxs-lookup"><span data-stu-id="1fe1a-134">Specify a name you can easily identify later;</span></span>
  * <span data-ttu-id="1fe1a-135">Per questa esercitazione, scegliere Autenticazione password</span><span class="sxs-lookup"><span data-stu-id="1fe1a-135">For this tutorial, choose Password authentication;</span></span>
  * <span data-ttu-id="1fe1a-136">Creare un nuovo gruppo di risorse con un nome identificabile</span><span class="sxs-lookup"><span data-stu-id="1fe1a-136">Create a new resource group with an identifiable name.</span></span>
* <span data-ttu-id="1fe1a-137">Per la dimensione della macchina virtuale hello, "A1 Standard" è una scelta ragionevole per questa esercitazione.</span><span class="sxs-lookup"><span data-stu-id="1fe1a-137">For hello Virtual Machine size, "A1 Standard" is a reasonable choice for this tutorial.</span></span>
* <span data-ttu-id="1fe1a-138">Per le impostazioni aggiuntive, verificare il tipo di disco hello "Standard" e accettare che tutti hello impostazioni predefinite rimanenti.</span><span class="sxs-lookup"><span data-stu-id="1fe1a-138">For additional settings, ensure hello disk type is "Standard" and accept all hello remaining defaults.</span></span>
* <span data-ttu-id="1fe1a-139">Avviare la creazione di hello nella pagina Riepilogo hello.</span><span class="sxs-lookup"><span data-stu-id="1fe1a-139">Kick off hello creation on hello summary page.</span></span>

<span data-ttu-id="1fe1a-140">Eseguire hello precedente elaborare due volte toocreate due le macchine virtuali Linux, uno per front-end web hello e uno per l'istanza di MongoDB hello.</span><span class="sxs-lookup"><span data-stu-id="1fe1a-140">Perform hello above process twice toocreate two Linux virtual machines, one for hello web frontend and one for hello MongoDB instance.</span></span> <span data-ttu-id="1fe1a-141">Creazione di macchine virtuali hello richiederà circa 5-10 minuti.</span><span class="sxs-lookup"><span data-stu-id="1fe1a-141">Creation of hello virtual machines will take about 5-10 minutes.</span></span>

### <a name="assigning-a-dns-entry-for-virtual-machines"></a><span data-ttu-id="1fe1a-142">Assegnazione di una voce DNS per le macchine virtuali</span><span class="sxs-lookup"><span data-stu-id="1fe1a-142">Assigning a DNS entry for Virtual Machines</span></span>
<span data-ttu-id="1fe1a-143">Per impostazione predefinita, è possibile accedere alle macchine virtuali create in Azure solo mediante un indirizzo IP pubblico, ad esempio 1.2.3.4.</span><span class="sxs-lookup"><span data-stu-id="1fe1a-143">Virtual machines created in Azure are by default only accessible through a public IP address like 1.2.3.4.</span></span> <span data-ttu-id="1fe1a-144">Verifichiamo macchine hello più facilmente identificabili assegnando le voci DNS.</span><span class="sxs-lookup"><span data-stu-id="1fe1a-144">Let's make hello machines more easily identifiable by assigning them DNS entries.</span></span>

<span data-ttu-id="1fe1a-145">Una volta portale hello indica che le macchine virtuali hello siano state create, fare clic sul collegamento "Macchine virtuali" hello nella barra di spostamento sinistro hello e individuare i computer.</span><span class="sxs-lookup"><span data-stu-id="1fe1a-145">Once hello portal indicates that hello virtual machines have been created, click on hello "Virtual machines" link in hello left navbar and locate your machines.</span></span> <span data-ttu-id="1fe1a-146">Per ogni macchina virtuale:</span><span class="sxs-lookup"><span data-stu-id="1fe1a-146">For each machine:</span></span>

* <span data-ttu-id="1fe1a-147">Scheda Essentials hello di individuare e fare clic su indirizzo IP pubblico; hello</span><span class="sxs-lookup"><span data-stu-id="1fe1a-147">Locate hello Essentials tab and click on hello Public IP Address;</span></span>
* <span data-ttu-id="1fe1a-148">Nella configurazione degli indirizzi IP pubblici hello, assegnare un'etichetta del nome DNS e salvare.</span><span class="sxs-lookup"><span data-stu-id="1fe1a-148">In hello public IP address configuration, assign a DNS name label and save.</span></span>

<span data-ttu-id="1fe1a-149">portale Hello garantisce che si specifica il nome di hello sia disponibile.</span><span class="sxs-lookup"><span data-stu-id="1fe1a-149">hello portal will ensure that hello name you specify is available.</span></span> <span data-ttu-id="1fe1a-150">Dopo aver salvato la configurazione hello, le macchine virtuali avranno nomi host troppo`machinename.region.cloudapp.azure.com`.</span><span class="sxs-lookup"><span data-stu-id="1fe1a-150">After saving hello configuration, your virtual machines will have host names similar too`machinename.region.cloudapp.azure.com`.</span></span>

### <a name="connecting-toohello-virtual-machines"></a><span data-ttu-id="1fe1a-151">Connessione toohello macchine virtuali</span><span class="sxs-lookup"><span data-stu-id="1fe1a-151">Connecting toohello Virtual Machines</span></span>
<span data-ttu-id="1fe1a-152">Quando è stato eseguito il provisioning delle macchine virtuali, erano le connessioni remote tooallow preconfigurata su SSH.</span><span class="sxs-lookup"><span data-stu-id="1fe1a-152">When your virtual machines were provisioned, they were pre-configured tooallow remote connections over SSH.</span></span> <span data-ttu-id="1fe1a-153">Questo è il meccanismo di hello utilizzeremo tooconfigure hello le macchine virtuali.</span><span class="sxs-lookup"><span data-stu-id="1fe1a-153">This is hello mechanism we will use tooconfigure hello virtual machines.</span></span> <span data-ttu-id="1fe1a-154">Se si utilizza Windows per lo sviluppo, è necessario un client SSH tooget se non hai già uno.</span><span class="sxs-lookup"><span data-stu-id="1fe1a-154">If you are using Windows for your development, you will need tooget an SSH client if you do not already have one.</span></span> <span data-ttu-id="1fe1a-155">Una soluzione comune è usare PuTTY, scaricabile da [qui](http://www.chiark.greenend.org.uk/~sgtatham/putty/).</span><span class="sxs-lookup"><span data-stu-id="1fe1a-155">A common choice here is PuTTY, which can be downloaded from [here](http://www.chiark.greenend.org.uk/~sgtatham/putty/).</span></span> <span data-ttu-id="1fe1a-156">I sistemi operativi Macintosh e Linux vengono forniti con una versione di SSH preinstallata.</span><span class="sxs-lookup"><span data-stu-id="1fe1a-156">Macintosh and Linux OSes come with a version of SSH pre-installed.</span></span>

### <a name="configuring-hello-web-frontend-virtual-machine"></a><span data-ttu-id="1fe1a-157">Configurazione di macchina virtuale di front-end Web hello</span><span class="sxs-lookup"><span data-stu-id="1fe1a-157">Configuring hello Web Frontend Virtual Machine</span></span>
<span data-ttu-id="1fe1a-158">Computer front-end web toohello SSH che è stato creato tramite PuTTY, ssh riga di comando o lo strumento SSH altri preferito.</span><span class="sxs-lookup"><span data-stu-id="1fe1a-158">SSH toohello web frontend machine you created using PuTTY, ssh command line or your other favorite SSH tool.</span></span> <span data-ttu-id="1fe1a-159">Verrà visualizzato un messaggio di benvenuto seguito da un prompt dei comandi:</span><span class="sxs-lookup"><span data-stu-id="1fe1a-159">You should see a welcome message followed by a command prompt.</span></span>

<span data-ttu-id="1fe1a-160">Assicurarsi innanzitutto che GIT e il nodo siano entrambi installati:</span><span class="sxs-lookup"><span data-stu-id="1fe1a-160">First, let's make sure that git and node are both installed:</span></span>

    sudo apt-get install -y git
    curl -sL https://deb.nodesource.com/setup_4.x | sudo -E bash -
    sudo apt-get install -y nodejs

<span data-ttu-id="1fe1a-161">Poiché front-end web dell'applicazione hello si basa su alcuni moduli Node.js nativi, è necessario anche set essenziale di hello tooinstall di strumenti di compilazione:</span><span class="sxs-lookup"><span data-stu-id="1fe1a-161">Since hello application's web frontend relies on some native Node.js modules, we also need tooinstall hello essential set of build tools:</span></span>

    sudo apt-get install -y build-essential

<span data-ttu-id="1fe1a-162">Infine, si installano un'applicazione di Node.js chiamata *forever*, che consente di toorun Node.js server applicazioni:</span><span class="sxs-lookup"><span data-stu-id="1fe1a-162">Finally, let's install a Node.js application called *forever*, which helps toorun Node.js server applications:</span></span>

    sudo npm install -g forever

<span data-ttu-id="1fe1a-163">Questi sono tutte le dipendenze di hello necessarie nel front-end web dell'applicazione questa macchina virtuale toobe toorun in grado di hello, così possiamo procedere all'esecuzione di applicazioni.</span><span class="sxs-lookup"><span data-stu-id="1fe1a-163">These are all hello dependencies needed on this virtual machine toobe able toorun hello application's web frontend, so let's get that running.</span></span> <span data-ttu-id="1fe1a-164">toodo, prima di tutto creata è un clone del repository GitHub hello è duplicato in precedenza in modo che è possibile pubblicare facilmente gli aggiornamenti macchina virtuale di toohello (verranno descritte in questo scenario di aggiornamento in un secondo momento) e quindi clonare hello clone bare tooprovide bare una versione di hello repository che in realtà può essere eseguito.</span><span class="sxs-lookup"><span data-stu-id="1fe1a-164">toodo this, we will first create a bare clone of hello GitHub repository you previously forked so that you can easily publish updates toohello virtual machine (we'll cover this update scenario later), and then clone hello bare clone tooprovide a version of hello repository that can actually be executed.</span></span>

<span data-ttu-id="1fe1a-165">A partire dalla directory home (~) hello, eseguire hello comandi seguente (sostituendo *accountname* con il nome dell'account utente GitHub):</span><span class="sxs-lookup"><span data-stu-id="1fe1a-165">Starting from hello home (~) directory, run hello following commands (replacing *accountname* with your GitHub user account name):</span></span>

    git clone --bare https://github.com/accountname/node-todo.git
    git clone node-todo.git

<span data-ttu-id="1fe1a-166">Ora immettere hello nodo todo directory ed eseguire questi comandi:</span><span class="sxs-lookup"><span data-stu-id="1fe1a-166">Now enter hello node-todo directory and run these commands:</span></span>

    npm install
    forever start server.js

<span data-ttu-id="1fe1a-167">Hello front-end web dell'applicazione è in esecuzione, tuttavia non esiste un altro passaggio prima di accedere a un'applicazione hello da un web browser.</span><span class="sxs-lookup"><span data-stu-id="1fe1a-167">hello application's web frontend is now running, however there is one more step before you can access hello application from a web browser.</span></span> <span data-ttu-id="1fe1a-168">Hello macchina virtuale creata è protetta da una risorsa di Azure chiamata un *il gruppo di sicurezza di rete*, che è stato creato per quando è stato eseguito il provisioning hello macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="1fe1a-168">hello virtual machine you created is protected by an Azure resource called a *network security group*, which was created for you when you provisioned hello virtual machine.</span></span> <span data-ttu-id="1fe1a-169">Attualmente, questa risorsa consente solo le richieste esterne tooport toobe 22 indirizzato toohello macchina virtuale, che consente le comunicazioni SSH con hello macchina, ma nessun altro elemento.</span><span class="sxs-lookup"><span data-stu-id="1fe1a-169">Currently, this resource only allows external requests tooport 22 toobe routed toohello virtual machine, which enables SSH communication with hello machine but nothing else.</span></span> <span data-ttu-id="1fe1a-170">In hello tooview ordine applicazione TODO, vale a dire toorun configurato sulla porta 8080, pertanto questa porta deve anche toobe aperto.</span><span class="sxs-lookup"><span data-stu-id="1fe1a-170">So in order tooview hello TODO application, which is configured toorun on port 8080, this port also needs toobe opened up.</span></span>

<span data-ttu-id="1fe1a-171">Restituire toohello portale di Azure e completare hello alla procedura seguente:</span><span class="sxs-lookup"><span data-stu-id="1fe1a-171">Return toohello Azure Portal and complete hello following steps:</span></span>

* <span data-ttu-id="1fe1a-172">Fare clic su "Gruppi di risorse" nella barra di spostamento sinistro hello;</span><span class="sxs-lookup"><span data-stu-id="1fe1a-172">Click on "Resource groups" in hello left navbar;</span></span>
* <span data-ttu-id="1fe1a-173">Selezionare gruppo di risorse hello che contiene la macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="1fe1a-173">Select hello resource group that contains your virtual machine;</span></span>
* <span data-ttu-id="1fe1a-174">Nell'elenco risultante di hello delle risorse, selezionare gruppo di sicurezza di rete hello (Buongiorno uno con un'icona dello scudo);</span><span class="sxs-lookup"><span data-stu-id="1fe1a-174">In hello resulting list of resources, select hello network security group (hello one with a shield icon);</span></span>
* <span data-ttu-id="1fe1a-175">Nelle proprietà hello, scegliere "regole di sicurezza in ingresso";</span><span class="sxs-lookup"><span data-stu-id="1fe1a-175">In hello properties, choose "Inbound security rules";</span></span>
* <span data-ttu-id="1fe1a-176">Nella barra degli strumenti hello, fare clic su "Aggiungi".</span><span class="sxs-lookup"><span data-stu-id="1fe1a-176">In hello toolbar, click "Add";</span></span>
* <span data-ttu-id="1fe1a-177">Specificare un nome, ad esempio "default-allow-todo"</span><span class="sxs-lookup"><span data-stu-id="1fe1a-177">Provide a name like "default-allow-todo";</span></span>
* <span data-ttu-id="1fe1a-178">Impostare il protocollo hello troppo "TCP";</span><span class="sxs-lookup"><span data-stu-id="1fe1a-178">Set hello protocol too"TCP";</span></span>
* <span data-ttu-id="1fe1a-179">Impostare l'intervallo di porte di destinazione hello troppo "8080;"</span><span class="sxs-lookup"><span data-stu-id="1fe1a-179">Set hello destination port range too"8080";</span></span>
* <span data-ttu-id="1fe1a-180">Fare clic su OK e attendere hello toobe di regola di sicurezza creato.</span><span class="sxs-lookup"><span data-stu-id="1fe1a-180">Click OK and wait for hello security rule toobe created.</span></span>

<span data-ttu-id="1fe1a-181">Dopo aver creato la regola di sicurezza, è visibile pubblicamente su hello applicazione TODO hello internet ed è possibile esplorare tooit, ad esempio tramite un URL, ad esempio:</span><span class="sxs-lookup"><span data-stu-id="1fe1a-181">After creating this security rule, hello TODO application is publically visible on hello internet and you can browse tooit, for instance using a URL such as:</span></span>

    http://machinename.region.cloudapp.azure.com:8080

<span data-ttu-id="1fe1a-182">Si noterà anche se non è stato ancora configurato macchina virtuale di MongoDB hello, hello applicazione TODO viene visualizzato toobe piuttosto funzionale.</span><span class="sxs-lookup"><span data-stu-id="1fe1a-182">You will notice that even though we have not yet configured hello MongoDB virtual machine, hello TODO application appears toobe quite functional.</span></span> <span data-ttu-id="1fe1a-183">In questo modo il repository di codice sorgente hello è hardcoded toouse un'istanza di MongoDB già distribuita.</span><span class="sxs-lookup"><span data-stu-id="1fe1a-183">This is because hello source repository is hardcoded toouse a pre-deployed MongoDB instance.</span></span> <span data-ttu-id="1fe1a-184">Dopo che è stato configurato macchina virtuale di MongoDB hello, si verrà tornare indietro e modificare hello origine codice tooutilize dell'istanza di MongoDB privata invece.</span><span class="sxs-lookup"><span data-stu-id="1fe1a-184">Once we have configured hello MongoDB virtual machine, we will go back and change hello source code tooutilize our private MongoDB instance instead.</span></span>

### <a name="configuring-hello-mongodb-virtual-machine"></a><span data-ttu-id="1fe1a-185">Configurazione di macchina virtuale di MongoDB hello</span><span class="sxs-lookup"><span data-stu-id="1fe1a-185">Configuring hello MongoDB Virtual Machine</span></span>
<span data-ttu-id="1fe1a-186">SSH toohello secondo computer che è stato creato tramite PuTTY, ssh riga di comando o lo strumento SSH altri preferito.</span><span class="sxs-lookup"><span data-stu-id="1fe1a-186">SSH toohello second machine you created using PuTTY, ssh command line or your other favorite SSH tool.</span></span> <span data-ttu-id="1fe1a-187">Dopo aver visualizzato un messaggio di benvenuto hello e il prompt dei comandi, installare MongoDB (queste istruzioni sono state ricavate dalla [qui](https://docs.mongodb.org/master/tutorial/install-mongodb-on-ubuntu/)):</span><span class="sxs-lookup"><span data-stu-id="1fe1a-187">After seeing hello welcome message and command prompt, install MongoDB (these instructions were taken from [here](https://docs.mongodb.org/master/tutorial/install-mongodb-on-ubuntu/)):</span></span>

    sudo apt-key adv --keyserver hkp://keyserver.ubuntu.com:80 --recv EA312927
    echo "deb http://repo.mongodb.org/apt/ubuntu trusty/mongodb-org/3.2 multiverse" | sudo tee /etc/apt/sources.list.d/mongodb-org-3.2.list
    sudo apt-get update
    sudo apt-get install -y mongodb-org

<span data-ttu-id="1fe1a-188">Per impostazione predefinita, MongoDB è configurato in modo da essere accessibile solo in locale.</span><span class="sxs-lookup"><span data-stu-id="1fe1a-188">By default, MongoDB is configured so it can only be accessed locally.</span></span> <span data-ttu-id="1fe1a-189">Per questa esercitazione, MongoDB verrà configurato in modo è possibile accedere dalla macchina virtuale dell'applicazione hello.</span><span class="sxs-lookup"><span data-stu-id="1fe1a-189">For this tutorial, we will configure MongoDB so it can be accessed from hello application's virtual machine.</span></span> <span data-ttu-id="1fe1a-190">In un contesto di sudo, aprire il file /etc/mongod.conf hello e individuare hello `# network interfaces` sezione.</span><span class="sxs-lookup"><span data-stu-id="1fe1a-190">In a sudo context, open hello /etc/mongod.conf file and locate hello `# network interfaces` section.</span></span> <span data-ttu-id="1fe1a-191">Hello modifica `net.bindIp` configurazione valore troppo`0.0.0.0`.</span><span class="sxs-lookup"><span data-stu-id="1fe1a-191">Change hello `net.bindIp` configuration value too`0.0.0.0`.</span></span>

> [!NOTE]
> <span data-ttu-id="1fe1a-192">Questa configurazione è per scopi di hello solo questa esercitazione.</span><span class="sxs-lookup"><span data-stu-id="1fe1a-192">This configuration is for hello purposes of this tutorial only.</span></span> <span data-ttu-id="1fe1a-193">**NON** è una procedura di sicurezza consigliata e non deve essere usata in ambienti di produzione.</span><span class="sxs-lookup"><span data-stu-id="1fe1a-193">It is **NOT** a recommended security practice and should not be used in production environments.</span></span>
> 
> 

<span data-ttu-id="1fe1a-194">Verificare ora hello MongoDB servizio è stato avviato:</span><span class="sxs-lookup"><span data-stu-id="1fe1a-194">Now ensure hello MongoDB service has been started:</span></span>

    sudo service mongod restart

<span data-ttu-id="1fe1a-195">Per impostazione predefinita, MongoDB è attivo sulla porta 27017.</span><span class="sxs-lookup"><span data-stu-id="1fe1a-195">MongoDB operates over port 27017 by default.</span></span> <span data-ttu-id="1fe1a-196">Pertanto, in hello allo stesso modo che era necessaria tooopen porta 8080 sulla macchina virtuale di hello web front-end, è necessario tooopen porta 27017 macchina virtuale di MongoDB hello.</span><span class="sxs-lookup"><span data-stu-id="1fe1a-196">So, in hello same way that we needed tooopen port 8080 on hello web frontend virtual machine, we need tooopen port 27017 on hello MongoDB virtual machine.</span></span>

<span data-ttu-id="1fe1a-197">Restituire toohello portale di Azure e completare hello alla procedura seguente:</span><span class="sxs-lookup"><span data-stu-id="1fe1a-197">Return toohello Azure Portal and complete hello following steps:</span></span>

* <span data-ttu-id="1fe1a-198">Fare clic su "Gruppi di risorse" nella barra di spostamento sinistro hello;</span><span class="sxs-lookup"><span data-stu-id="1fe1a-198">Click on "Resource groups" in hello left navbar;</span></span>
* <span data-ttu-id="1fe1a-199">Selezionare gruppo di risorse hello che contiene una macchina virtuale di MongoDB hello.</span><span class="sxs-lookup"><span data-stu-id="1fe1a-199">Select hello resource group that contains hello MongoDB virtual machine;</span></span>
* <span data-ttu-id="1fe1a-200">Nell'elenco risultante di hello delle risorse, selezionare gruppo di sicurezza di rete hello (Buongiorno uno con un'icona dello scudo) con stesso nome assegnato macchina virtuale di MongoDB toohello; hello</span><span class="sxs-lookup"><span data-stu-id="1fe1a-200">In hello resulting list of resources, select hello network security group (hello one with a shield icon) with hello same name that you gave toohello MongoDB virtual machine;</span></span>
* <span data-ttu-id="1fe1a-201">Nelle proprietà hello, scegliere "regole di sicurezza in ingresso";</span><span class="sxs-lookup"><span data-stu-id="1fe1a-201">In hello properties, choose "Inbound security rules";</span></span>
* <span data-ttu-id="1fe1a-202">Nella barra degli strumenti hello, fare clic su "Aggiungi".</span><span class="sxs-lookup"><span data-stu-id="1fe1a-202">In hello toolbar, click "Add";</span></span>
* <span data-ttu-id="1fe1a-203">Specificare un nome, ad esempio "default-allow-mongo"</span><span class="sxs-lookup"><span data-stu-id="1fe1a-203">Provide a name like "default-allow-mongo";</span></span>
* <span data-ttu-id="1fe1a-204">Impostare il protocollo hello troppo "TCP";</span><span class="sxs-lookup"><span data-stu-id="1fe1a-204">Set hello protocol too"TCP";</span></span>
* <span data-ttu-id="1fe1a-205">Impostare l'intervallo di porte di destinazione hello troppo "27017";</span><span class="sxs-lookup"><span data-stu-id="1fe1a-205">Set hello destination port range too"27017";</span></span>
* <span data-ttu-id="1fe1a-206">Fare clic su OK e attendere hello toobe di regola di sicurezza creato.</span><span class="sxs-lookup"><span data-stu-id="1fe1a-206">Click OK and wait for hello security rule toobe created.</span></span>

## <a name="iterating-on-hello-todo-application"></a><span data-ttu-id="1fe1a-207">L'iterazione hello applicazione TODO</span><span class="sxs-lookup"><span data-stu-id="1fe1a-207">Iterating on hello TODO application</span></span>
<span data-ttu-id="1fe1a-208">Finora è stato eseguito il provisioning due macchine virtuali Linux: uno che sia in esecuzione dell'applicazione hello front-end web e uno che esegue un'istanza di MongoDB.</span><span class="sxs-lookup"><span data-stu-id="1fe1a-208">So far, we have provisioned two Linux virtual machines: one that is running hello application's web frontend and one that is running a MongoDB instance.</span></span> <span data-ttu-id="1fe1a-209">Ma si è verificato un problema - istanza MongoDB hello il provisioning non è effettivamente usando ancora front-end web hello.</span><span class="sxs-lookup"><span data-stu-id="1fe1a-209">But there is a problem - hello web frontend isn't actually using hello provisioned MongoDB instance yet.</span></span> <span data-ttu-id="1fe1a-210">Errore verrà corretto nei aggiornando hello web front-end codice toouse una variabile di ambiente anziché un'istanza a livello di codice.</span><span class="sxs-lookup"><span data-stu-id="1fe1a-210">Let's fix that by updating hello web frontend code toouse an environment variable instead of a hard-coded instance.</span></span>

### <a name="changing-hello-todo-application"></a><span data-ttu-id="1fe1a-211">La modifica di un'applicazione hello TODO</span><span class="sxs-lookup"><span data-stu-id="1fe1a-211">Changing hello TODO application</span></span>
<span data-ttu-id="1fe1a-212">Nel computer di sviluppo in cui è stato clonato innanzitutto repository nodo todo hello, aprire hello `node-todo/config/database.js` file in un editor qualsiasi e modificare il valore di url hello da valore hardcoded hello come `mongodb://...` troppo`process.env.MONGODB`.</span><span class="sxs-lookup"><span data-stu-id="1fe1a-212">On your development machine where you first cloned hello node-todo repository, open hello `node-todo/config/database.js` file in your favorite editor and change hello url value from hello hard-coded value like `mongodb://...` too`process.env.MONGODB`.</span></span>

<span data-ttu-id="1fe1a-213">Eseguire il commit delle modifiche e push toohello GitHub master:</span><span class="sxs-lookup"><span data-stu-id="1fe1a-213">Commit your changes and push toohello GitHub master:</span></span>

    git commit -am "Get MongoDB instance from env"
    git push origin master

<span data-ttu-id="1fe1a-214">Sfortunatamente, questo non pubblica macchina virtuale di hello modifica toohello web front-end.</span><span class="sxs-lookup"><span data-stu-id="1fe1a-214">Unfortunately, this doesn't publish hello change toohello web frontend virtual machine.</span></span> <span data-ttu-id="1fe1a-215">Verifichiamo alcuni ulteriori modifiche toothat macchina virtuale tooenable un meccanismo semplice ma efficace per la pubblicazione degli aggiornamenti in modo rapido, è possibile osservare effetto di hello di hello modifiche nell'ambiente di produzione hello.</span><span class="sxs-lookup"><span data-stu-id="1fe1a-215">Let's make a few more changes toothat virtual machine tooenable a simple but effective mechanism for publishing updates so you can quickly observe hello effect of hello changes in hello live environment.</span></span>

### <a name="configuring-hello-web-frontend-virtual-machine"></a><span data-ttu-id="1fe1a-216">Configurazione di macchina virtuale di front-end Web hello</span><span class="sxs-lookup"><span data-stu-id="1fe1a-216">Configuring hello Web Frontend Virtual Machine</span></span>
<span data-ttu-id="1fe1a-217">Tenere presente che un clone del repository nodo todo hello bare abbiamo creato in precedenza nella macchina virtuale di hello web front-end.</span><span class="sxs-lookup"><span data-stu-id="1fe1a-217">Recall that we previously created a bare clone of hello node-todo repository on hello web frontend virtual machine.</span></span> <span data-ttu-id="1fe1a-218">Si scopre che verrà creato un nuovo Git modifiche toowhich remoto possono essere inserite.</span><span class="sxs-lookup"><span data-stu-id="1fe1a-218">It turns out that this action created a new Git remote toowhich changes can be pushed.</span></span> <span data-ttu-id="1fe1a-219">Tuttavia, semplicemente push toothis remoto piuttosto non offre modello iterazione rapido hello che gli sviluppatori stanno cercando quando si utilizza il proprio codice.</span><span class="sxs-lookup"><span data-stu-id="1fe1a-219">However, simply pushing toothis remote doesn't quite give hello rapid iteration model that developers are looking for when working on their code.</span></span>

<span data-ttu-id="1fe1a-220">Ciò che si desidera toodo in grado di toobe è garantire che, quando si verifica un repository remoto toohello di push nella macchina virtuale hello, in esecuzione un'applicazione TODO hello viene aggiornata automaticamente.</span><span class="sxs-lookup"><span data-stu-id="1fe1a-220">What we would like toobe able toodo is ensure that when a push toohello remote repository on hello virtual machine occurs, hello running TODO application is automatically updated.</span></span> <span data-ttu-id="1fe1a-221">Fortunatamente, questo è facile tooachieve con git.</span><span class="sxs-lookup"><span data-stu-id="1fe1a-221">Fortunately, this is easy tooachieve with git.</span></span>

<span data-ttu-id="1fe1a-222">GIT espone un numero di hook che vengono chiamati in determinati momenti tooreact tooactions eseguiti sul repository hello.</span><span class="sxs-lookup"><span data-stu-id="1fe1a-222">Git exposes a number of hooks that are called at particular times tooreact tooactions taken on hello repository.</span></span> <span data-ttu-id="1fe1a-223">Tali opzioni vengono specificate utilizzando gli script della shell del repository hello `hooks` cartella.</span><span class="sxs-lookup"><span data-stu-id="1fe1a-223">These are specified using shell scripts in hello repository's `hooks` folder.</span></span> <span data-ttu-id="1fe1a-224">hook di Hello che è più applicabile per uno scenario di aggiornamento automatico di hello è hello `post-update` evento.</span><span class="sxs-lookup"><span data-stu-id="1fe1a-224">hello hook that is most applicable for hello auto-update scenario is hello `post-update` event.</span></span>

<span data-ttu-id="1fe1a-225">In una SSH sessione toohello web front-end macchina virtuale, modificare toohello `~/node-todo.git/hooks` directory e aggiungere i seguenti file di contenuto tooa denominato hello `post-update` (sostituendo `machinename` e `region` con le informazioni della macchina virtuale MongoDB):</span><span class="sxs-lookup"><span data-stu-id="1fe1a-225">In a SSH session toohello web frontend virtual machine, change toohello `~/node-todo.git/hooks` directory and add hello following content tooa file named `post-update` (replacing `machinename` and `region` with your MongoDB virtual machine information):</span></span>

    #!/bin/bash

    forever stopall
    unset 'GIT_DIR'
    export MONGODB="mongodb://machinename.region.cloudapp.azure.com:27017/tododb"
    cd ~/node-todo && git fetch origin && git pull origin master && npm install && forever start ~/node-todo/server.js
    exec git update-server-info

<span data-ttu-id="1fe1a-226">Assicurarsi che il file sia eseguibile eseguendo hello comando seguente:</span><span class="sxs-lookup"><span data-stu-id="1fe1a-226">Ensure this file is executable by running hello following command:</span></span>

    chmod 755 post-update

<span data-ttu-id="1fe1a-227">Questo script assicura che un'applicazione server hello corrente viene arrestata, codice hello nel repository clonato hello sia toohello aggiornata più recente, eventuali dipendenze aggiornate vengono soddisfatte, e hello server viene riavviato.</span><span class="sxs-lookup"><span data-stu-id="1fe1a-227">This script ensures that hello current server application is stopped, hello code in hello cloned repository is updated toohello latest, any updated dependencies are satisfied, and hello server is restarted.</span></span> <span data-ttu-id="1fe1a-228">Garantisce inoltre che tale ambiente hello è stato configurato in preparazione per la ricezione la prima istanza dell'applicazione aggiornamento tooget hello MongoDB dalla variabile di ambiente.</span><span class="sxs-lookup"><span data-stu-id="1fe1a-228">It also ensures that hello environment has been configured in preparation for receiving our first application update tooget hello MongoDB instance from an environment variable.</span></span>

### <a name="configuring-your-development-machine"></a><span data-ttu-id="1fe1a-229">Configurazione del computer di sviluppo</span><span class="sxs-lookup"><span data-stu-id="1fe1a-229">Configuring your Development Machine</span></span>
<span data-ttu-id="1fe1a-230">Ora entriamo nel computer di sviluppo agganciato toohello macchina virtuale del server front-end web.</span><span class="sxs-lookup"><span data-stu-id="1fe1a-230">Now let's get your development machine hooked up toohello web frontend virtual machine.</span></span> <span data-ttu-id="1fe1a-231">Questo è semplice come l'aggiunta di repository bare hello nella macchina virtuale hello come remota.</span><span class="sxs-lookup"><span data-stu-id="1fe1a-231">This is as simple as adding hello bare repository on hello virtual machine as a remote.</span></span> <span data-ttu-id="1fe1a-232">Eseguire l'esempio hello toodo di comando seguente (sostituendo *utente* con il nome di accesso web front-end macchina virtuale e *machinename* e *area* a seconda dei casi):</span><span class="sxs-lookup"><span data-stu-id="1fe1a-232">Run hello following command toodo this (replacing *user* with your web frontend virtual machine login name and *machinename* and *region* as appropriate):</span></span>

    git remote add azure user@machinename.region.cloudapp.azure.com:node-todo.git

<span data-ttu-id="1fe1a-233">Questo è tutto ciò che è necessario tooenable push o attiva la pubblicazione, modifiche di macchina virtuale di toohello web front-end.</span><span class="sxs-lookup"><span data-stu-id="1fe1a-233">This is all that is needed tooenable pushing, or in effect publishing, changes toohello web frontend virtual machine.</span></span>

### <a name="publishing-updates"></a><span data-ttu-id="1fe1a-234">Pubblicazione degli aggiornamenti</span><span class="sxs-lookup"><span data-stu-id="1fe1a-234">Publishing Updates</span></span>
<span data-ttu-id="1fe1a-235">Si pubblica una modifica hello che è stata effettuata fino a questo punto, in modo che un'applicazione hello userà la propria istanza MongoDB:</span><span class="sxs-lookup"><span data-stu-id="1fe1a-235">Let's publish hello one change that has been made so far so that hello application will use our own MongoDB instance:</span></span>

    git push azure master

<span data-ttu-id="1fe1a-236">Dovrebbe essere simile toothis di output:</span><span class="sxs-lookup"><span data-stu-id="1fe1a-236">You should see output similar toothis:</span></span>

    Counting objects: 4, done.
    Delta compression using up too4 threads.
    Compressing objects: 100% (3/3), done.
    Writing objects: 100% (4/4), 406 bytes | 0 bytes/s, done.
    Total 4 (delta 1), reused 0 (delta 0)
    remote: info:    Forever stopped processes:
    remote: data:        uid  command         script    forever pid  id logfile                         uptime
    remote: data:    [0] 0Lyh /usr/bin/nodejs server.js 9064    9301    /home/username/.forever/0Lyh.log 0:0:3:17.487
    remote: From /home/username/node-todo
    remote:    5f31fd7..5bc7be5  master     -> origin/master
    remote: From /home/username/node-todo
    remote:  * branch            master     -> FETCH_HEAD
    remote: Updating 5f31fd7..5bc7be5
    remote: Fast-forward
    remote:  config/database.js | 2 +-
    remote:  1 file changed, 1 insertion(+), 1 deletion(-)
    remote: npm WARN package.json node-todo@0.0.0 No repository field.
    remote: npm WARN package.json node-todo@0.0.0 No license field.
    remote: warn:    --minUptime not set. Defaulting to: 1000ms
    remote: warn:    --spinSleepTime not set. Your script will exit if it does not stay up for at least 1000ms
    remote: info:    Forever processing file: /home/username/node-todo/server.js
    toousername@machinename.region.cloudapp.azure.com:node-todo.git
    5f31fd7..5bc7be5  master -> master

<span data-ttu-id="1fe1a-237">Dopo il completamento del comando, provare ad aggiornare un'applicazione hello in un web browser.</span><span class="sxs-lookup"><span data-stu-id="1fe1a-237">After this command completes, try refreshing hello application in a web browser.</span></span> <span data-ttu-id="1fe1a-238">È necessario essere in grado di toosee che elenco TODO hello presentata in questo documento è vuoto e non è più vincolata toohello condiviso distribuito istanza MongoDB.</span><span class="sxs-lookup"><span data-stu-id="1fe1a-238">You should be able toosee that hello TODO list presented here is empty and no longer tied toohello shared deployed MongoDB instance.</span></span>

<span data-ttu-id="1fe1a-239">esercitazione hello toocomplete verifichiamo modifica di un altro, è più visibile.</span><span class="sxs-lookup"><span data-stu-id="1fe1a-239">toocomplete hello tutorial, let's make another, more visible change.</span></span> <span data-ttu-id="1fe1a-240">Nel computer di sviluppo, aprire il file di node-todo/public/index.html hello usando l'editor preferito.</span><span class="sxs-lookup"><span data-stu-id="1fe1a-240">On your development machine, open hello node-todo/public/index.html file using your favorite editor.</span></span> <span data-ttu-id="1fe1a-241">Individuare l'intestazione jumbotron hello e modificare il titolo di hello da "Sono un Todo-aholic" troppo "sono un aholic Todo in Azure!".</span><span class="sxs-lookup"><span data-stu-id="1fe1a-241">Locate hello jumbotron header and change  hello title from "I'm a Todo-aholic" too"I'm a Todo-aholic on Azure!".</span></span>

<span data-ttu-id="1fe1a-242">A questo punto, eseguire il commit:</span><span class="sxs-lookup"><span data-stu-id="1fe1a-242">Now let's commit:</span></span>

    git commit -am "Azurify hello title"

<span data-ttu-id="1fe1a-243">Questa volta, consente di pubblicare hello modifica tooAzure prima di pubblicarlo come repository di GitHub toohello tooback:</span><span class="sxs-lookup"><span data-stu-id="1fe1a-243">This time, let's publish hello change tooAzure before pushing it tooback toohello GitHub repo:</span></span>

    git push azure master

<span data-ttu-id="1fe1a-244">Dopo il completamento del comando, pagina web hello di aggiornamento per visualizzare le modifiche di hello.</span><span class="sxs-lookup"><span data-stu-id="1fe1a-244">Once this command completes, refresh hello web page and you will see hello changes.</span></span> <span data-ttu-id="1fe1a-245">Perché vengano visualizzate correttamente, push hello modifica toohello indietro origine remota:</span><span class="sxs-lookup"><span data-stu-id="1fe1a-245">Since they look good, push hello change back toohello origin remote:</span></span> 

    git push origin master

## <a name="next-steps"></a><span data-ttu-id="1fe1a-246">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="1fe1a-246">Next Steps</span></span>
<span data-ttu-id="1fe1a-247">In questo articolo è stato illustrato come un'applicazione Node.js tootake e distribuirlo tooLinux le macchine virtuali in esecuzione in Azure.</span><span class="sxs-lookup"><span data-stu-id="1fe1a-247">This article showed how tootake a Node.js application and deploy it tooLinux virtual machines running in Azure.</span></span> <span data-ttu-id="1fe1a-248">toolearn informazioni sulle macchine virtuali Linux in Azure, vedere [tooLinux introduzione in Azure](/documentation/articles/virtual-machines-linux-introduction/).</span><span class="sxs-lookup"><span data-stu-id="1fe1a-248">toolearn more about Linux virtual machines in Azure, see [Introduction tooLinux on Azure](/documentation/articles/virtual-machines-linux-introduction/).</span></span>

<span data-ttu-id="1fe1a-249">Per ulteriori informazioni su come toodevelop delle applicazioni Node.js in Azure, vedere hello [Centro per sviluppatori di Node.js](/develop/nodejs/).</span><span class="sxs-lookup"><span data-stu-id="1fe1a-249">For more information about how toodevelop Node.js applications on Azure, see hello [Node.js Developer Center](/develop/nodejs/).</span></span>


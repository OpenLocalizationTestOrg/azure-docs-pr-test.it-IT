---
title: Distribuire un'applicazione Node.js in macchine virtuali Linux in Azure
description: Informazioni su come distribuire un'applicazione Node.js in macchine virtuali Linux in Azure.
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
ms.openlocfilehash: d3d9fecfafb9ba422420230716b9c985481d1e24
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="deploy-a-nodejs-application-to-linux-virtual-machines-in-azure"></a><span data-ttu-id="f97be-103">Distribuire un'applicazione Node.js in macchine virtuali Linux in Azure</span><span class="sxs-lookup"><span data-stu-id="f97be-103">Deploy a Node.js application to Linux Virtual Machines in Azure</span></span>
<span data-ttu-id="f97be-104">Questa esercitazione illustra come selezionare un'applicazione Node.js e distribuirla in macchine virtuali Linux eseguite in Azure.</span><span class="sxs-lookup"><span data-stu-id="f97be-104">This tutorial shows how to take a Node.js application and deploy it to Linux virtual machines running in Azure.</span></span> <span data-ttu-id="f97be-105">Le istruzioni di questa esercitazione possono essere eseguite in qualsiasi sistema operativo in grado di eseguire Node.js.</span><span class="sxs-lookup"><span data-stu-id="f97be-105">The instructions in this tutorial can be followed on any operating system that is capable of running Node.js.</span></span>

<span data-ttu-id="f97be-106">Si apprenderà come:</span><span class="sxs-lookup"><span data-stu-id="f97be-106">You'll learn how to:</span></span>

* <span data-ttu-id="f97be-107">Eseguire il fork e la clonazione di un repository GitHub contenente una semplice applicazione TODO;</span><span class="sxs-lookup"><span data-stu-id="f97be-107">Fork and clone a GitHub repository containing a simple TODO application;</span></span>
* <span data-ttu-id="f97be-108">Creare e configurare due macchine virtuali Linux in Azure per eseguire l'applicazione;</span><span class="sxs-lookup"><span data-stu-id="f97be-108">Create and configure two Linux virtual machines in Azure to run the application;</span></span>
* <span data-ttu-id="f97be-109">Iterare l'applicazione tramite il push degli aggiornamenti alla macchina virtuale front-end Web.</span><span class="sxs-lookup"><span data-stu-id="f97be-109">Iterate on the application by pushing updates to the web frontend virtual machine.</span></span>

> [!NOTE]
> <span data-ttu-id="f97be-110">Per completare l'esercitazione, sono necessari un account GitHub e un account Microsoft Azure. È inoltre necessario poter usare GIT da un computer di sviluppo.</span><span class="sxs-lookup"><span data-stu-id="f97be-110">To complete this tutorial, you need a GitHub account and a Microsoft Azure account, and the ability to use Git from a development machine.</span></span>
> 
> <span data-ttu-id="f97be-111">Se non si ha un account GitHub, è possibile iscriversi [qui](https://github.com/join).</span><span class="sxs-lookup"><span data-stu-id="f97be-111">If you don't have a GitHub account, you can sign up [here](https://github.com/join).</span></span>
> 
> <span data-ttu-id="f97be-112">Se non si ha un account [Microsoft Azure](https://azure.microsoft.com/), è possibile iscriversi [qui](https://azure.microsoft.com/pricing/free-trial/) per ottenere una versione di prova GRATUITA.</span><span class="sxs-lookup"><span data-stu-id="f97be-112">If you don't have a [Microsoft Azure](https://azure.microsoft.com/) account, you can sign up for a FREE trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span> <span data-ttu-id="f97be-113">Le istruzioni riportate consentiranno di completare il processo di iscrizione per ottenere un [account Microsoft](http://account.microsoft.com) , nel caso in cui non sia già presente.</span><span class="sxs-lookup"><span data-stu-id="f97be-113">This will also lead you through the sign up process for a [Microsoft Account](http://account.microsoft.com) if you do not already have one.</span></span> <span data-ttu-id="f97be-114">In alternativa, se si è eseguita la sottoscrizione a Visual Studio, è possibile [attivare i vantaggi di MSDN](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/?WT.mc_id=A261C142F).</span><span class="sxs-lookup"><span data-stu-id="f97be-114">Alternatively, if you are a Visual Studio subscriber, you can [activate your MSDN benefits](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/?WT.mc_id=A261C142F).</span></span>
> 
> <span data-ttu-id="f97be-115">Se sul computer di sviluppo non è presente GIT e si usa un sistema Macintosh o Windows, è possibile installarlo da [qui](http://www.git-scm.com).</span><span class="sxs-lookup"><span data-stu-id="f97be-115">If you do not have git on your development machine, then if you are using a Macintosh or Windows machine, install git from [here](http://www.git-scm.com).</span></span> <span data-ttu-id="f97be-116">Se si usa Linux, installare GIT mediante il meccanismo più adatto alle proprie esigenze, ad esempio `sudo apt-get install git`.</span><span class="sxs-lookup"><span data-stu-id="f97be-116">If you are using Linux, install git using the mechanism most appropriate for you, such as `sudo apt-get install git`.</span></span>
> 
> 

## <a name="forking-and-cloning-the-todo-application"></a><span data-ttu-id="f97be-117">Fork e clonazione dell'applicazione TODO</span><span class="sxs-lookup"><span data-stu-id="f97be-117">Forking and Cloning the TODO Application</span></span>
<span data-ttu-id="f97be-118">L'applicazione TODO usata in questa esercitazione implementa un semplice front-end Web in un'istanza di MongoDB che tiene traccia di un elenco TODO.</span><span class="sxs-lookup"><span data-stu-id="f97be-118">The TODO application used by this tutorial implements a simple web frontend over a MongoDB instance that keeps track of a TODO list.</span></span> <span data-ttu-id="f97be-119">Dopo l'iscrizione a GitHub, accedere [qui](https://github.com/stepro/node-todo) per trovare l'applicazione ed eseguirne il fork usando il collegamento in alto a destra.</span><span class="sxs-lookup"><span data-stu-id="f97be-119">After signing in to GitHub, go [here](https://github.com/stepro/node-todo) to find the application and fork it using the link in the top right.</span></span> <span data-ttu-id="f97be-120">In questo modo verrà creato un repository nell'account denominato *nomeaccount*/node-todo.</span><span class="sxs-lookup"><span data-stu-id="f97be-120">This should create a repository in your account named *accountname*/node-todo.</span></span>

<span data-ttu-id="f97be-121">A questo punto, clonare il repository nel computer di sviluppo:</span><span class="sxs-lookup"><span data-stu-id="f97be-121">Now on your development machine, clone this repository:</span></span>

    git clone https://github.com/accountname/node-todo.git

<span data-ttu-id="f97be-122">Il clone locale del repository verrà usato in seguito per apportare modifiche al codice sorgente.</span><span class="sxs-lookup"><span data-stu-id="f97be-122">We'll use this local clone of the repository a little later when making changes to the source code.</span></span>

## <a name="creating-and-configuring-the-linux-virtual-machines"></a><span data-ttu-id="f97be-123">Creazione e configurazione di macchine virtuali Linux</span><span class="sxs-lookup"><span data-stu-id="f97be-123">Creating and Configuring the Linux Virtual Machines</span></span>
<span data-ttu-id="f97be-124">Azure supporta il calcolo non elaborato mediante macchine virtuali Linux.</span><span class="sxs-lookup"><span data-stu-id="f97be-124">Azure has great support for raw compute using Linux virtual machines.</span></span> <span data-ttu-id="f97be-125">Questa parte dell'esercitazione illustra come è possibile attivare facilmente due macchine virtuali Linux e distribuire l'applicazione TODO in esse, eseguendo il front-end Web su di una e l'istanza di MongoDB sull'altra.</span><span class="sxs-lookup"><span data-stu-id="f97be-125">This part of the tutorial shows how you can easily spin up two Linux virtual machines and deploy the TODO application to them, running the web frontend on one and the MongoDB instance on the other.</span></span>

### <a name="creating-virtual-machines"></a><span data-ttu-id="f97be-126">Creazione di macchine virtuali</span><span class="sxs-lookup"><span data-stu-id="f97be-126">Creating Virtual Machines</span></span>
<span data-ttu-id="f97be-127">Il modo più semplice per creare una nuova macchina virtuale in Azure è usare il portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="f97be-127">The easiest way to create a new virtual machine in Azure is to use the Azure Portal.</span></span> <span data-ttu-id="f97be-128">Fare clic [qui](https://portal.azure.com) per accedere e avviare il portale di Azure sul Web browser.</span><span class="sxs-lookup"><span data-stu-id="f97be-128">Click [here](https://portal.azure.com) to sign in and launch the Azure Portal in your web browser.</span></span> <span data-ttu-id="f97be-129">Dopo aver caricato il portale di Azure, seguire questa procedura:</span><span class="sxs-lookup"><span data-stu-id="f97be-129">Once the Azure Portal has loaded, complete the following steps:</span></span>

* <span data-ttu-id="f97be-130">Fare clic sul collegamento "+ Nuovo"</span><span class="sxs-lookup"><span data-stu-id="f97be-130">Click the "+ New" link;</span></span>
* <span data-ttu-id="f97be-131">Scegliere la categoria "Calcolo", quindi scegliere "Ubuntu Server 14.04 LTS"</span><span class="sxs-lookup"><span data-stu-id="f97be-131">Pick the "Compute" category and choose "Ubuntu Server 14.04 LTS";</span></span>
* <span data-ttu-id="f97be-132">Selezionare il modello di distribuzione "Gestione risorse" e fare clic su "Crea"</span><span class="sxs-lookup"><span data-stu-id="f97be-132">Select the "Resource Manager" deployment model and click "Create";</span></span>
* <span data-ttu-id="f97be-133">Fornire le informazioni di base attenendosi alle linee guida seguenti:</span><span class="sxs-lookup"><span data-stu-id="f97be-133">Fill in the basics following these guidelines:</span></span>
  * <span data-ttu-id="f97be-134">Specificare un nome facilmente identificabile in un secondo momento</span><span class="sxs-lookup"><span data-stu-id="f97be-134">Specify a name you can easily identify later;</span></span>
  * <span data-ttu-id="f97be-135">Per questa esercitazione, scegliere Autenticazione password</span><span class="sxs-lookup"><span data-stu-id="f97be-135">For this tutorial, choose Password authentication;</span></span>
  * <span data-ttu-id="f97be-136">Creare un nuovo gruppo di risorse con un nome identificabile</span><span class="sxs-lookup"><span data-stu-id="f97be-136">Create a new resource group with an identifiable name.</span></span>
* <span data-ttu-id="f97be-137">Ai fini di questa esercitazione, specificare "A1 Standard" come dimensione della macchina virtuale è una scelta ragionevole</span><span class="sxs-lookup"><span data-stu-id="f97be-137">For the Virtual Machine size, "A1 Standard" is a reasonable choice for this tutorial.</span></span>
* <span data-ttu-id="f97be-138">Per le impostazioni aggiuntive, assicurarsi che il disco sia di tipo "Standard" e accettare tutte le restanti impostazioni predefinite</span><span class="sxs-lookup"><span data-stu-id="f97be-138">For additional settings, ensure the disk type is "Standard" and accept all the remaining defaults.</span></span>
* <span data-ttu-id="f97be-139">Avviare la creazione nella pagina di riepilogo</span><span class="sxs-lookup"><span data-stu-id="f97be-139">Kick off the creation on the summary page.</span></span>

<span data-ttu-id="f97be-140">Eseguire due volte il processo descritto in precedenza per creare due macchine virtuali Linux, una per il front-end Web e l'altra per l'istanza di MongoDB.</span><span class="sxs-lookup"><span data-stu-id="f97be-140">Perform the above process twice to create two Linux virtual machines, one for the web frontend and one for the MongoDB instance.</span></span> <span data-ttu-id="f97be-141">Per la creazione delle macchine virtuali saranno necessari da 5 a 10 minuti.</span><span class="sxs-lookup"><span data-stu-id="f97be-141">Creation of the virtual machines will take about 5-10 minutes.</span></span>

### <a name="assigning-a-dns-entry-for-virtual-machines"></a><span data-ttu-id="f97be-142">Assegnazione di una voce DNS per le macchine virtuali</span><span class="sxs-lookup"><span data-stu-id="f97be-142">Assigning a DNS entry for Virtual Machines</span></span>
<span data-ttu-id="f97be-143">Per impostazione predefinita, è possibile accedere alle macchine virtuali create in Azure solo mediante un indirizzo IP pubblico, ad esempio 1.2.3.4.</span><span class="sxs-lookup"><span data-stu-id="f97be-143">Virtual machines created in Azure are by default only accessible through a public IP address like 1.2.3.4.</span></span> <span data-ttu-id="f97be-144">Di seguito viene indicato come rendere le macchine più facilmente identificabili assegnando loro voci DNS.</span><span class="sxs-lookup"><span data-stu-id="f97be-144">Let's make the machines more easily identifiable by assigning them DNS entries.</span></span>

<span data-ttu-id="f97be-145">Dopo che nel portale è stata confermata la creazione delle macchine virtuali, fare clic sul collegamento "Macchine virtuali" nella barra di spostamento sinistra e individuare le macchine in questione.</span><span class="sxs-lookup"><span data-stu-id="f97be-145">Once the portal indicates that the virtual machines have been created, click on the "Virtual machines" link in the left navbar and locate your machines.</span></span> <span data-ttu-id="f97be-146">Per ogni macchina virtuale:</span><span class="sxs-lookup"><span data-stu-id="f97be-146">For each machine:</span></span>

* <span data-ttu-id="f97be-147">Individuare la scheda Informazioni di base e far clic su Indirizzo IP pubblico;</span><span class="sxs-lookup"><span data-stu-id="f97be-147">Locate the Essentials tab and click on the Public IP Address;</span></span>
* <span data-ttu-id="f97be-148">Nella configurazione dell'indirizzo IP pubblico assegnare un'etichetta di nome DNS e salvare.</span><span class="sxs-lookup"><span data-stu-id="f97be-148">In the public IP address configuration, assign a DNS name label and save.</span></span>

<span data-ttu-id="f97be-149">Il portale garantirà che il nome specificato sia disponibile.</span><span class="sxs-lookup"><span data-stu-id="f97be-149">The portal will ensure that the name you specify is available.</span></span> <span data-ttu-id="f97be-150">Dopo il salvataggio della configurazione, le macchine virtuali avranno nomi host simili a `machinename.region.cloudapp.azure.com`.</span><span class="sxs-lookup"><span data-stu-id="f97be-150">After saving the configuration, your virtual machines will have host names similar to `machinename.region.cloudapp.azure.com`.</span></span>

### <a name="connecting-to-the-virtual-machines"></a><span data-ttu-id="f97be-151">Connessione alle macchine virtuali</span><span class="sxs-lookup"><span data-stu-id="f97be-151">Connecting to the Virtual Machines</span></span>
<span data-ttu-id="f97be-152">Al momento del provisioning, le macchine virtuali sono state preconfigurate per consentire le connessioni remote su SSH.</span><span class="sxs-lookup"><span data-stu-id="f97be-152">When your virtual machines were provisioned, they were pre-configured to allow remote connections over SSH.</span></span> <span data-ttu-id="f97be-153">Si tratta del meccanismo che verrà usato per configurare le macchine virtuali.</span><span class="sxs-lookup"><span data-stu-id="f97be-153">This is the mechanism we will use to configure the virtual machines.</span></span> <span data-ttu-id="f97be-154">Se per la distribuzione si sta usando Windows e non si dispone di un client SSH, è necessario ottenerne uno.</span><span class="sxs-lookup"><span data-stu-id="f97be-154">If you are using Windows for your development, you will need to get an SSH client if you do not already have one.</span></span> <span data-ttu-id="f97be-155">Una soluzione comune è usare PuTTY, scaricabile da [qui](http://www.chiark.greenend.org.uk/~sgtatham/putty/).</span><span class="sxs-lookup"><span data-stu-id="f97be-155">A common choice here is PuTTY, which can be downloaded from [here](http://www.chiark.greenend.org.uk/~sgtatham/putty/).</span></span> <span data-ttu-id="f97be-156">I sistemi operativi Macintosh e Linux vengono forniti con una versione di SSH preinstallata.</span><span class="sxs-lookup"><span data-stu-id="f97be-156">Macintosh and Linux OSes come with a version of SSH pre-installed.</span></span>

### <a name="configuring-the-web-frontend-virtual-machine"></a><span data-ttu-id="f97be-157">Configurazione della macchina virtuale front-end Web</span><span class="sxs-lookup"><span data-stu-id="f97be-157">Configuring the Web Frontend Virtual Machine</span></span>
<span data-ttu-id="f97be-158">Usare SSH per connettersi alla macchina front-end Web creata usando PuTTY, la riga di comando ssh o un altro strumento SSH di propria scelta.</span><span class="sxs-lookup"><span data-stu-id="f97be-158">SSH to the web frontend machine you created using PuTTY, ssh command line or your other favorite SSH tool.</span></span> <span data-ttu-id="f97be-159">Verrà visualizzato un messaggio di benvenuto seguito da un prompt dei comandi:</span><span class="sxs-lookup"><span data-stu-id="f97be-159">You should see a welcome message followed by a command prompt.</span></span>

<span data-ttu-id="f97be-160">Assicurarsi innanzitutto che GIT e il nodo siano entrambi installati:</span><span class="sxs-lookup"><span data-stu-id="f97be-160">First, let's make sure that git and node are both installed:</span></span>

    sudo apt-get install -y git
    curl -sL https://deb.nodesource.com/setup_4.x | sudo -E bash -
    sudo apt-get install -y nodejs

<span data-ttu-id="f97be-161">Poiché il front-end Web dell'applicazione si basa su alcuni moduli Node.js nativi, è necessario installare anche il set essenziale di strumenti di compilazione:</span><span class="sxs-lookup"><span data-stu-id="f97be-161">Since the application's web frontend relies on some native Node.js modules, we also need to install the essential set of build tools:</span></span>

    sudo apt-get install -y build-essential

<span data-ttu-id="f97be-162">Al termine, installare un'applicazione Node.js denominata *forever*, che consentirà di eseguire le applicazioni server Node.js:</span><span class="sxs-lookup"><span data-stu-id="f97be-162">Finally, let's install a Node.js application called *forever*, which helps to run Node.js server applications:</span></span>

    sudo npm install -g forever

<span data-ttu-id="f97be-163">Queste sono tutte le dipendenze che devono essere presenti su questa macchina virtuale per eseguire il front-end Web dell'applicazione.</span><span class="sxs-lookup"><span data-stu-id="f97be-163">These are all the dependencies needed on this virtual machine to be able to run the application's web frontend, so let's get that running.</span></span> <span data-ttu-id="f97be-164">A questo scopo, creare innanzitutto un clone "bare" del repository GitHub precedentemente sottoposto a fork, in modo da poter pubblicare facilmente aggiornamenti nella macchina virtuale (lo scenario di aggiornamento verrà descritto in seguito) e quindi clonare il clone "bare" per fornire una versione del repository effettivamente eseguibile.</span><span class="sxs-lookup"><span data-stu-id="f97be-164">To do this, we will first create a bare clone of the GitHub repository you previously forked so that you can easily publish updates to the virtual machine (we'll cover this update scenario later), and then clone the bare clone to provide a version of the repository that can actually be executed.</span></span>

<span data-ttu-id="f97be-165">Dalla home directory (~) eseguire i comandi seguenti sostituendo *accountname* con il nome dell'account utente GitHub:</span><span class="sxs-lookup"><span data-stu-id="f97be-165">Starting from the home (~) directory, run the following commands (replacing *accountname* with your GitHub user account name):</span></span>

    git clone --bare https://github.com/accountname/node-todo.git
    git clone node-todo.git

<span data-ttu-id="f97be-166">Immettere la directory node-todo ed eseguire i comandi seguenti:</span><span class="sxs-lookup"><span data-stu-id="f97be-166">Now enter the node-todo directory and run these commands:</span></span>

    npm install
    forever start server.js

<span data-ttu-id="f97be-167">Il front-end Web dell'applicazione è ora in esecuzione. Per eccedere all'applicazione da un Web browser è tuttavia necessario eseguire ancora un passaggio.</span><span class="sxs-lookup"><span data-stu-id="f97be-167">The application's web frontend is now running, however there is one more step before you can access the application from a web browser.</span></span> <span data-ttu-id="f97be-168">La macchina virtuale creata è protetta da una risorsa di Azure denominata *gruppo di sicurezza di rete*. Tale risorsa è stata creata al momento del provisioning della macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="f97be-168">The virtual machine you created is protected by an Azure resource called a *network security group*, which was created for you when you provisioned the virtual machine.</span></span> <span data-ttu-id="f97be-169">Attualmente questa risorsa consente soltanto l'indirizzamento alla macchina virtuale delle richieste esterne alla porta 22. Questo permette unicamente la comunicazione di SSH con la macchina.</span><span class="sxs-lookup"><span data-stu-id="f97be-169">Currently, this resource only allows external requests to port 22 to be routed to the virtual machine, which enables SSH communication with the machine but nothing else.</span></span> <span data-ttu-id="f97be-170">Di conseguenza, per visualizzare l'applicazione TODO, configurata per essere eseguita sulla porta 8080, è necessario aprire anche tale porta.</span><span class="sxs-lookup"><span data-stu-id="f97be-170">So in order to view the TODO application, which is configured to run on port 8080, this port also needs to be opened up.</span></span>

<span data-ttu-id="f97be-171">Tornare al portale di Azure e seguire questa procedura:</span><span class="sxs-lookup"><span data-stu-id="f97be-171">Return to the Azure Portal and complete the following steps:</span></span>

* <span data-ttu-id="f97be-172">Fare clic su "Gruppi di risorse" nella barra di spostamento sinistra</span><span class="sxs-lookup"><span data-stu-id="f97be-172">Click on "Resource groups" in the left navbar;</span></span>
* <span data-ttu-id="f97be-173">Selezionare il gruppo di risorse contenente la macchina virtuale</span><span class="sxs-lookup"><span data-stu-id="f97be-173">Select the resource group that contains your virtual machine;</span></span>
* <span data-ttu-id="f97be-174">Dall'elenco di risorse visualizzato selezionare il gruppo di sicurezza di rete (quello contrassegnato dall'icona dello scudo)</span><span class="sxs-lookup"><span data-stu-id="f97be-174">In the resulting list of resources, select the network security group (the one with a shield icon);</span></span>
* <span data-ttu-id="f97be-175">In Proprietà scegliere "Regole di sicurezza in ingresso"</span><span class="sxs-lookup"><span data-stu-id="f97be-175">In the properties, choose "Inbound security rules";</span></span>
* <span data-ttu-id="f97be-176">Nella barra degli strumenti fare clic su "Aggiungi"</span><span class="sxs-lookup"><span data-stu-id="f97be-176">In the toolbar, click "Add";</span></span>
* <span data-ttu-id="f97be-177">Specificare un nome, ad esempio "default-allow-todo"</span><span class="sxs-lookup"><span data-stu-id="f97be-177">Provide a name like "default-allow-todo";</span></span>
* <span data-ttu-id="f97be-178">Impostare il protocollo su "TCP"</span><span class="sxs-lookup"><span data-stu-id="f97be-178">Set the protocol to "TCP";</span></span>
* <span data-ttu-id="f97be-179">Impostare l'intervallo di porte di destinazione su "8080"</span><span class="sxs-lookup"><span data-stu-id="f97be-179">Set the destination port range to "8080";</span></span>
* <span data-ttu-id="f97be-180">Fare clic su OK e attendere che la regola di sicurezza venga creata</span><span class="sxs-lookup"><span data-stu-id="f97be-180">Click OK and wait for the security rule to be created.</span></span>

<span data-ttu-id="f97be-181">Dopo la creazione della regola di sicurezza, l'applicazione TODO è visibile pubblicamente su Internet ed è possibile accedervi usando ad esempio un URL simile al seguente:</span><span class="sxs-lookup"><span data-stu-id="f97be-181">After creating this security rule, the TODO application is publically visible on the internet and you can browse to it, for instance using a URL such as:</span></span>

    http://machinename.region.cloudapp.azure.com:8080

<span data-ttu-id="f97be-182">Si noterà che, anche se la macchina virtuale MongoDB non è ancora stata configurata, l'applicazione TODO rende disponibile un certo numero di funzionalità.</span><span class="sxs-lookup"><span data-stu-id="f97be-182">You will notice that even though we have not yet configured the MongoDB virtual machine, the TODO application appears to be quite functional.</span></span> <span data-ttu-id="f97be-183">Il motivo di questo comportamento è che il repository di origine è hardcoded per l'uso di un'istanza di MongoDB già distribuita.</span><span class="sxs-lookup"><span data-stu-id="f97be-183">This is because the source repository is hardcoded to use a pre-deployed MongoDB instance.</span></span> <span data-ttu-id="f97be-184">Dopo la configurazione della macchina virtuale MongoDB, l'esercitazione prevede la modifica del codice sorgente per consentire l'utilizzo dell'istanza di MongoDB privata.</span><span class="sxs-lookup"><span data-stu-id="f97be-184">Once we have configured the MongoDB virtual machine, we will go back and change the source code to utilize our private MongoDB instance instead.</span></span>

### <a name="configuring-the-mongodb-virtual-machine"></a><span data-ttu-id="f97be-185">Configurazione della macchina virtuale MongoDB</span><span class="sxs-lookup"><span data-stu-id="f97be-185">Configuring the MongoDB Virtual Machine</span></span>
<span data-ttu-id="f97be-186">Usare SSH per connettersi alla seconda macchina virtuale creata usando PuTTY, la riga di comando ssh o un altro strumento SSH di propria scelta.</span><span class="sxs-lookup"><span data-stu-id="f97be-186">SSH to the second machine you created using PuTTY, ssh command line or your other favorite SSH tool.</span></span> <span data-ttu-id="f97be-187">Dopo aver visualizzato il messaggio di benvenuto e il prompt dei comandi, installare MongoDB (le istruzioni sono disponibili [qui](https://docs.mongodb.org/master/tutorial/install-mongodb-on-ubuntu/)):</span><span class="sxs-lookup"><span data-stu-id="f97be-187">After seeing the welcome message and command prompt, install MongoDB (these instructions were taken from [here](https://docs.mongodb.org/master/tutorial/install-mongodb-on-ubuntu/)):</span></span>

    sudo apt-key adv --keyserver hkp://keyserver.ubuntu.com:80 --recv EA312927
    echo "deb http://repo.mongodb.org/apt/ubuntu trusty/mongodb-org/3.2 multiverse" | sudo tee /etc/apt/sources.list.d/mongodb-org-3.2.list
    sudo apt-get update
    sudo apt-get install -y mongodb-org

<span data-ttu-id="f97be-188">Per impostazione predefinita, MongoDB è configurato in modo da essere accessibile solo in locale.</span><span class="sxs-lookup"><span data-stu-id="f97be-188">By default, MongoDB is configured so it can only be accessed locally.</span></span> <span data-ttu-id="f97be-189">Ai fini di questa esercitazione, MongoDB verrà configurato in modo che sia possibile accedervi dalla macchina virtuale dell'applicazione.</span><span class="sxs-lookup"><span data-stu-id="f97be-189">For this tutorial, we will configure MongoDB so it can be accessed from the application's virtual machine.</span></span> <span data-ttu-id="f97be-190">In un contesto sudo aprire il file /etc/mongod.conf e individuare la sezione `# network interfaces` .</span><span class="sxs-lookup"><span data-stu-id="f97be-190">In a sudo context, open the /etc/mongod.conf file and locate the `# network interfaces` section.</span></span> <span data-ttu-id="f97be-191">Modificare il valore di configurazione `net.bindIp` in `0.0.0.0`.</span><span class="sxs-lookup"><span data-stu-id="f97be-191">Change the `net.bindIp` configuration value to `0.0.0.0`.</span></span>

> [!NOTE]
> <span data-ttu-id="f97be-192">Questa configurazione verrà usata solo ai fini di questa esercitazione.</span><span class="sxs-lookup"><span data-stu-id="f97be-192">This configuration is for the purposes of this tutorial only.</span></span> <span data-ttu-id="f97be-193">**NON** è una procedura di sicurezza consigliata e non deve essere usata in ambienti di produzione.</span><span class="sxs-lookup"><span data-stu-id="f97be-193">It is **NOT** a recommended security practice and should not be used in production environments.</span></span>
> 
> 

<span data-ttu-id="f97be-194">Assicurarsi che il servizio MongoDB sia stato avviato:</span><span class="sxs-lookup"><span data-stu-id="f97be-194">Now ensure the MongoDB service has been started:</span></span>

    sudo service mongod restart

<span data-ttu-id="f97be-195">Per impostazione predefinita, MongoDB è attivo sulla porta 27017.</span><span class="sxs-lookup"><span data-stu-id="f97be-195">MongoDB operates over port 27017 by default.</span></span> <span data-ttu-id="f97be-196">Di conseguenza, come è stato necessario aprire la porta 8080 sulla macchina virtuale front-end Web, è ora necessario aprire la porta 27017 sulla macchina virtuale MongoDB.</span><span class="sxs-lookup"><span data-stu-id="f97be-196">So, in the same way that we needed to open port 8080 on the web frontend virtual machine, we need to open port 27017 on the MongoDB virtual machine.</span></span>

<span data-ttu-id="f97be-197">Tornare al portale di Azure e seguire questa procedura:</span><span class="sxs-lookup"><span data-stu-id="f97be-197">Return to the Azure Portal and complete the following steps:</span></span>

* <span data-ttu-id="f97be-198">Fare clic su "Gruppi di risorse" nella barra di spostamento sinistra</span><span class="sxs-lookup"><span data-stu-id="f97be-198">Click on "Resource groups" in the left navbar;</span></span>
* <span data-ttu-id="f97be-199">Selezionare il gruppo di risorse contenente la macchina virtuale MongoDB</span><span class="sxs-lookup"><span data-stu-id="f97be-199">Select the resource group that contains the MongoDB virtual machine;</span></span>
* <span data-ttu-id="f97be-200">Dall'elenco di risorse visualizzato selezionare il gruppo di sicurezza di rete (quello contrassegnato dall'icona dello scudo) denominato come la macchina virtuale MongoDB</span><span class="sxs-lookup"><span data-stu-id="f97be-200">In the resulting list of resources, select the network security group (the one with a shield icon) with the same name that you gave to the MongoDB virtual machine;</span></span>
* <span data-ttu-id="f97be-201">In Proprietà scegliere "Regole di sicurezza in ingresso"</span><span class="sxs-lookup"><span data-stu-id="f97be-201">In the properties, choose "Inbound security rules";</span></span>
* <span data-ttu-id="f97be-202">Nella barra degli strumenti fare clic su "Aggiungi"</span><span class="sxs-lookup"><span data-stu-id="f97be-202">In the toolbar, click "Add";</span></span>
* <span data-ttu-id="f97be-203">Specificare un nome, ad esempio "default-allow-mongo"</span><span class="sxs-lookup"><span data-stu-id="f97be-203">Provide a name like "default-allow-mongo";</span></span>
* <span data-ttu-id="f97be-204">Impostare il protocollo su "TCP"</span><span class="sxs-lookup"><span data-stu-id="f97be-204">Set the protocol to "TCP";</span></span>
* <span data-ttu-id="f97be-205">Impostare l'intervallo di porte di destinazione su "27017"</span><span class="sxs-lookup"><span data-stu-id="f97be-205">Set the destination port range to "27017";</span></span>
* <span data-ttu-id="f97be-206">Fare clic su OK e attendere che la regola di sicurezza venga creata</span><span class="sxs-lookup"><span data-stu-id="f97be-206">Click OK and wait for the security rule to be created.</span></span>

## <a name="iterating-on-the-todo-application"></a><span data-ttu-id="f97be-207">Iterazione dell'applicazione TODO</span><span class="sxs-lookup"><span data-stu-id="f97be-207">Iterating on the TODO application</span></span>
<span data-ttu-id="f97be-208">Nei precedenti passaggi dell'esercitazione è stato eseguito il provisioning di due macchine virtuali Linux: una esegue il front-end Web dell'applicazione, mentre l'altra esegue un'istanza di MongoDB.</span><span class="sxs-lookup"><span data-stu-id="f97be-208">So far, we have provisioned two Linux virtual machines: one that is running the application's web frontend and one that is running a MongoDB instance.</span></span> <span data-ttu-id="f97be-209">Si è tuttavia verificato un problema: il front-end Web non sta ancora effettivamente usando l'istanza di MongoDB sottoposta a provisioning.</span><span class="sxs-lookup"><span data-stu-id="f97be-209">But there is a problem - the web frontend isn't actually using the provisioned MongoDB instance yet.</span></span> <span data-ttu-id="f97be-210">È possibile risolvere il problema aggiornando il codice del front-end Web in modo che usi una variabile di ambiente anziché un'istanza hardcoded.</span><span class="sxs-lookup"><span data-stu-id="f97be-210">Let's fix that by updating the web frontend code to use an environment variable instead of a hard-coded instance.</span></span>

### <a name="changing-the-todo-application"></a><span data-ttu-id="f97be-211">Modifica dell'applicazione TODO</span><span class="sxs-lookup"><span data-stu-id="f97be-211">Changing the TODO application</span></span>
<span data-ttu-id="f97be-212">Nel computer di sviluppo in cui è stato clonato il repository node-todo aprire il file `node-todo/config/database.js` usando l'editor preferito e modificare l'URL da un valore hardcoded come `mongodb://...` in `process.env.MONGODB`.</span><span class="sxs-lookup"><span data-stu-id="f97be-212">On your development machine where you first cloned the node-todo repository, open the `node-todo/config/database.js` file in your favorite editor and change the url value from the hard-coded value like `mongodb://...` to `process.env.MONGODB`.</span></span>

<span data-ttu-id="f97be-213">Eseguire il commit e il push delle modifiche nel master GitHub:</span><span class="sxs-lookup"><span data-stu-id="f97be-213">Commit your changes and push to the GitHub master:</span></span>

    git commit -am "Get MongoDB instance from env"
    git push origin master

<span data-ttu-id="f97be-214">Sfortunatamente, questa operazione non determina la pubblicazione della modifica nella macchina virtuale front-end Web.</span><span class="sxs-lookup"><span data-stu-id="f97be-214">Unfortunately, this doesn't publish the change to the web frontend virtual machine.</span></span> <span data-ttu-id="f97be-215">Nei passaggi successivi verranno apportate altre modifiche alla macchina virtuale per consentire l'attivazione di un meccanismo semplice ma efficace. Tale meccanismo consente di pubblicare gli aggiornamenti in modo che sia possibile osservarne rapidamente gli effetti nell'ambiente di produzione.</span><span class="sxs-lookup"><span data-stu-id="f97be-215">Let's make a few more changes to that virtual machine to enable a simple but effective mechanism for publishing updates so you can quickly observe the effect of the changes in the live environment.</span></span>

### <a name="configuring-the-web-frontend-virtual-machine"></a><span data-ttu-id="f97be-216">Configurazione della macchina virtuale front-end Web</span><span class="sxs-lookup"><span data-stu-id="f97be-216">Configuring the Web Frontend Virtual Machine</span></span>
<span data-ttu-id="f97be-217">Si ricordi che nei passaggi precedenti è stato creato un clone "bare" del repository node-todo sulla macchina virtuale front-end Web.</span><span class="sxs-lookup"><span data-stu-id="f97be-217">Recall that we previously created a bare clone of the node-todo repository on the web frontend virtual machine.</span></span> <span data-ttu-id="f97be-218">Risulta che questa azione abbia creato un nuovo GIT remoto in cui è possibile eseguire il push delle modifiche.</span><span class="sxs-lookup"><span data-stu-id="f97be-218">It turns out that this action created a new Git remote to which changes can be pushed.</span></span> <span data-ttu-id="f97be-219">Tuttavia, il semplice push a questo GIT remoto non fornisce il modello di iterazione rapida richiesto dagli sviluppatori quando scrivono codice.</span><span class="sxs-lookup"><span data-stu-id="f97be-219">However, simply pushing to this remote doesn't quite give the rapid iteration model that developers are looking for when working on their code.</span></span>

<span data-ttu-id="f97be-220">Ciò che si desidera è assicurare che, quando si esegue un push al repository sulla macchina virtuale, l'applicazione TODO in esecuzione venga automaticamente aggiornata.</span><span class="sxs-lookup"><span data-stu-id="f97be-220">What we would like to be able to do is ensure that when a push to the remote repository on the virtual machine occurs, the running TODO application is automatically updated.</span></span> <span data-ttu-id="f97be-221">Fortunatamente, GIT consente di ottenere facilmente questo risultato.</span><span class="sxs-lookup"><span data-stu-id="f97be-221">Fortunately, this is easy to achieve with git.</span></span>

<span data-ttu-id="f97be-222">GIT espone un numero di hook che vengono chiamati in determinati momenti per rispondere alle azioni eseguite sul repository.</span><span class="sxs-lookup"><span data-stu-id="f97be-222">Git exposes a number of hooks that are called at particular times to react to actions taken on the repository.</span></span> <span data-ttu-id="f97be-223">Gli hook vengono specificati usando script della shell nella cartella `hooks` del repository.</span><span class="sxs-lookup"><span data-stu-id="f97be-223">These are specified using shell scripts in the repository's `hooks` folder.</span></span> <span data-ttu-id="f97be-224">L'hook più utilizzabile per lo scenario di aggiornamento automatico è l'evento `post-update` .</span><span class="sxs-lookup"><span data-stu-id="f97be-224">The hook that is most applicable for the auto-update scenario is the `post-update` event.</span></span>

<span data-ttu-id="f97be-225">In una sessione SSH per la connessione alla macchina virtuale front-end Web passare alla directory `~/node-todo.git/hooks` e aggiungere il contenuto seguente al file denominato `post-update` (sostituire `machinename` e `region` con le informazioni della macchina virtuale MongoDB):</span><span class="sxs-lookup"><span data-stu-id="f97be-225">In a SSH session to the web frontend virtual machine, change to the `~/node-todo.git/hooks` directory and add the following content to a file named `post-update` (replacing `machinename` and `region` with your MongoDB virtual machine information):</span></span>

    #!/bin/bash

    forever stopall
    unset 'GIT_DIR'
    export MONGODB="mongodb://machinename.region.cloudapp.azure.com:27017/tododb"
    cd ~/node-todo && git fetch origin && git pull origin master && npm install && forever start ~/node-todo/server.js
    exec git update-server-info

<span data-ttu-id="f97be-226">Verificare che il file sia eseguibile usando il comando seguente:</span><span class="sxs-lookup"><span data-stu-id="f97be-226">Ensure this file is executable by running the following command:</span></span>

    chmod 755 post-update

<span data-ttu-id="f97be-227">Questo script verifica che l'applicazione server corrente venga arrestata, che il codice nel repository clonato venga aggiornato alla versione più recente, che tutte le dipendenze aggiornate vengano soddisfatte e che il server venga riavviato.</span><span class="sxs-lookup"><span data-stu-id="f97be-227">This script ensures that the current server application is stopped, the code in the cloned repository is updated to the latest, any updated dependencies are satisfied, and the server is restarted.</span></span> <span data-ttu-id="f97be-228">Garantisce inoltre che l'ambiente sia stato configurato per il ricevimento del primo aggiornamento dell'applicazione, in modo da ottenere l'istanza di MongoDB da una variabile di ambiente.</span><span class="sxs-lookup"><span data-stu-id="f97be-228">It also ensures that the environment has been configured in preparation for receiving our first application update to get the MongoDB instance from an environment variable.</span></span>

### <a name="configuring-your-development-machine"></a><span data-ttu-id="f97be-229">Configurazione del computer di sviluppo</span><span class="sxs-lookup"><span data-stu-id="f97be-229">Configuring your Development Machine</span></span>
<span data-ttu-id="f97be-230">Di seguito il computer di sviluppo verrà collegato alla macchina virtuale front-end Web.</span><span class="sxs-lookup"><span data-stu-id="f97be-230">Now let's get your development machine hooked up to the web frontend virtual machine.</span></span> <span data-ttu-id="f97be-231">L'operazione è molto semplice ed è analoga all'aggiunta del repository "bare" alla macchina virtuale in remoto.</span><span class="sxs-lookup"><span data-stu-id="f97be-231">This is as simple as adding the bare repository on the virtual machine as a remote.</span></span> <span data-ttu-id="f97be-232">A questo scopo eseguire il comando seguente, sostituendo *user* con il nome di accesso della macchina virtuale front-end Web e *machinename* e *region* con i valori appropriati:</span><span class="sxs-lookup"><span data-stu-id="f97be-232">Run the following command to do this (replacing *user* with your web frontend virtual machine login name and *machinename* and *region* as appropriate):</span></span>

    git remote add azure user@machinename.region.cloudapp.azure.com:node-todo.git

<span data-ttu-id="f97be-233">Queste operazioni sono sufficienti per eseguire il push, o meglio la pubblicazione, delle modifiche nella macchina virtuale front-end Web.</span><span class="sxs-lookup"><span data-stu-id="f97be-233">This is all that is needed to enable pushing, or in effect publishing, changes to the web frontend virtual machine.</span></span>

### <a name="publishing-updates"></a><span data-ttu-id="f97be-234">Pubblicazione degli aggiornamenti</span><span class="sxs-lookup"><span data-stu-id="f97be-234">Publishing Updates</span></span>
<span data-ttu-id="f97be-235">Di seguito verrà pubblicata l'unica modifica apportata finora, in modo che l'applicazione usi l'istanza di MongoDB:</span><span class="sxs-lookup"><span data-stu-id="f97be-235">Let's publish the one change that has been made so far so that the application will use our own MongoDB instance:</span></span>

    git push azure master

<span data-ttu-id="f97be-236">Verrà visualizzato un output simile al seguente:</span><span class="sxs-lookup"><span data-stu-id="f97be-236">You should see output similar to this:</span></span>

    Counting objects: 4, done.
    Delta compression using up to 4 threads.
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
    To username@machinename.region.cloudapp.azure.com:node-todo.git
    5f31fd7..5bc7be5  master -> master

<span data-ttu-id="f97be-237">Dopo l'esecuzione del comando, tentare di aggiornare l'applicazione in un Web browser.</span><span class="sxs-lookup"><span data-stu-id="f97be-237">After this command completes, try refreshing the application in a web browser.</span></span> <span data-ttu-id="f97be-238">Dovrebbe essere possibile vedere che l'elenco TODO qui presentato è vuoto e non più collegato all'istanza di MongoDB distribuita che è stata condivisa.</span><span class="sxs-lookup"><span data-stu-id="f97be-238">You should be able to see that the TODO list presented here is empty and no longer tied to the shared deployed MongoDB instance.</span></span>

<span data-ttu-id="f97be-239">Per completare l'esercitazione, è necessario apportare un'altra modifica più evidente.</span><span class="sxs-lookup"><span data-stu-id="f97be-239">To complete the tutorial, let's make another, more visible change.</span></span> <span data-ttu-id="f97be-240">Nel computer di sviluppo aprire il file node-todo/public/index.html usando l'editor preferito.</span><span class="sxs-lookup"><span data-stu-id="f97be-240">On your development machine, open the node-todo/public/index.html file using your favorite editor.</span></span> <span data-ttu-id="f97be-241">Individuare l'intestazione jumbotron e modificare il titolo da "I'm a Todo-aholic" in "I'm a Todo-aholic on Azure!".</span><span class="sxs-lookup"><span data-stu-id="f97be-241">Locate the jumbotron header and change  the title from "I'm a Todo-aholic" to "I'm a Todo-aholic on Azure!".</span></span>

<span data-ttu-id="f97be-242">A questo punto, eseguire il commit:</span><span class="sxs-lookup"><span data-stu-id="f97be-242">Now let's commit:</span></span>

    git commit -am "Azurify the title"

<span data-ttu-id="f97be-243">Questa volta la modifica verrà pubblicata in Azure prima di eseguirne il push nel repository GitHub:</span><span class="sxs-lookup"><span data-stu-id="f97be-243">This time, let's publish the change to Azure before pushing it to back to the GitHub repo:</span></span>

    git push azure master

<span data-ttu-id="f97be-244">Dopo il completamento del comando, aggiornare la pagina Web per visualizzare le modifiche.</span><span class="sxs-lookup"><span data-stu-id="f97be-244">Once this command completes, refresh the web page and you will see the changes.</span></span> <span data-ttu-id="f97be-245">Poiché appare corretta, eseguire il push della modifica nell'origine remota:</span><span class="sxs-lookup"><span data-stu-id="f97be-245">Since they look good, push the change back to the origin remote:</span></span> 

    git push origin master

## <a name="next-steps"></a><span data-ttu-id="f97be-246">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="f97be-246">Next Steps</span></span>
<span data-ttu-id="f97be-247">Questo articolo ha illustrato come selezionare un'applicazione Node.js e distribuirla in macchine virtuali Linux eseguite in Azure.</span><span class="sxs-lookup"><span data-stu-id="f97be-247">This article showed how to take a Node.js application and deploy it to Linux virtual machines running in Azure.</span></span> <span data-ttu-id="f97be-248">Per altre informazioni sulle macchine virtuali Linux, vedere [Introduzione a Linux in Azure](/documentation/articles/virtual-machines-linux-introduction/).</span><span class="sxs-lookup"><span data-stu-id="f97be-248">To learn more about Linux virtual machines in Azure, see [Introduction to Linux on Azure](/documentation/articles/virtual-machines-linux-introduction/).</span></span>

<span data-ttu-id="f97be-249">Per altre informazioni su come sviluppare applicazioni Node.js in Azure, vedere il [centro per sviluppatori Node.js](/develop/nodejs/).</span><span class="sxs-lookup"><span data-stu-id="f97be-249">For more information about how to develop Node.js applications on Azure, see the [Node.js Developer Center](/develop/nodejs/).</span></span>


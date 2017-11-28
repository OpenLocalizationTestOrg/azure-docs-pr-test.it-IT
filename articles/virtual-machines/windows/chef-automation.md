---
title: distribuzione della macchina virtuale con Chef aaaAzure | Documenti Microsoft
description: Informazioni su come toouse Chef toodo automatizzata la distribuzione delle macchine virtuali e la configurazione in Microsoft Azure
services: virtual-machines-windows
documentationcenter: 
author: diegoviso
manager: timlt
tags: azure-service-management,azure-resource-manager
editor: 
ms.assetid: 0b82ca70-89ed-496d-bb49-c04ae59b4523
ms.service: virtual-machines-windows
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-multiple
ms.devlang: na
ms.topic: article
ms.date: 05/30/2017
ms.author: diviso
ms.openlocfilehash: c5ea98c673b2ee75dd4cedf27e50330af05230d3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="automating-azure-virtual-machine-deployment-with-chef"></a><span data-ttu-id="a9a8d-103">Automazione della distribuzione delle macchine virtuali di Azure con Chef</span><span class="sxs-lookup"><span data-stu-id="a9a8d-103">Automating Azure virtual machine deployment with Chef</span></span>
[!INCLUDE [learn-about-deployment-models](../../../includes/learn-about-deployment-models-both-include.md)]

<span data-ttu-id="a9a8d-104">Chef rappresenta uno strumento molto utile che fornisce soluzioni automatizzate e configurazioni di stato personalizzate.</span><span class="sxs-lookup"><span data-stu-id="a9a8d-104">Chef is a great tool for delivering automation and desired state configurations.</span></span>

<span data-ttu-id="a9a8d-105">Con la versione più recente di cloud api, Chef offre perfetta integrazione con Azure, offrendo hello tooprovision possibilità e distribuire gli stati di configurazione con un unico comando.</span><span class="sxs-lookup"><span data-stu-id="a9a8d-105">With our latest cloud-api release, Chef provides seamless integration with Azure, giving you hello ability tooprovision and deploy configuration states through a single command.</span></span>

<span data-ttu-id="a9a8d-106">In questo articolo verrà illustrato come tooset backup il tooprovision ambiente Chef virtuali di Azure dei computer e vengono illustrati la creazione di un criterio o "Guida di riferimento" e quindi distribuire questo tooan cookbook macchina virtuale di Azure.</span><span class="sxs-lookup"><span data-stu-id="a9a8d-106">In this article, I’ll show you how tooset up your Chef environment tooprovision Azure virtual machines and walk you through creating a policy or “CookBook” and then deploying this cookbook tooan Azure virtual machine.</span></span>

<span data-ttu-id="a9a8d-107">Verranno ora illustrate alcune nozioni di base su Chef.</span><span class="sxs-lookup"><span data-stu-id="a9a8d-107">Let’s begin!</span></span>

## <a name="chef-basics"></a><span data-ttu-id="a9a8d-108">Nozioni di base su Chef</span><span class="sxs-lookup"><span data-stu-id="a9a8d-108">Chef basics</span></span>
<span data-ttu-id="a9a8d-109">Prima di iniziare, è consigliabile che esaminare i concetti di base hello di Chef.</span><span class="sxs-lookup"><span data-stu-id="a9a8d-109">Before you begin, I suggest you review hello basic concepts of Chef.</span></span> <span data-ttu-id="a9a8d-110"><a href="http://www.chef.io/chef" target="_blank">qui</a> è disponibile del materiale che sarebbe opportuno leggere rapidamente prima di tentare di eseguire la procedura.</span><span class="sxs-lookup"><span data-stu-id="a9a8d-110">There is great material <a href="http://www.chef.io/chef" target="_blank">here</a> and I recommend you have a quick read before you attempt this walkthrough.</span></span> <span data-ttu-id="a9a8d-111">Prima di iniziare, verrà tuttavia riepilogo della nozioni di base hello.</span><span class="sxs-lookup"><span data-stu-id="a9a8d-111">I will however recap hello basics before we get started.</span></span>

<span data-ttu-id="a9a8d-112">Hello seguente diagramma viene illustrata l'architettura di Chef di alto livello hello.</span><span class="sxs-lookup"><span data-stu-id="a9a8d-112">hello following diagram depicts hello high-level Chef architecture.</span></span>

![][2]

<span data-ttu-id="a9a8d-113">Chef ha tre componenti principali dell'architettura: Chef Workstation, Chef Server e Chef Client (nodo).</span><span class="sxs-lookup"><span data-stu-id="a9a8d-113">Chef has three main architectural components: Chef Server, Chef Client (node), and Chef Workstation.</span></span>

<span data-ttu-id="a9a8d-114">Hello Chef Server è il punto di gestione e sono disponibili due opzioni per il Chef Server hello: una soluzione ospitata o una soluzione locale.</span><span class="sxs-lookup"><span data-stu-id="a9a8d-114">hello Chef Server is our management point and there are two options for hello Chef Server: a hosted solution or an on-premises solution.</span></span> <span data-ttu-id="a9a8d-115">Si utilizzerà una soluzione in hosting.</span><span class="sxs-lookup"><span data-stu-id="a9a8d-115">We will be using a hosted solution.</span></span>

<span data-ttu-id="a9a8d-116">Client Hello Chef (nodo) è agente hello che si trova nei server hello che si sta gestendo.</span><span class="sxs-lookup"><span data-stu-id="a9a8d-116">hello Chef Client (node) is hello agent that sits on hello servers you are managing.</span></span>

<span data-ttu-id="a9a8d-117">Hello Chef Workstation è la workstation di amministrazione in cui è creare i criteri e si eseguono i comandi di gestione.</span><span class="sxs-lookup"><span data-stu-id="a9a8d-117">hello Chef Workstation is our admin workstation where we create our policies and execute our management commands.</span></span> <span data-ttu-id="a9a8d-118">Esegui hello **knife** comando dalla Chef Workstation toomanage hello l'infrastruttura.</span><span class="sxs-lookup"><span data-stu-id="a9a8d-118">We run hello **knife** command from hello Chef Workstation toomanage our infrastructure.</span></span>

<span data-ttu-id="a9a8d-119">È inoltre disponibile il concetto di hello di "Cookbook" e "Soluzioni".</span><span class="sxs-lookup"><span data-stu-id="a9a8d-119">There is also hello concept of “Cookbooks” and “Recipes”.</span></span> <span data-ttu-id="a9a8d-120">Questi sono effettivamente criteri hello è definire e applicare tooour server.</span><span class="sxs-lookup"><span data-stu-id="a9a8d-120">These are effectively hello policies we define and apply tooour servers.</span></span>

## <a name="preparing-hello-workstation"></a><span data-ttu-id="a9a8d-121">Preparare la workstation hello</span><span class="sxs-lookup"><span data-stu-id="a9a8d-121">Preparing hello workstation</span></span>
<span data-ttu-id="a9a8d-122">In primo luogo, consente di workstation Prepara hello.</span><span class="sxs-lookup"><span data-stu-id="a9a8d-122">First, lets prep hello workstation.</span></span> <span data-ttu-id="a9a8d-123">Nel seguente esempio viene utilizzata una workstation Windows standard.</span><span class="sxs-lookup"><span data-stu-id="a9a8d-123">I’m using a standard Windows workstation.</span></span> <span data-ttu-id="a9a8d-124">È necessario toocreate toostore una directory del file di configurazione e guide.</span><span class="sxs-lookup"><span data-stu-id="a9a8d-124">We need toocreate a directory toostore our config files and cookbooks.</span></span>

<span data-ttu-id="a9a8d-125">Creare innanzitutto una directory denominata C:\chef.</span><span class="sxs-lookup"><span data-stu-id="a9a8d-125">First create a directory called C:\chef.</span></span>

<span data-ttu-id="a9a8d-126">Creare quindi una seconda directory denominata c:\chef\cookbooks.</span><span class="sxs-lookup"><span data-stu-id="a9a8d-126">Then create a second directory called c:\chef\cookbooks.</span></span>

<span data-ttu-id="a9a8d-127">È ora necessario toodownload il file di impostazioni di Azure affinché Chef possa comunicare con la sottoscrizione di Azure.</span><span class="sxs-lookup"><span data-stu-id="a9a8d-127">We now need toodownload our Azure settings file so Chef can communicate with our Azure subscription.</span></span>

<!--Download your publish settings from [here](https://manage.windowsazure.com/publishsettings/).-->
<span data-ttu-id="a9a8d-128">Scaricare il hello PowerShell Azure utilizzando impostazioni di pubblicazione [Get-AzurePublishSettingsFile](https://docs.microsoft.com/en-us/powershell/module/azure/get-azurepublishsettingsfile?view=azuresmps-4.0.0) comando.</span><span class="sxs-lookup"><span data-stu-id="a9a8d-128">Download your publish settings using hello PowerShell Azure [Get-AzurePublishSettingsFile](https://docs.microsoft.com/en-us/powershell/module/azure/get-azurepublishsettingsfile?view=azuresmps-4.0.0) command.</span></span> 

<span data-ttu-id="a9a8d-129">Salvare hello di file di impostazioni di pubblicazione in C:\chef.</span><span class="sxs-lookup"><span data-stu-id="a9a8d-129">Save hello publish settings file in C:\chef.</span></span>

## <a name="creating-a-managed-chef-account"></a><span data-ttu-id="a9a8d-130">Creazione di un account Chef gestito</span><span class="sxs-lookup"><span data-stu-id="a9a8d-130">Creating a managed Chef account</span></span>
<span data-ttu-id="a9a8d-131">Iscriversi per ottenere un account Chef ospitato [qui](https://manage.chef.io/signup)</span><span class="sxs-lookup"><span data-stu-id="a9a8d-131">Sign up for a hosted Chef account [here](https://manage.chef.io/signup).</span></span>

<span data-ttu-id="a9a8d-132">Durante il processo di iscrizione hello, sarà richiesto toocreate una nuova organizzazione.</span><span class="sxs-lookup"><span data-stu-id="a9a8d-132">During hello signup process, you will be asked toocreate a new organization.</span></span>

![][3]

<span data-ttu-id="a9a8d-133">Una volta creata l'organizzazione, è possibile scaricare hello starter kit.</span><span class="sxs-lookup"><span data-stu-id="a9a8d-133">Once your organization is created, download hello starter kit.</span></span>

![][4]

> [!NOTE]
> <span data-ttu-id="a9a8d-134">Se viene visualizzato un messaggio che informa che le chiavi verranno reimpostate, si tratta tooproceed ok è non disponibile alcuna infrastruttura esistente come ancora configurato.</span><span class="sxs-lookup"><span data-stu-id="a9a8d-134">If you receive a prompt warning you that your keys will be reset, it’s ok tooproceed as we have no existing infrastructure configured as yet.</span></span>
> 
> 

<span data-ttu-id="a9a8d-135">Il file ZIP dello Starter Kit contiene i file di configurazione e le chiavi dell'organizzazione.</span><span class="sxs-lookup"><span data-stu-id="a9a8d-135">This starter kit zip file contains your organization config files and keys.</span></span>

## <a name="configuring-hello-chef-workstation"></a><span data-ttu-id="a9a8d-136">Configurazione della workstation Chef hello</span><span class="sxs-lookup"><span data-stu-id="a9a8d-136">Configuring hello Chef workstation</span></span>
<span data-ttu-id="a9a8d-137">Estrarre il contenuto di hello di hello chef starter.zip tooC:\chef.</span><span class="sxs-lookup"><span data-stu-id="a9a8d-137">Extract hello content of hello chef-starter.zip tooC:\chef.</span></span>

<span data-ttu-id="a9a8d-138">Copiare tutti i file in starter\chef-chef-repo\.chef tooyour c:\chef directory.</span><span class="sxs-lookup"><span data-stu-id="a9a8d-138">Copy all files under chef-starter\chef-repo\.chef tooyour c:\chef directory.</span></span>

<span data-ttu-id="a9a8d-139">La directory dovrebbe essere simile al seguente hello di esempio seguente.</span><span class="sxs-lookup"><span data-stu-id="a9a8d-139">Your directory should now look something like hello following example.</span></span>

![][5]

<span data-ttu-id="a9a8d-140">È ora incluso un file di pubblicazione Azure hello radice hello c:\chef quattro file di.</span><span class="sxs-lookup"><span data-stu-id="a9a8d-140">You should now have four files including hello Azure publishing file in hello root of c:\chef.</span></span>

<span data-ttu-id="a9a8d-141">file PEM Hello contengono l'organizzazione e le chiavi private di amministratore per la comunicazione, mentre file knife hello contiene la configurazione efficace.</span><span class="sxs-lookup"><span data-stu-id="a9a8d-141">hello PEM files contain your organization and admin private keys for communication while hello knife.rb file contains your knife configuration.</span></span> <span data-ttu-id="a9a8d-142">È necessario tooedit hello knife file.</span><span class="sxs-lookup"><span data-stu-id="a9a8d-142">We will need tooedit hello knife.rb file.</span></span>

<span data-ttu-id="a9a8d-143">Aprire il file hello nell'editor preferito e modificare cookbook_path"hello" rimuovendo hello /... / dal percorso di hello viene visualizzato come indicato di seguito.</span><span class="sxs-lookup"><span data-stu-id="a9a8d-143">Open hello file in your editor of choice and modify hello “cookbook_path” by removing hello /../ from hello path so it appears as shown next.</span></span>

    cookbook_path  ["#{current_dir}/cookbooks"]

<span data-ttu-id="a9a8d-144">Aggiungere inoltre riflettente hello nome di Azure nelle righe seguenti hello file di impostazioni di pubblicazione.</span><span class="sxs-lookup"><span data-stu-id="a9a8d-144">Also add hello following line reflecting hello name of your Azure publish settings file.</span></span>

    knife[:azure_publish_settings_file] = "yourfilename.publishsettings"

<span data-ttu-id="a9a8d-145">Il file knife dovrebbe apparire simile toohello esempio seguente.</span><span class="sxs-lookup"><span data-stu-id="a9a8d-145">Your knife.rb file should now look similar toohello following example.</span></span>

![][6]

<span data-ttu-id="a9a8d-146">Queste righe garantisce che fa riferimento a directory Cookbook hello in c:\chef\cookbooks Knife e Usa anche il file di impostazioni di pubblicazione Azure durante le operazioni di Azure.</span><span class="sxs-lookup"><span data-stu-id="a9a8d-146">These lines will ensure that Knife references hello cookbooks directory under c:\chef\cookbooks, and also uses our Azure Publish Settings file during Azure operations.</span></span>

## <a name="installing-hello-chef-development-kit"></a><span data-ttu-id="a9a8d-147">L'installazione di hello Chef Development Kit</span><span class="sxs-lookup"><span data-stu-id="a9a8d-147">Installing hello Chef Development Kit</span></span>
<span data-ttu-id="a9a8d-148">Avanti [scaricare e installare](http://downloads.getchef.com/chef-dk/windows) hello tooset ChefDK (Chef Development Kit) di Chef Workstation.</span><span class="sxs-lookup"><span data-stu-id="a9a8d-148">Next [download and install](http://downloads.getchef.com/chef-dk/windows) hello ChefDK (Chef Development Kit) tooset up your Chef Workstation.</span></span>

![][7]

<span data-ttu-id="a9a8d-149">Installare nel percorso predefinito di hello di c:\opscode.</span><span class="sxs-lookup"><span data-stu-id="a9a8d-149">Install in hello default location of c:\opscode.</span></span> <span data-ttu-id="a9a8d-150">L'installazione richiederà all'incirca 10 minuti.</span><span class="sxs-lookup"><span data-stu-id="a9a8d-150">This install will take around 10 minutes.</span></span>

<span data-ttu-id="a9a8d-151">Verificare che la variabile PATH contenga voci relative ai percorsi C:\opscode\chefdk\bin;C:\opscode\chefdk\embedded\bin;c:\users\yourusername\.chefdk\gem\ruby\2.0.0\bin</span><span class="sxs-lookup"><span data-stu-id="a9a8d-151">Confirm your PATH variable contains entries for C:\opscode\chefdk\bin;C:\opscode\chefdk\embedded\bin;c:\users\yourusername\.chefdk\gem\ruby\2.0.0\bin</span></span>

<span data-ttu-id="a9a8d-152">Se questi percorsi non sono presenti, assicurarsi di aggiungerli.</span><span class="sxs-lookup"><span data-stu-id="a9a8d-152">If they are not there, make sure you add these paths!</span></span>

<span data-ttu-id="a9a8d-153">*Nota hello ordine di hello percorso è importante!*</span><span class="sxs-lookup"><span data-stu-id="a9a8d-153">*NOTE hello ORDER OF hello PATH IS IMPORTANT!*</span></span> <span data-ttu-id="a9a8d-154">Se i percorsi opscode non sono nell'ordine corretto hello è problemi.</span><span class="sxs-lookup"><span data-stu-id="a9a8d-154">If your opscode paths are not in hello correct order you will have issues.</span></span>

<span data-ttu-id="a9a8d-155">Prima di continuare, riavviare la workstation.</span><span class="sxs-lookup"><span data-stu-id="a9a8d-155">Reboot your workstation before you continue.</span></span>

<span data-ttu-id="a9a8d-156">Successivamente, verrà installato estensione Knife Azure hello.</span><span class="sxs-lookup"><span data-stu-id="a9a8d-156">Next, we will install hello Knife Azure extension.</span></span> <span data-ttu-id="a9a8d-157">In questo modo Knife hello "Plug-in Azure".</span><span class="sxs-lookup"><span data-stu-id="a9a8d-157">This provides Knife with hello “Azure Plugin”.</span></span>

<span data-ttu-id="a9a8d-158">Eseguire hello comando seguente.</span><span class="sxs-lookup"><span data-stu-id="a9a8d-158">Run hello following command.</span></span>

    chef gem install knife-azure ––pre

> [!NOTE]
> <span data-ttu-id="a9a8d-159">argomento di pre-Hello garantisce che si ricevono più recente versione RC di hello di hello Knife Azure plug-in che offre accesso toohello più recente di API.</span><span class="sxs-lookup"><span data-stu-id="a9a8d-159">hello –pre argument ensures you are receiving hello latest RC version of hello Knife Azure Plugin which provides access toohello latest set of APIs.</span></span>
> 
> 

<span data-ttu-id="a9a8d-160">È probabile che un numero di dipendenze verrà installato anche in hello contemporaneamente.</span><span class="sxs-lookup"><span data-stu-id="a9a8d-160">It’s likely that a number of dependencies will also be installed at hello same time.</span></span>

![][8]

<span data-ttu-id="a9a8d-161">tooensure che tutto è configurato correttamente, hello esecuzione comando seguente.</span><span class="sxs-lookup"><span data-stu-id="a9a8d-161">tooensure everything is configured correctly, run hello following command.</span></span>

    knife azure image list

<span data-ttu-id="a9a8d-162">Se tutto è stato configurato correttamente, verrà visualizzato un elenco delle immagini di Azure disponibili.</span><span class="sxs-lookup"><span data-stu-id="a9a8d-162">If everything is configured correctly, you will see a list of available Azure images scroll through.</span></span>

<span data-ttu-id="a9a8d-163">A questo punto</span><span class="sxs-lookup"><span data-stu-id="a9a8d-163">Congratulations.</span></span> <span data-ttu-id="a9a8d-164">impostazione di workstation Hello!</span><span class="sxs-lookup"><span data-stu-id="a9a8d-164">hello workstation is set up!</span></span>

## <a name="creating-a-cookbook"></a><span data-ttu-id="a9a8d-165">Creazione di un cookbook</span><span class="sxs-lookup"><span data-stu-id="a9a8d-165">Creating a Cookbook</span></span>
<span data-ttu-id="a9a8d-166">Viene utilizzato un Cookbook da Chef toodefine un set di comandi che si desidera tooexecute nel client gestito.</span><span class="sxs-lookup"><span data-stu-id="a9a8d-166">A Cookbook is used by Chef toodefine a set of commands that you wish tooexecute on your managed client.</span></span> <span data-ttu-id="a9a8d-167">Creare un Cookbook è semplice e utilizziamo hello **chef generare cookbook** comando toogenerate il nostro modello Cookbook.</span><span class="sxs-lookup"><span data-stu-id="a9a8d-167">Creating a Cookbook is straightforward and we use hello **chef generate cookbook** command toogenerate our Cookbook template.</span></span> <span data-ttu-id="a9a8d-168">In questo esempio il cookbook verrà denominato webserver, in quanto si desidera creare un criterio che distribuisca automaticamente IIS.</span><span class="sxs-lookup"><span data-stu-id="a9a8d-168">I will be calling my Cookbook web server as I would like a policy that automatically deploys IIS.</span></span>

<span data-ttu-id="a9a8d-169">Nella directory di C:\Chef eseguire hello comando seguente.</span><span class="sxs-lookup"><span data-stu-id="a9a8d-169">Under your C:\Chef directory run hello following command.</span></span>

    chef generate cookbook webserver

<span data-ttu-id="a9a8d-170">Verrà generato un set di file nella directory hello C:\Chef\cookbooks\webserver.</span><span class="sxs-lookup"><span data-stu-id="a9a8d-170">This will generate a set of files under hello directory C:\Chef\cookbooks\webserver.</span></span> <span data-ttu-id="a9a8d-171">È ora necessario set hello toodefine di comandi che desideriamo nostri tooexecute client Chef nella macchina virtuale gestita.</span><span class="sxs-lookup"><span data-stu-id="a9a8d-171">We now need toodefine hello set of commands we would like our Chef client tooexecute on our managed virtual machine.</span></span>

<span data-ttu-id="a9a8d-172">i comandi di Hello vengono archiviati in RB file hello.</span><span class="sxs-lookup"><span data-stu-id="a9a8d-172">hello commands are stored in hello file default.rb.</span></span> <span data-ttu-id="a9a8d-173">In questo file, sarà verranno definiti un set di comandi che viene installato IIS, IIS avvia e copia di una cartella wwwroot del modello file toohello.</span><span class="sxs-lookup"><span data-stu-id="a9a8d-173">In this file, I’ll be defining a set of commands that installs IIS, starts IIS and copies a template file toohello wwwroot folder.</span></span>

<span data-ttu-id="a9a8d-174">Modificare il file di C:\chef\cookbooks\webserver\recipes\default.rb hello e aggiungere hello seguenti righe.</span><span class="sxs-lookup"><span data-stu-id="a9a8d-174">Modify hello C:\chef\cookbooks\webserver\recipes\default.rb file and add hello following lines.</span></span>

    powershell_script 'Install IIS' do
         action :run
         code 'add-windowsfeature Web-Server'
    end

    service 'w3svc' do
         action [ :enable, :start ]
    end

    template 'c:\inetpub\wwwroot\Default.htm' do
         source 'Default.htm.erb'
         rights :read, 'Everyone'
    end

<span data-ttu-id="a9a8d-175">Dopo aver terminato, salvare file hello.</span><span class="sxs-lookup"><span data-stu-id="a9a8d-175">Save hello file once you are done.</span></span>

## <a name="creating-a-template"></a><span data-ttu-id="a9a8d-176">Creazione di un modello</span><span class="sxs-lookup"><span data-stu-id="a9a8d-176">Creating a template</span></span>
<span data-ttu-id="a9a8d-177">Come accennato in precedenza, è necessario un file di modello che verrà utilizzato come la pagina default.html toogenerate.</span><span class="sxs-lookup"><span data-stu-id="a9a8d-177">As we mentioned previously, we need toogenerate a template file which will be used as our default.html page.</span></span>

<span data-ttu-id="a9a8d-178">Eseguire hello seguente modello di comando toogenerate hello.</span><span class="sxs-lookup"><span data-stu-id="a9a8d-178">Run hello following command toogenerate hello template.</span></span>

    chef generate template webserver Default.htm

<span data-ttu-id="a9a8d-179">Passare ora toohello C:\chef\cookbooks\webserver\templates\default\Default.htm.erb file.</span><span class="sxs-lookup"><span data-stu-id="a9a8d-179">Now navigate toohello C:\chef\cookbooks\webserver\templates\default\Default.htm.erb file.</span></span> <span data-ttu-id="a9a8d-180">Modificare il file hello aggiungendo codice semplice "Hello World" HTML e quindi salvare il file hello.</span><span class="sxs-lookup"><span data-stu-id="a9a8d-180">Edit hello file by adding some simple “Hello World” HTML code, and then save hello file.</span></span>

## <a name="upload-hello-cookbook-toohello-chef-server"></a><span data-ttu-id="a9a8d-181">Caricare hello Cookbook toohello Chef Server</span><span class="sxs-lookup"><span data-stu-id="a9a8d-181">Upload hello Cookbook toohello Chef Server</span></span>
<span data-ttu-id="a9a8d-182">In questo passaggio, stiamo richiede una copia di hello Cookbook che abbiamo creato il computer locale e caricarlo toohello Chef Server ospitato.</span><span class="sxs-lookup"><span data-stu-id="a9a8d-182">In this step, we are taking a copy of hello Cookbook that we have created on our local machine and uploading it toohello Chef Hosted Server.</span></span> <span data-ttu-id="a9a8d-183">Una volta caricato, hello Cookbook verrà visualizzato in hello **criteri** scheda.</span><span class="sxs-lookup"><span data-stu-id="a9a8d-183">Once uploaded, hello Cookbook will appear under hello **Policy** tab.</span></span>

    knife cookbook upload webserver

![][9]

## <a name="deploy-a-virtual-machine-with-knife-azure"></a><span data-ttu-id="a9a8d-184">Distribuzione di una macchina virtuale con il comando Knife Azure</span><span class="sxs-lookup"><span data-stu-id="a9a8d-184">Deploy a virtual machine with Knife Azure</span></span>
<span data-ttu-id="a9a8d-185">Verrà ora distribuire una macchina virtuale di Azure e applicare hello Cookbook "Server Web" che consente di installare IIS web predefinito e servizio web page.</span><span class="sxs-lookup"><span data-stu-id="a9a8d-185">We will now deploy an Azure virtual machine and apply hello “Webserver” Cookbook which will install our IIS web service and default web page.</span></span>

<span data-ttu-id="a9a8d-186">In ordine toodo questo, utilizzare hello **server knife azure creare** comando.</span><span class="sxs-lookup"><span data-stu-id="a9a8d-186">In order toodo this, use hello **knife azure server create** command.</span></span>

<span data-ttu-id="a9a8d-187">Sto comando hello visualizzata del successivo.</span><span class="sxs-lookup"><span data-stu-id="a9a8d-187">Am example of hello command appears next.</span></span>

    knife azure server create --azure-dns-name 'diegotest01' --azure-vm-name 'testserver01' --azure-vm-size 'Small' --azure-storage-account 'portalvhdsxxxx' --bootstrap-protocol 'cloud-api' --azure-source-image 'a699494373c04fc0bc8f2bb1389d6106__Windows-Server-2012-Datacenter-201411.01-en.us-127GB.vhd' --azure-service-location 'Southeast Asia' --winrm-user azureuser --winrm-password 'myPassword123' --tcp-endpoints 80,3389 --r 'recipe[webserver]'

<span data-ttu-id="a9a8d-188">i parametri di Hello sono di chiara interpretazione.</span><span class="sxs-lookup"><span data-stu-id="a9a8d-188">hello parameters are self-explanatory.</span></span> <span data-ttu-id="a9a8d-189">Sostituire le variabili desiderate ed eseguire il comando.</span><span class="sxs-lookup"><span data-stu-id="a9a8d-189">Substitute your particular variables and run.</span></span>

> [!NOTE]
> <span data-ttu-id="a9a8d-190">Tramite riga di comando hello hello, sono automazione anche le regole di filtro dell'endpoint rete utilizzando il parametro – tcp endpoint hello.</span><span class="sxs-lookup"><span data-stu-id="a9a8d-190">Through hello hello command line, I’m also automating my endpoint network filter rules by using hello –tcp-endpoints parameter.</span></span> <span data-ttu-id="a9a8d-191">Dopo avere aperto le porte 80 e 3389 tooprovide toomy web pagina di accesso sessione RDP.</span><span class="sxs-lookup"><span data-stu-id="a9a8d-191">I’ve opened up ports 80 and 3389 tooprovide access toomy web page and RDP session.</span></span>
> 
> 

<span data-ttu-id="a9a8d-192">Dopo aver eseguito il comando hello, passare toohello Azure portal per visualizzare il computer iniziare tooprovision.</span><span class="sxs-lookup"><span data-stu-id="a9a8d-192">Once you run hello command, go toohello Azure portal and you will see your machine begin tooprovision.</span></span>

![][13]

<span data-ttu-id="a9a8d-193">prompt dei comandi di Hello viene visualizzato accanto.</span><span class="sxs-lookup"><span data-stu-id="a9a8d-193">hello command prompt appears next.</span></span>

![][10]

<span data-ttu-id="a9a8d-194">Una volta completata la distribuzione di hello, si dovrebbe essere servizio web di toohello tooconnect in grado di sulla porta 80 è fosse stata aperta la porta hello quando è stato eseguito il provisioning hello di macchina virtuale con il comando Knife Azure hello.</span><span class="sxs-lookup"><span data-stu-id="a9a8d-194">Once hello deployment is complete, we should be able tooconnect toohello web service over port 80 as we had opened hello port when we provisioned hello virtual machine with hello Knife Azure command.</span></span> <span data-ttu-id="a9a8d-195">Questa macchina virtuale è hello macchina virtuale solo il servizio cloud, sarà la connessione con l'url del servizio cloud hello.</span><span class="sxs-lookup"><span data-stu-id="a9a8d-195">As this virtual machine is hello only virtual machine in my cloud service, I’ll connect it with hello cloud service url.</span></span>

![][11]

<span data-ttu-id="a9a8d-196">In questo esempio è stata impiegata una certa dose di creatività nell'uso del codice HTML.</span><span class="sxs-lookup"><span data-stu-id="a9a8d-196">As you can see, I got creative with my HTML code.</span></span>

<span data-ttu-id="a9a8d-197">Non dimenticare che è anche possibile connettersi tramite una sessione RDP dal portale di Azure tramite la porta 3389 hello.</span><span class="sxs-lookup"><span data-stu-id="a9a8d-197">Don’t forget we can also connect through an RDP session from hello Azure portal via port 3389.</span></span>

<span data-ttu-id="a9a8d-198">Si spera che questa guida sia stata utile.</span><span class="sxs-lookup"><span data-stu-id="a9a8d-198">I hope this has been helpful!</span></span> <span data-ttu-id="a9a8d-199">Ora è possibile avviare l'infrastruttura come percorso di codice con Azure.</span><span class="sxs-lookup"><span data-stu-id="a9a8d-199">Go  and start your infrastructure as code journey with Azure today!</span></span>

<!--Image references-->
[2]: media/chef-automation/2.png
[3]: media/chef-automation/3.png
[4]: media/chef-automation/4.png
[5]: media/chef-automation/5.png
[6]: media/chef-automation/6.png
[7]: media/chef-automation/7.png
[8]: media/chef-automation/8.png
[9]: media/chef-automation/9.png
[10]: media/chef-automation/10.png
[11]: media/chef-automation/11.png
[13]: media/chef-automation/13.png


<!--Link references-->

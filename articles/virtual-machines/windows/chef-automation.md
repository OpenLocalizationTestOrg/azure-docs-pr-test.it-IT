---
title: Distribuzione delle macchine virtuali di Azure con Chef | Microsoft Docs
description: Imparare a utilizzare Chef per effettuare la distribuzione automatizzata della macchina virtuale e la configurazione in Microsoft Azure
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
ms.openlocfilehash: b6db0fbb4e0de896994954974ddcc39daad9c125
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="automating-azure-virtual-machine-deployment-with-chef"></a><span data-ttu-id="a5666-103">Automazione della distribuzione delle macchine virtuali di Azure con Chef</span><span class="sxs-lookup"><span data-stu-id="a5666-103">Automating Azure virtual machine deployment with Chef</span></span>
[!INCLUDE [learn-about-deployment-models](../../../includes/learn-about-deployment-models-both-include.md)]

<span data-ttu-id="a5666-104">Chef rappresenta uno strumento molto utile che fornisce soluzioni automatizzate e configurazioni di stato personalizzate.</span><span class="sxs-lookup"><span data-stu-id="a5666-104">Chef is a great tool for delivering automation and desired state configurations.</span></span>

<span data-ttu-id="a5666-105">Con il rilascio della più recente API cloud, Chef fornisce una perfetta integrazione con Azure, offrendo la possibilità di eseguire il provisioning e distribuire le configurazioni di stato attraverso un unico comando.</span><span class="sxs-lookup"><span data-stu-id="a5666-105">With our latest cloud-api release, Chef provides seamless integration with Azure, giving you the ability to provision and deploy configuration states through a single command.</span></span>

<span data-ttu-id="a5666-106">Questo articolo illustra come configurare l'ambiente Chef per il provisioning di macchine virtuali di Azure e descrive i passaggi per creare un criterio o "CookBook" e successivamente distribuire tale cookbook in una macchina virtuale di Azure.</span><span class="sxs-lookup"><span data-stu-id="a5666-106">In this article, I’ll show you how to set up your Chef environment to provision Azure virtual machines and walk you through creating a policy or “CookBook” and then deploying this cookbook to an Azure virtual machine.</span></span>

<span data-ttu-id="a5666-107">Verranno ora illustrate alcune nozioni di base su Chef.</span><span class="sxs-lookup"><span data-stu-id="a5666-107">Let’s begin!</span></span>

## <a name="chef-basics"></a><span data-ttu-id="a5666-108">Nozioni di base su Chef</span><span class="sxs-lookup"><span data-stu-id="a5666-108">Chef basics</span></span>
<span data-ttu-id="a5666-109">Prima di iniziare, si consiglia di acquisire familiarità con i concetti di base di Chef.</span><span class="sxs-lookup"><span data-stu-id="a5666-109">Before you begin, I suggest you review the basic concepts of Chef.</span></span> <span data-ttu-id="a5666-110"><a href="http://www.chef.io/chef" target="_blank">qui</a> è disponibile del materiale che sarebbe opportuno leggere rapidamente prima di tentare di eseguire la procedura.</span><span class="sxs-lookup"><span data-stu-id="a5666-110">There is great material <a href="http://www.chef.io/chef" target="_blank">here</a> and I recommend you have a quick read before you attempt this walkthrough.</span></span> <span data-ttu-id="a5666-111">Di seguito viene comunque presentato un riassunto delle nozioni di base su Chef.</span><span class="sxs-lookup"><span data-stu-id="a5666-111">I will however recap the basics before we get started.</span></span>

<span data-ttu-id="a5666-112">Il seguente diagramma illustra l'architettura di alto livello di Chef.</span><span class="sxs-lookup"><span data-stu-id="a5666-112">The following diagram depicts the high-level Chef architecture.</span></span>

![][2]

<span data-ttu-id="a5666-113">Chef ha tre componenti principali dell'architettura: Chef Workstation, Chef Server e Chef Client (nodo).</span><span class="sxs-lookup"><span data-stu-id="a5666-113">Chef has three main architectural components: Chef Server, Chef Client (node), and Chef Workstation.</span></span>

<span data-ttu-id="a5666-114">Il server Chef rappresenta il punto di gestione e per esso sono disponibili due opzioni: una soluzione in hosting e una soluzione in locale.</span><span class="sxs-lookup"><span data-stu-id="a5666-114">The Chef Server is our management point and there are two options for the Chef Server: a hosted solution or an on-premises solution.</span></span> <span data-ttu-id="a5666-115">Si utilizzerà una soluzione in hosting.</span><span class="sxs-lookup"><span data-stu-id="a5666-115">We will be using a hosted solution.</span></span>

<span data-ttu-id="a5666-116">Il client Chef (nodo) rappresenta l'agente che risiede nei server gestiti.</span><span class="sxs-lookup"><span data-stu-id="a5666-116">The Chef Client (node) is the agent that sits on the servers you are managing.</span></span>

<span data-ttu-id="a5666-117">La workstation Chef rappresenta la workstation amministrativa in cui vengono creati i criteri e si eseguono i comandi di gestione.</span><span class="sxs-lookup"><span data-stu-id="a5666-117">The Chef Workstation is our admin workstation where we create our policies and execute our management commands.</span></span> <span data-ttu-id="a5666-118">Dalla Chef Workstation è possibile eseguire il comando **knife** per gestire l'infrastruttura.</span><span class="sxs-lookup"><span data-stu-id="a5666-118">We run the **knife** command from the Chef Workstation to manage our infrastructure.</span></span>

<span data-ttu-id="a5666-119">I "cookbook" e i "recipe"</span><span class="sxs-lookup"><span data-stu-id="a5666-119">There is also the concept of “Cookbooks” and “Recipes”.</span></span> <span data-ttu-id="a5666-120">costituiscono invece i criteri effettivi che vengono definiti e applicati ai server.</span><span class="sxs-lookup"><span data-stu-id="a5666-120">These are effectively the policies we define and apply to our servers.</span></span>

## <a name="preparing-the-workstation"></a><span data-ttu-id="a5666-121">Predisposizione della workstation</span><span class="sxs-lookup"><span data-stu-id="a5666-121">Preparing the workstation</span></span>
<span data-ttu-id="a5666-122">In primo luogo, è necessario predisporre la workstation.</span><span class="sxs-lookup"><span data-stu-id="a5666-122">First, lets prep the workstation.</span></span> <span data-ttu-id="a5666-123">Nel seguente esempio viene utilizzata una workstation Windows standard.</span><span class="sxs-lookup"><span data-stu-id="a5666-123">I’m using a standard Windows workstation.</span></span> <span data-ttu-id="a5666-124">È necessario creare una directory per archiviare i file di configurazione e i cookbook.</span><span class="sxs-lookup"><span data-stu-id="a5666-124">We need to create a directory to store our config files and cookbooks.</span></span>

<span data-ttu-id="a5666-125">Creare innanzitutto una directory denominata C:\chef.</span><span class="sxs-lookup"><span data-stu-id="a5666-125">First create a directory called C:\chef.</span></span>

<span data-ttu-id="a5666-126">Creare quindi una seconda directory denominata c:\chef\cookbooks.</span><span class="sxs-lookup"><span data-stu-id="a5666-126">Then create a second directory called c:\chef\cookbooks.</span></span>

<span data-ttu-id="a5666-127">A questo punto, è necessario scaricare il file di impostazioni di Azure affinché Chef possa comunicare con la sottoscrizione Azure.</span><span class="sxs-lookup"><span data-stu-id="a5666-127">We now need to download our Azure settings file so Chef can communicate with our Azure subscription.</span></span>

<!--Download your publish settings from [here](https://manage.windowsazure.com/publishsettings/).-->
<span data-ttu-id="a5666-128">Scaricare le impostazioni di pubblicazione tramite il comando di Azure PowerShell [Get-AzurePublishSettingsFile](https://docs.microsoft.com/en-us/powershell/module/azure/get-azurepublishsettingsfile?view=azuresmps-4.0.0).</span><span class="sxs-lookup"><span data-stu-id="a5666-128">Download your publish settings using the PowerShell Azure [Get-AzurePublishSettingsFile](https://docs.microsoft.com/en-us/powershell/module/azure/get-azurepublishsettingsfile?view=azuresmps-4.0.0) command.</span></span> 

<span data-ttu-id="a5666-129">Salvare il file delle impostazioni di pubblicazione in C:\chef.</span><span class="sxs-lookup"><span data-stu-id="a5666-129">Save the publish settings file in C:\chef.</span></span>

## <a name="creating-a-managed-chef-account"></a><span data-ttu-id="a5666-130">Creazione di un account Chef gestito</span><span class="sxs-lookup"><span data-stu-id="a5666-130">Creating a managed Chef account</span></span>
<span data-ttu-id="a5666-131">Iscriversi per ottenere un account Chef ospitato [qui](https://manage.chef.io/signup)</span><span class="sxs-lookup"><span data-stu-id="a5666-131">Sign up for a hosted Chef account [here](https://manage.chef.io/signup).</span></span>

<span data-ttu-id="a5666-132">Durante il processo di iscrizione, verrà richiesto di creare una nuova organizzazione.</span><span class="sxs-lookup"><span data-stu-id="a5666-132">During the signup process, you will be asked to create a new organization.</span></span>

![][3]

<span data-ttu-id="a5666-133">Una volta creata l'organizzazione, scaricare lo Starter Kit.</span><span class="sxs-lookup"><span data-stu-id="a5666-133">Once your organization is created, download the starter kit.</span></span>

![][4]

> [!NOTE]
> <span data-ttu-id="a5666-134">Se viene visualizzato un messaggio di avviso che indica che le chiavi verranno reimpostate, è comunque possibile proseguire, in quanto non è stata ancora configurata alcuna infrastruttura.</span><span class="sxs-lookup"><span data-stu-id="a5666-134">If you receive a prompt warning you that your keys will be reset, it’s ok to proceed as we have no existing infrastructure configured as yet.</span></span>
> 
> 

<span data-ttu-id="a5666-135">Il file ZIP dello Starter Kit contiene i file di configurazione e le chiavi dell'organizzazione.</span><span class="sxs-lookup"><span data-stu-id="a5666-135">This starter kit zip file contains your organization config files and keys.</span></span>

## <a name="configuring-the-chef-workstation"></a><span data-ttu-id="a5666-136">Configurazione della workstation Chef</span><span class="sxs-lookup"><span data-stu-id="a5666-136">Configuring the Chef workstation</span></span>
<span data-ttu-id="a5666-137">Estrarre il contenuto del file chef-starter.zip in C:\chef.</span><span class="sxs-lookup"><span data-stu-id="a5666-137">Extract the content of the chef-starter.zip to C:\chef.</span></span>

<span data-ttu-id="a5666-138">Copiare tutti i file presenti nella directory chef-starter\chef-repo\.chef to your c:\chef.</span><span class="sxs-lookup"><span data-stu-id="a5666-138">Copy all files under chef-starter\chef-repo\.chef to your c:\chef directory.</span></span>

<span data-ttu-id="a5666-139">La directory avrà ora un aspetto analogo al seguente esempio:</span><span class="sxs-lookup"><span data-stu-id="a5666-139">Your directory should now look something like the following example.</span></span>

![][5]

<span data-ttu-id="a5666-140">Dovrebbero essere presenti quattro file, incluso il file di pubblicazione di Azure nella cartella c:\chef.</span><span class="sxs-lookup"><span data-stu-id="a5666-140">You should now have four files including the Azure publishing file in the root of c:\chef.</span></span>

<span data-ttu-id="a5666-141">I file PEM contengono le chiavi private dell'organizzazione e amministrative per la comunicazione, mentre il file knife.rb contiene la configurazione Knife.</span><span class="sxs-lookup"><span data-stu-id="a5666-141">The PEM files contain your organization and admin private keys for communication while the knife.rb file contains your knife configuration.</span></span> <span data-ttu-id="a5666-142">È necessario modificare il file knife.rb.</span><span class="sxs-lookup"><span data-stu-id="a5666-142">We will need to edit the knife.rb file.</span></span>

<span data-ttu-id="a5666-143">Aprire il file in un editor di testo e modificare la voce "cookbook_path" rimuovendo i caratteri /../ dal percorso. L'aspetto della riga dovrebbe essere simile al seguente:</span><span class="sxs-lookup"><span data-stu-id="a5666-143">Open the file in your editor of choice and modify the “cookbook_path” by removing the /../ from the path so it appears as shown next.</span></span>

    cookbook_path  ["#{current_dir}/cookbooks"]

<span data-ttu-id="a5666-144">Aggiungere inoltre la seguente riga, in cui è necessario specificare il nome del file delle impostazioni di pubblicazione di Azure.</span><span class="sxs-lookup"><span data-stu-id="a5666-144">Also add the following line reflecting the name of your Azure publish settings file.</span></span>

    knife[:azure_publish_settings_file] = "yourfilename.publishsettings"

<span data-ttu-id="a5666-145">Il file knife.rb dovrebbe avere un aspetto simile al seguente esempio:</span><span class="sxs-lookup"><span data-stu-id="a5666-145">Your knife.rb file should now look similar to the following example.</span></span>

![][6]

<span data-ttu-id="a5666-146">Queste righe sono necessarie per garantire la presenza di riferimenti Knife nella directory di cookbook c:\chef\cookbooks e per usare il file delle impostazioni di pubblicazione di Azure durante le operazioni con Azure.</span><span class="sxs-lookup"><span data-stu-id="a5666-146">These lines will ensure that Knife references the cookbooks directory under c:\chef\cookbooks, and also uses our Azure Publish Settings file during Azure operations.</span></span>

## <a name="installing-the-chef-development-kit"></a><span data-ttu-id="a5666-147">Installazione di Chef Development Kit</span><span class="sxs-lookup"><span data-stu-id="a5666-147">Installing the Chef Development Kit</span></span>
<span data-ttu-id="a5666-148">A questo punto, [scaricare e installare](http://downloads.getchef.com/chef-dk/windows) il ChefDK (Chef Development Kit) per configurare la workstation Chef.</span><span class="sxs-lookup"><span data-stu-id="a5666-148">Next [download and install](http://downloads.getchef.com/chef-dk/windows) the ChefDK (Chef Development Kit) to set up your Chef Workstation.</span></span>

![][7]

<span data-ttu-id="a5666-149">Installare nel percorso predefinito c:\opscode.</span><span class="sxs-lookup"><span data-stu-id="a5666-149">Install in the default location of c:\opscode.</span></span> <span data-ttu-id="a5666-150">L'installazione richiederà all'incirca 10 minuti.</span><span class="sxs-lookup"><span data-stu-id="a5666-150">This install will take around 10 minutes.</span></span>

<span data-ttu-id="a5666-151">Verificare che la variabile PATH contenga voci relative ai percorsi C:\opscode\chefdk\bin;C:\opscode\chefdk\embedded\bin;c:\users\yourusername\.chefdk\gem\ruby\2.0.0\bin</span><span class="sxs-lookup"><span data-stu-id="a5666-151">Confirm your PATH variable contains entries for C:\opscode\chefdk\bin;C:\opscode\chefdk\embedded\bin;c:\users\yourusername\.chefdk\gem\ruby\2.0.0\bin</span></span>

<span data-ttu-id="a5666-152">Se questi percorsi non sono presenti, assicurarsi di aggiungerli.</span><span class="sxs-lookup"><span data-stu-id="a5666-152">If they are not there, make sure you add these paths!</span></span>

<span data-ttu-id="a5666-153">*CONSIDERARE CHE L'ORDINE DEL PERCORSO È IMPORTANTE.*</span><span class="sxs-lookup"><span data-stu-id="a5666-153">*NOTE THE ORDER OF THE PATH IS IMPORTANT!*</span></span> <span data-ttu-id="a5666-154">Se i percorsi opscode non sono presenti nell'ordine corretto, si verificheranno dei problemi.</span><span class="sxs-lookup"><span data-stu-id="a5666-154">If your opscode paths are not in the correct order you will have issues.</span></span>

<span data-ttu-id="a5666-155">Prima di continuare, riavviare la workstation.</span><span class="sxs-lookup"><span data-stu-id="a5666-155">Reboot your workstation before you continue.</span></span>

<span data-ttu-id="a5666-156">Il passaggio successivo prevede l'installazione dell'estensione Knife di Azure,</span><span class="sxs-lookup"><span data-stu-id="a5666-156">Next, we will install the Knife Azure extension.</span></span> <span data-ttu-id="a5666-157">che fornisce il "plug-in Azure" a Knife.</span><span class="sxs-lookup"><span data-stu-id="a5666-157">This provides Knife with the “Azure Plugin”.</span></span>

<span data-ttu-id="a5666-158">Eseguire il comando indicato di seguito.</span><span class="sxs-lookup"><span data-stu-id="a5666-158">Run the following command.</span></span>

    chef gem install knife-azure ––pre

> [!NOTE]
> <span data-ttu-id="a5666-159">L'argomento "-pre" assicura che si riceverà la versione RC più recente del plug-in Azure di Knife, che fornisce l'accesso al set di API più recente.</span><span class="sxs-lookup"><span data-stu-id="a5666-159">The –pre argument ensures you are receiving the latest RC version of the Knife Azure Plugin which provides access to the latest set of APIs.</span></span>
> 
> 

<span data-ttu-id="a5666-160">È probabile che durante l'installazione verranno installate anche diverse dipendenze.</span><span class="sxs-lookup"><span data-stu-id="a5666-160">It’s likely that a number of dependencies will also be installed at the same time.</span></span>

![][8]

<span data-ttu-id="a5666-161">Per assicurarsi che tutto sia configurato correttamente, eseguire il seguente comando:</span><span class="sxs-lookup"><span data-stu-id="a5666-161">To ensure everything is configured correctly, run the following command.</span></span>

    knife azure image list

<span data-ttu-id="a5666-162">Se tutto è stato configurato correttamente, verrà visualizzato un elenco delle immagini di Azure disponibili.</span><span class="sxs-lookup"><span data-stu-id="a5666-162">If everything is configured correctly, you will see a list of available Azure images scroll through.</span></span>

<span data-ttu-id="a5666-163">A questo punto</span><span class="sxs-lookup"><span data-stu-id="a5666-163">Congratulations.</span></span> <span data-ttu-id="a5666-164">La workstation è impostata.</span><span class="sxs-lookup"><span data-stu-id="a5666-164">The workstation is set up!</span></span>

## <a name="creating-a-cookbook"></a><span data-ttu-id="a5666-165">Creazione di un cookbook</span><span class="sxs-lookup"><span data-stu-id="a5666-165">Creating a Cookbook</span></span>
<span data-ttu-id="a5666-166">Chef usa i cookbook per definire i set di comandi che si desidera eseguire nel client gestito.</span><span class="sxs-lookup"><span data-stu-id="a5666-166">A Cookbook is used by Chef to define a set of commands that you wish to execute on your managed client.</span></span> <span data-ttu-id="a5666-167">La creazione di un cookbook è molto semplice. A tale scopo viene usato il comando **chef generate cookbook** per generare il modello di cookbook.</span><span class="sxs-lookup"><span data-stu-id="a5666-167">Creating a Cookbook is straightforward and we use the **chef generate cookbook** command to generate our Cookbook template.</span></span> <span data-ttu-id="a5666-168">In questo esempio il cookbook verrà denominato webserver, in quanto si desidera creare un criterio che distribuisca automaticamente IIS.</span><span class="sxs-lookup"><span data-stu-id="a5666-168">I will be calling my Cookbook web server as I would like a policy that automatically deploys IIS.</span></span>

<span data-ttu-id="a5666-169">Nella directory C:\Chef eseguire il seguente comando.</span><span class="sxs-lookup"><span data-stu-id="a5666-169">Under your C:\Chef directory run the following command.</span></span>

    chef generate cookbook webserver

<span data-ttu-id="a5666-170">Verrà generato un set di file nella directory C:\Chef\cookbooks\webserver.</span><span class="sxs-lookup"><span data-stu-id="a5666-170">This will generate a set of files under the directory C:\Chef\cookbooks\webserver.</span></span> <span data-ttu-id="a5666-171">A questo punto è necessario definire il set di comandi che il client Chef dovrà eseguire nella macchina virtuale gestita.</span><span class="sxs-lookup"><span data-stu-id="a5666-171">We now need to define the set of commands we would like our Chef client to execute on our managed virtual machine.</span></span>

<span data-ttu-id="a5666-172">I comandi vengono archiviati nel file default.rb.</span><span class="sxs-lookup"><span data-stu-id="a5666-172">The commands are stored in the file default.rb.</span></span> <span data-ttu-id="a5666-173">In questo file verrà definito un set di comandi che consente di installare IIS, avviare IIS e copiare un file di modello nella cartella wwwroot.</span><span class="sxs-lookup"><span data-stu-id="a5666-173">In this file, I’ll be defining a set of commands that installs IIS, starts IIS and copies a template file to the wwwroot folder.</span></span>

<span data-ttu-id="a5666-174">Modificare il file C:\chef\cookbooks\webserver\recipes\default.rb e aggiungere le seguenti righe:</span><span class="sxs-lookup"><span data-stu-id="a5666-174">Modify the C:\chef\cookbooks\webserver\recipes\default.rb file and add the following lines.</span></span>

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

<span data-ttu-id="a5666-175">Al termine dell'operazione, salvare il file.</span><span class="sxs-lookup"><span data-stu-id="a5666-175">Save the file once you are done.</span></span>

## <a name="creating-a-template"></a><span data-ttu-id="a5666-176">Creazione di un modello</span><span class="sxs-lookup"><span data-stu-id="a5666-176">Creating a template</span></span>
<span data-ttu-id="a5666-177">Come accennato in precedenza, è necessario generare un file di modello che verrà usato come pagina Default.html.</span><span class="sxs-lookup"><span data-stu-id="a5666-177">As we mentioned previously, we need to generate a template file which will be used as our default.html page.</span></span>

<span data-ttu-id="a5666-178">Eseguire il seguente comando per generare il modello.</span><span class="sxs-lookup"><span data-stu-id="a5666-178">Run the following command to generate the template.</span></span>

    chef generate template webserver Default.htm

<span data-ttu-id="a5666-179">Selezionare ora il file C:\chef\cookbooks\webserver\templates\default\Default.htm.erb.</span><span class="sxs-lookup"><span data-stu-id="a5666-179">Now navigate to the C:\chef\cookbooks\webserver\templates\default\Default.htm.erb file.</span></span> <span data-ttu-id="a5666-180">Modificare il file aggiungendo un semplice codice HTML, ad esempio alcune parole di benvenuto, e salvare il file.</span><span class="sxs-lookup"><span data-stu-id="a5666-180">Edit the file by adding some simple “Hello World” HTML code, and then save the file.</span></span>

## <a name="upload-the-cookbook-to-the-chef-server"></a><span data-ttu-id="a5666-181">Caricare il cookbook nel server Chef</span><span class="sxs-lookup"><span data-stu-id="a5666-181">Upload the Cookbook to the Chef Server</span></span>
<span data-ttu-id="a5666-182">In questo passaggio il cookbook creato nel computer locale verrà copiato e caricato nel server Chef di hosting.</span><span class="sxs-lookup"><span data-stu-id="a5666-182">In this step, we are taking a copy of the Cookbook that we have created on our local machine and uploading it to the Chef Hosted Server.</span></span> <span data-ttu-id="a5666-183">Una volta caricato, il cookbook verrà visualizzato nella scheda dei **Criteri** .</span><span class="sxs-lookup"><span data-stu-id="a5666-183">Once uploaded, the Cookbook will appear under the **Policy** tab.</span></span>

    knife cookbook upload webserver

![][9]

## <a name="deploy-a-virtual-machine-with-knife-azure"></a><span data-ttu-id="a5666-184">Distribuzione di una macchina virtuale con il comando Knife Azure</span><span class="sxs-lookup"><span data-stu-id="a5666-184">Deploy a virtual machine with Knife Azure</span></span>
<span data-ttu-id="a5666-185">Questo passaggio descrive come distribuire una macchina virtuale di Azure e applicare il cookbook "Webserver", che installerà il servizio Web IIS e la pagina Web predefinita.</span><span class="sxs-lookup"><span data-stu-id="a5666-185">We will now deploy an Azure virtual machine and apply the “Webserver” Cookbook which will install our IIS web service and default web page.</span></span>

<span data-ttu-id="a5666-186">Per eseguire questa operazione, utilizzare il comando **knife azure server create** .</span><span class="sxs-lookup"><span data-stu-id="a5666-186">In order to do this, use the **knife azure server create** command.</span></span>

<span data-ttu-id="a5666-187">Un esempio del comando è visualizzato qui di seguito.</span><span class="sxs-lookup"><span data-stu-id="a5666-187">Am example of the command appears next.</span></span>

    knife azure server create --azure-dns-name 'diegotest01' --azure-vm-name 'testserver01' --azure-vm-size 'Small' --azure-storage-account 'portalvhdsxxxx' --bootstrap-protocol 'cloud-api' --azure-source-image 'a699494373c04fc0bc8f2bb1389d6106__Windows-Server-2012-Datacenter-201411.01-en.us-127GB.vhd' --azure-service-location 'Southeast Asia' --winrm-user azureuser --winrm-password 'myPassword123' --tcp-endpoints 80,3389 --r 'recipe[webserver]'

<span data-ttu-id="a5666-188">La funzione dei parametri è facilmente comprensibile.</span><span class="sxs-lookup"><span data-stu-id="a5666-188">The parameters are self-explanatory.</span></span> <span data-ttu-id="a5666-189">Sostituire le variabili desiderate ed eseguire il comando.</span><span class="sxs-lookup"><span data-stu-id="a5666-189">Substitute your particular variables and run.</span></span>

> [!NOTE]
> <span data-ttu-id="a5666-190">Nella riga di comando sono state automatizzate anche le regole di filtro per la rete degli endpoint mediante il parametro –tcp-endpoints.</span><span class="sxs-lookup"><span data-stu-id="a5666-190">Through the the command line, I’m also automating my endpoint network filter rules by using the –tcp-endpoints parameter.</span></span> <span data-ttu-id="a5666-191">Sono state aperte le porte 80 e 3389 per fornire l'accesso per la pagina Web e la sessione RDP.</span><span class="sxs-lookup"><span data-stu-id="a5666-191">I’ve opened up ports 80 and 3389 to provide access to my web page and RDP session.</span></span>
> 
> 

<span data-ttu-id="a5666-192">Una volta eseguito il comando, passare al portale di Azure, dove il computer inizia già a eseguire il provisioning.</span><span class="sxs-lookup"><span data-stu-id="a5666-192">Once you run the command, go to the Azure portal and you will see your machine begin to provision.</span></span>

![][13]

<span data-ttu-id="a5666-193">Di seguito viene visualizzato il prompt dei comandi.</span><span class="sxs-lookup"><span data-stu-id="a5666-193">The command prompt appears next.</span></span>

![][10]

<span data-ttu-id="a5666-194">Una volta completata la distribuzione, dovrebbe essere possibile connettersi al servizio Web attraverso la porta 80, che è stata aperta quando è stato eseguito il provisioning della macchina virtuale con il comando knife azure.</span><span class="sxs-lookup"><span data-stu-id="a5666-194">Once the deployment is complete, we should be able to connect to the web service over port 80 as we had opened the port when we provisioned the virtual machine with the Knife Azure command.</span></span> <span data-ttu-id="a5666-195">Dal momento che questa macchina virtuale è l'unica macchina virtuale presente nel servizio cloud di questo esempio, verrà connessa con l'URL del servizio cloud.</span><span class="sxs-lookup"><span data-stu-id="a5666-195">As this virtual machine is the only virtual machine in my cloud service, I’ll connect it with the cloud service url.</span></span>

![][11]

<span data-ttu-id="a5666-196">In questo esempio è stata impiegata una certa dose di creatività nell'uso del codice HTML.</span><span class="sxs-lookup"><span data-stu-id="a5666-196">As you can see, I got creative with my HTML code.</span></span>

<span data-ttu-id="a5666-197">Tenere anche presente che è anche possibile connettersi tramite una sessione RDP dal Portale di Azure attraverso la porta 3389.</span><span class="sxs-lookup"><span data-stu-id="a5666-197">Don’t forget we can also connect through an RDP session from the Azure portal via port 3389.</span></span>

<span data-ttu-id="a5666-198">Si spera che questa guida sia stata utile.</span><span class="sxs-lookup"><span data-stu-id="a5666-198">I hope this has been helpful!</span></span> <span data-ttu-id="a5666-199">Ora è possibile avviare l'infrastruttura come percorso di codice con Azure.</span><span class="sxs-lookup"><span data-stu-id="a5666-199">Go  and start your infrastructure as code journey with Azure today!</span></span>

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

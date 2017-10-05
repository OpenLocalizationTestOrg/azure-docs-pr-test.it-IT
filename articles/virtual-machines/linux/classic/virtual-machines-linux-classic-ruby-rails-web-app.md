---
title: Ospitare un sito Web Rails in una macchina virtuale di Linux su Ruby | Documentazione Microsoft
description: Impostare e ospitare un sito Web basato su Ruby on Rails in Azure usando una macchina virtuale Linux.
services: virtual-machines-linux
documentationcenter: ruby
author: rmcmurray
manager: erikre
editor: 
tags: azure-service-management
ms.assetid: aad32685-3550-4bff-9c73-beb8d70b3291
ms.service: virtual-machines-linux
ms.workload: web
ms.tgt_pltfrm: vm-linux
ms.devlang: ruby
ms.topic: article
ms.date: 06/27/2017
ms.author: robmcm
ms.openlocfilehash: 0518519da6c5e62a863a47d6743ab7b7c5923acf
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/29/2017
---
# <a name="ruby-on-rails-web-application-on-an-azure-vm"></a><span data-ttu-id="0e003-103">Applicazione Web Ruby on Rails in una macchina virtuale di Azure</span><span class="sxs-lookup"><span data-stu-id="0e003-103">Ruby on Rails Web application on an Azure VM</span></span>
<span data-ttu-id="0e003-104">Questa esercitazione mostra come ospitare un sito Web Ruby on Rails usando una macchina virtuale Linux.</span><span class="sxs-lookup"><span data-stu-id="0e003-104">This tutorial shows how to host a Ruby on Rails website on Azure using a Linux virtual machine.</span></span>  

<span data-ttu-id="0e003-105">Questa esercitazione è stata convalidata usando Ubuntu Server 14.04 LTS.</span><span class="sxs-lookup"><span data-stu-id="0e003-105">This tutorial was validated using Ubuntu Server 14.04 LTS.</span></span> <span data-ttu-id="0e003-106">Se si usa una distribuzione Linux diversa, è necessario modificare la procedura per installare Rails.</span><span class="sxs-lookup"><span data-stu-id="0e003-106">If you use a different Linux distribution, you might need to modify the steps to install Rails.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="0e003-107">Azure offre due modelli di distribuzione per creare e usare le risorse: [Gestione risorse e la distribuzione classica](../../../azure-resource-manager/resource-manager-deployment-model.md).</span><span class="sxs-lookup"><span data-stu-id="0e003-107">Azure has two different deployment models for creating and working with resources:  [Resource Manager and classic](../../../azure-resource-manager/resource-manager-deployment-model.md).</span></span>  <span data-ttu-id="0e003-108">Questo articolo illustra l'uso del modello di distribuzione classica.</span><span class="sxs-lookup"><span data-stu-id="0e003-108">This article covers using the classic deployment model.</span></span> <span data-ttu-id="0e003-109">Microsoft consiglia di usare il modello di Gestione risorse per le distribuzioni più recenti.</span><span class="sxs-lookup"><span data-stu-id="0e003-109">Microsoft recommends that most new deployments use the Resource Manager model.</span></span>
>
>

## <a name="create-an-azure-vm"></a><span data-ttu-id="0e003-110">Creare una macchina virtuale di Azure</span><span class="sxs-lookup"><span data-stu-id="0e003-110">Create an Azure VM</span></span>
<span data-ttu-id="0e003-111">Iniziare creando una macchina virtuale di Azure con un'immagine Linux.</span><span class="sxs-lookup"><span data-stu-id="0e003-111">Start by creating an Azure VM with a Linux image.</span></span>

<span data-ttu-id="0e003-112">Per creare la VM, è possibile usare il portale di Azure o l'interfaccia della riga di comando (CLI) di Azure.</span><span class="sxs-lookup"><span data-stu-id="0e003-112">To create the VM, you can use the Azure portal or the Azure Command-Line Interface (CLI).</span></span>

### <a name="azure-portal"></a><span data-ttu-id="0e003-113">Portale di Azure</span><span class="sxs-lookup"><span data-stu-id="0e003-113">Azure portal</span></span>
1. <span data-ttu-id="0e003-114">Accedere al [portale di Azure](https://portal.azure.com)</span><span class="sxs-lookup"><span data-stu-id="0e003-114">Sign into the [Azure portal](https://portal.azure.com)</span></span>
2. <span data-ttu-id="0e003-115">Fare clic su **Nuovo**, quindi digitare "Ubuntu Server 14.04" nella casella di ricerca.</span><span class="sxs-lookup"><span data-stu-id="0e003-115">Click **New**, then type "Ubuntu Server 14.04" in the search box.</span></span> <span data-ttu-id="0e003-116">Fare clic sulla voce restituita dalla ricerca.</span><span class="sxs-lookup"><span data-stu-id="0e003-116">Click the entry returned by the search.</span></span> <span data-ttu-id="0e003-117">Come modello di distribuzione selezionare **Classico**, quindi fare clic su "Crea".</span><span class="sxs-lookup"><span data-stu-id="0e003-117">For the deployment model, select **Classic**, then click "Create".</span></span>
3. <span data-ttu-id="0e003-118">Nel pannello Informazioni di base immettere i valori per i campi obbligatori: nome (per la VM), nome utente, tipo di autenticazione e le credenziali corrispondenti, sottoscrizione di Azure, gruppo di risorse e località.</span><span class="sxs-lookup"><span data-stu-id="0e003-118">In the Basics blade, supply values for the required fields: Name (for the VM), User name, Authentication type and the corresponding credentials, Azure subscription, Resource group, and Location.</span></span>

   ![Creare una nuova immagine Ubuntu](./media/virtual-machines-linux-classic-ruby-rails-web-app/createvm.png)

4. <span data-ttu-id="0e003-120">Dopo il provisioning della macchina virtuale, fare clic sul nome della macchina virtuale e quindi fare clic su **Endpoint** nella categoria **Impostazioni**.</span><span class="sxs-lookup"><span data-stu-id="0e003-120">After the VM is provisioned, click on the VM name, and click **Endpoints** in the **Settings** category.</span></span> <span data-ttu-id="0e003-121">Trovare l'endpoint SSH, elencato in **Autonomo**.</span><span class="sxs-lookup"><span data-stu-id="0e003-121">Find the SSH endpoint, listed under **Standalone**.</span></span>

   ![Endpoint predefinito](./media/virtual-machines-linux-classic-ruby-rails-web-app/endpointsnewportal.png)

### <a name="azure-cli"></a><span data-ttu-id="0e003-123">Interfaccia della riga di comando di Azure</span><span class="sxs-lookup"><span data-stu-id="0e003-123">Azure CLI</span></span>
<span data-ttu-id="0e003-124">Seguire i passaggi in [Creazione rapida di una macchina virtuale che esegue Linux][vm-instructions].</span><span class="sxs-lookup"><span data-stu-id="0e003-124">Follow the steps in [Create a Virtual Machine Running Linux][vm-instructions].</span></span>

<span data-ttu-id="0e003-125">Al termine del provisioning della macchina virtuale, è possibile ottenere l'endpoint SSH eseguendo il comando seguente:</span><span class="sxs-lookup"><span data-stu-id="0e003-125">After the VM is provisioned, you can get the SSH endpoint by running the following command:</span></span>

    azure vm endpoint list <vm-name>  

## <a name="install-ruby-on-rails"></a><span data-ttu-id="0e003-126">Installare Ruby on Rails</span><span class="sxs-lookup"><span data-stu-id="0e003-126">Install Ruby on Rails</span></span>
1. <span data-ttu-id="0e003-127">Usare SSH per connettersi alla macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="0e003-127">Use SSH to connect to the VM.</span></span>
2. <span data-ttu-id="0e003-128">Dalla sessione SSH usare i comandi seguenti per installare Ruby nella macchina virtuale:</span><span class="sxs-lookup"><span data-stu-id="0e003-128">From the SSH session, use the following commands to install Ruby on the VM:</span></span>

        sudo apt-get update -y
        sudo apt-get upgrade -y

        sudo apt-add-repository ppa:brightbox/ruby-ng
        sudo apt-get update
        sudo apt-get install ruby2.4

        > [!TIP]
        > The brightbox repository contains the current Ruby distribution.

    <span data-ttu-id="0e003-129">L'installazione potrebbe richiedere alcuni minuti.</span><span class="sxs-lookup"><span data-stu-id="0e003-129">The installation may take a few minutes.</span></span> <span data-ttu-id="0e003-130">Al termine, immettere il comando seguente per verificare se l'installazione di Ruby è stata completata:</span><span class="sxs-lookup"><span data-stu-id="0e003-130">When it completes, use the following command to verify that Ruby is installed:</span></span>

        ruby -v

3. <span data-ttu-id="0e003-131">Immettere il comando seguente per installare Rails:</span><span class="sxs-lookup"><span data-stu-id="0e003-131">Use the following command to install Rails:</span></span>

        sudo gem install rails --no-rdoc --no-ri -V

    <span data-ttu-id="0e003-132">Per velocizzare l'operazione, usare i flag --no-rdoc e --no-ri per ignorare l'installazione della documentazione.</span><span class="sxs-lookup"><span data-stu-id="0e003-132">Use the --no-rdoc and --no-ri flags to skip installing the documentation, which is faster.</span></span>
    <span data-ttu-id="0e003-133">È probabile che l'esecuzione di questo comando richieda tempo, quindi l'aggiunta di -V consentirà di visualizzare lo stato dell'installazione.</span><span class="sxs-lookup"><span data-stu-id="0e003-133">This command will likely take a long time to execute, so adding the -V will display information about the installation progress.</span></span>

## <a name="create-and-run-an-app"></a><span data-ttu-id="0e003-134">Creare ed eseguire un'applicazione</span><span class="sxs-lookup"><span data-stu-id="0e003-134">Create and run an app</span></span>
<span data-ttu-id="0e003-135">Mentre si è ancora connessi con SSH, eseguire i comandi seguenti:</span><span class="sxs-lookup"><span data-stu-id="0e003-135">While still logged in via SSH, run the following commands:</span></span>

    rails new myapp
    cd myapp
    rails server -b 0.0.0.0 -p 3000

<span data-ttu-id="0e003-136">Il comando [new](http://guides.rubyonrails.org/command_line.html#rails-new) crea una nuova app Rails.</span><span class="sxs-lookup"><span data-stu-id="0e003-136">The [new](http://guides.rubyonrails.org/command_line.html#rails-new) command creates a new Rails app.</span></span> <span data-ttu-id="0e003-137">Il comando [server](http://guides.rubyonrails.org/command_line.html#rails-server) avvia il server Web WEBrick fornito con Rails.</span><span class="sxs-lookup"><span data-stu-id="0e003-137">The [server](http://guides.rubyonrails.org/command_line.html#rails-server) command starts the WEBrick web server that comes with Rails.</span></span> <span data-ttu-id="0e003-138">(per l'uso in un ambiente di produzione sarà opportuno usare un server differente, ad esempio Unicorn o Passenger).</span><span class="sxs-lookup"><span data-stu-id="0e003-138">(For production use, you would probably want to use a different server, such as Unicorn or Passenger.)</span></span>

<span data-ttu-id="0e003-139">L'output dovrebbe essere simile al seguente.</span><span class="sxs-lookup"><span data-stu-id="0e003-139">You should see output similar to the following.</span></span>

    => Booting WEBrick
    => Rails 4.2.1 application starting in development on http://0.0.0.0:3000
    => Run `rails server -h` for more startup options
    => Ctrl-C to shutdown server
    [2015-06-09 23:34:23] INFO  WEBrick 1.3.1
    [2015-06-09 23:34:23] INFO  ruby 1.9.3 (2013-11-22) [x86_64-linux]
    [2015-06-09 23:34:23] INFO  WEBrick::HTTPServer#start: pid=27766 port=3000

## <a name="add-an-endpoint"></a><span data-ttu-id="0e003-140">Aggiungere un endpoint</span><span class="sxs-lookup"><span data-stu-id="0e003-140">Add an endpoint</span></span>
1. <span data-ttu-id="0e003-141">Andare al [portale di Azure][https://portal.azure.com] e selezionare la VM.</span><span class="sxs-lookup"><span data-stu-id="0e003-141">Go to the [Azure portal][https://portal.azure.com] and select your VM.</span></span>

2. <span data-ttu-id="0e003-142">Selezionare **ENDPOINT** in **Impostazioni** sul lato sinistro della pagina.</span><span class="sxs-lookup"><span data-stu-id="0e003-142">Select **ENDPOINTS** in the **Settings** along the left edge the page.</span></span>

3. <span data-ttu-id="0e003-143">Nella parte superiore della pagina fare clic su **AGGIUNGI**.</span><span class="sxs-lookup"><span data-stu-id="0e003-143">Click **ADD** at the top of the page.</span></span>

4. <span data-ttu-id="0e003-144">Nella finestra di dialogo **Aggiungi endpoint** immettere le informazioni seguenti:</span><span class="sxs-lookup"><span data-stu-id="0e003-144">In the **Add endpoint** dialog page, enter the following information:</span></span>

   * <span data-ttu-id="0e003-145">**Nome**: HTTP</span><span class="sxs-lookup"><span data-stu-id="0e003-145">**Name**: HTTP</span></span>
   * <span data-ttu-id="0e003-146">**Protocollo**: TCP</span><span class="sxs-lookup"><span data-stu-id="0e003-146">**Protocol**: TCP</span></span>
   * <span data-ttu-id="0e003-147">**Porta pubblica**: 80</span><span class="sxs-lookup"><span data-stu-id="0e003-147">**Public port**: 80</span></span>
   * <span data-ttu-id="0e003-148">**Porta privata**: 3000</span><span class="sxs-lookup"><span data-stu-id="0e003-148">**Private port**: 3000</span></span>
   * <span data-ttu-id="0e003-149">**Indirizzo IP mobile**: Disabilitato</span><span class="sxs-lookup"><span data-stu-id="0e003-149">**Floating PI address**: Disabled</span></span>
   * <span data-ttu-id="0e003-150">**Elenco di controllo di accesso - Ordine**: 1001 o un altro valore che imposta la priorità di questa regola di accesso.</span><span class="sxs-lookup"><span data-stu-id="0e003-150">**Access control list - Order**: 1001, or another value that sets the priority of this access rule.</span></span>
   * <span data-ttu-id="0e003-151">**Elenco di controllo di accesso - Nome**: allowHTTP</span><span class="sxs-lookup"><span data-stu-id="0e003-151">**Access control list - Name**: allowHTTP</span></span>
   * <span data-ttu-id="0e003-152">**Elenco di controllo di accesso - Azione**: consenti</span><span class="sxs-lookup"><span data-stu-id="0e003-152">**Access control list - Action**: permit</span></span>
   * <span data-ttu-id="0e003-153">**Elenco di controllo di accesso - Subnet remota**: 1.0.0.0/16</span><span class="sxs-lookup"><span data-stu-id="0e003-153">**Access control list - Remote subnet**: 1.0.0.0/16</span></span>

     <span data-ttu-id="0e003-154">Questo endpoint ha una porta pubblica 80 che instraderà il traffico alla porta privata 3000, dove è in ascolto il server Rails.</span><span class="sxs-lookup"><span data-stu-id="0e003-154">This endpoint  has a public port of 80 that will route traffic to the private port of 3000, where the Rails server is listening.</span></span> <span data-ttu-id="0e003-155">La regola dell'elenco di controllo di accesso consente il traffico pubblico sulla porta 80.</span><span class="sxs-lookup"><span data-stu-id="0e003-155">The access control list rule allows public traffic on port 80.</span></span>

     ![new-endpoint](./media/virtual-machines-linux-classic-ruby-rails-web-app/createendpoint.png)

5. <span data-ttu-id="0e003-157">Fare clic su OK per salvare l'endpoint.</span><span class="sxs-lookup"><span data-stu-id="0e003-157">Click OK to save the endpoint.</span></span>

6. <span data-ttu-id="0e003-158">Verrà visualizzato il messaggio **Salvataggio dell'endpoint della macchina virtuale**.</span><span class="sxs-lookup"><span data-stu-id="0e003-158">A message should appear that states **Saving virtual machine endpoint**.</span></span> <span data-ttu-id="0e003-159">Quando questo messaggio scompare, significa che l'endpoint è attivo.</span><span class="sxs-lookup"><span data-stu-id="0e003-159">Once this message disappears, the endpoint is active.</span></span> <span data-ttu-id="0e003-160">A questo punto è possibile testare l'applicazione passando al nome DNS della macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="0e003-160">You may now test your application by navigating to the DNS name of your virtual machine.</span></span> <span data-ttu-id="0e003-161">L'aspetto del sito Web dovrebbe essere simile al seguente:</span><span class="sxs-lookup"><span data-stu-id="0e003-161">The website should appear similar to the following:</span></span>

    ![Pagina predefinita Rails][default-rails-cloud]

## <a name="next-steps"></a><span data-ttu-id="0e003-163">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="0e003-163">Next steps</span></span>
<span data-ttu-id="0e003-164">In questa esercitazione è stata eseguita la maggior parte dei passaggi manualmente.</span><span class="sxs-lookup"><span data-stu-id="0e003-164">In this tutorial, you did most of the steps manually.</span></span> <span data-ttu-id="0e003-165">In un ambiente di produzione, si potrebbe scrivere l'applicazione in un computer di sviluppo e distribuirla nella macchina virtuale di Azure.</span><span class="sxs-lookup"><span data-stu-id="0e003-165">In a production environment, you would write your app on a development machine and deploy it to the Azure VM.</span></span> <span data-ttu-id="0e003-166">Inoltre, la maggior parte degli ambienti di produzione ospita l'applicazione Rails insieme a un altro processo server, ad esempio Apache o NginX, che gestisce il routing delle richieste a più istanze dell'applicazione Rails e la distribuzione di risorse statiche.</span><span class="sxs-lookup"><span data-stu-id="0e003-166">Also, most production environments host the Rails application in conjunction with another server process such as Apache or NginX, which handles request routing to multiple instances of the Rails application and serving static resources.</span></span> <span data-ttu-id="0e003-167">Per altre informazioni, vedere http://rubyonrails.org/deploy/.</span><span class="sxs-lookup"><span data-stu-id="0e003-167">For more information, see http://rubyonrails.org/deploy/.</span></span>

<span data-ttu-id="0e003-168">Per altre informazioni su Ruby on Rails, vedere le [Guide di Ruby on Rails][rails-guides].</span><span class="sxs-lookup"><span data-stu-id="0e003-168">To learn more about Ruby on Rails, visit the [Ruby on Rails Guides][rails-guides].</span></span>

<span data-ttu-id="0e003-169">Per usare servizi di Azure dall'applicazione Ruby, vedere:</span><span class="sxs-lookup"><span data-stu-id="0e003-169">To use Azure services from your Ruby application, see:</span></span>

* <span data-ttu-id="0e003-170">[Archiviare dati non strutturati mediante BLOB][blobs]</span><span class="sxs-lookup"><span data-stu-id="0e003-170">[Store unstructured data using blobs][blobs]</span></span>
* <span data-ttu-id="0e003-171">[Archiviare coppie chiave-valore mediante tabelle][tables]</span><span class="sxs-lookup"><span data-stu-id="0e003-171">[Store key/value pairs using tables][tables]</span></span>
* <span data-ttu-id="0e003-172">[Distribuire contenuti ad ampia larghezza di banda con la rete per la distribuzione di contenuti][cdn-howto]</span><span class="sxs-lookup"><span data-stu-id="0e003-172">[Serve high bandwidth content with the Content Delivery Network][cdn-howto]</span></span>

<!-- WA.com links -->
[blobs]:../../../storage/blobs/storage-ruby-how-to-use-blob-storage.md
[cdn-howto]:https://azure.microsoft.com/develop/ruby/app-services/
[tables]:../../../cosmos-db/table-storage-how-to-use-ruby.md
[vm-instructions]:createportal.md

<!-- External Links -->
[rails-guides]:http://guides.rubyonrails.org/
[sqlite3]:http://www.sqlite.org/

<!-- Images -->

[default-rails-cloud]:./media/virtual-machines-linux-classic-ruby-rails-web-app/basicrailscloud.png
[vmlist]:./media/virtual-machines-linux-classic-ruby-rails-web-app/vmlist.png
[endpoints]:./media/virtual-machines-linux-classic-ruby-rails-web-app/endpoints.png
[new-endpoint]:./media/virtual-machines-linux-classic-ruby-rails-web-app/newendpoint.png
[new-endpoint1]:./media/virtual-machines-linux-classic-ruby-rails-web-app/newendpoint1.png

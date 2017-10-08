---
title: aaaHost una trascrizione nel sito Web di guide in una VM Linux | Documenti Microsoft
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
ms.openlocfilehash: c545c24fc6c89497854bbe55a6d0d1d0b072c386
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="ruby-on-rails-web-application-on-an-azure-vm"></a><span data-ttu-id="4cff7-103">Applicazione Web Ruby on Rails in una macchina virtuale di Azure</span><span class="sxs-lookup"><span data-stu-id="4cff7-103">Ruby on Rails Web application on an Azure VM</span></span>
<span data-ttu-id="4cff7-104">Questa esercitazione viene illustrato come toohost una trascrizione nel sito Web di guide in Azure utilizzando una macchina virtuale di Linux.</span><span class="sxs-lookup"><span data-stu-id="4cff7-104">This tutorial shows how toohost a Ruby on Rails website on Azure using a Linux virtual machine.</span></span>  

<span data-ttu-id="4cff7-105">Questa esercitazione è stata convalidata usando Ubuntu Server 14.04 LTS.</span><span class="sxs-lookup"><span data-stu-id="4cff7-105">This tutorial was validated using Ubuntu Server 14.04 LTS.</span></span> <span data-ttu-id="4cff7-106">Se si utilizza una distribuzione Linux diversa, potrebbe essere necessario toomodify hello passaggi tooinstall Guide.</span><span class="sxs-lookup"><span data-stu-id="4cff7-106">If you use a different Linux distribution, you might need toomodify hello steps tooinstall Rails.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="4cff7-107">Azure offre due modelli di distribuzione per creare e usare le risorse: [Gestione risorse e la distribuzione classica](../../../azure-resource-manager/resource-manager-deployment-model.md).</span><span class="sxs-lookup"><span data-stu-id="4cff7-107">Azure has two different deployment models for creating and working with resources:  [Resource Manager and classic](../../../azure-resource-manager/resource-manager-deployment-model.md).</span></span>  <span data-ttu-id="4cff7-108">In questo articolo viene illustrato l'utilizzo del modello di distribuzione classica hello.</span><span class="sxs-lookup"><span data-stu-id="4cff7-108">This article covers using hello classic deployment model.</span></span> <span data-ttu-id="4cff7-109">Si consiglia di utilizzano il modello di gestione risorse hello più nuove distribuzioni.</span><span class="sxs-lookup"><span data-stu-id="4cff7-109">Microsoft recommends that most new deployments use hello Resource Manager model.</span></span>
>
>

## <a name="create-an-azure-vm"></a><span data-ttu-id="4cff7-110">Creare una macchina virtuale di Azure</span><span class="sxs-lookup"><span data-stu-id="4cff7-110">Create an Azure VM</span></span>
<span data-ttu-id="4cff7-111">Iniziare creando una macchina virtuale di Azure con un'immagine Linux.</span><span class="sxs-lookup"><span data-stu-id="4cff7-111">Start by creating an Azure VM with a Linux image.</span></span>

<span data-ttu-id="4cff7-112">toocreate hello VM, è possibile utilizzare il portale di Azure hello o hello Azure interfaccia della riga di comando (CLI).</span><span class="sxs-lookup"><span data-stu-id="4cff7-112">toocreate hello VM, you can use hello Azure portal or hello Azure Command-Line Interface (CLI).</span></span>

### <a name="azure-portal"></a><span data-ttu-id="4cff7-113">Portale di Azure</span><span class="sxs-lookup"><span data-stu-id="4cff7-113">Azure portal</span></span>
1. <span data-ttu-id="4cff7-114">Sign in hello [portale di Azure](https://portal.azure.com)</span><span class="sxs-lookup"><span data-stu-id="4cff7-114">Sign into hello [Azure portal](https://portal.azure.com)</span></span>
2. <span data-ttu-id="4cff7-115">Fare clic su **New**, quindi digitare "Ubuntu Server 14.04" nella casella di ricerca hello.</span><span class="sxs-lookup"><span data-stu-id="4cff7-115">Click **New**, then type "Ubuntu Server 14.04" in hello search box.</span></span> <span data-ttu-id="4cff7-116">Fare clic sulla voce hello restituito dalla ricerca hello.</span><span class="sxs-lookup"><span data-stu-id="4cff7-116">Click hello entry returned by hello search.</span></span> <span data-ttu-id="4cff7-117">Per il modello di distribuzione di hello, selezionare **classico**, quindi fare clic su "Crea".</span><span class="sxs-lookup"><span data-stu-id="4cff7-117">For hello deployment model, select **Classic**, then click "Create".</span></span>
3. <span data-ttu-id="4cff7-118">Nel Pannello di nozioni di base hello, specificare i valori per i campi necessario hello: nome (per hello VM), nome utente, tipo di autenticazione e le credenziali corrispondenti hello, sottoscrizione di Azure, gruppo di risorse e percorso.</span><span class="sxs-lookup"><span data-stu-id="4cff7-118">In hello Basics blade, supply values for hello required fields: Name (for hello VM), User name, Authentication type and hello corresponding credentials, Azure subscription, Resource group, and Location.</span></span>

   ![Creare una nuova immagine Ubuntu](./media/virtual-machines-linux-classic-ruby-rails-web-app/createvm.png)

4. <span data-ttu-id="4cff7-120">Dopo il provisioning di hello VM, fare clic sul nome della macchina virtuale hello e fare clic su **endpoint** in hello **impostazioni** categoria.</span><span class="sxs-lookup"><span data-stu-id="4cff7-120">After hello VM is provisioned, click on hello VM name, and click **Endpoints** in hello **Settings** category.</span></span> <span data-ttu-id="4cff7-121">Trovare l'endpoint SSH hello, elencati in **autonomo**.</span><span class="sxs-lookup"><span data-stu-id="4cff7-121">Find hello SSH endpoint, listed under **Standalone**.</span></span>

   ![Endpoint predefinito](./media/virtual-machines-linux-classic-ruby-rails-web-app/endpointsnewportal.png)

### <a name="azure-cli"></a><span data-ttu-id="4cff7-123">Interfaccia della riga di comando di Azure</span><span class="sxs-lookup"><span data-stu-id="4cff7-123">Azure CLI</span></span>
<span data-ttu-id="4cff7-124">Seguire i passaggi di hello in [creare una macchina virtuale che esegue Linux][vm-instructions].</span><span class="sxs-lookup"><span data-stu-id="4cff7-124">Follow hello steps in [Create a Virtual Machine Running Linux][vm-instructions].</span></span>

<span data-ttu-id="4cff7-125">Dopo il provisioning di hello VM, è possibile ottenere l'endpoint SSH hello eseguendo hello comando seguente:</span><span class="sxs-lookup"><span data-stu-id="4cff7-125">After hello VM is provisioned, you can get hello SSH endpoint by running hello following command:</span></span>

    azure vm endpoint list <vm-name>  

## <a name="install-ruby-on-rails"></a><span data-ttu-id="4cff7-126">Installare Ruby on Rails</span><span class="sxs-lookup"><span data-stu-id="4cff7-126">Install Ruby on Rails</span></span>
1. <span data-ttu-id="4cff7-127">Usare SSH tooconnect toohello macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="4cff7-127">Use SSH tooconnect toohello VM.</span></span>
2. <span data-ttu-id="4cff7-128">Dalla sessione SSH hello, utilizzare hello seguendo i comandi tooinstall Ruby hello VM:</span><span class="sxs-lookup"><span data-stu-id="4cff7-128">From hello SSH session, use hello following commands tooinstall Ruby on hello VM:</span></span>

        sudo apt-get update -y
        sudo apt-get upgrade -y

        sudo apt-add-repository ppa:brightbox/ruby-ng
        sudo apt-get update
        sudo apt-get install ruby2.4

        > [!TIP]
        > hello brightbox repository contains hello current Ruby distribution.

    <span data-ttu-id="4cff7-129">installazione di Hello potrebbe richiedere alcuni minuti.</span><span class="sxs-lookup"><span data-stu-id="4cff7-129">hello installation may take a few minutes.</span></span> <span data-ttu-id="4cff7-130">Quando viene completato, usare hello successivo comando tooverify Ruby è installato:</span><span class="sxs-lookup"><span data-stu-id="4cff7-130">When it completes, use hello following command tooverify that Ruby is installed:</span></span>

        ruby -v

3. <span data-ttu-id="4cff7-131">Comando che segue di hello utilizzare tooinstall Guide:</span><span class="sxs-lookup"><span data-stu-id="4cff7-131">Use hello following command tooinstall Rails:</span></span>

        sudo gem install rails --no-rdoc --no-ri -V

    <span data-ttu-id="4cff7-132">Utilizzare hello - no-rdoc e --no-ri flag tooskip installazione della documentazione di hello, che è più veloce.</span><span class="sxs-lookup"><span data-stu-id="4cff7-132">Use hello --no-rdoc and --no-ri flags tooskip installing hello documentation, which is faster.</span></span>
    <span data-ttu-id="4cff7-133">Questo comando richiederà probabilmente tooexecute, pertanto l'aggiunta di hello -V verrà visualizzate le informazioni sullo stato dell'installazione hello molto tempo.</span><span class="sxs-lookup"><span data-stu-id="4cff7-133">This command will likely take a long time tooexecute, so adding hello -V will display information about hello installation progress.</span></span>

## <a name="create-and-run-an-app"></a><span data-ttu-id="4cff7-134">Creare ed eseguire un'applicazione</span><span class="sxs-lookup"><span data-stu-id="4cff7-134">Create and run an app</span></span>
<span data-ttu-id="4cff7-135">Mentre si è ancora connessi tramite SSH, eseguire hello seguenti comandi:</span><span class="sxs-lookup"><span data-stu-id="4cff7-135">While still logged in via SSH, run hello following commands:</span></span>

    rails new myapp
    cd myapp
    rails server -b 0.0.0.0 -p 3000

<span data-ttu-id="4cff7-136">Hello [nuova](http://guides.rubyonrails.org/command_line.html#rails-new) comando crea una nuova app Guide.</span><span class="sxs-lookup"><span data-stu-id="4cff7-136">hello [new](http://guides.rubyonrails.org/command_line.html#rails-new) command creates a new Rails app.</span></span> <span data-ttu-id="4cff7-137">Hello [server](http://guides.rubyonrails.org/command_line.html#rails-server) comando Avvia hello server web WEBrick fornita con guide.</span><span class="sxs-lookup"><span data-stu-id="4cff7-137">hello [server](http://guides.rubyonrails.org/command_line.html#rails-server) command starts hello WEBrick web server that comes with Rails.</span></span> <span data-ttu-id="4cff7-138">(Per la produzione, è preferibile toouse un server diverso, ad esempio esclusive o passeggero.)</span><span class="sxs-lookup"><span data-stu-id="4cff7-138">(For production use, you would probably want toouse a different server, such as Unicorn or Passenger.)</span></span>

<span data-ttu-id="4cff7-139">Verrà visualizzato il seguente toohello simili di output.</span><span class="sxs-lookup"><span data-stu-id="4cff7-139">You should see output similar toohello following.</span></span>

    => Booting WEBrick
    => Rails 4.2.1 application starting in development on http://0.0.0.0:3000
    => Run `rails server -h` for more startup options
    => Ctrl-C tooshutdown server
    [2015-06-09 23:34:23] INFO  WEBrick 1.3.1
    [2015-06-09 23:34:23] INFO  ruby 1.9.3 (2013-11-22) [x86_64-linux]
    [2015-06-09 23:34:23] INFO  WEBrick::HTTPServer#start: pid=27766 port=3000

## <a name="add-an-endpoint"></a><span data-ttu-id="4cff7-140">Aggiungere un endpoint</span><span class="sxs-lookup"><span data-stu-id="4cff7-140">Add an endpoint</span></span>
1. <span data-ttu-id="4cff7-141">Passare toohello [portale] [https://portal.azure.com] e selezionare la macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="4cff7-141">Go toohello [Azure portal][https://portal.azure.com] and select your VM.</span></span>

2. <span data-ttu-id="4cff7-142">Selezionare **endpoint** in hello **impostazioni** lungo pagina hello di hello bordo sinistro.</span><span class="sxs-lookup"><span data-stu-id="4cff7-142">Select **ENDPOINTS** in hello **Settings** along hello left edge hello page.</span></span>

3. <span data-ttu-id="4cff7-143">Fare clic su **aggiungere** nella parte superiore di hello della pagina hello.</span><span class="sxs-lookup"><span data-stu-id="4cff7-143">Click **ADD** at hello top of hello page.</span></span>

4. <span data-ttu-id="4cff7-144">In hello **aggiungere endpoint** finestra di dialogo immettere hello le seguenti informazioni:</span><span class="sxs-lookup"><span data-stu-id="4cff7-144">In hello **Add endpoint** dialog page, enter hello following information:</span></span>

   * <span data-ttu-id="4cff7-145">**Nome**: HTTP</span><span class="sxs-lookup"><span data-stu-id="4cff7-145">**Name**: HTTP</span></span>
   * <span data-ttu-id="4cff7-146">**Protocollo**: TCP</span><span class="sxs-lookup"><span data-stu-id="4cff7-146">**Protocol**: TCP</span></span>
   * <span data-ttu-id="4cff7-147">**Porta pubblica**: 80</span><span class="sxs-lookup"><span data-stu-id="4cff7-147">**Public port**: 80</span></span>
   * <span data-ttu-id="4cff7-148">**Porta privata**: 3000</span><span class="sxs-lookup"><span data-stu-id="4cff7-148">**Private port**: 3000</span></span>
   * <span data-ttu-id="4cff7-149">**Indirizzo IP mobile**: Disabilitato</span><span class="sxs-lookup"><span data-stu-id="4cff7-149">**Floating PI address**: Disabled</span></span>
   * <span data-ttu-id="4cff7-150">**Elenco di controllo di accesso - ordine**: 1001, o in un altro valore che imposta la priorità hello della regola di accesso.</span><span class="sxs-lookup"><span data-stu-id="4cff7-150">**Access control list - Order**: 1001, or another value that sets hello priority of this access rule.</span></span>
   * <span data-ttu-id="4cff7-151">**Elenco di controllo di accesso - Nome**: allowHTTP</span><span class="sxs-lookup"><span data-stu-id="4cff7-151">**Access control list - Name**: allowHTTP</span></span>
   * <span data-ttu-id="4cff7-152">**Elenco di controllo di accesso - Azione**: consenti</span><span class="sxs-lookup"><span data-stu-id="4cff7-152">**Access control list - Action**: permit</span></span>
   * <span data-ttu-id="4cff7-153">**Elenco di controllo di accesso - Subnet remota**: 1.0.0.0/16</span><span class="sxs-lookup"><span data-stu-id="4cff7-153">**Access control list - Remote subnet**: 1.0.0.0/16</span></span>

     <span data-ttu-id="4cff7-154">Questo endpoint dispone di una porta pubblica 80 che indirizza il traffico toohello porta privata di 3000, in cui è in ascolto server Guide hello.</span><span class="sxs-lookup"><span data-stu-id="4cff7-154">This endpoint  has a public port of 80 that will route traffic toohello private port of 3000, where hello Rails server is listening.</span></span> <span data-ttu-id="4cff7-155">regola di elenco di controllo di accesso Hello consente il traffico pubblico sulla porta 80.</span><span class="sxs-lookup"><span data-stu-id="4cff7-155">hello access control list rule allows public traffic on port 80.</span></span>

     ![new-endpoint](./media/virtual-machines-linux-classic-ruby-rails-web-app/createendpoint.png)

5. <span data-ttu-id="4cff7-157">Fare clic su OK toosave hello endpoint.</span><span class="sxs-lookup"><span data-stu-id="4cff7-157">Click OK toosave hello endpoint.</span></span>

6. <span data-ttu-id="4cff7-158">Verrà visualizzato il messaggio **Salvataggio dell'endpoint della macchina virtuale**.</span><span class="sxs-lookup"><span data-stu-id="4cff7-158">A message should appear that states **Saving virtual machine endpoint**.</span></span> <span data-ttu-id="4cff7-159">Una volta che il messaggio scomparirà, endpoint hello è attiva.</span><span class="sxs-lookup"><span data-stu-id="4cff7-159">Once this message disappears, hello endpoint is active.</span></span> <span data-ttu-id="4cff7-160">È ora possibile testare l'applicazione passando il nome DNS toohello della macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="4cff7-160">You may now test your application by navigating toohello DNS name of your virtual machine.</span></span> <span data-ttu-id="4cff7-161">sito Web di Hello dovrebbe apparire simile toohello seguenti:</span><span class="sxs-lookup"><span data-stu-id="4cff7-161">hello website should appear similar toohello following:</span></span>

    ![Pagina predefinita Rails][default-rails-cloud]

## <a name="next-steps"></a><span data-ttu-id="4cff7-163">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="4cff7-163">Next steps</span></span>
<span data-ttu-id="4cff7-164">In questa esercitazione, si ha la maggior parte dei passaggi di hello manualmente.</span><span class="sxs-lookup"><span data-stu-id="4cff7-164">In this tutorial, you did most of hello steps manually.</span></span> <span data-ttu-id="4cff7-165">In un ambiente di produzione, è necessario scrivere la propria app in un computer di sviluppo e distribuirlo toohello macchina virtuale di Azure.</span><span class="sxs-lookup"><span data-stu-id="4cff7-165">In a production environment, you would write your app on a development machine and deploy it toohello Azure VM.</span></span> <span data-ttu-id="4cff7-166">Inoltre, la maggior parte degli ambienti di produzione ospitano un'applicazione hello Guide in combinazione con un altro processo server come Apache o NginX, che gestisce richieste routing toomultiple istanze di un'applicazione hello guide e serve risorse statiche.</span><span class="sxs-lookup"><span data-stu-id="4cff7-166">Also, most production environments host hello Rails application in conjunction with another server process such as Apache or NginX, which handles request routing toomultiple instances of hello Rails application and serving static resources.</span></span> <span data-ttu-id="4cff7-167">Per altre informazioni, vedere http://rubyonrails.org/deploy/.</span><span class="sxs-lookup"><span data-stu-id="4cff7-167">For more information, see http://rubyonrails.org/deploy/.</span></span>

<span data-ttu-id="4cff7-168">toolearn ulteriori informazioni su Ruby su Guide, visitare hello [Ruby le guide di Guide][rails-guides].</span><span class="sxs-lookup"><span data-stu-id="4cff7-168">toolearn more about Ruby on Rails, visit hello [Ruby on Rails Guides][rails-guides].</span></span>

<span data-ttu-id="4cff7-169">servizi di Azure toouse dall'applicazione Ruby, vedere:</span><span class="sxs-lookup"><span data-stu-id="4cff7-169">toouse Azure services from your Ruby application, see:</span></span>

* <span data-ttu-id="4cff7-170">[Archiviare dati non strutturati mediante BLOB][blobs]</span><span class="sxs-lookup"><span data-stu-id="4cff7-170">[Store unstructured data using blobs][blobs]</span></span>
* <span data-ttu-id="4cff7-171">[Archiviare coppie chiave-valore mediante tabelle][tables]</span><span class="sxs-lookup"><span data-stu-id="4cff7-171">[Store key/value pairs using tables][tables]</span></span>
* <span data-ttu-id="4cff7-172">[Fornire il contenuto di larghezza di banda elevata con hello Content Delivery Network][cdn-howto]</span><span class="sxs-lookup"><span data-stu-id="4cff7-172">[Serve high bandwidth content with hello Content Delivery Network][cdn-howto]</span></span>

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

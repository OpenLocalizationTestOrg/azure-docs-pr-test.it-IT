---
title: aaaHow toouse hello Azure slave plug-in con l'integrazione continua di Hudson | Documenti Microsoft
description: Viene descritto come slave toouse hello Azure plug-in con l'integrazione continua di Hudson.
services: virtual-machines-linux
documentationcenter: 
author: rmcmurray
manager: wpickett
editor: 
ms.assetid: b2083d1c-4de8-4a19-a615-ccc9d9b6e1d9
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-multiple
ms.devlang: java
ms.topic: article
ms.date: 04/25/2017
ms.author: robmcm
ms.openlocfilehash: cd6e67ad71c208aa56746aa8b70ba507da20bee9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-hello-azure-slave-plug-in-with-hudson-continuous-integration"></a><span data-ttu-id="d8cd8-103">Modalità slave toouse hello Azure plug-in con l'integrazione continua di Hudson</span><span class="sxs-lookup"><span data-stu-id="d8cd8-103">How toouse hello Azure slave plug-in with Hudson Continuous Integration</span></span>
<span data-ttu-id="d8cd8-104">in fase di compilazione in esecuzione distribuita, Hello Azure slave plug-in per Hudson consente tooprovision i nodi secondari in Azure.</span><span class="sxs-lookup"><span data-stu-id="d8cd8-104">hello Azure slave plug-in for Hudson enables you tooprovision slave nodes on Azure when running distributed builds.</span></span>

## <a name="install-hello-azure-slave-plug-in"></a><span data-ttu-id="d8cd8-105">Installare hello Azure Slave plug-in</span><span class="sxs-lookup"><span data-stu-id="d8cd8-105">Install hello Azure Slave plug-in</span></span>
1. <span data-ttu-id="d8cd8-106">Nel dashboard di Hudson hello, fare clic su **gestire Hudson**.</span><span class="sxs-lookup"><span data-stu-id="d8cd8-106">In hello Hudson dashboard, click **Manage Hudson**.</span></span>
2. <span data-ttu-id="d8cd8-107">In hello **gestire Hudson** pagina, fare clic su **gestire plug-in**.</span><span class="sxs-lookup"><span data-stu-id="d8cd8-107">In hello **Manage Hudson** page, click on **Manage Plugins**.</span></span>
3. <span data-ttu-id="d8cd8-108">Fare clic su hello **disponibile** scheda.</span><span class="sxs-lookup"><span data-stu-id="d8cd8-108">Click hello **Available** tab.</span></span>
4. <span data-ttu-id="d8cd8-109">Fare clic su **ricerca** e tipo **Azure** toolimit hello elenco toorelevant plug-in.</span><span class="sxs-lookup"><span data-stu-id="d8cd8-109">Click **Search** and type **Azure** toolimit hello list toorelevant plug-ins.</span></span>
   
    <span data-ttu-id="d8cd8-110">Se si sceglie tooscroll elenco hello di plug-in disponibili, si noterà hello Azure slave plug-in hello **distribuita di compilazione e gestione dei Cluster** sezione hello **altri** scheda.</span><span class="sxs-lookup"><span data-stu-id="d8cd8-110">If you opt tooscroll through hello list of available plug-ins, you will find hello Azure slave plug-in under hello **Cluster Management and Distributed Build** section in hello **Others** tab.</span></span>
5. <span data-ttu-id="d8cd8-111">Selezionare una casella di controllo hello **plug-in Azure Slave**.</span><span class="sxs-lookup"><span data-stu-id="d8cd8-111">Select hello checkbox for **Azure Slave Plugin**.</span></span>
6. <span data-ttu-id="d8cd8-112">Fare clic su **Installa**.</span><span class="sxs-lookup"><span data-stu-id="d8cd8-112">Click **Install**.</span></span>
7. <span data-ttu-id="d8cd8-113">Riavviare Hudson.</span><span class="sxs-lookup"><span data-stu-id="d8cd8-113">Restart Hudson.</span></span>

<span data-ttu-id="d8cd8-114">Ora è installato il plug-in hello, passaggi successivi hello sarebbe hello tooconfigure plug-in con il profilo di sottoscrizione di Azure e toocreate un modello che verrà utilizzato per la creazione di hello macchine Virtuali per nodo slave hello.</span><span class="sxs-lookup"><span data-stu-id="d8cd8-114">Now that hello plug-in is installed, hello next steps would be tooconfigure hello plug-in with your Azure subscription profile and toocreate a template that will be used in creating hello VM for hello slave node.</span></span>

## <a name="configure-hello-azure-slave-plug-in-with-your-subscription-profile"></a><span data-ttu-id="d8cd8-115">Configurare hello Azure Slave plug-in con il profilo di sottoscrizione</span><span class="sxs-lookup"><span data-stu-id="d8cd8-115">Configure hello Azure Slave plug-in with your subscription profile</span></span>
<span data-ttu-id="d8cd8-116">Un profilo di sottoscrizione, anche tooas cui le impostazioni di pubblicazione, è un file XML che contiene credenziali protette e informazioni aggiuntive, è necessario toowork con Azure nell'ambiente di sviluppo.</span><span class="sxs-lookup"><span data-stu-id="d8cd8-116">A subscription profile, also referred tooas publish settings, is an XML file that contains secure credentials and some additional information you'll need toowork with Azure in your development environment.</span></span> <span data-ttu-id="d8cd8-117">tooconfigure hello Azure slave plug-in, è necessario:</span><span class="sxs-lookup"><span data-stu-id="d8cd8-117">tooconfigure hello Azure slave plug-in, you need:</span></span>

* <span data-ttu-id="d8cd8-118">ID sottoscrizione personale</span><span class="sxs-lookup"><span data-stu-id="d8cd8-118">Your subscription id</span></span>
* <span data-ttu-id="d8cd8-119">Un certificato di gestione per la sottoscrizione</span><span class="sxs-lookup"><span data-stu-id="d8cd8-119">A management certificate for your subscription</span></span>

<span data-ttu-id="d8cd8-120">Questi elementi sono disponibili nel [profilo di sottoscrizione].</span><span class="sxs-lookup"><span data-stu-id="d8cd8-120">These can be found in your [subscription profile].</span></span> <span data-ttu-id="d8cd8-121">Di seguito è riportato un esempio di un profilo di sottoscrizione.</span><span class="sxs-lookup"><span data-stu-id="d8cd8-121">Below is an example of a subscription profile.</span></span>

    <?xml version="1.0" encoding="utf-8"?>

        <PublishData>

          <PublishProfile SchemaVersion="2.0" PublishMethod="AzureServiceManagementAPI">

        <Subscription

              ServiceManagementUrl="https://management.core.windows.net"

              Id="<Subscription ID>"

              Name="Pay-As-You-Go"
            ManagementCertificate="<Management certificate value>" />

          </PublishProfile>

    </PublishData>

<span data-ttu-id="d8cd8-122">Dopo aver creato il profilo di sottoscrizione, seguire questi hello tooconfigure passaggi Azure slave plug-in.</span><span class="sxs-lookup"><span data-stu-id="d8cd8-122">Once you have your subscription profile, follow these steps tooconfigure hello Azure slave plug-in.</span></span>

1. <span data-ttu-id="d8cd8-123">Nel dashboard di Hudson hello, fare clic su **gestire Hudson**.</span><span class="sxs-lookup"><span data-stu-id="d8cd8-123">In hello Hudson dashboard, click **Manage Hudson**.</span></span>
2. <span data-ttu-id="d8cd8-124">Fare clic su **Configure System**.</span><span class="sxs-lookup"><span data-stu-id="d8cd8-124">Click **Configure System**.</span></span>
3. <span data-ttu-id="d8cd8-125">Scorrere verso il basso hello di hello pagina toofind **Cloud** sezione.</span><span class="sxs-lookup"><span data-stu-id="d8cd8-125">Scroll down hello page toofind hello **Cloud** section.</span></span>
4. <span data-ttu-id="d8cd8-126">Fare clic su **Add new cloud > Microsoft Azure** (Aggiungi nuovo cloud > Microsoft Azure).</span><span class="sxs-lookup"><span data-stu-id="d8cd8-126">Click **Add new cloud > Microsoft Azure**.</span></span>
   
    ![aggiungere nuovo cloud][add new cloud]
   
    <span data-ttu-id="d8cd8-128">Campi hello in cui è necessario tooenter verranno visualizzati i dettagli della sottoscrizione.</span><span class="sxs-lookup"><span data-stu-id="d8cd8-128">This will show hello fields where you need tooenter your subscription details.</span></span>
   
    ![configurare profilo][configure profile]
5. <span data-ttu-id="d8cd8-130">Copiare i certificati di gestione e l'id sottoscrizione hello dal profilo di sottoscrizione e incollarli nei campi appropriati hello.</span><span class="sxs-lookup"><span data-stu-id="d8cd8-130">Copy hello subscription id and management certificate from your subscription profile and paste them in hello appropriate fields.</span></span>
   
    <span data-ttu-id="d8cd8-131">Quando si copia certificato di gestione e l'id di sottoscrizione hello, **non** includere hello virgolette che racchiudono i valori hello.</span><span class="sxs-lookup"><span data-stu-id="d8cd8-131">When copying hello subscription id and management certificate, **do not** include hello quotes that enclose hello values.</span></span>
6. <span data-ttu-id="d8cd8-132">Fare clic su **Verify configuration**.</span><span class="sxs-lookup"><span data-stu-id="d8cd8-132">Click on **Verify configuration**.</span></span>
7. <span data-ttu-id="d8cd8-133">Quando si verifica configurazione hello correttamente, fare clic su **salvare**.</span><span class="sxs-lookup"><span data-stu-id="d8cd8-133">When hello configuration is verified successfully, click **Save**.</span></span>

## <a name="set-up-a-virtual-machine-template-for-hello-azure-slave-plug-in"></a><span data-ttu-id="d8cd8-134">Impostare un modello di macchina virtuale per hello Azure Slave plug-in</span><span class="sxs-lookup"><span data-stu-id="d8cd8-134">Set up a virtual machine template for hello Azure Slave plug-in</span></span>
<span data-ttu-id="d8cd8-135">Un modello di macchina virtuale definisce i parametri di hello hello plug-in userà toocreate un nodo secondario in Azure.</span><span class="sxs-lookup"><span data-stu-id="d8cd8-135">A virtual machine template defines hello parameters hello plug-in will use toocreate a slave node on Azure.</span></span> <span data-ttu-id="d8cd8-136">In hello alla procedura seguente si sarà creazione modello per una VM Ubuntu.</span><span class="sxs-lookup"><span data-stu-id="d8cd8-136">In hello following steps we'll be creating template for an Ubuntu VM.</span></span>

1. <span data-ttu-id="d8cd8-137">Nel dashboard di Hudson hello, fare clic su **gestire Hudson**.</span><span class="sxs-lookup"><span data-stu-id="d8cd8-137">In hello Hudson dashboard, click **Manage Hudson**.</span></span>
2. <span data-ttu-id="d8cd8-138">Fare clic su **Configure System**.</span><span class="sxs-lookup"><span data-stu-id="d8cd8-138">Click on **Configure System**.</span></span>
3. <span data-ttu-id="d8cd8-139">Scorrere verso il basso hello di hello pagina toofind **Cloud** sezione.</span><span class="sxs-lookup"><span data-stu-id="d8cd8-139">Scroll down hello page toofind hello **Cloud** section.</span></span>
4. <span data-ttu-id="d8cd8-140">All'interno di hello **Cloud** sezione, trovare **aggiungere modello di macchina virtuale di Azure** e fare clic su hello **Aggiungi** pulsante.</span><span class="sxs-lookup"><span data-stu-id="d8cd8-140">Within hello **Cloud** section, find **Add Azure Virtual Machine Template** and click hello **Add** button.</span></span>
   
    ![aggiungere modello macchina virtuale][add vm template]
5. <span data-ttu-id="d8cd8-142">Specificare un nome di servizio cloud in hello **nome** campo.</span><span class="sxs-lookup"><span data-stu-id="d8cd8-142">Specify a cloud service name in hello **Name** field.</span></span> <span data-ttu-id="d8cd8-143">Se nome hello specificato fa riferimento tooan servizio cloud esistente, verrà eseguito il provisioning hello VM in quel servizio.</span><span class="sxs-lookup"><span data-stu-id="d8cd8-143">If hello name you specify refers tooan existing cloud service, hello VM will be provisioned in that service.</span></span> <span data-ttu-id="d8cd8-144">In caso contrario, Azure ne creerà uno nuovo.</span><span class="sxs-lookup"><span data-stu-id="d8cd8-144">Otherwise, Azure will create a new one.</span></span>
6. <span data-ttu-id="d8cd8-145">In hello **descrizione** immettere testo che descrive il modello di hello si sta creando.</span><span class="sxs-lookup"><span data-stu-id="d8cd8-145">In hello **Description** field, enter text that describes hello template you are creating.</span></span> <span data-ttu-id="d8cd8-146">Queste informazioni sono esclusivamente a scopo di documentazione e non vengono utilizzate nel provisioning di una macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="d8cd8-146">This information is only for documentary purposes and is not used in provisioning a VM.</span></span>
7. <span data-ttu-id="d8cd8-147">In hello **etichette** immettere **linux**.</span><span class="sxs-lookup"><span data-stu-id="d8cd8-147">In hello **Labels** field, enter **linux**.</span></span> <span data-ttu-id="d8cd8-148">Questa etichetta modello hello tooidentify usato che si sta creando e modello hello tooreference successivamente utilizzati durante la creazione di un processo Hudson.</span><span class="sxs-lookup"><span data-stu-id="d8cd8-148">This label is used tooidentify hello template you are creating and is subsequently used tooreference hello template when creating a Hudson job.</span></span>
8. <span data-ttu-id="d8cd8-149">Selezionare un'area in cui verrà creato hello macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="d8cd8-149">Select a region where hello VM will be created.</span></span>
9. <span data-ttu-id="d8cd8-150">Selezionare dimensioni della macchina virtuale appropriata hello.</span><span class="sxs-lookup"><span data-stu-id="d8cd8-150">Select hello appropriate VM size.</span></span>
10. <span data-ttu-id="d8cd8-151">Specificare un account di archiviazione in cui verrà creato hello macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="d8cd8-151">Specify a storage account where hello VM will be created.</span></span> <span data-ttu-id="d8cd8-152">Assicurarsi che sia in hello stessa area hello del servizio cloud che verranno utilizzati.</span><span class="sxs-lookup"><span data-stu-id="d8cd8-152">Make sure that it is in hello same region as hello cloud service you'll be using.</span></span> <span data-ttu-id="d8cd8-153">Se si desidera creare nuovo toobe di archiviazione, è possibile lasciare vuoto questo campo.</span><span class="sxs-lookup"><span data-stu-id="d8cd8-153">If you want new storage toobe created, you can leave this field blank.</span></span>
11. <span data-ttu-id="d8cd8-154">Periodo di conservazione hello numero di minuti prima dell'eliminazione di un secondario inattivo Hudson.</span><span class="sxs-lookup"><span data-stu-id="d8cd8-154">Retention time specifies hello number of minutes before Hudson deletes an idle slave.</span></span> <span data-ttu-id="d8cd8-155">Mantenere questa hello valore predefinito di 60.</span><span class="sxs-lookup"><span data-stu-id="d8cd8-155">Leave this at hello default value of 60.</span></span>
12. <span data-ttu-id="d8cd8-156">In **utilizzo**, selezionare hello condizione appropriata quando verrà utilizzato questo nodo secondario.</span><span class="sxs-lookup"><span data-stu-id="d8cd8-156">In **Usage**, select hello appropriate condition when this slave node will be used.</span></span> <span data-ttu-id="d8cd8-157">Per il momento, selezionare **Utilize this node as much as possible**.</span><span class="sxs-lookup"><span data-stu-id="d8cd8-157">For now, select **Utilize this node as much as possible**.</span></span>
    
     <span data-ttu-id="d8cd8-158">A questo punto, il modulo avrà un aspetto simile toothis:</span><span class="sxs-lookup"><span data-stu-id="d8cd8-158">At this point, your form would look somewhat similar toothis:</span></span>
    
     ![configurazione modello][template config]
13. <span data-ttu-id="d8cd8-160">In **famiglia di immagine o Id** è toospecify quale immagine del sistema verrà installato nella macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="d8cd8-160">In **Image Family or Id** you have toospecify what system image will be installed on your VM.</span></span> <span data-ttu-id="d8cd8-161">È possibile scegliere da un elenco di famiglie di immagini o specificare un'immagine personalizzata.</span><span class="sxs-lookup"><span data-stu-id="d8cd8-161">You can either select from a list of image families or specify a custom image.</span></span>
    
     <span data-ttu-id="d8cd8-162">Se si desidera tooselect da un elenco delle famiglie di immagine, immettere hello primo carattere (maiuscole/minuscole) del nome della famiglia hello immagine.</span><span class="sxs-lookup"><span data-stu-id="d8cd8-162">If you want tooselect from a list of image families, enter hello first character (case-sensitive) of hello image family name.</span></span> <span data-ttu-id="d8cd8-163">Ad esempio, digitando **U** verrà visualizzato l'elenco delle famiglie di Ubuntu Server.</span><span class="sxs-lookup"><span data-stu-id="d8cd8-163">For instance, typing **U** will bring up a list of Ubuntu Server families.</span></span> <span data-ttu-id="d8cd8-164">Dopo aver selezionato dall'elenco di hello, Jenkins utilizzerà più recente di tale immagine del sistema da tale gruppo hello durante il provisioning di una macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="d8cd8-164">Once you select from hello list, Jenkins will use hello latest version of that system image from that family when provisioning your VM.</span></span>
    
     ![elenco famiglie sistemi operativi][OS family list]
    
     <span data-ttu-id="d8cd8-166">Se si dispone di un'immagine personalizzata che si desidera invece toouse, immettere il nome di hello di tale immagine personalizzata.</span><span class="sxs-lookup"><span data-stu-id="d8cd8-166">If you have a custom image that you want toouse instead, enter hello name of that custom image.</span></span> <span data-ttu-id="d8cd8-167">I nomi delle immagini personalizzate non vengono visualizzati in un elenco in modo che sia tooensure che hello nome sia stato immesso correttamente.</span><span class="sxs-lookup"><span data-stu-id="d8cd8-167">Custom image names are not shown in a list so you have tooensure that hello name is entered correctly.</span></span>    
    
     <span data-ttu-id="d8cd8-168">Per questa esercitazione, digitare **U** toobring un elenco di immagini Ubuntu e selezionare **Ubuntu Server 14.04 LTS**.</span><span class="sxs-lookup"><span data-stu-id="d8cd8-168">For this tutorial, type **U** toobring up a list of Ubuntu images and select **Ubuntu Server 14.04 LTS**.</span></span>
14. <span data-ttu-id="d8cd8-169">Per **Launch method** (Metodo di avvio), selezionare **SSH**.</span><span class="sxs-lookup"><span data-stu-id="d8cd8-169">For **Launch method**, select **SSH**.</span></span>
15. <span data-ttu-id="d8cd8-170">Script hello seguente di copia e Incolla in hello **Init script** campo.</span><span class="sxs-lookup"><span data-stu-id="d8cd8-170">Copy hello script below and paste in hello **Init script** field.</span></span>
    
         # Install Java
    
         sudo apt-get -y update
    
         sudo apt-get install -y openjdk-7-jdk
    
         sudo apt-get -y update --fix-missing
    
         sudo apt-get install -y openjdk-7-jdk
    
         # Install git
    
         sudo apt-get install -y git
    
         #Install ant
    
         sudo apt-get install -y ant
    
         sudo apt-get -y update --fix-missing
    
         sudo apt-get install -y ant
    
     <span data-ttu-id="d8cd8-171">Hello **Init script** verrà eseguito dopo la creazione della macchina virtuale hello.</span><span class="sxs-lookup"><span data-stu-id="d8cd8-171">hello **Init script** will be executed after hello VM is created.</span></span> <span data-ttu-id="d8cd8-172">In questo esempio, script hello installa ant Java e git.</span><span class="sxs-lookup"><span data-stu-id="d8cd8-172">In this example, hello script installs Java, git, and ant.</span></span>
16. <span data-ttu-id="d8cd8-173">In hello **Username** e **Password** campi, immettere i valori preferiti per l'account amministratore hello che verrà creato nella macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="d8cd8-173">In hello **Username** and **Password** fields, enter your preferred values for hello administrator account that will be created on your VM.</span></span>
17. <span data-ttu-id="d8cd8-174">Fare clic su **verificare modello** toocheck se i parametri di hello specificati sono validi.</span><span class="sxs-lookup"><span data-stu-id="d8cd8-174">Click on **Verify Template** toocheck if hello parameters you specified are valid.</span></span>
18. <span data-ttu-id="d8cd8-175">Fare clic su **Save**.</span><span class="sxs-lookup"><span data-stu-id="d8cd8-175">Click on **Save**.</span></span>

## <a name="create-a-hudson-job-that-runs-on-a-slave-node-on-azure"></a><span data-ttu-id="d8cd8-176">Creare un processo Hudson eseguito in un nodo slave in Azure</span><span class="sxs-lookup"><span data-stu-id="d8cd8-176">Create a Hudson job that runs on a slave node on Azure</span></span>
<span data-ttu-id="d8cd8-177">In questa sezione si creerà un'attività di Hudson che verrà eseguita in un nodo slave in Azure.</span><span class="sxs-lookup"><span data-stu-id="d8cd8-177">In this section, you'll be creating a Hudson task that will run on a slave node on Azure.</span></span>

1. <span data-ttu-id="d8cd8-178">Nel dashboard di Hudson hello, fare clic su **nuovo processo**.</span><span class="sxs-lookup"><span data-stu-id="d8cd8-178">In hello Hudson dashboard, click **New Job**.</span></span>
2. <span data-ttu-id="d8cd8-179">Immettere un nome per il processo di hello che si sta creando.</span><span class="sxs-lookup"><span data-stu-id="d8cd8-179">Enter a name for hello job you are creating.</span></span>
3. <span data-ttu-id="d8cd8-180">Tipo di processo hello selezionare **compilazione di un processo software stile liberare**.</span><span class="sxs-lookup"><span data-stu-id="d8cd8-180">For hello job type, select **Build a free-style software job**.</span></span>
4. <span data-ttu-id="d8cd8-181">Fare clic su **OK**.</span><span class="sxs-lookup"><span data-stu-id="d8cd8-181">Click **OK**.</span></span>
5. <span data-ttu-id="d8cd8-182">Nella pagina di configurazione processo hello, selezionare **limita l'accesso in cui è possibile eseguire questo progetto**.</span><span class="sxs-lookup"><span data-stu-id="d8cd8-182">In hello job configuration page, select **Restrict where this project can be run**.</span></span>
6. <span data-ttu-id="d8cd8-183">Selezionare **nodo e l'etichetta del menu** e selezionare **linux** (è specificata questa etichetta quando si crea il modello di macchina virtuale hello nella sezione precedente hello).</span><span class="sxs-lookup"><span data-stu-id="d8cd8-183">Select **Node and label menu** and select **linux** (we specified this label when creating hello virtual machine template in hello previous section).</span></span>
7. <span data-ttu-id="d8cd8-184">In hello **compilare** fare clic su **istruzione di compilazione Aggiungi** e selezionare **eseguire shell**.</span><span class="sxs-lookup"><span data-stu-id="d8cd8-184">In hello **Build** section, click **Add build step** and select **Execute shell**.</span></span>
8. <span data-ttu-id="d8cd8-185">Modificare lo script seguente, la sostituzione di hello **{nome account github}**, **{nome del progetto}**, e **{directory del progetto}** con valori appropriati e incollare hello modificare uno script nell'area di testo hello che viene visualizzato.</span><span class="sxs-lookup"><span data-stu-id="d8cd8-185">Edit hello following script, replacing **{your github account name}**, **{your project name}**, and **{your project directory}** with appropriate values, and paste hello edited script in hello text area that appears.</span></span>
   
        # Clone from git repo
   
        currentDir="$PWD"
   
        if [ -e {your project directory} ]; then
   
              cd {your project directory}
   
              git pull origin master
   
        else
   
              git clone https://github.com/{your github account name}/{your project name}.git
   
        fi
   
        # change directory tooproject
   
        cd $currentDir/{your project directory}
   
        #Execute build task
   
        ant
9. <span data-ttu-id="d8cd8-186">Fare clic su **Save**.</span><span class="sxs-lookup"><span data-stu-id="d8cd8-186">Click on **Save**.</span></span>
10. <span data-ttu-id="d8cd8-187">In dashboard Hudson hello, trovare il processo di hello appena creato e fare clic su hello **pianificare una compilazione** icona.</span><span class="sxs-lookup"><span data-stu-id="d8cd8-187">In hello Hudson dashboard, find hello job you just created and click on hello **Schedule a build** icon.</span></span>

<span data-ttu-id="d8cd8-188">Hudson verrà quindi creare un nodo secondario utilizzando il modello di hello creato nella sezione precedente hello e hello script specificato in fase di compilazione hello per questa attività.</span><span class="sxs-lookup"><span data-stu-id="d8cd8-188">Hudson will then create a slave node using hello template created in hello previous section and execute hello script you specified in hello build step for this task.</span></span>

## <a name="next-steps"></a><span data-ttu-id="d8cd8-189">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="d8cd8-189">Next Steps</span></span>
<span data-ttu-id="d8cd8-190">Per ulteriori informazioni sull'uso di Azure con Java, vedere hello [Centro per sviluppatori Java di Azure].</span><span class="sxs-lookup"><span data-stu-id="d8cd8-190">For more information about using Azure with Java, see hello [Azure Java Developer Center].</span></span>

<!-- URL List -->

[Centro per sviluppatori Java di Azure]: https://azure.microsoft.com/develop/java/
[profilo di sottoscrizione]: http://go.microsoft.com/fwlink/?LinkID=396395

<!-- IMG List -->

[add new cloud]: ./media/virtual-machines-azure-slave-plugin-for-hudson/hudson-setup-addcloud.png
[configure profile]: ./media/virtual-machines-azure-slave-plugin-for-hudson/hudson-setup-configureprofile.png
[add vm template]: ./media/virtual-machines-azure-slave-plugin-for-hudson/hudson-setup-addnewvmtemplate.png
[template config]: ./media/virtual-machines-azure-slave-plugin-for-hudson/hudson-setup-templateconfig1-withdata.png
[OS family list]: ./media/virtual-machines-azure-slave-plugin-for-hudson/hudson-oslist.png


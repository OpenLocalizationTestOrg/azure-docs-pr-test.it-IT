---
title: Come usare il plug-in slave di Azure con una soluzione di integrazione continua Hudson | Microsoft Docs
description: Descrive come usare il plug-in slave di Azure con una soluzione di integrazione continua Hudson
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
ms.openlocfilehash: c11b59f8ea432075b147a391de4b7bd3331e639e
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="how-to-use-the-azure-slave-plug-in-with-hudson-continuous-integration"></a><span data-ttu-id="16f4d-103">Come usare il plug-in slave di Azure con una soluzione di integrazione continua Hudson</span><span class="sxs-lookup"><span data-stu-id="16f4d-103">How to use the Azure slave plug-in with Hudson Continuous Integration</span></span>
<span data-ttu-id="16f4d-104">Il plug-in slave di Azure per Hudson consente di eseguire il provisioning di nodi slave in Azure quando si eseguono build distribuite.</span><span class="sxs-lookup"><span data-stu-id="16f4d-104">The Azure slave plug-in for Hudson enables you to provision slave nodes on Azure when running distributed builds.</span></span>

## <a name="install-the-azure-slave-plug-in"></a><span data-ttu-id="16f4d-105">Installare il plug-in slave di Azure</span><span class="sxs-lookup"><span data-stu-id="16f4d-105">Install the Azure Slave plug-in</span></span>
1. <span data-ttu-id="16f4d-106">Nel dashboard di Hudson, fare clic su **Manage Hudson**.</span><span class="sxs-lookup"><span data-stu-id="16f4d-106">In the Hudson dashboard, click **Manage Hudson**.</span></span>
2. <span data-ttu-id="16f4d-107">Nella pagina **Manage Hudson** (Gestisci Hudson) fare clic su **Manage Plugins** (Gestisci plug-in).</span><span class="sxs-lookup"><span data-stu-id="16f4d-107">In the **Manage Hudson** page, click on **Manage Plugins**.</span></span>
3. <span data-ttu-id="16f4d-108">Fare clic sulla scheda **Available** .</span><span class="sxs-lookup"><span data-stu-id="16f4d-108">Click the **Available** tab.</span></span>
4. <span data-ttu-id="16f4d-109">Fare clic su **Search** (Cerca) e digitare **Azure** per limitare l'elenco ai plug-in pertinenti.</span><span class="sxs-lookup"><span data-stu-id="16f4d-109">Click **Search** and type **Azure** to limit the list to relevant plug-ins.</span></span>
   
    <span data-ttu-id="16f4d-110">Se si decide di scorrere l'elenco di plug-in disponibili, si troverà il plug-in slave di Azure nella sezione **Cluster Management and Distributed Build** (Gestione cluster e compilazione distribuita) nella scheda **Others** (Altri).</span><span class="sxs-lookup"><span data-stu-id="16f4d-110">If you opt to scroll through the list of available plug-ins, you will find the Azure slave plug-in under the **Cluster Management and Distributed Build** section in the **Others** tab.</span></span>
5. <span data-ttu-id="16f4d-111">Selezionare la casella di controllo **Azure Slave Plugin**.</span><span class="sxs-lookup"><span data-stu-id="16f4d-111">Select the checkbox for **Azure Slave Plugin**.</span></span>
6. <span data-ttu-id="16f4d-112">Fare clic su **Installa**.</span><span class="sxs-lookup"><span data-stu-id="16f4d-112">Click **Install**.</span></span>
7. <span data-ttu-id="16f4d-113">Riavviare Hudson.</span><span class="sxs-lookup"><span data-stu-id="16f4d-113">Restart Hudson.</span></span>

<span data-ttu-id="16f4d-114">Dopo aver installato il plug-in, è necessario procedere alla relativa configurazione tramite il profilo della sottoscrizione di Azure e alla creazione di un modello che verrà usato durante la creazione della VM relativa al nodo slave.</span><span class="sxs-lookup"><span data-stu-id="16f4d-114">Now that the plug-in is installed, the next steps would be to configure the plug-in with your Azure subscription profile and to create a template that will be used in creating the VM for the slave node.</span></span>

## <a name="configure-the-azure-slave-plug-in-with-your-subscription-profile"></a><span data-ttu-id="16f4d-115">Configurare il plug-in slave di Azure con il profilo di sottoscrizione</span><span class="sxs-lookup"><span data-stu-id="16f4d-115">Configure the Azure Slave plug-in with your subscription profile</span></span>
<span data-ttu-id="16f4d-116">Un profilo di sottoscrizione, noto anche come impostazioni di pubblicazione, è un file XML contenente le credenziali protette e alcune informazioni aggiuntive necessarie per usare Azure nel proprio ambiente di sviluppo.</span><span class="sxs-lookup"><span data-stu-id="16f4d-116">A subscription profile, also referred to as publish settings, is an XML file that contains secure credentials and some additional information you'll need to work with Azure in your development environment.</span></span> <span data-ttu-id="16f4d-117">Per configurare il plug-in slave di Azure, è necessario quanto segue:</span><span class="sxs-lookup"><span data-stu-id="16f4d-117">To configure the Azure slave plug-in, you need:</span></span>

* <span data-ttu-id="16f4d-118">ID sottoscrizione personale</span><span class="sxs-lookup"><span data-stu-id="16f4d-118">Your subscription id</span></span>
* <span data-ttu-id="16f4d-119">Un certificato di gestione per la sottoscrizione</span><span class="sxs-lookup"><span data-stu-id="16f4d-119">A management certificate for your subscription</span></span>

<span data-ttu-id="16f4d-120">Questi elementi sono disponibili nel [profilo di sottoscrizione].</span><span class="sxs-lookup"><span data-stu-id="16f4d-120">These can be found in your [subscription profile].</span></span> <span data-ttu-id="16f4d-121">Di seguito è riportato un esempio di un profilo di sottoscrizione.</span><span class="sxs-lookup"><span data-stu-id="16f4d-121">Below is an example of a subscription profile.</span></span>

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

<span data-ttu-id="16f4d-122">Dopo avere creato il profilo di sottoscrizione, attenersi alla seguente procedura per configurare il plug-in slave di Azure.</span><span class="sxs-lookup"><span data-stu-id="16f4d-122">Once you have your subscription profile, follow these steps to configure the Azure slave plug-in.</span></span>

1. <span data-ttu-id="16f4d-123">Nel dashboard di Hudson, fare clic su **Manage Hudson**.</span><span class="sxs-lookup"><span data-stu-id="16f4d-123">In the Hudson dashboard, click **Manage Hudson**.</span></span>
2. <span data-ttu-id="16f4d-124">Fare clic su **Configure System**.</span><span class="sxs-lookup"><span data-stu-id="16f4d-124">Click **Configure System**.</span></span>
3. <span data-ttu-id="16f4d-125">Scorrere verso il basso la pagina per trovare la sezione **Cloud** .</span><span class="sxs-lookup"><span data-stu-id="16f4d-125">Scroll down the page to find the **Cloud** section.</span></span>
4. <span data-ttu-id="16f4d-126">Fare clic su **Add new cloud > Microsoft Azure** (Aggiungi nuovo cloud > Microsoft Azure).</span><span class="sxs-lookup"><span data-stu-id="16f4d-126">Click **Add new cloud > Microsoft Azure**.</span></span>
   
    ![aggiungere nuovo cloud][add new cloud]
   
    <span data-ttu-id="16f4d-128">Verranno visualizzati i campi in cui è necessario immettere i dettagli della sottoscrizione.</span><span class="sxs-lookup"><span data-stu-id="16f4d-128">This will show the fields where you need to enter your subscription details.</span></span>
   
    ![configurare profilo][configure profile]
5. <span data-ttu-id="16f4d-130">Copiare l'ID sottoscrizione e il certificato di gestione dal profilo di sottoscrizione e incollarli nei campi appropriati.</span><span class="sxs-lookup"><span data-stu-id="16f4d-130">Copy the subscription id and management certificate from your subscription profile and paste them in the appropriate fields.</span></span>
   
    <span data-ttu-id="16f4d-131">Quando si copiano l'ID sottoscrizione e il certificato di gestione, **non** includere le virgolette che racchiudono i valori.</span><span class="sxs-lookup"><span data-stu-id="16f4d-131">When copying the subscription id and management certificate, **do not** include the quotes that enclose the values.</span></span>
6. <span data-ttu-id="16f4d-132">Fare clic su **Verify configuration**.</span><span class="sxs-lookup"><span data-stu-id="16f4d-132">Click on **Verify configuration**.</span></span>
7. <span data-ttu-id="16f4d-133">Quando la configurazione viene verificata correttamente, fare clic su **Save**.</span><span class="sxs-lookup"><span data-stu-id="16f4d-133">When the configuration is verified successfully, click **Save**.</span></span>

## <a name="set-up-a-virtual-machine-template-for-the-azure-slave-plug-in"></a><span data-ttu-id="16f4d-134">Configurare un modello di macchina virtuale per il plug-in slave di Azure</span><span class="sxs-lookup"><span data-stu-id="16f4d-134">Set up a virtual machine template for the Azure Slave plug-in</span></span>
<span data-ttu-id="16f4d-135">Un modello di macchina virtuale definisce i parametri che il plug-in userà per creare un nodo slave in Azure.</span><span class="sxs-lookup"><span data-stu-id="16f4d-135">A virtual machine template defines the parameters the plug-in will use to create a slave node on Azure.</span></span> <span data-ttu-id="16f4d-136">Nella procedura seguente verrà creato un modello per una macchina virtuale Ubuntu.</span><span class="sxs-lookup"><span data-stu-id="16f4d-136">In the following steps we'll be creating template for an Ubuntu VM.</span></span>

1. <span data-ttu-id="16f4d-137">Nel dashboard di Hudson, fare clic su **Manage Hudson**.</span><span class="sxs-lookup"><span data-stu-id="16f4d-137">In the Hudson dashboard, click **Manage Hudson**.</span></span>
2. <span data-ttu-id="16f4d-138">Fare clic su **Configure System**.</span><span class="sxs-lookup"><span data-stu-id="16f4d-138">Click on **Configure System**.</span></span>
3. <span data-ttu-id="16f4d-139">Scorrere verso il basso la pagina per trovare la sezione **Cloud** .</span><span class="sxs-lookup"><span data-stu-id="16f4d-139">Scroll down the page to find the **Cloud** section.</span></span>
4. <span data-ttu-id="16f4d-140">All'interno della sezione **Cloud**, trovare **Add Azure Virtual Machine Template** (Aggiungere modello di macchina virtuale Azure) e fare clic sul pulsante **Add** (Aggiungi).</span><span class="sxs-lookup"><span data-stu-id="16f4d-140">Within the **Cloud** section, find **Add Azure Virtual Machine Template** and click the **Add** button.</span></span>
   
    ![aggiungere modello macchina virtuale][add vm template]
5. <span data-ttu-id="16f4d-142">Specificare un nome del servizio cloud nel campo **Name** .</span><span class="sxs-lookup"><span data-stu-id="16f4d-142">Specify a cloud service name in the **Name** field.</span></span> <span data-ttu-id="16f4d-143">Se il nome specificato fa riferimento a un servizio cloud esistente, il provisioning della macchina virtuale verrà effettuato in tale servizio.</span><span class="sxs-lookup"><span data-stu-id="16f4d-143">If the name you specify refers to an existing cloud service, the VM will be provisioned in that service.</span></span> <span data-ttu-id="16f4d-144">In caso contrario, Azure ne creerà uno nuovo.</span><span class="sxs-lookup"><span data-stu-id="16f4d-144">Otherwise, Azure will create a new one.</span></span>
6. <span data-ttu-id="16f4d-145">Nel campo **Description** , immettere il testo che descrive il modello che si sta creando.</span><span class="sxs-lookup"><span data-stu-id="16f4d-145">In the **Description** field, enter text that describes the template you are creating.</span></span> <span data-ttu-id="16f4d-146">Queste informazioni sono esclusivamente a scopo di documentazione e non vengono utilizzate nel provisioning di una macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="16f4d-146">This information is only for documentary purposes and is not used in provisioning a VM.</span></span>
7. <span data-ttu-id="16f4d-147">Nel campo **Labels** (Etichette) immettere **linux**.</span><span class="sxs-lookup"><span data-stu-id="16f4d-147">In the **Labels** field, enter **linux**.</span></span> <span data-ttu-id="16f4d-148">Questa etichetta viene utilizzata per identificare il modello che si sta creando e viene successivamente utilizzata per fare riferimento al modello durante la creazione di un processo Hudson.</span><span class="sxs-lookup"><span data-stu-id="16f4d-148">This label is used to identify the template you are creating and is subsequently used to reference the template when creating a Hudson job.</span></span>
8. <span data-ttu-id="16f4d-149">Selezionare un'area in cui verrà creata la macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="16f4d-149">Select a region where the VM will be created.</span></span>
9. <span data-ttu-id="16f4d-150">Selezionare le dimensioni appropriate della macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="16f4d-150">Select the appropriate VM size.</span></span>
10. <span data-ttu-id="16f4d-151">Specificare un account di archiviazione in cui verrà creata la macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="16f4d-151">Specify a storage account where the VM will be created.</span></span> <span data-ttu-id="16f4d-152">Assicurarsi che l'account si trovi nella stessa area del servizio cloud che verrà utilizzato.</span><span class="sxs-lookup"><span data-stu-id="16f4d-152">Make sure that it is in the same region as the cloud service you'll be using.</span></span> <span data-ttu-id="16f4d-153">Per creare una nuova risorsa di archiviazione, lasciare questo campo vuoto.</span><span class="sxs-lookup"><span data-stu-id="16f4d-153">If you want new storage to be created, you can leave this field blank.</span></span>
11. <span data-ttu-id="16f4d-154">Il periodo di memorizzazione specifica il numero di minuti prima dell'eliminazione di uno slave inattivo da parte di Hudson.</span><span class="sxs-lookup"><span data-stu-id="16f4d-154">Retention time specifies the number of minutes before Hudson deletes an idle slave.</span></span> <span data-ttu-id="16f4d-155">Lasciare il valore predefinito pari a 60.</span><span class="sxs-lookup"><span data-stu-id="16f4d-155">Leave this at the default value of 60.</span></span>
12. <span data-ttu-id="16f4d-156">In **Usage**, selezionare la condizione appropriata quando verrà utilizzato questo nodo slave.</span><span class="sxs-lookup"><span data-stu-id="16f4d-156">In **Usage**, select the appropriate condition when this slave node will be used.</span></span> <span data-ttu-id="16f4d-157">Per il momento, selezionare **Utilize this node as much as possible**.</span><span class="sxs-lookup"><span data-stu-id="16f4d-157">For now, select **Utilize this node as much as possible**.</span></span>
    
     <span data-ttu-id="16f4d-158">A questo punto, il modulo dovrebbe avere un aspetto simile al seguente:</span><span class="sxs-lookup"><span data-stu-id="16f4d-158">At this point, your form would look somewhat similar to this:</span></span>
    
     ![configurazione modello][template config]
13. <span data-ttu-id="16f4d-160">In **Image Family or Id** è necessario specificare quale immagine del sistema verrà installata nella macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="16f4d-160">In **Image Family or Id** you have to specify what system image will be installed on your VM.</span></span> <span data-ttu-id="16f4d-161">È possibile scegliere da un elenco di famiglie di immagini o specificare un'immagine personalizzata.</span><span class="sxs-lookup"><span data-stu-id="16f4d-161">You can either select from a list of image families or specify a custom image.</span></span>
    
     <span data-ttu-id="16f4d-162">Per selezionare da un elenco di famiglie di immagini, immettere il primo carattere (maiuscole/minuscole) del nome della famiglia dell'immagine.</span><span class="sxs-lookup"><span data-stu-id="16f4d-162">If you want to select from a list of image families, enter the first character (case-sensitive) of the image family name.</span></span> <span data-ttu-id="16f4d-163">Ad esempio, digitando **U** verrà visualizzato l'elenco delle famiglie di Ubuntu Server.</span><span class="sxs-lookup"><span data-stu-id="16f4d-163">For instance, typing **U** will bring up a list of Ubuntu Server families.</span></span> <span data-ttu-id="16f4d-164">Dopo aver selezionato dall'elenco, Jenkins utilizzerà la versione più recente di tale immagine del sistema di tale famiglia durante il provisioning della macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="16f4d-164">Once you select from the list, Jenkins will use the latest version of that system image from that family when provisioning your VM.</span></span>
    
     ![elenco famiglie sistemi operativi][OS family list]
    
     <span data-ttu-id="16f4d-166">Se invece si dispone di un'immagine personalizzata che si desidera utilizzare, immettere il nome dell'immagine personalizzata.</span><span class="sxs-lookup"><span data-stu-id="16f4d-166">If you have a custom image that you want to use instead, enter the name of that custom image.</span></span> <span data-ttu-id="16f4d-167">I nomi delle immagini personalizzati non vengono visualizzati nell'elenco, pertanto è necessario verificare che il nome venga immesso correttamente.</span><span class="sxs-lookup"><span data-stu-id="16f4d-167">Custom image names are not shown in a list so you have to ensure that the name is entered correctly.</span></span>    
    
     <span data-ttu-id="16f4d-168">Per questa esercitazione, digitare **U** per visualizzare un elenco di immagini Ubuntu e selezionare **Ubuntu Server 14.04 LTS**.</span><span class="sxs-lookup"><span data-stu-id="16f4d-168">For this tutorial, type **U** to bring up a list of Ubuntu images and select **Ubuntu Server 14.04 LTS**.</span></span>
14. <span data-ttu-id="16f4d-169">Per **Launch method** (Metodo di avvio), selezionare **SSH**.</span><span class="sxs-lookup"><span data-stu-id="16f4d-169">For **Launch method**, select **SSH**.</span></span>
15. <span data-ttu-id="16f4d-170">Copiare lo script seguente e incollarlo nel campo **Init script** .</span><span class="sxs-lookup"><span data-stu-id="16f4d-170">Copy the script below and paste in the **Init script** field.</span></span>
    
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
    
     <span data-ttu-id="16f4d-171">L' **Init script** verrà eseguito dopo aver creato la macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="16f4d-171">The **Init script** will be executed after the VM is created.</span></span> <span data-ttu-id="16f4d-172">In questo esempio, lo script installa Java, git e ant.</span><span class="sxs-lookup"><span data-stu-id="16f4d-172">In this example, the script installs Java, git, and ant.</span></span>
16. <span data-ttu-id="16f4d-173">Nei campi **Username** (Nome utente) e **Password** immettere i valori preferiti relativi all'account amministratore che verrà creato nella macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="16f4d-173">In the **Username** and **Password** fields, enter your preferred values for the administrator account that will be created on your VM.</span></span>
17. <span data-ttu-id="16f4d-174">Fare clic su **Verify Template** per verificare che i parametri specificati siano validi.</span><span class="sxs-lookup"><span data-stu-id="16f4d-174">Click on **Verify Template** to check if the parameters you specified are valid.</span></span>
18. <span data-ttu-id="16f4d-175">Fare clic su **Save**.</span><span class="sxs-lookup"><span data-stu-id="16f4d-175">Click on **Save**.</span></span>

## <a name="create-a-hudson-job-that-runs-on-a-slave-node-on-azure"></a><span data-ttu-id="16f4d-176">Creare un processo Hudson eseguito in un nodo slave in Azure</span><span class="sxs-lookup"><span data-stu-id="16f4d-176">Create a Hudson job that runs on a slave node on Azure</span></span>
<span data-ttu-id="16f4d-177">In questa sezione si creerà un'attività di Hudson che verrà eseguita in un nodo slave in Azure.</span><span class="sxs-lookup"><span data-stu-id="16f4d-177">In this section, you'll be creating a Hudson task that will run on a slave node on Azure.</span></span>

1. <span data-ttu-id="16f4d-178">Nel dashboard di Hudson, fare clic su **New Job**.</span><span class="sxs-lookup"><span data-stu-id="16f4d-178">In the Hudson dashboard, click **New Job**.</span></span>
2. <span data-ttu-id="16f4d-179">Immettere un nome per il processo che si sta creando.</span><span class="sxs-lookup"><span data-stu-id="16f4d-179">Enter a name for the job you are creating.</span></span>
3. <span data-ttu-id="16f4d-180">Per il tipo di processo, selezionare **Build a free-style software job**.</span><span class="sxs-lookup"><span data-stu-id="16f4d-180">For the job type, select **Build a free-style software job**.</span></span>
4. <span data-ttu-id="16f4d-181">Fare clic su **OK**.</span><span class="sxs-lookup"><span data-stu-id="16f4d-181">Click **OK**.</span></span>
5. <span data-ttu-id="16f4d-182">Nella pagina di configurazione del processo, selezionare **Restrict where this project can be run**.</span><span class="sxs-lookup"><span data-stu-id="16f4d-182">In the job configuration page, select **Restrict where this project can be run**.</span></span>
6. <span data-ttu-id="16f4d-183">Selezionare **Node and label menu** (Menu Nodo ed etichetta) e **linux** (questa etichetta è stata specificata al momento della creazione del modello di macchina virtuale nella sezione precedente).</span><span class="sxs-lookup"><span data-stu-id="16f4d-183">Select **Node and label menu** and select **linux** (we specified this label when creating the virtual machine template in the previous section).</span></span>
7. <span data-ttu-id="16f4d-184">Nella sezione **Build** (Compilazione) fare clic su **Add build step** (Aggiungi passaggio di compilazione) e selezionare **Execute shell** (Esegui shell).</span><span class="sxs-lookup"><span data-stu-id="16f4d-184">In the **Build** section, click **Add build step** and select **Execute shell**.</span></span>
8. <span data-ttu-id="16f4d-185">Modificare lo script seguente sostituendo **(your GitHub account name)** (nome account GitHub), **(your project name)** (nome progetto) e **(your project directory)** (directory progetto) con i valori appropriati e incollare lo script modificato nell'area di testo visualizzata.</span><span class="sxs-lookup"><span data-stu-id="16f4d-185">Edit the following script, replacing **{your github account name}**, **{your project name}**, and **{your project directory}** with appropriate values, and paste the edited script in the text area that appears.</span></span>
   
        # Clone from git repo
   
        currentDir="$PWD"
   
        if [ -e {your project directory} ]; then
   
              cd {your project directory}
   
              git pull origin master
   
        else
   
              git clone https://github.com/{your github account name}/{your project name}.git
   
        fi
   
        # change directory to project
   
        cd $currentDir/{your project directory}
   
        #Execute build task
   
        ant
9. <span data-ttu-id="16f4d-186">Fare clic su **Save**.</span><span class="sxs-lookup"><span data-stu-id="16f4d-186">Click on **Save**.</span></span>
10. <span data-ttu-id="16f4d-187">Nel dashboard di Hudson, trovare il processo appena creato e fare clic sull'icona **Schedule a build** .</span><span class="sxs-lookup"><span data-stu-id="16f4d-187">In the Hudson dashboard, find the job you just created and click on the **Schedule a build** icon.</span></span>

<span data-ttu-id="16f4d-188">Hudson creerà quindi un nodo slave utilizzando il modello creato nella sezione precedente ed eseguirà lo script specificato nell'istruzione di compilazione di questa attività.</span><span class="sxs-lookup"><span data-stu-id="16f4d-188">Hudson will then create a slave node using the template created in the previous section and execute the script you specified in the build step for this task.</span></span>

## <a name="next-steps"></a><span data-ttu-id="16f4d-189">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="16f4d-189">Next Steps</span></span>
<span data-ttu-id="16f4d-190">Per altre informazioni su come usare Azure con Java, vedere il [Centro per sviluppatori Java di Azure].</span><span class="sxs-lookup"><span data-stu-id="16f4d-190">For more information about using Azure with Java, see the [Azure Java Developer Center].</span></span>

<!-- URL List -->

<span data-ttu-id="16f4d-191">[Centro per sviluppatori Java di Azure]: https://azure.microsoft.com/develop/java/</span><span class="sxs-lookup"><span data-stu-id="16f4d-191">[Azure Java Developer Center]: https://azure.microsoft.com/develop/java/</span></span>
<span data-ttu-id="16f4d-192">[profilo di sottoscrizione]: http://go.microsoft.com/fwlink/?LinkID=396395</span><span class="sxs-lookup"><span data-stu-id="16f4d-192">[subscription profile]: http://go.microsoft.com/fwlink/?LinkID=396395</span></span>

<!-- IMG List -->

[add new cloud]: ./media/virtual-machines-azure-slave-plugin-for-hudson/hudson-setup-addcloud.png
[configure profile]: ./media/virtual-machines-azure-slave-plugin-for-hudson/hudson-setup-configureprofile.png
[add vm template]: ./media/virtual-machines-azure-slave-plugin-for-hudson/hudson-setup-addnewvmtemplate.png
[template config]: ./media/virtual-machines-azure-slave-plugin-for-hudson/hudson-setup-templateconfig1-withdata.png
[OS family list]: ./media/virtual-machines-azure-slave-plugin-for-hudson/hudson-oslist.png


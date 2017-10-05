---
title: Usare l'acquisizione di pacchetti per eseguire il monitoraggio proattivo della rete con avvisi e Funzioni di Azure | Microsoft Docs
description: Questo articolo descrive come creare un'acquisizione di pacchetti attivata da un avviso con Azure Network Watcher
services: network-watcher
documentationcenter: na
author: georgewallace
manager: timlt
editor: 
ms.assetid: 75e6e7c4-b3ba-4173-8815-b00d7d824e11
ms.service: network-watcher
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/22/2017
ms.author: gwallace
ms.openlocfilehash: b813172fc1fc1cc683f463f05370c95bfec10f8d
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/29/2017
---
# <a name="use-packet-capture-for-proactive-network-monitoring-with-alerts-and-azure-functions"></a><span data-ttu-id="57e49-103">Usare l'acquisizione di pacchetti per il monitoraggio proattivo della rete con avvisi e Funzioni di Azure</span><span class="sxs-lookup"><span data-stu-id="57e49-103">Use packet capture for proactive network monitoring with alerts and Azure Functions</span></span>

<span data-ttu-id="57e49-104">Il servizio di acquisizione di pacchetti di Network Watcher crea sessioni di acquisizione per registrare il traffico da e verso le macchine virtuali.</span><span class="sxs-lookup"><span data-stu-id="57e49-104">Network Watcher packet capture creates capture sessions to track traffic in and out of virtual machines.</span></span> <span data-ttu-id="57e49-105">Il file di acquisizione può avere un filtro che viene definito per tenere traccia solo del traffico che si vuole monitorare.</span><span class="sxs-lookup"><span data-stu-id="57e49-105">The capture file can have a filter that is defined to track only the traffic that you want to monitor.</span></span> <span data-ttu-id="57e49-106">Questi dati vengono quindi archiviati in un BLOB di archiviazione o in locale nel computer guest.</span><span class="sxs-lookup"><span data-stu-id="57e49-106">This data is then stored in a storage blob or locally on the guest machine.</span></span>

<span data-ttu-id="57e49-107">Questa funzionalità può essere avviata in remoto da altri scenari di automazione, ad esempio Funzioni di Azure.</span><span class="sxs-lookup"><span data-stu-id="57e49-107">This capability can be started remotely from other automation scenarios such as Azure Functions.</span></span> <span data-ttu-id="57e49-108">L'acquisizione di pacchetti consente di eseguire acquisizioni proattive in base alle anomalie di rete definite.</span><span class="sxs-lookup"><span data-stu-id="57e49-108">Packet capture gives you the capability to run proactive captures based on defined network anomalies.</span></span> <span data-ttu-id="57e49-109">Altri utilizzi comprendono la raccolta di statistiche di rete, l'ottenimento di informazioni sulle intrusioni nella rete, il debug delle comunicazioni client-server e molto altro ancora.</span><span class="sxs-lookup"><span data-stu-id="57e49-109">Other uses include gathering network statistics, getting information about network intrusions, debugging client-server communications, and more.</span></span>

<span data-ttu-id="57e49-110">Le risorse distribuite in Azure sono in esecuzione 24 ore su 24, 7 giorni su 7.</span><span class="sxs-lookup"><span data-stu-id="57e49-110">Resources that are deployed in Azure run 24/7.</span></span> <span data-ttu-id="57e49-111">Nessuno può monitorare attivamente lo stato di tutte le risorse 24 ore su 24, 7 giorni su 7.</span><span class="sxs-lookup"><span data-stu-id="57e49-111">You and your staff cannot actively monitor the status of all resources 24/7.</span></span> <span data-ttu-id="57e49-112">Si pensi a cosa può accadere se si verifica un problema alle 2 del mattino.</span><span class="sxs-lookup"><span data-stu-id="57e49-112">For example, what happens if an issue occurs at 2 AM?</span></span>

<span data-ttu-id="57e49-113">Usando Network Watcher, gli avvisi e le funzioni dall'ecosistema di Azure, è possibile rispondere in modo proattivo alle problematiche della rete con i dati e gli strumenti più idonei.</span><span class="sxs-lookup"><span data-stu-id="57e49-113">By using Network Watcher, alerting, and functions from within the Azure ecosystem, you can proactively respond with the data and tools to solve problems in your network.</span></span>

![Scenario][scenario]

## <a name="prerequisites"></a><span data-ttu-id="57e49-115">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="57e49-115">Prerequisites</span></span>

* <span data-ttu-id="57e49-116">La versione più recente di [Azure PowerShell](/powershell/azure/install-azurerm-ps).</span><span class="sxs-lookup"><span data-stu-id="57e49-116">The latest version of [Azure PowerShell](/powershell/azure/install-azurerm-ps).</span></span>
* <span data-ttu-id="57e49-117">Un'istanza esistente di Network Watcher.</span><span class="sxs-lookup"><span data-stu-id="57e49-117">An existing instance of Network Watcher.</span></span> <span data-ttu-id="57e49-118">Se non è già presente, creare un'[istanza di Network Watcher](network-watcher-create.md).</span><span class="sxs-lookup"><span data-stu-id="57e49-118">If you don't already have one, [create an instance of Network Watcher](network-watcher-create.md).</span></span>
* <span data-ttu-id="57e49-119">Una macchina virtuale esistente nella stessa area di Network Watcher con [estensione Windows](../virtual-machines/windows/extensions-nwa.md) o [estensione della macchina virtuale Linux](../virtual-machines/linux/extensions-nwa.md).</span><span class="sxs-lookup"><span data-stu-id="57e49-119">An existing virtual machine in the same region as Network Watcher with the [Windows extension](../virtual-machines/windows/extensions-nwa.md) or [Linux virtual machine extension](../virtual-machines/linux/extensions-nwa.md).</span></span>

## <a name="scenario"></a><span data-ttu-id="57e49-120">Scenario</span><span class="sxs-lookup"><span data-stu-id="57e49-120">Scenario</span></span>

<span data-ttu-id="57e49-121">In questo esempio, la VM invia più segmenti TCP del solito e si vuole essere avvisati.</span><span class="sxs-lookup"><span data-stu-id="57e49-121">In this example, your VM is sending more TCP segments than usual, and you want to be alerted.</span></span> <span data-ttu-id="57e49-122">Come esempio qui vengono usati i segmenti TCP, ma è possibile usare qualsiasi condizione di avviso.</span><span class="sxs-lookup"><span data-stu-id="57e49-122">TCP segments are used as an example here, but you can use any alert condition.</span></span>

<span data-ttu-id="57e49-123">Una volta ricevuto l'avviso, si vogliono ricevere dati a livello di pacchetto per comprendere perché la comunicazione è aumentata.</span><span class="sxs-lookup"><span data-stu-id="57e49-123">When you are alerted, you want to receive packet-level data to understand why communication has increased.</span></span> <span data-ttu-id="57e49-124">Sarà così possibile intervenire per riportare la macchina virtuale in condizioni di normale comunicazione.</span><span class="sxs-lookup"><span data-stu-id="57e49-124">Then you can take steps to return the virtual machine to regular communication.</span></span>

<span data-ttu-id="57e49-125">Questo scenario presuppone che esistano già un'istanza di Network Watcher e un gruppo di risorse con una macchina virtuale valida.</span><span class="sxs-lookup"><span data-stu-id="57e49-125">This scenario assumes that you have an existing instance of Network Watcher and a resource group with a valid virtual machine.</span></span>

<span data-ttu-id="57e49-126">L'elenco seguente è una panoramica del flusso di lavoro effettivo:</span><span class="sxs-lookup"><span data-stu-id="57e49-126">The following list is an overview of the workflow that takes place:</span></span>

1. <span data-ttu-id="57e49-127">Nella macchina virtuale viene attivato un avviso.</span><span class="sxs-lookup"><span data-stu-id="57e49-127">An alert is triggered on your VM.</span></span>
1. <span data-ttu-id="57e49-128">L'avviso chiama la funzione di Azure tramite un webhook.</span><span class="sxs-lookup"><span data-stu-id="57e49-128">The alert calls your Azure function via a webhook.</span></span>
1. <span data-ttu-id="57e49-129">La funzione di Azure elabora l'avviso e avvia una sessione di acquisizione di pacchetti di Network Watcher.</span><span class="sxs-lookup"><span data-stu-id="57e49-129">Your Azure function processes the alert and starts a Network Watcher packet capture session.</span></span>
1. <span data-ttu-id="57e49-130">L'acquisizione di pacchetti viene eseguita nella macchina virtuale e raccoglie il traffico.</span><span class="sxs-lookup"><span data-stu-id="57e49-130">The packet capture runs on the VM and collects traffic.</span></span>
1. <span data-ttu-id="57e49-131">Il file di acquisizione pacchetto viene caricato in un account di archiviazione per revisione e diagnosi.</span><span class="sxs-lookup"><span data-stu-id="57e49-131">The packet capture file is uploaded to a storage account for review and diagnosis.</span></span>

<span data-ttu-id="57e49-132">Per automatizzare questo processo, nella VM viene creato e connesso un avviso da attivare quando si verifica l'evento imprevisto.</span><span class="sxs-lookup"><span data-stu-id="57e49-132">To automate this process, we create and connect an alert on our VM to trigger when the incident occurs.</span></span> <span data-ttu-id="57e49-133">Viene anche creata una funzione per chiamare Network Watcher.</span><span class="sxs-lookup"><span data-stu-id="57e49-133">We also create a function to call into Network Watcher.</span></span>

<span data-ttu-id="57e49-134">Questo scenario prevede le seguenti operazioni:</span><span class="sxs-lookup"><span data-stu-id="57e49-134">This scenario does the following:</span></span>

* <span data-ttu-id="57e49-135">Crea una funzione di Azure che avvia un'acquisizione di pacchetti.</span><span class="sxs-lookup"><span data-stu-id="57e49-135">Creates an Azure function that starts a packet capture.</span></span>
* <span data-ttu-id="57e49-136">Crea una regola di avviso in una macchina virtuale e configura la regola di avviso in modo da chiamare la funzione di Azure.</span><span class="sxs-lookup"><span data-stu-id="57e49-136">Creates an alert rule on a virtual machine and configures the alert rule to call the Azure function.</span></span>

## <a name="create-an-azure-function"></a><span data-ttu-id="57e49-137">Creare una funzione di Azure</span><span class="sxs-lookup"><span data-stu-id="57e49-137">Create an Azure function</span></span>

<span data-ttu-id="57e49-138">Il primo passaggio è la creazione di una funzione di Azure per elaborare l'avviso e creare un'acquisizione di pacchetti.</span><span class="sxs-lookup"><span data-stu-id="57e49-138">The first step is to create an Azure function to process the alert and create a packet capture.</span></span>

1. <span data-ttu-id="57e49-139">Nel [portale di Azure](https://portal.azure.com) selezionare **Nuovo** > **Calcolo** > **App per le funzioni**.</span><span class="sxs-lookup"><span data-stu-id="57e49-139">In the [Azure portal](https://portal.azure.com), select **New** > **Compute** > **Function App**.</span></span>

    ![Creazione di un'app per le funzioni][1-1]

2. <span data-ttu-id="57e49-141">Nel pannello **App per le funzioni** immettere i valori seguenti e fare clic su **OK** per creare l'app:</span><span class="sxs-lookup"><span data-stu-id="57e49-141">On the **Function App** blade, enter the following values, and then select **OK** to create the app:</span></span>

    |<span data-ttu-id="57e49-142">**Impostazione**</span><span class="sxs-lookup"><span data-stu-id="57e49-142">**Setting**</span></span> | <span data-ttu-id="57e49-143">**Valore**</span><span class="sxs-lookup"><span data-stu-id="57e49-143">**Value**</span></span> | <span data-ttu-id="57e49-144">**Dettagli**</span><span class="sxs-lookup"><span data-stu-id="57e49-144">**Details**</span></span> |
    |---|---|---|
    |<span data-ttu-id="57e49-145">**Nome app**</span><span class="sxs-lookup"><span data-stu-id="57e49-145">**App name**</span></span>|<span data-ttu-id="57e49-146">PacketCaptureExample</span><span class="sxs-lookup"><span data-stu-id="57e49-146">PacketCaptureExample</span></span>|<span data-ttu-id="57e49-147">Nome dell'app per le funzioni.</span><span class="sxs-lookup"><span data-stu-id="57e49-147">The name of the function app.</span></span>|
    |<span data-ttu-id="57e49-148">**Sottoscrizione**</span><span class="sxs-lookup"><span data-stu-id="57e49-148">**Subscription**</span></span>|<span data-ttu-id="57e49-149">[Sottoscrizione]: sottoscrizione in cui creare l'app per le funzioni.</span><span class="sxs-lookup"><span data-stu-id="57e49-149">[Your subscription]The subscription for which to create the function app.</span></span>||
    |<span data-ttu-id="57e49-150">**Gruppo di risorse**</span><span class="sxs-lookup"><span data-stu-id="57e49-150">**Resource Group**</span></span>|<span data-ttu-id="57e49-151">PacketCaptureRG</span><span class="sxs-lookup"><span data-stu-id="57e49-151">PacketCaptureRG</span></span>|<span data-ttu-id="57e49-152">Nome del gruppo di risorse che conterrà l'app per le funzioni.</span><span class="sxs-lookup"><span data-stu-id="57e49-152">The resource group to contain the function app.</span></span>|
    |<span data-ttu-id="57e49-153">**Piano di hosting**</span><span class="sxs-lookup"><span data-stu-id="57e49-153">**Hosting Plan**</span></span>|<span data-ttu-id="57e49-154">Piano a consumo</span><span class="sxs-lookup"><span data-stu-id="57e49-154">Consumption Plan</span></span>| <span data-ttu-id="57e49-155">Tipo di piano usato dall'app per le funzioni.</span><span class="sxs-lookup"><span data-stu-id="57e49-155">The type of plan your function app uses.</span></span> <span data-ttu-id="57e49-156">Le opzioni sono Consumo e Piano di servizio app di Azure.</span><span class="sxs-lookup"><span data-stu-id="57e49-156">Options are Consumption or Azure App Service plan.</span></span> |
    |<span data-ttu-id="57e49-157">**Posizione**</span><span class="sxs-lookup"><span data-stu-id="57e49-157">**Location**</span></span>|<span data-ttu-id="57e49-158">Stati Uniti centrali</span><span class="sxs-lookup"><span data-stu-id="57e49-158">Central US</span></span>| <span data-ttu-id="57e49-159">Area in cui creare l'app per le funzioni.</span><span class="sxs-lookup"><span data-stu-id="57e49-159">The region in which to create the function app.</span></span>|
    |<span data-ttu-id="57e49-160">**Storage Account**</span><span class="sxs-lookup"><span data-stu-id="57e49-160">**Storage Account**</span></span>|<span data-ttu-id="57e49-161">{generato automaticamente}</span><span class="sxs-lookup"><span data-stu-id="57e49-161">{autogenerated}</span></span>| <span data-ttu-id="57e49-162">Account di archiviazione richiesto da Funzioni di Azure per l'archiviazione di uso generico.</span><span class="sxs-lookup"><span data-stu-id="57e49-162">The storage account that Azure Functions needs for general-purpose storage.</span></span>|

3. <span data-ttu-id="57e49-163">Nel pannello delle app per le funzioni **PacketCaptureExample** selezionare **Funzioni** > **Funzione personalizzata** >**+**.</span><span class="sxs-lookup"><span data-stu-id="57e49-163">On the **PacketCaptureExample Function Apps** blade, select **Functions** > **Custom function** >**+**.</span></span>

4. <span data-ttu-id="57e49-164">Selezionare **HttpTrigger-Powershell** e quindi immettere le informazioni rimanenti.</span><span class="sxs-lookup"><span data-stu-id="57e49-164">Select **HttpTrigger-Powershell**, and then enter the remaining information.</span></span> <span data-ttu-id="57e49-165">Selezionare infine **Crea** per creare la funzione.</span><span class="sxs-lookup"><span data-stu-id="57e49-165">Finally, to create the function, select **Create**.</span></span>

    |<span data-ttu-id="57e49-166">**Impostazione**</span><span class="sxs-lookup"><span data-stu-id="57e49-166">**Setting**</span></span> | <span data-ttu-id="57e49-167">**Valore**</span><span class="sxs-lookup"><span data-stu-id="57e49-167">**Value**</span></span> | <span data-ttu-id="57e49-168">**Dettagli**</span><span class="sxs-lookup"><span data-stu-id="57e49-168">**Details**</span></span> |
    |---|---|---|
    |<span data-ttu-id="57e49-169">**Scenario**</span><span class="sxs-lookup"><span data-stu-id="57e49-169">**Scenario**</span></span>|<span data-ttu-id="57e49-170">Sperimentale</span><span class="sxs-lookup"><span data-stu-id="57e49-170">Experimental</span></span>|<span data-ttu-id="57e49-171">Tipo di scenario</span><span class="sxs-lookup"><span data-stu-id="57e49-171">Type of scenario</span></span>|
    |<span data-ttu-id="57e49-172">**Dare un nome alla funzione**</span><span class="sxs-lookup"><span data-stu-id="57e49-172">**Name your function**</span></span>|<span data-ttu-id="57e49-173">AlertPacketCapturePowerShell</span><span class="sxs-lookup"><span data-stu-id="57e49-173">AlertPacketCapturePowerShell</span></span>|<span data-ttu-id="57e49-174">Nome della funzione</span><span class="sxs-lookup"><span data-stu-id="57e49-174">Name of the function</span></span>|
    |<span data-ttu-id="57e49-175">**Livello di autorizzazione**</span><span class="sxs-lookup"><span data-stu-id="57e49-175">**Authorization level**</span></span>|<span data-ttu-id="57e49-176">Funzione</span><span class="sxs-lookup"><span data-stu-id="57e49-176">Function</span></span>|<span data-ttu-id="57e49-177">Livello di autorizzazione per la funzione</span><span class="sxs-lookup"><span data-stu-id="57e49-177">Authorization level for the function</span></span>|

![Esempio di funzioni][functions1]

> [!NOTE]
> <span data-ttu-id="57e49-179">Il modello di PowerShell è sperimentale e non dispone del supporto completo.</span><span class="sxs-lookup"><span data-stu-id="57e49-179">The PowerShell template is experimental and does not have full support.</span></span>

<span data-ttu-id="57e49-180">Per questo esempio sono richieste alcune personalizzazioni illustrate nei passaggi seguenti.</span><span class="sxs-lookup"><span data-stu-id="57e49-180">Customizations are required for this example and are explained in the following steps.</span></span>

### <a name="add-modules"></a><span data-ttu-id="57e49-181">Aggiungere moduli</span><span class="sxs-lookup"><span data-stu-id="57e49-181">Add modules</span></span>

<span data-ttu-id="57e49-182">Per usare i cmdlet PowerShell di Network Watcher, caricare il modulo PowerShell più recente nell'app per le funzioni.</span><span class="sxs-lookup"><span data-stu-id="57e49-182">To use Network Watcher PowerShell cmdlets, upload the latest PowerShell module to the function app.</span></span>

1. <span data-ttu-id="57e49-183">Nel computer locale con i moduli di Azure PowerShell più recenti installati, eseguire il seguente comando PowerShell:</span><span class="sxs-lookup"><span data-stu-id="57e49-183">On your local machine with the latest Azure PowerShell modules installed, run the following PowerShell command:</span></span>

    ```powershell
    (Get-Module AzureRM.Network).Path
    ```

    <span data-ttu-id="57e49-184">Questo esempio visualizza il percorso locale dei moduli di Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="57e49-184">This example gives you the local path of your Azure PowerShell modules.</span></span> <span data-ttu-id="57e49-185">Queste cartelle verranno usate in un passaggio successivo.</span><span class="sxs-lookup"><span data-stu-id="57e49-185">These folders are used in a later step.</span></span> <span data-ttu-id="57e49-186">I moduli usati in questo scenario sono:</span><span class="sxs-lookup"><span data-stu-id="57e49-186">The modules that are used in this scenario are:</span></span>

    * <span data-ttu-id="57e49-187">AzureRM.Network</span><span class="sxs-lookup"><span data-stu-id="57e49-187">AzureRM.Network</span></span>

    * <span data-ttu-id="57e49-188">AzureRM.Profile</span><span class="sxs-lookup"><span data-stu-id="57e49-188">AzureRM.Profile</span></span>

    * <span data-ttu-id="57e49-189">AzureRM.Resources</span><span class="sxs-lookup"><span data-stu-id="57e49-189">AzureRM.Resources</span></span>

    ![Cartelle di PowerShell][functions5]

1. <span data-ttu-id="57e49-191">Selezionare **Impostazioni dell'app per le funzioni** > **Passa all'editor del servizio app**.</span><span class="sxs-lookup"><span data-stu-id="57e49-191">Select **Function app settings** > **Go to App Service Editor**.</span></span>

    ![Impostazioni dell'app per le funzioni][functions2]

1. <span data-ttu-id="57e49-193">Fare clic con il pulsante destro del mouse sulla cartella **AlertPacketCapturePowershell** e quindi creare una cartella denominata **azuremodules**.</span><span class="sxs-lookup"><span data-stu-id="57e49-193">Right-click the **AlertPacketCapturePowershell** folder, and then create a folder called **azuremodules**.</span></span> 

4. <span data-ttu-id="57e49-194">Creare una sottocartella per ogni modulo necessario.</span><span class="sxs-lookup"><span data-stu-id="57e49-194">Create a subfolder for each module that you need.</span></span>

    ![Cartelle e sottocartelle][functions3]

    * <span data-ttu-id="57e49-196">AzureRM.Network</span><span class="sxs-lookup"><span data-stu-id="57e49-196">AzureRM.Network</span></span>

    * <span data-ttu-id="57e49-197">AzureRM.Profile</span><span class="sxs-lookup"><span data-stu-id="57e49-197">AzureRM.Profile</span></span>

    * <span data-ttu-id="57e49-198">AzureRM.Resources</span><span class="sxs-lookup"><span data-stu-id="57e49-198">AzureRM.Resources</span></span>

1. <span data-ttu-id="57e49-199">Fare clic con il pulsante destro del mouse sulla sottocartella **AzureRM.Network** e quindi scegliere **Carica file**.</span><span class="sxs-lookup"><span data-stu-id="57e49-199">Right-click the **AzureRM.Network** subfolder, and then select **Upload Files**.</span></span> 

6. <span data-ttu-id="57e49-200">Passare ai moduli di Azure.</span><span class="sxs-lookup"><span data-stu-id="57e49-200">Go to your Azure modules.</span></span> <span data-ttu-id="57e49-201">Nella cartella **AzureRM.Network** locale selezionare tutti i file presenti.</span><span class="sxs-lookup"><span data-stu-id="57e49-201">In the local **AzureRM.Network** folder, select all the files in the folder.</span></span> <span data-ttu-id="57e49-202">Selezionare **OK**.</span><span class="sxs-lookup"><span data-stu-id="57e49-202">Then select **OK**.</span></span> 

7. <span data-ttu-id="57e49-203">Ripetere questi passaggi per **AzureRM.Profile** e **AzureRM.Resources**.</span><span class="sxs-lookup"><span data-stu-id="57e49-203">Repeat these steps for **AzureRM.Profile** and **AzureRM.Resources**.</span></span>

    ![Caricare file][functions6]

1. <span data-ttu-id="57e49-205">Al termine, ogni cartella dovrebbe includere i file dei moduli di PowerShell del computer locale.</span><span class="sxs-lookup"><span data-stu-id="57e49-205">After you've finished, each folder should have the PowerShell module files from your local machine.</span></span>

    ![File di PowerShell][functions7]

### <a name="authentication"></a><span data-ttu-id="57e49-207">Autenticazione</span><span class="sxs-lookup"><span data-stu-id="57e49-207">Authentication</span></span>

<span data-ttu-id="57e49-208">Per usare i cmdlet PowerShell, è necessario eseguire l'autenticazione,</span><span class="sxs-lookup"><span data-stu-id="57e49-208">To use the PowerShell cmdlets, you must authenticate.</span></span> <span data-ttu-id="57e49-209">L'autenticazione viene configurata nell'app per le funzioni.</span><span class="sxs-lookup"><span data-stu-id="57e49-209">You configure authentication in the function app.</span></span> <span data-ttu-id="57e49-210">Per configurare l'autenticazione è necessario definire le variabili di ambiente e caricare un file di chiave crittografata nell'app per le funzioni.</span><span class="sxs-lookup"><span data-stu-id="57e49-210">To configure authentication, you must configure environment variables and upload an encrypted key file to the function app.</span></span>

> [!NOTE]
> <span data-ttu-id="57e49-211">Questo scenario fornisce solo un esempio di come implementare l'autenticazione con Funzioni di Azure.</span><span class="sxs-lookup"><span data-stu-id="57e49-211">This scenario provides just one example of how to implement authentication with Azure Functions.</span></span> <span data-ttu-id="57e49-212">Per eseguire questa operazione è possibile procedere in altri modi.</span><span class="sxs-lookup"><span data-stu-id="57e49-212">There are other ways to do this.</span></span>

#### <a name="encrypted-credentials"></a><span data-ttu-id="57e49-213">Credenziali crittografate</span><span class="sxs-lookup"><span data-stu-id="57e49-213">Encrypted credentials</span></span>

<span data-ttu-id="57e49-214">Lo script di PowerShell seguente crea un file di chiave denominato **PassEncryptKey.key**</span><span class="sxs-lookup"><span data-stu-id="57e49-214">The following PowerShell script creates a key file called **PassEncryptKey.key**.</span></span> <span data-ttu-id="57e49-215">e mette a disposizione una versione crittografata della password fornita.</span><span class="sxs-lookup"><span data-stu-id="57e49-215">It also provides an encrypted version of the password that's supplied.</span></span> <span data-ttu-id="57e49-216">Questa password è la stessa che viene definita per l'applicazione di Azure Active Directory usata per l'autenticazione.</span><span class="sxs-lookup"><span data-stu-id="57e49-216">This password is the same password that is defined for the Azure Active Directory application that's used for authentication.</span></span>

```powershell
#Variables
$keypath = "C:\temp\PassEncryptKey.key"
$AESKey = New-Object Byte[] 32
$Password = "<insert a password here>"

#Keys
[Security.Cryptography.RNGCryptoServiceProvider]::Create().GetBytes($AESKey) 
Set-Content $keypath $AESKey

#Get encrypted password
$secPw = ConvertTo-SecureString -AsPlainText $Password -Force
$AESKey = Get-content $KeyPath
$Encryptedpassword = $secPw | ConvertFrom-SecureString -Key $AESKey
$Encryptedpassword
```

<span data-ttu-id="57e49-217">Nell'editor del servizio app dell'app per le funzioni creare una cartella denominata **keys** in **AlertPacketCapturePowerShell**.</span><span class="sxs-lookup"><span data-stu-id="57e49-217">In the App Service Editor of the function app, create a folder called **keys** under **AlertPacketCapturePowerShell**.</span></span> <span data-ttu-id="57e49-218">Caricare quindi il file **PassEncryptKey.key** creato nell'esempio di PowerShell precedente.</span><span class="sxs-lookup"><span data-stu-id="57e49-218">Then upload the **PassEncryptKey.key** file that you created in the previous PowerShell sample.</span></span>

![Chiave delle funzioni][functions8]

### <a name="retrieve-values-for-environment-variables"></a><span data-ttu-id="57e49-220">Recuperare i valori per le variabili di ambiente</span><span class="sxs-lookup"><span data-stu-id="57e49-220">Retrieve values for environment variables</span></span>

<span data-ttu-id="57e49-221">L'ultimo requisito consiste nel configurare le variabili di ambiente necessarie per accedere ai valori per l'autenticazione.</span><span class="sxs-lookup"><span data-stu-id="57e49-221">The final requirement is to set up the environment variables that are necessary to access the values for authentication.</span></span> <span data-ttu-id="57e49-222">Di seguito è riportato un elenco delle variabili di ambiente create:</span><span class="sxs-lookup"><span data-stu-id="57e49-222">The following list shows the environment variables that are created:</span></span>

* <span data-ttu-id="57e49-223">AzureClientID</span><span class="sxs-lookup"><span data-stu-id="57e49-223">AzureClientID</span></span>

* <span data-ttu-id="57e49-224">AzureTenant</span><span class="sxs-lookup"><span data-stu-id="57e49-224">AzureTenant</span></span>

* <span data-ttu-id="57e49-225">AzureCredPassword</span><span class="sxs-lookup"><span data-stu-id="57e49-225">AzureCredPassword</span></span>


#### <a name="azureclientid"></a><span data-ttu-id="57e49-226">AzureClientID</span><span class="sxs-lookup"><span data-stu-id="57e49-226">AzureClientID</span></span>

<span data-ttu-id="57e49-227">L'ID client è l'ID applicazione di un'applicazione in Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="57e49-227">The client ID is the Application ID of an application in Azure Active Directory.</span></span>

1. <span data-ttu-id="57e49-228">Se non esiste già un'applicazione da usare, eseguire questo esempio per crearne una.</span><span class="sxs-lookup"><span data-stu-id="57e49-228">If you don't already have an application to use, run the following example to create an application.</span></span>

    ```powershell
    $app = New-AzureRmADApplication -DisplayName "ExampleAutomationAccount_MF" -HomePage "https://exampleapp.com" -IdentifierUris "https://exampleapp1.com/ExampleFunctionsAccount" -Password "<same password as defined earlier>"
    New-AzureRmADServicePrincipal -ApplicationId $app.ApplicationId
    Start-Sleep 15
    New-AzureRmRoleAssignment -RoleDefinitionName Contributor -ServicePrincipalName $app.ApplicationId
    ```

   > [!NOTE]
   > <span data-ttu-id="57e49-229">La password usata per la creazione dell'applicazione deve essere la stessa creata in precedenza durante il salvataggio del file di chiave.</span><span class="sxs-lookup"><span data-stu-id="57e49-229">The password that you use when creating the application should be the same password that you created earlier when saving the key file.</span></span>

1. <span data-ttu-id="57e49-230">Nel portale di Azure selezionare **Sottoscrizioni**.</span><span class="sxs-lookup"><span data-stu-id="57e49-230">In the Azure portal, select **Subscriptions**.</span></span> <span data-ttu-id="57e49-231">Selezionare la sottoscrizione da usare e quindi fare clic su **Controllo di accesso (IAM)**.</span><span class="sxs-lookup"><span data-stu-id="57e49-231">Select the subscription to use, and then select **Access control (IAM)**.</span></span>

    ![IAM delle funzioni][functions9]

1. <span data-ttu-id="57e49-233">Scegliere l'account da usare e quindi selezionare **Proprietà**.</span><span class="sxs-lookup"><span data-stu-id="57e49-233">Choose the account to use, and then select **Properties**.</span></span> <span data-ttu-id="57e49-234">Copiare l'ID applicazione.</span><span class="sxs-lookup"><span data-stu-id="57e49-234">Copy the Application ID.</span></span>

    ![ID applicazione per le funzioni][functions10]

#### <a name="azuretenant"></a><span data-ttu-id="57e49-236">AzureTenant</span><span class="sxs-lookup"><span data-stu-id="57e49-236">AzureTenant</span></span>

<span data-ttu-id="57e49-237">Ottenere l'ID tenant eseguendo questo esempio di PowerShell:</span><span class="sxs-lookup"><span data-stu-id="57e49-237">Obtain the tenant ID  by running the following PowerShell sample:</span></span>

```powershell
(Get-AzureRmSubscription -SubscriptionName "<subscriptionName>").TenantId
```

#### <a name="azurecredpassword"></a><span data-ttu-id="57e49-238">AzureCredPassword</span><span class="sxs-lookup"><span data-stu-id="57e49-238">AzureCredPassword</span></span>

<span data-ttu-id="57e49-239">Il valore della variabile di ambiente AzureCredPassword è il valore ottenuto eseguendo questo esempio di PowerShell.</span><span class="sxs-lookup"><span data-stu-id="57e49-239">The value of the AzureCredPassword environment variable is the value that you get from running the following PowerShell sample.</span></span> <span data-ttu-id="57e49-240">Si tratta dello stesso esempio riportato nella sezione **Credenziali crittografate** precedente.</span><span class="sxs-lookup"><span data-stu-id="57e49-240">This example is the same one that's shown in the preceding **Encrypted credentials** section.</span></span> <span data-ttu-id="57e49-241">Il valore richiesto è l'output della variabile `$Encryptedpassword`.</span><span class="sxs-lookup"><span data-stu-id="57e49-241">The value that's needed is the output of the `$Encryptedpassword` variable.</span></span>  <span data-ttu-id="57e49-242">Si tratta della password dell'entità servizio crittografata tramite lo script di PowerShell.</span><span class="sxs-lookup"><span data-stu-id="57e49-242">This is the service principal password that you encrypted by using the PowerShell script.</span></span>

```powershell
#Variables
$keypath = "C:\temp\PassEncryptKey.key"
$AESKey = New-Object Byte[] 32
$Password = "<insert a password here>"

#Keys
[Security.Cryptography.RNGCryptoServiceProvider]::Create().GetBytes($AESKey) 
Set-Content $keypath $AESKey

#Get encrypted password
$secPw = ConvertTo-SecureString -AsPlainText $Password -Force
$AESKey = Get-content $KeyPath
$Encryptedpassword = $secPw | ConvertFrom-SecureString -Key $AESKey
$Encryptedpassword
```

### <a name="store-the-environment-variables"></a><span data-ttu-id="57e49-243">Archiviare le variabili di ambiente</span><span class="sxs-lookup"><span data-stu-id="57e49-243">Store the environment variables</span></span>

1. <span data-ttu-id="57e49-244">Passare all'app per le funzioni.</span><span class="sxs-lookup"><span data-stu-id="57e49-244">Go to the function app.</span></span> <span data-ttu-id="57e49-245">Selezionare quindi **Impostazioni dell'app per le funzioni** > **Configurare le impostazioni dell'app**.</span><span class="sxs-lookup"><span data-stu-id="57e49-245">Then select **Function app settings** > **Configure app settings**.</span></span>

    ![Configurare le impostazioni applicazione][functions11]

1. <span data-ttu-id="57e49-247">Aggiungere le variabili di ambiente e i relativi valori alle impostazioni dell'app e quindi fare clic su **Salva**.</span><span class="sxs-lookup"><span data-stu-id="57e49-247">Add the environment variables and their values to the app settings, and then select **Save**.</span></span>

    ![Impostazioni app][functions12]

### <a name="add-powershell-to-the-function"></a><span data-ttu-id="57e49-249">Aggiunta di PowerShell alla funzione</span><span class="sxs-lookup"><span data-stu-id="57e49-249">Add PowerShell to the function</span></span>

<span data-ttu-id="57e49-250">A questo punto è necessario chiamare Network Watcher dalla funzione di Azure.</span><span class="sxs-lookup"><span data-stu-id="57e49-250">It's now time to make calls into Network Watcher from within the Azure function.</span></span> <span data-ttu-id="57e49-251">L'implementazione di questa funzione può variare a seconda dei requisiti.</span><span class="sxs-lookup"><span data-stu-id="57e49-251">Depending on the requirements, the implementation of this function can vary.</span></span> <span data-ttu-id="57e49-252">Il flusso generale del codice è tuttavia il seguente:</span><span class="sxs-lookup"><span data-stu-id="57e49-252">However, the general flow of the code is as follows:</span></span>

1. <span data-ttu-id="57e49-253">Elaborare i parametri di input.</span><span class="sxs-lookup"><span data-stu-id="57e49-253">Process input parameters.</span></span>
2. <span data-ttu-id="57e49-254">Eseguire una query sulle acquisizioni di pacchetti esistenti per verificare i limiti e risolvere i conflitti di nomi.</span><span class="sxs-lookup"><span data-stu-id="57e49-254">Query existing packet captures to verify limits and resolve name conflicts.</span></span>
3. <span data-ttu-id="57e49-255">Creare un'acquisizione di pacchetti con i parametri appropriati.</span><span class="sxs-lookup"><span data-stu-id="57e49-255">Create a packet capture with appropriate parameters.</span></span>
4. <span data-ttu-id="57e49-256">Eseguire periodicamente il polling dell'acquisizione di pacchetti fino al completamento.</span><span class="sxs-lookup"><span data-stu-id="57e49-256">Poll packet capture periodically until it's complete.</span></span>
5. <span data-ttu-id="57e49-257">Notificare all'utente che la sessione di acquisizione di pacchetti è completa.</span><span class="sxs-lookup"><span data-stu-id="57e49-257">Notify the user that the packet capture session is complete.</span></span>

<span data-ttu-id="57e49-258">L'esempio seguente è codice PowerShell che può essere usato nella funzione.</span><span class="sxs-lookup"><span data-stu-id="57e49-258">The following example is PowerShell code that can be used in the function.</span></span> <span data-ttu-id="57e49-259">È necessario sostituire i valori per **subscriptionId**, **resourceGroupName** e **storageAccountName**.</span><span class="sxs-lookup"><span data-stu-id="57e49-259">There are values that need to be replaced for **subscriptionId**, **resourceGroupName**, and **storageAccountName**.</span></span>

```powershell
            #Import Azure PowerShell modules required to make calls to Network Watcher
            Import-Module "D:\home\site\wwwroot\AlertPacketCapturePowerShell\azuremodules\AzureRM.Profile\AzureRM.Profile.psd1" -Global
            Import-Module "D:\home\site\wwwroot\AlertPacketCapturePowerShell\azuremodules\AzureRM.Network\AzureRM.Network.psd1" -Global
            Import-Module "D:\home\site\wwwroot\AlertPacketCapturePowerShell\azuremodules\AzureRM.Resources\AzureRM.Resources.psd1" -Global

            #Process alert request body
            $requestBody = Get-Content $req -Raw | ConvertFrom-Json

            #Storage account ID to save captures in
            $storageaccountid = "/subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Storage/storageAccounts/{storageAccountName}"

            #Packet capture vars
            $packetcapturename = "PSAzureFunction"
            $packetCaptureLimit = 10
            $packetCaptureDuration = 10

            #Credentials
            $tenant = $env:AzureTenant
            $pw = $env:AzureCredPassword
            $clientid = $env:AzureClientId
            $keypath = "D:\home\site\wwwroot\AlertPacketCapturePowerShell\keys\PassEncryptKey.key"

            #Authentication
            $secpassword = $pw | ConvertTo-SecureString -Key (Get-Content $keypath)
            $credential = New-Object System.Management.Automation.PSCredential ($clientid, $secpassword)
            Add-AzureRMAccount -ServicePrincipal -Tenant $tenant -Credential $credential #-WarningAction SilentlyContinue | out-null


            #Get the VM that fired the alert
            if($requestBody.context.resourceType -eq "Microsoft.Compute/virtualMachines")
            {
                Write-Output ("Subscription ID: {0}" -f $requestBody.context.subscriptionId)
                Write-Output ("Resource Group:  {0}" -f $requestBody.context.resourceGroupName)
                Write-Output ("Resource Name:  {0}" -f $requestBody.context.resourceName)
                Write-Output ("Resource Type:  {0}" -f $requestBody.context.resourceType)

                #Get the Network Watcher in the VM's region
                $nw = Get-AzurermResource | Where {$_.ResourceType -eq "Microsoft.Network/networkWatchers" -and $_.Location -eq $requestBody.context.resourceRegion}
                $networkWatcher = Get-AzureRmNetworkWatcher -Name $nw.Name -ResourceGroupName $nw.ResourceGroupName

                #Get existing packetCaptures
                $packetCaptures = Get-AzureRmNetworkWatcherPacketCapture -NetworkWatcher $networkWatcher

                #Remove existing packet capture created by the function (if it exists)
                $packetCaptures | %{if($_.Name -eq $packetCaptureName)
                { 
                    Remove-AzureRmNetworkWatcherPacketCapture -NetworkWatcher $networkWatcher -PacketCaptureName $packetCaptureName
                }}

                #Initiate packet capture on the VM that fired the alert
                if ((Get-AzureRmNetworkWatcherPacketCapture -NetworkWatcher $networkWatcher).Count -lt $packetCaptureLimit){
                    echo "Initiating Packet Capture"
                    New-AzureRmNetworkWatcherPacketCapture -NetworkWatcher $networkWatcher -TargetVirtualMachineId $requestBody.context.resourceId -PacketCaptureName $packetCaptureName -StorageAccountId $storageaccountid -TimeLimitInSeconds $packetCaptureDuration
                    Out-File -Encoding Ascii -FilePath $res -inputObject "Packet Capture created on ${requestBody.context.resourceID}"
                }
            } 
 ``` 
#### <a name="retrieve-the-function-url"></a><span data-ttu-id="57e49-260">Recuperare l'URL della funzione</span><span class="sxs-lookup"><span data-stu-id="57e49-260">Retrieve the function URL</span></span> 
1. <span data-ttu-id="57e49-261">Dopo avere creato la funzione, configurare l'avviso per chiamare l'URL associato alla funzione.</span><span class="sxs-lookup"><span data-stu-id="57e49-261">After you've created your function, configure your alert to call the URL that's associated with the function.</span></span> <span data-ttu-id="57e49-262">Per ottenere questo valore, copiare l'URL della funzione dall'app per le funzioni.</span><span class="sxs-lookup"><span data-stu-id="57e49-262">To get this value, copy the function URL from your function app.</span></span>

    ![Ricerca dell'URL della funzione][functions13]

2. <span data-ttu-id="57e49-264">Copiare l'URL della funzione per l'app per le funzioni.</span><span class="sxs-lookup"><span data-stu-id="57e49-264">Copy the function URL for your function app.</span></span>

    ![Copia dell'URL della funzione][2]

<span data-ttu-id="57e49-266">Se sono necessarie proprietà personalizzate nel payload della richiesta POST del webhook, vedere [Configurare un webhook in un avviso relativo alle metriche di Azure](../monitoring-and-diagnostics/insights-webhooks-alerts.md).</span><span class="sxs-lookup"><span data-stu-id="57e49-266">If you require custom properties in the payload of the webhook POST request, refer to [Configure a webhook on an Azure metric alert](../monitoring-and-diagnostics/insights-webhooks-alerts.md).</span></span>

## <a name="configure-an-alert-on-a-vm"></a><span data-ttu-id="57e49-267">Configurare un avviso in una VM</span><span class="sxs-lookup"><span data-stu-id="57e49-267">Configure an alert on a VM</span></span>

<span data-ttu-id="57e49-268">Si possono configurare avvisi per notificare alle singole persone quando una metrica specifica supera una soglia assegnata.</span><span class="sxs-lookup"><span data-stu-id="57e49-268">Alerts can be configured to notify individuals when a specific metric crosses a threshold that's assigned to it.</span></span> <span data-ttu-id="57e49-269">In questo esempio, l'avviso è sui segmenti TCP inviati, ma può essere attivato per molte altre metriche.</span><span class="sxs-lookup"><span data-stu-id="57e49-269">In this example, the alert is on the TCP segments that are sent, but the alert can be triggered for many other metrics.</span></span> <span data-ttu-id="57e49-270">In questo esempio viene configurato un avviso per chiamare un webhook per chiamare la funzione.</span><span class="sxs-lookup"><span data-stu-id="57e49-270">In this example, an alert is configured to call a webhook to call the function.</span></span>

### <a name="create-the-alert-rule"></a><span data-ttu-id="57e49-271">Creare la regola di avviso</span><span class="sxs-lookup"><span data-stu-id="57e49-271">Create the alert rule</span></span>

<span data-ttu-id="57e49-272">Passare a una macchina virtuale esistente, quindi aggiungere una regola di avviso.</span><span class="sxs-lookup"><span data-stu-id="57e49-272">Go to an existing virtual machine, and then add an alert rule.</span></span> <span data-ttu-id="57e49-273">Per informazioni più dettagliate sulla configurazione di avvisi, vedere [Creazione di avvisi in Monitoraggio di Azure per i servizi Azure - Portale di Azure](../monitoring-and-diagnostics/insights-alerts-portal.md).</span><span class="sxs-lookup"><span data-stu-id="57e49-273">More detailed documentation about configuring alerts can be found at [Create alerts in Azure Monitor for Azure services - Azure portal](../monitoring-and-diagnostics/insights-alerts-portal.md).</span></span> <span data-ttu-id="57e49-274">Immettere i valori seguenti nel pannello **Regola di avviso** e fare clic su **OK**.</span><span class="sxs-lookup"><span data-stu-id="57e49-274">Enter the following values in the **Alert rule** blade, and then select **OK**.</span></span>

  |<span data-ttu-id="57e49-275">**Impostazione**</span><span class="sxs-lookup"><span data-stu-id="57e49-275">**Setting**</span></span> | <span data-ttu-id="57e49-276">**Valore**</span><span class="sxs-lookup"><span data-stu-id="57e49-276">**Value**</span></span> | <span data-ttu-id="57e49-277">**Dettagli**</span><span class="sxs-lookup"><span data-stu-id="57e49-277">**Details**</span></span> |
  |---|---|---|
  |<span data-ttu-id="57e49-278">**Nome**</span><span class="sxs-lookup"><span data-stu-id="57e49-278">**Name**</span></span>|<span data-ttu-id="57e49-279">TCP_Segments_Sent_Exceeded</span><span class="sxs-lookup"><span data-stu-id="57e49-279">TCP_Segments_Sent_Exceeded</span></span>|<span data-ttu-id="57e49-280">Nome della regola di avviso.</span><span class="sxs-lookup"><span data-stu-id="57e49-280">Name of the alert rule.</span></span>|
  |<span data-ttu-id="57e49-281">**Descrizione**</span><span class="sxs-lookup"><span data-stu-id="57e49-281">**Description**</span></span>|<span data-ttu-id="57e49-282">Soglia superata segmenti TCP inviati</span><span class="sxs-lookup"><span data-stu-id="57e49-282">TCP segments sent exceeded threshold</span></span>|<span data-ttu-id="57e49-283">Descrizione della regola di avviso.</span><span class="sxs-lookup"><span data-stu-id="57e49-283">The description for the alert rule.</span></span>||
  |<span data-ttu-id="57e49-284">**Metrica**</span><span class="sxs-lookup"><span data-stu-id="57e49-284">**Metric**</span></span>|<span data-ttu-id="57e49-285">Segmenti TCP inviati</span><span class="sxs-lookup"><span data-stu-id="57e49-285">TCP segments sent</span></span>| <span data-ttu-id="57e49-286">La metrica da utilizzare per attivare l'avviso.</span><span class="sxs-lookup"><span data-stu-id="57e49-286">The metric to use to trigger the alert.</span></span> |
  |<span data-ttu-id="57e49-287">**Condition**</span><span class="sxs-lookup"><span data-stu-id="57e49-287">**Condition**</span></span>|<span data-ttu-id="57e49-288">Maggiore di</span><span class="sxs-lookup"><span data-stu-id="57e49-288">Greater than</span></span>| <span data-ttu-id="57e49-289">La condizione da utilizzare per valutare la metrica.</span><span class="sxs-lookup"><span data-stu-id="57e49-289">The condition to use when evaluating the metric.</span></span>|
  |<span data-ttu-id="57e49-290">**Soglia**</span><span class="sxs-lookup"><span data-stu-id="57e49-290">**Threshold**</span></span>|<span data-ttu-id="57e49-291">100</span><span class="sxs-lookup"><span data-stu-id="57e49-291">100</span></span>| <span data-ttu-id="57e49-292">Valore della metrica che attiva l'avviso.</span><span class="sxs-lookup"><span data-stu-id="57e49-292">The  value of the metric that triggers the alert.</span></span> <span data-ttu-id="57e49-293">Deve trattarsi di un valore valido per l'ambiente in uso.</span><span class="sxs-lookup"><span data-stu-id="57e49-293">This value should be set to a valid value for your environment.</span></span>|
  |<span data-ttu-id="57e49-294">**Periodo**</span><span class="sxs-lookup"><span data-stu-id="57e49-294">**Period**</span></span>|<span data-ttu-id="57e49-295">Negli ultimi cinque minuti</span><span class="sxs-lookup"><span data-stu-id="57e49-295">Over the last five minutes</span></span>| <span data-ttu-id="57e49-296">Determina il periodo in cui cercare la soglia per la metrica.</span><span class="sxs-lookup"><span data-stu-id="57e49-296">Determines the period in which to look for the threshold on the metric.</span></span>|
  |<span data-ttu-id="57e49-297">**Webhook**</span><span class="sxs-lookup"><span data-stu-id="57e49-297">**Webhook**</span></span>|<span data-ttu-id="57e49-298">[URL webhook dell'app per le funzioni]</span><span class="sxs-lookup"><span data-stu-id="57e49-298">[webhook URL from function app]</span></span>| <span data-ttu-id="57e49-299">URL webhook dall'app per le funzioni creata nei passaggi precedenti.</span><span class="sxs-lookup"><span data-stu-id="57e49-299">The webhook URL from the function app that was created in the previous steps.</span></span>|

> [!NOTE]
> <span data-ttu-id="57e49-300">La metrica di segmenti TCP non è abilitata per impostazione predefinita.</span><span class="sxs-lookup"><span data-stu-id="57e49-300">The TCP segments metric is not enabled by default.</span></span> <span data-ttu-id="57e49-301">Per altre informazioni su come abilitare metriche aggiuntive, vedere [Abilitare il monitoraggio e la diagnostica](../monitoring-and-diagnostics/insights-how-to-use-diagnostics.md).</span><span class="sxs-lookup"><span data-stu-id="57e49-301">Learn more about how to enable additional metrics by visiting [Enable monitoring and diagnostics](../monitoring-and-diagnostics/insights-how-to-use-diagnostics.md).</span></span>

## <a name="review-the-results"></a><span data-ttu-id="57e49-302">Esaminare i risultati</span><span class="sxs-lookup"><span data-stu-id="57e49-302">Review the results</span></span>

<span data-ttu-id="57e49-303">Dopo i criteri di attivazione dell'avviso, viene creata l'acquisizione di pacchetti.</span><span class="sxs-lookup"><span data-stu-id="57e49-303">After the criteria for the alert triggers, a packet capture is created.</span></span> <span data-ttu-id="57e49-304">Passare a Network Watcher e quindi selezionare **Acquisizione pacchetti**.</span><span class="sxs-lookup"><span data-stu-id="57e49-304">Go to Network Watcher, and then select **Packet capture**.</span></span> <span data-ttu-id="57e49-305">In questa pagina è possibile fare clic sul collegamento del file di acquisizione pacchetti per scaricare l'acquisizione di pacchetti.</span><span class="sxs-lookup"><span data-stu-id="57e49-305">On this page, you can select the packet capture file link to download the packet capture.</span></span>

![Visualizzare l'acquisizione di pacchetti][functions14]

<span data-ttu-id="57e49-307">Se il file di acquisizione è archiviato in locale, è possibile recuperarlo accedendo alla macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="57e49-307">If the capture file is stored locally, you can retrieve it by signing in to the virtual machine.</span></span>

<span data-ttu-id="57e49-308">Per istruzioni relative al download di file dagli account di archiviazione di Azure, vedere [Introduzione all'archivio BLOB di Azure con .NET](../storage/blobs/storage-dotnet-how-to-use-blobs.md).</span><span class="sxs-lookup"><span data-stu-id="57e49-308">For instructions about downloading files from Azure storage accounts, see [Get started with Azure Blob storage using .NET](../storage/blobs/storage-dotnet-how-to-use-blobs.md).</span></span> <span data-ttu-id="57e49-309">Un altro strumento è [Storage Explorer](http://storageexplorer.com/).</span><span class="sxs-lookup"><span data-stu-id="57e49-309">Another tool you can use is [Storage Explorer](http://storageexplorer.com/).</span></span>

<span data-ttu-id="57e49-310">Dopo il download dell'acquisizione, è possibile visualizzarla con qualsiasi strumento per la lettura di un file **.cap**.</span><span class="sxs-lookup"><span data-stu-id="57e49-310">After your capture has been downloaded, you can view it by using any tool that can read a **.cap** file.</span></span> <span data-ttu-id="57e49-311">Di seguito i collegamenti a due di questi strumenti:</span><span class="sxs-lookup"><span data-stu-id="57e49-311">Following are links to two of these tools:</span></span>

- [<span data-ttu-id="57e49-312">Microsoft Message Analyzer</span><span class="sxs-lookup"><span data-stu-id="57e49-312">Microsoft Message Analyzer</span></span>](https://technet.microsoft.com/library/jj649776.aspx)
- [<span data-ttu-id="57e49-313">WireShark</span><span class="sxs-lookup"><span data-stu-id="57e49-313">WireShark</span></span>](https://www.wireshark.org/)

## <a name="next-steps"></a><span data-ttu-id="57e49-314">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="57e49-314">Next steps</span></span>

<span data-ttu-id="57e49-315">Per informazioni su come visualizzare le acquisizioni di pacchetti, vedere [Analisi delle acquisizioni di pacchetti con Wireshark](network-watcher-deep-packet-inspection.md).</span><span class="sxs-lookup"><span data-stu-id="57e49-315">Learn how to view your packet captures by visiting [Packet capture analysis with Wireshark](network-watcher-deep-packet-inspection.md).</span></span>


[1]: ./media/network-watcher-alert-triggered-packet-capture/figure1.png
[1-1]: ./media/network-watcher-alert-triggered-packet-capture/figure1-1.png
[2]: ./media/network-watcher-alert-triggered-packet-capture/figure2.png
[3]: ./media/network-watcher-alert-triggered-packet-capture/figure3.png
[functions1]:./media/network-watcher-alert-triggered-packet-capture/functions1.png
[functions2]:./media/network-watcher-alert-triggered-packet-capture/functions2.png
[functions3]:./media/network-watcher-alert-triggered-packet-capture/functions3.png
[functions4]:./media/network-watcher-alert-triggered-packet-capture/functions4.png
[functions5]:./media/network-watcher-alert-triggered-packet-capture/functions5.png
[functions6]:./media/network-watcher-alert-triggered-packet-capture/functions6.png
[functions7]:./media/network-watcher-alert-triggered-packet-capture/functions7.png
[functions8]:./media/network-watcher-alert-triggered-packet-capture/functions8.png
[functions9]:./media/network-watcher-alert-triggered-packet-capture/functions9.png
[functions10]:./media/network-watcher-alert-triggered-packet-capture/functions10.png
[functions11]:./media/network-watcher-alert-triggered-packet-capture/functions11.png
[functions12]:./media/network-watcher-alert-triggered-packet-capture/functions12.png
[functions13]:./media/network-watcher-alert-triggered-packet-capture/functions13.png
[functions14]:./media/network-watcher-alert-triggered-packet-capture/functions14.png
[scenario]:./media/network-watcher-alert-triggered-packet-capture/scenario.png

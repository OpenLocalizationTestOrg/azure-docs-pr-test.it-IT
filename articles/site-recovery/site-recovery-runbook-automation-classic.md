---
title: Aggiungere runbook di Automazione di Azure ai piani di ripristino nel portale classico | Documentazione Microsoft
description: "In questo articolo viene descritto come Azure Site Recovery consente ora di estendere i piani di ripristino tramite Automazione di Azure per completare attività complesse durante il ripristino in Azure"
services: site-recovery
documentationcenter: 
author: ruturaj
manager: gauravd
editor: 
ms.assetid: f24eaa62-9dea-4fce-92e1-a72513ca0289
ms.service: site-recovery
ms.devlang: powershell
ms.tgt_pltfrm: na
ms.topic: article
ms.workload: storage-backup-recovery
ms.date: 08/11/2017
ms.author: ruturajd
ms.openlocfilehash: 0a248e7c3f39a35ac10dc6ac64e5cef7d152e033
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/18/2017
---
# <a name="add-azure-automation-runbooks-to-recovery-plans-in-the-classic-portal"></a><span data-ttu-id="9daeb-103">Aggiungere runbook di Automazione di Azure ai piani di ripristino nel portale classico</span><span class="sxs-lookup"><span data-stu-id="9daeb-103">Add Azure automation runbooks to recovery plans in the classic portal</span></span>
<span data-ttu-id="9daeb-104">In questa esercitazione viene descritto come Azure Site Recovery si integra con Automazione di Azure per fornire estendibilità ai piani di ripristino.</span><span class="sxs-lookup"><span data-stu-id="9daeb-104">This tutorial describes how Azure Site Recovery integrates with Azure Automation to provide extensibility to recovery plans.</span></span> <span data-ttu-id="9daeb-105">I piani di ripristino possono gestire il ripristino delle macchine virtuali protette tramite Azure Site Recovery per la replica nel cloud secondario e la replica negli scenari di Azure.</span><span class="sxs-lookup"><span data-stu-id="9daeb-105">Recovery plans can orchestrate recovery of your virtual machines protected using Azure Site Recovery for both replication to secondary cloud and replication to Azure scenarios.</span></span> <span data-ttu-id="9daeb-106">Consentono inoltre di effettuare il ripristino **costantemente accurato**, **ripetibile** e **automatizzato**.</span><span class="sxs-lookup"><span data-stu-id="9daeb-106">They also help in making the recovery **consistently accurate**, **repeatable**, and **automated**.</span></span> <span data-ttu-id="9daeb-107">Se viene eseguito il failover delle macchine virtuali in Azure, l’integrazione con Automazione di Azure si estende ai piani di ripristino e offre la possibilità di eseguire i runbook, consentendo in tal modo attività di automazione efficaci.</span><span class="sxs-lookup"><span data-stu-id="9daeb-107">If you are failing over your virtual machines to Azure, integration with Azure Automation extends the recovery plans and gives you capability to execute runbooks, thus allowing powerful automation tasks.</span></span>

<span data-ttu-id="9daeb-108">Se non si è ancora sentito parlare di Automazione di Azure, effettuare l'iscrizione [qui](https://azure.microsoft.com/services/automation/) e scaricare gli script di esempio [qui](https://azure.microsoft.com/documentation/scripts/).</span><span class="sxs-lookup"><span data-stu-id="9daeb-108">If you have not heard about Azure Automation yet, sign up [here](https://azure.microsoft.com/services/automation/) and download their sample scripts [here](https://azure.microsoft.com/documentation/scripts/).</span></span> <span data-ttu-id="9daeb-109">Altre informazioni su [Azure Site Recovery](https://azure.microsoft.com/services/site-recovery/) e su come gestire il ripristino in Azure usando piani di ripristino sono disponibili [qui](https://azure.microsoft.com/blog/?p=166264).</span><span class="sxs-lookup"><span data-stu-id="9daeb-109">Read more about [Azure Site Recovery](https://azure.microsoft.com/services/site-recovery/) and how to orchestrate recovery to Azure using recovery plans [here](https://azure.microsoft.com/blog/?p=166264).</span></span>

<span data-ttu-id="9daeb-110">In questa breve esercitazione verrà illustrato come integrare i runbook di Automazione di Azure nei piani di ripristino.</span><span class="sxs-lookup"><span data-stu-id="9daeb-110">In this short tutorial, we will look at how you can integrate Azure Automation runbooks into recovery plans.</span></span> <span data-ttu-id="9daeb-111">Verranno automatizzate attività semplici che in precedenza richiedevano un intervento manuale e verrà illustrato come convertire un ripristino in più passaggi in un'azione di ripristino a singolo clic.</span><span class="sxs-lookup"><span data-stu-id="9daeb-111">We will automate simple tasks that earlier required manual intervention and see how to convert a multi step recovery into a single-click recovery action.</span></span> <span data-ttu-id="9daeb-112">Verrà esaminato inoltre come risolvere eventuali problemi di un semplice script.</span><span class="sxs-lookup"><span data-stu-id="9daeb-112">We will also look at how you can troubleshoot a simple script if it goes wrong.</span></span>

## <a name="protect-the-application-to-azure"></a><span data-ttu-id="9daeb-113">Proteggere l'applicazione in Azure</span><span class="sxs-lookup"><span data-stu-id="9daeb-113">Protect the application to Azure</span></span>
<span data-ttu-id="9daeb-114">Si inizierà con una semplice applicazione costituita da due macchine virtuali.</span><span class="sxs-lookup"><span data-stu-id="9daeb-114">Let us begin with a simple application consisting of two virtual machines.</span></span> <span data-ttu-id="9daeb-115">In questo caso, viene usata un'applicazione HRweb di Fabrikam.</span><span class="sxs-lookup"><span data-stu-id="9daeb-115">Here, we have a HRweb application of Fabrikam.</span></span> <span data-ttu-id="9daeb-116">Fabrikam-HRweb-frontend e Fabrikam-Hrweb-backend sono le due macchine virtuali protette in Azure tramite Azure Site Recovery.</span><span class="sxs-lookup"><span data-stu-id="9daeb-116">Fabrikam-HRweb-frontend and Fabrikam-Hrweb-backend are the two virtual machines protected to Azure using Azure Site Recovery.</span></span> <span data-ttu-id="9daeb-117">Per proteggere le macchine virtuali tramite Azure Site Recover, attenersi alla procedura seguente.</span><span class="sxs-lookup"><span data-stu-id="9daeb-117">To protect the virtual machines using Azure Site Recovery, follow the steps below.</span></span>

1. <span data-ttu-id="9daeb-118">Abilitare la protezione per le macchine virtuali.</span><span class="sxs-lookup"><span data-stu-id="9daeb-118">Enable protection for your virtual machines.</span></span>
2. <span data-ttu-id="9daeb-119">Assicurarsi che le macchine virtuali abbiano completato la replica iniziale e stiano eseguendo la replica.</span><span class="sxs-lookup"><span data-stu-id="9daeb-119">Ensure that the virtual machines have completed initial replication and are replicating.</span></span>
3. <span data-ttu-id="9daeb-120">Attendere che la replica iniziale venga completata e che lo stato della replica sia Protetto.</span><span class="sxs-lookup"><span data-stu-id="9daeb-120">Wait till the initial replication completes and the Replication status says Protected.</span></span>

## ![](media/site-recovery-runbook-automation/01.png)
<span data-ttu-id="9daeb-121">In questa esercitazione si creerà un piano di ripristino per l'applicazione Fabrikam HRweb per eseguire il failover dell'applicazione in Azure.</span><span class="sxs-lookup"><span data-stu-id="9daeb-121">In this tutorial, we will create a recovery plan for the Fabrikam HRweb application to failover the application to Azure.</span></span> <span data-ttu-id="9daeb-122">Il piano di ripristino verrà quindi integrato con un runbook che creerà un endpoint sulla macchina virtuale di Azure sottoposta a failover, per utilizzare le pagine web sulla porta 80.</span><span class="sxs-lookup"><span data-stu-id="9daeb-122">Then we will integrate it with a runbook that will create an endpoint on the failed over Azure virtual machine to serve web pages at port 80.</span></span>

<span data-ttu-id="9daeb-123">Innanzitutto, verrà creato un piano di ripristino per l’applicazione.</span><span class="sxs-lookup"><span data-stu-id="9daeb-123">First, let's create a recovery plan for our application.</span></span>

## <a name="create-the-recovery-plan"></a><span data-ttu-id="9daeb-124">Creare il piano di ripristino</span><span class="sxs-lookup"><span data-stu-id="9daeb-124">Create the recovery plan</span></span>
<span data-ttu-id="9daeb-125">Per ripristinare l'applicazione in Azure, è necessario creare un piano di ripristino.</span><span class="sxs-lookup"><span data-stu-id="9daeb-125">To recover the application to Azure, you need to create a recovery plan.</span></span>
<span data-ttu-id="9daeb-126">Usando un piano di ripristino, è possibile specificare l'ordine di ripristino delle macchine virtuali.</span><span class="sxs-lookup"><span data-stu-id="9daeb-126">Using a recovery plan you can specify the order of recovery of the virtual machines.</span></span> <span data-ttu-id="9daeb-127">La macchina virtuale inserita nel gruppo 1 verrà ripristinata e avviata per prima e quindi seguirà la macchina virtuale nel gruppo 2.</span><span class="sxs-lookup"><span data-stu-id="9daeb-127">The virtual machine placed in group 1 will recover and start first, and then the virtual machine in group 2 will follow.</span></span>

<span data-ttu-id="9daeb-128">Creare un piano di ripristino simile al seguente.</span><span class="sxs-lookup"><span data-stu-id="9daeb-128">Create a Recovery Plan that looks like below.</span></span>

![](media/site-recovery-runbook-automation/12.png)

<span data-ttu-id="9daeb-129">Per ulteriori informazioni sui piani di ripristino, leggere la documentazione [qui](https://msdn.microsoft.com/library/azure/dn788799.aspx "qui").</span><span class="sxs-lookup"><span data-stu-id="9daeb-129">To read more about recovery plans, read documentation [here](https://msdn.microsoft.com/library/azure/dn788799.aspx "here").</span></span>

<span data-ttu-id="9daeb-130">Quindi, verranno creati gli elementi necessari in Automazione di Azure.</span><span class="sxs-lookup"><span data-stu-id="9daeb-130">Next, let's create the necessary artifacts in Azure Automation.</span></span>

## <a name="create-the-automation-account-and-its-assets"></a><span data-ttu-id="9daeb-131">Creare l'account di automazione e i relativi asset</span><span class="sxs-lookup"><span data-stu-id="9daeb-131">Create the automation account and its assets</span></span>
<span data-ttu-id="9daeb-132">Per creare i runbook è necessario un account di Automazione di Azure.</span><span class="sxs-lookup"><span data-stu-id="9daeb-132">You need an Azure Automation account to create runbooks.</span></span> <span data-ttu-id="9daeb-133">Se non si dispone già di un account, passare alla scheda Automazione di Azure identificata da ![](media/site-recovery-runbook-automation/02.png)e creare un nuovo account.</span><span class="sxs-lookup"><span data-stu-id="9daeb-133">If you do not already have an account, navigate to Azure Automation tab denoted by ![](media/site-recovery-runbook-automation/02.png)and create a new account.</span></span>

1. <span data-ttu-id="9daeb-134">Assegnare all'account un nome con cui identificarlo.</span><span class="sxs-lookup"><span data-stu-id="9daeb-134">Give the account a name to identify with.</span></span>
2. <span data-ttu-id="9daeb-135">Specificare un'area geografica in cui si desidera inserire l'account.</span><span class="sxs-lookup"><span data-stu-id="9daeb-135">Specify a geographical region where you want to place the account.</span></span>

<span data-ttu-id="9daeb-136">Si consiglia di inserire l'account nella stessa area dell’insieme di credenziali per il ripristino automatico di sistema.</span><span class="sxs-lookup"><span data-stu-id="9daeb-136">It is recommended to place the account in the same region as the ASR vault.</span></span>

![](media/site-recovery-runbook-automation/03.png)

<span data-ttu-id="9daeb-137">Successivamente, creare gli asset seguenti nell’account.</span><span class="sxs-lookup"><span data-stu-id="9daeb-137">Next, create the following assets in the Account.</span></span>

### <a name="add-a-subscription-name-as-asset"></a><span data-ttu-id="9daeb-138">Aggiungere un nome di sottoscrizione come asset</span><span class="sxs-lookup"><span data-stu-id="9daeb-138">Add a subscription name as asset</span></span>
1. <span data-ttu-id="9daeb-139">Aggiungere una nuova impostazione ![](media/site-recovery-runbook-automation/04.png) negli asset di Automazione di Azure e selezionare ![](media/site-recovery-runbook-automation/05.png)</span><span class="sxs-lookup"><span data-stu-id="9daeb-139">Add a new setting ![](media/site-recovery-runbook-automation/04.png) in the Azure Automation Assets and select to ![](media/site-recovery-runbook-automation/05.png)</span></span>
2. <span data-ttu-id="9daeb-140">Selezionare **String**</span><span class="sxs-lookup"><span data-stu-id="9daeb-140">Select the variable type as **String**</span></span>
3. <span data-ttu-id="9daeb-141">Specificare **AzureSubscriptionName**</span><span class="sxs-lookup"><span data-stu-id="9daeb-141">Specify variable name as **AzureSubscriptionName**</span></span>

   ![](media/site-recovery-runbook-automation/06.png)
4. <span data-ttu-id="9daeb-142">Specificare il nome effettivo della sottoscrizione di Azure come valore della variabile.</span><span class="sxs-lookup"><span data-stu-id="9daeb-142">Specify your actual Azure Subscription name as the variable value.</span></span>

   ![](media/site-recovery-runbook-automation/07_1.png)

<span data-ttu-id="9daeb-143">È possibile identificare il nome della sottoscrizione dalla pagina delle impostazioni dell'account nel portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="9daeb-143">You can identify the name of your subscription from the settings page of your account on the Azure portal.</span></span>

### <a name="add-an-azure-login-credential-as-asset"></a><span data-ttu-id="9daeb-144">Aggiungere una credenziale di accesso di Azure come asset</span><span class="sxs-lookup"><span data-stu-id="9daeb-144">Add an Azure login credential as asset</span></span>
<span data-ttu-id="9daeb-145">Automazione di Azure usa Azure PowerShell per connettersi alla sottoscrizione e opera sugli elementi disponibili.</span><span class="sxs-lookup"><span data-stu-id="9daeb-145">Azure Automation uses Azure PowerShell to connect to the subscription and operates on the artifacts there.</span></span> <span data-ttu-id="9daeb-146">A tale scopo, è necessario eseguire l'autenticazione usando l'account Microsoft o un account aziendale o dell’istituto di istruzione.</span><span class="sxs-lookup"><span data-stu-id="9daeb-146">For this, you need to authenticate using your Microsoft account or a work or school account.</span></span>
<span data-ttu-id="9daeb-147">È possibile archiviare le credenziali dell'account in un asset da utilizzare in modo sicuro nel runbook.</span><span class="sxs-lookup"><span data-stu-id="9daeb-147">You can store the account credentials in an asset to be used securely by the runbook.</span></span>

1. <span data-ttu-id="9daeb-148">Aggiungere una nuova impostazione ![](media/site-recovery-runbook-automation/04.png) negli asset di Automazione di Azure e selezionare ![](media/site-recovery-runbook-automation/09.png)</span><span class="sxs-lookup"><span data-stu-id="9daeb-148">Add a new setting ![](media/site-recovery-runbook-automation/04.png) in the Azure Automation Assets and select ![](media/site-recovery-runbook-automation/09.png)</span></span>
2. <span data-ttu-id="9daeb-149">Selezionare **Credenziali per Windows PowerShell**</span><span class="sxs-lookup"><span data-stu-id="9daeb-149">Select the Credential type as **Windows PowerShell Credential**</span></span>
3. <span data-ttu-id="9daeb-150">Specificare il nome **AzureCredential**</span><span class="sxs-lookup"><span data-stu-id="9daeb-150">Specify the name as **AzureCredential**</span></span>

   ![](media/site-recovery-runbook-automation/10.png)
4. <span data-ttu-id="9daeb-151">Specificare il nome utente e la password con cui effettuare l'accesso.</span><span class="sxs-lookup"><span data-stu-id="9daeb-151">Specify the username and password to sign-in with.</span></span>

<span data-ttu-id="9daeb-152">Entrambe queste impostazioni sono ora disponibili negli asset.</span><span class="sxs-lookup"><span data-stu-id="9daeb-152">Now both these settings are available in your assets.</span></span>

![](media/site-recovery-runbook-automation/11.png)

<span data-ttu-id="9daeb-153">Altre informazioni su come connettersi alla sottoscrizione tramite PowerShell sono disponibili [qui](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="9daeb-153">More information about how to connect to your subscription via PowerShell is given [here](/powershell/azure/overview).</span></span>

<span data-ttu-id="9daeb-154">Successivamente, verrà creato un runbook in Automazione di Azure che può aggiungere un endpoint per la macchina virtuale front-end dopo il failover.</span><span class="sxs-lookup"><span data-stu-id="9daeb-154">Next, you will create a runbook in Azure Automation that can add an endpoint for the front-end virtual machine after failover.</span></span>

## <a name="azure-automation-context"></a><span data-ttu-id="9daeb-155">Contesto di Automazione di Azure</span><span class="sxs-lookup"><span data-stu-id="9daeb-155">Azure automation context</span></span>
<span data-ttu-id="9daeb-156">Il ripristino automatico di sistema passa una variabile di contesto al runbook per consentire all’utente di scrivere script deterministici.</span><span class="sxs-lookup"><span data-stu-id="9daeb-156">ASR passes a context variable to the runbook to help you write deterministic scripts.</span></span> <span data-ttu-id="9daeb-157">Si potrebbe sostenere che i nomi del servizio cloud e della macchina virtuale siano prevedibili, ma ciò non si verifica sempre per determinati scenari, come quello in cui il nome della macchina virtuale potrebbe essere stato modificato a causa di caratteri non supportati in Azure.</span><span class="sxs-lookup"><span data-stu-id="9daeb-157">One could argue that the names of the Cloud Service and the Virtual Machine are predictable, but happens that it is not always the case owing to certain scenarios such as the one where the name of the virtual machine name might have changed due to unsupported characters in Azure.</span></span> <span data-ttu-id="9daeb-158">Di conseguenza, queste informazioni vengono passate al piano di ripristino automatico di sistema come parte del *contesto*.</span><span class="sxs-lookup"><span data-stu-id="9daeb-158">Hence this information is passed to the ASR recovery plan as part of the *context*.</span></span>

<span data-ttu-id="9daeb-159">La variabile di contesto avrà un aspetto simile a quello riportato nell’esempio seguente.</span><span class="sxs-lookup"><span data-stu-id="9daeb-159">Below is an example of how the context variable looks.</span></span>

        {"RecoveryPlanName":"hrweb-recovery",

        "FailoverType":"Test",

        "FailoverDirection":"PrimaryToSecondary",

        "GroupId":"1",

        "VmMap":{"7a1069c6-c1d6-49c5-8c5d-33bfce8dd183":

                {"CloudServiceName":"pod02hrweb-Chicago-test",

                "RoleName":"Fabrikam-Hrweb-frontend-test"}

                }

        }


<span data-ttu-id="9daeb-160">La tabella che segue contiene il nome e la descrizione di ciascuna variabile nel contesto.</span><span class="sxs-lookup"><span data-stu-id="9daeb-160">The table below contains name and description for each variable in the context.</span></span>

| <span data-ttu-id="9daeb-161">**Nome variabile**</span><span class="sxs-lookup"><span data-stu-id="9daeb-161">**Variable name**</span></span> | <span data-ttu-id="9daeb-162">**Descrizione**</span><span class="sxs-lookup"><span data-stu-id="9daeb-162">**Description**</span></span> |
| --- | --- |
| <span data-ttu-id="9daeb-163">RecoveryPlanName</span><span class="sxs-lookup"><span data-stu-id="9daeb-163">RecoveryPlanName</span></span> |<span data-ttu-id="9daeb-164">Nome del piano di esecuzione.</span><span class="sxs-lookup"><span data-stu-id="9daeb-164">Name of plan being run.</span></span> <span data-ttu-id="9daeb-165">Consente di agire in base al nome utilizzando lo stesso script</span><span class="sxs-lookup"><span data-stu-id="9daeb-165">Helps you take action based on name using the same script</span></span> |
| <span data-ttu-id="9daeb-166">FailoverType</span><span class="sxs-lookup"><span data-stu-id="9daeb-166">FailoverType</span></span> |<span data-ttu-id="9daeb-167">Specifica se il failover è di test, pianificato o non pianificato.</span><span class="sxs-lookup"><span data-stu-id="9daeb-167">Specifies whether the failover is test, planned, or unplanned.</span></span> |
| <span data-ttu-id="9daeb-168">FailoverDirection</span><span class="sxs-lookup"><span data-stu-id="9daeb-168">FailoverDirection</span></span> |<span data-ttu-id="9daeb-169">Specifica se il ripristino avviene su primario o secondario</span><span class="sxs-lookup"><span data-stu-id="9daeb-169">Specify whether recovery is to primary or secondary</span></span> |
| <span data-ttu-id="9daeb-170">GroupID</span><span class="sxs-lookup"><span data-stu-id="9daeb-170">GroupID</span></span> |<span data-ttu-id="9daeb-171">Identifica il numero del gruppo all'interno del piano di ripristino quando il piano è in esecuzione</span><span class="sxs-lookup"><span data-stu-id="9daeb-171">Identify the group number within the recovery plan when the plan is running</span></span> |
| <span data-ttu-id="9daeb-172">VmMap</span><span class="sxs-lookup"><span data-stu-id="9daeb-172">VmMap</span></span> |<span data-ttu-id="9daeb-173">Array di tutte le macchine virtuali presenti nel gruppo.</span><span class="sxs-lookup"><span data-stu-id="9daeb-173">Array of all the virtual machines in the group</span></span> |
| <span data-ttu-id="9daeb-174">VMMap key</span><span class="sxs-lookup"><span data-stu-id="9daeb-174">VMMap key</span></span> |<span data-ttu-id="9daeb-175">Chiave univoca (GUID) per ciascuna VM.</span><span class="sxs-lookup"><span data-stu-id="9daeb-175">Unique key (GUID) for each VM.</span></span> <span data-ttu-id="9daeb-176">È uguale all'ID di VMM della macchina virtuale, se applicabile.</span><span class="sxs-lookup"><span data-stu-id="9daeb-176">It's the same as the VMM ID of the virtual machine where applicable.</span></span> |
| <span data-ttu-id="9daeb-177">RoleName</span><span class="sxs-lookup"><span data-stu-id="9daeb-177">RoleName</span></span> |<span data-ttu-id="9daeb-178">Nome della VM di Azure in fase di ripristino</span><span class="sxs-lookup"><span data-stu-id="9daeb-178">Name of the Azure VM that's being recovered</span></span> |
| <span data-ttu-id="9daeb-179">CloudServiceName</span><span class="sxs-lookup"><span data-stu-id="9daeb-179">CloudServiceName</span></span> |<span data-ttu-id="9daeb-180">Nome servizio cloud di Azure in cui viene creata la macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="9daeb-180">Azure Cloud Service name under which the virtual machine is created.</span></span> |

<span data-ttu-id="9daeb-181">Per identificare la chiave VmMap nel contesto, è anche possibile andare alla pagina delle proprietà della macchina virtuale in Ripristino automatico di sistema e analizzare la proprietà VM GUID.</span><span class="sxs-lookup"><span data-stu-id="9daeb-181">To identify the VmMap Key in the context you could also go to the VM properties page in ASR and look at the VM GUID property.</span></span>

![](media/site-recovery-runbook-automation/13.png)

## <a name="author-an-automation-runbook"></a><span data-ttu-id="9daeb-182">Creare un runbook di Automazione</span><span class="sxs-lookup"><span data-stu-id="9daeb-182">Author an Automation runbook</span></span>
<span data-ttu-id="9daeb-183">A questo punto creare il runbook per aprire la porta 80 nella macchina virtuale front-end.</span><span class="sxs-lookup"><span data-stu-id="9daeb-183">Now create the runbook to open port 80 on the front-end virtual machine.</span></span>

1. <span data-ttu-id="9daeb-184">Creare un nuovo runbook nell'account di Automazione di Azure con il nome **OpenPort80**</span><span class="sxs-lookup"><span data-stu-id="9daeb-184">Create a new runbook in the Azure Automation account with the name **OpenPort80**</span></span>

   ![](media/site-recovery-runbook-automation/14.png)
2. <span data-ttu-id="9daeb-185">Passare alla visualizzazione Autore del runbook e inserire la modalità bozza.</span><span class="sxs-lookup"><span data-stu-id="9daeb-185">Navigate to the Author view of the runbook and enter the draft mode.</span></span>
3. <span data-ttu-id="9daeb-186">Specificare innanzitutto la variabile da utilizzare come contesto del piano di ripristino</span><span class="sxs-lookup"><span data-stu-id="9daeb-186">First specify the variable to use as the recovery plan context</span></span>

   ```
       param (
           [Object]$RecoveryPlanContext
       )

   ```
4. <span data-ttu-id="9daeb-187">Quindi, connettersi alla sottoscrizione tramite le credenziali e il nome della sottoscrizione</span><span class="sxs-lookup"><span data-stu-id="9daeb-187">Next connect to the subscription using the credential and subscription name</span></span>

   ```
       $Cred = Get-AutomationPSCredential -Name 'AzureCredential'

       # Connect to Azure
       $AzureAccount = Add-AzureAccount -Credential $Cred
       $AzureSubscriptionName = Get-AutomationVariable –Name ‘AzureSubscriptionName’
       Select-AzureSubscription -SubscriptionName $AzureSubscriptionName
   ```

   <span data-ttu-id="9daeb-188">Si noti che qui vengono usati gli asset di Azure: **AzureCredential** e **AzureSubscriptionName**.</span><span class="sxs-lookup"><span data-stu-id="9daeb-188">Note that you use the Azure assets – **AzureCredential** and **AzureSubscriptionName** here.</span></span>
5. <span data-ttu-id="9daeb-189">Specificare i dettagli di endpoint e il GUID della macchina virtuale per il quale si vuole esporre l'endpoint,</span><span class="sxs-lookup"><span data-stu-id="9daeb-189">Now specify the endpoint details and the GUID of the virtual machine for which you want to expose the endpoint.</span></span> <span data-ttu-id="9daeb-190">in questo caso la macchina virtuale front-end.</span><span class="sxs-lookup"><span data-stu-id="9daeb-190">In this case the front-end virtual machine.</span></span>

   ```
       # Specify the parameters to be used by the script
       $AEProtocol = "TCP"
       $AELocalPort = 80
       $AEPublicPort = 80
       $AEName = "Port 80 for HTTP"
       $VMGUID = "7a1069c6-c1d6-49c5-8c5d-33bfce8dd183"
   ```

   <span data-ttu-id="9daeb-191">Vengono specificati il protocollo di endpoint di Azure, la porta locale nella macchina virtuale e la porta pubblica mappata.</span><span class="sxs-lookup"><span data-stu-id="9daeb-191">This specifies the Azure endpoint protocol, local port on the VM and its mapped public port.</span></span> <span data-ttu-id="9daeb-192">Queste variabili rappresentano i parametri richiesti dai comandi di Azure che consentono di aggiungere endpoint alle macchine virtuali.</span><span class="sxs-lookup"><span data-stu-id="9daeb-192">These variables are parameters     required by the Azure commands that add endpoints to VMs.</span></span> <span data-ttu-id="9daeb-193">VMGUID contiene il GUID della macchina virtuale su cui è necessario operare.</span><span class="sxs-lookup"><span data-stu-id="9daeb-193">The VMGUID holds the GUID of the virtual machine you need to operate on.</span></span>
6. <span data-ttu-id="9daeb-194">Lo script estrae ora il contesto per la proprietà VM GUID specificata e crea un endpoint nella macchina virtuale a cui fa riferimento.</span><span class="sxs-lookup"><span data-stu-id="9daeb-194">The script will now extract the context for the given VM GUID and create an endpoint on the virtual machine referenced by it.</span></span>

   ```
       #Read the VM GUID from the context
       $VM = $RecoveryPlanContext.VmMap.$VMGUID

       if ($VM -ne $null)
       {
           # Invoke pipeline commands within an InlineScript

           $EndpointStatus = InlineScript {
               # Invoke the necessary pipeline commands to add a Azure Endpoint to a specified Virtual Machine
               # Commands include: Get-AzureVM | Add-AzureEndpoint | Update-AzureVM (including parameters)

               $Status = Get-AzureVM -ServiceName $Using:VM.CloudServiceName -Name $Using:VM.RoleName | `
                   Add-AzureEndpoint -Name $Using:AEName -Protocol $Using:AEProtocol -PublicPort $Using:AEPublicPort -LocalPort $Using:AELocalPort | `
                   Update-AzureVM
               Write-Output $Status
           }
       }
   ```
7. <span data-ttu-id="9daeb-195">Al termine, premere Pubblica ![](media/site-recovery-runbook-automation/20.png) per fare in modo che lo script sia disponibile per l'esecuzione.</span><span class="sxs-lookup"><span data-stu-id="9daeb-195">Once this is complete, hit Publish ![](media/site-recovery-runbook-automation/20.png) to allow your script to be available for execution.</span></span>

<span data-ttu-id="9daeb-196">Di seguito è riportato lo script completo per riferimento</span><span class="sxs-lookup"><span data-stu-id="9daeb-196">The complete script is given below for your reference</span></span>

```
  workflow OpenPort80
  {
    param (
        [Object]$RecoveryPlanContext
    )

    $Cred = Get-AutomationPSCredential -Name 'AzureCredential'

    # Connect to Azure
    $AzureAccount = Add-AzureAccount -Credential $Cred
    $AzureSubscriptionName = Get-AutomationVariable –Name ‘AzureSubscriptionName’
    Select-AzureSubscription -SubscriptionName $AzureSubscriptionName

    # Specify the parameters to be used by the script
    $AEProtocol = "TCP"
    $AELocalPort = 80
    $AEPublicPort = 80
    $AEName = "Port 80 for HTTP"
    $VMGUID = "7a1069c6-c1d6-49c5-8c5d-33bfce8dd183"

    #Read the VM GUID from the context
    $VM = $RecoveryPlanContext.VmMap.$VMGUID

    if ($VM -ne $null)
    {
        # Invoke pipeline commands within an InlineScript

        $EndpointStatus = InlineScript {
            # Invoke the necessary pipeline commands to add an Azure Endpoint to a specified Virtual Machine
            # This set of commands includes: Get-AzureVM | Add-AzureEndpoint | Update-AzureVM (including necessary parameters)

            $Status = Get-AzureVM -ServiceName $Using:VM.CloudServiceName -Name $Using:VM.RoleName | `
                Add-AzureEndpoint -Name $Using:AEName -Protocol $Using:AEProtocol -PublicPort $Using:AEPublicPort -LocalPort $Using:AELocalPort | `
                Update-AzureVM
            Write-Output $Status
        }
    }
  }
```

## <a name="add-the-script-to-the-recovery-plan"></a><span data-ttu-id="9daeb-197">Aggiungere lo script al piano di ripristino</span><span class="sxs-lookup"><span data-stu-id="9daeb-197">Add the script to the recovery plan</span></span>
<span data-ttu-id="9daeb-198">Quando lo script è pronto, è possibile aggiungerlo al piano di ripristino creato in precedenza.</span><span class="sxs-lookup"><span data-stu-id="9daeb-198">Once the script is ready, you can add it to the recovery plan that you created earlier.</span></span>

1. <span data-ttu-id="9daeb-199">Nel piano di ripristino creato, scegliere di aggiungere uno script dopo il gruppo 2.</span><span class="sxs-lookup"><span data-stu-id="9daeb-199">In the recovery plan you created, choose to add a script after the group 2.</span></span> ![](media/site-recovery-runbook-automation/15.png)
2. <span data-ttu-id="9daeb-200">Specificare un nome per lo script.</span><span class="sxs-lookup"><span data-stu-id="9daeb-200">Specify a script name.</span></span> <span data-ttu-id="9daeb-201">Si tratta semplicemente di un nome descrittivo per lo script, per la visualizzazione all'interno del piano di ripristino.</span><span class="sxs-lookup"><span data-stu-id="9daeb-201">This is just a friendly name for this script for showing within the Recovery plan.</span></span>
3. <span data-ttu-id="9daeb-202">Nel failover allo script di Azure, selezionare il nome dell'account di Automazione di Azure.</span><span class="sxs-lookup"><span data-stu-id="9daeb-202">In the failover to Azure script – Select the Azure Automation Account name.</span></span>
4. <span data-ttu-id="9daeb-203">Nei runbook di Azure, selezionare il runbook che è stato creato.</span><span class="sxs-lookup"><span data-stu-id="9daeb-203">In the Azure Runbooks, select the runbook you authored.</span></span>

![](media/site-recovery-runbook-automation/16.png)

## <a name="primary-side-scripts"></a><span data-ttu-id="9daeb-204">Script sul lato primario</span><span class="sxs-lookup"><span data-stu-id="9daeb-204">Primary side scripts</span></span>
<span data-ttu-id="9daeb-205">Quando si esegue un failover in Azure, è possibile scegliere di eseguire gli script sul lato primario.</span><span class="sxs-lookup"><span data-stu-id="9daeb-205">When you are executing a failover to Azure, you can also choose to execute primary side scripts.</span></span> <span data-ttu-id="9daeb-206">Questi script verranno eseguiti nel server VMM durante il failover.</span><span class="sxs-lookup"><span data-stu-id="9daeb-206">These scripts will run on the VMM server during failover.</span></span>
<span data-ttu-id="9daeb-207">Gli script sul lato primario sono disponibili solo nelle fasi precedente e successiva all’arresto.</span><span class="sxs-lookup"><span data-stu-id="9daeb-207">Primary side scripts are only available only for pre-shutdown and post shutdown stages.</span></span> <span data-ttu-id="9daeb-208">Questo perché in genere il sito primario non è disponibile in caso di emergenza.</span><span class="sxs-lookup"><span data-stu-id="9daeb-208">This is because we expect the primary site to be typically unavailable when a disaster strikes.</span></span>
<span data-ttu-id="9daeb-209">Durante un failover non pianificato, solo se si opta per le operazioni del sito primario, si tenterà di eseguire gli script sul lato primario.</span><span class="sxs-lookup"><span data-stu-id="9daeb-209">During an unplanned failover, only if you opt in for primary site operations, it will attempt to run the primary side scripts.</span></span> <span data-ttu-id="9daeb-210">Se non sono raggiungibili o sono in timeout, il failover continuerà a ripristinare le macchine virtuali.</span><span class="sxs-lookup"><span data-stu-id="9daeb-210">If they are not reachable or timeout, the failover will continue to recover the virtual machines.</span></span>
<span data-ttu-id="9daeb-211">Gli script sul lato primario non sono disponibili per i siti VMware/Physical/Hyper-V senza VMM protetti in Azure durante il failover in Azure.</span><span class="sxs-lookup"><span data-stu-id="9daeb-211">Primary side scripts are un-available for VMware/Physical/Hyper-v Sites without VMM protected to Azure - while you failover to Azure.</span></span>
<span data-ttu-id="9daeb-212">Tuttavia, se si esegue il failback da Azure in locale, gli script sul lato primario (runbook) possono essere usati per tutte le destinazioni, ad eccezione di VMware.</span><span class="sxs-lookup"><span data-stu-id="9daeb-212">However, when you failback from Azure to on-premises, primary side scripts (Runbooks) can be used for all targets except VMware.</span></span>

## <a name="test-the-recovery-plan"></a><span data-ttu-id="9daeb-213">Testare il piano di ripristino</span><span class="sxs-lookup"><span data-stu-id="9daeb-213">Test the recovery plan</span></span>
<span data-ttu-id="9daeb-214">Dopo avere aggiunto il runbook al piano è possibile avviare un failover di test e vederlo in azione.</span><span class="sxs-lookup"><span data-stu-id="9daeb-214">Once you have added the runbook to the plan you can initiate a test failover and see it in action.</span></span> <span data-ttu-id="9daeb-215">È sempre consigliabile eseguire un failover di test per testare l'applicazione e il piano di ripristino per assicurarsi che non siano presenti errori.</span><span class="sxs-lookup"><span data-stu-id="9daeb-215">It is always recommended to run a test failover to test your application and the recovery plan to ensure that there are no errors.</span></span>

1. <span data-ttu-id="9daeb-216">Selezionare il piano di ripristino e avviare un failover di test.</span><span class="sxs-lookup"><span data-stu-id="9daeb-216">Select the recovery plan and initiate a test failover.</span></span>
2. <span data-ttu-id="9daeb-217">Durante l'esecuzione del piano, è possibile verificare se il runbook è stato eseguito o meno tramite il relativo stato.</span><span class="sxs-lookup"><span data-stu-id="9daeb-217">During the plan execution, you can see whether the runbook has executed or not via its status.</span></span>

   ![](media/site-recovery-runbook-automation/17.png)
3. <span data-ttu-id="9daeb-218">È inoltre possibile visualizzare lo stato di esecuzione dettagliato del runbook nella pagina dei processi di Automazione di Azure relativa al runbook.</span><span class="sxs-lookup"><span data-stu-id="9daeb-218">You can also see the detailed runbook execution status on the Azure Automation jobs page for the runbook.</span></span>

   ![](media/site-recovery-runbook-automation/18.png)
4. <span data-ttu-id="9daeb-219">Dopo il failover, a parte il risultato dell'esecuzione del runbook, è possibile verificare se l'esecuzione ha avuto esito positivo o meno, visitando la pagina della macchina virtuale di Azure e analizzando gli endpoint.</span><span class="sxs-lookup"><span data-stu-id="9daeb-219">After the failover completes, apart from the runbook execution result, you can see whether the execution is successful or not by visiting the Azure virtual machine page and looking at the endpoints.</span></span>

![](media/site-recovery-runbook-automation/19.png)

## <a name="sample-scripts"></a><span data-ttu-id="9daeb-220">Script di esempio</span><span class="sxs-lookup"><span data-stu-id="9daeb-220">Sample scripts</span></span>
<span data-ttu-id="9daeb-221">Anche se in questa esercitazione è stata illustrata l'automazione di un’attività comunemente utilizzata di aggiunta di un endpoint a una macchina virtuale di Azure, tramite Automazione di Azure è possibile eseguire una serie di altre attività di automazione efficaci.</span><span class="sxs-lookup"><span data-stu-id="9daeb-221">While we walked through automating one commonly used task of adding an endpoint to an Azure virtual machine in this tutorial, you could do a number of other powerful automation tasks using Azure automation.</span></span> <span data-ttu-id="9daeb-222">Microsoft e la community di Automazione di Azure mettono a disposizione runbook di esempio, utili per iniziare a creare soluzioni personalizzate, nonché runbook di utilità, utili come componenti di base per attività di automazione più estese.</span><span class="sxs-lookup"><span data-stu-id="9daeb-222">Microsoft and the Azure Automation community provide sample runbooks which can help you get started creating your own solutions, and utility runbooks, which you can use as building blocks for larger automation tasks.</span></span> <span data-ttu-id="9daeb-223">Iniziare a usare i runbook dalla raccolta e generare piani di ripristino efficaci ad un solo clic per le applicazioni che usano Azure Site Recovery.</span><span class="sxs-lookup"><span data-stu-id="9daeb-223">Start using them from the gallery and build  powerful one-click recovery plans for your applications using Azure Site Recovery.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="9daeb-224">Risorse aggiuntive</span><span class="sxs-lookup"><span data-stu-id="9daeb-224">Additional Resources</span></span>
[<span data-ttu-id="9daeb-225">Panoramica di Automazione di Azure</span><span class="sxs-lookup"><span data-stu-id="9daeb-225">Azure Automation Overview</span></span>](http://msdn.microsoft.com/library/azure/dn643629.aspx "Panoramica di Automazione di Azure")

[<span data-ttu-id="9daeb-226">Script di esempio di Automazione di Azure</span><span class="sxs-lookup"><span data-stu-id="9daeb-226">Sample Azure Automation Scripts</span></span>](http://gallery.technet.microsoft.com/scriptcenter/site/search?f\[0\].Type=User&f\[0\].Value=SC%20Automation%20Product%20Team&f\[0\].Text=SC%20Automation%20Product%20Team "Script di esempio di Automazione di Azure")

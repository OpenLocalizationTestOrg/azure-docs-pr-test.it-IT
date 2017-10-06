---
title: aaaAdd piani toorecovery runbook di automazione di Azure nel portale classico hello | Documenti Microsoft
description: "Questo articolo viene descritto come Azure Site Recovery consente ora i piani di ripristino tooextend con complesse attività di automazione di Azure toocomplete durante il ripristino tooAzure"
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
ms.openlocfilehash: 3bb7420911afbce289b656f28823b1923e8af0c5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="add-azure-automation-runbooks-toorecovery-plans-in-hello-classic-portal"></a><span data-ttu-id="5900d-103">Aggiungere i piani toorecovery runbook di automazione di Azure nel portale classico hello</span><span class="sxs-lookup"><span data-stu-id="5900d-103">Add Azure automation runbooks toorecovery plans in hello classic portal</span></span>
<span data-ttu-id="5900d-104">In questa esercitazione viene descritta l'integrazione di Azure Site Recovery con automazione di Azure tooprovide estendibilità toorecovery piani.</span><span class="sxs-lookup"><span data-stu-id="5900d-104">This tutorial describes how Azure Site Recovery integrates with Azure Automation tooprovide extensibility toorecovery plans.</span></span> <span data-ttu-id="5900d-105">I piani di ripristino possono orchestrare il ripristino delle macchine virtuali protette mediante Azure Site Recovery per cloud di replica toosecondary e scenari di replica tooAzure.</span><span class="sxs-lookup"><span data-stu-id="5900d-105">Recovery plans can orchestrate recovery of your virtual machines protected using Azure Site Recovery for both replication toosecondary cloud and replication tooAzure scenarios.</span></span> <span data-ttu-id="5900d-106">Consentono inoltre di effettuare il ripristino di hello **in modo coerente accurate**, **repeatable**, e **automatizzati**.</span><span class="sxs-lookup"><span data-stu-id="5900d-106">They also help in making hello recovery **consistently accurate**, **repeatable**, and **automated**.</span></span> <span data-ttu-id="5900d-107">Se viene eseguito il failover tooAzure le macchine virtuali, integrazione con automazione di Azure estende i piani di ripristino e offre funzionalità tooexecute runbook, consentendo in tal modo l'attività di automazione potente.</span><span class="sxs-lookup"><span data-stu-id="5900d-107">If you are failing over your virtual machines tooAzure, integration with Azure Automation extends the recovery plans and gives you capability tooexecute runbooks, thus allowing powerful automation tasks.</span></span>

<span data-ttu-id="5900d-108">Se non si è ancora sentito parlare di Automazione di Azure, effettuare l'iscrizione [qui](https://azure.microsoft.com/services/automation/) e scaricare gli script di esempio [qui](https://azure.microsoft.com/documentation/scripts/).</span><span class="sxs-lookup"><span data-stu-id="5900d-108">If you have not heard about Azure Automation yet, sign up [here](https://azure.microsoft.com/services/automation/) and download their sample scripts [here](https://azure.microsoft.com/documentation/scripts/).</span></span> <span data-ttu-id="5900d-109">Altre informazioni sui [Azure Site Recovery](https://azure.microsoft.com/services/site-recovery/) e come tooorchestrate tooAzure di ripristino con ripristino prevede [qui](https://azure.microsoft.com/blog/?p=166264).</span><span class="sxs-lookup"><span data-stu-id="5900d-109">Read more about [Azure Site Recovery](https://azure.microsoft.com/services/site-recovery/) and how tooorchestrate recovery tooAzure using recovery plans [here](https://azure.microsoft.com/blog/?p=166264).</span></span>

<span data-ttu-id="5900d-110">In questa breve esercitazione verrà illustrato come integrare i runbook di Automazione di Azure nei piani di ripristino.</span><span class="sxs-lookup"><span data-stu-id="5900d-110">In this short tutorial, we will look at how you can integrate Azure Automation runbooks into recovery plans.</span></span> <span data-ttu-id="5900d-111">Ti consentono di automatizzare attività semplice precedenti richieste interventi manuali e vedere come tooconvert un multi passaggio ripristino in un'azione di ripristino con clic singolo.</span><span class="sxs-lookup"><span data-stu-id="5900d-111">We will automate simple tasks that earlier required manual intervention and see how tooconvert a multi step recovery into a single-click recovery action.</span></span> <span data-ttu-id="5900d-112">Verrà esaminato inoltre come risolvere eventuali problemi di un semplice script.</span><span class="sxs-lookup"><span data-stu-id="5900d-112">We will also look at how you can troubleshoot a simple script if it goes wrong.</span></span>

## <a name="protect-hello-application-tooazure"></a><span data-ttu-id="5900d-113">Proteggere tooAzure applicazione hello</span><span class="sxs-lookup"><span data-stu-id="5900d-113">Protect hello application tooAzure</span></span>
<span data-ttu-id="5900d-114">Si inizierà con una semplice applicazione costituita da due macchine virtuali.</span><span class="sxs-lookup"><span data-stu-id="5900d-114">Let us begin with a simple application consisting of two virtual machines.</span></span> <span data-ttu-id="5900d-115">In questo caso, viene usata un'applicazione HRweb di Fabrikam.</span><span class="sxs-lookup"><span data-stu-id="5900d-115">Here, we have a HRweb application of Fabrikam.</span></span> <span data-ttu-id="5900d-116">Fabrikam-HRweb-front-end e back-end Fabrikam Hrweb sono hello due macchine virtuali protette tooAzure usando Azure Site Recovery.</span><span class="sxs-lookup"><span data-stu-id="5900d-116">Fabrikam-HRweb-frontend and Fabrikam-Hrweb-backend are hello two virtual machines protected tooAzure using Azure Site Recovery.</span></span> <span data-ttu-id="5900d-117">macchine virtuali di hello tooprotect usando Azure Site Recovery, procedura hello riportata di seguito.</span><span class="sxs-lookup"><span data-stu-id="5900d-117">tooprotect hello virtual machines using Azure Site Recovery, follow hello steps below.</span></span>

1. <span data-ttu-id="5900d-118">Abilitare la protezione per le macchine virtuali.</span><span class="sxs-lookup"><span data-stu-id="5900d-118">Enable protection for your virtual machines.</span></span>
2. <span data-ttu-id="5900d-119">Verificare che le macchine virtuali hello aver completato la replica iniziale e sta eseguendo la replica.</span><span class="sxs-lookup"><span data-stu-id="5900d-119">Ensure that hello virtual machines have completed initial replication and are replicating.</span></span>
3. <span data-ttu-id="5900d-120">Consente di attendere il completamento della replica iniziale hello e hello lo stato della replica afferma protetti.</span><span class="sxs-lookup"><span data-stu-id="5900d-120">Wait till hello initial replication completes and hello Replication status says Protected.</span></span>

## ![](media/site-recovery-runbook-automation/01.png)
<span data-ttu-id="5900d-121">In questa esercitazione si creerà un piano di ripristino per Fabrikam HRweb applicazione toofailover hello applicazione tooAzure hello.</span><span class="sxs-lookup"><span data-stu-id="5900d-121">In this tutorial, we will create a recovery plan for hello Fabrikam HRweb application toofailover hello application tooAzure.</span></span> <span data-ttu-id="5900d-122">È quindi verrà integrarlo con un runbook che verrà creato un endpoint nel hello failover pagine web tooserve di macchina virtuale di Azure alla porta 80.</span><span class="sxs-lookup"><span data-stu-id="5900d-122">Then we will integrate it with a runbook that will create an endpoint on hello failed over Azure virtual machine tooserve web pages at port 80.</span></span>

<span data-ttu-id="5900d-123">Innanzitutto, verrà creato un piano di ripristino per l’applicazione.</span><span class="sxs-lookup"><span data-stu-id="5900d-123">First, let's create a recovery plan for our application.</span></span>

## <a name="create-hello-recovery-plan"></a><span data-ttu-id="5900d-124">Creare il piano di ripristino hello</span><span class="sxs-lookup"><span data-stu-id="5900d-124">Create hello recovery plan</span></span>
<span data-ttu-id="5900d-125">toorecover hello applicazione tooAzure, è necessario toocreate un piano di ripristino.</span><span class="sxs-lookup"><span data-stu-id="5900d-125">toorecover hello application tooAzure, you need toocreate a recovery plan.</span></span>
<span data-ttu-id="5900d-126">Utilizzo di un piano di ripristino che è possibile specificare l'ordine di hello del ripristino delle macchine virtuali.</span><span class="sxs-lookup"><span data-stu-id="5900d-126">Using a recovery plan you can specify hello order of recovery of the virtual machines.</span></span> <span data-ttu-id="5900d-127">verranno avviati prima e ripristina macchina virtuale Hello inserito nel gruppo 1, e seguire hello di macchina virtuale nel gruppo 2.</span><span class="sxs-lookup"><span data-stu-id="5900d-127">hello virtual machine placed in group 1 will recover and start first, and then hello virtual machine in group 2 will follow.</span></span>

<span data-ttu-id="5900d-128">Creare un piano di ripristino simile al seguente.</span><span class="sxs-lookup"><span data-stu-id="5900d-128">Create a Recovery Plan that looks like below.</span></span>

![](media/site-recovery-runbook-automation/12.png)

<span data-ttu-id="5900d-129">ulteriori informazioni sui piani di ripristino, leggere la documentazione tooread [qui](https://msdn.microsoft.com/library/azure/dn788799.aspx "qui").</span><span class="sxs-lookup"><span data-stu-id="5900d-129">tooread more about recovery plans, read documentation [here](https://msdn.microsoft.com/library/azure/dn788799.aspx "here").</span></span>

<span data-ttu-id="5900d-130">Successivamente, creare hello gli elementi necessari in automazione di Azure.</span><span class="sxs-lookup"><span data-stu-id="5900d-130">Next, let's create hello necessary artifacts in Azure Automation.</span></span>

## <a name="create-hello-automation-account-and-its-assets"></a><span data-ttu-id="5900d-131">Creare account di automazione hello e gli asset</span><span class="sxs-lookup"><span data-stu-id="5900d-131">Create hello automation account and its assets</span></span>
<span data-ttu-id="5900d-132">È necessario un runbook toocreate account di automazione di Azure.</span><span class="sxs-lookup"><span data-stu-id="5900d-132">You need an Azure Automation account toocreate runbooks.</span></span> <span data-ttu-id="5900d-133">Se si dispone già di un account, passare indicata dalla scheda di automazione tooAzure ![](media/site-recovery-runbook-automation/02.png)e creare un nuovo account.</span><span class="sxs-lookup"><span data-stu-id="5900d-133">If you do not already have an account, navigate tooAzure Automation tab denoted by ![](media/site-recovery-runbook-automation/02.png)and create a new account.</span></span>

1. <span data-ttu-id="5900d-134">Assegnare all'account hello tooidentify un nome con.</span><span class="sxs-lookup"><span data-stu-id="5900d-134">Give hello account a name tooidentify with.</span></span>
2. <span data-ttu-id="5900d-135">Specificare un'area geografica in cui si desidera account hello tooplace.</span><span class="sxs-lookup"><span data-stu-id="5900d-135">Specify a geographical region where you want tooplace hello account.</span></span>

<span data-ttu-id="5900d-136">È consigliabile tooplace account hello hello stessa area dell'insieme di credenziali di hello ripristino automatico di sistema.</span><span class="sxs-lookup"><span data-stu-id="5900d-136">It is recommended tooplace hello account in hello same region as hello ASR vault.</span></span>

![](media/site-recovery-runbook-automation/03.png)

<span data-ttu-id="5900d-137">Successivamente, creare hello asset in hello Account seguenti.</span><span class="sxs-lookup"><span data-stu-id="5900d-137">Next, create hello following assets in hello Account.</span></span>

### <a name="add-a-subscription-name-as-asset"></a><span data-ttu-id="5900d-138">Aggiungere un nome di sottoscrizione come asset</span><span class="sxs-lookup"><span data-stu-id="5900d-138">Add a subscription name as asset</span></span>
1. <span data-ttu-id="5900d-139">Aggiungere una nuova impostazione ![](media/site-recovery-runbook-automation/04.png) in hello asset di automazione di Azure e selezionare troppo![](media/site-recovery-runbook-automation/05.png)</span><span class="sxs-lookup"><span data-stu-id="5900d-139">Add a new setting ![](media/site-recovery-runbook-automation/04.png) in hello Azure Automation Assets and select too![](media/site-recovery-runbook-automation/05.png)</span></span>
2. <span data-ttu-id="5900d-140">Selezionare tipo di variabile come hello **stringa**</span><span class="sxs-lookup"><span data-stu-id="5900d-140">Select hello variable type as **String**</span></span>
3. <span data-ttu-id="5900d-141">Specificare **AzureSubscriptionName**</span><span class="sxs-lookup"><span data-stu-id="5900d-141">Specify variable name as **AzureSubscriptionName**</span></span>

   ![](media/site-recovery-runbook-automation/06.png)
4. <span data-ttu-id="5900d-142">Specificare il nome della sottoscrizione di Azure effettivo come valore della variabile hello.</span><span class="sxs-lookup"><span data-stu-id="5900d-142">Specify your actual Azure Subscription name as hello variable value.</span></span>

   ![](media/site-recovery-runbook-automation/07_1.png)

<span data-ttu-id="5900d-143">È possibile identificare il nome di hello della sottoscrizione dalla pagina Impostazioni hello dell'account nel portale di Azure hello.</span><span class="sxs-lookup"><span data-stu-id="5900d-143">You can identify hello name of your subscription from hello settings page of your account on hello Azure portal.</span></span>

### <a name="add-an-azure-login-credential-as-asset"></a><span data-ttu-id="5900d-144">Aggiungere una credenziale di accesso di Azure come asset</span><span class="sxs-lookup"><span data-stu-id="5900d-144">Add an Azure login credential as asset</span></span>
<span data-ttu-id="5900d-145">Automazione di Azure Usa una sottoscrizione di Azure PowerShell tooconnect toothe e opera sugli elementi hello non esiste.</span><span class="sxs-lookup"><span data-stu-id="5900d-145">Azure Automation uses Azure PowerShell tooconnect toothe subscription and operates on hello artifacts there.</span></span> <span data-ttu-id="5900d-146">A tale scopo, è necessario eseguire l'autenticazione usando l'account Microsoft o un account aziendale o dell’istituto di istruzione.</span><span class="sxs-lookup"><span data-stu-id="5900d-146">For this, you need to authenticate using your Microsoft account or a work or school account.</span></span>
<span data-ttu-id="5900d-147">È possibile archiviare le credenziali dell'account hello in toobe un asset in modo sicuro utilizzato dal runbook hello.</span><span class="sxs-lookup"><span data-stu-id="5900d-147">You can store hello account credentials in an asset toobe used securely by hello runbook.</span></span>

1. <span data-ttu-id="5900d-148">Aggiungere una nuova impostazione ![](media/site-recovery-runbook-automation/04.png) in hello asset di automazione di Azure e selezionare![](media/site-recovery-runbook-automation/09.png)</span><span class="sxs-lookup"><span data-stu-id="5900d-148">Add a new setting ![](media/site-recovery-runbook-automation/04.png) in hello Azure Automation Assets and select ![](media/site-recovery-runbook-automation/09.png)</span></span>
2. <span data-ttu-id="5900d-149">Selezionare il tipo di credenziale hello come **credenziali di Windows PowerShell**</span><span class="sxs-lookup"><span data-stu-id="5900d-149">Select hello Credential type as **Windows PowerShell Credential**</span></span>
3. <span data-ttu-id="5900d-150">Specificare il nome di hello come **AzureCredential**</span><span class="sxs-lookup"><span data-stu-id="5900d-150">Specify hello name as **AzureCredential**</span></span>

   ![](media/site-recovery-runbook-automation/10.png)
4. <span data-ttu-id="5900d-151">Specificare nome utente hello e una password toosign-con.</span><span class="sxs-lookup"><span data-stu-id="5900d-151">Specify hello username and password toosign-in with.</span></span>

<span data-ttu-id="5900d-152">Entrambe queste impostazioni sono ora disponibili negli asset.</span><span class="sxs-lookup"><span data-stu-id="5900d-152">Now both these settings are available in your assets.</span></span>

![](media/site-recovery-runbook-automation/11.png)

<span data-ttu-id="5900d-153">Ulteriori informazioni sulla modalità in cui viene assegnato tooconnect tooyour sottoscrizione tramite PowerShell [qui](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="5900d-153">More information about how tooconnect tooyour subscription via PowerShell is given [here](/powershell/azure/overview).</span></span>

<span data-ttu-id="5900d-154">Successivamente, si creerà un runbook in automazione di Azure che è possibile aggiungere un endpoint per la macchina virtuale front-end hello dopo il failover.</span><span class="sxs-lookup"><span data-stu-id="5900d-154">Next, you will create a runbook in Azure Automation that can add an endpoint for hello front-end virtual machine after failover.</span></span>

## <a name="azure-automation-context"></a><span data-ttu-id="5900d-155">Contesto di Automazione di Azure</span><span class="sxs-lookup"><span data-stu-id="5900d-155">Azure automation context</span></span>
<span data-ttu-id="5900d-156">Ripristino automatico di sistema passa un toohelp runbook toohello variabile di contesto è scrivere script deterministico.</span><span class="sxs-lookup"><span data-stu-id="5900d-156">ASR passes a context variable toohello runbook toohelp you write deterministic scripts.</span></span> <span data-ttu-id="5900d-157">È possibile sostenere che i nomi di hello di hello servizio Cloud e hello macchina virtuale sono prevedibili, ma si verifica che non è sempre case hello dovuti toocertain scenari, ad esempio hello uno in cui il nome di hello del nome della macchina virtuale hello potrebbe essere stato modificato a causa caratteri toounsupported in Azure.</span><span class="sxs-lookup"><span data-stu-id="5900d-157">One could argue that hello names of hello Cloud Service and hello Virtual Machine are predictable, but happens that it is not always hello case owing toocertain scenarios such as hello one where hello name of hello virtual machine name might have changed due toounsupported characters in Azure.</span></span> <span data-ttu-id="5900d-158">Di conseguenza queste informazioni vengono passate piano di ripristino toohello ripristino automatico di sistema come parte di hello *contesto*.</span><span class="sxs-lookup"><span data-stu-id="5900d-158">Hence this information is passed toohello ASR recovery plan as part of hello *context*.</span></span>

<span data-ttu-id="5900d-159">Di seguito è riportato un esempio dell'aspetto di variabile di contesto hello.</span><span class="sxs-lookup"><span data-stu-id="5900d-159">Below is an example of how hello context variable looks.</span></span>

        {"RecoveryPlanName":"hrweb-recovery",

        "FailoverType":"Test",

        "FailoverDirection":"PrimaryToSecondary",

        "GroupId":"1",

        "VmMap":{"7a1069c6-c1d6-49c5-8c5d-33bfce8dd183":

                {"CloudServiceName":"pod02hrweb-Chicago-test",

                "RoleName":"Fabrikam-Hrweb-frontend-test"}

                }

        }


<span data-ttu-id="5900d-160">tabella Hello riportata di seguito contiene nome e una descrizione per ogni variabile nel contesto di hello.</span><span class="sxs-lookup"><span data-stu-id="5900d-160">hello table below contains name and description for each variable in hello context.</span></span>

| <span data-ttu-id="5900d-161">**Nome variabile**</span><span class="sxs-lookup"><span data-stu-id="5900d-161">**Variable name**</span></span> | <span data-ttu-id="5900d-162">**Descrizione**</span><span class="sxs-lookup"><span data-stu-id="5900d-162">**Description**</span></span> |
| --- | --- |
| <span data-ttu-id="5900d-163">RecoveryPlanName</span><span class="sxs-lookup"><span data-stu-id="5900d-163">RecoveryPlanName</span></span> |<span data-ttu-id="5900d-164">Nome del piano di esecuzione.</span><span class="sxs-lookup"><span data-stu-id="5900d-164">Name of plan being run.</span></span> <span data-ttu-id="5900d-165">Consente di sfruttare l'azione in base a nome utilizzando hello stesso script</span><span class="sxs-lookup"><span data-stu-id="5900d-165">Helps you take action based on name using hello same script</span></span> |
| <span data-ttu-id="5900d-166">FailoverType</span><span class="sxs-lookup"><span data-stu-id="5900d-166">FailoverType</span></span> |<span data-ttu-id="5900d-167">Specifica se hello failover è il test, pianificato o non pianificato.</span><span class="sxs-lookup"><span data-stu-id="5900d-167">Specifies whether hello failover is test, planned, or unplanned.</span></span> |
| <span data-ttu-id="5900d-168">FailoverDirection</span><span class="sxs-lookup"><span data-stu-id="5900d-168">FailoverDirection</span></span> |<span data-ttu-id="5900d-169">Specificare se il ripristino è tooprimary o secondario</span><span class="sxs-lookup"><span data-stu-id="5900d-169">Specify whether recovery is tooprimary or secondary</span></span> |
| <span data-ttu-id="5900d-170">GroupID</span><span class="sxs-lookup"><span data-stu-id="5900d-170">GroupID</span></span> |<span data-ttu-id="5900d-171">Identificare il numero di gruppo hello nel piano di ripristino hello quando piano hello è in esecuzione</span><span class="sxs-lookup"><span data-stu-id="5900d-171">Identify hello group number within hello recovery plan when hello plan is running</span></span> |
| <span data-ttu-id="5900d-172">VmMap</span><span class="sxs-lookup"><span data-stu-id="5900d-172">VmMap</span></span> |<span data-ttu-id="5900d-173">Matrice di tutte le macchine virtuali hello gruppo hello</span><span class="sxs-lookup"><span data-stu-id="5900d-173">Array of all hello virtual machines in hello group</span></span> |
| <span data-ttu-id="5900d-174">VMMap key</span><span class="sxs-lookup"><span data-stu-id="5900d-174">VMMap key</span></span> |<span data-ttu-id="5900d-175">Chiave univoca (GUID) per ciascuna VM.</span><span class="sxs-lookup"><span data-stu-id="5900d-175">Unique key (GUID) for each VM.</span></span> <span data-ttu-id="5900d-176">È hello uguali a quelli hello VMM ID della macchina virtuale hello dove applicabile.</span><span class="sxs-lookup"><span data-stu-id="5900d-176">It's hello same as hello VMM ID of hello virtual machine where applicable.</span></span> |
| <span data-ttu-id="5900d-177">RoleName</span><span class="sxs-lookup"><span data-stu-id="5900d-177">RoleName</span></span> |<span data-ttu-id="5900d-178">Nome della macchina virtuale di Azure che viene ripristinato hello</span><span class="sxs-lookup"><span data-stu-id="5900d-178">Name of hello Azure VM that's being recovered</span></span> |
| <span data-ttu-id="5900d-179">CloudServiceName</span><span class="sxs-lookup"><span data-stu-id="5900d-179">CloudServiceName</span></span> |<span data-ttu-id="5900d-180">Nome del servizio Cloud Azure in cui hello viene creata la macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="5900d-180">Azure Cloud Service name under which hello virtual machine is created.</span></span> |

<span data-ttu-id="5900d-181">hello tooidentify VmMap Key nel contesto di hello è possibile anche passare toohello pagina delle proprietà macchina virtuale in ASR e osservare hello proprietà GUID di VM.</span><span class="sxs-lookup"><span data-stu-id="5900d-181">tooidentify hello VmMap Key in hello context you could also go toohello VM properties page in ASR and look at hello VM GUID property.</span></span>

![](media/site-recovery-runbook-automation/13.png)

## <a name="author-an-automation-runbook"></a><span data-ttu-id="5900d-182">Creare un runbook di Automazione</span><span class="sxs-lookup"><span data-stu-id="5900d-182">Author an Automation runbook</span></span>
<span data-ttu-id="5900d-183">A questo punto creare hello runbook tooopen porta 80 nella macchina virtuale front-end hello.</span><span class="sxs-lookup"><span data-stu-id="5900d-183">Now create hello runbook tooopen port 80 on hello front-end virtual machine.</span></span>

1. <span data-ttu-id="5900d-184">Creare un nuovo runbook nell'account di automazione di Azure con nome hello hello **OpenPort80**</span><span class="sxs-lookup"><span data-stu-id="5900d-184">Create a new runbook in hello Azure Automation account with hello name **OpenPort80**</span></span>

   ![](media/site-recovery-runbook-automation/14.png)
2. <span data-ttu-id="5900d-185">Passare toohello Visualizza di autore del runbook hello e passare alla modalità di bozza hello.</span><span class="sxs-lookup"><span data-stu-id="5900d-185">Navigate toohello Author view of hello runbook and enter hello draft mode.</span></span>
3. <span data-ttu-id="5900d-186">Specificare innanzitutto toouse variabile hello come contesto di piano di ripristino hello</span><span class="sxs-lookup"><span data-stu-id="5900d-186">First specify hello variable toouse as hello recovery plan context</span></span>

   ```
       param (
           [Object]$RecoveryPlanContext
       )

   ```
4. <span data-ttu-id="5900d-187">Riconnette toohello sottoscrizione utilizzando un nome delle credenziali e sottoscrizione hello</span><span class="sxs-lookup"><span data-stu-id="5900d-187">Next connect toohello subscription using hello credential and subscription name</span></span>

   ```
       $Cred = Get-AutomationPSCredential -Name 'AzureCredential'

       # Connect tooAzure
       $AzureAccount = Add-AzureAccount -Credential $Cred
       $AzureSubscriptionName = Get-AutomationVariable –Name ‘AzureSubscriptionName’
       Select-AzureSubscription -SubscriptionName $AzureSubscriptionName
   ```

   <span data-ttu-id="5900d-188">Si noti che è utilizzare hello Azure principali: **AzureCredential** e **AzureSubscriptionName** qui.</span><span class="sxs-lookup"><span data-stu-id="5900d-188">Note that you use hello Azure assets – **AzureCredential** and **AzureSubscriptionName** here.</span></span>
5. <span data-ttu-id="5900d-189">GUID della macchina virtuale hello per cui si desidera endpoint hello tooexpose hello ora specificare i dettagli degli endpoint hello.</span><span class="sxs-lookup"><span data-stu-id="5900d-189">Now specify hello endpoint details and hello GUID of hello virtual machine for which you want tooexpose hello endpoint.</span></span> <span data-ttu-id="5900d-190">In questa macchina virtuale front-end hello case.</span><span class="sxs-lookup"><span data-stu-id="5900d-190">In this case hello front-end virtual machine.</span></span>

   ```
       # Specify hello parameters toobe used by hello script
       $AEProtocol = "TCP"
       $AELocalPort = 80
       $AEPublicPort = 80
       $AEName = "Port 80 for HTTP"
       $VMGUID = "7a1069c6-c1d6-49c5-8c5d-33bfce8dd183"
   ```

   <span data-ttu-id="5900d-191">Questo valore specifica hello protocollo dell'endpoint di Azure, porta locale hello macchina virtuale e la relativa porta pubblica mappata.</span><span class="sxs-lookup"><span data-stu-id="5900d-191">This specifies hello Azure endpoint protocol, local port on hello VM and its mapped public port.</span></span> <span data-ttu-id="5900d-192">Queste variabili sono i parametri necessari per hello Azure comandi che aggiungono tooVMs endpoint.</span><span class="sxs-lookup"><span data-stu-id="5900d-192">These variables are parameters     required by hello Azure commands that add endpoints tooVMs.</span></span> <span data-ttu-id="5900d-193">Hello VMGUID contiene hello GUID della macchina virtuale hello in che è necessario toooperate.</span><span class="sxs-lookup"><span data-stu-id="5900d-193">hello VMGUID holds hello GUID of hello virtual machine you need toooperate on.</span></span>
6. <span data-ttu-id="5900d-194">script Hello ora estrarre contesto hello per hello dato GUID di VM e creare un endpoint nella macchina virtuale hello contiene i riferimenti.</span><span class="sxs-lookup"><span data-stu-id="5900d-194">hello script will now extract hello context for hello given VM GUID and create an endpoint on hello virtual machine referenced by it.</span></span>

   ```
       #Read hello VM GUID from hello context
       $VM = $RecoveryPlanContext.VmMap.$VMGUID

       if ($VM -ne $null)
       {
           # Invoke pipeline commands within an InlineScript

           $EndpointStatus = InlineScript {
               # Invoke hello necessary pipeline commands tooadd a Azure Endpoint tooa specified Virtual Machine
               # Commands include: Get-AzureVM | Add-AzureEndpoint | Update-AzureVM (including parameters)

               $Status = Get-AzureVM -ServiceName $Using:VM.CloudServiceName -Name $Using:VM.RoleName | `
                   Add-AzureEndpoint -Name $Using:AEName -Protocol $Using:AEProtocol -PublicPort $Using:AEPublicPort -LocalPort $Using:AELocalPort | `
                   Update-AzureVM
               Write-Output $Status
           }
       }
   ```
7. <span data-ttu-id="5900d-195">Al termine, premere pubblica ![](media/site-recovery-runbook-automation/20.png) tooallow il toobe script disponibili per l'esecuzione.</span><span class="sxs-lookup"><span data-stu-id="5900d-195">Once this is complete, hit Publish ![](media/site-recovery-runbook-automation/20.png) tooallow your script toobe available for execution.</span></span>

<span data-ttu-id="5900d-196">script completo di Hello è indicato di seguito per riferimento</span><span class="sxs-lookup"><span data-stu-id="5900d-196">hello complete script is given below for your reference</span></span>

```
  workflow OpenPort80
  {
    param (
        [Object]$RecoveryPlanContext
    )

    $Cred = Get-AutomationPSCredential -Name 'AzureCredential'

    # Connect tooAzure
    $AzureAccount = Add-AzureAccount -Credential $Cred
    $AzureSubscriptionName = Get-AutomationVariable –Name ‘AzureSubscriptionName’
    Select-AzureSubscription -SubscriptionName $AzureSubscriptionName

    # Specify hello parameters toobe used by hello script
    $AEProtocol = "TCP"
    $AELocalPort = 80
    $AEPublicPort = 80
    $AEName = "Port 80 for HTTP"
    $VMGUID = "7a1069c6-c1d6-49c5-8c5d-33bfce8dd183"

    #Read hello VM GUID from hello context
    $VM = $RecoveryPlanContext.VmMap.$VMGUID

    if ($VM -ne $null)
    {
        # Invoke pipeline commands within an InlineScript

        $EndpointStatus = InlineScript {
            # Invoke hello necessary pipeline commands tooadd an Azure Endpoint tooa specified Virtual Machine
            # This set of commands includes: Get-AzureVM | Add-AzureEndpoint | Update-AzureVM (including necessary parameters)

            $Status = Get-AzureVM -ServiceName $Using:VM.CloudServiceName -Name $Using:VM.RoleName | `
                Add-AzureEndpoint -Name $Using:AEName -Protocol $Using:AEProtocol -PublicPort $Using:AEPublicPort -LocalPort $Using:AELocalPort | `
                Update-AzureVM
            Write-Output $Status
        }
    }
  }
```

## <a name="add-hello-script-toohello-recovery-plan"></a><span data-ttu-id="5900d-197">Aggiungi piano di ripristino toohello script hello</span><span class="sxs-lookup"><span data-stu-id="5900d-197">Add hello script toohello recovery plan</span></span>
<span data-ttu-id="5900d-198">Una volta script hello è pronto, è possibile aggiungere toohello piano di ripristino creato in precedenza.</span><span class="sxs-lookup"><span data-stu-id="5900d-198">Once hello script is ready, you can add it toohello recovery plan that you created earlier.</span></span>

1. <span data-ttu-id="5900d-199">Nel piano di ripristino hello che è stato creato, scegliere tooadd uno script dopo il gruppo 2.</span><span class="sxs-lookup"><span data-stu-id="5900d-199">In hello recovery plan you created, choose tooadd a script after the group 2.</span></span> ![](media/site-recovery-runbook-automation/15.png)
2. <span data-ttu-id="5900d-200">Specificare un nome per lo script.</span><span class="sxs-lookup"><span data-stu-id="5900d-200">Specify a script name.</span></span> <span data-ttu-id="5900d-201">Questo è solo un nome descrittivo per questo script per la visualizzazione nel piano di ripristino hello.</span><span class="sxs-lookup"><span data-stu-id="5900d-201">This is just a friendly name for this script for showing within hello Recovery plan.</span></span>
3. <span data-ttu-id="5900d-202">Nello script di tooAzure failover hello: selezionare il nome dell'Account di automazione di Azure hello.</span><span class="sxs-lookup"><span data-stu-id="5900d-202">In hello failover tooAzure script – Select hello Azure Automation Account name.</span></span>
4. <span data-ttu-id="5900d-203">Hello runbook di Azure, selezionare runbook hello che è stato creato.</span><span class="sxs-lookup"><span data-stu-id="5900d-203">In hello Azure Runbooks, select hello runbook you authored.</span></span>

![](media/site-recovery-runbook-automation/16.png)

## <a name="primary-side-scripts"></a><span data-ttu-id="5900d-204">Script sul lato primario</span><span class="sxs-lookup"><span data-stu-id="5900d-204">Primary side scripts</span></span>
<span data-ttu-id="5900d-205">Quando si eseguono tooAzure un failover, è anche possibile scegliere tooexecute script lato primario.</span><span class="sxs-lookup"><span data-stu-id="5900d-205">When you are executing a failover tooAzure, you can also choose tooexecute primary side scripts.</span></span> <span data-ttu-id="5900d-206">Questi script vengono eseguiti nel server VMM hello durante il failover.</span><span class="sxs-lookup"><span data-stu-id="5900d-206">These scripts will run on hello VMM server during failover.</span></span>
<span data-ttu-id="5900d-207">Gli script sul lato primario sono disponibili solo nelle fasi precedente e successiva all’arresto.</span><span class="sxs-lookup"><span data-stu-id="5900d-207">Primary side scripts are only available only for pre-shutdown and post shutdown stages.</span></span> <span data-ttu-id="5900d-208">Questo avviene perché è probabile che hello toobe di sito primario non è in genere quando un'eventuale emergenza.</span><span class="sxs-lookup"><span data-stu-id="5900d-208">This is because we expect hello primary site toobe typically unavailable when a disaster strikes.</span></span>
<span data-ttu-id="5900d-209">Durante un failover non pianificato, solo se si sceglie di partecipare per operazioni del sito primario, verrà eseguito un tentativo script lato primario di hello toorun.</span><span class="sxs-lookup"><span data-stu-id="5900d-209">During an unplanned failover, only if you opt in for primary site operations, it will attempt toorun hello primary side scripts.</span></span> <span data-ttu-id="5900d-210">Se non sono raggiungibili o timeout, il failover di hello continuerà toorecover hello macchine virtuali.</span><span class="sxs-lookup"><span data-stu-id="5900d-210">If they are not reachable or timeout, hello failover will continue toorecover hello virtual machines.</span></span>
<span data-ttu-id="5900d-211">Script lato primario sono non disponibili per i siti di VMware/fisici, Hyper-v senza tooAzure VMM protetto - durante il failover tooAzure.</span><span class="sxs-lookup"><span data-stu-id="5900d-211">Primary side scripts are un-available for VMware/Physical/Hyper-v Sites without VMM protected tooAzure - while you failover tooAzure.</span></span>
<span data-ttu-id="5900d-212">Tuttavia, quando il failback da Azure tooon sedi locali, gli script lato primario (runbook) è possibile utilizzare per tutte le destinazioni, ad eccezione di VMware.</span><span class="sxs-lookup"><span data-stu-id="5900d-212">However, when you failback from Azure tooon-premises, primary side scripts (Runbooks) can be used for all targets except VMware.</span></span>

## <a name="test-hello-recovery-plan"></a><span data-ttu-id="5900d-213">Piano di ripristino hello di test</span><span class="sxs-lookup"><span data-stu-id="5900d-213">Test hello recovery plan</span></span>
<span data-ttu-id="5900d-214">Dopo aver aggiunto piano toohello di hello runbook è possibile avviare un failover di test e visualizzarlo in azione.</span><span class="sxs-lookup"><span data-stu-id="5900d-214">Once you have added hello runbook toohello plan you can initiate a test failover and see it in action.</span></span> <span data-ttu-id="5900d-215">È sempre consigliabile toorun un tootest di failover di test del tooensure piano ripristino di hello e di applicazione che non siano presenti errori.</span><span class="sxs-lookup"><span data-stu-id="5900d-215">It is always recommended toorun a test failover tootest your application and hello recovery plan tooensure that there are no errors.</span></span>

1. <span data-ttu-id="5900d-216">Selezionare il piano di ripristino hello e avviare un failover di test.</span><span class="sxs-lookup"><span data-stu-id="5900d-216">Select hello recovery plan and initiate a test failover.</span></span>
2. <span data-ttu-id="5900d-217">Durante l'esecuzione di piani hello, è possibile visualizzare se hello runbook è stato eseguito o non mediante il relativo stato.</span><span class="sxs-lookup"><span data-stu-id="5900d-217">During hello plan execution, you can see whether hello runbook has executed or not via its status.</span></span>

   ![](media/site-recovery-runbook-automation/17.png)
3. <span data-ttu-id="5900d-218">È inoltre possibile visualizzare hello dettagliate sullo stato di esecuzione di runbook nella pagina processi di automazione di Azure hello per hello runbook.</span><span class="sxs-lookup"><span data-stu-id="5900d-218">You can also see hello detailed runbook execution status on hello Azure Automation jobs page for hello runbook.</span></span>

   ![](media/site-recovery-runbook-automation/18.png)
4. <span data-ttu-id="5900d-219">Dopo aver completato il failover hello, oltre al risultato dell'esecuzione runbook hello, è possibile visualizzare se l'esecuzione di hello ha esito positivo o non visita pagina macchina virtuale di Azure hello e analizzando gli endpoint hello.</span><span class="sxs-lookup"><span data-stu-id="5900d-219">After hello failover completes, apart from hello runbook execution result, you can see whether hello execution is successful or not by visiting hello Azure virtual machine page and looking at hello endpoints.</span></span>

![](media/site-recovery-runbook-automation/19.png)

## <a name="sample-scripts"></a><span data-ttu-id="5900d-220">Script di esempio</span><span class="sxs-lookup"><span data-stu-id="5900d-220">Sample scripts</span></span>
<span data-ttu-id="5900d-221">Anche se abbiamo esaminato in dettaglio automazione uno comunemente utilizzato l'operazione di aggiunta di una macchina virtuale di Azure di tooan endpoint in questa esercitazione, è possibile eseguire un numero di altre attività di automazione potente utilizzando l'automazione di Azure.</span><span class="sxs-lookup"><span data-stu-id="5900d-221">While we walked through automating one commonly used task of adding an endpoint tooan Azure virtual machine in this tutorial, you could do a number of other powerful automation tasks using Azure automation.</span></span> <span data-ttu-id="5900d-222">Microsoft e hello community di automazione di Azure forniscono i runbook di esempio che consentono di iniziare a creare la propria soluzioni e i runbook di utilità, che è possibile utilizzare come blocchi predefiniti per le attività di automazione più grandi.</span><span class="sxs-lookup"><span data-stu-id="5900d-222">Microsoft and hello Azure Automation community provide sample runbooks which can help you get started creating your own solutions, and utility runbooks, which you can use as building blocks for larger automation tasks.</span></span> <span data-ttu-id="5900d-223">Iniziare a utilizzare dalla raccolta hello e compilare i piani di ripristino di un solo clic potente per le applicazioni con Azure Site Recovery.</span><span class="sxs-lookup"><span data-stu-id="5900d-223">Start using them from hello gallery and build  powerful one-click recovery plans for your applications using Azure Site Recovery.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="5900d-224">Risorse aggiuntive</span><span class="sxs-lookup"><span data-stu-id="5900d-224">Additional Resources</span></span>
[<span data-ttu-id="5900d-225">Panoramica di Automazione di Azure</span><span class="sxs-lookup"><span data-stu-id="5900d-225">Azure Automation Overview</span></span>](http://msdn.microsoft.com/library/azure/dn643629.aspx "Panoramica di Automazione di Azure")

[<span data-ttu-id="5900d-226">Script di esempio di Automazione di Azure</span><span class="sxs-lookup"><span data-stu-id="5900d-226">Sample Azure Automation Scripts</span></span>](http://gallery.technet.microsoft.com/scriptcenter/site/search?f\[0\].Type=User&f\[0\].Value=SC%20Automation%20Product%20Team&f\[0\].Text=SC%20Automation%20Product%20Team "Script di esempio di Automazione di Azure")

---
title: aaaAdd piani toorecovery runbook di automazione di Azure in Azure Site Recovery | Documenti Microsoft
description: "Informazioni su come Azure Site Recovery può essere utile per estendere i piani di ripristino tramite Automazione di Azure. Informazioni su come le attività durante il ripristino tooAzure toocomplete complesso."
services: site-recovery
documentationcenter: 
author: ruturaj
manager: gauravd
editor: 
ms.assetid: ecece14d-5f92-4596-bbaf-5204addb95c2
ms.service: site-recovery
ms.devlang: powershell
ms.tgt_pltfrm: na
ms.topic: article
ms.workload: storage-backup-recovery
ms.date: 06/23/2017
ms.author: ruturajd@microsoft.com
ms.openlocfilehash: 90d517200cec5527e98a0d00da466bace587b70b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="add-azure-automation-runbooks-toorecovery-plans"></a><span data-ttu-id="283b7-104">Aggiungere i piani toorecovery runbook di automazione di Azure</span><span class="sxs-lookup"><span data-stu-id="283b7-104">Add Azure Automation runbooks toorecovery plans</span></span>
<span data-ttu-id="283b7-105">In questo articolo viene descritto l'integrazione di Azure Site Recovery con toohelp di automazione di Azure estendere i piani di ripristino.</span><span class="sxs-lookup"><span data-stu-id="283b7-105">In this article, we describe how Azure Site Recovery integrates with Azure Automation toohelp you extend your recovery plans.</span></span> <span data-ttu-id="283b7-106">I piani di ripristino possono orchestrare il ripristino di macchine virtuali protette con Site Recovery.</span><span class="sxs-lookup"><span data-stu-id="283b7-106">Recovery plans can orchestrate recovery of VMs that are protected with Site Recovery.</span></span> <span data-ttu-id="283b7-107">I piani di ripristino di lavoro per il cloud secondario tooa di replica e per la replica tooAzure.</span><span class="sxs-lookup"><span data-stu-id="283b7-107">Recovery plans work both for replication tooa secondary cloud, and for replication tooAzure.</span></span> <span data-ttu-id="283b7-108">I piani di ripristino consentono inoltre di garantire il ripristino di hello **in modo coerente accurate**, **repeatable**, e **automatizzati**.</span><span class="sxs-lookup"><span data-stu-id="283b7-108">Recovery plans also help make hello recovery **consistently accurate**, **repeatable**, and **automated**.</span></span> <span data-ttu-id="283b7-109">Se si esegue il failover tooAzure le macchine virtuali, integrazione con automazione di Azure estende i piani di ripristino.</span><span class="sxs-lookup"><span data-stu-id="283b7-109">If you fail over your VMs tooAzure, integration with Azure Automation extends your recovery plans.</span></span> <span data-ttu-id="283b7-110">È possibile utilizzarlo tooexecute runbook, che offrono l'attività di automazione potenti.</span><span class="sxs-lookup"><span data-stu-id="283b7-110">You can use it tooexecute runbooks, which offer powerful automation tasks.</span></span>

<span data-ttu-id="283b7-111">Nel caso di nuova tooAzure automazione, è possibile [iscriversi](https://azure.microsoft.com/services/automation/) e [scaricare gli script di esempio](https://azure.microsoft.com/documentation/scripts/).</span><span class="sxs-lookup"><span data-stu-id="283b7-111">If you are new tooAzure Automation, you can [sign up](https://azure.microsoft.com/services/automation/) and [download sample scripts](https://azure.microsoft.com/documentation/scripts/).</span></span> <span data-ttu-id="283b7-112">Per ulteriori informazioni e toolearn come tooorchestrate ripristino tooAzure utilizzando [i piani di ripristino](https://azure.microsoft.com/blog/?p=166264), vedere [Azure Site Recovery](https://azure.microsoft.com/services/site-recovery/).</span><span class="sxs-lookup"><span data-stu-id="283b7-112">For more information, and toolearn how tooorchestrate recovery tooAzure by using [recovery plans](https://azure.microsoft.com/blog/?p=166264), see [Azure Site Recovery](https://azure.microsoft.com/services/site-recovery/).</span></span>

<span data-ttu-id="283b7-113">Questo articolo descrive come è possibile integrare i runbook di Automazione di Azure nei piani di ripristino.</span><span class="sxs-lookup"><span data-stu-id="283b7-113">In this article, we describe how you can integrate Azure Automation runbooks into your recovery plans.</span></span> <span data-ttu-id="283b7-114">Utilizziamo esempi tooautomate attività di base che richiedevano in precedenza un intervento manuale.</span><span class="sxs-lookup"><span data-stu-id="283b7-114">We use examples tooautomate basic tasks that previously required manual intervention.</span></span> <span data-ttu-id="283b7-115">È inoltre possibile descrivere come tooconvert tooa un ripristino di più passaggi con clic singolo un'operazione di ripristino.</span><span class="sxs-lookup"><span data-stu-id="283b7-115">We also describe how tooconvert a multi-step recovery tooa single-click recovery action.</span></span>

## <a name="customize-hello-recovery-plan"></a><span data-ttu-id="283b7-116">Personalizzare il piano di ripristino hello</span><span class="sxs-lookup"><span data-stu-id="283b7-116">Customize hello recovery plan</span></span>
1. <span data-ttu-id="283b7-117">Passare toohello **Site Recovery** pannello risorsa piano di ripristino.</span><span class="sxs-lookup"><span data-stu-id="283b7-117">Go toohello **Site Recovery** recovery plan resource blade.</span></span> <span data-ttu-id="283b7-118">Per questo esempio, il piano di ripristino di hello ha due tooit aggiunte le macchine virtuali, per il ripristino.</span><span class="sxs-lookup"><span data-stu-id="283b7-118">For this example, hello recovery plan has two VMs added tooit, for recovery.</span></span> <span data-ttu-id="283b7-119">toobegin aggiunta di un runbook, fare clic su hello **Personalizza** scheda.</span><span class="sxs-lookup"><span data-stu-id="283b7-119">toobegin adding a runbook, click hello **Customize** tab.</span></span>

    ![Fare clic sul pulsante Personalizza hello](media/site-recovery-runbook-automation-new/essentials-rp.png)


2. <span data-ttu-id="283b7-121">Fare clic con il pulsante destro del mouse su **Gruppo 1: Avvio** e quindi scegliere **Aggiungi post-azione**.</span><span class="sxs-lookup"><span data-stu-id="283b7-121">Right-click **Group 1: Start**, and then select **Add post action**.</span></span>

    ![Fare clic con il pulsante destro del mouse su Gruppo 1: Avvio e scegliere Aggiungi post-azione](media/site-recovery-runbook-automation-new/customize-rp.png)

3. <span data-ttu-id="283b7-123">Fare clic su **Choose a script** (Scegli uno script).</span><span class="sxs-lookup"><span data-stu-id="283b7-123">Click **Choose a script**.</span></span>

4. <span data-ttu-id="283b7-124">In hello **azione Aggiorna** blade, script hello nome **Hello World**.</span><span class="sxs-lookup"><span data-stu-id="283b7-124">On hello **Update action** blade, name hello script **Hello World**.</span></span>

    ![Pannello di azione di aggiornamento Hello](media/site-recovery-runbook-automation-new/update-rp.png)

5. <span data-ttu-id="283b7-126">Immettere il nome di un account di Automazione.</span><span class="sxs-lookup"><span data-stu-id="283b7-126">Enter an Automation account name.</span></span>
    >[!NOTE]
    > <span data-ttu-id="283b7-127">account di automazione Hello può trovarsi in qualsiasi area di Azure.</span><span class="sxs-lookup"><span data-stu-id="283b7-127">hello Automation account can be in any Azure region.</span></span> <span data-ttu-id="283b7-128">account di automazione Hello deve essere in hello stessa sottoscrizione dell'insieme di credenziali di Azure Site Recovery hello.</span><span class="sxs-lookup"><span data-stu-id="283b7-128">hello Automation account must be in hello same subscription as hello Azure Site Recovery vault.</span></span>

6. <span data-ttu-id="283b7-129">Nell'account di Automazione selezionare un runbook.</span><span class="sxs-lookup"><span data-stu-id="283b7-129">In your Automation account, select a runbook.</span></span> <span data-ttu-id="283b7-130">Questo runbook è hello dello script eseguito durante l'esecuzione di hello hello del piano di ripristino, dopo il ripristino di hello del primo gruppo di hello.</span><span class="sxs-lookup"><span data-stu-id="283b7-130">This runbook is hello script that runs during hello execution of hello recovery plan, after hello recovery of hello first group.</span></span>

7. <span data-ttu-id="283b7-131">script di hello toosave, fare clic su **OK**.</span><span class="sxs-lookup"><span data-stu-id="283b7-131">toosave hello script, click **OK**.</span></span> <span data-ttu-id="283b7-132">script di Hello viene aggiunto troppo**gruppo 1: post-passaggi**.</span><span class="sxs-lookup"><span data-stu-id="283b7-132">hello script is added too**Group 1: Post-steps**.</span></span>

    ![Post-azione Gruppo 1: Avvio](media/site-recovery-runbook-automation-new/addedscript-rp.PNG)


## <a name="considerations-for-adding-a-script"></a><span data-ttu-id="283b7-134">Considerazioni per l'aggiunta di uno script</span><span class="sxs-lookup"><span data-stu-id="283b7-134">Considerations for adding a script</span></span>

* <span data-ttu-id="283b7-135">Per le opzioni troppo**eliminare un passaggio** o **aggiornare script hello**, fare doppio clic su script hello.</span><span class="sxs-lookup"><span data-stu-id="283b7-135">For options too**delete a step** or **update hello script**, right-click hello script.</span></span>
* <span data-ttu-id="283b7-136">Uno script è possibile eseguire in Azure durante il failover da un tooAzure macchina locale.</span><span class="sxs-lookup"><span data-stu-id="283b7-136">A script can run on Azure during failover from an on-premises machine tooAzure.</span></span> <span data-ttu-id="283b7-137">Inoltre possibile eseguire in Azure come sito primario di script prima della chiusura, durante il failback da tooan Azure nel computer locale.</span><span class="sxs-lookup"><span data-stu-id="283b7-137">It also can run on Azure as a primary-site script before shutdown, during failback from Azure tooan on-premises machine.</span></span>
* <span data-ttu-id="283b7-138">Quando è in esecuzione, inserisce un contesto del piano di ripristino.</span><span class="sxs-lookup"><span data-stu-id="283b7-138">When a script runs, it injects a recovery plan context.</span></span> <span data-ttu-id="283b7-139">Hello di esempio seguente viene illustrata una variabile di contesto:</span><span class="sxs-lookup"><span data-stu-id="283b7-139">hello following example shows a context variable:</span></span>

    ```
            {"RecoveryPlanName":"hrweb-recovery",

            "FailoverType":"Test",

            "FailoverDirection":"PrimaryToSecondary",

            "GroupId":"1",

            "VmMap":{"7a1069c6-c1d6-49c5-8c5d-33bfce8dd183":

                    { "SubscriptionId":"7a1111111-c1d6-49c5-8c5d-111ce8dd183",

                    "ResourceGroupName":"ContosoRG",

                    "CloudServiceName":"pod02hrweb-Chicago-test",

                    "RoleName":"Fabrikam-Hrweb-frontend-test",

                    "RecoveryPointId":"TimeStamp"}

                    }

            }
    ```

    <span data-ttu-id="283b7-140">Hello nella tabella seguente sono elencati il nome di hello e una descrizione di ogni variabile nel contesto di hello.</span><span class="sxs-lookup"><span data-stu-id="283b7-140">hello following table lists hello name and description of each variable in hello context.</span></span>

    | <span data-ttu-id="283b7-141">**Nome variabile**</span><span class="sxs-lookup"><span data-stu-id="283b7-141">**Variable name**</span></span> | <span data-ttu-id="283b7-142">**Descrizione**</span><span class="sxs-lookup"><span data-stu-id="283b7-142">**Description**</span></span> |
    | --- | --- |
    | <span data-ttu-id="283b7-143">RecoveryPlanName</span><span class="sxs-lookup"><span data-stu-id="283b7-143">RecoveryPlanName</span></span> |<span data-ttu-id="283b7-144">nome Hello del piano di hello in esecuzione.</span><span class="sxs-lookup"><span data-stu-id="283b7-144">hello name of hello plan being run.</span></span> <span data-ttu-id="283b7-145">Questa variabile consente di eseguire azioni diverse in base a nome piano di ripristino hello.</span><span class="sxs-lookup"><span data-stu-id="283b7-145">This variable helps you take different actions based on hello recovery plan name.</span></span> <span data-ttu-id="283b7-146">È inoltre possibile utilizzare script hello.</span><span class="sxs-lookup"><span data-stu-id="283b7-146">You also can reuse hello script.</span></span> |
    | <span data-ttu-id="283b7-147">FailoverType</span><span class="sxs-lookup"><span data-stu-id="283b7-147">FailoverType</span></span> |<span data-ttu-id="283b7-148">Specifica se il failover hello è un test, pianificato o non pianificato.</span><span class="sxs-lookup"><span data-stu-id="283b7-148">Specifies whether hello failover is a test, planned, or unplanned.</span></span> |
    | <span data-ttu-id="283b7-149">FailoverDirection</span><span class="sxs-lookup"><span data-stu-id="283b7-149">FailoverDirection</span></span> |<span data-ttu-id="283b7-150">Specifica se il ripristino del sito primario o secondario di tooa.</span><span class="sxs-lookup"><span data-stu-id="283b7-150">Specifies whether recovery is tooa primary or secondary site.</span></span> |
    | <span data-ttu-id="283b7-151">GroupID</span><span class="sxs-lookup"><span data-stu-id="283b7-151">GroupID</span></span> |<span data-ttu-id="283b7-152">Identifica il numero di gruppo hello nel piano di ripristino hello quando piano hello è in esecuzione.</span><span class="sxs-lookup"><span data-stu-id="283b7-152">Identifies hello group number in hello recovery plan when hello plan is running.</span></span> |
    | <span data-ttu-id="283b7-153">VmMap</span><span class="sxs-lookup"><span data-stu-id="283b7-153">VmMap</span></span> |<span data-ttu-id="283b7-154">Matrice di tutte le macchine virtuali nel gruppo di hello.</span><span class="sxs-lookup"><span data-stu-id="283b7-154">An array of all VMs in hello group.</span></span> |
    | <span data-ttu-id="283b7-155">VMMap key</span><span class="sxs-lookup"><span data-stu-id="283b7-155">VMMap key</span></span> |<span data-ttu-id="283b7-156">Chiave univoca (GUID) per ogni macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="283b7-156">A unique key (GUID) for each VM.</span></span> <span data-ttu-id="283b7-157">Di hello identico hello Azure Virtual Machine Manager (VMM) ID di hello macchina virtuale, se applicabile.</span><span class="sxs-lookup"><span data-stu-id="283b7-157">It's hello same as hello Azure Virtual Machine Manager (VMM) ID of hello VM, where applicable.</span></span> |
    | <span data-ttu-id="283b7-158">SubscriptionId</span><span class="sxs-lookup"><span data-stu-id="283b7-158">SubscriptionId</span></span> |<span data-ttu-id="283b7-159">ID sottoscrizione di Azure Hello in cui hello VM è stato creato.</span><span class="sxs-lookup"><span data-stu-id="283b7-159">hello Azure subscription ID in which hello VM was created.</span></span> |
    | <span data-ttu-id="283b7-160">RoleName</span><span class="sxs-lookup"><span data-stu-id="283b7-160">RoleName</span></span> |<span data-ttu-id="283b7-161">nome Hello di hello macchina virtuale di Azure che viene ripristinato.</span><span class="sxs-lookup"><span data-stu-id="283b7-161">hello name of hello Azure VM that's being recovered.</span></span> |
    | <span data-ttu-id="283b7-162">CloudServiceName</span><span class="sxs-lookup"><span data-stu-id="283b7-162">CloudServiceName</span></span> |<span data-ttu-id="283b7-163">nome del servizio cloud di Azure Hello che in cui hello VM è stato creato.</span><span class="sxs-lookup"><span data-stu-id="283b7-163">hello Azure cloud service name under which hello VM was created.</span></span> |
    | <span data-ttu-id="283b7-164">ResourceGroupName</span><span class="sxs-lookup"><span data-stu-id="283b7-164">ResourceGroupName</span></span>|<span data-ttu-id="283b7-165">nome del gruppo di risorse di Azure Hello che in cui hello VM è stato creato.</span><span class="sxs-lookup"><span data-stu-id="283b7-165">hello Azure resource group name under which hello VM was created.</span></span> |
    | <span data-ttu-id="283b7-166">RecoveryPointId</span><span class="sxs-lookup"><span data-stu-id="283b7-166">RecoveryPointId</span></span>|<span data-ttu-id="283b7-167">timestamp di Hello per quando viene recuperato hello macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="283b7-167">hello timestamp for when hello VM is recovered.</span></span> |

* <span data-ttu-id="283b7-168">Verificare che account di automazione di hello disponga hello seguenti moduli:</span><span class="sxs-lookup"><span data-stu-id="283b7-168">Ensure that hello Automation account has hello following modules:</span></span>
    * <span data-ttu-id="283b7-169">AzureRM.profile</span><span class="sxs-lookup"><span data-stu-id="283b7-169">AzureRM.profile</span></span>
    * <span data-ttu-id="283b7-170">AzureRM.Resources</span><span class="sxs-lookup"><span data-stu-id="283b7-170">AzureRM.Resources</span></span>
    * <span data-ttu-id="283b7-171">AzureRM.Automation</span><span class="sxs-lookup"><span data-stu-id="283b7-171">AzureRM.Automation</span></span>
    * <span data-ttu-id="283b7-172">AzureRM.Network</span><span class="sxs-lookup"><span data-stu-id="283b7-172">AzureRM.Network</span></span>
    * <span data-ttu-id="283b7-173">AzureRM.Compute</span><span class="sxs-lookup"><span data-stu-id="283b7-173">AzureRM.Compute</span></span>

<span data-ttu-id="283b7-174">Tutti i moduli devono essere di versioni compatibili.</span><span class="sxs-lookup"><span data-stu-id="283b7-174">All modules should be of compatible versions.</span></span> <span data-ttu-id="283b7-175">Un modo semplice di tooensure che tutti i moduli siano compatibili è versioni più recenti di hello toouse di tutti i moduli di hello.</span><span class="sxs-lookup"><span data-stu-id="283b7-175">An easy way tooensure that all modules are compatible is toouse hello latest versions of all hello modules.</span></span>

### <a name="access-all-vms-of-hello-vmmap-in-a-loop"></a><span data-ttu-id="283b7-176">Accedere a tutte le macchine virtuali di hello VMMap in un ciclo</span><span class="sxs-lookup"><span data-stu-id="283b7-176">Access all VMs of hello VMMap in a loop</span></span>
<span data-ttu-id="283b7-177">Utilizzare hello seguendo tooloop codice tra tutte le macchine virtuali di Microsoft VMMap hello:</span><span class="sxs-lookup"><span data-stu-id="283b7-177">Use hello following code tooloop across all VMs of hello Microsoft VMMap:</span></span>

```
$VMinfo = $RecoveryPlanContext.VmMap | Get-Member | Where-Object MemberType -EQ NoteProperty | select -ExpandProperty Name
$vmMap = $RecoveryPlanContext.VmMap
 foreach($VMID in $VMinfo)
 {
     $VM = $vmMap.$VMID                
             if( !(($VM -eq $Null) -Or ($VM.ResourceGroupName -eq $Null) -Or ($VM.RoleName -eq $Null))) {
         #this check is tooensure that we skip when some data is not available else it will fail
 Write-output "Resource group name ", $VM.ResourceGroupName
 Write-output "Rolename " = $VM.RoleName
     }
 }

```

> [!NOTE]
> <span data-ttu-id="283b7-178">Hello risorsa nome e il ruolo nome valori di gruppo sono vuoti quando script hello è un gruppo di avvio tooa pre-azione.</span><span class="sxs-lookup"><span data-stu-id="283b7-178">hello resource group name and role name values are empty when hello script is a pre-action tooa boot group.</span></span> <span data-ttu-id="283b7-179">i valori Hello vengono popolati solo se ha esito positivo hello VM del gruppo di failover.</span><span class="sxs-lookup"><span data-stu-id="283b7-179">hello values are populated only if hello VM of that group succeeds in failover.</span></span> <span data-ttu-id="283b7-180">script Hello è post-un'azione del gruppo di avvio hello.</span><span class="sxs-lookup"><span data-stu-id="283b7-180">hello script is a post-action of hello boot group.</span></span>

## <a name="use-hello-same-automation-runbook-in-multiple-recovery-plans"></a><span data-ttu-id="283b7-181">Utilizzare hello stesso runbook di automazione in più piani di ripristino</span><span class="sxs-lookup"><span data-stu-id="283b7-181">Use hello same Automation runbook in multiple recovery plans</span></span>

<span data-ttu-id="283b7-182">È possibile usare un unico script in più piani di ripristino servendosi di variabili esterne.</span><span class="sxs-lookup"><span data-stu-id="283b7-182">You can use a single script in multiple recovery plans by using external variables.</span></span> <span data-ttu-id="283b7-183">È possibile utilizzare [le variabili di automazione di Azure](../automation/automation-variables.md) toostore parametri che è possibile passare per il ripristino di un piano di esecuzione.</span><span class="sxs-lookup"><span data-stu-id="283b7-183">You can use [Azure Automation variables](../automation/automation-variables.md) toostore parameters that you can pass for a recovery plan execution.</span></span> <span data-ttu-id="283b7-184">Aggiungendo nome piano di ripristino hello come variabile toohello prefisso, è possibile creare le singole variabili per ogni piano di ripristino.</span><span class="sxs-lookup"><span data-stu-id="283b7-184">By adding hello recovery plan name as a prefix toohello variable, you can create individual variables for each recovery plan.</span></span> <span data-ttu-id="283b7-185">Quindi, è possibile usare le variabili di hello come parametri.</span><span class="sxs-lookup"><span data-stu-id="283b7-185">Then, use hello variables as parameters.</span></span> <span data-ttu-id="283b7-186">È possibile modificare un parametro senza modificare script hello, ma ancora modifica hello hello modo il funzionamento di script.</span><span class="sxs-lookup"><span data-stu-id="283b7-186">You can change a parameter without changing hello script, but still change hello way hello script works.</span></span>

### <a name="use-a-simple-string-variable-in-a-runbook-script"></a><span data-ttu-id="283b7-187">Usare una variabile di tipo stringa semplice nello script di un runbook</span><span class="sxs-lookup"><span data-stu-id="283b7-187">Use a simple string variable in a runbook script</span></span>

<span data-ttu-id="283b7-188">In questo esempio, uno script accetta input hello di un gruppo di sicurezza di rete (gruppo) e le applica toohello macchine virtuali di un piano di ripristino.</span><span class="sxs-lookup"><span data-stu-id="283b7-188">In this example, a script takes hello input of a Network Security Group (NSG) and applies it toohello VMs of a recovery plan.</span></span>

<span data-ttu-id="283b7-189">Per toodetect di script hello piano di ripristino è in esecuzione, utilizzare contesto piano di ripristino hello:</span><span class="sxs-lookup"><span data-stu-id="283b7-189">For hello script toodetect which recovery plan is running, use hello recovery plan context:</span></span>

```
workflow AddPublicIPAndNSG {
    param (
          [parameter(Mandatory=$false)]
          [Object]$RecoveryPlanContext
    )

    $RPName = $RecoveryPlanContext.RecoveryPlanName
```

<span data-ttu-id="283b7-190">tooapply un gruppo esistente, è necessario conoscere il nome di gruppo hello e nome del gruppo di risorse gruppo hello.</span><span class="sxs-lookup"><span data-stu-id="283b7-190">tooapply an existing NSG, you must know hello NSG name and hello NSG resource group name.</span></span> <span data-ttu-id="283b7-191">Usare queste variabili come input per gli script dei piani di ripristino.</span><span class="sxs-lookup"><span data-stu-id="283b7-191">Use these variables as inputs for recovery plan scripts.</span></span> <span data-ttu-id="283b7-192">toodo, creare due variabili in hello asset di account di automazione.</span><span class="sxs-lookup"><span data-stu-id="283b7-192">toodo this, create two variables in hello Automation account assets.</span></span> <span data-ttu-id="283b7-193">Aggiungere nome hello hello del piano di ripristino che si siano creando parametri hello per come nome di variabile toohello prefisso.</span><span class="sxs-lookup"><span data-stu-id="283b7-193">Add hello name of hello recovery plan that you are creating hello parameters for as a prefix toohello variable name.</span></span>

1. <span data-ttu-id="283b7-194">Creare un nome di gruppo hello toostore variabile.</span><span class="sxs-lookup"><span data-stu-id="283b7-194">Create a variable toostore hello NSG name.</span></span> <span data-ttu-id="283b7-195">Aggiungere un nome di variabile toohello prefisso utilizzando il nome di hello hello del piano di ripristino.</span><span class="sxs-lookup"><span data-stu-id="283b7-195">Add a prefix toohello variable name by using hello name of hello recovery plan.</span></span>

    ![Creare una variabile per il nome del gruppo sicurezza di rete](media/site-recovery-runbook-automation-new/var1.png)

2. <span data-ttu-id="283b7-197">Creare nome gruppo di risorse del gruppo una variabile toostore hello.</span><span class="sxs-lookup"><span data-stu-id="283b7-197">Create a variable toostore hello NSG's resource group name.</span></span> <span data-ttu-id="283b7-198">Aggiungere un nome di variabile toohello prefisso utilizzando il nome di hello hello del piano di ripristino.</span><span class="sxs-lookup"><span data-stu-id="283b7-198">Add a prefix toohello variable name by using hello name of hello recovery plan.</span></span>

    ![Creare un nome del gruppo di risorse del gruppo sicurezza di rete](media/site-recovery-runbook-automation-new/var2.png)


3.  <span data-ttu-id="283b7-200">Nello script hello utilizzare hello seguente i valori delle variabili riferimento codice tooget hello:</span><span class="sxs-lookup"><span data-stu-id="283b7-200">In hello script, use hello following reference code tooget hello variable values:</span></span>

    ```
    $NSGValue = $RecoveryPlanContext.RecoveryPlanName + "-NSG"
    $NSGRGValue = $RecoveryPlanContext.RecoveryPlanName + "-NSGRG"

    $NSGnameVar = Get-AutomationVariable -Name $NSGValue
    $RGnameVar = Get-AutomationVariable -Name $NSGRGValue
    ```

4.  <span data-ttu-id="283b7-201">Utilizzare le variabili di hello in hello runbook tooapply hello NSG toohello interfaccia di rete di hello failover VM:</span><span class="sxs-lookup"><span data-stu-id="283b7-201">Use hello variables in hello runbook tooapply hello NSG toohello network interface of hello failed-over VM:</span></span>

    ```
    InlineScript {
    if (($Using:NSGname -ne $Null) -And ($Using:NSGRGname -ne $Null)) {
            $NSG = Get-AzureRmNetworkSecurityGroup -Name $Using:NSGname -ResourceGroupName $Using:NSGRGname
            Write-output $NSG.Id
            #Apply hello NSG tooa network interface
            #$vnet = Get-AzureRmVirtualNetwork -ResourceGroupName TestRG -Name TestVNet
            #Set-AzureRmVirtualNetworkSubnetConfig -VirtualNetwork $vnet -Name FrontEnd `
            #  -AddressPrefix 192.168.1.0/24 -NetworkSecurityGroup $NSG
        }
    }
    ```

<span data-ttu-id="283b7-202">Per ogni piano di ripristino, creare variabili indipendenti, in modo che è possibile riutilizzare script hello.</span><span class="sxs-lookup"><span data-stu-id="283b7-202">For each recovery plan, create independent variables so that you can reuse hello script.</span></span> <span data-ttu-id="283b7-203">Aggiungere un prefisso con nome piano di ripristino hello.</span><span class="sxs-lookup"><span data-stu-id="283b7-203">Add a prefix by using hello recovery plan name.</span></span> <span data-ttu-id="283b7-204">Per uno script completo, end-to-end per questo scenario, vedere [aggiungere un tooVMs IP e di gruppo pubblico durante il failover di test di un piano di ripristino di Site Recovery](https://gallery.technet.microsoft.com/Add-Public-IP-and-NSG-to-a6bb8fee).</span><span class="sxs-lookup"><span data-stu-id="283b7-204">For a complete, end-to-end script for this scenario, see [Add a public IP and NSG tooVMs during test failover of a Site Recovery recovery plan](https://gallery.technet.microsoft.com/Add-Public-IP-and-NSG-to-a6bb8fee).</span></span>


### <a name="use-a-complex-variable-toostore-more-information"></a><span data-ttu-id="283b7-205">Utilizzare una variabile complessa di toostore ulteriori informazioni</span><span class="sxs-lookup"><span data-stu-id="283b7-205">Use a complex variable toostore more information</span></span>

<span data-ttu-id="283b7-206">Si consideri uno scenario in cui si desidera tooturn un singolo script in un indirizzo IP pubblico in macchine virtuali specifiche.</span><span class="sxs-lookup"><span data-stu-id="283b7-206">Consider a scenario in which you want a single script tooturn on a public IP on specific VMs.</span></span> <span data-ttu-id="283b7-207">In un altro scenario, è opportuno tooapply NSGs diversi in diverse macchine virtuali (non su tutte le macchine virtuali).</span><span class="sxs-lookup"><span data-stu-id="283b7-207">In another scenario, you might want tooapply different NSGs on different VMs (not on all VMs).</span></span> <span data-ttu-id="283b7-208">È possibile creare uno script riutilizzabile per qualsiasi piano di ripristino.</span><span class="sxs-lookup"><span data-stu-id="283b7-208">You can make a script that is reusable for any recovery plan.</span></span> <span data-ttu-id="283b7-209">Ogni piano di ripristino può avere un numero variabile di macchine virtuali.</span><span class="sxs-lookup"><span data-stu-id="283b7-209">Each recovery plan can have a variable number of VMs.</span></span> <span data-ttu-id="283b7-210">Ad esempio, un ripristino di SharePoint ha due front-end.</span><span class="sxs-lookup"><span data-stu-id="283b7-210">For example, a SharePoint recovery has two front ends.</span></span> <span data-ttu-id="283b7-211">Un'applicazione line-of-business (LOB) semplice ha un solo front-end.</span><span class="sxs-lookup"><span data-stu-id="283b7-211">A basic line-of-business (LOB) application has only one front end.</span></span> <span data-ttu-id="283b7-212">Non è possibile creare variabili separate per ogni piano di ripristino.</span><span class="sxs-lookup"><span data-stu-id="283b7-212">You cannot create separate variables for each recovery plan.</span></span> 

<span data-ttu-id="283b7-213">Nell'esempio seguente di hello, usare una tecnica di nuovo e creare un [variabile complessa](https://msdn.microsoft.com/library/dn913767.aspx?f=255&MSPPError=-2147217396) nell'asset di account di automazione di Azure hello.</span><span class="sxs-lookup"><span data-stu-id="283b7-213">In hello following example, we use a new technique and create a [complex variable](https://msdn.microsoft.com/library/dn913767.aspx?f=255&MSPPError=-2147217396) in hello Azure Automation account assets.</span></span> <span data-ttu-id="283b7-214">Questo risultato si ottiene specificando più valori.</span><span class="sxs-lookup"><span data-stu-id="283b7-214">You do this by specifying multiple values.</span></span> <span data-ttu-id="283b7-215">È necessario usare Azure PowerShell toocomplete hello alla procedura seguente:</span><span class="sxs-lookup"><span data-stu-id="283b7-215">You must use Azure PowerShell toocomplete hello following steps:</span></span>

1. <span data-ttu-id="283b7-216">In PowerShell, eseguire l'accesso tooyour sottoscrizione di Azure:</span><span class="sxs-lookup"><span data-stu-id="283b7-216">In PowerShell, sign in tooyour Azure subscription:</span></span>

    ```
    login-azurermaccount
    $sub = Get-AzureRmSubscription -Name <SubscriptionName>
    $sub | Select-AzureRmSubscription
    ```

2. <span data-ttu-id="283b7-217">parametri di hello toostore, creare hello complesso variabile utilizzando il nome di hello hello del piano di ripristino:</span><span class="sxs-lookup"><span data-stu-id="283b7-217">toostore hello parameters, create hello complex variable by using hello name of hello recovery plan:</span></span>

    ```
    $VMDetails = @{"VMGUID"=@{"ResourceGroupName"="RGNameOfNSG";"NSGName"="NameOfNSG"};"VMGUID2"=@{"ResourceGroupName"="RGNameOfNSG";"NSGName"="NameOfNSG"}}
        New-AzureRmAutomationVariable -ResourceGroupName <RG of Automation Account> -AutomationAccountName <AA Name> -Name <RecoveryPlanName> -Value $VMDetails -Encrypted $false
    ```

3. <span data-ttu-id="283b7-218">In questa variabile complesso, **VMDetails** è hello ID macchina virtuale per hello protetto macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="283b7-218">In this complex variable, **VMDetails** is hello VM ID for hello protected VM.</span></span> <span data-ttu-id="283b7-219">tooget hello, ID di macchina virtuale, nel portale di Azure hello visualizzare le proprietà VM hello.</span><span class="sxs-lookup"><span data-stu-id="283b7-219">tooget hello VM ID, in hello Azure portal, view hello VM properties.</span></span> <span data-ttu-id="283b7-220">Hello schermata riportata di seguito viene illustrata una variabile che archivia i dettagli di hello di due macchine virtuali:</span><span class="sxs-lookup"><span data-stu-id="283b7-220">hello following screenshot shows a variable that stores hello details of two VMs:</span></span>

    ![Utilizzare hello ID macchina virtuale come hello GUID](media/site-recovery-runbook-automation-new/vmguid.png)

4. <span data-ttu-id="283b7-222">Usare questa variabile nel runbook.</span><span class="sxs-lookup"><span data-stu-id="283b7-222">Use this variable in your runbook.</span></span> <span data-ttu-id="283b7-223">Se hello indicato che GUID di VM viene trovato nel contesto di piano di ripristino hello, applicare hello NSG hello VM:</span><span class="sxs-lookup"><span data-stu-id="283b7-223">If hello indicated VM GUID is found in hello recovery plan context, apply hello NSG on hello VM:</span></span>

    ```
    $VMDetailsObj = Get-AutomationVariable -Name $RecoveryPlanContext.RecoveryPlanName
    ```

4. <span data-ttu-id="283b7-224">Nel runbook, scorrere in ciclo hello macchine virtuali del contesto di piano di ripristino hello.</span><span class="sxs-lookup"><span data-stu-id="283b7-224">In your runbook, loop through hello VMs of hello recovery plan context.</span></span> <span data-ttu-id="283b7-225">Verificare l'esistenza di hello VM in **$VMDetailsObj**.</span><span class="sxs-lookup"><span data-stu-id="283b7-225">Check whether hello VM exists in **$VMDetailsObj**.</span></span> <span data-ttu-id="283b7-226">Se esiste, è possibile accedere alle proprietà di hello di hello tooapply variabile hello gruppo:</span><span class="sxs-lookup"><span data-stu-id="283b7-226">If it exists, access hello properties of hello variable tooapply hello NSG:</span></span>

    ```
        $VMinfo = $RecoveryPlanContext.VmMap | Get-Member | Where-Object MemberType -EQ NoteProperty | select -ExpandProperty Name
        $vmMap = $RecoveryPlanContext.VmMap

        foreach($VMID in $VMinfo) {
            Write-output $VMDetailsObj.value.$VMID

            if ($VMDetailsObj.value.$VMID -ne $Null) { #If hello VM exists in hello context, this will not b Null
                $VM = $vmMap.$VMID
                # Access hello properties of hello variable
                $NSGname = $VMDetailsObj.value.$VMID.'NSGName'
                $NSGRGname = $VMDetailsObj.value.$VMID.'NSGResourceGroupName'

                # Add code tooapply hello NSG properties toohello VM
            }
        }
    ```

<span data-ttu-id="283b7-227">È possibile utilizzare hello stesso script per i piani di ripristino diverso.</span><span class="sxs-lookup"><span data-stu-id="283b7-227">You can use hello same script for different recovery plans.</span></span> <span data-ttu-id="283b7-228">Immettere i parametri diversi archiviando hello corrispondente il piano di ripristino tooa in variabili diverse.</span><span class="sxs-lookup"><span data-stu-id="283b7-228">Enter different parameters by storing hello value that corresponds tooa recovery plan in different variables.</span></span>

## <a name="sample-scripts"></a><span data-ttu-id="283b7-229">Script di esempio</span><span class="sxs-lookup"><span data-stu-id="283b7-229">Sample scripts</span></span>

<span data-ttu-id="283b7-230">tooyour gli script di esempio toodeploy account di automazione, fare clic su hello **distribuire tooAzure** pulsante.</span><span class="sxs-lookup"><span data-stu-id="283b7-230">toodeploy sample scripts tooyour Automation account, click hello **Deploy tooAzure** button.</span></span>

<span data-ttu-id="283b7-231">[![Distribuire tooAzure](https://azurecomcdn.azureedge.net/mediahandler/acomblog/media/Default/blog/c4803408-340e-49e3-9a1f-0ed3f689813d.png)](https://aka.ms/asr-automationrunbooks-deploy)</span><span class="sxs-lookup"><span data-stu-id="283b7-231">[![Deploy tooAzure](https://azurecomcdn.azureedge.net/mediahandler/acomblog/media/Default/blog/c4803408-340e-49e3-9a1f-0ed3f689813d.png)](https://aka.ms/asr-automationrunbooks-deploy)</span></span>

<span data-ttu-id="283b7-232">Per un altro esempio, vedere hello video seguenti.</span><span class="sxs-lookup"><span data-stu-id="283b7-232">For another example, see hello following video.</span></span> <span data-ttu-id="283b7-233">Viene illustrato come toorecover tooAzure di applicazione WordPress una a due livelli:</span><span class="sxs-lookup"><span data-stu-id="283b7-233">It demonstrates how toorecover a two-tier WordPress application tooAzure:</span></span>


> [!VIDEO https://channel9.msdn.com/Series/Azure-Site-Recovery/One-click-failover-of-a-2-tier-WordPress-application-using-Azure-Site-Recovery/player]



## <a name="additional-resources"></a><span data-ttu-id="283b7-234">Risorse aggiuntive</span><span class="sxs-lookup"><span data-stu-id="283b7-234">Additional resources</span></span>
* [<span data-ttu-id="283b7-235">Account RunAs per il servizio Automazione di Azure</span><span class="sxs-lookup"><span data-stu-id="283b7-235">Azure Automation service Run As account</span></span>](../automation/automation-sec-configure-azure-runas-account.md)
* [<span data-ttu-id="283b7-236">Panoramica di Automazione di Azure</span><span class="sxs-lookup"><span data-stu-id="283b7-236">Azure Automation overview</span></span>](http://msdn.microsoft.com/library/azure/dn643629.aspx "Panoramica di Automazione di Azure")
* [<span data-ttu-id="283b7-237">Script di esempio di Automazione di Azure</span><span class="sxs-lookup"><span data-stu-id="283b7-237">Azure Automation sample scripts</span></span>](http://gallery.technet.microsoft.com/scriptcenter/site/search?f\[0\].Type=User&f\[0\].Value=SC%20Automation%20Product%20Team&f\[0\].Text=SC%20Automation%20Product%20Team "Script di esempio di Automazione di Azure")

---
title: Aggiungere runbook di Automazione di Azure ai piani di ripristino in Azure Site Recovery| Microsoft Docs
description: "Informazioni su come Azure Site Recovery può essere utile per estendere i piani di ripristino tramite Automazione di Azure. Informazioni su come eseguire attività complesse durante il ripristino in Azure."
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
ms.openlocfilehash: 064a6782970b950543f93c24800998c1f104c8df
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/29/2017
---
# <a name="add-azure-automation-runbooks-to-recovery-plans"></a><span data-ttu-id="9f72c-104">Aggiungere runbook di Automazione di Azure ai piani di ripristino</span><span class="sxs-lookup"><span data-stu-id="9f72c-104">Add Azure Automation runbooks to recovery plans</span></span>
<span data-ttu-id="9f72c-105">Questo articolo descrive come Azure Site Recovery si integra con Automazione di Azure per facilitare l'estensione dei piani di ripristino.</span><span class="sxs-lookup"><span data-stu-id="9f72c-105">In this article, we describe how Azure Site Recovery integrates with Azure Automation to help you extend your recovery plans.</span></span> <span data-ttu-id="9f72c-106">I piani di ripristino possono orchestrare il ripristino di macchine virtuali protette con Site Recovery.</span><span class="sxs-lookup"><span data-stu-id="9f72c-106">Recovery plans can orchestrate recovery of VMs that are protected with Site Recovery.</span></span> <span data-ttu-id="9f72c-107">I piani di ripristino possono essere usati sia per la replica in un cloud secondario che per la replica in Azure</span><span class="sxs-lookup"><span data-stu-id="9f72c-107">Recovery plans work both for replication to a secondary cloud, and for replication to Azure.</span></span> <span data-ttu-id="9f72c-108">e consentono anche di ottenere un ripristino **costantemente accurato**, **ripetibile** e **automatizzato**.</span><span class="sxs-lookup"><span data-stu-id="9f72c-108">Recovery plans also help make the recovery **consistently accurate**, **repeatable**, and **automated**.</span></span> <span data-ttu-id="9f72c-109">Se si esegue il failover delle macchine virtuali in Azure, l'integrazione con Automazione di Azure estende i piani di ripristino.</span><span class="sxs-lookup"><span data-stu-id="9f72c-109">If you fail over your VMs to Azure, integration with Azure Automation extends your recovery plans.</span></span> <span data-ttu-id="9f72c-110">È possibile usare questa funzionalità per eseguire runbook, che offrono attività di automazione dalle grandi potenzialità.</span><span class="sxs-lookup"><span data-stu-id="9f72c-110">You can use it to execute runbooks, which offer powerful automation tasks.</span></span>

<span data-ttu-id="9f72c-111">Se non si ha familiarità con Automazione di Azure, è possibile [iscriversi](https://azure.microsoft.com/services/automation/) e [scaricare script di esempio](https://azure.microsoft.com/documentation/scripts/).</span><span class="sxs-lookup"><span data-stu-id="9f72c-111">If you are new to Azure Automation, you can [sign up](https://azure.microsoft.com/services/automation/) and [download sample scripts](https://azure.microsoft.com/documentation/scripts/).</span></span> <span data-ttu-id="9f72c-112">Per altre informazioni e per scoprire come orchestrare il ripristino in Azure tramite i [piani di ripristino](https://azure.microsoft.com/blog/?p=166264), vedere [Azure Site Recovery](https://azure.microsoft.com/services/site-recovery/).</span><span class="sxs-lookup"><span data-stu-id="9f72c-112">For more information, and to learn how to orchestrate recovery to Azure by using [recovery plans](https://azure.microsoft.com/blog/?p=166264), see [Azure Site Recovery](https://azure.microsoft.com/services/site-recovery/).</span></span>

<span data-ttu-id="9f72c-113">Questo articolo descrive come è possibile integrare i runbook di Automazione di Azure nei piani di ripristino.</span><span class="sxs-lookup"><span data-stu-id="9f72c-113">In this article, we describe how you can integrate Azure Automation runbooks into your recovery plans.</span></span> <span data-ttu-id="9f72c-114">Vengono usati alcuni esempi per automatizzare attività di base che richiedevano in precedenza un intervento manuale.</span><span class="sxs-lookup"><span data-stu-id="9f72c-114">We use examples to automate basic tasks that previously required manual intervention.</span></span> <span data-ttu-id="9f72c-115">Viene anche descritto come convertire un ripristino in più passaggi in un'azione di ripristino con clic singolo.</span><span class="sxs-lookup"><span data-stu-id="9f72c-115">We also describe how to convert a multi-step recovery to a single-click recovery action.</span></span>

## <a name="customize-the-recovery-plan"></a><span data-ttu-id="9f72c-116">Personalizzare il piano di ripristino</span><span class="sxs-lookup"><span data-stu-id="9f72c-116">Customize the recovery plan</span></span>
1. <span data-ttu-id="9f72c-117">Passare al pannello delle risorse per il piano di ripristino di **Site Recovery**.</span><span class="sxs-lookup"><span data-stu-id="9f72c-117">Go to the **Site Recovery** recovery plan resource blade.</span></span> <span data-ttu-id="9f72c-118">In questo esempio, al piano di ripristino sono state aggiunte due macchine virtuali per il ripristino.</span><span class="sxs-lookup"><span data-stu-id="9f72c-118">For this example, the recovery plan has two VMs added to it, for recovery.</span></span> <span data-ttu-id="9f72c-119">Per iniziare ad aggiungere un runbook, fare clic sulla scheda **Personalizza**.</span><span class="sxs-lookup"><span data-stu-id="9f72c-119">To begin adding a runbook, click the **Customize** tab.</span></span>

    ![Fare clic sul pulsante Personalizza](media/site-recovery-runbook-automation-new/essentials-rp.png)


2. <span data-ttu-id="9f72c-121">Fare clic con il pulsante destro del mouse su **Gruppo 1: Avvio** e quindi scegliere **Aggiungi post-azione**.</span><span class="sxs-lookup"><span data-stu-id="9f72c-121">Right-click **Group 1: Start**, and then select **Add post action**.</span></span>

    ![Fare clic con il pulsante destro del mouse su Gruppo 1: Avvio e scegliere Aggiungi post-azione](media/site-recovery-runbook-automation-new/customize-rp.png)

3. <span data-ttu-id="9f72c-123">Fare clic su **Choose a script** (Scegli uno script).</span><span class="sxs-lookup"><span data-stu-id="9f72c-123">Click **Choose a script**.</span></span>

4. <span data-ttu-id="9f72c-124">Nel pannello **Aggiorna azione** assegnare il nome **Hello World** allo script.</span><span class="sxs-lookup"><span data-stu-id="9f72c-124">On the **Update action** blade, name the script **Hello World**.</span></span>

    ![Pannello Aggiorna azione](media/site-recovery-runbook-automation-new/update-rp.png)

5. <span data-ttu-id="9f72c-126">Immettere il nome di un account di Automazione.</span><span class="sxs-lookup"><span data-stu-id="9f72c-126">Enter an Automation account name.</span></span>
    >[!NOTE]
    > <span data-ttu-id="9f72c-127">L'account di Automazione può essere in qualsiasi area di Azure</span><span class="sxs-lookup"><span data-stu-id="9f72c-127">The Automation account can be in any Azure region.</span></span> <span data-ttu-id="9f72c-128">e deve trovarsi nella stessa sottoscrizione dell'insieme di credenziali di Azure Site Recovery.</span><span class="sxs-lookup"><span data-stu-id="9f72c-128">The Automation account must be in the same subscription as the Azure Site Recovery vault.</span></span>

6. <span data-ttu-id="9f72c-129">Nell'account di Automazione selezionare un runbook.</span><span class="sxs-lookup"><span data-stu-id="9f72c-129">In your Automation account, select a runbook.</span></span> <span data-ttu-id="9f72c-130">Questo runbook è lo script che viene eseguito durante l'esecuzione del piano di ripristino dopo il ripristino del primo gruppo.</span><span class="sxs-lookup"><span data-stu-id="9f72c-130">This runbook is the script that runs during the execution of the recovery plan, after the recovery of the first group.</span></span>

7. <span data-ttu-id="9f72c-131">Fare clic su **OK** per salvare lo script.</span><span class="sxs-lookup"><span data-stu-id="9f72c-131">To save the script, click **OK**.</span></span> <span data-ttu-id="9f72c-132">Lo script viene aggiunto a **Gruppo 1: passaggi successivi**.</span><span class="sxs-lookup"><span data-stu-id="9f72c-132">The script is added to **Group 1: Post-steps**.</span></span>

    ![Post-azione Gruppo 1: Avvio](media/site-recovery-runbook-automation-new/addedscript-rp.PNG)


## <a name="considerations-for-adding-a-script"></a><span data-ttu-id="9f72c-134">Considerazioni per l'aggiunta di uno script</span><span class="sxs-lookup"><span data-stu-id="9f72c-134">Considerations for adding a script</span></span>

* <span data-ttu-id="9f72c-135">Per accedere alle opzioni per **eliminare un passaggio** o **aggiornare lo script**, fare clic con il pulsante destro del mouse sullo script.</span><span class="sxs-lookup"><span data-stu-id="9f72c-135">For options to **delete a step** or **update the script**, right-click the script.</span></span>
* <span data-ttu-id="9f72c-136">È possibile eseguire uno script in Azure durante il failover da un computer locale ad Azure.</span><span class="sxs-lookup"><span data-stu-id="9f72c-136">A script can run on Azure during failover from an on-premises machine to Azure.</span></span> <span data-ttu-id="9f72c-137">È anche possibile eseguirlo in Azure come script del sito primario prima dell'arresto, durante il failback da Azure a un computer locale.</span><span class="sxs-lookup"><span data-stu-id="9f72c-137">It also can run on Azure as a primary-site script before shutdown, during failback from Azure to an on-premises machine.</span></span>
* <span data-ttu-id="9f72c-138">Quando è in esecuzione, inserisce un contesto del piano di ripristino.</span><span class="sxs-lookup"><span data-stu-id="9f72c-138">When a script runs, it injects a recovery plan context.</span></span> <span data-ttu-id="9f72c-139">L'esempio seguente mostra una variabile di contesto:</span><span class="sxs-lookup"><span data-stu-id="9f72c-139">The following example shows a context variable:</span></span>

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

    <span data-ttu-id="9f72c-140">La tabella seguente indica il nome e la descrizione di ogni variabile nel contesto.</span><span class="sxs-lookup"><span data-stu-id="9f72c-140">The following table lists the name and description of each variable in the context.</span></span>

    | <span data-ttu-id="9f72c-141">**Nome variabile**</span><span class="sxs-lookup"><span data-stu-id="9f72c-141">**Variable name**</span></span> | <span data-ttu-id="9f72c-142">**Descrizione**</span><span class="sxs-lookup"><span data-stu-id="9f72c-142">**Description**</span></span> |
    | --- | --- |
    | <span data-ttu-id="9f72c-143">RecoveryPlanName</span><span class="sxs-lookup"><span data-stu-id="9f72c-143">RecoveryPlanName</span></span> |<span data-ttu-id="9f72c-144">Nome del piano in esecuzione.</span><span class="sxs-lookup"><span data-stu-id="9f72c-144">The name of the plan being run.</span></span> <span data-ttu-id="9f72c-145">Questa variabile consente di eseguire azioni diverse in base al nome del piano di ripristino.</span><span class="sxs-lookup"><span data-stu-id="9f72c-145">This variable helps you take different actions based on the recovery plan name.</span></span> <span data-ttu-id="9f72c-146">È anche possibile riutilizzare lo script.</span><span class="sxs-lookup"><span data-stu-id="9f72c-146">You also can reuse the script.</span></span> |
    | <span data-ttu-id="9f72c-147">FailoverType</span><span class="sxs-lookup"><span data-stu-id="9f72c-147">FailoverType</span></span> |<span data-ttu-id="9f72c-148">Specifica se il failover è di test, pianificato o non pianificato.</span><span class="sxs-lookup"><span data-stu-id="9f72c-148">Specifies whether the failover is a test, planned, or unplanned.</span></span> |
    | <span data-ttu-id="9f72c-149">FailoverDirection</span><span class="sxs-lookup"><span data-stu-id="9f72c-149">FailoverDirection</span></span> |<span data-ttu-id="9f72c-150">Specifica se il ripristino avviene in un sito primario o secondario.</span><span class="sxs-lookup"><span data-stu-id="9f72c-150">Specifies whether recovery is to a primary or secondary site.</span></span> |
    | <span data-ttu-id="9f72c-151">GroupID</span><span class="sxs-lookup"><span data-stu-id="9f72c-151">GroupID</span></span> |<span data-ttu-id="9f72c-152">Identifica il numero del gruppo nel piano di ripristino quando il piano è in esecuzione.</span><span class="sxs-lookup"><span data-stu-id="9f72c-152">Identifies the group number in the recovery plan when the plan is running.</span></span> |
    | <span data-ttu-id="9f72c-153">VmMap</span><span class="sxs-lookup"><span data-stu-id="9f72c-153">VmMap</span></span> |<span data-ttu-id="9f72c-154">Matrice di tutte le macchine virtuali nel gruppo.</span><span class="sxs-lookup"><span data-stu-id="9f72c-154">An array of all VMs in the group.</span></span> |
    | <span data-ttu-id="9f72c-155">VMMap key</span><span class="sxs-lookup"><span data-stu-id="9f72c-155">VMMap key</span></span> |<span data-ttu-id="9f72c-156">Chiave univoca (GUID) per ogni macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="9f72c-156">A unique key (GUID) for each VM.</span></span> <span data-ttu-id="9f72c-157">È uguale all'ID di Azure Virtual Machine Manager (VMM) della macchina virtuale, se applicabile.</span><span class="sxs-lookup"><span data-stu-id="9f72c-157">It's the same as the Azure Virtual Machine Manager (VMM) ID of the VM, where applicable.</span></span> |
    | <span data-ttu-id="9f72c-158">SubscriptionId</span><span class="sxs-lookup"><span data-stu-id="9f72c-158">SubscriptionId</span></span> |<span data-ttu-id="9f72c-159">ID della sottoscrizione di Azure in cui viene creata la macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="9f72c-159">The Azure subscription ID in which the VM was created.</span></span> |
    | <span data-ttu-id="9f72c-160">RoleName</span><span class="sxs-lookup"><span data-stu-id="9f72c-160">RoleName</span></span> |<span data-ttu-id="9f72c-161">Nome della macchina virtuale di Azure in corso di ripristino.</span><span class="sxs-lookup"><span data-stu-id="9f72c-161">The name of the Azure VM that's being recovered.</span></span> |
    | <span data-ttu-id="9f72c-162">CloudServiceName</span><span class="sxs-lookup"><span data-stu-id="9f72c-162">CloudServiceName</span></span> |<span data-ttu-id="9f72c-163">Nome del servizio cloud di Azure in cui è stata creata la macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="9f72c-163">The Azure cloud service name under which the VM was created.</span></span> |
    | <span data-ttu-id="9f72c-164">ResourceGroupName</span><span class="sxs-lookup"><span data-stu-id="9f72c-164">ResourceGroupName</span></span>|<span data-ttu-id="9f72c-165">Nome del gruppo di risorse di Azure in cui è stata creata la macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="9f72c-165">The Azure resource group name under which the VM was created.</span></span> |
    | <span data-ttu-id="9f72c-166">RecoveryPointId</span><span class="sxs-lookup"><span data-stu-id="9f72c-166">RecoveryPointId</span></span>|<span data-ttu-id="9f72c-167">Timestamp del ripristino della macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="9f72c-167">The timestamp for when the VM is recovered.</span></span> |

* <span data-ttu-id="9f72c-168">Assicurarsi che l'account di Automazione abbia i moduli seguenti:</span><span class="sxs-lookup"><span data-stu-id="9f72c-168">Ensure that the Automation account has the following modules:</span></span>
    * <span data-ttu-id="9f72c-169">AzureRM.profile</span><span class="sxs-lookup"><span data-stu-id="9f72c-169">AzureRM.profile</span></span>
    * <span data-ttu-id="9f72c-170">AzureRM.Resources</span><span class="sxs-lookup"><span data-stu-id="9f72c-170">AzureRM.Resources</span></span>
    * <span data-ttu-id="9f72c-171">AzureRM.Automation</span><span class="sxs-lookup"><span data-stu-id="9f72c-171">AzureRM.Automation</span></span>
    * <span data-ttu-id="9f72c-172">AzureRM.Network</span><span class="sxs-lookup"><span data-stu-id="9f72c-172">AzureRM.Network</span></span>
    * <span data-ttu-id="9f72c-173">AzureRM.Compute</span><span class="sxs-lookup"><span data-stu-id="9f72c-173">AzureRM.Compute</span></span>

<span data-ttu-id="9f72c-174">Tutti i moduli devono essere di versioni compatibili.</span><span class="sxs-lookup"><span data-stu-id="9f72c-174">All modules should be of compatible versions.</span></span> <span data-ttu-id="9f72c-175">Un modo semplice per assicurarsi che tutti i moduli siano compatibili consiste nell'usare le versioni più recenti di tutti i moduli.</span><span class="sxs-lookup"><span data-stu-id="9f72c-175">An easy way to ensure that all modules are compatible is to use the latest versions of all the modules.</span></span>

### <a name="access-all-vms-of-the-vmmap-in-a-loop"></a><span data-ttu-id="9f72c-176">Accedere a tutte le macchine virtuali di VMMap in ciclo</span><span class="sxs-lookup"><span data-stu-id="9f72c-176">Access all VMs of the VMMap in a loop</span></span>
<span data-ttu-id="9f72c-177">Usare il frammento di codice seguente per accedere a tutte le macchine virtuali di Microsoft VMMap in ciclo:</span><span class="sxs-lookup"><span data-stu-id="9f72c-177">Use the following code to loop across all VMs of the Microsoft VMMap:</span></span>

```
$VMinfo = $RecoveryPlanContext.VmMap | Get-Member | Where-Object MemberType -EQ NoteProperty | select -ExpandProperty Name
$vmMap = $RecoveryPlanContext.VmMap
 foreach($VMID in $VMinfo)
 {
     $VM = $vmMap.$VMID                
             if( !(($VM -eq $Null) -Or ($VM.ResourceGroupName -eq $Null) -Or ($VM.RoleName -eq $Null))) {
         #this check is to ensure that we skip when some data is not available else it will fail
 Write-output "Resource group name ", $VM.ResourceGroupName
 Write-output "Rolename " = $VM.RoleName
     }
 }

```

> [!NOTE]
> <span data-ttu-id="9f72c-178">Il nome del gruppo di risorse e il nome del ruolo sono vuoti quando lo script è una pre-azione per un gruppo di avvio.</span><span class="sxs-lookup"><span data-stu-id="9f72c-178">The resource group name and role name values are empty when the script is a pre-action to a boot group.</span></span> <span data-ttu-id="9f72c-179">I valori vengono popolati solo se il failover della macchina virtuale di tale gruppo ha esito positivo.</span><span class="sxs-lookup"><span data-stu-id="9f72c-179">The values are populated only if the VM of that group succeeds in failover.</span></span> <span data-ttu-id="9f72c-180">Lo script è una post-azione del gruppo di avvio.</span><span class="sxs-lookup"><span data-stu-id="9f72c-180">The script is a post-action of the boot group.</span></span>

## <a name="use-the-same-automation-runbook-in-multiple-recovery-plans"></a><span data-ttu-id="9f72c-181">Usare lo stesso runbook di Automazione in più piani di ripristino</span><span class="sxs-lookup"><span data-stu-id="9f72c-181">Use the same Automation runbook in multiple recovery plans</span></span>

<span data-ttu-id="9f72c-182">È possibile usare un unico script in più piani di ripristino servendosi di variabili esterne.</span><span class="sxs-lookup"><span data-stu-id="9f72c-182">You can use a single script in multiple recovery plans by using external variables.</span></span> <span data-ttu-id="9f72c-183">È possibile usare le [variabili di Automazione di Azure](../automation/automation-variables.md) per archiviare i parametri da passare per l'esecuzione di un piano di ripristino.</span><span class="sxs-lookup"><span data-stu-id="9f72c-183">You can use [Azure Automation variables](../automation/automation-variables.md) to store parameters that you can pass for a recovery plan execution.</span></span> <span data-ttu-id="9f72c-184">Aggiungendo il nome del piano di ripristino come prefisso per la variabile, è possibile creare singole variabili per ogni piano di ripristino.</span><span class="sxs-lookup"><span data-stu-id="9f72c-184">By adding the recovery plan name as a prefix to the variable, you can create individual variables for each recovery plan.</span></span> <span data-ttu-id="9f72c-185">Usare quindi le variabili come parametri.</span><span class="sxs-lookup"><span data-stu-id="9f72c-185">Then, use the variables as parameters.</span></span> <span data-ttu-id="9f72c-186">È possibile modificare un parametro senza modificare lo script, cambiando comunque il funzionamento dello script.</span><span class="sxs-lookup"><span data-stu-id="9f72c-186">You can change a parameter without changing the script, but still change the way the script works.</span></span>

### <a name="use-a-simple-string-variable-in-a-runbook-script"></a><span data-ttu-id="9f72c-187">Usare una variabile di tipo stringa semplice nello script di un runbook</span><span class="sxs-lookup"><span data-stu-id="9f72c-187">Use a simple string variable in a runbook script</span></span>

<span data-ttu-id="9f72c-188">In questo esempio, uno script accetta l'input di un gruppo di sicurezza di rete e lo applica alle macchine virtuali di un piano di ripristino.</span><span class="sxs-lookup"><span data-stu-id="9f72c-188">In this example, a script takes the input of a Network Security Group (NSG) and applies it to the VMs of a recovery plan.</span></span>

<span data-ttu-id="9f72c-189">Per fare in modo che lo script rilevi quale piano di ripristino è in esecuzione, usare il contesto del piano di ripristino:</span><span class="sxs-lookup"><span data-stu-id="9f72c-189">For the script to detect which recovery plan is running, use the recovery plan context:</span></span>

```
workflow AddPublicIPAndNSG {
    param (
          [parameter(Mandatory=$false)]
          [Object]$RecoveryPlanContext
    )

    $RPName = $RecoveryPlanContext.RecoveryPlanName
```

<span data-ttu-id="9f72c-190">Per applicare un gruppo di sicurezza di rete esistente, è necessario conoscere il nome e il gruppo di risorse del gruppo sicurezza di rete.</span><span class="sxs-lookup"><span data-stu-id="9f72c-190">To apply an existing NSG, you must know the NSG name and the NSG resource group name.</span></span> <span data-ttu-id="9f72c-191">Usare queste variabili come input per gli script dei piani di ripristino.</span><span class="sxs-lookup"><span data-stu-id="9f72c-191">Use these variables as inputs for recovery plan scripts.</span></span> <span data-ttu-id="9f72c-192">A tale scopo, creare due variabili negli asset dell'account di Automazione.</span><span class="sxs-lookup"><span data-stu-id="9f72c-192">To do this, create two variables in the Automation account assets.</span></span> <span data-ttu-id="9f72c-193">Aggiungere il nome del piano di ripristino per il quale si stanno creando i parametri come prefisso del nome della variabile.</span><span class="sxs-lookup"><span data-stu-id="9f72c-193">Add the name of the recovery plan that you are creating the parameters for as a prefix to the variable name.</span></span>

1. <span data-ttu-id="9f72c-194">Creare una variabile per archiviare il nome del gruppo sicurezza di rete.</span><span class="sxs-lookup"><span data-stu-id="9f72c-194">Create a variable to store the NSG name.</span></span> <span data-ttu-id="9f72c-195">Aggiungere un prefisso al nome della variabile usando il nome del piano di ripristino.</span><span class="sxs-lookup"><span data-stu-id="9f72c-195">Add a prefix to the variable name by using the name of the recovery plan.</span></span>

    ![Creare una variabile per il nome del gruppo sicurezza di rete](media/site-recovery-runbook-automation-new/var1.png)

2. <span data-ttu-id="9f72c-197">Creare una variabile per archiviare il nome del gruppo di risorse del gruppo sicurezza di rete.</span><span class="sxs-lookup"><span data-stu-id="9f72c-197">Create a variable to store the NSG's resource group name.</span></span> <span data-ttu-id="9f72c-198">Aggiungere un prefisso al nome della variabile usando il nome del piano di ripristino.</span><span class="sxs-lookup"><span data-stu-id="9f72c-198">Add a prefix to the variable name by using the name of the recovery plan.</span></span>

    ![Creare un nome del gruppo di risorse del gruppo sicurezza di rete](media/site-recovery-runbook-automation-new/var2.png)


3.  <span data-ttu-id="9f72c-200">Nello script usare il codice di riferimento seguente per ottenere i valori delle variabili:</span><span class="sxs-lookup"><span data-stu-id="9f72c-200">In the script, use the following reference code to get the variable values:</span></span>

    ```
    $NSGValue = $RecoveryPlanContext.RecoveryPlanName + "-NSG"
    $NSGRGValue = $RecoveryPlanContext.RecoveryPlanName + "-NSGRG"

    $NSGnameVar = Get-AutomationVariable -Name $NSGValue
    $RGnameVar = Get-AutomationVariable -Name $NSGRGValue
    ```

4.  <span data-ttu-id="9f72c-201">Usare le variabili nel runbook per applicare il gruppo di sicurezza di rete all'interfaccia di rete della macchina virtuale di cui è stato eseguito il failover:</span><span class="sxs-lookup"><span data-stu-id="9f72c-201">Use the variables in the runbook to apply the NSG to the network interface of the failed-over VM:</span></span>

    ```
    InlineScript {
    if (($Using:NSGname -ne $Null) -And ($Using:NSGRGname -ne $Null)) {
            $NSG = Get-AzureRmNetworkSecurityGroup -Name $Using:NSGname -ResourceGroupName $Using:NSGRGname
            Write-output $NSG.Id
            #Apply the NSG to a network interface
            #$vnet = Get-AzureRmVirtualNetwork -ResourceGroupName TestRG -Name TestVNet
            #Set-AzureRmVirtualNetworkSubnetConfig -VirtualNetwork $vnet -Name FrontEnd `
            #  -AddressPrefix 192.168.1.0/24 -NetworkSecurityGroup $NSG
        }
    }
    ```

<span data-ttu-id="9f72c-202">Creare variabili indipendenti per ogni piano di ripristino, in modo che sia possibile riutilizzare lo script.</span><span class="sxs-lookup"><span data-stu-id="9f72c-202">For each recovery plan, create independent variables so that you can reuse the script.</span></span> <span data-ttu-id="9f72c-203">Aggiungere un prefisso con il nome del piano di ripristino.</span><span class="sxs-lookup"><span data-stu-id="9f72c-203">Add a prefix by using the recovery plan name.</span></span> <span data-ttu-id="9f72c-204">Per uno script completo per questo scenario, vedere [Add a public IP and NSG to VMs during test failover of a Site Recovery recovery plan](https://gallery.technet.microsoft.com/Add-Public-IP-and-NSG-to-a6bb8fee) (Aggiungere un indirizzo IP pubblico e un gruppo di sicurezza di rete alle macchina virtuali durante il failover di test di un piano di ripristino di Site Recovery).</span><span class="sxs-lookup"><span data-stu-id="9f72c-204">For a complete, end-to-end script for this scenario, see [Add a public IP and NSG to VMs during test failover of a Site Recovery recovery plan](https://gallery.technet.microsoft.com/Add-Public-IP-and-NSG-to-a6bb8fee).</span></span>


### <a name="use-a-complex-variable-to-store-more-information"></a><span data-ttu-id="9f72c-205">Usare una variabile complessa per archiviare altre informazioni</span><span class="sxs-lookup"><span data-stu-id="9f72c-205">Use a complex variable to store more information</span></span>

<span data-ttu-id="9f72c-206">Si consideri uno scenario in cui si vuole usare un singolo script per attivare un indirizzo IP pubblico in macchine virtuali specifiche.</span><span class="sxs-lookup"><span data-stu-id="9f72c-206">Consider a scenario in which you want a single script to turn on a public IP on specific VMs.</span></span> <span data-ttu-id="9f72c-207">In un altro scenario potrebbe essere necessario applicare gruppi di sicurezza di rete diversi in diverse macchine virtuali e non in tutte le macchine virtuali.</span><span class="sxs-lookup"><span data-stu-id="9f72c-207">In another scenario, you might want to apply different NSGs on different VMs (not on all VMs).</span></span> <span data-ttu-id="9f72c-208">È possibile creare uno script riutilizzabile per qualsiasi piano di ripristino.</span><span class="sxs-lookup"><span data-stu-id="9f72c-208">You can make a script that is reusable for any recovery plan.</span></span> <span data-ttu-id="9f72c-209">Ogni piano di ripristino può avere un numero variabile di macchine virtuali.</span><span class="sxs-lookup"><span data-stu-id="9f72c-209">Each recovery plan can have a variable number of VMs.</span></span> <span data-ttu-id="9f72c-210">Ad esempio, un ripristino di SharePoint ha due front-end.</span><span class="sxs-lookup"><span data-stu-id="9f72c-210">For example, a SharePoint recovery has two front ends.</span></span> <span data-ttu-id="9f72c-211">Un'applicazione line-of-business (LOB) semplice ha un solo front-end.</span><span class="sxs-lookup"><span data-stu-id="9f72c-211">A basic line-of-business (LOB) application has only one front end.</span></span> <span data-ttu-id="9f72c-212">Non è possibile creare variabili separate per ogni piano di ripristino.</span><span class="sxs-lookup"><span data-stu-id="9f72c-212">You cannot create separate variables for each recovery plan.</span></span> 

<span data-ttu-id="9f72c-213">Nell'esempio seguente viene usata una nuova tecnica e viene creata una [variabile complessa](https://msdn.microsoft.com/library/dn913767.aspx?f=255&MSPPError=-2147217396) negli asset dell'account di Automazione di Azure.</span><span class="sxs-lookup"><span data-stu-id="9f72c-213">In the following example, we use a new technique and create a [complex variable](https://msdn.microsoft.com/library/dn913767.aspx?f=255&MSPPError=-2147217396) in the Azure Automation account assets.</span></span> <span data-ttu-id="9f72c-214">Questo risultato si ottiene specificando più valori.</span><span class="sxs-lookup"><span data-stu-id="9f72c-214">You do this by specifying multiple values.</span></span> <span data-ttu-id="9f72c-215">Per eseguire questa procedura, è necessario usare Azure PowerShell:</span><span class="sxs-lookup"><span data-stu-id="9f72c-215">You must use Azure PowerShell to complete the following steps:</span></span>

1. <span data-ttu-id="9f72c-216">In PowerShell accedere alla sottoscrizione di Azure:</span><span class="sxs-lookup"><span data-stu-id="9f72c-216">In PowerShell, sign in to your Azure subscription:</span></span>

    ```
    login-azurermaccount
    $sub = Get-AzureRmSubscription -Name <SubscriptionName>
    $sub | Select-AzureRmSubscription
    ```

2. <span data-ttu-id="9f72c-217">Per archiviare i parametri, creare la variabile complessa usando il nome del piano di ripristino:</span><span class="sxs-lookup"><span data-stu-id="9f72c-217">To store the parameters, create the complex variable by using the name of the recovery plan:</span></span>

    ```
    $VMDetails = @{"VMGUID"=@{"ResourceGroupName"="RGNameOfNSG";"NSGName"="NameOfNSG"};"VMGUID2"=@{"ResourceGroupName"="RGNameOfNSG";"NSGName"="NameOfNSG"}}
        New-AzureRmAutomationVariable -ResourceGroupName <RG of Automation Account> -AutomationAccountName <AA Name> -Name <RecoveryPlanName> -Value $VMDetails -Encrypted $false
    ```

3. <span data-ttu-id="9f72c-218">In questa variabile complessa **VMDetails** è l'ID della macchina virtuale protetta.</span><span class="sxs-lookup"><span data-stu-id="9f72c-218">In this complex variable, **VMDetails** is the VM ID for the protected VM.</span></span> <span data-ttu-id="9f72c-219">Per ottenere l'ID di macchina virtuale, visualizzare le proprietà della macchina virtuale nel portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="9f72c-219">To get the VM ID, in the Azure portal, view the VM properties.</span></span> <span data-ttu-id="9f72c-220">Lo screenshot seguente mostra una variabile che archivia i dettagli di due macchine virtuali:</span><span class="sxs-lookup"><span data-stu-id="9f72c-220">The following screenshot shows a variable that stores the details of two VMs:</span></span>

    ![Usare l'ID della macchina virtuale come GUID](media/site-recovery-runbook-automation-new/vmguid.png)

4. <span data-ttu-id="9f72c-222">Usare questa variabile nel runbook.</span><span class="sxs-lookup"><span data-stu-id="9f72c-222">Use this variable in your runbook.</span></span> <span data-ttu-id="9f72c-223">Se il GUID della macchina virtuale indicato viene trovato nel contesto del piano di ripristino, è possibile applicare il gruppo di sicurezza di rete nella macchina virtuale:</span><span class="sxs-lookup"><span data-stu-id="9f72c-223">If the indicated VM GUID is found in the recovery plan context, apply the NSG on the VM:</span></span>

    ```
    $VMDetailsObj = Get-AutomationVariable -Name $RecoveryPlanContext.RecoveryPlanName
    ```

4. <span data-ttu-id="9f72c-224">Nel runbook scorrere in ciclo le macchine virtuali del contesto del piano di ripristino.</span><span class="sxs-lookup"><span data-stu-id="9f72c-224">In your runbook, loop through the VMs of the recovery plan context.</span></span> <span data-ttu-id="9f72c-225">Controllare se la macchina virtuale esiste in **$VMDetailsObj**.</span><span class="sxs-lookup"><span data-stu-id="9f72c-225">Check whether the VM exists in **$VMDetailsObj**.</span></span> <span data-ttu-id="9f72c-226">Se esiste, accedere alle proprietà della variabile per applicare il gruppo di sicurezza di rete:</span><span class="sxs-lookup"><span data-stu-id="9f72c-226">If it exists, access the properties of the variable to apply the NSG:</span></span>

    ```
        $VMinfo = $RecoveryPlanContext.VmMap | Get-Member | Where-Object MemberType -EQ NoteProperty | select -ExpandProperty Name
        $vmMap = $RecoveryPlanContext.VmMap

        foreach($VMID in $VMinfo) {
            Write-output $VMDetailsObj.value.$VMID

            if ($VMDetailsObj.value.$VMID -ne $Null) { #If the VM exists in the context, this will not b Null
                $VM = $vmMap.$VMID
                # Access the properties of the variable
                $NSGname = $VMDetailsObj.value.$VMID.'NSGName'
                $NSGRGname = $VMDetailsObj.value.$VMID.'NSGResourceGroupName'

                # Add code to apply the NSG properties to the VM
            }
        }
    ```

<span data-ttu-id="9f72c-227">È possibile usare lo stesso script per piani di ripristino diversi.</span><span class="sxs-lookup"><span data-stu-id="9f72c-227">You can use the same script for different recovery plans.</span></span> <span data-ttu-id="9f72c-228">Immettere parametri diversi archiviando il valore corrispondente a un piano di ripristino in variabili diverse.</span><span class="sxs-lookup"><span data-stu-id="9f72c-228">Enter different parameters by storing the value that corresponds to a recovery plan in different variables.</span></span>

## <a name="sample-scripts"></a><span data-ttu-id="9f72c-229">Script di esempio</span><span class="sxs-lookup"><span data-stu-id="9f72c-229">Sample scripts</span></span>

<span data-ttu-id="9f72c-230">Per distribuire gli script di esempio nell'account di Automazione, fare clic sul pulsante **Distribuisci in Azure**.</span><span class="sxs-lookup"><span data-stu-id="9f72c-230">To deploy sample scripts to your Automation account, click the **Deploy to Azure** button.</span></span>

<span data-ttu-id="9f72c-231">[![Distribuzione in Azure](https://azurecomcdn.azureedge.net/mediahandler/acomblog/media/Default/blog/c4803408-340e-49e3-9a1f-0ed3f689813d.png)](https://aka.ms/asr-automationrunbooks-deploy)</span><span class="sxs-lookup"><span data-stu-id="9f72c-231">[![Deploy to Azure](https://azurecomcdn.azureedge.net/mediahandler/acomblog/media/Default/blog/c4803408-340e-49e3-9a1f-0ed3f689813d.png)](https://aka.ms/asr-automationrunbooks-deploy)</span></span>

<span data-ttu-id="9f72c-232">Per un altro esempio, vedere il video seguente</span><span class="sxs-lookup"><span data-stu-id="9f72c-232">For another example, see the following video.</span></span> <span data-ttu-id="9f72c-233">che mostra come ripristinare un'applicazione di WordPress a due livelli in Azure:</span><span class="sxs-lookup"><span data-stu-id="9f72c-233">It demonstrates how to recover a two-tier WordPress application to Azure:</span></span>


> [!VIDEO https://channel9.msdn.com/Series/Azure-Site-Recovery/One-click-failover-of-a-2-tier-WordPress-application-using-Azure-Site-Recovery/player]



## <a name="additional-resources"></a><span data-ttu-id="9f72c-234">Risorse aggiuntive</span><span class="sxs-lookup"><span data-stu-id="9f72c-234">Additional resources</span></span>
* [<span data-ttu-id="9f72c-235">Account RunAs per il servizio Automazione di Azure</span><span class="sxs-lookup"><span data-stu-id="9f72c-235">Azure Automation service Run As account</span></span>](../automation/automation-sec-configure-azure-runas-account.md)
* [<span data-ttu-id="9f72c-236">Panoramica di Automazione di Azure</span><span class="sxs-lookup"><span data-stu-id="9f72c-236">Azure Automation overview</span></span>](http://msdn.microsoft.com/library/azure/dn643629.aspx "Panoramica di Automazione di Azure")
* [<span data-ttu-id="9f72c-237">Script di esempio di Automazione di Azure</span><span class="sxs-lookup"><span data-stu-id="9f72c-237">Azure Automation sample scripts</span></span>](http://gallery.technet.microsoft.com/scriptcenter/site/search?f\[0\].Type=User&f\[0\].Value=SC%20Automation%20Product%20Team&f\[0\].Text=SC%20Automation%20Product%20Team "Script di esempio di Automazione di Azure")

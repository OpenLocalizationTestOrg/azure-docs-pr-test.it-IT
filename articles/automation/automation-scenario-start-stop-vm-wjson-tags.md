---
title: stato della macchina virtuale di Azure in formato JSON tag tooschedule aaaUse | Documenti Microsoft
description: In questo articolo viene illustrato come le stringhe di toouse JSON in hello pianificazione tooautomate tag di chiusura e avvio VM.
services: automation
documentationcenter: 
author: MGoedtel
manager: jwhit
editor: tysonn
ms.assetid: 6afed5d2-e939-4749-8b2c-9312b4c16fb2
ms.service: automation
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 01/23/2017
ms.author: magoedte;paulomarquesc
ms.openlocfilehash: f6bbf1dea1c193e5d1010f12f3b1ed63562f9daf
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="azure-automation-scenario-using-json-formatted-tags-toocreate-a-schedule-for-azure-vm-startup-and-shutdown"></a><span data-ttu-id="e7b73-103">Scenario di automazione di Azure: con formato JSON tag toocreate una pianificazione per la macchina virtuale di Azure avvio e arresto</span><span class="sxs-lookup"><span data-stu-id="e7b73-103">Azure Automation scenario: Using JSON-formatted tags toocreate a schedule for Azure VM startup and shutdown</span></span>
<span data-ttu-id="e7b73-104">I clienti desiderano spesso avvio hello tooschedule e arresto di macchine virtuali toohelp ridurre i costi di sottoscrizione o supportare i requisiti aziendali e tecnici.</span><span class="sxs-lookup"><span data-stu-id="e7b73-104">Customers often want tooschedule hello startup and shutdown of virtual machines toohelp reduce subscription costs or support business and technical requirements.</span></span>

<span data-ttu-id="e7b73-105">Hello nello scenario seguente consente di tooset backup automatizzato di avvio e arresto delle macchine virtuali, utilizzando un tag denominato pianificazione a un livello di macchina virtuale in Azure o il livello di gruppo di risorse.</span><span class="sxs-lookup"><span data-stu-id="e7b73-105">hello following scenario enables you tooset up automated startup and shutdown of your VMs by using a tag called Schedule at a resource group level or virtual machine level in Azure.</span></span> <span data-ttu-id="e7b73-106">Questa pianificazione può essere configurata da domenica tooSaturday con un'ora di avvio e arresto.</span><span class="sxs-lookup"><span data-stu-id="e7b73-106">This schedule can be configured from Sunday tooSaturday with a startup time and shutdown time.</span></span>

<span data-ttu-id="e7b73-107">Sono disponibili opzioni predefinite.</span><span class="sxs-lookup"><span data-stu-id="e7b73-107">We do have some out-of-the-box options.</span></span> <span data-ttu-id="e7b73-108">incluse le seguenti:</span><span class="sxs-lookup"><span data-stu-id="e7b73-108">These include:</span></span>

* <span data-ttu-id="e7b73-109">[Set di scalabilità di macchine virtuali](../virtual-machine-scale-sets/virtual-machine-scale-sets-overview.md) con le impostazioni di scalabilità automatica che consentono di tooscale in o out.</span><span class="sxs-lookup"><span data-stu-id="e7b73-109">[Virtual machine scale sets](../virtual-machine-scale-sets/virtual-machine-scale-sets-overview.md) with autoscale settings that enable you tooscale in or out.</span></span>
* <span data-ttu-id="e7b73-110">[DevTest Labs](../devtest-lab/devtest-lab-overview.md) servizio, che dispone di funzionalità predefinite di hello della pianificazione di operazioni di avvio e arresto.</span><span class="sxs-lookup"><span data-stu-id="e7b73-110">[DevTest Labs](../devtest-lab/devtest-lab-overview.md) service, which has hello built-in capability of scheduling startup and shutdown operations.</span></span>

<span data-ttu-id="e7b73-111">Tuttavia, queste opzioni solo supportano scenari specifici e non possono essere macchine virtuali applicato tooinfrastructure-as-a-service (IaaS).</span><span class="sxs-lookup"><span data-stu-id="e7b73-111">However, these options only support specific scenarios and cannot be applied tooinfrastructure-as-a-service (IaaS) VMs.</span></span>

<span data-ttu-id="e7b73-112">Quando hello tag pianificazione è il gruppo di risorse tooa applicato, è inoltre applicato tooall le macchine virtuali all'interno di tale gruppo di risorse.</span><span class="sxs-lookup"><span data-stu-id="e7b73-112">When hello Schedule tag is applied tooa resource group, it's also applied tooall virtual machines inside that resource group.</span></span> <span data-ttu-id="e7b73-113">Se una pianificazione è anche tooa applicato direttamente VM, ultima pianificazione hello ha la precedenza in hello seguente ordine:</span><span class="sxs-lookup"><span data-stu-id="e7b73-113">If a schedule is also directly applied tooa VM, hello last schedule takes precedence in hello following order:</span></span>

1. <span data-ttu-id="e7b73-114">Gruppo di risorse applicata tooa pianificazione</span><span class="sxs-lookup"><span data-stu-id="e7b73-114">Schedule applied tooa resource group</span></span>
2. <span data-ttu-id="e7b73-115">Pianificare il gruppo di risorse tooa applicato e la macchina virtuale nel gruppo di risorse hello</span><span class="sxs-lookup"><span data-stu-id="e7b73-115">Schedule applied tooa resource group and virtual machine in hello resource group</span></span>
3. <span data-ttu-id="e7b73-116">Macchina virtuale di pianificazione applicato tooa</span><span class="sxs-lookup"><span data-stu-id="e7b73-116">Schedule applied tooa virtual machine</span></span>

<span data-ttu-id="e7b73-117">Questo scenario è essenzialmente accetta una stringa JSON con un formato specificato e lo aggiunge come valore di hello per un tag denominato pianificazione.</span><span class="sxs-lookup"><span data-stu-id="e7b73-117">This scenario essentially takes a JSON string with a specified format and adds it as hello value for a tag called Schedule.</span></span> <span data-ttu-id="e7b73-118">Quindi, un runbook sono elencati tutti i gruppi di risorse e le macchine virtuali e identifica le pianificazioni di hello per ogni macchina virtuale in base agli scenari di hello elencati in precedenza.</span><span class="sxs-lookup"><span data-stu-id="e7b73-118">Then a runbook lists all resource groups and virtual machines and identifies hello schedules for each VM based on hello scenarios listed earlier.</span></span> <span data-ttu-id="e7b73-119">Successivamente scorre in ciclo hello macchine virtuali con pianificazioni collegate e restituisce l'azione che deve essere eseguita.</span><span class="sxs-lookup"><span data-stu-id="e7b73-119">Next it loops through hello VMs that have schedules attached and evaluates what action should be taken.</span></span> <span data-ttu-id="e7b73-120">Ad esempio, determina che le macchine virtuali devono toobe arrestato, arrestare o ignorato.</span><span class="sxs-lookup"><span data-stu-id="e7b73-120">For example, it determines which VMs need toobe stopped, shut down, or ignored.</span></span>

<span data-ttu-id="e7b73-121">Questi runbook autenticare con hello [account RunAs di Azure](automation-sec-configure-azure-runas-account.md).</span><span class="sxs-lookup"><span data-stu-id="e7b73-121">These runbooks authenticate by using hello [Azure Run As account](automation-sec-configure-azure-runas-account.md).</span></span>

## <a name="download-hello-runbooks-for-hello-scenario"></a><span data-ttu-id="e7b73-122">Scarica runbook hello per scenario hello</span><span class="sxs-lookup"><span data-stu-id="e7b73-122">Download hello runbooks for hello scenario</span></span>
<span data-ttu-id="e7b73-123">Questo scenario è composto da quattro runbook del flusso di lavoro di PowerShell che è possibile scaricare da hello [Raccolta TechNet](https://gallery.technet.microsoft.com/Azure-Automation-Runbooks-84f0efc7) o hello [GitHub](https://github.com/paulomarquesdacosta/azure-automation-scheduled-shutdown-and-startup) repository per il progetto.</span><span class="sxs-lookup"><span data-stu-id="e7b73-123">This scenario consists of four PowerShell Workflow runbooks that you can download from hello [TechNet Gallery](https://gallery.technet.microsoft.com/Azure-Automation-Runbooks-84f0efc7) or hello [GitHub](https://github.com/paulomarquesdacosta/azure-automation-scheduled-shutdown-and-startup) repository for this project.</span></span>

| <span data-ttu-id="e7b73-124">Runbook</span><span class="sxs-lookup"><span data-stu-id="e7b73-124">Runbook</span></span> | <span data-ttu-id="e7b73-125">Descrizione</span><span class="sxs-lookup"><span data-stu-id="e7b73-125">Description</span></span> |
| --- | --- |
| <span data-ttu-id="e7b73-126">Test-ResourceSchedule</span><span class="sxs-lookup"><span data-stu-id="e7b73-126">Test-ResourceSchedule</span></span> |<span data-ttu-id="e7b73-127">Controlla pianificazione ogni macchina virtuale ed esegue l'arresto o l'avvio a seconda della pianificazione hello.</span><span class="sxs-lookup"><span data-stu-id="e7b73-127">Checks each virtual machine schedule and performs shutdown or startup depending on hello schedule.</span></span> |
| <span data-ttu-id="e7b73-128">Add-ResourceSchedule</span><span class="sxs-lookup"><span data-stu-id="e7b73-128">Add-ResourceSchedule</span></span> |<span data-ttu-id="e7b73-129">Aggiunge hello tag tooa VM o una risorsa gruppo di pianificazione.</span><span class="sxs-lookup"><span data-stu-id="e7b73-129">Adds hello Schedule tag tooa VM or resource group.</span></span> |
| <span data-ttu-id="e7b73-130">Update-ResourceSchedule</span><span class="sxs-lookup"><span data-stu-id="e7b73-130">Update-ResourceSchedule</span></span> |<span data-ttu-id="e7b73-131">Modifica tag pianificazione esistente hello sostituendolo con uno nuovo.</span><span class="sxs-lookup"><span data-stu-id="e7b73-131">Modifies hello existing Schedule tag by replacing it with a new one.</span></span> |
| <span data-ttu-id="e7b73-132">Remove-ResourceSchedule</span><span class="sxs-lookup"><span data-stu-id="e7b73-132">Remove-ResourceSchedule</span></span> |<span data-ttu-id="e7b73-133">Rimuove i tag di pianificazione hello da un macchina virtuale, un gruppo di risorse.</span><span class="sxs-lookup"><span data-stu-id="e7b73-133">Removes hello Schedule tag from a VM or resource group.</span></span> |

## <a name="install-and-configure-this-scenario"></a><span data-ttu-id="e7b73-134">Installare e configurare lo scenario</span><span class="sxs-lookup"><span data-stu-id="e7b73-134">Install and configure this scenario</span></span>
### <a name="install-and-publish-hello-runbooks"></a><span data-ttu-id="e7b73-135">Installare e pubblicare i runbook hello</span><span class="sxs-lookup"><span data-stu-id="e7b73-135">Install and publish hello runbooks</span></span>
<span data-ttu-id="e7b73-136">Dopo aver scaricato hello runbook, è possibile importarli usando la procedura hello in [creazione o importazione di un runbook in automazione di Azure](automation-creating-importing-runbook.md#importing-a-runbook-from-a-file-into-azure-automation).</span><span class="sxs-lookup"><span data-stu-id="e7b73-136">After downloading hello runbooks, you can import them by using hello procedure in [Creating or importing a runbook in Azure Automation](automation-creating-importing-runbook.md#importing-a-runbook-from-a-file-into-azure-automation).</span></span>  <span data-ttu-id="e7b73-137">Pubblicare ogni runbook dopo averlo importato correttamente nell'account di automazione.</span><span class="sxs-lookup"><span data-stu-id="e7b73-137">Publish each runbook after it has been successfully imported into your Automation account.</span></span>

### <a name="add-a-schedule-toohello-test-resourceschedule-runbook"></a><span data-ttu-id="e7b73-138">Aggiungere un runbook toohello ResourceSchedule di Test di pianificazione</span><span class="sxs-lookup"><span data-stu-id="e7b73-138">Add a schedule toohello Test-ResourceSchedule runbook</span></span>
<span data-ttu-id="e7b73-139">Attenersi alla pianificazione di hello tooenable questi passaggi per hello ResourceSchedule di Test runbook.</span><span class="sxs-lookup"><span data-stu-id="e7b73-139">Follow these steps tooenable hello schedule for hello Test-ResourceSchedule runbook.</span></span> <span data-ttu-id="e7b73-140">Si tratta runbook hello che verifica le macchine virtuali che deve essere avviate, arrestata, o lasciati inalterati.</span><span class="sxs-lookup"><span data-stu-id="e7b73-140">This is hello runbook that verifies which virtual machines should be started, shut down, or left as is.</span></span>

1. <span data-ttu-id="e7b73-141">Dal portale di Azure hello, aprire l'account di automazione e quindi fare clic su hello **runbook** riquadro.</span><span class="sxs-lookup"><span data-stu-id="e7b73-141">From hello Azure portal, open your Automation account, and then click hello **Runbooks** tile.</span></span>
2. <span data-ttu-id="e7b73-142">In hello **Test ResourceSchedule** pannello, fare clic su hello **pianificazioni** riquadro.</span><span class="sxs-lookup"><span data-stu-id="e7b73-142">On hello **Test-ResourceSchedule** blade, click hello **Schedules** tile.</span></span>
3. <span data-ttu-id="e7b73-143">In hello **pianificazioni** pannello, fare clic su **aggiungere una pianificazione**.</span><span class="sxs-lookup"><span data-stu-id="e7b73-143">On hello **Schedules** blade, click **Add a schedule**.</span></span>
4. <span data-ttu-id="e7b73-144">In hello **pianificazioni** pannello seleziona **collega un runbook tooyour pianificazione**.</span><span class="sxs-lookup"><span data-stu-id="e7b73-144">On hello **Schedules** blade, select **Link a schedule tooyour runbook**.</span></span> <span data-ttu-id="e7b73-145">Selezionare quindi **Crea una nuova pianificazione**.</span><span class="sxs-lookup"><span data-stu-id="e7b73-145">Then select **Create a new schedule**.</span></span>
5. <span data-ttu-id="e7b73-146">In hello **nuova pianificazione** pannello, digitare il nome di hello della pianificazione, ad esempio: *HourlyExecution*.</span><span class="sxs-lookup"><span data-stu-id="e7b73-146">On hello **New schedule** blade, type in hello name of this schedule, for example: *HourlyExecution*.</span></span>
6. <span data-ttu-id="e7b73-147">Per la pianificazione di hello **avviare**, impostare hello inizio tooan ora tempo.</span><span class="sxs-lookup"><span data-stu-id="e7b73-147">For hello schedule **Start**, set hello start time tooan hour increment.</span></span>
7. <span data-ttu-id="e7b73-148">Selezionare **Ricorrenza** e quindi in **Ricorre ogni** (intervallo) selezionare **1 ora**.</span><span class="sxs-lookup"><span data-stu-id="e7b73-148">Select **Recurrence**, and then for **Recur every interval**, select **1 hour**.</span></span>
8. <span data-ttu-id="e7b73-149">Verificare che **scadenza Set di** è troppo**n**, quindi fare clic su **crea** toosave la nuova pianificazione.</span><span class="sxs-lookup"><span data-stu-id="e7b73-149">Verify that **Set expiration** is set too**No**, and then click **Create** toosave your new schedule.</span></span>
9. <span data-ttu-id="e7b73-150">In hello **pianificazione Runbook** Pannello opzioni, seleziona **parametri e le impostazioni di esecuzione**.</span><span class="sxs-lookup"><span data-stu-id="e7b73-150">On hello **Schedule Runbook** options blade, select **Parameters and run settings**.</span></span> <span data-ttu-id="e7b73-151">In hello Test ResourceSchedule **parametri** pannello, immettere il nome di hello della sottoscrizione in hello **SubscriptionName** campo.</span><span class="sxs-lookup"><span data-stu-id="e7b73-151">In hello Test-ResourceSchedule **Parameters** blade, enter hello name of your subscription in hello **SubscriptionName** field.</span></span>  <span data-ttu-id="e7b73-152">Questo parametro solo hello che ha richiesto per il runbook hello è.</span><span class="sxs-lookup"><span data-stu-id="e7b73-152">This is hello only parameter that's required for hello runbook.</span></span>  <span data-ttu-id="e7b73-153">Al termine, fare clic su **OK**.</span><span class="sxs-lookup"><span data-stu-id="e7b73-153">When you're finished, click **OK**.</span></span>

<span data-ttu-id="e7b73-154">pianificazione del runbook Hello dovrebbe essere simile hello seguente completata:</span><span class="sxs-lookup"><span data-stu-id="e7b73-154">hello runbook schedule should look like hello following when it's completed:</span></span>

![Runbook Test-ResourceSchedule configurato](./media/automation-scenario-start-stop-vm-wjson-tags/automation-schedule-config.png)<br>

## <a name="format-hello-json-string"></a><span data-ttu-id="e7b73-156">Hello formato stringa JSON</span><span class="sxs-lookup"><span data-stu-id="e7b73-156">Format hello JSON string</span></span>
<span data-ttu-id="e7b73-157">Questa soluzione fondamentalmente ha un formato JSON di stringhe con un formato specificato e lo aggiunge come valore di hello per un tag chiamato pianificazione.</span><span class="sxs-lookup"><span data-stu-id="e7b73-157">This solution basically takes a JSON string with a specified format and adds it as hello value for a tag called Schedule.</span></span> <span data-ttu-id="e7b73-158">Quindi, un runbook sono elencati tutti i gruppi di risorse e le macchine virtuali e identifica le pianificazioni di hello per ogni macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="e7b73-158">Then a runbook lists all resource groups and virtual machines and identifies hello schedules for each virtual machine.</span></span>

<span data-ttu-id="e7b73-159">runbook Hello esaminati hello macchine che dispongono di pianificazioni collegate e controlla quali operazioni devono essere eseguite.</span><span class="sxs-lookup"><span data-stu-id="e7b73-159">hello runbook loops over hello virtual machines that have schedules attached and checks what actions should be taken.</span></span> <span data-ttu-id="e7b73-160">Hello Ecco un esempio di modalità di formattazione delle soluzioni di hello:</span><span class="sxs-lookup"><span data-stu-id="e7b73-160">hello following is an example of how hello solutions should be formatted:</span></span>

```json
{
    "TzId": "Eastern Standard Time",
    "0": {
        "S": "11",
        "E": "17"
    },
    "1": {
        "S": "9",
        "E": "19"
    },
    "2": {
        "S": "9",
        "E": "19"
    },
}
```

<span data-ttu-id="e7b73-161">Ecco alcune informazioni dettagliate su questa struttura:</span><span class="sxs-lookup"><span data-stu-id="e7b73-161">Here is some detailed information about this structure:</span></span>

1. <span data-ttu-id="e7b73-162">formato di Hello di questa struttura JSON è ottimizzato toowork intorno al limite di 256 caratteri hello di un valore singolo tag in Azure.</span><span class="sxs-lookup"><span data-stu-id="e7b73-162">hello format of this JSON structure is optimized toowork around hello 256-character limitation of a single tag value in Azure.</span></span>
2. <span data-ttu-id="e7b73-163">*TzId* rappresenta hello fuso orario della macchina virtuale hello.</span><span class="sxs-lookup"><span data-stu-id="e7b73-163">*TzId* represents hello time zone of hello virtual machine.</span></span> <span data-ttu-id="e7b73-164">Questo ID può essere ottenuto utilizzando classe TimeZoneInfo .NET hello in una sessione di PowerShell -**[System.TimeZoneInfo]:: GetSystemTimeZones()**.</span><span class="sxs-lookup"><span data-stu-id="e7b73-164">This ID can be obtained by using hello TimeZoneInfo .NET class in a PowerShell session--**[System.TimeZoneInfo]::GetSystemTimeZones()**.</span></span>

   ![GetSystemTimeZones in PowerShell](./media/automation-scenario-start-stop-vm-wjson-tags/automation-get-timzone-powershell.png)

   * <span data-ttu-id="e7b73-166">Giorni della settimana sono rappresentati con un valore numerico pari a zero toosix.</span><span class="sxs-lookup"><span data-stu-id="e7b73-166">Weekdays are represented with a numeric value of zero toosix.</span></span> <span data-ttu-id="e7b73-167">il valore di Hello zero è uguale a domenica.</span><span class="sxs-lookup"><span data-stu-id="e7b73-167">hello value zero equals Sunday.</span></span>
   * <span data-ttu-id="e7b73-168">Hello ora di inizio è rappresentato dalla hello **S** attributo e il relativo valore è nel formato 24 ore.</span><span class="sxs-lookup"><span data-stu-id="e7b73-168">hello start time is represented with hello **S** attribute, and its value is in a 24-hour format.</span></span>
   * <span data-ttu-id="e7b73-169">Hello ora di fine o l'arresto è rappresentato dalla hello **E** attributo e il relativo valore è nel formato 24 ore.</span><span class="sxs-lookup"><span data-stu-id="e7b73-169">hello end or shutdown time is represented with hello **E** attribute, and its value is in a 24-hour format.</span></span>

     <span data-ttu-id="e7b73-170">Se hello **S** e **E** ogni attributo dispone di un valore pari a zero (0), macchina virtuale hello rimarrà nello stato attuale in fase di valutazione di hello.</span><span class="sxs-lookup"><span data-stu-id="e7b73-170">If hello **S** and **E** attributes each have a value of zero (0), hello virtual machine will be left in its present state at hello time of evaluation.</span></span>
3. <span data-ttu-id="e7b73-171">Se si desidera tooskip valutazione per un giorno specifico della settimana hello, non aggiungere una sezione per tale giorno della settimana hello.</span><span class="sxs-lookup"><span data-stu-id="e7b73-171">If you want tooskip evaluation for a specific day of hello week, don’t add a section for that day of hello week.</span></span> <span data-ttu-id="e7b73-172">In hello seguente esempio, solo lunedì viene valutata e hello altri giorni della settimana hello vengono ignorati:</span><span class="sxs-lookup"><span data-stu-id="e7b73-172">In hello following example, only Monday is evaluated, and hello other days of hello week are ignored:</span></span>

    ```json
    {
        "TzId": "Eastern Standard Time",
        "1": {
            "S": "11",
            "E": "17"
        }
    }
    ```

## <a name="tag-resource-groups-or-vms"></a><span data-ttu-id="e7b73-173">Aggiungere tag a gruppi di risorse o macchine virtuali</span><span class="sxs-lookup"><span data-stu-id="e7b73-173">Tag resource groups or VMs</span></span>
<span data-ttu-id="e7b73-174">tooshut verso il basso le macchine virtuali, è necessario tootag macchine virtuali hello o gruppi di risorse hello in cui si trovano.</span><span class="sxs-lookup"><span data-stu-id="e7b73-174">tooshut down VMs, you need tootag either hello VMs or hello resource groups in which they're located.</span></span> <span data-ttu-id="e7b73-175">Le macchine virtuali che non hanno un tag Schedule non vengono valutate.</span><span class="sxs-lookup"><span data-stu-id="e7b73-175">Virtual machines that don't have a Schedule tag are not evaluated.</span></span> <span data-ttu-id="e7b73-176">Di conseguenza, non vengono avviate né arrestate.</span><span class="sxs-lookup"><span data-stu-id="e7b73-176">Therefore, they aren't started or shut down.</span></span>

<span data-ttu-id="e7b73-177">Esistono due macchine virtuali o i gruppi di risorse tootag modi con questa soluzione.</span><span class="sxs-lookup"><span data-stu-id="e7b73-177">There are two ways tootag resource groups or VMs with this solution.</span></span> <span data-ttu-id="e7b73-178">È possibile farlo direttamente dal portale hello.</span><span class="sxs-lookup"><span data-stu-id="e7b73-178">You can do it directly from hello portal.</span></span> <span data-ttu-id="e7b73-179">È possibile utilizzare hello Aggiungi ResourceSchedule aggiornamento ResourceSchedule e Remove-ResourceSchedule runbook.</span><span class="sxs-lookup"><span data-stu-id="e7b73-179">Or you can use hello Add-ResourceSchedule, Update-ResourceSchedule, and Remove-ResourceSchedule runbooks.</span></span>

### <a name="tag-through-hello-portal"></a><span data-ttu-id="e7b73-180">Tag tramite il portale di hello</span><span class="sxs-lookup"><span data-stu-id="e7b73-180">Tag through hello portal</span></span>
<span data-ttu-id="e7b73-181">Seguire questi passaggi tootag una macchina virtuale o un gruppo di risorse nel portale di hello:</span><span class="sxs-lookup"><span data-stu-id="e7b73-181">Follow these steps tootag a virtual machine or resource group in hello portal:</span></span>

1. <span data-ttu-id="e7b73-182">Convertire una stringa JSON hello e verificare che non vi siano spazi.</span><span class="sxs-lookup"><span data-stu-id="e7b73-182">Flatten hello JSON string and verify that there aren't any spaces.</span></span>  <span data-ttu-id="e7b73-183">La stringa JSON dovrebbe avere un aspetto simile al seguente:</span><span class="sxs-lookup"><span data-stu-id="e7b73-183">Your JSON string should look like this:</span></span>

    ```json
    {"TzId":"Eastern Standard Time","0":{"S":"11","E":"17"},"1":{"S":"9","E":"19"},"2": {"S":"9","E":"19"},"3":{"S":"9","E":"19"},"4":{"S":"9","E":"19"},"5":{"S":"9","E":"19"},"6":{"S":"11","E":"17"}}
    ```

2. <span data-ttu-id="e7b73-184">Seleziona hello **Tag** icona per una macchina virtuale o di una risorsa gruppo tooapply questa pianificazione.</span><span class="sxs-lookup"><span data-stu-id="e7b73-184">Select hello **Tag** icon for a VM or resource group tooapply this schedule.</span></span>

   ![Opzione per i tag delle VM](./media/automation-scenario-start-stop-vm-wjson-tags/automation-vm-tag-option.png)

3. <span data-ttu-id="e7b73-186">I tag vengono definiti in base a una coppia chiave/valore.</span><span class="sxs-lookup"><span data-stu-id="e7b73-186">Tags are defined following a key/value pair.</span></span> <span data-ttu-id="e7b73-187">Tipo **pianificazione** in hello **chiave** campo e quindi incollare stringa JSON hello hello **valore** campo.</span><span class="sxs-lookup"><span data-stu-id="e7b73-187">Type **Schedule** in hello **Key** field, and then paste hello JSON string into hello **Value** field.</span></span> <span data-ttu-id="e7b73-188">Fare clic su **Salva**.</span><span class="sxs-lookup"><span data-stu-id="e7b73-188">Click **Save**.</span></span> <span data-ttu-id="e7b73-189">Il nuovo tag verrà ora visualizzato nell'elenco di hello di tag per la risorsa.</span><span class="sxs-lookup"><span data-stu-id="e7b73-189">Your new tag should now appear in hello list of tags for your resource.</span></span>

   ![Tag di pianificazione delle VM](./media/automation-scenario-start-stop-vm-wjson-tags/automation-vm-schedule-tag.png)

### <a name="tag-from-powershell"></a><span data-ttu-id="e7b73-191">Aggiungere tag da PowerShell</span><span class="sxs-lookup"><span data-stu-id="e7b73-191">Tag from PowerShell</span></span>
<span data-ttu-id="e7b73-192">Tutti i runbook importati contengono le informazioni della Guida all'inizio di hello dello script hello che descrive la modalità tooexecute hello runbook direttamente da PowerShell.</span><span class="sxs-lookup"><span data-stu-id="e7b73-192">All imported runbooks contain help information at hello beginning of hello script that describes how tooexecute hello runbooks directly from PowerShell.</span></span> <span data-ttu-id="e7b73-193">È possibile chiamare i runbook Aggiungi ScheduleResource e aggiornamento ScheduleResource hello da PowerShell.</span><span class="sxs-lookup"><span data-stu-id="e7b73-193">You can call hello Add-ScheduleResource and Update-ScheduleResource runbooks from PowerShell.</span></span> <span data-ttu-id="e7b73-194">Questo caso passando i parametri necessari che consentono di tag di pianificazione di hello toocreate o update in un gruppo di macchina virtuale o una risorsa all'esterno di portale hello.</span><span class="sxs-lookup"><span data-stu-id="e7b73-194">You do this by passing required parameters that enable you toocreate or update hello Schedule tag on a VM or resource group outside of hello portal.</span></span>

<span data-ttu-id="e7b73-195">toocreate, aggiungere ed eliminare i tag mediante PowerShell, è innanzitutto necessario troppo[configurare l'ambiente di PowerShell per Azure](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="e7b73-195">toocreate, add, and delete tags through PowerShell, you first need too[set up your PowerShell environment for Azure](/powershell/azure/overview).</span></span> <span data-ttu-id="e7b73-196">Dopo aver completato l'installazione di hello, è possibile procedere con hello alla procedura seguente.</span><span class="sxs-lookup"><span data-stu-id="e7b73-196">After you complete hello setup, you can proceed with hello following steps.</span></span>

### <a name="create-a-schedule-tag-with-powershell"></a><span data-ttu-id="e7b73-197">Creare un tag di pianificazione con PowerShell</span><span class="sxs-lookup"><span data-stu-id="e7b73-197">Create a schedule tag with PowerShell</span></span>
1. <span data-ttu-id="e7b73-198">Aprire una sessione di PowerShell.</span><span class="sxs-lookup"><span data-stu-id="e7b73-198">Open a PowerShell session.</span></span> <span data-ttu-id="e7b73-199">Utilizzare quindi hello tooauthenticate di esempio con l'account RunAs e toospecify una sottoscrizione di seguito:</span><span class="sxs-lookup"><span data-stu-id="e7b73-199">Then use hello following example tooauthenticate with your Run As account and toospecify a subscription:</span></span>

    ```powershell
    $Conn = Get-AutomationConnection -Name AzureRunAsConnection
    Add-AzureRMAccount -ServicePrincipal -Tenant $Conn.TenantID `
    -ApplicationId $Conn.ApplicationID -CertificateThumbprint $Conn.CertificateThumbprint
    Select-AzureRmSubscription -SubscriptionName "MySubscription"
    ```

2. <span data-ttu-id="e7b73-200">Definire una tabella hash di pianificazione.</span><span class="sxs-lookup"><span data-stu-id="e7b73-200">Define a schedule hash table.</span></span> <span data-ttu-id="e7b73-201">Di seguito è riportato un esempio di come dovrebbe essere costruita:</span><span class="sxs-lookup"><span data-stu-id="e7b73-201">Here is an example of how it should be constructed:</span></span>

    ```powershell
    $schedule= @{ "TzId"="Eastern Standard Time"; "0"= @{"S"="11";"E"="17"};"1"= @{"S"="9";"E"="19"};"2"= @{"S"="9";"E"="19"};"3"= @{"S"="9";"E"="19"};"4"= @{"S"="9";"E"="19"};"5"= @{"S"="9";"E"="19"};"6"= @{"S"="11";"E"="17"}}
    ```

3. <span data-ttu-id="e7b73-202">Definire i parametri di hello richiesti dal runbook hello.</span><span class="sxs-lookup"><span data-stu-id="e7b73-202">Define hello parameters that are required by hello runbook.</span></span> <span data-ttu-id="e7b73-203">Nell'esempio seguente di hello, destinazione interessato una macchina virtuale:</span><span class="sxs-lookup"><span data-stu-id="e7b73-203">In hello following example, we are targeting a VM:</span></span>

    ```powershell
    $params = @{"SubscriptionName"="MySubscription";"ResourceGroupName"="ResourceGroup01"; "VmName"="VM01";"Schedule"=$schedule}
    ```

    <span data-ttu-id="e7b73-204">Se si sta tag a un gruppo di risorse, rimuovere hello *VMName* parametro dall'hash hello $params tabella come segue:</span><span class="sxs-lookup"><span data-stu-id="e7b73-204">If you’re tagging a resource group, remove hello *VMName* parameter from hello $params hash table as follows:</span></span>

    ```powershell
    $params = @{"SubscriptionName"="MySubscription";"ResourceGroupName"="ResourceGroup01"; "Schedule"=$schedule}
    ```

4. <span data-ttu-id="e7b73-205">Eseguire runbook hello Aggiungi ResourceSchedule con hello successivo tag di pianificazione hello toocreate parametri:</span><span class="sxs-lookup"><span data-stu-id="e7b73-205">Run hello Add-ResourceSchedule runbook with hello following parameters toocreate hello Schedule tag:</span></span>

    ```powershell
    Start-AzureRmAutomationRunbook -Name "Add-ResourceSchedule" -Parameters $params `
    -AutomationAccountName "AutomationAccount" -ResourceGroupName "ResourceGroup01"
    ```

5. <span data-ttu-id="e7b73-206">tooupdate un tag delle risorse gruppo o una macchina virtuale, eseguire hello **aggiornamento ResourceSchedule** runbook con hello seguenti parametri:</span><span class="sxs-lookup"><span data-stu-id="e7b73-206">tooupdate a resource group or virtual machine tag, execute hello **Update-ResourceSchedule** runbook with hello following parameters:</span></span>

    ```powershell
    Start-AzureRmAutomationRunbook -Name "Update-ResourceSchedule" -Parameters $params `
    -AutomationAccountName "AutomationAccount" -ResourceGroupName "ResourceGroup01"
    ```

### <a name="remove-a-schedule-tag-with-powershell"></a><span data-ttu-id="e7b73-207">Rimuovere un tag di pianificazione con PowerShell</span><span class="sxs-lookup"><span data-stu-id="e7b73-207">Remove a schedule tag with PowerShell</span></span>
1. <span data-ttu-id="e7b73-208">Aprire una sessione di PowerShell eseguire hello seguente tooauthenticate con l'account RunAs e tooselect e specificare una sottoscrizione:</span><span class="sxs-lookup"><span data-stu-id="e7b73-208">Open a PowerShell session and run hello following tooauthenticate with your Run As account and tooselect and specify a subscription:</span></span>

    ```powershell
    Conn = Get-AutomationConnection -Name AzureRunAsConnection
    Add-AzureRMAccount -ServicePrincipal -Tenant $Conn.TenantID `
    -ApplicationId $Conn.ApplicationID -CertificateThumbprint $Conn.CertificateThumbprint
    Select-AzureRmSubscription -SubscriptionName "MySubscription"
    ```

2. <span data-ttu-id="e7b73-209">Definire i parametri di hello richiesti dal runbook hello.</span><span class="sxs-lookup"><span data-stu-id="e7b73-209">Define hello parameters that are required by hello runbook.</span></span> <span data-ttu-id="e7b73-210">Nell'esempio seguente di hello, destinazione interessato una macchina virtuale:</span><span class="sxs-lookup"><span data-stu-id="e7b73-210">In hello following example, we are targeting a VM:</span></span>

    ```powershell
    $params = @{"SubscriptionName"="MySubscription";"ResourceGroupName"="ResourceGroup01";"VmName"="VM01"}
    ```

    <span data-ttu-id="e7b73-211">Se si elimina un tag da un gruppo di risorse, rimuovere hello *VMName* parametro dall'hash hello $params tabella come segue:</span><span class="sxs-lookup"><span data-stu-id="e7b73-211">If you’re removing a tag from a resource group, remove hello *VMName* parameter from hello $params hash table as follows:</span></span>

    ```powershell
    $params = @{"SubscriptionName"="MySubscription";"ResourceGroupName"="ResourceGroup01"}
    ```

3. <span data-ttu-id="e7b73-212">Eseguire i tag di hello Remove ResourceSchedule runbook tooremove hello pianificazione:</span><span class="sxs-lookup"><span data-stu-id="e7b73-212">Execute hello Remove-ResourceSchedule runbook tooremove hello Schedule tag:</span></span>

    ```powershell
    Start-AzureRmAutomationRunbook -Name "Remove-ResourceSchedule" -Parameters $params `
    -AutomationAccountName "AutomationAccount" -ResourceGroupName "ResourceGroup01"
    ```

4. <span data-ttu-id="e7b73-213">tooupdate un tag delle risorse gruppo o una macchina virtuale, eseguire Remove-ResourceSchedule hello runbook con hello seguenti parametri:</span><span class="sxs-lookup"><span data-stu-id="e7b73-213">tooupdate a resource group or virtual machine tag, execute hello Remove-ResourceSchedule runbook with hello following parameters:</span></span>

    ```powershell
    Start-AzureRmAutomationRunbook -Name "Remove-ResourceSchedule" -Parameters $params `
    -AutomationAccountName "AutomationAccount" -ResourceGroupName "ResourceGroup01"
    ```

> [!NOTE]
> <span data-ttu-id="e7b73-214">È consigliabile monitorare in modo proattivo questi runbook (e degli stati della macchina virtuale hello) tooverify che le macchine virtuali vengono arrestato e avviato di conseguenza.</span><span class="sxs-lookup"><span data-stu-id="e7b73-214">We recommend that you proactively monitor these runbooks (and hello virtual machine states) tooverify that your virtual machines are being shut down and started accordingly.</span></span>
>

<span data-ttu-id="e7b73-215">dettagli di hello tooview di runbook hello Test ResourceSchedule processo portale di Azure seleziona hello hello **processi** tessera di hello runbook.</span><span class="sxs-lookup"><span data-stu-id="e7b73-215">tooview hello details of hello Test-ResourceSchedule runbook job in hello Azure portal, select hello **Jobs** tile of hello runbook.</span></span> <span data-ttu-id="e7b73-216">Hello processo Visualizza riepilogo hello i parametri di input e output di hello flussi, inoltre toogeneral informazioni processo hello e alle eventuali eccezioni se si sono verificate.</span><span class="sxs-lookup"><span data-stu-id="e7b73-216">hello job summary displays hello input parameters and hello output stream, in addition toogeneral information about hello job and any exceptions if they occurred.</span></span>

<span data-ttu-id="e7b73-217">Hello **riepilogo** include i messaggi da flussi di errore, avviso e di output di hello.</span><span class="sxs-lookup"><span data-stu-id="e7b73-217">hello **Job Summary** includes messages from hello output, warning, and error streams.</span></span> <span data-ttu-id="e7b73-218">Seleziona hello **Output** tooview riquadro risultati dell'esecuzione di runbook hello dettagliati.</span><span class="sxs-lookup"><span data-stu-id="e7b73-218">Select hello **Output** tile tooview detailed results from hello runbook execution.</span></span>

![Output di Test-ResourceSchedule](./media/automation-scenario-start-stop-vm-wjson-tags/automation-job-output.png)

## <a name="next-steps"></a><span data-ttu-id="e7b73-220">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="e7b73-220">Next steps</span></span>
* <span data-ttu-id="e7b73-221">tooget avviato con runbook del flusso di lavoro di PowerShell, vedere [il primo runbook del flusso di lavoro PowerShell](automation-first-runbook-textual.md).</span><span class="sxs-lookup"><span data-stu-id="e7b73-221">tooget started with PowerShell workflow runbooks, see [My first PowerShell workflow runbook](automation-first-runbook-textual.md).</span></span>
* <span data-ttu-id="e7b73-222">toolearn ulteriori informazioni sui tipi di runbook e i relativi vantaggi e limitazioni, vedere [tipi di runbook di automazione di Azure](automation-runbook-types.md).</span><span class="sxs-lookup"><span data-stu-id="e7b73-222">toolearn more about runbook types, and their advantages and limitations, see [Azure Automation runbook types](automation-runbook-types.md).</span></span>
* <span data-ttu-id="e7b73-223">Per altre informazioni sulla funzionalità di supporto degli script PowerShell, vedere il blog relativo al [Announcing Native PowerShell Script Support in Azure Automation](https://azure.microsoft.com/blog/announcing-powershell-script-support-azure-automation-2/)(Supporto di script PowerShell nativi in Automazione di Azure).</span><span class="sxs-lookup"><span data-stu-id="e7b73-223">For more information about PowerShell script support features, see [Native PowerShell script support in Azure Automation](https://azure.microsoft.com/blog/announcing-powershell-script-support-azure-automation-2/).</span></span>
* <span data-ttu-id="e7b73-224">toolearn ulteriori informazioni su registrazione runbook e l'output, vedere [Runbook in automazione di Azure messaggi e output](automation-runbook-output-and-messages.md).</span><span class="sxs-lookup"><span data-stu-id="e7b73-224">toolearn more about runbook logging and output, see [Runbook output and messages in Azure Automation](automation-runbook-output-and-messages.md).</span></span>
* <span data-ttu-id="e7b73-225">informazioni su un account RunAs di Azure e come tooauthenticate runbook con questo nuovo modello, vedere toolearn [autenticare runbook con l'account RunAs di Azure](automation-sec-configure-azure-runas-account.md).</span><span class="sxs-lookup"><span data-stu-id="e7b73-225">toolearn more about an Azure Run As account and how tooauthenticate your runbooks by using it, see [Authenticate runbooks with Azure Run As account](automation-sec-configure-azure-runas-account.md).</span></span>

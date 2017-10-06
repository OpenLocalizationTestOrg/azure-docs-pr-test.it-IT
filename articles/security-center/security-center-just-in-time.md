---
title: aaaJust nella macchina virtuale ora accedere nel Centro protezione di Azure | Documenti Microsoft
description: "Questo documento illustra la modalità in-time VM in consente di Centro protezione Azure controllare accedere tooyour Azure le macchine virtuali."
services: security-center
documentationcenter: na
author: TerryLanfear
manager: MBaldwin
editor: 
ms.assetid: 
ms.service: security-center
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/08/2017
ms.author: terrylan
ms.openlocfilehash: e6b58dd2c686cb227392b294e85914df5a546016
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="manage-virtual-machine-access-using-just-in-time"></a><span data-ttu-id="be42e-103">Gestire l'accesso alle macchine virtuali con la funzionalità JIT (Just-in-Time)</span><span class="sxs-lookup"><span data-stu-id="be42e-103">Manage virtual machine access using just in time</span></span>

<span data-ttu-id="be42e-104">Solo nella macchina virtuale ora (VM) accesso può essere utilizzato toolock verso il basso il traffico in entrata tooyour macchine virtuali di Azure, riducendo l'esposizione tooattacks fornendo un accesso semplice tooconnect tooVMs quando necessario.</span><span class="sxs-lookup"><span data-stu-id="be42e-104">Just in time virtual machine (VM) access can be used toolock down inbound traffic tooyour Azure VMs, reducing exposure tooattacks while providing easy access tooconnect tooVMs when needed.</span></span>

> [!NOTE]
> <span data-ttu-id="be42e-105">Hello solo nella funzione di tempo è in anteprima e disponibile nel livello Standard del Centro sicurezza PC hello.</span><span class="sxs-lookup"><span data-stu-id="be42e-105">hello just in time feature is in preview and available on hello Standard tier of Security Center.</span></span>  <span data-ttu-id="be42e-106">Vedere [prezzi](security-center-pricing.md) toolearn ulteriori informazioni su Centro sicurezza di livelli di prezzo.</span><span class="sxs-lookup"><span data-stu-id="be42e-106">See [Pricing](security-center-pricing.md) toolearn more about Security Center's pricing tiers.</span></span>
>
>

## <a name="attack-scenario"></a><span data-ttu-id="be42e-107">Scenario di attacco</span><span class="sxs-lookup"><span data-stu-id="be42e-107">Attack scenario</span></span>

<span data-ttu-id="be42e-108">Attacchi di forza bruta attacchi comunemente porte di gestione di destinazione come un tooa di accesso toogain significa macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="be42e-108">Brute force attacks commonly target management ports as a means toogain access tooa VM.</span></span> <span data-ttu-id="be42e-109">Se ha esito positivo, un utente malintenzionato può assumere il controllo hello VM e stabilire un mercato nel proprio ambiente.</span><span class="sxs-lookup"><span data-stu-id="be42e-109">If successful, an attacker can take control over hello VM and establish a foothold into your environment.</span></span>

<span data-ttu-id="be42e-110">Attacco di forza bruta tooa esposizione tooreduce unidirezionale è toolimit hello periodo di tempo che una porta è aperta.</span><span class="sxs-lookup"><span data-stu-id="be42e-110">One way tooreduce exposure tooa brute force attack is toolimit hello amount of time that a port is open.</span></span> <span data-ttu-id="be42e-111">Porte di gestione eseguire non è necessario toobe aprire in qualsiasi momento.</span><span class="sxs-lookup"><span data-stu-id="be42e-111">Management ports do not need toobe open at all times.</span></span> <span data-ttu-id="be42e-112">È necessario toobe aprire mentre si toohello connesso macchina virtuale, ad esempio tooperform di sono attività di gestione o manutenzione.</span><span class="sxs-lookup"><span data-stu-id="be42e-112">They only need toobe open while you are connected toohello VM, for example tooperform management or maintenance tasks.</span></span> <span data-ttu-id="be42e-113">Quando è abilitata in-time, viene utilizzato il Centro sicurezza PC [Network Security Group](../virtual-network/virtual-networks-nsg.md) regole (gruppo), che limitano l'accesso a porte toomanagement in modo che non possono essere assegnati da utenti malintenzionati.</span><span class="sxs-lookup"><span data-stu-id="be42e-113">When just in time is enabled, Security Center uses [Network Security Group](../virtual-network/virtual-networks-nsg.md) (NSG) rules, which restrict access toomanagement ports so they cannot be targeted by attackers.</span></span>

![Scenario Just-in-Time][1]

## <a name="how-does-just-in-time-access-work"></a><span data-ttu-id="be42e-115">Come funziona l'accesso Just-in-Time?</span><span class="sxs-lookup"><span data-stu-id="be42e-115">How does just in time access work?</span></span>

<span data-ttu-id="be42e-116">Quando è abilitata in-time, il Centro sicurezza PC protegge il traffico in entrata tooyour macchine virtuali di Azure tramite la creazione di una regola di gruppo.</span><span class="sxs-lookup"><span data-stu-id="be42e-116">When just in time is enabled, Security Center locks down inbound traffic tooyour Azure VMs by creating an NSG rule.</span></span> <span data-ttu-id="be42e-117">Selezionare le porte hello in hello VM toowhich verrà bloccato il traffico in ingresso verso il basso.</span><span class="sxs-lookup"><span data-stu-id="be42e-117">You select hello ports on hello VM toowhich inbound traffic will be locked down.</span></span> <span data-ttu-id="be42e-118">Queste porte sono controllate da hello solo nella soluzione di tempo.</span><span class="sxs-lookup"><span data-stu-id="be42e-118">These ports are controlled by hello just in time solution.</span></span>

<span data-ttu-id="be42e-119">Quando un utente richiede accesso tooa macchina virtuale, il Centro sicurezza PC controlla tale utente hello [controllo di accesso basato sui ruoli (RBAC)](../active-directory/role-based-access-control-configure.md) delle autorizzazioni per l'accesso in scrittura per hello risorse di Azure.</span><span class="sxs-lookup"><span data-stu-id="be42e-119">When a user requests access tooa VM, Security Center checks that hello user has [Role-Based Access Control (RBAC)](../active-directory/role-based-access-control-configure.md) permissions that provide write access for hello Azure resource.</span></span> <span data-ttu-id="be42e-120">Se dispongono delle autorizzazioni di scrittura, hello richiesta viene approvata e il Centro sicurezza PC configura automaticamente hello rete sicurezza gruppi di porte di gestione del traffico toohello di tooallow in ingresso per hello di tempo specificato.</span><span class="sxs-lookup"><span data-stu-id="be42e-120">If they have write permissions, hello request is approved and Security Center automatically configures hello Network Security Groups (NSGs) tooallow inbound traffic toohello management ports for hello amount of time you specified.</span></span> <span data-ttu-id="be42e-121">Dopo il tempo di hello è scaduto, il Centro sicurezza PC Ripristina lo stato precedente hello NSGs tootheir.</span><span class="sxs-lookup"><span data-stu-id="be42e-121">After hello time has expired, Security Center restores hello NSGs tootheir previous states.</span></span>

> [!NOTE]
> <span data-ttu-id="be42e-122">L'accesso Just-in-Time alle macchine virtuali in Centro sicurezza attualmente supporta solo le macchine virtuali distribuite tramite Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="be42e-122">Security Center just in time VM access currently supports only VMs deployed through Azure Resource Manager.</span></span> <span data-ttu-id="be42e-123">informazioni su hello classic e modelli di distribuzione di gestione delle risorse, vedere toolearn [Azure Resource Manager e distribuzione classica](../azure-resource-manager/resource-manager-deployment-model.md).</span><span class="sxs-lookup"><span data-stu-id="be42e-123">toolearn more about hello classic and Resource Manager deployment models see [Azure Resource Manager vs. classic deployment](../azure-resource-manager/resource-manager-deployment-model.md).</span></span>
>
>

## <a name="using-just-in-time-access"></a><span data-ttu-id="be42e-124">Uso dell'accesso Just-in-Time</span><span class="sxs-lookup"><span data-stu-id="be42e-124">Using just in time access</span></span>

<span data-ttu-id="be42e-125">Hello **immediatamente nell'accesso alla VM ora** riquadro hello **Centro sicurezza PC** pannello viene visualizzato il numero di hello di macchine virtuali configurate per solo nel tempo accesso e hello il numero di richieste di accesso approvato effettuate in hello ultima settimana.</span><span class="sxs-lookup"><span data-stu-id="be42e-125">hello **Just in time VM access** tile on hello **Security Center** blade shows hello number of VMs configured for just in time access and hello number of approved access requests made in hello last week.</span></span>

<span data-ttu-id="be42e-126">Hello seleziona **immediatamente nell'accesso in fase di VM** riquadro e hello **immediatamente nell'accesso in fase di VM** apre pannello.</span><span class="sxs-lookup"><span data-stu-id="be42e-126">Select hello **Just in time VM access** tile and hello **Just in time VM access** blade opens.</span></span>

![Riquadro Accesso Just-In-Time alla VM][2]

<span data-ttu-id="be42e-128">Hello **immediatamente nell'accesso in fase di VM** pannello fornisce informazioni sullo stato di hello delle macchine virtuali:</span><span class="sxs-lookup"><span data-stu-id="be42e-128">hello **Just in time VM access** blade provides information on hello state of your VMs:</span></span>

- <span data-ttu-id="be42e-129">**Configurato** -macchine virtuali che sono stati configurati toosupport just-in-accesso in fase di macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="be42e-129">**Configured** - VMs that have been configured toosupport just in time VM access.</span></span> <span data-ttu-id="be42e-130">dati Hello presentati per hello settimana scorsa e includono per ogni VM hello numerose richieste approvate, data dell'ultimo accesso e l'ora e dell'ultimo utente.</span><span class="sxs-lookup"><span data-stu-id="be42e-130">hello data presented is for hello last week and includes for each VM hello number of approved requests, last access date and time, and last user.</span></span>
- <span data-ttu-id="be42e-131">**Consigliata** - Macchine virtuali che possono supportare l'accesso Just-In-Time, ma che non sono state configurate a tale scopo.</span><span class="sxs-lookup"><span data-stu-id="be42e-131">**Recommended** - VMs that can support just in time VM access but have not been configured to.</span></span> <span data-ttu-id="be42e-132">È consigliabile abilitare il controllo dell'accesso Just-In-Time per queste macchine virtuali.</span><span class="sxs-lookup"><span data-stu-id="be42e-132">We recommend that you enable just in time VM access control for these VMs.</span></span> <span data-ttu-id="be42e-133">Vedere [Abilitare l'accesso Just-In-Time alle macchine virtuali](#enable-just-in-time-vm-access).</span><span class="sxs-lookup"><span data-stu-id="be42e-133">See [Enable just in time VM access](#enable-just-in-time-vm-access).</span></span>
- <span data-ttu-id="be42e-134">**Nessuna raccomandazione** -motivi che possono causare una macchina virtuale non toobe consigliati sono:</span><span class="sxs-lookup"><span data-stu-id="be42e-134">**No recommendation** - Reasons that can cause a VM not toobe recommended are:</span></span>
  - <span data-ttu-id="be42e-135">Mancante NSG - hello solo nella soluzione ora richiede un toobe NSG sul posto.</span><span class="sxs-lookup"><span data-stu-id="be42e-135">Missing NSG - hello just in time solution requires an NSG toobe in place.</span></span>
  - <span data-ttu-id="be42e-136">Macchina virtuale classica - L'accesso Just-in-Time alle macchine virtuali in Centro sicurezza attualmente supporta solo le macchine virtuali distribuite tramite Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="be42e-136">Classic VM - Security Center just in time VM access currently supports only VMs deployed through Azure Resource Manager.</span></span> <span data-ttu-id="be42e-137">Una distribuzione classica non è supportata da hello solo nella soluzione di tempo.</span><span class="sxs-lookup"><span data-stu-id="be42e-137">A classic deployment is not supported by hello just in time solution.</span></span>
  - <span data-ttu-id="be42e-138">Altro - una macchina virtuale si trova in questa categoria se hello in-time soluzione è stata disattivata in Criteri di sicurezza hello di sottoscrizione hello o un gruppo di risorse hello o tale hello VM manca un indirizzo IP pubblico e non dispone di un gruppo sul posto.</span><span class="sxs-lookup"><span data-stu-id="be42e-138">Other - A VM is in this category if hello just in time solution is turned off in hello security policy of hello subscription or hello resource group, or that hello VM is missing a public IP and doesn't have an NSG in place.</span></span>

## <a name="configuring-a-just-in-time-access-policy"></a><span data-ttu-id="be42e-139">Configurazione dei criteri di accesso Just-In-Time</span><span class="sxs-lookup"><span data-stu-id="be42e-139">Configuring a just in time access policy</span></span>

<span data-ttu-id="be42e-140">hello tooselect macchine virtuali che si desidera tooenable:</span><span class="sxs-lookup"><span data-stu-id="be42e-140">tooselect hello VMs that you want tooenable:</span></span>

1. <span data-ttu-id="be42e-141">In hello **immediatamente nell'accesso alla VM ora** blade, seleziona hello **consigliato** scheda.</span><span class="sxs-lookup"><span data-stu-id="be42e-141">On hello **Just in time VM access** blade, select hello **Recommended** tab.</span></span>

  ![Abilitare l'accesso Just-in-Time][3]

2. <span data-ttu-id="be42e-143">In **macchine virtuali**, selezionare le macchine virtuali hello che si desidera tooenable.</span><span class="sxs-lookup"><span data-stu-id="be42e-143">Under **VMs**, select hello VMs that you want tooenable.</span></span> <span data-ttu-id="be42e-144">In questo modo un tooa Avanti VM di segno di spunta.</span><span class="sxs-lookup"><span data-stu-id="be42e-144">This puts a checkmark next tooa VM.</span></span>
3. <span data-ttu-id="be42e-145">Selezionare **Abilita JIT in VM**.</span><span class="sxs-lookup"><span data-stu-id="be42e-145">Select **Enable JIT on VMs**.</span></span>
4. <span data-ttu-id="be42e-146">Selezionare **Salva**.</span><span class="sxs-lookup"><span data-stu-id="be42e-146">Select **Save**.</span></span>

### <a name="default-ports"></a><span data-ttu-id="be42e-147">Porte predefinite</span><span class="sxs-lookup"><span data-stu-id="be42e-147">Default ports</span></span>

<span data-ttu-id="be42e-148">È possibile visualizzare porte predefinite hello che centro di sicurezza è consigliabile specificare in-time.</span><span class="sxs-lookup"><span data-stu-id="be42e-148">You can see hello default ports that Security Center recommends enabling just in time.</span></span>

1. <span data-ttu-id="be42e-149">In hello **immediatamente nell'accesso alla VM ora** blade, seleziona hello **consigliato** scheda.</span><span class="sxs-lookup"><span data-stu-id="be42e-149">On hello **Just in time VM access** blade, select hello **Recommended** tab.</span></span>

  ![Visualizzare le porte predefinite][6]

2. <span data-ttu-id="be42e-151">In **Macchine virtuali** selezionare una macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="be42e-151">Under **VMs**, select a VM.</span></span> <span data-ttu-id="be42e-152">In questo modo un segno di spunta successivo toohello macchina virtuale e quindi apre hello **configurazione di accesso VM JIT** blade.</span><span class="sxs-lookup"><span data-stu-id="be42e-152">This puts a checkmark next toohello VM and opens hello **JIT VM access configuration** blade.</span></span> <span data-ttu-id="be42e-153">Questo pannello consente di visualizzare le porte predefinite hello.</span><span class="sxs-lookup"><span data-stu-id="be42e-153">This blade displays hello default ports.</span></span>

### <a name="add-ports"></a><span data-ttu-id="be42e-154">Aggiungere porte</span><span class="sxs-lookup"><span data-stu-id="be42e-154">Add ports</span></span>

<span data-ttu-id="be42e-155">Da hello **configurazione di accesso VM JIT** pannello, è possibile anche aggiungere e configurare una nuova porta su cui si desidera hello tooenable solo nella soluzione di tempo.</span><span class="sxs-lookup"><span data-stu-id="be42e-155">From hello **JIT VM access configuration** blade, you can also add and configure a new port on which you want tooenable hello just in time solution.</span></span>

1. <span data-ttu-id="be42e-156">In hello **configurazione di accesso VM JIT** pannello seleziona **Aggiungi**.</span><span class="sxs-lookup"><span data-stu-id="be42e-156">On hello **JIT VM access configuration** blade, select **Add**.</span></span> <span data-ttu-id="be42e-157">Verrà visualizzata hello **Aggiungi configurazione della porta** blade.</span><span class="sxs-lookup"><span data-stu-id="be42e-157">This opens hello **Add port configuration** blade.</span></span>

  ![Configurazione delle porte][7]

2. <span data-ttu-id="be42e-159">In **Aggiungi configurazione della porta** pannello identificare hello porta, il tipo di protocollo, tempo di richiesta gli IP di origine e numero massimo consentita.</span><span class="sxs-lookup"><span data-stu-id="be42e-159">On **Add port configuration** blade, you identify hello port, protocol type, allowed source IPs, and maximum request time.</span></span>

  <span data-ttu-id="be42e-160">Consentito gli IP di origine sono hello accesso consentito tooget gli intervalli IP durante una richiesta approvata.</span><span class="sxs-lookup"><span data-stu-id="be42e-160">Allowed source IPs are hello IP ranges allowed tooget access upon an approved request.</span></span>

  <span data-ttu-id="be42e-161">Tempo massimo della richiesta è l'intervallo di tempo massimo di hello che possa essere aperta una porta specifica.</span><span class="sxs-lookup"><span data-stu-id="be42e-161">Maximum request time is hello maximum time window that a specific port can be opened.</span></span>

3. <span data-ttu-id="be42e-162">Selezionare **OK**.</span><span class="sxs-lookup"><span data-stu-id="be42e-162">Select **OK**.</span></span>

## <a name="requesting-access-tooa-vm"></a><span data-ttu-id="be42e-163">La richiesta di accesso tooa VM</span><span class="sxs-lookup"><span data-stu-id="be42e-163">Requesting access tooa VM</span></span>

<span data-ttu-id="be42e-164">toorequest accesso tooa VM:</span><span class="sxs-lookup"><span data-stu-id="be42e-164">toorequest access tooa VM:</span></span>

1. <span data-ttu-id="be42e-165">In hello **immediatamente nell'accesso alla VM ora** blade, seleziona hello **configurata** scheda.</span><span class="sxs-lookup"><span data-stu-id="be42e-165">On hello **Just in time VM access** blade, select hello **Configured** tab.</span></span>
2. <span data-ttu-id="be42e-166">In **macchine virtuali**, selezionare le macchine virtuali hello che si desidera tooenable accesso.</span><span class="sxs-lookup"><span data-stu-id="be42e-166">Under **VMs**, select hello VMs that you want tooenable access.</span></span> <span data-ttu-id="be42e-167">In questo modo un tooa Avanti VM di segno di spunta.</span><span class="sxs-lookup"><span data-stu-id="be42e-167">This puts a checkmark next tooa VM.</span></span>
3. <span data-ttu-id="be42e-168">Selezionare **Richiedi accesso**.</span><span class="sxs-lookup"><span data-stu-id="be42e-168">Select **Request access**.</span></span> <span data-ttu-id="be42e-169">Verrà visualizzata hello **richiedere l'accesso** blade.</span><span class="sxs-lookup"><span data-stu-id="be42e-169">This opens hello **Request access** blade.</span></span>

  ![Richiesta di accesso tooa VM][4]

4. <span data-ttu-id="be42e-171">In hello **richiedere l'accesso** pannello è configurare per ogni tooopen porte hello di macchina virtuale con indirizzo IP di origine hello hello porta è aperta intervallo di tempo hello tooand per cui hello porta è aperta.</span><span class="sxs-lookup"><span data-stu-id="be42e-171">On hello **Request access** blade, you configure for each VM hello ports tooopen along with hello source IP that hello port is opened tooand hello time window for which hello port is opened.</span></span> <span data-ttu-id="be42e-172">È possibile richiedere l'accesso toohello solo a porte configurate in hello solo nei criteri di tempo.</span><span class="sxs-lookup"><span data-stu-id="be42e-172">You can request access only toohello ports that are configured in hello just in time policy.</span></span> <span data-ttu-id="be42e-173">Ogni porta ha un tempo massimo consentito, derivato da hello solo nei criteri di tempo.</span><span class="sxs-lookup"><span data-stu-id="be42e-173">Each port has a maximum allowed time derived from hello just in time policy.</span></span>
5. <span data-ttu-id="be42e-174">Selezionare **Open ports** (Apri porte).</span><span class="sxs-lookup"><span data-stu-id="be42e-174">Select **Open ports**.</span></span>

## <a name="editing-a-just-in-time-access-policy"></a><span data-ttu-id="be42e-175">Modifica dei criteri di accesso Just-In-Time</span><span class="sxs-lookup"><span data-stu-id="be42e-175">Editing a just in time access policy</span></span>

<span data-ttu-id="be42e-176">È possibile modificare una macchina virtuale esistente solo nei criteri di tempo aggiungendo e configurando un nuovo tooopen porta per la macchina virtuale o mediante la modifica di qualsiasi altro parametro porta tooan correlate già protetta.</span><span class="sxs-lookup"><span data-stu-id="be42e-176">You can change a VM's existing just in time policy by adding and configuring a new port tooopen for that VM, or by changing any other parameter related tooan already protected port.</span></span>

<span data-ttu-id="be42e-177">In ordine tooedit esistente solo nei criteri di tempo di una macchina virtuale, hello **configurata** scheda viene usata:</span><span class="sxs-lookup"><span data-stu-id="be42e-177">In order tooedit an existing just in time policy of a VM, hello **Configured** tab is used:</span></span>

1. <span data-ttu-id="be42e-178">In **macchine virtuali**, selezionare una macchina virtuale tooadd tooby una porta facendo clic su punti hello tre all'interno di riga hello per la macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="be42e-178">Under **VMs**, select a VM tooadd a port tooby clicking on hello three dots within hello row for that VM.</span></span> <span data-ttu-id="be42e-179">Verrà aperto un menu.</span><span class="sxs-lookup"><span data-stu-id="be42e-179">This opens a menu.</span></span>
2. <span data-ttu-id="be42e-180">Selezionare **modifica** nel menu hello.</span><span class="sxs-lookup"><span data-stu-id="be42e-180">Select **Edit** in hello menu.</span></span> <span data-ttu-id="be42e-181">Verrà visualizzata hello **configurazione di accesso VM JIT** blade.</span><span class="sxs-lookup"><span data-stu-id="be42e-181">This opens hello **JIT VM access configuration** blade.</span></span>

  ![Modificare i criteri][8]

3. <span data-ttu-id="be42e-183">In hello **configurazione di accesso VM JIT** pannello, è possibile modificare le impostazioni esistenti di hello di una porta già protetta facendo clic su una porta specifica, o è possibile selezionare **Aggiungi**.</span><span class="sxs-lookup"><span data-stu-id="be42e-183">On hello **JIT VM access configuration** blade, you can either edit hello existing settings of an already protected port by clicking on its port, or you can select **Add**.</span></span> <span data-ttu-id="be42e-184">Verrà visualizzata hello **Aggiungi configurazione della porta** blade.</span><span class="sxs-lookup"><span data-stu-id="be42e-184">This opens hello **Add port configuration** blade.</span></span>

  ![Aggiungere una porta][7]

4. <span data-ttu-id="be42e-186">In **Aggiungi configurazione della porta** pannello identificare porta hello, tipo di protocollo, gli indirizzi IP di origine consentiti e tempo massimo della richiesta.</span><span class="sxs-lookup"><span data-stu-id="be42e-186">On **Add port configuration** blade identify hello port, protocol type, allowed source IPs, and maximum request time.</span></span>
5. <span data-ttu-id="be42e-187">Selezionare **OK**.</span><span class="sxs-lookup"><span data-stu-id="be42e-187">Select **OK**.</span></span>
6. <span data-ttu-id="be42e-188">Selezionare **Salva**.</span><span class="sxs-lookup"><span data-stu-id="be42e-188">Select **Save**.</span></span>

## <a name="auditing-just-in-time-access-activity"></a><span data-ttu-id="be42e-189">Controllo delle attività di accesso Just-in-Time</span><span class="sxs-lookup"><span data-stu-id="be42e-189">Auditing just in time access activity</span></span>

<span data-ttu-id="be42e-190">È possibile ottenere informazioni approfondite sulle attività delle macchine virtuali tramite la funzionalità Ricerca log.</span><span class="sxs-lookup"><span data-stu-id="be42e-190">You can gain insights into VM activities using log search.</span></span> <span data-ttu-id="be42e-191">registri tooview:</span><span class="sxs-lookup"><span data-stu-id="be42e-191">tooview logs:</span></span>

1. <span data-ttu-id="be42e-192">In hello **immediatamente nell'accesso alla VM ora** blade, seleziona hello **configurata** scheda.</span><span class="sxs-lookup"><span data-stu-id="be42e-192">On hello **Just in time VM access** blade, select hello **Configured** tab.</span></span>
2. <span data-ttu-id="be42e-193">In **macchine virtuali**, selezionare un informazioni tooview VM su facendo clic su punti hello tre all'interno di riga hello per la macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="be42e-193">Under **VMs**, select a VM tooview information about by clicking on hello three dots within hello row for that VM.</span></span> <span data-ttu-id="be42e-194">Verrà aperto un menu.</span><span class="sxs-lookup"><span data-stu-id="be42e-194">This opens a menu.</span></span>
3. <span data-ttu-id="be42e-195">Selezionare **Log attività** nel menu hello.</span><span class="sxs-lookup"><span data-stu-id="be42e-195">Select **Activity Log** in hello menu.</span></span> <span data-ttu-id="be42e-196">Verrà visualizzata hello **log attività** blade.</span><span class="sxs-lookup"><span data-stu-id="be42e-196">This opens hello **Activity log** blade.</span></span>

![Selezionare il log attività][9]

<span data-ttu-id="be42e-198">Hello **log attività** pannello fornisce una visualizzazione filtrata di operazioni precedenti per la macchina virtuale con data, ora e sottoscrizione.</span><span class="sxs-lookup"><span data-stu-id="be42e-198">hello **Activity log** blade provides a filtered view of previous operations for that VM along with time, date, and subscription.</span></span>

![Visualizzare il log attività][5]

<span data-ttu-id="be42e-200">È possibile scaricare informazioni sul log hello selezionando **fare clic qui toodownload tutti gli elementi di hello in formato CSV**.</span><span class="sxs-lookup"><span data-stu-id="be42e-200">You can download hello log information by selecting **Click here toodownload all hello items as CSV**.</span></span>

<span data-ttu-id="be42e-201">Modificare i filtri di hello e selezionare **applica** toocreate una ricerca e log.</span><span class="sxs-lookup"><span data-stu-id="be42e-201">Modify hello filters and select **Apply** toocreate a search and log.</span></span>

## <a name="using-just-in-time-vm-access-via-powershell"></a><span data-ttu-id="be42e-202">Uso dell'accesso Just-In-Time alle macchine virtuali tramite PowerShell</span><span class="sxs-lookup"><span data-stu-id="be42e-202">Using just in time VM access via PowerShell</span></span>

<span data-ttu-id="be42e-203">In ordine toouse Ciao solo tempi di una soluzione tramite PowerShell, assicurarsi di avere hello [più recente](/powershell/azure/install-azurerm-ps) versione di Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="be42e-203">In order toouse hello just in time solution via PowerShell, make sure you have hello [latest](/powershell/azure/install-azurerm-ps) Azure PowerShell version.</span></span>
<span data-ttu-id="be42e-204">Al termine dell'operazione, è necessario hello tooinstall [più recente](https://www.powershellgallery.com/packages/Azure-Security-Center/0.0.12) Centro sicurezza di Azure dalla raccolta di PowerShell hello.</span><span class="sxs-lookup"><span data-stu-id="be42e-204">Once you do, you need tooinstall hello [latest](https://www.powershellgallery.com/packages/Azure-Security-Center/0.0.12) Azure Security Center from hello PowerShell gallery.</span></span>

### <a name="configuring-a-just-in-time-policy-for-a-vm"></a><span data-ttu-id="be42e-205">Configurazione dei criteri Just-In-Time per una macchina virtuale</span><span class="sxs-lookup"><span data-stu-id="be42e-205">Configuring a just in time policy for a VM</span></span>

<span data-ttu-id="be42e-206">tooconfigure un solo nei criteri di tempo in una macchina virtuale specifica, è necessario toorun questo comando nella sessione di PowerShell: Set-ASCJITAccessPolicy.</span><span class="sxs-lookup"><span data-stu-id="be42e-206">tooconfigure a just in time policy on a specific VM, you need toorun this command in your PowerShell session: Set-ASCJITAccessPolicy.</span></span>
<span data-ttu-id="be42e-207">Seguire hello cmdlet documentazione toolearn altre.</span><span class="sxs-lookup"><span data-stu-id="be42e-207">Follow hello cmdlet documentation toolearn more.</span></span>

### <a name="requesting-access-tooa-vm"></a><span data-ttu-id="be42e-208">La richiesta di accesso tooa VM</span><span class="sxs-lookup"><span data-stu-id="be42e-208">Requesting access tooa VM</span></span>

<span data-ttu-id="be42e-209">una macchina virtuale specifica che è protetta con tooaccess hello solo nella soluzione di tempo, è necessario toorun questo comando nella sessione di PowerShell: ASCJITAccess Invoke.</span><span class="sxs-lookup"><span data-stu-id="be42e-209">tooaccess a specific VM that is protected with hello just in time solution, you need toorun this command in your PowerShell session: Invoke-ASCJITAccess.</span></span>
<span data-ttu-id="be42e-210">Seguire hello cmdlet documentazione toolearn altre.</span><span class="sxs-lookup"><span data-stu-id="be42e-210">Follow hello cmdlet documentation toolearn more.</span></span>

## <a name="next-steps"></a><span data-ttu-id="be42e-211">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="be42e-211">Next steps</span></span>
<span data-ttu-id="be42e-212">In questo articolo è stato descritto come in-time accesso macchina virtuale in Centro sicurezza PC consente accesso tooyour Azure è possibile controllare le macchine virtuali.</span><span class="sxs-lookup"><span data-stu-id="be42e-212">In this article, you learned how just in time VM access in Security Center helps you control access tooyour Azure virtual machines.</span></span>

<span data-ttu-id="be42e-213">toolearn ulteriori informazioni su Centro di sicurezza, vedere l'esempio hello:</span><span class="sxs-lookup"><span data-stu-id="be42e-213">toolearn more about Security Center, see hello following:</span></span>

- <span data-ttu-id="be42e-214">[L'impostazione di criteri di sicurezza](security-center-policies.md) -informazioni come tooconfigure i criteri di sicurezza per le sottoscrizioni di Azure e i gruppi di risorse.</span><span class="sxs-lookup"><span data-stu-id="be42e-214">[Setting security policies](security-center-policies.md) — Learn how tooconfigure security policies for your Azure subscriptions and resource groups.</span></span>
- <span data-ttu-id="be42e-215">[Gestione delle raccomandazioni di sicurezza](security-center-recommendations.md): informazioni sul modo in cui le raccomandazioni semplificano la protezione delle risorse di Azure.</span><span class="sxs-lookup"><span data-stu-id="be42e-215">[Managing security recommendations](security-center-recommendations.md) — Learn how recommendations help you protect your Azure resources.</span></span>
- <span data-ttu-id="be42e-216">[Il monitoraggio dello stato di sicurezza](security-center-monitoring.md) : informazioni su come toomonitor hello integrità delle risorse di Azure.</span><span class="sxs-lookup"><span data-stu-id="be42e-216">[Security health monitoring](security-center-monitoring.md) — Learn how toomonitor hello health of your Azure resources.</span></span>
- <span data-ttu-id="be42e-217">[La gestione e risponde avvisi toosecurity](security-center-managing-and-responding-alerts.md) , informazioni come avvisi toosecurity toomanage e rispondere.</span><span class="sxs-lookup"><span data-stu-id="be42e-217">[Managing and responding toosecurity alerts](security-center-managing-and-responding-alerts.md) — Learn how toomanage and respond toosecurity alerts.</span></span>
- <span data-ttu-id="be42e-218">[Monitoraggio di soluzioni per i partner](security-center-partner-solutions.md) : informazioni su come toomonitor hello lo stato di integrità delle soluzioni di partner.</span><span class="sxs-lookup"><span data-stu-id="be42e-218">[Monitoring partner solutions](security-center-partner-solutions.md) — Learn how toomonitor hello health status of your partner solutions.</span></span>
- <span data-ttu-id="be42e-219">[Domande frequenti su Centro sicurezza PC](security-center-faq.md) : domande frequenti sull'utilizzo di hello servizio di ricerca.</span><span class="sxs-lookup"><span data-stu-id="be42e-219">[Security Center FAQ](security-center-faq.md) — Find frequently asked questions about using hello service.</span></span>
- <span data-ttu-id="be42e-220">[Blog sulla sicurezza di Azure](https://blogs.msdn.microsoft.com/azuresecurity/) : post di blog sulla sicurezza e sulla conformità di Azure.</span><span class="sxs-lookup"><span data-stu-id="be42e-220">[Azure Security blog](https://blogs.msdn.microsoft.com/azuresecurity/) — Find blog posts about Azure security and compliance.</span></span>


<!--Image references-->
[1]: ./media/security-center-just-in-time/just-in-time-scenario.png
[2]: ./media/security-center-just-in-time/just-in-time.png
[3]: ./media/security-center-just-in-time/enable-just-in-time-access.png
[4]: ./media/security-center-just-in-time/request-access-to-a-vm.png
[5]: ./media/security-center-just-in-time/activity-log.png
[6]: ./media/security-center-just-in-time/default-ports.png
[7]: ./media/security-center-just-in-time/add-a-port.png
[8]: ./media/security-center-just-in-time/edit-policy.png
[9]: ./media/security-center-just-in-time/select-activity-log.png

---
title: Accesso JIT (Just-in-Time) alle macchine virtuali nel Centro sicurezza di Azure | Microsoft Docs
description: In questo documento viene illustrato come usare l'accesso JIT (Just-in-Time) alle macchine virtuali nel Centro sicurezza di Azure per controllare l'accesso alle macchine virtuali di Azure.
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
ms.openlocfilehash: 5bb87488dcfc79ed4baa1dbd81dc4e1174f84e4b
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/18/2017
---
# <a name="manage-virtual-machine-access-using-just-in-time"></a><span data-ttu-id="3cf09-103">Gestire l'accesso alle macchine virtuali con la funzionalità JIT (Just-in-Time)</span><span class="sxs-lookup"><span data-stu-id="3cf09-103">Manage virtual machine access using just in time</span></span>

<span data-ttu-id="3cf09-104">L'accesso Just-in-Time alle macchine virtuali può essere usato per bloccare il traffico in ingresso alle macchine virtuali di Azure, riducendo l'esposizione agli attacchi e al tempo stesso offrendo un facile accesso per connettersi alle macchine virtuali quando necessario.</span><span class="sxs-lookup"><span data-stu-id="3cf09-104">Just in time virtual machine (VM) access can be used to lock down inbound traffic to your Azure VMs, reducing exposure to attacks while providing easy access to connect to VMs when needed.</span></span>

> [!NOTE]
> <span data-ttu-id="3cf09-105">La funzionalità Just-In-Time è in anteprima e disponibile nel livello Standard di Centro sicurezza.</span><span class="sxs-lookup"><span data-stu-id="3cf09-105">The just in time feature is in preview and available on the Standard tier of Security Center.</span></span>  <span data-ttu-id="3cf09-106">Per altre informazioni sui piani tariffari di Centro sicurezza, vedere [Prezzi](security-center-pricing.md).</span><span class="sxs-lookup"><span data-stu-id="3cf09-106">See [Pricing](security-center-pricing.md) to learn more about Security Center's pricing tiers.</span></span>
>
>

## <a name="attack-scenario"></a><span data-ttu-id="3cf09-107">Scenario di attacco</span><span class="sxs-lookup"><span data-stu-id="3cf09-107">Attack scenario</span></span>

<span data-ttu-id="3cf09-108">Gli attacchi di forza bruta generalmente prendono di mira le porte di gestione per tentare di ottenere l'accesso a una macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="3cf09-108">Brute force attacks commonly target management ports as a means to gain access to a VM.</span></span> <span data-ttu-id="3cf09-109">Se l'attacco ha esito positivo, un utente malintenzionato può assumere il controllo della macchina virtuale e penetrare nell'ambiente.</span><span class="sxs-lookup"><span data-stu-id="3cf09-109">If successful, an attacker can take control over the VM and establish a foothold into your environment.</span></span>

<span data-ttu-id="3cf09-110">Un modo per ridurre l'esposizione agli attacchi di forza bruta consiste nel limitare la quantità di tempo per cui la porta è aperta.</span><span class="sxs-lookup"><span data-stu-id="3cf09-110">One way to reduce exposure to a brute force attack is to limit the amount of time that a port is open.</span></span> <span data-ttu-id="3cf09-111">Non è necessario lasciare aperte le porte di gestione in qualsiasi momento.</span><span class="sxs-lookup"><span data-stu-id="3cf09-111">Management ports do not need to be open at all times.</span></span> <span data-ttu-id="3cf09-112">Devono essere aperte solo durante la connessione alla macchina virtuale, ad esempio per eseguire attività di gestione o manutenzione.</span><span class="sxs-lookup"><span data-stu-id="3cf09-112">They only need to be open while you are connected to the VM, for example to perform management or maintenance tasks.</span></span> <span data-ttu-id="3cf09-113">Quando la funzionalità Just-In-Time è abilitata, Centro sicurezza usa le regole del [gruppo di sicurezza di rete ](../virtual-network/virtual-networks-nsg.md) (NSG), che limitano l'accesso alle porte di gestione per impedire che possano essere attaccate da utenti malintenzionati.</span><span class="sxs-lookup"><span data-stu-id="3cf09-113">When just in time is enabled, Security Center uses [Network Security Group](../virtual-network/virtual-networks-nsg.md) (NSG) rules, which restrict access to management ports so they cannot be targeted by attackers.</span></span>

![Scenario Just-in-Time][1]

## <a name="how-does-just-in-time-access-work"></a><span data-ttu-id="3cf09-115">Come funziona l'accesso Just-in-Time?</span><span class="sxs-lookup"><span data-stu-id="3cf09-115">How does just in time access work?</span></span>

<span data-ttu-id="3cf09-116">Quando è abilitata la funzionalità Just-in-Time, Centro sicurezza protegge il traffico in ingresso alle macchine virtuali di Azure creando una regola NSG.</span><span class="sxs-lookup"><span data-stu-id="3cf09-116">When just in time is enabled, Security Center locks down inbound traffic to your Azure VMs by creating an NSG rule.</span></span> <span data-ttu-id="3cf09-117">Selezionare le porte nella macchina virtuale per cui proteggere il traffico in ingresso.</span><span class="sxs-lookup"><span data-stu-id="3cf09-117">You select the ports on the VM to which inbound traffic will be locked down.</span></span> <span data-ttu-id="3cf09-118">Queste porte sono controllate dalla soluzione Just-in-Time.</span><span class="sxs-lookup"><span data-stu-id="3cf09-118">These ports are controlled by the just in time solution.</span></span>

<span data-ttu-id="3cf09-119">Quando un utente richiede l'accesso a una macchina virtuale, Centro sicurezza controlla che l'utente disponga di autorizzazioni di [controllo degli accessi in base al ruolo (RBAC)](../active-directory/role-based-access-control-configure.md) che forniscono l'accesso in scrittura alla risorsa di Azure.</span><span class="sxs-lookup"><span data-stu-id="3cf09-119">When a user requests access to a VM, Security Center checks that the user has [Role-Based Access Control (RBAC)](../active-directory/role-based-access-control-configure.md) permissions that provide write access for the Azure resource.</span></span> <span data-ttu-id="3cf09-120">Se l'utente dispone delle autorizzazioni di scrittura, la richiesta viene approvata e Centro sicurezza configura automaticamente i gruppi di sicurezza di rete per consentire il traffico in entrata alle porte di gestione per il periodo di tempo specificato.</span><span class="sxs-lookup"><span data-stu-id="3cf09-120">If they have write permissions, the request is approved and Security Center automatically configures the Network Security Groups (NSGs) to allow inbound traffic to the management ports for the amount of time you specified.</span></span> <span data-ttu-id="3cf09-121">Al termine di questo periodo, Centro sicurezza ripristina gli stati precedenti dei gruppi di sicurezza di rete.</span><span class="sxs-lookup"><span data-stu-id="3cf09-121">After the time has expired, Security Center restores the NSGs to their previous states.</span></span>

> [!NOTE]
> <span data-ttu-id="3cf09-122">L'accesso Just-in-Time alle macchine virtuali in Centro sicurezza attualmente supporta solo le macchine virtuali distribuite tramite Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="3cf09-122">Security Center just in time VM access currently supports only VMs deployed through Azure Resource Manager.</span></span> <span data-ttu-id="3cf09-123">Per altre informazioni sui modelli di distribuzione classica e con Azure Resource Manager, vedere [Distribuzione Azure Resource Manager o classica](../azure-resource-manager/resource-manager-deployment-model.md).</span><span class="sxs-lookup"><span data-stu-id="3cf09-123">To learn more about the classic and Resource Manager deployment models see [Azure Resource Manager vs. classic deployment](../azure-resource-manager/resource-manager-deployment-model.md).</span></span>
>
>

## <a name="using-just-in-time-access"></a><span data-ttu-id="3cf09-124">Uso dell'accesso Just-in-Time</span><span class="sxs-lookup"><span data-stu-id="3cf09-124">Using just in time access</span></span>

<span data-ttu-id="3cf09-125">Il riquadro **Accesso Just-In-Time alla VM** nel pannello **Centro sicurezza** mostra il numero di macchine virtuali configurate per l'accesso Just-in-Time e il numero di richieste di accesso approvate nell'ultima settimana.</span><span class="sxs-lookup"><span data-stu-id="3cf09-125">The **Just in time VM access** tile on the **Security Center** blade shows the number of VMs configured for just in time access and the number of approved access requests made in the last week.</span></span>

<span data-ttu-id="3cf09-126">Selezionare il riquadro **Accesso Just-In-Time alla VM** per aprire il pannello **Accesso Just-In-Time alla VM**.</span><span class="sxs-lookup"><span data-stu-id="3cf09-126">Select the **Just in time VM access** tile and the **Just in time VM access** blade opens.</span></span>

![Riquadro Accesso Just-In-Time alla VM][2]

<span data-ttu-id="3cf09-128">Il pannello **Accesso Just-In-Time alla VM** fornisce informazioni sullo stato delle macchine virtuali:</span><span class="sxs-lookup"><span data-stu-id="3cf09-128">The **Just in time VM access** blade provides information on the state of your VMs:</span></span>

- <span data-ttu-id="3cf09-129">**Configurata** - Macchine virtuali che sono state configurate per supportare l'accesso Just-In-Time.</span><span class="sxs-lookup"><span data-stu-id="3cf09-129">**Configured** - VMs that have been configured to support just in time VM access.</span></span> <span data-ttu-id="3cf09-130">I dati visualizzati sono relativi all'ultima settimana e includono, per ogni macchina virtuale, il numero di richieste approvate, la data e l'ora dell'ultimo accesso e l'ultimo utente.</span><span class="sxs-lookup"><span data-stu-id="3cf09-130">The data presented is for the last week and includes for each VM the number of approved requests, last access date and time, and last user.</span></span>
- <span data-ttu-id="3cf09-131">**Consigliata** - Macchine virtuali che possono supportare l'accesso Just-In-Time, ma che non sono state configurate a tale scopo.</span><span class="sxs-lookup"><span data-stu-id="3cf09-131">**Recommended** - VMs that can support just in time VM access but have not been configured to.</span></span> <span data-ttu-id="3cf09-132">È consigliabile abilitare il controllo dell'accesso Just-In-Time per queste macchine virtuali.</span><span class="sxs-lookup"><span data-stu-id="3cf09-132">We recommend that you enable just in time VM access control for these VMs.</span></span> <span data-ttu-id="3cf09-133">Vedere [Abilitare l'accesso Just-In-Time alle macchine virtuali](#enable-just-in-time-vm-access).</span><span class="sxs-lookup"><span data-stu-id="3cf09-133">See [Enable just in time VM access](#enable-just-in-time-vm-access).</span></span>
- <span data-ttu-id="3cf09-134">**Nessuna raccomandazione** - I motivi per cui una macchina virtuale può risultare non raccomandata sono:</span><span class="sxs-lookup"><span data-stu-id="3cf09-134">**No recommendation** - Reasons that can cause a VM not to be recommended are:</span></span>
  - <span data-ttu-id="3cf09-135">Gruppo di sicurezza di rete mancante - La soluzione Just-In-Time richiede la presenza di un gruppo di sicurezza di rete.</span><span class="sxs-lookup"><span data-stu-id="3cf09-135">Missing NSG - The just in time solution requires an NSG to be in place.</span></span>
  - <span data-ttu-id="3cf09-136">Macchina virtuale classica - L'accesso Just-in-Time alle macchine virtuali in Centro sicurezza attualmente supporta solo le macchine virtuali distribuite tramite Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="3cf09-136">Classic VM - Security Center just in time VM access currently supports only VMs deployed through Azure Resource Manager.</span></span> <span data-ttu-id="3cf09-137">Una distribuzione classica non è supportata dalla soluzione Just-In-Time.</span><span class="sxs-lookup"><span data-stu-id="3cf09-137">A classic deployment is not supported by the just in time solution.</span></span>
  - <span data-ttu-id="3cf09-138">Altro - Una macchina virtuale rientra in questa categoria se la soluzione Just-In-Time è disattivata nei criteri di sicurezza della sottoscrizione o del gruppo di risorse oppure se la macchina virtuale non dispone di un indirizzo IP pubblico e di un gruppo di sicurezza di rete.</span><span class="sxs-lookup"><span data-stu-id="3cf09-138">Other - A VM is in this category if the just in time solution is turned off in the security policy of the subscription or the resource group, or that the VM is missing a public IP and doesn't have an NSG in place.</span></span>

## <a name="configuring-a-just-in-time-access-policy"></a><span data-ttu-id="3cf09-139">Configurazione dei criteri di accesso Just-In-Time</span><span class="sxs-lookup"><span data-stu-id="3cf09-139">Configuring a just in time access policy</span></span>

<span data-ttu-id="3cf09-140">Per selezionare le macchine virtuali da abilitare:</span><span class="sxs-lookup"><span data-stu-id="3cf09-140">To select the VMs that you want to enable:</span></span>

1. <span data-ttu-id="3cf09-141">Nel pannello **Accesso Just-In-Time alla VM** selezionare la scheda **Consigliata**.</span><span class="sxs-lookup"><span data-stu-id="3cf09-141">On the **Just in time VM access** blade, select the **Recommended** tab.</span></span>

  ![Abilitare l'accesso Just-in-Time][3]

2. <span data-ttu-id="3cf09-143">In **Macchine virtuali** selezionare le macchine virtuali da abilitare.</span><span class="sxs-lookup"><span data-stu-id="3cf09-143">Under **VMs**, select the VMs that you want to enable.</span></span> <span data-ttu-id="3cf09-144">Verrà visualizzato un segno di spunta accanto a una macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="3cf09-144">This puts a checkmark next to a VM.</span></span>
3. <span data-ttu-id="3cf09-145">Selezionare **Abilita JIT in VM**.</span><span class="sxs-lookup"><span data-stu-id="3cf09-145">Select **Enable JIT on VMs**.</span></span>
4. <span data-ttu-id="3cf09-146">Selezionare **Salva**.</span><span class="sxs-lookup"><span data-stu-id="3cf09-146">Select **Save**.</span></span>

### <a name="default-ports"></a><span data-ttu-id="3cf09-147">Porte predefinite</span><span class="sxs-lookup"><span data-stu-id="3cf09-147">Default ports</span></span>

<span data-ttu-id="3cf09-148">È possibile visualizzare le porte predefinite per cui Centro sicurezza consiglia l'abilitazione della funzionalità Just-In-Time.</span><span class="sxs-lookup"><span data-stu-id="3cf09-148">You can see the default ports that Security Center recommends enabling just in time.</span></span>

1. <span data-ttu-id="3cf09-149">Nel pannello **Accesso Just-In-Time alla VM** selezionare la scheda **Consigliata**.</span><span class="sxs-lookup"><span data-stu-id="3cf09-149">On the **Just in time VM access** blade, select the **Recommended** tab.</span></span>

  ![Visualizzare le porte predefinite][6]

2. <span data-ttu-id="3cf09-151">In **Macchine virtuali** selezionare una macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="3cf09-151">Under **VMs**, select a VM.</span></span> <span data-ttu-id="3cf09-152">Verrà visualizzato un segno di spunta accanto alla macchina virtuale e verrà aperto il pannello **JIT VM access configuration** (Configurazione accesso Just-In-Time alla VM).</span><span class="sxs-lookup"><span data-stu-id="3cf09-152">This puts a checkmark next to the VM and opens the **JIT VM access configuration** blade.</span></span> <span data-ttu-id="3cf09-153">Questo pannello consente di visualizzare le porte predefinite.</span><span class="sxs-lookup"><span data-stu-id="3cf09-153">This blade displays the default ports.</span></span>

### <a name="add-ports"></a><span data-ttu-id="3cf09-154">Aggiungere porte</span><span class="sxs-lookup"><span data-stu-id="3cf09-154">Add ports</span></span>

<span data-ttu-id="3cf09-155">Dal pannello **JIT VM access configuration** (Configurazione accesso Just-In-Time alla VM) è anche possibile aggiungere e configurare una nuova porta per cui abilitare la soluzione Just-In-Time.</span><span class="sxs-lookup"><span data-stu-id="3cf09-155">From the **JIT VM access configuration** blade, you can also add and configure a new port on which you want to enable the just in time solution.</span></span>

1. <span data-ttu-id="3cf09-156">Nel pannello **JIT VM access configuration** (Configurazione accesso Just-In-Time alla VM) selezionare **Aggiungi**.</span><span class="sxs-lookup"><span data-stu-id="3cf09-156">On the **JIT VM access configuration** blade, select **Add**.</span></span> <span data-ttu-id="3cf09-157">Verrà aperto il pannello **Add port configuration** (Aggiungi configurazione porta).</span><span class="sxs-lookup"><span data-stu-id="3cf09-157">This opens the **Add port configuration** blade.</span></span>

  ![Configurazione delle porte][7]

2. <span data-ttu-id="3cf09-159">Nel pannello **Add port configuration** (Aggiungi configurazione porta) identificare la porta, il tipo di protocollo, gli indirizzi IP di origine consentiti e il tempo massimo per la richiesta.</span><span class="sxs-lookup"><span data-stu-id="3cf09-159">On **Add port configuration** blade, you identify the port, protocol type, allowed source IPs, and maximum request time.</span></span>

  <span data-ttu-id="3cf09-160">Gli indirizzi IP di origine consentiti sono gli intervalli IP a cui è consentito di ottenere l'accesso in seguito a una richiesta approvata.</span><span class="sxs-lookup"><span data-stu-id="3cf09-160">Allowed source IPs are the IP ranges allowed to get access upon an approved request.</span></span>

  <span data-ttu-id="3cf09-161">Il tempo massimo per la richiesta è l'intervallo di tempo massimo che può essere aperto da una porta specifica.</span><span class="sxs-lookup"><span data-stu-id="3cf09-161">Maximum request time is the maximum time window that a specific port can be opened.</span></span>

3. <span data-ttu-id="3cf09-162">Selezionare **OK**.</span><span class="sxs-lookup"><span data-stu-id="3cf09-162">Select **OK**.</span></span>

## <a name="requesting-access-to-a-vm"></a><span data-ttu-id="3cf09-163">Richiedere l'accesso a una macchina virtuale</span><span class="sxs-lookup"><span data-stu-id="3cf09-163">Requesting access to a VM</span></span>

<span data-ttu-id="3cf09-164">Per richiedere l'accesso a una macchina virtuale:</span><span class="sxs-lookup"><span data-stu-id="3cf09-164">To request access to a VM:</span></span>

1. <span data-ttu-id="3cf09-165">Nel pannello **Accesso Just-In-Time alla VM** selezionare la scheda **Configurata**.</span><span class="sxs-lookup"><span data-stu-id="3cf09-165">On the **Just in time VM access** blade, select the **Configured** tab.</span></span>
2. <span data-ttu-id="3cf09-166">In **Macchine virtuali** selezionare le macchine virtuali per cui abilitare l'accesso.</span><span class="sxs-lookup"><span data-stu-id="3cf09-166">Under **VMs**, select the VMs that you want to enable access.</span></span> <span data-ttu-id="3cf09-167">Verrà visualizzato un segno di spunta accanto a una macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="3cf09-167">This puts a checkmark next to a VM.</span></span>
3. <span data-ttu-id="3cf09-168">Selezionare **Richiedi accesso**.</span><span class="sxs-lookup"><span data-stu-id="3cf09-168">Select **Request access**.</span></span> <span data-ttu-id="3cf09-169">Verrà aperto il pannello **Richiedi accesso**.</span><span class="sxs-lookup"><span data-stu-id="3cf09-169">This opens the **Request access** blade.</span></span>

  ![Richiedere l'accesso a una macchina virtuale][4]

4. <span data-ttu-id="3cf09-171">Nel pannello **Richiedi accesso** è possibile configurare, per ogni macchina virtuale, le porte da aprire, l'indirizzo IP di origine per cui la porta è aperta e l'intervallo di tempo per l'apertura della porta.</span><span class="sxs-lookup"><span data-stu-id="3cf09-171">On the **Request access** blade, you configure for each VM the ports to open along with the source IP that the port is opened to and the time window for which the port is opened.</span></span> <span data-ttu-id="3cf09-172">È possibile richiedere l'accesso solo alle porte configurate nei criteri Just-In-Time.</span><span class="sxs-lookup"><span data-stu-id="3cf09-172">You can request access only to the ports that are configured in the just in time policy.</span></span> <span data-ttu-id="3cf09-173">Ogni porta ha un tempo massimo consentito, derivato dai criteri Just-In-Time.</span><span class="sxs-lookup"><span data-stu-id="3cf09-173">Each port has a maximum allowed time derived from the just in time policy.</span></span>
5. <span data-ttu-id="3cf09-174">Selezionare **Open ports** (Apri porte).</span><span class="sxs-lookup"><span data-stu-id="3cf09-174">Select **Open ports**.</span></span>

## <a name="editing-a-just-in-time-access-policy"></a><span data-ttu-id="3cf09-175">Modifica dei criteri di accesso Just-In-Time</span><span class="sxs-lookup"><span data-stu-id="3cf09-175">Editing a just in time access policy</span></span>

<span data-ttu-id="3cf09-176">È possibile modificare i criteri Just-In-Time esistenti di una macchina virtuale aggiungendo e configurando una nuova porta da aprire per la macchina virtuale o modificando qualsiasi altro parametro correlato a una porta già protetta.</span><span class="sxs-lookup"><span data-stu-id="3cf09-176">You can change a VM's existing just in time policy by adding and configuring a new port to open for that VM, or by changing any other parameter related to an already protected port.</span></span>

<span data-ttu-id="3cf09-177">Per modificare i criteri Just-In-Time esistenti di una macchina virtuale, viene usata la scheda **Configurata**:</span><span class="sxs-lookup"><span data-stu-id="3cf09-177">In order to edit an existing just in time policy of a VM, the **Configured** tab is used:</span></span>

1. <span data-ttu-id="3cf09-178">In **Macchine virtuali** selezionare una macchina virtuale a cui aggiungere una porta facendo clic sui tre puntini nella riga della macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="3cf09-178">Under **VMs**, select a VM to add a port to by clicking on the three dots within the row for that VM.</span></span> <span data-ttu-id="3cf09-179">Verrà aperto un menu.</span><span class="sxs-lookup"><span data-stu-id="3cf09-179">This opens a menu.</span></span>
2. <span data-ttu-id="3cf09-180">Selezionare **Modifica** nel menu.</span><span class="sxs-lookup"><span data-stu-id="3cf09-180">Select **Edit** in the menu.</span></span> <span data-ttu-id="3cf09-181">Verrà visualizzato il pannello **JIT VM access configuration** (Configurazione accesso Just-In-Time alla VM).</span><span class="sxs-lookup"><span data-stu-id="3cf09-181">This opens the **JIT VM access configuration** blade.</span></span>

  ![Modificare i criteri][8]

3. <span data-ttu-id="3cf09-183">Nel pannello **JIT VM access configuration** (Configurazione accesso Just-In-Time alla VM) è possibile modificare le impostazioni esistenti di una porta già protetta facendo clic sulla porta desiderata oppure è possibile selezionare **Aggiungi**.</span><span class="sxs-lookup"><span data-stu-id="3cf09-183">On the **JIT VM access configuration** blade, you can either edit the existing settings of an already protected port by clicking on its port, or you can select **Add**.</span></span> <span data-ttu-id="3cf09-184">Verrà aperto il pannello **Add port configuration** (Aggiungi configurazione porta).</span><span class="sxs-lookup"><span data-stu-id="3cf09-184">This opens the **Add port configuration** blade.</span></span>

  ![Aggiungere una porta][7]

4. <span data-ttu-id="3cf09-186">Nel pannello **Add port configuration** (Aggiungi configurazione porta) identificare la porta, il tipo di protocollo, gli indirizzi IP di origine consentiti e il tempo massimo per la richiesta.</span><span class="sxs-lookup"><span data-stu-id="3cf09-186">On **Add port configuration** blade identify the port, protocol type, allowed source IPs, and maximum request time.</span></span>
5. <span data-ttu-id="3cf09-187">Selezionare **OK**.</span><span class="sxs-lookup"><span data-stu-id="3cf09-187">Select **OK**.</span></span>
6. <span data-ttu-id="3cf09-188">Selezionare **Salva**.</span><span class="sxs-lookup"><span data-stu-id="3cf09-188">Select **Save**.</span></span>

## <a name="auditing-just-in-time-access-activity"></a><span data-ttu-id="3cf09-189">Controllo delle attività di accesso Just-in-Time</span><span class="sxs-lookup"><span data-stu-id="3cf09-189">Auditing just in time access activity</span></span>

<span data-ttu-id="3cf09-190">È possibile ottenere informazioni approfondite sulle attività delle macchine virtuali tramite la funzionalità Ricerca log.</span><span class="sxs-lookup"><span data-stu-id="3cf09-190">You can gain insights into VM activities using log search.</span></span> <span data-ttu-id="3cf09-191">Per visualizzare i log:</span><span class="sxs-lookup"><span data-stu-id="3cf09-191">To view logs:</span></span>

1. <span data-ttu-id="3cf09-192">Nel pannello **Accesso Just-In-Time alla VM** selezionare la scheda **Configurata**.</span><span class="sxs-lookup"><span data-stu-id="3cf09-192">On the **Just in time VM access** blade, select the **Configured** tab.</span></span>
2. <span data-ttu-id="3cf09-193">In **Macchine virtuali** selezionare una macchina virtuale per cui visualizzare le informazioni facendo clic sui tre puntini nella riga della macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="3cf09-193">Under **VMs**, select a VM to view information about by clicking on the three dots within the row for that VM.</span></span> <span data-ttu-id="3cf09-194">Verrà aperto un menu.</span><span class="sxs-lookup"><span data-stu-id="3cf09-194">This opens a menu.</span></span>
3. <span data-ttu-id="3cf09-195">Selezionare **Log attività** nel menu.</span><span class="sxs-lookup"><span data-stu-id="3cf09-195">Select **Activity Log** in the menu.</span></span> <span data-ttu-id="3cf09-196">Verrà aperto il pannello **Log attività**.</span><span class="sxs-lookup"><span data-stu-id="3cf09-196">This opens the **Activity log** blade.</span></span>

![Selezionare il log attività][9]

<span data-ttu-id="3cf09-198">Il pannello **Log attività** fornisce una visualizzazione filtrata delle operazioni precedenti per la macchina virtuale, con data, ora e sottoscrizione.</span><span class="sxs-lookup"><span data-stu-id="3cf09-198">The **Activity log** blade provides a filtered view of previous operations for that VM along with time, date, and subscription.</span></span>

![Visualizzare il log attività][5]

<span data-ttu-id="3cf09-200">È possibile scaricare le informazioni del log selezionando **Fare clic qui per scaricare tutti gli elementi come file CSV**.</span><span class="sxs-lookup"><span data-stu-id="3cf09-200">You can download the log information by selecting **Click here to download all the items as CSV**.</span></span>

<span data-ttu-id="3cf09-201">Modificare i filtri e selezionare **Applica** per creare un log ed eseguire ricerche.</span><span class="sxs-lookup"><span data-stu-id="3cf09-201">Modify the filters and select **Apply** to create a search and log.</span></span>

## <a name="using-just-in-time-vm-access-via-powershell"></a><span data-ttu-id="3cf09-202">Uso dell'accesso Just-In-Time alle macchine virtuali tramite PowerShell</span><span class="sxs-lookup"><span data-stu-id="3cf09-202">Using just in time VM access via PowerShell</span></span>

<span data-ttu-id="3cf09-203">Per usare la soluzione Just-In-Time tramite PowerShell, verificare di disporre della [versione più recente](/powershell/azure/install-azurerm-ps) di Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="3cf09-203">In order to use the just in time solution via PowerShell, make sure you have the [latest](/powershell/azure/install-azurerm-ps) Azure PowerShell version.</span></span>
<span data-ttu-id="3cf09-204">È quindi necessario installare la [versione più recente](https://www.powershellgallery.com/packages/Azure-Security-Center/0.0.12) del Centro sicurezza di Azure da PowerShell Gallery.</span><span class="sxs-lookup"><span data-stu-id="3cf09-204">Once you do, you need to install the [latest](https://www.powershellgallery.com/packages/Azure-Security-Center/0.0.12) Azure Security Center from the PowerShell gallery.</span></span>

### <a name="configuring-a-just-in-time-policy-for-a-vm"></a><span data-ttu-id="3cf09-205">Configurazione dei criteri Just-In-Time per una macchina virtuale</span><span class="sxs-lookup"><span data-stu-id="3cf09-205">Configuring a just in time policy for a VM</span></span>

<span data-ttu-id="3cf09-206">Per configurare i criteri Just-In-Time in una macchina virtuale specifica, è necessario eseguire il comando seguente nella sessione di PowerShell: Set-ASCJITAccessPolicy.</span><span class="sxs-lookup"><span data-stu-id="3cf09-206">To configure a just in time policy on a specific VM, you need to run this command in your PowerShell session: Set-ASCJITAccessPolicy.</span></span>
<span data-ttu-id="3cf09-207">Per altre informazioni, vedere la documentazione del cmdlet.</span><span class="sxs-lookup"><span data-stu-id="3cf09-207">Follow the cmdlet documentation to learn more.</span></span>

### <a name="requesting-access-to-a-vm"></a><span data-ttu-id="3cf09-208">Richiedere l'accesso a una macchina virtuale</span><span class="sxs-lookup"><span data-stu-id="3cf09-208">Requesting access to a VM</span></span>

<span data-ttu-id="3cf09-209">Per accedere a una macchina virtuale specifica che è protetta con la soluzione Just-In-Time, è necessario eseguire il comando seguente nella sessione di PowerShell: Invoke-ASCJITAccess.</span><span class="sxs-lookup"><span data-stu-id="3cf09-209">To access a specific VM that is protected with the just in time solution, you need to run this command in your PowerShell session: Invoke-ASCJITAccess.</span></span>
<span data-ttu-id="3cf09-210">Per altre informazioni, vedere la documentazione del cmdlet.</span><span class="sxs-lookup"><span data-stu-id="3cf09-210">Follow the cmdlet documentation to learn more.</span></span>

## <a name="next-steps"></a><span data-ttu-id="3cf09-211">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="3cf09-211">Next steps</span></span>
<span data-ttu-id="3cf09-212">In questo articolo è stato illustrato come usare l'accesso JIT (Just-in-Time) alle macchine virtuali in Centro sicurezza per controllare l'accesso alle macchine virtuali di Azure.</span><span class="sxs-lookup"><span data-stu-id="3cf09-212">In this article, you learned how just in time VM access in Security Center helps you control access to your Azure virtual machines.</span></span>

<span data-ttu-id="3cf09-213">Per altre informazioni sul Centro sicurezza, vedere gli argomenti seguenti:</span><span class="sxs-lookup"><span data-stu-id="3cf09-213">To learn more about Security Center, see the following:</span></span>

- <span data-ttu-id="3cf09-214">[Impostazione dei criteri di sicurezza](security-center-policies.md): informazioni su come configurare i criteri di sicurezza per le sottoscrizioni e i gruppi di risorse di Azure.</span><span class="sxs-lookup"><span data-stu-id="3cf09-214">[Setting security policies](security-center-policies.md) — Learn how to configure security policies for your Azure subscriptions and resource groups.</span></span>
- <span data-ttu-id="3cf09-215">[Gestione delle raccomandazioni di sicurezza](security-center-recommendations.md): informazioni sul modo in cui le raccomandazioni semplificano la protezione delle risorse di Azure.</span><span class="sxs-lookup"><span data-stu-id="3cf09-215">[Managing security recommendations](security-center-recommendations.md) — Learn how recommendations help you protect your Azure resources.</span></span>
- <span data-ttu-id="3cf09-216">[Monitoraggio dell'integrità della sicurezza](security-center-monitoring.md): informazioni su come monitorare l'integrità delle risorse di Azure.</span><span class="sxs-lookup"><span data-stu-id="3cf09-216">[Security health monitoring](security-center-monitoring.md) — Learn how to monitor the health of your Azure resources.</span></span>
- <span data-ttu-id="3cf09-217">[Gestione e risposta agli avvisi di sicurezza](security-center-managing-and-responding-alerts.md): informazioni su come gestire e rispondere agli avvisi di sicurezza.</span><span class="sxs-lookup"><span data-stu-id="3cf09-217">[Managing and responding to security alerts](security-center-managing-and-responding-alerts.md) — Learn how to manage and respond to security alerts.</span></span>
- <span data-ttu-id="3cf09-218">[Monitoraggio delle soluzioni dei partner](security-center-partner-solutions.md): informazioni su come monitorare l'integrità delle soluzioni dei partner.</span><span class="sxs-lookup"><span data-stu-id="3cf09-218">[Monitoring partner solutions](security-center-partner-solutions.md) — Learn how to monitor the health status of your partner solutions.</span></span>
- <span data-ttu-id="3cf09-219">[Domande frequenti sul Centro sicurezza](security-center-faq.md): leggere le domande frequenti sull'uso del servizio.</span><span class="sxs-lookup"><span data-stu-id="3cf09-219">[Security Center FAQ](security-center-faq.md) — Find frequently asked questions about using the service.</span></span>
- <span data-ttu-id="3cf09-220">[Blog sulla sicurezza di Azure](https://blogs.msdn.microsoft.com/azuresecurity/) : post di blog sulla sicurezza e sulla conformità di Azure.</span><span class="sxs-lookup"><span data-stu-id="3cf09-220">[Azure Security blog](https://blogs.msdn.microsoft.com/azuresecurity/) — Find blog posts about Azure security and compliance.</span></span>


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

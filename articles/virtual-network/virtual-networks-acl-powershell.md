---
title: elenchi di controllo di accesso all'endpoint Azure aaaManage | PowerShell | Classico | Documenti Microsoft
description: Informazioni su come toomanage ACL con PowerShell
services: virtual-network
documentationcenter: na
author: jimdial
manager: carmonm
editor: tysonn
ms.assetid: c84e40af-f351-4572-b3f0-d572d46bafe7
ms.service: virtual-network
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 03/15/2016
ms.author: jdial
ms.openlocfilehash: a7ca241ea108a266085bfb689b742d781e58da1c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="manage-endpoint-access-control-lists-using-powershell-in-hello-classic-deployment-model"></a><span data-ttu-id="32ac4-103">Gestire elenchi di controllo di accesso endpoint tramite PowerShell nel modello di distribuzione classica hello</span><span class="sxs-lookup"><span data-stu-id="32ac4-103">Manage endpoint access control lists using PowerShell in hello classic deployment model</span></span>
<span data-ttu-id="32ac4-104">È possibile creare e gestire elenchi controllo accesso rete (ACL) per gli endpoint tramite Azure PowerShell o nel portale di gestione di hello.</span><span class="sxs-lookup"><span data-stu-id="32ac4-104">You can create and manage Network Access Control Lists (ACLs) for endpoints by using Azure PowerShell or in hello Management Portal.</span></span> <span data-ttu-id="32ac4-105">Questo argomento illustra le procedure per le attività comuni che è possibile eseguire per tali elenchi usando PowerShell.</span><span class="sxs-lookup"><span data-stu-id="32ac4-105">In this topic, you'll find procedures for ACL common tasks that you can complete using PowerShell.</span></span> <span data-ttu-id="32ac4-106">Per l'elenco hello di Azure PowerShell cmdlet vedere [cmdlet di gestione di Azure](http://go.microsoft.com/fwlink/?LinkId=317721).</span><span class="sxs-lookup"><span data-stu-id="32ac4-106">For hello list of Azure PowerShell cmdlets see [Azure Management Cmdlets](http://go.microsoft.com/fwlink/?LinkId=317721).</span></span> <span data-ttu-id="32ac4-107">Per altre informazioni sugli elenchi di controllo di accesso, vedere l'articolo relativo alla [definizione di un elenco di controllo di accesso di rete](virtual-networks-acl.md).</span><span class="sxs-lookup"><span data-stu-id="32ac4-107">For more information about ACLs, see [What is a Network Access Control List (ACL)?](virtual-networks-acl.md).</span></span> <span data-ttu-id="32ac4-108">Se si desidera toomanage gli ACL usando hello portale di gestione, vedere [come configurare gli endpoint di tooSet tooa macchina virtuale](../virtual-machines/windows/classic/setup-endpoints.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="32ac4-108">If you want toomanage your ACLs by using hello Management Portal, see [How tooSet Up Endpoints tooa Virtual Machine](../virtual-machines/windows/classic/setup-endpoints.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json).</span></span>

## <a name="manage-network-acls-by-using-azure-powershell"></a><span data-ttu-id="32ac4-109">Gestire gli elenchi di controllo di accesso di rete tramite Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="32ac4-109">Manage Network ACLs by using Azure PowerShell</span></span>
<span data-ttu-id="32ac4-110">È possibile utilizzare toocreate cmdlet PowerShell di Azure, rimuovere e configurare (set) elenchi controllo accesso rete (ACL).</span><span class="sxs-lookup"><span data-stu-id="32ac4-110">You can use Azure PowerShell cmdlets toocreate, remove, and configure (set) Network Access Control Lists (ACLs).</span></span> <span data-ttu-id="32ac4-111">Sono stati inclusi alcuni esempi di alcuni dei modi hello che è possibile configurare un ACL tramite PowerShell.</span><span class="sxs-lookup"><span data-stu-id="32ac4-111">We've included a few examples of some of hello ways you can configure an ACL using PowerShell.</span></span>

<span data-ttu-id="32ac4-112">un elenco completo dei cmdlet di PowerShell ACL hello tooretrieve, è possibile utilizzare uno dei seguenti hello:</span><span class="sxs-lookup"><span data-stu-id="32ac4-112">tooretrieve a complete list of hello ACL PowerShell cmdlets, you can use either of hello following:</span></span>

    Get-Help *AzureACL*
    Get-Command -Noun AzureACLConfig

### <a name="create-a-network-acl-with-rules-that-permit-access-from-a-remote-subnet"></a><span data-ttu-id="32ac4-113">Creare un elenco di controllo di accesso di rete con regole che consentano l'accesso da una subnet remota</span><span class="sxs-lookup"><span data-stu-id="32ac4-113">Create a Network ACL with rules that permit access from a remote subnet</span></span>
<span data-ttu-id="32ac4-114">esempio Hello riportato di seguito viene illustrato un toocreate modo un nuovo ACL contenente regole.</span><span class="sxs-lookup"><span data-stu-id="32ac4-114">hello example below illustrates a way toocreate a new ACL that contains rules.</span></span> <span data-ttu-id="32ac4-115">Viene quindi applicato l'ACL tooa endpoint della macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="32ac4-115">This ACL is then applied tooa virtual machine endpoint.</span></span> <span data-ttu-id="32ac4-116">regole ACL Hello nel seguente esempio hello consentirà l'accesso da una subnet remota.</span><span class="sxs-lookup"><span data-stu-id="32ac4-116">hello ACL rules in hello example below will allow access from a remote subnet.</span></span> <span data-ttu-id="32ac4-117">toocreate un nuovo ACL di rete con regole Consenti per una subnet remota, aprire Azure PowerShell ISE.</span><span class="sxs-lookup"><span data-stu-id="32ac4-117">toocreate a new Network ACL with permit rules for a remote subnet, open an Azure PowerShell ISE.</span></span> <span data-ttu-id="32ac4-118">Copiare e incollare hello script seguente, configurando script hello con i valori desiderati e quindi eseguire script hello.</span><span class="sxs-lookup"><span data-stu-id="32ac4-118">Copy and paste hello script below, configuring hello script with your own values, and then run hello script.</span></span>

1. <span data-ttu-id="32ac4-119">Creare hello nuovo oggetto ACL di rete.</span><span class="sxs-lookup"><span data-stu-id="32ac4-119">Create hello new network ACL object.</span></span>
   
        $acl1 = New-AzureAclConfig
2. <span data-ttu-id="32ac4-120">Impostare una regola che consenta l'accesso da una subnet remota.</span><span class="sxs-lookup"><span data-stu-id="32ac4-120">Set a rule that permits access from a remote subnet.</span></span> <span data-ttu-id="32ac4-121">Nell'esempio hello seguente, si imposta regola *100* (che ha la priorità sulla regola 200 e versioni successiva) della subnet remota hello tooallow *10.0.0.0/8* accedere toohello endpoint della macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="32ac4-121">In hello example below, you set rule *100* (which has priority over rule 200 and higher) tooallow hello remote subnet *10.0.0.0/8* access toohello virtual machine endpoint.</span></span> <span data-ttu-id="32ac4-122">Sostituire i valori hello con requisiti di configurazione.</span><span class="sxs-lookup"><span data-stu-id="32ac4-122">Replace hello values with your own configuration requirements.</span></span> <span data-ttu-id="32ac4-123">nome Hello "SharePoint ACL config" deve essere sostituito con un nome di hello che si desidera toocall questa regola.</span><span class="sxs-lookup"><span data-stu-id="32ac4-123">hello name "SharePoint ACL config" should be replaced with hello friendly name that you want toocall this rule.</span></span>
   
        Set-AzureAclConfig –AddRule –ACL $acl1 –Order 100 `
            –Action permit –RemoteSubnet "10.0.0.0/8" `
            –Description "SharePoint ACL config"
3. <span data-ttu-id="32ac4-124">Per altre regole, ripetere il cmdlet hello, sostituendo i valori hello con requisiti di configurazione.</span><span class="sxs-lookup"><span data-stu-id="32ac4-124">For additional rules, repeat hello cmdlet, replacing hello values with your own configuration requirements.</span></span> <span data-ttu-id="32ac4-125">Essere certi toochange hello regola numero tooreflect hello ordine in cui si desidera hello regole toobe applicato.</span><span class="sxs-lookup"><span data-stu-id="32ac4-125">Be sure toochange hello rule number Order tooreflect hello order in which you want hello rules toobe applied.</span></span> <span data-ttu-id="32ac4-126">Hello regola più basso ha la precedenza sul numero più alto hello.</span><span class="sxs-lookup"><span data-stu-id="32ac4-126">hello lower rule number takes precedence over hello higher number.</span></span>
   
        Set-AzureAclConfig –AddRule –ACL $acl1 –Order 200 `
            –Action permit –RemoteSubnet "157.0.0.0/8" `
            –Description "web frontend ACL config"
4. <span data-ttu-id="32ac4-127">Successivamente, è possibile creare un nuovo endpoint (Add) o impostare hello ACL per un endpoint esistente (Set).</span><span class="sxs-lookup"><span data-stu-id="32ac4-127">Next, you can either create a new endpoint (Add) or set hello ACL for an existing endpoint (Set).</span></span> <span data-ttu-id="32ac4-128">In questo esempio, si aggiungerà che un nuovo endpoint della macchina virtuale denominata "web" e aggiornamento endpoint della macchina virtuale hello con hello impostazioni ACL.</span><span class="sxs-lookup"><span data-stu-id="32ac4-128">In this example, we will add a new virtual machine endpoint called "web" and update hello virtual machine endpoint with hello ACL settings.</span></span>
   
        Get-AzureVM –ServiceName $serviceName –Name $vmName `
        | Add-AzureEndpoint –Name "web" –Protocol tcp –Localport 80 - PublicPort 80 –ACL $acl1 `
        | Update-AzureVM
5. <span data-ttu-id="32ac4-129">Successivamente, combinare i cmdlet di hello ed eseguire script hello.</span><span class="sxs-lookup"><span data-stu-id="32ac4-129">Next, combine hello cmdlets and run hello script.</span></span> <span data-ttu-id="32ac4-130">In questo esempio hello cmdlet combinati sarebbe simile al seguente:</span><span class="sxs-lookup"><span data-stu-id="32ac4-130">For this example, hello combined cmdlets would look like this:</span></span>
   
        $acl1 = New-AzureAclConfig
        Set-AzureAclConfig –AddRule –ACL $acl1 –Order 100 `
            –Action permit –RemoteSubnet "10.0.0.0/8" `
            –Description "Sharepoint ACL config"
        Set-AzureAclConfig –AddRule –ACL $acl1 –Order 200 `
            –Action permit –RemoteSubnet "157.0.0.0/8" `
            –Description "web frontend ACL config"
        Get-AzureVM –ServiceName $serviceName –Name $vmName `
        |Add-AzureEndpoint –Name "web" –Protocol tcp –Localport 80 - PublicPort 80 –ACL $acl1 `
        |Update-AzureVM

### <a name="remove-a-network-acl-rule-that-permits-access-from-a-remote-subnet"></a><span data-ttu-id="32ac4-131">Rimuovere una regola dell'elenco di controllo di accesso che consente l'accesso da una subnet remota</span><span class="sxs-lookup"><span data-stu-id="32ac4-131">Remove a Network ACL rule that permits access from a remote subnet</span></span>
<span data-ttu-id="32ac4-132">esempio Hello riportato di seguito viene illustrato un tooremove modo una regola ACL di rete.</span><span class="sxs-lookup"><span data-stu-id="32ac4-132">hello example below illustrates a way tooremove a network ACL rule.</span></span>  <span data-ttu-id="32ac4-133">le regole di tooremove una regola ACL di rete con l'autorizzazione per una subnet remota, aprire Azure PowerShell ISE.</span><span class="sxs-lookup"><span data-stu-id="32ac4-133">tooremove a Network ACL rule with permit rules for a remote subnet, open an Azure PowerShell ISE.</span></span> <span data-ttu-id="32ac4-134">Copiare e incollare hello script seguente, configurando script hello con i valori desiderati e quindi eseguire script hello.</span><span class="sxs-lookup"><span data-stu-id="32ac4-134">Copy and paste hello script below, configuring hello script with your own values, and then run hello script.</span></span>

1. <span data-ttu-id="32ac4-135">Primo passaggio è l'oggetto ACL di rete di hello tooget per l'endpoint della macchina virtuale hello.</span><span class="sxs-lookup"><span data-stu-id="32ac4-135">First step is tooget hello Network ACL object for hello virtual machine endpoint.</span></span> <span data-ttu-id="32ac4-136">Verrà rimossa regola ACL hello.</span><span class="sxs-lookup"><span data-stu-id="32ac4-136">You'll then remove hello ACL rule.</span></span> <span data-ttu-id="32ac4-137">In questo caso, la si rimuoverà in base all'ID regola.</span><span class="sxs-lookup"><span data-stu-id="32ac4-137">In this case, we are removing it by rule ID.</span></span> <span data-ttu-id="32ac4-138">Questo verrà rimosso solo hello l'ID regola 0 dall'ACL hello.</span><span class="sxs-lookup"><span data-stu-id="32ac4-138">This will only remove hello rule ID 0 from hello ACL.</span></span> <span data-ttu-id="32ac4-139">Non rimuove oggetto ACL hello dall'endpoint della macchina virtuale hello.</span><span class="sxs-lookup"><span data-stu-id="32ac4-139">It does not remove hello ACL object from hello virtual machine endpoint.</span></span>
   
        Get-AzureVM –ServiceName $serviceName –Name $vmName `
        | Get-AzureAclConfig –EndpointName "web" `
        | Set-AzureAclConfig –RemoveRule –ID 0 –ACL $acl1
2. <span data-ttu-id="32ac4-140">Successivamente, è necessario applicare l'endpoint della macchina virtuale toohello oggetto ACL di rete hello e aggiornare la macchina virtuale hello.</span><span class="sxs-lookup"><span data-stu-id="32ac4-140">Next, you must apply hello Network ACL object toohello virtual machine endpoint and update hello virtual machine.</span></span>
   
        Get-AzureVM –ServiceName $serviceName –Name $vmName `
        | Set-AzureEndpoint –ACL $acl1 –Name "web" `
        | Update-AzureVM

### <a name="remove-a-network-acl-from-a-virtual-machine-endpoint"></a><span data-ttu-id="32ac4-141">Rimuovere un elenco di controllo di accesso di rete dall'endpoint di una macchina virtuale</span><span class="sxs-lookup"><span data-stu-id="32ac4-141">Remove a Network ACL from a virtual machine endpoint</span></span>
<span data-ttu-id="32ac4-142">In alcuni scenari, è possibile tooremove un oggetto ACL di rete da un endpoint della macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="32ac4-142">In certain scenarios, you might want tooremove a Network ACL object from a virtual machine endpoint.</span></span> <span data-ttu-id="32ac4-143">toodo che, aprire Azure PowerShell ISE.</span><span class="sxs-lookup"><span data-stu-id="32ac4-143">toodo that, open an Azure PowerShell ISE.</span></span> <span data-ttu-id="32ac4-144">Copiare e incollare hello script seguente, configurando script hello con i valori desiderati e quindi eseguire script hello.</span><span class="sxs-lookup"><span data-stu-id="32ac4-144">Copy and paste hello script below, configuring hello script with your own values, and then run hello script.</span></span>

        Get-AzureVM –ServiceName $serviceName –Name $vmName `
        | Remove-AzureAclConfig –EndpointName "web" `
        | Update-AzureVM

## <a name="next-steps"></a><span data-ttu-id="32ac4-145">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="32ac4-145">Next steps</span></span>
[<span data-ttu-id="32ac4-146">Che cos'è un elenco di controllo di accesso di rete?</span><span class="sxs-lookup"><span data-stu-id="32ac4-146">What is a Network Access Control List (ACL)?</span></span>](virtual-networks-acl.md)


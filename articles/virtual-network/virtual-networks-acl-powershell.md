---
title: Gestire elenchi di controllo di accesso di endpoint di Azure | PowerShell | Modello di distribuzione classica | Documentazione Microsoft
description: Informazioni su come gestire gli elenchi di controllo di accesso con PowerShell
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
ms.openlocfilehash: c3476908447380ccd7e8b9c0f1c2a55ae763cc1e
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="manage-endpoint-access-control-lists-using-powershell-in-the-classic-deployment-model"></a><span data-ttu-id="564e9-103">Gestire elenchi di controllo di accesso di endpoint con PowerShell nel modello di distribuzione classica</span><span class="sxs-lookup"><span data-stu-id="564e9-103">Manage endpoint access control lists using PowerShell in the classic deployment model</span></span>
<span data-ttu-id="564e9-104">È possibile creare e gestire gli elenchi di controllo di accesso di rete per gli endpoint tramite Azure PowerShell o nel portale di gestione.</span><span class="sxs-lookup"><span data-stu-id="564e9-104">You can create and manage Network Access Control Lists (ACLs) for endpoints by using Azure PowerShell or in the Management Portal.</span></span> <span data-ttu-id="564e9-105">Questo argomento illustra le procedure per le attività comuni che è possibile eseguire per tali elenchi usando PowerShell.</span><span class="sxs-lookup"><span data-stu-id="564e9-105">In this topic, you'll find procedures for ACL common tasks that you can complete using PowerShell.</span></span> <span data-ttu-id="564e9-106">Per l'elenco dei cmdlet di Azure PowerShell, vedere l'articolo relativo ai [cmdlet di gestione di Azure](http://go.microsoft.com/fwlink/?LinkId=317721).</span><span class="sxs-lookup"><span data-stu-id="564e9-106">For the list of Azure PowerShell cmdlets see [Azure Management Cmdlets](http://go.microsoft.com/fwlink/?LinkId=317721).</span></span> <span data-ttu-id="564e9-107">Per altre informazioni sugli elenchi di controllo di accesso, vedere l'articolo relativo alla [definizione di un elenco di controllo di accesso di rete](virtual-networks-acl.md).</span><span class="sxs-lookup"><span data-stu-id="564e9-107">For more information about ACLs, see [What is a Network Access Control List (ACL)?](virtual-networks-acl.md).</span></span> <span data-ttu-id="564e9-108">Se si intende gestire gli elenchi di controllo di accesso tramite il portale di gestione, vedere [Come configurare gli endpoint in una macchina virtuale](../virtual-machines/windows/classic/setup-endpoints.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="564e9-108">If you want to manage your ACLs by using the Management Portal, see [How to Set Up Endpoints to a Virtual Machine](../virtual-machines/windows/classic/setup-endpoints.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json).</span></span>

## <a name="manage-network-acls-by-using-azure-powershell"></a><span data-ttu-id="564e9-109">Gestire gli elenchi di controllo di accesso di rete tramite Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="564e9-109">Manage Network ACLs by using Azure PowerShell</span></span>
<span data-ttu-id="564e9-110">È possibile usare i cmdlet di Azure PowerShell per creare, rimuovere e configurare (impostare) gli elenchi di controllo di accesso di rete.</span><span class="sxs-lookup"><span data-stu-id="564e9-110">You can use Azure PowerShell cmdlets to create, remove, and configure (set) Network Access Control Lists (ACLs).</span></span> <span data-ttu-id="564e9-111">Di seguito sono riportati alcuni esempi di come configurare un elenco di controllo di accesso tramite PowerShell.</span><span class="sxs-lookup"><span data-stu-id="564e9-111">We've included a few examples of some of the ways you can configure an ACL using PowerShell.</span></span>

<span data-ttu-id="564e9-112">Per recuperare un elenco completo dei cmdlet PowerShell per gli elenchi di controllo di accesso, è possibile usare uno dei comandi seguenti:</span><span class="sxs-lookup"><span data-stu-id="564e9-112">To retrieve a complete list of the ACL PowerShell cmdlets, you can use either of the following:</span></span>

    Get-Help *AzureACL*
    Get-Command -Noun AzureACLConfig

### <a name="create-a-network-acl-with-rules-that-permit-access-from-a-remote-subnet"></a><span data-ttu-id="564e9-113">Creare un elenco di controllo di accesso di rete con regole che consentano l'accesso da una subnet remota</span><span class="sxs-lookup"><span data-stu-id="564e9-113">Create a Network ACL with rules that permit access from a remote subnet</span></span>
<span data-ttu-id="564e9-114">L'esempio seguente illustra come creare un nuovo elenco di controllo di accesso contenente regole.</span><span class="sxs-lookup"><span data-stu-id="564e9-114">The example below illustrates a way to create a new ACL that contains rules.</span></span> <span data-ttu-id="564e9-115">Tale elenco viene quindi applicato all'endpoint di una macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="564e9-115">This ACL is then applied to a virtual machine endpoint.</span></span> <span data-ttu-id="564e9-116">Le regole dell'elenco di controllo di accesso nell'esempio seguente consentiranno l'accesso da una subnet remota.</span><span class="sxs-lookup"><span data-stu-id="564e9-116">The ACL rules in the example below will allow access from a remote subnet.</span></span> <span data-ttu-id="564e9-117">Per creare un nuovo elenco di controllo di accesso di rete con regole di autorizzazione per una subnet remota, aprire un'istanza di Azure PowerShell ISE.</span><span class="sxs-lookup"><span data-stu-id="564e9-117">To create a new Network ACL with permit rules for a remote subnet, open an Azure PowerShell ISE.</span></span> <span data-ttu-id="564e9-118">Copiare e incollare lo script seguente, configurandolo con valori personalizzati, e quindi eseguirlo.</span><span class="sxs-lookup"><span data-stu-id="564e9-118">Copy and paste the script below, configuring the script with your own values, and then run the script.</span></span>

1. <span data-ttu-id="564e9-119">Creare il nuovo oggetto elenco di controllo di accesso (ACL) di rete.</span><span class="sxs-lookup"><span data-stu-id="564e9-119">Create the new network ACL object.</span></span>
   
        $acl1 = New-AzureAclConfig
2. <span data-ttu-id="564e9-120">Impostare una regola che consenta l'accesso da una subnet remota.</span><span class="sxs-lookup"><span data-stu-id="564e9-120">Set a rule that permits access from a remote subnet.</span></span> <span data-ttu-id="564e9-121">Nell'esempio seguente si imposta la regola *100* (che ha la priorità sulla regola 200 e superiori) per consentire alla subnet remota *10.0.0.0/8* di accedere all'endpoint della macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="564e9-121">In the example below, you set rule *100* (which has priority over rule 200 and higher) to allow the remote subnet *10.0.0.0/8* access to the virtual machine endpoint.</span></span> <span data-ttu-id="564e9-122">Sostituire i valori con quelli necessari per la propria configurazione.</span><span class="sxs-lookup"><span data-stu-id="564e9-122">Replace the values with your own configuration requirements.</span></span> <span data-ttu-id="564e9-123">Il nome "SharePoint ACL config" deve essere sostituito dal nome descrittivo che si intende assegnare alla regola.</span><span class="sxs-lookup"><span data-stu-id="564e9-123">The name "SharePoint ACL config" should be replaced with the friendly name that you want to call this rule.</span></span>
   
        Set-AzureAclConfig –AddRule –ACL $acl1 –Order 100 `
            –Action permit –RemoteSubnet "10.0.0.0/8" `
            –Description "SharePoint ACL config"
3. <span data-ttu-id="564e9-124">Per aggiungere altre regole, ripetere il cmdlet sostituendo i valori con quelli necessari per la propria configurazione.</span><span class="sxs-lookup"><span data-stu-id="564e9-124">For additional rules, repeat the cmdlet, replacing the values with your own configuration requirements.</span></span> <span data-ttu-id="564e9-125">Ricordarsi di modificare il numero di regola per Order in base all'ordine in cui devono essere applicate le regole.</span><span class="sxs-lookup"><span data-stu-id="564e9-125">Be sure to change the rule number Order to reflect the order in which you want the rules to be applied.</span></span> <span data-ttu-id="564e9-126">La regola con il numero più basso ha la precedenza sulla regola con il numero più alto.</span><span class="sxs-lookup"><span data-stu-id="564e9-126">The lower rule number takes precedence over the higher number.</span></span>
   
        Set-AzureAclConfig –AddRule –ACL $acl1 –Order 200 `
            –Action permit –RemoteSubnet "157.0.0.0/8" `
            –Description "web frontend ACL config"
4. <span data-ttu-id="564e9-127">È quindi possibile creare un nuovo endpoint (Add) o impostare l'elenco di controllo di accesso per un endpoint esistente (Set).</span><span class="sxs-lookup"><span data-stu-id="564e9-127">Next, you can either create a new endpoint (Add) or set the ACL for an existing endpoint (Set).</span></span> <span data-ttu-id="564e9-128">In questo esempio si aggiungerà un nuovo endpoint di macchina virtuale denominato "web" e si aggiornerà l'endpoint con le impostazioni dell'elenco di controllo di accesso.</span><span class="sxs-lookup"><span data-stu-id="564e9-128">In this example, we will add a new virtual machine endpoint called "web" and update the virtual machine endpoint with the ACL settings.</span></span>
   
        Get-AzureVM –ServiceName $serviceName –Name $vmName `
        | Add-AzureEndpoint –Name "web" –Protocol tcp –Localport 80 - PublicPort 80 –ACL $acl1 `
        | Update-AzureVM
5. <span data-ttu-id="564e9-129">Si combineranno quindi i cmdlet e si eseguirà lo script.</span><span class="sxs-lookup"><span data-stu-id="564e9-129">Next, combine the cmdlets and run the script.</span></span> <span data-ttu-id="564e9-130">Per questo esempio i cmdlet combinati saranno simili ai seguenti:</span><span class="sxs-lookup"><span data-stu-id="564e9-130">For this example, the combined cmdlets would look like this:</span></span>
   
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

### <a name="remove-a-network-acl-rule-that-permits-access-from-a-remote-subnet"></a><span data-ttu-id="564e9-131">Rimuovere una regola dell'elenco di controllo di accesso che consente l'accesso da una subnet remota</span><span class="sxs-lookup"><span data-stu-id="564e9-131">Remove a Network ACL rule that permits access from a remote subnet</span></span>
<span data-ttu-id="564e9-132">L'esempio seguente illustra come rimuovere una regola dell'elenco di controllo di accesso di rete.</span><span class="sxs-lookup"><span data-stu-id="564e9-132">The example below illustrates a way to remove a network ACL rule.</span></span>  <span data-ttu-id="564e9-133">Per rimuovere una regola dell'elenco di controllo di accesso di rete con regole di autorizzazione per una subnet remota, aprire un'istanza di Azure PowerShell ISE.</span><span class="sxs-lookup"><span data-stu-id="564e9-133">To remove a Network ACL rule with permit rules for a remote subnet, open an Azure PowerShell ISE.</span></span> <span data-ttu-id="564e9-134">Copiare e incollare lo script seguente, configurandolo con valori personalizzati, e quindi eseguirlo.</span><span class="sxs-lookup"><span data-stu-id="564e9-134">Copy and paste the script below, configuring the script with your own values, and then run the script.</span></span>

1. <span data-ttu-id="564e9-135">È innanzitutto necessario ottenere l'oggetto elenco di controllo di accesso (ACL) di rete per l'endpoint della macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="564e9-135">First step is to get the Network ACL object for the virtual machine endpoint.</span></span> <span data-ttu-id="564e9-136">Quindi si rimuoverà la regola dell'elenco di controllo di accesso.</span><span class="sxs-lookup"><span data-stu-id="564e9-136">You'll then remove the ACL rule.</span></span> <span data-ttu-id="564e9-137">In questo caso, la si rimuoverà in base all'ID regola.</span><span class="sxs-lookup"><span data-stu-id="564e9-137">In this case, we are removing it by rule ID.</span></span> <span data-ttu-id="564e9-138">In questo modo, dall'elenco di controllo di accesso verrà rimosso solo l'ID regola 0.</span><span class="sxs-lookup"><span data-stu-id="564e9-138">This will only remove the rule ID 0 from the ACL.</span></span> <span data-ttu-id="564e9-139">L'oggetto ACL non verrà eliminato dall'endpoint della macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="564e9-139">It does not remove the ACL object from the virtual machine endpoint.</span></span>
   
        Get-AzureVM –ServiceName $serviceName –Name $vmName `
        | Get-AzureAclConfig –EndpointName "web" `
        | Set-AzureAclConfig –RemoveRule –ID 0 –ACL $acl1
2. <span data-ttu-id="564e9-140">È quindi necessario applicare l'oggetto ACL di rete all'endpoint della macchina virtuale e aggiornare quest'ultima.</span><span class="sxs-lookup"><span data-stu-id="564e9-140">Next, you must apply the Network ACL object to the virtual machine endpoint and update the virtual machine.</span></span>
   
        Get-AzureVM –ServiceName $serviceName –Name $vmName `
        | Set-AzureEndpoint –ACL $acl1 –Name "web" `
        | Update-AzureVM

### <a name="remove-a-network-acl-from-a-virtual-machine-endpoint"></a><span data-ttu-id="564e9-141">Rimuovere un elenco di controllo di accesso di rete dall'endpoint di una macchina virtuale</span><span class="sxs-lookup"><span data-stu-id="564e9-141">Remove a Network ACL from a virtual machine endpoint</span></span>
<span data-ttu-id="564e9-142">In alcuni scenari potrebbe essere necessario rimuovere un oggetto ACL di rete dall'endpoint di una macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="564e9-142">In certain scenarios, you might want to remove a Network ACL object from a virtual machine endpoint.</span></span> <span data-ttu-id="564e9-143">A tale scopo, aprire un'istanza di Azure PowerShell ISE.</span><span class="sxs-lookup"><span data-stu-id="564e9-143">To do that, open an Azure PowerShell ISE.</span></span> <span data-ttu-id="564e9-144">Copiare e incollare lo script seguente, configurandolo con valori personalizzati, e quindi eseguirlo.</span><span class="sxs-lookup"><span data-stu-id="564e9-144">Copy and paste the script below, configuring the script with your own values, and then run the script.</span></span>

        Get-AzureVM –ServiceName $serviceName –Name $vmName `
        | Remove-AzureAclConfig –EndpointName "web" `
        | Update-AzureVM

## <a name="next-steps"></a><span data-ttu-id="564e9-145">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="564e9-145">Next steps</span></span>
[<span data-ttu-id="564e9-146">Che cos'è un elenco di controllo di accesso di rete?</span><span class="sxs-lookup"><span data-stu-id="564e9-146">What is a Network Access Control List (ACL)?</span></span>](virtual-networks-acl.md)


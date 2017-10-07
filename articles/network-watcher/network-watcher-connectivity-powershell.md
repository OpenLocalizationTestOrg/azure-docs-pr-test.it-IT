---
title: "connettività aaaCheck con Watcher di rete di Azure - PowerShell | Documenti Microsoft"
description: "Questa pagina viene illustrato come la connettività tootest con Watcher di rete con PowerShell"
services: network-watcher
documentationcenter: na
author: georgewallace
manager: timlt
editor: 
ms.service: network-watcher
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 07/11/2017
ms.author: gwallace
ms.openlocfilehash: 4bcb90a72f178445c38b7bd7fc5054c5d0c200bb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="check-connectivity-with-azure-network-watcher-using-powershell"></a><span data-ttu-id="38260-103">Controllare la connettività con Azure Network Watcher usando PowerShell</span><span class="sxs-lookup"><span data-stu-id="38260-103">Check connectivity with Azure Network Watcher using PowerShell</span></span>

> [!div class="op_single_selector"]
> - [<span data-ttu-id="38260-104">Portale</span><span class="sxs-lookup"><span data-stu-id="38260-104">Portal</span></span>](network-watcher-connectivity-portal.md)
> - [<span data-ttu-id="38260-105">PowerShell</span><span class="sxs-lookup"><span data-stu-id="38260-105">PowerShell</span></span>](network-watcher-connectivity-powershell.md)
> - [<span data-ttu-id="38260-106">Interfaccia della riga di comando 2.0</span><span class="sxs-lookup"><span data-stu-id="38260-106">CLI 2.0</span></span>](network-watcher-connectivity-cli.md)
> - [<span data-ttu-id="38260-107">API REST di Azure</span><span class="sxs-lookup"><span data-stu-id="38260-107">Azure REST API</span></span>](network-watcher-connectivity-rest.md)

<span data-ttu-id="38260-108">Informazioni su come è possibile stabilire toouse connettività tooverify se una connessione TCP diretta da una macchina virtuale di tooa dato endpoint.</span><span class="sxs-lookup"><span data-stu-id="38260-108">Learn how toouse connectivity tooverify if a direct TCP connection from a virtual machine tooa given endpoint can be established.</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="38260-109">Prima di iniziare</span><span class="sxs-lookup"><span data-stu-id="38260-109">Before you begin</span></span>

<span data-ttu-id="38260-110">Questo articolo si presuppone di che aver hello seguenti risorse:</span><span class="sxs-lookup"><span data-stu-id="38260-110">This article assumes you have hello following resources:</span></span>

* <span data-ttu-id="38260-111">Un'istanza del controllo di rete nell'area di hello desiderato toocheck connettività.</span><span class="sxs-lookup"><span data-stu-id="38260-111">An instance of Network Watcher in hello region you want toocheck connectivity.</span></span>

* <span data-ttu-id="38260-112">Connettività toocheck di macchine virtuali con.</span><span class="sxs-lookup"><span data-stu-id="38260-112">Virtual machines toocheck connectivity with.</span></span>

[!INCLUDE [network-watcher-preview](../../includes/network-watcher-public-preview-notice.md)]

> [!IMPORTANT]
> <span data-ttu-id="38260-113">Il controllo della connettività richiede un'estensione macchina virtuale `AzureNetworkWatcherExtension`.</span><span class="sxs-lookup"><span data-stu-id="38260-113">Connectivity check requires a virtual machine extension `AzureNetworkWatcherExtension`.</span></span> <span data-ttu-id="38260-114">Per l'installazione dell'estensione hello in una macchina virtuale di Windows, visitare [estensione della macchina virtuale Azure rete Watcher agente per Windows](../virtual-machines/windows/extensions-nwa.md) e per la visita di VM Linux [estensione della macchina virtuale Azure rete Watcher agente per Linux](../virtual-machines/linux/extensions-nwa.md).</span><span class="sxs-lookup"><span data-stu-id="38260-114">For installing hello extension on a Windows VM visit [Azure Network Watcher Agent virtual machine extension for Windows](../virtual-machines/windows/extensions-nwa.md) and for Linux VM visit [Azure Network Watcher Agent virtual machine extension for Linux](../virtual-machines/linux/extensions-nwa.md).</span></span>

## <a name="register-hello-preview-capability"></a><span data-ttu-id="38260-115">Registrare la funzionalità di anteprima hello</span><span class="sxs-lookup"><span data-stu-id="38260-115">Register hello preview capability</span></span>

<span data-ttu-id="38260-116">La connettività è attualmente in anteprima pubblica, toouse questa funzionalità che è necessario toobe registrato.</span><span class="sxs-lookup"><span data-stu-id="38260-116">Connectivity is currently in public preview, toouse this feature it needs toobe registered.</span></span> <span data-ttu-id="38260-117">toodo, hello esecuzione seguente esempio di PowerShell:</span><span class="sxs-lookup"><span data-stu-id="38260-117">toodo this, run hello following PowerShell sample:</span></span>

```powershell
Register-AzureRmProviderFeature -FeatureName AllowNetworkWatcherConnectivityCheck  -ProviderNamespace Microsoft.Network
Register-AzureRmResourceProvider -ProviderNamespace Microsoft.Network
```

<span data-ttu-id="38260-118">la registrazione di hello tooverify è stata completata correttamente, eseguire hello seguente esempio di Powershell:</span><span class="sxs-lookup"><span data-stu-id="38260-118">tooverify hello registration was successful, run hello following Powershell sample:</span></span>

```powershell
Get-AzureRmProviderFeature -FeatureName AllowNetworkWatcherConnectivityCheck  -ProviderNamespace  Microsoft.Network
```

<span data-ttu-id="38260-119">Se è stato registrato correttamente funzionalità hello, output di hello devono corrispondere seguente hello:</span><span class="sxs-lookup"><span data-stu-id="38260-119">If hello feature was properly registered, hello output should match hello following:</span></span>

```
FeatureName         ProviderName      RegistrationState
-----------         ------------      -----------------
AllowNetworkWatcherConnectivityCheck  Microsoft.Network Registered
```

## <a name="check-connectivity-tooa-virtual-machine"></a><span data-ttu-id="38260-120">Verificare la connettività tooa virtual machine</span><span class="sxs-lookup"><span data-stu-id="38260-120">Check connectivity tooa virtual machine</span></span>

<span data-ttu-id="38260-121">Questo esempio viene verificata la connettività tooa macchina virtuale di destinazione sulla porta 80.</span><span class="sxs-lookup"><span data-stu-id="38260-121">This example checks connectivity tooa destination virtual machine over port 80.</span></span>

### <a name="example"></a><span data-ttu-id="38260-122">Esempio</span><span class="sxs-lookup"><span data-stu-id="38260-122">Example</span></span>

```powershell
$rgName = "ContosoRG"
$sourceVMName = "MultiTierApp0"
$destVMName = "Database0"

$RG = Get-AzureRMResourceGroup -Name $rgName

$nw = Get-AzurermResource | Where {$_.ResourceType -eq "Microsoft.Network/networkWatchers" -and $_.Location -eq $RG.Location } 
$networkWatcher = Get-AzureRmNetworkWatcher -Name $nw.Name -ResourceGroupName $nw.ResourceGroupName

$VM1 = Get-AzureRMVM -ResourceGroupName $rgName | Where-Object -Property Name -EQ $sourceVMName
$VM2 = Get-AzureRMVM -ResourceGroupName $rgName | Where-Object -Property Name -EQ $destVMName

Test-AzureRmNetworkWatcherConnectivity -NetworkWatcher $networkWatcher -SourceId $VM1.Id -DestinationId $VM2.Id -DestinationPort 80
```

### <a name="response"></a><span data-ttu-id="38260-123">Response</span><span class="sxs-lookup"><span data-stu-id="38260-123">Response</span></span>

<span data-ttu-id="38260-124">Hello seguente risposta è tratto dall'esempio precedente hello.</span><span class="sxs-lookup"><span data-stu-id="38260-124">hello following response is from hello previous example.</span></span>  <span data-ttu-id="38260-125">Nella risposta, hello `ConnectionStatus` è **non raggiungibile**.</span><span class="sxs-lookup"><span data-stu-id="38260-125">In this response, hello `ConnectionStatus` is **Unreachable**.</span></span> <span data-ttu-id="38260-126">Si noterà che tutti hello probe inviati non riuscite.</span><span class="sxs-lookup"><span data-stu-id="38260-126">You can see that all hello probes sent failed.</span></span> <span data-ttu-id="38260-127">connettività Hello non riuscita nel dispositivo virtuale hello tooa scadenza configurata dall'utente `NetworkSecurityRule` denominato **UserRule_Port80**, configurato tooblock il traffico in entrata sulla porta 80.</span><span class="sxs-lookup"><span data-stu-id="38260-127">hello connectivity failed at hello virtual appliance due tooa user-configured `NetworkSecurityRule` named **UserRule_Port80**, configured tooblock incoming traffic on port 80.</span></span> <span data-ttu-id="38260-128">Queste informazioni possono essere utilizzati tooresearch i problemi di connessione.</span><span class="sxs-lookup"><span data-stu-id="38260-128">This information can be used tooresearch connection issues.</span></span>

```
ConnectionStatus : Unreachable
AvgLatencyInMs   : 
MinLatencyInMs   : 
MaxLatencyInMs   : 
ProbesSent       : 100
ProbesFailed     : 100
Hops             : [
                     {
                       "Type": "Source",
                       "Id": "c5222ea0-3213-4f85-a642-cee63217c2f3",
                       "Address": "10.1.1.4",
                       "ResourceId": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGrou
                   ps/ContosoRG/providers/Microsoft.Network/networkInterfaces/appNic0/ipConfigurat
                   ions/ipconfig1",
                       "NextHopIds": [
                         "9283a9f0-cc5e-4239-8f5e-ae0f3c19fbaa"
                       ],
                       "Issues": []
                     },
                     {
                       "Type": "VirtualAppliance",
                       "Id": "9283a9f0-cc5e-4239-8f5e-ae0f3c19fbaa",
                       "Address": "10.1.2.4",
                       "ResourceId": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGrou
                   ps/ContosoRG/providers/Microsoft.Network/networkInterfaces/fwNic/ipConfiguratio
                   ns/ipconfig1",
                       "NextHopIds": [
                         "0f1500cd-c512-4d43-b431-7267e4e67017"
                       ],
                       "Issues": []
                     },
                     {
                       "Type": "VirtualAppliance",
                       "Id": "0f1500cd-c512-4d43-b431-7267e4e67017",
                       "Address": "10.1.3.4",
                       "ResourceId": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGrou
                   ps/ContosoRG/providers/Microsoft.Network/networkInterfaces/auNic/ipConfiguratio
                   ns/ipconfig1",
                       "NextHopIds": [
                         "a88940f8-5fbe-40da-8d99-1dee89240f64"
                       ],
                       "Issues": [
                         {
                           "Origin": "Outbound",
                           "Severity": "Error",
                           "Type": "NetworkSecurityRule",
                           "Context": [
                             {
                               "key": "RuleName",
                               "value": "UserRule_Port80"
                             }
                           ]
                         }
                       ]
                     },
                     {
                       "Type": "VnetLocal",
                       "Id": "a88940f8-5fbe-40da-8d99-1dee89240f64",
                       "Address": "10.1.4.4",
                       "ResourceId": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGrou
                   ps/ContosoRG/providers/Microsoft.Network/networkInterfaces/dbNic0/ipConfigurati
                   ons/ipconfig1",
                       "NextHopIds": [],
                       "Issues": []
                     }
                   ]
```

## <a name="validate-routing-issues"></a><span data-ttu-id="38260-129">Problemi relativi alla convalida del routing</span><span class="sxs-lookup"><span data-stu-id="38260-129">Validate routing issues</span></span>

<span data-ttu-id="38260-130">esempio Hello controlla la connettività tra una macchina virtuale e un endpoint remoto.</span><span class="sxs-lookup"><span data-stu-id="38260-130">hello example checks connectivity between a virtual machine and a remote endpoint.</span></span>

### <a name="example"></a><span data-ttu-id="38260-131">Esempio</span><span class="sxs-lookup"><span data-stu-id="38260-131">Example</span></span>

```powershell
$rgName = "ContosoRG"
$sourceVMName = "MultiTierApp0"

$RG = Get-AzureRMResourceGroup -Name $rgName

$nw = Get-AzurermResource | Where {$_.ResourceType -eq "Microsoft.Network/networkWatchers" -and $_.Location -eq $RG.Location } 
$networkWatcher = Get-AzureRmNetworkWatcher -Name $nw.Name -ResourceGroupName $nw.ResourceGroupName

$VM1 = Get-AzureRMVM -ResourceGroupName $rgName | Where-Object -Property Name -EQ $sourceVMName

Test-AzureRmNetworkWatcherConnectivity -NetworkWatcher $networkWatcher -SourceId $VM1.Id -DestinationAddress 13.107.21.200 -DestinationPort 80
```

### <a name="response"></a><span data-ttu-id="38260-132">Response</span><span class="sxs-lookup"><span data-stu-id="38260-132">Response</span></span>

<span data-ttu-id="38260-133">Nell'esempio seguente di hello, hello `ConnectionStatus` viene visualizzato come **non raggiungibile**.</span><span class="sxs-lookup"><span data-stu-id="38260-133">In hello following example, hello `ConnectionStatus` is shown as **Unreachable**.</span></span> <span data-ttu-id="38260-134">In hello `Hops` informazioni dettagliate, è possibile visualizzare in `Issues` che è stato bloccato scadenza traffico hello tooa `UserDefinedRoute`.</span><span class="sxs-lookup"><span data-stu-id="38260-134">In hello `Hops` details, you can see under `Issues` that hello traffic was blocked due tooa `UserDefinedRoute`.</span></span> 

```
ConnectionStatus : Unreachable
AvgLatencyInMs   : 
MinLatencyInMs   : 
MaxLatencyInMs   : 
ProbesSent       : 100
ProbesFailed     : 100
Hops             : [
                     {
                       "Type": "Source",
                       "Id": "b4f7bceb-07a3-44ca-8bae-adec6628225f",
                       "Address": "10.1.1.4",
                       "ResourceId": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/ContosoRG/providers/Microsoft.Network/networkInterfaces/appNic0/ipConfigurations/ipconfig1",
                       "NextHopIds": [
                         "3fee8adf-692f-4523-b742-f6fdf6da6584"
                       ],
                       "Issues": [
                         {
                           "Origin": "Outbound",
                           "Severity": "Error",
                           "Type": "UserDefinedRoute",
                           "Context": [
                             {
                               "key": "RouteType",
                               "value": "User"
                             }
                           ]
                         }
                       ]
                     },
                     {
                       "Type": "Destination",
                       "Id": "3fee8adf-692f-4523-b742-f6fdf6da6584",
                       "Address": "13.107.21.200",
                       "ResourceId": "Unknown",
                       "NextHopIds": [],
                       "Issues": []
                     }
                   ]
```

## <a name="check-website-latency"></a><span data-ttu-id="38260-135">Controllare la latenza del sito Web</span><span class="sxs-lookup"><span data-stu-id="38260-135">Check website latency</span></span>

<span data-ttu-id="38260-136">Hello esempio controlla sito Web di tooa connettività hello.</span><span class="sxs-lookup"><span data-stu-id="38260-136">hello following example checks hello connectivity tooa website.</span></span>

### <a name="example"></a><span data-ttu-id="38260-137">Esempio</span><span class="sxs-lookup"><span data-stu-id="38260-137">Example</span></span>

```powershell
$rgName = "ContosoRG"
$sourceVMName = "MultiTierApp0"

$RG = Get-AzureRMResourceGroup -Name $rgName

$nw = Get-AzurermResource | Where {$_.ResourceType -eq "Microsoft.Network/networkWatchers" -and $_.Location -eq $RG.Location } 
$networkWatcher = Get-AzureRmNetworkWatcher -Name $nw.Name -ResourceGroupName $nw.ResourceGroupName

$VM1 = Get-AzureRMVM -ResourceGroupName $rgName | Where-Object -Property Name -EQ $sourceVMName

Test-AzureRmNetworkWatcherConnectivity -NetworkWatcher $networkWatcher -SourceId $VM1.Id -DestinationAddress http://bing.com/
```

### <a name="response"></a><span data-ttu-id="38260-138">Response</span><span class="sxs-lookup"><span data-stu-id="38260-138">Response</span></span>

<span data-ttu-id="38260-139">In hello seguente risposta, è possibile vedere hello `ConnectionStatus` viene illustrato come **raggiungibile**.</span><span class="sxs-lookup"><span data-stu-id="38260-139">In hello following response, you can see hello `ConnectionStatus` shows as **Reachable**.</span></span> <span data-ttu-id="38260-140">In caso di esito positivo della connessione vengono forniti i valori della latenza.</span><span class="sxs-lookup"><span data-stu-id="38260-140">When a connection is successful, latency values are provided.</span></span>

```
ConnectionStatus : Reachable
AvgLatencyInMs   : 1
MinLatencyInMs   : 0
MaxLatencyInMs   : 7
ProbesSent       : 100
ProbesFailed     : 0
Hops             : [
                     {
                       "Type": "Source",
                       "Id": "1f0e3415-27b0-4bf7-a59d-3e19fb854e3e",
                       "Address": "10.1.1.4",
                       "ResourceId": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/ContosoRG/providers/Microsoft.Network/networkInterfaces/appNic0/ipConfigurations/ipconfig1",
                       "NextHopIds": [
                         "f99f2bd1-42e8-4bbf-85b6-5d21d00c84e0"
                       ],
                       "Issues": []
                     },
                     {
                       "Type": "Internet",
                       "Id": "f99f2bd1-42e8-4bbf-85b6-5d21d00c84e0",
                       "Address": "204.79.197.200",
                       "ResourceId": "Internet",
                       "NextHopIds": [],
                       "Issues": []
                     }
                   ]
```

## <a name="check-connectivity-tooa-storage-endpoint"></a><span data-ttu-id="38260-141">Controllare la connettività tooa archiviazione endpoint</span><span class="sxs-lookup"><span data-stu-id="38260-141">Check connectivity tooa storage endpoint</span></span>

<span data-ttu-id="38260-142">Hello di esempio seguente verifica la connettività di hello da un account di archiviazione blog tooa macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="38260-142">hello following example tests hello connectivity from a virtual machine tooa blog storage account.</span></span>

### <a name="example"></a><span data-ttu-id="38260-143">Esempio</span><span class="sxs-lookup"><span data-stu-id="38260-143">Example</span></span>

```powershell
$rgName = "ContosoRG"
$sourceVMName = "MultiTierApp0"

$RG = Get-AzureRMResourceGroup -Name $rgName

$nw = Get-AzurermResource | Where {$_.ResourceType -eq "Microsoft.Network/networkWatchers" -and $_.Location -eq $RG.Location }
$networkWatcher = Get-AzureRmNetworkWatcher -Name $nw.Name -ResourceGroupName $nw.ResourceGroupName

$VM1 = Get-AzureRMVM -ResourceGroupName $rgName | Where-Object -Property Name -EQ $sourceVMName

Test-AzureRmNetworkWatcherConnectivity -NetworkWatcher $networkWatcher -SourceId $VM1.Id -DestinationAddress https://contosostorageexample.blob.core.windows.net/ 
```

### <a name="response"></a><span data-ttu-id="38260-144">Response</span><span class="sxs-lookup"><span data-stu-id="38260-144">Response</span></span>

<span data-ttu-id="38260-145">Hello json seguente è la risposta di esempio hello dall'esecuzione di cmdlet precedente hello.</span><span class="sxs-lookup"><span data-stu-id="38260-145">hello following json is hello example response from running hello previous cmdlet.</span></span> <span data-ttu-id="38260-146">Come destinazione di hello è raggiungibile, hello `ConnectionStatus` vengono visualizzate le proprietà come **raggiungibile**.</span><span class="sxs-lookup"><span data-stu-id="38260-146">As hello destination is reachable, hello `ConnectionStatus` property shows as **Reachable**.</span></span>  <span data-ttu-id="38260-147">Vengono fornite informazioni hello riguardanti hello numero di hop tooreach obbligatorio hello archiviazione blob e latenza.</span><span class="sxs-lookup"><span data-stu-id="38260-147">You are provided hello details regarding hello number of hops required tooreach hello storage blob and latency.</span></span>

```
ConnectionStatus : Reachable
AvgLatencyInMs   : 1
MinLatencyInMs   : 0
MaxLatencyInMs   : 8
ProbesSent       : 100
ProbesFailed     : 0
Hops             : [
                     {
                       "Type": "Source",
                       "Id": "9e7f61d9-fb45-41db-83e2-c815a919b8ed",
                       "Address": "10.1.1.4",
                       "ResourceId": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/ContosoRG/providers/Microsoft.Network/networkInterfaces/appNic0/ipConfigurations/ipconfig1",
                       "NextHopIds": [
                         "1e6d4b3c-7964-4afd-b959-aaa746ee0f15"
                       ],
                       "Issues": []
                     },
                     {
                       "Type": "Internet",
                       "Id": "1e6d4b3c-7964-4afd-b959-aaa746ee0f15",
                       "Address": "13.71.200.248",
                       "ResourceId": "Internet",
                       "NextHopIds": [],
                       "Issues": []
                     }
                   ]
```

## <a name="next-steps"></a><span data-ttu-id="38260-148">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="38260-148">Next steps</span></span>

<span data-ttu-id="38260-149">Per stabilire se un traffico specificato è consentito all'interno o all'esterno di una macchina virtuale, vedere [Check IP flow verify](network-watcher-check-ip-flow-verify-portal.md) (Controllare la verifica del flusso IP).</span><span class="sxs-lookup"><span data-stu-id="38260-149">Find if certain traffic is allowed in or out of your VM by visiting [Check IP flow verify](network-watcher-check-ip-flow-verify-portal.md)</span></span>

<span data-ttu-id="38260-150">Se il traffico viene bloccato e non può essere, vedere [gestire gruppi di sicurezza di rete](../virtual-network/virtual-network-manage-nsg-arm-portal.md) tootrack verso il basso hello rete sicurezza e gruppo di regole di sicurezza definiti.</span><span class="sxs-lookup"><span data-stu-id="38260-150">If traffic is being blocked and it should not be, see [Manage Network Security Groups](../virtual-network/virtual-network-manage-nsg-arm-portal.md) tootrack down hello network security group and security rules that are defined.</span></span>

<!-- Image references -->















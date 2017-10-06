---
title: acquisizioni di pacchetti aaaManage con Watcher di rete di Azure - PowerShell | Documenti Microsoft
description: "Questa pagina viene illustrato come i pacchetti hello toomanage acquisire funzionalità del controllo di rete con PowerShell"
services: network-watcher
documentationcenter: na
author: georgewallace
manager: timlt
editor: 
ms.assetid: 04d82085-c9ea-4ea1-b050-a3dd4960f3aa
ms.service: network-watcher
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/22/2017
ms.author: gwallace
ms.openlocfilehash: 77a522a1b05e020a73ba7140c1410615eb8761da
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="manage-packet-captures-with-azure-network-watcher-using-powershell"></a><span data-ttu-id="e073d-103">Gestire le acquisizioni di pacchetti con Azure Network Watcher tramite PowerShell</span><span class="sxs-lookup"><span data-stu-id="e073d-103">Manage packet captures with Azure Network Watcher using PowerShell</span></span>

> [!div class="op_single_selector"]
> - [<span data-ttu-id="e073d-104">Portale di Azure</span><span class="sxs-lookup"><span data-stu-id="e073d-104">Azure portal</span></span>](network-watcher-packet-capture-manage-portal.md)
> - [<span data-ttu-id="e073d-105">PowerShell</span><span class="sxs-lookup"><span data-stu-id="e073d-105">PowerShell</span></span>](network-watcher-packet-capture-manage-powershell.md)
> - [<span data-ttu-id="e073d-106">Interfaccia della riga di comando 1.0</span><span class="sxs-lookup"><span data-stu-id="e073d-106">CLI 1.0</span></span>](network-watcher-packet-capture-manage-cli-nodejs.md)
> - [<span data-ttu-id="e073d-107">Interfaccia della riga di comando 2.0</span><span class="sxs-lookup"><span data-stu-id="e073d-107">CLI 2.0</span></span>](network-watcher-packet-capture-manage-cli.md)
> - [<span data-ttu-id="e073d-108">API REST di Azure</span><span class="sxs-lookup"><span data-stu-id="e073d-108">Azure REST API</span></span>](network-watcher-packet-capture-manage-rest.md)

<span data-ttu-id="e073d-109">Acquisizione di pacchetti di rete Watcher consente tooand toocreate acquisizione sessioni tootrack traffico da una macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="e073d-109">Network Watcher packet capture allows you toocreate capture sessions tootrack traffic tooand from a virtual machine.</span></span> <span data-ttu-id="e073d-110">I filtri vengono forniti per hello acquisizione sessione tooensure che si acquisisce solo il traffico hello desiderato.</span><span class="sxs-lookup"><span data-stu-id="e073d-110">Filters are provided for hello capture session tooensure you capture only hello traffic you want.</span></span> <span data-ttu-id="e073d-111">Acquisizione di pacchetti consente toodiagnose anomalie di rete in modo proattivo e reattivo.</span><span class="sxs-lookup"><span data-stu-id="e073d-111">Packet capture helps toodiagnose network anomalies both reactively and proactively.</span></span> <span data-ttu-id="e073d-112">Altri usi includono la raccolta di statistiche di rete, ottenere informazioni su intrusioni di rete, client-server toodebug le comunicazioni e molto altro ancora.</span><span class="sxs-lookup"><span data-stu-id="e073d-112">Other uses include gathering network statistics, gaining information on network intrusions, toodebug client-server communications and much more.</span></span> <span data-ttu-id="e073d-113">Essendo in grado di tooremotely trigger pacchetto acquisizioni, questa funzionalità semplifica il carico di hello dell'esecuzione di acquisizione pacchetto eseguita manualmente e nel computer desiderato hello, che consente di risparmiare tempo prezioso.</span><span class="sxs-lookup"><span data-stu-id="e073d-113">By being able tooremotely trigger packet captures, this capability eases hello burden of running a packet capture manually and on hello desired machine, which saves valuable time.</span></span>

<span data-ttu-id="e073d-114">In questo articolo illustra hello diverse operazioni di gestione che sono attualmente disponibili per l'acquisizione di pacchetti.</span><span class="sxs-lookup"><span data-stu-id="e073d-114">This article takes you through hello different management tasks that are currently available for packet capture.</span></span>

- [<span data-ttu-id="e073d-115">**Avviare un'acquisizione di pacchetti**</span><span class="sxs-lookup"><span data-stu-id="e073d-115">**Start a packet capture**</span></span>](#start-a-packet-capture)
- [<span data-ttu-id="e073d-116">**Interrompere un'acquisizione di pacchetti**</span><span class="sxs-lookup"><span data-stu-id="e073d-116">**Stop a packet capture**</span></span>](#stop-a-packet-capture)
- [<span data-ttu-id="e073d-117">**Eliminare un'acquisizione di pacchetti**</span><span class="sxs-lookup"><span data-stu-id="e073d-117">**Delete a packet capture**</span></span>](#delete-a-packet-capture)
- [<span data-ttu-id="e073d-118">**Scaricare un'acquisizione di pacchetti**</span><span class="sxs-lookup"><span data-stu-id="e073d-118">**Download a packet capture**</span></span>](#download-a-packet-capture)

## <a name="before-you-begin"></a><span data-ttu-id="e073d-119">Prima di iniziare</span><span class="sxs-lookup"><span data-stu-id="e073d-119">Before you begin</span></span>

<span data-ttu-id="e073d-120">Questo articolo si presuppone di che aver hello seguenti risorse:</span><span class="sxs-lookup"><span data-stu-id="e073d-120">This article assumes you have hello following resources:</span></span>

* <span data-ttu-id="e073d-121">Un'istanza del controllo di rete nell'area di hello desiderato toocreate un'acquisizione pacchetti</span><span class="sxs-lookup"><span data-stu-id="e073d-121">An instance of Network Watcher in hello region you want toocreate a packet capture</span></span>

* <span data-ttu-id="e073d-122">Una macchina virtuale con i pacchetti hello acquisire estensione abilitata.</span><span class="sxs-lookup"><span data-stu-id="e073d-122">A virtual machine with hello packet capture extension enabled.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="e073d-123">L'acquisizione di pacchetti richiede un'estensione macchina virtuale `AzureNetworkWatcherExtension`.</span><span class="sxs-lookup"><span data-stu-id="e073d-123">Packet capture requires a virtual machine extension `AzureNetworkWatcherExtension`.</span></span> <span data-ttu-id="e073d-124">Per l'installazione dell'estensione hello in una macchina virtuale di Windows, visitare [estensione della macchina virtuale Azure rete Watcher agente per Windows](../virtual-machines/windows/extensions-nwa.md) e per la visita di VM Linux [estensione della macchina virtuale Azure rete Watcher agente per Linux](../virtual-machines/linux/extensions-nwa.md).</span><span class="sxs-lookup"><span data-stu-id="e073d-124">For installing hello extension on a Windows VM visit [Azure Network Watcher Agent virtual machine extension for Windows](../virtual-machines/windows/extensions-nwa.md) and for Linux VM visit [Azure Network Watcher Agent virtual machine extension for Linux](../virtual-machines/linux/extensions-nwa.md).</span></span>

## <a name="install-vm-extension"></a><span data-ttu-id="e073d-125">Installare un'estensione di macchina virtuale</span><span class="sxs-lookup"><span data-stu-id="e073d-125">Install VM extension</span></span>

### <a name="step-1"></a><span data-ttu-id="e073d-126">Passaggio 1</span><span class="sxs-lookup"><span data-stu-id="e073d-126">Step 1</span></span>

```powershell
$VM = Get-AzureRmVM -ResourceGroupName testrg -Name VM1
```

### <a name="step-2"></a><span data-ttu-id="e073d-127">Passaggio 2</span><span class="sxs-lookup"><span data-stu-id="e073d-127">Step 2</span></span>

<span data-ttu-id="e073d-128">esempio recupera informazioni sull'estensione di hello Hello necessari hello toorun `Set-AzureRmVMExtension` cmdlet.</span><span class="sxs-lookup"><span data-stu-id="e073d-128">hello following example retrieves hello extension information needed toorun hello `Set-AzureRmVMExtension` cmdlet.</span></span> <span data-ttu-id="e073d-129">Questo cmdlet installa l'agente di acquisizione di pacchetti hello in macchina virtuale guest di hello.</span><span class="sxs-lookup"><span data-stu-id="e073d-129">This cmdlet installs hello packet capture agent on hello guest virtual machine.</span></span>

> [!NOTE]
> <span data-ttu-id="e073d-130">Hello `Set-AzureRmVMExtension` cmdlet potrebbe richiedere diversi minuti toocomplete.</span><span class="sxs-lookup"><span data-stu-id="e073d-130">hello `Set-AzureRmVMExtension` cmdlet may take several minutes toocomplete.</span></span>

<span data-ttu-id="e073d-131">Per le macchine virtuali Windows:</span><span class="sxs-lookup"><span data-stu-id="e073d-131">For Windows virtual machines:</span></span>

```powershell
$AzureNetworkWatcherExtension = Get-AzureRmVMExtensionImage -Location WestCentralUS -PublisherName Microsoft.Azure.NetworkWatcher -Type NetworkWatcherAgentWindows -Version 1.4.13.0
$ExtensionName = "AzureNetworkWatcherExtension"
Set-AzureRmVMExtension -ResourceGroupName $VM.ResourceGroupName  -Location $VM.Location -VMName $VM.Name -Name $ExtensionName -Publisher $AzureNetworkWatcherExtension.PublisherName -ExtensionType $AzureNetworkWatcherExtension.Type -TypeHandlerVersion $AzureNetworkWatcherExtension.Version.Substring(0,3)
```

<span data-ttu-id="e073d-132">Per le macchine virtuali Linux:</span><span class="sxs-lookup"><span data-stu-id="e073d-132">For Linux virtual machines:</span></span>

```powershell
$AzureNetworkWatcherExtension = Get-AzureRmVMExtensionImage -Location WestCentralUS -PublisherName Microsoft.Azure.NetworkWatcher -Type NetworkWatcherAgentLinux -Version 1.4.13.0
$ExtensionName = "AzureNetworkWatcherExtension"
Set-AzureRmVMExtension -ResourceGroupName $VM.ResourceGroupName  -Location $VM.Location -VMName $VM.Name -Name $ExtensionName -Publisher $AzureNetworkWatcherExtension.PublisherName -ExtensionType $AzureNetworkWatcherExtension.Type -TypeHandlerVersion $AzureNetworkWatcherExtension.Version.Substring(0,3)
````

<span data-ttu-id="e073d-133">Hello seguito è riportata una risposta corretta dopo l'esecuzione di hello `Set-AzureRmVMExtension` cmdlet.</span><span class="sxs-lookup"><span data-stu-id="e073d-133">hello following example is a successful response after running hello `Set-AzureRmVMExtension` cmdlet.</span></span>

```
RequestId IsSuccessStatusCode StatusCode ReasonPhrase
--------- ------------------- ---------- ------------
                         True         OK OK   
```

### <a name="step-3"></a><span data-ttu-id="e073d-134">Passaggio 3</span><span class="sxs-lookup"><span data-stu-id="e073d-134">Step 3</span></span>

<span data-ttu-id="e073d-135">tooensure che hello agente è installato, eseguire hello `Get-AzureRmVMExtension` cmdlet e passare il nome della macchina virtuale hello ed estensione hello.</span><span class="sxs-lookup"><span data-stu-id="e073d-135">tooensure that hello agent is installed, run hello `Get-AzureRmVMExtension` cmdlet and pass it hello virtual machine name and hello extension name.</span></span>

```powershell
Get-AzureRmVMExtension -ResourceGroupName $VM.ResourceGroupName  -VMName $VM.Name -Name $ExtensionName
```

<span data-ttu-id="e073d-136">Hello di esempio seguente è riportato un esempio di risposta hello esecuzione`Get-AzureRmVMExtension`</span><span class="sxs-lookup"><span data-stu-id="e073d-136">hello following sample is an example of hello response from running `Get-AzureRmVMExtension`</span></span>

```
ResourceGroupName       : testrg
VMName                  : testvm1
Name                    : AzureNetworkWatcherExtension
Location                : westcentralus
Etag                    : null
Publisher               : Microsoft.Azure.NetworkWatcher
ExtensionType           : NetworkWatcherAgentWindows
TypeHandlerVersion      : 1.4
Id                      : /subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/testrg/providers/Microsoft.Compute/virtualMachines/testvm1/
                          extensions/AzureNetworkWatcherExtension
PublicSettings          : 
ProtectedSettings       : 
ProvisioningState       : Succeeded
Statuses                : 
SubStatuses             : 
AutoUpgradeMinorVersion : True
ForceUpdateTag          : 
```

## <a name="start-a-packet-capture"></a><span data-ttu-id="e073d-137">Avviare un'acquisizione di pacchetti</span><span class="sxs-lookup"><span data-stu-id="e073d-137">Start a packet capture</span></span>

<span data-ttu-id="e073d-138">Una volta hello passaggi precedenti, agente di acquisizione di pacchetti hello è installato nella macchina virtuale hello.</span><span class="sxs-lookup"><span data-stu-id="e073d-138">Once hello preceding steps are complete, hello packet capture agent is installed on hello virtual machine.</span></span>

### <a name="step-1"></a><span data-ttu-id="e073d-139">Passaggio 1</span><span class="sxs-lookup"><span data-stu-id="e073d-139">Step 1</span></span>

<span data-ttu-id="e073d-140">passaggio successivo Hello è istanza di tooretrieve hello Watcher di rete.</span><span class="sxs-lookup"><span data-stu-id="e073d-140">hello next step is tooretrieve hello Network Watcher instance.</span></span> <span data-ttu-id="e073d-141">Questa variabile viene passata toohello `New-AzureRmNetworkWatcherPacketCapture` cmdlet nel passaggio 4.</span><span class="sxs-lookup"><span data-stu-id="e073d-141">This variable is passed toohello `New-AzureRmNetworkWatcherPacketCapture` cmdlet in step 4.</span></span>

```powershell
$nw = Get-AzurermResource | Where {$_.ResourceType -eq "Microsoft.Network/networkWatchers" -and $_.Location -eq "WestCentralUS" }
$networkWatcher = Get-AzureRmNetworkWatcher -Name $nw.Name -ResourceGroupName $nw.ResourceGroupName  
```

### <a name="step-2"></a><span data-ttu-id="e073d-142">Passaggio 2</span><span class="sxs-lookup"><span data-stu-id="e073d-142">Step 2</span></span>

<span data-ttu-id="e073d-143">Recuperare un account di archiviazione.</span><span class="sxs-lookup"><span data-stu-id="e073d-143">Retrieve a storage account.</span></span> <span data-ttu-id="e073d-144">Questo account di archiviazione è file di acquisizione di pacchetti hello toostore utilizzato.</span><span class="sxs-lookup"><span data-stu-id="e073d-144">This storage account is used toostore hello packet capture file.</span></span>

```powershell
$storageAccount = Get-AzureRmStorageAccount -ResourceGroupName testrg -Name testrgsa123
```

### <a name="step-3"></a><span data-ttu-id="e073d-145">Passaggio 3</span><span class="sxs-lookup"><span data-stu-id="e073d-145">Step 3</span></span>

<span data-ttu-id="e073d-146">I filtri possono essere utilizzati toolimit hello i dati archiviati dall'acquisizione di pacchetti hello.</span><span class="sxs-lookup"><span data-stu-id="e073d-146">Filters can be used toolimit hello data that is stored by hello packet capture.</span></span> <span data-ttu-id="e073d-147">Hello esempio due filtri impostati.</span><span class="sxs-lookup"><span data-stu-id="e073d-147">hello following example sets up two filters.</span></span>  <span data-ttu-id="e073d-148">Raccoglie un filtro in uscita TCP traffico solo da indirizzo IP locale 10.0.0.3 toodestination porte 20, 80 e 443.</span><span class="sxs-lookup"><span data-stu-id="e073d-148">One filter collects outgoing TCP traffic only from local IP 10.0.0.3 toodestination ports 20, 80 and 443.</span></span>  <span data-ttu-id="e073d-149">secondo filtro Hello raccoglie solo il traffico UDP.</span><span class="sxs-lookup"><span data-stu-id="e073d-149">hello second filter collects only UDP traffic.</span></span>

```powershell
$filter1 = New-AzureRmPacketCaptureFilterConfig -Protocol TCP -RemoteIPAddress "1.1.1.1-255.255.255" -LocalIPAddress "10.0.0.3" -LocalPort "1-65535" -RemotePort "20;80;443"
$filter2 = New-AzureRmPacketCaptureFilterConfig -Protocol UDP
```

> [!NOTE]
> <span data-ttu-id="e073d-150">Per un'acquisizione di pacchetti è possibile definire più filtri.</span><span class="sxs-lookup"><span data-stu-id="e073d-150">Multiple filters can be defined for a packet capture.</span></span>

### <a name="step-4"></a><span data-ttu-id="e073d-151">Passaggio 4</span><span class="sxs-lookup"><span data-stu-id="e073d-151">Step 4</span></span>

<span data-ttu-id="e073d-152">Eseguire hello `New-AzureRmNetworkWatcherPacketCapture` cmdlet toostart hello pacchetto acquisizione processo, passando valori hello necessario recuperati in hello passaggi precedenti.</span><span class="sxs-lookup"><span data-stu-id="e073d-152">Run hello `New-AzureRmNetworkWatcherPacketCapture` cmdlet toostart hello packet capture process, passing hello required values retrieved in hello preceding steps.</span></span>
```powershell

New-AzureRmNetworkWatcherPacketCapture -NetworkWatcher $networkWatcher -TargetVirtualMachineId $vm.Id -PacketCaptureName "PacketCaptureTest" -StorageAccountId $storageAccount.id -TimeLimitInSeconds 60 -Filters $filter1, $filter2
```

<span data-ttu-id="e073d-153">esempio Hello è output di hello prevista dell'esecuzione hello `New-AzureRmNetworkWatcherPacketCapture` cmdlet.</span><span class="sxs-lookup"><span data-stu-id="e073d-153">hello following example is hello expected output from running hello `New-AzureRmNetworkWatcherPacketCapture` cmdlet.</span></span>

```
Name                    : PacketCaptureTest
Id                      : /subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/NetworkWatcherRG/providers/Microsoft.Network/networkWatcher
                          s/NetworkWatcher_westcentralus/packetCaptures/PacketCaptureTest
Etag                    : W/"3bf27278-8251-4651-9546-c7f369855e4e"
ProvisioningState       : Succeeded
Target                  : /subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/testrg/providers/Microsoft.Compute/virtualMachines/testvm1
BytesToCapturePerPacket : 0
TotalBytesPerSession    : 1073741824
TimeLimitInSeconds      : 60
StorageLocation         : {
                            "StorageId": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/testrg/providers/Microsoft.Storage/storageA
                          ccounts/examplestorage",
                            "StoragePath": "https://examplestorage.blob.core.windows.net/network-watcher-logs/subscriptions/00000000-0000-0000-0000-00000
                          0000000/resourcegroups/testrg/providers/microsoft.compute/virtualmachines/testvm1/2017/02/01/packetcapture_22_42_48_238.cap"
                          }
Filters                 : [
                            {
                              "Protocol": "TCP",
                              "RemoteIPAddress": "1.1.1.1-255.255.255",
                              "LocalIPAddress": "10.0.0.3",
                              "LocalPort": "1-65535",
                              "RemotePort": "20;80;443"
                            },
                            {
                              "Protocol": "UDP",
                              "RemoteIPAddress": "",
                              "LocalIPAddress": "",
                              "LocalPort": "",
                              "RemotePort": ""
                            }
                          ]


```

## <a name="get-a-packet-capture"></a><span data-ttu-id="e073d-154">Ottenere un'acquisizione di pacchetti</span><span class="sxs-lookup"><span data-stu-id="e073d-154">Get a packet capture</span></span>

<span data-ttu-id="e073d-155">Esecuzione hello `Get-AzureRmNetworkWatcherPacketCapture` cmdlet recupera informazioni sullo stato hello di un'acquisizione di pacchetti attualmente in esecuzione o è stata completata.</span><span class="sxs-lookup"><span data-stu-id="e073d-155">Running hello `Get-AzureRmNetworkWatcherPacketCapture` cmdlet, retrieves hello status of a currently running, or completed packet capture.</span></span>

```powershell
Get-AzureRmNetworkWatcherPacketCapture -NetworkWatcher $networkWatcher -PacketCaptureName "PacketCaptureTest"
```

<span data-ttu-id="e073d-156">esempio Hello è output hello hello `Get-AzureRmNetworkWatcherPacketCapture` cmdlet.</span><span class="sxs-lookup"><span data-stu-id="e073d-156">hello following example is hello output from hello `Get-AzureRmNetworkWatcherPacketCapture` cmdlet.</span></span> <span data-ttu-id="e073d-157">Hello seguito è riportata al termine dell'acquisizione hello.</span><span class="sxs-lookup"><span data-stu-id="e073d-157">hello following example is after hello capture is complete.</span></span> <span data-ttu-id="e073d-158">valore PacketCaptureStatus Hello viene arrestato, con un StopReason di TimeExceeded.</span><span class="sxs-lookup"><span data-stu-id="e073d-158">hello PacketCaptureStatus value is Stopped, with a StopReason of TimeExceeded.</span></span> <span data-ttu-id="e073d-159">Questo valore indica che acquisizione pacchetti hello ha avuto esito positivo e il tempo di esecuzione.</span><span class="sxs-lookup"><span data-stu-id="e073d-159">This value shows that hello packet capture was successful and ran its time.</span></span>
```
Name                    : PacketCaptureTest
Id                      : /subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/NetworkWatcherRG/providers/Microsoft.Network/networkWatcher
                          s/NetworkWatcher_westcentralus/packetCaptures/PacketCaptureTest
Etag                    : W/"4b9a81ed-dc63-472e-869e-96d7166ccb9b"
ProvisioningState       : Succeeded
Target                  : /subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/testrg/providers/Microsoft.Compute/virtualMachines/testvm1
BytesToCapturePerPacket : 0
TotalBytesPerSession    : 1073741824
TimeLimitInSeconds      : 60
StorageLocation         : {
                            "StorageId": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/testrg/providers/Microsoft.Storage/storageA
                          ccounts/examplestorage",
                            "StoragePath": "https://examplestorage.blob.core.windows.net/network-watcher-logs/subscriptions/00000000-0000-0000-0000-00000
                          0000000/resourcegroups/testrg/providers/microsoft.compute/virtualmachines/testvm1/2017/02/01/packetcapture_22_42_48_238.cap"
                          }
Filters                 : [
                            {
                              "Protocol": "TCP",
                              "RemoteIPAddress": "1.1.1.1-255.255.255",
                              "LocalIPAddress": "10.0.0.3",
                              "LocalPort": "1-65535",
                              "RemotePort": "20;80;443"
                            },
                            {
                              "Protocol": "UDP",
                              "RemoteIPAddress": "",
                              "LocalIPAddress": "",
                              "LocalPort": "",
                              "RemotePort": ""
                            }
                          ]
CaptureStartTime        : 2/1/2017 10:43:01 PM
PacketCaptureStatus     : Stopped
StopReason              : TimeExceeded
PacketCaptureError      : []
```

## <a name="stop-a-packet-capture"></a><span data-ttu-id="e073d-160">Interrompere un'acquisizione di pacchetti</span><span class="sxs-lookup"><span data-stu-id="e073d-160">Stop a packet capture</span></span>

<span data-ttu-id="e073d-161">Eseguendo hello `Stop-AzureRmNetworkWatcherPacketCapture` cmdlet, se una sessione di acquisizione è in corso viene arrestata.</span><span class="sxs-lookup"><span data-stu-id="e073d-161">By running hello `Stop-AzureRmNetworkWatcherPacketCapture` cmdlet, if a capture session is in progress it is stopped.</span></span>

```powershell
Stop-AzureRmNetworkWatcherPacketCapture -NetworkWatcher $networkWatcher -PacketCaptureName "PacketCaptureTest"
```

> [!NOTE]
> <span data-ttu-id="e073d-162">cmdlet di Hello non restituisce alcuna risposta quando è stato eseguito in una sessione di acquisizione attualmente in esecuzione o di una sessione esistente che è già stato arrestato.</span><span class="sxs-lookup"><span data-stu-id="e073d-162">hello cmdlet returns no response when ran on a currently running capture session or an existing session that has already stopped.</span></span>

## <a name="delete-a-packet-capture"></a><span data-ttu-id="e073d-163">Eliminare un'acquisizione di pacchetti</span><span class="sxs-lookup"><span data-stu-id="e073d-163">Delete a packet capture</span></span>

```powershell
Remove-AzureRmNetworkWatcherPacketCapture -NetworkWatcher $networkWatcher -PacketCaptureName "PacketCaptureTest"
```

> [!NOTE]
> <span data-ttu-id="e073d-164">L'eliminazione di un'acquisizione di pacchetti non elimina il file hello nell'account di archiviazione hello.</span><span class="sxs-lookup"><span data-stu-id="e073d-164">Deleting a packet capture does not delete hello file in hello storage account.</span></span>

## <a name="download-a-packet-capture"></a><span data-ttu-id="e073d-165">Scaricare un'acquisizione di pacchetti</span><span class="sxs-lookup"><span data-stu-id="e073d-165">Download a packet capture</span></span>

<span data-ttu-id="e073d-166">Una volta completata la sessione di acquisizione di pacchetti, hello acquisizione file può essere caricato tooblob tooa o archiviazione locale nella macchina virtuale hello.</span><span class="sxs-lookup"><span data-stu-id="e073d-166">Once your packet capture session has completed, hello capture file can be uploaded tooblob storage or tooa local file on hello VM.</span></span> <span data-ttu-id="e073d-167">percorso di archiviazione Hello dell'acquisizione di pacchetti hello è definito al momento della creazione della sessione hello.</span><span class="sxs-lookup"><span data-stu-id="e073d-167">hello storage location of hello packet capture is defined at creation of hello session.</span></span> <span data-ttu-id="e073d-168">Tooaccess un utile strumento questi file di acquisizione di account di archiviazione tooa salvato è Microsoft Azure Storage Explorer, che può essere scaricata qui: http://storageexplorer.com/</span><span class="sxs-lookup"><span data-stu-id="e073d-168">A convenient tool tooaccess these capture files saved tooa storage account is Microsoft Azure Storage Explorer, which can be downloaded here:  http://storageexplorer.com/</span></span>

<span data-ttu-id="e073d-169">Se viene specificato un account di archiviazione, i file di acquisizione dei pacchetti vengono salvati tooa account di archiviazione in hello seguente posizione:</span><span class="sxs-lookup"><span data-stu-id="e073d-169">If a storage account is specified, packet capture files are saved tooa storage account at hello following location:</span></span>

```
https://{storageAccountName}.blob.core.windows.net/network-watcher-logs/subscriptions/{subscriptionId}/resourcegroups/{storageAccountResourceGroup}/providers/microsoft.compute/virtualmachines/{VMName}/{year}/{month}/{day}/packetCapture_{creationTime}.cap
```

## <a name="next-steps"></a><span data-ttu-id="e073d-170">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="e073d-170">Next steps</span></span>

<span data-ttu-id="e073d-171">Informazioni su come acquisizioni di pacchetti tooautomate con gli avvisi di macchina virtuale visualizzando [creare un'acquisizione pacchetto attivati avvisi](network-watcher-alert-triggered-packet-capture.md)</span><span class="sxs-lookup"><span data-stu-id="e073d-171">Learn how tooautomate packet captures with Virtual machine alerts by viewing [Create an alert triggered packet capture](network-watcher-alert-triggered-packet-capture.md)</span></span>

<span data-ttu-id="e073d-172">Per stabilire se un traffico specificato è consentito all'interno o all'esterno di una macchina virtuale, leggere l'articolo su come [controllare la verifica del flusso IP](network-watcher-check-ip-flow-verify-portal.md).</span><span class="sxs-lookup"><span data-stu-id="e073d-172">Find if certain traffic is allowed in orr out of your VM by visiting [Check IP flow verify](network-watcher-check-ip-flow-verify-portal.md)</span></span>

<!-- Image references -->















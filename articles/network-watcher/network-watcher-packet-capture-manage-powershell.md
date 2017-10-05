---
title: Gestire le acquisizioni di pacchetti con Azure Network Watcher - PowerShell | Documentazione Microsoft
description: "Questa pagina illustra come gestire la funzionalità di acquisizione di pacchetti di Network Watcher tramite PowerShell"
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
ms.openlocfilehash: abd3b3641da80ee835fac85b4bde68594449e451
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="manage-packet-captures-with-azure-network-watcher-using-powershell"></a><span data-ttu-id="39f73-103">Gestire le acquisizioni di pacchetti con Azure Network Watcher tramite PowerShell</span><span class="sxs-lookup"><span data-stu-id="39f73-103">Manage packet captures with Azure Network Watcher using PowerShell</span></span>

> [!div class="op_single_selector"]
> - [<span data-ttu-id="39f73-104">Portale di Azure</span><span class="sxs-lookup"><span data-stu-id="39f73-104">Azure portal</span></span>](network-watcher-packet-capture-manage-portal.md)
> - [<span data-ttu-id="39f73-105">PowerShell</span><span class="sxs-lookup"><span data-stu-id="39f73-105">PowerShell</span></span>](network-watcher-packet-capture-manage-powershell.md)
> - [<span data-ttu-id="39f73-106">Interfaccia della riga di comando 1.0</span><span class="sxs-lookup"><span data-stu-id="39f73-106">CLI 1.0</span></span>](network-watcher-packet-capture-manage-cli-nodejs.md)
> - [<span data-ttu-id="39f73-107">Interfaccia della riga di comando 2.0</span><span class="sxs-lookup"><span data-stu-id="39f73-107">CLI 2.0</span></span>](network-watcher-packet-capture-manage-cli.md)
> - [<span data-ttu-id="39f73-108">API REST di Azure</span><span class="sxs-lookup"><span data-stu-id="39f73-108">Azure REST API</span></span>](network-watcher-packet-capture-manage-rest.md)

<span data-ttu-id="39f73-109">Il servizio di acquisizione di pacchetti di Network Watcher consente di creare sessioni di acquisizione per registrare il traffico da e verso una macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="39f73-109">Network Watcher packet capture allows you to create capture sessions to track traffic to and from a virtual machine.</span></span> <span data-ttu-id="39f73-110">Sono disponibili filtri per la sessione di acquisizione per garantire che venga acquisito solo il traffico desiderato.</span><span class="sxs-lookup"><span data-stu-id="39f73-110">Filters are provided for the capture session to ensure you capture only the traffic you want.</span></span> <span data-ttu-id="39f73-111">Il servizio di acquisizione di pacchetti consente di individuare eventuali anomalie di rete in modo proattivo e reattivo.</span><span class="sxs-lookup"><span data-stu-id="39f73-111">Packet capture helps to diagnose network anomalies both reactively and proactively.</span></span> <span data-ttu-id="39f73-112">Altri utilizzi comprendono la raccolta di statistiche di rete, informazioni sulle intrusioni nella rete, debug delle comunicazioni client-server e molto altro ancora.</span><span class="sxs-lookup"><span data-stu-id="39f73-112">Other uses include gathering network statistics, gaining information on network intrusions, to debug client-server communications and much more.</span></span> <span data-ttu-id="39f73-113">La possibilità di attivare da remoto l'acquisizione di pacchetti evita di dover eseguire manualmente questa operazione sul computer desiderato, consentendo un notevole risparmio di tempo.</span><span class="sxs-lookup"><span data-stu-id="39f73-113">By being able to remotely trigger packet captures, this capability eases the burden of running a packet capture manually and on the desired machine, which saves valuable time.</span></span>

<span data-ttu-id="39f73-114">Questo articolo illustra le diverse attività di gestione attualmente disponibili per l'acquisizione di pacchetti.</span><span class="sxs-lookup"><span data-stu-id="39f73-114">This article takes you through the different management tasks that are currently available for packet capture.</span></span>

- [<span data-ttu-id="39f73-115">**Avviare un'acquisizione di pacchetti**</span><span class="sxs-lookup"><span data-stu-id="39f73-115">**Start a packet capture**</span></span>](#start-a-packet-capture)
- [<span data-ttu-id="39f73-116">**Interrompere un'acquisizione di pacchetti**</span><span class="sxs-lookup"><span data-stu-id="39f73-116">**Stop a packet capture**</span></span>](#stop-a-packet-capture)
- [<span data-ttu-id="39f73-117">**Eliminare un'acquisizione di pacchetti**</span><span class="sxs-lookup"><span data-stu-id="39f73-117">**Delete a packet capture**</span></span>](#delete-a-packet-capture)
- [<span data-ttu-id="39f73-118">**Scaricare un'acquisizione di pacchetti**</span><span class="sxs-lookup"><span data-stu-id="39f73-118">**Download a packet capture**</span></span>](#download-a-packet-capture)

## <a name="before-you-begin"></a><span data-ttu-id="39f73-119">Prima di iniziare</span><span class="sxs-lookup"><span data-stu-id="39f73-119">Before you begin</span></span>

<span data-ttu-id="39f73-120">Questo articolo presuppone che l'utente disponga delle risorse seguenti:</span><span class="sxs-lookup"><span data-stu-id="39f73-120">This article assumes you have the following resources:</span></span>

* <span data-ttu-id="39f73-121">Un'istanza di Network Watcher nell'area in cui creare un'acquisizione di pacchetti.</span><span class="sxs-lookup"><span data-stu-id="39f73-121">An instance of Network Watcher in the region you want to create a packet capture</span></span>

* <span data-ttu-id="39f73-122">Una macchina virtuale con l'estensione di acquisizione di pacchetti abilitata.</span><span class="sxs-lookup"><span data-stu-id="39f73-122">A virtual machine with the packet capture extension enabled.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="39f73-123">L'acquisizione di pacchetti richiede un'estensione macchina virtuale `AzureNetworkWatcherExtension`.</span><span class="sxs-lookup"><span data-stu-id="39f73-123">Packet capture requires a virtual machine extension `AzureNetworkWatcherExtension`.</span></span> <span data-ttu-id="39f73-124">Per installare l'estensione in una VM Windows, vedere [Estensione macchina virtuale agente Azure Network Watcher per Windows](../virtual-machines/windows/extensions-nwa.md) e per una VM Linux VM vedere [Estensione macchina virtuale Azure Network Watcher Agent per Linux](../virtual-machines/linux/extensions-nwa.md).</span><span class="sxs-lookup"><span data-stu-id="39f73-124">For installing the extension on a Windows VM visit [Azure Network Watcher Agent virtual machine extension for Windows](../virtual-machines/windows/extensions-nwa.md) and for Linux VM visit [Azure Network Watcher Agent virtual machine extension for Linux](../virtual-machines/linux/extensions-nwa.md).</span></span>

## <a name="install-vm-extension"></a><span data-ttu-id="39f73-125">Installare un'estensione macchina virtuale</span><span class="sxs-lookup"><span data-stu-id="39f73-125">Install VM extension</span></span>

### <a name="step-1"></a><span data-ttu-id="39f73-126">Passaggio 1</span><span class="sxs-lookup"><span data-stu-id="39f73-126">Step 1</span></span>

```powershell
$VM = Get-AzureRmVM -ResourceGroupName testrg -Name VM1
```

### <a name="step-2"></a><span data-ttu-id="39f73-127">Passaggio 2</span><span class="sxs-lookup"><span data-stu-id="39f73-127">Step 2</span></span>

<span data-ttu-id="39f73-128">Nell'esempio seguente vengono recuperate le informazioni sull'estensione necessarie per eseguire il cmdlet `Set-AzureRmVMExtension`.</span><span class="sxs-lookup"><span data-stu-id="39f73-128">The following example retrieves the extension information needed to run the `Set-AzureRmVMExtension` cmdlet.</span></span> <span data-ttu-id="39f73-129">Il cmdlet installa l'agente di acquisizione di pacchetti sulla macchina virtuale guest.</span><span class="sxs-lookup"><span data-stu-id="39f73-129">This cmdlet installs the packet capture agent on the guest virtual machine.</span></span>

> [!NOTE]
> <span data-ttu-id="39f73-130">Il completamento del cmdlet `Set-AzureRmVMExtension` può richiedere alcuni minuti.</span><span class="sxs-lookup"><span data-stu-id="39f73-130">The `Set-AzureRmVMExtension` cmdlet may take several minutes to complete.</span></span>

<span data-ttu-id="39f73-131">Per le macchine virtuali Windows:</span><span class="sxs-lookup"><span data-stu-id="39f73-131">For Windows virtual machines:</span></span>

```powershell
$AzureNetworkWatcherExtension = Get-AzureRmVMExtensionImage -Location WestCentralUS -PublisherName Microsoft.Azure.NetworkWatcher -Type NetworkWatcherAgentWindows -Version 1.4.13.0
$ExtensionName = "AzureNetworkWatcherExtension"
Set-AzureRmVMExtension -ResourceGroupName $VM.ResourceGroupName  -Location $VM.Location -VMName $VM.Name -Name $ExtensionName -Publisher $AzureNetworkWatcherExtension.PublisherName -ExtensionType $AzureNetworkWatcherExtension.Type -TypeHandlerVersion $AzureNetworkWatcherExtension.Version.Substring(0,3)
```

<span data-ttu-id="39f73-132">Per le macchine virtuali Linux:</span><span class="sxs-lookup"><span data-stu-id="39f73-132">For Linux virtual machines:</span></span>

```powershell
$AzureNetworkWatcherExtension = Get-AzureRmVMExtensionImage -Location WestCentralUS -PublisherName Microsoft.Azure.NetworkWatcher -Type NetworkWatcherAgentLinux -Version 1.4.13.0
$ExtensionName = "AzureNetworkWatcherExtension"
Set-AzureRmVMExtension -ResourceGroupName $VM.ResourceGroupName  -Location $VM.Location -VMName $VM.Name -Name $ExtensionName -Publisher $AzureNetworkWatcherExtension.PublisherName -ExtensionType $AzureNetworkWatcherExtension.Type -TypeHandlerVersion $AzureNetworkWatcherExtension.Version.Substring(0,3)
````

<span data-ttu-id="39f73-133">L'esempio seguente rappresenta una risposta corretta dopo l'esecuzione del cmdlet `Set-AzureRmVMExtension`.</span><span class="sxs-lookup"><span data-stu-id="39f73-133">The following example is a successful response after running the `Set-AzureRmVMExtension` cmdlet.</span></span>

```
RequestId IsSuccessStatusCode StatusCode ReasonPhrase
--------- ------------------- ---------- ------------
                         True         OK OK   
```

### <a name="step-3"></a><span data-ttu-id="39f73-134">Passaggio 3</span><span class="sxs-lookup"><span data-stu-id="39f73-134">Step 3</span></span>

<span data-ttu-id="39f73-135">Per verificare che l'agente sia stato installato, eseguire il cmdlet `Get-AzureRmVMExtension` e passarlo al nome della macchina virtuale e al nome dell'estensione.</span><span class="sxs-lookup"><span data-stu-id="39f73-135">To ensure that the agent is installed, run the `Get-AzureRmVMExtension` cmdlet and pass it the virtual machine name and the extension name.</span></span>

```powershell
Get-AzureRmVMExtension -ResourceGroupName $VM.ResourceGroupName  -VMName $VM.Name -Name $ExtensionName
```

<span data-ttu-id="39f73-136">L'esempio seguente riporta una possibile risposta all'esecuzione di `Get-AzureRmVMExtension`.</span><span class="sxs-lookup"><span data-stu-id="39f73-136">The following sample is an example of the response from running `Get-AzureRmVMExtension`</span></span>

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

## <a name="start-a-packet-capture"></a><span data-ttu-id="39f73-137">Avviare un'acquisizione di pacchetti</span><span class="sxs-lookup"><span data-stu-id="39f73-137">Start a packet capture</span></span>

<span data-ttu-id="39f73-138">Dopo aver completato i passaggi precedenti, l'agente di acquisizione di pacchetti è installato nella macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="39f73-138">Once the preceding steps are complete, the packet capture agent is installed on the virtual machine.</span></span>

### <a name="step-1"></a><span data-ttu-id="39f73-139">Passaggio 1</span><span class="sxs-lookup"><span data-stu-id="39f73-139">Step 1</span></span>

<span data-ttu-id="39f73-140">Il passaggio successivo consente di recuperare l'istanza di Network Watcher.</span><span class="sxs-lookup"><span data-stu-id="39f73-140">The next step is to retrieve the Network Watcher instance.</span></span> <span data-ttu-id="39f73-141">Questa variabile viene passata al cmdlet `New-AzureRmNetworkWatcherPacketCapture` nel passaggio 4.</span><span class="sxs-lookup"><span data-stu-id="39f73-141">This variable is passed to the `New-AzureRmNetworkWatcherPacketCapture` cmdlet in step 4.</span></span>

```powershell
$nw = Get-AzurermResource | Where {$_.ResourceType -eq "Microsoft.Network/networkWatchers" -and $_.Location -eq "WestCentralUS" }
$networkWatcher = Get-AzureRmNetworkWatcher -Name $nw.Name -ResourceGroupName $nw.ResourceGroupName  
```

### <a name="step-2"></a><span data-ttu-id="39f73-142">Passaggio 2</span><span class="sxs-lookup"><span data-stu-id="39f73-142">Step 2</span></span>

<span data-ttu-id="39f73-143">Recuperare un account di archiviazione.</span><span class="sxs-lookup"><span data-stu-id="39f73-143">Retrieve a storage account.</span></span> <span data-ttu-id="39f73-144">L'account di archiviazione viene usato per archiviare il file di acquisizione di pacchetti.</span><span class="sxs-lookup"><span data-stu-id="39f73-144">This storage account is used to store the packet capture file.</span></span>

```powershell
$storageAccount = Get-AzureRmStorageAccount -ResourceGroupName testrg -Name testrgsa123
```

### <a name="step-3"></a><span data-ttu-id="39f73-145">Passaggio 3</span><span class="sxs-lookup"><span data-stu-id="39f73-145">Step 3</span></span>

<span data-ttu-id="39f73-146">È possibile usare i filtri per limitare i dati archiviati dall'acquisizione di pacchetti.</span><span class="sxs-lookup"><span data-stu-id="39f73-146">Filters can be used to limit the data that is stored by the packet capture.</span></span> <span data-ttu-id="39f73-147">Nell'esempio seguente vengono impostati due filtri.</span><span class="sxs-lookup"><span data-stu-id="39f73-147">The following example sets up two filters.</span></span>  <span data-ttu-id="39f73-148">Un filtro acquisisce il traffico TCP in uscita solo dall'indirizzo IP 10.0.0.3 locale verso le porte di destinazione 20, 80 e 443.</span><span class="sxs-lookup"><span data-stu-id="39f73-148">One filter collects outgoing TCP traffic only from local IP 10.0.0.3 to destination ports 20, 80 and 443.</span></span>  <span data-ttu-id="39f73-149">Il secondo filtro acquisisce solo il traffico UDP.</span><span class="sxs-lookup"><span data-stu-id="39f73-149">The second filter collects only UDP traffic.</span></span>

```powershell
$filter1 = New-AzureRmPacketCaptureFilterConfig -Protocol TCP -RemoteIPAddress "1.1.1.1-255.255.255" -LocalIPAddress "10.0.0.3" -LocalPort "1-65535" -RemotePort "20;80;443"
$filter2 = New-AzureRmPacketCaptureFilterConfig -Protocol UDP
```

> [!NOTE]
> <span data-ttu-id="39f73-150">Per un'acquisizione di pacchetti è possibile definire più filtri.</span><span class="sxs-lookup"><span data-stu-id="39f73-150">Multiple filters can be defined for a packet capture.</span></span>

### <a name="step-4"></a><span data-ttu-id="39f73-151">Passaggio 4</span><span class="sxs-lookup"><span data-stu-id="39f73-151">Step 4</span></span>

<span data-ttu-id="39f73-152">Eseguire il cmdlet `New-AzureRmNetworkWatcherPacketCapture` per avviare il processo di acquisizione dei pacchetti, passando i valori richiesti recuperati nei passaggi precedenti.</span><span class="sxs-lookup"><span data-stu-id="39f73-152">Run the `New-AzureRmNetworkWatcherPacketCapture` cmdlet to start the packet capture process, passing the required values retrieved in the preceding steps.</span></span>
```powershell

New-AzureRmNetworkWatcherPacketCapture -NetworkWatcher $networkWatcher -TargetVirtualMachineId $vm.Id -PacketCaptureName "PacketCaptureTest" -StorageAccountId $storageAccount.id -TimeLimitInSeconds 60 -Filters $filter1, $filter2
```

<span data-ttu-id="39f73-153">L'esempio seguente riporta l'output previsto dall'esecuzione del cmdlet `New-AzureRmNetworkWatcherPacketCapture`.</span><span class="sxs-lookup"><span data-stu-id="39f73-153">The following example is the expected output from running the `New-AzureRmNetworkWatcherPacketCapture` cmdlet.</span></span>

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

## <a name="get-a-packet-capture"></a><span data-ttu-id="39f73-154">Ottenere un'acquisizione di pacchetti</span><span class="sxs-lookup"><span data-stu-id="39f73-154">Get a packet capture</span></span>

<span data-ttu-id="39f73-155">L'esecuzione del cmdlet `Get-AzureRmNetworkWatcherPacketCapture` consente di recuperare lo stato di un'acquisizione di pacchetti attualmente in esecuzione o completata.</span><span class="sxs-lookup"><span data-stu-id="39f73-155">Running the `Get-AzureRmNetworkWatcherPacketCapture` cmdlet, retrieves the status of a currently running, or completed packet capture.</span></span>

```powershell
Get-AzureRmNetworkWatcherPacketCapture -NetworkWatcher $networkWatcher -PacketCaptureName "PacketCaptureTest"
```

<span data-ttu-id="39f73-156">L'esempio seguente riporta l'output ottenuto dall'esecuzione del cmdlet `Get-AzureRmNetworkWatcherPacketCapture`.</span><span class="sxs-lookup"><span data-stu-id="39f73-156">The following example is the output from the `Get-AzureRmNetworkWatcherPacketCapture` cmdlet.</span></span> <span data-ttu-id="39f73-157">L'esempio seguente mostra il risultato ottenuto al completamento dell'acquisizione di pacchetti.</span><span class="sxs-lookup"><span data-stu-id="39f73-157">The following example is after the capture is complete.</span></span> <span data-ttu-id="39f73-158">Il valore PacketCaptureStatus è Stopped, mentre il valore StopReason corrisponde a TimeExceeded.</span><span class="sxs-lookup"><span data-stu-id="39f73-158">The PacketCaptureStatus value is Stopped, with a StopReason of TimeExceeded.</span></span> <span data-ttu-id="39f73-159">Questo valore indica che l'acquisizione di pacchetti ha avuto esito positivo ed è stata eseguita per il tempo necessario.</span><span class="sxs-lookup"><span data-stu-id="39f73-159">This value shows that the packet capture was successful and ran its time.</span></span>
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

## <a name="stop-a-packet-capture"></a><span data-ttu-id="39f73-160">Interrompere un'acquisizione di pacchetti</span><span class="sxs-lookup"><span data-stu-id="39f73-160">Stop a packet capture</span></span>

<span data-ttu-id="39f73-161">L'esecuzione del cmdlet `Stop-AzureRmNetworkWatcherPacketCapture` consente di interrompere un'acquisizione di pacchetti in corso.</span><span class="sxs-lookup"><span data-stu-id="39f73-161">By running the `Stop-AzureRmNetworkWatcherPacketCapture` cmdlet, if a capture session is in progress it is stopped.</span></span>

```powershell
Stop-AzureRmNetworkWatcherPacketCapture -NetworkWatcher $networkWatcher -PacketCaptureName "PacketCaptureTest"
```

> [!NOTE]
> <span data-ttu-id="39f73-162">Il cmdlet non restituisce alcuna risposta se eseguito in una sessione di acquisizione in corso o in una sessione esistente che è già stata interrotta.</span><span class="sxs-lookup"><span data-stu-id="39f73-162">The cmdlet returns no response when ran on a currently running capture session or an existing session that has already stopped.</span></span>

## <a name="delete-a-packet-capture"></a><span data-ttu-id="39f73-163">Eliminare un'acquisizione di pacchetti</span><span class="sxs-lookup"><span data-stu-id="39f73-163">Delete a packet capture</span></span>

```powershell
Remove-AzureRmNetworkWatcherPacketCapture -NetworkWatcher $networkWatcher -PacketCaptureName "PacketCaptureTest"
```

> [!NOTE]
> <span data-ttu-id="39f73-164">L'eliminazione di un'acquisizione di pacchetti non elimina il file nell'account di archiviazione.</span><span class="sxs-lookup"><span data-stu-id="39f73-164">Deleting a packet capture does not delete the file in the storage account.</span></span>

## <a name="download-a-packet-capture"></a><span data-ttu-id="39f73-165">Scaricare un'acquisizione di pacchetti</span><span class="sxs-lookup"><span data-stu-id="39f73-165">Download a packet capture</span></span>

<span data-ttu-id="39f73-166">Dopo aver completato la sessione di acquisizione di pacchetti, è possibile scaricare il file di acquisizione nell'archiviazione BLOB o in un file locale nella macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="39f73-166">Once your packet capture session has completed, the capture file can be uploaded to blob storage or to a local file on the VM.</span></span> <span data-ttu-id="39f73-167">La posizione di archiviazione dell'acquisizione di pacchetti viene definita al momento della creazione della sessione.</span><span class="sxs-lookup"><span data-stu-id="39f73-167">The storage location of the packet capture is defined at creation of the session.</span></span> <span data-ttu-id="39f73-168">Uno strumento utile per accedere ai file di acquisizione salvati in un account di archiviazione è Esplora archivi di Microsoft Azure, disponibile qui: http://storageexplorer.com/</span><span class="sxs-lookup"><span data-stu-id="39f73-168">A convenient tool to access these capture files saved to a storage account is Microsoft Azure Storage Explorer, which can be downloaded here:  http://storageexplorer.com/</span></span>

<span data-ttu-id="39f73-169">Se viene specificato un account di archiviazione, i file di acquisizione di pacchetti vengono salvati in un account di archiviazione nel percorso seguente:</span><span class="sxs-lookup"><span data-stu-id="39f73-169">If a storage account is specified, packet capture files are saved to a storage account at the following location:</span></span>

```
https://{storageAccountName}.blob.core.windows.net/network-watcher-logs/subscriptions/{subscriptionId}/resourcegroups/{storageAccountResourceGroup}/providers/microsoft.compute/virtualmachines/{VMName}/{year}/{month}/{day}/packetCapture_{creationTime}.cap
```

## <a name="next-steps"></a><span data-ttu-id="39f73-170">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="39f73-170">Next steps</span></span>

<span data-ttu-id="39f73-171">Per altre informazioni su come automatizzare le acquisizioni di pacchetti tramite gli avvisi della macchina virtuale, leggere l'articolo su come [creare un'acquisizione di pacchetti attivata da un avviso](network-watcher-alert-triggered-packet-capture.md).</span><span class="sxs-lookup"><span data-stu-id="39f73-171">Learn how to automate packet captures with Virtual machine alerts by viewing [Create an alert triggered packet capture](network-watcher-alert-triggered-packet-capture.md)</span></span>

<span data-ttu-id="39f73-172">Per stabilire se un traffico specificato è consentito all'interno o all'esterno di una macchina virtuale, leggere l'articolo su come [controllare la verifica del flusso IP](network-watcher-check-ip-flow-verify-portal.md).</span><span class="sxs-lookup"><span data-stu-id="39f73-172">Find if certain traffic is allowed in orr out of your VM by visiting [Check IP flow verify](network-watcher-check-ip-flow-verify-portal.md)</span></span>

<!-- Image references -->















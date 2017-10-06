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
# <a name="manage-packet-captures-with-azure-network-watcher-using-powershell"></a>Gestire le acquisizioni di pacchetti con Azure Network Watcher tramite PowerShell

> [!div class="op_single_selector"]
> - [Portale di Azure](network-watcher-packet-capture-manage-portal.md)
> - [PowerShell](network-watcher-packet-capture-manage-powershell.md)
> - [Interfaccia della riga di comando 1.0](network-watcher-packet-capture-manage-cli-nodejs.md)
> - [Interfaccia della riga di comando 2.0](network-watcher-packet-capture-manage-cli.md)
> - [API REST di Azure](network-watcher-packet-capture-manage-rest.md)

Acquisizione di pacchetti di rete Watcher consente tooand toocreate acquisizione sessioni tootrack traffico da una macchina virtuale. I filtri vengono forniti per hello acquisizione sessione tooensure che si acquisisce solo il traffico hello desiderato. Acquisizione di pacchetti consente toodiagnose anomalie di rete in modo proattivo e reattivo. Altri usi includono la raccolta di statistiche di rete, ottenere informazioni su intrusioni di rete, client-server toodebug le comunicazioni e molto altro ancora. Essendo in grado di tooremotely trigger pacchetto acquisizioni, questa funzionalità semplifica il carico di hello dell'esecuzione di acquisizione pacchetto eseguita manualmente e nel computer desiderato hello, che consente di risparmiare tempo prezioso.

In questo articolo illustra hello diverse operazioni di gestione che sono attualmente disponibili per l'acquisizione di pacchetti.

- [**Avviare un'acquisizione di pacchetti**](#start-a-packet-capture)
- [**Interrompere un'acquisizione di pacchetti**](#stop-a-packet-capture)
- [**Eliminare un'acquisizione di pacchetti**](#delete-a-packet-capture)
- [**Scaricare un'acquisizione di pacchetti**](#download-a-packet-capture)

## <a name="before-you-begin"></a>Prima di iniziare

Questo articolo si presuppone di che aver hello seguenti risorse:

* Un'istanza del controllo di rete nell'area di hello desiderato toocreate un'acquisizione pacchetti

* Una macchina virtuale con i pacchetti hello acquisire estensione abilitata.

> [!IMPORTANT]
> L'acquisizione di pacchetti richiede un'estensione macchina virtuale `AzureNetworkWatcherExtension`. Per l'installazione dell'estensione hello in una macchina virtuale di Windows, visitare [estensione della macchina virtuale Azure rete Watcher agente per Windows](../virtual-machines/windows/extensions-nwa.md) e per la visita di VM Linux [estensione della macchina virtuale Azure rete Watcher agente per Linux](../virtual-machines/linux/extensions-nwa.md).

## <a name="install-vm-extension"></a>Installare un'estensione di macchina virtuale

### <a name="step-1"></a>Passaggio 1

```powershell
$VM = Get-AzureRmVM -ResourceGroupName testrg -Name VM1
```

### <a name="step-2"></a>Passaggio 2

esempio recupera informazioni sull'estensione di hello Hello necessari hello toorun `Set-AzureRmVMExtension` cmdlet. Questo cmdlet installa l'agente di acquisizione di pacchetti hello in macchina virtuale guest di hello.

> [!NOTE]
> Hello `Set-AzureRmVMExtension` cmdlet potrebbe richiedere diversi minuti toocomplete.

Per le macchine virtuali Windows:

```powershell
$AzureNetworkWatcherExtension = Get-AzureRmVMExtensionImage -Location WestCentralUS -PublisherName Microsoft.Azure.NetworkWatcher -Type NetworkWatcherAgentWindows -Version 1.4.13.0
$ExtensionName = "AzureNetworkWatcherExtension"
Set-AzureRmVMExtension -ResourceGroupName $VM.ResourceGroupName  -Location $VM.Location -VMName $VM.Name -Name $ExtensionName -Publisher $AzureNetworkWatcherExtension.PublisherName -ExtensionType $AzureNetworkWatcherExtension.Type -TypeHandlerVersion $AzureNetworkWatcherExtension.Version.Substring(0,3)
```

Per le macchine virtuali Linux:

```powershell
$AzureNetworkWatcherExtension = Get-AzureRmVMExtensionImage -Location WestCentralUS -PublisherName Microsoft.Azure.NetworkWatcher -Type NetworkWatcherAgentLinux -Version 1.4.13.0
$ExtensionName = "AzureNetworkWatcherExtension"
Set-AzureRmVMExtension -ResourceGroupName $VM.ResourceGroupName  -Location $VM.Location -VMName $VM.Name -Name $ExtensionName -Publisher $AzureNetworkWatcherExtension.PublisherName -ExtensionType $AzureNetworkWatcherExtension.Type -TypeHandlerVersion $AzureNetworkWatcherExtension.Version.Substring(0,3)
````

Hello seguito è riportata una risposta corretta dopo l'esecuzione di hello `Set-AzureRmVMExtension` cmdlet.

```
RequestId IsSuccessStatusCode StatusCode ReasonPhrase
--------- ------------------- ---------- ------------
                         True         OK OK   
```

### <a name="step-3"></a>Passaggio 3

tooensure che hello agente è installato, eseguire hello `Get-AzureRmVMExtension` cmdlet e passare il nome della macchina virtuale hello ed estensione hello.

```powershell
Get-AzureRmVMExtension -ResourceGroupName $VM.ResourceGroupName  -VMName $VM.Name -Name $ExtensionName
```

Hello di esempio seguente è riportato un esempio di risposta hello esecuzione`Get-AzureRmVMExtension`

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

## <a name="start-a-packet-capture"></a>Avviare un'acquisizione di pacchetti

Una volta hello passaggi precedenti, agente di acquisizione di pacchetti hello è installato nella macchina virtuale hello.

### <a name="step-1"></a>Passaggio 1

passaggio successivo Hello è istanza di tooretrieve hello Watcher di rete. Questa variabile viene passata toohello `New-AzureRmNetworkWatcherPacketCapture` cmdlet nel passaggio 4.

```powershell
$nw = Get-AzurermResource | Where {$_.ResourceType -eq "Microsoft.Network/networkWatchers" -and $_.Location -eq "WestCentralUS" }
$networkWatcher = Get-AzureRmNetworkWatcher -Name $nw.Name -ResourceGroupName $nw.ResourceGroupName  
```

### <a name="step-2"></a>Passaggio 2

Recuperare un account di archiviazione. Questo account di archiviazione è file di acquisizione di pacchetti hello toostore utilizzato.

```powershell
$storageAccount = Get-AzureRmStorageAccount -ResourceGroupName testrg -Name testrgsa123
```

### <a name="step-3"></a>Passaggio 3

I filtri possono essere utilizzati toolimit hello i dati archiviati dall'acquisizione di pacchetti hello. Hello esempio due filtri impostati.  Raccoglie un filtro in uscita TCP traffico solo da indirizzo IP locale 10.0.0.3 toodestination porte 20, 80 e 443.  secondo filtro Hello raccoglie solo il traffico UDP.

```powershell
$filter1 = New-AzureRmPacketCaptureFilterConfig -Protocol TCP -RemoteIPAddress "1.1.1.1-255.255.255" -LocalIPAddress "10.0.0.3" -LocalPort "1-65535" -RemotePort "20;80;443"
$filter2 = New-AzureRmPacketCaptureFilterConfig -Protocol UDP
```

> [!NOTE]
> Per un'acquisizione di pacchetti è possibile definire più filtri.

### <a name="step-4"></a>Passaggio 4

Eseguire hello `New-AzureRmNetworkWatcherPacketCapture` cmdlet toostart hello pacchetto acquisizione processo, passando valori hello necessario recuperati in hello passaggi precedenti.
```powershell

New-AzureRmNetworkWatcherPacketCapture -NetworkWatcher $networkWatcher -TargetVirtualMachineId $vm.Id -PacketCaptureName "PacketCaptureTest" -StorageAccountId $storageAccount.id -TimeLimitInSeconds 60 -Filters $filter1, $filter2
```

esempio Hello è output di hello prevista dell'esecuzione hello `New-AzureRmNetworkWatcherPacketCapture` cmdlet.

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

## <a name="get-a-packet-capture"></a>Ottenere un'acquisizione di pacchetti

Esecuzione hello `Get-AzureRmNetworkWatcherPacketCapture` cmdlet recupera informazioni sullo stato hello di un'acquisizione di pacchetti attualmente in esecuzione o è stata completata.

```powershell
Get-AzureRmNetworkWatcherPacketCapture -NetworkWatcher $networkWatcher -PacketCaptureName "PacketCaptureTest"
```

esempio Hello è output hello hello `Get-AzureRmNetworkWatcherPacketCapture` cmdlet. Hello seguito è riportata al termine dell'acquisizione hello. valore PacketCaptureStatus Hello viene arrestato, con un StopReason di TimeExceeded. Questo valore indica che acquisizione pacchetti hello ha avuto esito positivo e il tempo di esecuzione.
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

## <a name="stop-a-packet-capture"></a>Interrompere un'acquisizione di pacchetti

Eseguendo hello `Stop-AzureRmNetworkWatcherPacketCapture` cmdlet, se una sessione di acquisizione è in corso viene arrestata.

```powershell
Stop-AzureRmNetworkWatcherPacketCapture -NetworkWatcher $networkWatcher -PacketCaptureName "PacketCaptureTest"
```

> [!NOTE]
> cmdlet di Hello non restituisce alcuna risposta quando è stato eseguito in una sessione di acquisizione attualmente in esecuzione o di una sessione esistente che è già stato arrestato.

## <a name="delete-a-packet-capture"></a>Eliminare un'acquisizione di pacchetti

```powershell
Remove-AzureRmNetworkWatcherPacketCapture -NetworkWatcher $networkWatcher -PacketCaptureName "PacketCaptureTest"
```

> [!NOTE]
> L'eliminazione di un'acquisizione di pacchetti non elimina il file hello nell'account di archiviazione hello.

## <a name="download-a-packet-capture"></a>Scaricare un'acquisizione di pacchetti

Una volta completata la sessione di acquisizione di pacchetti, hello acquisizione file può essere caricato tooblob tooa o archiviazione locale nella macchina virtuale hello. percorso di archiviazione Hello dell'acquisizione di pacchetti hello è definito al momento della creazione della sessione hello. Tooaccess un utile strumento questi file di acquisizione di account di archiviazione tooa salvato è Microsoft Azure Storage Explorer, che può essere scaricata qui: http://storageexplorer.com/

Se viene specificato un account di archiviazione, i file di acquisizione dei pacchetti vengono salvati tooa account di archiviazione in hello seguente posizione:

```
https://{storageAccountName}.blob.core.windows.net/network-watcher-logs/subscriptions/{subscriptionId}/resourcegroups/{storageAccountResourceGroup}/providers/microsoft.compute/virtualmachines/{VMName}/{year}/{month}/{day}/packetCapture_{creationTime}.cap
```

## <a name="next-steps"></a>Passaggi successivi

Informazioni su come acquisizioni di pacchetti tooautomate con gli avvisi di macchina virtuale visualizzando [creare un'acquisizione pacchetto attivati avvisi](network-watcher-alert-triggered-packet-capture.md)

Per stabilire se un traffico specificato è consentito all'interno o all'esterno di una macchina virtuale, leggere l'articolo su come [controllare la verifica del flusso IP](network-watcher-check-ip-flow-verify-portal.md).

<!-- Image references -->















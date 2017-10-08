---
title: aaaUse una macchina virtuale con Azure PowerShell di risoluzione dei problemi di Windows | Documenti Microsoft
description: Informazioni su come problemi tootroubleshoot macchina virtuale Windows in Azure tramite la connessione di ripristino di tooa dischi hello del sistema operativo VM con Azure PowerShell
services: virtual-machines-windows
documentationCenter: 
authors: genlin
manager: timlt
editor: 
ms.service: virtual-machines-windows
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: infrastructure
ms.date: 05/26/2017
ms.author: genli
ms.openlocfilehash: 7a6a76f64824fe5d06dc4286cb1d87ab8bb794e0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshoot-a-windows-vm-by-attaching-hello-os-disk-tooa-recovery-vm-using-azure-powershell"></a>Risolvere i problemi relativi a una macchina virtuale di Windows tramite il collegamento di ripristino di tooa dischi hello del sistema operativo VM con Azure PowerShell
Se la macchina di virtuale (VM) di Windows in Azure rileva un errore di avvio o un disco, potrebbe essere tooperform risoluzione dei problemi in disco rigido virtuale hello stesso. Un esempio comune sarebbe un aggiornamento di applicazione non riuscita che impedisce hello macchina virtuale in grado di tooboot correttamente. Questo articolo come dettagli toouse Azure PowerShell tooconnect toofix di macchina virtuale Windows tooanother il disco rigido virtuale eventuali errori, quindi ricreare la macchina virtuale originale.


## <a name="recovery-process-overview"></a>Panoramica del processo di ripristino
processo di risoluzione dei problemi di Hello è indicato di seguito:

1. Eliminare hello VM rilevati problemi, mantenendo i dischi rigidi virtuali hello.
2. Collegare e montare hello tooanother di disco rigido virtuale a macchina virtuale di Windows per la risoluzione dei problemi.
3. Connettersi toohello risoluzione dei problemi di macchina virtuale. Modificare i file o eseguire gli strumenti toofix problemi del disco rigido virtuale originale di hello.
4. Smontare e scollegare hello disco rigido virtuale da hello risoluzione dei problemi di macchina virtuale.
5. Creare una macchina virtuale con disco rigido virtuale originale di hello.

Assicurarsi di aver [hello più recente di Azure PowerShell](/powershell/azure/overview) installato e registrato nella sottoscrizione tooyour:

```powershell
Login-AzureRMAccount
```

In hello negli esempi seguenti, sostituire i nomi dei parametri con valori personalizzati. I nomi dei parametri di esempio includono `myResourceGroup`, `mystorageaccount` e `myVM`.


## <a name="determine-boot-issues"></a>Individuare i problemi di avvio
È possibile visualizzare una schermata della macchina virtuale in Azure toohelp di risolvere i problemi di avvio. Questa schermata consente di identificare il motivo di una macchina virtuale ha esito negativo tooboot. Hello seguente esempio mostra come ottenere schermata hello dalla macchina virtuale di Windows denominata hello `myVM` nel gruppo di risorse hello denominato `myResourceGroup`:

```powershell
Get-AzureRmVMBootDiagnosticsData -ResourceGroupName myResourceGroup `
    -Name myVM -Windows -LocalPath C:\Users\ops\
```

Esaminare toodetermine schermata hello hello VM motivi tooboot. Esaminare i messaggi di errore o i codici di errore specifici visualizzati.


## <a name="view-existing-virtual-hard-disk-details"></a>Visualizzare i dettagli del disco rigido virtuale esistente
Prima di poter allegare i tooanother di disco rigido virtuale a macchina virtuale, è necessario il nome hello tooidentify di hello disco rigido virtuale (VHD).

Hello seguente esempio mostra come ottenere informazioni per la macchina virtuale denominata hello `myVM` nel gruppo di risorse hello denominato `myResourceGroup`:

```powershell
Get-AzureRmVM -ResourceGroupName "myResourceGroup" -Name "myVM"
```

Cercare `Vhd URI` all'interno di hello `StorageProfile` sezione dall'output di hello di hello precedente comando. output di esempio troncato seguente Hello Mostra hello `Vhd URI` verso la fine hello del blocco di codice hello:

```powershell
RequestId                     : 8a134642-2f01-4e08-bb12-d89b5b81a0a0
StatusCode                    : OK
ResourceGroupName             : myResourceGroup
Id                            : /subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Compute/virtualMachines/myVM
Name                          : myVM
Type                          : Microsoft.Compute/virtualMachines
...
StorageProfile                :
  ImageReference              :
    Publisher                 : MicrosoftWindowsServer
    Offer                     : WindowsServer
    Sku                       : 2016-Datacenter
    Version                   : latest
  OsDisk                      :
    OsType                    : Windows
    Name                      : myVM
    Vhd                       :
      Uri                     : https://mystorageaccount.blob.core.windows.net/vhds/myVM.vhd
    Caching                   : ReadWrite
    CreateOption              : FromImage
```


## <a name="delete-existing-vm"></a>Eliminare la VM esistente
In Azure, i dischi rigidi virtuali e le macchine virtuali sono due risorse distinte. Un disco rigido virtuale è in cui sono archiviate hello sistema operativo, applicazioni e le configurazioni. Hello macchina virtuale stessa è esclusivamente i metadati che definisce dimensioni hello o il percorso, quindi fa riferimento a risorse, ad esempio un disco rigido virtuale o di una scheda di interfaccia di rete virtuale (NIC). Ogni disco rigido virtuale presenta un lease assegnato quando collegato tooa macchina virtuale. Anche se è possano collegare e scollegare anche durante l'esecuzione di hello VM dischi dati, non è possibile scollegare disco del sistema operativo hello, a meno che non viene eliminato hello risorsa macchina virtuale. lease Hello continua il disco del sistema operativo hello tooassociate con una macchina virtuale, anche quando tale macchina virtuale è in uno stato arrestato e deallocato.

primo passaggio toorecover Hello la macchina virtuale è una risorsa di macchina virtuale hello toodelete stesso. L'eliminazione hello VM lascia i dischi rigidi virtuali hello nell'account di archiviazione. Dopo hello che macchina virtuale viene eliminata, collegare hello disco rigido virtuale tooanother VM tootroubleshoot e risolvere gli errori di hello.

Hello seguente esempio vengono eliminate hello macchina virtuale denominata `myVM` dal gruppo di risorse hello denominato `myResourceGroup`:

```powershell
Remove-AzureRmVM -ResourceGroupName "myResourceGroup" -Name "myVM"
```

Attendere il completamento l'eliminazione prima di collegare il disco rigido virtuale di hello tooanother VM hello macchina virtuale. lease Hello sul disco rigido virtuale hello che associa hello VM deve toobe rilasciati prima di collegare un disco rigido virtuale di hello tooanother macchina virtuale.


## <a name="attach-existing-virtual-hard-disk-tooanother-vm"></a>Collegare tooanother disco rigido virtuale esistente VM
Per hello successivamente alcuni passaggi, si utilizza un'altra macchina virtuale per la risoluzione dei problemi. Per collegare hello toothis di disco rigido virtuale esistente toobrowse VM di risoluzione dei problemi e modificare il contenuto del disco hello. Questo processo consente toocorrect eventuali errori di configurazione o esame delle applicazioni aggiuntive o file di log, ad esempio system. Scegliere o creare un'altra macchina virtuale toouse per la risoluzione dei problemi.

Quando si collega hello disco rigido virtuale esistente, specificare disco toohello di URL hello ottenuto in precedenza hello `Get-AzureRmVM` comando. esempio Hello collega un toohello disco rigido virtuale esistente, risoluzione dei problemi di macchina virtuale denominata `myVMRecovery` nel gruppo di risorse hello denominato `myResourceGroup`:

```powershell
$myVM = Get-AzureRmVM -ResourceGroupName "myResourceGroup" -Name "myVMRecovery"
Add-AzureRmVMDataDisk -VM $myVM -CreateOption "Attach" -Name "DataDisk" -DiskSizeInGB $null `
    -VhdUri "https://mystorageaccount.blob.core.windows.net/vhds/myVM.vhd"
Update-AzureRmVM -ResourceGroup "myResourceGroup" -VM $myVM
```

> [!NOTE]
> Aggiunta di un disco, è necessario dimensioni hello toospecify del disco hello. Come si collega un disco esistente, hello `-DiskSizeInGB` è specificato come `$null`. Questo valore garantisce disco dati hello è correttamente associato e senza hello necessario toodetermine hello dimensione effettiva del disco dati.


## <a name="mount-hello-attached-data-disk"></a>Montare il disco di dati collegato hello

1. Risoluzione dei problemi di macchina virtuale utilizzando le credenziali appropriate hello tooyour RDP. esempio Hello Scarica file di connessione RDP hello per la macchina virtuale denominata hello `myVMRecovery` nel gruppo di risorse hello denominato `myResourceGroup`e lo scarica troppo`C:\Users\ops\Documents`"

    ```powershell
    Get-AzureRMRemoteDesktopFile -ResourceGroupName "myResourceGroup" -Name "myVMRecovery" `
        -LocalPath "C:\Users\ops\Documents\myVMRecovery.rdp"
    ```

2. disco dati Hello viene automaticamente rilevato e collegato. Elenco hello volumi collegati toodetermine hello di lettera di unità come indicato di seguito:

    ```powershell
    Get-Disk
    ```

    Hello output di esempio seguente viene illustrato il disco rigido virtuale di hello connesso un disco **2**. (È anche possibile usare `Get-Volume` lettera di unità hello tooview):

    ```powershell
    Number   Friendly Name   Serial Number   HealthStatus   OperationalStatus   Total Size   Partition
                                                                                             Style
    ------   -------------   -------------   ------------   -----------------   ----------   ----------
    0        Virtual HD                                     Healthy             Online       127 GB MBR
    1        Virtual HD                                     Healthy             Online       50 GB MBR
    2        Msft Virtu...                                  Healthy             Online       127 GB MBR
    ```

## <a name="fix-issues-on-original-virtual-hard-disk"></a>Risolvere i problemi del disco rigido virtuale originale
Con hello esistente disco rigido virtuale montato, è ora possibile eseguire operazioni di manutenzione e risoluzione dei problemi in base alle esigenze. Dopo avere risolto i problemi di hello, continuare con hello alla procedura seguente.


## <a name="unmount-and-detach-original-virtual-hard-disk"></a>Smontare e scollegare il disco rigido virtuale originale
Una volta risolti gli errori, si smontare e Scollega hello disco rigido virtuale esistente dalla VM sulla risoluzione dei problemi. È possibile utilizzare il disco rigido virtuale con qualsiasi altra macchina virtuale finché non viene rilasciato il lease hello collegamento hello disco rigido virtuale toohello risoluzione dei problemi di macchina virtuale.

1. Dalla sessione RDP, smontare disco dati hello nella macchina virtuale di ripristino. È necessario il numero di disco hello da hello precedente `Get-Disk` cmdlet. Utilizzare quindi `Set-Disk` disco come non in linea di tooset hello:

    ```powershell
    Set-Disk -Number 2 -IsOffline $True
    ```

    Verificare il disco di hello è impostato come non in linea utilizzando `Get-Disk` nuovamente. Hello output di esempio seguente viene illustrato il disco di hello è ora impostato come offline:

    ```powershell
    Number   Friendly Name   Serial Number   HealthStatus   OperationalStatus   Total Size   Partition
                                                                                             Style
    ------   -------------   -------------   ------------   -----------------   ----------   ----------
    0        Virtual HD                                     Healthy             Online       127 GB MBR
    1        Virtual HD                                     Healthy             Online       50 GB MBR
    2        Msft Virtu...                                  Healthy             Offline      127 GB MBR
    ```

2. Uscire dalla sessione RDP. Dalla sessione di PowerShell di Azure, rimuovere il disco rigido virtuale di hello hello risoluzione dei problemi di macchina virtuale.

    ```powershell
    $myVM = Get-AzureRmVM -ResourceGroupName "myResourceGroup" -Name "myVMRecovery"
    Remove-AzureRmVMDataDisk -VM $myVM -Name "DataDisk"
    Update-AzureRmVM -ResourceGroup "myResourceGroup" -VM $myVM
    ```


## <a name="create-vm-from-original-hard-disk"></a>Creare una macchina virtuale dal disco rigido originale
utilizzare una macchina virtuale dal disco rigido virtuale originale, toocreate [questo modello di gestione risorse di Azure](https://github.com/Azure/azure-quickstart-templates/tree/master/201-vm-specialized-vhd-existing-vnet). modello JSON effettivi Hello è hello link riportato di seguito:

- https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/201-vm-specialized-vhd-existing-vnet/azuredeploy.json

modello Hello distribuisce una macchina virtuale in una rete virtuale esistente, utilizzando il messaggio hello URL VHD from hello in precedenza di comando. esempio Hello distribuisce hello modello toohello gruppo di risorse `myResourceGroup`:

```powershell
New-AzureRmResourceGroupDeployment -Name myDeployment -ResourceGroupName myResourceGroup `
  -TemplateUri https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/201-vm-specialized-vhd-existing-vnet/azuredeploy.json
```

Hello risposta richiesto per il modello di hello come nome della macchina virtuale, il tipo del sistema operativo e dimensioni della macchina virtuale. Hello `osDiskVhdUri` è hello stesso utilizzato in precedenza durante l'associazione toohello disco rigido virtuale esistente hello risoluzione dei problemi di macchina virtuale.


## <a name="re-enable-boot-diagnostics"></a>Riabilitare la diagnostica di avvio

Quando si crea la macchina virtuale dal disco rigido virtuale esistente di hello, la diagnostica di avvio potrebbe non essere attivata automaticamente. esempio Hello consente hello un'estensione di diagnostica nella macchina virtuale denominata hello `myVMDeployed` nel gruppo di risorse hello denominato `myResourceGroup`:

```powershell
$myVM = Get-AzureRmVM -ResourceGroupName "myResourceGroup" -Name "myVMDeployed"
Set-AzureRmVMBootDiagnostics -ResourceGroupName myResourceGroup -VM $myVM -enable
Update-AzureRmVM -ResourceGroup "myResourceGroup" -VM $myVM
```

## <a name="next-steps"></a>Passaggi successivi
Se si sono verificati problemi di connessione tooyour VM, vedere [tooan connessioni RDP risolvere macchina virtuale di Azure](troubleshoot-rdp-connection.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json). Per problemi relativi all'accesso alle applicazioni in esecuzione nella VM, vedere [Risolvere i problemi di connettività a un'applicazione in una macchina virtuale Windows](troubleshoot-app-connection.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).

Per altre informazioni sull'uso di Resource Manager, vedere [Panoramica di Azure Resource Manager](../../azure-resource-manager/resource-group-overview.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).

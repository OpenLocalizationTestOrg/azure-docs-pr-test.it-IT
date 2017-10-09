## <a name="overview"></a>Panoramica
Quando si crea una nuova macchina virtuale (VM) in un gruppo di risorse tramite la distribuzione di un'immagine da [Azure Marketplace](https://azure.microsoft.com/marketplace/), unità di sistema operativo predefinita hello è di 127 GB. Anche se è possibile tooadd dati dischi toohello VM (seconda quanti hello SKU scelta) e inoltre è consigliato tooinstall applicazioni e carichi di lavoro con utilizzo intensivo della CPU su tali dischi supplemento, spesso i clienti devono tooexpand hello del sistema operativo unità toosupport determinati scenari, ad esempio i seguenti:

1. Supporto di applicazioni legacy che installano componenti nell'unità del sistema operativo.
2. Migrazione di un computer fisico o di una macchina virtuale locali a un'unità del sistema operativo più grande.

> [!IMPORTANT]
> Azure offre due diversi modelli di distribuzione per creare e usare le risorse: Gestione risorse e la distribuzione classica. In questo articolo viene illustrato l'utilizzo del modello di gestione risorse di hello. Si consiglia di utilizzano il modello di gestione risorse hello più nuove distribuzioni.
> 
> 

## <a name="resize-hello-os-drive"></a>Ridimensionare l'unità del sistema operativo hello
In questo articolo si sarà attività hello di ridimensionamento di un'unità hello del sistema operativo tramite i moduli di gestione delle risorse [Azure Powershell](/powershell/azureps-cmdlets-docs). Aprire Powershell ISE della finestra di Powershell in modalità amministrativa e seguire i passaggi di hello riportati di seguito:

1. Accedi tooyour Microsoft Azure in modalità di gestione delle risorse dell'account e selezionare la sottoscrizione, come indicato di seguito:
   
   ```Powershell
   Login-AzureRmAccount
   Select-AzureRmSubscription –SubscriptionName 'my-subscription-name'
   ```
2. Impostare il nome del gruppo di risorse e il nome della VM come segue:
   
   ```Powershell
   $rgName = 'my-resource-group-name'
   $vmName = 'my-vm-name'
   ```
3. Ottenere un tooyour riferimento VM come indicato di seguito:
   
   ```Powershell
   $vm = Get-AzureRmVM -ResourceGroupName $rgName -Name $vmName
   ```
4. Arrestare VM hello prima del ridimensionamento del disco hello come indicato di seguito:
   
    ```Powershell
    Stop-AzureRmVM -ResourceGroupName $rgName -Name $vmName
    ```
5. Di seguito e il momento di hello di che è stato in attesa! Impostare dimensioni hello del valore di hello del sistema operativo del disco toohello desiderato e aggiornare hello VM come indicato di seguito:
   
   ```Powershell
   $vm.StorageProfile.OSDisk.DiskSizeGB = 1023
   Update-AzureRmVM -ResourceGroupName $rgName -VM $vm
   ```
   
   > [!WARNING]
   > nuova dimensione Hello deve essere maggiore di dimensioni del disco esistente hello. Hello massimo consentito è 1023 GB.
   > 
   > 
6. Aggiornamento hello VM potrebbe richiedere alcuni secondi. Una volta terminato il comando hello in esecuzione, riavviare hello VM come indicato di seguito:
   
   ```Powershell
   Start-AzureRmVM -ResourceGroupName $rgName -Name $vmName
   ```

L'operazione è terminata. Ora RDP in hello macchina virtuale, aprire Gestione Computer (o Gestione disco) ed espandere l'unità di hello tramite hello appena allocato.

## <a name="summary"></a>Riepilogo
In questo articolo, abbiamo utilizzato Gestione risorse di Azure i moduli di Powershell tooexpand hello unità del sistema operativo di una macchina virtuale IaaS. Riprodotta sotto è script completo di hello riferimento:

```Powershell
Login-AzureRmAccount
Select-AzureRmSubscription -SubscriptionName 'my-subscription-name'
$rgName = 'my-resource-group-name'
$vmName = 'my-vm-name'
$vm = Get-AzureRmVM -ResourceGroupName $rgName -Name $vmName
Stop-AzureRmVM -ResourceGroupName $rgName -Name $vmName
$vm.StorageProfile.OSDisk.DiskSizeGB = 1023
Update-AzureRmVM -ResourceGroupName $rgName -VM $vm
Start-AzureRmVM -ResourceGroupName $rgName -Name $vmName
```

## <a name="next-steps"></a>Passaggi successivi
Sebbene sia in questo articolo è incentrato principalmente sull'espansione disco hello del sistema operativo della macchina virtuale hello, hello sviluppato script può anche essere usato per l'espansione di hello dati dischi collegati toohello macchina virtuale tramite la modifica di una singola riga di codice. Ad esempio, dati prima di hello tooexpand disco collegato toohello VM, sostituire hello ```OSDisk``` oggetto ```StorageProfile``` con ```DataDisks``` matrice e come utilizzare un tooobtain indice numerico, un disco dati collegato toofirst di riferimento, come illustrato di seguito:

```Powershell
$vm.StorageProfile.DataDisks[0].DiskSizeGB = 1023
```
Analogamente è possibile fare riferimento a altri dati dischi collegati toohello macchina virtuale, è necessario utilizzare un indice, come illustrato in precedenza o hello ```Name``` hello disco come illustrato di seguito:

```Powershell
($vm.StorageProfile.DataDisks | Where {$_.Name -eq 'my-second-data-disk'})[0].DiskSizeGB = 1023
```

Se si desidera toofind out come tooattach dischi tooan VM di Azure Resource Manager, selezionare questa opzione [articolo](../articles/virtual-machines/windows/attach-managed-disk-portal.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).


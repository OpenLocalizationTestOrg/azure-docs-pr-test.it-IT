È possibile connettersi tooa macchina virtuale che viene distribuito tooyour rete virtuale tramite la creazione di una macchina virtuale di tooyour connessione Desktop remoto. Hello migliore tooinitially modo verificare che sia possibile connettersi tooyour macchina virtuale è tooconnect dal relativo IP privati risolvere, anziché il nome di computer. In questo modo, si sta testando toosee se è possibile connettersi, non indica se la risoluzione dei nomi sia configurato correttamente.

1. Individuare l'indirizzo IP privato hello. È possibile trovare l'indirizzo IP privato hello di una macchina virtuale in più modi. Di seguito, vengono illustrati i passaggi di hello per hello portale di Azure e per PowerShell.

  - Portale di Azure - individuare la macchina virtuale nel portale di Azure hello. Visualizzare le proprietà hello hello macchina virtuale. indirizzo IP privato Hello è elencato.

  - PowerShell - tooview di esempio hello di utilizzare un elenco di macchine virtuali e gli indirizzi IP privati da gruppi di risorse. Non è necessario toomodify in questo esempio viene prima di utilizzarlo.

    ```powershell
    $VMs = Get-AzureRmVM
    $Nics = Get-AzureRmNetworkInterface | Where VirtualMachine -ne $null

    foreach($Nic in $Nics)
    {
      $VM = $VMs | Where-Object -Property Id -eq $Nic.VirtualMachine.Id
      $Prv = $Nic.IpConfigurations | Select-Object -ExpandProperty PrivateIpAddress
      $Alloc = $Nic.IpConfigurations | Select-Object -ExpandProperty PrivateIpAllocationMethod
      Write-Output "$($VM.Name): $Prv,$Alloc"
    }
    ```

2. Verificare di essere connessi tooyour rete virtuale mediante una connessione VPN hello.
3. Aprire **connessione Desktop remoto** digitando nella casella di ricerca hello sulla barra delle applicazioni hello "RDP" o "Connessione Desktop remoto", quindi selezionare connessione Desktop remoto. È anche possibile aprire connessione Desktop remoto, uso del comando 'mstsc' hello in PowerShell. 
4. In connessione Desktop remoto, immettere l'indirizzo IP privato hello di hello macchina virtuale. È possibile fare clic su "Mostra opzioni" tooadjust ulteriori impostazioni, quindi connettersi.

### <a name="tootroubleshoot-an-rdp-connection-tooa-vm"></a>tootroubleshoot un tooa connessione RDP VM

Se si riscontrano problemi nella connessione macchina virtuale tooa tramite la connessione VPN, verificare i seguenti di hello:

- Verificare che la connessione VPN sia attiva.
- Verificare che ci si connette l'indirizzo IP privato toohello per hello macchina virtuale.
- Se è possibile connettersi toohello VM con IP privato hello indirizzo, ma non hello Nome computer, verificare che DNS sia stato configurato correttamente. Per altre informazioni sul funzionamento della risoluzione dei nomi per le macchine virtuali, vedere [Risoluzione dei nomi per le macchine virtuali](../articles/virtual-network/virtual-networks-name-resolution-for-vms-and-role-instances.md).
- Per ulteriori informazioni sulle connessioni RDP, vedere [tooa connessioni Desktop remoto di risolvere i problemi VM](../articles/virtual-machines/windows/troubleshoot-rdp-connection.md).

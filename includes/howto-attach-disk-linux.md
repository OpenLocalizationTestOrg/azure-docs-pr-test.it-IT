
Per altre informazioni sui dischi, vedere [Informazioni sui dischi e sui dischi rigidi virtuali per le macchine virtuali](../articles/virtual-machines/linux/about-disks-and-vhds.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).

<a id="attachempty"></a>

## <a name="attach-an-empty-disk"></a>Collegare un disco vuoto
1. Aprire l'interfaccia CLI di Azure 1.0 e [tooyour sottoscrizione di Azure connettersi](../articles/xplat-cli-connect.md). Assicurarsi che sia attiva la modalità Azure Service Management (`azure config mode asm`).
2. Immettere `azure vm disk attach-new` toocreate e collega un nuovo disco, come illustrato nell'esempio seguente hello. Sostituire *myVM* con nome hello la macchina virtuale di Linux e specificare dimensioni di hello del disco hello in GB, ovvero *100GB* in questo esempio:

    ```azurecli
    azure vm disk attach-new myVM 100
    ```

3. Dopo il disco dati hello viene creato e collegato, è elencata nell'output di hello di `azure vm disk list <virtual-machine-name>` come illustrato nell'esempio seguente hello:
   
    ```azurecli
    azure vm disk list TestVM
    ```

    Hello l'output è simile toohello seguente esempio:

    ```bash
    info:    Executing command vm disk list
   
   * Fetching disk images
   * Getting virtual machines
   * Getting VM disks
     data:    Lun  Size(GB)  Blob-Name                         OS
     data:    ---  --------  --------------------------------  -----
     data:         30        myVM-2645b8030676c8f8.vhd  Linux
     data:    0    100       myVM-76f7ee1ef0f6dddc.vhd
     info:    vm disk list command OK
    ```

<a id="attachexisting"></a>

## <a name="attach-an-existing-disk"></a>Collegare un disco esistente
Per collegare un disco esistente, è necessario che in un account di archiviazione sia disponibile un file con estensione vhd.

1. Aprire l'interfaccia CLI di Azure 1.0 e [tooyour sottoscrizione di Azure connettersi](../articles/xplat-cli-connect.md). Assicurarsi che sia attiva la modalità Azure Service Management (`azure config mode asm`).
2. Controllare se hello disco rigido virtuale che si desidera aggiungere tooattach già caricate tooyour sottoscrizione di Azure:
   
    ```azurecli
    azure vm disk list
    ```

    Hello l'output è simile toohello seguente esempio:

    ```azurecli
     info:    Executing command vm disk list
   
   * Fetching disk images
     data:    Name                                          OS
     data:    --------------------------------------------  -----
     data:    myTestVhd                                     Linux
     data:    TestVM-ubuntuVMasm-0-201508060029150744  Linux
     data:    TestVM-ubuntuVMasm-0-201508060040530369
     info:    vm disk list command OK
    ```

3. Se non si trova il disco hello che si desidera toouse, è possibile caricare una sottoscrizione di tooyour disco rigido virtuale locale tramite `azure vm disk create` o `azure vm disk upload`. Un esempio di `disk create` sarebbe come hello di esempio seguente:
   
    ```azurecli
    azure vm disk create myVhd .\TempDisk\test.VHD -l "East US" -o Linux
    ```

    Hello l'output è simile toohello seguente esempio:

    ```azurecli
    info:    Executing command vm disk create
    + Retrieving storage accounts
    info:    VHD size : 10 GB
    info:    Uploading 10485760.5 KB
    Requested:100.0% Completed:100.0% Running:   0 Time:   25s Speed:    82 KB/s
    info:    Finishing computing MD5 hash, 16% is complete.
    info:    https://mystorageaccount.blob.core.windows.net/disks/myVHD.vhd was
    uploaded successfully
    info:    vm disk create command OK
    ```
   
   È inoltre possibile utilizzare `azure vm disk upload` tooupload un account di archiviazione specifico tooa disco rigido virtuale. Leggere ulteriori informazioni su hello comandi toomanage i dischi di dati della macchina virtuale di Azure [qui](https://docs.microsoft.com/cli/azure/get-started-with-az-cli2).

4. Ora si collega hello desiderato macchina virtuale tooyour di disco rigido virtuale:
   
    ```azurecli
    azure vm disk attach myVM myVhd
    ```
   
   Verificare che tooreplace *myVM* con nome hello della macchina virtuale e *myVHD* con il disco rigido virtuale desiderato.

5. È possibile verificare il disco di hello è collegato toohello la macchina virtuale con `azure vm disk list <virtual-machine-name>`:
   
    ```azurecli
    azure vm disk list myVM
    ```

    Hello l'output è simile toohello seguente esempio:

    ```azurecli
     info:    Executing command vm disk list
   
   * Fetching disk images
   * Getting virtual machines
   * Getting VM disks
     data:    Lun  Size(GB)  Blob-Name                         OS
     data:    ---  --------  --------------------------------  -----
     data:         30        TestVM-2645b8030676c8f8.vhd  Linux
     data:    1    10        test.VHD
     data:    0    100        TestVM-76f7ee1ef0f6dddc.vhd
     info:    vm disk list command OK
    ```

> [!NOTE]
> Dopo aver aggiunto un disco dati, è necessario sarà necessario toolog nella macchina virtuale toohello e inizializzare disco hello macchina virtuale hello consentono di usare per l'archiviazione disco hello (vedere hello seguendo i passaggi per altre informazioni su come toodo inizializzare disco hello).
> 
> 


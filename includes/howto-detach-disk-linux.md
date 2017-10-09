Quando non è più necessario un disco dati collegato tooa virtual machine (VM), è possibile scollegarlo facilmente. Quando si scollega un disco da hello VM, hello disco non è stato rimosso dall'archivio. Se si desiderano nuovamente toouse hello esistente dati hello disco, è possibile ricollegarlo toohello stessa macchina virtuale o un altro.  

> [!NOTE]
> Una macchina virtuale in Azure usa diversi tipi di dischi, ad esempio un disco del sistema operativo, un disco temporaneo locale e un disco dati facoltativo. Per informazioni dettagliate, vedere [Informazioni sui dischi e sui dischi rigidi virtuali per le macchine virtuali](../articles/virtual-machines/linux/about-disks-and-vhds.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json). A meno che non si elimina anche hello VM non è possibile scollegare un disco del sistema operativo.

## <a name="find-hello-disk"></a>Trovare il disco hello
Prima di poter scollegare un disco da una macchina virtuale è necessario toofind out hello numero LUN, che è un identificatore hello disco toobe scollegato. toodo che, seguire questi passaggi:

1. Aprire l'interfaccia CLI di Azure e [tooyour sottoscrizione di Azure connettersi](../articles/xplat-cli-connect.md). Assicurarsi che sia attiva la modalità Azure Service Management (`azure config mode asm`).
2. Individuare i dischi collegati tooyour macchina virtuale. Hello esempio seguente vengono elencati i dischi per la macchina virtuale denominata hello `myVM`:

    ```azurecli
    azure vm disk list myVM
    ```

    Hello l'output è simile toohello seguente esempio:

    ```azurecli
    * Fetching disk images
    * Getting virtual machines
    * Getting VM disks
      data:    Lun  Size(GB)  Blob-Name                         OS
      data:    ---  --------  --------------------------------  -----
      data:         30        ubuntuVM-2645b8030676c8f8.vhd  Linux
      data:    0    30        myDataDisk.vhd
      info:    vm disk list command OK
    ```

3. Si noti hello LUN o hello **numero di unità logica** per disco hello che si desidera toodetach.

## <a name="remove-operating-system-references-toohello-disk"></a>Rimuovere il disco di sistema operativo riferimenti toohello
Prima di scollegare il disco hello Guest Linux hello, è necessario assicurarsi che tutte le partizioni disco hello non sono in uso. Verificare che il sistema operativo hello non tooremount loro dopo il riavvio. Questi passaggi Annulla configurazione hello probabilmente creato quando [collegamento](../articles/virtual-machines/linux/classic/attach-disk.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json) disco hello.

1. Hello utilizzare `lsscsi` identificatore di comando toodiscover hello del disco. `lsscsi` può essere installato tramite `yum install lsscsi` (su distribuzioni basate su Red Hat) o `apt-get install lsscsi` (su distribuzioni basate su Debian). È possibile trovare l'identificatore del disco hello desiderata utilizzando il numero LUN hello. ultimo numero di Hello nella tupla hello in ogni riga è hello LUN. Nel seguente esempio di hello `lsscsi`, LUN 0 esegue il mapping troppo*dev/sdc*

    ```bash
    [1:0:0:0]    cd/dvd  Msft     Virtual CD/ROM   1.0   /dev/sr0
    [2:0:0:0]    disk    Msft     Virtual Disk     1.0   /dev/sda
    [3:0:1:0]    disk    Msft     Virtual Disk     1.0   /dev/sdb
    [5:0:0:0]    disk    Msft     Virtual Disk     1.0   /dev/sdc
    ```

2. Utilizzare `fdisk -l <disk>` partizioni hello toodiscover associate hello disco toobe scollegato. esempio Hello Mostra output di hello per `/dev/sdc`:

    ```bash
    Disk /dev/sdc: 1098.4 GB, 1098437885952 bytes, 2145386496 sectors
    Units = sectors of 1 * 512 = 512 bytes
    Sector size (logical/physical): 512 bytes / 512 bytes
    I/O size (minimum/optimal): 512 bytes / 512 bytes
    Disk label type: dos
    Disk identifier: 0x5a1d2a1a
    
        Device Boot      Start         End      Blocks   Id  System
    /dev/sdc1            2048  2145386495  1072692224   83  Linux
    ```

3. Smonta ogni partizione per disco hello. Smonta Hello esempio `/dev/sdc1`:

    ```bash
    sudo umount /dev/sdc1
    ```

4. Hello utilizzare `blkid` comando toodiscovery hello UUID per tutte le partizioni. Hello l'output è simile toohello seguente esempio:

    ```bash
    /dev/sda1: UUID="11111111-1b1b-1c1c-1d1d-1e1e1e1e1e1e" TYPE="ext4"
    /dev/sdb1: UUID="22222222-2b2b-2c2c-2d2d-2e2e2e2e2e2e" TYPE="ext4"
    /dev/sdc1: UUID="33333333-3b3b-3c3c-3d3d-3e3e3e3e3e3e" TYPE="ext4"
    ```

5. Rimuovere le voci in hello **/e così via/fstab** file associato con i percorsi di dispositivo hello o UUID per tutte le partizioni per hello disco toobe scollegato.  Le voci per questo esempio potrebbero essere:

    ```sh  
   UUID=33333333-3b3b-3c3c-3d3d-3e3e3e3e3e3e   /datadrive   ext4   defaults   1   2
   ```

    oppure
   
   ```sh   
   /dev/sdc1   /datadrive   ext4   defaults   1   2
   ```

## <a name="detach-hello-disk"></a>Scollegare il disco hello
Dopo aver trovato il numero LUN hello del disco di hello e i riferimenti del sistema operativo hello rimosso, si è pronti toodetach è:

1. Scollegare il disco selezionato di hello dalla macchina virtuale hello eseguendo il comando hello `azure vm disk detach
   <virtual-machine-name> <LUN>`. Nell'esempio seguente viene Hello scollegato LUN `0` dalla macchina virtuale denominata hello `myVM`:
   
    ```azurecli
    azure vm disk detach myVM 0
    ```

2. È possibile verificare se il disco hello ottenuto disconnessa eseguendo `azure vm disk list` nuovamente. Hello seguente esempio viene controllato hello macchina virtuale denominata `myVM`:
   
    ```azurecli
    azure vm disk list myVM
    ```

    l'output è simile toohello seguente esempio, disco dati hello non è più allegato Hello:

    ```azurecli
    info:    Executing command vm disk list
   
   * Fetching disk images
   * Getting virtual machines
   * Getting VM disks
     data:    Lun  Size(GB)  Blob-Name                         OS
     data:    ---  --------  --------------------------------  -----
     data:         30        ubuntuVM-2645b8030676c8f8.vhd  Linux
     info:    vm disk list command OK
    ```

disco Hello scollegato rimane nel servizio di archiviazione ma non è più macchine virtuali tooa associata.


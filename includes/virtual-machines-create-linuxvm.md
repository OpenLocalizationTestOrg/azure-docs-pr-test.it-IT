
1. Accedi tooyour sottoscrizione di Azure seguendo i passaggi di hello elencati [connettersi tooAzure da hello Azure CLI 1.0](../articles/xplat-cli-connect.md).

2. Verificare di disporre in modalità di distribuzione classica hello come indicato di seguito:

    ```azurecli
    azure config mode asm
    ```

3. Scoprire immagine Linux hello che si desidera tooload dalle immagini disponibili hello come indicato di seguito:

   ```azurecli   
    azure vm image list | grep "Linux"
    ```
   
    In una finestra del prompt dei comandi di Windows usare **find** anziché grep.
   
4. Utilizzare `azure vm create` toocreate una macchina virtuale con immagine di Linux hello dall'elenco precedente hello. Questo passaggio crea un servizio cloud e un account di archiviazione. È possibile connettersi questo servizio cloud di esistente tooan macchina virtuale con un `-c` opzione. Creare un toolog endpoint SSH nella macchina virtuale di Linux toohello con hello `-e` opzione. esempio Hello crea una macchina virtuale denominata `myVM` utilizzando hello `Ubuntu-14_04_4-LTS` immagine hello `West US` posizione e aggiunge un nome utente `ops`:
   
    ```azurecli
    azure vm create myVM \
        b39f27a8b8c64d52b05eac6a62ebad85__Ubuntu-14_04_4-LTS-amd64-server-20160516-en-us-30GB \
        -g ops -p P@ssw0rd! -z "Small" -e -l "West US"
    ```

    Hello l'output è simile toohello seguente esempio:

    ```azurecli
    info:    Executing command vm create
    + Looking up image b39f27a8b8c64d52b05eac6a62ebad85__Ubuntu-14_04_4-LTS-amd64-server-20160516-en-us-30GB
    + Looking up cloud service
    info:    cloud service myVM not found.
    + Creating cloud service
    + Retrieving storage accounts
    + Creating VM
    info:    vm create command OK
    ```
   
   > [!NOTE]
   > Per una macchina virtuale Linux, è necessario fornire hello `-e` opzione `vm create`. Non è possibile tooenable SSH dopo che è stata creata la macchina virtuale hello. Per ulteriori dettagli su SSH, leggere [come tooUse SSH con Linux in Azure](../articles/virtual-machines/linux/mac-create-ssh-keys.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).

5. È possibile verificare gli attributi di hello di hello VM utilizzando hello `azure vm show` comando. Hello seguente esempio vengono restituite informazioni per la macchina virtuale denominata hello `myVM`:

    ```azurecli   
    azure vm show myVM
    ```

6. Avviare la macchina virtuale con hello `azure vm start` comando come segue:

    ```azurecli
    azure vm start myVM
    ```

## <a name="next-steps"></a>Passaggi successivi
Per informazioni dettagliate su tutti questi comandi di macchina virtuale di Azure CLI 1.0, leggere hello [Using hello Azure CLI 1.0 con l'API della distribuzione classica hello](https://docs.microsoft.com/cli/azure/get-started-with-az-cli2).


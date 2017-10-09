


In questo argomento viene spiegato come:

* Inserire dati in una macchina virtuale (VM) di Azure durante il provisioning.
* Recuperare i dati sia in Windows che in Linux.
* Utilizzare strumenti speciali su alcuni sistemi toodetect e gestisce automaticamente i dati personalizzati.

> [!NOTE]
> Questo articolo descrive i dati come personalizzati possono essere inserite utilizzando una macchina virtuale creata con hello API di gestione del servizio di Azure. toosee toouse hello API di gestione risorse di Azure, vedere [il modello di esempio hello](https://github.com/Azure/azure-quickstart-templates/tree/master/101-vm-customdata).
> 
> 

## <a name="injecting-custom-data-into-your-azure-virtual-machine"></a>Inserimento di dati personalizzati nella macchina virtuale di Azure
Questa funzionalità è attualmente supportata solo in hello [interfaccia della riga di comando di Azure](https://github.com/Azure/azure-xplat-cli). Verrà creato un `custom-data.txt` file che contiene i dati, quindi inserire che in toohello VM durante il provisioning. Anche se è possibile utilizzare una delle opzioni di hello per hello `azure vm create` comando seguente hello viene illustrato un approccio molto semplice:

```
    azure vm create <vmname> <vmimage> <username> <password> \  
    --location "West US" --ssh 22 \  
    --custom-data ./custom-data.txt  
```


## <a name="using-custom-data-in-hello-virtual-machine"></a>Utilizza dati personalizzata nella macchina virtuale hello
* Se la macchina virtuale di Azure è una macchina virtuale basata su Windows, quindi hello dati personalizzato viene salvato troppo`%SYSTEMDRIVE%\AzureData\CustomData.bin`. Sebbene sia con codifica base64 tootransfer da hello computer locale toohello nuova macchina virtuale, viene automaticamente decodificati e può essere aperta o utilizzati immediatamente.
  
  > [!NOTE]
  > Se il file hello esiste, viene sovrascritto. protezione Hello hello directory è stata impostata troppo**System: Full Control** e **Administrators: Full Control**.
  > 
  > 
* Se la macchina virtuale di Azure è una macchina virtuale basata su Linux, il file di dati personalizzati hello si troverà uno dei seguenti hello inserisce a seconda del tipo di distribuzione. dati Hello potrebbero essere con codifica base64, potrebbe essere necessario innanzitutto dati hello toodecode:
  
  * `/var/lib/waagent/ovf-env.xml`
  * `/var/lib/waagent/CustomData`
  * `/var/lib/cloud/instance/user-data.txt` 

## <a name="cloud-init-on-azure"></a>Inizializzazione cloud di Azure
Se la macchina virtuale di Azure da un'immagine Ubuntu o CoreOS, è possibile utilizzare CustomData toosend una configurazione cloud toocloud-init. Se il file di dati personalizzato è uno script, cloud-init può semplicemente eseguirlo.

### <a name="ubuntu-cloud-images"></a>Immagini di Ubuntu Cloud
Nella maggior parte delle immagini Linux di Azure, è necessario modificare "/ etc/waagent.conf" tooconfigure hello temporaneo su disco e lo scambio file di risorse. Per altre informazioni, vedere [Guida dell'utente dell'agente Linux di Azure](../articles/virtual-machines/linux/agent-user-guide.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).

Le immagini di Cloud Ubuntu hello, tuttavia, è necessario utilizzare cloud init tooconfigure hello risorsa disco (vale a dire hello "temporaneo") e spazio di swapping partizione. Vedere hello seguente pagina nel sito wiki Ubuntu hello per altri dettagli: [AzureSwapPartitions](https://wiki.ubuntu.com/AzureSwapPartitions).

<!--Every topic should have next steps and links toohello next logical set of content tookeep hello customer engaged-->
## <a name="next-steps-using-cloud-init"></a>Passaggi successivi: Utilizzo cloud-init
Per ulteriori informazioni, vedere hello [cloud init documentazione per Ubuntu](https://help.ubuntu.com/community/CloudInit).

<!--Link references-->
[Aggiungere il riferimento all'API REST di gestione del servizio ruolo](http://msdn.microsoft.com/library/azure/jj157186.aspx)

[Interfaccia della riga di comando di Azure](https://github.com/Azure/azure-xplat-cli)


Prima di poter usare hello CLI di Azure con Gestione risorse toodeploy Azure comandi e i modelli di risorse e i carichi di lavoro con i gruppi di risorse, è necessario un account con Azure. Se non si dispone di un account, è possibile ottenere un [Azure qui versione di valutazione gratuita](https://azure.microsoft.com/pricing/free-trial/).

Se non è ancora installato hello Azure CLI e sottoscrizione tooyour connessi, vedere [installazione hello Azure CLI](../articles/cli-install-nodejs.md) impostare modalità hello troppo`arm` con `azure config mode arm`e connettersi tooAzure con hello `azure login` comando.

## <a name="cli-versions-toocomplete-hello-task"></a>Attività hello toocomplete versioni CLI
È possibile completare l'attività hello utilizzando una delle seguenti versioni CLI hello:

- CLI di Azure 10: l'interfaccia CLI per hello classic risorse Gestione modelli di distribuzione e (in questo articolo)
- [Azure CLI 2.0](../articles/virtual-machines/linux/cli-manage.md) -la prossima generazione CLI per modello di distribuzione di gestione risorse hello

## <a name="basic-azure-resource-manager-commands-in-azure-cli"></a>Comandi di base di Azure Resource Manager nell'interfaccia della riga di comando di Azure
In questo articolo vengono illustrati i comandi di base verrà toouse con toomanage CLI di Azure che desideri interagire con le risorse (principalmente le macchine virtuali) nella sottoscrizione di Azure.  Per più dettagliate della Guida dei parametri della riga di comando specifici e sulle opzioni, è possibile utilizzare la Guida in linea di comando hello e opzioni digitando `azure <command> <subcommand> --help` o `azure help <command> <subcommand>`.

> [!NOTE]
> Questi esempi non includono operazioni basate su modelli che sono in genere consigliate per distribuzioni di macchine virtuali in Gestione risorse. Per informazioni, vedere [hello utilizzare CLI di Azure con Azure Resource Manager](../articles/xplat-cli-azure-resource-manager.md) e [distribuire e gestire macchine virtuali utilizzando modelli di gestione risorse di Azure e hello Azure CLI](../articles/virtual-machines/linux/create-ssh-secured-vm-from-template.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).
> 
> 

| Attività | Gestione risorse |
| --- | --- | --- |
| Creare hello più basic per VM |`azure vm quick-create [options] <resource-group> <name> <location> <os-type> <image-urn> <admin-username> <admin-password>`<br/><br/>(Ottenere hello `image-urn` da hello `azure vm image list` comando. Vedere [questo articolo](../articles/virtual-machines/linux/cli-ps-findimage.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) per esempi. |
| Creare una macchina virtuale Linux |`azure  vm create [options] <resource-group> <name> <location> -y "Linux"` |
| Creare un'app Windows |`azure  vm create [options] <resource-group> <name> <location> -y "Windows"` |
| Elenco delle macchine virtuali |`azure  vm list [options]` |
| Visualizzare informazioni su una macchina virtuale |`azure  vm show [options] <resource_group> <name>` |
| Avviare una macchina virtuale |`azure vm start [options] <resource_group> <name>` |
| Arrestare una macchina virtuale |`azure vm stop [options] <resource_group> <name>` |
| Deallocare una macchina virtuale |`azure vm deallocate [options] <resource-group> <name>` |
| Riavviare una macchina virtuale |`azure vm restart [options] <resource_group> <name>` |
| Eliminare una macchina virtuale |`azure vm delete [options] <resource_group> <name>` |
| Acquisire una macchina virtuale |`azure vm capture [options] <resource_group> <name>` |
| Creare una macchina virtuale da un'immagine dell'utente |`azure  vm create [options] –q <image-name> <resource-group> <name> <location> <os-type>` |
| Creare una macchina virtuale da un disco specializzato |`azue  vm create [options] –d <os-disk-vhd> <resource-group> <name> <location> <os-type>` |
| Aggiungere un tooa disco dati VM |`azure  vm disk attach-new [options] <resource-group> <vm-name> <size-in-gb> [vhd-name]` |
| Rimuovere un disco dati da una macchina virtuale |`azure  vm disk detach [options] <resource-group> <vm-name> <lun>` |
| Aggiungere un tooa di estensione generico VM |`azure  vm extension set [options] <resource-group> <vm-name> <name> <publisher-name> <version>` |
| Aggiungere l'accesso alla VM estensione tooa VM |`azure vm reset-access [options] <resource-group> <name>` |
| Aggiungere tooa estensione Docker VM |`azure  vm docker create [options] <resource-group> <name> <location> <os-type>` |
| Rimuovere un'estensione di macchina virtuale |`azure  vm extension set [options] –u <resource-group> <vm-name> <name> <publisher-name> <version>` |
| Ottenere l'utilizzo delle risorse della macchina virtuale |`azure vm list-usage [options] <location>` |
| Ottenere tutte le dimensioni delle macchine virtuali disponibili |`azure vm sizes [options]` |

## <a name="next-steps"></a>Passaggi successivi
* Per ulteriori esempi di comandi CLI hello a oltrepassare la gestione di base VM, vedere [Using hello CLI di Azure con Azure Resource Manager](../articles/virtual-machines/azure-cli-arm-commands.md).

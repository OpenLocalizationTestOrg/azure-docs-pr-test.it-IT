---
title: aaaCapture toouse una macchina virtuale Linux di Azure come modello | Documenti Microsoft
description: Informazioni su come toocapture e generalizzare un'immagine di una basata su Linux Azure macchina virtuale (VM) creata con modello di distribuzione Azure Resource Manager hello.
services: virtual-machines-linux
documentationcenter: 
author: iainfoulds
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: e608116f-f478-41be-b787-c2ad91b5a802
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.topic: article
ms.date: 02/09/2017
ms.author: iainfou
ms.openlocfilehash: 877eee5c842bebe80e755c2240cdaaef4ade6ff5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="capture-a-linux-virtual-machine-running-on-azure"></a>Acquisire una VM Linux in esecuzione su Azure
Seguire i passaggi hello in toogeneralize questo articolo e acquisire una macchina virtuale Linux di Azure (VM) in modello di distribuzione di gestione risorse di hello. Quando si generalizza hello macchina virtuale, si rimuovere informazioni sull'account personale e si prepara hello VM toobe utilizzato come immagine. È quindi l'acquisizione dell'immagine di un disco rigido virtuale generalizzato (VHD) per hello del sistema operativo, i dischi rigidi virtuali per i dischi dati collegati, e un [modello di gestione risorse](../../azure-resource-manager/resource-group-overview.md) per nuove distribuzioni di macchine Virtuali. In questo articolo illustra in dettaglio come immagine toocapture una macchina virtuale con hello Azure CLI 1.0 per una macchina virtuale tramite dischi non gestiti. È anche possibile [acquisire una macchina virtuale con dischi di Azure gestiti hello Azure CLI 2.0](capture-image.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json). Dischi gestiti vengono gestiti dal hello piattaforma Azure e non richiedono alcun toostore preparazione o percorso li. Per altre informazioni, vedere [Azure Managed Disks Overview](../windows/managed-disks-overview.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) (Panoramica di Azure Managed Disks). 

toocreate macchine virtuali con immagine di hello, configurare le risorse di rete per ogni nuova macchina virtuale e utilizzare toodeploy modello (un file JavaScript Object Notation o JSON) hello dalla hello acquisita immagini VHD. In questo modo, è possibile replicare una macchina virtuale con la configurazione corrente di software, analogamente toohello usare immagini in hello Azure Marketplace.

> [!TIP]
> Se si desidera toocreate una copia della VM Linux esistente con il relativo stato specializzato per il backup o il debug, vedere [creare una copia di una macchina virtuale di Linux in esecuzione in Azure](copy-vm.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json). Se si desidera tooupload un VHD Linux da una macchina virtuale locale, vedere [caricare e creare una VM Linux dall'immagine del disco personalizzato](upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).  

## <a name="cli-versions-toocomplete-hello-task"></a>Attività hello toocomplete versioni CLI
È possibile completare l'attività hello utilizzando una delle seguenti versioni CLI hello:

- [Azure CLI 1.0](#before-you-begin) : l'interfaccia CLI per hello classic risorse Gestione modelli di distribuzione e (in questo articolo)
- [Azure CLI 2.0](capture-image.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) -la prossima generazione CLI per modello di distribuzione di gestione risorse hello

## <a name="before-you-begin"></a>Prima di iniziare
Verificare che siano soddisfatti hello seguenti prerequisiti:

* **Macchina virtuale di Azure creata nel modello di distribuzione di gestione risorse di hello** -se è stata creata una VM Linux, è possibile utilizzare hello [portale](quick-create-portal.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json), hello [CLI di Azure](quick-create-cli.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json), o [Gestione risorse modelli](create-ssh-secured-vm-from-template.md). 
  
    Configurare hello macchina virtuale in base alle esigenze. Ad esempio, [aggiungere dischi dati](add-disk.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json), applicare aggiornamenti e installare applicazioni. 
* **CLI di Azure** -Install hello [CLI di Azure](../../cli-install-nodejs.md) in un computer locale.

## <a name="step-1-remove-hello-azure-linux-agent"></a>Passaggio 1: Rimuovere l'agente Linux di Azure hello
Eseguire innanzitutto hello **waagent** con hello **deprovisioning** parametro hello VM Linux. Questo comando Elimina i file e dati toomake hello VM pronto per la generalizzazione. Per informazioni dettagliate, vedere hello [Guida dell'utente dell'agente Linux di Azure](../windows/agent-user-guide.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).

1. Connettersi tooyour VM Linux utilizzando un client SSH.
2. Nella finestra di hello SSH, digitare hello comando seguente:
   
    ```bash
    sudo waagent -deprovision+user
    ```
   > [!NOTE]
   > Solo il seguente comando in una macchina virtuale che si desidera toocapture come immagine. Non garantisce che l'immagine hello viene cancellato di tutte le informazioni riservate o adatto per la ridistribuzione.
 
3. Tipo **y** toocontinue. È possibile aggiungere hello **-force** tooavoid parametro questo passaggio di conferma.
4. Al termine del comando di hello, digitare **uscire**. Questo passaggio consente di chiudere client SSH hello.

## <a name="step-2-capture-hello-vm"></a>Passaggio 2: Acquisizione hello VM
Utilizzare toogeneralize CLI di Azure hello e acquisire hello macchina virtuale. In hello negli esempi seguenti, sostituire i nomi dei parametri di esempio con i valori desiderati. I nomi dei parametri di esempio includono **myResourceGroup**, **myVnet** e **myVM**.

1. Dal computer locale, aprire hello Azure CLI e [tooyour accesso sottoscrizione di Azure](../../xplat-cli-connect.md). 
2. Verificare di essere in modalità Resource Manager.
   
    ```azurecli
    azure config mode arm
    ```
3. Arrestare hello macchina virtuale che già deprovisioning utilizzando hello comando seguente:
   
    ```azurecli
    azure vm deallocate -g myResourceGroup -n myVM
    ```
4. Generalizzare hello VM con hello comando seguente:
   
    ```azurecli
    azure vm generalize -g myResourceGroup -n myVM
    ```
5. A questo punto eseguire hello **acquisizione macchina virtuale di azure** comando, che acquisisce hello macchina virtuale. Nell'esempio seguente di hello, immagine hello vengono acquisiti i dischi rigidi virtuali con nomi che iniziano con **MyVHDNamePrefix**, hello e **-t** opzione specifica un modello di percorso toohello **MyTemplate.json**. 
   
    ```azurecli
    azure vm capture -g myResourceGroup -n myVM -p myVHDNamePrefix -t myTemplate.json
    ```
   
   > [!IMPORTANT]
   > i file VHD di Hello immagine vengono creati per impostazione predefinita in hello stesso account di archiviazione che hello VM originale utilizzato. Hello utilizzare *stesso account di archiviazione* toostore hello dischi rigidi virtuali per nuove macchine virtuali create da immagini hello. 

6. percorso di hello toofind di un'immagine acquisita, il modello JSON hello aperto in un editor di testo. In hello **storageProfile**, trovare hello **uri** di hello **immagine** si trova in hello **sistema** contenitore. Ad esempio, hello URI dell'immagine del disco del sistema operativo hello è simile troppo`https://xxxxxxxxxxxxxx.blob.core.windows.net/system/Microsoft.Compute/Images/vhds/MyVHDNamePrefix-osDisk.xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx.vhd`

## <a name="step-3-create-a-vm-from-hello-captured-image"></a>Passaggio 3: Creare una macchina virtuale dall'immagine acquisita hello
Ora è possibile utilizzare immagini hello con un toocreate modello una VM Linux. Questi passaggi mostrano come toouse hello Azure CLI e hello modello file JSON acquisita toocreate hello VM in una nuova rete virtuale.

### <a name="create-network-resources"></a>Creare risorse di rete
modello di hello toouse, è necessario innanzitutto tooset di una rete virtuale e una scheda di rete per la nuova macchina virtuale. È consigliabile che creare un gruppo di risorse per tali risorse in posizione hello in cui memorizzare l'immagine di macchina virtuale. Eseguire i comandi simile toohello seguente, sostituendo i nomi per le risorse e un percorso appropriato di Azure ("centralus" in questi comandi):

```azurecli
azure group create myResourceGroup1 -l "centralus"

azure network vnet create myResourceGroup1 myVnet -l "centralus"

azure network vnet subnet create myResourceGroup1 myVnet mySubnet

azure network public-ip create myResourceGroup1 myPublicIP -l "centralus"

azure network nic create myResourceGroup1 myNIC -k mySubnet -m myVnet -p myPublicIP -l "centralus"
```

### <a name="get-hello-id-of-hello-nic"></a>Ottenere l'Id di hello NIC hello
toodeploy una macchina virtuale dall'immagine hello utilizzando hello JSON è stato salvato durante l'acquisizione, è necessario hello Id di hello scheda di rete. Ottenerlo eseguendo hello comando seguente:

```azurecli
azure network nic show myResourceGroup1 myNIC
```

Hello **Id** hello output è analogo troppo`/subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourceGroups/MyResourceGroup1/providers/Microsoft.Network/networkInterfaces/myNic`

### <a name="create-a-vm"></a>Creare una macchina virtuale
Dopo il comando che segue hello esecuzione toocreate la macchina virtuale da hello acquisito l'immagine di macchina virtuale. Hello utilizzare **-f** parametro toospecify hello percorso toohello modello JSON file salvato.

```azurecli
azure group deployment create myResourceGroup1 MyDeployment -f MyTemplate.json
```

Nell'output del comando hello, sono richieste toosupply un nuovo nome della macchina virtuale, nome utente amministratore di hello e una password e Id della scheda di rete creato in precedenza hello hello.

```bash
info:    Executing command group deployment create
info:    Supply values for hello following parameters
vmName: myNewVM
adminUserName: myAdminuser
adminPassword: ********
networkInterfaceId: /subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resource Groups/myResourceGroup1/providers/Microsoft.Network/networkInterfaces/myNic
```

Hello seguente esempio viene illustrato ciò che viene visualizzato per una corretta distribuzione:

```bash
+ Initializing template configurations and parameters
+ Creating a deployment
info:    Created template deployment xxxxxxx
+ Waiting for deployment toocomplete
data:    DeploymentName     : MyDeployment
data:    ResourceGroupName  : MyResourceGroup1
data:    ProvisioningState  : Succeeded
data:    Timestamp          : xxxxxxx
data:    Mode               : Incremental
data:    Name                Type          Value

data:    ------------------  ------------  -------------------------------------

data:    vmName              String        myNewVM

data:    vmSize              String        Standard_D1

data:    adminUserName       String        myAdminuser

data:    adminPassword       SecureString  undefined

data:    networkInterfaceId  String        /subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourceGroups/MyResourceGroup1/providers/Microsoft.Network/networkInterfaces/myNic
info:    group deployment create command OK
```

### <a name="verify-hello-deployment"></a>Verificare la distribuzione di hello
Ora SSH toohello macchina virtuale è stato creato distribuzione hello tooverify e iniziare a usare hello nuova macchina virtuale. tooconnect tramite SSH, trovare l'indirizzo IP di hello di hello macchina virtuale creata tramite l'esecuzione di hello comando seguente:

```azurecli
azure network public-ip show myResourceGroup1 myPublicIP
```

indirizzo IP pubblico Hello è elencato nella finestra di output del comando hello. Per impostazione predefinita si connetterà toohello VM Linux da SSH sulla porta 22.

## <a name="create-additional-vms"></a>Creare altre macchine virtuali
Hello utilizzare acquisiti toodeploy immagine e il modello di altre macchine virtuali utilizzando i passaggi di hello hello precedente sezione. Altre opzioni toocreate macchine virtuali, dall'immagine hello includono utilizzando un modello di avvio rapido o l'esecuzione di hello **macchina virtuale di azure creare** comando.

### <a name="use-hello-captured-template"></a>Modello di hello acquisita
hello toouse acquisiti immagine e il modello, seguire questi passaggi (descritta in dettaglio nella precedente sezione hello):

* Verificare che l'immagine di macchina virtuale sia in hello stesso account di archiviazione che ospita VHD virtuale della macchina.
* Copiare i file JSON del modello di hello e specificare un nome univoco per il disco del sistema operativo hello del hello nuova macchina virtuale disco rigido virtuale (o i dischi rigidi virtuali). Ad esempio, in hello **storageProfile**, in **vhd**nella **uri**, specificare un nome univoco per hello **osDisk** disco rigido virtuale, simile troppo`https://xxxxxxxxxxxxxx.blob.core.windows.net/vhds/MyNewVHDNamePrefix-osDisk.xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx.vhd`
* Creare una scheda di rete in uno hello stesso o in un'altra rete virtuale.
* Utilizza file JSON di hello modificato del modello, creare una distribuzione nel gruppo di risorse hello in cui impostare la rete virtuale hello.

### <a name="use-a-quickstart-template"></a>Uso di un modello di Guida introduttiva
Se si desidera configurare automaticamente quando si crea una macchina virtuale dall'immagine hello rete di hello, è possibile specificare tali risorse in un modello. Ad esempio, vedere hello [101 vm da utente immagine modello](https://github.com/Azure/azure-quickstart-templates/tree/master/101-vm-from-user-image) da GitHub. Questo modello consente di creare una macchina virtuale dall'immagine personalizzata e rete virtuale necessaria hello, indirizzo IP pubblico e le risorse di interfaccia di rete. Per una procedura dettagliata dell'utilizzo di modello hello in hello portale di Azure, vedere [come una macchina virtuale da un'immagine personalizzata utilizzando un modello di gestione risorse toocreate](http://codeisahighway.com/how-to-create-a-virtual-machine-from-a-custom-image-using-an-arm-template/).

### <a name="use-hello-azure-vm-create-command"></a>Utilizzare hello azure vm creare un comando
In genere è più semplice toouse toocreate di modello una macchina virtuale dall'immagine hello un gestore delle risorse. Tuttavia, è possibile creare VM hello *in modo imperativo* utilizzando hello **macchina virtuale di azure creare** con hello **-Q** (**-immagine urn**) parametro . Se si utilizza questo metodo, è anche passare hello **-d** (**- os-disco-disco rigido virtuale**) percorso hello toospecify di parametro del file con estensione vhd hello del sistema operativo per hello nuova macchina virtuale. Questo file deve essere nel contenitore di dischi rigidi virtuali hello hello dell'account di archiviazione in cui è archiviato i file VHD dell'immagine hello. comando copie hello VHD per hello Hello nuova macchina virtuale automaticamente toohello **dischi rigidi virtuali** contenitore.

Prima di eseguire **macchina virtuale di azure creare** con immagine di hello, completare hello alla procedura seguente:

1. Creare un gruppo di risorse, o identificare un gruppo di risorse esistente per la distribuzione di hello.
2. Creare un pubblico risorsa indirizzo IP e una risorsa NIC per hello nuova macchina virtuale. Per passaggi toocreate rete virtuale, un indirizzo IP di pubblico e NIC mediante hello CLI, vedere più indietro in questo articolo. (**macchina virtuale di azure creare** inoltre possibile creare una scheda di rete, ma è necessario toopass di parametri aggiuntivi per una rete virtuale e una subnet.)

Quindi eseguire un comando che passa gli URI tooboth hello nuovo disco rigido virtuale del sistema operativo file e hello immagine esistente. In questo esempio viene creata una dimensione VM Standard_A1 nell'area Stati Uniti orientali hello.

```azurecli
azure vm create -g myResourceGroup1 -n myNewVM -l eastus -y Linux \
-z Standard_A1 -u myAdminname -p myPassword -f myNIC \
-d "https://xxxxxxxxxxxxxx.blob.core.windows.net/vhds/MyNewVHDNamePrefix.vhd" \
-Q "https://xxxxxxxxxxxxxx.blob.core.windows.net/system/Microsoft.Compute/Images/vhds/MyVHDNamePrefix-osDisk.vhd"
```

Per altre opzioni del comando, eseguire `azure help vm create`.

## <a name="next-steps"></a>Passaggi successivi
toomanage le macchine virtuali con hello CLI, vedere attività hello [distribuire e gestire macchine virtuali utilizzando modelli di gestione risorse di Azure e hello Azure CLI](create-ssh-secured-vm-from-template.md).


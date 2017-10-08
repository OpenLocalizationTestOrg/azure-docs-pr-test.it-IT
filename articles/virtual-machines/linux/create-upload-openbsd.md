---
title: aaaCreate e caricamento di una VM OpenBSD immagine tooAzure | Documenti Microsoft
description: Informazioni su come toocreate e caricare un disco rigido virtuale (VHD) che contiene hello OpenBSD del sistema operativo toocreate una macchina virtuale di Azure mediante Azure CLI
services: virtual-machines-linux
documentationcenter: 
author: KylieLiang
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 1ef30f32-61c1-4ba8-9542-801d7b18e9bf
ms.service: virtual-machines-linux
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure-services
ms.date: 05/24/2017
ms.author: kyliel
ms.openlocfilehash: 0524f45ea1ecec37e55cbe9d54438a571a831de7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="create-and-upload-an-openbsd-disk-image-tooazure"></a>Creare e caricare un tooAzure di immagine disco OpenBSD
Questo articolo illustra come toocreate e caricare un disco rigido virtuale (VHD) che contiene hello OpenBSD del sistema operativo. Dopo aver caricato il, è possibile utilizzare, come la propria toocreate immagine una macchina virtuale (VM) in Azure mediante Azure CLI.


## <a name="prerequisites"></a>Prerequisiti
Questo articolo si presuppone di aver hello seguenti elementi:

* **Una sottoscrizione Azure**: se non è già disponibile un account, è possibile crearne uno in pochi minuti. Se si ha un abbonamento a MSDN, vedere [Credito Azure mensile per sottoscrittori di Visual Studio](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/). In caso contrario, informazioni su come troppo[creare un account di prova](https://azure.microsoft.com/pricing/free-trial/).  
* **Azure CLI 2.0** -assicurarsi di disporre di più recente hello [CLI di Azure 2.0](/cli/azure/install-azure-cli) installato e registrato nel tooyour account Azure con [accesso az](/cli/azure/#login).
* **Sistema operativo OpenBSD installato in un file con estensione vhd** -un sistema operativo OpenBSD (6.1 versione) deve essere il disco rigido virtuale di tooa installato. Più strumenti esistono toocreate file con estensione vhd. Ad esempio, è possibile usare una soluzione di virtualizzazione, ad esempio file con estensione vhd di Hyper-V toocreate hello e installare hello del sistema operativo. Per istruzioni su come tooinstall e utilizzare Hyper-V, vedere [installare Hyper-V e creare una macchina virtuale](http://technet.microsoft.com/library/hh846766.aspx).


## <a name="prepare-openbsd-image-for-azure"></a>Preparare l'immagine OpenBSD per Azure
Nella macchina virtuale in cui è installato hello OpenBSD sistema operativo 6.1, aggiunto il supporto di Hyper-V, hello completare hello seguire le procedure seguenti:

1. Se DHCP non è abilitato durante l'installazione, abilitare il servizio hello come segue:

    ```sh    
    echo dhcp > /etc/hostname.hvn0
    ```

2. Configurare una console seriale come segue:

    ```sh
    echo "stty com0 115200" >> /etc/boot.conf
    echo "set tty com0" >> /etc/boot.conf
    ```

3. Configurare l'installazione del pacchetto come segue:

    ```sh
    echo "https://ftp.openbsd.org/pub/OpenBSD" > /etc/installurl
    ```
   
4. Per impostazione predefinita, hello `root` utente è disabilitato nelle macchine virtuali in Azure. Gli utenti possono eseguire i comandi con privilegi elevati tramite hello `doas` comando OpenBSD VM. Doas è abilitato per impostazione predefinita. Per altre informazioni, vedere [doas.conf](http://man.openbsd.org/doas.conf.5). 

5. Installare e configurare i prerequisiti per l'agente di Azure hello come indicato di seguito:

    ```sh
    pkg_add py-setuptools openssl git
    ln -sf /usr/local/bin/python2.7 /usr/local/bin/python
    ln -sf /usr/local/bin/python2.7-2to3 /usr/local/bin/2to3
    ln -sf /usr/local/bin/python2.7-config /usr/local/bin/python-config
    ln -sf /usr/local/bin/pydoc2.7  /usr/local/bin/pydoc
    ```

6. versione più recente di Hello di hello agente di Azure è sempre disponibile nel [Github](https://github.com/Azure/WALinuxAgent/releases). Installare l'agente hello come indicato di seguito:

    ```sh
    git clone https://github.com/Azure/WALinuxAgent 
    cd WALinuxAgent
    python setup.py install
    waagent -register-service
    ```

    > [!IMPORTANT]
    > Dopo aver installato l'agente di Azure, è un tooverify buona norma che è in esecuzione come indicato di seguito:
    >
    > ```bash
    > ps auxw | grep waagent
    > root     79309  0.0  1.5  9184 15356 p1  S      4:11PM    0:00.46 python /usr/local/sbin/waagent -daemon (python2.7)
    > cat /var/log/waagent.log
    > ```

7. Deprovisioning hello tooclean di sistema e verificare che è adatto per la riconfigurazione. Hello seguente comando Elimina inoltre ultimo account di provisioning utente hello e dati hello associata:

    ```sh
    waagent -deprovision+user -force
    ```

Ora è possibile arrestare la macchina virtuale.


## <a name="prepare-hello-vhd"></a>Preparare hello disco rigido virtuale
formato VHDX Hello non è supportato solo in Azure, **disco rigido virtuale fisso**. È possibile convertire formato VHD, hello disco toofixed tramite Hyper-V Manager oppure Powershell hello [convert-vhd](https://technet.microsoft.com/itpro/powershell/windows/hyper-v/convert-vhd) cmdlet. Di seguito è riportato un esempio.

```powershell
Convert-VHD OpenBSD61.vhdx OpenBSD61.vhd -VHDType Fixed
```

## <a name="create-storage-resources-and-upload"></a>Creare e caricare risorse di archiviazione
Creare prima un gruppo di risorse con [az group create](/cli/azure/group#create). esempio Hello crea un gruppo di risorse denominato *myResourceGroup* in hello *eastus* percorso:

```azurecli
az group create --name myResourceGroup --location eastus
```

tooupload il disco rigido virtuale, creare un account di archiviazione con [creare account di archiviazione az](/cli/azure/storage/account#create). Il nome dell'account di archiviazione deve essere univoco; assegnare quindi all'account il proprio nome. esempio Hello crea un account di archiviazione denominato *mystorageaccount*:

```azurecli
az storage account create --resource-group myResourceGroup \
    --name mystorageaccount \
    --location eastus \
    --sku Premium_LRS
```

toocontrol accedere toohello account di archiviazione, ottenere la chiave di archiviazione hello con [elenco di chiavi di account di archiviazione az](/cli/azure/storage/account/keys#list) come indicato di seguito:

```azurecli
STORAGE_KEY=$(az storage account keys list \
    --resource-group myResourceGroup \
    --account-name mystorageaccount \
    --query "[?keyName=='key1']  | [0].value" -o tsv)
```

hello separato toologically i dischi rigidi virtuali, caricare, creare un contenitore nell'account di archiviazione hello con [creare il contenitore di archiviazione az](/cli/azure/storage/container#create):

```azurecli
az storage container create \
    --name vhds \
    --account-name mystorageaccount \
    --account-key ${STORAGE_KEY}
```

Caricare infine il disco rigido virtuale con [az storage blob upload](/cli/azure/storage/blob#upload) come segue:

```azurecli
az storage blob upload \
    --container-name vhds \
    --file ./OpenBSD61.vhd \
    --name OpenBSD61.vhd \
    --account-name mystorageaccount \
    --account-key ${STORAGE_KEY}
```


## <a name="create-vm-from-your-vhd"></a>Creare una macchina virtuale dal disco rigido virtuale
È possibile creare una macchina virtuale con un [script di esempio](../scripts/virtual-machines-linux-cli-sample-create-vm-vhd.md) o direttamente con [az vm create](/cli/azure/vm#create). toospecify hello OpenBSD VHD caricato, utilizzare hello `--image` parametro come indicato di seguito:

```azurecli
az vm create \
    --resource-group myResourceGroup \
    --name myOpenBSD61 \
    --image "https://mystorageaccount.blob.core.windows.net/vhds/OpenBSD61.vhd" \
    --os-type linux \
    --admin-username azureuser \
    --ssh-key-value ~/.ssh/id_rsa.pub
```

Ottenere l'indirizzo IP hello per le VM OpenBSD con [az vm gli indirizzi ip elenco](/cli/azure/vm#list-ip-addresses) come indicato di seguito:

```azurecli
az vm list-ip-addresses --resource-group myResourceGroup --name myOpenBSD61
```

È ora possibile SSH tooyour OpenBSD VM come di consueto:
        
```bash
ssh azureuser@<ip address>
```


## <a name="next-steps"></a>Passaggi successivi
Se si desidera ulteriori informazioni su Hyper-V supporta in OpenBSD6.1 tooknow, leggere [OpenBSD 6.1](https://www.openbsd.org/61.html) e [hyperv.4](http://man.openbsd.org/hyperv.4).

Se si desidera toocreate una macchina virtuale dal disco gestito, leggere [disco az](/cli/azure/disk). 

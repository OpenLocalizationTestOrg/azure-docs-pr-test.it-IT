---
title: macchine virtuali Linux di aaaMonitor in Azure | Documenti Microsoft
description: Informazioni su come toomonitor avvio metriche delle prestazioni e diagnostica in una macchina virtuale di Linux in Azure
services: virtual-machines-linux
documentationcenter: virtual-machines
author: davidmu1
manager: timlt
editor: tysonn
tags: azure-resource-manager
ms.assetid: 
ms.service: virtual-machines-linux
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure
ms.date: 05/08/2017
ms.author: davidmu
ms.custom: mvc
ms.openlocfilehash: 282da0f03ab0bf37bd44750c22813ca8d1c89560
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="how-toomonitor-a-linux-virtual-machine-in-azure"></a>Come toomonitor una macchina virtuale di Linux in Azure

tooensure che eseguono correttamente le macchine virtuali (VM) in Azure, è possibile esaminare le metriche delle prestazioni e diagnostica di avvio. In questa esercitazione si apprenderà come:

> [!div class="checklist"]
> * Abilitare la diagnostica di avvio su hello VM
> * Visualizzare la diagnostica di avvio
> * Visualizzare le metriche host
> * Abilitare l'estensione di diagnostica per hello VM
> * Visualizzare le metriche della macchina virtuale
> * Creare avvisi basati sulle metriche di diagnostica
> * Configurare il monitoraggio avanzato


[!INCLUDE [cloud-shell-try-it.md](../../../includes/cloud-shell-try-it.md)]

Se si sceglie tooinstall e utilizza hello CLI in locale, questa esercitazione, è necessario che sia in esecuzione hello Azure CLI versione 2.0.4 o versioni successive. Eseguire `az --version` versione hello toofind. Se è necessario tooinstall o l'aggiornamento, vedere [installare Azure CLI 2.0]( /cli/azure/install-azure-cli). 

## <a name="create-vm"></a>Creare una macchina virtuale

diagnostica toosee e metriche in azione, è necessario una macchina virtuale. Creare prima un gruppo di risorse con [az group create](/cli/azure/group#create). esempio Hello crea un gruppo di risorse denominato *myResourceGroupMonitor* in hello *eastus* percorso.

```azurecli-interactive 
az group create --name myResourceGroupMonitor --location eastus
```

Creare quindi una macchina virtuale con il comando [az vm create](https://docs.microsoft.com/cli/azure/vm#create). esempio Hello crea una macchina virtuale denominata *myVM*:

```azurecli-interactive 
az vm create \
  --resource-group myResourceGroupMonitor \
  --name myVM \
  --image UbuntuLTS \
  --admin-username azureuser \
  --generate-ssh-keys
```

## <a name="enable-boot-diagnostics"></a>Abilitare la diagnostica di avvio

Come avviare le macchine virtuali Linux, estensione di diagnostica di avvio hello acquisisce l'output di avvio e lo archivia nell'archiviazione di Azure. Questi dati possono essere utilizzati tootroubleshoot problemi di avvio VM. Diagnostica di avvio non è abilitata automaticamente quando si crea una VM Linux di hello CLI di Azure.

Prima di abilitare la diagnostica di avvio, un account di archiviazione deve toobe creato per l'archiviazione dei log di avvio. Gli account di archiviazione devono avere un nome univoco globale, che abbia tra i 3 e i 24 caratteri e devono contenere solo numeri e lettere minuscole. Creare un account di archiviazione con hello [creare account di archiviazione az](/cli/azure/storage/account#create) comando. In questo esempio, una stringa casuale è toocreate utilizzati un nome di account di archiviazione univoco. 

```azurecli-interactive 
storageacct=mydiagdata$RANDOM

az storage account create \
  --resource-group myResourceGroupMonitor \
  --name $storageacct \
  --sku Standard_LRS \
  --location eastus
```

Quando si abilita la diagnostica di avvio, è necessario contenitore di archiviazione blob toohello hello URI. Hello seguenti query di comando hello tooreturn account di archiviazione questo URI. valore dell'URI Hello viene archiviato nei nomi di variabili *bloburi*, che viene utilizzato nel passaggio successivo hello.

```azurecli-interactive 
bloburi=$(az storage account show --resource-group myResourceGroupMonitor --name $storageacct --query 'primaryEndpoints.blob' -o tsv)
```

Abilitare ora la diagnostica di avvio con [az vm boot-diagnostics enable](https://docs.microsoft.com/cli/azure/vm/boot-diagnostics#enable). Hello `--storage` valore è il blob hello URI raccolti nel passaggio precedente hello.

```azurecli-interactive 
az vm boot-diagnostics enable \
  --resource-group myResourceGroupMonitor \
  --name myVM \
  --storage $bloburi
```


## <a name="view-boot-diagnostics"></a>Visualizzare la diagnostica di avvio

Quando è abilitata la diagnostica di avvio, ogni volta che si arresta e avvia hello VM, informazioni sul processo di avvio hello viene scritto il file di log tooa. Per questo esempio, prima deallocare hello VM con hello [az vm deallocare](/cli/azure/vm#deallocate) comando come segue:

```azurecli-interactive 
az vm deallocate --resource-group myResourceGroupMonitor --name myVM
```

Ora avviare hello VM con hello [inizio vm az]( /cli/azure/vm#stop) comando come segue:

```azurecli-interactive 
az vm start --resource-group myResourceGroupMonitor --name myVM
```

È possibile ottenere dati di diagnostica di avvio hello per *myVM* con hello [az vm get diagnostica di avvio-avvio-log](https://docs.microsoft.com/cli/azure/vm/boot-diagnostics#get-boot-log) comando come segue:

```azurecli-interactive 
az vm boot-diagnostics get-boot-log --resource-group myResourceGroupMonitor --name myVM
```


## <a name="view-host-metrics"></a>Visualizzare le metriche host

Una macchina virtuale Linux è un host dedicato in Azure con cui interagisce. Le metriche vengono automaticamente raccolte per host hello e possono essere visualizzate nel portale di Azure hello come indicato di seguito:

1. Nel portale di Azure hello, fare clic su **gruppi di risorse**selezionare **myResourceGroupMonitor**, quindi selezionare **myVM** nell'elenco di risorse hello.
1. toosee come macchina virtuale host hello viene eseguita, fare clic su **metriche** nel pannello VM hello, quindi selezionare una qualsiasi delle hello *[Host]* metriche in **le metriche disponibili**.

    ![Visualizzare le metriche host](./media/tutorial-monitoring/monitor-host-metrics.png)


## <a name="install-diagnostics-extension"></a>Installare l'estensione di diagnostica

> [!IMPORTANT]
> Questo documento descrive versione 2.3 di hello estensione diagnostica per Linux, che è stato deprecato. La versione 2.3 sarà supportata fino al 30 giugno 2018.
>
> Versione 3.0 di hello che estensione diagnostica per Linux può invece essere abilitato. Per ulteriori informazioni, vedere [hello documentazione](./diagnostic-extension.md).

le metriche di base host Hello sono disponibili, ma toosee più granulare e metriche specifiche di macchina virtuale, si tooneed tooinstall hello Azure estensione diagnostica per hello VM. Hello estensione diagnostica di Azure consente un monitoraggio aggiuntivo e toobe di dati di diagnostica recuperati hello macchina virtuale. È possibile visualizzare queste misurazioni delle prestazioni e creare avvisi basati sulle modalità di funzionamento hello macchina virtuale. estensione di diagnostica Hello viene installata tramite il portale di Azure hello come segue:

1. Nel portale di Azure hello, fare clic su **gruppi di risorse**selezionare **myResourceGroup**, quindi selezionare **myVM** nell'elenco di risorse hello.
1. Fare clic su **Impostazioni di diagnostica**. elenco di Hello mostra che *diagnostica di avvio* è già stata abilitata dalla sezione precedente hello. Fare clic sulla casella di controllo hello *metriche base*.
1. In hello *account di archiviazione* sezione, passare hello selezionare tooand *mydiagdata [1234]* account creato nella sezione precedente hello.
1. Fare clic su hello **salvare** pulsante.

    ![Visualizzare le metriche di diagnostica](./media/tutorial-monitoring/enable-diagnostics-extension.png)


## <a name="view-vm-metrics"></a>Visualizzare le metriche della macchina virtuale

È possibile visualizzare le metriche VM hello in hello allo stesso modo visualizzato metriche di hello host macchina virtuale:

1. Nel portale di Azure hello, fare clic su **gruppi di risorse**selezionare **myResourceGroup**, quindi selezionare **myVM** nell'elenco di risorse hello.
1. toosee come hello macchina virtuale viene eseguita, fare clic su **metriche** hello pannello VM e quindi selezionare una delle metriche di diagnostica hello in **le metriche disponibili**.

    ![Visualizzare le metriche della macchina virtuale](./media/tutorial-monitoring/monitor-vm-metrics.png)


## <a name="create-alerts"></a>Creare avvisi

È possibile creare avvisi basati sulle metriche di prestazioni specifiche. Gli avvisi possono essere ad esempio toonotify utilizzato per l'utilizzo medio della CPU supera una determinata soglia o spazio su disco disponibile scende di sotto di una certa quantità. Gli avvisi vengono visualizzati nel portale di Azure hello o possono essere inviati tramite posta elettronica. È inoltre possibile attivare i runbook di automazione di Azure o Azure logica App in tooalerts risposta in corso la generazione.

Hello seguente viene creato un avviso per l'utilizzo medio della CPU.

1. Nel portale di Azure hello, fare clic su **gruppi di risorse**selezionare **myResourceGroup**, quindi selezionare **myVM** nell'elenco di risorse hello.
2. Fare clic su **regole di avviso** nel pannello VM hello, quindi fare clic su **Aggiungi avviso metrica** in alto di hello del pannello avvisi hello.
4. Inserire un **Nome** per l'avviso, ad esempio *myAlertRule*
5. tootrigger un avviso quando la percentuale della CPU supera 1.0 per cinque minuti, lasciare hello tutti gli altri valori predefiniti selezionati.
6. Facoltativamente, selezionare la casella di hello per *i proprietari, collaboratori e lettori di posta elettronica* toosend notifica di posta elettronica. azione predefinita Hello è toopresent una notifica nel portale di hello.
7. Fare clic su hello **OK** pulsante.


## <a name="advanced-monitoring"></a>Monitoraggio avanzato 

È possibile eseguire un monitoraggio più approfondito della macchina virtuale tramite [Operations Management Suite](https://docs.microsoft.com/azure/operations-management-suite/operations-management-suite-overview). Se non è già stato fatto, è possibile iscriversi per avere una [versione di prova gratuita](https://www.microsoft.com/en-us/cloud-platform/operations-management-suite-trial) di Operations Management Suite.

Quando si dispone di accesso toohello OMS portale, è possibile trovare l'identificatore di chiave e dell'area di lavoro dell'area di lavoro hello nel pannello impostazioni hello. Sostituire < chiave dell'area di lavoro > e < id area di lavoro > con i valori hello per le OMS è possibile utilizzare area di lavoro e quindi **az vm estensione set** tooadd hello OMS estensione toohello VM:

```azurecli-interactive 
az vm extension set \
  --resource-group myResourceGroupMonitor \
  --vm-name myVM \
  --name OmsAgentForLinux \
  --publisher Microsoft.EnterpriseCloud.Monitoring \
  --version 1.3 \
  --protected-settings '{"workspaceKey": "<workspace-key>"}' \
  --settings '{"workspaceId": "<workspace-id>"}'
```

Nel Pannello di hello ricerca nei Log del portale OMS hello, dovrebbe essere *myVM* , ad esempio quello mostrato nella seguente immagine hello:

![Pannello OMS](./media/tutorial-monitoring/tutorial-monitor-oms.png)

## <a name="next-steps"></a>Passaggi successivi

In questa esercitazione le macchine virtuali sono state configurate ed esaminate con il Centro sicurezza di Azure. Si è appreso come:

> [!div class="checklist"]
> * Abilitare la diagnostica di avvio su hello VM
> * Visualizzare la diagnostica di avvio
> * Visualizzare le metriche host
> * Abilitare l'estensione di diagnostica per hello VM
> * Visualizzare le metriche della macchina virtuale
> * Creare avvisi basati sulle metriche di diagnostica
> * Configurare il monitoraggio avanzato

Spostare toohello toolearn esercitazione successiva sul Centro protezione di Azure.

> [!div class="nextstepaction"]
> [Gestire la sicurezza delle VM](./tutorial-azure-security.md)
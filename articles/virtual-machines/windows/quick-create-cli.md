---
title: Avvio rapido - aaaAzure creare CLI VM di Windows | Documenti Microsoft
description: Informazioni toocreate rapidamente una macchina virtuale di Windows con hello CLI di Azure.
services: virtual-machines-windows
documentationcenter: virtual-machines
author: neilpeterson
manager: timlt
editor: tysonn
tags: azure-resource-manager
ms.assetid: 
ms.service: virtual-machines-windows
ms.devlang: na
ms.topic: hero-article
ms.tgt_pltfrm: vm-windows
ms.workload: infrastructure
ms.date: 05/11/2017
ms.author: nepeters
ms.custom: mvc
ms.openlocfilehash: 029bdecec219b12b80b958ceeedda214f1b13149
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-windows-virtual-machine-with-hello-azure-cli"></a>Creare una macchina virtuale Windows con hello CLI di Azure

Hello CLI di Azure viene utilizzato toocreate e gestire le risorse di Azure dalla riga di comando hello o negli script. Questa guida descrive l'utilizzo di una macchina virtuale in esecuzione Windows Server 2016 hello Azure CLI toodeploy. Una volta completata la distribuzione, è connettersi toohello server e installare IIS.

Se non si ha una sottoscrizione di Azure, creare un [account gratuito](https://azure.microsoft.com/free/?WT.mc_id=A261C142F) prima di iniziare.


[!INCLUDE [cloud-shell-try-it.md](../../../includes/cloud-shell-try-it.md)]

Se si sceglie tooinstall e utilizza hello CLI in locale, questa Guida rapida richiede che sia in esecuzione hello Azure CLI versione 2.0.4 o versioni successive. Eseguire `az --version` versione hello toofind. Se è necessario tooinstall o l'aggiornamento, vedere [installare Azure CLI 2.0]( /cli/azure/install-azure-cli). 


## <a name="create-a-resource-group"></a>Creare un gruppo di risorse

Come prima cosa creare un gruppo di risorse con [az group create](/cli/azure/group#create). Un gruppo di risorse di Azure è un contenitore logico in cui le risorse di Azure vengono distribuite e gestite. 

esempio Hello crea un gruppo di risorse denominato *myResourceGroup* in hello *eastus* percorso.

```azurecli-interactive 
az group create --name myResourceGroup --location eastus
```

## <a name="create-virtual-machine"></a>Crea macchina virtuale

Creare una VM con il comando [az vm create](/cli/azure/vm#create). 

esempio Hello crea una macchina virtuale denominata *myVM*. Questo esempio viene utilizzato *azureuser* per un nome utente amministrativo e *myPassword12* come password hello. Aggiornare questi ambiente appropriato tooyour toosomething di valori. Questi valori sono necessari quando si crea una connessione con la macchina virtuale hello.

```azurecli-interactive 
az vm create --resource-group myResourceGroup --name myVM --image win2016datacenter --admin-username azureuser --admin-password myPassword12
```

Quando è stato creato hello VM, hello CLI di Azure Mostra toohello di informazioni simili esempio seguente. Prendere nota di hello `publicIpAaddress`. Questo indirizzo è utilizzato tooaccess hello macchina virtuale.

```azurecli-interactive 
{
  "fqdns": "",
  "id": "/subscriptions/d5b9d4b7-6fc1-0000-0000-000000000000/resourceGroups/myResourceGroup/providers/Microsoft.Compute/virtualMachines/myVM",
  "location": "eastus",
  "macAddress": "00-0D-3A-23-9A-49",
  "powerState": "VM running",
  "privateIpAddress": "10.0.0.4",
  "publicIpAddress": "52.174.34.95",
  "resourceGroup": "myResourceGroup"
}
```

## <a name="open-port-80-for-web-traffic"></a>Aprire la porta 80 per il traffico Web 

Per impostazione predefinita sono consentite solo le connessioni RDP in tooWindows le macchine virtuali distribuite in Azure. Se questa macchina virtuale verrà toobe un server Web, è necessario tooopen la porta 80 da hello Internet. Hello utilizzare [az vm aprire porte](/cli/azure/vm#open-port) comando tooopen hello desiderato porta.  
 
 ```azurecli-interactive  
az vm open-port --port 80 --resource-group myResourceGroup --name myVM
```


## <a name="connect-toovirtual-machine"></a>Connettere la macchina toovirtual

Comando che segue di hello utilizzare toocreate una sessione desktop remota con la macchina virtuale hello. Sostituire l'indirizzo IP hello con indirizzo IP pubblico hello della macchina virtuale. Quando richiesto, immettere le credenziali di hello utilizzate durante la creazione di macchine virtuali hello.

```bash 
mstsc /v:<Public IP Address>
```

## <a name="install-iis-using-powershell"></a>Installare IIS tramite PowerShell

Ora che è stato effettuato in toohello macchina virtuale di Azure, è possibile utilizzare una singola riga di PowerShell tooinstall IIS e abilitare il traffico web tooallow di hello firewall locale regola. Aprire un prompt dei comandi di PowerShell ed eseguire hello comando seguente:

```powershell
Install-WindowsFeature -name Web-Server -IncludeManagementTools
```

## <a name="view-hello-iis-welcome-page"></a>Hello Visualizza la pagina iniziale di IIS

Con IIS installato e la porta 80 è aperta nella VM da hello Internet, è possibile utilizzare un browser web la pagina iniziale tooview scelte hello predefinita IIS. Impossibile verificare toouse hello indirizzo IP pubblico che descritto in precedenza pagina predefinita di toovisit hello. 

![Sito IIS predefinito](./media/quick-create-powershell/default-iis-website.png) 

## <a name="clean-up-resources"></a>Pulire le risorse

Quando non è più necessario, è possibile utilizzare hello [eliminazione gruppo az](/cli/azure/group#delete) comando gruppo di risorse tooremove hello, macchina virtuale e tutte le relative risorse.

```azurecli-interactive 
az group delete --name myResourceGroup
```

## <a name="next-steps"></a>Passaggi successivi

In questa guida introduttiva è stata distribuita una macchina virtuale semplice, è stata creata una regola del gruppo di sicurezza di rete ed è stato installato un server Web. toolearn informazioni sulle macchine virtuali di Azure, continuare l'esercitazione toohello per le macchine virtuali di Windows.

> [!div class="nextstepaction"]
> [Esercitazioni per le macchine virtuali di Windows in Azure](./tutorial-manage-vm.md)

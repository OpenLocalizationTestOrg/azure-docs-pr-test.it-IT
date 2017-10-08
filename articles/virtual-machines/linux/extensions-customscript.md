---
title: gli script personalizzati aaaRun nelle macchine virtuali Linux in Azure | Documenti Microsoft
description: "Automatizzare le attività di configurazione Linux VM utilizzando l'estensione dello Script personalizzata hello"
services: virtual-machines-linux
documentationcenter: 
author: neilpeterson
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: cf17ab2b-8d7e-4078-b6df-955c6d5071c2
ms.service: virtual-machines-linux
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure-services
ms.date: 04/26/2017
ms.author: nepeters
ms.openlocfilehash: f2c273a5fbd4cd1695aea48fa4bd08e691511e5f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="using-hello-azure-custom-script-extension-with-linux-virtual-machines"></a>Utilizzo di hello estensione Script personalizzata di Azure con le macchine virtuali Linux
Estensione dello Script personalizzata Hello Scarica ed esegue gli script in macchine virtuali di Azure. Questa estensione è utile per la configurazione post-distribuzione, l'installazione di software o qualsiasi altra attività di configurazione o gestione. Gli script possono essere scaricati dall'archiviazione di Azure o un altro percorso internet accessibile o forniti estensione toohello fase di esecuzione. estensione Script personalizzata Hello si integra con i modelli di gestione risorse di Azure e può essere eseguito anche tramite hello Azure CLI, PowerShell, il portale di Azure o hello API REST di macchina virtuale di Azure.

Questo documento illustra come toouse hello estensione Script personalizzata da hello CLI di Azure e un modello di gestione risorse di Azure, nonché dettagli risoluzione dei problemi in sistemi Linux.

## <a name="extension-configuration"></a>Configurazione dell'estensione
configurazione di estensione dello Script personalizzata Hello specifica come percorso dello script e hello toobe di comando eseguire. Questa configurazione può essere archiviata nei file di configurazione specificati nella riga di comando hello o in un modello di gestione risorse di Azure. Dati sensibili possono essere archiviati in una configurazione protetta, che verrà crittografata e decrittografata solo macchina virtuale hello. la configurazione protetta Hello è utile quando il comando di esecuzione hello include segreti, ad esempio una password.

### <a name="public-configuration"></a>Configurazione pubblica
Schema:

**Nota**: questi nomi di proprietà fanno distinzione tra maiuscole e minuscole. Utilizzare nomi di hello, come illustrato di seguito tooavoid problemi di distribuzione.

* **commandToExecute**: (obbligatorio, string) hello tooexecute script punto di ingresso
* **fileUris**: (facoltativa, matrice di stringhe) hello URL per il file toobe scaricato.
* **timestamp** (intero facoltativo) utilizzare questo tootrigger solo una riesecuzione dello script hello di campo tramite la modifica del valore di questo campo.

```json
{
  "fileUris": ["<url>"],
  "commandToExecute": "<command-to-execute>"
}
```

### <a name="protected-configuration"></a>Configurazione protetta
Schema:

**Nota**: questi nomi di proprietà fanno distinzione tra maiuscole e minuscole. Utilizzare nomi di hello, come illustrato di seguito tooavoid problemi di distribuzione.

* **commandToExecute**: (facoltativa, string) hello tooexecute script punto di ingresso. Usare in alternativa questo campo se il comando contiene segreti, ad esempio password.
* **storageAccountName**: (facoltativa, string) nome hello dell'account di archiviazione. Se si specificano credenziali di archiviazione, tutti i valori di fileUris devono essere URL relativi a BLOB di Azure.
* **storageAccountKey**: (facoltativa, string) la chiave di accesso hello dell'account di archiviazione.

```json
{
  "commandToExecute": "<command-to-execute>",
  "storageAccountName": "<storage-account-name>",
  "storageAccountKey": "<storage-account-key>"
}
```

## <a name="azure-cli"></a>Interfaccia della riga di comando di Azure
Quando si utilizza hello toorun di hello Azure CLI estensione Script personalizzata, creare un file di configurazione o file contenenti uri di file minimo hello e comando di esecuzione di script hello.

```azurecli
az vm extension set --resource-group myResourceGroup --vm-name myVM --name customScript --publisher Microsoft.Azure.Extensions --settings ./script-config.json
```

Facoltativamente impostazioni hello possono essere specificate nel comando hello sotto forma di stringa in formato JSON. In questo modo toobe configurazione hello specificato durante l'esecuzione e senza un file di configurazione separato.

```azurecli
az vm extension set '
  --resource-group exttest `
  --vm-name exttest `
  --name customScript `
  --publisher Microsoft.Azure.Extensions `
  --settings '{"fileUris": ["https://raw.githubusercontent.com/neilpeterson/test-extension/master/test.sh"],"commandToExecute": "./test.sh"}'
```

### <a name="azure-cli-examples"></a>Esempi di interfaccia della riga di comando di Azure

**Esempio 1** : configurazione pubblica con file di script.

```json
{
  "fileUris": ["https://raw.githubusercontent.com/neilpeterson/test-extension/master/test.sh"],
  "commandToExecute": "./test.sh"
}
```

Comando dell'interfaccia della riga di comando di Azure:

```azurecli
az vm extension set --resource-group myResourceGroup --vm-name myVM --name customScript --publisher Microsoft.Azure.Extensions --settings ./script-config.json
```

**Esempio 2** : configurazione pubblica senza file di script.

```json
{
  "commandToExecute": "apt-get -y update && apt-get install -y apache2"
}
```

Comando dell'interfaccia della riga di comando di Azure:

```azurecli
az vm extension set --resource-group myResourceGroup --vm-name myVM --name customScript --publisher Microsoft.Azure.Extensions --settings ./script-config.json
```

**Esempio 3** : un file di configurazione pubblico è l'URI di file di script hello toospecify utilizzato e un file di configurazione protetto è utilizzato toospecify hello comando toobe eseguita.

File di configurazione pubblica:

```json
{
  "fileUris": ["https://gist.github.com/ahmetalpbalkan/b5d4a856fe15464015ae87d5587a4439/raw/466f5c30507c990a4d5a2f5c79f901fa89a80841/hello.sh"]
}
```

File di configurazione protetta:  

```json
{
  "commandToExecute": "./hello.sh <password>"
}
```

Comando dell'interfaccia della riga di comando di Azure:

```azurecli
az vm extension set --resource-group myResourceGroup --vm-name myVM --name customScript --publisher Microsoft.Azure.Extensions --settings ./script-config.json --protected-settings ./protected-config.json
```

## <a name="resource-manager-template"></a>Modello di Resource Manager
è possibile eseguire l'estensione dello Script di Azure personalizzata Hello in fase di distribuzione di macchina virtuale utilizzando un modello di gestione risorse. toodo in tal caso, aggiungere modello di distribuzione toohello JSON formattato correttamente.

### <a name="resource-manager-examples"></a>Esempi di Resource Manager
**Esempio 1** : configurazione pubblica.

```json
{
    "name": "scriptextensiondemo",
    "type": "extensions",
    "location": "[resourceGroup().location]",
    "apiVersion": "2015-06-15",
    "dependsOn": [
        "[concat('Microsoft.Compute/virtualMachines/', parameters('scriptextensiondemoName'))]"
    ],
    "tags": {
        "displayName": "scriptextensiondemo"
    },
    "properties": {
        "publisher": "Microsoft.Azure.Extensions",
        "type": "CustomScript",
        "typeHandlerVersion": "2.0",
        "autoUpgradeMinorVersion": true,
      "settings": {
        "fileUris": [
          "https://gist.github.com/ahmetalpbalkan/b5d4a856fe15464015ae87d5587a4439/raw/466f5c30507c990a4d5a2f5c79f901fa89a80841/hello.sh"
        ],
        "commandToExecute": "sh hello.sh"
      }
    }
}
```

**Esempio 2** : comando di esecuzione nella configurazione protetta.

```json
{
  "name": "config-app",
  "type": "extensions",
  "location": "[resourceGroup().location]",
  "apiVersion": "2015-06-15",
  "dependsOn": [
    "[concat('Microsoft.Compute/virtualMachines/', concat(variables('vmName'),copyindex()))]"
  ],
  "tags": {
    "displayName": "config-app"
  },
  "properties": {
    "publisher": "Microsoft.Azure.Extensions",
    "type": "CustomScript",
    "typeHandlerVersion": "2.0",
    "autoUpgradeMinorVersion": true,
    "settings": {
      "fileUris": [
        "https://gist.github.com/ahmetalpbalkan/b5d4a856fe15464015ae87d5587a4439/raw/466f5c30507c990a4d5a2f5c79f901fa89a80841/hello.sh"
      ]              
    },
    "protectedSettings": {
      "commandToExecute": "sh hello.sh <password>"
    }
  }
}
```

Vedere hello .net Core negozio Demo per un esempio completo - [musica Store Demo](https://github.com/neilpeterson/nepeters-azure-templates/tree/master/dotnet-core-music-linux-vm-sql-db).

## <a name="troubleshooting"></a>Risoluzione dei problemi
Quando viene eseguita l'estensione dello Script personalizzata hello, script hello viene creato o scaricati in un toohello simile directory esempio seguente. output del comando Hello viene salvato anche in questa directory `stdout` e `stderr` file.

```bash
/var/lib/waagent/custom-script/download/0/
```

Estensione dello Script di Azure Hello produce un log, che è disponibili qui.

```bash
/var/log/azure/custom-script/handler.log
```

Inoltre, è possibile recuperare lo stato di esecuzione di Hello di hello estensione Script personalizzata con hello CLI di Azure.

```azurecli
az vm extension list -g myResourceGroup --vm-name myVM
```

output di Hello è simile hello seguente testo:

```azurecli
info:    Executing command vm extension get
+ Looking up hello VM "scripttst001"
data:    Publisher                   Name                                      Version  State
data:    --------------------------  ----------------------------------------  -------  ---------
data:    Microsoft.Azure.Extensions  CustomScript                              2.0      Succeeded
data:    Microsoft.OSTCExtensions    Microsoft.Insights.VMDiagnosticsSettings  2.3      Succeeded
info:    vm extension get command OK
```

## <a name="next-steps"></a>Passaggi successivi
Per informazioni su altre estensioni script delle macchine virtuali, vedere [Panoramica sulle estensioni script di Azure per Linux](extensions-features.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).


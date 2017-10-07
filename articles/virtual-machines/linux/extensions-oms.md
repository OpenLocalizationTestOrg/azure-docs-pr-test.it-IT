---
title: estensione di macchina virtuale di Azure per Linux aaaOMS | Documenti Microsoft
description: Distribuire l'agente OMS hello nella macchina virtuale di Linux mediante un'estensione di macchina virtuale.
services: virtual-machines-linux
documentationcenter: 
author: neilpeterson
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: c7bbf210-7d71-4a37-ba47-9c74567a9ea6
ms.service: virtual-machines-linux
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure-services
ms.date: 04/26/2017
ms.author: nepeters
ms.openlocfilehash: 0fc8003d1fae6c043eef18ae78d12f9304b70832
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="oms-virtual-machine-extension-for-linux"></a>Estensione macchina virtuale OMS per Linux

## <a name="overview"></a>Panoramica

In Operations Management Suite (OMS) sono disponibili funzionalità di monitoraggio, avviso e correzione tramite avvisi in risorse cloud e locali. Hello estensione della macchina virtuale agente OMS per Linux è pubblicato e supportato da Microsoft. estensione Hello installa l'agente OMS hello in macchine virtuali di Azure e registra le macchine virtuali in un'area di lavoro OMS. Opzioni di distribuzione, le configurazioni e piattaforme hello di dettagli in questo documento supportato per hello estensione della macchina virtuale OMS per Linux.

## <a name="prerequisites"></a>Prerequisiti

### <a name="operating-system"></a>Sistema operativo

Hello estensione OMS Agent possa essere eseguita su queste distribuzioni di Linux.

| Distribuzione | Versione |
|---|---|
| CentOS Linux | 5, 6 e 7 |
| Oracle Linux | 5, 6 e 7 |
| Red Hat Enterprise Linux Server | 5, 6 e 7 |
| Debian GNU/Linux | 6, 7 e 8 |
| Ubuntu | 12.04 LTS, 14.04 LTS, 15.04, 15.10, 16.04 LTS |
| SUSE Linux Enterprise Server | 11 e 12 |

### <a name="internet-connectivity"></a>Connettività Internet

Hello estensione agente OMS per Linux richiede tale macchina virtuale di destinazione hello è connesso toohello internet. 

## <a name="extension-schema"></a>Schema dell'estensione

Hello JSON seguente viene illustrato lo schema di hello per hello estensione OMS Agent. estensione Hello richiede hello dell'area di lavoro area di lavoro e l'ID chiave dall'area di lavoro di hello destinazione OMS; Questi valori sono disponibili nel portale OMS hello. Poiché chiave dell'area di lavoro hello deve essere considerate come dati sensibili, devono essere archiviato in una configurazione di impostazione protetto. Dati impostazione protette dell'estensione di macchina virtuale di Azure sono crittografati e decrittografati solo nella macchina virtuale di destinazione hello. Tenere presente che **workspaceId** e **workspaceKey** distinguono tra maiuscole e minuscole.

```json
{
  "type": "extensions",
  "name": "OMSExtension",
  "apiVersion": "2015-06-15",
  "location": "<location>",
  "dependsOn": [
    "[concat('Microsoft.Compute/virtualMachines/', <vm-name>)]"
  ],
  "properties": {
    "publisher": "Microsoft.EnterpriseCloud.Monitoring",
    "type": "OmsAgentForLinux",
    "typeHandlerVersion": "1.4",
    "settings": {
      "workspaceId": "myWorkspaceId"
    },
    "protectedSettings": {
      "workspaceKey": "myWorkSpaceKey"
    }
  }
}
```

### <a name="property-values"></a>Valori delle proprietà

| Nome | Valore/Esempio |
| ---- | ---- |
| apiVersion | 2015-06-15 |
| publisher | Microsoft.EnterpriseCloud.Monitoring |
| type | OmsAgentForLinux |
| typeHandlerVersion | 1.4 |
| workspaceId (esempio) | 6f680a37-00c6-41c7-a93f-1437e3462574 |
| workspaceKey (esempio) | z4bU3p1/GrnWpQkky4gdabWXAhbWSTz70hm4m2Xt92XI+rSRgE8qVvRhsGo9TXffbrTahyrwv35W0pOqQAU7uQ== |


## <a name="template-deployment"></a>Distribuzione del modello

Le estensioni macchina virtuale di Azure possono essere distribuite con i modelli di Azure Resource Manager. Modelli sono ideali per la distribuzione di uno o più macchine virtuali che richiedono la configurazione di distribuzione post, ad esempio tooOMS onboarding. Un modello di gestione risorse di esempio che include l'estensione della macchina virtuale di agente OMS hello è reperibile in hello [raccolta avvio rapido di Azure](https://github.com/Azure/azure-quickstart-templates/tree/master/201-oms-extension-ubuntu-vm). 

configurazione JSON Hello per un'estensione della macchina virtuale può essere annidata all'interno di risorsa di macchina virtuale hello o posizionati nella radice di hello o un livello superiore di un modello di gestione risorse di JSON. posizionamento di Hello di configurazione JSON hello influisce sul valore di hello del nome della risorsa hello e tipo. Per altre informazioni, vedere [Set name and type for child resources](../../azure-resource-manager/resource-manager-template-child-resource.md) (Impostare il nome e il tipo per le risorse figlio). 

Hello seguente si presuppone hello OMS estensione annidata all'interno di hello risorsa di macchina virtuale. Quando la nidificazione di risorse di estensione hello, hello JSON viene inserito nel hello `"resources": []` oggetto della macchina virtuale hello.

```json
{
  "type": "extensions",
  "name": "OMSExtension",
  "apiVersion": "2015-06-15",
  "location": "<location>",
  "dependsOn": [
    "[concat('Microsoft.Compute/virtualMachines/', <vm-name>)]"
  ],
  "properties": {
    "publisher": "Microsoft.EnterpriseCloud.Monitoring",
    "type": "OmsAgentForLinux",
    "typeHandlerVersion": "1.4",
    "settings": {
      "workspaceId": "myWorkspaceId"
    },
    "protectedSettings": {
      "workspaceKey": "myWorkSpaceKey"
    }
  }
}
```

Quando si inseriscono estensione hello JSON nella radice di hello del modello di hello, il nome di risorsa hello include una macchina virtuale di riferimento toohello padre e il tipo hello riflette configurazione annidati hello.  

```json
{
  "type": "Microsoft.Compute/virtualMachines/extensions",
  "name": "<parentVmResource>/OMSExtension",
  "apiVersion": "2015-06-15",
  "location": "<location>",
  "dependsOn": [
    "[concat('Microsoft.Compute/virtualMachines/', <vm-name>)]"
  ],
  "properties": {
    "publisher": "Microsoft.EnterpriseCloud.Monitoring",
    "type": "OmsAgentForLinux",
    "typeHandlerVersion": "1.4",
    "settings": {
      "workspaceId": "myWorkspaceId"
    },
    "protectedSettings": {
      "workspaceKey": "myWorkSpaceKey"
    }
  }
}
```

## <a name="azure-cli-deployment"></a>Distribuzione dell'interfaccia della riga di comando di Azure

Hello CLI di Azure può essere utilizzato toodeploy hello OMS agente VM estensione tooan macchina virtuale esistente. Sostituire chiave OMS hello e l'ID di OMS con quelle dell'area di lavoro OMS. 

```azurecli
az vm extension set \
  --resource-group myResourceGroup \
  --vm-name myVM \
  --name OmsAgentForLinux \
  --publisher Microsoft.EnterpriseCloud.Monitoring \
  --version 1.4 --protected-settings '{"workspaceKey": "omskey"}' \
  --settings '{"workspaceId": "omsid"}'
```

## <a name="troubleshoot-and-support"></a>Risoluzione dei problemi e supporto

### <a name="troubleshoot"></a>Risoluzione dei problemi

Dati sullo stato di hello delle distribuzioni di estensione possono essere recuperati dal portale di Azure hello e, utilizzando hello CLI di Azure. lo stato di distribuzione hello toosee delle estensioni per una macchina virtuale specificata, eseguire hello seguente comando utilizzando hello CLI di Azure.

```azurecli
az vm extension list --resource-group myResourceGroup --vm-name myVM -o table
```

Esecuzione di estensione di output è connesso toohello seguenti file:

```
/opt/microsoft/omsagent/bin/stdout
```

### <a name="error-codes-and-their-meanings"></a>Codici di errore e relativi significati

| Codice di errore | Significato | Azione possibile |
| :---: | --- | --- |
| 10 | Macchina virtuale è già connesso tooan area di lavoro OMS | tooconnect hello VM toohello dell'area di lavoro specificata nello schema di estensione hello, impostare stopOnMultipleConnections toofalse nelle impostazioni pubbliche o rimuovere la proprietà. Questa macchina virtuale viene fatturata una volta per ogni area di lavoro a cui è connessa. |
| 11 | Configurazione non valido fornito toohello estensione | Seguire hello precedenti esempi tooset tutti i valori delle proprietà necessari per la distribuzione. |
| 12 | gestione di pacchetti Hello dpkg è bloccato | Assicurarsi che tutte le operazioni di aggiornamento dpkg computer hello è stata completata e riprovare. |
| 20 | Chiamata Enable anomala | [Hello aggiornamento agente Linux di Azure](https://docs.microsoft.com/en-us/azure/virtual-machines/linux/update-agent) toohello versione più recente disponibile. |
| 51 | Questa estensione non è supportata nel sistema operativo della macchina virtuale di hello | |
| 55 | Non è possibile connettere il servizio di Microsoft Operations Management Suite toohello | Verificare che il sistema hello disponga dell'accesso a Internet o che è stato fornito un proxy HTTP valido. Inoltre, controllare correttezza hello dell'ID dell'area di lavoro di hello. |

Ulteriori informazioni sulla risoluzione dei problemi possono trovarsi in hello [agente OMS per Linux Troubleshooting Guide](https://github.com/Microsoft/OMS-Agent-for-Linux/blob/master/docs/Troubleshooting.md#).

### <a name="support"></a>Supporto

Se è necessario ulteriore assistenza in qualsiasi punto in questo articolo, è possibile contattare hello Azure esperti hello [forum MSDN di Azure e di Overflow dello Stack](https://azure.microsoft.com/en-us/support/forums/). In alternativa, è possibile archiviare un evento imprevisto di supporto tecnico di Azure. Passare toohello [sito del supporto tecnico di Azure](https://azure.microsoft.com/en-us/support/options/) e scegliere supporto tecnico. Per informazioni sull'utilizzo di supporto di Azure, leggere hello [supporto tecnico di Microsoft Azure domande frequenti su](https://azure.microsoft.com/en-us/support/faq/).

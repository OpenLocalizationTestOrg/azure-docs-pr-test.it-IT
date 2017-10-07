---
title: aaaView e utilizzare il modello di gestione risorse di Azure di una macchina virtuale | Documenti Microsoft
description: Informazioni su come toouse hello modello di gestione risorse di Azure da una macchina virtuale di toocreate altre macchine virtuali
services: devtest-lab,virtual-machines,visual-studio-online
documentationcenter: na
author: tomarcher
manager: douge
editor: 
ms.assetid: a759d9ce-655c-4ac6-8834-cb29dd7d30dd
ms.service: devtest-lab
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/05/2017
ms.author: tarcher
ms.openlocfilehash: b79f7eb4171793681a0b654e6e72a83191c76bde
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="use-a-virtual-machines-azure-resource-manager-template"></a>Usare un modello di Azure Resource Manager di una macchina virtuale

Quando si crea una macchina virtuale (VM) in DevTest Labs tramite hello [portale di Azure](http://go.microsoft.com/fwlink/p/?LinkID=525040), è possibile visualizzare il modello di Azure Resource Manager hello prima di salvare hello macchina virtuale. Hello modello può quindi essere utilizzato come un toocreate base più macchine virtuali di laboratorio con hello stesse impostazioni.

In questo articolo viene descritto come tooview hello modello di gestione risorse durante la creazione di una macchina virtuale e come toodeploy è successiva creazione tooautomate di hello stessa macchina virtuale.

## <a name="multi-vm-vs-single-vm-resource-manager-templates"></a>Modello di Resource Manager di più macchine virtuali rispetto al modello di Resource Manager di una singola macchina virtuale
Sono disponibili due modi per le macchine virtuali toocreate in un modello di gestione risorse di DevTest Labs: effettuare il provisioning di risorse Microsoft.DevTestLab/labs/virtualmachines hello o eseguire il provisioning di risorse Microsoft.Commpute/virtualmachines hello. Ognuno viene usato in diversi scenari e richiede autorizzazioni diverse.

- Possono eseguire il provisioning di macchine virtuali lab singoli modelli di gestione risorse che utilizzano un tipo di risorsa Microsoft.DevTestLab/labs/virtualmachines (come dichiarato nella proprietà "resource" hello nel modello hello). Ogni macchina virtuale viene quindi visualizzato come un singolo elemento nell'elenco di macchine virtuali di DevTest Labs hello:

   ![Elenco delle macchine virtuali come singoli elementi nell'elenco di macchine virtuali di DevTest Labs hello](./media/devtest-lab-use-arm-template/devtestlab-lab-vm-single-item.png)

   Può eseguire il provisioning di questo tipo di modello di gestione risorse tramite il comando di Azure PowerShell hello **New AzureRmResourceGroupDeployment** o tramite comando CLI di Azure hello **distribuzione gruppo az creare** . Richiede le autorizzazioni di amministratore, in modo che gli utenti assegnati a un ruolo utente DevTest Labs non è possibile eseguire la distribuzione di hello. 

- Modelli di gestione risorse che utilizzano un tipo di risorsa Microsoft.Compute/virtualmachines è possono eseguire il provisioning di più macchine virtuali come un unico ambiente nell'elenco di macchine virtuali di DevTest Labs hello:

   ![Elenco delle macchine virtuali come singoli elementi nell'elenco di macchine virtuali di DevTest Labs hello](./media/devtest-lab-use-arm-template/devtestlab-lab-vm-single-environment.png)

   Macchine virtuali in hello stesso ambiente può essere gestito insieme e condivisione hello stesso ciclo di vita. Gli utenti assegnati a un ruolo utente DevTest Labs è possono creare gli ambienti che utilizzano tali modelli come messaggio per l'amministratore ha configurato lab hello in questo modo.

Hello parte restante di questo articolo sono descritti i modelli di gestione risorse che utilizzano Mirosoft.DevTestLab/labs/virtualmachines. Questi vengono utilizzati dal lab admins tooautomate lab la creazione di VM (ad esempio, claimable VM) o la generazione di immagine finale (ad esempio, i factory immagine).

[Procedure consigliate per la creazione di modelli di Azure Resource Manager](https://docs.microsoft.com/azure/azure-resource-manager/resource-manager-template-best-practices) offre molti toohelp linee guida e suggerimenti si creano modelli di gestione risorse di Azure che sono toouse semplice e affidabile.

## <a name="view-and-save-a-virtual-machines-resource-manager-template"></a>Visualizzare e usare un modello di Resource Manager di Azure di una macchina virtuale
1. Seguire i passaggi hello in [creare la prima macchina virtuale in un ambiente lab](devtest-lab-create-first-vm.md) toobegin la creazione di una macchina virtuale.
1. Immettere le informazioni di hello necessario per la macchina virtuale e aggiungere eventuali elementi desiderato per questa macchina virtuale.
1. Nella parte inferiore di hello della finestra di hello Configura le impostazioni, scegliere **modello ARM vista**.

   ![Pulsante View ARM template](./media/devtest-lab-use-arm-template/devtestlab-lab-view-rm-template.png)
1. Copiare e salvare hello Gestione risorse modello toouse toocreate successive un'altra macchina virtuale.

   ![Toosave modello di gestione risorse per un utilizzo successivo](./media/devtest-lab-use-arm-template/devtestlab-lab-copy-rm-template.png)

Dopo aver salvato il modello di gestione risorse di hello, è necessario aggiornare sezione parametri hello del modello di hello prima che sia possibile utilizzarlo. È possibile creare un parameter.json che consente di personalizzare solo i parametri di hello, di fuori di modello di gestione risorse hello effettivo. 

![Personalizzare i parametri usando un file JSON](./media/devtest-lab-use-arm-template/devtestlab-lab-custom-params.png)

## <a name="deploy-a-resource-manager-template-toocreate-a-vm"></a>Distribuire un toocreate di modello una macchina virtuale di gestione risorse
Dopo aver salvato un modello di gestione delle risorse e personalizzarlo per le proprie esigenze, è possibile utilizzare la creazione di VM tooautomate. [Distribuire le risorse e modelli di gestione risorse di Azure PowerShell](https://docs.microsoft.com/azure/azure-resource-manager/resource-group-template-deploy) viene descritto come toouse Azure PowerShell con Gestione risorse modelli toodeploy tooAzure le risorse. [Distribuire le risorse con i modelli di gestione risorse e CLI di Azure](https://docs.microsoft.com/azure/azure-resource-manager/resource-group-template-deploy-cli) viene descritto come toouse CLI di Azure con Gestione risorse modelli toodeploy tooAzure le risorse.

> [!NOTE]
> Solo un utente con autorizzazioni di proprietario lab può creare macchine virtuali da un modello di Resource Manager usando Azure PowerShell. Se si desidera la creazione di VM tooautomate utilizzando un modello di gestione delle risorse e si dispone solo delle autorizzazioni utente, è possibile utilizzare hello [ **creare vm lab az** comando hello CLI](https://docs.microsoft.com/cli/azure/lab/vm#create).

### <a name="next-steps"></a>Passaggi successivi
* Informazioni su come troppo[creare ambienti multi-VM con modelli di gestione risorse](devtest-lab-create-environment-from-arm.md).
* Esplorare altri modelli di gestione risorse di avvio rapido per l'automazione di DevTest Labs da hello [pubblica repository GitHub di DevTest Labs](https://github.com/Azure/azure-quickstart-templates).

---
title: aaaUse toodeploy portale Azure le risorse di Azure | Documenti Microsoft
description: Utilizzare il portale di Azure e gestire risorse di Azure toodeploy le risorse.
services: azure-resource-manager,azure-portal
documentationcenter: 
author: tfitzmac
manager: timlt
editor: tysonn
ms.assetid: 2c98a4aa-8d9f-4a0a-b764-214dbe8ed009
ms.service: azure-resource-manager
ms.workload: multiple
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 12/19/2016
ms.author: tomfitz
ms.openlocfilehash: 5a5217f94c8dfc0c1ebd613903ea3dcbe1197bfc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-resources-with-resource-manager-templates-and-azure-portal"></a>Distribuire le risorse con i modelli di Azure Resource Manager e il portale di Azure
> [!div class="op_single_selector"]
> * [PowerShell](resource-group-template-deploy.md)
> * [Interfaccia della riga di comando di Azure](resource-group-template-deploy-cli.md)
> * [Portale](resource-group-template-deploy-portal.md)
> * [API REST](resource-group-template-deploy-rest.md)
> 
> 

Questo argomento viene illustrato come hello toouse [portale di Azure](https://portal.azure.com) con [Azure Resource Manager](resource-group-overview.md) toodeploy le risorse di Azure. toolearn sulla gestione delle risorse, vedere [le risorse di gestione di Azure tramite il portale](resource-group-portal.md).

Attualmente, non a ogni servizio supporta portale hello o gestione delle risorse. Per tali servizi, è necessario hello toouse [portale classico](https://manage.windowsazure.com). Per hello lo stato di ogni servizio, vedere [grafico disponibilità portale Azure](https://azure.microsoft.com/features/azure-portal/availability/).

## <a name="create-resource-group"></a>Creare un gruppo di risorse
1. Selezionare un gruppo di risorse vuoto, toocreate **New** > **Management** > **gruppo di risorse**.
   
    ![creare un gruppo di risorse vuoto](./media/resource-group-template-deploy-portal/create-empty-group.png)
2. Assegnare un nome e un percorso e, se necessario, selezionare una sottoscrizione. È necessario tooprovide un percorso per il gruppo di risorse hello perché il gruppo di risorse hello archivia i metadati sulle risorse hello. Per motivi di conformità, è consigliabile toospecify archiviati che i metadati. In generale è consigliabile specificare un percorso in cui risiederà la maggior parte delle risorse. Utilizzando hello stessa posizione può semplificare il modello.
   
    ![impostare i valori del gruppo](./media/resource-group-template-deploy-portal/set-group-properties.png)

## <a name="deploy-resources-from-marketplace"></a>Distribuire le risorse da Marketplace
Dopo aver creato un gruppo di risorse, è possibile distribuire le risorse tooit da hello Marketplace. Hello Marketplace fornisce soluzioni predefinite per gli scenari comuni.

1. toostart una distribuzione, selezionare **New** e hello tipo di risorsa desiderato toodeploy. Esaminare per una particolare versione di hello della risorsa hello quali toodeploy.
   
    ![distribuire risorse](./media/resource-group-template-deploy-portal/deploy-resource.png)
2. Se non viene visualizzata particolare soluzione hello toodeploy desiderato, è possibile cercare hello Marketplace.
   
    ![cercare nel Marketplace](./media/resource-group-template-deploy-portal/search-resource.png)
3. A seconda di tipo hello di risorse selezionato, è una raccolta di proprietà rilevanti tooset prima della distribuzione. Le opzioni non sono visualizzate in questo articolo, perché variano in base al tipo di risorsa. Per tutti i tipi è necessario selezionare un gruppo di risorse di destinazione. esempio Hello figura viene illustrato come toocreate un'app web e distribuirlo toohello gruppo di risorse creato.
   
    ![Creare un gruppo di risorse](./media/resource-group-template-deploy-portal/select-existing-group.png)
   
    In alternativa, è possibile decidere toocreate un gruppo di risorse durante la distribuzione delle risorse. Selezionare **Crea nuovo** e assegnare un nome di gruppo di risorse hello.
   
    ![creare un nuovo gruppo di risorse](./media/resource-group-template-deploy-portal/select-new-group.png)
4. La distribuzione ha inizio. distribuzione di Hello potrebbe richiedere alcuni minuti. Al termine della distribuzione di hello, viene visualizzata una notifica.
   
    ![visualizzare notifiche](./media/resource-group-template-deploy-portal/view-notification.png)
5. Dopo la distribuzione delle risorse, è possibile aggiungere un gruppo di risorse di ulteriori risorse toohello utilizzando hello **Aggiungi** comando pannello della risorsa gruppo hello.
   
    ![aggiungere una risorsa](./media/resource-group-template-deploy-portal/add-resource.png)

## <a name="deploy-resources-from-custom-template"></a>Distribuire risorse da un modello personalizzato
Se si desidera tooexecute una distribuzione ma non utilizzare nessuno dei modelli di hello in hello Marketplace, è possibile creare un modello personalizzato che definisce l'infrastruttura di hello per la soluzione. toolearn sulla creazione di modelli, vedere [modelli Authoring Azure Resource Manager](resource-group-authoring-templates.md).

1. Selezionare un modello personalizzato tramite il portale di hello toodeploy **New**e iniziare a cercare **distribuzione modello** fino a quando non è possibile scegliere le opzioni di hello.
   
    ![cercare la distribuzione del modello](./media/resource-group-template-deploy-portal/search-template.png)
2. Selezionare **distribuzione modello** dalle risorse disponibili hello.
   
    ![selezionare la distribuzione del modello](./media/resource-group-template-deploy-portal/select-template.png)
3. Dopo aver avviato la distribuzione dei modelli di hello, aprire il modello vuoto hello che è disponibile per la personalizzazione.
   
    ![creare un modello](./media/resource-group-template-deploy-portal/show-custom-template.png)
   
    Nell'editor di hello, aggiungere la sintassi JSON hello che definisce le risorse di hello desiderato toodeploy. Al termine, selezionare **Salva** . Per istruzioni su come scrivere la sintassi JSON hello, vedere [procedura dettagliata di modello di gestione risorse](resource-manager-template-walkthrough.md).
   
    ![modificare un modello](./media/resource-group-template-deploy-portal/edit-template.png)
4. In alternativa, è possibile selezionare un modello esistente da hello [modelli di avvio rapido di Azure](https://azure.microsoft.com/documentation/templates/). Questi modelli vengono forniti dalla community di hello. Coprono molti scenari comuni e un utente può essere aggiunti a un modello simile toowhat che si sta tentando di toodeploy. È possibile cercare hello modelli toofind un elemento che corrisponde allo scenario.
   
    ![selezionare un modello di Guida introduttiva](./media/resource-group-template-deploy-portal/select-quickstart-template.png)
   
    È possibile visualizzare modello selezionato hello nell'editor di hello.
5. Dopo aver fornito hello tutti gli altri valori, selezionare **crea** modello hello toodeploy. 
   
    ![distribuire un modello](./media/resource-group-template-deploy-portal/create-custom-deploy.png)

## <a name="deploy-resources-from-a-template-saved-tooyour-account"></a>Distribuire le risorse da un modello salvato tooyour account
portale Hello consente si toosave tooyour un modello account Azure e distribuirlo in un secondo momento. Per ulteriori informazioni sull'utilizzo di questi modelli, salvato [introduzione privati modelli nel portale di Azure hello](../marketplace-consumer/mytemplates-getstarted.md).

1. Selezionare i modelli salvati, toofind **Sfoglia** > **modelli**.
   
    ![esplorare i modelli](./media/resource-group-template-deploy-portal/browse-templates.png)
2. Hello l'elenco dei modelli salvati tooyour account, selezionare quello che si desidera toowork su hello.
   
    ![modelli salvati](./media/resource-group-template-deploy-portal/saved-templates.png)
3. Selezionare **Distribuisci** tooredeploy questo modello salvato.
   
    ![distribuire un modello salvato](./media/resource-group-template-deploy-portal/deploy-saved-template.png)

## <a name="next-steps"></a>Passaggi successivi
* vedere i log di controllo, tooview [controllare le operazioni con Gestione risorse di](resource-group-audit.md).
* vedere gli errori di distribuzione, tootroubleshoot [per visualizzare le operazioni di distribuzione](resource-manager-deployment-operations.md).
* tooretrieve un modello da una distribuzione o un gruppo di risorse, vedere [modello esportare Gestione risorse di Azure da risorse esistenti](resource-manager-export-template.md).
* Per istruzioni su come le aziende possono usare tooeffectively Gestione risorse di gestione di sottoscrizioni, vedere [lo scaffolding di Azure enterprise - governance sottoscrizione rigorosa](resource-manager-subscription-governance.md).


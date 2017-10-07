---
title: aaaUse toomanage portale Azure le risorse di Azure | Documenti Microsoft
description: Utilizzare il portale di Azure e gestire risorse di Azure toomanage le risorse. Viene illustrato come toowork con risorse toomonitor dashboard.
services: azure-resource-manager,azure-portal
documentationcenter: 
author: tfitzmac
manager: timlt
editor: tysonn
ms.assetid: 0725bbf2-5913-4c07-af6e-24e11d957fbc
ms.service: azure-resource-manager
ms.workload: multiple
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 12/19/2016
ms.author: tomfitz
ms.openlocfilehash: 0c89a197a31c5b6dd03ba457cb4d1fdf9f6d00f6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="manage-azure-resources-through-portal"></a>Gestire le risorse di Azure mediante il portale
> [!div class="op_single_selector"]
> * [Azure PowerShell](powershell-azure-resource-manager.md)
> * [Interfaccia della riga di comando di Azure](xplat-cli-azure-resource-manager.md)
> * [Portale](resource-group-portal.md) 
> * [API REST](resource-manager-rest-api.md)
> 
> 

Questo argomento viene illustrato come hello toouse [portale di Azure](https://portal.azure.com) con [Azure Resource Manager](resource-group-overview.md) toomanage le risorse di Azure. vedere toolearn sulla distribuzione di risorse tramite il portale di hello [distribuire le risorse con modelli di gestione risorse e il portale di Azure](resource-group-template-deploy-portal.md).

Attualmente, non a ogni servizio supporta portale hello o gestione delle risorse. Per tali servizi, è necessario hello toouse [portale classico](https://manage.windowsazure.com). Per hello lo stato di ogni servizio, vedere [grafico disponibilità portale Azure](https://azure.microsoft.com/features/azure-portal/availability/).

## <a name="manage-resource-groups"></a>Gestire gruppi di risorse

Un gruppo di risorse è un contenitore con risorse correlate per una soluzione Azure. gruppo di risorse Hello può includere tutte le risorse di hello per soluzione hello o solo le risorse che si desidera toomanage come gruppo. Si decide come risorse tooallocate tooresource gruppi basati su cosa hello più utile per l'organizzazione. In genere, aggiungere le risorse che condividono hello stesso toohello del ciclo di vita stessa risorsa di raggruppare in modo che è facilmente possibile distribuire, aggiornare ed eliminarli come gruppo. 

gruppo di risorse Hello archivia i metadati sulle risorse hello. Pertanto, quando si specifica un percorso per il gruppo di risorse hello, si specifica la memorizzazione dei metadati. Per motivi di conformità, potrebbe essere necessario tooensure che i dati sono archiviati in una determinata area.

1. Selezionare tutti i gruppi di risorse di hello nella sottoscrizione, toosee **gruppi di risorse**.
   
    ![esplorare i gruppi di risorse](./media/resource-group-portal/browse-groups.png)
2. Selezionare un gruppo di risorse vuoto, toocreate **Aggiungi**.
   
    ![aggiungere un gruppo di risorse](./media/resource-group-portal/add-resource-group.png)
3. Specificare un nome e percorso per il nuovo gruppo di risorse hello. Selezionare **Crea**.
   
    ![Creare un gruppo di risorse](./media/resource-group-portal/create-empty-group.png)
4. Potrebbe essere necessario tooselect **aggiornamento** toosee gruppo di risorse hello creato di recente.
   
    ![aggiornare un gruppo di risorse](./media/resource-group-portal/refresh-resource-groups.png)
5. informazioni di hello toocustomize visualizzate per i gruppi di risorse, selezionare **colonne**.
   
    ![personalizzare colonne](./media/resource-group-portal/select-columns.png)
6. Selezionare tooadd colonne hello e quindi selezionare **aggiornamento**.
   
    ![aggiungere colonne](./media/resource-group-portal/add-columns.png)
7. toolearn sulla distribuzione di risorse tooyour nuovo gruppo di risorse, vedere [distribuire le risorse con modelli di gestione risorse e il portale di Azure](resource-group-template-deploy-portal.md).
8. Per gruppo di risorse tooa di accesso rapido, è possibile aggiungere dashboard di tooyour hello blade.
   
    ![aggiungere un gruppo di risorse](./media/resource-group-portal/pin-group.png)
9. Consente di visualizzare dashboard Hello gruppo di risorse hello e le relative risorse. È possibile selezionare i gruppi di risorse hello o qualsiasi elemento toohello toonavigate di risorse.
   
    ![aggiungere un gruppo di risorse](./media/resource-group-portal/show-resource-group-dashboard.png)

## <a name="tag-resources"></a>Aggiungere tag alle risorse
È possibile applicare tag tooresource gruppi e le risorse toologically organizzare le risorse. Per informazioni sull'utilizzo di tag, vedere [tramite tag tooorganize le risorse di Azure](resource-group-using-tags.md).

[!INCLUDE [resource-manager-tag-resource](../../includes/resource-manager-tag-resources.md)]

## <a name="monitor-resources"></a>Monitorare le risorse
Quando si seleziona una risorsa, il pannello della risorsa hello presenta predefinito grafici e tabelle per il monitoraggio di tale tipo di risorsa.

1. Selezionare una risorsa e notare di hello **monitoraggio** sezione. Include grafici che sono il tipo di risorsa toohello pertinente. Hello immagine seguente mostra i dati per un account di archiviazione di monitoraggio predefinite hello.
   
    ![visualizzare il monitoraggio](./media/resource-group-portal/show-monitoring.png)
2. È possibile aggiungere una sezione di dashboard di hello pannello tooyour selezionando hello i puntini di sospensione (…) sopra la sezione hello. È anche possibile personalizzare hello dimensioni hello sezione nel pannello hello o rimuoverlo completamente. Hello immagine seguente mostra come toopin, personalizzare o rimuovere una sezione di memoria e CPU hello.
   
    ![sezione di aggiunta](./media/resource-group-portal/pin-cpu-section.png)
3. Dopo aver aggiunto i dashboard di hello sezione toohello, hello riepilogo verrà visualizzato nel dashboard di hello. E, selezionandolo immediatamente accetta toomore dettagli sui dati hello.
   
    ![visualizzare il dashboard](./media/resource-group-portal/view-startboard.png)
4. toocompletely personalizzare i dati di hello monitorare tramite il portale di hello, spostarsi dashboard predefinito tooyour e selezionare **nuovo dashboard**.
   
    ![dashboard](./media/resource-group-portal/dashboard.png)
5. Denominare il nuovo dashboard e trascinare i riquadri nel dashboard hello. Hello riquadri vengono filtrati in base a opzioni diverse.
   
    ![dashboard](./media/resource-group-portal/create-dashboard.png)
   
     toolearn sull'utilizzo dei dashboard, vedere [creazione e condivisione dei dashboard nel portale di Azure hello](../azure-portal/azure-portal-dashboards.md).

## <a name="manage-resources"></a>Gestire risorse
Nel pannello hello per una risorsa, vedrai opzioni hello per la gestione delle risorse di hello. portale di Hello Visualizza opzioni di gestione per quel determinato tipo di risorsa. Verranno visualizzati i comandi di gestione hello in alto di hello del pannello della risorsa hello e sul lato sinistro di hello.

![Gestire risorse](./media/resource-group-portal/manage-resources.png)

Da queste opzioni, è possibile eseguire operazioni quali l'avvio e arresto di una macchina virtuale o riconfigurare le proprietà di hello della macchina virtuale hello.

## <a name="move-resources"></a>Spostare le risorse
Se è necessario toomove risorse tooanother risorse gruppo o un'altra sottoscrizione, vedere [spostare sottoscrizione o il gruppo di risorse toonew risorse](resource-group-move-resources.md).

## <a name="lock-resources"></a>Bloccare le risorse
È possibile bloccare una sottoscrizione, un gruppo di risorse o una risorsa tooprevent ad altri utenti nell'organizzazione da un'accidentale eliminazione o modifica di risorse critiche. Per altre informazioni, vedere [Bloccare le risorse con Gestione risorse di Azure](resource-group-lock-resources.md).

[!INCLUDE [resource-manager-lock-resources](../../includes/resource-manager-lock-resources.md)]

## <a name="view-your-subscription-and-costs"></a>Visualizzare la sottoscrizione e i costi
È possibile visualizzare informazioni sui costi riportati hello e della sottoscrizione per tutte le risorse. Selezionare **sottoscrizioni** e sottoscrizione hello da toosee. È necessario solo un tooselect di sottoscrizione.

![sottoscrizione](./media/resource-group-portal/select-subscription.png)

Nel Pannello di sottoscrizione hello, vedrai una velocità.

![velocità](./media/resource-group-portal/burn-rate.png)

E una suddivisione dei costi in base al tipo di risorsa.

![costo delle risorse](./media/resource-group-portal/cost-by-resource.png)

## <a name="export-template"></a>Esportare il modello
Dopo aver configurato il gruppo di risorse, è opportuno modello di gestione risorse di hello tooview per il gruppo di risorse hello. Esportazione modello hello offre due vantaggi:

1. È possibile automatizzare facilmente le distribuzioni future di soluzione hello perché il modello di hello contiene tutta l'infrastruttura completa hello.
2. È possibile acquisire familiarità con la sintassi dei modelli esaminando hello notazione JSON (JavaScript Object) che rappresenta la soluzione.

Per istruzioni dettagliate, vedere [Esportare un modello di Azure Resource Manager da risorse esistenti](resource-manager-export-template.md).

## <a name="delete-resource-group-or-resources"></a>Eliminare risorse o gruppi di risorse
Se si elimina un gruppo di risorse, tutte le risorse di hello in esso contenute. È anche possibile eliminare singole risorse all'interno di un gruppo. Si desidera tooexercise attenzione quando si elimina un gruppo di risorse perché in altri gruppi di risorse che sono collegati tooit potrebbero essere presenti risorse. Gestione risorse non elimina le risorse collegate, ma potrebbero non funzionare correttamente senza risorse hello previsto.

![eliminare un gruppo](./media/resource-group-portal/delete-group.png)

## <a name="next-steps"></a>Passaggi successivi
* log attività tooview, vedere [controllare le operazioni con Gestione risorse di](resource-group-audit.md).
* Dettagli tooview su una distribuzione, vedere [per visualizzare le operazioni di distribuzione](resource-manager-deployment-operations.md).
* vedere le risorse toodeploy tramite il portale di hello [distribuire le risorse con modelli di gestione risorse e il portale di Azure](resource-group-template-deploy-portal.md).
* toomanage tooresources di accesso, vedere [utilizzare le risorse di sottoscrizione di Azure tooyour accesso toomanage assegnazioni ruolo](../active-directory/role-based-access-control-configure.md).
* Per istruzioni su come le aziende possono usare tooeffectively Gestione risorse di gestione di sottoscrizioni, vedere [lo scaffolding di Azure enterprise - governance sottoscrizione rigorosa](resource-manager-subscription-governance.md).


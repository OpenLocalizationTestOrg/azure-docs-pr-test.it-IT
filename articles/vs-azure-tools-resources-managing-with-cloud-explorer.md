---
title: aaaManaging Azure risorse con Cloud Explorer | Documenti Microsoft
description: Informazioni su come toouse Cloud Explorer toobrowse e gestire le risorse di Azure in Visual Studio.
services: visual-studio-online
documentationcenter: na
author: kraigb
manager: ghogen
editor: 
ms.assetid: 6347dc53-f497-49d5-b29b-e8b9f0e939d7
ms.service: multiple
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: multiple
ms.date: 03/25/2017
ms.author: kraigb
ms.openlocfilehash: 8a81660074d5d04be063df9e25076b7a97586514
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="manage-hello-resources-associated-with-your-azure-accounts-in-visual-studio-cloud-explorer"></a>Gestire le risorse di hello associate agli account di Azure in Visual Studio Cloud Explorer
Cloud Explorer consente si tooview le risorse di Azure e i gruppi di risorse, controllare le relative proprietà ed eseguire azioni di diagnostica chiave sviluppatore da Visual Studio. 

Ad esempio hello [portale di Azure](http://go.microsoft.com/fwlink/p/?LinkID=525040), Cloud Explorer viene compilato nello stack di hello Azure Resource Manager. Pertanto riconosce risorse, come i gruppi di risorse di Azure e i servizi di Azure, come le app per la logica e le app per le API. Supporta infine il [controllo degli accessi in base al ruolo](active-directory/role-based-access-control-configure.md) (RBAC). 

## <a name="prerequisites"></a>Prerequisiti
- [Visual Studio 2017](https://www.visualstudio.com/downloads/) con hello **carico di lavoro Azure** selezionato, o una versione precedente di Visual Studio con hello [Microsoft Azure SDK per .NET 2.9](https://www.microsoft.com/en-us/download/details.aspx?id=51657).
- Account di Microsoft Azure: se non si ha un account, è possibile [iscriversi per ottenere una versione di valutazione gratuita](http://go.microsoft.com/fwlink/?LinkId=623901) oppure [attivare i vantaggi della sottoscrizione di Visual Studio](http://go.microsoft.com/fwlink/?LinkId=623901).

> [!NOTE]
> tooview Cloud Explorer, selezionare **vista** > **Cloud Explorer** sulla barra dei menu hello.   
> 
> 

## <a name="add-an-azure-account-toocloud-explorer"></a>Aggiungere un tooCloud account Azure Explorer
risorse di hello tooview associate a un account Azure, è necessario prima aggiungere hello account tooCloud Explorer. 

1. In **Cloud Explorer**, selezionare **Impostazioni account Azure**.

    ![Icona delle impostazioni account di Azure di Cloud Explorer](media/vs-azure-tools-resources-managing-with-cloud-explorer/azure-account-settings.png)

1. Selezionare **Aggiungi un nuovo account**. 

    ![Collegamento per l'aggiunta dell'account di Cloud Explorer](media/vs-azure-tools-resources-managing-with-cloud-explorer/add-account-link.png)

1. Accedi toohello account Azure con risorse di cui si desidera toobrowse. 

1. Una volta effettuato l'accesso tooan account Azure, visualizzare le sottoscrizioni di hello associate all'account. Selezionare hello per le sottoscrizioni degli account hello toobrowse desiderato e quindi selezionare le caselle di controllo **applica**. 
 
    ![Cloud Explorer: selezionare le sottoscrizioni di Azure toodisplay](media/vs-azure-tools-resources-managing-with-cloud-explorer/select-subscriptions.png)

1. Dopo aver selezionato le sottoscrizioni di hello con risorse di cui si desidera toobrowse, tali sottoscrizioni e le risorse visualizzare hello Cloud Explorer.

    ![Elenco delle risorse di Cloud Explorer per un account Azure](media/vs-azure-tools-resources-managing-with-cloud-explorer/resources-listed.png)

## <a name="remove-an-azure-account-from-cloud-explorer"></a>Rimuovere un account di Azure da Cloud Explorer 

1. In **Cloud Explorer**, selezionare **Impostazioni account Azure**.

    ![Icona delle impostazioni account di Azure di Cloud Explorer](media/vs-azure-tools-resources-managing-with-cloud-explorer/azure-account-settings.png)

1. Selezionare Avanti toohello account cui si vuole tooremove, **rimuovere**.

    ![Icona delle impostazioni account di Azure di Cloud Explorer](media/vs-azure-tools-resources-managing-with-cloud-explorer/remove-account.png)

## <a name="view-resource-types-or-resource-groups"></a>Visualizzare i tipi o i gruppi di risorse
tooview le risorse di Azure, è possibile scegliere una **tipi di risorse** o **gruppi di risorse** visualizzazione.

1. In **Cloud Explorer**, selezionare hello a discesa di visualizzazione di risorse.

    ![Visualizzazione di risorse hello desiderato tooselect elenco a discesa Esplora del cloud](media/vs-azure-tools-resources-managing-with-cloud-explorer/resources-view-dropdown.png)

1. Dal menu di scelta rapida hello, selezionare visualizzazione di hello desiderato: 

    - **Tipi di risorse** visualizzazione - hello comune utilizzato in hello [portale di Azure](http://go.microsoft.com/fwlink/p/?LinkID=525040), Mostra le risorse di Azure classificati in base al tipo, ad esempio applicazioni web, gli account di archiviazione e macchine virtuali. 
    - **Gruppi di risorse** visualizzazione - le risorse di Azure vengono suddivisi in categorie per il gruppo di risorse di Azure hello con cui si associato. Un gruppo di risorse è un bundle di risorse di Azure, in genere usate da un'applicazione specifica. toolearn altre informazioni sui gruppi di risorse di Azure, vedere [Panoramica di gestione risorse di Azure](./azure-resource-manager/resource-group-overview.md).

    Hello immagine seguente mostra un confronto di hello due viste di risorsa:

    ![Confronto tra visualizzazioni delle risorse di Cloud Explorer](media/vs-azure-tools-resources-managing-with-cloud-explorer/resource-views-comparison.png)

## <a name="view-and-navigate-resources-in-cloud-explorer"></a>Visualizzare ed esplorare le risorse in Cloud Explorer
toonavigate tooan risorse di Azure e visualizzare le informazioni in Cloud Explorer espandere tipo dell'elemento hello o un gruppo di risorse associati, quindi selezionare la risorsa hello. Quando si seleziona una risorsa, vengono visualizzate informazioni nelle schede hello due - **azioni** e **proprietà** : nella parte inferiore di hello del Cloud Explorer. 

- **Azioni** scheda - elenchi hello azioni eseguibili in Cloud Explorer per la risorsa hello selezionato. È inoltre possibile visualizzare queste opzioni facendo hello risorsa tooview menu di scelta rapida.

- **Proprietà** scheda - Visualizza le proprietà di hello della risorsa hello, ad esempio il gruppo di tipo, delle impostazioni locali e delle risorse a cui è associato.

Hello immagine seguente mostra un confronto di esempio di ciò che viene visualizzato in ogni scheda per un servizio App:

![](./media/vs-azure-tools-resources-managing-with-cloud-explorer/actions-and-properties.png)

Ogni risorsa ha azione hello **Apri nel portale di**. Quando si sceglie questa azione, Cloud Explorer consente di visualizzare risorse hello selezionato in hello [portale di Azure](http://go.microsoft.com/fwlink/p/?LinkID=525040). Hello **Apri nel portale** funzionalità è utile per spostarsi tra le risorse toodeeply annidati.

Azioni aggiuntive e i valori delle proprietà possono essere visualizzata anche in base alle risorse di Azure hello. Ad esempio, le applicazioni web e App per la logica anche avere azioni hello **Apri nel browser** e **collega debugger** inoltre troppo**Apri nel portale di**. Editor di azioni tooopen vengono visualizzati quando si sceglie un blob dell'account di archiviazione, una coda o una tabella. Per le app Azure sono disponibili le proprietà relative a **URL** e **stato**, mentre per le risorse di archiviazione sono disponibili le proprietà relative alle chiavi e alle stringhe di connessione.

## <a name="find-resources-in-cloud-explorer"></a>Cercare risorse in Cloud Explorer
risorse toolocate con un nome specifico in una delle sottoscrizioni di account di Azure, immettere il nome di hello in hello **ricerca** casella in Cloud Explorer.

![Ricerca di risorse in Cloud Explorer](./media/vs-azure-tools-resources-managing-with-cloud-explorer/search-for-resources.png)

Mentre si immettono caratteri in hello **ricerca** casella, solo le risorse che corrispondono a tali caratteri vengono visualizzati nell'albero di risorse hello.

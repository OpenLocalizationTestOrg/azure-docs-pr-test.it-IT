---
title: aaaGet un'introduzione ai modelli privati | Documenti Microsoft
description: Aggiungere, gestire e condividere i modelli privati utilizzando hello portale di Azure, hello CLI di Azure o PowerShell.
services: marketplace-customer
documentationcenter: 
author: VybavaRamadoss
manager: asimm
editor: 
tags: marketplace, azure-resource-manager
keywords: 
ms.assetid: 6ec20778-b578-4885-acb5-104b0e51ea1a
ms.service: marketplace
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 05/18/2016
ms.author: vybavar
ms.openlocfilehash: 1fe2c6422f62a98f7ae9ba5c61b9639d993f0bca
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-private-templates-on-hello-azure-portal"></a>Introduzione a modelli privati su hello portale di Azure
Un [Azure Resource Manager](../azure-resource-manager/resource-group-authoring-templates.md) modello è un modello dichiarativo utilizzato toodefine la distribuzione. È possibile definire hello toodeploy di risorse per una soluzione e specificare i parametri e variabili che consentono valori tooinput per ambienti diversi. Hello costituito da JSON e le espressioni che è possibile utilizzare valori tooconstruct per la distribuzione.

È possibile usare hello nuovo **modelli** funzionalità hello [portale Azure](https://portal.azure.com) insieme hello **Microsoft.Gallery** provider di risorse come estensione di hello [ Azure Marketplace](https://azure.microsoft.com/marketplace/) tooenable utenti toocreate, gestire e distribuire modelli privati da una libreria personale.

Questo documento illustra la procedura aggiunta, la gestione e condivisione privata **modello** utilizzando hello portale di Azure.

## <a name="guidance"></a>Indicazioni
Hello suggerimenti seguenti consentono di sfruttare appieno **modelli** quando si lavora con le soluzioni:

* Un **modello** è una risorsa di incapsulamento contenente un modello di Resource Manager e metadati aggiuntivi. Si comporta in modo molto simile elemento tooan hello Marketplace. la differenza principale Hello è che è un elemento privato come elementi del Marketplace pubblici toohello anziché.
* Hello **modelli** libreria funziona anche per gli utenti che richiedono toocustomize le distribuzioni.
* **modelli** permettono di usare un repository semplice all'interno di Azure.
* Iniziare con un modello di Resource Manager esistente. In [GitHub](https://github.com/Azure/azure-quickstart-templates) o nel post di blog relativo all'[esportazione modelli](../azure-resource-manager/resource-manager-export-template.md) è possibile trovare modelli a partire da un gruppo di risorse esistente.
* **Modelli** toohello collegati gli utenti che li pubblica. nome del server di pubblicazione Hello è visibile tooeveryone che dispone di accesso in lettura tooit.
* **modelli** sono risorse di Resource Manager e non possono essere rinominati dopo la pubblicazione.

## <a name="add-a-template-resource"></a>Aggiungere una risorsa modello
Esistono due modi toocreate un **modello** risorsa nel portale di Azure hello.

### <a name="method-1--create-a-new-template-resource-from-a-running-resource-group"></a>Metodo 1: creare una nuova risorsa modello da un gruppo di risorse in esecuzione
1. Passare tooan gruppo di risorse esistente nel portale di Azure hello. In **Impostazioni** selezionare **Esporta modello**.
2. Dopo aver esportato il modello di gestione risorse di hello, utilizzare hello **Salva modello** toosave pulsante è toohello **modelli** repository. Per informazioni dettagliate sull'esportazione di modelli, vedere questa [pagina](../azure-resource-manager/resource-manager-export-template.md).
   <br /><br />
   ![Esportazione di un gruppo di risorse](media/rg-export-portal1.PNG)  <br />
3. Seleziona hello **salvare tooTemplate** pulsante di comando.
   <br /><br />
4. Immettere hello le seguenti informazioni:
   
   * Name: nome dell'oggetto modello hello (Nota: questo è un nome di base di Azure Resource Manager. È soggetto a tutte le limitazioni relative all'assegnazione dei nomi non può essere modificato dopo la creazione.
   * Descrizione: riepilogo rapido sul modello hello.
     
     ![Salva modello](media/save-template-portal1.PNG)  <br />
5. Fare clic su **Salva**.
   
   > [!NOTE]
   > Hello pannello modello esportazione Mostra notifiche quando il modello di gestione delle risorse esportato hello presenta errori, ma sarà comunque in grado di toosave questo toohello modello di gestione risorse modelli. Assicurarsi di controllare e correggere problemi nel modello un gestore delle risorse prima di ridistribuzione hello esportata modello di gestione risorse.
   > 
   > 

### <a name="method-2--add-a-new-template-resource-from-browse"></a>Metodo 2: aggiungere una nuova risorsa modello dall'esplorazione
È inoltre possibile aggiungere un nuovo **modello** da zero utilizzando hello + Aggiungi pulsante di comando in **Sfoglia > modelli**. Tooprovide sarà necessario un nome, descrizione e il modello di gestione risorse JSON hello.

![Aggiungi modello](media/add-template-portal1.PNG)  <br />

> [!NOTE]
> Microsoft.Gallery è un provider di risorse di Azure basato su tenant. Hello risorsa modello è abbinato toohello utente che lo ha creato. Non è vincolata tooany specifica sottoscrizione. Una sottoscrizione deve toobe scelte solo durante la distribuzione di un modello.
> 
> 

## <a name="view-template-resources"></a>Visualizzare le risorse modello
Tutti **modelli** tooyou disponibili possono essere visualizzati in **Sfoglia > modelli**. Sono inclusi i **modelli** creati dall'utente e quelli condivisi con l'utente a vari livelli di autorizzazione. Altre informazioni, vedere hello [il controllo degli accessi](#access-control-for-a-tenant-resource-provider) sezione riportata di seguito.

![Visualizza modello](media/view-template-portal1.PNG)  <br />

È possibile visualizzare i dettagli di hello di un **modello** facendo clic in un elemento nell'elenco di hello.

![Visualizza modello](media/view-template-portal2c.png)  <br />

## <a name="edit-a-template-resource"></a>Modificare una risorsa modello
È possibile avviare il flusso di modifica hello per un **modello** dall'elemento di hello facendo clic su elenco hello o scegliendo pulsante di comando di modifica hello.

![Modifica modello](media/edit-template-portal1a.PNG)  <br />

È possibile modificare la descrizione hello o il testo del modello di gestione risorse. È possibile modificare il nome di hello perché è un nome di risorsa di gestione risorse. Quando si modifica il modello di gestione risorse di hello JSON è convaliderà tooensure è costituito da un oggetto JSON valido. Scegliere **OK** e quindi **salvare** toosave il modello aggiornato.

![Modifica modello](media/edit-template-portal2a.PNG)  <br />

Una volta hello **modello** viene salvato verrà visualizzata una notifica di conferma.

![Modifica modello](media/edit-template-portal3b.png)  <br />

## <a name="deploy-a-template-resource"></a>Distribuire una risorsa modello
È possibile distribuire qualsiasi **modello** per cui si hanno autorizzazioni di **lettura**. flusso di distribuzione Hello avvia pannello distribuzione il modello di Azure standard di hello. Compilare i valori hello per hello tooproceed parametri modello di gestione delle risorse con la distribuzione di hello.

![Modello di distribuzione](media/deploy-template-portal1b.png)  <br />

## <a name="share-a-template-resource"></a>Condividere una risorsa modello
È possibile condividere le risorse **modello** con altri utenti. Condivisione presenta un comportamento simile troppo[assegnazione di ruolo per qualsiasi risorsa di Azure](../active-directory/role-based-access-control-configure.md). Hello **modello** proprietario fornisce le autorizzazioni tooother gli utenti possono interagire con una risorsa di modello. Hello persona o il gruppo di utenti condividere hello **modello** sarà in grado di toosee modello di gestione risorse di hello e le relative proprietà di raccolta.

### <a name="access-control-for-hello-microsoftgallery-resources"></a>Controllo di accesso per le risorse Microsoft.Gallery hello
| Ruolo | Autorizzazioni |
| --- | --- |
| Proprietario |Consente il controllo completo su una risorsa modello di hello inclusi condivisione |
| Reader |Consente di lettura ed Execute(Deploy) su hello risorsa modello |
| Collaboratore |Consente l'autorizzazione per modificare ed eliminare hello risorse modello. Utente non può condividere hello modello con altri utenti |

Selezionare **condivisione** sull'elemento di visualizzazione hello facendo clic o nel Pannello di visualizzazione hello di un elemento specifico. Verrà avviata la condivisione.

![Condividi modello](media/share-template-portal1a.png)  <br />

 È ora possibile scegliere un ruolo e un utente o gruppo tooprovide accesso tooa particolare **modello**. i ruoli disponibili Hello sono proprietario, il lettore e collaboratore. Altre informazioni, vedere hello [il controllo degli accessi](#access-control-for-a-tenant-resource-provider) sezione precedente.

![Condividi modello](media/share-template-portal2b.png)  <br />

![Condividi modello](media/share-template-portal3b.png)  <br />

Fare clic su **Seleziona** e quindi su **OK**. È ora possibile visualizzare hello utenti o gruppi aggiunti toohello risorse.

![Condividi modello](media/share-template-portal4b.png)  <br />

> [!NOTE]
> Un modello può essere condiviso solo con utenti e gruppi in hello stesso tenant di Azure Active Directory. Se si condivide un modello con un indirizzo di posta elettronica che non è nel tenant, verrà inviato un invito porre tenant di hello utente toojoin hello come guest.
> 
> 

## <a name="next-steps"></a>Passaggi successivi
* toolearn sulla creazione di modelli di gestione delle risorse, vedere [creazione di modelli](../azure-resource-manager/resource-group-authoring-templates.md)
* le funzioni hello toounderstand è possibile utilizzare in un modello di gestione delle risorse, vedere [funzioni di modello](../azure-resource-manager/resource-group-template-functions.md)
* Per informazioni aggiuntive sulla progettazione di modelli, vedere [Procedure consigliate per la progettazione di modelli di Gestione risorse di Azure](../azure-resource-manager/best-practices-resource-manager-design-templates.md)


---
title: un'app web con un modello - DB Cosmos Azure aaaDeploy | Documenti Microsoft
description: Informazioni su come toodeploy un account Azure Cosmos DB App Web di servizio App di Azure e un esempio di utilizzo di un modello di gestione risorse di Azure di applicazioni web.
services: cosmos-db, app-service\web
author: mimig1
manager: jhubbard
editor: monicar
documentationcenter: 
ms.assetid: 087d8786-1155-42c7-924b-0eaba5a8b3e0
ms.service: cosmos-db
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 12/08/2016
ms.author: mimig
ms.openlocfilehash: b2bdde9279aad570606d7bf06dfc710f564b4d0c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-azure-cosmos-db-and-azure-app-service-web-apps-using-an-azure-resource-manager-template"></a>Distribuire Azure Cosmos DB e app Web del servizio app di Azure tramite un modello di Azure Resource Manager
In questa esercitazione illustra come toouse un toodeploy modello di gestione risorse di Azure e integrare [DB di Microsoft Azure Cosmos](https://azure.microsoft.com/services/cosmos-db/), un [Azure App Service](http://go.microsoft.com/fwlink/?LinkId=529714) app web e un'applicazione web di esempio.

Utilizzo di modelli di gestione risorse di Azure, è possibile automatizzare facilmente hello distribuzione e configurazione delle risorse di Azure.  Questa esercitazione viene illustrato come toodeploy un'applicazione web e configurare automaticamente le informazioni di connessione di account Azure Cosmos DB.

Dopo aver completato questa esercitazione, sarà in grado di tooanswer hello seguenti domande:  

* Come è possibile utilizzare un toodeploy modello di gestione risorse di Azure e integrazione di un account Azure Cosmos DB e un'app web nel servizio App di Azure?
* Come è possibile utilizzare un toodeploy modello di gestione risorse di Azure e integrare un'applicazione Webdeploy, un'app web nel servizio App dell'App Web e un account Azure Cosmos DB?

<a id="Prerequisites"></a>

## <a name="prerequisites"></a>Prerequisiti
> [!TIP]
> Durante questa esercitazione si presume precedente esperienza con i modelli di gestione risorse di Azure o JSON, si desidera hello toomodify fa riferimento a modelli o le opzioni di distribuzione, quindi sarà necessaria una conoscenza di ognuna di queste aree.
> 
> 

Prima di seguire le istruzioni di hello in questa esercitazione, assicurarsi di aver seguito hello:

* Una sottoscrizione di Azure. Azure è una piattaforma basata su sottoscrizione.  Per altre informazioni su come ottenere una sottoscrizione, vedere [Opzioni di acquisto](https://azure.microsoft.com/pricing/purchase-options/), [Offerte per i membri](https://azure.microsoft.com/pricing/member-offers/) oppure [Versione di valutazione gratuita](https://azure.microsoft.com/pricing/free-trial/).

## <a id="CreateDB"></a>Passaggio 1: Scaricare file di modello hello
Per iniziare, scaricare il file di modello hello che verrà utilizzato in questa esercitazione.

1. Scaricare hello [creare un account Azure Cosmos DB, le applicazioni Web e distribuire un esempio di applicazione demo](https://portalcontent.blob.core.windows.net/samples/DocDBWebsiteTodo.json) cartella locale tooa modello (ad esempio C:\Azure Cosmos DBTemplates). Questo modello distribuirà un account Azure Cosmos DB, un'app Web del servizio app e un'applicazione Web.  Verrà configurato automaticamente anche account Azure Cosmos DB toohello tooconnect dell'applicazione web di hello.
2. Scaricare hello [creare un account Azure Cosmos DB e un esempio di App Web](https://portalcontent.blob.core.windows.net/samples/DocDBWebSite.json) cartella locale tooa modello (ad esempio C:\Azure Cosmos DBTemplates). Questo modello verrà distribuito a un account Azure Cosmos DB, un'app web di servizio App e verrà modificato applicazione impostazioni tooeasily area Azure Cosmos DB informazioni di connessione del sito hello, ma non include un'applicazione web.  

<a id="Build"></a>

## <a name="step-2-deploy-hello-azure-cosmos-db-account-app-service-web-app-and-demo-application-sample"></a>Passaggio 2: Distribuire l'account di Azure Cosmos DB hello, servizio App web app e demo di esempio di applicazione
Si procederà a questo punto alla distribuzione del primo modello.

> [!TIP]
> modello di Hello non convalidare hello nome dell'applicazione web e il nome di account Azure Cosmos DB immesso di sotto) valido e b) disponibile.  Si consiglia di verificare la disponibilità di hello di hello Nome pianificare la distribuzione di hello toosupply toosubmitting precedente.
> 
> 

1. Account di accesso toohello [portale Azure](https://portal.azure.com), fare clic su Nuovo e cercare "Distribuzione del modello".
    ![Schermata di distribuzione del modello hello dell'interfaccia utente](./media/create-website/TemplateDeployment1.png)
2. Selezionare l'elemento di distribuzione modello hello e fare clic su **crea** ![schermata della distribuzione del modello hello dell'interfaccia utente](./media/create-website/TemplateDeployment2.png)
3. Fare clic su **modifica modelli**, incollare il contenuto di hello hello DocDBWebsiteTodo.json del file di modello e fare clic su **salvare**.
   ![Schermata di distribuzione del modello hello dell'interfaccia utente](./media/create-website/TemplateDeployment3.png)
4. Fare clic su **modificare parametri**, fornire i valori per ognuno dei parametri obbligatori hello e fare clic su **OK**.  come indicato di seguito sono riportati i parametri di Hello:
   
   1. Nome sito: Specifica hello Nome applicazione di servizio App web ed è utilizzato tooconstruct hello URL che si utilizzerà tooaccess hello web app (ad esempio, se si specifica "mydemodocdbwebapp", quindi sarà hello URL da cui si accederà hello web app mydemodocdbwebapp.azurewebsites.NET).
   2. HOSTINGPLANNAME: Specifica il nome di hello del servizio App toocreate piano di hosting.
   3. PERCORSO: Specifica hello Azure posizione in cui toocreate hello Azure Cosmos DB e app risorse web.
   4. DATABASEACCOUNTNAME: Specifica il nome di hello di hello Azure Cosmos DB account toocreate.   
      
      ![Schermata di distribuzione del modello hello dell'interfaccia utente](./media/create-website/TemplateDeployment4.png)
5. Scegliere un gruppo di risorse esistente o fornire un nome toomake un nuovo gruppo di risorse e scegliere un percorso per il gruppo di risorse hello.

    ![Schermata di distribuzione del modello hello dell'interfaccia utente](./media/create-website/TemplateDeployment5.png)
6. Fare clic su **esaminare le note legali**, **acquisto**, quindi fare clic su **crea** distribuzione hello toobegin.  Selezionare **toodashboard Pin** distribuzione risultante hello è facilmente visibile nella pagina Home page del portale Azure.
   ![Schermata di distribuzione del modello hello dell'interfaccia utente](./media/create-website/TemplateDeployment6.png)
7. Al termine della distribuzione di hello, si aprirà pannello della risorsa gruppo hello.
   ![Schermata del Pannello di gruppo di risorse hello](./media/create-website/TemplateDeployment7.png)  
8. toouse hello applicazione, passare semplicemente l'URL dell'app web toohello (nell'esempio hello sopra, hello URL sarebbe http://mydemodocdbwebapp.azurewebsites.net).  Si noterà hello dopo l'applicazione web:
   
   ![Applicazione di esempio](./media/create-website/image2.png)
9. Vado avanti e creare un paio di attività in hello web app e quindi tornare toohello pannello gruppo della risorsa nel portale di Azure hello. Fare clic sulla risorsa di account Azure Cosmos DB hello nell'elenco di risorse hello e quindi fare clic su **Esplora Query**.
    ![Schermata di hello riepilogo obiettivo con app web hello evidenziato](./media/create-website/TemplateDeployment8.png)  
10. Eseguire una query predefinita hello, "selezionare * da c" ed esaminare i risultati di hello.  Si noti che eseguono query hello ha recuperato una rappresentazione JSON hello delle attività hello creato nel passaggio 7 precedente.  È gratuito tooexperiment con query. ad esempio, provare a eseguire SELECT * FROM c WHERE c.isComplete = true tooreturn tutti gli elementi di attività che sono stati contrassegnati come completati.
    
    ![Schermata dei pannelli Esplora Query e i risultati mostrano i risultati di query hello, hello](./media/create-website/image5.png)
11. È gratuita tooexplore hello esperienza del portale Azure Cosmos DB o modificare un'applicazione Todo esempio hello.  A questo punto si è pronti per distribuire un altro modello.

<a id="Build"></a> 

## <a name="step-3-deploy-hello-document-account-and-web-app-sample"></a>Passaggio 3: Distribuire hello account documento e l'esempio di app web
Si procederà ora alla distribuzione del secondo modello.  Questo modello è utile tooshow come è possibile inserire informazioni di connessione di database di Azure Cosmos quali endpoint dell'account e la chiave master in un'app web, come le impostazioni dell'applicazione o come una stringa di connessione personalizzata. Ad esempio, potrebbe essere la propria applicazione web che desideri toodeploy con un account Azure Cosmos DB e le informazioni di connessione hello popolato automaticamente durante la distribuzione.

> [!TIP]
> modello di Hello non convalidare hello nome dell'applicazione web e il nome di account Azure Cosmos DB immesso di sotto) valido e b) disponibile.  Si consiglia di verificare la disponibilità di hello di hello Nome pianificare la distribuzione di hello toosupply toosubmitting precedente.
> 
> 

1. In hello [portale Azure](https://portal.azure.com), fare clic su Nuovo e cercare "Distribuzione del modello".
    ![Schermata di distribuzione del modello hello dell'interfaccia utente](./media/create-website/TemplateDeployment1.png)
2. Selezionare l'elemento di distribuzione modello hello e fare clic su **crea** ![schermata della distribuzione del modello hello dell'interfaccia utente](./media/create-website/TemplateDeployment2.png)
3. Fare clic su **modifica modelli**, incollare il contenuto di hello hello DocDBWebSite.json del file di modello e fare clic su **salvare**.
   ![Schermata di distribuzione del modello hello dell'interfaccia utente](./media/create-website/TemplateDeployment3.png)
4. Fare clic su **modificare parametri**, fornire i valori per ognuno dei parametri obbligatori hello e fare clic su **OK**.  come indicato di seguito sono riportati i parametri di Hello:
   
   1. Nome sito: Specifica hello Nome applicazione di servizio App web ed è utilizzato tooconstruct hello URL che si utilizzerà tooaccess hello web app (ad esempio, se si specifica "mydemodocdbwebapp", quindi sarà hello URL da cui si accederà hello web app mydemodocdbwebapp.azurewebsites.NET).
   2. HOSTINGPLANNAME: Specifica il nome di hello del servizio App toocreate piano di hosting.
   3. PERCORSO: Specifica hello Azure posizione in cui toocreate hello Azure Cosmos DB e app risorse web.
   4. DATABASEACCOUNTNAME: Specifica il nome di hello di hello Azure Cosmos DB account toocreate.   
      
      ![Schermata di distribuzione del modello hello dell'interfaccia utente](./media/create-website/TemplateDeployment4.png)
5. Scegliere un gruppo di risorse esistente o fornire un nome toomake un nuovo gruppo di risorse e scegliere un percorso per il gruppo di risorse hello.

    ![Schermata di distribuzione del modello hello dell'interfaccia utente](./media/create-website/TemplateDeployment5.png)
6. Fare clic su **esaminare le note legali**, **acquisto**, quindi fare clic su **crea** distribuzione hello toobegin.  Selezionare **toodashboard Pin** distribuzione risultante hello è facilmente visibile nella pagina Home page del portale Azure.
   ![Schermata di distribuzione del modello hello dell'interfaccia utente](./media/create-website/TemplateDeployment6.png)
7. Al termine della distribuzione di hello, si aprirà pannello della risorsa gruppo hello.
   ![Schermata del Pannello di gruppo di risorse hello](./media/create-website/TemplateDeployment7.png)  
8. Fare clic sulla risorsa App Web hello nell'elenco di risorse hello e quindi fare clic su **le impostazioni dell'applicazione** ![schermata hello del gruppo di risorse](./media/create-website/TemplateDeployment9.png)  
9. Si noti sono presenti per l'endpoint di Azure Cosmos DB hello e ognuna delle chiavi master di database di Azure Cosmos hello le impostazioni dell'applicazione.

    ![Screenshot delle impostazioni dell'applicazione](./media/create-website/TemplateDeployment10.png)  
10. È gratuito toocontinue esplorazione hello portale di Azure o seguire uno dei nostri DB Cosmos Azure [esempi](http://go.microsoft.com/fwlink/?LinkID=402386) toocreate un'applicazione Azure Cosmos DB.

<a name="NextSteps"></a>

## <a name="next-steps"></a>Passaggi successivi
Congratulazioni. È stata completata la distribuzione di Azure Cosmos DB, di un'app Web del servizio app e di un'applicazione Web di esempio usando i modelli di Azure Resource Manager.

* Fare clic su toolearn ulteriori informazioni su Azure Cosmos DB, [qui](http://azure.com/docdb).
* toolearn ulteriori informazioni sull'App Web di servizio App di Azure, fare clic su [qui](http://go.microsoft.com/fwlink/?LinkId=325362).
* toolearn più sui modelli di gestione risorse di Azure, fare clic su [qui](https://msdn.microsoft.com/library/azure/dn790549.aspx).

## <a name="whats-changed"></a>Modifiche apportate
* Per una Guida toohello modifica da siti Web tooApp servizio vedere: [relativo impatto sui servizi di Azure esistente e servizio App di Azure](http://go.microsoft.com/fwlink/?LinkId=529714)
* Per una Guida toohello change hello vecchio portale toohello nuovo portale, vedere: [riferimento per la navigazione hello portale classico di Azure](http://go.microsoft.com/fwlink/?LinkId=529715)

> [!NOTE]
> Se si desidera tooget avviato con il servizio App di Azure prima di effettuare l'iscrizione per un account Azure, andare troppo[tenta di servizio App](http://go.microsoft.com/fwlink/?LinkId=523751), in cui è possibile creare subito un'app web di breve durata starter nel servizio App. Non è necessario fornire una carta di credito né impegnarsi in alcun modo.
> 
> 


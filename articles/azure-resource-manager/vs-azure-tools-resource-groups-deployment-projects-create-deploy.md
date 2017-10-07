---
title: progetti di gruppo di risorse Azure Studio aaaVisual | Documenti Microsoft
description: Utilizzare Visual Studio toocreate un progetto di gruppo di risorse di Azure e distribuire tooAzure risorse hello.
services: azure-resource-manager
documentationcenter: na
author: tfitzmac
manager: timlt
editor: tysonn
ms.assetid: 4bd084c8-0842-4a10-8460-080c6a085bec
ms.service: azure-resource-manager
ms.devlang: multiple
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/10/2017
ms.author: tomfitz
ms.openlocfilehash: 672c1e71fb809b3b547f0fad30240d45de1ba923
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="creating-and-deploying-azure-resource-groups-through-visual-studio"></a>Creazione e distribuzione di gruppi di risorse di Azure tramite Visual Studio
Con Visual Studio e hello [Azure SDK](https://azure.microsoft.com/downloads/), è possibile creare un progetto che distribuisce tooAzure l'infrastruttura e il codice. Ad esempio, definire hello web host, il sito web e database per l'app e distribuire un'infrastruttura che insieme al codice hello. In alternativa, è possibile definire una macchina virtuale, una rete virtuale e un account di archiviazione e distribuire questa infrastruttura insieme a uno script che viene eseguito nella macchina virtuale. Hello **il gruppo di risorse di Azure** progetto di distribuzione consente si toodeploy tutte le risorse necessita hello in un'operazione singola e ripetibile. Per altre informazioni sulla distribuzione e sulla gestione delle risorse, vedere [Panoramica di Azure Resource Manager](resource-group-overview.md).

Progetti di gruppo di risorse di Azure contengono modelli JSON Gestione risorse di Azure, che definiscono le risorse di hello distribuire tooAzure. toolearn sugli elementi hello del modello di gestione risorse di hello, vedere [modelli Authoring Azure Resource Manager](resource-group-authoring-templates.md). Visual Studio consente di questi modelli è tooedit e sono disponibili strumenti che semplificano l'utilizzo dei modelli.

In questo articolo viene eseguita la distribuzione di un'app Web e un database SQL. Passaggi di hello, tuttavia, sono quasi hello lo stesso per qualsiasi tipo di risorsa. È possibile distribuire con altrettanta facilità una macchina virtuale e le rispettive risorse. Visual Studio offre molti modelli di partenza per la distribuzione di scenari comuni.

Questo articolo illustra la procedura per Visual Studio 2017. Se si utilizza Visual Studio 2015 Update 2 e Microsoft Azure SDK per .NET 2.9, o è in gran parte di Visual Studio 2013 con Azure SDK 2.9, l'esperienza di hello stesso. È possibile utilizzare le versioni di hello Azure SDK da 2.6 o versione successiva. Tuttavia, l'esperienza dell'interfaccia utente di hello può essere diverso da quello dell'interfaccia utente di hello illustrato in questo articolo. Si consiglia di installare una versione più recente di hello di hello [Azure SDK](https://azure.microsoft.com/downloads/) prima di iniziare i passaggi di hello. 

## <a name="create-azure-resource-group-project"></a>Creare un progetto Gruppo di risorse di Azure
In questa procedura verrà creato un progetto Gruppo di risorse di Azure con un modello **App Web e SQL** .

1. In Visual Studio scegliere **File**, **Nuovo progetto**, scegliere **C#** o **Visual Basic**. Scegliere quindi **Cloud** e scegliere il progetto **Gruppo di risorse di Azure**.
   
    ![Progetto Distribuzione cloud](./media/vs-azure-tools-resource-groups-deployment-projects-create-deploy/create-project.png)
2. Scegliere il modello di hello che si desidera toodeploy tooAzure Gestione risorse. Si noti che esistono molte opzioni diverse in base a hello tipo di progetto a cui toodeploy. Per questo articolo, scegliere hello **Web app + SQL** modello.
   
    ![Scelta di un modello](./media/vs-azure-tools-resource-groups-deployment-projects-create-deploy/select-project.png)
   
    modello di Hello che si sceglie è solo un punto di partenza; è possibile aggiungere e rimuovere risorse toofulfill lo scenario.
   
   > [!NOTE]
   > Visual Studio consente di recuperare un elenco dei modelli disponibili online. elenco di Hello potrebbe cambiare.
   > 
   > 
   
    Visual Studio crea un progetto di distribuzione gruppo di risorse per app web hello e database SQL.
3. toosee cosa è stato creato, cercare nel nodo hello nel progetto di distribuzione hello.
   
    ![visualizzazione dei nodi](./media/vs-azure-tools-resource-groups-deployment-projects-create-deploy/show-items.png)
   
    Poiché è stato scelto di app Web hello + modello SQL per questo esempio, viene visualizzato hello i seguenti file: 
   
   | Nome file | Descrizione |
   | --- | --- |
   | Deploy-AzureResourceGroup.ps1 |Uno script di PowerShell che richiama tooAzure toodeploy tramite i comandi PowerShell Gestione risorse.<br />**Nota** Visual Studio viene utilizzato il modello di questo toodeploy di script di PowerShell. Le modifiche apportate toothis script influiscono sulla distribuzione in Visual Studio, occorre quindi prestare attenzione. |
   | WebSiteSQLDatabase.json |modello di gestione risorse di Hello che definisce l'infrastruttura di hello che si desidera distribuire tooAzure e i parametri di hello che è possibile specificare durante la distribuzione. Definisce inoltre le dipendenze di hello tra risorse hello in modo da Gestione risorse consente di distribuire risorse hello nell'ordine corretto hello. |
   | WebSiteSQLDatabase.parameters.json |File dei parametri contenente valori necessari per il modello di hello. Passare nel parametro valori toocustomize ogni distribuzione. |
   
    Tutti i progetti di distribuzione di tipo Gruppo di risorse contengono questi file di base. Altri progetti potrebbero includere file aggiuntivi toosupport altre funzionalità.

## <a name="customize-hello-resource-manager-template"></a>Personalizzare il modello di gestione risorse di hello
È possibile personalizzare un progetto di distribuzione modificando i modelli di hello JSON che descrivono risorse hello è toodeploy. JSON è l'acronimo di JavaScript Object Notation ed è un formato dati serializzati facile toowork con. file JSON Hello usano uno schema a cui si fa riferimento nella parte superiore di hello di ogni file. Se si desidera schema hello toounderstand, è possibile scaricare e analizzarlo. Hello schema definisce gli elementi sono validi, hello tipi e i formati dei campi, hello i valori possibili dei valori enumerati e così via. toolearn sugli elementi hello del modello di gestione risorse di hello, vedere [modelli Authoring Azure Resource Manager](resource-group-authoring-templates.md).

Aprire toowork sul modello di **WebSiteSQLDatabase.json**.

Hello Visual Studio, l'editor fornisce strumenti tooassist si con funzionalità di modifica hello modello di gestione risorse. Hello **struttura JSON** finestra rende più facile toosee gli elementi di hello definiti nel modello.

![visualizzazione della struttura JSON](./media/vs-azure-tools-resource-groups-deployment-projects-create-deploy/show-json-outline.png)

Selezionare gli elementi di hello nella struttura hello consente toothat parte del modello di hello ed evidenziare hello corrispondente JSON.

![esplorazione di JSON](./media/vs-azure-tools-resource-groups-deployment-projects-create-deploy/navigate-json.png)

È possibile aggiungere una risorsa da una seleziona hello **Aggiungi risorsa** pulsante nella parte superiore di hello della finestra Struttura JSON hello o facendo clic **risorse** e selezionando **Aggiungi nuova risorsa**.

![aggiungere una risorsa](./media/vs-azure-tools-resource-groups-deployment-projects-create-deploy/add-resource.png)

Per questa esercitazione selezionare **Account di archiviazione** e specificare un nome. Specificare un nome contenente non più di 11 caratteri costituiti solo da numeri e lettere minuscole.

![aggiunta di una risorsa di archiviazione](./media/vs-azure-tools-resource-groups-deployment-projects-create-deploy/add-storage.png)

Si noti che non solo è stata aggiunta la risorsa hello, ma anche un parametro per hello digitare l'account di archiviazione e una variabile per il nome dell'account di archiviazione hello hello.

![visualizzazione della struttura](./media/vs-azure-tools-resource-groups-deployment-projects-create-deploy/show-new-items.png)

Hello **storageType** parametro è definito con i tipi consentiti e un tipo predefinito. È possibile usare questi valori o modificarli per il proprio scenario. Se non si desidera che tutti gli utenti toodeploy un **Premium_LRS** account di archiviazione con questo modello, rimuoverlo da hello tipi consentito. 

```json
"storageType": {
  "type": "string",
  "defaultValue": "Standard_LRS",
  "allowedValues": [
    "Standard_LRS",
    "Standard_ZRS",
    "Standard_GRS",
    "Standard_RAGRS"
  ]
}
```

Visual Studio fornisce inoltre toohelp intellisense è comprendere quali proprietà sono disponibili quando si modifica il modello di hello. Ad esempio, le proprietà di hello tooedit per il piano di servizio App, passare toohello **HostingPlan** risorsa e aggiungere un valore per hello **proprietà**. Si noti che intellisense Mostra i valori disponibili hello e viene fornita una descrizione di tale valore.

![visualizzazione di IntelliSense](./media/vs-azure-tools-resource-groups-deployment-projects-create-deploy/show-intellisense.png)

È possibile impostare **il numero di lavori** too1.

```json
"properties": {
  "name": "[parameters('hostingPlanName')]",
  "numberOfWorkers": 1
}
```

## <a name="deploy-hello-resource-group-project-tooazure"></a>Distribuire hello gruppo di risorse progetto tooAzure
Si sono ora pronti toodeploy il progetto. Quando si distribuisce un progetto di gruppo di risorse di Azure, si distribuisce il gruppo di risorse di Azure tooan. gruppo di risorse Hello è un raggruppamento logico di risorse che condividono un ciclo di vita comune.

1. Scegliere hello dal menu di scelta rapida del nodo di progetto di distribuzione hello, **Distribuisci** > **New**.
   
    ![Voce di menu Distribuisci, Nuova distribuzione](./media/vs-azure-tools-resource-groups-deployment-projects-create-deploy/deploy.png)
   
    Hello **distribuire tooResource gruppo** viene visualizzata la finestra di dialogo.
   
    ![Distribuire tooResource la finestra di dialogo di gruppo](./media/vs-azure-tools-resource-groups-deployment-projects-create-deploy/show-deployment.png)
2. In hello **gruppo di risorse** casella a discesa, scegliere un gruppo di risorse esistente o crearne uno nuovo. toocreate un gruppo di risorse, aprire hello **gruppo di risorse** elenco a discesa e scegliere **Crea nuovo**.
   
    ![Distribuire tooResource la finestra di dialogo di gruppo](./media/vs-azure-tools-resource-groups-deployment-projects-create-deploy/create-new-group.png)
   
    Hello **Crea gruppo di risorse** viene visualizzata la finestra di dialogo. Assegnare al gruppo un nome e il percorso e selezionare hello **crea** pulsante.
   
    ![Finestra di dialogo Crea gruppo di risorse](./media/vs-azure-tools-resource-groups-deployment-projects-create-deploy/create-resource-group.png)
3. Modificare i parametri di hello per la distribuzione di hello selezionando hello **modifica parametri** pulsante.
   
    ![Pulsante Modifica parametri](./media/vs-azure-tools-resource-groups-deployment-projects-create-deploy/edit-parameters.png)
4. Fornire valori per parametri vuoto hello e selezionare hello **salvare** pulsante. i parametri vuoto Hello sono **hostingPlanName**, **administratorLogin**, **administratorLoginPassword**, e **databaseName**.
   
    **hostingPlanName** specifica un nome per hello [piano di servizio App](../app-service/azure-web-sites-web-hosting-plans-in-depth-overview.md) toocreate. 
   
    **administratorLogin** specifica il nome utente hello per l'amministratore di SQL Server hello. Non usare nomi di amministratore comuni, ad esempio **sa** o **admin**. 
   
    Hello **administratorLoginPassword** specifica una password per l'amministratore di SQL Server. Hello **salvare le password come testo normale nel file dei parametri hello** opzione non è sicura; pertanto, non selezionare questa opzione. Poiché la password di hello non viene salvata come testo normale, è necessario tooprovide questa password nuovamente durante la distribuzione. 
   
    **databaseName** specifica un nome per hello toocreate di database. 
   
    ![Finestra di dialogo Modifica parametri](./media/vs-azure-tools-resource-groups-deployment-projects-create-deploy/provide-parameters.png)
5. Scegliere hello **Distribuisci** pulsante toodeploy hello progetto tooAzure. Consente di aprire una console di PowerShell all'esterno di istanza di Visual Studio hello. Immettere la password di amministratore SQL Server hello nella console di PowerShell hello quando richiesto. **La console di PowerShell può essere nascosta da altri elementi o ridotta a icona nella barra delle applicazioni hello.** Cercare la console e selezionarlo password hello tooprovide.
   
   > [!NOTE]
   > Visual Studio potrebbe essere richiesto tooinstall hello cmdlet di Azure PowerShell. È necessario hello Azure PowerShell cmdlet toosuccessfully distribuire gruppi di risorse. Se richiesto, occorre installarli.
   > 
   > 
6. distribuzione di Hello potrebbe richiedere alcuni minuti. In hello **Output** windows, viene visualizzato lo stato di hello della distribuzione hello. Al termine della distribuzione di hello, ultimo messaggio hello indica una corretta distribuzione con un risultato simile a:
   
        ... 
        18:00:58 - Successfully deployed template 'websitesqldatabase.json' tooresource group 'DemoSiteGroup'.
7. In un browser, aprire hello [portale di Azure](https://portal.azure.com/) ed eseguire l'accesso tooyour account. toosee hello gruppo di risorse, seleziona **gruppi di risorse** e gruppo di risorse hello è distribuito.
   
    ![selezione di un gruppo](./media/vs-azure-tools-resource-groups-deployment-projects-create-deploy/select-group.png)
8. Visualizzare tutte le risorse di hello distribuito. Si noti che il nome hello del hello account di archiviazione non è esattamente ciò che si è specificato durante l'aggiunta di tale risorsa. account di archiviazione Hello devono essere univoci. Hello modello aggiunge automaticamente una stringa del nome toohello di caratteri immessa tooprovide un nome univoco. 
   
    ![visualizzazione delle risorse](./media/vs-azure-tools-resource-groups-deployment-projects-create-deploy/show-deployed-resources.png)
9. Se si apportano modifiche e si desidera tooredeploy il progetto, scegliere il gruppo di risorse esistente hello hello menu di scelta rapida del progetto di gruppo di risorse di Azure. Scegliere dal menu di scelta rapida di hello **Distribuisci**, quindi scegliere il gruppo di risorse hello è stato distribuito.
   
    ![Gruppo di risorse di Azure distribuito](./media/vs-azure-tools-resource-groups-deployment-projects-create-deploy/redeploy.png)

## <a name="deploy-code-with-your-infrastructure"></a>Distribuire codice con l'infrastruttura
A questo punto, è stata distribuita un'infrastruttura di hello per l'app, ma non è presente codice effettivo distribuito con il progetto di hello. Questo articolo illustra come toodeploy un'app web e il Database SQL le tabelle durante la distribuzione. Se si distribuisce una macchina virtuale invece di un'app web, si desidera toorun codice nel computer di hello come parte della distribuzione. Hello processo per la distribuzione di codice per un'app web o per la configurazione di una macchina virtuale è quasi hello stesso.

1. Aggiungere un tooyour di progetto, soluzione di Visual Studio. Soluzione hello e scegliere **Aggiungi** > **nuovo progetto**.
   
    ![Aggiunta del progetto](./media/vs-azure-tools-resource-groups-deployment-projects-create-deploy/add-project.png)
2. Aggiungere un' **Applicazione Web ASP.NET**. 
   
    ![aggiunta di un'app Web](./media/vs-azure-tools-resource-groups-deployment-projects-create-deploy/add-app.png)
3. Selezionare **MVC**.
   
    ![selezione di MVC](./media/vs-azure-tools-resource-groups-deployment-projects-create-deploy/select-mvc.png)
4. Dopo Visual Studio crea app web, vengono visualizzati entrambi i progetti nella soluzione hello.
   
    ![Visualizzazione dei progetti](./media/vs-azure-tools-resource-groups-deployment-projects-create-deploy/show-projects.png)
5. A questo punto, è necessario toomake il progetto di gruppo di risorse di essere consapevole di nuovo progetto hello. Tornare indietro di progetto di gruppo di risorse tooyour (AzureResourceGroup1). Fare clic con il pulsante destro del mouse su **Riferimenti** e scegliere **Aggiungi riferimento**.
   
    ![Aggiungi riferimento](./media/vs-azure-tools-resource-groups-deployment-projects-create-deploy/add-new-reference.png)
6. Seleziona progetto di app web hello creato.
   
    ![Aggiungi riferimento](./media/vs-azure-tools-resource-groups-deployment-projects-create-deploy/add-reference.png)
   
    Aggiungendo un riferimento, collegare hello progetto toohello risorse gruppo progetto di app web e impostare tre proprietà chiave. Per visualizzare le proprietà questi hello **proprietà** finestra per riferimento hello.
   
      ![visualizzazione di un riferimento](./media/vs-azure-tools-resource-groups-deployment-projects-create-deploy/see-reference.png)
   
    proprietà Hello sono:
   
   * Hello **proprietà aggiuntive** contiene pacchetto di distribuzione web hello percorso inserito toohello di archiviazione di Azure di gestione temporanea. Si noti la cartella hello (ExampleApp) e file (package.zip). È necessario tooknow questi valori in quanto fornirli come parametri durante la distribuzione di hello app. 
   * Hello **del percorso di File di inclusione** contiene hello percorso in cui viene creato il pacchetto di hello. Hello **destinazioni includono** contiene hello comando che viene eseguita la distribuzione. 
   * il valore predefinito di Hello **compilazione; Pacchetto** Abilita distribuzione toobuild hello e creare un pacchetto di distribuzione web (package.zip).  
     
     Non è necessario un profilo di pubblicazione come distribuzione hello Ottiene le informazioni necessarie hello dal pacchetto di hello toocreate proprietà hello.
7. Tornare indietro tooWebSiteSQLDatabase.json e aggiungere un modello di risorsa toohello.
   
    ![aggiungere una risorsa](./media/vs-azure-tools-resource-groups-deployment-projects-create-deploy/add-resource-2.png)
8. Questa volta selezionare **Distribuzione Web per app Web**. 
   
    ![aggiunta della distribuzione Web](./media/vs-azure-tools-resource-groups-deployment-projects-create-deploy/add-web-deploy.png)
9. Ridistribuire il gruppo di risorse toohello project gruppo di risorse. Questa volta sono disponibili alcuni nuovi parametri. Non è necessario per i valori tooprovide **_artifactsLocation** o **_artifactsLocationSasToken** perché Visual Studio genera automaticamente tali valori. Tuttavia, è tooset hello cartella e il nome file toohello percorso contenente il pacchetto di distribuzione hello (visualizzate come **ExampleAppPackageFolder** e **ExampleAppPackageFileName** nella seguente immagine hello ). Fornire i valori hello è stato illustrato in precedenza nella hello le proprietà di riferimento (**ExampleApp** e **package.zip**).
   
    ![aggiunta della distribuzione Web](./media/vs-azure-tools-resource-groups-deployment-projects-create-deploy/set-new-parameters.png)
   
    Per hello **account di archiviazione di artefatti**, selezionare hello uno distribuito con il gruppo di risorse.
10. Al termine della distribuzione di hello, selezionare l'app web nel portale di hello. Selezionare hello URL toobrowse toohello sito.
    
     ![Esplorazione del sito](./media/vs-azure-tools-resource-groups-deployment-projects-create-deploy/browse-site.png)
11. Si noti che è stata distribuita applicazione ASP.NET predefinita hello.
    
     ![visualizzazione dell'app distribuita](./media/vs-azure-tools-resource-groups-deployment-projects-create-deploy/show-deployed-app.png)

## <a name="next-steps"></a>Passaggi successivi
* vedere toolearn sulla gestione delle risorse tramite il portale di hello [Using hello toomanage portale Azure le risorse di Azure](resource-group-portal.md).
* toolearn più informazioni sui modelli, vedere [modelli Authoring Azure Resource Manager](resource-group-authoring-templates.md).


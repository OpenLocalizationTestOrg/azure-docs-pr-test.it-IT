---
title: aaaCreate, compilare e distribuire App in Visual Studio - App Azure per la logica per la logica | Documenti Microsoft
description: Creare progetti di Visual Studio per poter progettare, compilare e distribuire app per la logica di Azure.
author: jeffhollan
manager: anneta
editor: 
services: logic-apps
documentationcenter: 
ms.assetid: e484e5ce-77e9-4fa9-bcbe-f851b4eb42a6
ms.service: logic-apps
ms.workload: integration
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.custom: H1Hack27Feb2017
ms.date: 2/14/2017
ms.author: LADocs; jehollan
ms.openlocfilehash: 5154cb05f9a48e9f0f2381a6953947217f7bb114
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="design-build-and-deploy-azure-logic-apps-in-visual-studio"></a>Progettare, compilare e distribuire app per la logica di Azure in Visual Studio

Sebbene hello [portale di Azure](https://portal.azure.com/) offre un modo eccellente per si toocreate e gestire le app di logica di Azure, è possibile utilizzare Visual Studio per la progettazione, compilazione e distribuzione di App per la logica. Visual Studio fornisce strumenti avanzati come hello progettazione applicazione logica per l'utente toocreate logica App, configurare i modelli di distribuzione e l'automazione e distribuire l'ambiente tooany. 

informazioni su tooget iniziare con le app di logica di Azure, [come toocreate la prima app logica nel portale di Azure hello](logic-apps-create-a-logic-app.md).

## <a name="installation-steps"></a>Procedura di installazione

tooinstall e configurare gli strumenti di Visual Studio per le app di logica di Azure, seguire questi passaggi.

### <a name="prerequisites"></a>Prerequisiti

* [Visual Studio 2017](https://www.visualstudio.com/downloads/download-visual-studio-vs.aspx) o Visual Studio 2015
* [Versione più recente di Azure SDK](https://azure.microsoft.com/downloads/) (2.9.1 o versione successiva)
* [Azure PowerShell](https://github.com/Azure/azure-powershell#installation)
* Web toohello Access quando si utilizza Progettazione incorporato hello

### <a name="install-visual-studio-tools-for-azure-logic-apps"></a>Installare gli strumenti di Visual Studio per le app per la logica di Azure

Dopo aver installato i prerequisiti di hello:

1. Aprire Visual Studio. In hello **strumenti** dal menu **estensioni e aggiornamenti**.
2. Espandere hello **Online** categoria, eseguire la ricerca online.
3. Sfogliare o cercare **App per la logica** per visualizzare **Azure Logic Apps Tools for Visual Studio** (Strumenti per app per la logica di Azure per Visual Studio).
4. toodownload e l'estensione di hello installazione, fare clic su **scaricare**.
5. Al termine dell'installazione riavviare Visual Studio.

> [!NOTE]
> È inoltre possibile scaricare [Azure logica App Tools per Visual Studio 2017](https://marketplace.visualstudio.com/items?itemName=VinaySinghMSFT.AzureLogicAppsToolsforVisualStudio-18551) hello e [Azure logica App Tools per Visual Studio 2015](https://marketplace.visualstudio.com/items?itemName=VinaySinghMSFT.AzureLogicAppsToolsforVisualStudio) direttamente da Visual Studio Marketplace hello.

Al termine dell'installazione, è possibile utilizzare il progetto di gruppo di risorse di Azure hello con logica di progettazione di App.

## <a name="create-your-project"></a>Creare il progetto

1. In hello **File** dal menu Vai troppo**New**e selezionare **progetto**. O tooadd tooan il progetto esistente di soluzione, andare troppo**Aggiungi**e selezionare **nuovo progetto**.

    ![File menu](./media/logic-apps-deploy-from-vs/filemenu.png)

2. In hello **nuovo progetto** finestra Trova **Cloud**e selezionare **il gruppo di risorse di Azure**. Assegnare un nome al progetto e fare clic su **OK**.

    ![Add new project](./media/logic-apps-deploy-from-vs/addnewproject.png)

3. Seleziona hello **logica App** modello, che viene creato un modello di distribuzione app vuota logica toouse. Dopo aver selezionato il modello, fare clic su **OK**.

    ![Selezionare il modello App per la logica](./media/logic-apps-deploy-from-vs/selectazuretemplate1.png)

    È stato aggiunto a questo punto soluzione logica app progetto tooyour. 
    In Esplora soluzioni hello, dovrebbe essere visualizzato il file di distribuzione.

    ![File di distribuzione](./media/logic-apps-deploy-from-vs/deployment.png)

## <a name="create-your-logic-app-with-logic-app-designer"></a>Creare l'app per la logica con la finestra di progettazione

Quando si dispone di un progetto di gruppo di risorse di Azure che contiene una logica app, è possibile aprire hello logica di progettazione di App in Visual Studio toocreate il flusso di lavoro. 

> [!NOTE]
> finestra di progettazione Hello richiede una connessione a internet eseguire una query troppo connettori per i dati e le proprietà disponibili. Ad esempio, se si utilizza hello connettore di Dynamics CRM Online, progettazione hello query il personalizzato CRM istanza tooshow disponibile e le proprietà predefinite.

1. Fare clic con il pulsante destro del mouse sul file `<template>.json` e scegliere **Open with Logic App Designer** (Apri con Progettazione app per la logica). (`Ctrl+L`)

2. Scegliere la sottoscrizione di Azure, il gruppo di risorse e la posizione per il modello di distribuzione.

    > [!NOTE]
    > Progettando un'app per la logica verranno create risorse di connessione API per l'esecuzione di query per ottenere le proprietà durante la progettazione. Visual Studio Usa il toocreate gruppo di risorse selezionato tali connessioni in fase di progettazione. tooview o modificare le connessioni di API, recarsi toohello portale di Azure e cercare **connessioni API**.

    ![Selezione della sottoscrizione](./media/logic-apps-deploy-from-vs/designer_picker.png)

    finestra di progettazione di Hello Usa definizione hello in hello `<template>.json` file per il rendering.

4. Creare e progettare l'app per la logica. Il modello di distribuzione viene aggiornato con le modifiche.

    ![Progettazione app per la logica in Visual Studio](./media/logic-apps-deploy-from-vs/designer_in_vs.png)

Visual Studio aggiunge `Microsoft.Web/connections` troppo la risorsa del file di risorse per tutte le connessioni app logica deve toofunction. Queste proprietà di connessione possono essere impostate durante la distribuzione e gestite dopo aver distribuito **connessioni API** in hello portale di Azure.

### <a name="switch-toojson-code-view"></a>Visualizzazione di codice tooJSON commutatore

hello tooshow rappresentazione JSON per l'app di logica, seleziona hello **visualizzazione codice** scheda nella parte inferiore di hello della finestra di progettazione hello.

tooswitch toohello completo della risorsa JSON di eseguire il pulsante destro del mouse hello `<template>.json` file e selezionare **aprire**.

### <a name="add-references-for-dependent-resources-toovisual-studio-deployment-templates"></a>Aggiungere i riferimenti per i modelli di distribuzione di risorse dipendenti tooVisual Studio

Quando si desidera che la logica app tooreference da risorse dipendenti, è possibile utilizzare [funzioni di modello di gestione risorse di Azure](https://docs.microsoft.com/azure/azure-resource-manager/resource-group-template-functions) nel modello di distribuzione di app logica. Ad esempio, è consigliabile il tooreference app logica un account Azure funzione o di integrazione che si desidera toodeploy insieme all'app di logica. Seguire queste linee guida sulle modalità di rendering correttamente toouse parametri nel modello di distribuzione in modo che hello progettazione applicazione logica. 

È possibile usare i parametri dell'app per la logica in questi tipi di trigger e azioni:

*   Flusso di lavoro figlio
*   App per le funzioni
*   Chiamata APIM
*   URL di runtime della connessione API
*   Percorso di connessione API

Ed è possibile usare le funzioni di modello, ad esempio parametri, variabili, resourceId, CONCAT e così via. Ad esempio, ecco come è possibile sostituire l'ID di risorsa di Azure funzione hello:

```
"parameters":{
    "functionName": {
        "type":"string",
        "minLength":1,
        "defaultValue":"<FunctionName>"
    }
},
```

E dove si useranno i parametri:

```
"MyFunction": {
    "type": "Function",
    "inputs": {
        "body":{},
        "function":{
            "id":"[resourceid('Microsoft.Web/sites/functions','functionApp',parameters('functionName'))]"
        }
    },
    "runAfter":{}
}
```
Un altro esempio è possibile parametrizzare hello Bus di servizio invia l'operazione di messaggio:

```
"Send_message": {
    "type": "ApiConnection",
        "inputs": {
            "host": {
                "connection": {
                    "name": "@parameters('$connections')['servicebus']['connectionId']"
                }
            },
            "method": "post",
            "path": "[concat('/@{encodeURIComponent(''', parameters('queueuname'), ''')}/messages')]",
            "body": {
                "ContentData": "@{base64(triggerBody())}"
            },
            "queries": {
                "systemProperties": "None"
            }
        },
        "runAfter": {}
    }
```
> [!NOTE] 
> host.runtimeUrl è facoltativo e può essere rimosso dal modello, se presente.
> 


> [!NOTE] 
> Per hello progettazione applicazione logica toowork quando si utilizzano parametri, è necessario fornire valori predefiniti, ad esempio:
> 
> ```
> "parameters": {
>     "IntegrationAccount": {
>     "type":"string",
>     "minLength":1,
>     "defaultValue":"/subscriptions/<subscriptionID>/resourceGroups/<resourceGroupName>/providers/Microsoft.Logic/integrationAccounts/<integrationAccountName>"
>     }
> },
> ```

### <a name="save-your-logic-app"></a>Salvare l'app per la logica

toosave app logica in qualsiasi momento, andare troppo**File** > **salvare**. (`Ctrl+S`) 

Se l'applicazione di logica ha tutti gli errori quando si salva l'applicazione, vengono visualizzati in Visual Studio hello **output** finestra.

## <a name="deploy-your-logic-app-from-visual-studio"></a>Distribuire l'app per la logica da Visual Studio

Dopo aver configurato l'app, è possibile distribuirla direttamente da Visual Studio in pochi passaggi. 

1. In Esplora risorse, mouse sul progetto e passare troppo**Distribuisci** > **nuova distribuzione...**

    ![New deployment](./media/logic-apps-deploy-from-vs/newdeployment.png)

2. Quando richiesto, accedere tooyour sottoscrizione di Azure. 

3. A questo punto è necessario selezionare i dettagli di hello per il gruppo di risorse hello in cui si desidera toodeploy app logica. Al termine, fare clic su **Distribuisci**.

    > [!NOTE]
    > Assicurarsi di selezionare il modello corretto di hello e file dei parametri per il gruppo di risorse hello. Ad esempio, se si desidera toodeploy tooa ambiente di produzione, scegliere file dei parametri di produzione hello.

    ![Distribuire un gruppo di tooresource](./media/logic-apps-deploy-from-vs/deploytoresourcegroup.png)

    viene visualizzato lo stato di distribuzione Hello in hello **Output** finestra. 
    Potrebbe essere tooselect **Azure Provisioning** in hello **Mostra output di** elenco.

    ![Output dello stato di distribuzione](./media/logic-apps-deploy-from-vs/output.png)

In futuro hello, è possibile modificare l'applicazione logica in un controllo del codice sorgente e utilizzare le nuove versioni toodeploy di Visual Studio.

> [!NOTE]
> Se si modifica direttamente la definizione di hello in hello portale di Azure, tali modifiche vengono sovrascritte durante la distribuzione da Visual Studio successivo. 

## <a name="add-your-logic-app-tooan-existing-resource-group-project"></a>Aggiungere il progetto di gruppo di risorse esistente logica app tooan

Se si dispone di un progetto di gruppo di risorse esistente, è possibile aggiungere il progetto di logica app toothat nella finestra Struttura JSON hello. È anche possibile aggiungere un'altra app logica insieme app hello creato in precedenza.

1. Aprire hello `<template>.json` file.

2. hello tooopen finestra Struttura JSON, andare troppo**vista** > **altre finestre** > **struttura JSON**.

3. Fare clic su un file modello di risorsa toohello, tooadd **Aggiungi risorsa** nella parte superiore di hello della finestra Struttura JSON hello. Nella finestra Struttura JSON hello mouse oppure **risorse**e selezionare **Aggiungi nuova risorsa**.

    ![Finestra Struttura JSON](./media/logic-apps-deploy-from-vs/jsonoutline.png)
    
4. In hello **Aggiungi risorsa** la finestra di dialogo, trovare e selezionare **logica App**. Dare un nome all'app per la logica e scegliere **Aggiungi**.

    ![Aggiungere una risorsa](./media/logic-apps-deploy-from-vs/addresource.png)

## <a name="next-steps"></a>Passaggi successivi

* [Gestire le app per la logica con Visual Studio Cloud Explorer](logic-apps-manage-from-vs.md)
* [Visualizzare esempi e scenari comuni](logic-apps-examples-and-scenarios.md)
* [Informazioni su come i processi di business tooautomate con Azure logica App](http://channel9.msdn.com/Events/Build/2016/T694)
* [Informazioni su come toointegrate i sistemi con Azure logica App](http://channel9.msdn.com/Events/Build/2016/P462)

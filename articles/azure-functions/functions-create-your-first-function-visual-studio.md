---
title: la prima funzione in Azure utilizzando Visual Studio aaaCreate | Documenti Microsoft
description: Creare e pubblicare un semplice tooAzure funzione HTTP attivato mediante gli strumenti di funzioni di Azure per Visual Studio.
services: functions
documentationcenter: na
author: rachelappel
manager: erikre
editor: 
tags: 
keywords: Funzioni di Azure, funzioni, elaborazione eventi, calcolo, architettura senza server
ms.assetid: 82db1177-2295-4e39-bd42-763f6082e796
ms.service: functions
ms.devlang: multiple
ms.topic: quickstart
ms.tgt_pltfrm: multiple
ms.workload: na
ms.date: 07/05/2017
ms.author: glenga
ms.custom: mvc
ms.openlocfilehash: 851e5b98dcc2da00334620896a0ea31f566589f7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="create-your-first-function-using-visual-studio"></a>Creare la prima funzione con Visual Studio

Funzioni di Azure consente di eseguire il codice in un ambiente senza server senza dover toofirst crea una macchina virtuale o si pubblica un'applicazione web.

In questo argomento, è illustrato come toouse hello 2017 di Visual Studio tools per toocreate funzioni di Azure e testare una funzione di "hello world" in locale. Verrà quindi pubblicato tooAzure codice di funzione hello. Questi strumenti sono disponibili come parte del carico di lavoro di hello lo sviluppo di Azure in Visual Studio 2017 versione 15.3 o versione successiva.

![Codice di Funzioni di Azure in un progetto di Visual Studio](./media/functions-create-your-first-function-visual-studio/functions-vstools-intro.png)

## <a name="prerequisites"></a>Prerequisiti

toocomplete questa esercitazione, installare:

* [Visual Studio 2017 versione 15.3](https://www.visualstudio.com/vs/preview/), tra cui hello **lo sviluppo di Azure** carico di lavoro.

    ![Installare Visual Studio 2017 con carico di lavoro di hello lo sviluppo di Azure](./media/functions-create-your-first-function-visual-studio/functions-vs-workloads.png)
    
    >[!NOTE]  
    Dopo l'installazione o aggiornamento tooVisual Studio 2017 versione 15.3, si potrebbe essere necessario anche strumenti di Visual Studio 2017 hello toomanually update per le funzioni di Azure. È possibile aggiornare gli strumenti hello hello **strumenti** menu sotto **estensioni e aggiornamenti...**   >  **Aggiornamenti** > **Visual Studio Marketplace** > **strumenti i processi di funzioni di Azure e Web**  >  **Aggiornamento**. 

[!INCLUDE [quickstarts-free-trial-note](../../includes/quickstarts-free-trial-note.md)] 

## <a name="create-an-azure-functions-project-in-visual-studio"></a>Creare un progetto Funzioni di Azure in Visual Studio

[!INCLUDE [Create a project using hello Azure Functions template](../../includes/functions-vstools-create.md)]

Ora che è stato creato il progetto di hello, è possibile creare la prima funzione.

## <a name="create-hello-function"></a>Creare la funzione hello

1. In **Esplora soluzioni** fare clic con il pulsante destro del mouse sul nodo del progetto e scegliere **Aggiungi** > **Nuovo elemento**. Selezionare **Funzione di Azure** e fare clic su **Aggiungi**.

2. Selezionare **HttpTrigger**, digitare un **nome di funzione**, selezionare **Anonimo** in **Diritti di accesso** e fare clic su **Crea**. funzione di Hello creato è accessibile tramite una richiesta HTTP da qualsiasi client. 

    ![Creare una nuova funzione di Azure](./media/functions-create-your-first-function-visual-studio/functions-vstools-add-new-function-2.png)

    Un file di codice viene aggiunto il progetto tooyour che contiene una classe che implementa il codice della funzione. Questo codice è basato su un modello, che riceve un valore di nome e lo ritrasmette. Hello **FunctionName** attributo imposta hello nome della funzione. Hello **HttpTrigger** attributo indica il messaggio hello che attiva la funzione hello. 

    ![File di codice della funzione](./media/functions-create-your-first-function-visual-studio/functions-code-page.png)

Ora che è stata creata una funzione attivata tramite HTTP, si può testare la funzione nel computer locale.

## <a name="test-hello-function-locally"></a>Funzione hello di test in locale

Azure Functions Core Tools consente di eseguire il progetto Funzioni di Azure nel computer di sviluppo locale. Si è richiesta tooinstall questi strumenti hello primo avvio di una funzione da Visual Studio.  

1. tootest della funzione, premere F5. Se richiesto, accettare la richiesta di hello da toodownload di Visual Studio e installare gli strumenti di Azure funzioni Core (CLI).  È necessario anche tooenable un'eccezione del firewall in modo che gli strumenti di hello possono gestire le richieste HTTP.

2. Copia URL hello della funzione di runtime di Azure funzioni hello di output.  

    ![Runtime locale di Azure](./media/functions-create-your-first-function-visual-studio/functions-vstools-f5.png)

3. Incollare l'URL di hello per richiesta HTTP hello nella barra degli indirizzi del browser. Aggiungere la stringa di query hello `&name=<yourname>` toothis URL ed eseguire la richiesta hello. Hello seguente risposta hello in hello browser toohello locale richiesta GET restituito dalla funzione hello: 

    ![Risposta della funzione localhost nel browser hello](./media/functions-create-your-first-function-visual-studio/functions-test-local-browser.png)

4. toostop debug, fare clic su hello **arrestare** sulla barra degli strumenti di Visual Studio hello.

Dopo aver verificato che la funzione hello venga eseguita correttamente nel computer locale, è ora toopublish hello progetto tooAzure.

## <a name="publish-hello-project-tooazure"></a>Pubblicare hello progetto tooAzure

Per poter pubblicare il progetto, è necessario che la sottoscrizione di Azure includa un'app per le funzioni. È possibile creare un'app per le funzioni direttamente da Visual Studio.

[!INCLUDE [Publish hello project tooAzure](../../includes/functions-vstools-publish.md)]

## <a name="test-your-function-in-azure"></a>Testare la funzione in Azure

1. Copiare l'URL di base dell'app di funzione hello hello dalla pagina del profilo di pubblicazione hello. Sostituire hello `localhost:port` parte dell'URL di hello è utilizzata per la verifica di funzione hello in locale con hello nuovo URL di base. Come in precedenza, verificare che stringa di query hello tooappend `&name=<yourname>` toothis URL ed eseguire la richiesta hello.

    URL di Hello che chiama HTTP attivato funzione ha un aspetto simile al seguente:

        http://<functionappname>.azurewebsites.net/api/<functionname>?name=<yourname> 

2. Incollare questo nuovo URL per la richiesta HTTP hello nella barra degli indirizzi del browser. Hello seguente risposta hello in hello browser toohello remoto richiesta GET restituito dalla funzione hello: 

    ![Risposta della funzione nel browser hello](./media/functions-create-your-first-function-visual-studio/functions-test-remote-browser.png)
 
## <a name="next-steps"></a>Passaggi successivi

È stata usata l'app di funzione toocreate c# di Visual Studio con una semplice funzione HTTP attivato. 

+ toolearn come tooconfigure toosupport il progetto altri tipi di trigger e le associazioni, vedere hello [progetto hello Configura per lo sviluppo locale](functions-develop-vs.md#configure-the-project-for-local-development) sezione [gli strumenti di funzioni di Azure per Visual Studio](functions-develop-vs.md).
+ toolearn ulteriori informazioni sui test locale e il debug con strumenti di base di hello Azure funzioni, vedere [codice e testare le funzioni di Azure localmente](functions-run-local.md). 
+ toolearn più sullo sviluppo di funzioni come librerie di classi .NET, vedere [librerie di classi .NET utilizzando con le funzioni di Azure](functions-dotnet-class-library.md). 


---
title: la prima funzione dal portale di Azure hello aaaCreate | Documenti Microsoft
description: Informazioni su come toocreate di Azure prima funzione per l'esecuzione senza tramite hello portale di Azure.
services: functions
documentationcenter: na
author: ggailey777
manager: erikre
editor: 
tags: 
ms.assetid: 96cf87b9-8db6-41a8-863a-abb828e3d06d
ms.service: functions
ms.devlang: multiple
ms.topic: quickstart
ms.tgt_pltfrm: multiple
ms.workload: na
ms.date: 08/07/2017
ms.author: glenga
ms.custom: mvc
ms.openlocfilehash: 84283d7d4bc6015061946af4589f9a70ae61f36b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="create-your-first-function-in-hello-azure-portal"></a>Creare la prima funzione in hello portale di Azure

Funzioni di Azure consente di eseguire il codice in un ambiente senza server senza dover toofirst crea una macchina virtuale o si pubblica un'applicazione web. In questo argomento, informazioni su come toouse funzioni toocreate una funzione di "hello world" nel portale di Azure hello.

![Creare app di funzione in hello portale di Azure](./media/functions-create-first-azure-function/function-app-in-portal-editor.png)

[!INCLUDE [quickstarts-free-trial-note](../../includes/quickstarts-free-trial-note.md)]

## <a name="log-in-tooazure"></a>Accedi tooAzure

Accedi toohello [portale di Azure](https://portal.azure.com/).

## <a name="create-a-function-app"></a>Creare un'app per le funzioni

È necessario disporre di un'esecuzione di hello toohost app funzione delle funzioni. Un'app per le funzioni consente di raggruppare le funzioni come un'unità logica per semplificare la gestione, la distribuzione e la condivisione delle risorse. 

[!INCLUDE [Create function app Azure portal](../../includes/functions-create-function-app-portal.md)]

[!INCLUDE [functions-portal-favorite-function-apps](../../includes/functions-portal-favorite-function-apps.md)]

Creare quindi una funzione in hello nuova funzione app.

## <a name="create-function"></a>Creare una funzione attivata tramite HTTP

1. Espandere la nuova app di funzione, quindi fare clic su hello  **+**  accanto troppo**funzioni**.

2.  In hello **iniziare rapidamente** selezionare **WebHook + API**, **scegliere una lingua** per la funzione, fare clic su **creare questa funzione** . 
   
    ![Funzioni delle Guide rapide in hello portale di Azure.](./media/functions-create-first-azure-function/function-app-quickstart-node-webhook.png)

Viene creata una funzione nella lingua scelta, utilizzando il modello di hello per una funzione di attivazione HTTP. È possibile eseguire una nuova funzione hello inviando una richiesta HTTP.

## <a name="test-hello-function"></a>Funzione hello test

1. Nella nuova funzione fare clic su **</> Recupera URL della funzione**, selezionare **predefinito (tasto funzione)** e quindi fare clic su **Copia**. 

    ![Copiare l'URL funzione hello da hello portale di Azure](./media/functions-create-first-azure-function/function-app-develop-tab-testing.png)

2. Incollare l'URL funzione hello nella barra degli indirizzi del browser. Aggiungere la stringa di query hello `&name=<yourname>` toothis URL e premere hello `Enter` chiave della richiesta di hello tooexecute tastiera. Hello Ecco un esempio di risposta hello restituito dalla funzione hello nel browser Edge hello:

    ![Risposta della funzione nel browser hello.](./media/functions-create-first-azure-function/function-app-browser-testing.png)

    richiesta di Hello URL include una chiave che è necessario, per impostazione predefinita, tooaccess la funzione su HTTP.   

3. Quando viene eseguita la funzione, le informazioni di traccia viene scritto toohello log. output di traccia toosee hello in seguito all'esecuzione precedente hello, restituire la funzione tooyour nel portale di hello e fare clic su hello freccia nella parte inferiore di hello di hello schermata tooexpand **log**. 

   ![Funzioni di accesso Visualizzatore hello portale di Azure.](./media/functions-create-first-azure-function/function-view-logs.png)

## <a name="clean-up-resources"></a>Pulire le risorse

[!INCLUDE [Clean up resources](../../includes/functions-quickstart-cleanup.md)]

## <a name="next-steps"></a>Passaggi successivi

È stata creata un'app per le funzioni con una semplice funzione attivata tramite HTTP.  

[!INCLUDE [Next steps note](../../includes/functions-quickstart-next-steps.md)]

Per altre informazioni rivedere [Binding HTTP e webhook in Funzioni di Azure](functions-bindings-http-webhook.md).




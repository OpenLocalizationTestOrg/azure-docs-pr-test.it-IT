---
title: una funzione in Azure attivata da un webhook di GitHub aaaCreate | Documenti Microsoft
description: Utilizzare le funzioni di Azure toocreate una funzione senza che viene richiamata da un webhook di GitHub.
services: functions
documentationcenter: na
author: ggailey777
manager: erikre
editor: 
tags: 
ms.assetid: 36ef34b8-3729-4940-86d2-cb8e176fcc06
ms.service: functions
ms.devlang: multiple
ms.topic: quickstart
ms.tgt_pltfrm: multiple
ms.workload: na
ms.date: 05/31/2017
ms.author: glenga
ms.custom: mvc
ms.openlocfilehash: 8ffcde82c9310d749159ed53eab113658e38a030
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-function-triggered-by-a-github-webhook"></a>Creare una funzione attivata da un webhook GitHub

Informazioni su come toocreate una funzione che viene attivata da una richiesta di webhook HTTP con un payload specifico di GitHub.

![Github Webhook è attivata nel portale di Azure hello (funzione)](./media/functions-create-github-webhook-triggered-function/function-app-in-portal-editor.png)

## <a name="prerequisites"></a>Prerequisiti

+ Un account GitHub con almeno un progetto.
+ Una sottoscrizione di Azure. Se non se ne ha una, creare un [account gratuito](https://azure.microsoft.com/free/?WT.mc_id=A261C142F) prima di iniziare.

[!INCLUDE [functions-portal-favorite-function-apps](../../includes/functions-portal-favorite-function-apps.md)]

## <a name="create-an-azure-function-app"></a>Creare un'app per le funzioni di Azure

[!INCLUDE [Create function app Azure portal](../../includes/functions-create-function-app-portal.md)]

![App per le funzioni creata correttamente.](./media/functions-create-first-azure-function/function-app-create-success.png)

Creare quindi una funzione in hello nuova funzione app.

<a name="create-function"></a>

## <a name="create-a-github-webhook-triggered-function"></a>Creare una funzione attivata da webhook GitHub

1. Espandere l'applicazione di funzione e fare clic su hello  **+**  accanto troppo**funzioni**. Se si tratta di hello prima funzione di app di funzione, selezionare **funzione personalizzata**. Consente di visualizzare il set completo di hello dei modelli di funzione.

    ![Pagina di avvio rapido di funzioni in hello portale di Azure](./media/functions-create-github-webhook-triggered-function/add-first-function.png)

2. Seleziona hello **GitHub WebHook** modello per la lingua desiderata. **Assegnare un nome alla funzione** e quindi selezionare **Crea**.

     ![Creare una funzione di webhook attivato GitHub in hello portale di Azure](./media/functions-create-github-webhook-triggered-function/functions-create-github-webhook-trigger.png) 

3. Nella nuova funzione, fare clic su **<> / Get funzione URL**, quindi copiare e salvare i valori hello. Hello stessa operazione per **<> / GitHub ottenere segreto**. Utilizzare queste webhook hello tooconfigure di valori in GitHub.

    ![Esaminare il codice di funzione hello](./media/functions-create-github-webhook-triggered-function/functions-copy-function-url-github-secret.png)

Viene successivamente creato un webhook nel repository GitHub.

## <a name="configure-hello-webhook"></a>Configurare hello webhook

1. In GitHub passare tooa repository che si è proprietari. È possibile usare anche qualsiasi repository biforcato. Se è necessario un repository toofork, utilizzare <https://github.com/Azure-Samples/functions-quickstart>.

1. Fare clic su **Impostazioni**, quindi su **Webhook** e infine su **Aggiungi webhook**.

    ![Aggiungere un webhook di GitHub](./media/functions-create-github-webhook-triggered-function/functions-create-new-github-webhook-2.png)

1. Utilizzare le impostazioni come specificato nella tabella hello, quindi fare clic su **aggiungere webhook**.

    ![Impostare l'URL del webhook hello e il segreto](./media/functions-create-github-webhook-triggered-function/functions-create-new-github-webhook-3.png)

| Impostazione | Valore consigliato | Descrizione |
|---|---|---|
| **Payload URL** (URL payload) | Valore copiato | Utilizzare il valore di hello restituito da **<> / Get funzione URL**. |
| **Segreto**   | Valore copiato | Utilizzare il valore di hello restituito da **<> / GitHub ottenere segreto**. |
| **Tipo contenuto** | application/json | funzione Hello prevede un payload JSON. |
| Trigger di evento | Selezione di singoli eventi | Vogliamo solo tootrigger sugli eventi di commento problema.  |
| | Commento al problema |  |

A questo punto, hello webhook è la funzione tootrigger configurata quando viene aggiunto un nuovo commento problema.

## <a name="test-hello-function"></a>Funzione hello test

1. Nel repository GitHub, aprire hello **problemi** scheda in una nuova finestra del browser.

1. In nuova finestra hello, fare clic su **nuovo problema**, digitare un titolo e quindi fare clic su **inviare di nuovo problema**.

1. Problema di hello, digitare un commento e fare clic su **commento**.

    ![Aggiungere un commento al problema GitHub.](./media/functions-create-github-webhook-triggered-function/functions-github-webhook-add-comment.png)

1. Tornare indietro toohello portale e visualizzare i registri di hello. Verrà visualizzata una voce di traccia con nuovo testo del commento hello.

     ![Visualizza il testo del commento hello nei registri hello.](./media/functions-create-github-webhook-triggered-function/function-app-view-logs.png)

## <a name="clean-up-resources"></a>Pulire le risorse

[!INCLUDE [Next steps note](../../includes/functions-quickstart-cleanup.md)]

## <a name="next-steps"></a>Passaggi successivi

È stata creata una funzione che viene eseguita quando viene ricevuta una richiesta da un webhook GitHub.

[!INCLUDE [Next steps note](../../includes/functions-quickstart-next-steps.md)]

Per altre informazioni sui trigger webhook, vedere [Associazioni HTTP e webhook in Funzioni di Azure](functions-bindings-http-webhook.md).

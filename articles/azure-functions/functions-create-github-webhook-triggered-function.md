---
title: Creare una funzione in Azure attivata da un webhook GitHub | Microsoft Docs
description: Usare Funzioni di Azure per creare una funzione senza server che viene richiamata da un webhook GitHub.
services: functions
documentationcenter: na
author: ggailey777
manager: cfowler
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
ms.openlocfilehash: cdfb5db7b304a18d6945328abc0ca7ebf2f9ec6a
ms.sourcegitcommit: fa28ca091317eba4e55cef17766e72475bdd4c96
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 12/14/2017
---
# <a name="create-a-function-triggered-by-a-github-webhook"></a>Creare una funzione attivata da un webhook GitHub

Informazioni su come creare una funzione attivata da una richiesta di webhook HTTP con un payload specifico di GitHub.

![Funzione attivata da un webhook GitHub nel portale di Azure](./media/functions-create-github-webhook-triggered-function/function-app-in-portal-editor.png)

## <a name="prerequisites"></a>Prerequisiti

+ Un account GitHub con almeno un progetto.
+ Una sottoscrizione di Azure. Se non se ne ha una, creare un [account gratuito](https://azure.microsoft.com/free/?WT.mc_id=A261C142F) prima di iniziare.

[!INCLUDE [functions-portal-favorite-function-apps](../../includes/functions-portal-favorite-function-apps.md)]

## <a name="create-an-azure-function-app"></a>Creare un'app per le funzioni di Azure

[!INCLUDE [Create function app Azure portal](../../includes/functions-create-function-app-portal.md)]

![App per le funzioni creata correttamente.](./media/functions-create-first-azure-function/function-app-create-success.png)

Si creerà ora una funzione nella nuova app per le funzioni.

<a name="create-function"></a>

## <a name="create-a-github-webhook-triggered-function"></a>Creare una funzione attivata da webhook GitHub

1. Espandere l'app per le funzioni e fare clic sul pulsante **+** accanto a **Funzioni**. Se questa è la prima funzione nell'app per le funzioni, selezionare **Funzione personalizzata**. Verrà visualizzato il set completo di modelli di funzione.

    ![Pagina della guida introduttiva di Funzioni nel portale di Azure](./media/functions-create-github-webhook-triggered-function/add-first-function.png)

2. Nel campo di ricerca digitare `github` e quindi scegliere la lingua da usare per il modello di attivazione del webhook GitHub. 

     ![Scegliere il modello di attivazione del webhook GitHub](./media/functions-create-github-webhook-triggered-function/functions-create-github-webhook-trigger.png) 

2. Digitare un **Nome** per la funzione e quindi selezionare **Crea**. 

     ![Configurare la funzione attivata da webhook GitHub nel portale di Azure](./media/functions-create-github-webhook-triggered-function/functions-create-github-webhook-trigger-2.png) 

3. Nella nuova funzione fare clic su **</> Get function URL** (Ottieni URL funzione) e quindi copiare e salvare i valori. Eseguire la stessa operazione per **</> Recupera segreto GitHub**. Questi valori servono per configurare il webhook in GitHub.

    ![Esaminare il codice funzione](./media/functions-create-github-webhook-triggered-function/functions-copy-function-url-github-secret.png)

Viene successivamente creato un webhook nel repository GitHub.

## <a name="configure-the-webhook"></a>Configurare il webhook

1. In GitHub passare a un repository di cui si è proprietari. È possibile usare anche qualsiasi repository biforcato. Se è necessario creare una copia tramite fork di un repository, usare <https://github.com/Azure-Samples/functions-quickstart>.

1. Fare clic su **Impostazioni**, quindi su **Webhook** e infine su **Aggiungi webhook**.

    ![Aggiungere un webhook di GitHub](./media/functions-create-github-webhook-triggered-function/functions-create-new-github-webhook-2.png)

1. Usare le impostazioni come indicato nella tabella e quindi fare clic su **Add webhook** (Aggiungi webhook).

    ![Impostare l'URL del webhook e il segreto](./media/functions-create-github-webhook-triggered-function/functions-create-new-github-webhook-3.png)

| Impostazione | Valore consigliato | Descrizione |
|---|---|---|
| **Payload URL** (URL payload) | Valore copiato | Usare il valore restituito da **</> Get function URL** (Ottieni URL funzione). |
| **Segreto**   | Valore copiato | Usare il valore restituito da **</> Get GitHub secret** (Ottieni segreto GitHub). |
| **Tipo contenuto** | application/json | La funzione prevede un payload JSON. |
| Trigger di evento | Selezione di singoli eventi | Attivazione solo in caso di eventi di commento al problema.  |
| | Commento al problema |  |

Il webhook ora è configurato per attivare la funzione quando un nuovo commento al problema viene aggiunto.

## <a name="test-the-function"></a>Testare la funzione

1. Nel repository GitHub aprire la scheda **Issues** (Problemi) in una nuova finestra del browser.

1. Nella nuova finestra fare clic su **Nuovo problema**, digitare un titolo e quindi fare clic su **Submit new issue** (Invia nuovo problema).

1. Nel problema, digitare un commento e fare clic su **Comment (Commento)**.

    ![Aggiungere un commento al problema GitHub.](./media/functions-create-github-webhook-triggered-function/functions-github-webhook-add-comment.png)

1. Tornare al portale e visualizzare i log. Verrà visualizzata una voce di traccia con il nuovo testo del commento.

     ![Visualizzare il testo del commento nei log.](./media/functions-create-github-webhook-triggered-function/function-app-view-logs.png)

## <a name="clean-up-resources"></a>Pulire le risorse

[!INCLUDE [Next steps note](../../includes/functions-quickstart-cleanup.md)]

## <a name="next-steps"></a>Passaggi successivi

È stata creata una funzione che viene eseguita quando viene ricevuta una richiesta da un webhook GitHub.

[!INCLUDE [Next steps note](../../includes/functions-quickstart-next-steps.md)]

Per altre informazioni sui trigger webhook, vedere [Associazioni HTTP e webhook in Funzioni di Azure](functions-bindings-http-webhook.md).

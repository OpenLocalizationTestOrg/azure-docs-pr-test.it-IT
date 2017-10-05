---
title: Creare una funzione che viene eseguita in una pianificazione | Microsoft Docs
description: Informazioni su come creare una funzione in Azure eseguita in base a una pianificazione definita.
services: functions
documentationcenter: na
author: ggailey777
manager: erikre
editor: 
tags: 
ms.assetid: ba50ee47-58e0-4972-b67b-828f2dc48701
ms.service: functions
ms.devlang: multiple
ms.topic: quickstart
ms.tgt_pltfrm: multiple
ms.workload: na
ms.date: 05/31/2017
ms.author: glenga
ms.custom: mvc
ms.openlocfilehash: 03cc5e71e8eb20002cf58e713fc0fc92a9129874
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/29/2017
---
# <a name="create-a-function-in-azure-that-is-triggered-by-a-timer"></a>Creare una funzione in Azure attivata da un timer

Informazioni su come usare Funzioni di Azure per creare una funzione eseguita in base a una pianificazione definita.

![Creare un'app per le funzioni nel portale di Azure](./media/functions-create-scheduled-function/function-app-in-portal-editor.png)

## <a name="prerequisites"></a>Prerequisiti

Per completare questa esercitazione:

+ Se non si ha una sottoscrizione di Azure, creare un [account gratuito](https://azure.microsoft.com/free/?WT.mc_id=A261C142F) prima di iniziare.

[!INCLUDE [functions-portal-favorite-function-apps](../../includes/functions-portal-favorite-function-apps.md)]

## <a name="create-an-azure-function-app"></a>Creare un'app per le funzioni di Azure

[!INCLUDE [Create function app Azure portal](../../includes/functions-create-function-app-portal.md)]

![App per le funzioni creata correttamente.](./media/functions-create-first-azure-function/function-app-create-success.png)

Si creerà ora una funzione nella nuova app per le funzioni.

<a name="create-function"></a>

## <a name="create-a-timer-triggered-function"></a>Creare una funzione attivata da un timer

1. Espandere l'app per le funzioni e fare clic sul pulsante **+** accanto a **Funzioni**. Se questa è la prima funzione nell'app per le funzioni, selezionare **Funzione personalizzata**. Verrà visualizzato il set completo di modelli di funzione.

    ![Pagina della guida introduttiva di Funzioni nel portale di Azure](./media/functions-create-scheduled-function/add-first-function.png)

2. Selezionare il modello **TimerTrigger** per la lingua desiderata. Usare quindi le impostazioni specificate nella tabella:

    ![Creare una funzione attivata da un timer nel portale di Azure.](./media/functions-create-scheduled-function/functions-create-timer-trigger.png)

    | Impostazione | Valore consigliato | Descrizione |
    |---|---|---|
    | **Dare un nome alla funzione** | TimerTriggerCSharp1 | Definisce il nome della funzione attivata dal timer. |
    | **[Pianificazione](http://en.wikipedia.org/wiki/Cron#CRON_expression)** | 0 \*/1 \* \* \* \* | [Espressione CRON](http://en.wikipedia.org/wiki/Cron#CRON_expression) a sei campi che pianifica la funzione in modo che venga eseguita ogni minuto. |

2. Fare clic su **Crea**. Viene creata una funzione nel linguaggio scelto che verrà eseguita ogni minuto.

3. Verificare l'esecuzione visualizzando le informazioni di traccia scritte nei log.

    ![Visualizzatore log di Funzioni nel portale di Azure.](./media/functions-create-scheduled-function/functions-timer-trigger-view-logs2.png)

È possibile ora modificare la pianificazione della funzione in modo che venga eseguita con meno frequenza, ad esempio ogni ora. 

## <a name="update-the-timer-schedule"></a>Aggiornare la pianificazione del timer

1. Espandere la funzione e fare clic su **Integrazione**. È a questo punto che si definiscono i binding di input e di output e si imposta la pianificazione. 

2. Nel campo **Pianificazione** immettere il nuovo valore `0 0 */1 * * *` e quindi fare clic su **Salva**.  

![Pianificazione del timer di aggiornamento di Funzioni nel portale di Azure.](./media/functions-create-scheduled-function/functions-timer-trigger-change-schedule.png)

È ora disponibile una funzione che viene eseguita ogni ora. 

## <a name="clean-up-resources"></a>Pulire le risorse

[!INCLUDE [Next steps note](../../includes/functions-quickstart-cleanup.md)]

## <a name="next-steps"></a>Passaggi successivi

È stata creata una funzione eseguita in base a una pianificazione.

[!INCLUDE [Next steps note](../../includes/functions-quickstart-next-steps.md)]

Per altre informazioni sui trigger timer, vedere [Pianificare l'esecuzione di codice con Funzioni di Azure](functions-bindings-timer.md).
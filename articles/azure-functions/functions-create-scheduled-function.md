---
title: una funzione che viene eseguito in una pianificazione in Azure aaaCreate | Documenti Microsoft
description: Informazioni su come toocreate in Azure che esegue una funzione basato su una pianificazione definita.
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
ms.openlocfilehash: 793b06a65a154466dfd4c121bcc88082227cd597
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-function-in-azure-that-is-triggered-by-a-timer"></a>Creare una funzione in Azure attivata da un timer

Informazioni su come toouse Azure funzioni toocreate una funzione che viene eseguito in base una pianificazione definita.

![Creare app di funzione in hello portale di Azure](./media/functions-create-scheduled-function/function-app-in-portal-editor.png)

## <a name="prerequisites"></a>Prerequisiti

toocomplete questa esercitazione:

+ Se non si ha una sottoscrizione di Azure, creare un [account gratuito](https://azure.microsoft.com/free/?WT.mc_id=A261C142F) prima di iniziare.

[!INCLUDE [functions-portal-favorite-function-apps](../../includes/functions-portal-favorite-function-apps.md)]

## <a name="create-an-azure-function-app"></a>Creare un'app per le funzioni di Azure

[!INCLUDE [Create function app Azure portal](../../includes/functions-create-function-app-portal.md)]

![App per le funzioni creata correttamente.](./media/functions-create-first-azure-function/function-app-create-success.png)

Creare quindi una funzione in hello nuova funzione app.

<a name="create-function"></a>

## <a name="create-a-timer-triggered-function"></a>Creare una funzione attivata da un timer

1. Espandere l'applicazione di funzione e fare clic su hello  **+**  accanto troppo**funzioni**. Se si tratta di hello prima funzione di app di funzione, selezionare **funzione personalizzata**. Consente di visualizzare il set completo di hello dei modelli di funzione.

    ![Pagina di avvio rapido di funzioni in hello portale di Azure](./media/functions-create-scheduled-function/add-first-function.png)

2. Seleziona hello **TimerTrigger** modello per la lingua desiderata. Utilizzare quindi le impostazioni di hello come specificato nella tabella hello:

    ![Creare una funzione di timer attivato in hello portale di Azure.](./media/functions-create-scheduled-function/functions-create-timer-trigger.png)

    | Impostazione | Valore consigliato | Descrizione |
    |---|---|---|
    | **Dare un nome alla funzione** | TimerTriggerCSharp1 | Definisce il nome di hello della funzione di timer attivato. |
    | **[Pianificazione](http://en.wikipedia.org/wiki/Cron#CRON_expression)** | 0 \*/1 \* \* \* \* | Un campo sei [espressione CRON](http://en.wikipedia.org/wiki/Cron#CRON_expression) toorun la funzione che pianifica ogni minuto. |

2. Fare clic su **Crea**. Viene creata una funzione nel linguaggio scelto che verrà eseguita ogni minuto.

3. Verificare l'esecuzione visualizzando le informazioni di traccia toohello log scritte.

    ![Funzioni di accesso Visualizzatore hello portale di Azure.](./media/functions-create-scheduled-function/functions-timer-trigger-view-logs2.png)

A questo punto, è possibile modificare la pianificazione della funzione hello in modo che venga eseguito meno frequentemente, ad esempio una volta ogni ora. 

## <a name="update-hello-timer-schedule"></a>Pianificazione di aggiornamento hello timer

1. Espandere la funzione e fare clic su **Integrazione**. Questo è possibile definire l'input e output associazioni per la funzione e inoltre impostare la pianificazione hello. 

2. Nel campo **Pianificazione** immettere il nuovo valore `0 0 */1 * * *` e quindi fare clic su **Salva**.  

![Funzioni di aggiornare la pianificazione di timer in hello portale di Azure.](./media/functions-create-scheduled-function/functions-timer-trigger-change-schedule.png)

È ora disponibile una funzione che viene eseguita ogni ora. 

## <a name="clean-up-resources"></a>Pulire le risorse

[!INCLUDE [Next steps note](../../includes/functions-quickstart-cleanup.md)]

## <a name="next-steps"></a>Passaggi successivi

È stata creata una funzione eseguita in base a una pianificazione.

[!INCLUDE [Next steps note](../../includes/functions-quickstart-next-steps.md)]

Per altre informazioni sui trigger timer, vedere [Pianificare l'esecuzione di codice con Funzioni di Azure](functions-bindings-timer.md).
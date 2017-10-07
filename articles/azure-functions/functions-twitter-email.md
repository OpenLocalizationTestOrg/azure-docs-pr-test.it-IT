---
title: una funzione che si integra con Azure logica App aaaCreate | Documenti Microsoft
description: "Creare una funzione che si integra con Azure logica App e servizi di Azure cognitivi sentiment tweet toocategorize e inviare notifiche quando sentiment è scarsa."
services: functions, logic-apps, cognitive-services
keywords: flusso di lavoro, app cloud, servizi cloud, processi aziendali, integrazione di sistemi, enterprise application integration, EAI
documentationcenter: 
author: ggailey777
manager: erikre
editor: 
ms.assetid: 60495cc5-1638-4bf0-8174-52786d227734
ms.service: functions
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/15/2017
ms.author: glenga
ms.custom: mvc
ms.openlocfilehash: e176bd946af9a3684b3ad0e4b1bed1c3ee344019
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-function-that-integrates-with-azure-logic-apps"></a>Creare una funzione che si integra con le app per la logica di Azure

Funzioni di Azure si integra con Azure logica App in hello logica di progettazione di App. Questa integrazione consente di usare hello elaborazione delle funzioni in orchestrazioni con altri servizi di terze parti e di Azure. 

Questa esercitazione viene illustrato il funzionamento toouse con logica App e servizi di Azure cognitivi sentiment tooanalyze da Twitter post. Una funzione di attivazione HTTP classifica TWEET come verde, giallo o rosso basato sul punteggio sentiment hello. Quando viene rilevato un livello di sentiment basso viene inviato un messaggio di posta elettronica. 

![immagine dei primi due passaggi dell'app in Progettazione app per la logica](media/functions-twitter-email/designer1.png)

In questa esercitazione si apprenderà come:

> [!div class="checklist"]
> * Creare un account di Servizi cognitivi.
> * Creare una funzione che classifica i sentiment nei tweet.
> * Creare un'app di logica che si connette tooTwitter.
> * Aggiungere app per la logica toohello sentiment rilevamento. 
> * Hello logica app toohello funzione di connessione.
> * Inviare un messaggio di posta elettronica in base alla risposta hello dalla funzione hello.

## <a name="prerequisites"></a>Prerequisiti

+ Un account [Twitter](https://twitter.com/) attivo. 
+ Un account [Outlook.com](https://outlook.com/) per l'invio delle notifiche.
+ Questo argomento viene utilizzato come le risorse di hello punto iniziale create in [creare la prima funzione dal portale di Azure hello](functions-create-first-azure-function.md).  
Se non già stato fatto, completare questi toocreate ora i passaggi dell'app di funzione.

## <a name="create-a-cognitive-services-account"></a>Creare un account Servizi cognitivi

Un account di servizi cognitivi è obbligatorio toodetect hello sentiment di tweet monitorato.

1. Accedi toohello [portale di Azure](https://portal.azure.com/).

2. Fare clic su hello **New** pulsante disponibile nella hello angolo superiore sinistro del portale di Azure hello.

3. Fare clic su **Dati e analisi** > **Servizi cognitivi**. Quindi, utilizza le impostazioni di hello come specificato nella tabella di hello, accettare le condizioni di hello e controllare **toodashboard Pin**.

    ![Pannello Creare account Servizi cognitivi](media/functions-twitter-email/cog_svcs_account.png)

    | Impostazione      |  Valore consigliato   | Descrizione                                        |
    | --- | --- | --- |
    | **Nome** | MyCognitiveServicesAccnt | Scegliere un nome dell'account univoco. |
    | **Tipo di API** | API Analisi del testo | L'API utilizzata tooanalyze testo.  |
    | **Posizione** | Stati Uniti occidentali | Attualmente, per l'analisi è disponibile solo **Stati Uniti occidentali**. |
    | **Piano tariffario** | F0 | Iniziare con il livello più basso di hello. Se si esauriscono le chiamate, applicare la scalabilità tooa di livello superiore.|
    | **Gruppo di risorse** | myResourceGroup | Utilizzare hello stesso gruppo di risorse per tutti i servizi in questa esercitazione.|

4. Fare clic su **crea** toocreate l'account. Dopo aver creato l'account di hello, fare clic su nuovo dashboard toohello aggiunti account servizi cognitivi. 

5. Nell'account hello, fare clic su **chiavi**e quindi copiare il valore di hello di **tasto 1** e salvarlo. Utilizzare questo tooyour di app logica hello tooconnect chiave account di servizi cognitivi. 
 
    ![Chiavi](media/functions-twitter-email/keys.png)

## <a name="create-hello-function"></a>Creare la funzione hello

Funzioni include le attività di elaborazione in un flusso di lavoro logica App toooffload un ottimo modo. Questa esercitazione viene utilizzato un punteggi HTTP attivato funzione tooprocess tweet sentiment da servizi cognitivi e restituire un valore di categoria.  

1. Espandere l'applicazione di funzione, fare clic su hello  **+**  accanto troppo**funzioni**, fare clic su hello **HTTPTrigger** modello. Tipo `CategorizeSentiment` per la funzione hello **nome** e fare clic su **crea**.

    ![Pannello App per le funzioni, Funzioni +](media/functions-twitter-email/add_fun.png)

2. Sostituire il contenuto di hello del file run.csx hello con hello seguente di codice, quindi fare clic su **salvare**:

    ```c#
    using System.Net;
    
    public static async Task<HttpResponseMessage> Run(HttpRequestMessage req, TraceWriter log)
    {
        // hello sentiment category defaults too'GREEN'. 
        string category = "GREEN";
    
        // Get hello sentiment score from hello request body.
        double score = await req.Content.ReadAsAsync<double>();
        log.Info(string.Format("hello sentiment score received is '{0}'.",
                    score.ToString()));
    
        // Set hello category based on hello sentiment score.
        if (score < .3)
        {
            category = "RED";
        }
        else if (score < .6)
        {
            category = "YELLOW";
        }
        return req.CreateResponse(HttpStatusCode.OK, category);
    }
    ```
    Questo codice di funzione restituisce una categoria di colore basata sul punteggio sentiment hello ricevuti nella richiesta di hello. 

3. funzione hello tootest, fare clic su **Test** scheda Test hello di hello tooexpand estrema destra. Digitare un valore di `0.2` per hello **corpo della richiesta**, quindi fare clic su **eseguire**. Il valore **rosso** viene restituito nel corpo di hello della risposta hello. 

    ![Testare la funzione hello in hello portale di Azure](./media/functions-twitter-email/test.png)

A questo punto è disponibile una funzione che classifica i punteggi dei sentiment. Nella fase successiva viene creata un'app per la logica che integra la funzione con gli account Twitter e Servizi cognitivi. 

## <a name="create-a-logic-app"></a>Creare un'app per la logica   

1. In hello portale di Azure, fare clic su hello **New** pulsante disponibile nella hello angolo superiore sinistro del portale di Azure hello.

2. Fare clic su **Integrazione aziendale** > **App per la logica**. Quindi, utilizza le impostazioni di hello come specificato nella tabella di hello, controllare **Pin toodashboard**, fare clic su **crea**.
 
4. Digitare quindi un **nome** come `TweetSentiment`, utilizzare le impostazioni di hello come specificato nella tabella hello, accettare le condizioni di hello e controllare **toodashboard Pin**.

    ![Creare app per la logica in hello portale di Azure](./media/functions-twitter-email/new_logicApp.png)

    | Impostazione      |  Valore consigliato   | Descrizione                                        |
    | ----------------- | ------------ | ------------- |
    | **Nome** | TweetSentiment | Scegliere un nome appropriato per l'app. |
    | **Gruppo di risorse** | myResourceGroup | L'API utilizzata tooanalyze testo.  |
    | **Posizione** | Stati Uniti Orientali | Scegliere un tooyou Chiudi percorso. |
    | **Gruppo di risorse** | myResourceGroup | Scegliere hello stesso gruppo di risorse esistente come prima.|

4. Fare clic su **crea** toocreate app logica. Dopo aver creato l'applicazione hello, fare clic su nuovo dashboard aggiunti toohello logica app. Nella finestra di progettazione logica App hello, scorrere verso il basso, quindi fare clic su hello **App vuota per la logica** modello. 

    ![Modello App per la logica vuota](media/functions-twitter-email/blank.png)

È ora possibile utilizzare hello logica App tooadd servizi e i trigger tooyour app Designer.

## <a name="connect-tootwitter"></a>Connettersi tooTwitter

Innanzitutto, creare un account Twitter di tooyour connessione. Hello logica app esegue il polling di tweet, che attivano toorun app hello.

1. Nella finestra di progettazione hello, fare clic su hello **Twitter** del servizio e fare clic su hello **durante il postback un tweet nuovo** trigger. Accedi tooyour account Twitter e autorizzare la logica App toouse l'account.

2. Utilizzare le impostazioni di trigger di hello Twitter come specificato nella tabella hello. 

    ![Impostazioni del connettore Twitter](media/functions-twitter-email/azure_tweet.png)

    | Impostazione      |  Valore consigliato   | Descrizione                                        |
    | ----------------- | ------------ | ------------- |
    | **Testo di ricerca** | #Azure | Utilizzare un hashtag che è abbastanza comune per toogenerate nuovo TWEET nell'intervallo di hello scelto. Quando si utilizza livello gratuito hello e il hashtag è troppo comune, è possibile utilizzare le transazioni hello rapidamente nell'account di servizi cognitivi. |
    | **Frequenza** | Minuto | unità di frequenza Hello utilizzato per il polling di Twitter.  |
    | **Interval** | 15 | tempo di Hello trascorso tra le richieste a Twitter, in unità di frequenza. |

3.  Fare clic su **salvare** tooconnect tooyour account Twitter. 

A questo punto l'app tooTwitter connesso. Connettersi quindi sentiment di tootext analitica toodetect hello di tweet raccolti.

## <a name="add-sentiment-detection"></a>Aggiungere il rilevamento dei sentiment

1. Selezionare **Nuovo passaggio** e quindi **Aggiungi un'azione**.

    ![Nuovo passaggio e quindi Aggiungi un'azione.](media/functions-twitter-email/new_step.png)

2. In **scegliere un'azione**, fare clic su **testo Analitica**, quindi fare clic su hello **rilevare sentiment** azione.

    ![Rileva sentiment](media/functions-twitter-email/detect_sent.png)

3. Digitare un nome di connessione, ad esempio `MyCognitiveServicesConnection`, incollare la chiave hello per i servizi cognitivi account salvato e fare clic su **crea**.  

4. Fare clic su **testo tooanalyze** > **Tweet testo**, quindi fare clic su **salvare**.  

    ![Rileva sentiment](media/functions-twitter-email/ds_tta.png)

Dopo avere configurato il rilevamento di valutazione, è possibile aggiungere una funzione tooyour di connessione che utilizza l'output di hello sentiment punteggio.

## <a name="connect-sentiment-output-tooyour-function"></a>Sentiment output tooyour funzione di connessione

1. Nella finestra di progettazione logica App hello, fare clic su **nuovo passaggio** > **aggiungere un'azione**e quindi fare clic su **Azure funzioni**. 

2. Fare clic su **scegliere una funzione di Azure**selezionare hello **CategorizeSentiment** funzione creata in precedenza.  

    ![Casella Funzione Azure con Scegliere una funzione di Azure](media/functions-twitter-email/choose_fun.png)

3. In **Corpo della richiesta** fare clic su **Punteggio** e quindi su **Salva**.

    ![Score](media/functions-twitter-email/trigger_score.png)

A questo punto, la funzione viene attivata quando viene inviato un punteggio sentiment da hello logica app. Una categoria con codifica a colori viene restituita toohello logica app dalla funzione hello. Aggiungere quindi una notifica di posta elettronica viene inviata quando il valore sentiment **rosso** restituiti dalla funzione hello. 

## <a name="add-email-notifications"></a>Aggiungere le notifiche di posta elettronica

ultima parte di Hello del flusso di lavoro hello è tootrigger un messaggio di posta elettronica quando viene calcolato il punteggio sentiment hello come _rosso_. Questo argomento fa uso di un connettore Outlook.com. È possibile eseguire simile passaggi toouse un connettore Gmail o Outlook di Office 365.   

1. Nella finestra di progettazione logica App hello, fare clic su **nuovo passaggio** > **aggiungere una condizione**. 

2. Fare clic su **Scegliere un valore** e quindi su **Corpo**. Selezionare **è uguale a**, fare clic su **Scegliere un valore**, digitare `RED` e quindi fare clic su **Salva**. 

    ![Aggiungi condizione toohello logica app.](media/functions-twitter-email/condition.png)

3. In **in caso AFFERMATIVO, non eseguire alcuna operazione**, fare clic su **aggiungere un'azione**, cercare `outlook.com`, fare clic su **invia un messaggio di posta elettronica**ed eseguire l'accesso tooyour account Outlook.com.
    
    ![Scegliere un'azione per la condizione hello.](media/functions-twitter-email/outlook.png)

    > [!NOTE]
    > Se non è disponibile un account Outlook.com, è possibile scegliere un altro connettore, ad esempio Gmail o Office 365 Outlook.

4. In hello **invia un messaggio di posta elettronica** azione, utilizza le impostazioni di posta elettronica hello come specificato nella tabella hello. 

    ![Configurare la posta elettronica hello per l'invio di hello un'azione di posta elettronica.](media/functions-twitter-email/sendemail.png)

    | Impostazione      |  Valore consigliato   | Descrizione  |
    | ----------------- | ------------ | ------------- |
    | **To** | Digitare l'indirizzo di posta elettronica | indirizzo di posta elettronica Hello che riceve la notifica di hello. |
    | **Oggetto** | Rilevato sentiment di tweet negativo  | riga dell'oggetto Hello di notifica tramite posta elettronica hello.  |
    | **Corpo** | Testo tweet, Località | Fare clic su hello **Tweet testo** e **percorso** parametri. |

5.  Fare clic su **Salva**.

Ora che hello è completato, è possibile abilitare hello logica app e vedere la funzione hello al lavoro.

## <a name="test-hello-workflow"></a>Flusso di lavoro di test hello

1. Nella finestra di progettazione logica App hello, fare clic su **eseguire** toostart hello app.

2. Nella colonna sinistra hello, fare clic su **Panoramica** stato hello toosee di hello logica app. 
 
    ![Stato di esecuzione dell'app per la logica](media/functions-twitter-email/over1.png)

3. (Facoltativo) Fare clic su uno di hello esecuzioni toosee dettagli di esecuzione hello.

4. Funzione tooyour mano, visualizzare i log di hello e verificare che i valori di valutazione ricevuti ed elaborati.
 
    ![Visualizzare i log della funzione](media/functions-twitter-email/sent.png)

5. Quando viene rilevato un sentiment potenzialmente negativo, si riceve un messaggio di posta elettronica. Se non si è ricevuto un messaggio di posta elettronica, è possibile modificare ogni volta hello funzione codice tooreturn rosso:

        return req.CreateResponse(HttpStatusCode.OK, "RED");

    Dopo aver verificato le notifiche di posta elettronica, modificare il codice originale toohello indietro:

        return req.CreateResponse(HttpStatusCode.OK, category);

    > [!IMPORTANT]
    > Dopo aver completato questa esercitazione, è consigliabile disabilitare hello logica app. Disabilitando l'applicazione hello evitare di essere addebitati per le esecuzioni e utilizzare le transazioni hello nell'account di servizi cognitivi.

Ora è stato illustrato come è facile toointegrate funzioni in un flusso di lavoro App per la logica.

## <a name="disable-hello-logic-app"></a>Disabilitare hello logica app

toodisable hello logica app, fare clic su **Panoramica** e quindi fare clic su **disabilitare** in alto hello hello. Questo arresta hello app per la logica di esecuzione e gli addebiti senza eliminare l'applicazione hello. 

![Log della funzione](media/functions-twitter-email/disable-logic-app.png)

## <a name="next-steps"></a>Passaggi successivi

In questa esercitazione si è appreso come:

> [!div class="checklist"]
> * Creare un account di Servizi cognitivi.
> * Creare una funzione che classifica i sentiment nei tweet.
> * Creare un'app di logica che si connette tooTwitter.
> * Aggiungere app per la logica toohello sentiment rilevamento. 
> * Hello logica app toohello funzione di connessione.
> * Inviare un messaggio di posta elettronica in base alla risposta hello dalla funzione hello.

Spostare toolearn esercitazione successiva toohello come toocreate un'API senza server per la funzione.

> [!div class="nextstepaction"] 
> [Creare un'API senza server mediante Funzioni di Azure](functions-create-serverless-api.md)

toolearn informazioni sulle App per la logica, vedere [Azure logica app](../logic-apps/logic-apps-what-are-logic-apps.md).


---
title: aaaConfigure autenticazione e autorizzazione per un'applicazione personalizzata che chiama hello Azure ora serie Insights API | Documenti Microsoft
description: In questa esercitazione viene illustrato come tooconfigure autenticazione e autorizzazione per un'applicazione personalizzata che chiama hello Azure ora serie Insights API
keywords: 
services: time-series-insights
documentationcenter: 
author: dmdenmsft
manager: almineev
editor: cgronlun
ms.assetid: 
ms.service: time-series-insights
ms.devlang: na
ms.topic: how-to-article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 05/24/2017
ms.author: dmden
ms.openlocfilehash: 5043468bfc2af3c0d27e8602508d92ba2848409e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="authentication-and-authorization-for-azure-time-series-insights-api"></a>Autenticazione e autorizzazione per l'API Azure Time Series Insights

In questo articolo viene illustrato come un'applicazione personalizzata che chiama tooconfigure hello Azure ora serie Insights API.

## <a name="service-principal"></a>Entità servizio

Questa sezione viene illustrato come tooconfigure tooaccess un'applicazione hello ora serie Insights API per conto di un'applicazione hello. un'applicazione Hello può quindi eseguire query sui dati o pubblicare dati di riferimento nell'ambiente di tempo serie Insights hello con le credenziali dell'applicazione e non le credenziali utente hello.

Quando si dispone di un'applicazione che richiede tooaccess ora serie Insights, è necessario configurare un'applicazione Azure Active Directory e assegnare criteri di accesso ai dati hello nell'ambiente di tempo serie Insights hello. Questo approccio è preferibile toorunning hello app con le proprie credenziali perché:

* È possibile assegnare le autorizzazioni di identità app toohello che sono diverse dalle autorizzazioni personalizzate. In genere, queste autorizzazioni sono limitate tooexactly quali app hello deve toodo. Ad esempio, è possibile consentire hello app tooonly leggere i dati in un ambiente di Insights di serie di tempo specifico.
* Non si dispone delle credenziali dell'applicazione hello toochange se Modifica responsabilità dell'utente.
* Quando si esegue uno script automatico, è possibile utilizzare un certificato o l'autenticazione chiave tooautomate un'applicazione.

Questo articolo illustra come quelli passaggi tooperform hello portale di Azure. Si concentra in un'applicazione single-tenant in cui un'applicazione hello è toorun previsti in una sola organizzazione. Le applicazioni con un tenant singolo si usano in genere per applicazioni line-of-business eseguite all'interno dell'organizzazione.

flusso di programma di installazione di Hello è costituito da tre passaggi generali:

1. Creare un'applicazione in Azure Active Directory.
2. Autorizzare l'ambiente di applicazione tooaccess hello ora serie Insights.
3. Utilizzare l'ID applicazione hello e la chiave tooacquire toohello un token `"https://api.timeseries.azure.com/"` destinatario o una risorsa. token Hello può quindi essere utilizzato toocall hello ora serie Insights API.

Ecco i passaggi dettagliati hello:

1. Nel portale di Azure hello, selezionare **Azure Active Directory** > **registrazioni di App** > **nuova registrazione applicazione**.

   ![Registrazione di una nuova applicazione in Azure Active Directory](media/authentication-and-authorization/active-directory-new-application-registration.png)  

2. Assegnare un'applicazione hello toobe di tipo un nome, selezionare hello **app Web / API**, selezionare qualsiasi URI valido per **Sign-on URL**, fare clic su **crea**.

   ![Creare un'applicazione hello in Azure Active Directory](media/authentication-and-authorization/active-directory-create-web-api-application.png)

3. Selezionare l'applicazione appena creata e copiare il relativo editor di testo preferito tooyour ID applicazione.

   ![Copiare l'ID dell'applicazione hello](media/authentication-and-authorization/active-directory-copy-application-id.png)

4. Selezionare **chiavi**, immettere nome chiave hello, scadenza hello select e fare clic su **salvare**.

   ![Selezionare le chiavi dell'applicazione](media/authentication-and-authorization/active-directory-application-keys.png)

   ![Immettere nome della chiave hello e la scadenza e fare clic su Salva](media/authentication-and-authorization/active-directory-application-keys-save.png)

5. Editor di testo preferito tooyour chiave hello copia.

   ![Chiave dell'applicazione hello copia](media/authentication-and-authorization/active-directory-copy-application-key.png)

6. Per ambiente ora serie Insights hello, selezionare **i criteri di accesso dati** e fare clic su **Aggiungi**.

   ![Aggiungere nuovi dati accesso criteri toohello ora serie Insights ambiente](media/authentication-and-authorization/time-series-insights-data-access-policies-add.png)

7. In hello **Seleziona utente** la finestra di dialogo, nome dell'applicazione hello Incolla (dal passaggio 2) o ID dell'applicazione (dal passaggio 3).

   ![Trovare un'applicazione nella finestra di dialogo Seleziona utente hello](media/authentication-and-authorization/time-series-insights-data-access-policies-select-user.png)

8. Ruolo selezionare hello (**lettore** per eseguire query sui dati, **collaboratore** per eseguire query sui dati e la modifica di dati di riferimento) e fare clic su **Ok**.

   ![Selezionare lettore o collaboratore nella finestra di dialogo selezionare il ruolo di hello](media/authentication-and-authorization/time-series-insights-data-access-policies-select-role.png)

9. Salvare il criterio di hello facendo **Ok**.

10. Utilizzare l'ID dell'applicazione hello (dal passaggio 3) e token hello tooacquire chiave (dal passaggio 5) dell'applicazione per conto di un'applicazione hello. Hello token può quindi essere passato in hello `Authorization` intestazione quando l'applicazione hello chiama hello ora serie Insights API.

    Se si usa c#, è possibile utilizzare i seguenti token hello tooacquire di codice per conto di un'applicazione hello hello. Per un esempio completo, vedere [Eseguire query sui dati tramite C#](time-series-insights-query-data-csharp.md).

    ```csharp
    var authenticationContext = new AuthenticationContext(
        "https://login.microsoftonline.com/common",
        TokenCache.DefaultShared);

    AuthenticationResult token = await authenticationContext.AcquireTokenAsync(
        // Set hello resource URI toohello Azure Time Series Insights API
        resource: "https://api.timeseries.azure.com/", 
        clientCredential: new ClientCredential(
            // Application ID of application registered in Azure Active Directory
            clientId: "1bc3af48-7e2f-4845-880a-c7649a6470b8", 
            // Application key of hello application that's registered in Azure Active Directory
            clientSecret: "aBcdEffs4XYxoAXzLB1n3R2meNCYdGpIGBc2YC5D6L2="));

    string accessToken = token.AccessToken;
    ```

## <a name="next-steps"></a>Passaggi successivi

Utilizzare l'ID applicazione hello e la chiave nell'applicazione. Per esempio di codice che chiama hello ora serie Insights API, vedere [eseguire query sui dati utilizzando il linguaggio c#](time-series-insights-query-data-csharp.md).

## <a name="see-also"></a>Vedere anche

* [Le query API](/rest/api/time-series-insights/time-series-insights-reference-queryapi) per riferimento API di Query completo hello
* [Creare un servizio principale in hello portale di Azure](../azure-resource-manager/resource-group-create-service-principal-portal.md)

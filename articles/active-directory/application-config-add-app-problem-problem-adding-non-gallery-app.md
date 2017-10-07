---
title: aggiunta di un'applicazione non raccolta aaaProblem | Documenti Microsoft
description: Comprendere faccia persone problemi comuni di hello durante l'aggiunta di applicazioni non raccolta personalizzate
services: active-directory
documentationcenter: 
author: ajamess
manager: femila
ms.assetid: 
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/11/2017
ms.author: asteen
ms.openlocfilehash: cfe9b657ae18cbacaddbd85658471a2c57c9cf95
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="problem-adding-a-non-gallery-application"></a>Errore durante l'aggiunta di un'applicazione non inclusa nella raccolta

Questo articolo è utile faccia di persone di toounderstand hello comuni problemi durante l'aggiunta di **applicazioni non raccolta personalizzate** e a cosa può tooresolve li. 

## <a name="i-clicked-hello-add-button-and-my-application-took-a-long-time-tooappear"></a>Facendo clic su "Aggiungi" pulsante e l'applicazione ha richiesto un tempo tooappear hello

In alcuni casi, può richiedere 1-2 minuti (o più) per un'applicazione tooappear dopo averlo aggiunto tooyour directory. Quando non si tratta di prestazioni previsto normali hello, è possibile visualizzare l'aggiunta dell'applicazione hello è in corso facendo clic su hello **notifiche** icona (campana hello) in alto a hello destra hello [il portale di Azure](https://portal.azure.com/)e cercando un **In corso** o **completato** notifica con l'etichetta **creare applicazione**.

Se l'applicazione non viene mai aggiunto o si verifica un errore quando si fa clic hello **Aggiungi** pulsante, verrà visualizzato un **notifica** in un **errore** stato. Se si desidera visualizzare ulteriori dettagli su hello errore toolearn tooor più condividere con engingeer un supporto, è possibile visualizzare ulteriori informazioni sull'errore hello seguendo procedure hello hello [come dettagli di hello toosee di una notifica tramite il portale](#how-to-see-the-details-of-a-portal-notification) sezione.

## <a name="i-clicked-hello-add-button-and-my-application-didnt-appear"></a>Fa clic sul pulsante "Aggiungi" hello e non è presente l'applicazione

In alcuni casi, a causa di problemi di tootransient, problemi di rete o un bug, aggiunta di un errore di applicazione. È possibile indicare ciò si verifica quando si fa clic su hello **notifiche** icona (campana hello) in alto a destra hello di hello portale di Azure e vedere un rosso (!) icona Avanti tooyour **creare applicazione** notifica. Ciò indica che si è verificato un errore durante la creazione di un'applicazione hello.

Se si verifica un errore quando si fa clic hello **Aggiungi** pulsante, verrà visualizzato un **notifica** in un **errore** stato. Se si desidera visualizzare ulteriori dettagli su hello errore toolearn tooor più condividere con engingeer un supporto, è possibile visualizzare ulteriori informazioni sull'errore hello seguendo procedure hello hello [come dettagli di hello toosee di una notifica tramite il portale](#how-to-see-the-details-of-a-portal-notification) sezione.

## <a name="i-dont-know-how-tooset-up-my-application-once-ive-added-it"></a>Non so come tooset backup una volta l'applicazione è stato aggiunto

Se assistenza apprendendo ora delle applicazioni personalizzate, hello [raccolta documenti di Azure AD applicazioni](https://docs.microsoft.com/azure/active-directory/active-directory-apps-index) consentono toolearn ulteriori informazioni su single sign-on con Azure AD e il relativo funzionamento.

## <a name="how-toosee-hello-details-of-a-portal-notification"></a>Modalità dettagli hello toosee di una notifica del portale

È possibile visualizzare i dettagli di hello di qualsiasi notifica tramite il portale seguendo i passaggi di hello riportati di seguito:

1.  Fare clic su hello **notifiche** icona (campana hello) in alto a destra hello di hello portale di Azure

2.  Selezionare qualsiasi notifica in un **errore** stato (quelli con un toothem Avanti rosso (!)).

   >[!NOTE]
   >Non è possibile fare clic sulle notifiche con stato **Operazione completata** o **In corso**.
   >
   >

3.  Questo hello aprire **i dettagli sulla notifica** blade.

4.  Utilizzare queste informazioni manualmente toounderstand ulteriori dettagli sul problema hello.

5.  Se è ancora necessario della Guida, è possibile condividere queste informazioni con il problema con un supporto tecnico o hello gruppo tooget Guida del prodotto.

6.  Fare clic su hello **sull'icona Copia** toohello diritto di hello **copiare errore** toocopy textbox tutti hello tooshare dettagli di notifica con un ingegnere del supporto o il prodotto gruppo.

## <a name="how-tooget-help-by-sending-notification-details-tooa-support-engineer"></a>Informazioni tooget inviando al supporto tecnico tooa dettagli di notifica

È molto importante che si condivide **tutti hello dettagli riportati di seguito** con un supporto tecnico per assistenza, in modo che tali eventi consentono rapidamente. Tale scopo, **acquisire uno screenshot,** o facendo clic su hello **sull'icona di errore di copia**, trovato toohello destra di hello **copiare errore** casella di testo.

## <a name="notification-details-explained"></a>Spiegazione dei dettagli della notifica

Hello seguente illustra più quali tutti gli elementi hello notifica significa e fornisce esempi di ognuno di essi.

### <a name="essential-notification-items"></a>Elementi essenziali della notifica

-   **Titolo** : hello titolo descrittivo della notifica hello
   *  Esempio: **Impostazioni proxy di applicazione**

-   **Descrizione** : hello descrizione di ciò che si è verificato in seguito a operazione hello

   *  Esempio: **L'URL interno immesso è già usato da un'altra applicazione**

-   **Id di notifica** : id univoco di hello della notifica hello

   *  Esempio: **clientNotification-2adbfc06-2073-4678-a69f-7eb78d96b068**

-   **Id richiesta client** : id richiesta specifico hello apportate dal browser

   *  Esempio: **302fd775-3329-4670-a9f3-bea37004f0bc**

-   **Ora UTC timbro** : hello timestamp durante il quale la notifica hello si è verificato, in formato UTC

   *  Esempio: **2017-03-23T19:50:43.7583681Z**

-   **Id della transazione interna** : hello ID interno, è possibile utilizzare l'errore hello toolook nei nostri sistemi

   *  Esempio: **71a2f329-ca29-402f-aa72-bc00a7aca603**

-   **UPN** – utente hello che ha eseguito l'operazione di hello

   *  Esempio: **tperkins@f128.info**

-   **Id tenant** : hello ID univoco del tenant hello che hello utente che ha eseguito l'operazione di hello è un membro di

   *  Esempio: **7918d4b5-0442-4a97-be2d-36f9f9962ece**

-   **L'Id di oggetto utente** : hello ID univoco dell'utente di hello che ha eseguito l'operazione di hello

 *  Esempio: **17f84be4-51f8-483a-b533-383791227a99**

### <a name="detailed-notification-items"></a>Elementi della notifica dettagliati

-   **Nome visualizzato** – **(può essere vuoto)** un nome di visualizzazione più dettagliato per correggere l'errore hello

  *  Esempio: **Impostazioni proxy di applicazione**

-   **Stato** : hello specifico stato di notifica di hello

   *  Esempio: **Operazione non riuscita**

-   **Id di oggetto** – **(può essere vuoto)** hello ID di oggetto su cui hello è stata eseguita l'operazione

   *  Esempio: **8e08161d-f2fd-40ad-a34a-a9632d6bb599**

-   **Dettagli** : hello descrizione dettagliata dell'accaduto come risultato di operazione hello

   *  Esempio: **L'URL interno "http://bing.com/" non è valido perché è già in uso**

-   **Copiare l'errore** – fare clic su hello **sull'icona Copia** toohello diritto di hello **copiare errore** toocopy textbox tutti hello tooshare dettagli di notifica con un ingegnere del supporto o il prodotto gruppo

   *  Esempio```{"errorCode":"InternalUrl\_Duplicate","localizedErrorDetails":{"errorDetail":"Internal url 'http://google.com/' is invalid since it is already in use"},"operationResults":\[{"objectId":null,"displayName":null,"status":0,"details":"Internal url 'http://bing.com/' is invalid since it is already in use"}\],"timeStampUtc":"2017-03-23T19:50:26.465743Z","clientRequestId":"302fd775-3329-4670-a9f3-bea37004f0bb","internalTransactionId":"ea5b5475-03b9-4f08-8e95-bbb11289ab65","upn":"tperkins@f128.info","tenantId":"7918d4b5-0442-4a97-be2d-36f9f9962ece","userObjectId":"17f84be4-51f8-483a-b533-383791227a99"}```

## <a name="next-steps"></a>Passaggi successivi
[Gestione di applicazioni con Azure Active Directory](active-directory-enable-sso-scenario.md)




---
title: "autenticazione a più fattori aaaAzure Accedi con verifica in due passaggi | Documenti Microsoft"
description: Questa pagina forniranno per indicazioni su dove toogo toosee hello vari metodi di accesso disponibili con Azure MFA.
keywords: autenticazione utente, esperienza di accesso con telefono cellulare, accesso con telefono dell'ufficio
services: multi-factor-authentication
documentationcenter: 
author: kgremban
manager: femila
ms.assetid: b310b762-471b-4b26-887a-a321c9e81d46
ms.service: multi-factor-authentication
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/02/2017
ms.author: kgremban
ms.reviewer: librown
ms.custom: end-user
ms.openlocfilehash: fcd5eb5e8426eda537db9e099bf247bde29c195b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="hello-sign-in-experience-with-azure-multi-factor-authentication"></a>Hello esperienza di accesso con Azure multi-Factor Authentication
> [!NOTE]
> Hello in questo articolo mira toowalk tramite un'esperienza di accesso tipico. Per informazioni sull'accesso o tootroubleshoot problemi, vedere [problemi con Azure multi-Factor Authentication](multi-factor-authentication-end-user-troubleshoot.md).

## <a name="what-will-your-sign-in-experience-be"></a>Come sarà l'esperienza di accesso?
L'esperienza di accesso varia a seconda della scelta effettuata toouse come il secondo fattore: una chiamata telefonica, un'app di autenticazione o testi. Scegliere l'opzione hello che meglio descrive le operazioni:

| Come si accede? | 
| --- |
| [Con un telefono cellulare o dell'ufficio toomy telefonata](#signing-in-with-a-phone-call) |
| [Con un telefono cellulare toomy testo](#signing-in-with-a-text-message)
| [Le notifiche da app Microsoft Authenticator hello](#signing-in-with-the-microsoft-authenticator-app-using-notification) |
| [Con i codici di verifica dall'app Microsoft Authenticator hello](#signing-in-with-the-microsoft-authenticator-app-using-verification-code) |
| [Con un metodo alternativo, perché non è possibile usare subito il metodo preferito](#signing-in-with-an-alternate-method) |

## <a name="signing-in-with-a-phone-call"></a>Accesso tramite telefonata
le seguenti informazioni Hello descrive telefono dell'ufficio o dell'esperienza di verifica in due passaggi hello mobili tooyour chiamata.

1. Accedi tooan applicazione o servizio, ad esempio Office 365 usando il nome utente e password.  
2. Microsoft telefona all'utente.  
3. Rispondere hello telefono e premere il tasto di # hello.  

## <a name="signing-in-with-a-text-message"></a>Accesso tramite messaggio di testo
le seguenti informazioni Hello descrive hello esperienza di verifica in due passaggi con un telefono cellulare tooyour messaggio testo:

1. Accedi tooan applicazione o servizio, ad esempio Office 365 usando il nome utente e password. 
2. Microsoft invia un messaggio di testo che contiene un codice numerico. 
3. Immettere il codice hello in hello apposita casella sulla pagina di accesso hello. 

## <a name="signing-in-with-hello-microsoft-authenticator-app"></a>Accedere con l'app Microsoft Authenticator hello 
Hello informazioni riportate di seguito viene descritta hello esperienza di uso dell'app di Microsoft Authenticator hello per le verifiche in due passaggi. Esistono due modi diversi toouse hello app. È possibile ricevere notifiche push sul dispositivo, oppure è possibile aprire hello app tooget un codice di verifica.

### <a name="toosign-in-with-a-notification-from-hello-microsoft-authenticator-app"></a>toosign con una notifica dall'app Microsoft Authenticator hello
1. Accedi tooan applicazione o servizio, ad esempio Office 365 usando il nome utente e password.
2. Microsoft invia un'app di Microsoft Authenticator toohello notifica sul dispositivo.

  ![Microsoft invia una notifica](./media/multi-factor-authentication-end-user-signin/notify.png)

3. Notifica di hello aperto sul telefono e seleziona hello **verificare** chiave. Se la società richiede un PIN, immetterlo qui.
4. Ora dovrebbe essere stato effettuato l'accesso.

### <a name="toosign-in-using-a-verification-code-with-hello-microsoft-authenticator-app"></a>toosign utilizzando un codice di verifica con app Microsoft Authenticator hello

Se si utilizzano i codici di verifica tooget app Authenticator Microsoft hello, quando si apre l'applicazione hello visibili un numero con il nome dell'account. Questo valore cambia ogni 30 secondi in modo che non si utilizza hello stesso numero di due volte. Quando viene richiesto un codice di verifica, aprire l'applicazione hello e utilizzare il numero è attualmente visualizzato. 

1. Accedi tooan applicazione o servizio, ad esempio Office 365 usando il nome utente e password.
2. Microsoft richiede un codice di verifica.

  ![Inserire il codice di verifica dell'app](./media/multi-factor-authentication-end-user-signin/verify3.png)

3. Aprire l'app Microsoft Authenticator hello sul telefono e immettere il codice hello nella casella di hello in cui si accede.

## <a name="signing-in-with-an-alternate-method"></a>Accesso con un metodo alternativo
Non è a volte hello telefono o un dispositivo che è configurato come metodo di verifica preferita. Per questo motivo è consigliabile configurare metodi di backup per l'account. Hello nella sezione seguente illustra come toosign con un metodo alternativo quando il metodo principale potrebbe non essere disponibile.

1. Accedi tooan applicazione o servizio, ad esempio Office 365 usando il nome utente e password.
2. Selezionare **Usa un'opzione di verifica diversa**. Vengono visualizzate diverse opzioni di verifica in base al numero di opzioni configurate.
3. Scegliere un metodo alternativo ed effettuare l’accesso.

  ![Utilizzare un metodo alternativo](./media/multi-factor-authentication-end-user-signin/alt.png)

## <a name="next-steps"></a>Passaggi successivi

In caso di problemi di accesso con la verifica in due passaggi, è possibile ottenere altre informazioni in [Problemi con Multi-Factor Authentication di Azure](multi-factor-authentication-end-user-troubleshoot.md).

Informazioni su come troppo[gestire le impostazioni di verifica in due passaggi](multi-factor-authentication-end-user-manage-settings.md).

Scoprire come troppo[introduzione app Microsoft Authenticator hello](microsoft-authenticator-app-how-to.md) in modo che è possibile utilizzare le notifiche toosign in, invece di testi e chiamate telefoniche. 

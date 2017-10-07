---
title: 'Azure AD: registrazione per la reimpostazione password self-service | Microsoft Docs'
description: Registrare i dati di autenticazione per la reimpostazione password self-service di Azure AD
services: active-directory
keywords: 
documentationcenter: 
author: MicrosoftGuyJFlo
manager: femila
ms.reviewer: gahug
ms.assetid: 
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/07/2017
ms.author: joflore
ms.custom: end-user
ms.openlocfilehash: dfcd0106616218c84d23920b124bed5b202cdd6a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="register-for-self-service-password-reset"></a>Eseguire la registrazione per la reimpostazione password self-service

> [!IMPORTANT]
> **Se si sta visualizzando questa pagina perché si riscontrano problemi nell'accesso,** [seguire questa procedura per cambiare e reimpostare la password](active-directory-passwords-update-your-own-password.md).

Come un utente finale, è possibile reimpostare la password o sbloccare l'account senza toospeak tooa persona utilizzando la reimpostazione della password self-service (SSPR). Prima di poter utilizzare questa funzionalità, sono metodi di autenticazione tooregister o verificare i metodi di autenticazione predefinito hello è popolato l'amministratore.

## <a name="register-or-confirm-authentication-data-with-sspr"></a>Registrare o confermare i dati di autenticazione con la reimpostazione password self-service

1. Hello aperta nel web browser toohello il dispositivo e passare [pagina di registrazione di reimpostazione della password](http://aka.ms/ssprsetup)
2. Immettere il nome utente e la password forniti dall'amministratore.
3. A seconda di come il personale IT stati configurati elementi, uno o più dei seguenti hello opzioni sono disponibili per si tooconfigure e verificano. L'amministratore può popolare alcuni di questi è se hanno le informazioni di autorizzazione toouse hello.
    * Telefono ufficio è solo possibile toobe impostati dall'amministratore
    * Telefono per l'autenticazione deve essere impostato il numero di telefono tooanother toolike accesso sarebbe necessario un telefono cellulare in grado di ricevere un SMS o telefonata.
    * Posta elettronica di autenticazione deve essere impostato come indirizzo di posta elettronica alternativo tooan che è possibile accedere senza password hello è necessario tooreset.
    * Domande di sicurezza fornisce un elenco di domande che l'amministratore ha approvato per si tooanswer. Non è possibile utilizzare hello stessa domanda o di rispondere a più di una volta.
4. Fornire e verificare le informazioni di hello richieste dall'amministratore. Se più di un'opzione è disponibile, è consigliabile registrare la flessibilità di tooprovide più metodi quando non è disponibile un altro metodo (esempio: tooaccess in viaggio e non è possibile telefono dell'ufficio)

    ![Registrare i metodi di autenticazione e fare clic su Fine][Register]

5. Al termine con il passaggio 4 scegliere **fine** e sarà quindi in grado di toouse self-service la reimpostazione della password quando è necessario tooin hello futuro.

Se si immettono dati hello telefono per l'autenticazione o di posta elettronica di autenticazione, non è visibile nella directory globale hello. Hello solo gli utenti autorizzati a visualizzare questi dati sono si e gli amministratori. È solo possibile visualizzare hello risponde alle domande di sicurezza tooyour.

Gli amministratori potrebbero richiedere si tooconfirm i metodi di autenticazione dopo un periodo di tempo toomake che vengano visualizzati i metodi appropriati hello registrati.

## <a name="common-problems-and-their-solutions"></a>Problemi frequenti e relative soluzioni

 Di seguito sono riportati alcuni degli errori più comuni e le relative soluzioni:

| Scenario di errore| Tipo di errore visualizzato| Soluzione |
| --- | --- | --- |
| Dopo aver immesso l'ID utente viene visualizzata una pagina "Contattare l'amministratore" | Contattare l'amministratore <br> <br> È stato rilevato che la password dell'account utente non è gestita da Microsoft. Di conseguenza, non è possibile tooautomatically reimpostare la password. <br> <br> È necessario toocontact il personale IT per ulteriore assistenza. | Questo messaggio viene visualizzato perché il personale IT gestisce la password nell'ambiente locale e non è possibile tooreset la password dal non può accedere il collegamento di account. <br> <br> tooreset la password, contatta il personale IT direttamente per la Guida in linea e consentire loro di conoscono si tooreset la password in modo da consentire questa funzionalità per l'utente.|
| Dopo aver immesso l'ID utente viene visualizzato il messaggio di errore "Account non abilitato per la reimpostazione della password"  | Account non abilitato per la reimpostazione della password <br> <br> Il personale IT non ha configurato l'account per l'uso di questo servizio. <br> <br> Se si desidera, è possibile contattare un amministratore in tooreset l'organizzazione la password per l'utente. | Questo messaggio viene visualizzato perché il personale IT non ha abilitato reimpostazione della password per l'organizzazione dal non può accedere il collegamento di account, o non è concesso in licenza è funzionalità hello toouse. <br> <br> tooreset la password, fare clic sul contatto toosend di collegamento un amministratore della società tooyour un messaggio di posta elettronica del personale IT e informarli desideri tooreset la password in modo da consentire questa funzionalità per l'utente. |
| Dopo aver immesso l'ID utente viene visualizzato il messaggio di errore "Non è stato possibile verificare l'account". | Non è stato possibile verificare l'account <br> <br> Se si desidera, è possibile contattare un amministratore in tooreset l'organizzazione la password per l'utente. | Questo messaggio viene visualizzato perché sono abilitati per la reimpostazione della password, ma non è stato registrato il servizio di hello toouse. tooregister password reimpostata, visitare toohttp://aka.ms/ssprsetup dopo aver recuperato il account di accesso tooyour si dispone. <br> <br> tooreset la password, fare clic su di contattare un amministratore collegamento toosend una società tooyour di posta elettronica personale IT. |

## <a name="next-steps"></a>Passaggi successivi

* [Come toochange l'utilizzo di password self-service di reimpostazione della password](active-directory-passwords-update-your-own-password.md)
* [Pagina di registrazione per la reimpostazione della password](http://aka.ms/ssprsetup)
* [Portale di reimpostazione della password](https://passwordreset.microsoftonline.com/)
* [Impossibile accedere tooyour account Microsoft](https://support.microsoft.com/help/12429/microsoft-account-sign-in-cant)

[Register]: ./media/active-directory-passwords-reset-register/register-2-methods.png "Pagina di registrazione per la reimpostazione della password con metodi registrati e pulsante Fine"


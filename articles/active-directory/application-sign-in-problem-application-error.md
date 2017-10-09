---
title: aaaError nella pagina di un'applicazione dopo l'accesso | Documenti Microsoft
description: Come tooresolve problemi con Azure AD accesso quando un'applicazione hello stesso genera un errore
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
ms.openlocfilehash: 317b6f8e6417520ead80ae4e26c591ba6b134683
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="error-on-an-applications-page-after-signing-in"></a>Errore nella pagina di un'applicazione dopo l'accesso

In questo scenario, Azure AD ha eseguito l'accesso utente hello in, ma un'applicazione hello viene visualizzato un errore non consentire hello utente toosuccessfully fine hello sign in flusso. In questo scenario, un'applicazione hello non accetta il problema di risposta hello da Azure AD.

Esistono alcune delle possibili cause per cui un'applicazione hello rifiutata risposta hello da Azure AD. Se l'errore hello in un'applicazione hello non è sufficientemente chiaro tooknow cosa manca in risposta hello, quindi:

-   Se un'applicazione hello raccolta hello Azure AD, verificare di aver seguito tutti i passaggi nell'articolo hello hello [come toodebug basato su SAML single sign-on tooapplications in Azure Active Directory](https://azure.microsoft.com/documentation/articles/active-directory-saml-debugging).

-   Utilizzare uno strumento come [Fiddler](http://www.telerik.com/fiddler) toocapture SAML richiesta, risposta SAML e token SAML.

-   Condividere risposta SAML hello con hello applicazione fornitore tooknow cosa manca.

## <a name="missing-attributes-in-hello-saml-response"></a>Attributi mancanti hello risposta SAML

un attributo in toobe di configurazione di Azure AD hello inviato in risposta hello Azure AD, tooadd procedura hello riportata di seguito:

1.  Aprire hello [ **portale Azure** ](https://portal.azure.com/) e accedere come un **amministratore globale** o **Co-amministratore.**

2.  Aprire hello **estensione di Azure Active Directory** facendo **più servizi** nella parte inferiore di hello del menu di navigazione a sinistra principale hello.

3.  Digitare **"Azure Active Directory**" nella casella di ricerca di filtro hello e seleziona hello **Azure Active Directory** elemento.

4.  Fare clic su **applicazioni aziendali** dal menu di navigazione a sinistra di hello Azure Active Directory.

5.  Fare clic su **tutte le applicazioni** tooview un elenco di tutte le applicazioni.

   * Se non viene visualizzata l'applicazione hello da visualizzare qui, utilizzare hello **filtro** controllo nella parte superiore di hello di hello **elenco di tutte le applicazioni** e set hello **Mostra** opzione troppo **Tutte le applicazioni.**

6.  Selezionare l'applicazione hello tooconfigure single sign-on.

7.  Una volta che un'applicazione hello caricato, fare clic su hello **Single sign-on** dal menu di navigazione a sinistra dell'applicazione hello.

8.  Fare clic su **visualizzare e modificare gli attributi di tutti gli altri utenti in** hello **gli attributi utente** hello tooedit sezione attributi applicazione toohello toobe inviati nel token SAML hello quando l'utente accede.

   un attributo tooadd:

   * Fare clic su **Aggiungi attributo**. Immettere hello **nome** hello selezionare hello e **valore** dall'elenco a discesa hello.

   * Fare clic su **Salva**. Vedrai hello nuovo attributo tabella hello.

9.  Salvare la configurazione di hello.

Successivo accesso dell'applicazione toohello, hello utente Azure AD inviare nuovo attributo hello hello risposta SAML.

## <a name="hello-application-expects-a-different-user-identifier-value-or-format"></a>un'applicazione Hello prevede un formato o un valore di identificatore utente diverso

Hello Accedi toohello applicazione non riesce perché hello risposta SAML mancano gli attributi, ad esempio i ruoli o un'applicazione hello è previsto un formato diverso per l'attributo EntityID hello.

## <a name="add-an-attribute-in-hello-azure-ad-application-configuration"></a>Aggiungere un attributo nella configurazione dell'applicazione hello Azure AD:

hello toochange valore identificatore utente, effettuare i passaggi di hello seguenti:

1.  Aprire hello [ **portale Azure** ](https://portal.azure.com/) e accedere come un **amministratore globale** o **Co-amministratore.**

2.  Aprire hello **estensione di Azure Active Directory** facendo **più servizi** nella parte inferiore di hello del menu di navigazione a sinistra principale hello.

3.  Digitare **"Azure Active Directory**" nella casella di ricerca di filtro hello e seleziona hello **Azure Active Directory** elemento.

4.  Fare clic su **applicazioni aziendali** dal menu di navigazione a sinistra di hello Azure Active Directory.

5.  Fare clic su **tutte le applicazioni** tooview un elenco di tutte le applicazioni.

   * Se non viene visualizzata l'applicazione hello da visualizzare qui, utilizzare hello **filtro** controllo nella parte superiore di hello di hello **elenco di tutte le applicazioni** e set hello **Mostra** opzione troppo **Tutte le applicazioni.**

6.  Selezionare l'applicazione hello tooconfigure single sign-on.

7.  Una volta che un'applicazione hello caricato, fare clic su hello **Single sign-on** dal menu di navigazione a sinistra dell'applicazione hello.

8.  In hello **gli attributi utente**, selezionare hello identificatore univoco per gli utenti in hello **identificatore utente** elenco a discesa.

## <a name="change-entityid-user-identifier-format"></a>Modificare il formato di EntityID (ID utente)

Se un'applicazione hello prevede che un altro formato per l'attributo EntityID hello. Quindi, non sarà formato EntityID (ID utente) di hello tooselect in grado di Azure AD invia toohello applicazione in risposta hello dopo l'autenticazione utente.

Azure AD selezionare hello formato attributo NameID hello (ID utente) in base al valore di hello selezionato o per hello formato richiesto da un'applicazione hello in hello AuthRequest SAML. Per ulteriori informazioni visitare articolo hello [protocollo Single Sign-On SAML](https://docs.microsoft.com/azure/active-directory/develop/active-directory-single-sign-on-protocol-reference#authnrequest) in hello sezione NameIDPolicy.

## <a name="hello-application-expects-a-different-signature-method-for-hello-saml-response"></a>un'applicazione Hello prevede un metodo di firma diversa per la risposta SAML hello

toochange quali parti del token SAML hello sono firmate digitalmente da Azure Active Directory. Attenersi alla procedura hello riportata di seguito:

1.  Aprire hello [ **portale Azure** ](https://portal.azure.com/) e accedere come un **amministratore globale** o **Co-amministratore.**

2.  Aprire hello **estensione di Azure Active Directory** facendo **più servizi** nella parte inferiore di hello del menu di navigazione a sinistra principale hello.

3.  Digitare **"Azure Active Directory**" nella casella di ricerca di filtro hello e seleziona hello **Azure Active Directory** elemento.

4.  Fare clic su **applicazioni aziendali** dal menu di navigazione a sinistra di hello Azure Active Directory.

5.  Fare clic su **tutte le applicazioni** tooview un elenco di tutte le applicazioni.

  * Se non viene visualizzata l'applicazione hello da visualizzare qui, utilizzare hello **filtro** controllo nella parte superiore di hello di hello **elenco di tutte le applicazioni** e set hello **Mostra** opzione troppo **Tutte le applicazioni.**

6.  Selezionare l'applicazione hello tooconfigure single sign-on.

7.  Una volta che un'applicazione hello caricato, fare clic su hello **Single sign-on** dal menu di navigazione a sinistra dell'applicazione hello.

8.  Fare clic su **Mostra impostazioni di firma certificato avanzate** in hello **certificato di firma SAML** sezione.

9.  Seleziona hello appropriato **opzione firma** previsto dall'applicazione hello:

  * Firma risposta SAML

  * Firma asserzione e risposta SAML

  * Firma asserzione SAML

Successivo accesso dell'applicazione toohello, hello utente l'accesso di Azure AD hello parte della risposta SAML hello selezionato.

## <a name="hello-application-expects-hello-signing-algorithm-toobe-sha-1"></a>un'applicazione Hello prevede hello firma toobe algoritmo SHA-1

Per impostazione predefinita, Azure AD firma token SAML hello utilizzando hello la maggior parte delle algoritmo di sicurezza. Si consiglia di non modificare hello sign algoritmo tooSHA-1 se non richiesto da un'applicazione hello.

toochange hello algoritmo di firma, attenersi alla procedura hello riportata di seguito:

1.  Aprire hello [ **portale Azure** ](https://portal.azure.com/) e accedere come un **amministratore globale** o **Co-amministratore.**

2.  Aprire hello **estensione di Azure Active Directory** facendo **più servizi** nella parte inferiore di hello del menu di navigazione a sinistra principale hello.

3.  Digitare **"Azure Active Directory**" nella casella di ricerca di filtro hello e seleziona hello **Azure Active Directory** elemento.

4.  Fare clic su **applicazioni aziendali** dal menu di navigazione a sinistra di hello Azure Active Directory.

5.  Fare clic su **tutte le applicazioni** tooview un elenco di tutte le applicazioni.

   * Se non viene visualizzata l'applicazione hello da visualizzare qui, utilizzare hello **filtro** controllo nella parte superiore di hello di hello **elenco di tutte le applicazioni** e set hello **Mostra** opzione troppo **Tutte le applicazioni.**

6.  Selezionare l'applicazione hello tooconfigure single sign-on.

7.  Una volta che un'applicazione hello caricato, fare clic su hello **Single sign-on** dal menu di navigazione a sinistra dell'applicazione hello.

8.  Fare clic su **Mostra impostazioni di firma certificato avanzate** in hello **certificato di firma SAML** sezione.

9.  Selezionare SHA-1, hello **algoritmo di firma**.

Successivo hello utente esegue l'accesso nell'applicazione toohello, accesso di Azure AD hello token SAML con l'algoritmo SHA-1.

## <a name="next-steps"></a>Passaggi successivi
[Come toodebug basato su SAML single sign-on tooapplications in Azure Active Directory](https://azure.microsoft.com/documentation/articles/active-directory-saml-debugging)

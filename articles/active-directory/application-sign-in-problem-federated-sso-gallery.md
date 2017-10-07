---
title: aaaProblems applicazione raccolta tooa configurata per federati l'accesso single sign-on | Documenti Microsoft
description: "Linee guida per errori specifici di hello quando si accede a un'applicazione che è stata configurata per basato su SAML single sign-on federato con Azure AD"
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
ms.openlocfilehash: ba20a4904860cf063967029cad33fb80f16e4956
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="problems-signing-in-tooa-gallery-application-configured-for-federated-single-sign-on"></a>Problemi durante l'accesso dell'applicazione raccolta tooa configurata per single sign-on federato

tootroubleshoot il problema, è necessario tooverify configurazione dell'applicazione hello in Azure AD come segue:

-   Aver seguito tutti i passaggi di configurazione di hello per hello applicazione raccolta di Azure AD.

-   Identificatore Hello e configurata in AAD l'URL di risposta corrispondono sono i valori previsti in un'applicazione hello

-   È stato assegnato agli utenti dell'applicazione toohello

## <a name="application-not-found-in-directory"></a>Applicazione non trovata nella directory

*Errore AADSTS70001: Impossibile trovare l'applicazione con identificatore 'https://contoso.com' nella directory hello*.

**Causa possibile**

attributo dell'autorità di certificazione Hello invia da tooAzure applicazione hello che ad nella richiesta SAML hello non corrisponde al valore di identificatore hello configurato nell'applicazione hello Azure AD.

**Risoluzione**

Verificare che tale attributo dell'autorità di certificazione hello nella richiesta SAML hello che corrispondenza hello valore identificatore configurato in Azure AD:

1.  Aprire hello [ **portale Azure** ](https://portal.azure.com/) e accedere come un **amministratore globale** o **Co-amministratore.**

2.  Aprire hello **estensione di Azure Active Directory** facendo **più servizi** nella parte inferiore di hello del menu di navigazione a sinistra principale hello.

3.  Digitare **"Azure Active Directory**" nella casella di ricerca di filtro hello e seleziona hello **Azure Active Directory** elemento.

4.  Fare clic su **applicazioni aziendali** dal menu di navigazione a sinistra di hello Azure Active Directory.

5.  Fare clic su **tutte le applicazioni** tooview un elenco di tutte le applicazioni.

  * Se non viene visualizzata l'applicazione hello da visualizzare qui, utilizzare hello **filtro** controllo nella parte superiore di hello di hello **elenco di tutte le applicazioni** e set hello **Mostra** opzione troppo **Tutte le applicazioni.**

6.  Selezionare l'applicazione hello da tooconfigure single sign-on

7.  Una volta che un'applicazione hello caricato, fare clic su hello **Single sign-on** dal menu di navigazione a sinistra dell'applicazione hello.

8.  Andare troppo**dominio e gli URL** sezione. Verificare che il valore hello nella casella di testo corrispondenti valore hello per il valore di identificatore hello visualizzato per errore hello identificatore hello.

Dopo che è stato aggiornato il valore di identificatore hello in Azure AD e il valore corrispondente a hello invia da un'applicazione hello nella richiesta SAML hello, si dovrebbe essere in grado di toosign toohello applicazione.

## <a name="hello-reply-address-does-not-match-hello-reply-addresses-configured-for-hello-application"></a>indirizzo di risposta Hello corrispondono agli indirizzi di risposta hello configurati per l'applicazione hello.

*Errore AADSTS50011: l'indirizzo di risposta hello 'https://contoso.com' non corrispondono agli indirizzi di risposta hello configurati per l'applicazione hello*

**Causa possibile**

Hello AssertionConsumerServiceURL valore nella richiesta SAML hello non corrisponde al valore di URL di risposta hello o un modello configurato in Azure AD. valore AssertionConsumerServiceURL nella richiesta SAML hello Hello è hello URL viene visualizzato l'errore hello.

**Risoluzione**

Verificare che tale valore AssertionConsumerServiceURL hello nella richiesta SAML hello di corrispondenza hello valore URL di risposta è configurata in Azure AD.

1.  Aprire hello [ **portale Azure** ](https://portal.azure.com/) e accedere come un **amministratore globale** o **Co-amministratore.**

2.  Aprire hello **estensione di Azure Active Directory** facendo **più servizi** nella parte inferiore di hello del menu di navigazione a sinistra principale hello.

3.  Digitare **"Azure Active Directory**" nella casella di ricerca di filtro hello e seleziona hello **Azure Active Directory** elemento.

4.  Fare clic su **applicazioni aziendali** dal menu di navigazione a sinistra di hello Azure Active Directory.

5.  Fare clic su **tutte le applicazioni** tooview un elenco di tutte le applicazioni.

  * Se non viene visualizzata l'applicazione hello da visualizzare qui, utilizzare hello **filtro** controllo nella parte superiore di hello di hello **elenco di tutte le applicazioni** e set hello **Mostra** opzione troppo **Tutte le applicazioni.**

6.  Selezionare l'applicazione hello da tooconfigure single sign-on

7.  Una volta che un'applicazione hello caricato, fare clic su hello **Single sign-on** dal menu di navigazione a sinistra dell'applicazione hello.

8.  Andare troppo**dominio e gli URL** sezione. Verificare o aggiornare il valore di hello nella casella di testo toomatch hello AssertionConsumerServiceURL valore nella richiesta SAML hello di hello URL di risposta.  
    * Se non viene visualizzato hello URL di risposta casella di testo, selezionare hello **Mostra URL impostazioni avanzate** casella di controllo.

Dopo che è stato aggiornato il valore di URL di risposta hello in Azure AD e ha corrispondente valore hello viene inviato per un'applicazione hello in hello richiesta SAML, dovrebbe essere in grado di toosign toohello applicazione.

## <a name="user-not-assigned-a-role"></a>All'utente non è stato assegnato un ruolo

*Errore AADSTS50105: hello effettuato l'accesso utente 'brian@contoso.com' non è assegnato il ruolo di tooa per un'applicazione hello*.

**Causa possibile**

Hello utente non ha ottenuto accesso toohello applicazione in Azure AD.

**Risoluzione**

tooassign uno o più applicazioni tooan utenti direttamente, procedura hello riportata di seguito:

1.  Aprire hello [ **portale Azure** ](https://portal.azure.com/) e accedere come un **amministratore globale.**

2.  Aprire hello **estensione di Azure Active Directory** facendo **più servizi** nella parte inferiore di hello del menu di navigazione a sinistra principale hello.

3.  Digitare **"Azure Active Directory**" nella casella di ricerca di filtro hello e seleziona hello **Azure Active Directory** elemento.

4.  Fare clic su **applicazioni aziendali** dal menu di navigazione a sinistra di hello Azure Active Directory.

5.  Fare clic su **tutte le applicazioni** tooview un elenco di tutte le applicazioni.

  * Se non viene visualizzata l'applicazione hello da visualizzare qui, utilizzare hello **filtro** controllo nella parte superiore di hello di hello **elenco di tutte le applicazioni** e set hello **Mostra** opzione troppo **Tutte le applicazioni.**

6.  Selezionare l'applicazione hello da un elenco di utenti toofrom hello tooassign.

7.  Una volta che un'applicazione hello caricato, fare clic su **utenti e gruppi** dal menu di navigazione a sinistra dell'applicazione hello.

8.  Fare clic su hello **Aggiungi** pulsante sopra hello **utenti e gruppi** hello tooopen elenco **Aggiungi** blade.

9.  Fare clic su hello **utenti e gruppi** selettore di hello **Aggiungi** blade.

10. Tipo di hello **nome completo** o **indirizzo di posta elettronica** dell'utente hello si è interessati nell'assegnazione di hello **ricerca per nome o indirizzo di posta** casella di ricerca.

11. Passare il mouse su hello **utente** in hello elenco tooreveal un **casella di controllo**. Fare clic su tooadd di foto o logo profilo hello casella di controllo successivo toohello dell'utente il toohello utente **selezionati** elenco.

12. **Facoltativo:** se si desidera troppo**aggiungere più di un utente**, in un altro tipo di **nome completo** o **indirizzo di posta elettronica** in hello **Cerca per nome o l'indirizzo di posta elettronica** casella di ricerca e fare clic su questo toohello utente hello casella di controllo tooadd **selezionati** elenco.

13. Al termine della selezione utenti, fare clic su hello **selezionare** tooadd pulsante li toohello elenco di utenti e gruppi toobe assegnato toohello applicazione.

14. **Facoltativo:** fare clic su hello **selezionare il ruolo** selettore di hello **Aggiungi** pannello tooselect un ruolo tooassign toohello utenti selezionati.

15. Fare clic su hello **assegnare** pulsante tooassign hello applicazione toohello gli utenti selezionati.

Dopo un breve periodo di tempo, gli utenti di hello selezionato in toolaunch in grado di queste applicazioni utilizzano hello metodi descritti nella sezione Descrizione della soluzione hello.

## <a name="not-a-valid-saml-request"></a>La richiesta non è un messaggio SAML valido

*Errore AADSTS75005: hello richiesta non è un messaggio di protocollo Saml2 valido.*

**Causa possibile**

Azure Active Directory non supporta hello SAML richiesta inviata da un'applicazione hello per Single Sign-on. Alcuni problemi comuni sono:

-   I campi obbligatori nella richiesta SAML hello mancante

-   Metodo codificato della richiesta SAML

**Risoluzione**

1.  Acquisire la richiesta SAML. seguire l'esercitazione hello [come toodebug basato su SAML single sign-on tooapplications in Azure AD](https://docs.microsoft.com/azure/active-directory/develop/active-directory-saml-debugging) toolearn come toocapture hello SAML richiesta.

2.  Contattare il fornitore dell'applicazione hello e condivisione:

   -   Richiesta SAML

   -   [Requisiti del protocollo SAML per Single Sign-On di Azure](https://docs.microsoft.com/azure/active-directory/develop/active-directory-single-sign-on-protocol-reference)

È necessario convalidare supportano l'implementazione di Azure AD SAML hello per Single Sign-on.

## <a name="no-resource-in-requiredresourceaccess-list"></a>Nessuna risorsa nell'elenco requiredResourceAccess

*Errore AADSTS65005:hello client applicazione ha richiesto l'accesso tooresource ' 00000002-0000-0000-c000-000000000000'. Questa richiesta non riuscito perché il client hello questa risorsa non è specificato nel relativo elenco requiredResourceAccess*.

**Causa possibile**

oggetto applicazione Hello è danneggiato.

**Risoluzione: opzione 1**

problema di hello toosolve, aggiungere il valore dell'identificatore univoco di hello nella configurazione di hello Azure AD. un valore dell'identificatore, tooadd procedura hello riportata di seguito:

1.  Aprire hello [ **portale Azure** ](https://portal.azure.com/) e accedere come un **amministratore globale** o **Co-amministratore.**

2.  Aprire hello **estensione di Azure Active Directory** facendo **più servizi** nella parte inferiore di hello del menu di navigazione a sinistra principale hello.

3.  Digitare **"Azure Active Directory**" nella casella di ricerca di filtro hello e seleziona hello **Azure Active Directory** elemento.

4.  Fare clic su **applicazioni aziendali** dal menu di navigazione a sinistra di hello Azure Active Directory.

5.  Fare clic su **tutte le applicazioni** tooview un elenco di tutte le applicazioni.

  * Se non viene visualizzata l'applicazione hello da visualizzare qui, utilizzare hello **filtro** controllo nella parte superiore di hello di hello **elenco di tutte le applicazioni** e set hello **Mostra** opzione troppo **Tutte le applicazioni.**

6.  Selezionare un'applicazione hello è stato configurato single sign-on.

7.  Una volta che un'applicazione hello caricato, fare clic su hello **Single sign-on** dal menu di navigazione a sinistra dell'applicazione hello

8.  In hello **dominio e l'URL** sezione, verificare hello **Mostra URL impostazioni avanzate**.

9.  in hello **identificatore** casella di testo digitare un identificatore univoco per un'applicazione hello.

10. **Salvare** configurazione hello.


**Risoluzione: opzione 2**

Se l'opzione 1 sopra non non risolvere il problema, provare a rimuovere l'applicazione hello dalla directory hello. Quindi, aggiungere e riconfigurare un'applicazione hello, attenersi alla procedura hello riportata di seguito:

1.  Aprire hello [ **portale Azure** ](https://portal.azure.com/) e accedere come un **amministratore globale** o **Co-amministratore.**

2.  Aprire hello **estensione di Azure Active Directory** facendo **più servizi** nella parte inferiore di hello del menu di navigazione a sinistra principale hello.

3.  Digitare **"Azure Active Directory**" nella casella di ricerca di filtro hello e seleziona hello **Azure Active Directory** elemento.

4.  Fare clic su **applicazioni aziendali** dal menu di navigazione a sinistra di hello Azure Active Directory.

5.  Fare clic su **tutte le applicazioni** tooview un elenco di tutte le applicazioni.

  * Se non viene visualizzata l'applicazione hello da visualizzare qui, utilizzare hello **filtro** controllo nella parte superiore di hello di hello **elenco di tutte le applicazioni** e set hello **Mostra** opzione troppo **Tutte le applicazioni.**

6.  Selezionare l'applicazione hello da tooconfigure single sign-on

7.  Fare clic su **eliminare** in hello alto a sinistra di un'applicazione hello **Panoramica** blade.

8.  Aggiornare Azure AD e aggiungere un'applicazione hello hello raccolta di Azure AD. Quindi, configurare un'applicazione hello

<span id="_Hlk477190176" class="anchor"></span>Dopo la riconfigurazione di un'applicazione hello, si dovrebbe essere in grado di toosign toohello applicazione.

## <a name="certificate-or-key-not-configured"></a>Chiave o certificato non configurato

*Error AADSTS50003: No signing key configured.* (Errore AADSTS50003: nessuna chiave di firma configurata).

**Causa possibile**

oggetto applicazione Hello è danneggiato e Azure AD non riconosce il certificato di hello configurato per un'applicazione hello.

**Risoluzione**

toodelete e creare un nuovo certificato, seguire i passaggi di hello riportati di seguito:

1.  Aprire hello [ **portale Azure** ](https://portal.azure.com/) e accedere come un **amministratore globale** o **Co-amministratore.**

2.  Aprire hello **estensione di Azure Active Directory** facendo **più servizi** nella parte inferiore di hello del menu di navigazione a sinistra principale hello.

3.  Digitare **"Azure Active Directory**" nella casella di ricerca di filtro hello e seleziona hello **Azure Active Directory** elemento.

4.  Fare clic su **applicazioni aziendali** dal menu di navigazione a sinistra di hello Azure Active Directory.

5.  Fare clic su **tutte le applicazioni** tooview un elenco di tutte le applicazioni.

 * Se non viene visualizzata l'applicazione hello da visualizzare qui, utilizzare hello **filtro** controllo nella parte superiore di hello di hello **elenco di tutte le applicazioni** e set hello **Mostra** opzione troppo **Tutte le applicazioni.**

6.  Selezionare l'applicazione hello da tooconfigure single sign-on

7.  Una volta che un'applicazione hello caricato, fare clic su hello **Single sign-on** dal menu di navigazione a sinistra dell'applicazione hello.

8.  Fare clic su **Crea nuovo certificato** in hello **SAML certificato di firma** sezione.

9.  Selezionare la data di scadenza. Fare quindi clic su **Salva**.

10. Controllare **attivare di nuovo certificato** toooverride certificato active di hello. Quindi, fare clic su **salvare** nella parte superiore di hello del pannello hello e accettare il certificato di rollover tooactivate hello.

11. In hello **certificato di firma SAML** fare clic su **rimuovere** tooremove hello **inutilizzato** certificato.

## <a name="problem-when-customizing-hello-saml-claims-sent-tooan-application"></a>Problema durante la personalizzazione delle attestazioni SAML hello inviati tooan applicazione

toolearn come le attestazioni degli attributi toocustomize hello SAML inviato tooyour applicazione, vedere [attestazioni mapping in Azure Active Directory](https://docs.microsoft.com/azure/active-directory/active-directory-claims-mapping) per ulteriori informazioni.

## <a name="next-steps"></a>Passaggi successivi
[Come toodebug basato su SAML single sign-on tooapplications in Azure AD](https://docs.microsoft.com/azure/active-directory/develop/active-directory-saml-debugging)

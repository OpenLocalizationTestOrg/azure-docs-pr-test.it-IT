---
title: aaaHow tooconfigure password single sign-on per un applicationn non raccolta | Documenti Microsoft
description: "Come tooconfigure un'applicazione non raccolta personalizzata per proteggere basato su password single sign-on quando non è elencato nella raccolta di applicazioni Azure AD hello"
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
ms.openlocfilehash: e3d0e658f792a0a63110a198811edc66acd6ccf4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooconfigure-password-single-sign-on-for-a-non-gallery-application"></a>Come password tooconfigure single sign-on per un'applicazione non-raccolta

Inoltre scelte toohello trovato all'interno della raccolta applicazione hello Azure AD, è inoltre hello opzione tooadd un **applicazione non raccolta** quando un'applicazione hello desiderato non è elencata. Mediante questa funzionalità, è possibile aggiungere qualsiasi applicazione che esiste già all'interno dell'organizzazione o in qualsiasi applicazione di terze parti che è possibile utilizzare da un fornitore che non fa già parte di hello [raccolta di applicazioni Azure AD](https://docs.microsoft.com/azure/active-directory/active-directory-appssoaccess-whatis#get-started-with-the-azure-ad-application-gallery).

Dopo aver aggiunto un'applicazione non raccolta, è quindi possibile configurare hello metodo Single sign-on questa applicazione usa selezionando hello **Single Sign-on** elemento di navigazione in un'applicazione aziendale in hello [portale di Azure ](https://portal.azure.com/).

Uno dei hello Single Sign-on metodi disponibili tooyou è hello [basato su Password Single Sign-on](https://docs.microsoft.com/azure/active-directory/active-directory-appssoaccess-whatis#how-does-single-sign-on-with-azure-active-directory-work) opzione. Con hello **aggiungere un'applicazione non raccolta** esperienza, è possibile integrare qualsiasi applicazione che esegue il rendering di un nome utente basato su HTML e la password anche se non è il set di applicazioni preintegrate campo, di input.

Hello questo procedimento funziona consiste in una pagina scraping tecnologia che fa parte di hello estensione del Pannello di accesso che consente di elaborare tooauto-rileva i campi di input nome utente e password, archiviarli in modo sicuro per l'istanza dell'applicazione specifici. Quindi riprodurre in modo sicuro i nomi utente e i campi di toothose password quando un utente si sposta toothat applicazioni nel Pannello di accesso dell'applicazione hello.

Questo è un ottimo modo tooget avviato l'integrazione di qualsiasi tipo di applicazione in Azure AD rapidamente e consente di:

-   Integrare **qualsiasi applicazione HelloWorld** con il tenant di Azure AD, purché il rendering di un nome utente e password campo di input HTML

-   Abilitare **Single Sign-on per gli utenti** archiviandoli in modo sicuro e riproduzione di nomi utente e password per l'applicazione hello è stata integrata con Azure AD

-   **Rilevamento automatico di input** campi per qualsiasi applicazione e consentono di toomanually rilevare tali campi utilizzando hello estensione Browser del Pannello di accesso, nel caso in cui non viene trovato il rilevamento automatico

-   **Supporto di applicazioni che richiedono più campi Accedi** per applicazioni che richiedono più di un semplice nome utente e password campi toosign in

-   **Personalizzare le etichette di hello** hello nome utente e password dei campi di input utente di vedere in hello [Pannello di accesso dell'applicazione](https://docs.microsoft.com/azure/active-directory/active-directory-saas-access-panel-introduction) quando si immettono le proprie credenziali

-   Consenti il **utenti** tooprovide i propri nomi utente e password per tutti gli account esistenti dell'applicazione che sta digitando manualmente su hello [Pannello di accesso dell'applicazione](https://docs.microsoft.com/azure/active-directory/active-directory-saas-access-panel-introduction)

-   Consentire un **membro del gruppo aziendale hello** toospecify hello utente e password utente tooa da assegnato utilizzando hello [accesso all'applicazione Self-Service](https://docs.microsoft.com/azure/active-directory/active-directory-self-service-application-access) funzionalità

-   Consentire un **amministratore** funzionalità quando i nomi utente hello toospecify e le password assegnate tooa utente con credenziali di aggiornamento hello [l'assegnazione di un'applicazione tooan utente](#_How_to_configure_1)

-   Consentire un **amministratore** toospecify hello condiviso username o password utilizzata da un gruppo di persone con le credenziali di aggiornamento hello funzionalità quando [l'assegnazione di un'applicazione di gruppo tooan](#assign-an-application-to-a-group-directly)

Di seguito viene descritto come abilitare [basato su Password Single Sign-on](https://docs.microsoft.com/azure/active-directory/active-directory-appssoaccess-whatis#how-does-single-sign-on-with-azure-active-directory-work) tooany applicazione aggiungere utilizzando hello **aggiungere un'applicazione non raccolta** esperienza.

## <a name="overview-of-steps-required"></a>Panoramica dei passaggi necessari

un'applicazione dalla raccolta di Azure AD hello tooconfigure è necessario:

-   [Aggiungere un'applicazione non inclusa nella raccolta](#add-a-non-gallery-application)

-   [Configurare un'applicazione hello password single sign-on](#configure-the-application-for-password-single-sign-on)

-   [Assegnare l'utente tooa dell'applicazione hello o un gruppo](#assign-the-application-to-a-user-or-a-group)

    -   [Assegnare un'applicazione tooan utente direttamente](#assign-a-user-to-an-application-directly)

    -   [Assegnare un gruppo di applicazioni tooa direttamente](#assign-an-application-to-a-group-directly)

## <a name="add-a-non-gallery-application"></a>Aggiungere un'applicazione non inclusa nella raccolta

un'applicazione dalla raccolta di Azure AD, hello tooadd procedura hello riportata di seguito:

1.  Aprire hello [portale Azure](https://portal.azure.com) e accedere come un **amministratore globale** o **Co-amministratore**

2.  Aprire hello **estensione di Azure Active Directory** facendo **più servizi** nella parte inferiore di hello del menu di navigazione a sinistra principale hello.

3.  Digitare **"Azure Active Directory**" nella casella di ricerca di filtro hello e seleziona hello **Azure Active Directory** elemento.

4.  Fare clic su **applicazioni aziendali** dal menu di navigazione a sinistra di hello Azure Active Directory.

5.  Fare clic su hello **Aggiungi** pulsante nell'angolo superiore destro di hello in hello **applicazioni aziendali** pannello

6.  Fare clic su**Applicazione non nella raccolta**.

7.  Immettere il nome di hello dell'applicazione in hello **nome** casella di testo. Fare clic su **Aggiungi**.

Dopo un breve periodo, è il pannello di configurazione dell'applicazione in grado di toosee hello.

## <a name="configure-hello-application-for-password-single-sign-on"></a>Configurare un'applicazione hello password single sign-on

tooconfigure single sign-on per un'applicazione, attenersi alla procedura hello riportata di seguito:

1.  Aprire hello [ **portale Azure** ](https://portal.azure.com/) e accedere come un **amministratore globale** o **Co-amministratore.**

2.  Aprire hello **estensione di Azure Active Directory** facendo **più servizi** nella parte inferiore di hello del menu di navigazione a sinistra principale hello.

3.  Digitare **"Azure Active Directory**" nella casella di ricerca di filtro hello e seleziona hello **Azure Active Directory** elemento.

4.  Fare clic su **applicazioni aziendali** dal menu di navigazione a sinistra di hello Azure Active Directory.

5.  Fare clic su **tutte le applicazioni** tooview un elenco di tutte le applicazioni.

  * Se non viene visualizzata l'applicazione hello da visualizzare qui, utilizzare hello **filtro** controllo nella parte superiore di hello di hello **elenco di tutte le applicazioni** e set hello **Mostra** opzione troppo **Tutte le applicazioni.**

6.  Selezionare l'applicazione hello tooconfigure single sign-on.

7.  Una volta che un'applicazione hello caricato, fare clic su hello **Single sign-on** dal menu di navigazione a sinistra dell'applicazione hello.

8.  Modalità di selezione hello **basato su Password Sign-on.**

9.  Immettere hello **Sign-on URL**. Si tratta hello URL in cui gli utenti immettono il nome utente e password toosign in a. Verificare i campi di accesso hello sono visibili nell'URL hello.

10. Assegnare gli utenti dell'applicazione toohello.

11. Inoltre, è anche possibile fornire credenziali per conto dell'utente hello selezionando le righe di hello di utenti hello e facendo clic su **credenziali di aggiornamento** e l'immissione di nome utente hello e una password per conto degli utenti hello. In caso contrario, gli utenti in tooenter richiesta hello credenziali stessi all'avvio.

## <a name="assign-a-user-tooan-application-directly"></a>Assegnare un'applicazione tooan utente direttamente

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

## <a name="assign-an-application-tooa-group-directly"></a>Assegnare un gruppo di applicazioni tooa direttamente

tooassign uno o più gruppi di applicazioni tooan direttamente, seguire hello passaggi riportati di seguito:

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

10. Tipo di hello **nome del gruppo completo** del gruppo di hello si è interessati nell'assegnazione di hello **ricerca per nome o indirizzo di posta** casella di ricerca.

11. Passare il mouse su hello **gruppo** in hello elenco tooreveal un **casella di controllo**. Fare clic su tooadd di foto o logo profilo hello casella di controllo successivo toohello del gruppo toohello l'utente **selezionati** elenco.

12. **Facoltativo:** se si desidera troppo**aggiungere più di un gruppo**, in un altro tipo di **nome del gruppo completo** in hello **ricerca per nome o indirizzo di posta** casella di ricerca Fare clic su hello casella di controllo tooadd toohello questo gruppo **selezionati** elenco.

13. Al termine della selezione gruppi, fare clic su hello **selezionare** tooadd pulsante li toohello elenco di utenti e gruppi toobe assegnato toohello applicazione.

14. **Facoltativo:** fare clic su hello **selezionare il ruolo** selettore di hello **Aggiungi** pannello tooselect un toohello tooassign ruolo gruppi di sicurezza selezionato.

15. Fare clic su hello **assegnare** pulsante tooassign hello applicazione toohello gruppi selezionati.

Dopo un breve periodo, gli utenti di hello selezionato toolaunch in grado di queste applicazioni in hello Pannello di accesso.

## <a name="next-steps"></a>Passaggi successivi
[Fornire le applicazioni single sign-on tooyour con Proxy dell'applicazione](active-directory-application-proxy-sso-using-kcd.md)

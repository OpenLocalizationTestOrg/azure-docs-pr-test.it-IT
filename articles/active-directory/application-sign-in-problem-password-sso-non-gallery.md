---
title: aaaProblems tooan applicazione raccolta di Azure AD configurata per la password l'accesso single sign-on | Documenti Microsoft
description: Vengono illustrate le aree problematiche che forniscono indicazioni tootroubleshoot problemi correlati toosigning in tooAzure applicazioni raccolta AD configurate per la password single sign-on
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
ms.openlocfilehash: f53ef4176db37dc6b1da2d61027155a6ba8f331e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="problems-signing-in-tooan-azure-ad-gallery-application-configured-for-password-single-sign-on"></a>Problemi durante l'accesso tooan applicazione raccolta di Azure AD configurata per la password single sign-on

Hello Pannello di accesso è un portale basato sul web che consente un utente che ha un lavoro o scuola account in Azure Active Directory (Azure AD) tooview e avviare basato su cloud applicazioni che amministratore hello Azure AD ha concesso l'accesso a. Un utente con le edizioni di Azure AD consente inoltre di gruppi self-service e funzionalità di gestione di app tramite hello Pannello di accesso. Hello Pannello di accesso è separato dal portale di Azure hello e non richiede agli utenti toohave una sottoscrizione di Azure.

toouse basato su password single sign-on (SSO nel Pannello di accesso, hello estensione del Pannello di accesso hello) deve essere installato nel browser dell'utente hello. Questa estensione viene scaricata automaticamente quando un utente seleziona un'applicazione configurata per il servizio Single Sign-On basato su password.

## <a name="meeting-browser-requirements-for-hello-access-panel"></a>Requisiti del browser per hello Pannello di accesso

Pannello di accesso Hello richiede un browser che supporta JavaScript e CSS sono state abilitate. toouse basato su password single sign-on (SSO nel Pannello di accesso, hello estensione del Pannello di accesso hello) deve essere installato nel browser dell'utente hello. Questa estensione viene scaricata automaticamente quando un utente seleziona un'applicazione configurata per il servizio Single Sign-On basato su password.

Per SSO basato su password, browser dell'utente finale di hello può essere:

-   Internet Explorer 8, 9, 10, 11 su Windows 7 o versioni successive

-   Chrome in Windows 7 o versione successiva e MacOS X o versione successiva

-   Firefox 26.0 o versione successiva in Windows XP SP2 o versione successiva e in Mac OS X 10.6 o versione successiva

>[!NOTE]
>estensione SSO basato su password Hello diventano disponibili per Edge in Windows 10 quando diventano supportate le estensioni del browser per Edge.
>
>

## <a name="how-tooinstall-hello-access-panel-browser-extension"></a>Come tooinstall hello estensione Browser Pannello di accesso

hello tooinstall estensione Browser Pannello di accesso, le operazioni di hello seguenti:

1.  Aprire hello [Pannello di accesso](https://myapps.microsoft.com) in uno dei browser supportato hello e accedere come un **utente** in Azure AD.

2.  Fare clic su un **applicazione password SSO** in hello Pannello di accesso.

3.  Hello prompt dei comandi in cui viene chiesto tooinstall hello selezionare software **installa**.

4.  Basata sul browser è il collegamento di download toohello diretto. **Aggiungere** browser tooyour di estensione hello.

5.  Se il browser viene richiesto, selezionare tooeither **abilitare** o **Consenti** hello estensione.

6.  Al termine dell'installazione, **riavviare** la sessione del browser.

7.  Accedere in hello Pannello di accesso e di vedere se è possibile **avviare** applicazioni password SSO

È anche possibile scaricare l'estensione hello per Chrome e Firefox dai collegamenti diretti hello riportato di seguito:

-   [Estensione Pannello di accesso per Chrome](https://chrome.google.com/webstore/detail/access-panel-extension/ggjhpefgjjfobnfoldnjipclpcfbgbhl)

-   [Estensione Pannello di accesso per Firefox](https://addons.mozilla.org/firefox/addon/access-panel-extension/)

## <a name="setting-up-a-group-policy-for-internet-explorer"></a>Impostazione dei Criteri di gruppo per Internet Explorer

È possibile configurare criteri di gruppo che consentono di estensione del Pannello di accesso tooremotely installazione hello per Internet Explorer nei computer degli utenti.

prerequisiti di Hello includono:

-   È stato impostato [servizi di dominio Active Directory](https://msdn.microsoft.com/library/aa362244%28v=vs.85%29.aspx), e sono stati aggiunti dominio tooyour di computer degli utenti.

-   È necessario disporre di hello tooedit autorizzazione "Modifica impostazioni" hello oggetto Criteri di gruppo (GPO). Per impostazione predefinita, i membri di gruppi di sicurezza seguente hello dispongono di questa autorizzazione: Domain Administrators, Enterprise Administrators e Group Policy Creator Owners. [Altre informazioni](https://technet.microsoft.com/library/cc781991%28v=ws.10%29.aspx)

Seguire l'esercitazione hello [come tooDeploy hello estensione del Pannello di accesso per Internet Explorer utilizzando criteri di gruppo](https://docs.microsoft.com/azure/active-directory/active-directory-saas-ie-group-policy) per istruzioni dettagliate su come tooconfigure hello criteri di gruppo e distribuirlo toousers.

## <a name="troubleshoot-hello-access-panel-in-internet-explorer"></a>Risoluzione dei problemi hello Pannello di accesso in Internet Explorer

Seguire hello [Troubleshoot hello estensione del Pannello di accesso per Internet Explorer](https://docs.microsoft.com/azure/active-directory/active-directory-saas-ie-Troubleshoot) della Guida per l'accesso in uno strumento di diagnostica e istruzioni dettagliate sulla configurazione di estensione hello per Internet Explorer.

## <a name="how-tooconfigure-password-single-sign-on-for-a-non-gallery-application"></a>Come password tooconfigure single sign-on per un'applicazione non-raccolta

un'applicazione dalla raccolta di Azure AD hello tooconfigure è necessario:

-   [Aggiungere un'applicazione non inclusa nella raccolta](#add-a-non-gallery-application)

-   [Configurare un'applicazione hello password single sign-on](#configure-the-application-for-password-single-sign-on)

-   [Assegnare gli utenti dell'applicazione toohello](#assign-users-to-the-application)

### <a name="add-a-non-gallery-application"></a>Aggiungere un'applicazione non inclusa nella raccolta

un'applicazione dalla raccolta di Azure AD, hello tooadd procedura hello riportata di seguito:

1.  Aprire hello [portale Azure](https://portal.azure.com) e accedere come un **amministratore globale** o **Co-amministratore**

2.  Aprire hello **estensione di Azure Active Directory** facendo **più servizi** nella parte inferiore di hello del menu di navigazione a sinistra principale hello.

3.  Digitare **"Azure Active Directory**" nella casella di ricerca di filtro hello e seleziona hello **Azure Active Directory** elemento.

4.  Fare clic su **applicazioni aziendali** dal menu di navigazione a sinistra di hello Azure Active Directory.

5.  Fare clic su hello **Aggiungi** pulsante nell'angolo superiore destro di hello in hello **applicazioni aziendali** pannello

6.  Fare clic su**Applicazione non nella raccolta**.

7.  Immettere il nome di hello dell'applicazione in hello **nome** casella di testo. Fare clic su **Aggiungi**.

Dopo un breve periodo, è il pannello di configurazione dell'applicazione in grado di toosee hello.

### <a name="configure-hello-application-for-password-single-sign-on"></a>Configurare un'applicazione hello password single sign-on

tooconfigure single sign-on per un'applicazione, attenersi alla procedura hello riportata di seguito:

1.  Aprire hello [ **portale Azure** ](https://portal.azure.com/) e accedere come un **amministratore globale** o **Co-amministratore.**

2.  Aprire hello **estensione di Azure Active Directory** facendo **più servizi** nella parte inferiore di hello del menu di navigazione a sinistra principale hello.

3.  Digitare **"Azure Active Directory**" nella casella di ricerca di filtro hello e seleziona hello **Azure Active Directory** elemento.

4.  Fare clic su **applicazioni aziendali** dal menu di navigazione a sinistra di hello Azure Active Directory.

5.  Fare clic su **tutte le applicazioni** tooview un elenco di tutte le applicazioni.

   * Se non viene visualizzata l'applicazione hello da visualizzare qui, utilizzare hello **filtro** controllo nella parte superiore di hello di hello **elenco di tutte le applicazioni** e set hello **Mostra** opzione troppo **Tutte le applicazioni.**

6.  Selezionare l'applicazione hello da tooconfigure single sign-on

7.  Una volta che un'applicazione hello caricato, fare clic su hello **Single sign-on** dal menu di navigazione a sinistra dell'applicazione hello.

8.  Modalità di selezione hello **basato su Password Sign-on.**

9.  Immettere hello **Sign-on URL**. Si tratta hello URL in cui gli utenti immettono il nome utente e password toosign in a. Verificare i campi di accesso hello sono visibili nell'URL hello.

10. Assegnare gli utenti dell'applicazione toohello.

11. Inoltre, è anche possibile fornire credenziali per conto dell'utente hello selezionando le righe di hello di utenti hello e facendo clic su **credenziali di aggiornamento** e l'immissione di nome utente hello e una password per conto degli utenti hello. In caso contrario, gli utenti in tooenter richiesta hello credenziali stessi all'avvio.

### <a name="assign-users-toohello-application"></a>Assegnare gli utenti dell'applicazione toohello

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

Dopo un breve periodo, gli utenti di hello selezionato toolaunch in grado di queste applicazioni in hello Pannello di accesso.

## <a name="if-these-troubleshooting-steps-do-not-hello-resolve-hello-issue"></a>Se questi passaggi di risoluzione dei problemi non hello di risolvere il problema di hello

Aprire un ticket di supporto con hello se disponibili le seguenti informazioni:

-   ID errore di correlazione

-   UPN (indirizzo di posta elettronica dell'utente)

-   ID tenant

-   Tipo di browser

-   Fuso orario e ora o intervallo di tempo durante il quale si verifica l'errore

-   Tracce Fiddler

## <a name="next-steps"></a>Passaggi successivi
[Fornire le applicazioni single sign-on tooyour con Proxy dell'applicazione](active-directory-application-proxy-sso-using-kcd.md)


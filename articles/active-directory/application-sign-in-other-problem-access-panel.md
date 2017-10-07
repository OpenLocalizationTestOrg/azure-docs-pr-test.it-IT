---
title: la firma nell'applicazione tooan dal Pannello di accesso hello aaaProblems | Documenti Microsoft
description: Come l'accesso a un'applicazione da problemi di tootroubleshoot hello Pannello di accesso di Microsoft Azure AD all'indirizzo myapps.microsoft.com
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
ms.reviewer: japere
ms.openlocfilehash: 346c4da06416bb9b330bdd5b1201253af19ba58b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="problems-signing-in-tooan-application-from-hello-access-panel"></a>Problemi durante l'accesso dell'applicazione tooan dal Pannello di accesso hello

Hello Pannello di accesso è un portale basato sul web che consente a un utente con un lavoro o account Azure Active Directory (Azure AD) tooview avvio basato su cloud le applicazioni e dell'istituto di istruzione che hello amministratore di Azure AD ha concesso l'accesso a. 

Queste applicazioni sono configurate per conto di utente hello nel portale di Azure AD hello. un'applicazione Hello deve essere configurata correttamente e toohello assegnato utente o un utente di hello gruppo è un membro di un'applicazione hello toosee in hello Pannello di accesso.

tipo Hello delle App, potrebbe essere visualizzato un utente rientrano nelle seguenti categorie di hello:

-   Applicazioni di Office 365

-   Applicazioni Microsoft e di terze parti configurate con il servizio Single Sign-On basato su federazione

-   Applicazioni SSO basate su password

-   Applicazioni con soluzioni SSO esistenti

## <a name="general-issues-toocheck-first"></a>Generale problemi toocheck prima

-   Assicurarsi di usare un **browser** che soddisfi i requisiti minimi di hello per hello Pannello di accesso.

-   Assicurarsi che il browser dell'utente hello sia aggiunto URL hello di hello applicazione tooits **siti attendibili**.

-   Assicurarsi che sia un'applicazione hello toocheck **configurato** correttamente.

-   Verificare che l'account dell'utente hello è **abilitato** per accessi.

-   Verificare che l'account dell'utente hello è **non bloccato.**

-   Assicurarsi che utente hello **password non è scaduta o è stata dimenticata.**

-   Verificare che **Multi-Factor Authentication** non blocchi l'accesso utente.

-   Verificare che un criterio di **accesso condizionale** o di **protezione delle identità** non blocchi l'accesso utente.

-   Assicurarsi che un utente **informazioni di contatto autenticazione** è toodate tooallow multi-Factor Authentication o l'accesso condizionale criteri toobe applicata.

-   Verificare che tooalso try cancellare i cookie del browser e riprovare toosign in.

## <a name="meeting-browser-requirements-for-hello-access-panel"></a>Requisiti del browser per hello Pannello di accesso

Pannello di accesso Hello richiede un browser che supporta JavaScript e CSS sono state abilitate. toouse basato su password single sign-on (SSO nel Pannello di accesso, hello estensione del Pannello di accesso hello) deve essere installato nel browser dell'utente hello. Questa estensione viene scaricata automaticamente quando un utente seleziona un'applicazione configurata per il servizio Single Sign-On basato su password.

Per SSO basato su password, browser dell'utente finale di hello può essere:

-   Internet Explorer 8, 9, 10, 11 su Windows 7 o versioni successive

-   Edge su Windows 10 Anniversary Edition o versioni successive

-   Chrome in Windows 7 o versione successiva e MacOS X o versione successiva

-   Firefox 26.0 o versione successiva in Windows XP SP2 o versione successiva e in Mac OS X 10.6 o versione successiva

## <a name="how-tooinstall-hello-access-panel-browser-extension"></a>Come tooinstall hello estensione Browser Pannello di accesso

hello tooinstall estensione Browser Pannello di accesso, le operazioni di hello seguenti:

1.  Aprire hello [Pannello di accesso](https://myapps.microsoft.com) in uno dei browser supportato hello e accedere come un **utente** in Azure AD.

2.  Fare clic su un **applicazione password SSO** in hello Pannello di accesso.

3.  Hello prompt dei comandi in cui viene chiesto tooinstall hello selezionare software **installa**.

4.  Basata sul browser è il collegamento di download toohello diretto. **Aggiungere** browser tooyour di estensione hello.

5.  Se il browser viene richiesto, selezionare tooeither **abilitare** o **Consenti** hello estensione.

6.  Al termine dell'installazione, **riavviare** la sessione del browser.

7.  Accedere in hello Pannello di accesso e di vedere se è possibile **avviare** applicazioni password SSO

È anche possibile scaricare l'estensione hello per colore e bordo da collegamenti diretti hello riportati di seguito:

-   [Estensione Pannello di accesso per Chrome](https://chrome.google.com/webstore/detail/access-panel-extension/ggjhpefgjjfobnfoldnjipclpcfbgbhl)

-   [Estensione Pannello di accesso per Edge](https://www.microsoft.com/store/apps/9pc9sckkzk84)

## <a name="how-tooconfigure-federated-single-sign-on-for-an-azure-ad-gallery-application"></a>Come tooconfigure federata single sign-on per un'applicazione di raccolta di Azure AD

Tutte le applicazioni nella raccolta di Azure AD hello abilitata con funzionalità di Enterprise Single Sign-On con un'esercitazione dettagliata disponibile. È possibile accedere hello [elenco di esercitazioni sull'App SaaS toointegrate con Azure Active Directory](https://azure.microsoft.com/documentation/articles/active-directory-saas-tutorial-list/) per una Guida di dettaglio.

un'applicazione dalla raccolta di Azure AD hello tooconfigure è necessario:

-   [Aggiungere un'applicazione hello raccolta di Azure AD](#add-an-application)

-   [Configurare i valori dei metadati dell'applicazione hello in Azure AD (accesso URL, identificatore, l'URL di risposta)](#configure-single-sign-on-for-an-application-from-the-azure-ad-gallery)

-   [Identificatore utente di selezionare e aggiungere l'applicazione toohello toobe inviati gli attributi di utente](#select-user-identifier-and-add-user-attributes-to-be-sent-to-the-application)

-   [Recuperare il certificato e i metadati di Azure AD](#download-the-azure-ad-metadata-or-certificate)

-   [Configurare i valori dei metadati di Azure AD in un'applicazione hello (accesso URL, autorità emittente, Logout URL e certificato)](#configure-single-sign-on-for-an-application-from-the-azure-ad-gallery)

-   [Assegnare gli utenti dell'applicazione toohello](#assign-users-to-the-application)

### <a name="add-an-application-from-hello-azure-ad-gallery"></a>Aggiungere un'applicazione hello raccolta di Azure AD

un'applicazione dalla raccolta di Azure AD, hello tooadd procedura hello riportata di seguito:

1.  Aprire hello [portale Azure](https://portal.azure.com) e accedere come un **amministratore globale** o **Co-amministratore**

2.  Aprire hello **estensione di Azure Active Directory** facendo **più servizi** nella parte inferiore di hello del menu di navigazione a sinistra principale hello.

3.  Digitare **"Azure Active Directory**" nella casella di ricerca di filtro hello e seleziona hello **Azure Active Directory** elemento.

4.  Fare clic su **applicazioni aziendali** dal menu di navigazione a sinistra di hello Azure Active Directory.

5.  Fare clic su hello **Aggiungi** pulsante nell'angolo superiore destro di hello in hello **applicazioni aziendali** pannello

6.  In hello **immettere un nome** casella di testo da hello **Aggiungi dalla raccolta hello** sezione, il nome del tipo hello di un'applicazione hello.

7.  Selezionare l'applicazione hello da tooconfigure per single sign-on.

8.  Prima di aggiungere un'applicazione hello, è possibile modificarne il nome da hello **nome** casella di testo.

9.  Fare clic su **Aggiungi** pulsante, un'applicazione hello tooadd.

Dopo un breve periodo, è il pannello di configurazione dell'applicazione in grado di toosee hello.

### <a name="configure-single-sign-on-for-an-application-from-hello-azure-ad-gallery"></a>Configurare single sign-on per un'applicazione hello raccolta di Azure AD

tooconfigure single sign-on per un'applicazione, attenersi alla procedura hello riportata di seguito:

1.  <span id="_Hlk477187909" class="anchor"><span id="_Hlk477001983" class="anchor"></span></span>Aprire hello [ **portale Azure** ](https://portal.azure.com/) e accedere come un **amministratore globale** o **Co-amministratore.**

2.  Aprire hello **estensione di Azure Active Directory** facendo **più servizi** nella parte inferiore di hello del menu di navigazione a sinistra principale hello.

3.  Digitare **"Azure Active Directory**" nella casella di ricerca di filtro hello e seleziona hello **Azure Active Directory** elemento.

4.  Fare clic su **applicazioni aziendali** dal menu di navigazione a sinistra di hello Azure Active Directory.

5.  Fare clic su **tutte le applicazioni** tooview un elenco di tutte le applicazioni.

  * Se non viene visualizzata l'applicazione hello da visualizzare qui, utilizzare hello **filtro** controllo nella parte superiore di hello di hello **elenco di tutte le applicazioni** e set hello **Mostra** opzione troppo **Tutte le applicazioni.**

6.  Selezionare l'applicazione hello tooconfigure single sign-on.

7.  Una volta che un'applicazione hello caricato, fare clic su hello **Single sign-on** dal menu di navigazione a sinistra dell'applicazione hello.

8.  Selezionare **basato su SAML Sign-on** da hello **modalità** elenco a discesa.

9.  Immettere i valori hello necessarie nelle **dominio e gli URL.** È necessario ottenere questi valori dal fornitore dell'applicazione hello.

   1. un'applicazione hello tooconfigure come SSO avviato da SP, hello Sign in URL è un valore obbligatorio. Per alcune applicazioni, identificatore hello è anche un valore obbligatorio.

   2. applicazione hello tooconfigure come avviata da IdP SSO, hello URL di risposta è un valore obbligatorio. Per alcune applicazioni, identificatore hello è anche un valore obbligatorio.

10. **Facoltativo:** fare clic su **Mostra URL impostazioni avanzate** se si desidera toosee hello non obbligatori valori.

11. In hello **gli attributi utente**, selezionare hello identificatore univoco per gli utenti in hello **identificatore utente** elenco a discesa.

12. **Facoltativo:** fare clic su **visualizzare e modificare tutti gli altri attributi utente** tooedit hello attributi applicazione toohello toobe inviati nel token SAML hello quando l'utente accede.

   un attributo tooadd:

   1. Fare clic su **Aggiungi attributo**. Immettere hello **nome** hello selezionare hello e **valore** dall'elenco a discesa hello.

   2. Fare clic su **Salva**. Vedrai hello nuovo attributo tabella hello.

13. Fare clic su **configura &lt;nome applicazione&gt;**  tooaccess documentazione sulla tooconfigure single sign-on nell'applicazione hello. È inoltre gli URL dei metadati di hello e certificato richiesto toosetup SSO con un'applicazione hello.

14. Fare clic su **salvare** configurazione hello toosave.

15. Assegnare gli utenti dell'applicazione toohello.

### <a name="select-user-identifier-and-add-user-attributes-toobe-sent-toohello-application"></a>Identificatore utente di selezionare e aggiungere l'applicazione toohello toobe inviati gli attributi di utente

tooselect hello identificatore utente o aggiungere gli attributi utente, attenersi alla procedura hello riportata di seguito:

1.  Aprire hello [ **portale Azure** ](https://portal.azure.com/) e accedere come un **amministratore globale** o **Co-amministratore.**

2.  Aprire hello **estensione di Azure Active Directory** facendo **più servizi** nella parte inferiore di hello del menu di navigazione a sinistra principale hello.

3.  Digitare **"Azure Active Directory**" nella casella di ricerca di filtro hello e seleziona hello **Azure Active Directory** elemento.

4.  Fare clic su **applicazioni aziendali** dal menu di navigazione a sinistra di hello Azure Active Directory.

5.  Fare clic su **tutte le applicazioni** tooview un elenco di tutte le applicazioni.

  * Se non viene visualizzata l'applicazione hello da tooshow qui, utilizzare hello **filtro** controllo nella parte superiore di hello di hello **elenco di tutte le applicazioni** e set hello **Mostra** opzione troppo **Tutte le applicazioni.**

6.  Selezionare un'applicazione hello è stato configurato single sign-on.

7.  Una volta che un'applicazione hello caricato, fare clic su hello **Single sign-on** dal menu di navigazione a sinistra dell'applicazione hello.

8.  In hello **gli attributi utente** hello di sezione, selezionare un identificatore univoco per gli utenti in hello **identificatore utente** elenco a discesa. Hello opzione selezionata deve toomatch hello previsto valore utente hello tooauthenticate dell'applicazione hello.

    >[!NOTE]
    >Azure AD selezionare hello formato attributo NameID hello (ID utente) in base al valore di hello selezionato o per hello formato richiesto da un'applicazione hello in hello AuthRequest SAML. Per ulteriori informazioni visitare articolo hello [protocollo Single Sign-On SAML](https://docs.microsoft.com/azure/active-directory/develop/active-directory-single-sign-on-protocol-reference#authnrequest) in hello sezione NameIDPolicy.
    >
    >

9.  Fare clic su attributi utente tooadd, **visualizzazione e modificare tutti gli altri attributi utente** tooedit hello attributi applicazione toohello toobe inviati nel token SAML hello quando l'utente accede.

   un attributo tooadd:

   1. Fare clic su **Aggiungi attributo**. Immettere hello **nome** hello selezionare hello e **valore** dall'elenco a discesa hello.

   2. Fare clic su **Salva**. Vedrai hello nuovo attributo tabella hello.

### <a name="download-hello-azure-ad-metadata-or-certificate"></a>Scaricare i metadati di Azure AD hello o certificato

i metadati dell'applicazione hello toodownload o un certificato da Azure AD, procedura hello riportata di seguito:

1.  Aprire hello [ **portale Azure** ](https://portal.azure.com/) e accedere come un **amministratore globale** o **Co-amministratore.**

2.  Aprire hello **estensione di Azure Active Directory** facendo **più servizi** nella parte inferiore di hello del menu di navigazione a sinistra principale hello.

3.  Digitare **"Azure Active Directory**" nella casella di ricerca di filtro hello e seleziona hello **Azure Active Directory** elemento.

4.  Fare clic su **applicazioni aziendali** dal menu di navigazione a sinistra di hello Azure Active Directory.

5.  Fare clic su **tutte le applicazioni** tooview un elenco di tutte le applicazioni.

  * Se non viene visualizzata l'applicazione hello da visualizzare qui, utilizzare hello **filtro** controllo nella parte superiore di hello di hello **elenco di tutte le applicazioni** e set hello **Mostra** opzione troppo **Tutte le applicazioni.**

6.  Selezionare un'applicazione hello è stato configurato single sign-on.

7.  Una volta che un'applicazione hello caricato, fare clic su hello **Single sign-on** dal menu di navigazione a sinistra dell'applicazione hello.

8.  Andare troppo**certificato di firma SAML** sezione, quindi fare clic su **scaricare** valore della colonna. A seconda di quale applicazione hello richiede la configurazione di single sign-on, vedere uno toodownload opzione hello hello Metadata XML o hello certificato.

    Azure AD non fornisce i metadati hello tooget URL. Hello metadati possono essere recuperati solo come un file XML.

## <a name="how-tooconfigure-federated-single-sign-on-for-a-non-gallery-application"></a>Come tooconfigure federata single sign-on per un'applicazione non-raccolta

un'applicazione non raccolta tooconfigure, è necessario toohave Azure AD premium e un'applicazione hello supporta SAML 2.0. Per altre informazioni sulle versioni di Azure AD, vedere [Prezzi di Azure Active Directory](https://azure.microsoft.com/pricing/details/active-directory/).

-   [Configurare i valori dei metadati dell'applicazione hello in Azure AD (accesso URL, identificatore, l'URL di risposta)](#configuring-single-sign-on)

-   [Identificatore utente di selezionare e aggiungere l'applicazione toohello toobe inviati gli attributi di utente](#select-user-identifier-and-add-user-attributes-to-be-sent-to-the-application)

-   [Recuperare il certificato e i metadati di Azure AD](#download-the-azure-ad-metadata-or-certificate)

-   [Configurare i valori dei metadati di Azure AD in un'applicazione hello (accesso URL, autorità emittente, Logout URL e certificato)](#configuring-single-sign-on)

### <a name="configure-hello-applications-metadata-values-in-azure-ad-sign-on-url-identifier-reply-url"></a>Configurare i valori dei metadati dell'applicazione hello in Azure AD (accesso URL, identificatore, l'URL di risposta)

tooconfigure single sign-on per un'applicazione che non si trova nella raccolta di Azure AD hello, attenersi alla procedura hello riportata di seguito:

1.  Aprire hello [ **portale Azure** ](https://portal.azure.com/) e accedere come un **amministratore globale** o **Co-amministratore.**

2.  Aprire hello **estensione di Azure Active Directory** facendo **più servizi** nella parte inferiore di hello del menu di navigazione a sinistra principale hello.

3.  Digitare **"Azure Active Directory**" nella casella di ricerca di filtro hello e seleziona hello **Azure Active Directory** elemento.

4.  Fare clic su **applicazioni aziendali** dal menu di navigazione a sinistra di hello Azure Active Directory.

5.  Fare clic su hello **Aggiungi** pulsante nell'angolo superiore destro di hello in hello **applicazioni aziendali** pannello

6.  Fare clic su **applicazione Non raccolta** in hello **aggiungere la propria app** sezione

7.  Immettere il nome di hello dell'applicazione hello in hello **nome** casella di testo.

8.  Fare clic su **Aggiungi** pulsante, un'applicazione hello tooadd.

9.  Una volta che un'applicazione hello caricato, fare clic su hello **Single sign-on** dal menu di navigazione a sinistra dell'applicazione hello.

10. Selezionare **basato su SAML Sign-on** in hello **modalità** elenco a discesa

11. Immettere i valori hello necessarie nelle **dominio e gli URL.** È necessario ottenere questi valori dal fornitore dell'applicazione hello.

  1. un'applicazione hello tooconfigure come avviata da IdP SSO, immettere hello URL di risposta e l'identificatore hello.

  2. **Facoltativo:** tooconfigure un'applicazione hello come SSO avviato da SP, hello Sign in URL è un valore obbligatorio.

12. In hello **gli attributi utente**, selezionare hello identificatore univoco per gli utenti in hello **identificatore utente** elenco a discesa.

13. **Facoltativo:** fare clic su **visualizzare e modificare tutti gli altri attributi utente** tooedit hello attributi applicazione toohello toobe inviati nel token SAML hello quando l'utente accede.

   un attributo tooadd:

   1. Fare clic su **Aggiungi attributo**. Immettere hello **nome** hello selezionare hello e **valore** dall'elenco a discesa hello.

   2. Fare clic su **Salva**. Vedrai hello nuovo attributo tabella hello.

14. Fare clic su **configura &lt;nome applicazione&gt;**  tooaccess documentazione sulla tooconfigure single sign-on nell'applicazione hello. È inoltre URL AD Azure e certificato richiesto per un'applicazione hello.

### <a name="select-user-identifier-and-add-user-attributes-toobe-sent-toohello-application"></a>Identificatore utente di selezionare e aggiungere l'applicazione toohello toobe inviati gli attributi di utente

tooselect hello identificatore utente o aggiungere gli attributi utente, attenersi alla procedura hello riportata di seguito:

1.  Aprire hello [ **portale Azure** ](https://portal.azure.com/) e accedere come un **amministratore globale** o **Co-amministratore.**

2.  Aprire hello **estensione di Azure Active Directory** facendo **più servizi** nella parte inferiore di hello del menu di navigazione a sinistra principale hello.

3.  Digitare **"Azure Active Directory**" nella casella di ricerca di filtro hello e seleziona hello **Azure Active Directory** elemento.

4.  Fare clic su **applicazioni aziendali** dal menu di navigazione a sinistra di hello Azure Active Directory.

5.  Fare clic su **tutte le applicazioni** tooview un elenco di tutte le applicazioni.

  * Se non viene visualizzata l'applicazione hello da visualizzare qui, utilizzare hello **filtro** controllo nella parte superiore di hello di hello **elenco di tutte le applicazioni** e set hello **Mostra** opzione troppo **Tutte le applicazioni.**

6.  Selezionare un'applicazione hello è stato configurato single sign-on.

7.  Una volta che un'applicazione hello caricato, fare clic su hello **Single sign-on** dal menu di navigazione a sinistra dell'applicazione hello.

8.  In hello **gli attributi utente** hello di sezione, selezionare un identificatore univoco per gli utenti in hello **identificatore utente** elenco a discesa. Hello opzione selezionata deve toomatch hello previsto valore utente hello tooauthenticate dell'applicazione hello.

   >[!NOTE]
   >Azure AD selezionare hello formato attributo NameID hello (ID utente) in base al valore di hello selezionato o per hello formato richiesto da un'applicazione hello in hello AuthRequest SAML. Per ulteriori informazioni visitare articolo hello [protocollo Single Sign-On SAML](https://docs.microsoft.com/azure/active-directory/develop/active-directory-single-sign-on-protocol-reference#authnrequest) in hello sezione NameIDPolicy.
   >
   >

9.  Fare clic su attributi utente tooadd, **visualizzazione e modificare tutti gli altri attributi utente** tooedit hello attributi applicazione toohello toobe inviati nel token SAML hello quando l'utente accede.

   un attributo tooadd:

   1. Fare clic su **Aggiungi attributo**. Immettere hello **nome** hello selezionare hello e **valore** dall'elenco a discesa hello.

   2. Fare clic su **Salva**. Vedrai hello nuovo attributo tabella hello.

### <a name="download-hello-azure-ad-metadata-or-certificate"></a>Scaricare i metadati di Azure AD hello o certificato

i metadati dell'applicazione hello toodownload o un certificato da Azure AD, procedura hello riportata di seguito:

1.  Aprire hello [ **portale Azure** ](https://portal.azure.com/) e accedere come un **amministratore globale** o **Co-amministratore.**

2.  Aprire hello **estensione di Azure Active Directory** facendo **più servizi** nella parte inferiore di hello del menu di navigazione a sinistra principale hello.

3.  Digitare **"Azure Active Directory**" nella casella di ricerca di filtro hello e seleziona hello **Azure Active Directory** elemento.

4.  Fare clic su **applicazioni aziendali** dal menu di navigazione a sinistra di hello Azure Active Directory.

5.  Fare clic su **tutte le applicazioni** tooview un elenco di tutte le applicazioni.

   * Se non viene visualizzata l'applicazione hello da visualizzare qui, utilizzare hello **filtro** controllo nella parte superiore di hello di hello **elenco di tutte le applicazioni** e set hello **Mostra** opzione troppo **Tutte le applicazioni.**

6.  Selezionare un'applicazione hello è stato configurato single sign-on.

7.  Una volta che un'applicazione hello caricato, fare clic su hello **Single sign-on** dal menu di navigazione a sinistra dell'applicazione hello.

8.  Andare troppo**certificato di firma SAML** sezione, quindi fare clic su **scaricare** valore della colonna. A seconda di quale applicazione hello richiede la configurazione di single sign-on, vedere uno toodownload opzione hello hello Metadata XML o hello certificato.

    Azure AD non fornisce i metadati hello tooget URL. Hello metadati possono essere recuperati solo come un file XML.

## <a name="how-tooconfigure-password-single-sign-on-for-an-azure-ad-gallery-application"></a>Come password tooconfigure single sign-on per un'applicazione di raccolta di Azure AD

un'applicazione dalla raccolta di Azure AD hello tooconfigure è necessario:

-   [Aggiungere un'applicazione hello raccolta di Azure AD](#add-an-application)

-   [Configurare un'applicazione hello password single sign-on](#configure-the-application)

### <a name="add-an-application-from-hello-azure-ad-gallery"></a>Aggiungere un'applicazione hello raccolta di Azure AD

un'applicazione dalla raccolta di Azure AD, hello tooadd procedura hello riportata di seguito:

1.  Aprire hello [portale Azure](https://portal.azure.com) e accedere come un **amministratore globale** o **Co-amministratore**

2.  Aprire hello **estensione di Azure Active Directory** facendo **più servizi** nella parte inferiore di hello del menu di navigazione a sinistra principale hello.

3.  Digitare **"Azure Active Directory**" nella casella di ricerca di filtro hello e seleziona hello **Azure Active Directory** elemento.

4.  Fare clic su **applicazioni aziendali** dal menu di navigazione a sinistra di hello Azure Active Directory.

5.  Fare clic su hello **Aggiungi** pulsante nell'angolo superiore destro di hello in hello **applicazioni aziendali** pannello

6.  In hello **immettere un nome** casella di testo da hello **Aggiungi dalla raccolta hello** sezione, il nome del tipo hello di un'applicazione hello

7.  Selezionare l'applicazione hello da tooconfigure per single sign-on

8.  Prima di aggiungere un'applicazione hello, è possibile modificarne il nome da hello **nome** casella di testo.

9.  Fare clic su **Aggiungi** pulsante, un'applicazione hello tooadd.

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

9.  Assegnare gli utenti dell'applicazione toohello.

10. Inoltre, è anche possibile fornire credenziali per conto dell'utente hello selezionando le righe di hello di utenti hello e facendo clic su **credenziali di aggiornamento** e l'immissione di nome utente hello e una password per conto degli utenti hello. In caso contrario, gli utenti in tooenter richiesta hello credenziali stessi all'avvio.

## <a name="how-tooconfigure-password-single-sign-on-for-a-non-gallery-application"></a>Come password tooconfigure single sign-on per un'applicazione non-raccolta

un'applicazione dalla raccolta di Azure AD hello tooconfigure è necessario:

-   [Aggiungere un'applicazione non inclusa nella raccolta](#add-a-non-gallery-application)

-   [Configurare un'applicazione hello password single sign-on](#configure-the-application-for-password-single-sign-on)

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

6.  Selezionare l'applicazione hello tooconfigure single sign-on.

7.  Una volta che un'applicazione hello caricato, fare clic su hello **Single sign-on** dal menu di navigazione a sinistra dell'applicazione hello.

8.  Modalità di selezione hello **basato su Password Sign-on.**

9.  Immettere hello **Sign-on URL**. Si tratta hello URL in cui gli utenti immettono il nome utente e password toosign in a. Verificare i campi di accesso hello sono visibili nell'URL hello.

10. Assegnare gli utenti dell'applicazione toohello.

11. Inoltre, è anche possibile fornire credenziali per conto dell'utente hello selezionando le righe di hello di utenti hello e facendo clic su **credenziali di aggiornamento** e l'immissione di nome utente hello e una password per conto degli utenti hello. In caso contrario, gli utenti in tooenter richiesta hello credenziali stessi all'avvio.

## <a name="how-tooassign-a-user-tooan-application-directly"></a>Come tooassign direttamente un'applicazione utente tooan

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


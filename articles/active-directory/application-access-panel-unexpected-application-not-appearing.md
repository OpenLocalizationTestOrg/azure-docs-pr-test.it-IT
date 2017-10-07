---
title: applicazione aaaAn assegnato non viene visualizzato nel Pannello di accesso hello | Documenti Microsoft
description: "Risoluzione dei problemi perché un'applicazione non viene visualizzato nel Pannello di accesso hello"
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
ms.reviwer: japere
ms.openlocfilehash: 089883f406267df4552c7fc991883f335ad49fd5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="an-assigned-application-is-not-appearing-on-hello-access-panel"></a>Un'applicazione assegnata non viene visualizzato nel Pannello di accesso hello

Hello Pannello di accesso è un portale basato sul web che consente a un utente con un lavoro o account Azure Active Directory (Azure AD) tooview avvio basato su cloud le applicazioni e dell'istituto di istruzione che hello amministratore di Azure AD ha concesso l'accesso a. Queste applicazioni sono configurate per conto di utente hello nel portale di Azure AD hello. un'applicazione Hello deve essere configurata correttamente e toohello assegnato utente o un utente di hello gruppo è un membro di un'applicazione hello toosee in hello Pannello di accesso.

tipo Hello delle App, potrebbe essere visualizzato un utente rientrano nelle seguenti categorie di hello:

-   Applicazioni di Office 365

-   Applicazioni Microsoft e di terze parti configurate con il servizio Single Sign-On basato su federazione

-   Applicazioni SSO basate su password

-   Applicazioni con soluzioni SSO esistenti

## <a name="general-issues-toocheck-first"></a>Generale problemi toocheck prima

-   Se un'applicazione è stata appena aggiunta utente tooa, riprovare toosign avanti e indietro nel Pannello di accesso dell'utente hello dopo pochi minuti toosee se viene aggiunta un'applicazione hello.

-   Se una licenza è stata rimossa solo da un utente o gruppo utente hello è che un membro di questo potrebbe richiedere molto tempo, a seconda delle dimensioni di hello e la complessità del gruppo di hello per toobe le modifiche apportate. Consentire del tempo aggiuntivo prima della firma in hello Pannello di accesso.

## <a name="problems-related-tooapplication-configuration"></a>Configurazione di problemi correlati tooapplication

È possibile che un'applicazione non venga visualizzata nel pannello di accesso dell'utente a causa di un'errata configurazione della stessa. Ecco alcuni modi in cui che è possibile risolvere problemi di configurazione correlati tooapplication problemi:

-   [Come tooconfigure federata single sign-on per un'applicazione di raccolta di Azure AD](#how-to-configure-federated-single-sign-on-for-an-azure-ad-gallery-application)

-   [Come tooconfigure federata single sign-on per un'applicazione non-raccolta](#how-to-configure-federated-single-sign-on-for-a-non-gallery-application)

-   [Come tooconfigure una password single sign-on dell'applicazione per un'applicazione di raccolta di Azure AD](#how-to-configure-password-single-sign-on-for-a-non-gallery-application)

-   [Come tooconfigure una password single sign-on dell'applicazione per un'applicazione non-raccolta](#how-to-configure-password-single-sign-on-for-a-non-gallery-application)

### <a name="how-tooconfigure-federated-single-sign-on-for-an-azure-ad-gallery-application"></a>Come tooconfigure federata single sign-on per un'applicazione di raccolta di Azure AD

Tutte le applicazioni nella raccolta di Azure AD hello abilitata con funzionalità di Enterprise Single Sign-On con un'esercitazione dettagliata disponibile. È possibile accedere hello [elenco di esercitazioni sull'App SaaS toointegrate con Azure Active Directory](https://azure.microsoft.com/documentation/articles/active-directory-saas-tutorial-list/) per una Guida di dettaglio.

un'applicazione dalla raccolta di Azure AD hello tooconfigure è necessario:

-   [Aggiungere un'applicazione hello raccolta di Azure AD](#add-an-application-from-the-azure-ad-gallery)

-   [Configurare i valori dei metadati dell'applicazione hello in Azure AD (accesso URL, identificatore, l'URL di risposta)](#configure-single-sign-on-for-an-application-from-the-azure-ad-gallery)

-   [Identificatore utente di selezionare e aggiungere l'applicazione toohello toobe inviati gli attributi di utente](#select-user-identifier-and-add-user-attributes-to-be-sent-to-the-application)

-   [Recuperare il certificato e i metadati di Azure AD](#download-the-azure-ad-metadata-or-certificate)

-   [Configurare i valori dei metadati di Azure AD in un'applicazione hello (accesso URL, autorità emittente, Logout URL e certificato)](#configure-single-sign-on-for-an-application-from-the-azure-ad-gallery)

#### <a name="add-an-application-from-hello-azure-ad-gallery"></a>Aggiungere un'applicazione hello raccolta di Azure AD

un'applicazione dalla raccolta di Azure AD, hello tooadd procedura hello riportata di seguito:

1.  Aprire hello [portale Azure](https://portal.azure.com) e accedere come un **amministratore globale** o **Co-amministratore**

2.  Aprire hello **estensione di Azure Active Directory** facendo **più servizi** nella parte inferiore di hello del menu di navigazione a sinistra principale hello.

3.  Digitare **"Azure Active Directory**" nella casella di ricerca di filtro hello e seleziona hello **Azure Active Directory** elemento.

4.  Fare clic su **applicazioni aziendali** dal menu di navigazione a sinistra di hello Azure Active Directory.

5.  Fare clic su hello **Aggiungi** pulsante nell'angolo superiore destro di hello in hello **applicazioni aziendali** blade.

6.  In hello **immettere un nome** casella di testo da hello **Aggiungi dalla raccolta hello** sezione, il nome del tipo hello di un'applicazione hello.

7.  Selezionare l'applicazione hello da tooconfigure per single sign-on.

8.  Prima di aggiungere un'applicazione hello, è possibile modificarne il nome da hello **nome** casella di testo.

9.  Fare clic su **Aggiungi** pulsante, un'applicazione hello tooadd.

Dopo un breve periodo, è il pannello di configurazione dell'applicazione in grado di toosee hello.

#### <a name="configure-single-sign-on-for-an-application-from-hello-azure-ad-gallery"></a>Configurare single sign-on per un'applicazione hello raccolta di Azure AD

tooconfigure single sign-on per un'applicazione, attenersi alla procedura hello riportata di seguito:

1.  Aprire hello [ **portale Azure** ](https://portal.azure.com/) e accedere come un **amministratore globale** o **Co-amministratore.**

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

   2. fare clic su **Salva**. Vedrai hello nuovo attributo tabella hello.

13. Fare clic su **configura &lt;nome applicazione&gt;**  tooaccess documentazione sulla tooconfigure single sign-on nell'applicazione hello. È inoltre gli URL dei metadati di hello e certificato richiesto toosetup SSO con un'applicazione hello.

14. Fare clic su **salvare** configurazione hello toosave.

15. Assegnare gli utenti dell'applicazione toohello.

#### <a name="select-user-identifier-and-add-user-attributes-toobe-sent-toohello-application"></a>Identificatore utente di selezionare e aggiungere l'applicazione toohello toobe inviati gli attributi di utente

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

   2. fare clic su **Salva**. Si noterà hello nuovo attributo tabella hello.

#### <a name="download-hello-azure-ad-metadata-or-certificate"></a>Scaricare i metadati di Azure AD hello o certificato

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

### <a name="how-tooconfigure-federated-single-sign-on-for-a-non-gallery-application"></a>Come tooconfigure federata single sign-on per un'applicazione non-raccolta

un'applicazione non raccolta tooconfigure, è necessario toohave Azure AD premium e un'applicazione hello supporta SAML 2.0. Per altre informazioni sulle versioni di Azure AD, vedere [Prezzi di Azure Active Directory](https://azure.microsoft.com/pricing/details/active-directory/).

-   [Configurare i valori dei metadati dell'applicazione hello in Azure AD (accesso URL, identificatore, l'URL di risposta)](#configuring-single-sign-on)

-   [Identificatore utente di selezionare e aggiungere l'applicazione toohello toobe inviati gli attributi di utente](#select-user-identifier-and-add-user-attributes-to-be-sent-to-the-application)

-   [Recuperare il certificato e i metadati di Azure AD](#download-the-azure-ad-metadata-or-certificate)

-   [Configurare i valori dei metadati di Azure AD in un'applicazione hello (accesso URL, autorità emittente, Logout URL e certificato)](#configuring-single-sign-on)

#### <a name="configure-hello-applications-metadata-values-in-azure-ad-sign-on-url-identifier-reply-url"></a>Configurare i valori dei metadati dell'applicazione hello in Azure AD (accesso URL, identificatore, l'URL di risposta)

tooconfigure single sign-on per un'applicazione che non si trova nella raccolta di Azure AD hello, attenersi alla procedura hello riportata di seguito:

1.  Aprire hello [ **portale Azure** ](https://portal.azure.com/) e accedere come un **amministratore globale** o **Co-amministratore.**

2.  Aprire hello **estensione di Azure Active Directory** facendo **più servizi** nella parte inferiore di hello del menu di navigazione a sinistra principale hello.

3.  Digitare **"Azure Active Directory**" nella casella di ricerca di filtro hello e seleziona hello **Azure Active Directory** elemento.

4.  Fare clic su **applicazioni aziendali** dal menu di navigazione a sinistra di hello Azure Active Directory.

5.  Fare clic su hello **Aggiungi** pulsante nell'angolo superiore destro di hello in hello **applicazioni aziendali** blade.

6.  Fare clic su **applicazione Non raccolta** in hello **aggiungere la propria app** sezione.

7.  Immettere il nome di hello dell'applicazione hello in hello **nome** casella di testo.

8.  Fare clic su **Aggiungi** pulsante, un'applicazione hello tooadd.

9.  Una volta che un'applicazione hello caricato, fare clic su hello **Single sign-on** dal menu di navigazione a sinistra dell'applicazione hello.

10. Selezionare **basato su SAML Sign-on** in hello **modalità** elenco a discesa.

11. Immettere i valori hello necessarie nelle **dominio e gli URL.** È necessario ottenere questi valori dal fornitore dell'applicazione hello.

   1. un'applicazione hello tooconfigure come avviata da IdP SSO, immettere hello URL di risposta e l'identificatore hello.

   2.  **Facoltativo:** tooconfigure un'applicazione hello come SSO avviato da SP, hello Sign in URL è un valore obbligatorio.

12. In hello **gli attributi utente**, selezionare hello identificatore univoco per gli utenti in hello **identificatore utente** elenco a discesa.

13. **Facoltativo:** fare clic su **visualizzare e modificare tutti gli altri attributi utente** tooedit hello attributi applicazione toohello toobe inviati nel token SAML hello quando l'utente accede.

   un attributo tooadd:

   1. Fare clic su **Aggiungi attributo**. Immettere hello **nome** hello selezionare hello e **valore** dall'elenco a discesa hello.

   2. Fare clic su **Salva**. Vedrai hello nuovo attributo tabella hello.

14. Fare clic su **configura &lt;nome applicazione&gt;**  tooaccess documentazione sulla tooconfigure single sign-on nell'applicazione hello. È inoltre URL AD Azure e certificato richiesto per un'applicazione hello.

#### <a name="select-user-identifier-and-add-user-attributes-toobe-sent-toohello-application"></a>Identificatore utente di selezionare e aggiungere l'applicazione toohello toobe inviati gli attributi di utente

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

#### <a name="download-hello-azure-ad-metadata-or-certificate"></a>Scaricare i metadati di Azure AD hello o certificato

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

### <a name="how-tooconfigure-password-single-sign-on-for-an-azure-ad-gallery-application"></a>Come password tooconfigure single sign-on per un'applicazione di raccolta di Azure AD

un'applicazione dalla raccolta di Azure AD hello tooconfigure è necessario:

-   [Aggiungere un'applicazione hello raccolta di Azure AD](#add-an-application-from-the-azure-ad-gallery)

-   [Configurare un'applicazione hello password single sign-on](#configure-the-application-for-password-single-sign-on)

#### <a name="add-an-application-from-hello-azure-ad-gallery"></a>Aggiungere un'applicazione hello raccolta di Azure AD

un'applicazione dalla raccolta di Azure AD, hello tooadd procedura hello riportata di seguito:

1.  Aprire hello [portale Azure](https://portal.azure.com) e accedere come un **amministratore globale** o **Co-amministratore**

2.  Aprire hello **estensione di Azure Active Directory** facendo **più servizi** nella parte inferiore di hello del menu di navigazione a sinistra principale hello.

3.  Digitare **"Azure Active Directory**" nella casella di ricerca di filtro hello e seleziona hello **Azure Active Directory** elemento.

4.  Fare clic su **applicazioni aziendali** dal menu di navigazione a sinistra di hello Azure Active Directory.

5.  Fare clic su hello **Aggiungi** pulsante nell'angolo superiore destro di hello in hello **applicazioni aziendali** blade.

6.  In hello **immettere un nome** casella di testo da hello **Aggiungi dalla raccolta hello** sezione, il nome del tipo hello di un'applicazione hello.

7.  Selezionare l'applicazione hello da tooconfigure per single sign-on.

8.  Prima di aggiungere un'applicazione hello, è possibile modificarne il nome da hello **nome** casella di testo.

9.  Fare clic su **Aggiungi** pulsante, un'applicazione hello tooadd.

Dopo un breve periodo, è il pannello di configurazione dell'applicazione in grado di toosee hello.

#### <a name="configure-hello-application-for-password-single-sign-on"></a>Configurare un'applicazione hello password single sign-on

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

9.  [Assegnare gli utenti dell'applicazione toohello](#how-to-assign-a-user-to-an-application-directly).

10. Inoltre, è anche possibile fornire credenziali per conto dell'utente hello selezionando le righe di hello di utenti hello e facendo clic su **credenziali di aggiornamento** e l'immissione di nome utente hello e una password per conto degli utenti hello. In caso contrario, gli utenti in tooenter richiesta hello credenziali stessi all'avvio.

### <a name="how-tooconfigure-password-single-sign-on-for-a-non-gallery-application"></a>Come password tooconfigure single sign-on per un'applicazione non-raccolta

un'applicazione dalla raccolta di Azure AD hello tooconfigure è necessario:

-   [Aggiungere un'applicazione non inclusa nella raccolta](#add-a-non-gallery-application)

-   [Configurare un'applicazione hello password single sign-on](#configure-the-application-for-password-single-sign-on)

#### <a name="add-a-non-gallery-application"></a>Aggiungere un'applicazione non inclusa nella raccolta

un'applicazione dalla raccolta di Azure AD, hello tooadd procedura hello riportata di seguito:

1.  Aprire hello [portale Azure](https://portal.azure.com) e accedere come un **amministratore globale** o **Co-amministratore**.

2.  Aprire hello **estensione di Azure Active Directory** facendo **più servizi** nella parte inferiore di hello del menu di navigazione a sinistra principale hello.

3.  Digitare **"Azure Active Directory**" nella casella di ricerca di filtro hello e seleziona hello **Azure Active Directory** elemento.

4.  Fare clic su **applicazioni aziendali** dal menu di navigazione a sinistra di hello Azure Active Directory.

5.  Fare clic su hello **Aggiungi** pulsante nell'angolo superiore destro di hello in hello **applicazioni aziendali** blade.

6.  Fare clic su**Applicazione non nella raccolta**.

7.  Immettere il nome di hello dell'applicazione in hello **nome** casella di testo. Fare clic su **Aggiungi**.

Dopo un breve periodo, è il pannello di configurazione dell'applicazione in grado di toosee hello.

#### <a name="configure-hello-application-for-password-single-sign-on"></a>Configurare un'applicazione hello password single sign-on

tooconfigure single sign-on per un'applicazione, attenersi alla procedura hello riportata di seguito:

1.  Aprire hello [ **portale Azure** ](https://portal.azure.com/) e accedere come un **amministratore globale** o **Co-amministratore.**

2.  Aprire hello **estensione di Azure Active Directory** facendo **più servizi** nella parte inferiore di hello del menu di navigazione a sinistra principale hello.

3.  Digitare **"Azure Active Directory**" nella casella di ricerca di filtro hello e seleziona hello **Azure Active Directory** elemento.

4.  Fare clic su **applicazioni aziendali** dal menu di navigazione a sinistra di hello Azure Active Directory.

5.  Fare clic su **tutte le applicazioni** tooview un elenco di tutte le applicazioni.

    1.  Se non viene visualizzata l'applicazione hello da visualizzare qui, utilizzare hello **filtro** controllo nella parte superiore di hello di hello **elenco di tutte le applicazioni** e set hello **Mostra** opzione troppo **Tutte le applicazioni.**

6.  Selezionare l'applicazione hello tooconfigure single sign-on.

7.  Una volta che un'applicazione hello caricato, fare clic su hello **Single sign-on** dal menu di navigazione a sinistra dell'applicazione hello.

8.  Modalità di selezione hello **basato su Password Sign-on.**

9.  Immettere hello **Sign-on URL**. Si tratta hello URL in cui gli utenti immettono il nome utente e password toosign in a. Verificare i campi di accesso hello sono visibili nell'URL hello.

10. [Assegnare gli utenti dell'applicazione toohello](#how-to-assign-a-user-to-an-application-directly).

11. Inoltre, è anche possibile fornire credenziali per conto dell'utente hello selezionando le righe di hello di utenti hello e facendo clic su **credenziali di aggiornamento** e l'immissione di nome utente hello e una password per conto degli utenti hello. In caso contrario, gli utenti in tooenter richiesta hello credenziali stessi all'avvio.

## <a name="problems-related-tooassigning-applications-toousers"></a>Problemi correlati tooassigning applicazioni toousers

Un utente potrebbe non contenere un'applicazione nel proprio pannello di accesso perché non sono assegnati toohello applicazione. Di seguito sono toocheck alcuni modi:

-   [Verificare se un utente è assegnato toohello applicazione](#check-if-a-user-is-assigned-to-the-application)

-   [Come tooassign direttamente un'applicazione utente tooan](#how-to-assign-a-user-to-an-application-directly)

-   [Verificare se un utente viene assegnata una licenza tooa correlati toohello applicazione](#check-if-a-user-is-under-a-license-related-to-the-application)

-   [Come un utente tooa licenza tooassign](#how-to-assign-a-user-a-license)

### <a name="check-if-a-user-is-assigned-toohello-application"></a>Verificare se un utente è assegnato toohello applicazione

toocheck se un utente è assegnato toohello applicazione, attenersi alla procedura hello riportata di seguito:

1.  Aprire hello [ **portale Azure** ](https://portal.azure.com/) e accedere come un **amministratore globale.**

2.  Aprire hello **estensione di Azure Active Directory** facendo **più servizi** nella parte inferiore di hello del menu di navigazione a sinistra principale hello.

3.  Digitare **"Azure Active Directory**" nella casella di ricerca di filtro hello e seleziona hello **Azure Active Directory** elemento.

4.  Fare clic su **applicazioni aziendali** dal menu di navigazione a sinistra di hello Azure Active Directory.

5.  Fare clic su **tutte le applicazioni** tooview un elenco di tutte le applicazioni.

6.  **Ricerca** per nome hello dell'applicazione hello in questione.

7.  Fare clic su **Utenti e gruppi**.

8.  Controllare toosee se l'utente è assegnato toohello applicazione.

   * In caso contrario, seguire i passaggi di hello in "modalità tooassign direttamente un'applicazione utente tooan" toodo in modo.

### <a name="how-tooassign-a-user-tooan-application-directly"></a>Come tooassign direttamente un'applicazione utente tooan

tooassign uno o più applicazioni tooan utenti direttamente, procedura hello riportata di seguito:

1.  Aprire hello [ **portale Azure** ](https://portal.azure.com/) e accedere come un **amministratore globale**.

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

### <a name="check-if-a-user-is-under-a-license-related-toohello-application"></a>Controllare se un utente è in una licenza correlati toohello applicazione

toocheck un utente assegnate le licenze, seguire hello passaggi riportati di seguito:

1.  Aprire hello [ **portale Azure** ](https://portal.azure.com/) e accedere come un **amministratore globale.**

2.  Aprire hello **estensione di Azure Active Directory** facendo **più servizi** nella parte inferiore di hello del menu di navigazione a sinistra principale hello.

3.  Digitare **"Azure Active Directory**" nella casella di ricerca di filtro hello e seleziona hello **Azure Active Directory** elemento.

4.  Fare clic su **utenti e gruppi** nel menu di navigazione hello.

5.  Fare clic su **Tutti gli utenti**.

6.  **Ricerca** per utente hello si è interessati e **fare clic sulla riga hello** tooselect.

7.  Fare clic su **licenze** toosee utente hello licenze è attualmente assegnato.

  * Se utente hello viene assegnata una licenza di Office tooan tooappear applicazioni di Office di terze parti prima in questo modo su hello nel Pannello di accesso dell'utente.

### <a name="how-tooassign-a-user-a-license"></a>Come tooassign una licenza utente 

un utente, tooa licenza tooassign procedura hello riportata di seguito:

1.  Aprire hello [ **portale Azure** ](https://portal.azure.com/) e accedere come un **amministratore globale.**

2.  Aprire hello **estensione di Azure Active Directory** facendo **più servizi** nella parte inferiore di hello del menu di navigazione a sinistra principale hello.

3.  Digitare **"Azure Active Directory**" nella casella di ricerca di filtro hello e seleziona hello **Azure Active Directory** elemento.

4.  Fare clic su **utenti e gruppi** nel menu di navigazione hello.

5.  Fare clic su **Tutti gli utenti**.

6.  **Ricerca** per utente hello si è interessati e **fare clic sulla riga hello** tooselect.

7.  Fare clic su **licenze** toosee utente hello licenze è attualmente assegnato.

8.  Fare clic su hello **assegnare** pulsante.

9.  Selezionare **uno o più prodotti** dall'elenco di hello dei prodotti disponibili.

10. **Parametro facoltativo** fare clic su hello **opzioni assegnazione** toogranularly elemento assegnare i prodotti. Fare clic su **OK** al termine.

11. Fare clic su hello **assegnare** pulsante tooassign questi utente toothis licenze.

## <a name="problems-related-tooassigning-applications-toogroups"></a>Problemi correlati tooassigning applicazioni toogroups

Un utente potrebbe contenere un'applicazione nel proprio pannello di accesso perché fanno parte di un gruppo che dispone di un'applicazione hello. Di seguito sono toocheck alcuni modi:

-   [Controllare le appartenenze ai gruppi di un utente ](#check-a-users-group-memberships)

-   [Come tooassign tooa un'applicazione di gruppo direttamente](#how-to-assign-an-application-to-a-group-directly)

-   [Controllare se un utente fa parte del gruppo assegnato tooa licenza](#check-if-a-user-is-part-of-group-assigned-to-a-license)

-   [Come un gruppo di licenze tooa tooassign](#how-to-assign-a-license-to-a-group)

### <a name="check-a-users-group-memberships"></a>Controllare le appartenenze a gruppi dell'utente

toocheck appartenenza a un gruppo, seguire hello passaggi riportati di seguito:

1.  Aprire hello [ **portale Azure** ](https://portal.azure.com/) e accedere come un **amministratore globale.**

2.  Aprire hello **estensione di Azure Active Directory** facendo **più servizi** nella parte inferiore di hello del menu di navigazione a sinistra principale hello.

3.  Digitare **"Azure Active Directory**" nella casella di ricerca di filtro hello e seleziona hello **Azure Active Directory** elemento.

4.  Fare clic su **utenti e gruppi** nel menu di navigazione hello.

5.  Fare clic su **Tutti gli utenti**.

6.  **Ricerca** per utente hello si è interessati e **fare clic sulla riga hello** tooselect.

7.  Fare clic su **Gruppi**.

8.  Controllare toosee se l'utente fa parte di un'applicazione toohello gruppo assegnato.

  * Se si desidera tooremove hello utente dal gruppo di hello, **fare clic sulla riga hello** del gruppo di hello e seleziona Elimina.

### <a name="how-tooassign-an-application-tooa-group-directly"></a>Come tooassign tooa un'applicazione di gruppo direttamente

tooassign uno o più gruppi di applicazioni tooan direttamente, seguire hello passaggi riportati di seguito:

1.  Aprire hello [ **portale Azure** ](https://portal.azure.com/) e accedere come un **amministratore globale**.

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

### <a name="check-if-a-user-is-part-of-group-assigned-tooa-license"></a>Controllare se un utente fa parte del gruppo assegnato tooa licenza

1.  Aprire hello [ **portale Azure** ](https://portal.azure.com/) e accedere come un **amministratore globale.**

2.  Aprire hello **estensione di Azure Active Directory** facendo **più servizi** nella parte inferiore di hello del menu di navigazione a sinistra principale hello.

3.  Digitare **"Azure Active Directory**" nella casella di ricerca di filtro hello e seleziona hello **Azure Active Directory** elemento.

4.  Fare clic su **utenti e gruppi** nel menu di navigazione hello.

5.  Fare clic su **Tutti gli utenti**.

6.  **Ricerca** per utente hello si è interessati e **fare clic sulla riga hello** tooselect.

7.  Fare clic su **Gruppi**.

8.  Fare clic sulla riga hello di un gruppo specifico.

9.  Fare clic su **licenze** toosee quale gruppo di licenze hello è assegnato tooit.

   * Se gruppo hello viene assegnata una licenza di Office tooan in che questo potrebbe rendere determinati tooappear applicazioni di Office di terze parti prima hello nel Pannello di accesso dell'utente.

### <a name="how-tooassign-a-license-tooa-group"></a>Come un gruppo di licenze tooa tooassign

un gruppo di licenze tooa tooassign procedura hello riportata di seguito:

1.  Aprire hello [ **portale Azure** ](https://portal.azure.com/) e accedere come un **amministratore globale.**

2.  Aprire hello **estensione di Azure Active Directory** facendo **più servizi** nella parte inferiore di hello del menu di navigazione a sinistra principale hello.

3.  Digitare **"Azure Active Directory**" nella casella di ricerca di filtro hello e seleziona hello **Azure Active Directory** elemento.

4.  Fare clic su **utenti e gruppi** nel menu di navigazione hello.

5.  Fare clic su **Tutti i gruppi**.

6.  **Ricerca** per gruppo hello si è interessati e **fare clic sulla riga hello** tooselect.

7.  Fare clic su **licenze** toosee quale gruppo di licenze hello è attualmente assegnato.

8.  Fare clic su hello **assegnare** pulsante.

9.  Selezionare **uno o più prodotti** dall'elenco di hello dei prodotti disponibili.

10. **Parametro facoltativo** fare clic su hello **opzioni assegnazione** toogranularly elemento assegnare i prodotti. Fare clic su **OK** al termine.

11. Fare clic su hello **assegnare** pulsante tooassign questi toothis di gruppo di licenze. L'operazione potrebbe richiedere molto tempo, a seconda delle dimensioni di hello e la complessità del gruppo di hello.

>[!NOTE]
>toodo questo più velocemente, è consigliabile temporaneamente assegna una licenza toohello utente direttamente. 
>
>

## <a name="next-steps"></a>Passaggi successivi
[Aggiungere nuovi utenti tooAzure Active Directory](active-directory-users-create-azure-portal.md)


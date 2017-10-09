---
title: aaaHow tooconfigure federata single sign-on per un'applicazione non raccolta | Documenti Microsoft
description: Come tooconfigure federata single sign-on per un'applicazione non raccolta personalizzata che si desidera toointegrate con Azure AD
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
ms.openlocfilehash: f4a37cb500c075d0ce917ad8f13411f2ce208c56
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooconfigure-federated-single-sign-on-for-a-non-gallery-application"></a>Come tooconfigure federata single sign-on per un'applicazione non-raccolta

un'applicazione non raccolta tooconfigure, è necessario toohave Azure AD premium e un'applicazione hello supporta SAML 2.0. Per altre informazioni sulle versioni di Azure AD, vedere [Prezzi di Azure Active Directory](https://azure.microsoft.com/pricing/details/active-directory/).

## <a name="overview-of-steps-required"></a>Panoramica dei passaggi necessari
Di seguito viene fornita una panoramica ad alto livello di hello passaggi necessari tooconfigure federata single sign-on per un non-raccolta (ad esempio, personalizzata) dell'applicazione.

-   [Configurare i valori dei metadati dell'applicazione hello in Azure AD (accesso URL, identificatore, l'URL di risposta)](#_Configuring_single_sign-on)

-   [Identificatore utente di selezionare e aggiungere l'applicazione toohello toobe inviati gli attributi di utente](#select-user-identifier-and-add-user-attributes-to-be-sent-to-the-application)

-   [Recuperare il certificato e i metadati di Azure AD](#download-the-azure-ad-metadata-or-certificate)

-   [Configurare i valori dei metadati di Azure AD in un'applicazione hello (accesso URL, autorità emittente, Logout URL e certificato)](#_Configuring_single_sign-on)

-   [Assegnare gli utenti dell'applicazione toohello](#_Assign_users_to_the_application)

## <a name="configuring-single-sign-on-toonon-gallery-applications"></a>Configurazione di applicazioni single sign-on toonon-raccolta

tooconfigure single sign-on per un'applicazione che non si trova nella raccolta di Azure AD hello, attenersi alla procedura hello riportata di seguito:

1.  Aprire hello [ **portale Azure** ](https://portal.azure.com/) e accedere come un **amministratore globale** o **Co-amministratore.**

2.  Aprire hello **estensione di Azure Active Directory** facendo **più servizi** nella parte inferiore di hello del menu di navigazione a sinistra principale hello.

3.  Digitare **"Azure Active Directory**" nella casella di ricerca di filtro hello e seleziona hello **Azure Active Directory** elemento.

4.  Fare clic su **applicazioni aziendali** dal menu di navigazione a sinistra di hello Azure Active Directory.

5.  Fare clic su hello **Aggiungi** pulsante nell'angolo superiore destro di hello in hello **applicazioni aziendali** blade.

6.  Fare clic su **applicazione Non raccolta** in hello **aggiungere la propria app** sezione

7.  Immettere il nome di hello dell'applicazione hello in hello **nome** casella di testo.

8.  Fare clic su **Aggiungi** pulsante, un'applicazione hello tooadd.

9.  Una volta che un'applicazione hello caricato, fare clic su hello **Single sign-on** dal menu di navigazione a sinistra dell'applicazione hello.

10. Selezionare **basato su SAML Sign-on** in hello **modalità** elenco a discesa.

11. Immettere i valori hello necessarie nelle **dominio e gli URL.** È necessario ottenere questi valori dal fornitore dell'applicazione hello.

   1. un'applicazione hello tooconfigure come avviata da IdP SSO, immettere hello URL di risposta e l'identificatore hello.

   2. **Facoltativo:** tooconfigure un'applicazione hello come SSO avviato da SP, hello Sign in URL è un valore obbligatorio.

12. In hello **gli attributi utente**, selezionare hello identificatore univoco per gli utenti in hello **identificatore utente** elenco a discesa.

13. **Facoltativo:** fare clic su **visualizzare e modificare tutti gli altri attributi utente** tooedit hello attributi applicazione toohello toobe inviati nel token SAML hello quando l'utente accede.

   un attributo tooadd:

   1. Fare clic su **Aggiungi attributo**. Immettere hello **nome** hello selezionare hello e **valore** dall'elenco a discesa hello.

   2. Fare clic su **Salva**. Vedrai hello nuovo attributo tabella hello.

14. Fare clic su **configura &lt;nome applicazione&gt;**  tooaccess documentazione sulla tooconfigure single sign-on nell'applicazione hello. È inoltre URL AD Azure e certificato richiesto per un'applicazione hello.

15. [Assegnare gli utenti dell'applicazione toohello.](#assign-users-to-the-application)

## <a name="select-user-identifier-and-add-user-attributes-toobe-sent-toohello-application"></a>Identificatore utente di selezionare e aggiungere l'applicazione toohello toobe inviati gli attributi di utente

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

 >[! Nota} di Azure Active Directory, selezionare il formato di hello per hello NameID identificatore dell'attributo (utente) in base al valore di hello selezionato o hello formato richiesto da un'applicazione hello in hello AuthRequest SAML. Per ulteriori informazioni visitare articolo hello [protocollo Single Sign-On SAML](https://docs.microsoft.com/azure/active-directory/develop/active-directory-single-sign-on-protocol-reference#authnrequest) in hello sezione NameIDPolicy.
 >
 >

9.  Fare clic su attributi utente tooadd, **visualizzazione e modificare tutti gli altri attributi utente** tooedit hello attributi applicazione toohello toobe inviati nel token SAML hello quando l'utente accede.

   un attributo tooadd:

   1. Fare clic su **Aggiungi attributo**. Immettere hello **nome** hello selezionare hello e **valore** dall'elenco a discesa hello.

   2. Fare clic su **Salva**. Vedrai hello nuovo attributo tabella hello.

## <a name="download-hello-azure-ad-metadata-or-certificate"></a>Scaricare i metadati di Azure AD hello o certificato

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

## <a name="assign-users-toohello-application"></a>Assegnare gli utenti dell'applicazione toohello

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

## <a name="customizing-hello-saml-claims-sent-tooan-application"></a>Personalizzazione di attestazioni SAML hello inviati tooan applicazione

toolearn come le attestazioni degli attributi toocustomize hello SAML inviato tooyour applicazione, vedere [attestazioni mapping in Azure Active Directory](https://docs.microsoft.com/azure/active-directory/active-directory-claims-mapping) per ulteriori informazioni.

## <a name="next-steps"></a>Passaggi successivi
[Fornire le applicazioni single sign-on tooyour con Proxy dell'applicazione](active-directory-application-proxy-sso-using-kcd.md)

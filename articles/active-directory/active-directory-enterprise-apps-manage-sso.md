---
title: aaaSingle sign-on gestione per applicazioni aziendali in Azure Active Directory hello | Documenti Microsoft
description: Informazioni su come toomanage single sign-on per le app aziendali usando hello Azure Active Directory
services: active-directory
documentationcenter: 
author: asmalser
manager: femila
editor: 
ms.assetid: bcc954d3-ddbe-4ec2-96cc-3df996cbc899
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 07/26/2017
ms.author: asmalser
ms.openlocfilehash: b0a8e622ab10517b7b69f786406b6e9b9f2e7eaa
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="managing-single-sign-on-for-enterprise-apps"></a>Gestione dell'accesso Single Sign-On per le app aziendali
> [!div class="op_single_selector"]
> * [Portale di Azure](active-directory-enterprise-apps-manage-sso.md)
> * [portale di Azure classico](active-directory-sso-integrate-saas-apps.md)
> 

Questo articolo viene descritto come hello toouse [portale di Azure](https://portal.azure.com) toomanage impostazioni single sign-on per le applicazioni aziendali. Le app aziendali sono app distribuite e usate all'interno dell'organizzazione. In questo articolo si applica in particolare tooapps che sono stati aggiunti da hello [raccolta di applicazioni per Azure Active Directory](active-directory-appssoaccess-whatis.md#get-started-with-the-azure-ad-application-gallery). 

## <a name="finding-your-apps-in-hello-portal"></a>Ricerca di App nel portale di hello
Tutte le app aziendali che vengono impostate per single sign-on possono essere visualizzate e gestite nel portale di Azure hello. applicazioni Hello sono reperibile in hello **più servizi** &gt; **applicazioni aziendali** sezione del portale hello. 

![Pannello Applicazioni aziendali][1]

Selezionare **tutte le applicazioni** tooview un elenco di tutte le app che sono stati configurati. Selezione di un'app carica pannello della risorsa hello per l'app, in cui per l'app, è possibile visualizzare i report e una serie di impostazioni può essere gestita.

toomanage impostazioni single sign-on, selezionare **Single sign-on**.

![Pannello Risorsa applicazione][2]

## <a name="single-sign-on-modes"></a>Modalità dell'accesso Single Sign-On
Hello **Single sign-on** pannello inizia con un **modalità** menu, che consente di hello modalità single sign-on toobe configurato. Hello le opzioni disponibili includono:

* **Accesso basato su SAML** -questa opzione è disponibile se l'applicazione hello supporta completo single sign-on federato con Azure Active Directory tramite il protocollo hello SAML 2.0.
* **Password-based sign on** (Accesso basato su password): questa opzione è disponibile se Azure AD supporta la compilazione di moduli con password per questa applicazione.
* **Collegato sign in** -precedentemente noto come "Esistente single sign-on", questa opzione consente agli amministratori tooplace un'applicazione toothis collegamento avvio delle applicazioni dal Pannello di accesso AD Azure o Office 365 dell'utente.

Per altre informazioni su queste modalità, vedere [Come funziona Single Sign-On con Azure Active Directory (PHP)?](active-directory-appssoaccess-whatis.md#how-does-single-sign-on-with-azure-active-directory-work).

## <a name="saml-based-sign-on"></a>Accesso basato su SAML
Hello **accesso basato su SAML** opzione consente di visualizzare un pannello che è suddivisa nelle quattro sezioni:

### <a name="domains-and-urls"></a>Domains and URLs (Domini e URL)
Si tratta in tutti i dettagli sul dominio dell'applicazione hello e gli URL vengono aggiunti tooyour directory di Azure AD. Tutti gli input richiesto app single sign-on lavoro toomake vengono visualizzati direttamente nella schermata di hello, mentre tutti gli input facoltativi possono essere visualizzati selezionando hello **Mostra URL impostazioni avanzate** casella di controllo. elenco completo di Hello di input supportati sono inclusi:

* **URL di accesso** : in cui l'utente di hello non toothis toosign-nell'applicazione. Se un'applicazione hello è servizio configurato tooperform singolo avviato dal provider di accesso, quando l'utente passa toothis URL, il provider di servizi di hello hello necessarie segno e il reindirizzamento AD tooAzure tooauthenticate hello utente. Se questo campo viene popolato, Azure AD utilizzerà l'applicazione hello toolaunch di URL da Office 365 e hello Pannello di accesso AD Azure. Se questo campo viene omesso, Azure AD esegue invece il provider di identità-avvio sign-on quando hello app viene avviata da Office 365, hello Pannello di accesso AD Azure o da hello Azure AD single sign-on URL.
* **Identificatore** -questo URI deve identificare in modo univoco un'applicazione hello per il singolo accesso è stata configurata. Si tratta valore hello che Azure AD invia tooapplication indietro come parametro di destinatari del token SAML hello hello e un'applicazione hello toovalidate previsto è. Questo valore viene inoltre visualizzato come hello ID entità in qualsiasi metadati SAML forniti da un'applicazione hello.
* **URL di risposta** -URL di risposta di hello è in un'applicazione hello prevede token SAML di hello tooreceive. È anche URL servizio Consumer di asserzione (ACS) di cui viene fatto riferimento tooas hello. Dopo avere immesso queste, fare clic su Avanti tooproceed toohello nella schermata successiva. Questa schermata fornisce informazioni su quali toobe esigenze configurato su hello applicazione lato tooenable tooaccept un token SAML da Azure AD.
* **Stato di inoltro** -stato di inoltro hello è un parametro facoltativo che consente di indicare un'applicazione hello in tooredirect hello utente dopo aver completata l'autenticazione. In genere il valore di hello è un URL valido in un'applicazione hello, tuttavia, alcune applicazioni di utilizzare questo campo in modo diverso (sulla documentazione per informazioni dettagliate, vedere l'accesso single sign hello dell'app). stato di inoltro di Hello possibilità tooset hello è una nuova funzionalità che è univoco toohello nuovo portale di Azure.

### <a name="user-attributes"></a>Attributi utente
Si tratta in cui gli amministratori possono visualizzare e modificare gli attributi di hello inviati nel token SAML hello che Azure AD rilascia toohello applicazione ogni volta che gli utenti l'accesso.

Hello solo attributo modificabile supportato è hello **identificatore utente** attributo. il valore di Hello di questo attributo è il campo hello in Azure AD che identifica in modo univoco ogni utente all'interno di un'applicazione hello. Ad esempio, se è stata distribuita l'applicazione di hello utilizzando hello "indirizzo di posta elettronica" come nome utente hello e l'identificatore univoco, quindi il valore di hello viene impostato toohello "user.mail" campo nella Azure AD.

### <a name="saml-signing-certificate"></a>Certificato di firma SAML
In questa sezione mostra i dettagli di hello del certificato hello che Azure AD Usa i token SAML di hello toosign emessi toohello applicazione che ogni utente hello ora esegue l'autenticazione. In questo modo le proprietà di hello di hello corrente certificato toobe controllato, tra cui data di scadenza hello.

### <a name="application-configuration"></a>Configurazione dell'applicazione
la sezione finale Hello fornisce documentazione hello e/o i controlli necessari tooconfigure hello applicazione stessa toouse Azure Active Directory come provider di identità.

Hello **Configura applicazione** menu a comparsa fornisce nuove istruzioni concise e incorporate per la configurazione di un'applicazione hello. Si tratta di un'altra nuova funzionalità toohello univoco nuovo portale di Azure.

> [!NOTE]
> Per un esempio completo della documentazione incorporato, vedere un'applicazione hello Salesforce.com. La documentazione per app aggiuntive viene aggiunta continuamente.
> 
> 

![Documenti incorporati][3]

## <a name="password-based-sign-on"></a>Password-based sign on
Se è supportato per un'applicazione hello, selezionando hello basato su password modalità SSO e selezionando **salvare** Configura immediatamente toodo SSO basato su password. Per altre informazioni sulla distribuzione dell'accesso Single Sign-On basato su password, vedere [Come funziona Single Sign-On con Azure Active Directory (PHP)?](active-directory-appssoaccess-whatis.md#how-does-single-sign-on-with-azure-active-directory-work).

![Password-based sign on][4]

## <a name="linked-sign-on"></a>Linked sign on
Se è supportato per un'applicazione hello, hello collegato in modalità SSO consente tooenter hello URL che si desidera hello Pannello di accesso AD Azure o Office 365 tooredirect toowhen utenti fare clic su questa app. Per altre informazioni sull'accesso Single Sign-On collegato, noto in precedenza come "Accesso Single Sign-On esistente", vedere [Come funziona Single Sign-On con Azure Active Directory (PHP)?](active-directory-appssoaccess-whatis.md#how-does-single-sign-on-with-azure-active-directory-work).

![Linked sign-on (Accesso collegato)][5]

##<a name="feedback"></a>Commenti e suggerimenti

Ci auguriamo che è simile all'utilizzo di hello migliorata l'esperienza di Azure AD. Tenere feedback hello in arrivo. Inviare commenti e suggerimenti e idee per analisi utilizzo software hello **portale di amministrazione** sezione del nostro [forum sul feedback su](https://feedback.azure.com/forums/169401-azure-active-directory/category/162510-admin-portal).  Si sta entusiasti compilazione curiosi di nuovo ogni giorno e tooshape le linee guida e definire cosa creiamo successivamente.

[1]: ./media/active-directory-enterprise-apps-manage-sso/enterprise-apps-blade.PNG
[2]: ./media/active-directory-enterprise-apps-manage-sso/enterprise-apps-sso-blade.PNG
[3]: ./media/active-directory-enterprise-apps-manage-sso/enterprise-apps-blade-embedded-docs.PNG
[4]: ./media/active-directory-enterprise-apps-manage-sso/enterprise-apps-blade-password-sso.PNG
[5]: ./media/active-directory-enterprise-apps-manage-sso/enterprise-apps-blade-linked-sso.PNG

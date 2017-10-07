---
title: aaaHow toodetermine quali single-sign-on metodo toouse | Documenti Microsoft
description: "Comprendere hello single sign-on modalità supportate da Azure AD e come toopick quali uno toochoose per hello applicazione si è interessati."
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
ms.openlocfilehash: 64f0bc1dc8281d1ab8222fd50eaceaf710704886
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="how-toodetermine-what-single-sign-on-method-toouse"></a>Come toodetermine quali single-sign-on toouse (metodo)

Questo articolo è utile toounderstand hello single sign-on modalità supportate da Azure AD e come toopick quali uno toochoose per hello applicazione si è interessati.

## <a name="single-sign-on-and-provisioning-modes-supported-by-specific-application-types"></a>Modalità Single Sign-On e di provisioning supportate da tipi di applicazione specifici

tabella Hello riportata di seguito descrive hello diversi single sign-on e provisioning modalità supportate da ciascuna hello sopra i tipi di applicazione. È possibile utilizzare questa tabella toohelp toounderstand l'applicazione che è necessario tooadd toosupport uno specifico obiettivo.

  ![Tabella tipi di app](./media/application-tables/table1.png)

## <a name="how-toochoose-a-single-sign-on-mode"></a>Come toochoose una modalità single sign-on

Hello supportato **accesso single sign-on** di seguito sono elencate le modalità per le applicazioni di Azure AD.

-   **Azure single sign-on AD disabilitato** – scegliere Azure single sign-on AD disabilitato **modalità single sign-on** se si toointegrate non è ancora disponibile l'applicazione con single sign-on con Azure AD, o semplicemente i test

-   **Collegato Sign-on** – scegliere hello [collegato Sign-on](https://docs.microsoft.com/azure/active-directory/active-directory-appssoaccess-whatis#how-does-single-sign-on-with-azure-active-directory-work) **modalità single sign-on** se si dispone di un'applicazione che è già connesso con single sign-on soluzione esistente o se si desidera toopublish un semplice collegamento per gli utenti nella loro [Pannello di accesso dell'applicazione](https://docs.microsoft.com/azure/active-directory/active-directory-saas-access-panel-introduction) o [avvio applicazione di Office 365](https://login.microsoftonline.com/common/oauth2/authorize?response_mode=form_post&response_type=id_token&scope=openid&nonce=d508a995-f6d6-4b8a-81b8-825c71f1be46.636253878097046923&state=https%3a%2f%2fsupport.office.com%2farticle%2fMeet-the-Office-365-app-launcher-79f12104-6fed-442f-96a0-eb089a3f476a%3fui%3den-US%26rs%3den-US%26ad%3dUS&client_id=4b233688-031c-404b-9a80-a4f3f2351f90&redirect_uri=https%3a%2f%2fsupport.office.com%2fauth%2fsignin&login_hint=asteen%40microsoft.com&prompt=none)

-   **Password-Sign-on basato su** – scegliere hello [basato su Password Sign-on](https://docs.microsoft.com/azure/active-directory/active-directory-appssoaccess-whatis#how-does-single-sign-on-with-azure-active-directory-work) **modalità single sign-on** se l'applicazione esegue il rendering di un campo di nome utente e password HTML e si desidera toostore che nome utente e password in modo sicuro toobe riprodotti in un secondo momento l'applicazione toohello

-   **Basato su SAML Sign-on** – scegliere hello [basato su SAML Sign-on](https://docs.microsoft.com/azure/active-directory/active-directory-appssoaccess-whatis#how-does-single-sign-on-with-azure-active-directory-work) basato su ruoli applicazione toospecific single-sign-on in modalità applicazione supporta i protocolli SAML o OpenID Connect di hello, se si desidera che gli utenti in grado di toomap toobe in regole definite nel SAML attestazioni *(**Nota:** questa opzione non è disponibile quando il proxy di applicazione hello è configurato per un'applicazione) *

-   **Intestazione-Sign-on basato su** : scegliere questa opzione [intestazione-Sign-on basato su](https://docs.microsoft.com/azure/active-directory/application-proxy-ping-access#what-is-pingaccess-for-azure-ad) modalità single sign-on se si dispone di un'applicazione utilizzando PingAccess che supporta l'intestazione HTTP in base l'autenticazione per cui si intende troppo tooperform single sign-in *(**Nota:** questa opzione è disponibile solo quando il proxy di applicazione hello e PingAccess è configurato per un'applicazione) *

-   **Autenticazione integrata di Windows** – scegliere hello [autenticazione integrata di Windows](https://docs.microsoft.com/azure/active-directory/active-directory-application-proxy-sso-using-kcd) single-sign-on in modalità quando si espone un'applicazione WIA locale che si desidera tooperform single sign-in troppo*(*  *Nota:** questa opzione è disponibile solo quando il proxy di applicazione hello è configurato per un'applicazione) *

## <a name="single-sign-on-modes-for-custom-developed-applications"></a>Modalità Single Sign-On per le applicazioni personalizzate

Le applicazioni sono personalizzate sviluppate tramite hello [applicazione personalizzata](#_Custom-Developed_Applications) esperienza supportano anche single sign-on modalità aggiuntive non elencate in precedenza. incluse le seguenti:

-   Accesso basato su [OAuth 2.0](https://docs.microsoft.com/azure/active-directory/develop/active-directory-protocols-oauth-code)

-   Accesso basato su [OpenID Connect 1.0](https://docs.microsoft.com/azure/active-directory/develop/active-directory-protocols-openid-connect-code)

-   Accesso basato su [WS-Federation 1.2](http://docs.oasis-open.org/wsfed/federation/v1.2/os/ws-federation-1.2-spec-os.html)

-   Accesso basato su [SAML 2.0](https://docs.microsoft.com/azure/active-directory/develop/active-directory-saml-protocol-reference)

Hello lettura [Guida per gli sviluppatori di Azure Active Directory](https://docs.microsoft.com/azure/active-directory/develop/active-directory-developers-guide) toolearn ulteriori informazioni sulla modalità applicazione toocreate sviluppato personalizzato che supporta questi single sign-on modalità.

## <a name="how-tooset-an-applications-single-sign-on-mode"></a>Come tooset un'applicazione di single sign-on modalità

del tooset un'applicazione **accesso single sign-on** modalità, seguire le istruzioni di hello riportato di seguito:

1.  Aprire hello [ **portale Azure** ](https://portal.azure.com/) e accedere come un **amministratore globale** o **Co-amministratore.**

2.  Aprire hello **estensione di Azure Active Directory** facendo **più servizi** nella parte inferiore di hello del menu di navigazione a sinistra principale hello.

3.  Digitare **"Azure Active Directory**" nella casella di ricerca di filtro hello e seleziona hello **Azure Active Directory** elemento.

4.  Fare clic su **applicazioni aziendali** dal menu di navigazione a sinistra di hello Azure Active Directory.

5.  Fare clic su **tutte le applicazioni** tooview un elenco di tutte le applicazioni.

   * Se non viene visualizzata l'applicazione hello da visualizzare qui, utilizzare hello **filtro** controllo nella parte superiore di hello di hello **elenco di tutte le applicazioni** e set hello **Mostra** opzione troppo **Tutte le applicazioni.**

6.  Selezionare l'applicazione hello da tooconfigure single sign-on

7.  Una volta che un'applicazione hello caricato, fare clic su **Single sign-on** dal menu di navigazione a sinistra dell'applicazione hello.

## <a name="next-steps"></a>Passaggi successivi
[Fornire le applicazioni single sign-on tooyour con Proxy dell'applicazione](active-directory-application-proxy-sso-using-kcd.md)


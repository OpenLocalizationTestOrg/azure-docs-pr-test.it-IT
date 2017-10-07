---
title: toochoose aaaHow quale applicazione digitare toouse durante l'aggiunta di un'applicazione | Documenti Microsoft
description: "Comprendere hello supportato tipi di applicazioni è possibile integrare con Azure AD e le opzioni di configurazione correlati"
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
ms.openlocfilehash: 46e3672e7f5048b0fa54171f0fc169362c9d5ac6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="how-toochoose-which-application-type-toouse-when-adding-an-application"></a>Come toochoose quale applicazione digitare toouse durante l'aggiunta di un'applicazione

Questo articolo è utile toounderstand hello quattro tipi principali di applicazioni è possibile integrare con Azure AD:

* Applicazioni supportate da ciascuno di essi
* Motivo per cui scegliere una determinata applicazione
* Tooconfigure proprietà principali di tali dell'applicazione, come come gli utenti sono **provisioning**, o cosa **accesso single sign-on** toouse tecnologia.

## <a name="supported-application-types-in-azure-ad"></a>Tipi di applicazioni supportate in Azure AD

Azure AD supporta quattro principali tipi di applicazioni che è possibile aggiungere tramite hello **Aggiungi** funzionalità disponibile in **applicazioni aziendali**. incluse le seguenti:

-   **Applicazioni della raccolta di Azure AD**: un'applicazione che è già stata integrata per un accesso Single Sign-On con Azure AD.

-   **Le applicazioni di Proxy applicazione** : un'applicazione in esecuzione nell'ambiente locale che si desidera tooprovide protetta single-sign-on tooexternally.

-   **Applicazioni sviluppate personalizzato** : hello di un'applicazione che l'organizzazione intende toodevelop nella piattaforma di sviluppo dell'applicazione AD Azure, ma che non esista ancora.

-   **Applicazioni non incluse nella raccolta**: tutte le altre applicazioni. Qualsiasi collegamento web da o in qualsiasi applicazione che esegue il rendering di un campo di nome utente e password, supporta i protocolli SAML o OpenID Connect o supporti SCIM che si desidera toointegrate per single sign-on con Azure AD.

## <a name="features-and-capabilities-supported-by-all-hello-above-application-types"></a>Caratteristiche e funzionalità supportate da tutti hello sopra i tipi di applicazione

Hello funzionalità seguenti sono supportate da uno qualsiasi dei hello sopra 4 tipi di applicazione in Azure AD:

-   **Avvio rapido**: consente l'uso rapido di un'applicazione tramite una [semplice procedura di distribuzione](https://docs.microsoft.com/azure/active-directory/active-directory-integrating-applications-getting-started)

-   **Gestione delle proprietà Generale** : ottenere un [diretta con collegamento diretto](https://docs.microsoft.com/azure/active-directory/active-directory-appssoaccess-whatis#deploying-azure-ad-integrated-applications-to-users) applicazione tooan, [personalizzazione hello](https://docs.microsoft.com/azure/active-directory/active-directory-coreapps-change-app-logo-user-azure-portal) di un'applicazione, o [disabilitare un'applicazione hello](https://docs.microsoft.com/azure/active-directory/active-directory-coreapps-disable-app-azure-portal) per tutti gli utenti.

-   **Gestione di utenti e gruppi** – [assegnare](https://docs.microsoft.com/azure/active-directory/active-directory-coreapps-assign-user-azure-portal) o [rimuovere](https://docs.microsoft.com/azure/active-directory/active-directory-coreapps-remove-assignment-azure-portal) applicazione tooan utenti e gruppi e, facoltativamente, assegnare ruoli specifici dell'applicazione di hello questi utenti e gruppi di avere a dispongano

-   **Accesso all'applicazione self-service** : abilitare il toorequest utenti [accesso all'applicazione self-service](https://docs.microsoft.com/azure/active-directory/active-directory-self-service-application-access) applicazione tooan da loro accesso all'applicazione pannelli aggiungendo un'applicazione, direttamente o [ unione di un gruppo abilitato self-service](https://docs.microsoft.com/azure/active-directory/active-directory-accessmanagement-self-service-group-management)facoltativamente che richiedono l'approvazione di business lungo hello modo

-   **I log di accesso** – vedere [tutti hello applicazione tooan accessi](https://docs.microsoft.com/azure/active-directory/active-directory-reporting-activity-sign-ins), o tutte le applicazioni

-   **Log di controllo** – vedere [dettagliati registri di controllo sull'applicazione di modifiche tooan](https://docs.microsoft.com/azure/active-directory/active-directory-reporting-activity-audit-logs), tooall o le applicazioni

-   **Accesso condizionale e basati sui rischi** : impostare potenti [le regole di accesso basata sulla condizione](https://docs.microsoft.com/azure/active-directory/active-directory-conditional-access) che vengono applicate quando gli utenti tentano di toosign tooa di applicazione specifico

-   **Visualizzazione autorizzazioni** – visualizzare hello [autorizzazioni OAuth2](https://docs.microsoft.com/azure/active-directory/active-directory-apps-permissions-consent) un'applicazione con accesso tooin la directory da un'unica posizione

## <a name="single-sign-on-and-provisioning-modes-supported-by-specific-application-types"></a>Modalità Single Sign-On e di provisioning supportate da tipi di applicazione specifici

tabella Hello riportata di seguito descrive hello diversi single sign-on e provisioning modalità supportate da ciascuna hello sopra i tipi di applicazione. È possibile utilizzare questa tabella toohelp toounderstand l'applicazione che è necessario tooadd toosupport uno specifico obiettivo.

  ![Tabella tipi di app](./media/application-tables/table1.png)

## <a name="how-toochoose-a-single-sign-on-mode"></a>Come toochoose una modalità single sign-on

Hello supportato **accesso single sign-on** di seguito sono elencate le modalità per le applicazioni di Azure AD.

-   **Azure single sign-on AD disabilitato** – scegliere Azure single sign-on AD disabilitato **modalità single sign-on** se si toointegrate non è ancora disponibile l'applicazione con single sign-on con Azure AD, o semplicemente i test

-   **Collegato Sign-on** – scegliere hello [collegato Sign-on](https://docs.microsoft.com/azure/active-directory/active-directory-appssoaccess-whatis#how-does-single-sign-on-with-azure-active-directory-work) **modalità single sign-on** se si dispone di un'applicazione che è già connesso con single sign-on soluzione esistente o se si desidera toopublish un semplice collegamento per gli utenti nella loro [Pannello di accesso dell'applicazione](https://docs.microsoft.com/azure/active-directory/active-directory-saas-access-panel-introduction) o [avvio applicazione di Office 365](https://login.microsoftonline.com/common/oauth2/authorize?response_mode=form_post&response_type=id_token&scope=openid&nonce=d508a995-f6d6-4b8a-81b8-825c71f1be46.636253878097046923&state=https%3a%2f%2fsupport.office.com%2farticle%2fMeet-the-Office-365-app-launcher-79f12104-6fed-442f-96a0-eb089a3f476a%3fui%3den-US%26rs%3den-US%26ad%3dUS&client_id=4b233688-031c-404b-9a80-a4f3f2351f90&redirect_uri=https%3a%2f%2fsupport.office.com%2fauth%2fsignin&login_hint=asteen%40microsoft.com&prompt=none)

-   **Password-Sign-on basato su** – scegliere hello [basato su Password Sign-on](https://docs.microsoft.com/azure/active-directory/active-directory-appssoaccess-whatis#how-does-single-sign-on-with-azure-active-directory-work) **modalità single sign-on** se l'applicazione esegue il rendering di un campo di nome utente e password HTML e si desidera toostore che nome utente e password in modo sicuro toobe riprodotti in un secondo momento l'applicazione toohello

-   **Basato su SAML Sign-on** – scegliere hello [basato su SAML Sign-on](https://docs.microsoft.com/azure/active-directory/active-directory-appssoaccess-whatis#how-does-single-sign-on-with-azure-active-directory-work) basato su ruoli applicazione toospecific single-sign-on in modalità applicazione supporta i protocolli SAML o OpenID Connect di hello, se si desidera che gli utenti in grado di toomap toobe in regole definite nel SAML attestazioni *

   >[!NOTE]
   >Questa opzione non è disponibile quando il proxy di applicazione hello è configurato per un'applicazione.
   >
   >

-   **Intestazione-Sign-on basato su** : scegliere questa opzione [intestazione-Sign-on basato su](https://docs.microsoft.com/azure/active-directory/application-proxy-ping-access#what-is-pingaccess-for-azure-ad) modalità single sign-on se si dispone di un'applicazione utilizzando PingAccess che supporta l'intestazione HTTP in base l'autenticazione per cui si intende troppo tooperform single sign-in

   >[!NOTE]
   >Questa opzione è disponibile solo quando il proxy di applicazione hello e PingAccess è configurato per un'applicazione.
   >
   >

-   **Autenticazione integrata di Windows** – scegliere hello [autenticazione integrata di Windows](https://docs.microsoft.com/azure/active-directory/active-directory-application-proxy-sso-using-kcd) single-sign-on in modalità quando si espone un'applicazione WIA locale che si desidera troppo tooperform single sign-in

   >[!NOTE]
   >Questa opzione è disponibile solo quando il proxy di applicazione hello è configurato per un'applicazione.
   >
   >

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

6.  Selezionare un'applicazione hello per cui si desidera tooconfigure single sign-on.

7.  Una volta che un'applicazione hello caricato, fare clic su **Single sign-on** dal menu di navigazione a sinistra dell'applicazione hello.

## <a name="how-toochoose-a-provisioning-mode"></a>Come toochoose una modalità di provisioning

-   **Provisioning manuale** – scegliere hello [manuale](https://docs.microsoft.com/azure/active-directory/active-directory-enterprise-apps-manage-provisioning#provisioning-modes) modalità di provisioning, se si dispone di account esistenti o si desidera toomanage account per l'applicazione all'esterno di Azure AD.

-   **Provisioning automatico** – scegliere hello [automatica](https://docs.microsoft.com/azure/active-directory/active-directory-enterprise-apps-manage-provisioning#configuring-automatic-user-account-provisioning) **modalità di provisioning** se si desidera tooenable basate su API il provisioning automatico e/o del deprovisioning di toothis degli account utente applicazione 

   >[!NOTE]
   >Questa opzione è disponibile solo per le applicazioni all'interno di hello **in primo piano** categoria di hello [raccolta di applicazioni Azure AD](https://docs.microsoft.com/azure/active-directory/active-directory-enterprise-apps-whats-new-azure-portal#the-new-and-improved-application-gallery).
   >
   >

-   **Il Provisioning automatico basato su SCIM** : utilizzare [il Provisioning automatico basato su SCIM](https://docs.microsoft.com/azure/active-directory/active-directory-scim-provisioning) un'applicazione che supporta il protocollo SCIM hello per il rilevamento delle modifiche toousers e gruppi, che vengono generati automaticamente per le modifiche un'applicazione tooany integrata con Azure AD 

   >[!NOTE]
   >Questa opzione non è elencata come una modalità specifica di provisioning, ma è abilitata per impostazione predefinita per tutte le applicazioni integrate in Azure AD.
   >
   >

## <a name="how-tooset-an-applications-provisioning-mode"></a>Come tooset un'applicazione della modalità di provisioning

del tooset un'applicazione **provisioning** modalità, seguire le istruzioni di hello riportato di seguito:

del tooset un'applicazione **accesso single sign-on** modalità, seguire le istruzioni di hello riportato di seguito:

1.  Aprire hello [ **portale Azure** ](https://portal.azure.com/) e accedere come un **amministratore globale** o **Co-amministratore.**

2.  Aprire hello **estensione di Azure Active Directory** facendo **più servizi** nella parte inferiore di hello del menu di navigazione a sinistra principale hello.

3.  Digitare **"Azure Active Directory**" nella casella di ricerca di filtro hello e seleziona hello **Azure Active Directory** elemento.

4.  Fare clic su **applicazioni aziendali** dal menu di navigazione a sinistra di hello Azure Active Directory.

5.  Fare clic su **tutte le applicazioni** tooview un elenco di tutte le applicazioni.

  * Se non viene visualizzata l'applicazione hello da visualizzare qui, utilizzare hello **filtro** controllo nella parte superiore di hello di hello **elenco di tutte le applicazioni** e set hello **Mostra** opzione troppo **Tutte le applicazioni.**

6.  Selezionare un'applicazione hello per cui si desidera tooconfigure provisioning.

7.  Una volta che un'applicazione hello caricato, fare clic su **Provisioning** dal menu di navigazione a sinistra dell'applicazione hello.

## <a name="next-steps"></a>Passaggi successivi
[Gestione di applicazioni con Azure Active Directory](active-directory-enable-sso-scenario.md)

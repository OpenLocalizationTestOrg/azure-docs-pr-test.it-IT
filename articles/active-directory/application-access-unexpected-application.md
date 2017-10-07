---
title: applicazione aaaUnexpected in un elenco di applicazioni | Documenti Microsoft
description: Come toosee nel tenant di tutte le applicazioni e comprendere come le applicazioni vengono visualizzate nell'elenco di tutte le applicazioni in applicazioni aziendali
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
ms.openlocfilehash: 2f974046b655bc36a05f002c56511a8a988cd01c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="unexpected-application-in-my-applications-list"></a>Applicazione non prevista nell'elenco delle applicazioni

Questo articolo è utile toounderstand modalità di visualizzazione in applicazioni il **tutte le applicazioni** elenco sotto **applicazioni aziendali**. 

## <a name="how-toosee-all-applications-in-your-tenant"></a>Come toosee tutte le applicazioni nel tenant

toosee tutti hello applicazioni nel tenant, è necessario hello toouse **filtro** controllare tooshow **tutte le applicazioni** in hello **tutte le applicazioni** elenco. toodo, questa procedura hello seguire seguente:

1.  Aprire hello [ **portale Azure** ](https://portal.azure.com/) e accedere come un **amministratore globale** o **Co-amministratore.**

2.  Aprire hello **estensione di Azure Active Directory** facendo **più servizi** nella parte inferiore di hello del menu di navigazione a sinistra principale hello.

3.  Digitare **"Azure Active Directory**" nella casella di ricerca di filtro hello e seleziona hello **Azure Active Directory** elemento.

4.  Fare clic su **applicazioni aziendali** dal menu di navigazione a sinistra di hello Azure Active Directory.

5.  Fare clic su **tutte le applicazioni** tooview un elenco di tutte le applicazioni.

6.  Fare clic su hello utilizzare hello **filtro** controllo nella parte superiore di hello di hello **elenco di tutte le applicazioni**.

7.  In hello **filtro** blade, hello set **Mostra** opzione troppo**tutte le applicazioni.**

## <a name="why-does-a-specific-application-appear-in-my-all-applications-list"></a>Perché viene visualizzata un'applicazione specifica nell'elenco di tutte le applicazioni?

Quando filtrata troppo**tutte le applicazioni**, hello **tutte le applicazioni** **elenco** Mostra tutti gli oggetti entità servizio nel tenant. Gli oggetti entità servizio possono essere visualizzati in questo elenco in diversi modi:

1.  Quando si aggiunge un'applicazione dalla raccolta applicazione hello, tra cui:

   1. **Applicazioni della raccolta di Azure AD**: un'applicazione che è già stata integrata per un accesso Single Sign-On con Azure AD.

   2. **Le applicazioni di Proxy applicazione** : un'applicazione in esecuzione nell'ambiente locale che si desidera tooprovide protetta single-sign-on tooexternally.

   3. **Applicazioni sviluppate personalizzato** : hello di un'applicazione che l'organizzazione intende toodevelop nella piattaforma di sviluppo dell'applicazione AD Azure, ma che non esista ancora.

   4. **Applicazioni non incluse nella raccolta**: tutte le altre applicazioni. Qualsiasi collegamento web da o in qualsiasi applicazione che esegue il rendering di un campo di nome utente e password, supporta i protocolli SAML o OpenID Connect o supporti SCIM che si desidera toointegrate per single sign-on con Azure AD.

2.  Quando si effettua l'iscrizione o si esegue l'accesso a un'applicazione di terze parti integrata con Azure Active Directory<sup></sup>, ad esempio [Smartsheet](https://app.smartsheet.com/b/home) o [DocuSign](https://www.docusign.net/member/MemberLogin.aspx).

3.  Quando di iscriversi o aggiunta di un utente di tooa licenza o una gruppo tooa prima parte dell'applicazione, come [Microsoft Office 365](http://products.office.com/).

4.  Quando si aggiunge una nuova registrazione di applicazione tramite la creazione di un'applicazione sviluppata utilizzando hello [Registro di sistema di](https://docs.microsoft.com/azure/active-directory/active-directory-app-registration).

5.  Quando si aggiunge una nuova registrazione di applicazione tramite la creazione di un'applicazione sviluppata utilizzando hello [portale di registrazione applicazione v 2.0](https://docs.microsoft.com/azure/active-directory/develop/active-directory-v2-app-registration#visit-the-microsoft-app-registration-portal).

6.  Quando si aggiunge un'applicazione sviluppata con i [metodi di autenticazione ASP.net](http://www.asp.net/visual-studio/overview/2013/creating-web-projects-in-visual-studio#orgauthoptions) o con i [Servizi connessi](http://blogs.msdn.com/b/visualstudio/archive/2014/11/19/connecting-to-cloud-services.aspx) di Visual Studio .

7.  Quando si crea un oggetto entità servizio utilizzando hello [modulo Azure AD PowerShell](/powershell/azure/install-adv2?view=azureadps-2.0).

8.  Quando si [consenso all'applicazione tooan](https://docs.microsoft.com/azure/active-directory/develop/active-directory-devhowto-multi-tenant-overview#understanding-user-and-admin-consent) come dati toouse amministratore nel tenant.

9.  Quando un [consenso dell'utente, applicazione tooan](https://docs.microsoft.com/azure/active-directory/develop/active-directory-devhowto-multi-tenant-overview#understanding-user-and-admin-consent) toouse dati nel tenant.

10. Quando si abilitano determinati servizi che archiviano dati nel tenant, Un esempio è la reimpostazione della Password, modellata come un toostore dell'entità servizio i criteri di reimpostazione password in modo sicuro.

leggere ulteriori informazioni su come le app vengono aggiunti directory tooyour, tooget [come e perché le applicazioni vengono aggiunte AD tooAzure](https://docs.microsoft.com/azure/active-directory/develop/active-directory-how-applications-are-added).

## <a name="i-want-tooremove-a-specific-users-or-groups-assignment-tooan-application"></a>Voglio tooremove dell'applicazione tooan di assegnazione di un utente specifico o del gruppo

tooremove un'applicazione di tooan assegnazione utente o gruppo, seguire i passaggi di hello elencati in hello [rimuovere l'assegnazione di un utente o gruppo da un'applicazione aziendale in Azure Active Directory](https://docs.microsoft.com/azure/active-directory/active-directory-coreapps-remove-assignment-azure-portal) articolo.

## <a name="i-want-toodisable-all-access-tooan-application-for-every-user"></a>Voglio toodisable tutte le applicazioni di tooan di accesso per ogni utente

toodisable tutti utente accessi tooan dell'applicazione, seguire la procedura seguente hello elencata in hello [disabilitare l'accesso degli utenti per un'applicazione aziendale in Azure Active Directory](https://docs.microsoft.com/azure/active-directory/active-directory-coreapps-disable-app-azure-portal) articolo.

## <a name="i-want-toodelete-an-application-entirely"></a>Voglio toodelete un'applicazione completamente

troppo**eliminare un'applicazione**, seguire le istruzioni di hello seguenti:

1.  Aprire hello [ **portale Azure** ](https://portal.azure.com/) e accedere come un **amministratore globale** o **Co-amministratore.**

2.  Aprire hello **estensione di Azure Active Directory** facendo **più servizi** nella parte inferiore di hello del menu di navigazione a sinistra principale hello.

3.  Digitare **"Azure Active Directory**" nella casella di ricerca di filtro hello e seleziona hello **Azure Active Directory** elemento.

4.  Fare clic su **applicazioni aziendali** dal menu di navigazione a sinistra di hello Azure Active Directory.

5.  Fare clic su **tutte le applicazioni** tooview un elenco di tutte le applicazioni.

  * Se non viene visualizzata l'applicazione hello da visualizzare qui, utilizzare hello **filtro** controllo nella parte superiore di hello di hello **elenco di tutte le applicazioni** e set hello **Mostra** opzione troppo **Tutte le applicazioni.**

6.  Selezionare l'applicazione hello da toodelete.

7.  Una volta che un'applicazione hello caricato, fare clic su **eliminare** icona dell'applicazione principale hello **Panoramica** blade.

## <a name="i-want-toodisable-all-future-user-consent-operations-tooany-application"></a>Voglio toodisable tutti i futuri consenso operazioni tooany dell'applicazione

La disabilitazione di consenso dell'utente per l'intera directory impedire agli utenti finali di consenso tooany applicazione. Gli amministratori possono sempre dare consenso per conto degli utenti. toolearn più sull'applicazione di consenso e motivi per cui è possibile o potrebbe non essere toodo, lettura [consenso dell'amministratore e utente di conoscenza](https://docs.microsoft.com/azure/active-directory/develop/active-directory-devhowto-multi-tenant-overview#understanding-user-and-admin-consent).

troppo**disabilitare tutte le operazioni utente future consenso nella directory intera**, seguire le istruzioni di hello seguenti:

1.  Aprire hello [ **portale Azure** ](https://portal.azure.com/) e accedere come un **amministratore globale.**

2.  Aprire hello **estensione di Azure Active Directory** facendo **più servizi** nella parte inferiore di hello del menu di navigazione a sinistra principale hello.

3.  Digitare **"Azure Active Directory**" nella casella di ricerca di filtro hello e seleziona hello **Azure Active Directory** elemento.

4.  Fare clic su **utenti e gruppi** nel menu di navigazione hello.

5.  Fare clic su **Impostazioni utente**.

6.  Disabilitare tutte le operazioni di consenso utente future impostazione hello **gli utenti possono consentire App tooaccess i propri dati** attivare o disattivare troppo**n** e fare clic su hello **salvare** pulsante.

## <a name="next-steps"></a>Passaggi successivi
[Gestione di applicazioni con Azure Active Directory](active-directory-enable-sso-scenario.md)

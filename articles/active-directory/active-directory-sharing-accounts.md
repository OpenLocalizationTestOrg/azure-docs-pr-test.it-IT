---
title: account aaaSharing mediante Azure AD | Documenti Microsoft
description: Viene descritto come Azure Active Directory consente gli account di condivisione toosecurely organizzazioni per applicazioni locali e i servizi cloud di consumer.
services: active-directory
documentationcenter: 
author: curtand
manager: femila
editor: 
ms.assetid: e2d77104-d978-46a3-bfea-03ffdf3b61e6
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/04/2017
ms.author: curtand
ms.openlocfilehash: 9f98bfa97a6c9ba1566d3f921c1b676d5f3c2a88
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="sharing-accounts-with-azure-ad"></a>Condivisione di account con Azure AD
## <a name="overview"></a>Panoramica
Le organizzazioni richiedono talvolta toouse un singolo nome di utente e password per più persone. Questa situazione si verifica in genere in due casi:

* Quando si accede alle applicazioni che richiedono account di accesso e password univoci per ogni utente, in caso di app locali o servizi cloud di livello consumer (ad esempio, gli account aziendali di social media).
* Quando si creano ambienti multiutente. Potrebbe essere un account locale con privilegi elevati e possono essere utilizzato toodo core il programma di installazione, amministrazione e il ripristino (ad esempio hello locale "" account dell'amministratore globale per Office 365 o hello account radice in Salesforce).

In genere, questi account potrebbero essere condiviso da distribuire singoli destra toohello di hello credenziali (nome utente/password) o conservarli in un percorso condiviso in cui più attendibili gli agenti possano accedervi.

modello di condivisione tradizionale Hello presenta numerosi svantaggi:

* Abilitazione delle applicazioni di accesso toonew richiede toodistribute credenziali tooeveryone che richiede l'accesso.
* Ogni applicazione condiviso potrebbe richiedere un proprio set univoco di credenziali condivise, richiedere agli utenti tooremember più set di credenziali. Quando gli utenti dispongono tooremember molti credenziali, aumenta il rischio di hello che essi verrà utilizzato toorisky consigliate. (ad esempio annotare le password).
* È possibile stabilire chi ha accesso tooan applicazione.
* Non è possibile individuare gli utenti che hanno *effettuato l'accesso* a un'applicazione.
* Quando è necessaria l'applicazione di tooan tooremove accesso, si dispone di credenziali hello tooupdate e distribuirli nuovamente tooeveryone che deve accedere a toothat applicazione.

## <a name="azure-active-directory-account-sharing"></a>Condivisione account di Azure Active Directory
Azure Active Directory fornisce un nuovo approccio account toousing condiviso che consente di eliminare questi svantaggi.

amministratore di Azure AD Hello consente di configurare le applicazioni che un utente può accedere utilizzando hello Pannello di accesso e scegliendo il tipo di hello di single sign-on più adatto per l'applicazione. Uno di questi tipi, *basato su password single sign-in*, consente di agire come un tipo di "gestore" processo hello sign-on per l'app Azure AD.

Gli utenti accedono una volta con l'account aziendale. Si tratta di hello stesso account che si utilizza regolarmente tooaccess desktop o posta elettronica. Possono individuare e accedere solo alle applicazioni a cui sono assegnati. Con gli account condivisi, questo elenco di applicazioni può includere qualsiasi numero di credenziali condivise. utente finale di Hello non necessario tooremember o annotare hello vari account che utilizzano.

Gli account condivisi non solo consentono di aumentare la supervisione e migliorare l'usabilità, ma anche di aumentare la sicurezza. Gli utenti con autorizzazioni toouse hello credenziali non vengono visualizzate password condivisa hello, ma piuttosto ottenere password hello toouse di autorizzazione come parte di un flusso di autenticazione orchestrato. Inoltre, con alcune applicazioni SSO password, è necessario toohave opzione hello Azure AD periodicamente password hello rollover (aggiornamento) utilizzo di password complesse di grandi dimensioni, l'aumento di sicurezza dell'account hello. messaggio per l'amministratore può facilmente concedere o revocare l'accesso tooan applicazione e anche sapere chi ha accesso toohello account e chi lo ha aperto in hello precedente.

Azure AD supporta gli account condivisi per gli utenti con licenza Enterprise Mobility Suite (EMS), Premium o Basic, in tutti i tipi di applicazioni con accesso Single Sign-On basato su password. È possibile condividere gli account per le migliaia di applicazioni già integrate nella raccolta di applicazione hello e aggiungere l'applicazione con l'autenticazione di password con [App SSO personalizzate](active-directory-sso-integrate-saas-apps.md).

Le funzionalità di Azure AD che consentono la condivisione di account includono:

* [Password Single Sign-On](active-directory-appssoaccess-whatis.md#password-based-single-sign-on)
* Agente di password Single Sign-On
* [Assegnazione di gruppi](active-directory-accessmanagement-self-service-group-management.md)
* App personalizzate basate su password
* [Dashboard/report sull'utilizzo di app](active-directory-passwords-get-insights.md)
* Portali di accesso dell'utente finale
* [Proxy di app](active-directory-application-proxy-get-started.md)
* [Marketplace di Active Directory](https://azure.microsoft.com/marketplace/active-directory/all/)

## <a name="sharing-an-account"></a>Condivisione di un account
tooshare toouse Azure AD un account è necessario:

* Aggiungere un'applicazione alla [raccolta di app](https://azure.microsoft.com/marketplace/active-directory/) o integrarla con un'[applicazione personalizzata](http://blogs.technet.com/b/ad/archive/2015/06/17/bring-your-own-app-with-azure-ad-self-service-saml-configuration-gt-now-in-preview.aspx)
* Configurare un'applicazione hello password Single Sign-On (SSO)
* Utilizzare [assegnazione basata su gruppo](active-directory-accessmanagement-group-saasapps.md) e selezionare hello tooenter opzione credenziali condivise
* Facoltativo: in alcune applicazioni, ad esempio Facebook, Twitter e LinkedIn, è possibile abilitare opzione hello per [Azure AD automatizzata ribaltamento password](http://blogs.technet.com/b/ad/archive/2015/02/20/azure-ad-automated-password-roll-over-for-facebook-twitter-and-linkedin-now-in-preview.aspx)

È inoltre possibile rendere l'account condiviso più sicura con multi-Factor Authentication (MFA) (altre informazioni, vedere [la protezione delle applicazioni con Azure AD](../multi-factor-authentication/multi-factor-authentication-get-started.md)) ed è possibile delegare toomanage possibilità hello che dispone di accesso toohello applicazione mediante [Self-Service di azure AD](active-directory-accessmanagement-self-service-group-management.md) gestione gruppo.

## <a name="related-articles"></a>Articoli correlati
* [Indice di articoli per la gestione di applicazioni in Azure Active Directory](active-directory-apps-index.md)
* [Sicurezza delle app con l'accesso condizionale](active-directory-conditional-access.md)
* [Gestione di gruppi self-service/SSAA](active-directory-accessmanagement-self-service-group-management.md)


---
title: App tooon locale di accesso aaaConditional - Azure AD | Documenti Microsoft
description: "Descrive come tooset di accesso condizionale per le applicazioni pubblicate toobe accedere in modalità remota tramite Proxy di applicazione di Azure AD."
services: active-directory
documentationcenter: 
author: kgremban
manager: femila
ms.assetid: 2e97722b-eb4e-4078-b607-9fed210d8a0f
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/23/2017
ms.author: kgremban
ms.reviewer: harshja
ms.custom: it-pro; oldportal
ms.openlocfilehash: 7bed25dd4ba17941e77d8c4b2b9ba4edcf0cf597
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="working-with-conditional-access-in-azure-ad-application-proxy"></a>Uso dell'accesso condizionale nel proxy applicazione di Azure AD

>[!NOTE]
>Questo articolo riguarda toohello portale di Azure classico, in cui è stata ritirata. È consigliabile usare hello [portale di Azure](https://portal.azure.com). Nel portale di Azure hello, Proxy di applicazione App hanno hello stesse funzionalità di accesso condizionale come qualsiasi altra app SaaS. toolearn ulteriori informazioni sull'accesso condizionale, vedere [iniziare con l'accesso condizionale in Azure Active Directory](active-directory-conditional-access-azure-portal-get-started.md).

È possibile configurare l'accesso tooapplications di accesso condizionale toogrant regole pubblicate con il Proxy di applicazione. Ciò consente di:

* Richiedere l'autenticazione a più fattori per ogni applicazione
* Richiedere l'autenticazione a più fattori solo quando gli utenti non sono al lavoro
* Impedire agli utenti di accedere a un'applicazione hello quando non sono al lavoro

Queste regole possono essere applicati tooall utenti o solo gli utenti toospecific e i gruppi. Per impostazione predefinita la regola hello applica tooall gli utenti con accesso toohello applicazione. Regola di hello tuttavia può essere anche toousers con restrizioni che sono membri di gruppi di sicurezza specificati.  

Quando un utente accede a un'applicazione federata che usa OAuth 2.0, OpenID Connect, SAML o WS-Federation, vengono valutate le regole di accesso. Inoltre, le regole di accesso vengono valutate con OAuth 2.0 e OpenID Connect quando un token di aggiornamento è tooacquire usato un token di accesso.

## <a name="conditional-access-prerequisites"></a>Prerequisiti per l'accesso condizionale
* Sottoscrizione tooAzure Active Directory Premium
* Un tenant di Azure Active Directory federato o gestito
* I tenant federati richiedono l'autenticazione a più fattori  
    ![Richiedere la Multi-Factor Authentication](./media/active-directory-application-proxy-conditional-access/application-proxy-conditional-access.png)

## <a name="configure-per-application-multi-factor-authentication"></a>Configurare l'autenticazione a più fattori per applicazione
1. Accedere come amministratore in hello portale di Azure classico.
2. TooActive Directory scegliere hello directory in cui si desidera tooenable Proxy dell'applicazione.
3. Fare clic su **applicazioni** e scorrere verso il basso toohello **le regole di accesso** sezione. sezione regole di accesso Hello viene visualizzata solo per le applicazioni pubblicate con il Proxy di applicazione che usano l'autenticazione federata.
4. Abilitare la regola hello selezionando **abilitare le regole di accesso** troppo**su**.
5. Specificare hello utenti e gruppi toowhom hello si applicano le regole. Hello utilizzare **Aggiungi gruppo** pulsante tooselect toowhich hello accesso regola si applica a uno o più gruppi. Questa finestra di dialogo può anche essere gruppi utilizzati tooremove selezionato.  Quando le regole di hello sono toogroups tooapply selezionata, le regole di accesso hello vengono applicate solo per gli utenti che appartengono tooone di hello specificato gruppi di sicurezza.  

   * gruppi di sicurezza tooexplicitly escludere dalla regola hello, controllare **tranne** e specificare uno o più gruppi. Gli utenti che sono membri di un gruppo di hello ad eccezione di elenco non sono necessari tooperform autenticazione a più fattori.  
   * Se un utente è stato configurato con funzionalità di autenticazione a più fattori per utente hello, questa impostazione ha la precedenza su hello regole di applicazione multi-factor authentication. Un utente che è stato configurato per l'autenticazione a più fattori per utente è obbligatorio tooperform autenticazione a più fattori anche se è stato escluso dalle regole di autenticazione a più fattori dell'applicazione hello. Altre informazioni su [autenticazione a più fattori e impostazioni per utente](../multi-factor-authentication/multi-factor-authentication.md).
6. Selezionare una regola di accesso hello da tooset:

   * **Richiedere l'autenticazione a più fattori**: gli utenti si applicano le regole di accesso toowhom sono necessari toocomplete multi-factor prima che l'accesso ai hello applicazione toowhich hello regola si applica.
   * **Richiedere l'autenticazione a più fattori quando non al lavoro**: gli utenti che tentano di un'applicazione hello tooaccess da un indirizzo IP attendibile non sarà necessario tooperform autenticazione a più fattori. Hello attendibili gli intervalli di indirizzi IP possono essere configurati nella pagina Impostazioni di autenticazione a più fattori hello.
   * **Bloccare l'accesso quando non al lavoro**: gli utenti che tentano di un'applicazione hello tooaccess dall'esterno della rete aziendale non sarà in grado di tooaccess un'applicazione hello.

## <a name="configuring-mfa-for-federation-services"></a>Configurazione di autenticazione a più fattori per servizi di federazione
Per i tenant federati, multi-factor authentication (MFA) può essere eseguita da Azure Active Directory o da hello server ADFS locale. Per impostazione predefinita, l'autenticazione a più fattori viene eseguita in qualsiasi pagina ospitata da Azure Active Directory. tooconfigure autenticazione a più fattori in locale, eseguire Windows PowerShell e usare hello-SupportsMFA proprietà tooset hello modulo di Azure AD.

Hello esempio seguente viene illustrato come tooenable locale autenticazione a più fattori tramite hello [cmdlet Set-MsolDomainFederationSettings](https://msdn.microsoft.com/library/azure/dn194088.aspx) nel tenant contoso.com hello:`Set-MsolDomainFederationSettings -DomainName contoso.com -SupportsMFA $true `

In aggiunta toosetting questo flag, hello tenant federato AD FS istanza deve essere configurato tooperform multi-factor authentication. Seguire le istruzioni di hello per [la distribuzione di Microsoft Azure multi-factor authentication locale](../multi-factor-authentication/multi-factor-authentication-get-started-server.md).

## <a name="see-also"></a>Vedere anche
* [Lavorare con applicazioni grado di riconoscere attestazioni](active-directory-application-proxy-claims-aware-apps.md)
* [Pubblicare le applicazioni con il proxy di applicazione](active-directory-application-proxy-publish.md)
* [Abilitare l'accesso Single Sign-On](active-directory-application-proxy-sso-using-kcd.md)
* [Pubblicare applicazioni mediante il proprio nome di dominio](active-directory-application-proxy-custom-domains.md)

Per informazioni più recenti hello e gli aggiornamenti, consultare hello [blog del Proxy dell'applicazione](http://blogs.technet.com/b/applicationproxyblog/)

---
title: 'Azure AD Connect: Autenticazione pass-through - Domande frequenti | Microsoft Docs'
description: Domande frequenti su Azure Active Directory pass-through Authentication toofrequently di risposte.
services: active-directory
keywords: Autenticazione pass-through di Azure AD Connect, installare Active Directory, componenti necessari per Azure AD, SSO, Single Sign-On
documentationcenter: 
author: swkrish
manager: femila
ms.assetid: 9f994aca-6088-40f5-b2cc-c753a4f41da7
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/03/2017
ms.author: billmath
ms.openlocfilehash: 550e2599177682f8ea971a05485dd5ac12b9b072
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="azure-active-directory-pass-through-authentication-frequently-asked-questions"></a>Autenticazione pass-through di Azure Active Directory: domande frequenti

Questo articolo risponde ad alcune domande frequenti relative all'autenticazione pass-through di Azure Active Directory (Azure AD). Visitare questa pagina regolarmente per nuovi contenuti.

>[!IMPORTANT]
>funzionalità di autenticazione pass-through Hello è attualmente in anteprima.

## <a name="which-of-hello-azure-ad-sign-in-methods---pass-through-authentication-password-hash-synchronization-and-active-directory-federation-services-ad-fs---should-i-choose"></a>Quali hello Azure AD metodi di accesso - autenticazione pass-through, la sincronizzazione dell'Hash Password e Active Directory Federation Services (ADFS), è consigliabile scegliere?

Dipende dall'ambiente locale e dai requisiti dell'organizzazione. Questo articolo per esaminare un [hello di confronto tra vari metodi di Azure AD](active-directory-aadconnect-user-signin.md).

## <a name="is-pass-through-authentication-a-free-feature"></a>L'autenticazione pass-through è una funzionalità gratuita?

L'autenticazione pass-through è una funzionalità disponibile gratuitamente e non è necessario qualsiasi edizione a pagamento di Azure AD toouse è. Rimane disponibile quando la funzionalità hello raggiunge disponibilità generale.

## <a name="is-pass-through-authentication-available-in-microsoft-cloud-germanyhttpwwwmicrosoftdecloud-deutschland-and-microsoft-azure-government-cloudhttpsazuremicrosoftcomfeaturesgov"></a>L'autenticazione pass-through è disponibile in [Microsoft Cloud per la Germania](http://www.microsoft.de/cloud-deutschland) e [Microsoft Azure Government Cloud](https://azure.microsoft.com/features/gov/)?

No, l'autenticazione pass-through è disponibile solo nell'istanza di hello world wide di Azure Active Directory.

## <a name="does-conditional-accessactive-directory-conditional-accessmd-work-with-pass-through-authentication"></a>L'[accesso condizionale](../active-directory-conditional-access.md) funziona con l'autenticazione pass-through?

Sì, tutte le funzionalità di accesso condizionale, incluso Azure Multi-Factor Authentication, funzionano con l'autenticazione pass-through.

## <a name="does-pass-through-authentication-support-alternate-id-as-hello-username-instead-of-userprincipalname"></a>L'autenticazione pass-through supporta "ID alternativo" come nome utente di hello, anziché "userPrincipalName"?

Sì. Supporta l'autenticazione pass-through `Alternate ID` come nome utente quando è configurato in Azure AD Connect, come indicato di hello [qui](active-directory-aadconnect-get-started-custom.md). Non tutte le applicazioni di Office 365 supportano `Alternate ID`. Consultare la documentazione dell'applicazione di toohello specifico per l'istruzione di supporto hello.

## <a name="does-password-hash-synchronization-act-as-a-fallback-toopass-through-authentication"></a>Sincronizzazione dell'Hash Password fungono un'autenticazione fallback tooPass-through?

No, la sincronizzazione dell'Hash Password non è un generico tooPass-tramite l'autenticazione di fallback. Agisce da fallback solo in [scenari che l'autenticazione pass-through attualmente non supporta](active-directory-aadconnect-pass-through-authentication-current-limitations.md#unsupported-scenarios). tooavoid utente errori di accesso, è necessario configurare l'autenticazione pass-through per [la disponibilità elevata](active-directory-aadconnect-pass-through-authentication-quick-start.md#step-5-ensure-high-availability).

## <a name="can-i-install-an-azure-ad-application-proxyactive-directory-application-proxy-get-startedmd-connector-on-hello-same-server-as-a-pass-through-authentication-agent"></a>È possibile installare un [Proxy dell'applicazione AD Azure](../active-directory-application-proxy-get-started.md) connettore hello nello stesso server di un agente autenticazione pass-through?

Sì, questa configurazione è supportata con hello re-branding di versioni di hello agente autenticazione pass-through (versioni 1.5.193.0 o versione successiva).

## <a name="what-versions-of-azure-ad-connect-and-pass-through-authentication-agent-do-you-need"></a>Quali versioni di Azure AD Connect e dell'agente di autenticazione pass-through sono necessarie?

È necessario versione 1.1.486.0 o versioni successive per Azure AD Connect e 1.5.58.0 o versione successiva per hello agente autenticazione pass-through per toowork questa funzionalità. Tutto il software deve essere installato in server con Windows Server 2012 R2 o versioni successive.

## <a name="what-happens-if-my-users-password-has-expired-and-they-try-toosign-in-using-pass-through-authentication"></a>Cosa succede se la password dell'utente è scaduta e provare toosign utilizzando l'autenticazione pass-through?

Se è stato configurato [writeback delle password](../active-directory-passwords-update-your-own-password.md) per un utente specifico, e se hello utente accede utilizzando l'autenticazione pass-through, possono modificare o reimpostare la password. le password Hello vengono scritte tooon locale di Active Directory come previsto.

Tuttavia, se il writeback delle password non è configurato per un utente specifico o se hello utente non dispone di un annuncio di Azure valido, assegnata una licenza utente hello non è possibile aggiornare la password nel cloud hello. neanche se la password è scaduta. utente Hello invece vede il messaggio: "l'organizzazione non consente tooupdate la password in questo sito. Aggiornare il secondo metodo toohello consigliato dall'organizzazione, o chiedere all'amministratore per assistenza." utente Hello o un messaggio per l'amministratore ha tooreset la propria password in Active Directory locale.

## <a name="how-does-pass-through-authentication-protect-you-against-brute-force-password-attacks"></a>La modalità autenticazione pass-through è una protezione dagli attacchi di forza bruta alle password?

Per maggiori informazioni, leggere [questo articolo](active-directory-aadconnect-pass-through-authentication-smart-lockout.md).

## <a name="what-do-pass-through-authentication-agents-communicate-over-ports-80-and-443"></a>Cosa comunicano gli agenti di autenticazione pass-through sulle porte 80 e 443?

- gli agenti di autenticazione Hello verificare le richieste HTTPS sulla porta 443 per tutte le operazioni di funzionalità.
- gli agenti di autenticazione Hello effettuare richieste HTTP sulla porta 80 toodownload SSL gli elenchi di revoche.

     >[!NOTE]
     >Aggiornamenti recenti è hello numero ridotto di porte richiesti dalla funzionalità hello. Se si dispone di versioni precedenti di Azure AD Connect o hello agente Authentication, tenere anche aperte tali porte: 5671, 8080, 9090, 9091, 9350, 9352 e 10100 10120.

## <a name="can-hello-pass-through-authentication-agents-communicate-over-an-outbound-web-proxy-server"></a>Gli agenti di autenticazione pass-through hello possono comunicare su un server proxy web in uscita?

Sì. Se WPAD (Web Proxy Auto-Discovery) è abilitata nell'ambiente locale, gli agenti di autenticazione automaticamente tenta toolocate e utilizzare un server proxy web sulla rete hello.

## <a name="can-i-install-two-or-more-pass-through-authentication-agents-on-hello-same-server"></a>È possibile installare due o più agenti di autenticazione pass-through in hello nello stesso server?

No, è possibile installare solo un agente di autenticazione pass-through in un singolo server. Se si vuole tooconfigure autenticazione pass-through per la disponibilità elevata, seguire le istruzioni di hello in questo [articolo](active-directory-aadconnect-pass-through-authentication-quick-start.md#step-5-ensure-high-availability) invece.

## <a name="i-already-use-active-directory-federation-services-ad-fs-for-azure-ad-sign-in-how-do-i-switch-it-toopass-through-authentication"></a>Si usa già Active Directory Federation Services (ADFS) per l'accesso ad AD Azure. Come passare è autenticazione tooPass-through?

Se ADFS è stato configurato come il metodo di accesso tramite procedura guidata di hello Azure AD Connect, modificare il metodo di accesso utente hello tooPass-tramite l'autenticazione. Questa modifica consente l'autenticazione pass-through tenant hello e converte _tutti_ i domini federati nei domini gestiti. Tutte le successive richieste di accesso nel tenant verranno gestite mediante l'autenticazione pass-through. Attualmente, non è supportato in Azure AD Connect toouse una combinazione di AD FS e l'autenticazione pass-through in domini diversi.

Se ADFS è stato configurato come metodo di accesso hello _esterno_ della procedura guidata Connetti hello Azure AD, modificare il metodo di accesso utente hello tooPass-through dell'autenticazione (opzione "Non si configura" hello). Questa modifica consente l'autenticazione pass-through tenant hello. Tuttavia, tutti i domini federati continuano toouse ADFS per l'accesso. Utilizzare PowerShell toomanually convert alcuni o tutti questi federato domini tooManaged domini. Tutte le richieste di accesso nei domini gestiti (_solo_) verranno quindi gestite mediante l'autenticazione pass-through.

>[!IMPORTANT]
>L'autenticazione pass-through non gestisce l'accesso per gli utenti di Active Directory solo cloud.

## <a name="can-i-use-pass-through-authentication-in-a-multi-forest-ad-environment"></a>È possibile usare l'autenticazione pass-through in un ambiente Active Directory a più foreste?

Sì. Gli ambienti a più foreste sono supportati se sono presenti relazioni di trust tra le foreste AD e se il routing del suffisso del nome è configurato correttamente.

## <a name="do-pass-through-authentication-agents-provide-load-balancing-capability"></a>Gli agenti di autenticazione pass-through includono la funzionalità di bilanciamento del carico?

No, l'installazione di più agenti di autenticazione pass-through assicura la [disponibilità elevata](active-directory-aadconnect-pass-through-authentication-quick-start.md#step-5-ensure-high-availability) ma non il bilanciamento del carico. La gestione delle operazioni bulk hello di richieste di accesso hello possono terminare uno o due di hello gli agenti di autenticazione.

Le richieste di convalida di password che gli agenti di autenticazione necessario toohandle hello presentano una struttura semplice. I carichi medio e di punta per la maggior parte dei clienti sono pertanto facilmente gestibili con due o tre agenti di autenticazione in totale.

Si consiglia di installare gli agenti di autenticazione tooyour Chiudi i controller di dominio tooimprove Accedi latenza.

## <a name="can-i-install-hello-first-pass-through-authentication-agent-on-a-server-other-than-hello-one-that-runs-azure-ad-connect"></a>È possibile installare hello agente prima di autenticazione pass-through in un server diverso da hello uno che esegue Azure AD Connect?

No, questo scenario _non_ è supportato.

## <a name="how-many-pass-through-authentication-agents-should-i-install"></a>Quanti agenti di autenticazione pass-through è consigliabile installare?

È consigliabile:

- Installare due o tre agenti di autenticazione in totale. Questa configurazione è sufficiente per la maggior parte dei clienti.
- Installare gli agenti di autenticazione nei controller di dominio (o Chiudi toothem possibile) tooimprove Accedi la latenza.
- Assicurarsi che i server (in cui sono installati gli agenti di autenticazione) vengono aggiunti foresta toohello stesso Active Directory come utenti hello le cui password è necessario convalidare toobe.

>[!NOTE]
>Esiste un limite di sistema di 12 agenti di autenticazione per ogni tenant.

## <a name="how-can-i-disable-pass-through-authentication"></a>Come si disabilita l'autenticazione pass-through?

Eseguire di nuovo hello Azure AD Connect guidata e modificare il metodo di accesso utente hello dal metodo di autenticazione pass-through tooanother. Questa modifica disabilita l'autenticazione pass-through tenant hello e Disinstalla hello agente di autenticazione dal server di hello. È necessario toomanually Disinstalla hello gli agenti di autenticazione da altri server.

## <a name="what-happens-when-i-uninstall-a-pass-through-authentication-agent"></a>Cosa accade quando si disinstalla un agente di autenticazione pass-through?

La disinstallazione di un agente autenticazione pass-through da un server rende toostop accettando le richieste di accesso. Verificare che si dispone di un altro agente di autenticazione in esecuzione prima di eseguire questa operazione, tooavoid interruzione utente accesso al tenant.

## <a name="next-steps"></a>Passaggi successivi
- [**Current limitations**](active-directory-aadconnect-pass-through-authentication-current-limitations.md) (Limitazioni correnti): questa funzionalità è attualmente in anteprima. Informazioni su quali scenari sono supportati e quali non lo sono.
- [**Guida introduttiva**](active-directory-aadconnect-pass-through-authentication-quick-start.md): informazioni per configurare e usare l'autenticazione pass-through di Azure AD.
- [**Approfondimento tecnico**](active-directory-aadconnect-pass-through-authentication-how-it-works.md): informazioni sul funzionamento di questa funzionalità.
- [**Risoluzione dei problemi** ](active-directory-aadconnect-troubleshoot-pass-through-authentication.md) -informazioni su come le problematiche comuni tooresolve con funzionalità hello.
- [**Seamless Single Sign-On di Azure AD**](active-directory-aadconnect-sso.md): altre informazioni su questa funzionalità complementare.
- [**UserVoice**](https://feedback.azure.com/forums/169401-azure-active-directory/category/160611-directory-synchronization-aad-connect): per l'invio di richieste di nuove funzionalità.

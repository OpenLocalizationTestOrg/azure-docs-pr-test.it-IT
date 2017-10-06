---
title: Accesso con privilegi in Azure AD aaaSecuring | Documenti Microsoft
description: Un argomento che spiega hello approcci per proteggere l'accesso con privilegi in Azure, Azure Active Directory e Microsoft Online Services.
services: active-directory
documentationcenter: 
author: kgremban
manager: femila
editor: mwahl
ms.assetid: 235a0ce9-1daf-4433-8f65-9c6afcd64d08
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/16/2017
ms.author: kgremban
ms.custom: pim
ms.openlocfilehash: 694835dc5c41640673dbd996d44b0d1f217220de
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="securing-privileged-access-in-azure-ad"></a>Protezione dell'accesso con privilegi in Azure AD
Con privilegi di sicurezza di accesso è il primo importante passaggio toohelp proteggere risorse di business in un'organizzazione moderna. Gli account con privilegi sono gli account che amministrano e gestiscono i sistemi IT. Dati dell'organizzazione questi account toogain accesso tooan e sistemi di destinazione informatici. toosecure di accesso con privilegi, è necessario isolare gli account hello e sistemi dal rischio di hello di esposti a utenti malintenzionati tooa.

Più utenti stanno iniziando tooget con privilegiata di accesso tramite i servizi cloud. Tra questi, sono inclusi gli amministratori globali di Office 365, gli amministratori delle sottoscrizioni di Azure e gli utenti che dispongono dell'accesso amministrativo alle macchine virtuali o alle app SaaS.

Microsoft consiglia di seguire questa guida di orientamento sulla [protezione dell'accesso con privilegi](https://technet.microsoft.com/library/mt631194.aspx).

Per i clienti che usano Azure Active Directory, Office 365 o altri servizi e applicazioni Microsoft, questi principi si applicano sia se gli account utente sono gestiti e autenticati da Active Directory o Azure Active Directory o meno. Hello nelle sezioni seguenti forniscono altre informazioni sulla protezione dell'accesso con privilegi di Azure AD funzionalità toosupport.

## <a name="azure-multi-factor-authentication"></a>Azure Multi-Factor Authentication
sicurezza di hello tooincrease dell'autenticazione di amministrazione, è consigliabile richiedere la verifica in due passaggi prima di concedere privilegi. Verifica in due passaggi è un metodo di verifica dell'identità dell'utente che richiede l'utilizzo di hello di molto più di un nome utente e una password. Fornisce un secondo livello di sicurezza toouser accessi e le transazioni.

Azure multi-Factor Authentication (MFA) è una soluzione di verifica in due fasi di Microsoft, che consente di proteggere toodata di accesso e le applicazioni rispettando richiesta dell'utente per un semplice processo. Offre un'autenticazione avanzata con una gamma di opzioni di verifica semplici che includono:

- le telefonate
- i messaggi di testo
- le notifiche dell'app per dispositivi mobili
- i codici di verifica dell'app per dispositivi mobili
- Token OATH di terze parti

Per una panoramica del funzionamento di Azure multi-Factor Authentication vedere hello video seguente:

> [!VIDEO https://channel9.msdn.com/Blogs/Azure/Windows-Azure-Multi-Factor-Authentication/player]

Per altre informazioni, vedere [MFA for Office 365 and MFA for Azure](https://blogs.technet.microsoft.com/ad/2014/02/11/mfa-for-office-365-and-mfa-for-azure/) (MFA per Office 365 e MFA per Azure).

## <a name="time-bound-privileges"></a>Privilegi con vincoli di tempo
Per alcune organizzazioni, il numero di utenti assegnati a ruoli con privilegi elevati potrebbe essere ritenuto eccessivo. Un utente potrebbe essere state aggiunte toohello ruolo per una determinata attività, ad esempio toosign iscrizione a un servizio, ma non utilizza i privilegi di frequente in un secondo momento.

tempo di esposizione hello toolower di privilegi e aumentare il livello di visibilità in uso, creare i propri privilegi "just in time" di limite utenti tooonly (JIT), quando sono necessari tooperform un'attività. Per Azure Active Directory e Microsoft Online Services è possibile usare [Azure AD Privileged Identity Management (PIM)](http://aka.ms/AzurePIM).

![Dashboard di PIM][2]

## <a name="attack-detection"></a>Rilevamento degli attacchi
[Azure Active Directory Identity Protection](../active-directory-identityprotection.md) offre una visualizzazione consolidata degli eventi di rischio e delle potenziali vulnerabilità che interessano le identità dell'organizzazione. Basato su eventi di rischio, la protezione dell'identità calcola un livello di rischio utente per ogni utente, consentendo di criteri basati sul rischio tooconfigure tooautomatically proteggere hello identità dell'organizzazione. Questi criteri, insieme ad altri controlli di accesso condizionale fornite da Azure Active Directory ed EMS, automaticamente Blocca utente hello o fornire suggerimenti che includono la reimpostazione della password e l'applicazione multi-factor authentication.

![Azure AD Identity Protection][3]

## <a name="conditional-access"></a>Accesso condizionale
Con il controllo di accesso condizionale, Azure Active Directory verifica specifiche condizioni hello che scelto durante l'autenticazione di un utente, prima di consentire l'accesso tooan applicazione. Quando queste condizioni sono soddisfatte, l'utente di hello è autenticato e accesso toohello applicazione consentita.

![Impostazione delle regole di accesso condizionale con MFA][4]

## <a name="related-articles"></a>Articoli correlati
* Abilitare [Azure Multi-Factor Authentication](../../multi-factor-authentication/multi-factor-authentication-get-started-cloud.md)
* Abilitare [Azure AD Privileged Identity Management](../active-directory-privileged-identity-management-configure.md)
* Abilitare [Azure AD Identity Protection](../active-directory-identityprotection.md)
* Abilitare i [controlli di accesso condizionale](../active-directory-conditional-access.md)

Per ulteriori informazioni sulla creazione di una Guida di orientamento per la sicurezza, vedere sezione "Guida di orientamento e responsabilità del cliente" hello, di hello [Microsoft Cloud Security per Enterprise Architects](http://aka.ms/securecustomer) documento. Per ulteriori informazioni sull'impegno di Microsoft services tooassist con uno qualsiasi di questi argomenti, contattare il rappresentante Microsoft oppure visitare il nostro [pagina riguardanti la sicurezza delle soluzioni](https://www.microsoft.com/en-us/microsoftservices/campaigns/cybersecurity-protection.aspx).

<!--Image references-->
[1]: ../media/active-directory-privileged-identity-management-configure/Search_PIM.png
[2]: ../media/active-directory-privileged-identity-management-configure/PIM_Dash.png
[3]: ../media/active-directory-identityprotection/29.png
[4]: ../media/active-directory-conditional-access/conditionalaccess-saas-apps.png

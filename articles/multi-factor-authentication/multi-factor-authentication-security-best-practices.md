---
title: "aaaSecurity le procedure consigliate per l'autenticazione a più fattori | Documenti Microsoft"
description: Questo documento illustra le procedure consigliate per l'uso di Azure MFA con account Azure
services: multi-factor-authentication
documentationcenter: 
author: kgremban
manager: femila
ms.assetid: 3be7d968-96bb-4320-8701-869fd04a2595
ms.service: multi-factor-authentication
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/15/2017
ms.author: kgremban
ms.reviewer: yossib
ms.custom: it-pro
ms.openlocfilehash: 7f18c2592764878b842d81783b321a05f29ee3d2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="security-best-practices-for-using-azure-multi-factor-authentication-with-azure-ad-accounts"></a>Procedure consigliate sulla sicurezza per usare Azure Multi-Factor Authentication con account Azure AD

Verifica in due passaggi viene scelta hello preferito per la maggior parte delle organizzazioni che desidera tooenhance il processo di autenticazione. Azure Multi-Factor Authentication (MFA) consente alle aziende di soddisfare i requisiti di sicurezza e conformità, offrendo un'esperienza di accesso semplice per gli utenti. Questo articolo descrive alcuni suggerimenti da prendere in considerazione durante la pianificazione per l'adozione di hello di Azure MFA.

## <a name="deploy-azure-mfa-in-hello-cloud"></a>Distribuire Azure MFA nel cloud hello

Esistono due modi tooenable Azure MFA per tutti gli utenti.

* Acquistare licenze per ogni utente (Azure MFA, Azure AD Premium o Enterprise Mobility + Security)
* Creare un provider di Multi-Factor Authentication scegliendo di pagare in base al numero di utenti o di autenticazioni

### <a name="licenses"></a>Licenze
![EMS](./media/multi-factor-authentication-security-best-practices/ems.png)

Se si dispone di licenze Azure AD Premium o Enterprise Mobility + Security, si può già usare Azure MFA. L'organizzazione non richiede agli utenti di tooall funzionalità verifica in due passaggi hello tooextend nulla aggiuntive. È necessario solo un utente tooa licenza tooassign e quindi è possibile attivare autenticazione a più fattori.

Quando si configura multi-Factor Authentication, prendere in considerazione hello suggerimenti seguenti:

* Non creare un provider di Multi-Factor Authentication in base al numero di autenticazioni. Questo perché si rischia di pagare per richieste di verifica provenienti da utenti che dispongono già di licenze.
* Se non si dispone di licenze sufficiente per tutti gli utenti, è possibile creare un resto di hello toocover Provider multi-Factor Authentication per ogni utente dell'organizzazione. 
* Azure AD Connect è un requisito solo se si sincronizza l'ambiente Active Directory locale con una directory di Azure AD. Se si usa una directory di Azure AD non sincronizzata con un'istanza locale di Active Directory, Azure AD Connect non è necessario.

### <a name="multi-factor-auth-provider"></a>Provider di Multi-Factor Authentication
![Provider di Multi-Factor Authentication](./media/multi-factor-authentication-security-best-practices/authprovider.png)

Se non si dispone di licenze che includono Azure MFA, è possibile creare un provider di autenticazione MFA. 

Quando si creano hello Provider di autenticazione, è necessario tooselect una directory e considerare hello seguenti dettagli:

* Non è necessario un toocreate directory Azure AD un Provider multi-Factor Authentication, ma ottenere altre funzionalità con uno. Quando si associa hello Provider di autenticazione a una directory di Azure AD, è attivata Hello seguenti caratteristiche:  
  * Estendere gli utenti di tooall verifica in due passaggi  
  * Offrono funzionalità aggiuntive, ad esempio il portale di gestione di hello, messaggi di saluto personalizzati e i report di consentire agli amministratori globali.
* Se si esegue la sincronizzazione dell'ambiente Active Directory locale con una directory di Azure AD, sono necessarie le funzionalità DirSync o AAD Sync. Se si usa una directory di Azure AD non sincronizzata con un'istanza locale di Active Directory, non sono necessarie le funzionalità DirSync o AAD Sync.
* Scegliere modello consumo hello più appropriata per l'azienda. Dopo aver selezionato il modello di utilizzo di hello, è possibile modificarlo. Hello due modelli sono:
  * Per autenticazione: viene applicato un addebito per ogni verifica. Usare questo modello per usare la verifica in due passaggi per qualsiasi utente che accede a una determinata app, non per utenti specifici.
  * Per utente abilitato: viene applicato un addebito per ogni utente che viene abilitato per Azure MFA. Usare questo modello se non tutti gli utenti dispongono di licenze Azure AD Premium o Enterprise Mobility Suite.

### <a name="supportability"></a>Supporto
Poiché la maggior parte degli utenti sono abituati toousing password solo tooauthenticate, è importante che l'azienda elenca gli utenti tooall su questo processo. Questa consapevolezza può ridurre il rischio di hello che gli utenti chiamare l'help desk per tooMFA correlate a problemi di lieve entità. Esistono tuttavia alcuni scenari in cui è necessario disabilitare temporaneamente MFA. Hello utilizzare seguenti come linee guida toounderstand toohandle questi scenari:

* Eseguire il training gli scenari di toohandle personale di supporto tecnico in cui hello utente non è possibile accedere perché l'app per dispositivi mobili hello o il telefono non riceve una notifica o una telefonata. Il supporto tecnico può [attivare un bypass monouso](multi-factor-authentication-whats-next.md#one-time-bypass) tooallow tooauthenticate un utente una sola volta "ignorando" verifica in due passaggi. Hello bypass è temporaneo e scade dopo un numero di secondi specificato.
* Prendere in considerazione hello [funzionalità indirizzi IP attendibili](multi-factor-authentication-whats-next.md#trusted-ips) in Azure MFA per la verifica in due passaggi toominimize modo. Con questa funzionalità, gli amministratori di un tenant gestito o federato possono ignorare la verifica in due passaggi per gli utenti che accedono dalla rete intranet locale della società hello. Hello funzionalità sono disponibili per i tenant di Azure AD che dispone di licenze di Azure AD Premium, Enterprise Mobility Suite o Azure multi-Factor Authentication.

## <a name="best-practices-for-an-on-premises-deployment"></a>Procedure consigliate per una distribuzione locale
Se la società ha deciso tooleverage proprio tooenable infrastruttura autenticazione a più fattori, è necessario toodeploy un Server Azure multi-Factor Authentication locale. i componenti Server di autenticazione a più fattori di Hello vengono visualizzati nel seguente diagramma hello:

![Componenti predefiniti di un server MFA: console, motore di sincronizzazione, portale di gestione, servizio cloud](./media/multi-factor-authentication-security-best-practices/server.png) \*Non installato per impostazione predefinita \**Installato ma non abilitato per impostazione predefinita

Il server Azure Multi-Factor Authentication può proteggere le risorse del cloud e locali usando la federazione. È necessario avere AD FS federato con un tenant di Azure AD.
Quando si configurano i Server multi-Factor Authentication, prendere in considerazione hello seguenti dettagli:

* Se si desidera proteggere le risorse di Azure AD utilizzando Active Directory Federation Services (ADFS), il primo passaggio di verifica hello viene eseguita in locale con ADFS. secondo passaggio Hello viene eseguito localmente rispettando l'attestazione hello.
* Non è necessario tooinstall hello del Server Azure multi-Factor Authentication server federativo AD FS. Tuttavia, è necessario installare hello adapter per l'autenticazione a più fattori per AD FS in Windows Server 2012 R2 che esegue AD FS. È possibile installare server hello in un computer diverso, purché si tratta di una versione supportata e installa scheda ADFS hello AD separatamente nel server federativo AD FS. 
* procedura guidata di installazione scheda ADFS di multi-Factor Authentication Hello Crea gruppo di sicurezza PhoneFactor Admins in Active Directory e quindi aggiunge il gruppo di toothis account del servizio ADFS. Verificare che hello gruppo PhoneFactor Admins è stato creato nel controller di dominio e account del servizio che hello AD FS è un membro di questo gruppo. Se necessario, aggiungere toohello account di servizio AD FS hello gruppo PhoneFactor Admins manualmente nel controller di dominio.

### <a name="user-portal"></a>Portale per gli utenti
portale per gli utenti Hello consente funzionalità self-service e fornisce un set completo di funzionalità di amministrazione di utente. Viene eseguito in un sito web di Internet Information Server (IIS). Utilizzare questo componente di hello tooconfigure linee guida seguenti:

* Usare IIS 6 o versione successiva
* Installare e registrare ASP.NET v2.0.507207
* Assicurarsi che il server possa essere distribuito in una rete perimetrale

### <a name="app-passwords"></a>Password dell'app
Se l'organizzazione è federata per SSO con Azure AD e si sta usando Azure MFA toobe, quindi tenere hello seguenti dettagli:

* password dell'app Hello viene verificata da Azure AD e pertanto ignora la federazione. La federazione viene usata solo quando si configura la password dell'app.
* Per gli utenti federati (SSO), le password vengono archiviate nell'id organizzativo hello. Se l'utente hello lascia la società hello, tooflow tooorganizational id mediante DirSync tali informazioni. Disabilitazione o eliminazione di account potrebbe richiedere toothree ore toosync, che ritarda disabilitazione o eliminazione di password di app in Azure AD.
* Le impostazioni locali di Controllo dell'accesso Client non vengono rispettate dalla password dell'app.
* Per le password dell'app non è disponibile alcuna funzionalità di registrazione o controllo dell'autenticazione in locale.
* Alcune architetture avanzate possono richiedere una combinazione di nome utente e password dell'organizzazione e password dell'app quando si usa la verifica in due passaggi con i client, a seconda della posizione in cui viene eseguita l'autenticazione. Per i client che si autenticano con un'infrastruttura locale, verranno usati un nome utente e una password dell'organizzazione. Per i client che eseguono l'autenticazione con Azure AD, utilizzare una password di app hello.
* Per impostazione predefinita, gli utenti non possono creare password dell'app. Se sono necessarie password di app tooallow utenti toocreate, selezionare hello **consentono agli utenti toocreate app password toosign in applicazioni diverse dai browser** opzione.

## <a name="additional-considerations"></a>Considerazione aggiuntive
Usare questo elenco per leggere alcune considerazioni e procedure consigliate aggiuntive per ogni componente che viene distribuito in locale:

- Configurare Azure Multi-Factor Authentication con [Active Directory Federation Service](multi-factor-authentication-get-started-adfs.md).
- Installare e configurare Azure MFA Server con hello [l'autenticazione RADIUS](multi-factor-authentication-get-started-server-radius.md).
- Installare e configurare Azure MFA Server con hello [autenticazione IIS](multi-factor-authentication-get-started-server-iis.md).
- Installare e configurare Azure MFA Server con hello [l'autenticazione di Windows](multi-factor-authentication-get-started-server-windows.md).
- Installare e configurare Azure MFA Server con hello [autenticazione LDAP](multi-factor-authentication-get-started-server-ldap.md).
- Installare e configurare Azure MFA Server con hello [Gateway Desktop remoto e il Server Azure multi-Factor Authentication tramite RADIUS](multi-factor-authentication-get-started-server-rdg.md).
- Installare e configurare la sincronizzazione tra hello Azure MFA Server e [Windows Server Active Directory](multi-factor-authentication-get-started-server-dirint.md).
- [Distribuire hello Azure multi-Factor Authentication Server servizio Web App Mobile](multi-factor-authentication-get-started-server-webservice.md).
- [Configurazione VPN avanzata con Azure Multi-Factor Authentication](multi-factor-authentication-advanced-vpn-configurations.md) per appliance Cisco ASA, Citrix Netscaler e Juniper/Pulse Secure VPN con LDAP o RADIUS.

## <a name="next-steps"></a>Passaggi successivi
Anche se questo articolo evidenzia alcune procedure consigliate per Azure MFA, sono disponibili anche altre risorse che è possibile usare quando si pianifica la distribuzione di MFA. elenco Hello seguente presenta alcuni articoli chiavi che possono fornire assistenza durante questo processo:

* [Report in Azure Multi-Factor Authentication](multi-factor-authentication-manage-reports.md)
* [esperienza di registrazione di verifica in due passaggi Hello](multi-factor-authentication-end-user-first-time.md)
* [Domande frequenti su Azure Multi-Factor Authentication](multi-factor-authentication-faq.md)


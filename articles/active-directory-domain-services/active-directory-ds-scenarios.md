---
title: 'Servizi di dominio Azure Active Directory: Scenari di distribuzione | Microsoft Docs'
description: Scenari di distribuzione per i Servizi di dominio Azure Active Directory
services: active-directory-ds
documentationcenter: 
author: mahesh-unnikrishnan
manager: stevenpo
editor: curtand
ms.assetid: c5216ec9-4c4f-4b7e-830b-9d70cf176b20
ms.service: active-directory-ds
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/23/2017
ms.author: maheshu
ms.openlocfilehash: 8a64bd8f7c6eba8f6490e10fa62bef195b6b3d5f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="deployment-scenarios-and-use-cases"></a>Scenari di distribuzione e casi d'uso
Questa sezione illustra alcuni scenari e casi d'uso che traggono vantaggio dall'utilizzo di Servizi di dominio Azure Active Directory (AD).

## <a name="secure-easy-administration-of-azure-virtual-machines"></a>Gestione sicura e semplificata delle macchine virtuali di Azure
È possibile utilizzare Azure Active Directory Domain Services toomanage macchine virtuali di Azure in modo ottimizzato. Macchine virtuali di Azure può essere toohello aggiunti a un dominio gestito, consentendo in questo toouse toolog in credenziali di Active Directory aziendale. Questo approccio consente di evitare complicazioni con la gestione delle credenziali, ad esempio la gestione degli account di amministratore locali su ciascuna delle macchine virtuali di Azure.

Macchine virtuali di server di dominio gestiti toohello unita in join può anche essere gestite e protette tramite i criteri di gruppo. È possibile applicare le linee di base di sicurezza necessarie tooyour virtuali di Azure macchine e bloccare in base alle linee guida di sicurezza aziendali. Ad esempio, è possibile utilizzare i tipi di hello toorestrict per la funzionalità Gestione gruppo criteri delle applicazioni che possono essere avviate in tali macchine virtuali.

![Gestione ottimizzata delle macchine virtuali di Azure](./media/active-directory-domain-services-scenarios/streamlined-vm-administration.png)

Come server e un'altra infrastruttura raggiunta fine del ciclo di vita, Contoso è lo spostamento di molte applicazioni ospitate nel cloud toohello locale. Lo standard IT corrente prevede che i server che ospitano applicazioni aziendali sia aggiunto a un dominio e gestito tramite Criteri di gruppo. Contoso amministratore IT si preferisce toodomain join le macchine virtuali distribuite in Azure, amministrazione toomake più semplice. Di conseguenza, gli amministratori e gli utenti possono accedere utilizzando le proprie credenziali aziendali. In hello stesso tempo, le macchine possono essere configurati toocomply con linee di base di sicurezza necessarie tramite criteri di gruppo. Contoso desidera non toohave toodeploy, monitorare e gestire i controller di dominio in Azure toosecure macchine virtuali di Azure. Servizi di dominio Azure Active Directory è quindi un'ottima soluzione per questo caso di utilizzo.

**Note sulla distribuzione**

Prendere in considerazione hello seguenti punti importanti per questo scenario di distribuzione:

* Per impostazione predefinita, i domini gestiti forniti da Servizi di dominio Azure AD offrono una singola struttura di unità organizzativa di tipo semplice. Tutte le macchine aggiunte al dominio si trovano in una singola unità organizzativa di tipo semplice. È tuttavia possibile scegliere toocreate unità organizzative personalizzate.
* Servizi di dominio Active Directory di Azure supporta semplice i criteri di gruppo nel modulo hello un predefinito dell'oggetto Criteri di ogni per hello utenti e computer di contenitori. È possibile creare oggetti Criteri di gruppo personalizzati e usarli come destinazione le unità organizzative toocustom.
* Servizi di dominio Active Directory di Azure supporta schema oggetto computer hello base Active Directory. È possibile estendere lo schema dell'oggetto computer hello.

## <a name="lift-and-shift-an-on-premises-application-that-uses-ldap-bind-authentication-tooazure-infrastructure-services"></a>Accuratezza di spostamento e un'applicazione locale che utilizza tooAzure l'autenticazione di binding LDAP servizi di infrastruttura
![Binding LDAP](./media/active-directory-domain-services-scenarios/ldap-bind.png)

Contoso ha un'applicazione locale acquistata da un fornitore di software indipendente molti anni fa. un'applicazione Hello è attualmente in modalità manutenzione per hello ISV e applicazione richiedente toohello di modifiche viene impedito perché costoso per Contoso. L'applicazione è un basata sul web front-end che raccoglie le credenziali utente tramite un modulo web ed eseguendo un toohello di binding LDAP autentica gli utenti aziendali di Active Directory. Contoso desidera toomigrate questo tooAzure applicazione Servizi di infrastruttura. È consigliabile che l'applicazione hello funziona così com'è, senza richiedere alcuna modifica. Inoltre, gli utenti devono essere in grado di tooauthenticate utilizzando le credenziali aziendali esistenti e senza con operazioni di toodo tooretrain gli utenti in modo diverso. In altre parole, gli utenti finali devono essere ignorando di in cui è in esecuzione un'applicazione hello e migrazione hello deve essere toothem trasparente.

**Note sulla distribuzione**

Prendere in considerazione hello seguenti punti importanti per questo scenario di distribuzione:

* Verificare che un'applicazione hello non è necessario directory toohello toomodify/scrittura. Domini toomanaged di accesso in scrittura LDAP forniti da servizi di dominio Azure Active Directory non è supportata.
* È possibile modificare le password direttamente a fronte di dominio gestiti hello. Gli utenti finali possono modificare la password utente utilizzando meccanismo di modifica della password self-service di Azure AD o in una directory locale hello. Queste modifiche vengono automaticamente sincronizzati e disponibile nel dominio gestito hello.

## <a name="lift-and-shift-an-on-premises-application-that-uses-ldap-read-tooaccess-hello-directory-tooazure-infrastructure-services"></a>Lettura di un'applicazione locale che utilizza il protocollo LDAP accuratezza e MAIUSC tooaccess hello directory tooAzure servizi di infrastruttura
Contoso ha un'applicazione line-of-business locale (LOB) che è stata sviluppata quasi un decennio fa. Questa applicazione è compatibile con directory ed è stato progettato toowork con Windows Server Active Directory. un'applicazione Hello utilizza LDAP (Lightweight Directory Access Protocol) tooread informazioni o gli attributi relativi agli utenti da Active Directory. un'applicazione Hello non modificare gli attributi o scrivere in caso contrario toohello directory. Contoso desidera toomigrate questo tooAzure applicazione Servizi di infrastruttura e ritirare l'hardware locale di durata hello ospita questa applicazione. un'applicazione Hello non può essere riscritto toouse moderna directory API, ad esempio hello basato su REST API Azure AD Graph. Pertanto, un'opzione di accuratezza e MAIUSC desiderata con un'applicazione hello può essere migrati toorun nel cloud hello, senza modificare il codice o riscrivere l'applicazione hello.

**Note sulla distribuzione**

Prendere in considerazione hello seguenti punti importanti per questo scenario di distribuzione:

* Verificare che un'applicazione hello non è necessario directory toohello toomodify/scrittura. Domini toomanaged di accesso in scrittura LDAP forniti da servizi di dominio Azure Active Directory non è supportata.
* Verificare che un'applicazione hello non è necessario uno schema di Active Directory esteso personalizzato. Le estensioni dello schema non sono supportate in Servizi di dominio Azure AD.

## <a name="migrate-an-on-premises-service-or-daemon-application-tooazure-infrastructure-services"></a>Eseguire la migrazione di un locale del servizio o daemon applicazione tooAzure servizi di infrastruttura
Alcune applicazioni sono costituiti da più livelli, in cui uno dei livelli di hello deve tooperform chiamate autenticate tooa back-end livello, ad esempio un livello di database. Gli account di servizio di Active Directory vengono comunemente utilizzati per questi casi di utilizzo. È possibile accuratezza e MAIUSC, ad esempio applicazioni tooAzure servizi di infrastruttura e utilizzare servizi di dominio di Azure AD per esigenze di identità hello di queste applicazioni. È possibile scegliere toouse hello stesso account del servizio che vengono sincronizzati dal tooAzure di directory Active Directory locale. In alternativa, è possibile creare un'unità Organizzativa e quindi creare un account del servizio distinto nell'unità Organizzativa, toodeploy tali applicazioni.

![Account del servizio mediante WIA](./media/active-directory-domain-services-scenarios/wia-service-account.png)

Contoso ha un'applicazione di insieme di credenziali appositamente sviluppata e personalizzata che include un front-end Web, un server SQL e un server FTP back-end. L'autenticazione integrata di Windows dell'account del servizio è il server FTP toohello front-end di tooauthenticate utilizzati hello web. front-end web Hello impostare toorun come account del servizio. Hello server back-end è configurato l'accesso dall'account di servizio hello tooauthorize per front-end web hello. Contoso preferisce non toohave toodeploy una macchina virtuale controller di dominio in hello cloud toomove questo tooAzure applicazione Servizi di infrastruttura. Contoso amministratore IT può distribuire hello che ospitano macchine virtuali di hello FTP server tooAzure front-end web hello e SQL server. Questi computer sono unite in join tooan servizi di dominio Active Directory di Azure gestita dominio. Quindi, utilizzano hello stesso account del servizio nella directory locale per scopi di autenticazione dell'applicazione hello. Questo account di servizio è sincronizzata toohello dominio gestito di servizi di dominio Active Directory di Azure ed è disponibile per l'utilizzo.

**Note sulla distribuzione**

Prendere in considerazione hello seguenti punti importanti per questo scenario di distribuzione:

* Verificare che l'applicazione hello Usa nome utente/password per l'autenticazione. L'autenticazione basata su certificati/smart card non è supportata da Servizi di dominio Azure AD.
* È possibile modificare le password direttamente a fronte di dominio gestiti hello. Gli utenti finali possono modificare la password utente utilizzando meccanismo di modifica della password self-service di Azure AD o in una directory locale hello. Queste modifiche vengono automaticamente sincronizzati e disponibile nel dominio gestito hello.

## <a name="windows-server-remote-desktop-services-deployments-in-azure"></a>Distribuzioni di Servizi Desktop remoto di Windows Server in Azure
È possibile utilizzare servizi di dominio Active Directory di Azure tooprovide gestiti AD tooyour desktop remoti distribuiti in Azure di servizi di dominio.

Per ulteriori informazioni su questo scenario di distribuzione, vedere come troppo[integrare servizi di dominio Active Directory di Azure con la distribuzione di servizi desktop remoto](https://docs.microsoft.com/windows-server/remote/remote-desktop-services/rds-azure-adds).

---
title: aaaAzure Panoramica di monitoraggio e gestione della sicurezza | Documenti Microsoft
description: " Azure offre tooaid meccanismi di sicurezza in hello gestione e monitoraggio di servizi cloud di Azure e macchine virtuali.  Questo articolo offre una panoramica dei servizi e delle funzionalità di sicurezza di base. "
services: security
documentationcenter: na
author: TerryLanfear
manager: StevenPo
editor: TomSh
ms.assetid: 5cf2827b-6cd3-434d-9100-d7411f7ed424
ms.service: security
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 11/21/2016
ms.author: terrylan
ms.openlocfilehash: 0026fa97bab7e15c9f8de6856b5075abe2288f61
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="azure-security-management-and-monitoring-overview"></a>Panoramica su gestione e monitoraggio della sicurezza di Azure
Azure offre tooaid meccanismi di sicurezza in hello gestione e monitoraggio di servizi cloud di Azure e macchine virtuali. Questo articolo offre una panoramica dei servizi e delle funzionalità di sicurezza di base. Vengono forniti tooarticles che forniscono i dettagli di ogni in modo da acquisire più collegamenti.

sicurezza di Hello dei servizi cloud Microsoft è una relazione e condivise con Microsoft. Responsabilità condivisa significa che Microsoft è responsabile di hello Microsoft Azure e la sicurezza fisica dei propri data Center (utilizzando meccanismi di protezione, ad esempio le porte di ingresso badge bloccato, recinti e Guard). Inoltre, Azure fornisce livelli di protezione cloud a livello software hello in grado di soddisfare esigenze di conformità dei propri clienti complesse, privacy e sicurezza hello.

Si è proprietari, i dati e delle identità, responsabilità hello per la protezione di essi, hello sicurezza delle risorse locali e hello sicurezza dei componenti di cloud in cui si dispone di controllo. Microsoft fornisce con toohelp controlli e funzionalità di sicurezza proteggere i dati e le applicazioni. Il livello di responsabilità per la sicurezza è basata sul tipo hello del servizio cloud.

Hello seguente grafico riepiloga saldo hello del responsabile clienti Microsoft e hello.

![Responsabilità condivisa][1]

Per un approfondimento sulla gestione della sicurezza, vedere [Gestione della sicurezza in Azure](azure-security-management.md).

Di seguito sono hello core funzionalità toobe illustrate in questo articolo:

* Controllo degli accessi in base al ruolo
* Antimalware
* Autenticazione a più fattori
* ExpressRoute
* Gateway di rete virtuale
* Privileged Identity Management
* Identity Protection
* Centro sicurezza

## <a name="role-based-access-control"></a>Controllo degli accessi in base al ruolo
Il controllo degli accessi in base al ruolo consente la gestione specifica degli accessi per le risorse di Azure. Usa tale controllo, è possibile concedere agli utenti solo quantità di hello di accesso di cui necessitano di tooperform i processi.  RBAC consentono inoltre di verificare che quando gli utenti lasciano l'organizzazione di hello perdono tooresources access nel cloud hello.

Altre informazioni:

* [Blog del team di Active Directory sul controllo degli accessi in base al ruolo](http://i1.blogs.technet.com/b/ad/archive/2015/10/12/azure-rbac-is-ga.aspx)
* [Controllo degli accessi in base al ruolo di Azure](../active-directory/role-based-access-control-configure.md)

## <a name="antimalware"></a>Antimalware
Con Azure, è possibile utilizzare il software antimalware fornitori principali di sicurezza, ad esempio Microsoft, Symantec, Trend Micro, McAfee e toohelp Kaspersky proteggere le macchine virtuali da file dannosi, adware e altre minacce.

Microsoft Antimalware offre che Hello possibilità tooinstall un agente antimalware per i ruoli PaaS e macchine virtuali. In base a System Center Endpoint Protection, questa funzionalità offre locale si basa sulla collaudata cloud toohello tecnologia di sicurezza.

Integrazione perfetta per della tendenza offre [Deep Security](http://www.trendmicro.com/us/enterprise/cloud-solutions/deep-security/)™ e [SecureCloud](http://www.trendmicro.com/us/enterprise/cloud-solutions/secure-cloud/)™ prodotti hello piattaforma Azure. DeepSecurity è una soluzione antivirus e SecureCloud è una soluzione di crittografia. La soluzione DeepSecurity viene distribuita nelle VM con un modello di estensione. Tramite l'interfaccia utente del portale hello e PowerShell, è possibile scegliere toouse DeepSecurity all'interno di nuove macchine virtuali che sono viene riattivate o le macchine virtuali esistenti che sono già state distribuite.

Anche Symantec Endpoint Protection (SEP) è supportato in Azure. Tramite l'integrazione del portale, i clienti possono specificare che intendono toouse settembre all'interno di una macchina virtuale. SET può essere installato in una nuova macchina virtuale tramite il portale di Azure hello o può essere installato in una macchina virtuale esistente tramite PowerShell.

Altre informazioni:

* [Distribuzione di soluzioni antimalware in macchine virtuali di Azure](https://azure.microsoft.com/blog/deploying-antimalware-solutions-on-azure-virtual-machines/)
* [Microsoft Antimalware per Servizi cloud e Macchine virtuali di Azure](azure-security-antimalware.md)
* [Come tooinstall e configurare Trend Micro Deep Security come servizio in una macchina virtuale Windows](../virtual-machines/windows/classic/install-trend.md)
* [Come tooinstall e configurare Symantec Endpoint Protection in una macchina virtuale Windows](../virtual-machines/windows/classic/install-symantec.md)
* [Nuove opzioni antimalware per la protezione di macchine virtuali di Azure: McAfee Endpoint Protection](https://azure.microsoft.com/blog/new-antimalware-options-for-protecting-azure-virtual-machines/)

## <a name="multi-factor-authentication"></a>Multi-Factor Authentication
Azure multi-factor authentication (MFA) è un metodo di autenticazione che richiede l'uso di hello di più di un metodo di verifica e aggiunge un secondo livello critico di sicurezza toouser accessi e le transazioni. MFA contribuisce a salvaguardare toodata di accesso e le applicazioni rispettando richiesta dell'utente per un semplice processo. Offre autenticazione avanzata tramite diverse opzioni di verifica, ad esempio una telefonata, un SMS, una notifica dell'app per dispositivi mobili o un codice di verifica e token OATH di terze parti.

Altre informazioni:

* [Autenticazione a più fattori](https://azure.microsoft.com/documentation/services/multi-factor-authentication/)
* [Informazioni su Azure Multi-Factor Authentication](../multi-factor-authentication/multi-factor-authentication.md)
* [Come funziona Azure Multi-Factor Authentication](../multi-factor-authentication/multi-factor-authentication-how-it-works.md)

## <a name="expressroute"></a>ExpressRoute
Microsoft Azure ExpressRoute consente di estendere le reti locali nel cloud di Microsoft hello su una connessione privata dedicata mediante un provider di connettività. Con ExpressRoute, è possibile stabilire i servizi cloud di tooMicrosoft connessioni, come Microsoft Azure, Office 365 e CRM Online. La connettività può essere stabilita da una rete (IP VPN) any-to-any, da una rete Ethernet punto a punto o da una Cross Connection virtuale tramite un provider di connettività presso una struttura di condivisione del percorso. Le connessioni ExpressRoute non sfruttano hello rete Internet pubblica. In questo modo toooffer connessioni ExpressRoute più affidabilità, velocità più elevate, minori latenze e una maggiore sicurezza rispetto alle connessioni tramite hello Internet.

Altre informazioni:

* [Panoramica tecnica relativa a ExpressRoute](../expressroute/expressroute-introduction.md)

## <a name="virtual-network-gateways"></a>Gateway di rete virtuale
Gateway VPN, denominato anche gateway di rete virtuale Azure, vengono utilizzati toosend il traffico tra reti virtuali e i percorsi locali. Sono anche utilizzati toosend il traffico tra più reti virtuali in Azure (da-rete).  I gateway VPN offrono connettività cross-premise sicura tra Azure e l'infrastruttura locale.

Altre informazioni:

* [Informazioni sui gateway VPN](../vpn-gateway/vpn-gateway-about-vpngateways.md)
* [Panoramica della sicurezza di rete di Azure](security-network-overview.md)

## <a name="privileged-identity-management"></a>Privileged Identity Management
In alcuni casi gli utenti devono toocarry operazioni privilegiate in risorse di Azure o altre applicazioni SaaS. Questo spesso significa che le organizzazioni possono toogive di accesso con privilegi permanenti usarle in Azure Active Directory (Azure AD). Questo rappresenta un rischio di sicurezza crescente per le risorse ospitate nel cloud poiché le organizzazioni non sono in grado di monitorare completamente le operazioni eseguite dagli utenti con l'accesso con privilegi.
Se un account utente con accesso privilegiato è compromesso, tale singola violazione può inoltre compromettere la sicurezza dell'intero cloud. Azure AD Privileged Identity Management consente tooresolve questo rischio riducendo il tempo di esposizione dei privilegi hello e aumentando visibilità sull'utilizzo.  

Privileged Identity Management è stato introdotto il concetto di hello di un amministratore temporaneo per un ruolo o "just in time" accesso come amministratore, ovvero un utente che necessita di un processo di attivazione per tale ruolo toocomplete. modifiche di processo di attivazione Hello hello assegnazione del ruolo di tooa utente hello in Azure AD da tooactive inattivo, per un periodo di tempo specificato, ad esempio otto ore.

Altre informazioni:

* [Gestione identità con privilegi di Azure AD](../active-directory/active-directory-privileged-identity-management-configure.md)
* [Introduzione ad Azure AD Privileged Identity Management](../active-directory/active-directory-privileged-identity-management-getting-started.md)

## <a name="identity-protection"></a>Identity Protection
La protezione dell'identità di Azure Active Directory (AD) fornisce una visualizzazione consolidata di attività sospette Accedi e potenziali vulnerabilità toohelp proteggere l'azienda. Identity Protection rileva le attività sospette per le identità utente e con privilegi (amministratore), in base a segnali come attacchi di forza bruta, perdita di credenziali e accessi da località ignote e dispositivi infetti.

Fornendo le notifiche e correzione consigliata, la protezione dell'identità consente di rischi toomitigate in tempo reale. Calcola la gravità di utente dei rischi ed è possibile configurare criteri basati sul rischio tooautomatically help misura di protezione accesso all'applicazione da eventuali minacce future.

Altre informazioni:

* [Azure Active Directory Identity Protection](../active-directory/active-directory-identityprotection.md)
* [Channel 9: Azure AD and Identity Show: Identity Protection Preview](https://channel9.msdn.com/Series/Azure-AD-Identity/Azure-AD-and-Identity-Show-Identity-Protection-Preview)

## <a name="security-center"></a>Centro sicurezza
Centro sicurezza di Azure consente di impedire, rilevare e rispondere toothreats e fornisce che maggiore visibilità e controllare i sicurezza hello delle risorse di Azure. Offre funzionalità integrate di monitoraggio della sicurezza e gestione dei criteri tra le sottoscrizioni di Azure, facilita il rilevamento delle minacce che altrimenti passerebbero inosservate e funziona con un ampio ecosistema di soluzioni di sicurezza.

Centro sicurezza PC consente di ottimizzare e sicurezza hello di risorse di Azure da monitorare:

* Sicurezza della società consentendo toodefine criteri per le risorse di sottoscrizione di Azure in base tooyour deve e hello il tipo di applicazioni o riservatezza dei dati di hello in ogni sottoscrizione.
* Monitoraggio stato hello di macchine virtuali di Azure, la rete e le applicazioni.
* Fornisce un elenco di priorità degli avvisi di sicurezza, inclusi gli avvisi di partner integrata soluzioni, insieme alle informazioni di hello è necessario tooquickly esaminare e indicazioni su come tooremediate un attacco.

Altre informazioni:

* [Introduzione tooAzure Centro sicurezza](../security-center/security-center-intro.md)

<!--Image references-->
[1]: ./media/security-management-and-monitoring-overview/shared-responsibility.png

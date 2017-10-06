---
title: procedure consigliate di sicurezza operativa aaaAzure | Documenti Microsoft
description: Questo articolo propone un set di procedure consigliate per la sicurezza operativa di Azure.
services: security
documentationcenter: na
author: unifycloud
manager: swadhwa
editor: tomsh
ms.assetid: 
ms.service: security
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/04/2017
ms.author: tomsh
ms.openlocfilehash: b3b17ef20fb3545b1c268ac0d7ce692e07c8da00
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="azure-operational-security-best-practices"></a>Procedure consigliate per la sicurezza operativa di Azure
Sicurezza operativa Azure fa riferimento toohello servizi, i controlli e toousers disponibili funzionalità per la protezione dei dati, applicazioni e altre risorse in Microsoft Azure. Sicurezza operative di Azure si basa su un framework che incorpora informazioni hello ottenute tramite varie funzionalità che sono univoci tooMicrosoft, tra cui Microsoft Security Development Lifecycle (SDL), Microsoft Security Response Center hello hello programma e conoscenza approfondita dei panorama delle minacce alla sicurezza informatica hello.

In questo articolo viene illustrata una raccolta di procedure consigliate per la sicurezza del database di Azure, Queste procedure consigliate derivano dall'esperienza acquisita con la protezione del database di Azure e l'esperienza dei clienti hello come manualmente.

Per ogni procedura consigliata verrà illustrato:
-   Quali consigliabile hello
-   Motivo per cui si desidera tooenable consigliata
-   Se non è consigliata di hello tooenable, quale potrebbe essere il risultato di hello
- Informazioni come procedura consigliata hello tooenable

Questo articolo Azure Operational procedure ottimali di protezione si basa su un parere di consenso e funzionalità della piattaforma Azure e il set di funzionalità, in cui si trovano in fase di hello in questo articolo è stato scritto. Opinioni e le tecnologie cambiano nel tempo e questo articolo verrà aggiornato in un tooreflect regolarmente le modifiche.

Le procedure consigliate per la sicurezza operativa di Azure discusse in questo articolo includono:

-   Monitorare, gestire e proteggere l'infrastruttura cloud
-   Gestire le identità e implementare Single Sign-On (SSO)
-   Tenere traccia delle richieste, analizzare le tendenze di utilizzo e diagnosticare i problemi
-   Monitoraggio dei servizi con una soluzione di monitoraggio centralizzata
-   Impedire, rilevare e rispondere toothreats
-   Monitoraggio della rete basato su scenari end-to-end
-   Distribuzione sicura tramite strumenti DevOps collaudati

## <a name="monitor-manage-and-protect-cloud-infrastructure"></a>Monitorare, gestire e proteggere l'infrastruttura cloud
Il reparto IT è responsabile della gestione dei dati, tra cui hello stabilità e sicurezza di questi sistemi, applicazioni e dell'infrastruttura Data Center. Ottenere informazioni di sicurezza in ad aumentare gli ambienti IT complessi spesso richiede, tuttavia, le organizzazioni toocobble uniscono i dati da più sistemi di sicurezza e la gestione.

[Microsoft Operations Management Suite (OMS)](https://docs.microsoft.com/azure/operations-management-suite/operations-management-suite-overview) è la soluzione Microsoft per la gestione IT basata sul cloud che consente di gestire e proteggere l'infrastruttura locale e cloud.

[Soluzioni OMS Security and Audit](https://docs.microsoft.com/azure/operations-management-suite/oms-security-monitoring-resources) Abilita tooactively IT di monitorare tutte le risorse, che consentono di ridurre al minimo l'impatto di hello di eventi di sicurezza. OMS Security and Audit prevede domini di sicurezza che possono essere usati per il monitoraggio delle risorse.

Per ulteriori informazioni su OMS, leggere l'articolo hello [Operations Management Suite](https://technet.microsoft.com/library/mt484091.aspx).

toohelp impedire, rilevare e rispondere toothreats, [soluzione di controllo e protezione di Operations Management Suite (OMS)](https://docs.microsoft.com/azure/operations-management-suite/oms-security-getting-started) raccoglie ed elabora i dati sulle risorse, che includono:

-   Registri eventi sicurezza
-   Tracciamento degli eventi di Windows (ETW)
-   Eventi di controllo AppLocker
-   Log di Windows Firewall
-   Eventi di Advanced Threat Analytics
-   Risultati della valutazione baseline
-   Risultati di Antimalware Assessment
-   Risultati della valutazione di aggiornamenti/patch
-   Flussi Syslog che sono abilitati in modo esplicito sull'agente hello


## <a name="manage-identity-and-implement-single-sign-on"></a>Gestire le identità e implementare Single Sign-On
[Azure Active Directory (Azure AD)](https://docs.microsoft.com/azure/active-directory/active-directory-whatis) è il servizio Microsoft di gestione di identità e directory basato sul cloud e multi-tenant.

[Azure AD](https://azure.microsoft.com/services/active-directory/) include anche un insieme completo di funzionalità per la [gestione delle identità](https://docs.microsoft.com/azure/security/security-identity-management-overview), tra cui l'[autenticazione a più fattori](https://docs.microsoft.com/azure/multi-factor-authentication/multi-factor-authentication), la registrazione dei dispositivi, la gestione self-service delle password e dei gruppi, la gestione degli account con privilegi, il controllo degli accessi in base al ruolo, il monitoraggio dell'utilizzo dell'applicazione, il controllo avanzato e il monitoraggio e avvisi relativi alla sicurezza.

Hello seguente funzionalità possibile la protezione delle applicazioni basate su cloud, semplificare i processi IT, ridurre i costi e garantire che siano soddisfatti gli obiettivi aziendali di conformità:

-   Gestione delle identità e accesso per il cloud hello
-   Semplificare l'accesso utente tooany. app cloud
-   Protezione di dati e applicazioni sensibili
-   Abilitazione della modalità self-service per i dipendenti
-   Integrazione con Azure Active Directory

### <a name="identity-and-access-management-for-hello-cloud"></a>Gestione delle identità e accesso per il cloud hello
Azure Active Directory (Azure AD) è una serie completa [soluzione cloud di gestione di identità e accessi](https://www.microsoft.com/cloud-platform/identity-management), che offre un set affidabile di funzionalità toomanage utenti e gruppi. Consente di proteggere l'accesso locale tooon cloud e applicazioni, compresi servizi web di Microsoft come Office 365 e quantità software non Microsoft come applicazioni di servizio (SaaS).
più la protezione dell'identità tooenable in Azure AD, vedere toolearn [attivazione di Azure Active Directory Identity Protection](https://docs.microsoft.com/azure/active-directory/active-directory-identityprotection-enable).

### <a name="simplify-user-access-tooany-cloud-app"></a>Semplificare l'accesso utente tooany. app cloud
[Abilita single sign-on](https://docs.microsoft.com/azure/active-directory/active-directory-sso-integrate-saas-apps) toosimplify utente accesso toothousands delle applicazioni cloud dai dispositivi Windows, Mac, Android e iOS. Gli utenti possono avviare applicazioni cloud da un pannello di accesso Web personalizzato usando le proprie credenziali aziendali. Utilizzare toogo di modulo Proxy dell'applicazione hello Azure AD oltre applicazioni SaaS e pubblicare on premise web applicazioni tooprovide estremamente sicuro accesso remoto e accesso single sign-on.

### <a name="protect-sensitive-data-and-applications"></a>Protezione di dati e applicazioni sensibili
Abilitare [Azure multi-Factor Authentication](https://docs.microsoft.com/azure/multi-factor-authentication/multi-factor-authentication) tooprevent non autorizzato ai tooon locale e applicazioni cloud, fornendo un ulteriore livello di autenticazione. Proteggere l'azienda e prevenire le possibili minacce mediante monitoraggio della sicurezza, avvisi e report basati su Machine Learning in grado di identificare i modelli di accesso non coerenti.

### <a name="enable-self-service-for-your-employees"></a>Abilitazione della modalità self-service per i dipendenti
Delegare dipendenti tooyour attività importanti, ad esempio la reimpostazione delle password e la creazione e gestione dei gruppi. [Abilitare la modifica self-service della password](https://docs.microsoft.com/azure/active-directory/active-directory-passwords-update-your-own-password), la reimpostazione e la gestione di gruppi in modalità self-service con Azure AD.

### <a name="integrate-with-azure-active-directory"></a>Integrazione con Azure Active Directory
Estendere [Active Directory](https://docs.microsoft.com/azure/active-directory/develop/active-directory-how-to-integrate) e qualsiasi altro locale directory tooAzure AD tooenable single sign-on per tutte le applicazioni basate su cloud. Gli attributi utente possono essere una directory cloud tooyour automaticamente sincronizzate da tutti i tipi di directory locali.

toolearn ulteriori informazioni sull'integrazione di Azure Active Directory e come tooenable, leggere hello articolo [integrare le directory locali con Azure Active Directory](https://docs.microsoft.com/azure/active-directory/connect/active-directory-aadconnect).

## <a name="trace-requests-analyze-usage-trends-and-diagnose-issues"></a>Tenere traccia delle richieste, analizzare le tendenze di utilizzo e diagnosticare i problemi
L'[Analisi archiviazione di Azure](https://docs.microsoft.com/azure/storage/storage-analytics) esegue la registrazione e restituisce i dati delle metriche per un account di archiviazione. È possibile usare questo richieste tootrace dati, analizzare le tendenze di utilizzo e diagnosticare i problemi con l'account di archiviazione.

Le metriche di Analisi archiviazione sono abilitate per impostazione predefinita per i nuovi account di archiviazione. È possibile abilitare la registrazione e configurare le metriche e registrazione nel portale di Azure; hello Per informazioni dettagliate, vedere [monitorare un account di archiviazione nel portale di Azure hello](https://docs.microsoft.com/azure/storage/storage-monitor-storage-account). È anche possibile abilitare Analitica di archiviazione a livello di programmazione tramite hello API REST o libreria client hello. Utilizzare hello Set Service Properties operazione tooenable archiviazione Analitica singolarmente per ogni servizio.

Per una guida approfondita sull'uso di archiviazione Analitica e tooidentify altri strumenti, diagnosticare e risoluzione dei problemi relativi al servizio di archiviazione Azure, vedere [Monitor, diagnosticare e risolvere i problemi di archiviazione di Microsoft Azure](https://docs.microsoft.com/azure/storage/storage-monitoring-diagnosing-troubleshooting).

toolearn ulteriori informazioni sull'integrazione di Azure Active Directory e come tooenable, leggere articolo hello [abilitazione e configurazione di archiviazione Analitica](https://docs.microsoft.com/rest/api/storageservices/Enabling-and-Configuring-Storage-Analytics?redirectedfrom=MSDN).

## <a name="monitoring-services"></a>Monitoraggio dei servizi
Le applicazioni cloud sono complesse e hanno molte parti mobili. Il monitoraggio fornisce tooensure dati che l'applicazione resta alto e in esecuzione in uno stato integro. Consente inoltre toostave è impostata su off problemi potenziali o risolvere i problemi oltre quelle. Inoltre, è possibile utilizzare Monitoraggio dati toogain approfondite sull'applicazione. Tali informazioni possono consentono di prestazioni dell'applicazione tooimprove o manutenibilità o automatizzare le operazioni che altrimenti richiederebbero un intervento manuale.

### <a name="monitor-azure-resources"></a>Monitorare le risorse di Azure
[Monitoraggio Azure](https://docs.microsoft.com/azure/monitoring-and-diagnostics/monitoring-get-started) è servizio di piattaforma hello che fornisce un'unica origine per il monitoraggio delle risorse di Azure. Con il monitoraggio di Azure, è possibile visualizzare, richiedere, route, archiviare e intraprendere un'azione in metriche hello e log provenienti dalle risorse in Azure. È possibile utilizzare questo dati pannello portale monitoraggio di hello, con [i cmdlet PowerShell di monitoraggio](https://docs.microsoft.com/azure/monitoring-and-diagnostics/insights-powershell-samples), [CLI multipiattaforma](https://docs.microsoft.com/azure/monitoring-and-diagnostics/insights-cli-samples), o [API REST di Azure monitoraggio](https://msdn.microsoft.com/library/dn931943.aspx).

### <a name="enable-autoscale-with-azure-monitor"></a>Abilitare la scalabilità automatica con Monitoraggio di Azure
Abilitare [scalabilità automatica di monitoraggio di Azure](https://docs.microsoft.com/azure/monitoring-and-diagnostics/monitoring-autoscale-get-started) si applica solo set di scalabilità macchina toovirtual (VMSS), servizi cloud, piani di servizio app e gli ambienti del servizio app.

### <a name="manage-roles-permissions-and-security"></a>Gestire le autorizzazioni e la sicurezza dei ruoli
Molti team necessario toostrictly [regolare accesso toomonitoring](https://docs.microsoft.com/azure/monitoring-and-diagnostics/monitoring-roles-permissions-security) dati e le impostazioni. Ad esempio, se si dispongono di membri del team che lavorano esclusivamente sul monitoraggio (tecnici del supporto, i tecnici devops) o se si utilizza un provider del servizio gestito, è opportuno toogrant tooonly dati di monitoraggio limitando la possibilità toocreate loro l'accesso, modificare, o eliminare le risorse.

Viene illustrato come tooquickly applicare un monitoraggio RBAC ruolo tooa utente incorporato in Azure o creare il proprio ruolo personalizzato per un utente che necessita di autorizzazioni limitate di monitoraggio. Quindi illustra le considerazioni sulla sicurezza per le risorse correlate al monitoraggio di Azure e come è possibile limitare l'accesso ai dati toohello contengono.

## <a name="prevent-detect-and-respond-toothreats"></a>Impedire, rilevare e rispondere toothreats
Rilevamento minacce del Centro sicurezza PC funziona automaticamente la raccolta di informazioni di sicurezza da risorse di Azure, rete hello e soluzioni partner connesso. Analizza queste informazioni, correlazione spesso informazioni provenienti da più origini, tooidentify minacce. Avvisi di sicurezza sono classificati in Centro sicurezza PC insieme ai consigli su come tooremediate hello minaccia.

-   [Configurare i criteri di sicurezza](https://docs.microsoft.com/azure/security-center/security-center-policies) per la sottoscrizione di Azure.
-   Hello utilizzare [indicazioni del Centro sicurezza PC](https://docs.microsoft.com/azure/security-center/security-center-recommendations) toohelp proteggere le risorse di Azure.
-   Esaminare e gestire gli [avvisi di sicurezza](https://docs.microsoft.com/azure/security-center/security-center-managing-and-responding-alerts) correnti.

[Centro sicurezza di Azure](https://docs.microsoft.com/azure/security-center/security-center-intro) consente di impedire, rilevare e rispondere toothreats con una maggiore visibilità e controllo sui hello protezione delle risorse di Azure. Offre funzionalità integrate di monitoraggio della sicurezza e gestione dei criteri tra le sottoscrizioni di Azure, facilita il rilevamento delle minacce che altrimenti passerebbero inosservate e funziona con un ampio ecosistema di soluzioni di sicurezza.

Centro sicurezza PC offre minaccia di semplice utilizzo ed efficace funzionalità di prevenzione, rilevamento e risposta che vengono compilate in tooAzure. Funzionalità principali:

-   Ottenere informazioni sullo stato della sicurezza nel cloud
-   Acquisire il controllo della sicurezza nel cloud
-   Distribuire in tutta semplicità soluzioni di sicurezza nel cloud integrate
-   Rilevare le minacce e rispondere rapidamente

### <a name="understand-cloud-security-state"></a>Ottenere informazioni sullo stato della sicurezza nel cloud
Utilizzare il Centro protezione Azure tooget una vista centrale dello stato di sicurezza hello di tutte le risorse di Azure. In breve, verificare che siano soddisfatti i controlli di sicurezza appropriati hello e configurato correttamente e identificano rapidamente eventuali risorse che richiedono attenzione.

### <a name="take-control-of-cloud-security"></a>Acquisire il controllo della sicurezza nel cloud
Definire [criteri di sicurezza](https://docs.microsoft.com/azure/security-center/security-center-policies) per le sottoscrizioni di Azure in base della società tooyour del protezione cloud, è necessario adattato toohello tipi di applicazioni o riservatezza dei dati hello in ogni sottoscrizione. Usare proprietari delle risorse basato su criteri indicazioni tooguide processo hello di implementazione di controlli necessari, ovvero richiedere supporto per hello protezione cloud.

### <a name="easily-deploy-integrated-cloud-security-solutions"></a>Distribuire in tutta semplicità soluzioni di sicurezza nel cloud integrate
[Abilitare soluzioni di sicurezza](https://docs.microsoft.com/azure/security-center/security-center-partner-integration) di Microsoft e dei suoi partner, tra cui firewall e antimalware leader del settore. Utilizzo semplificato soluzioni per la sicurezza toodeploy provisioning, modifiche anche rete vengono configurate automaticamente. Gli eventi di sicurezza delle soluzioni dei partner vengono raccolti automaticamente per l'analisi e la creazione di avvisi.

### <a name="detect-threats-and-respond-fast"></a>Rilevare le minacce e rispondere rapidamente
Per anticipare le minacce al cloud attuali ed emergenti, è necessario un approccio integrato basato sull'analisi. Combinando l'esperienza e l'[intelligence per le minacce](https://docs.microsoft.com/azure/security-center/security-center-detection-capabilities) globali di Microsoft con informazioni dettagliate su eventi correlati alla sicurezza in tutte le distribuzioni di Azure, Centro sicurezza consente di rilevare in anticipo le minacce effettive con minori falsi positivi. Avvisi di protezione cloud offrono informazioni dettagliate sui campagna attacco hello, inclusi gli eventi correlati e le risorse interessate e vengono forniti suggerimenti tooremediate problemi e ripristinare rapidamente.

## <a name="end-to-end-scenario-based-network-monitoring"></a>Monitoraggio della rete basato su scenari end-to-end
Per creare una rete end-to-end in Azure è possibile orchestrare e comporre varie risorse di rete individuali, quali rete virtuale, ExpressRoute, gateway applicazione, servizi di bilanciamento del carico e altro ancora. Il monitoraggio è disponibile in ogni hello risorse di rete.

[Controllo di rete](https://docs.microsoft.com/azure/network-watcher/network-watcher-monitoring-overview) è un servizio consente toomonitor internazionale e diagnosticare le condizioni a un livello di uno scenario di rete in, a e da Azure. Diagnostica di rete e gli strumenti di visualizzazione disponibili con Watcher di rete consentono di comprendere, diagnosticare e ottenere rete tooyour insights in Azure.

### <a name="automate-remote-network-monitoring-with-packet-capture"></a>Automatizzare il monitoraggio di rete remoto con l'acquisizione pacchetti
Monitoraggio e diagnosi di problemi di rete senza effettuare l'accesso tooyour macchine virtuali (VM) utilizzando Watcher di rete. Trigger [acquisizione pacchetto](https://docs.microsoft.com/azure/network-watcher/network-watcher-alert-triggered-packet-capture) impostando gli avvisi e ottenere informazioni di accesso tooreal prestazioni a livello di pacchetto hello. Quando viene rilevato un problema, è possibile esaminarlo in dettaglio per una diagnosi migliore.

### <a name="gain-insight-into-your-network-traffic-using-flow-logs"></a>Acquisire informazioni dettagliate sul traffico di rete con i log dei flussi
Ottenere informazioni approfondite sul modello del traffico di rete con i [log dei flussi del gruppo di sicurezza di rete](https://docs.microsoft.com/en-us/azure/network-watcher/network-watcher-nsg-flow-logging-overview). Le informazioni fornite dai log dei flussi permettono di raccogliere i dati per la conformità, il controllo e il monitoraggio del profilo di sicurezza della rete.

### <a name="diagnose-vpn-connectivity-issues"></a>Diagnosticare i problemi di connettività della VPN
Watcher di rete fornisce si hello possibilità troppo[diagnosticare i problemi più comuni di Gateway VPN e connessioni](https://docs.microsoft.com/azure/network-watcher/network-watcher-diagnose-on-premises-connectivity). Che consente non solo problema hello tooidentify, ma anche toouse hello dettagliati registri esaminare ulteriormente toohelp creato.

altre informazioni su come toolearn tooconfigure watcher di rete e come tooenable, leggere hello articolo [configurare watcher di rete](https://docs.microsoft.com/azure/network-watcher/network-watcher-create).

## <a name="secure-deployment-using-proven-devops-tools"></a>Distribuzione sicura tramite strumenti DevOps collaudati
Questi sono alcuni dei hello elenco di Azure DevOps consigliate in questo spazio Cloud Microsoft, che rende le aziende e i team produttivi ed efficienti.

-   **Infrastruttura come codice (IaC):** infrastruttura come codice è un set di tecniche e procedure consigliate, che aiutano i professionisti IT rimuovere onere hello associate alla compilazione tooday giorno di hello e gestione dell'infrastruttura modulare. Consente ai professionisti IT toobuild e mantenere l'ambiente server moderna in modo simile a quello descritto agli sviluppatori di software compilare e gestire il codice dell'applicazione. Per Azure, è possibile utilizzare [Azure Resource Manager]( https://azure.microsoft.com/documentation/articles/resource-group-authoring-templates/) tooprovision consente le applicazioni con un modello dichiarativo. In un unico modello, è possibile distribuire più servizi con le relative dipendenze. Utilizzare hello stesso modello toorepeatedly distribuire l'applicazione durante ogni fase del ciclo di vita dell'applicazione hello.
-   **Integrazione continua e della distribuzione:** è possibile configurare i progetti team di Visual Studio Online troppo[compilare e distribuire automaticamente](https://www.visualstudio.com/docs/build/overview) tooAzure le app web o servizi cloud. Visual Studio online distribuisce automaticamente i file binari hello dopo aver eseguito un tooAzure compilazione dopo ogni archiviazione codice. il processo di compilazione pacchetto descritto qui Hello è comando pacchetto toohello equivalente in Visual Studio, e passaggi di pubblicazione hello comando Pubblica toohello equivalente in Visual Studio.
-   **Gestione del rilascio:** Visual Studio [Release Management](https://msdn.microsoft.com/library/vs/alm/release/overview) è un'ottima soluzione per automatizzare la distribuzione a più fasi e la gestione di hello processo di rilascio. Creare la distribuzione continua gestito pipeline toorelease rapidamente, semplice e spesso. Con Release Management è possibile automatizzare in gran parte il processo di rilascio e definire flussi di lavoro predefiniti per l'approvazione. La distribuzione locale e toohello cloud, estendere e personalizzare in base alle esigenze.
-   **Monitoraggio delle prestazioni delle app:** rilevare problemi, risolverli e migliorare continuamente le applicazioni. Diagnosticare rapidamente eventuali problemi nell'applicazione live. Comprendere in che modo gli utenti lo usano. Configurazione riguarda semplice aggiunta di codice JS e una voce webconfig e vengono visualizzati i risultati in pochi minuti nel portale di hello con tutti i dettagli di hello. [App insights](https://azure.microsoft.com/documentation/articles/app-insights-start-monitoring-app-health-usage/) aiuta le aziende per una maggiore velocità di rilevamento di problemi e monitoraggio e aggiornamento.
-   **Scalabilità automatica e test di carico:** è possibile trovare i problemi di prestazioni qualità di distribuzione di app tooimprove e toomake l'app sia sempre attivo o disponibile toocater toohello le esigenze aziendali. Verificare che l'app possa gestire il traffico per la prossima campagna di lancio o di marketing. Con Visual Studio Online è possibile iniziare molto velocemente a eseguire [test di carico](https://www.visualstudio.com/docs/test/performance-testing/getting-started/getting-started-with-performance-testing) basati sul cloud.

## <a name="next-steps"></a>Passaggi successivi
- Altre informazioni sulla [sicurezza operativa di Azure](https://docs.microsoft.com/azure/security/azure-operational-security).
- tooLearn più [Operations Management Suite | Sicurezza e conformità](https://www.microsoft.com/cloud-platform/security-and-compliance).
- [Introduzione alla soluzione Sicurezza e controllo di Operations Management Suite](https://docs.microsoft.com/azure/operations-management-suite/oms-security-getting-started).

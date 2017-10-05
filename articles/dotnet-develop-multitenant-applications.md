---
title: Modello di applicazione Web multi-tenant | Microsoft Docs
description: Sono disponibili informazioni generali sull'architettura e modelli di progettazione che descrivono come implementare un'applicazione Web multi-tenant in Azure.
services: 
documentationcenter: .net
author: wadepickett
manager: wpickett
editor: 
ms.assetid: 4f0281d2-1555-42b0-a99d-1222fade0b0f
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 06/05/2015
ms.author: wpickett
ms.openlocfilehash: 57ba0e46139bda2d74c9f7db0ffab2f2122b0df2
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/03/2017
---
# <a name="multitenant-applications-in-azure"></a>Applicazioni multi-tenant in Azure
Un'applicazione multi-tenant è una risorsa condivisa che consente a utenti separati, o "tenant", di visualizzare l'applicazione come se fosse la propria. Uno degli scenari tipici di un'applicazione multi-tenant è quando tutti gli utenti dell'applicazione desiderano personalizzare l'esperienza utente, ma dispongono tutti degli stessi requisiti aziendali di base. Esempi di grandi applicazioni multi-tenant sono Office 365, Outlook.com e visualstudio.com.

Dal punto di vista del fornitore di applicazioni, i vantaggi della multi-tenancy risiedono principalmente nell'efficienza operativa e dei costi. Una versione dell'applicazione può soddisfare le esigenze di molti tenant/client, consentendo il consolidamento di attività amministrative del sistema come il monitoraggio, l'ottimizzazione delle prestazioni, la manutenzione del software e i backup di dati.

Di seguito è riportato un elenco degli obiettivi e dei requisiti più significativi dal punto di vista di un fornitore.

* **Provisioning**: è necessario essere in grado di eseguire il provisioning di nuovi tenant per l'applicazione.  Per le applicazioni multi-tenant che contano un ingente numero di tenant, di solito è necessario automatizzare il processo abilitando il provisioning self-service.
* **Manutenibilità**: è necessario essere in grado di aggiornare l'applicazione ed eseguire altre attività di manutenzione quando è usata da più tenant.
* **Monitoraggio**: è necessario essere in grado di monitorare l'applicazione in ogni momento allo scopo di identificare eventuali problemi e risolverli. Ciò include il monitoraggio della modalità di uso dell'applicazione da parte di ogni tenant.

Un'applicazione multi-tenant correttamente implementata offre agli utenti i vantaggi seguenti.

* **Isolamento**: le attività dei singoli tenant non incidono sull'uso dell'applicazione da parte degli altri tenant. I tenant non possono accedere ai dati reciproci. Ogni tenant avrà apparentemente l'uso esclusivo dell'applicazione.
* **Disponibilità**: i singoli tenant vogliono che l'applicazione sia sempre disponibile, meglio se con garanzie definite in un contratto di servizio (SLA, Service Level Agreement). Come già accennato, le attività dei singoli tenant non dovrebbero incidere sulla disponibilità dell'applicazione.
* **Scalabilità**: è possibile scalare l'applicazione in modo da soddisfare la domanda di singoli tenant. La presenza e le azioni degli altri tenant non dovrebbero incidere sulle prestazioni dell'applicazione.
* **Costi**: i costi sono inferiori rispetto all'esecuzione di un'applicazione single-tenant dedicata, in quanto la multi-tenancy consente la condivisione delle risorse.
* **Personalizzabilità**. la possibilità di personalizzare l'applicazione per un singolo tenant in vari modi, ad esempio con l'aggiunta o la rimozione di funzionalità, la modifica di colori e loghi o persino l'aggiunta di un proprio codice o script.

In breve, benché sia necessario prendere in considerazione vari aspetti al fine di fornire un servizio altamente scalabile, vi è anche una serie di obiettivi e requisiti comuni a molte applicazioni multi-tenant. Alcuni potrebbero non essere pertinenti in scenari specifici e l'importanza dei singoli obiettivi e requisiti varierà in ogni scenario. Anche il fornitore di un'applicazione multi-tenant avrà obiettivi e requisiti, ad esempio soddisfare gli obiettivi e i requisiti dei tenant, redditività, fatturazione, vari livelli di servizio, provisioning, monitoraggio della manutenibilità e automazione.

Per altre informazioni sulle considerazioni di progettazione di un'applicazione multi-tenant vedere [Hosting a Multi-Tenant Application on Azure][Hosting a Multi-Tenant Application on Azure] (Hosting di un'applicazione multi-tenant in Azure). Per informazioni sugli schemi di architettura dati comuni delle applicazioni di database multi-tenant software come un servizio (SaaS), vedere [Schemi progettuali per applicazioni SaaS multi-tenant con il database SQL di Azure](sql-database/sql-database-design-patterns-multi-tenancy-saas-applications.md). 

Azure offre molte funzionalità che consentono di risolvere i principali problemi riscontrati durante la progettazione di un sistema multi-tenant.

**Isolamento**

* Segmentare i tenant del sito Web in base alle intestazioni host con o senza comunicazione SSL
* Segmentare i tenant del sito Web in base ai parametri della query
* Servizi Web nei ruoli di lavoro
  * Ruoli di lavoro che solitamente elaborano i dati sul back-end di un'applicazione.
  * Ruoli Web che solitamente fungono da front-end per le applicazioni.

**Archiviazione**

Gestione di dati come il database SQL di Azure o i servizi di archiviazione di Azure (ad esempio il servizio tabelle, che offre servizi di archiviazione di grandi quantità di dati non strutturati, e il servizio BLOB, che offre servizi di archiviazione di grandi quantità di dati testuali o binari non strutturati come video, audio e immagini).

* Protezione di dati multi-tenant nel database SQL appropriati per l'accesso a SQL Server di ogni tenant.
* Uso di tabelle Azure per le risorse dell'applicazione - Specificando criteri di accesso a livello di contenitore, sarà possibile modificare le autorizzazioni senza dover generare nuovi URL per le risorse protette mediante firme di accesso condiviso.
* Code di Azure per le risorse dell'applicazione - Le code di Azure sono comunemente utilizzate per attivare l'elaborazione per conto dei tenant, ma possono essere utilizzate anche per distribuire il lavoro richiesto per il provisioning o la gestione.
* Code di bus di servizio - Per le risorse dell'applicazione che effettuano il push del lavoro a un servizio condiviso, è possibile usare una singola coda in cui ogni mittente del tenant dispone solo delle autorizzazioni (in base alle attestazioni generate da ACS) per effettuare il push a quella coda, mentre solo i ricevitori dal servizio dispongono dell'autorizzazione per effettuare il pull dei dati provenienti da più tenant dalla coda.

**Servizi di connessione e sicurezza**

* Il bus di servizio di Azure, un'infrastruttura di messaggistica che consente di scambiare messaggi tra le applicazioni con approccio "a regime di controllo libero" per migliorare la scalabilità e la resilienza.

**Servizi di rete**

Azure offre diversi servizi di rete che supportano l'autenticazione e migliorano la gestibilità delle applicazioni ospitate. Di seguito sono indicati alcuni servizi disponibili:

* La rete virtuale di Azure consente di effettuare il provisioning e la gestione delle reti private virtuali (VPN) in Azure e di collegare queste reti in modo sicuro con l'infrastruttura IT locale.
* Rete virtuale - Gestione traffico consente di bilanciare il carico del traffico in ingresso tra più servizi di Azure ospitati, in esecuzione sia nello stesso data center sia in data center diversi distribuiti in tutto il mondo.
* Azure Active Directory (Azure AD) è un servizio moderno basato su REST che fornisce funzionalità di gestione dell'identità e controllo di accesso per le applicazioni cloud. L'utilizzo di Azure AD per le risorse dell'applicazione semplifica le procedure di autenticazione e autorizzazione degli utenti affinché venga loro concesso l'accesso a servizi e applicazioni Web, consentendo al contempo il factoring delle funzionalità di autenticazione e autorizzazione al di fuori del codice.
* Il bus di servizio di Azure fornisce una funzionalità protetta di messaggistica e flusso dei dati per le applicazioni distribuite e ibride, ad esempio la comunicazione tra le applicazioni ospitate su Azure e le applicazioni e i servizi locali, senza richiedere complesse infrastrutture di sicurezza e firewall. Uso dell'inoltro del bus di servizio per le risorse dell'applicazione - I servizi esposti come endpoint possono appartenere al tenant (ad esempio, ospitati al di fuori del sistema, come in locale) o essere forniti in maniera specifica per il tenant (perché usati per il trasferimento di dati riservati, specifici del tenant).

**Provisioning delle risorse**

Azure offre diverse modalità per eseguire il provisioning di nuovi tenant per l'applicazione. Per le applicazioni multi-tenant che contano un ingente numero di tenant, di solito è necessario automatizzare il processo abilitando il provisioning self-service.

* I ruoli di lavoro consentono di eseguire il provisioning e il deprovisioning delle risorse per ogni tenant (ad esempio quando un nuovo tenant effettua o annulla l'iscrizione), raccogliendo metriche per misurare l'utilizzo e gestendo la scalabilità in base a una determinata pianificazione o in risposta al superamento di soglie degli indicatori di prestazioni chiave. Questo stesso ruolo può essere utilizzato anche per effettuare il push di aggiornamenti alla soluzione.
* È possibile utilizzare l'archivio BLOB di Azure per effettuare il provisioning delle risorse di calcolo o di archiviazione preinizializzate per i nuovi tenant, fornendo criteri di accesso a livello di contenitore per proteggere i pacchetti del servizio di calcolo, le immagini del disco rigido virtuale e altre risorse.
* Le opzioni per il provisioning delle risorse del database SQL per un tenant includono:
  
  * DDL in script o incorporate come risorse negli assembly
  * Distribuzione a livello di codice dei pacchetti SQL Server 2008 R2 DAC
  * Copia da un database di riferimento master
  * Uso delle funzionalità di importazione ed esportazione del database per il provisioning di nuovi database da un file

<!--links-->

[Hosting a Multi-Tenant Application on Azure]: http://msdn.microsoft.com/library/hh534480.aspx
[Designing Multitenant Applications on Azure]: http://msdn.microsoft.com/library/windowsazure/hh689716

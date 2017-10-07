---
title: Modello di applicazione Web Tenant aaaMulti | Documenti Microsoft
description: "Sono disponibili una panoramica dell'architettura e i modelli di progettazione che descrivono la modalità multi-tenant tooimplement web dell'applicazione in Azure."
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
ms.openlocfilehash: 3b7822c8ca4aa50d295a174973ae4746c230ba66
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="multitenant-applications-in-azure"></a>Applicazioni multi-tenant in Azure
Un'applicazione multi-tenant è una risorsa condivisa che consente agli utenti, o "tenant", tooview hello applicazione separata come se fosse proprio. Uno scenario tipico che si presta applicazione multi-tenant tooa è uno in cui tutti gli utenti di hello applicazione potrebbe desidera esperienza utente di hello toocustomize ma in caso contrario hello stessi requisiti aziendali di base. Esempi di grandi applicazioni multi-tenant sono Office 365, Outlook.com e visualstudio.com.

Dalla prospettiva di un provider applicazione, vantaggi hello di multi-tenancy principalmente correlate toooperational e l'efficienza dei costi. Una versione dell'applicazione è possibile soddisfare le esigenze di hello di molti tenant/clienti, che consente di attività di amministrazione quali monitoraggio, l'ottimizzazione delle prestazioni, manutenzione del software e i backup dei dati di consolidamento del sistema.

esempio Hello fornisce un elenco di requisiti dal punto di vista di un provider di servizi e degli obiettivi principali di hello.

* **Provisioning**: È necessario essere in grado di tooprovision nuovi tenant per un'applicazione hello.  Per le applicazioni multi-tenant con un numero elevato di tenant, è in genere necessario tooautomate questo processo dall'abilitazione del provisioning self-service.
* **Manutenibilità**: È necessario essere in grado di tooupgrade hello applicazione ed eseguire altre attività di manutenzione mentre si utilizzano più tenant.
* **Monitoraggio**: si deve essere in grado di toomonitor applicazione hello tooidentify sempre eventuali problemi e tootroubleshoot li. Ciò include il monitoraggio come ogni tenant Usa un'applicazione hello.

Un'applicazione multi-tenant implementata correttamente fornisce toousers i vantaggi seguenti hello.

* **Isolamento**: attività hello di singoli tenant non influiscono sull'uso di hello di un'applicazione hello da altri tenant. I tenant non possono accedere ai dati reciproci. Tenant toohello viene visualizzato come se è presente l'utilizzo esclusivo dell'applicazione hello.
* **Disponibilità**: singoli tenant vuole toobe applicazione hello continuamente disponibili, ad esempio con garanzie definite in un contratto di servizio. Nuovamente, le attività di hello di altri tenant non dovrebbero influire disponibilità hello applicazione hello.
* **Scalabilità**: scalabilità dell'applicazione hello è richiesta hello toomeet di singoli tenant. Hello presenza e le azioni di altri tenant non dovrebbero influire sulle prestazioni di hello di un'applicazione hello.
* **I costi**: i costi sono inferiori rispetto all'esecuzione di un'applicazione dedicata, single-tenant perché consente di multi-tenancy hello condivisione delle risorse.
* **Personalizzabilità**. Hello possibilità toocustomize hello applicazione per un singolo tenant in vari modi, ad esempio aggiunta o rimozione di funzionalità, modifica di colori e logo o persino aggiungendo il proprio codice o script.

In breve, mentre in considerazione numerosi fattori che è necessario prendere in considerazione tooprovide un servizio altamente scalabile, esistono anche un numero di obiettivi di hello e i requisiti delle applicazioni multi-tenant toomany comuni. Alcuni potrebbero non essere rilevanti in scenari specifici e importanza hello di singoli obiettivi e requisiti variano in ogni scenario. Come provider di un'applicazione hello multi-tenant, si avrà inoltre gli obiettivi e requisiti, ad esempio, riunione tenant hello obiettivi e requisiti, redditività, fatturazione, più livelli di servizio, il provisioning, manutenibilità monitoraggio e automazione.

Per altre informazioni sulle considerazioni di progettazione di un'applicazione multi-tenant vedere [Hosting a Multi-Tenant Application on Azure][Hosting a Multi-Tenant Application on Azure] (Hosting di un'applicazione multi-tenant in Azure). Per informazioni sugli schemi di architettura dati comuni delle applicazioni di database multi-tenant software come un servizio (SaaS), vedere [Schemi progettuali per applicazioni SaaS multi-tenant con il database SQL di Azure](sql-database/sql-database-design-patterns-multi-tenancy-saas-applications.md). 

Azure offre numerose funzionalità che consentono di tooaddress hello chiave ai problemi riscontrati quando si progetta un sistema multi-tenant.

**Isolamento**

* Segmentare i tenant del sito Web in base alle intestazioni host con o senza comunicazione SSL
* Segmentare i tenant del sito Web in base ai parametri della query
* Servizi Web nei ruoli di lavoro
  * Ruoli di lavoro in genere che elabora i dati nel back-end hello di un'applicazione.
  * Ruoli Web che in genere fungono da front-end hello per le applicazioni.

**Archiviazione**

Servizio che fornisce servizi per l'archiviazione di grandi quantità di dati non strutturati tabelle di gestione di dati, ad esempio servizi di Database SQL di Azure o di archiviazione di Azure, ad esempio hello e hello servizio Blob che fornisce servizi toostore grandi quantità di testo non strutturato o dati binari come video, audio e immagini.

* Protezione di dati multi-tenant nel database SQL appropriati per l'accesso a SQL Server di ogni tenant.
* Utilizzo di tabelle di Azure per l'applicazione risorse specificando criteri di accesso a livello di contenitore, è possibile hello autorizzazioni tooadjust possibilità senza tooissue nuovi URL per le risorse di hello protette con firme di accesso condiviso.
* Le code di Azure per le code di Azure le risorse dell'applicazione sono diffuse toodrive l'elaborazione per conto di tenant, ma può anche essere richiesto lavoro toodistribute utilizzato per il provisioning o la gestione.
* Un servizio condiviso di code di Service Bus per le risorse dell'applicazione che tooa lavoro push, è possibile usare una singola coda in cui ogni mittente del tenant dispone solo della coda di toothat toopush autorizzazioni (in base alle attestazioni generate da ACS), mentre solo i ricevitori hello dal servizio hello dispone dell'autorizzazione toopull dai dati di hello coda hello provenienti da più tenant.

**Servizi di connessione e sicurezza**

* Service Bus di Azure, un'infrastruttura di messaggistica che si trova tra applicazioni consentendo tooexchange messaggi in modo regime di controllo per una migliore scalabilità e resilienza.

**Servizi di rete**

Azure offre diversi servizi di rete che supportano l'autenticazione e migliorano la gestibilità delle applicazioni ospitate. Questi servizi includono seguente hello:

* La rete virtuale di Azure consente di effettuare il provisioning e la gestione delle reti private virtuali (VPN) in Azure e di collegare queste reti in modo sicuro con l'infrastruttura IT locale.
* Gestione traffico di rete virtuale consente di bilanciare tooload il traffico in ingresso attraverso Azure ospitati più servizi, in esecuzione in hello stesso Data Center o in Data Center diversi in tutto il mondo hello.
* Azure Active Directory (Azure AD) è un servizio moderno basato su REST che fornisce funzionalità di gestione dell'identità e controllo di accesso per le applicazioni cloud. Con Azure AD per tooprovides risorse dell'applicazione Azure AD un metodo semplice per autenticare e autorizzare gli utenti toogain accesso tooyour applicazioni e servizi web, consentendo hello delle funzionalità di autenticazione e autorizzazione toobe factoring fuori il codice.
* Il bus di servizio di Azure fornisce una funzionalità protetta di messaggistica e flusso dei dati per le applicazioni distribuite e ibride, ad esempio la comunicazione tra le applicazioni ospitate su Azure e le applicazioni e i servizi locali, senza richiedere complesse infrastrutture di sicurezza e firewall. Utilizzando l'inoltro del Bus di servizio per le risorse dell'applicazione toohello tenant dei servizi che vengono esposti come endpoint possono appartenere toohello (ad esempio, ospitato di fuori del sistema hello, ad esempio in locale) o possono essere forniti in modo specifico per hello tenant ( Poiché i dati riservati, specifici del tenant viene spostato su di essi).

**Provisioning delle risorse**

Azure offre diversi modi nuovi tenant di effettuare il provisioning per l'applicazione hello. Per le applicazioni multi-tenant con un numero elevato di tenant, è in genere necessario tooautomate questo processo dall'abilitazione del provisioning self-service.

* I ruoli di lavoro consentono di tooprovision e-provisioning di risorse per tenant (ad esempio quando un nuovo tenant effettua o Annulla), raccogliere le metriche per il controllo utilizzare e gestire la scalabilità di una determinata pianificazione o in d'incrocio toohello di risposta delle soglie di chiave indicatori di prestazioni. Questo stesso ruolo può essere anche usato toopush soluzione toohello gli aggiornamenti.
* BLOB di Azure può essere utilizzato tooprovision calcolo o le risorse di archiviazione già inizializzato per i nuovi tenant fornendo contenitore accesso a livello criteri tooprotect hello calcolo pacchetti del servizio, le immagini VHD e altre risorse.
* Le opzioni per il provisioning delle risorse del database SQL per un tenant includono:
  
  * DDL in script o incorporate come risorse negli assembly
  * Distribuzione a livello di codice dei pacchetti SQL Server 2008 R2 DAC
  * Copia da un database di riferimento master
  * Utilizzo di esportazione tooprovision nuovi database e database di importazione da un file.

<!--links-->

[Hosting a Multi-Tenant Application on Azure]: http://msdn.microsoft.com/library/hh534480.aspx
[Designing Multitenant Applications on Azure]: http://msdn.microsoft.com/library/windowsazure/hh689716

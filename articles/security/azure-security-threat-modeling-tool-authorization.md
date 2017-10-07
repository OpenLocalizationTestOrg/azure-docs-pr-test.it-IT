---
title: aaaAuthorization - modellazione strumento Microsoft Threat - Azure | Documenti Microsoft
description: misure di attenuazione esposte in hello strumento di modellazione del rischio di minacce per la
services: security
documentationcenter: na
author: RodSan
manager: RodSan
editor: RodSan
ms.assetid: na
ms.service: security
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/17/2017
ms.author: rodsan
ms.openlocfilehash: 3ea7ae2b46baa8578e574e6006b98dfe172829e7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="security-frame-authorization--mitigations"></a>Infrastruttura di sicurezza: autorizzazione - Procedure di mitigazione 
| Prodotto o servizio | Articolo |
| --------------- | ------- |
| **Limite di Trust del computer** | <ul><li>[Verificare che l'ACL appropriati siano configurati toorestrict non autorizzato accesso toodata sul dispositivo hello](#acl-restricted-access)</li><li>[Verificare che il contenuto sensibile dell'applicazione specifico dell'utente venga archiviato nella directory del profilo utente](#sensitive-directory)</li><li>[Verificare che le applicazioni distribuita hello vengono eseguite con privilegi minimi](#deployed-privileges)</li></ul> |
| **Applicazione Web** | <ul><li>[Applicare l'ordine dei passaggi in sequenza durante l'elaborazione di flussi di logica di business](#sequential-logic)</li><li>[Implementare l'enumerazione tooprevent meccanismo di limitazione della frequenza](#rate-enumeration)</li><li>[Verificare che sia presente l'autorizzazione necessaria e che venga seguito il principio dei privilegi minimi](#principle-least-privilege)</li><li>[Le decisioni riguardanti la logica di business e l'autorizzazione di accesso alle risorse non devono basarsi sui parametri di richiesta in ingresso](#logic-request-parameters)</li><li>[Verificare che il contenuto e le risorse non siano enumerabili o accessibili tramite browsing forzato](#enumerable-browsing)</li></ul> |
| **Database** | <ul><li>[Verificare che l'account con privilegi minimi siano utilizzati tooconnect tooDatabase server](#privileged-server)</li><li>[Implementare i tenant di sicurezza di livello di riga tooprevent l'accesso ai dati reciproci](#rls-tenants)</li><li>[Il ruolo sysadmin deve avere solo utenti necessari validi](#sysadmin-users)</li></ul> |
| **Gateway IoT cloud** | <ul><li>[Connessione Gateway tooCloud utilizzando i token con privilegi minimi](#cloud-least-privileged)</li></ul> |
| **Hub eventi di Azure** | <ul><li>[Usare una chiave di firma di accesso condiviso per autorizzazioni di solo invio per la generazione di token di dispositivo](#sendonly-sas)</li><li>[Non utilizzare i token di accesso che forniscono l'accesso diretto toohello Hub eventi](#access-tokens-hub)</li><li>[Connettersi tooEvent Hub utilizzando SAS chiavi che dispone delle autorizzazioni minime hello obbligatori](#sas-minimum-permissions)</li></ul> |
| **Azure Document DB** | <ul><li>[Risorsa token tooconnect tooDocumentDB ogni volta che è possibile utilizzare](#resource-docdb)</li></ul> |
| **Limite di trust di Azure** | <ul><li>[Abilitare la gestione di accesso con granularità fine tooAzure sottoscrizione RBAC tramite](#grained-rbac)</li></ul> |
| **Limite di trust di Service Fabric** | <ul><li>[Limitare le operazioni toocluster di accesso del client utilizzando RBAC](#cluster-rbac)</li></ul> |
| **Dynamics CRM** | <ul><li>[Eseguire la modellazione di sicurezza e usare la sicurezza a livello di campo quando richiesto](#modeling-field)</li></ul> |
| **Portale di Dynamics CRM** | <ul><li>[Eseguire la modellazione di sicurezza di portale account tenendo in considerazione il modello di sicurezza hello per portale hello è diverso dal resto hello di CRM](#portal-security)</li></ul> |
| **Archiviazione di Azure** | <ul><li>[Concedere l'autorizzazione con granularità fine in un intervallo di entità nell'archiviazione tabelle di Azure](#permission-entities)</li><li>[Abilitare l'account di archiviazione tooAzure di controllo di accesso basato sui ruoli (RBAC) tramite Gestione risorse di Azure](#rbac-azure-manager)</li></ul> |
| **Client per dispositivi mobili** | <ul><li>[Implementare il rilevamento implicito di jailbreak o rooting](#rooting-detection)</li></ul> |
| **WCF** | <ul><li>[Riferimento debole alla classe in WCF](#weak-class-wcf)</li><li>[WCF: implementare il controllo di autorizzazione](#wcf-authz)</li></ul> |
| **API Web** | <ul><li>[Implementare il meccanismo di autorizzazione appropriato nell'API Web ASP.NET](#authz-aspnet)</li></ul> |
| **Dispositivo IoT** | <ul><li>[Eseguire controlli di autorizzazione nel dispositivo hello se supporta varie azioni che richiedono diversi livelli di autorizzazione](#device-permission)</li></ul> |
| **Gateway IoT sul campo** | <ul><li>[Eseguire controlli di autorizzazione nel campo Gateway hello se supporta varie azioni che richiedono diversi livelli di autorizzazione](#field-permission)</li></ul> |

## <a id="acl-restricted-access"></a>Verificare che l'ACL appropriati siano configurati toorestrict non autorizzato accesso toodata sul dispositivo hello

| Titolo                   | Dettagli      |
| ----------------------- | ------------ |
| **Componente**               | Limite di trust dei computer | 
| **Fase SDL**               | Distribuzione |  
| **Tecnologie applicabili** | Generico |
| **Attributes (Attributi) (Attributi)**              | N/D  |
| **Riferimenti**              | N/D  |
| **Passaggi** | Verificare che l'ACL appropriati siano configurati toorestrict non autorizzato accesso toodata sul dispositivo hello|

## <a id="sensitive-directory"></a>Verificare che il contenuto sensibile dell'applicazione specifico dell'utente venga archiviato nella directory del profilo utente

| Titolo                   | Dettagli      |
| ----------------------- | ------------ |
| **Componente**               | Limite di trust dei computer | 
| **Fase SDL**               | Distribuzione |  
| **Tecnologie applicabili** | Generico |
| **Attributes (Attributi) (Attributi)**              | N/D  |
| **Riferimenti**              | N/D  |
| **Passaggi** | Verificare che il contenuto sensibile dell'applicazione specifico dell'utente venga archiviato nella directory del profilo utente. Si tratta di tooprevent più utenti di hello del computer di accedere ai dati reciproci.|

## <a id="deployed-privileges"></a>Verificare che le applicazioni distribuita hello vengono eseguite con privilegi minimi

| Titolo                   | Dettagli      |
| ----------------------- | ------------ |
| **Componente**               | Limite di trust dei computer | 
| **Fase SDL**               | Distribuzione |  
| **Tecnologie applicabili** | Generico |
| **Attributes (Attributi) (Attributi)**              | N/D  |
| **Riferimenti**              | N/D  |
| **Passaggi** | Verificare che l'applicazione hello distribuito venga eseguita con privilegi minimi. |

## <a id="sequential-logic"></a>Applicare l'ordine dei passaggi in sequenza durante l'elaborazione di flussi di logica di business

| Titolo                   | Dettagli      |
| ----------------------- | ------------ |
| **Componente**               | Applicazione Web. | 
| **Fase SDL**               | Compilare |  
| **Tecnologie applicabili** | Generico |
| **Attributes (Attributi) (Attributi)**              | N/D  |
| **Riferimenti**              | N/D  |
| **Passaggi** | In ordine tooverify cui questa fase è stata eseguita da un utente autentico desiderato tooenforce hello applicazione tooonly business logica flussi del processo in ordine sequenziale passaggio, con tutti i passaggi in fase di elaborazione in tempo umano realistici e non elaborare in ordine, ignorato i passaggi, elaborati i passaggi da un altro utente o inviata troppo rapidamente le transazioni.|

## <a id="rate-enumeration"></a>Implementare l'enumerazione tooprevent meccanismo di limitazione della frequenza

| Titolo                   | Dettagli      |
| ----------------------- | ------------ |
| **Componente**               | Applicazione Web. | 
| **Fase SDL**               | Compilare |  
| **Tecnologie applicabili** | Generico |
| **Attributes (Attributi) (Attributi)**              | N/D  |
| **Riferimenti**              | N/D  |
| **Passaggi** | Assicurarsi che gli identificatori sensibili siano casuali. Implementare il controllo CAPTCHA nelle pagine anonime. Verificare che errori ed eccezioni non rivelino dati specifici|

## <a id="principle-least-privilege"></a>Verificare che sia presente l'autorizzazione necessaria e che venga seguito il principio dei privilegi minimi

| Titolo                   | Dettagli      |
| ----------------------- | ------------ |
| **Componente**               | Applicazione Web. | 
| **Fase SDL**               | Compilare |  
| **Tecnologie applicabili** | Generico |
| **Attributes (Attributi) (Attributi)**              | N/D  |
| **Riferimenti**              | N/D  |
| **Passaggi** | <p>principio di Hello significa che un account utente solo i privilegi che sono essenziali toothat utenti lavoro. Ad esempio, un utente per il backup non è necessario software tooinstall: pertanto, l'utente per il backup hello ha le applicazioni di backup e legate al backup toorun solo dei diritti. Gli altri privilegi, ad esempio l'installazione di nuovo software, saranno bloccati. Hello principio è applicabile anche tooa personal computer utente che ha in genere funzionano in un normale account utente, viene aperto un account con privilegi, protetto da password (ovvero, un utente avanzato) solo quando la situazione hello assolutamente lo richiede. </p><p>Questo principio può anche essere applicato tooyour le applicazioni web. Invece di base esclusivamente sui metodi di autenticazione basata sui ruoli usando le sessioni, piuttosto vogliamo tooassign privilegi toousers mezzo di un sistema di autenticazione basato su Database. È comunque possibile utilizzare le sessioni in ordine tooidentify se hello utente è stato eseguito correttamente, solo ora invece di assegnare l'utente a un ruolo specifico, che abbiamo assegnare quest'ultimo con privilegi tooverify quali azioni è tooperform con privilegi nel sistema hello. Anche un grande pro di questo metodo è ogni volta che un utente ha toobe assegnati privilegi meno che le modifiche verranno applicate in tempo reale hello poiché l'assegnazione di hello non dipende dalla sessione hello che aveva prima tooexpire in caso contrario.</p>|

## <a id="logic-request-parameters"></a>Le decisioni riguardanti la logica di business e l'autorizzazione di accesso alle risorse non devono basarsi sui parametri di richiesta in ingresso

| Titolo                   | Dettagli      |
| ----------------------- | ------------ |
| **Componente**               | Applicazione Web. | 
| **Fase SDL**               | Compilare |  
| **Tecnologie applicabili** | Generico |
| **Attributes (Attributi) (Attributi)**              | N/D  |
| **Riferimenti**              | N/D  |
| **Passaggi** | Ogni volta che si stia controllando se un utente è limitato tooreview determinati dati, accesso hello restrizioni devono essere elaborato sul lato server. userID Hello devono essere archiviati all'interno di una variabile di sessione su account di accesso e devono essere utilizzati tooretrieve utente dati dal database hello |

### <a name="example"></a>Esempio
```SQL
SELECT data 
FROM personaldata 
WHERE userID=:id < - session var 
```
Ora un possibile attacco può non alterare e modificare l'operazione di applicazione hello poiché l'identificatore per il recupero dei dati sono hello hello gestita sul lato server.

## <a id="enumerable-browsing"></a>Verificare che il contenuto e le risorse non siano enumerabili o accessibili tramite browsing forzato

| Titolo                   | Dettagli      |
| ----------------------- | ------------ |
| **Componente**               | Applicazione Web. | 
| **Fase SDL**               | Compilare |  
| **Tecnologie applicabili** | Generico |
| **Attributes (Attributi) (Attributi)**              | N/D  |
| **Riferimenti**              | N/D  |
| **Passaggi** | <p>I file riservati statici e di configurazione non devono essere conservati in hello web radice. Per contenuto toobe obbligatorio non pubblici, applicare controlli di accesso appropriato o la rimozione di hello contenuto stesso.</p><p>Inoltre, esplorazione forzata è solitamente combinato con informazioni toogather tecniche di attacchi di forza bruta tentando tooaccess tutti gli URL come possibili tooenumerate directory e file in un server. Gli utenti malintenzionati possono cercare tutte le varianti dei file comunemente esistenti. La ricerca di file di password include ad esempio file come psswd.txt, password.htm, password.dat e altre varianti.</p><p>Questa funzionalità per il rilevamento di attacchi di forza bruta toomitigate prova deve essere incluso.</p>|

## <a id="privileged-server"></a>Verificare che l'account con privilegi minimi siano utilizzati tooconnect tooDatabase server

| Titolo                   | Dettagli      |
| ----------------------- | ------------ |
| **Componente**               | Database | 
| **Fase SDL**               | Compilare |  
| **Tecnologie applicabili** | Generico |
| **Attributes (Attributi) (Attributi)**              | N/D  |
| **Riferimenti**              | [Gerarchia delle autorizzazioni del database SQL](https://msdn.microsoft.com/library/ms191465), [Entità a protezione diretta del database SQL](https://msdn.microsoft.com/library/ms190401) |
| **Passaggi** | Account con privilegi minimi deve essere utilizzato tooconnect toohello database. Account di accesso dell'applicazione deve essere limitata nel database di hello e devono essere eseguiti solo stored procedure selezionate. L'account di accesso dell'applicazione non deve avere accesso diretto alle tabelle. |

## <a id="rls-tenants"></a>Implementare i tenant di sicurezza di livello di riga tooprevent l'accesso ai dati reciproci

| Titolo                   | Dettagli      |
| ----------------------- | ------------ |
| **Componente**               | Database | 
| **Fase SDL**               | Compilare |  
| **Tecnologie applicabili** | SQL Azure, locale |
| **Attributes (Attributi) (Attributi)**              | Versione SQL: 12, versione SQL: MSSQL2016 |
| **Riferimenti**              | [Sicurezza a livello di riga di SQL Server](https://msdn.microsoft.com/library/azure/dn765131.aspx) |
| **Passaggi** | <p>Sicurezza a livello di riga consente ai clienti toocontrol accesso toorows in una tabella di database in base alle caratteristiche di hello dell'utente hello esegue una query (ad esempio, gruppo appartenenza o l'esecuzione del contesto).</p><p>Sicurezza a livello di riga (riga) semplifica la progettazione di hello e la codifica della sicurezza nell'applicazione. E consente le restrizioni tooimplement sull'accesso alle righe di dati. Ad esempio assicurandosi che i lavoratori possano accedere solo le righe di dati che sono pertinenti tootheir reparto o limitare i dati rilevanti tootheir società di un cliente dati accesso tooonly hello.</p><p>logica di restrizione di accesso Hello si trova sul livello di database hello piuttosto che distante dai dati hello in un altro livello applicazione. sistema di database Hello applica restrizioni di accesso di hello ogni volta che viene eseguito un tentativo di accesso ai dati da qualsiasi livello. In questo modo il sistema di sicurezza hello più affidabile e solido grazie alla riduzione della superficie di attacco di hello hello del sistema di sicurezza.</p><p>|

Si noti come una funzionalità di database della casella di tale riga è applicabile tooSQL solo Server a partire da 2016 e database SQL di Azure. Se non viene implementata funzionalità di hello della casella di riga, è opportuno che l'accesso ai dati sia limitato utilizzando le viste e procedure

## <a id="sysadmin-users"></a>Il ruolo sysadmin deve avere solo utenti necessari validi

| Titolo                   | Dettagli      |
| ----------------------- | ------------ |
| **Componente**               | Database | 
| **Fase SDL**               | Compilare |  
| **Tecnologie applicabili** | Generico |
| **Attributes (Attributi) (Attributi)**              | N/D  |
| **Riferimenti**              | [Gerarchia delle autorizzazioni del database SQL](https://msdn.microsoft.com/library/ms191465), [Entità a protezione diretta del database SQL](https://msdn.microsoft.com/library/ms190401) |
| **Passaggi** | I membri del ruolo predefinito del server SysAdmin hello devono essere molto limitato e non possono mai contenere gli account utilizzati dalle applicazioni.  Rivedere l'elenco hello degli utenti nel ruolo hello e rimuovere gli account non necessari|

## <a id="cloud-least-privileged"></a>Connessione Gateway tooCloud utilizzando i token con privilegi minimi

| Titolo                   | Dettagli      |
| ----------------------- | ------------ |
| **Componente**               | Gateway IoT cloud | 
| **Fase SDL**               | Distribuzione |  
| **Tecnologie applicabili** | Generico |
| **Attributes (Attributi) (Attributi)**              | Opzione gateway: Hub IoT di Azure |
| **Riferimenti**              | [Controllo di accesso dell'hub IoT](https://azure.microsoft.com/documentation/articles/iot-hub-devguide/#Security) |
| **Passaggi** | Fornire privilegi minimi componenti toovarious autorizzazioni che si connettono tooCloud Gateway (IoT Hub). Esempio tipico: il componente di gestione/provisioning di dispositivi usa registryread/write, l'elaboratore eventi (ASA) usa Connessione servizio. I singoli dispositivi si connettono usando le credenziali dispositivo|

## <a id="sendonly-sas"></a>Usare una chiave di firma di accesso condiviso per autorizzazioni di solo invio per la generazione di token di dispositivo

| Titolo                   | Dettagli      |
| ----------------------- | ------------ |
| **Componente**               | Hub eventi di Azure | 
| **Fase SDL**               | Compilare |  
| **Tecnologie applicabili** | Generico |
| **Attributes (Attributi) (Attributi)**              | N/D  |
| **Riferimenti**              | [Panoramica del modello di sicurezza e autenticazione di Hub eventi](https://azure.microsoft.com/documentation/articles/event-hubs-authentication-and-security-model-overview/) |
| **Passaggi** | Una chiave di firma di accesso condiviso è toogenerate utilizzati token di singoli dispositivi. Utilizzare una chiave SAS le autorizzazioni di sola trasmissione durante il token del dispositivo hello generazione per un server di pubblicazione specificato|

## <a id="access-tokens-hub"></a>Non utilizzare i token di accesso che forniscono l'accesso diretto toohello Hub eventi

| Titolo                   | Dettagli      |
| ----------------------- | ------------ |
| **Componente**               | Hub eventi di Azure | 
| **Fase SDL**               | Compilare |  
| **Tecnologie applicabili** | Generico |
| **Attributes (Attributi) (Attributi)**              | N/D  |
| **Riferimenti**              | [Panoramica del modello di sicurezza e autenticazione di Hub eventi](https://azure.microsoft.com/documentation/articles/event-hubs-authentication-and-security-model-overview/) |
| **Passaggi** | Un token che concede l'hub di eventi di accesso diretto toohello non deve essere assegnato toohello dispositivo. Usando un token con privilegiato minimi per il dispositivo hello che concede l'accesso tooa solo server di pubblicazione consente di identificare e disattivare, se trovato toobe malintenzionati o dispositivo compromesso.|

## <a id="sas-minimum-permissions"></a>Connettersi tooEvent Hub utilizzando SAS chiavi che dispone delle autorizzazioni minime hello obbligatori

| Titolo                   | Dettagli      |
| ----------------------- | ------------ |
| **Componente**               | Hub eventi di Azure | 
| **Fase SDL**               | Compilare |  
| **Tecnologie applicabili** | Generico |
| **Attributes (Attributi) (Attributi)**              | N/D  |
| **Riferimenti**              | [Panoramica del modello di sicurezza e autenticazione di Hub eventi](https://azure.microsoft.com/documentation/articles/event-hubs-authentication-and-security-model-overview/) |
| **Passaggi** | Fornire privilegi minimi autorizzazioni toovarious applicazioni back-end che si connettono toohello Hub eventi. Generare le chiavi di firma di accesso condiviso separate per ogni applicazione back-end e fornire solo le autorizzazioni necessarie hello - toothem invio, ricezione o di gestione.|

## <a id="resource-docdb"></a>Risorsa token tooconnect tooCosmos DB ogni volta che è possibile utilizzare

| Titolo                   | Dettagli      |
| ----------------------- | ------------ |
| **Componente**               | Azure DocumentDB | 
| **Fase SDL**               | Compilare |  
| **Tecnologie applicabili** | Generico |
| **Attributes (Attributi) (Attributi)**              | N/D  |
| **Riferimenti**              | N/D  |
| **Passaggi** | Un token della risorsa è associato a una risorsa di autorizzazione DocumentDB e acquisizioni hello relazione tra utente hello di un'autorizzazione di database e hello dispone di tale utente per una risorsa di applicazione DocumentDB specifica (ad esempio, collection, documento). Utilizzare sempre un hello tooaccess token risorsa DocumentDB se client hello non può essere considerato attendibile con la gestione delle chiavi master o di sola lettura, ad esempio un'applicazione utente finale, ad esempio un client mobile o desktop. Utilizzare la chiave Master o le chiavi di sola lettura da applicazioni back-end che consente di archiviare queste chiavi in modo sicuro.|

## <a id="grained-rbac"></a>Abilitare la gestione di accesso con granularità fine tooAzure sottoscrizione RBAC tramite

| Titolo                   | Dettagli      |
| ----------------------- | ------------ |
| **Componente**               | Limite di trust di Azure | 
| **Fase SDL**               | Compilare |  
| **Tecnologie applicabili** | Generico |
| **Attributes (Attributi) (Attributi)**              | N/D  |
| **Riferimenti**              | [Utilizzare le risorse di sottoscrizione di Azure tooyour accesso toomanage assegnazioni ruolo](https://azure.microsoft.com/documentation/articles/role-based-access-control-configure/)  |
| **Passaggi** | Il Controllo degli accessi in base al ruolo di Azure (RBAC) consente la gestione specifica degli accessi per Azure. Usa tale controllo, è possibile concedere solo quantità di hello di accesso che gli utenti devono tooperform i processi.|

## <a id="cluster-rbac"></a>Limitare le operazioni toocluster di accesso del client utilizzando RBAC

| Titolo                   | Dettagli      |
| ----------------------- | ------------ |
| **Componente**               | Limite di trust di Service Fabric | 
| **Fase SDL**               | Distribuzione |  
| **Tecnologie applicabili** | Generico |
| **Attributes (Attributi) (Attributi)**              | Ambiente: Azure |
| **Riferimenti**              | [Controllo degli accessi in base al ruolo per i client di Service Fabric](https://azure.microsoft.com/documentation/articles/service-fabric-cluster-security-roles/) |
| **Passaggi** | <p>Azure Service Fabric supporta due tipi di controllo di accesso diversi per i client che sono connessi tooa cluster di Service Fabric: amministratore e utente. Controllo degli accessi consente hello cluster amministratore toolimit accesso toocertain le operazioni del cluster per diversi gruppi di utenti, di rendere più sicuro cluster hello.</p><p>Gli amministratori hanno capacità di toomanagement accesso completo (incluse le funzionalità di lettura/scrittura). Gli utenti, per impostazione predefinita, dispongono solo dell'accesso in lettura toomanagement funzionalità (ad esempio, funzionalità di query), hello possibilità tooresolve applicazioni e servizi e.</p><p>Specificare i ruoli client hello due (amministratore e client) in fase di creazione del cluster di hello fornendo certificati separati per ogni.</p>|

## <a id="modeling-field"></a>Eseguire la modellazione di sicurezza e usare la sicurezza a livello di campo quando richiesto

| Titolo                   | Dettagli      |
| ----------------------- | ------------ |
| **Componente**               | Dynamics CRM | 
| **Fase SDL**               | Compilare |  
| **Tecnologie applicabili** | Generico |
| **Attributes (Attributi) (Attributi)**              | N/D  |
| **Riferimenti**              | N/D  |
| **Passaggi** | Eseguire la modellazione di sicurezza e usare la sicurezza a livello di campo quando richiesto|

## <a id="portal-security"></a>Eseguire la modellazione di sicurezza di portale account tenendo in considerazione il modello di sicurezza hello per portale hello è diverso dal resto hello di CRM

| Titolo                   | Dettagli      |
| ----------------------- | ------------ |
| **Componente**               | Portale di Dynamics CRM | 
| **Fase SDL**               | Compilare |  
| **Tecnologie applicabili** | Generico |
| **Attributes (Attributi) (Attributi)**              | N/D  |
| **Riferimenti**              | N/D  |
| **Passaggi** | Eseguire la modellazione di sicurezza di portale account tenendo in considerazione il modello di sicurezza hello per portale hello è diverso dal resto hello di CRM|

## <a id="permission-entities"></a>Concedere l'autorizzazione con granularità fine in un intervallo di entità nell'archiviazione tabelle di Azure

| Titolo                   | Dettagli      |
| ----------------------- | ------------ |
| **Componente**               | Archiviazione di Azure | 
| **Fase SDL**               | Compilare |  
| **Tecnologie applicabili** | Generico |
| **Attributes (Attributi) (Attributi)**              | Tipo di archiviazione: tabella |
| **Riferimenti**              | [Modalità di accesso tooobjects nell'account di archiviazione di Azure con firma di accesso condiviso toodelegate](https://azure.microsoft.com/documentation/articles/storage-security-guide/#_data-plane-security) |
| **Passaggi** | In alcuni scenari di business, archiviazione tabelle di Azure possono essere riservati toostore obbligatorio che si occupa toodifferent parti. Ad esempio, dati sensibili relativi toodifferent paesi. In questi casi, le firme di firma di accesso condiviso possono essere costruite specificando hello riga e partizione intervalli di chiavi, in modo che un utente può accedere paese specifico tooa specifico di dati.| 

## <a id="rbac-azure-manager"></a>Abilitare l'account di archiviazione tooAzure di controllo di accesso basato sui ruoli (RBAC) tramite Gestione risorse di Azure

| Titolo                   | Dettagli      |
| ----------------------- | ------------ |
| **Componente**               | Archiviazione di Azure | 
| **Fase SDL**               | Compilare |  
| **Tecnologie applicabili** | Generico |
| **Attributes (Attributi) (Attributi)**              | N/D  |
| **Riferimenti**              | [Come toosecure account di archiviazione con il controllo di accesso basato sui ruoli (RBAC)](https://azure.microsoft.com/documentation/articles/storage-security-guide/#management-plane-security) |
| **Passaggi** | <p>Quando si crea un nuovo account di archiviazione, si seleziona un modello di distribuzione classica o di Azure Resource Manager. il modello classico Hello di creazione di risorse in Azure consente solo di sottoscrizione toohello accesso radicale e hello a sua volta, l'account di archiviazione.</p><p>Con il modello di gestione risorse di Azure hello, inserire l'account di archiviazione hello in una risorsa gruppo e controllo accesso toohello piano di gestione di account di archiviazione specifico tramite Azure Active Directory. Ad esempio, è possibile assegnare utenti specifici hello possibilità tooaccess hello chiavi account di archiviazione, mentre altri utenti possono visualizzare le informazioni sull'account di archiviazione hello, ma non è possibile accedere alle chiavi dell'account di archiviazione hello.</p>|

## <a id="rooting-detection"></a>Implementare il rilevamento implicito di jailbreak o rooting

| Titolo                   | Dettagli      |
| ----------------------- | ------------ |
| **Componente**               | Client per dispositivi mobili | 
| **Fase SDL**               | Compilare |  
| **Tecnologie applicabili** | Generico |
| **Attributes (Attributi) (Attributi)**              | N/D  |
| **Riferimenti**              | N/D  |
| **Passaggi** | <p>L'applicazione deve proteggere i propri dati di configurazione e dell'utente in caso di jailbreak o rooting del telefono. Il rooting/jailbreak implica un accesso non autorizzato che gli utenti normali non eseguono sui propri telefoni. Di conseguenza l'applicazione dovrebbe avere logica di rilevamento implicita all'avvio dell'applicazione, toodetect se phone hello è rooted.</p><p>logica di rilevamento Hello può essere semplicemente accedere ai file che in genere solo radice consente l'accesso, ad esempio:</p><ul><li>/system/app/Superuser.apk</li><li>/sbin/su</li><li>/system/bin/su</li><li>/system/xbin/su</li><li>/data/local/xbin/su</li><li>/data/local/bin/su</li><li>/system/sd/xbin/su</li><li>/system/bin/failsafe/su</li><li>/data/local/su</li></ul><p>Se un'applicazione hello può accedere a uno di questi file, indica che un'applicazione hello è in esecuzione come utente root.</p>|

## <a id="weak-class-wcf"></a>Riferimento debole alla classe in WCF

| Titolo                   | Dettagli      |
| ----------------------- | ------------ |
| **Componente**               | WCF | 
| **Fase SDL**               | Compilare |  
| **Tecnologie applicabili** | Generico, .NET Framework 3 |
| **Attributes (Attributi) (Attributi)**              | N/D  |
| **Riferimenti**              | [MSDN](https://msdn.microsoft.com/library/ff648500.aspx), [Fortify Kingdom](https://vulncat.fortify.com/en/vulncat/index.html) |
| **Passaggi** | <p>sistema di Hello utilizza un riferimento debole di classe, che potrebbe consentire un attacco codice tooexecute non autorizzato. programma Hello fa riferimento a una classe definita dall'utente che non viene identificata in modo univoco. .NET il caricamento di questa classe identificata in modo debole, hello CLR tipo caricatore Cerca classe hello in posizioni in hello seguenti hello specificato ordine:</p><ol><li>Se l'assembly hello del tipo di hello è noto, esegue la ricerca del caricatore hello hello reindirizzamento posizioni, Global Assembly Cache, hello assembly corrente del file di configurazione usando le informazioni di configurazione e hello directory base dell'applicazione</li><li>Se l'assembly hello è sconosciuto, hello caricatore ricerche hello assembly corrente, in mscorlib e percorso hello restituito dal gestore dell'evento TypeResolve hello</li><li>In questo ordine di ricerca CLR può essere modificato con hook quali hello meccanismo di inoltro dei tipi ed evento TypeResolve hello</li></ol><p>Se un utente malintenzionato sfrutta l'ordine di ricerca CLR hello creando una classe alternativa con hello stesso nome e posizionarlo in un percorso alternativo che hello CLR caricherà prima, hello CLR involontariamente eseguirà il codice fornito dal pirata informatico di hello</p>|

### <a name="example"></a>Esempio
Hello `<behaviorExtensions/>` elemento del file di configurazione WCF hello seguente indica WCF tooadd un'estensione WCF particolare comportamento personalizzato classe tooa.
```
<system.serviceModel>
    <extensions>
        <behaviorExtensions>
            <add name=""myBehavior"" type=""MyBehavior"" />
        </behaviorExtensions>
    </extensions>
</system.serviceModel>
```
L'uso di nomi completi (sicuri) identifica un tipo in modo univoco e aumenta la sicurezza del sistema. Quando si registra tipi nel file Machine. config e App. config di hello, utilizzare nomi di assembly completo.

### <a name="example"></a>Esempio
Hello `<behaviorExtensions/>` elemento del file di configurazione WCF hello seguente indica WCF tooadd riferimento forte classe tooa particolare WCF estensione di comportamento personalizzato.
```
<system.serviceModel>
    <extensions>
        <behaviorExtensions>
            <add name=""myBehavior"" type=""Microsoft.ServiceModel.Samples.MyBehaviorSection, MyBehavior,
            Version=1.0.0.0, Culture=neutral, PublicKeyToken=null"" />
        </behaviorExtensions>
    </extensions>
</system.serviceModel>
```

## <a id="wcf-authz"></a>WCF: implementare il controllo di autorizzazione

| Titolo                   | Dettagli      |
| ----------------------- | ------------ |
| **Componente**               | WCF | 
| **Fase SDL**               | Compilare |  
| **Tecnologie applicabili** | Generico, .NET Framework 3 |
| **Attributes (Attributi) (Attributi)**              | N/D  |
| **Riferimenti**              | [MSDN](https://msdn.microsoft.com/library/ff648500.aspx), [Fortify Kingdom](https://vulncat.fortify.com/en/vulncat/index.html) |
| **Passaggi** | <p>Questo servizio non usa un controllo di autorizzazione. Quando un client chiama un servizio WCF, WCF fornisce vari schemi di autorizzazione per verificare che il chiamante hello con metodo di servizio di autorizzazione tooexecute hello nel server di hello. Se i controlli di autorizzazione non sono abilitati per i servizi WCF, un utente autenticato può ottenere l'escalation dei privilegi.</p>|

### <a name="example"></a>Esempio
Quando si esegue il servizio di hello, Hello seguente configurazione indica WCF toonot controllo hello livello di autorizzazione del client hello:
```
<behaviors>
    <serviceBehaviors>
        <behavior>
            ...
            <serviceAuthorization principalPermissionMode=""None"" />
        </behavior>
    </serviceBehaviors>
</behaviors>
```
Utilizzare un tooverify lo schema di autorizzazione del servizio che hello chiamante del metodo del servizio hello è così toodo autorizzato. WCF fornisce due modalità e consente la definizione di uno schema di autorizzazione personalizzata hello. modalità UseWindowsGroups Hello utilizza utenti e ruoli di Windows e modalità UseAspNetRoles hello utilizza un provider di ruoli ASP.NET, ad esempio SQL Server, tooauthenticate.

### <a name="example"></a>Esempio
Hello configurazione seguente indica che tale client hello sia parte del gruppo Administrators hello prima dell'esecuzione hello Aggiungi servizio toomake WCF:
```
<behaviors>
    <serviceBehaviors>
        <behavior>
            ...
            <serviceAuthorization principalPermissionMode=""UseWindowsGroups"" />
        </behavior>
    </serviceBehaviors>
</behaviors>
```
servizio Hello è dichiarato come riportato di seguito hello:
```
[PrincipalPermission(SecurityAction.Demand,
Role = ""Builtin\\Administrators"")]
public double Add(double n1, double n2)
{
double result = n1 + n2;
return result;
}
```

## <a id="authz-aspnet"></a>Implementare il meccanismo di autorizzazione appropriato nell'API Web ASP.NET

| Titolo                   | Dettagli      |
| ----------------------- | ------------ |
| **Componente**               | API Web | 
| **Fase SDL**               | Compilare |  
| **Tecnologie applicabili** | Generico, MVC 5 |
| **Attributes (Attributi) (Attributi)**              | N/D, provider di identità: AD FS, provider di identità: Azure AD |
| **Riferimenti**              | [Autenticazione e autorizzazione nell'API Web ASP.NET](http://www.asp.net/web-api/overview/security/authentication-and-authorization-in-aspnet-web-api) |
| **Passaggi** | <p>Informazioni sui ruoli per gli utenti dell'applicazione hello possono essere derivate da Azure AD oppure le attestazioni ADFS se un'applicazione hello si basa su di essi come provider di identità o un'applicazione hello stesso potrebbe fornita. In ognuno di questi casi, implementazione di autorizzazione personalizzato hello deve convalidare le informazioni sui ruoli utente di hello.</p><p>Informazioni sui ruoli per gli utenti dell'applicazione hello possono essere derivate da Azure AD oppure le attestazioni ADFS se un'applicazione hello si basa su di essi come provider di identità o un'applicazione hello stesso potrebbe fornita. In ognuno di questi casi, implementazione di autorizzazione personalizzato hello deve convalidare le informazioni sui ruoli utente di hello.</p>

### <a name="example"></a>Esempio
```C#
[AttributeUsage(AttributeTargets.Class | AttributeTargets.Method, Inherited = true, AllowMultiple = true)]
public class ApiAuthorizeAttribute : System.Web.Http.AuthorizeAttribute
{
        public async override Task OnAuthorizationAsync(HttpActionContext actionContext, CancellationToken cancellationToken)
        {
            if (actionContext == null)
            {
                throw new Exception();
            }

            if (!string.IsNullOrEmpty(base.Roles))
            {
                bool isAuthorized = ValidateRoles(actionContext);
                if (!isAuthorized)
                {
                    HandleUnauthorizedRequest(actionContext);
                }
            }

            base.OnAuthorization(actionContext);
        }

public bool ValidateRoles(actionContext)
{
   //Authorization logic here; returns true or false
}

}
```
Tutti i controller di hello e metodi di azione che deve tooprotected devono essere decorati con precedenza attributo.
```C#
[ApiAuthorize]
public class CustomController : ApiController
{
     //Application code goes here
}
```

## <a id="device-permission"></a>Eseguire controlli di autorizzazione nel dispositivo hello se supporta varie azioni che richiedono diversi livelli di autorizzazione

| Titolo                   | Dettagli      |
| ----------------------- | ------------ |
| **Componente**               | Dispositivo IoT | 
| **Fase SDL**               | Compilare |  
| **Tecnologie applicabili** | Generico |
| **Attributes (Attributi) (Attributi)**              | N/D  |
| **Riferimenti**              | N/D  |
| **Passaggi** | <p>Hello dispositivo deve autorizzare hello chiamante toocheck se hello chiamante dispone di azione di hello necessarie autorizzazioni tooperform hello richiesta. Per consente ad esempio, ad esempio hello dispositivo è un blocco dello sportello Smart che può essere monitorato dal cloud hello e fornisce funzionalità come il blocco in modalità remota sportello hello.</p><p>Hello Smart Lock sportello fornisce funzionalità di sblocco solo quando un utente viene fisicamente vicino sportello hello con una scheda. In questo caso, hello implementazione del comando remoto hello e il controllo deve essere eseguita in modo che non fornisce una porta hello toounlock funzionalità gateway del cloud hello non è autorizzato toosend una porta di hello toounlock di comando.</p>|

## <a id="field-permission"></a>Eseguire controlli di autorizzazione nel campo Gateway hello se supporta varie azioni che richiedono diversi livelli di autorizzazione

| Titolo                   | Dettagli      |
| ----------------------- | ------------ |
| **Componente**               | Gateway IoT sul campo | 
| **Fase SDL**               | Compilare |  
| **Tecnologie applicabili** | Generico |
| **Attributes (Attributi) (Attributi)**              | N/D  |
| **Riferimenti**              | N/D  |
| **Passaggi** | Gateway campo Hello deve autorizzare hello chiamante toocheck se hello chiamante dispone di azione di hello necessarie autorizzazioni tooperform hello richiesta. Per ad esempio, dovrebbero essere presenti diverse autorizzazioni per un utente amministratore di interfaccia/API tooconfigure un campo gateway v/s: i dispositivi di uso che si connettono tooit.|

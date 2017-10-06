---
title: aaaAuditing e registrazione - modellazione strumento Microsoft Threat - Azure | Documenti Microsoft
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
ms.openlocfilehash: f28988833eba251b6ceb8bbd47cde37e871af609
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="security-frame-auditing-and-logging--mitigations"></a>Infrastruttura di sicurezza: controllo e registrazione | Soluzioni di riduzione 
| Prodotto o servizio | Articolo |
| --------------- | ------- |
| **Dynamics CRM**    | <ul><li>[Identificare le entità sensibili nella soluzione e implementare il controllo delle modifiche](#sensitive-entities)</li></ul> |
| **Applicazione Web** | <ul><li>[Verificare che il controllo e la registrazione viene applicata in un'applicazione hello](#auditing)</li><li>[Assicurarsi che la rotazione e la separazione dei log siano abilitate](#log-rotation)</li><li>[Verificare che un'applicazione hello non registra i dati riservati dell'utente](#log-sensitive-data)</li><li>[Assicurarsi che l'accesso ai file di log e di controllo sia limitato](#log-restricted-access)</li><li>[Assicurarsi che gli eventi di Gestione utenti vengano registrati nel log](#user-management)</li><li>[Assicurarsi che il sistema hello abbia incorporate difese contro un utilizzo improprio](#inbuilt-defenses)</li><li>[Abilitare la registrazione diagnostica per le app Web nel servizio app di Azure](#diagnostics-logging)</li></ul> |
| **Database** | <ul><li>[Verificare che il controllo degli accessi sia abilitato in SQL Server](#identify-sensitive-entities)</li><li>[Abilitare il rilevamento delle minacce in SQL Azure](#threat-detection)</li></ul> |
| **Archiviazione di Azure** | <ul><li>[Usare l'accesso tooaudit Analitica di archiviazione di Azure di archiviazione di Azure](#analytics)</li></ul> |
| **WCF** | <ul><li>[Implementare un livello di registrazione sufficiente](#sufficient-logging)</li><li>[Implementare un livello di gestione degli errori di controllo sufficiente](#audit-failure-handling)</li></ul> |
| **API Web** | <ul><li>[Assicurarsi che la funzionalità di controllo e registrazione venga applicata nell'API Web](#logging-web-api)</li></ul> |
| **Gateway IoT sul campo** | <ul><li>[Assicurarsi che la funzionalità di controllo e registrazione appropriata venga applicata nel gateway sul campo](#logging-field-gateway)</li></ul> |
| **Gateway IoT cloud** | <ul><li>[Assicurarsi che la funzionalità di controllo e registrazione appropriata venga applicata nel gateway nel cloud](#logging-cloud-gateway)</li></ul> |

## <a id="sensitive-entities"></a>Identificare le entità sensibili nella soluzione e implementare il controllo delle modifiche

| Titolo                   | Dettagli      |
| ----------------------- | ------------ |
| **Componente**               | Dynamics CRM | 
| **Fase SDL**               | Compilare |  
| **Tecnologie applicabili** | Generico |
| **Attributes (Attributi) (Attributi)**              | N/D  |
| **Riferimenti**              | N/D  |
| **Passaggi**                   | Identificare le entità nella soluzione che contengono dati sensibili e implementare il controllo delle modifiche in tali entità e campi |

## <a id="auditing"></a>Verificare che il controllo e la registrazione viene applicata in un'applicazione hello

| Titolo                   | Dettagli      |
| ----------------------- | ------------ |
| **Componente**               | Applicazione Web. | 
| **Fase SDL**               | Compilare |  
| **Tecnologie applicabili** | Generico |
| **Attributes (Attributi) (Attributi)**              | N/D  |
| **Riferimenti**              | N/D  |
| **Passaggi**                   | Abilitare il controllo e la registrazione su tutti i componenti. I log di controllo devono acquisire il contesto utente. Identificare tutti gli eventi importanti e registrarli nel log. Implementare la registrazione centralizzata |

## <a id="log-rotation"></a>Assicurarsi che la rotazione e la separazione dei log siano abilitate

| Titolo                   | Dettagli      |
| ----------------------- | ------------ |
| **Componente**               | Applicazione Web. | 
| **Fase SDL**               | Compilare |  
| **Tecnologie applicabili** | Generico |
| **Attributes (Attributi) (Attributi)**              | N/D  |
| **Riferimenti**              | N/D  |
| **Passaggi**                   | <p>La rotazione dei log è un processo automatizzato usato nell'amministrazione di sistema che prevede l'archiviazione dei file di log datati. Server che esegue applicazioni di grandi dimensioni, spesso di registrare qualsiasi richiesta: in faccia hello dei registri ingombranti, rotazione del log è un hello toolimit modo totale dimensioni dei log hello consentendo l'analisi degli eventi recenti. </p><p>La separazione dei log in pratica è pertanto necessario toostore i file di log in una partizione diversa come in cui l'applicazione o sistema operativo è in esecuzione in ordine tooavert un attacco Denial of service attaccano o hello downgrade dell'applicazione, le prestazioni</p>|

## <a id="log-sensitive-data"></a>Verificare che un'applicazione hello non registra i dati riservati dell'utente

| Titolo                   | Dettagli      |
| ----------------------- | ------------ |
| **Componente**               | Applicazione Web. | 
| **Fase SDL**               | Compilare |  
| **Tecnologie applicabili** | Generico |
| **Attributes (Attributi) (Attributi)**              | N/D  |
| **Riferimenti**              | N/D  |
| **Passaggi**                   | <p>Verificare che non si effettua tutti i dati riservati che un utente invia tooyour sito. Verificare la registrazione intenzionale, nonché gli effetti collaterali causati da problemi di progettazione. Esempi di dati sensibili:</p><ul><li>Credenziali dell'utente</li><li>Codice fiscale o altre informazioni di identificazione</li><li>Numeri di carta di credito o altre informazioni finanziarie</li><li>Informazioni sulla salute</li><li>Le chiavi private o altri dati che può essere utilizzato toodecrypt informazioni crittografate</li><li>Informazioni di sistema o un'applicazione che possono essere usate toomore attacchi in modo efficace applicazione hello</li></ul>|

## <a id="log-restricted-access"></a>Assicurarsi che l'accesso ai file di log e di controllo sia limitato

| Titolo                   | Dettagli      |
| ----------------------- | ------------ |
| **Componente**               | Applicazione Web. | 
| **Fase SDL**               | Compilare |  
| **Tecnologie applicabili** | Generico |
| **Attributes (Attributi) (Attributi)**              | N/D  |
| **Riferimenti**              | N/D  |
| **Passaggi**                   | <p>Controllare i file toolog diritti di accesso tooensure sono impostati in modo appropriato. Gli account dell'applicazione devono avere l'accesso in sola scrittura, mentre gli operatori e il personale di supporto devono disporre dell'accesso in sola lettura a seconda delle esigenze.</p><p>Gli account di amministratori sono hello solo gli account che devono avere accesso completo. Controllare il che ACL di Windows nel log file tooensure sono soggetti a restrizioni correttamente:</p><ul><li>Gli account dell'applicazione devono disporre dell'accesso in sola scrittura</li><li>Gli operatori e il personale di supporto devono disporre dell'accesso in sola lettura a seconda delle esigenze</li><li>Gli amministratori sono hello solo gli account che devono avere accesso completo</li></ul>|

## <a id="user-management"></a>Assicurarsi che gli eventi di Gestione utenti vengano registrati nel log

| Titolo                   | Dettagli      |
| ----------------------- | ------------ |
| **Componente**               | Applicazione Web. | 
| **Fase SDL**               | Compilare |  
| **Tecnologie applicabili** | Generico |
| **Attributes (Attributi) (Attributi)**              | N/D  |
| **Riferimenti**              | N/D  |
| **Passaggi**                   | <p>Assicurarsi che l'applicazione hello controlla gli eventi di gestione utente, ad esempio account di accesso riusciti e non utente, reimpostazione delle password, le modifiche delle password, il blocco degli account, la registrazione utente. In questo modo consente toodetect e reazione toopotentially di comportamenti sospetti. Consente inoltre di dati delle operazioni toogather; ad esempio, tootrack che accede a un'applicazione hello</p>|

## <a id="inbuilt-defenses"></a>Assicurarsi che il sistema hello abbia incorporate difese contro un utilizzo improprio

| Titolo                   | Dettagli      |
| ----------------------- | ------------ |
| **Componente**               | Applicazione Web. | 
| **Fase SDL**               | Compilare |  
| **Tecnologie applicabili** | Generico |
| **Attributes (Attributi) (Attributi)**              | N/D  |
| **Riferimenti**              | N/D  |
| **Passaggi**                   | <p>È necessario impostare dei controlli che generino un'eccezione di sicurezza in caso di utilizzo improprio dell'applicazione. Ad esempio, se è attiva la convalida dell'input e un utente malintenzionato tenta di codice dannoso tooinject che non corrisponde a regex hello, un'eccezione di sicurezza può essere generata che può essere un indicativo di un utilizzo improprio del sistema</p><p>Ad esempio, si consiglia di eccezioni di sicurezza toohave registrate e le azioni intraprese per hello seguenti problemi:</p><ul><li>Convalida dell'input</li><li>Violazioni di richiesta intersito falsa</li><li>Attacchi di forza bruta (limite massimo del numero di richieste per utente per risorsa)</li><li>Violazioni di caricamento file</li><ul>|

## <a id="diagnostics-logging"></a>Abilitare la registrazione diagnostica per le app Web nel servizio app di Azure

| Titolo                   | Dettagli      |
| ----------------------- | ------------ |
| **Componente**               | Applicazione Web. | 
| **Fase SDL**               | Compilare |  
| **Tecnologie applicabili** | Generico |
| **Attributes (Attributi) (Attributi)**              | Tipo di ambiente: Azure |
| **Riferimenti**              | N/D  |
| **Passaggi** | <p>Azure offre tooassist di diagnostica con il debug di un'applicazione di servizio app web. Si applica anche tooAPI App e App per dispositivi mobili. Le applicazioni di servizio App web forniscono funzionalità di diagnostica per la registrazione delle informazioni dal server web hello e un'applicazione web hello.</p><p>logicamente separate in diagnostica server Web e diagnostica applicazioni.</p>|

## <a id="identify-sensitive-entities"></a>Verificare che il controllo degli accessi sia abilitato in SQL Server

| Titolo                   | Dettagli      |
| ----------------------- | ------------ |
| **Componente**               | Database | 
| **Fase SDL**               | Compilare |  
| **Tecnologie applicabili** | Generico |
| **Attributes (Attributi) (Attributi)**              | N/D  |
| **Riferimenti**              | [Configurare il controllo degli accessi](https://msdn.microsoft.com/library/ms175850.aspx) |
| **Passaggi** | <p>Il controllo degli accessi al Server di database deve essere abilitato toodetect/Conferma password informatico. È importante tentativi di accesso non riusciti toocapture. L'acquisizione dei tentativi di accesso riusciti e non offre vantaggi aggiuntivi nelle indagini forensi</p>|

## <a id="threat-detection"></a>Abilitare il rilevamento delle minacce in SQL Azure

| Titolo                   | Dettagli      |
| ----------------------- | ------------ |
| **Componente**               | Database | 
| **Fase SDL**               | Compilare |  
| **Tecnologie applicabili** | SQL Azure |
| **Attributes (Attributi) (Attributi)**              | Versione SQL: 12 |
| **Riferimenti**              | [Introduzione al rilevamento delle minacce nel database SQL](https://azure.microsoft.com/documentation/articles/sql-database-threat-detection-get-started/)|
| **Passaggi** |<p>Rilevamento minacce consente attività di database anomale che possono indicare potenziali database toohello rischi di sicurezza. Fornisce un nuovo livello di sicurezza, che consente ai clienti toodetect e risposta toopotential minacce che si verificano fornendo gli avvisi di sicurezza sull'attività anomale.</p><p>Gli utenti possono esplorare eventi sospetti di hello utilizzando Azure SQL Database Auditing toodetermine se sono il risultato di un tentativo tooaccess, violazioni o sfruttare i dati nel database di hello.</p><p>Rilevamento minacce rende semplice tooaddress potenziali minacce toohello database di senza necessità di hello toobe un esperto della sicurezza o gestire i sistemi di monitoraggio di sicurezza avanzata</p>|

## <a id="analytics"></a>Usare l'accesso tooaudit Analitica di archiviazione di Azure di archiviazione di Azure

| Titolo                   | Dettagli      |
| ----------------------- | ------------ |
| **Componente**               | Archiviazione di Azure | 
| **Fase SDL**               | Distribuzione |  
| **Tecnologie applicabili** | Generico |
| **Attributes (Attributi) (Attributi)**              | N/D |
| **Riferimenti**              | [Utilizzando il tipo di autorizzazione toomonitor Analitica di archiviazione](https://azure.microsoft.com/documentation/articles/storage-security-guide/#storage-analytics) |
| **Passaggi** | <p>Per ogni account di archiviazione, una possibile abilitare la registrazione di tooperform Analitica di archiviazione di Azure e archiviare i dati di metrica. i log di Hello archiviazione analitica forniscono importanti informazioni quali il metodo di autenticazione utilizzato da un utente durante l'accesso di archiviazione.</p><p>Può essere molto utile se si è strettamente protegge toostorage di accesso. Ad esempio, nell'archiviazione Blob, è possibile impostare tutte tooprivate contenitori hello e implementare l'utilizzo di hello di un servizio di firma di accesso condiviso all'interno delle applicazioni. È quindi possibile controllare hello registra regolarmente toosee se i BLOB sono accessibili tramite chiavi account di archiviazione di hello che potrebbero indicare una violazione della sicurezza, o se BLOB hello sono pubblici, ma non deve essere.</p>|

## <a id="sufficient-logging"></a>Implementare un livello di registrazione sufficiente

| Titolo                   | Dettagli      |
| ----------------------- | ------------ |
| **Componente**               | WCF | 
| **Fase SDL**               | Compilare |  
| **Tecnologie applicabili** | .NET Framework |
| **Attributes (Attributi) (Attributi)**              | N/D  |
| **Riferimenti**              | [MSDN](https://msdn.microsoft.com/library/ff648500.aspx), [Fortify Kingdom](https://vulncat.fortify.com/en/vulncat/index.html) |
| **Passaggi** | <p>mancanza di Hello di un itinerario di controllo appropriata dopo un attacco può compromettere sforzi forensi. Windows Communication Foundation (WCF) offre i tentativi di autenticazione ha esito positivo e/o non riusciti toolog di hello possibilità.</p><p>La registrazione dei tentativi di autenticazione non riusciti può avvisare gli amministratori di potenziali attacchi di forza bruta. Analogamente, la registrazione di eventi di autenticazione riusciti può offrire una utile audit trail in presenza di compromissioni dei account validi. Abilitare la funzionalità di controllo di sicurezza del servizio di WCF |

### <a name="example"></a>Esempio
Hello seguito è riportato un esempio di configurazione con il controllo abilitato
```
<system.serviceModel>
    <behaviors>
        <serviceBehaviors>
            <behavior name=""NewBehavior"">
                <serviceSecurityAudit auditLogLocation=""Default""
                suppressAuditFailure=""false"" 
                serviceAuthorizationAuditLevel=""SuccessAndFailure""
                messageAuthenticationAuditLevel=""SuccessAndFailure"" />
                ...
            </behavior>
        </servicebehaviors>
    </behaviors>
</system.serviceModel>
```

## <a id="audit-failure-handling"></a>Implementare un livello di gestione degli errori di controllo sufficiente

| Titolo                   | Dettagli      |
| ----------------------- | ------------ |
| **Componente**               | WCF | 
| **Fase SDL**               | Compilare |  
| **Tecnologie applicabili** | .NET Framework |
| **Attributes (Attributi) (Attributi)**              | N/D  |
| **Riferimenti**              | [MSDN](https://msdn.microsoft.com/library/ff648500.aspx), [Fortify Kingdom](https://vulncat.fortify.com/en/vulncat/index.html) |
| **Passaggi** | <p>Soluzione sviluppata è configurato non toogenerate un'eccezione in caso di log di controllo tooan toowrite. Se è configurato WCF non toothrow un'eccezione quando è Impossibile toowrite tooan log di controllo, non verrà notificato programma hello dell'errore hello e controllo di eventi critico per la protezione potrebbe non verificarsi.</p>|

### <a name="example"></a>Esempio
Hello `<behavior/>` elemento del file di configurazione WCF hello seguente indica WCF toonot notificano applicazione hello WCF ha esito negativo toowrite tooan log di controllo.
````
<behaviors>
    <serviceBehaviors>
        <behavior name="NewBehavior">
            <serviceSecurityAudit auditLogLocation="Application"
            suppressAuditFailure="true"
            serviceAuthorizationAuditLevel="Success"
            messageAuthenticationAuditLevel="Success" />
        </behavior>
    </serviceBehaviors>
</behaviors>
````
Ogni volta che è Impossibile toowrite tooan log di controllo, configurare programma hello toonotify WCF. il programma di Hello deve disporre di uno schema di notifica alternativo nell'organizzazione di hello tooalert sul posto che gli itinerari di controllo non viene gestiti. 

## <a id="logging-web-api"></a>Assicurarsi che la funzionalità di controllo e registrazione venga applicata nell'API Web

| Titolo                   | Dettagli      |
| ----------------------- | ------------ |
| **Componente**               | API Web | 
| **Fase SDL**               | Compilare |  
| **Tecnologie applicabili** | Generico |
| **Attributes (Attributi) (Attributi)**              | N/D  |
| **Riferimenti**              | N/D  |
| **Passaggi** | Abilitare il controllo e la registrazione su tutte le API Web. I log di controllo devono acquisire il contesto utente. Identificare tutti gli eventi importanti e registrarli nel log. Implementare la registrazione centralizzata |

## <a id="logging-field-gateway"></a>Assicurarsi che la funzionalità di controllo e registrazione appropriata venga applicata nel gateway sul campo

| Titolo                   | Dettagli      |
| ----------------------- | ------------ |
| **Componente**               | Gateway IoT sul campo | 
| **Fase SDL**               | Compilare |  
| **Tecnologie applicabili** | Generico |
| **Attributes (Attributi) (Attributi)**              | N/D  |
| **Riferimenti**              | N/D  |
| **Passaggi** | <p>Quando più dispositivi si connettono tooa campo Gateway, verificare che i tentativi di connessione e lo stato di autenticazione (esito positivo o negativo) per i singoli dispositivi sono registrati e gestite nel campo Gateway hello.</p><p>Inoltre, nei casi in cui il Gateway campo gestisce hello IoT Hub le credenziali per i singoli dispositivi, verificare che il controllo viene eseguito quando queste credenziali vengono recuperate. Sviluppare un processo tooperiodically caricamento hello registri tooAzure IoT Hub o dell'archiviazione per la conservazione a lungo termine.</p> |

## <a id="logging-cloud-gateway"></a>Assicurarsi che la funzionalità di controllo e registrazione appropriata venga applicata nel gateway nel cloud

| Titolo                   | Dettagli      |
| ----------------------- | ------------ |
| **Componente**               | Gateway IoT cloud | 
| **Fase SDL**               | Compilare |  
| **Tecnologie applicabili** | Generico |
| **Attributes (Attributi) (Attributi)**              | N/D  |
| **Riferimenti**              | [Monitoraggio delle operazioni di introduzione tooIoT Hub](https://azure.microsoft.com/documentation/articles/iot-hub-operations-monitoring/) |
| **Passaggi** | <p>Progettare la raccolta e l'archiviazione dei dati di controllo raccolti tramite il monitoraggio delle operazioni IoT Hub. Abilitare hello monitoraggio categorie seguenti:</p><ul><li>Operazioni relative alle identità dei dispositivi</li><li>Comunicazioni da dispositivo a cloud</li><li>Comunicazioni da cloud a dispositivo</li><li>Connessioni</li><li>Caricamenti di file</li></ul>|

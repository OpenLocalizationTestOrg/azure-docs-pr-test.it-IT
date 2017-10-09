---
title: aaaAuthentication - modellazione strumento Microsoft Threat - Azure | Documenti Microsoft
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
ms.openlocfilehash: 06c1b1aebab25e6fb5b666d24ecd9d86085d656c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="security-frame-authentication--mitigations"></a>Infrastruttura di sicurezza: autenticazione - Procedure di mitigazione 
| Prodotto o servizio | Articolo |
| --------------- | ------- |
| **Applicazione Web**    | <ul><li>[È consigliabile utilizzare un tooWeb tooauthenticate meccanismo di autenticazione standard dell'applicazione](#standard-authn-web-app)</li><li>[Gestire in modo sicuro scenari di autenticazione non riuscita mediante le applicazioni](#handle-failed-authn)</li><li>[Abilitare l'autenticazione adattiva o incrementale](#step-up-adaptive-authn)</li><li>[Assicurarsi che le interfacce amministrative siano bloccate correttamente](#admin-interface-lockdown)</li><li>[Implementare in modo sicuro funzionalità per la password dimenticata](#forgot-pword-fxn)</li><li>[Assicurarsi che vengano implementati criteri di account e password](#pword-account-policy)</li><li>[Enumerazione di nome utente di implementare controlli tooprevent](#controls-username-enum)</li></ul> |
| **Database** | <ul><li>[Quando possibile, utilizzare l'autenticazione di Windows per la connessione Server tooSQL](#win-authn-sql)</li><li>[Quando possibile utilizzare l'autenticazione di Azure Active Directory per tooSQL connessione Database](#aad-authn-sql)</li><li>[Assicurarsi che vengano applicati i criteri di account e password in SQL Server quando viene usata la modalità di autenticazione SQL](#authn-account-pword)</li><li>[Non usare l'autenticazione SQL in database indipendenti](#autn-contained-db)</li></ul> |
| **Hub eventi di Azure** | <ul><li>[Usare credenziali di autenticazione per dispositivo con i token di firma di accesso condiviso](#authn-sas-tokens)</li></ul> |
| **Limite di trust di Azure** | <ul><li>[Abilitare Azure Multi-Factor Authentication per amministratori di Azure](#multi-factor-azure-admin)</li></ul> |
| **Limite di trust di Service Fabric** | <ul><li>[Limitare l'accesso anonimo tooService dell'infrastruttura Cluster](#anon-access-cluster)</li><li>[Assicurarsi che il certificato da client a nodo di Service Fabric sia diverso dal certificato da nodo a nodo](#fabric-cn-nn)</li><li>[Utilizzare AAD tooauthenticate client tooservice dell'infrastruttura cluster](#aad-client-fabric)</li><li>[Assicurarsi che i certificati di Service Fabric vengano ottenuti da un'Autorità di certificazione (CA) approvata](#fabric-cert-ca)</li></ul> |
| **Identity Server** | <ul><li>[Usare scenari di autenticazione standard supportati da Identity Server](#standard-authn-id)</li><li>[Eseguire l'override di cache token hello predefinita Identity Server con un'alternativa scalabile](#override-token)</li></ul> |
| **Limite di Trust del computer** | <ul><li>[Assicurarsi che i file binari dell'applicazione distribuita abbiano una firma digitale](#binaries-signed)</li></ul> |
| **WCF** | <ul><li>[Abilitare l'autenticazione quando ci si connette tooMSMQ code in WCF](#msmq-queues)</li><li>[-Non WCF non impostato toonone clientCredentialType messaggio](#message-none)</li><li>[-Non WCF non impostato trasporto clientCredentialType toonone](#transport-none)</li></ul> |
| **API Web** | <ul><li>[Verificare che le tecniche di autenticazione standard siano utilizzati toosecure API Web](#authn-secure-api)</li></ul> |
| **Azure AD** | <ul><li>[Usare scenari di autenticazione standard supportati da Azure Active Directory](#authn-aad)</li><li>[Eseguire l'override di hello ADAL token cache predefinita con un'alternativa scalabile](#adal-scalable)</li><li>[Verificare che TokenReplayCache sia riproduzione hello tooprevent utilizzati dei token di autenticazione ADAL](#tokenreplaycache-adal)</li><li>[Usare il token toomanage librerie ADAL richiede da OAuth2 client tooAAD (locale o Active Directory)](#adal-oauth2)</li></ul> |
| **Gateway IoT sul campo** | <ul><li>[Autenticare i dispositivi si connettono toohello Gateway campo](#authn-devices-field)</li></ul> |
| **Gateway IoT cloud** | <ul><li>[Verificare che i dispositivi si connettono tooCloud gateway sono autenticati](#authn-devices-cloud)</li><li>[Usare credenziali di autenticazione per dispositivo](#authn-cred)</li></ul> |
| **Archiviazione di Azure** | <ul><li>[Verificare che solo hello richiesto contenitori e BLOB viene assegnato l'accesso in lettura anonimo](#req-containers-anon)</li><li>[Concedere l'accesso limitato tooobjects nell'archiviazione di Azure usando SAS o SAP](#limited-access-sas)</li></ul> |

## <a id="standard-authn-web-app"></a>È consigliabile utilizzare un tooWeb tooauthenticate meccanismo di autenticazione standard dell'applicazione

| Titolo                   | Dettagli      |
| ----------------------- | ------------ |
| **Componente**               | Applicazione Web. | 
| **Fase SDL**               | Compilare |  
| **Tecnologie applicabili** | Generico |
| **Attributes (Attributi) (Attributi)**              | N/D  |
| **Riferimenti**              | N/D  |
| Dettagli | <p>L'autenticazione è il processo di hello in cui un'entità prova la propria identità, in genere tramite le credenziali, ad esempio un nome utente e una password. È possibile prendere in considerazione diversi protocolli di autenticazione disponibili, alcuni dei quali sono elencati di seguito:</p><ul><li>Certificati client</li><li>Basato su Windows</li><li>Basato su form</li><li>Federazione: AD FS</li><li>Federazione: Azure AD</li><li>Federazione: Identity Server</li></ul><p>È consigliabile utilizzare un processo di origine hello tooidentify meccanismo di autenticazione standard</p>|

## <a id="handle-failed-authn"></a>Gestire in modo sicuro scenari di autenticazione non riuscita mediante le applicazioni

| Titolo                   | Dettagli      |
| ----------------------- | ------------ |
| **Componente**               | Applicazione Web. | 
| **Fase SDL**               | Compilare |  
| **Tecnologie applicabili** | Generico |
| **Attributes (Attributi) (Attributi)**              | N/D  |
| **Riferimenti**              | N/D  |
| Dettagli | <p>Le applicazioni che in modo esplicito l'autenticazione degli utenti devono gestire gli scenari di autenticazione non riuscito il meccanismo di autenticazione securely.hello deve:</p><ul><li>Negare l'accesso alle risorse tooprivileged quando l'autenticazione ha esito negativo</li><li>Visualizzare un messaggio di errore generico in caso di autenticazione non riuscita e accesso negato.</li></ul><p>Verificare quanto segue:</p><ul><li>Protezione delle risorse con privilegi dopo accessi non riusciti.</li><li>Visualizzazione di un messaggio di errore generico in caso di autenticazione non riuscita e accesso negato.</li><li>Disabilitazione degli account dopo un numero eccessivo di tentativi non riusciti.</li><ul>|

## <a id="step-up-adaptive-authn"></a>Abilitare l'autenticazione adattiva o incrementale

| Titolo                   | Dettagli      |
| ----------------------- | ------------ |
| **Componente**               | Applicazione Web. | 
| **Fase SDL**               | Compilare |  
| **Tecnologie applicabili** | Generico |
| **Attributes (Attributi) (Attributi)**              | N/D  |
| **Riferimenti**              | N/D  |
| Dettagli | <p>Verificare un'applicazione hello disponga delle autorizzazioni aggiuntivo (ad esempio l'istruzione o autenticazione adattiva, tramite l'autenticazione a più fattori, ad esempio l'invio di SMS, posta elettronica e così via o chiedere conferma per la riesecuzione dell'autenticazione OTP) in modo utente hello è carente prima di concedere l'accesso informazioni toosensitive. Questa regola si applica anche per rendere conto tooan modifiche critici o azione</p><p>Questo significa pertanto che adattamento hello di autenticazione è toobe implementato in tale modo un'applicazione hello correttamente applicato da autorizzazione sensibile al contesto in modo da toonot consentono la non autorizzata manipolazione per mezzo di nell'esempio, la manomissione di parametro</p>|

## <a id="admin-interface-lockdown"></a>Assicurarsi che le interfacce amministrative siano bloccate correttamente

| Titolo                   | Dettagli      |
| ----------------------- | ------------ |
| **Componente**               | Applicazione Web. | 
| **Fase SDL**               | Compilare |  
| **Tecnologie applicabili** | Generico |
| **Attributes (Attributi) (Attributi)**              | N/D  |
| **Riferimenti**              | N/D  |
| Dettagli | prima di soluzione hello è toogrant l'accesso solo da una determinata origine IP intervallo toohello amministrativa interfaccia. Se la soluzione non è possibile che non è sempre consigliabile tooenforce un'autenticazione adattata o aggiornamento all'edizione superiore per l'accesso all'interfaccia di amministrazione di hello |

## <a id="forgot-pword-fxn"></a>Implementare in modo sicuro funzionalità per la password dimenticata

| Titolo                   | Dettagli      |
| ----------------------- | ------------ |
| **Componente**               | Applicazione Web. | 
| **Fase SDL**               | Compilare |  
| **Tecnologie applicabili** | Generico |
| **Attributes (Attributi) (Attributi)**              | N/D  |
| **Riferimenti**              | N/D  |
| Dettagli | <p>in primo luogo, Hello è tooverify che hai dimenticato la password e altri percorsi di recupero inviano un collegamento tra un tempo limitato attivazione token, anziché hello stessa password. Autenticazione aggiuntiva in base a soft token (ad esempio SMS token mobili applicazioni native, e così via) può essere necessario anche collegamento hello viene inviato tramite. In secondo luogo, è necessario non bloccare l'account di utenti hello al contempo hello processo di acquisizione di una nuova password è in corso.</p><p>Questo potrebbe causare attacchi Denial of service tooa ogni volta che un utente malintenzionato decide toointentionally blocca gli utenti di hello con un attacco automatizzato. In terzo luogo, ogni nuova richiesta di password hello è stato impostato in corso, il messaggio hello che è visualizzare deve essere generalizzato nell'enumerazione di ordine tooprevent nome utente. La quarta sempre impedisce hello uso delle password precedenti e implementare criteri password complessi.</p> |

## <a id="pword-account-policy"></a>Assicurarsi che vengano implementati criteri di account e password

| Titolo                   | Dettagli      |
| ----------------------- | ------------ |
| **Componente**               | Applicazione Web. | 
| **Fase SDL**               | Compilare |  
| **Tecnologie applicabili** | Generico |
| **Attributes (Attributi) (Attributi)**              | N/D  |
| **Riferimenti**              | N/D  |
| Dettagli | <p>È necessario implementare criteri di account e password in conformità con i criteri e le procedure consigliate dell'organizzazione.</p><p>toodefend contro attacchi di forza bruta e dizionario basato su un'ipotesi: criteri password complessa devono essere implementato tooensure che gli utenti creare password complesse (ad esempio, la lunghezza minima di 12 caratteri, caratteri alfanumerici e caratteri speciali).</p><p>Criteri di blocco account possono essere implementati nel seguente modo hello:</p><ul><li>**Blocco temporaneo:** questo tipo di blocco è utile per proteggere gli utenti da attacchi di forza bruta. Ad esempio, ogni volta che l'utente hello immette una password errata, un'applicazione hello tre volte in grado di bloccare account hello per un minuto in ordine tooslow processo hello della sua password rendendo meno redditività per hello autore dell'attacco tooproceed violazione. Se si tooimplement rigido contromisure di blocco per questo esempio si ottiene una "Dichiarazione" bloccando gli account in modo permanente. In alternativa, l'applicazione può generare un OTP (una sola volta Password) e inviarlo out of band (tramite posta elettronica, sms e così via) toohello utente. Un altro approccio potrebbe essere tooimplement CAPTCHA dopo aver raggiunto una soglia del numero di tentativi non riusciti.</li><li>**Blocco di disco rigido:** questo tipo di blocco deve essere applicato quando si rileva un utente attaccare l'applicazione e quest'ultimo contatore tramite il blocco in modo permanente il suo account fino a quando il team di risposta toodo ora le analisi forensi. Dopo questo processo è possibile decidere di suo account utente di hello toogive nuovamente o richiedere ulteriori azioni legali contro di lui. Questo tipo di approccio impedisce l'utente malintenzionato di hello di penetrare ulteriormente l'applicazione e dell'infrastruttura.</li></ul><p>toodefend attacchi predefinito e account stimabile, verificare che tutte le chiavi e le password sono sostituibili e vengono generate o sostituite dopo la fase di installazione.</p><p>Se un'applicazione hello è tooauto-generare le password, verificare che le password hello generato sono casuali e hanno un'entropia elevata.</p>|

## <a id="controls-username-enum"></a>Enumerazione di nome utente di implementare controlli tooprevent

| Titolo                   | Dettagli      |
| ----------------------- | ------------ |
| **Componente**               | Applicazione Web. | 
| **Fase SDL**               | Compilare |  
| **Tecnologie applicabili** | Generico |
| **Attributes (Attributi) (Attributi)**              | N/D  |
| **Riferimenti**              | N/D  |
| **Passaggi** | Tutti i messaggi di errore devono essere generalizzati nell'enumerazione di ordine tooprevent nome utente. A volte non è possibile evitare la divulgazione di informazioni nelle funzionalità, ad esempio in una pagina di registrazione. In questo caso, è necessario toouse limitazione di velocità di metodi come CAPTCHA tooprevent un attacco automatizzato da un utente malintenzionato. |

## <a id="win-authn-sql"></a>Quando possibile, utilizzare l'autenticazione di Windows per la connessione Server tooSQL

| Titolo                   | Dettagli      |
| ----------------------- | ------------ |
| **Componente**               | Database | 
| **Fase SDL**               | Compilare |  
| **Tecnologie applicabili** | Locale |
| **Attributes (Attributi) (Attributi)**              | Versione SQL: tutte |
| **Riferimenti**              | [SQL Server: scegliere una modalità di autenticazione](https://msdn.microsoft.com/library/ms144284.aspx) |
| **Passaggi** | L'autenticazione di Windows utilizza il protocollo di sicurezza Kerberos, fornisce l'applicazione dei criteri password con convalida toocomplexity considerare per le password complesse, fornisce il supporto per il blocco account e supporta la scadenza delle password.|

## <a id="aad-authn-sql"></a>Quando possibile utilizzare l'autenticazione di Azure Active Directory per tooSQL connessione Database

| Titolo                   | Dettagli      |
| ----------------------- | ------------ |
| **Componente**               | Database | 
| **Fase SDL**               | Compilare |  
| **Tecnologie applicabili** | SQL Azure |
| **Attributes (Attributi) (Attributi)**              | Versione SQL: 12 |
| **Riferimenti**              | [Connessione tooSQL Database usando Azure Active Directory l'autenticazione](https://azure.microsoft.com/documentation/articles/sql-database-aad-authentication/) |
| **Passaggi** | **Versione minima:** Database SQL di Azure V12 necessari tooallow Database SQL di Azure toouse l'autenticazione AAD contro hello Directory Microsoft |

## <a id="authn-account-pword"></a>Assicurarsi che vengano applicati i criteri di account e password in SQL Server quando viene usata la modalità di autenticazione SQL

| Titolo                   | Dettagli      |
| ----------------------- | ------------ |
| **Componente**               | Database | 
| **Fase SDL**               | Compilare |  
| **Tecnologie applicabili** | Generico |
| **Attributes (Attributi) (Attributi)**              | N/D  |
| **Riferimenti**              | [Criteri password di SQL Server](https://technet.microsoft.com/library/ms161959(v=sql.110).aspx) |
| **Passaggi** | Quando si usa l'autenticazione di SQL Server, in SQL Server vengono creati account di accesso che non sono basati su account utente di Windows. Nome utente hello e la password di hello creati utilizzando SQL Server e archiviati in SQL Server. SQL Server può fare uso di meccanismi dei criteri password di Windows. È possibile applicare hello stessi criteri di complessità e scadenza utilizzati in Windows toopasswords utilizzata all'interno di SQL Server. |

## <a id="autn-contained-db"></a>Non usare l'autenticazione SQL in database indipendenti

| Titolo                   | Dettagli      |
| ----------------------- | ------------ |
| **Componente**               | Database | 
| **Fase SDL**               | Compilare |  
| **Tecnologie applicabili** | Locale, SQL Azure |
| **Attributes (Attributi) (Attributi)**              | Versione SQL: MSSQL2012, versione SQL: 12 |
| **Riferimenti**              | [Procedure di sicurezza consigliate con i database indipendenti](http://msdn.microsoft.com/library/ff929055.aspx) |
| **Passaggi** | assenza di Hello dei criteri password applicati può aumentare la probabilità hello di una credenziale debole viene stabilita in un database indipendente. Fare uso dell'autenticazione di Windows. |

## <a id="authn-sas-tokens"></a>Usare credenziali di autenticazione per dispositivo con i token di firma di accesso condiviso

| Titolo                   | Dettagli      |
| ----------------------- | ------------ |
| **Componente**               | Hub eventi di Azure | 
| **Fase SDL**               | Compilare |  
| **Tecnologie applicabili** | Generico |
| **Attributes (Attributi) (Attributi)**              | N/D  |
| **Riferimenti**              | [Panoramica del modello di sicurezza e autenticazione di Hub eventi](https://azure.microsoft.com/documentation/articles/event-hubs-authentication-and-security-model-overview/) |
| **Passaggi** | <p>modello di sicurezza degli hub eventi Hello è basato su una combinazione di token di firma di accesso condiviso (SAS) e i Publisher di eventi. nome dell'autore Hello rappresenta hello DeviceID che riceve il token hello. Ciò consente di associare token hello generati con dispositivi rispettivi hello.</p><p>Tutti i messaggi vengono contrassegnati con l'iniziatore sul lato del servizio, per consentire il rilevamento di tentativi di spoofing dell'origine nel payload. Durante l'autenticazione dei dispositivi, generare una per ogni dispositivo SaS tooa con ambito token univoco dell'editore.</p>|

## <a id="multi-factor-azure-admin"></a>Abilitare Azure Multi-Factor Authentication per amministratori di Azure

| Titolo                   | Dettagli      |
| ----------------------- | ------------ |
| **Componente**               | Limite di trust di Azure | 
| **Fase SDL**               | Distribuzione |  
| **Tecnologie applicabili** | Generico |
| **Attributes (Attributi) (Attributi)**              | N/D  |
| **Riferimenti**              | [Informazioni su Azure Multi-Factor Authentication](https://azure.microsoft.com/documentation/articles/multi-factor-authentication/) |
| **Passaggi** | <p>Multi-factor authentication (MFA) è un metodo di autenticazione che richiede più di un metodo di verifica e aggiunge un secondo livello critico di sicurezza toouser accessi e le transazioni. Funziona richiedendo due o più dei seguenti metodi di verifica hello:</p><ul><li>Un'informazione nota (in genere una password)</li><li>Un oggetto che si possiede (un dispositivo attendibile non facile da duplicare, ad esempio un telefono)</li><li>Una caratteristica fisica dell'utente (biometrica)</li><ul>|

## <a id="anon-access-cluster"></a>Limitare l'accesso anonimo tooService dell'infrastruttura Cluster

| Titolo                   | Dettagli      |
| ----------------------- | ------------ |
| **Componente**               | Limite di trust di Service Fabric | 
| **Fase SDL**               | Distribuzione |  
| **Tecnologie applicabili** | Generico |
| **Attributes (Attributi) (Attributi)**              | Ambiente: Azure  |
| **Riferimenti**              | [Scenari di sicurezza di un cluster di Service Fabric](https://azure.microsoft.com/documentation/articles/service-fabric-cluster-security) |
| **Passaggi** | <p>I cluster devono essere sempre agli utenti di tooprevent protetto non autorizzata di connessione tooyour cluster, in particolare quando dispone i carichi di lavoro in esecuzione su di esso.</p><p>Durante la creazione di un cluster di service fabric, verificare che la modalità sicurezza hello sia impostata troppo "sicura" e configurare hello necessario server x. 509. La creazione di un cluster "non sicuro" consente qualsiasi tooit tooconnect utente anonimo se espone Gestione endpoint toohello rete Internet pubblica.</p>|

## <a id="fabric-cn-nn"></a>Assicurarsi che il certificato da client a nodo di Service Fabric sia diverso dal certificato da nodo a nodo

| Titolo                   | Dettagli      |
| ----------------------- | ------------ |
| **Componente**               | Limite di trust di Service Fabric | 
| **Fase SDL**               | Distribuzione |  
| **Tecnologie applicabili** | Generico |
| **Attributes (Attributi) (Attributi)**              | Ambiente: Azure, ambiente: autonomo |
| **Riferimenti**              | [Sicurezza di Service Fabric per nodo Client certificato](https://azure.microsoft.com/documentation/articles/service-fabric-cluster-security/#_client-to-node-certificate-security), [Connetti tooa cluster sicuro utilizzando il certificato client](https://azure.microsoft.com/documentation/articles/service-fabric-connect-to-secure-cluster/) |
| **Passaggi** | <p>Certificato client da nodo sicurezza configurata durante la creazione di cluster hello tramite hello portale di Azure, modelli di gestione risorse o un modello JSON autonoma specificando un certificato client di amministrazione e/o di un certificato client utente.</p><p>Hello amministrazione utente client i certificati client e che si specifica devono essere diversi rispetto ai certificati primari e secondari hello specificate per la sicurezza del nodo per nodo.</p>|

## <a id="aad-client-fabric"></a>Utilizzare AAD tooauthenticate client tooservice dell'infrastruttura cluster

| Titolo                   | Dettagli      |
| ----------------------- | ------------ |
| **Componente**               | Limite di trust di Service Fabric | 
| **Fase SDL**               | Distribuzione |  
| **Tecnologie applicabili** | Generico |
| **Attributes (Attributi) (Attributi)**              | Ambiente: Azure |
| **Riferimenti**              | [Scenari di sicurezza per i cluster: raccomandazioni sulla sicurezza](https://azure.microsoft.com/documentation/articles/service-fabric-cluster-security/#security-recommendations) |
| **Passaggi** | I cluster in esecuzione in Azure possono inoltre proteggere accesso toohello gli endpoint di gestione tramite Azure Active Directory (AAD), oltre ai certificati client. Per i cluster di Azure, è consigliabile usare i client tooauthenticate di sicurezza di Azure ad e i certificati per la sicurezza del nodo per nodo.|

## <a id="fabric-cert-ca"></a>Assicurarsi che i certificati di Service Fabric vengano ottenuti da un'Autorità di certificazione (CA) approvata

| Titolo                   | Dettagli      |
| ----------------------- | ------------ |
| **Componente**               | Limite di trust di Service Fabric | 
| **Fase SDL**               | Distribuzione |  
| **Tecnologie applicabili** | Generico |
| **Attributes (Attributi) (Attributi)**              | Ambiente: Azure |
| **Riferimenti**              | [Certificati X.509 e Service Fabric](https://azure.microsoft.com/documentation/articles/service-fabric-cluster-security/#x509-certificates-and-service-fabric) |
| **Passaggi** | <p>Service Fabric usa i certificati server X.509 per l'autenticazione dei nodi e dei client.</p><p>Tooconsider alcuni aspetti importanti durante l'utilizzo di certificati in infrastrutture di servizio:</p><ul><li>È consigliabile creare i certificati usati nei cluster che eseguono carichi di lavoro di produzione con un servizio certificati di Windows Server configurato correttamente oppure ottenerli da un'Autorità di certificazione (CA) approvata. Hello CA può essere una CA esterna approvata o un correttamente gestito interno chiave infrastruttura pubblica (PKI)</li><li>Non usare mai in fase di produzione certificati temporanei o di test creati con strumenti come MakeCert.exe.</li><li>È possibile usare un certificato autofirmato, ma solo per i cluster di test e non nell'ambiente di produzione.</li></ul>|

## <a id="standard-authn-id"></a>Usare scenari di autenticazione standard supportati da Identity Server

| Titolo                   | Dettagli      |
| ----------------------- | ------------ |
| **Componente**               | Identity Server | 
| **Fase SDL**               | Compilare |  
| **Tecnologie applicabili** | Generico |
| **Attributes (Attributi) (Attributi)**              | N/D  |
| **Riferimenti**              | [IdentityServer3 - hello quadro generale](https://identityserver.github.io/Documentation/docsv2/overview/bigPicture.html) |
| **Passaggi** | <p>Di seguito è hello interazioni tipiche supportate dal Server di identità:</p><ul><li>Comunicazione tra browser e applicazioni Web.</li><li>Comunicazione tra applicazioni Web e API Web, talvolta in modo autonomo e talvolta per conto dell'utente.</li><li>Comunicazione tra applicazioni basate su browser e API Web.</li><li>Comunicazione tra applicazioni native e API Web.</li><li>Comunicazione tra applicazioni basate su server e API Web.</li><li>Comunicazione tra API Web e API Web, talvolta in modo autonomo e talvolta per conto dell'utente.</li></ul>|

## <a id="override-token"></a>Eseguire l'override di cache token hello predefinita Identity Server con un'alternativa scalabile

| Titolo                   | Dettagli      |
| ----------------------- | ------------ |
| **Componente**               | Identity Server | 
| **Fase SDL**               | Distribuzione |  
| **Tecnologie applicabili** | Generico |
| **Attributes (Attributi) (Attributi)**              | N/D  |
| **Riferimenti**              | [Distribuzione di Identity Server: memorizzazione nella cache](https://identityserver.github.io/Documentation/docsv2/advanced/deployment.html) |
| **Passaggi** | <p>IdentityServer ha una semplice cache in memoria predefinita. Mentre questo è utile per applicazioni native su scala ridotta, non è adatta per le applicazioni di back-end e di livello intermedio per hello seguenti motivi:</p><ul><li>Queste applicazioni sono accessibili da più utenti contemporaneamente. Salvataggio di tutti i token di accesso in hello stesso archivio crea problemi di isolamento e presenta problemi quando si opera su larga scala: molti utenti, ognuno con un numero di token come risorse hello hello accede alle app per loro conto, può significare ricerca molto costosa e i numeri di grandi dimensioni operazioni</li><li>Queste applicazioni sono in genere distribuite in topologie distribuite, in cui più nodi devono avere accesso toohello stessa cache</li><li>I token memorizzati nella cache devono resistere in caso di disattivazione e riciclo del processo.</li><li>Per tutti i hello sopra motivi, durante l'implementazione di applicazioni web, è consigliabile cache dei token del Server di toooverride hello predefinito Identity con un'alternativa scalabile, ad esempio la cache Redis di Azure</li></ul>|

## <a id="binaries-signed"></a>Assicurarsi che i file binari dell'applicazione distribuita abbiano una firma digitale

| Titolo                   | Dettagli      |
| ----------------------- | ------------ |
| **Componente**               | Limite di trust dei computer | 
| **Fase SDL**               | Distribuzione |  
| **Tecnologie applicabili** | Generico |
| **Attributes (Attributi) (Attributi)**              | N/D  |
| **Riferimenti**              | N/D  |
| **Passaggi** | Assicurarsi che i file binari dell'applicazione distribuita siano firmati digitalmente in modo che sia possibile verificare l'integrità dei file binari di hello hello|

## <a id="msmq-queues"></a>Abilitare l'autenticazione quando ci si connette tooMSMQ code in WCF

| Titolo                   | Dettagli      |
| ----------------------- | ------------ |
| **Componente**               | WCF | 
| **Fase SDL**               | Compilare |  
| **Tecnologie applicabili** | Generico, .NET Framework 3 |
| **Attributes (Attributi) (Attributi)**              | N/D |
| **Riferimenti**              | [MSDN](https://msdn.microsoft.com/library/ff648500.aspx) |
| **Passaggi** | Programma ha esito negativo tooenable autenticazione quando ci si connette tooMSMQ code, un utente malintenzionato può inviare in modo anonimo toohello coda dei messaggi per l'elaborazione. Se l'autenticazione non è usato tooconnect tooan MSMQ coda utilizzata toodeliver un programma tooanother messaggio, un utente malintenzionato potrebbe inviare un messaggio di tipo anonimo che sia dannoso.|

### <a name="example"></a>Esempio
Hello `<netMsmqBinding/>` elemento del file di configurazione WCF hello seguente indica l'autenticazione WCF toodisable quando ci si connette coda MSMQ tooan per il recapito dei messaggi.
```
<bindings>
    <netMsmqBinding>
        <binding>
            <security>
                <transport msmqAuthenticationMode=""None"" />
            </security>
        </binding>
    </netMsmqBinding>
</bindings>
```
Configurare l'autenticazione di dominio Windows o un certificato toorequire MSMQ sempre disponibile per i messaggi in ingresso o in uscita.

### <a name="example"></a>Esempio
Hello `<netMsmqBinding/>` elemento del file di configurazione WCF hello seguente indica l'autenticazione del certificato tooenable WCF durante la connessione coda MSMQ tooan. client di Hello viene autenticato mediante certificati x. 509. certificato client Hello deve essere presente nell'archivio certificati hello del server di hello.
```
<bindings>
    <netMsmqBinding>
        <binding>
            <security>
                <transport msmqAuthenticationMode=""Certificate"" />
            </security>
        </binding>
    </netMsmqBinding>
</bindings>
```

## <a id="message-none"></a>-Non WCF non impostato toonone clientCredentialType messaggio

| Titolo                   | Dettagli      |
| ----------------------- | ------------ |
| **Componente**               | WCF | 
| **Fase SDL**               | Compilare |  
| **Tecnologie applicabili** | .NET Framework 3 |
| **Attributes (Attributi) (Attributi)**              | Tipo di credenziali client: nessuno |
| **Riferimenti**              | [MSDN](https://msdn.microsoft.com/library/ff648500.aspx), [Fortify](https://vulncat.fortify.com/en/vulncat/index.html) |
| **Passaggi** | assenza di Hello di autenticazione significa che tutti gli utenti è in grado di tooaccess questo servizio. Un servizio che non esegue l'autenticazione dei client consente l'accesso agli utenti di tooall. Configurare tooauthenticate applicazione hello contro le credenziali client. Questa operazione può essere eseguita impostando tooWindows clientCredentialType di messaggio hello o un certificato. |

### <a name="example"></a>Esempio
```
<message clientCredentialType=""Certificate""/>
```

## <a id="transport-none"></a>-Non WCF non impostato trasporto clientCredentialType toonone

| Titolo                   | Dettagli      |
| ----------------------- | ------------ |
| **Componente**               | WCF | 
| **Fase SDL**               | Compilare |  
| **Tecnologie applicabili** | Generico, .NET Framework 3 |
| **Attributes (Attributi) (Attributi)**              | Tipo di credenziali client: nessuno |
| **Riferimenti**              | [MSDN](https://msdn.microsoft.com/library/ff648500.aspx), [Fortify](https://vulncat.fortify.com/en/vulncat/index.html) |
| **Passaggi** | assenza di Hello di autenticazione significa che tutti gli utenti è in grado di tooaccess questo servizio. Un servizio che non esegue l'autenticazione dei client consente a tutti gli utenti tooaccess le funzionalità. Configurare tooauthenticate applicazione hello contro le credenziali client. Questa operazione può essere eseguita impostando hello trasporto clientCredentialType tooWindows o certificato. |

### <a name="example"></a>Esempio
```
<transport clientCredentialType=""Certificate""/>
```

## <a id="authn-secure-api"></a>Verificare che le tecniche di autenticazione standard siano utilizzati toosecure API Web

| Titolo                   | Dettagli      |
| ----------------------- | ------------ |
| **Componente**               | API Web | 
| **Fase SDL**               | Compilare |  
| **Tecnologie applicabili** | Generico |
| **Attributes (Attributi) (Attributi)**              | N/D  |
| **Riferimenti**              | [Autenticazione e autorizzazione nell'API Web ASP.NET](http://www.asp.net/web-api/overview/security/authentication-and-authorization-in-aspnet-web-api), [Servizi di autenticazione esterna con l'API Web ASP.NET (C#)](http://www.asp.net/web-api/overview/security/external-authentication-services) |
| **Passaggi** | <p>L'autenticazione è il processo di hello in cui un'entità prova la propria identità, in genere tramite le credenziali, ad esempio un nome utente e una password. È possibile prendere in considerazione diversi protocolli di autenticazione disponibili, alcuni dei quali sono elencati di seguito:</p><ul><li>Certificati client</li><li>Basato su Windows</li><li>Basato su form</li><li>Federazione: AD FS</li><li>Federazione: Azure AD</li><li>Federazione: Identity Server</li></ul><p>I collegamenti nella sezione dei riferimenti hello forniscono dettagli di basso livello su ciascuno degli schemi di autenticazione hello come può essere implementato toosecure un'API Web.</p>|

## <a id="authn-aad"></a>Usare scenari di autenticazione standard supportati da Azure Active Directory

| Titolo                   | Dettagli      |
| ----------------------- | ------------ |
| **Componente**               | Azure AD | 
| **Fase SDL**               | Compilare |  
| **Tecnologie applicabili** | Generico |
| **Attributes (Attributi) (Attributi)**              | N/D  |
| **Riferimenti**              | [Scenari di autenticazione per Azure AD](https://azure.microsoft.com/documentation/articles/active-directory-authentication-scenarios/), [Esempi di codice di Azure Active Directory](https://azure.microsoft.com/documentation/articles/active-directory-code-samples/), [Guida per gli sviluppatori di Azure Active Directory](https://azure.microsoft.com/documentation/articles/active-directory-developers-guide/) |
| **Passaggi** | <p>Azure Active Directory (Azure AD) semplifica l'autenticazione per gli sviluppatori fornendo le identità come servizio, con il supporto per protocolli standard del settore come OAuth 2.0 e OpenID Connect. Di seguito è hello cinque scenari di applicazione principali supportati da Azure AD:</p><ul><li>Web Browser tooWeb applicazione: un utente deve toosign nell'applicazione web tooa protetta da Azure AD</li><li>Applicazione a pagina singola (SPA): Un utente deve toosign in tooa applicazione a pagina singola protetta da Azure AD</li><li>TooWeb applicazione nativa API: un'applicazione nativa che viene eseguito su un telefono, tablet o PC esigenze tooauthenticate tooget un utente le risorse da un'API web protetta da Azure AD</li><li>API tooWeb dell'applicazione Web: un'applicazione web deve tooget risorse da un'API web protetta da Azure AD</li><li>Applicazione daemon o Server tooWeb API: un'applicazione daemon o un'applicazione server senza interfaccia utente web deve tooget risorse da un'API web protetta da Azure AD</li></ul><p>Per i dettagli di implementazione di basso livello, vedere toohello collegamenti nella sezione dei riferimenti hello</p>|

## <a id="adal-scalable"></a>Eseguire l'override di hello ADAL token cache predefinita con un'alternativa scalabile

| Titolo                   | Dettagli      |
| ----------------------- | ------------ |
| **Componente**               | Azure AD | 
| **Fase SDL**               | Compilare |  
| **Tecnologie applicabili** | Generico |
| **Attributes (Attributi) (Attributi)**              | N/D  |
| **Riferimenti**              | [Modern Authentication with Azure Active Directory for Web Applications](https://blogs.msdn.microsoft.com/microsoft_press/2016/01/04/new-book-modern-authentication-with-azure-active-directory-for-web-applications/) (Autenticazione moderna con Azure Active Directory per applicazioni Web), [Using Redis as ADAL token cache](https://blogs.msdn.microsoft.com/mrochon/2016/09/19/using-redis-as-adal-token-cache/) (Uso di Redis come cache dei token ADAL)  |
| **Passaggi** | <p>cache predefinita di Hello che usa ADAL (Active Directory Authentication Library) è una cache in memoria che si basa su un archivio statico, disponibile a livello di processo. Quando questo viene utilizzato per le applicazioni native, non è adatta per le applicazioni di back-end e di livello intermedio per hello seguenti motivi:</p><ul><li>Queste applicazioni sono accessibili da più utenti contemporaneamente. Salvataggio di tutti i token di accesso in hello stesso archivio crea problemi di isolamento e presenta problemi quando si opera su larga scala: molti utenti, ognuno con un numero di token come risorse hello hello accede alle app per loro conto, può significare ricerca molto costosa e i numeri di grandi dimensioni operazioni</li><li>Queste applicazioni sono in genere distribuite in topologie distribuite, in cui più nodi devono avere accesso toohello stessa cache</li><li>I token memorizzati nella cache devono resistere in caso di disattivazione e riciclo del processo.</li></ul><p>Per tutti i hello sopra motivi, durante l'implementazione di applicazioni web, è consigliabile toooverride hello ADAL token cache predefinita con un'alternativa scalabile, ad esempio la cache Redis di Azure.</p>|

## <a id="tokenreplaycache-adal"></a>Verificare che TokenReplayCache sia riproduzione hello tooprevent utilizzati dei token di autenticazione ADAL

| Titolo                   | Dettagli      |
| ----------------------- | ------------ |
| **Componente**               | Azure AD | 
| **Fase SDL**               | Compilare |  
| **Tecnologie applicabili** | Generico |
| **Attributes (Attributi) (Attributi)**              | N/D  |
| **Riferimenti**              | [Modern Authentication with Azure Active Directory for Web Applications](https://blogs.msdn.microsoft.com/microsoft_press/2016/01/04/new-book-modern-authentication-with-azure-active-directory-for-web-applications/) (Autenticazione moderna con Azure Active Directory per applicazioni Web) |
| **Passaggi** | <p>proprietà TokenReplayCache Hello consente agli sviluppatori toodefine una cache di riproduzione token, un archivio che può essere utilizzato per il salvataggio di alcun token di token allo scopo di hello di controllare che può essere usati più di una volta.</p><p>Si tratta di una misura da attacchi comuni, hello denominato attacco di tipo replay di token: toosend potrebbe provare a un utente malintenzionato intercetta i token di hello inviato al momento dell'accesso viene nuovamente app toohello ("riprodurla") per stabilire una nuova sessione. Ad esempio, In OIDC-concessione del codice di flusso, dopo l'autenticazione dell'utente, una richiesta troppo "/ signin oidc" endpoint del componente hello viene effettuata con "id_token", "code" e "stato" parametri.</p><p>Hello relying party convalida la richiesta e stabilisce una nuova sessione. Se un avversario acquisisce la richiesta e riprodurlo in seguito, se possibile stabilire una sessione di esito positivo e l'utente hello contraffatta. presenza Hello del nonce hello in OpenID Connect è possibile limitare ma non completamente eliminare circostanze hello in cui attacco hello può essere eseguito correttamente. tooprotect delle applicazioni, gli sviluppatori possono fornire un'implementazione di ITokenReplayCache e assegnare tooTokenReplayCache un'istanza.</p>|

### <a name="example"></a>Esempio
```C#
// ITokenReplayCache defined in ADAL
public interface ITokenReplayCache
{
bool TryAdd(string securityToken, DateTime expiresOn);
bool TryFind(string securityToken);
}
```

### <a name="example"></a>Esempio
Di seguito è riportato un esempio di implementazione dell'interfaccia ITokenReplayCache hello. Personalizzare l'esempio e implementare il framework di memorizzazione nella cache specifico del progetto.
```C#
public class TokenReplayCache : ITokenReplayCache
{
    private readonly ICacheProvider cache; // Your project-specific cache provider
    public TokenReplayCache(ICacheProvider cache)
    {
        this.cache = cache;
    }
    public bool TryAdd(string securityToken, DateTime expiresOn)
    {
        if (this.cache.Get<string>(securityToken) == null)
        {
            this.cache.Set(securityToken, securityToken);
            return true;
        }
        return false;
    }
    public bool TryFind(string securityToken)
    {
        return this.cache.Get<string>(securityToken) != null;
    }
}
```
cache di Hello implementato ha toobe a cui fa riferimento nelle opzioni OIDC tramite hello "TokenValidationParameters" proprietà come indicato di seguito.
```C#
OpenIdConnectOptions openIdConnectOptions = new OpenIdConnectOptions
{
    AutomaticAuthenticate = true,
    ... // other configuration properties follow..
    TokenValidationParameters = new TokenValidationParameters
    {
        TokenReplayCache = new TokenReplayCache(/*Inject your cache provider*/);
    }
}
```

Annotare tale efficacia hello tootest di questa configurazione, l'account di accesso nell'applicazione locale protetto OIDC e acquisire richiesta hello troppo`"/signin-oidc"` endpoint in fiddler. Se protezione hello non è in uso, riproduzione di richiesta nel fiddler imposterà un nuovo cookie di sessione. Quando la richiesta hello riproduzione viene eseguita dopo l'aggiunta di hello TokenReplayCache protezione, un'applicazione hello genererà un'eccezione nel modo seguente:`SecurityTokenReplayDetectedException: IDX10228: hello securityToken has previously been validated, securityToken: 'eyJ0eXAiOiJKV1QiLCJhbGciOiJSUzI1NiIsIng1dCI6Ik1uQ19WWmNBVGZNNXBPWWlKSE1iYTlnb0VLWSIsImtpZCI6Ik1uQ1......`

## <a id="adal-oauth2"></a>Usare il token toomanage librerie ADAL richiede da OAuth2 client tooAAD (locale o Active Directory)

| Titolo                   | Dettagli      |
| ----------------------- | ------------ |
| **Componente**               | Azure AD | 
| **Fase SDL**               | Compilare |  
| **Tecnologie applicabili** | Generico |
| **Attributes (Attributi) (Attributi)**              | N/D  |
| **Riferimenti**              | [ADAL](https://azure.microsoft.com/documentation/articles/active-directory-authentication-libraries/) |
| **Passaggi** | <p>Hello Azure AD authentication Library (ADAL) Abilita client applicazione sviluppatori tooeasily autenticare gli utenti toocloud o Active Directory (AD) locale e ottenere quindi i token di accesso per proteggere le chiamate API.</p><p>Azure AD Authentication Library offre numerose funzionalità che semplificano l'integrazione dell'autenticazione nelle applicazioni da parte degli sviluppatori, ad esempio il supporto asincrono, la cache di token configurabile per l'archiviazione dei token di accesso e dei token di aggiornamento e l'aggiornamento automatico dei token alla scadenza dei token di accesso, i token di aggiornamento e altre ancora.</p><p>Se si gestisce la maggior parte delle complessità hello, ADAL può consentono un sviluppatore di concentrarsi sulla logica di business nella propria applicazione e proteggere facilmente le risorse senza essere esperti di sicurezza. Sono disponibili librerie separate per .NET, JavaScript (client e Node.js), iOS, Android e Java.</p>|

## <a id="authn-devices-field"></a>Autenticare i dispositivi si connettono toohello Gateway campo

| Titolo                   | Dettagli      |
| ----------------------- | ------------ |
| **Componente**               | Gateway IoT sul campo | 
| **Fase SDL**               | Compilare |  
| **Tecnologie applicabili** | Generico |
| **Attributes (Attributi) (Attributi)**              | N/D  |
| **Riferimenti**              | N/D  |
| **Passaggi** | Verificare che ogni dispositivo è autenticato da hello Gateway campo prima di accettare i dati in essi contenuti e gestione delle comunicazioni upstream con hello Gateway del Cloud. Assicurarsi anche che i dispositivi si connettano con credenziali per dispositivo, in modo che sia possibile identificare i singoli dispositivi in modo univoco.|

## <a id="authn-devices-cloud"></a>Verificare che i dispositivi si connettono tooCloud gateway sono autenticati

| Titolo                   | Dettagli      |
| ----------------------- | ------------ |
| **Componente**               | Gateway IoT cloud | 
| **Fase SDL**               | Compilare |  
| **Tecnologie applicabili** | Generico, C#, Node.js  |
| **Attributes (Attributi) (Attributi)**              | N/A, opzione gateway: Hub IoT di Azure |
| **Riferimenti**              | N/A, [Hub IoT di Azure con .NET](https://azure.microsoft.com/documentation/articles/iot-hub-csharp-csharp-getstarted/), [Introduzione all'hub IoT e Node.js](https://azure.microsoft.com/documentation/articles/iot-hub-node-node-getstarted), [Proteggere l'hub IoT con certificati e firma di accesso condiviso](https://azure.microsoft.com/documentation/articles/iot-hub-sas-tokens/), [Repository Git](https://github.com/Azure/azure-iot-sdks/tree/master/node) |
| **Passaggi** | <ul><li>**Generico:** dispositivo hello autentica utilizzando Transport Layer Security (TLS) o IPSec. L'infrastruttura deve supportare l'uso di una chiave precondivisa (PSK) nei dispositivi che non riescono a gestire la crittografia asimmetrica completa. Usare Azure AD, OAuth.</li><li>**In c#:** quando si crea un'istanza di DeviceClient, per impostazione predefinita, hello metodo Create Crea un'istanza di DeviceClient che utilizza hello AMQP protocollo toocommunicate con l'IoT Hub. hello toouse il protocollo HTTPS, utilizzare l'override di hello del metodo di creazione hello che consente di protocollo hello toospecify. Se si utilizza il protocollo HTTPS hello, è necessario aggiungere hello `Microsoft.AspNet.WebApi.Client` hello di NuGet pacchetto tooyour progetto tooinclude `System.Net.Http.Formatting` dello spazio dei nomi.</li></ul>|

### <a name="example"></a>Esempio
```C#
static DeviceClient deviceClient;

static string deviceKey = "{device key}";
static string iotHubUri = "{iot hub hostname}";

var messageString = "{message in string format}";
var message = new Message(Encoding.ASCII.GetBytes(messageString));

deviceClient = DeviceClient.Create(iotHubUri, new DeviceAuthenticationWithRegistrySymmetricKey("myFirstDevice", deviceKey));

await deviceClient.SendEventAsync(message);
```

### <a name="example"></a>Esempio
**Node.js: autenticazione**
#### <a name="symmetric-key"></a>Chiave simmetrica
* Creare un hub IoT in Azure
* Creare una voce nel Registro di identità dispositivo hello
    ```javascript
    var device = new iothub.Device(null);
    device.deviceId = <DeviceId >
    registry.create(device, function(err, deviceInfo, res) {})
    ```
* Creare un dispositivo simulato
    ```javascript
    var clientFromConnectionString = require('azure-iot-device-amqp').clientFromConnectionString;
    var Message = require('azure-iot-device').Message;
    var connectionString = 'HostName=<HostName>DeviceId=<DeviceId>SharedAccessKey=<SharedAccessKey>';
    var client = clientFromConnectionString(connectionString);
    ```
#### <a name="sas-token"></a>Token di firma di accesso condiviso
* Viene generato internamente quando si usa una chiave simmetrica, ma è anche possibile generarlo e usarlo in modo esplicito
* Definire un protocollo: `var Http = require('azure-iot-device-http').Http;`
* Creare un token di firma di accesso condiviso:
    ```javascript
    resourceUri = encodeURIComponent(resourceUri.toLowerCase()).toLowerCase();
    var deviceName = "<deviceName >";
    var expires = (Date.now() / 1000) + expiresInMins * 60;
    var toSign = resourceUri + '\n' + expires;
    // using crypto
    var decodedPassword = new Buffer(signingKey, 'base64').toString('binary');
    const hmac = crypto.createHmac('sha256', decodedPassword);
    hmac.update(toSign);
    var base64signature = hmac.digest('base64');
    var base64UriEncoded = encodeURIComponent(base64signature);
    // construct authorization string
    var token = "SharedAccessSignature sr=" + resourceUri + "%2fdevices%2f"+deviceName+"&sig="
    + base64UriEncoded + "&se=" + expires;
    if (policyName) token += "&skn="+policyName;
    return token;
    ```
* Connettersi tramite un token di firma di accesso condiviso: 
    ```javascript
    Client.fromSharedAccessSignature(sas, Http); 
    ```
#### <a name="certificates"></a>Certificati
* Generare un X509 autofirmato certificato utilizzando uno strumento, ad esempio toogenerate OpenSSL una con estensione CERT e Key file toostore hello certificato e hello chiave rispettivamente
* Effettuare il provisioning di un dispositivo che accetta connessioni protette tramite i certificati
    ```javascript
    var connectionString = '<connectionString>';
    var registry = iothub.Registry.fromConnectionString(connectionString);
    var deviceJSON = {deviceId:"<deviceId>",
    authentication: {
        x509Thumbprint: {
        primaryThumbprint: "<PrimaryThumbprint>",
        secondaryThumbprint: "<SecondaryThumbprint>"
        }
    }}
    var device = deviceJSON;
    registry.create(device, function (err) {});
    ```
* Connettere un dispositivo usando un certificato
    ```javascript
    var Protocol = require('azure-iot-device-http').Http;
    var Client = require('azure-iot-device').Client;
    var connectionString = 'HostName=<HostName>DeviceId=<DeviceId>x509=true';
    var client = Client.fromConnectionString(connectionString, Protocol);
    var options = {
        key: fs.readFileSync('./key.pem', 'utf8'),
        cert: fs.readFileSync('./server.crt', 'utf8')
    }; 
    // Calling setOptions with hello x509 certificate and key (and optionally, passphrase) will configure hello client //transport toouse x509 when connecting tooIoT Hub
    client.setOptions(options);
    //call fn tooexecute after hello connection is set up
    client.open(fn);
    ```

## <a id="authn-cred"></a>Usare credenziali di autenticazione per dispositivo

| Titolo                   | Dettagli      |
| ----------------------- | ------------ |
| **Componente**               | Gateway IoT cloud  | 
| **Fase SDL**               | Compilare |  
| **Tecnologie applicabili** | Generico |
| **Attributes (Attributi) (Attributi)**              | Opzione gateway: Hub IoT di Azure |
| **Riferimenti**              | [Token di sicurezza dell'hub IoT di Azure](https://azure.microsoft.com/documentation/articles/iot-hub-sas-tokens/) |
| **Passaggi** | Usare credenziali di autenticazione per dispositivo tramite token di firma di accesso condiviso basati sulla chiave del dispositivo o sul certificato client, anziché criteri di accesso condiviso a livello di hub IoT. Ciò impedisce il riutilizzo di hello dei token di autenticazione di un gateway di dispositivo o un campo da un altro |

## <a id="req-containers-anon"></a>Verificare che solo hello richiesto contenitori e BLOB viene assegnato l'accesso in lettura anonimo

| Titolo                   | Dettagli      |
| ----------------------- | ------------ |
| **Componente**               | Archiviazione di Azure | 
| **Fase SDL**               | Compilare |  
| **Tecnologie applicabili** | Generico |
| **Attributes (Attributi) (Attributi)**              | Tipo di archiviazione: BLOB |
| **Riferimenti**              | [Gestire l'accesso in lettura anonimo toocontainers e blob](https://azure.microsoft.com/documentation/articles/storage-manage-access-to-resources/), [firme di accesso condiviso, parte 1: modello di firma di accesso condiviso di conoscenza hello](https://azure.microsoft.com/documentation/articles/storage-dotnet-shared-access-signature-part-1/) |
| **Passaggi** | <p>Per impostazione predefinita, un contenitore e tutti i BLOB in esso contenuti sono accessibili solo dal proprietario hello hello dell'account di archiviazione. contenitore di tooa toogive gli utenti anonimi le autorizzazioni di lettura e i relativi BLOB, può impostare uno accesso pubblico tooallow autorizzazioni al contenitore hello. Gli utenti anonimi possono leggere i BLOB in un contenitore accessibile pubblicamente senza effettuare l'autenticazione richiesta hello.</p><p>I contenitori forniscono hello le opzioni per la gestione dell'accesso seguenti:</p><ul><li>Accesso in lettura pubblico completo: i dati del BLOB e del contenitore possono essere letti tramite richiesta anonima. I client possono enumerare i BLOB all'interno del contenitore di hello tramite una richiesta anonima, ma non è possibile enumerare i contenitori nell'account di archiviazione hello.</li><li>Accesso in lettura pubblico solo per i BLOB: i dati del BLOB all'interno del contenitore possono essere letti tramite richiesta anonima, ma i dati del contenitore non sono disponibili. I client non è possibile enumerare i BLOB all'interno del contenitore di hello tramite una richiesta anonima</li><li>Accesso in lettura non pubblico: i dati blob e contenitore possono essere letti hello account solo dal proprietario</li></ul><p>L'accesso anonimo è ideale per scenari in cui alcuni BLOB devono essere sempre disponibili per l'accesso in lettura anonimo. Per un controllo preciso, uno può creare una firma di accesso condiviso, che consente l'accesso con restrizioni toodelegate con autorizzazioni diverse e in un intervallo di tempo specificato. Assicurarsi che non venga assegnato per errore l'accesso anonimo a contenitori e BLOB, che possono contenere dati sensibili.</p>|

## <a id="limited-access-sas"></a>Concedere l'accesso limitato tooobjects nell'archiviazione di Azure usando SAS o SAP

| Titolo                   | Dettagli      |
| ----------------------- | ------------ |
| **Componente**               | Archiviazione di Azure | 
| **Fase SDL**               | Compilare |  
| **Tecnologie applicabili** | Generico |
| **Attributes (Attributi) (Attributi)**              | N/D |
| **Riferimenti**              | [Firme di accesso condiviso, parte 1: Modello di firma di accesso condiviso hello informazioni](https://azure.microsoft.com/documentation/articles/storage-dotnet-shared-access-signature-part-1/), [firme di accesso condiviso, parte 2: creare e usare una firma di accesso condiviso con archiviazione Blob](https://azure.microsoft.com/documentation/articles/storage-dotnet-shared-access-signature-part-2/), [come toodelegate accedere tooobjects nell'account utilizzando Firme di accesso condiviso e criteri di accesso archiviati](https://azure.microsoft.com/documentation/articles/storage-security-guide/#_how-to-delegate-access-to-objects-in-your-account-using-shared-access-signatures-and-stored-access-policies) |
| **Passaggi** | <p>Utilizzando una firma di accesso condiviso (SAS) è un tooobjects di accesso limitato toogrant efficace in un client tooother di account di archiviazione, senza la chiave di accesso account tooexpose. Hello firma di accesso condiviso è un URI che include i parametri di query tutte hello informazioni necessarie per l'autenticazione di accesso tooa risorsa di archiviazione. risorse di archiviazione tooaccess con hello SAS, hello client deve disporre solo toopass nel metodo o costruttore di hello SAS toohello appropriato.</p><p>Quando si desidera che nel client tooa account di archiviazione che non può essere considerato attendibile con chiave dell'account hello tooprovide tooresources di accesso, è possibile utilizzare una firma di accesso condiviso. Le chiavi di account di archiviazione includono sia una chiave primaria e secondaria, di concedere l'account di accesso amministrativo tooyour e tutte le risorse di hello in essa contenuti. Esposizione di uno delle chiavi dell'account viene aperto il possibilità toohello account d'uso dannoso o non appropriata. Le firme di accesso condiviso forniscono un metodo alternativo che consente ad altri client tooread, scrittura ed eliminare i dati nell'account di archiviazione in base sono state concesse le autorizzazioni di toohello e senza necessità di chiave dell'account hello.</p><p>Se è disponibile un set logico di parametri simili ogni volta, è preferibile usare i criteri di accesso archiviati. Poiché l'utilizzo di una SAS derivata da un criterio di accesso archiviato offre toorevoke possibilità hello che firma di accesso condiviso immediatamente, è hello consigliata best practice tooalways utilizzare criteri di accesso archiviati quando possibile.</p>|

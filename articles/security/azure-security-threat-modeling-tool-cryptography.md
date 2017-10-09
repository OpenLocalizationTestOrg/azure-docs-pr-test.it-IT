---
title: aaaCryptography - modellazione strumento Microsoft Threat - Azure | Documenti Microsoft
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
ms.openlocfilehash: cab981bf116a0e76bbf44fe0f0a1a3650e4ab0f8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="security-frame-cryptography--mitigations"></a>Infrastruttura di sicurezza: crittografia - Procedure di mitigazione 
| Prodotto o servizio | Articolo |
| --------------- | ------- |
| **Applicazione Web** | <ul><li>[Usare solo crittografie a blocchi simmetriche e lunghezze di chiave approvate](#cipher-length)</li><li>[Usare modalità di crittografia a blocchi approvate e vettori di inizializzazione per crittografie simmetriche](#vector-ciphers)</li><li>[Usare riempimenti, lunghezze di chiave e algoritmi asimmetrici approvati](#padding)</li><li>[Usare generatori di numeri casuali approvati](#numgen)</li><li>[Non usare crittografie di flusso simmetriche](#stream-ciphers)</li><li>[Usare algoritmi MAC/HMAC/hash con chiave](#mac-hash)</li><li>[Usare solo funzioni hash crittografiche approvate](#hash-functions)</li></ul> |
| **Database** | <ul><li>[Utilizzare dati tooencrypt algoritmi di crittografia nel database di hello](#strong-db)</li><li>[I pacchetti SSIS devono essere crittografati ed essere con firma digitale](#ssis-signed)</li><li>[Aggiungere entità a protezione diretta di firma digitale toocritical database](#securables-db)</li><li>[Usare chiavi di crittografia tooprotect EKM di SQL server](#ekm-keys)</li><li>[Utilizzare la funzionalità crittografia sempre attiva, se le chiavi di crittografia non devono essere individuate tooDatabase motore](#keys-engine)</li></ul> |
| **Dispositivo IoT** | <ul><li>[Archiviare le chiavi di crittografia in modo sicuro nel dispositivo IoT](#keys-iot)</li></ul> | 
| **Gateway IoT cloud** | <ul><li>[Generare una chiave simmetrica casuale di lunghezza sufficiente per l'autenticazione tooIoT Hub](#random-hub)</li></ul> | 
| **Client Dynamics CRM Mobile** | <ul><li>[Assicurarsi che sia attivo un criterio di gestione dei dispositivi che richiede di usare il PIN e consente la cancellazione remota](#pin-remote)</li></ul> | 
| **Client Dynamics CRM per Outlook** | <ul><li>[Assicurarsi che sia attivo un criterio di gestione dei dispositivi che richiede PIN/password/blocco automatico e crittografa tutti i dati (ad esempio, Bitlocker)](#bitlocker)</li></ul> | 
| **Identity Server** | <ul><li>[Assicurarsi che venga eseguito il rollover delle chiavi di firma quando si usa Identity Server](#rolled-server)</li><li>[Assicurarsi che vengano usati un ID client e un segreto client con crittografia complessa in Identity Server](#client-server)</li></ul> | 

## <a id="cipher-length"></a>Usare solo crittografie a blocchi simmetriche e lunghezze di chiave approvate

| Titolo                   | Dettagli      |
| ----------------------- | ------------ |
| **Componente**               | Applicazione Web. | 
| **Fase SDL**               | Compilare |  
| **Tecnologie applicabili** | Generico |
| **Attributes (Attributi) (Attributi)**              | N/D  |
| **Riferimenti**              | N/D  |
| **Passaggi** | <p>I prodotti devono utilizzare solo i blocchi simmetrica e le lunghezze delle chiavi associate in modo esplicito riconosciuti da hello Crypto Advisor nell'organizzazione. Gli algoritmi simmetrici approvati Microsoft includono hello seguendo le crittografie a blocchi:</p><ul><li>Per il codice nuovo, sono accettabili AES-128, AES-192 e AES-256.</li><li>Per la compatibilità con le versioni precedenti del codice esistente, è accettabile 3DES a tre chiavi.</li><li>Per i prodotti che usano le crittografie a blocchi simmetriche:<ul><li>Per il codice nuovo, è necessario Advanced Encryption Standard (AES).</li><li>Triple Data Encryption Standard (3DES) a tre chiavi è consentito nel codice esistente per la compatibilità con le versioni precedenti.</li><li>Tutte le altre crittografie a blocchi, incluse RC2, DES, 3DES a 2 chiavi, DESX e Skipjack, possono essere usate solo per decrittografare i dati precedenti e devono essere sostituite se usate per la crittografia.</li></ul></li><li>Per gli algoritmi di crittografia a blocchi simmetrici, è necessaria una lunghezza minima della chiave di 128 bit. Hello solo l'algoritmo di crittografia di blocco consigliato per il nuovo codice è AES (AES-128, AES 192 e AES-256 sono consentiti)</li><li>Tre chiavi 3DES è attualmente accettabile se è già in uso nel codice esistente. è consigliabile tooAES di transizione. DES, DESX, RC2 e Skipjack non sono più considerati sicuri. Questi algoritmi possono essere utilizzati solo per la decrittografia dei dati esistenti per i migliori risultati hello di compatibilità con le versioni precedenti, e dati devono essere crittografati nuovamente utilizzando una crittografia a blocchi consigliato</li></ul><p>Si noti che tutte le crittografie a blocchi simmetriche devono essere usate con una modalità di crittografia approvata, che richiede l'uso di un vettore di inizializzazione appropriato. Un vettore di inizializzazione appropriato è in genere un numero casuale, mai un valore costante.</p><p>utilizzo di Hello di algoritmi di crittografia non approvati legacy o in caso contrario e lunghezze di chiave inferiore per la lettura dei dati esistenti (come toowriting anziché nuovi dati) è ammessa dopo esaminare scheda crittografia della propria organizzazione. È tuttavia necessario prevedere un'eccezione per questo requisito. Inoltre, nelle distribuzioni aziendali, i prodotti opportuno gli amministratori di avviso quando la crittografia debole tooread utilizzati dati. Tali avvisi devono essere descrittivi e operativi. In alcuni casi, potrebbe essere toohave appropriato utilizzare hello controllo di criteri di gruppo di crittografia debole</p><p>Algoritmi .NET consentiti per la flessibilità crittografica gestita (in ordine di preferenza):</p><ul><li>AesCng (conforme allo standard FIPS)</li><li>AuthenticatedAesCng (conforme allo standard FIPS)</li><li>AESCryptoServiceProvider (conforme allo standard FIPS)</li><li>AESManaged (non conforme allo standard FIPS)</li></ul><p>Si noti che nessuno di questi algoritmi possono essere specificate tramite hello `SymmetricAlgorithm.Create` o `CryptoConfig.CreateFromName` metodi senza file Machine. config toohello di modifiche. Si noti inoltre che nelle versioni di .NET precedente too.NET 3.5 AES è denominato `RijndaelManaged`, e `AesCng` e `AuthenticatedAesCng` sono > disponibile tramite CodePlex necessari CNG hello sottostante del sistema operativo</p>

## <a id="vector-ciphers"></a>Usare modalità di crittografia a blocchi approvate e vettori di inizializzazione per crittografie simmetriche

| Titolo                   | Dettagli      |
| ----------------------- | ------------ |
| **Componente**               | Applicazione Web. | 
| **Fase SDL**               | Compilare |  
| **Tecnologie applicabili** | Generico |
| **Attributes (Attributi) (Attributi)**              | N/D  |
| **Riferimenti**              | N/D  |
| **Passaggi** | Tutte le crittografie a blocchi simmetriche devono essere usate con una modalità di crittografia a blocchi approvata. modalità di Hello solo approvato sono CBC e CTS. In particolare, è opportuno evitare hello codice elettronico libro (ECB) modalità operativa; utilizzo di ECB richiede revisione scheda crittografia della propria organizzazione. Ogni utilizzo di OFB, CFB, CTR, CCM e GCM o di altre modalità di crittografia deve essere esaminato dal team di crittografia dell'organizzazione. Riutilizzo di hello stesso vettore di inizializzazione (IV) con crittografia a blocchi in "streaming gli algoritmi di crittografia, le modalità", ad esempio CTRL, potrebbe essere rivelate toobe di dati crittografati. Tutte le crittografie a blocchi simmetriche devono anche essere usate con un vettore di inizializzazione appropriato. Un vettore di inizializzazione appropriato è un numero casuale con una crittografia complessa, mai un valore costante. |

## <a id="padding"></a>Usare riempimenti, lunghezze di chiave e algoritmi asimmetrici approvati

| Titolo                   | Dettagli      |
| ----------------------- | ------------ |
| **Componente**               | Applicazione Web. | 
| **Fase SDL**               | Compilare |  
| **Tecnologie applicabili** | Generico |
| **Attributes (Attributi) (Attributi)**              | N/D  |
| **Riferimenti**              | N/D  |
| **Passaggi** | <p>utilizzo di Hello escluso di algoritmi di crittografia introduce sicurezza tooproduct rischio significativo e deve essere evitato. I prodotti devono usare solo gli algoritmi di crittografia e le lunghezze di chiave e i riempimenti associati esplicitamente approvati dal team di crittografia dell'organizzazione.</p><ul><li>**RSA**: può essere usato per la crittografia, lo scambio di chiave e la firma. La crittografia RSA deve usare solo hello OAEP o RSA KEM modalità di spaziatura interna. Il codice esistente può usare la modalità di riempimento PKCS #1 v1.5 solo per la compatibilità. L'uso del riempimento null è esplicitamente vietato. Per il codice nuovo sono necessarie chiavi >= 2048 bit. Il codice esistente può supportare chiavi < 2048 bit solo per la compatibilità con le versioni precedenti dopo una revisione da parte del team di crittografia dell'organizzazione. Le chiavi < 1024 bit possono essere usate solo per decrittografare/verificare i dati precedenti e devono essere sostituite se usate per operazioni di crittografia o di firma.</li><li>**ECDSA**: può essere usato solo per la firma. Per il codice nuovo è necessario ECDSA con chiavi >=256 bit. Le firme basate su ECDSA devono usare una delle curve NIST approvato hello tre (p-256, p-384 o P521). Le curve che sono state analizzate a fondo possono essere usate solo dopo una revisione da parte del team di crittografia dell'organizzazione.</li><li>**ECDH**: può essere usato solo per lo scambio di chiave. Per il codice nuovo è necessario ECDH con chiavi >=256 bit. Scambio di chiavi basate su ECDH deve usare una delle curve NIST approvato hello tre (p-256, p-384 o P521). Le curve che sono state analizzate a fondo possono essere usate solo dopo una revisione da parte del team di crittografia dell'organizzazione.</li><li>**DSA**: può essere accettabile dopo la revisione e l'approvazione da parte del team di crittografia dell'organizzazione. Contattare il tooschedule advisor sicurezza revisione scheda crittografia della propria organizzazione. Se l'utilizzo di DSA viene approvata, si noti che è necessario utilizzare tooprohibit delle chiavi di meno di 2048 bit. CNG supporta chiavi di lunghezza pari e superiore a 2048 bit a partire da Windows 8.</li><li>**Diffie-Hellman**: può essere usato solo per la gestione delle chiavi della sessione. Per il codice nuovo sono necessarie chiavi di lunghezza >= 2048 bit. Il codice esistente può supportare chiavi di lunghezza < 2048 bit solo per la compatibilità con le versioni precedenti dopo una revisione da parte del team di crittografia dell'organizzazione. Le chiavi < 1024 bit non possono essere usate.</li><ul>

## <a id="numgen"></a>Usare generatori di numeri casuali approvati

| Titolo                   | Dettagli      |
| ----------------------- | ------------ |
| **Componente**               | Applicazione Web. | 
| **Fase SDL**               | Compilare |  
| **Tecnologie applicabili** | Generico |
| **Attributes (Attributi) (Attributi)**              | N/D  |
| **Riferimenti**              | N/D  |
| **Passaggi** | <p>I prodotti devono usare generatori di numeri casuali approvati. Funzioni pseudocasuale, ad esempio hello C runtime funzione rand, classe di .NET Framework hello Random o funzioni di sistema, ad esempio GetTickCount, pertanto, non devono essere utilizzate in tale codice. Utilizzo di hello doppio a curva ellittica algoritmo numeri casuali generatore (DUAL_EC_DRBG) non è consentito</p><ul><li>**CNG -** BCryptGenRandom (utilizzo del flag BCRYPT_USE_SYSTEM_PREFERRED_RNG hello consigliato a meno che il chiamante hello potrebbe essere eseguito in qualsiasi livello IRQL maggiore di 0 [, ovvero PASSIVE_LEVEL])</li><li>**CAPI**: cryptGenRandom.</li><li>**Win32/64**: RtlGenRandom (le nuove implementazioni devono usare BCryptGenRandom o CryptGenRandom) * rand_s * SystemPrng (per la modalità kernel)</li><li>**.NET**: RNGCryptoServiceProvider o RNGCng.</li><li>**Applicazioni Windows Store**: Windows.Security.Cryptography.CryptographicBuffer.GenerateRandom o .GenerateRandomNumber.</li><li>**Apple OS X (10.7+)/iOS(2.0+) -** int SecRandomCopyBytes (SecRandomRef casuale, conteggio size_t, uint8_t *byte)</li><li>**Apple OS X (< 10.7)-** utilizzare / tooretrieve DEV/casuale di numeri casuali</li><li>**Java(compreso il codice Java di Google per Android) -** classe java.security.SecureRandom. Si noti che per Android 4.3 (gelatina Bean), gli sviluppatori devono seguire hello Android consigliato soluzione alternativa e aggiornare le applicazioni tooexplicitly inizializzare hello PRNG con entropia da /dev/urandom o /dev/random</li></ul>|

## <a id="stream-ciphers"></a>Non usare crittografie di flusso simmetriche

| Titolo                   | Dettagli      |
| ----------------------- | ------------ |
| **Componente**               | Applicazione Web. | 
| **Fase SDL**               | Compilare |  
| **Tecnologie applicabili** | Generico |
| **Attributes (Attributi) (Attributi)**              | N/D  |
| **Riferimenti**              | N/D  |
| **Passaggi** | Non devono essere usate crittografie di flusso simmetriche, ad esempio RC4. Invece delle crittografie di flusso simmetriche, i prodotti devono usare una crittografia a blocchi, in particolare AES con una lunghezza di chiave di almeno 128 bit. |

## <a id="mac-hash"></a>Usare algoritmi MAC/HMAC/hash con chiave

| Titolo                   | Dettagli      |
| ----------------------- | ------------ |
| **Componente**               | Applicazione Web. | 
| **Fase SDL**               | Compilare |  
| **Tecnologie applicabili** | Generico |
| **Attributes (Attributi) (Attributi)**              | N/D  |
| **Riferimenti**              | N/D  |
| **Passaggi** | <p>I prodotti devono usare solo algoritmi MAC (Message Authentication Code) o HMAC (Hash Message Authentication Code) approvati.</p><p>Un message authentication code (MAC) è una parte del messaggio associata tooa informazioni che consente il destinatario tooverify sia hello autenticità del mittente hello e l'integrità di hello del messaggio hello utilizzando una chiave privata. utilizzo di un MAC basati su hash Hello ([HMAC](http://csrc.nist.gov/publications/nistpubs/800-107-rev1/sp800-107-rev1.pdf)) o [MAC basato su crittografia a blocchi](http://csrc.nist.gov/publications/nistpubs/800-38B/SP_800-38B.pdf) è consentito, purché tutti sottostante hash o gli algoritmi di crittografia simmetrica anche approvati per l'uso; attualmente questo include funzioni HMAC SHA2 (HMAC-SHA256, SHA384 di HMAC e HMAC-SHA512) hello e hello CMAC/OMAC1 e OMAC2 blocco basati su crittografia Mac (basati su AES).</p><p>Utilizzo del valore HMAC-SHA1 potrebbe essere consentito per compatibilità con la piattaforma, ma verrà richiesto toofile routine eccezione toothis ed essere sottoposto a revisione di crittografia dell'organizzazione. Non è consentito il troncamento dei tooless Hashed a 128 bit. Utilizzando cliente metodi toohash una chiave e i dati non viene approvata e deve essere sottoposto a toouse precedente revisione di lavagna di crittografia dell'organizzazione.</p>|

## <a id="hash-functions"></a>Usare solo funzioni hash crittografiche approvate

| Titolo                   | Dettagli      |
| ----------------------- | ------------ |
| **Componente**               | Applicazione Web. | 
| **Fase SDL**               | Compilare |  
| **Tecnologie applicabili** | Generico |
| **Attributes (Attributi) (Attributi)**              | N/D  |
| **Riferimenti**              | N/D  |
| **Passaggi** | <p>I prodotti devono utilizzare famiglia hello SHA-2 degli algoritmi di hash (SHA256, SHA384 e SHA512). Se è necessario un hash più breve, ad esempio una lunghezza di 128 bit output in ordine toofit una struttura di dati progettata con hash MD5 più breve di hello presenti, i team di prodotto possono troncare uno degli hash SHA2 hello (in genere SHA256). Si noti che SHA384 è una versione troncata di SHA512. Troncamento di hash di crittografia per tooless a scopo di sicurezza a 128 bit non è consentito. Nuovo codice non deve utilizzare gli algoritmi di hash MD2, MD4, MD5, SHA-0, SHA-1 o RIPEMD hello. Da un punto di vista computazionale, le collisioni di hash sono possibili per questi algoritmi, che li interrompono in modo efficace.</p><p>Algoritmi hash .NET consentiti per la flessibilità crittografica gestita (in ordine di preferenza):</p><ul><li>SHA512Cng (conforme allo standard FIPS)</li><li>SHA384Cng (conforme allo standard FIPS)</li><li>SHA256Cng (conforme allo standard FIPS)</li><li>SHA512Managed (non-conformi a FIPS) (utilizzare SHA512 come nome di algoritmo in chiamate tooHashAlgorithm.Create o CryptoConfig.CreateFromName)</li><li>SHA384Managed (non-conformi a FIPS) (utilizzare SHA384 come nome di algoritmo in chiamate tooHashAlgorithm.Create o CryptoConfig.CreateFromName)</li><li>SHA256Managed (non-conformi a FIPS) (utilizzare SHA256 come nome di algoritmo in chiamate tooHashAlgorithm.Create o CryptoConfig.CreateFromName)</li><li>SHA512CryptoServiceProvider (conforme allo standard FIPS)</li><li>SHA256CryptoServiceProvider (conforme allo standard FIPS)</li><li>SHA384CryptoServiceProvider (conforme allo standard FIPS)</li></ul>| 

## <a id="strong-db"></a>Utilizzare dati tooencrypt algoritmi di crittografia nel database di hello

| Titolo                   | Dettagli      |
| ----------------------- | ------------ |
| **Componente**               | Database | 
| **Fase SDL**               | Compilare |  
| **Tecnologie applicabili** | Generico |
| **Attributes (Attributi) (Attributi)**              | N/D  |
| **Riferimenti**              | [Scelta di un algoritmo di crittografia](https://technet.microsoft.com/library/ms345262(v=sql.130).aspx) |
| **Passaggi** | Gli algoritmi di crittografia definiscono trasformazioni dei dati che non possono essere facilmente invertite da utenti non autorizzati. SQL Server consente agli amministratori e sviluppatori toochoose tra diversi algoritmi, tra cui DES, Triple DES, TRIPLE_DES_3KEY, RC2, RC4, RC4 a 128 bit, DESX, AES a 128 bit, AES a 192 bit e AES a 256 bit |

## <a id="ssis-signed"></a>I pacchetti SSIS devono essere crittografati ed essere con firma digitale

| Titolo                   | Dettagli      |
| ----------------------- | ------------ |
| **Componente**               | Database | 
| **Fase SDL**               | Compilare |  
| **Tecnologie applicabili** | Generico |
| **Attributes (Attributi) (Attributi)**              | N/D  |
| **Riferimenti**              | [Identificare l'origine dei pacchetti con firme digitali hello](https://msdn.microsoft.com/library/ms141174.aspx), [attenuazione di minacce e vulnerabilità (Integration Services)](https://msdn.microsoft.com/library/bb522559.aspx) |
| **Passaggi** | origine Hello di un pacchetto è hello singoli o un'organizzazione che ha creato il pacchetto di hello. Eseguire un pacchetto da un'origine sconosciuta o non attendibile può essere rischioso. tooprevent non autorizzato l'eventuale manomissione di pacchetti SSIS, è necessario usare firme digitali. Necessario, inoltre, la riservatezza di hello tooensure dei pacchetti hello durante l'archiviazione/transito, pacchetti SSIS toobe crittografati |

## <a id="securables-db"></a>Aggiungere entità a protezione diretta di firma digitale toocritical database

| Titolo                   | Dettagli      |
| ----------------------- | ------------ |
| **Componente**               | Database | 
| **Fase SDL**               | Compilare |  
| **Tecnologie applicabili** | Generico |
| **Attributes (Attributi) (Attributi)**              | N/D  |
| **Riferimenti**              | [ADD SIGNATURE (Transact-SQL)](https://msdn.microsoft.com/library/ms181700) |
| **Passaggi** | Nei casi in cui l'integrità di un'entità a protezione diretta del database di importanza critica hello presenti toobe verificato, le firme digitali da utilizzare. Le entità a protezione diretta del database critiche, ad esempio stored procedure, funzioni, assembly o trigger, possono essere con firma digitale. Di seguito è riportato un esempio di quando può essere utile: supponiamo un ISV (Independent Software Vendor) è fornito supporto tooa software recapitati tooone dei clienti. Prima di fornire supporto, hello ISV desideri tooensure che un database a protezione diretta nel software hello non sia stato manomesso per errore o da un tentativo non autorizzato. Se è firmato digitalmente hello entità a protezione diretta, hello ISV può verificare la firma digitale e convalidare l'integrità.| 

## <a id="ekm-keys"></a>Usare chiavi di crittografia tooprotect EKM di SQL server

| Titolo                   | Dettagli      |
| ----------------------- | ------------ |
| **Componente**               | Database | 
| **Fase SDL**               | Compilare |  
| **Tecnologie applicabili** | Generico |
| **Attributes (Attributi) (Attributi)**              | N/D  |
| **Riferimenti**              | [Extensible Key Management (EKM) di SQL Server](https://msdn.microsoft.com/library/bb895340), [Extensible Key Management con Azure Key Vault (SQL Server)](https://msdn.microsoft.com/library/dn198405) |
| **Passaggi** | SQL Server Extensible Key Management consente le chiavi di crittografia hello proteggere hello toobe di file di database archiviati in un dispositivo esterno come una smart card, un dispositivo USB o un modulo EKM/HSM. Consente anche la protezione dei dati da parte degli amministratori di database (tranne i membri del gruppo sysadmin hello). Dati possono essere crittografati utilizzando le chiavi di crittografia che solo hello utente del database ha accesso tooon hello modulo esterno EKM/HSM. |

## <a id="keys-engine"></a>Utilizzare la funzionalità crittografia sempre attiva, se le chiavi di crittografia non devono essere individuate tooDatabase motore

| Titolo                   | Dettagli      |
| ----------------------- | ------------ |
| **Componente**               | Database | 
| **Fase SDL**               | Compilare |  
| **Tecnologie applicabili** | SQL Azure, locale |
| **Attributes (Attributi) (Attributi)**              | Versione SQL: V12, MsSQL2016 |
| **Riferimenti**              | [Always Encrypted (Motore di database)](https://msdn.microsoft.com/library/mt163865) |
| **Passaggi** | Always Encrypted è un funzionalità progettata tooprotect dati sensibili, ad esempio numeri di carta di credito o numeri di identificazione nazionali (ad esempio fiscali), archiviati in Database SQL di Azure o SQL Server database. Always Encrypted consente ai client tooencrypt dati sensibili all'interno delle applicazioni client senza mai rivelare toohello le chiavi di crittografia hello motore di Database (Database SQL o SQL Server). Di conseguenza, crittografia sempre attiva crea una separazione tra chi possiede i dati di hello (e può visualizzarli) e chi gestisce i dati hello (ma non può accedervi) |

## <a id="keys-iot"></a>Archiviare le chiavi di crittografia in modo sicuro nel dispositivo IoT

| Titolo                   | Dettagli      |
| ----------------------- | ------------ |
| **Componente**               | Dispositivo IoT | 
| **Fase SDL**               | Compilare |  
| **Tecnologie applicabili** | Generico |
| **Attributes (Attributi) (Attributi)**              | Sistema operativo dispositivo: Windows IoT Core, connettività dispositivo: Azure IoT SDK per dispositivi |
| **Riferimenti**              | [TPM on Windows IoT Core](https://developer.microsoft.com/windows/iot/docs/tpm) (TPM in Windows IoT Core), [Set up TPM on Windows IoT Core](https://developer.microsoft.com/windows/iot/win10/setuptpm) (Configurare TPM in Windows IoT Core), [Azure IoT Device SDK TPM](https://github.com/Azure/azure-iot-hub-vs-cs/wiki/Device-Provisioning-with-TPM) (TPM di Azure IoT SDK per dispositivi) |
| **Passaggi** | Archiviare le chiavi private dei certificati o simmetriche in modo sicuro in una risorsa di archiviazione hardware protetta, ad esempio chip di smart card o TPM. Windows 10 IoT Core supporta utente hello di un TPM e sono disponibili diversi moduli TPM compatibile che può essere utilizzato: https://developer.microsoft.com/windows/iot/win10/tpm. È consigliabile toouse un Firmware o TPM discreti. Un modulo TPM software deve essere usato solo a scopo di sviluppo e test. Una volta un TPM è disponibile e vengono effettuato il provisioning di chiavi hello in essa contenuti, hello che genera token hello scrivere il codice senza livello di codice informazioni riservate in essa contenuti. | 

### <a name="example"></a>Esempio
```
TpmDevice myDevice = new TpmDevice(0);
// Use logical device 0 on hello TPM 
string hubUri = myDevice.GetHostName(); 
string deviceId = myDevice.GetDeviceId(); 
string sasToken = myDevice.GetSASToken(); 

var deviceClient = DeviceClient.Create( hubUri, AuthenticationMethodFactory. CreateAuthenticationWithToken(deviceId, sasToken), TransportType.Amqp); 
```
Come si può notare, chiave primaria di hello dispositivo non è presente nel codice hello. Viene invece memorizzato in hello TPM nello slot 0. Dispositivo TPM genera un breve durata token di firma di accesso condiviso che viene quindi utilizzato tooconnect toohello IoT Hub. 

## <a id="random-hub"></a>Generare una chiave simmetrica casuale di lunghezza sufficiente per l'autenticazione tooIoT Hub

| Titolo                   | Dettagli      |
| ----------------------- | ------------ |
| **Componente**               | Gateway IoT cloud | 
| **Fase SDL**               | Compilare |  
| **Tecnologie applicabili** | Generico |
| **Attributes (Attributi) (Attributi)**              | Opzione gateway: Hub IoT di Azure |
| **Riferimenti**              | N/D  |
| **Passaggi** | L'hub IoT contiene un registro di identità del dispositivo e durante il provisioning genera automaticamente una chiave simmetrica casuale. È consigliabile toouse questa funzionalità di hello Azure IoT Hub identità toogenerate hello chiave utilizzata per l'autenticazione. IoT Hub consente inoltre di una chiave toobe specificato durante la creazione dispositivo hello. Se viene generata una chiave di fuori di IoT Hub durante il provisioning del dispositivo, è consigliabile toocreate una chiave simmetrica casuale o almeno 256 bit. |

## <a id="pin-remote"></a>Assicurarsi che sia attivo un criterio di gestione dei dispositivi che richiede di usare il PIN e consente la cancellazione remota

| Titolo                   | Dettagli      |
| ----------------------- | ------------ |
| **Componente**               | Client Dynamics CRM Mobile | 
| **Fase SDL**               | Distribuzione |  
| **Tecnologie applicabili** | Generico |
| **Attributes (Attributi) (Attributi)**              | N/D  |
| **Riferimenti**              | N/D  |
| **Passaggi** | Assicurarsi che sia attivo un criterio di gestione dei dispositivi che richiede di usare il PIN e consente la cancellazione remota. |

## <a id="bitlocker"></a>Assicurarsi che sia attivo un criterio di gestione dei dispositivi che richiede PIN/password/blocco automatico e crittografa tutti i dati (ad esempio, Bitlocker)

| Titolo                   | Dettagli      |
| ----------------------- | ------------ |
| **Componente**               | Client Dynamics CRM per Outlook | 
| **Fase SDL**               | Compilare |  
| **Tecnologie applicabili** | Generico |
| **Attributes (Attributi) (Attributi)**              | N/D  |
| **Riferimenti**              | N/D  |
| **Passaggi** | Assicurarsi che sia attivo un criterio di gestione dei dispositivi che richiede PIN/password/blocco automatico e crittografa tutti i dati (ad esempio, Bitlocker). |

## <a id="rolled-server"></a>Assicurarsi che venga eseguito il rollover delle chiavi di firma quando si usa Identity Server

| Titolo                   | Dettagli      |
| ----------------------- | ------------ |
| **Componente**               | Identity Server | 
| **Fase SDL**               | Distribuzione |  
| **Tecnologie applicabili** | Generico |
| **Attributes (Attributi) (Attributi)**              | N/D  |
| **Riferimenti**              | [Identity Server - Keys, Signatures and Cryptography](https://identityserver.github.io/Documentation/docsv2/configuration/crypto.html) (Identity Server: chiavi, firme e crittografia) |
| **Passaggi** | Assicurarsi che venga eseguito il rollover delle chiavi di firma quando si usa Identity Server. collegamento Hello nella sezione dei riferimenti hello viene illustrato come questa dovrebbe essere pianificata senza provocare interruzioni tooapplications basarsi su identità Server. |

## <a id="client-server"></a>Assicurarsi che vengano usati un ID client e un segreto client con crittografia complessa in Identity Server

| Titolo                   | Dettagli      |
| ----------------------- | ------------ |
| **Componente**               | Identity Server | 
| **Fase SDL**               | Compilare |  
| **Tecnologie applicabili** | Generico |
| **Attributes (Attributi) (Attributi)**              | N/D  |
| **Riferimenti**              | N/D  |
| **Passaggi** | <p>Assicurarsi che vengano usati un ID client e un segreto client con crittografia complessa in Identity Server. durante la generazione di un ID client e un segreto, è necessario utilizzare Hello alle linee guida:</p><ul><li>Generare un GUID casuale come hello client ID</li><li>Generare una chiave casuale a 256 bit come segreto hello</li></ul>|

---
title: note sulla versione di .NET insieme di credenziali 2. x API aaaKey | Documenti Microsoft
description: Gli sviluppatori .NET utilizzeranno questo toocode API per insieme credenziali chiavi Azure
services: key-vault
author: BrucePerlerMS
manager: mbaldwin
editor: bruceper
ms.assetid: 1cccf21b-5be9-4a49-8145-483b695124ba
ms.service: key-vault
ms.devlang: CSharp
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 05/02/2017
ms.author: bruceper
ms.openlocfilehash: d95b84cf73c155f117f37e93893f27b02a75855c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="azure-key-vault-net-20---release-notes-and-migration-guide"></a>Guida alla migrazione e note sulla versione .NET 2.0 per l'insieme di credenziali delle chiavi di Azure
Hello note e linee guida seguenti sono per gli sviluppatori che utilizzano .NET insieme di credenziali chiave di Azure / libreria di c#. In fase di transizione hello dalla versione di hello 1.0 versione toohello 2.0, un numero di aggiornamenti è stato apportato che richiedono operazioni di migrazione del codice affinché toobenefit dai miglioramenti funzionali hello e funzionalità aggiunte come **insieme di credenziali chiave i certificati** supportano.

## <a name="key-vault-certificates"></a>Certificati Key Vault

Fornisce il supporto di certificati di chiave dell'insieme di credenziali per la gestione del x509 certificati e hello comportamenti seguenti:  

* Consente un toocreate di proprietario del certificato a un certificato tramite un processo di creazione dell'insieme di credenziali chiave o importazione di hello di un certificato esistente. Sono inclusi i certificati autofirmati e i certificati generati dall'autorità di certificazione.
* Consente il proprietario di un certificato di chiave dell'insieme di credenziali di archiviazione protetta tooimplement e la gestione di X509 certificati senza l'interazione con materiale della chiave privata.  
* Consente un toocreate di proprietario del certificato di un criterio che indirizza l'insieme di credenziali chiave toomanage hello del ciclo di vita di un certificato.  
* Consente ai proprietari di certificato tooprovide informazioni di contatto per la notifica sugli eventi del ciclo di vita di scadenza e il rinnovo del certificato.  
* Viene supportato il rinnovo automatico con autorità di certificazione selezionate, ad esempio provider di certificati X509 / Autorità di certificazione partner dell'insieme di credenziali delle chiavi.
  
  * Nota: Non collaborato provider/autorità sono inoltre consentite ma non supporta funzionalità di rinnovo automatico hello.

## <a name="net-support"></a>Supporto .NET

* **.NET 4.0** non è supportata dalla versione di hello 2.0 di .NET insieme credenziali chiavi Azure hello / libreria di c#
* **.NET core** è supportata dalla versione di hello 2.0 di .NET insieme credenziali chiavi Azure hello / libreria di c#

## <a name="namespaces"></a>Spazi dei nomi

* spazio dei nomi per Hello **modelli** viene modificato da **Microsoft.Azure.KeyVault** troppo**Microsoft.Azure.KeyVault.Models**.
* Hello **Microsoft.Azure.KeyVault.Internal** dello spazio dei nomi viene eliminato.
* spazio dei nomi di Hello Azure SDK le dipendenze vengono modificate da **Hyak.Common** e **Hyak.Common.Internals** troppo**Microsoft.Rest** e  **Microsoft.Rest.Serialization**

## <a name="type-changes"></a>Modifiche del tipo

* *Segreto* modificato troppo*SecretBundle*
* *Dizionario* modificato troppo*IDictionary*
* *Elenco<T>, string []* modificato troppo*IList<T>*
* *NextList* modificato troppo *NextPageLink*

## <a name="return-types"></a>Tipi restituiti

* **KeyList** e **SecretList** restituiranno *IPage<T>* anziché *ListKeysResponseMessage*
* Hello generato **BackupKeyAsync** restituirà *BackupKeyResult* contenente *valore* (blob di backup). Prima di hello metodo è stato sottoposto a wrapping e restituire unico valore hello.

## <a name="exceptions"></a>Eccezioni

* *KeyVaultClientException* è stato modificato anche*KeyVaultErrorException*
* Errore del servizio Hello viene modificato da *eccezione. Errore* troppo*eccezione. Body.Error.Message*.
* Rimuovere informazioni aggiuntive nel messaggio di errore hello per **[JsonExtensionData]**.

## <a name="constructors"></a>Costruttori

* Invece di accettare un *HttpClient* come un argomento del costruttore, hello costruttore accetta solo *HttpClientHandler* o *DelegatingHandler []*.

## <a name="downloaded-packages"></a>Pacchetti scaricati

Quando un client viene elaborata una dipendenza in seguito hello insieme di credenziali chiave sono stati scaricati

### <a name="previous-package-list"></a>Elenco dei pacchetti precedenti

* package id="Hyak.Common" version="1.0.2" targetFramework="net45"
* package id="Microsoft.Azure.Common" version="2.0.4" targetFramework="net45"
* package id="Microsoft.Azure.Common.Dependencies" version="1.0.0" targetFramework="net45"
* package id="Microsoft.Azure.KeyVault" version="1.0.0" targetFramework="net45"
* package id="Microsoft.Bcl" version="1.1.9" targetFramework="net45"
* package id="Microsoft.Bcl.Async" version="1.0.168" targetFramework="net45"
* package id="Microsoft.Bcl.Build" version="1.0.14" targetFramework="net45"
* package id="Microsoft.Net.Http" version="2.2.22" targetFramework="net45"

### <a name="current-package-list"></a>Elenco dei pacchetti correnti

* package id="Microsoft.Azure.KeyVault" version="2.0.0-preview" targetFramework="net45"
* package id="Microsoft.Rest.ClientRuntime" version="2.2.0" targetFramework="net45"
* package id="Microsoft.Rest.ClientRuntime.Azure" version="3.2.0" targetFramework="net45"

## <a name="class-changes"></a>Modifiche alle classi

* La **UnixEpoch** è stata rimossa
* **Base64UrlConverter** classe viene rinominata troppo**Base64UrlJsonConverter**

## <a name="other-changes"></a>Altre modifiche

* È stato aggiunto supporto per la configurazione di hello del criterio di ripetizione KV operazione nel caso di errori temporanei versione toothis di hello API.

## <a name="microsoftazuremanagementkeyvault-nuget"></a>Microsoft.Azure.Management.KeyVault NuGet

* Per le operazioni di hello che ha restituito un *insieme di credenziali*, tipo restituito di hello è una classe che contiene una proprietà dell'insieme di credenziali. Hello tipo restituito è ora *insieme di credenziali*.
* *PermissionsToKeys* e *PermissionsToSecrets* ora sono *Permissions.Keys* e *Permissions.Secrets*
* Alcune di hello restituiscono toohello Pannello di controllo anche di applicare le modifiche di tipi.

## <a name="microsoftazurekeyvaultextensions-nuget"></a>Microsoft.Azure.KeyVault.Extensions NuGet

* pacchetto di Hello viene suddivisa in troppo**Microsoft.Azure.KeyVault.Extensions** e **Microsoft.Azure.KeyVault.Cryptography** per le operazioni di crittografia hello.


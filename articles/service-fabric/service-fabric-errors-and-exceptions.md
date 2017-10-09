---
title: eccezioni FabricClient aaaCommon | Documenti Microsoft
description: Descrive le eccezioni comuni di hello e gli errori che possono essere generati da hello FabricClient APIs durante l'esecuzione di operazioni di gestione di applicazioni e i cluster.
services: service-fabric
documentationcenter: .net
author: rwike77
manager: timlt
editor: 
ms.assetid: bb821313-b221-479f-b08e-36cf07e60a07
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 06/01/2017
ms.author: ryanwi
ms.openlocfilehash: 55bb556b25150524ebc28756eb1bd3e91dc37853
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="common-exceptions-and-errors-when-working-with-hello-fabricclient-apis"></a>Eccezioni e gli errori quando si lavora con hello FabricClient APIs comuni
Hello [FabricClient](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient#System_Fabric_FabricClient) API consentono cluster applicazione amministratori tooperform attività amministrative e in un'applicazione di Service Fabric, servizio o del cluster. Ad esempio, la distribuzione di applicazioni, l'aggiornamento e la rimozione, verifica integrità hello un cluster o il test di un servizio. Gli sviluppatori di applicazioni e gli amministratori di cluster, utilizzare gli strumenti toodevelop hello FabricClient API per la gestione delle applicazioni e i cluster di Service Fabric hello.

Esistono molti tipi diversi di operazioni che possono essere eseguite tramite FabricClient.  Ogni metodo può generare eccezioni per gli errori a causa di problemi di infrastruttura temporanei, errori di runtime o tooincorrect input.  Vedere toofind documentazione di riferimento hello API quali eccezioni vengono generate da un metodo specifico. Esistono alcune eccezioni, tuttavia, che possono essere generate da diverse API [FabricClient](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient#System_Fabric_FabricClient). Hello nella tabella seguente vengono elencate hello le eccezioni che sono comuni a hello FabricClient APIs.

| Eccezione | Generata quando |
| --- |:--- |
| [System.Fabric.FabricObjectClosedException](https://docs.microsoft.com/dotnet/api/system.fabric.fabricobjectclosedexception#System_Fabric_FabricObjectClosedException) |Hello [FabricClient](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient#System_Fabric_FabricClient) oggetto si trova in uno stato chiuso. Smaltire hello [FabricClient](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient#System_Fabric_FabricClient) oggetto si utilizza e creare un'istanza di un nuovo [FabricClient](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient#System_Fabric_FabricClient) oggetto. |
| [System.TimeoutException](https://docs.microsoft.com/dotnet/core/api/system.timeoutexception#System_TimeoutException) |timeout dell'operazione Hello. [OperationTimedOut](https://docs.microsoft.com/dotnet/api/system.fabric.fabricerrorcode#System_Fabric_FabricErrorCode) viene restituito quando l'operazione di hello richiede più toocomplete MaxOperationTimeout. |
| [System.UnauthorizedAccessException](https://docs.microsoft.com/dotnet/core/api/system.unauthorizedaccessexception#System_UnauthorizedAccessException) |controllo dell'accesso per l'operazione di hello Hello non riuscita. Viene restituito E_ACCESSDENIED. |
| [System.Fabric.FabricException](https://docs.microsoft.com/dotnet/api/system.fabric.fabricexception#System_Fabric_FabricException) |Si è verificato un errore di runtime durante l'esecuzione dell'operazione di hello. Uno dei metodi FabricClient hello può potenzialmente generare [FabricException](https://docs.microsoft.com/dotnet/api/system.fabric.fabricexception#System_Fabric_FabricException), hello [ErrorCode](https://docs.microsoft.com/dotnet/api/system.fabric.fabricexception#System_Fabric_FabricException_ErrorCode) causa hello dell'eccezione hello è indicata dalla proprietà. Codici di errore definiti in hello [FabricErrorCode](https://docs.microsoft.com/dotnet/api/system.fabric.fabricerrorcode#System_Fabric_FabricErrorCode) enumerazione. |
| [System.Fabric.FabricTransientException](https://docs.microsoft.com/dotnet/api/system.fabric.fabrictransientexception#System_Fabric_FabricTransientException) |Hello non riuscita a causa di condizione di errore temporaneo tooa di qualche tipo. Ad esempio, un'operazione potrebbe non riuscire perché un quorum di repliche non è temporaneamente raggiungibile. Eccezioni temporanee corrispondono toofailed operazioni che è possibile ritentare. |

Alcuni errori [FabricErrorCode](https://docs.microsoft.com/dotnet/api/system.fabric.fabricerrorcode#System_Fabric_FabricErrorCode) comuni che possono essere restituiti in un'eccezione [FabricException](https://docs.microsoft.com/dotnet/api/system.fabric.fabricexception#System_Fabric_FabricException):

| Errore | Condizione |
| --- |:--- |
| CommunicationError |A causa di un errore di comunicazione hello operazione toofail, operazione hello tentativi. |
| InvalidCredentialType |tipo di credenziale Hello non è valido. |
| InvalidX509FindType |Hello X509FindType non è valido. |
| InvalidX509StoreLocation |percorso dell'archivio Hello X509 non è valido. |
| InvalidX509StoreName |nome dell'archivio Hello X509 non è valido. |
| InvalidX509Thumbprint |la stringa di identificazione personale del certificato X509 Hello non è valida. |
| InvalidProtectionLevel |livello di protezione Hello non è valido. |
| InvalidX509Store |Impossibile aprire l'archivio di certificati X509 Hello. |
| InvalidSubjectName |nome del soggetto Hello non è valido. |
| InvalidAllowedCommonNameList |Hello formato della stringa di elenco nome comune non è valido. Deve essere un elenco delimitato da virgole. |


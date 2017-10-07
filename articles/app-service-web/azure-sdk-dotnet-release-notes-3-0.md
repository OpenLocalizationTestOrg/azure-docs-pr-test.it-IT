---
title: note sulla versione di .NET 3.0 SDK per aaaAzure | Documenti Microsoft
description: Note sulla versione di Azure SDK per .NET 3.0
services: app-service\web
documentationcenter: .net
author: chrissfanos
editor: 
ms.assetid: c83d815b-fc19-4260-821e-7d2a7206dffc
ms.service: app-service
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: integration
ms.date: 03/07/2017
ms.author: juliako
ms.openlocfilehash: 8970b4c9b64de40dc29a33d69006a00ae5e38a50
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="azure-sdk-for-net-30-release-notes"></a>Note sulla versione di Azure SDK per .NET 3.0

In questo argomento include le note sulla versione per la versione 3.0 di hello Azure SDK per .NET.

##<a name="azure-sdk-for-net-30-release-summary"></a>Riepilogo sulla versione Azure SDK per .NET 3.0

Data di rilascio: 07/03/2017
 
Nessun toohello modifiche di rilievo Azure SDK 3.0 sono state introdotte in questa versione. Non è inoltre alcun tooleverage del processo di aggiornamento necessita questo SDK con i progetti servizio Cloud esistenti. Utilizzare tooallow di hello Azure SDK 3.0 senza la necessità di un processo di aggiornamento, Azure SDK 3.0 installa toohello stesse directory come Azure SDK 2.9. La maggior parte dei componenti di hello non è stata modificata la versione principale di hello da 2.9 ma invece appena aggiornato il numero di build hello.

## <a name="visual-studio-2017-rtw"></a>Visual Studio 2017 RTW

- In Visual Studio 2017, questa versione di hello Azure SDK per .NET è incorporata in toohello del carico di lavoro di Azure. Tutti gli strumenti di hello è necessario lo sviluppo di Azure toodo faranno parte di Visual Studio 2017, in futuro. Per Visual Studio 2015 SDK hello sarà comunque disponibile tramite WebPI. Con il rilascio di Visual Studio 2017 sono state sospese le versioni di Azure SDK per .NET per Visual Studio 2013.

### <a name="azure-diagnostics"></a>Diagnostica Azure

- Tooonly comportamento modificato hello archiviare una stringa di connessione parziale con chiave hello sostituito da un token di stringa di connessione di archiviazione di diagnostica servizi Cloud. chiave di archiviazione effettivo Hello è ora archiviata nella cartella del profilo utente hello quindi può essere controllato l'accesso. Visual Studio verrà letta la chiave di archiviazione hello dalla cartella del profilo utente per il debug locale e il processo di pubblicazione. 
- Modifica di risposta toohello descritto in precedenza, Visual Studio Online team hello avanzato modello di attività di distribuzione di servizi Cloud di Azure pertanto gli utenti è possibile specificare la chiave di archiviazione hello per impostare l'estensione di diagnostica quando si pubblicano tooAzure nell'integrazione continua e la distribuzione.
- Abbiamo apportato la stringa di connessione protetta toostore possibili e per diagnostica Azure (WAD), risolvere i problemi di configurazione tra environements toohelp la suddivisione in token.
 
### <a name="windows-server-2016-virtual-machines"></a>Macchine virtuali Windows Server 2016

- Visual Studio supporta ora la distribuzione tooOS servizi Cloud macchine virtuali famiglia 5 (Windows Server 2016). Per i servizi cloud esistenti, è possibile modificare le impostazioni tootarget hello nuova famiglia di sistemi operativi. Quando si creano nuovi servizi cloud, se si sceglie il servizio di hello toocreate usando .net 4.6 o successiva, esso verrà aperto hello servizio toouse 5 famiglia del sistema operativo.  Per ulteriori informazioni, è possibile esaminare hello [famiglia di sistemi operativi Guest supportano tabella](../cloud-services/cloud-services-guestos-update-matrix.md).

### <a name="known-issues"></a>Problemi noti

- In Azure .NET SDK 3.0 si verifica un problema quando si rimuove Visual Studio 2017 in una configurazione side-by-side con Visual Studio 2015.  Se si dispone di hello Azure SDK installata per Visual Studio 2015, hello emulatore di archiviazione di Microsoft Azure e l'emulatore di calcolo di Microsoft Azure vengono rimosse se si disinstalla Visual Studio 2017.  Di conseguenza, durante la creazione e il debug di nuovi progetti di servizi cloud in Visual Studio 2015 verrà generato un errore. In ordine toofix questo problema, reinstallare hello Azure SDK da hello installazione guidata piattaforma Web.  Hello problema verrà risolto in un futuro aggiornamento a Visual Studio 2017.  .

 
### <a name="azure-in-role-cache"></a>Cache nel ruolo di Azure 

- Il supporto per Cache nel ruolo di Azure è terminato il 30 novembre 2016. Per altri dettagli, fare clic [qui](https://azure.microsoft.com/blog/azure-managed-cache-and-in-role-cache-services-to-be-retired-on-11-30-2016/).





---
title: note sulla versione 2.9 di .NET SDK per aaaAzure
description: Note sulla versione di Azure SDK per .NET 2.9
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
ms.date: 02/24/2017
ms.author: juliako
ms.openlocfilehash: 96df2b80224190cc2093e6bf350eaec224ac2e98
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="azure-sdk-for-net-29-release-notes"></a>Note sulla versione di Azure SDK per .NET 2.9

Questo argomento contiene le note sulle versioni 2.9 e 2.9.6 di Azure SDK per .NET.

##<a name="azure-sdk-for-net-296-release-summary"></a>Riepilogo sulla versione Azure SDK per .NET 2.9.6

Data di rilascio: 16/11/2016
 
Non toohello modifiche di rilievo in Azure SDK 2.9 sono state introdotte in questa versione. Non è inoltre alcun tooleverage del processo di aggiornamento necessita questo SDK con i progetti servizio Cloud esistenti.

### <a name="visual-studio-2017-release-candidate"></a>Visual Studio 2017 Release Candidate

- In Visual Studio RC 2017, questa versione di hello Azure SDK per .NET è incorporata in hello del carico di lavoro di Azure. Tutti gli strumenti di hello è necessario lo sviluppo di Azure toodo faranno parte di Visual Studio 2017 RC in futuro. Per Visual Studio 2015 e Visual Studio 2013, hello SDK sarà comunque disponibile tramite WebPI. Le versioni per Visual Studio 2013 di Azure SDK per .NET verranno sospese quando Visual Studio 2017 verrà rilasciato come prodotto finale. Seguire questa toodownload collegamento Visual Studio 2017 RC: https://www.visualstudio.com/vs/visual-studio-2017-rc/

### <a name="azure-diagnostics"></a>Diagnostica Azure

- Tooonly comportamento modificato hello archiviare una stringa di connessione parziale con chiave hello sostituito da un token di stringa di connessione di archiviazione di diagnostica servizi Cloud. chiave di archiviazione effettivo Hello è ora archiviata nella cartella del profilo utente hello quindi può essere controllato l'accesso. Visual Studio verrà letta la chiave di archiviazione hello dalla cartella del profilo utente per il debug locale e il processo di pubblicazione. 
- Modifica di risposta toohello descritto in precedenza, Visual Studio Online team hello avanzato modello di attività di distribuzione di servizi Cloud di Azure pertanto gli utenti è possibile specificare la chiave di archiviazione hello per impostare l'estensione di diagnostica quando si pubblicano tooAzure nell'integrazione continua e la distribuzione.
- Abbiamo apportato la stringa di connessione protetta toostore possibili e per diagnostica Azure (WAD), risolvere i problemi di configurazione tra environements toohelp la suddivisione in token.
 
### <a name="windows-server-2016-virtual-machines"></a>Macchine virtuali Windows Server 2016

- Visual Studio supporta ora la distribuzione tooOS servizi Cloud macchine virtuali famiglia 5 (Windows Server 2016). Per i servizi cloud esistenti, è possibile modificare le impostazioni tootarget hello nuova famiglia di sistemi operativi. Quando si creano nuovi servizi cloud, se si sceglie il servizio di hello toocreate usando .net 4.6 o successiva, esso verrà aperto hello servizio toouse 5 famiglia del sistema operativo.  Per ulteriori informazioni, è possibile esaminare hello [famiglia di sistemi operativi Guest supportano tabella](https://azure.microsoft.com/en-us/documentation/articles/cloud-services-guestos-update-matrix/).

#### <a name="known-issues"></a>Problemi noti

- Azure .NET SDK 2.9.6 è stata introdotta una restrizione che blocca la distribuzione di progetti non supportati .NET Framework (ad esempio .NET 4.6) tooany famiglia di sistemi operativi utilizzando < 5. Una soluzione alternativa viene fornita [qui](https://github.com/MicrosoftDocs/azure-cloud-services-files/tree/master/Azure%20Targets%20SDK%202.9).

 
### <a name="azure-in-role-cache"></a>Cache nel ruolo di Azure 

- Il supporto per Cache nel ruolo di Azure termina il 30 novembre 2016. Per altri dettagli, fare clic [qui](https://azure.microsoft.com/en-us/blog/azure-managed-cache-and-in-role-cache-services-to-be-retired-on-11-30-2016/).

### <a name="azure-resource-manager-templates-for-azure-stack"></a>Modelli di Azure Resource Manager per Azure Stack

- Azure Stack è stato introdotto come destinazione di distribuzione per i modelli di Azure Resource Manager.


## <a name="azure-sdk-for-net-29-summary"></a>Riepilogo su Azure SDK per .NET 2.9

## <a name="overview"></a>Panoramica
Questo documento contiene le note sulla versione di hello per hello Azure SDK versione 2.9 .NET. 

Per informazioni dettagliate sugli aggiornamenti in questa versione, vedere hello [post annuncio di Azure SDK 2.9](https://azure.microsoft.com/blog/announcing-visual-studio-azure-tools-and-sdk-2-9/).

## <a name="azure-sdk-29-for-visual-studio-2015-update-2-and-visual-studio-15-preview"></a>Anteprima di Azure SDK 2.9 per Visual Studio 2015 Update 2 e Visual Studio "15"
Questo aggiornamento include hello seguenti correzioni di bug:

* Problema correlato tooREST API Client generazione nella cui stringa hello "Tipo sconosciuto" venisse visualizzato come nome di hello della cartella di generazione di codice hello e/o nome hello dello spazio dei nomi hello rilasciati nel codice hello generato.
* Eseguire i processi Web tooScheduled correlate in cui hello informazioni di autenticazione si verifica un errore toobe passato toohello processo di provisioning dell'utilità di pianificazione.

Questo aggiornamento include hello nuova funzionalità seguente:

* Supporto per i servizi di App secondario nella scheda "Servizi" hello di hello finestra di dialogo provisioning di servizio App. 

## <a name="azure-data-lake-tools-for-visual-studio-2015-update-2"></a>Strumenti di Azure Data Lake per Visual Studio 2015 Update 2
Questo aggiornamento include seguente hello:

* **Gli strumenti di Azure Data Lake** per Visual Studio viene quindi unita hello Azure SDK per la versione di .NET. Hello viene installato automaticamente quando si installa Azure SDK. 
  
    strumento Hello viene aggiornato di frequente, visitare [qui](http://aka.ms/datalaketool) tooget hello aggiornamenti.
* **Esplora server** ora consente tooview tutti e creare alcune entità di metadati U-SQL. Per altre informazioni, vedere [questo](https://azure.microsoft.com/documentation/services/data-lake-analytics/) blog.

## <a name="hdinsight-tools"></a>Strumenti HDInsight
**Strumenti HDInsight** per Visual Studio ora supporta HDInsight versione 3.3, che include la visualizzazione di grafici Tez e altre correzioni della lingua.

## <a name="azure-resource-manager"></a>Gestione risorse di Azure
In questa versione è stato aggiunto il supporto di [KeyVault](../azure-resource-manager/resource-manager-keyvault-parameter.md) per i modelli di Resource Manager.

## <a name="see-also"></a>Vedere anche
[Post di annuncio di Azure SDK 2.9](https://azure.microsoft.com/blog/announcing-visual-studio-azure-tools-and-sdk-2-9/)


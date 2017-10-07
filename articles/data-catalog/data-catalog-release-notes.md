---
title: note sulla versione di catalogo dati aaaAzure | Documenti Microsoft
description: Note sulla versione del Catalogo dati di Azure.
services: data-catalog
documentationcenter: 
author: steelanddata
manager: NA
editor: 
tags: 
ms.assetid: 3aca9c49-45a4-4352-92e6-bd25ee3eacf7
ms.service: data-catalog
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-catalog
ms.date: 08/15/2017
ms.author: maroche
ms.openlocfilehash: 661826f66020ba72a885c6b14522b53c8b469d20
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="azure-data-catalog-release-notes"></a>Note sulla versione del Catalogo dati di Azure
## <a name="notes-for-hello-november-20-2015-release-of-azure-data-catalog"></a>Note sulla versione di hello 20 novembre 2015 di Azure Data Catalog
### <a name="opening-data-sources-in-power-bi-desktop"></a>Apertura di origini di dati in Power BI Desktop
Quando si utilizza l'opzione "Apri in Power BI Desktop" hello hello **Azure Data Catalog** portale, gli utenti possono verificarsi uno dei due problemi in hello applicazione Power BI Desktop:

* Viene visualizzata una finestra di dialogo con titolo hello "Non è possibile tooOpen documento"
* si apre Hello applicazione Power BI Desktop, ma sembra che file hello toobe vuoto

Per ogni situazione, è possibile risolvere il problema di hello scaricando e installando l'ultima versione di hello di Power BI Desktop da [PowerBI.com](https://powerbi.com).

## <a name="notes-for-hello-november-13-2015-release-of-azure-data-catalog"></a>Note sulla versione di hello 13 novembre 2015 di Azure Data Catalog
### <a name="registering-and-connecting-tooteradata"></a>La registrazione e connessione tooTeradata
Quando ci si connette a origini dati tooTeradata utenti sia installato il driver ODBC di Teradata corretto di hello che corrispondono ai bit hello (32 bit o 64 bit) del software hello in uso.

A partire da questo servizio ADC data di rilascio, hello più recente [driver ODBC di Teradata per windows (versione 15.10)](http://downloads.teradata.com/download/connectivity/odbc-driver/windows) è compatibile con Office 2013, ma non con Office 2016.

## <a name="notes-for-hello-july-13-2015-release-of-azure-data-catalog"></a>Note sulla versione di hello il 13 luglio 2015 di Azure Data Catalog
### <a name="registering-and-connecting-toooracle-database"></a>La registrazione e la connessione di Database tooOracle
Quando la connessione degli utenti di origini dati di tooOracle Database deve essere installato driver Oracle corretti hello che corrispondono ai bit hello (32 bit o 64 bit) del software hello in uso.

* Verrà utilizzato durante la registrazione di origini dati Oracle in un computer che esegue Windows a 32 bit, driver Oracle a 32 bit hello
* Verrà utilizzato durante la registrazione di origini dati Oracle in un computer che esegue Windows a 64 bit, driver Oracle a 64 bit hello
* Quando ci si connette a origini dati tooOracle utilizzando Excel in un computer con una versione a 32 bit hello di Microsoft Office, è incluso in Windows a 64 bit, verrà utilizzato driver Oracle a 32 bit hello
* Verrà utilizzato durante la connessione a origini dati tooOracle utilizzando Excel in un computer con una versione a 64 bit di Microsoft Office hello, driver Oracle a 64 bit hello

### <a name="registering-and-connecting-toosql-server-reporting-services"></a>La registrazione e connessione tooSQL Server Reporting Services
Il supporto per le origini dati di SQL Server Reporting Services (SSRS) è attualmente limitata tooNative solo i server in modalità. Il supporto per SSRS in modalità SharePoint verrà aggiunto in una versione successiva.

### <a name="opening-data-assets-in-excel"></a>Apertura degli asset di dati in Excel
Quando si apre l'asset di dati in Microsoft Excel dal hello **Azure Data Catalog** portale, gli utenti potrebbero essere richieste con un **avviso di protezione di Microsoft Excel** la finestra di dialogo. Si tratta di standard, il comportamento previsto e gli utenti possono selezionare **abilitare** toocontinue.

Per altre informazioni, vedere [Attivazione o disattivazione degli avvisi di protezione relativi ai collegamenti a siti Web sospetti e a file scaricati da tali siti](https://support.office.com/article/Enable-or-disable-security-alerts-about-links-and-files-from-suspicious-websites-A1AC6AE9-5C4A-4EB3-B3F8-143336039BBE).

### <a name="proxy-and-policy-configuration-and-data-source-registration"></a>Configurazione di proxy e criteri e registrazione dell'origine dati
Gli utenti possono riscontrare situazioni in cui possono registrare nel portale di Azure Data Catalog toohello, ma quando tentano di toolog su toohello strumento di registrazione origine dati che viene rilevato un messaggio di errore che ne impedisce l'accesso.

Le possibili cause di questo comportamento problematico sono due:

**Causa 1: Configurazione di Active Directory Federation Services** strumento per la registrazione di origine dati hello utilizza gli accessi utente toovalidate di autenticazione basata su form in Active Directory. Per l'accesso con esito positivo, autenticazione basata su form deve essere abilitato in Criteri di autenticazione globali hello dall'amministratore di Active Directory.

In alcuni casi, questo errore può verificarsi solo quando l'utente hello è nella rete aziendale hello o solo quando si connette utente hello dalla rete aziendale esterna hello. Criteri di autenticazione globali Hello consente toobe di metodi di autenticazione abilitato separatamente per le connessioni extranet e intranet. Se l'autenticazione basata su form non è abilitato per la rete hello dal quale hello utente si connette, potrebbero verificarsi errori di accesso.

Per altre informazioni, vedere [Configurare i criteri di autenticazione](https://technet.microsoft.com/library/dn486781.aspx).

**Causa 2: Configurazione del proxy di rete** se la rete aziendale hello utilizza un server proxy, lo strumento di registrazione hello potrebbe non essere in grado di tooconnect tooAzure Active Directory tramite proxy hello. Gli utenti possono verificare che lo strumento di registrazione hello modificando il file di configurazione dello strumento hello, aggiunta di questo file toohello sezione:

      <system.net>
        <defaultProxy useDefaultCredentials="true" enabled="true">
          <proxy usesystemdefault="True"
                          proxyaddress="http://<your corporate network proxy url>"
                          bypassonlocal="True"/>
        </defaultProxy>
      </system.net>


toolocate hello RegistrationTool.exe.config file, avviare lo strumento di registrazione hello e quindi aprire l'utilità Gestione attività Windows hello. Nella scheda dettagli di hello in Gestione attività, fare clic su RegistrationTool.exe e scegliere Apri percorso file dal menu a comparsa hello.

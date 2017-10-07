---
title: aaaAzure diagnostica versioni dello schema di configurazione dell'estensione e la cronologia | Documenti Microsoft
description: "Contatori delle prestazioni toocollecting rilevanti in macchine virtuali di Azure, il set di scalabilità di macchine Virtuali, Service Fabric e servizi Cloud."
services: monitoring-and-diagnostics
documentationcenter: .net
author: rboucher
manager: carmonm
editor: 
ms.assetid: 
ms.service: monitoring-and-diagnostics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 05/16/2017
ms.author: robb
ms.openlocfilehash: 854ad118f660810aa38703670284794d658142c7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="azure-diagnostics-extention-configuration-schema-versions-and-history"></a>Versioni e cronologia degli schemi di configurazione dell'estensione di Diagnostica di Azure
Gli indici di questa pagina versioni dello schema di estensione diagnostica di Azure fornito come parte di Microsoft Azure SDK hello.  

> [!NOTE]
> Hello estensione diagnostica di Azure è il componente di hello utilizzato toocollect contatori delle prestazioni e altre statistiche da:
> - Macchine virtuali di Azure 
> - Set di scalabilità di macchine virtuali
> - Service Fabric 
> - Servizi cloud 
> - Gruppi di sicurezza di rete
> 
> Questa pagina è utile solo se si usa uno di questi servizi.

Hello estensione diagnostica di Azure viene utilizzato con altri prodotti Microsoft, diagnostica quali monitoraggio di Azure, Application Insights e Analitica di Log. Per altre informazioni vedere [Panoramica degli strumenti di monitoraggio Microsoft](monitoring-overview.md).

## <a name="azure-sdk-and-diagnostics-versions-shipping-chart"></a>Grafico delle versioni fornite per Azure SDK e Diagnostica  

|Versione di Azure SDK | Versione dell'estensione di Diagnostica | Modello|  
|------------------|-------------------------------|------|  
|1.x               |1.0                            |plug-in|  
|2.0 - 2.4         |1.0                            |plug-in|  
|2.5               |1.2                            |estensione|  
|2.6               |1.3                            |"|  
|2.7               |1.4                            |"|  
|2.8               |1,5                            |"|  
|2,9               |1.6                            |"|
|2.96              |1.7                            |"|
|2.96              |1.8                            |"|
|2.96              |1.8.1                          |"|
|2.96              |1.9                            |"|



 Fornito in un modello di plug-in, vale a dire che al momento dell'installazione hello Azure SDK, è stato ottenuto con versione di hello di diagnostica Azure è dotata di diagnostica di Azure versione 1.0.  

 A partire da SDK 2.5 (diagnostica versione 1.2), diagnostica di Azure è verificato un modello di estensione tooan. nuove funzionalità di Hello strumenti tooutilize erano disponibili solo in SDK più recente di Azure, ma qualsiasi servizio mediante la diagnostica di Azure preleverebbe hello shipping più recente direttamente da Azure. Ad esempio, qualsiasi utente che utilizza ancora SDK 2.5 sarebbe caricamento illustrata nella tabella precedente hello, indipendentemente dal fatto che se usano le funzionalità più recenti di hello la versione più recente hello.  

## <a name="schemas-index"></a>Indice degli schemi  
Versioni diverse di Diagnostica di Azure usano schemi di configurazione diversi. 

[Schema di configurazione di Diagnostica 1.0](azure-diagnostics-schema-1dot0.md)  

[Schema di configurazione di Diagnostica 1.2](azure-diagnostics-schema-1dot2.md)  

[Schema di configurazione di Diagnostica 1.3 e versioni successive](azure-diagnostics-schema-1dot3-and-later.md)  

## <a name="version-history"></a>Cronologia delle versioni


### <a name="diagnostics-extension-19"></a>Estensione di Diagnostica 1.9 
Aggiunta del supporto Docker.


### <a name="diagnostics-extension-181"></a>Estensione di Diagnostica 1.8.1 
Può specificare un token di firma di accesso condiviso anziché una chiave di account di archiviazione nel file di configurazione privata hello. Se viene fornito un token di firma di accesso condiviso, chiave di account di archiviazione hello viene ignorato.


```json
{
    "storageAccountName": "diagstorageaccount",
    "storageAccountEndPoint": "https://core.windows.net",
    "storageAccountSasToken": "{sas token}",
    "SecondaryStorageAccounts": {
        "StorageAccount": [
            {
                "name": "secondarydiagstorageaccount",
                "endpoint": "https://core.windows.net",
                "sasToken": "{sas token}"
            }
        ]
    }
}
```

```xml
<PrivateConfig>
    <StorageAccount name="diagstorageaccount" endpoint="https://core.windows.net" sasToken="{sas token}" />
    <SecondaryStorageAccounts>
        <StorageAccount name="secondarydiagstorageaccount" endpoint="https://core.windows.net" sasToken="{sas token}" />
    </SecondaryStorageAccounts>
</PrivateConfig>
```


### <a name="diagnostics-extension-18"></a>Estensione di Diagnostica 1.8 
Aggiunta tooPublicConfig tipo di archiviazione. Il tipo di archiviazione può essere *Table*, *Blob* e *TableAndBlob*. *Tabella* hello predefinito.


```json
{
    "WadCfg": {
    },
    "StorageAccount": "diagstorageaccount",
    "StorageType": "TableAndBlob"
}
```

```xml
<PublicConfig>
    <WadCfg />
    <StorageAccount>diagstorageaccount</StorageAccount>
    <StorageType>TableAndBlob</StorageType>
</PublicConfig>
```


### <a name="diagnostics-extension-17"></a>Estensione di Diagnostica 1.7 
Aggiunta di hello possibilità tooroute tooEventHub.

### <a name="diagnostics-extension-15"></a>Estensione di Diagnostica 1.5
Aggiunto hello sink hello e elemento di dati di diagnostica di toosend possibilità troppo[Application Insights](../application-insights/app-insights-cloudservices.md) rendendo più semplice toodiagnose problemi tra l'applicazione, nonché a livello di sistema e l'infrastruttura di hello.

### <a name="azure-sdk-26-and-diagnostics-extension-13"></a>Azure SDK 2.6 ed estensione di Diagnostica 1.3 
Per i progetti servizio Cloud in Visual Studio, hello dopo le modifiche apportata. (Queste modifiche si applicano anche toolater versioni di Azure SDK.)

* emulatore locale Hello supporta ora la diagnostica. Questo significa che è possibile raccogliere dati di diagnostica e verificare che l'applicazione crea hello tracce corrette durante lo sviluppo ed il test in Visual Studio. stringa di connessione Hello `UseDevelopmentStorage=true` Abilita raccolta dati di diagnostica, mentre si esegue il progetto servizio cloud in Visual Studio utilizzando l'emulatore di archiviazione Azure hello. Tutti i dati di diagnostica vengono raccolti nell'account di archiviazione hello (archiviazione di sviluppo).
* stringa di connessione account archiviazione diagnostica Hello (Microsoft.WindowsAzure.Plugins.Diagnostics.ConnectionString) viene archiviato nuovamente nel file di configurazione (. cscfg) servizio hello. In Azure SDK 2.5 l'account di archiviazione di diagnostica hello è stato specificato nel file Diagnostics. wadcfgx hello.

Esistono alcune differenze sostanziali tra la stringa di connessione hello lavorato in Azure SDK 2.4 e versioni precedenti e sul relativo funzionamento in Azure SDK 2.6 e versioni successive.

* In Azure SDK 2.4 e versioni precedenti, la stringa di connessione hello è stata utilizzata come runtime dalle hello tooget di plug-in di diagnostica hello informazioni di account di archiviazione per il trasferimento di log di diagnostica.
* In Azure SDK 2.6 e versioni successive, stringa di connessione di diagnostica hello viene utilizzato dall'estensione di diagnostica di Visual Studio tooconfigure hello con informazioni sull'account di archiviazione appropriato hello durante la pubblicazione. stringa di connessione Hello consente di definire diversi account di archiviazione per le configurazioni di servizio diverso che Visual Studio verrà utilizzato durante la pubblicazione. Tuttavia, poiché plug-in di hello diagnostica non è più disponibile (dopo Azure SDK 2.5), file con estensione cscfg hello da sola non è possibile abilitare hello estensione di diagnostica. È l'estensione di hello tooenable separatamente tramite strumenti quali Visual Studio o PowerShell.
* processo di hello toosimplify di configurazione dell'estensione di diagnostica hello con PowerShell, output del pacchetto hello da Visual Studio contiene anche hello pubblico XML di configurazione per l'estensione diagnostica hello per ogni ruolo. Visual Studio Usa hello diagnostica sulle stringhe di connessione toopopulate hello storage account presenti nella configurazione pubblica hello. file di configurazione pubblica Hello vengono creati nella cartella estensioni hello e seguono pattern hello PaaSDiagnostics. <RoleName>. Paasdiagnostics.<NomeRuolo>.pubconfig.Xml. Tutte le distribuzioni basate su PowerShell è possono utilizzare il toomap questo modello ogni tooa configurazione ruolo.
* Hello stringa di connessione nel file con estensione cscfg hello viene anche usato dai dati di diagnostica di Azure tooaccess portale hello hello in modo che può essere visualizzati in hello **monitoraggio** stringa di connessione scheda hello è tooconfigure necessari hello servizio tooshow dettagliato dati di monitoraggio nel portale di hello.

#### <a name="migrating-projects-tooazure-sdk-26-and-later"></a>La migrazione dei progetti tooAzure SDK 2.6 e versioni successive
Quando la migrazione da Azure SDK 2.5 tooAzure SDK 2.6 o versione successiva, se si dispone di un account di archiviazione di diagnostica specificato nel file con estensione wadcfgx hello, quindi viene mantenuta non esiste. account tootake sfruttare la flessibilità di hello dell'utilizzo di archiviazione diversi per diverse configurazioni di archiviazione, sarà necessario toomanually aggiungere progetto tooyour stringa di connessione hello. Se si sta eseguendo la migrazione di un progetto da Azure SDK 2.4 o versioni precedenti tooAzure SDK 2.6, quindi hello vengono mantenute le stringhe di connessione di diagnostica. Tuttavia, si noti come stringhe di connessione vengono considerate in Azure SDK 2.6 specificato nella sezione precedente hello modifiche hello.

#### <a name="how-visual-studio-determines-hello-diagnostics-storage-account"></a>Determinazione di account di archiviazione di diagnostica hello Visual Studio
* Se si specifica una stringa di connessione di diagnostica nel file con estensione cscfg hello, Visual Studio viene utilizzata l'estensione diagnostica hello tooconfigure durante la pubblicazione e durante la generazione di file xml di configurazione pubblica hello durante la creazione di pacchetti.
* Se viene specificata alcuna stringa di connessione di diagnostica nel file con estensione cscfg hello, quindi Visual Studio esegue il fallback account di archiviazione hello toousing specificato hello wadcfgx tooconfigure hello diagnostica estensione di file durante la pubblicazione e la generazione di hello pubblico file di configurazione xml quando creazione del pacchetto.
* stringa di connessione di diagnostica Hello in file con estensione cscfg hello ha la precedenza su account di archiviazione hello in file con estensione wadcfgx hello. Se è una stringa di connessione di diagnostica specificati nel file con estensione cscfg hello, Visual Studio utilizza che e ignora l'account di archiviazione hello in con estensione wadcfgx.

#### <a name="what-does-hello-update-development-storage-connection-strings-checkbox-do"></a>Cosa does hello "Aggiorna stringhe di connessione di archiviazione..." …"
casella di controllo per Hello **Aggiorna stringhe di connessione di archiviazione per la diagnostica e la memorizzazione nella cache con le credenziali dell'account di archiviazione di Microsoft Azure quando si pubblicano tooMicrosoft Azure** offre un modo pratico di tooupdate qualsiasi archiviazione account stringhe di connessione con l'account di archiviazione di Azure hello specificato durante la pubblicazione.

Si supponga ad esempio si seleziona questa casella di controllo e hello stringa di connessione specifichi `UseDevelopmentStorage=true`. Quando si pubblica hello tooAzure di progetto, Visual Studio aggiornerà automaticamente stringa di connessione di diagnostica hello con account di archiviazione hello specificato nella procedura guidata di pubblicazione hello. Tuttavia, se un account di archiviazione reale è stato specificato come stringa di connessione di diagnostica hello, allora tale account viene utilizzato invece.

### <a name="diagnostics-functionality-differences-between-azure-sdk-24-and-earlier-and-azure-sdk-25-and-later"></a>Differenze della funzionalità di diagnostica tra Azure SDK 2.4 e versioni precedenti e Azure SDK 2.5 e versioni successive
Se si esegue l'aggiornamento del progetto da Azure SDK 2.4 tooAzure SDK 2.5 o versioni successive, è necessario tenere hello presente seguenti differenze di funzionalità di diagnostica.

* **Le API di configurazione sono deprecate** : la configurazione a livello di codice della diagnostica è disponibile in Azure SDK 2.4 o versioni precedenti, ma è deprecata in Azure SDK 2.5 e versioni successive. Se la configurazione della diagnostica è attualmente definita nel codice, è necessario tooreconfigure tali impostazioni da zero nel progetto di migrazione hello in ordine per l'utilizzo di diagnostica tookeep. file di configurazione di diagnostica di Hello per Azure SDK 2.4 è Diagnostics. wadcfg e Diagnostics. wadcfgx per Azure SDK 2.5 e versioni successive.
* **Diagnostica per le applicazioni di servizio cloud può essere configurata solo a livello di ruolo hello, non a livello di istanza hello.**
* **Ogni volta che si distribuisce l'app, viene aggiornata la configurazione di diagnostica hello** : ciò può causare problemi di parità se si modifica la configurazione di diagnostica da Esplora Server e quindi distribuire nuovamente l'app.
* **In Azure SDK 2.5 e versioni successive, i dump di arresto anomalo del sistema sono configurati nel file di configurazione diagnostica hello, non nel codice** : nel caso di arresto anomalo del sistema configurato nel codice, sarà necessario configurazione hello di trasferimento toomanually dal file di configurazione toohello di codice, perché i dump di arresto anomalo di hello non vengono trasferiti durante la migrazione di hello tooAzure SDK 2.6.


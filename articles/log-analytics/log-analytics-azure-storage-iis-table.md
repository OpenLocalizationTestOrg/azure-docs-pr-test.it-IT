---
title: archiviazione di blob aaaUse per IIS e la tabella di archiviazione per gli eventi in Azure Log Analitica | Documenti Microsoft
description: "Log Analitica può leggere i log di hello per servizi di Azure che scrivere di archiviazione di diagnostica tootable o scrittura tooblob archiviazione dei log IIS."
services: log-analytics
documentationcenter: 
author: MGoedtel
manager: carmonm
editor: 
ms.assetid: bf444752-ecc1-4306-9489-c29cb37d6045
ms.service: log-analytics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/12/2017
ms.author: magoedte
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: ff3de04dc8cb6729c1443372ec31a0e8dc47f273
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="use-azure-blob-storage-for-iis-and-azure-table-storage-for-events-with-log-analytics"></a>Usare l'archiviazione BLOB di Azure per IIS e l'archiviazione tabelle di Azure per gli eventi con Log Analytics

Log Analitica può leggere i log di hello per i seguenti servizi di archiviazione o IIS log scritto tooblob archiviazione scrivere diagnostica tootable hello:

* Cluster di Service Fabric (Anteprima)
* Macchine virtuali
* Ruoli di lavoro/Web

Affinché Log Analytics possa raccogliere i dati per tali risorse, è necessario abilitare la diagnostica di Azure.

Quando è abilitata la diagnostica, è possibile usare hello portale di Azure o PowerShell configurare Log Analitica toocollect hello registri.

Diagnostica di Azure è un'estensione di Azure che permette toocollect i dati di diagnostica da un ruolo di lavoro, un ruolo web o una macchina virtuale in esecuzione in Azure. dati di Hello vengono archiviati in un account di archiviazione di Azure e possono quindi essere raccolti da Log Analitica.

Per Log Analitica toocollect questi registri di diagnostica di Azure, hello log devono trovarsi in hello posizioni seguenti:

| Tipo di log | Tipo di risorsa | Località |
| --- | --- | --- |
| Log di IIS |Macchine virtuali <br> Ruoli Web <br> Ruoli di lavoro |wad-iis-logfiles (archivio BLOB) |
| syslog |Macchine virtuali |LinuxsyslogVer2v0 (archivio tabelle) |
| Eventi operativi di Service Fabric |Nodi di Service Fabric |WADServiceFabricSystemEventTable |
| Eventi di Reliable Actor di Service Fabric |Nodi di Service Fabric |WADServiceFabricReliableActorEventTable |
| Eventi di Reliable Service di Service Fabric |Nodi di Service Fabric |WADServiceFabricReliableServiceEventTable |
| Registri eventi di Windows |Nodi di Service Fabric <br> Macchine virtuali <br> Ruoli Web <br> Ruoli di lavoro |WADWindowsEventLogsTable (archivio tabelle) |
| Log di Windows ETW |Nodi di Service Fabric <br> Macchine virtuali <br> Ruoli Web <br> Ruoli di lavoro |WADETWEventTable (archivio tabelle) |

> [!NOTE]
> I log IIS provenienti dai siti Web di Azure non sono attualmente supportati.
>
>

Per le macchine virtuali, è possibile hello installazione hello [agente Log Analitica](log-analytics-azure-vm-extension.md) in informazioni aggiuntive dettagliate tooenable macchina virtuale. Inoltre i registri eventi e registri di IIS in grado di tooanalyze toobeing è possibile eseguire ulteriori analisi, tra cui il rilevamento delle modifiche di configurazione, valutazione di SQL e aggiornamento.

## <a name="enable-azure-diagnostics-in-a-virtual-machine-for-event-log-and-iis-log-collection"></a>Abilitare la diagnostica di Azure in una macchina virtuale per la raccolta di log eventi e IIS
Hello utilizzare seguendo procedure tooenable diagnostica di Azure in una macchina virtuale per il log eventi e IIS tramite il portale di Microsoft Azure hello insieme.

### <a name="tooenable-azure-diagnostics-in-a-virtual-machine-with-hello-azure-portal"></a>tooenable diagnostica di Azure in una macchina virtuale con hello portale di Azure
1. Installare l'agente VM hello quando si crea una macchina virtuale. Se esiste già una macchina virtuale hello, verificare che hello che agente VM è già installato.

   * In hello portale di Azure, passare una macchina virtuale toohello, selezionare **configurazione facoltativa**, quindi **diagnostica** e impostare **stato** troppo**su**.

     Al termine, hello VM ha estensione di diagnostica Azure hello installato e in esecuzione. che ha il compito di raccogliere i dati di diagnostica.
2. Abilitare il monitoraggio e configurare la registrazione degli eventi su una macchina virtuale esistente. È possibile abilitare la diagnostica in hello livello macchina virtuale. diagnostica tooenable e quindi configurare la registrazione degli eventi, eseguire hello alla procedura seguente:

   1. Selezionare hello macchina virtuale.
   2. Fare clic su **Monitoraggio**.
   3. Fare clic su **Diagnostica**.
   4. Set hello **stato** troppo**ON**.
   5. Selezionare ogni log di diagnostica che si desidera toocollect.
   6. Fare clic su **OK**.

## <a name="enable-azure-diagnostics-in-a-web-role-for-iis-log-and-event-collection"></a>Abilitare Diagnostica di Azure in un ruolo Web per la raccolta di eventi e log IIS
Fare riferimento troppo[come tooEnable diagnostica in un servizio Cloud](../cloud-services/cloud-services-dotnet-diagnostics.md) per i passaggi generali per l'abilitazione della diagnostica di Azure. istruzioni di Hello seguenti usare queste informazioni e personalizzarlo per l'utilizzo con Log Analitica.

Con Diagnostica di Azure abilitata:

* I log IIS vengono archiviati per impostazione predefinita, i dati di log trasferiti nell'intervallo di trasferimento scheduledTransferPeriod hello.
* Per impostazione predefinita, i registri eventi di Windows non vengono trasferiti.

### <a name="tooenable-diagnostics"></a>diagnostica tooenable
tooenable registri eventi di Windows o toochange hello scheduledTransferPeriod, configurare la diagnostica di Azure utilizzando hello file di configurazione XML (Diagnostics. wadcfg), come illustrato nella [passaggio 4: creare il file di configurazione di diagnostica e installare hello estensione](../cloud-services/cloud-services-dotnet-diagnostics.md)

Hello file di configurazione di esempio seguente raccoglie i log di IIS e tutti gli eventi dall'applicazione hello e registri di sistema:

```
    <?xml version="1.0" encoding="utf-8" ?>
    <DiagnosticMonitorConfiguration xmlns="http://schemas.microsoft.com/ServiceHosting/2010/10/DiagnosticsConfiguration"
          configurationChangePollInterval="PT1M"
          overallQuotaInMB="4096">

      <Directories bufferQuotaInMB="0"
         scheduledTransferPeriod="PT10M">  
        <!-- IISLogs are only relevant tooWeb roles -->
        <IISLogs container="wad-iis" directoryQuotaInMB="0" />
      </Directories>

      <WindowsEventLog bufferQuotaInMB="0"
         scheduledTransferLogLevelFilter="Verbose"
         scheduledTransferPeriod="PT10M">
        <DataSource name="Application!*" />
        <DataSource name="System!*" />
      </WindowsEventLog>

    </DiagnosticMonitorConfiguration>
```

Assicurarsi che ConfigurationSettings specifichi un account di archiviazione, come hello di esempio seguente:

```
    <ConfigurationSettings>
       <Setting name="Microsoft.WindowsAzure.Plugins.Diagnostics.ConnectionString" value="DefaultEndpointsProtocol=https;AccountName=<AccountName>;AccountKey=<AccountKey>"/>
    </ConfigurationSettings>
```

Hello **AccountName** e **AccountKey** i valori sono disponibili in hello portale Azure nel dashboard dell'account di archiviazione hello, in Gestisci chiavi di accesso. protocollo Hello hello stringa di connessione deve essere **https**.

Dopo aver applicata la configurazione di diagnostica aggiornati hello tooyour cloud service e sta scrivendo tooAzure diagnostica archiviazione, sarà necessario tooconfigure pronto Analitica di Log.

## <a name="use-hello-azure-portal-toocollect-logs-from-azure-storage"></a>Utilizzare i log di Azure toocollect portale hello da archiviazione di Azure
È possibile usare il log hello toocollect di hello tooconfigure portale Azure Log Analitica per hello seguenti servizi di Azure:

* Cluster di Service Fabric
* Macchine virtuali
* Ruoli di lavoro/Web

Nel portale di Azure hello, passare l'area di lavoro Log Analitica tooyour ed eseguire hello seguenti attività:

1. Fare clic su *Log account di archiviazione*
2. Fare clic su hello *Aggiungi* attività
3. Selezionare l'account di archiviazione hello che contiene i log di diagnostica hello
   * L'account di archiviazione può essere di tipo classico oppure un account di archiviazione di Azure Resource Manager
4. Selezionare il tipo di dati desiderato nei registri toocollect hello
   * opzioni di Hello sono registri IIS Eventi; Syslog (Linux); Log ETW; Eventi dell'infrastruttura del servizio
5. valore Hello di origine viene popolato automaticamente in base hello tipo di dati e non possono essere modificati
6. Fare clic su OK toosave hello configurazione

Ripetere i passaggi da 2 a 6 per i tipi di dati e gli account di ulteriore spazio di archiviazione che si desidera toocollect Analitica di Log.

In circa 30 minuti, si è in grado di toosee dati dall'account di archiviazione hello in Log Analitica. Viene visualizzata solo i dati scritti toostorage dopo la configurazione di hello viene applicata. Log Analitica leggere dati preesistenti hello dall'account di archiviazione hello.

> [!NOTE]
> portale Hello non convalidare tale hello origine esista nell'account di archiviazione hello o se sono scritti nuovi dati.
>
>

## <a name="enable-azure-diagnostics-in-a-virtual-machine-for-event-log-and-iis-log-collection-using-powershell"></a>Abilitare la diagnostica di Azure in una macchina virtuale per la raccolta di log eventi e log IIS tramite PowerShell
Hello di utilizzare i passaggi [tooindex Analitica Log di configurazione di diagnostica di Azure](log-analytics-powershell-workspace-configuration.md#configuring-log-analytics-to-index-azure-diagnostics) toouse PowerShell tooread da diagnostica di Azure che viene scritti tootable archiviazione.

Utilizzo di PowerShell di Azure è possibile specificare più precisamente hello gli eventi scritti tooAzure archiviazione.
Per altre informazioni, vedere [Abilitare la diagnostica nelle macchine virtuali di Azure](../virtual-machines-dotnet-diagnostics.md).

È possibile abilitare e aggiornare diagnostica Windows Azure utilizzando lo script di PowerShell seguente hello.
È possibile usare questo script anche con una configurazione della registrazione personalizzata.
Modificare l'account di archiviazione di hello script tooset hello, nome del servizio e il nome di macchina virtuale.
script di Hello Usa i cmdlet per le macchine virtuali classiche.

Esaminare hello seguente script di esempio, copiarlo, modificarlo se necessario, salvare l'esempio hello come file script di PowerShell e quindi eseguire script hello.

```
    #Connect tooAzure
    Add-AzureAccount

    # settings toochange:
    $wad_storage_account_name = "myStorageAccount"
    $service_name = "myService"
    $vm_name = "myVM"

    #Construct Azure Diagnostics public config and convert tooconfig format

    # Collect just system error events:
    $wad_xml_config = "<WadCfg><DiagnosticMonitorConfiguration><WindowsEventLog scheduledTransferPeriod=""PT1M""><DataSource name=""System!* "" /></WindowsEventLog></DiagnosticMonitorConfiguration></WadCfg>"

    $wad_b64_config = [System.Convert]::ToBase64String([System.Text.Encoding]::UTF8.GetBytes($wad_xml_config))
    $wad_public_config = [string]::Format("{{""xmlCfg"":""{0}""}}",$wad_b64_config)

    #Construct Azure diagnostics private config

    $wad_storage_account_key = (Get-AzureStorageKey $wad_storage_account_name).Primary
    $wad_private_config = [string]::Format("{{""storageAccountName"":""{0}"",""storageAccountKey"":""{1}""}}",$wad_storage_account_name,$wad_storage_account_key)

    #Enable Diagnostics Extension for Virtual Machine

    $wad_extension_name = "IaaSDiagnostics"
    $wad_publisher = "Microsoft.Azure.Diagnostics"
    $wad_version = (Get-AzureVMAvailableExtension -Publisher $wad_publisher -ExtensionName $wad_extension_name).Version # Gets latest version of hello extension

    (Get-AzureVM -ServiceName $service_name -Name $vm_name) | Set-AzureVMExtension -ExtensionName $wad_extension_name -Publisher $wad_publisher -PublicConfiguration $wad_public_config -PrivateConfiguration $wad_private_config -Version $wad_version | Update-AzureVM
```


## <a name="next-steps"></a>Passaggi successivi
* [Raccogliere i log e le metriche per i servizi di Azure](log-analytics-azure-storage.md) per i servizi supportati di Azure.
* [Abilitare soluzioni](log-analytics-add-solutions.md) tooprovide comprendere dati hello.
* [Utilizzare le query di ricerca](log-analytics-log-searches.md) dati hello tooanalyze.

---
title: aaaHow toouse diagnostica Windows Azure (.NET) con i servizi Cloud | Documenti Microsoft
description: Tramite diagnostica Azure toogather dati da Azure servizi cloud per il debug, la misurazione delle prestazioni, monitoraggio, analisi del traffico e altro ancora.
services: cloud-services
documentationcenter: .net
author: rboucher
manager: jwhit
editor: 
ms.assetid: 89623a0e-4e78-4b67-a446-7d19a35a44be
ms.service: cloud-services
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 05/22/2017
ms.author: robb
ms.openlocfilehash: 1525eac1e85955d8f05aa21a9805e0a80d0e4bca
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="enabling-azure-diagnostics-in-azure-cloud-services"></a>Abilitazione di Diagnostica di Azure in servizi cloud di Azure
Vedere [Panoramica di Diagnostica di Azure](../azure-diagnostics.md) per un'introduzione a Diagnostica di Azure.

## <a name="how-tooenable-diagnostics-in-a-worker-role"></a>Come tooEnable diagnostica in un ruolo di lavoro
Questa procedura dettagliata viene descritto come un ruolo di lavoro di Azure che genera dati di telemetria usando tooimplement hello classe EventSource .NET. Diagnostica di Azure è toocollect utilizzati dati di telemetria hello e archiviarlo in un account di archiviazione di Azure. Quando si crea un ruolo di lavoro, Visual Studio consente automaticamente Diagnostics 1.0 come parte della soluzione hello in Azure SDK per .NET 2.4 e versioni precedenti. Hello istruzioni seguenti descrivono il processo di hello per la creazione di ruolo di lavoro hello, disabilitazione Diagnostics 1.0 da soluzione hello e la distribuzione di diagnostica 1.2 o ruolo di lavoro tooyour 1.3.

### <a name="prerequisites"></a>Prerequisiti
In questo articolo si presuppone che si dispone di una sottoscrizione di Azure e si usa Visual Studio con hello Azure SDK. Se non si dispone di una sottoscrizione di Azure, è possibile iscriversi per hello [versione di valutazione gratuita][Free Trial]. Assicurarsi che troppo[installare e configurare Azure PowerShell 0.8.7 o versione successiva][Install and configure Azure PowerShell version 0.8.7 or later].

### <a name="step-1-create-a-worker-role"></a>Passaggio 1: Creare un ruolo di lavoro
1. Avviare **Visual Studio**.
2. Creare un **servizio Cloud di Azure** progetto da hello **Cloud** modello destinato a .NET Framework 4.5.  Nome progetto hello "WadExample" e fare clic su Ok.
3. Selezionare **Ruolo di lavoro** e fare clic su OK. verrà creato il progetto Hello.
4. In **Esplora**, fare doppio clic su hello **WorkerRole1** file delle proprietà.
5. In hello **configurazione** scheda deselezionare **Abilita diagnostica** toodisable Diagnostics 1.0 (Azure SDK 2.4 e versioni precedenti).
6. Compilare la soluzione tooverify che non siano presenti errori.

### <a name="step-2-instrument-your-code"></a>Passaggio 2: Instrumentare il codice
Sostituire il contenuto di hello del WorkerRole.cs con hello seguente codice. classe SampleEventSourceWriter, ereditato da hello Hello [classe EventSource][EventSource Class], implementa i quattro metodi di registrazione: **SendEnums**, **MessageMethod** , **SetOther** e **HighFreq**. primo parametro toohello Hello **WriteEvent** metodo definisce hello ID evento rispettivi hello. metodo Run Hello implementa un ciclo infinito che ogni hello chiama i metodi di registrazione implementati in hello **SampleEventSourceWriter** classe ogni 10 secondi.

```csharp
using Microsoft.WindowsAzure.ServiceRuntime;
using System;
using System.Diagnostics;
using System.Diagnostics.Tracing;
using System.Net;
using System.Threading;

namespace WorkerRole1
{
    sealed class SampleEventSourceWriter : EventSource
    {
        public static SampleEventSourceWriter Log = new SampleEventSourceWriter();
        public void SendEnums(MyColor color, MyFlags flags) { if (IsEnabled())  WriteEvent(1, (int)color, (int)flags); }// Cast enums tooint for efficient logging.
        public void MessageMethod(string Message) { if (IsEnabled())  WriteEvent(2, Message); }
        public void SetOther(bool flag, int myInt) { if (IsEnabled())  WriteEvent(3, flag, myInt); }
        public void HighFreq(int value) { if (IsEnabled()) WriteEvent(4, value); }

    }

    enum MyColor
    {
        Red,
        Blue,
        Green
    }

    [Flags]
    enum MyFlags
    {
        Flag1 = 1,
        Flag2 = 2,
        Flag3 = 4
    }

    public class WorkerRole : RoleEntryPoint
    {
        public override void Run()
        {
            // This is a sample worker implementation. Replace with your logic.
            Trace.TraceInformation("WorkerRole1 entry point called");

            int value = 0;

            while (true)
            {
                Thread.Sleep(10000);
                Trace.TraceInformation("Working");

                // Emit several events every time we go through hello loop
                for (int i = 0; i < 6; i++)
                {
                    SampleEventSourceWriter.Log.SendEnums(MyColor.Blue, MyFlags.Flag2 | MyFlags.Flag3);
                }

                for (int i = 0; i < 3; i++)
                {
                    SampleEventSourceWriter.Log.MessageMethod("This is a message.");
                    SampleEventSourceWriter.Log.SetOther(true, 123456789);
                }

                if (value == int.MaxValue) value = 0;
                SampleEventSourceWriter.Log.HighFreq(value++);
            }
        }

        public override bool OnStart()
        {
            // Set hello maximum number of concurrent connections
            ServicePointManager.DefaultConnectionLimit = 12;

            // For information on handling configuration changes
            // see hello MSDN topic at http://go.microsoft.com/fwlink/?LinkId=166357.

            return base.OnStart();
        }
    }
}
```


### <a name="step-3-deploy-your-worker-role"></a>Passaggio 3: Distribuire il ruolo di lavoro

[!INCLUDE [cloud-services-wad-warning](../../includes/cloud-services-wad-warning.md)]

1. Distribuire il tooAzure ruolo worker da Visual Studio selezionando hello **WadExample** progetto in hello quindi Esplora **pubblica** da hello **compilare** menu.
2. Scegliere la propria sottoscrizione.
3. In hello **impostazioni di pubblicazione di Microsoft Azure** finestra di dialogo Seleziona **Crea nuovo...** .
4. In hello **Crea servizio Cloud e Account di archiviazione** finestra di dialogo immettere un **nome** (ad esempio, "WadExample") e selezionare un'area o un gruppo di affinità.
5. Set hello **ambiente** troppo**gestione temporanea**.
6. Modificare le altre **impostazioni** nel modo appropriato e fare clic su **Pubblica**.
7. Una volta completata la distribuzione, verificare nel portale di Azure che il servizio cloud hello un **esecuzione** stato.

### <a name="step-4-create-your-diagnostics-configuration-file-and-install-hello-extension"></a>Passaggio 4: Creare il file di configurazione di diagnostica e installare l'estensione hello
1. Scarica definizione dello schema file di configurazione pubblica hello eseguendo hello comando PowerShell seguente:

    ```powershell
    (Get-AzureServiceAvailableExtension -ExtensionName 'PaaSDiagnostics' -ProviderNamespace 'Microsoft.Azure.Diagnostics').PublicConfigurationSchema | Out-File -Encoding utf8 -FilePath 'WadConfig.xsd'
    ```
2. Aggiungere un tooyour file XML **WorkerRole1** progetto facendo clic su hello **WorkerRole1** del progetto e selezionare **Aggiungi** -> **nuovo elemento...** -> **Elementi di Visual C#** -> **Dati** -> **File XML**. Il nome file hello "WadExample.xml".

   ![CloudServices_diag_add_xml](./media/cloud-services-dotnet-diagnostics/AddXmlFile.png)
3. Associare il file di configurazione di hello hello WadConfig.xsd. Verificare che nella finestra dell'editor WadExample.xml hello è la finestra attiva di hello. Premere **F4** tooopen hello **proprietà** finestra. Fare clic su hello **schemi** proprietà hello **proprietà** finestra. Fare clic su hello **...** in hello **schemi** proprietà. Fare clic su hello **Aggiungi...** pulsante e passare toohello percorso in cui è stato salvato file XSD hello e selezionare hello WadConfig.xsd. Fare clic su **OK**.

4. Sostituire il contenuto di hello hello WadExample.xml del file di configurazione con hello XML seguente e salvare il file hello. Questo file di configurazione definisce un paio toocollect di contatori delle prestazioni: uno per l'utilizzo della CPU e uno per l'utilizzo della memoria. Configurazione di hello definisce quattro eventi hello corrispondente toohello metodi nella classe SampleEventSourceWriter hello.

```xml
<?xml version="1.0" encoding="utf-8"?>
<PublicConfig xmlns="http://schemas.microsoft.com/ServiceHosting/2010/10/DiagnosticsConfiguration">
  <WadCfg>
    <DiagnosticMonitorConfiguration overallQuotaInMB="25000">
      <PerformanceCounters scheduledTransferPeriod="PT1M">
        <PerformanceCounterConfiguration counterSpecifier="\Processor(_Total)\% Processor Time" sampleRate="PT1M" unit="percent" />
        <PerformanceCounterConfiguration counterSpecifier="\Memory\Committed Bytes" sampleRate="PT1M" unit="bytes"/>
      </PerformanceCounters>
      <EtwProviders>
        <EtwEventSourceProviderConfiguration provider="SampleEventSourceWriter" scheduledTransferPeriod="PT5M">
          <Event id="1" eventDestination="EnumsTable"/>
          <Event id="2" eventDestination="MessageTable"/>
          <Event id="3" eventDestination="SetOtherTable"/>
          <Event id="4" eventDestination="HighFreqTable"/>
          <DefaultEvents eventDestination="DefaultTable" />
        </EtwEventSourceProviderConfiguration>
      </EtwProviders>
    </DiagnosticMonitorConfiguration>
  </WadCfg>
</PublicConfig>
```

### <a name="step-5-install-diagnostics-on-your-worker-role"></a>Passaggio 5: Installare la diagnostica nel ruolo di lavoro
Hello cmdlet PowerShell per la gestione di diagnostica in un ruolo web o di lavoro sono: Set-AzureServiceDiagnosticsExtension, Get-AzureServiceDiagnosticsExtension e Remove-AzureServiceDiagnosticsExtension.

1. Aprire Azure PowerShell.
2. Eseguire tooinstall script hello diagnostica nel ruolo di lavoro (sostituire *StorageAccountKey* con chiave dell'account di archiviazione per l'account di archiviazione wadexample hello e *config_path* con percorso hello toohello *WadExample.xml* file):

```powershell
$storage_name = "wadexample"
$key = "<StorageAccountKey>"
$config_path="c:\users\<user>\documents\visual studio 2013\Projects\WadExample\WorkerRole1\WadExample.xml"
$service_name="wadexample"
$storageContext = New-AzureStorageContext -StorageAccountName $storage_name -StorageAccountKey $key
Set-AzureServiceDiagnosticsExtension -StorageContext $storageContext -DiagnosticsConfigurationPath $config_path -ServiceName $service_name -Slot Staging -Role WorkerRole1
```

### <a name="step-6-look-at-your-telemetry-data"></a>Passaggio 6: Esaminare i dati di telemetria
In Visual Studio hello **Esplora Server**, passare toohello wadexample account di archiviazione. Dopo circa cinque (5) minuti è stato in esecuzione il servizio di cloud hello, dovrebbe essere tabelle hello **WADEnumsTable**, **WADHighFreqTable**, **WADMessageTable**, **WADPerformanceCountersTable** e **WADSetOtherTable**. Fare doppio clic su uno dei hello tabelle tooview hello dati di telemetria che sono stati raccolti.

![CloudServices_diag_tables](./media/cloud-services-dotnet-diagnostics/WadExampleTables.png)

## <a name="configuration-file-schema"></a>Schema del file di configurazione
file di configurazione della diagnostica Hello definisce i valori vengono utilizzati tooinitialize le impostazioni di configurazione all'avvio dell'agente di diagnostica hello. Vedere hello [riferimento allo schema più recente](https://msdn.microsoft.com/library/azure/mt634524.aspx) per i valori validi ed esempi.

## <a name="troubleshooting"></a>Risoluzione dei problemi
Se si verificano problemi, vedere l'argomento relativo alla [risoluzione dei problemi di Diagnostica di Azure](../azure-diagnostics-troubleshooting.md) per informazioni sui problemi comuni.

## <a name="next-steps"></a>Passaggi successivi
[Visualizzare un elenco di Azure macchina virtuale diagnostica articoli correlati](../monitoring-and-diagnostics/azure-diagnostics.md#cloud-services-using-azure-diagnostics) dati hello toochange si raccolgono, risolvere i problemi o per altre informazioni sulla diagnostica in generale.

[EventSource Class]: http://msdn.microsoft.com/library/system.diagnostics.tracing.eventsource(v=vs.110).aspx

[Debugging an Azure Application]: http://msdn.microsoft.com/library/windowsazure/ee405479.aspx   
[Collect Logging Data by Using Azure Diagnostics]: http://msdn.microsoft.com/library/windowsazure/gg433048.aspx
[Free Trial]: http://azure.microsoft.com/pricing/free-trial/
[Install and configure Azure PowerShell version 0.8.7 or later]: http://azure.microsoft.com/documentation/articles/install-configure-powershell/

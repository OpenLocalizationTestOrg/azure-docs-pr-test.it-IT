---
title: aaaHow toouse diagnostica nelle macchine virtuali di Azure | Documenti Microsoft
description: Utilizzando i dati di toogather diagnostica di Azure da macchine virtuali di Azure per il debug, la misurazione delle prestazioni, monitoraggio, analisi del traffico e altro ancora.
services: virtual-machines
documentationcenter: .net
author: davidmu1
manager: 
editor: 
ms.assetid: dfaabc7a-23e7-4af0-8369-f504d2915b3d
ms.service: virtual-machines
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 02/16/2016
ms.author: davidmu
ms.openlocfilehash: 54cdfd30d7bbbb71af449826e90234faf5ecdf44
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="enabling-diagnostics-in-azure-virtual-machines"></a>Abilitare la diagnostica nelle macchine virtuali di Azure
Vedere [Panoramica di Diagnostica di Azure](../monitoring-and-diagnostics/azure-diagnostics.md) per un'introduzione a Diagnostica di Azure.

## <a name="how-tooenable-diagnostics-in-a-virtual-machine"></a>Come tooEnable diagnostica in una macchina virtuale
Questa procedura dettagliata viene descritto come installare diagnostica tooan macchina virtuale di Azure di tooremotely da un computer di sviluppo. Verrà inoltre descritto come un'applicazione in esecuzione su tale macchina virtuale di Azure e genera dati di telemetria usando tooimplement hello .NET [classe EventSource][EventSource Class]. Diagnostica di Azure è dati di telemetria hello toocollect utilizzato e archiviarlo in un account di archiviazione di Azure.

### <a name="pre-requisites"></a>Prerequisiti
Questa procedura dettagliata si presuppone che si dispone di una sottoscrizione di Azure e si sta utilizzando Visual Studio 2017 con hello Azure SDK. Se non si dispone di una sottoscrizione di Azure, è possibile iscriversi per hello [versione di valutazione gratuita][Free Trial]. Assicurarsi che troppo[installare e configurare Azure PowerShell 0.8.7 o versione successiva][Install and configure Azure PowerShell version 0.8.7 or later].

### <a name="step-1-create-a-virtual-machine"></a>Passaggio 1: Creare una macchina virtuale
1. Nel computer di sviluppo, avviare Visual Studio 2017.
2. In Visual Studio hello **Esplora Server** espandere **Azure**, fare doppio clic su **macchine virtuali** selezionare **crea macchina virtuale**.
3. Selezionare la sottoscrizione di Azure in hello **scegliere una sottoscrizione** finestra di dialogo e fare clic su **Avanti**.
4. Selezionare **giugno 2017, Windows Server 2012 R2 Datacenter** in hello **selezionare un'immagine di macchina virtuale** finestra di dialogo e fare clic su **Avanti**.
5. In hello **le impostazioni di base di macchina virtuale**, impostare il nome di macchina virtuale hello troppo "wadexample". Impostare il nome utente e la password dell'amministratore e fare clic su **Avanti**.
6. In hello **le impostazioni del servizio Cloud** finestra di dialogo Crea un nuovo servizio cloud denominato "wadexampleVM". Creare un nuovo account di archiviazione denominato "wadexample" e fare clic su **Avanti**.
7. Fare clic su **Create**.

### <a name="step-2-create-your-application"></a>Passaggio 2: Creare l'applicazione
1. Nel computer di sviluppo, avviare Visual Studio 2017.
2. Creare una nuova applicazione console Visual C# per .NET Framework 4.5. Nome progetto hello "WadExampleVM".

   ![CloudServices_diag_new_project](./media/virtual-machines-dotnet-diagnostics/NewProject.png)
3. Sostituire il contenuto di hello del file Program.cs con hello seguente codice. classe Hello **SampleEventSourceWriter** implementa i quattro metodi di registrazione: **SendEnums**, **MessageMethod**, **SetOther** e  **HighFreq**. Hello primo parametro toohello metodo WriteEvent definisce hello ID evento rispettivi hello. metodo Run Hello implementa un ciclo infinito che ogni hello chiama i metodi di registrazione implementati in hello **SampleEventSourceWriter** classe ogni 10 secondi.

    ```csharp
     using System;
     using System.Diagnostics;
     using System.Diagnostics.Tracing;
     using System.Threading;

     namespace WadExampleVM
     {
       sealed class SampleEventSourceWriter : EventSource {
         public static SampleEventSourceWriter Log = new SampleEventSourceWriter();
         public void SendEnums(MyColor color, MyFlags flags) { if (IsEnabled())  WriteEvent(1, (int)color, (int)flags); } // Cast enums tooint for efficient logging.
         public void MessageMethod(string Message) { if (IsEnabled())  WriteEvent(2, Message); }
         public void SetOther(bool flag, int myInt) { if (IsEnabled())  WriteEvent(3, flag, myInt); }
         public void HighFreq(int value) { if (IsEnabled()) WriteEvent(4, value); }
       }

       enum MyColor {
         Red,
         Blue,
         Green
       }

       [Flags]
       enum MyFlags {
         Flag1 = 1,
         Flag2 = 2,
         Flag3 = 4
       }

       class Program
       {
         static void Main(string[] args) {
         Trace.TraceInformation("My application entry point called");

         int value = 0;

         while (true) {
             Thread.Sleep(10000);
             Trace.TraceInformation("Working");

             // Emit several events every time we go through hello loop
             for (int i = 0; i < 6; i++) {
                 SampleEventSourceWriter.Log.SendEnums(MyColor.Blue, MyFlags.Flag2 | MyFlags.Flag3);
             }

             for (int i = 0; i < 3; i++) {
                 SampleEventSourceWriter.Log.MessageMethod("This is a message.");
                 SampleEventSourceWriter.Log.SetOther(true, 123456789);
             }

             if (value == int.MaxValue) value = 0;
             SampleEventSourceWriter.Log.HighFreq(value++);
         }

        }
      }
     }
     ```
4. Salva file hello e selezionare **Compila soluzione** da hello **compilare** toobuild menu il codice.

### <a name="step-3-deploy-your-application"></a>Passaggio 3: Distribuire l'applicazione
1. Fare clic su hello **WadExampleVM** nel progetto **Esplora** e scegliere **Apri cartella in Esplora File**.
2. Passare toohello *bin\Debug* cartella e copia hello tutti i file (WadExampleVM.*)
3. In **Esplora Server** pulsante destro del mouse sulla macchina virtuale hello e scegliere **connessione tramite Desktop remoto**.
4. Una volta connessi toohello VM, creare una cartella denominata WadExampleVM e incollare i file dell'applicazione nella cartella hello.
5. Avvia un'applicazione hello WadExampleVM.exe. Verrà visualizzata una finestra della console vuota.

### <a name="step-4-create-your-diagnostics-configuration-and-install-hello-extension"></a>Passaggio 4: Creare la configurazione della diagnostica e installare l'estensione hello
1. Scaricare i computer di sviluppo di hello configurazione pubblica file schema definizione tooyour eseguendo hello comando PowerShell seguente:

     (Get-AzureServiceAvailableExtension -ExtensionName 'PaaSDiagnostics' -ProviderNamespace 'Microsoft.Azure.Diagnostics').PublicConfigurationSchema | Out-File -Encoding utf8 -FilePath 'WadConfig.xsd'
2. Aprire un nuovo file XML in Visual Studio, in un progetto già aperto o in un'istanza di Visual Studio senza progetti aperti In Visual Studio selezionare **Aggiungi** -> **Nuovo elemento...** -> **Elementi di Visual C#** -> **Dati** -> **File XML**. Nome file hello "WadExample.xml"
3. Associare il file di configurazione di hello hello WadConfig.xsd. Verificare che nella finestra dell'editor WadExample.xml hello è la finestra attiva di hello. Premere **F4** tooopen hello **proprietà** finestra. Fare clic su hello **schemi** proprietà hello **proprietà** finestra. Fare clic su hello **...** in hello **schemi** proprietà. Fare clic su hello **Aggiungi...** pulsante e passare toohello percorso in cui è stato salvato file XSD hello e selezionare hello WadConfig.xsd. Fare clic su **OK**.
4. Sostituire il contenuto di hello hello WadExample.xml del file di configurazione con hello XML seguente e salvare il file hello. Questo file di configurazione definisce un paio toocollect di contatori delle prestazioni: uno per l'utilizzo della CPU e uno per l'utilizzo della memoria. Configurazione di hello definisce quattro eventi hello corrispondente toohello metodi nella classe SampleEventSourceWriter hello.

```
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

### <a name="step-5-remotely-install-diagnostics-on-your-azure-virtual-machine"></a>Passaggio 5: Installare in remoto la diagnostica nella macchina virtuale di Azure
Hello cmdlet PowerShell per la gestione di diagnostica in una macchina virtuale sono: Set-AzureVMDiagnosticsExtension, Get-AzureVMDiagnosticsExtension e Remove-AzureVMDiagnosticsExtension.

1. Nel computer dello sviluppatore aprire Azure PowerShell.
2. Eseguire installazione di tooremotely script hello diagnostica nella macchina virtuale (sostituire `<user>` con il nome di directory utente. Sostituire `<StorageAccountKey>` con chiave dell'account di archiviazione per l'account di archiviazione wadexamplevm hello):
```
     $storage_name = "wadexamplevm"
     $key = "<StorageAccountKey>"
     $config_path="c:\users\<user>\documents\visual studio 2017\Projects\WadExampleVM\WadExampleVM\WadExample.xml"
     $service_name="wadexamplevm"
     $vm_name="WadExample"
     $storageContext = New-AzureStorageContext -StorageAccountName $storage_name -StorageAccountKey $key
     $VM1 = Get-AzureVM -ServiceName $service_name -Name $vm_name
     $VM2 = Set-AzureVMDiagnosticsExtension -DiagnosticsConfigurationPath $config_path -Version "1.*" -VM $VM1 -StorageContext $storageContext
     $VM3 = Update-AzureVM -ServiceName $service_name -Name $vm_name -VM $VM2.VM
```
### <a name="step-6-look-at-your-telemetry-data"></a>Passaggio 6: Esaminare i dati di telemetria
In Visual Studio hello **Esplora Server** passare toohello wadexample account di archiviazione. Dopo aver hello macchina virtuale è in esecuzione circa 5 minuti dovrebbe essere tabelle hello **WADEnumsTable**, **WADHighFreqTable**, **WADMessageTable**,  **WADPerformanceCountersTable** e **WADSetOtherTable**. Fare doppio clic su uno dei hello tabelle tooview hello dati di telemetria che sono stati raccolti.

![CloudServices_diag_wadexamplevm_tables](./media/virtual-machines-dotnet-diagnostics/WadExampleVMTables.png)

## <a name="configuration-file-schema"></a>Schema del file di configurazione
file di configurazione della diagnostica Hello definisce i valori vengono utilizzati tooinitialize le impostazioni di configurazione all'avvio dell'agente di diagnostica hello. Vedere hello [riferimento allo schema più recente](https://msdn.microsoft.com/library/azure/mt634524.aspx) per i valori validi ed esempi.

## <a name="troubleshooting"></a>Risoluzione dei problemi
Per altre informazioni, vedere [Risoluzione dei problemi di Diagnostica di Azure](../monitoring-and-diagnostics/azure-diagnostics-troubleshooting.md)

## <a name="next-steps"></a>Passaggi successivi
[Diagnostica di Azure articoli relativi a vedere un elenco di macchine virtuali](../monitoring-and-diagnostics/azure-diagnostics.md#virtual-machines-using-azure-diagnostics) dati hello toochange si raccolgono, risolvere i problemi o per altre informazioni sulla diagnostica in generale.

[EventSource Class]: http://msdn.microsoft.com/library/system.diagnostics.tracing.eventsource(v=vs.110).aspx

[Debugging an Azure Application]: http://msdn.microsoft.com/library/windowsazure/ee405479.aspx   
[Collect Logging Data by Using Azure Diagnostics]: http://msdn.microsoft.com/library/windowsazure/gg433048.aspx
[Free Trial]: http://azure.microsoft.com/pricing/free-trial/
[Install and configure Azure PowerShell version 0.8.7 or later]: http://azure.microsoft.com/documentation/articles/install-configure-powershell/

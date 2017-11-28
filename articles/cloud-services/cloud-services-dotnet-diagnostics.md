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
# <a name="enabling-azure-diagnostics-in-azure-cloud-services"></a><span data-ttu-id="8fa15-103">Abilitazione di Diagnostica di Azure in servizi cloud di Azure</span><span class="sxs-lookup"><span data-stu-id="8fa15-103">Enabling Azure Diagnostics in Azure Cloud Services</span></span>
<span data-ttu-id="8fa15-104">Vedere [Panoramica di Diagnostica di Azure](../azure-diagnostics.md) per un'introduzione a Diagnostica di Azure.</span><span class="sxs-lookup"><span data-stu-id="8fa15-104">See [Azure Diagnostics Overview](../azure-diagnostics.md) for a background on Azure Diagnostics.</span></span>

## <a name="how-tooenable-diagnostics-in-a-worker-role"></a><span data-ttu-id="8fa15-105">Come tooEnable diagnostica in un ruolo di lavoro</span><span class="sxs-lookup"><span data-stu-id="8fa15-105">How tooEnable Diagnostics in a Worker Role</span></span>
<span data-ttu-id="8fa15-106">Questa procedura dettagliata viene descritto come un ruolo di lavoro di Azure che genera dati di telemetria usando tooimplement hello classe EventSource .NET.</span><span class="sxs-lookup"><span data-stu-id="8fa15-106">This walkthrough describes how tooimplement an Azure worker role that emits telemetry data using hello .NET EventSource class.</span></span> <span data-ttu-id="8fa15-107">Diagnostica di Azure è toocollect utilizzati dati di telemetria hello e archiviarlo in un account di archiviazione di Azure.</span><span class="sxs-lookup"><span data-stu-id="8fa15-107">Azure Diagnostics is used toocollect hello telemetry data and store it in an Azure storage account.</span></span> <span data-ttu-id="8fa15-108">Quando si crea un ruolo di lavoro, Visual Studio consente automaticamente Diagnostics 1.0 come parte della soluzione hello in Azure SDK per .NET 2.4 e versioni precedenti.</span><span class="sxs-lookup"><span data-stu-id="8fa15-108">When creating a worker role, Visual Studio automatically enables Diagnostics 1.0 as part of hello solution in Azure SDKs for .NET 2.4 and earlier.</span></span> <span data-ttu-id="8fa15-109">Hello istruzioni seguenti descrivono il processo di hello per la creazione di ruolo di lavoro hello, disabilitazione Diagnostics 1.0 da soluzione hello e la distribuzione di diagnostica 1.2 o ruolo di lavoro tooyour 1.3.</span><span class="sxs-lookup"><span data-stu-id="8fa15-109">hello following instructions describe hello process for creating hello worker role, disabling Diagnostics 1.0 from hello solution, and deploying Diagnostics 1.2 or 1.3 tooyour worker role.</span></span>

### <a name="prerequisites"></a><span data-ttu-id="8fa15-110">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="8fa15-110">Prerequisites</span></span>
<span data-ttu-id="8fa15-111">In questo articolo si presuppone che si dispone di una sottoscrizione di Azure e si usa Visual Studio con hello Azure SDK.</span><span class="sxs-lookup"><span data-stu-id="8fa15-111">This article assumes you have an Azure subscription and are using Visual Studio with hello Azure SDK.</span></span> <span data-ttu-id="8fa15-112">Se non si dispone di una sottoscrizione di Azure, è possibile iscriversi per hello [versione di valutazione gratuita][Free Trial].</span><span class="sxs-lookup"><span data-stu-id="8fa15-112">If you do not have an Azure subscription, you can sign up for hello [Free Trial][Free Trial].</span></span> <span data-ttu-id="8fa15-113">Assicurarsi che troppo[installare e configurare Azure PowerShell 0.8.7 o versione successiva][Install and configure Azure PowerShell version 0.8.7 or later].</span><span class="sxs-lookup"><span data-stu-id="8fa15-113">Make sure too[Install and configure Azure PowerShell version 0.8.7 or later][Install and configure Azure PowerShell version 0.8.7 or later].</span></span>

### <a name="step-1-create-a-worker-role"></a><span data-ttu-id="8fa15-114">Passaggio 1: Creare un ruolo di lavoro</span><span class="sxs-lookup"><span data-stu-id="8fa15-114">Step 1: Create a Worker Role</span></span>
1. <span data-ttu-id="8fa15-115">Avviare **Visual Studio**.</span><span class="sxs-lookup"><span data-stu-id="8fa15-115">Launch **Visual Studio**.</span></span>
2. <span data-ttu-id="8fa15-116">Creare un **servizio Cloud di Azure** progetto da hello **Cloud** modello destinato a .NET Framework 4.5.</span><span class="sxs-lookup"><span data-stu-id="8fa15-116">Create an **Azure Cloud Service** project from hello **Cloud** template that targets .NET Framework 4.5.</span></span>  <span data-ttu-id="8fa15-117">Nome progetto hello "WadExample" e fare clic su Ok.</span><span class="sxs-lookup"><span data-stu-id="8fa15-117">Name hello project "WadExample" and click Ok.</span></span>
3. <span data-ttu-id="8fa15-118">Selezionare **Ruolo di lavoro** e fare clic su OK.</span><span class="sxs-lookup"><span data-stu-id="8fa15-118">Select **Worker Role** and click Ok.</span></span> <span data-ttu-id="8fa15-119">verrà creato il progetto Hello.</span><span class="sxs-lookup"><span data-stu-id="8fa15-119">hello project will be created.</span></span>
4. <span data-ttu-id="8fa15-120">In **Esplora**, fare doppio clic su hello **WorkerRole1** file delle proprietà.</span><span class="sxs-lookup"><span data-stu-id="8fa15-120">In **Solution Explorer**, double-click hello **WorkerRole1** properties file.</span></span>
5. <span data-ttu-id="8fa15-121">In hello **configurazione** scheda deselezionare **Abilita diagnostica** toodisable Diagnostics 1.0 (Azure SDK 2.4 e versioni precedenti).</span><span class="sxs-lookup"><span data-stu-id="8fa15-121">In hello **Configuration** tab, un-check **Enable Diagnostics** toodisable Diagnostics 1.0 (Azure SDK 2.4 and earlier).</span></span>
6. <span data-ttu-id="8fa15-122">Compilare la soluzione tooverify che non siano presenti errori.</span><span class="sxs-lookup"><span data-stu-id="8fa15-122">Build your solution tooverify that you have no errors.</span></span>

### <a name="step-2-instrument-your-code"></a><span data-ttu-id="8fa15-123">Passaggio 2: Instrumentare il codice</span><span class="sxs-lookup"><span data-stu-id="8fa15-123">Step 2: Instrument your code</span></span>
<span data-ttu-id="8fa15-124">Sostituire il contenuto di hello del WorkerRole.cs con hello seguente codice.</span><span class="sxs-lookup"><span data-stu-id="8fa15-124">Replace hello contents of WorkerRole.cs with hello following code.</span></span> <span data-ttu-id="8fa15-125">classe SampleEventSourceWriter, ereditato da hello Hello [classe EventSource][EventSource Class], implementa i quattro metodi di registrazione: **SendEnums**, **MessageMethod** , **SetOther** e **HighFreq**.</span><span class="sxs-lookup"><span data-stu-id="8fa15-125">hello class SampleEventSourceWriter, inherited from hello [EventSource Class][EventSource Class], implements four logging methods: **SendEnums**, **MessageMethod**, **SetOther** and **HighFreq**.</span></span> <span data-ttu-id="8fa15-126">primo parametro toohello Hello **WriteEvent** metodo definisce hello ID evento rispettivi hello.</span><span class="sxs-lookup"><span data-stu-id="8fa15-126">hello first parameter toohello **WriteEvent** method defines hello ID for hello respective event.</span></span> <span data-ttu-id="8fa15-127">metodo Run Hello implementa un ciclo infinito che ogni hello chiama i metodi di registrazione implementati in hello **SampleEventSourceWriter** classe ogni 10 secondi.</span><span class="sxs-lookup"><span data-stu-id="8fa15-127">hello Run method implements an infinite loop that calls each of hello logging methods implemented in hello **SampleEventSourceWriter** class every 10 seconds.</span></span>

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


### <a name="step-3-deploy-your-worker-role"></a><span data-ttu-id="8fa15-128">Passaggio 3: Distribuire il ruolo di lavoro</span><span class="sxs-lookup"><span data-stu-id="8fa15-128">Step 3: Deploy your Worker Role</span></span>

[!INCLUDE [cloud-services-wad-warning](../../includes/cloud-services-wad-warning.md)]

1. <span data-ttu-id="8fa15-129">Distribuire il tooAzure ruolo worker da Visual Studio selezionando hello **WadExample** progetto in hello quindi Esplora **pubblica** da hello **compilare** menu.</span><span class="sxs-lookup"><span data-stu-id="8fa15-129">Deploy your worker role tooAzure from within Visual Studio by selecting hello **WadExample** project in hello Solution Explorer then **Publish** from hello **Build** menu.</span></span>
2. <span data-ttu-id="8fa15-130">Scegliere la propria sottoscrizione.</span><span class="sxs-lookup"><span data-stu-id="8fa15-130">Choose your subscription.</span></span>
3. <span data-ttu-id="8fa15-131">In hello **impostazioni di pubblicazione di Microsoft Azure** finestra di dialogo Seleziona **Crea nuovo...** .</span><span class="sxs-lookup"><span data-stu-id="8fa15-131">In hello **Microsoft Azure Publish Settings** dialog, select **Create New…**.</span></span>
4. <span data-ttu-id="8fa15-132">In hello **Crea servizio Cloud e Account di archiviazione** finestra di dialogo immettere un **nome** (ad esempio, "WadExample") e selezionare un'area o un gruppo di affinità.</span><span class="sxs-lookup"><span data-stu-id="8fa15-132">In hello **Create Cloud Service and Storage Account** dialog, enter a **Name** (for example, "WadExample") and select a region or affinity group.</span></span>
5. <span data-ttu-id="8fa15-133">Set hello **ambiente** troppo**gestione temporanea**.</span><span class="sxs-lookup"><span data-stu-id="8fa15-133">Set hello **Environment** too**Staging**.</span></span>
6. <span data-ttu-id="8fa15-134">Modificare le altre **impostazioni** nel modo appropriato e fare clic su **Pubblica**.</span><span class="sxs-lookup"><span data-stu-id="8fa15-134">Modify any other **Settings** as appropriate and click **Publish**.</span></span>
7. <span data-ttu-id="8fa15-135">Una volta completata la distribuzione, verificare nel portale di Azure che il servizio cloud hello un **esecuzione** stato.</span><span class="sxs-lookup"><span data-stu-id="8fa15-135">After deployment has completed, verify in hello Azure portal that your cloud service is in a **Running** state.</span></span>

### <a name="step-4-create-your-diagnostics-configuration-file-and-install-hello-extension"></a><span data-ttu-id="8fa15-136">Passaggio 4: Creare il file di configurazione di diagnostica e installare l'estensione hello</span><span class="sxs-lookup"><span data-stu-id="8fa15-136">Step 4: Create your Diagnostics configuration file and install hello extension</span></span>
1. <span data-ttu-id="8fa15-137">Scarica definizione dello schema file di configurazione pubblica hello eseguendo hello comando PowerShell seguente:</span><span class="sxs-lookup"><span data-stu-id="8fa15-137">Download hello public configuration file schema definition by executing hello following PowerShell command:</span></span>

    ```powershell
    (Get-AzureServiceAvailableExtension -ExtensionName 'PaaSDiagnostics' -ProviderNamespace 'Microsoft.Azure.Diagnostics').PublicConfigurationSchema | Out-File -Encoding utf8 -FilePath 'WadConfig.xsd'
    ```
2. <span data-ttu-id="8fa15-138">Aggiungere un tooyour file XML **WorkerRole1** progetto facendo clic su hello **WorkerRole1** del progetto e selezionare **Aggiungi** -> **nuovo elemento...**</span><span class="sxs-lookup"><span data-stu-id="8fa15-138">Add an XML file tooyour **WorkerRole1** project by right-clicking on hello **WorkerRole1** project and select **Add** -> **New Item…**</span></span><span data-ttu-id="8fa15-139"> -> **Elementi di Visual C#** -> **Dati** -> **File XML**.</span><span class="sxs-lookup"><span data-stu-id="8fa15-139"> -> **Visual C# items** -> **Data** -> **XML File**.</span></span> <span data-ttu-id="8fa15-140">Il nome file hello "WadExample.xml".</span><span class="sxs-lookup"><span data-stu-id="8fa15-140">Name hello file "WadExample.xml".</span></span>

   ![CloudServices_diag_add_xml](./media/cloud-services-dotnet-diagnostics/AddXmlFile.png)
3. <span data-ttu-id="8fa15-142">Associare il file di configurazione di hello hello WadConfig.xsd.</span><span class="sxs-lookup"><span data-stu-id="8fa15-142">Associate hello WadConfig.xsd with hello configuration file.</span></span> <span data-ttu-id="8fa15-143">Verificare che nella finestra dell'editor WadExample.xml hello è la finestra attiva di hello.</span><span class="sxs-lookup"><span data-stu-id="8fa15-143">Make sure hello WadExample.xml editor window is hello active window.</span></span> <span data-ttu-id="8fa15-144">Premere **F4** tooopen hello **proprietà** finestra.</span><span class="sxs-lookup"><span data-stu-id="8fa15-144">Press **F4** tooopen hello **Properties** window.</span></span> <span data-ttu-id="8fa15-145">Fare clic su hello **schemi** proprietà hello **proprietà** finestra.</span><span class="sxs-lookup"><span data-stu-id="8fa15-145">Click hello **Schemas** property in hello **Properties** window.</span></span> <span data-ttu-id="8fa15-146">Fare clic su hello **...**</span><span class="sxs-lookup"><span data-stu-id="8fa15-146">Click hello **…**</span></span> <span data-ttu-id="8fa15-147">in hello **schemi** proprietà.</span><span class="sxs-lookup"><span data-stu-id="8fa15-147">in hello **Schemas** property.</span></span> <span data-ttu-id="8fa15-148">Fare clic su hello **Aggiungi...**</span><span class="sxs-lookup"><span data-stu-id="8fa15-148">Click hello **Add…**</span></span> <span data-ttu-id="8fa15-149">pulsante e passare toohello percorso in cui è stato salvato file XSD hello e selezionare hello WadConfig.xsd.</span><span class="sxs-lookup"><span data-stu-id="8fa15-149">button and navigate toohello location where you saved hello XSD file and select hello file WadConfig.xsd.</span></span> <span data-ttu-id="8fa15-150">Fare clic su **OK**.</span><span class="sxs-lookup"><span data-stu-id="8fa15-150">Click **OK**.</span></span>

4. <span data-ttu-id="8fa15-151">Sostituire il contenuto di hello hello WadExample.xml del file di configurazione con hello XML seguente e salvare il file hello.</span><span class="sxs-lookup"><span data-stu-id="8fa15-151">Replace hello contents of hello WadExample.xml configuration file with hello following XML and save hello file.</span></span> <span data-ttu-id="8fa15-152">Questo file di configurazione definisce un paio toocollect di contatori delle prestazioni: uno per l'utilizzo della CPU e uno per l'utilizzo della memoria.</span><span class="sxs-lookup"><span data-stu-id="8fa15-152">This configuration file defines a couple performance counters toocollect: one for CPU utilization and one for memory utilization.</span></span> <span data-ttu-id="8fa15-153">Configurazione di hello definisce quattro eventi hello corrispondente toohello metodi nella classe SampleEventSourceWriter hello.</span><span class="sxs-lookup"><span data-stu-id="8fa15-153">Then hello configuration defines hello four events corresponding toohello methods in hello SampleEventSourceWriter class.</span></span>

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

### <a name="step-5-install-diagnostics-on-your-worker-role"></a><span data-ttu-id="8fa15-154">Passaggio 5: Installare la diagnostica nel ruolo di lavoro</span><span class="sxs-lookup"><span data-stu-id="8fa15-154">Step 5: Install Diagnostics on your Worker Role</span></span>
<span data-ttu-id="8fa15-155">Hello cmdlet PowerShell per la gestione di diagnostica in un ruolo web o di lavoro sono: Set-AzureServiceDiagnosticsExtension, Get-AzureServiceDiagnosticsExtension e Remove-AzureServiceDiagnosticsExtension.</span><span class="sxs-lookup"><span data-stu-id="8fa15-155">hello PowerShell cmdlets for managing Diagnostics on a web or worker role are: Set-AzureServiceDiagnosticsExtension, Get-AzureServiceDiagnosticsExtension, and Remove-AzureServiceDiagnosticsExtension.</span></span>

1. <span data-ttu-id="8fa15-156">Aprire Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="8fa15-156">Open Azure PowerShell.</span></span>
2. <span data-ttu-id="8fa15-157">Eseguire tooinstall script hello diagnostica nel ruolo di lavoro (sostituire *StorageAccountKey* con chiave dell'account di archiviazione per l'account di archiviazione wadexample hello e *config_path* con percorso hello toohello *WadExample.xml* file):</span><span class="sxs-lookup"><span data-stu-id="8fa15-157">Execute hello script tooinstall Diagnostics on your worker role (replace *StorageAccountKey* with hello storage account key for your wadexample storage account and *config_path* with hello path toohello *WadExample.xml* file):</span></span>

```powershell
$storage_name = "wadexample"
$key = "<StorageAccountKey>"
$config_path="c:\users\<user>\documents\visual studio 2013\Projects\WadExample\WorkerRole1\WadExample.xml"
$service_name="wadexample"
$storageContext = New-AzureStorageContext -StorageAccountName $storage_name -StorageAccountKey $key
Set-AzureServiceDiagnosticsExtension -StorageContext $storageContext -DiagnosticsConfigurationPath $config_path -ServiceName $service_name -Slot Staging -Role WorkerRole1
```

### <a name="step-6-look-at-your-telemetry-data"></a><span data-ttu-id="8fa15-158">Passaggio 6: Esaminare i dati di telemetria</span><span class="sxs-lookup"><span data-stu-id="8fa15-158">Step 6: Look at your telemetry data</span></span>
<span data-ttu-id="8fa15-159">In Visual Studio hello **Esplora Server**, passare toohello wadexample account di archiviazione.</span><span class="sxs-lookup"><span data-stu-id="8fa15-159">In hello Visual Studio **Server Explorer**, navigate toohello wadexample storage account.</span></span> <span data-ttu-id="8fa15-160">Dopo circa cinque (5) minuti è stato in esecuzione il servizio di cloud hello, dovrebbe essere tabelle hello **WADEnumsTable**, **WADHighFreqTable**, **WADMessageTable**, **WADPerformanceCountersTable** e **WADSetOtherTable**.</span><span class="sxs-lookup"><span data-stu-id="8fa15-160">After hello cloud service has been running about five (5) minutes, you should see hello tables **WADEnumsTable**, **WADHighFreqTable**, **WADMessageTable**, **WADPerformanceCountersTable** and **WADSetOtherTable**.</span></span> <span data-ttu-id="8fa15-161">Fare doppio clic su uno dei hello tabelle tooview hello dati di telemetria che sono stati raccolti.</span><span class="sxs-lookup"><span data-stu-id="8fa15-161">Double-click one of hello tables tooview hello telemetry that has been collected.</span></span>

![CloudServices_diag_tables](./media/cloud-services-dotnet-diagnostics/WadExampleTables.png)

## <a name="configuration-file-schema"></a><span data-ttu-id="8fa15-163">Schema del file di configurazione</span><span class="sxs-lookup"><span data-stu-id="8fa15-163">Configuration File Schema</span></span>
<span data-ttu-id="8fa15-164">file di configurazione della diagnostica Hello definisce i valori vengono utilizzati tooinitialize le impostazioni di configurazione all'avvio dell'agente di diagnostica hello.</span><span class="sxs-lookup"><span data-stu-id="8fa15-164">hello Diagnostics configuration file defines values that are used tooinitialize diagnostic configuration settings when hello diagnostics agent starts.</span></span> <span data-ttu-id="8fa15-165">Vedere hello [riferimento allo schema più recente](https://msdn.microsoft.com/library/azure/mt634524.aspx) per i valori validi ed esempi.</span><span class="sxs-lookup"><span data-stu-id="8fa15-165">See hello [latest schema reference](https://msdn.microsoft.com/library/azure/mt634524.aspx) for valid values and examples.</span></span>

## <a name="troubleshooting"></a><span data-ttu-id="8fa15-166">Risoluzione dei problemi</span><span class="sxs-lookup"><span data-stu-id="8fa15-166">Troubleshooting</span></span>
<span data-ttu-id="8fa15-167">Se si verificano problemi, vedere l'argomento relativo alla [risoluzione dei problemi di Diagnostica di Azure](../azure-diagnostics-troubleshooting.md) per informazioni sui problemi comuni.</span><span class="sxs-lookup"><span data-stu-id="8fa15-167">If you have trouble, see [Troubleshooting Azure Diagnostics](../azure-diagnostics-troubleshooting.md) for help with common problems.</span></span>

## <a name="next-steps"></a><span data-ttu-id="8fa15-168">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="8fa15-168">Next Steps</span></span>
<span data-ttu-id="8fa15-169">[Visualizzare un elenco di Azure macchina virtuale diagnostica articoli correlati](../monitoring-and-diagnostics/azure-diagnostics.md#cloud-services-using-azure-diagnostics) dati hello toochange si raccolgono, risolvere i problemi o per altre informazioni sulla diagnostica in generale.</span><span class="sxs-lookup"><span data-stu-id="8fa15-169">[See a list of related Azure virtual-machine diagnostic articles](../monitoring-and-diagnostics/azure-diagnostics.md#cloud-services-using-azure-diagnostics) toochange hello data you are collecting, troubleshoot problems or learn more about diagnostics in general.</span></span>

[EventSource Class]: http://msdn.microsoft.com/library/system.diagnostics.tracing.eventsource(v=vs.110).aspx

[Debugging an Azure Application]: http://msdn.microsoft.com/library/windowsazure/ee405479.aspx   
[Collect Logging Data by Using Azure Diagnostics]: http://msdn.microsoft.com/library/windowsazure/gg433048.aspx
[Free Trial]: http://azure.microsoft.com/pricing/free-trial/
[Install and configure Azure PowerShell version 0.8.7 or later]: http://azure.microsoft.com/documentation/articles/install-configure-powershell/

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
# <a name="enabling-diagnostics-in-azure-virtual-machines"></a><span data-ttu-id="55a50-103">Abilitare la diagnostica nelle macchine virtuali di Azure</span><span class="sxs-lookup"><span data-stu-id="55a50-103">Enabling Diagnostics in Azure Virtual Machines</span></span>
<span data-ttu-id="55a50-104">Vedere [Panoramica di Diagnostica di Azure](../monitoring-and-diagnostics/azure-diagnostics.md) per un'introduzione a Diagnostica di Azure.</span><span class="sxs-lookup"><span data-stu-id="55a50-104">See [Azure Diagnostics Overview](../monitoring-and-diagnostics/azure-diagnostics.md) for a background on Azure Diagnostics.</span></span>

## <a name="how-tooenable-diagnostics-in-a-virtual-machine"></a><span data-ttu-id="55a50-105">Come tooEnable diagnostica in una macchina virtuale</span><span class="sxs-lookup"><span data-stu-id="55a50-105">How tooEnable Diagnostics in a Virtual Machine</span></span>
<span data-ttu-id="55a50-106">Questa procedura dettagliata viene descritto come installare diagnostica tooan macchina virtuale di Azure di tooremotely da un computer di sviluppo.</span><span class="sxs-lookup"><span data-stu-id="55a50-106">This walk through describes how tooremotely install Diagnostics tooan Azure virtual machine from a development computer.</span></span> <span data-ttu-id="55a50-107">Verrà inoltre descritto come un'applicazione in esecuzione su tale macchina virtuale di Azure e genera dati di telemetria usando tooimplement hello .NET [classe EventSource][EventSource Class].</span><span class="sxs-lookup"><span data-stu-id="55a50-107">You also learn how tooimplement an application that runs on that Azure virtual machine and emits telemetry data using hello .NET [EventSource Class][EventSource Class].</span></span> <span data-ttu-id="55a50-108">Diagnostica di Azure è dati di telemetria hello toocollect utilizzato e archiviarlo in un account di archiviazione di Azure.</span><span class="sxs-lookup"><span data-stu-id="55a50-108">Azure Diagnostics is used toocollect hello telemetry and store it in an Azure storage account.</span></span>

### <a name="pre-requisites"></a><span data-ttu-id="55a50-109">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="55a50-109">Pre-requisites</span></span>
<span data-ttu-id="55a50-110">Questa procedura dettagliata si presuppone che si dispone di una sottoscrizione di Azure e si sta utilizzando Visual Studio 2017 con hello Azure SDK.</span><span class="sxs-lookup"><span data-stu-id="55a50-110">This walk through assumes you have an Azure subscription and are using Visual Studio 2017 with hello Azure SDK.</span></span> <span data-ttu-id="55a50-111">Se non si dispone di una sottoscrizione di Azure, è possibile iscriversi per hello [versione di valutazione gratuita][Free Trial].</span><span class="sxs-lookup"><span data-stu-id="55a50-111">If you do not have an Azure subscription, you can sign up for hello [Free Trial][Free Trial].</span></span> <span data-ttu-id="55a50-112">Assicurarsi che troppo[installare e configurare Azure PowerShell 0.8.7 o versione successiva][Install and configure Azure PowerShell version 0.8.7 or later].</span><span class="sxs-lookup"><span data-stu-id="55a50-112">Make sure too[Install and configure Azure PowerShell version 0.8.7 or later][Install and configure Azure PowerShell version 0.8.7 or later].</span></span>

### <a name="step-1-create-a-virtual-machine"></a><span data-ttu-id="55a50-113">Passaggio 1: Creare una macchina virtuale</span><span class="sxs-lookup"><span data-stu-id="55a50-113">Step 1: Create a Virtual Machine</span></span>
1. <span data-ttu-id="55a50-114">Nel computer di sviluppo, avviare Visual Studio 2017.</span><span class="sxs-lookup"><span data-stu-id="55a50-114">On your development computer, launch Visual Studio 2017.</span></span>
2. <span data-ttu-id="55a50-115">In Visual Studio hello **Esplora Server** espandere **Azure**, fare doppio clic su **macchine virtuali** selezionare **crea macchina virtuale**.</span><span class="sxs-lookup"><span data-stu-id="55a50-115">In hello Visual Studio **Server Explorer** expand **Azure**, right-click **Virtual Machines** then select **Create Virtual Machine**.</span></span>
3. <span data-ttu-id="55a50-116">Selezionare la sottoscrizione di Azure in hello **scegliere una sottoscrizione** finestra di dialogo e fare clic su **Avanti**.</span><span class="sxs-lookup"><span data-stu-id="55a50-116">Select your Azure subscription in hello **Choose a Subscription** dialog and click **Next**.</span></span>
4. <span data-ttu-id="55a50-117">Selezionare **giugno 2017, Windows Server 2012 R2 Datacenter** in hello **selezionare un'immagine di macchina virtuale** finestra di dialogo e fare clic su **Avanti**.</span><span class="sxs-lookup"><span data-stu-id="55a50-117">Select **Windows Server 2012 R2 Datacenter, June 2017** in hello **Select a Virtual Machine Image** dialog and click **Next**.</span></span>
5. <span data-ttu-id="55a50-118">In hello **le impostazioni di base di macchina virtuale**, impostare il nome di macchina virtuale hello troppo "wadexample".</span><span class="sxs-lookup"><span data-stu-id="55a50-118">In hello **Virtual Machine Basic Settings**, set hello virtual machine name too"wadexample".</span></span> <span data-ttu-id="55a50-119">Impostare il nome utente e la password dell'amministratore e fare clic su **Avanti**.</span><span class="sxs-lookup"><span data-stu-id="55a50-119">Set your Administrator user name and password and click **Next**.</span></span>
6. <span data-ttu-id="55a50-120">In hello **le impostazioni del servizio Cloud** finestra di dialogo Crea un nuovo servizio cloud denominato "wadexampleVM".</span><span class="sxs-lookup"><span data-stu-id="55a50-120">In hello **Cloud Service Settings** dialog create a new cloud service named "wadexampleVM".</span></span> <span data-ttu-id="55a50-121">Creare un nuovo account di archiviazione denominato "wadexample" e fare clic su **Avanti**.</span><span class="sxs-lookup"><span data-stu-id="55a50-121">Create a new Storage account named "wadexample" and click **Next**.</span></span>
7. <span data-ttu-id="55a50-122">Fare clic su **Create**.</span><span class="sxs-lookup"><span data-stu-id="55a50-122">Click **Create**.</span></span>

### <a name="step-2-create-your-application"></a><span data-ttu-id="55a50-123">Passaggio 2: Creare l'applicazione</span><span class="sxs-lookup"><span data-stu-id="55a50-123">Step 2: Create your Application</span></span>
1. <span data-ttu-id="55a50-124">Nel computer di sviluppo, avviare Visual Studio 2017.</span><span class="sxs-lookup"><span data-stu-id="55a50-124">On your development computer, launch Visual Studio 2017.</span></span>
2. <span data-ttu-id="55a50-125">Creare una nuova applicazione console Visual C# per .NET Framework 4.5.</span><span class="sxs-lookup"><span data-stu-id="55a50-125">Create a new Visual C# Console Application that targets .NET Framework 4.5.</span></span> <span data-ttu-id="55a50-126">Nome progetto hello "WadExampleVM".</span><span class="sxs-lookup"><span data-stu-id="55a50-126">Name hello project "WadExampleVM".</span></span>

   ![CloudServices_diag_new_project](./media/virtual-machines-dotnet-diagnostics/NewProject.png)
3. <span data-ttu-id="55a50-128">Sostituire il contenuto di hello del file Program.cs con hello seguente codice.</span><span class="sxs-lookup"><span data-stu-id="55a50-128">Replace hello contents of Program.cs with hello following code.</span></span> <span data-ttu-id="55a50-129">classe Hello **SampleEventSourceWriter** implementa i quattro metodi di registrazione: **SendEnums**, **MessageMethod**, **SetOther** e  **HighFreq**.</span><span class="sxs-lookup"><span data-stu-id="55a50-129">hello class **SampleEventSourceWriter** implements four logging methods: **SendEnums**, **MessageMethod**, **SetOther** and **HighFreq**.</span></span> <span data-ttu-id="55a50-130">Hello primo parametro toohello metodo WriteEvent definisce hello ID evento rispettivi hello.</span><span class="sxs-lookup"><span data-stu-id="55a50-130">hello first parameter toohello WriteEvent method defines hello ID for hello respective event.</span></span> <span data-ttu-id="55a50-131">metodo Run Hello implementa un ciclo infinito che ogni hello chiama i metodi di registrazione implementati in hello **SampleEventSourceWriter** classe ogni 10 secondi.</span><span class="sxs-lookup"><span data-stu-id="55a50-131">hello Run method implements an infinite loop that calls each of hello logging methods implemented in hello **SampleEventSourceWriter** class every 10 seconds.</span></span>

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
4. <span data-ttu-id="55a50-132">Salva file hello e selezionare **Compila soluzione** da hello **compilare** toobuild menu il codice.</span><span class="sxs-lookup"><span data-stu-id="55a50-132">Save hello file and select **Build Solution** from hello **Build** menu toobuild your code.</span></span>

### <a name="step-3-deploy-your-application"></a><span data-ttu-id="55a50-133">Passaggio 3: Distribuire l'applicazione</span><span class="sxs-lookup"><span data-stu-id="55a50-133">Step 3: Deploy your Application</span></span>
1. <span data-ttu-id="55a50-134">Fare clic su hello **WadExampleVM** nel progetto **Esplora** e scegliere **Apri cartella in Esplora File**.</span><span class="sxs-lookup"><span data-stu-id="55a50-134">Right-click on hello **WadExampleVM** project in **Solution Explorer** and choose **Open Folder in File Explorer**.</span></span>
2. <span data-ttu-id="55a50-135">Passare toohello *bin\Debug* cartella e copia hello tutti i file (WadExampleVM.*)</span><span class="sxs-lookup"><span data-stu-id="55a50-135">Navigate toohello *bin\Debug* folder and copy all hello files (WadExampleVM.*)</span></span>
3. <span data-ttu-id="55a50-136">In **Esplora Server** pulsante destro del mouse sulla macchina virtuale hello e scegliere **connessione tramite Desktop remoto**.</span><span class="sxs-lookup"><span data-stu-id="55a50-136">In **Server Explorer** right-click on hello virtual machine and choose **Connect using Remote Desktop**.</span></span>
4. <span data-ttu-id="55a50-137">Una volta connessi toohello VM, creare una cartella denominata WadExampleVM e incollare i file dell'applicazione nella cartella hello.</span><span class="sxs-lookup"><span data-stu-id="55a50-137">Once connected toohello VM create a folder named WadExampleVM and paste your application files into hello folder.</span></span>
5. <span data-ttu-id="55a50-138">Avvia un'applicazione hello WadExampleVM.exe.</span><span class="sxs-lookup"><span data-stu-id="55a50-138">Launch hello application WadExampleVM.exe.</span></span> <span data-ttu-id="55a50-139">Verrà visualizzata una finestra della console vuota.</span><span class="sxs-lookup"><span data-stu-id="55a50-139">You should see a blank console window.</span></span>

### <a name="step-4-create-your-diagnostics-configuration-and-install-hello-extension"></a><span data-ttu-id="55a50-140">Passaggio 4: Creare la configurazione della diagnostica e installare l'estensione hello</span><span class="sxs-lookup"><span data-stu-id="55a50-140">Step 4: Create your Diagnostics configuration and install hello Extension</span></span>
1. <span data-ttu-id="55a50-141">Scaricare i computer di sviluppo di hello configurazione pubblica file schema definizione tooyour eseguendo hello comando PowerShell seguente:</span><span class="sxs-lookup"><span data-stu-id="55a50-141">Download hello public configuration file schema definition tooyour development computer by executing hello following PowerShell command:</span></span>

     <span data-ttu-id="55a50-142">(Get-AzureServiceAvailableExtension -ExtensionName 'PaaSDiagnostics' -ProviderNamespace 'Microsoft.Azure.Diagnostics').PublicConfigurationSchema | Out-File -Encoding utf8 -FilePath 'WadConfig.xsd'</span><span class="sxs-lookup"><span data-stu-id="55a50-142">(Get-AzureServiceAvailableExtension -ExtensionName 'PaaSDiagnostics' -ProviderNamespace 'Microsoft.Azure.Diagnostics').PublicConfigurationSchema | Out-File -Encoding utf8 -FilePath 'WadConfig.xsd'</span></span>
2. <span data-ttu-id="55a50-143">Aprire un nuovo file XML in Visual Studio, in un progetto già aperto o in un'istanza di Visual Studio senza progetti aperti</span><span class="sxs-lookup"><span data-stu-id="55a50-143">Open a new XML file in Visual Studio, either in a project you already have open or in a Visual Studio instance with no open projects.</span></span> <span data-ttu-id="55a50-144">In Visual Studio selezionare **Aggiungi** -> **Nuovo elemento...**</span><span class="sxs-lookup"><span data-stu-id="55a50-144">In Visual Studio, select **Add** -> **New Item…**</span></span><span data-ttu-id="55a50-145"> -> **Elementi di Visual C#** -> **Dati** -> **File XML**.</span><span class="sxs-lookup"><span data-stu-id="55a50-145"> -> **Visual C# items** -> **Data** -> **XML File**.</span></span> <span data-ttu-id="55a50-146">Nome file hello "WadExample.xml"</span><span class="sxs-lookup"><span data-stu-id="55a50-146">Name hello file "WadExample.xml"</span></span>
3. <span data-ttu-id="55a50-147">Associare il file di configurazione di hello hello WadConfig.xsd.</span><span class="sxs-lookup"><span data-stu-id="55a50-147">Associate hello WadConfig.xsd with hello configuration file.</span></span> <span data-ttu-id="55a50-148">Verificare che nella finestra dell'editor WadExample.xml hello è la finestra attiva di hello.</span><span class="sxs-lookup"><span data-stu-id="55a50-148">Make sure hello WadExample.xml editor window is hello active window.</span></span> <span data-ttu-id="55a50-149">Premere **F4** tooopen hello **proprietà** finestra.</span><span class="sxs-lookup"><span data-stu-id="55a50-149">Press **F4** tooopen hello **Properties** window.</span></span> <span data-ttu-id="55a50-150">Fare clic su hello **schemi** proprietà hello **proprietà** finestra.</span><span class="sxs-lookup"><span data-stu-id="55a50-150">Click on hello **Schemas** property in hello **Properties** window.</span></span> <span data-ttu-id="55a50-151">Fare clic su hello **...**</span><span class="sxs-lookup"><span data-stu-id="55a50-151">Click hello **…**</span></span> <span data-ttu-id="55a50-152">in hello **schemi** proprietà.</span><span class="sxs-lookup"><span data-stu-id="55a50-152">in hello **Schemas** property.</span></span> <span data-ttu-id="55a50-153">Fare clic su hello **Aggiungi...**</span><span class="sxs-lookup"><span data-stu-id="55a50-153">Click hello **Add…**</span></span> <span data-ttu-id="55a50-154">pulsante e passare toohello percorso in cui è stato salvato file XSD hello e selezionare hello WadConfig.xsd.</span><span class="sxs-lookup"><span data-stu-id="55a50-154">button and navigate toohello location where you saved hello XSD file and select hello file WadConfig.xsd.</span></span> <span data-ttu-id="55a50-155">Fare clic su **OK**.</span><span class="sxs-lookup"><span data-stu-id="55a50-155">Click **OK**.</span></span>
4. <span data-ttu-id="55a50-156">Sostituire il contenuto di hello hello WadExample.xml del file di configurazione con hello XML seguente e salvare il file hello.</span><span class="sxs-lookup"><span data-stu-id="55a50-156">Replace hello contents of hello WadExample.xml configuration file with hello following XML and save hello file.</span></span> <span data-ttu-id="55a50-157">Questo file di configurazione definisce un paio toocollect di contatori delle prestazioni: uno per l'utilizzo della CPU e uno per l'utilizzo della memoria.</span><span class="sxs-lookup"><span data-stu-id="55a50-157">This configuration file defines a couple performance counters toocollect: one for CPU utilization and one for memory utilization.</span></span> <span data-ttu-id="55a50-158">Configurazione di hello definisce quattro eventi hello corrispondente toohello metodi nella classe SampleEventSourceWriter hello.</span><span class="sxs-lookup"><span data-stu-id="55a50-158">Then hello configuration defines hello four events corresponding toohello methods in hello SampleEventSourceWriter class.</span></span>

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

### <a name="step-5-remotely-install-diagnostics-on-your-azure-virtual-machine"></a><span data-ttu-id="55a50-159">Passaggio 5: Installare in remoto la diagnostica nella macchina virtuale di Azure</span><span class="sxs-lookup"><span data-stu-id="55a50-159">Step 5: Remotely install Diagnostics on your Azure Virtual Machine</span></span>
<span data-ttu-id="55a50-160">Hello cmdlet PowerShell per la gestione di diagnostica in una macchina virtuale sono: Set-AzureVMDiagnosticsExtension, Get-AzureVMDiagnosticsExtension e Remove-AzureVMDiagnosticsExtension.</span><span class="sxs-lookup"><span data-stu-id="55a50-160">hello PowerShell cmdlets for managing Diagnostics on a VM are: Set-AzureVMDiagnosticsExtension, Get-AzureVMDiagnosticsExtension, and Remove-AzureVMDiagnosticsExtension.</span></span>

1. <span data-ttu-id="55a50-161">Nel computer dello sviluppatore aprire Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="55a50-161">On your developer computer, open Azure PowerShell.</span></span>
2. <span data-ttu-id="55a50-162">Eseguire installazione di tooremotely script hello diagnostica nella macchina virtuale (sostituire `<user>` con il nome di directory utente.</span><span class="sxs-lookup"><span data-stu-id="55a50-162">Execute hello script tooremotely install Diagnostics on your VM (Replace `<user>` with your user directory name.</span></span> <span data-ttu-id="55a50-163">Sostituire `<StorageAccountKey>` con chiave dell'account di archiviazione per l'account di archiviazione wadexamplevm hello):</span><span class="sxs-lookup"><span data-stu-id="55a50-163">Replace `<StorageAccountKey>` with hello storage account key for your wadexamplevm storage account):</span></span>
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
### <a name="step-6-look-at-your-telemetry-data"></a><span data-ttu-id="55a50-164">Passaggio 6: Esaminare i dati di telemetria</span><span class="sxs-lookup"><span data-stu-id="55a50-164">Step 6: Look at your telemetry data</span></span>
<span data-ttu-id="55a50-165">In Visual Studio hello **Esplora Server** passare toohello wadexample account di archiviazione.</span><span class="sxs-lookup"><span data-stu-id="55a50-165">In hello Visual Studio **Server Explorer** navigate toohello wadexample storage account.</span></span> <span data-ttu-id="55a50-166">Dopo aver hello macchina virtuale è in esecuzione circa 5 minuti dovrebbe essere tabelle hello **WADEnumsTable**, **WADHighFreqTable**, **WADMessageTable**,  **WADPerformanceCountersTable** e **WADSetOtherTable**.</span><span class="sxs-lookup"><span data-stu-id="55a50-166">After hello VM has been running about 5 minutes you should see hello tables **WADEnumsTable**, **WADHighFreqTable**, **WADMessageTable**, **WADPerformanceCountersTable** and **WADSetOtherTable**.</span></span> <span data-ttu-id="55a50-167">Fare doppio clic su uno dei hello tabelle tooview hello dati di telemetria che sono stati raccolti.</span><span class="sxs-lookup"><span data-stu-id="55a50-167">Double-click on one of hello tables tooview hello telemetry that has been collected.</span></span>

![CloudServices_diag_wadexamplevm_tables](./media/virtual-machines-dotnet-diagnostics/WadExampleVMTables.png)

## <a name="configuration-file-schema"></a><span data-ttu-id="55a50-169">Schema del file di configurazione</span><span class="sxs-lookup"><span data-stu-id="55a50-169">Configuration file schema</span></span>
<span data-ttu-id="55a50-170">file di configurazione della diagnostica Hello definisce i valori vengono utilizzati tooinitialize le impostazioni di configurazione all'avvio dell'agente di diagnostica hello.</span><span class="sxs-lookup"><span data-stu-id="55a50-170">hello Diagnostics configuration file defines values that are used tooinitialize diagnostic configuration settings when hello diagnostics agent starts.</span></span> <span data-ttu-id="55a50-171">Vedere hello [riferimento allo schema più recente](https://msdn.microsoft.com/library/azure/mt634524.aspx) per i valori validi ed esempi.</span><span class="sxs-lookup"><span data-stu-id="55a50-171">See hello [latest schema reference](https://msdn.microsoft.com/library/azure/mt634524.aspx) for valid values and examples.</span></span>

## <a name="troubleshooting"></a><span data-ttu-id="55a50-172">Risoluzione dei problemi</span><span class="sxs-lookup"><span data-stu-id="55a50-172">Troubleshooting</span></span>
<span data-ttu-id="55a50-173">Per altre informazioni, vedere [Risoluzione dei problemi di Diagnostica di Azure](../monitoring-and-diagnostics/azure-diagnostics-troubleshooting.md)</span><span class="sxs-lookup"><span data-stu-id="55a50-173">See [Troubleshooting Azure Diagnostics](../monitoring-and-diagnostics/azure-diagnostics-troubleshooting.md) for more information.</span></span>

## <a name="next-steps"></a><span data-ttu-id="55a50-174">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="55a50-174">Next steps</span></span>
<span data-ttu-id="55a50-175">[Diagnostica di Azure articoli relativi a vedere un elenco di macchine virtuali](../monitoring-and-diagnostics/azure-diagnostics.md#virtual-machines-using-azure-diagnostics) dati hello toochange si raccolgono, risolvere i problemi o per altre informazioni sulla diagnostica in generale.</span><span class="sxs-lookup"><span data-stu-id="55a50-175">[See a list of virtual machine related Azure Diagnostics articles](../monitoring-and-diagnostics/azure-diagnostics.md#virtual-machines-using-azure-diagnostics) toochange hello data you are collecting, troubleshoot problems or learn more about diagnostics in general.</span></span>

[EventSource Class]: http://msdn.microsoft.com/library/system.diagnostics.tracing.eventsource(v=vs.110).aspx

[Debugging an Azure Application]: http://msdn.microsoft.com/library/windowsazure/ee405479.aspx   
[Collect Logging Data by Using Azure Diagnostics]: http://msdn.microsoft.com/library/windowsazure/gg433048.aspx
[Free Trial]: http://azure.microsoft.com/pricing/free-trial/
[Install and configure Azure PowerShell version 0.8.7 or later]: http://azure.microsoft.com/documentation/articles/install-configure-powershell/

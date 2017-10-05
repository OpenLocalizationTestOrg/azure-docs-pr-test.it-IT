---
title: Come usare la diagnostica di Azure nelle macchine virtuali | Microsoft Docs
description: Uso della diagnostica di Azure per raccogliere dati dalle macchine virtuali di Azure per debug, valutazione delle prestazioni, monitoraggio, analisi del traffico e altro ancora.
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
ms.openlocfilehash: 8ff6b9825212359617b748aba1c78ed789b130dd
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/03/2017
---
# <a name="enabling-diagnostics-in-azure-virtual-machines"></a><span data-ttu-id="dbaf0-103">Abilitare la diagnostica nelle macchine virtuali di Azure</span><span class="sxs-lookup"><span data-stu-id="dbaf0-103">Enabling Diagnostics in Azure Virtual Machines</span></span>
<span data-ttu-id="dbaf0-104">Vedere [Panoramica di Diagnostica di Azure](../monitoring-and-diagnostics/azure-diagnostics.md) per un'introduzione a Diagnostica di Azure.</span><span class="sxs-lookup"><span data-stu-id="dbaf0-104">See [Azure Diagnostics Overview](../monitoring-and-diagnostics/azure-diagnostics.md) for a background on Azure Diagnostics.</span></span>

## <a name="how-to-enable-diagnostics-in-a-virtual-machine"></a><span data-ttu-id="dbaf0-105">Come abilitare la diagnostica in una macchina virtuale</span><span class="sxs-lookup"><span data-stu-id="dbaf0-105">How to Enable Diagnostics in a Virtual Machine</span></span>
<span data-ttu-id="dbaf0-106">Questa procedura dettagliata descrive come installare in remoto la diagnostica in una macchina virtuale di Azure da un computer di sviluppo.</span><span class="sxs-lookup"><span data-stu-id="dbaf0-106">This walk through describes how to remotely install Diagnostics to an Azure virtual machine from a development computer.</span></span> <span data-ttu-id="dbaf0-107">Si apprenderà anche come implementare un'applicazione che viene eseguita in una macchina virtuale di Azure ed emette i dati di telemetria con la [classe EventSource][EventSource Class] .NET.</span><span class="sxs-lookup"><span data-stu-id="dbaf0-107">You also learn how to implement an application that runs on that Azure virtual machine and emits telemetry data using the .NET [EventSource Class][EventSource Class].</span></span> <span data-ttu-id="dbaf0-108">Il modulo Diagnostica Azure viene usato per raccogliere la telemetria e memorizzarla in un account di archiviazione di Azure.</span><span class="sxs-lookup"><span data-stu-id="dbaf0-108">Azure Diagnostics is used to collect the telemetry and store it in an Azure storage account.</span></span>

### <a name="pre-requisites"></a><span data-ttu-id="dbaf0-109">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="dbaf0-109">Pre-requisites</span></span>
<span data-ttu-id="dbaf0-110">In questa procedura si presuppone che l'utente abbia una sottoscrizione di Azure e usi Visual Studio 2017 con Azure SDK.</span><span class="sxs-lookup"><span data-stu-id="dbaf0-110">This walk through assumes you have an Azure subscription and are using Visual Studio 2017 with the Azure SDK.</span></span> <span data-ttu-id="dbaf0-111">Se non si ha una sottoscrizione di Azure, è possibile ottenere una [versione di prova gratuita][Free Trial].</span><span class="sxs-lookup"><span data-stu-id="dbaf0-111">If you do not have an Azure subscription, you can sign up for the [Free Trial][Free Trial].</span></span> <span data-ttu-id="dbaf0-112">Assicurarsi di [installare e configurare Azure PowerShell versione 0.8.7 o successiva][Install and configure Azure PowerShell version 0.8.7 or later].</span><span class="sxs-lookup"><span data-stu-id="dbaf0-112">Make sure to [Install and configure Azure PowerShell version 0.8.7 or later][Install and configure Azure PowerShell version 0.8.7 or later].</span></span>

### <a name="step-1-create-a-virtual-machine"></a><span data-ttu-id="dbaf0-113">Passaggio 1: Creare una macchina virtuale</span><span class="sxs-lookup"><span data-stu-id="dbaf0-113">Step 1: Create a Virtual Machine</span></span>
1. <span data-ttu-id="dbaf0-114">Nel computer di sviluppo, avviare Visual Studio 2017.</span><span class="sxs-lookup"><span data-stu-id="dbaf0-114">On your development computer, launch Visual Studio 2017.</span></span>
2. <span data-ttu-id="dbaf0-115">In **Esplora server** di Visual Studio espandere **Azure**, fare clic con il pulsante destro del mouse su **Macchine virtuali** e selezionare **Crea macchina virtuale**.</span><span class="sxs-lookup"><span data-stu-id="dbaf0-115">In the Visual Studio **Server Explorer** expand **Azure**, right-click **Virtual Machines** then select **Create Virtual Machine**.</span></span>
3. <span data-ttu-id="dbaf0-116">Selezionare la sottoscrizione Azure nella finestra di dialogo **Scegliere una sottoscrizione** e fare clic su **Avanti**.</span><span class="sxs-lookup"><span data-stu-id="dbaf0-116">Select your Azure subscription in the **Choose a Subscription** dialog and click **Next**.</span></span>
4. <span data-ttu-id="dbaf0-117">Selezionare **Windows Server 2012 R2 Datacenter, giugno 2017** nella finestra di dialogo **Selezionare un'immagine per la macchina virtuale** e fare clic su **Avanti**.</span><span class="sxs-lookup"><span data-stu-id="dbaf0-117">Select **Windows Server 2012 R2 Datacenter, June 2017** in the **Select a Virtual Machine Image** dialog and click **Next**.</span></span>
5. <span data-ttu-id="dbaf0-118">In **Impostazioni di base della macchina virtuale**impostare il nome della macchina virtuale su "wadexample".</span><span class="sxs-lookup"><span data-stu-id="dbaf0-118">In the **Virtual Machine Basic Settings**, set the virtual machine name to "wadexample".</span></span> <span data-ttu-id="dbaf0-119">Impostare il nome utente e la password dell'amministratore e fare clic su **Avanti**.</span><span class="sxs-lookup"><span data-stu-id="dbaf0-119">Set your Administrator user name and password and click **Next**.</span></span>
6. <span data-ttu-id="dbaf0-120">Nella finestra di dialogo **Impostazioni servizio cloud** creare un nuovo servizio cloud denominato "wadexampleVM".</span><span class="sxs-lookup"><span data-stu-id="dbaf0-120">In the **Cloud Service Settings** dialog create a new cloud service named "wadexampleVM".</span></span> <span data-ttu-id="dbaf0-121">Creare un nuovo account di archiviazione denominato "wadexample" e fare clic su **Avanti**.</span><span class="sxs-lookup"><span data-stu-id="dbaf0-121">Create a new Storage account named "wadexample" and click **Next**.</span></span>
7. <span data-ttu-id="dbaf0-122">Fare clic su **Create**.</span><span class="sxs-lookup"><span data-stu-id="dbaf0-122">Click **Create**.</span></span>

### <a name="step-2-create-your-application"></a><span data-ttu-id="dbaf0-123">Passaggio 2: Creare l'applicazione</span><span class="sxs-lookup"><span data-stu-id="dbaf0-123">Step 2: Create your Application</span></span>
1. <span data-ttu-id="dbaf0-124">Nel computer di sviluppo, avviare Visual Studio 2017.</span><span class="sxs-lookup"><span data-stu-id="dbaf0-124">On your development computer, launch Visual Studio 2017.</span></span>
2. <span data-ttu-id="dbaf0-125">Creare una nuova applicazione console Visual C# per .NET Framework 4.5.</span><span class="sxs-lookup"><span data-stu-id="dbaf0-125">Create a new Visual C# Console Application that targets .NET Framework 4.5.</span></span> <span data-ttu-id="dbaf0-126">Assegnare al progetto il nome "WadExampleVM".</span><span class="sxs-lookup"><span data-stu-id="dbaf0-126">Name the project "WadExampleVM".</span></span>

   ![CloudServices_diag_new_project](./media/virtual-machines-dotnet-diagnostics/NewProject.png)
3. <span data-ttu-id="dbaf0-128">Sostituire il contenuto del file Program.cs con il codice seguente.</span><span class="sxs-lookup"><span data-stu-id="dbaf0-128">Replace the contents of Program.cs with the following code.</span></span> <span data-ttu-id="dbaf0-129">La classe **SampleEventSourceWriter** implementa quattro metodi di registrazione: **SendEnums**, **MessageMethod**, **SetOther** e **HighFreq**.</span><span class="sxs-lookup"><span data-stu-id="dbaf0-129">The class **SampleEventSourceWriter** implements four logging methods: **SendEnums**, **MessageMethod**, **SetOther** and **HighFreq**.</span></span> <span data-ttu-id="dbaf0-130">Il primo parametro per il metodo WriteEvent definisce l'ID per il rispettivo evento.</span><span class="sxs-lookup"><span data-stu-id="dbaf0-130">The first parameter to the WriteEvent method defines the ID for the respective event.</span></span> <span data-ttu-id="dbaf0-131">Il metodo Run implementa un ciclo infinito che chiama ognuno dei metodi di registrazione implementati nella classe **SampleEventSourceWriter** ogni 10 secondi.</span><span class="sxs-lookup"><span data-stu-id="dbaf0-131">The Run method implements an infinite loop that calls each of the logging methods implemented in the **SampleEventSourceWriter** class every 10 seconds.</span></span>

    ```csharp
     using System;
     using System.Diagnostics;
     using System.Diagnostics.Tracing;
     using System.Threading;

     namespace WadExampleVM
     {
       sealed class SampleEventSourceWriter : EventSource {
         public static SampleEventSourceWriter Log = new SampleEventSourceWriter();
         public void SendEnums(MyColor color, MyFlags flags) { if (IsEnabled())  WriteEvent(1, (int)color, (int)flags); } // Cast enums to int for efficient logging.
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

             // Emit several events every time we go through the loop
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
4. <span data-ttu-id="dbaf0-132">Salvare il file e scegliere **Compila soluzione** dal menu **Compila** per compilare il codice.</span><span class="sxs-lookup"><span data-stu-id="dbaf0-132">Save the file and select **Build Solution** from the **Build** menu to build your code.</span></span>

### <a name="step-3-deploy-your-application"></a><span data-ttu-id="dbaf0-133">Passaggio 3: Distribuire l'applicazione</span><span class="sxs-lookup"><span data-stu-id="dbaf0-133">Step 3: Deploy your Application</span></span>
1. <span data-ttu-id="dbaf0-134">Fare clic con il pulsante destro del mouse sul progetto **WadExampleVM** in **Esplora soluzioni** e scegliere **Apri cartella in Esplora file**.</span><span class="sxs-lookup"><span data-stu-id="dbaf0-134">Right-click on the **WadExampleVM** project in **Solution Explorer** and choose **Open Folder in File Explorer**.</span></span>
2. <span data-ttu-id="dbaf0-135">Passare alla cartella *bin\Debug* e copiare tutti i file (WadExampleVM.*)</span><span class="sxs-lookup"><span data-stu-id="dbaf0-135">Navigate to the *bin\Debug* folder and copy all the files (WadExampleVM.*)</span></span>
3. <span data-ttu-id="dbaf0-136">In **Esplora server** fare clic con il pulsante destro del mouse sulla macchina virtuale e scegliere **Connessione tramite desktop remoto**.</span><span class="sxs-lookup"><span data-stu-id="dbaf0-136">In **Server Explorer** right-click on the virtual machine and choose **Connect using Remote Desktop**.</span></span>
4. <span data-ttu-id="dbaf0-137">Una volta connessi alla macchina virtuale, creare una cartella denominata WadExampleVM e incollare i file dell'applicazione nella cartella.</span><span class="sxs-lookup"><span data-stu-id="dbaf0-137">Once connected to the VM create a folder named WadExampleVM and paste your application files into the folder.</span></span>
5. <span data-ttu-id="dbaf0-138">Avviare l'applicazione WadExampleVM.exe.</span><span class="sxs-lookup"><span data-stu-id="dbaf0-138">Launch the application WadExampleVM.exe.</span></span> <span data-ttu-id="dbaf0-139">Verrà visualizzata una finestra della console vuota.</span><span class="sxs-lookup"><span data-stu-id="dbaf0-139">You should see a blank console window.</span></span>

### <a name="step-4-create-your-diagnostics-configuration-and-install-the-extension"></a><span data-ttu-id="dbaf0-140">Passaggio 4: Creare la configurazione per la diagnostica e installare l'estensione</span><span class="sxs-lookup"><span data-stu-id="dbaf0-140">Step 4: Create your Diagnostics configuration and install the Extension</span></span>
1. <span data-ttu-id="dbaf0-141">Scaricare la definizione dello schema del file di configurazione pubblico nel computer di sviluppo eseguendo il comando PowerShell seguente:</span><span class="sxs-lookup"><span data-stu-id="dbaf0-141">Download the public configuration file schema definition to your development computer by executing the following PowerShell command:</span></span>

     <span data-ttu-id="dbaf0-142">(Get-AzureServiceAvailableExtension -ExtensionName 'PaaSDiagnostics' -ProviderNamespace 'Microsoft.Azure.Diagnostics').PublicConfigurationSchema | Out-File -Encoding utf8 -FilePath 'WadConfig.xsd'</span><span class="sxs-lookup"><span data-stu-id="dbaf0-142">(Get-AzureServiceAvailableExtension -ExtensionName 'PaaSDiagnostics' -ProviderNamespace 'Microsoft.Azure.Diagnostics').PublicConfigurationSchema | Out-File -Encoding utf8 -FilePath 'WadConfig.xsd'</span></span>
2. <span data-ttu-id="dbaf0-143">Aprire un nuovo file XML in Visual Studio, in un progetto già aperto o in un'istanza di Visual Studio senza progetti aperti</span><span class="sxs-lookup"><span data-stu-id="dbaf0-143">Open a new XML file in Visual Studio, either in a project you already have open or in a Visual Studio instance with no open projects.</span></span> <span data-ttu-id="dbaf0-144">In Visual Studio selezionare **Aggiungi** -> **Nuovo elemento...**</span><span class="sxs-lookup"><span data-stu-id="dbaf0-144">In Visual Studio, select **Add** -> **New Item…**</span></span><span data-ttu-id="dbaf0-145"> -> **Elementi di Visual C#** -> **Dati** -> **File XML**.</span><span class="sxs-lookup"><span data-stu-id="dbaf0-145"> -> **Visual C# items** -> **Data** -> **XML File**.</span></span> <span data-ttu-id="dbaf0-146">Assegnare al file il nome "WadExample.xml".</span><span class="sxs-lookup"><span data-stu-id="dbaf0-146">Name the file "WadExample.xml"</span></span>
3. <span data-ttu-id="dbaf0-147">Associare WadConfig.xsd al file di configurazione.</span><span class="sxs-lookup"><span data-stu-id="dbaf0-147">Associate the WadConfig.xsd with the configuration file.</span></span> <span data-ttu-id="dbaf0-148">Assicurarsi che la finestra dell'editor di WadExample.xml sia la finestra attiva.</span><span class="sxs-lookup"><span data-stu-id="dbaf0-148">Make sure the WadExample.xml editor window is the active window.</span></span> <span data-ttu-id="dbaf0-149">Premere **F4** per aprire la finestra **Proprietà**.</span><span class="sxs-lookup"><span data-stu-id="dbaf0-149">Press **F4** to open the **Properties** window.</span></span> <span data-ttu-id="dbaf0-150">Fare clic sulla proprietà **Schemi** nella finestra **Proprietà**.</span><span class="sxs-lookup"><span data-stu-id="dbaf0-150">Click on the **Schemas** property in the **Properties** window.</span></span> <span data-ttu-id="dbaf0-151">Fare clic su **...**</span><span class="sxs-lookup"><span data-stu-id="dbaf0-151">Click the **…**</span></span> <span data-ttu-id="dbaf0-152">in the **Schemi** .</span><span class="sxs-lookup"><span data-stu-id="dbaf0-152">in the **Schemas** property.</span></span> <span data-ttu-id="dbaf0-153">Fare clic su **Aggiungi**</span><span class="sxs-lookup"><span data-stu-id="dbaf0-153">Click the **Add…**</span></span> <span data-ttu-id="dbaf0-154">, passare al percorso in cui si è salvato il file XSD e selezionare il file WadConfig.xsd.</span><span class="sxs-lookup"><span data-stu-id="dbaf0-154">button and navigate to the location where you saved the XSD file and select the file WadConfig.xsd.</span></span> <span data-ttu-id="dbaf0-155">Fare clic su **OK**.</span><span class="sxs-lookup"><span data-stu-id="dbaf0-155">Click **OK**.</span></span>
4. <span data-ttu-id="dbaf0-156">Sostituire i contenuti del file di configurazione WadExample.xml con il codice XML seguente e salvare il file.</span><span class="sxs-lookup"><span data-stu-id="dbaf0-156">Replace the contents of the WadExample.xml configuration file with the following XML and save the file.</span></span> <span data-ttu-id="dbaf0-157">Questo file di configurazione definisce due contatori delle prestazioni per la raccolta: uno per l'uso della CPU e uno per l'uso della memoria.</span><span class="sxs-lookup"><span data-stu-id="dbaf0-157">This configuration file defines a couple performance counters to collect: one for CPU utilization and one for memory utilization.</span></span> <span data-ttu-id="dbaf0-158">La configurazione definisce quindi quattro eventi corrispondenti ai metodi della classe SampleEventSourceWriter.</span><span class="sxs-lookup"><span data-stu-id="dbaf0-158">Then the configuration defines the four events corresponding to the methods in the SampleEventSourceWriter class.</span></span>

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

### <a name="step-5-remotely-install-diagnostics-on-your-azure-virtual-machine"></a><span data-ttu-id="dbaf0-159">Passaggio 5: Installare in remoto la diagnostica nella macchina virtuale di Azure</span><span class="sxs-lookup"><span data-stu-id="dbaf0-159">Step 5: Remotely install Diagnostics on your Azure Virtual Machine</span></span>
<span data-ttu-id="dbaf0-160">I cmdlet di PowerShell per la gestione della diagnostica in una macchina virtuale sono: Set-AzureVMDiagnosticsExtension, Get-AzureVMDiagnosticsExtension e Remove-AzureVMDiagnosticsExtension.</span><span class="sxs-lookup"><span data-stu-id="dbaf0-160">The PowerShell cmdlets for managing Diagnostics on a VM are: Set-AzureVMDiagnosticsExtension, Get-AzureVMDiagnosticsExtension, and Remove-AzureVMDiagnosticsExtension.</span></span>

1. <span data-ttu-id="dbaf0-161">Nel computer dello sviluppatore aprire Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="dbaf0-161">On your developer computer, open Azure PowerShell.</span></span>
2. <span data-ttu-id="dbaf0-162">Eseguire lo script per installare in modalità remota la Diagnostica sulla macchina virtuale (Sostituire `<user>` con il nome della directory utente.</span><span class="sxs-lookup"><span data-stu-id="dbaf0-162">Execute the script to remotely install Diagnostics on your VM (Replace `<user>` with your user directory name.</span></span> <span data-ttu-id="dbaf0-163">Sostituire `<StorageAccountKey>` con la chiave dell'account di archiviazione per l'account di archiviazione wadexamplevm):</span><span class="sxs-lookup"><span data-stu-id="dbaf0-163">Replace `<StorageAccountKey>` with the storage account key for your wadexamplevm storage account):</span></span>
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
### <a name="step-6-look-at-your-telemetry-data"></a><span data-ttu-id="dbaf0-164">Passaggio 6: Esaminare i dati di telemetria</span><span class="sxs-lookup"><span data-stu-id="dbaf0-164">Step 6: Look at your telemetry data</span></span>
<span data-ttu-id="dbaf0-165">In **Esplora server** di Visual Studio passare all'account di archiviazione di wadexample.</span><span class="sxs-lookup"><span data-stu-id="dbaf0-165">In the Visual Studio **Server Explorer** navigate to the wadexample storage account.</span></span> <span data-ttu-id="dbaf0-166">Dopo che la macchina virtuale è rimasta in esecuzione per circa 5 minuti, vengono visualizzate le tabelle **WADEnumsTable**, **WADHighFreqTable**, **WADMessageTable**, **WADPerformanceCountersTable** e **WADSetOtherTable**.</span><span class="sxs-lookup"><span data-stu-id="dbaf0-166">After the VM has been running about 5 minutes you should see the tables **WADEnumsTable**, **WADHighFreqTable**, **WADMessageTable**, **WADPerformanceCountersTable** and **WADSetOtherTable**.</span></span> <span data-ttu-id="dbaf0-167">Fare doppio clic su una delle tabelle per visualizzare i dati di telemetria raccolti.</span><span class="sxs-lookup"><span data-stu-id="dbaf0-167">Double-click on one of the tables to view the telemetry that has been collected.</span></span>

![CloudServices_diag_wadexamplevm_tables](./media/virtual-machines-dotnet-diagnostics/WadExampleVMTables.png)

## <a name="configuration-file-schema"></a><span data-ttu-id="dbaf0-169">Schema del file di configurazione</span><span class="sxs-lookup"><span data-stu-id="dbaf0-169">Configuration file schema</span></span>
<span data-ttu-id="dbaf0-170">Il file di configurazione della diagnostica definisce i valori usati per inizializzare le impostazioni di diagnostica quando viene avviato il monitor di diagnostica.</span><span class="sxs-lookup"><span data-stu-id="dbaf0-170">The Diagnostics configuration file defines values that are used to initialize diagnostic configuration settings when the diagnostics agent starts.</span></span> <span data-ttu-id="dbaf0-171">Vedere il [riferimento allo schema più recente](https://msdn.microsoft.com/library/azure/mt634524.aspx) per i valori validi ed alcuni esempi.</span><span class="sxs-lookup"><span data-stu-id="dbaf0-171">See the [latest schema reference](https://msdn.microsoft.com/library/azure/mt634524.aspx) for valid values and examples.</span></span>

## <a name="troubleshooting"></a><span data-ttu-id="dbaf0-172">Risoluzione dei problemi</span><span class="sxs-lookup"><span data-stu-id="dbaf0-172">Troubleshooting</span></span>
<span data-ttu-id="dbaf0-173">Per altre informazioni, vedere [Risoluzione dei problemi di Diagnostica di Azure](../monitoring-and-diagnostics/azure-diagnostics-troubleshooting.md)</span><span class="sxs-lookup"><span data-stu-id="dbaf0-173">See [Troubleshooting Azure Diagnostics](../monitoring-and-diagnostics/azure-diagnostics-troubleshooting.md) for more information.</span></span>

## <a name="next-steps"></a><span data-ttu-id="dbaf0-174">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="dbaf0-174">Next steps</span></span>
<span data-ttu-id="dbaf0-175">[Vedere un elenco di articoli sulla diagnostica di Azure relativi a macchine virtuali](../monitoring-and-diagnostics/azure-diagnostics.md#virtual-machines-using-azure-diagnostics) per modificare i dati raccolti, risolvere i problemi o ottenere altre informazioni sulla diagnostica in generale.</span><span class="sxs-lookup"><span data-stu-id="dbaf0-175">[See a list of virtual machine related Azure Diagnostics articles](../monitoring-and-diagnostics/azure-diagnostics.md#virtual-machines-using-azure-diagnostics) to change the data you are collecting, troubleshoot problems or learn more about diagnostics in general.</span></span>

[EventSource Class]: http://msdn.microsoft.com/library/system.diagnostics.tracing.eventsource(v=vs.110).aspx

[Debugging an Azure Application]: http://msdn.microsoft.com/library/windowsazure/ee405479.aspx   
[Collect Logging Data by Using Azure Diagnostics]: http://msdn.microsoft.com/library/windowsazure/gg433048.aspx
[Free Trial]: http://azure.microsoft.com/pricing/free-trial/
[Install and configure Azure PowerShell version 0.8.7 or later]: http://azure.microsoft.com/documentation/articles/install-configure-powershell/

---
title: un modulo di Edge IoT di Azure con c# aaaCreate | Documenti Microsoft
description: "In questa esercitazione illustra come una tabella dati convertitore modulo utilizzando toowrite hello pacchetti di Azure IoT Edge NuGet più recenti, in c# e Visual Studio Code."
services: iot-hub
author: jeffreyCline
manager: timlt
keywords: azure, iot, esercitazione, modulo, nuget, vscode, csharp, edge
ms.service: iot-hub
ms.devlang: csharp
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 06/28/2017
ms.author: jcline
ms.openlocfilehash: b104609c05d1613e21acc7d7bed547f311179151
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="create-an-azure-iot-edge-module-with-cx23"></a><span data-ttu-id="d643b-104">Creare un modulo Azure IoT Edge con C&#x23;</span><span class="sxs-lookup"><span data-stu-id="d643b-104">Create an Azure IoT Edge Module with C&#x23;</span></span>

<span data-ttu-id="d643b-105">In questa esercitazione illustra come toocreate un modulo per `Azure IoT Edge` utilizzando `Visual Studio Code` e `C#`.</span><span class="sxs-lookup"><span data-stu-id="d643b-105">This tutorial showcases how toocreate a module for `Azure IoT Edge` using `Visual Studio Code` and `C#`.</span></span>

<span data-ttu-id="d643b-106">In questa esercitazione vengono illustrate le impostazione di ambiente e come toowrite un [BILITA](https://en.wikipedia.org/wiki/Bluetooth_Low_Energy) modulo convertitore di tipi di dati tramite hello più recente `Azure IoT Edge NuGet` pacchetti.</span><span class="sxs-lookup"><span data-stu-id="d643b-106">In this tutorial, we walk through environment set-up and how toowrite a [BLE](https://en.wikipedia.org/wiki/Bluetooth_Low_Energy) data converter module using hello latest `Azure IoT Edge NuGet` packages.</span></span> 

>[!NOTE]
<span data-ttu-id="d643b-107">In questa esercitazione Usa hello `.NET Core SDK`, che supporta compatibilità multipiattaforma.</span><span class="sxs-lookup"><span data-stu-id="d643b-107">This tutorial is using hello `.NET Core SDK`, which supports cross-platform compatibility.</span></span> <span data-ttu-id="d643b-108">Hello esercitazione seguente viene scritto utilizzando hello `Windows 10` del sistema operativo.</span><span class="sxs-lookup"><span data-stu-id="d643b-108">hello following tutorial is written using hello `Windows 10` operating system.</span></span> <span data-ttu-id="d643b-109">Alcuni dei comandi di hello in questa esercitazione potrebbero essere diverse a seconda del `development environment`.</span><span class="sxs-lookup"><span data-stu-id="d643b-109">Some of hello commands in this tutorial may be different depending on your `development environment`.</span></span> 

## <a name="prerequisites"></a><span data-ttu-id="d643b-110">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="d643b-110">Prerequisites</span></span>

<span data-ttu-id="d643b-111">In questa sezione si configura l'ambiente per lo sviluppo del modulo `Azure IoT Edge`.</span><span class="sxs-lookup"><span data-stu-id="d643b-111">In this section, we set-up your environment for `Azure IoT Edge` module development.</span></span> <span data-ttu-id="d643b-112">Si applica tooboth **Windows a 64 bit** e **Linux a 64 bit (8 Ubuntu/Debian)** i sistemi operativi.</span><span class="sxs-lookup"><span data-stu-id="d643b-112">It applies tooboth **64-bit Windows** and **64-bit Linux (Ubuntu/Debian 8)** operating systems.</span></span>

<span data-ttu-id="d643b-113">Hello seguente software è necessario:</span><span class="sxs-lookup"><span data-stu-id="d643b-113">hello following software is required:</span></span>

- [<span data-ttu-id="d643b-114">Client Git</span><span class="sxs-lookup"><span data-stu-id="d643b-114">Git Client</span></span>](https://git-scm.com/downloads)
- [<span data-ttu-id="d643b-115">ASP.NET Core SDK</span><span class="sxs-lookup"><span data-stu-id="d643b-115">.NET Core SDK</span></span>](https://www.microsoft.com/net/core#windowscmd)
- [<span data-ttu-id="d643b-116">Visual Studio Code</span><span class="sxs-lookup"><span data-stu-id="d643b-116">Visual Studio Code</span></span>](https://code.visualstudio.com/)

<span data-ttu-id="d643b-117">Non è necessario repository hello tooclone per questo esempio, tuttavia tutte hello esempi di codice illustrati in questa esercitazione si trova nella seguente repository hello:</span><span class="sxs-lookup"><span data-stu-id="d643b-117">You do not need tooclone hello repo for this sample, however all of hello sample code discussed in this tutorial is located in hello following repository:</span></span>

- <span data-ttu-id="d643b-118">`git clone https://github.com/Azure-Samples/iot-edge-samples.git`.</span><span class="sxs-lookup"><span data-stu-id="d643b-118">`git clone https://github.com/Azure-Samples/iot-edge-samples.git`.</span></span>
- `cd iot-edge-samples/dotnetcore/simulated_ble`

## <a name="getting-started"></a><span data-ttu-id="d643b-119">Introduzione</span><span class="sxs-lookup"><span data-stu-id="d643b-119">Getting started</span></span>

1. <span data-ttu-id="d643b-120">Installare `.NET Core SDK`.</span><span class="sxs-lookup"><span data-stu-id="d643b-120">Install `.NET Core SDK`.</span></span>
2. <span data-ttu-id="d643b-121">Installare `Visual Studio Code` hello e `C# extension` da Visual Studio Marketplace di codice hello.</span><span class="sxs-lookup"><span data-stu-id="d643b-121">Install `Visual Studio Code` and hello `C# extension` from hello Visual Studio Code Marketplace.</span></span>

<span data-ttu-id="d643b-122">Visualizzare questo [video di esercitazione rapida](https://channel9.msdn.com/Blogs/dotnet/Get-started-VSCode-Csharp-NET-Core-Windows) sulla modalità di avvio utilizzando tooget `Visual Studio Code` hello e `.NET Core SDK`.</span><span class="sxs-lookup"><span data-stu-id="d643b-122">View this [quick video tutorial](https://channel9.msdn.com/Blogs/dotnet/Get-started-VSCode-Csharp-NET-Core-Windows) about how tooget started using `Visual Studio Code` and hello `.NET Core SDK`.</span></span>

## <a name="creating-hello-azure-iot-edge-converter-module"></a><span data-ttu-id="d643b-123">Creazione di hello Azure IoT Edge convertitore modulo</span><span class="sxs-lookup"><span data-stu-id="d643b-123">Creating hello Azure IoT Edge converter module</span></span>

1. <span data-ttu-id="d643b-124">Inizializzare un nuovo progetto C# di libreria di classi `.NET Core`:</span><span class="sxs-lookup"><span data-stu-id="d643b-124">Initialize a new `.NET Core` class library C# project:</span></span>
    - <span data-ttu-id="d643b-125">Aprire il prompt dei comandi (`Windows + R` -> `cmd` -> `enter`).</span><span class="sxs-lookup"><span data-stu-id="d643b-125">Open a command prompt (`Windows + R` -> `cmd` -> `enter`).</span></span>
    - <span data-ttu-id="d643b-126">Esplorazione delle cartelle toohello in cui si desidera toocreate hello `C#` progetto.</span><span class="sxs-lookup"><span data-stu-id="d643b-126">Navigate toohello folder where you'd like toocreate hello `C#` project.</span></span>
    - <span data-ttu-id="d643b-127">Digitare **dotnet new classlib -o IoTEdgeConverterModule -f netstandard1.3**.</span><span class="sxs-lookup"><span data-stu-id="d643b-127">Type **dotnet new classlib -o IoTEdgeConverterModule -f netstandard1.3**.</span></span> 
    - <span data-ttu-id="d643b-128">Questo comando crea una classe vuota denominata `Class1.cs` nella directory dei progetti.</span><span class="sxs-lookup"><span data-stu-id="d643b-128">This command creates an empty class called `Class1.cs` in your projects directory.</span></span>
2. <span data-ttu-id="d643b-129">Passare toohello nella cartella in cui è appena creata progetto libreria di classi hello digitando **cd IoTEdgeConverterModule**.</span><span class="sxs-lookup"><span data-stu-id="d643b-129">Navigate toohello folder where we just created hello class library project by typing **cd IoTEdgeConverterModule**.</span></span>
3. <span data-ttu-id="d643b-130">Progetto aperto hello in `Visual Studio Code` digitando **codice.**.</span><span class="sxs-lookup"><span data-stu-id="d643b-130">Open hello project in `Visual Studio Code` by typing **code .**.</span></span>
4. <span data-ttu-id="d643b-131">Una volta hello progetto è aperto in `Visual Studio Code`, fare clic su hello **IoTEdgeConverterModule.csproj** il file hello tooopen come illustrato nella seguente immagine hello:</span><span class="sxs-lookup"><span data-stu-id="d643b-131">Once hello project is opened in `Visual Studio Code`, click on hello **IoTEdgeConverterModule.csproj** tooopen hello file as shown in hello following image:</span></span>

    ![Finestra di modifica di Visual Studio Code](media/iot-hub-iot-edge-create-module/vscode-edit-csproj.png)

5. <span data-ttu-id="d643b-133">Inserisci hello `XML` blob illustrato nel seguente frammento di codice tra chiusura hello hello `PropertyGroup` tag e hello chiusura `Project` tag; riga sei hello immagine precedente e salvare il file hello premendo `Ctrl`  +  `S`.</span><span class="sxs-lookup"><span data-stu-id="d643b-133">Insert hello `XML` blob shown in hello following code snippet between hello closing `PropertyGroup` tag and hello closing `Project` tag; line six in hello preceding image and save hello file by pressing `Ctrl` + `S`.</span></span>

   ```xml
     <ItemGroup>
       <PackageReference Include="Microsoft.Azure.Devices.Gateway.Module.NetStandard" Version="1.0.5" />
       <PackageReference Include="System.Threading.Thread" Version="4.3.0" />
       <PackageReference Include="Newtonsoft.Json" Version="10.0.2" />
     </ItemGroup> 
   ```

6. <span data-ttu-id="d643b-134">Dopo aver salvato hello `.csproj` file `Visual Studio Code` dovrebbe ricevere una richiesta con un `unresolved dependencies` finestra di dialogo come illustrato nella seguente immagine hello:</span><span class="sxs-lookup"><span data-stu-id="d643b-134">Once you save hello `.csproj` file, `Visual Studio Code` should prompt you with an `unresolved dependencies` dialog as seen in hello following image:</span></span> 

    ![Finestra di Visual Studio Code per il ripristino delle dipendenze](media/iot-hub-iot-edge-create-module/vscode-restore.png)

    <span data-ttu-id="d643b-136">a) fare clic su `Restore` toorestore tutti di hello i riferimenti nei progetti di hello `.csproj` file incluso hello `PackageReferences` è stato aggiunto.</span><span class="sxs-lookup"><span data-stu-id="d643b-136">a) Click `Restore` toorestore all of hello references in hello projects `.csproj` file including hello `PackageReferences` we have added.</span></span> 

    <span data-ttu-id="d643b-137">b) `Visual Studio Code` crea automaticamente hello `project.assets.json` file nei progetti `obj` cartella.</span><span class="sxs-lookup"><span data-stu-id="d643b-137">b) `Visual Studio Code` automatically creates hello `project.assets.json` file in your projects `obj` folder.</span></span> <span data-ttu-id="d643b-138">Questo file contiene informazioni le dipendenze toomake ripristini successivi del progetto più veloce.</span><span class="sxs-lookup"><span data-stu-id="d643b-138">This file contains information about your project's dependencies toomake subsequent restores quicker.</span></span>
 
    >[!NOTE]
    <span data-ttu-id="d643b-139">`.NET Core Tools`sono ora basati su MSBuild.</span><span class="sxs-lookup"><span data-stu-id="d643b-139">`.NET Core Tools` are now MSBuild-based.</span></span> <span data-ttu-id="d643b-140">Ciò significa che viene creato un file di progetto `.csproj` anziché un file `project.json`.</span><span class="sxs-lookup"><span data-stu-id="d643b-140">Which means a `.csproj` project file is created instead of a `project.json`.</span></span>

    - <span data-ttu-id="d643b-141">Se `Visual Studio Code` non riesce a crearlo automaticamente, è possibile eseguire l'operazione manualmente.</span><span class="sxs-lookup"><span data-stu-id="d643b-141">If `Visual Studio Code` does not prompt you that is ok, we can do it manually.</span></span> <span data-ttu-id="d643b-142">Aprire hello `Visual Studio Code` integrata finestra terminal premendo hello `Ctrl`  +  `backtick` chiavi o utilizzando i menu hello `View`  ->  `Integrated Terminal`.</span><span class="sxs-lookup"><span data-stu-id="d643b-142">Open hello `Visual Studio Code` integrated terminal window by pressing hello `Ctrl` + `backtick` keys or using hello menus `View` -> `Integrated Terminal`.</span></span>
    - <span data-ttu-id="d643b-143">In hello `Integrated Terminal` tipo di finestra **ripristino dotnet**.</span><span class="sxs-lookup"><span data-stu-id="d643b-143">In hello `Integrated Terminal` window type **dotnet restore**.</span></span>
    
7. <span data-ttu-id="d643b-144">Rinominare hello `Class1.cs` file troppo`BleConverterModule.cs`.</span><span class="sxs-lookup"><span data-stu-id="d643b-144">Rename hello `Class1.cs` file too`BleConverterModule.cs`.</span></span> 

    <span data-ttu-id="d643b-145">) file hello toorename innanzitutto fare clic sul file hello quindi premere hello `F2` chiave.</span><span class="sxs-lookup"><span data-stu-id="d643b-145">a) toorename hello file first click on hello file then press hello `F2` key.</span></span>
    
    <span data-ttu-id="d643b-146">b) tipo in un nuovo nome hello **BleConverterModule**, come illustrato nella seguente immagine hello:</span><span class="sxs-lookup"><span data-stu-id="d643b-146">b) Type in hello new name **BleConverterModule**, as seen in hello following image:</span></span>

    ![Assegnazione di un nuovo nome a una classe da parte di Visual Studio Code](media/iot-hub-iot-edge-create-module/vscode-rename.png)

8. <span data-ttu-id="d643b-148">Sostituire il codice esistente in hello hello `BleConverterModule.cs` file da copiare e incollare hello seguente frammento di codice il `BleConverterModule.cs` file.</span><span class="sxs-lookup"><span data-stu-id="d643b-148">Replace hello existing code in hello `BleConverterModule.cs` file by copying and pasting hello following code snippet into your `BleConverterModule.cs` file.</span></span>

   ```csharp
   using System;
   using System.Collections.Generic;
   using System.Globalization;
   using System.Linq;
   using System.Text;
   using System.Threading;
   using System.Threading.Tasks;
   using Microsoft.Azure.Devices.Gateway;
   using Newtonsoft.Json;
   
   namespace IoTEdgeConverterModule
   {
       public class BleConverterModule : IGatewayModule, IGatewayModuleStart
       {
           private Broker broker;
           private string configuration;
           private int messageCount;

           public void Create(Broker broker, byte[] configuration)
           {
               this.broker = broker;
               this.configuration = System.Text.Encoding.UTF8.GetString(configuration);
           }
   
           public void Start()
           {
           }

           public void Destroy()
           {
           }

           public void Receive(Message received_message)
           {
               string recMsg = Encoding.UTF8.GetString(received_message.Content, 0, received_message.Content.Length);
               BleData receivedData = JsonConvert.DeserializeObject<BleData>(recMsg);

               float temperature = float.Parse(receivedData.Temperature, CultureInfo.InvariantCulture.NumberFormat); 
               Dictionary<string, string> receivedProperties = received_message.Properties;
            
               Dictionary<string, string> properties = new Dictionary<string, string>();
               properties.Add("source", receivedProperties["source"]);
               properties.Add("macAddress", receivedProperties["macAddress"]);
               properties.Add("temperatureAlert", temperature > 30 ? "true" : "false");
   
               String content = String.Format("{0} \"deviceId\": \"Intel NUC Gateway\", \"messageId\": {1}, \"temperature\": {2} {3}", "{", ++this.messageCount, temperature, "}");
               Message messageToPublish = new Message(content, properties);
   
               this.broker.Publish(messageToPublish);
           }
       }
   }
   ```

9. <span data-ttu-id="d643b-149">Salvare il file hello premendo `Ctrl`  +  `S`.</span><span class="sxs-lookup"><span data-stu-id="d643b-149">Save hello file by pressing `Ctrl` + `S`.</span></span>

10. <span data-ttu-id="d643b-150">Creare un nuovo file denominato `Untitled-1` da premendo hello `Ctrl`  +  `N` tasti come illustrato nella seguente immagine hello:</span><span class="sxs-lookup"><span data-stu-id="d643b-150">Create a new file called `Untitled-1` by pressing hello `Ctrl` + `N` keys as seen in hello following image:</span></span>

    ![Nuovo file di Visual Studio Code](media/iot-hub-iot-edge-create-module/vscode-new-file.png)

11. <span data-ttu-id="d643b-152">hello toodeserialize `JSON` oggetto riceviamo hello simulato `BLE` dispositivo, hello copia seguente di codice in hello `Untitled-1` finestra dell'editor di codice file.</span><span class="sxs-lookup"><span data-stu-id="d643b-152">toodeserialize hello `JSON` object that we receive from hello simulated `BLE` device, copy hello following code into hello `Untitled-1` file code editor window.</span></span> 

   ```csharp
   using System;
   using Newtonsoft.Json;

   namespace IoTEdgeConverterModule
   {
       public class BleData
       {
           [JsonProperty(PropertyName = "temperature")]
           public string Temperature { get; set; }
       }
   }
   ```

12. <span data-ttu-id="d643b-153">Salvare il file hello come `BleData.cs` premendo `Ctrl`  +  `Shift`  +  `S` chiavi.</span><span class="sxs-lookup"><span data-stu-id="d643b-153">Save hello file as `BleData.cs` by pressing `Ctrl` + `Shift` + `S` keys.</span></span>
    - <span data-ttu-id="d643b-154">In hello salvare come finestra di dialogo hello `Save as Type` menu a discesa, seleziona `C# (*.cs;*.csx)` come illustrato nella seguente immagine hello:</span><span class="sxs-lookup"><span data-stu-id="d643b-154">On hello save as dialog box, in hello `Save as Type` dropdown menu, select `C# (*.cs;*.csx)` as seen in hello following image:</span></span>

    ![Finestra di dialogo Salva con nome di Visual Studio Code](media/iot-hub-iot-edge-create-module/vscode-save-as.png)

13. <span data-ttu-id="d643b-156">Creare un nuovo file denominato `Untitled-1` da premendo hello `Ctrl`  +  `N` chiavi.</span><span class="sxs-lookup"><span data-stu-id="d643b-156">Create a new file called `Untitled-1` by pressing hello `Ctrl` + `N` keys.</span></span>

14. <span data-ttu-id="d643b-157">Copiare e incollare hello seguente frammento di codice in hello `Untitled-1` file.</span><span class="sxs-lookup"><span data-stu-id="d643b-157">Copy and paste hello following code snippet into hello `Untitled-1` file.</span></span> <span data-ttu-id="d643b-158">Questa classe è un `Azure IoT Edge` modulo, utilizziamo dati hello toooutput ricevuti dai nostri `BleConverterModule`.</span><span class="sxs-lookup"><span data-stu-id="d643b-158">This class is a `Azure IoT Edge` module, which we use toooutput hello data received from our `BleConverterModule`.</span></span>

   ```csharp
   using System;
   using System.Collections.Generic;
   using System.Linq;
   using System.Text;
   using System.Threading.Tasks;
   using Microsoft.Azure.Devices.Gateway;
   using Newtonsoft.Json;
   
   namespace PrinterModule
   {
       public class DotNetPrinterModule : IGatewayModule
       {
           private string configuration;
           public void Create(Broker broker, byte[] configuration)
           {
               this.configuration = System.Text.Encoding.UTF8.GetString(configuration);
           }
   
           public void Destroy()
           {
           }
   
           public void Receive(Message received_message)
           {
               string recMsg = System.Text.Encoding.UTF8.GetString(received_message.Content, 0, received_message.Content.Length);
               Dictionary<string, string> receivedProperties = received_message.Properties;
               
               BleConverterData receivedData = JsonConvert.DeserializeObject<BleConverterData>(recMsg);
   
               Console.WriteLine();
               Console.WriteLine("Module           : [DotNetPrinterModule]");
               Console.WriteLine("received_message : {0}", recMsg);
   
               if(received_message.Properties["source"] == "bleTelemetry")
               {
                   Console.WriteLine("Source           : {0}", receivedProperties["source"]);
                   Console.WriteLine("MAC address      : {0}", receivedProperties["macAddress"]);
                   Console.WriteLine("Temperature Alert: {0}", receivedProperties["temperatureAlert"]);
                   Console.WriteLine("Deserialized Obj : [BleConverterData]");
                   Console.WriteLine("  DeviceId       : {0}", receivedData.DeviceId);
                   Console.WriteLine("  MessageId      : {0}", receivedData.MessageId);
                   Console.WriteLine("  Temperature    : {0}", receivedData.Temperature);
               }
   
               Console.WriteLine();
           }
       }
   }
   ```

15. <span data-ttu-id="d643b-159">Salvare il file hello come `DotNetPrinterModule.cs` premendo `Ctrl`  +  `Shift`  +  `S`.</span><span class="sxs-lookup"><span data-stu-id="d643b-159">Save hello file as `DotNetPrinterModule.cs` by pressing `Ctrl` + `Shift` + `S`.</span></span>
    - <span data-ttu-id="d643b-160">In hello salvare come finestra di dialogo hello `Save as Type` menu a discesa, seleziona `C# (*.cs;*.csx)`.</span><span class="sxs-lookup"><span data-stu-id="d643b-160">On hello save as dialog box, in hello `Save as Type` dropdown menu, select `C# (*.cs;*.csx)`.</span></span>

16. <span data-ttu-id="d643b-161">Creare un nuovo file denominato `Untitled-1` da premendo hello `Ctrl`  +  `N` chiavi.</span><span class="sxs-lookup"><span data-stu-id="d643b-161">Create a new file called `Untitled-1` by pressing hello `Ctrl` + `N` keys.</span></span>

17. <span data-ttu-id="d643b-162">hello toodeserialize `JSON` oggetto riceviamo hello `BleConverterModule`, copia e Incolla seguenti di hello frammento di codice hello `Untitled-1` file.</span><span class="sxs-lookup"><span data-stu-id="d643b-162">toodeserialize hello `JSON` object that we receive from hello `BleConverterModule`, Copy and paste hello following code snippet into hello `Untitled-1` file.</span></span> 

   ```csharp
   using System;
   using Newtonsoft.Json;

   namespace PrinterModule
   {
       public class BleConverterData
       {
           [JsonProperty(PropertyName = "deviceId")]
           public string DeviceId { get; set; }
   
           [JsonProperty(PropertyName = "messageId")]
           public string MessageId { get; set; }
   
           [JsonProperty(PropertyName = "temperature")]
           public string Temperature { get; set; }
       }
   }
   ```

18. <span data-ttu-id="d643b-163">Salvare il file hello come `BleConverterData.cs` premendo `Ctrl`  +  `Shift`  +  `S`.</span><span class="sxs-lookup"><span data-stu-id="d643b-163">Save hello file as `BleConverterData.cs` by pressing `Ctrl` + `Shift` + `S`.</span></span>
    - <span data-ttu-id="d643b-164">In hello salvare come finestra di dialogo hello `Save as Type` menu a discesa, seleziona `C# (*.cs;*.csx)`.</span><span class="sxs-lookup"><span data-stu-id="d643b-164">On hello save as dialog box, in hello `Save as Type` dropdown menu, select `C# (*.cs;*.csx)`.</span></span>

19. <span data-ttu-id="d643b-165">Creare un nuovo file denominato `Untitled-1` da premendo hello `Ctrl`  +  `N` chiavi.</span><span class="sxs-lookup"><span data-stu-id="d643b-165">Create a new file called `Untitled-1` by pressing hello `Ctrl` + `N` keys.</span></span>

20. <span data-ttu-id="d643b-166">Copiare e incollare hello seguente frammento di codice in hello `Untitled-1` file.</span><span class="sxs-lookup"><span data-stu-id="d643b-166">Copy and paste hello following code snippet into hello `Untitled-1` file.</span></span>

   ```json
   {
       "loaders": [
           {
               "type": "dotnetcore",
               "name": "dotnetcore",
               "configuration": {
                   "binding.path": "dotnetcore.dll",
                   "binding.coreclrpath": "C:\\Program Files\\dotnet\\shared\\Microsoft.NETCore.App\\1.1.1\\coreclr.dll",
                   "binding.trustedplatformassemblieslocation": "C:\\Program Files\\dotnet\\shared\\Microsoft.NETCore.App\\1.1.1\\"
               }
           }
       ],
          "modules": [
           {
               "name": "simulated_device",
               "loader": {
                   "name": "native",
                   "entrypoint": {
                       "module.path": "simulated_device.dll"
                   }
               },
               "args": {
                   "macAddress": "01:02:03:03:02:01",
                   "messagePeriod": 500
               }
           },
           {
               "name": "ble_converter_module",
               "loader": {
                   "name": "dotnetcore",
                   "entrypoint": {
                       "assembly.name": "IoTEdgeConverterModule",
                       "entry.type": "IoTEdgeConverterModule.BleConverterModule"
                   }
               },
               "args": ""
           },
           {
               "name": "printer_module",
               "loader": {
                   "name": "dotnetcore",
                   "entrypoint": {
                       "assembly.name": "IoTEdgeConverterModule",
                       "entry.type": "PrinterModule.DotNetPrinterModule"
                   }
               },
               "args": ""
           }
       ],
       "links": [
           {
               "source": "simulated_device", "sink": "ble_converter_module"
           },
           {
               "source": "ble_converter_module", "sink": "printer_module"
           }
   ]
   }
   ```

21. <span data-ttu-id="d643b-167">Salvare il file hello come `gw-config.json` premendo `Ctrl`  +  `Shift`  +  `S`.</span><span class="sxs-lookup"><span data-stu-id="d643b-167">Save hello file as `gw-config.json` by pressing `Ctrl` + `Shift` + `S`.</span></span>
    - <span data-ttu-id="d643b-168">In hello salvare come finestra di dialogo hello `Save as Type` menu a discesa, seleziona `JSON (*.json;*.bowerrc;*.jshintrc;*.jscsrc;*.eslintrc;*.babelrc;*webmanifest)`.</span><span class="sxs-lookup"><span data-stu-id="d643b-168">On hello save as dialog box, in hello `Save as Type` dropdown menu, select `JSON (*.json;*.bowerrc;*.jshintrc;*.jscsrc;*.eslintrc;*.babelrc;*webmanifest)`.</span></span>

22. <span data-ttu-id="d643b-169">tooenable copia di toohello file di configurazione hello output directory, hello aggiornamento `IoTEdgeConverterModule.csproj` con hello blob XML seguente:</span><span class="sxs-lookup"><span data-stu-id="d643b-169">tooenable copying of hello configuration file toohello output directory, update hello `IoTEdgeConverterModule.csproj` with hello following XML blob:</span></span>

   ```xml
     <ItemGroup>
       <None Update="gw-config.json" CopyToOutputDirectory="PreserveNewest" />
     </ItemGroup>
   ```
    
   - <span data-ttu-id="d643b-170">Hello aggiornato `IoTEdgeConverterModule.csproj` deve hello l'aspetto seguente immagine:</span><span class="sxs-lookup"><span data-stu-id="d643b-170">hello updated `IoTEdgeConverterModule.csproj` should look like hello following image:</span></span>

    ![File con estensione csproj aggiornato di Visual Studio Code](media/iot-hub-iot-edge-create-module/vscode-update-csproj.png)

23. <span data-ttu-id="d643b-172">Creare un nuovo file denominato `Untitled-1` da premendo hello `Ctrl`  +  `N` chiavi.</span><span class="sxs-lookup"><span data-stu-id="d643b-172">Create a new file called `Untitled-1` by pressing hello `Ctrl` + `N` keys.</span></span>

24. <span data-ttu-id="d643b-173">Copiare e incollare hello seguente frammento di codice in hello `Untitled-1` file.</span><span class="sxs-lookup"><span data-stu-id="d643b-173">Copy and paste hello following code snippet into hello `Untitled-1` file.</span></span>

   ```powershell
   Copy-Item -Path $env:userprofile\.nuget\packages\microsoft.azure.devices.gateway.native.windows.x64\1.1.3\runtimes\win-x64\native\* -Destination .\bin\Debug\netstandard1.3
   Copy-Item -Path $env:userprofile\.nuget\packages\system.runtime.serialization.formatters\4.3.0\lib\netstandard1.4\* -Destination .\bin\Debug\netstandard1.3
   Copy-Item -Path $env:userprofile\.nuget\packages\system.runtime.serialization.primitives\4.3.0\lib\netstandard1.3\* -Destination .\bin\Debug\netstandard1.3
   Copy-Item -Path $env:userprofile\.nuget\packages\newtonsoft.json\10.0.2\lib\netstandard1.3\* -Destination .\bin\Debug\netstandard1.3
   Copy-Item -Path $env:userprofile\.nuget\packages\system.componentmodel.typeconverter\4.3.0\lib\netstandard1.5\* -Destination .\bin\Debug\netstandard1.3
   Copy-Item -Path $env:userprofile\.nuget\packages\system.collections.nongeneric\4.3.0\lib\netstandard1.3\* -Destination .\bin\Debug\netstandard1.3
   Copy-Item -Path $env:userprofile\.nuget\packages\system.collections.specialized\4.3.0\lib\netstandard1.3\* -Destination .\bin\Debug\netstandard1.3
   ```

25. <span data-ttu-id="d643b-174">Salvare il file hello come `binplace.ps1` premendo `Ctrl`  +  `Shift`  +  `S`.</span><span class="sxs-lookup"><span data-stu-id="d643b-174">Save hello file as `binplace.ps1` by pressing `Ctrl` + `Shift` + `S`.</span></span>
    - <span data-ttu-id="d643b-175">In hello salvare come finestra di dialogo hello `Save as Type` menu a discesa, seleziona `PowerShell (*.ps1;*.psm1;*.psd1;*.pssc;*.psrc)`.</span><span class="sxs-lookup"><span data-stu-id="d643b-175">On hello save as dialog box, in hello `Save as Type` dropdown menu, select `PowerShell (*.ps1;*.psm1;*.psd1;*.pssc;*.psrc)`.</span></span>

26. <span data-ttu-id="d643b-176">Compilare il progetto hello premendo hello `Ctrl`  +  `Shift`  +  `B` chiavi.</span><span class="sxs-lookup"><span data-stu-id="d643b-176">Build hello project by pressing hello `Ctrl` + `Shift` + `B` keys.</span></span> <span data-ttu-id="d643b-177">Quando si compila il progetto di hello hello per la prima volta, `Visual Studio Code` viene chiesto di hello `No build task defined.` finestra di dialogo come illustrato nella seguente immagine hello:</span><span class="sxs-lookup"><span data-stu-id="d643b-177">When you build hello project for hello first time, `Visual Studio Code` prompts you with hello `No build task defined.` dialog as seen in hello following image:</span></span>

    ![Finestra di dialogo dell'attività di compilazione di Visual Studio Code](media/iot-hub-iot-edge-create-module/vscode-build-task.png)

    <span data-ttu-id="d643b-179">a) fare clic su hello `Configure Build Task` pulsante.</span><span class="sxs-lookup"><span data-stu-id="d643b-179">a) Click hello `Configure Build Task` button.</span></span>

    <span data-ttu-id="d643b-180">b) in hello `Select a Task Runner` menu a discesa di finestra di dialogo.</span><span class="sxs-lookup"><span data-stu-id="d643b-180">b) In hello `Select a Task Runner` dialog dropdown menu.</span></span> <span data-ttu-id="d643b-181">Selezionare `.NET Core` come illustrato nella seguente immagine hello:</span><span class="sxs-lookup"><span data-stu-id="d643b-181">Select `.NET Core` as seen in hello following image:</span></span> 

    ![Finestra di dialogo di selezione di un'attività di Visual Studio Code](media/iot-hub-iot-edge-create-module/vscode-build-task-runner.png)

    <span data-ttu-id="d643b-183">c) facendo clic su hello `.NET Core` elemento crea hello `tasks.json` file nel `.vscode` directory e quindi apre hello file hello `code editor` finestra.</span><span class="sxs-lookup"><span data-stu-id="d643b-183">c) Clicking hello `.NET Core` item creates hello `tasks.json` file in your `.vscode` directory and opens hello file in hello `code editor` window.</span></span> <span data-ttu-id="d643b-184">Non è alcuna necessità toomodify questo file, scheda hello Chiudi.</span><span class="sxs-lookup"><span data-stu-id="d643b-184">There is no need toomodify this file, close hello tab.</span></span>

27.  <span data-ttu-id="d643b-185">Aprire hello `Visual Studio Code` integrata finestra terminal premendo hello `Ctrl`  +  `backtick` chiavi o utilizzando i menu hello `View`  ->  `Integrated Terminal` e tipo **.\binplace.ps1**in hello `PowerShell` prompt dei comandi.</span><span class="sxs-lookup"><span data-stu-id="d643b-185">Open hello `Visual Studio Code` integrated terminal window by pressing hello `Ctrl` + `backtick` keys or using hello menus `View` -> `Integrated Terminal` and type **.\binplace.ps1** into hello `PowerShell` command prompt.</span></span> <span data-ttu-id="d643b-186">Questo comando Copia tutti i nostri dipendenze toohello la directory di output.</span><span class="sxs-lookup"><span data-stu-id="d643b-186">This command copies all our dependencies toohello output directory.</span></span>

28. <span data-ttu-id="d643b-187">Passare toohello progetti di directory di output di hello `Integrated Terminal` finestra digitando **.\bin\Debug\netstandard1.3 cd**.</span><span class="sxs-lookup"><span data-stu-id="d643b-187">Navigate toohello projects output directory in hello `Integrated Terminal` window by typing **cd .\bin\Debug\netstandard1.3**.</span></span>

29. <span data-ttu-id="d643b-188">Eseguire il progetto di esempio hello digitando **. \gw.exe gw-config. JSON** in hello `Integrated Terminal` finestra.</span><span class="sxs-lookup"><span data-stu-id="d643b-188">Run hello sample project by typing **.\gw.exe gw-config.json** into hello `Integrated Terminal` window prompt.</span></span> 
    - <span data-ttu-id="d643b-189">Se è stata seguita strettamente passaggi hello in questa esercitazione, si dovrebbe ora essere in esecuzione hello `Azure IoT Edge BLE Data Converter Module` progetto di esempio come illustrato nella seguente immagine hello:</span><span class="sxs-lookup"><span data-stu-id="d643b-189">If you have followed hello steps in this tutorial closely, you should now be running hello `Azure IoT Edge BLE Data Converter Module` sample project as seen in hello following image:</span></span>
    
        ![Esempio di dispositivo simulato in esecuzione in Visual Studio Code](media/iot-hub-iot-edge-create-module/vscode-run.png)
    
    - <span data-ttu-id="d643b-191">Se si desidera un'applicazione hello tooterminate, premere hello `<Enter>` chiave.</span><span class="sxs-lookup"><span data-stu-id="d643b-191">If you want tooterminate hello application, press hello `<Enter>` key.</span></span>

>[!IMPORTANT]
<span data-ttu-id="d643b-192">Non è consigliabile toouse `Ctrl`  +  `C` tooterminate hello `IoT Edge` applicazione gateway (vale a dire **gw.exe**).</span><span class="sxs-lookup"><span data-stu-id="d643b-192">It is not recommended toouse `Ctrl` + `C` tooterminate hello `IoT Edge` gateway application (that is, **gw.exe**).</span></span> <span data-ttu-id="d643b-193">Poiché questa operazione potrebbe causare tooterminate processo hello in modo anomalo.</span><span class="sxs-lookup"><span data-stu-id="d643b-193">As this action may cause hello process tooterminate abnormally.</span></span>


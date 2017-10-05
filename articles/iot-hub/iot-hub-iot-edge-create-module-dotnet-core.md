---
title: Creare un modulo Azure IoT Edge con C# | Microsoft Docs
description: "Questa esercitazione illustra come scrivere un modulo convertitore di dati BLE usando i pacchetti NuGet di Azure IoT Edge più recenti, Visual Studio Code e C#."
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
ms.openlocfilehash: 7175ffc8de2c043593d61143b402484d33e4a8cc
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/03/2017
---
# <a name="create-an-azure-iot-edge-module-with-cx23"></a><span data-ttu-id="f8282-104">Creare un modulo Azure IoT Edge con C&#x23;</span><span class="sxs-lookup"><span data-stu-id="f8282-104">Create an Azure IoT Edge Module with C&#x23;</span></span>

<span data-ttu-id="f8282-105">Questa esercitazione illustra come creare un modulo per `Azure IoT Edge` usando `Visual Studio Code` e `C#`.</span><span class="sxs-lookup"><span data-stu-id="f8282-105">This tutorial showcases how to create a module for `Azure IoT Edge` using `Visual Studio Code` and `C#`.</span></span>

<span data-ttu-id="f8282-106">L'esercitazione illustra i passaggi per configurare l'ambiente e spiega come scrivere un modulo convertitore di dati [BLE](https://en.wikipedia.org/wiki/Bluetooth_Low_Energy) con la versione più recente dei pacchetti `Azure IoT Edge NuGet`.</span><span class="sxs-lookup"><span data-stu-id="f8282-106">In this tutorial, we walk through environment set-up and how to write a [BLE](https://en.wikipedia.org/wiki/Bluetooth_Low_Energy) data converter module using the latest `Azure IoT Edge NuGet` packages.</span></span> 

>[!NOTE]
<span data-ttu-id="f8282-107">L'esercitazione usa `.NET Core SDK`, che supporta la compatibilità multipiattaforma.</span><span class="sxs-lookup"><span data-stu-id="f8282-107">This tutorial is using the `.NET Core SDK`, which supports cross-platform compatibility.</span></span> <span data-ttu-id="f8282-108">L'esercitazione seguente è scritta usando il sistema operativo `Windows 10`.</span><span class="sxs-lookup"><span data-stu-id="f8282-108">The following tutorial is written using the `Windows 10` operating system.</span></span> <span data-ttu-id="f8282-109">Alcuni dei comandi in questa esercitazione potrebbero variare a seconda del `development environment` in uso.</span><span class="sxs-lookup"><span data-stu-id="f8282-109">Some of the commands in this tutorial may be different depending on your `development environment`.</span></span> 

## <a name="prerequisites"></a><span data-ttu-id="f8282-110">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="f8282-110">Prerequisites</span></span>

<span data-ttu-id="f8282-111">In questa sezione si configura l'ambiente per lo sviluppo del modulo `Azure IoT Edge`.</span><span class="sxs-lookup"><span data-stu-id="f8282-111">In this section, we set-up your environment for `Azure IoT Edge` module development.</span></span> <span data-ttu-id="f8282-112">Si applica sia a **Windows a 64 bit** che a **Linux a 64 bit (Ubuntu/Debian 8)**.</span><span class="sxs-lookup"><span data-stu-id="f8282-112">It applies to both **64-bit Windows** and **64-bit Linux (Ubuntu/Debian 8)** operating systems.</span></span>

<span data-ttu-id="f8282-113">È richiesto il software seguente:</span><span class="sxs-lookup"><span data-stu-id="f8282-113">The following software is required:</span></span>

- [<span data-ttu-id="f8282-114">Client Git</span><span class="sxs-lookup"><span data-stu-id="f8282-114">Git Client</span></span>](https://git-scm.com/downloads)
- [<span data-ttu-id="f8282-115">ASP.NET Core SDK</span><span class="sxs-lookup"><span data-stu-id="f8282-115">.NET Core SDK</span></span>](https://www.microsoft.com/net/core#windowscmd)
- [<span data-ttu-id="f8282-116">Visual Studio Code</span><span class="sxs-lookup"><span data-stu-id="f8282-116">Visual Studio Code</span></span>](https://code.visualstudio.com/)

<span data-ttu-id="f8282-117">Non è necessario clonare il repository per questo esempio, comunque tutto il codice di esempio illustrato in questa esercitazione si trova nel repository seguente:</span><span class="sxs-lookup"><span data-stu-id="f8282-117">You do not need to clone the repo for this sample, however all of the sample code discussed in this tutorial is located in the following repository:</span></span>

- <span data-ttu-id="f8282-118">`git clone https://github.com/Azure-Samples/iot-edge-samples.git`.</span><span class="sxs-lookup"><span data-stu-id="f8282-118">`git clone https://github.com/Azure-Samples/iot-edge-samples.git`.</span></span>
- `cd iot-edge-samples/dotnetcore/simulated_ble`

## <a name="getting-started"></a><span data-ttu-id="f8282-119">Introduzione</span><span class="sxs-lookup"><span data-stu-id="f8282-119">Getting started</span></span>

1. <span data-ttu-id="f8282-120">Installare `.NET Core SDK`.</span><span class="sxs-lookup"><span data-stu-id="f8282-120">Install `.NET Core SDK`.</span></span>
2. <span data-ttu-id="f8282-121">Installare `Visual Studio Code` e la `C# extension` dal Visual Studio Code Marketplace.</span><span class="sxs-lookup"><span data-stu-id="f8282-121">Install `Visual Studio Code` and the `C# extension` from the Visual Studio Code Marketplace.</span></span>

<span data-ttu-id="f8282-122">Vedere questo [video di esercitazione rapida](https://channel9.msdn.com/Blogs/dotnet/Get-started-VSCode-Csharp-NET-Core-Windows) di introduzione all'utilizzo di `Visual Studio Code` e della `.NET Core SDK`.</span><span class="sxs-lookup"><span data-stu-id="f8282-122">View this [quick video tutorial](https://channel9.msdn.com/Blogs/dotnet/Get-started-VSCode-Csharp-NET-Core-Windows) about how to get started using `Visual Studio Code` and the `.NET Core SDK`.</span></span>

## <a name="creating-the-azure-iot-edge-converter-module"></a><span data-ttu-id="f8282-123">Creazione del modulo convertitore di Azure IoT Edge</span><span class="sxs-lookup"><span data-stu-id="f8282-123">Creating the Azure IoT Edge converter module</span></span>

1. <span data-ttu-id="f8282-124">Inizializzare un nuovo progetto C# di libreria di classi `.NET Core`:</span><span class="sxs-lookup"><span data-stu-id="f8282-124">Initialize a new `.NET Core` class library C# project:</span></span>
    - <span data-ttu-id="f8282-125">Aprire il prompt dei comandi (`Windows + R` -> `cmd` -> `enter`).</span><span class="sxs-lookup"><span data-stu-id="f8282-125">Open a command prompt (`Windows + R` -> `cmd` -> `enter`).</span></span>
    - <span data-ttu-id="f8282-126">Passare alla cartella in cui si desidera creare il progetto `C#`.</span><span class="sxs-lookup"><span data-stu-id="f8282-126">Navigate to the folder where you'd like to create the `C#` project.</span></span>
    - <span data-ttu-id="f8282-127">Digitare **dotnet new classlib -o IoTEdgeConverterModule -f netstandard1.3**.</span><span class="sxs-lookup"><span data-stu-id="f8282-127">Type **dotnet new classlib -o IoTEdgeConverterModule -f netstandard1.3**.</span></span> 
    - <span data-ttu-id="f8282-128">Questo comando crea una classe vuota denominata `Class1.cs` nella directory dei progetti.</span><span class="sxs-lookup"><span data-stu-id="f8282-128">This command creates an empty class called `Class1.cs` in your projects directory.</span></span>
2. <span data-ttu-id="f8282-129">Passare alla cartella in cui si è appena creato il progetto libreria di classi digitando **cd IoTEdgeConverterModule**.</span><span class="sxs-lookup"><span data-stu-id="f8282-129">Navigate to the folder where we just created the class library project by typing **cd IoTEdgeConverterModule**.</span></span>
3. <span data-ttu-id="f8282-130">Aprire il progetto in `Visual Studio Code` digitando **code .**.</span><span class="sxs-lookup"><span data-stu-id="f8282-130">Open the project in `Visual Studio Code` by typing **code .**.</span></span>
4. <span data-ttu-id="f8282-131">Dopo avere aperto il progetto in `Visual Studio Code`, fare clic su **IoTEdgeConverterModule.csproj** per aprire il file come illustrato nell'immagine seguente:</span><span class="sxs-lookup"><span data-stu-id="f8282-131">Once the project is opened in `Visual Studio Code`, click on the **IoTEdgeConverterModule.csproj** to open the file as shown in the following image:</span></span>

    ![Finestra di modifica di Visual Studio Code](media/iot-hub-iot-edge-create-module/vscode-edit-csproj.png)

5. <span data-ttu-id="f8282-133">Inserire il BLOB `XML` mostrato nel frammento di codice seguente tra i tag di chiusura `PropertyGroup` e `Project`, riga sei nell'immagine precedente e salvare il file premendo `Ctrl` + `S`.</span><span class="sxs-lookup"><span data-stu-id="f8282-133">Insert the `XML` blob shown in the following code snippet between the closing `PropertyGroup` tag and the closing `Project` tag; line six in the preceding image and save the file by pressing `Ctrl` + `S`.</span></span>

   ```xml
     <ItemGroup>
       <PackageReference Include="Microsoft.Azure.Devices.Gateway.Module.NetStandard" Version="1.0.5" />
       <PackageReference Include="System.Threading.Thread" Version="4.3.0" />
       <PackageReference Include="Newtonsoft.Json" Version="10.0.2" />
     </ItemGroup> 
   ```

6. <span data-ttu-id="f8282-134">Dopo avere salvato il file con estensione `.csproj`, `Visual Studio Code` dovrebbe visualizzare una finestra `unresolved dependencies` come mostrato nell'immagine seguente:</span><span class="sxs-lookup"><span data-stu-id="f8282-134">Once you save the `.csproj` file, `Visual Studio Code` should prompt you with an `unresolved dependencies` dialog as seen in the following image:</span></span> 

    ![Finestra di Visual Studio Code per il ripristino delle dipendenze](media/iot-hub-iot-edge-create-module/vscode-restore.png)

    <span data-ttu-id="f8282-136">a) Fare clic su `Restore` per ripristinare tutti i riferimenti nel file `.csproj` di progetto, inclusi i `PackageReferences` precedentemente aggiunti.</span><span class="sxs-lookup"><span data-stu-id="f8282-136">a) Click `Restore` to restore all of the references in the projects `.csproj` file including the `PackageReferences` we have added.</span></span> 

    <span data-ttu-id="f8282-137">b) `Visual Studio Code` crea automaticamente il file `project.assets.json` nella cartella `obj` di progetto.</span><span class="sxs-lookup"><span data-stu-id="f8282-137">b) `Visual Studio Code` automatically creates the `project.assets.json` file in your projects `obj` folder.</span></span> <span data-ttu-id="f8282-138">Questo file contiene informazioni sulle dipendenze del progetto allo scopo di rendere più veloci i ripristini successivi.</span><span class="sxs-lookup"><span data-stu-id="f8282-138">This file contains information about your project's dependencies to make subsequent restores quicker.</span></span>
 
    >[!NOTE]
    <span data-ttu-id="f8282-139">`.NET Core Tools`sono ora basati su MSBuild.</span><span class="sxs-lookup"><span data-stu-id="f8282-139">`.NET Core Tools` are now MSBuild-based.</span></span> <span data-ttu-id="f8282-140">Ciò significa che viene creato un file di progetto `.csproj` anziché un file `project.json`.</span><span class="sxs-lookup"><span data-stu-id="f8282-140">Which means a `.csproj` project file is created instead of a `project.json`.</span></span>

    - <span data-ttu-id="f8282-141">Se `Visual Studio Code` non riesce a crearlo automaticamente, è possibile eseguire l'operazione manualmente.</span><span class="sxs-lookup"><span data-stu-id="f8282-141">If `Visual Studio Code` does not prompt you that is ok, we can do it manually.</span></span> <span data-ttu-id="f8282-142">Aprire la finestra Terminale integrato di `Visual Studio Code` premendo `Ctrl` + `backtick` o usando i menu `View` -> `Integrated Terminal`.</span><span class="sxs-lookup"><span data-stu-id="f8282-142">Open the `Visual Studio Code` integrated terminal window by pressing the `Ctrl` + `backtick` keys or using the menus `View` -> `Integrated Terminal`.</span></span>
    - <span data-ttu-id="f8282-143">Nella finestra `Integrated Terminal` digitare **dotnet restore**.</span><span class="sxs-lookup"><span data-stu-id="f8282-143">In the `Integrated Terminal` window type **dotnet restore**.</span></span>
    
7. <span data-ttu-id="f8282-144">Rinominare il file `Class1.cs` in `BleConverterModule.cs`.</span><span class="sxs-lookup"><span data-stu-id="f8282-144">Rename the `Class1.cs` file to `BleConverterModule.cs`.</span></span> 

    <span data-ttu-id="f8282-145">a) Per rinominare il file fare prima clic sul file e quindi premere `F2`.</span><span class="sxs-lookup"><span data-stu-id="f8282-145">a) To rename the file first click on the file then press the `F2` key.</span></span>
    
    <span data-ttu-id="f8282-146">b) Digitare il nuovo nome **BleConverterModule**, come mostrato nell'immagine seguente:</span><span class="sxs-lookup"><span data-stu-id="f8282-146">b) Type in the new name **BleConverterModule**, as seen in the following image:</span></span>

    ![Assegnazione di un nuovo nome a una classe da parte di Visual Studio Code](media/iot-hub-iot-edge-create-module/vscode-rename.png)

8. <span data-ttu-id="f8282-148">Sostituire il codice esistente nel file `BleConverterModule.cs` copiando e incollando il frammento di codice seguente nel file `BleConverterModule.cs`.</span><span class="sxs-lookup"><span data-stu-id="f8282-148">Replace the existing code in the `BleConverterModule.cs` file by copying and pasting the following code snippet into your `BleConverterModule.cs` file.</span></span>

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

9. <span data-ttu-id="f8282-149">Salvare il file premendo `Ctrl` + `S`.</span><span class="sxs-lookup"><span data-stu-id="f8282-149">Save the file by pressing `Ctrl` + `S`.</span></span>

10. <span data-ttu-id="f8282-150">Creare un nuovo file denominato `Untitled-1` premendo `Ctrl` + `N` come mostrato nell'immagine seguente:</span><span class="sxs-lookup"><span data-stu-id="f8282-150">Create a new file called `Untitled-1` by pressing the `Ctrl` + `N` keys as seen in the following image:</span></span>

    ![Nuovo file di Visual Studio Code](media/iot-hub-iot-edge-create-module/vscode-new-file.png)

11. <span data-ttu-id="f8282-152">Per deserializzare l'oggetto `JSON` che si riceve dal dispositivo `BLE` simulato, copiare il codice seguente nella finestra dell'editor di codice del file `Untitled-1`.</span><span class="sxs-lookup"><span data-stu-id="f8282-152">To deserialize the `JSON` object that we receive from the simulated `BLE` device, copy the following code into the `Untitled-1` file code editor window.</span></span> 

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

12. <span data-ttu-id="f8282-153">Salvare il file come `BleData.cs` premendo `Ctrl` + `Shift` + `S`.</span><span class="sxs-lookup"><span data-stu-id="f8282-153">Save the file as `BleData.cs` by pressing `Ctrl` + `Shift` + `S` keys.</span></span>
    - <span data-ttu-id="f8282-154">Nel menu a discesa `Save as Type` della finestra di dialogo Salva con nome selezionare `C# (*.cs;*.csx)` come mostrato nell'immagine seguente:</span><span class="sxs-lookup"><span data-stu-id="f8282-154">On the save as dialog box, in the `Save as Type` dropdown menu, select `C# (*.cs;*.csx)` as seen in the following image:</span></span>

    ![Finestra di dialogo Salva con nome di Visual Studio Code](media/iot-hub-iot-edge-create-module/vscode-save-as.png)

13. <span data-ttu-id="f8282-156">Creare un nuovo file denominato `Untitled-1` premendo `Ctrl` + `N`.</span><span class="sxs-lookup"><span data-stu-id="f8282-156">Create a new file called `Untitled-1` by pressing the `Ctrl` + `N` keys.</span></span>

14. <span data-ttu-id="f8282-157">Copiare e incollare il frammento di codice seguente nel file `Untitled-1`.</span><span class="sxs-lookup"><span data-stu-id="f8282-157">Copy and paste the following code snippet into the `Untitled-1` file.</span></span> <span data-ttu-id="f8282-158">Questa classe è un modulo di `Azure IoT Edge` che si usa per produrre i dati ricevuti dal `BleConverterModule`.</span><span class="sxs-lookup"><span data-stu-id="f8282-158">This class is a `Azure IoT Edge` module, which we use to output the data received from our `BleConverterModule`.</span></span>

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

15. <span data-ttu-id="f8282-159">Salvare il file come `DotNetPrinterModule.cs` premendo `Ctrl` + `Shift` + `S`.</span><span class="sxs-lookup"><span data-stu-id="f8282-159">Save the file as `DotNetPrinterModule.cs` by pressing `Ctrl` + `Shift` + `S`.</span></span>
    - <span data-ttu-id="f8282-160">Nel menu a discesa `Save as Type` della finestra di dialogo Salva con nome selezionare `C# (*.cs;*.csx)`.</span><span class="sxs-lookup"><span data-stu-id="f8282-160">On the save as dialog box, in the `Save as Type` dropdown menu, select `C# (*.cs;*.csx)`.</span></span>

16. <span data-ttu-id="f8282-161">Creare un nuovo file denominato `Untitled-1` premendo `Ctrl` + `N`.</span><span class="sxs-lookup"><span data-stu-id="f8282-161">Create a new file called `Untitled-1` by pressing the `Ctrl` + `N` keys.</span></span>

17. <span data-ttu-id="f8282-162">Per deserializzare l'oggetto `JSON` che si riceve da `BleConverterModule`, copiare e incollare il frammento di codice seguente nel file `Untitled-1`.</span><span class="sxs-lookup"><span data-stu-id="f8282-162">To deserialize the `JSON` object that we receive from the `BleConverterModule`, Copy and paste the following code snippet into the `Untitled-1` file.</span></span> 

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

18. <span data-ttu-id="f8282-163">Salvare il file come `BleConverterData.cs` premendo `Ctrl` + `Shift` + `S`.</span><span class="sxs-lookup"><span data-stu-id="f8282-163">Save the file as `BleConverterData.cs` by pressing `Ctrl` + `Shift` + `S`.</span></span>
    - <span data-ttu-id="f8282-164">Nel menu a discesa `Save as Type` della finestra di dialogo Salva con nome selezionare `C# (*.cs;*.csx)`.</span><span class="sxs-lookup"><span data-stu-id="f8282-164">On the save as dialog box, in the `Save as Type` dropdown menu, select `C# (*.cs;*.csx)`.</span></span>

19. <span data-ttu-id="f8282-165">Creare un nuovo file denominato `Untitled-1` premendo `Ctrl` + `N`.</span><span class="sxs-lookup"><span data-stu-id="f8282-165">Create a new file called `Untitled-1` by pressing the `Ctrl` + `N` keys.</span></span>

20. <span data-ttu-id="f8282-166">Copiare e incollare il frammento di codice seguente nel file `Untitled-1`.</span><span class="sxs-lookup"><span data-stu-id="f8282-166">Copy and paste the following code snippet into the `Untitled-1` file.</span></span>

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

21. <span data-ttu-id="f8282-167">Salvare il file come `gw-config.json` premendo `Ctrl` + `Shift` + `S`.</span><span class="sxs-lookup"><span data-stu-id="f8282-167">Save the file as `gw-config.json` by pressing `Ctrl` + `Shift` + `S`.</span></span>
    - <span data-ttu-id="f8282-168">Nel menu a discesa `Save as Type` della finestra di dialogo Salva con nome selezionare `JSON (*.json;*.bowerrc;*.jshintrc;*.jscsrc;*.eslintrc;*.babelrc;*webmanifest)`.</span><span class="sxs-lookup"><span data-stu-id="f8282-168">On the save as dialog box, in the `Save as Type` dropdown menu, select `JSON (*.json;*.bowerrc;*.jshintrc;*.jscsrc;*.eslintrc;*.babelrc;*webmanifest)`.</span></span>

22. <span data-ttu-id="f8282-169">Per abilitare la copia del file di configurazione nella directory di output, aggiornare il file `IoTEdgeConverterModule.csproj` con il BLOB XML seguente:</span><span class="sxs-lookup"><span data-stu-id="f8282-169">To enable copying of the configuration file to the output directory, update the `IoTEdgeConverterModule.csproj` with the following XML blob:</span></span>

   ```xml
     <ItemGroup>
       <None Update="gw-config.json" CopyToOutputDirectory="PreserveNewest" />
     </ItemGroup>
   ```
    
   - <span data-ttu-id="f8282-170">Il file `IoTEdgeConverterModule.csproj` aggiornato dovrebbe essere simile all'immagine seguente:</span><span class="sxs-lookup"><span data-stu-id="f8282-170">The updated `IoTEdgeConverterModule.csproj` should look like the following image:</span></span>

    ![File con estensione csproj aggiornato di Visual Studio Code](media/iot-hub-iot-edge-create-module/vscode-update-csproj.png)

23. <span data-ttu-id="f8282-172">Creare un nuovo file denominato `Untitled-1` premendo `Ctrl` + `N`.</span><span class="sxs-lookup"><span data-stu-id="f8282-172">Create a new file called `Untitled-1` by pressing the `Ctrl` + `N` keys.</span></span>

24. <span data-ttu-id="f8282-173">Copiare e incollare il frammento di codice seguente nel file `Untitled-1`.</span><span class="sxs-lookup"><span data-stu-id="f8282-173">Copy and paste the following code snippet into the `Untitled-1` file.</span></span>

   ```powershell
   Copy-Item -Path $env:userprofile\.nuget\packages\microsoft.azure.devices.gateway.native.windows.x64\1.1.3\runtimes\win-x64\native\* -Destination .\bin\Debug\netstandard1.3
   Copy-Item -Path $env:userprofile\.nuget\packages\system.runtime.serialization.formatters\4.3.0\lib\netstandard1.4\* -Destination .\bin\Debug\netstandard1.3
   Copy-Item -Path $env:userprofile\.nuget\packages\system.runtime.serialization.primitives\4.3.0\lib\netstandard1.3\* -Destination .\bin\Debug\netstandard1.3
   Copy-Item -Path $env:userprofile\.nuget\packages\newtonsoft.json\10.0.2\lib\netstandard1.3\* -Destination .\bin\Debug\netstandard1.3
   Copy-Item -Path $env:userprofile\.nuget\packages\system.componentmodel.typeconverter\4.3.0\lib\netstandard1.5\* -Destination .\bin\Debug\netstandard1.3
   Copy-Item -Path $env:userprofile\.nuget\packages\system.collections.nongeneric\4.3.0\lib\netstandard1.3\* -Destination .\bin\Debug\netstandard1.3
   Copy-Item -Path $env:userprofile\.nuget\packages\system.collections.specialized\4.3.0\lib\netstandard1.3\* -Destination .\bin\Debug\netstandard1.3
   ```

25. <span data-ttu-id="f8282-174">Salvare il file come `binplace.ps1` premendo `Ctrl` + `Shift` + `S`.</span><span class="sxs-lookup"><span data-stu-id="f8282-174">Save the file as `binplace.ps1` by pressing `Ctrl` + `Shift` + `S`.</span></span>
    - <span data-ttu-id="f8282-175">Nel menu a discesa `Save as Type` della finestra di dialogo Salva con nome selezionare `PowerShell (*.ps1;*.psm1;*.psd1;*.pssc;*.psrc)`.</span><span class="sxs-lookup"><span data-stu-id="f8282-175">On the save as dialog box, in the `Save as Type` dropdown menu, select `PowerShell (*.ps1;*.psm1;*.psd1;*.pssc;*.psrc)`.</span></span>

26. <span data-ttu-id="f8282-176">Compilare il progetto premendo `Ctrl` + `Shift` + `B`.</span><span class="sxs-lookup"><span data-stu-id="f8282-176">Build the project by pressing the `Ctrl` + `Shift` + `B` keys.</span></span> <span data-ttu-id="f8282-177">Quando si compila il progetto per la prima volta, `Visual Studio Code` visualizza la finestra di dialogo `No build task defined.` come mostrato nell'immagine seguente:</span><span class="sxs-lookup"><span data-stu-id="f8282-177">When you build the project for the first time, `Visual Studio Code` prompts you with the `No build task defined.` dialog as seen in the following image:</span></span>

    ![Finestra di dialogo dell'attività di compilazione di Visual Studio Code](media/iot-hub-iot-edge-create-module/vscode-build-task.png)

    <span data-ttu-id="f8282-179">a) Fare clic sul pulsante `Configure Build Task`.</span><span class="sxs-lookup"><span data-stu-id="f8282-179">a) Click the `Configure Build Task` button.</span></span>

    <span data-ttu-id="f8282-180">b) Nel menu a discesa `Select a Task Runner` della finestra di dialogo</span><span class="sxs-lookup"><span data-stu-id="f8282-180">b) In the `Select a Task Runner` dialog dropdown menu.</span></span> <span data-ttu-id="f8282-181">selezionare `.NET Core` come mostrato nell'immagine seguente:</span><span class="sxs-lookup"><span data-stu-id="f8282-181">Select `.NET Core` as seen in the following image:</span></span> 

    ![Finestra di dialogo di selezione di un'attività di Visual Studio Code](media/iot-hub-iot-edge-create-module/vscode-build-task-runner.png)

    <span data-ttu-id="f8282-183">c) Se si fa clic sulla voce `.NET Core`, viene creato il file `tasks.json` nella directory `.vscode` e il file viene aperto nella finestra `code editor`.</span><span class="sxs-lookup"><span data-stu-id="f8282-183">c) Clicking the `.NET Core` item creates the `tasks.json` file in your `.vscode` directory and opens the file in the `code editor` window.</span></span> <span data-ttu-id="f8282-184">Non è necessario modificare il file, quindi chiudere la scheda.</span><span class="sxs-lookup"><span data-stu-id="f8282-184">There is no need to modify this file, close the tab.</span></span>

27.  <span data-ttu-id="f8282-185">Aprire la finestra Terminale integrato di `Visual Studio Code` premendo `Ctrl` + `backtick` o usando i menu `View` -> `Integrated Terminal` e digitare **.\binplace.ps1** al prompt dei comandi di `PowerShell`.</span><span class="sxs-lookup"><span data-stu-id="f8282-185">Open the `Visual Studio Code` integrated terminal window by pressing the `Ctrl` + `backtick` keys or using the menus `View` -> `Integrated Terminal` and type **.\binplace.ps1** into the `PowerShell` command prompt.</span></span> <span data-ttu-id="f8282-186">Questo comando copia tutte le dipendenze nella directory di output.</span><span class="sxs-lookup"><span data-stu-id="f8282-186">This command copies all our dependencies to the output directory.</span></span>

28. <span data-ttu-id="f8282-187">Passare alla directory di output dei progetti nella finestra `Integrated Terminal` digitando **cd .\bin\Debug\netstandard1.3**.</span><span class="sxs-lookup"><span data-stu-id="f8282-187">Navigate to the projects output directory in the `Integrated Terminal` window by typing **cd .\bin\Debug\netstandard1.3**.</span></span>

29. <span data-ttu-id="f8282-188">Eseguire il progetto di esempio digitando **.\gw.exe gw-config.json** al prompt della finestra `Integrated Terminal`.</span><span class="sxs-lookup"><span data-stu-id="f8282-188">Run the sample project by typing **.\gw.exe gw-config.json** into the `Integrated Terminal` window prompt.</span></span> 
    - <span data-ttu-id="f8282-189">Se sono stati seguiti attentamente i passaggi dell'esercitazione, si dovrebbe eseguire il progetto di esempio `Azure IoT Edge BLE Data Converter Module` come mostrato nell'immagine seguente:</span><span class="sxs-lookup"><span data-stu-id="f8282-189">If you have followed the steps in this tutorial closely, you should now be running the `Azure IoT Edge BLE Data Converter Module` sample project as seen in the following image:</span></span>
    
        ![Esempio di dispositivo simulato in esecuzione in Visual Studio Code](media/iot-hub-iot-edge-create-module/vscode-run.png)
    
    - <span data-ttu-id="f8282-191">Se si intende terminare l'applicazione premere `<Enter>`.</span><span class="sxs-lookup"><span data-stu-id="f8282-191">If you want to terminate the application, press the `<Enter>` key.</span></span>

>[!IMPORTANT]
<span data-ttu-id="f8282-192">Non è consigliabile usare `Ctrl` + `C` per terminare l'applicazione gateway `IoT Edge` (vale a dire **gw.exe**)</span><span class="sxs-lookup"><span data-stu-id="f8282-192">It is not recommended to use `Ctrl` + `C` to terminate the `IoT Edge` gateway application (that is, **gw.exe**).</span></span> <span data-ttu-id="f8282-193">in quanto questa azione può determinare un arresto anomalo del processo.</span><span class="sxs-lookup"><span data-stu-id="f8282-193">As this action may cause the process to terminate abnormally.</span></span>


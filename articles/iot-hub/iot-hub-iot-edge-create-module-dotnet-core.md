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
# <a name="create-an-azure-iot-edge-module-with-cx23"></a>Creare un modulo Azure IoT Edge con C&#x23;

In questa esercitazione illustra come toocreate un modulo per `Azure IoT Edge` utilizzando `Visual Studio Code` e `C#`.

In questa esercitazione vengono illustrate le impostazione di ambiente e come toowrite un [BILITA](https://en.wikipedia.org/wiki/Bluetooth_Low_Energy) modulo convertitore di tipi di dati tramite hello più recente `Azure IoT Edge NuGet` pacchetti. 

>[!NOTE]
In questa esercitazione Usa hello `.NET Core SDK`, che supporta compatibilità multipiattaforma. Hello esercitazione seguente viene scritto utilizzando hello `Windows 10` del sistema operativo. Alcuni dei comandi di hello in questa esercitazione potrebbero essere diverse a seconda del `development environment`. 

## <a name="prerequisites"></a>Prerequisiti

In questa sezione si configura l'ambiente per lo sviluppo del modulo `Azure IoT Edge`. Si applica tooboth **Windows a 64 bit** e **Linux a 64 bit (8 Ubuntu/Debian)** i sistemi operativi.

Hello seguente software è necessario:

- [Client Git](https://git-scm.com/downloads)
- [ASP.NET Core SDK](https://www.microsoft.com/net/core#windowscmd)
- [Visual Studio Code](https://code.visualstudio.com/)

Non è necessario repository hello tooclone per questo esempio, tuttavia tutte hello esempi di codice illustrati in questa esercitazione si trova nella seguente repository hello:

- `git clone https://github.com/Azure-Samples/iot-edge-samples.git`.
- `cd iot-edge-samples/dotnetcore/simulated_ble`

## <a name="getting-started"></a>Introduzione

1. Installare `.NET Core SDK`.
2. Installare `Visual Studio Code` hello e `C# extension` da Visual Studio Marketplace di codice hello.

Visualizzare questo [video di esercitazione rapida](https://channel9.msdn.com/Blogs/dotnet/Get-started-VSCode-Csharp-NET-Core-Windows) sulla modalità di avvio utilizzando tooget `Visual Studio Code` hello e `.NET Core SDK`.

## <a name="creating-hello-azure-iot-edge-converter-module"></a>Creazione di hello Azure IoT Edge convertitore modulo

1. Inizializzare un nuovo progetto C# di libreria di classi `.NET Core`:
    - Aprire il prompt dei comandi (`Windows + R` -> `cmd` -> `enter`).
    - Esplorazione delle cartelle toohello in cui si desidera toocreate hello `C#` progetto.
    - Digitare **dotnet new classlib -o IoTEdgeConverterModule -f netstandard1.3**. 
    - Questo comando crea una classe vuota denominata `Class1.cs` nella directory dei progetti.
2. Passare toohello nella cartella in cui è appena creata progetto libreria di classi hello digitando **cd IoTEdgeConverterModule**.
3. Progetto aperto hello in `Visual Studio Code` digitando **codice.**.
4. Una volta hello progetto è aperto in `Visual Studio Code`, fare clic su hello **IoTEdgeConverterModule.csproj** il file hello tooopen come illustrato nella seguente immagine hello:

    ![Finestra di modifica di Visual Studio Code](media/iot-hub-iot-edge-create-module/vscode-edit-csproj.png)

5. Inserisci hello `XML` blob illustrato nel seguente frammento di codice tra chiusura hello hello `PropertyGroup` tag e hello chiusura `Project` tag; riga sei hello immagine precedente e salvare il file hello premendo `Ctrl`  +  `S`.

   ```xml
     <ItemGroup>
       <PackageReference Include="Microsoft.Azure.Devices.Gateway.Module.NetStandard" Version="1.0.5" />
       <PackageReference Include="System.Threading.Thread" Version="4.3.0" />
       <PackageReference Include="Newtonsoft.Json" Version="10.0.2" />
     </ItemGroup> 
   ```

6. Dopo aver salvato hello `.csproj` file `Visual Studio Code` dovrebbe ricevere una richiesta con un `unresolved dependencies` finestra di dialogo come illustrato nella seguente immagine hello: 

    ![Finestra di Visual Studio Code per il ripristino delle dipendenze](media/iot-hub-iot-edge-create-module/vscode-restore.png)

    a) fare clic su `Restore` toorestore tutti di hello i riferimenti nei progetti di hello `.csproj` file incluso hello `PackageReferences` è stato aggiunto. 

    b) `Visual Studio Code` crea automaticamente hello `project.assets.json` file nei progetti `obj` cartella. Questo file contiene informazioni le dipendenze toomake ripristini successivi del progetto più veloce.
 
    >[!NOTE]
    `.NET Core Tools`sono ora basati su MSBuild. Ciò significa che viene creato un file di progetto `.csproj` anziché un file `project.json`.

    - Se `Visual Studio Code` non riesce a crearlo automaticamente, è possibile eseguire l'operazione manualmente. Aprire hello `Visual Studio Code` integrata finestra terminal premendo hello `Ctrl`  +  `backtick` chiavi o utilizzando i menu hello `View`  ->  `Integrated Terminal`.
    - In hello `Integrated Terminal` tipo di finestra **ripristino dotnet**.
    
7. Rinominare hello `Class1.cs` file troppo`BleConverterModule.cs`. 

    ) file hello toorename innanzitutto fare clic sul file hello quindi premere hello `F2` chiave.
    
    b) tipo in un nuovo nome hello **BleConverterModule**, come illustrato nella seguente immagine hello:

    ![Assegnazione di un nuovo nome a una classe da parte di Visual Studio Code](media/iot-hub-iot-edge-create-module/vscode-rename.png)

8. Sostituire il codice esistente in hello hello `BleConverterModule.cs` file da copiare e incollare hello seguente frammento di codice il `BleConverterModule.cs` file.

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

9. Salvare il file hello premendo `Ctrl`  +  `S`.

10. Creare un nuovo file denominato `Untitled-1` da premendo hello `Ctrl`  +  `N` tasti come illustrato nella seguente immagine hello:

    ![Nuovo file di Visual Studio Code](media/iot-hub-iot-edge-create-module/vscode-new-file.png)

11. hello toodeserialize `JSON` oggetto riceviamo hello simulato `BLE` dispositivo, hello copia seguente di codice in hello `Untitled-1` finestra dell'editor di codice file. 

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

12. Salvare il file hello come `BleData.cs` premendo `Ctrl`  +  `Shift`  +  `S` chiavi.
    - In hello salvare come finestra di dialogo hello `Save as Type` menu a discesa, seleziona `C# (*.cs;*.csx)` come illustrato nella seguente immagine hello:

    ![Finestra di dialogo Salva con nome di Visual Studio Code](media/iot-hub-iot-edge-create-module/vscode-save-as.png)

13. Creare un nuovo file denominato `Untitled-1` da premendo hello `Ctrl`  +  `N` chiavi.

14. Copiare e incollare hello seguente frammento di codice in hello `Untitled-1` file. Questa classe è un `Azure IoT Edge` modulo, utilizziamo dati hello toooutput ricevuti dai nostri `BleConverterModule`.

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

15. Salvare il file hello come `DotNetPrinterModule.cs` premendo `Ctrl`  +  `Shift`  +  `S`.
    - In hello salvare come finestra di dialogo hello `Save as Type` menu a discesa, seleziona `C# (*.cs;*.csx)`.

16. Creare un nuovo file denominato `Untitled-1` da premendo hello `Ctrl`  +  `N` chiavi.

17. hello toodeserialize `JSON` oggetto riceviamo hello `BleConverterModule`, copia e Incolla seguenti di hello frammento di codice hello `Untitled-1` file. 

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

18. Salvare il file hello come `BleConverterData.cs` premendo `Ctrl`  +  `Shift`  +  `S`.
    - In hello salvare come finestra di dialogo hello `Save as Type` menu a discesa, seleziona `C# (*.cs;*.csx)`.

19. Creare un nuovo file denominato `Untitled-1` da premendo hello `Ctrl`  +  `N` chiavi.

20. Copiare e incollare hello seguente frammento di codice in hello `Untitled-1` file.

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

21. Salvare il file hello come `gw-config.json` premendo `Ctrl`  +  `Shift`  +  `S`.
    - In hello salvare come finestra di dialogo hello `Save as Type` menu a discesa, seleziona `JSON (*.json;*.bowerrc;*.jshintrc;*.jscsrc;*.eslintrc;*.babelrc;*webmanifest)`.

22. tooenable copia di toohello file di configurazione hello output directory, hello aggiornamento `IoTEdgeConverterModule.csproj` con hello blob XML seguente:

   ```xml
     <ItemGroup>
       <None Update="gw-config.json" CopyToOutputDirectory="PreserveNewest" />
     </ItemGroup>
   ```
    
   - Hello aggiornato `IoTEdgeConverterModule.csproj` deve hello l'aspetto seguente immagine:

    ![File con estensione csproj aggiornato di Visual Studio Code](media/iot-hub-iot-edge-create-module/vscode-update-csproj.png)

23. Creare un nuovo file denominato `Untitled-1` da premendo hello `Ctrl`  +  `N` chiavi.

24. Copiare e incollare hello seguente frammento di codice in hello `Untitled-1` file.

   ```powershell
   Copy-Item -Path $env:userprofile\.nuget\packages\microsoft.azure.devices.gateway.native.windows.x64\1.1.3\runtimes\win-x64\native\* -Destination .\bin\Debug\netstandard1.3
   Copy-Item -Path $env:userprofile\.nuget\packages\system.runtime.serialization.formatters\4.3.0\lib\netstandard1.4\* -Destination .\bin\Debug\netstandard1.3
   Copy-Item -Path $env:userprofile\.nuget\packages\system.runtime.serialization.primitives\4.3.0\lib\netstandard1.3\* -Destination .\bin\Debug\netstandard1.3
   Copy-Item -Path $env:userprofile\.nuget\packages\newtonsoft.json\10.0.2\lib\netstandard1.3\* -Destination .\bin\Debug\netstandard1.3
   Copy-Item -Path $env:userprofile\.nuget\packages\system.componentmodel.typeconverter\4.3.0\lib\netstandard1.5\* -Destination .\bin\Debug\netstandard1.3
   Copy-Item -Path $env:userprofile\.nuget\packages\system.collections.nongeneric\4.3.0\lib\netstandard1.3\* -Destination .\bin\Debug\netstandard1.3
   Copy-Item -Path $env:userprofile\.nuget\packages\system.collections.specialized\4.3.0\lib\netstandard1.3\* -Destination .\bin\Debug\netstandard1.3
   ```

25. Salvare il file hello come `binplace.ps1` premendo `Ctrl`  +  `Shift`  +  `S`.
    - In hello salvare come finestra di dialogo hello `Save as Type` menu a discesa, seleziona `PowerShell (*.ps1;*.psm1;*.psd1;*.pssc;*.psrc)`.

26. Compilare il progetto hello premendo hello `Ctrl`  +  `Shift`  +  `B` chiavi. Quando si compila il progetto di hello hello per la prima volta, `Visual Studio Code` viene chiesto di hello `No build task defined.` finestra di dialogo come illustrato nella seguente immagine hello:

    ![Finestra di dialogo dell'attività di compilazione di Visual Studio Code](media/iot-hub-iot-edge-create-module/vscode-build-task.png)

    a) fare clic su hello `Configure Build Task` pulsante.

    b) in hello `Select a Task Runner` menu a discesa di finestra di dialogo. Selezionare `.NET Core` come illustrato nella seguente immagine hello: 

    ![Finestra di dialogo di selezione di un'attività di Visual Studio Code](media/iot-hub-iot-edge-create-module/vscode-build-task-runner.png)

    c) facendo clic su hello `.NET Core` elemento crea hello `tasks.json` file nel `.vscode` directory e quindi apre hello file hello `code editor` finestra. Non è alcuna necessità toomodify questo file, scheda hello Chiudi.

27.  Aprire hello `Visual Studio Code` integrata finestra terminal premendo hello `Ctrl`  +  `backtick` chiavi o utilizzando i menu hello `View`  ->  `Integrated Terminal` e tipo **.\binplace.ps1**in hello `PowerShell` prompt dei comandi. Questo comando Copia tutti i nostri dipendenze toohello la directory di output.

28. Passare toohello progetti di directory di output di hello `Integrated Terminal` finestra digitando **.\bin\Debug\netstandard1.3 cd**.

29. Eseguire il progetto di esempio hello digitando **. \gw.exe gw-config. JSON** in hello `Integrated Terminal` finestra. 
    - Se è stata seguita strettamente passaggi hello in questa esercitazione, si dovrebbe ora essere in esecuzione hello `Azure IoT Edge BLE Data Converter Module` progetto di esempio come illustrato nella seguente immagine hello:
    
        ![Esempio di dispositivo simulato in esecuzione in Visual Studio Code](media/iot-hub-iot-edge-create-module/vscode-run.png)
    
    - Se si desidera un'applicazione hello tooterminate, premere hello `<Enter>` chiave.

>[!IMPORTANT]
Non è consigliabile toouse `Ctrl`  +  `C` tooterminate hello `IoT Edge` applicazione gateway (vale a dire **gw.exe**). Poiché questa operazione potrebbe causare tooterminate processo hello in modo anomalo.


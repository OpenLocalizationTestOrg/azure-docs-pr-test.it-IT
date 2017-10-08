---
title: aaaEnable Azure Application Insights Profiler su una risorsa di servizi Cloud | Documenti Microsoft
description: Informazioni su come tooset di profiler hello in un'applicazione ASP.NET ospitato da una risorsa di servizi Cloud di Azure.
services: application-insights
documentationcenter: 
author: CFreemanwa
manager: carmonm
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: article
ms.date: 07/25/2017
ms.author: bwren
ms.openlocfilehash: b9ac3bca513bf4518f44780389a9f2945f6ccc98
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="enable-application-insights-profiler-on-an-azure-cloud-services-resource"></a>Abilitare Application Insights Profiler in una risorsa di Servizi cloud di Azure

Questa procedura dettagliata illustra come tooenable Profiler Insights per le applicazioni Azure in un'applicazione ASP.NET ospitato da una risorsa di servizi Cloud di Azure. esempi di Hello includono il supporto per le macchine virtuali di Azure, il set di scalabilità di macchine virtuali e Azure Service Fabric. tutti gli esempi di Hello si basano su modelli che supportano il modello di distribuzione Azure Resource Manager hello. Per ulteriori informazioni sul modello di distribuzione hello, esaminare [Azure Resource Manager e distribuzione classica: comprendere i modelli di distribuzione e lo stato delle risorse di hello](/azure-resource-manager/resource-manager-deployment-model).

## <a name="overview"></a>Panoramica

Hello seguente diagramma illustra il funzionamento di profiler hello per le risorse di servizi Cloud di Azure. Come esempio viene usata una macchina virtuale di Azure.

![Panoramica](./media/enable-profiler-compute/overview.png) hello di toocollect informazioni per l'elaborazione e la visualizzazione sul portale di Azure, è necessario installare il componente Agente di diagnostica hello per le risorse di servizi Cloud di Azure hello. Hello rest hello procedura dettagliata vengono fornite indicazioni su come tooinstall e configurare hello tooenable di agente di diagnostica del Profiler di Application Insights.

## <a name="prerequisites-for-hello-walkthrough"></a>Prerequisiti per questa procedura dettagliata hello

* Un modello di gestione risorse di distribuzione che installa gli agenti di profiler hello in macchine virtuali hello ([WindowsVirtualMachine.json](https://github.com/Azure/azure-docs-json-samples/blob/master/application-insights/WindowsVirtualMachine.json)) o set di scalabilità ([WindowsVirtualMachineScaleSet.json](https://github.com/Azure/azure-docs-json-samples/blob/master/application-insights/WindowsVirtualMachineScaleSet.json)).

* Istanza di Application Insights abilitata per la profilatura. Per istruzioni, vedere [abilitare il profilo di hello](https://docs.microsoft.com/en-us/azure/application-insights/app-insights-profiler#enable-the-profiler).

* Risorsa di servizi Cloud di Azure di destinazione di .NET framework 4.6.1 o versione successiva installato in hello.

## <a name="create-a-resource-group-in-your-azure-subscription"></a>Creare un gruppo di risorse nella sottoscrizione di Azure
Hello di esempio seguente viene illustrato come una risorsa toocreate gruppo usando uno script di PowerShell:

```
New-AzureRmResourceGroup -Name "Replace_With_Resource_Group_Name" -Location "Replace_With_Resource_Group_Location"
```

## <a name="create-an-application-insights-resource-in-hello-resource-group"></a>Creare una risorsa di Application Insights nel gruppo di risorse hello
In hello **Application Insights** pannello, immettere le informazioni di hello per la risorsa, come illustrato nel seguente esempio: 

![Pannello Application Insights](./media/enable-profiler-compute/createai.png)

## <a name="apply-an-application-insights-instrumentation-key-in-hello-azure-resource-manager-template"></a>Applicare una chiave di strumentazione di Application Insights nel modello di gestione risorse di Azure hello

1. Se non è stato scaricato il modello di hello, scaricarlo dal [GitHub](https://github.com/Azure/azure-docs-json-samples/blob/master/application-insights/WindowsVirtualMachine.json).

2. Trovare la chiave di Application Insights hello.
   
   ![Percorso della chiave hello](./media/enable-profiler-compute/copyaikey.png)

3. Sostituire il valore di modello hello.
   
   ![Valore sostituito nel modello hello](./media/enable-profiler-compute/copyaikeytotemplate.png)

## <a name="create-an-azure-vm-toohost-hello-web-application"></a>Creare un'applicazione web di Azure VM toohost hello
1. Creare una password di hello toosave stringa sicura.

   ```
   $password = ConvertTo-SecureString -String "Replace_With_Your_Password" -AsPlainText -Force
   ```

2. Distribuire il modello di gestione risorse di Azure hello.

   Cambiare directory hello in hello PowerShell console toohello cartella contiene il modello di gestione risorse. modello di hello toodeploy, eseguire hello comando seguente:

   ```
   New-AzureRmResourceGroupDeployment -ResourceGroupName "Replace_With_Resource_Group_Name" -TemplateFile .\WindowsVirtualMachine.json -adminUsername "Replace_With_your_user_name" -adminPassword $password -dnsNameForPublicIP "Replace_WIth_your_DNS_Name" -Verbose
   ```

Dopo l'esecuzione dello script di hello è completata, è necessario trovare una macchina virtuale denominata **MyWindowsVM** nel gruppo di risorse.

## <a name="configure-web-deploy-on-hello-vm"></a>Distribuzione Web su hello VM
Assicurarsi che il servizio Distribuzione Web sia abilitato nella VM per poter pubblicare l'applicazione Web da Visual Studio.

tooinstall distribuzione Web in una macchina virtuale manualmente tramite WebPI, vedere [installazione e configurazione di distribuzione Web in IIS 8.0 o successiva](https://docs.microsoft.com/en-us/iis/install/installing-publishing-technologies/installing-and-configuring-web-deploy-on-iis-80-or-later). Per un esempio di come tooautomate installare distribuzione Web utilizzando un modello di gestione risorse di Azure, vedere [creare, configurare e distribuire un tooan di applicazione web Azure VM](https://azure.microsoft.com/en-us/resources/templates/201-web-app-vm-dsc/).

Se si distribuisce un'applicazione ASP.NET MVC, visitare tooServer Manager, selezionare **Aggiungi ruoli e funzionalità** > **Server Web (IIS)** > **Server Web**  >  **Lo sviluppo di applicazioni**e abilitare ASP.NET 4.5 nel server.

![Aggiungere ASP.NET](./media/enable-profiler-compute/addaspnet45.png)

## <a name="install-hello-azure-application-insights-sdk-for-your-project"></a>Installare hello Azure Application Insights SDK per il progetto
1. Aprire l'applicazione Web ASP.NET in Visual Studio.

2. Fare clic sul progetto hello e selezionare **Aggiungi** > **servizi connessi**.

3. Selezionare **Application Insights**.

4. Seguire le istruzioni di hello nella pagina di hello. Selezionare una risorsa di Application Insights hello creato in precedenza.

5. Seleziona hello **registrare** pulsante.


## <a name="publish-hello-project-tooan-azure-vm"></a>Pubblicare hello progetto tooan macchina virtuale di Azure
Esistono diversi modi toopublish un tooan applicazione macchina virtuale di Azure. Un modo consiste toouse 2017 di Visual Studio.

1. Fare clic sul progetto hello e selezionare **pubblica**.

2. Selezionare **macchine virtuali di Microsoft Azure** come hello destinazione di pubblicazione e seguire i passaggi di hello.

   ![Pubblicare da VS](./media/enable-profiler-compute/publishtoVM.png)

3. Eseguire un test di carico sull'applicazione. Si otterranno risultati nella pagina Web del portale di hello Application Insights istanza.


## <a name="enable-hello-profiler"></a>Attivare il profiler hello
1. Passare tooyour Application Insights **prestazioni** pannello e selezionare **configura**.
   
   ![Icona Configura](./media/enable-profiler-compute/enableprofiler1.png)
 
2. Selezionare **Abilita profiler**.
   
   ![Icona Abilita profiler](./media/enable-profiler-compute/enableprofiler2.png)

## <a name="add-a-performance-test-tooyour-application"></a>Aggiungere un'applicazione di tooyour test delle prestazioni
In modo da poter raccogliere alcuni toobe di dati di esempio visualizzati nel Profiler di Application Insights, seguire questi passaggi:

1. Sfoglia risorsa di Application Insights toohello creato in precedenza. 

2. Passare toohello **disponibilità** pannello e aggiungere un test delle prestazioni che invia l'URL dell'applicazione tooyour le richieste web. 

   ![Aggiungere il test delle prestazioni](./media/enable-profiler-compute/AvailabilityTest.png)

## <a name="view-your-performance-data"></a>Visualizzare i dati sulle prestazioni

1. Attendere 10-15 minuti per toocollect profiler hello e analizzare i dati di hello. 

2. Passare toohello **prestazioni** pannello nella risorsa di Application Insights e visualizzazione delle prestazioni dell'applicazione quando è in condizioni di carico.

   ![Visualizzazione delle prestazioni](./media/enable-profiler-compute/aiperformance.png)

3. Icona di hello selezionare sotto **esempi** tooopen hello **visualizzazione traccia** blade.

   ![Aprire il pannello di visualizzazione traccia hello](./media/enable-profiler-compute/traceview.png)


## <a name="work-with-an-existing-template"></a>Utilizzare un modello esistente

1. Individuare una dichiarazione della risorsa di diagnostica Azure hello nel modello di distribuzione.
   
   Se non si dispone di una dichiarazione, è possibile creare una dichiarazione hello nel seguente esempio hello simile. È possibile aggiornare il modello di hello da hello [sito Web di Azure Resource Explorer](https://resources.azure.com).

2. Server di pubblicazione hello modifica da `Microsoft.Azure.Diagnostics` troppo`AIP.Diagnostics.Test`.

3. Per `typeHandlerVersion`, usare `0.0`.

4. Assicurarsi che `autoUpgradeMinorVersion` è troppo`true`.

5. Aggiungi nuova hello `ApplicationInsightsProfiler` istanza sink in hello `WadCfg` oggetto impostazioni, come illustrato nell'esempio seguente hello:

```
"resources": [
        {
          "type": "extensions",
          "name": "Microsoft.Insights.VMDiagnosticsSettings",
          "apiVersion": "2016-03-30",
          "properties": {
            "publisher": "AIP.Diagnostics.Test",
            "type": "IaaSDiagnostics",
            "typeHandlerVersion": "0.0",
            "autoUpgradeMinorVersion": true,
            "settings": {
              "WadCfg": {
                "SinksConfig": {
                  "Sink": [
                    {
                      "name": "Give a descriptive short name. E.g.: MyApplicationInsightsProfilerSink",
                      "ApplicationInsightsProfiler": "Enter hello Application Insights instance instrumentation key guid here"
                    }
                  ]
                },
                "DiagnosticMonitorConfiguration": {
                    ...
                }
                ...
              }
              ...
            }
            ...
          }
          ...
]
```

## <a name="enable-hello-profiler-on-virtual-machine-scale-sets"></a>Attivare il profiler di hello sul set di scalabilità di macchine virtuali
toosee come tooenable hello profiler, download hello [WindowsVirtualMachineScaleSet.json](https://github.com/Azure/azure-docs-json-samples/blob/master/application-insights/WindowsVirtualMachineScaleSet.json) modello. Applicare hello stesso viene modificato in una risorsa di estensione VM modello toohello diagnostica per hello set di scalabilità della macchina virtuale.

Assicurarsi che ogni istanza nel set di scalabilità hello dispone di accesso toohello internet. Hello agente Profiler può quindi inviare i campioni raccolti hello tooApplication Insights per la visualizzazione e analisi.

## <a name="enable-hello-profiler-on-service-fabric-applications"></a>Attivare il profiler hello sulle applicazioni di Service Fabric
1. Hello di effettuare il provisioning dell'infrastruttura del servizio cluster toohave hello Azure estensione di diagnostica che installa l'agente di Profiler hello.

2. Installare Application Insights SDK hello nel progetto hello e configurare la chiave di Application Insights hello.

3. Aggiungere dati di telemetria tooinstrument codice dell'applicazione.

### <a name="provision-hello-service-fabric-cluster-toohave-hello-azure-diagnostics-extension-that-installs-hello-profiler-agent"></a>Eseguire il provisioning hello Service Fabric cluster toohave hello estensione diagnostica di Azure che installa l'agente di Profiler hello
Un cluster di Service Fabric può essere sicuro o non sicuro. È possibile impostare un gateway cluster toobe non protetto e pertanto non richiede un certificato per l'accesso. I cluster che ospitano la logica di business e i dati devono essere sicuri. È possibile attivare il profiler hello nei cluster di Service Fabric protetto e non sicure. Questa procedura dettagliata Usa un cluster di non protetto come un esempio tooexplain quali modifiche sono necessari tooenable hello profiler. È possibile eseguire il provisioning di un cluster protetto in hello allo stesso modo.

1. Scaricare [ServiceFabricCluster.json](https://github.com/Azure/azure-docs-json-samples/blob/master/application-insights/ServiceFabricCluster.json). Come per le VM e i set di scalabilità di macchine virtuali, sostituire `Application_Insights_Key` con la propria chiave di Application Insights:

   ```
   "publisher": "AIP.Diagnostics.Test",
                 "settings": {
                   "WadCfg": {
                     "SinksConfig": {
                       "Sink": [
                         {
                           "name": "MyApplicationInsightsProfilerSinkVMSS",
                           "ApplicationInsightsProfiler": "[Application_Insights_Key]"
                         }
                       ]
                     },
   ```

2. Distribuire il modello di hello usando uno script di PowerShell:

   ```
   Login-AzureRmAccount
   New-AzureRmResourceGroup -Name [Your_Resource_Group_Name] -Location [Your_Resource_Group_Location] -Verbose -Force
   New-AzureRmResourceGroupDeployment -Name [Choose_An_Arbitrary_Name] -ResourceGroupName [Your_Resource_Group_Name] -TemplateFile [Path_To_Your_Template]

   ```

### <a name="install-hello-application-insights-sdk-in-hello-project-and-configure-hello-application-insights-key"></a>Installare Application Insights SDK hello nel progetto hello e configurare la chiave di Application Insights hello
Installare Application Insights SDK hello da hello [pacchetto NuGet](https://www.nuget.org/packages/Microsoft.ApplicationInsights.Web/). Assicurarsi di installare una versione stabile, 2.3 o successiva. 

Per informazioni sulla configurazione di Application Insights nei progetti, vedere [Using Service Fabric with Application Insights](https://github.com/Azure-Samples/service-fabric-dotnet-getting-started/blob/dev/appinsights/ApplicationInsights.md) (Uso di Service Fabric con Application Insights).

### <a name="add-application-code-tooinstrument-telemetry"></a>Aggiungere dati di telemetria tooinstrument codice dell'applicazione
1. Per qualsiasi parte di codice che si desidera tooinstrument, aggiungere un tramite l'istruzione intorno a esso. 

   Nell'esempio seguente di hello, hello `RunAsync` metodo esegue alcune operazioni e hello `telemetryClient` classe acquisisce i dati di telemetria hello dopo l'avvio. evento Hello è necessario un nome univoco in un'applicazione hello.

   ```
   protected override async Task RunAsync(CancellationToken cancellationToken)
       {
           // TODO: Replace hello following sample code with your own logic
           //       or remove this RunAsync override if it's not needed in your service.

           while (true)
           {
               using( var operation = telemetryClient.StartOperation<RequestTelemetry>("[Insert_Event_Unique_Name]"))
               {
                   cancellationToken.ThrowIfCancellationRequested();

                   ++this.iterations;

                   ServiceEventSource.Current.ServiceMessage(this.Context, "Working-{0}", this.iterations);

                   await Task.Delay(TimeSpan.FromSeconds(1), cancellationToken);
               }

           }
       }
   ```

2. Distribuire il cluster di Service Fabric toohello dell'applicazione. Attesa di hello app toorun per 10 minuti. Per una migliore effetto, è possibile eseguire un test di carico in app hello. Portale andare toohello Application Insights **prestazioni** pannello e si dovrebbero venire visualizzati esempi delle tracce di profiling.

<!---
Commenting out these sections for now
## Enable hello Profiler on Cloud Services applications
[TODO]
## Enable hello Profiler on classic Azure Virtual Machines
[TODO]
## Enable hello Profiler on on-premise servers
[TODO]
--->

## <a name="next-steps"></a>Passaggi successivi

- Per informazioni su come risolvere i problemi relativi al profiler, vedere [Risoluzione dei problemi del profiler](app-insights-profiler.md#troubleshooting).

- Altre informazioni su profiler hello in [Application Insights Profiler](app-insights-profiler.md).

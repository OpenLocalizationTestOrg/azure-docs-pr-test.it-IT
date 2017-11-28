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
# <a name="enable-application-insights-profiler-on-an-azure-cloud-services-resource"></a><span data-ttu-id="d3b12-103">Abilitare Application Insights Profiler in una risorsa di Servizi cloud di Azure</span><span class="sxs-lookup"><span data-stu-id="d3b12-103">Enable Application Insights Profiler on an Azure Cloud Services resource</span></span>

<span data-ttu-id="d3b12-104">Questa procedura dettagliata illustra come tooenable Profiler Insights per le applicazioni Azure in un'applicazione ASP.NET ospitato da una risorsa di servizi Cloud di Azure.</span><span class="sxs-lookup"><span data-stu-id="d3b12-104">This walkthrough demonstrates how tooenable Azure Application Insights Profiler on an ASP.NET application hosted by an Azure Cloud Services resource.</span></span> <span data-ttu-id="d3b12-105">esempi di Hello includono il supporto per le macchine virtuali di Azure, il set di scalabilità di macchine virtuali e Azure Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="d3b12-105">hello examples include support for Azure Virtual Machines, virtual machine scale sets, and Azure Service Fabric.</span></span> <span data-ttu-id="d3b12-106">tutti gli esempi di Hello si basano su modelli che supportano il modello di distribuzione Azure Resource Manager hello.</span><span class="sxs-lookup"><span data-stu-id="d3b12-106">hello examples all rely on templates that support hello Azure Resource Manager deployment model.</span></span> <span data-ttu-id="d3b12-107">Per ulteriori informazioni sul modello di distribuzione hello, esaminare [Azure Resource Manager e distribuzione classica: comprendere i modelli di distribuzione e lo stato delle risorse di hello](/azure-resource-manager/resource-manager-deployment-model).</span><span class="sxs-lookup"><span data-stu-id="d3b12-107">For more information about hello deployment model, review [Azure Resource Manager vs. classic deployment: Understand deployment models and hello state of your resources](/azure-resource-manager/resource-manager-deployment-model).</span></span>

## <a name="overview"></a><span data-ttu-id="d3b12-108">Panoramica</span><span class="sxs-lookup"><span data-stu-id="d3b12-108">Overview</span></span>

<span data-ttu-id="d3b12-109">Hello seguente diagramma illustra il funzionamento di profiler hello per le risorse di servizi Cloud di Azure.</span><span class="sxs-lookup"><span data-stu-id="d3b12-109">hello following diagram illustrates how hello profiler works for Azure Cloud Services resources.</span></span> <span data-ttu-id="d3b12-110">Come esempio viene usata una macchina virtuale di Azure.</span><span class="sxs-lookup"><span data-stu-id="d3b12-110">It uses an Azure virtual machine as an example.</span></span>

<span data-ttu-id="d3b12-111">![Panoramica](./media/enable-profiler-compute/overview.png) hello di toocollect informazioni per l'elaborazione e la visualizzazione sul portale di Azure, è necessario installare il componente Agente di diagnostica hello per le risorse di servizi Cloud di Azure hello.</span><span class="sxs-lookup"><span data-stu-id="d3b12-111">![Overview](./media/enable-profiler-compute/overview.png) toocollect information for processing and display on hello Azure portal, you must install hello Diagnostics Agent component for hello Azure Cloud Services resources.</span></span> <span data-ttu-id="d3b12-112">Hello rest hello procedura dettagliata vengono fornite indicazioni su come tooinstall e configurare hello tooenable di agente di diagnostica del Profiler di Application Insights.</span><span class="sxs-lookup"><span data-stu-id="d3b12-112">hello rest of hello walkthrough provides guidance on how tooinstall and configure hello Diagnostics Agent tooenable Application Insights Profiler.</span></span>

## <a name="prerequisites-for-hello-walkthrough"></a><span data-ttu-id="d3b12-113">Prerequisiti per questa procedura dettagliata hello</span><span class="sxs-lookup"><span data-stu-id="d3b12-113">Prerequisites for hello walkthrough</span></span>

* <span data-ttu-id="d3b12-114">Un modello di gestione risorse di distribuzione che installa gli agenti di profiler hello in macchine virtuali hello ([WindowsVirtualMachine.json](https://github.com/Azure/azure-docs-json-samples/blob/master/application-insights/WindowsVirtualMachine.json)) o set di scalabilità ([WindowsVirtualMachineScaleSet.json](https://github.com/Azure/azure-docs-json-samples/blob/master/application-insights/WindowsVirtualMachineScaleSet.json)).</span><span class="sxs-lookup"><span data-stu-id="d3b12-114">A deployment Resource Manager template that installs hello profiler agents on hello VMs ([WindowsVirtualMachine.json](https://github.com/Azure/azure-docs-json-samples/blob/master/application-insights/WindowsVirtualMachine.json)) or scale sets ([WindowsVirtualMachineScaleSet.json](https://github.com/Azure/azure-docs-json-samples/blob/master/application-insights/WindowsVirtualMachineScaleSet.json)).</span></span>

* <span data-ttu-id="d3b12-115">Istanza di Application Insights abilitata per la profilatura.</span><span class="sxs-lookup"><span data-stu-id="d3b12-115">An Application Insights instance enabled for profiling.</span></span> <span data-ttu-id="d3b12-116">Per istruzioni, vedere [abilitare il profilo di hello](https://docs.microsoft.com/en-us/azure/application-insights/app-insights-profiler#enable-the-profiler).</span><span class="sxs-lookup"><span data-stu-id="d3b12-116">For instructions, see [Enable hello profile](https://docs.microsoft.com/en-us/azure/application-insights/app-insights-profiler#enable-the-profiler).</span></span>

* <span data-ttu-id="d3b12-117">Risorsa di servizi Cloud di Azure di destinazione di .NET framework 4.6.1 o versione successiva installato in hello.</span><span class="sxs-lookup"><span data-stu-id="d3b12-117">.NET Framework 4.6.1 or later installed on hello target Azure Cloud Services resource.</span></span>

## <a name="create-a-resource-group-in-your-azure-subscription"></a><span data-ttu-id="d3b12-118">Creare un gruppo di risorse nella sottoscrizione di Azure</span><span class="sxs-lookup"><span data-stu-id="d3b12-118">Create a resource group in your Azure subscription</span></span>
<span data-ttu-id="d3b12-119">Hello di esempio seguente viene illustrato come una risorsa toocreate gruppo usando uno script di PowerShell:</span><span class="sxs-lookup"><span data-stu-id="d3b12-119">hello following example demonstrates how toocreate a resource group by using a PowerShell script:</span></span>

```
New-AzureRmResourceGroup -Name "Replace_With_Resource_Group_Name" -Location "Replace_With_Resource_Group_Location"
```

## <a name="create-an-application-insights-resource-in-hello-resource-group"></a><span data-ttu-id="d3b12-120">Creare una risorsa di Application Insights nel gruppo di risorse hello</span><span class="sxs-lookup"><span data-stu-id="d3b12-120">Create an Application Insights resource in hello resource group</span></span>
<span data-ttu-id="d3b12-121">In hello **Application Insights** pannello, immettere le informazioni di hello per la risorsa, come illustrato nel seguente esempio:</span><span class="sxs-lookup"><span data-stu-id="d3b12-121">On hello **Application Insights** blade, enter hello information for your resource, as shown in this example:</span></span> 

![Pannello Application Insights](./media/enable-profiler-compute/createai.png)

## <a name="apply-an-application-insights-instrumentation-key-in-hello-azure-resource-manager-template"></a><span data-ttu-id="d3b12-123">Applicare una chiave di strumentazione di Application Insights nel modello di gestione risorse di Azure hello</span><span class="sxs-lookup"><span data-stu-id="d3b12-123">Apply an Application Insights instrumentation key in hello Azure Resource Manager template</span></span>

1. <span data-ttu-id="d3b12-124">Se non è stato scaricato il modello di hello, scaricarlo dal [GitHub](https://github.com/Azure/azure-docs-json-samples/blob/master/application-insights/WindowsVirtualMachine.json).</span><span class="sxs-lookup"><span data-stu-id="d3b12-124">If you haven't downloaded hello template yet, download it from [GitHub](https://github.com/Azure/azure-docs-json-samples/blob/master/application-insights/WindowsVirtualMachine.json).</span></span>

2. <span data-ttu-id="d3b12-125">Trovare la chiave di Application Insights hello.</span><span class="sxs-lookup"><span data-stu-id="d3b12-125">Find hello Application Insights key.</span></span>
   
   ![Percorso della chiave hello](./media/enable-profiler-compute/copyaikey.png)

3. <span data-ttu-id="d3b12-127">Sostituire il valore di modello hello.</span><span class="sxs-lookup"><span data-stu-id="d3b12-127">Replace hello template value.</span></span>
   
   ![Valore sostituito nel modello hello](./media/enable-profiler-compute/copyaikeytotemplate.png)

## <a name="create-an-azure-vm-toohost-hello-web-application"></a><span data-ttu-id="d3b12-129">Creare un'applicazione web di Azure VM toohost hello</span><span class="sxs-lookup"><span data-stu-id="d3b12-129">Create an Azure VM toohost hello web application</span></span>
1. <span data-ttu-id="d3b12-130">Creare una password di hello toosave stringa sicura.</span><span class="sxs-lookup"><span data-stu-id="d3b12-130">Create a secure string toosave hello password.</span></span>

   ```
   $password = ConvertTo-SecureString -String "Replace_With_Your_Password" -AsPlainText -Force
   ```

2. <span data-ttu-id="d3b12-131">Distribuire il modello di gestione risorse di Azure hello.</span><span class="sxs-lookup"><span data-stu-id="d3b12-131">Deploy hello Azure Resource Manager template.</span></span>

   <span data-ttu-id="d3b12-132">Cambiare directory hello in hello PowerShell console toohello cartella contiene il modello di gestione risorse.</span><span class="sxs-lookup"><span data-stu-id="d3b12-132">Change hello directory in hello PowerShell console toohello folder that contains your Resource Manager template.</span></span> <span data-ttu-id="d3b12-133">modello di hello toodeploy, eseguire hello comando seguente:</span><span class="sxs-lookup"><span data-stu-id="d3b12-133">toodeploy hello template, run hello following command:</span></span>

   ```
   New-AzureRmResourceGroupDeployment -ResourceGroupName "Replace_With_Resource_Group_Name" -TemplateFile .\WindowsVirtualMachine.json -adminUsername "Replace_With_your_user_name" -adminPassword $password -dnsNameForPublicIP "Replace_WIth_your_DNS_Name" -Verbose
   ```

<span data-ttu-id="d3b12-134">Dopo l'esecuzione dello script di hello è completata, è necessario trovare una macchina virtuale denominata **MyWindowsVM** nel gruppo di risorse.</span><span class="sxs-lookup"><span data-stu-id="d3b12-134">After hello script runs successfully, you should find a VM named **MyWindowsVM** in your resource group.</span></span>

## <a name="configure-web-deploy-on-hello-vm"></a><span data-ttu-id="d3b12-135">Distribuzione Web su hello VM</span><span class="sxs-lookup"><span data-stu-id="d3b12-135">Configure Web Deploy on hello VM</span></span>
<span data-ttu-id="d3b12-136">Assicurarsi che il servizio Distribuzione Web sia abilitato nella VM per poter pubblicare l'applicazione Web da Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="d3b12-136">Make sure that Web Deploy is enabled on your VM so you can publish your web application from Visual Studio.</span></span>

<span data-ttu-id="d3b12-137">tooinstall distribuzione Web in una macchina virtuale manualmente tramite WebPI, vedere [installazione e configurazione di distribuzione Web in IIS 8.0 o successiva](https://docs.microsoft.com/en-us/iis/install/installing-publishing-technologies/installing-and-configuring-web-deploy-on-iis-80-or-later).</span><span class="sxs-lookup"><span data-stu-id="d3b12-137">tooinstall Web Deploy on a VM manually via WebPI, see [Installing and Configuring Web Deploy on IIS 8.0 or Later](https://docs.microsoft.com/en-us/iis/install/installing-publishing-technologies/installing-and-configuring-web-deploy-on-iis-80-or-later).</span></span> <span data-ttu-id="d3b12-138">Per un esempio di come tooautomate installare distribuzione Web utilizzando un modello di gestione risorse di Azure, vedere [creare, configurare e distribuire un tooan di applicazione web Azure VM](https://azure.microsoft.com/en-us/resources/templates/201-web-app-vm-dsc/).</span><span class="sxs-lookup"><span data-stu-id="d3b12-138">For an example of how tooautomate installing Web Deploy by using an Azure Resource Manager template, see [Create, configure, and deploy a web application tooan Azure VM](https://azure.microsoft.com/en-us/resources/templates/201-web-app-vm-dsc/).</span></span>

<span data-ttu-id="d3b12-139">Se si distribuisce un'applicazione ASP.NET MVC, visitare tooServer Manager, selezionare **Aggiungi ruoli e funzionalità** > **Server Web (IIS)** > **Server Web**  >  **Lo sviluppo di applicazioni**e abilitare ASP.NET 4.5 nel server.</span><span class="sxs-lookup"><span data-stu-id="d3b12-139">If you are deploying an ASP.NET MVC application, go tooServer Manager, select **Add Roles and Features** > **Web Server (IIS)** > **Web Server** > **Application Development**, and enable ASP.NET 4.5 on your server.</span></span>

![Aggiungere ASP.NET](./media/enable-profiler-compute/addaspnet45.png)

## <a name="install-hello-azure-application-insights-sdk-for-your-project"></a><span data-ttu-id="d3b12-141">Installare hello Azure Application Insights SDK per il progetto</span><span class="sxs-lookup"><span data-stu-id="d3b12-141">Install hello Azure Application Insights SDK for your project</span></span>
1. <span data-ttu-id="d3b12-142">Aprire l'applicazione Web ASP.NET in Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="d3b12-142">Open your ASP.NET web application in Visual Studio.</span></span>

2. <span data-ttu-id="d3b12-143">Fare clic sul progetto hello e selezionare **Aggiungi** > **servizi connessi**.</span><span class="sxs-lookup"><span data-stu-id="d3b12-143">Right-click hello project and select **Add** > **Connected Services**.</span></span>

3. <span data-ttu-id="d3b12-144">Selezionare **Application Insights**.</span><span class="sxs-lookup"><span data-stu-id="d3b12-144">Select **Application Insights**.</span></span>

4. <span data-ttu-id="d3b12-145">Seguire le istruzioni di hello nella pagina di hello.</span><span class="sxs-lookup"><span data-stu-id="d3b12-145">Follow hello instructions on hello page.</span></span> <span data-ttu-id="d3b12-146">Selezionare una risorsa di Application Insights hello creato in precedenza.</span><span class="sxs-lookup"><span data-stu-id="d3b12-146">Select hello Application Insights resource that you created earlier.</span></span>

5. <span data-ttu-id="d3b12-147">Seleziona hello **registrare** pulsante.</span><span class="sxs-lookup"><span data-stu-id="d3b12-147">Select hello **Register** button.</span></span>


## <a name="publish-hello-project-tooan-azure-vm"></a><span data-ttu-id="d3b12-148">Pubblicare hello progetto tooan macchina virtuale di Azure</span><span class="sxs-lookup"><span data-stu-id="d3b12-148">Publish hello project tooan Azure VM</span></span>
<span data-ttu-id="d3b12-149">Esistono diversi modi toopublish un tooan applicazione macchina virtuale di Azure.</span><span class="sxs-lookup"><span data-stu-id="d3b12-149">There are several ways toopublish an application tooan Azure VM.</span></span> <span data-ttu-id="d3b12-150">Un modo consiste toouse 2017 di Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="d3b12-150">One way is toouse Visual Studio 2017.</span></span>

1. <span data-ttu-id="d3b12-151">Fare clic sul progetto hello e selezionare **pubblica**.</span><span class="sxs-lookup"><span data-stu-id="d3b12-151">Right-click hello project and select **Publish**.</span></span>

2. <span data-ttu-id="d3b12-152">Selezionare **macchine virtuali di Microsoft Azure** come hello destinazione di pubblicazione e seguire i passaggi di hello.</span><span class="sxs-lookup"><span data-stu-id="d3b12-152">Select **Microsoft Azure Virtual Machines** as hello publish target and follow hello steps.</span></span>

   ![Pubblicare da VS](./media/enable-profiler-compute/publishtoVM.png)

3. <span data-ttu-id="d3b12-154">Eseguire un test di carico sull'applicazione.</span><span class="sxs-lookup"><span data-stu-id="d3b12-154">Run a load test against your application.</span></span> <span data-ttu-id="d3b12-155">Si otterranno risultati nella pagina Web del portale di hello Application Insights istanza.</span><span class="sxs-lookup"><span data-stu-id="d3b12-155">You should see results on hello Application Insights instance portal webpage.</span></span>


## <a name="enable-hello-profiler"></a><span data-ttu-id="d3b12-156">Attivare il profiler hello</span><span class="sxs-lookup"><span data-stu-id="d3b12-156">Enable hello profiler</span></span>
1. <span data-ttu-id="d3b12-157">Passare tooyour Application Insights **prestazioni** pannello e selezionare **configura**.</span><span class="sxs-lookup"><span data-stu-id="d3b12-157">Go tooyour Application Insights **Performance** blade and select **Configure**.</span></span>
   
   ![Icona Configura](./media/enable-profiler-compute/enableprofiler1.png)
 
2. <span data-ttu-id="d3b12-159">Selezionare **Abilita profiler**.</span><span class="sxs-lookup"><span data-stu-id="d3b12-159">Select **Enable Profiler**.</span></span>
   
   ![Icona Abilita profiler](./media/enable-profiler-compute/enableprofiler2.png)

## <a name="add-a-performance-test-tooyour-application"></a><span data-ttu-id="d3b12-161">Aggiungere un'applicazione di tooyour test delle prestazioni</span><span class="sxs-lookup"><span data-stu-id="d3b12-161">Add a performance test tooyour application</span></span>
<span data-ttu-id="d3b12-162">In modo da poter raccogliere alcuni toobe di dati di esempio visualizzati nel Profiler di Application Insights, seguire questi passaggi:</span><span class="sxs-lookup"><span data-stu-id="d3b12-162">Follow these steps so we can collect some sample data toobe displayed in Application Insights Profiler:</span></span>

1. <span data-ttu-id="d3b12-163">Sfoglia risorsa di Application Insights toohello creato in precedenza.</span><span class="sxs-lookup"><span data-stu-id="d3b12-163">Browse toohello Application Insights resource that you created earlier.</span></span> 

2. <span data-ttu-id="d3b12-164">Passare toohello **disponibilità** pannello e aggiungere un test delle prestazioni che invia l'URL dell'applicazione tooyour le richieste web.</span><span class="sxs-lookup"><span data-stu-id="d3b12-164">Go toohello **Availability** blade and add a performance test that sends web requests tooyour application URL.</span></span> 

   ![Aggiungere il test delle prestazioni](./media/enable-profiler-compute/AvailabilityTest.png)

## <a name="view-your-performance-data"></a><span data-ttu-id="d3b12-166">Visualizzare i dati sulle prestazioni</span><span class="sxs-lookup"><span data-stu-id="d3b12-166">View your performance data</span></span>

1. <span data-ttu-id="d3b12-167">Attendere 10-15 minuti per toocollect profiler hello e analizzare i dati di hello.</span><span class="sxs-lookup"><span data-stu-id="d3b12-167">Wait 10-15 minutes for hello profiler toocollect and analyze hello data.</span></span> 

2. <span data-ttu-id="d3b12-168">Passare toohello **prestazioni** pannello nella risorsa di Application Insights e visualizzazione delle prestazioni dell'applicazione quando è in condizioni di carico.</span><span class="sxs-lookup"><span data-stu-id="d3b12-168">Go toohello **Performance** blade in your Application Insights resource and view how your application is performing when it's under load.</span></span>

   ![Visualizzazione delle prestazioni](./media/enable-profiler-compute/aiperformance.png)

3. <span data-ttu-id="d3b12-170">Icona di hello selezionare sotto **esempi** tooopen hello **visualizzazione traccia** blade.</span><span class="sxs-lookup"><span data-stu-id="d3b12-170">Select hello icon under **Examples** tooopen hello **Trace View** blade.</span></span>

   ![Aprire il pannello di visualizzazione traccia hello](./media/enable-profiler-compute/traceview.png)


## <a name="work-with-an-existing-template"></a><span data-ttu-id="d3b12-172">Utilizzare un modello esistente</span><span class="sxs-lookup"><span data-stu-id="d3b12-172">Work with an existing template</span></span>

1. <span data-ttu-id="d3b12-173">Individuare una dichiarazione della risorsa di diagnostica Azure hello nel modello di distribuzione.</span><span class="sxs-lookup"><span data-stu-id="d3b12-173">Locate hello Azure Diagnostics resource declaration in your deployment template.</span></span>
   
   <span data-ttu-id="d3b12-174">Se non si dispone di una dichiarazione, è possibile creare una dichiarazione hello nel seguente esempio hello simile.</span><span class="sxs-lookup"><span data-stu-id="d3b12-174">If you don't have a declaration, you can create one that resembles hello declaration in hello following example.</span></span> <span data-ttu-id="d3b12-175">È possibile aggiornare il modello di hello da hello [sito Web di Azure Resource Explorer](https://resources.azure.com).</span><span class="sxs-lookup"><span data-stu-id="d3b12-175">You can update hello template from hello [Azure Resource Explorer website](https://resources.azure.com).</span></span>

2. <span data-ttu-id="d3b12-176">Server di pubblicazione hello modifica da `Microsoft.Azure.Diagnostics` troppo`AIP.Diagnostics.Test`.</span><span class="sxs-lookup"><span data-stu-id="d3b12-176">Change hello publisher from `Microsoft.Azure.Diagnostics` too`AIP.Diagnostics.Test`.</span></span>

3. <span data-ttu-id="d3b12-177">Per `typeHandlerVersion`, usare `0.0`.</span><span class="sxs-lookup"><span data-stu-id="d3b12-177">For `typeHandlerVersion`, use `0.0`.</span></span>

4. <span data-ttu-id="d3b12-178">Assicurarsi che `autoUpgradeMinorVersion` è troppo`true`.</span><span class="sxs-lookup"><span data-stu-id="d3b12-178">Make sure that `autoUpgradeMinorVersion` is set too`true`.</span></span>

5. <span data-ttu-id="d3b12-179">Aggiungi nuova hello `ApplicationInsightsProfiler` istanza sink in hello `WadCfg` oggetto impostazioni, come illustrato nell'esempio seguente hello:</span><span class="sxs-lookup"><span data-stu-id="d3b12-179">Add hello new `ApplicationInsightsProfiler` sink instance in hello `WadCfg` settings object, as shown in hello following example:</span></span>

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

## <a name="enable-hello-profiler-on-virtual-machine-scale-sets"></a><span data-ttu-id="d3b12-180">Attivare il profiler di hello sul set di scalabilità di macchine virtuali</span><span class="sxs-lookup"><span data-stu-id="d3b12-180">Enable hello profiler on virtual machine scale sets</span></span>
<span data-ttu-id="d3b12-181">toosee come tooenable hello profiler, download hello [WindowsVirtualMachineScaleSet.json](https://github.com/Azure/azure-docs-json-samples/blob/master/application-insights/WindowsVirtualMachineScaleSet.json) modello.</span><span class="sxs-lookup"><span data-stu-id="d3b12-181">toosee how tooenable hello profiler, download hello [WindowsVirtualMachineScaleSet.json](https://github.com/Azure/azure-docs-json-samples/blob/master/application-insights/WindowsVirtualMachineScaleSet.json) template.</span></span> <span data-ttu-id="d3b12-182">Applicare hello stesso viene modificato in una risorsa di estensione VM modello toohello diagnostica per hello set di scalabilità della macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="d3b12-182">Apply hello same changes in a VM template toohello diagnostics extension resource for hello virtual machine scale set.</span></span>

<span data-ttu-id="d3b12-183">Assicurarsi che ogni istanza nel set di scalabilità hello dispone di accesso toohello internet.</span><span class="sxs-lookup"><span data-stu-id="d3b12-183">Make sure that each instance in hello scale set has access toohello internet.</span></span> <span data-ttu-id="d3b12-184">Hello agente Profiler può quindi inviare i campioni raccolti hello tooApplication Insights per la visualizzazione e analisi.</span><span class="sxs-lookup"><span data-stu-id="d3b12-184">hello Profiler Agent can then send hello collected samples tooApplication Insights for display and analysis.</span></span>

## <a name="enable-hello-profiler-on-service-fabric-applications"></a><span data-ttu-id="d3b12-185">Attivare il profiler hello sulle applicazioni di Service Fabric</span><span class="sxs-lookup"><span data-stu-id="d3b12-185">Enable hello profiler on Service Fabric applications</span></span>
1. <span data-ttu-id="d3b12-186">Hello di effettuare il provisioning dell'infrastruttura del servizio cluster toohave hello Azure estensione di diagnostica che installa l'agente di Profiler hello.</span><span class="sxs-lookup"><span data-stu-id="d3b12-186">Provision hello Service Fabric cluster toohave hello Azure Diagnostics extension that installs hello Profiler Agent.</span></span>

2. <span data-ttu-id="d3b12-187">Installare Application Insights SDK hello nel progetto hello e configurare la chiave di Application Insights hello.</span><span class="sxs-lookup"><span data-stu-id="d3b12-187">Install hello Application Insights SDK in hello project and configure hello Application Insights key.</span></span>

3. <span data-ttu-id="d3b12-188">Aggiungere dati di telemetria tooinstrument codice dell'applicazione.</span><span class="sxs-lookup"><span data-stu-id="d3b12-188">Add application code tooinstrument telemetry.</span></span>

### <a name="provision-hello-service-fabric-cluster-toohave-hello-azure-diagnostics-extension-that-installs-hello-profiler-agent"></a><span data-ttu-id="d3b12-189">Eseguire il provisioning hello Service Fabric cluster toohave hello estensione diagnostica di Azure che installa l'agente di Profiler hello</span><span class="sxs-lookup"><span data-stu-id="d3b12-189">Provision hello Service Fabric cluster toohave hello Azure Diagnostics extension that installs hello Profiler Agent</span></span>
<span data-ttu-id="d3b12-190">Un cluster di Service Fabric può essere sicuro o non sicuro.</span><span class="sxs-lookup"><span data-stu-id="d3b12-190">A Service Fabric cluster can be secure or non-secure.</span></span> <span data-ttu-id="d3b12-191">È possibile impostare un gateway cluster toobe non protetto e pertanto non richiede un certificato per l'accesso.</span><span class="sxs-lookup"><span data-stu-id="d3b12-191">You can set one gateway cluster toobe non-secure so it doesn't require a certificate for access.</span></span> <span data-ttu-id="d3b12-192">I cluster che ospitano la logica di business e i dati devono essere sicuri.</span><span class="sxs-lookup"><span data-stu-id="d3b12-192">Clusters that host business logic and data should be secure.</span></span> <span data-ttu-id="d3b12-193">È possibile attivare il profiler hello nei cluster di Service Fabric protetto e non sicure.</span><span class="sxs-lookup"><span data-stu-id="d3b12-193">You can enable hello profiler on both secure and non-secure Service Fabric clusters.</span></span> <span data-ttu-id="d3b12-194">Questa procedura dettagliata Usa un cluster di non protetto come un esempio tooexplain quali modifiche sono necessari tooenable hello profiler.</span><span class="sxs-lookup"><span data-stu-id="d3b12-194">This walkthrough uses a non-secure cluster as an example tooexplain what changes are required tooenable hello profiler.</span></span> <span data-ttu-id="d3b12-195">È possibile eseguire il provisioning di un cluster protetto in hello allo stesso modo.</span><span class="sxs-lookup"><span data-stu-id="d3b12-195">You can provision a secure cluster in hello same way.</span></span>

1. <span data-ttu-id="d3b12-196">Scaricare [ServiceFabricCluster.json](https://github.com/Azure/azure-docs-json-samples/blob/master/application-insights/ServiceFabricCluster.json).</span><span class="sxs-lookup"><span data-stu-id="d3b12-196">Download [ServiceFabricCluster.json](https://github.com/Azure/azure-docs-json-samples/blob/master/application-insights/ServiceFabricCluster.json).</span></span> <span data-ttu-id="d3b12-197">Come per le VM e i set di scalabilità di macchine virtuali, sostituire `Application_Insights_Key` con la propria chiave di Application Insights:</span><span class="sxs-lookup"><span data-stu-id="d3b12-197">As you did for VMs and virtual machine scale sets, replace `Application_Insights_Key` with your Application Insights key:</span></span>

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

2. <span data-ttu-id="d3b12-198">Distribuire il modello di hello usando uno script di PowerShell:</span><span class="sxs-lookup"><span data-stu-id="d3b12-198">Deploy hello template by using a PowerShell script:</span></span>

   ```
   Login-AzureRmAccount
   New-AzureRmResourceGroup -Name [Your_Resource_Group_Name] -Location [Your_Resource_Group_Location] -Verbose -Force
   New-AzureRmResourceGroupDeployment -Name [Choose_An_Arbitrary_Name] -ResourceGroupName [Your_Resource_Group_Name] -TemplateFile [Path_To_Your_Template]

   ```

### <a name="install-hello-application-insights-sdk-in-hello-project-and-configure-hello-application-insights-key"></a><span data-ttu-id="d3b12-199">Installare Application Insights SDK hello nel progetto hello e configurare la chiave di Application Insights hello</span><span class="sxs-lookup"><span data-stu-id="d3b12-199">Install hello Application Insights SDK in hello project and configure hello Application Insights key</span></span>
<span data-ttu-id="d3b12-200">Installare Application Insights SDK hello da hello [pacchetto NuGet](https://www.nuget.org/packages/Microsoft.ApplicationInsights.Web/).</span><span class="sxs-lookup"><span data-stu-id="d3b12-200">Install hello Application Insights SDK from hello [NuGet package](https://www.nuget.org/packages/Microsoft.ApplicationInsights.Web/).</span></span> <span data-ttu-id="d3b12-201">Assicurarsi di installare una versione stabile, 2.3 o successiva.</span><span class="sxs-lookup"><span data-stu-id="d3b12-201">Make sure that you install a stable version, 2.3 or later.</span></span> 

<span data-ttu-id="d3b12-202">Per informazioni sulla configurazione di Application Insights nei progetti, vedere [Using Service Fabric with Application Insights](https://github.com/Azure-Samples/service-fabric-dotnet-getting-started/blob/dev/appinsights/ApplicationInsights.md) (Uso di Service Fabric con Application Insights).</span><span class="sxs-lookup"><span data-stu-id="d3b12-202">For information about configuring Application Insights in your projects, see [Using Service Fabric with Application Insights](https://github.com/Azure-Samples/service-fabric-dotnet-getting-started/blob/dev/appinsights/ApplicationInsights.md).</span></span>

### <a name="add-application-code-tooinstrument-telemetry"></a><span data-ttu-id="d3b12-203">Aggiungere dati di telemetria tooinstrument codice dell'applicazione</span><span class="sxs-lookup"><span data-stu-id="d3b12-203">Add application code tooinstrument telemetry</span></span>
1. <span data-ttu-id="d3b12-204">Per qualsiasi parte di codice che si desidera tooinstrument, aggiungere un tramite l'istruzione intorno a esso.</span><span class="sxs-lookup"><span data-stu-id="d3b12-204">For any piece of code that you want tooinstrument, add a using statement around it.</span></span> 

   <span data-ttu-id="d3b12-205">Nell'esempio seguente di hello, hello `RunAsync` metodo esegue alcune operazioni e hello `telemetryClient` classe acquisisce i dati di telemetria hello dopo l'avvio.</span><span class="sxs-lookup"><span data-stu-id="d3b12-205">In hello following  example, hello `RunAsync` method is doing some work, and hello `telemetryClient` class captures hello telemetry after it starts.</span></span> <span data-ttu-id="d3b12-206">evento Hello è necessario un nome univoco in un'applicazione hello.</span><span class="sxs-lookup"><span data-stu-id="d3b12-206">hello event needs a unique name across hello application.</span></span>

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

2. <span data-ttu-id="d3b12-207">Distribuire il cluster di Service Fabric toohello dell'applicazione.</span><span class="sxs-lookup"><span data-stu-id="d3b12-207">Deploy your application toohello Service Fabric cluster.</span></span> <span data-ttu-id="d3b12-208">Attesa di hello app toorun per 10 minuti.</span><span class="sxs-lookup"><span data-stu-id="d3b12-208">Wait for hello app toorun for 10 minutes.</span></span> <span data-ttu-id="d3b12-209">Per una migliore effetto, è possibile eseguire un test di carico in app hello.</span><span class="sxs-lookup"><span data-stu-id="d3b12-209">For better effect, you can run a load test on hello app.</span></span> <span data-ttu-id="d3b12-210">Portale andare toohello Application Insights **prestazioni** pannello e si dovrebbero venire visualizzati esempi delle tracce di profiling.</span><span class="sxs-lookup"><span data-stu-id="d3b12-210">Go toohello Application Insights portal's **Performance** blade, and you should see examples of profiling traces appear.</span></span>

<!---
Commenting out these sections for now
## Enable hello Profiler on Cloud Services applications
[TODO]
## Enable hello Profiler on classic Azure Virtual Machines
[TODO]
## Enable hello Profiler on on-premise servers
[TODO]
--->

## <a name="next-steps"></a><span data-ttu-id="d3b12-211">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="d3b12-211">Next steps</span></span>

- <span data-ttu-id="d3b12-212">Per informazioni su come risolvere i problemi relativi al profiler, vedere [Risoluzione dei problemi del profiler](app-insights-profiler.md#troubleshooting).</span><span class="sxs-lookup"><span data-stu-id="d3b12-212">Find help with troubleshooting profiler issues in [Profiler troubleshooting](app-insights-profiler.md#troubleshooting).</span></span>

- <span data-ttu-id="d3b12-213">Altre informazioni su profiler hello in [Application Insights Profiler](app-insights-profiler.md).</span><span class="sxs-lookup"><span data-stu-id="d3b12-213">Read more about hello profiler in [Application Insights Profiler](app-insights-profiler.md).</span></span>

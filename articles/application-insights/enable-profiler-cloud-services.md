---
title: Abilitare Azure Application Insights Profiler in una risorsa di Servizi cloud | Microsoft Docs
description: Informazioni su come configurare il profiler in un'applicazione ASP.NET ospitata da una risorsa di Servizi Cloud di Azure.
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
ms.openlocfilehash: 5ff062ac81dca9d8b205cec966d2a9c11a4005b6
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/29/2017
---
# <a name="enable-application-insights-profiler-on-an-azure-cloud-services-resource"></a><span data-ttu-id="7cb35-103">Abilitare Application Insights Profiler in una risorsa di Servizi cloud di Azure</span><span class="sxs-lookup"><span data-stu-id="7cb35-103">Enable Application Insights Profiler on an Azure Cloud Services resource</span></span>

<span data-ttu-id="7cb35-104">Questa procedura dettagliata illustra come abilitare Azure Application Insights Profiler in un'applicazione ASP.NET ospitata da una risorsa di Servizi cloud di Azure.</span><span class="sxs-lookup"><span data-stu-id="7cb35-104">This walkthrough demonstrates how to enable Azure Application Insights Profiler on an ASP.NET application hosted by an Azure Cloud Services resource.</span></span> <span data-ttu-id="7cb35-105">Gli esempi includono il supporto per Macchine virtuali di Azure, set di scalabilità di macchine virtuali e Azure Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="7cb35-105">The examples include support for Azure Virtual Machines, virtual machine scale sets, and Azure Service Fabric.</span></span> <span data-ttu-id="7cb35-106">Tutti gli esempi si basano su modelli che supportano il modello di distribuzione Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="7cb35-106">The examples all rely on templates that support the Azure Resource Manager deployment model.</span></span> <span data-ttu-id="7cb35-107">Per altre informazioni sul modello di distribuzione, vedere [Confronto tra distribuzione di Azure Resource Manager e classica: comprensione dei modelli di implementazione e dello stato delle risorse](/azure-resource-manager/resource-manager-deployment-model).</span><span class="sxs-lookup"><span data-stu-id="7cb35-107">For more information about the deployment model, review [Azure Resource Manager vs. classic deployment: Understand deployment models and the state of your resources](/azure-resource-manager/resource-manager-deployment-model).</span></span>

## <a name="overview"></a><span data-ttu-id="7cb35-108">Panoramica</span><span class="sxs-lookup"><span data-stu-id="7cb35-108">Overview</span></span>

<span data-ttu-id="7cb35-109">Il diagramma seguente illustra come funziona il profiler per le risorse di Servizi cloud di Azure.</span><span class="sxs-lookup"><span data-stu-id="7cb35-109">The following diagram illustrates how the profiler works for Azure Cloud Services resources.</span></span> <span data-ttu-id="7cb35-110">Come esempio viene usata una macchina virtuale di Azure.</span><span class="sxs-lookup"><span data-stu-id="7cb35-110">It uses an Azure virtual machine as an example.</span></span>

<span data-ttu-id="7cb35-111">![Panoramica](./media/enable-profiler-compute/overview.png) Per raccogliere le informazioni per l'elaborazione e la visualizzazione nel portale di Azure, è necessario installare il componente Diagnostics Agent per le risorse di Servizi cloud di Azure.</span><span class="sxs-lookup"><span data-stu-id="7cb35-111">![Overview](./media/enable-profiler-compute/overview.png) To collect information for processing and display on the Azure portal, you must install the Diagnostics Agent component for the Azure Cloud Services resources.</span></span> <span data-ttu-id="7cb35-112">Il resto della procedura dettagliata contiene indicazioni su come installare e configurare Diagnostics Agent per abilitare Application Insights Profiler.</span><span class="sxs-lookup"><span data-stu-id="7cb35-112">The rest of the walkthrough provides guidance on how to install and configure the Diagnostics Agent to enable Application Insights Profiler.</span></span>

## <a name="prerequisites-for-the-walkthrough"></a><span data-ttu-id="7cb35-113">Prerequisiti per la procedura dettagliata</span><span class="sxs-lookup"><span data-stu-id="7cb35-113">Prerequisites for the walkthrough</span></span>

* <span data-ttu-id="7cb35-114">Un modello di distribuzione Resource Manager che consente di installare gli agenti del profiler nelle VM ([WindowsVirtualMachine.json](https://github.com/Azure/azure-docs-json-samples/blob/master/application-insights/WindowsVirtualMachine.json)) o nei set di scalabilità ([WindowsVirtualMachineScaleSet.json](https://github.com/Azure/azure-docs-json-samples/blob/master/application-insights/WindowsVirtualMachineScaleSet.json)).</span><span class="sxs-lookup"><span data-stu-id="7cb35-114">A deployment Resource Manager template that installs the profiler agents on the VMs ([WindowsVirtualMachine.json](https://github.com/Azure/azure-docs-json-samples/blob/master/application-insights/WindowsVirtualMachine.json)) or scale sets ([WindowsVirtualMachineScaleSet.json](https://github.com/Azure/azure-docs-json-samples/blob/master/application-insights/WindowsVirtualMachineScaleSet.json)).</span></span>

* <span data-ttu-id="7cb35-115">Istanza di Application Insights abilitata per la profilatura.</span><span class="sxs-lookup"><span data-stu-id="7cb35-115">An Application Insights instance enabled for profiling.</span></span> <span data-ttu-id="7cb35-116">Per istruzioni, vedere [Abilitare il profiler](https://docs.microsoft.com/en-us/azure/application-insights/app-insights-profiler#enable-the-profiler).</span><span class="sxs-lookup"><span data-stu-id="7cb35-116">For instructions, see [Enable the profile](https://docs.microsoft.com/en-us/azure/application-insights/app-insights-profiler#enable-the-profiler).</span></span>

* <span data-ttu-id="7cb35-117">.NET Framework 4.6.1 o versione successiva installato nella risorsa di Servizi cloud di Azure di destinazione.</span><span class="sxs-lookup"><span data-stu-id="7cb35-117">.NET Framework 4.6.1 or later installed on the target Azure Cloud Services resource.</span></span>

## <a name="create-a-resource-group-in-your-azure-subscription"></a><span data-ttu-id="7cb35-118">Creare un gruppo di risorse nella sottoscrizione di Azure</span><span class="sxs-lookup"><span data-stu-id="7cb35-118">Create a resource group in your Azure subscription</span></span>
<span data-ttu-id="7cb35-119">L'esempio seguente illustra come creare un gruppo di risorse usando uno script di PowerShell:</span><span class="sxs-lookup"><span data-stu-id="7cb35-119">The following example demonstrates how to create a resource group by using a PowerShell script:</span></span>

```
New-AzureRmResourceGroup -Name "Replace_With_Resource_Group_Name" -Location "Replace_With_Resource_Group_Location"
```

## <a name="create-an-application-insights-resource-in-the-resource-group"></a><span data-ttu-id="7cb35-120">Creare una risorsa di Application Insights nel gruppo di risorse</span><span class="sxs-lookup"><span data-stu-id="7cb35-120">Create an Application Insights resource in the resource group</span></span>
<span data-ttu-id="7cb35-121">Nel pannello **Application Insights** immettere le informazioni per la risorsa, come illustrato nell'esempio:</span><span class="sxs-lookup"><span data-stu-id="7cb35-121">On the **Application Insights** blade, enter the information for your resource, as shown in this example:</span></span> 

![Pannello Application Insights](./media/enable-profiler-compute/createai.png)

## <a name="apply-an-application-insights-instrumentation-key-in-the-azure-resource-manager-template"></a><span data-ttu-id="7cb35-123">Applicare una chiave di strumentazione di Application Insights nel modello di Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="7cb35-123">Apply an Application Insights instrumentation key in the Azure Resource Manager template</span></span>

1. <span data-ttu-id="7cb35-124">Se il modello non è ancora stato scaricato, scaricarlo da [GitHub](https://github.com/Azure/azure-docs-json-samples/blob/master/application-insights/WindowsVirtualMachine.json).</span><span class="sxs-lookup"><span data-stu-id="7cb35-124">If you haven't downloaded the template yet, download it from [GitHub](https://github.com/Azure/azure-docs-json-samples/blob/master/application-insights/WindowsVirtualMachine.json).</span></span>

2. <span data-ttu-id="7cb35-125">Trovare la chiave di Application Insights.</span><span class="sxs-lookup"><span data-stu-id="7cb35-125">Find the Application Insights key.</span></span>
   
   ![Posizione della chiave](./media/enable-profiler-compute/copyaikey.png)

3. <span data-ttu-id="7cb35-127">Sostituire il valore del modello.</span><span class="sxs-lookup"><span data-stu-id="7cb35-127">Replace the template value.</span></span>
   
   ![Valore sostituito nel modello](./media/enable-profiler-compute/copyaikeytotemplate.png)

## <a name="create-an-azure-vm-to-host-the-web-application"></a><span data-ttu-id="7cb35-129">Creare una VM di Azure per ospitare l'applicazione Web</span><span class="sxs-lookup"><span data-stu-id="7cb35-129">Create an Azure VM to host the web application</span></span>
1. <span data-ttu-id="7cb35-130">Creare una stringa sicura per salvare la password.</span><span class="sxs-lookup"><span data-stu-id="7cb35-130">Create a secure string to save the password.</span></span>

   ```
   $password = ConvertTo-SecureString -String "Replace_With_Your_Password" -AsPlainText -Force
   ```

2. <span data-ttu-id="7cb35-131">Distribuire il modello di Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="7cb35-131">Deploy the Azure Resource Manager template.</span></span>

   <span data-ttu-id="7cb35-132">Sostituire la directory nella console di PowerShell con la cartella contenente il modello di Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="7cb35-132">Change the directory in the PowerShell console to the folder that contains your Resource Manager template.</span></span> <span data-ttu-id="7cb35-133">Per distribuire il modello, eseguire il comando seguente:</span><span class="sxs-lookup"><span data-stu-id="7cb35-133">To deploy the template, run the following command:</span></span>

   ```
   New-AzureRmResourceGroupDeployment -ResourceGroupName "Replace_With_Resource_Group_Name" -TemplateFile .\WindowsVirtualMachine.json -adminUsername "Replace_With_your_user_name" -adminPassword $password -dnsNameForPublicIP "Replace_WIth_your_DNS_Name" -Verbose
   ```

<span data-ttu-id="7cb35-134">Al termine dell'esecuzione dello script, nel gruppo di risorse sarà presente una VM denominata **MyWindowsVM**.</span><span class="sxs-lookup"><span data-stu-id="7cb35-134">After the script runs successfully, you should find a VM named **MyWindowsVM** in your resource group.</span></span>

## <a name="configure-web-deploy-on-the-vm"></a><span data-ttu-id="7cb35-135">Configurare Distribuzione Web nella VM</span><span class="sxs-lookup"><span data-stu-id="7cb35-135">Configure Web Deploy on the VM</span></span>
<span data-ttu-id="7cb35-136">Assicurarsi che il servizio Distribuzione Web sia abilitato nella VM per poter pubblicare l'applicazione Web da Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="7cb35-136">Make sure that Web Deploy is enabled on your VM so you can publish your web application from Visual Studio.</span></span>

<span data-ttu-id="7cb35-137">Per installare Distribuzione Web in una VM manualmente tramite WebPI, vedere [Installing and Configuring Web Deploy on IIS 8.0 or Later](https://docs.microsoft.com/en-us/iis/install/installing-publishing-technologies/installing-and-configuring-web-deploy-on-iis-80-or-later) (Installazione e configurazione di Distribuzione Web in IIS 8.0 e versioni successive).</span><span class="sxs-lookup"><span data-stu-id="7cb35-137">To install Web Deploy on a VM manually via WebPI, see [Installing and Configuring Web Deploy on IIS 8.0 or Later](https://docs.microsoft.com/en-us/iis/install/installing-publishing-technologies/installing-and-configuring-web-deploy-on-iis-80-or-later).</span></span> <span data-ttu-id="7cb35-138">Per un esempio di come automatizzare l'installazione di Distribuzione Web usando un modello di Azure Resource Manager, vedere [Create, configure, and deploy Web Application to an Azure VM](https://azure.microsoft.com/en-us/resources/templates/201-web-app-vm-dsc/) (Creare, configurare e distribuire un'applicazione Web in una VM di Azure).</span><span class="sxs-lookup"><span data-stu-id="7cb35-138">For an example of how to automate installing Web Deploy by using an Azure Resource Manager template, see [Create, configure, and deploy a web application to an Azure VM](https://azure.microsoft.com/en-us/resources/templates/201-web-app-vm-dsc/).</span></span>

<span data-ttu-id="7cb35-139">Per distribuire un'applicazione ASP.NET MVC, passare a Server Manager, selezionare **Aggiungi ruoli e funzionalità** > **Server Web (IIS)** > **Server Web** > **Sviluppo applicazioni** e abilitare ASP.NET 4.5 nel server.</span><span class="sxs-lookup"><span data-stu-id="7cb35-139">If you are deploying an ASP.NET MVC application, go to Server Manager, select **Add Roles and Features** > **Web Server (IIS)** > **Web Server** > **Application Development**, and enable ASP.NET 4.5 on your server.</span></span>

![Aggiungere ASP.NET](./media/enable-profiler-compute/addaspnet45.png)

## <a name="install-the-azure-application-insights-sdk-for-your-project"></a><span data-ttu-id="7cb35-141">Installare Azure Application Insights SDK per il progetto</span><span class="sxs-lookup"><span data-stu-id="7cb35-141">Install the Azure Application Insights SDK for your project</span></span>
1. <span data-ttu-id="7cb35-142">Aprire l'applicazione Web ASP.NET in Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="7cb35-142">Open your ASP.NET web application in Visual Studio.</span></span>

2. <span data-ttu-id="7cb35-143">Fare clic con il pulsante destro del mouse sul progetto e scegliere **Aggiungi** > **Servizi connessi**.</span><span class="sxs-lookup"><span data-stu-id="7cb35-143">Right-click the project and select **Add** > **Connected Services**.</span></span>

3. <span data-ttu-id="7cb35-144">Selezionare **Application Insights**.</span><span class="sxs-lookup"><span data-stu-id="7cb35-144">Select **Application Insights**.</span></span>

4. <span data-ttu-id="7cb35-145">Seguire le istruzioni visualizzate.</span><span class="sxs-lookup"><span data-stu-id="7cb35-145">Follow the instructions on the page.</span></span> <span data-ttu-id="7cb35-146">Selezionare la risorsa di Application Insights creata in precedenza.</span><span class="sxs-lookup"><span data-stu-id="7cb35-146">Select the Application Insights resource that you created earlier.</span></span>

5. <span data-ttu-id="7cb35-147">Fare clic sul pulsante **Registra**.</span><span class="sxs-lookup"><span data-stu-id="7cb35-147">Select the **Register** button.</span></span>


## <a name="publish-the-project-to-an-azure-vm"></a><span data-ttu-id="7cb35-148">Pubblicare il progetto in una VM di Azure</span><span class="sxs-lookup"><span data-stu-id="7cb35-148">Publish the project to an Azure VM</span></span>
<span data-ttu-id="7cb35-149">Esistono diversi modi per pubblicare un'applicazione in una macchina virtuale di Azure.</span><span class="sxs-lookup"><span data-stu-id="7cb35-149">There are several ways to publish an application to an Azure VM.</span></span> <span data-ttu-id="7cb35-150">Un modo consiste nell'usare Visual Studio 2017.</span><span class="sxs-lookup"><span data-stu-id="7cb35-150">One way is to use Visual Studio 2017.</span></span>

1. <span data-ttu-id="7cb35-151">Fare clic con il pulsante destro del mouse sul progetto e scegliere **Pubblica**.</span><span class="sxs-lookup"><span data-stu-id="7cb35-151">Right-click the project and select **Publish**.</span></span>

2. <span data-ttu-id="7cb35-152">Selezionare **Macchine virtuali di Microsoft Azure** come destinazione di pubblicazione e seguire i passaggi.</span><span class="sxs-lookup"><span data-stu-id="7cb35-152">Select **Microsoft Azure Virtual Machines** as the publish target and follow the steps.</span></span>

   ![Pubblicare da VS](./media/enable-profiler-compute/publishtoVM.png)

3. <span data-ttu-id="7cb35-154">Eseguire un test di carico sull'applicazione.</span><span class="sxs-lookup"><span data-stu-id="7cb35-154">Run a load test against your application.</span></span> <span data-ttu-id="7cb35-155">I risultati dovrebbero venire visualizzati nella pagina Web del portale dell'istanza di Application Insights.</span><span class="sxs-lookup"><span data-stu-id="7cb35-155">You should see results on the Application Insights instance portal webpage.</span></span>


## <a name="enable-the-profiler"></a><span data-ttu-id="7cb35-156">Abilitare il profiler</span><span class="sxs-lookup"><span data-stu-id="7cb35-156">Enable the profiler</span></span>
1. <span data-ttu-id="7cb35-157">Passare al pannello **Prestazioni** di Application Insights e selezionare **Configura**.</span><span class="sxs-lookup"><span data-stu-id="7cb35-157">Go to your Application Insights **Performance** blade and select **Configure**.</span></span>
   
   ![Icona Configura](./media/enable-profiler-compute/enableprofiler1.png)
 
2. <span data-ttu-id="7cb35-159">Selezionare **Abilita profiler**.</span><span class="sxs-lookup"><span data-stu-id="7cb35-159">Select **Enable Profiler**.</span></span>
   
   ![Icona Abilita profiler](./media/enable-profiler-compute/enableprofiler2.png)

## <a name="add-a-performance-test-to-your-application"></a><span data-ttu-id="7cb35-161">Aggiungere un test delle prestazioni all'applicazione</span><span class="sxs-lookup"><span data-stu-id="7cb35-161">Add a performance test to your application</span></span>
<span data-ttu-id="7cb35-162">Seguire questa procedura per poter raccogliere alcuni dati di esempio da visualizzare in Application Insights Profiler:</span><span class="sxs-lookup"><span data-stu-id="7cb35-162">Follow these steps so we can collect some sample data to be displayed in Application Insights Profiler:</span></span>

1. <span data-ttu-id="7cb35-163">Passare alla risorsa di Application Insights creata in precedenza.</span><span class="sxs-lookup"><span data-stu-id="7cb35-163">Browse to the Application Insights resource that you created earlier.</span></span> 

2. <span data-ttu-id="7cb35-164">Passare al pannello **Disponibilità** e aggiungere un test delle prestazioni che invia richieste Web all'URL dell'applicazione.</span><span class="sxs-lookup"><span data-stu-id="7cb35-164">Go to the **Availability** blade and add a performance test that sends web requests to your application URL.</span></span> 

   ![Aggiungere il test delle prestazioni](./media/enable-profiler-compute/AvailabilityTest.png)

## <a name="view-your-performance-data"></a><span data-ttu-id="7cb35-166">Visualizzare i dati sulle prestazioni</span><span class="sxs-lookup"><span data-stu-id="7cb35-166">View your performance data</span></span>

1. <span data-ttu-id="7cb35-167">Attendere 10-15 minuti mentre il profiler raccoglie e analizza i dati.</span><span class="sxs-lookup"><span data-stu-id="7cb35-167">Wait 10-15 minutes for the profiler to collect and analyze the data.</span></span> 

2. <span data-ttu-id="7cb35-168">Passare al pannello **Prestazioni** nella risorsa di Application Insights e visualizzare le prestazioni dell'applicazione sotto carico.</span><span class="sxs-lookup"><span data-stu-id="7cb35-168">Go to the **Performance** blade in your Application Insights resource and view how your application is performing when it's under load.</span></span>

   ![Visualizzazione delle prestazioni](./media/enable-profiler-compute/aiperformance.png)

3. <span data-ttu-id="7cb35-170">Selezionare l'icona sotto **Esempi** per aprire il pannello **Trace View** (Visualizzazione traccia).</span><span class="sxs-lookup"><span data-stu-id="7cb35-170">Select the icon under **Examples** to open the **Trace View** blade.</span></span>

   ![Aprire il pannello di visualizzazione traccia](./media/enable-profiler-compute/traceview.png)


## <a name="work-with-an-existing-template"></a><span data-ttu-id="7cb35-172">Utilizzare un modello esistente</span><span class="sxs-lookup"><span data-stu-id="7cb35-172">Work with an existing template</span></span>

1. <span data-ttu-id="7cb35-173">Individuare la dichiarazione della risorsa di Diagnostica di Azure nel modello di distribuzione.</span><span class="sxs-lookup"><span data-stu-id="7cb35-173">Locate the Azure Diagnostics resource declaration in your deployment template.</span></span>
   
   <span data-ttu-id="7cb35-174">Se non si ha una dichiarazione, è possibile crearne una simile a quella nell'esempio seguente.</span><span class="sxs-lookup"><span data-stu-id="7cb35-174">If you don't have a declaration, you can create one that resembles the declaration in the following example.</span></span> <span data-ttu-id="7cb35-175">È possibile aggiornare il modello dal [sito Web di Azure Resource Explorer](https://resources.azure.com).</span><span class="sxs-lookup"><span data-stu-id="7cb35-175">You can update the template from the [Azure Resource Explorer website](https://resources.azure.com).</span></span>

2. <span data-ttu-id="7cb35-176">Modificare il valore di publisher da `Microsoft.Azure.Diagnostics` a `AIP.Diagnostics.Test`.</span><span class="sxs-lookup"><span data-stu-id="7cb35-176">Change the publisher from `Microsoft.Azure.Diagnostics` to `AIP.Diagnostics.Test`.</span></span>

3. <span data-ttu-id="7cb35-177">Per `typeHandlerVersion`, usare `0.0`.</span><span class="sxs-lookup"><span data-stu-id="7cb35-177">For `typeHandlerVersion`, use `0.0`.</span></span>

4. <span data-ttu-id="7cb35-178">Assicurarsi che `autoUpgradeMinorVersion` sia impostato su `true`.</span><span class="sxs-lookup"><span data-stu-id="7cb35-178">Make sure that `autoUpgradeMinorVersion` is set to `true`.</span></span>

5. <span data-ttu-id="7cb35-179">Aggiungere la nuova istanza del sink `ApplicationInsightsProfiler` nell'oggetto impostazioni `WadCfg`, come illustrato nell'esempio seguente:</span><span class="sxs-lookup"><span data-stu-id="7cb35-179">Add the new `ApplicationInsightsProfiler` sink instance in the `WadCfg` settings object, as shown in the following example:</span></span>

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
                      "ApplicationInsightsProfiler": "Enter the Application Insights instance instrumentation key guid here"
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

## <a name="enable-the-profiler-on-virtual-machine-scale-sets"></a><span data-ttu-id="7cb35-180">Abilitare il profiler nei set di scalabilità di macchine virtuali</span><span class="sxs-lookup"><span data-stu-id="7cb35-180">Enable the profiler on virtual machine scale sets</span></span>
<span data-ttu-id="7cb35-181">Per informazioni su come abilitare il profiler, scaricare il modello [WindowsVirtualMachineScaleSet.json](https://github.com/Azure/azure-docs-json-samples/blob/master/application-insights/WindowsVirtualMachineScaleSet.json).</span><span class="sxs-lookup"><span data-stu-id="7cb35-181">To see how to enable the profiler, download the [WindowsVirtualMachineScaleSet.json](https://github.com/Azure/azure-docs-json-samples/blob/master/application-insights/WindowsVirtualMachineScaleSet.json) template.</span></span> <span data-ttu-id="7cb35-182">Applicare le stesse modifiche di un modello di VM alla risorsa di estensione di diagnostica per il set di scalabilità di macchine virtuali.</span><span class="sxs-lookup"><span data-stu-id="7cb35-182">Apply the same changes in a VM template to the diagnostics extension resource for the virtual machine scale set.</span></span>

<span data-ttu-id="7cb35-183">Assicurarsi che ogni istanza nel set di scalabilità abbia accesso a Internet.</span><span class="sxs-lookup"><span data-stu-id="7cb35-183">Make sure that each instance in the scale set has access to the internet.</span></span> <span data-ttu-id="7cb35-184">L'agente del profiler può quindi inviare i campioni raccolti ad Application Insights per la visualizzazione e l'analisi.</span><span class="sxs-lookup"><span data-stu-id="7cb35-184">The Profiler Agent can then send the collected samples to Application Insights for display and analysis.</span></span>

## <a name="enable-the-profiler-on-service-fabric-applications"></a><span data-ttu-id="7cb35-185">Abilitare il profiler nelle applicazioni di Service Fabric</span><span class="sxs-lookup"><span data-stu-id="7cb35-185">Enable the profiler on Service Fabric applications</span></span>
1. <span data-ttu-id="7cb35-186">Effettuare il provisioning del cluster di Service Fabric in modo da avere l'estensione di Diagnostica di Azure che installa l'agente del profiler.</span><span class="sxs-lookup"><span data-stu-id="7cb35-186">Provision the Service Fabric cluster to have the Azure Diagnostics extension that installs the Profiler Agent.</span></span>

2. <span data-ttu-id="7cb35-187">Installare Application Insights SDK nel progetto e configurare la chiave di Application Insights.</span><span class="sxs-lookup"><span data-stu-id="7cb35-187">Install the Application Insights SDK in the project and configure the Application Insights key.</span></span>

3. <span data-ttu-id="7cb35-188">Aggiungere il codice dell'applicazione per instrumentare la telemetria.</span><span class="sxs-lookup"><span data-stu-id="7cb35-188">Add application code to instrument telemetry.</span></span>

### <a name="provision-the-service-fabric-cluster-to-have-the-azure-diagnostics-extension-that-installs-the-profiler-agent"></a><span data-ttu-id="7cb35-189">Effettuare il provisioning del cluster di Service Fabric in modo da avere l'estensione di Diagnostica di Azure che installa l'agente del profiler</span><span class="sxs-lookup"><span data-stu-id="7cb35-189">Provision the Service Fabric cluster to have the Azure Diagnostics extension that installs the Profiler Agent</span></span>
<span data-ttu-id="7cb35-190">Un cluster di Service Fabric può essere sicuro o non sicuro.</span><span class="sxs-lookup"><span data-stu-id="7cb35-190">A Service Fabric cluster can be secure or non-secure.</span></span> <span data-ttu-id="7cb35-191">È possibile impostare un cluster di gateway come non sicuro in modo che non richieda un certificato per l'accesso.</span><span class="sxs-lookup"><span data-stu-id="7cb35-191">You can set one gateway cluster to be non-secure so it doesn't require a certificate for access.</span></span> <span data-ttu-id="7cb35-192">I cluster che ospitano la logica di business e i dati devono essere sicuri.</span><span class="sxs-lookup"><span data-stu-id="7cb35-192">Clusters that host business logic and data should be secure.</span></span> <span data-ttu-id="7cb35-193">È possibile abilitare il profiler in cluster di Service Fabric sia sicuri che non sicuri.</span><span class="sxs-lookup"><span data-stu-id="7cb35-193">You can enable the profiler on both secure and non-secure Service Fabric clusters.</span></span> <span data-ttu-id="7cb35-194">Questa procedura dettagliata usa un cluster non sicuro come esempio per illustrare le modifiche necessarie per abilitare il profiler.</span><span class="sxs-lookup"><span data-stu-id="7cb35-194">This walkthrough uses a non-secure cluster as an example to explain what changes are required to enable the profiler.</span></span> <span data-ttu-id="7cb35-195">È possibile effettuare il provisioning di un cluster sicuro nello stesso modo.</span><span class="sxs-lookup"><span data-stu-id="7cb35-195">You can provision a secure cluster in the same way.</span></span>

1. <span data-ttu-id="7cb35-196">Scaricare [ServiceFabricCluster.json](https://github.com/Azure/azure-docs-json-samples/blob/master/application-insights/ServiceFabricCluster.json).</span><span class="sxs-lookup"><span data-stu-id="7cb35-196">Download [ServiceFabricCluster.json](https://github.com/Azure/azure-docs-json-samples/blob/master/application-insights/ServiceFabricCluster.json).</span></span> <span data-ttu-id="7cb35-197">Come per le VM e i set di scalabilità di macchine virtuali, sostituire `Application_Insights_Key` con la propria chiave di Application Insights:</span><span class="sxs-lookup"><span data-stu-id="7cb35-197">As you did for VMs and virtual machine scale sets, replace `Application_Insights_Key` with your Application Insights key:</span></span>

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

2. <span data-ttu-id="7cb35-198">Distribuire il modello usando uno script di PowerShell:</span><span class="sxs-lookup"><span data-stu-id="7cb35-198">Deploy the template by using a PowerShell script:</span></span>

   ```
   Login-AzureRmAccount
   New-AzureRmResourceGroup -Name [Your_Resource_Group_Name] -Location [Your_Resource_Group_Location] -Verbose -Force
   New-AzureRmResourceGroupDeployment -Name [Choose_An_Arbitrary_Name] -ResourceGroupName [Your_Resource_Group_Name] -TemplateFile [Path_To_Your_Template]

   ```

### <a name="install-the-application-insights-sdk-in-the-project-and-configure-the-application-insights-key"></a><span data-ttu-id="7cb35-199">Installare Application Insights SDK nel progetto e configurare la chiave di Application Insights</span><span class="sxs-lookup"><span data-stu-id="7cb35-199">Install the Application Insights SDK in the project and configure the Application Insights key</span></span>
<span data-ttu-id="7cb35-200">Installare Application Insights SDK dal [pacchetto NuGet](https://www.nuget.org/packages/Microsoft.ApplicationInsights.Web/).</span><span class="sxs-lookup"><span data-stu-id="7cb35-200">Install the Application Insights SDK from the [NuGet package](https://www.nuget.org/packages/Microsoft.ApplicationInsights.Web/).</span></span> <span data-ttu-id="7cb35-201">Assicurarsi di installare una versione stabile, 2.3 o successiva.</span><span class="sxs-lookup"><span data-stu-id="7cb35-201">Make sure that you install a stable version, 2.3 or later.</span></span> 

<span data-ttu-id="7cb35-202">Per informazioni sulla configurazione di Application Insights nei progetti, vedere [Using Service Fabric with Application Insights](https://github.com/Azure-Samples/service-fabric-dotnet-getting-started/blob/dev/appinsights/ApplicationInsights.md) (Uso di Service Fabric con Application Insights).</span><span class="sxs-lookup"><span data-stu-id="7cb35-202">For information about configuring Application Insights in your projects, see [Using Service Fabric with Application Insights](https://github.com/Azure-Samples/service-fabric-dotnet-getting-started/blob/dev/appinsights/ApplicationInsights.md).</span></span>

### <a name="add-application-code-to-instrument-telemetry"></a><span data-ttu-id="7cb35-203">Aggiungere il codice dell'applicazione per instrumentare la telemetria</span><span class="sxs-lookup"><span data-stu-id="7cb35-203">Add application code to instrument telemetry</span></span>
1. <span data-ttu-id="7cb35-204">Per ogni parte del codice che si vuole instrumentare, aggiungere un'istruzione using.</span><span class="sxs-lookup"><span data-stu-id="7cb35-204">For any piece of code that you want to instrument, add a using statement around it.</span></span> 

   <span data-ttu-id="7cb35-205">Nell'esempio seguente il metodo `RunAsync` esegue alcune operazioni e la classe `telemetryClient` acquisisce i dati di telemetria dopo l'avvio.</span><span class="sxs-lookup"><span data-stu-id="7cb35-205">In the following  example, the `RunAsync` method is doing some work, and the `telemetryClient` class captures the telemetry after it starts.</span></span> <span data-ttu-id="7cb35-206">È necessario un nome univoco per l'evento nell'applicazione.</span><span class="sxs-lookup"><span data-stu-id="7cb35-206">The event needs a unique name across the application.</span></span>

   ```
   protected override async Task RunAsync(CancellationToken cancellationToken)
       {
           // TODO: Replace the following sample code with your own logic
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

2. <span data-ttu-id="7cb35-207">Distribuire l'applicazione nel cluster di Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="7cb35-207">Deploy your application to the Service Fabric cluster.</span></span> <span data-ttu-id="7cb35-208">Lasciare l'app in esecuzione per 10 minuti.</span><span class="sxs-lookup"><span data-stu-id="7cb35-208">Wait for the app to run for 10 minutes.</span></span> <span data-ttu-id="7cb35-209">Per un risultato migliore, è possibile eseguire un test di carico sull'app.</span><span class="sxs-lookup"><span data-stu-id="7cb35-209">For better effect, you can run a load test on the app.</span></span> <span data-ttu-id="7cb35-210">Passare al pannello **Prestazioni** del portale di Application Insights. Dovrebbero venire visualizzati gli esempi di tracce di profilatura.</span><span class="sxs-lookup"><span data-stu-id="7cb35-210">Go to the Application Insights portal's **Performance** blade, and you should see examples of profiling traces appear.</span></span>

<!---
Commenting out these sections for now
## Enable the Profiler on Cloud Services applications
[TODO]
## Enable the Profiler on classic Azure Virtual Machines
[TODO]
## Enable the Profiler on on-premise servers
[TODO]
--->

## <a name="next-steps"></a><span data-ttu-id="7cb35-211">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="7cb35-211">Next steps</span></span>

- <span data-ttu-id="7cb35-212">Per informazioni su come risolvere i problemi relativi al profiler, vedere [Risoluzione dei problemi del profiler](app-insights-profiler.md#troubleshooting).</span><span class="sxs-lookup"><span data-stu-id="7cb35-212">Find help with troubleshooting profiler issues in [Profiler troubleshooting](app-insights-profiler.md#troubleshooting).</span></span>

- <span data-ttu-id="7cb35-213">Per altre informazioni sul profiler, vedere [Application Insights Profiler](app-insights-profiler.md).</span><span class="sxs-lookup"><span data-stu-id="7cb35-213">Read more about the profiler in [Application Insights Profiler](app-insights-profiler.md).</span></span>

---
title: Creare una regola personalizzata in Azure IoT Suite | Documentazione Microsoft
description: Come creare una regola personalizzata in una soluzione IoT Suite preconfigurata.
services: 
suite: iot-suite
documentationcenter: 
author: dominicbetts
manager: timlt
editor: 
ms.assetid: 562799dc-06ea-4cdd-b822-80d1f70d2f09
ms.service: iot-suite
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/24/2017
ms.author: dobett
ms.openlocfilehash: d58c27234ea05a82aaa3e8d72f70c1449980df09
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/29/2017
---
# <a name="create-a-custom-rule-in-the-remote-monitoring-preconfigured-solution"></a><span data-ttu-id="e288b-103">Creare una regola personalizzata nella soluzione di monitoraggio remota preconfigurata</span><span class="sxs-lookup"><span data-stu-id="e288b-103">Create a custom rule in the remote monitoring preconfigured solution</span></span>

## <a name="introduction"></a><span data-ttu-id="e288b-104">Introduzione</span><span class="sxs-lookup"><span data-stu-id="e288b-104">Introduction</span></span>

<span data-ttu-id="e288b-105">Nelle soluzioni preconfigurate è possibile configurare [regole che si attivano quando un valore di telemetria per un dispositivo raggiunge una soglia specifica][lnk-builtin-rule].</span><span class="sxs-lookup"><span data-stu-id="e288b-105">In the preconfigured solutions, you can configure [rules that trigger when a telemetry value for a device reaches a specific threshold][lnk-builtin-rule].</span></span> <span data-ttu-id="e288b-106">[Usare i dati di telemetria dinamica con la soluzione di monitoraggio remoto preconfigurata][lnk-dynamic-telemetry] descrive come aggiungere alla soluzione valori di telemetria personalizzati, ad esempio *ExternalTemperature*.</span><span class="sxs-lookup"><span data-stu-id="e288b-106">[Use dynamic telemetry with the remote monitoring preconfigured solution][lnk-dynamic-telemetry] describes how you can add custom telemetry values, such as *ExternalTemperature* to your solution.</span></span> <span data-ttu-id="e288b-107">Questo articolo illustra come creare regole personalizzate per tipi di dati di telemetria dinamica nella soluzione.</span><span class="sxs-lookup"><span data-stu-id="e288b-107">This article shows you how to create custom rule for dynamic telemetry types in your solution.</span></span>

<span data-ttu-id="e288b-108">Questa esercitazione usa un semplice dispositivo simulato Node.js per generare dati di telemetria dinamica da inviare al back-end della soluzione preconfigurata.</span><span class="sxs-lookup"><span data-stu-id="e288b-108">This tutorial uses a simple Node.js simulated device to generate dynamic telemetry to send to the preconfigured solution back end.</span></span> <span data-ttu-id="e288b-109">Si aggiungeranno quindi regole personalizzate nella soluzione **RemoteMonitoring** di Visual Studio e si distribuirà questo back-end personalizzato alla sottoscrizione di Azure.</span><span class="sxs-lookup"><span data-stu-id="e288b-109">You then add custom rules in the **RemoteMonitoring** Visual Studio solution and deploy this customized back end to your Azure subscription.</span></span>

<span data-ttu-id="e288b-110">Per completare questa esercitazione, sono necessari:</span><span class="sxs-lookup"><span data-stu-id="e288b-110">To complete this tutorial, you need:</span></span>

* <span data-ttu-id="e288b-111">Una sottoscrizione di Azure attiva.</span><span class="sxs-lookup"><span data-stu-id="e288b-111">An active Azure subscription.</span></span> <span data-ttu-id="e288b-112">Se non si dispone di un account, è possibile creare un account di valutazione gratuita in pochi minuti.</span><span class="sxs-lookup"><span data-stu-id="e288b-112">If you don’t have an account, you can create a free trial account in just a couple of minutes.</span></span> <span data-ttu-id="e288b-113">Per informazioni dettagliate, vedere la pagina relativa alla [versione di valutazione gratuita di Azure][lnk_free_trial].</span><span class="sxs-lookup"><span data-stu-id="e288b-113">For details, see [Azure Free Trial][lnk_free_trial].</span></span>
* <span data-ttu-id="e288b-114">[Node.js][lnk-node] versione 0.12.x o successiva per creare un dispositivo simulato.</span><span class="sxs-lookup"><span data-stu-id="e288b-114">[Node.js][lnk-node] version 0.12.x or later to create a simulated device.</span></span>
* <span data-ttu-id="e288b-115">Visual Studio 2015 o Visual Studio 2017 per modificare nuovamente il back-end della soluzione preconfigurata con le nuove regole.</span><span class="sxs-lookup"><span data-stu-id="e288b-115">Visual Studio 2015 or Visual Studio 2017 to modify the preconfigured solution back end with your new rules.</span></span>

[!INCLUDE [iot-suite-provision-remote-monitoring](../../includes/iot-suite-provision-remote-monitoring.md)]

<span data-ttu-id="e288b-116">Prendere nota del nome della soluzione che si è scelto per la distribuzione.</span><span class="sxs-lookup"><span data-stu-id="e288b-116">Make a note of the solution name you chose for your deployment.</span></span> <span data-ttu-id="e288b-117">Il nome della soluzione sarà necessario più avanti nell'esercitazione.</span><span class="sxs-lookup"><span data-stu-id="e288b-117">You need this solution name later in this tutorial.</span></span>

[!INCLUDE [iot-suite-send-external-temperature](../../includes/iot-suite-send-external-temperature.md)]

<span data-ttu-id="e288b-118">È possibile arrestare l'applicazione console Node.js dopo avere verificato che sta inviando i dati di telemetria **ExternalTemperature** alla soluzione preconfigurata.</span><span class="sxs-lookup"><span data-stu-id="e288b-118">You can stop the Node.js console app when you have verified that it is sending **ExternalTemperature** telemetry to the preconfigured solution.</span></span> <span data-ttu-id="e288b-119">Mantenere aperta la finestra della console in quanto si eseguirà nuovamente l'applicazione console Node.js dopo aver aggiunto la regola personalizzata alla soluzione.</span><span class="sxs-lookup"><span data-stu-id="e288b-119">Keep the console window open because you run this Node.js console app again after you add the custom rule to the solution.</span></span>

## <a name="rule-storage-locations"></a><span data-ttu-id="e288b-120">Posizioni di archiviazione delle regole</span><span class="sxs-lookup"><span data-stu-id="e288b-120">Rule storage locations</span></span>

<span data-ttu-id="e288b-121">Le informazioni sulle regole vengono mantenute in due posizioni:</span><span class="sxs-lookup"><span data-stu-id="e288b-121">Information about rules is persisted in two locations:</span></span>

* <span data-ttu-id="e288b-122">Tabella **DeviceRulesNormalizedTable**: questa tabella archivia un riferimento normalizzato alle regole definite dal portale della soluzione.</span><span class="sxs-lookup"><span data-stu-id="e288b-122">**DeviceRulesNormalizedTable** table – This table stores a normalized reference to the rules defined by the solution portal.</span></span> <span data-ttu-id="e288b-123">Quando il portale della soluzione visualizza le regole del dispositivo, interroga questa tabella per trovare le definizioni delle regole.</span><span class="sxs-lookup"><span data-stu-id="e288b-123">When the solution portal displays device rules, it queries this table for the rule definitions.</span></span>
* <span data-ttu-id="e288b-124">BLOB **DeviceRules**: questo BLOB archivia tutte le regole definite per tutti i dispositivi registrati ed è definito come input di riferimento per i processi di analisi di flusso di Azure.</span><span class="sxs-lookup"><span data-stu-id="e288b-124">**DeviceRules** blob – This blob stores all the rules defined for all registered devices and is defined as a reference input to the Azure Stream Analytics jobs.</span></span>
 
<span data-ttu-id="e288b-125">Quando si aggiorna una regola esistente o si definisce una nuova regola nel portale della soluzione, sia la tabella sia il BLOB vengono aggiornati per riflettere le modifiche.</span><span class="sxs-lookup"><span data-stu-id="e288b-125">When you update an existing rule or define a new rule in the solution portal, both the table and blob are updated to reflect the changes.</span></span> <span data-ttu-id="e288b-126">La definizione della regola visualizzata nel portale proviene dall'archivio tabelle e la definizione della regola a cui fanno riferimento i processi di analisi di flusso proviene dal BLOB.</span><span class="sxs-lookup"><span data-stu-id="e288b-126">The rule definition displayed in the portal comes from the table store, and the rule definition referenced by the Stream Analytics jobs comes from the blob.</span></span> 

## <a name="update-the-remotemonitoring-visual-studio-solution"></a><span data-ttu-id="e288b-127">Aggiornare la soluzione RemoteMonitoring di Visual Studio</span><span class="sxs-lookup"><span data-stu-id="e288b-127">Update the RemoteMonitoring Visual Studio solution</span></span>

<span data-ttu-id="e288b-128">La procedura seguente mostra come modificare la soluzione RemoteMonitoring di Visual Studio per includere una nuova regola che usa i dati di telemetria **ExternalTemperature** inviati dal dispositivo simulato:</span><span class="sxs-lookup"><span data-stu-id="e288b-128">The following steps show you how to modify the RemoteMonitoring Visual Studio solution to include a new rule that uses the **ExternalTemperature** telemetry sent from the simulated device:</span></span>

1. <span data-ttu-id="e288b-129">Se non è ancora stato fatto, clonare il repository **azure-iot-remote-monitoring** in un percorso appropriato nel computer locale usando il comando Git seguente:</span><span class="sxs-lookup"><span data-stu-id="e288b-129">If you have not already done so, clone the **azure-iot-remote-monitoring** repository to a suitable location on your local machine using the following Git command:</span></span>

    ```
    git clone https://github.com/Azure/azure-iot-remote-monitoring.git
    ```

2. <span data-ttu-id="e288b-130">In Visual Studio aprire il file RemoteMonitoring.sln dalla copia locale del repository **azure-iot-remote-monitoring**.</span><span class="sxs-lookup"><span data-stu-id="e288b-130">In Visual Studio, open the RemoteMonitoring.sln file from your local copy of the **azure-iot-remote-monitoring** repository.</span></span>

3. <span data-ttu-id="e288b-131">Aprire il file Infrastructure\Models\DeviceRuleBlobEntity.cs e aggiungere una proprietà **ExternalTemperature** come segue:</span><span class="sxs-lookup"><span data-stu-id="e288b-131">Open the file Infrastructure\Models\DeviceRuleBlobEntity.cs and add an **ExternalTemperature** property as follows:</span></span>

    ```csharp
    public double? Temperature { get; set; }
    public double? Humidity { get; set; }
    public double? ExternalTemperature { get; set; }
    ```

4. <span data-ttu-id="e288b-132">Nello stesso file aggiungere una proprietà **ExternalTemperatureRuleOutput** come indicato di seguito:</span><span class="sxs-lookup"><span data-stu-id="e288b-132">In the same file, add an **ExternalTemperatureRuleOutput** property as follows:</span></span>

    ```csharp
    public string TemperatureRuleOutput { get; set; }
    public string HumidityRuleOutput { get; set; }
    public string ExternalTemperatureRuleOutput { get; set; }
    ```

5. <span data-ttu-id="e288b-133">Aprire il file Infrastructure\Models\DeviceRuleDataFields.cs e aggiungere la seguente proprietà **ExternalTemperature** dopo la proprietà **Humidity** esistente:</span><span class="sxs-lookup"><span data-stu-id="e288b-133">Open the file Infrastructure\Models\DeviceRuleDataFields.cs and add the following **ExternalTemperature** property after the existing **Humidity** property:</span></span>

    ```csharp
    public static string ExternalTemperature
    {
        get { return "ExternalTemperature"; }
    }
    ```

6. <span data-ttu-id="e288b-134">Nello stesso file aggiornare il metodo **_availableDataFields** in modo che includa **ExternalTemperature** come segue:</span><span class="sxs-lookup"><span data-stu-id="e288b-134">In the same file, update the **_availableDataFields** method to include **ExternalTemperature** as follows:</span></span>

    ```csharp
    private static List<string> _availableDataFields = new List<string>
    {                    
        Temperature, Humidity, ExternalTemperature
    };
    ```

7. <span data-ttu-id="e288b-135">Aprire il file Infrastructure\Repository\DeviceRulesRepository.cs e modificare il metodo **BuildBlobEntityListFromTableRows** come segue:</span><span class="sxs-lookup"><span data-stu-id="e288b-135">Open the file Infrastructure\Repository\DeviceRulesRepository.cs and modify the **BuildBlobEntityListFromTableRows** method as follows:</span></span>

    ```csharp
    else if (rule.DataField == DeviceRuleDataFields.Humidity)
    {
        entity.Humidity = rule.Threshold;
        entity.HumidityRuleOutput = rule.RuleOutput;
    }
    else if (rule.DataField == DeviceRuleDataFields.ExternalTemperature)
    {
      entity.ExternalTemperature = rule.Threshold;
      entity.ExternalTemperatureRuleOutput = rule.RuleOutput;
    }
    ```

## <a name="rebuild-and-redeploy-the-solution"></a><span data-ttu-id="e288b-136">Ricompilare e ridistribuire la soluzione.</span><span class="sxs-lookup"><span data-stu-id="e288b-136">Rebuild and redeploy the solution.</span></span>

<span data-ttu-id="e288b-137">È ora possibile distribuire la soluzione aggiornata alla sottoscrizione di Azure.</span><span class="sxs-lookup"><span data-stu-id="e288b-137">You can now deploy the updated solution to your Azure subscription.</span></span>

1. <span data-ttu-id="e288b-138">Aprire un prompt dei comandi con privilegi elevati e passare alla radice della copia locale del repository azure-iot-remote-monitoring.</span><span class="sxs-lookup"><span data-stu-id="e288b-138">Open an elevated command prompt and navigate to the root of your local copy of the azure-iot-remote-monitoring repository.</span></span>

2. <span data-ttu-id="e288b-139">Per distribuire la soluzione aggiornata, eseguire il comando seguente sostituendo **{nome distribuzione}** con il nome della distribuzione della soluzione preconfigurata annotato in precedenza:</span><span class="sxs-lookup"><span data-stu-id="e288b-139">To deploy your updated solution, run the following command substituting **{deployment name}** with the name of your preconfigured solution deployment that you noted previously:</span></span>

    ```
    build.cmd cloud release {deployment name}
    ```

## <a name="update-the-stream-analytics-job"></a><span data-ttu-id="e288b-140">Aggiornare il processo di analisi di flusso</span><span class="sxs-lookup"><span data-stu-id="e288b-140">Update the Stream Analytics job</span></span>

<span data-ttu-id="e288b-141">Dopo aver completato la distribuzione, è possibile aggiornare il processo di analisi di flusso in modo che usi le nuove definizioni delle regole.</span><span class="sxs-lookup"><span data-stu-id="e288b-141">When the deployment is complete, you can update the Stream Analytics job to use the new rule definitions.</span></span>

1. <span data-ttu-id="e288b-142">Nel portale di Azure passare al gruppo di risorse che contiene le risorse della soluzione preconfigurata.</span><span class="sxs-lookup"><span data-stu-id="e288b-142">In the Azure portal, navigate to the resource group that contains your preconfigured solution resources.</span></span> <span data-ttu-id="e288b-143">Questo gruppo di risorse ha lo stesso nome specificato per la soluzione durante la distribuzione.</span><span class="sxs-lookup"><span data-stu-id="e288b-143">This resource group has the same name you specified for the solution during the deployment.</span></span>

2. <span data-ttu-id="e288b-144">Passare al processo di analisi di flusso {nome distribuzione}-Regole.</span><span class="sxs-lookup"><span data-stu-id="e288b-144">Navigate to the {deployment name}-Rules Stream Analytics job.</span></span> 

3. <span data-ttu-id="e288b-145">Fare clic su **Stop** per arrestare l'esecuzione del processo di analisi di flusso.</span><span class="sxs-lookup"><span data-stu-id="e288b-145">Click **Stop** to stop the Stream Analytics job from running.</span></span> <span data-ttu-id="e288b-146">È necessario attendere che il processo di analisi di flusso si arresti prima di poter modificare la query.</span><span class="sxs-lookup"><span data-stu-id="e288b-146">(You must wait for the streaming job to stop before you can edit the query).</span></span>

4. <span data-ttu-id="e288b-147">Fare clic su **Query**.</span><span class="sxs-lookup"><span data-stu-id="e288b-147">Click **Query**.</span></span> <span data-ttu-id="e288b-148">Modificare la query aggiungendo l'istruzione **SELECT** per **ExternalTemperature**.</span><span class="sxs-lookup"><span data-stu-id="e288b-148">Edit the query to include the **SELECT** statement for **ExternalTemperature**.</span></span> <span data-ttu-id="e288b-149">L'esempio seguente illustra la query completa con la nuova istruzione **SELECT**:</span><span class="sxs-lookup"><span data-stu-id="e288b-149">The following sample shows the complete query with the new **SELECT** statement:</span></span>

    ```
    WITH AlarmsData AS 
    (
    SELECT
         Stream.IoTHub.ConnectionDeviceId AS DeviceId,
         'Temperature' as ReadingType,
         Stream.Temperature as Reading,
         Ref.Temperature as Threshold,
         Ref.TemperatureRuleOutput as RuleOutput,
         Stream.EventEnqueuedUtcTime AS [Time]
    FROM IoTTelemetryStream Stream
    JOIN DeviceRulesBlob Ref ON Stream.IoTHub.ConnectionDeviceId = Ref.DeviceID
    WHERE
         Ref.Temperature IS NOT null AND Stream.Temperature > Ref.Temperature
     
    UNION ALL
     
    SELECT
         Stream.IoTHub.ConnectionDeviceId AS DeviceId,
         'Humidity' as ReadingType,
         Stream.Humidity as Reading,
         Ref.Humidity as Threshold,
         Ref.HumidityRuleOutput as RuleOutput,
         Stream.EventEnqueuedUtcTime AS [Time]
    FROM IoTTelemetryStream Stream
    JOIN DeviceRulesBlob Ref ON Stream.IoTHub.ConnectionDeviceId = Ref.DeviceID
    WHERE
         Ref.Humidity IS NOT null AND Stream.Humidity > Ref.Humidity
     
    UNION ALL
     
    SELECT
         Stream.IoTHub.ConnectionDeviceId AS DeviceId,
         'ExternalTemperature' as ReadingType,
         Stream.ExternalTemperature as Reading,
         Ref.ExternalTemperature as Threshold,
         Ref.ExternalTemperatureRuleOutput as RuleOutput,
         Stream.EventEnqueuedUtcTime AS [Time]
    FROM IoTTelemetryStream Stream
    JOIN DeviceRulesBlob Ref ON Stream.IoTHub.ConnectionDeviceId = Ref.DeviceID
    WHERE
         Ref.ExternalTemperature IS NOT null AND Stream.ExternalTemperature > Ref.ExternalTemperature
    )
     
    SELECT *
    INTO DeviceRulesMonitoring
    FROM AlarmsData
     
    SELECT *
    INTO DeviceRulesHub
    FROM AlarmsData
    ```

5. <span data-ttu-id="e288b-150">Fare clic su **Salva** per modificare la query di regola aggiornata.</span><span class="sxs-lookup"><span data-stu-id="e288b-150">Click **Save** to change the updated rule query.</span></span>

6. <span data-ttu-id="e288b-151">Fare clic su **Avvia** per avviare nuovamente il processo di analisi di flusso.</span><span class="sxs-lookup"><span data-stu-id="e288b-151">Click **Start** to start the Stream Analytics job running again.</span></span>

## <a name="add-your-new-rule-in-the-dashboard"></a><span data-ttu-id="e288b-152">Aggiungere la nuova regola nel dashboard</span><span class="sxs-lookup"><span data-stu-id="e288b-152">Add your new rule in the dashboard</span></span>

<span data-ttu-id="e288b-153">È ora possibile aggiungere la regola **ExternalTemperature** a un dispositivo nel dashboard della soluzione.</span><span class="sxs-lookup"><span data-stu-id="e288b-153">You can now add the **ExternalTemperature** rule to a device in the solution dashboard.</span></span>

1. <span data-ttu-id="e288b-154">Passare al portale della soluzione.</span><span class="sxs-lookup"><span data-stu-id="e288b-154">Navigate to the solution portal.</span></span>

2. <span data-ttu-id="e288b-155">Passare al pannello **Dispositivi**.</span><span class="sxs-lookup"><span data-stu-id="e288b-155">Navigate to the **Devices** panel.</span></span>

3. <span data-ttu-id="e288b-156">Individuare il dispositivo personalizzato che è stato creato che invia i dati di telemetria **ExternalTemperature** e nel pannello **Dettagli dispositivo** fare clic su **Aggiungi regola**.</span><span class="sxs-lookup"><span data-stu-id="e288b-156">Locate the custom device you created that sends **ExternalTemperature** telemetry and on the **Device Details** panel, click **Add Rule**.</span></span>

4. <span data-ttu-id="e288b-157">Selezionare **ExternalTemperature** in **Campo dati**.</span><span class="sxs-lookup"><span data-stu-id="e288b-157">Select **ExternalTemperature** in **Data Field**.</span></span>

5. <span data-ttu-id="e288b-158">Impostare **Soglia** su 56.</span><span class="sxs-lookup"><span data-stu-id="e288b-158">Set **Threshold** to 56.</span></span> <span data-ttu-id="e288b-159">Quindi fare clic su **Salva e visualizza regole**.</span><span class="sxs-lookup"><span data-stu-id="e288b-159">Then click **Save and view rules**.</span></span>

6. <span data-ttu-id="e288b-160">Tornare al dashboard per visualizzare la cronologia avvisi.</span><span class="sxs-lookup"><span data-stu-id="e288b-160">Return to the dashboard to view the alarm history.</span></span>

7. <span data-ttu-id="e288b-161">Nella finestra della console che è stata lasciata aperta avviare l'applicazione console Node.js per iniziare a inviare i dati di telemetria **ExternalTemperature**.</span><span class="sxs-lookup"><span data-stu-id="e288b-161">In the console window you left open, start the Node.js console app to begin sending **ExternalTemperature** telemetry data.</span></span>

8. <span data-ttu-id="e288b-162">Si noti che la tabella **Cronologia avvisi** mostra nuovi avvisi quando viene attivata la nuova regola.</span><span class="sxs-lookup"><span data-stu-id="e288b-162">Notice that the **Alarm History** table shows new alarms when the new rule is triggered.</span></span>
 
## <a name="additional-information"></a><span data-ttu-id="e288b-163">Informazioni aggiuntive</span><span class="sxs-lookup"><span data-stu-id="e288b-163">Additional information</span></span>

<span data-ttu-id="e288b-164">Modificare l'operatore  **>**  è più complesso ed esula dalla procedura descritta in questa esercitazione.</span><span class="sxs-lookup"><span data-stu-id="e288b-164">Changing the operator **>** is more complex and goes beyond the steps outlined in this tutorial.</span></span> <span data-ttu-id="e288b-165">Mentre è possibile modificare il processo di analisi di flusso perché usi qualsiasi operatore desiderato, riflettere tale operatore nel portale della soluzione è un'attività più complessa.</span><span class="sxs-lookup"><span data-stu-id="e288b-165">While you can change the Stream Analytics job to use whatever operator you like, reflecting that operator in the solution portal is a more complex task.</span></span> 

## <a name="next-steps"></a><span data-ttu-id="e288b-166">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="e288b-166">Next steps</span></span>
<span data-ttu-id="e288b-167">Ora che si è appreso come creare regole personalizzate, è possibile vedere altre informazioni sulle soluzioni preconfigurate:</span><span class="sxs-lookup"><span data-stu-id="e288b-167">Now that you've seen how to create custom rules, you can learn more about the preconfigured solutions:</span></span>

- <span data-ttu-id="e288b-168">[Connettere l'app per la logica alla soluzione preconfigurata per il monitoraggio remoto Azure IoT Suite][lnk-logic-app]</span><span class="sxs-lookup"><span data-stu-id="e288b-168">[Connect Logic App to your Azure IoT Suite Remote Monitoring preconfigured solution][lnk-logic-app]</span></span>
- <span data-ttu-id="e288b-169">[Metadati di informazioni sul dispositivo nella soluzione preconfigurata per il monitoraggio remoto][lnk-devinfo].</span><span class="sxs-lookup"><span data-stu-id="e288b-169">[Device information metadata in the remote monitoring preconfigured solution][lnk-devinfo].</span></span>

[lnk-devinfo]: iot-suite-remote-monitoring-device-info.md

[lnk_free_trial]: http://azure.microsoft.com/pricing/free-trial/
[lnk-node]: http://nodejs.org
[lnk-builtin-rule]: iot-suite-getstarted-preconfigured-solutions.md#view-alarms
[lnk-dynamic-telemetry]: iot-suite-dynamic-telemetry.md
[lnk-logic-app]: iot-suite-logic-apps-tutorial.md
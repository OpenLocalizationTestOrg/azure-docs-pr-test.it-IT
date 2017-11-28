---
title: una regola personalizzata in Azure IoT Suite aaaCreate | Documenti Microsoft
description: Una regola personalizzata in un gruppo di IoT toocreate preconfigurato come soluzione.
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
ms.openlocfilehash: 6c5bb2ca54f3f17b99ad482e727c8e9fa28d7fe5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-custom-rule-in-hello-remote-monitoring-preconfigured-solution"></a><span data-ttu-id="e02aa-103">Creare una regola personalizzata in hello soluzione preconfigurata di monitoraggio remoto</span><span class="sxs-lookup"><span data-stu-id="e02aa-103">Create a custom rule in hello remote monitoring preconfigured solution</span></span>

## <a name="introduction"></a><span data-ttu-id="e02aa-104">Introduzione</span><span class="sxs-lookup"><span data-stu-id="e02aa-104">Introduction</span></span>

<span data-ttu-id="e02aa-105">Nelle soluzioni hello preconfigurato, è possibile configurare [regole che attivano quando un telemetria valore per un dispositivo raggiunge una soglia specifica][lnk-builtin-rule].</span><span class="sxs-lookup"><span data-stu-id="e02aa-105">In hello preconfigured solutions, you can configure [rules that trigger when a telemetry value for a device reaches a specific threshold][lnk-builtin-rule].</span></span> <span data-ttu-id="e02aa-106">[Utilizzare i dati di telemetria dinamico con hello soluzione preconfigurata di monitoraggio remoto] [ lnk-dynamic-telemetry] descrive come è possibile aggiungere valori di dati di telemetria personalizzati, ad esempio *ExternalTemperature* tooyour soluzione.</span><span class="sxs-lookup"><span data-stu-id="e02aa-106">[Use dynamic telemetry with hello remote monitoring preconfigured solution][lnk-dynamic-telemetry] describes how you can add custom telemetry values, such as *ExternalTemperature* tooyour solution.</span></span> <span data-ttu-id="e02aa-107">In questo articolo viene illustrato come tipi di toocreate regola personalizzata per dati di telemetria dinamico nella soluzione.</span><span class="sxs-lookup"><span data-stu-id="e02aa-107">This article shows you how toocreate custom rule for dynamic telemetry types in your solution.</span></span>

<span data-ttu-id="e02aa-108">Questa esercitazione viene utilizzato un semplice Node.js dispositivo simulato toogenerate telemetria dinamica toosend toohello soluzione preconfigurata back-end.</span><span class="sxs-lookup"><span data-stu-id="e02aa-108">This tutorial uses a simple Node.js simulated device toogenerate dynamic telemetry toosend toohello preconfigured solution back end.</span></span> <span data-ttu-id="e02aa-109">Aggiungere quindi una serie di regole personalizzate in hello **RemoteMonitoring** soluzione di Visual Studio e distribuire questo tooyour back-end personalizzato sottoscrizione di Azure.</span><span class="sxs-lookup"><span data-stu-id="e02aa-109">You then add custom rules in hello **RemoteMonitoring** Visual Studio solution and deploy this customized back end tooyour Azure subscription.</span></span>

<span data-ttu-id="e02aa-110">toocomplete questa esercitazione, è necessario:</span><span class="sxs-lookup"><span data-stu-id="e02aa-110">toocomplete this tutorial, you need:</span></span>

* <span data-ttu-id="e02aa-111">Una sottoscrizione di Azure attiva.</span><span class="sxs-lookup"><span data-stu-id="e02aa-111">An active Azure subscription.</span></span> <span data-ttu-id="e02aa-112">Se non si dispone di un account, è possibile creare un account di valutazione gratuita in pochi minuti.</span><span class="sxs-lookup"><span data-stu-id="e02aa-112">If you don’t have an account, you can create a free trial account in just a couple of minutes.</span></span> <span data-ttu-id="e02aa-113">Per informazioni dettagliate, vedere la pagina relativa alla [versione di valutazione gratuita di Azure][lnk_free_trial].</span><span class="sxs-lookup"><span data-stu-id="e02aa-113">For details, see [Azure Free Trial][lnk_free_trial].</span></span>
* <span data-ttu-id="e02aa-114">[Node.js] [ lnk-node] versione 0.12.x o versioni successive toocreate un dispositivo simulato.</span><span class="sxs-lookup"><span data-stu-id="e02aa-114">[Node.js][lnk-node] version 0.12.x or later toocreate a simulated device.</span></span>
* <span data-ttu-id="e02aa-115">Visual Studio 2015 o Visual Studio 2017 toomodify hello preconfigurato soluzione nuovamente terminare con le nuove regole.</span><span class="sxs-lookup"><span data-stu-id="e02aa-115">Visual Studio 2015 or Visual Studio 2017 toomodify hello preconfigured solution back end with your new rules.</span></span>

[!INCLUDE [iot-suite-provision-remote-monitoring](../../includes/iot-suite-provision-remote-monitoring.md)]

<span data-ttu-id="e02aa-116">Prendere nota del nome di soluzione hello che scelto per la distribuzione.</span><span class="sxs-lookup"><span data-stu-id="e02aa-116">Make a note of hello solution name you chose for your deployment.</span></span> <span data-ttu-id="e02aa-117">Il nome della soluzione sarà necessario più avanti nell'esercitazione.</span><span class="sxs-lookup"><span data-stu-id="e02aa-117">You need this solution name later in this tutorial.</span></span>

[!INCLUDE [iot-suite-send-external-temperature](../../includes/iot-suite-send-external-temperature.md)]

<span data-ttu-id="e02aa-118">È possibile arrestare l'applicazione console in Node.js hello dopo avere verificato che stia inviando **ExternalTemperature** toohello telemetria preconfigurato soluzione.</span><span class="sxs-lookup"><span data-stu-id="e02aa-118">You can stop hello Node.js console app when you have verified that it is sending **ExternalTemperature** telemetry toohello preconfigured solution.</span></span> <span data-ttu-id="e02aa-119">Mantenere aperta la finestra di console hello perché si esegue nuovamente l'app console Node.js dopo aver aggiunto una soluzione di toohello hello regola personalizzata.</span><span class="sxs-lookup"><span data-stu-id="e02aa-119">Keep hello console window open because you run this Node.js console app again after you add hello custom rule toohello solution.</span></span>

## <a name="rule-storage-locations"></a><span data-ttu-id="e02aa-120">Posizioni di archiviazione delle regole</span><span class="sxs-lookup"><span data-stu-id="e02aa-120">Rule storage locations</span></span>

<span data-ttu-id="e02aa-121">Le informazioni sulle regole vengono mantenute in due posizioni:</span><span class="sxs-lookup"><span data-stu-id="e02aa-121">Information about rules is persisted in two locations:</span></span>

* <span data-ttu-id="e02aa-122">**DeviceRulesNormalizedTable** -questa tabella archivia un normalizzato fanno riferimento a regole toohello definite dal portale di soluzione hello.</span><span class="sxs-lookup"><span data-stu-id="e02aa-122">**DeviceRulesNormalizedTable** table – This table stores a normalized reference toohello rules defined by hello solution portal.</span></span> <span data-ttu-id="e02aa-123">Quando il portale di soluzione hello Visualizza le regole del dispositivo, viene eseguita una query in questa tabella per le definizioni delle regole di hello.</span><span class="sxs-lookup"><span data-stu-id="e02aa-123">When hello solution portal displays device rules, it queries this table for hello rule definitions.</span></span>
* <span data-ttu-id="e02aa-124">**DeviceRules** blob: blob archivia tutte le regole di hello definite per tutti i dispositivi registrati e viene definiti come processi di Azure flusso Analitica toohello input un riferimento.</span><span class="sxs-lookup"><span data-stu-id="e02aa-124">**DeviceRules** blob – This blob stores all hello rules defined for all registered devices and is defined as a reference input toohello Azure Stream Analytics jobs.</span></span>
 
<span data-ttu-id="e02aa-125">Quando si aggiorna una regola esistente o definita una nuova regola nel portale di soluzione hello sia la tabella di hello blob sono modifiche hello tooreflect aggiornato.</span><span class="sxs-lookup"><span data-stu-id="e02aa-125">When you update an existing rule or define a new rule in hello solution portal, both hello table and blob are updated tooreflect hello changes.</span></span> <span data-ttu-id="e02aa-126">regola Hello definizione visualizzata nel portale di hello proviene dall'archivio tabelle hello e regola hello definizione fa riferimento a processi di flusso Analitica hello proviene dal blob hello.</span><span class="sxs-lookup"><span data-stu-id="e02aa-126">hello rule definition displayed in hello portal comes from hello table store, and hello rule definition referenced by hello Stream Analytics jobs comes from hello blob.</span></span> 

## <a name="update-hello-remotemonitoring-visual-studio-solution"></a><span data-ttu-id="e02aa-127">Aggiornare qualsiasi soluzione di Visual Studio RemoteMonitoring hello</span><span class="sxs-lookup"><span data-stu-id="e02aa-127">Update hello RemoteMonitoring Visual Studio solution</span></span>

<span data-ttu-id="e02aa-128">Hello passaggi seguenti viene illustrato come toomodify hello tooinclude soluzione Visual Studio RemoteMonitoring una nuova regola che usi hello **ExternalTemperature** telemetria inviato dal dispositivo simulato hello:</span><span class="sxs-lookup"><span data-stu-id="e02aa-128">hello following steps show you how toomodify hello RemoteMonitoring Visual Studio solution tooinclude a new rule that uses hello **ExternalTemperature** telemetry sent from hello simulated device:</span></span>

1. <span data-ttu-id="e02aa-129">Se non si è già fatto, hello clone **azure iot-remoto monitoraggio** percorso del repository tooa appropriato nel computer locale utilizzando hello Git comando seguente:</span><span class="sxs-lookup"><span data-stu-id="e02aa-129">If you have not already done so, clone hello **azure-iot-remote-monitoring** repository tooa suitable location on your local machine using hello following Git command:</span></span>

    ```
    git clone https://github.com/Azure/azure-iot-remote-monitoring.git
    ```

2. <span data-ttu-id="e02aa-130">In Visual Studio, aprire il file di RemoteMonitoring.sln hello dalla copia locale di hello **azure iot-remoto monitoraggio** repository.</span><span class="sxs-lookup"><span data-stu-id="e02aa-130">In Visual Studio, open hello RemoteMonitoring.sln file from your local copy of hello **azure-iot-remote-monitoring** repository.</span></span>

3. <span data-ttu-id="e02aa-131">Aprire il file hello Infrastructure\Models\DeviceRuleBlobEntity.cs e aggiungere un **ExternalTemperature** proprietà come indicato di seguito:</span><span class="sxs-lookup"><span data-stu-id="e02aa-131">Open hello file Infrastructure\Models\DeviceRuleBlobEntity.cs and add an **ExternalTemperature** property as follows:</span></span>

    ```csharp
    public double? Temperature { get; set; }
    public double? Humidity { get; set; }
    public double? ExternalTemperature { get; set; }
    ```

4. <span data-ttu-id="e02aa-132">In hello stesso file, aggiungere un **ExternalTemperatureRuleOutput** proprietà come indicato di seguito:</span><span class="sxs-lookup"><span data-stu-id="e02aa-132">In hello same file, add an **ExternalTemperatureRuleOutput** property as follows:</span></span>

    ```csharp
    public string TemperatureRuleOutput { get; set; }
    public string HumidityRuleOutput { get; set; }
    public string ExternalTemperatureRuleOutput { get; set; }
    ```

5. <span data-ttu-id="e02aa-133">Aprire il file hello Infrastructure\Models\DeviceRuleDataFields.cs e aggiungere il seguente hello **ExternalTemperature** proprietà dopo hello esistente **umidità** proprietà:</span><span class="sxs-lookup"><span data-stu-id="e02aa-133">Open hello file Infrastructure\Models\DeviceRuleDataFields.cs and add hello following **ExternalTemperature** property after hello existing **Humidity** property:</span></span>

    ```csharp
    public static string ExternalTemperature
    {
        get { return "ExternalTemperature"; }
    }
    ```

6. <span data-ttu-id="e02aa-134">Nel file stesso hello, aggiornare hello **_availableDataFields** metodo tooinclude **ExternalTemperature** come indicato di seguito:</span><span class="sxs-lookup"><span data-stu-id="e02aa-134">In hello same file, update hello **_availableDataFields** method tooinclude **ExternalTemperature** as follows:</span></span>

    ```csharp
    private static List<string> _availableDataFields = new List<string>
    {                    
        Temperature, Humidity, ExternalTemperature
    };
    ```

7. <span data-ttu-id="e02aa-135">Aprire il file hello Infrastructure\Repository\DeviceRulesRepository.cs e modificare hello **BuildBlobEntityListFromTableRows** metodo come indicato di seguito:</span><span class="sxs-lookup"><span data-stu-id="e02aa-135">Open hello file Infrastructure\Repository\DeviceRulesRepository.cs and modify hello **BuildBlobEntityListFromTableRows** method as follows:</span></span>

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

## <a name="rebuild-and-redeploy-hello-solution"></a><span data-ttu-id="e02aa-136">Ricompilare e ridistribuire la soluzione hello.</span><span class="sxs-lookup"><span data-stu-id="e02aa-136">Rebuild and redeploy hello solution.</span></span>

<span data-ttu-id="e02aa-137">È ora possibile distribuire hello aggiornato soluzione tooyour sottoscrizione di Azure.</span><span class="sxs-lookup"><span data-stu-id="e02aa-137">You can now deploy hello updated solution tooyour Azure subscription.</span></span>

1. <span data-ttu-id="e02aa-138">Aprire un prompt dei comandi con privilegi elevati e passare toohello radice della copia locale del repository di hello azure iot-remoto monitoraggio.</span><span class="sxs-lookup"><span data-stu-id="e02aa-138">Open an elevated command prompt and navigate toohello root of your local copy of hello azure-iot-remote-monitoring repository.</span></span>

2. <span data-ttu-id="e02aa-139">toodeploy la soluzione aggiornata, eseguire hello seguente sostituendo comando **{nome distribuzione}** con nome hello della distribuzione di soluzioni preconfigurate che si è preso nota in precedenza:</span><span class="sxs-lookup"><span data-stu-id="e02aa-139">toodeploy your updated solution, run hello following command substituting **{deployment name}** with hello name of your preconfigured solution deployment that you noted previously:</span></span>

    ```
    build.cmd cloud release {deployment name}
    ```

## <a name="update-hello-stream-analytics-job"></a><span data-ttu-id="e02aa-140">Aggiornare il processo di flusso Analitica hello</span><span class="sxs-lookup"><span data-stu-id="e02aa-140">Update hello Stream Analytics job</span></span>

<span data-ttu-id="e02aa-141">Una volta completata la distribuzione di hello, è possibile aggiornare hello Analitica flusso processo toouse hello nuove definizioni regole.</span><span class="sxs-lookup"><span data-stu-id="e02aa-141">When hello deployment is complete, you can update hello Stream Analytics job toouse hello new rule definitions.</span></span>

1. <span data-ttu-id="e02aa-142">Nel portale di Azure hello, passare toohello gruppo di risorse che contiene le risorse della soluzione preconfigurata.</span><span class="sxs-lookup"><span data-stu-id="e02aa-142">In hello Azure portal, navigate toohello resource group that contains your preconfigured solution resources.</span></span> <span data-ttu-id="e02aa-143">Questo gruppo di risorse hello stesso nome è specificato per hello soluzione durante la distribuzione di hello.</span><span class="sxs-lookup"><span data-stu-id="e02aa-143">This resource group has hello same name you specified for hello solution during hello deployment.</span></span>

2. <span data-ttu-id="e02aa-144">Passare toohello {nome distribuzione}-processo regole flusso Analitica.</span><span class="sxs-lookup"><span data-stu-id="e02aa-144">Navigate toohello {deployment name}-Rules Stream Analytics job.</span></span> 

3. <span data-ttu-id="e02aa-145">Fare clic su **arrestare** toostop hello Analitica flusso processo in esecuzione.</span><span class="sxs-lookup"><span data-stu-id="e02aa-145">Click **Stop** toostop hello Stream Analytics job from running.</span></span> <span data-ttu-id="e02aa-146">(È necessario attendere hello toostop processo di streaming prima di poter modificare query hello).</span><span class="sxs-lookup"><span data-stu-id="e02aa-146">(You must wait for hello streaming job toostop before you can edit hello query).</span></span>

4. <span data-ttu-id="e02aa-147">Fare clic su **Query**.</span><span class="sxs-lookup"><span data-stu-id="e02aa-147">Click **Query**.</span></span> <span data-ttu-id="e02aa-148">Modifica hello di hello query tooinclude **selezionare** istruzione per **ExternalTemperature**.</span><span class="sxs-lookup"><span data-stu-id="e02aa-148">Edit hello query tooinclude hello **SELECT** statement for **ExternalTemperature**.</span></span> <span data-ttu-id="e02aa-149">Hello seguenti vengono illustrate query completa di hello con hello nuovo **selezionare** istruzione:</span><span class="sxs-lookup"><span data-stu-id="e02aa-149">hello following sample shows hello complete query with hello new **SELECT** statement:</span></span>

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

5. <span data-ttu-id="e02aa-150">Fare clic su **salvare** toochange hello aggiornato query della regola.</span><span class="sxs-lookup"><span data-stu-id="e02aa-150">Click **Save** toochange hello updated rule query.</span></span>

6. <span data-ttu-id="e02aa-151">Fare clic su **avviare** processo di flusso Analitica hello toostart eseguire di nuovo.</span><span class="sxs-lookup"><span data-stu-id="e02aa-151">Click **Start** toostart hello Stream Analytics job running again.</span></span>

## <a name="add-your-new-rule-in-hello-dashboard"></a><span data-ttu-id="e02aa-152">Aggiungere la nuova regola nel dashboard di hello</span><span class="sxs-lookup"><span data-stu-id="e02aa-152">Add your new rule in hello dashboard</span></span>

<span data-ttu-id="e02aa-153">È ora possibile aggiungere hello **ExternalTemperature** dispositivo tooa regola nel dashboard di soluzione hello.</span><span class="sxs-lookup"><span data-stu-id="e02aa-153">You can now add hello **ExternalTemperature** rule tooa device in hello solution dashboard.</span></span>

1. <span data-ttu-id="e02aa-154">Passare il portale di soluzione toohello.</span><span class="sxs-lookup"><span data-stu-id="e02aa-154">Navigate toohello solution portal.</span></span>

2. <span data-ttu-id="e02aa-155">Passare toohello **dispositivi** pannello.</span><span class="sxs-lookup"><span data-stu-id="e02aa-155">Navigate toohello **Devices** panel.</span></span>

3. <span data-ttu-id="e02aa-156">Individuare hello dispositivo personalizzata creata che invia **ExternalTemperature** telemetria e hello **dettagli dispositivo** pannello, fare clic su **Aggiungi regola**.</span><span class="sxs-lookup"><span data-stu-id="e02aa-156">Locate hello custom device you created that sends **ExternalTemperature** telemetry and on hello **Device Details** panel, click **Add Rule**.</span></span>

4. <span data-ttu-id="e02aa-157">Selezionare **ExternalTemperature** in **Campo dati**.</span><span class="sxs-lookup"><span data-stu-id="e02aa-157">Select **ExternalTemperature** in **Data Field**.</span></span>

5. <span data-ttu-id="e02aa-158">Impostare **soglia** too56.</span><span class="sxs-lookup"><span data-stu-id="e02aa-158">Set **Threshold** too56.</span></span> <span data-ttu-id="e02aa-159">Quindi fare clic su **Salva e visualizza regole**.</span><span class="sxs-lookup"><span data-stu-id="e02aa-159">Then click **Save and view rules**.</span></span>

6. <span data-ttu-id="e02aa-160">Restituisce la cronologia allarme toohello dashboard tooview hello.</span><span class="sxs-lookup"><span data-stu-id="e02aa-160">Return toohello dashboard tooview hello alarm history.</span></span>

7. <span data-ttu-id="e02aa-161">Nella finestra di console hello è lasciato aperto, avviare l'invio di hello Node.js console app toobegin **ExternalTemperature** i dati di telemetria.</span><span class="sxs-lookup"><span data-stu-id="e02aa-161">In hello console window you left open, start hello Node.js console app toobegin sending **ExternalTemperature** telemetry data.</span></span>

8. <span data-ttu-id="e02aa-162">Si noti che hello **cronologia allarme** tabella illustra i nuovi avvisi quando hello nuova regola viene attivata.</span><span class="sxs-lookup"><span data-stu-id="e02aa-162">Notice that hello **Alarm History** table shows new alarms when hello new rule is triggered.</span></span>
 
## <a name="additional-information"></a><span data-ttu-id="e02aa-163">Informazioni aggiuntive</span><span class="sxs-lookup"><span data-stu-id="e02aa-163">Additional information</span></span>

<span data-ttu-id="e02aa-164">Modifica operatore hello  **>**  è più complessa e va oltre hello descritte in questa esercitazione.</span><span class="sxs-lookup"><span data-stu-id="e02aa-164">Changing hello operator **>** is more complex and goes beyond hello steps outlined in this tutorial.</span></span> <span data-ttu-id="e02aa-165">Mentre è possibile modificare hello Analitica flusso processo toouse qualsiasi operatore a cui si desidera, indicare che l'operatore nel portale di soluzione hello è un'attività più complessa.</span><span class="sxs-lookup"><span data-stu-id="e02aa-165">While you can change hello Stream Analytics job toouse whatever operator you like, reflecting that operator in hello solution portal is a more complex task.</span></span> 

## <a name="next-steps"></a><span data-ttu-id="e02aa-166">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="e02aa-166">Next steps</span></span>
<span data-ttu-id="e02aa-167">Ora che si è visto come toocreate regole personalizzate, sono disponibili ulteriori informazioni sulle soluzioni preconfigurata hello:</span><span class="sxs-lookup"><span data-stu-id="e02aa-167">Now that you've seen how toocreate custom rules, you can learn more about hello preconfigured solutions:</span></span>

- <span data-ttu-id="e02aa-168">[Connessione logica App tooyour Azure IoT Suite remoto preconfigurato soluzione di monitoraggio][lnk-logic-app]</span><span class="sxs-lookup"><span data-stu-id="e02aa-168">[Connect Logic App tooyour Azure IoT Suite Remote Monitoring preconfigured solution][lnk-logic-app]</span></span>
- <span data-ttu-id="e02aa-169">[Metadati del dispositivo informazioni di monitoraggio remoto hello preconfigurato soluzione][lnk-devinfo].</span><span class="sxs-lookup"><span data-stu-id="e02aa-169">[Device information metadata in hello remote monitoring preconfigured solution][lnk-devinfo].</span></span>

[lnk-devinfo]: iot-suite-remote-monitoring-device-info.md

[lnk_free_trial]: http://azure.microsoft.com/pricing/free-trial/
[lnk-node]: http://nodejs.org
[lnk-builtin-rule]: iot-suite-getstarted-preconfigured-solutions.md#view-alarms
[lnk-dynamic-telemetry]: iot-suite-dynamic-telemetry.md
[lnk-logic-app]: iot-suite-logic-apps-tutorial.md
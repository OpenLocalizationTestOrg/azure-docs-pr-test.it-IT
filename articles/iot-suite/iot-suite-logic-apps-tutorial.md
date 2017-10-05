---
title: Azure IoT Suite e App per la logica | Microsoft Docs
description: Esercitazione su come associare App per la logica a Azure IoT Suite per un processo aziendale.
services: 
suite: iot-suite
documentationcenter: 
author: dominicbetts
manager: timlt
editor: 
ms.assetid: 4629a7af-56ca-4b21-a769-5fa18bc3ab07
ms.service: iot-suite
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 06/16/2017
ms.author: corywink
ms.openlocfilehash: 2e7997e2a8bdeeec6083d40acb55e653f87e140b
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-connect-logic-app-to-your-azure-iot-suite-remote-monitoring-preconfigured-solution"></a><span data-ttu-id="94a70-103">Esercitazione: Connettere l'app per la logica alla soluzione preconfigurata per il monitoraggio remoto Azure IoT Suite</span><span class="sxs-lookup"><span data-stu-id="94a70-103">Tutorial: Connect Logic App to your Azure IoT Suite Remote Monitoring preconfigured solution</span></span>
<span data-ttu-id="94a70-104">La soluzione preconfigurata per il monitoraggio remoto [Microsoft Azure IoT Suite][lnk-internetofthings] consente di iniziare a usare rapidamente un set di funzionalità end-to-end che esemplifica una soluzione IoT.</span><span class="sxs-lookup"><span data-stu-id="94a70-104">The [Microsoft Azure IoT Suite][lnk-internetofthings] remote monitoring preconfigured solution is a great way to get started quickly with an end-to-end feature set that exemplifies an IoT solution.</span></span> <span data-ttu-id="94a70-105">Questa esercitazione illustra come aggiungere l'app per la logica alla soluzione preconfigurata per il monitoraggio remoto Microsoft Azure IoT Suite.</span><span class="sxs-lookup"><span data-stu-id="94a70-105">This tutorial walks you through how to add Logic App to your Microsoft Azure IoT Suite remote monitoring preconfigured solution.</span></span> <span data-ttu-id="94a70-106">Questi passaggi descrivono come usare la soluzione IoT in modo avanzato collegandola a un processo aziendale.</span><span class="sxs-lookup"><span data-stu-id="94a70-106">These steps demonstrate how you can take your IoT solution even further by connecting it to a business process.</span></span>

<span data-ttu-id="94a70-107">*Per una descrizione dettagliata dell'esecuzione del provisioning di una soluzione preconfigurata per il monitoraggio remoto, vedere [Esercitazione: Introduzione alle soluzioni preconfigurate][lnk-getstarted].*</span><span class="sxs-lookup"><span data-stu-id="94a70-107">*If you’re looking for a walkthrough on how to provision a remote monitoring preconfigured solution, see [Tutorial: Get started with the IoT preconfigured solutions][lnk-getstarted].*</span></span>

<span data-ttu-id="94a70-108">Prima di iniziare questa esercitazione, è necessario:</span><span class="sxs-lookup"><span data-stu-id="94a70-108">Before you start this tutorial, you should:</span></span>

* <span data-ttu-id="94a70-109">Eseguire il provisioning della soluzione preconfigurata di monitoraggio remoto nella sottoscrizione di Azure.</span><span class="sxs-lookup"><span data-stu-id="94a70-109">Provision the remote monitoring preconfigured solution in your Azure subscription.</span></span>
* <span data-ttu-id="94a70-110">Creare un account SendGrid che consenta di inviare un messaggio di posta elettronica che attivi il processo aziendale.</span><span class="sxs-lookup"><span data-stu-id="94a70-110">Create a SendGrid account to enable you to send an email that triggers your business process.</span></span> <span data-ttu-id="94a70-111">È possibile richiedere un account di valutazione gratuito accedendo al sito Web [SendGrid](https://sendgrid.com/) e facendo clic su **Try for Free**(Prova gratuitamente).</span><span class="sxs-lookup"><span data-stu-id="94a70-111">You can sign up for a free trial account at [SendGrid](https://sendgrid.com/) by clicking **Try for Free**.</span></span> <span data-ttu-id="94a70-112">Dopo aver eseguito la registrazione per ottenere un account di valutazione gratuito, è necessario creare in SendGrid una [chiave API](https://sendgrid.com/docs/User_Guide/Settings/api_keys.html) che concede le autorizzazioni per l'invio di messaggi di posta elettronica.</span><span class="sxs-lookup"><span data-stu-id="94a70-112">After you have registered for your free trial account, you need to create an [API key](https://sendgrid.com/docs/User_Guide/Settings/api_keys.html) in SendGrid that grants permissions to send mail.</span></span> <span data-ttu-id="94a70-113">La chiave API sarà necessaria più avanti nell'esercitazione.</span><span class="sxs-lookup"><span data-stu-id="94a70-113">You need this API key later in the tutorial.</span></span>

<span data-ttu-id="94a70-114">Per completare questa esercitazione, è necessario Visual Studio 2015 o Visual Studio 2017 per modificare le azioni del back-end della soluzione preconfigurata.</span><span class="sxs-lookup"><span data-stu-id="94a70-114">To complete this tutorial, you need Visual Studio 2015 or Visual Studio 2017 to modify the actions in the preconfigured solution back end.</span></span>

<span data-ttu-id="94a70-115">Supponendo di avere già eseguito il provisioning della soluzione preconfigurata per il monitoraggio remoto, passare al gruppo di risorse per la soluzione nel [portale di Azure][lnk-azureportal].</span><span class="sxs-lookup"><span data-stu-id="94a70-115">Assuming you’ve already provisioned your remote monitoring preconfigured solution, navigate to the resource group for that solution in the [Azure portal][lnk-azureportal].</span></span> <span data-ttu-id="94a70-116">Il nome del gruppo di risorse coincide con quello assegnato alla soluzione per il monitoraggio remoto al momento del provisioning.</span><span class="sxs-lookup"><span data-stu-id="94a70-116">The resource group has the same name as the solution name you chose when you provisioned your remote monitoring solution.</span></span> <span data-ttu-id="94a70-117">Nel gruppo di risorse è possibile visualizzare tutte le risorse di Azure con provisioning per la soluzione, ad eccezione dell'applicazione Azure Active Directory disponibile nel portale di Azure classico.</span><span class="sxs-lookup"><span data-stu-id="94a70-117">In the resource group, you can see all the provisioned Azure resources for your solution except for the Azure Active Directory application that you can find in the Azure Classic Portal.</span></span> <span data-ttu-id="94a70-118">La schermata seguente mostra un pannello **Gruppo di risorse** di esempio per una soluzione preconfigurata per il monitoraggio remoto:</span><span class="sxs-lookup"><span data-stu-id="94a70-118">The following screenshot shows an example **Resource group** blade for a remote monitoring preconfigured solution:</span></span>

![](media/iot-suite-logic-apps-tutorial/resourcegroup.png)

<span data-ttu-id="94a70-119">Per iniziare, impostare l'app per la logica da usare con la soluzione preconfigurata.</span><span class="sxs-lookup"><span data-stu-id="94a70-119">To begin, set up the logic app to use with the preconfigured solution.</span></span>

## <a name="set-up-the-logic-app"></a><span data-ttu-id="94a70-120">Impostare l'app per la logica</span><span class="sxs-lookup"><span data-stu-id="94a70-120">Set up the Logic App</span></span>
1. <span data-ttu-id="94a70-121">Nel Portale di Azure fare clic su **Aggiungi** nella parte superiore del pannello del gruppo di risorse.</span><span class="sxs-lookup"><span data-stu-id="94a70-121">Click **Add** at the top of your resource group blade in the Azure portal.</span></span>
2. <span data-ttu-id="94a70-122">Cercare **App per la logica**, farci clic e quindi scegliere **Crea**.</span><span class="sxs-lookup"><span data-stu-id="94a70-122">Search for **Logic App**, select it and then click **Create**.</span></span>
3. <span data-ttu-id="94a70-123">Compilare il campo **Nome** e immettere le stesse informazioni di **Sottoscrizione**e **Gruppo di risorse** usate al momento del provisioning della soluzione per il monitoraggio remoto.</span><span class="sxs-lookup"><span data-stu-id="94a70-123">Fill out the **Name** and use the same **Subscription** and **Resource group** that you used when you provisioned your remote monitoring solution.</span></span> <span data-ttu-id="94a70-124">Fare clic su **Crea**.</span><span class="sxs-lookup"><span data-stu-id="94a70-124">Click **Create**.</span></span>
   
    ![](media/iot-suite-logic-apps-tutorial/createlogicapp.png)
4. <span data-ttu-id="94a70-125">Dopo il completamento della distribuzione, l'app per la logica viene elencata come risorsa nel gruppo di risorse.</span><span class="sxs-lookup"><span data-stu-id="94a70-125">When your deployment completes, you can see the Logic App is listed as a resource in your resource group.</span></span>
5. <span data-ttu-id="94a70-126">Fare clic sull'app per la logica per passare al pannello App per la logica e scegliere il modello di **app per la logica vuoto** per aprire la finestra **Progettazione app per la logica**.</span><span class="sxs-lookup"><span data-stu-id="94a70-126">Click the Logic App to navigate to the Logic App blade, select the **Blank Logic App** template to open the **Logic Apps Designer**.</span></span>
   
    ![](media/iot-suite-logic-apps-tutorial/logicappsdesigner.png)
6. <span data-ttu-id="94a70-127">Selezionare **Richiesta**.</span><span class="sxs-lookup"><span data-stu-id="94a70-127">Select **Request**.</span></span> <span data-ttu-id="94a70-128">Questa azione specifica che una richiesta HTTP in ingresso con uno specifico payload in formato JSON agisce come trigger.</span><span class="sxs-lookup"><span data-stu-id="94a70-128">This action specifies that an incoming HTTP request with a specific JSON formatted payload acts as a trigger.</span></span>
7. <span data-ttu-id="94a70-129">Incollare il codice seguente nello schema JSON del corpo della richiesta:</span><span class="sxs-lookup"><span data-stu-id="94a70-129">Paste the following code into the Request Body JSON Schema:</span></span>
   
    ```json
    {
      "$schema": "http://json-schema.org/draft-04/schema#",
      "id": "/",
      "properties": {
        "DeviceId": {
          "id": "DeviceId",
          "type": "string"
        },
        "measuredValue": {
          "id": "measuredValue",
          "type": "integer"
        },
        "measurementName": {
          "id": "measurementName",
          "type": "string"
        }
      },
      "required": [
        "DeviceId",
        "measurementName",
        "measuredValue"
      ],
      "type": "object"
    }
    ```
   
   > [!NOTE]
   > <span data-ttu-id="94a70-130">È possibile copiare l'URL per il post HTTP dopo aver salvato l'app per la logica. È tuttavia necessario aggiungere prima un'azione.</span><span class="sxs-lookup"><span data-stu-id="94a70-130">You can copy the URL for the HTTP post after you save the logic app, but first you must add an action.</span></span>
   > 
   > 
8. <span data-ttu-id="94a70-131">Fare clic su **+ Nuovo passaggio** nel trigger manuale.</span><span class="sxs-lookup"><span data-stu-id="94a70-131">Click **+ New step** under your manual trigger.</span></span> <span data-ttu-id="94a70-132">Fare quindi clic su **Aggiungi un'azione**.</span><span class="sxs-lookup"><span data-stu-id="94a70-132">Then click **Add an action**.</span></span>
   
    ![](media/iot-suite-logic-apps-tutorial/logicappcode.png)
9. <span data-ttu-id="94a70-133">Cercare **SendGrid - Send email** (SendGrid - Invia messaggio di posta elettronica) e fare clic.</span><span class="sxs-lookup"><span data-stu-id="94a70-133">Search for **SendGrid - Send email** and click it.</span></span>
   
    ![](media/iot-suite-logic-apps-tutorial/logicappaction.png)
10. <span data-ttu-id="94a70-134">Digitare un nome da assegnare alla connessione, ad esempio **SendGridConnection**, immettere la **Chiave API SendGrid** creata al momento di impostare l'account SendGrid e fare clic su **Crea**.</span><span class="sxs-lookup"><span data-stu-id="94a70-134">Enter a name for the connection, such as **SendGridConnection**, enter the **SendGrid API Key** you created when you set up your SendGrid account, and click **Create**.</span></span>
    
    ![](media/iot-suite-logic-apps-tutorial/sendgridconnection.png)
11. <span data-ttu-id="94a70-135">Aggiungere gli indirizzi e-mail di cui si è proprietari in entrambi campi **Da** e **A**.</span><span class="sxs-lookup"><span data-stu-id="94a70-135">Add email addresses you own to both the **From** and **To** fields.</span></span> <span data-ttu-id="94a70-136">Aggiungere **Avviso di monitoraggio remoto [IDDispositivo]** nel campo **Oggetto**.</span><span class="sxs-lookup"><span data-stu-id="94a70-136">Add **Remote monitoring alert [DeviceId]** to the **Subject** field.</span></span> <span data-ttu-id="94a70-137">Nel campo del **corpo dell'e-mail** aggiungere **Il dispositivo [Dispositivo] ha segnalato [NomeMisurazione] con il valore [ValoreMisurato].**</span><span class="sxs-lookup"><span data-stu-id="94a70-137">In the **Email Body** field, add **Device [DeviceId] has reported [measurementName] with value [measuredValue].**</span></span> <span data-ttu-id="94a70-138">È possibile aggiungere **[IDDispositivo]**, **[NomeMisurazione]** e **[ValoreMisurato]** facendo clic sulla sezione **È possibile inserire dati dai passaggi precedenti**.</span><span class="sxs-lookup"><span data-stu-id="94a70-138">You can add **[DeviceId]**, **[measurementName]**, and **[measuredValue]** by clicking in the **You can insert data from previous steps** section.</span></span>
    
    ![](media/iot-suite-logic-apps-tutorial/sendgridaction.png)
12. <span data-ttu-id="94a70-139">Fare clic su **Salva** nel menu in alto.</span><span class="sxs-lookup"><span data-stu-id="94a70-139">Click **Save** in the top menu.</span></span>
13. <span data-ttu-id="94a70-140">Fare clic sul trigger **Richiesta** e copiare il valore **HTTP POST in questo URL**.</span><span class="sxs-lookup"><span data-stu-id="94a70-140">Click the **Request** trigger and copy the **Http Post to this URL** value.</span></span> <span data-ttu-id="94a70-141">Questo URL sarà necessario più avanti nell'esercitazione.</span><span class="sxs-lookup"><span data-stu-id="94a70-141">You need this URL later in this tutorial.</span></span>

> [!NOTE]
> <span data-ttu-id="94a70-142">Le app per la logica consentono di eseguire [molti tipi di azioni][lnk-logic-apps-actions], incluse azioni in Office 365.</span><span class="sxs-lookup"><span data-stu-id="94a70-142">Logic Apps enable you to run [many different types of action][lnk-logic-apps-actions] including actions in Office 365.</span></span> 
> 
> 

## <a name="set-up-the-eventprocessor-web-job"></a><span data-ttu-id="94a70-143">Configurare il processo Web EventProcessor</span><span class="sxs-lookup"><span data-stu-id="94a70-143">Set up the EventProcessor Web Job</span></span>
<span data-ttu-id="94a70-144">In questa sezione si esegue la connessione della soluzione preconfigurata all'App per la logica creata.</span><span class="sxs-lookup"><span data-stu-id="94a70-144">In this section, you connect your preconfigured solution to the Logic App you created.</span></span> <span data-ttu-id="94a70-145">Per completare questa attività, aggiungere l'URL per attivare l'App per la logica all'azione che viene generata quando il valore del sensore del dispositivo supera la soglia.</span><span class="sxs-lookup"><span data-stu-id="94a70-145">To complete this task, you add the URL to trigger the Logic App to the action that fires when a device sensor value exceeds a threshold.</span></span>

1. <span data-ttu-id="94a70-146">Usare il client git per clonare la versione più recente del [repository GitHub azure-iot-remote-monitoring][lnk-rmgithub].</span><span class="sxs-lookup"><span data-stu-id="94a70-146">Use your git client to clone the latest version of the [azure-iot-remote-monitoring github repository][lnk-rmgithub].</span></span> <span data-ttu-id="94a70-147">Ad esempio:</span><span class="sxs-lookup"><span data-stu-id="94a70-147">For example:</span></span>
   
    ```cmd
    git clone https://github.com/Azure/azure-iot-remote-monitoring.git
    ```
2. <span data-ttu-id="94a70-148">In Visual Studio aprire il file **RemoteMonitoring.sln** dalla copia locale del repository.</span><span class="sxs-lookup"><span data-stu-id="94a70-148">In Visual Studio, open the **RemoteMonitoring.sln** from the local copy of the repository.</span></span>
3. <span data-ttu-id="94a70-149">Aprire il file **ActionRepository.cs** nella cartella **Infrastruttura\\Repository** cartella.</span><span class="sxs-lookup"><span data-stu-id="94a70-149">Open the **ActionRepository.cs** file in the **Infrastructure\\Repository** folder.</span></span>
4. <span data-ttu-id="94a70-150">Aggiornare il dizionario degli **ID azione** con l'informazione **HTTP POST in questo URL** annotato dall'app per la logica come indicato di seguito:</span><span class="sxs-lookup"><span data-stu-id="94a70-150">Update the **actionIds** dictionary with the **Http Post to this URL** you noted from your Logic App as follows:</span></span>
   
    ```csharp
    private Dictionary<string,string> actionIds = new Dictionary<string, string>()
    {
        { "Send Message", "<Http Post to this URL>" },
        { "Raise Alarm", "<Http Post to this URL>" }
    };
    ```
5. <span data-ttu-id="94a70-151">Salvare le modifiche nella soluzione e uscire da Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="94a70-151">Save the changes in solution and exit Visual Studio.</span></span>

## <a name="deploy-from-the-command-line"></a><span data-ttu-id="94a70-152">Eseguire la distribuzione dalla riga di comando</span><span class="sxs-lookup"><span data-stu-id="94a70-152">Deploy from the command line</span></span>
<span data-ttu-id="94a70-153">In questa sezione verrà distribuita la versione aggiornata della soluzione per il monitoraggio remoto per sostituire quella attualmente in esecuzione in Azure.</span><span class="sxs-lookup"><span data-stu-id="94a70-153">In this section, you deploy your updated version of the remote monitoring solution to replace the version currently running in Azure.</span></span>

1. <span data-ttu-id="94a70-154">Per istruzioni sulla configurazione dell'ambiente per la distribuzione, fare clic [qui][lnk-devsetup].</span><span class="sxs-lookup"><span data-stu-id="94a70-154">Following the [dev set-up][lnk-devsetup] instructions to set up your environment for deployment.</span></span>
2. <span data-ttu-id="94a70-155">Per istruzioni sulla distribuzione in locale, fare clic [qui][lnk-localdeploy].</span><span class="sxs-lookup"><span data-stu-id="94a70-155">To deploy locally, follow the [local deployment][lnk-localdeploy] instructions.</span></span>
3. <span data-ttu-id="94a70-156">Per istruzioni su come eseguire la distribuzione nel cloud e aggiornare la distribuzione nel cloud esistente, fare clic [qui][lnk-clouddeploy].</span><span class="sxs-lookup"><span data-stu-id="94a70-156">To deploy to the cloud and update your existing cloud deployment, follow the [cloud deployment][lnk-clouddeploy] instructions.</span></span> <span data-ttu-id="94a70-157">Come nome della distribuzione usare quello della distribuzione originale.</span><span class="sxs-lookup"><span data-stu-id="94a70-157">Use the name of your original deployment as the deployment name.</span></span> <span data-ttu-id="94a70-158">Se, ad esempio, la distribuzione originale era denominata **demologicapp**, usare il comando seguente:</span><span class="sxs-lookup"><span data-stu-id="94a70-158">For example if the original deployment was called **demologicapp**, use the following command:</span></span>
   
   ```cmd
   build.cmd cloud release demologicapp
   ```
   
   <span data-ttu-id="94a70-159">Quando si esegue lo script di compilazione, assicurarsi di usare gli stessi account, sottoscrizione e area di Azure nonché la stessa istanza di Active Directory usati per il provisioning della soluzione.</span><span class="sxs-lookup"><span data-stu-id="94a70-159">When the build script runs, be sure to use the same Azure account, subscription, region, and Active Directory instance you used when you provisioned the solution.</span></span>

## <a name="see-your-logic-app-in-action"></a><span data-ttu-id="94a70-160">App per la logica in azione</span><span class="sxs-lookup"><span data-stu-id="94a70-160">See your Logic App in action</span></span>
<span data-ttu-id="94a70-161">La soluzione preconfigurata per il monitoraggio remoto dispone di due regole specificate per impostazione predefinita al provisioning di una soluzione.</span><span class="sxs-lookup"><span data-stu-id="94a70-161">The remote monitoring preconfigured solution has two rules set up by default when you provision a solution.</span></span> <span data-ttu-id="94a70-162">Entrambe le regole riguardano il dispositivo **SampleDevice001** :</span><span class="sxs-lookup"><span data-stu-id="94a70-162">Both rules are on the **SampleDevice001** device:</span></span>

* <span data-ttu-id="94a70-163">Temperature > 38.00</span><span class="sxs-lookup"><span data-stu-id="94a70-163">Temperature > 38.00</span></span>
* <span data-ttu-id="94a70-164">Humidity > 48.00</span><span class="sxs-lookup"><span data-stu-id="94a70-164">Humidity > 48.00</span></span>

<span data-ttu-id="94a70-165">La regola della temperatura attiva l'azione **Raise Alarm**, mentre la regola dell'umidità attiva l'azione **SendMessage**.</span><span class="sxs-lookup"><span data-stu-id="94a70-165">The temperature rule triggers the **Raise Alarm** action and the Humidity rule triggers the **SendMessage** action.</span></span> <span data-ttu-id="94a70-166">Supponendo che sia stato usato lo stesso URL per entrambe le azioni della classe **ActionRepository** , l'app per la logica si attiva per entrambe le regole.</span><span class="sxs-lookup"><span data-stu-id="94a70-166">Assuming you used the same URL for both actions the **ActionRepository** class, your logic app triggers for either rule.</span></span> <span data-ttu-id="94a70-167">Entrambe le regole usano SendGrid per inviare un messaggio di posta elettronica all'indirizzo **A** con i dettagli dell'avviso.</span><span class="sxs-lookup"><span data-stu-id="94a70-167">Both rules use SendGrid to send an email to the **To** address with details of the alert.</span></span>

> [!NOTE]
> <span data-ttu-id="94a70-168">L'app per la logica continua ad attivare le regole ogni volta che i valori soglia vengono superati.</span><span class="sxs-lookup"><span data-stu-id="94a70-168">The Logic App continues to trigger every time the threshold is met.</span></span> <span data-ttu-id="94a70-169">Per evitare l'invio di messaggi di posta elettronica non necessari, è possibile disabilitare le regole nel portale della soluzione o disabilitare l'app per la logica nel [portale di Azure][lnk-azureportal].</span><span class="sxs-lookup"><span data-stu-id="94a70-169">To avoid unnecessary emails, you can either disable the rules in your solution portal or disable the Logic App in the [Azure portal][lnk-azureportal].</span></span>
> 
> 

<span data-ttu-id="94a70-170">Oltre a ricevere messaggi di posta elettronica, è anche possibile vedere quando l'app per la logica è in esecuzione nel portale:</span><span class="sxs-lookup"><span data-stu-id="94a70-170">In addition to receiving emails, you can also see when the Logic App runs in the portal:</span></span>

![](media/iot-suite-logic-apps-tutorial/logicapprun.png)

## <a name="next-steps"></a><span data-ttu-id="94a70-171">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="94a70-171">Next steps</span></span>
<span data-ttu-id="94a70-172">Dopo aver usato un'app per la logica per connettere la soluzione preconfigurata a un processo aziendale, è possibile leggere le informazioni sulle opzioni per la personalizzazione delle soluzioni preconfigurate:</span><span class="sxs-lookup"><span data-stu-id="94a70-172">Now that you've used a Logic App to connect the preconfigured solution to a business process, you can learn more about the options for customizing the preconfigured solutions:</span></span>

* <span data-ttu-id="94a70-173">[Usare la telemetria dinamica con la soluzione preconfigurata per il monitoraggio remoto][lnk-dynamic]</span><span class="sxs-lookup"><span data-stu-id="94a70-173">[Use dynamic telemetry with the remote monitoring preconfigured solution][lnk-dynamic]</span></span>
* <span data-ttu-id="94a70-174">[Metadati di informazioni sul dispositivo nella soluzione preconfigurata per il monitoraggio remoto][lnk-devinfo]</span><span class="sxs-lookup"><span data-stu-id="94a70-174">[Device information metadata in the remote monitoring preconfigured solution][lnk-devinfo]</span></span>

[lnk-dynamic]: iot-suite-dynamic-telemetry.md
[lnk-devinfo]: iot-suite-remote-monitoring-device-info.md

[lnk-internetofthings]: https://azure.microsoft.com/documentation/suites/iot-suite/
[lnk-getstarted]: iot-suite-getstarted-preconfigured-solutions.md
[lnk-azureportal]: https://portal.azure.com
[lnk-logic-apps-actions]: ../connectors/apis-list.md
[lnk-rmgithub]: https://github.com/Azure/azure-iot-remote-monitoring
[lnk-devsetup]: https://github.com/Azure/azure-iot-remote-monitoring/blob/master/Docs/dev-setup.md
[lnk-localdeploy]: https://github.com/Azure/azure-iot-remote-monitoring/blob/master/Docs/local-deployment.md
[lnk-clouddeploy]: https://github.com/Azure/azure-iot-remote-monitoring/blob/master/Docs/cloud-deployment.md

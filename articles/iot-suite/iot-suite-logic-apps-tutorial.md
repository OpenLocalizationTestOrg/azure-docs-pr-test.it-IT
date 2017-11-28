---
title: aaaAzure IoT Suite e logica App | Documenti Microsoft
description: Un'esercitazione sulla toohook di App per la logica tooAzure IoT Suite per il processo di business.
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
ms.openlocfilehash: 6ef7311ac38f4e2ddb032cff0fb73591da5f76c2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-connect-logic-app-tooyour-azure-iot-suite-remote-monitoring-preconfigured-solution"></a><span data-ttu-id="e30b4-103">Esercitazione: Connessione logica App tooyour Azure IoT Suite remoto preconfigurato soluzione di monitoraggio</span><span class="sxs-lookup"><span data-stu-id="e30b4-103">Tutorial: Connect Logic App tooyour Azure IoT Suite Remote Monitoring preconfigured solution</span></span>
<span data-ttu-id="e30b4-104">Hello [Microsoft Azure IoT Suite] [ lnk-internetofthings] soluzione preconfigurata di monitoraggio remoto è tooget un modo utile per iniziare rapidamente con un set di funzionalità end-to-end per semplificare la soluzione IoT.</span><span class="sxs-lookup"><span data-stu-id="e30b4-104">hello [Microsoft Azure IoT Suite][lnk-internetofthings] remote monitoring preconfigured solution is a great way tooget started quickly with an end-to-end feature set that exemplifies an IoT solution.</span></span> <span data-ttu-id="e30b4-105">In questa esercitazione viene illustrato come tooadd logica App tooyour Microsoft Azure IoT Suite monitoraggio remoto preconfigurato soluzione.</span><span class="sxs-lookup"><span data-stu-id="e30b4-105">This tutorial walks you through how tooadd Logic App tooyour Microsoft Azure IoT Suite remote monitoring preconfigured solution.</span></span> <span data-ttu-id="e30b4-106">In questa procedura viene illustrano soluzione IoT ulteriormente connettendola tooa processo di business.</span><span class="sxs-lookup"><span data-stu-id="e30b4-106">These steps demonstrate how you can take your IoT solution even further by connecting it tooa business process.</span></span>

<span data-ttu-id="e30b4-107">*Se si sta cercando una procedura dettagliata su come un'operazione di monitoraggio remoto tooprovision preconfigurato soluzione, vedere [esercitazione: Introduzione a soluzioni IoT preconfigurato hello][lnk-getstarted].*</span><span class="sxs-lookup"><span data-stu-id="e30b4-107">*If you’re looking for a walkthrough on how tooprovision a remote monitoring preconfigured solution, see [Tutorial: Get started with hello IoT preconfigured solutions][lnk-getstarted].*</span></span>

<span data-ttu-id="e30b4-108">Prima di iniziare questa esercitazione, è necessario:</span><span class="sxs-lookup"><span data-stu-id="e30b4-108">Before you start this tutorial, you should:</span></span>

* <span data-ttu-id="e30b4-109">Monitoraggio remoto di eseguire il provisioning hello preconfigurato soluzione nella sottoscrizione di Azure.</span><span class="sxs-lookup"><span data-stu-id="e30b4-109">Provision hello remote monitoring preconfigured solution in your Azure subscription.</span></span>
* <span data-ttu-id="e30b4-110">Creare un tooenable di account di SendGrid è toosend un messaggio di posta elettronica che attiva il processo di business.</span><span class="sxs-lookup"><span data-stu-id="e30b4-110">Create a SendGrid account tooenable you toosend an email that triggers your business process.</span></span> <span data-ttu-id="e30b4-111">È possibile richiedere un account di valutazione gratuito accedendo al sito Web [SendGrid](https://sendgrid.com/) e facendo clic su **Try for Free**(Prova gratuitamente).</span><span class="sxs-lookup"><span data-stu-id="e30b4-111">You can sign up for a free trial account at [SendGrid](https://sendgrid.com/) by clicking **Try for Free**.</span></span> <span data-ttu-id="e30b4-112">Dopo avere registrato per l'account di valutazione gratuita, è necessario toocreate un [chiave API](https://sendgrid.com/docs/User_Guide/Settings/api_keys.html) in SendGrid che concede le autorizzazioni di posta elettronica toosend.</span><span class="sxs-lookup"><span data-stu-id="e30b4-112">After you have registered for your free trial account, you need toocreate an [API key](https://sendgrid.com/docs/User_Guide/Settings/api_keys.html) in SendGrid that grants permissions toosend mail.</span></span> <span data-ttu-id="e30b4-113">Questa chiave API è necessario più avanti nell'esercitazione di hello.</span><span class="sxs-lookup"><span data-stu-id="e30b4-113">You need this API key later in hello tutorial.</span></span>

<span data-ttu-id="e30b4-114">toocomplete questa esercitazione, è necessario Visual Studio 2015 o Visual Studio 2017 azioni hello toomodify nel back-end di hello soluzione preconfigurata.</span><span class="sxs-lookup"><span data-stu-id="e30b4-114">toocomplete this tutorial, you need Visual Studio 2015 or Visual Studio 2017 toomodify hello actions in hello preconfigured solution back end.</span></span>

<span data-ttu-id="e30b4-115">Supponendo che è già stato effettuato il provisioning del monitoraggio remoto preconfigurato soluzione, passare il gruppo di risorse toohello per tale soluzione di hello [portale di Azure][lnk-azureportal].</span><span class="sxs-lookup"><span data-stu-id="e30b4-115">Assuming you’ve already provisioned your remote monitoring preconfigured solution, navigate toohello resource group for that solution in hello [Azure portal][lnk-azureportal].</span></span> <span data-ttu-id="e30b4-116">gruppo di risorse Hello è hello stesso nome come hello soluzione nome scelto quando è stato eseguito il provisioning la soluzione di monitoraggio remota.</span><span class="sxs-lookup"><span data-stu-id="e30b4-116">hello resource group has hello same name as hello solution name you chose when you provisioned your remote monitoring solution.</span></span> <span data-ttu-id="e30b4-117">Nel gruppo di risorse hello, è possibile visualizzare tutti hello il provisioning delle risorse di Azure per la soluzione, ad eccezione dell'applicazione Azure Active Directory che è possibile trovare nel portale di Azure classico hello hello.</span><span class="sxs-lookup"><span data-stu-id="e30b4-117">In hello resource group, you can see all hello provisioned Azure resources for your solution except for hello Azure Active Directory application that you can find in hello Azure Classic Portal.</span></span> <span data-ttu-id="e30b4-118">Hello schermata riportata di seguito viene illustrato un esempio **gruppo di risorse** pannello per un'operazione di monitoraggio remoto preconfigurato soluzione:</span><span class="sxs-lookup"><span data-stu-id="e30b4-118">hello following screenshot shows an example **Resource group** blade for a remote monitoring preconfigured solution:</span></span>

![](media/iot-suite-logic-apps-tutorial/resourcegroup.png)

<span data-ttu-id="e30b4-119">toobegin, impostare hello logica app toouse con hello preconfigurato soluzione.</span><span class="sxs-lookup"><span data-stu-id="e30b4-119">toobegin, set up hello logic app toouse with hello preconfigured solution.</span></span>

## <a name="set-up-hello-logic-app"></a><span data-ttu-id="e30b4-120">Impostare hello logica App</span><span class="sxs-lookup"><span data-stu-id="e30b4-120">Set up hello Logic App</span></span>
1. <span data-ttu-id="e30b4-121">Fare clic su **Aggiungi** nella parte superiore di hello del Pannello di gruppo risorsa nel portale di Azure hello.</span><span class="sxs-lookup"><span data-stu-id="e30b4-121">Click **Add** at hello top of your resource group blade in hello Azure portal.</span></span>
2. <span data-ttu-id="e30b4-122">Cercare **App per la logica**, farci clic e quindi scegliere **Crea**.</span><span class="sxs-lookup"><span data-stu-id="e30b4-122">Search for **Logic App**, select it and then click **Create**.</span></span>
3. <span data-ttu-id="e30b4-123">Compilare hello **nome** e utilizzare hello stesso **sottoscrizione** e **gruppo di risorse** utilizzato quando è stato effettuato il provisioning la soluzione di monitoraggio remota.</span><span class="sxs-lookup"><span data-stu-id="e30b4-123">Fill out hello **Name** and use hello same **Subscription** and **Resource group** that you used when you provisioned your remote monitoring solution.</span></span> <span data-ttu-id="e30b4-124">Fare clic su **Crea**.</span><span class="sxs-lookup"><span data-stu-id="e30b4-124">Click **Create**.</span></span>
   
    ![](media/iot-suite-logic-apps-tutorial/createlogicapp.png)
4. <span data-ttu-id="e30b4-125">Al termine della distribuzione, è possibile visualizzare hello che App per la logica è elencato come risorsa nel gruppo di risorse.</span><span class="sxs-lookup"><span data-stu-id="e30b4-125">When your deployment completes, you can see hello Logic App is listed as a resource in your resource group.</span></span>
5. <span data-ttu-id="e30b4-126">Fare clic su hello logica App toonavigate toohello pannello App logica, seleziona hello **App vuota per la logica** hello tooopen modello **logica App progettazione**.</span><span class="sxs-lookup"><span data-stu-id="e30b4-126">Click hello Logic App toonavigate toohello Logic App blade, select hello **Blank Logic App** template tooopen hello **Logic Apps Designer**.</span></span>
   
    ![](media/iot-suite-logic-apps-tutorial/logicappsdesigner.png)
6. <span data-ttu-id="e30b4-127">Selezionare **Richiesta**.</span><span class="sxs-lookup"><span data-stu-id="e30b4-127">Select **Request**.</span></span> <span data-ttu-id="e30b4-128">Questa azione specifica che una richiesta HTTP in ingresso con uno specifico payload in formato JSON agisce come trigger.</span><span class="sxs-lookup"><span data-stu-id="e30b4-128">This action specifies that an incoming HTTP request with a specific JSON formatted payload acts as a trigger.</span></span>
7. <span data-ttu-id="e30b4-129">Incollare hello seguente di codice in hello dello Schema JSON del corpo della richiesta:</span><span class="sxs-lookup"><span data-stu-id="e30b4-129">Paste hello following code into hello Request Body JSON Schema:</span></span>
   
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
   > <span data-ttu-id="e30b4-130">È possibile copiare URL hello per post HTTP hello dopo il salvataggio hello logica app, ma è innanzitutto necessario aggiungere un'azione.</span><span class="sxs-lookup"><span data-stu-id="e30b4-130">You can copy hello URL for hello HTTP post after you save hello logic app, but first you must add an action.</span></span>
   > 
   > 
8. <span data-ttu-id="e30b4-131">Fare clic su **+ Nuovo passaggio** nel trigger manuale.</span><span class="sxs-lookup"><span data-stu-id="e30b4-131">Click **+ New step** under your manual trigger.</span></span> <span data-ttu-id="e30b4-132">Fare quindi clic su **Aggiungi un'azione**.</span><span class="sxs-lookup"><span data-stu-id="e30b4-132">Then click **Add an action**.</span></span>
   
    ![](media/iot-suite-logic-apps-tutorial/logicappcode.png)
9. <span data-ttu-id="e30b4-133">Cercare **SendGrid - Send email** (SendGrid - Invia messaggio di posta elettronica) e fare clic.</span><span class="sxs-lookup"><span data-stu-id="e30b4-133">Search for **SendGrid - Send email** and click it.</span></span>
   
    ![](media/iot-suite-logic-apps-tutorial/logicappaction.png)
10. <span data-ttu-id="e30b4-134">Immettere un nome per la connessione hello, ad esempio **SendGridConnection**, immettere hello **chiave API SendGrid** creato quando si imposta l'account di SendGrid e fare clic su **crea**.</span><span class="sxs-lookup"><span data-stu-id="e30b4-134">Enter a name for hello connection, such as **SendGridConnection**, enter hello **SendGrid API Key** you created when you set up your SendGrid account, and click **Create**.</span></span>
    
    ![](media/iot-suite-logic-apps-tutorial/sendgridconnection.png)
11. <span data-ttu-id="e30b4-135">Aggiungere indirizzi di posta elettronica è proprio tooboth hello **da** e **a** campi.</span><span class="sxs-lookup"><span data-stu-id="e30b4-135">Add email addresses you own tooboth hello **From** and **To** fields.</span></span> <span data-ttu-id="e30b4-136">Aggiungere **avviso di monitoraggio remoto [DeviceId]** toohello **soggetto** campo.</span><span class="sxs-lookup"><span data-stu-id="e30b4-136">Add **Remote monitoring alert [DeviceId]** toohello **Subject** field.</span></span> <span data-ttu-id="e30b4-137">In hello **corpo del messaggio di posta elettronica** campo, aggiungere **dispositivo [DeviceId] ha segnalato [measurementName] con valore [measuredValue].**</span><span class="sxs-lookup"><span data-stu-id="e30b4-137">In hello **Email Body** field, add **Device [DeviceId] has reported [measurementName] with value [measuredValue].**</span></span> <span data-ttu-id="e30b4-138">È possibile aggiungere **[DeviceId]**, **[measurementName]**, e **[measuredValue]** facendo hello **è possibile inserire i dati nei passaggi precedenti**sezione.</span><span class="sxs-lookup"><span data-stu-id="e30b4-138">You can add **[DeviceId]**, **[measurementName]**, and **[measuredValue]** by clicking in hello **You can insert data from previous steps** section.</span></span>
    
    ![](media/iot-suite-logic-apps-tutorial/sendgridaction.png)
12. <span data-ttu-id="e30b4-139">Fare clic su **salvare** nel menu superiore hello.</span><span class="sxs-lookup"><span data-stu-id="e30b4-139">Click **Save** in hello top menu.</span></span>
13. <span data-ttu-id="e30b4-140">Fare clic su hello **richiesta** hello trigger e copia **Http Post toothis URL** valore.</span><span class="sxs-lookup"><span data-stu-id="e30b4-140">Click hello **Request** trigger and copy hello **Http Post toothis URL** value.</span></span> <span data-ttu-id="e30b4-141">Questo URL sarà necessario più avanti nell'esercitazione.</span><span class="sxs-lookup"><span data-stu-id="e30b4-141">You need this URL later in this tutorial.</span></span>

> [!NOTE]
> <span data-ttu-id="e30b4-142">Logica App consentono di toorun [molti tipi diversi di azione] [ lnk-logic-apps-actions] incluse azioni in Office 365.</span><span class="sxs-lookup"><span data-stu-id="e30b4-142">Logic Apps enable you toorun [many different types of action][lnk-logic-apps-actions] including actions in Office 365.</span></span> 
> 
> 

## <a name="set-up-hello-eventprocessor-web-job"></a><span data-ttu-id="e30b4-143">Impostare hello processo Web EventProcessor</span><span class="sxs-lookup"><span data-stu-id="e30b4-143">Set up hello EventProcessor Web Job</span></span>
<span data-ttu-id="e30b4-144">In questa sezione è connettersi il toohello soluzione preconfigurata logica App è stato creato.</span><span class="sxs-lookup"><span data-stu-id="e30b4-144">In this section, you connect your preconfigured solution toohello Logic App you created.</span></span> <span data-ttu-id="e30b4-145">toocomplete questa attività, si aggiunge hello tootrigger hello logica App toohello azione URL che viene generato quando un valore del sensore dispositivo supera una soglia.</span><span class="sxs-lookup"><span data-stu-id="e30b4-145">toocomplete this task, you add hello URL tootrigger hello Logic App toohello action that fires when a device sensor value exceeds a threshold.</span></span>

1. <span data-ttu-id="e30b4-146">Utilizzare la git client tooclone hello più recente versione di hello [azure iot-remoto monitoraggio repository github][lnk-rmgithub].</span><span class="sxs-lookup"><span data-stu-id="e30b4-146">Use your git client tooclone hello latest version of hello [azure-iot-remote-monitoring github repository][lnk-rmgithub].</span></span> <span data-ttu-id="e30b4-147">ad esempio:</span><span class="sxs-lookup"><span data-stu-id="e30b4-147">For example:</span></span>
   
    ```cmd
    git clone https://github.com/Azure/azure-iot-remote-monitoring.git
    ```
2. <span data-ttu-id="e30b4-148">In Visual Studio, aprire hello **RemoteMonitoring.sln** copia locale di hello del repository hello.</span><span class="sxs-lookup"><span data-stu-id="e30b4-148">In Visual Studio, open hello **RemoteMonitoring.sln** from hello local copy of hello repository.</span></span>
3. <span data-ttu-id="e30b4-149">Aprire hello **ActionRepository.cs** file hello **infrastruttura\\Repository** cartella.</span><span class="sxs-lookup"><span data-stu-id="e30b4-149">Open hello **ActionRepository.cs** file in hello **Infrastructure\\Repository** folder.</span></span>
4. <span data-ttu-id="e30b4-150">Hello aggiornamento **actionIds** dizionario con hello **Http Post toothis URL** indicato dall'App logica come indicato di seguito:</span><span class="sxs-lookup"><span data-stu-id="e30b4-150">Update hello **actionIds** dictionary with hello **Http Post toothis URL** you noted from your Logic App as follows:</span></span>
   
    ```csharp
    private Dictionary<string,string> actionIds = new Dictionary<string, string>()
    {
        { "Send Message", "<Http Post toothis URL>" },
        { "Raise Alarm", "<Http Post toothis URL>" }
    };
    ```
5. <span data-ttu-id="e30b4-151">Salvare le modifiche di hello nella soluzione e uscire da Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="e30b4-151">Save hello changes in solution and exit Visual Studio.</span></span>

## <a name="deploy-from-hello-command-line"></a><span data-ttu-id="e30b4-152">Distribuzione dalla riga di comando hello</span><span class="sxs-lookup"><span data-stu-id="e30b4-152">Deploy from hello command line</span></span>
<span data-ttu-id="e30b4-153">In questa sezione, si distribuisce la versione aggiornata di hello remoto monitoraggio tooreplace hello versione della soluzione attualmente in esecuzione in Azure.</span><span class="sxs-lookup"><span data-stu-id="e30b4-153">In this section, you deploy your updated version of hello remote monitoring solution tooreplace hello version currently running in Azure.</span></span>

1. <span data-ttu-id="e30b4-154">In seguito hello [configurazione dev] [ lnk-devsetup] tooset istruzioni dell'ambiente per la distribuzione.</span><span class="sxs-lookup"><span data-stu-id="e30b4-154">Following hello [dev set-up][lnk-devsetup] instructions tooset up your environment for deployment.</span></span>
2. <span data-ttu-id="e30b4-155">toodeploy in locale, seguire hello [distribuzione locale] [ lnk-localdeploy] istruzioni.</span><span class="sxs-lookup"><span data-stu-id="e30b4-155">toodeploy locally, follow hello [local deployment][lnk-localdeploy] instructions.</span></span>
3. <span data-ttu-id="e30b4-156">toodeploy toohello cloud e aggiornare la distribuzione cloud esistente, seguire hello [distribuzione cloud] [ lnk-clouddeploy] istruzioni.</span><span class="sxs-lookup"><span data-stu-id="e30b4-156">toodeploy toohello cloud and update your existing cloud deployment, follow hello [cloud deployment][lnk-clouddeploy] instructions.</span></span> <span data-ttu-id="e30b4-157">Utilizzare il nome di hello della distribuzione originale come nome della distribuzione hello.</span><span class="sxs-lookup"><span data-stu-id="e30b4-157">Use hello name of your original deployment as hello deployment name.</span></span> <span data-ttu-id="e30b4-158">Ad esempio se è stata chiamata distribuzione originale hello **demologicapp**, utilizzare hello comando seguente:</span><span class="sxs-lookup"><span data-stu-id="e30b4-158">For example if hello original deployment was called **demologicapp**, use hello following command:</span></span>
   
   ```cmd
   build.cmd cloud release demologicapp
   ```
   
   <span data-ttu-id="e30b4-159">Quando viene eseguito lo script di compilazione hello, prestare attenzione toouse hello stesso account Azure, sottoscrizione, area e istanza di Active Directory è utilizzata quando è stato effettuato il provisioning soluzione hello.</span><span class="sxs-lookup"><span data-stu-id="e30b4-159">When hello build script runs, be sure toouse hello same Azure account, subscription, region, and Active Directory instance you used when you provisioned hello solution.</span></span>

## <a name="see-your-logic-app-in-action"></a><span data-ttu-id="e30b4-160">App per la logica in azione</span><span class="sxs-lookup"><span data-stu-id="e30b4-160">See your Logic App in action</span></span>
<span data-ttu-id="e30b4-161">Hello soluzione preconfigurata di monitoraggio remoto dispone di due regole impostate per impostazione predefinita quando si esegue il provisioning di una soluzione.</span><span class="sxs-lookup"><span data-stu-id="e30b4-161">hello remote monitoring preconfigured solution has two rules set up by default when you provision a solution.</span></span> <span data-ttu-id="e30b4-162">Entrambe le regole presenti hello **SampleDevice001** dispositivo:</span><span class="sxs-lookup"><span data-stu-id="e30b4-162">Both rules are on hello **SampleDevice001** device:</span></span>

* <span data-ttu-id="e30b4-163">Temperature > 38.00</span><span class="sxs-lookup"><span data-stu-id="e30b4-163">Temperature > 38.00</span></span>
* <span data-ttu-id="e30b4-164">Humidity > 48.00</span><span class="sxs-lookup"><span data-stu-id="e30b4-164">Humidity > 48.00</span></span>

<span data-ttu-id="e30b4-165">regola di temperatura Hello attiva hello **generare allarme** azione e hello regola umidità attiva hello **SendMessage** azione.</span><span class="sxs-lookup"><span data-stu-id="e30b4-165">hello temperature rule triggers hello **Raise Alarm** action and hello Humidity rule triggers hello **SendMessage** action.</span></span> <span data-ttu-id="e30b4-166">Presupponendo che utilizzate hello stesso URL per entrambi hello azioni **ActionRepository** classe, i trigger di app logica per una regola.</span><span class="sxs-lookup"><span data-stu-id="e30b4-166">Assuming you used hello same URL for both actions hello **ActionRepository** class, your logic app triggers for either rule.</span></span> <span data-ttu-id="e30b4-167">Entrambe le regole di utilizzano SendGrid toosend toohello un messaggio di posta elettronica **a** indirizzo con i dettagli dell'avviso hello.</span><span class="sxs-lookup"><span data-stu-id="e30b4-167">Both rules use SendGrid toosend an email toohello **To** address with details of hello alert.</span></span>

> [!NOTE]
> <span data-ttu-id="e30b4-168">Hello logica App continua tootrigger ogni volta che viene raggiunta la soglia di hello.</span><span class="sxs-lookup"><span data-stu-id="e30b4-168">hello Logic App continues tootrigger every time hello threshold is met.</span></span> <span data-ttu-id="e30b4-169">tooavoid email non necessarie, è possibile disattivare le regole di hello nella soluzione portale o disabilitare Ciao logica App hello [portale di Azure][lnk-azureportal].</span><span class="sxs-lookup"><span data-stu-id="e30b4-169">tooavoid unnecessary emails, you can either disable hello rules in your solution portal or disable hello Logic App in hello [Azure portal][lnk-azureportal].</span></span>
> 
> 

<span data-ttu-id="e30b4-170">Inoltre tooreceiving messaggi di posta elettronica, è possibile anche visualizzare quando viene eseguito hello logica App nel portale di hello:</span><span class="sxs-lookup"><span data-stu-id="e30b4-170">In addition tooreceiving emails, you can also see when hello Logic App runs in hello portal:</span></span>

![](media/iot-suite-logic-apps-tutorial/logicapprun.png)

## <a name="next-steps"></a><span data-ttu-id="e30b4-171">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="e30b4-171">Next steps</span></span>
<span data-ttu-id="e30b4-172">Ora che è stato utilizzato un processo di business tooa logica App tooconnect hello preconfigurato soluzione, è possibile ulteriori informazioni sulle opzioni di hello per personalizzare soluzioni preconfigurata hello:</span><span class="sxs-lookup"><span data-stu-id="e30b4-172">Now that you've used a Logic App tooconnect hello preconfigured solution tooa business process, you can learn more about hello options for customizing hello preconfigured solutions:</span></span>

* <span data-ttu-id="e30b4-173">[Utilizzare i dati di telemetria dinamico con hello soluzione preconfigurata di monitoraggio remoto][lnk-dynamic]</span><span class="sxs-lookup"><span data-stu-id="e30b4-173">[Use dynamic telemetry with hello remote monitoring preconfigured solution][lnk-dynamic]</span></span>
* <span data-ttu-id="e30b4-174">[Metadati informazioni del dispositivo nella soluzione preconfigurata di monitoraggio remoto hello][lnk-devinfo]</span><span class="sxs-lookup"><span data-stu-id="e30b4-174">[Device information metadata in hello remote monitoring preconfigured solution][lnk-devinfo]</span></span>

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

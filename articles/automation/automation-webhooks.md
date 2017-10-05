---
title: Avvio di un runbook di Automazione di Azure con un webhook | Documentazione Microsoft
description: Un webhook che consente a un client di avviare un Runbook in Automazione di Azure da una chiamata HTTP.  Questo articolo descrive come creare un webhook e come chiamarne uno per avviare un Runbook.
services: automation
documentationcenter: 
author: mgoedtel
manager: jwhit
editor: tysonn
ms.assetid: 9b20237c-a593-4299-bbdc-35c47ee9e55d
ms.service: automation
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/22/2017
ms.author: magoedte;bwren;sngun
ms.openlocfilehash: 6c65427fcd18e41a90dfb872aa9525f758b17b87
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="starting-an-azure-automation-runbook-with-a-webhook"></a><span data-ttu-id="0a770-104">Avviare un runbook di Automazione di Azure con un webhook</span><span class="sxs-lookup"><span data-stu-id="0a770-104">Starting an Azure Automation runbook with a webhook</span></span>
<span data-ttu-id="0a770-105">Un *webhook* consente di avviare un Runbook specifico in Automazione di Azure tramite una singola richiesta HTTP.</span><span class="sxs-lookup"><span data-stu-id="0a770-105">A *webhook* allows you to start a particular runbook in Azure Automation through a single HTTP request.</span></span> <span data-ttu-id="0a770-106">In questo modo, i servizi esterni come Visual Studio Team Services, GitHub o Microsoft Operations Management Suite Log Analytics o le applicazioni personalizzate possono avviare i runbook senza implementare una soluzione completa usando l'API di Automazione di Azure.</span><span class="sxs-lookup"><span data-stu-id="0a770-106">This allows external services such as Visual Studio Team Services, GitHub, Microsoft Operations Management Suite Log Analytics, or custom applications to start runbooks without implementing a full solution using the Azure Automation API.</span></span>  
<span data-ttu-id="0a770-107">![Panoramica dei webhook](media/automation-webhooks/webhook-overview-image.png)</span><span class="sxs-lookup"><span data-stu-id="0a770-107">![WebhooksOverview](media/automation-webhooks/webhook-overview-image.png)</span></span>

<span data-ttu-id="0a770-108">È possibile confrontare i webhook con altre modalità di avvio di un Runbook nell'articolo relativo all' [avvio di un Runbook in Automazione di Azure](automation-starting-a-runbook.md)</span><span class="sxs-lookup"><span data-stu-id="0a770-108">You can compare webhooks to other methods of starting a runbook in [Starting a runbook in Azure Automation](automation-starting-a-runbook.md)</span></span>

## <a name="details-of-a-webhook"></a><span data-ttu-id="0a770-109">Informazioni dettagliate sui webhook</span><span class="sxs-lookup"><span data-stu-id="0a770-109">Details of a webhook</span></span>
<span data-ttu-id="0a770-110">La tabella seguente descrive le proprietà che devono essere configurate per un webhook.</span><span class="sxs-lookup"><span data-stu-id="0a770-110">The following table describes the properties that you must configure for a webhook.</span></span>

| <span data-ttu-id="0a770-111">Proprietà</span><span class="sxs-lookup"><span data-stu-id="0a770-111">Property</span></span> | <span data-ttu-id="0a770-112">Descrizione</span><span class="sxs-lookup"><span data-stu-id="0a770-112">Description</span></span> |
|:--- |:--- |
| <span data-ttu-id="0a770-113">Nome</span><span class="sxs-lookup"><span data-stu-id="0a770-113">Name</span></span> |<span data-ttu-id="0a770-114">È possibile specificare un nome qualsiasi per un webhook dal momento che non viene esposto al client.</span><span class="sxs-lookup"><span data-stu-id="0a770-114">You can provide any name you want for a webhook since this is not exposed to the client.</span></span>  <span data-ttu-id="0a770-115">Viene usato solo per consentire all'utente di identificare il Runbook in Automazione di Azure.</span><span class="sxs-lookup"><span data-stu-id="0a770-115">It is only used for you to identify the runbook in Azure Automation.</span></span> <br>  <span data-ttu-id="0a770-116">Come procedura consigliata, è opportuno assegnare al webhook un nome correlato al client in cui verrà usato.</span><span class="sxs-lookup"><span data-stu-id="0a770-116">As a best practice, you should give the webhook a name related to the client that will use it.</span></span> |
| <span data-ttu-id="0a770-117">URL</span><span class="sxs-lookup"><span data-stu-id="0a770-117">URL</span></span> |<span data-ttu-id="0a770-118">L'URL del webhook è l'indirizzo univoco che viene chiamato da un client con HTTP POST per avviare il Runbook collegato al webhook.</span><span class="sxs-lookup"><span data-stu-id="0a770-118">The URL of the webhook is the unique address that a client calls with an HTTP POST to start the runbook linked to the webhook.</span></span>  <span data-ttu-id="0a770-119">Viene generato automaticamente al momento della creazione del webhook.</span><span class="sxs-lookup"><span data-stu-id="0a770-119">It is automatically generated when you create the webhook.</span></span>  <span data-ttu-id="0a770-120">Non è possibile specificare un URL personalizzato.</span><span class="sxs-lookup"><span data-stu-id="0a770-120">You cannot specify a custom URL.</span></span> <br> <br>  <span data-ttu-id="0a770-121">L'URL contiene un token di sicurezza che consente al Runbook di essere richiamato da un sistema di terze parti senza un'autenticazione aggiuntiva.</span><span class="sxs-lookup"><span data-stu-id="0a770-121">The URL contains a security token that allows the runbook to be invoked by a third party system with no further authentication.</span></span> <span data-ttu-id="0a770-122">Per questo motivo, deve essere considerato come una password.</span><span class="sxs-lookup"><span data-stu-id="0a770-122">For this reason, it should be treated like a password.</span></span>  <span data-ttu-id="0a770-123">Per motivi di sicurezza, è possibile visualizzare l'URL solo nel portale di Azure al momento della creazione del webhook.</span><span class="sxs-lookup"><span data-stu-id="0a770-123">For security reasons, you can only view the URL in the Azure portal at the time the webhook is created.</span></span> <span data-ttu-id="0a770-124">È consigliabile prendere nota dell'URL e conservarlo in un luogo sicuro per usi futuri.</span><span class="sxs-lookup"><span data-stu-id="0a770-124">You should note the URL in a secure location for future use.</span></span> |
| <span data-ttu-id="0a770-125">Expiration date</span><span class="sxs-lookup"><span data-stu-id="0a770-125">Expiration date</span></span> |<span data-ttu-id="0a770-126">Analogamente a un certificato, un webhook ha una data di scadenza oltre la quale non può più essere usato.</span><span class="sxs-lookup"><span data-stu-id="0a770-126">Like a certificate, each webhook has an expiration date at which time it can no longer be used.</span></span>  <span data-ttu-id="0a770-127">La data di scadenza può essere modificata dopo la creazione del webhook.</span><span class="sxs-lookup"><span data-stu-id="0a770-127">This expiration date can be modified after the webhook is created.</span></span> |
| <span data-ttu-id="0a770-128">Enabled</span><span class="sxs-lookup"><span data-stu-id="0a770-128">Enabled</span></span> |<span data-ttu-id="0a770-129">Un webhook viene abilitato per impostazione predefinita nel momento in cui viene creato.</span><span class="sxs-lookup"><span data-stu-id="0a770-129">A webhook is enabled by default when it is created.</span></span>  <span data-ttu-id="0a770-130">Se viene impostato su Disabled, nessun client sarà in grado di usarlo.</span><span class="sxs-lookup"><span data-stu-id="0a770-130">If you set it to Disabled, then no client will be able to use it.</span></span>  <span data-ttu-id="0a770-131">È possibile impostare la proprietà **Enabled** quando si crea il webhook o in qualsiasi momento successivo.</span><span class="sxs-lookup"><span data-stu-id="0a770-131">You can set the **Enabled** property when you create the webhook or anytime once it is created.</span></span> |

### <a name="parameters"></a><span data-ttu-id="0a770-132">Parametri</span><span class="sxs-lookup"><span data-stu-id="0a770-132">Parameters</span></span>
<span data-ttu-id="0a770-133">Un webhook può definire valori per parametri di Runbook usati quando il Runbook viene avviato dal webhook.</span><span class="sxs-lookup"><span data-stu-id="0a770-133">A webhook can define values for runbook parameters that are used when the runbook is started by that webhook.</span></span> <span data-ttu-id="0a770-134">Il webhook deve includere valori per tutti i parametri obbligatori del Runbook e può includere valori per i parametri facoltativi.</span><span class="sxs-lookup"><span data-stu-id="0a770-134">The webhook must include values for any mandatory parameters of the runbook and may include values for optional parameters.</span></span> <span data-ttu-id="0a770-135">Un valore di parametro configurato per un webhook può essere modificato anche dopo aver creato il webhoook.</span><span class="sxs-lookup"><span data-stu-id="0a770-135">A parameter value configured to a webhook can be modified even after creating the webhoook.</span></span> <span data-ttu-id="0a770-136">Se esistono più webhook collegati a un singolo Runbook, ognuno di essi potrà usare valori di parametri diversi.</span><span class="sxs-lookup"><span data-stu-id="0a770-136">Multiple webhooks linked to a single runbook can each use different parameter values.</span></span>

<span data-ttu-id="0a770-137">Quando avvia un Runbook con un webhook, un client non può eseguire l'override dei valori di parametri definiti nel webhook.</span><span class="sxs-lookup"><span data-stu-id="0a770-137">When a client starts a runbook using a webhook, it cannot override the parameter values defined in the webhook.</span></span>  <span data-ttu-id="0a770-138">Per ricevere dati dal client, il Runbook può accettare un singolo parametro denominato **$WebhookData** di tipo [object] che conterrà i dati inclusi dal client nella richiesta POST.</span><span class="sxs-lookup"><span data-stu-id="0a770-138">To receive data from the client, the runbook can accept a single parameter called **$WebhookData** of type [object] that will contain data that the client includes in the POST request.</span></span>

![Proprietà Webhookdata](media/automation-webhooks/webhook-data-properties.png)

<span data-ttu-id="0a770-140">L'oggetto **$WebhookData** disporrà delle proprietà seguenti:</span><span class="sxs-lookup"><span data-stu-id="0a770-140">The **$WebhookData** object will have the following properties:</span></span>

| <span data-ttu-id="0a770-141">Proprietà</span><span class="sxs-lookup"><span data-stu-id="0a770-141">Property</span></span> | <span data-ttu-id="0a770-142">Descrizione</span><span class="sxs-lookup"><span data-stu-id="0a770-142">Description</span></span> |
|:--- |:--- |
| <span data-ttu-id="0a770-143">WebhookName</span><span class="sxs-lookup"><span data-stu-id="0a770-143">WebhookName</span></span> |<span data-ttu-id="0a770-144">Nome del webhook.</span><span class="sxs-lookup"><span data-stu-id="0a770-144">The name of the webhook.</span></span> |
| <span data-ttu-id="0a770-145">RequestHeader</span><span class="sxs-lookup"><span data-stu-id="0a770-145">RequestHeader</span></span> |<span data-ttu-id="0a770-146">Tabella hash contenente le intestazioni della richiesta POST in ingresso.</span><span class="sxs-lookup"><span data-stu-id="0a770-146">Hash table containing the headers of the incoming POST request.</span></span> |
| <span data-ttu-id="0a770-147">RequestBody</span><span class="sxs-lookup"><span data-stu-id="0a770-147">RequestBody</span></span> |<span data-ttu-id="0a770-148">Corpo della richiesta POST in ingresso.</span><span class="sxs-lookup"><span data-stu-id="0a770-148">The body of the incoming POST request.</span></span>  <span data-ttu-id="0a770-149">Manterrà tutta la formattazione, ad esempio stringa, JSON, XML o dati codificati in un form.</span><span class="sxs-lookup"><span data-stu-id="0a770-149">This will retain any formatting such as string, JSON, XML, or form encoded data.</span></span> <span data-ttu-id="0a770-150">Il Runbook deve essere scritto in modo che funzioni con il formato di dati previsto.</span><span class="sxs-lookup"><span data-stu-id="0a770-150">The runbook must be written to work with the data format that is expected.</span></span> |

<span data-ttu-id="0a770-151">Non è richiesta alcuna configurazione del webhook per supportare il parametro **$WebhookData** e il Runbook non deve necessariamente accettarlo.</span><span class="sxs-lookup"><span data-stu-id="0a770-151">There is no configuration of the webhook required to support the **$WebhookData** parameter, and the runbook is not required to accept it.</span></span>  <span data-ttu-id="0a770-152">Se il Runbook non definisce il parametro, gli eventuali dettagli della richiesta inviata dal client verranno ignorati.</span><span class="sxs-lookup"><span data-stu-id="0a770-152">If the runbook does not define the parameter, then any details of the request sent from the client is ignored.</span></span>

<span data-ttu-id="0a770-153">Se si specifica un valore per $WebhookData quando si crea il webhook, viene eseguito l'override di tale valore quando il webhook avvia il Runbook con i dati della richiesta POST del client, anche se il client non include dati nel corpo della richiesta.</span><span class="sxs-lookup"><span data-stu-id="0a770-153">If you specify a value for $WebhookData when you create the webhook, that value will be overriden when the webhook starts the runbook with the data from the client POST request, even if the client does not include any data in the request body.</span></span>  <span data-ttu-id="0a770-154">Se si avvia un Runbook con l'oggetto $WebhookData che usa un metodo diverso da un webhook, è possibile specificare un valore per $Webhookdata che verrà riconosciuto dal Runbook.</span><span class="sxs-lookup"><span data-stu-id="0a770-154">If you start a runbook that has $WebhookData using a method other than a webhook, you can provide a value for $Webhookdata that will be recognized by the runbook.</span></span>  <span data-ttu-id="0a770-155">Questo valore deve essere un oggetto con le stesse [proprietà](#details-of-a-webhook) di $Webhookdata in modo che il Runbook possa usarlo correttamente come se stesse usando con il WebhookData effettivo passato da un webhook.</span><span class="sxs-lookup"><span data-stu-id="0a770-155">This value should be an object with the same [properties](#details-of-a-webhook) as $Webhookdata so that the runbook can properly work with it as if it was working with actual WebhookData passed by a webhook.</span></span>

<span data-ttu-id="0a770-156">Ad esempio, se si inizia il seguente runbook dal portale di Azure e si desidera passare alcuni esempi WebhookData per testarli, poiché WebhookData è un oggetto, deve essere passato come JSON nell'interfaccia utente.</span><span class="sxs-lookup"><span data-stu-id="0a770-156">For example, if you are starting the following runbook from the Azure Portal and want to pass some sample WebhookData for testing, since WebhookData is an object, it should be passed as JSON in the UI.</span></span>

![Parametro WebhookData dall'interfaccia utente](media/automation-webhooks/WebhookData-parameter-from-UI.png)

<span data-ttu-id="0a770-158">Per il runbook riportato sopra, se si hanno le seguenti proprietà per il parametro WebhookData:</span><span class="sxs-lookup"><span data-stu-id="0a770-158">For the above runbook, if you have the following properties for the WebhookData parameter:</span></span>

1. <span data-ttu-id="0a770-159">WebhookName: *MyWebhook*</span><span class="sxs-lookup"><span data-stu-id="0a770-159">WebhookName: *MyWebhook*</span></span>
2. <span data-ttu-id="0a770-160">RequestHeader: *From=Test User*</span><span class="sxs-lookup"><span data-stu-id="0a770-160">RequestHeader: *From=Test User*</span></span>
3. <span data-ttu-id="0a770-161">RequestBody: *[“VM1”, “VM2”]*</span><span class="sxs-lookup"><span data-stu-id="0a770-161">RequestBody: *[“VM1”, “VM2”]*</span></span>

<span data-ttu-id="0a770-162">Passare quindi il seguente valore JSON nell'interfaccia utente per il parametro WebhookData:</span><span class="sxs-lookup"><span data-stu-id="0a770-162">Then you would pass the following JSON value in the UI for the WebhookData parameter:</span></span>  

* <span data-ttu-id="0a770-163">{"WebhookName":"MyWebhook", "RequestHeader":{"From":"Test User"}, "RequestBody":"[\"VM1\",\"VM2\"]"}</span><span class="sxs-lookup"><span data-stu-id="0a770-163">{"WebhookName":"MyWebhook", "RequestHeader":{"From":"Test User"}, "RequestBody":"[\"VM1\",\"VM2\"]"}</span></span>

![Parametro WebhookData Start dall'interfaccia utente](media/automation-webhooks/Start-WebhookData-parameter-from-UI.png)

> [!NOTE]
> <span data-ttu-id="0a770-165">I valori di tutti i parametri di input vengono registrati con il processo di Runbook.</span><span class="sxs-lookup"><span data-stu-id="0a770-165">The values of all input parameters are logged with the runbook job.</span></span>  <span data-ttu-id="0a770-166">Qualsiasi input fornito dal client nella richiesta del webhook verrà quindi registrato e sarà disponibile per chiunque abbia accesso al processo di automazione.</span><span class="sxs-lookup"><span data-stu-id="0a770-166">This means that any input provided by the client in the webhook request will be logged and available to anyone with access to the automation job.</span></span>  <span data-ttu-id="0a770-167">Per questo motivo è consigliabile procedere con cautela quando si includono dati sensibili nelle chiamate di webhook.</span><span class="sxs-lookup"><span data-stu-id="0a770-167">For this reason, you should be cautious about including sensitive information in webhook calls.</span></span>
>

## <a name="security"></a><span data-ttu-id="0a770-168">Sicurezza</span><span class="sxs-lookup"><span data-stu-id="0a770-168">Security</span></span>
<span data-ttu-id="0a770-169">La sicurezza di un webhook si basa sulla privacy dell'URL che contiene un token di sicurezza che consente di richiamarlo.</span><span class="sxs-lookup"><span data-stu-id="0a770-169">The security of a webhook relies on the privacy of its URL which contains a security token that allows it to be invoked.</span></span> <span data-ttu-id="0a770-170">Automazione di Azure non esegue alcuna autenticazione per la richiesta, purché venga inviata all'URL corretto.</span><span class="sxs-lookup"><span data-stu-id="0a770-170">Azure Automation does not perform any authentication on the request as long as it is made to the correct URL.</span></span> <span data-ttu-id="0a770-171">Per questo motivo, non è consigliabile usare i webhook per i Runbook che eseguono funzioni sensibili senza usare una modalità alternativa di convalida della richiesta.</span><span class="sxs-lookup"><span data-stu-id="0a770-171">For this reason, webhooks should not be used for runbooks that perform highly sensitive functions without using an alternate means of validating the request.</span></span>

<span data-ttu-id="0a770-172">È possibile includere nel Runbook la logica per determinare che è stato chiamato da un webhook selezionando la proprietà **WebhookName** del parametro $WebhookData.</span><span class="sxs-lookup"><span data-stu-id="0a770-172">You can include logic within the runbook to determine that it was called by a webhook by checking the **WebhookName** property of the $WebhookData parameter.</span></span> <span data-ttu-id="0a770-173">Il runbook può eseguire altre convalide cercando informazioni specifiche nella proprietà **RequestHeader** o **RequestBody**.</span><span class="sxs-lookup"><span data-stu-id="0a770-173">The runbook could perform further validation by looking for particular information in the **RequestHeader** or **RequestBody** properties.</span></span>

<span data-ttu-id="0a770-174">Un'altra strategia consiste nel fare in modo che il Runbook esegua la convalida di una condizione esterna quando riceve una richiesta da un webhook.</span><span class="sxs-lookup"><span data-stu-id="0a770-174">Another strategy is to have the runbook perform some validation of an external condition when it received a webhook request.</span></span>  <span data-ttu-id="0a770-175">Si consideri ad esempio un Runbook chiamato da GitHub ogni volta che si verifica un nuovo commit in un repository di GitHub.</span><span class="sxs-lookup"><span data-stu-id="0a770-175">For example, consider a runbook that is called by GitHub whenever there is a new commit to a GitHub repository.</span></span>  <span data-ttu-id="0a770-176">Il Runbook può connettersi a GitHub per convalidare che si sia effettivamente verificato un nuovo commit prima di continuare.</span><span class="sxs-lookup"><span data-stu-id="0a770-176">The runbook might connect to GitHub to validate that a new commit had actually just occurred before continuing.</span></span>

## <a name="creating-a-webhook"></a><span data-ttu-id="0a770-177">Creazione di un webhook</span><span class="sxs-lookup"><span data-stu-id="0a770-177">Creating a webhook</span></span>
<span data-ttu-id="0a770-178">Seguire questa procedura per creare un nuovo webhook collegato a un Runbook nel portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="0a770-178">Use the following procedure to create a new webhook linked to a runbook in the Azure portal.</span></span>

1. <span data-ttu-id="0a770-179">Nel pannello **Runbook** nel portale di Azure fare clic sul Runbook che verrà avviato dal webhook per visualizzare il pannello dei dettagli.</span><span class="sxs-lookup"><span data-stu-id="0a770-179">From the **Runbooks blade** in the Azure portal, click the runbook that the webhook will start to view its detail blade.</span></span>
2. <span data-ttu-id="0a770-180">Fare clic su **Webhook** nella parte superiore del pannello per aprire il pannello **Aggiungi webhook**.</span><span class="sxs-lookup"><span data-stu-id="0a770-180">Click **Webhook** at the top of the blade to open the **Add Webhook** blade.</span></span> <br><span data-ttu-id="0a770-181">
   ![Pulsante Webhook](media/automation-webhooks/webhooks-button.png)</span><span class="sxs-lookup"><span data-stu-id="0a770-181">
![Webhooks button](media/automation-webhooks/webhooks-button.png)</span></span>
3. <span data-ttu-id="0a770-182">Fare clic su **Creare un nuovo webhook** per aprire il pannello **Create webhook (Crea webhook)**.</span><span class="sxs-lookup"><span data-stu-id="0a770-182">Click **Create new webhook** to open the **Create webhook blade**.</span></span>
4. <span data-ttu-id="0a770-183">Specificare un valore per **Nome** e **Data scadenza** per il webhook e indicare se deve essere abilitato.</span><span class="sxs-lookup"><span data-stu-id="0a770-183">Specify a **Name**, **Expiration Date** for the webhook and whether it should be enabled.</span></span> <span data-ttu-id="0a770-184">Per altre informazioni su queste proprietà, vedere [Informazioni dettagliate sui webhook](#details-of-a-webhook) .</span><span class="sxs-lookup"><span data-stu-id="0a770-184">See [Details of a webhook](#details-of-a-webhook) for more information these properties.</span></span>
5. <span data-ttu-id="0a770-185">Fare clic sull'icona di copia e premere CTRL+C per copiare l'URL del webhook.</span><span class="sxs-lookup"><span data-stu-id="0a770-185">Click the copy icon and press Ctrl+C to copy the URL of the webhook.</span></span>  <span data-ttu-id="0a770-186">Annotarlo in un luogo sicuro.</span><span class="sxs-lookup"><span data-stu-id="0a770-186">Then record it in a safe place.</span></span>  <span data-ttu-id="0a770-187">**Dopo aver creato il webhook, non è possibile recuperare di nuovo l'URL.**</span><span class="sxs-lookup"><span data-stu-id="0a770-187">**Once you create the webhook, you cannot retrieve the URL again.**</span></span> <br><span data-ttu-id="0a770-188">
   ![URL webhook](media/automation-webhooks/copy-webhook-url.png)</span><span class="sxs-lookup"><span data-stu-id="0a770-188">
![Webhook URL](media/automation-webhooks/copy-webhook-url.png)</span></span>
6. <span data-ttu-id="0a770-189">Fare clic su **Parameters** per specificare i valori per i parametri del Runbook.</span><span class="sxs-lookup"><span data-stu-id="0a770-189">Click **Parameters** to provide values for the runbook parameters.</span></span>  <span data-ttu-id="0a770-190">Se il Runbook ha parametri obbligatori, non sarà possibile creare il webhook a meno che non vengano messi a disposizione i valori.</span><span class="sxs-lookup"><span data-stu-id="0a770-190">If the runbook has mandatory parameters, then you will not be able to create the webhook unless values are provided.</span></span>
7. <span data-ttu-id="0a770-191">Fare clic su **Create** per creare il webhook.</span><span class="sxs-lookup"><span data-stu-id="0a770-191">Click **Create** to create the webhook.</span></span>

## <a name="using-a-webhook"></a><span data-ttu-id="0a770-192">Uso di un webhook</span><span class="sxs-lookup"><span data-stu-id="0a770-192">Using a webhook</span></span>
<span data-ttu-id="0a770-193">Per usare un webhook dopo averlo creato, l'applicazione client deve inviare una richiesta HTTP POST con l'URL del webhook.</span><span class="sxs-lookup"><span data-stu-id="0a770-193">To use a webhook after it has been created, your client application must issue an HTTP POST with the URL for the webhook.</span></span>  <span data-ttu-id="0a770-194">La sintassi del webhook sarà nel formato seguente.</span><span class="sxs-lookup"><span data-stu-id="0a770-194">The syntax of the webhook will be in the following format.</span></span>

    http://<Webhook Server>/token?=<Token Value>

<span data-ttu-id="0a770-195">Il client riceverà uno dei codici restituiti seguenti dalla richiesta POST.</span><span class="sxs-lookup"><span data-stu-id="0a770-195">The client will receive one of the following return codes from the POST request.</span></span>  

| <span data-ttu-id="0a770-196">Codice</span><span class="sxs-lookup"><span data-stu-id="0a770-196">Code</span></span> | <span data-ttu-id="0a770-197">Testo</span><span class="sxs-lookup"><span data-stu-id="0a770-197">Text</span></span> | <span data-ttu-id="0a770-198">Descrizione</span><span class="sxs-lookup"><span data-stu-id="0a770-198">Description</span></span> |
|:--- |:--- |:--- |
| <span data-ttu-id="0a770-199">202</span><span class="sxs-lookup"><span data-stu-id="0a770-199">202</span></span> |<span data-ttu-id="0a770-200">Accepted</span><span class="sxs-lookup"><span data-stu-id="0a770-200">Accepted</span></span> |<span data-ttu-id="0a770-201">La richiesta è stata accettata e il Runbook è stato accodato.</span><span class="sxs-lookup"><span data-stu-id="0a770-201">The request was accepted, and the runbook was successfully queued.</span></span> |
| <span data-ttu-id="0a770-202">400</span><span class="sxs-lookup"><span data-stu-id="0a770-202">400</span></span> |<span data-ttu-id="0a770-203">Bad Request</span><span class="sxs-lookup"><span data-stu-id="0a770-203">Bad Request</span></span> |<span data-ttu-id="0a770-204">La richiesta non è stata accettata per uno dei motivi seguenti.</span><span class="sxs-lookup"><span data-stu-id="0a770-204">The request was not accepted for one of the following reasons.</span></span> <ul> <li><span data-ttu-id="0a770-205">Il webhook è scaduto.</span><span class="sxs-lookup"><span data-stu-id="0a770-205">The webhook has expired.</span></span></li> <li><span data-ttu-id="0a770-206">Il webhook è disabilitato.</span><span class="sxs-lookup"><span data-stu-id="0a770-206">The webhook is disabled.</span></span></li> <li><span data-ttu-id="0a770-207">Il token nell'URL non è valido.</span><span class="sxs-lookup"><span data-stu-id="0a770-207">The token in the URL is invalid.</span></span></li>  </ul> |
| <span data-ttu-id="0a770-208">404</span><span class="sxs-lookup"><span data-stu-id="0a770-208">404</span></span> |<span data-ttu-id="0a770-209">Non trovato</span><span class="sxs-lookup"><span data-stu-id="0a770-209">Not Found</span></span> |<span data-ttu-id="0a770-210">La richiesta non è stata accettata per uno dei motivi seguenti.</span><span class="sxs-lookup"><span data-stu-id="0a770-210">The request was not accepted for one of the following reasons.</span></span> <ul> <li><span data-ttu-id="0a770-211">Il webhook non è stato trovato.</span><span class="sxs-lookup"><span data-stu-id="0a770-211">The webhook was not found.</span></span></li> <li><span data-ttu-id="0a770-212">Il runbook non è stato trovato.</span><span class="sxs-lookup"><span data-stu-id="0a770-212">The runbook was not found.</span></span></li> <li><span data-ttu-id="0a770-213">L'account non è stato trovato.</span><span class="sxs-lookup"><span data-stu-id="0a770-213">The account was not found.</span></span></li>  </ul> |
| <span data-ttu-id="0a770-214">500</span><span class="sxs-lookup"><span data-stu-id="0a770-214">500</span></span> |<span data-ttu-id="0a770-215">Internal Server Error</span><span class="sxs-lookup"><span data-stu-id="0a770-215">Internal Server Error</span></span> |<span data-ttu-id="0a770-216">L'URL è valido, ma si è verificato un errore.</span><span class="sxs-lookup"><span data-stu-id="0a770-216">The URL was valid, but an error occurred.</span></span>  <span data-ttu-id="0a770-217">Inviare di nuovo la richiesta.</span><span class="sxs-lookup"><span data-stu-id="0a770-217">Please resubmit the request.</span></span> |

<span data-ttu-id="0a770-218">Presupponendo che la richiesta riesca, la risposta del webhook conterrà l'ID processo in formato JSON come indicato di seguito.</span><span class="sxs-lookup"><span data-stu-id="0a770-218">Assuming the request is successful, the webhook response contains the job id in JSON format as follows.</span></span> <span data-ttu-id="0a770-219">Conterrà un singolo ID processo, ma il formato JSON consente potenziali miglioramenti futuri.</span><span class="sxs-lookup"><span data-stu-id="0a770-219">It will contain a single job id, but the JSON format allows for potential future enhancements.</span></span>

    {"JobIds":["<JobId>"]}  

<span data-ttu-id="0a770-220">Il client non è in grado di determinare quando viene completato il processo del Runbook o lo stato di avanzamento dal webhook.</span><span class="sxs-lookup"><span data-stu-id="0a770-220">The client cannot determine when the runbook job completes or its completion status from the webhook.</span></span>  <span data-ttu-id="0a770-221">Può determinare queste informazioni usando l'ID processo con un altro metodo, ad esempio [Windows PowerShell](http://msdn.microsoft.com/library/azure/dn690263.aspx) o l'[API di Automazione di Azure](https://msdn.microsoft.com/library/azure/mt163826.aspx).</span><span class="sxs-lookup"><span data-stu-id="0a770-221">It can determine this information using the job id with another method such as [Windows PowerShell](http://msdn.microsoft.com/library/azure/dn690263.aspx) or the [Azure Automation API](https://msdn.microsoft.com/library/azure/mt163826.aspx).</span></span>

### <a name="example"></a><span data-ttu-id="0a770-222">Esempio</span><span class="sxs-lookup"><span data-stu-id="0a770-222">Example</span></span>
<span data-ttu-id="0a770-223">L'esempio seguente usa Windows PowerShell per avviare un Runbook con un webhook.</span><span class="sxs-lookup"><span data-stu-id="0a770-223">The following example uses Windows PowerShell to start a runbook with a webhook.</span></span>  <span data-ttu-id="0a770-224">Si noti che qualsiasi linguaggio in grado di creare una richiesta HTTP può usare un webhook. Windows PowerShell viene usato qui solo come esempio.</span><span class="sxs-lookup"><span data-stu-id="0a770-224">Note that any language that can make an HTTP request can use a webhook; Windows PowerShell is just used here as an example.</span></span>

<span data-ttu-id="0a770-225">Il Runbook prevede un elenco di macchine virtuali in formato JSON nel corpo della richiesta.</span><span class="sxs-lookup"><span data-stu-id="0a770-225">The runbook is expecting a list of virtual machines formatted in JSON in the body of the request.</span></span> <span data-ttu-id="0a770-226">Nell'intestazione della richiesta vengono incluse anche informazioni sull'utente che avvia il Runbook e la data e l'ora di avvio.</span><span class="sxs-lookup"><span data-stu-id="0a770-226">We also are including information about who is starting the runbook and the date and time it is being started in the header of the request.</span></span>      

    $uri = "https://s1events.azure-automation.net/webhooks?token=8ud0dSrSo%2fvHWpYbklW%3c8s0GrOKJZ9Nr7zqcS%2bIQr4c%3d"
    $headers = @{"From"="user@contoso.com";"Date"="05/28/2015 15:47:00"}

    $vms  = @(
                @{ Name="vm01";ServiceName="vm01"},
                @{ Name="vm02";ServiceName="vm02"}
            )
    $body = ConvertTo-Json -InputObject $vms

    $response = Invoke-RestMethod -Method Post -Uri $uri -Headers $headers -Body $body
    $jobid = ConvertFrom-Json $response


<span data-ttu-id="0a770-227">L'immagine seguente illustra le informazioni di intestazione (usando una traccia di [Fiddler](http://www.telerik.com/fiddler) ) dalla richiesta.</span><span class="sxs-lookup"><span data-stu-id="0a770-227">The following image shows the header information (using a [Fiddler](http://www.telerik.com/fiddler) trace) from this request.</span></span> <span data-ttu-id="0a770-228">Sono incluse le intestazioni standard di una richiesta HTTP, oltre alla data personalizzata e le intestazioni DA aggiunte.</span><span class="sxs-lookup"><span data-stu-id="0a770-228">This includes standard headers of an HTTP request in addition to the custom Date and From headers that we added.</span></span>  <span data-ttu-id="0a770-229">Ognuno di questi valori è disponibile per il runbook nella proprietà **RequestHeaders** di **WebhookData**.</span><span class="sxs-lookup"><span data-stu-id="0a770-229">Each of these values is available to the runbook in the **RequestHeaders** property of **WebhookData**.</span></span>

![Pulsante Webhooks](media/automation-webhooks/webhook-request-headers.png)

<span data-ttu-id="0a770-231">L'immagine seguente mostra il corpo della richiesta (usando una traccia di [Fiddler](http://www.telerik.com/fiddler)) disponibile per il runbook nella proprietà **RequestBody** di **WebhookData**.</span><span class="sxs-lookup"><span data-stu-id="0a770-231">The following image shows the body of the request (using a [Fiddler](http://www.telerik.com/fiddler) trace)  that is available to the runbook in the **RequestBody** property of **WebhookData**.</span></span> <span data-ttu-id="0a770-232">Viene formattata come JSON perché questo era il formato incluso nel corpo della richiesta.</span><span class="sxs-lookup"><span data-stu-id="0a770-232">This is formatted as JSON because that was the format that was included in the body of the request.</span></span>     

![Pulsante Webhooks](media/automation-webhooks/webhook-request-body.png)

<span data-ttu-id="0a770-234">L'immagine seguente mostra la richiesta inviata da Windows PowerShell e la risposta risultante.</span><span class="sxs-lookup"><span data-stu-id="0a770-234">The following image shows the request being sent from Windows PowerShell and the resulting response.</span></span>  <span data-ttu-id="0a770-235">L'ID processo viene estratto dalla risposta e convertito in una stringa.</span><span class="sxs-lookup"><span data-stu-id="0a770-235">The job id is extracted from the response and converted to a string.</span></span>

![Pulsante Webhooks](media/automation-webhooks/webhook-request-response.png)

<span data-ttu-id="0a770-237">Il Runbook di esempio seguente accetta la richiesta di esempio precedente e avvia le macchine virtuali specificate nel corpo della richiesta.</span><span class="sxs-lookup"><span data-stu-id="0a770-237">The following sample runbook accepts the previous example request and starts the virtual machines specified in the request body.</span></span>

    workflow Test-StartVirtualMachinesFromWebhook
    {
        param (
            [object]$WebhookData
        )

        # If runbook was called from Webhook, WebhookData will not be null.
        if ($WebhookData -ne $null) {

            # Collect properties of WebhookData
            $WebhookName     =     $WebhookData.WebhookName
            $WebhookHeaders =     $WebhookData.RequestHeader
            $WebhookBody     =     $WebhookData.RequestBody

            # Collect individual headers. VMList converted from JSON.
            $From = $WebhookHeaders.From
            $VMList = ConvertFrom-Json -InputObject $WebhookBody
            Write-Output "Runbook started from webhook $WebhookName by $From."

            # Authenticate to Azure resources
            $Cred = Get-AutomationPSCredential -Name 'MyAzureCredential'
            Add-AzureAccount -Credential $Cred

            # Start each virtual machine
            foreach ($VM in $VMList)
            {
                $VMName = $VM.Name
                Write-Output "Starting $VMName"
                Start-AzureVM -Name $VM.Name -ServiceName $VM.ServiceName
            }
        }
        else {
            Write-Error "Runbook mean to be started only from webhook."
        }
    }


## <a name="starting-runbooks-in-response-to-azure-alerts"></a><span data-ttu-id="0a770-238">Avvio di runbook in risposta agli avvisi di Azure</span><span class="sxs-lookup"><span data-stu-id="0a770-238">Starting runbooks in response to Azure alerts</span></span>
<span data-ttu-id="0a770-239">I runbook abilitati per i webhook possono essere usati in risposta agli [avvisi di Azure](../monitoring-and-diagnostics/insights-receive-alert-notifications.md).</span><span class="sxs-lookup"><span data-stu-id="0a770-239">Webhook-enabled runbooks can be used to react to [Azure alerts](../monitoring-and-diagnostics/insights-receive-alert-notifications.md).</span></span> <span data-ttu-id="0a770-240">È possibile monitorare le risorse in Azure grazie alla raccolta di statistiche relative, ad esempio, a prestazioni, disponibilità e uso con l'aiuto degli avvisi di Azure.</span><span class="sxs-lookup"><span data-stu-id="0a770-240">Resources in Azure can be monitored by collecting the statistics like performance, availability and usage with the help of Azure alerts.</span></span> <span data-ttu-id="0a770-241">È possibile ricevere avvisi basati su metriche o eventi di monitoraggio per i servizi di Azure, attualmente gli account di automazione supportano solo le metriche.</span><span class="sxs-lookup"><span data-stu-id="0a770-241">You can receive an alert based on monitoring metrics or events for your Azure resources, currently Automation Accounts support only metrics.</span></span> <span data-ttu-id="0a770-242">Quando il valore di una metrica specifica supera la soglia assegnata o se l'evento configurato viene attivato quando una notifica viene inviata all'amministratore o ai coamministratori del servizio per risolvere l'avviso, per altre informazioni sulle metriche e sugli eventi, vedere gli [avvisi di Azure](../monitoring-and-diagnostics/insights-receive-alert-notifications.md).</span><span class="sxs-lookup"><span data-stu-id="0a770-242">When the value of a specified metric exceeds the threshold assigned or if the configured event is triggered then a notification is sent to the service admin or co-admins to resolve the alert, for more information on metrics and events please refer to [Azure alerts](../monitoring-and-diagnostics/insights-receive-alert-notifications.md).</span></span>

<span data-ttu-id="0a770-243">Oltre a usare gli avvisi di Azure come sistema di notifica, è anche possibile avviare i runbook in risposta agli avvisi.</span><span class="sxs-lookup"><span data-stu-id="0a770-243">Besides using Azure alerts as a notification system, you can also kick off runbooks in response to alerts.</span></span> <span data-ttu-id="0a770-244">Automazione di Azure offre la possibilità di eseguire runbook abilitati per i webhook con gli avvisi di Azure.</span><span class="sxs-lookup"><span data-stu-id="0a770-244">Azure Automation provides the capability to run webhook-enabled runbooks with Azure alerts.</span></span> <span data-ttu-id="0a770-245">Quando una metrica supera il valore di soglia configurato, la regola dell'avviso viene abilitata e attiva il webhook di automazione che a sua volta esegue il runbook.</span><span class="sxs-lookup"><span data-stu-id="0a770-245">When a metric exceeds the configured threshold value then the alert rule becomes active and triggers the automation webhook which in turn executes the runbook.</span></span>

![Webhook](media/automation-webhooks/webhook-alert.jpg)

### <a name="alert-context"></a><span data-ttu-id="0a770-247">Contesto dell'avviso</span><span class="sxs-lookup"><span data-stu-id="0a770-247">Alert context</span></span>
<span data-ttu-id="0a770-248">Se si considera una risorsa di Azure, ad esempio una macchina virtuale, l'uso della CPU del computer rappresenta una delle metriche fondamentali relative alle prestazioni.</span><span class="sxs-lookup"><span data-stu-id="0a770-248">Consider an Azure resource such as a virtual machine, CPU utilization of this machine is one of the key performance metric.</span></span> <span data-ttu-id="0a770-249">Se l'uso della CPU è pari al 100% o più di una certa quantità per un lungo periodo di tempo, si potrebbe voler riavviare la macchina virtuale per risolvere il problema.</span><span class="sxs-lookup"><span data-stu-id="0a770-249">If the CPU utilization is 100% or more than a certain amount for long period of time, you might want to restart the virtual machine to fix the problem.</span></span> <span data-ttu-id="0a770-250">Questo problema può essere risolto tramite la configurazione di una regola di avviso per la macchina virtuale. Tale regola userà la percentuale di CPU come metrica.</span><span class="sxs-lookup"><span data-stu-id="0a770-250">This can be solved by configuring an alert rule to the virtual machine and this rule takes CPU percentage as its metric.</span></span> <span data-ttu-id="0a770-251">La percentuale di CPU viene usata solo come esempio. È tuttavia possibile configurare numerose altre metriche per le risorse di Azure e riavviare la macchina virtuale per risolvere il problema. È comunque possibile configurare il runbook per eseguire altre operazioni.</span><span class="sxs-lookup"><span data-stu-id="0a770-251">CPU percentage here is just taken as an example but there are many other metrics that you can configure to your Azure resources and restarting the virtual machine is an action that is taken to fix this issue, you can configure the runbook to take other actions.</span></span>

<span data-ttu-id="0a770-252">Quando la regola di avviso viene abilitata e attiva il runbook abilitato per i webhook, la regola invia il contesto dell'avviso al runbook.</span><span class="sxs-lookup"><span data-stu-id="0a770-252">When this the alert rule becomes active and triggers the webhook-enabled runbook, it sends the alert context to the runbook.</span></span> <span data-ttu-id="0a770-253">Il [contesto dell'avviso](../monitoring-and-diagnostics/insights-receive-alert-notifications.md) contiene dettagli, tra cui i valori di **SubscriptionID**, **ResourceGroupName**, **ResourceName**, **ResourceType**, **ResourceId** e **Timestamp** richiesti dal runbook per identificare la risorsa in cui verrà eseguita l'azione.</span><span class="sxs-lookup"><span data-stu-id="0a770-253">[Alert context](../monitoring-and-diagnostics/insights-receive-alert-notifications.md) contains details including **SubscriptionID**, **ResourceGroupName**, **ResourceName**, **ResourceType**, **ResourceId** and **Timestamp** which are required for the runbook to identify the resource on which it will be taking action.</span></span> <span data-ttu-id="0a770-254">Il contesto dell'avviso è incorporato nel corpo del contesto dell'oggetto **WebhookData** inviato al runbook, a cui è possibile accedere con la proprietà **Webhook.RequestBody**.</span><span class="sxs-lookup"><span data-stu-id="0a770-254">Alert context is embedded in the body part of the **WebhookData** object sent to the runbook and it can be accessed with **Webhook.RequestBody** property</span></span>

### <a name="example"></a><span data-ttu-id="0a770-255">Esempio</span><span class="sxs-lookup"><span data-stu-id="0a770-255">Example</span></span>
<span data-ttu-id="0a770-256">Creare una macchina virtuale di Azure nella sottoscrizione corrente e associare un [avviso per monitorare la metrica relativa alla percentuale della CPU](../monitoring-and-diagnostics/insights-receive-alert-notifications.md).</span><span class="sxs-lookup"><span data-stu-id="0a770-256">Create an Azure virtual machine in your subscription and associate an [alert to monitor CPU percentage metric](../monitoring-and-diagnostics/insights-receive-alert-notifications.md).</span></span> <span data-ttu-id="0a770-257">Durante la creazione dell'avviso assicurarsi di popolare il campo del webhook con l'URL del webhook generato durante la creazione del webhook stesso.</span><span class="sxs-lookup"><span data-stu-id="0a770-257">While creating the alert make sure you populate the webhook field with the URL of the webhook which was generated while creating the webhook.</span></span>

<span data-ttu-id="0a770-258">Il seguente runbook di esempio viene attivato quando la regola dell'avviso diventa attiva e raccoglie i parametri del contesto dell'avviso. Tali parametri consentono al runbook di identificare la risorsa in cui verrà eseguita l'azione.</span><span class="sxs-lookup"><span data-stu-id="0a770-258">The following sample runbook is triggered when the alert rule becomes active and it collects the Alert context parameters which are required for the runbook to identify the resource on which it will be taking action.</span></span>

    workflow Invoke-RunbookUsingAlerts
    {
        param (      
            [object]$WebhookData
        )

        # If runbook was called from Webhook, WebhookData will not be null.
        if ($WebhookData -ne $null) {   
            # Collect properties of WebhookData.
            $WebhookName    =   $WebhookData.WebhookName
            $WebhookBody    =   $WebhookData.RequestBody
            $WebhookHeaders =   $WebhookData.RequestHeader

            # Outputs information on the webhook name that called This
            Write-Output "This runbook was started from webhook $WebhookName."


            # Obtain the WebhookBody containing the AlertContext
            $WebhookBody = (ConvertFrom-Json -InputObject $WebhookBody)
            Write-Output "`nWEBHOOK BODY"
            Write-Output "============="
            Write-Output $WebhookBody

            # Obtain the AlertContext     
            $AlertContext = [object]$WebhookBody.context

            # Some selected AlertContext information
            Write-Output "`nALERT CONTEXT DATA"
            Write-Output "==================="
            Write-Output $AlertContext.name
            Write-Output $AlertContext.subscriptionId
            Write-Output $AlertContext.resourceGroupName
            Write-Output $AlertContext.resourceName
            Write-Output $AlertContext.resourceType
            Write-Output $AlertContext.resourceId
            Write-Output $AlertContext.timestamp

            # Act on the AlertContext data, in our case restarting the VM.
            # Authenticate to your Azure subscription using Organization ID to be able to restart that Virtual Machine.
            $cred = Get-AutomationPSCredential -Name "MyAzureCredential"
            Add-AzureAccount -Credential $cred
            Select-AzureSubscription -subscriptionName "Visual Studio Ultimate with MSDN"

            #Check the status property of the VM
            Write-Output "Status of VM before taking action"
            Get-AzureVM -Name $AlertContext.resourceName -ServiceName $AlertContext.resourceName
            Write-Output "Restarting VM"

            # Restart the VM by passing VM name and Service name which are same in this case
            Restart-AzureVM -ServiceName $AlertContext.resourceName -Name $AlertContext.resourceName
            Write-Output "Status of VM after alert is active and takes action"
            Get-AzureVM -Name $AlertContext.resourceName -ServiceName $AlertContext.resourceName
        }
        else  
        {
            Write-Error "This runbook is meant to only be started from a webhook."  
        }  
    }



## <a name="next-steps"></a><span data-ttu-id="0a770-259">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="0a770-259">Next steps</span></span>
* <span data-ttu-id="0a770-260">Per informazioni dettagliate sulle diverse modalità disponibili per l'avvio dei runbook, vedere [Avvio di un runbook](automation-starting-a-runbook.md).</span><span class="sxs-lookup"><span data-stu-id="0a770-260">For details on different ways to start a runbook, see [Starting a Runbook](automation-starting-a-runbook.md).</span></span>
* <span data-ttu-id="0a770-261">Per informazioni sulla visualizzazione dello stato di un processo del runbook, vedere [Esecuzione di runbook in Automazione di Azure](automation-runbook-execution.md).</span><span class="sxs-lookup"><span data-stu-id="0a770-261">For information on viewing the Status of a Runbook Job, refer to [Runbook execution in Azure Automation](automation-runbook-execution.md).</span></span>
* <span data-ttu-id="0a770-262">Per informazioni su come usare Automazione di Azure per agire sugli avvisi di Azure, vedere [Soluzione di Automazione di Azure: risolvere gli avvisi delle macchine virtuali di Azure](automation-azure-vm-alert-integration.md).</span><span class="sxs-lookup"><span data-stu-id="0a770-262">To learn how to use Azure Automation to take action on Azure Alerts, see [Remediate Azure VM Alerts with Automation Runbooks](automation-azure-vm-alert-integration.md).</span></span>

---
title: un runbook di automazione di Azure con un webhook aaaStarting | Documenti Microsoft
description: Un webhook che consente a un client toostart un runbook in automazione di Azure da una chiamata HTTP.  Questo articolo viene descritto come toocreate un webhook e come toocall uno toostart un runbook.
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
ms.openlocfilehash: ca6cde66b3784ceb5d0bc5921cee87aea74cb150
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="starting-an-azure-automation-runbook-with-a-webhook"></a><span data-ttu-id="13f56-104">Avviare un runbook di Automazione di Azure con un webhook</span><span class="sxs-lookup"><span data-stu-id="13f56-104">Starting an Azure Automation runbook with a webhook</span></span>
<span data-ttu-id="13f56-105">Oggetto *webhook* consente toostart un determinato runbook in automazione di Azure tramite una singola richiesta HTTP.</span><span class="sxs-lookup"><span data-stu-id="13f56-105">A *webhook* allows you toostart a particular runbook in Azure Automation through a single HTTP request.</span></span> <span data-ttu-id="13f56-106">In questo modo i servizi esterni, ad esempio Visual Studio Team Services, GitHub, Microsoft Operations Management Suite Log Analitica o applicazioni personalizzate toostart runbook senza implementare una soluzione completa utilizzando hello API di automazione di Azure.</span><span class="sxs-lookup"><span data-stu-id="13f56-106">This allows external services such as Visual Studio Team Services, GitHub, Microsoft Operations Management Suite Log Analytics, or custom applications toostart runbooks without implementing a full solution using hello Azure Automation API.</span></span>  
<span data-ttu-id="13f56-107">![Panoramica dei webhook](media/automation-webhooks/webhook-overview-image.png)</span><span class="sxs-lookup"><span data-stu-id="13f56-107">![WebhooksOverview](media/automation-webhooks/webhook-overview-image.png)</span></span>

<span data-ttu-id="13f56-108">È possibile confrontare webhook tooother metodi di avvio di un runbook in [avvio di un runbook in automazione di Azure](automation-starting-a-runbook.md)</span><span class="sxs-lookup"><span data-stu-id="13f56-108">You can compare webhooks tooother methods of starting a runbook in [Starting a runbook in Azure Automation](automation-starting-a-runbook.md)</span></span>

## <a name="details-of-a-webhook"></a><span data-ttu-id="13f56-109">Informazioni dettagliate sui webhook</span><span class="sxs-lookup"><span data-stu-id="13f56-109">Details of a webhook</span></span>
<span data-ttu-id="13f56-110">Hello nella tabella seguente vengono descritte hello proprietà che devono essere configurati per un webhook.</span><span class="sxs-lookup"><span data-stu-id="13f56-110">hello following table describes hello properties that you must configure for a webhook.</span></span>

| <span data-ttu-id="13f56-111">Proprietà</span><span class="sxs-lookup"><span data-stu-id="13f56-111">Property</span></span> | <span data-ttu-id="13f56-112">Descrizione</span><span class="sxs-lookup"><span data-stu-id="13f56-112">Description</span></span> |
|:--- |:--- |
| <span data-ttu-id="13f56-113">Nome</span><span class="sxs-lookup"><span data-stu-id="13f56-113">Name</span></span> |<span data-ttu-id="13f56-114">È possibile specificare qualsiasi nome desiderato per un webhook poiché si tratta di non esposti toohello client.</span><span class="sxs-lookup"><span data-stu-id="13f56-114">You can provide any name you want for a webhook since this is not exposed toohello client.</span></span>  <span data-ttu-id="13f56-115">Viene utilizzato solo per si tooidentify hello runbook in automazione di Azure.</span><span class="sxs-lookup"><span data-stu-id="13f56-115">It is only used for you tooidentify hello runbook in Azure Automation.</span></span> <br>  <span data-ttu-id="13f56-116">Come procedura consigliata, è necessario assegnare un nome toohello correlati client che verrà usato hello webhook.</span><span class="sxs-lookup"><span data-stu-id="13f56-116">As a best practice, you should give hello webhook a name related toohello client that will use it.</span></span> |
| <span data-ttu-id="13f56-117">URL</span><span class="sxs-lookup"><span data-stu-id="13f56-117">URL</span></span> |<span data-ttu-id="13f56-118">URL Hello del webhook hello è l'indirizzo di hello univoco che un client chiama con un runbook di hello toostart HTTP POST collegata toohello webhook.</span><span class="sxs-lookup"><span data-stu-id="13f56-118">hello URL of hello webhook is hello unique address that a client calls with an HTTP POST toostart hello runbook linked toohello webhook.</span></span>  <span data-ttu-id="13f56-119">Viene generato automaticamente quando si crea hello webhook.</span><span class="sxs-lookup"><span data-stu-id="13f56-119">It is automatically generated when you create hello webhook.</span></span>  <span data-ttu-id="13f56-120">Non è possibile specificare un URL personalizzato.</span><span class="sxs-lookup"><span data-stu-id="13f56-120">You cannot specify a custom URL.</span></span> <br> <br>  <span data-ttu-id="13f56-121">Hello URL contiene un token di sicurezza che consente di hello runbook toobe richiamato da un sistema di terze parti con alcuna ulteriore autenticazione.</span><span class="sxs-lookup"><span data-stu-id="13f56-121">hello URL contains a security token that allows hello runbook toobe invoked by a third party system with no further authentication.</span></span> <span data-ttu-id="13f56-122">Per questo motivo, deve essere considerato come una password.</span><span class="sxs-lookup"><span data-stu-id="13f56-122">For this reason, it should be treated like a password.</span></span>  <span data-ttu-id="13f56-123">Per motivi di sicurezza, è possibile solo hello di visualizzazione che URL nel portale di Azure all'indirizzo hello ora hello webhook hello viene creato.</span><span class="sxs-lookup"><span data-stu-id="13f56-123">For security reasons, you can only view hello URL in hello Azure portal at hello time hello webhook is created.</span></span> <span data-ttu-id="13f56-124">Si noti hello URL in un luogo sicuro per un utilizzo futuro.</span><span class="sxs-lookup"><span data-stu-id="13f56-124">You should note hello URL in a secure location for future use.</span></span> |
| <span data-ttu-id="13f56-125">Expiration date</span><span class="sxs-lookup"><span data-stu-id="13f56-125">Expiration date</span></span> |<span data-ttu-id="13f56-126">Analogamente a un certificato, un webhook ha una data di scadenza oltre la quale non può più essere usato.</span><span class="sxs-lookup"><span data-stu-id="13f56-126">Like a certificate, each webhook has an expiration date at which time it can no longer be used.</span></span>  <span data-ttu-id="13f56-127">Dopo aver creato il webhook hello, è possibile modificare la data di scadenza.</span><span class="sxs-lookup"><span data-stu-id="13f56-127">This expiration date can be modified after hello webhook is created.</span></span> |
| <span data-ttu-id="13f56-128">Enabled</span><span class="sxs-lookup"><span data-stu-id="13f56-128">Enabled</span></span> |<span data-ttu-id="13f56-129">Un webhook viene abilitato per impostazione predefinita nel momento in cui viene creato.</span><span class="sxs-lookup"><span data-stu-id="13f56-129">A webhook is enabled by default when it is created.</span></span>  <span data-ttu-id="13f56-130">Se si imposta la proprietà tooDisabled, quindi nessun client sarà in grado di toouse è.</span><span class="sxs-lookup"><span data-stu-id="13f56-130">If you set it tooDisabled, then no client will be able toouse it.</span></span>  <span data-ttu-id="13f56-131">È possibile impostare hello **abilitato** proprietà quando si creano hello webhook o in qualsiasi momento una volta viene creata.</span><span class="sxs-lookup"><span data-stu-id="13f56-131">You can set hello **Enabled** property when you create hello webhook or anytime once it is created.</span></span> |

### <a name="parameters"></a><span data-ttu-id="13f56-132">parameters</span><span class="sxs-lookup"><span data-stu-id="13f56-132">Parameters</span></span>
<span data-ttu-id="13f56-133">Un webhook è possibile definire i valori per parametri del runbook vengono utilizzati quando runbook hello viene avviata da quel webhook.</span><span class="sxs-lookup"><span data-stu-id="13f56-133">A webhook can define values for runbook parameters that are used when hello runbook is started by that webhook.</span></span> <span data-ttu-id="13f56-134">Hello webhook deve includere i valori per eventuali parametri obbligatori di hello runbook e possono includere valori per i parametri facoltativi.</span><span class="sxs-lookup"><span data-stu-id="13f56-134">hello webhook must include values for any mandatory parameters of hello runbook and may include values for optional parameters.</span></span> <span data-ttu-id="13f56-135">Un webhook tooa valore configurato di parametro può essere modificato anche dopo aver creato webhoook hello.</span><span class="sxs-lookup"><span data-stu-id="13f56-135">A parameter value configured tooa webhook can be modified even after creating hello webhoook.</span></span> <span data-ttu-id="13f56-136">Più webhook collegati tooa singolo runbook può utilizzare valori di parametro diversi.</span><span class="sxs-lookup"><span data-stu-id="13f56-136">Multiple webhooks linked tooa single runbook can each use different parameter values.</span></span>

<span data-ttu-id="13f56-137">Quando un client avvia un runbook tramite un webhook, è possibile eseguire l'override di valori di parametro hello definiti in webhook hello.</span><span class="sxs-lookup"><span data-stu-id="13f56-137">When a client starts a runbook using a webhook, it cannot override hello parameter values defined in hello webhook.</span></span>  <span data-ttu-id="13f56-138">dati tooreceive dal client di hello, hello runbook può accettare un singolo parametro chiamato **$WebhookData** di tipo [object] contenenti dati che il client hello include nella richiesta POST hello.</span><span class="sxs-lookup"><span data-stu-id="13f56-138">tooreceive data from hello client, hello runbook can accept a single parameter called **$WebhookData** of type [object] that will contain data that hello client includes in hello POST request.</span></span>

![Proprietà Webhookdata](media/automation-webhooks/webhook-data-properties.png)

<span data-ttu-id="13f56-140">Hello **$WebhookData** oggetto avrà hello le proprietà seguenti:</span><span class="sxs-lookup"><span data-stu-id="13f56-140">hello **$WebhookData** object will have hello following properties:</span></span>

| <span data-ttu-id="13f56-141">Proprietà</span><span class="sxs-lookup"><span data-stu-id="13f56-141">Property</span></span> | <span data-ttu-id="13f56-142">Descrizione</span><span class="sxs-lookup"><span data-stu-id="13f56-142">Description</span></span> |
|:--- |:--- |
| <span data-ttu-id="13f56-143">WebhookName</span><span class="sxs-lookup"><span data-stu-id="13f56-143">WebhookName</span></span> |<span data-ttu-id="13f56-144">nome Hello del webhook hello.</span><span class="sxs-lookup"><span data-stu-id="13f56-144">hello name of hello webhook.</span></span> |
| <span data-ttu-id="13f56-145">RequestHeader</span><span class="sxs-lookup"><span data-stu-id="13f56-145">RequestHeader</span></span> |<span data-ttu-id="13f56-146">Tabella hash contenente hello intestazioni della richiesta POST in arrivo hello.</span><span class="sxs-lookup"><span data-stu-id="13f56-146">Hash table containing hello headers of hello incoming POST request.</span></span> |
| <span data-ttu-id="13f56-147">RequestBody</span><span class="sxs-lookup"><span data-stu-id="13f56-147">RequestBody</span></span> |<span data-ttu-id="13f56-148">corpo Hello della richiesta POST in arrivo hello.</span><span class="sxs-lookup"><span data-stu-id="13f56-148">hello body of hello incoming POST request.</span></span>  <span data-ttu-id="13f56-149">Manterrà tutta la formattazione, ad esempio stringa, JSON, XML o dati codificati in un form.</span><span class="sxs-lookup"><span data-stu-id="13f56-149">This will retain any formatting such as string, JSON, XML, or form encoded data.</span></span> <span data-ttu-id="13f56-150">Hello runbook deve essere scritto toowork con formato dati hello previsto.</span><span class="sxs-lookup"><span data-stu-id="13f56-150">hello runbook must be written toowork with hello data format that is expected.</span></span> |

<span data-ttu-id="13f56-151">Nessuna configurazione di prova webhook obbligatorio toosupport prova **$WebhookData** parametro e hello runbook non è necessario tooaccept è.</span><span class="sxs-lookup"><span data-stu-id="13f56-151">There is no configuration of hello webhook required toosupport hello **$WebhookData** parameter, and hello runbook is not required tooaccept it.</span></span>  <span data-ttu-id="13f56-152">Se il runbook hello non definisce il parametro hello, i dettagli della richiesta di hello inviati dal client hello viene ignorato.</span><span class="sxs-lookup"><span data-stu-id="13f56-152">If hello runbook does not define hello parameter, then any details of hello request sent from hello client is ignored.</span></span>

<span data-ttu-id="13f56-153">Se si specifica un valore per $WebhookData quando si crea il webhook hello, tale valore sarà sottoposta a override all'avvio hello webhook hello runbook con i dati hello richiesta POST di hello del client, anche se hello client non include tutti i dati nel corpo della richiesta hello.</span><span class="sxs-lookup"><span data-stu-id="13f56-153">If you specify a value for $WebhookData when you create hello webhook, that value will be overriden when hello webhook starts hello runbook with hello data from hello client POST request, even if hello client does not include any data in hello request body.</span></span>  <span data-ttu-id="13f56-154">Se si avvia un runbook con $WebhookData utilizzando un metodo diverso da un webhook, è possibile fornire un valore per $Webhookdata che verrà riconosciuto dal runbook hello.</span><span class="sxs-lookup"><span data-stu-id="13f56-154">If you start a runbook that has $WebhookData using a method other than a webhook, you can provide a value for $Webhookdata that will be recognized by hello runbook.</span></span>  <span data-ttu-id="13f56-155">Questo valore deve essere un oggetto con hello stesso [proprietà](#details-of-a-webhook) come $Webhookdata runbook hello poter lavorare correttamente con esso, come se ha lavorato con WebhookData effettivo passato da un webhook.</span><span class="sxs-lookup"><span data-stu-id="13f56-155">This value should be an object with hello same [properties](#details-of-a-webhook) as $Webhookdata so that hello runbook can properly work with it as if it was working with actual WebhookData passed by a webhook.</span></span>

<span data-ttu-id="13f56-156">Ad esempio, se si inizia hello seguente runbook dal portale di Azure hello e si desidera toopass alcuni WebhookData di esempio per test, perché WebhookData è un oggetto, deve essere passata come JSON in hello dell'interfaccia utente.</span><span class="sxs-lookup"><span data-stu-id="13f56-156">For example, if you are starting hello following runbook from hello Azure Portal and want toopass some sample WebhookData for testing, since WebhookData is an object, it should be passed as JSON in hello UI.</span></span>

![Parametro WebhookData dall'interfaccia utente](media/automation-webhooks/WebhookData-parameter-from-UI.png)

<span data-ttu-id="13f56-158">Per hello sopra runbook, se si dispone delle seguenti proprietà per il parametro WebhookData hello hello:</span><span class="sxs-lookup"><span data-stu-id="13f56-158">For hello above runbook, if you have hello following properties for hello WebhookData parameter:</span></span>

1. <span data-ttu-id="13f56-159">WebhookName: *MyWebhook*</span><span class="sxs-lookup"><span data-stu-id="13f56-159">WebhookName: *MyWebhook*</span></span>
2. <span data-ttu-id="13f56-160">RequestHeader: *From=Test User*</span><span class="sxs-lookup"><span data-stu-id="13f56-160">RequestHeader: *From=Test User*</span></span>
3. <span data-ttu-id="13f56-161">RequestBody: *[“VM1”, “VM2”]*</span><span class="sxs-lookup"><span data-stu-id="13f56-161">RequestBody: *[“VM1”, “VM2”]*</span></span>

<span data-ttu-id="13f56-162">Passare quindi hello il valore JSON in hello dell'interfaccia utente per il parametro WebhookData hello seguente:</span><span class="sxs-lookup"><span data-stu-id="13f56-162">Then you would pass hello following JSON value in hello UI for hello WebhookData parameter:</span></span>  

* <span data-ttu-id="13f56-163">{"WebhookName":"MyWebhook", "RequestHeader":{"From":"Test User"}, "RequestBody":"[\"VM1\",\"VM2\"]"}</span><span class="sxs-lookup"><span data-stu-id="13f56-163">{"WebhookName":"MyWebhook", "RequestHeader":{"From":"Test User"}, "RequestBody":"[\"VM1\",\"VM2\"]"}</span></span>

![Parametro WebhookData Start dall'interfaccia utente](media/automation-webhooks/Start-WebhookData-parameter-from-UI.png)

> [!NOTE]
> <span data-ttu-id="13f56-165">i valori Hello di tutti i parametri di input vengono registrati con il processo di runbook hello.</span><span class="sxs-lookup"><span data-stu-id="13f56-165">hello values of all input parameters are logged with hello runbook job.</span></span>  <span data-ttu-id="13f56-166">Ciò significa che qualsiasi input fornito dal client hello nella richiesta webhook hello sarà tooanyone registrati e disponibili con il processo di automazione toohello di accesso.</span><span class="sxs-lookup"><span data-stu-id="13f56-166">This means that any input provided by hello client in hello webhook request will be logged and available tooanyone with access toohello automation job.</span></span>  <span data-ttu-id="13f56-167">Per questo motivo è consigliabile procedere con cautela quando si includono dati sensibili nelle chiamate di webhook.</span><span class="sxs-lookup"><span data-stu-id="13f56-167">For this reason, you should be cautious about including sensitive information in webhook calls.</span></span>
>

## <a name="security"></a><span data-ttu-id="13f56-168">Sicurezza</span><span class="sxs-lookup"><span data-stu-id="13f56-168">Security</span></span>
<span data-ttu-id="13f56-169">sicurezza di Hello di un webhook si basa su privacy hello del relativo URL che contiene un token di sicurezza che ne consenta toobe richiamato.</span><span class="sxs-lookup"><span data-stu-id="13f56-169">hello security of a webhook relies on hello privacy of its URL which contains a security token that allows it toobe invoked.</span></span> <span data-ttu-id="13f56-170">Automazione di Azure non esegue alcuna autenticazione sulla richiesta di hello fino a quando viene reso toohello URL sia corretto.</span><span class="sxs-lookup"><span data-stu-id="13f56-170">Azure Automation does not perform any authentication on hello request as long as it is made toohello correct URL.</span></span> <span data-ttu-id="13f56-171">Per questo motivo, webhook non devono essere utilizzati per i runbook che eseguono funzioni estremamente riservate senza utilizzare un metodo alternativo di convalida richiesta hello.</span><span class="sxs-lookup"><span data-stu-id="13f56-171">For this reason, webhooks should not be used for runbooks that perform highly sensitive functions without using an alternate means of validating hello request.</span></span>

<span data-ttu-id="13f56-172">È possibile includere logica all'interno di hello toodetermine di runbook che è stato chiamato da un webhook controllando hello **WebhookName** proprietà del parametro hello $WebhookData.</span><span class="sxs-lookup"><span data-stu-id="13f56-172">You can include logic within hello runbook toodetermine that it was called by a webhook by checking hello **WebhookName** property of hello $WebhookData parameter.</span></span> <span data-ttu-id="13f56-173">Hello runbook potrebbe eseguire un'ulteriore convalida mediante la ricerca di particolari informazioni di hello **RequestHeader** o **RequestBody** proprietà.</span><span class="sxs-lookup"><span data-stu-id="13f56-173">hello runbook could perform further validation by looking for particular information in hello **RequestHeader** or **RequestBody** properties.</span></span>

<span data-ttu-id="13f56-174">Un'altra strategia consiste toohave hello runbook eseguire una convalida di una condizione di esterna quando ricevuta una richiesta di webhook.</span><span class="sxs-lookup"><span data-stu-id="13f56-174">Another strategy is toohave hello runbook perform some validation of an external condition when it received a webhook request.</span></span>  <span data-ttu-id="13f56-175">Ad esempio, si consideri un runbook che viene chiamato da GitHub tutte le volte che un nuovo repository GitHub tooa di commit.</span><span class="sxs-lookup"><span data-stu-id="13f56-175">For example, consider a runbook that is called by GitHub whenever there is a new commit tooa GitHub repository.</span></span>  <span data-ttu-id="13f56-176">Hello runbook potrebbero connettersi toovalidate tooGitHub che il commit di una nuova semplicemente si è verificato prima di continuare.</span><span class="sxs-lookup"><span data-stu-id="13f56-176">hello runbook might connect tooGitHub toovalidate that a new commit had actually just occurred before continuing.</span></span>

## <a name="creating-a-webhook"></a><span data-ttu-id="13f56-177">Creazione di un webhook</span><span class="sxs-lookup"><span data-stu-id="13f56-177">Creating a webhook</span></span>
<span data-ttu-id="13f56-178">Utilizzare hello seguendo procedure toocreate un nuovo runbook tooa webhook collegati in hello portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="13f56-178">Use hello following procedure toocreate a new webhook linked tooa runbook in hello Azure portal.</span></span>

1. <span data-ttu-id="13f56-179">Da hello **pannello runbook** hello portale di Azure, fare clic su runbook hello hello webhook inizierà tooview il pannello di dettaglio.</span><span class="sxs-lookup"><span data-stu-id="13f56-179">From hello **Runbooks blade** in hello Azure portal, click hello runbook that hello webhook will start tooview its detail blade.</span></span>
2. <span data-ttu-id="13f56-180">Fare clic su **Webhook** nella parte superiore di hello di hello di hello pannello tooopen **Webhook aggiungere** blade.</span><span class="sxs-lookup"><span data-stu-id="13f56-180">Click **Webhook** at hello top of hello blade tooopen hello **Add Webhook** blade.</span></span> <br><span data-ttu-id="13f56-181">
   ![Pulsante Webhook](media/automation-webhooks/webhooks-button.png)</span><span class="sxs-lookup"><span data-stu-id="13f56-181">
![Webhooks button](media/automation-webhooks/webhooks-button.png)</span></span>
3. <span data-ttu-id="13f56-182">Fare clic su **creare nuovo webhook** tooopen hello **crea webhook pannello**.</span><span class="sxs-lookup"><span data-stu-id="13f56-182">Click **Create new webhook** tooopen hello **Create webhook blade**.</span></span>
4. <span data-ttu-id="13f56-183">Specificare un **nome**, **data di scadenza** per webhook hello e se deve essere abilitata.</span><span class="sxs-lookup"><span data-stu-id="13f56-183">Specify a **Name**, **Expiration Date** for hello webhook and whether it should be enabled.</span></span> <span data-ttu-id="13f56-184">Per altre informazioni su queste proprietà, vedere [Informazioni dettagliate sui webhook](#details-of-a-webhook) .</span><span class="sxs-lookup"><span data-stu-id="13f56-184">See [Details of a webhook](#details-of-a-webhook) for more information these properties.</span></span>
5. <span data-ttu-id="13f56-185">Fare clic sull'icona di copia hello e premere Ctrl + C toocopy hello URL del webhook hello.</span><span class="sxs-lookup"><span data-stu-id="13f56-185">Click hello copy icon and press Ctrl+C toocopy hello URL of hello webhook.</span></span>  <span data-ttu-id="13f56-186">Annotarlo in un luogo sicuro.</span><span class="sxs-lookup"><span data-stu-id="13f56-186">Then record it in a safe place.</span></span>  <span data-ttu-id="13f56-187">**Dopo aver creato il webhook hello, è possibile recuperare nuovamente hello URL.**</span><span class="sxs-lookup"><span data-stu-id="13f56-187">**Once you create hello webhook, you cannot retrieve hello URL again.**</span></span> <br><span data-ttu-id="13f56-188">
   ![URL webhook](media/automation-webhooks/copy-webhook-url.png)</span><span class="sxs-lookup"><span data-stu-id="13f56-188">
![Webhook URL](media/automation-webhooks/copy-webhook-url.png)</span></span>
6. <span data-ttu-id="13f56-189">Fare clic su **parametri** tooprovide valori per parametri del runbook hello.</span><span class="sxs-lookup"><span data-stu-id="13f56-189">Click **Parameters** tooprovide values for hello runbook parameters.</span></span>  <span data-ttu-id="13f56-190">Se il runbook di hello include i parametri obbligatori, quindi non sarà in grado di toocreate hello webhook a meno che non vengono forniti i valori.</span><span class="sxs-lookup"><span data-stu-id="13f56-190">If hello runbook has mandatory parameters, then you will not be able toocreate hello webhook unless values are provided.</span></span>
7. <span data-ttu-id="13f56-191">Fare clic su **crea** toocreate hello webhook.</span><span class="sxs-lookup"><span data-stu-id="13f56-191">Click **Create** toocreate hello webhook.</span></span>

## <a name="using-a-webhook"></a><span data-ttu-id="13f56-192">Uso di un webhook</span><span class="sxs-lookup"><span data-stu-id="13f56-192">Using a webhook</span></span>
<span data-ttu-id="13f56-193">toouse un webhook dopo che è stato creato, l'applicazione client deve eseguire un POST HTTP con hello URL per il webhook hello.</span><span class="sxs-lookup"><span data-stu-id="13f56-193">toouse a webhook after it has been created, your client application must issue an HTTP POST with hello URL for hello webhook.</span></span>  <span data-ttu-id="13f56-194">sintassi di Hello del webhook hello sarà nel seguente formato hello.</span><span class="sxs-lookup"><span data-stu-id="13f56-194">hello syntax of hello webhook will be in hello following format.</span></span>

    http://<Webhook Server>/token?=<Token Value>

<span data-ttu-id="13f56-195">Hello client riceverà uno dei seguenti codici restituiti da una richiesta POST hello hello.</span><span class="sxs-lookup"><span data-stu-id="13f56-195">hello client will receive one of hello following return codes from hello POST request.</span></span>  

| <span data-ttu-id="13f56-196">Codice</span><span class="sxs-lookup"><span data-stu-id="13f56-196">Code</span></span> | <span data-ttu-id="13f56-197">Testo</span><span class="sxs-lookup"><span data-stu-id="13f56-197">Text</span></span> | <span data-ttu-id="13f56-198">Descrizione</span><span class="sxs-lookup"><span data-stu-id="13f56-198">Description</span></span> |
|:--- |:--- |:--- |
| <span data-ttu-id="13f56-199">202</span><span class="sxs-lookup"><span data-stu-id="13f56-199">202</span></span> |<span data-ttu-id="13f56-200">Accepted</span><span class="sxs-lookup"><span data-stu-id="13f56-200">Accepted</span></span> |<span data-ttu-id="13f56-201">è stata accettata la richiesta di Hello e hello runbook è stato accodato correttamente.</span><span class="sxs-lookup"><span data-stu-id="13f56-201">hello request was accepted, and hello runbook was successfully queued.</span></span> |
| <span data-ttu-id="13f56-202">400</span><span class="sxs-lookup"><span data-stu-id="13f56-202">400</span></span> |<span data-ttu-id="13f56-203">Bad Request</span><span class="sxs-lookup"><span data-stu-id="13f56-203">Bad Request</span></span> |<span data-ttu-id="13f56-204">richiesta di Hello non è stata accettata per uno dei seguenti motivi hello.</span><span class="sxs-lookup"><span data-stu-id="13f56-204">hello request was not accepted for one of hello following reasons.</span></span> <ul> <li><span data-ttu-id="13f56-205">Hello webhook è scaduto.</span><span class="sxs-lookup"><span data-stu-id="13f56-205">hello webhook has expired.</span></span></li> <li><span data-ttu-id="13f56-206">Hello webhook è disabilitata.</span><span class="sxs-lookup"><span data-stu-id="13f56-206">hello webhook is disabled.</span></span></li> <li><span data-ttu-id="13f56-207">token Hello hello URL è valido.</span><span class="sxs-lookup"><span data-stu-id="13f56-207">hello token in hello URL is invalid.</span></span></li>  </ul> |
| <span data-ttu-id="13f56-208">404</span><span class="sxs-lookup"><span data-stu-id="13f56-208">404</span></span> |<span data-ttu-id="13f56-209">Non trovato</span><span class="sxs-lookup"><span data-stu-id="13f56-209">Not Found</span></span> |<span data-ttu-id="13f56-210">richiesta di Hello non è stata accettata per uno dei seguenti motivi hello.</span><span class="sxs-lookup"><span data-stu-id="13f56-210">hello request was not accepted for one of hello following reasons.</span></span> <ul> <li><span data-ttu-id="13f56-211">Hello webhook non è stato trovato.</span><span class="sxs-lookup"><span data-stu-id="13f56-211">hello webhook was not found.</span></span></li> <li><span data-ttu-id="13f56-212">Hello runbook non è stato trovato.</span><span class="sxs-lookup"><span data-stu-id="13f56-212">hello runbook was not found.</span></span></li> <li><span data-ttu-id="13f56-213">Impossibile trovare l'account di Hello.</span><span class="sxs-lookup"><span data-stu-id="13f56-213">hello account was not found.</span></span></li>  </ul> |
| <span data-ttu-id="13f56-214">500</span><span class="sxs-lookup"><span data-stu-id="13f56-214">500</span></span> |<span data-ttu-id="13f56-215">Internal Server Error</span><span class="sxs-lookup"><span data-stu-id="13f56-215">Internal Server Error</span></span> |<span data-ttu-id="13f56-216">Hello URL è valido, ma si è verificato un errore.</span><span class="sxs-lookup"><span data-stu-id="13f56-216">hello URL was valid, but an error occurred.</span></span>  <span data-ttu-id="13f56-217">Inviare nuovamente la richiesta hello.</span><span class="sxs-lookup"><span data-stu-id="13f56-217">Please resubmit hello request.</span></span> |

<span data-ttu-id="13f56-218">Supponendo che hello richiesta ha esito positivo, hello webhook risposta contiene come indicato di seguito id processo hello in formato JSON.</span><span class="sxs-lookup"><span data-stu-id="13f56-218">Assuming hello request is successful, hello webhook response contains hello job id in JSON format as follows.</span></span> <span data-ttu-id="13f56-219">Contiene un id di processo, ma il formato JSON hello consente per possibili miglioramenti futuri.</span><span class="sxs-lookup"><span data-stu-id="13f56-219">It will contain a single job id, but hello JSON format allows for potential future enhancements.</span></span>

    {"JobIds":["<JobId>"]}  

<span data-ttu-id="13f56-220">Hello client non può determinare quando viene completato il processo di runbook hello o lo stato di completamento da hello webhook.</span><span class="sxs-lookup"><span data-stu-id="13f56-220">hello client cannot determine when hello runbook job completes or its completion status from hello webhook.</span></span>  <span data-ttu-id="13f56-221">È possibile determinare queste informazioni utilizzando l'id di processo hello con un altro metodo, ad esempio [Windows PowerShell](http://msdn.microsoft.com/library/azure/dn690263.aspx) o hello [API di automazione di Azure](https://msdn.microsoft.com/library/azure/mt163826.aspx).</span><span class="sxs-lookup"><span data-stu-id="13f56-221">It can determine this information using hello job id with another method such as [Windows PowerShell](http://msdn.microsoft.com/library/azure/dn690263.aspx) or hello [Azure Automation API](https://msdn.microsoft.com/library/azure/mt163826.aspx).</span></span>

### <a name="example"></a><span data-ttu-id="13f56-222">Esempio</span><span class="sxs-lookup"><span data-stu-id="13f56-222">Example</span></span>
<span data-ttu-id="13f56-223">Hello di esempio seguente viene utilizzato Windows PowerShell toostart un runbook con un webhook.</span><span class="sxs-lookup"><span data-stu-id="13f56-223">hello following example uses Windows PowerShell toostart a runbook with a webhook.</span></span>  <span data-ttu-id="13f56-224">Si noti che qualsiasi linguaggio in grado di creare una richiesta HTTP può usare un webhook. Windows PowerShell viene usato qui solo come esempio.</span><span class="sxs-lookup"><span data-stu-id="13f56-224">Note that any language that can make an HTTP request can use a webhook; Windows PowerShell is just used here as an example.</span></span>

<span data-ttu-id="13f56-225">runbook Hello è previsto un elenco di macchine virtuali in formato JSON nel corpo di hello di hello richiesta.</span><span class="sxs-lookup"><span data-stu-id="13f56-225">hello runbook is expecting a list of virtual machines formatted in JSON in hello body of hello request.</span></span> <span data-ttu-id="13f56-226">È inoltre incluso informazioni che è l'avvio di runbook hello e hello data e l'ora viene avviato nell'intestazione hello hello richiesta.</span><span class="sxs-lookup"><span data-stu-id="13f56-226">We also are including information about who is starting hello runbook and hello date and time it is being started in hello header of hello request.</span></span>      

    $uri = "https://s1events.azure-automation.net/webhooks?token=8ud0dSrSo%2fvHWpYbklW%3c8s0GrOKJZ9Nr7zqcS%2bIQr4c%3d"
    $headers = @{"From"="user@contoso.com";"Date"="05/28/2015 15:47:00"}

    $vms  = @(
                @{ Name="vm01";ServiceName="vm01"},
                @{ Name="vm02";ServiceName="vm02"}
            )
    $body = ConvertTo-Json -InputObject $vms

    $response = Invoke-RestMethod -Method Post -Uri $uri -Headers $headers -Body $body
    $jobid = ConvertFrom-Json $response


<span data-ttu-id="13f56-227">Hello figura seguente vengono illustrate le informazioni di intestazione hello (utilizzando un [Fiddler](http://www.telerik.com/fiddler) traccia) dalla richiesta.</span><span class="sxs-lookup"><span data-stu-id="13f56-227">hello following image shows hello header information (using a [Fiddler](http://www.telerik.com/fiddler) trace) from this request.</span></span> <span data-ttu-id="13f56-228">Sono incluse le intestazioni standard di una richiesta HTTP in aggiunta toohello data personalizzato e da intestazioni che è stato aggiunto.</span><span class="sxs-lookup"><span data-stu-id="13f56-228">This includes standard headers of an HTTP request in addition toohello custom Date and From headers that we added.</span></span>  <span data-ttu-id="13f56-229">Ognuno di questi valori è runbook toohello disponibile in hello **RequestHeaders** proprietà di **WebhookData**.</span><span class="sxs-lookup"><span data-stu-id="13f56-229">Each of these values is available toohello runbook in hello **RequestHeaders** property of **WebhookData**.</span></span>

![Pulsante Webhooks](media/automation-webhooks/webhook-request-headers.png)

<span data-ttu-id="13f56-231">Hello immagine seguente viene illustrato hello corpo della richiesta di hello (utilizzando un [Fiddler](http://www.telerik.com/fiddler) traccia) che è disponibile toohello runbook hello **RequestBody** proprietà di **WebhookData**.</span><span class="sxs-lookup"><span data-stu-id="13f56-231">hello following image shows hello body of hello request (using a [Fiddler](http://www.telerik.com/fiddler) trace)  that is available toohello runbook in hello **RequestBody** property of **WebhookData**.</span></span> <span data-ttu-id="13f56-232">Questo è formattato come JSON, perché questo è il formato hello che è stato incluso nel corpo di hello di hello richiesta.</span><span class="sxs-lookup"><span data-stu-id="13f56-232">This is formatted as JSON because that was hello format that was included in hello body of hello request.</span></span>     

![Pulsante Webhooks](media/automation-webhooks/webhook-request-body.png)

<span data-ttu-id="13f56-234">Hello immagine seguente mostra la richiesta di hello inviata da Windows PowerShell e la risposta risultante hello.</span><span class="sxs-lookup"><span data-stu-id="13f56-234">hello following image shows hello request being sent from Windows PowerShell and hello resulting response.</span></span>  <span data-ttu-id="13f56-235">id di processo Hello viene estratto dalla risposta hello e stringa tooa convertito.</span><span class="sxs-lookup"><span data-stu-id="13f56-235">hello job id is extracted from hello response and converted tooa string.</span></span>

![Pulsante Webhooks](media/automation-webhooks/webhook-request-response.png)

<span data-ttu-id="13f56-237">Hello runbook di esempio seguente accetta una richiesta di esempio precedente hello e avvia le macchine virtuali hello specificate nel corpo della richiesta hello.</span><span class="sxs-lookup"><span data-stu-id="13f56-237">hello following sample runbook accepts hello previous example request and starts hello virtual machines specified in hello request body.</span></span>

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

            # Authenticate tooAzure resources
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
            Write-Error "Runbook mean toobe started only from webhook."
        }
    }


## <a name="starting-runbooks-in-response-tooazure-alerts"></a><span data-ttu-id="13f56-238">A partire da runbook avvisi tooAzure risposta</span><span class="sxs-lookup"><span data-stu-id="13f56-238">Starting runbooks in response tooAzure alerts</span></span>
<span data-ttu-id="13f56-239">Abilitato Webhook runbook può essere utilizzato tooreact troppo[gli avvisi di Azure](../monitoring-and-diagnostics/insights-receive-alert-notifications.md).</span><span class="sxs-lookup"><span data-stu-id="13f56-239">Webhook-enabled runbooks can be used tooreact too[Azure alerts](../monitoring-and-diagnostics/insights-receive-alert-notifications.md).</span></span> <span data-ttu-id="13f56-240">Le risorse in Azure possono essere monitorate tramite la raccolta di statistiche hello come prestazioni, disponibilità e utilizzo con l'aiuto di hello degli avvisi di Azure.</span><span class="sxs-lookup"><span data-stu-id="13f56-240">Resources in Azure can be monitored by collecting hello statistics like performance, availability and usage with hello help of Azure alerts.</span></span> <span data-ttu-id="13f56-241">È possibile ricevere avvisi basati su metriche o eventi di monitoraggio per i servizi di Azure, attualmente gli account di automazione supportano solo le metriche.</span><span class="sxs-lookup"><span data-stu-id="13f56-241">You can receive an alert based on monitoring metrics or events for your Azure resources, currently Automation Accounts support only metrics.</span></span> <span data-ttu-id="13f56-242">Quando il valore di hello di una specifica metrica supera la soglia di hello assegnata o se hello configurato evento viene generato una notifica viene inviata toohello servizio amministratore o co-amministratori tooresolve hello avviso, per ulteriori informazioni sulle metriche e gli eventi, vedere troppo[ Gli avvisi di Azure](../monitoring-and-diagnostics/insights-receive-alert-notifications.md).</span><span class="sxs-lookup"><span data-stu-id="13f56-242">When hello value of a specified metric exceeds hello threshold assigned or if hello configured event is triggered then a notification is sent toohello service admin or co-admins tooresolve hello alert, for more information on metrics and events please refer too[Azure alerts](../monitoring-and-diagnostics/insights-receive-alert-notifications.md).</span></span>

<span data-ttu-id="13f56-243">Oltre a utilizzare gli avvisi di Azure come un sistema di notifica, è possibile anche avviare i runbook in risposta tooalerts.</span><span class="sxs-lookup"><span data-stu-id="13f56-243">Besides using Azure alerts as a notification system, you can also kick off runbooks in response tooalerts.</span></span> <span data-ttu-id="13f56-244">Automazione di Azure fornisce hello funzionalità toorun abilitato webhook runbook con gli avvisi di Azure.</span><span class="sxs-lookup"><span data-stu-id="13f56-244">Azure Automation provides hello capability toorun webhook-enabled runbooks with Azure alerts.</span></span> <span data-ttu-id="13f56-245">Quando una metrica supera hello configurato il valore di soglia hello regola di avviso diventa attiva e trigger hello webhook di automazione che a sua volta esegue hello runbook.</span><span class="sxs-lookup"><span data-stu-id="13f56-245">When a metric exceeds hello configured threshold value then hello alert rule becomes active and triggers hello automation webhook which in turn executes hello runbook.</span></span>

![Webhook](media/automation-webhooks/webhook-alert.jpg)

### <a name="alert-context"></a><span data-ttu-id="13f56-247">Contesto dell'avviso</span><span class="sxs-lookup"><span data-stu-id="13f56-247">Alert context</span></span>
<span data-ttu-id="13f56-248">Si consideri una risorsa di Azure, ad esempio una macchina virtuale, utilizzo della CPU del computer è uno della metrica di prestazioni chiave hello.</span><span class="sxs-lookup"><span data-stu-id="13f56-248">Consider an Azure resource such as a virtual machine, CPU utilization of this machine is one of hello key performance metric.</span></span> <span data-ttu-id="13f56-249">Utilizzo della CPU hello è 100% o più di una certa quantità per lunghi periodi di tempo, è possibile problema hello toofix di toorestart hello macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="13f56-249">If hello CPU utilization is 100% or more than a certain amount for long period of time, you might want toorestart hello virtual machine toofix hello problem.</span></span> <span data-ttu-id="13f56-250">Questo può essere risolto configurando una macchina virtuale toohello di regola di avviso e questa regola ha la percentuale di CPU come la metrica.</span><span class="sxs-lookup"><span data-stu-id="13f56-250">This can be solved by configuring an alert rule toohello virtual machine and this rule takes CPU percentage as its metric.</span></span> <span data-ttu-id="13f56-251">Percentuale CPU qui viene eseguita solo come esempio, ma sono disponibili molte altre metriche che è possibile configurare tooyour Azure risorse e riavvio della macchina virtuale hello è un'azione che viene eseguita toofix questo problema, è possibile configurare hello runbook tootake altre azioni.</span><span class="sxs-lookup"><span data-stu-id="13f56-251">CPU percentage here is just taken as an example but there are many other metrics that you can configure tooyour Azure resources and restarting hello virtual machine is an action that is taken toofix this issue, you can configure hello runbook tootake other actions.</span></span>

<span data-ttu-id="13f56-252">Quando la regola di avviso hello diventa attiva e trigger hello abilitato webhook runbook, invia hello al contesto dell'avviso toohello runbook.</span><span class="sxs-lookup"><span data-stu-id="13f56-252">When this hello alert rule becomes active and triggers hello webhook-enabled runbook, it sends hello alert context toohello runbook.</span></span> <span data-ttu-id="13f56-253">[Contesto dell'avviso](../monitoring-and-diagnostics/insights-receive-alert-notifications.md) contiene i dettagli inclusi **SubscriptionID**, **ResourceGroupName**, **ResourceName**, **ResourceType**, **ResourceId** e **Timestamp** che sono necessari per la risorsa di hello runbook tooidentify hello in cui in corso azione.</span><span class="sxs-lookup"><span data-stu-id="13f56-253">[Alert context](../monitoring-and-diagnostics/insights-receive-alert-notifications.md) contains details including **SubscriptionID**, **ResourceGroupName**, **ResourceName**, **ResourceType**, **ResourceId** and **Timestamp** which are required for hello runbook tooidentify hello resource on which it will be taking action.</span></span> <span data-ttu-id="13f56-254">Avviso di contesto è incorporato nella parte corpo hello di hello **WebhookData** oggetto runbook toohello inviato e sono accessibili con **Webhook.RequestBody** proprietà</span><span class="sxs-lookup"><span data-stu-id="13f56-254">Alert context is embedded in hello body part of hello **WebhookData** object sent toohello runbook and it can be accessed with **Webhook.RequestBody** property</span></span>

### <a name="example"></a><span data-ttu-id="13f56-255">Esempio</span><span class="sxs-lookup"><span data-stu-id="13f56-255">Example</span></span>
<span data-ttu-id="13f56-256">Creare una macchina virtuale di Azure nella sottoscrizione e associare un [avviso metriche Percentuale CPU toomonitor](../monitoring-and-diagnostics/insights-receive-alert-notifications.md).</span><span class="sxs-lookup"><span data-stu-id="13f56-256">Create an Azure virtual machine in your subscription and associate an [alert toomonitor CPU percentage metric](../monitoring-and-diagnostics/insights-receive-alert-notifications.md).</span></span> <span data-ttu-id="13f56-257">Durante la creazione avviso hello assicurarsi che inserire hello webhook campo hello URL del webhook hello generato durante la creazione del webhook hello.</span><span class="sxs-lookup"><span data-stu-id="13f56-257">While creating hello alert make sure you populate hello webhook field with hello URL of hello webhook which was generated while creating hello webhook.</span></span>

<span data-ttu-id="13f56-258">runbook di esempio seguente Hello viene generato quando la regola di avviso hello diventa attiva e raccoglie i parametri di contesto dell'avviso hello che sono necessari per la risorsa di hello runbook tooidentify hello in cui in corso azione.</span><span class="sxs-lookup"><span data-stu-id="13f56-258">hello following sample runbook is triggered when hello alert rule becomes active and it collects hello Alert context parameters which are required for hello runbook tooidentify hello resource on which it will be taking action.</span></span>

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

            # Outputs information on hello webhook name that called This
            Write-Output "This runbook was started from webhook $WebhookName."


            # Obtain hello WebhookBody containing hello AlertContext
            $WebhookBody = (ConvertFrom-Json -InputObject $WebhookBody)
            Write-Output "`nWEBHOOK BODY"
            Write-Output "============="
            Write-Output $WebhookBody

            # Obtain hello AlertContext     
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

            # Act on hello AlertContext data, in our case restarting hello VM.
            # Authenticate tooyour Azure subscription using Organization ID toobe able toorestart that Virtual Machine.
            $cred = Get-AutomationPSCredential -Name "MyAzureCredential"
            Add-AzureAccount -Credential $cred
            Select-AzureSubscription -subscriptionName "Visual Studio Ultimate with MSDN"

            #Check hello status property of hello VM
            Write-Output "Status of VM before taking action"
            Get-AzureVM -Name $AlertContext.resourceName -ServiceName $AlertContext.resourceName
            Write-Output "Restarting VM"

            # Restart hello VM by passing VM name and Service name which are same in this case
            Restart-AzureVM -ServiceName $AlertContext.resourceName -Name $AlertContext.resourceName
            Write-Output "Status of VM after alert is active and takes action"
            Get-AzureVM -Name $AlertContext.resourceName -ServiceName $AlertContext.resourceName
        }
        else  
        {
            Write-Error "This runbook is meant tooonly be started from a webhook."  
        }  
    }



## <a name="next-steps"></a><span data-ttu-id="13f56-259">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="13f56-259">Next steps</span></span>
* <span data-ttu-id="13f56-260">Per informazioni su modi toostart un runbook, vedere [avvio di un Runbook](automation-starting-a-runbook.md).</span><span class="sxs-lookup"><span data-stu-id="13f56-260">For details on different ways toostart a runbook, see [Starting a Runbook](automation-starting-a-runbook.md).</span></span>
* <span data-ttu-id="13f56-261">Per informazioni sulla visualizzazione hello stato di un Runbook Job, vedere troppo[esecuzione di Runbook in automazione di Azure](automation-runbook-execution.md).</span><span class="sxs-lookup"><span data-stu-id="13f56-261">For information on viewing hello Status of a Runbook Job, refer too[Runbook execution in Azure Automation](automation-runbook-execution.md).</span></span>
* <span data-ttu-id="13f56-262">toolearn toouse azione tootake di automazione di Azure per gli avvisi di Azure, vedere [correggere gli avvisi di macchina virtuale di Azure con i runbook di automazione](automation-azure-vm-alert-integration.md).</span><span class="sxs-lookup"><span data-stu-id="13f56-262">toolearn how toouse Azure Automation tootake action on Azure Alerts, see [Remediate Azure VM Alerts with Automation Runbooks](automation-azure-vm-alert-integration.md).</span></span>

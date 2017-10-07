---
title: aaaUse hello toocreate portale Azure un IoT Hub | Documenti Microsoft
description: Come toocreate, gestire ed eliminare hub IoT di Azure tramite hello portale di Azure. Include informazioni su piani tariffari, ridimensionamento, sicurezza e configurazione della messaggistica.
services: iot-hub
documentationcenter: 
author: dominicbetts
manager: timlt
editor: 
ms.assetid: 0909cd2b-4c1e-49e0-b68a-75532caf0a6a
ms.service: iot-hub
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/26/2017
ms.author: dobett
ms.openlocfilehash: 383968c90ee7ef3bff85a6c90efbf5f0e8fbb208
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="create-an-iot-hub-using-hello-azure-portal"></a><span data-ttu-id="04966-104">Creazione di un hub IoT utilizzando hello portale di Azure</span><span class="sxs-lookup"><span data-stu-id="04966-104">Create an IoT hub using hello Azure portal</span></span>

[!INCLUDE [iot-hub-resource-manager-selector](../../includes/iot-hub-resource-manager-selector.md)]

<span data-ttu-id="04966-105">L'articolo illustra:</span><span class="sxs-lookup"><span data-stu-id="04966-105">This article describes:</span></span>

* <span data-ttu-id="04966-106">Come toofind hello servizio IoT Hub in hello portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="04966-106">How toofind hello IoT Hub service in hello Azure portal.</span></span>
* <span data-ttu-id="04966-107">Come toocreate e gestire hub IoT.</span><span class="sxs-lookup"><span data-stu-id="04966-107">How toocreate and manage IoT hubs.</span></span>

## <a name="where-toofind-hello-iot-hub-service"></a><span data-ttu-id="04966-108">Dove toofind hello servizio IoT Hub</span><span class="sxs-lookup"><span data-stu-id="04966-108">Where toofind hello IoT Hub service</span></span>

<span data-ttu-id="04966-109">È possibile trovare hello servizio IoT Hub in hello posizioni nel portale di hello seguenti:</span><span class="sxs-lookup"><span data-stu-id="04966-109">You can find hello IoT Hub service in hello following locations in hello portal:</span></span>

* <span data-ttu-id="04966-110">Scegliere **+ Nuovo** e quindi scegliere **Internet delle cose**.</span><span class="sxs-lookup"><span data-stu-id="04966-110">Choose **+ New**, then choose **Internet of Things**.</span></span>
* <span data-ttu-id="04966-111">In hello Marketplace, scegliere **Internet of Things**.</span><span class="sxs-lookup"><span data-stu-id="04966-111">In hello Marketplace, choose **Internet of Things**.</span></span>

## <a name="create-an-iot-hub"></a><span data-ttu-id="04966-112">Creare un hub IoT</span><span class="sxs-lookup"><span data-stu-id="04966-112">Create an IoT hub</span></span>

<span data-ttu-id="04966-113">È possibile creare un hub IoT utilizzando hello dei seguenti metodi:</span><span class="sxs-lookup"><span data-stu-id="04966-113">You can create an IoT hub using hello following methods:</span></span>

* <span data-ttu-id="04966-114">Hello **+ nuovo** opzione apre il pannello hello mostrato nella seguente cattura di schermata hello.</span><span class="sxs-lookup"><span data-stu-id="04966-114">hello **+ New** option opens hello blade shown in hello following screen shot.</span></span> <span data-ttu-id="04966-115">Hello passaggi per la creazione di hub IoT hello tramite questo metodo e marketplace hello sono identici.</span><span class="sxs-lookup"><span data-stu-id="04966-115">hello steps for creating hello IoT hub through this method and through hello marketplace are identical.</span></span>
* <span data-ttu-id="04966-116">In hello Marketplace, scegliere **crea** pannello hello tooopen illustrato nella seguente cattura di schermata hello.</span><span class="sxs-lookup"><span data-stu-id="04966-116">In hello Marketplace, choose **Create** tooopen hello blade shown in hello following screen shot.</span></span>

<span data-ttu-id="04966-117">Hello nelle sezioni seguenti vengono descritti hello diversi passaggi toocreate un hub IoT:</span><span class="sxs-lookup"><span data-stu-id="04966-117">hello following sections describe hello several steps toocreate an IoT hub:</span></span>

### <a name="choose-hello-name-of-hello-iot-hub"></a><span data-ttu-id="04966-118">Scegliere nome hello dell'hub IoT hello</span><span class="sxs-lookup"><span data-stu-id="04966-118">Choose hello name of hello IoT hub</span></span>

<span data-ttu-id="04966-119">un hub IoT toocreate, è necessario assegnare un nome hub IoT hello.</span><span class="sxs-lookup"><span data-stu-id="04966-119">toocreate an IoT hub, you must name hello IoT hub.</span></span> <span data-ttu-id="04966-120">Questo nome deve essere univoco in tutti gli hub IoT.</span><span class="sxs-lookup"><span data-stu-id="04966-120">This name must be unique across all IoT hubs.</span></span>

[!INCLUDE [iot-hub-pii-note-naming-hub](../../includes/iot-hub-pii-note-naming-hub.md)]

### <a name="choose-hello-pricing-tier"></a><span data-ttu-id="04966-121">Scegliere hello a livello di prezzo</span><span class="sxs-lookup"><span data-stu-id="04966-121">Choose hello pricing tier</span></span>

<span data-ttu-id="04966-122">È possibile scegliere fra quattro piani: **Gratuito**, **Standard 1**, **Standard 2** e **Standard S3**.</span><span class="sxs-lookup"><span data-stu-id="04966-122">You can choose from four tiers: **Free**, **Standard 1** and **Standard 2**, and **Standard S3**.</span></span> <span data-ttu-id="04966-123">livello gratuito Hello consente solo 500 toobe dispositivi connessi hub IoT toohello e too8, 000 messaggi al giorno.</span><span class="sxs-lookup"><span data-stu-id="04966-123">hello free tier allows only 500 devices toobe connected toohello IoT hub and up too8,000 messages per day.</span></span>

<span data-ttu-id="04966-124">**S1 standard**: edizione hello S1 utilizzare per le soluzioni IoT con un numero elevato di dispositivi che ogni genera piccole quantità di dati.</span><span class="sxs-lookup"><span data-stu-id="04966-124">**Standard S1**: Use hello S1 edition for IoT solutions with a large number of devices that each generate small amounts of data.</span></span> <span data-ttu-id="04966-125">Ogni unità dell'edizione hello S1 consente backup too400, 000 messaggi al giorno per tutti i dispositivi connessi.</span><span class="sxs-lookup"><span data-stu-id="04966-125">Each unit of hello S1 edition allows up too400,000 messages per day across all connected devices.</span></span>

<span data-ttu-id="04966-126">**S2 standard**: edizione hello S2 utilizzare per le soluzioni di IoT in cui i dispositivi generare grandi quantità di dati.</span><span class="sxs-lookup"><span data-stu-id="04966-126">**Standard S2**: Use hello S2 edition for IoT solutions in which devices generate large amounts of data.</span></span> <span data-ttu-id="04966-127">Ogni unità dell'edizione S2 hello consente backup too6 milioni di messaggi al giorno tra tutti i dispositivi connessi.</span><span class="sxs-lookup"><span data-stu-id="04966-127">Each unit of hello S2 edition allows up too6 million messages per day between all connected devices.</span></span>

<span data-ttu-id="04966-128">**S3 standard**: edizione hello S3 utilizzare per le soluzioni di IoT che generano grandi quantità di dati.</span><span class="sxs-lookup"><span data-stu-id="04966-128">**Standard S3**: Use hello S3 edition for IoT solutions that generate large amounts of data.</span></span> <span data-ttu-id="04966-129">Ogni unità dell'edizione S3 hello consente backup too300 milioni di messaggi al giorno tra tutti i dispositivi connessi.</span><span class="sxs-lookup"><span data-stu-id="04966-129">Each unit of hello S3 edition allows up too300 million messages per day between all connected devices.</span></span>

![][4]

> [!NOTE]
> <span data-ttu-id="04966-130">L'hub IoT consente solo un hub gratuito per sottoscrizione di Azure.</span><span class="sxs-lookup"><span data-stu-id="04966-130">IoT Hub only allows one free hub per Azure subscription.</span></span>

### <a name="iot-hub-units"></a><span data-ttu-id="04966-131">Unità hub IoT</span><span class="sxs-lookup"><span data-stu-id="04966-131">IoT hub units</span></span>

<span data-ttu-id="04966-132">numero di Hello di messaggi consentiti per ogni unità al giorno dipende dal livello di prezzo dell'hub.</span><span class="sxs-lookup"><span data-stu-id="04966-132">hello number of messages allowed per unit per day depends on your hub's pricing tier.</span></span> <span data-ttu-id="04966-133">Ad esempio, se si desidera in ingresso di IoT hub toosupport di 700.000 messaggi hello, selezionare due unità di livello S1.</span><span class="sxs-lookup"><span data-stu-id="04966-133">For example, if you want hello IoT hub toosupport ingress of 700,000 messages, you choose two S1 tier units.</span></span>

### <a name="device-toocloud-partitions-and-resource-group"></a><span data-ttu-id="04966-134">Le partizioni toocloud dispositivo e gruppo di risorse</span><span class="sxs-lookup"><span data-stu-id="04966-134">Device toocloud partitions and resource group</span></span>

<span data-ttu-id="04966-135">È possibile modificare il numero di hello di partizioni per un hub IoT.</span><span class="sxs-lookup"><span data-stu-id="04966-135">You can change hello number of partitions for an IoT hub.</span></span> <span data-ttu-id="04966-136">numero di partizioni di Hello predefinito è 4, è possibile scegliere un numero diverso dall'elenco a discesa hello.</span><span class="sxs-lookup"><span data-stu-id="04966-136">hello default number of partitions is 4, you can choose a different number from hello drop-down list.</span></span>

<span data-ttu-id="04966-137">Non è necessario tooexplicitly creare un gruppo di risorse vuoto.</span><span class="sxs-lookup"><span data-stu-id="04966-137">You do not need tooexplicitly create an empty resource group.</span></span> <span data-ttu-id="04966-138">Quando si crea una risorsa, è possibile scegliere entrambi toocreate un nuovo o utilizzare un gruppo di risorse esistente.</span><span class="sxs-lookup"><span data-stu-id="04966-138">When you create a resource, you can choose either toocreate a new, or use an existing resource group.</span></span>

![][5]

### <a name="choose-subscription"></a><span data-ttu-id="04966-139">Scegliere la sottoscrizione</span><span class="sxs-lookup"><span data-stu-id="04966-139">Choose subscription</span></span>

<span data-ttu-id="04966-140">IoT Hub Azure automaticamente hello elenchi di account utente di hello le sottoscrizioni di Azure è collegato.</span><span class="sxs-lookup"><span data-stu-id="04966-140">Azure IoT Hub automatically lists hello Azure subscriptions hello user account is linked to.</span></span> <span data-ttu-id="04966-141">È possibile scegliere l'hub IoT per hello sottoscrizione di Azure tooassociate hello.</span><span class="sxs-lookup"><span data-stu-id="04966-141">You can choose hello Azure subscription tooassociate hello IoT hub to.</span></span>

### <a name="choose-hello-location"></a><span data-ttu-id="04966-142">Scegliere percorso hello</span><span class="sxs-lookup"><span data-stu-id="04966-142">Choose hello location</span></span>

<span data-ttu-id="04966-143">opzione del percorso Hello fornisce un elenco delle aree di hello in cui sono disponibili IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="04966-143">hello location option provides a list of hello regions where IoT Hub is available.</span></span>

### <a name="create-hello-iot-hub"></a><span data-ttu-id="04966-144">Creazione di hub IoT hello</span><span class="sxs-lookup"><span data-stu-id="04966-144">Create hello IoT hub</span></span>

<span data-ttu-id="04966-145">Dopo aver completato tutti i passaggi precedenti, è possibile creare l'hub IoT hello.</span><span class="sxs-lookup"><span data-stu-id="04966-145">When all previous steps are complete, you can create hello IoT hub.</span></span> <span data-ttu-id="04966-146">Fare clic su **crea** toostart hello toocreate processo back-end e distribuire l'hub IoT hello con le opzioni di hello scelto.</span><span class="sxs-lookup"><span data-stu-id="04966-146">Click **Create** toostart hello back-end process toocreate and deploy hello IoT hub with hello options you chose.</span></span>

<span data-ttu-id="04966-147">Come il tempo per hello distribuzione back-end toorun nei server di percorso appropriato hello può richiedere alcuni minuti toocreate hello l'hub IoT.</span><span class="sxs-lookup"><span data-stu-id="04966-147">It can take a few minutes toocreate hello IoT hub as it takes time for hello back-end deployment toorun on hello appropriate location servers.</span></span>

## <a name="change-hello-settings-of-hello-iot-hub"></a><span data-ttu-id="04966-148">Modificare le impostazioni di hello dell'hub IoT hello</span><span class="sxs-lookup"><span data-stu-id="04966-148">Change hello settings of hello IoT hub</span></span>

<span data-ttu-id="04966-149">È possibile modificare le impostazioni di hello di un hub IoT esistente dopo averlo creato da hello pannello IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="04966-149">You can change hello settings of an existing IoT hub after it is created from hello IoT Hub blade.</span></span>

![][8]

<span data-ttu-id="04966-150">**Criteri di accesso condiviso**: I criteri definiscono autorizzazioni hello per i dispositivi e servizi tooIoT tooconnect Hub.</span><span class="sxs-lookup"><span data-stu-id="04966-150">**Shared access policies**: These policies define hello permissions for devices and services tooconnect tooIoT Hub.</span></span> <span data-ttu-id="04966-151">È possibile accedere a questi criteri facendo clic su **Criteri di accesso condiviso** in **Generale**.</span><span class="sxs-lookup"><span data-stu-id="04966-151">You can access these policies by clicking **Shared access policies** under **General**.</span></span> <span data-ttu-id="04966-152">In questo pannello è possibile modificare i criteri esistenti o aggiungerne di nuovi.</span><span class="sxs-lookup"><span data-stu-id="04966-152">In this blade, you can either modify existing policies or add a new policy.</span></span>

### <a name="create-a-policy"></a><span data-ttu-id="04966-153">Creare un criterio</span><span class="sxs-lookup"><span data-stu-id="04966-153">Create a policy</span></span>

* <span data-ttu-id="04966-154">Fare clic su **Aggiungi** tooopen un pannello.</span><span class="sxs-lookup"><span data-stu-id="04966-154">Click **Add** tooopen a blade.</span></span> <span data-ttu-id="04966-155">È possibile immettere il nuovo nome di criterio hello e autorizzazioni hello che si desidera tooassociate con questo criterio, come illustrato nell'esempio hello figura:</span><span class="sxs-lookup"><span data-stu-id="04966-155">Here you can enter hello new policy name and hello permissions that you want tooassociate with this policy, as shown in hello following figure:</span></span>

    <span data-ttu-id="04966-156">Sono disponibili numerose autorizzazioni che possono essere associate a questi criteri condivisi.</span><span class="sxs-lookup"><span data-stu-id="04966-156">There are several permissions that can be associated with these shared policies.</span></span> <span data-ttu-id="04966-157">Hello **Registro di sistema leggere** e **scrittura del Registro di sistema** criteri concedono in lettura e registro identità toohello diritti di accesso in scrittura.</span><span class="sxs-lookup"><span data-stu-id="04966-157">hello **Registry read** and **Registry write** policies grant read and write access rights toohello identity registry.</span></span> <span data-ttu-id="04966-158">Opzione hello scrittura automaticamente sceglie l'opzione di lettura hello.</span><span class="sxs-lookup"><span data-stu-id="04966-158">Choosing hello write option automatically chooses hello read option.</span></span>

    <span data-ttu-id="04966-159">Hello **servizio connettersi** vengono concesse autorizzazioni tooaccess gli endpoint del servizio, ad esempio **ricevere da dispositivo a cloud**.</span><span class="sxs-lookup"><span data-stu-id="04966-159">hello **Service connect** policy grants permission tooaccess service endpoints such as **Receive device-to-cloud**.</span></span> <span data-ttu-id="04966-160">Hello **dispositivo connettersi** criteri concedono le autorizzazioni per l'invio e ricezione di messaggi utilizzando gli endpoint IoT Hub sul lato dispositivo hello.</span><span class="sxs-lookup"><span data-stu-id="04966-160">hello **Device connect** policy grants permissions for sending and receiving messages using hello IoT Hub device-side endpoints.</span></span>

* <span data-ttu-id="04966-161">Fare clic su **crea** tooadd questo nuovo elenco di criteri toohello esistente.</span><span class="sxs-lookup"><span data-stu-id="04966-161">Click **Create** tooadd this newly created policy toohello existing list.</span></span>

![][10]

## <a name="endpoints"></a><span data-ttu-id="04966-162">Endpoint</span><span class="sxs-lookup"><span data-stu-id="04966-162">Endpoints</span></span>

<span data-ttu-id="04966-163">Fare clic su **endpoint** toodisplay un elenco di endpoint per l'hub IoT hello che si desidera modificare.</span><span class="sxs-lookup"><span data-stu-id="04966-163">Click **Endpoints** toodisplay a list of endpoints for hello IoT hub that you are modifying.</span></span> <span data-ttu-id="04966-164">Esistono due tipi di endpoint: gli endpoint che sono integrati in hub IoT hello e gli endpoint aggiunti hub IoT toohello dopo la sua creazione.</span><span class="sxs-lookup"><span data-stu-id="04966-164">There are two types of endpoints: endpoints that are built into hello IoT hub, and endpoints that you add toohello IoT hub after its creation.</span></span>

![][11]

### <a name="built-in-endpoints"></a><span data-ttu-id="04966-165">Endpoint predefiniti</span><span class="sxs-lookup"><span data-stu-id="04966-165">Built-in endpoints</span></span>

<span data-ttu-id="04966-166">Esistono due endpoint predefiniti: **Cloud feedback toodevice** e **eventi**.</span><span class="sxs-lookup"><span data-stu-id="04966-166">There are two built-in endpoints: **Cloud toodevice feedback** and **Events**.</span></span>

* <span data-ttu-id="04966-167">**Cloud feedback toodevice** impostazioni: questa impostazione non ha due impostazioni secondarie: **Cloud tooDevice TTL** (time-to-live) e **periodo di conservazione** (in ore) per i messaggi hello.</span><span class="sxs-lookup"><span data-stu-id="04966-167">**Cloud toodevice feedback** settings: This setting has two subsettings: **Cloud tooDevice TTL** (time-to-live) and **Retention time** (in hours) for hello messages.</span></span> <span data-ttu-id="04966-168">Quando il primo crea un hub IoT, entrambe queste impostazioni hanno il valore predefinito hello di un'ora.</span><span class="sxs-lookup"><span data-stu-id="04966-168">When your first create an IoT hub, both these settings have hello default value of one hour.</span></span> <span data-ttu-id="04966-169">tooadjust queste impostazioni, utilizzare dispositivi di scorrimento hello o digitare i valori hello.</span><span class="sxs-lookup"><span data-stu-id="04966-169">tooadjust these settings, use hello sliders or type hello values.</span></span>
* <span data-ttu-id="04966-170">Impostazioni **Eventi**: questa impostazione presenta diverse impostazioni secondarie, alcune delle quali sono di sola lettura.</span><span class="sxs-lookup"><span data-stu-id="04966-170">**Events** settings: This setting has several subsettings, some of which are read-only.</span></span> <span data-ttu-id="04966-171">Hello seguente elenco vengono descritte queste impostazioni:</span><span class="sxs-lookup"><span data-stu-id="04966-171">hello following list describes these settings:</span></span>

  * <span data-ttu-id="04966-172">**Partizioni**: un valore predefinito viene impostato quando viene creato l'hub IoT hello.</span><span class="sxs-lookup"><span data-stu-id="04966-172">**Partitions**: A default value is set when hello IoT hub is created.</span></span> <span data-ttu-id="04966-173">È possibile modificare il numero di hello di partizioni tramite questa impostazione.</span><span class="sxs-lookup"><span data-stu-id="04966-173">You can change hello number of partitions through this setting.</span></span>

  * <span data-ttu-id="04966-174">**Nome compatibile con Hub eventi e l'endpoint**: quando viene creato l'hub IoT hello, un Hub eventi è stato creato internamente che è necessario accessibili toounder determinate circostanze.</span><span class="sxs-lookup"><span data-stu-id="04966-174">**Event Hub-compatible name and endpoint**: When hello IoT hub is created, an Event Hub is created internally that you may need access toounder certain circumstances.</span></span> <span data-ttu-id="04966-175">Non è possibile personalizzare i valori di nome e l'endpoint di hello compatibile con Hub eventi, ma è possibile copiarli facendo **copia**.</span><span class="sxs-lookup"><span data-stu-id="04966-175">You cannot customize hello Event Hub-compatible name and endpoint values but you can copy them by clicking **Copy**.</span></span>

  * <span data-ttu-id="04966-176">**Periodo di conservazione**: giorno tooone l'impostazione predefinita, ma è possibile modificarlo tramite l'elenco a discesa hello.</span><span class="sxs-lookup"><span data-stu-id="04966-176">**Retention Time**: Set tooone day by default but you can change it using hello drop-down list.</span></span> <span data-ttu-id="04966-177">Questo valore è espresso in giorni per l'impostazione di dispositivo a cloud hello.</span><span class="sxs-lookup"><span data-stu-id="04966-177">This value is in days for hello device-to-cloud setting.</span></span>

  * <span data-ttu-id="04966-178">**Gruppi di consumer**: gruppi di Consumer consentono a più messaggi di tooread Reader in modo indipendente dall'hub IoT hello.</span><span class="sxs-lookup"><span data-stu-id="04966-178">**Consumer Groups**: Consumer groups enable multiple readers tooread messages independently from hello IoT hub.</span></span> <span data-ttu-id="04966-179">Ogni hub IoT viene creato con un gruppo di consumer predefinito.</span><span class="sxs-lookup"><span data-stu-id="04966-179">Every IoT hub is created with a default consumer group.</span></span> <span data-ttu-id="04966-180">Tuttavia, è possibile aggiungere o eliminare l'hub IoT tooyour gruppi di consumer con questa impostazione.</span><span class="sxs-lookup"><span data-stu-id="04966-180">However, you can add or delete consumer groups tooyour IoT hubs using this setting.</span></span>

  > [!NOTE]
  > <span data-ttu-id="04966-181">gruppo di consumer predefinito Hello non può essere modificato o eliminato.</span><span class="sxs-lookup"><span data-stu-id="04966-181">hello default consumer group cannot be edited or deleted.</span></span>

### <a name="custom-endpoints"></a><span data-ttu-id="04966-182">Endpoint personalizzati</span><span class="sxs-lookup"><span data-stu-id="04966-182">Custom endpoints</span></span>

<span data-ttu-id="04966-183">È possibile aggiungere endpoint personalizzati su hub IoT utilizzando portale hello.</span><span class="sxs-lookup"><span data-stu-id="04966-183">You can add custom endpoints on your IoT hub using hello portal.</span></span> <span data-ttu-id="04966-184">Da hello **endpoint** pannello, fare clic su **Aggiungi** in hello tooopen superiore hello **aggiungere endpoint** blade.</span><span class="sxs-lookup"><span data-stu-id="04966-184">From hello **Endpoints** blade, click **Add** at hello top tooopen hello **Add endpoint** blade.</span></span> <span data-ttu-id="04966-185">Immettere informazioni hello necessarie, quindi fare clic su **OK**.</span><span class="sxs-lookup"><span data-stu-id="04966-185">Enter hello required information, then click **OK**.</span></span> <span data-ttu-id="04966-186">L'endpoint personalizzato è ora elencata in hello principale **endpoint** blade.</span><span class="sxs-lookup"><span data-stu-id="04966-186">Your custom endpoint is now listed in hello main **Endpoints** blade.</span></span>

![][13]

<span data-ttu-id="04966-187">Altre informazioni sugli endpoint personalizzati sono disponibili in [Reference - IoT hub endpoints][lnk-devguide-endpoints] (Riferimenti: endpoint di hub IoT).</span><span class="sxs-lookup"><span data-stu-id="04966-187">You can read more about custom endpoints in [Reference - IoT hub endpoints][lnk-devguide-endpoints].</span></span>

## <a name="routes"></a><span data-ttu-id="04966-188">Route</span><span class="sxs-lookup"><span data-stu-id="04966-188">Routes</span></span>

<span data-ttu-id="04966-189">Fare clic su **route** toomanage come IoT Hub recapita i messaggi da dispositivo a cloud.</span><span class="sxs-lookup"><span data-stu-id="04966-189">Click **Routes** toomanage how IoT Hub dispatches your device-to-cloud messages.</span></span>

![][14]

<span data-ttu-id="04966-190">È possibile aggiungere l'hub IoT tooyour route facendo **Aggiungi** nella parte superiore di hello di hello **route*** immissione delle informazioni necessarie hello e facendo clic su pannello **OK**.</span><span class="sxs-lookup"><span data-stu-id="04966-190">You can add routes tooyour IoT hub by clicking **Add** at hello top of hello **Routes*** blade, entering hello required information, and clicking **OK**.</span></span> <span data-ttu-id="04966-191">La route è quindi elencata in hello principale **route** blade.</span><span class="sxs-lookup"><span data-stu-id="04966-191">Your route is then listed in hello main **Routes** blade.</span></span> <span data-ttu-id="04966-192">È possibile modificare una route selezionandola nell'elenco di hello di route.</span><span class="sxs-lookup"><span data-stu-id="04966-192">You can edit a route by clicking it in hello list of routes.</span></span> <span data-ttu-id="04966-193">tooenable una route, selezionarlo nell'elenco di hello di route e impostare hello **abilitato** attivare o disattivare troppo**Off**.</span><span class="sxs-lookup"><span data-stu-id="04966-193">tooenable a route, click it in hello list of routes and set hello **Enabled** toggle too**Off**.</span></span> <span data-ttu-id="04966-194">modifica di hello toosave, fare clic su **OK** nella parte inferiore di hello del pannello hello.</span><span class="sxs-lookup"><span data-stu-id="04966-194">toosave hello change, click **OK** at hello bottom of hello blade.</span></span>

![][15]

## <a name="pricing-and-scale"></a><span data-ttu-id="04966-195">Prezzi e scalabilità</span><span class="sxs-lookup"><span data-stu-id="04966-195">Pricing and scale</span></span>

<span data-ttu-id="04966-196">Hello prezzi di un hub IoT esistente può essere modificato tramite hello **prezzi** le impostazioni, con hello le eccezioni seguenti:</span><span class="sxs-lookup"><span data-stu-id="04966-196">hello pricing of an existing IoT hub can be changed through hello **Pricing** settings, with hello following exceptions:</span></span>

* <span data-ttu-id="04966-197">Nell'implementazione corrente di hello, un hub IoT con uno SKU disponibile non è possibile modificare tooone livelli di hello, SKU a pagamento, o viceversa.</span><span class="sxs-lookup"><span data-stu-id="04966-197">In hello current implementation, an IoT hub with a free SKU cannot change tiers tooone of hello paid SKUs, or vice versa.</span></span>
* <span data-ttu-id="04966-198">Può esistere solo un hub IoT di livello gratuito nella sottoscrizione di Azure hello.</span><span class="sxs-lookup"><span data-stu-id="04966-198">There can only be one free tier IoT hub in hello Azure subscription.</span></span>

![][12]

<span data-ttu-id="04966-199">È possibile spostare da un livello superiore di toolower solo quando il numero di hello di messaggi inviati del giorno corrente superano la quota di hello per livello più basso hello.</span><span class="sxs-lookup"><span data-stu-id="04966-199">You can move from a higher toolower tier only when hello number of messages sent that day do exceed hello quota for hello lower tier.</span></span> <span data-ttu-id="04966-200">Ad esempio, se il numero di hello di messaggi al giorno supera 400.000, hello livello per hello IoT hub può essere modificato.</span><span class="sxs-lookup"><span data-stu-id="04966-200">For example, if hello number of messages per day exceeds 400,000, then hello tier for hello IoT hub can be changed.</span></span> <span data-ttu-id="04966-201">Tuttavia, se si modifica il livello di S1 toohello hub IoT hello è limitata per tale giorno.</span><span class="sxs-lookup"><span data-stu-id="04966-201">However, if you change toohello S1 tier then hello IoT hub is throttled for that day.</span></span>

## <a name="delete-hello-iot-hub"></a><span data-ttu-id="04966-202">Eliminare l'hub IoT hello</span><span class="sxs-lookup"><span data-stu-id="04966-202">Delete hello IoT hub</span></span>

<span data-ttu-id="04966-203">È possibile esplorare l'hub IoT toohello desiderato toodelete facendo **Sfoglia**, e scegliendo hello toodelete hub appropriato.</span><span class="sxs-lookup"><span data-stu-id="04966-203">You can browse toohello IoT hub you want toodelete by clicking **Browse**, and then choosing hello appropriate hub toodelete.</span></span> <span data-ttu-id="04966-204">toodelete hello hub IoT, fare clic su hello **eliminare** pulsante sotto il nome dell'hub IoT hello.</span><span class="sxs-lookup"><span data-stu-id="04966-204">toodelete hello IoT hub, click hello **Delete** button below hello IoT hub name.</span></span>

## <a name="next-steps"></a><span data-ttu-id="04966-205">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="04966-205">Next steps</span></span>

<span data-ttu-id="04966-206">Seguire questi toolearn collegamenti ulteriori informazioni sulla gestione di Azure IoT Hub:</span><span class="sxs-lookup"><span data-stu-id="04966-206">Follow these links toolearn more about managing Azure IoT Hub:</span></span>

* <span data-ttu-id="04966-207">[Gestire in blocco i dispositivi IoT][lnk-bulk]</span><span class="sxs-lookup"><span data-stu-id="04966-207">[Bulk manage IoT devices][lnk-bulk]</span></span>
* <span data-ttu-id="04966-208">[Metriche di Hub IoT][lnk-metrics]</span><span class="sxs-lookup"><span data-stu-id="04966-208">[IoT Hub metrics][lnk-metrics]</span></span>
* <span data-ttu-id="04966-209">[Monitoraggio delle operazioni][lnk-monitor]</span><span class="sxs-lookup"><span data-stu-id="04966-209">[Operations monitoring][lnk-monitor]</span></span>

<span data-ttu-id="04966-210">toofurther esplorare le funzionalità di hello di IoT Hub, vedere:</span><span class="sxs-lookup"><span data-stu-id="04966-210">toofurther explore hello capabilities of IoT Hub, see:</span></span>

* <span data-ttu-id="04966-211">[Guida per gli sviluppatori dell'hub IoT][lnk-devguide]</span><span class="sxs-lookup"><span data-stu-id="04966-211">[IoT Hub developer guide][lnk-devguide]</span></span>
* <span data-ttu-id="04966-212">[Simulazione di un dispositivo con IoT Edge][lnk-iotedge]</span><span class="sxs-lookup"><span data-stu-id="04966-212">[Simulating a device with IoT Edge][lnk-iotedge]</span></span>
* <span data-ttu-id="04966-213">[Soluzione IoT da hello la messa a terra sicura][lnk-securing]</span><span class="sxs-lookup"><span data-stu-id="04966-213">[Secure your IoT solution from hello ground up][lnk-securing]</span></span>

[4]: ./media/iot-hub-create-through-portal/create-iothub.png
[5]: ./media/iot-hub-create-through-portal/location1.png
[8]: ./media/iot-hub-create-through-portal/portal-settings.png
[10]: ./media/iot-hub-create-through-portal/shared-access-policies.png
[11]: ./media/iot-hub-create-through-portal/messaging-settings.png
[12]: ./media/iot-hub-create-through-portal/pricing-error.png
[13]: ./media/iot-hub-create-through-portal/endpoint-creation.png
[14]: ./media/iot-hub-create-through-portal/routes-list.png
[15]: ./media/iot-hub-create-through-portal/route-edit.png

[lnk-bulk]: iot-hub-bulk-identity-mgmt.md
[lnk-metrics]: iot-hub-metrics.md
[lnk-monitor]: iot-hub-operations-monitoring.md

[lnk-devguide]: iot-hub-devguide.md
[lnk-iotedge]: iot-hub-linux-iot-edge-simulated-device.md
[lnk-securing]: iot-hub-security-ground-up.md
[lnk-devguide-endpoints]: iot-hub-devguide-endpoints.md

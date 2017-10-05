---
title: Usare il portale di Azure per creare un hub IoT | Microsoft Docs
description: Come creare, gestire ed eliminare hub IoT di Azure con il portale di Azure. Include informazioni su piani tariffari, ridimensionamento, sicurezza e configurazione della messaggistica.
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
ms.openlocfilehash: bca7eea5f44bbed3b784b56edaac235161b43e5e
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/03/2017
---
# <a name="create-an-iot-hub-using-the-azure-portal"></a><span data-ttu-id="a070c-104">Creare un hub IoT usando il portale di Azure</span><span class="sxs-lookup"><span data-stu-id="a070c-104">Create an IoT hub using the Azure portal</span></span>

[!INCLUDE [iot-hub-resource-manager-selector](../../includes/iot-hub-resource-manager-selector.md)]

<span data-ttu-id="a070c-105">L'articolo illustra:</span><span class="sxs-lookup"><span data-stu-id="a070c-105">This article describes:</span></span>

* <span data-ttu-id="a070c-106">Come trovare il servizio hub IoT nel portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="a070c-106">How to find the IoT Hub service in the Azure portal.</span></span>
* <span data-ttu-id="a070c-107">Come creare e gestire hub IoT.</span><span class="sxs-lookup"><span data-stu-id="a070c-107">How to create and manage IoT hubs.</span></span>

## <a name="where-to-find-the-iot-hub-service"></a><span data-ttu-id="a070c-108">Dove trovare il servizio hub IoT</span><span class="sxs-lookup"><span data-stu-id="a070c-108">Where to find the IoT Hub service</span></span>

<span data-ttu-id="a070c-109">È possibile trovare il servizio hub IoT nelle posizioni seguenti nel portale:</span><span class="sxs-lookup"><span data-stu-id="a070c-109">You can find the IoT Hub service in the following locations in the portal:</span></span>

* <span data-ttu-id="a070c-110">Scegliere **+ Nuovo** e quindi scegliere **Internet delle cose**.</span><span class="sxs-lookup"><span data-stu-id="a070c-110">Choose **+ New**, then choose **Internet of Things**.</span></span>
* <span data-ttu-id="a070c-111">Nel marketplace scegliere **Internet delle cose**.</span><span class="sxs-lookup"><span data-stu-id="a070c-111">In the Marketplace, choose **Internet of Things**.</span></span>

## <a name="create-an-iot-hub"></a><span data-ttu-id="a070c-112">Creare un hub IoT</span><span class="sxs-lookup"><span data-stu-id="a070c-112">Create an IoT hub</span></span>

<span data-ttu-id="a070c-113">È possibile creare un hub IoT usando i metodi seguenti:</span><span class="sxs-lookup"><span data-stu-id="a070c-113">You can create an IoT hub using the following methods:</span></span>

* <span data-ttu-id="a070c-114">L'opzione **+ Nuovo** apre il pannello illustrato nello screenshot seguente.</span><span class="sxs-lookup"><span data-stu-id="a070c-114">The **+ New** option opens the blade shown in the following screen shot.</span></span> <span data-ttu-id="a070c-115">I passaggi per la creazione di un hub IoT tramite questo metodo e tramite il Marketplace sono identici.</span><span class="sxs-lookup"><span data-stu-id="a070c-115">The steps for creating the IoT hub through this method and through the marketplace are identical.</span></span>
* <span data-ttu-id="a070c-116">Nel marketplace scegliere **Crea** per aprire il pannello visualizzato nello screenshot seguente.</span><span class="sxs-lookup"><span data-stu-id="a070c-116">In the Marketplace, choose **Create** to open the blade shown in the following screen shot.</span></span>

<span data-ttu-id="a070c-117">Le sezioni seguenti descrivono i diversi passaggi per creare un hub IoT:</span><span class="sxs-lookup"><span data-stu-id="a070c-117">The following sections describe the several steps to create an IoT hub:</span></span>

### <a name="choose-the-name-of-the-iot-hub"></a><span data-ttu-id="a070c-118">Scegliere il nome dell'hub IoT</span><span class="sxs-lookup"><span data-stu-id="a070c-118">Choose the name of the IoT hub</span></span>

<span data-ttu-id="a070c-119">Per creare un hub IoT, è necessario assegnare un nome all'hub IoT.</span><span class="sxs-lookup"><span data-stu-id="a070c-119">To create an IoT hub, you must name the IoT hub.</span></span> <span data-ttu-id="a070c-120">Questo nome deve essere univoco in tutti gli hub IoT.</span><span class="sxs-lookup"><span data-stu-id="a070c-120">This name must be unique across all IoT hubs.</span></span>

[!INCLUDE [iot-hub-pii-note-naming-hub](../../includes/iot-hub-pii-note-naming-hub.md)]

### <a name="choose-the-pricing-tier"></a><span data-ttu-id="a070c-121">Scegliere il piano tariffario</span><span class="sxs-lookup"><span data-stu-id="a070c-121">Choose the pricing tier</span></span>

<span data-ttu-id="a070c-122">È possibile scegliere fra quattro piani: **Gratuito**, **Standard 1**, **Standard 2** e **Standard S3**.</span><span class="sxs-lookup"><span data-stu-id="a070c-122">You can choose from four tiers: **Free**, **Standard 1** and **Standard 2**, and **Standard S3**.</span></span> <span data-ttu-id="a070c-123">Il piano gratuito consente la connessione di solo 500 dispositivi all'hub IoT e di un massimo di 8.000 messaggi al giorno.</span><span class="sxs-lookup"><span data-stu-id="a070c-123">The free tier allows only 500 devices to be connected to the IoT hub and up to 8,000 messages per day.</span></span>

<span data-ttu-id="a070c-124">**Standard S1**: usare l'edizione S1 per le soluzioni IoT con un numero elevato di dispositivi, ognuno dei quali genera quantità limitate di dati.</span><span class="sxs-lookup"><span data-stu-id="a070c-124">**Standard S1**: Use the S1 edition for IoT solutions with a large number of devices that each generate small amounts of data.</span></span> <span data-ttu-id="a070c-125">Ogni unità dell'edizione S1 consente fino a 400.000 messaggi al giorno tra tutti i dispositivi.</span><span class="sxs-lookup"><span data-stu-id="a070c-125">Each unit of the S1 edition allows up to 400,000 messages per day across all connected devices.</span></span>

<span data-ttu-id="a070c-126">**Standard S2**: usare l'edizione S2 per le soluzioni IoT in cui i dispositivi generano grandi quantità di dati.</span><span class="sxs-lookup"><span data-stu-id="a070c-126">**Standard S2**: Use the S2 edition for IoT solutions in which devices generate large amounts of data.</span></span> <span data-ttu-id="a070c-127">Ogni unità dell'edizione S2 consente fino a 6 milioni di messaggi al giorno tra tutti i dispositivi connessi.</span><span class="sxs-lookup"><span data-stu-id="a070c-127">Each unit of the S2 edition allows up to 6 million messages per day between all connected devices.</span></span>

<span data-ttu-id="a070c-128">**Standard S3**: usare l'edizione S3 per soluzioni IoT che generano grandi quantità di dati.</span><span class="sxs-lookup"><span data-stu-id="a070c-128">**Standard S3**: Use the S3 edition for IoT solutions that generate large amounts of data.</span></span> <span data-ttu-id="a070c-129">Ogni unità dell'edizione S3 consente fino a 300 milioni di messaggi al giorno tra tutti i dispositivi connessi.</span><span class="sxs-lookup"><span data-stu-id="a070c-129">Each unit of the S3 edition allows up to 300 million messages per day between all connected devices.</span></span>

![][4]

> [!NOTE]
> <span data-ttu-id="a070c-130">L'hub IoT consente solo un hub gratuito per sottoscrizione di Azure.</span><span class="sxs-lookup"><span data-stu-id="a070c-130">IoT Hub only allows one free hub per Azure subscription.</span></span>

### <a name="iot-hub-units"></a><span data-ttu-id="a070c-131">Unità hub IoT</span><span class="sxs-lookup"><span data-stu-id="a070c-131">IoT hub units</span></span>

<span data-ttu-id="a070c-132">Il numero di messaggi consentiti per unità al giorno dipende dal piano tariffario dell'hub.</span><span class="sxs-lookup"><span data-stu-id="a070c-132">The number of messages allowed per unit per day depends on your hub's pricing tier.</span></span> <span data-ttu-id="a070c-133">Ad esempio, se si desidera che l'hub IoT supporti 700.000 messaggi in entrata, selezionare due unità del piano S1.</span><span class="sxs-lookup"><span data-stu-id="a070c-133">For example, if you want the IoT hub to support ingress of 700,000 messages, you choose two S1 tier units.</span></span>

### <a name="device-to-cloud-partitions-and-resource-group"></a><span data-ttu-id="a070c-134">Partizioni da dispositivo a cloud e gruppo di risorse</span><span class="sxs-lookup"><span data-stu-id="a070c-134">Device to cloud partitions and resource group</span></span>

<span data-ttu-id="a070c-135">È possibile modificare il numero di partizioni per un hub IoT.</span><span class="sxs-lookup"><span data-stu-id="a070c-135">You can change the number of partitions for an IoT hub.</span></span> <span data-ttu-id="a070c-136">Il numero predefinito di partizioni è 4 ed è possibile scegliere un altro numero nell'elenco a discesa.</span><span class="sxs-lookup"><span data-stu-id="a070c-136">The default number of partitions is 4, you can choose a different number from the drop-down list.</span></span>

<span data-ttu-id="a070c-137">Non è necessario creare in modo esplicito un gruppo di risorse vuoto.</span><span class="sxs-lookup"><span data-stu-id="a070c-137">You do not need to explicitly create an empty resource group.</span></span> <span data-ttu-id="a070c-138">Quando si crea una risorsa, è possibile scegliere di creare un nuovo gruppo di risorse o usarne uno esistente.</span><span class="sxs-lookup"><span data-stu-id="a070c-138">When you create a resource, you can choose either to create a new, or use an existing resource group.</span></span>

![][5]

### <a name="choose-subscription"></a><span data-ttu-id="a070c-139">Scegliere la sottoscrizione</span><span class="sxs-lookup"><span data-stu-id="a070c-139">Choose subscription</span></span>

<span data-ttu-id="a070c-140">L'hub IoT di Azure mostra automaticamente l'elenco di sottoscrizioni di Azure alle quali è collegato l'account utente.</span><span class="sxs-lookup"><span data-stu-id="a070c-140">Azure IoT Hub automatically lists the Azure subscriptions the user account is linked to.</span></span> <span data-ttu-id="a070c-141">È possibile scegliere la sottoscrizione di Azure a cui associare l'hub IoT.</span><span class="sxs-lookup"><span data-stu-id="a070c-141">You can choose the Azure subscription to associate the IoT hub to.</span></span>

### <a name="choose-the-location"></a><span data-ttu-id="a070c-142">Scegliere la località</span><span class="sxs-lookup"><span data-stu-id="a070c-142">Choose the location</span></span>

<span data-ttu-id="a070c-143">L'opzione relativa alla posizione offre un elenco delle aree in cui è disponibile l'hub IoT.</span><span class="sxs-lookup"><span data-stu-id="a070c-143">The location option provides a list of the regions where IoT Hub is available.</span></span>

### <a name="create-the-iot-hub"></a><span data-ttu-id="a070c-144">Creare l'hub IoT</span><span class="sxs-lookup"><span data-stu-id="a070c-144">Create the IoT hub</span></span>

<span data-ttu-id="a070c-145">Dopo aver completato tutti i passaggi precedenti, è possibile creare l'hub IoT.</span><span class="sxs-lookup"><span data-stu-id="a070c-145">When all previous steps are complete, you can create the IoT hub.</span></span> <span data-ttu-id="a070c-146">Fare clic su **Crea** per avviare il processo di back-end per creare e distribuire l'hub IoT con le opzioni scelte.</span><span class="sxs-lookup"><span data-stu-id="a070c-146">Click **Create** to start the back-end process to create and deploy the IoT hub with the options you chose.</span></span>

<span data-ttu-id="a070c-147">Possono essere necessari alcuni minuti per creare l'hub IoT, perché l'esecuzione della distribuzione del back-end nei server delle località appropriate richiede tempo.</span><span class="sxs-lookup"><span data-stu-id="a070c-147">It can take a few minutes to create the IoT hub as it takes time for the back-end deployment to run on the appropriate location servers.</span></span>

## <a name="change-the-settings-of-the-iot-hub"></a><span data-ttu-id="a070c-148">Modificare le impostazioni dell'hub IoT</span><span class="sxs-lookup"><span data-stu-id="a070c-148">Change the settings of the IoT hub</span></span>

<span data-ttu-id="a070c-149">È possibile modificare le impostazioni di un hub IoT esistente dopo averlo creato dal pannello Hub IoT.</span><span class="sxs-lookup"><span data-stu-id="a070c-149">You can change the settings of an existing IoT hub after it is created from the IoT Hub blade.</span></span>

![][8]

<span data-ttu-id="a070c-150">**Criteri di accesso condiviso**: questi criteri definiscono le autorizzazioni per la connessione di dispositivi e servizi all'hub IoT.</span><span class="sxs-lookup"><span data-stu-id="a070c-150">**Shared access policies**: These policies define the permissions for devices and services to connect to IoT Hub.</span></span> <span data-ttu-id="a070c-151">È possibile accedere a questi criteri facendo clic su **Criteri di accesso condiviso** in **Generale**.</span><span class="sxs-lookup"><span data-stu-id="a070c-151">You can access these policies by clicking **Shared access policies** under **General**.</span></span> <span data-ttu-id="a070c-152">In questo pannello è possibile modificare i criteri esistenti o aggiungerne di nuovi.</span><span class="sxs-lookup"><span data-stu-id="a070c-152">In this blade, you can either modify existing policies or add a new policy.</span></span>

### <a name="create-a-policy"></a><span data-ttu-id="a070c-153">Creare un criterio</span><span class="sxs-lookup"><span data-stu-id="a070c-153">Create a policy</span></span>

* <span data-ttu-id="a070c-154">Fare clic su **Aggiungi** per aprire un pannello.</span><span class="sxs-lookup"><span data-stu-id="a070c-154">Click **Add** to open a blade.</span></span> <span data-ttu-id="a070c-155">Qui è possibile immettere il nome dei nuovi criteri e le autorizzazioni da associare a questi criteri, come illustrato nella figura seguente:</span><span class="sxs-lookup"><span data-stu-id="a070c-155">Here you can enter the new policy name and the permissions that you want to associate with this policy, as shown in the following figure:</span></span>

    <span data-ttu-id="a070c-156">Sono disponibili numerose autorizzazioni che possono essere associate a questi criteri condivisi.</span><span class="sxs-lookup"><span data-stu-id="a070c-156">There are several permissions that can be associated with these shared policies.</span></span> <span data-ttu-id="a070c-157">I criteri **Lettura registro** e **Scrittura registro** consentono di concedere diritti di accesso in lettura e scrittura per il registro delle identità.</span><span class="sxs-lookup"><span data-stu-id="a070c-157">The **Registry read** and **Registry write** policies grant read and write access rights to the identity registry.</span></span> <span data-ttu-id="a070c-158">La scelta dell'opzione di scrittura include automaticamente l'opzione di lettura.</span><span class="sxs-lookup"><span data-stu-id="a070c-158">Choosing the write option automatically chooses the read option.</span></span>

    <span data-ttu-id="a070c-159">I criteri **Connessione servizio** concedono le autorizzazioni per accedere agli endpoint del servizio, ad esempio per la **ricezione di messaggi da dispositivo a cloud**.</span><span class="sxs-lookup"><span data-stu-id="a070c-159">The **Service connect** policy grants permission to access service endpoints such as **Receive device-to-cloud**.</span></span> <span data-ttu-id="a070c-160">I criteri **Connessione dispositivo** concedono le autorizzazioni per l'invio e la ricezione di messaggi tramite gli endpoint sul lato dispositivo dell'hub IoT.</span><span class="sxs-lookup"><span data-stu-id="a070c-160">The **Device connect** policy grants permissions for sending and receiving messages using the IoT Hub device-side endpoints.</span></span>

* <span data-ttu-id="a070c-161">Fare clic su **Crea** per aggiungere i criteri appena creati all'elenco esistente.</span><span class="sxs-lookup"><span data-stu-id="a070c-161">Click **Create** to add this newly created policy to the existing list.</span></span>

![][10]

## <a name="endpoints"></a><span data-ttu-id="a070c-162">Endpoint</span><span class="sxs-lookup"><span data-stu-id="a070c-162">Endpoints</span></span>

<span data-ttu-id="a070c-163">Fare clic su **Endpoint** per visualizzare un elenco di endpoint per l'hub IoT che si sta modificando.</span><span class="sxs-lookup"><span data-stu-id="a070c-163">Click **Endpoints** to display a list of endpoints for the IoT hub that you are modifying.</span></span> <span data-ttu-id="a070c-164">Esistono due principali tipi di endpoint: endpoint predefinti nell'hub IoT ed endpoint aggiunti all'hub IoT in seguito alla sua creazione.</span><span class="sxs-lookup"><span data-stu-id="a070c-164">There are two types of endpoints: endpoints that are built into the IoT hub, and endpoints that you add to the IoT hub after its creation.</span></span>

![][11]

### <a name="built-in-endpoints"></a><span data-ttu-id="a070c-165">Endpoint predefiniti</span><span class="sxs-lookup"><span data-stu-id="a070c-165">Built-in endpoints</span></span>

<span data-ttu-id="a070c-166">Esistono due tipi di endpoint predefiniti: **Cloud to device feedback** (Commenti da cloud a dispositivi) ed **Eventi**.</span><span class="sxs-lookup"><span data-stu-id="a070c-166">There are two built-in endpoints: **Cloud to device feedback** and **Events**.</span></span>

* <span data-ttu-id="a070c-167">Impostazioni **Cloud to device feedback** (Commenti da cloud a dispositiv): questa impostazione include due impostazioni secondarie **Cloud to Device TTL** (Durata (TTL) da cloud a dispositivo) e **Tempo di conservazione** (in ore) per i messaggi.</span><span class="sxs-lookup"><span data-stu-id="a070c-167">**Cloud to device feedback** settings: This setting has two subsettings: **Cloud to Device TTL** (time-to-live) and **Retention time** (in hours) for the messages.</span></span> <span data-ttu-id="a070c-168">Quando si crea per la prima volta un hub IoT, entrambe queste impostazioni hanno il valore predefinito di un'ora.</span><span class="sxs-lookup"><span data-stu-id="a070c-168">When your first create an IoT hub, both these settings have the default value of one hour.</span></span> <span data-ttu-id="a070c-169">Per modificare queste impostazioni usare i dispositivi di scorrimento o digitare i valori.</span><span class="sxs-lookup"><span data-stu-id="a070c-169">To adjust these settings, use the sliders or type the values.</span></span>
* <span data-ttu-id="a070c-170">Impostazioni **Eventi**: questa impostazione presenta diverse impostazioni secondarie, alcune delle quali sono di sola lettura.</span><span class="sxs-lookup"><span data-stu-id="a070c-170">**Events** settings: This setting has several subsettings, some of which are read-only.</span></span> <span data-ttu-id="a070c-171">L'elenco seguente descrive le singole impostazioni:</span><span class="sxs-lookup"><span data-stu-id="a070c-171">The following list describes these settings:</span></span>

  * <span data-ttu-id="a070c-172">**Partizioni**: viene impostato un valore predefinito quando viene creato l'hub IoT.</span><span class="sxs-lookup"><span data-stu-id="a070c-172">**Partitions**: A default value is set when the IoT hub is created.</span></span> <span data-ttu-id="a070c-173">Grazie a questa impostazione è possibile modificare il numero di partizioni.</span><span class="sxs-lookup"><span data-stu-id="a070c-173">You can change the number of partitions through this setting.</span></span>

  * <span data-ttu-id="a070c-174">**Event Hub-compatible name and endpoint** (Nomi ed endpoint compatibili con Hub eventi): quando viene creato l'hub IoT, viene creato internamente un Hub eventi a cui potrebbe essere necessario accedere in determinate circostanze.</span><span class="sxs-lookup"><span data-stu-id="a070c-174">**Event Hub-compatible name and endpoint**: When the IoT hub is created, an Event Hub is created internally that you may need access to under certain circumstances.</span></span> <span data-ttu-id="a070c-175">Non è possibile personalizzare i valori del nome e dell'endpoint compatibile con l'hub eventi, ma è possibile copiarli facendo clic su **Copia**.</span><span class="sxs-lookup"><span data-stu-id="a070c-175">You cannot customize the Event Hub-compatible name and endpoint values but you can copy them by clicking **Copy**.</span></span>

  * <span data-ttu-id="a070c-176">**Tempo di conservazione**: per impostazione predefinita è impostato su un giorno ma è possibile modificarlo tramite l'elenco a discesa.</span><span class="sxs-lookup"><span data-stu-id="a070c-176">**Retention Time**: Set to one day by default but you can change it using the drop-down list.</span></span> <span data-ttu-id="a070c-177">Questo valore è espresso in giorni per l'impostazione da dispositivo a cloud.</span><span class="sxs-lookup"><span data-stu-id="a070c-177">This value is in days for the device-to-cloud setting.</span></span>

  * <span data-ttu-id="a070c-178">**Gruppi di consumer**: i gruppi di consumer consentono a più lettori di leggere i messaggi in modo indipendente dall'hub IoT.</span><span class="sxs-lookup"><span data-stu-id="a070c-178">**Consumer Groups**: Consumer groups enable multiple readers to read messages independently from the IoT hub.</span></span> <span data-ttu-id="a070c-179">Ogni hub IoT viene creato con un gruppo di consumer predefinito.</span><span class="sxs-lookup"><span data-stu-id="a070c-179">Every IoT hub is created with a default consumer group.</span></span> <span data-ttu-id="a070c-180">Tuttavia, con questa impostazione è possibile aggiungere o eliminare gruppi di consumer negli hub IoT.</span><span class="sxs-lookup"><span data-stu-id="a070c-180">However, you can add or delete consumer groups to your IoT hubs using this setting.</span></span>

  > [!NOTE]
  > <span data-ttu-id="a070c-181">Il gruppo di consumer predefinito non può essere modificato o eliminato.</span><span class="sxs-lookup"><span data-stu-id="a070c-181">The default consumer group cannot be edited or deleted.</span></span>

### <a name="custom-endpoints"></a><span data-ttu-id="a070c-182">Endpoint personalizzati</span><span class="sxs-lookup"><span data-stu-id="a070c-182">Custom endpoints</span></span>

<span data-ttu-id="a070c-183">È possibile aggiungere endpoint personalizzati all'hub IoT tramite il portale.</span><span class="sxs-lookup"><span data-stu-id="a070c-183">You can add custom endpoints on your IoT hub using the portal.</span></span> <span data-ttu-id="a070c-184">Nel pannello **Endpoint**, fare clic su **Aggiungi** nella parte superiore del pannello per aprire il pannello **Aggiungi endpoint**.</span><span class="sxs-lookup"><span data-stu-id="a070c-184">From the **Endpoints** blade, click **Add** at the top to open the **Add endpoint** blade.</span></span> <span data-ttu-id="a070c-185">Immettere le informazioni necessarie, quindi fare clic su **OK**.</span><span class="sxs-lookup"><span data-stu-id="a070c-185">Enter the required information, then click **OK**.</span></span> <span data-ttu-id="a070c-186">L'endpoint personalizzato viene ora elencato nel pannello principale **Endpoint**.</span><span class="sxs-lookup"><span data-stu-id="a070c-186">Your custom endpoint is now listed in the main **Endpoints** blade.</span></span>

![][13]

<span data-ttu-id="a070c-187">Altre informazioni sugli endpoint personalizzati sono disponibili in [Reference - IoT hub endpoints][lnk-devguide-endpoints] (Riferimenti: endpoint di hub IoT).</span><span class="sxs-lookup"><span data-stu-id="a070c-187">You can read more about custom endpoints in [Reference - IoT hub endpoints][lnk-devguide-endpoints].</span></span>

## <a name="routes"></a><span data-ttu-id="a070c-188">Route</span><span class="sxs-lookup"><span data-stu-id="a070c-188">Routes</span></span>

<span data-ttu-id="a070c-189">Fare clic su **Route** per gestire la modalità di invio dei messaggi da dispositivo a cloud dell'hub IoT.</span><span class="sxs-lookup"><span data-stu-id="a070c-189">Click **Routes** to manage how IoT Hub dispatches your device-to-cloud messages.</span></span>

![][14]

<span data-ttu-id="a070c-190">È possibile aggiungere i route all'hub IoT facendo clic su **Aggiungi** nella parte superiore del pannello **Route*** inserendo le informazioni necessarie e facendo clic su **OK**.</span><span class="sxs-lookup"><span data-stu-id="a070c-190">You can add routes to your IoT hub by clicking **Add** at the top of the **Routes*** blade, entering the required information, and clicking **OK**.</span></span> <span data-ttu-id="a070c-191">Il route viene quindi elencato nel pannello principale **Route**.</span><span class="sxs-lookup"><span data-stu-id="a070c-191">Your route is then listed in the main **Routes** blade.</span></span> <span data-ttu-id="a070c-192">È possibile modificare un route selezionandolo nell'elenco di route.</span><span class="sxs-lookup"><span data-stu-id="a070c-192">You can edit a route by clicking it in the list of routes.</span></span> <span data-ttu-id="a070c-193">Per abilitare un route, selezionarlo nell'elenco di route e impostare l'interruttore **Enabled** su **Off**.</span><span class="sxs-lookup"><span data-stu-id="a070c-193">To enable a route, click it in the list of routes and set the **Enabled** toggle to **Off**.</span></span> <span data-ttu-id="a070c-194">Per salvare le modifiche, fare clic su **OK** nella parte inferiore del pannello.</span><span class="sxs-lookup"><span data-stu-id="a070c-194">To save the change, click **OK** at the bottom of the blade.</span></span>

![][15]

## <a name="pricing-and-scale"></a><span data-ttu-id="a070c-195">Prezzi e scalabilità</span><span class="sxs-lookup"><span data-stu-id="a070c-195">Pricing and scale</span></span>

<span data-ttu-id="a070c-196">I prezzi di un hub IoT esistente possono essere modificati tramite le impostazioni disponibili in **Prezzi** con le eccezioni seguenti:</span><span class="sxs-lookup"><span data-stu-id="a070c-196">The pricing of an existing IoT hub can be changed through the **Pricing** settings, with the following exceptions:</span></span>

* <span data-ttu-id="a070c-197">Nell'implementazione corrente un hub IoT con uno SKU gratuito non può cambiare i piani con quelli di uno degli SKU a pagamento o viceversa.</span><span class="sxs-lookup"><span data-stu-id="a070c-197">In the current implementation, an IoT hub with a free SKU cannot change tiers to one of the paid SKUs, or vice versa.</span></span>
* <span data-ttu-id="a070c-198">Nella sottoscrizione Azure può essere presente un solo livello gratuito per l'hub IoT.</span><span class="sxs-lookup"><span data-stu-id="a070c-198">There can only be one free tier IoT hub in the Azure subscription.</span></span>

![][12]

<span data-ttu-id="a070c-199">È possibile passare da un livello più elevato a uno inferiore solo quando il numero di messaggi inviati per un dato giorno supera la quota per il livello inferiore.</span><span class="sxs-lookup"><span data-stu-id="a070c-199">You can move from a higher to lower tier only when the number of messages sent that day do exceed the quota for the lower tier.</span></span> <span data-ttu-id="a070c-200">Ad esempio, se il numero di messaggi al giorno supera 400.000, il livello per l'hub IoT può essere cambiato.</span><span class="sxs-lookup"><span data-stu-id="a070c-200">For example, if the number of messages per day exceeds 400,000, then the tier for the IoT hub can be changed.</span></span> <span data-ttu-id="a070c-201">Tuttavia, se si modifica il piano S1, l'hub IoT è limitato per il giorno in questione.</span><span class="sxs-lookup"><span data-stu-id="a070c-201">However, if you change to the S1 tier then the IoT hub is throttled for that day.</span></span>

## <a name="delete-the-iot-hub"></a><span data-ttu-id="a070c-202">Eliminare l'hub IoT</span><span class="sxs-lookup"><span data-stu-id="a070c-202">Delete the IoT hub</span></span>

<span data-ttu-id="a070c-203">È possibile passare all'hub IoT che si vuole eliminare facendo clic su **Sfoglia** e quindi scegliendo l'hub appropriato da eliminare.</span><span class="sxs-lookup"><span data-stu-id="a070c-203">You can browse to the IoT hub you want to delete by clicking **Browse**, and then choosing the appropriate hub to delete.</span></span> <span data-ttu-id="a070c-204">Fare clic sul pulsante **Elimina** sotto il nome dell'hub IoT per eliminarlo.</span><span class="sxs-lookup"><span data-stu-id="a070c-204">To delete the IoT hub, click the **Delete** button below the IoT hub name.</span></span>

## <a name="next-steps"></a><span data-ttu-id="a070c-205">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="a070c-205">Next steps</span></span>

<span data-ttu-id="a070c-206">Per ulteriori informazioni sulla gestione dell'hub IoT di Azure, consultare questi collegamenti:</span><span class="sxs-lookup"><span data-stu-id="a070c-206">Follow these links to learn more about managing Azure IoT Hub:</span></span>

* <span data-ttu-id="a070c-207">[Gestire in blocco i dispositivi IoT][lnk-bulk]</span><span class="sxs-lookup"><span data-stu-id="a070c-207">[Bulk manage IoT devices][lnk-bulk]</span></span>
* <span data-ttu-id="a070c-208">[Metriche di Hub IoT][lnk-metrics]</span><span class="sxs-lookup"><span data-stu-id="a070c-208">[IoT Hub metrics][lnk-metrics]</span></span>
* <span data-ttu-id="a070c-209">[Monitoraggio delle operazioni][lnk-monitor]</span><span class="sxs-lookup"><span data-stu-id="a070c-209">[Operations monitoring][lnk-monitor]</span></span>

<span data-ttu-id="a070c-210">Per altre informazioni sulle funzionalità dell'hub IoT, vedere:</span><span class="sxs-lookup"><span data-stu-id="a070c-210">To further explore the capabilities of IoT Hub, see:</span></span>

* <span data-ttu-id="a070c-211">[Guida per gli sviluppatori dell'hub IoT][lnk-devguide]</span><span class="sxs-lookup"><span data-stu-id="a070c-211">[IoT Hub developer guide][lnk-devguide]</span></span>
* <span data-ttu-id="a070c-212">[Simulazione di un dispositivo con IoT Edge][lnk-iotedge]</span><span class="sxs-lookup"><span data-stu-id="a070c-212">[Simulating a device with IoT Edge][lnk-iotedge]</span></span>
* <span data-ttu-id="a070c-213">[Proteggere la soluzione IoT sin dall'inizio][lnk-securing]</span><span class="sxs-lookup"><span data-stu-id="a070c-213">[Secure your IoT solution from the ground up][lnk-securing]</span></span>

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

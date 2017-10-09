---
title: sicurezza di Azure IoT Hub aaaUnderstand | Documenti Microsoft
description: "Le istruzioni per sviluppatori - modalità toocontrol accesso tooIoT Hub per le app di dispositivo e back-end. Include informazioni sui token di sicurezza e sul supporto per i certificati x.509."
services: iot-hub
documentationcenter: .net
author: dominicbetts
manager: timlt
editor: 
ms.assetid: 45631e70-865b-4e06-bb1d-aae1175a52ba
ms.service: iot-hub
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/08/2017
ms.author: dobett
ms.openlocfilehash: 717726328a6bb5c5c334a123d0abfed711b2c3b1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="control-access-tooiot-hub"></a><span data-ttu-id="4d730-104">Controllo accesso tooIoT Hub</span><span class="sxs-lookup"><span data-stu-id="4d730-104">Control access tooIoT Hub</span></span>

<span data-ttu-id="4d730-105">Questo articolo descrive le opzioni di hello per proteggere l'hub IoT.</span><span class="sxs-lookup"><span data-stu-id="4d730-105">This article describes hello options for securing your IoT hub.</span></span> <span data-ttu-id="4d730-106">Usa IoT Hub *autorizzazioni* endpoint hub IoT di toogrant accesso tooeach.</span><span class="sxs-lookup"><span data-stu-id="4d730-106">IoT Hub uses *permissions* toogrant access tooeach IoT hub endpoint.</span></span> <span data-ttu-id="4d730-107">Le autorizzazioni di limitano l'hub IoT tooan accesso hello in base alle funzionalità.</span><span class="sxs-lookup"><span data-stu-id="4d730-107">Permissions limit hello access tooan IoT hub based on functionality.</span></span>

<span data-ttu-id="4d730-108">L'articolo illustra:</span><span class="sxs-lookup"><span data-stu-id="4d730-108">This article describes:</span></span>

* <span data-ttu-id="4d730-109">Hello diverse autorizzazioni che è possibile concedere tooa dispositivo o app back-end tooaccess l'hub IoT.</span><span class="sxs-lookup"><span data-stu-id="4d730-109">hello different permissions that you can grant tooa device or back-end app tooaccess your IoT hub.</span></span>
* <span data-ttu-id="4d730-110">Hello processo e hello i token di autenticazione usa tooverify autorizzazioni.</span><span class="sxs-lookup"><span data-stu-id="4d730-110">hello authentication process and hello tokens it uses tooverify permissions.</span></span>
* <span data-ttu-id="4d730-111">Come tooscope credenziali toospecific toolimit accedere alle risorse.</span><span class="sxs-lookup"><span data-stu-id="4d730-111">How tooscope credentials toolimit access toospecific resources.</span></span>
* <span data-ttu-id="4d730-112">Supporto dell'hub IoT per i certificati x.509.</span><span class="sxs-lookup"><span data-stu-id="4d730-112">IoT Hub support for X.509 certificates.</span></span>
* <span data-ttu-id="4d730-113">Meccanismo di autenticazione personalizzata del dispositivo che usa gli schemi di autenticazione o i registri di identità del dispositivo esistenti.</span><span class="sxs-lookup"><span data-stu-id="4d730-113">Custom device authentication mechanisms that use existing device identity registries or authentication schemes.</span></span>

### <a name="when-toouse"></a><span data-ttu-id="4d730-114">Quando toouse</span><span class="sxs-lookup"><span data-stu-id="4d730-114">When toouse</span></span>

<span data-ttu-id="4d730-115">È necessario disporre delle autorizzazioni appropriate tooaccess qualsiasi endpoint Hub IoT hello.</span><span class="sxs-lookup"><span data-stu-id="4d730-115">You must have appropriate permissions tooaccess any of hello IoT Hub endpoints.</span></span> <span data-ttu-id="4d730-116">Ad esempio, un dispositivo deve includere un token contenente le credenziali di sicurezza con ogni messaggio inviato tooIoT Hub.</span><span class="sxs-lookup"><span data-stu-id="4d730-116">For example, a device must include a token containing security credentials along with every message it sends tooIoT Hub.</span></span>

## <a name="access-control-and-permissions"></a><span data-ttu-id="4d730-117">Controllo dell'accesso e autorizzazioni</span><span class="sxs-lookup"><span data-stu-id="4d730-117">Access control and permissions</span></span>

<span data-ttu-id="4d730-118">È possibile concedere [autorizzazioni](#iot-hub-permissions) in hello seguenti modi:</span><span class="sxs-lookup"><span data-stu-id="4d730-118">You can grant [permissions](#iot-hub-permissions) in hello following ways:</span></span>

* <span data-ttu-id="4d730-119">**Criteri di accesso condivisi a livello di hub IoT**.</span><span class="sxs-lookup"><span data-stu-id="4d730-119">**IoT hub-level shared access policies**.</span></span> <span data-ttu-id="4d730-120">I criteri di accesso condiviso possono concedere qualsiasi combinazione di [autorizzazioni](#iot-hub-permissions).</span><span class="sxs-lookup"><span data-stu-id="4d730-120">Shared access policies can grant any combination of [permissions](#iot-hub-permissions).</span></span> <span data-ttu-id="4d730-121">È possibile definire i criteri in hello [portale di Azure][lnk-management-portal], o a livello di programmazione utilizzando hello [il provider di risorse IoT Hub API REST][lnk-resource-provider-apis].</span><span class="sxs-lookup"><span data-stu-id="4d730-121">You can define policies in hello [Azure portal][lnk-management-portal], or programmatically by using hello [IoT Hub resource provider REST APIs][lnk-resource-provider-apis].</span></span> <span data-ttu-id="4d730-122">Un hub IoT appena creato è hello criteri predefiniti seguenti:</span><span class="sxs-lookup"><span data-stu-id="4d730-122">A newly created IoT hub has hello following default policies:</span></span>

  * <span data-ttu-id="4d730-123">**iothubowner**: criteri con tutte le autorizzazioni.</span><span class="sxs-lookup"><span data-stu-id="4d730-123">**iothubowner**: Policy with all permissions.</span></span>
  * <span data-ttu-id="4d730-124">**service**: criteri con autorizzazione **ServiceConnect**.</span><span class="sxs-lookup"><span data-stu-id="4d730-124">**service**: Policy with **ServiceConnect** permission.</span></span>
  * <span data-ttu-id="4d730-125">**device**: criteri con autorizzazione **DeviceConnect**.</span><span class="sxs-lookup"><span data-stu-id="4d730-125">**device**: Policy with **DeviceConnect** permission.</span></span>
  * <span data-ttu-id="4d730-126">**registryRead**: criteri con autorizzazione **RegistryRead**.</span><span class="sxs-lookup"><span data-stu-id="4d730-126">**registryRead**: Policy with **RegistryRead** permission.</span></span>
  * <span data-ttu-id="4d730-127">**registryReadWrite**: criteri con autorizzazioni **RegistryRead** e RegistryWrite.</span><span class="sxs-lookup"><span data-stu-id="4d730-127">**registryReadWrite**: Policy with **RegistryRead** and RegistryWrite permissions.</span></span>
  * <span data-ttu-id="4d730-128">**Credenziali di sicurezza specifiche del dispositivo**.</span><span class="sxs-lookup"><span data-stu-id="4d730-128">**Per-device security credentials**.</span></span> <span data-ttu-id="4d730-129">Ogni hub IoT contiene un [registro delle identità][lnk-identity-registry].</span><span class="sxs-lookup"><span data-stu-id="4d730-129">Each IoT Hub contains an [identity registry][lnk-identity-registry].</span></span> <span data-ttu-id="4d730-130">Per ogni dispositivo in questo registro di sistema di identità, è possibile configurare le credenziali di sicurezza che concedono **DeviceConnect** autorizzazioni con ambito toohello gli endpoint di periferica corrispondente.</span><span class="sxs-lookup"><span data-stu-id="4d730-130">For each device in this identity registry, you can configure security credentials that grant **DeviceConnect** permissions scoped toohello corresponding device endpoints.</span></span>

<span data-ttu-id="4d730-131">Ad esempio, in una soluzione IoT tipica:</span><span class="sxs-lookup"><span data-stu-id="4d730-131">For example, in a typical IoT solution:</span></span>

* <span data-ttu-id="4d730-132">componente di Gestione periferiche Hello utilizza hello *registryReadWrite* criteri.</span><span class="sxs-lookup"><span data-stu-id="4d730-132">hello device management component uses hello *registryReadWrite* policy.</span></span>
* <span data-ttu-id="4d730-133">componente elaboratore eventi di Hello utilizza hello *servizio* criteri.</span><span class="sxs-lookup"><span data-stu-id="4d730-133">hello event processor component uses hello *service* policy.</span></span>
* <span data-ttu-id="4d730-134">componente della logica di business in fase di esecuzione dispositivo Hello utilizza hello *servizio* criteri.</span><span class="sxs-lookup"><span data-stu-id="4d730-134">hello run-time device business logic component uses hello *service* policy.</span></span>
* <span data-ttu-id="4d730-135">I singoli dispositivi di connetteranno utilizzando le credenziali archiviate nel Registro di sistema dell'hub IoT hello identità.</span><span class="sxs-lookup"><span data-stu-id="4d730-135">Individual devices connect using credentials stored in hello IoT hub's identity registry.</span></span>

> [!NOTE]
> <span data-ttu-id="4d730-136">Per informazioni dettagliate, vedere [Autorizzazioni](#iot-hub-permissions).</span><span class="sxs-lookup"><span data-stu-id="4d730-136">See [permissions](#iot-hub-permissions) for detailed information.</span></span>

## <a name="authentication"></a><span data-ttu-id="4d730-137">Autenticazione</span><span class="sxs-lookup"><span data-stu-id="4d730-137">Authentication</span></span>

<span data-ttu-id="4d730-138">IoT Hub Azure concede accesso tooendpoints verificando un token con i criteri di accesso condiviso hello e credenziali di sicurezza del Registro di sistema di identità.</span><span class="sxs-lookup"><span data-stu-id="4d730-138">Azure IoT Hub grants access tooendpoints by verifying a token against hello shared access policies and identity registry security credentials.</span></span>

<span data-ttu-id="4d730-139">Le credenziali di sicurezza, ad esempio le chiavi simmetriche, non vengono mai inviate in transito hello.</span><span class="sxs-lookup"><span data-stu-id="4d730-139">Security credentials, such as symmetric keys, are never sent over hello wire.</span></span>

> [!NOTE]
> <span data-ttu-id="4d730-140">Hello provider di risorse IoT Hub di Azure è protetto tramite una sottoscrizione di Azure, sono tutti i provider di hello [Azure Resource Manager][lnk-azure-resource-manager].</span><span class="sxs-lookup"><span data-stu-id="4d730-140">hello Azure IoT Hub resource provider is secured through your Azure subscription, as are all providers in hello [Azure Resource Manager][lnk-azure-resource-manager].</span></span>

<span data-ttu-id="4d730-141">Per ulteriori informazioni su come tooconstruct e l'utilizzo di token di sicurezza, vedere [i token di sicurezza di IoT Hub][lnk-sas-tokens].</span><span class="sxs-lookup"><span data-stu-id="4d730-141">For more information about how tooconstruct and use security tokens, see [IoT Hub security tokens][lnk-sas-tokens].</span></span>

### <a name="protocol-specifics"></a><span data-ttu-id="4d730-142">Specifiche del protocollo</span><span class="sxs-lookup"><span data-stu-id="4d730-142">Protocol specifics</span></span>

<span data-ttu-id="4d730-143">Ogni protocollo supportato, ad esempio MQTT, AMQP e HTTP, trasporta i token in modo diverso.</span><span class="sxs-lookup"><span data-stu-id="4d730-143">Each supported protocol, such as MQTT, AMQP, and HTTP, transports tokens in different ways.</span></span>

<span data-ttu-id="4d730-144">Quando si utilizza MQTT, pacchetto CONNETTI hello ha hello deviceId hello ClientId, {iothubhostname} / {deviceId} nel campo nome utente hello e un token di firma di accesso condiviso nel campo Password hello.</span><span class="sxs-lookup"><span data-stu-id="4d730-144">When using MQTT, hello CONNECT packet has hello deviceId as hello ClientId, {iothubhostname}/{deviceId} in hello Username field, and a SAS token in hello Password field.</span></span> <span data-ttu-id="4d730-145">{iothubhostname} deve essere hello CName completo dell'hub IoT hello (ad esempio, contoso.azure devices.net).</span><span class="sxs-lookup"><span data-stu-id="4d730-145">{iothubhostname} should be hello full CName of hello IoT hub (for example, contoso.azure-devices.net).</span></span>

<span data-ttu-id="4d730-146">Quando si usa [AMQP][lnk-amqp], l'hub IoT supporta [SASL PLAIN][lnk-sasl-plain] e la [sicurezza basata sulle attestazioni AMQP][lnk-cbs].</span><span class="sxs-lookup"><span data-stu-id="4d730-146">When using [AMQP][lnk-amqp], IoT Hub supports [SASL PLAIN][lnk-sasl-plain] and [AMQP Claims-Based-Security][lnk-cbs].</span></span>

<span data-ttu-id="4d730-147">Se si usa AMQP attestazioni in base a sicurezza, specifica hello standard come tootransmit questi token.</span><span class="sxs-lookup"><span data-stu-id="4d730-147">If you use AMQP claims-based-security, hello standard specifies how tootransmit these tokens.</span></span>

<span data-ttu-id="4d730-148">Per il normale SASL, hello **username** può essere:</span><span class="sxs-lookup"><span data-stu-id="4d730-148">For SASL PLAIN, hello **username** can be:</span></span>

* <span data-ttu-id="4d730-149">`{policyName}@sas.root.{iothubName}` nel caso di token a livello di hub IoT.</span><span class="sxs-lookup"><span data-stu-id="4d730-149">`{policyName}@sas.root.{iothubName}` if using IoT hub-level tokens.</span></span>
* <span data-ttu-id="4d730-150">`{deviceId}@sas.{iothubname}` ne caso di token con ambito relativo al dispositivo.</span><span class="sxs-lookup"><span data-stu-id="4d730-150">`{deviceId}@sas.{iothubname}` if using device-scoped tokens.</span></span>

<span data-ttu-id="4d730-151">In entrambi i casi, il campo di password hello contiene token hello, come descritto in [i token di sicurezza di IoT Hub][lnk-sas-tokens].</span><span class="sxs-lookup"><span data-stu-id="4d730-151">In both cases, hello password field contains hello token, as described in [IoT Hub security tokens][lnk-sas-tokens].</span></span>

<span data-ttu-id="4d730-152">HTTP implementa l'autenticazione con l'inclusione di un token valido in hello **autorizzazione** intestazione della richiesta.</span><span class="sxs-lookup"><span data-stu-id="4d730-152">HTTP implements authentication by including a valid token in hello **Authorization** request header.</span></span>

#### <a name="example"></a><span data-ttu-id="4d730-153">Esempio</span><span class="sxs-lookup"><span data-stu-id="4d730-153">Example</span></span>

<span data-ttu-id="4d730-154">Nome utente (per DeviceId viene fatta distinzione tra maiuscole e minuscole): `iothubname.azure-devices.net/DeviceId`</span><span class="sxs-lookup"><span data-stu-id="4d730-154">Username (DeviceId is case-sensitive): `iothubname.azure-devices.net/DeviceId`</span></span>

<span data-ttu-id="4d730-155">Password (token di firma di accesso condiviso generato con hello [Esplora dispositivo] [ lnk-device-explorer] strumento):`SharedAccessSignature sr=iothubname.azure-devices.net%2fdevices%2fDeviceId&sig=kPszxZZZZZZZZZZZZZZZZZAhLT%2bV7o%3d&se=1487709501`</span><span class="sxs-lookup"><span data-stu-id="4d730-155">Password (Generate SAS token with hello [device explorer][lnk-device-explorer] tool): `SharedAccessSignature sr=iothubname.azure-devices.net%2fdevices%2fDeviceId&sig=kPszxZZZZZZZZZZZZZZZZZAhLT%2bV7o%3d&se=1487709501`</span></span>

> [!NOTE]
> <span data-ttu-id="4d730-156">Hello [Azure IoT SDK] [ lnk-sdks] generare automaticamente i token durante la connessione del servizio toohello.</span><span class="sxs-lookup"><span data-stu-id="4d730-156">hello [Azure IoT SDKs][lnk-sdks] automatically generate tokens when connecting toohello service.</span></span> <span data-ttu-id="4d730-157">In alcuni casi, hello Azure IoT SDK non supportano tutti i protocolli di hello o tutti i metodi di autenticazione hello.</span><span class="sxs-lookup"><span data-stu-id="4d730-157">In some cases, hello Azure IoT SDKs do not support all hello protocols or all hello authentication methods.</span></span>

### <a name="special-considerations-for-sasl-plain"></a><span data-ttu-id="4d730-158">Considerazioni speciali su SASL PLAIN</span><span class="sxs-lookup"><span data-stu-id="4d730-158">Special considerations for SASL PLAIN</span></span>

<span data-ttu-id="4d730-159">Quando si utilizza SASL normale con AMQP, un client che si connette l'hub IoT tooan è possibile utilizzare un token singolo per ogni connessione TCP.</span><span class="sxs-lookup"><span data-stu-id="4d730-159">When using SASL PLAIN with AMQP, a client connecting tooan IoT hub can use a single token for each TCP connection.</span></span> <span data-ttu-id="4d730-160">Quando il token hello scade, hello connessione TCP disconnette dal servizio hello e viene attivata una riconnessione.</span><span class="sxs-lookup"><span data-stu-id="4d730-160">When hello token expires, hello TCP connection disconnects from hello service and triggers a reconnect.</span></span> <span data-ttu-id="4d730-161">Questo comportamento, mentre non problematico per un'applicazione back-end, danneggiare per un'applicazione di dispositivo per hello seguenti motivi:</span><span class="sxs-lookup"><span data-stu-id="4d730-161">This behavior, while not problematic for a back-end app, is damaging for a device app for hello following reasons:</span></span>

* <span data-ttu-id="4d730-162">I gateway si connettono in genere per conto di molti dispositivi.</span><span class="sxs-lookup"><span data-stu-id="4d730-162">Gateways usually connect on behalf of many devices.</span></span> <span data-ttu-id="4d730-163">Quando si utilizza SASL normale, hanno il toocreate una connessione TCP distinta per ogni dispositivo di connessione hub IoT tooan.</span><span class="sxs-lookup"><span data-stu-id="4d730-163">When using SASL PLAIN, they have toocreate a distinct TCP connection for each device connecting tooan IoT hub.</span></span> <span data-ttu-id="4d730-164">Questo scenario notevolmente aumenta al consumo di energia e le risorse di rete hello e aumenta la latenza di hello di ogni connessione del dispositivo.</span><span class="sxs-lookup"><span data-stu-id="4d730-164">This scenario considerably increases hello consumption of power and networking resources, and increases hello latency of each device connection.</span></span>
* <span data-ttu-id="4d730-165">Dispositivi con risorse limitate possono essere influenzati negativamente mediante l'utilizzo di hello aumentato di risorse tooreconnect dopo ogni scadenza del token.</span><span class="sxs-lookup"><span data-stu-id="4d730-165">Resource-constrained devices are adversely affected by hello increased use of resources tooreconnect after each token expiration.</span></span>

## <a name="scope-iot-hub-level-credentials"></a><span data-ttu-id="4d730-166">Definire l'ambito delle credenziali a livello di hub IoT</span><span class="sxs-lookup"><span data-stu-id="4d730-166">Scope IoT hub-level credentials</span></span>

<span data-ttu-id="4d730-167">È possibile definire l'ambito dei criteri di sicurezza a livello di hub IoT creando token con URI di risorsa con limitazioni.</span><span class="sxs-lookup"><span data-stu-id="4d730-167">You can scope IoT hub-level security policies by creating tokens with a restricted resource URI.</span></span> <span data-ttu-id="4d730-168">Ad esempio, i messaggi da dispositivo a cloud di hello endpoint toosend da un dispositivo è **/devices/ {deviceId} / messaggi/eventi**.</span><span class="sxs-lookup"><span data-stu-id="4d730-168">For example, hello endpoint toosend device-to-cloud messages from a device is **/devices/{deviceId}/messages/events**.</span></span> <span data-ttu-id="4d730-169">È inoltre possibile utilizzare un criterio di accesso condiviso a livello di hub IoT con **DeviceConnect** toosign autorizzazioni un token di cui resourceURI **/devices/ {deviceId}**.</span><span class="sxs-lookup"><span data-stu-id="4d730-169">You can also use an IoT hub-level shared access policy with **DeviceConnect** permissions toosign a token whose resourceURI is **/devices/{deviceId}**.</span></span> <span data-ttu-id="4d730-170">Questo approccio consente di creare un token solo messaggi toosend utilizzabile per conto di dispositivo **deviceId**.</span><span class="sxs-lookup"><span data-stu-id="4d730-170">This approach creates a token that is only usable toosend messages on behalf of device **deviceId**.</span></span>

<span data-ttu-id="4d730-171">Questo meccanismo è simile toohello [criteri dell'editore hub eventi][lnk-event-hubs-publisher-policy]ed è possibile tooimplement metodi di autenticazione personalizzati.</span><span class="sxs-lookup"><span data-stu-id="4d730-171">This mechanism is similar toohello [Event Hubs publisher policy][lnk-event-hubs-publisher-policy], and enables you tooimplement custom authentication methods.</span></span>

## <a name="security-tokens"></a><span data-ttu-id="4d730-172">Token di sicurezza</span><span class="sxs-lookup"><span data-stu-id="4d730-172">Security tokens</span></span>

<span data-ttu-id="4d730-173">IoT Hub utilizza la protezione del token tooauthenticate dispositivi e servizi tooavoid l'invio delle chiavi durante la trasmissione hello.</span><span class="sxs-lookup"><span data-stu-id="4d730-173">IoT Hub uses security tokens tooauthenticate devices and services tooavoid sending keys on hello wire.</span></span> <span data-ttu-id="4d730-174">Inoltre, i token di sicurezza hanno una validità limitata in termini di tempo e portata.</span><span class="sxs-lookup"><span data-stu-id="4d730-174">Additionally, security tokens are limited in time validity and scope.</span></span> <span data-ttu-id="4d730-175">Gli [Azure IoT SDK][lnk-sdks] generano automaticamente i token senza richiedere una configurazione speciale.</span><span class="sxs-lookup"><span data-stu-id="4d730-175">[Azure IoT SDKs][lnk-sdks] automatically generate tokens without requiring any special configuration.</span></span> <span data-ttu-id="4d730-176">Alcuni scenari richiedono toogenerate e utilizzare direttamente i token di sicurezza.</span><span class="sxs-lookup"><span data-stu-id="4d730-176">Some scenarios do require you toogenerate and use security tokens directly.</span></span> <span data-ttu-id="4d730-177">Tali scenari includono:</span><span class="sxs-lookup"><span data-stu-id="4d730-177">Such scenarios include:</span></span>

* <span data-ttu-id="4d730-178">utilizzo diretto di Hello superfici hello MQTT, AMQP o HTTP.</span><span class="sxs-lookup"><span data-stu-id="4d730-178">hello direct use of hello MQTT, AMQP, or HTTP surfaces.</span></span>
* <span data-ttu-id="4d730-179">Hello implementazione del modello di servizio token di hello, come illustrato in [l'autenticazione del dispositivo personalizzato][lnk-custom-auth].</span><span class="sxs-lookup"><span data-stu-id="4d730-179">hello implementation of hello token service pattern, as explained in [Custom device authentication][lnk-custom-auth].</span></span>

<span data-ttu-id="4d730-180">IoT Hub consente inoltre alle periferiche tooauthenticate con l'IoT Hub utilizzando [certificati x. 509][lnk-x509].</span><span class="sxs-lookup"><span data-stu-id="4d730-180">IoT Hub also allows devices tooauthenticate with IoT Hub using [X.509 certificates][lnk-x509].</span></span>

### <a name="security-token-structure"></a><span data-ttu-id="4d730-181">Formato del token di sicurezza</span><span class="sxs-lookup"><span data-stu-id="4d730-181">Security token structure</span></span>

<span data-ttu-id="4d730-182">Si utilizza protezione token toogrant accesso limitato al tempo toodevices e servizi toospecific funzionalità nell'IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="4d730-182">You use security tokens toogrant time-bounded access toodevices and services toospecific functionality in IoT Hub.</span></span> <span data-ttu-id="4d730-183">tooget autorizzazione tooconnect tooIoT Hub, dispositivi e servizi devono inviare i token di sicurezza firmati con un accesso condiviso o della chiave simmetrica.</span><span class="sxs-lookup"><span data-stu-id="4d730-183">tooget authorization tooconnect tooIoT Hub, devices and services must send security tokens signed with either a shared access or symmetric key.</span></span> <span data-ttu-id="4d730-184">Tali chiavi vengono archiviate con un'identità del dispositivo nel Registro di sistema di hello identità.</span><span class="sxs-lookup"><span data-stu-id="4d730-184">These keys are stored with a device identity in hello identity registry.</span></span>

<span data-ttu-id="4d730-185">Un token firmato con un'accesso condiviso chiave concede accesso tooall hello funzionalità associate le autorizzazioni di criteri di accesso condiviso hello.</span><span class="sxs-lookup"><span data-stu-id="4d730-185">A token signed with a shared access key grants access tooall hello functionality associated with hello shared access policy permissions.</span></span> <span data-ttu-id="4d730-186">Un token firmato con hello simmetrica chiave concede solo dell'identità del dispositivo **DeviceConnect** l'autorizzazione per hello è associata l'identità del dispositivo.</span><span class="sxs-lookup"><span data-stu-id="4d730-186">A token signed with a device identity's symmetric key only grants hello **DeviceConnect** permission for hello associated device identity.</span></span>

<span data-ttu-id="4d730-187">token di sicurezza Hello è hello seguente formato:</span><span class="sxs-lookup"><span data-stu-id="4d730-187">hello security token has hello following format:</span></span>

`SharedAccessSignature sig={signature-string}&se={expiry}&skn={policyName}&sr={URL-encoded-resourceURI}`

<span data-ttu-id="4d730-188">Di seguito sono i valori previsti hello:</span><span class="sxs-lookup"><span data-stu-id="4d730-188">Here are hello expected values:</span></span>

| <span data-ttu-id="4d730-189">Valore</span><span class="sxs-lookup"><span data-stu-id="4d730-189">Value</span></span> | <span data-ttu-id="4d730-190">Descrizione</span><span class="sxs-lookup"><span data-stu-id="4d730-190">Description</span></span> |
| --- | --- |
| <span data-ttu-id="4d730-191">{signature}</span><span class="sxs-lookup"><span data-stu-id="4d730-191">{signature}</span></span> |<span data-ttu-id="4d730-192">Una stringa di firma del modulo hello HMAC-SHA256: `{URL-encoded-resourceURI} + "\n" + expiry`.</span><span class="sxs-lookup"><span data-stu-id="4d730-192">An HMAC-SHA256 signature string of hello form: `{URL-encoded-resourceURI} + "\n" + expiry`.</span></span> <span data-ttu-id="4d730-193">**Importante**: chiave hello è decodificare da base64 e utilizzato come chiave tooperform calcolo di hello HMAC-SHA256.</span><span class="sxs-lookup"><span data-stu-id="4d730-193">**Important**: hello key is decoded from base64 and used as key tooperform hello HMAC-SHA256 computation.</span></span> |
| <span data-ttu-id="4d730-194">{resourceURI}</span><span class="sxs-lookup"><span data-stu-id="4d730-194">{resourceURI}</span></span> |<span data-ttu-id="4d730-195">Prefisso URI (per segmento) di endpoint hello che è possibile accedere con questo token, a partire da nome host dell'hub IoT hello (nessun protocol).</span><span class="sxs-lookup"><span data-stu-id="4d730-195">URI prefix (by segment) of hello endpoints that can be accessed with this token, starting with host name of hello IoT hub (no protocol).</span></span> <span data-ttu-id="4d730-196">Ad esempio, `myHub.azure-devices.net/devices/device1`</span><span class="sxs-lookup"><span data-stu-id="4d730-196">For example, `myHub.azure-devices.net/devices/device1`</span></span> |
| <span data-ttu-id="4d730-197">{expiry}</span><span class="sxs-lookup"><span data-stu-id="4d730-197">{expiry}</span></span> |<span data-ttu-id="4d730-198">Stringhe UTF8 per il numero di secondi trascorsi hello epoch 00:00:00 UTC del 1 ° gennaio 1970.</span><span class="sxs-lookup"><span data-stu-id="4d730-198">UTF8 strings for number of seconds since hello epoch 00:00:00 UTC on 1 January 1970.</span></span> |
| <span data-ttu-id="4d730-199">{URL-encoded-resourceURI}</span><span class="sxs-lookup"><span data-stu-id="4d730-199">{URL-encoded-resourceURI}</span></span> |<span data-ttu-id="4d730-200">Più basso caso la codifica URL della risorsa di lettere minuscole hello URI</span><span class="sxs-lookup"><span data-stu-id="4d730-200">Lower case URL-encoding of hello lower case resource URI</span></span> |
| <span data-ttu-id="4d730-201">{policyName}</span><span class="sxs-lookup"><span data-stu-id="4d730-201">{policyName}</span></span> |<span data-ttu-id="4d730-202">nome di Hello di hello condiviso toowhich di criteri di accesso che fa riferimento il token.</span><span class="sxs-lookup"><span data-stu-id="4d730-202">hello name of hello shared access policy toowhich this token refers.</span></span> <span data-ttu-id="4d730-203">Assente se il token hello fa riferimento credenziali toodevice Registro di sistema.</span><span class="sxs-lookup"><span data-stu-id="4d730-203">Absent if hello token refers toodevice-registry credentials.</span></span> |

<span data-ttu-id="4d730-204">**Nota sul prefisso**: prefisso URI hello viene calcolato dal segmento e non dai caratteri.</span><span class="sxs-lookup"><span data-stu-id="4d730-204">**Note on prefix**: hello URI prefix is computed by segment and not by character.</span></span> <span data-ttu-id="4d730-205">Ad esempio `/a/b` è un prefisso per `/a/b/c` ma non per `/a/bc`.</span><span class="sxs-lookup"><span data-stu-id="4d730-205">For example `/a/b` is a prefix for `/a/b/c` but not for `/a/bc`.</span></span>

<span data-ttu-id="4d730-206">Hello frammento Node.js seguente viene illustrata una funzione denominata **generateSasToken** che calcola hello token dagli input hello `resourceUri, signingKey, policyName, expiresInMins`.</span><span class="sxs-lookup"><span data-stu-id="4d730-206">hello following Node.js snippet shows a function called **generateSasToken** that computes hello token from hello inputs `resourceUri, signingKey, policyName, expiresInMins`.</span></span> <span data-ttu-id="4d730-207">Nelle sezioni successive di Hello in dettaglio come i diversi input hello tooinitialize per token diverso hello casi d'uso.</span><span class="sxs-lookup"><span data-stu-id="4d730-207">hello next sections detail how tooinitialize hello different inputs for hello different token use cases.</span></span>

```nodejs
var generateSasToken = function(resourceUri, signingKey, policyName, expiresInMins) {
    resourceUri = encodeURIComponent(resourceUri);

    // Set expiration in seconds
    var expires = (Date.now() / 1000) + expiresInMins * 60;
    expires = Math.ceil(expires);
    var toSign = resourceUri + '\n' + expires;

    // Use crypto
    var hmac = crypto.createHmac('sha256', new Buffer(signingKey, 'base64'));
    hmac.update(toSign);
    var base64UriEncoded = encodeURIComponent(hmac.digest('base64'));

    // Construct autorization string
    var token = "SharedAccessSignature sr=" + resourceUri + "&sig="
    + base64UriEncoded + "&se=" + expires;
    if (policyName) token += "&skn="+policyName;
    return token;
};
```

<span data-ttu-id="4d730-208">Come un confronto, hello equivalente toogenerate di codice Python che è un token di sicurezza:</span><span class="sxs-lookup"><span data-stu-id="4d730-208">As a comparison, hello equivalent Python code toogenerate a security token is:</span></span>

```python
from base64 import b64encode, b64decode
from hashlib import sha256
from time import time
from urllib import quote_plus, urlencode
from hmac import HMAC

def generate_sas_token(uri, key, policy_name, expiry=3600):
    ttl = time() + expiry
    sign_key = "%s\n%d" % ((quote_plus(uri)), int(ttl))
    print sign_key
    signature = b64encode(HMAC(b64decode(key), sign_key, sha256).digest())

    rawtoken = {
        'sr' :  uri,
        'sig': signature,
        'se' : str(int(ttl))
    }

    if policy_name is not None:
        rawtoken['skn'] = policy_name

    return 'SharedAccessSignature ' + urlencode(rawtoken)
```

> [!NOTE]
> <span data-ttu-id="4d730-209">Poiché hello tempo di validità delle token hello viene convalidato in computer IoT Hub, deviazione hello su clock hello del computer di hello che genera token hello deve essere minimo.</span><span class="sxs-lookup"><span data-stu-id="4d730-209">Since hello time validity of hello token is validated on IoT Hub machines, hello drift on hello clock of hello machine that generates hello token must be minimal.</span></span>

### <a name="use-sas-tokens-in-a-device-app"></a><span data-ttu-id="4d730-210">Usare i token di firma di accesso condiviso in un dispositivo client</span><span class="sxs-lookup"><span data-stu-id="4d730-210">Use SAS tokens in a device app</span></span>

<span data-ttu-id="4d730-211">Esistono due modi tooobtain **DeviceConnect** autorizzazioni con l'IoT Hub con i token di sicurezza: utilizzare un [chiave simmetrica dispositivo dal Registro di sistema identità hello](#use-a-symmetric-key-in-the-identity-registry), oppure utilizzare un [chiavediaccessocondiviso](#use-a-shared-access-policy).</span><span class="sxs-lookup"><span data-stu-id="4d730-211">There are two ways tooobtain **DeviceConnect** permissions with IoT Hub with security tokens: use a [symmetric device key from hello identity registry](#use-a-symmetric-key-in-the-identity-registry), or use a [shared access key](#use-a-shared-access-policy).</span></span>

<span data-ttu-id="4d730-212">Tenere presente che, per impostazione predefinita, tutte le funzionalità accessibili dai dispositivi vengono esposte negli endpoint con il prefisso `/devices/{deviceId}`.</span><span class="sxs-lookup"><span data-stu-id="4d730-212">Remember that all functionality accessible from devices is exposed by design on endpoints with prefix `/devices/{deviceId}`.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="4d730-213">chiave simmetrica identità del dispositivo hello utilizza Hello unico modo che l'IoT Hub autentica un dispositivo specifico.</span><span class="sxs-lookup"><span data-stu-id="4d730-213">hello only way that IoT Hub authenticates a specific device is using hello device identity symmetric key.</span></span> <span data-ttu-id="4d730-214">Quando un criterio di accesso condiviso viene usato tooaccess funzionalità del dispositivo, soluzione hello deve considerare la possibilità componente hello emissione di token di sicurezza hello come sottocomponente attendibile.</span><span class="sxs-lookup"><span data-stu-id="4d730-214">In cases when a shared access policy is used tooaccess device functionality, hello solution must consider hello component issuing hello security token as a trusted subcomponent.</span></span>

<span data-ttu-id="4d730-215">gli endpoint che utilizzano il dispositivo di Hello sono (indipendentemente dal protocollo hello):</span><span class="sxs-lookup"><span data-stu-id="4d730-215">hello device-facing endpoints are (irrespective of hello protocol):</span></span>

| <span data-ttu-id="4d730-216">Endpoint</span><span class="sxs-lookup"><span data-stu-id="4d730-216">Endpoint</span></span> | <span data-ttu-id="4d730-217">Funzionalità</span><span class="sxs-lookup"><span data-stu-id="4d730-217">Functionality</span></span> |
| --- | --- |
| `{iot hub host name}/devices/{deviceId}/messages/events` |<span data-ttu-id="4d730-218">Invio di messaggi da dispositivo a cloud.</span><span class="sxs-lookup"><span data-stu-id="4d730-218">Send device-to-cloud messages.</span></span> |
| `{iot hub host name}/devices/{deviceId}/devicebound` |<span data-ttu-id="4d730-219">Ricezione di messaggi da cloud a dispositivo.</span><span class="sxs-lookup"><span data-stu-id="4d730-219">Receive cloud-to-device messages.</span></span> |

### <a name="use-a-symmetric-key-in-hello-identity-registry"></a><span data-ttu-id="4d730-220">Utilizzare una chiave simmetrica nel Registro di sistema di hello identità</span><span class="sxs-lookup"><span data-stu-id="4d730-220">Use a symmetric key in hello identity registry</span></span>

<span data-ttu-id="4d730-221">Quando si utilizza toogenerate chiave simmetrica un token dell'identità del dispositivo, hello policyName (`skn`) elemento di token hello viene omesso.</span><span class="sxs-lookup"><span data-stu-id="4d730-221">When using a device identity's symmetric key toogenerate a token, hello policyName (`skn`) element of hello token is omitted.</span></span>

<span data-ttu-id="4d730-222">Ad esempio, un token creato tooaccess tutte le funzionalità di dispositivo deve avere hello seguenti parametri:</span><span class="sxs-lookup"><span data-stu-id="4d730-222">For example, a token created tooaccess all device functionality should have hello following parameters:</span></span>

* <span data-ttu-id="4d730-223">URI della risorsa: `{IoT hub name}.azure-devices.net/devices/{device id}`,</span><span class="sxs-lookup"><span data-stu-id="4d730-223">resource URI: `{IoT hub name}.azure-devices.net/devices/{device id}`,</span></span>
* <span data-ttu-id="4d730-224">chiave di firma: qualsiasi chiave simmetrica per hello `{device id}` identità,</span><span class="sxs-lookup"><span data-stu-id="4d730-224">signing key: any symmetric key for hello `{device id}` identity,</span></span>
* <span data-ttu-id="4d730-225">Nessun nome di criterio,</span><span class="sxs-lookup"><span data-stu-id="4d730-225">no policy name,</span></span>
* <span data-ttu-id="4d730-226">Qualsiasi ora di scadenza.</span><span class="sxs-lookup"><span data-stu-id="4d730-226">any expiration time.</span></span>

<span data-ttu-id="4d730-227">Un esempio di utilizzo hello precedente Node.js funzione sarà:</span><span class="sxs-lookup"><span data-stu-id="4d730-227">An example using hello preceding Node.js function would be:</span></span>

```nodejs
var endpoint ="myhub.azure-devices.net/devices/device1";
var deviceKey ="...";

var token = generateSasToken(endpoint, deviceKey, null, 60);
```

<span data-ttu-id="4d730-228">risultato Hello, che concede l'accesso tooall funzionalità per la periferica 1, sarà:</span><span class="sxs-lookup"><span data-stu-id="4d730-228">hello result, which grants access tooall functionality for device1, would be:</span></span>

`SharedAccessSignature sr=myhub.azure-devices.net%2fdevices%2fdevice1&sig=13y8ejUk2z7PLmvtwR5RqlGBOVwiq7rQR3WZ5xZX3N4%3D&se=1456971697`

> [!NOTE]
> <span data-ttu-id="4d730-229">È possibile toogenerate un token di firma di accesso condiviso usando .NET hello [Esplora dispositivo] [ lnk-device-explorer] degli strumenti o hello multipiattaforma, basato su nodi [l'hub IOT Esplora] [ lnk-iothub-explorer] utilità della riga di comando.</span><span class="sxs-lookup"><span data-stu-id="4d730-229">It is possible toogenerate a SAS token using hello .NET [device explorer][lnk-device-explorer] tool or hello cross-platform, node-based [iothub-explorer][lnk-iothub-explorer] command-line utility.</span></span>

### <a name="use-a-shared-access-policy"></a><span data-ttu-id="4d730-230">Usare criteri di accesso condiviso</span><span class="sxs-lookup"><span data-stu-id="4d730-230">Use a shared access policy</span></span>

<span data-ttu-id="4d730-231">Quando si crea un token da un criterio di accesso condiviso, impostare hello `skn` toohello nome dei criteri di hello.</span><span class="sxs-lookup"><span data-stu-id="4d730-231">When you create a token from a shared access policy, set hello `skn` field toohello name of hello policy.</span></span> <span data-ttu-id="4d730-232">Questo criterio deve concedere hello **DeviceConnect** autorizzazione.</span><span class="sxs-lookup"><span data-stu-id="4d730-232">This policy must grant hello **DeviceConnect** permission.</span></span>

<span data-ttu-id="4d730-233">Hello due scenari principali per l'utilizzo di funzionalità della periferica di tooaccess criteri di accesso condiviso sono:</span><span class="sxs-lookup"><span data-stu-id="4d730-233">hello two main scenarios for using shared access policies tooaccess device functionality are:</span></span>

* <span data-ttu-id="4d730-234">[gateway del protocollo cloud][lnk-endpoints],</span><span class="sxs-lookup"><span data-stu-id="4d730-234">[cloud protocol gateways][lnk-endpoints],</span></span>
* <span data-ttu-id="4d730-235">[servizi token] [ lnk-custom-auth] utilizzato tooimplement schemi di autenticazione personalizzati.</span><span class="sxs-lookup"><span data-stu-id="4d730-235">[token services][lnk-custom-auth] used tooimplement custom authentication schemes.</span></span>

<span data-ttu-id="4d730-236">Poiché hello criteri di accesso condiviso possono potenzialmente concedere accesso tooconnect qualsiasi dispositivo, che è importante toouse hello corretto URI della risorsa durante la creazione di token di sicurezza.</span><span class="sxs-lookup"><span data-stu-id="4d730-236">Since hello shared access policy can potentially grant access tooconnect as any device, it is important toouse hello correct resource URI when creating security tokens.</span></span> <span data-ttu-id="4d730-237">Questa impostazione è particolarmente importante per i servizi token, che hanno tooscope hello tooa token dispositivo specifico utilizzando l'URI della risorsa hello.</span><span class="sxs-lookup"><span data-stu-id="4d730-237">This setting is especially important for token services, which have tooscope hello token tooa specific device using hello resource URI.</span></span> <span data-ttu-id="4d730-238">Questo punto è meno importante per i gateway di protocollo, in quanto già filtrano il traffico per tutti i dispositivi.</span><span class="sxs-lookup"><span data-stu-id="4d730-238">This point is less relevant for protocol gateways as they are already mediating traffic for all devices.</span></span>

<span data-ttu-id="4d730-239">Ad esempio, un servizio token utilizzando hello creato in precedenza condivise criterio di accesso denominato **dispositivo** creerebbe un token con hello seguenti parametri:</span><span class="sxs-lookup"><span data-stu-id="4d730-239">As an example, a token service using hello pre-created shared access policy called **device** would create a token with hello following parameters:</span></span>

* <span data-ttu-id="4d730-240">URI della risorsa: `{IoT hub name}.azure-devices.net/devices/{device id}`,</span><span class="sxs-lookup"><span data-stu-id="4d730-240">resource URI: `{IoT hub name}.azure-devices.net/devices/{device id}`,</span></span>
* <span data-ttu-id="4d730-241">chiave di firma: una delle chiavi di hello di hello `device` criteri,</span><span class="sxs-lookup"><span data-stu-id="4d730-241">signing key: one of hello keys of hello `device` policy,</span></span>
* <span data-ttu-id="4d730-242">nome criterio: `device`,</span><span class="sxs-lookup"><span data-stu-id="4d730-242">policy name: `device`,</span></span>
* <span data-ttu-id="4d730-243">Qualsiasi ora di scadenza.</span><span class="sxs-lookup"><span data-stu-id="4d730-243">any expiration time.</span></span>

<span data-ttu-id="4d730-244">Un esempio di utilizzo hello precedente Node.js funzione sarà:</span><span class="sxs-lookup"><span data-stu-id="4d730-244">An example using hello preceding Node.js function would be:</span></span>

```nodejs
var endpoint ="myhub.azure-devices.net/devices/device1";
var policyName = 'device';
var policyKey = '...';

var token = generateSasToken(endpoint, policyKey, policyName, 60);
```

<span data-ttu-id="4d730-245">risultato Hello, che concede l'accesso tooall funzionalità per la periferica 1, sarà:</span><span class="sxs-lookup"><span data-stu-id="4d730-245">hello result, which grants access tooall functionality for device1, would be:</span></span>

`SharedAccessSignature sr=myhub.azure-devices.net%2fdevices%2fdevice1&sig=13y8ejUk2z7PLmvtwR5RqlGBOVwiq7rQR3WZ5xZX3N4%3D&se=1456971697&skn=device`

<span data-ttu-id="4d730-246">Un gateway di protocollo Impossibile usare hello stesso token per tutti i dispositivi semplicemente impostazione hello URI risorsa troppo`myhub.azure-devices.net/devices`.</span><span class="sxs-lookup"><span data-stu-id="4d730-246">A protocol gateway could use hello same token for all devices simply setting hello resource URI too`myhub.azure-devices.net/devices`.</span></span>

### <a name="use-security-tokens-from-service-components"></a><span data-ttu-id="4d730-247">Usare token di sicurezza da componenti del servizio</span><span class="sxs-lookup"><span data-stu-id="4d730-247">Use security tokens from service components</span></span>

<span data-ttu-id="4d730-248">Componenti del servizio possono solo generare token di sicurezza usando i criteri di accesso condiviso concessione delle autorizzazioni appropriate di hello come descritto in precedenza.</span><span class="sxs-lookup"><span data-stu-id="4d730-248">Service components can only generate security tokens using shared access policies granting hello appropriate permissions as explained previously.</span></span>

<span data-ttu-id="4d730-249">Ecco funzioni hello del servizio esposte su endpoint hello:</span><span class="sxs-lookup"><span data-stu-id="4d730-249">Here is hello service functions exposed on hello endpoints:</span></span>

| <span data-ttu-id="4d730-250">Endpoint</span><span class="sxs-lookup"><span data-stu-id="4d730-250">Endpoint</span></span> | <span data-ttu-id="4d730-251">Funzionalità</span><span class="sxs-lookup"><span data-stu-id="4d730-251">Functionality</span></span> |
| --- | --- |
| `{iot hub host name}/devices` |<span data-ttu-id="4d730-252">Creazione, aggiornamento, recupero ed eliminazione delle identità dispositivo.</span><span class="sxs-lookup"><span data-stu-id="4d730-252">Create, update, retrieve, and delete device identities.</span></span> |
| `{iot hub host name}/messages/events` |<span data-ttu-id="4d730-253">Ricezione di messaggi da dispositivo a cloud.</span><span class="sxs-lookup"><span data-stu-id="4d730-253">Receive device-to-cloud messages.</span></span> |
| `{iot hub host name}/servicebound/feedback` |<span data-ttu-id="4d730-254">Ricezione di feedback per messaggi da cloud a dispositivo.</span><span class="sxs-lookup"><span data-stu-id="4d730-254">Receive feedback for cloud-to-device messages.</span></span> |
| `{iot hub host name}/devicebound` |<span data-ttu-id="4d730-255">Invio di messaggi da cloud a dispositivo.</span><span class="sxs-lookup"><span data-stu-id="4d730-255">Send cloud-to-device messages.</span></span> |

<span data-ttu-id="4d730-256">Ad esempio, un servizio di generazione utilizzando hello creato in precedenza condivise criterio di accesso denominato **registryRead** creerebbe un token con hello seguenti parametri:</span><span class="sxs-lookup"><span data-stu-id="4d730-256">As an example, a service generating using hello pre-created shared access policy called **registryRead** would create a token with hello following parameters:</span></span>

* <span data-ttu-id="4d730-257">URI della risorsa: `{IoT hub name}.azure-devices.net/devices`,</span><span class="sxs-lookup"><span data-stu-id="4d730-257">resource URI: `{IoT hub name}.azure-devices.net/devices`,</span></span>
* <span data-ttu-id="4d730-258">chiave di firma: una delle chiavi di hello di hello `registryRead` criteri,</span><span class="sxs-lookup"><span data-stu-id="4d730-258">signing key: one of hello keys of hello `registryRead` policy,</span></span>
* <span data-ttu-id="4d730-259">nome criterio: `registryRead`,</span><span class="sxs-lookup"><span data-stu-id="4d730-259">policy name: `registryRead`,</span></span>
* <span data-ttu-id="4d730-260">Qualsiasi ora di scadenza.</span><span class="sxs-lookup"><span data-stu-id="4d730-260">any expiration time.</span></span>

```nodejs
var endpoint ="myhub.azure-devices.net/devices";
var policyName = 'device';
var policyKey = '...';

var token = generateSasToken(endpoint, policyKey, policyName, 60);
```

<span data-ttu-id="4d730-261">risultato Hello, che viene concesso l'accesso tooread tutte le identità del dispositivo, sarà:</span><span class="sxs-lookup"><span data-stu-id="4d730-261">hello result, which would grant access tooread all device identities, would be:</span></span>

`SharedAccessSignature sr=myhub.azure-devices.net%2fdevices&sig=JdyscqTpXdEJs49elIUCcohw2DlFDR3zfH5KqGJo4r4%3D&se=1456973447&skn=registryRead`

## <a name="supported-x509-certificates"></a><span data-ttu-id="4d730-262">Certificati X.509 supportati</span><span class="sxs-lookup"><span data-stu-id="4d730-262">Supported X.509 certificates</span></span>

<span data-ttu-id="4d730-263">È possibile utilizzare qualsiasi tooauthenticate certificato x. 509 un dispositivo con l'IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="4d730-263">You can use any X.509 certificate tooauthenticate a device with IoT Hub.</span></span> <span data-ttu-id="4d730-264">I certificati inclusi sono i seguenti:</span><span class="sxs-lookup"><span data-stu-id="4d730-264">Certificates include:</span></span>

* <span data-ttu-id="4d730-265">**Un certificato X.509 esistente**.</span><span class="sxs-lookup"><span data-stu-id="4d730-265">**An existing X.509 certificate**.</span></span> <span data-ttu-id="4d730-266">Un dispositivo potrebbe già avere un certificato X.509 associato.</span><span class="sxs-lookup"><span data-stu-id="4d730-266">A device may already have an X.509 certificate associated with it.</span></span> <span data-ttu-id="4d730-267">dispositivo Hello è possibile utilizzare questo tooauthenticate certificato con l'IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="4d730-267">hello device can use this certificate tooauthenticate with IoT Hub.</span></span>
* <span data-ttu-id="4d730-268">**Un certificato X-509 auto-generato e auto-firmato**.</span><span class="sxs-lookup"><span data-stu-id="4d730-268">**A self-generated and self-signed X-509 certificate**.</span></span> <span data-ttu-id="4d730-269">Un produttore del dispositivo o i distributori interne possono generare questi certificati e archiviare la chiave privata corrispondente di hello (e certificato) su dispositivo hello.</span><span class="sxs-lookup"><span data-stu-id="4d730-269">A device manufacturer or in-house deployer can generate these certificates and store hello corresponding private key (and certificate) on hello device.</span></span> <span data-ttu-id="4d730-270">È possibile usare strumenti come [OpenSSL][lnk-openssl] e l'utilità [Windows SelfSignedCertificate][lnk-selfsigned] per questo scopo.</span><span class="sxs-lookup"><span data-stu-id="4d730-270">You can use tools such as [OpenSSL][lnk-openssl] and [Windows SelfSignedCertificate][lnk-selfsigned] utility for this purpose.</span></span>
* <span data-ttu-id="4d730-271">**Certificato X.509 firmato da un'autorità di certificazione**.</span><span class="sxs-lookup"><span data-stu-id="4d730-271">**CA-signed X.509 certificate**.</span></span> <span data-ttu-id="4d730-272">tooidentify un dispositivo e l'autenticazione con l'IoT Hub, è possibile usare un certificato x. 509 generato e firmato da un'autorità di certificazione (CA).</span><span class="sxs-lookup"><span data-stu-id="4d730-272">tooidentify a device and authenticate it with IoT Hub, you can use an X.509 certificate generated and signed by a Certification Authority (CA).</span></span> <span data-ttu-id="4d730-273">IoT Hub verifica solo tale identificazione digitale hello presentati corrispondente identificazione personale hello configurato.</span><span class="sxs-lookup"><span data-stu-id="4d730-273">IoT Hub only verifies that hello thumbprint presented matches hello configured thumbprint.</span></span> <span data-ttu-id="4d730-274">L'hub IOT non viene convalidata la catena di certificati hello.</span><span class="sxs-lookup"><span data-stu-id="4d730-274">IotHub does not validate hello certificate chain.</span></span>

<span data-ttu-id="4d730-275">Un dispositivo può usare un certificato X.509 o un token di sicurezza per l'autenticazione, ma non per entrambi.</span><span class="sxs-lookup"><span data-stu-id="4d730-275">A device may either use an X.509 certificate or a security token for authentication, but not both.</span></span>

### <a name="register-an-x509-certificate-for-a-device"></a><span data-ttu-id="4d730-276">Registrare un certificato X.509 per un dispositivo</span><span class="sxs-lookup"><span data-stu-id="4d730-276">Register an X.509 certificate for a device</span></span>

<span data-ttu-id="4d730-277">Hello [SDK di servizi IoT di Azure per c#] [ lnk-service-sdk] (versione 1.0.8+) supporta la registrazione di un dispositivo che usa un certificato x. 509 per l'autenticazione.</span><span class="sxs-lookup"><span data-stu-id="4d730-277">hello [Azure IoT Service SDK for C#][lnk-service-sdk] (version 1.0.8+) supports registering a device that uses an X.509 certificate for authentication.</span></span> <span data-ttu-id="4d730-278">Anche altre API come quelle per l'importazione e l'esportazione dei dispositivi supportano i certificati X.509.</span><span class="sxs-lookup"><span data-stu-id="4d730-278">Other APIs such as import/export of devices also support X.509 certificates.</span></span>

### <a name="c-support"></a><span data-ttu-id="4d730-279">Supporto per C\#</span><span class="sxs-lookup"><span data-stu-id="4d730-279">C\# Support</span></span>

<span data-ttu-id="4d730-280">Hello **RegistryManager** classe fornisce un modo programmatico di tooregister un dispositivo.</span><span class="sxs-lookup"><span data-stu-id="4d730-280">hello **RegistryManager** class provides a programmatic way tooregister a device.</span></span> <span data-ttu-id="4d730-281">In particolare, hello **AddDeviceAsync** e **UpdateDeviceAsync** metodi consentono di tooregister e aggiornare un dispositivo in hello del Registro di sistema di IoT Hub identità.</span><span class="sxs-lookup"><span data-stu-id="4d730-281">In particular, hello **AddDeviceAsync** and **UpdateDeviceAsync** methods enable you tooregister and update a device in hello IoT Hub identity registry.</span></span> <span data-ttu-id="4d730-282">Questi due metodi accettano un'istanza **Device** come input.</span><span class="sxs-lookup"><span data-stu-id="4d730-282">These two methods take a **Device** instance as input.</span></span> <span data-ttu-id="4d730-283">Hello **dispositivo** classe include un **autenticazione** proprietà che è possibile toospecify primarie e secondarie x. 509 identificazioni personali del certificato.</span><span class="sxs-lookup"><span data-stu-id="4d730-283">hello **Device** class includes an **Authentication** property that allows you toospecify primary and secondary X.509 certificate thumbprints.</span></span> <span data-ttu-id="4d730-284">identificazione personale Hello rappresenta un hash SHA-1 del certificato x. 509 hello (archiviato utilizzando la codifica DER binaria).</span><span class="sxs-lookup"><span data-stu-id="4d730-284">hello thumbprint represents a SHA-1 hash of hello X.509 certificate (stored using binary DER encoding).</span></span> <span data-ttu-id="4d730-285">È possibile hello che specifica un'identificazione personale del primaria o un'identificazione personale del secondario o entrambi.</span><span class="sxs-lookup"><span data-stu-id="4d730-285">You have hello option of specifying a primary thumbprint or a secondary thumbprint or both.</span></span> <span data-ttu-id="4d730-286">Identificazioni personali primarie e secondarie sono toohandle supportati scenari di rollover dei certificati.</span><span class="sxs-lookup"><span data-stu-id="4d730-286">Primary and secondary thumbprints are supported toohandle certificate rollover scenarios.</span></span>

> [!NOTE]
> <span data-ttu-id="4d730-287">IoT Hub non è necessario né archiviare il certificato x. 509 intera hello, solo identificazione personale hello.</span><span class="sxs-lookup"><span data-stu-id="4d730-287">IoT Hub does not require or store hello entire X.509 certificate, only hello thumbprint.</span></span>

<span data-ttu-id="4d730-288">Di seguito è riportato un esempio C\# tooregister frammento di codice un dispositivo utilizzando un certificato x. 509:</span><span class="sxs-lookup"><span data-stu-id="4d730-288">Here is a sample C\# code snippet tooregister a device using an X.509 certificate:</span></span>

```csharp
var device = new Device(deviceId)
{
  Authentication = new AuthenticationMechanism()
  {
    X509Thumbprint = new X509Thumbprint()
    {
      PrimaryThumbprint = "921BC9694ADEB8929D4F7FE4B9A3A6DE58B0790B"
    }
  }
};
RegistryManager registryManager = RegistryManager.CreateFromConnectionString(deviceGatewayConnectionString);
await registryManager.AddDeviceAsync(device);
```

### <a name="use-an-x509-certificate-during-run-time-operations"></a><span data-ttu-id="4d730-289">Usare un certificato X.509 durante le operazioni di runtime</span><span class="sxs-lookup"><span data-stu-id="4d730-289">Use an X.509 certificate during run-time operations</span></span>

<span data-ttu-id="4d730-290">Hello [dispositivo IoT di Azure SDK per .NET] [ lnk-client-sdk] (versione 1.0.11+) supporta l'utilizzo di hello di certificati x. 509.</span><span class="sxs-lookup"><span data-stu-id="4d730-290">hello [Azure IoT device SDK for .NET][lnk-client-sdk] (version 1.0.11+) supports hello use of X.509 certificates.</span></span>

### <a name="c-support"></a><span data-ttu-id="4d730-291">Supporto per C\#</span><span class="sxs-lookup"><span data-stu-id="4d730-291">C\# Support</span></span>

<span data-ttu-id="4d730-292">classe Hello **DeviceAuthenticationWithX509Certificate** supporta hello creazione di **DeviceClient** istanze tramite un certificato x. 509.</span><span class="sxs-lookup"><span data-stu-id="4d730-292">hello class **DeviceAuthenticationWithX509Certificate** supports hello creation of **DeviceClient** instances using an X.509 certificate.</span></span> <span data-ttu-id="4d730-293">certificato x. 509 Hello deve essere nel formato PFX (denominato anche PKCS #12) hello che include la chiave privata di hello.</span><span class="sxs-lookup"><span data-stu-id="4d730-293">hello X.509 certificate must be in hello PFX (also called PKCS #12) format that includes hello private key.</span></span>

<span data-ttu-id="4d730-294">Di seguito è riportato un frammento di codice di esempio:</span><span class="sxs-lookup"><span data-stu-id="4d730-294">Here is a sample code snippet:</span></span>

```csharp
var authMethod = new DeviceAuthenticationWithX509Certificate("<device id>", x509Certificate);

var deviceClient = DeviceClient.Create("<IotHub DNS HostName>", authMethod);
```

## <a name="custom-device-authentication"></a><span data-ttu-id="4d730-295">Autenticazione personalizzata del dispositivo</span><span class="sxs-lookup"><span data-stu-id="4d730-295">Custom device authentication</span></span>

<span data-ttu-id="4d730-296">È possibile usare l'IoT Hub hello [Registro di sistema di identità] [ lnk-identity-registry] tooconfigure le credenziali di sicurezza per ogni dispositivo e controllo dell'accesso tramite [token] [ lnk-sas-tokens] .</span><span class="sxs-lookup"><span data-stu-id="4d730-296">You can use hello IoT Hub [identity registry][lnk-identity-registry] tooconfigure per-device security credentials and access control using [tokens][lnk-sas-tokens].</span></span> <span data-ttu-id="4d730-297">Se una soluzione IoT dispone già di una combinazione di identità personalizzato del Registro di sistema e/o l'autenticazione, è consigliabile creare un *servizio token* toointegrate questa infrastruttura con l'IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="4d730-297">If an IoT solution already has a custom identity registry and/or authentication scheme, consider creating a *token service* toointegrate this infrastructure with IoT Hub.</span></span> <span data-ttu-id="4d730-298">In questo modo, è possibile usare altre funzionalità IoT nella soluzione.</span><span class="sxs-lookup"><span data-stu-id="4d730-298">In this way, you can use other IoT features in your solution.</span></span>

<span data-ttu-id="4d730-299">Un servizio token è un servizio cloud personalizzato.</span><span class="sxs-lookup"><span data-stu-id="4d730-299">A token service is a custom cloud service.</span></span> <span data-ttu-id="4d730-300">Usa un IoT Hub *criterio di accesso condiviso* con **DeviceConnect** autorizzazioni toocreate *con ambito dispositivo* token.</span><span class="sxs-lookup"><span data-stu-id="4d730-300">It uses an IoT Hub *shared access policy* with **DeviceConnect** permissions toocreate *device-scoped* tokens.</span></span> <span data-ttu-id="4d730-301">Questi token abilitare l'hub IoT tooyour tooconnect un dispositivo.</span><span class="sxs-lookup"><span data-stu-id="4d730-301">These tokens enable a device tooconnect tooyour IoT hub.</span></span>

![Passaggi del modello di servizio token di hello][img-tokenservice]

<span data-ttu-id="4d730-303">Ecco i passaggi principali hello del modello di servizio token di hello:</span><span class="sxs-lookup"><span data-stu-id="4d730-303">Here are hello main steps of hello token service pattern:</span></span>

1. <span data-ttu-id="4d730-304">Creare i criteri di accesso condiviso dell'hub IoT con autorizzazioni **DeviceConnect** per l'hub IoT.</span><span class="sxs-lookup"><span data-stu-id="4d730-304">Create an IoT Hub shared access policy with **DeviceConnect** permissions for your IoT hub.</span></span> <span data-ttu-id="4d730-305">È possibile creare questo criterio in hello [portale di Azure] [ lnk-management-portal] o a livello di codice.</span><span class="sxs-lookup"><span data-stu-id="4d730-305">You can create this policy in hello [Azure portal][lnk-management-portal] or programmatically.</span></span> <span data-ttu-id="4d730-306">il servizio token di Hello utilizza i token di hello toosign questo criterio viene creato.</span><span class="sxs-lookup"><span data-stu-id="4d730-306">hello token service uses this policy toosign hello tokens it creates.</span></span>
1. <span data-ttu-id="4d730-307">Quando un dispositivo deve tooaccess l'hub IoT, richiede un token firmato dal servizio token.</span><span class="sxs-lookup"><span data-stu-id="4d730-307">When a device needs tooaccess your IoT hub, it requests a signed token from your token service.</span></span> <span data-ttu-id="4d730-308">Hello dispositivo può eseguire l'autenticazione con l'identità del dispositivo identità personalizzato del Registro di sistema o di autenticazione schema toodetermine hello che il servizio token di hello utilizza token hello toocreate.</span><span class="sxs-lookup"><span data-stu-id="4d730-308">hello device can authenticate with your custom identity registry/authentication scheme toodetermine hello device identity that hello token service uses toocreate hello token.</span></span>
1. <span data-ttu-id="4d730-309">il servizio token di Hello restituisce un token.</span><span class="sxs-lookup"><span data-stu-id="4d730-309">hello token service returns a token.</span></span> <span data-ttu-id="4d730-310">Hello token viene creato utilizzando `/devices/{deviceId}` come `resourceURI`, con `deviceId` come dispositivo hello da autenticare.</span><span class="sxs-lookup"><span data-stu-id="4d730-310">hello token is created by using `/devices/{deviceId}` as `resourceURI`, with `deviceId` as hello device being authenticated.</span></span> <span data-ttu-id="4d730-311">il servizio token di Hello utilizza il token hello tooconstruct di hello accesso condiviso dei criteri.</span><span class="sxs-lookup"><span data-stu-id="4d730-311">hello token service uses hello shared access policy tooconstruct hello token.</span></span>
1. <span data-ttu-id="4d730-312">dispositivo di Hello Usa token hello direttamente con l'hub IoT hello.</span><span class="sxs-lookup"><span data-stu-id="4d730-312">hello device uses hello token directly with hello IoT hub.</span></span>

> [!NOTE]
> <span data-ttu-id="4d730-313">È possibile utilizzare una classe .NET hello [SharedAccessSignatureBuilder] [ lnk-dotnet-sas] o hello classe Java [IotHubServiceSasToken] [ lnk-java-sas] toocreate un token nel servizio di token.</span><span class="sxs-lookup"><span data-stu-id="4d730-313">You can use hello .NET class [SharedAccessSignatureBuilder][lnk-dotnet-sas] or hello Java class [IotHubServiceSasToken][lnk-java-sas] toocreate a token in your token service.</span></span>

<span data-ttu-id="4d730-314">il servizio token di Hello è possibile impostare scadenza del token hello in base alle esigenze.</span><span class="sxs-lookup"><span data-stu-id="4d730-314">hello token service can set hello token expiration as desired.</span></span> <span data-ttu-id="4d730-315">Quando il token hello scade, l'hub IoT hello server connessione dispositivo hello.</span><span class="sxs-lookup"><span data-stu-id="4d730-315">When hello token expires, hello IoT hub severs hello device connection.</span></span> <span data-ttu-id="4d730-316">Quindi, dispositivo hello deve richiedere un nuovo token dal servizio token di hello.</span><span class="sxs-lookup"><span data-stu-id="4d730-316">Then, hello device must request a new token from hello token service.</span></span> <span data-ttu-id="4d730-317">Una scadenza breve aumenta il carico di hello sul dispositivo hello e servizio token di hello.</span><span class="sxs-lookup"><span data-stu-id="4d730-317">A short expiry time increases hello load on both hello device and hello token service.</span></span>

<span data-ttu-id="4d730-318">Per un hub di tooyour tooconnect dispositivo, è necessario comunque aggiungerla toohello del Registro di sistema di IoT Hub identità, anche se hello dispositivo usa un token e non una chiave tooconnect di dispositivo.</span><span class="sxs-lookup"><span data-stu-id="4d730-318">For a device tooconnect tooyour hub, you must still add it toohello IoT Hub identity registry — even though hello device is using a token and not a device key tooconnect.</span></span> <span data-ttu-id="4d730-319">Pertanto, è possibile continuare controllo di accesso per ogni dispositivo toouse abilitando o disabilitando le identità del dispositivo in hello [Registro di sistema di identità][lnk-identity-registry].</span><span class="sxs-lookup"><span data-stu-id="4d730-319">Therefore, you can continue toouse per-device access control by enabling or disabling device identities in hello [identity registry][lnk-identity-registry].</span></span> <span data-ttu-id="4d730-320">Questo approccio consente di ridurre i rischi di hello di utilizzo di token con ore di scadenza lunga.</span><span class="sxs-lookup"><span data-stu-id="4d730-320">This approach mitigates hello risks of using tokens with long expiry times.</span></span>

### <a name="comparison-with-a-custom-gateway"></a><span data-ttu-id="4d730-321">Confronto con un gateway personalizzato</span><span class="sxs-lookup"><span data-stu-id="4d730-321">Comparison with a custom gateway</span></span>

<span data-ttu-id="4d730-322">modello di servizio token di Hello è hello consigliato in modo tooimplement una combinazione di identità personalizzato del Registro di sistema o di autenticazione con l'IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="4d730-322">hello token service pattern is hello recommended way tooimplement a custom identity registry/authentication scheme with IoT Hub.</span></span> <span data-ttu-id="4d730-323">Questo modello è consigliato perché l'IoT Hub continua toohandle la maggior parte del traffico di soluzione hello.</span><span class="sxs-lookup"><span data-stu-id="4d730-323">This pattern is recommended because IoT Hub continues toohandle most of hello solution traffic.</span></span> <span data-ttu-id="4d730-324">Tuttavia, se lo schema di autenticazione personalizzato hello è così interconnesse con protocollo hello, potrebbe essere necessario un *gateway personalizzato* tooprocess tutti hello traffico.</span><span class="sxs-lookup"><span data-stu-id="4d730-324">However, if hello custom authentication scheme is so intertwined with hello protocol, you may require a *custom gateway* tooprocess all hello traffic.</span></span> <span data-ttu-id="4d730-325">Un esempio di tale scenario prevede l'uso del [protocollo TLS (Transport Layer Security) e di chiavi precondivise][lnk-tls-psk].</span><span class="sxs-lookup"><span data-stu-id="4d730-325">An example of such a scenario is using[Transport Layer Security (TLS) and pre-shared keys (PSKs)][lnk-tls-psk].</span></span> <span data-ttu-id="4d730-326">Per ulteriori informazioni, vedere hello [gateway del protocollo] [ lnk-protocols] argomento.</span><span class="sxs-lookup"><span data-stu-id="4d730-326">For more information, see hello [protocol gateway][lnk-protocols] topic.</span></span>

## <a name="reference-topics"></a><span data-ttu-id="4d730-327">Argomenti di riferimento:</span><span class="sxs-lookup"><span data-stu-id="4d730-327">Reference topics:</span></span>

<span data-ttu-id="4d730-328">Hello argomenti di riferimento seguenti offrono ulteriori informazioni su controllo hub IoT tooyour di accesso.</span><span class="sxs-lookup"><span data-stu-id="4d730-328">hello following reference topics provide you with more information about controlling access tooyour IoT hub.</span></span>

## <a name="iot-hub-permissions"></a><span data-ttu-id="4d730-329">Autorizzazioni per l'hub IoT</span><span class="sxs-lookup"><span data-stu-id="4d730-329">IoT Hub permissions</span></span>

<span data-ttu-id="4d730-330">Hello nella tabella seguente elenca le autorizzazioni di hello è possibile usare l'hub IoT accesso tooyour toocontrol.</span><span class="sxs-lookup"><span data-stu-id="4d730-330">hello following table lists hello permissions you can use toocontrol access tooyour IoT hub.</span></span>

| <span data-ttu-id="4d730-331">Autorizzazione</span><span class="sxs-lookup"><span data-stu-id="4d730-331">Permission</span></span> | <span data-ttu-id="4d730-332">Note</span><span class="sxs-lookup"><span data-stu-id="4d730-332">Notes</span></span> |
| --- | --- |
| <span data-ttu-id="4d730-333">**RegistryRead**</span><span class="sxs-lookup"><span data-stu-id="4d730-333">**RegistryRead**</span></span> |<span data-ttu-id="4d730-334">Concede l'accesso in lettura toohello identità Registro di sistema.</span><span class="sxs-lookup"><span data-stu-id="4d730-334">Grants read access toohello identity registry.</span></span> <span data-ttu-id="4d730-335">Per altre informazioni, vedere [Registro delle identità][lnk-identity-registry].</span><span class="sxs-lookup"><span data-stu-id="4d730-335">For more information, see [Identity registry][lnk-identity-registry].</span></span> <br/><span data-ttu-id="4d730-336">Questa autorizzazione viene usata dai servizi cloud back-end.</span><span class="sxs-lookup"><span data-stu-id="4d730-336">This permission is used by back-end cloud services.</span></span> |
| <span data-ttu-id="4d730-337">**RegistryReadWrite**</span><span class="sxs-lookup"><span data-stu-id="4d730-337">**RegistryReadWrite**</span></span> |<span data-ttu-id="4d730-338">Concede l'accesso in lettura e scrittura toohello identità Registro di sistema.</span><span class="sxs-lookup"><span data-stu-id="4d730-338">Grants read and write access toohello identity registry.</span></span> <span data-ttu-id="4d730-339">Per altre informazioni, vedere [Registro delle identità][lnk-identity-registry].</span><span class="sxs-lookup"><span data-stu-id="4d730-339">For more information, see [Identity registry][lnk-identity-registry].</span></span> <br/><span data-ttu-id="4d730-340">Questa autorizzazione viene usata dai servizi cloud back-end.</span><span class="sxs-lookup"><span data-stu-id="4d730-340">This permission is used by back-end cloud services.</span></span> |
| <span data-ttu-id="4d730-341">**ServiceConnect**</span><span class="sxs-lookup"><span data-stu-id="4d730-341">**ServiceConnect**</span></span> |<span data-ttu-id="4d730-342">Concede l'accesso toocloud orientati ai servizi comunicazione e gli endpoint di monitoraggio.</span><span class="sxs-lookup"><span data-stu-id="4d730-342">Grants access toocloud service-facing communication and monitoring endpoints.</span></span> <br/><span data-ttu-id="4d730-343">Concede l'autorizzazione i messaggi da dispositivo a cloud tooreceive, inviare messaggi da cloud a dispositivo e recuperare hello corrispondente conferma di recapito.</span><span class="sxs-lookup"><span data-stu-id="4d730-343">Grants permission tooreceive device-to-cloud messages, send cloud-to-device messages, and retrieve hello corresponding delivery acknowledgments.</span></span> <br/><span data-ttu-id="4d730-344">Concede l'autorizzazione tooretrieve recapito riconoscimenti per il file caricato.</span><span class="sxs-lookup"><span data-stu-id="4d730-344">Grants permission tooretrieve delivery acknowledgements for file uploads.</span></span> <br/><span data-ttu-id="4d730-345">Concede l'autorizzazione tooaccess dispositivo gemelli tooupdate tag e le proprietà desiderate, recuperare le proprietà segnalate ed eseguire query.</span><span class="sxs-lookup"><span data-stu-id="4d730-345">Grants permission tooaccess device twins tooupdate tags and desired properties, retrieve reported properties, and run queries.</span></span> <br/><span data-ttu-id="4d730-346">Questa autorizzazione viene usata dai servizi cloud back-end.</span><span class="sxs-lookup"><span data-stu-id="4d730-346">This permission is used by back-end cloud services.</span></span> |
| <span data-ttu-id="4d730-347">**DeviceConnect**</span><span class="sxs-lookup"><span data-stu-id="4d730-347">**DeviceConnect**</span></span> |<span data-ttu-id="4d730-348">Concede l'accesso gli endpoint orientati toodevice.</span><span class="sxs-lookup"><span data-stu-id="4d730-348">Grants access toodevice-facing endpoints.</span></span> <br/><span data-ttu-id="4d730-349">Concede l'autorizzazione toosend dispositivo a cloud dei messaggi e ricevere messaggi da cloud a dispositivo.</span><span class="sxs-lookup"><span data-stu-id="4d730-349">Grants permission toosend device-to-cloud messages and receive cloud-to-device messages.</span></span> <br/><span data-ttu-id="4d730-350">Concede l'autorizzazione tooperform il caricamento di file da un dispositivo.</span><span class="sxs-lookup"><span data-stu-id="4d730-350">Grants permission tooperform file upload from a device.</span></span> <br/><span data-ttu-id="4d730-351">Concede l'autorizzazione tooreceive doppi desiderato proprietà notifiche e aggiornamento dispositivo doppio proprietà segnalate.</span><span class="sxs-lookup"><span data-stu-id="4d730-351">Grants permission tooreceive device twin desired property notifications and update device twin reported properties.</span></span> <br/><span data-ttu-id="4d730-352">Carica file di tooperform concede l'autorizzazione.</span><span class="sxs-lookup"><span data-stu-id="4d730-352">Grants permission tooperform file uploads.</span></span> <br/><span data-ttu-id="4d730-353">Questa autorizzazione viene usata dai dispositivi.</span><span class="sxs-lookup"><span data-stu-id="4d730-353">This permission is used by devices.</span></span> |

## <a name="additional-reference-material"></a><span data-ttu-id="4d730-354">Materiale di riferimento</span><span class="sxs-lookup"><span data-stu-id="4d730-354">Additional reference material</span></span>

<span data-ttu-id="4d730-355">Altri argomenti di riferimento nella Guida per sviluppatori di IoT Hub hello includono:</span><span class="sxs-lookup"><span data-stu-id="4d730-355">Other reference topics in hello IoT Hub developer guide include:</span></span>

* <span data-ttu-id="4d730-356">[Gli endpoint IoT Hub] [ lnk-endpoints] descrive hello vari endpoint che espone ogni hub IoT per le operazioni in fase di esecuzione e gestione.</span><span class="sxs-lookup"><span data-stu-id="4d730-356">[IoT Hub endpoints][lnk-endpoints] describes hello various endpoints that each IoT hub exposes for run-time and management operations.</span></span>
* <span data-ttu-id="4d730-357">[Limitazione delle richieste e le quote] [ lnk-quotas] descrive le quote di hello e la limitazione di comportamenti che si applicano toohello servizio IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="4d730-357">[Throttling and quotas][lnk-quotas] describes hello quotas and throttling behaviors that apply toohello IoT Hub service.</span></span>
* <span data-ttu-id="4d730-358">[Gli SDK di dispositivi e servizi di Azure IoT] [ lnk-sdks] elenchi hello language vari SDK è possibile utilizzare quando si sviluppano applicazioni di servizio sia sul dispositivo che interagiscono con l'IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="4d730-358">[Azure IoT device and service SDKs][lnk-sdks] lists hello various language SDKs you can use when you develop both device and service apps that interact with IoT Hub.</span></span>
* <span data-ttu-id="4d730-359">[Il linguaggio di query di IoT Hub] [ lnk-query] descrive il linguaggio di query hello è possibile utilizzare tooretrieve informazioni dall'IoT Hub sul gemelli di dispositivo e i processi.</span><span class="sxs-lookup"><span data-stu-id="4d730-359">[IoT Hub query language][lnk-query] describes hello query language you can use tooretrieve information from IoT Hub about your device twins and jobs.</span></span>
* <span data-ttu-id="4d730-360">[Supporto di IoT Hub MQTT] [ lnk-devguide-mqtt] fornisce ulteriori informazioni sul supporto di IoT Hub per protocollo MQTT hello.</span><span class="sxs-lookup"><span data-stu-id="4d730-360">[IoT Hub MQTT support][lnk-devguide-mqtt] provides more information about IoT Hub support for hello MQTT protocol.</span></span>

## <a name="next-steps"></a><span data-ttu-id="4d730-361">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="4d730-361">Next steps</span></span>

<span data-ttu-id="4d730-362">Ora si è appreso come toocontrol accedere IoT Hub, potrebbero essere interessati hello seguenti argomenti della Guida per sviluppatori IoT Hub:</span><span class="sxs-lookup"><span data-stu-id="4d730-362">Now you have learned how toocontrol access IoT Hub, you may be interested in hello following IoT Hub developer guide topics:</span></span>

* <span data-ttu-id="4d730-363">[Utilizzare lo stato del dispositivo gemelli toosynchronize e configurazioni][lnk-devguide-device-twins]</span><span class="sxs-lookup"><span data-stu-id="4d730-363">[Use device twins toosynchronize state and configurations][lnk-devguide-device-twins]</span></span>
* <span data-ttu-id="4d730-364">[Richiamare un metodo diretto in un dispositivo][lnk-devguide-directmethods]</span><span class="sxs-lookup"><span data-stu-id="4d730-364">[Invoke a direct method on a device][lnk-devguide-directmethods]</span></span>
* <span data-ttu-id="4d730-365">[Pianificare processi in più dispositivi][lnk-devguide-jobs]</span><span class="sxs-lookup"><span data-stu-id="4d730-365">[Schedule jobs on multiple devices][lnk-devguide-jobs]</span></span>

<span data-ttu-id="4d730-366">Se si desidera tootry alcuni dei concetti di hello descritti in questo articolo, si potrebbero essere interessati hello seguenti esercitazioni IoT Hub:</span><span class="sxs-lookup"><span data-stu-id="4d730-366">If you would like tootry out some of hello concepts described in this article, you may be interested in hello following IoT Hub tutorials:</span></span>

* <span data-ttu-id="4d730-367">[Introduzione all'hub IoT di Azure][lnk-getstarted-tutorial]</span><span class="sxs-lookup"><span data-stu-id="4d730-367">[Get started with Azure IoT Hub][lnk-getstarted-tutorial]</span></span>
* <span data-ttu-id="4d730-368">[La modalità toosend cloud a dispositivo dei messaggi con l'IoT Hub][lnk-c2d-tutorial]</span><span class="sxs-lookup"><span data-stu-id="4d730-368">[How toosend cloud-to-device messages with IoT Hub][lnk-c2d-tutorial]</span></span>
* <span data-ttu-id="4d730-369">[Come tooprocess messaggi da dispositivo a cloud IoT Hub][lnk-d2c-tutorial]</span><span class="sxs-lookup"><span data-stu-id="4d730-369">[How tooprocess IoT Hub device-to-cloud messages][lnk-d2c-tutorial]</span></span>

<!-- links and images -->

[img-tokenservice]: ./media/iot-hub-devguide-security/tokenservice.png
[lnk-endpoints]: iot-hub-devguide-endpoints.md
[lnk-quotas]: iot-hub-devguide-quotas-throttling.md
[lnk-sdks]: iot-hub-devguide-sdks.md
[lnk-query]: iot-hub-devguide-query-language.md
[lnk-devguide-mqtt]: iot-hub-mqtt-support.md
[lnk-openssl]: https://www.openssl.org/
[lnk-selfsigned]: https://technet.microsoft.com/library/hh848633

[lnk-resource-provider-apis]: https://docs.microsoft.com/rest/api/iothub/iothubresource
[lnk-sas-tokens]: iot-hub-devguide-security.md#security-tokens
[lnk-amqp]: https://www.amqp.org/
[lnk-azure-resource-manager]: ../azure-resource-manager/resource-group-overview.md
[lnk-cbs]: https://www.oasis-open.org/committees/download.php/50506/amqp-cbs-v1%200-wd02%202013-08-12.doc
[lnk-event-hubs-publisher-policy]: https://code.msdn.microsoft.com/Service-Bus-Event-Hub-99ce67ab
[lnk-management-portal]: https://portal.azure.com
[lnk-sasl-plain]: http://tools.ietf.org/html/rfc4616
[lnk-identity-registry]: iot-hub-devguide-identity-registry.md
[lnk-dotnet-sas]: https://msdn.microsoft.com/library/microsoft.azure.devices.common.security.sharedaccesssignaturebuilder.aspx
[lnk-java-sas]: https://docs.microsoft.com/java/api/com.microsoft.azure.sdk.iot.service.auth._iot_hub_service_sas_token
[lnk-tls-psk]: https://tools.ietf.org/html/rfc4279
[lnk-protocols]: iot-hub-protocol-gateway.md
[lnk-custom-auth]: iot-hub-devguide-security.md#custom-device-authentication
[lnk-x509]: iot-hub-devguide-security.md#supported-x509-certificates
[lnk-devguide-device-twins]: iot-hub-devguide-device-twins.md
[lnk-devguide-directmethods]: iot-hub-devguide-direct-methods.md
[lnk-devguide-jobs]: iot-hub-devguide-jobs.md
[lnk-service-sdk]: https://github.com/Azure/azure-iot-sdk-csharp/tree/master/service
[lnk-client-sdk]: https://github.com/Azure/azure-iot-sdk-csharp/tree/master/device
[lnk-device-explorer]: https://github.com/Azure/azure-iot-sdk-csharp/blob/master/tools/DeviceExplorer
[lnk-iothub-explorer]: https://github.com/azure/iothub-explorer

[lnk-getstarted-tutorial]: iot-hub-csharp-csharp-getstarted.md
[lnk-c2d-tutorial]: iot-hub-csharp-csharp-c2d.md
[lnk-d2c-tutorial]: iot-hub-csharp-csharp-process-d2c.md

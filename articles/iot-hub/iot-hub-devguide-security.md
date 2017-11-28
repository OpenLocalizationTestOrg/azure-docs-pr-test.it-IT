---
title: Informazioni sulla sicurezza dell'hub IoT di Azure | Microsoft Docs
description: Guida per sviluppatori - Come controllare l'accesso all'hub IoT per app back-end e per dispositivi. Include informazioni sui token di sicurezza e sul supporto per i certificati x.509.
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
ms.openlocfilehash: e4fe5400ffcf4446392015aada031dd4dfbf238a
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/18/2017
---
# <a name="control-access-to-iot-hub"></a><span data-ttu-id="87ba6-104">Controllare l'accesso all'hub IoT</span><span class="sxs-lookup"><span data-stu-id="87ba6-104">Control access to IoT Hub</span></span>

<span data-ttu-id="87ba6-105">Questo articolo illustra le opzioni per la protezione dell'hub IoT.</span><span class="sxs-lookup"><span data-stu-id="87ba6-105">This article describes the options for securing your IoT hub.</span></span> <span data-ttu-id="87ba6-106">L'hub IoT usa le *autorizzazioni* per concedere l'accesso a ogni endpoint dell'hub stesso.</span><span class="sxs-lookup"><span data-stu-id="87ba6-106">IoT Hub uses *permissions* to grant access to each IoT hub endpoint.</span></span> <span data-ttu-id="87ba6-107">Le autorizzazioni limitano l'accesso a un hub IoT in base alla funzionalità.</span><span class="sxs-lookup"><span data-stu-id="87ba6-107">Permissions limit the access to an IoT hub based on functionality.</span></span>

<span data-ttu-id="87ba6-108">L'articolo illustra:</span><span class="sxs-lookup"><span data-stu-id="87ba6-108">This article describes:</span></span>

* <span data-ttu-id="87ba6-109">Le diverse autorizzazioni che è possibile concedere a un'app per dispositivo o back-end per accedere all'hub IoT.</span><span class="sxs-lookup"><span data-stu-id="87ba6-109">The different permissions that you can grant to a device or back-end app to access your IoT hub.</span></span>
* <span data-ttu-id="87ba6-110">Il processo di autenticazione e i token usati per verificare le autorizzazioni.</span><span class="sxs-lookup"><span data-stu-id="87ba6-110">The authentication process and the tokens it uses to verify permissions.</span></span>
* <span data-ttu-id="87ba6-111">Come definire l'ambito delle credenziali per limitare l'accesso a risorse specifiche.</span><span class="sxs-lookup"><span data-stu-id="87ba6-111">How to scope credentials to limit access to specific resources.</span></span>
* <span data-ttu-id="87ba6-112">Supporto dell'hub IoT per i certificati x.509.</span><span class="sxs-lookup"><span data-stu-id="87ba6-112">IoT Hub support for X.509 certificates.</span></span>
* <span data-ttu-id="87ba6-113">Meccanismo di autenticazione personalizzata del dispositivo che usa gli schemi di autenticazione o i registri di identità del dispositivo esistenti.</span><span class="sxs-lookup"><span data-stu-id="87ba6-113">Custom device authentication mechanisms that use existing device identity registries or authentication schemes.</span></span>

### <a name="when-to-use"></a><span data-ttu-id="87ba6-114">Quando usare le autorizzazioni</span><span class="sxs-lookup"><span data-stu-id="87ba6-114">When to use</span></span>

<span data-ttu-id="87ba6-115">È necessario avere le autorizzazioni appropriate per accedere agli endpoint dell'hub IoT.</span><span class="sxs-lookup"><span data-stu-id="87ba6-115">You must have appropriate permissions to access any of the IoT Hub endpoints.</span></span> <span data-ttu-id="87ba6-116">Un dispositivo, ad esempio, deve includere un token contenente le credenziali di sicurezza con ogni messaggio inviato all'hub IoT.</span><span class="sxs-lookup"><span data-stu-id="87ba6-116">For example, a device must include a token containing security credentials along with every message it sends to IoT Hub.</span></span>

## <a name="access-control-and-permissions"></a><span data-ttu-id="87ba6-117">Controllo dell'accesso e autorizzazioni</span><span class="sxs-lookup"><span data-stu-id="87ba6-117">Access control and permissions</span></span>

<span data-ttu-id="87ba6-118">Per concedere le [autorizzazioni](#iot-hub-permissions) è possibile procedere nei modi seguenti:</span><span class="sxs-lookup"><span data-stu-id="87ba6-118">You can grant [permissions](#iot-hub-permissions) in the following ways:</span></span>

* <span data-ttu-id="87ba6-119">**Criteri di accesso condivisi a livello di hub IoT**.</span><span class="sxs-lookup"><span data-stu-id="87ba6-119">**IoT hub-level shared access policies**.</span></span> <span data-ttu-id="87ba6-120">I criteri di accesso condiviso possono concedere qualsiasi combinazione di [autorizzazioni](#iot-hub-permissions).</span><span class="sxs-lookup"><span data-stu-id="87ba6-120">Shared access policies can grant any combination of [permissions](#iot-hub-permissions).</span></span> <span data-ttu-id="87ba6-121">È possibile definire i criteri nel [portale di Azure][lnk-management-portal] o a livello di codice usando le [API REST del provider di risorse dell'hub IoT][lnk-resource-provider-apis].</span><span class="sxs-lookup"><span data-stu-id="87ba6-121">You can define policies in the [Azure portal][lnk-management-portal], or programmatically by using the [IoT Hub resource provider REST APIs][lnk-resource-provider-apis].</span></span> <span data-ttu-id="87ba6-122">Un hub IoT appena creato ha i criteri predefiniti seguenti:</span><span class="sxs-lookup"><span data-stu-id="87ba6-122">A newly created IoT hub has the following default policies:</span></span>

  * <span data-ttu-id="87ba6-123">**iothubowner**: criteri con tutte le autorizzazioni.</span><span class="sxs-lookup"><span data-stu-id="87ba6-123">**iothubowner**: Policy with all permissions.</span></span>
  * <span data-ttu-id="87ba6-124">**service**: criteri con autorizzazione **ServiceConnect**.</span><span class="sxs-lookup"><span data-stu-id="87ba6-124">**service**: Policy with **ServiceConnect** permission.</span></span>
  * <span data-ttu-id="87ba6-125">**device**: criteri con autorizzazione **DeviceConnect**.</span><span class="sxs-lookup"><span data-stu-id="87ba6-125">**device**: Policy with **DeviceConnect** permission.</span></span>
  * <span data-ttu-id="87ba6-126">**registryRead**: criteri con autorizzazione **RegistryRead**.</span><span class="sxs-lookup"><span data-stu-id="87ba6-126">**registryRead**: Policy with **RegistryRead** permission.</span></span>
  * <span data-ttu-id="87ba6-127">**registryReadWrite**: criteri con autorizzazioni **RegistryRead** e RegistryWrite.</span><span class="sxs-lookup"><span data-stu-id="87ba6-127">**registryReadWrite**: Policy with **RegistryRead** and RegistryWrite permissions.</span></span>
  * <span data-ttu-id="87ba6-128">**Credenziali di sicurezza specifiche del dispositivo**.</span><span class="sxs-lookup"><span data-stu-id="87ba6-128">**Per-device security credentials**.</span></span> <span data-ttu-id="87ba6-129">Ogni hub IoT contiene un [registro delle identità][lnk-identity-registry].</span><span class="sxs-lookup"><span data-stu-id="87ba6-129">Each IoT Hub contains an [identity registry][lnk-identity-registry].</span></span> <span data-ttu-id="87ba6-130">Per ogni dispositivo presente in questo registro delle identità è possibile configurare credenziali di sicurezza che concedono autorizzazioni **DeviceConnect** con ambito agli endpoint di dispositivo corrispondenti.</span><span class="sxs-lookup"><span data-stu-id="87ba6-130">For each device in this identity registry, you can configure security credentials that grant **DeviceConnect** permissions scoped to the corresponding device endpoints.</span></span>

<span data-ttu-id="87ba6-131">Ad esempio, in una soluzione IoT tipica:</span><span class="sxs-lookup"><span data-stu-id="87ba6-131">For example, in a typical IoT solution:</span></span>

* <span data-ttu-id="87ba6-132">Il componente di gestione dei dispositivi usa i criteri *registryReadWrite* .</span><span class="sxs-lookup"><span data-stu-id="87ba6-132">The device management component uses the *registryReadWrite* policy.</span></span>
* <span data-ttu-id="87ba6-133">Il componente processore di eventi usa i criteri *service* .</span><span class="sxs-lookup"><span data-stu-id="87ba6-133">The event processor component uses the *service* policy.</span></span>
* <span data-ttu-id="87ba6-134">Il componente della logica di business di runtime del dispositivo usa i criteri *service* .</span><span class="sxs-lookup"><span data-stu-id="87ba6-134">The run-time device business logic component uses the *service* policy.</span></span>
* <span data-ttu-id="87ba6-135">I singoli dispositivi si connettono usando le credenziali archiviate nel registro delle identità dell'hub IoT.</span><span class="sxs-lookup"><span data-stu-id="87ba6-135">Individual devices connect using credentials stored in the IoT hub's identity registry.</span></span>

> [!NOTE]
> <span data-ttu-id="87ba6-136">Per informazioni dettagliate, vedere [Autorizzazioni](#iot-hub-permissions).</span><span class="sxs-lookup"><span data-stu-id="87ba6-136">See [permissions](#iot-hub-permissions) for detailed information.</span></span>

## <a name="authentication"></a><span data-ttu-id="87ba6-137">Authentication</span><span class="sxs-lookup"><span data-stu-id="87ba6-137">Authentication</span></span>

<span data-ttu-id="87ba6-138">L'hub IoT di Azure concede l'accesso agli endpoint tramite la verifica di un token rispetto ai criteri di accesso condiviso e alle credenziali di sicurezza del registro delle identità.</span><span class="sxs-lookup"><span data-stu-id="87ba6-138">Azure IoT Hub grants access to endpoints by verifying a token against the shared access policies and identity registry security credentials.</span></span>

<span data-ttu-id="87ba6-139">Le credenziali di sicurezza, ad esempio le chiavi asimmetriche, non vengono mai trasmesse in rete.</span><span class="sxs-lookup"><span data-stu-id="87ba6-139">Security credentials, such as symmetric keys, are never sent over the wire.</span></span>

> [!NOTE]
> <span data-ttu-id="87ba6-140">Il provider di risorse dell'hub IoT di Azure viene protetto tramite la sottoscrizione di Azure, analogamente a tutti i provider in [Azure Resource Manager][lnk-azure-resource-manager].</span><span class="sxs-lookup"><span data-stu-id="87ba6-140">The Azure IoT Hub resource provider is secured through your Azure subscription, as are all providers in the [Azure Resource Manager][lnk-azure-resource-manager].</span></span>

<span data-ttu-id="87ba6-141">Per altre informazioni sulla creazione e sull'uso di token di sicurezza, vedere [Token di sicurezza dell'hub IoT][lnk-sas-tokens].</span><span class="sxs-lookup"><span data-stu-id="87ba6-141">For more information about how to construct and use security tokens, see [IoT Hub security tokens][lnk-sas-tokens].</span></span>

### <a name="protocol-specifics"></a><span data-ttu-id="87ba6-142">Specifiche del protocollo</span><span class="sxs-lookup"><span data-stu-id="87ba6-142">Protocol specifics</span></span>

<span data-ttu-id="87ba6-143">Ogni protocollo supportato, ad esempio MQTT, AMQP e HTTP, trasporta i token in modo diverso.</span><span class="sxs-lookup"><span data-stu-id="87ba6-143">Each supported protocol, such as MQTT, AMQP, and HTTP, transports tokens in different ways.</span></span>

<span data-ttu-id="87ba6-144">Quando si usa MQTT, il pacchetto CONNECT ha deviceId come valore di ClientId, {iothubhostname}/{deviceId} nel campo Username e un token di firma di accesso condiviso nel campo Password.</span><span class="sxs-lookup"><span data-stu-id="87ba6-144">When using MQTT, the CONNECT packet has the deviceId as the ClientId, {iothubhostname}/{deviceId} in the Username field, and a SAS token in the Password field.</span></span> <span data-ttu-id="87ba6-145">Il valore di {iothubhostname} deve essere il record CName completo dell'hub IoT, ad esempio contoso.azure-devices.net.</span><span class="sxs-lookup"><span data-stu-id="87ba6-145">{iothubhostname} should be the full CName of the IoT hub (for example, contoso.azure-devices.net).</span></span>

<span data-ttu-id="87ba6-146">Quando si usa [AMQP][lnk-amqp], l'hub IoT supporta [SASL PLAIN][lnk-sasl-plain] e la [sicurezza basata sulle attestazioni AMQP][lnk-cbs].</span><span class="sxs-lookup"><span data-stu-id="87ba6-146">When using [AMQP][lnk-amqp], IoT Hub supports [SASL PLAIN][lnk-sasl-plain] and [AMQP Claims-Based-Security][lnk-cbs].</span></span>

<span data-ttu-id="87ba6-147">Se si usa la sicurezza basata sulle attestazioni AMQP, lo standard specifica come trasmettere questi token.</span><span class="sxs-lookup"><span data-stu-id="87ba6-147">If you use AMQP claims-based-security, the standard specifies how to transmit these tokens.</span></span>

<span data-ttu-id="87ba6-148">Per SASL PLAIN **username** può essere:</span><span class="sxs-lookup"><span data-stu-id="87ba6-148">For SASL PLAIN, the **username** can be:</span></span>

* <span data-ttu-id="87ba6-149">`{policyName}@sas.root.{iothubName}` nel caso di token a livello di hub IoT.</span><span class="sxs-lookup"><span data-stu-id="87ba6-149">`{policyName}@sas.root.{iothubName}` if using IoT hub-level tokens.</span></span>
* <span data-ttu-id="87ba6-150">`{deviceId}@sas.{iothubname}` ne caso di token con ambito relativo al dispositivo.</span><span class="sxs-lookup"><span data-stu-id="87ba6-150">`{deviceId}@sas.{iothubname}` if using device-scoped tokens.</span></span>

<span data-ttu-id="87ba6-151">In entrambi i casi, il campo della password contiene il token, come descritto in [Token di sicurezza dell'hub IoT][lnk-sas-tokens].</span><span class="sxs-lookup"><span data-stu-id="87ba6-151">In both cases, the password field contains the token, as described in [IoT Hub security tokens][lnk-sas-tokens].</span></span>

<span data-ttu-id="87ba6-152">Il protocollo HTTP implementa l'autenticazione includendo un token valido nell'intestazione della richiesta **Authorization** .</span><span class="sxs-lookup"><span data-stu-id="87ba6-152">HTTP implements authentication by including a valid token in the **Authorization** request header.</span></span>

#### <a name="example"></a><span data-ttu-id="87ba6-153">Esempio</span><span class="sxs-lookup"><span data-stu-id="87ba6-153">Example</span></span>

<span data-ttu-id="87ba6-154">Nome utente (per DeviceId viene fatta distinzione tra maiuscole e minuscole): `iothubname.azure-devices.net/DeviceId`</span><span class="sxs-lookup"><span data-stu-id="87ba6-154">Username (DeviceId is case-sensitive): `iothubname.azure-devices.net/DeviceId`</span></span>

<span data-ttu-id="87ba6-155">Password (generare il token di firma di accesso condiviso con lo strumento [Device Explorer][lnk-device-explorer]): `SharedAccessSignature sr=iothubname.azure-devices.net%2fdevices%2fDeviceId&sig=kPszxZZZZZZZZZZZZZZZZZAhLT%2bV7o%3d&se=1487709501`</span><span class="sxs-lookup"><span data-stu-id="87ba6-155">Password (Generate SAS token with the [device explorer][lnk-device-explorer] tool): `SharedAccessSignature sr=iothubname.azure-devices.net%2fdevices%2fDeviceId&sig=kPszxZZZZZZZZZZZZZZZZZAhLT%2bV7o%3d&se=1487709501`</span></span>

> [!NOTE]
> <span data-ttu-id="87ba6-156">Gli [Azure IoT SDK][lnk-sdks] generano automaticamente i token durante la connessione al servizio.</span><span class="sxs-lookup"><span data-stu-id="87ba6-156">The [Azure IoT SDKs][lnk-sdks] automatically generate tokens when connecting to the service.</span></span> <span data-ttu-id="87ba6-157">In alcuni casi, gli Azure IoT SDK non supportano tutti i protocolli o tutti i metodi di autenticazione.</span><span class="sxs-lookup"><span data-stu-id="87ba6-157">In some cases, the Azure IoT SDKs do not support all the protocols or all the authentication methods.</span></span>

### <a name="special-considerations-for-sasl-plain"></a><span data-ttu-id="87ba6-158">Considerazioni speciali su SASL PLAIN</span><span class="sxs-lookup"><span data-stu-id="87ba6-158">Special considerations for SASL PLAIN</span></span>

<span data-ttu-id="87ba6-159">Quando si usa SASL PLAIN con AMQP, un client che si connette a un hub IoT potrà usare un singolo token per ogni connessione TCP.</span><span class="sxs-lookup"><span data-stu-id="87ba6-159">When using SASL PLAIN with AMQP, a client connecting to an IoT hub can use a single token for each TCP connection.</span></span> <span data-ttu-id="87ba6-160">Quando il token scade, la connessione TCP si disconnette dal servizio e attiva una riconnessione.</span><span class="sxs-lookup"><span data-stu-id="87ba6-160">When the token expires, the TCP connection disconnects from the service and triggers a reconnect.</span></span> <span data-ttu-id="87ba6-161">Questo comportamento non genera problemi per un'app back-end, ma è dannoso per un'app per dispositivi per i motivi seguenti:</span><span class="sxs-lookup"><span data-stu-id="87ba6-161">This behavior, while not problematic for a back-end app, is damaging for a device app for the following reasons:</span></span>

* <span data-ttu-id="87ba6-162">I gateway si connettono in genere per conto di molti dispositivi.</span><span class="sxs-lookup"><span data-stu-id="87ba6-162">Gateways usually connect on behalf of many devices.</span></span> <span data-ttu-id="87ba6-163">Quando si usa SASL PLAIN, devono creare una connessione TCP distinta per ogni dispositivo che si connette a un hub IoT.</span><span class="sxs-lookup"><span data-stu-id="87ba6-163">When using SASL PLAIN, they have to create a distinct TCP connection for each device connecting to an IoT hub.</span></span> <span data-ttu-id="87ba6-164">Questo scenario aumenta in modo considerevole il consumo energetico e delle risorse di rete e incrementa la latenza della connessione di ogni dispositivo.</span><span class="sxs-lookup"><span data-stu-id="87ba6-164">This scenario considerably increases the consumption of power and networking resources, and increases the latency of each device connection.</span></span>
* <span data-ttu-id="87ba6-165">L'aumento dell'uso delle risorse per la riconnessione dopo la scadenza di ogni token influisce negativamente sui dispositivi vincolati alle risorse.</span><span class="sxs-lookup"><span data-stu-id="87ba6-165">Resource-constrained devices are adversely affected by the increased use of resources to reconnect after each token expiration.</span></span>

## <a name="scope-iot-hub-level-credentials"></a><span data-ttu-id="87ba6-166">Definire l'ambito delle credenziali a livello di hub IoT</span><span class="sxs-lookup"><span data-stu-id="87ba6-166">Scope IoT hub-level credentials</span></span>

<span data-ttu-id="87ba6-167">È possibile definire l'ambito dei criteri di sicurezza a livello di hub IoT creando token con URI di risorsa con limitazioni.</span><span class="sxs-lookup"><span data-stu-id="87ba6-167">You can scope IoT hub-level security policies by creating tokens with a restricted resource URI.</span></span> <span data-ttu-id="87ba6-168">L'endpoint per l'invio di messaggi da dispositivo a cloud da un dispositivo, ad esempio, è **/devices/{deviceId}/messages/events**.</span><span class="sxs-lookup"><span data-stu-id="87ba6-168">For example, the endpoint to send device-to-cloud messages from a device is **/devices/{deviceId}/messages/events**.</span></span> <span data-ttu-id="87ba6-169">È anche possibile usare criteri di accesso condiviso a livello di hub IoT con autorizzazioni **DeviceConnect** per firmare un token il cui valore resourceURI è **/devices/{deviceId}**.</span><span class="sxs-lookup"><span data-stu-id="87ba6-169">You can also use an IoT hub-level shared access policy with **DeviceConnect** permissions to sign a token whose resourceURI is **/devices/{deviceId}**.</span></span> <span data-ttu-id="87ba6-170">Questo approccio crea un token che può essere usato solo per l'invio di messaggi per conto del dispositivo **deviceId**.</span><span class="sxs-lookup"><span data-stu-id="87ba6-170">This approach creates a token that is only usable to send messages on behalf of device **deviceId**.</span></span>

<span data-ttu-id="87ba6-171">Questo meccanismo è simile ai [criteri dell'entità di pubblicazione di Hub eventi][lnk-event-hubs-publisher-policy] e consente di implementare metodi di autenticazione personalizzati.</span><span class="sxs-lookup"><span data-stu-id="87ba6-171">This mechanism is similar to the [Event Hubs publisher policy][lnk-event-hubs-publisher-policy], and enables you to implement custom authentication methods.</span></span>

## <a name="security-tokens"></a><span data-ttu-id="87ba6-172">Token di sicurezza</span><span class="sxs-lookup"><span data-stu-id="87ba6-172">Security tokens</span></span>

<span data-ttu-id="87ba6-173">Hub IoT usa i token di sicurezza per autenticare i dispositivi e i servizi ed evitare l'invio in rete delle chiavi.</span><span class="sxs-lookup"><span data-stu-id="87ba6-173">IoT Hub uses security tokens to authenticate devices and services to avoid sending keys on the wire.</span></span> <span data-ttu-id="87ba6-174">Inoltre, i token di sicurezza hanno una validità limitata in termini di tempo e portata.</span><span class="sxs-lookup"><span data-stu-id="87ba6-174">Additionally, security tokens are limited in time validity and scope.</span></span> <span data-ttu-id="87ba6-175">Gli [Azure IoT SDK][lnk-sdks] generano automaticamente i token senza richiedere una configurazione speciale.</span><span class="sxs-lookup"><span data-stu-id="87ba6-175">[Azure IoT SDKs][lnk-sdks] automatically generate tokens without requiring any special configuration.</span></span> <span data-ttu-id="87ba6-176">In alcuni scenari è necessario generare e usare direttamente i token di sicurezza.</span><span class="sxs-lookup"><span data-stu-id="87ba6-176">Some scenarios do require you to generate and use security tokens directly.</span></span> <span data-ttu-id="87ba6-177">Tali scenari includono:</span><span class="sxs-lookup"><span data-stu-id="87ba6-177">Such scenarios include:</span></span>

* <span data-ttu-id="87ba6-178">L'uso diretto di superfici MQTT, AMQP o HTTP.</span><span class="sxs-lookup"><span data-stu-id="87ba6-178">The direct use of the MQTT, AMQP, or HTTP surfaces.</span></span>
* <span data-ttu-id="87ba6-179">L'implementazione del modello di servizio token, come descritto in [Autenticazione personalizzata del dispositivo][lnk-custom-auth].</span><span class="sxs-lookup"><span data-stu-id="87ba6-179">The implementation of the token service pattern, as explained in [Custom device authentication][lnk-custom-auth].</span></span>

<span data-ttu-id="87ba6-180">Hub IoT consente ai dispositivi di autenticarsi con l'hub IoT usando [certificati X.509][lnk-x509].</span><span class="sxs-lookup"><span data-stu-id="87ba6-180">IoT Hub also allows devices to authenticate with IoT Hub using [X.509 certificates][lnk-x509].</span></span>

### <a name="security-token-structure"></a><span data-ttu-id="87ba6-181">Formato del token di sicurezza</span><span class="sxs-lookup"><span data-stu-id="87ba6-181">Security token structure</span></span>

<span data-ttu-id="87ba6-182">I token di sicurezza consentono di concedere a dispositivi e servizi l'accesso con limite temporale a funzionalità specifiche dell'hub IoT.</span><span class="sxs-lookup"><span data-stu-id="87ba6-182">You use security tokens to grant time-bounded access to devices and services to specific functionality in IoT Hub.</span></span> <span data-ttu-id="87ba6-183">Per ottenere l'autorizzazione per connettersi all'hub IoT, i dispositivi e i servizi devono inviare i token di sicurezza firmati con una chiave di accesso condiviso o una chiave simmetrica.</span><span class="sxs-lookup"><span data-stu-id="87ba6-183">To get authorization to connect to IoT Hub, devices and services must send security tokens signed with either a shared access or symmetric key.</span></span> <span data-ttu-id="87ba6-184">Tali chiavi vengono archiviate con un'identità del dispositivo nel registro delle identità.</span><span class="sxs-lookup"><span data-stu-id="87ba6-184">These keys are stored with a device identity in the identity registry.</span></span>

<span data-ttu-id="87ba6-185">Un token firmato con una chiave di accesso condiviso concede l'accesso a tutte le funzionalità associate alle autorizzazioni dei criteri di accesso condiviso.</span><span class="sxs-lookup"><span data-stu-id="87ba6-185">A token signed with a shared access key grants access to all the functionality associated with the shared access policy permissions.</span></span> <span data-ttu-id="87ba6-186">Un token firmato con una chiave simmetrica dell'identità dispositivo concede solo l'autorizzazione **DeviceConnect** per l'identità del dispositivo associato.</span><span class="sxs-lookup"><span data-stu-id="87ba6-186">A token signed with a device identity's symmetric key only grants the **DeviceConnect** permission for the associated device identity.</span></span>

<span data-ttu-id="87ba6-187">Il token di sicurezza ha il formato seguente:</span><span class="sxs-lookup"><span data-stu-id="87ba6-187">The security token has the following format:</span></span>

`SharedAccessSignature sig={signature-string}&se={expiry}&skn={policyName}&sr={URL-encoded-resourceURI}`

<span data-ttu-id="87ba6-188">I valori previsti sono i seguenti:</span><span class="sxs-lookup"><span data-stu-id="87ba6-188">Here are the expected values:</span></span>

| <span data-ttu-id="87ba6-189">Valore</span><span class="sxs-lookup"><span data-stu-id="87ba6-189">Value</span></span> | <span data-ttu-id="87ba6-190">Descrizione</span><span class="sxs-lookup"><span data-stu-id="87ba6-190">Description</span></span> |
| --- | --- |
| <span data-ttu-id="87ba6-191">{signature}</span><span class="sxs-lookup"><span data-stu-id="87ba6-191">{signature}</span></span> |<span data-ttu-id="87ba6-192">Stringa della firma HMAC-SHA256 nel formato: `{URL-encoded-resourceURI} + "\n" + expiry`.</span><span class="sxs-lookup"><span data-stu-id="87ba6-192">An HMAC-SHA256 signature string of the form: `{URL-encoded-resourceURI} + "\n" + expiry`.</span></span> <span data-ttu-id="87ba6-193">**Importante**: la chiave viene decodificata dalla codifica Base64 e usata come chiave per eseguire il calcolo di HMAC-SHA256.</span><span class="sxs-lookup"><span data-stu-id="87ba6-193">**Important**: The key is decoded from base64 and used as key to perform the HMAC-SHA256 computation.</span></span> |
| <span data-ttu-id="87ba6-194">{resourceURI}</span><span class="sxs-lookup"><span data-stu-id="87ba6-194">{resourceURI}</span></span> |<span data-ttu-id="87ba6-195">Prefisso URI (per segmento) degli endpoint a cui è possibile accedere tramite questo token e che inizia con il nome host dell'hub IoT senza il protocollo.</span><span class="sxs-lookup"><span data-stu-id="87ba6-195">URI prefix (by segment) of the endpoints that can be accessed with this token, starting with host name of the IoT hub (no protocol).</span></span> <span data-ttu-id="87ba6-196">Ad esempio: `myHub.azure-devices.net/devices/device1`</span><span class="sxs-lookup"><span data-stu-id="87ba6-196">For example, `myHub.azure-devices.net/devices/device1`</span></span> |
| <span data-ttu-id="87ba6-197">{expiry}</span><span class="sxs-lookup"><span data-stu-id="87ba6-197">{expiry}</span></span> |<span data-ttu-id="87ba6-198">Stringhe UTF8 per il numero di secondi trascorsi dalle 00:00:00 UTC dell'1 gennaio 1970.</span><span class="sxs-lookup"><span data-stu-id="87ba6-198">UTF8 strings for number of seconds since the epoch 00:00:00 UTC on 1 January 1970.</span></span> |
| <span data-ttu-id="87ba6-199">{URL-encoded-resourceURI}</span><span class="sxs-lookup"><span data-stu-id="87ba6-199">{URL-encoded-resourceURI}</span></span> |<span data-ttu-id="87ba6-200">Codifica URL con lettere minuscole dell'URI della risorsa con lettere minuscole</span><span class="sxs-lookup"><span data-stu-id="87ba6-200">Lower case URL-encoding of the lower case resource URI</span></span> |
| <span data-ttu-id="87ba6-201">{policyName}</span><span class="sxs-lookup"><span data-stu-id="87ba6-201">{policyName}</span></span> |<span data-ttu-id="87ba6-202">Nome del criterio di accesso condiviso a cui fa riferimento il token.</span><span class="sxs-lookup"><span data-stu-id="87ba6-202">The name of the shared access policy to which this token refers.</span></span> <span data-ttu-id="87ba6-203">Assente se il token fa riferimento a credenziali del registro dei dispositivi.</span><span class="sxs-lookup"><span data-stu-id="87ba6-203">Absent if the token refers to device-registry credentials.</span></span> |

<span data-ttu-id="87ba6-204">**Nota sul prefisso**: il prefisso dell'URI viene calcolato in base al segmento e non in base al carattere.</span><span class="sxs-lookup"><span data-stu-id="87ba6-204">**Note on prefix**: The URI prefix is computed by segment and not by character.</span></span> <span data-ttu-id="87ba6-205">Ad esempio `/a/b` è un prefisso per `/a/b/c` ma non per `/a/bc`.</span><span class="sxs-lookup"><span data-stu-id="87ba6-205">For example `/a/b` is a prefix for `/a/b/c` but not for `/a/bc`.</span></span>

<span data-ttu-id="87ba6-206">Il frammento seguente di Node.js mostra una funzione denominata **generateSasToken** che calcola il token dagli input `resourceUri, signingKey, policyName, expiresInMins`.</span><span class="sxs-lookup"><span data-stu-id="87ba6-206">The following Node.js snippet shows a function called **generateSasToken** that computes the token from the inputs `resourceUri, signingKey, policyName, expiresInMins`.</span></span> <span data-ttu-id="87ba6-207">Nelle sezioni successive viene illustrato nel dettaglio come inizializzare gli input a seconda del caso d'uso.</span><span class="sxs-lookup"><span data-stu-id="87ba6-207">The next sections detail how to initialize the different inputs for the different token use cases.</span></span>

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

<span data-ttu-id="87ba6-208">Per fare un confronto, l'equivalente in termini di codice Python per generare un token di sicurezza è:</span><span class="sxs-lookup"><span data-stu-id="87ba6-208">As a comparison, the equivalent Python code to generate a security token is:</span></span>

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
> <span data-ttu-id="87ba6-209">Poiché la validità temporale del token viene verificata sui computer hub IoT, lo sfasamento dell'orologio del computer che genera il token deve essere minimo.</span><span class="sxs-lookup"><span data-stu-id="87ba6-209">Since the time validity of the token is validated on IoT Hub machines, the drift on the clock of the machine that generates the token must be minimal.</span></span>

### <a name="use-sas-tokens-in-a-device-app"></a><span data-ttu-id="87ba6-210">Usare i token di firma di accesso condiviso in un dispositivo client</span><span class="sxs-lookup"><span data-stu-id="87ba6-210">Use SAS tokens in a device app</span></span>

<span data-ttu-id="87ba6-211">Esistono due modi per ottenere le autorizzazioni **DeviceConnect** con l'hub IoT con i token di sicurezza: usare una [chiave del dispositivo simmetrica dal registro delle identità](#use-a-symmetric-key-in-the-identity-registry) oppure usare una [chiave di accesso condiviso](#use-a-shared-access-policy).</span><span class="sxs-lookup"><span data-stu-id="87ba6-211">There are two ways to obtain **DeviceConnect** permissions with IoT Hub with security tokens: use a [symmetric device key from the identity registry](#use-a-symmetric-key-in-the-identity-registry), or use a [shared access key](#use-a-shared-access-policy).</span></span>

<span data-ttu-id="87ba6-212">Tenere presente che, per impostazione predefinita, tutte le funzionalità accessibili dai dispositivi vengono esposte negli endpoint con il prefisso `/devices/{deviceId}`.</span><span class="sxs-lookup"><span data-stu-id="87ba6-212">Remember that all functionality accessible from devices is exposed by design on endpoints with prefix `/devices/{deviceId}`.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="87ba6-213">L'unico modo di cui dispone l'hub IoT per autenticare un dispositivo specifico è tramite la chiave simmetrica identità dispositivo.</span><span class="sxs-lookup"><span data-stu-id="87ba6-213">The only way that IoT Hub authenticates a specific device is using the device identity symmetric key.</span></span> <span data-ttu-id="87ba6-214">Nei casi in cui si acceda alle funzionalità del dispositivo tramite criteri di accesso condiviso, la soluzione deve considerare il componente che emette il token di sicurezza come sottocomponente attendibile.</span><span class="sxs-lookup"><span data-stu-id="87ba6-214">In cases when a shared access policy is used to access device functionality, the solution must consider the component issuing the security token as a trusted subcomponent.</span></span>

<span data-ttu-id="87ba6-215">Gli endpoint per il dispositivo sono, indipendentemente dal protocollo:</span><span class="sxs-lookup"><span data-stu-id="87ba6-215">The device-facing endpoints are (irrespective of the protocol):</span></span>

| <span data-ttu-id="87ba6-216">Endpoint</span><span class="sxs-lookup"><span data-stu-id="87ba6-216">Endpoint</span></span> | <span data-ttu-id="87ba6-217">Funzionalità</span><span class="sxs-lookup"><span data-stu-id="87ba6-217">Functionality</span></span> |
| --- | --- |
| `{iot hub host name}/devices/{deviceId}/messages/events` |<span data-ttu-id="87ba6-218">Invio di messaggi da dispositivo a cloud.</span><span class="sxs-lookup"><span data-stu-id="87ba6-218">Send device-to-cloud messages.</span></span> |
| `{iot hub host name}/devices/{deviceId}/devicebound` |<span data-ttu-id="87ba6-219">Ricezione di messaggi da cloud a dispositivo.</span><span class="sxs-lookup"><span data-stu-id="87ba6-219">Receive cloud-to-device messages.</span></span> |

### <a name="use-a-symmetric-key-in-the-identity-registry"></a><span data-ttu-id="87ba6-220">Usare una chiave simmetrica nel registro identità</span><span class="sxs-lookup"><span data-stu-id="87ba6-220">Use a symmetric key in the identity registry</span></span>

<span data-ttu-id="87ba6-221">Quando si usa una chiave simmetrica dell'identità del dispositivo per generare un token, l'elemento policyName (`skn`) del token viene omesso.</span><span class="sxs-lookup"><span data-stu-id="87ba6-221">When using a device identity's symmetric key to generate a token, the policyName (`skn`) element of the token is omitted.</span></span>

<span data-ttu-id="87ba6-222">Ad esempio, un token creato per accedere a tutte le funzionalità del dispositivo deve avere i seguenti parametri:</span><span class="sxs-lookup"><span data-stu-id="87ba6-222">For example, a token created to access all device functionality should have the following parameters:</span></span>

* <span data-ttu-id="87ba6-223">URI della risorsa: `{IoT hub name}.azure-devices.net/devices/{device id}`,</span><span class="sxs-lookup"><span data-stu-id="87ba6-223">resource URI: `{IoT hub name}.azure-devices.net/devices/{device id}`,</span></span>
* <span data-ttu-id="87ba6-224">Chiave di firma: qualsiasi chiave simmetrica per l'identità `{device id}` ,</span><span class="sxs-lookup"><span data-stu-id="87ba6-224">signing key: any symmetric key for the `{device id}` identity,</span></span>
* <span data-ttu-id="87ba6-225">Nessun nome di criterio,</span><span class="sxs-lookup"><span data-stu-id="87ba6-225">no policy name,</span></span>
* <span data-ttu-id="87ba6-226">Qualsiasi ora di scadenza.</span><span class="sxs-lookup"><span data-stu-id="87ba6-226">any expiration time.</span></span>

<span data-ttu-id="87ba6-227">Un esempio di uso della funzione di Node.js precedente sarebbe il seguente:</span><span class="sxs-lookup"><span data-stu-id="87ba6-227">An example using the preceding Node.js function would be:</span></span>

```nodejs
var endpoint ="myhub.azure-devices.net/devices/device1";
var deviceKey ="...";

var token = generateSasToken(endpoint, deviceKey, null, 60);
```

<span data-ttu-id="87ba6-228">Il risultato, che concede l'accesso a tutte le funzionalità per device1, sarà:</span><span class="sxs-lookup"><span data-stu-id="87ba6-228">The result, which grants access to all functionality for device1, would be:</span></span>

`SharedAccessSignature sr=myhub.azure-devices.net%2fdevices%2fdevice1&sig=13y8ejUk2z7PLmvtwR5RqlGBOVwiq7rQR3WZ5xZX3N4%3D&se=1456971697`

> [!NOTE]
> <span data-ttu-id="87ba6-229">È possibile generare un token SAS con lo strumento [Esplora dispositivi][lnk-device-explorer] di .NET o tramite l'utilità da riga di comando [iothub-explorer][lnk-iothub-explorer], multipiattaforma e basata su nodi.</span><span class="sxs-lookup"><span data-stu-id="87ba6-229">It is possible to generate a SAS token using the .NET [device explorer][lnk-device-explorer] tool or the cross-platform, node-based [iothub-explorer][lnk-iothub-explorer] command-line utility.</span></span>

### <a name="use-a-shared-access-policy"></a><span data-ttu-id="87ba6-230">Usare criteri di accesso condiviso</span><span class="sxs-lookup"><span data-stu-id="87ba6-230">Use a shared access policy</span></span>

<span data-ttu-id="87ba6-231">Quando si crea un token da criteri di accesso condiviso, impostare il campo `skn` sul nome dei criteri.</span><span class="sxs-lookup"><span data-stu-id="87ba6-231">When you create a token from a shared access policy, set the `skn` field to the name of the policy.</span></span> <span data-ttu-id="87ba6-232">Questi criteri devono concedere l'autorizzazione **DeviceConnect**.</span><span class="sxs-lookup"><span data-stu-id="87ba6-232">This policy must grant the **DeviceConnect** permission.</span></span>

<span data-ttu-id="87ba6-233">I due scenari principali per l'uso di criteri di accesso condiviso per accedere alla funzionalità dei dispositivi sono:</span><span class="sxs-lookup"><span data-stu-id="87ba6-233">The two main scenarios for using shared access policies to access device functionality are:</span></span>

* <span data-ttu-id="87ba6-234">[gateway del protocollo cloud][lnk-endpoints],</span><span class="sxs-lookup"><span data-stu-id="87ba6-234">[cloud protocol gateways][lnk-endpoints],</span></span>
* <span data-ttu-id="87ba6-235">[servizi token][lnk-custom-auth] tramite i quali implementare schemi di autenticazione personalizzati.</span><span class="sxs-lookup"><span data-stu-id="87ba6-235">[token services][lnk-custom-auth] used to implement custom authentication schemes.</span></span>

<span data-ttu-id="87ba6-236">Poiché i criteri di accesso condiviso possono potenzialmente autorizzare la connessione a qualsiasi dispositivo, in fase di creazione dei token di sicurezza è importante usare l'URI risorsa corretto.</span><span class="sxs-lookup"><span data-stu-id="87ba6-236">Since the shared access policy can potentially grant access to connect as any device, it is important to use the correct resource URI when creating security tokens.</span></span> <span data-ttu-id="87ba6-237">Questa impostazione è particolarmente importante per i servizi token, che devono limitare l'ambito del token a un dispositivo specifico usando l'URI risorsa.</span><span class="sxs-lookup"><span data-stu-id="87ba6-237">This setting is especially important for token services, which have to scope the token to a specific device using the resource URI.</span></span> <span data-ttu-id="87ba6-238">Questo punto è meno importante per i gateway di protocollo, in quanto già filtrano il traffico per tutti i dispositivi.</span><span class="sxs-lookup"><span data-stu-id="87ba6-238">This point is less relevant for protocol gateways as they are already mediating traffic for all devices.</span></span>

<span data-ttu-id="87ba6-239">Ad esempio, un servizio token che usa il criterio di accesso condiviso già esistente denominato **device** creerebbe un token con i parametri seguenti:</span><span class="sxs-lookup"><span data-stu-id="87ba6-239">As an example, a token service using the pre-created shared access policy called **device** would create a token with the following parameters:</span></span>

* <span data-ttu-id="87ba6-240">URI della risorsa: `{IoT hub name}.azure-devices.net/devices/{device id}`,</span><span class="sxs-lookup"><span data-stu-id="87ba6-240">resource URI: `{IoT hub name}.azure-devices.net/devices/{device id}`,</span></span>
* <span data-ttu-id="87ba6-241">chiave di firma: una delle chiavi del criterio `device` ,</span><span class="sxs-lookup"><span data-stu-id="87ba6-241">signing key: one of the keys of the `device` policy,</span></span>
* <span data-ttu-id="87ba6-242">nome criterio: `device`,</span><span class="sxs-lookup"><span data-stu-id="87ba6-242">policy name: `device`,</span></span>
* <span data-ttu-id="87ba6-243">Qualsiasi ora di scadenza.</span><span class="sxs-lookup"><span data-stu-id="87ba6-243">any expiration time.</span></span>

<span data-ttu-id="87ba6-244">Un esempio di uso della funzione di Node.js precedente sarebbe il seguente:</span><span class="sxs-lookup"><span data-stu-id="87ba6-244">An example using the preceding Node.js function would be:</span></span>

```nodejs
var endpoint ="myhub.azure-devices.net/devices/device1";
var policyName = 'device';
var policyKey = '...';

var token = generateSasToken(endpoint, policyKey, policyName, 60);
```

<span data-ttu-id="87ba6-245">Il risultato, che concede l'accesso a tutte le funzionalità per device1, sarà:</span><span class="sxs-lookup"><span data-stu-id="87ba6-245">The result, which grants access to all functionality for device1, would be:</span></span>

`SharedAccessSignature sr=myhub.azure-devices.net%2fdevices%2fdevice1&sig=13y8ejUk2z7PLmvtwR5RqlGBOVwiq7rQR3WZ5xZX3N4%3D&se=1456971697&skn=device`

<span data-ttu-id="87ba6-246">Un gateway di protocollo potrebbe usare lo stesso token per tutti i dispositivi semplicemente impostando l'URI della risorsa su `myhub.azure-devices.net/devices`.</span><span class="sxs-lookup"><span data-stu-id="87ba6-246">A protocol gateway could use the same token for all devices simply setting the resource URI to `myhub.azure-devices.net/devices`.</span></span>

### <a name="use-security-tokens-from-service-components"></a><span data-ttu-id="87ba6-247">Usare token di sicurezza da componenti del servizio</span><span class="sxs-lookup"><span data-stu-id="87ba6-247">Use security tokens from service components</span></span>

<span data-ttu-id="87ba6-248">I componenti del servizio possono generare token di sicurezza solo usando criteri di accesso condiviso che concedono le autorizzazioni appropriate, come illustrato prima.</span><span class="sxs-lookup"><span data-stu-id="87ba6-248">Service components can only generate security tokens using shared access policies granting the appropriate permissions as explained previously.</span></span>

<span data-ttu-id="87ba6-249">Di seguito vengono indicate le funzioni del servizio esposte sugli endpoint:</span><span class="sxs-lookup"><span data-stu-id="87ba6-249">Here is the service functions exposed on the endpoints:</span></span>

| <span data-ttu-id="87ba6-250">Endpoint</span><span class="sxs-lookup"><span data-stu-id="87ba6-250">Endpoint</span></span> | <span data-ttu-id="87ba6-251">Funzionalità</span><span class="sxs-lookup"><span data-stu-id="87ba6-251">Functionality</span></span> |
| --- | --- |
| `{iot hub host name}/devices` |<span data-ttu-id="87ba6-252">Creazione, aggiornamento, recupero ed eliminazione delle identità dispositivo.</span><span class="sxs-lookup"><span data-stu-id="87ba6-252">Create, update, retrieve, and delete device identities.</span></span> |
| `{iot hub host name}/messages/events` |<span data-ttu-id="87ba6-253">Ricezione di messaggi da dispositivo a cloud.</span><span class="sxs-lookup"><span data-stu-id="87ba6-253">Receive device-to-cloud messages.</span></span> |
| `{iot hub host name}/servicebound/feedback` |<span data-ttu-id="87ba6-254">Ricezione di feedback per messaggi da cloud a dispositivo.</span><span class="sxs-lookup"><span data-stu-id="87ba6-254">Receive feedback for cloud-to-device messages.</span></span> |
| `{iot hub host name}/devicebound` |<span data-ttu-id="87ba6-255">Invio di messaggi da cloud a dispositivo.</span><span class="sxs-lookup"><span data-stu-id="87ba6-255">Send cloud-to-device messages.</span></span> |

<span data-ttu-id="87ba6-256">Ad esempio, un servizio che usa il criterio di accesso condiviso già esistente denominato **registryRead** creerebbe un token con i parametri seguenti:</span><span class="sxs-lookup"><span data-stu-id="87ba6-256">As an example, a service generating using the pre-created shared access policy called **registryRead** would create a token with the following parameters:</span></span>

* <span data-ttu-id="87ba6-257">URI della risorsa: `{IoT hub name}.azure-devices.net/devices`,</span><span class="sxs-lookup"><span data-stu-id="87ba6-257">resource URI: `{IoT hub name}.azure-devices.net/devices`,</span></span>
* <span data-ttu-id="87ba6-258">chiave di firma: una delle chiavi del criterio `registryRead` ,</span><span class="sxs-lookup"><span data-stu-id="87ba6-258">signing key: one of the keys of the `registryRead` policy,</span></span>
* <span data-ttu-id="87ba6-259">nome criterio: `registryRead`,</span><span class="sxs-lookup"><span data-stu-id="87ba6-259">policy name: `registryRead`,</span></span>
* <span data-ttu-id="87ba6-260">Qualsiasi ora di scadenza.</span><span class="sxs-lookup"><span data-stu-id="87ba6-260">any expiration time.</span></span>

```nodejs
var endpoint ="myhub.azure-devices.net/devices";
var policyName = 'device';
var policyKey = '...';

var token = generateSasToken(endpoint, policyKey, policyName, 60);
```

<span data-ttu-id="87ba6-261">Il risultato, che concede l'accesso in lettura a tutte le identità dispositivo, sarà:</span><span class="sxs-lookup"><span data-stu-id="87ba6-261">The result, which would grant access to read all device identities, would be:</span></span>

`SharedAccessSignature sr=myhub.azure-devices.net%2fdevices&sig=JdyscqTpXdEJs49elIUCcohw2DlFDR3zfH5KqGJo4r4%3D&se=1456973447&skn=registryRead`

## <a name="supported-x509-certificates"></a><span data-ttu-id="87ba6-262">Certificati X.509 supportati</span><span class="sxs-lookup"><span data-stu-id="87ba6-262">Supported X.509 certificates</span></span>

<span data-ttu-id="87ba6-263">È possibile usare qualsiasi certificato X.509 per autenticare un dispositivo con hub IoT.</span><span class="sxs-lookup"><span data-stu-id="87ba6-263">You can use any X.509 certificate to authenticate a device with IoT Hub.</span></span> <span data-ttu-id="87ba6-264">I certificati inclusi sono i seguenti:</span><span class="sxs-lookup"><span data-stu-id="87ba6-264">Certificates include:</span></span>

* <span data-ttu-id="87ba6-265">**Un certificato X.509 esistente**.</span><span class="sxs-lookup"><span data-stu-id="87ba6-265">**An existing X.509 certificate**.</span></span> <span data-ttu-id="87ba6-266">Un dispositivo potrebbe già avere un certificato X.509 associato.</span><span class="sxs-lookup"><span data-stu-id="87ba6-266">A device may already have an X.509 certificate associated with it.</span></span> <span data-ttu-id="87ba6-267">Il dispositivo può usare questo certificato per autenticarsi con hub IoT.</span><span class="sxs-lookup"><span data-stu-id="87ba6-267">The device can use this certificate to authenticate with IoT Hub.</span></span>
* <span data-ttu-id="87ba6-268">**Un certificato X-509 auto-generato e auto-firmato**.</span><span class="sxs-lookup"><span data-stu-id="87ba6-268">**A self-generated and self-signed X-509 certificate**.</span></span> <span data-ttu-id="87ba6-269">Un produttore di dispositivi o un distributore interno può generare questi certificati e archiviare la chiave privata corrispondente (e il certificato) nel dispositivo.</span><span class="sxs-lookup"><span data-stu-id="87ba6-269">A device manufacturer or in-house deployer can generate these certificates and store the corresponding private key (and certificate) on the device.</span></span> <span data-ttu-id="87ba6-270">È possibile usare strumenti come [OpenSSL][lnk-openssl] e l'utilità [Windows SelfSignedCertificate][lnk-selfsigned] per questo scopo.</span><span class="sxs-lookup"><span data-stu-id="87ba6-270">You can use tools such as [OpenSSL][lnk-openssl] and [Windows SelfSignedCertificate][lnk-selfsigned] utility for this purpose.</span></span>
* <span data-ttu-id="87ba6-271">**Certificato X.509 firmato da un'autorità di certificazione**.</span><span class="sxs-lookup"><span data-stu-id="87ba6-271">**CA-signed X.509 certificate**.</span></span> <span data-ttu-id="87ba6-272">Per identificare un dispositivo e autenticarlo con l'hub IoT, è possibile usare un certificato X.509 generato e firmato da un'autorità di certificazione (CA).</span><span class="sxs-lookup"><span data-stu-id="87ba6-272">To identify a device and authenticate it with IoT Hub, you can use an X.509 certificate generated and signed by a Certification Authority (CA).</span></span> <span data-ttu-id="87ba6-273">L'hub IoT verifica solo che l'identificazione personale presentata corrisponda all'identificazione personale configurata.</span><span class="sxs-lookup"><span data-stu-id="87ba6-273">IoT Hub only verifies that the thumbprint presented matches the configured thumbprint.</span></span> <span data-ttu-id="87ba6-274">IoTHub non convalida la catena di certificati.</span><span class="sxs-lookup"><span data-stu-id="87ba6-274">IotHub does not validate the certificate chain.</span></span>

<span data-ttu-id="87ba6-275">Un dispositivo può usare un certificato X.509 o un token di sicurezza per l'autenticazione, ma non per entrambi.</span><span class="sxs-lookup"><span data-stu-id="87ba6-275">A device may either use an X.509 certificate or a security token for authentication, but not both.</span></span>

### <a name="register-an-x509-certificate-for-a-device"></a><span data-ttu-id="87ba6-276">Registrare un certificato X.509 per un dispositivo</span><span class="sxs-lookup"><span data-stu-id="87ba6-276">Register an X.509 certificate for a device</span></span>

<span data-ttu-id="87ba6-277">Il componente [Azure IoT SDK per servizi per C#][lnk-service-sdk] (versione 1.0.8+) supporta la registrazione di un dispositivo che usa un certificato X.509 per l'autenticazione.</span><span class="sxs-lookup"><span data-stu-id="87ba6-277">The [Azure IoT Service SDK for C#][lnk-service-sdk] (version 1.0.8+) supports registering a device that uses an X.509 certificate for authentication.</span></span> <span data-ttu-id="87ba6-278">Anche altre API come quelle per l'importazione e l'esportazione dei dispositivi supportano i certificati X.509.</span><span class="sxs-lookup"><span data-stu-id="87ba6-278">Other APIs such as import/export of devices also support X.509 certificates.</span></span>

### <a name="c-support"></a><span data-ttu-id="87ba6-279">Supporto per C\#</span><span class="sxs-lookup"><span data-stu-id="87ba6-279">C\# Support</span></span>

<span data-ttu-id="87ba6-280">La classe **RegistryManager** offre un modo di registrare un dispositivo a livello di codice.</span><span class="sxs-lookup"><span data-stu-id="87ba6-280">The **RegistryManager** class provides a programmatic way to register a device.</span></span> <span data-ttu-id="87ba6-281">In particolare, i metodi **AddDeviceAsync** e **UpdateDeviceAsync** consentono di registrare e aggiornare un dispositivo nel registro delle identità dell'hub IoT.</span><span class="sxs-lookup"><span data-stu-id="87ba6-281">In particular, the **AddDeviceAsync** and **UpdateDeviceAsync** methods enable you to register and update a device in the IoT Hub identity registry.</span></span> <span data-ttu-id="87ba6-282">Questi due metodi accettano un'istanza **Device** come input.</span><span class="sxs-lookup"><span data-stu-id="87ba6-282">These two methods take a **Device** instance as input.</span></span> <span data-ttu-id="87ba6-283">La classe **Device** include una proprietà **Authentication** che consente di specificare le identificazioni primarie e secondarie del certificato X.509.</span><span class="sxs-lookup"><span data-stu-id="87ba6-283">The **Device** class includes an **Authentication** property that allows you to specify primary and secondary X.509 certificate thumbprints.</span></span> <span data-ttu-id="87ba6-284">L'identificazione personale rappresenta un hash SHA-1 del certificato X.509 archiviato usando la codifica DER binaria.</span><span class="sxs-lookup"><span data-stu-id="87ba6-284">The thumbprint represents a SHA-1 hash of the X.509 certificate (stored using binary DER encoding).</span></span> <span data-ttu-id="87ba6-285">Gli utenti hanno la possibilità di specificare un'identificazione personale primaria, una secondaria o entrambe.</span><span class="sxs-lookup"><span data-stu-id="87ba6-285">You have the option of specifying a primary thumbprint or a secondary thumbprint or both.</span></span> <span data-ttu-id="87ba6-286">Le identificazioni personali primarie e secondarie sono supportate per gestire scenari di rollover dei certificati.</span><span class="sxs-lookup"><span data-stu-id="87ba6-286">Primary and secondary thumbprints are supported to handle certificate rollover scenarios.</span></span>

> [!NOTE]
> <span data-ttu-id="87ba6-287">L'hub IoT non richiede o archivia l'intero certificato X.509 ma solo l'identificazione personale.</span><span class="sxs-lookup"><span data-stu-id="87ba6-287">IoT Hub does not require or store the entire X.509 certificate, only the thumbprint.</span></span>

<span data-ttu-id="87ba6-288">Ecco un frammento di codice C\# di esempio per registrare un dispositivo usando un certificato X.509:</span><span class="sxs-lookup"><span data-stu-id="87ba6-288">Here is a sample C\# code snippet to register a device using an X.509 certificate:</span></span>

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

### <a name="use-an-x509-certificate-during-run-time-operations"></a><span data-ttu-id="87ba6-289">Usare un certificato X.509 durante le operazioni di runtime</span><span class="sxs-lookup"><span data-stu-id="87ba6-289">Use an X.509 certificate during run-time operations</span></span>

<span data-ttu-id="87ba6-290">[Azure IoT SDK per dispositivi per .NET][lnk-client-sdk] (versione 1.0.11+) supporta l'uso dei certificati X.509.</span><span class="sxs-lookup"><span data-stu-id="87ba6-290">The [Azure IoT device SDK for .NET][lnk-client-sdk] (version 1.0.11+) supports the use of X.509 certificates.</span></span>

### <a name="c-support"></a><span data-ttu-id="87ba6-291">Supporto per C\#</span><span class="sxs-lookup"><span data-stu-id="87ba6-291">C\# Support</span></span>

<span data-ttu-id="87ba6-292">La classe **DeviceAuthenticationWithX509Certificate** supporta la creazione di istanze di **DeviceClient** usando un certificato X.509.</span><span class="sxs-lookup"><span data-stu-id="87ba6-292">The class **DeviceAuthenticationWithX509Certificate** supports the creation of **DeviceClient** instances using an X.509 certificate.</span></span> <span data-ttu-id="87ba6-293">Il certificato X.509 deve essere nel formato PFX, denominato anche PKCS #12, che include la chiave privata.</span><span class="sxs-lookup"><span data-stu-id="87ba6-293">The X.509 certificate must be in the PFX (also called PKCS #12) format that includes the private key.</span></span>

<span data-ttu-id="87ba6-294">Di seguito è riportato un frammento di codice di esempio:</span><span class="sxs-lookup"><span data-stu-id="87ba6-294">Here is a sample code snippet:</span></span>

```csharp
var authMethod = new DeviceAuthenticationWithX509Certificate("<device id>", x509Certificate);

var deviceClient = DeviceClient.Create("<IotHub DNS HostName>", authMethod);
```

## <a name="custom-device-authentication"></a><span data-ttu-id="87ba6-295">Autenticazione personalizzata del dispositivo</span><span class="sxs-lookup"><span data-stu-id="87ba6-295">Custom device authentication</span></span>

<span data-ttu-id="87ba6-296">È possibile usare il [registro delle identità][lnk-identity-registry] dell'hub IoT per configurare il controllo dell'accesso e le credenziali di sicurezza per ogni dispositivo usando i [token][lnk-sas-tokens].</span><span class="sxs-lookup"><span data-stu-id="87ba6-296">You can use the IoT Hub [identity registry][lnk-identity-registry] to configure per-device security credentials and access control using [tokens][lnk-sas-tokens].</span></span> <span data-ttu-id="87ba6-297">Se una soluzione IoT ha già un registro personalizzato delle identità e/o uno schema di autenticazione, valutare la possibilità di creare un *servizio token* per integrare l'infrastruttura con l'hub IoT.</span><span class="sxs-lookup"><span data-stu-id="87ba6-297">If an IoT solution already has a custom identity registry and/or authentication scheme, consider creating a *token service* to integrate this infrastructure with IoT Hub.</span></span> <span data-ttu-id="87ba6-298">In questo modo, è possibile usare altre funzionalità IoT nella soluzione.</span><span class="sxs-lookup"><span data-stu-id="87ba6-298">In this way, you can use other IoT features in your solution.</span></span>

<span data-ttu-id="87ba6-299">Un servizio token è un servizio cloud personalizzato.</span><span class="sxs-lookup"><span data-stu-id="87ba6-299">A token service is a custom cloud service.</span></span> <span data-ttu-id="87ba6-300">Usa i *criteri di accesso condiviso* dell'hub IoT con autorizzazioni **DeviceConnect** per creare token *basati sul dispositivo*.</span><span class="sxs-lookup"><span data-stu-id="87ba6-300">It uses an IoT Hub *shared access policy* with **DeviceConnect** permissions to create *device-scoped* tokens.</span></span> <span data-ttu-id="87ba6-301">Questi token abilitano la connessione di un dispositivo all'hub IoT.</span><span class="sxs-lookup"><span data-stu-id="87ba6-301">These tokens enable a device to connect to your IoT hub.</span></span>

![Passaggi del modello di servizio token][img-tokenservice]

<span data-ttu-id="87ba6-303">Di seguito vengono indicati i passaggi principali del modello del servizio token:</span><span class="sxs-lookup"><span data-stu-id="87ba6-303">Here are the main steps of the token service pattern:</span></span>

1. <span data-ttu-id="87ba6-304">Creare i criteri di accesso condiviso dell'hub IoT con autorizzazioni **DeviceConnect** per l'hub IoT.</span><span class="sxs-lookup"><span data-stu-id="87ba6-304">Create an IoT Hub shared access policy with **DeviceConnect** permissions for your IoT hub.</span></span> <span data-ttu-id="87ba6-305">È possibile creare questi criteri nel [portale di Azure][lnk-management-portal] o a livello di programmazione.</span><span class="sxs-lookup"><span data-stu-id="87ba6-305">You can create this policy in the [Azure portal][lnk-management-portal] or programmatically.</span></span> <span data-ttu-id="87ba6-306">Il servizio token usa questi criteri per firmare i token creati.</span><span class="sxs-lookup"><span data-stu-id="87ba6-306">The token service uses this policy to sign the tokens it creates.</span></span>
1. <span data-ttu-id="87ba6-307">Quando un dispositivo deve accedere all'hub IoT, richiede un token firmato dal servizio token.</span><span class="sxs-lookup"><span data-stu-id="87ba6-307">When a device needs to access your IoT hub, it requests a signed token from your token service.</span></span> <span data-ttu-id="87ba6-308">Il dispositivo può eseguire l'autenticazione con il registro delle identità personalizzato/lo schema di autenticazione per determinare l'identità del dispositivo usata dal servizio token per creare il token.</span><span class="sxs-lookup"><span data-stu-id="87ba6-308">The device can authenticate with your custom identity registry/authentication scheme to determine the device identity that the token service uses to create the token.</span></span>
1. <span data-ttu-id="87ba6-309">Il servizio token restituisce un token.</span><span class="sxs-lookup"><span data-stu-id="87ba6-309">The token service returns a token.</span></span> <span data-ttu-id="87ba6-310">Il token viene creato usando `/devices/{deviceId}` come `resourceURI`, con `deviceId` come dispositivo da autenticare.</span><span class="sxs-lookup"><span data-stu-id="87ba6-310">The token is created by using `/devices/{deviceId}` as `resourceURI`, with `deviceId` as the device being authenticated.</span></span> <span data-ttu-id="87ba6-311">Il servizio token usa i criteri di accesso condivisi per costruire il token.</span><span class="sxs-lookup"><span data-stu-id="87ba6-311">The token service uses the shared access policy to construct the token.</span></span>
1. <span data-ttu-id="87ba6-312">Il dispositivo usa il token direttamente con l'hub IoT.</span><span class="sxs-lookup"><span data-stu-id="87ba6-312">The device uses the token directly with the IoT hub.</span></span>

> [!NOTE]
> <span data-ttu-id="87ba6-313">È possibile usare la classe .NET [SharedAccessSignatureBuilder][lnk-dotnet-sas] o la classe Java [IotHubServiceSasToken][lnk-java-sas] per creare un token nel servizio token.</span><span class="sxs-lookup"><span data-stu-id="87ba6-313">You can use the .NET class [SharedAccessSignatureBuilder][lnk-dotnet-sas] or the Java class [IotHubServiceSasToken][lnk-java-sas] to create a token in your token service.</span></span>

<span data-ttu-id="87ba6-314">Il servizio token può impostare la scadenza del token, in base alle esigenze.</span><span class="sxs-lookup"><span data-stu-id="87ba6-314">The token service can set the token expiration as desired.</span></span> <span data-ttu-id="87ba6-315">Quando il token scade, l'hub IoT interrompe la connessione del dispositivo.</span><span class="sxs-lookup"><span data-stu-id="87ba6-315">When the token expires, the IoT hub severs the device connection.</span></span> <span data-ttu-id="87ba6-316">Quindi, il dispositivo deve richiedere un nuovo token dal servizio token.</span><span class="sxs-lookup"><span data-stu-id="87ba6-316">Then, the device must request a new token from the token service.</span></span> <span data-ttu-id="87ba6-317">Un intervallo di scadenza breve aumenta il carico sia sul dispositivo che sul servizio token.</span><span class="sxs-lookup"><span data-stu-id="87ba6-317">A short expiry time increases the load on both the device and the token service.</span></span>

<span data-ttu-id="87ba6-318">Perché un dispositivo si connetta all'hub, è comunque necessario aggiungerlo al registro delle identità dell'hub IoT anche se il dispositivo usa un token e non una chiave di dispositivo per la connessione.</span><span class="sxs-lookup"><span data-stu-id="87ba6-318">For a device to connect to your hub, you must still add it to the IoT Hub identity registry — even though the device is using a token and not a device key to connect.</span></span> <span data-ttu-id="87ba6-319">È quindi possibile continuare a usare il controllo dell'accesso per ogni dispositivo abilitando o disabilitando le identità dei dispositivi nel [registro delle identità][lnk-identity-registry].</span><span class="sxs-lookup"><span data-stu-id="87ba6-319">Therefore, you can continue to use per-device access control by enabling or disabling device identities in the [identity registry][lnk-identity-registry].</span></span> <span data-ttu-id="87ba6-320">In questo modo si riduce il rischio che vengano usati token con intervalli di scadenza prolungati.</span><span class="sxs-lookup"><span data-stu-id="87ba6-320">This approach mitigates the risks of using tokens with long expiry times.</span></span>

### <a name="comparison-with-a-custom-gateway"></a><span data-ttu-id="87ba6-321">Confronto con un gateway personalizzato</span><span class="sxs-lookup"><span data-stu-id="87ba6-321">Comparison with a custom gateway</span></span>

<span data-ttu-id="87ba6-322">Il modello di servizio token è il metodo consigliato per implementare uno schema di autenticazione/registro di identità personalizzato con l'hub IoT.</span><span class="sxs-lookup"><span data-stu-id="87ba6-322">The token service pattern is the recommended way to implement a custom identity registry/authentication scheme with IoT Hub.</span></span> <span data-ttu-id="87ba6-323">Questo schema è consigliato perché l'hub IoT continua a gestire la maggior parte del traffico della soluzione.</span><span class="sxs-lookup"><span data-stu-id="87ba6-323">This pattern is recommended because IoT Hub continues to handle most of the solution traffic.</span></span> <span data-ttu-id="87ba6-324">Tuttavia, se lo schema di autenticazione personalizzato è molto legato al protocollo, può essere necessario un *gateway personalizzato* per elaborare tutto il traffico.</span><span class="sxs-lookup"><span data-stu-id="87ba6-324">However, if the custom authentication scheme is so intertwined with the protocol, you may require a *custom gateway* to process all the traffic.</span></span> <span data-ttu-id="87ba6-325">Un esempio di tale scenario prevede l'uso del [protocollo TLS (Transport Layer Security) e di chiavi precondivise][lnk-tls-psk].</span><span class="sxs-lookup"><span data-stu-id="87ba6-325">An example of such a scenario is using[Transport Layer Security (TLS) and pre-shared keys (PSKs)][lnk-tls-psk].</span></span> <span data-ttu-id="87ba6-326">Per altre informazioni, vedere l'articolo relativo al [gateway del protocollo][lnk-protocols].</span><span class="sxs-lookup"><span data-stu-id="87ba6-326">For more information, see the [protocol gateway][lnk-protocols] topic.</span></span>

## <a name="reference-topics"></a><span data-ttu-id="87ba6-327">Argomenti di riferimento:</span><span class="sxs-lookup"><span data-stu-id="87ba6-327">Reference topics:</span></span>

<span data-ttu-id="87ba6-328">Gli argomenti di riferimento seguenti offrono altre informazioni sul controllo dell'accesso all'hub IoT.</span><span class="sxs-lookup"><span data-stu-id="87ba6-328">The following reference topics provide you with more information about controlling access to your IoT hub.</span></span>

## <a name="iot-hub-permissions"></a><span data-ttu-id="87ba6-329">Autorizzazioni per l'hub IoT</span><span class="sxs-lookup"><span data-stu-id="87ba6-329">IoT Hub permissions</span></span>

<span data-ttu-id="87ba6-330">La tabella seguente elenca le autorizzazioni che è possibile usare per controllare l'accesso all'hub IoT.</span><span class="sxs-lookup"><span data-stu-id="87ba6-330">The following table lists the permissions you can use to control access to your IoT hub.</span></span>

| <span data-ttu-id="87ba6-331">Autorizzazione</span><span class="sxs-lookup"><span data-stu-id="87ba6-331">Permission</span></span> | <span data-ttu-id="87ba6-332">Note</span><span class="sxs-lookup"><span data-stu-id="87ba6-332">Notes</span></span> |
| --- | --- |
| <span data-ttu-id="87ba6-333">**RegistryRead**</span><span class="sxs-lookup"><span data-stu-id="87ba6-333">**RegistryRead**</span></span> |<span data-ttu-id="87ba6-334">Concede l'accesso di sola lettura al registro di identità.</span><span class="sxs-lookup"><span data-stu-id="87ba6-334">Grants read access to the identity registry.</span></span> <span data-ttu-id="87ba6-335">Per altre informazioni, vedere [Registro delle identità][lnk-identity-registry].</span><span class="sxs-lookup"><span data-stu-id="87ba6-335">For more information, see [Identity registry][lnk-identity-registry].</span></span> <br/><span data-ttu-id="87ba6-336">Questa autorizzazione viene usata dai servizi cloud back-end.</span><span class="sxs-lookup"><span data-stu-id="87ba6-336">This permission is used by back-end cloud services.</span></span> |
| <span data-ttu-id="87ba6-337">**RegistryReadWrite**</span><span class="sxs-lookup"><span data-stu-id="87ba6-337">**RegistryReadWrite**</span></span> |<span data-ttu-id="87ba6-338">Concede l'accesso di lettura e scrittura al registro di identità.</span><span class="sxs-lookup"><span data-stu-id="87ba6-338">Grants read and write access to the identity registry.</span></span> <span data-ttu-id="87ba6-339">Per altre informazioni, vedere [Registro delle identità][lnk-identity-registry].</span><span class="sxs-lookup"><span data-stu-id="87ba6-339">For more information, see [Identity registry][lnk-identity-registry].</span></span> <br/><span data-ttu-id="87ba6-340">Questa autorizzazione viene usata dai servizi cloud back-end.</span><span class="sxs-lookup"><span data-stu-id="87ba6-340">This permission is used by back-end cloud services.</span></span> |
| <span data-ttu-id="87ba6-341">**ServiceConnect**</span><span class="sxs-lookup"><span data-stu-id="87ba6-341">**ServiceConnect**</span></span> |<span data-ttu-id="87ba6-342">Concede l'accesso alle comunicazioni per il servizio cloud e al monitoraggio degli endpoint.</span><span class="sxs-lookup"><span data-stu-id="87ba6-342">Grants access to cloud service-facing communication and monitoring endpoints.</span></span> <br/><span data-ttu-id="87ba6-343">Concede l'autorizzazione per la ricezione di messaggi da dispositivo a cloud, l'invio di messaggi da cloud a dispositivo e il recupero degli acknowledgment di recapito corrispondenti.</span><span class="sxs-lookup"><span data-stu-id="87ba6-343">Grants permission to receive device-to-cloud messages, send cloud-to-device messages, and retrieve the corresponding delivery acknowledgments.</span></span> <br/><span data-ttu-id="87ba6-344">Concede l'autorizzazione per il recupero degli acknowledgement di recapito per caricamenti di file.</span><span class="sxs-lookup"><span data-stu-id="87ba6-344">Grants permission to retrieve delivery acknowledgements for file uploads.</span></span> <br/><span data-ttu-id="87ba6-345">Concede l'autorizzazione per l'accesso a dispositivi gemelli per l'aggiornamento dei tag e delle proprietà indicate, il recupero delle proprietà segnalate e l'esecuzione di query.</span><span class="sxs-lookup"><span data-stu-id="87ba6-345">Grants permission to access device twins to update tags and desired properties, retrieve reported properties, and run queries.</span></span> <br/><span data-ttu-id="87ba6-346">Questa autorizzazione viene usata dai servizi cloud back-end.</span><span class="sxs-lookup"><span data-stu-id="87ba6-346">This permission is used by back-end cloud services.</span></span> |
| <span data-ttu-id="87ba6-347">**DeviceConnect**</span><span class="sxs-lookup"><span data-stu-id="87ba6-347">**DeviceConnect**</span></span> |<span data-ttu-id="87ba6-348">Concede l'accesso agli endpoint per il dispositivo.</span><span class="sxs-lookup"><span data-stu-id="87ba6-348">Grants access to device-facing endpoints.</span></span> <br/><span data-ttu-id="87ba6-349">Concede l'autorizzazione per l'invio di messaggi da dispositivo a cloud e la ricezione di messaggi da cloud a dispositivo.</span><span class="sxs-lookup"><span data-stu-id="87ba6-349">Grants permission to send device-to-cloud messages and receive cloud-to-device messages.</span></span> <br/><span data-ttu-id="87ba6-350">Concede l'autorizzazione per il caricamento di file da un dispositivo.</span><span class="sxs-lookup"><span data-stu-id="87ba6-350">Grants permission to perform file upload from a device.</span></span> <br/><span data-ttu-id="87ba6-351">Concede l'autorizzazione per la ricezione di notifiche su particolari proprietà del dispositivo gemello e l'aggiornamento delle proprietà segnalate di quest'ultimo.</span><span class="sxs-lookup"><span data-stu-id="87ba6-351">Grants permission to receive device twin desired property notifications and update device twin reported properties.</span></span> <br/><span data-ttu-id="87ba6-352">Concede l'autorizzazione per il caricamento di file.</span><span class="sxs-lookup"><span data-stu-id="87ba6-352">Grants permission to perform file uploads.</span></span> <br/><span data-ttu-id="87ba6-353">Questa autorizzazione viene usata dai dispositivi.</span><span class="sxs-lookup"><span data-stu-id="87ba6-353">This permission is used by devices.</span></span> |

## <a name="additional-reference-material"></a><span data-ttu-id="87ba6-354">Materiale di riferimento</span><span class="sxs-lookup"><span data-stu-id="87ba6-354">Additional reference material</span></span>

<span data-ttu-id="87ba6-355">Di seguito sono indicati altri argomenti di riferimento reperibili nella Guida per gli sviluppatori dell'hub IoT:</span><span class="sxs-lookup"><span data-stu-id="87ba6-355">Other reference topics in the IoT Hub developer guide include:</span></span>

* <span data-ttu-id="87ba6-356">[Endpoint dell'hub IoT][lnk-endpoints] illustra i diversi endpoint esposti da ogni hub IoT per operazioni della fase di esecuzione e di gestione.</span><span class="sxs-lookup"><span data-stu-id="87ba6-356">[IoT Hub endpoints][lnk-endpoints] describes the various endpoints that each IoT hub exposes for run-time and management operations.</span></span>
* <span data-ttu-id="87ba6-357">[Quote e limitazioni][lnk-quotas] descrive le quote e i comportamenti di limitazione applicabili al servizio hub IoT.</span><span class="sxs-lookup"><span data-stu-id="87ba6-357">[Throttling and quotas][lnk-quotas] describes the quotas and throttling behaviors that apply to the IoT Hub service.</span></span>
* <span data-ttu-id="87ba6-358">[Azure IoT SDK per dispositivi e servizi][lnk-sdks] elenca gli SDK nei diversi linguaggi che è possibile usare quando si sviluppano app per dispositivi e servizi che interagiscono con l'hub IoT.</span><span class="sxs-lookup"><span data-stu-id="87ba6-358">[Azure IoT device and service SDKs][lnk-sdks] lists the various language SDKs you can use when you develop both device and service apps that interact with IoT Hub.</span></span>
* <span data-ttu-id="87ba6-359">[Linguaggio di query dell'hub IoT][lnk-query] descrive il linguaggio di query che è possibile usare per recuperare informazioni dall'hub IoT sui dispositivi gemelli e sui processi.</span><span class="sxs-lookup"><span data-stu-id="87ba6-359">[IoT Hub query language][lnk-query] describes the query language you can use to retrieve information from IoT Hub about your device twins and jobs.</span></span>
* <span data-ttu-id="87ba6-360">[Supporto di MQTT nell'hub IoT][lnk-devguide-mqtt] offre altre informazioni sul supporto dell'hub IoT per il protocollo MQTT.</span><span class="sxs-lookup"><span data-stu-id="87ba6-360">[IoT Hub MQTT support][lnk-devguide-mqtt] provides more information about IoT Hub support for the MQTT protocol.</span></span>

## <a name="next-steps"></a><span data-ttu-id="87ba6-361">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="87ba6-361">Next steps</span></span>

<span data-ttu-id="87ba6-362">In questa esercitazione si è appreso come controllare l'accesso all'hub IoT. Altri argomenti di interesse reperibili nella Guida per sviluppatori sono i seguenti:</span><span class="sxs-lookup"><span data-stu-id="87ba6-362">Now you have learned how to control access IoT Hub, you may be interested in the following IoT Hub developer guide topics:</span></span>

* <span data-ttu-id="87ba6-363">[Use device twins to synchronize state and configurations][lnk-devguide-device-twins] (Usare dispositivi gemelli per sincronizzare lo stato e le configurazioni)</span><span class="sxs-lookup"><span data-stu-id="87ba6-363">[Use device twins to synchronize state and configurations][lnk-devguide-device-twins]</span></span>
* <span data-ttu-id="87ba6-364">[Richiamare un metodo diretto in un dispositivo][lnk-devguide-directmethods]</span><span class="sxs-lookup"><span data-stu-id="87ba6-364">[Invoke a direct method on a device][lnk-devguide-directmethods]</span></span>
* <span data-ttu-id="87ba6-365">[Pianificare processi in più dispositivi][lnk-devguide-jobs]</span><span class="sxs-lookup"><span data-stu-id="87ba6-365">[Schedule jobs on multiple devices][lnk-devguide-jobs]</span></span>

<span data-ttu-id="87ba6-366">Per provare alcuni dei concetti descritti in questo articolo, possono essere utili le esercitazioni di hub IoT seguenti:</span><span class="sxs-lookup"><span data-stu-id="87ba6-366">If you would like to try out some of the concepts described in this article, you may be interested in the following IoT Hub tutorials:</span></span>

* <span data-ttu-id="87ba6-367">[Introduzione all'hub IoT di Azure][lnk-getstarted-tutorial]</span><span class="sxs-lookup"><span data-stu-id="87ba6-367">[Get started with Azure IoT Hub][lnk-getstarted-tutorial]</span></span>
* <span data-ttu-id="87ba6-368">[Inviare messaggi da cloud a dispositivo con l'hub IoT][lnk-c2d-tutorial]</span><span class="sxs-lookup"><span data-stu-id="87ba6-368">[How to send cloud-to-device messages with IoT Hub][lnk-c2d-tutorial]</span></span>
* <span data-ttu-id="87ba6-369">[Elaborare messaggi da dispositivo a cloud dell'hub IoT][lnk-d2c-tutorial]</span><span class="sxs-lookup"><span data-stu-id="87ba6-369">[How to process IoT Hub device-to-cloud messages][lnk-d2c-tutorial]</span></span>

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

---
title: "notifiche di avviso tramite posta elettronica toosend azioni di scalabilità automatica aaaUse e webhook. | Microsoft Docs"
description: "Vedere come toocall azioni di scalabilità automatica toouse URL web o inviare notifiche tramite posta elettronica in Monitor di Azure. "
author: anirudhcavale
manager: orenr
editor: 
services: monitoring-and-diagnostics
documentationcenter: monitoring-and-diagnostics
ms.assetid: eb9a4c98-0894-488c-8ee8-5df0065d094f
ms.service: monitoring-and-diagnostics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/03/2017
ms.author: ancav
ms.openlocfilehash: f611a18f5a808412fbdd0c89e3addb36437064c4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="use-autoscale-actions-toosend-email-and-webhook-alert-notifications-in-azure-monitor"></a><span data-ttu-id="e874b-104">Utilizzare scalabilità automatica azioni toosend posta elettronica e ai webhook notifiche di avviso in Monitoraggio di Azure</span><span class="sxs-lookup"><span data-stu-id="e874b-104">Use autoscale actions toosend email and webhook alert notifications in Azure Monitor</span></span>
<span data-ttu-id="e874b-105">Questo articolo illustra come configurare i trigger per poter chiamare URL Web specifici o inviare messaggi di posta elettronica in base alle azioni di scalabilità automatica in Azure.</span><span class="sxs-lookup"><span data-stu-id="e874b-105">This article shows you how set up triggers so that you can call specific web URLs or send emails based on autoscale actions in Azure.</span></span>  

## <a name="webhooks"></a><span data-ttu-id="e874b-106">Webhook</span><span class="sxs-lookup"><span data-stu-id="e874b-106">Webhooks</span></span>
<span data-ttu-id="e874b-107">Webhook consentono di sistemi di tooother tooroute hello Azure notifiche di avviso per le notifiche di post-elaborazione o personalizzate.</span><span class="sxs-lookup"><span data-stu-id="e874b-107">Webhooks allow you tooroute hello Azure alert notifications tooother systems for post-processing or custom notifications.</span></span> <span data-ttu-id="e874b-108">Ad esempio, routing tooservices avviso hello in grado di gestire un in ingresso web richiesta toosend SMS, i bug di log, inviare una notifica di un team utilizzando chat o servizi di messaggistica, e così via hello webhook URI deve essere un endpoint HTTP o HTTPS valido.</span><span class="sxs-lookup"><span data-stu-id="e874b-108">For example, routing hello alert tooservices that can handle an incoming web request toosend SMS, log bugs, notify a team using chat or messaging services, etc. hello webhook URI must be a valid HTTP or HTTPS endpoint.</span></span>

## <a name="email"></a><span data-ttu-id="e874b-109">Email</span><span class="sxs-lookup"><span data-stu-id="e874b-109">Email</span></span>
<span data-ttu-id="e874b-110">È possibile inviare tramite posta elettronica tooany indirizzo di posta elettronica valido.</span><span class="sxs-lookup"><span data-stu-id="e874b-110">Email can be sent tooany valid email address.</span></span> <span data-ttu-id="e874b-111">Gli amministratori e i coamministratori della sottoscrizione hello in cui è in esecuzione regola hello anche essere avvisati.</span><span class="sxs-lookup"><span data-stu-id="e874b-111">Administrators and co-administrators of hello subscription where hello rule is running will also be notified.</span></span>

## <a name="cloud-services-and-web-apps"></a><span data-ttu-id="e874b-112">Servizi cloud e app Web</span><span class="sxs-lookup"><span data-stu-id="e874b-112">Cloud Services and Web Apps</span></span>
<span data-ttu-id="e874b-113">È possibile acconsentire esplicitamente dal portale di Azure hello per servizi Cloud e la Server farm (app Web).</span><span class="sxs-lookup"><span data-stu-id="e874b-113">You can opt-in from hello Azure portal for Cloud Services and Server Farms (Web Apps).</span></span>

* <span data-ttu-id="e874b-114">Scegliere hello **scalare** metrica.</span><span class="sxs-lookup"><span data-stu-id="e874b-114">Choose hello **scale by** metric.</span></span>

![Ridimensiona di](./media/insights-autoscale-to-webhook-email/insights-autoscale-notify.png)

## <a name="virtual-machine-scale-sets"></a><span data-ttu-id="e874b-116">Set di scalabilità di macchine virtuali</span><span class="sxs-lookup"><span data-stu-id="e874b-116">Virtual Machine scale sets</span></span>
<span data-ttu-id="e874b-117">Per le macchine virtuali più recenti create con Resource Manager (set di scalabilità di macchine virtuali), è possibile configurare questa opzione tramite l'API REST, i modelli di Resource Manager, PowerShell e l'interfaccia della riga di comando.</span><span class="sxs-lookup"><span data-stu-id="e874b-117">For newer Virtual Machines created with Resource Manager (Virtual Machine scale sets), you can configure this using REST API, Resource Manager templates, PowerShell, and CLI.</span></span> <span data-ttu-id="e874b-118">Un'interfaccia del portale non è ancora disponibile.</span><span class="sxs-lookup"><span data-stu-id="e874b-118">A portal interface is not yet available.</span></span>
<span data-ttu-id="e874b-119">Quando si utilizza l'API REST hello o un modello di gestione risorse, includere l'elemento notifiche hello con hello le opzioni seguenti.</span><span class="sxs-lookup"><span data-stu-id="e874b-119">When using hello REST API or Resource Manager template, include hello notifications element with hello following options.</span></span>

```
"notifications": [
      {
        "operation": "Scale",
        "email": {
          "sendToSubscriptionAdministrator": false,
          "sendToSubscriptionCoAdministrators": false,
          "customEmails": [
              "user1@mycompany.com",
              "user2@mycompany.com"
              ]
        },
        "webhooks": [
          {
            "serviceUri": "https://foo.webhook.example.com?token=abcd1234",
            "properties": {
              "optional_key1": "optional_value1",
              "optional_key2": "optional_value2"
            }
          }
        ]
      }
    ]
```
| <span data-ttu-id="e874b-120">Campo</span><span class="sxs-lookup"><span data-stu-id="e874b-120">Field</span></span> | <span data-ttu-id="e874b-121">Obbligatorio?</span><span class="sxs-lookup"><span data-stu-id="e874b-121">Mandatory?</span></span> | <span data-ttu-id="e874b-122">Descrizione</span><span class="sxs-lookup"><span data-stu-id="e874b-122">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="e874b-123">operation</span><span class="sxs-lookup"><span data-stu-id="e874b-123">operation</span></span> |<span data-ttu-id="e874b-124">sì</span><span class="sxs-lookup"><span data-stu-id="e874b-124">yes</span></span> |<span data-ttu-id="e874b-125">Il valore deve essere "Scale"</span><span class="sxs-lookup"><span data-stu-id="e874b-125">value must be "Scale"</span></span> |
| <span data-ttu-id="e874b-126">sendToSubscriptionAdministrator</span><span class="sxs-lookup"><span data-stu-id="e874b-126">sendToSubscriptionAdministrator</span></span> |<span data-ttu-id="e874b-127">sì</span><span class="sxs-lookup"><span data-stu-id="e874b-127">yes</span></span> |<span data-ttu-id="e874b-128">Il valore deve essere "true" o "false"</span><span class="sxs-lookup"><span data-stu-id="e874b-128">value must be "true" or "false"</span></span> |
| <span data-ttu-id="e874b-129">sendToSubscriptionCoAdministrators</span><span class="sxs-lookup"><span data-stu-id="e874b-129">sendToSubscriptionCoAdministrators</span></span> |<span data-ttu-id="e874b-130">sì</span><span class="sxs-lookup"><span data-stu-id="e874b-130">yes</span></span> |<span data-ttu-id="e874b-131">Il valore deve essere "true" o "false"</span><span class="sxs-lookup"><span data-stu-id="e874b-131">value must be "true" or "false"</span></span> |
| <span data-ttu-id="e874b-132">customEmails</span><span class="sxs-lookup"><span data-stu-id="e874b-132">customEmails</span></span> |<span data-ttu-id="e874b-133">sì</span><span class="sxs-lookup"><span data-stu-id="e874b-133">yes</span></span> |<span data-ttu-id="e874b-134">Il valore può essere null [] o la matrice di stringhe di messaggi di posta elettronica</span><span class="sxs-lookup"><span data-stu-id="e874b-134">value can be null [] or string array of emails</span></span> |
| <span data-ttu-id="e874b-135">Webhook</span><span class="sxs-lookup"><span data-stu-id="e874b-135">webhooks</span></span> |<span data-ttu-id="e874b-136">sì</span><span class="sxs-lookup"><span data-stu-id="e874b-136">yes</span></span> |<span data-ttu-id="e874b-137">Il valore può essere null o un URI valido</span><span class="sxs-lookup"><span data-stu-id="e874b-137">value can be null or valid Uri</span></span> |
| <span data-ttu-id="e874b-138">serviceUri</span><span class="sxs-lookup"><span data-stu-id="e874b-138">serviceUri</span></span> |<span data-ttu-id="e874b-139">sì</span><span class="sxs-lookup"><span data-stu-id="e874b-139">yes</span></span> |<span data-ttu-id="e874b-140">Un URI HTTPS valido</span><span class="sxs-lookup"><span data-stu-id="e874b-140">a valid https Uri</span></span> |
| <span data-ttu-id="e874b-141">properties</span><span class="sxs-lookup"><span data-stu-id="e874b-141">properties</span></span> |<span data-ttu-id="e874b-142">sì</span><span class="sxs-lookup"><span data-stu-id="e874b-142">yes</span></span> |<span data-ttu-id="e874b-143">Il valore deve essere vuoto {} o può contenere coppie chiave-valore</span><span class="sxs-lookup"><span data-stu-id="e874b-143">value must be empty {} or can contain key-value pairs</span></span> |

## <a name="authentication-in-webhooks"></a><span data-ttu-id="e874b-144">Autenticazione nei webhook</span><span class="sxs-lookup"><span data-stu-id="e874b-144">Authentication in webhooks</span></span>
<span data-ttu-id="e874b-145">Hello webhook autenticazione utilizzando l'autenticazione basata su token, in cui vengono salvati hello webhook URI con un ID token come un parametro di query.</span><span class="sxs-lookup"><span data-stu-id="e874b-145">hello webhook can authenticate using token-based authentication, where you save hello webhook URI with a token ID as a query parameter.</span></span> <span data-ttu-id="e874b-146">Ad esempio, https://mysamplealert/webcallback?tokenid=sometokenid&someparameter=somevalue</span><span class="sxs-lookup"><span data-stu-id="e874b-146">For example, https://mysamplealert/webcallback?tokenid=sometokenid&someparameter=somevalue</span></span>

## <a name="autoscale-notification-webhook-payload-schema"></a><span data-ttu-id="e874b-147">Schema di payload del webhook di notifica di scalabilità automatica</span><span class="sxs-lookup"><span data-stu-id="e874b-147">Autoscale notification webhook payload schema</span></span>
<span data-ttu-id="e874b-148">Quando viene generata la notifica di scalabilità automatica hello, hello metadati seguenti sono incluse nel payload webhook hello:</span><span class="sxs-lookup"><span data-stu-id="e874b-148">When hello autoscale notification is generated, hello following metadata is included in hello webhook payload:</span></span>

```
{
        "version": "1.0",
        "status": "Activated",
        "operation": "Scale In",
        "context": {
                "timestamp": "2016-03-11T07:31:04.5834118Z",
                "id": "/subscriptions/s1/resourceGroups/rg1/providers/microsoft.insights/autoscalesettings/myautoscaleSetting",
                "name": "myautoscaleSetting",
                "details": "Autoscale successfully started scale operation for resource 'MyCSRole' from capacity '3' toocapacity '2'",
                "subscriptionId": "s1",
                "resourceGroupName": "rg1",
                "resourceName": "MyCSRole",
                "resourceType": "microsoft.classiccompute/domainnames/slots/roles",
                "resourceId": "/subscriptions/s1/resourceGroups/rg1/providers/microsoft.classicCompute/domainNames/myCloudService/slots/Production/roles/MyCSRole",
                "portalLink": "https://portal.azure.com/#resource/subscriptions/s1/resourceGroups/rg1/providers/microsoft.classicCompute/domainNames/myCloudService",
                "oldCapacity": "3",
                "newCapacity": "2"
        },
        "properties": {
                "key1": "value1",
                "key2": "value2"
        }
}
```


| <span data-ttu-id="e874b-149">Campo</span><span class="sxs-lookup"><span data-stu-id="e874b-149">Field</span></span> | <span data-ttu-id="e874b-150">Obbligatorio?</span><span class="sxs-lookup"><span data-stu-id="e874b-150">Mandatory?</span></span> | <span data-ttu-id="e874b-151">Descrizione</span><span class="sxs-lookup"><span data-stu-id="e874b-151">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="e874b-152">status</span><span class="sxs-lookup"><span data-stu-id="e874b-152">status</span></span> |<span data-ttu-id="e874b-153">sì</span><span class="sxs-lookup"><span data-stu-id="e874b-153">yes</span></span> |<span data-ttu-id="e874b-154">stato Hello che indica che un'azione di scalabilità automatica è stata generata</span><span class="sxs-lookup"><span data-stu-id="e874b-154">hello status that indicates that an autoscale action was generated</span></span> |
| <span data-ttu-id="e874b-155">operation</span><span class="sxs-lookup"><span data-stu-id="e874b-155">operation</span></span> |<span data-ttu-id="e874b-156">sì</span><span class="sxs-lookup"><span data-stu-id="e874b-156">yes</span></span> |<span data-ttu-id="e874b-157">Per un aumento delle istanze, sarà "Scale Out", mentre per una riduzione delle istanze, sarà "Scale In"</span><span class="sxs-lookup"><span data-stu-id="e874b-157">For an increase of instances, it will be "Scale Out" and for a decrease in instances, it will be "Scale In"</span></span> |
| <span data-ttu-id="e874b-158">context</span><span class="sxs-lookup"><span data-stu-id="e874b-158">context</span></span> |<span data-ttu-id="e874b-159">sì</span><span class="sxs-lookup"><span data-stu-id="e874b-159">yes</span></span> |<span data-ttu-id="e874b-160">contesto dell'azione di scalabilità automatica Hello</span><span class="sxs-lookup"><span data-stu-id="e874b-160">hello autoscale action context</span></span> |
| <span data-ttu-id="e874b-161">timestamp</span><span class="sxs-lookup"><span data-stu-id="e874b-161">timestamp</span></span> |<span data-ttu-id="e874b-162">sì</span><span class="sxs-lookup"><span data-stu-id="e874b-162">yes</span></span> |<span data-ttu-id="e874b-163">Timestamp relativo all'azione di scalabilità automatica hello è stata attivata</span><span class="sxs-lookup"><span data-stu-id="e874b-163">Time stamp when hello autoscale action was triggered</span></span> |
| <span data-ttu-id="e874b-164">id</span><span class="sxs-lookup"><span data-stu-id="e874b-164">id</span></span> |<span data-ttu-id="e874b-165">Sì</span><span class="sxs-lookup"><span data-stu-id="e874b-165">Yes</span></span> |<span data-ttu-id="e874b-166">Gestione risorse di ID dell'impostazione di scalabilità automatica hello</span><span class="sxs-lookup"><span data-stu-id="e874b-166">Resource Manager ID of hello autoscale setting</span></span> |
| <span data-ttu-id="e874b-167">name</span><span class="sxs-lookup"><span data-stu-id="e874b-167">name</span></span> |<span data-ttu-id="e874b-168">Sì</span><span class="sxs-lookup"><span data-stu-id="e874b-168">Yes</span></span> |<span data-ttu-id="e874b-169">nome Hello dell'impostazione di scalabilità automatica hello</span><span class="sxs-lookup"><span data-stu-id="e874b-169">hello name of hello autoscale setting</span></span> |
| <span data-ttu-id="e874b-170">informazioni dettagliate</span><span class="sxs-lookup"><span data-stu-id="e874b-170">details</span></span> |<span data-ttu-id="e874b-171">Sì</span><span class="sxs-lookup"><span data-stu-id="e874b-171">Yes</span></span> |<span data-ttu-id="e874b-172">Descrizione dell'azione hello che ha richiesto il servizio di scalabilità automatica hello e hello viene modificato il numero di istanze di hello</span><span class="sxs-lookup"><span data-stu-id="e874b-172">Explanation of hello action that hello autoscale service took and hello change in hello instance count</span></span> |
| <span data-ttu-id="e874b-173">subscriptionId</span><span class="sxs-lookup"><span data-stu-id="e874b-173">subscriptionId</span></span> |<span data-ttu-id="e874b-174">Sì</span><span class="sxs-lookup"><span data-stu-id="e874b-174">Yes</span></span> |<span data-ttu-id="e874b-175">ID di sottoscrizione della risorsa di destinazione hello che viene ridimensionato</span><span class="sxs-lookup"><span data-stu-id="e874b-175">Subscription ID of hello target resource that is being scaled</span></span> |
| <span data-ttu-id="e874b-176">resourceGroupName</span><span class="sxs-lookup"><span data-stu-id="e874b-176">resourceGroupName</span></span> |<span data-ttu-id="e874b-177">Sì</span><span class="sxs-lookup"><span data-stu-id="e874b-177">Yes</span></span> |<span data-ttu-id="e874b-178">Nome gruppo di risorse della risorsa di destinazione hello che viene ridimensionato</span><span class="sxs-lookup"><span data-stu-id="e874b-178">Resource Group name of hello target resource that is being scaled</span></span> |
| <span data-ttu-id="e874b-179">resourceName</span><span class="sxs-lookup"><span data-stu-id="e874b-179">resourceName</span></span> |<span data-ttu-id="e874b-180">Sì</span><span class="sxs-lookup"><span data-stu-id="e874b-180">Yes</span></span> |<span data-ttu-id="e874b-181">Nome della risorsa di destinazione hello che viene ridimensionato</span><span class="sxs-lookup"><span data-stu-id="e874b-181">Name of hello target resource that is being scaled</span></span> |
| <span data-ttu-id="e874b-182">resourceType</span><span class="sxs-lookup"><span data-stu-id="e874b-182">resourceType</span></span> |<span data-ttu-id="e874b-183">Sì</span><span class="sxs-lookup"><span data-stu-id="e874b-183">Yes</span></span> |<span data-ttu-id="e874b-184">Hello tre valori supportati: "microsoft.classiccompute/domainnames/slots/roles" - ruoli servizio Cloud, "microsoft.compute/virtualmachinescalesets" - set di scalabilità di macchine virtuali e "Web/serverfarms" - App Web</span><span class="sxs-lookup"><span data-stu-id="e874b-184">hello three supported values: "microsoft.classiccompute/domainnames/slots/roles" - Cloud Service roles, "microsoft.compute/virtualmachinescalesets" - Virtual Machine Scale Sets,  and "Microsoft.Web/serverfarms" - Web App</span></span> |
| <span data-ttu-id="e874b-185">resourceId</span><span class="sxs-lookup"><span data-stu-id="e874b-185">resourceId</span></span> |<span data-ttu-id="e874b-186">Sì</span><span class="sxs-lookup"><span data-stu-id="e874b-186">Yes</span></span> |<span data-ttu-id="e874b-187">Gestione risorse di ID della risorsa di destinazione hello che viene ridimensionato</span><span class="sxs-lookup"><span data-stu-id="e874b-187">Resource Manager ID of hello target resource that is being scaled</span></span> |
| <span data-ttu-id="e874b-188">portalLink</span><span class="sxs-lookup"><span data-stu-id="e874b-188">portalLink</span></span> |<span data-ttu-id="e874b-189">Sì</span><span class="sxs-lookup"><span data-stu-id="e874b-189">Yes</span></span> |<span data-ttu-id="e874b-190">Pagina Riepilogo di collegamento del portale Azure toohello della risorsa di destinazione hello</span><span class="sxs-lookup"><span data-stu-id="e874b-190">Azure portal link toohello summary page of hello target resource</span></span> |
| <span data-ttu-id="e874b-191">oldCapacity</span><span class="sxs-lookup"><span data-stu-id="e874b-191">oldCapacity</span></span> |<span data-ttu-id="e874b-192">Sì</span><span class="sxs-lookup"><span data-stu-id="e874b-192">Yes</span></span> |<span data-ttu-id="e874b-193">Hello (precedente) numero di istanze correnti quando scalabilità automatica ha richiesto un'azione di scalabilità</span><span class="sxs-lookup"><span data-stu-id="e874b-193">hello current (old) instance count when Autoscale took a scale action</span></span> |
| <span data-ttu-id="e874b-194">newCapacity</span><span class="sxs-lookup"><span data-stu-id="e874b-194">newCapacity</span></span> |<span data-ttu-id="e874b-195">Sì</span><span class="sxs-lookup"><span data-stu-id="e874b-195">Yes</span></span> |<span data-ttu-id="e874b-196">Hello nuovo numero di istanze di scalabilità automatica ridimensionato risorse hello troppo</span><span class="sxs-lookup"><span data-stu-id="e874b-196">hello new instance count that Autoscale scaled hello resource too</span></span>|
| <span data-ttu-id="e874b-197">Proprietà</span><span class="sxs-lookup"><span data-stu-id="e874b-197">Properties</span></span> |<span data-ttu-id="e874b-198">No</span><span class="sxs-lookup"><span data-stu-id="e874b-198">No</span></span> |<span data-ttu-id="e874b-199">Facoltativo.</span><span class="sxs-lookup"><span data-stu-id="e874b-199">Optional.</span></span> <span data-ttu-id="e874b-200">Set di coppie <chiave, valore> (ad esempio Dizionario <Stringa, Stringa>).</span><span class="sxs-lookup"><span data-stu-id="e874b-200">Set of <Key, Value> pairs (for example,  Dictionary <String, String>).</span></span> <span data-ttu-id="e874b-201">campo di proprietà Hello è facoltativo.</span><span class="sxs-lookup"><span data-stu-id="e874b-201">hello properties field is optional.</span></span> <span data-ttu-id="e874b-202">In un'interfaccia utente personalizzata o un flusso di lavoro di logica app in base, è possibile immettere le chiavi e valori che possono essere passati usando payload hello.</span><span class="sxs-lookup"><span data-stu-id="e874b-202">In a custom user interface  or Logic app based workflow, you can enter keys and values that can be passed using hello payload.</span></span> <span data-ttu-id="e874b-203">Un modo alternativo di proprietà personalizzate toopass nuovamente chiamata webhook in uscita toohello è toouse hello webhook URI stesso (come parametri di query)</span><span class="sxs-lookup"><span data-stu-id="e874b-203">An alternate way toopass custom properties back toohello outgoing webhook call is toouse hello webhook URI itself (as query parameters)</span></span> |

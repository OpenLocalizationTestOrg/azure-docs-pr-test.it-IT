---
title: "Usare le azioni di scalabilità automatica per inviare notifiche di avviso di webhook e posta elettronica. | Microsoft Docs"
description: "Informazioni su come usare le azioni di scalabilità automatica per chiamare URL Web o inviare notifiche di posta elettronica in Monitoraggio di Azure. "
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
ms.openlocfilehash: 16caf14028494800e9259f0296c292b606d0210a
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/03/2017
---
# <a name="use-autoscale-actions-to-send-email-and-webhook-alert-notifications-in-azure-monitor"></a><span data-ttu-id="ba960-104">Usare le azioni di scalabilità automatica per inviare notifiche di avviso di webhook e posta elettronica in Monitoraggio di Azure</span><span class="sxs-lookup"><span data-stu-id="ba960-104">Use autoscale actions to send email and webhook alert notifications in Azure Monitor</span></span>
<span data-ttu-id="ba960-105">Questo articolo illustra come configurare i trigger per poter chiamare URL Web specifici o inviare messaggi di posta elettronica in base alle azioni di scalabilità automatica in Azure.</span><span class="sxs-lookup"><span data-stu-id="ba960-105">This article shows you how set up triggers so that you can call specific web URLs or send emails based on autoscale actions in Azure.</span></span>  

## <a name="webhooks"></a><span data-ttu-id="ba960-106">Webhook</span><span class="sxs-lookup"><span data-stu-id="ba960-106">Webhooks</span></span>
<span data-ttu-id="ba960-107">I webhook consentono di instradare le notifiche di avviso di Azure ad altri sistemi per la post-elaborazione o le notifiche personalizzate.</span><span class="sxs-lookup"><span data-stu-id="ba960-107">Webhooks allow you to route the Azure alert notifications to other systems for post-processing or custom notifications.</span></span> <span data-ttu-id="ba960-108">È possibile, ad esempio, eseguire il routing degli avvisi a servizi che possono gestire una richiesta Web in ingresso per inviare SMS, registrare bug, inviare notifiche a un team usando servizi di messaggistica o chat e così via. L'URI del webhook deve essere un endpoint HTTP o HTTPS valido.</span><span class="sxs-lookup"><span data-stu-id="ba960-108">For example, routing the alert to services that can handle an incoming web request to send SMS, log bugs, notify a team using chat or messaging services, etc. The webhook URI must be a valid HTTP or HTTPS endpoint.</span></span>

## <a name="email"></a><span data-ttu-id="ba960-109">Email</span><span class="sxs-lookup"><span data-stu-id="ba960-109">Email</span></span>
<span data-ttu-id="ba960-110">È possibile inviare un messaggio di posta elettronica a qualsiasi indirizzo di posta elettronica valido.</span><span class="sxs-lookup"><span data-stu-id="ba960-110">Email can be sent to any valid email address.</span></span> <span data-ttu-id="ba960-111">Verrà inviata una notifica anche agli amministratori e ai coamministratori della sottoscrizione in cui viene eseguita la regola.</span><span class="sxs-lookup"><span data-stu-id="ba960-111">Administrators and co-administrators of the subscription where the rule is running will also be notified.</span></span>

## <a name="cloud-services-and-web-apps"></a><span data-ttu-id="ba960-112">Servizi cloud e app Web</span><span class="sxs-lookup"><span data-stu-id="ba960-112">Cloud Services and Web Apps</span></span>
<span data-ttu-id="ba960-113">È possibile acconsentire esplicitamente dal portale di Azure ai servizi cloud e alle server farm (app Web).</span><span class="sxs-lookup"><span data-stu-id="ba960-113">You can opt-in from the Azure portal for Cloud Services and Server Farms (Web Apps).</span></span>

* <span data-ttu-id="ba960-114">Scegliere la metrica **Ridimensiona di** .</span><span class="sxs-lookup"><span data-stu-id="ba960-114">Choose the **scale by** metric.</span></span>

![Ridimensiona di](./media/insights-autoscale-to-webhook-email/insights-autoscale-notify.png)

## <a name="virtual-machine-scale-sets"></a><span data-ttu-id="ba960-116">Set di scalabilità di macchine virtuali</span><span class="sxs-lookup"><span data-stu-id="ba960-116">Virtual Machine scale sets</span></span>
<span data-ttu-id="ba960-117">Per le macchine virtuali più recenti create con Resource Manager (set di scalabilità di macchine virtuali), è possibile configurare questa opzione tramite l'API REST, i modelli di Resource Manager, PowerShell e l'interfaccia della riga di comando.</span><span class="sxs-lookup"><span data-stu-id="ba960-117">For newer Virtual Machines created with Resource Manager (Virtual Machine scale sets), you can configure this using REST API, Resource Manager templates, PowerShell, and CLI.</span></span> <span data-ttu-id="ba960-118">Un'interfaccia del portale non è ancora disponibile.</span><span class="sxs-lookup"><span data-stu-id="ba960-118">A portal interface is not yet available.</span></span>
<span data-ttu-id="ba960-119">Quando si usa l'API REST o il modello di Resource Manager, includere l'elemento Notifiche con le opzioni seguenti.</span><span class="sxs-lookup"><span data-stu-id="ba960-119">When using the REST API or Resource Manager template, include the notifications element with the following options.</span></span>

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
| <span data-ttu-id="ba960-120">Campo</span><span class="sxs-lookup"><span data-stu-id="ba960-120">Field</span></span> | <span data-ttu-id="ba960-121">Obbligatorio?</span><span class="sxs-lookup"><span data-stu-id="ba960-121">Mandatory?</span></span> | <span data-ttu-id="ba960-122">Descrizione</span><span class="sxs-lookup"><span data-stu-id="ba960-122">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="ba960-123">operation</span><span class="sxs-lookup"><span data-stu-id="ba960-123">operation</span></span> |<span data-ttu-id="ba960-124">sì</span><span class="sxs-lookup"><span data-stu-id="ba960-124">yes</span></span> |<span data-ttu-id="ba960-125">Il valore deve essere "Scale"</span><span class="sxs-lookup"><span data-stu-id="ba960-125">value must be "Scale"</span></span> |
| <span data-ttu-id="ba960-126">sendToSubscriptionAdministrator</span><span class="sxs-lookup"><span data-stu-id="ba960-126">sendToSubscriptionAdministrator</span></span> |<span data-ttu-id="ba960-127">sì</span><span class="sxs-lookup"><span data-stu-id="ba960-127">yes</span></span> |<span data-ttu-id="ba960-128">Il valore deve essere "true" o "false"</span><span class="sxs-lookup"><span data-stu-id="ba960-128">value must be "true" or "false"</span></span> |
| <span data-ttu-id="ba960-129">sendToSubscriptionCoAdministrators</span><span class="sxs-lookup"><span data-stu-id="ba960-129">sendToSubscriptionCoAdministrators</span></span> |<span data-ttu-id="ba960-130">sì</span><span class="sxs-lookup"><span data-stu-id="ba960-130">yes</span></span> |<span data-ttu-id="ba960-131">Il valore deve essere "true" o "false"</span><span class="sxs-lookup"><span data-stu-id="ba960-131">value must be "true" or "false"</span></span> |
| <span data-ttu-id="ba960-132">customEmails</span><span class="sxs-lookup"><span data-stu-id="ba960-132">customEmails</span></span> |<span data-ttu-id="ba960-133">sì</span><span class="sxs-lookup"><span data-stu-id="ba960-133">yes</span></span> |<span data-ttu-id="ba960-134">Il valore può essere null [] o la matrice di stringhe di messaggi di posta elettronica</span><span class="sxs-lookup"><span data-stu-id="ba960-134">value can be null [] or string array of emails</span></span> |
| <span data-ttu-id="ba960-135">Webhook</span><span class="sxs-lookup"><span data-stu-id="ba960-135">webhooks</span></span> |<span data-ttu-id="ba960-136">sì</span><span class="sxs-lookup"><span data-stu-id="ba960-136">yes</span></span> |<span data-ttu-id="ba960-137">Il valore può essere null o un URI valido</span><span class="sxs-lookup"><span data-stu-id="ba960-137">value can be null or valid Uri</span></span> |
| <span data-ttu-id="ba960-138">serviceUri</span><span class="sxs-lookup"><span data-stu-id="ba960-138">serviceUri</span></span> |<span data-ttu-id="ba960-139">sì</span><span class="sxs-lookup"><span data-stu-id="ba960-139">yes</span></span> |<span data-ttu-id="ba960-140">Un URI HTTPS valido</span><span class="sxs-lookup"><span data-stu-id="ba960-140">a valid https Uri</span></span> |
| <span data-ttu-id="ba960-141">properties</span><span class="sxs-lookup"><span data-stu-id="ba960-141">properties</span></span> |<span data-ttu-id="ba960-142">sì</span><span class="sxs-lookup"><span data-stu-id="ba960-142">yes</span></span> |<span data-ttu-id="ba960-143">Il valore deve essere vuoto {} o può contenere coppie chiave-valore</span><span class="sxs-lookup"><span data-stu-id="ba960-143">value must be empty {} or can contain key-value pairs</span></span> |

## <a name="authentication-in-webhooks"></a><span data-ttu-id="ba960-144">Autenticazione nei webhook</span><span class="sxs-lookup"><span data-stu-id="ba960-144">Authentication in webhooks</span></span>
<span data-ttu-id="ba960-145">È possibile autenticare il webhook usando l'autenticazione basata su token, che prevede il salvataggio dell'URI del webhook con un ID token come parametro di query.</span><span class="sxs-lookup"><span data-stu-id="ba960-145">The webhook can authenticate using token-based authentication, where you save the webhook URI with a token ID as a query parameter.</span></span> <span data-ttu-id="ba960-146">Ad esempio, https://mysamplealert/webcallback?tokenid=sometokenid&someparameter=somevalue</span><span class="sxs-lookup"><span data-stu-id="ba960-146">For example, https://mysamplealert/webcallback?tokenid=sometokenid&someparameter=somevalue</span></span>

## <a name="autoscale-notification-webhook-payload-schema"></a><span data-ttu-id="ba960-147">Schema di payload del webhook di notifica di scalabilità automatica</span><span class="sxs-lookup"><span data-stu-id="ba960-147">Autoscale notification webhook payload schema</span></span>
<span data-ttu-id="ba960-148">Quando viene generata la notifica di scalabilità automatica, nel payload del webhook vengono inclusi i metadati seguenti:</span><span class="sxs-lookup"><span data-stu-id="ba960-148">When the autoscale notification is generated, the following metadata is included in the webhook payload:</span></span>

```
{
        "version": "1.0",
        "status": "Activated",
        "operation": "Scale In",
        "context": {
                "timestamp": "2016-03-11T07:31:04.5834118Z",
                "id": "/subscriptions/s1/resourceGroups/rg1/providers/microsoft.insights/autoscalesettings/myautoscaleSetting",
                "name": "myautoscaleSetting",
                "details": "Autoscale successfully started scale operation for resource 'MyCSRole' from capacity '3' to capacity '2'",
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


| <span data-ttu-id="ba960-149">Campo</span><span class="sxs-lookup"><span data-stu-id="ba960-149">Field</span></span> | <span data-ttu-id="ba960-150">Obbligatorio?</span><span class="sxs-lookup"><span data-stu-id="ba960-150">Mandatory?</span></span> | <span data-ttu-id="ba960-151">Descrizione</span><span class="sxs-lookup"><span data-stu-id="ba960-151">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="ba960-152">status</span><span class="sxs-lookup"><span data-stu-id="ba960-152">status</span></span> |<span data-ttu-id="ba960-153">sì</span><span class="sxs-lookup"><span data-stu-id="ba960-153">yes</span></span> |<span data-ttu-id="ba960-154">Stato che indica che è stata generata un'azione di scalabilità automatica</span><span class="sxs-lookup"><span data-stu-id="ba960-154">The status that indicates that an autoscale action was generated</span></span> |
| <span data-ttu-id="ba960-155">operation</span><span class="sxs-lookup"><span data-stu-id="ba960-155">operation</span></span> |<span data-ttu-id="ba960-156">sì</span><span class="sxs-lookup"><span data-stu-id="ba960-156">yes</span></span> |<span data-ttu-id="ba960-157">Per un aumento delle istanze, sarà "Scale Out", mentre per una riduzione delle istanze, sarà "Scale In"</span><span class="sxs-lookup"><span data-stu-id="ba960-157">For an increase of instances, it will be "Scale Out" and for a decrease in instances, it will be "Scale In"</span></span> |
| <span data-ttu-id="ba960-158">context</span><span class="sxs-lookup"><span data-stu-id="ba960-158">context</span></span> |<span data-ttu-id="ba960-159">sì</span><span class="sxs-lookup"><span data-stu-id="ba960-159">yes</span></span> |<span data-ttu-id="ba960-160">Contesto dell'azione di scalabilità automatica</span><span class="sxs-lookup"><span data-stu-id="ba960-160">The autoscale action context</span></span> |
| <span data-ttu-id="ba960-161">timestamp</span><span class="sxs-lookup"><span data-stu-id="ba960-161">timestamp</span></span> |<span data-ttu-id="ba960-162">sì</span><span class="sxs-lookup"><span data-stu-id="ba960-162">yes</span></span> |<span data-ttu-id="ba960-163">Timestamp in cui è stata attivata l'azione di scalabilità automatica</span><span class="sxs-lookup"><span data-stu-id="ba960-163">Time stamp when the autoscale action was triggered</span></span> |
| <span data-ttu-id="ba960-164">id</span><span class="sxs-lookup"><span data-stu-id="ba960-164">id</span></span> |<span data-ttu-id="ba960-165">sì</span><span class="sxs-lookup"><span data-stu-id="ba960-165">Yes</span></span> |<span data-ttu-id="ba960-166">ID di Resource Manager dell'impostazione di scalabilità automatica</span><span class="sxs-lookup"><span data-stu-id="ba960-166">Resource Manager ID of the autoscale setting</span></span> |
| <span data-ttu-id="ba960-167">name</span><span class="sxs-lookup"><span data-stu-id="ba960-167">name</span></span> |<span data-ttu-id="ba960-168">sì</span><span class="sxs-lookup"><span data-stu-id="ba960-168">Yes</span></span> |<span data-ttu-id="ba960-169">Nome dell'impostazione di scalabilità automatica</span><span class="sxs-lookup"><span data-stu-id="ba960-169">The name of the autoscale setting</span></span> |
| <span data-ttu-id="ba960-170">informazioni dettagliate</span><span class="sxs-lookup"><span data-stu-id="ba960-170">details</span></span> |<span data-ttu-id="ba960-171">sì</span><span class="sxs-lookup"><span data-stu-id="ba960-171">Yes</span></span> |<span data-ttu-id="ba960-172">Spiegazione dell'azione eseguita dal servizio di scalabilità automatica e della modifica al conteggio delle istanze</span><span class="sxs-lookup"><span data-stu-id="ba960-172">Explanation of the action that the autoscale service took and the change in the instance count</span></span> |
| <span data-ttu-id="ba960-173">subscriptionId</span><span class="sxs-lookup"><span data-stu-id="ba960-173">subscriptionId</span></span> |<span data-ttu-id="ba960-174">sì</span><span class="sxs-lookup"><span data-stu-id="ba960-174">Yes</span></span> |<span data-ttu-id="ba960-175">ID sottoscrizione della risorsa di destinazione da ridimensionare</span><span class="sxs-lookup"><span data-stu-id="ba960-175">Subscription ID of the target resource that is being scaled</span></span> |
| <span data-ttu-id="ba960-176">resourceGroupName</span><span class="sxs-lookup"><span data-stu-id="ba960-176">resourceGroupName</span></span> |<span data-ttu-id="ba960-177">sì</span><span class="sxs-lookup"><span data-stu-id="ba960-177">Yes</span></span> |<span data-ttu-id="ba960-178">Nome del gruppo di risorse della risorsa di destinazione da ridimensionare</span><span class="sxs-lookup"><span data-stu-id="ba960-178">Resource Group name of the target resource that is being scaled</span></span> |
| <span data-ttu-id="ba960-179">resourceName</span><span class="sxs-lookup"><span data-stu-id="ba960-179">resourceName</span></span> |<span data-ttu-id="ba960-180">sì</span><span class="sxs-lookup"><span data-stu-id="ba960-180">Yes</span></span> |<span data-ttu-id="ba960-181">Nome della risorsa di destinazione da ridimensionare</span><span class="sxs-lookup"><span data-stu-id="ba960-181">Name of the target resource that is being scaled</span></span> |
| <span data-ttu-id="ba960-182">resourceType</span><span class="sxs-lookup"><span data-stu-id="ba960-182">resourceType</span></span> |<span data-ttu-id="ba960-183">Sì</span><span class="sxs-lookup"><span data-stu-id="ba960-183">Yes</span></span> |<span data-ttu-id="ba960-184">I tre valori supportati: "microsoft.classiccompute/domainnames/slots/roles" (ruoli dei servizi cloud), "microsoft.compute/virtualmachinescalesets" (set di scalabilità di macchine virtuali) e "Microsoft.Web/serverfarms" (app Web)</span><span class="sxs-lookup"><span data-stu-id="ba960-184">The three supported values: "microsoft.classiccompute/domainnames/slots/roles" - Cloud Service roles, "microsoft.compute/virtualmachinescalesets" - Virtual Machine Scale Sets,  and "Microsoft.Web/serverfarms" - Web App</span></span> |
| <span data-ttu-id="ba960-185">resourceId</span><span class="sxs-lookup"><span data-stu-id="ba960-185">resourceId</span></span> |<span data-ttu-id="ba960-186">sì</span><span class="sxs-lookup"><span data-stu-id="ba960-186">Yes</span></span> |<span data-ttu-id="ba960-187">ID di Resource Manager della risorsa di destinazione da ridimensionare</span><span class="sxs-lookup"><span data-stu-id="ba960-187">Resource Manager ID of the target resource that is being scaled</span></span> |
| <span data-ttu-id="ba960-188">portalLink</span><span class="sxs-lookup"><span data-stu-id="ba960-188">portalLink</span></span> |<span data-ttu-id="ba960-189">sì</span><span class="sxs-lookup"><span data-stu-id="ba960-189">Yes</span></span> |<span data-ttu-id="ba960-190">Collegamento del portale di Azure alla pagina di riepilogo della risorsa di destinazione</span><span class="sxs-lookup"><span data-stu-id="ba960-190">Azure portal link to the summary page of the target resource</span></span> |
| <span data-ttu-id="ba960-191">oldCapacity</span><span class="sxs-lookup"><span data-stu-id="ba960-191">oldCapacity</span></span> |<span data-ttu-id="ba960-192">sì</span><span class="sxs-lookup"><span data-stu-id="ba960-192">Yes</span></span> |<span data-ttu-id="ba960-193">Conteggio delle istanze corrente (precedente) quando la scalabilità automatica ha eseguito un'azione di scalabilità</span><span class="sxs-lookup"><span data-stu-id="ba960-193">The current (old) instance count when Autoscale took a scale action</span></span> |
| <span data-ttu-id="ba960-194">newCapacity</span><span class="sxs-lookup"><span data-stu-id="ba960-194">newCapacity</span></span> |<span data-ttu-id="ba960-195">sì</span><span class="sxs-lookup"><span data-stu-id="ba960-195">Yes</span></span> |<span data-ttu-id="ba960-196">Nuovo conteggio delle istanze in base al quale la scalabilità automatica ha ridimensionato la risorsa</span><span class="sxs-lookup"><span data-stu-id="ba960-196">The new instance count that Autoscale scaled the resource to</span></span> |
| <span data-ttu-id="ba960-197">properties</span><span class="sxs-lookup"><span data-stu-id="ba960-197">Properties</span></span> |<span data-ttu-id="ba960-198">No</span><span class="sxs-lookup"><span data-stu-id="ba960-198">No</span></span> |<span data-ttu-id="ba960-199">Facoltativo.</span><span class="sxs-lookup"><span data-stu-id="ba960-199">Optional.</span></span> <span data-ttu-id="ba960-200">Set di coppie <chiave, valore> (ad esempio Dizionario <Stringa, Stringa>).</span><span class="sxs-lookup"><span data-stu-id="ba960-200">Set of <Key, Value> pairs (for example,  Dictionary <String, String>).</span></span> <span data-ttu-id="ba960-201">Il campo properties è facoltativo.</span><span class="sxs-lookup"><span data-stu-id="ba960-201">The properties field is optional.</span></span> <span data-ttu-id="ba960-202">In un flusso di lavoro basato su un'interfaccia utente personalizzata o un'app per la logica, è possibile immettere chiavi e valori che possono essere passati usando il payload.</span><span class="sxs-lookup"><span data-stu-id="ba960-202">In a custom user interface  or Logic app based workflow, you can enter keys and values that can be passed using the payload.</span></span> <span data-ttu-id="ba960-203">Un metodo alternativo per passare le proprietà personalizzate alla chiamata al webhook in uscita è di usare l'URI del webhook stesso (sotto forma di parametri di query)</span><span class="sxs-lookup"><span data-stu-id="ba960-203">An alternate way to pass custom properties back to the outgoing webhook call is to use the webhook URI itself (as query parameters)</span></span> |

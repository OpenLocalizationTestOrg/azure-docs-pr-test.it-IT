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
# <a name="use-autoscale-actions-toosend-email-and-webhook-alert-notifications-in-azure-monitor"></a>Utilizzare scalabilità automatica azioni toosend posta elettronica e ai webhook notifiche di avviso in Monitoraggio di Azure
Questo articolo illustra come configurare i trigger per poter chiamare URL Web specifici o inviare messaggi di posta elettronica in base alle azioni di scalabilità automatica in Azure.  

## <a name="webhooks"></a>Webhook
Webhook consentono di sistemi di tooother tooroute hello Azure notifiche di avviso per le notifiche di post-elaborazione o personalizzate. Ad esempio, routing tooservices avviso hello in grado di gestire un in ingresso web richiesta toosend SMS, i bug di log, inviare una notifica di un team utilizzando chat o servizi di messaggistica, e così via hello webhook URI deve essere un endpoint HTTP o HTTPS valido.

## <a name="email"></a>Email
È possibile inviare tramite posta elettronica tooany indirizzo di posta elettronica valido. Gli amministratori e i coamministratori della sottoscrizione hello in cui è in esecuzione regola hello anche essere avvisati.

## <a name="cloud-services-and-web-apps"></a>Servizi cloud e app Web
È possibile acconsentire esplicitamente dal portale di Azure hello per servizi Cloud e la Server farm (app Web).

* Scegliere hello **scalare** metrica.

![Ridimensiona di](./media/insights-autoscale-to-webhook-email/insights-autoscale-notify.png)

## <a name="virtual-machine-scale-sets"></a>Set di scalabilità di macchine virtuali
Per le macchine virtuali più recenti create con Resource Manager (set di scalabilità di macchine virtuali), è possibile configurare questa opzione tramite l'API REST, i modelli di Resource Manager, PowerShell e l'interfaccia della riga di comando. Un'interfaccia del portale non è ancora disponibile.
Quando si utilizza l'API REST hello o un modello di gestione risorse, includere l'elemento notifiche hello con hello le opzioni seguenti.

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
| Campo | Obbligatorio? | Descrizione |
| --- | --- | --- |
| operation |sì |Il valore deve essere "Scale" |
| sendToSubscriptionAdministrator |sì |Il valore deve essere "true" o "false" |
| sendToSubscriptionCoAdministrators |sì |Il valore deve essere "true" o "false" |
| customEmails |sì |Il valore può essere null [] o la matrice di stringhe di messaggi di posta elettronica |
| Webhook |sì |Il valore può essere null o un URI valido |
| serviceUri |sì |Un URI HTTPS valido |
| properties |sì |Il valore deve essere vuoto {} o può contenere coppie chiave-valore |

## <a name="authentication-in-webhooks"></a>Autenticazione nei webhook
Hello webhook autenticazione utilizzando l'autenticazione basata su token, in cui vengono salvati hello webhook URI con un ID token come un parametro di query. Ad esempio, https://mysamplealert/webcallback?tokenid=sometokenid&someparameter=somevalue

## <a name="autoscale-notification-webhook-payload-schema"></a>Schema di payload del webhook di notifica di scalabilità automatica
Quando viene generata la notifica di scalabilità automatica hello, hello metadati seguenti sono incluse nel payload webhook hello:

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


| Campo | Obbligatorio? | Descrizione |
| --- | --- | --- |
| status |sì |stato Hello che indica che un'azione di scalabilità automatica è stata generata |
| operation |sì |Per un aumento delle istanze, sarà "Scale Out", mentre per una riduzione delle istanze, sarà "Scale In" |
| context |sì |contesto dell'azione di scalabilità automatica Hello |
| timestamp |sì |Timestamp relativo all'azione di scalabilità automatica hello è stata attivata |
| id |Sì |Gestione risorse di ID dell'impostazione di scalabilità automatica hello |
| name |Sì |nome Hello dell'impostazione di scalabilità automatica hello |
| informazioni dettagliate |Sì |Descrizione dell'azione hello che ha richiesto il servizio di scalabilità automatica hello e hello viene modificato il numero di istanze di hello |
| subscriptionId |Sì |ID di sottoscrizione della risorsa di destinazione hello che viene ridimensionato |
| resourceGroupName |Sì |Nome gruppo di risorse della risorsa di destinazione hello che viene ridimensionato |
| resourceName |Sì |Nome della risorsa di destinazione hello che viene ridimensionato |
| resourceType |Sì |Hello tre valori supportati: "microsoft.classiccompute/domainnames/slots/roles" - ruoli servizio Cloud, "microsoft.compute/virtualmachinescalesets" - set di scalabilità di macchine virtuali e "Web/serverfarms" - App Web |
| resourceId |Sì |Gestione risorse di ID della risorsa di destinazione hello che viene ridimensionato |
| portalLink |Sì |Pagina Riepilogo di collegamento del portale Azure toohello della risorsa di destinazione hello |
| oldCapacity |Sì |Hello (precedente) numero di istanze correnti quando scalabilità automatica ha richiesto un'azione di scalabilità |
| newCapacity |Sì |Hello nuovo numero di istanze di scalabilità automatica ridimensionato risorse hello troppo|
| Proprietà |No |Facoltativo. Set di coppie <chiave, valore> (ad esempio Dizionario <Stringa, Stringa>). campo di proprietà Hello è facoltativo. In un'interfaccia utente personalizzata o un flusso di lavoro di logica app in base, è possibile immettere le chiavi e valori che possono essere passati usando payload hello. Un modo alternativo di proprietà personalizzate toopass nuovamente chiamata webhook in uscita toohello è toouse hello webhook URI stesso (come parametri di query) |

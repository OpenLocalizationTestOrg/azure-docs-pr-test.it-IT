---
title: aaaEnable monitoraggio e diagnostica Microsoft Azure | Documenti Microsoft
description: Informazioni su come tooset di diagnostica per le risorse in Azure.
author: rboucher
manager: carolz
editor: 
services: monitoring-and-diagnostics
documentationcenter: monitoring-and-diagnostics
ms.assetid: af1947a9-c211-4aa1-8924-880a86240be4
ms.service: monitoring-and-diagnostics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/06/2017
ms.author: robb
ms.openlocfilehash: 865d010c5846fff6d871e20eca2bc4ac35028354
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="enable-monitoring-and-diagnostics"></a>Abilitare il monitoraggio e la diagnostica
In hello [portale Azure](https://portal.azure.com), è possibile configurare i dati di monitoraggio e diagnostica avanzati, frequenti, sulle risorse. È inoltre possibile utilizzare hello [API REST](https://msdn.microsoft.com/library/azure/dn931932.aspx) o [.NET SDK](http://www.nuget.org/packages/Microsoft.Azure.Management.Monitor) tooconfigure diagnostica a livello di codice.

I dati di diagnostica, di monitoraggio e delle metriche di Azure vengono salvati nell'account di archiviazione preferito. In questo modo è toouse qualsiasi tooling si desidera che i dati di hello tooread, dalla finestra di esplorazione dell'archiviazione, gli strumenti di terze parti toothird BI tooPower.

## <a name="when-you-create-a-resource"></a>Quando si crea una risorsa
La maggior parte dei servizi consentono di diagnostica tooenable quando viene innanzitutto creata in hello [portale Azure](https://portal.azure.com).

1. Andare troppo**New** e hello risorse si è interessati.
2. Selezionare **Configurazione facoltativa**.
    ![Pannello Diagnostica](./media/insights-how-to-use-diagnostics/Insights_CreateTime.png)
3. Selezionare **Diagnostica** e fare clic sull'opzione di **attivazione**. Sarà necessario toochoose hello account di archiviazione che toobe diagnostica salvato. Ti verrà addebitata normali tariffe dati per l'archiviazione e le transazioni quando si invia l'account di archiviazione di diagnostica tooa.
4. Fare clic su **OK** e creare la risorsa hello.

## <a name="change-settings-for-an-existing-resource"></a>Modificare le impostazioni per una risorsa esistente
Se una risorsa è già stato creato e si desidera utilizzare impostazioni di diagnostica hello toochange (livello toochange hello della raccolta di dati, ad esempio), è possibile eseguire nel portale di Azure hello tale diritto.

1. Risorsa toohello, fare clic su hello **impostazioni** comando.
2. Selezionare **Diagnostica**.
3. Hello **diagnostica** pannello dispone di tutte diagnostica hello e monitoraggio dei dati di raccolta per tale risorsa. Per alcune risorse è anche possibile scegliere un **conservazione** criteri per i dati di hello, tooclean, configurarlo dall'account di archiviazione.
    ![Diagnostica dell'archiviazione](./media/insights-how-to-use-diagnostics/Insights_StorageDiagnostics.png)
4. Dopo avere scelto le impostazioni, fare clic su hello **salvare** comando. Potrebbe richiedere un po' per monitoraggio tooshow dati backup se si sta abilitando il hello per la prima volta.

### <a name="categories-of-data-collection-for-virtual-machines"></a>Categorie di raccolta dati per le macchine virtuali
Per le macchine virtuali tutte le metriche e i log verranno registrati a intervalli di un minuto, in modo da poter sempre hello la maggior parte delle informazioni aggiornate relative al computer.

* **Metriche di base** : metriche sull'integrità relative alla macchina virtuale in uso, ad esempio il processore e la memoria
* **Metriche Web e di rete** : metriche relative alle connessioni di rete e ai servizi Web
* **Le metriche .NET** : metriche sulle applicazioni .NET e ASP.NET hello in esecuzione sulla macchina virtuale
* **Metriche di SQL** : metriche delle prestazioni, se si esegue il servizio Microsoft SQL
* **Log eventi dell'applicazione Windows** : eventi di Windows che vengono inviati toohello canale dell'applicazione
* **Log eventi del sistema Windows** : eventi di Windows che vengono inviati toohello canale di sistema. inclusi tutti gli eventi [Microsoft Antimalware](http://go.microsoft.com/fwlink/?LinkID=404171&clcid=0x409)
* **Log eventi di sicurezza Windows** : eventi di Windows che vengono inviati toohello canale di sicurezza
* **Registri infrastruttura diagnostica** : registrazione sull'infrastruttura di raccolta diagnostica hello
* **Log di IIS** : log relativi al server IIS in uso

Si noti che in questo momento non sono supportate alcune distribuzioni di Linux, e, hello agente Guest deve essere installato nella macchina virtuale hello.

## <a name="next-steps"></a>Passaggi successivi
* [Ricevere notifiche di avviso](insights-receive-alert-notifications.md) ogni volta che si verificano eventi operativi o le metriche superano una soglia.
* [Monitorare le metriche di servizio](insights-how-to-customize-monitoring.md) toomake che il servizio sia disponibile e reattiva.
* [Ridimensionamento automatico di conteggio delle istanze](insights-how-to-scale.md) toomake che la scala del servizio in base alle esigenze.
* [Monitorare le prestazioni dell'applicazione](../application-insights/app-insights-azure-web-apps.md) se si desidera toounderstand esattamente come il codice viene eseguito nel cloud hello.
* [Visualizzare eventi e log attività](insights-debugging-with-events.md) toolearn tutto ciò che si è verificato nel servizio.
* [Tenere traccia dell'integrità del servizio](insights-service-health.md) toofind out quando Azure ha riscontrato interruzioni del servizio o una riduzione delle prestazioni.


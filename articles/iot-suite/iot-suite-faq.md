---
title: domande frequenti di IoT Suite aaaAzure | Documenti Microsoft
description: Domande frequenti su IoT Suite
services: 
suite: iot-suite
documentationcenter: 
author: dominicbetts
manager: timlt
editor: 
ms.assetid: cb537749-a8a1-4e53-b3bf-f1b64a38188a
ms.service: iot-suite
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 05/15/2017
ms.author: corywink
ms.openlocfilehash: cb39e24af6d1ce2afea554285512d05b2d7c721e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="frequently-asked-questions-for-iot-suite"></a>Domande frequenti su IoT Suite

Vedere anche, specifici di factory connesso hello [domande frequenti su](iot-suite-faq-cf.md).

### <a name="where-can-i-find-hello-source-code-for-hello-preconfigured-solutions"></a>Dove trovare il codice sorgente hello per le soluzioni hello preconfigurato

codice di origine Hello è archiviato in hello repository GitHub seguente:
* [Soluzione preconfigurata per il monitoraggio remoto][lnk-remote-monitoring-github]
* [Soluzione preconfigurata di manutenzione predittiva][lnk-predictive-maintenance-github]
* [Connected factory preconfigured solution](https://github.com/Azure/azure-iot-connected-factory) (Soluzione preconfigurata di connected factory)

### <a name="how-do-i-update-toohello-latest-version-of-hello-remote-monitoring-preconfigured-solution-that-uses-hello-iot-hub-device-management-features"></a>Come posso aggiornare toohello ultima versione di hello remoto monitoraggio preconfigurato soluzione che utilizza hello funzionalità di gestione dei dispositivi IoT Hub?

* Se si distribuisce una soluzione preconfigurata dal sito https://www.azureiotsuite.com/ hello, distribuisce sempre una nuova istanza della versione più recente di hello della soluzione hello.
* Se si distribuisce una soluzione preconfigurata tramite la riga di comando hello, è possibile aggiornare una distribuzione esistente con il nuovo codice. Vedere [distribuzione Cloud] [ lnk-cloud-deployment] in hello GitHub [repository][lnk-remote-monitoring-github].

### <a name="how-can-i-add-support-for-a-new-device-method-toohello-remote-monitoring-preconfigured-solution"></a>Come è possibile aggiungere il supporto per un nuovo dispositivo metodo toohello soluzione preconfigurata di monitoraggio remoto?

Vedere la sezione hello [aggiungere il supporto per un nuovo simulatore toohello metodo] [ lnk-add-method] in hello [personalizzare una soluzione preconfigurata] [ lnk-customize] articolo.

### <a name="hello-simulated-device-is-ignoring-my-desired-property-changes-why"></a>Ignora le modifiche di proprietà desiderato, il dispositivo simulato Hello perché?
In hello monitoraggio remoto preconfigurato soluzione, il codice di dispositivo simulato hello utilizza solo hello **Desired.Config.TemperatureMeanValue** e **Desired.Config.TelemetryInterval** le proprietà desiderate hello tooupdate segnalato proprietà. Tutte le altre richieste di modifica delle proprietà desiderate vengono ignorate.

### <a name="my-device-does-not-appear-in-hello-list-of-devices-in-hello-solution-dashboard-why"></a>Il dispositivo non viene visualizzato nell'elenco di hello dei dispositivi nel dashboard di soluzione hello, perché?

elenco Hello dei dispositivi nel dashboard di soluzione hello utilizza un elenco di hello tooreturn query di dispositivi. Attualmente, una query non può restituire più di 10.000 dispositivi. Provare a eseguire i criteri di ricerca hello per le query più restrittiva.

### <a name="whats-hello-difference-between-deleting-a-resource-group-in-hello-azure-portal-and-clicking-delete-on-a-preconfigured-solution-in-azureiotsuitecom"></a>Qual è la differenza hello tra l'eliminazione di un gruppo di risorse in Azure nel portale e facendo clic su delete su una soluzione preconfigurata in azureiotsuite.com hello?

* Se si elimina una soluzione di hello preconfigurato in [azureiotsuite.com][lnk-azureiotsuite], si eliminano tutte le risorse di hello che ha effettuato il provisioning durante la creazione di soluzioni hello preconfigurato. Se è stato aggiunto gruppo di risorse toohello risorse aggiuntive, vengono eliminate anche tali risorse. 
* Se si elimina il gruppo di risorse hello in hello [portale di Azure][lnk-azure-portal], si eliminano solo risorse di hello in tale gruppo di risorse. È inoltre necessario associata alla soluzione hello preconfigurato in hello un'applicazione Azure Active Directory hello toodelete [portale di Azure classico][lnk-classic-portal].

### <a name="how-many-iot-hub-instances-can-i-provision-in-a-subscription"></a>Di quante istanze dell'hub IoT è possibile eseguire il provisioning in una sottoscrizione?

Per impostazione predefinita, è possibile eseguire il provisioning di [10 hub IoT per ogni sottoscrizione][link-azuresublimits]. È possibile creare un [ticket di supporto tecnico di Azure] [ link-azuresupportticket] tooraise questo limite. Di conseguenza, poiché ogni disposizioni soluzione preconfigurata un nuovo IoT Hub, è possibile solo effettuare il provisioning di too10 preconfigurato soluzioni in una specifica sottoscrizione. 

### <a name="how-many-azure-cosmos-db-instances-can-i-provision-in-a-subscription"></a>Di quante istanze di Azure Cosmos DB è possibile effettuare il provisioning in una sottoscrizione?

Cinquanta. È possibile creare un [ticket di supporto tecnico di Azure] [ link-azuresupportticket] tooraise questo limite, ma per impostazione predefinita, è possibile fornire solo 50 istanze DB Cosmos per ogni sottoscrizione. 

### <a name="how-many-free-bing-maps-apis-can-i-provision-in-a-subscription"></a>Di quante API di Bing Maps gratuite è possibile eseguire il provisioning in una sottoscrizione?

Due. È possibile creare solo due Transazioni sito Web interno - Livello 1 per Bing Maps per i piani aziendali in una sottoscrizione di Azure. soluzione di monitoraggio remoto Hello viene eseguito il provisioning per impostazione predefinita con piano hello interna 1 livello di transazioni. Di conseguenza, è possibile fornire solo backup tootwo soluzioni in una sottoscrizione senza modifiche di monitoraggio remoto.

### <a name="i-have-a-remote-monitoring-solution-deployment-with-a-static-map-how-do-i-add-an-interactive-bing-map"></a>Se si usa la distribuzione di soluzioni di monitoraggio remoto con una mappa statica, come si aggiunge una mappa di Bing interattiva?

1. È possibile ottenere la chiave QueryKey di Bing Maps API for Enterprise dal [portale di Azure][lnk-azure-portal]: 
   
   1. Passare il gruppo di risorse in cui l'API di Bing Maps per Enterprise è in hello toohello [portale di Azure][lnk-azure-portal].
   2. Fare clic su **All Settings** (Tutte le impostazioni) e quindi su **Key Management** (Gestione chiavi). 
   3. Vengono visualizzate le due chiavi **MasterKey** e **QueryKey**. Copiare il valore di hello per **QueryKey**.
      
      > [!NOTE]
      > Se non si ha un account Bing Maps API for Enterprise, Crearne una nel hello [portale di Azure] [ lnk-azure-portal] facendo clic su + nuova, la ricerca di API di Bing Maps per l'organizzazione e seguire richiede toocreate.
      > 
      > 
2. Verso il basso il codice più recente di hello da hello [Azure IoT-remoto Monitoring][lnk-remote-monitoring-github].
3. Esecuzione locale o nel cloud di distribuzione seguente Guida alla distribuzione della riga di comando hello nella cartella /docs/ hello nel repository di hello. 
4. Dopo aver eseguito una variabile locale o cloud di distribuzione, cercare nella cartella radice per hello *. file User. config creato durante la distribuzione. Aprire il file in un editor di testo. 
5. Il valore di hello tooinclude copiato nelle righe seguenti hello di modifica del **QueryKey**: 
   
   `<setting name="MapApiQueryKey" value="" />`

### <a name="can-i-create-a-preconfigured-solution-if-i-have-microsoft-azure-for-dreamspark"></a>È possibile creare una soluzione preconfigurata se è disponibile Microsoft Azure per DreamSpark?

Al momento non è possibile creare una soluzione preconfigurata con un account [Microsoft Azure for DreamSpark][lnk-dreamspark], ma è possibile creare facilmente un [account di valutazione gratuito per][lnk-30daytrial] che consente di creare una soluzione preconfigurata.

### <a name="can-i-create-a-preconfigured-solution-if-i-have-cloud-solution-provider-csp-subscription"></a>È possibile creare una soluzione preconfigurata se si dispone di una sottoscrizione di Cloud Solution Provider?

È possibile attualmente creare una soluzione preconfigurata con una sottoscrizione di Cloud Solution Provider, ma è possibile creare facilmente un [account di valutazione gratuito per][lnk-30daytrial] che consente di creare una soluzione preconfigurata.

### <a name="how-do-i-delete-an-aad-tenant"></a>Come si elimina un tenant AAD?

Vedere il post del blog di Eric Golpe relativo alla [procedura dettagliata di eliminazione di un tenant di Azure AD][lnk-delete-aad-tennant].

### <a name="next-steps"></a>Passaggi successivi

È anche possibile esplorare alcune hello altre caratteristiche e funzionalità di soluzioni di IoT Suite preconfigurato hello:

* [Panoramica della soluzione preconfigurata di manutenzione predittiva][lnk-predictive-overview]
* [Panoramica della soluzione preconfigurata di connected factory](iot-suite-connected-factory-overview.md)
* [Sicurezza di IoT da hello messa a terra][lnk-security-groundup]

[lnk-predictive-overview]: iot-suite-predictive-overview.md
[lnk-security-groundup]: securing-iot-ground-up.md

[link-azuresupportticket]: https://portal.azure.com/#blade/Microsoft_Azure_Support/HelpAndSupportBlade 
[link-azuresublimits]: https://azure.microsoft.com/documentation/articles/azure-subscription-service-limits/#iot-hub-limits
[lnk-azure-portal]: https://portal.azure.com
[lnk-azureiotsuite]: https://www.azureiotsuite.com/
[lnk-classic-portal]: https://manage.windowsazure.com
[lnk-remote-monitoring-github]: https://github.com/Azure/azure-iot-remote-monitoring 
[lnk-dreamspark]: https://www.dreamspark.com/Product/Product.aspx?productid=99 
[lnk-30daytrial]: https://azure.microsoft.com/free/
[lnk-delete-aad-tennant]: http://blogs.msdn.com/b/ericgolpe/archive/2015/04/30/walkthrough-of-deleting-an-azure-ad-tenant.aspx
[lnk-cloud-deployment]: https://github.com/Azure/azure-iot-remote-monitoring/blob/master/Docs/cloud-deployment.md
[lnk-add-method]: iot-suite-guidance-on-customizing-preconfigured-solutions.md#add-support-for-a-new-method-to-the-simulator
[lnk-customize]: iot-suite-guidance-on-customizing-preconfigured-solutions.md
[lnk-remote-monitoring-github]: https://github.com/Azure/azure-iot-remote-monitoring
[lnk-predictive-maintenance-github]: https://github.com/Azure/azure-iot-predictive-maintenance

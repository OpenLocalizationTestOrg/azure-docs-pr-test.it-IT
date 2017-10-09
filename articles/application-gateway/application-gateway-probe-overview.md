---
title: Panoramica del monitoraggio per il Gateway applicazione Azure aaaHealth | Documenti Microsoft
description: "Informazioni su hello monitoraggio funzionalità di Gateway applicazione Azure"
services: application-gateway
documentationcenter: na
author: georgewallace
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 7eeba328-bb2d-4d3e-bdac-7552e7900b7f
ms.service: application-gateway
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 12/14/2016
ms.author: gwallace
ms.openlocfilehash: 5091d80394a354ff849ce7ccee8cc9d2fd0456db
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="application-gateway-health-monitoring-overview"></a>Panoramica del monitoraggio dell'integrità del gateway applicazione

Gateway applicazione Azure per impostazione predefinita Controlla integrità hello di tutte le risorse nel relativo pool back-end e rimuove automaticamente qualsiasi risorsa considerato non integro dal pool hello. Gateway applicazione continua a istanze di tipo non integro hello toomonitor e li aggiunge eseguire il pool back-end integro toohello quando diventano disponibili e rispondono toohealth probe. Gateway applicazione invia hello probe di integrità con hello è definita nelle impostazioni HTTP back-end di hello stessa porta. Questa configurazione assicura che probe hello è test hello stessa porta che i clienti utilizzassero back-end toohello tooconnect.

![Esempio di probe del gateway applicazione][1]

In aggiunta toousing predefinito probe monitoraggio dell'integrità, è anche possibile personalizzare toosuit probe di integrità hello i requisiti dell'applicazione. In questo articolo vengono illustrati i probe di integrità predefiniti e personalizzati.

> [!NOTE]
> Se nella subnet del Gateway applicazione è presente un gruppo, gli intervalli di porte 65503 65534 devono essere aperta sulla subnet di Gateway applicazione hello per il traffico in ingresso. Queste porte sono obbligatorie per hello back-end integrità API toowork.

## <a name="default-health-probe"></a>Probe di integrità predefinito

Un gateway applicazione configura automaticamente un probe di integrità predefinito quando non si configura nessuna configurazione di probe personalizzato. Hello monitoraggio comportamento consente di rendere che gli indirizzi IP toohello richiesta HTTP configurati per il pool back-end hello. Per le ricerche predefinito se le impostazioni http back-end di hello sono configurate per HTTPS, probe hello usa HTTPS come integrità tootest e di back-end hello.

Ad esempio: configurare l'applicazione gateway toouse server back-end A, B e C tooreceive HTTP il traffico di rete sulla porta 80. il monitoraggio dello stato predefinito di Hello verifica tre server hello ogni 30 secondi per una risposta HTTP integro. Una risposta HTTP integra ha un [codice di stato](https://msdn.microsoft.com/library/aa287675.aspx) compreso tra 200 e 399.

Se il controllo di probe predefinito hello non riesce per server A, gateway applicazione hello rimuoverlo dal pool back-end e il traffico di rete viene interrotto il flusso di toothis server. probe predefinito Hello continuerà toocheck per server un ogni 30 secondi. Quando il server A risponde correttamente tooone richiesta da un probe di integrità predefinito, viene aggiunto nuovamente come pool back-end toohello integra e avvia il traffico propagazione server toohello nuovamente.

### <a name="default-health-probe-settings"></a>Impostazioni del probe di integrità predefinito

| Proprietà probe | Valore | Descrizione |
| --- | --- | --- |
| URL probe |http://127.0.0.1:\<porta\>/ |Percorso URL |
| Interval |30 |Intervallo di probe in secondi |
| Timeout |30 |Timeout di probe in secondi |
| Soglia non integra |3 |Numero di tentativi di probe. server di back-end Hello è contrassegnato come inattivo dopo il conteggio degli errori di probe consecutivi hello raggiunge la soglia non integra hello. |

> [!NOTE]
> Hello porta è hello stessa porta come impostazioni HTTP back-end di hello.

probe predefinito Hello esamina solo http://127.0.0.1:\<porta\> toodetermine lo stato di integrità. Se è necessario tooconfigure hello integrità toogo tooa personalizzato URL del probe o modificare altre impostazioni, è necessario utilizzare un probe personalizzato come descritto in hello alla procedura seguente:

## <a name="custom-health-probe"></a>Probe di integrità personalizzato

Probe personalizzati consentono un controllo più granulare sul monitoraggio dello stato di hello toohave. Quando si utilizzano probe personalizzati, è possibile configurare l'intervallo di probe hello tootest URL e il percorso di hello e quanti tooaccept risposte non riuscito prima di contrassegnare l'istanza del pool back-end di hello come non integro.

### <a name="custom-health-probe-settings"></a>Impostazioni del probe di integrità personalizzato

Hello nella tabella seguente vengono fornite le definizioni per le proprietà di hello un probe di stato personalizzati.

| Proprietà probe | Descrizione |
| --- | --- |
| Nome |Nome del probe hello. Questo nome è di tipo probe toohello toorefer utilizzati nelle impostazioni HTTP back-end. |
| Protocol |Protocollo utilizzato probe hello toosend. probe Hello hello protocollo definito nelle impostazioni HTTP back-end di hello |
| Host |Probe di hello toosend nome host. Applicabile solo quando vengono configurati più siti nel gateway applicazione. In caso contrario, usare "127.0.0.1". Questo valore è diverso dal nome host della VM. |
| Path |Percorso relativo del probe hello. path valido Hello inizia con '/'. |
| Interval |Intervallo di probe in secondi. Questo valore è l'intervallo di tempo hello tra due probe consecutivi. |
| Timeout |Timeout del probe in secondi. Se una risposta valida non viene ricevuta entro questo periodo di timeout, probe hello è contrassegnato come non riuscito.  |
| Soglia non integra |Numero di tentativi di probe. server di back-end Hello è contrassegnato come inattivo dopo il conteggio degli errori di probe consecutivi hello raggiunge la soglia non integra hello. |

> [!IMPORTANT]
> Se il Gateway applicazione è configurato per un singolo sito, da hello predefinito Host nome deve essere specificato come '127.0.0.1', se non diversamente configurato in probe personalizzato.
> Per il riferimento viene inviato un probe personalizzato\<protocollo\>://\<host\>:\<porta\>\<percorso\>. Hello porta utilizzata sarà hello stessa porta, come definito nelle impostazioni HTTP back-end di hello.

## <a name="next-steps"></a>Passaggi successivi
Dopo aver imparare il monitoraggio dello stato di Gateway applicazione, è possibile configurare un [probe di integrità personalizzato](application-gateway-create-probe-portal.md) nel portale di Azure hello o un [probe di integrità personalizzato](application-gateway-create-probe-ps.md) tramite PowerShell e hello Azure Resource Manager modello di distribuzione.

[1]: ./media/application-gateway-probe-overview/appgatewayprobe.png

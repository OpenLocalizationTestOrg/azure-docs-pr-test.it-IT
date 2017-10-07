---
title: impostazioni di metrica e la posizione di aaaSpecify microservizi Azure | Documenti Microsoft
description: Descrive un servizio di Service Fabric specificando metriche, vincoli di posizionamento e altri criteri di posizionamento.
services: service-fabric
documentationcenter: .net
author: masnider
manager: timlt
editor: 
ms.assetid: 16e135c1-a00a-4c6f-9302-6651a090571a
ms.service: Service-Fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 08/18/2017
ms.author: masnider
ms.openlocfilehash: c633518b5dbf0c7b84e0d46c06bf1f92365d184d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="configuring-cluster-resource-manager-settings-for-service-fabric-services"></a>Configurazione delle impostazioni di Cluster Resource Manager per i servizi Service Fabric
Hello servizio di gestione delle risorse Cluster dell'infrastruttura consente un controllo accurato regole hello che regolano ogni singolo utente denominato "service". Ogni servizio in questione è possibile specificare regole per la modalità deve essere allocata in cluster hello. Ogni servizio in questione è inoltre possibile definire set di hello di metriche che desideri tooreport, tra cui il livello di importanza sono toothat servizio. La configurazione dei servizi prevede tre diverse attività:

1. Configurazione dei vincoli di posizionamento
2. Configurazione delle metriche
3. Configurazione dei criteri di posizionamento avanzati e di altre regole (meno comune)

## <a name="placement-constraints"></a>Vincoli di posizionamento
Vincoli di posizionamento sono utilizzati toocontrol quali nodi cluster hello effettivamente esecuzione di un servizio. In genere un determinato nome istanza del servizio o tutti i servizi di un determinato tipo vincolato di toorun su un particolare tipo di nodo. I vincoli di posizionamento sono estendibili. È possibile definire qualsiasi set di proprietà per ogni tipo di nodo e quindi selezionarle con i vincoli durante la creazione di servizi. È inoltre possibile modificare i vincoli di posizionamento di un servizio mentre è in esecuzione. In questo modo toochanges toorespond in cluster hello hello requisiti o del servizio hello. proprietà Hello di un determinato nodo può essere aggiornata in modo dinamico anche cluster hello. Ulteriori informazioni sui vincoli di posizionamento e come tooconfigure li è reperibile [in questo articolo](service-fabric-cluster-resource-manager-cluster-description.md#node-properties-and-placement-constraints)

## <a name="metrics"></a>Metrica
Le metriche sono set di hello delle risorse necessarie per un servizio denominato specificato. La configurazione delle metriche di un servizio include informazioni relative alla quantità della risorsa che ogni replica con stato o istanza senza stato usa per impostazione predefinita. Le metriche includono anche un valore che indica l'importanza bilanciamento del carico tale metrica servizio toothat, nel caso in cui sono necessari compromessi.

## <a name="advanced-placement-rules"></a>Regole di posizionamento avanzate
Sono disponibili altri tipi di regole di posizionamento che sono utili negli scenari meno comuni. Di seguito sono riportati alcuni esempi:
- Vincoli che sono di ausilio con i cluster geograficamente distribuiti
- Determinate architetture di applicazioni

Altre regole di posizionamento sono configurate tramite correlazioni o criteri.

## <a name="next-steps"></a>Passaggi successivi
- Le metriche sono la modalità di gestione di consumo e la capacità in cluster hello in hello gestore di risorse Cluster dell'infrastruttura del servizio. ulteriori informazioni sulle metriche toolearn come tooconfigure, archiviazione ed estrazione [in questo articolo](service-fabric-cluster-resource-manager-metrics.md)
- L'affinità è un modo di configurare i servizi. Non è un'operazione frequente, ma se necessario sono disponibili altre informazioni [qui](service-fabric-cluster-resource-manager-advanced-placement-rules-affinity.md)
- Sono disponibili molte regole di selezione host diversi che possono essere configurate in scenari aggiuntivi di toohandle del servizio. È possibile trovare informazioni sui vari criteri di posizionamento [qui](service-fabric-cluster-resource-manager-advanced-placement-rules-placement-policies.md)
- Iniziare dall'inizio hello e [ottenere un servizio di gestione delle risorse Cluster dell'infrastruttura di toohello introduzione](service-fabric-cluster-resource-manager-introduction.md)
- toofind out sulla modalità di gestione delle risorse Cluster hello gestisce e bilancia il carico nel cluster hello, controllare l'articolo hello [bilanciamento del carico](service-fabric-cluster-resource-manager-balancing.md)
- Hello gestione delle risorse Cluster dispone di numerose opzioni per la descrizione del cluster di hello. toofind ulteriori informazioni, consultare questo articolo in [che descrive un cluster di Service Fabric](service-fabric-cluster-resource-manager-cluster-description.md)

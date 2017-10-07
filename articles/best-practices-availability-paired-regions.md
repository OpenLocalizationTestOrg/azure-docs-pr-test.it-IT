---
title: "Continuità aziendale e ripristino di emergenza nelle aree abbinate di Azure | Documentazione Microsoft"
description: Informazioni su Azure regionale tooensure di associazione, che le applicazioni siano resilienti guasti del centro dati.
services: site-recovery
documentationcenter: 
author: rayne-wiselman
manager: cfreeman
editor: 
ms.assetid: c2d0a21c-2564-4d42-991a-bc31723f61a4
ms.service: site-recovery
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/23/2017
ms.author: raynew
ms.openlocfilehash: 68a3a33a8e768c72fa296d42c9ab97049232d169
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="business-continuity-and-disaster-recovery-bcdr-azure-paired-regions"></a>Continuità aziendale e ripristino di emergenza nelle aree geografiche abbinate di Azure

## <a name="what-are-paired-regions"></a>Definizione di aree abbinate

Azure viene eseguita in più aree geografiche in tutto il mondo hello. Un'area geografica di Azure è un'area definita di hello world contenente almeno un'area di Azure. Un'area di Azure all'interno di un'area geografica include uno o più data center.

Ogni area di Azure è associato a un'altra area all'interno di hello stesso geografia, rendendo insieme una coppia internazionale. eccezione di Hello è Brasile meridionale, cui è associato a un'area di fuori di relativo geography.

![AzureGeography](./media/best-practices-availability-paired-regions/GeoRegionDataCenter.png)

Figura 1: Diagramma di una coppia di aree di Azure

| Area geografica | Aree abbinate |  |
|:--- |:--- |:--- |
| Asia |Asia orientale |Asia sudorientale |
| Australia |Australia orientale |Australia sudorientale |
| Canada |Canada centrale |Canada orientale |
| Cina |Cina settentrionale |Cina orientale|
| India |India centrale |India meridionale |
| Giappone |Giappone orientale |Giappone occidentale |
| Corea |Corea centrale |Corea meridionale |
| America del Nord |Stati Uniti centro-settentrionali |Stati Uniti centro-meridionali |
| America del Nord |Stati Uniti orientali |Stati Uniti occidentali |
| America del Nord |Stati Uniti orientali 2 |Stati Uniti centrali |
| America del Nord |Stati Uniti occidentali 2 |Stati Uniti centro-occidentali |
| Europa |Europa settentrionale |Europa occidentale |
| Giappone |Giappone orientale |Giappone occidentale |
| Brasile |Brasile meridionale (1) |Stati Uniti centro-meridionali |
| Governo degli Stati Uniti |Governo degli Stati Uniti - Iowa |Governo degli Stati Uniti - Virginia |
| Governo degli Stati Uniti |Governo degli Stati Uniti - Virginia |Governo degli Stati Uniti - Texas |
| Governo degli Stati Uniti |Governo degli Stati Uniti - Texas |Governo degli Stati Uniti - Arizona |
| Governo degli Stati Uniti |Governo degli Stati Uniti - Arizona |Governo degli Stati Uniti - Texas |
| Regno Unito |Regno Unito occidentale |Regno Unito meridionale |
| Germania |Germania centrale |Germania nord-orientale |

Tabella 1 - Mapping di coppie di aree di Azure

> (1) L'area Brasile meridionale è unica, perché è abbinata a un'area esterna alla propria area geografica. L'area secondaria del Brasile meridionale sono gli Stati Uniti centro-meridionali, ma l'area secondaria degli Stati Uniti centro-meridionali non è il Brasile meridionale.


Si consiglia di replicare i carichi di lavoro tra toobenefit internazionali coppie dai criteri di isolamento e la disponibilità di Azure. Ad esempio, gli aggiornamenti pianificati del sistema Azure vengono distribuiti in modo sequenziale (non a hello contemporaneamente) tra aree abbinate. Ciò significa che anche nell'evento raro di hello di un aggiornamento errato, entrambe le aree non saranno interessate contemporaneamente. Inoltre, in caso di guasto di hello di un'interruzione ampia, ripristino di almeno un'area da ogni coppia è una priorità.

## <a name="an-example-of-paired-regions"></a>Esempio di aree abbinate
Figura 2 mostra un'ipotetica applicazione che utilizza coppia internazionali hello per il ripristino di emergenza. numeri verdi Hello evidenziare le attività tra aree hello di tre servizi di Azure (Azure di calcolo, archiviazione e database) e il modo in cui configurato tooreplicate in aree geografiche. vantaggi esclusivi di Hello di distribuzione tra aree abbinate sono evidenziati dai numeri hello arancione.

![Panoramica dei vantaggi delle aree abbinate](./media/best-practices-availability-paired-regions/PairedRegionsOverview2.png)

Figura 2: ipotetica coppia di aree di Azure

## <a name="cross-region-activities"></a>Attività tra aree
Come tooin cui viene fatto riferimento nella figura 2.

![PaaS](./media/best-practices-availability-paired-regions/1Green.png) **calcolo di Azure (PaaS)** : È necessario eseguire il provisioning di risorse di calcolo aggiuntive in anticipo tooensure risorse disponibili in un'altra area durante un'emergenza. Per altre informazioni, vedere [Informazioni tecniche sulla resilienza di Azure](resiliency/resiliency-technical-guidance.md).

![Archiviazione](./media/best-practices-availability-paired-regions/2Green.png) **Archiviazione di Azure**: per impostazione predefinita, quando si crea un account di archiviazione di Azure viene configurata l'archiviazione con ridondanza geografica. Con l'archiviazione con ridondanza geografica, i dati vengono automaticamente replicati tre volte nell'area primaria hello e tre volte nell'area abbinata hello. Per altre informazioni, vedere [Opzioni di ridondanza di Archiviazione di Azure](storage/common/storage-redundancy.md).

![SQL Azure](./media/best-practices-availability-paired-regions/3Green.png) **database SQL di Azure** : con Azure SQL replica geografica Standard, è possibile configurare la replica asincrona di area abbinata tooa di transazioni. Con la replica-premium, è possibile configurare l'area tooany replica in HelloWorld; Tuttavia, è consigliabile che distribuire queste risorse in un'area associata per la maggior parte degli scenari di ripristino di emergenza. Per altre informazioni, vedere l'articolo relativo alla [replica geografica nel database SQL di Azure](sql-database/sql-database-geo-replication-overview.md).

![Resource Manager](./media/best-practices-availability-paired-regions/4Green.png)**Azure Resource Manager**: Resource Manager fornisce implicitamente l'isolamento logico dei componenti di gestione del servizio tra le aree. Questo significa che gli errori di logici in un'unica area sono tooimpact meno probabile che un altro.

## <a name="benefits-of-paired-regions"></a>Vantaggi delle aree abbinate
Come tooin cui viene fatto riferimento nella figura 2.  

![Isolamento](./media/best-practices-availability-paired-regions/5Orange.png)
**Isolamento fisico**: quando possibile, per Azure è preferibile una separazione di almeno 480 km tra i data center di una coppia di aree, anche se ciò non è sempre pratico o possibile in tutte le aree geografiche. La separazione dei Data Center fisico riduce il rischio di hello di calamità naturali, unrest civile, interruzioni dell'alimentazione o interruzioni della rete fisica che interessano entrambe le aree in una sola volta. L'isolamento è vincoli toohello soggetto geography hello (dimensione geography, disponibilità di alimentazione/di rete dell'infrastruttura, normative e così via).  

![Replica](./media/best-practices-availability-paired-regions/6Orange.png)
**fornita dalla piattaforma replica** -area abbinata di replica automatica toohello di fornire alcuni servizi, ad esempio l'archiviazione con ridondanza geografica.

![Ripristino](./media/best-practices-availability-paired-regions/7Orange.png)
**ordine ripristino area** – nell'evento hello di un'interruzione ampia, ripristino di un'area è assegnata la priorità da ogni coppia. Le applicazioni che vengono distribuite tra più aree abbinate sono garantite toohave una delle aree di hello recuperata con priorità. Se un'applicazione viene distribuita tra le aree che non sono abbinate, ripristino può essere ritardato: hello peggiore aree scelto hello case possono essere hello toobe ultime due recuperato.

![Aggiornamenti](./media/best-practices-availability-paired-regions/8Orange.png)
**aggiornamenti sequenziali** : gli aggiornamenti del sistema Azure pianificati vengono implementati in modo sequenziale aree toopaired (non a hello contemporaneamente) toominimize i tempi di inattività, effetto hello di bug ed errori logici nell'evento raro hello di un aggiornamento non valido.

![Dati](./media/best-practices-availability-paired-regions/9Orange.png)
**residenza dati** : un'area si trova all'interno di hello stesso geography come la relativa coppia (con eccezione hello del Brasile meridionale) ordine toomeet dati residenza dei requisiti per le imposte e il diritto a scopo di competenza imposizione.

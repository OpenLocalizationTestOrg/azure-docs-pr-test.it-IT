---
title: pool di agenti aaaDC/del sistema operativo per il servizio contenitore di Azure | Documenti Microsoft
description: Funzionamento dei pool di agenti pubbliche e private di hello con un cluster di Azure contenitore del servizio controller di dominio o del sistema operativo
services: container-service
documentationcenter: 
author: dlepow
manager: timlt
editor: 
tags: acs, azure-container-service
keywords: Docker, Contenitori, Micro-servizi, Mesos, Azure
ms.service: container-service
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 01/04/2017
ms.author: danlep
ms.custom: mvc
ms.openlocfilehash: c7d3889db07cb9908e8b68b668bd8a14ef3c2552
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="dcos-agent-pools-for-azure-container-service"></a>Pool di agenti DC/OS per il servizio contenitore di Azure
I cluster DC/OS nel servizio contenitore di Azure contengono nodi di agenti in due pool, uno pubblico e uno privato. Un'applicazione può essere distribuita tooeither pool, avere effetto sull'accessibilità tra i computer nel servizio contenitore. Hello macchine possono essere esposto toohello internet (pubblica) o interno (privato). Questo articolo descrive brevemente il motivo per cui esistono i pool pubblici e i pool privati.


* **Agenti privati**: i nodi di agenti privati vengono eseguiti tramite una rete non instradabile, Questa rete è accessibile solo dall'area di amministrazione di hello o tramite router perimetrale di hello zona pubblico. Per impostazione predefinita, il DC/OS avvia le applicazioni in nodi di agenti privati. 

* **Agenti pubblici**: i nodi di agenti pubblici eseguono app e servizi DC/OS attraverso una rete accessibile pubblicamente. 

Per ulteriori informazioni sulla sicurezza di rete di controller di dominio o del sistema operativo, vedere hello [documentazione DC/OS](https://dcos.io/docs/1.7/administration/securing-your-cluster/).

## <a name="deploy-agent-pools"></a>Distribuire pool di agenti

pool di agenti Hello controller di dominio o del sistema operativo del servizio di contenitore di Azure vengono creati come indicato di seguito:

* Hello **pool privata** contiene il numero di hello di nodi di agente che si specifica quando si [distribuire cluster di controller di dominio/OS hello](container-service-deployment.md). 

* Hello **pool pubblica** inizialmente contiene un numero predeterminato di nodi dell'agente. Il pool viene aggiunto automaticamente quando viene eseguito il provisioning di cluster di controller di dominio/OS hello.

pool privata Hello e pool pubblica hello sono set di scalabilità di macchine virtuali di Azure. È possibile ridimensionare questi pool dopo la distribuzione.

## <a name="use-agent-pools"></a>Uso dei pool di agenti
Per impostazione predefinita, **maratona** consente di distribuire qualsiasi nuova toohello applicazione *privata* nodi agente. Si dispone di tooexplicitly distribuire toohello applicazione hello *pubblica* nodi durante la creazione di un'applicazione hello hello. Seleziona hello **facoltativo** scheda e immettere **slave_public** per hello **accettato ruoli risorse** valore. Questo processo è documentato [qui](container-service-mesos-marathon-ui.md#deploy-a-docker-formatted-container) e hello [DC/OS](https://dcos.io/docs/1.7/administration/installing/custom/create-public-agent/) documentazione.

## <a name="next-steps"></a>Passaggi successivi
* Sono disponibili altre informazioni sulla [gestione dei contenitori DC/OS](container-service-mesos-marathon-ui.md).

* Informazioni su come troppo[aprire hello firewall](container-service-enable-public-access.md) fornito dai contenitori di Azure tooallow accesso pubblico tooyour controller di dominio o del sistema operativo.


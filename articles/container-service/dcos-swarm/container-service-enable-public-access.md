---
title: aaaEnable accesso tooAzure controller di dominio o del sistema operativo contenitore app | Documenti Microsoft
description: Come pubblico tooenable accedere ai contenitori di tooDC/OS contenitore nel servizio di Azure.
services: container-service
documentationcenter: 
author: sauryadas
manager: madhana
editor: 
tags: acs, azure-container-service
keywords: Docker, Contenitori, Micro-servizi, Mesos, Azure
ms.service: container-service
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/26/2016
ms.author: saudas
ms.custom: mvc
ms.openlocfilehash: 1ba251ba5a176a6a5e1c7831655164e380a62b27
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="enable-public-access-tooan-azure-container-service-application"></a>Abilitare l'applicazione del servizio di contenitore di Azure tooan accesso pubblico
Qualsiasi contenitore di controller di dominio/OS hello ACS [pool di agenti pubblica](container-service-mesos-marathon-ui.md#deploy-a-docker-formatted-container) viene automaticamente esposta toohello internet. Per impostazione predefinita, le porte **80**, **443**, **8080** sono aperte e qualsiasi contenitore (pubblico) in ascolto su queste porte è accessibile. Questo articolo illustra come tooopen più porte per le applicazioni nel servizio contenitore di Azure.

## <a name="open-a-port-portal"></a>Aprire una porta (portale)
Innanzitutto, è necessario porta hello tooopen desiderato.

1. Accedi a portale toohello.
2. Trovare il gruppo di risorse hello distribuito hello servizio contenitore di Azure.
3. Selezionare servizio di bilanciamento del carico agente hello (denominato simile troppo**lb-XXXX-XXXX-agente**).
   
    ![Servizio di bilanciamento del carico del servizio contenitore di Azure](./media/container-service-enable-public-access/agent-load-balancer.png)
4. Fare clic su **Probe** e quindi su **Aggiungi**.
   
    ![Probe del servizio di bilanciamento del carico del servizio contenitore di Azure](./media/container-service-enable-public-access/add-probe.png)
5. Compilazione del modulo probe hello e fare clic su **OK**.
   
   | Campo | Descrizione |
   | --- | --- |
   | Nome |Un nome descrittivo del probe hello. |
   | Porta |porta Hello hello contenitore tootest. |
   | Path |(In modalità HTTP) hello tooprobe percorso relativo del sito Web. HTTPS non è supportato. |
   | Interval |Hello tempo tra probe tentativi, in secondi. |
   | Soglia non integra |Numero di probe consecutivi tentativi prima che venga considerato non integro contenitore hello. |
6. Nella proprietà hello di bilanciamento del carico di hello agente, fare clic su **regole di bilanciamento del carico** e quindi **Aggiungi**.
   
    ![Regole del servizio di bilanciamento del carico del servizio contenitore di Azure](./media/container-service-enable-public-access/add-balancer-rule.png)
7. Compilazione del modulo del servizio di bilanciamento carico di hello e fare clic su **OK**.
   
   | Campo | Descrizione |
   | --- | --- |
   | Nome |Nome descrittivo del servizio di bilanciamento del carico hello. |
   | Porta |porta in ingresso Hello pubblica. |
   | Porta back-end |porta interna pubblico di Hello del hello contenitore tooroute del traffico. |
   | Pool back-end |contenitori di Hello in questo pool sarà destinazione hello per il bilanciamento del carico. |
   | Probe |Hello toodetermine probe utilizzata se una destinazione in hello **pool back-end** è integro. |
   | Persistenza della sessione |Determina la modalità di gestione traffico da un client per la durata di hello della sessione hello.<br><br>**Nessuna**: richieste Successive provenienti dallo stesso client può essere gestita da qualsiasi contenitore hello.<br>**Client IP**: richieste Successive provenienti dallo stesso indirizzo IP del client vengono gestiti da hello hello stesso contenitore.<br>**Client IP e protocollo**: le richieste Successive dalla stessa combinazione di indirizzo IP e protocollo client vengono gestiti da hello hello stesso contenitore. |
   | Timeout di inattività |(Solo TCP) In minuti, hello tookeep ora aprire un client TCP o HTTP senza basarsi su *keep-alive* messaggi. |

## <a name="add-a-security-rule-portal"></a>Aggiungere una regola di sicurezza (portale)
È quindi necessario tooadd una regola di sicurezza che instrada il traffico dal nostro porta aperta attraverso il firewall hello.

1. Accedi a portale toohello.
2. Trovare il gruppo di risorse hello distribuito hello servizio contenitore di Azure.
3. Seleziona hello **pubblica** gruppo di sicurezza di rete dell'agente (denominato simile troppo**XXXX-agent-public-gruppo-XXXX**).
   
    ![Gruppo di sicurezza di rete del servizio contenitore di Azure](./media/container-service-enable-public-access/agent-nsg.png)
4. Selezionare **Regole di sicurezza in ingresso** e quindi fare clic su **Aggiungi**.
   
    ![Regole del gruppo di sicurezza di rete del servizio contenitore di Azure](./media/container-service-enable-public-access/add-firewall-rule.png)
5. Compilare tooallow regola firewall di hello la porta pubblica e fare clic su **OK**.
   
   | Campo | Descrizione |
   | --- | --- |
   | Nome |Un nome descrittivo della regola firewall hello. |
   | Priorità |Priorità per la regola hello. Hello hello numero hello superiore hello priorità inferiore. |
   | Sorgente |Limitare hello in arrivo IP indirizzo intervallo toobe consentito o negato da questa regola. Utilizzare **qualsiasi** toonot specificare una restrizione. |
   | Service |Selezionare un set di servizi predefiniti a cui è destinata questa regola di sicurezza. In caso contrario utilizzare **personalizzato** toocreate personalizzati. |
   | Protocol |Consente di limitare il traffico in base a **TCP** o **UDP**. Utilizzare **qualsiasi** toonot specificare una restrizione. |
   | Intervallo di porte |Quando **servizio** è **personalizzata**, specifica l'intervallo di hello di porte che influisce su questa regola. È possibile usare una singola porta, ad esempio **80**, o un intervallo come **1024-1500**. |
   | Azione |Consentire o negare il traffico che soddisfa i criteri di hello. |

## <a name="next-steps"></a>Passaggi successivi
Informazioni sulle differenze hello [gli agenti di controller di dominio/OS pubblici e privati](container-service-dcos-agents.md).

Sono disponibili altre informazioni sulla [gestione dei contenitori DC/OS](container-service-mesos-marathon-ui.md).


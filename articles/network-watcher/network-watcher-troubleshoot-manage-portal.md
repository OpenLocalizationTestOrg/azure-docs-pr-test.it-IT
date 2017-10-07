---
title: aaaTroubleshoot connessioni - PowerShell e il Gateway di rete virtuale di Azure | Documenti Microsoft
description: Questa pagina viene illustrato come toouse hello Watcher di rete di Azure risolvere i cmdlet di PowerShell
services: network-watcher
documentationcenter: na
author: georgewallace
manager: timlt
editor: 
ms.assetid: f6f0a813-38b6-4a1f-8cfc-1dfdf979f595
ms.service: network-watcher
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 06/19/2017
ms.author: gwallace
ms.openlocfilehash: bd568d34091209390c57d22475559bdb99ad2c59
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshoot-virtual-network-gateway-and-connections-using-azure-network-watcher-powershell"></a>Risolvere i problemi relativi al gateway di rete virtuale e alle connessioni di Azure tramite PowerShell in Network Watcher di Azure

> [!div class="op_single_selector"]
> - [Portale](network-watcher-troubleshoot-manage-portal.md)
> - [PowerShell](network-watcher-troubleshoot-manage-powershell.md)
> - [Interfaccia della riga di comando 1.0](network-watcher-troubleshoot-manage-cli-nodejs.md)
> - [Interfaccia della riga di comando 2.0](network-watcher-troubleshoot-manage-cli.md)
> - [API REST](network-watcher-troubleshoot-manage-rest.md)

Watcher di rete fornisce numerose funzionalità toounderstanding in relazione le risorse di rete in Azure. Una di queste funzionalità è la risoluzione dei problemi riscontrati con le risorse. Risoluzione dei problemi di risorse può essere chiamato tramite il portale di hello, PowerShell, CLI o API REST. Quando viene chiamato, Watcher di rete Controlla integrità hello di un Gateway di rete virtuale o una connessione e restituisce i risultati della ricerca.

## <a name="before-you-begin"></a>Prima di iniziare

Questo scenario si presuppone che si sono già stati seguiti i passaggi di hello in [creare un controllo di rete](network-watcher-create.md) toocreate Watcher di rete.

Per un elenco dei tipi di gateway supportati, consultare i [tipi di gateway supportati](network-watcher-troubleshoot-overview.md#supported-gateway-types).

## <a name="overview"></a>Panoramica

Risoluzione dei problemi di risorse consente di hello risolvere i problemi che si verificano con gateway di rete virtuale e le connessioni. Quando viene effettuata una richiesta di risoluzione dei problemi tooresource, i registri vengono eseguite query e controllato. Una volta completato controllo, vengono restituiti risultati hello. Richieste di risorse, le richieste di risoluzione dei problemi sono a esecuzione prolungata, che potrebbe richiedere più minuti tooreturn un risultato. i log di Hello dalla risoluzione dei problemi vengono archiviati in un contenitore in un account di archiviazione specificato.

## <a name="troubleshoot-a-gateway-or-connection"></a>Risolvere i problemi relativi a una connessione o a un gateway

1. Passare toohello [portale di Azure](https://portal.azure.com) e fare clic su **rete** > **Watcher di rete** > **diagnostica VPN**
2. Selezionare una **Sottoscrizione**, un **Gruppo di risorse** e la **Località**.
3. Risoluzione dei problemi di risorse restituisce i dati sull'integrità hello della risorsa hello. Salva anche l'account di archiviazione tooa log rilevanti toobe esaminato. Fare clic su **Account di archiviazione** tooselect un account di archiviazione.
4. In hello **gli account di archiviazione** pannello selezionare un account di archiviazione esistente o fare clic su **+ account di archiviazione** toocreate uno nuovo.
5. In hello **contenitori** pannello, scegliere un contenitore esistente oppure fare clic su **+ contenitore** toocreate un nuovo contenitore. Al termine, fare clic su **Seleziona**
6. Selezionare tootroubleshoot di hello Gateway e connessione alle risorse e fare clic su **avviare la risoluzione dei problemi**

Se si selezionano più risorse, la risoluzione dei problemi viene eseguita contemporaneamente sulle risorse del gateway. Non può essere eseguito su una connessione ed è associata al gateway in posizione hello contemporaneamente. È consigliabile tootroubleshoot gateway innanzitutto la risoluzione dei problemi di connessione è un processo più lungo. Durante l'esecuzione di diagnostica di VPN in hello una risorsa **lo stato di risoluzione dei problemi** colonna verrà visualizzato lo stato di **in esecuzione**

Al termine, hello le modifiche dello stato della colonna troppo**integro** o **Unhealthy**.

![risoluzione dei problemi completa][2]

## <a name="understanding-hello-results"></a>Informazioni sui risultati hello

In hello **dettagli** sezione della finestra hello, hello **stato** scheda Mostra stato hello di hello ultima risoluzione dei problemi di esecuzione sulla risorsa hello selezionato. Risultati della diagnostica più recente hello sono mostrati xx minuti dopo l'ultima esecuzione hello.

|Proprietà  |Descrizione  |
|---------|---------|
|Risorsa     | Una risorsa toohello di collegamento.        |
|Percorso di archiviazione     |  Percorso toohello account di archiviazione e contenitore che contengono i registri di hello (se qualsiasi sono stato generato durante l'esecuzione di hello). Questa impostazione non viene mantenuto dopo essere usciti da portale hello.        |
|Riepilogo     | Riepilogo hello dell'integrità delle risorse.        |
|Dettagli     | Informazioni dettagliate sull'integrità delle risorse hello.        |
|Ultima esecuzione     | Hello hello ora ultimo tempo di risoluzione dei problemi è stato eseguito.        |


Hello **azione** scheda vengono fornite indicazioni generali su come tooresolve hello problema. Se è possibile eseguire un'azione per il problema di hello, viene fornito un collegamento con informazioni aggiuntive. In caso di hello in cui è presente alcun altro materiale sussidiario, risposta hello fornisce hello url tooopen un caso di supporto.  Per ulteriori informazioni sulle proprietà hello di risposta hello e cosa è inclusa, visitare [Panoramica monitoraggio risolvere i problemi di rete](network-watcher-troubleshoot-overview.md)


## <a name="next-steps"></a>Passaggi successivi

Se le impostazioni sono state modificate che arresta la connettività VPN, vedere [gestire gruppi di sicurezza di rete](../virtual-network/virtual-network-manage-nsg-arm-portal.md) tootrack verso il basso hello rete sicurezza e gruppo di regole di sicurezza che possono essere in questione.


[2]: ./media/network-watcher-troubleshoot-manage-portal/2.png

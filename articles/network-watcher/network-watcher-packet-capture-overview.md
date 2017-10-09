---
title: l'acquisizione tooPacket aaaIntroduction Watcher di rete di Azure | Documenti Microsoft
description: "Questa pagina viene fornita una panoramica della funzionalità di acquisizione dei pacchetti di hello Watcher di rete"
services: network-watcher
documentationcenter: na
author: georgewallace
manager: timlt
editor: 
ms.assetid: 3a81afaa-ecd9-4004-b68e-69ab56913356
ms.service: network-watcher
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/22/2017
ms.author: gwallace
ms.openlocfilehash: 2ce01b391b9c1a1c19aa29c8620628c55586df03
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="introduction-toovariable-packet-capture-in-azure-network-watcher"></a>Acquisizione di pacchetti toovariable introduzione in Watcher di rete di Azure

Acquisizione pacchetto variabile Watcher di rete consente toocreate pacchetto acquisizione sessioni tootrack traffico tooand da una macchina virtuale. Acquisizione di pacchetti consente toodiagnose anomalie di rete sia reattivo e proactivity. Altri usi includono la raccolta di statistiche di rete, ottenere informazioni su intrusioni di rete, client-server toodebug le comunicazioni e molto altro ancora.

L'acquisizione di pacchetti è un'estensione macchina virtuale che viene avviata da remoto tramite Network Watcher. Questa funzionalità semplifica il compito di hello di esecuzione manuale di acquisizione pacchetto eseguita nella macchina virtuale desiderata hello, che consente di risparmiare tempo prezioso. Acquisizione pacchetto può essere attivato tramite il portale di hello, PowerShell, CLI o API REST. Un esempio di modalità di attivazione è rappresentata dagli avvisi della macchina virtuale. I filtri vengono forniti per tooensure sessione di acquisizione hello è acquisire il traffico si desidera toomonitor. I filtri si basano su informazioni a 5 tuple (protocollo, indirizzo IP locale, indirizzo IP remoto, porta locale e porta remota). Hello acquisito vengono archiviati nel disco locale hello o un blob di archiviazione. È previsto un limite di 10 sessioni di acquisizione dei pacchetti per area per sottoscrizione. Questo limite si applica solo le sessioni toohello e non toohello salvato il file di acquisizione di pacchetti in hello VM locale o in un account di archiviazione.

> [!IMPORTANT]
> L'acquisizione di pacchetti richiede un'estensione macchina virtuale `AzureNetworkWatcherExtension`. Per l'installazione dell'estensione hello in una macchina virtuale di Windows, visitare [estensione della macchina virtuale Azure rete Watcher agente per Windows](../virtual-machines/windows/extensions-nwa.md) e per la visita di VM Linux [estensione della macchina virtuale Azure rete Watcher agente per Linux](../virtual-machines/linux/extensions-nwa.md).

informazioni di hello tooreduce di acquisire le informazioni di hello tooonly desiderato, hello le opzioni seguenti sono disponibile per una sessione di acquisizione di pacchetti:

**Acquisisci configurazione**

|Proprietà|Descrizione|
|---|---|
|**Numero massimo di byte per pacchetto (byte)** | Hello numero di byte da ogni pacchetto che vengono acquisiti, vengono acquisiti tutti i byte se lasciato vuoto. Hello numero di byte da ogni pacchetto che vengono acquisiti, vengono acquisiti tutti i byte se lasciato vuoto. Se è necessario solo intestazione IPv4 di hello: indicare 34 qui |
|**Numero massimo di byte per sessione (byte)** | Numero totale di byte in cui viene acquisito, una volta raggiunto il valore di hello hello sessione termina.|
|**Limite di tempo (secondi)** | Imposta un vincolo di tempo per i pacchetti hello sessione di acquisizione. valore predefinito di Hello è 18000 secondi o 5 ore.|

**Filtro (facoltativo)**

|Proprietà|Descrizione|
|---|---|
|**Protocollo** | acquisire Hello toofilter di protocollo per pacchetti hello. i valori disponibili Hello sono TCP, UDP e tutti.|
|**Indirizzo IP locale** | Questo valore consente di filtrare toopackets acquisizione di pacchetti hello in cui l'indirizzo IP locale hello corrisponde a questo valore di filtro.|
|**Porta locale** | Questo valore filtri hello pacchetto acquisizione toopackets in cui la porta locale hello corrisponde a questo valore di filtro.|
|**Indirizzo IP remoto** | Questo valore filtri hello pacchetto acquisizione toopackets dove IP remoti hello corrisponde a questo valore di filtro.|
|**Porta remota** | Questo valore filtri hello pacchetto acquisizione toopackets in cui la porta remota hello corrisponde a questo valore di filtro.|

### <a name="next-steps"></a>Passaggi successivi

Informazioni su come è possibile gestire le acquisizioni di pacchetti tramite il portale di hello visitando [gestire l'acquisizione di pacchetti nel portale di Azure hello](network-watcher-packet-capture-manage-portal.md) o con PowerShell visitando [gestire pacchetti acquisire con PowerShell](network-watcher-packet-capture-manage-powershell.md).

Informazioni su come pacchetto proattiva toocreate acquisisce in base agli avvisi di macchina virtuale, visitare il sito [creare un'acquisizione pacchetto attivati avvisi](network-watcher-alert-triggered-packet-capture.md)

<!--Image references-->
[1]: ./media/network-watcher-packet-capture-overview/figure1.png














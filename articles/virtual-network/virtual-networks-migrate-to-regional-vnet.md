---
title: "una rete virtuale di Azure (classica) da un'area del gruppo di affinità tooa aaaMigrate | Documenti Microsoft"
description: "Informazioni su come toomigrate una rete virtuale (classica) da un'affinità gruppo tooa area."
services: virtual-network
documentationcenter: na
author: jimdial
manager: timlt
editor: 
tags: azure-service-management
ms.assetid: 84febcb9-bb8b-4e79-ab91-865ad9de41cb
ms.service: virtual-network
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 03/15/2016
ms.author: jdial
ms.openlocfilehash: e3a5c0f21e748912e29e2e8d03f4295720e63637
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="migrate-a-virtual-network-classic-from-an-affinity-group-tooa-region"></a>Eseguire la migrazione di una rete virtuale (classico) da un'area del gruppo di affinità tooa

> [!IMPORTANT]
> Azure offre due diversi modelli di distribuzione per creare e usare le risorse: [Gestione risorse e la distribuzione classica](../resource-manager-deployment-model.md?toc=%2fazure%2fvirtual-network%2ftoc.json). In questo articolo viene illustrato l'utilizzo del modello di distribuzione classica hello. Si consiglia di utilizzano modello di distribuzione di gestione risorse di hello più nuove distribuzioni.

Gruppi di affinità assicurarsi che le risorse create all'interno di hello stesso gruppo di affinità fisicamente ospitate dai server che sono vicini, abilitazione toocommunicate queste risorse più veloce. In hello precedente, i gruppi di affinità rappresentavano un requisito per la creazione di reti virtuali (classico). In quel momento, servizio di gestione di rete hello gestito reti virtuali (classico) poteva funzionare solo all'interno di un set di server fisici o unità di scala. Miglioramenti architettonici hanno aumentato ambito hello dell'area tooa gestione di rete.

A seguito di questi miglioramenti, i gruppi di affinità non sono più consigliati o necessari per le reti virtuali (classiche). utilizzo di Hello di gruppi di affinità per le reti virtuali (classico) viene sostituito dalle aree. Le reti virtuali (classiche) associate alle aree prendono il nome di reti virtuali a livello di area.

L'uso dei gruppi di affinità non è consigliabile in generale. A parte i requisiti di rete virtuale hello, gruppi di affinità sono anche importanti toouse tooensure risorse, ad esempio di calcolo (classico) e di archiviazione (classico), sono stati inseriti uno vicino a altro. Tuttavia, con l'architettura di rete di Azure corrente hello, questi requisiti di posizionamento non sono più necessari.

> [!IMPORTANT]
> Sebbene sia ancora tecnicamente possibile toocreate una rete virtuale associata a un gruppo di affinità, non è pertanto interessanti toodo motivo. Molte funzionalità delle reti virtuali, come i gruppi di sicurezza di rete, sono disponibili solo se si usa una rete virtuale a livello di area e non per le reti virtuali associate a gruppi di affinità.
> 
> 

## <a name="edit-hello-network-configuration-file"></a>Modificare i file di configurazione di rete hello

1. Esportare i file di configurazione di rete hello. toolearn come tooexport una configurazione di rete del file tramite PowerShell o hello Azure interfaccia della riga di comando (CLI) 1.0, vedere [configurare una rete virtuale usando un file di configurazione di rete](virtual-networks-using-network-configuration-file.md#export).
2. Modificare i file di configurazione di rete hello, sostituendo **AffinityGroup** con **percorso**. Specificare un'[area](https://azure.microsoft.com/regions) di Azure per **Location**.
   
   > [!NOTE]
   > Hello **percorso** hello area specificata per il gruppo di affinità hello associata con la rete virtuale (classico). Ad esempio, se la rete virtuale (classico) è associata a un gruppo di affinità che si trova negli Stati Uniti occidentali, quando esegue la migrazione, il **percorso** deve puntare tooWest Stati Uniti. 
   > 
   > 
   
    Modificare hello dopo le righe nel file di configurazione di rete, la sostituzione di valori hello con valori personalizzati: 
   
    **Valore precedente:** \<VirtualNetworkSitename="VNetUSWest" AffinityGroup="VNetDemoAG"\> 
   
    **Nuovo valore:**\<VirtualNetworkSitename="VNetUSWest" Location="West US"\>
3. Salvare le modifiche e [importare](virtual-networks-using-network-configuration-file.md#import) hello tooAzure di configurazione di rete.

> [!NOTE]
> Questa migrazione non provoca alcun tempo di inattività tooyour servizi.
> 
> 

## <a name="what-toodo-if-you-have-a-vm-classic-in-an-affinity-group"></a>Quali toodo se si dispone di una macchina virtuale (classico) in un gruppo di affinità
Le macchine virtuali (classiche) che sono attualmente in un gruppo di affinità non è necessario toobe rimosso dal gruppo di affinità hello. Una volta distribuita, una macchina virtuale è distribuita tooa singola unità di scala. Gruppi di affinità possono limitare il set di hello di dimensioni di macchine Virtuali disponibili per una nuova distribuzione di macchina virtuale, ma qualsiasi macchina virtuale esistente distribuita è già limitato set toohello della macchina virtuale di dimensioni disponibili in unità di scala hello in cui hello macchina virtuale viene distribuita. Poiché hello che macchina virtuale è già distribuita tooa unità di scala, la rimozione di una macchina virtuale da un gruppo di affinità non ha alcun effetto su hello macchina virtuale.

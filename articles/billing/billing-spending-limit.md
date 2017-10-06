---
title: limite di spesa Azure aaaUnderstand | Documenti Microsoft
description: Descrive come limite di spesa Azure funziona e come tooremove,
services: 
documentationcenter: 
author: genlin
manager: jlian
editor: 
tags: billing
ms.service: billing
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/12/2017
ms.author: genli
ms.openlocfilehash: ed01401a07c3d0e7edebe42fb1482b7b60b1df51
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="understand-azure-spending-limit-and-how-tooremove-it"></a>Comprendere limite di spesa di Azure e come tooremove,

Il limite di spesa di Azure è un limite sulla spesa possibile della sottoscrizione di Azure. Tutti i nuovi clienti che esegue l'iscrizione per offerta di valutazione hello o le offerte che include i crediti più mesi sono hello attivato per impostazione predefinita di limite di spesa. limite di spesa Hello è $0. ma non può essere modificato. Hello limite di spesa non è disponibile per i tipi di sottoscrizione, ad esempio le sottoscrizioni a pagamento a consumo e i piani di impegno. Vedere hello [elenco completo delle offerte di Azure e la disponibilità di hello del limite di spesa hello](https://azure.microsoft.com/support/legal/offer-details/).

## <a name="what-happens-when-i-reach-hello-spending-limit"></a>Cosa accade quando viene raggiunto limite di spesa hello?

Quando l'utilizzo comporta addebiti esaurire importi mensili di hello inclusi nell'offerta, servizi hello distribuito sono disabilitati per il resto di hello del mese di fatturazione. Ad esempio, i Servizi cloud distribuiti verranno rimossi dalla produzione e le macchine virtuali di Azure verranno arrestate e deallocate. tooprevent dei servizi venga disabilitato, è possibile scegliere tooremove il limite di spesa. Quando i servizi sono disabilitati, dati hello gli account di archiviazione e i database sono disponibili in modalità sola lettura per gli amministratori. Hello inizio hello mese di fatturazione successivo, se l'offerta include crediti più mesi, la sottoscrizione sarà abilitata di nuovo. Quindi è possibile ridistribuire i servizi Cloud e i database e account di archiviazione tooyour accesso completo.

Dopo la sottoscrizione di valutazione gratuita di hello raggiunge hello limite di spesa, è possibile abilitare nuovamente la sottoscrizione hello e automaticamente [offerta prepagata standard tooour aggiornamento](billing-upgrade-azure-subscription.md) entro 90 giorni.

Ricevere notifiche quando si raggiunge hello limite di spesa per l'offerta. Accesso toohello [centro Account Azure](https://account.windowsazure.com)selezionare **ACCOUNT**, quindi selezionare **sottoscrizioni**. Si visualizzano le notifiche sulle sottoscrizioni che hanno raggiunto hello limite di spesa.

## <a name="things-you-are-charged-for-even-if-you-have-a-spending-limit-enabled"></a>Elementi che prevedono un addebito anche in presenza di un limite di spesa

Alcuni servizi di Azure e [Marketplace acquisti](https://azure.microsoft.com/marketplace/) può comportare costi in metodo di pagamento hello (CC), anche se è impostato un limite di spesa. Esempi sono le licenze di Visual studio, Azure Active Directory premium, piani di supporto e la maggior parte delle terze marchio servizi venduti tramite hello Marketplace.


## <a name="when-not-toouse-hello-spending-limit"></a>Quando non toouse hello limite di spesa

limite di spesa Hello potrebbe impedire la distribuzione o utilizzo di determinati marketplace e servizi Microsoft. Ecco gli scenari di hello in cui è necessario rimuovere hello limite di spesa della sottoscrizione.

- Pianificare toodeploy prima entità immagini quali Oracle e servizi, ad esempio Visual Studio Team Services. Questo scenario si tooexceed la spesa limitare quasi immediatamente, mentre il toobe sottoscrizione disabilitata.

- Se si usano servizi che non possono essere interrotti.

- Si dispone di servizi e le risorse con le impostazioni come gli indirizzi IP virtuali che si desidera toolose. Queste impostazioni vengono perse quando vengono deallocate hello servizi e le risorse.


## <a name="remove-hello-spending-limit"></a>Rimuovere hello limite di spesa

È possibile rimuovere hello limite in qualsiasi momento di spesa, purché vi sia un metodo di pagamento valido associato alla sottoscrizione. Per le offerte con carta di credito più mesi, è possibile anche abilitare nuovamente hello limite di spesa all'inizio di hello del ciclo di fatturazione successivo.

la spesa limitare tooremove, seguire questi passaggi:

1. Accesso toohello [centro Account Azure](https://account.windowsazure.com).

2. Selezionare una sottoscrizione.

3. Se la sottoscrizione di hello è disabilitata a causa toohello è stato raggiunto il limite di spesa, fare clic su questa notifica: "Sottoscrizione ha raggiunto hello il limite di spesa ed è stato disabilitato tooprevent spese". In caso contrario, fare clic su **Rimuovi limite di spesa** in hello **lo stato della SOTTOSCRIZIONE** area.

4. Seleziona l'opzione appropriata.

|Opzione|Effetto|
|-------|-----|
|Rimuovi il limite di spesa per un periodo illimitato|Rimuove hello limite di spesa senza riattivarlo automaticamente all'avvio di hello di hello successivo periodo di fatturazione.|
|Rimuovere il limite di spesa per hello periodo di fatturazione corrente|Rimuove hello limite di spesa in modo che lo riattiva torna automaticamente all'avvio di hello di hello successivo periodo di fatturazione.|

## <a name="need-help-contact-support"></a>Richiesta di assistenza Contattare il supporto tecnico.
Se è ancora necessario della Guida, [contattare il supporto tecnico](https://portal.azure.com/?#blade/Microsoft_Azure_Support/HelpAndSupportBlade) tooget risolta il problema.

---
title: aaaCancel la sottoscrizione di Azure | Documenti Microsoft
description: Viene descritto come toocancel la sottoscrizione di Azure, ad esempio hello sottoscrizione di valutazione gratuita
services: 
documentationcenter: 
author: genlin
manager: jlian
editor: 
tags: billing
ms.assetid: 3051d6b0-179f-4e3a-bda4-3fee7135eac5
ms.service: billing
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/27/2017
ms.author: genli
ms.openlocfilehash: 198d6ab3de143c071a572db899037f8de85a8cb4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="cancel-your-subscription-for-azure"></a>Annullare la sottoscrizione di Azure

È possibile annullare la sottoscrizione di Azure come hello [amministratore dell'Account](billing-subscription-transfer.md#whoisaa). Dopo aver annullato la sottoscrizione hello, i servizi di accesso tooAzure e le risorse termina.

Prima di annullare la sottoscrizione:

* Eseguire il backup dei dati. Se ad esempio si archiviano i dati in Archiviazione di Azure o SQL, scaricare una copia. Se si ha una macchina virtuale, salvare un'immagine in locale.
* Arrestare i servizi. Passare toohello [pagine di risorse nel portale di gestione di hello](https://ms.portal.azure.com/?flight=1#blade/HubsExtension/Resources/resourceType/Microsoft.Resources%2Fresources), e **arrestare** qualsiasi esecuzione di macchine virtuali, applicazioni o altri servizi.
* Prendere in considerazione la migrazione dei dati. Vedere [spostare sottoscrizione o il gruppo di risorse toonew risorse](../azure-resource-manager/resource-group-move-resources.md).

Se si annulla un pagamento [piano di supporto di Azure](https://azure.microsoft.com/support/plans/), verrà comunque addebitato mensile per il resto di hello del termine di 6 mesi hello.

## <a name="cancel-subscription-using-hello-azure-portal"></a>Annullare una sottoscrizione utilizzando hello portale di Azure

1. Selezionare la sottoscrizione da hello [pagina sottoscrizioni](https://portal.azure.com/#blade/Microsoft_Azure_Billing/SubscriptionsBlade).

1. Selezionare la sottoscrizione di hello toocancel desiderati e fare clic su **Annulla sottoscrizione**.

    ![Schermata che Mostra pulsante Annulla hello](./media/billing-how-to-cancel-azure-subscription/cancel_ibiza.png)

1. Seguire le istruzioni e completare la procedura di annullamento.

## <a name="cancel-subscription-using-hello-azure-account-center"></a>Annullamento della sottoscrizione utilizzando il centro Account Azure hello

1. Accedi toohello [centro Account Azure](https://account.windowsazure.com/subscriptions) come hello amministratore dell'Account.

1. In **tooview una sottoscrizione di fare clic su utilizzo e dettagli**, selezionare hello sottoscrizione che si desidera toocancel.

    ![Screenshot che mostra un esempio di sottoscrizione selezionata](./media/billing-how-to-cancel-azure-subscription/Selectsub.png)

1. Sul lato destro di hello della pagina hello, selezionare **Annulla sottoscrizione**.

    ![Schermata che Mostra pulsante di hello Annulla sottoscrizione](./media/billing-how-to-cancel-azure-subscription/cancelsub.png)

1. Selezionare **Sì, annulla la sottoscrizione**.

    ![Schermata che Mostra finestra di dialogo Annulla hello](./media/billing-how-to-cancel-azure-subscription/cancelbox.png)

1. Fare clic su  ![pulsante con segno di spunta](./media/billing-how-to-cancel-azure-subscription/checkbutton.png) tooclose hello nella finestra e restituire tooyour sottoscrizione pagina.

## <a name="what-happens-after-i-cancel-my-subscription"></a>Cosa accade quando si annulla la sottoscrizione?

Nel momento in cui viene annullata, la fatturazione viene interrotta immediatamente. Tuttavia, potrebbe essere necessaria fino too10 minuti per hello annullamento Mostra nel portale di hello.

Dopo questo intervallo, i servizi vengono disabilitati. Le macchine virtuali vengono quindi deallocate e gli indirizzi IP temporanei liberati e la risorsa di archiviazione diventa di sola lettura.

A meno che non si è in una versione di valutazione gratuita o di crediti, sta fatturato per eventuali addebiti di utilizzo in sospeso generati tra l'ultimo ciclo di fatturazione e la data di annullamento hello. È possibile ottenere la fattura ultimo alla fine hello hello del ciclo di fatturazione.

Dopo aver annullato la sottoscrizione, attendiamo 90 giorni prima di eliminare definitivamente i dati nel caso in cui è necessario tooaccess oppure si cambia idea. Non addebito per la conservazione dei dati hello. vedere, più toolearn [Microsoft Trust Center - come si gestisce i dati](https://go.microsoft.com/fwLink/p/?LinkID=822930&clcid=0x409).

## <a name="reactivate-subscription"></a>Riattivare la sottoscrizione

Se si annulla la sottoscrizione a pagamento accidentalmente, è possibile [riattivarla in hello centro account](billing-subscription-become-disable.md).

Se la sottoscrizione non è a consumo, contattare il supporto tecnico entro 90 giorni dall'annullamento tooreactivate la sottoscrizione.

## <a name="need-help-contact-support"></a>Richiesta di assistenza Contattare il supporto tecnico.

Se hai domande, [contattare il supporto tecnico](https://portal.azure.com/?#blade/Microsoft_Azure_Support/HelpAndSupportBlade) tooget risolta il problema.

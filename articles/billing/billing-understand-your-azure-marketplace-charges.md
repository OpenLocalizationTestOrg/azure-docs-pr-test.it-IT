---
title: aaaUnderstand costi di servizio esterni Azure | Documenti Microsoft
description: Informazioni sulla fatturazione di servizi esterni, noti in precedenza come Marketplace, in Azure.
services: 
documentationcenter: 
author: adpick
manager: tonguyen
editor: 
tags: billing
ms.assetid: 5e0e2a3c-d111-4054-8508-0c111c1b749b
ms.service: billing
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/13/2017
ms.author: adpick
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 1d2cb28319e2ab4eff753177220993cbf94c96ac
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="understand-your-azure-billing-for-external-service-charges"></a>Informazioni sulla fatturazione di Azure per gli addebiti dei servizi esterni
Servizi esterni utilizzati toobe chiamato Azure Marketplace. Si tratta in genere di servizi pubblicati da terze parti disponibili per Azure, ma integrati completamente in Azure. Ad esempio, ClearDB e SendGrid sono servizi esterni che è possibile acquistare in Azure, ma che non vengono pubblicati da Microsoft.

Durante il provisioning di un nuovo servizio esterno o di una nuova risorsa, viene visualizzato un avviso:

![Avviso di acquisto di Marketplace](./media/billing-understand-your-azure-marketplace-charges/marketplace-warning.PNG)

> [!NOTE]
> I servizi esterni vengono pubblicati da società non Microsoft, ma talvolta anche i prodotti Microsoft sono classificati come servizi esterni.
> 
> 

## <a name="how-external-services-are-billed"></a>Modalità di fatturazione dei servizi esterni
- I servizi esterni vengono fatturati separatamente. Vengono gestiti come ordini singoli all'interno della sottoscrizione di Azure. periodo di fatturazione Hello per ogni servizio è impostato al momento dell'acquisto del servizio hello. Non i toobe confusa con periodo di fatturazione della sottoscrizione hello in cui è stato acquistato hello. Si ricevono anche fatture separate e l'addebito sulla carta di credito viene applicato separatamente.
- Per ogni servizio esterno è previsto un modello di fatturazione diverso. Alcuni servizi vengono fatturati con pagamento in base al consumo, mentre altri prevedono un modello di pagamento su base mensile. Per i servizi esterni di Azure è necessaria una carta di credito e non è possibile pagare tramite fattura.
- Non è possibile usare i crediti gratuiti mensili per i servizi esterni. Se si utilizza una sottoscrizione di Azure che include [libero crediti](https://azure.microsoft.com/pricing/spending-limits/), non possono essere applicati tooexternal servizio distinte. Utilizzare i servizi esterni di toopurchase una carta di credito.


## <a name="view-external-service-spending-and-history-in-hello-azure-portal"></a>Uso dei servizi esterni di visualizzazione e la cronologia nel portale di Azure hello
È possibile visualizzare un elenco di servizi esterni hello in ogni sottoscrizione all'interno di hello [portale di Azure](https://portal.azure.com/): 

1. Accedi toohello [portale di Azure](https://portal.azure.com/) come amministratore dell'account hello.
2. Nel menu Hub hello, selezionare **sottoscrizioni**.
   
    ![Selezionare le sottoscrizioni nel menu Hub hello](./media/billing-understand-your-azure-marketplace-charges/sub-button.png) 
3. In hello **sottoscrizioni** blade, sottoscrizione selezionare hello desidera tooview e quindi selezionare **servizi esterni**.
   
    ![Selezionare una sottoscrizione nel pannello fatturazione hello](./media/billing-understand-your-azure-marketplace-charges/select-sub-external-services.png)
4. Si dovrebbero apparire gli ordini di servizio esterno, il nome di server di pubblicazione hello, il livello di servizio che è stato acquistato, nome assegnato alla risorsa hello e lo stato dell'ordine corrente hello. toosee oltre distinte, selezionare un servizio esterno.
   
    ![Selezionare un servizio esterno](./media/billing-understand-your-azure-marketplace-charges/external-service-blade2.png)
5. Da qui è possibile visualizzare oltre gli importi degli effetti inclusi dettagli imposte hello.
   
    ![Visualizzare la cronologia di fatturazione dei servizi esterni](./media/billing-understand-your-azure-marketplace-charges/billing-overview-blade.png)

## <a name="view-external-service-spending-for-enterprise-agreement-ea-customers"></a>Visualizzare la spesa dei servizi esterni per i clienti con contratto Enterprise (EA, Enterprise Agreement)
I clienti EA vedere spesa servizio esterno e scaricare i report nel portale di hello EA. Vedere [Azure Marketplace per i clienti EA](https://ea.azure.com/helpdocs/azureMarketplace) tooget avviato.

## <a name="manage-payment-methods-for-external-service-orders"></a>Gestire i metodi di pagamento per gli ordini di servizi esterni
Aggiornare i metodi di pagamento per gli ordini di servizio esterno da hello [centro Account](https://account.windowsazure.com/).

> [!NOTE]
> Se è stata acquistata una sottoscrizione con un account aziendale o dell'istituto di istruzione, [contattare il supporto tecnico](https://portal.azure.com/?#blade/Microsoft_Azure_Support/HelpAndSupportBlade) toomake Modifica metodo di pagamento tooyour.
> 
> 

1. Accedi toohello [centro Account](https://account.windowsazure.com/) e [passare toohello **marketplace** scheda](https://account.windowsazure.com/Store)
   
    ![Selezionare marketplace nel centro account hello](./media/billing-understand-your-azure-marketplace-charges/select-marketplace.png)
2. Selezionare hello esterno servizio toomanage
   
    ![Selezionare hello esterno servizio toomanage](./media/billing-understand-your-azure-marketplace-charges/select-ext-service.png)
3. Fare clic su **modificare il metodo di pagamento** hello destra della pagina hello. Questo collegamento consente di visualizzare è tooa diversi portale toomanage il metodo di pagamento.
   
    ![Riepilogo degli ordini](./media/billing-understand-your-azure-marketplace-charges/change-payment.PNG)
4. Fare clic su **Modifica informazioni** e seguire le istruzioni tooupdate le informazioni di pagamento.
   
    ![Selezionare Modifica informazioni](./media/billing-understand-your-azure-marketplace-charges/edit-info.png)

## <a name="cancel-an-external-service-order"></a>Annullare un ordine di servizio esterno
Se si desidera toocancel l'ordine di servizio esterno, eliminare la risorsa hello in hello [portale di Azure](https://portal.azure.com).

![Eliminare una risorsa](./media/billing-understand-your-azure-marketplace-charges/deleteMarketplaceOrder.PNG)

## <a name="need-help-contact-support"></a>Richiesta di assistenza Contattare il supporto tecnico.
Se hai domande, [contattare il supporto tecnico](https://portal.azure.com/?#blade/Microsoft_Azure_Support/HelpAndSupportBlade) tooget risolta il problema.


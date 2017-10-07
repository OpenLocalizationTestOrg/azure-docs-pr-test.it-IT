---
title: aaaUnderstand la fattura per Azure | Documenti Microsoft
description: Informazioni su come tooread e comprendere l'utilizzo e costi per la sottoscrizione di Azure
services: 
documentationcenter: 
author: tonguyen10
manager: tonguyen
editor: 
tags: billing
ms.assetid: 32eea268-161c-4b93-8774-bc435d78a8c9
ms.service: billing
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/14/2017
ms.author: tonguyen
ms.openlocfilehash: a3195eb129b1576e8cb665aa6f88a1a2647edd78
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="understand-your-bill-for-microsoft-azure"></a>Comprendere la fattura per Microsoft Azure
toounderstand fatturazione di Azure, confrontare la fattura con il file di utilizzo di hello dettagliato giornaliera e hello Gestione report nel portale di Azure hello dei costi.

tooobtain un fattura in formato PDF e una copia di dettagliate giornaliero utilizzo download del file CSV, vedere [ottenere di Azure i dati di utilizzo giornaliero e fatturazione di fatturazione](billing-download-azure-invoice-daily-usage-date.md). 

Per una spiegazione dettagliata dei termini e delle descrizioni nella fattura e nel file dei dettagli di utilizzo giornaliero, vedere [Understand terms on your Microsoft Azure invoice](billing-understand-your-invoice.md) (Comprendere i termini nella fattura di Microsoft Azure) e [Understand terms on your Microsoft Azure detailed usage](billing-understand-your-usage.md) (Comprendere i termini nel file dei dettagli di utilizzo giornaliero). 

Per informazioni dettagliate su hello costi di gestione report, vedere [la gestione dei costi Azure portal](https://docs.microsoft.com/en-us/azure/billing/billing-getting-started).


## <a name="charges"></a>Come assicurarsi che siano corretti addebiti hello in fattura
Se nella fattura è presente un addebito su cui si vogliono ricevere altre informazioni, sono disponibili due opzioni.

### <a name="option-1-review-your-invoice-and-compare-hello-usage-and-costs-with-hello-detailed-usage-csv-file"></a>Opzione 1: Esaminare la fattura e confrontare i costi e utilizzo di hello con hello dettagliata file CSV di utilizzo

Hello file CSV dettagliate sull'utilizzo mostra gli addebiti per il periodo di fatturazione e utilizzo giornaliero. vedere il file CSV, sull'utilizzo dettagliati tooget [ottenere di Azure i dati di utilizzo giornaliero e fatturazione di fatturazione](https://docs.microsoft.com/en-us/azure/billing/billing-download-azure-invoice-daily-usage-date).

Gli addebiti di utilizzo vengono visualizzati a livello di misuratore hello. Hello seguenti termini hello stessa operazione nella fattura entrambi hello e hello file dettagliate sull'utilizzo. Ad esempio, hello fatturazione ciclo nella fattura hello è il periodo di fatturazione toohello equivalente illustrato nel file di hello dettagliate sull'utilizzo.

 | Fattura (PDF) | Dettagli di utilizzo (CSV)|
 | --- | --- |
|Ciclo di fatturazione | Periodo di fatturazione |
 |Nome |Categoria misuratore |
 |Type |Sottocategoria contatore |
 |Risorsa |Nome misuratore |
 |Region |Area misuratore |
 |Consumato |Quantità consumata |
 |Incluso |Quantità inclusa |
 |Fatturabile |Quantità in eccesso |

Hello **addebiti di utilizzo** sezione della fattura è hello totale per ogni controllo che è stata utilizzata durante il periodo di fatturazione. Ad esempio, hello cattura di schermata seguente mostra un addebito di utilizzo per hello servizio Utilità di pianificazione di Azure.

![Addebiti di utilizzo nella fattura](./media/billing-understand-your-bill/1.png)

Hello **istruzione** sezione relativa all'utilizzo dettagliato CSV Mostra hello addebito stesso. Entrambi hello *consumato* quantità e *valore* corrispondenza hello fattura.

![Addebiti di utilizzo nel file CSV](./media/billing-understand-your-bill/2.png)

dettagli di questo addebito su base giornaliera, andare toohello toosee **utilizzo giornaliero** sezione di hello CSV. Filtrare per "Utilità di pianificazione" sotto *misuratore categoria* ed è possibile visualizzare il misuratore hello giorni è stato utilizzato e quanto è stato elaborato. Hello *risorse* e *gruppo di risorse* informazioni sono disponibile anche per il confronto. Hello *consumato* valori devono sommare del toowhat visualizzato nella fattura hello.

![Sezione Utilizzo giornaliera hello CSV](./media/billing-understand-your-bill/3.png)

costo di hello tooget al giorno, moltiplicare hello *consumato* quantità con hello *frequenza* valore hello **istruzione** sezione.

toolearn ulteriori informazioni su invoice hello, vedere [comprendere la fattura di Azure](billing-understand-your-invoice.md).

toolearn su ognuna delle colonne hello hello CSV, vedere [comprendere l'utilizzo dettagliato Azure](billing-understand-your-invoice.md).

### <a name="option-2-review-your-invoice-and-compare-with-hello-usage-and-costs-in-hello-azure-portal"></a>Opzione 2: Esaminare la fattura e confrontare con l'utilizzo di hello e i costi di hello portale di Azure

Hello portale di Azure consente inoltre di verificare gli addebiti. Hello portale di Azure fornisce i grafici di gestione dei costi per una panoramica dei costi di utilizzo e hello nella fattura.

toocontinue con hello esempio precedente, visitare hello [pagina sottoscrizioni](https://portal.azure.com/#blade/Microsoft_Azure_Billing/SubscriptionsBlade), selezionare la sottoscrizione e quindi scegliere **analisi dei costi**. Da qui, è possibile specificare l'intervallo di tempo hello e vedere i costi di utilizzo per il servizio Utilità di pianificazione di Azure hello.

![Visualizzazione dell'analisi dei costi nel Portale di Azure](./media/billing-understand-your-bill/4.png)

suddivisione giornaliera dei costi toosee hello in **storico costo**, fare clic sulla riga hello.

![Visualizzazione Cronologia dei costi nel portale di Azure](./media/billing-understand-your-bill/5.png)

vedere, più toolearn [evitare i costi imprevisti con la fatturazione di Azure e gestione dei costi](billing-getting-started.md#costs).

## <a name="external"></a>A cosa si riferiscono gli addebiti per servizi esterni?
I servizi esterni, noti anche come ordini di Azure Marketplace, sono erogati da fornitori di servizi indipendenti e vengono fatturati separatamente. gli addebiti di Hello non vengono visualizzati nella fattura di Azure. vedere, più toolearn [comprendere gli addebiti di servizio esterni Azure](billing-understand-your-azure-marketplace-charges.md).

## <a name="payment"></a>Come si effettua il pagamento?

Se si imposta una carta di credito o sulla carta di credito come metodo di pagamento, pagamento hello viene addebitato automaticamente entro 10 giorni di scadenza del periodo di fatturazione hello. L'istruzione di carta di credito, hello voce direbbe **MSFT Azure**.

Se si [pagamento per la fatturazione](billing-how-to-pay-by-invoice.md), trasmissione, la posizione di pagamento toohello elencata nella parte inferiore di hello della fattura. Per altre informazioni, [contattare il supporto tecnico](https://portal.azure.com/?#blade/Microsoft_Azure_Support/HelpAndSupportBlade).

## <a name="how-do-i-check-hello-status-of-a-payment-made-by-credit-card"></a>Come è possibile controllare lo stato di hello di pagamento effettuato con carta di credito?

[Creare un ticket di supporto](https://portal.azure.com/?#blade/Microsoft_Azure_Support/HelpAndSupportBlade) tooask per lo stato di hello del pagamento. 

## <a name="tips-for-cost-management"></a>Suggerimenti per la gestione dei costi
- Stima dei costi mediante hello [calcolatore dei costi](https://azure.microsoft.com/pricing/calculator/) e [costo totale di calcolatrice di proprietà](https://aka.ms/azure-tco-calculator)e ottenere hello [dettagliate informazioni sui prezzi per ogni servizio](https://azure.microsoft.com/en-us/pricing/).
- [Impostare avvisi di fatturazione](billing-set-up-alerts.md).
- [Esaminare le informazioni sull'utilizzo e costi regolarmente nel portale di Azure hello](billing-getting-started.md#costs).

## <a name="need-help-contact-support"></a>Richiesta di assistenza Contattare il supporto tecnico.

Se è ancora necessario della Guida, [contattare il supporto tecnico](https://portal.azure.com/?#blade/Microsoft_Azure_Support/HelpAndSupportBlade) tooget risolta il problema.

---
title: aaaDownload fatturazione fattura e giornaliera utilizzo dati di Azure | Documenti Microsoft
description: Viene descritto come toodownload o della vista di fatturazione di Azure fattura e dati di utilizzo giornalieri.
keywords: fatturazione, scaricare la fatture, fattura di Azure, uso di Azure
services: 
documentationcenter: 
author: genlin
manager: tonguyen
editor: 
tags: billing
ms.assetid: 6d568d1d-3bd6-4348-97d0-1098b5fe0661
ms.service: billing
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/25/2017
ms.author: genli
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 2826df10f39914fcaeb9985271dadde550c68dfd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="download-or-view-your-azure-billing-invoice-and-daily-usage-data"></a>Scaricare o visualizzare la fattura e i dati di uso giornalieri di Azure
È possibile scaricare la fattura da hello [portale di Azure](https://portal.azure.com/#blade/Microsoft_Azure_Billing/SubscriptionsBlade) o inviarlo tramite posta elettronica. toodownload l'utilizzo giornaliero, andare toohello [centro Account Azure](https://account.windowsazure.com). Solo determinati ruoli dispongono di autorizzazione tooget informazioni fattura e l'utilizzo, ad esempio hello amministratore dell'Account di fatturazione. toolearn più su come ottenere accesso toobilling informazioni, vedere [tooAzure accesso Gestisci fatturazione utilizzando ruoli](billing-manage-access.md).

## <a name="get-your-invoice-in-email-pdf"></a>Ottenere la fattura tramite posta elettronica (formato PDF)
È possibile acconsentire esplicitamente all'invio e configurare altri destinatari tooreceive fattura di Azure tramite posta elettronica. Questa funzionalità potrebbe non essere disponibile per alcune sottoscrizioni, ad esempio offerte di supporto, contratti Enterprise o Azure in Open.

1. Selezionare la sottoscrizione da hello [pannello sottoscrizioni](https://portal.azure.com/#blade/Microsoft_Azure_Billing/SubscriptionsBlade). Dare il consenso esplicito per ogni sottoscrizione posseduta. Fare clic su **Invoices** (Fatture) quindi su **Email my invoice** (Invia fattura tramite posta elettronica). 

    ![Schermata che mostra hello registrarsi flusso](./media/billing-download-azure-invoice-daily-usage-date/InvoicesDeepLink.PNG)
    
2. Fare clic su **acconsentire esplicitamente all'invio** e accettare le condizioni di hello.

    ![Schermata che mostra hello registrarsi flusso](./media/billing-download-azure-invoice-daily-usage-date/InvoiceArticleStep2.PNG)
 
3. Una volta che si accetta il contratto di hello, è possibile configurare altri destinatari.

    ![Schermata che mostra hello registrarsi flusso](./media/billing-download-azure-invoice-daily-usage-date/InvoiceArticleStep3.PNG)
    
Se non si ottiene un messaggio di posta elettronica dopo aver completato i passaggi di hello, assicurarsi che l'indirizzo di posta elettronica sia corretto in hello [le preferenze di comunicazione nel proprio profilo](https://account.windowsazure.com/profile).

## <a name="download-invoice-from-azure-portal-pdf"></a>Scaricare la fattura dal portale di Azure (PDF)

1. Selezionare la sottoscrizione da hello [pannello sottoscrizioni](https://portal.azure.com/#blade/Microsoft_Azure_Billing/SubscriptionsBlade) nel portale di Azure come [un utente con accesso tooinvoices](billing-manage-access.md).

2. Selezionare **Fatture**. 

    ![Schermata che mostra l'opzione di fatturazione e utilizzo di hello](./media/billing-download-azure-invoice-daily-usage-date/billingandusage.png) 

3. Fare clic su **Scarica fattura** tooview una copia della fattura PDF. Se l'indicazione è **non disponibile**, vedere [perché non è presente una fattura per hello ultimo periodo di fatturazione?](#noinvoice)

    ![Schermata che mostra i periodi di fatturazione, opzione di download hello e costi totali per ogni periodo di fatturazione](./media/billing-download-azure-invoice-daily-usage-date/billing4.png)

4. È anche possibile visualizzare l'utilizzo giornaliero facendo clic sul periodo di fatturazione hello. 

Per altre informazioni sulla fattura, vedere [Comprendere la fattura per Microsoft Azure](billing-understand-your-bill.md). Per informazioni sulla gestione dei costi, vedere [Evitare costi aggiuntivi con la gestione dei costi e la fatturazione di Azure](billing-getting-started.md).

## <a name="download-usage-from-hello-account-center-csv"></a>Scaricare l'utilizzo da hello centro Account (. csv)

1. Sign in hello [centro Account Azure](https://account.windowsazure.com/subscriptions) come hello amministratore dell'Account.

2. Selezionare la sottoscrizione di hello per cui si desiderano informazioni di fatturazione e utilizzo di hello.

3. Selezionare **Cronologia di fatturazione**. 

    ![Schermata che mostra l'opzione Cronologia di fatturazione](./media/billing-download-azure-invoice-daily-usage-date/Billinghisotry.png)

4. È possibile visualizzare le istruzioni per hello ultimi sei periodi di fatturazione e hello fatturati periodo corrente. 

    ![Schermata che mostra i periodi di fatturazione, opzioni toodownload fattura e dell'utilizzo giornaliero e costi totali per ogni periodo di fatturazione](./media/billing-download-azure-invoice-daily-usage-date/billingSum.png)

5. Selezionare **Visualizza estratto conto corrente** toosee è stata generata una stima degli addebiti in hello tempo hello stimato. Queste informazioni vengono aggiornate solo una volta al giorno e potrebbero non includere tutti gli utilizzi effettuati. È possibile che la fattura mensile non corrisponda a questa stima.

    ![Schermata che mostra l'opzione dell'istruzione corrente visualizzazione hello](./media/billing-download-azure-invoice-daily-usage-date/billingSum2.png)

    ![Schermata che mostra stima hello del costo corrente](./media/billing-download-azure-invoice-daily-usage-date/billingSum3.png)

6. Selezionare **Scarica utilizzo** toodownload hello dati di utilizzo giornalieri come file CSV. Se sono disponibili due versioni, scaricare la versione 2.

    ![Schermata che mostra l'opzione Scarica utilizzo hello](./media/billing-download-azure-invoice-daily-usage-date/DLusage.png)

Solo hello amministratore dell'Account può accedere hello centro Account di Azure. Altri amministratori fatturazione, ad esempio un proprietario, è possono ottenere informazioni sull'utilizzo utilizzando hello [API fatturazione](billing-usage-rate-card-overview.md).

Per altre informazioni sui dati di utilizzo giornalieri, vedere [Comprendere la fattura per Microsoft Azure](billing-understand-your-bill.md). Per informazioni sulla gestione dei costi, vedere [Evitare costi aggiuntivi con la gestione dei costi e la fatturazione di Azure](billing-getting-started.md).

## <a name="noinvoice"></a>Perché non è presente una fattura per hello ultimo periodo di fatturazione?

Potrebbero esserci diversi motivi per cui non è visualizzata alcuna fattura:

- Si dispone di un credito mensile per la sottoscrizione che non è stato superato oppure si sta usando una versione di prova gratuita. La fattura viene generata solo quando si possiede del denaro.

- È minore di 30 giorni dalla data di hello che sottoscritto tooAzure.

- fattura Hello non è ancora generata. Attendere la fine hello del periodo di fatturazione hello.

- Se non si è amministratore dell'Account hello, fatture precedente potrebbero non essere tooyou sono disponibili.

## <a name="need-help-contact-support"></a>Richiesta di assistenza Contattare il supporto tecnico.
Se è ancora più domande, [contattare il supporto tecnico](https://portal.azure.com/?#blade/Microsoft_Azure_Support/HelpAndSupportBlade) tooget risolta il problema.


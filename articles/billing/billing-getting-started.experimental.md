---
title: aaaPrevent imprevisti costi, gestire la fatturazione - Azure | Documenti Microsoft
description: "Informazioni su come tooavoid spese impreviste nella fattura di Azure. Usare le funzionalità di gestione e verifica dei costi per una sottoscrizione di Microsoft Azure."
services: 
documentationcenter: 
author: tonguyen10
manager: tonguyen
editor: 
tags: billing
ms.assetid: 482191ac-147e-4eb6-9655-c40c13846672
ms.service: billing
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/10/2017
ms.author: tonguyen
ms.openlocfilehash: d380f27861531351ac8e570469c59a84b9ca99e8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="prevent-unexpected-charges-with-azure-billing-and-cost-management"></a>Evitare addebiti imprevisti con la gestione dei costi e della fatturazione di Azure

Quando effettua l'iscrizione per Azure, esistono alcune operazioni, è possibile eseguire un'idea precisa la spesa tooget. Hello [calcolatore dei costi](https://azure.microsoft.com/pricing/calculator/) può fornire una stima dei costi prima di creare una risorsa di Azure. Hello [portale di Azure](https://portal.azure.com/#blade/Microsoft_Azure_Billing/SubscriptionsBlade) fornisce suddivisione del costo corrente hello e previsione per la sottoscrizione. Se si desidera toogroup e comprendere i costi per progetti diversi o team, esaminare [tag risorsa](../azure-resource-manager/resource-group-using-tags.md). Se l'organizzazione dispone di un sistema che si preferisce toouse, estrarre hello [fatturazione API](billing-usage-rate-card-overview.md). 

È anche possibile [scaricare le fatture precedenti e file di utilizzo in dettaglio](billing-download-azure-invoice-daily-usage-date.md) toomake che verrà addebitato correttamente. Per altre informazioni sul confronto tra i dati di utilizzo giornalieri e la fattura, vedere [Comprendere la fattura per Microsoft Azure](billing-understand-your-bill.md).

Se la sottoscrizione è tramite un Enterprise Agreement (EA), il Provider di soluzioni Cloud (CSP) o Azure Sponsorship, molte funzionalità di questo articolo non applicare tooyou. Al contrario, l'utente può usare diversi set di strumenti per la gestione dei costi. Vedere [Risorse aggiuntive per EA, CSP e Sponsorship](#other-offers).

Se la sottoscrizione è una versione di valutazione gratuita, [Visual Studio](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/), Azure in Open (AIO) o BizSpark, la sottoscrizione verrà automaticamente disabilitata quando vengono usati tutti i crediti. Informazioni su [i limiti di spesa](#spending-limit) tooavoid con la sottoscrizione unexpectantly disabilitata. 

## <a name="get-estimated-costs-before-adding-azure-services"></a>Ottenere una stima dei costi prima di aggiungere servizi di Azure

### <a name="estimate-cost-online-using-hello-pricing-calculator"></a>Costo stimato online utilizzando calcolatore dei costi di hello

Estrarre hello [calcolatore dei costi](https://azure.microsoft.com/pricing/calculator/) tooget un costo mensile stimato del servizio hello si è interessati. È possibile aggiungere qualsiasi tooget di risorse di Azure prima di terze parti una stima dei costi.

![Schermata di hello menu calcolatore di prezzi](./media/billing-getting-started/pricing-calc.png)

Ad esempio, una macchina virtuale di Windows A1 (VM) è stimato toocost $66.96 USD/mese nel calcolo ore se si lascia in esecuzione hello intero:

![Schermata del calcolatore dei costi di hello viene dimostrato che una macchina virtuale Windows A1 stimato toocost $66.96 USD al mese](./media/billing-getting-started/pricing-calcVM.png)

Per altre informazioni sui prezzi, vedere queste [domande frequenti](https://azure.microsoft.com/pricing/faq/). O se si desidera tootalk tooan agente di Azure, contattare 1-800-867-1389.

### <a name="review-hello-estimated-cost-in-hello-azure-portal"></a>Costo stimato hello revisione in hello portale di Azure

In genere quando si aggiunge un servizio nel portale di Azure hello, è disponibile una visualizzazione che mostra un costo stimato simile al mese. Ad esempio, quando si sceglie di dimensioni hello della macchina virtuale Windows, viene visualizzato hello stimato costo mensile per ore di calcolo hello:

![Esempio: una macchina virtuale Windows A1 viene stimato toocost $66.96 USD al mese](./media/billing-getting-started/vm-size-cost.PNG)

### <a name="set-up-billing-alerts"></a>Impostare avvisi di fatturazione per le sottoscrizioni Microsoft Azure

Impostare gli avvisi di fatturazione tooget messaggi di posta elettronica quando i costi di utilizzo superano un importo specificato. In caso di crediti mensili, configurare avvisi per il raggiungimento di un importo specificato. Per altre informazioni, vedere [Configurare avvisi di fatturazione per le sottoscrizioni di Microsoft Azure](billing-set-up-alerts.md).

![Schermata di un messaggio di posta elettronica relativo a un avviso di fatturazione](./media/billing-getting-started/billing-alert.png)

> [!NOTE]
> Dato che questa funzionalità è ancora in anteprima, è consigliabile controllare regolarmente l'utilizzo.

È possibile stima dei costi di hello toouse da hello calcolatore dei costi come linee guida per il primo avviso.

### <a name="spending-limit"></a> Controllare se è attivo un limite di spesa

Se si dispone di una sottoscrizione che utilizza crediti, quindi hello limite di spesa è attivata automaticamente per impostazione predefinita. In questo modo, quando si esauriscono tutti i crediti non verrà effettuato alcun addebito sulla carta di credito. Vedere hello [elenco completo delle offerte di Azure e la disponibilità di hello del limite di spesa](https://azure.microsoft.com/support/legal/offer-details/).

Quando si raggiunge il limite di spesa, tuttavia, i servizi vengono disabilitati. Le VM vengono quindi deallocate. tooavoid i tempi di inattività, è necessario disattivare hello limite di spesa. Qualsiasi eccedenza verrà addebitata sulla carta di credito in archivio. 

toosee se è stato ottenuto limite di spesa, visitare toohello [consente di visualizzare le sottoscrizioni nel centro Account hello](https://account.windowsazure.com/Subscriptions). Se il limite di spesa è attivato, viene visualizzato un banner:

![Schermata che mostra un avviso relativo limite di si trova su hello centro Account di spesa](./media/billing-getting-started/spending-limit-banner.PNG)

Fare clic su intestazione hello e seguire i prompt tooremove hello limite di spesa. Se non è stato immesso le informazioni della carta di credito al momento dell'iscrizione, è necessario immettere hello tooremove limite di spesa. Per ulteriori informazioni, vedere [Azure limite di spesa: come funziona e come tooenable o rimuoverlo](https://azure.microsoft.com/pricing/spending-limits/).

## <a name="ways-toomonitor-your-costs-when-using-azure-services"></a>Toomonitor modi i costi quando si utilizza servizi di Azure

### <a name="tags"></a>Aggiungere tag tooyour risorse toogroup i dati di fatturazione

È possibile utilizzare i dati di fatturazione toogroup tag per i servizi supportati. Ad esempio, se si eseguono più macchine virtuali per diversi team, è possibile utilizzare i costi toocategorize tag dall'ambiente (test pre-produzione, produzione) o il centro di costo (HR, marketing, finanza). 

![Schermata che mostra l'impostazione di tag nel portale di hello](./media/billing-getting-started/tags.PNG)

tag Hello visualizzati in tutto il costo diverso visualizzazioni Creazione rapporti. Ad esempio, sono visibili immediatamente nella [visualizzazione dell'analisi dei costi](#costs) e dopo il primo periodo di fatturazione nel [file CSV dei dati dettagliati di utilizzo](#invoice-and-usage).

Per ulteriori informazioni, vedere [tramite tag tooorganize le risorse di Azure](../azure-resource-manager/resource-group-using-tags.md).

### <a name="costs"></a>Controllare il portale di hello scomposizione dei costi regolarmente e velocità

Quando i servizi sono in esecuzione, controllare regolarmente a quanto ammonta il relativo costo. È possibile visualizzare hello corrente spesa e velocità nel portale di Azure. 

1. Visitare hello [pannello sottoscrizioni nel portale di Azure](https://portal.azure.com/#blade/Microsoft_Azure_Billing/SubscriptionsBlade) e selezionare una sottoscrizione.

2. È consigliabile vedere scomposizione dei costi di hello e velocità nel Pannello di hello popup. Potrebbe non essere supportato per l'offerta (verrà visualizzato un avviso superiore hello).

    ![Schermata di velocità e suddivisione in hello portale di Azure](./media/billing-getting-started/burn-rate.PNG)

3. Fare clic su **analisi dei costi** in hello elenco toohello toosee sinistro hello costo dettagli in base alla risorsa. Attendere 24 ore dopo l'aggiunta di un servizio per toopopulate dati hello.

    ![Schermata di hello. analisi costo nel portale di Azure](./media/billing-getting-started/cost-analysis.PNG)

4. È possibile filtrare la visualizzazione in base a diverse proprietà, come [tag](#tags), gruppo di risorse e intervallo di tempo. Fare clic su **applica** filtri hello tooconfirm e **scaricare** se si desidera tooexport hello vista tooa comma-separated CSV (valori) file.

5. Inoltre, è possibile fare clic su una risorsa toosee spesa cronologia e quanto risorse hello costi ogni giorno.

    ![Schermata di hello spesa visualizzazione della cronologia nel portale di Azure](./media/billing-getting-started/costhistory.PNG)

Si consiglia di controllare i costi di hello che viene visualizzato con le stime hello che si verifica quando si seleziona servizi hello. Se i costi di hello differiscono notevolmente dalle stime, verificare hello piano dei prezzi (A1 vs VM A0, ad esempio) che è stato selezionato per le risorse. 

### <a name="consider-enabling-cost-cutting-features-like-auto-shutdown-for-vms"></a>Provare ad abilitare funzionalità per la riduzione dei costi come l'arresto automatico delle VM

A seconda dello scenario, è possibile configurare l'arresto automatico per le macchine virtuali in hello portale di Azure. Per altre informazioni, vedere il post sull'[arresto automatico delle VM con Azure Resource Manager](https://azure.microsoft.com/blog/announcing-auto-shutdown-for-vms-using-azure-resource-manager/).

![Schermata dell'opzione di arresto automatici nel portale di hello](./media/billing-getting-started/auto-shutdown.PNG)

Arresto automatici non hello uguali a quelli quando si arresta all'interno di hello macchina virtuale con opzioni risparmio energia. Auto-shutdown arresta e dealloca toostop le macchine virtuali spese aggiuntive. Per altre informazioni, vedere le domande frequenti sui prezzi per le [VM Linux](https://azure.microsoft.com/pricing/details/virtual-machines/linux/) e le [VM Windows](https://azure.microsoft.com/pricing/details/virtual-machines/windows/) in relazione agli stati delle VM.

Per informazioni su altre funzionalità per la riduzione dei costi per gli ambienti di sviluppo e test, vedere [Azure DevTest Labs](https://azure.microsoft.com/services/devtest-lab/).

### <a name="turn-on-and-check-out-azure-advisor-recommendations"></a>Attivare e controllare le raccomandazioni di Azure Advisor

[Azure Advisor](../advisor/advisor-overview.md) è una funzionalità in anteprima che consente di ridurre i costi identificando le risorse con un utilizzo basso. Riaccendere in hello portale di Azure:

![Screenshot del pulsante Azure Advisor nel portale di Azure](./media/billing-getting-started/advisor-button.PNG)

Quindi, è possibile ottenere indicazioni utilizzabili in hello **costo** scheda nel dashboard di Advisor hello:

![Screenshot di un esempio di raccomandazione sui costi di Advisor](./media/billing-getting-started/advisor-action.PNG)

Per altre informazioni, vedere [Advisor Cost recommendations](../advisor/advisor-cost-recommendations.md) (Consigli di Azure sui costi).

### <a name="billing-api"></a>API per la fatturazione

Utilizzare i dati di utilizzo di API tooprogrammatically get fatturazione. Utilizzare hello RateCard API e hello utilizzo API insieme tooget uso fatturato. Per altre informazioni, vedere [Ottenere informazioni dettagliate sul consumo di risorse di Microsoft Azure](billing-usage-rate-card-overview.md).

## <a name="other-offers"></a> Risorse aggiuntive e casi speciali

### <a name="ea-csp-and-sponsorship-customers"></a>Clienti EA, CSP e Sponsorship
È consigliabile consultare tooyour account manager o il partner Azure tooget avviato.

| Offerta | Risorse |
|-------------------------------|-----------------------------------------------------------------------------------|
| Contratto Enterprise Agreement (EA) | [Portale EA](https://ea.azure.com/), [documentazione della guida](https://ea.azure.com/helpdocs) e [report di Power BI](https://powerbi.microsoft.com/documentation/powerbi-content-pack-azure-enterprise/) |
| Provider di soluzioni cloud (CSP) | Comunicare con il provider tooyour |
| Azure Sponsorship | [Portale Sponsorship](https://www.microsoftazuresponsorships.com/) |

Se si gestiscono IT per un'organizzazione di grandi dimensioni, è consigliabile leggere [lo scaffolding di Azure enterprise](../azure-resource-manager/resource-manager-subscription-governance.md) hello e [enterprise IT white paper](http://download.microsoft.com/download/F/F/F/FFF60E6C-DBA1-4214-BEFD-3130C340B138/Azure_Onboarding_Guide_for_IT_Organizations_EN_US.pdf) (download di file PDF, solo in lingua inglese).

### <a name="check-your-subscription-and-access"></a>Controllare la sottoscrizione e l'accesso

I costi di visualizzazione richiedono [informazioni toobilling sottoscrizioni a livello di accesso](billing-manage-access.md), ma solo hello amministratore dell'Account può accedere hello [centro Account](https://account.windowsazure.com/Home/Index), modifica delle informazioni di fatturazione e gestire le sottoscrizioni. salve Account è hello parlato iscrizione hello. Per ulteriori informazioni, vedere [aggiungere o modificare ruoli di amministratore di Azure che gestiscono la sottoscrizione hello o servizi](billing-add-change-azure-subscription-administrator.md).

toosee se si sta hello amministratore dell'Account, Vai toohello [pannello sottoscrizioni nel portale di Azure hello](https://portal.azure.com/#blade/Microsoft_Azure_Billing/SubscriptionsBlade) ed esaminare hello elenco delle sottoscrizioni, è possibile accedere. Se in **Ruolo personale** è riportato *Amministratore dell'account*, non sussistono problemi. Se il ruolo indicato è diverso, ad esempio *Proprietario*, non si hanno privilegi completi.

![Schermata del ruolo nella vista delle sottoscrizioni nel portale di Azure hello hello](./media/billing-getting-started/sub-blade-view.PNG)

Se non si sta hello amministratore dell'Account, significa che qualcuno probabilmente ha fornito l'accesso parziale tramite [controllo di accesso basato sui ruoli di Azure Active Directory](../active-directory/role-based-access-control-configure.md) (RBAC). toomanage sottoscrizioni e modificare le informazioni di fatturazione [trovare Account salve](billing-subscription-transfer.md#whoisaa) e chiedere attività hello tooperform o [trasferimento hello sottoscrizione tooyou](billing-subscription-transfer.md).

Se l'amministratore dell'Account non è più con l'organizzazione ed è necessario toomanage fatturazione, [contattare il supporto tecnico](https://portal.azure.com/?#blade/Microsoft_Azure_Support/HelpAndSupportBlade). 
## <a name="need-help-contact-support"></a>Richiesta di assistenza Contattare il supporto tecnico

Per ulteriori informazioni, [contattare il supporto tecnico](https://portal.azure.com/?#blade/Microsoft_Azure_Support/HelpAndSupportBlade) tooget risolta il problema.

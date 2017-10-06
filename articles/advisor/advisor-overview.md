---
title: aaaIntroduction tooAzure Advisor | Documenti Microsoft
description: Utilizzare Advisor Azure toooptimize le distribuzioni di Azure.
services: advisor
documentationcenter: NA
author: kumudd
manager: carmonm
editor: 
ms.assetid: 
ms.service: advisor
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 11/16/2016
ms.author: kumud
ms.openlocfilehash: 5d796fc06366221efdb6f1bda39ab3fb676abfd2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="introduction-tooazure-advisor"></a>Introduzione tooAzure Advisor

Informazioni sulla preparazione di Azure e alle relative funzionalità chiave e le risposte toofrequently domande frequenti.

## <a name="what-is-advisor"></a>Cos'è Advisor?
Advisor è un consulente cloud personalizzate che consentono di eseguire best practices toooptimize le distribuzioni di Azure. Analizza la configurazione di risorsa e i dati di telemetria sull'utilizzo e suggerisce le soluzioni che consentono di migliorare l'economicità hello, prestazioni, disponibilità elevata e sicurezza delle risorse di Azure.

Con Advisor, è possibile:
* Ottenere consigli personalizzati, attuabili e proattivi sulle procedure consigliate. 
* Migliorare le prestazioni hello, sicurezza e la disponibilità elevata delle risorse, non appena si identifica tooreduce opportunità spesa di Azure complessiva.
* Ricevere consigli con azioni proposte incorporate.

È possibile accedere Advisor tramite hello [portale di Azure](https://aka.ms/azureadvisordashboard). Accedi toohello [portale](https://portal.azure.com)selezionare **Sfoglia**, quindi scorrere troppo**Advisor Azure**. dashboard di Advisor Hello visualizza consigli personalizzati per una sottoscrizione selezionata. 

indicazioni Hello sono suddivisi in quattro categorie: 

* **Disponibilità elevata**: tooensure e migliorare la continuità hello delle applicazioni business-critical. Per altre informazioni, vedere [Advisor High Availability recommendations](advisor-high-availability-recommendations.md) (Consigli di Advisor sulla disponibilità elevata).

* **Sicurezza**: toodetect minacce e vulnerabilità che potrebbe causare toosecurity violazioni. Per altre informazioni, vedere [Advisor Security recommendations](advisor-security-recommendations.md) (Consigli di Advisor sulla sicurezza).

* **Prestazioni**: velocità di hello tooimprove delle applicazioni. Per altre informazioni, vedere [Advisor Performance recommendations](advisor-performance-recommendations.md) (Consigli di Advisor sulle prestazioni).

* **Costo**: toooptimize e ridurre di Azure complessivo spesa. Per altre informazioni, vedere [Advisor Cost recommendations](advisor-cost-recommendations.md) (Consigli di Azure sui costi).

  ![Tipi di consigli di Advisor](./media/advisor-overview/advisor-all-tab-examples.png)

> [!NOTE]
> tooaccess raccomandazioni di Advisor, è innanzitutto necessario *registrare la sottoscrizione* con Advisor. Una sottoscrizione viene registrata quando un *sottoscrizione proprietario* avvia hello hello di dashboard e fa clic su Advisor **consigli** pulsante. Si tratta di un'*operazione una tantum*. Dopo la sottoscrizione hello è registrata, è possibile accedere raccomandazioni di Advisor come *proprietario*, *collaboratore*, o *lettore* per una sottoscrizione, un gruppo di risorse, o risorsa specifica.

È possibile fare clic su una raccomandazione toolearn ulteriori informazioni. È possibile inoltre sulle azioni che è possibile eseguire tootake sfruttare l'opportunità o risolvere un problema. 

Advisor offre consigli con azioni incorporate o collegamenti alla documentazione. Fare clic su un'azione inline vengono illustrati un tooimplement "viaggio utente interattiva". Fare clic su un collegamento di documentazione punta toodocumentation che descrive come implementare l'azione di hello toomanually. 

Advisor aggiorna i consigli ogni ora. Se non si prevede un intervento immediato tootake su una raccomandazione, è possibile Posponi per un periodo di tempo specificato o ignorarla. 

## <a name="frequently-asked-questions"></a>Domande frequenti

### <a name="how-do-i-access-advisor"></a>Come si accede ad Advisor?
È possibile accedere Advisor tramite hello [portale di Azure](https://aka.ms/azureadvisordashboard). Accedi toohello [portale](https://portal.azure.com)selezionare **Sfoglia**, quindi scorrere troppo**Advisor Azure**. dashboard di Advisor Hello visualizza consigli personalizzati per una sottoscrizione selezionata. 

È inoltre possibile visualizzare raccomandazioni di Advisor tramite pannello della risorsa macchina virtuale hello. Scegliere una macchina virtuale e quindi scorrere indicazioni tooAdvisor nel menu hello. 

### <a name="what-permissions-do-i-need-tooaccess-advisor"></a>Operazioni di autorizzazioni è necessario tooaccess Advisor?

tooaccess raccomandazioni di Advisor, è innanzitutto necessario *registrare la sottoscrizione* con Advisor. Una sottoscrizione viene registrata quando un *sottoscrizione proprietario* avvia hello hello di dashboard e fa clic su Advisor **consigli** pulsante. Si tratta di un'*operazione una tantum*. Dopo la sottoscrizione hello è registrata, è possibile accedere raccomandazioni di Advisor come *proprietario*, *collaboratore*, o *lettore* per una sottoscrizione, un gruppo di risorse, o risorsa specifica.

### <a name="how-often-are-advisor-recommendations-updated"></a>Con che frequenza vengono aggiornati i consigli di Advisor?

I consigli di Advisor vengono aggiornati ogni ora.

### <a name="what-resources-does-advisor-provide-recommendations-for"></a>Per quali risorse fornisce consigli Advisor?

Advisor fornisce consigli per macchine virtuali, set di disponibilità, gateway applicazione, Servizi app, SQL Server, database SQL e Cache Redis.

### <a name="can-i-snooze-or-dismiss-a-recommendation"></a>È possibile posporre o ignorare un consiglio?

toosnooze o ignorare una raccomandazione, fare clic su hello **Posponi** pulsante o collegamento. È possibile specificare un orario periodo oppure seleziona **mai** toodismiss hello raccomandazione.

## <a name="next-steps"></a>Passaggi successivi

toolearn sulle raccomandazioni di Advisor, vedere:

* [Introduzione ad Advisor](advisor-get-started.md)
* [Advisor High Availability recommendations](advisor-high-availability-recommendations.md) (Consigli di Advisor sulla disponibilità elevata)
* [Advisor Security recommendations](advisor-security-recommendations.md) (Consigli di Advisor sulla sicurezza)
* [Advisor Performance recommendations](advisor-performance-recommendations.md) (Consigli di Advisor sulle prestazioni)
* [Advisor Cost recommendations](advisor-cost-recommendations.md) (Consigli di Advisor sui costi)

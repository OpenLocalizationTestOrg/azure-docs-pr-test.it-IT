---
title: aaaAuto scalare un servizio cloud nel portale di hello | Documenti Microsoft
description: "Informazioni su come toouse hello tooconfigure portale regole di scalabilità automatica per un ruolo web del servizio cloud o un ruolo di lavoro in Azure."
services: cloud-services
documentationcenter: 
author: Thraka
manager: timlt
editor: 
ms.assetid: 701d4404-5cc0-454b-999c-feb94c1685c0
ms.service: cloud-services
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/18/2017
ms.author: adegeo
ms.openlocfilehash: 265f4c8ec5e1ec2f85585df25f18cd0d0c9946a7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooconfigure-auto-scaling-for-a-cloud-service-in-hello-portal"></a>Come tooconfigure auto scaling per un servizio Cloud nel portale di hello
> [!div class="op_single_selector"]
> * [Portale di Azure](cloud-services-how-to-scale-portal.md)
> * [Portale di Azure classico](cloud-services-how-to-scale.md)

È possibile impostare condizioni per un ruolo di lavoro del servizio cloud che attivano operazioni di scalabilità verticale o orizzontale. le condizioni di Hello per ruolo hello possono essere basate su hello CPU, disco o il carico di rete del ruolo hello. È inoltre possibile impostare una condizione in base a una metrica messaggio hello o coda di un'altra risorsa di Azure associata alla sottoscrizione.

> [!NOTE]
> Questo articolo è incentrato sui ruoli Web e di lavoro del servizio cloud. Quando si crea una macchina virtuale (distribuzione classica) direttamente, questa viene ospitata in un servizio cloud. È possibile ridimensionare una macchina virtuale standard tramite l'associazione con un [set di disponibilità](../virtual-machines/windows/classic/configure-availability.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json) e attivarla o disattivarla manualmente.

## <a name="considerations"></a>Considerazioni
È necessario considerare le seguenti informazioni prima di configurare la scalabilità per l'applicazione hello:

* La scalabilità è influenzata dall'utilizzo di core.

    Le istanze del ruolo più ampie usano più core. È possibile scalare un'applicazione solo entro il limite di hello di core per la sottoscrizione. Si supponga, ad esempio, che la sottoscrizione abbia un limite di 20 core. Se si esegue un'applicazione con i due servizi di cloud di medie dimensioni (un totale di 4 core), è possibile solo scalabilità verticale altre distribuzioni del servizio cloud nella sottoscrizione da 16 core hello rimanenti. Per altre informazioni sulle dimensioni, vedere [Dimensioni dei servizi cloud](cloud-services-sizes-specs.md).

* È possibile eseguire la scalabilità in base a una soglia di messaggi in coda. Per ulteriori informazioni su come toouse code, vedere [come toouse hello servizio di archiviazione code](../storage/queues/storage-dotnet-how-to-use-queues.md).

* È anche possibile ridimensionare altre risorse associate alla sottoscrizione.

* tooenable la disponibilità elevata dell'applicazione, è necessario assicurarsi che venga distribuito con due o più istanze del ruolo. Per altre informazioni, vedere [Contratti di servizio](https://azure.microsoft.com/support/legal/sla/).


## <a name="where-scale-is-located"></a>Posizione della scalabilità
Dopo aver selezionato il servizio cloud, è necessario il pannello servizi di cloud hello è visibile.

1. Nel pannello del servizio cloud hello, su hello **ruoli e istanze** riquadro, nome selezionare hello del servizio cloud hello.   
   **IMPORTANTE**: rendere cloud di hello tooclick che servizio ruolo, non hello istanza del ruolo che si trova sotto il ruolo di hello.

    ![](./media/cloud-services-how-to-scale-portal/roles-instances.png)
2. Seleziona hello **scala** riquadro.

    ![](./media/cloud-services-how-to-scale-portal/scale-tile.png)

## <a name="automatic-scale"></a>Scalabilità automatica
È possibile configurare le impostazioni di scalabilità per un ruolo scegliendo tra due modalità **manuale** o **automatica**. Manuale è come previsto, si imposta numero assoluto di hello delle istanze. Automatica consente tuttavia tooset regole che determinano la modalità e in quale molto è consigliabile applicare la scalabilità.

Set hello **scalare** opzione troppo**le regole di pianificazione e delle prestazioni**.

![Impostazioni di scalabilità dei servizi cloud con profilo e regola](./media/cloud-services-how-to-scale-portal/schedule-basics.png)

1. Un profilo esistente.
2. Aggiungere una regola per profilo padre hello.
3. Aggiungere un altro profilo.

Selezionare **Aggiungi profilo**. profilo Hello determina la modalità desiderata toouse per scala hello: **sempre**, **ricorrenza**, **data fissa**.

Dopo aver configurato il profilo di hello e regole, selezionare hello **salvare** icona nella parte superiore di hello.

#### <a name="profile"></a>Profilo
profilo Hello imposta minimo e massimo di istanze per hello scalabilità anche quando l'intervallo di scala è attivo.

* **Sempre**

    Consente di mantenere sempre disponibile questo intervallo di istanze.  

    ![Servizio cloud che esegue sempre la scalabilità](./media/cloud-services-how-to-scale-portal/select-always.png)
* **Ricorrenza**

    Scegliere un set di giorni di hello settimana tooscale.

    ![Scalabilità del servizio cloud con pianificazione ricorrente](./media/cloud-services-how-to-scale-portal/select-recurrence.png)
* **Data fissa**

    Un ruolo di hello tooscale intervallo di date fisse.

    ![Scalabilità del servizio cloud con data fissa](./media/cloud-services-how-to-scale-portal/select-fixed.png)

Dopo aver configurato il profilo di hello, selezionare hello **OK** pulsante nella parte inferiore di hello del pannello profilo hello.

#### <a name="rule"></a>Regola
Le regole vengono aggiunti tooa profilo e rappresentano una condizione che attiva la scala hello.

trigger della regola Hello è basato su una metrica di servizio cloud di hello (utilizzo della CPU, attività del disco o un'attività di rete) toowhich è possibile aggiungere un valore condizionale. È inoltre possibile avere trigger hello in base a una metrica messaggio hello o coda di un'altra risorsa di Azure associata alla sottoscrizione.

![](./media/cloud-services-how-to-scale-portal/rule-settings.png)

Dopo aver configurato la regola hello, selezionare hello **OK** pulsante nella parte inferiore di hello del pannello regole hello.

## <a name="back-toomanual-scale"></a>Scala toomanual indietro
Passare toohello [le impostazioni di scalabilità](#where-scale-is-located) e set hello **scalare** opzione troppo**un numero di istanze immesso manualmente**.

![Impostazioni di scalabilità dei servizi cloud con profilo e regola](./media/cloud-services-how-to-scale-portal/manual-basics.png)

Questa impostazione consente di rimuovere il ridimensionamento automatico dal ruolo hello e quindi è possibile impostare il numero di istanze di hello direttamente.

1. opzione della scala (manuali o automatizzati) Hello.
2. Un ruolo istanza dispositivo di scorrimento tooset hello istanze tooscale per.
3. Istanze di hello ruolo tooscale per.

Dopo aver configurato le impostazioni di scalabilità di hello, selezionare hello **salvare** icona nella parte superiore di hello.

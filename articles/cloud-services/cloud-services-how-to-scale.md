---
title: aaaAuto scalare un servizio cloud nel portale classico hello | Documenti Microsoft
description: "(versione classica) Informazioni su come toouse hello tooconfigure portale classico regole di scalabilità automatica per un ruolo web del servizio cloud o un ruolo di lavoro in Azure."
services: cloud-services
documentationcenter: 
author: Thraka
manager: timlt
editor: 
ms.assetid: eb167d70-4eba-42a4-b157-d8d0688abf4b
ms.service: cloud-services
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/18/2017
ms.author: adegeo
ms.openlocfilehash: ddb5816d4d22192c6d2f51d7508e390779742078
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooconfigure-auto-scaling-for-a-cloud-service-in-hello-classic-portal"></a>Come tooconfigure auto scaling per un servizio Cloud nel portale classico hello
> [!div class="op_single_selector"]
> * [Portale di Azure](cloud-services-how-to-scale-portal.md)
> * [portale di Azure classico](cloud-services-how-to-scale.md)

Nella pagina di scala hello di hello portale di Azure classico, è possibile configurare le impostazioni di scalabilità automatica per il ruolo web o un ruolo di lavoro. In alternativa, è possibile configurare la scalabilità manuale invece della scalabilità automatica basata su regole.

> [!NOTE]
> Questo articolo è incentrato sui ruoli Web e di lavoro del servizio cloud. Quando si crea una macchina virtuale (distribuzione classica) direttamente, questa viene ospitata in un servizio cloud. Alcune di queste informazioni si applicano tipi toothese di macchine virtuali. Ridimensionamento di un set di disponibilità delle macchine virtuali è solo in corso l'arresto li attivare e disattivare in base alle regole di scala hello che è configurare. Per ulteriori informazioni sulle macchine virtuali e i set di disponibilità, vedere [Gestisci hello disponibilità delle macchine virtuali](../virtual-machines/windows/classic/configure-availability.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json)

È necessario considerare le seguenti informazioni prima di configurare la scalabilità per l'applicazione hello:

* La scalabilità è influenzata dall'utilizzo di core.

    Le istanze del ruolo più ampie usano più core. È possibile scalare un'applicazione solo entro il limite di hello di core per la sottoscrizione. Si supponga, ad esempio, che la sottoscrizione abbia un limite di 20 core. Se si esegue un'applicazione con i due servizi di cloud di medie dimensioni (un totale di 4 core), è possibile solo scalabilità verticale altre distribuzioni del servizio cloud nella sottoscrizione da 16 core hello rimanenti. Per altre informazioni sulle dimensioni, vedere [Dimensioni dei servizi cloud](cloud-services-sizes-specs.md).

* È necessario creare una coda e associarla a un ruolo prima di ridimensionare il numero di istanze di un'applicazione in base a una soglia di messaggi. Per ulteriori informazioni, vedere [come toouse hello servizio di archiviazione code](../storage/queues/storage-dotnet-how-to-use-queues.md).

* È possibile scalare le risorse che sono collegati tooyour servizio cloud. Per ulteriori informazioni sul collegamento di risorse, vedere [procedura: collegamento di un servizio cloud di risorse tooa](cloud-services-how-to-manage.md#how-to-link-a-resource-to-a-cloud-service).

* tooenable la disponibilità elevata dell'applicazione, è necessario assicurarsi che venga distribuito con due o più istanze del ruolo. Per altre informazioni, vedere [Contratti di servizio](https://azure.microsoft.com/support/legal/sla/).

## <a name="schedule-scaling"></a>Pianificazione della scalabilità
Per impostazione predefinita, i ruoli non seguono una pianificazione specifica. Pertanto, le impostazioni modificate valide tooall volte e tutti i giorni anno hello. Se si desidera, è possibile configurare il ridimensionamento manuale o automatica per una delle seguenti modalità hello:

* Giorni della settimana
* Fine settimana
* Ore notturne
* Ore diurne
* Date specifiche
* Intervalli di date specifiche

Hello pianificazione è configurata in hello [portale di Azure classico](https://manage.windowsazure.com/) su hello  
**Servizi cloud** > **\[Servizio cloud utente\]** > **Piano** > **\[Produzione o Staging\]**.

Fare clic su hello **Imposta ore di pianificazione** pulsante per ogni ruolo desiderato toochange.

![Ridimensionamento automatico del servizio cloud in base a una pianificazione][scale_schedules]

## <a name="manual-scale"></a>Scalabilità manuale
In hello **scala** pagina, è possibile manualmente aumentare o diminuire il numero di hello di istanze in esecuzione in un servizio cloud. Questa impostazione è configurata per ogni pianificazione che è stato creato o tooall tempo se non è stata creata una pianificazione.

1. In hello [portale di Azure classico](https://manage.windowsazure.com/), fare clic su **servizi Cloud**, quindi fare clic su nome hello del dashboard hello tooopen del servizio cloud hello.
   
   > [!TIP]
   > Se non viene visualizzato il servizio cloud, potrebbe essere necessario toochange da **produzione** troppo**gestione temporanea** o viceversa.

2. Fare clic su **Scale**.
3. Selezionare una pianificazione di hello desiderata toochange sicure per. *Non orari pianificati* è hello predefinito se non si dispone di Nessuna pianificazione definita.
4. Trovare hello **scala in base alla metrica** sezione e selezionare **Nessuno**. Questa impostazione è predefinita hello per tutti i ruoli.
5. Ogni ruolo nel servizio cloud hello dispone di un dispositivo di scorrimento per modificare il numero di hello di toouse di istanze.
   
    ![Ridimensionare manualmente un ruolo del servizio cloud][manual_scale]
   
    Se è necessario più istanze, potrebbe essere necessario hello toochange [dimensione di macchina virtuale del servizio cloud](cloud-services-sizes-specs.md).
6. Fare clic su **Salva**.  
   Verranno aggiunte o rimosse istanze del ruolo in base alle selezioni effettuate.

> [!TIP]
> Ogni volta che viene visualizzato ![][tip_icon] spostare tooit il mouse ed è possibile ottenere la Guida sulle quali un'impostazione specifica.

## <a name="automatic-scale---cpu"></a>Scalabilità automatica - CPU
Questa modalità è adatta se percentuale media di hello di utilizzo della CPU è superiore o inferiore alle soglie specificate. Quando accade questo, vengono create o eliminate istanze del ruolo.

1. In hello [portale di Azure classico](https://manage.windowsazure.com/), fare clic su **servizi Cloud**, quindi fare clic su nome hello del dashboard hello tooopen del servizio cloud hello.
   
   > [!TIP]
   > Se non viene visualizzato il servizio cloud, potrebbe essere necessario toochange da **produzione** troppo**gestione temporanea** o viceversa.

2. Fare clic su **Scale**.
3. Selezionare una pianificazione di hello desiderata toochange sicure per. *Non orari pianificati* è hello predefinito se non si dispone di Nessuna pianificazione definita.
4. Trovare hello **scala in base alla metrica** sezione e selezionare **CPU**.
5. È ora possibile configurare un intervallo minimo e massimo di istanze dei ruoli, l'utilizzo di CPU destinazione hello (tootrigger una scalabilità verticale) e il numero di istanze tooscale su e giù per.

![Ridimensionare un ruolo del servizio cloud per carico CPU][cpu_scale]

> [!TIP]
> Ogni volta che viene visualizzato ![][tip_icon] spostare tooit il mouse ed è possibile ottenere la Guida sulle quali un'impostazione specifica.

## <a name="automatic-scale---queue"></a>Scalabilità automatica - Coda
Questa modalità viene ridimensionato automaticamente se il numero di hello di messaggi in una coda passa sopra o sotto la soglia specificata. Quando accade questo, vengono create o eliminate istanze del ruolo.

1. In hello [portale di Azure classico](https://manage.windowsazure.com/), fare clic su **servizi Cloud**, quindi fare clic su nome hello del dashboard hello tooopen del servizio cloud hello.
   
   > [!TIP]
   > Se non viene visualizzato il servizio cloud, potrebbe essere necessario toochange da **produzione** troppo**gestione temporanea** o viceversa.

2. Fare clic su **Scale**.
3. Trovare hello **scala in base alla metrica** sezione e selezionare **coda**.
4. È ora possibile configurare un intervallo minimo e massimo di istanze di ruoli, coda hello e numero di coda messaggi tooprocess per ogni istanza e il numero di istanze tooscale su e giù per.

![Ridimensionare un ruolo del servizio cloud per coda di messaggi][queue_scale]

> [!TIP]
> Ogni volta che viene visualizzato ![][tip_icon] spostare tooit il mouse ed è possibile ottenere la Guida sulle quali un'impostazione specifica.

## <a name="scale-linked-resources"></a>Scalare risorse collegate
Spesso quando si ridimensiona un ruolo, è utile tooscale i database di hello che utilizza anche l'applicazione hello. Se si collega servizio cloud di hello database toohello, è possibile accedere hello scalabilità impostazioni per tale risorsa facendo clic sul collegamento appropriato hello.

1. In hello [portale di Azure classico](https://manage.windowsazure.com/), fare clic su **servizi Cloud**, quindi fare clic su nome hello del dashboard hello tooopen del servizio cloud hello.
   
   > [!TIP]
   > Se non viene visualizzato il servizio cloud, potrebbe essere necessario toochange da **produzione** troppo**gestione temporanea** o viceversa.

2. Fare clic su **Scale**.
3. Trovare hello **risorse collegate** sezione e fare clic su **gestire la scalabilità per questo database**.
   
   > [!NOTE]
   > Se la sezione delle **risorse collegate** non viene visualizzata, è probabile che non sia presente alcuna risorsa.

![][linked_resource]

[manual_scale]: ./media/cloud-services-how-to-scale/manual-scale.png
[queue_scale]: ./media/cloud-services-how-to-scale/queue-scale.png
[cpu_scale]: ./media/cloud-services-how-to-scale/cpu-scale.png
[tip_icon]: ./media/cloud-services-how-to-scale/tip.png
[scale_schedules]: ./media/cloud-services-how-to-scale/schedules.png
[scale_popup]: ./media/cloud-services-how-to-scale/schedules-dialog.png
[linked_resource]: ./media/cloud-services-how-to-scale/linked-resources.png

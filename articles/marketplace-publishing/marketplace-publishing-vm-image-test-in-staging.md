---
title: "la macchina virtuale è offrire per hello Marketplace aaaTest | Documenti Microsoft"
description: Comprendere in che modo tootest immagine di macchina virtuale per hello Azure Marketplace.
services: marketplace-publishing
documentationcenter: 
author: HannibalSII
manager: hascipio
editor: 
ms.assetid: 7a41c3c6-625c-4478-b804-e124dee89040
ms.service: marketplace
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/01/2016
ms.author: hascipio
ms.openlocfilehash: ab166d2c3c536810a3a8f48330f0482b9b4e58d5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="test-your-vm-offer-for-hello-azure-marketplace-in-staging"></a>Testare l'offerta VM per hello Azure Marketplace in gestione temporanea
Indica lo SKU in una "sandbox" in cui è possibile testare e convalidare le funzionalità prima di distribuirlo toohello Marketplace privata di distribuzione di gestione temporanea. Hello SKU viene visualizzato come nel caso tooa cliente che ha distribuito di gestione temporanea. L'immagine di macchina virtuale deve essere toostaging toobe Certificate inserito.

## <a name="step-1-push-your-offer-toostaging"></a>Passaggio 1: Push toostaging l'offerta
1. In hello **pubblica** scheda, fare clic su **Push tooStaging**.
   
    ![disegno](media/marketplace-publishing-vm-image-test-in-staging/vm-image-push-to-staging.png)
2. Se hello portale di pubblicazione invia una notifica di eventuali errori, è necessario correggerli.
3. In hello **chi può accedere l'offerta di installazione di appoggio?** finestra di dialogo immettere elenco hello delle sottoscrizioni di Azure che si utilizzeranno toopreview l'offerta in hello [portale di anteprima Azure](https://portal.azure.com).
   
   > [!NOTE]
   > Per le macchine virtuali e i modelli di soluzioni, **non** aggiungere all'elenco degli elementi consentiti le sottoscrizioni di tipo CSP, DreamSpark o Azure in Open.
   > 
   > 

    > In caso di macchine virtuali, quando si fa clic sul pulsante hello **tooSTAGING PUSH**, hello alla procedura seguente viene eseguita dietro la scena hello. Si sarà in grado di tooview lo stato di avanzamento hello di ogni passaggio nella scheda pubblicazione hello hello portale di pubblicazione. È necessario controllare questa pagina a intervalli regolari (fino a ottenere lo stato di hello APPRONTATO) per qualsiasi informazione di errore che necessitano di correzione da end.

    > - Inizialmente la richiesta di gestione temporanea passa team certificazione toohello che convalidare hello vhd. Tuttavia, se la richiesta dispone solo di marketing modifica, quindi hello certificazione passaggio viene ignorato.
    > - Una volta completata la certificazione hello, replica di inizio offerta hello in tutti hello Data Center di Azure. In genere richiede 24-48hours per hello replica toocomplete ma può richiedere fino a settimana tooa a seconda delle dimensioni di hello del disco rigido virtuale hello. Tuttavia, se la richiesta dispone di marketing solo modifiche, replica hello è più veloce.
    > - Una volta completata la replica di hello, quindi offerta hello saranno disponibile in hello [portale di Azure](http:/portal.azure.com). A tale hello ora stato diventano presenti hello portale di pubblicazione. Un'offerta di gestione temporanea è visibile in hello [portale di Azure](http:/portal.azure.com) solo tramite gli ID di posta elettronica hello associati hello sottoscrizione con cui hello viene gestita l'offerta.

1. Accedi toohello [portale di anteprima Azure](https://portal.azure.com) utilizzando uno dei hello le sottoscrizioni di Azure è elencato nel passaggio precedente hello.
2. Individuare la propria offerta e convalidare i punti dell'immagine della macchina virtuale:
   
   * Assicurarsi che il contenuto di marketing venga visualizzata correttamente in hello Marketplace.
   * Distribuzione end-to-end dell'immagine di macchina virtuale hello.
     
      ![img-map-portal](media/marketplace-publishing-push-to-staging/pubportal-mapping-azure-portal.jpg)

> [!IMPORTANT]
> L'offerta rimarrà fino a quando non è informare Microsoft tramite hello portale di pubblicazione di gestione temporanea [**pubblica** scheda > fare clic sul pulsante hello **"Richiesta di approvazione tooPush tooProduction"**] che si è pronti toopush tooproduction. Si tratta di un toohave ideale ora che tutti i membri del team di controllare tutti gli elementi in preparazione per l'offerta prevede elencati.
> 
> Hello piattaforma di gestione temporanea è progettato per test offerta hello in modalità di anteprima da server di pubblicazione hello. È fortemente sconsigliato l'uso di questa piattaforma a fini commerciali.
> 
> 

## <a name="next-steps"></a>Passaggi successivi
Ora che l'offerta è "gestione temporanea" e dopo aver testato le funzionalità e contenuti di marketing, è possibile procedere pubblicazione finale toohello fase **passaggio 4**: [distribuzione il toohello offerta Marketplace](marketplace-publishing-push-to-production.md).

## <a name="see-also"></a>Vedere anche
* [Guida introduttiva: come toopublish un toohello offerta Azure Marketplace](marketplace-publishing-getting-started.md)


---
title: aaaDeploy il toohello offerta Azure Marketplace | Documenti Microsoft
description: "Apprendere e seguire i passaggi hello istruzioni toodeploy l'offerta, l'immagine di macchina virtuale, il servizio di sviluppatore, servizio dati e così via - toohello Azure Marketplace."
services: marketplace-publishing
documentationcenter: 
author: HannibalSII
manager: hascipio
editor: 
ms.assetid: 8f79b891-84e2-4f41-ba0d-66420e2c6b2e
ms.service: marketplace
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/02/2016
ms.author: hascipio
ms.openlocfilehash: ab0bb7c78020187505c2d5f09c4de246987ecd97
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-your-offer-toohello-azure-marketplace"></a>Distribuire il toohello offerta Azure Marketplace
Quando si è soddisfatti dell'offerta (ovvero, il test di scenari dei clienti, marketing contenuto e così via) e si è pronti toolaunch, richiesta **Push tooproduction** su hello **pubblica** scheda.  

1. Hello quattro passaggi nella pagina di procedura dettagliata hello in hello portale di pubblicazione deve essere completato e verde. Per le offerte di macchina virtuale, verificare che hello indicazioni vengono seguiti.
   
    ![disegno][img-pubportal-walkthru-checked]
2. Seleziona hello **pubblica** scheda elenco hello hello lato sinistro.
   
    ![disegno][img-pubportal-menu-publish]
3. Fare clic sul pulsante hello **richiesta approvazione toopush tooproduction**. Una volta effettuata la richiesta di hello, team approvazione hello esegue una verifica finale e quindi l'offerta è disponibile nel hello Azure Marketplace.
   
    ![disegno][img-pubportal-publish-pushproduction]

> [!IMPORTANT]
> In caso di macchine virtuali, quando si fa clic su hello pulsante richiesta approvazione toopush tooproduction hello alla procedura seguente viene eseguita dietro la scena hello. Si sarà in grado di tooview lo stato di avanzamento hello di ogni passaggio nella scheda pubblicazione hello hello portale di pubblicazione. È necessario controllare questa pagina a intervalli regolari (fino a ottenere lo stato di hello "Elencati") per qualsiasi informazione di errore che necessitano di correzione da end.
> 
> * Inizialmente la richiesta di produzione va team certificazione toohello che convalidare hello vhd. Tuttavia, se si sta aggiornando l'offerta già elencato e richiesta hello dispone solo di marketing modifica, quindi hello certificazione passaggio viene ignorato.
> * Al passaggio successivo hello, richiesta hello provenire team di convalida del contenuto toohello che verificare hello contenuti dell'offerta di hello di marketing.
> * Se hello sopra passaggi hanno esito positivo, l'offerta hello è approvato nell'ambiente di produzione. In questo momento, hello stato diventi "elencate" nel portale di pubblicazione hello. Questo stato di "Elencati" non implica tuttavia che il processo di hello è stato completato. Hello dopo toobe necessità passaggi completo prima di avviare hello offerta è disponibile in hello Azure Marketplace.
> * Una volta approvata offerta hello nell'ambiente di produzione nel passaggio hello precedente, la replica di inizio offerta hello in tutti hello Data Center di Azure. In genere richiede 24-48hours per hello replica toocomplete ma può richiedere fino a settimana tooa a seconda delle dimensioni di hello del disco rigido virtuale hello. Tuttavia, se si sta aggiornando l'offerta già elencato e ha solo marketing modifiche, replica hello è più veloce.
> * Al termine della replica hello viene offerta hello sarà disponibile in hello Azure Marketplace.
> 
> È sempre possibile eliminare l'offerta di hello mentre è in un **bozza** stato (ad esempio, mai **Push toostaging** o **Push tooproduction**). In hello **cronologia** scheda, fare clic su hello **Elimina bozza** pulsante nella parte inferiore di hello di hello pagina toodelete una bozza.
> 
> 

## <a name="production-checklist-for-all-virtual-machine-offers"></a>Elenco di controllo di produzione per tutte le offerte per macchina virtuale
* Assicurarsi di essere un partner Microsoft Azure Certified
* Nella scheda SKU hello, opzione hello "Hide SKU da hello Marketplace perché deve sempre essere acquistato tramite un modello di soluzione" deve essere contrassegnato come Sì solo se hello SKU è una parte di un modello di soluzione. In tutti gli altri casi di hello, questa opzione deve sempre essere contrassegnata come No.
* Ricorda: Non modificare impostazione di visibilità SKU hello quando hello SKU è elencata. Questa funzionalità non è supportata.
* Verificare che i logo hello osservate le linee guida del logo di Azure Marketplace toohello specificate di seguito.
* L'offerta e la descrizione dello SKU non devono essere uguali.
* Il titolo dello SKU e il riepilogo lungo dell'offerta non devono essere uguali.
* Il titolo dello SKU e il riepilogo dell'offerta non devono essere uguali.
* Per un'offerta con più SKU, i titoli degli SKU non devono essere identici.

**Linee guida per i logo in Azure Marketplace**

* Hello progettazione di Azure dispone di una tavolozza dei colori semplice. Mantenere il numero di hello database primario e secondario colori sul logo bassa.
* colori del tema Hello di hello portale di Azure sono bianchi e neri. Pertanto evitare di utilizzare i colori come colore di sfondo hello di loghi. Utilizzare alcuni colore che renderebbe i logo classificarli hello portale di Azure. Si consiglia di usare colori primari semplici. Se si utilizza sfondo trasparente, assicurarsi che tale hello logo, testo non bianchi o neri.
* Non utilizzare uno sfondo sfumato sul logo hello.
* Evitare di inserire testo, anche l'azienda o il nome dell'organizzazione, sul logo hello.
* Hello aspetto del logo deve essere 'semplice' ed evitare le sfumature.
* logo di Hello non possono essere ridimensionato.

**Ulteriori linee guida per il logo Hero hello:**

* logo Hero Hello è facoltativo. server di pubblicazione Hello possibile scegliere di non tooupload un logo Hero. **Icona di hero hello tuttavia una volta caricato non può essere eliminato da hello portale di pubblicazione. In quel momento, partner hello deve seguire le istruzioni di hello Azure Marketplace per le icone Hero offerta hello else non saranno tooproduction approvati.**
* Nome visualizzato editore, hello e titolo SKU Hello offrono riepilogo lungo vengono visualizzati nel colore bianco. Pertanto è consigliabile evitare di mantenere qualsiasi colore chiaro in background hello di hello Hero icona. Lo sfondo nero, bianco o trasparente non è ammesso per le icone del logo alto.
* Hello nome visualizzato editore, titolo SKU, offerta hello riepilogo lunghe e hello pulsante Crea sono incorporati a livello di codice all'interno di logo Hero hello dopo offerta hello passa elencato. Pertanto non è necessario immettere il testo durante la progettazione dei logo Hero hello. Lasciare vuoto lo spazio vuoto a destra di hello poiché testo hello (ad esempio nome visualizzato editore, titolo SKU, offerta hello riepilogo lunghe) verrà inclusa a livello di codice da Microsoft lì. spazio vuoto di Hello per testo hello deve essere 415 x 100 su hello destra (e viene applicato un offset da 370px da sinistra hello).

## <a name="additional-production-checklist-for-already-listed-virtual-machine-offers"></a>Elenco di controllo di produzione aggiuntivo per le offerte per macchina virtuale già elencate
* Controllare che se è già presente un'offerta con hello nome stesso offerte dall'azienda. Se Sì, è necessario aggiungere una nuova versione di hello SKU nell'offerta esistente di hello anziché creare una nuova offerta di duplicati.
* Disco dati non modifichino tra due versioni di hello stesso SKU.
* Hello Azure Marketplace non supporta la modifica di hello prezzi elencati SKU quanto che influisce sulla fatturazione hello di clienti esistenti hello. Assicurarsi di non modificare hello prezzi di SKU hello elencato in aree geografiche di hello in hello SKU è disponibile. Tuttavia, è possibile aggiungere nuovi SKU o aggiungere nuovo tooan aree esistente SKU.

## <a name="next-steps"></a>Passaggi successivi
Una volta offerta hello passa in tempo reale, test hello cliente scenari toovalidate che tutti i contratti di hello e funzionalità di lavoro correttamente nell'ambiente di produzione hello come ambiente di gestione temporanea hello testata e convalidata in.

## <a name="see-also"></a>Vedere anche
* [Guida introduttiva: come toopublish un toohello offerta Azure Marketplace](marketplace-publishing-getting-started.md)

[img-pubportal-walkthru-checked]:media/marketplace-publishing-push-to-production/pubportal-walkthru-checked.png
[img-pubportal-menu-publish]:media/marketplace-publishing-push-to-production/pubportal-menu-publish.png
[img-pubportal-publish-pushproduction]:media/marketplace-publishing-push-to-production/pubportal-publish-pushproduction.png

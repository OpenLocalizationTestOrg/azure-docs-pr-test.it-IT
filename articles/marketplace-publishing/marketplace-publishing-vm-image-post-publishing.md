---
title: immagine di macchina virtuale in Azure Marketplace hello aaaManaging | Documenti Microsoft
description: "Guida dettagliata sulla modalità toomanage la macchina virtuale dell'immagine in Azure Marketplace hello dopo la pubblicazione iniziale"
services: Azure Marketplace
documentationcenter: 
author: HannibalSII
manager: hascipio
editor: 
ms.assetid: cc8648d4-59c2-4678-b47d-992300677537
ms.service: marketplace
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: Azure
ms.workload: na
ms.date: 08/03/2016
ms.author: hascipio;
ms.openlocfilehash: 47a082e686e1248ceacb844d3c0f2f5c33133dab
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="post-production-guide-for-virtual-machine-offers-in-hello-azure-marketplace"></a>Guida di post-produzione per la macchina virtuale offre hello Azure Marketplace
In questo articolo viene illustrato come aggiornare un'offerta di macchina virtuale in tempo reale in hello Azure Marketplace. Semplificato il processo di hello di aggiunta di uno o più nuovi SKU tooan offerta esistente. Vengono inoltre processo hello di rimozione di un'offerta di macchina virtuale in tempo reale o SKU da hello Marketplace.

Dopo un'offerta/SKU preconfigurato in hello [portale di Azure](http://portal.azure.com), non è possibile modificare hello caselle di testo seguente:

* **Identificatore offerta**: In hello pubblicazione portale andare troppo**macchine virtuali** e selezionare l'offerta. Quindi fare clic su **Immagini VM** > **Offer Identifier** (Identificatore offerta).
* **Identificatore di SKU**: In hello pubblicazione portale andare troppo**macchine virtuali** e selezionare l'offerta. Quindi fare clic su **SKU** > **Aggiungere uno SKU**.
* **Server di pubblicazione Namespace**: In hello pubblicazione portale andare troppo**macchine virtuali** > **procedura dettagliata** > **indicare ci sulla società** (disponibile in "Passaggio 2 registrazione della propria azienda") > **Namespace Publisher** > **Namespace**.

Dopo l'offerta/SKU hello è elencato nella hello [Marketplace](http://azure.microsoft.com/marketplace), non è possibile modificare hello caselle di testo seguente:

* **Identificatore offerta**: In hello pubblicazione portale andare troppo**macchine virtuali** e selezionare l'offerta. Quindi fare clic su **Immagini VM** > **Offer Identifier** (Identificatore offerta).
* **Identificatore di SKU**: In hello pubblicazione portale andare troppo**macchine virtuali** e selezionare l'offerta. Quindi fare clic su **SKU** > **Aggiungere uno SKU**.
* **Server di pubblicazione Namespace**: In hello pubblicazione portale andare troppo**macchine virtuali** > **procedura dettagliata** > **indicare ci sulla società** (disponibile in "Passaggio 2 Register") **Namespace publisher** > **Namespace**.
* **Porte**: In hello pubblicazione portale andare troppo**macchine virtuali** e selezionare l'offerta. Quindi fare clic su **Immagini VM** > **Porte aperte**.
* **Modifica dei prezzi degli SKU elencati**
* **Modifica del modello di fatturazione degli SKU elencati**
* **Rimozione delle aree di fatturazione degli SKU elencati**
* **Numero di SKU(s) elencati del disco dati in continua evoluzione hello**

## <a name="update-hello-technical-details-of-a-sku"></a>Aggiornare i dettagli tecnici di hello di uno SKU
un nuovo toohello versione tooadd elencati SKU e ripubblicare l'offerta, seguire questi passaggi:

1. Accedi toohello [pubblicazione portale](https://publish.windowsazure.com).
2. Passare toohello **macchine virtuali** scheda e selezionare l'offerta.
3. Dal menu hello hello sinistra, fare clic su hello **immagini di macchina virtuale** scheda.
4. In hello **SKU** sezione, individuare hello SKU che si desidera tooupdate.
5. Aggiungere un nuovo numero di versione per hello SKU e fare clic su hello  **+**  pulsante. nuova versione di Hello deve essere in formato X.Y.Z, dove X, Y e Z sono numeri interi. Le modifiche della versione devono essere solo incrementali.
6. In hello **URL VHD del sistema operativo** immettere firma di accesso condiviso hello URI creato per il sistema operativo hello disco rigido virtuale, quindi salvare le modifiche di hello.

   > [!IMPORTANT]
   > È Impossibile incremento/decremento numero di dischi dati hello di uno SKU elencato. È necessario in questo caso toocreate uno SKU di nuovo. Per istruzioni dettagliate, vedere la sezione toohello [aggiungere uno SKU di nuovo in un'offerta elencato](#add-a-new-sku-under-a-listed-offer).
   >
   >
7. Passare toohello **pubblica** scheda e fare clic su **tooSTAGING PUSH**. Per istruzioni dettagliate sulla verifica l'offerta in hello ambiente di gestione temporanea, vedere [testare l'offerta VM per hello Marketplace](marketplace-publishing-vm-image-test-in-staging.md).
8. Dopo aver testato l'offerta in gestione temporanea, andare toohello **pubblica** scheda hello portale di pubblicazione. Fare clic su **richiesta approvazione tooPUSH tooPRODUCTION** toorepublish l'offerta in Marketplace hello.

    ![VM Images (Immagini di VM)](media/marketplace-publishing-vm-image-post-publishing/img01_07.png)

## <a name="update-hello-nontechnical-details-of-an-offer-or-a-sku"></a>L'aggiornamento dei dettagli di tecniche hello di un'offerta o di uno SKU
È possibile aggiornare hello tecniche (marketing, legale, supporto, categorie) i dettagli dell'offerta in tempo reale o SKU in hello Marketplace.

### <a name="update-hello-offer-description-and-logos"></a>Descrizione dell'offerta aggiornamento hello e logo
hello tooupdate i dettagli dell'offerta e ripubblicare l'offerta, eseguire la procedura seguente:

1. Accedi toohello [pubblicazione portale](https://publish.windowsazure.com).
2. Passare toohello **macchine virtuali** scheda e selezionare l'offerta.
3. Dal menu hello hello sinistra, fare clic su hello **MARKETING** scheda.
4. Fare clic su **English (US)**.
5. Fare clic su hello **dettagli** scheda. In hello **descrizione** una sezione di offerta di aggiornamento hello **titolo**, **riepilogo**, e **riepilogo lungo** e salvare le modifiche di hello.

   > [!NOTE]
   > Quando si aggiornano i dettagli SKU hello, tenere presenti queste limitazioni: 
   * Non immettere testo duplicato per descrizione offerta hello e una descrizione di SKU hello.
   * Non immettere testo duplicato per il titolo SKU hello e offerta hello riepilogo lunghe. 
   * Non immettere testo duplicato per il riepilogo di offerta di hello e hello SKU titolo.
   >
   >

    ![Dettagli](media/marketplace-publishing-vm-image-post-publishing/img02.1_05.png)
6. In hello **logo** sezione di hello **dettagli** scheda, aggiornare il logo hello. Assicurarsi che i logo hello seguano hello [linee guida di Azure Marketplace](marketplace-publishing-push-to-staging.md#step-1-provide-marketplace-marketing-content).

   > [!NOTE]
   > L'icona alta è facoltativa. È possibile scegliere non tooupload un'icona hero. Dopo aver caricata un'icona eroe, vi sono non comunque toodelete effettuare il provisioning da hello portale di pubblicazione. Seguire hello [linee guida sull'icona hero](marketplace-publishing-push-to-staging.md#step-1-provide-marketplace-marketing-content).
   >
   >
7. Passare toohello **pubblica** scheda e fare clic su **tooSTAGING PUSH**. Per istruzioni dettagliate sulla verifica l'offerta in hello ambiente di gestione temporanea, vedere [testare l'offerta VM per hello Marketplace](marketplace-publishing-vm-image-test-in-staging.md).
8. Dopo aver testato l'offerta in gestione temporanea, andare toohello **pubblica** scheda hello portale di pubblicazione. Fare clic su **richiesta approvazione tooPUSH tooPRODUCTION** toorepublish l'offerta in Marketplace hello.

    ![Loghi](media/marketplace-publishing-vm-image-post-publishing/img02.1_08.png)

### <a name="update-hello-sku-description"></a>Aggiornare la descrizione di SKU hello
hello tooupdate SKU dettagli e ripubblicare l'offerta, seguire questi passaggi:

1. Accedi toohello [pubblicazione portale](https://publish.windowsazure.com).
2. Passare toohello **macchine virtuali** scheda e selezionare l'offerta.
3. Dal menu hello hello sinistra, fare clic su hello **MARKETING** scheda.
4. Fare clic su **English (US)**.
5. Fare clic su hello **piani** scheda. In hello **SKU** sezione, aggiornare hello SKU **titolo**, **riepilogo**, e **descrizione** e salvare le modifiche di hello.

   > [!NOTE]
   > Quando si aggiornano i dettagli SKU hello, tenere presenti queste limitazioni: 
   * Non immettere testo duplicato per descrizione offerta hello e una descrizione di SKU hello. 
   * Non immettere testo duplicato per il titolo SKU hello e offerta hello riepilogo lunghe. 
   * Non immettere testo duplicato per il riepilogo di offerta di hello e hello SKU titolo.
   >
   >
6. Passare toohello **pubblica** scheda e fare clic su **tooSTAGING PUSH**. Per istruzioni dettagliate sulla verifica l'offerta in hello ambiente di gestione temporanea, vedere [testare l'offerta VM per hello Marketplace](marketplace-publishing-vm-image-test-in-staging.md).
7. Dopo aver testato l'offerta in gestione temporanea, andare toohello **pubblica** scheda hello portale di pubblicazione. Fare clic su **richiesta approvazione tooPUSH tooPRODUCTION** toorepublish l'offerta in Marketplace hello.

    ![Piani](media/marketplace-publishing-vm-image-post-publishing/img02.2_07.png)

### <a name="change-existing-links-or-add-new-links"></a>Modificare i collegamenti esistenti o aggiungere nuovi collegamenti
i collegamenti esistenti toochange o aggiungere nuovi collegamenti e quindi ripubblicare l'offerta, eseguire la procedura seguente:

1. Accedi toohello [pubblicazione portale](https://publish.windowsazure.com).
2. Passare toohello **macchine virtuali** scheda e selezionare l'offerta.
3. Dal menu hello hello sinistra, fare clic su hello **MARKETING** scheda.
4. Fare clic su **English (US)**.
5. Fare clic su hello **collegamenti** scheda.
6. un nuovo collegamento, hello tooadd **collegamenti** fare clic su **+ Aggiungi collegamento**. In hello **Aggiungi collegamento** finestra di dialogo immettere il collegamento hello **titolo** e **URL** e salvare le modifiche di hello. È possibile immettere qualsiasi collegamento che contiene informazioni utili per i clienti.
7. tooupdate o eliminare un collegamento esistente, selezionare il collegamento di hello e fare clic su hello **modifica** pulsante o hello **eliminare** pulsante.

   > [!NOTE]
   > Verificare che i collegamenti di hello immesse in questa sezione funzionino correttamente, poiché questi collegamenti vengono convalidati durante il processo di richiesta di produzione.
   >
   >
8. Passare toohello **pubblica** scheda e fare clic su **tooSTAGING PUSH**. Per istruzioni dettagliate sulla verifica l'offerta in hello ambiente di gestione temporanea, vedere [testare l'offerta VM per hello Marketplace](marketplace-publishing-vm-image-test-in-staging.md).
9. Dopo aver testato l'offerta in gestione temporanea, andare toohello **pubblica** scheda hello portale di pubblicazione. Fare clic su **richiesta approvazione tooPUSH tooPRODUCTION** toorepublish l'offerta in Marketplace hello.

    ![Collegamenti](media/marketplace-publishing-vm-image-post-publishing/img02.3_09-01.png)

    ![Aggiungi collegamento](media/marketplace-publishing-vm-image-post-publishing/img02.3-2.png)

### <a name="change-an-existing-sample-image-or-add-a-new-sample-image"></a>Modificare un'immagine di esempio esistente o aggiungere una nuova immagine di esempio
un esempio esistente toochange immagine o aggiungere nuove immagini di esempio e quindi ripubblicare l'offerta, eseguire la procedura seguente:

> [!NOTE]
> Viene visualizzata l'immagine di un solo campione in hello [portale di Azure](https://portal.azure.com).
>
>

1. Accedi toohello [pubblicazione portale](https://publish.windowsazure.com).
2. Passare toohello **macchine virtuali** scheda e selezionare l'offerta.
3. Dal menu hello hello sinistra, fare clic su hello **MARKETING** scheda.
4. Fare clic su **English (US)**.
5. Fare clic su hello **immagini di esempio** scheda.
6. una nuova immagine di esempio, in hello tooadd **immagini di esempio** fare clic su **caricare una nuova immagine** e salvare le modifiche di hello.

   > [!NOTE]
   > L'inclusione di un'immagine di esempio è facoltativa.
   >
7. Passare toohello **pubblica** scheda e fare clic su **tooSTAGING PUSH**. Per istruzioni dettagliate sulla verifica l'offerta in hello ambiente di gestione temporanea, vedere [testare l'offerta VM per hello Marketplace](marketplace-publishing-vm-image-test-in-staging.md).
8. Dopo aver testato l'offerta in gestione temporanea, andare toohello **pubblica** scheda hello portale di pubblicazione. Fare clic su **richiesta approvazione tooPUSH tooPRODUCTION** toorepublish l'offerta in Marketplace hello.

    ![Immagini di esempio](media/marketplace-publishing-vm-image-post-publishing/img02.4_09.png)

### <a name="update-hello-legal-content"></a>Aggiornare il contenuto di persone hello
tooupdate hello contenuto legale e ripubblicare l'offerta, eseguire la procedura seguente:

1. Accedi toohello [pubblicazione portale](https://publish.windowsazure.com).
2. Passare toohello **macchine virtuali** scheda e selezionare l'offerta.
3. Dal menu hello hello sinistra, fare clic su hello **MARKETING** scheda.
4. Fare clic su **English (US)**.
5. Fare clic su hello **legali** scheda. In hello **legali** sezione, aggiornare i criteri o condizioni di utilizzo. Immettere o incollare i criteri o condizioni di hello in hello **condizioni per l'utilizzo** e salvare le modifiche di hello.
6. Hello carattere limite legali hello d'uso è di 1 milione di caratteri.
7. Passare toohello **pubblica** scheda e fare clic su **tooSTAGING PUSH**. Per istruzioni dettagliate sulla verifica l'offerta in hello ambiente di gestione temporanea, vedere [testare l'offerta VM per hello Marketplace](marketplace-publishing-vm-image-test-in-staging.md).
8. Dopo aver testato l'offerta in gestione temporanea, andare toohello **pubblica** scheda hello portale di pubblicazione. Fare clic su **richiesta approvazione tooPUSH tooPRODUCTION** toorepublish l'offerta in Marketplace hello.

    ![Note legali](media/marketplace-publishing-vm-image-post-publishing/img02.5_08.png)

### <a name="update-hello-support-information"></a>Aggiornare le informazioni di supporto hello
hello tooupdate informazioni sul supporto e ripubblicare l'offerta, eseguire la procedura seguente:

1. Accedi toohello [pubblicazione portale](https://publish.windowsazure.com).
2. Passare toohello **macchine virtuali** scheda e selezionare l'offerta.
3. Dal menu hello hello sinistra, fare clic su hello **supporto** scheda.
4. In hello **contattare Engineering** sezione aggiornamento hello engineering i dettagli di contatto. Tali dettagli vengono utilizzati solo le comunicazioni interne tra partner hello e Microsoft.
5. In hello **il supporto clienti** sezione, aggiornare i dettagli di contatto di supporto di hello e hello **SUPPORTANO URL**. Tali dettagli vengono utilizzati solo le comunicazioni interne tra partner hello e Microsoft.

   > [!NOTE]
   > Se si desidera tooprovide solo il supporto di posta elettronica, immettere un numero di telefono fittizio in hello **il supporto clienti** sezione. In questo caso, viene utilizzato l'email hello fornito.
   >
   >
6. Passare toohello **pubblica** scheda e fare clic su **tooSTAGING PUSH**. Per istruzioni dettagliate sulla verifica l'offerta in hello ambiente di gestione temporanea, vedere [testare l'offerta VM per hello Marketplace](marketplace-publishing-vm-image-test-in-staging.md).
7. Dopo aver testato l'offerta in gestione temporanea, andare toohello **pubblica** scheda hello portale di pubblicazione. Fare clic su **richiesta approvazione tooPUSH tooPRODUCTION** toorepublish l'offerta in Marketplace hello.

    ![Supporto](media/marketplace-publishing-vm-image-post-publishing/img02.6_07.png)

### <a name="update-hello-categories"></a>Aggiornare le categorie di hello
hello tooupdate categorie sezione per l'offerta e ripubblicano l'offerta, seguire questi passaggi:

1. Accedi toohello [pubblicazione portale](https://publish.windowsazure.com).
2. Passare toohello **macchine virtuali** scheda e selezionare l'offerta.
3. Dal menu hello hello sinistra, fare clic su hello **categorie** scheda.
4. In hello **categorie** sezione, aggiornare le categorie di hello per l'offerta e salvare le modifiche di hello. È possibile scegliere le categorie di toofive per la raccolta di hello Azure Marketplace.
5. Passare toohello **pubblica** scheda e fare clic su **tooSTAGING PUSH**. Per istruzioni dettagliate sulla verifica l'offerta in hello ambiente di gestione temporanea, vedere [testare l'offerta VM per hello Marketplace](marketplace-publishing-vm-image-test-in-staging.md).
6. Dopo aver testato l'offerta in gestione temporanea, andare toohello **pubblica** scheda hello portale di pubblicazione. Fare clic su **richiesta approvazione tooPUSH tooPRODUCTION** toorepublish l'offerta in Marketplace hello.

    ![Categorie](media/marketplace-publishing-vm-image-post-publishing/img02.7_06.png)

## <a name="add-a-new-sku-under-a-listed-offer"></a>Aggiungere un nuovo SKU in un'offerta elencata
tooadd uno SKU di nuovo nell'offerta in tempo reale, seguire questi passaggi:

1. Accedi toohello [pubblicazione portale](https://publish.windowsazure.com).
2. Passare toohello **macchine virtuali** scheda e selezionare l'offerta.
3. Dal menu hello hello sinistra, fare clic su hello **SKU** scheda. Fare quindi clic su **Add a SKU** (Aggiungi SKU). 
4. Nella finestra di dialogo hello, immettere un **identificatore SKU** in lettere minuscole. Seleziona hello **portare il proprio modello di fatturazione di licenza (BYOL)** casella di controllo se si desidera toopublish hello SKU di nuovo con un modello di fatturazione BYOL. In caso contrario, deselezionare la casella di controllo hello. Fare clic su hello segni di graduazione contrassegno toocreate uno SKU di nuovo. Se non si sceglie di modello di fatturazione BYOL hello, modello di fatturazione hello viene impostata automaticamente toohourly. Se si desidera prova gratuita di 30 giorni hello per modello di fatturazione oraria hello, selezionare **un mese** per **è disponibile una versione di valutazione gratuita?** In caso contrario, selezionare **Nessuna versione di prova**. (**è disponibile una versione di valutazione gratuita?**  viene visualizzata solo se non è stato selezionato BYOL durante la creazione di hello nuovo SKU.)

   > [!IMPORTANT]
   > **Nascondere questa SKU di hello Marketplace perché deve sempre essere acquistato tramite un modello di soluzione** deve essere **Sì** *solo* se approvazione per la pubblicazione di un modello di soluzione. Diversamente, l'opzione deve essere sempre **No**.
   >
   >
4. Dal menu hello hello sinistra, fare clic su hello **immagini di macchina virtuale** scheda e scoprire hello nuova unità SKU che è stato creato.
5. tooset hello SKU di nuovo verso l'alto, vedere [ottenere certificazione per l'immagine di macchina virtuale](marketplace-publishing-vm-image-creation.md#5-obtain-certification-for-your-vm-image) per informazioni aggiuntive.
6. materiale di marketing tooadd hello nuovo SKU, vedere [Marketplace fornire contenuti di marketing](marketplace-publishing-push-to-staging.md#step-1-provide-marketplace-marketing-content).
7. informazioni sui prezzi per tooadd hello nuovo SKU, vedere [impostare i prezzi](marketplace-publishing-push-to-staging.md#step-2-set-your-prices).
8. Passare toohello **pubblica** scheda e fare clic su **tooSTAGING PUSH**. Per istruzioni dettagliate sulla verifica l'offerta in hello ambiente di gestione temporanea, vedere [testare l'offerta VM per hello Marketplace](marketplace-publishing-vm-image-test-in-staging.md).
9. Dopo aver testato l'offerta in gestione temporanea, andare toohello **pubblica** scheda hello portale di pubblicazione. Fare clic su **richiesta approvazione tooPUSH tooPRODUCTION** toorepublish l'offerta in Marketplace hello.

    ![SKU](media/marketplace-publishing-vm-image-post-publishing/img03_09-01.png)

    ![Aggiungere uno SKU](media/marketplace-publishing-vm-image-post-publishing/img03_09-02.png)

## <a name="change-hello-data-disk-count-for-a-listed-sku"></a>Modificare hello numero di dischi dati per una SKU elencati
È Impossibile incremento/decremento numero di dischi dati hello di uno SKU elencato. È necessario in questo caso toocreate uno SKU di nuovo. Per istruzioni dettagliate, vedere la sezione toohello [aggiungere uno SKU di nuovo in un'offerta elencato](#add-a-new-sku-under-a-listed-offer).

## <a name="delete-a-listed-offer-from-hello-marketplace"></a>Eliminare un'offerta elencata da hello Marketplace
Vari aspetti necessario toobe preso in considerazione nel caso di hello di tooremove una richiesta di un'offerta in tempo reale. alle linee guida tooget tooremove team di supporto hello un'offerta elencata da hello Marketplace, seguire questi passaggi:

1. Generare un ticket di supporto su hello [creare un evento imprevisto](https://support.microsoft.com/en-us/getsupport?wf=0&tenant=ClassicCommercial&oaspworkflow=start_1.0.0.0&locale=en-us&supportregion=en-us&pesid=15635&ccsid=635993707583706681) pagina.

2. Selezionare il **Tipo di problema** nell'elenco **Gestione delle offerte** e selezionare una **Categoria** come **Modifying an offer and/or SKU already in production** (Modifica di un'offerta e/o di uno SKU già in produzione).
3. Inviare la richiesta di hello.

il team di supporto Hello semplificato processo di eliminazione hello offerta/SKU.

> [!NOTE]
> È sempre possibile eliminare offerta hello mentre è in stato di bozza (ma non gestione temporanea o produzione). In hello **cronologia** scheda, fare clic su **Elimina bozza**.
>
>

## <a name="delete-a-listed-sku-from-hello-marketplace"></a>Eliminare un elenco di SKU dal hello Marketplace
toodelete uno SKU elencato da hello Marketplace, seguire questi passaggi:

1. Accedi toohello [pubblicazione portale](https://publish.windowsazure.com).

2. Passare toohello **macchine virtuali** scheda e selezionare l'offerta.
3. Nel riquadro a sinistra di hello hello fare clic su hello **SKU** scheda.
4. Seleziona hello SKU che si desidera toodelete e fare clic su hello **eliminare** pulsante.
5. Passare toohello **pubblica** scheda hello portale di pubblicazione. Fare clic su **richiesta approvazione tooPUSH tooPRODUCTION** toorepublish hello offerta in Marketplace hello.
6. Dopo l'offerta di hello viene ripubblicata senza modifiche in hello Marketplace, hello SKU viene eliminato dal hello Marketplace e hello portale di Azure.

## <a name="delete-hello-current-version-of-a-listed-sku-from-hello-marketplace"></a>Elimina versione corrente di hello di uno SKU elencato da hello Marketplace
versione corrente di hello toodelete di uno SKU elencato da hello Marketplace, seguire questi passaggi: 

1. Accedi toohello [pubblicazione portale](https://publish.windowsazure.com).

2. Passare toohello **macchine virtuali** scheda e selezionare l'offerta.
3. Dal menu hello hello sinistra, fare clic su hello **immagini di macchina virtuale** scheda.
4. Seleziona hello SKU cui corrente versione toodelete desiderato e fare clic su hello **eliminare** pulsante.
5. Passare toohello **pubblica** scheda hello portale di pubblicazione. Fare clic su **richiesta approvazione tooPUSH tooPRODUCTION** toorepublish hello offerta in Marketplace hello.
6. Dopo l'offerta di hello Ottiene ripubblicare hello Marketplace, hello versione corrente di hello SKU elencato viene eliminato dal hello Marketplace e hello portale di Azure. Hello SKU viene quindi eseguito il rollback tooits di versione precedente.

## <a name="revert-hello-listing-price-tooproduction-values"></a>Ripristinare l'elenco di valori dei prezzi tooproduction hello
toorevert hello listato tooproduction dei valori dei prezzi, seguire questi passaggi:

1. Accedi toohello [pubblicazione portale](https://publish.windowsazure.com).
2. Passare toohello **macchine virtuali** scheda e selezionare l'offerta.
3. Dal menu hello hello sinistra, fare clic su hello **prezzi** scheda.
4. Selezionare un'area desiderata il cui prezzo tooreset.

    ![Aree dei prezzi](media/marketplace-publishing-vm-image-post-publishing/img08-04.png)
5. Per gli SKU con un modello di fatturazione orario, reimpostare i prezzi hello per tutti i core hello come se fossero nell'ambiente di produzione per un'area selezionata hello. Per gli SKU con un modello di fatturazione BYOL, rendere hello SKU disponibile nell'area di hello, selezionando la casella di controllo hello per hello SKU hello **EXTERNALLY-LICENSED (BYOL) SKU disponibilità** sezione.

    ![Modelli di prezzi](media/marketplace-publishing-vm-image-post-publishing/img08-05.png)
6. Fare clic su **AUTOPRICE OTHER MARKETS BASED ON PRICES IN UNITED STATE** (IMPOSTA AUTOMATICAMENTE I PREZZI PER GLI ALTRI MERCATI IN BASE A QUELLI DEGLI STATI UNITI).

   > [!NOTE]
   > etichetta del pulsante Hello potrebbe essere diverso a seconda area hello selezionato. Poiché è selezionato, Stati Uniti, il pulsante di hello è denominato **AUTOPRICE altri mercati basato su prezzi IN UNITED stati**.
   >
   >

    ![Impostare automaticamente i prezzi](media/marketplace-publishing-vm-image-post-publishing/img08-06.png)
7. Nella pagina 1 della procedura guidata Autoprice hello, scegliere mercato base hello e fare clic su hello **freccia** pulsante.

    ![Mercato di base](media/marketplace-publishing-vm-image-post-publishing/img08-07.png)
8. Nella pagina 2, scegliere i piani di servizio e metri (Core) e fare clic su hello **freccia** pulsante.

    ![Misuratori e piani di servizio](media/marketplace-publishing-vm-image-post-publishing/img08-08.png)
9. Nella pagina 3, fare clic su **attiva/disattiva tutte** tooselect tutte le aree. In alternativa, è possibile selezionare manualmente le caselle di controllo per aree specifiche. Fare clic su hello **freccia** pulsante.

    ![Scegliere i mercati](media/marketplace-publishing-vm-image-post-publishing/img08-09.png)
10. Nella pagina 4, esaminare i tassi di cambio hello e fare clic su **fine**. la procedura guidata Hello Reimposta hello prezzi in base tooyour selezioni.

11. In hello **prezzi** scheda, fare clic su **Visualizza riepilogo modifiche e**.
    Per **View Version** (Visualizza versione) selezionare **Draft** (Bozza) e per **Compare with** (Confronta con) selezionare **Production** (Produzione). Se viene visualizzata alcuna differenza di prezzo, hello prezzi ripristinato correttamente i valori di produzione toohello.

    ![Visualizza riepilogo e modifiche](media/marketplace-publishing-vm-image-post-publishing/img08-11.png)
12. Passare toohello **pubblica** scheda e fare clic su **tooSTAGING PUSH**. Per istruzioni dettagliate sulla verifica l'offerta in hello ambiente di gestione temporanea, vedere [testare l'offerta VM per hello Marketplace](marketplace-publishing-vm-image-test-in-staging.md).
13. Dopo aver testato l'offerta in gestione temporanea, andare toohello **pubblica** scheda hello portale di pubblicazione. Fare clic su **richiesta approvazione tooPUSH tooPRODUCTION** toorepublish l'offerta in Marketplace hello.

## <a name="revert-hello-billing-model-tooproduction-values"></a>Ripristinare hello tooproduction valori del modello di fatturazione
toorevert hello fatturazione tooproduction valori del modello, seguire questi passaggi:

1. Accedi toohello [pubblicazione portale](https://publish.windowsazure.com).

2. Passare toohello **macchine virtuali** scheda e selezionare l'offerta.
3. Dal menu hello hello sinistra, fare clic su hello **SKU** scheda.
4. Fare clic su hello **modifica** modello di fatturazione hello toorevert pulsante. Nella finestra di hello visualizzata, selezionare o deselezionare hello **fatturazione e la gestione delle licenze viene eseguita esternamente da Azure (noto anche come portare il propria licenza)** casella di controllo.

    ![Modificare la fatturazione](media/marketplace-publishing-vm-image-post-publishing/img09-04.png)
5. Seguire i passaggi di hello in "Hello Revert Elenca i valori dei prezzi tooproduction" in questo articolo.
6. Passare toohello **pubblica** scheda e fare clic su **tooSTAGING PUSH**. Per istruzioni dettagliate sulla verifica l'offerta in hello ambiente di gestione temporanea, vedere [testare l'offerta VM per hello Marketplace](marketplace-publishing-vm-image-test-in-staging.md).
7. Dopo aver testato l'offerta in gestione temporanea, andare toohello **pubblica** scheda hello portale di pubblicazione. Fare clic su **richiesta approvazione tooPUSH tooPRODUCTION** toorepublish l'offerta in Marketplace hello.

## <a name="revert-hello-visibility-setting-of-a-listed-sku-toohello-production-value"></a>Ripristinare hello impostazione di visibilità di un valore di produzione toohello SKU elencato
impostazione di visibilità hello toorevert di un valore di produzione toohello SKU elencato, seguire questi passaggi:

1. Accedi toohello [pubblicazione portale](https://publish.windowsazure.com).

2. Passare toohello **macchine virtuali** scheda e selezionare l'offerta.
3. Dal menu hello hello sinistra, fare clic su hello **SKU** scheda.
4. Selezionare lo SKU e ripristinare l'impostazione di visibilità hello del valore di produzione di SKU toohello hello.

    ![Visibilità](media/marketplace-publishing-vm-image-post-publishing/img10-04.png)
5. Dopo aver con modifiche hello, fare clic su **richiesta approvazione tooPUSH tooPRODUCTION** toorepublish l'offerta in Marketplace hello.

## <a name="see-also"></a>Vedere anche
* [Guida introduttiva: Pubblicare un toohello offerta Azure Marketplace](marketplace-publishing-getting-started.md)
* [Informazioni sui report sui proventi di Azure Marketplace](marketplace-publishing-report-payout.md)
* [Visualizzare e modificare il Cloud Solution Provider "Incentivi rivenditore" in Azure Marketplace](marketplace-publishing-csp-incentive.md)
* [Risolvere i problemi comuni di pubblicazione nel Marketplace hello](marketplace-publishing-support-common-issues.md)
* [Ottenere supporto come editore](marketplace-publishing-get-publisher-support.md)
* [Sviluppare l'immagine di una macchina virtuale in locale per Azure Marketplace](marketplace-publishing-vm-image-creation-on-premise.md)
* [Creare una macchina virtuale in esecuzione Windows nel portale di anteprima di Azure hello](../virtual-machines/virtual-machines-windows-hero-tutorial.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)

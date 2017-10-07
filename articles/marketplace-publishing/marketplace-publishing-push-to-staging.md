---
title: aaaPrepare e testare l'offerta per la distribuzione toohello Azure Marketplace | Documenti Microsoft
description: Istruzioni dettagliate sulla fornisce contenuti di marketing, la configurazione dei prezzi e il test l'offerta prima di distribuire toohello Azure Marketplace.
services: marketplace-publishing
documentationcenter: 
author: HannibalSII
manager: hascipio
editor: 
ms.assetid: 3ccd2448-895b-477e-adf6-ab655a21d2fa
ms.service: marketplace
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: Azure
ms.workload: na
ms.date: 08/17/2016
ms.author: hascipio
ms.openlocfilehash: 04f142c2dc894716c187751736549586c24a9d01
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="complete-hello-offer-creation-with-marketing-content"></a>Creazione con contenuti di marketing di offrire hello completo
In questo passaggio del processo di pubblicazione hello, sarà necessario tooprovide determinati marketing contenuto e informazioni dettagliate sull'offerta e/o SKU in hello Azure Marketplace. Una descrizione del prodotto, il logo della società, i piani di prezzo, dettagli dei piani e altri toopush necessarie informazioni, ad esempio, si fornirà l'offerta e/o toostaging SKU. Queste informazioni vengono utilizzate come contenuto di marketing hello portale di Azure. Si inizierà a questo processo in hello [portale pubblicazione][link-pubportal].

## <a name="step-1-provide-marketplace-marketing-content"></a>Passaggio 1: Fornire contenuti di marketing di Marketplace
**Inglese è hello predefinito e supportato solo linguaggio.** Verificare che tutte le informazioni fornite nei campi hello sono in inglese. Tutte le informazioni possono essere modificate in qualsiasi momento premendo toostaging.

1. Passare toohello pubblicazione portale [https://publish.windowsazure.com](https://publish.windowsazure.com).
2. Scegliere dal menu a sinistra, hello hello **Marketing** scheda.
3. Nel pannello principale hello, fare clic su hello **inglese (Stati Uniti)** pulsante.
   
   > [!IMPORTANT]
   > Tutti i campi devono avere voci, incluse le immagini di hello, per è toobe toopush in grado di toostaging.
   > 
   > 

### <a name="details-and-plans"></a>Dettagli e piani
1. Immettere il titolo di offerta hello (massimo 50 caratteri), offrono riepilogo (massimo 100 caratteri), offrono un riepilogo lungo (massimo 256 caratteri), offrono una descrizione (massimo 1300 caratteri), i logo in hello **dettagli** scheda
2. Immettere piano titolo (massimo 50 caratteri), il riepilogo del piano (massimo 100 caratteri), pianificare la descrizione (massimo 2000 caratteri) in hello **piani** scheda.
   
   > [!NOTE]
   > È possibile utilizzare hello seguito HTML tag tooformat hello riepilogo, riepilogo lunghe e descrizione dell'offerta hello e piani. Hello consentiti tag HTML sono h1, h2, h3, h4, h5, p, ol, ul, li, un [destinazione | href] complessa, em, b, si.
   > 
   > 
3. Non immettere testi duplicati nell'offerta e nella descrizione del piano.
4. Non immettere testi duplicati nel titolo del piano e nel riepilogo lungo dell'offerta.
5. Non immettere testi duplicati nel titolo del piano e nel riepilogo dell'offerta.
6. Non immettere titoli di piano identici per un'offerta con più piani.
7. Caricare le immagini di hello necessarie specifiche (hello portale di pubblicazione) in formato PNG, uno per ogni dimensione.
8. Verificare che i logo hello indicazioni hello Azure Marketplace logo riportata di seguito.
   
   ![disegno](media/marketplace-publishing-push-to-staging/pubportal-marketingcontent-details-02.png)

**Linee guida per il Logo di Azure Marketplace**

Tutti i logo hello caricati nel portale di pubblicazione hello eseguire hello sotto le linee guida seguenti:

* Hello progettazione di Azure dispone di una tavolozza dei colori semplice. Mantenere il numero di hello database primario e secondario colori sul logo bassa.
* colori del tema Hello di hello portale di Azure sono bianchi e neri. Pertanto evitare di utilizzare i colori come colore di sfondo hello di loghi. Utilizzare alcuni colore che renderebbe i logo classificarli hello portale di Azure. Si consiglia di usare colori primari semplici. **Se si utilizza sfondo trasparente, assicurarsi che tale hello logo, testo non sono bianchi o neri o blu.**
* Non utilizzare uno sfondo sfumato sul logo hello.
* Evitare di inserire testo, anche l'azienda o il nome dell'organizzazione, sul logo hello. Hello aspetto del logo deve essere 'semplice' ed evitare le sfumature.
* logo di Hello non possono essere ridimensionato.
* Il formato del logo piccolo deve essere di 40 X 40 pixel
* Il formato del logo medio deve essere 90 X 90 pixel
* Il formato del logo grande deve essere di 115 X 115 pixel
* Il formato del logo largo deve essere di 255 X 115 pixel
* Il formato del logo alto deve essere di 815 X 290 pixel

> [!NOTE]
> logo Hero Hello è facoltativo. server di pubblicazione Hello possibile scegliere di non tooupload un logo Hero. Icona di hero hello tuttavia una volta caricato non può essere eliminato da hello portale di pubblicazione. In quel momento, partner hello deve seguire le istruzioni di Azure Marketplace hello per le icone Hero.
> 
> 

  ![disegno](media/marketplace-publishing-push-to-staging/pubportal-marketingcontent-details-03.png)

**Ulteriori linee guida per l'icona del logo Hero hello (facoltativo)**

* logo Hero Hello è facoltativo. server di pubblicazione Hello possibile scegliere di non tooupload un logo Hero. **Icona di hero hello tuttavia una volta caricato non può essere eliminato da hello portale di pubblicazione. In quel momento, partner hello deve seguire le istruzioni di hello Azure Marketplace per le icone Hero offerta hello else non saranno tooproduction approvati.**
* Hello nome visualizzato editore, titolo e hello offrono riepilogo lungo vengono visualizzati nel colore bianco piano. Pertanto è consigliabile evitare di mantenere qualsiasi colore chiaro in background hello di hello Hero icona. Lo sfondo nero, bianco o trasparente non è ammesso per le icone del logo alto.
* nome visualizzato di publisher Hello, titolo, offerta hello riepilogo lunghe e hello pulsante Crea piano sono incorporati a livello di codice all'interno di hello logo Hero dopo offerta hello passa elencato. Pertanto non è necessario immettere il testo durante la progettazione dei logo Hero hello. Lasciare spazio vuoto in hello destra poiché hello testo (ad esempio nome visualizzato editore, titolo di piano, offerta hello riepilogo lunghe) verrà inclusa a livello di codice da Microsoft lì. spazio vuoto di Hello per testo hello deve essere 415 x 100 su hello destra (e viene applicato un offset da 370px da sinistra hello).
  
  ![disegno](media/marketplace-publishing-push-to-staging/pubportal-herobanner.png)

### <a name="links"></a>Collegamenti
In hello **collegamenti** nella barra sinistra hello, immettere tutti i collegamenti con informazioni che possono aiutare i clienti. Immettere un nome e un URL per ogni collegamento.

![disegno](media/marketplace-publishing-push-to-staging/pubportal-marketingcontent-link-01.png)

### <a name="sample-images-optional"></a>Immagini di esempio (facoltative)
> [!NOTE]
> L’inclusione di un'immagine di esempio è un passaggio facoltativo.
> Anche se è possibile caricare più immagini di esempio in hello portale di pubblicazione, solo un'immagine (selezionata in modo casuale dal sistema hello) viene visualizzata nel portale di Azure hello. Per questo motivo si consiglia di caricare al massimo un'immagine di esempio.
> 
> 

In hello **immagini di esempio** scheda nel menu di sinistra hello, caricare una nuova immagine, fare clic su **caricare una nuova immagine**. Se si dispone di un'immagine esistente e si desidera tooreplace, fare clic su **Sostituisci immagine**.

![disegno](media/marketplace-publishing-push-to-staging/pubportal-marketingcontent-sampleimg-01.png)

### <a name="legal"></a>Note legali
In hello **legali** scheda, fornire un collegamento tooyour criteri o condizioni di utilizzo. Immettere o incollare i termini di hello in hello grandi **condizioni per l'utilizzo** casella. limite di caratteri Hello per legali hello d'uso è 1.000.000 caratteri.

![disegno](media/marketplace-publishing-push-to-staging/pubportal-marketingcontent-legal-01.png)

**Nota:** per le offerte di macchina virtuale, una volta un'offerta/SKU viene gestita nel portale di Azure, hello non è possibile modificare i campi di hello specificati di seguito:

* **Offer Identifier (Identificatore offerte):** [Portale di pubblicazione -> Macchine virtuali -> selezionare l'offerta -> scheda Immagini VM -> Offer Identifier (Identificatore offerte)]
* **SKU Identifier (Identificatore SKU):** [Portale di pubblicazione -> Macchine virtuali -> selezionare l'offerta -> scheda SKU -> Add a SKU (Aggiungi uno SKU)]
* **Publisher Namespace (Spazio dei nomi dell'entità di pubblicazione):** [Portale di pubblicazione -&gt; Macchine virtuali -&gt; scheda Procedura dettagliata -&gt; Tell Us About Your Company (Informazioni sull'azienda), disponibile nel Passaggio 2 "Registrazione dell'azienda" -&gt; Publisher Namespace (Spazio dei nomi dell'entità di pubblicazione) -&gt;Spazio dei nomi]

Per le offerte di macchina virtuale quando hello offerta/SKU è elencato in hello Azure Marketplace, è possibile modificare i campi di hello specificati di seguito:

* **Offer Identifier (Identificatore offerte):** [Portale di pubblicazione -&gt; Macchine virtuali -&gt; selezionare l'offerta -&gt; Immagini VM -&gt; Offer Identifier (Identificatore offerte)]
* **SKU Identifier (Identificatore SKU):** [Portale di pubblicazione -&gt; Macchine virtuali -&gt; selezionare l'offerta -&gt; scheda SKU -&gt; Add a SKU (Aggiungi uno SKU)]
* **Publisher Namespace (Spazio dei nomi dell'entità di pubblicazione):** [Portale di pubblicazione -&gt; Macchine virtuali -&gt; scheda Procedura dettagliata -&gt; Tell Us About Your Company (Informazioni sull'azienda), disponibile nel Passaggio 2 "Registrazione -&gt; Publisher Namespace (Spazio dei nomi dell'entità di pubblicazione) -&gt; Spazio dei nomi]
* **Porte:** [Portale di pubblicazione -&gt; Macchine virtuali -&gt; selezionare l'offerta -&gt; scheda Immagini VM -&gt; Open Ports (Porte aperte)]
* **Modifica dei prezzi degli SKU elencati**
* **Modifica del modello di fatturazione degli SKU elencati**
* **Rimozione delle aree di fatturazione degli SKU elencati**
* **Numero di SKU(s) elencati del disco dati in continua evoluzione hello**

## <a name="step-2-set-your-prices"></a>Passaggio 2: Impostare i prezzi
### <a name="pricing-models"></a>Modelli di prezzi
| Modello di prezzi | Descrizione |
| --- | --- |
| Base |Tariffa mensile fissa al momento dell'acquisto, ad esempio $10/mese. |
| Consumo (noto come uso o misuratore) |Pagare per ogni utilizzo, che è definito dall'autore hello dell'offerta di hello. Non è possibile definire eccedenza per postazione, per ogni utente e così via, perché non esiste alcun concetto di una frazione di un utente o proration toodo funzionalità. L'utilizzo è segnalato dal partner hello su base oraria. Il cliente paga in hello del ciclo di fatturazione mensile, come parte anteriore tooup anziché come piani mensili. |
| Versione di prova gratuita |Il cliente può utilizzare il servizio gratuitamente per un periodo limitato e quindi pagare le tariffe normali in seguito. |
| Livello gratuito |Il piano è sempre gratuito. |
| Migrazione (nota come conversione o aggiornamento/downgrade) del piano |Concetto di un utente lo spostamento da loro piano tooanother accettabile piano corrente; definito da partner. |

**Modelli di prezzi disponibili per tipo di offerta**

> [!IMPORTANT]
> La disponibilità di determinati modelli di prezzi variano in base al tipo di offerta. Vedere la tabella hello seguente.
> 
> 

|  | Solo Base | Solo Consumo | Base + Consumo |
| --- | --- | --- | --- |
| Immagine di macchina virtuale |No |Sì |No |
| Servizio per gli sviluppatori |Sì |Sì |Sì |

### <a name="21-set-your-vm-prices"></a>2.1. Impostare i prezzi della VM
Attualmente le macchine virtuali, può essere seguito hello **3 tipi di modelli di fatturazione:**

* **Ogni ora:** vengono addebitate in base ai clienti in base all'ora in base alle tariffe di hello impostati dal server di pubblicazione hello dimensioni delle macchine Virtuali di hello. In caso di **fatturazione oraria** modello di hello SKU, prezzo totale hello sarà somma hello del costo di software hello addebitato hello server di pubblicazione e hello costi dell'infrastruttura addebitato da Microsoft. Il costo totale sarà cliente toohello visualizzato come un prezzo di ogni orario e mensile quando si sta considerando l'acquisto hello (vedere hello schermata riportata di seguito). **Server di pubblicazione riceve l'80% del costo di software hello addebito in base a essi.** Di conseguenza assicurarsi calcolo hello conseguenza prima di impostare i prezzi per le SKU.
  
    ![disegno](media/marketplace-publishing-push-to-staging/img2.1-01.png)
* **Versione di valutazione gratuita:** si tratta di un'altra versione del modello oraria hello. Qui cliente hello non vengono addebitate costi di software per hello primi 30 days(Free) dopo la distribuzione hello macchina virtuale. Dopo aver 30days sono ottenere addebitati su base oraria in base alle tariffe di hello impostare dai server di pubblicazione hello nel modello di oraria hello.
* **Bring-Your-proprietari-licenza (BYOL):** editori hello gestire hello le licenze di software hello in esecuzione su hello VM.

**Importante:** una volta hello offerta/SKU è elencato nella hello Azure Marketplace, è possibile modificare i campi hello specificati di seguito.

* **Modifica dei prezzi degli SKU elencati**
* **Modifica del modello di fatturazione degli SKU elencati**
* **Rimozione delle aree di fatturazione degli SKU elencati**
* **Numero di SKU(s) elencati del disco dati in continua evoluzione hello**
* **Offer Identifier (Identificatore offerte):** [Portale di pubblicazione -&gt; Macchine virtuali -&gt; selezionare l'offerta -&gt; Immagini VM -&gt; Offer Identifier (Identificatore offerte)]
* **SKU Identifier (Identificatore SKU):** [Portale di pubblicazione -&gt; Macchine virtuali -&gt; selezionare l'offerta -&gt; scheda SKU -&gt; Add a SKU (Aggiungi uno SKU)]
* **Publisher Namespace (Spazio dei nomi dell'entità di pubblicazione):** [Portale di pubblicazione -> Macchine virtuali -> scheda Procedura dettagliata -> Tell Us About Your Company (Informazioni sull'azienda), disponibile nel Passaggio 2 "Registrazione -> Publisher Namespace (Spazio dei nomi dell'entità di pubblicazione) -> Spazio dei nomi]
* **Porte:** [Portale di pubblicazione -&gt; Macchine virtuali -&gt; selezionare l'offerta -&gt; scheda Immagini VM -&gt; Open Ports (Porte aperte)]

### <a name="sell-to-countries-of-hello-sku"></a>"Vendere-a" paesi di hello SKU
È necessario toocarefully considerare dove si rende la SKU disponibile. Alcuni paesi sono classificati come "a rimessa Microsoft" e altri come "a rimessa ISV".

* In paesi "Rimessi Microsoft", Microsoft raccoglie le imposte dai clienti e paga imposte (mandati) toohello government.
* In paesi "ISV rimettere", sono responsabili per la raccolta di clienti di imposte e pagamento imposte toohello government partner. Se si sceglie toosell in paesi "ISV rimettere", è necessario disporre di hello funzionalità toocalculate e pagare le imposte in paesi hello selezionati.

> [!NOTE]
> Lo SKU non sarà disponibile in paesi hello a meno che non si imposta il piano tariffario in hello [pubblicazione portale](https://publish.windowsazure.com). Materiale sussidiario tooget set hello prezzi di ogni ora e SKU BYOL è indicato di seguito.
> 
> 

### <a name="211-how-toosetup-hourly-pricing-model-for-a-sku"></a>2.1.1 come toosetup modello ai costi orari per una SKU
Eseguire le operazioni di hello specificati di seguito toosetup modello ai costi orari per una SKU:

1. Account di accesso toohello [pubblicazione portale](https://publish.windowsazure.com).
2. Passare toohello **macchine VIRTUALI** e selezionare l'offerta.
3. Dal menu laterale a sinistra di hello, fare clic su hello **SKU** scheda.
4. Verificare che hello che SKU è contrassegnato come "Modello di fatturazione oraria". Se non, fare clic su hello **modifica** modello di fatturazione hello toorevert pulsante. Verrà visualizzata una finestra. Deselezionare la casella di controllo di hello ' fatturazione e la gestione delle licenze viene eseguita esternamente da Azure (noto anche come portare il propria licenza)' e salvare le modifiche di hello.
5. Se si desidera tooenable versione di valutazione gratuita per 30days di hello prima della distribuzione di SKU, quindi selezionare opzione hello "Un mese" per hello domanda "è una versione di valutazione gratuita?" In caso contrario, selezionare opzione hello "Nessuna versione di valutazione". Seguire ora i passaggi di hello riportati di seguito.
6. Dal menu laterale a sinistra di hello, fare clic su hello **prezzi** scheda.
7. Selezionare l'area di base.
   
   ![disegno](media/marketplace-publishing-push-to-staging/img2.1.1_07.png)
8. Impostare i prezzi hello per tutti i core. **È necessario fornire un prezzo per tutti i core hello di uno SKU anche se le SKU non è supportata.**
   
    ![disegno](media/marketplace-publishing-push-to-staging/img2.1.1_08.png)
9. Impostare manualmente i prezzi hello per hello altre aree o è possibile usare i prezzi hello AUTOPRICE guidata tooset hello di altre aree basati sull'area di base hello. toouse hello AUTOPRICE guidata fare clic sul pulsante hello **AUTOPRICE altri mercati basato su ON prezzi IN Stati Uniti.** **Nota:** hello etichetta può essere diverso a seconda area hello che è stato selezionato. Poiché durante la creazione di questo documento è stato selezionato Stati Uniti, pertanto pulsante hello viene etichettato come "Auto price altri mercati in base ai prezzi negli Stati Uniti" nella schermata di hello riportata di seguito.
   
   ![disegno](media/marketplace-publishing-push-to-staging/img2.1.1_09.png)
10. Creazione guidata di prezzo di Hello automatica verrà aperto. prima pagina Hello Visualizza selezione hello di mercato di base. Verificare la sezione e spostare la pagina successiva toohello facendo clic sul pulsante "->" hello.
    
    ![disegno](media/marketplace-publishing-push-to-staging/img2.1.1_10.png)
11. Opzione per la selezione di piani e core hello verrà visualizzato nella pagina hello 2. Selezionare i piani di hello desiderato e fare clic su "->" pulsante. Fare clic su hello **attiva/disattiva tutte** tooselect pulsante tutti hello **piani di servizio** e **metri** o è possibile verificare manualmente hello caselle di controllo. **È necessario fornire un prezzo per tutti i core hello di uno SKU anche se le SKU non è supportata.** Pertanto, verificare che siano selezionate tutte le dimensioni di base hello.
    
    ![disegno](media/marketplace-publishing-push-to-staging/img2.1.1_11.png)
12. Pagina 3 Visualizza hello mercati/aree geografiche. Fare clic su hello **attiva/disattiva tutte** pulsante tooselect tutte le aree o le caselle di hello per area di controllo manualmente. Fare clic su hello "->" pagina successiva di pulsante toomove toohello. **Nota:** i paesi in cui Microsoft riscuote e versa le imposte sono contrassegnati da un simbolo che raffigura una casa. Per ulteriori informazioni, vedere toohello sezione "Vendere-a" paesi di hello SKU di questa pagina.
    
    ![disegno](media/marketplace-publishing-push-to-staging/img2.1.1_12.png)
13. Pagina 4 Visualizza hello i tassi di cambio. Fare clic su hello completare i passaggi di hello toocomplete pulsante.

### <a name="212-how-toosetup-byol-pricing-model-for-a-sku"></a>2.1.2 come modello di determinazione dei prezzi BYOL toosetup per uno SKU
Eseguire le operazioni di hello specificati di seguito piano tariffario BYOL toosetup per una SKU:

1. Account di accesso toohello [pubblicazione portale](https://publish.windowsazure.com).
2. Passare toohello **macchine VIRTUALI** e selezionare l'offerta.
3. Dal menu laterale a sinistra di hello, fare clic su hello **SKU** scheda.
4. Verificare che hello che SKU è contrassegnato come "Bring your own license SKU". In caso contrario, quindi fare clic su hello toorevert pulsante Modifica di hello modello di fatturazione. Verrà visualizzata una finestra. Controllare la casella di controllo di hello ' fatturazione e la gestione delle licenze viene eseguita esternamente da Azure (noto anche come portare il propria licenza)' e salvare le modifiche di hello.
   
   ![disegno](media/marketplace-publishing-push-to-staging/img2.1.2_04.png)
5. Dal menu laterale a sinistra di hello, fare clic su hello **prezzi** scheda.
6. Selezionare l'area di base e verificare hello SKU disponibile nell'area di hello selezionando la casella di controllo hello contro hello SKU nella sezione hello disponibilità SKU EXTERNALLY-LICENSED (BYOL) (vedere hello schermata riportata di seguito).
   
   ![disegno](media/marketplace-publishing-push-to-staging/img2.1.2_06.png)
7. Rendere hello SKU disponibile in hello altre regioni manualmente o è possibile utilizzare Creazione guidata AUTOPRICE hello a questo scopo. Vedere troppo toohello punti &#9; #13 (che descrive l'utilizzo di hello della procedura guidata AUTOPRICE hello) nella sezione hello **"2.1.1 come toosetup modello ai costi orari per una SKU"** di questa pagina.

### <a name="22-set-your-developer-service-prices"></a>2.2. Impostare i prezzi del servizio di sviluppatore
Piani possono essere qualsiasi combinazione di base + consumo, in base è prezzo mensile hello ed eccedenza è il prezzo di pagamento in base all'utilizzo hello. (Vedere di seguito per ulteriori dettagli).

**Esempio:** offerta di servizio per sviluppatori di Contoso

| Pianificazione | Prezzo | Include | Percorso di migrazione |
| --- | --- | --- | --- |
| Gratuito |$0/mese |Funzionalità di base |Eseguire la migrazione tooany altro piano |
| Bronze |$10/mese |Funzionalità di base e una quota pari a 1.000 della funzionalità X. |Può eseguire la migrazione tooBronze Plus, argento e oro piani |
| Bronze Plus |Periodo di prova gratuita: $0/mese + $0/contatore01 |Funzionalità di base e una quota di 10.000 funzionalità X.  Una volta utilizzato quota funzionalità X, il cliente hello pagare per ogni utilizzo tramite meter01. |Eseguire la migrazione tooSilver segni più e Gold piani |
| Bronze Plus |Periodo di pagamento (noto come versione di prova gratuita scaduta): $10/mese + $0,05/misuratore01 |Funzionalità di base e una quota di 10.000 funzionalità X.  Una volta utilizzato quota funzionalità X, il cliente hello pagare per ogni utilizzo tramite meter01. |Eseguire la migrazione tooSilver segni più e Gold piani |
| Silver |$0,15/contatore01 |Hello cliente può pagare per ogni utilizzo tramite meter01, ovvero per funzionalità X. |Può eseguire la migrazione tooBronze e piani oro |
| Silver Plus |$20/mese + $ 0,15/contatore01 + $ 0,01/contatore02 |Funzionalità di base e una quota di 10.000 della funzionalità X e 100 della funzionalità Y.  Una volta utilizzato quota funzionalità X hello, cliente hello pagare per ogni utilizzo tramite meter01.  Una volta utilizzato quota funzionalità Y hello, cliente hello pagare per ogni utilizzo tramite meter02. |Eseguire la migrazione tooBronze segni più e Gold piani |
| Gold |$1,000/mese |Quota di 10.000 funzionalità X, 1.000 funzionalità Y e un numero illimitato di funzionalità Z. |Può eseguire la migrazione di piani tooall ad eccezione del fatto libero |

## <a name="step-3-provide-support-information"></a>Passaggio 3: Fornire informazioni di supporto
i dettagli di contatto Hello permettono di eseguire solo le comunicazioni interne tra il partner di hello e Microsoft. l'URL di supporto Hello sarà clienti finali toohello disponibili.

1. Passare toohello **supporto** titolo sul lato sinistro di portale di pubblicazione hello hello.
2. Immettere le informazioni nella sezione **Contatto tecnico**.
3. Immettere le informazioni nella sezione **Supporto tecnico**. Se si è scelto di fornire supporto solo tramite posta elettronica, immettere un numero di telefono fittizio. Al suo posto verrà utilizzato l'indirizzo di posta elettronica specificato.
4. Immettere l'URL di supporto hello.

## <a name="step-4-choose-azure-marketplace-categories"></a>Passaggio 4: Scegliere le categorie di Azure Marketplace
Hello **categorie** scheda fornisce una matrice delle selezioni. L'offerta può rientrare in questa ed è possibile selezionare le categorie di toofive.

## <a name="how-your-marketing-will-appear"></a>Visualizzazione del marketing
Di seguito è una visualizzazione dettagliata dell'utilizzo di offerta hello marketing informazioni su hello [sito Web di Azure Marketplace](https://azure.microsoft.com/marketplace/) e hello [portale di Azure](https://portal.azure.com).

### <a name="azure-marketplace-website"></a>Sito Web di Azure Marketplace
![disegno](media/marketplace-publishing-push-to-staging/acom-catalog-01.png)

![disegno](media/marketplace-publishing-push-to-staging/acom-catalog-02.png)

*Elenco delle offerte nel sito Web di Azure Marketplace hello*

![disegno](media/marketplace-publishing-push-to-staging/acom-listing-details-01.png)

*Dettagli nel sito Web di Azure Marketplace hello descrizione dell'offerta*

![disegno](media/marketplace-publishing-push-to-staging/acom-listing-details-02.png)

*Dettagli prezzi nel sito Web di Azure Marketplace hello descrizione dell'offerta*

### <a name="azure-portal"></a>Portale di Azure
![disegno](media/marketplace-publishing-push-to-staging/azureportal-galleryblade-01.png)

*Elenco di offerte di hello portale di Azure*

![disegno](media/marketplace-publishing-push-to-staging/azureportal-galleryblade-02.png)

*Dettagli dell'offerta descrizione in hello portale di Azure*

## <a name="next-steps"></a>Passaggi successivi
Ora che il contenuto del Marketplace è caricato, è possibile passare al test dell'offerta nella gestione temporanea. Tuttavia, è necessario selezionare il tipo di offerta appropriato hello hello seguente elenco, come passaggi variano in base al tipo di offerta.

* [Testare l'offerta VM nello staging](marketplace-publishing-vm-image-test-in-staging.md)
* [Test dell'offerta di modello di soluzione nello staging](marketplace-publishing-solution-template-test-in-staging.md)

## <a name="see-also"></a>Vedere anche
* [Guida introduttiva: come toopublish un toohello offerta Azure Marketplace](marketplace-publishing-getting-started.md)

[img-map-acom]:media/marketplace-publishing-push-to-staging/pubportal-mapping-acom.jpg
[img-map-portal]:media/marketplace-publishing-push-to-staging/pubportal-mapping-azure-portal.jpg
[img-map-link]:media/marketplace-publishing-push-to-staging/marketing-content-guide-links.jpg
[img-map-logo]:media/marketplace-publishing-push-to-staging/marketing-content-guide-logos.jpg
[img-map-title]:media/marketplace-publishing-push-to-staging/marketing-content-guide-publisher-offer.png

[link-pubportal]:https://publish.windowsazure.com
[link-push-to-production]:marketplace-publishing-push-to-production.md

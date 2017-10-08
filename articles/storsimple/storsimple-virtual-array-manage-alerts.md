---
title: aaaView e gestire gli avvisi di Microsoft Azure StorSimple Virtual Array | Documenti Microsoft
description: "Descrive le condizioni di avviso Array virtuale StorSimple e gravità e la modalità del servizio Avvisi toomanage toouse hello StorSimple Manager."
services: storsimple
documentationcenter: NA
author: alkohli
manager: timlt
editor: 
ms.assetid: 97ee25a1-0ec3-4883-9a0a-54b722598462
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 02/27/2017
ms.author: alkohli
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: b0fb5b1b9064f33df1d8fa7ace45f0d72b0a1622
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="use-storsimple-device-manager-toomanage-alerts-for-hello-storsimple-virtual-array"></a>Utilizzare Gestione periferiche di StorSimple toomanage avvisi per hello Array virtuale StorSimple

## <a name="overview"></a>Panoramica

funzionalità di avvisi Hello in hello del servizio di gestione di dispositivi StorSimple offre un modo per si tooreview e cancellare avvisi correlati tooStorSimple array virtuale in tempo reale. È possibile utilizzare gli avvisi di hello in hello **riepilogo servizio** toocentrally pannello monitorare problemi di integrità hello degli array virtuale StorSimple e hello soluzione globale di Microsoft Azure StorSimple.

Questa esercitazione viene descritto come tooconfigure le notifiche di avviso, le condizioni di avviso comuni, livelli di gravità di avviso e come tooview e tenere traccia degli avvisi. Sono inoltre incluse avviso riferimento rapido, tabelle, che consentono di tooquickly individuare un avviso specifico e rispondono in modo appropriato.

![Pagina degli avvisi](./media/storsimple-virtual-array-manage-alerts/alerts1.png)

## <a name="configure-alert-settings"></a>Configurare le impostazioni degli avvisi

È possibile scegliere se si desidera toobe una notifica tramite posta elettronica hello delle condizioni di avviso per ogni array virtuale di StorSimple. Inoltre, è possibile identificare altri destinatari delle notifiche di avviso immettendo i relativi indirizzi di posta elettronica in hello **destinatari di posta elettronica aggiuntivi** casella, separati da punti e virgola.

> [!NOTE]
> È possibile immettere un massimo di 20 indirizzi di posta elettronica per ogni array virtuale.


Dopo aver abilitato la notifica tramite posta elettronica per un array virtuale, i membri dell'elenco di notifica hello riceveranno un messaggio di posta elettronica ogni volta che si verifica un avviso critico. verranno inviati messaggi Hello da  *storsimple-alerts-noreply@mail.windowsazure.com*  e descriveranno la condizione dell'avviso hello. I destinatari possono fare clic su **Unsubscribe** tooremove stessi dall'elenco di notifica di posta elettronica hello.

#### <a name="tooenable-email-notification-for-alerts"></a>notifica tramite posta elettronica tooenable per gli avvisi

1. Passare tooyour dispositivo StorSimple Manager service e hello **Management** sezione, selezionare e fare clic su **dispositivi**. Hello l'elenco di dispositivi visualizzato, selezionare e fare clic sul dispositivo.
   
    ![Impostazione avvisi](./media/storsimple-virtual-array-manage-alerts/alerts2.png)
2. Verrà visualizzata hello **impostazioni** blade. In hello **le impostazioni del dispositivo** selezionare **generale**. Verrà visualizzata hello **impostazioni generali** blade.
   
    ![configurazione delle notifiche degli avvisi](./media/storsimple-virtual-array-manage-alerts/alerts4.png)
3. In hello **impostazioni generali** pannello andare troppo**Impostazioni avviso** sezione e impostare hello seguenti:
   
   1. In hello **Abilita notifica posta elettronica** campi, selezionare **Sì**.
   2. In hello **gli amministratori del servizio di posta elettronica** campi, selezionare **Sì** se si desidera l'amministratore del servizio toohave hello e tutti i coamministratori ricevano le notifiche di avviso hello.
   3. In hello **destinatari di posta elettronica aggiuntivi** immettere indirizzi di posta elettronica hello di tutti gli altri destinatari che riceveranno le notifiche di avviso hello. Immettere i nomi nel formato di hello  *someone@somewhere.com* . Utilizzare gli indirizzi di posta elettronica di un punto e virgola tooseparate hello. È possibile configurare un massimo di 20 indirizzi di posta elettronica per ogni dispositivo virtuale.
      
       ![configurazione delle notifiche degli avvisi](./media/storsimple-virtual-array-manage-alerts/alerts6.png)
   4. Fare clic su una notifica di posta elettronica di prova, toosend **invia posta elettronica di prova**. Hello del servizio di gestione di dispositivi StorSimple verrà visualizzati messaggi di stato durante l'inoltro di notifica di prova hello.
      
       ![Messaggio di posta elettronica di prova della notifica di avviso inviato](./media/storsimple-virtual-array-manage-alerts/alerts7.png)
      
      > [!NOTE]
      > Se test hello messaggio di notifica non inviare, il servizio di gestione di dispositivi StorSimple hello verrà visualizzato un messaggio appropriato. Fare clic su **OK**, attendere qualche minuto e riprovare toosend il messaggio di notifica di test.
      > 
      > 
   5. Nella parte inferiore di hello della pagina hello, fare clic su **salvare** toosave la configurazione. Alla richiesta di conferma fare clic su **Sì**.
      
      ![Messaggio di posta elettronica di prova della notifica di avviso inviato](./media/storsimple-virtual-array-manage-alerts/alerts10.png)

## <a name="common-alert-conditions"></a>Condizioni di avviso comuni

L'Array virtuale StorSimple genera avvisi in condizioni diverse tooa risposta. di seguito Hello sono tipi di condizioni di avviso più comuni di hello:

* **Problemi di connettività** : questi avvisi vengono generati in caso di difficoltà di trasferimento dei dati. Problemi di comunicazione possono verificarsi durante il trasferimento dei dati tooand da account di archiviazione di Azure hello o scadenza toolack di connettività tra i dispositivi virtuali hello e servizio di gestione di dispositivi StorSimple hello. Problemi di comunicazione sono alcuni dei più difficili toofix di hello poiché esistono molti punti di errore. Verificare sempre prima che la connettività di rete e accesso a Internet siano disponibili prima di proseguire toomore risoluzione avanzata dei problemi. Per informazioni sulle porte e le impostazioni del firewall, visitare troppo[requisiti di sistema StorSimple Virtual Array](storsimple-ova-system-requirements.md). Per informazioni sulla risoluzione dei problemi, andare troppo[risoluzione dei problemi con il cmdlet Test-Connection hello](storsimple-troubleshoot-deployment.md).
* **Problemi di prestazioni** : questi avvisi vengono generati quando le prestazioni del sistema non sono ottimali, ad esempio in presenza di un forte carico.

Inoltre, si potrebbe visualizzare toosecurity correlati gli avvisi, aggiornamenti o errori nel processo.

## <a name="alert-severity-levels"></a>Livelli di gravità dell'avviso

Gli avvisi hanno diversi livelli di gravità, a seconda di impatto hello hello situazione di avviso verrà e hello necessità di un avviso di toohello di risposta. livelli di gravità Hello sono:

* **Critico** : questo avviso è in condizione di tooa risposta che influisce sulle prestazioni del sistema hello. Azione è necessario tooensure che il servizio di StorSimple hello non è stato interrotto.
* **Avviso** : questa condizione potrebbe diventare critica se non viene risolta. È consigliabile esaminare la situazione hello e richiedere qualsiasi problema di hello tooclear azione richiesta.
* **Informazioni** : questo avviso contiene informazioni che possono essere utili per la verifica e la gestione del sistema.

## <a name="view-and-track-alerts"></a>Visualizzare e tenere traccia degli avvisi

Pannello riepilogo servizio di gestione di dispositivi StorSimple Hello fornisce un riepilogo rapido numero hello di avvisi su dispositivi virtuali, disposti in base al livello di gravità.

![Dashboard degli avvisi](./media/storsimple-virtual-array-manage-alerts/alerts14.png)

Fare clic su hello tooopen livello di gravità hello **avvisi** blade. i risultati di Hello includono solo gli avvisi di hello che soddisfano tale livello di gravità.

![Report avvisi con ambito di tipo tooalert](./media/storsimple-virtual-array-manage-alerts/alerts15.png)

Fare clic su un avviso in hello elenco tooget ulteriori dettagli per l'avviso hello, tra cui hello ora dell'ultimo avviso hello è stato segnalato, il numero di hello di occorrenze dell'avviso hello sul dispositivo hello e hello azione consigliata tooresolve hello avviso.

![Elenco degli avvisi e dettagli](./media/storsimple-virtual-array-manage-alerts/alerts16.png)

È possibile copiare i file di testo tooa hello dettagli dell'avviso se è necessario toosend hello informazioni tooMicrosoft supporto. Dopo aver seguito raccomandazione hello e risolto una condizione di avviso hello in locale, è necessario cancellare l'avviso hello dall'elenco di hello. Selezionare avviso hello hello elenco e quindi fare clic su **deselezionare**. tooclear più avvisi, selezionare ogni avviso, fare clic su qualsiasi colonna eccetto hello **avviso** colonna e quindi fare clic su **deselezionare** dopo aver selezionato tutti hello toobe avvisi deselezionata.

Quando fa clic su **deselezionare**, si disporrà di commenti di tooprovide hello opportunità su avviso hello e hello passaggi che tooresolve hello problema. 

![commenti degli avvisi](./media/storsimple-virtual-array-manage-alerts/alerts17.png)

Alcuni eventi vengono cancellati dal sistema hello se viene attivato un altro evento con nuove informazioni. 

## <a name="sort-and-review-alerts"></a>Ordinare e rivedere gli avvisi

Hello **avvisi** pannello è possibile visualizzare avvisi too250. Se è stato superato il numero di avvisi, non tutti gli avvisi verranno visualizzati nella visualizzazione predefinita hello. È possibile combinare hello toocustomize campi vengono visualizzati gli avvisi seguenti:

* **Stato**: è possibile visualizzare gli avvisi di tipo **Attivo** o **Cancellato**. Gli avvisi attivi vengono ancora attivati sul sistema, mentre gli avvisi cancellati sono stati cancellati manualmente da un amministratore o a livello di codice deselezionati, in quanto il sistema hello aggiornato condizione di avviso hello con nuove informazioni.
* **Gravità** : è possibile visualizzare gli avvisi di tutti i livelli di gravità (critico, avviso, informazioni) o solo di una determinata gravità, ad esempio solo gli avvisi critici.
* **Origine** : È possibile visualizzare gli avvisi da tutte le origini o limitare hello avvisi toothose che provengono dal servizio hello o uno o tutti hello dispositivi virtuali.
* **Intervallo di tempo** : specificando hello **da** e **a** date e time stamp, è possibile esaminare gli avvisi durante il periodo di tempo che si è interessati a hello.

## <a name="alerts-quick-reference"></a>Riferimento rapido degli avvisi

Hello le tabelle seguenti elenca alcuni degli avvisi di StorSimple hello che possono verificarsi, nonché consigli e informazioni aggiuntive in cui è disponibile. Gli avvisi di StorSimple Virtual Array rientrano in una delle seguenti categorie di hello:

* [Avvisi di connettività cloud](#cloud-connectivity-alerts)
* [Avvisi di configurazione](#configuration-alerts)
* [Avvisi di errore di processo](#job-failure-alerts)
* [Avvisi di prestazioni](#performance-alerts)
* [Avvisi di sicurezza](#security-alerts)
* [Avvisi di aggiornamento](#update-alerts)

### <a name="cloud-connectivity-alerts"></a>Avvisi di connettività cloud

| Testo dell'avviso | Evento | Ulteriori informazioni/Azioni consigliate |
|:--- |:--- |:--- |
| Dispositivo  *<device name>*  è toohello cloud non è connesso. |Hello denominato dispositivo non è possibile connettersi toohello cloud. |Impossibile connettersi toohello cloud. Questo potrebbe essere stato causato tooone seguenti hello:<ul><li>Potrebbe esserci un problema con le impostazioni di rete hello sul dispositivo.</li><li>Potrebbe esserci un problema con le credenziali dell'account di archiviazione hello.</li></ul>Per ulteriori informazioni sulla risoluzione dei problemi di connettività, visitare toohello [interfaccia utente web locale](storsimple-ova-web-ui-admin.md) del dispositivo hello. |

### <a name="configuration-alerts"></a>Avvisi di configurazione

| Testo dell'avviso | Evento | Ulteriori informazioni/Azioni consigliate |
|:--- |:--- |:--- |
| Configurazione del servizio virtuale locale non supportata. |Rallentamento delle prestazioni. |la configurazione corrente di Hello può comportare una riduzione delle prestazioni. Verificare che il server soddisfi i requisiti minimi delle configurazioni di hello. Per ulteriori informazioni, visitare troppo[StorSimple Virtual Array requisiti](storsimple-ova-system-requirements.md). |
| Lo spazio su disco di cui è stato eseguito il provisioning in <*nome dispositivo*> è quasi esaurito. |Avviso relativo allo spazio su disco. |Sta per esaurirsi lo spazio su disco con provisioning. toofree spazio, provare a spostare i carichi di lavoro tooanother volume o condivisione file o l'eliminazione dei dati. |

### <a name="job-failure-alerts"></a>Avvisi di errore di processo

| Testo dell'avviso | Evento | Ulteriori informazioni/Azioni consigliate |
|:--- |:--- |:--- |
| Non è stato possibile completare il backup di <*nome dispositivo*>. |Il processo di backup non è riuscito. |Non è stato possibile creare un backup. Considerare una delle seguenti hello:<ul><li>Problemi di connettività potrebbero impedire di operazione di backup hello completato. Assicurarsi che non siano presenti problemi di connettività. Per ulteriori informazioni sulla risoluzione dei problemi di connettività, visitare toohello [interfaccia utente web locale](storsimple-ova-web-ui-admin.md) per il dispositivo virtuale.</li><li>È stato raggiunto il limite di archiviazione disponibile hello. toofree spazio, prendere in considerazione l'eliminazione di tutti i backup che non sono più necessari.</li></ul> Risolvere i problemi di hello, cancellare hello avviso e ripetere l'operazione di hello. |
| Non è stato possibile completare la creazione del clone di <*nome dispositivo*>. |Il processo di clonazione non è riuscito. |Impossibile creare un clone. Considerare una delle seguenti hello:<ul><li>L'elenco di backup potrebbe non essere valido. Aggiornare tooverify elenco hello è ancora valido.</li><li>Problemi di connettività potrebbero impedire il completamento dell'operazione clone hello. Assicurarsi che non siano presenti problemi di connettività.</li><li>È stato raggiunto il limite di archiviazione disponibile hello. toofree spazio, prendere in considerazione l'eliminazione di tutti i backup che non sono più necessari.</li></ul>Risolvere i problemi di hello, cancellare hello avviso e ripetere l'operazione di hello. |

### <a name="performance-alerts"></a>Avvisi di prestazioni

| Testo dell'avviso | Evento | Ulteriori informazioni/Azioni consigliate |
|:--- |:--- |:--- |
| Si stanno verificando ritardi imprevisti nel trasferimento dei dati. |Trasferimento dati lento. |Quando si superano le destinazioni di scalabilità hello di un servizio di archiviazione, si verificano errori di limitazione delle richieste. il servizio di archiviazione Hello effettua questo tooensure che nessun client o tenant può usare servizio hello spese hello di altri utenti. Per ulteriori informazioni sulla risoluzione dei problemi di account di archiviazione Azure, visitare troppo[Monitor, diagnosticare e risolvere i problemi di archiviazione di Microsoft Azure](../storage/common/storage-monitoring-diagnosing-troubleshooting.md). |
| Lo spazio su disco riservato in locale in <*nome dispositivo*> è quasi esaurito. |Tempo di risposta lento. |10% di hello totale dimensioni provisioning per <*nome dispositivo*> è riservato in hello dispositivo locale e si sta esaurendo hello spazio riservato. carico di lavoro Hello <*nome dispositivo*> è la generazione di una maggiore frequenza di varianza o si potrebbe avere eseguita di recente una grande quantità di dati. Questo può comportare una riduzione delle prestazioni. Considerare una delle hello seguenti azioni tooresolve questo:<ul><li>Aumentare hello cloud del dispositivo toothis della larghezza di banda.</li><li>Ridurre o spostare i carichi di lavoro tooanother volume o condivisione.</li></ul> |

### <a name="security-alerts"></a>Avvisi di sicurezza

| Testo dell'avviso | Evento | Ulteriori informazioni/Azioni consigliate |
|:--- |:--- |:--- |
| La password per <*nome dispositivo*> scadrà tra <*numero*> giorni. |Avviso relativo alla password. |La password scadrà tra <numero> giorni. Provare a modificare la password. Per ulteriori informazioni, visitare troppo[password amministratore del dispositivo StorSimple Virtual Array hello modifica](storsimple-virtual-array-change-device-admin-password.md). |

### <a name="update-alerts"></a>Avvisi di aggiornamento

| Testo dell'avviso | Evento | Ulteriori informazioni/Azioni consigliate |
|:--- |:--- |:--- |
| Sono disponibili nuovi aggiornamenti per il dispositivo. |Aggiornamenti toohello Array virtuale StorSimple sono disponibili. |È possibile installare nuovi aggiornamenti da hello **manutenzione** pagina. |
| Non è stato possibile verificare la disponibilità di nuovi aggiornamenti in <*nome dispositivo*>. |Errore durante l'aggiornamento. |Errore durante l'installazione di nuovi aggiornamenti. È possibile installare manualmente gli aggiornamenti di hello. Se hello problema persiste, contattare [supporto Microsoft](storsimple-contact-microsoft-support.md). |

## <a name="next-steps"></a>Passaggi successivi

* [Informazioni su StorSimple Virtual Array hello](storsimple-ova-overview.md).


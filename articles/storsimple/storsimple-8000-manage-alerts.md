---
title: aaaView e gestire gli avvisi per il dispositivo StorSimple serie 8000 | Documenti Microsoft
description: "Descrive le condizioni di avviso StorSimple e gravità, come tooconfigure notifiche di avviso e modalità del servizio Avvisi toomanage toouse hello dispositivo StorSimple Manager."
services: storsimple
documentationcenter: NA
author: alkohli
manager: timlt
editor: 
ms.assetid: 
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 08/22/2017
ms.author: alkohli
ms.openlocfilehash: fdd1a911ceff542bc6bdeae877e1f0fc381bf27c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="use-hello-storsimple-device-manager-service-tooview-and-manage-storsimple-alerts"></a>Utilizzare tooview servizio di gestione di dispositivi StorSimple hello e gestire gli avvisi di StorSimple

## <a name="overview"></a>Panoramica

Hello **avvisi** pannello nel servizio di gestione di dispositivi StorSimple hello offre un modo per si tooreview e deselezionare gli avvisi relativi ai dispositivi StorSimple in tempo reale. Questo pannello, è possibile monitorare i problemi di integrità hello i dispositivi StorSimple in modo centralizzato e hello soluzione globale di Microsoft Azure StorSimple.

Questa esercitazione vengono descritti le condizioni di avviso comuni, i livelli di gravità dell'avviso e come tooconfigure notifiche di avviso. Sono inoltre incluse avviso riferimento rapido, tabelle, che consentono di tooquickly individuare un avviso specifico e rispondono in modo appropriato.

![Pagina degli avvisi](./media/storsimple-8000-manage-alerts/configure-alerts-email11.png)

## <a name="common-alert-conditions"></a>Condizioni di avviso comuni

Genera avvisi nel dispositivo StorSimple in condizioni diverse tooa risposta. di seguito Hello sono tipi di condizioni di avviso più comuni di hello:

* **Problemi hardware** – questi avvisi forniscono informazioni sull'integrità hello dell'hardware. Consentono di sapere se sono necessari aggiornamenti del firmware, se un'interfaccia di rete presenta problemi oppure se si è verificato un problema con una delle unità dati.
* **Problemi di connettività** : questi avvisi vengono generati in caso di difficoltà di trasferimento dei dati. Problemi di comunicazione possono verificarsi durante il trasferimento dei dati tooand da account di archiviazione di Azure hello o scadenza toolack di connettività tra i dispositivi hello e servizio di gestione di dispositivi StorSimple hello. Problemi di comunicazione sono alcuni dei più difficili toofix di hello poiché esistono molti punti di errore. Verificare sempre prima che la connettività di rete e accesso a Internet siano disponibili prima di proseguire toomore risoluzione avanzata dei problemi. Per informazioni sulla risoluzione dei problemi, andare troppo[risoluzione dei problemi con il cmdlet Test-Connection hello](storsimple-troubleshoot-deployment.md).
* **Problemi di prestazioni** : questi avvisi vengono generati quando le prestazioni del sistema non sono ottimali, ad esempio in presenza di un forte carico.

Inoltre, si potrebbe visualizzare toosecurity correlati gli avvisi, aggiornamenti o errori nel processo.

## <a name="alert-severity-levels"></a>Livelli di gravità dell'avviso

Gli avvisi hanno diversi livelli di gravità, a seconda di impatto hello hello situazione di avviso verrà e hello necessità di un avviso di toohello di risposta. livelli di gravità Hello sono:

* **Critico** : questo avviso è in condizione di tooa risposta che influisce sulle prestazioni del sistema hello. Azione è necessario tooensure che il servizio di StorSimple hello non è stato interrotto.
* **Avviso** : questa condizione potrebbe diventare critica se non viene risolta. È consigliabile esaminare la situazione hello e richiedere qualsiasi problema di hello tooclear azione richiesta.
* **Informazioni** : questo avviso contiene informazioni che possono essere utili per la verifica e la gestione del sistema.

## <a name="configure-alert-settings"></a>Configurare le impostazioni degli avvisi

È possibile scegliere se si desidera ricevere una notifica tramite posta elettronica delle condizioni di avviso per ognuno dei dispositivi StorSimple toobe. Inoltre, è possibile identificare altri destinatari delle notifiche di avviso immettendo i relativi indirizzi di posta elettronica in hello **altri destinatari di posta elettronica** casella, separati da punti e virgola.

> [!NOTE]
> È possibile immettere un massimo di 20 indirizzi di posta elettronica per ogni dispositivo.

Dopo aver abilitato la notifica tramite posta elettronica per un dispositivo, i membri dell'elenco di notifica hello riceveranno un messaggio di posta elettronica ogni volta che si verifica un avviso critico. verranno inviati messaggi Hello da  *storsimple-alerts-noreply@mail.windowsazure.com*  e descriveranno la condizione dell'avviso hello. I destinatari possono fare clic su **Unsubscribe** tooremove stessi dall'elenco di notifica di posta elettronica hello.

#### <a name="tooenable-email-notification-of-alerts-for-a-device"></a>notifica di posta elettronica tooenable degli avvisi per un dispositivo
1. Passare il servizio di gestione di dispositivi StorSimple tooyour. Hello l'elenco di dispositivi, selezionare e fare clic su dispositivo di hello che si desidera tooconfigure.
2. Andare troppo**impostazioni** > **generale** per dispositivo hello.

   ![Pannello Avvisi](./media/storsimple-8000-manage-alerts/configure-alerts-email2.png)
   
2. In hello **impostazioni generali** pannello andare troppo**Impostazioni avviso** e impostare hello seguenti:
   
   1. In hello **invia notifica e-mail** campi, selezionare **Sì**.
   2. In hello **gli amministratori del servizio di posta elettronica** campi, selezionare **Sì** amministratore del servizio toohave hello e tutti i coamministratori ricevano notifiche di avviso hello.
   3. In hello **altri destinatari di posta elettronica** immettere indirizzi di posta elettronica hello di tutti gli altri destinatari che riceveranno le notifiche di avviso hello. Immettere i nomi nel formato di hello  *someone@somewhere.com* . Utilizzare gli indirizzi di posta elettronica di un punto e virgola tooseparate hello. È possibile configurare un massimo di 20 indirizzi di posta elettronica per ogni dispositivo. 
      
3. Fare clic su una notifica di posta elettronica di prova, toosend **invia posta elettronica di prova**. Hello del servizio di gestione di dispositivi StorSimple verrà visualizzati messaggi di stato durante l'inoltro di notifica di prova hello.

    ![Impostazione avviso](./media/storsimple-8000-manage-alerts/configure-alerts-email3.png)

4. Viene visualizzata una notifica quando viene inviato tramite posta elettronica di prova hello. 
   
    ![Messaggio di posta elettronica di prova della notifica di avviso inviato](./media/storsimple-8000-manage-alerts/configure-alerts-email4.png)
   
   > [!NOTE]
   > Se test hello messaggio di notifica non inviare, il servizio di gestione di dispositivi StorSimple hello verrà visualizzato un messaggio di errore appropriato. Attendere qualche minuto e riprovare toosend il messaggio di notifica di test. 

5. Dopo aver completato la configurazione hello, fare clic su **salvare**. Alla richiesta di conferma fare clic su **Sì**.

     ![Messaggio di posta elettronica di prova della notifica di avviso inviato](./media/storsimple-8000-manage-alerts/configure-alerts-email5.png)

## <a name="view-and-track-alerts"></a>Visualizzare e tenere traccia degli avvisi

Pannello riepilogo servizio di gestione di dispositivi StorSimple Hello fornisce un riepilogo rapido numero hello di avvisi per i dispositivi, disposti in base al livello di gravità.

![Dashboard degli avvisi](./media/storsimple-8000-manage-alerts/device-summary4.png)

Fare clic sul livello di gravità hello apre hello **avvisi** blade. i risultati di Hello includono solo gli avvisi di hello che soddisfano tale livello di gravità.

Facendo clic su un avviso nell'elenco di hello fornisce dettagli aggiuntivi per l'avviso hello, tra cui hello ultimo tempo hello avviso è stato segnalato, hello numero di occorrenze dell'avviso hello sul dispositivo hello e hello è consigliabile avviso hello tooresolve di azione. Se si tratta di un avviso di hardware, verrà anche identificato componente hardware hello.

![Esempio di avviso hardware](./media/storsimple-8000-manage-alerts/configure-alerts-email14.png)

È possibile copiare i file di testo tooa hello dettagli dell'avviso se è necessario toosend hello informazioni tooMicrosoft supporto. Dopo aver seguito raccomandazione hello e risolto una condizione di avviso hello in locale, è necessario cancellare l'avviso hello dal dispositivo hello selezionando avviso hello in hello **avvisi** blade e facendo clic su **deselezionare**. tooclear più avvisi, selezionare ogni avviso, fare clic su qualsiasi colonna eccetto hello **avviso** colonna e quindi fare clic su **deselezionare** dopo aver selezionato tutti hello toobe avvisi deselezionata. Si noti che alcuni avvisi vengono automaticamente cancellati quando hello problema viene risolto oppure quando il sistema hello Aggiorna avviso hello con nuove informazioni.

Quando fa clic su **deselezionare**, si disporrà di commenti di tooprovide hello opportunità su avviso hello e hello passaggi che tooresolve hello problema. Alcuni eventi vengono cancellati dal sistema hello se viene attivato un altro evento con nuove informazioni. In tal caso, si noterà che segue messaggio hello.

![Cancellare il messaggio di avviso](./media/storsimple-manage-alerts/admin_alerts_system_clear.png)

## <a name="sort-and-review-alerts"></a>Ordinare e rivedere gli avvisi

Può risultare più efficiente toorun report avvisi in modo che è possibile esaminare e cancellarli in gruppo. Inoltre, hello **avvisi** pannello è possibile visualizzare avvisi too250. Se è stato superato il numero di avvisi, non tutti gli avvisi verranno visualizzati nella visualizzazione predefinita hello. È possibile combinare hello toocustomize campi vengono visualizzati gli avvisi seguenti:

* **Stato**: è possibile visualizzare gli avvisi di tipo **Attivo** o **Cancellato**. Gli avvisi attivi vengono ancora attivati sul sistema, mentre gli avvisi cancellati sono stati cancellati manualmente da un amministratore o a livello di codice deselezionati, in quanto il sistema hello aggiornato condizione di avviso hello con nuove informazioni.
* **Gravità** : è possibile visualizzare gli avvisi di tutti i livelli di gravità (critico, avviso, informazioni) o solo di una determinata gravità, ad esempio solo gli avvisi critici.
* **Origine** : È possibile visualizzare gli avvisi da tutte le origini o limitare hello avvisi toothose che provengono dal servizio hello o uno o tutti i dispositivi di hello.
* **Intervallo di tempo** : specificando hello **da** e **a** date e time stamp, è possibile esaminare gli avvisi durante il periodo di tempo che si è interessati a hello.

![Elenco degli avvisi](./media/storsimple-8000-manage-alerts/configure-alerts-email11.png)

## <a name="alerts-quick-reference"></a>Riferimento rapido degli avvisi

Hello le tabelle seguenti elenca alcuni degli avvisi di Microsoft Azure StorSimple hello che possono verificarsi, nonché consigli e informazioni aggiuntive in cui è disponibile. Avvisi del dispositivo StorSimple rientrano in una delle seguenti categorie di hello:

* [Avvisi di connettività cloud](#cloud-connectivity-alerts)
* [Avvisi di cluster](#cluster-alerts)
* [Avvisi di ripristino di emergenza](#disaster-recovery-alerts)
* [Avvisi di hardware](#hardware-alerts)
* [Avvisi di errore di processo](#job-failure-alerts)
* [Avvisi sul volume aggiunto in locale](#locally-pinned-volume-alerts)
* [Avvisi di rete](#networking-alerts)
* [Avvisi di prestazioni](#performance-alerts)
* [Avvisi di sicurezza](#security-alerts)
* [Avvisi del pacchetto per il supporto](#support-package-alerts)

### <a name="cloud-connectivity-alerts"></a>Avvisi di connettività cloud

| Testo dell'avviso | Evento | Ulteriori informazioni/Azioni consigliate |
|:--- |:--- |:--- |
| Connettività troppo <*nome delle credenziali cloud*> non può essere stabilita. |Impossibile connettersi toohello account di archiviazione. |Potrebbe essersi verificato un problema di connettività con il dispositivo. Eseguire hello `Test-HcsmConnection` cmdlet hello interfaccia di Windows PowerShell per StorSimple nel tooidentify dispositivo e risolvere il problema di hello. Se hello impostazioni sono corrette, potrebbe essere problema hello con credenziali hello hello dell'account di archiviazione per cui è stato generato l'avviso di hello. In questo caso, utilizzare hello `Test-HcsStorageAccountCredential` toodetermine cmdlet se sono presenti problemi che possono essere risolti.<ul><li>Verificare le impostazioni di rete.</li><li>Verificare le credenziali dell'account di archiviazione.</li></ul> |
| Abbiamo ancora ricevuto un heartbeat dal dispositivo per hello ultima <*numero*> minuti. |Impossibile connettersi toodevice. |Potrebbe essersi verificato un problema di connettività con il dispositivo. Utilizzare hello `Test-HcsmConnection` cmdlet hello interfaccia di Windows PowerShell per StorSimple nel tooidentify dispositivo e risolvere il problema di hello o contattare l'amministratore di rete. |

### <a name="storsimple-behavior-when-cloud-connectivity-fails"></a>StorSimple comportamento quando si verifica un errore di connettività cloud

Cosa accade se si verifica un errore di connettività cloud per il dispositivo StorSimple in esecuzione nell'ambiente di produzione?

Se la connettività di cloud non riesce nel dispositivo StorSimple di produzione, quindi a seconda dello stato di hello del dispositivo, seguente hello può verificarsi:

* **Per dati locali di hello sul dispositivo**: per un certo tempo, non sarà presente alcuna interruzione del servizio e di lettura saranno ancora toobe servita. Tuttavia, come numero hello di IOs in attesa aumenta e supera un limite, è possibile avviare toofail hello letture.

    A seconda della quantità di hello di dati nel dispositivo, scritture hello continueranno toooccur per hello prima alcune ore dopo l'interruzione hello nella connettività cloud hello. scritture Hello verranno avviati infine toofail se l'interruzione della connettività cloud hello per diverse ore e quindi rallentano. (È archiviazione temporanea nel dispositivo hello per dati toobe inserito toohello cloud. Quest'area viene scaricata quando vengono inviati dati hello. Se si verifica un errore di connettività, dati in questa area di archiviazione non saranno inseriti toohello cloud e IO non riuscirà.)
* **Per i dati nel cloud hello hello**: per la maggior parte degli errori di connettività cloud, viene restituito un errore. Una volta ripristinata la connettività di hello, IOs hello vengono ripresi senza utente hello con volume hello toobring online. In rari casi, l'intervento dell'utente potrebbe essere toobring obbligatorio hello indietro volume online dal portale di Azure hello.
* **Per gli snapshot cloud in corso**: hello operazione viene ritentata più volte all'interno di 4 e 5 ore e se non viene ripristinata la connettività di hello, gli snapshot cloud hello avrà esito negativo.

### <a name="cluster-alerts"></a>Avvisi di cluster

| Testo dell'avviso | Evento | Ulteriori informazioni/Azioni consigliate |
|:--- |:--- |:--- |
| Failover del dispositivo troppo <*nome dispositivo*>. |Il dispositivo è in modalità di manutenzione. |Failover del dispositivo a causa di tooentering o in fase di chiusura in modalità manutenzione. Si tratta di un comportamento normale e non è richiesto alcun intervento. Dopo avere confermato ricezione dell'avviso, cancellarlo dalla pagina avvisi hello. |
| Failover del dispositivo troppo <*nome dispositivo*>. |Il software o il firmware del dispositivo è stato appena aggiornato. |Si è verificato un failover del cluster a causa di tooan update. Si tratta di un comportamento normale e non è richiesto alcun intervento. Dopo avere confermato ricezione dell'avviso, cancellarlo dalla pagina avvisi hello. |
| Failover del dispositivo troppo <*nome dispositivo*>. |Il controller è stato arrestato o riavviato. |Failover del dispositivo perché il controller attivo hello è stato arrestato o riavviato da un amministratore. Non è richiesto alcun intervento. Dopo avere confermato ricezione dell'avviso, cancellarlo dalla pagina avvisi hello. |
| Failover del dispositivo troppo <*nome dispositivo*>. |Failover pianificato. |Verificare che si tratta di un failover pianificato. Dopo avere eseguito l'azione appropriata, cancellare questo avviso dalla pagina degli avvisi di hello. |
| Failover del dispositivo troppo <*nome dispositivo*>. |Failover non pianificato. |StorSimple è progettato Ripristina tooautomatically failover non pianificato. Se viene visualizzato un numero elevato di questi avvisi, contattare il supporto tecnico Microsoft. |
| Failover del dispositivo troppo <*nome dispositivo*>. |Causa diversa/sconosciuta. |Se viene visualizzato un numero elevato di questi avvisi, contattare il supporto tecnico Microsoft. Dopo aver risolto il problema di hello, cancellare questo avviso dalla pagina avvisi hello. |
| Un servizio critico del dispositivo è segnalato come non riuscito. |Errore del servizio percorso dati. |Contattare il supporto tecnico Microsoft per ottenere assistenza. |
| Lo stato dell'indirizzo IP virtuale per l'interfaccia di rete <*DATA #*> è segnalato come non riuscito. |Causa diversa/sconosciuta. |Le condizioni temporanee possono talvolta provocare questi avvisi. In caso di hello, quindi questo avviso verrà cancellato automaticamente dopo alcuni minuti. Se hello problema persiste, contattare il supporto Microsoft. |
| Lo stato dell'indirizzo IP virtuale per l'interfaccia di rete <*DATA #*> è segnalato come non riuscito. |Nome dell'interfaccia: <*dati #*> indirizzo IP <IP address> non può essere portata online perché è stato rilevato un indirizzo IP duplicato sulla rete hello. |Verificare che l'indirizzo IP duplicato hello viene rimosso dalla rete hello o riconfigurare l'interfaccia hello con un indirizzo IP diverso. |

### <a name="disaster-recovery-alerts"></a>Avvisi di ripristino di emergenza

| Testo dell'avviso | Evento | Ulteriori informazioni/Azioni consigliate |
|:--- |:--- |:--- |
| Ripristino non è possibile ripristinare tutte le impostazioni di hello per questo servizio. I dati di configurazione del dispositivo si trovano in uno stato incoerente per alcuni dispositivi. |Incoerenza dei dati rilevata dopo il ripristino di emergenza. |I dati crittografati nel servizio hello non sono sincronizzati con quello sul dispositivo hello. Autorizzare il dispositivo hello <*nome dispositivo*> dal processo di sincronizzazione di gestione di dispositivi StorSimple toostart hello. Hello utilizzo interfaccia di Windows PowerShell per StorSimple toorun hello `Restore-HcsmEncryptedServiceData` sul dispositivo <*nome dispositivo*> cmdlet, fornendo vecchia password hello come un input toothis profilo di sicurezza hello toorestore cmdlet. Eseguire quindi hello `Invoke-HcsmServiceDataEncryptionKeyChange` cmdlet tooupdate hello chiave DEK del servizio. Dopo avere eseguito l'azione appropriata, cancellare questo avviso dalla pagina degli avvisi di hello. |

### <a name="hardware-alerts"></a>Avvisi di hardware

| Testo dell'avviso | Evento | Ulteriori informazioni/Azioni consigliate |
|:--- |:--- |:--- |
| Lo stato del componente hardware <*ID componente*> è segnalato come <*stato*>. | |Le condizioni temporanee possono talvolta provocare questi avvisi. In tal caso, l'avviso viene cancellato automaticamente dopo un periodo di tempo. Se hello problema persiste, contattare il supporto Microsoft. |
| Malfunzionamento del controller passivo. |il controller passivo (secondario) Hello non funziona. |Il dispositivo è operativo, ma uno dei controller non funziona correttamente. Provare a riavviare il controller. Se il problema di hello non viene risolto, contattare il supporto Microsoft. |

### <a name="job-failure-alerts"></a>Avvisi di errore di processo

| Testo dell'avviso | Evento | Ulteriori informazioni/Azioni consigliate |
|:--- |:--- |:--- |
| Backup di <*ID gruppo di volumi di origine*> non riuscito. |Il processo di backup non è riuscito. |Problemi di connettività potrebbero impedire di operazione di backup hello completato. Se non siano presenti problemi di connettività, si potrebbe sia stato raggiunto il numero massimo di hello di backup. Eliminare tutti i backup che non sono più necessari e ripetere l'operazione di hello. Dopo avere eseguito l'azione appropriata, cancellare questo avviso dalla pagina degli avvisi di hello. |
| Creazione del clone di <*gli ID elemento di backup di origine*> troppo <*numeri di serie volume di destinazione*> non è riuscita. |Il processo di clonazione non è riuscito. |Aggiornamento hello elenco di backup tooverify che hello backup è ancora valido. Se il backup di hello è valido, è possibile che problemi di connettività cloud impediscano il completamento dell'operazione clone hello. Se non siano presenti problemi di connettività, si potrebbe sia stato raggiunto il limite di archiviazione hello. Eliminare tutti i backup che non sono più necessari e ripetere l'operazione di hello. Dopo aver acquisito problema di hello tooresolve azione appropriata, cancellare questo avviso dalla pagina avvisi hello. |
| Ripristino di <*ID elementi di backup di origine*> non riuscito. |Il processo di ripristino non è riuscito. |Aggiornamento hello elenco di backup tooverify che hello backup è ancora valido. Se il backup di hello è valido, è possibile che problemi di connettività cloud impediscano il completamento dell'operazione ripristino hello. Se non siano presenti problemi di connettività, si potrebbe sia stato raggiunto il limite di archiviazione hello. Eliminare tutti i backup che non sono più necessari e ripetere l'operazione di hello. Dopo aver acquisito problema di hello tooresolve azione appropriata, cancellare questo avviso dalla pagina avvisi hello. |

### <a name="locally-pinned-volume-alerts"></a>Avvisi sul volume aggiunto in locale

| Testo dell'avviso | Evento | Ulteriori informazioni/Azioni consigliate |
|:--- |:--- |:--- |
| Creazione del volume locale <*nome volume*> non riuscita. |il processo di creazione di Hello volume non è riuscita. <*Toohello corrispondente messaggio di errore non riuscita*>. |Problemi di connettività potrebbero impedire hello spazio operazione di creazione completato. Volumi aggiunti in locale sono stati sottoposti a thick provisioning e il processo di hello di creazione dello spazio implica la distribuzione cloud toohello volumi a livelli. Se non si verificano problemi di connettività, potrebbe essere esaurito lo spazio locale hello sul dispositivo hello. Determinare se esiste spazio disponibile nel dispositivo hello prima di riprovare questa operazione. |
| Espansione del volume locale <*nome volume*> non riuscita. |processo di modifica di Hello volume non è riuscita a causa troppo <*toohello corrispondente messaggio di errore non riuscita*>. |Problemi di connettività potrebbero impedire di operazione di espansione del volume hello corretto completamento. Volumi aggiunti in locale sono stati sottoposti a thick provisioning e il processo di hello di espansione hello di spazio esistente implica la distribuzione cloud toohello volumi a livelli. Se non si verificano problemi di connettività, potrebbe essere esaurito lo spazio locale hello sul dispositivo hello. Determinare se esiste spazio disponibile nel dispositivo hello prima di riprovare questa operazione. |
| Conversione del volume <*nome volume*> non riuscita. |Hello conversione processo tooconvert hello volume dal tipo tootiered aggiunti in locale non è riuscita. |Impossibile completare la conversione del volume hello da tootiered tipo aggiunto in locale. Verificare che non siano presenti problemi di connettività impedire hello operazione completata. Risoluzione dei problemi di connettività problemi andare troppo[risoluzione dei problemi con il cmdlet Test-HcsmConnection hello](storsimple-troubleshoot-deployment.md#troubleshoot-with-the-test-hcsmconnection-cmdlet).<br>il volume aggiunto in locale Hello originale ora è stato contrassegnato come un volume a livelli poiché alcuni dati hello dal volume aggiunto in locale hello è distribuito toohello cloud durante la conversione di hello. volume a livelli risultante Hello ancora occupa spazio locale nel dispositivo hello che non può essere recuperata per i volumi locali future.<br>Risolvere eventuali problemi di connettività, cancellare l'avviso hello e convertire questo volume toohello indietro originale volume aggiunto in locale tipo tooensure tutti i dati di hello viene resa disponibile localmente. |
| Conversione del volume <*nome volume*> non riuscita. |Hello conversione processo tooconvert hello volume dal tipo a livelli toolocally aggiunto non è riuscita. |Impossibile completare la conversione del volume hello dal tipo a livelli toolocally bloccato. Verificare che non siano presenti problemi di connettività impedire hello operazione completata. Risoluzione dei problemi di connettività problemi andare troppo[risoluzione dei problemi con il cmdlet Test-HcsmConnection hello](storsimple-troubleshoot-deployment.md#troubleshoot-with-the-test-hcsmconnection-cmdlet).<br>volume a più livelli con Hello originale ora contrassegnato come volume aggiunto in locale come parte del processo di conversione hello continua toohave dati che risiedono nel cloud hello durante hello stati sottoposti a thick provisioning spazio sul dispositivo hello per questo volume non può essere recuperata per future locale volumi.<br>Risolvere eventuali problemi di connettività, avviso crittografato hello e convertire questo volume toohello indietro originale volume a livelli tipo tooensure locale stati sottoposti a thick provisioning nel dispositivo hello è espressamente. |
| Consumo di spazio locale quasi esaurito per gli snapshot locali di <*nome gruppo di volumi*> |Gli snapshot locali per i criteri di backup hello appena potrebbero esaurire lo spazio ed essere invalidato tooavoid errori di scrittura dell'host. |Snapshot locali frequenti insieme a un'elevata varianza dei dati nei volumi di hello associata a questo gruppo di criteri di backup causano spazio locale nel toobe dispositivo hello consumati velocemente. Eliminare gli snapshot locali che non sono più necessari. Inoltre, aggiornare le pianificazioni degli snapshot locali per tootake questo criterio di backup meno snapshot locali frequenti e verificare che gli snapshot cloud sono eseguiti regolarmente. Se non vengono intraprese queste azioni, potrebbe esaurirsi presto spazio locale per questi snapshot e sistema hello verrà automaticamente eliminati tooensure che scrive host continuare toobe elaborato correttamente. |
| Snapshot locali per <*nome gruppo di volumi*> invalidati. |gli snapshot locali per Hello <*nome gruppo di volumi*> sono stati invalidati ed eliminati quindi perché che sono stati supera lo spazio locale hello sul dispositivo hello. |Questo problema non si ripresenti in futuro, hello tooensure verificare pianificazioni degli snapshot locali hello per questo criterio di backup ed eliminare tutti gli snapshot locali che non sono più necessari. Snapshot locali frequenti insieme a un'elevata varianza dei dati nei volumi di hello associata a questo gruppo di criteri di backup potrebbe spazio locale nel toobe dispositivo hello consumati velocemente. |
| Ripristino di <*ID elementi di backup di origine*> non riuscito. |il processo di ripristino di Hello non è riuscita. |Se hanno aggiunto in locale o una combinazione di volumi localmente bloccati e a più livelli nel criterio di backup, l'aggiornamento hello elenco di backup tooverify che hello backup sia ancora valida. Se il backup di hello è valido, è possibile che problemi di connettività cloud impediscano il completamento dell'operazione ripristino hello. Hello localmente aggiunti volumi che sono stati ripristinati come parte di questo gruppo di snapshot non dispongono di tutto del dispositivo toohello scaricato dati e, se si dispone di una combinazione di volumi aggiunti in locale e a più livelli di questo gruppo di snapshot, non saranno sincronizzati tra loro. toosuccessfully completare hello operazione di ripristino, portare i volumi di hello in questo gruppo host hello e ripetere l'operazione di ripristino hello. Si noti che i dati di volume toohello modifiche che sono stati eseguiti durante hello processo di ripristino andrà perso. |

### <a name="networking-alerts"></a>Avvisi di rete

| Testo dell'avviso | Evento | Ulteriori informazioni/Azioni consigliate |
|:--- |:--- |:--- |
| Impossibile avviare i servizi StorSimple. |Errore di percorso dati |Se hello problema persiste, contattare il supporto Microsoft. |
| Indirizzo IP duplicato rilevato per "Data0". | |sistema di Hello ha rilevato un conflitto per l'indirizzo IP '10.0.0.1'. Hello 'Data0' risorsa di rete nel dispositivo hello  *<device1>*  è offline. Assicurarsi che questo indirizzo IP non venga usato da nessuna altra entità nella rete. problemi di rete tootroubleshoot, andare troppo[risoluzione dei problemi con il cmdlet Get-NetAdapter hello](storsimple-troubleshoot-deployment.md#troubleshoot-with-the-get-netadapter-cmdlet). Per risolvere il problema, contattare l'amministratore di rete. Se hello problema persiste, contattare il supporto Microsoft. |
| L'indirizzo IPv4 (o IPv6) per "Data0" è offline. | |risorse di rete Hello 'Data0' con indirizzo IP '10.0.0.1'. prefisso di lunghezza '22' sul dispositivo hello  *<device1>*  è offline. Verificare che toowhich porte del commutatore hello questa interfaccia è connessa siano operative. problemi di rete tootroubleshoot, andare troppo[risoluzione dei problemi con il cmdlet Get-NetAdapter hello](storsimple-troubleshoot-deployment.md#troubleshoot-with-the-get-netadapter-cmdlet). |
| Impossibile connettere il servizio di autenticazione toohello. |Errore di percorso dati |Hello URLthat utilizzato tooauthenticate non è raggiungibile. Verificare che le regole del firewall includono modelli di hello URL specificati per il dispositivo StorSimple hello. Per ulteriori informazioni sui pattern di URL nel portale di Azure, visitare toohttps://aka.ms/ss-8000-network-reqs. Se utilizza Cloud di Azure per enti pubblici, scegliere i modelli di URL toohello in https://aka.ms/ss8000-gov-network-reqs.|

### <a name="performance-alerts"></a>Avvisi di prestazioni

| Testo dell'avviso | Evento | Ulteriori informazioni/Azioni consigliate |
|:--- |:--- |:--- |
| Hello carico del dispositivo ha superato <*soglia*>. |Tempi di risposta più lenti del previsto. |Il dispositivo segnala un carico di input/output eccessivo Ciò potrebbe causare il lavoro toonot dispositivo nonché come dovrebbe. Esaminare i carichi di lavoro di hello collegati toohello dispositivo e determinare se sono presenti che possono essere spostati tooanother dispositivo o che non sono più necessari.| Impossibile avviare i servizi StorSimple. |Errore di percorso dati |Se hello problema persiste, contattare il supporto Microsoft. |e lo stato corrente di hello, andare troppo[utilizzare hello toomonitor servizio di gestione di dispositivi StorSimple del dispositivo](storsimple-monitor-device.md) |

### <a name="security-alerts"></a>Avvisi di sicurezza

| Testo dell'avviso | Evento | Ulteriori informazioni/Azioni consigliate |
|:--- |:--- |:--- |
| La sessione del supporto tecnico Microsoft è stata avviata. |Sessione di supporto per l'accesso di terze parti. |Verificare che l'accesso sia autorizzato. Dopo avere eseguito l'azione appropriata, cancellare questo avviso dalla pagina degli avvisi di hello. |
| La password per <*elemento*> scadrà tra <*periodo di tempo*>. |La scadenza della password è prossima. |Modificare la password prima della scadenza. |
| Informazioni sulla configurazione di sicurezza mancanti per <*ID elemento*>. | |Hello volumi associati a questo contenitore del volume non può essere utilizzato tooreplicate la configurazione di StorSimple. tooensure che i dati sono archiviati in modo sicuro, è consigliabile eliminare il contenitore di volumi hello e tutti i volumi associati al contenitore del volume hello. Dopo avere eseguito l'azione appropriata, cancellare questo avviso dalla pagina degli avvisi di hello. |
| <*numero*&gt; di tentativi di accesso non riusciti per &lt;*ID elemento*&gt;. |Più tentativi di accesso non riusciti. |Il dispositivo potrebbe essere sotto attacco o un utente autorizzato stia tentando tooconnect con una password errata.<ul><li>Contattare gli utenti autorizzati e verificare che questi tentativi provengano da un'origine legittima. Se si continua toosee un numero elevato di tentativi di accesso, provare a disabilitare la gestione remota e contattare l'amministratore di rete. Dopo avere eseguito l'azione appropriata, cancellare questo avviso dalla pagina degli avvisi di hello.</li><li>Controllare che le istanze di gestione Snapshot siano configurate con la password corretta hello. Dopo avere eseguito l'azione appropriata, cancellare questo avviso dalla pagina degli avvisi di hello.</li></ul>Per ulteriori informazioni, visitare troppo[modificare una password del dispositivo scaduta](storsimple-snapshot-manager-manage-devices.md#change-an-expired-device-password). |
| Uno o più errori durante la modifica chiave DEK del servizio hello. | |Si sono verificati errori durante la modifica chiave DEK hello. Dopo avere risolto le condizioni di errore hello, eseguire hello `Invoke-HcsmServiceDataEncryptionKeyChange` cmdlet hello interfaccia di Windows PowerShell per StorSimple sul servizio hello tooupdate dispositivo. Se questo problema persiste, contattare il supporto tecnico Microsoft. Dopo aver risolto il problema di hello, cancellare questo avviso dalla pagina avvisi hello. |

### <a name="support-package-alerts"></a>Avvisi del pacchetto per il supporto

| Testo dell'avviso | Evento | Ulteriori informazioni/Azioni consigliate |
|:--- |:--- |:--- |
| Creazione del pacchetto per il supporto non riuscita. |StorSimple non è stato possibile generare il pacchetto di hello. |Ripetere l'operazione. Se hello problema persiste, contattare il supporto Microsoft. Dopo aver risolto il problema di hello, cancellare questo avviso dalla pagina avvisi hello. |

## <a name="next-steps"></a>Passaggi successivi

Altre informazioni su [Errori di StorSimple e risoluzione dei problemi relativi a un dispositivo operativo](storsimple-troubleshoot-operational-device.md).


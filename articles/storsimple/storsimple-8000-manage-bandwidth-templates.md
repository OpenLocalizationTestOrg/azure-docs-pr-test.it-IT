---
title: modelli di larghezza di banda aaaManage per StorSimple serie 8000 | Documenti Microsoft
description: Viene descritto come modelli di larghezza di banda StorSimple toomanage, che consentono di larghezza di banda toocontrol.
services: storsimple
documentationcenter: 
author: alkohli
manager: timlt
editor: 
ms.assetid: 
ms.service: storsimple
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 06/29/2017
ms.author: alkohli
ms.openlocfilehash: ebcd1824d7bb9e4c235194c04edbfe8001a3e794
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="use-hello-storsimple-device-manager-service-toomanage-storsimple-bandwidth-templates"></a>Utilizzare i modelli di larghezza di banda StorSimple di hello dispositivo StorSimple Manager servizio toomanage

## <a name="overview"></a>Panoramica

I modelli di larghezza di banda consentono di utilizzo della larghezza di banda di rete tooconfigure tra più pianificazioni di ore del giorno tootier hello dati hello cloud toohello di dispositivo StorSimple.

Utilizzando le pianificazioni relative alla limitazione larghezza di banda è possibile:

* Specificare le pianificazioni di larghezza di banda personalizzato a seconda di utilizzi di rete di hello del carico di lavoro.
* Centralizzare la gestione e riutilizzare le pianificazioni di hello tra più dispositivi in modo facile e uniforme.

> [!NOTE]
> Questa funzionalità è disponibile solo per i dispositivi StorSimple fisici (modelli 8100 e 8600) e non per i dispositivi appliance cloud StorSimple (modelli 8010 e 8020).


## <a name="hello-bandwidth-templates-blade"></a>Pannello di modelli di larghezza di banda Hello

Hello **modelli di larghezza di banda** pannello ha tutti i modelli di larghezza di banda hello per il servizio in un formato tabulare e contiene hello le seguenti informazioni:

* **Nome** : un modello di larghezza di banda toohello nome univoco assegnato al momento della creazione.
* **Pianificazione** : hello numero di pianificazioni contenute in un modello di larghezza di banda specificato.
* **Utilizzato da** : numero di volumi che usano i modelli di larghezza di banda hello hello.

È anche possibile trovare informazioni aggiuntive toohelp configurare i modelli di larghezza di banda in:

* [Domande e risposte sui modelli di larghezza di banda](#questions-and-answers-about-bandwidth-templates)
* [Procedure consigliate per i modelli di larghezza di banda](#best-practices-for-bandwidth-templates)

## <a name="add-a-bandwidth-template"></a>Aggiunta di un modello di larghezza di banda

Eseguire hello seguendo i passaggi toocreate un nuovo modello di larghezza di banda.

#### <a name="tooadd-a-bandwidth-template"></a>un modello di larghezza di banda tooadd

1. Il servizio di gestione di dispositivi StorSimple tooyour, quindi scegliere **modelli di larghezza di banda** e quindi fare clic su **+ il modello di larghezza di banda Aggiungi**.

    ![Fare clic su + Aggiungi modelli larghezza di banda](./media/storsimple-8000-manage-bandwidth-templates/addbwtemp1.png)

2. In hello **Aggiungi modello di larghezza di banda** pannello hello i passaggi seguenti:
   
    1. Specificare un nome univoco per il modello di larghezza di banda.
    2. Definire una pianificazione per la larghezza di banda. toocreate una pianificazione:
   
        1. Dall'elenco a discesa hello scegliere hello **giorni** di hello settimana hello pianificazione è configurata per. È possibile selezionare più giorni.        
        
        2. Immettere un'**Ora di inizio** nel formato _hh:mm_. Ciò avviene pianificazione hello avrà inizio.

        3. Immettere un'**Ora di fine** nel formato _hh:mm_. Ciò avviene pianificazione hello verrà interrotta.
      
           > [!NOTE]
           > Le pianificazioni sovrapposte non sono consentite. Se hello ora di inizio e fine producono una pianificazione sovrapposta, verrà visualizzato un effetto toothat messaggio di errore.

        4. Specificare hello **velocità larghezza di banda**. Si tratta di hello della larghezza di banda in megabit al secondo (Mbps) usato dal dispositivo StorSimple nelle operazioni che comportano cloud hello (caricamento e download). Specificare un numero compreso tra 1 e 1000 per questo campo.

            ![Definire una pianificazione per la larghezza di banda](./media/storsimple-8000-manage-bandwidth-templates/addbwtemp2.png)
         
            Ripetere hello sopra toodefine passaggi più pianificazioni per il modello di termine.

        5. Fare clic su **Aggiungi** toostart creazione di un modello di larghezza di banda. Hello modello creato viene aggiunto toohello elenco dei modelli di larghezza di banda.
      

## <a name="edit-a-bandwidth-template"></a>Modifica di un modello di larghezza di banda

Eseguire hello seguendo i passaggi tooedit un modello di larghezza di banda.

### <a name="tooedit-a-bandwidth-template"></a>un modello di larghezza di banda tooedit

1. Il servizio di gestione di dispositivi StorSimple tooyour, fare clic su **modelli di larghezza di banda**.
2. Nell'elenco di hello di modelli di larghezza di banda, selezionare il modello di hello desiderato toodelete. Fare clic e selezionare il menu di scelta rapida hello **eliminare**.
3. Alla richiesta di conferma fare clic su **Sì**. Si deve eliminare il modello di larghezza di banda hello. 
4. elenco di Hello dei modelli di larghezza di banda di eliminazione hello tooreflect verrà aggiornato.

> [!NOTE]
> È possibile salvare le modifiche se hello Modifica pianificazione si sovrappone a una pianificazione esistente nel modello di larghezza di banda hello che si desidera modificare.

## <a name="delete-a-bandwidth-template"></a>Eliminazione di un modello di larghezza di banda

Eseguire hello seguendo i passaggi toodelete un modello di larghezza di banda.

#### <a name="toodelete-a-bandwidth-template"></a>un modello di larghezza di banda toodelete

1. Il servizio di gestione di dispositivi StorSimple tooyour, fare clic su **modelli di larghezza di banda**.
2. Nell'elenco di hello di modelli di larghezza di banda, selezionare il modello di hello desiderato toodelete. Mouse e dal menu di scelta rapida hello, scegliere Elimina.
3. Alla richiesta di conferma fare clic su **Sì**. Si deve eliminare il modello di larghezza di banda hello.
4. elenco di Hello dei modelli di larghezza di banda di eliminazione hello tooreflect verrà aggiornato.

Se il modello di hello è utilizzato da uno o più volumi, non sarà possibile toodelete è. Verrà visualizzato un messaggio di errore che indica che il modello hello è in uso. Verrà visualizzata nella finestra di dialogo di messaggio di errore segnalare che tutti i modelli di toohello riferimenti hello devono essere rimosse.

È possibile eliminare tutti i modelli di toohello riferimenti hello accedendo hello **contenitori di volumi** pagina e la modifica di contenitori di volumi hello che usano il modello in modo che utilizzino un altro modello o utilizzare una larghezza di banda personalizzata o illimitata l'impostazione. Quando sono stati rimossi tutti i riferimenti di hello, è possibile eliminare il modello di hello.

## <a name="use-a-default-bandwidth-template"></a>Utilizzo di un modello di larghezza di banda predefinito

Un modello di larghezza di banda predefinito viene fornito e usato dai contenitori di volumi dai controlli di larghezza di banda tooenforce predefinito per l'accesso cloud hello. modello predefinito Hello funge anche da riferimento pronto per gli utenti che creare modelli personalizzati. Dettagli Hello del modello predefinito sono:

* **Nome** : notte e fine settimana senza limiti
* **Pianificazione** : una singola pianificazione da lunedì tooFriday che applica una velocità di larghezza di banda di 1 Mbps tra le 8.00 e l'ora del dispositivo 17: 00. larghezza di banda Hello è impostato tooUnlimited per il resto di hello della settimana hello.

modello predefinito Hello può essere modificato. uso di Hello del modello (incluse le versioni modificate) viene monitorato.

## <a name="create-an-all-day-bandwidth-template-that-starts-at-a-specified-time"></a>Creazione di un modello di larghezza di banda giornaliero che viene avviato a un determinato orario

Seguire questa toocreate procedure una pianificazione che inizia in corrispondenza di un'ora specificata e viene eseguito tutto il giorno. Nell'esempio hello pianificazione hello inizia alle 9.00 del mattino hello e viene eseguito finché hello 09: 00 mattino successivo. È importante toonote che hello di inizio e ora di fine per una determinata pianificazione deve essere contenute entrambe nella hello uguale a 24 ore pianificazione e non può estendersi su più giorni. Se è necessario tooset i modelli di larghezza di banda che si estendono su più giorni, è necessario toouse più pianificazioni (come illustrato nell'esempio hello).

#### <a name="toocreate-an-all-day-bandwidth-template"></a>un modello di larghezza di banda tutto il giorno toocreate

1. Creare una pianificazione che inizia alle 9.00 del mattino hello e viene eseguito a mezzanotte.
2. Aggiungere un'altra pianificazione. Configurare hello secondo pianificazione toorun da mezzanotte fino alle 9.00 mattino hello.
3. Salvare il modello di larghezza di banda hello.

pianificazione composta Hello verrà quindi avviare contemporaneamente scelta ed eseguire tutto il giorno.

## <a name="questions-and-answers-about-bandwidth-templates"></a>Domande e risposte sui modelli di larghezza di banda

**D**. Controlli toobandwidth cosa accade quando si è tra le pianificazioni di hello? ossia quando una pianificazione è terminata e un'altra non è ancora stata avviata?

**R**. In questi casi, non verranno utilizzati controlli relativi alla larghezza di banda. Ciò significa che il dispositivo hello può utilizzare larghezza di banda illimitata quando suddivisione in livelli toohello dati nel cloud.

**D**. È possibile modificare i modelli di larghezza di banda in un dispositivo offline?

**R**. Non sarà in grado di toomodify modelli di larghezza di banda in contenitori di volumi se il dispositivo corrispondente hello è offline.

**D**. È possibile modificare un modello di larghezza di banda associato a un contenitore di volumi quando i volumi di hello associato sono offline?

**R**. È possibile modificare un modello di larghezza di banda associato a un contenitore di volume, i cui volumi sono offline. Si noti che quando i volumi sono offline, dati non vengono suddivisi in livelli dal cloud di toohello dispositivo hello.

**D**. È possibile eliminare un modello predefinito?

**R**. Sebbene sia possibile eliminare un modello predefinito, non è una buona idea toodo così. utilizzo di Hello di un modello predefinito, incluse le versioni modificate, viene controllato. dati di rilevamento Hello viene analizzato e nel corso del tempo hello è usato tooimprove hello predefinito.

**D**. Come si determina che i modelli di larghezza di banda necessario toobe modificato

**R**. Uno dei simboli necessari modelli di larghezza di banda toomodify hello sono quando si avvia hello visualizzazione rete hello rallentare o riduzione più volte in un giorno. In questo caso, il monitoraggio rete di archiviazione e l'uso di hello esaminando i grafici delle prestazioni dei / o e velocità effettiva della rete di hello.

Dai dati di velocità effettiva di rete hello, identificare l'ora del giorno in hello e hello contenitori dei volumi in cui hello rete collo di bottiglia. Se ciò accade quando i dati vengono toohello a più livelli cloud (ottenere queste informazioni dalle prestazioni dei / o per tutti i contenitori di volumi per dispositivo toocloud), sarà necessario modelli di larghezza di banda hello toomodify associati ai contenitori del volume.

Dopo avere modificato hello modelli sono in uso, è necessario rete hello toomonitor nuovamente le latenze significative. Se questi sono ancora presenti, quindi occorre toorevisit i modelli di larghezza di banda.

**D**. Cosa accade se dispongono di più contenitori del volume nel dispositivo pianificazioni sovrapposte, ma tooeach applicati limiti diversi?

**R**. Si consideri la situazione in cui un utente dispone di un dispositivo con 3 contenitori di volume. Hello pianificazioni associate a questi contenitori completamente si sovrappongono. Per ognuno di questi contenitori, i limiti di larghezza di banda hello utilizzati sono rispettivamente 5, 10 e 15 Mbps. Quando si verificano i/o su tutti questi contenitori in hello può essere applicati contemporaneamente, minimo hello dei limiti di larghezza di banda hello 3: in questo caso 5 Mbps, perché queste in uscita sulla condivisione di richieste dei / o hello stessa coda.

## <a name="best-practices-for-bandwidth-templates"></a>Procedure consigliate per i modelli di larghezza di banda

Seguire queste procedure consigliate relative al dispositivo StorSimple:

* Configurare i modelli di larghezza di banda nel dispositivo tooenable limitazione variabile della velocità effettiva della rete hello dal dispositivo hello in momenti diversi del giorno hello. Questi modelli di larghezza di banda, quando vengono usati con le pianificazioni di backup, possono sfruttare in modo efficace ulteriore larghezza di banda della rete al fine di eseguire operazioni sul cloud durante le ore non di punta.
* Calcolare hello larghezza di banda effettivamente necessaria per una particolare distribuzione in base alle dimensioni di hello della distribuzione di hello e obiettivo del tempo di ripristino richiesto hello (RTO).

## <a name="next-steps"></a>Passaggi successivi

Altre informazioni, vedere [utilizzando hello tooadminister servizio di gestione di dispositivi StorSimple dispositivo StorSimple](storsimple-8000-manager-service-administration.md).


---
title: Gestire i modelli di larghezza di banda di StorSimple | Microsoft Docs
description: In questo articolo viene descritto come gestire i modelli di banda larga di StorSimple, i quali consentono di controllare il consumo di banda larga.
services: storsimple
documentationcenter: 
author: alkohli
manager: carmonm
editor: 
ms.assetid: 0027b90e-91a5-437d-9bd0-06b05674aa5f
ms.service: storsimple
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/16/2016
ms.author: alkohli
ms.openlocfilehash: df3ae8bf775370432b3648459a7c942afe69fb17
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="use-the-storsimple-manager-service-to-manage-storsimple-bandwidth-templates"></a>Utilizzare il servizio StorSimple Manager per gestire i modelli di larghezza di banda StorSimple.
## <a name="overview"></a>Overview
I modelli di larghezza di banda consentono di configurare l'uso della larghezza di banda della rete in più pianificazioni orarie, per suddividere in livelli i dati del dispositivo StorSimple nel cloud.

Utilizzando le pianificazioni relative alla limitazione larghezza di banda è possibile:

* Specificare pianificazioni della larghezza di banda personalizzate in base agli utilizzi di rete dipendenti dal carico di lavoro.
* Centralizzare la gestione e riutilizzare le pianificazioni su più dispositivi in modo semplice e immediato.

> [!NOTE]
> Questa funzionalità è disponibile soltanto per i dispositivi fisici StorSimple e non per quelli virtuali.
> 
> 

Tutti i modelli di larghezza di banda relativi al servizio vengono visualizzati in formato tabulare e contengono le informazioni seguenti:

* **Nome** : il nome univoco assegnato al modello di larghezza di banda al momento della creazione.
* **Pianificazione** : il numero di pianificazioni incluse in un determinato modello di larghezza di banda.
* **Utilizzato da** : il numero di volumi che utilizzano i modelli di larghezza di banda.

Per gestire i modelli di larghezza di banda, è possibile utilizzare la pagina la pagina **Configura** del servizio StorSimple Manager presente nel portale di Azure classico.

Inoltre, è possibile trovare ulteriori informazioni per configurare i modelli di larghezza di banda in:

* Domande e risposte sui modelli di larghezza di banda
* Procedure consigliate per i modelli di larghezza di banda

## <a name="add-a-bandwidth-template"></a>Aggiunta di un modello di larghezza di banda
Per creare un nuovo modello di larghezza di banda, attenersi alla procedura seguente.

#### <a name="to-add-a-bandwidth-template"></a>Per aggiungere un modello di larghezza di banda
1. Nella pagina **Configura** del servizio StorSimple Manager, fare clic sull'opzione per **aggiungere/modificare il modello di larghezza di banda**.
2. Nella finestra di dialogo **Aggiungi/modifica modello di larghezza di banda** :
   
   1. Dall'elenco a discesa **Modello** selezionare **Crea nuovo** per aggiungere un nuovo modello di larghezza di banda.
   2. Specificare un nome univoco per il modello di larghezza di banda.
3. Definire una **Pianificazione per la larghezza di banda**. Per creare una pianificazione:
   
   1. Dall'elenco a discesa, selezionare i giorni della settimana per i quali è stata configurata la pianificazione. È possibile selezionare più giorni, scegliendo le caselle di controllo posizionate prima dei rispettivi giorni.
   2. Selezionare l'opzione **Tutto il giorno** se la pianificazione viene applicata per l'intera giornata. Se questa opzione è selezionata, non sarà più possibile specificare un'opzione **Ora di inizio** oppure **Ora di fine**. La pianificazione viene eseguita dalle 12:00 alle 23:59.
   3. Dall'elenco a discesa, selezionare l'opzione **Ora di inizio**. Si tratta dell'orario relativo all'inizio della pianificazione.
   4. Dall'elenco a discesa, selezionare l'opzione **Ora di fine**. Si tratta dell'orario relativo all'interruzione della pianificazione.
      
      > [!NOTE]
      > Le pianificazioni sovrapposte non sono consentite. Se gli orari di inizio e di fine sono sovrapposti con altre pianificazioni, verrà visualizzato un messaggio di errore.
      > 
      > 
   5. Specificare **Velocità larghezza di banda**. Si tratta della larghezza di banda espressa in megabit al secondo (Mbps) usata dal dispositivo StorSimple nelle operazioni che coinvolgono il cloud (sia caricamento sia download). Specificare un numero compreso tra 1 e 1000 per questo campo.
   6. Fare clic sull’icona del segno di spunta ![Icona del segno di spunta](./media/storsimple-manage-bandwidth-templates/HCS_CheckIcon.png). Il modello creato verrà aggiunto all'elenco relativo ai modelli di larghezza di banda nella pagina **Configura** del servizio.
      
      ![Creare il modello di larghezza di banda.](./media/storsimple-manage-bandwidth-templates/HCS_CreateNewBT1.png)
4. Fare clic sull'opzione **Salva** nella parte inferiore della pagina, quindi selezionare **Sì** quando viene richiesta la conferma. In questo modo, verranno salvate le modifiche di configurazione apportate.

## <a name="edit-a-bandwidth-template"></a>Modifica di un modello di larghezza di banda
Eseguire la procedura seguente per modificare un modello di larghezza di banda.

### <a name="to-edit-a-bandwidth-template"></a>Per modificare un modello di larghezza di banda
1. Fare clic su **aggiungi/modifica modello di larghezza di banda**.
2. Nella finestra di dialogo **Aggiungi/modifica modello di larghezza di banda** :
   
   1. Dall'elenco a discesa **Modello** , selezionare un modello di larghezza di banda che si desidera modificare.
   2. Completare le modifiche. È possibile modificare qualsiasi impostazione esistente.
   3. Fare clic sull’icona del segno di spunta  ![Icona del segno di spunta](./media/storsimple-manage-bandwidth-templates/HCS_CheckIcon.png). Nella pagina Configura del servizio, il modello modificato viene visualizzato nell'elenco relativo ai modelli di larghezza di banda.
3. Per salvare le modifiche, fare clic su **Salva** nella parte inferiore della pagina. Fare clic sull'opzione **Sì** quando viene richiesta la conferma.

> [!NOTE]
> Non è possibile salvare le modifiche se la pianificazione modificata si sovrappone a una esistente nel modello di larghezza di banda che si sta modificando.
> 
> 

## <a name="delete-a-bandwidth-template"></a>Eliminazione di un modello di larghezza di banda
Eseguire la procedura seguente per eliminare un modello di larghezza di banda.

#### <a name="to-delete-a-bandwidth-template"></a>Per eliminare un modello di larghezza di banda
1. Nell'elenco tabulare relativo ai modelli di larghezza di banda disponibili per il servizio, selezionare il modello che si desidera eliminare. Nella parte più a destra del modello selezionato, viene visualizzata l'icona di eliminazione (**x**). Fare clic sull'icona **x** per eliminare il modello.
2. Verrà richiesto di confermare. Fare clic su **OK** per procedere.

Se il modello è utilizzato da qualche volume, non sarà possibile eliminarlo. Verrà visualizzato un messaggio di errore che indica che il modello è in uso. Viene visualizzata una finestra di dialogo di errore che indica che tutti i riferimenti al modello devono essere eliminati.

È possibile eliminare tutti i riferimenti al modello accedendo alla pagina **Contenitori di volume** e modificando i contenitori di volumi che usano questo modello. In questo modo, i contenitori useranno un altro modello oppure un'impostazione di larghezza di banda personalizzata o senza limiti. Una volta rimossi tutti i riferimenti, è possibile eliminare il modello.

## <a name="use-a-default-bandwidth-template"></a>Utilizzo di un modello di larghezza di banda predefinito
Per impostazione predefinita, un modello di larghezza di banda viene fornito e viene utilizzato dai contenitori di volume al fine di applicare i controlli di larghezza di banda richiesti per accedere al cloud. Il modello predefinito può essere utilizzato anche come riferimento immediato per gli utenti che creano modelli personalizzati. Di seguito, sono indicati i dettagli di questo modello predefinito:

* **Nome** : notte e fine settimana senza limiti
* **Pianificazione**: una pianificazione singola, dal lunedì al venerdì. Applica una velocità di larghezza di banda di 1 Mbps nell'intervallo d'uso del dispositivo compreso tra le 08:00 e le 17:00. La larghezza di banda viene impostata su Illimitata per tutto il resto della settimana.

È possibile modificare il modello predefinito. L'utilizzo di questo modello (incluse le versioni modificate) viene monitorato.

## <a name="create-an-all-day-bandwidth-template-that-starts-at-a-specified-time"></a>Creazione di un modello di larghezza di banda giornaliero che viene avviato a un determinato orario
Attenersi a questa procedura per creare una pianificazione che si avvia a un orario specifico e resta in esecuzione per tutto il giorno. In questo esempio, la pianificazione viene avviata alle 09:00 del mattino e resta in esecuzione fino alle 09:00 del mattino successivo. Tenere presente che gli orari di inizio e di fine relativi a una determinata pianificazione devono essere inclusi nella stessa pianificazione di 24 ore e non possono estendersi per più giorni. Nel caso in cui sia necessario impostare i modelli di larghezza di banda che si estendono per più giorni, è necessario utilizzare più pianificazioni, come illustrato nell'esempio.

#### <a name="to-create-an-all-day-bandwidth-template"></a>Per creare un modello di larghezza di banda giornaliero
1. Creare una pianificazione che viene avviata alle 09:00 del mattino e resta in esecuzione fino a mezzanotte.
2. Aggiungere un'altra pianificazione. Configurare la seconda pianificazione affinché venga eseguita da mezzanotte alle 09:00 del mattino.
3. Salvare il modello di larghezza di banda.

A questo punto, la pianificazione composta viene avviata a un orario scelto dall'utente e resta in esecuzione per tutto il giorno.

## <a name="questions-and-answers-about-bandwidth-templates"></a>Domande e risposte sui modelli di larghezza di banda
**D**. Cosa accade ai controlli della larghezza di banda nei periodi tra pianificazioni, ossia quando una pianificazione è terminata e un'altra non è ancora stata avviata?

**R**. In questi casi, non verranno utilizzati controlli relativi alla larghezza di banda. Ciò significa che il dispositivo può usare una larghezza di banda illimitata, quando si suddividono su livelli i dati nel cloud.

**D**. È possibile modificare i modelli di larghezza di banda in un dispositivo offline?

**R**. Non è possibile modificare i modelli di larghezza di banda nei contenitori di volume, se il dispositivo corrispondente è offline.

**D**. È possibile modificare un modello di larghezza di banda associato a un contenitore di volume, quando i volumi associati sono offline?

**R**. È possibile modificare un modello di larghezza di banda associato a un contenitore di volume, i cui volumi sono offline. Tenere presente che quando i volumi sono offline, nessun dato viene suddiviso in livelli dal dispositivo al cloud.

**D**. È possibile eliminare un modello predefinito?

**R**. Sebbene sia possibile eliminare un modello predefinito, non si consiglia di effettuare tale operazione. L'utilizzo di questo modello predefinito (comprese le versioni modificate) viene monitorato. I dati di rilevamento vengono analizzati nel tempo e utilizzati al fine di migliorare il modello predefinito.

**D**. Come si determina la necessità di modificare i modelli di larghezza di banda?

**R**. Quando si assiste a un rallentamento o una riduzione delle prestazioni per più volte al giorno, vuol dire che è necessario modificare i modelli di larghezza di banda. In questo caso, monitorare l'archiviazione e l'utilizzo della rete controllando i grafici di input e output relativi alle prestazioni e alla produttività della rete.

Dai dati relativi alla produttività della rete, identificare l'orario e i contenitori di volume in cui si verifica il collo di bottiglia della rete. In questo caso, quando i dati vengono suddivisi in livelli nel cloud (informazioni disponibili nelle prestazioni di I/O per tutti i contenitori di volume da dispositivo a cloud), sarà necessario modificare i modelli di larghezza di banda associati con i contenitori di volume.

Quando i modelli modificati sono in uso, è necessario monitorare di nuovo la rete per latenze significative. Se vengono rilevate, sarà necessario rivedere i modelli di larghezza di banda.

**D**. Cosa accade se in più contenitori di volume del dispositivo sono presenti pianificazioni che si sovrappongono, ma alle quali vengono applicati limitazioni differenti?

**R**. Si consideri la situazione in cui un utente dispone di un dispositivo con 3 contenitori di volume. Le pianificazioni associate a questi contenitori si sovrappongono completamente. Per ognuno di questi contenitori, i limiti di larghezza di banda usati corrispondo a 5, 10 e 15 Mbps. Quando gli input/output si verificano su tali contenitori contemporaneamente, è possibile che si applichino i 3 limiti di larghezza di banda. In questo caso, 5 Mbps poiché le richieste I/O in uscita condividono la stessa coda.

## <a name="best-practices-for-bandwidth-templates"></a>Procedure consigliate per i modelli di larghezza di banda
Seguire queste procedure consigliate relative al dispositivo StorSimple:

* Configurare i modelli di larghezza di banda sul dispositivo al fine di attivare la limitazione della variabile relativa alla produttività di rete in base al dispositivo e a diversi momenti della giornata. Questi modelli di larghezza di banda, quando vengono usati con le pianificazioni di backup, possono sfruttare in modo efficace ulteriore larghezza di banda della rete al fine di eseguire operazioni sul cloud durante le ore non di punta.
* Calcolare la larghezza di banda necessaria per eseguire una distribuzione particolare basata sulle dimensioni della distribuzione e sull'obiettivo tempo di ripristino.

## <a name="next-steps"></a>Passaggi successivi
Ulteriori informazioni sull’ [utilizzo del servizio StorSimple Manager per amministrare il dispositivo StorSimple](storsimple-manager-service-administration.md).


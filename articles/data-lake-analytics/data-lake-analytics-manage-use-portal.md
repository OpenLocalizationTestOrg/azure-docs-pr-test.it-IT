---
title: portale di Azure di hello aaaManage Azure Data Lake Analitica con | Documenti Microsoft
description: Informazioni su come toomanage acounts Data Lake Analitica, dati di origini, gli utenti e i processi.
services: data-lake-analytics
documentationcenter: 
author: saveenr
manager: jhubbard
editor: cgronlun
ms.assetid: a0e045f1-73d6-427f-868d-7b55c10f811b
ms.service: data-lake-analytics
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 12/05/2016
ms.author: edmaca
ms.openlocfilehash: f63ccdfae79772c92e92462194e8cdc636a73dc6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="manage-azure-data-lake-analytics-by-using-hello-azure-portal"></a>Gestire Azure Data Lake Analitica con hello portale di Azure
[!INCLUDE [manage-selector](../../includes/data-lake-analytics-selector-manage.md)]

Informazioni su come gli account di Azure Data Lake Analitica toomanage, origini dati di account, gli utenti e i processi tramite hello portale di Azure. argomenti relativi alla gestione toosee sull'uso di altri strumenti, fare clic su una scheda nella parte superiore di hello della pagina hello.

<!-- ################################ -->
<!-- ################################ -->

## <a name="manage-data-lake-analytics-accounts"></a>Gestire gli account di Data Lake Analytics

### <a name="create-an-account"></a>Creare un account

1. Accedi toohello [portale di Azure](https://portal.azure.com).
2. Fare clic su **Nuovo** > **Intelligence e analisi** > **Data Lake Analytics**.
3. Selezionare i valori per hello seguenti elementi: 
   1. **Nome**: nome hello di hello account Data Lake Analitica.
   2. **Sottoscrizione**: hello sottoscrizione di Azure usata per l'account di hello.
   3. **Gruppo di risorse**: gruppo di risorse di Azure hello in quale account hello toocreate. 
   4. **Percorso**: hello Data Center di Azure per l'account Data Lake Analitica hello. 
   5. **Archivio Data Lake**: hello toobe archivio predefinito utilizzato per l'account Data Lake Analitica hello. account archivio Azure Data Lake Hello e hello Data Lake Analitica account deve trovarsi in hello nello stesso percorso.
4. Fare clic su **Crea**. 

### <a name="delete-a-data-lake-analytics-account"></a>Eliminare un account di Data Lake Analytics

Prima di eliminare un account di Data Lake Analytics, eliminare il relativo account di Data Lake Store predefinito.

1. Nel portale di Azure hello, visitare l'account Data Lake Analitica tooyour.
2. Fare clic su **Elimina**.
3. Nome account hello del tipo.
4. Fare clic su **Elimina**.

<!-- ################################ -->
<!-- ################################ -->

## <a name="manage-data-sources"></a>Gestire le origini dati

Data Lake Analitica supporta le seguenti origini dati hello:

* Data Lake Store
* Archiviazione di Azure

È possibile usare Esplora dati toobrowse le origini dati ed eseguire operazioni di gestione di file di base. 

### <a name="add-a-data-source"></a>Aggiungere un'origine dati

1. Nel portale di Azure hello, visitare l'account Data Lake Analitica tooyour.
2. Fare clic su **Origini dati**.
3. Fare clic su **Aggiungi origine dati**.
    
   * un account archivio Data Lake tooadd, è necessario hello account toohello nome e l'accesso tooquery in grado di toobe è.
   * tooadd archiviazione Blob di Azure, è necessario che account di archiviazione hello e hello chiave dell'account. toofind account di archiviazione toohello usarle, andare nel portale di hello.

## <a name="set-up-firewall-rules"></a>Configurare le regole del firewall

È possibile utilizzare Data Lake Analitica toofurther bloccare l'accesso tooyour account Data Lake Analitica a livello di rete hello. È possibile abilitare un firewall, specificare un indirizzo IP o definire un intervallo di indirizzi IP per i client attendibili. Dopo aver abilitato queste misure, solo i client che dispongono degli indirizzi IP hello intervallo hello definito possono connettersi toohello store.

Se altri servizi di Azure, ad esempio Data Factory di Azure o le macchine virtuali, connettono l'account Data Lake Analitica toohello, verificare che **consentire servizi Azure** sia **su**. 

### <a name="set-up-a-firewall-rule"></a>Configurare una regola del firewall

1. Nel portale di Azure hello, visitare l'account Data Lake Analitica tooyour.
2. Scegliere hello dal menu a sinistra di hello **Firewall**.

## <a name="add-a-new-user"></a>Aggiungere un nuovo utente

È possibile utilizzare hello **Aggiunta guidata utente** tooeasily effettuare il provisioning di nuovi utenti Data Lake.

1. Nel portale di Azure hello, visitare l'account Data Lake Analitica tooyour.
2. In hello a sinistra, sotto **Introduzione**, fare clic su **Aggiunta guidata utente**.
3. Selezionare un utente e quindi fare clic su **Seleziona**.
4. Selezionare un ruolo e quindi fare clic su **Seleziona**. tooset di un nuovo toouse sviluppatore Azure Data Lake, seleziona hello **Data Lake Analitica Developer** ruolo.
5. Selezionare hello elenchi di controllo accesso (ACL) per i database hello U-SQL. Dopo aver completato le selezioni, fare clic su **Seleziona**.
6. Selezionare gli elenchi ACL hello per file. Per l'archivio predefinito hello, non modificare hello ACL per la cartella radice hello "/" e per la cartella /system hello. Fare clic su **Seleziona**.
7. Esaminare tutte le modifiche selezionate e quindi fare clic su **Esegui**.
8. Al termine procedura guidata hello, fare clic su **eseguita**.

## <a name="manage-role-based-access-control"></a>Gestire il controllo degli accessi in base al ruolo

Analogamente ad altri servizi Azure, è possibile utilizzare toocontrol di controllo di accesso basato sui ruoli (RBAC) come gli utenti interagiscono con il servizio di hello.

ruoli RBAC standard Hello hanno hello seguenti funzionalità:
* **Proprietario**: può inviare i processi, monitorare i processi, annullare i processi da qualsiasi utente e configurare l'account di hello.
* **Collaboratore**: può inviare i processi, monitorare i processi, annullare i processi da qualsiasi utente e configurare l'account di hello.
* **Lettore**: può monitorare i processi.

Usare hello Data Lake Analitica Developer tooenable U-SQL sviluppatori toouse hello Data Lake Analitica servizio ruolo. È possibile utilizzare il ruolo Data Lake Analitica Developer hello per:
* Inviare processi.
* Monitorare lo stato di stato e hello processo dei processi inviati da qualsiasi utente.
* Vedere script U-SQL hello i processi inviati da qualsiasi utente.
* Annullare solo i processi creati personalmente.

### <a name="add-users-or-security-groups-tooa-data-lake-analytics-account"></a>Aggiungere utenti o gruppi di sicurezza tooa account Data Lake Analitica

1. Nel portale di Azure hello, visitare l'account Data Lake Analitica tooyour.
2. Fare clic su **Controllo di accesso (IAM)** > **Aggiungi**.
3. Selezionare un ruolo.
4. Aggiungere un utente.
5. Fare clic su **OK**.

>[!NOTE]
>Se un utente o un gruppo di sicurezza deve toosubmit processi, devono anche l'autorizzazione nell'account di archiviazione hello. Per altre informazioni, vedere [Protezione dei dati presenti in Data Lake Store](../data-lake-store/data-lake-store-secure-data.md).
>

<!-- ################################ -->
<!-- ################################ -->

## <a name="manage-jobs"></a>Gestire i processi

### <a name="submit-a-job"></a>Inviare un processo

1. Nel portale di Azure hello, visitare l'account Data Lake Analitica tooyour.

2. Fare clic su **Nuovo processo**. Per ogni processo, configurare quanto segue:

    1. **Nome del processo**: nome hello del processo di hello.
    2. **Priorità**: i numeri più bassi hanno maggiore priorità. Se i due processi sono in coda, hello con valore di priorità inferiore viene eseguito per primo.
    3. **Parallelismo**: numero massimo di hello di calcolo elabora tooreserve per questo processo.

3. Fare clic su **Submit Job**.

### <a name="monitor-jobs"></a>Monitorare i processi

1. Nel portale di Azure hello, visitare l'account Data Lake Analitica tooyour.
2. Fare clic su **Visualizza tutti i processi**. Viene visualizzato un elenco di tutti i processi di hello attive e completate di recente nell'account hello.
3. Facoltativamente, fare clic su **filtro** toohelp è trovare processi hello da **intervallo di tempo**, **nome del processo**, e **autore** valori. 

### <a name="monitoring-pipeline-jobs"></a>Monitoraggio dei processi della pipeline
I processi che fanno parte di una pipeline di lavoro, in genere in sequenza, tooaccomplish uno scenario specifico. È ad esempio possibile avere una pipeline che esegue la pulizia, estrae, trasforma, e aggrega l'utilizzo per Customer Insights. I processi di pipeline vengono identificati utilizzando proprietà "Pipeline" hello, quando è stato inviato il processo di hello. Per i processi pianificati usando ADF V2 questa proprietà viene popolata automaticamente. 

tooview un elenco di processi U-SQL che fanno parte della pipeline: 

1. Nel portale di Azure hello, andare account Data Lake Analitica tooyour.
2. Fare clic su **Informazioni dettagliate sul processo**. Hello che scheda "Tutti i processi" verrà automaticamente modificata, che mostra un elenco di esecuzione, in coda e i processi di fine.
3. Fare clic su hello **processi Pipeline** scheda. Verrà visualizzato un elenco di processi della pipeline, con statistiche aggregate per ogni pipeline.

### <a name="monitoring-recurring-jobs"></a>Monitoraggio dei processi ricorrenti
Un processo ricorrente è quello che ha hello stessa logica di business ma utilizza dati di input diversi ogni volta che viene eseguito. Idealmente, devono sempre avere esito positivo e i processi ricorrenti con tempo di esecuzione relativamente stabile; monitoraggio di questi comportamenti consente di verificare che il processo di hello sia integro. I processi ricorrenti vengono identificati utilizzando proprietà di "Recurrence" hello. Per i processi pianificati usando ADF V2 questa proprietà viene popolata automaticamente.

un elenco di processi U-SQL che sono ricorrenti tooview: 

1. Nel portale di Azure hello, andare account Data Lake Analitica tooyour.
2. Fare clic su **Informazioni dettagliate sul processo**. Hello che scheda "Tutti i processi" verrà automaticamente modificata, che mostra un elenco di esecuzione, in coda e i processi di fine.
3. Fare clic su hello **processi ricorrenti** scheda. Verrà visualizzato un elenco di processi ricorrenti, con statistiche aggregate per ogni processo.

## <a name="manage-policies"></a>Gestire i criteri

### <a name="account-level-policies"></a>Criteri a livello di account

Questi criteri si applicano i processi di tooall in un account Data Lake Analitica.

#### <a name="maximum-number-of-aus-in-a-data-lake-analytics-account"></a>Numero massimo di unità di analisi in un account di Data Lake Analytics
Un criterio hello indica quante unità Analitica (Australia) può utilizzare l'account Data Lake Analitica. Per impostazione predefinita, il valore di hello è too250. Ad esempio, se questo valore è impostato too250 Australia, è possibile fare un processo in esecuzione con 250 tooit AUs assegnato o 10 processi in esecuzione con 25 AUs ogni. Processi aggiuntivi che vengono inviati vengono messe in coda finché non vengono completati i processi in esecuzione hello. Completamento dei processi in esecuzione, AUs vengono liberate per hello in coda toorun processi.

numero hello toochange di AUs per l'account Data Lake Analitica:

1. Nel portale di Azure hello, visitare l'account Data Lake Analitica tooyour.
2. Fare clic su **Proprietà**.
3. In **AUs massimo**, spostare hello dispositivo di scorrimento tooselect un valore o immettere il valore di hello nella casella di testo hello. 
4. Fare clic su **Salva**.

> [!NOTE]
> Se è necessario più di hello predefinito (250) Australia, nel portale di hello, fare clic su **+ supporto** toosubmit una richiesta di supporto. numero di Hello di AUs disponibili nell'account Data Lake Analitica può essere aumentato.
>

#### <a name="maximum-number-of-jobs-that-can-run-simultaneously"></a>Numero massimo di processi che possono essere eseguiti contemporaneamente
Un criterio controlla il numero di processi è possibile eseguire in hello contemporaneamente. Per impostazione predefinita, questo valore è impostato too20. Se il Analitica Lake dati include AUs disponibili, nuovi processi sono pianificati toorun immediatamente finché il numero totale di hello di processi in esecuzione raggiunge il valore di hello dei criteri. Quando si raggiunge hello il numero massimo di processi che possono essere eseguite contemporaneamente, i processi successivi vengono accodati in ordine di priorità fino al completamento di uno o più processi in esecuzione (a seconda della disponibilità di aggiornamenti automatici).

numero di hello toochange di processi che possono essere eseguite contemporaneamente:

1. Nel portale di Azure hello, visitare l'account Data Lake Analitica tooyour.
2. Fare clic su **Proprietà**.
3. In **numero massimo di processi in esecuzione**, spostare hello dispositivo di scorrimento tooselect un valore o immettere il valore di hello nella casella di testo hello. 
4. Fare clic su **Salva**.

> [!NOTE]
> Se è necessario più di hello numero (20) predefinito dei processi, nel portale di hello, fare clic su toorun **+ supporto** toosubmit una richiesta di supporto. numero di Hello dei processi che è possibile eseguire contemporaneamente l'account Data Lake Analitica può essere aumentato.
>

#### <a name="how-long-tookeep-job-metadata-and-resources"></a>Quanto tempo i metadati del processo tookeep e risorse 
Quando gli utenti eseguono processi U-SQL, il servizio Data Lake Analitica hello mantiene tutti i file correlati. I file correlati includono script hello U-SQL, file DLL hello a cui fa riferimento in script hello U-SQL, risorse compilate e statistiche. file Hello sono nella cartella /system/ hello dell'account di archiviazione di Azure Data Lake hello predefinito. Questo criterio controlla per quanto tempo queste risorse si trovano prima di essere eliminati automaticamente (valore predefinito di hello è 30 giorni). È possibile utilizzare questi file per il debug e per ottimizzare le prestazioni dei processi che saranno nuovamente in futuro hello.

toochange quanto tempo i metadati del processo tookeep e risorse:

1. Nel portale di Azure hello, visitare l'account Data Lake Analitica tooyour.
2. Fare clic su **Proprietà**.
3. In **giorni tooRetain processo query**, spostare hello dispositivo di scorrimento tooselect un valore o immettere il valore di hello nella casella di testo hello.  
4. Fare clic su **Salva**.

### <a name="job-level-policies"></a>Criteri a livello di processo
Con i criteri a livello di processo, è possibile controllare hello AUs massimo e hello priorità massima che singoli utenti (o i membri di gruppi di sicurezza specifici) è possono impostare per i processi che hanno inviato personalmente. Questo consente di controllare i costi di hello sostenuti dagli utenti. Consente inoltre di effetto hello controllo che i processi pianificati con priorità alta potrebbe essere processi di produzione che sono in esecuzione hello stesso account Data Lake Analitica.

Data Lake Analitica presenta due criteri che è possibile impostare a livello di processo hello:

* **Limite massimo di aggiornamenti automatici per processo**: agli utenti di inviare solo i processi con numero toothis di Australia. Per impostazione predefinita, questo limite è hello come hello Australia massimo per l'account di hello.
* **Priorità**: agli utenti di inviare solo i processi che hanno un valore di priorità toothis inferiori o uguali. Si noti che un numero più alto indica una priorità più bassa. Per impostazione predefinita, questo viene impostato too1, hello più alto possibile di priorità.

Per ogni account è impostato un criterio predefinito criteri predefiniti Hello applicano tooall gli utenti dell'account hello. È possibile impostare altri criteri per utenti e gruppi specifici. 

> [!NOTE]
> I criteri a livello di account e quelli a livello di processo vengono applicati contemporaneamente.
>

#### <a name="add-a-policy-for-a-specific-user-or-group"></a>Aggiungere un criterio per un utente o un gruppo specifico

1. Nel portale di Azure hello, visitare l'account Data Lake Analitica tooyour.
2. Fare clic su **Proprietà**.
3. In **limiti invio processo**, fare clic su hello **Aggiungi criterio** pulsante. Quindi, selezionare o immettere hello seguenti impostazioni:
    1. **Nome del criterio di calcolo**: immettere un nome di criterio, tooremind di scopo hello del criterio di hello.
    2. **Seleziona utente o gruppo**: selezionare utente hello o un gruppo a cui si applica questo criterio.
    3. **Impostare hello processo Australia limite**: limite di hello Australia che applica toohello selezionato utente o gruppo.
    4. **Impostare il limite di priorità hello**: hello priorità limite che applica toohello selezionato utente o gruppo.

4. Fare clic su **OK**.

5. il nuovo criterio di Hello è elencato nella hello **predefinito** in Criteri di tabella **limiti di processo di invio**. 

#### <a name="delete-or-edit-an-existing-policy"></a>Eliminare o modificare un criterio esistente

1. Nel portale di Azure hello, visitare l'account Data Lake Analitica tooyour.
2. Fare clic su **Proprietà**.
3. In **limiti invio processo**, criteri di ricerca hello desiderato tooedit.
4.  hello toosee **eliminare** e **modifica** fare clic su Opzioni, nella colonna più a destra di hello della tabella di hello, **...** .

### <a name="additional-resources-for-job-policies"></a>Risorse aggiuntive per i criteri dei processi
* [Post di blog con una panoramica dei criteri](https://blogs.msdn.microsoft.com/azuredatalake/2017/06/08/managing-your-azure-data-lake-analytics-compute-resources-overview/)
* [Post di blog sui criteri a livello di account](https://blogs.msdn.microsoft.com/azuredatalake/2017/06/08/managing-your-azure-data-lake-analytics-compute-resources-account-level-policy/)
* [Post di blog sui criteri a livello di processo](https://blogs.msdn.microsoft.com/azuredatalake/2017/06/08/managing-your-azure-data-lake-analytics-compute-resources-job-level-policy/)

## <a name="next-steps"></a>Passaggi successivi

* [Panoramica di Azure Data Lake Analytics](data-lake-analytics-overview.md)
* [Introduzione a Data Lake Analitica utilizzando hello portale di Azure](data-lake-analytics-get-started-portal.md)
* [Gestire Azure Data Lake Analytics tramite Azure PowerShell](data-lake-analytics-manage-use-powershell.md)


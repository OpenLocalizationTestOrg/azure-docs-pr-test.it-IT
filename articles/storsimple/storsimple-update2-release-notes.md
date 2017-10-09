---
title: note sulla versione di aggiornamento 2 di serie 8000 aaaStorSimple | Documenti Microsoft
description: "Descrive le nuove funzionalità hello, problemi e soluzioni alternative per StorSimple 8000 Series Update 2."
services: storsimple
documentationcenter: NA
author: SharS
manager: carmonm
editor: 
ms.assetid: e2c8bffd-7fc5-4b77-b632-a4f59edacc3a
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: TBD
ms.date: 05/24/2016
ms.author: v-sharos
ms.openlocfilehash: 36c75aad900c7b1286a924732967b8ee519a3d4a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="storsimple-8000-series-update-2-release-notes"></a>Note sulla versione dell'aggiornamento 2 di StorSimple serie 8000
## <a name="overview"></a>Panoramica
Hello note sulla versione seguenti descrivono le nuove funzionalità di hello e identificare i problemi critici aperti di hello per StorSimple 8000 Series Update 2. Contengono inoltre un elenco di software di StorSimple hello, driver e aggiornamenti del firmware del disco inclusi in questa versione. 

Aggiornamento 2 può essere dispositivo StorSimple tooany applicato in esecuzione Release (GA) o aggiornamento 0,1 tramite aggiornamento 1.2. versione del dispositivo Hello associata a Update 2 è 6.3.9600.17673.

Esaminare informazioni hello contenute in versione di hello note prima di distribuire hello aggiornare nella soluzione StorSimple.

> [!IMPORTANT]
> * Sono necessari circa 4-7 ore tooinstall questo aggiornamento (inclusi gli aggiornamenti di Windows hello). 
> * L'aggiornamento 2 contiene aggiornamenti del software, del driver LSI e del firmware SSD.
> * Per le nuove versioni, non sarà possibile visualizzare gli aggiornamenti immediatamente perché è un'implementazione graduale dei hello aggiornamenti. Attendere alcuni giorni e quindi provare a cercare nuovamente gli aggiornamenti, perché verranno presto resi disponibili.
> 
> 

## <a name="whats-new-in-update-2"></a>Novità dell'aggiornamento 2
Aggiornamento 2 introduce nuove funzionalità seguenti di hello.

* **Aggiunto in locale volumi** : nelle versioni precedenti della serie StorSimple 8000 hello, blocchi di dati sono stati cloud toohello a più livelli in base all'utilizzo. Si è verificato alcun tooguarantee di modo che blocchi sarebbero rimangono in locale. In Update 2, quando si crea un volume, è possibile designare un volume di dati aggiunti in locale e primari di tale volume non verrà cloud toohello a più livelli. Snapshot dei volumi aggiunti in locale sarà comunque copiati toohello cloud per il backup in modo che il cloud hello può essere utilizzato per scopi di ripristino di emergenza e mobilità dei dati. Inoltre, è possibile modificare il tipo di volume hello (convertire toolocally bloccato di volumi a livelli e Converti in locale aggiunto volumi tootiered). 
* **Miglioramenti di dispositivo virtuale StorSimple** : in precedenza, hello StorSimple serie 8000 posizionato dispositivo virtuale hello come soluzione di sviluppo/test o di ripristino di emergenza. Era disponibile un solo modello di dispositivo virtuale (modello 1100). L'aggiornamento 2 introduce due modelli di dispositivi virtuali: 
  
  * Nessuna modifica, 8010: spazio (in precedenza noti come hello 1100): ha una capacità di 30 TB e Usa Azure storage standard.
  * 8020: ha una capacità di 64 TB e usa l'archiviazione Premium di Azure per migliorare le prestazioni.
    
    È presente un singolo disco rigido virtuale per entrambi i modelli di dispositivi virtuali (8010/8020). Al primo avvio di dispositivo virtuale hello, vengono rilevati i parametri di piattaforma hello e lo applica la versione di hello modello corretto.
* **Miglioramenti alla rete** – Update 2 contiene hello seguenti miglioramenti di rete:
  
  * Più schede di rete può essere abilitati per il cloud hello in modo che il failover può verificarsi se una scheda di rete ha esito negativo.
  * Miglioramenti di routing, con metriche fisse per blocchi abilitati per il cloud.
  * Nuovo tentativo online delle risorse con errori prima di un failover.
  * Nuovi avvisi per gli errori del servizio.
* **Aggiornamento dei miglioramenti** : In Aggiornamento 1.2 e versioni precedenti, serie StorSimple 8000 hello è stato aggiornato tramite due canali: Windows Update per il clustering, iSCSI e così via e Microsoft Update per i file binari e del firmware.
    L'aggiornamento 2 usa Microsoft Update per tutti i pacchetti di aggiornamento. Questo dovrebbe condurre ora tooless oppure l'applicazione di patch al failover. 
* **Aggiornamenti del firmware** : hello seguenti firmware aggiornamenti sono inclusi:
  
  * LSI: lsi_sas2.sys versione del prodotto 2.00.72.10
  * Solo unità SSD (non sono presenti aggiornamenti dell'unità disco rigido): XMGG, XGEG, KZ50, F6C2 e VR08
* **Supporto proattivo** – aggiornamento 2 abilita Microsoft toopull informazioni diagnostiche aggiuntive dal dispositivo hello. Quando il team operativo identifica i dispositivi che si sono verificati problemi, siamo migliori informazioni toocollect forniti dal dispositivo hello e diagnosticare i problemi. **Accettando Update 2, ci Consenti tooprovide questo supporto proattivo**.    

## <a name="issues-fixed-in-update-2"></a>Problemi risolti nell'aggiornamento 2
Hello le tabelle seguenti viene fornito un riepilogo dei problemi che sono stati risolti in 2 gli aggiornamenti.    

| No. | Funzionalità | Problema | Si applica toophysical dispositivo | Si applica toovirtual dispositivo |
| --- | --- | --- | --- | --- |
| 1 |Interfacce di rete |Dopo un aggiornamento tooUpdate 1, hello servizio StorSimple Manager ha segnalato che le porte Data2 e Data3 hello non è riuscita in un controller. Il problema è stato risolto. |Sì |No |
| 2 |Aggiornamenti |Dopo un aggiornamento tooUpdate 1, gli avvisi di allarme acustico durante hello portale di Azure classico su più dispositivi. Il problema è stato risolto. |Sì |No |
| 3 |Autenticazione Openstack |Quando si usa Openstack come provider di servizi cloud, potrebbe venire visualizzato un errore che informa che la stringa di autenticazione cloud è troppo lunga. Questo problema è stato risolto. |Sì |No |

## <a name="known-issues-in-update-2"></a>Problemi noti nell'aggiornamento 2
Hello nella tabella seguente fornisce un riepilogo dei problemi noti in questa versione.

| No. | Funzionalità | Problema | Commenti/Soluzione alternativa | Si applica toophysical dispositivo | Si applica toovirtual dispositivo |
| --- | --- | --- | --- | --- | --- |
| 1 |Quorum disco |In rari casi, se la maggior parte hello dei dischi nell'enclosure EBOD hello di un dispositivo 8600 si disconnette e il quorum dischi non è disponibile, quindi il pool di archiviazione hello passerà alla modalità offline. E rimarrà offline anche se hello dischi vengono riconnessi. |Sarà necessario dispositivo hello tooreboot. Se hello problema persiste, contattare il supporto Microsoft per i passaggi successivi. |Sì |No |
| 2 |ID controller non corretto |Quando viene eseguita la sostituzione di un controller, il controller 0 potrebbe essere visualizzato come controller 1. Durante la sostituzione del controller, quando hello immagine viene caricata dal nodo peer hello, ID controller hello è inoltre possibile scaricare inizialmente come ID del controller peer hello In rari casi, questo comportamento può verificarsi anche dopo un riavvio del sistema. |Non è necessaria alcuna azione da parte dell’utente. Questa situazione si risolverà da solo dopo la sostituzione dei controller hello è stata completata. |Sì |No |
| 3 |Account di archiviazione |Utilizzando l'account di archiviazione di hello toodelete servizio di archiviazione hello è uno scenario non supportato. Questo conduce tooa situazione in cui non è possibile recuperare i dati utente. | |Sì |Sì |
| 4 |Failover del dispositivo |Failover multipli di un contenitore del volume da hello dispositivi di destinazione toodifferent origine dispositivo stesso non è supportata. Il failover da un singolo messaggi non recapitabili toomultiple dispositivi renderà i contenitori di volumi hello nel primo dispositivo sottoposto a failover hello perdere la proprietà dei dati. Dopo un failover, questi contenitori di volumi o di un comportamento diverso quando vengono visualizzati nel portale di Azure classico hello. | |Sì |No |
| 5 |Installazione |Durante l'adattatore StorSimple per l'installazione di SharePoint, è necessario tooprovide IP di un dispositivo affinché hello installazione toofinish correttamente. | |Sì |No |
| 6 |Proxy Web |Se la configurazione del proxy web è HTTPS come hello specificato protocollo, la comunicazione del dispositivo al servizio ne risentirà e dispositivo hello passerà alla modalità offline. Verranno inoltre generati pacchetti di supporto nel processo di hello, usando risorse significative sul dispositivo. |Verificare che URL del proxy web hello disponga di HTTP hello protocollo specificato. Per ulteriori informazioni, visitare troppo[configurare il proxy web per il dispositivo](storsimple-configure-web-proxy.md). |Sì |No |
| 7 |Proxy Web |Se si configurano e abilitare il proxy web su un dispositivo registrato, è necessario controller attivo di hello toorestart sul dispositivo. | |Sì |No |
| 8 |Elevata latenza del cloud ed elevato carico di lavoro I/O |Quando il dispositivo StorSimple rileva una combinazione di cloud ad alta latenza (ordine di secondi) e un elevato carico di lavoro dei / o, i volumi del dispositivo hello entrano in uno stato danneggiato e hello i/o potrebbe verificarsi un errore "dispositivo non pronto". |Si verrà necessario controller del dispositivo toomanually riavvio hello o eseguire un toorecover di failover del dispositivo da questa situazione. |Sì |No |
| 9 |Azure PowerShell |Quando si usa il cmdlet di StorSimple hello **Get AzureStorSimpleStorageAccountCredential &#124; Select-Object - Wait prima 1 -** tooselect hello primo oggetto in modo che è possibile creare un nuovo **VolumeContainer** oggetto hello cmdlet restituisce tutti gli oggetti di hello. |Eseguire il wrapping hello cmdlet tra parentesi, come indicato di seguito: **(Get-Azure-StorSimpleStorageAccountCredential) &#124; Select-Object - Wait prima 1 -** |Sì |Sì |
| 10 |Migrazione |Quando più contenitori di volumi vengono passati per la migrazione, hello greco per il backup più recente è preciso solo per il primo contenitore di volume hello. Inoltre, la migrazione parallela inizierà dopo hello backup primi 4 hello primo contenitore del volume viene eseguita la migrazione. |Si consiglia di migrare un contenitore del volume alla volta. |Sì |No |
| 11 |Migrazione |Dopo il ripristino di hello, i volumi non vengono aggiunti toohello backup hello o criteri di gruppo del disco virtuale. |È necessario tooadd questi volumi tooa dei criteri di backup nei backup toocreate ordine. |Sì |Sì |
| 12 |Migrazione |Al termine della migrazione hello, non devono accedere a dispositivi serie 5000 o 7000 hello hello eseguita la migrazione di contenitori di dati. |È consigliabile eliminare hello che la migrazione di contenitori di dati dopo la migrazione di hello completo viene eseguito il commit. |Sì |No |
| 13 |Clonazione e ripristino di emergenza |Un dispositivo StorSimple esegue Update 1 non è possibile clonare o eseguire disaster recovery tooa dispositivo che esegue pre-aggiornamento 1. |Sarà necessario tooupdate hello destinazione dispositivo tooUpdate 1 tooallow queste operazioni |Sì |Sì |
| 14 |Migrazione |La configurazione del backup per la migrazione potrebbe non riuscire in un dispositivo di serie 5000-7000 quando sono presenti gruppi di volumi senza volumi associati. |Eliminare tutti i gruppi di volumi vuoto hello con associato alcun volume, quindi ripetere il backup di configurazione hello. |Sì |No |
| 15 |Cmdlet di Azure PowerShell e volumi aggiunti in locale |Non è possibile creare un volume aggiunto in locale tramite i cmdlet di Azure PowerShell. I volumi creati tramite Azure PowerShell verranno suddivisi in livelli. |Utilizzare sempre volumi tooconfigure aggiunto in locale del servizio StorSimple Manager di hello. |Sì |No |
| 16 |Spazio disponibile per i volumi aggiunti in locale |Se si elimina un volume aggiunto in locale, spazio hello disponibile per nuovi volumi non può essere aggiornato immediatamente. aggiornamenti del servizio StorSimple Manager Hello hello spazio locale disponibile circa ogni ora. |Attendere un'ora prima di tentare di nuovo volume di toocreate hello. |Sì |No |
| 17 |Volumi aggiunti in locale |Il processo di ripristino espone i backup di snapshot temporanei hello in hello catalogo di Backup, ma solo per la durata hello hello del processo di ripristino. Inoltre, che espone un gruppo di dischi virtuali con prefisso **tmpCollection** su hello **criteri di Backup** pagina, ma solo per la durata hello di hello processo di ripristino. |Questo comportamento può verificarsi se il processo di ripristino dispone solo di volumi associati in locale o di una combinazione di volumi associati in locale e a livelli. Se il processo di ripristino hello include solo i volumi a livelli, questo comportamento non verrà eseguita. Non è necessario alcun intervento dell'utente. |Sì |No |
| 18 |Volumi aggiunti in locale |Se si annulla un processo di ripristino e si verifica un failover del controller immediatamente in seguito, si visualizzerà il processo di ripristino hello **Failed** anziché **Canceled**. Se un processo di ripristino non riesce e si verifica un failover del controller immediatamente in seguito, si visualizzerà il processo di ripristino hello **Canceled** anziché **Failed**. |Questo comportamento può verificarsi se il processo di ripristino dispone solo di volumi associati in locale o di una combinazione di volumi associati in locale e a livelli. Se il processo di ripristino hello include solo i volumi a livelli, questo comportamento non verrà eseguita. Non è necessario alcun intervento dell'utente. |Sì |No |
| 19 |Volumi aggiunti in locale |Se si annulla un processo di ripristino oppure se un ripristino non riesce e viene quindi eseguito un failover del controller, un processo di ripristino aggiuntive viene visualizzato in hello **processi** pagina. |Questo comportamento può verificarsi se il processo di ripristino dispone solo di volumi associati in locale o di una combinazione di volumi associati in locale e a livelli. Se il processo di ripristino hello include solo i volumi a livelli, questo comportamento non verrà eseguita. Non è necessario alcun intervento dell'utente. |Sì |No |
| 20 |Volumi aggiunti in locale |Se si tenta di tooconvert un volume a livelli (creato e duplicato con aggiornamento 1.2 o versioni precedente) tooa localmente bloccato volume e il dispositivo sta esaurendo lo spazio o si verifica un'interruzione di cloud, quindi hello clone(s) potrebbe essere danneggiata. |Questo problema si verifica solo con i volumi che sono stati creati e clonati con software precedente all'aggiornamento 2. Si tratta di uno scenario poco frequente. | | |
| 21 |Conversione del volume |Non aggiornare hello ACR tooa collegato volume durante una conversione del volume è in corso (a più livelli toolocally bloccato o viceversa). Aggiornamento hello ACR potrebbe causare il danneggiamento dei dati. |Se necessario, aggiornare conversione del volume hello ACR toohello precedenti e non apportare ulteriori aggiornamenti ACR durante la conversione di hello è in corso. | | |

## <a name="controller-and-firmware-updates-in-update-2"></a>Aggiornamenti del controller e del firmware presenti nell'aggiornamento 2
Questa versione Aggiorna driver hello e il firmware del disco hello sul dispositivo.

* Per ulteriori informazioni su firmware LSI hello aggiornamento, vedere l'articolo della Microsoft Knowledge base 3121900. 
* Per ulteriori informazioni su firmware del disco hello aggiornamento, vedere l'articolo della Microsoft Knowledge base 3121899.

## <a name="virtual-device-updates-in-update-2"></a>Aggiornamenti del dispositivo virtuale nell'aggiornamento 2
Questo aggiornamento non può essere applicato toohello dispositivo virtuale. Nuovi dispositivi virtuali saranno necessario toobe creato. 

## <a name="next-step"></a>Passaggio successivo
Informazioni su come troppo[installare l'aggiornamento 2](storsimple-install-update-2.md) nel dispositivo StorSimple.


---
title: note sulla versione di aaaStorSimple 8000 Series Update 3 | Documenti Microsoft
description: "Descrive le nuove funzionalità hello, problemi e soluzioni alternative per StorSimple 8000 Series Update 3."
services: storsimple
documentationcenter: NA
author: alkohli
manager: timlt
editor: 
ms.assetid: 2158aa7a-4ac3-42ba-8796-610d1adb984d
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: TBD
ms.date: 02/27/2017
ms.author: alkohli
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 5bfcba61f7f210531437f650eafaad4dbd8c7c45
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="update-3-release-notes-for-your-storsimple-8000-series-device"></a>Note sulla versione dell'aggiornamento 3 del dispositivo StorSimple serie 8000

## <a name="overview"></a>Panoramica
Hello note sulla versione seguenti descrivono le nuove funzionalità di hello e identificare i problemi critici aperti di hello per StorSimple 8000 Series Update 3. Contengono inoltre un elenco degli aggiornamenti software di StorSimple hello inclusi in questa versione. 

È possibile dispositivo StorSimple tooany applicato in esecuzione Release (GA) o aggiornamento 0,1 tramite aggiornamento 2.2 Update 3. versione del dispositivo Hello associata a Update 3 è 6.3.9600.17759.

Esaminare informazioni hello contenute in versione di hello note prima di distribuire hello aggiornare nella soluzione StorSimple.

> [!IMPORTANT]
> * L'aggiornamento 3 include software per dispositivi, firmware e driver LSI e aggiornamenti Storport e Spaceport. Sono necessari circa 1,5-2 ore tooinstall questo aggiornamento. 
> * Per le nuove versioni, non sarà possibile visualizzare gli aggiornamenti immediatamente perché è un'implementazione graduale dei hello aggiornamenti. Attendere alcuni giorni e quindi provare a cercare nuovamente gli aggiornamenti, perché verranno presto resi disponibili.
> 
> 

## <a name="whats-new-in-update-3"></a>Novità dell'aggiornamento 3
Hello seguenti importanti miglioramenti e correzioni di bug sono state apportate in Update 3.

* **Automatico delle modifiche di recupero di spazio** : avvio di Update 3, algoritmi di recupero di spazio hello eseguire nel controller in standby hello del sistema hello risultante in un'esecuzione più rapida. Per ulteriori informazioni sulle porte hello toowork obbligatorio con recupero di spazio, fare riferimento toohello [StorSimple requisiti di rete](storsimple-system-requirements.md#networking-requirements-for-your-storsimple-device).
* **Miglioramenti delle prestazioni** – Update 3 sono state migliorate le prestazioni di lettura / scrittura toohello cloud.
* **Miglioramenti relativi alla migrazione** : In questa versione, alcune correzioni di bug e miglioramenti sono stati eseguiti per la funzionalità di migrazione hello da dispositivi della serie too8000 dispositivi serie 5000 o 7000. Per ulteriori informazioni su come toouse hello funzionalità di migrazione, visitare troppo[la migrazione da una serie 5000 o 7000 dispositivo too8000 serie dispositivo](https://gallery.technet.microsoft.com/Azure-StorSimple-50007000-c1a0460b). 
* **Correzioni relative a monitoraggio** : In questa versione, i bug correlati sono stati risolti toomonitoring grafici, dashboard del servizio e dashboard del dispositivo.

## <a name="issues-fixed-in-update-3"></a>Problemi risolti nell'aggiornamento 3
Hello le tabelle seguenti viene fornito un riepilogo dei problemi che sono stati risolti in Update 3.    

| No | Funzionalità | Problema | Si applica toophysical dispositivo | Si applica toovirtual dispositivo |
| --- | --- | --- | --- | --- |
| 1 |Migrazione dei dati lato host |In hello versione precedente, hello StorSimple Appliance di Cloud era in corso offline durante una migrazione dei dati sul lato host. Tale problema è stato corretto in questa versione. |No |Sì |
| 2 |Volumi aggiunti in locale |Nelle release precedenti hello, sono presenti problemi correlati tooI/O errori, errori di conversione volume ed errori relativo al percorso dati per i volumi aggiunti in locale. In questa versione i problemi sono stati corretti una volta individuata la causa radice. |Sì |No |
| 3 |Monitoraggio |Si sono verificati più unità tooreporting correlati di problemi e monitoraggio oltre a grafici dashboard del dispositivo in cui è state visualizzate informazioni non corrette per localmente bloccato volumi. Tali problemi sono stati risolti in questa versione. |Sì |No |
| 4 |I/O a scrittura intensiva |Quando si utilizza StorSimple per carichi di lavoro che includono operazioni di scrittura pesanti, utente hello verrebbe eseguito in un bug poco frequente in hello working set è la suddivisione in livelli nel cloud hello. Tale bug è stato risolto in questa versione. |Sì |Sì |
| 5 |Backup |In alcuni casi rari, nelle versioni precedenti di hello del software, quando l'utente ha eseguito un backup di un clone remoto, eseguono errori cloud e operazione hello verrebbe generato un errore. In questa versione, problema hello e hello operazione ha esito positivo. |Sì |Sì |
| 6 |Criterio di backup |In alcuni rari casi, in hello versioni precedenti del software, si è verificato un errore correlato toohello l'eliminazione del criterio di backup. Tale problema è stato corretto in questa versione. |Sì |Sì |

## <a name="known-issues-in-update-3"></a>Problemi noti nell'aggiornamento 3
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
| 20 |Volumi aggiunti in locale |Se si tenta di tooconvert un volume a livelli (creato e duplicato con aggiornamento 1.2 o versioni precedente) tooa localmente bloccato volume e il dispositivo sta esaurendo lo spazio o si verifica un'interruzione di cloud, quindi hello clone(s) potrebbe essere danneggiata. |Questo problema si verifica solo con i volumi che sono stati creati e clonati con software precedente all'aggiornamento 2.1. Si tratta di uno scenario poco frequente. | | |
| 21 |Conversione del volume |Non aggiornare hello ACR tooa collegato volume durante una conversione del volume è in corso (a più livelli toolocally bloccato o viceversa). Aggiornamento hello ACR potrebbe causare il danneggiamento dei dati. |Se necessario, aggiornare conversione del volume hello ACR toohello precedenti e non apportare ulteriori aggiornamenti ACR durante la conversione di hello è in corso. | | |
| 22 |Aggiornamenti |Quando si applica l'aggiornamento 3, hello **manutenzione** pagina hello Azure verrà portale classico seguente hello di visualizzazione dei messaggi correlati tooUpdate 2 - "serie StorSimple 8000 aggiornamento 2 include il possibilità hello per raccogliere tooproactively Microsoft registrare le informazioni dal dispositivo quando vengono rilevati problemi potenziali". Questo è fuorviante in quanto indica che il dispositivo hello viene aggiornato tooUpdate 2. Dopo aver aggiornato succeesfully tooUpdate 3 dispositivo hello, il messaggio verrà rimosso. |Questo comportamento verrà risolto in una versione futura. |Sì |No |

## <a name="controller-and-firmware-updates-in-update-3"></a>Aggiornamenti firmware e controller presenti nell'aggiornamento 3
Questa versione dispone degli aggiornamenti del firmware e del driver LSI. Per ulteriori informazioni su come tooinstall hello LSI aggiornamenti di driver e firmware, vedere [installare Update 3](storsimple-install-update-3.md) nel dispositivo StorSimple.

## <a name="virtual-device-updates-in-update-3"></a>Aggiornamenti del dispositivo virtuale nell'aggiornamento 3
Questo aggiornamento non può essere applicato toohello StorSimple Appliance di Cloud (noto anche come hello dispositivo virtuale). Nuovi dispositivi virtuali saranno necessario toobe creato. 

## <a name="next-step"></a>Passaggio successivo
Informazioni su come troppo[installare Update 3](storsimple-install-update-3.md) nel dispositivo StorSimple.


---
title: note sulla versione di 2.2 aggiornamento serie 8000 aaaStorSimple | Documenti Microsoft
description: "Descrive le nuove funzionalità hello, problemi e soluzioni alternative per StorSimple 8000 Series aggiornamento 2.2."
services: storsimple
documentationcenter: NA
author: alkohli
manager: carmonm
editor: 
ms.assetid: 5cf03ea8-2a0f-4552-b6dc-7ea517783d7b
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: TBD
ms.date: 07/18/2016
ms.author: alkohli
ms.openlocfilehash: a2902126f4011fa9ade64f63a8abdec095874fb1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="storsimple-8000-series-update-22-release-notes"></a>Note sulla versione dell'aggiornamento 2.2 di StorSimple serie 8000
## <a name="overview"></a>Panoramica
Hello note sulla versione seguenti descrivono le nuove funzionalità di hello e identificare i problemi critici aperti di hello per StorSimple 8000 Series aggiornamento 2.2. Contengono inoltre un elenco degli aggiornamenti software di StorSimple hello inclusi in questa versione. 

Aggiornamento 2.2 può essere applicato tooany StorSimple dispositivo esecuzione versione (GA) o aggiornamento 0,1 tramite Update 2.1. versione del dispositivo Hello associato aggiornamento 2.2 è 6.3.9600.17708.

Esaminare informazioni hello contenute in versione di hello note prima di distribuire hello aggiornare nella soluzione StorSimple.

> [!IMPORTANT]
> * L'aggiornamento 2.2 include aggiornamenti solo per il software. Sono necessari circa 1,5-2 ore tooinstall questo aggiornamento. 
> * Se si esegue ancora l'aggiornamento 2.1, si consiglia di applicare l'aggiornamento 2.2 appena possibile.
> * Per le nuove versioni, non sarà possibile visualizzare gli aggiornamenti immediatamente perché è un'implementazione graduale dei hello aggiornamenti. Attendere alcuni giorni e quindi provare a cercare nuovamente gli aggiornamenti, perché verranno presto resi disponibili.
> 
> 

## <a name="whats-new-in-update-22"></a>Novità dell'aggiornamento 2.2
Hello seguenti chiavi sono stati apportati miglioramenti 2.2 di aggiornamento.

* **Ottimizzazione dello spazio di recupero automatico** : quando vengono eliminati dati in volumi con thin provisioning, blocchi di archiviazione inutilizzato hello necessario toobe recuperato. Questa versione dispone del processo di recupero dello spazio hello migliorate dal cloud hello risultante in hello inutilizzato spazio diventa disponibile più rapidamente rispetto a come toohello le versioni precedenti.
* **Miglioramenti delle prestazioni per gli snapshot** – 2.2 aggiornamento ha tooprocess ora migliorate hello uno snapshot nel cloud in determinati scenari dove vengono utilizzati i volumi di grandi dimensioni ed è presente una varianza dati toono minimo. Uno scenario che può costituire un vantaggio da questa funzionalità avanzata sarebbe volumi di archiviazione hello.
* **Protezione avanzata del pacchetto di supporto di raccolta** : è stato migliorato in modo hello pacchetto per il supporto hello verrà raccolte e caricato in questa versione. 
* **Miglioramenti per l'affidabilità degli aggiornamenti** : questa versione include correzioni di bug che consentono di ottenere un incremento dell'affidabilità degli aggiornamenti.

## <a name="issues-fixed-in-update-22"></a>Problemi risolti nell'aggiornamento 2.2
Hello le tabelle seguenti viene fornito un riepilogo dei problemi che sono stati risolti in aggiornamenti 2.2 e 2.1.    

| No | Funzionalità | Problema | Si applica toophysical dispositivo | Si applica toovirtual dispositivo |
| --- | --- | --- | --- | --- |
| 1 |Prestazioni dell'host |Hello precedente versione, i problemi di prestazioni sul lato host sono stati rilevati durante la creazione di un volume aggiunto in locale hello e durante la conversione di un tooa volume a livelli localmente hello bloccato volume. In questa versione, determinando così un miglioramento delle prestazioni di host hello durante le procedure di creazione e la conversione di volume hello risolto questi problemi. |Sì |No |
| 2 |Volumi aggiunti in locale |In rari casi, sistema hello potrebbe bloccarsi durante la creazione di un volume aggiunto in locale. Tale bug è stato risolto in questa versione. |Sì |No |
| 3 |Suddivisione in livelli |Quando i metadati di hello per hello dispositivi Cloud StorSimple (8010: spazio e 8020) a più livelli hello troppo cloud si sono verificati sporadici arresti anomali del sistema. Tale problema è stato corretto in questa versione. |No |Sì |
| 4 |Creazione di snapshot |Si sono verificati problemi correlati toohello creazione di snapshot incrementali in scenari con volumi di grandi dimensioni e varianza dei dati toono minimo. Tali problemi sono stati risolti in questa versione. |Sì |Sì |
| 5 |Autenticazione Openstack |Quando si utilizza Openstack come provider di servizi cloud hello, utente hello verrebbe eseguito in un'autenticazione toohello correlati bug poco frequenti in cui parser JSON hello ha restituito un arresto anomalo. Tale bug è stato risolto in questa versione. |Sì |No |
| 6 |Copia lato host |Nelle versioni precedenti del software, un bug poco frequente correlate temporizzazione ODX toohello è stata individuata la copia di dati di hello dal volume tooanother un volume. In questo modo, un failover del controller e il sistema hello potrebbe superare la modalità di ripristino. Il bug è stato risolto in questa versione. |sì |No |
| 7 |Strumentazione gestione Windows (WMI) |Nelle versioni precedenti di hello del software, sono presenti più istanze di un errore di proxy web con l'eccezione hello "<ManagementException> errore nel caricamento". Questo bug è stato attribuito tooa perdita di memoria WMI ed è stato ora corretto. |Sì |No |
| 8 |Aggiornare |In alcuni casi rari, nelle versioni precedenti di hello del software, utente hello ha ricevuto un "CisPowershellHcsscripterror" durante il tentativo di tooscan o installare gli aggiornamenti. Tale problema è stato corretto in questa versione. |Sì |Sì |
| 9 |Pacchetto di supporto |In questa versione, è stato migliorato toohello modo il pacchetto di supporto hello verrà raccolte e caricato. |Sì |Sì |

## <a name="known-issues-in-update-22"></a>Problemi noti nell'aggiornamento 2.2
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

## <a name="controller-and-firmware-updates-in-update-22"></a>Aggiornamenti firmware e controller presenti nell'aggiornamento 2.2
Questa versione include aggiornamenti solo per il software. Tuttavia, se si sta aggiornando un tooUpdate precedente versione 2, è necessario tooinstall driver Storport, Spaceport e (in alcuni casi) disco aggiornamenti del firmware sul dispositivo.

Per ulteriori informazioni su driver hello tooinstall, Storport, Spaceport e aggiornamenti del firmware del disco, vedere [installare aggiornamento 2.2](storsimple-install-update-21.md) nel dispositivo StorSimple.

## <a name="virtual-device-updates-in-update-22"></a>Aggiornamenti del dispositivo virtuale nell'aggiornamento 2.2
Questo aggiornamento non può essere applicato toohello dispositivo virtuale. Nuovi dispositivi virtuali saranno necessario toobe creato. 

## <a name="next-step"></a>Passaggio successivo
Informazioni su come troppo[installare aggiornamento 2.2](storsimple-install-update-21.md) nel dispositivo StorSimple.


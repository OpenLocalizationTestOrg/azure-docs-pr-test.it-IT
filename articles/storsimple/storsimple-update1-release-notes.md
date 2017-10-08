---
title: note sulla versione di aggiornamento serie 1.2 aaaStorSimple 8000 | Documenti Microsoft
description: "Descrive le nuove funzionalità hello, problemi e soluzioni alternative per StorSimple 8000 Series aggiornamento 1.2."
services: storsimple
documentationcenter: NA
author: alkohli
manager: timlt
editor: 
ms.assetid: 6c9aae87-6f77-44b8-b7fa-ebbdc9d8517c
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: TBD
ms.date: 02/27/2017
ms.author: alkohli
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 7f564b794573fc3302ab15732e8dd85632ab9243
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="update-12-release-notes-for-your-storsimple-8000-series-device"></a>Note sulla versione dell'aggiornamento 1.2 del dispositivo StorSimple serie 8000

## <a name="overview"></a>Panoramica
Hello note sulla versione seguenti descrivono le nuove funzionalità di hello e identificare i problemi critici aperti di hello per StorSimple 8000 Series aggiornamento 1.2. Contengono inoltre un elenco di software di StorSimple hello, driver e aggiornamenti del firmware del disco inclusi in questa versione. 

Aggiornamento 1.2 può essere dispositivo StorSimple tooany applicato in esecuzione Release (GA), aggiornamento 0,1, aggiornamento 0,2 o 0,3 di aggiornamento software. L’aggiornamento 1.2 non è disponibile se il dispositivo esegue l’aggiornamento 1 o 1.1. Se il dispositivo è in esecuzione Release (GA), [contattare il supporto Microsoft](storsimple-contact-microsoft-support.md) tooassist è l'installazione dell'aggiornamento.

Hello nella seguente tabella elenca hello dispositivo versioni del software corrispondente tooUpdates 1, 1.1 e 1.2.

| Se si esegue l’aggiornamento... | questa è la versione del software del dispositivo. |
| --- | --- |
| Aggiornamento 1.2 |6.3.9600.17584 |
| Aggiornamento 1.1 |6.3.9600.17521 |
| Aggiornamento 1.0 |6.3.9600.17491 |

Esaminare informazioni hello contenute in versione di hello note prima di distribuire hello aggiornare nella soluzione StorSimple. Per ulteriori informazioni, vedere come troppo[installare Aggiornamento 1.2 nel dispositivo StorSimple](storsimple-install-update-1.md). 

> [!IMPORTANT]
> * Sono necessari circa 5-10 ore tooinstall questo aggiornamento (inclusi gli aggiornamenti di Windows hello). 
> * L’aggiornamento 1.2 dispone di aggiornamenti del software, del driver LSI e del firmware del disco. tooinstall, seguire le istruzioni di hello in [installare Aggiornamento 1.2 nel dispositivo StorSimple](storsimple-install-update-1.md).
> * Per le nuove versioni, non sarà possibile visualizzare gli aggiornamenti immediatamente perché è un'implementazione graduale dei hello aggiornamenti. Provare a cercare nuovamente gli aggiornamenti dopo qualche giorno perché verranno presto resi disponibili.
> 
> 

## <a name="whats-new-in-update-12"></a>Novità dell'aggiornamento 1.2
Queste funzionalità sono state rilasciate inizialmente con Update 1 che è stata effettuata tooa disponibili limitato set di utenti. Con la versione di hello 1.2 di aggiornamento, la maggior parte degli utenti di StorSimple hello vedrà hello seguenti miglioramenti e nuove funzionalità:

* **Migrazione da dispositivi della serie 5000 7000 serie too8000** : questa versione introduce una nuova funzionalità di migrazione che consente di hello StorSimple 5000 7000 series appliance utenti toomigrate i dispositivi della serie tooa StorSimple 8000 dati fisici o dispositivo virtuale. funzionalità di migrazione Hello presenta due proposte di valore di chiave:                                                                  
  
  * **Continuità aziendale**, abilitando la migrazione dei dati esistenti nei dispositivi di 5000 7000 serie accessori too8000 serie.
  * **Migliorate offerte funzionalità dei dispositivi serie 8000 hello**, ad esempio efficiente gestione centralizzata di più dispositivi attraverso il servizio StorSimple Manager, una migliore classe di hardware e aggiornamento del firmware, dispositivi di rete, mobilità dei dati, e funzionalità in progetti futuri hello.
    
    Fare riferimento toohello [Guida alla migrazione](http://www.microsoft.com/download/details.aspx?id=47322) per informazioni dettagliate su come un dispositivo di serie 5000 7000 StorSimple serie 8000 tooan toomigrate. 
* **Disponibilità nel portale di Azure per enti pubblici hello** – StorSimple è ora disponibile nel portale di Azure per enti pubblici hello. Vedere come troppo[la distribuzione di un dispositivo StorSimple nel portale di Azure per enti pubblici hello](storsimple-deployment-walkthrough-gov.md).
* **Supporto per altri provider di servizi cloud** : hello altri provider di servizi cloud supportati sono S3 Amazon, Amazon S3 con record di risorse, HP e OpenStack (beta).
* **Aggiornare le API di archiviazione toolatest** : con questa versione, StorSimple è stato aggiornato il servizio di archiviazione di Azure più recente toohello API. Dispositivi della serie StorSimple 8000 che eseguono versioni del software pre-aggiornamento 1 (versione 0,1, 0,2 e 0,3) utilizzano versioni di hello API del Servizio archiviazione di Azure più vecchi di 17 luglio 2009. Come indicato nella hello aggiornato [annuncio sulla rimozione delle versioni del servizio di archiviazione](http://blogs.msdn.com/b/windowsazurestorage/archive/2015/10/19/microsoft-azure-storage-service-version-removal-update-extension-to-2016.aspx), da 1 agosto 2016, queste API verranno deprecate. È essenziale applicare tooAugust precedente hello StorSimple 8000 Series Update 1 1, 2016. Se non si toodo pertanto, i dispositivi StorSimple verranno smettere di funzionare correttamente.
* **Supporto per la zona ridondanti archiviazione zona** – con hello toohello aggiornamento più recente di hello API di archiviazione, serie StorSimple 8000 hello supporteranno zona ridondanti archiviazione (ZRS) in aggiunta tooLocally archiviazione ridondante (LRS) e con ridondanza geografica Archiviazione (GRS). Fare riferimento toothis [articolo sulle opzioni di ridondanza di archiviazione di Azure](../storage/common/storage-redundancy.md) per i dettagli di ridondanza della zona.
* **Migliorata l'esperienza di distribuzione e l'aggiornamento iniziale** : In questa versione, hello installazione e i processi di aggiornamento sono stati migliorati. installazione di Hello tramite installazione guidata di hello è utente toohello commenti e suggerimenti di miglioramento tooprovide se impostazioni di configurazione e del firewall di rete hello non sono corrette. Altri cmdlet di diagnostica sono stati forniti toohelp è la risoluzione dei problemi di rete del dispositivo hello. Vedere hello [risoluzione dei problemi di articolo distribuzione](storsimple-troubleshoot-deployment.md) per ulteriori informazioni su hello nuovi cmdlet di diagnostica utilizzato per la risoluzione dei problemi.

## <a name="issues-fixed-in-update-12"></a>Problemi risolti nell'aggiornamento 1.2
Hello nella tabella seguente fornisce un riepilogo dei problemi che sono stati risolti in aggiornamenti 1, 1.1 e 1.2.    

| No. | Funzionalità | Problema | Risolto nell'aggiornamento | Si applica toophysical dispositivo | Si applica toovirtual dispositivo |
| --- | --- | --- | --- | --- | --- |
| 1 |Windows PowerShell per StorSimple  |Quando un utente di accedere in modalità remota al dispositivo StorSimple hello tramite Windows PowerShell per StorSimple e quindi avviata l'installazione guidata di hello, un arresto anomalo appena Data 0 è stato immesso IP. Nell'aggiornamento 1, questo bug è stato corretto. |Aggiornamento 1 |Sì |Sì |
| 2 |Ripristino delle impostazioni predefinite |In alcuni casi, quando si esegue un ripristino delle impostazioni predefinite, il dispositivo di StorSimple hello è diventato bloccarsi e visualizzato questo messaggio: **reimpostazione toofactory è in corso (fase 8)**. Ciò avviene se si preme CTRL + C mentre hello cmdlet è in corso. Il bug è stato corretto. |Aggiornamento 1 |Sì |No |
| 3 |Ripristino delle impostazioni predefinite |Dopo la reimpostazione di una factory di entrambi i controller non riuscito, era possibile tooproceed con la registrazione del dispositivo. Ciò determinava una configurazione di sistema non supportata. Nell'aggiornamento 1, viene visualizzato un messaggio di errore e la registrazione è bloccata su un dispositivo in cui il ripristino delle impostazioni predefinite non è riuscito. |Aggiornamento 1 |Sì |No |
| 4 |Ripristino delle impostazioni predefinite |In alcuni casi, sono stati generati avvisi falsi positivi di mancata corrispondenza. Sui dispositivi che eseguono l'aggiornamento 1 non verranno più generati avvisi di mancata corrispondenza non corretti. |Aggiornamento 1 |Sì |No |
| 5 |Ripristino delle impostazioni predefinite |Se è stata interrotta ripristino delle impostazioni predefinite precedenti toocompletion, hello modalità di ripristino del dispositivo immesso e non consente tooaccess Windows PowerShell per StorSimple. Il bug è stato corretto. |Aggiornamento 1 |Sì |No |
| 6 |Ripristino di emergenza |È stato corretto un bug di ripristino di emergenza di emergenza in cui ripristino di emergenza avrà esito negativo durante l'individuazione di hello di backup nel dispositivo di destinazione hello. |Aggiornamento 1 |Sì |Sì |
| 7 |LED di monitoraggio |In alcuni casi, il monitoraggio LED hello parte posteriore dell'accessorio non indica lo stato corretto. LED blu Hello è stato disattivato. I LED DATA 0 e 1 lampeggiavano anche quando le interfacce non erano configurate. è stato risolto il problema di Hello e LED di monitoraggio ora allo stato hello corretto. |Aggiornamento 1 |Sì |No |
| 8 |LED di monitoraggio |In alcuni casi, dopo aver applicato l'aggiornamento 1, luce hello blu nel controller attivo hello disattivato rendendo controller attivo di disco rigido tooidentify hello. Questo problema è stato risolto in questa versione patch. |Aggiornamento 1.2 |Sì |No |
| 9 |Interfacce di rete |Nelle versioni precedenti, un dispositivo StorSimple configurato con un gateway non indirizzabile poteva disconnettersi. In questa versione, metrica di routing hello per Data 0 è diventato hello più basso; Pertanto, anche se altre interfacce di rete abilitata per il cloud, tutto il traffico cloud hello dal dispositivo hello verrà indirizzato tramite Data 0. |Aggiornamento 1 |Sì |Sì |
| 10 |Backup |Un bug nell'aggiornamento 1 che ha causato toofail backup dopo 24 giorni è stato risolto in patch hello versione 1.1 di aggiornamento. |Aggiornamento 1.1 |Sì |Sì |
| 11 |Backup |Un bug nelle versioni precedenti che comprometteva le prestazioni degli snapshot cloud con bassi tassi di cambio. Questo bug è stato risolto in questa versione patch. |Aggiornamento 1.2 |Sì |Sì |
| 12 |Aggiornamenti |Un bug nell'aggiornamento 1 che ha segnalato un aggiornamento non riuscito e ha causato toogo controller hello in modalità di ripristino, è stato risolto in questa versione di patch. |Aggiornamento 1.2 |Sì |Sì |

## <a name="known-issues-in-update-12"></a>Problemi noti nell'aggiornamento 1.2
Hello nella tabella seguente fornisce un riepilogo dei problemi noti in questa versione.

| No. | Funzionalità | Problema | Commenti/Soluzione alternativa | Si applica toophysical dispositivo | Si applica toovirtual dispositivo |
| --- | --- | --- | --- | --- | --- |
| 1 |Quorum disco |In rari casi, se la maggior parte hello dei dischi nell'enclosure EBOD hello di un dispositivo 8600 si disconnette e il quorum dischi non è disponibile, quindi il pool di archiviazione hello sarà offline. E rimarrà offline anche se hello dischi vengono riconnessi. |Sarà necessario dispositivo hello tooreboot. Se hello problema persiste, contattare il supporto Microsoft per i passaggi successivi. |Sì |No |
| 2 |ID controller non corretto |Quando viene eseguita la sostituzione di un controller, il controller 0 potrebbe essere visualizzato come controller 1. Durante la sostituzione del controller, quando hello immagine viene caricata dal nodo peer hello, ID controller hello è inoltre possibile scaricare inizialmente come ID del controller peer hello In rari casi, questo comportamento può verificarsi anche dopo un riavvio del sistema. |Non è necessaria alcuna azione da parte dell’utente. Questa situazione si risolverà da solo dopo la sostituzione dei controller hello è stata completata. |Sì |No |
| 3 |Account di archiviazione |Utilizzando l'account di archiviazione di hello toodelete servizio di archiviazione hello è uno scenario non supportato. Questo conduce tooa situazione in cui non è possibile recuperare i dati utente. |Sì |Sì | |
| 4 |Failover del dispositivo |Failover multipli di un contenitore del volume da hello dispositivi di destinazione toodifferent origine dispositivo stesso non è supportata. Failover del dispositivo da un singolo messaggi non recapitabili toomultiple dispositivi renderà i contenitori di volumi hello nel primo dispositivo sottoposto a failover hello perdere la proprietà dei dati. Dopo un failover, questi contenitori di volumi o di un comportamento diverso quando vengono visualizzati nel portale di Azure classico hello. | |Sì |No |
| 5 |Installazione |Durante l'adattatore StorSimple per l'installazione di SharePoint, è necessario tooprovide IP di un dispositivo affinché hello installazione toofinish correttamente. | |Sì |No |
| 6 |Proxy Web |Se la configurazione del proxy web è HTTPS come hello specificato protocollo, la comunicazione del dispositivo al servizio ne risentirà e dispositivo hello passerà alla modalità offline. Verranno inoltre generati pacchetti di supporto nel processo di hello, usando risorse significative sul dispositivo. |Verificare che URL del proxy web hello disponga di HTTP hello protocollo specificato. Per ulteriori informazioni, visitare troppo[configurare il proxy web per il dispositivo](storsimple-configure-web-proxy.md). |Sì |No |
| 7 |Proxy Web |Se si configurano e abilitare il proxy web su un dispositivo registrato, è necessario controller attivo di hello toorestart sul dispositivo. | |Sì |No |
| 8 |Elevata latenza del cloud ed elevato carico di lavoro I/O |Quando il dispositivo StorSimple rileva una combinazione di cloud ad alta latenza (ordine di secondi) e un elevato carico di lavoro dei / o, i volumi del dispositivo hello entrano in uno stato danneggiato e hello i/o potrebbe verificarsi un errore "dispositivo non pronto". |Si verrà necessario controller del dispositivo toomanually riavvio hello o eseguire un toorecover di failover del dispositivo da questa situazione. |Sì |No |
| 9 |Azure PowerShell |Quando si usa il cmdlet di StorSimple hello **Get AzureStorSimpleStorageAccountCredential &#124; Select-Object - Wait prima 1 -** tooselect hello primo oggetto in modo che è possibile creare un nuovo **VolumeContainer** oggetto hello cmdlet restituisce tutti gli oggetti di hello. |Eseguire il wrapping hello cmdlet tra parentesi, come indicato di seguito: **(Get-Azure-StorSimpleStorageAccountCredential) &#124; Select-Object - Wait prima 1 -** |Sì |Sì |
| 10 |Migrazione |Quando più contenitori di volumi vengono passati per la migrazione, hello greco per il backup più recente è preciso solo per il primo contenitore di volume hello. Inoltre, la migrazione parallela inizierà dopo hello backup primi 4 hello primo contenitore del volume viene eseguita la migrazione. |Si consiglia di migrare un contenitore del volume alla volta. |Sì |No |
| 11 |Migrazione |Dopo il ripristino di hello, i volumi non vengono aggiunti toohello backup hello o criteri di gruppo del disco virtuale. |È necessario tooadd questi volumi tooa dei criteri di backup nei backup toocreate ordine. |Sì |Sì |
| 12 |Migrazione |Al termine della migrazione hello, non devono accedere a dispositivi serie 5000 o 7000 hello hello eseguita la migrazione di contenitori di dati. |È consigliabile eliminare hello che la migrazione di contenitori di dati dopo la migrazione di hello completo viene eseguito il commit. |Sì |No |
| 13 |Clonazione e ripristino di emergenza |Un dispositivo StorSimple esegue Update 1 non è possibile clonare o eseguire il ripristino di emergenza tooa dispositivo che esegue pre-aggiornamento 1. |Sarà necessario tooupdate hello destinazione dispositivo tooUpdate 1 tooallow queste operazioni |Sì |Sì |
| 14 |Migrazione |La configurazione del backup per la migrazione potrebbe non riuscire in un dispositivo di serie 5000-7000 quando sono presenti gruppi di volumi senza volumi associati. |Eliminare tutti i gruppi di volumi vuoto hello con associato alcun volume, quindi ripetere il backup di configurazione hello. |Sì |No |

## <a name="physical-device-updates-in-update-12"></a>Aggiornamenti del dispositivo fisico nell'aggiornamento 1.2
Se l'aggiornamento patch 1.2 è applicato tooa dispositivo fisico (in esecuzione versioni precedenti tooUpdate 1), versione del software hello cambierà too6.3.9600.17584.

## <a name="controller-and-firmware-updates-in-update-12"></a>Aggiornamenti firmware e controller presenti nell'aggiornamento 1.2
Questa versione Aggiorna driver hello e il firmware del disco hello sul dispositivo.

* Per ulteriori informazioni sull'aggiornamento del controller SAS hello, vedere [aggiornamento 1 per controller SAS LSI nel dispositivo Microsoft Azure StorSimple](https://support.microsoft.com/kb/3043005). 
* Per ulteriori informazioni sull'aggiornamento del firmware di hello disco, vedere [1 aggiornamento firmware del disco per il dispositivo StorSimple di Microsoft Azure](https://support.microsoft.com/kb/3063416).

## <a name="virtual-device-updates-in-update-12"></a>Aggiornamenti del dispositivo virtuale nell'aggiornamento 1.2
Questo aggiornamento non può essere applicato toohello dispositivo virtuale. Nuovi dispositivi virtuali saranno necessario toobe creato. 

## <a name="next-steps"></a>Passaggi successivi
* [Installare l'aggiornamento 1.2 nel dispositivo](storsimple-install-update-1.md).


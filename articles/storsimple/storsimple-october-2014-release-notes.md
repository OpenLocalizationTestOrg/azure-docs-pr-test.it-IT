---
title: aaaStorSimple 8000 aggiornamento 0,1 note sulla versione | Documenti Microsoft
description: "Vengono descritte le nuove funzionalità hello e correzioni di problemi aperti e disponibili soluzioni alternative per hello ottobre 2014 versione di Microsoft Azure StorSimple (aggiornamento 0,1)."
services: storsimple
documentationcenter: NA
author: alkohli
manager: carmonm
editor: 
ms.assetid: fd35e3c3-4770-460c-999d-f72ab7053a20
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: TBD
ms.date: 09/21/2016
ms.author: alkohli
ms.openlocfilehash: 684e31cb0b356ec59a9d6c245e5d2bc062cc4f0d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="storsimple-8000-series-update-01-release-notes--october-2014"></a>Note sulla versione dell'aggiornamento 0.1 di StorSimple serie 8000 - Ottobre 2014
## <a name="overview"></a>Panoramica
Hello seguenti note sulla versione di identifica problemi critici aperti di hello per l'aggiornamento di serie StorSimple 8000 0,1 rilasciato in ottobre 2014. Contengono inoltre un elenco di hello StorSimple software e aggiornamenti del firmware inclusi in questa versione. Questo è hello primo rilascio dopo hello StorSimple 8000 Series versione è stata effettuata in genere disponibili nel luglio 2014 e corrisponde toosoftware versione 6.3.9600.17312.  

Si consiglia di cercare e applicare eventuali aggiornamenti disponibili immediatamente dopo aver installato la periferica hello. È anche possibile attivare toodownload aggiornamenti automatici e installare gli aggiornamenti ad alta priorità da Microsoft, non appena vengono rilasciate. Per ulteriori informazioni, vedere come troppo[aggiornare il dispositivo StorSimple](storsimple-update-device.md).  

Esaminare hello informazioni contenute nelle note sulla versione di hello prima di distribuire gli aggiornamenti di hello nella soluzione StorSimple.  

> [!IMPORTANT]
> * Usare servizio StorSimple Manager hello e non di Windows PowerShell per StorSimple tooinstall hello che degli aggiornamenti di ottobre.  
> * gli aggiornamenti di Hello in genere richiedono circa 3 ore toocomplete.  
> * Hello versione di ottobre di StorSimple non contiene alcun dispositivo virtuale di aggiornamenti toohello StorSimple. È comunque possibile applicare eventuali aggiornamenti disponibili di Windows, inclusi i recenti aggiornamenti per la sicurezza, ma non si noterà una modifica nella versione per il dispositivo virtuale hello.  
> 
> 

Verificare che hello seguenti prerequisiti sono soddisfatto tooupdating precedente del dispositivo StorSimple.  

* Assicurarsi che entrambi i controller di dispositivo siano in esecuzione prima di cercare nuovi aggiornamenti. Se dei controller non è in esecuzione, l'analisi di hello avrà esito negativo. tooverify che hello controller sono in uno stato integro, passare troppo**stato Hardware** in hello **manutenzione** pagina. Se vi sono componenti di tipo **Richiesta attenzione**, contattare il supporto tecnico Microsoft prima di continuare.  
* Verificare che gli indirizzi IP fissi per Controller 0 e Controller 1 siano instradabili e possono connettersi toohello Internet quando questi vengono usati per gestire i dispositivi di hello aggiornamenti toohello. È possibile utilizzare hello [cmdlet Test-Connection](https://technet.microsoft.com/library/hh849808.aspx) tooping un indirizzo noto esterno rete hello, ad esempio outlook.com, tooverify che hello controller dispone di connettività toohello all'esterno di rete.  
* Verificare che hello richiesti porte in uscita sono disponibili nel dispositivo StorSimple per le comunicazioni in uscita. Per ulteriori informazioni, vedere hello [requisiti di rete per il dispositivo StorSimple](storsimple-system-requirements.md#networking-requirements-for-your-storsimple-device).  
* Se versione software del dispositivo hello è antecedente a 6.3.9600.17312 (aggiornamento di ottobre 2014), disabilitare le porte Data 2 e Data 3 hello, se abilitate, prima di avviare l'aggiornamento di hello. Se si lasciano hello Data 2 o Data 3 abilitate quando si applica l'aggiornamento di hello le porte, potrebbe causare il toogo di controller di dispositivo in modalità di ripristino. Si noti che quando si disabilitano le interfacce di rete hello, tutti i volumi di hello associata verranno reso offline e hello i/o potrebbero essere compromesse per durata hello dell'aggiornamento di hello.  

## <a name="whats-new-in-hello-october-release"></a>Novità nella versione di ottobre hello
Questo aggiornamento include hello seguenti miglioramenti:

* È ora possibile utilizzare toomanage dell'interfaccia utente del servizio StorSimple Manager di hello ai controller dei dispositivi. Hello operazioni di gestione includono riavvio, l'arresto o attivare un controller. Per ulteriori informazioni, visitare troppo[controller del dispositivo StorSimple gestire](storsimple-manage-device-controller.md).  
* È possibile pianificare l'allocazione della larghezza di banda WAN in base a combinazioni tooday della settimana e ora del giorno. In questo modo toomake migliorare l'utilizzo della larghezza di banda WAN durante le fasce orarie. Per diversi contenitori di volume, sono consentiti diversi modelli di larghezza di banda. Per ulteriori informazioni, visitare troppo[gestire i modelli di larghezza di banda StorSimple](storsimple-manage-bandwidth-templates.md).  
* È possibile configurare notifiche tramite posta elettronica tooproactively avvisare hello amministratori e altri utenti dei problemi esistenti o forse imminenti. Per ulteriori informazioni, visitare troppo[configurare le impostazioni degli avvisi](storsimple-manage-alerts.md#configure-alert-settings).  

## <a name="issues-fixed-in-hello-october-release"></a>Problemi risolti nella versione di ottobre hello
Hello nella tabella seguente fornisce un riepilogo dei problemi che sono stati risolti in questo aggiornamento.  

| No. | Funzionalità | Problema | Si applica toophysical dispositivo | Si applica toovirtual dispositivo |
| --- | --- | --- | --- | --- |
| 1 |Interfacce di rete |In hello precedente versione, le interfacce di rete hello DATA 2 e DATA 3 sono state scambiate nel software hello. Tale problema è stato risolto nel presente aggiornamento. Rimuovere le impostazioni di hello e disabilitare queste interfacce di rete prima di installare l'aggiornamento di hello. Dopo aver installato l'aggiornamento di hello, sarà necessario tooreconfigure queste interfacce. |Sì |No |
| 2 |Pacchetto di supporto |Nella versione precedente di hello, se si esegue Windows PowerShell hello **Export-HcsSupportPackage** registra cmdlet tooretrieve hello Baseboard Management Controller (BMC), operazione hello non riuscita con hello seguente avviso: "hello operazione riuscita su questo controller, ma non sul controller peer hello scadenza toohello seguenti errori. Verificare che il peer hello sia integro e se il nodo corrente di hello può connettersi toohello peer." Questo problema ora è stato corretto. |Sì |No |
| 3 |Failover del dispositivo |Nella versione precedente di hello, c'era la possibilità di incoerenza dei dati se un **individuare il backup** processo non riuscito durante un failover del dispositivo. Questo problema ora è stato corretto. |Sì |No |
| 4 |Failover del dispositivo |Nella precedente hello versione, dopo un failover del dispositivo, i backup erano visibili, ma contenitore del volume associato hello non era presente sul dispositivo di destinazione hello. Questo problema ora è stato corretto. |Sì |No |
| 5 |Failover del dispositivo |Nella versione precedente di hello, si è verificato un bug nell'enumerazione hello di backup cloud durante l'operazione di ripristino del Registro di sistema hello avrebbe potuto causare un'incoerenza toodata se si sono verificati problemi di connettività sul cloud. |Sì |No |
| 6 |Aggiornamento del firmware |Nella versione precedente di hello, hello processo di aggiornamento del firmware dispositivo non riuscita e visualizzato un errore che informava che hello cmdlet non erano riconoscibili e che gli aggiornamenti di hello non riuscito di conseguenza. controller Hello entrava quindi in modalità di ripristino. Questo problema ora è stato corretto. |Sì |No |
| 7 |Installazione |Sono stati corretti gli errori causati da dispositivo hello Imaging errato durante l'installazione. |Sì |No |
| 8 |Ripristino delle impostazioni predefinite |Ora è possibile facoltativamente ignorare il controllo del firmware hello per la reimpostazione della factory. Si tratta di una modifica precedente versione di hello. |Sì |No |
| 9 |Ripristino delle impostazioni predefinite |Nella versione precedente di hello, durante l'esecuzione di un cmdlet di reimpostazione della factory, i controlli di versione del firmware venivano eseguiti solo per alcuni componenti hardware. Controlli del firmware aggiuntive sono stati apportati dopo il riavvio del primo hello in processo hello, che potrebbe causare toofail reimpostazione hello. Questa correzione assicura che tutti i controlli del firmware hello vengono effettuati quando hello factory reset cmdlet viene eseguito e prima di hello prima che il sistema riavviato. |Sì |No |
| 10 |Rotazione delle chiavi dell’account di archiviazione |Hello **Invoke-HcsmServiceDataEncryptionKeyChange** cmdlet utilizzato chiavi dell'account di archiviazione hello toorotate ora richieste hello utente tooenter hello chiave DEK del servizio. Si tratta di una modifica di versione precedente di hello in cui hello chiave DEK del servizio è stata passata come parametro incorporato. |Sì |No |
| 11 |Failback entro 24 ore |Durante il ripristino di emergenza, pulizia hello sul dispositivo di origine hello non sia stata eseguita correttamente e il failback toofail. Tale problema è stato risolto in questa versione. |Sì |No |

## <a name="known-issues-in-hello-october-release"></a>Problemi noti nella versione di ottobre hello
Hello nella tabella seguente fornisce un riepilogo dei problemi noti in questa versione.

| No. | Funzionalità | Problema | Commenti/Soluzione alternativa | Si applica toophysical dispositivo | Si applica toovirtual dispositivo |
| --- | --- | --- | --- | --- | --- |
| 1 |Ripristino delle impostazioni predefinite |In alcuni casi, quando si esegue un ripristino delle impostazioni predefinite, hello dispositivo StorSimple può bloccarsi e visualizzare questo messaggio: **reimpostazione toofactory è in corso (fase 8)**. Ciò avviene se si preme CTRL + C mentre hello cmdlet è in corso. |Non premere CTRL + C dopo l'avvio di un ripristino delle impostazioni predefinite. Se si è già in questo stato, contattare il supporto tecnico Microsoft per i passaggi successivi. |Sì |No |
| 2 |Ripristino delle impostazioni predefinite |Eseguire Ripristino impostazioni predefinite non di un dispositivo StorSimple aggiornato dalla versione 2014 tooOctober GA. |Questa operazione funziona solo se è installata una patch. Contattare il supporto Microsoft tooget questa patch obbligatoria. |Sì |No |
| 3 |Quorum disco |In rari casi, se la maggior parte hello dei dischi nell'enclosure EBOD hello di un dispositivo 8600 si disconnette e il quorum dischi non è disponibile, quindi il pool di archiviazione hello sarà offline. E rimarrà offline anche se hello dischi vengono riconnessi. |Sarà necessario dispositivo hello tooreboot. Se hello problema persiste, contattare il supporto Microsoft per i passaggi successivi. |Sì |No |
| 4 |Errori di snapshot nel cloud |In rari casi, uno snapshot nel cloud potrebbe non riuscire con l'errore hello **limite massimo di backup raggiunto**. Questo errore si verifica se si superano 255 cloni online sullo hello stesso dispositivo, da hello stesso volume originale eliminato. | |Sì |Sì |
| 5 |ID controller non corretto |Quando viene eseguita la sostituzione di un controller, il controller 0 potrebbe essere visualizzato come controller 1. Durante la sostituzione del controller, quando hello immagine viene caricata dal nodo peer hello, ID controller hello è inoltre possibile scaricare inizialmente come ID del controller peer hello In rari casi, questo comportamento può verificarsi anche dopo un riavvio del sistema. |Non è necessaria alcuna azione da parte dell’utente. Questa situazione si risolverà da solo dopo la sostituzione dei controller hello è stata completata. |Sì |No |
| 6 |Grafici di monitoraggio del dispositivo |Nel servizio StorSimple Manager hello, grafici di monitoraggio del dispositivo hello non funzionano quando base o l'autenticazione NTLM è abilitata nella configurazione del server proxy hello per dispositivo hello. |Modificare una configurazione del proxy web hello per hello dispositivo registrato con il servizio StorSimple Manager in modo che l'autenticazione è impostata tooNONE. toodo, hello hello eseguire Windows PowerShell per il cmdlet Set-HcsWebProxy di StorSimple. |Sì |Sì |
| 7 |Account di archiviazione |Utilizzando l'account di archiviazione di hello toodelete servizio di archiviazione hello è uno scenario non supportato. Questo conduce tooa situazione in cui non è possibile recuperare i dati utente. | |Sì |Sì |
| 8 |Failover del dispositivo |Failover multipli di un contenitore del volume da hello dispositivi di destinazione toodifferent origine dispositivo stesso non è supportata. |Il failover da un singolo messaggi non recapitabili toomultiple dispositivi renderà i contenitori di volumi hello nel primo dispositivo sottoposto a failover hello perdere la proprietà dei dati. Dopo un failover, questi contenitori di volumi o di un comportamento diverso quando vengono visualizzati nel portale di Azure classico hello. |Sì |No |
| 9 |Installazione |Durante l'adattatore StorSimple per l'installazione di SharePoint, è necessario tooprovide IP di un dispositivo affinché hello installazione toofinish correttamente. | |Sì |No |
| 10 |Proxy Web |Se la configurazione del proxy web è HTTPS come hello specificato protocollo, la comunicazione del dispositivo al servizio ne risentirà e dispositivo hello passerà alla modalità offline. Verranno inoltre generati pacchetti di supporto nel processo di hello, usando risorse significative sul dispositivo. |Verificare che URL del proxy web hello disponga di HTTP hello protocollo specificato. Ulteriori informazioni su come troppo[configurare il proxy web per il dispositivo](storsimple-configure-web-proxy.md). |Sì |No |
| 11 |Proxy Web |Se si configurano e abilitare il proxy web su un dispositivo registrato, è necessario controller attivo di hello toorestart sul dispositivo. | |Sì |No |
| 12 |Elevata latenza del cloud ed elevato carico di lavoro I/O |Quando il dispositivo StorSimple rileva una combinazione di cloud ad alta latenza (ordine di secondi) e un elevato carico di lavoro dei / o, i volumi del dispositivo hello entrano in uno stato danneggiato e hello i/o potrebbe verificarsi un errore "dispositivo non pronto". |Si verrà necessario controller del dispositivo toomanually riavvio hello o eseguire un toorecover di failover del dispositivo da questa situazione. |Sì |No |

## <a name="physical-device-updates-in-hello-october-release"></a>Aggiornamenti del dispositivo fisico nella versione di ottobre hello
Quando questi aggiornamenti vengono applicati tooa dispositivo fisico, versione del software hello passerà too6.3.9600.17312. Se non diversamente specificato, queste note sulla versione si applicano tooall modelli del dispositivo StorSimple hello. Per altre informazioni su tali aggiornamenti, vedere [Aggiornamento software del dispositivo fisico di ottobre 2014 per il dispositivo Microsoft Azure StorSimple](http://support.microsoft.com/kb/2986997).  

## <a name="serial-attached-scsi-sas-controller-and-firmware-updates-in-hello-october-release"></a>Serie-attached SCSI (SAS) controller e del firmware aggiornamenti nella versione di ottobre hello
Questa versione Aggiorna driver hello e firmware di hello sul controller SAS hello del dispositivo fisico. Per ulteriori informazioni sull'aggiornamento del controller SAS hello, vedere [aggiornamento di ottobre 2014 per controller SAS LSI nel dispositivo Microsoft Azure StorSimple](http://support.microsoft.com/kb/2987020).   

Questa versione applica anche un aggiornamento del firmware cumulativo che risolve i problemi di affidabilità con componenti hardware del dispositivo hello. Per ulteriori informazioni sull'aggiornamento del firmware hello, vedere [aggiornamento del firmware di ottobre 2014 per il dispositivo StorSimple di Microsoft Azure](http://support.microsoft.com/kb/2987015).  

## <a name="virtual-device-updates-in-hello-october-release"></a>Aggiornamenti del dispositivo virtuale in versione di ottobre hello
Questa versione non contiene tutti gli aggiornamenti per la periferica virtuale hello. Applicare questo aggiornamento, versione del software hello di un dispositivo virtuale non verrà modificato.


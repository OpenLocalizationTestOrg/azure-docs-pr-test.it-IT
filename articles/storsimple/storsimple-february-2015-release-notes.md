---
title: aaaStorSimple 8000 aggiornamento 0,3 note sulla versione | Documenti Microsoft
description: "Vengono descritte le nuove funzionalità hello e correzioni di problemi aperti e disponibili soluzioni alternative per hello febbraio 2015 release di Microsoft Azure StorSimple (aggiornamento 0.3)."
services: storsimple
documentationcenter: NA
author: SharS
manager: carmonm
editor: 
ms.assetid: b01bfd04-f9f8-45f4-ade8-95ac2b979e6a
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: TBD
ms.date: 04/18/2016
ms.author: v-sharos
ms.openlocfilehash: 53638f9d286b2085c6b45f9e3fae75c34fc73e7b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="storsimple-8000-series-update-03-release-notes---february-2015"></a>Note sulla versione dell'aggiornamento 0.3 di StorSimple serie 8000 - Febbraio 2015
## <a name="overview"></a>Panoramica
Hello seguenti note sulla versione di identifica i problemi critici aperti di hello per l'aggiornamento di serie StorSimple 8000 0,3 rilasciata nel febbraio 2015. Contengono inoltre un elenco di hello StorSimple software e aggiornamenti del firmware inclusi in questa versione. Si tratta di terza versione di hello dopo hello StorSimple 8000 Series versione è stata eseguita in genere disponibili nel luglio 2014.

Questo aggiornamento non modifica versione software del dispositivo hello dall'aggiornamento di gennaio hello. Continua toobe versione 6.3.9600.17312. È possibile verificare che gli aggiornamenti di hello sia stato installato controllando hello **ultimo aggiornamento** Data. Se data hello è 2/10/2015 o versione successiva, quindi che hello aggiornamento è stato installato correttamente.  

Si consiglia di cercare e installare eventuali aggiornamenti disponibili subito dopo l'installazione del dispositivo StorSimple. È anche possibile attivare toodownload aggiornamenti automatici e installare gli aggiornamenti ad alta priorità da Microsoft, non appena vengono rilasciate. Per altre informazioni, vedere [Aggiornare il dispositivo StorSimple](storsimple-update-device.md).  

Esaminare informazioni hello contenute in versione di hello note prima di distribuire hello aggiornare nella soluzione StorSimple.  

> [!IMPORTANT]
> * Usare servizio StorSimple Manager hello e non di Windows PowerShell per aggiornamento di febbraio di StorSimple tooinstall hello.   
> * Sono necessari circa un tooinstall ora questo aggiornamento. Tuttavia, se si siano installando gli aggiornamenti cumulativi, il processo di hello può richiedere circa 3 ore toocomplete.  
> * Hello versione di febbraio di StorSimple non contiene alcun dispositivo virtuale di aggiornamenti toohello StorSimple. È comunque possibile applicare Windows aggiornamenti toohello virtuale periferiche disponibili, tra cui sicurezza recente correzioni, ma non verrà visualizzato una modifica nella versione per il dispositivo virtuale hello.  
> 
> 

Verificare che tale hello seguenti prerequisiti sono soddisfatto tooupdating precedente del dispositivo StorSimple.  

* Assicurarsi che entrambi i controller di dispositivo siano in esecuzione prima di cercare nuovi aggiornamenti. Se dei controller non è in esecuzione, l'analisi di hello avrà esito negativo. tooverify che hello controller sono in uno stato integro, passare troppo**stato Hardware** in hello **manutenzione** pagina. Se vi sono componenti di tipo **Richiesta attenzione**, contattare il supporto tecnico Microsoft prima di continuare.
* Verificare che gli indirizzi IP fissi per controller 0 e controller 1 siano instradabili e possano connettersi toohello Internet poiché verranno usati per la manutenzione dispositivo toohello gli aggiornamenti di hello. È possibile utilizzare hello [cmdlet Test-Connection](https://technet.microsoft.com/library/hh849808.aspx) tooping un indirizzo noto esterno rete hello, ad esempio outlook.com, tooverify che hello controller dispone di connettività toohello all'esterno di rete.
* Assicurarsi che le porte 80 e 443 siano disponibili sul dispositivo StorSimple per le comunicazioni in uscita. Per ulteriori informazioni, vedere hello [requisiti di rete per il dispositivo StorSimple](storsimple-system-requirements.md#networking-requirements-for-your-storsimple-device).
* Se versione software del dispositivo hello è antecedente a 6.3.9600.17312 (aggiornamento di ottobre 2014), disabilitare le porte Data 2 e Data 3 hello, se abilitate, prima di avviare l'aggiornamento di hello. Lasciando hello Data 2 o Data 3 abilitate quando si applicano aggiornamenti hello porte potrebbe toogo di controller del dispositivo in modalità di ripristino. Si noti che quando si disabilitano le interfacce di rete hello, tutti i volumi di hello associata verranno reso offline e hello i/o potrebbero essere compromesse per durata hello dell'aggiornamento di hello.  

## <a name="whats-new-in-hello-february-release"></a>Novità nella versione di febbraio hello
Questo aggiornamento contiene una correzione per hello factory reset problema che si è verificato nei dispositivi che erano stati aggiornati dalla versione di hello GA toohello versione di ottobre 2014. Per ulteriori informazioni, vedere i [problemi corretti in questa versione](#issues-fixed-in-the-february-release).   

Questo aggiornamento non contiene nuove funzionalità.  

## <a name="issues-fixed-in-hello-february-release"></a>Problemi risolti nella versione di febbraio hello
Hello nella tabella seguente descrive il problema hello che è stato risolto in questo aggiornamento.  

| No. | Funzionalità | Problema | Si applica toophysical dispositivo | Si applica toovirtual dispositivo |
| --- | --- | --- | --- | --- |
| 1 |Ripristino delle impostazioni predefinite |Si tenta di tooperform delle impostazioni di fabbrica su un dispositivo che aveva originariamente hello GA alla versione (6.3.9600.17215) installato, ma sono stata aggiornata toohello ottobre (versione 6.3.9600.17312). factory Hello reimpostare ha esito negativo e il dispositivo hello diventa instabile. |Sì |No |

## <a name="known-issues-in-hello-february-release"></a>Problemi noti nella versione di febbraio hello
Hello nella tabella seguente fornisce un riepilogo dei problemi noti in questa versione.

| No. | Funzionalità | Problema | Commenti/Soluzione alternativa | Si applica toophysical dispositivo | Si applica toovirtual dispositivo |
| --- | --- | --- | --- | --- | --- |
| 1 |Ripristino delle impostazioni predefinite |In alcuni casi, quando si esegue un ripristino delle impostazioni predefinite, hello dispositivo StorSimple può bloccarsi e visualizzare questo messaggio: **reimpostazione toofactory è in corso (fase 8)**. Ciò avviene se si preme CTRL + C mentre hello cmdlet è in corso. |Non premere CTRL + C dopo l'avvio di un ripristino delle impostazioni predefinite. Se si è già in questo stato, contattare il supporto tecnico Microsoft per i passaggi successivi. |Sì |No |
| 2 |Quorum disco |In rari casi, se la maggior parte hello dei dischi nell'enclosure EBOD hello di un 8600device si disconnette e il quorum dischi non è disponibile, quindi il pool di archiviazione di hello sarà offline. E rimarrà offline anche se hello dischi vengono riconnessi. |Sarà necessario dispositivo hello tooreboot. Se hello problema persiste, contattare il supporto Microsoft per i passaggi successivi. |Sì |No |
| 3 |Errori di snapshot nel cloud |In rari casi, uno snapshot nel cloud potrebbe non riuscire con l'errore hello **limite massimo di backup raggiunto**. Questo errore si verifica se si superano 255 cloni online sullo hello stesso dispositivo, da hello stesso volume originale eliminato. | |Sì |Sì |
| 4 |ID controller non corretto |Quando viene eseguita la sostituzione di un controller, il controller 0 potrebbe essere visualizzato come controller 1. Durante la sostituzione del controller, quando hello immagine viene caricata dal nodo peer hello, ID controller hello è inoltre possibile scaricare inizialmente come ID del controller peer hello In rari casi, questo comportamento può verificarsi anche dopo un riavvio del sistema. |Non è necessaria alcuna azione da parte dell’utente. Questa situazione si risolverà da solo dopo la sostituzione dei controller hello è stata completata. |Sì |No |
| 5 |Grafici di monitoraggio del dispositivo |Nel servizio StorSimple Manager hello, grafici di monitoraggio del dispositivo hello non funzionano quando base o l'autenticazione NTLM è abilitata nella configurazione del server proxy hello per dispositivo hello. |Modificare una configurazione del proxy web hello per hello dispositivo registrato con il servizio StorSimple Manager in modo che l'autenticazione è impostata tooNONE. toodo, hello hello eseguire Windows PowerShell per il cmdlet Set-HcsWebProxy di StorSimple. |Sì |Sì |
| 6 |Account di archiviazione |Utilizzando l'account di archiviazione di hello toodelete servizio di archiviazione hello è uno scenario non supportato. Questo conduce tooa situazione in cui non è possibile recuperare i dati utente. | |Sì |Sì |
| 7 |Failover del dispositivo |Failover multipli di un contenitore del volume da hello dispositivi di destinazione toodifferent origine dispositivo stesso non è supportata.    Il failover da un singolo messaggi non recapitabili toomultiple dispositivi renderà i contenitori di volumi hello nel primo dispositivo sottoposto a failover hello perdere la proprietà dei dati. Dopo un failover, questi contenitori di volumi o di un comportamento diverso quando vengono visualizzati nel portale di Azure classico hello. | |Sì |No |
| 8 |Installazione |Durante l'adattatore StorSimple per l'installazione di SharePoint, è necessario tooprovide IP di un dispositivo affinché hello installazione toofinish correttamente. | |Sì |No |
| 9 |Proxy Web |Se la configurazione del proxy web è HTTPS come hello specificato protocollo, la comunicazione del dispositivo al servizio ne risentirà e dispositivo hello passerà alla modalità offline. Verranno inoltre generati pacchetti di supporto nel processo di hello, usando risorse significative sul dispositivo. |Verificare che URL del proxy web hello disponga di HTTP hello protocollo specificato. Ulteriori informazioni su come troppo[configurare il proxy web per il dispositivo](storsimple-configure-web-proxy.md). |Sì |No |
| 10 |Proxy Web |Se si configurano e abilitare il proxy web su un dispositivo registrato, è necessario controller attivo di hello toorestart sul dispositivo. | |Sì |No |
| 11 |Elevata latenza del cloud ed elevato carico di lavoro I/O |Quando il dispositivo StorSimple rileva una combinazione di cloud ad alta latenza (ordine di secondi) e un elevato carico di lavoro dei / o, i volumi del dispositivo hello entrano in uno stato danneggiato e hello i/o potrebbe verificarsi un errore "dispositivo non pronto". |Si verrà necessario controller del dispositivo toomanually riavvio hello o eseguire un toorecover di failover del dispositivo da questa situazione. |Sì |No |

## <a name="physical-device-updates-in-hello-february-release"></a>Aggiornamenti del dispositivo fisico in versione di febbraio hello
Questa factory di hello correzioni aggiornamento Reimposta problema che si è verificato nei dispositivi che erano stati aggiornati dalla versione di hello GA toohello versione di ottobre 2014. Non contiene qualsiasi altro dispositivo StorSimple toohello gli aggiornamenti.  

## <a name="serial-attached-scsi-sas-controller-and-firmware-updates-in-hello-february-release"></a>Collegata alla serie SCSI (SAS) del firmware e del controller di aggiornamenti in versione di febbraio hello
Questa versione non contiene alcun controller di aggiornamenti toohello seriale-attached SCSI (SAS) o firmware hello. durante l'aggiornamento del driver Hello hello ottobre, versione 2014.  

## <a name="virtual-device-updates-in-hello-february-release"></a>Aggiornamenti del dispositivo virtuale in versione di febbraio hello
Questa versione non contiene tutti gli aggiornamenti per la periferica virtuale hello. Applicare questo aggiornamento, versione del software hello di un dispositivo virtuale non verrà modificato.


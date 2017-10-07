---
title: aaaStorSimple 8000 aggiornamento 0,2 note sulla versione | Documenti Microsoft
description: "Vengono descritte le nuove funzionalità hello e correzioni di problemi aperti e disponibili soluzioni alternative per hello gennaio 2015 release di Microsoft Azure StorSimple (aggiornamento 0,2)."
services: storsimple
documentationcenter: NA
author: SharS
manager: carmonm
editor: 
ms.assetid: d9684ae3-b38f-4678-9d70-e5dbc6b03350
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: TBD
ms.date: 05/16/2016
ms.author: v-sharos
ms.openlocfilehash: 1cee795df0b53d9b9276bc33074cf1a7aa188835
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="storsimple-8000-series-update-02-release-notes---january-2015"></a>Note sulla versione dell'aggiornamento 0.2 di StorSimple serie 8000 - Gennaio 2015
## <a name="overview"></a>Panoramica
Hello note sulla versione seguenti identificare hello problemi critici aperti per hello gennaio 2015 release di Microsoft Azure StorSimple. Contengono inoltre un elenco di hello StorSimple software e aggiornamenti del firmware inclusi in questa versione. Si tratta secondo rilascio hello dopo hello StorSimple 8000 Series versione è stata eseguita in genere disponibili nel luglio 2014.

Questo aggiornamento non modifica versione software del dispositivo fisico hello dall'aggiornamento di ottobre hello. Continua toobe versione 6.3.9600.17312. immagine di Hello usata dall'immagine del dispositivo virtuale hello è stata modificata in questa versione. Pertanto, tutti hello nuovi dispositivi virtuali creati dopo il 20/1/2015 sarà versione hello 6.3.9600.17361.  

Verificare le seguenti informazioni contenute nelle note sulla versione di hello per l'aggiornamento di gennaio 2015 hello hello.

> [!IMPORTANT]
> * Questo aggiornamento non è disponibile tramite Windows Update e non può essere installato come gli altri aggiornamenti. Il dispositivo non riceverà questo aggiornamento anche se è stato applicato gli aggiornamenti di hello utilizzando hello portale di Azure classico. Questo aggiornamento si applica solo a dispositivi toovirtual creati dopo il 20 gennaio 2015. 
> * Hello versione di gennaio di StorSimple non contiene alcun dispositivo fisico di aggiornamenti toohello StorSimple. È comunque possibile applicare Windows aggiornamenti toohello virtuale periferiche disponibili, tra cui sicurezza recente correzioni, ma non verrà visualizzato una modifica nella versione per il dispositivo fisico StorSimple di hello.
> 
> 

## <a name="whats-new-in-hello-january-release"></a>Novità nella versione di gennaio hello
Questo aggiornamento contiene una correzione relativi volumi toohello che passano offline nel dispositivo virtuale hello. (vedere [Problemi corretti in questa versione](#issues-fixed-in-the-january-release)).  

aggiornamento di Hello non contiene nuove funzionalità o funzionalità.  

## <a name="issues-fixed-in-hello-january-release"></a>Problemi risolti nella versione di gennaio hello
Hello nella tabella seguente descrive il problema hello che è stato risolto in questo aggiornamento.

| No. | Funzionalità | Problema | Si applica toophysical dispositivo | Si applica toovirtual dispositivo |
| --- | --- | --- | --- | --- |
| 1 |Volumi che passano offline |Quando persistenza delle latenze cloud per alcuni minuti, i volumi del dispositivo virtuale StorSimple hello passano offline negli host hello. Questa correzione aumenta la soglia hello per le latenze cloud, riducendo così al minimo le situazioni hello che provocherebbero toogo offline di hello volumi negli host. |No |Sì |

## <a name="known-issues-in-hello-january-release"></a>Problemi noti nella versione di gennaio hello
Hello nella tabella seguente fornisce un riepilogo dei problemi noti in questa versione.

| No. | Funzionalità | Problema | Commenti/Soluzione alternativa | Si applica toophysical dispositivo | Si applica toovirtual dispositivo |
| --- | --- | --- | --- | --- | --- |
| 1 |Ripristino delle impostazioni predefinite |In alcuni casi, quando si esegue un ripristino delle impostazioni predefinite, hello dispositivo StorSimple può bloccarsi e visualizzare questo messaggio: **reimpostazione toofactory è in corso (fase 8).** Ciò avviene se si preme CTRL + C mentre hello cmdlet è in corso. |Non premere CTRL + C dopo l'avvio di un ripristino delle impostazioni predefinite. Se si è già in questo stato, contattare il supporto tecnico Microsoft per i passaggi successivi. |Sì |No |
| 2 |Quorum disco |In rari casi, se la maggior parte hello dei dischi nell'enclosure EBOD hello di un dispositivo 8600 si disconnette e il quorum dischi non è disponibile, quindi il pool di archiviazione hello sarà offline. E rimarrà offline anche se hello dischi vengono riconnessi. |Sarà necessario dispositivo hello tooreboot. Se hello problema persiste, contattare il supporto Microsoft per i passaggi successivi. |Sì |No |
| 3 |Errori di snapshot nel cloud |In rari casi, uno snapshot nel cloud potrebbe non riuscire con l'errore hello **limite massimo di backup raggiunto**. Questo errore si verifica se si superano 255 cloni online sullo hello stesso dispositivo, da hello stesso volume originale eliminato. | |Sì |Sì |
| 4 |ID controller non corretto |Quando viene eseguita la sostituzione di un controller, il controller 0 potrebbe essere visualizzato come controller 1. Durante la sostituzione del controller, quando hello immagine viene caricata dal nodo peer hello, ID controller hello è inoltre possibile scaricare inizialmente come ID del controller peer hello  In rari casi, questo comportamento può verificarsi anche dopo un riavvio del sistema. |Non è necessaria alcuna azione da parte dell’utente. Questa situazione si risolverà da solo dopo la sostituzione dei controller hello è stata completata. |Sì |No |
| 5 |Grafici di monitoraggio del dispositivo |Nel servizio StorSimple Manager hello, grafici di monitoraggio del dispositivo hello non funzionano quando base o l'autenticazione NTLM è abilitata nella configurazione del server proxy hello per dispositivo hello. |Modificare una configurazione del proxy web hello per hello dispositivo registrato con il servizio StorSimple Manager in modo che l'autenticazione è impostata tooNONE. toodo, hello hello eseguire Windows PowerShell per il cmdlet Set-HcsWebProxy di StorSimple. |Sì |Sì |
| 6 |Account di archiviazione |Utilizzando l'account di archiviazione di hello toodelete servizio di archiviazione hello è uno scenario non supportato. Questo conduce tooa situazione in cui non è possibile recuperare i dati utente. | |Sì |Sì |
| 7 |Failover del dispositivo |Failover multipli di un contenitore del volume da hello dispositivi di destinazione toodifferent origine dispositivo stesso non è supportata. |Il failover da un singolo messaggi non recapitabili toomultiple dispositivi renderà i contenitori di volumi hello nel primo dispositivo sottoposto a failover hello perdere la proprietà dei dati. Dopo un failover, questi contenitori di volumi o di un comportamento diverso quando vengono visualizzati nel portale di Azure classico hello. |Sì |No |
| 8 |Installazione |Durante l'adattatore StorSimple per l'installazione di SharePoint, è necessario tooprovide IP di un dispositivo affinché hello installazione toofinish correttamente. | |Sì |No |
| 9 |Proxy Web |Se la configurazione del proxy web è HTTPS come hello specificato protocollo, la comunicazione del dispositivo al servizio ne risentirà e dispositivo hello passerà alla modalità offline. Verranno inoltre generati pacchetti di supporto nel processo di hello, usando risorse significative sul dispositivo. |Verificare che URL del proxy web hello disponga di HTTP hello protocollo specificato. Visualizzare ulteriori informazioni su come troppo[configurare il proxy web per il dispositivo](storsimple-configure-web-proxy.md). |Sì |No |
| 10 |Proxy Web |Se si configurano e abilitare il proxy web su un dispositivo registrato, è necessario controller attivo di hello toorestart sul dispositivo. | |Sì |No |
| 11 |Elevata latenza del cloud ed elevato carico di lavoro I/O |Quando il dispositivo StorSimple rileva una combinazione di cloud ad alta latenza (ordine di secondi) e un elevato carico di lavoro dei / o, i volumi del dispositivo hello entrano in uno stato danneggiato e hello i/o potrebbe verificarsi un errore "dispositivo non pronto". |Si verrà necessario controller del dispositivo toomanually riavvio hello o eseguire un toorecover di failover del dispositivo da questa situazione. |Sì |No |

## <a name="physical-device-updates-in-hello-january-release"></a>Aggiornamenti del dispositivo fisico in versione di gennaio hello
Questo aggiornamento non contiene qualsiasi altro dispositivo StorSimple toohello le modifiche.

## <a name="serial-attached-scsi-sas-controller-and-firmware-updates-in-hello-january-release"></a>Serie-attached SCSI (SAS) controller e del firmware gli aggiornamenti in rilasci di gennaio hello
Questa versione non contiene alcun controller di aggiornamenti toohello seriale-attached SCSI (SAS) o firmware hello. durante l'aggiornamento del driver Hello hello ottobre, versione 2014. 

## <a name="virtual-device-updates-in-hello-january-release"></a>Aggiornamenti del dispositivo virtuale in versione di gennaio hello
Questa versione contiene un'immagine per dispositivo virtuale hello aggiornata. Tutti i dispositivi virtuali hello creati dopo il 20 gennaio 2015 sarà 6.3.9600.17361 versione software hello.


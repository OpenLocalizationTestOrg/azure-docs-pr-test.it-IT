---
title: note sulla versione di aaaStorSimple 8000 versione versione | Documenti Microsoft
description: "Descrive le nuove funzionalità hello, problemi aperti e soluzioni alternative disponibili per hello luglio 2014 versione di Microsoft Azure StorSimple."
services: storsimple
documentationcenter: NA
author: SharS
manager: carmonm
editor: 
ms.assetid: 12f1796e-37c3-42b4-b997-a84fc1950c20
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: TBD
ms.date: 04/18/2016
ms.author: v-sharos
ms.openlocfilehash: 74863a3e2811dc7be5e6f482a5be4bbc37e3cd71
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="storsimple-8000-series-release-version-release-notes---july-2014"></a>Note sulla versione di rilascio di StorSimple serie 8000 - Luglio 2014
## <a name="overview"></a>Panoramica
note sulla versione di Hello seguire identificare hello problemi critici aperti per hello StorSimple 8000 Series versione di luglio 2014 disponibilità generale (GA) di Microsoft Azure StorSimple. Questa versione corrisponde toosoftware versione 6.3.9600.17215.  

Se non diversamente specificato, queste note sulla versione si applicano tooall modelli del dispositivo StorSimple hello. note sulla versione di Hello vengono aggiornati continuamente; come vengono individuati problemi critici che richiedono una soluzione alternativa, vengono aggiunti. Prima di distribuire la soluzione di Microsoft Azure StorSimple, considerare le seguenti informazioni hello.  

## <a name="known-issues-in-this-release"></a>Problemi noti in questa versione
Hello nella tabella seguente fornisce un riepilogo dei problemi noti in questa versione.  

| No. | Funzionalità | Problema | Commenti/Soluzione alternativa | Si applica toophysical dispositivo | Si applica toovirtual dispositivo |
| --- | --- | --- | --- | --- | --- |
| 1 |Ripristino delle impostazioni predefinite |In alcuni casi, quando si esegue un ripristino delle impostazioni predefinite, hello dispositivo StorSimple può bloccarsi e visualizzare questo messaggio: **reimpostazione toofactory è in corso (fase 8)**. Ciò avviene se si preme CTRL + C mentre hello cmdlet è in corso. |Non premere CTRL + C dopo l'avvio di un ripristino delle impostazioni predefinite. Se si è già in questo stato, contattare il supporto tecnico Microsoft per i passaggi successivi. |Sì |No |
| 2 |Quorum disco |In rari casi, se la maggior parte hello dei dischi nell'enclosure EBOD hello di un dispositivo 8600 si disconnette e il quorum dischi non è disponibile, quindi il pool di archiviazione hello sarà offline. E rimarrà offline anche se hello dischi vengono riconnessi. |Sarà necessario dispositivo hello tooreboot. Se hello problema persiste, contattare il supporto Microsoft per i passaggi successivi. |Sì |No |
| 3 |Errori di snapshot nel cloud |In rari casi, uno snapshot nel cloud potrebbe non riuscire con l'errore hello **limite massimo di backup raggiunto**. Questo errore si verifica se si superano 255 cloni online sullo hello stesso dispositivo, da hello stesso volume originale eliminato. | |Sì |Sì |
| 4 |ID controller non corretto |Quando viene eseguita la sostituzione di un controller, il controller 0 potrebbe essere visualizzato come controller 1. Durante la sostituzione del controller, quando hello immagine viene caricata dal nodo peer hello, ID controller hello è inoltre possibile scaricare inizialmente come ID del controller peer hello In rari casi, questo comportamento può verificarsi anche dopo un riavvio del sistema. |Non è necessaria alcuna azione da parte dell’utente. Questa situazione si risolverà da solo dopo la sostituzione dei controller hello è stata completata. |Sì |No |
| 5 |Grafici di monitoraggio del dispositivo |Nel servizio StorSimple Manager hello, grafici di monitoraggio del dispositivo hello non funzionano quando base o l'autenticazione NTLM è abilitata nella configurazione del server proxy hello per dispositivo hello. |Modificare una configurazione del proxy web hello per hello dispositivo registrato con il servizio StorSimple Manager in modo che l'autenticazione è impostata tooNONE. toodo, hello hello eseguire Windows PowerShell per il cmdlet Set-HcsWebProxy di StorSimple. |Sì |Sì |
| 6 |Account di archiviazione |Utilizzando l'account di archiviazione di hello toodelete servizio di archiviazione hello è uno scenario non supportato. Questo conduce tooa situazione in cui non è possibile recuperare i dati utente. | |Sì |Sì |
| 7 |Failback |Il failback entro 24 ore di ripristino di emergenza (DR) non è supportato. | |Sì |No |
| 8 |Failover del dispositivo |Failover multipli di un contenitore del volume da hello dispositivi di destinazione toodifferent origine dispositivo stesso non è supportata. Il failover da un singolo messaggi non recapitabili toomultiple dispositivi renderà i contenitori di volumi hello nel primo dispositivo sottoposto a failover hello perdere la proprietà dei dati. Dopo un failover, questi contenitori di volumi o di un comportamento diverso quando vengono visualizzati nel portale di Azure classico hello. | |Sì |No |
| 9 |Installazione |Durante l'adattatore StorSimple per l'installazione di SharePoint, è necessario tooprovide IP di un dispositivo per hello installazione toofinish correttamente. | |Sì |No |
| 10 |Interfacce di rete |Interfacce di rete DATA 2 e DATA 3 sono state scambiate nel software hello. |Se è necessario tooconfigure queste interfacce, contattare il supporto Microsoft. |Sì |No |


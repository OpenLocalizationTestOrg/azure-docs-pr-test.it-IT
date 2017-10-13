---
title: Note sulla versione dell'aggiornamento 0.2 di StorSimple 8000 | Microsoft Docs
description: "Vengono descritte le nuove funzionalità e correzioni, i problemi e le soluzioni alternative disponibili per la versione di gennaio 2015 di Microsoft Azure StorSimple. (aggiornamento 0.2)."
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
ms.openlocfilehash: 2fc50f7faddb4b61ea5e7d328469fc3cc0eb6f3e
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="storsimple-8000-series-update-02-release-notes---january-2015"></a>Note sulla versione dell'aggiornamento 0.2 di StorSimple serie 8000 - Gennaio 2015
## <a name="overview"></a>Panoramica
Le seguenti note sulla versione identificano i problemi critici aperti per la versione di gennaio 2015 di StorSimple di Microsoft Azure. Contengono inoltre un elenco degli aggiornamenti software e firmware di StorSimple inclusi in questa versione. Si tratta della seconda versione dopo la versione di rilascio di StorSimple serie 8000 resa disponibile a livello generale a luglio 2014.

Questo aggiornamento non modifica la versione del software del dispositivo rispetto all'aggiornamento di ottobre,  che continua a essere la versione 6.3.9600.17312. L'immagine utilizzata per l'immagine del dispositivo virtuale è stata modificata in questa versione. Di conseguenza, tutti i nuovi dispositivi virtuali creati dopo il 20 gennaio 2015 visualizzeranno la versione come 6.3.9600.17361.  

Esaminare le seguenti informazioni contenute nelle note sulla versione per l'aggiornamento di gennaio 2015.

> [!IMPORTANT]
> * Questo aggiornamento non è disponibile tramite Windows Update e non può essere installato come gli altri aggiornamenti. Il dispositivo non riceverà questo aggiornamento neanche se gli aggiornamenti sono stati applicati tramite il portale di Azure classico. Questo aggiornamento verrà applicato solo ai dispositivi virtuali creati dopo il 20 gennaio 2015. 
> * La versione di gennaio di StorSimple non contiene aggiornamenti per il dispositivo fisico StorSimple. Anche se è possibile applicare gli aggiornamenti di Windows disponibili al dispositivo virtuale, incluse le ultime correzioni rapide per la protezione, nella versione per il dispositivo virtuale non apparirà alcuna modifica.
> 
> 

## <a name="whats-new-in-the-january-release"></a>Novità nella versione di gennaio
Questo aggiornamento contiene una correzione relativa ai volumi che passano alla modalità offline sul dispositivo virtuale  (vedere [Problemi corretti in questa versione](#issues-fixed-in-the-january-release)).  

Questo aggiornamento non contiene nuove funzionalità.  

## <a name="issues-fixed-in-the-january-release"></a>Problemi risolti nella versione di gennaio
Nella tabella seguente viene descritto il problema risolto in questo aggiornamento.

| No. | Funzionalità | Problema | Si applica a un dispositivo fisico | Si applica a un dispositivo virtuale |
| --- | --- | --- | --- | --- |
| 1 |Volumi che passano offline |Quando le latenze elevate del cloud persistono per diversi minuti, i volumi del dispositivo virtuale StorSimple passano offline negli host. Questa correzione aumenta la soglia per le latenze del cloud, riducendo così al minimo le situazioni che causano il passaggio dei volumi offline sugli host. |No |Sì |

## <a name="known-issues-in-the-january-release"></a>Problemi noti risolti nella versione di gennaio
Nella tabella seguente viene fornito un riepilogo dei problemi noti in questa versione.

| No. | Funzionalità | Problema | Commenti/Soluzione alternativa | Si applica a un dispositivo fisico | Si applica a un dispositivo virtuale |
| --- | --- | --- | --- | --- | --- |
| 1 |Ripristino delle impostazioni predefinite |In alcuni casi, quando si esegue un ripristino delle impostazioni predefinite, il dispositivo StorSimple potrebbe bloccarsi e l'utente potrebbe visualizzare il messaggio: **Ripristino delle impostazioni predefinite in corso (fase 8)**. Ciò si verifica se si preme CTRL + C mentre il cmdlet è in esecuzione. |Non premere CTRL + C dopo l'avvio di un ripristino delle impostazioni predefinite. Se si è già in questo stato, contattare il supporto tecnico Microsoft per i passaggi successivi. |Sì |No |
| 2 |Quorum disco |In rari casi, se la maggior parte dei dischi nello chassis EBOD di un dispositivo 8600 è disconnessa generando un’assenza di quorum disco, il pool di archiviazione sarà offline  e rimarrà in tale stato anche se i dischi vengono riconnessi. |Sarà necessario riavviare il dispositivo. Se il problema persiste, contattare il supporto tecnico Microsoft per i passaggi successivi. |Sì |No |
| 3 |Errori di snapshot nel cloud |In rari casi, uno snapshot cloud potrebbe non riuscire a causa dell’errore **Raggiunto il limite massimo di backup**. Ciò si verifica se si superano i 255 cloni online sullo stesso dispositivo, dallo stesso volume originale eliminato. | |Sì |Sì |
| 4 |ID controller non corretto |Quando viene eseguita la sostituzione di un controller, il controller 0 potrebbe essere visualizzato come controller 1. Durante la sostituzione del controller, quando l'immagine viene caricata dal nodo peer, l'ID del controller può presentarsi inizialmente come ID del controller peer.  In rari casi, questo comportamento può verificarsi anche dopo un riavvio del sistema. |Non è necessaria alcuna azione da parte dell’utente. Questa situazione si risolverà dopo la sostituzione del controller. |Sì |No |
| 5 |Grafici di monitoraggio del dispositivo |Nel servizio StorSimple Manager, i grafici di monitoraggio del dispositivo non funzionano quando l’autenticazione di base o NTLM è abilitata nella configurazione del server proxy per il dispositivo. |Modificare la configurazione del proxy Web per il dispositivo registrato con il servizio StorSimple Manager in modo che l'autenticazione sia impostata su NESSUNA. A tale scopo, eseguire il cmdlet Set-HcsWebProxy di Windows PowerShell per StorSimple. |Sì |Sì |
| 6 |Account di archiviazione |L’utilizzo del servizio di archiviazione per eliminare l'account di archiviazione non è supportato. Tale operazione causerebbe una situazione in cui non è possibile recuperare i dati dell'utente. | |Sì |Sì |
| 7 |Failover del dispositivo |I failover multipli di un contenitore di volumi dallo stesso dispositivo di origine verso dispositivi di destinazione diversi non sono supportati. |Il failover da un singolo dispositivo inattivo a più dispositivi causerà la perdita della proprietà dei dati dei contenitori di volumi sul primo dispositivo sottoposto a failover. Dopo un tale failover, questi contenitori di volumi appariranno o si comporteranno in maniera diversa quando vengono visualizzati nel portale di Azure classico. |Sì |No |
| 8 |Installazione |Durante l’installazione dell'adattatore StorSimple per SharePoint è necessario fornire un IP del dispositivo affinché l'installazione possa essere completata correttamente. | |Sì |No |
| 9 |Proxy Web |Se nella configurazione del proxy Web è specificato il protocollo HTTPS, la comunicazione tra dispositivo e servizio ne sarà interessata e il dispositivo verrà portato offline. Nel processo, inoltre, verranno generati pacchetti di supporto, consumando risorse significative sul dispositivo. |Assicurarsi che l'URL del proxy Web abbia HTTP come protocollo specificato. Vedere altre informazioni su come [configurare il proxy Web per il dispositivo](storsimple-configure-web-proxy.md). |Sì |No |
| 10 |Proxy Web |Se si configura e si abilita il proxy Web su un dispositivo registrato, è necessario riavviare il controller attivo sul dispositivo. | |Sì |No |
| 11 |Elevata latenza del cloud ed elevato carico di lavoro I/O |Quando il dispositivo StorSimple rileva una combinazione di latenze cloud molto elevate (nell’ordine di secondi) e carico di lavoro I/O elevato, i volumi del dispositivo entrano in uno stato con funzionalità ridotte e gli I/O potrebbero non riuscire a causa di un errore di "dispositivo non pronto". |In questo caso è necessario riavviare manualmente i controller del dispositivo o eseguire un failover del dispositivo per risolvere  il problema. |Sì |No |

## <a name="physical-device-updates-in-the-january-release"></a>Aggiornamenti del dispositivo fisico nella versione di gennaio
Questo aggiornamento non contiene altre modifiche per il dispositivo StorSimple.

## <a name="serial-attached-scsi-sas-controller-and-firmware-updates-in-the-january-release"></a>Aggiornamenti firmware e controller SAS (Serial Attached SCSI) presenti nella versione di gennaio
Questa versione non contiene aggiornamenti per il controller SAS (Serial Attached SCSI) o il firmware. L'aggiornamento del driver era nella versione di ottobre 2014. 

## <a name="virtual-device-updates-in-the-january-release"></a>Aggiornamenti del dispositivo virtuale nella versione di gennaio
Questa versione contiene un'immagine aggiornata per il dispositivo virtuale. Di conseguenza, tutti i dispositivi virtuali creati dopo il 20 gennaio 2015 visualizzeranno la versione del software come 6.3.9600.17361.


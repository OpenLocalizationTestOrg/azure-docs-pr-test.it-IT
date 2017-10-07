---
title: aaaMicrosoft amministrazione Array virtuale di Azure StorSimple Manager | Documenti Microsoft
description: Informazioni su come toomanage StorSimple locale Array virtuale tramite servizio di gestione di dispositivi StorSimple hello in hello portale di Azure.
services: storsimple
documentationcenter: 
author: alkohli
manager: carmonm
editor: 
ms.assetid: 958244a5-f9f5-455e-b7ef-71a65558872e
ms.service: storsimple
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 12/1/2016
ms.author: alkohli
ms.openlocfilehash: 1fabf9ca524b461266346a6cabf49aef772032ea
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="use-hello-storsimple-device-manager-service-tooadminister-your-storsimple-virtual-array"></a>Utilizzare tooadminister servizio di gestione di dispositivi StorSimple hello l'Array virtuale StorSimple
![flusso del processo di installazione](./media/storsimple-virtual-array-manager-service-administration/manage4.png)

## <a name="overview"></a>Panoramica
Questo articolo descrive l'interfaccia del servizio gestione di dispositivi StorSimple hello, incluso come tooconnect tooit e hello varie opzioni disponibili e fornisce collegamenti toohello flussi di lavoro che possono essere eseguite mediante questa interfaccia.

Dopo aver letto l'articolo, l'utente sarà in grado di:

* Connettere il servizio di gestione di dispositivi StorSimple toohello
* Passare hello UI Gestione dispositivi StorSimple
* Amministrare l'Array virtuale StorSimple tramite hello del servizio di gestione di dispositivi StorSimple

> [!NOTE]
> opzioni di gestione hello tooview disponibili per il dispositivo di serie StorSimple 8000 hello, andare troppo[utilizzare hello tooadminister servizio StorSimple Manager dispositivo StorSimple](storsimple-manager-service-administration.md).
> 
> 

## <a name="connect-toohello-storsimple-device-manager-service"></a>Connettere il servizio di gestione di dispositivi StorSimple toohello
servizio di gestione di dispositivi StorSimple Hello in esecuzione in Microsoft Azure e si connette toomultiple StorSimple Virtual Array. Utilizzare un portale di Microsoft Azure centrale in esecuzione in un browser toomanage questi dispositivi. tooconnect toohello servizio di gestione di dispositivi StorSimple, hello seguente.

#### <a name="tooconnect-toohello-service"></a>servizio toohello tooconnect
1. Andare troppo[https://ms.portal.azure.com](https://ms.portal.azure.com).
2. Utilizzando le credenziali dell'account Microsoft, accedere al portale di Microsoft Azure toohello (a cui si trovano in alto a destra di hello del riquadro hello).
3. Passare tooBrowse--> 'Filter' su StorSimple Device Managers tooview tutti i responsabili di dispositivo in una specifica sottoscrizione.

## <a name="use-hello-storsimple-device-manager-service-tooperform-management-tasks"></a>Utilizzare le attività di gestione di hello dispositivo StorSimple Manager servizio tooperform
Hello nella tabella seguente mostra un riepilogo di tutti i flussi di lavoro complessi che possono essere eseguite all'interno di pannello riepilogo servizio di gestione di dispositivi StorSimple hello e le attività di gestione comuni hello. Queste attività sono organizzate in base ai pannelli hello in cui sono state avviate.

Per ulteriori informazioni su ogni flusso di lavoro, fare clic su una procedura appropriata presente hello nella tabella hello.

#### <a name="storsimple-device-manager-workflows"></a>Flussi di lavoro di Gestione dispositivi StorSimple
| Se si desidera toodo... | Seguire questa procedura |
| --- | --- | --- |
| Creare un servizio</br>Eliminare un servizio</br>Ottenere una chiave di registrazione del servizio hello</br>Rigenerare la chiave di registrazione del servizio hello |[Distribuire il servizio di gestione di dispositivi StorSimple hello](storsimple-virtual-array-manage-service.md) |
| Visualizzare i registri attività hello |[Utilizzare il servizio StorSimple hello riepilogo](storsimple-virtual-array-service-summary.md) |
| Disattivare un array virtuale</br>Eliminare un array virtuale |[Disattivare o eliminare un array virtuale](storsimple-virtual-array-deactivate-and-delete-device.md) |
| Ripristino di emergenza e failover del dispositivo</br>Prerequisiti di failover</br>Ripristino di emergenza di continuità aziendale (BCDR)</br>Errori durante il ripristino di emergenza |[Ripristino di emergenza e failover del dispositivo per l'array virtuale StorSimple](storsimple-virtual-array-failover-dr.md) |
| Backup di condivisioni e volumi</br>Creazione di un backup manuale</br>Modifica pianificazione backup hello</br>Visualizzare i backup esistenti |[Backup dell'array virtuale StorSimple](storsimple-virtual-array-backup.md) |
| Clonare condivisioni da un set di backup</br>Clonare volumi da un set di backup</br>Ripristino a livello di elementi (solo file server) |[Clonare da un backup dell'array virtuale StorSimple](storsimple-virtual-array-clone.md) |
| Informazioni sugli account di archiviazione</br>Aggiungere un account di archiviazione</br>Modificare un account di archiviazione</br>Eliminare un account di archiviazione |[Gestire gli account di archiviazione per hello Array virtuale StorSimple](storsimple-virtual-array-manage-storage-accounts.md) |
| Informazioni sui record di controllo di accesso</br>Aggiungere o modificare un record di controllo di accesso </br>Eliminare un record di controllo di accesso |[Gestire i record di controllo di accesso per hello Array virtuale StorSimple](storsimple-virtual-array-manage-acrs.md) |
| Visualizza i dettagli dei processi |[Gestire processi di array virtuali StorSimple](storsimple-virtual-array-manage-jobs.md) |
| Configurare le impostazioni degli avvisi</br>Ricevere notifiche di avviso</br>Gestisci avvisi</br>Esaminare gli avvisi |[Consente di visualizzare e gestire gli avvisi per hello Array virtuale StorSimple](storsimple-virtual-array-manage-alerts.md) |
| Modifica password di amministratore del dispositivo hello |[Modifica password amministratore del dispositivo StorSimple Virtual Array hello](storsimple-virtual-array-change-device-admin-password.md) |
| Installare gli aggiornamenti del software |[Aggiornare l'array virtuale](storsimple-virtual-array-install-update.md) |

> [!NOTE]
> È necessario utilizzare hello [interfaccia utente web locale](storsimple-ova-web-ui-admin.md) per hello seguenti attività:
> 
> * [Recuperare una chiave DEK hello](storsimple-ova-web-ui-admin.md#get-the-service-data-encryption-key)
> * [Creare un pacchetto di supporto](storsimple-ova-web-ui-admin.md#generate-a-log-package)
> * [Arrestare e riavviare l'array virtuale](storsimple-ova-web-ui-admin.md#shut-down-and-restart-your-device)
> 
> 

## <a name="next-steps"></a>Passaggi successivi
Per informazioni su hello interfaccia utente web e come toouse, andare troppo[utilizzare hello tooadminister dell'interfaccia utente web di StorSimple l'Array virtuale StorSimple](storsimple-ova-web-ui-admin.md).


---
title: amministrazione di service Manager aaaStorSimple | Documenti Microsoft
description: Informazioni su come toomanage dispositivo StorSimple tramite hello servizio StorSimple Manager in hello portale di Azure classico.
services: storsimple
documentationcenter: 
author: alkohli
manager: carmonm
editor: 
ms.assetid: 2586582e-d85c-42e1-afb3-be734c1c0461
ms.service: storsimple
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 09/21/2016
ms.author: alkohli
ms.openlocfilehash: 695ebbb785590a0e3d6de4c73125f65b16dcb776
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="use-hello-storsimple-manager-service-tooadminister-your-storsimple-device"></a>Utilizzare tooadminister servizio StorSimple Manager di hello del dispositivo StorSimple
## <a name="overview"></a>Panoramica
Questo articolo descrive l'interfaccia del servizio StorSimple Manager hello, inclusi come tooit tooconnect, hello diverse opzioni disponibili e collega out toohello flussi di lavoro che possono essere eseguite mediante questa interfaccia. Questa guida è applicabile tooboth; Hello fisico StorSimple e dispositivo virtuale hello.

Una volta letto l'articolo, si sarà in grado di:

* La connessione del servizio di gestione tooStorSimple
* Passare hello UI StorSimple Manager
* Amministrare il dispositivo StorSimple tramite hello servizio StorSimple Manager

## <a name="connect-toostorsimple-manager-service"></a>La connessione del servizio di gestione tooStorSimple
Hello servizio StorSimple Manager in esecuzione in Microsoft Azure e si connette dispositivi StorSimple toomultiple. Utilizzare un portale classico centrale di Microsoft Azure in esecuzione in un browser toomanage questi dispositivi. tooconnect toohello servizio StorSimple Manager, hello seguente.

#### <a name="tooconnect-toohello-service"></a>servizio toohello tooconnect
1. Passare troppo[https://manage.windowsazure.com/](https://manage.windowsazure.com/).
2. Utilizzando le credenziali dell'account Microsoft, accedere al portale classico Microsoft Azure toohello (a cui si trovano in alto a destra di hello del riquadro hello).
3. Scorrere verso il basso a sinistra del servizio StorSimple Manager di navigazione riquadro tooaccess hello hello.

## <a name="navigate-storsimple-manager-service-ui"></a>Passare all'interfaccia utente del servizio StorSimple Manager
Hello gerarchia di navigazione per il servizio StorSimple Manager hello che in hello nella tabella seguente viene visualizzata l'interfaccia utente.

* **StorSimple Manager** pagina di destinazione accetta toohello dispositivi tooall applicabile pagine a livello di servizio di interfaccia utente all'interno di un servizio.
* **Dispositivi** pagina richiede dispositivo specifico di toohello dispositivo a livello dell'interfaccia utente pagine tooa applicabile.
* **Contenitori di volumi** pagina richiede pagina volume toohello che mostra tutti i volumi di hello associati a un dispositivo.

#### <a name="storsimple-manager-service-navigational-hierarchy"></a>Gerarchia di spostamento del servizio StorSimple Manager
| Pagina di destinazione | Pagine a livello di servizio | Pagine a livello di dispositivo | Pagine a livello di dispositivo |
| --- | --- | --- | --- |
| Servizio StorSimple Manager |Dashboard del servizio |Pagina dashboard | |
| Dispositivi → |Monitoraggio | | |
| Catalogo di backup |Contenitori di volume → |Volumi | |
| Configura (servizio) |Criteri di backup | | |
| Processi |Configura (dispositivo) | | |
| Avvisi |Manutenzione | | |

![Video disponibile](./media/storsimple-manager-service-administration/Video_icon.png)**Video disponibile**

Fare clic su un video che illustra l'interfaccia utente del servizio StorSimple Manager hello, toowatch [qui](https://azure.microsoft.com/documentation/videos/storsimple-manager-service-overview/).

## <a name="administer-storsimple-device-using-storsimple-manager-service"></a>Gestire il dispositivo StorSimple tramite il servizio StorSimple Manager
Hello nella tabella seguente mostra un riepilogo di tutte le attività di gestione comuni hello e flussi di lavoro complessi che possono essere eseguite all'interno di hello interfaccia utente del servizio StorSimple Manager. Queste attività sono organizzate in base alle pagine dell'interfaccia utente di hello in cui sono state avviate.

Per ulteriori informazioni su ogni flusso di lavoro, fare clic su una procedura appropriata presente hello nella tabella hello.

#### <a name="storsimple-manager-workflows"></a>Flussi di lavoro di StorSimple Manager
| Se si desidera toodo... | Vai a pagina UI toothis... | Usare questa procedura. |
| --- | --- | --- |
| Creare un servizio</br>Eliminare un servizio</br>Ottenere la chiave di registrazione del servizio</br>Rigenerare la chiave di registrazione |Servizio StorSimple Manager |[Distribuire un servizio StorSimple Manager](storsimple-manage-service.md) |
| Modifica chiave DEK del servizio hello</br>Visualizzare log operazioni hello |Servizio StorSimple Manager → Dashboard |[Utilizzare dashboard del servizio StorSimple Manager hello](storsimple-service-dashboard.md) |
| Disattivare un dispositivo</br>Eliminare un dispositivo |Servizio StorSimple Manager → Dispositivi |[Disattivare o eliminare un dispositivo](storsimple-deactivate-and-delete-device.md) |
| Informazioni sul failover del dispositivo e sul ripristino di emergenza</br>Dispositivo fisico tooa di failover</br>Dispositivo virtuale tooa di failover</br>Ripristino di emergenza di continuità aziendale (BCDR) |Servizio StorSimple Manager → Dispositivi |[Failover e ripristino di emergenza per il dispositivo StorSimple](storsimple-device-failover-disaster-recovery.md) |
| Elenco di backup per un volume</br>Selezionare un set di backup</br>Eliminare un set di backup |Servizio StorSimple Manager → Catalogo di backup |[Gestire i backup](storsimple-manage-backup-catalog.md) |
| Clonare un volume |Servizio StorSimple Manager → Catalogo di backup |[Clonare un volume](storsimple-clone-volume.md) |
| Ripristinare un set di backup |Servizio StorSimple Manager → Catalogo di backup |[Ripristinare un set di backup](storsimple-restore-from-backup-set.md) |
| Informazioni sugli account di archiviazione</br>Aggiungere un account di archiviazione</br>Modificare un account di archiviazione</br>Eliminare un account di archiviazione</br>Rotazione della chiave degli account di archiviazione |Servizio StorSimple Manager → Configura |[Gestire gli account di archiviazione](storsimple-manage-storage-accounts.md) |
| Informazioni sui modelli di larghezza di banda</br>Aggiunta di un modello di larghezza di banda</br>Modifica di un modello di larghezza di banda</br>Eliminazione di un modello di larghezza di banda</br>Utilizzo di un modello di larghezza di banda predefinito</br>Creare un modello di larghezza di banda giornata intera che inizia a un'ora specificata |Servizio StorSimple Manager → Configura |[Gestire i modelli di larghezza di banda](storsimple-manage-bandwidth-templates.md) |
| Informazioni sui record di controllo di accesso</br>Creare un record di controllo di accesso</br>Modificare un record di controllo di accesso</br>Eliminare un record di controllo di accesso |Servizio StorSimple Manager → Configura |[Gestire record di controllo di accesso](storsimple-manage-acrs.md) |
| Visualizzare i dettagli dei processi</br>Annullare un processo |Servizio StorSimple Manager → Processi |[Gestire i processi](storsimple-manage-jobs.md) |
| Ricevere notifiche di avviso</br>Gestisci avvisi</br>Esaminare gli avvisi |Servizio StorSimple Manager → Avvisi |[Visualizzare e gestire gli avvisi di StorSimple](storsimple-manage-alerts.md) |
| Visualizzare gli iniziatori connessi</br>Trovare il numero di serie hello</br>Trovare la destinazione di hello IQN |Servizio StorSimple Manager → Dispositivi → Dashboard |[Utilizzare i dashboard del dispositivo StorSimple hello](storsimple-device-dashboard.md) |
| Creare grafici di monitoraggio |Servizio StorSimple Manager → Dispositivi → Monitora |[Monitoraggio del dispositivo StorSimple](storsimple-monitor-device.md) |
| Aggiungere un contenitore del volume</br>Modificare un contenitore di volumi</br>Eliminare un contenitore del volume |Servizio StorSimple Manager → Dispositivi → Contenitori dei volumi |[Gestisci contenitori dei volumi](storsimple-manage-volume-containers.md) |
| Aggiungere un volume</br>Modificare un volume</br>Portare un volume offline</br>Eliminare un volume</br>Monitorare un volume |Servizio StorSimple Manager → Dispositivi → Contenitori dei volumi → Volumi |[Gestire i volumi](storsimple-manage-volumes.md) |
| Modificare le impostazioni del dispositivo</br>Modificare le impostazioni di tempo</br>Modificare le impostazioni DNS.md</br>Configurare le interfacce di rete |Servizio StorSimple Manager → Dispositivi → Configura |[Modificare la configurazione per il dispositivo StorSimple](storsimple-modify-device-config.md) |
| Visualizzare le impostazioni proxy Web |Servizio StorSimple Manager → Dispositivi → Configura |[Configurare il proxy Web per il dispositivo](storsimple-configure-web-proxy.md) |
| Modificare la password amministratore del dispositivo</br>Modificare la password di Gestione snapshot StorSimple |Servizio StorSimple Manager → Dispositivi → Configura |[Modificare le password di StorSimple](storsimple-change-passwords.md) |
| Configurare la gestione remota |Servizio StorSimple Manager → Dispositivi → Configura |[Connettersi in remoto il dispositivo di StorSimple tooyour](storsimple-remote-connect.md) |
| Configurare le impostazioni degli avvisi |Servizio StorSimple Manager → Dispositivi → Configura |[Visualizzare e gestire gli avvisi di StorSimple](storsimple-manage-alerts.md) |
| Configurare CHAP per il dispositivo StorSimple |Servizio StorSimple Manager → Dispositivi → Configura |[Configurare CHAP per il dispositivo StorSimple](storsimple-configure-chap.md) |
| Aggiungere un criterio di backup</br>Aggiungere o modificare una pianificazione</br>Eliminare un criterio di backup</br>Creazione di un backup manuale</br>Creare un criterio di backup personalizzato con più volumi e pianificazioni |Servizio StorSimple Manager → Dispositivi → Criteri di backup |[Gestire i criteri di backup](storsimple-manage-backup-policies.md) |
| Arrestare i controller dei dispositivi</br>Riavviare i controller dei dispositivi</br>Arrestare i controller dei dispositivi</br>Reimpostare le impostazioni predefinite del dispositivo toofactory</br>(I valori precedenti sono solo per il dispositivo locale) |Servizio StorSimple Manager → Dispositivi → Manutenzione |[Gestire il controller del dispositivo StorSimple](storsimple-manage-device-controller.md) |
| Informazioni sui componenti hardware di StorSimple</br>Monitorare lo stato dell'hardware</br>(I valori precedenti sono solo per il dispositivo locale) |Servizio StorSimple Manager → Dispositivi → Manutenzione |[Monitorare i componenti hardware](storsimple-monitor-hardware-status.md) |
| Creare un pacchetto di supporto |Servizio StorSimple Manager → Dispositivi → Manutenzione |[Creare e gestire un pacchetto di supporto](storsimple-create-manage-support-package.md) |
| Installare gli aggiornamenti del software |Servizio StorSimple Manager → Dispositivi → Manutenzione |[Aggiornare il dispositivo](storsimple-update-device.md) |

## <a name="next-steps"></a>Passaggi successivi
Se si verificano problemi con quotidiana hello del dispositivo StorSimple o con uno qualsiasi dei relativi componenti hardware, vedere:

* [Risoluzione dei problemi relativi a un dispositivo operativo](storsimple-troubleshoot-operational-device.md)
* [Utilizzare gli indicatori LED di monitoraggio di StorSimple](storsimple-monitoring-indicators.md)

Se non è possibile risolvere i problemi di hello ed è necessario toocreate una richiesta di servizio, fare riferimento troppo[contattare il supporto tecnico Microsoft](storsimple-contact-microsoft-support.md).


---
title: interfaccia utente di gestione Snapshot aaaStorSimple | Documenti Microsoft
description: Descrive l'interfaccia utente di StorSimple Snapshot Manager hello e illustra come toouse, i processi di backup toomanage e hello del catalogo di backup.
services: storsimple
documentationcenter: NA
author: SharS
manager: timlt
editor: 
ms.assetid: c7d91892-2881-41a2-a7a2-908dc3646493
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: TBD
ms.date: 06/05/2017
ms.author: v-sharos
ms.custom: 
ms.openlocfilehash: 865520fdaf1b559714b52b428ad136b084d65c99
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="use-storsimple-snapshot-manager-user-interface-toomanage-backup-jobs-and-backup-catalog"></a>Usare Gestione Snapshot StorSimple utente interfaccia toomanage i processi di backup e di catalogo di backup

## <a name="overview"></a>Panoramica
Gestione Snapshot StorSimple Hello è un'interfaccia utente intuitiva che è possibile utilizzare tootake e gestire i backup. In questa esercitazione fornisce un'interfaccia utente di introduzione toohello e quindi viene illustrato come toouse componenti hello. Per una descrizione dettagliata di hello gestione Snapshot StorSimple, vedere [che cos'è StorSimple Snapshot Manager?](storsimple-what-is-snapshot-manager.md)

### <a name="console-description"></a>Descrizione della console
utente hello tooview interfaccia, fare clic sull'icona di gestione Snapshot StorSimple hello sul desktop. verrà visualizzata la finestra di console Hello, come illustrato nella seguente figura hello.

![Riquadri di StorSimple Snapshot Manager](./media/storsimple-use-snapshot-manager/HCS_SSM_gui_panes.png)

finestra di console Hello ha cinque elementi principali. Fare clic sul collegamento appropriato di hello per una descrizione completa di ogni elemento.

* [Barra dei menu](#menu-bar) 
* [Barra degli strumenti](#tool-bar) 
* [Riquadro Ambito](#scope-pane) 
* [Riquadro Risultati](#results-pane) 
* [Riquadro Azioni](#actions-pane) 

Inoltre, hello supporta gestione Snapshot StorSimple [tasti di navigazione e un numero di tasti di scelta rapida](#keyboard-navigation-and-shortcuts).

### <a name="console-accessibility"></a>Accessibilità della console
interfaccia utente di StorSimple Snapshot Manager Hello supporta funzionalità di accessibilità di hello fornite dal sistema operativo di Windows hello e hello Microsoft Management Console (MMC), nonché alcuni tasti di scelta rapida specifici di gestione Snapshot StorSimple. 

* Per una descrizione delle funzionalità di accessibilità di Windows hello, andare troppo[tasti di scelta rapida per Windows](https://support.microsoft.com/kb/126449). 
* Per una descrizione delle funzionalità di accessibilità MMC hello, andare troppo[accessibilità per MMC 3.0](https://technet.microsoft.com/library/cc766075.aspx)
* Per una descrizione delle funzionalità di accessibilità di gestione Snapshot StorSimple hello, andare troppo[tasti di scelta rapida e navigazione](#keyboard-navigation-and-shortcuts).

## <a name="menu-bar"></a>Barra dei menu
barra dei menu nella parte superiore di hello della finestra della console hello Hello contiene [File](#file-menu), [azione](#action-menu), [vista](#view-menu), [Preferiti](#favorites-menu), [finestra ](#window-menu), e [Guida](#help-menu) menu.

Fare clic su qualsiasi elemento hello menu barra toosee un elenco dei comandi disponibili nel menu. Hello riportato di seguito hello **vista** menu selezionato nella barra dei menu hello.

![Menu Visualizza selezionato](./media/storsimple-use-snapshot-manager/HCS_SSM_View_menu.png)

### <a name="file-menu"></a>File menu
Hello **File** menu contiene i comandi standard di Microsoft Management Console (MMC).

#### <a name="menu-access"></a>Accesso al menu
hello tooview **File** menu, fare clic su **File** sulla barra dei menu hello. Hello seguenti dal menu visualizzato.

![Menu File di StorSimple Snapshot Manager](./media/storsimple-use-snapshot-manager/HCS_SSM_FileMenu.png) 

#### <a name="menu-description"></a>Descrizione del menu
Hello nella tabella seguente descrive gli elementi visualizzati in hello **File** menu.

| Voce di menu | Descrizione |
|:--- |:--- |
| Nuovo |Fare clic su **New** toocreate in base una nuova console di gestione Snapshot StorSimple hello. |
| Apri |Fare clic su **aprire** tooopen una console esistente. |
| Salva |Fare clic su **salvare** toosave console corrente di hello. |
| Salva con nome |Fare clic su **Salva con nome** toocreate una nuova istanza rinominata della console corrente hello. Hello utilizzare **Salva con nome** opzione toocustomize una vista e salvarla per poterla recuperare in seguito. Ad esempio, è possibile creare snap-in di gestione Snapshot StorSimple tale server toospecific punto. |
| Aggiungi/Rimuovi snap-in |Fare clic su **Aggiungi/Rimuovi Snap-in** tooadd o Rimuovi snap-in e tooorganize nodi hello **ambito** riquadro. Per ulteriori informazioni, visitare troppo[Add, Remove e organizzare Snap-in ed estensioni in MMC 3.0](https://technet.microsoft.com/library/cc722035.aspx). |
| Opzioni |Fare clic su **opzioni** toochange hello console, specificare la modalità di accesso utente e autorizzazioni oppure eliminare lo spazio disponibile su disco di tooincrease i file di console. |
| Elenco dei percorsi di file |Fare clic su un percorso nell'elenco di hello numerato tooreopen un file aperto di recente. |
| Esci |Fare clic su **uscita** tooclose hello **File** menu. |

### <a name="action-menu"></a>Menu Azione
Hello utilizzare **azione** tooselect menu Azioni disponibili. Hello elementi disponibili tooyou dipendono dalla selezione di hello apportate hello **ambito** riquadro o **risultati** riquadro.

#### <a name="menu-access"></a>Accesso al menu
hello tooview **azione** menu, effettuare una delle seguenti hello:

* Fare doppio clic su un elemento in hello **ambito** riquadro o **risultati** riquadro.
* Selezionare un elemento in hello **ambito** riquadro o **risultati** riquadro e quindi fare clic su **azione** sulla barra dei menu hello. 

Ad esempio, se si seleziona nodo principale hello in hello **ambito** riquadro e quindi i pulsante destro del mouse oppure fare clic su **azione** sulla barra dei menu hello, hello menu riportato di seguito viene visualizzata.

![Menu Azione di StorSimple Snapshot Manager](./media/storsimple-use-snapshot-manager/HCS_SSM_Action_menu.png)

Hello **azioni** riquadro (Buongiorno destra della console hello) contiene hello stesso elenco di azioni di hello **azione** menu. Inoltre, hello **azioni** riquadro contiene hello **vista** opzioni di menu, che consentono una visualizzazione personalizzata di hello toocreate **risultati** riquadro.

![Riquadro Azioni con menu Visualizza aperto](./media/storsimple-use-snapshot-manager/HCS_SSM_ActionsPane_Results.png)

#### <a name="menu-description"></a>Descrizione del menu
Hello nella tabella seguente contiene un elenco alfabetico di azioni di gestione Snapshot StorSimple. 

* Hello **azione** colonna elenca le azioni che è possibile eseguire sui nodi e i risultati. 
* Hello **navigazione** colonna spiega come toodisplay hello appropriato **azione** menu in modo che è possibile selezionare l'azione di hello. Alcune azioni vengono visualizzate in più menu **Azione** . Per eseguire queste azioni, selezionare una **navigazione** opzione dall'elenco puntato hello. 
* Hello **descrizione** colonna descrive come toouse ciascuna azione hello **azione** menu o il riquadro azioni e viene spiegato cosa accade.

> [!NOTE]
> Hello **azioni** riquadro e **azione** menu contengono opzioni aggiuntive, ad esempio **vista**, **nuova finestra da qui**,  **Aggiorna**, **Esporta elenco**, e **Guida**. Queste opzioni sono disponibili come parte di hello MMC e non sono specifiche tooStorSimple gestione Snapshot. tabella Hello include descrizioni di queste opzioni.
> 
> 

| Azione | Navigazione | Descrizione |
|:--- |:--- |:--- |
| Autentica |Fare clic su hello **dispositivi** nodo e un dispositivo in hello rapida **risultati** riquadro. |Fare clic su **Authenticate** password hello tooenter configurata per il dispositivo hello. |
| Clone |Espandere **catalogo di Backup**, espandere **gli snapshot Cloud**, fare clic su un backup con data di validità e quindi selezionare un volume in hello **risultati** riquadro. |Fare clic su **Clone** toocreate una copia di un cloud di snapshot e archiviarlo in una posizione designata. |
| Configurare un dispositivo |Pulsante destro del mouse hello **dispositivi** nodo. |Fare clic su **configurare un dispositivo** tooconfigure uno o più host di Windows dal toohello tooconnect dispositivi. |
| Crea criterio di backup |Eseguire una delle seguenti hello:<ul><li>Fare clic con il pulsante destro del mouse su **Criteri di backup**.</li><li>Fare clic o espandere **Gruppi volumi**, quindi fare clic con il pulsante destro del mouse su un gruppo di volumi.</li><li>Fare clic o espandere **Catalogo backup**, quindi fare clic con il pulsante destro del mouse su un gruppo di volumi.</li></ul> |Fare clic su **Crea criteri di Backup** tooconfigure un backup pianificato per un gruppo di volumi. |
| Crea gruppo di volumi |Eseguire una delle seguenti hello:<ul><li>Fare clic su hello **volumi** nodo e quindi fare un volume in hello **risultati** riquadro.</li><li>Pulsante destro del mouse hello **gruppi di volumi** nodo.</li></ul> |Fare clic su **Crea gruppo di volumi** gruppo di volumi tooa tooassign volumi. |
| Elimina |Fare clic su un nodo o su un risultato; questa voce viene visualizzata in diversi menu **Azione** e riquadri **Azioni**. |Fare clic su **eliminare** toodelete hello nodo o un risultato selezionato. Quando viene visualizzata la finestra di dialogo di conferma hello, confermare o annullare l'eliminazione di hello. |
| Dettagli |Fare clic su hello **dispositivi** nodo e quindi fare un dispositivo in hello **risultati** riquadro. |Fare clic su **dettagli** dettagli di configurazione di hello toosee per un dispositivo. |
| Modificare |Fare clic su **criteri di Backup**e quindi fare doppio clic su un criterio di hello **risultati** riquadro. |Fare clic su **modifica** pianificazione del backup hello toochange per un gruppo di volumi. |
| Esporta elenco |Fare clic su un nodo o su un risultato. Questa voce viene visualizzata in tutti i menu **Azione** e i riquadri **Azioni**. |Fare clic su **Esporta elenco** toosave un elenco in un file con valori delimitato da virgole (CSV). È quindi possibile importare questo file in un’applicazione foglio di calcolo per l'analisi. |
| Guida |Fare clic su un nodo o su un risultato. Questa voce viene visualizzata in tutti i menu **Azione** e i riquadri **Azioni**. |Fare clic su **Guida** tooopen Guida in linea in una finestra distinta del browser. |
| Nuova finestra da qui |Fare clic su un nodo o su un risultato. Questa voce viene visualizzata in tutti i menu **Azione** e i riquadri **Azioni**. |Fare clic su **nuova finestra da qui** tooopen una nuova finestra di gestione Snapshot StorSimple. |
| Aggiorna |Fare clic su un nodo o su un risultato. Questa voce viene visualizzata in tutti i menu **Azione** e i riquadri **Azioni**. |Fare clic su **aggiornamento** finestra di gestione Snapshot StorSimple tooupdate hello attualmente visualizzato. |
| Aggiorna dispositivo |Fare clic su hello **dispositivi** nodo e un dispositivo in hello rapida **risultati** riquadro. |Fare clic su **Aggiorna dispositivo** toosynchronize un dispositivo connesso specifico con StorSimple Snapshot Manager. |
| Aggiorna dispositivi |Pulsante destro del mouse hello **dispositivi** nodo. |Fare clic su **Aggiorna dispositivi** toosynchronize all'elenco di dispositivi connessi con StorSimple Snapshot Manager. |
| Ripetere la scansione dei volumi |Pulsante destro del mouse hello **volumi** nodo. |Fare clic su **Ripeti analisi dei volumi** tooupdate hello elenco dei volumi in hello **risultati** riquadro. |
| Ripristino |Espandere **Catalogo backup**, espandere un gruppo di volumi, quindi **Snapshot locali** o **Snapshot cloud** e fare clic con il pulsante destro del mouse su un backup. |Fare clic su **ripristinare** tooreplace hello corrente volume raggruppare i dati con i dati di backup selezionati hello hello. |
| Esegui backup |Eseguire una delle seguenti hello:<ul><li>Espandere **Gruppi volumi**, quindi fare clic con il pulsante destro del mouse su un gruppo di volumi.</li><li>Espandere **Catalogo backup**, quindi fare clic con il pulsante destro del mouse su un gruppo di volumi.</li></ul> |Fare clic su **Esegui Backup** toostart immediatamente un processo di backup. |
| Visualizza/Nascondi importazioni |Nodo principale di hello pulsante destro del mouse in hello **ambito** riquadro (hello **gestione Snapshot StorSimple** nodo negli esempi di hello). |Fare clic su **Visualizza/Nascondi importazioni** tooshow o nascondere i gruppi di volumi hello e i backup associati sono stati importati da hello dashboard del servizio di gestione di dispositivi StorSimple. |

### <a name="view-menu"></a>Menu Visualizza
Hello utilizzare **vista** toocreate menu una visualizzazione personalizzata di hello **risultati** contenuto riquadro. Hello **vista** menu contiene **Aggiungi/Rimuovi colonne** e **Personalizza** opzioni.

#### <a name="menu-access"></a>Accesso al menu
È possibile accedere hello **vista** dal menu sulla barra dei menu hello o hello **azioni** riquadro.

![Menu Visualizza di StorSimple Snapshot Manager](./media/storsimple-use-snapshot-manager/HCS_SSM_View_menu.png) 

#### <a name="menu-description"></a>Descrizione del menu
Hello nella tabella seguente descrive gli elementi visualizzati in hello **vista** menu.

| Voce di menu | Descrizione |
|:--- |:--- |
| Aggiungi/Rimuovi colonne |Fare clic su **Aggiungi/Rimuovi colonne** tooadd o rimuovere colonne in hello **risultati** riquadro. |
| Personalizza |Fare clic su **Personalizza** tooshow o nascondere gli elementi nella finestra di console di gestione Snapshot StorSimple hello. |

### <a name="favorites-menu"></a>Menu Preferiti
Utilizzare hello **Preferiti** tooadd menu, rimuovere e organizzare le visualizzazioni di pagina e le attività di uso frequente. 

#### <a name="menu-access"></a>Accesso al menu
È possibile accedere hello **Preferiti** menu sulla barra dei menu hello.

![Menu Preferiti di StorSimple Snapshot Manager](./media/storsimple-use-snapshot-manager/HCS_SSM_FavoritesMenu.png)

#### <a name="menu-description"></a>Descrizione del menu
Hello nella tabella seguente descrive gli elementi visualizzati in hello **Preferiti** menu.

| Voce di menu | Descrizione |
|:--- |:--- |
| Aggiungere tooFavorites |Fare clic su **aggiungere tooFavorites** tooadd hello vista tooyour elenco corrente dei Preferiti. |
| Organizza Preferiti |Fare clic su **Organizza Preferiti** contenuto hello tooorganize della cartella Preferiti. |

### <a name="window-menu"></a>Menu Finestra
Hello utilizzare **finestra** menu tooadd e ridisporre gestione Snapshot StorSimple finestre della console.

#### <a name="menu-access"></a>Accesso al menu
È possibile accedere hello **finestra** menu sulla barra dei menu hello.

![Menu Finestra di StorSimple Snapshot Manager](./media/storsimple-use-snapshot-manager/HCS_SSM_WindowMenu.png)

elenco numerato di Hello nella parte inferiore di hello del menu hello Mostra hello finestre attualmente aperte. Fare clic su qualsiasi finestra nella finestra elenco toobring hello in primo piano hello. 

#### <a name="menu-description"></a>Descrizione del menu
Hello nella tabella seguente vengono descritti hello elementi visualizzati nel menu finestra hello.

| Voce di menu | Descrizione |
|:--- |:--- |
| Nuova finestra |Fare clic su **nuova finestra** tooopen una nuova finestra della console (in una finestra esistente toohello aggiunta). |
| Sovrapponi |Fare clic su **Cascade** finestre aperte della console di hello toodisplay in uno stile CSS. |
| Affianca orizzontalmente |Fare clic su **Affianca orizzontalmente** finestre aperte della console di hello toodisplay sotto forma di riquadro (o griglia). |
| Disponi icone |Se si dispone di più console di windows aprire e sparpagliate sul desktop, ridurle e quindi fare clic su **Disponi icone** tooarrange multipla in una riga orizzontale nella parte inferiore di hello dello schermo. |

### <a name="help-menu"></a>Menu Guida
Hello utilizzare **Guida** menu tooview Guida disponibile online per gestione Snapshot StorSimple e hello MMC. È inoltre possibile visualizzare informazioni hello MMC e gestione Snapshot StorSimple versioni del software che sono attualmente installati nel sistema. 

È possibile accedere hello **Guida** menu sulla barra dei menu hello. È possibile accedere anche gli argomenti della Guida di gestione Snapshot StorSimple da hello **azioni** riquadro.

![Menu Guida di StorSimple Snapshot Manager](./media/storsimple-use-snapshot-manager/HCS_SSM_HelpMenu.png)

#### <a name="menu-description"></a>Descrizione del menu
Hello nella tabella seguente descrive gli elementi visualizzati nel menu Guida hello.

| Voce di menu | Descrizione |
|:--- |:--- |
| Guida di StorSimple Snapshot Manager |Fare clic su **Guida StorSimple Snapshot Manager** tooopen della Guida di gestione Snapshot StorSimple in una finestra separata. |
| Argomenti della Guida |Fare clic su **argomenti della Guida** tooopen Guida di MMC in una finestra separata. |
| Sito Web TechCenter |Fare clic su **sito Web TechCenter** home page per tooopen hello Microsoft TechNet Tech Center in una finestra separata. |
| Informazioni su Microsoft Management Console |Fare clic su **informazioni su Microsoft Management Console** toosee quale versione di hello Microsoft Management Console è installato nel sistema. |
| Informazioni su StorSimple Snapshot Manager |Fare clic su **su StorSimple Snapshot Manager** toosee quale versione di hello snap-in è installata nel sistema. |

## <a name="tool-bar"></a>Barra degli strumenti
barra degli strumenti Hello, che si trova sotto la barra dei menu hello contiene icone di attività e di navigazione. Ogni icona rappresenta un'attività specifica tooa di scelta rapida.

### <a name="icon-descriptions"></a>Descrizioni delle icone
Hello nella tabella seguente sono descritte hello icone visualizzate sulla barra degli strumenti hello. 

| Icona | Descrizione |
|:--- |:--- |
| ![Freccia sinistra](./media/storsimple-use-snapshot-manager/HCS_SSM_LeftArrow.png) |Fare clic sulla pagina precedente di hello freccia sinistra icona tooreturn toohello. |
| ![Freccia destra](./media/storsimple-use-snapshot-manager/HCS_SSM_RightArrow.png) |Fare clic sulla pagina successiva di hello freccia destra toogo toohello (se hello freccia è grigia, azione hello è disponibile). |
| ![Icona su](./media/storsimple-use-snapshot-manager/HCS_SSM_Up.png) |Fare clic su hello backup icona toogo al superiore livello nella struttura della console hello (hello **ambito** riquadro). |
| ![Mostra/Nascondi albero della console](./media/storsimple-use-snapshot-manager/HCS_SSM_ShowConsoleTree.png) |Fare clic su hello Mostra/Nascondi console albero icona tooshow o nascondere hello **ambito** riquadro. |
| ![Esporta elenco](./media/storsimple-use-snapshot-manager/HCS_SSM_ExportListIcon.png) |Fare clic su hello esportazione elenco icona tooexport un file CSV tooa elenco specificato. |
| ![Icona della guida](./media/storsimple-use-snapshot-manager/HCS_SSM_HelpIcon.png) |Fare clic su hello Guida icona tooopen un argomento della Guida MMC in linea. |
| ![Mostra/Nascondi riquadro Azioni](./media/storsimple-use-snapshot-manager/HCS_SSM_ShowAction.png) |Fare clic su Mostra/Nascondi hello **azioni** hello di tooshow o Nascondi icona riquadro **azioni** riquadro. |

## <a name="scope-pane"></a>Riquadro Ambito
Hello **ambito** hello riquadro all'estrema sinistra in hello UI gestione Snapshot StorSimple. Contiene una struttura ad albero console (o nodo) hello ed è il meccanismo di spostamento principale hello gestione Snapshot StorSimple. 

### <a name="scope-pane-structure"></a>Struttura del riquadro Ambito
Hello **ambito** riquadro contiene una serie di oggetti selezionabili (nodi) organizzata in una struttura ad albero. 

![Riquadro Ambito](./media/storsimple-use-snapshot-manager/HCS_SSM_Scope_pane.png) 

* tooexpand o comprimere un nodo, fare clic su hello freccia icona Avanti toohello nome del nodo.
* stato di hello tooview o il contenuto di un nodo, fare clic su nome del nodo hello. Hello informazione viene visualizzata nel hello **risultati** riquadro. 

Hello **ambito** riquadro contiene hello seguenti nodi: 

* [Nodo Dispositivi](#devices-node) 
* [Nodo Volumi](#volumes-node) 
* [Nodo Gruppi volumi](#volume-groups-node) 
* [Nodo Criteri di backup](#backup-policies-node) 
* [Nodo Catalogo di backup](#backup-catalog-node) 
* [Nodo Processi](#jobs-node) 

### <a name="scope-pane-tasks"></a>Attività riquadro Ambito
È possibile utilizzare hello **ambito** riquadro toocomplete un'azione su un nodo specifico. tooselect un'attività, eseguire una delle seguenti hello:

* Nodo hello e quindi scegliere attività hello dal menu di scelta rapida hello.
* Fare clic sul nodo hello e quindi fare clic su **azione** sulla barra dei menu hello. Selezionare l'attività hello dal menu di scelta rapida hello.
* Fare clic su nodo hello e quindi selezionare hello in hello **azioni** riquadro.

Quando si seleziona un nodo e utilizza uno di questi metodi toosee un elenco di attività, vengono visualizzate solo le azioni che possono essere eseguite su tale nodo.

### <a name="devices-node"></a>Nodo Dispositivi
Hello **dispositivi** nodo rappresenta dispositivi StorSimple hello e i dispositivi virtuali StorSimple che sono connessi tooStorSimple gestione Snapshot. Selezionare tooconnect questo nodo e configurare un dispositivo e importare relativi volumi associati, i gruppi di volumi e copie di backup esistenti. Più dispositivi possono essere connesso tooa singolo host.

* nodo hello tooexpand, fare clic su freccia hello Avanti troppo**dispositivi**.
* toosee un menu di azioni disponibili, fare doppio clic su hello **dispositivi** nodo o rapida vista tutti i nodi che vengono visualizzati in hello hello ingrandita.
* Fare clic su un elenco di dispositivi configurati, toosee **dispositivi** in hello **ambito** riquadro. elenco di Hello dei dispositivi, insieme alle informazioni su ogni dispositivo, viene visualizzato nel hello **risultati** riquadro.

### <a name="volumes-node"></a>Nodo Volumi
Hello **volumi** nodo rappresenta le unità hello corrispondenti toohello volumi montati dall'host di hello, inclusi quelli individuati tramite iSCSI e quelli individuati tramite un dispositivo. Utilizzare questo elenco di hello tooview di nodo di volumi disponibili e assegnare volumi singoli gruppi toovolume.

* nodo hello tooexpand, fare clic su freccia hello Avanti troppo**volumi**.
* toosee un menu di azioni disponibili, fare doppio clic su hello **volumi** nodo o rapida vista tutti i nodi che vengono visualizzati in hello hello ingrandita.
* Fare clic su un elenco di volumi, toosee **volumi** in hello **ambito** riquadro. viene visualizzato l'elenco di Hello di volumi, insieme alle informazioni su ogni volume, in hello **risultati** riquadro.

### <a name="volume-groups-node"></a>Nodo Gruppi volumi
I gruppi di volumi sono noti anche come gruppi di coerenza. Ogni gruppo di volumi è un pool di volumi correlati alle applicazioni che consente la coerenza delle applicazioni tooensure durante le operazioni di backup. Hello utilizzare **gruppi di volumi** tooconfigure nodo questi gruppi e i backup interattivo tootake o creare pianificazioni di backup. 

* nodo hello tooexpand, fare clic su freccia hello Avanti troppo**gruppi di volumi**.
* toosee un menu di azioni disponibili, fare doppio clic su hello **gruppi di volumi** nodo o rapida vista tutti i nodi che vengono visualizzati in hello hello ingrandita.
* Fare clic su un elenco di gruppi di volumi, toosee **gruppi di volumi** in hello **ambito** riquadro. elenco di Hello di gruppi di volumi, insieme alle informazioni su ogni gruppo di volumi, vengono visualizzati nel hello **risultati** riquadro.

### <a name="backup-policies-node"></a>Nodo Criteri di backup
I criteri di backup sono pianificazioni dei processi per snapshot locali e cloud. Hello utilizzare **criteri di Backup** nodo toospecify la frequenza con cui viene creato un backup e per quanto tempo una copia di backup debba essere mantenuti. 

* nodo hello tooexpand, fare clic su freccia hello Avanti troppo**criteri di Backup**.
* toosee un menu di azioni disponibili, fare doppio clic su hello **criteri di Backup** nodo o rapida vista tutti i nodi che vengono visualizzati in hello hello ingrandita.
* Fare clic su un elenco di criteri di backup, toosee **criteri di Backup** in hello **ambito** riquadro. elenco di Hello di criteri di backup, insieme alle informazioni su tutti i criteri, viene visualizzato nel hello **risultati** riquadro.

> [!NOTE]
> È possibile conservare un massimo di 64 backup.


### <a name="backup-catalog-node"></a>Nodo Catalogo di backup
Hello **catalogo di Backup** nodo contiene elenchi di backup in sede e fuori sede di volumi StorSimple di Azure. Questo nodo viene organizzato per gruppo di volumi e ciascun contenitore gruppo di volumi contiene strutture separate per snapshot locali (hello **Snapshot locale**nodo s) e gli snapshot cloud (hello **gli snapshot Cloud** nodo ). Quando viene espanso, ogni contenitore gruppo di volumi Elenca tutti i backup riusciti hello che sono stati eseguiti in modo interattivo o da un criterio configurato.

* nodo hello tooexpand, fare clic su freccia hello Avanti troppo**catalogo di Backup**.
* toosee un menu di azioni disponibili, fare doppio clic su hello **catalogo di Backup** nodo o rapida vista tutti i nodi che vengono visualizzati in hello hello ingrandita.
* Fare clic su un elenco di snapshot di backup, toosee **catalogo di Backup** in hello **ambito** riquadro. elenco di Hello di snapshot, insieme alle informazioni su ogni snapshot, viene visualizzato nel hello **risultati** riquadro.

### <a name="local-snapshots-node"></a>Nodo Snapshot locali
Hello **gli snapshot locali** nodo sono elencati gli snapshot locali per un gruppo di volumi specifico. nodo Hello si trova sotto hello **catalogo di Backup** nodo hello **ambito** riquadro. Gli snapshot locali sono copie punto nel tempo dei dati di volume archiviati nel dispositivo Azure StorSimple hello. In genere, questo tipo di backup può essere creato e ripristinato rapidamente. È possibile utilizzare uno snapshot locale come copia di backup locale.

* nodo hello tooexpand, fare clic su freccia hello Avanti troppo**gli snapshot locali**.
* toosee un menu di azioni disponibili, fare doppio clic su hello **gli snapshot locali** nodo o rapida vista tutti i nodi che vengono visualizzati in hello hello ingrandita.
* Fare clic su un elenco di snapshot locali, toosee **gli snapshot locali** in hello **ambito** riquadro. elenco di Hello di snapshot, insieme alle informazioni su ogni snapshot, viene visualizzato nel hello **risultati** riquadro.

### <a name="cloud-snapshots-node"></a>Nodo Snapshot cloud
Hello **gli snapshot Cloud** nodo sono elencati gli snapshot cloud per un gruppo di volumi specifico. nodo Hello si trova sotto hello **catalogo di Backup** nodo hello **ambito** riquadro. Gli snapshot cloud sono copie punto nel tempo dei dati di volume archiviati nel cloud hello. Uno snapshot cloud equivale tooa snapshot replicato su un sistema di archiviazione fuori sede diversi. Gli snapshot cloud sono particolarmente utili negli scenari di ripristino di emergenza.

* nodo hello tooexpand, fare clic su freccia hello Avanti troppo**gli snapshot Cloud**.
* toosee un menu di azioni disponibili, fare doppio clic su hello **gli snapshot Cloud** nodo o rapida vista tutti i nodi che vengono visualizzati in hello hello ingrandita.
* Fare clic su un elenco di snapshot nel cloud, toosee **gli snapshot Cloud** in hello **ambito** riquadro. elenco di Hello di snapshot, insieme alle informazioni su ogni snapshot, viene visualizzato nel hello **risultati** riquadro.

### <a name="jobs-node"></a>Nodo Processi
Hello **processi** nodo contiene informazioni sui processi di backup pianificati, in esecuzione e completati di recente. 

* nodo hello tooexpand, fare clic su freccia hello Avanti troppo**processi**.
* toosee un menu di azioni disponibili, fare doppio clic su hello **processi** nodo o rapida vista tutti i nodi che vengono visualizzati in hello hello ingrandita.
* toosee un elenco dei processi pianificati, espandere hello **processi** nodo e quindi fare clic su **pianificato**. Hello elenco di processi configurati in precedenza e informazioni su ogni processo viene visualizzato in hello **risultati** riquadro. 
* un elenco di processi completati di recente, toosee espandere hello **processi** nodo e quindi fare clic su **ultime 24 ore**. Viene visualizzato un elenco di processi completati nelle hello ultime 24 ore in hello **risultati** riquadro. Hello **risultati** riquadro contiene anche informazioni su ogni processo completato.
* toosee un elenco di processi attualmente in esecuzione, espandere hello **processi** nodo e quindi fare clic su **esecuzione**. viene visualizzato l'elenco di Hello di attualmente in esecuzione processi e informazioni su ogni processo in hello **risultati** riquadro.

## <a name="results-pane"></a>Riquadro Risultati
Hello **risultati** riquadro center hello in hello UI gestione Snapshot StorSimple. Contiene elenchi e informazioni dettagliate sullo stato per il nodo hello selezionato in hello **ambito** riquadro.

### <a name="example"></a>Esempio
hello toosee seguente esempio, fare clic su hello **gruppi di volumi** nodo hello **ambito** riquadro. Hello **risultati** riquadro viene visualizzato un elenco di gruppi di volumi con informazioni dettagliate su ogni gruppo.

![Riquadro Risultati](./media/storsimple-use-snapshot-manager/HCS_SSM_Results_pane.png) 

È possibile configurare i dettagli di hello mostrati nel hello **risultati** riquadro: fare doppio clic su un nodo in hello **ambito** riquadro, fare clic su **vista**, quindi fare clic su **Aggiungi/Rimuovi Colonne**.

## <a name="actions-pane"></a>Riquadro Azioni
Hello **azioni** riquadro di destra hello in hello UI gestione Snapshot StorSimple. Contiene un menu di operazioni che è possibile eseguire sul nodo hello, vista o sui dati che si seleziona in hello **ambito** riquadro o **risultati** riquadro. Hello **azioni** riquadro contiene hello stesso comandi come hello **azione** i menu disponibili per gli elementi di hello **ambito** riquadro e **risultati**riquadro. Per una descrizione di ogni azione, vedere la tabella hello in hello **azione** sezione del menu.

### <a name="examples"></a>esempi
hello toosee seguente esempio, in hello **ambito** riquadro espandere hello **processi** nodo e fare clic su **pianificato**. Hello **azioni** riquadro vengono visualizzate le azioni disponibili per hello hello **pianificato** nodo.

![Esempio processi pianificati nel riquadro Azioni](./media/storsimple-use-snapshot-manager/HCS_SSM_ActionsPane.png) 

toosee altre opzioni, in hello **ambito** riquadro espandere hello **processi** nodo, fare clic su **pianificato**, quindi fare clic su un processo pianificato in hello **risultati**riquadro. Hello **azioni** riquadro vengono visualizzate le azioni disponibili per il processo pianificato hello, hello, come illustrato nell'esempio seguente hello.

![Esempio azioni del processo nel riquadro Azioni](./media/storsimple-use-snapshot-manager/HCS_SSM_ActionsPane_Results.png)

## <a name="keyboard-navigation-and-shortcuts"></a>Navigazione da tastiera e tasti di scelta rapida
Gestione Snapshot StorSimple Abilita le funzionalità di accessibilità di hello del sistema operativo di Windows hello e hello Microsoft Management Console (MMC). Include inoltre alcune funzionalità di navigazione da tastiera e tasti di scelta rapida sono specifico toohello gestione Snapshot StorSimple, come descritto in hello le sezioni seguenti.

* [Tasti di navigazione da tastiera](#keyboard-navigation-keys) 
* [Tasti di scelta rapida della barra dei menu](#menu-bar-shortcut-keys) 
* [Tasti di scelta rapida del riquadro Ambito](#scope-pane-shortcut-keys) 

### <a name="keyboard-navigation-keys"></a>Tasti di navigazione da tastiera
Hello nella tabella seguente vengono descritte hello chiavi che è possibile utilizzare l'interfaccia utente di gestione Snapshot StorSimple hello toonavigate. 

| Tasto di navigazione | Azione |
|:--- |:--- |
| Tasto freccia giù |Utilizzare hello toomove chiave sulla freccia verso il basso in verticale toohello elemento successivo in un menu o un riquadro. |
| Immettere |Premere hello invio chiave toocomplete un'azione e quindi procedere toohello successivo. Ad esempio, è possibile premere INVIO tooselect **Avanti**, **OK**, o **crea**, quindi andare toohello il passaggio successivo in una procedura guidata. |
| ESC |Premere hello Esc chiave tooclose un menu o toocancel e chiudere una pagina. |
| F1 |Premere hello F1 chiave tooview un argomento della Guida per la finestra attualmente attiva di hello. |
| F5 |Premere hello F5 chiave toorefresh un nodo. |
| F6 |Premere toomove di chiave F6 hello da hello **ambito** riquadro toohello **risultati** riquadro. |
| F10 |Premere barra dei menu toohello toogo chiave hello F10. |
| Tasto freccia sinistra |Utilizzare hello orizzontalmente a sinistra toomove chiave freccia opzione di menu barra opzione toohello precedente. Quando si sposta toohello precedente viene visualizzato il menu elemento hello menu barra, azione hello (o contesto) per l'elemento precedente hello. |
| Tasto freccia destra |Utilizzare toomove chiave sulla freccia a destra di hello in senso orizzontale da un menu barra toohello opzione. Quando si sposta toohello successivo elemento hello menu barra, azione hello (o contesto) menu nuovo elemento hello. |
| Tasto TAB |Utilizzare riquadro successivo di hello scheda toomove chiave toohello su hello console o toohello successiva selezione o casella di testo in una pagina. |
| Tasto freccia su |Utilizzare hello backup toomove chiave freccia verticalmente toohello elemento precedente in un menu o un riquadro. |

### <a name="menu-bar-shortcut-keys"></a>Tasti di scelta rapida della barra dei menu
Hello nella tabella seguente descrive hello tasti di scelta rapida per la barra dei menu hello. Dopo che si premono i tasti di scelta rapida hello e verrà visualizzato il menu di hello, è possibile utilizzare i tasti di scelta rapida (hello tasti sottolineati nel menu hello). Per ulteriori informazioni sulla barra dei menu hello, andare troppo[barra dei Menu](#menu-bar).

| Tasto di scelta rapida | Risultato | Tasti di scelta rapida del menu | Risultato |
|:--- |:--- |:--- |:--- |
| ALT + F |Verrà visualizzata la hello **File** menu. |N |Consente di aprire l’istanza di una nuova console. |
|  |O |Verrà visualizzata la hello **strumenti di amministrazione** pagina. | |
|  |S |Salva una console di gestione Snapshot StorSimple hello. | |
|  |Una  |Verrà visualizzata la hello **Salva con nome** pagina. | |
|  |M |Verrà visualizzata la hello **Aggiungi/Rimuovi Snap-in** pagina. | |
|  |P |Verrà visualizzata la hello **opzioni** pagina. | |
|  |H |Consente di aprire la guida in linea. | |
| ALT + A |Verrà visualizzata la hello **azione** menu. |I |Attiva e disattiva l'opzione di visualizzazione di importazione hello. |
|  |W |Consente di aprire una nuova console di StorSimple Snapshot Manager. | |
|  |F |Aggiorna console di gestione Snapshot StorSimple hello. | |
|  |L |Verrà visualizzata la hello **Esporta elenco** pagina. | |
|  |H |Consente di aprire la guida in linea. | |
| ALT + V |Verrà visualizzata la hello **vista** menu. |Una  |Verrà visualizzata la hello **Aggiungi/Rimuovi colonne** pagina. |
|  |U |Verrà visualizzata la hello **Personalizza visualizzazione** pagina. | |
| ALT + O |Verrà visualizzata la hello **Preferiti** menu. |Una  |Verrà visualizzata la hello **aggiungere tooFavorites** pagina. |
|  |O |Verrà visualizzata la hello **Organizza Preferiti** pagina. | |
| ALT + W |Verrà visualizzata la hello **finestra** menu. |N |Consente di aprire un'altra finestra di StorSimple Snapshot Manager. |
|  |C |Consente di visualizzare tutte le finestre della console aperte in uno stile a cascata. | |
|  |T |Consente di visualizzare tutte le finestre della console aperte in motivo di griglia. | |
|  |I |Dispone le icone in una riga orizzontale nella parte inferiore di hello dello schermo. | |
| ALT + H |Verrà visualizzata la hello **Guida** menu. |H |Consente di aprire la guida in linea. |
|  |T |Verrà visualizzata la pagina web di Microsoft TechNet Tech Center hello. | |
|  |Una  |Verrà visualizzata la hello **informazioni su Microsoft Management Console** pagina. | |

### <a name="scope-pane-shortcut-keys"></a>Tasti di scelta rapida del riquadro Ambito
Hello nelle tabelle seguenti viene scelta rapida hello combinazioni di tasti per ogni nodo in hello **ambito** riquadro. 

* [Tasti di scelta rapida del nodo Dispositivi](#devices-node-shortcut-keys)
* [Tasti di scelta rapida del nodo Volumi](#volumes-node-shortcut-keys)
* [Tasti di scelta rapida del nodo Gruppi di volumi](#volume-groups-node-shortcut-keys)
* [Tasti di scelta rapida del nodo Criteri di backup](#backup-policies-node-shortcut-keys)
* [Tasti di scelta rapida del nodo Catalogo di backup](#backup-catalog-node-shortcut-keys)
* [Tasti di scelta rapida del nodo Processi](#jobs-node-shortcut-keys)

#### <a name="devices-node-shortcut-keys"></a>Tasti di scelta rapida del nodo Dispositivi
| Tasti di scelta rapida del menu | Risultato |
|:--- |:--- |
| C |Verrà visualizzata la hello **configurare un dispositivo** pagina. |
| D |Aggiorna elenco hello di dispositivi e i dettagli. |
| V |Verrà visualizzata la hello **vista** menu. |
| W |Apre una nuova console di gestione Snapshot StorSimple con stato attivo su hello **dettagli** nodo. |
| F |Aggiorna console di gestione Snapshot StorSimple hello. |
| L |Verrà visualizzata la hello **Esporta elenco** pagina. |
| H |Consente di aprire la guida in linea. |

#### <a name="volumes-node-shortcut-keys"></a>Tasti di scelta rapida del nodo Volumi
| Tasti di scelta rapida del menu | Risultato |
|:--- |:--- |
| V |Elenco di aggiornamenti hello di volumi. |
| V (premere due volte) |Verrà visualizzata la hello **vista** menu. |
| W |Apre una nuova console di gestione Snapshot StorSimple con stato attivo su hello **volumi** nodo. |
| F |Aggiorna console di gestione Snapshot StorSimple hello. |
| L |Verrà visualizzata la hello **Esporta elenco** pagina. |
| H |Consente di aprire la guida in linea. |

#### <a name="volume-groups-node-shortcut-keys"></a>Tasti di scelta rapida del nodo Gruppi di volumi
| Tasti di scelta rapida del menu | Risultato |
|:--- |:--- |
| G |Verrà visualizzata la hello **creare un gruppo di volumi** pagina. |
| V |Verrà visualizzata la hello **vista** menu. |
| W |Apre una nuova console di gestione Snapshot StorSimple con stato attivo su hello **gruppi di volumi** nodo. |
| F |Aggiorna console di gestione Snapshot StorSimple hello. |
| L |Verrà visualizzata la hello **Esporta elenco** pagina. |
| H |Consente di aprire la guida in linea. |

#### <a name="backup-policies-node-shortcut-keys"></a>Tasti di scelta rapida del nodo Criteri di backup
| Tasti di scelta rapida del menu | Risultato |
|:--- |:--- |
| B |Verrà visualizzata la hello **creare un criterio** pagina. |
| V |Verrà visualizzata la hello **vista** menu. |
| W |Apre una nuova console di gestione Snapshot StorSimple con stato attivo su hello **gruppi di volumi** nodo. |
| F |Aggiorna console di gestione Snapshot StorSimple hello. |
| L |Verrà visualizzata la hello * * Esporta elenco * * pagina. |
| H |Consente di aprire la guida in linea. |

#### <a name="backup-catalog-node-shortcut-keys"></a>Tasti di scelta rapida del nodo Catalogo di backup
| Tasti di scelta rapida del menu | Risultato |
|:--- |:--- |
| W |Apre una nuova console di gestione Snapshot StorSimple con stato attivo su hello **gruppi di volumi** nodo. |
| F |Aggiorna console di gestione Snapshot StorSimple hello. |
| H |Consente di aprire la guida in linea. |

#### <a name="jobs-node-shortcut-keys"></a>Tasti di scelta rapida del nodo Processi
| Tasti di scelta rapida del menu | Risultato |
|:--- |:--- |
| V |Verrà visualizzata la hello **vista** menu. |
| W |Apre una nuova console di gestione Snapshot StorSimple con stato attivo su hello **processi** nodo. |
| F |Aggiorna console di gestione Snapshot StorSimple hello. |
| L |Verrà visualizzata la hello **Esporta elenco** pagina. |
| H |Consente di aprire la guida in linea. |

## <a name="next-steps"></a>Passaggi successivi
* Informazioni su come troppo[usare Gestione Snapshot StorSimple tooadminister la soluzione StorSimple](storsimple-snapshot-manager-admin.md).
* Informazioni su come troppo[tooconnect StorSimple Snapshot Manager di utilizzare e gestire i dispositivi](storsimple-snapshot-manager-manage-devices.md).


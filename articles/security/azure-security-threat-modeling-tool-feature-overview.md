---
title: aaaMicrosoft dello strumento di modellazione minaccia, Azure | Documenti Microsoft
description: "Informazioni su tutte le funzionalità di hello disponibili in hello strumento di modellazione delle minacce"
services: security
documentationcenter: na
author: RodSan
manager: RodSan
editor: RodSan
ms.assetid: na
ms.service: security
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/17/2017
ms.author: rodsan
ms.openlocfilehash: f9ad5e623e7758063084cb7fc723c5735161a846
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="threat-modeling-tool-feature-overview"></a>Panoramica della funzione Threat Modeling Tool

Siamo lieti di sapere che scelto hello toouse strumento di modellazione delle minacce per le esigenze di modellazione. Se non è ancora fatto, visitare  **[introduzione hello strumento di modellazione delle minacce](./azure-security-threat-modeling-tool-getting-started.md)**  toolearn nozioni fondamentali di hello.

> Lo strumento viene aggiornato spesso, controllare questa guida toosee spesso la funzionalità e i miglioramenti più recenti.

Fare clic sul pulsante "Crea un nuovo modello" hello, verrà visualizzata una pagina iniziale vuota, l'immagine toohello simile sotto:

![Pagina iniziale vuota](./media/azure-security-threat-modeling-tool/tmtstart.png)

Utilizzando il modello di minaccia hello creato dal nostro team in hello  **[Introduzione](./azure-security-threat-modeling-tool-getting-started.md)**  esempio analizziamo di oggi tutte le funzionalità di hello disponibile nello strumento hello.

![Modello di minaccia di base](./media/azure-security-threat-modeling-tool/basictmt.png)

## <a name="navigation"></a>Navigazione

Prima di entrare nel funzionalità incorporate di hello, è opportuno discutere i componenti principali di hello presenti nello strumento hello

### <a name="menu-items"></a>Voci di menu

esperienza di Hello deve essere prodotti Microsoft tooother analoghi. Iniziamo attraverso le voci di menu di primo livello hello:

![Voci di menu](./media/azure-security-threat-modeling-tool/menuitems.png)

| Etichetta                               | Dettagli      |
| --------------------------------------- | ------------ |
| **File** | <ul><li>Aprire, salvare e chiudere i file</li><li>Accedere e disconnettersi dagli account di OneDrive</li><li>Condividere collegamenti (visualizzazione + modifica)</li><li>Visualizzare le informazioni di file</li><li>Applicare i modelli di tooExisting nuovo modello</li></ul> |
| **Modifica** | Annullare/ripristinare azioni, nonché copia, incolla ed elimina |
| **Visualizza** | <ul><li>Passare fra le visualizzazioni **Analisi** e **Progettazione**</li><li>Aprire finestre chiuse (ad es. stencil, proprietà degli elementi e messaggi)</li><li>Ripristinare le impostazioni di layout toodefault</li></ul> |
| **Diagramma** | Aggiungere/eliminare diagrammi e spostarsi tra le "schede" dei diagrammi |
| **Report** | Creare tooshare report HTML con altri utenti |
| **Guida** | Lo strumento di hello toohelp di guide |

icone di Hello sono tasti di scelta rapida per i menu di primo livello hello:

| Icona                               | Dettagli      |
| --------------------------------------- | ------------ |
| **Apri** | Apre un nuovo file |
| **Salva** | Salva il file corrente |
| **Progettazione** | Passa alla visualizzazione progettazione dove è possibile creare modelli |
| **Analizzare** | Mostra le minacce generate e le relative proprietà |
| **Aggiungi diagramma** | Aggiunge di nuovo diagramma (simile toonew schede in Excel) |
| **Elimina diagramma** | Elimina il diagramma corrente |
| **Copia/Taglia/Incolla** | Copia/taglia /incolla elementi |
| **Annulla/Ripeti** | Annulla/ripete azioni |
| **Zoom avanti/Zoom indietro** | Esegue lo zoom avanti e indietro diagramma hello per una migliore visualizzazione |
| **Commenti e suggerimenti** | Apre hello Forum MSDN |

### <a name="canvas"></a>Canvas

spazio di Hello in cui si trascinano gli elementi. Trascinamento della selezione è hello più rapido e modelli di toobuild modo più efficienti. È anche possibile fare clic e scegliere dal menu di hello, che aggiunge le versioni generiche degli elementi di hello in uso, come illustrato di seguito.

#### <a name="dropping-hello-stencil-on-hello-canvas"></a>Eliminazione di uno stencil di hello nell'area di disegno hello

![Rilascio sul canvas](./media/azure-security-threat-modeling-tool/canvasdrop1.png)

#### <a name="clicking-on-hello-stencil"></a>Facendo clic su uno stencil di hello

![Proprietà dell'elemento](./media/azure-security-threat-modeling-tool/canvasdrop2.png)

### <a name="stencils"></a>Stencil

In cui è possibile trovare tutti stencil disponibili toouse basato sul modello hello selezionato. Se non è possibile trovare gli elementi a destra di hello, provare a utilizzare un altro modello o modificare uno toofit le proprie esigenze. In genere, deve essere in grado di toofind una combinazione di categorie come hello quelli di sotto:

| Nome dello stencil                               | Dettagli      |
| --------------------------------------- | ------------ |
| **Processo** | Applicazioni, plugin del browser, minacce, macchine virtuali |
| **Interazione esterna** | Provider di autenticazione, browser, utenti, applicazioni Web |
| **Archivio dati** | Cache, archiviazione, file di configurazione, database, registro |
| **Flusso di dati** | File binario, ALPC, HTTP, HTTPS/TLS/SSL, IOCTL, IPSec, named pipe, RPC/DCOM, SMB, UDP |
| **Linea di trust/limite perimetrale** | Reti aziendali, Internet, computer, Sandbox, modalità utente/kernel |

### <a name="notesmessages"></a>Note/messaggi

| Componente                               | Dettagli      |
| --------------------------------------- | ------------ |
| **Messaggi** | Logica dello strumento interno che avvisa gli utenti ogni volta che si verifica un errore, ad esempio l'assenza di flusso di dati tra gli elementi |
| **Note** | File toohello aggiunta manuale di note dal team di progettazione per l'intero hello progettazione e processo di revisione |

### <a name="element-properties"></a>Proprietà dell'elemento

Questi variano in base a elementi hello selezionati. Oltre ai limiti di trust, tutti gli altri elementi contengono 3 selezioni generali:

| Proprietà dell'elemento                               | Dettagli      |
| --------------------------------------- | ------------ |
| **Nome** | Utile per la denominazione toobe i processi, archivi, chi interagisce dall'e flussi facilmente riconosciuto |
| **Fuori ambito** | Se selezionata, l'elemento hello viene escluso dalla matrice di generazione di minaccia hello (scelta non consigliata) |
| **Ragioni per il fuori ambito** | Gli utenti di giustificazione campo toolet conoscono il motivo per cui è stato selezionato dall'ambito |

Vengono modificate le proprietà sotto ogni categoria di elemento. Fare clic su ogni elemento tooinspect hello le opzioni disponibili, o aprire hello modello toolearn altre. Iniziamo in funzionalità hello.

## <a name="welcome-screen"></a>Schermata iniziale

schermata di Hello viene innanzitutto hello che viene visualizzato quando si apre l'applicazione hello.

### <a name="open-a-model"></a>Aprire un modello

Passando con il mouse sul pulsante "Apri un modello" vengono visualizzate 2 opzioni nascoste: "Apri da questo computer" e "Apri da OneDrive". Hello apre prima schermata Apri File hello, mentre hello secondo vengono illustrati hello processo di accesso per OneDrive, consentendo di file e cartelle toopick dopo il completamento dell'autenticazione.

![Aprire un modello](./media/azure-security-threat-modeling-tool/openmodel.png)

![Aprire dal computer o da OneDrive](./media/azure-security-threat-modeling-tool/openmodel2.png)

### <a name="feedback-suggestions-and-issues"></a>Commenti, suggerimenti e problemi

Se si seleziona questa opzione si passerà toohello forum di MSDN per gli strumenti di SDL. È toocheck un modo efficace le opinioni di altri utenti su strumento di hello, incluse nuove idee e soluzioni alternative.

![Commenti e suggerimenti](./media/azure-security-threat-modeling-tool/feedback.png)

## <a name="design-view"></a>Visualizzazione progettazione

Ogni volta che si apre o si crea un nuovo modello, verrà visualizzato Progettazione toohello.

### <a name="adding-elements"></a>Aggiunta di elementi

Esistono 2 metodi tooadd elementi sulla griglia hello:

- **Trascinare e rilasciare** -trascinare hello elemento desiderato toohello griglia, quindi utilizzare informazioni aggiuntive tooprovide hello elemento proprietà.
- **Fare clic destro** : fare clic in un punto qualsiasi della griglia hello e scegliere dal menu a discesa hello. Una rappresentazione generica di tale elemento verrà visualizzato nella schermata di hello.

### <a name="connecting-elements"></a>Collegamento di elementi

Esistono 2 metodi tooconnect elementi nello strumento hello:

- **Trascinare e rilasciare** : trascinare griglia toohello di hello desiderata del flusso di dati e connettere entrambi gli elementi appropriati di toohello termina.
- **Fare clic su + MAIUSC** : fare clic sul primo elemento hello (invio di dati), premere e tenere premuto MAIUSC hello quindi secondo elemento selezionare hello (ricezione di dati). Fare clic con il pulsante destro del mouse e selezionare "Connetti". Se si utilizza un flusso di dati bidirezionale, ordine di hello non è importante.

### <a name="properties"></a>Proprietà

Mostra tutte le proprietà di hello che possono essere modificate in stencil hello inserito nel diagramma hello. proprietà hello toosee, fare clic su uno stencil di hello e informazioni hello verranno popolate di conseguenza. esempio Hello riportato di seguito mostra prima e dopo un stencil viene trascinato sul diagramma hello "Database":

#### <a name="before"></a>Prima

![Prima](./media/azure-security-threat-modeling-tool/properties1.png)

#### <a name="after"></a>Dopo

![Dopo](./media/azure-security-threat-modeling-tool/properties2.png)

### <a name="messages"></a>Messaggi

Se si crea un modello di minacce e si dimentica di fluiscono di dati tooconnect tooelements, finestra di messaggio hello notifica tooact. È possibile scegliere tooignore o seguire hello problema hello toofix di istruzioni. 

![Messaggi](./media/azure-security-threat-modeling-tool/messages.png)

### <a name="notes"></a>Note

Cambio di schede da messaggi tooNotes consente tutte le proprie opinioni si tooadd note tooyour diagramma toocapture

## <a name="analysis-view"></a>Visualizzazione analisi

Dopo aver completato la creazione del diagramma, passare tooanalysis visualizzazione selezionando le selezioni di menu in alto toohello e scegliendo hello lente di ingrandimento Avanti toohello tavolozza.

![Visualizzazione analisi](./media/azure-security-threat-modeling-tool/analysisview.png)

### <a name="generated-threat-selection"></a>Selezione di minacce generata

Quando si fa clic su una minaccia, è possibile sfruttare tre funzioni uniche:

| Funzionalità                               | Info      |
| --------------------------------------- | ------------ |
| **Indicatore letto** | <p>Minaccia viene contrassegnato come lettura, che può facilmente consentono di tenere traccia degli elementi di hello che già parlato</p><p>![Indicatore letto/non letto](./media/azure-security-threat-modeling-tool/readmode.png)</p> |
| **Centro di interazione** | <p>Interazione nel diagramma hello appartenenti toothat minaccia viene evidenziato</p><p>![Centro di interazione](./media/azure-security-threat-modeling-tool/interactionfocus.png)</p> |
| **Proprietà della minaccia** | <p>Informazioni aggiuntive sulla minaccia hello viene popolate nella finestra proprietà di hello minaccia</p><p>![Proprietà della minaccia](./media/azure-security-threat-modeling-tool/threatproperties.png)</p> |

### <a name="priority-change"></a>Modifica della priorità

Livello di priorità hello di ciascuna minaccia generato modifica anche i relativi toomake colori è facile tooidentify minacce di priorità alta, Media e bassa.

![Modifica della priorità](./media/azure-security-threat-modeling-tool/prioritychange.png)

### <a name="threat-properties-editable-fields"></a>Campi modificabili delle proprietà della minaccia

Come illustrato nell'immagine di hello precedente, gli utenti possono modificare le informazioni di hello generate dallo strumento hello un anche aggiungere informazioni toocertain campi, ad esempio giustificazione. Questi campi vengono generati dal modello hello, pertanto se sono necessarie ulteriori informazioni per ogni minaccia, consigliabile toomake modifiche.

![Proprietà della minaccia](./media/azure-security-threat-modeling-tool/threatproperties.png)

## <a name="reports"></a>Report

Dopo aver completato la modifica delle priorità e lo stato degli aggiornamenti di hello di ogni generato minaccia, è possibile salvare il file hello e/o stampare un report passando troppo "Report" e quindi "Creazione di Report completo." Verrà chiesto report hello tooname e una volta eseguita, verrà visualizzato un codice simile immagine toohello riportata di seguito:

![Report](./media/azure-security-threat-modeling-tool/report.png)

## <a name="next-steps"></a>Passaggi successivi

toocontribute un modello per la community di hello, visitare tooour  **[GitHub](https://github.com/Microsoft/threat-modeling-templates)**  pagina. **[Scaricare](https://aka.ms/tmtpreview)**  tooget strumento hello subito.

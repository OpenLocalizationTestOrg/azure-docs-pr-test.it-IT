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
# <a name="threat-modeling-tool-feature-overview"></a><span data-ttu-id="93684-103">Panoramica della funzione Threat Modeling Tool</span><span class="sxs-lookup"><span data-stu-id="93684-103">Threat Modeling Tool feature overview</span></span>

<span data-ttu-id="93684-104">Siamo lieti di sapere che scelto hello toouse strumento di modellazione delle minacce per le esigenze di modellazione.</span><span class="sxs-lookup"><span data-stu-id="93684-104">We are glad you chose toouse hello Threat Modeling Tool for your threat modeling needs!</span></span> <span data-ttu-id="93684-105">Se non è ancora fatto, visitare  **[introduzione hello strumento di modellazione delle minacce](./azure-security-threat-modeling-tool-getting-started.md)**  toolearn nozioni fondamentali di hello.</span><span class="sxs-lookup"><span data-stu-id="93684-105">If you haven’t done so, visit **[Getting Started with hello Threat Modeling Tool](./azure-security-threat-modeling-tool-getting-started.md)** toolearn hello basics.</span></span>

> <span data-ttu-id="93684-106">Lo strumento viene aggiornato spesso, controllare questa guida toosee spesso la funzionalità e i miglioramenti più recenti.</span><span class="sxs-lookup"><span data-stu-id="93684-106">Our tool is updated often, so check this guide often toosee our latest features and improvements.</span></span>

<span data-ttu-id="93684-107">Fare clic sul pulsante "Crea un nuovo modello" hello, verrà visualizzata una pagina iniziale vuota, l'immagine toohello simile sotto:</span><span class="sxs-lookup"><span data-stu-id="93684-107">Clicking on hello "Create a New Model" button opens a blank start page, similar toohello image below:</span></span>

![Pagina iniziale vuota](./media/azure-security-threat-modeling-tool/tmtstart.png)

<span data-ttu-id="93684-109">Utilizzando il modello di minaccia hello creato dal nostro team in hello  **[Introduzione](./azure-security-threat-modeling-tool-getting-started.md)**  esempio analizziamo di oggi tutte le funzionalità di hello disponibile nello strumento hello.</span><span class="sxs-lookup"><span data-stu-id="93684-109">Using hello threat model created by our team in hello **[Getting Started](./azure-security-threat-modeling-tool-getting-started.md)** example, let’s check out all hello features available in hello tool today.</span></span>

![Modello di minaccia di base](./media/azure-security-threat-modeling-tool/basictmt.png)

## <a name="navigation"></a><span data-ttu-id="93684-111">Navigazione</span><span class="sxs-lookup"><span data-stu-id="93684-111">Navigation</span></span>

<span data-ttu-id="93684-112">Prima di entrare nel funzionalità incorporate di hello, è opportuno discutere i componenti principali di hello presenti nello strumento hello</span><span class="sxs-lookup"><span data-stu-id="93684-112">Before diving into hello built-in features, let’s go over hello main components found in hello tool</span></span>

### <a name="menu-items"></a><span data-ttu-id="93684-113">Voci di menu</span><span class="sxs-lookup"><span data-stu-id="93684-113">Menu items</span></span>

<span data-ttu-id="93684-114">esperienza di Hello deve essere prodotti Microsoft tooother analoghi.</span><span class="sxs-lookup"><span data-stu-id="93684-114">hello experience should be similar tooother Microsoft products.</span></span> <span data-ttu-id="93684-115">Iniziamo attraverso le voci di menu di primo livello hello:</span><span class="sxs-lookup"><span data-stu-id="93684-115">Let’s begin by going through hello top-level menu items:</span></span>

![Voci di menu](./media/azure-security-threat-modeling-tool/menuitems.png)

| <span data-ttu-id="93684-117">Etichetta</span><span class="sxs-lookup"><span data-stu-id="93684-117">Label</span></span>                               | <span data-ttu-id="93684-118">Dettagli</span><span class="sxs-lookup"><span data-stu-id="93684-118">Details</span></span>      |
| --------------------------------------- | ------------ |
| <span data-ttu-id="93684-119">**File**</span><span class="sxs-lookup"><span data-stu-id="93684-119">**File**</span></span> | <ul><li><span data-ttu-id="93684-120">Aprire, salvare e chiudere i file</span><span class="sxs-lookup"><span data-stu-id="93684-120">Open, Save and Close Files</span></span></li><li><span data-ttu-id="93684-121">Accedere e disconnettersi dagli account di OneDrive</span><span class="sxs-lookup"><span data-stu-id="93684-121">Sign In/Out of OneDrive accounts</span></span></li><li><span data-ttu-id="93684-122">Condividere collegamenti (visualizzazione + modifica)</span><span class="sxs-lookup"><span data-stu-id="93684-122">Share Links (View + Edit)</span></span></li><li><span data-ttu-id="93684-123">Visualizzare le informazioni di file</span><span class="sxs-lookup"><span data-stu-id="93684-123">View File Information</span></span></li><li><span data-ttu-id="93684-124">Applicare i modelli di tooExisting nuovo modello</span><span class="sxs-lookup"><span data-stu-id="93684-124">Apply New Template tooExisting Models</span></span></li></ul> |
| <span data-ttu-id="93684-125">**Modifica**</span><span class="sxs-lookup"><span data-stu-id="93684-125">**Edit**</span></span> | <span data-ttu-id="93684-126">Annullare/ripristinare azioni, nonché copia, incolla ed elimina</span><span class="sxs-lookup"><span data-stu-id="93684-126">Undo/redo actions, as well a copy, paste and delete</span></span> |
| <span data-ttu-id="93684-127">**Visualizza**</span><span class="sxs-lookup"><span data-stu-id="93684-127">**View**</span></span> | <ul><li><span data-ttu-id="93684-128">Passare fra le visualizzazioni **Analisi** e **Progettazione**</span><span class="sxs-lookup"><span data-stu-id="93684-128">Switch between **Analysis** and **Design** views</span></span></li><li><span data-ttu-id="93684-129">Aprire finestre chiuse (ad es. stencil, proprietà degli elementi e messaggi)</span><span class="sxs-lookup"><span data-stu-id="93684-129">Open closed windows (e.g.stencils, element properties and messages)</span></span></li><li><span data-ttu-id="93684-130">Ripristinare le impostazioni di layout toodefault</span><span class="sxs-lookup"><span data-stu-id="93684-130">Reset layout toodefault settings</span></span></li></ul> |
| <span data-ttu-id="93684-131">**Diagramma**</span><span class="sxs-lookup"><span data-stu-id="93684-131">**Diagram**</span></span> | <span data-ttu-id="93684-132">Aggiungere/eliminare diagrammi e spostarsi tra le "schede" dei diagrammi</span><span class="sxs-lookup"><span data-stu-id="93684-132">Add/Delete diagrams and navigate through “tabs” of diagrams</span></span> |
| <span data-ttu-id="93684-133">**Report**</span><span class="sxs-lookup"><span data-stu-id="93684-133">**Reports**</span></span> | <span data-ttu-id="93684-134">Creare tooshare report HTML con altri utenti</span><span class="sxs-lookup"><span data-stu-id="93684-134">Create HTML reports tooshare with others</span></span> |
| <span data-ttu-id="93684-135">**Guida**</span><span class="sxs-lookup"><span data-stu-id="93684-135">**Help**</span></span> | <span data-ttu-id="93684-136">Lo strumento di hello toohelp di guide</span><span class="sxs-lookup"><span data-stu-id="93684-136">Guides toohelp you use hello tool</span></span> |

<span data-ttu-id="93684-137">icone di Hello sono tasti di scelta rapida per i menu di primo livello hello:</span><span class="sxs-lookup"><span data-stu-id="93684-137">hello icons are shortcuts for hello top-level menus:</span></span>

| <span data-ttu-id="93684-138">Icona</span><span class="sxs-lookup"><span data-stu-id="93684-138">Icon</span></span>                               | <span data-ttu-id="93684-139">Dettagli</span><span class="sxs-lookup"><span data-stu-id="93684-139">Details</span></span>      |
| --------------------------------------- | ------------ |
| <span data-ttu-id="93684-140">**Apri**</span><span class="sxs-lookup"><span data-stu-id="93684-140">**Open**</span></span> | <span data-ttu-id="93684-141">Apre un nuovo file</span><span class="sxs-lookup"><span data-stu-id="93684-141">Opens a new file</span></span> |
| <span data-ttu-id="93684-142">**Salva**</span><span class="sxs-lookup"><span data-stu-id="93684-142">**Save**</span></span> | <span data-ttu-id="93684-143">Salva il file corrente</span><span class="sxs-lookup"><span data-stu-id="93684-143">Saves current file</span></span> |
| <span data-ttu-id="93684-144">**Progettazione**</span><span class="sxs-lookup"><span data-stu-id="93684-144">**Design**</span></span> | <span data-ttu-id="93684-145">Passa alla visualizzazione progettazione dove è possibile creare modelli</span><span class="sxs-lookup"><span data-stu-id="93684-145">Goes into design view, where you can create models</span></span> |
| <span data-ttu-id="93684-146">**Analizzare**</span><span class="sxs-lookup"><span data-stu-id="93684-146">**Analyze**</span></span> | <span data-ttu-id="93684-147">Mostra le minacce generate e le relative proprietà</span><span class="sxs-lookup"><span data-stu-id="93684-147">Shows generated threats and their properties</span></span> |
| <span data-ttu-id="93684-148">**Aggiungi diagramma**</span><span class="sxs-lookup"><span data-stu-id="93684-148">**Add Diagram**</span></span> | <span data-ttu-id="93684-149">Aggiunge di nuovo diagramma (simile toonew schede in Excel)</span><span class="sxs-lookup"><span data-stu-id="93684-149">Adds new diagram (similar toonew tabs in Excel)</span></span> |
| <span data-ttu-id="93684-150">**Elimina diagramma**</span><span class="sxs-lookup"><span data-stu-id="93684-150">**Delete Diagram**</span></span> | <span data-ttu-id="93684-151">Elimina il diagramma corrente</span><span class="sxs-lookup"><span data-stu-id="93684-151">Deletes current diagram</span></span> |
| <span data-ttu-id="93684-152">**Copia/Taglia/Incolla**</span><span class="sxs-lookup"><span data-stu-id="93684-152">**Copy/Cut/Paste**</span></span> | <span data-ttu-id="93684-153">Copia/taglia /incolla elementi</span><span class="sxs-lookup"><span data-stu-id="93684-153">Copies/cuts/pastes elements</span></span> |
| <span data-ttu-id="93684-154">**Annulla/Ripeti**</span><span class="sxs-lookup"><span data-stu-id="93684-154">**Undo/Redo**</span></span> | <span data-ttu-id="93684-155">Annulla/ripete azioni</span><span class="sxs-lookup"><span data-stu-id="93684-155">Undoes/redoes actions</span></span> |
| <span data-ttu-id="93684-156">**Zoom avanti/Zoom indietro**</span><span class="sxs-lookup"><span data-stu-id="93684-156">**Zoom In/Zoom Out**</span></span> | <span data-ttu-id="93684-157">Esegue lo zoom avanti e indietro diagramma hello per una migliore visualizzazione</span><span class="sxs-lookup"><span data-stu-id="93684-157">Zooms in and out of hello diagram for a better view</span></span> |
| <span data-ttu-id="93684-158">**Commenti e suggerimenti**</span><span class="sxs-lookup"><span data-stu-id="93684-158">**Feedback**</span></span> | <span data-ttu-id="93684-159">Apre hello Forum MSDN</span><span class="sxs-lookup"><span data-stu-id="93684-159">Opens hello MSDN Forum</span></span> |

### <a name="canvas"></a><span data-ttu-id="93684-160">Canvas</span><span class="sxs-lookup"><span data-stu-id="93684-160">Canvas</span></span>

<span data-ttu-id="93684-161">spazio di Hello in cui si trascinano gli elementi.</span><span class="sxs-lookup"><span data-stu-id="93684-161">hello space where you drag and drop elements into.</span></span> <span data-ttu-id="93684-162">Trascinamento della selezione è hello più rapido e modelli di toobuild modo più efficienti.</span><span class="sxs-lookup"><span data-stu-id="93684-162">Drag and drop is hello quickest and most efficient way toobuild models.</span></span> <span data-ttu-id="93684-163">È anche possibile fare clic e scegliere dal menu di hello, che aggiunge le versioni generiche degli elementi di hello in uso, come illustrato di seguito.</span><span class="sxs-lookup"><span data-stu-id="93684-163">You may also right click and select from hello menu, which adds generic versions of hello elements you’re using, as shown below.</span></span>

#### <a name="dropping-hello-stencil-on-hello-canvas"></a><span data-ttu-id="93684-164">Eliminazione di uno stencil di hello nell'area di disegno hello</span><span class="sxs-lookup"><span data-stu-id="93684-164">Dropping hello stencil on hello canvas</span></span>

![Rilascio sul canvas](./media/azure-security-threat-modeling-tool/canvasdrop1.png)

#### <a name="clicking-on-hello-stencil"></a><span data-ttu-id="93684-166">Facendo clic su uno stencil di hello</span><span class="sxs-lookup"><span data-stu-id="93684-166">Clicking on hello stencil</span></span>

![Proprietà dell'elemento](./media/azure-security-threat-modeling-tool/canvasdrop2.png)

### <a name="stencils"></a><span data-ttu-id="93684-168">Stencil</span><span class="sxs-lookup"><span data-stu-id="93684-168">Stencils</span></span>

<span data-ttu-id="93684-169">In cui è possibile trovare tutti stencil disponibili toouse basato sul modello hello selezionato.</span><span class="sxs-lookup"><span data-stu-id="93684-169">Where you can find all stencils available toouse based on hello template selected.</span></span> <span data-ttu-id="93684-170">Se non è possibile trovare gli elementi a destra di hello, provare a utilizzare un altro modello o modificare uno toofit le proprie esigenze.</span><span class="sxs-lookup"><span data-stu-id="93684-170">If you can’t find hello right elements, try using another template, or modify one toofit your needs.</span></span> <span data-ttu-id="93684-171">In genere, deve essere in grado di toofind una combinazione di categorie come hello quelli di sotto:</span><span class="sxs-lookup"><span data-stu-id="93684-171">Generally, you should be able toofind a combination of categories like hello ones below:</span></span>

| <span data-ttu-id="93684-172">Nome dello stencil</span><span class="sxs-lookup"><span data-stu-id="93684-172">Stencil Name</span></span>                               | <span data-ttu-id="93684-173">Dettagli</span><span class="sxs-lookup"><span data-stu-id="93684-173">Details</span></span>      |
| --------------------------------------- | ------------ |
| <span data-ttu-id="93684-174">**Processo**</span><span class="sxs-lookup"><span data-stu-id="93684-174">**Process**</span></span> | <span data-ttu-id="93684-175">Applicazioni, plugin del browser, minacce, macchine virtuali</span><span class="sxs-lookup"><span data-stu-id="93684-175">Applications, Browser Plugins, Threads, Virtual Machines</span></span> |
| <span data-ttu-id="93684-176">**Interazione esterna**</span><span class="sxs-lookup"><span data-stu-id="93684-176">**External Interactor**</span></span> | <span data-ttu-id="93684-177">Provider di autenticazione, browser, utenti, applicazioni Web</span><span class="sxs-lookup"><span data-stu-id="93684-177">Authentication Providers, Browsers, Users, Web Applications</span></span> |
| <span data-ttu-id="93684-178">**Archivio dati**</span><span class="sxs-lookup"><span data-stu-id="93684-178">**Data Store**</span></span> | <span data-ttu-id="93684-179">Cache, archiviazione, file di configurazione, database, registro</span><span class="sxs-lookup"><span data-stu-id="93684-179">Cache, Storage, Configuration Files, Databases, Registry</span></span> |
| <span data-ttu-id="93684-180">**Flusso di dati**</span><span class="sxs-lookup"><span data-stu-id="93684-180">**Data Flow**</span></span> | <span data-ttu-id="93684-181">File binario, ALPC, HTTP, HTTPS/TLS/SSL, IOCTL, IPSec, named pipe, RPC/DCOM, SMB, UDP</span><span class="sxs-lookup"><span data-stu-id="93684-181">Binary, ALPC, HTTP, HTTPS/TLS/SSL, IOCTL, IPSec, Named Pipe, RPC/DCOM, SMB, UDP</span></span> |
| <span data-ttu-id="93684-182">**Linea di trust/limite perimetrale**</span><span class="sxs-lookup"><span data-stu-id="93684-182">**Trust Line/Border Boundary**</span></span> | <span data-ttu-id="93684-183">Reti aziendali, Internet, computer, Sandbox, modalità utente/kernel</span><span class="sxs-lookup"><span data-stu-id="93684-183">Corporate Networks, Internet, Machine, Sandbox, User/Kernel Mode</span></span> |

### <a name="notesmessages"></a><span data-ttu-id="93684-184">Note/messaggi</span><span class="sxs-lookup"><span data-stu-id="93684-184">Notes/Messages</span></span>

| <span data-ttu-id="93684-185">Componente</span><span class="sxs-lookup"><span data-stu-id="93684-185">Component</span></span>                               | <span data-ttu-id="93684-186">Dettagli</span><span class="sxs-lookup"><span data-stu-id="93684-186">Details</span></span>      |
| --------------------------------------- | ------------ |
| <span data-ttu-id="93684-187">**Messaggi**</span><span class="sxs-lookup"><span data-stu-id="93684-187">**Messages**</span></span> | <span data-ttu-id="93684-188">Logica dello strumento interno che avvisa gli utenti ogni volta che si verifica un errore, ad esempio l'assenza di flusso di dati tra gli elementi</span><span class="sxs-lookup"><span data-stu-id="93684-188">Internal tool logic that alerts users whenever there is an error, such as no data flows between elements</span></span> |
| <span data-ttu-id="93684-189">**Note**</span><span class="sxs-lookup"><span data-stu-id="93684-189">**Notes**</span></span> | <span data-ttu-id="93684-190">File toohello aggiunta manuale di note dal team di progettazione per l'intero hello progettazione e processo di revisione</span><span class="sxs-lookup"><span data-stu-id="93684-190">Manual notes added toohello file by engineering teams throughout hello design and review process</span></span> |

### <a name="element-properties"></a><span data-ttu-id="93684-191">Proprietà dell'elemento</span><span class="sxs-lookup"><span data-stu-id="93684-191">Element properties</span></span>

<span data-ttu-id="93684-192">Questi variano in base a elementi hello selezionati.</span><span class="sxs-lookup"><span data-stu-id="93684-192">These vary by hello elements selected.</span></span> <span data-ttu-id="93684-193">Oltre ai limiti di trust, tutti gli altri elementi contengono 3 selezioni generali:</span><span class="sxs-lookup"><span data-stu-id="93684-193">Apart from Trust Boundaries, all other elements contain 3 general selections:</span></span>

| <span data-ttu-id="93684-194">Proprietà dell'elemento</span><span class="sxs-lookup"><span data-stu-id="93684-194">Element Property</span></span>                               | <span data-ttu-id="93684-195">Dettagli</span><span class="sxs-lookup"><span data-stu-id="93684-195">Details</span></span>      |
| --------------------------------------- | ------------ |
| <span data-ttu-id="93684-196">**Nome**</span><span class="sxs-lookup"><span data-stu-id="93684-196">**Name**</span></span> | <span data-ttu-id="93684-197">Utile per la denominazione toobe i processi, archivi, chi interagisce dall'e flussi facilmente riconosciuto</span><span class="sxs-lookup"><span data-stu-id="93684-197">Useful for naming your processes, stores, interactors and flows toobe easily recognized</span></span> |
| <span data-ttu-id="93684-198">**Fuori ambito**</span><span class="sxs-lookup"><span data-stu-id="93684-198">**Out of Scope**</span></span> | <span data-ttu-id="93684-199">Se selezionata, l'elemento hello viene escluso dalla matrice di generazione di minaccia hello (scelta non consigliata)</span><span class="sxs-lookup"><span data-stu-id="93684-199">If selected, hello element is taken out of hello threat generation matrix (not recommended)</span></span> |
| <span data-ttu-id="93684-200">**Ragioni per il fuori ambito**</span><span class="sxs-lookup"><span data-stu-id="93684-200">**Reason for Out of Scope**</span></span> | <span data-ttu-id="93684-201">Gli utenti di giustificazione campo toolet conoscono il motivo per cui è stato selezionato dall'ambito</span><span class="sxs-lookup"><span data-stu-id="93684-201">Justification field toolet users know why out of scope was selected</span></span> |

<span data-ttu-id="93684-202">Vengono modificate le proprietà sotto ogni categoria di elemento.</span><span class="sxs-lookup"><span data-stu-id="93684-202">Properties are changed under each element category.</span></span> <span data-ttu-id="93684-203">Fare clic su ogni elemento tooinspect hello le opzioni disponibili, o aprire hello modello toolearn altre.</span><span class="sxs-lookup"><span data-stu-id="93684-203">Click on each element tooinspect hello available options, or open hello template toolearn more.</span></span> <span data-ttu-id="93684-204">Iniziamo in funzionalità hello.</span><span class="sxs-lookup"><span data-stu-id="93684-204">Let’s get into hello features.</span></span>

## <a name="welcome-screen"></a><span data-ttu-id="93684-205">Schermata iniziale</span><span class="sxs-lookup"><span data-stu-id="93684-205">Welcome screen</span></span>

<span data-ttu-id="93684-206">schermata di Hello viene innanzitutto hello che viene visualizzato quando si apre l'applicazione hello.</span><span class="sxs-lookup"><span data-stu-id="93684-206">hello welcome screen is hello first thing you see when you open hello app.</span></span>

### <a name="open-a-model"></a><span data-ttu-id="93684-207">Aprire un modello</span><span class="sxs-lookup"><span data-stu-id="93684-207">Open A model</span></span>

<span data-ttu-id="93684-208">Passando con il mouse sul pulsante "Apri un modello" vengono visualizzate 2 opzioni nascoste: "Apri da questo computer" e "Apri da OneDrive".</span><span class="sxs-lookup"><span data-stu-id="93684-208">Hovering over “Open a Model” button shows you 2 hidden options: “Open From this Computer” and “Open from OneDrive.”</span></span> <span data-ttu-id="93684-209">Hello apre prima schermata Apri File hello, mentre hello secondo vengono illustrati hello processo di accesso per OneDrive, consentendo di file e cartelle toopick dopo il completamento dell'autenticazione.</span><span class="sxs-lookup"><span data-stu-id="93684-209">hello first opens hello File Open screen, while hello second takes you through hello sign in process for OneDrive, allowing you toopick folders and files after a successful authentication.</span></span>

![Aprire un modello](./media/azure-security-threat-modeling-tool/openmodel.png)

![Aprire dal computer o da OneDrive](./media/azure-security-threat-modeling-tool/openmodel2.png)

### <a name="feedback-suggestions-and-issues"></a><span data-ttu-id="93684-212">Commenti, suggerimenti e problemi</span><span class="sxs-lookup"><span data-stu-id="93684-212">Feedback, suggestions and issues</span></span>

<span data-ttu-id="93684-213">Se si seleziona questa opzione si passerà toohello forum di MSDN per gli strumenti di SDL.</span><span class="sxs-lookup"><span data-stu-id="93684-213">Selecting this option will take you toohello MSDN Forums for SDL Tools.</span></span> <span data-ttu-id="93684-214">È toocheck un modo efficace le opinioni di altri utenti su strumento di hello, incluse nuove idee e soluzioni alternative.</span><span class="sxs-lookup"><span data-stu-id="93684-214">It’s a great way toocheck out what other people are saying about hello tool, including workarounds and new ideas.</span></span>

![Commenti e suggerimenti](./media/azure-security-threat-modeling-tool/feedback.png)

## <a name="design-view"></a><span data-ttu-id="93684-216">Visualizzazione progettazione</span><span class="sxs-lookup"><span data-stu-id="93684-216">Design view</span></span>

<span data-ttu-id="93684-217">Ogni volta che si apre o si crea un nuovo modello, verrà visualizzato Progettazione toohello.</span><span class="sxs-lookup"><span data-stu-id="93684-217">Whenever you open or create a new model, you’ll be taken toohello design view.</span></span>

### <a name="adding-elements"></a><span data-ttu-id="93684-218">Aggiunta di elementi</span><span class="sxs-lookup"><span data-stu-id="93684-218">Adding elements</span></span>

<span data-ttu-id="93684-219">Esistono 2 metodi tooadd elementi sulla griglia hello:</span><span class="sxs-lookup"><span data-stu-id="93684-219">There are 2 ways tooadd elements on hello grid:</span></span>

- <span data-ttu-id="93684-220">**Trascinare e rilasciare** -trascinare hello elemento desiderato toohello griglia, quindi utilizzare informazioni aggiuntive tooprovide hello elemento proprietà.</span><span class="sxs-lookup"><span data-stu-id="93684-220">**Drag and Drop** – drag hello desired element toohello grid, then use hello element properties tooprovide additional information.</span></span>
- <span data-ttu-id="93684-221">**Fare clic destro** : fare clic in un punto qualsiasi della griglia hello e scegliere dal menu a discesa hello.</span><span class="sxs-lookup"><span data-stu-id="93684-221">**Right Click** – right click anywhere on hello grid and select from hello dropdown menu.</span></span> <span data-ttu-id="93684-222">Una rappresentazione generica di tale elemento verrà visualizzato nella schermata di hello.</span><span class="sxs-lookup"><span data-stu-id="93684-222">A generic representation of that element will appear on hello screen.</span></span>

### <a name="connecting-elements"></a><span data-ttu-id="93684-223">Collegamento di elementi</span><span class="sxs-lookup"><span data-stu-id="93684-223">Connecting elements</span></span>

<span data-ttu-id="93684-224">Esistono 2 metodi tooconnect elementi nello strumento hello:</span><span class="sxs-lookup"><span data-stu-id="93684-224">There are 2 ways tooconnect elements in hello tool:</span></span>

- <span data-ttu-id="93684-225">**Trascinare e rilasciare** : trascinare griglia toohello di hello desiderata del flusso di dati e connettere entrambi gli elementi appropriati di toohello termina.</span><span class="sxs-lookup"><span data-stu-id="93684-225">**Drag and Drop** – drag hello desired dataflow toohello grid, and connect both ends toohello appropriate elements.</span></span>
- <span data-ttu-id="93684-226">**Fare clic su + MAIUSC** : fare clic sul primo elemento hello (invio di dati), premere e tenere premuto MAIUSC hello quindi secondo elemento selezionare hello (ricezione di dati).</span><span class="sxs-lookup"><span data-stu-id="93684-226">**Click + Shift** – click on hello first element (sending data), press and hold hello Shift key, then select hello second element (receiving data).</span></span> <span data-ttu-id="93684-227">Fare clic con il pulsante destro del mouse e selezionare "Connetti".</span><span class="sxs-lookup"><span data-stu-id="93684-227">Right click, and select “Connect.”</span></span> <span data-ttu-id="93684-228">Se si utilizza un flusso di dati bidirezionale, ordine di hello non è importante.</span><span class="sxs-lookup"><span data-stu-id="93684-228">If you’re using a bi-directional dataflow, hello order is not as important.</span></span>

### <a name="properties"></a><span data-ttu-id="93684-229">Proprietà</span><span class="sxs-lookup"><span data-stu-id="93684-229">Properties</span></span>

<span data-ttu-id="93684-230">Mostra tutte le proprietà di hello che possono essere modificate in stencil hello inserito nel diagramma hello.</span><span class="sxs-lookup"><span data-stu-id="93684-230">Shows all hello properties that can be modified on hello stencils placed in hello diagram.</span></span> <span data-ttu-id="93684-231">proprietà hello toosee, fare clic su uno stencil di hello e informazioni hello verranno popolate di conseguenza.</span><span class="sxs-lookup"><span data-stu-id="93684-231">toosee hello properties, just click on hello stencil and hello information will be populated accordingly.</span></span> <span data-ttu-id="93684-232">esempio Hello riportato di seguito mostra prima e dopo un stencil viene trascinato sul diagramma hello "Database":</span><span class="sxs-lookup"><span data-stu-id="93684-232">hello example below shows before and after a "Database" stencil is dragged onto hello diagram:</span></span>

#### <a name="before"></a><span data-ttu-id="93684-233">Prima</span><span class="sxs-lookup"><span data-stu-id="93684-233">Before</span></span>

![Prima](./media/azure-security-threat-modeling-tool/properties1.png)

#### <a name="after"></a><span data-ttu-id="93684-235">Dopo</span><span class="sxs-lookup"><span data-stu-id="93684-235">After</span></span>

![Dopo](./media/azure-security-threat-modeling-tool/properties2.png)

### <a name="messages"></a><span data-ttu-id="93684-237">Messaggi</span><span class="sxs-lookup"><span data-stu-id="93684-237">Messages</span></span>

<span data-ttu-id="93684-238">Se si crea un modello di minacce e si dimentica di fluiscono di dati tooconnect tooelements, finestra di messaggio hello notifica tooact.</span><span class="sxs-lookup"><span data-stu-id="93684-238">If you create a threat model and forget tooconnect data flows tooelements, hello message window notifies you tooact.</span></span> <span data-ttu-id="93684-239">È possibile scegliere tooignore o seguire hello problema hello toofix di istruzioni.</span><span class="sxs-lookup"><span data-stu-id="93684-239">You can choose tooignore it or follow hello instructions toofix hello issue.</span></span> 

![Messaggi](./media/azure-security-threat-modeling-tool/messages.png)

### <a name="notes"></a><span data-ttu-id="93684-241">Note</span><span class="sxs-lookup"><span data-stu-id="93684-241">Notes</span></span>

<span data-ttu-id="93684-242">Cambio di schede da messaggi tooNotes consente tutte le proprie opinioni si tooadd note tooyour diagramma toocapture</span><span class="sxs-lookup"><span data-stu-id="93684-242">Switching tabs from Messages tooNotes allows you tooadd notes tooyour diagram toocapture all your thoughts</span></span>

## <a name="analysis-view"></a><span data-ttu-id="93684-243">Visualizzazione analisi</span><span class="sxs-lookup"><span data-stu-id="93684-243">Analysis view</span></span>

<span data-ttu-id="93684-244">Dopo aver completato la creazione del diagramma, passare tooanalysis visualizzazione selezionando le selezioni di menu in alto toohello e scegliendo hello lente di ingrandimento Avanti toohello tavolozza.</span><span class="sxs-lookup"><span data-stu-id="93684-244">Once you're done building your diagram, switch over tooanalysis view by going toohello top menu selections and choosing hello magnifying glass next toohello paint palette.</span></span>

![Visualizzazione analisi](./media/azure-security-threat-modeling-tool/analysisview.png)

### <a name="generated-threat-selection"></a><span data-ttu-id="93684-246">Selezione di minacce generata</span><span class="sxs-lookup"><span data-stu-id="93684-246">Generated threat selection</span></span>

<span data-ttu-id="93684-247">Quando si fa clic su una minaccia, è possibile sfruttare tre funzioni uniche:</span><span class="sxs-lookup"><span data-stu-id="93684-247">When you click on a threat, you can leverage three unique functions:</span></span>

| <span data-ttu-id="93684-248">Funzionalità</span><span class="sxs-lookup"><span data-stu-id="93684-248">Feature</span></span>                               | <span data-ttu-id="93684-249">Info</span><span class="sxs-lookup"><span data-stu-id="93684-249">Info</span></span>      |
| --------------------------------------- | ------------ |
| <span data-ttu-id="93684-250">**Indicatore letto**</span><span class="sxs-lookup"><span data-stu-id="93684-250">**Read Indicator**</span></span> | <p><span data-ttu-id="93684-251">Minaccia viene contrassegnato come lettura, che può facilmente consentono di tenere traccia degli elementi di hello che già parlato</span><span class="sxs-lookup"><span data-stu-id="93684-251">Threat is now marked as read, which can easily help you keep track of hello items you already went through</span></span></p><p>![Indicatore letto/non letto](./media/azure-security-threat-modeling-tool/readmode.png)</p> |
| <span data-ttu-id="93684-253">**Centro di interazione**</span><span class="sxs-lookup"><span data-stu-id="93684-253">**Interaction Focus**</span></span> | <p><span data-ttu-id="93684-254">Interazione nel diagramma hello appartenenti toothat minaccia viene evidenziato</span><span class="sxs-lookup"><span data-stu-id="93684-254">Interaction in hello diagram belonging toothat threat is highlighted</span></span></p><p>![Centro di interazione](./media/azure-security-threat-modeling-tool/interactionfocus.png)</p> |
| <span data-ttu-id="93684-256">**Proprietà della minaccia**</span><span class="sxs-lookup"><span data-stu-id="93684-256">**Threat Properties**</span></span> | <p><span data-ttu-id="93684-257">Informazioni aggiuntive sulla minaccia hello viene popolate nella finestra proprietà di hello minaccia</span><span class="sxs-lookup"><span data-stu-id="93684-257">Additional information about hello threat is populated in hello threat properties window</span></span></p><p>![Proprietà della minaccia](./media/azure-security-threat-modeling-tool/threatproperties.png)</p> |

### <a name="priority-change"></a><span data-ttu-id="93684-259">Modifica della priorità</span><span class="sxs-lookup"><span data-stu-id="93684-259">Priority change</span></span>

<span data-ttu-id="93684-260">Livello di priorità hello di ciascuna minaccia generato modifica anche i relativi toomake colori è facile tooidentify minacce di priorità alta, Media e bassa.</span><span class="sxs-lookup"><span data-stu-id="93684-260">Changing hello priority level of each generated threat also changes their colors toomake it easy tooidentify high, medium and low priority threats.</span></span>

![Modifica della priorità](./media/azure-security-threat-modeling-tool/prioritychange.png)

### <a name="threat-properties-editable-fields"></a><span data-ttu-id="93684-262">Campi modificabili delle proprietà della minaccia</span><span class="sxs-lookup"><span data-stu-id="93684-262">Threat properties editable fields</span></span>

<span data-ttu-id="93684-263">Come illustrato nell'immagine di hello precedente, gli utenti possono modificare le informazioni di hello generate dallo strumento hello un anche aggiungere informazioni toocertain campi, ad esempio giustificazione.</span><span class="sxs-lookup"><span data-stu-id="93684-263">As seen in hello image above, users can change hello information generated by hello tool an also add information toocertain fields, such as justification.</span></span> <span data-ttu-id="93684-264">Questi campi vengono generati dal modello hello, pertanto se sono necessarie ulteriori informazioni per ogni minaccia, consigliabile toomake modifiche.</span><span class="sxs-lookup"><span data-stu-id="93684-264">These fields are generated by hello template, so if you need more information for each threat, you're encouraged toomake modifications.</span></span>

![Proprietà della minaccia](./media/azure-security-threat-modeling-tool/threatproperties.png)

## <a name="reports"></a><span data-ttu-id="93684-266">Report</span><span class="sxs-lookup"><span data-stu-id="93684-266">Reports</span></span>

<span data-ttu-id="93684-267">Dopo aver completato la modifica delle priorità e lo stato degli aggiornamenti di hello di ogni generato minaccia, è possibile salvare il file hello e/o stampare un report passando troppo "Report" e quindi "Creazione di Report completo."</span><span class="sxs-lookup"><span data-stu-id="93684-267">Once you're done changing priorities and updating hello status of each generated threat, you can save hello file and/or print out a report by going too"Report" and then "Create Full Report."</span></span> <span data-ttu-id="93684-268">Verrà chiesto report hello tooname e una volta eseguita, verrà visualizzato un codice simile immagine toohello riportata di seguito:</span><span class="sxs-lookup"><span data-stu-id="93684-268">You'll be asked tooname hello report, and once you do, you should see something similar toohello image below:</span></span>

![Report](./media/azure-security-threat-modeling-tool/report.png)

## <a name="next-steps"></a><span data-ttu-id="93684-270">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="93684-270">Next steps</span></span>

<span data-ttu-id="93684-271">toocontribute un modello per la community di hello, visitare tooour  **[GitHub](https://github.com/Microsoft/threat-modeling-templates)**  pagina.</span><span class="sxs-lookup"><span data-stu-id="93684-271">toocontribute a template for hello community, please go tooour **[GitHub](https://github.com/Microsoft/threat-modeling-templates)** page.</span></span> <span data-ttu-id="93684-272">**[Scaricare](https://aka.ms/tmtpreview)**  tooget strumento hello subito.</span><span class="sxs-lookup"><span data-stu-id="93684-272">**[Download](https://aka.ms/tmtpreview)** hello tool tooget started today.</span></span>

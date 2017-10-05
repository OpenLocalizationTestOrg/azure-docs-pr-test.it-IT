---
title: Microsoft Threat Modeling Tool - Azure | Microsoft Docs
description: "Informazioni su tutte le funzionalità disponibili in Threat Modeling Tool"
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
ms.openlocfilehash: 621ff305d7e782f85eeaae6c3fb02031673549c6
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/29/2017
---
# <a name="threat-modeling-tool-feature-overview"></a><span data-ttu-id="08dec-103">Panoramica della funzione Threat Modeling Tool</span><span class="sxs-lookup"><span data-stu-id="08dec-103">Threat Modeling Tool feature overview</span></span>

<span data-ttu-id="08dec-104">Siamo lieti della scelta dell'utente di impiegare Threat Modeling Tool per le esigenze di modellazione.</span><span class="sxs-lookup"><span data-stu-id="08dec-104">We are glad you chose to use the Threat Modeling Tool for your threat modeling needs!</span></span> <span data-ttu-id="08dec-105">Se non lo si è ancora fatto, visitare **[Guida introduttiva a Threat Modeling Tool](./azure-security-threat-modeling-tool-getting-started.md)** per apprendere le nozioni di base.</span><span class="sxs-lookup"><span data-stu-id="08dec-105">If you haven’t done so, visit **[Getting Started with the Threat Modeling Tool](./azure-security-threat-modeling-tool-getting-started.md)** to learn the basics.</span></span>

> <span data-ttu-id="08dec-106">Lo strumento viene aggiornato spesso, perciò si consiglia di controllare questa guida di frequente per vedere le ultime funzionalità e miglioramenti.</span><span class="sxs-lookup"><span data-stu-id="08dec-106">Our tool is updated often, so check this guide often to see our latest features and improvements.</span></span>

<span data-ttu-id="08dec-107">Facendo clic sul pulsante "Crea un nuovo modello" viene visualizzata una pagina iniziale vuota, simile all'immagine riportata di seguito:</span><span class="sxs-lookup"><span data-stu-id="08dec-107">Clicking on the "Create a New Model" button opens a blank start page, similar to the image below:</span></span>

![Pagina iniziale vuota](./media/azure-security-threat-modeling-tool/tmtstart.png)

<span data-ttu-id="08dec-109">Utilizzando il modello delle minacce creato dal nostro team nell'esempio **[Introduzione](./azure-security-threat-modeling-tool-getting-started.md)** esempio, controlliamo tutte le funzionalità disponibili nello strumento oggi.</span><span class="sxs-lookup"><span data-stu-id="08dec-109">Using the threat model created by our team in the **[Getting Started](./azure-security-threat-modeling-tool-getting-started.md)** example, let’s check out all the features available in the tool today.</span></span>

![Modello di minaccia di base](./media/azure-security-threat-modeling-tool/basictmt.png)

## <a name="navigation"></a><span data-ttu-id="08dec-111">Navigazione</span><span class="sxs-lookup"><span data-stu-id="08dec-111">Navigation</span></span>

<span data-ttu-id="08dec-112">Prima di illustrare le caratteristiche, è opportuno discutere dei componenti principali presenti nello strumento</span><span class="sxs-lookup"><span data-stu-id="08dec-112">Before diving into the built-in features, let’s go over the main components found in the tool</span></span>

### <a name="menu-items"></a><span data-ttu-id="08dec-113">Voci di menu</span><span class="sxs-lookup"><span data-stu-id="08dec-113">Menu items</span></span>

<span data-ttu-id="08dec-114">L'esperienza dovrebbe essere simile ad altri prodotti Microsoft.</span><span class="sxs-lookup"><span data-stu-id="08dec-114">The experience should be similar to other Microsoft products.</span></span> <span data-ttu-id="08dec-115">Iniziamo esaminando le voci di menu di primo livello:</span><span class="sxs-lookup"><span data-stu-id="08dec-115">Let’s begin by going through the top-level menu items:</span></span>

![Voci di menu](./media/azure-security-threat-modeling-tool/menuitems.png)

| <span data-ttu-id="08dec-117">Etichetta</span><span class="sxs-lookup"><span data-stu-id="08dec-117">Label</span></span>                               | <span data-ttu-id="08dec-118">Dettagli</span><span class="sxs-lookup"><span data-stu-id="08dec-118">Details</span></span>      |
| --------------------------------------- | ------------ |
| <span data-ttu-id="08dec-119">**File**</span><span class="sxs-lookup"><span data-stu-id="08dec-119">**File**</span></span> | <ul><li><span data-ttu-id="08dec-120">Aprire, salvare e chiudere i file</span><span class="sxs-lookup"><span data-stu-id="08dec-120">Open, Save and Close Files</span></span></li><li><span data-ttu-id="08dec-121">Accedere e disconnettersi dagli account di OneDrive</span><span class="sxs-lookup"><span data-stu-id="08dec-121">Sign In/Out of OneDrive accounts</span></span></li><li><span data-ttu-id="08dec-122">Condividere collegamenti (visualizzazione + modifica)</span><span class="sxs-lookup"><span data-stu-id="08dec-122">Share Links (View + Edit)</span></span></li><li><span data-ttu-id="08dec-123">Visualizzare le informazioni di file</span><span class="sxs-lookup"><span data-stu-id="08dec-123">View File Information</span></span></li><li><span data-ttu-id="08dec-124">Applicare un nuovo modello a modellazioni esistenti</span><span class="sxs-lookup"><span data-stu-id="08dec-124">Apply New Template to Existing Models</span></span></li></ul> |
| <span data-ttu-id="08dec-125">**Modifica**</span><span class="sxs-lookup"><span data-stu-id="08dec-125">**Edit**</span></span> | <span data-ttu-id="08dec-126">Annullare/ripristinare azioni, nonché copia, incolla ed elimina</span><span class="sxs-lookup"><span data-stu-id="08dec-126">Undo/redo actions, as well a copy, paste and delete</span></span> |
| <span data-ttu-id="08dec-127">**Visualizza**</span><span class="sxs-lookup"><span data-stu-id="08dec-127">**View**</span></span> | <ul><li><span data-ttu-id="08dec-128">Passare fra le visualizzazioni **Analisi** e **Progettazione**</span><span class="sxs-lookup"><span data-stu-id="08dec-128">Switch between **Analysis** and **Design** views</span></span></li><li><span data-ttu-id="08dec-129">Aprire finestre chiuse (ad es. stencil, proprietà degli elementi e messaggi)</span><span class="sxs-lookup"><span data-stu-id="08dec-129">Open closed windows (e.g.stencils, element properties and messages)</span></span></li><li><span data-ttu-id="08dec-130">Ripristinare le impostazioni predefinite del layout</span><span class="sxs-lookup"><span data-stu-id="08dec-130">Reset layout to default settings</span></span></li></ul> |
| <span data-ttu-id="08dec-131">**Diagramma**</span><span class="sxs-lookup"><span data-stu-id="08dec-131">**Diagram**</span></span> | <span data-ttu-id="08dec-132">Aggiungere/eliminare diagrammi e spostarsi tra le "schede" dei diagrammi</span><span class="sxs-lookup"><span data-stu-id="08dec-132">Add/Delete diagrams and navigate through “tabs” of diagrams</span></span> |
| <span data-ttu-id="08dec-133">**Report**</span><span class="sxs-lookup"><span data-stu-id="08dec-133">**Reports**</span></span> | <span data-ttu-id="08dec-134">Creare report HTML da condividere con altri utenti</span><span class="sxs-lookup"><span data-stu-id="08dec-134">Create HTML reports to share with others</span></span> |
| <span data-ttu-id="08dec-135">**Guida**</span><span class="sxs-lookup"><span data-stu-id="08dec-135">**Help**</span></span> | <span data-ttu-id="08dec-136">Informazioni di guida sull'uso dello strumento</span><span class="sxs-lookup"><span data-stu-id="08dec-136">Guides to help you use the tool</span></span> |

<span data-ttu-id="08dec-137">Le icone sono collegamenti ai menu di primo livello:</span><span class="sxs-lookup"><span data-stu-id="08dec-137">The icons are shortcuts for the top-level menus:</span></span>

| <span data-ttu-id="08dec-138">Icona</span><span class="sxs-lookup"><span data-stu-id="08dec-138">Icon</span></span>                               | <span data-ttu-id="08dec-139">Dettagli</span><span class="sxs-lookup"><span data-stu-id="08dec-139">Details</span></span>      |
| --------------------------------------- | ------------ |
| <span data-ttu-id="08dec-140">**Apri**</span><span class="sxs-lookup"><span data-stu-id="08dec-140">**Open**</span></span> | <span data-ttu-id="08dec-141">Apre un nuovo file</span><span class="sxs-lookup"><span data-stu-id="08dec-141">Opens a new file</span></span> |
| <span data-ttu-id="08dec-142">**Salva**</span><span class="sxs-lookup"><span data-stu-id="08dec-142">**Save**</span></span> | <span data-ttu-id="08dec-143">Salva il file corrente</span><span class="sxs-lookup"><span data-stu-id="08dec-143">Saves current file</span></span> |
| <span data-ttu-id="08dec-144">**Progettazione**</span><span class="sxs-lookup"><span data-stu-id="08dec-144">**Design**</span></span> | <span data-ttu-id="08dec-145">Passa alla visualizzazione progettazione dove è possibile creare modelli</span><span class="sxs-lookup"><span data-stu-id="08dec-145">Goes into design view, where you can create models</span></span> |
| <span data-ttu-id="08dec-146">**Analizzare**</span><span class="sxs-lookup"><span data-stu-id="08dec-146">**Analyze**</span></span> | <span data-ttu-id="08dec-147">Mostra le minacce generate e le relative proprietà</span><span class="sxs-lookup"><span data-stu-id="08dec-147">Shows generated threats and their properties</span></span> |
| <span data-ttu-id="08dec-148">**Aggiungi diagramma**</span><span class="sxs-lookup"><span data-stu-id="08dec-148">**Add Diagram**</span></span> | <span data-ttu-id="08dec-149">Aggiunge un nuovo diagramma (simile a nuove schede di Excel)</span><span class="sxs-lookup"><span data-stu-id="08dec-149">Adds new diagram (similar to new tabs in Excel)</span></span> |
| <span data-ttu-id="08dec-150">**Elimina diagramma**</span><span class="sxs-lookup"><span data-stu-id="08dec-150">**Delete Diagram**</span></span> | <span data-ttu-id="08dec-151">Elimina il diagramma corrente</span><span class="sxs-lookup"><span data-stu-id="08dec-151">Deletes current diagram</span></span> |
| <span data-ttu-id="08dec-152">**Copia/Taglia/Incolla**</span><span class="sxs-lookup"><span data-stu-id="08dec-152">**Copy/Cut/Paste**</span></span> | <span data-ttu-id="08dec-153">Copia/taglia /incolla elementi</span><span class="sxs-lookup"><span data-stu-id="08dec-153">Copies/cuts/pastes elements</span></span> |
| <span data-ttu-id="08dec-154">**Annulla/Ripeti**</span><span class="sxs-lookup"><span data-stu-id="08dec-154">**Undo/Redo**</span></span> | <span data-ttu-id="08dec-155">Annulla/ripete azioni</span><span class="sxs-lookup"><span data-stu-id="08dec-155">Undoes/redoes actions</span></span> |
| <span data-ttu-id="08dec-156">**Zoom avanti/Zoom indietro**</span><span class="sxs-lookup"><span data-stu-id="08dec-156">**Zoom In/Zoom Out**</span></span> | <span data-ttu-id="08dec-157">Esegue lo zoom avanti e indietro del diagramma per una migliore visualizzazione</span><span class="sxs-lookup"><span data-stu-id="08dec-157">Zooms in and out of the diagram for a better view</span></span> |
| <span data-ttu-id="08dec-158">**Commenti e suggerimenti**</span><span class="sxs-lookup"><span data-stu-id="08dec-158">**Feedback**</span></span> | <span data-ttu-id="08dec-159">Apre il Forum MSDN</span><span class="sxs-lookup"><span data-stu-id="08dec-159">Opens the MSDN Forum</span></span> |

### <a name="canvas"></a><span data-ttu-id="08dec-160">Canvas</span><span class="sxs-lookup"><span data-stu-id="08dec-160">Canvas</span></span>

<span data-ttu-id="08dec-161">Lo spazio in cui si trascinano gli elementi.</span><span class="sxs-lookup"><span data-stu-id="08dec-161">The space where you drag and drop elements into.</span></span> <span data-ttu-id="08dec-162">Il trascinamento è il modo più rapido ed efficiente per creare i modelli.</span><span class="sxs-lookup"><span data-stu-id="08dec-162">Drag and drop is the quickest and most efficient way to build models.</span></span> <span data-ttu-id="08dec-163">È anche possibile fare clic e selezionare dal menu, per aggiungere versioni generiche degli elementi che si stanno utilizzando, come illustrato di seguito.</span><span class="sxs-lookup"><span data-stu-id="08dec-163">You may also right click and select from the menu, which adds generic versions of the elements you’re using, as shown below.</span></span>

#### <a name="dropping-the-stencil-on-the-canvas"></a><span data-ttu-id="08dec-164">Rilascio dello stencil sul canvas</span><span class="sxs-lookup"><span data-stu-id="08dec-164">Dropping the stencil on the canvas</span></span>

![Rilascio sul canvas](./media/azure-security-threat-modeling-tool/canvasdrop1.png)

#### <a name="clicking-on-the-stencil"></a><span data-ttu-id="08dec-166">Clic sullo stencil</span><span class="sxs-lookup"><span data-stu-id="08dec-166">Clicking on the stencil</span></span>

![Proprietà dell'elemento](./media/azure-security-threat-modeling-tool/canvasdrop2.png)

### <a name="stencils"></a><span data-ttu-id="08dec-168">Stencil</span><span class="sxs-lookup"><span data-stu-id="08dec-168">Stencils</span></span>

<span data-ttu-id="08dec-169">Dove è possibile trovare tutti gli stencil disponibili per l'uso sul modello selezionato.</span><span class="sxs-lookup"><span data-stu-id="08dec-169">Where you can find all stencils available to use based on the template selected.</span></span> <span data-ttu-id="08dec-170">Se non è possibile trovare gli elementi giusti, provare a usare un altro modello o a modificarne uno in base alle proprie esigenze.</span><span class="sxs-lookup"><span data-stu-id="08dec-170">If you can’t find the right elements, try using another template, or modify one to fit your needs.</span></span> <span data-ttu-id="08dec-171">In genere si dovrebbe riuscire a trovare una combinazione di categorie come quelli indicati di seguito:</span><span class="sxs-lookup"><span data-stu-id="08dec-171">Generally, you should be able to find a combination of categories like the ones below:</span></span>

| <span data-ttu-id="08dec-172">Nome dello stencil</span><span class="sxs-lookup"><span data-stu-id="08dec-172">Stencil Name</span></span>                               | <span data-ttu-id="08dec-173">Dettagli</span><span class="sxs-lookup"><span data-stu-id="08dec-173">Details</span></span>      |
| --------------------------------------- | ------------ |
| <span data-ttu-id="08dec-174">**Processo**</span><span class="sxs-lookup"><span data-stu-id="08dec-174">**Process**</span></span> | <span data-ttu-id="08dec-175">Applicazioni, plugin del browser, minacce, macchine virtuali</span><span class="sxs-lookup"><span data-stu-id="08dec-175">Applications, Browser Plugins, Threads, Virtual Machines</span></span> |
| <span data-ttu-id="08dec-176">**Interazione esterna**</span><span class="sxs-lookup"><span data-stu-id="08dec-176">**External Interactor**</span></span> | <span data-ttu-id="08dec-177">Provider di autenticazione, browser, utenti, applicazioni Web</span><span class="sxs-lookup"><span data-stu-id="08dec-177">Authentication Providers, Browsers, Users, Web Applications</span></span> |
| <span data-ttu-id="08dec-178">**Archivio dati**</span><span class="sxs-lookup"><span data-stu-id="08dec-178">**Data Store**</span></span> | <span data-ttu-id="08dec-179">Cache, archiviazione, file di configurazione, database, registro</span><span class="sxs-lookup"><span data-stu-id="08dec-179">Cache, Storage, Configuration Files, Databases, Registry</span></span> |
| <span data-ttu-id="08dec-180">**Flusso di dati**</span><span class="sxs-lookup"><span data-stu-id="08dec-180">**Data Flow**</span></span> | <span data-ttu-id="08dec-181">File binario, ALPC, HTTP, HTTPS/TLS/SSL, IOCTL, IPSec, named pipe, RPC/DCOM, SMB, UDP</span><span class="sxs-lookup"><span data-stu-id="08dec-181">Binary, ALPC, HTTP, HTTPS/TLS/SSL, IOCTL, IPSec, Named Pipe, RPC/DCOM, SMB, UDP</span></span> |
| <span data-ttu-id="08dec-182">**Linea di trust/limite perimetrale**</span><span class="sxs-lookup"><span data-stu-id="08dec-182">**Trust Line/Border Boundary**</span></span> | <span data-ttu-id="08dec-183">Reti aziendali, Internet, computer, Sandbox, modalità utente/kernel</span><span class="sxs-lookup"><span data-stu-id="08dec-183">Corporate Networks, Internet, Machine, Sandbox, User/Kernel Mode</span></span> |

### <a name="notesmessages"></a><span data-ttu-id="08dec-184">Note/messaggi</span><span class="sxs-lookup"><span data-stu-id="08dec-184">Notes/Messages</span></span>

| <span data-ttu-id="08dec-185">Componente</span><span class="sxs-lookup"><span data-stu-id="08dec-185">Component</span></span>                               | <span data-ttu-id="08dec-186">Dettagli</span><span class="sxs-lookup"><span data-stu-id="08dec-186">Details</span></span>      |
| --------------------------------------- | ------------ |
| <span data-ttu-id="08dec-187">**Messaggi**</span><span class="sxs-lookup"><span data-stu-id="08dec-187">**Messages**</span></span> | <span data-ttu-id="08dec-188">Logica dello strumento interno che avvisa gli utenti ogni volta che si verifica un errore, ad esempio l'assenza di flusso di dati tra gli elementi</span><span class="sxs-lookup"><span data-stu-id="08dec-188">Internal tool logic that alerts users whenever there is an error, such as no data flows between elements</span></span> |
| <span data-ttu-id="08dec-189">**Note**</span><span class="sxs-lookup"><span data-stu-id="08dec-189">**Notes**</span></span> | <span data-ttu-id="08dec-190">Note manuali aggiunte al file dai team di tecnici nel corso del processo di progettazione e revisione</span><span class="sxs-lookup"><span data-stu-id="08dec-190">Manual notes added to the file by engineering teams throughout the design and review process</span></span> |

### <a name="element-properties"></a><span data-ttu-id="08dec-191">Proprietà dell'elemento</span><span class="sxs-lookup"><span data-stu-id="08dec-191">Element properties</span></span>

<span data-ttu-id="08dec-192">Queste variano in base agli elementi selezionati.</span><span class="sxs-lookup"><span data-stu-id="08dec-192">These vary by the elements selected.</span></span> <span data-ttu-id="08dec-193">Oltre ai limiti di trust, tutti gli altri elementi contengono 3 selezioni generali:</span><span class="sxs-lookup"><span data-stu-id="08dec-193">Apart from Trust Boundaries, all other elements contain 3 general selections:</span></span>

| <span data-ttu-id="08dec-194">Proprietà dell'elemento</span><span class="sxs-lookup"><span data-stu-id="08dec-194">Element Property</span></span>                               | <span data-ttu-id="08dec-195">Dettagli</span><span class="sxs-lookup"><span data-stu-id="08dec-195">Details</span></span>      |
| --------------------------------------- | ------------ |
| <span data-ttu-id="08dec-196">**Nome**</span><span class="sxs-lookup"><span data-stu-id="08dec-196">**Name**</span></span> | <span data-ttu-id="08dec-197">Utile per assegnare nomi a processi, archivi, interazioni e flussi in modo da facilitarne il riconoscimento</span><span class="sxs-lookup"><span data-stu-id="08dec-197">Useful for naming your processes, stores, interactors and flows to be easily recognized</span></span> |
| <span data-ttu-id="08dec-198">**Fuori ambito**</span><span class="sxs-lookup"><span data-stu-id="08dec-198">**Out of Scope**</span></span> | <span data-ttu-id="08dec-199">Se selezionato, l'elemento viene sottratto dalla matrice di generazione delle minacce (scelta non consigliata)</span><span class="sxs-lookup"><span data-stu-id="08dec-199">If selected, the element is taken out of the threat generation matrix (not recommended)</span></span> |
| <span data-ttu-id="08dec-200">**Ragioni per il fuori ambito**</span><span class="sxs-lookup"><span data-stu-id="08dec-200">**Reason for Out of Scope**</span></span> | <span data-ttu-id="08dec-201">Campo di giustificazione per informare gli utenti perché è stato selezionato il fuori ambito</span><span class="sxs-lookup"><span data-stu-id="08dec-201">Justification field to let users know why out of scope was selected</span></span> |

<span data-ttu-id="08dec-202">Vengono modificate le proprietà sotto ogni categoria di elemento.</span><span class="sxs-lookup"><span data-stu-id="08dec-202">Properties are changed under each element category.</span></span> <span data-ttu-id="08dec-203">Fare clic su ciascun elemento per controllare le opzioni disponibili o aprire il modello per altre informazioni.</span><span class="sxs-lookup"><span data-stu-id="08dec-203">Click on each element to inspect the available options, or open the template to learn more.</span></span> <span data-ttu-id="08dec-204">Esaminiamo le funzionalità.</span><span class="sxs-lookup"><span data-stu-id="08dec-204">Let’s get into the features.</span></span>

## <a name="welcome-screen"></a><span data-ttu-id="08dec-205">Schermata iniziale</span><span class="sxs-lookup"><span data-stu-id="08dec-205">Welcome screen</span></span>

<span data-ttu-id="08dec-206">La schermata di benvenuto è la prima cosa che viene visualizzato quando si apre l'app.</span><span class="sxs-lookup"><span data-stu-id="08dec-206">The welcome screen is the first thing you see when you open the app.</span></span>

### <a name="open-a-model"></a><span data-ttu-id="08dec-207">Aprire un modello</span><span class="sxs-lookup"><span data-stu-id="08dec-207">Open A model</span></span>

<span data-ttu-id="08dec-208">Passando con il mouse sul pulsante "Apri un modello" vengono visualizzate 2 opzioni nascoste: "Apri da questo computer" e "Apri da OneDrive".</span><span class="sxs-lookup"><span data-stu-id="08dec-208">Hovering over “Open a Model” button shows you 2 hidden options: “Open From this Computer” and “Open from OneDrive.”</span></span> <span data-ttu-id="08dec-209">La prima apre la schermata Apri file, mentre la seconda conduce l'utenre attraverso la procedura di accesso a OneDrive, consentendo di scegliere cartelle e file dopo l'autenticazione.</span><span class="sxs-lookup"><span data-stu-id="08dec-209">The first opens the File Open screen, while the second takes you through the sign in process for OneDrive, allowing you to pick folders and files after a successful authentication.</span></span>

![Aprire un modello](./media/azure-security-threat-modeling-tool/openmodel.png)

![Aprire dal computer o da OneDrive](./media/azure-security-threat-modeling-tool/openmodel2.png)

### <a name="feedback-suggestions-and-issues"></a><span data-ttu-id="08dec-212">Commenti, suggerimenti e problemi</span><span class="sxs-lookup"><span data-stu-id="08dec-212">Feedback, suggestions and issues</span></span>

<span data-ttu-id="08dec-213">Selezionando questa opzione si passa al forum MSDN per gli strumenti SDL.</span><span class="sxs-lookup"><span data-stu-id="08dec-213">Selecting this option will take you to the MSDN Forums for SDL Tools.</span></span> <span data-ttu-id="08dec-214">È un ottimo modo per vedere opinioni di altri utenti sullo strumento nonché nuove idee e soluzioni alternative.</span><span class="sxs-lookup"><span data-stu-id="08dec-214">It’s a great way to check out what other people are saying about the tool, including workarounds and new ideas.</span></span>

![Commenti e suggerimenti](./media/azure-security-threat-modeling-tool/feedback.png)

## <a name="design-view"></a><span data-ttu-id="08dec-216">Visualizzazione progettazione</span><span class="sxs-lookup"><span data-stu-id="08dec-216">Design view</span></span>

<span data-ttu-id="08dec-217">Ogni volta che si apre o si crea un nuovo modello, viene mostrata la visualizzazione progettazione.</span><span class="sxs-lookup"><span data-stu-id="08dec-217">Whenever you open or create a new model, you’ll be taken to the design view.</span></span>

### <a name="adding-elements"></a><span data-ttu-id="08dec-218">Aggiunta di elementi</span><span class="sxs-lookup"><span data-stu-id="08dec-218">Adding elements</span></span>

<span data-ttu-id="08dec-219">Esistono 2 modi per aggiungere elementi sulla griglia:</span><span class="sxs-lookup"><span data-stu-id="08dec-219">There are 2 ways to add elements on the grid:</span></span>

- <span data-ttu-id="08dec-220">**Trascinare e rilasciare**: trascinare l'elemento desiderato nella griglia, quindi usare le proprietà dell'elemento per fornire informazioni aggiuntive.</span><span class="sxs-lookup"><span data-stu-id="08dec-220">**Drag and Drop** – drag the desired element to the grid, then use the element properties to provide additional information.</span></span>
- <span data-ttu-id="08dec-221">**Clic con il pulsante destro del mouse**: fare clic con il pulsante destro del mouse in punto qualsiasi della griglia e scegliere dal menu a discesa.</span><span class="sxs-lookup"><span data-stu-id="08dec-221">**Right Click** – right click anywhere on the grid and select from the dropdown menu.</span></span> <span data-ttu-id="08dec-222">Una rappresentazione generica dell'elemento verrà visualizzata sullo schermo.</span><span class="sxs-lookup"><span data-stu-id="08dec-222">A generic representation of that element will appear on the screen.</span></span>

### <a name="connecting-elements"></a><span data-ttu-id="08dec-223">Collegamento di elementi</span><span class="sxs-lookup"><span data-stu-id="08dec-223">Connecting elements</span></span>

<span data-ttu-id="08dec-224">Sono disponibili 2 modi per connettere gli elementi nello strumento:</span><span class="sxs-lookup"><span data-stu-id="08dec-224">There are 2 ways to connect elements in the tool:</span></span>

- <span data-ttu-id="08dec-225">**Trascinare e rilasciare**: trascinare il flusso di dati desiderato sulla griglia e connettere entrambe le estremità agli elementi appropriati.</span><span class="sxs-lookup"><span data-stu-id="08dec-225">**Drag and Drop** – drag the desired dataflow to the grid, and connect both ends to the appropriate elements.</span></span>
- <span data-ttu-id="08dec-226">**Eseguire clic + MAIUSC**: fare clic sul primo elemento (invio di dati), premere e tenere premuto il tasto MAIUSC, quindi selezionare il secondo elemento (ricezione di dati).</span><span class="sxs-lookup"><span data-stu-id="08dec-226">**Click + Shift** – click on the first element (sending data), press and hold the Shift key, then select the second element (receiving data).</span></span> <span data-ttu-id="08dec-227">Fare clic con il pulsante destro del mouse e selezionare "Connetti".</span><span class="sxs-lookup"><span data-stu-id="08dec-227">Right click, and select “Connect.”</span></span> <span data-ttu-id="08dec-228">Se si utilizza un flusso di dati bidirezionale, l'ordine non è importante.</span><span class="sxs-lookup"><span data-stu-id="08dec-228">If you’re using a bi-directional dataflow, the order is not as important.</span></span>

### <a name="properties"></a><span data-ttu-id="08dec-229">Proprietà</span><span class="sxs-lookup"><span data-stu-id="08dec-229">Properties</span></span>

<span data-ttu-id="08dec-230">Mostra tutte le proprietà che possono essere modificate negli stencil inseriti nel diagramma.</span><span class="sxs-lookup"><span data-stu-id="08dec-230">Shows all the properties that can be modified on the stencils placed in the diagram.</span></span> <span data-ttu-id="08dec-231">Per visualizzare le proprietà, fare clic sullo stencil e le informazioni verranno popolate di conseguenza.</span><span class="sxs-lookup"><span data-stu-id="08dec-231">To see the properties, just click on the stencil and the information will be populated accordingly.</span></span> <span data-ttu-id="08dec-232">L'esempio seguente mostra la situazione prima e dopo il trascinamento di uno stencil "Database" nel diagramma:</span><span class="sxs-lookup"><span data-stu-id="08dec-232">The example below shows before and after a "Database" stencil is dragged onto the diagram:</span></span>

#### <a name="before"></a><span data-ttu-id="08dec-233">Prima</span><span class="sxs-lookup"><span data-stu-id="08dec-233">Before</span></span>

![Prima](./media/azure-security-threat-modeling-tool/properties1.png)

#### <a name="after"></a><span data-ttu-id="08dec-235">Dopo</span><span class="sxs-lookup"><span data-stu-id="08dec-235">After</span></span>

![Dopo](./media/azure-security-threat-modeling-tool/properties2.png)

### <a name="messages"></a><span data-ttu-id="08dec-237">Messaggi</span><span class="sxs-lookup"><span data-stu-id="08dec-237">Messages</span></span>

<span data-ttu-id="08dec-238">Se si crea un modello di minacce e si dimentica di connettere i flussi di dati agli elementi, la finestra messaggio notifica l'azione da eseguire. È possibile scegliere di ignorarla o seguire le istruzioni per risolvere il problema.</span><span class="sxs-lookup"><span data-stu-id="08dec-238">If you create a threat model and forget to connect data flows to elements, the message window notifies you to act. You can choose to ignore it or follow the instructions to fix the issue.</span></span> 

![Messaggi](./media/azure-security-threat-modeling-tool/messages.png)

### <a name="notes"></a><span data-ttu-id="08dec-240">Note</span><span class="sxs-lookup"><span data-stu-id="08dec-240">Notes</span></span>

<span data-ttu-id="08dec-241">Alternando le schede dai messaggi alle note è possibile aggiungere note al diagramma per catturare tutti i pensieri</span><span class="sxs-lookup"><span data-stu-id="08dec-241">Switching tabs from Messages to Notes allows you to add notes to your diagram to capture all your thoughts</span></span>

## <a name="analysis-view"></a><span data-ttu-id="08dec-242">Visualizzazione analisi</span><span class="sxs-lookup"><span data-stu-id="08dec-242">Analysis view</span></span>

<span data-ttu-id="08dec-243">Dopo aver compilato il diagramma, passare alla visualizzazione analisi passando alle selezioni di menu in alto e scegliendo la lente di ingrandimento accanto alla tavolozza.</span><span class="sxs-lookup"><span data-stu-id="08dec-243">Once you're done building your diagram, switch over to analysis view by going to the top menu selections and choosing the magnifying glass next to the paint palette.</span></span>

![Visualizzazione analisi](./media/azure-security-threat-modeling-tool/analysisview.png)

### <a name="generated-threat-selection"></a><span data-ttu-id="08dec-245">Selezione di minacce generata</span><span class="sxs-lookup"><span data-stu-id="08dec-245">Generated threat selection</span></span>

<span data-ttu-id="08dec-246">Quando si fa clic su una minaccia, è possibile sfruttare tre funzioni uniche:</span><span class="sxs-lookup"><span data-stu-id="08dec-246">When you click on a threat, you can leverage three unique functions:</span></span>

| <span data-ttu-id="08dec-247">Funzionalità</span><span class="sxs-lookup"><span data-stu-id="08dec-247">Feature</span></span>                               | <span data-ttu-id="08dec-248">Info</span><span class="sxs-lookup"><span data-stu-id="08dec-248">Info</span></span>      |
| --------------------------------------- | ------------ |
| <span data-ttu-id="08dec-249">**Indicatore letto**</span><span class="sxs-lookup"><span data-stu-id="08dec-249">**Read Indicator**</span></span> | <p><span data-ttu-id="08dec-250">La minaccia è ora contrassegnato come letta, il che può facilitare il monitoraggio degli elementi già analizzati</span><span class="sxs-lookup"><span data-stu-id="08dec-250">Threat is now marked as read, which can easily help you keep track of the items you already went through</span></span></p><p>![Indicatore letto/non letto](./media/azure-security-threat-modeling-tool/readmode.png)</p> |
| <span data-ttu-id="08dec-252">**Centro di interazione**</span><span class="sxs-lookup"><span data-stu-id="08dec-252">**Interaction Focus**</span></span> | <p><span data-ttu-id="08dec-253">Viene evidenziata l'interazione nel diagramma appartenente a tale minaccia</span><span class="sxs-lookup"><span data-stu-id="08dec-253">Interaction in the diagram belonging to that threat is highlighted</span></span></p><p>![Centro di interazione](./media/azure-security-threat-modeling-tool/interactionfocus.png)</p> |
| <span data-ttu-id="08dec-255">**Proprietà della minaccia**</span><span class="sxs-lookup"><span data-stu-id="08dec-255">**Threat Properties**</span></span> | <p><span data-ttu-id="08dec-256">Altre informazioni sulla minaccia sono aggiunte nella finestra delle proprietà della minaccia</span><span class="sxs-lookup"><span data-stu-id="08dec-256">Additional information about the threat is populated in the threat properties window</span></span></p><p>![Proprietà della minaccia](./media/azure-security-threat-modeling-tool/threatproperties.png)</p> |

### <a name="priority-change"></a><span data-ttu-id="08dec-258">Modifica della priorità</span><span class="sxs-lookup"><span data-stu-id="08dec-258">Priority change</span></span>

<span data-ttu-id="08dec-259">La modifica del livello di priorità di ciascuna minaccia generata modifica anche i colori per facilitare l'identificazione delle minacce a priorità alta, media e bassa.</span><span class="sxs-lookup"><span data-stu-id="08dec-259">Changing the priority level of each generated threat also changes their colors to make it easy to identify high, medium and low priority threats.</span></span>

![Modifica della priorità](./media/azure-security-threat-modeling-tool/prioritychange.png)

### <a name="threat-properties-editable-fields"></a><span data-ttu-id="08dec-261">Campi modificabili delle proprietà della minaccia</span><span class="sxs-lookup"><span data-stu-id="08dec-261">Threat properties editable fields</span></span>

<span data-ttu-id="08dec-262">Come illustrato nell'immagine precedente, gli utenti possono modificare le informazioni generate dallo strumento a anche aggiungere informazioni a determinati campi, ad esempio una giustificazione.</span><span class="sxs-lookup"><span data-stu-id="08dec-262">As seen in the image above, users can change the information generated by the tool an also add information to certain fields, such as justification.</span></span> <span data-ttu-id="08dec-263">Questi campi vengono generati dal modello, pertanto se sono necessarie altre informazioni per ogni minaccia, si consiglia di apportare modifiche.</span><span class="sxs-lookup"><span data-stu-id="08dec-263">These fields are generated by the template, so if you need more information for each threat, you're encouraged to make modifications.</span></span>

![Proprietà della minaccia](./media/azure-security-threat-modeling-tool/threatproperties.png)

## <a name="reports"></a><span data-ttu-id="08dec-265">Report</span><span class="sxs-lookup"><span data-stu-id="08dec-265">Reports</span></span>

<span data-ttu-id="08dec-266">Dopo aver completato la modifica delle priorità e aggiornato lo stato di ciascuna minaccia generata, è possibile salvare il file e/o stampare un report passando a "Report" e poi a "Crea report completo".</span><span class="sxs-lookup"><span data-stu-id="08dec-266">Once you're done changing priorities and updating the status of each generated threat, you can save the file and/or print out a report by going to "Report" and then "Create Full Report."</span></span> <span data-ttu-id="08dec-267">Verrà chiesto di assegnare un nome al report e, al termine dell'operazione, si dovrebbe vedere qualcosa di simile all'immagine riportata di seguito:</span><span class="sxs-lookup"><span data-stu-id="08dec-267">You'll be asked to name the report, and once you do, you should see something similar to the image below:</span></span>

![Report](./media/azure-security-threat-modeling-tool/report.png)

## <a name="next-steps"></a><span data-ttu-id="08dec-269">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="08dec-269">Next steps</span></span>

<span data-ttu-id="08dec-270">Per rilasciare un modello alla community, visitare la nostra pagina **[GitHub](https://github.com/Microsoft/threat-modeling-templates)**.</span><span class="sxs-lookup"><span data-stu-id="08dec-270">To contribute a template for the community, please go to our **[GitHub](https://github.com/Microsoft/threat-modeling-templates)** page.</span></span> <span data-ttu-id="08dec-271">**[Scaricare](https://aka.ms/tmtpreview)** lo strumento per iniziare oggi stesso.</span><span class="sxs-lookup"><span data-stu-id="08dec-271">**[Download](https://aka.ms/tmtpreview)** the tool to get started today.</span></span>

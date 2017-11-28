---
title: Azure DevTest Labs aaaAbout | Documenti Microsoft
description: Informazioni su come DevTest Labs possibile renderlo toocreate semplice, gestire e monitorare macchine virtuali di Azure
services: devtest-lab,virtual-machines
documentationcenter: na
author: tomarcher
manager: douge
editor: 
ms.assetid: 1b9eed3b-c69a-4c49-a36e-f388efea6f39
ms.service: devtest-lab
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/11/2017
ms.author: tarcher
ms.openlocfilehash: 5e5aa683f80144a2f6872c7fa328016120ea6253
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="about-azure-devtest-labs"></a><span data-ttu-id="0d0eb-103">Informazioni su Azure DevTest Labs</span><span class="sxs-lookup"><span data-stu-id="0d0eb-103">About Azure DevTest Labs</span></span>
## <a name="overview"></a><span data-ttu-id="0d0eb-104">Panoramica</span><span class="sxs-lookup"><span data-stu-id="0d0eb-104">Overview</span></span>
<span data-ttu-id="0d0eb-105">Gli sviluppatori e tester sono alla ricerca ritardi hello toosolve nella creazione e gestione dei propri ambienti passando toohello cloud.</span><span class="sxs-lookup"><span data-stu-id="0d0eb-105">Developers and testers are looking toosolve hello delays in creating and managing their environments by going toohello cloud.</span></span>  <span data-ttu-id="0d0eb-106">Azure consente di risolvere il problema di hello di ritardi di ambiente e consente di self-service all'interno di una nuova struttura efficiente di costo.</span><span class="sxs-lookup"><span data-stu-id="0d0eb-106">Azure solves hello problem of environment delays and allows self-service within a new cost efficient structure.</span></span>  <span data-ttu-id="0d0eb-107">Tuttavia, gli sviluppatori e tester ancora necessario la configurazione di ambienti self-serviti toospend molto tempo.</span><span class="sxs-lookup"><span data-stu-id="0d0eb-107">However, developers and testers still need toospend considerable time configuring their self-served environments.</span></span> <span data-ttu-id="0d0eb-108">Inoltre, responsabili delle decisioni sono sicuri come tooleverage hello cloud toomaximize i risparmi sui costi senza aggiungere troppo elaborare overhead.</span><span class="sxs-lookup"><span data-stu-id="0d0eb-108">Also, decision makers are uncertain about how tooleverage hello cloud toomaximize their cost savings without adding too much process overhead.</span></span>

<span data-ttu-id="0d0eb-109">Lab di sviluppo e test di Azure è un servizio che consente agli sviluppatori e ai tester di creare rapidamente ambienti in Azure riducendo al minimo gli sprechi e i costi di controllo.</span><span class="sxs-lookup"><span data-stu-id="0d0eb-109">Azure DevTest Labs is a service that helps developers and testers quickly create environments in Azure while minimizing waste and controlling cost.</span></span> <span data-ttu-id="0d0eb-110">È possibile verificare più recente dell'applicazione hello da rapidamente il provisioning di ambienti Windows e Linux utilizzando gli elementi e modelli riutilizzabili.</span><span class="sxs-lookup"><span data-stu-id="0d0eb-110">You can test hello latest version of your application by quickly provisioning Windows and Linux environments using reusable templates and artifacts.</span></span> <span data-ttu-id="0d0eb-111">Consente di integrare facilmente la pipeline di distribuzione con gli ambienti di DevTest Labs tooprovision su richiesta.</span><span class="sxs-lookup"><span data-stu-id="0d0eb-111">Easily integrate your deployment pipeline with DevTest Labs tooprovision on-demand environments.</span></span> <span data-ttu-id="0d0eb-112">Aumentare i propri test di carico tramite il provisioning di più agenti di test e creare ambienti di pre-provisioning per training e demo.</span><span class="sxs-lookup"><span data-stu-id="0d0eb-112">Scale up your load testing by provisioning multiple test agents, and create pre-provisioned environments for training and demos.</span></span>

> [!VIDEO https://channel9.msdn.com/Blogs/Azure/What-is-Azure-DevTest-Labs/player]
> 
> 

<span data-ttu-id="0d0eb-113">DevTest Labs fornisce i seguenti vantaggi nella creazione, configurazione e la gestione di ambienti di sviluppo e test nel cloud hello hello</span><span class="sxs-lookup"><span data-stu-id="0d0eb-113">DevTest Labs provides hello following benefits in creating, configuring, and managing developer and test environments in hello cloud</span></span>

## <a name="worry-free-self-service"></a><span data-ttu-id="0d0eb-114">Self-service di semplice uso</span><span class="sxs-lookup"><span data-stu-id="0d0eb-114">Worry-free self-service</span></span>
<span data-ttu-id="0d0eb-115">DevTest Labs rende più semplice toocontrol costi consentendo tooset criteri nel lab - ad esempio il numero di macchine virtuali (VM) per utente e numero di macchine virtuali per lab.</span><span class="sxs-lookup"><span data-stu-id="0d0eb-115">DevTest Labs makes it easier toocontrol costs by allowing you tooset policies on your lab - such as number of virtual machines (VM) per user and number of VMs per lab.</span></span> <span data-ttu-id="0d0eb-116">DevTest Labs, inoltre, consente di toocreate criteri tooautomatically arrestare e avviare le macchine virtuali.</span><span class="sxs-lookup"><span data-stu-id="0d0eb-116">DevTest Labs also enables you toocreate policies tooautomatically shut down and start VMs.</span></span>

## <a name="quickly-get-tooready-to-test"></a><span data-ttu-id="0d0eb-117">Ottenere rapidamente tooready a test</span><span class="sxs-lookup"><span data-stu-id="0d0eb-117">Quickly get tooready-to-test</span></span>
<span data-ttu-id="0d0eb-118">DevTest Labs consente gli ambienti di pre-provisioning toocreate tutto ciò che il team deve toostart lo sviluppo e test delle applicazioni.</span><span class="sxs-lookup"><span data-stu-id="0d0eb-118">DevTest Labs enables you toocreate pre-provisioned environments with everything your team needs toostart developing and testing applications.</span></span> <span data-ttu-id="0d0eb-119">È sufficiente attestazione ambienti hello in cui è installato l'ultima compilazione valida hello dell'applicazione e ottenere subito a lavorare.</span><span class="sxs-lookup"><span data-stu-id="0d0eb-119">Simply claim hello environments where hello last good build of your application is installed and get working right away.</span></span> <span data-ttu-id="0d0eb-120">Oppure utilizzare i contenitori per creare gli ambienti in modo ancora più veloce ed efficiente.</span><span class="sxs-lookup"><span data-stu-id="0d0eb-120">Or, use containers for even faster and leaner environment creation.</span></span>

## <a name="create-once-use-everywhere"></a><span data-ttu-id="0d0eb-121">Creazione di un'unica soluzione per scenari di diverso tipo</span><span class="sxs-lookup"><span data-stu-id="0d0eb-121">Create once, use everywhere</span></span>
<span data-ttu-id="0d0eb-122">Acquisire e condividere modelli di ambiente e gli elementi all'interno del team o organizzazione - in controllo del codice sorgente - toocreate developer e ambienti di test con facilità.</span><span class="sxs-lookup"><span data-stu-id="0d0eb-122">Capture and share environment templates and artifacts within your team or organization - all in source control - toocreate developer and test environments easily.</span></span>

## <a name="integrates-with-your-existing-toolchain"></a><span data-ttu-id="0d0eb-123">Integrazione con la toolchain esistente</span><span class="sxs-lookup"><span data-stu-id="0d0eb-123">Integrates with your existing toolchain</span></span>
<span data-ttu-id="0d0eb-124">Sfruttare i plug-in predefinito o l'API tooprovision Dev/negli ambienti di Test direttamente dallo strumento preferito integrazione continua (CI), integrato (IDE) di ambiente di sviluppo o automatici della pipeline di rilascio.</span><span class="sxs-lookup"><span data-stu-id="0d0eb-124">Leverage pre-made plug-ins or our API tooprovision Dev/Test environments directly from your preferred continuous integration (CI) tool, integrated development environment (IDE), or automated release pipeline.</span></span> <span data-ttu-id="0d0eb-125">E’ anche possibile utilizzare il nostro strumento da riga di comando completo.</span><span class="sxs-lookup"><span data-stu-id="0d0eb-125">You can also use our comprehensive command-line tool.</span></span>


[!INCLUDE [devtest-lab-try-it-out](../../includes/devtest-lab-try-it-out.md)]

## <a name="next-steps"></a><span data-ttu-id="0d0eb-126">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="0d0eb-126">Next steps</span></span>
[<span data-ttu-id="0d0eb-127">Concetti di Lab di sviluppo e test</span><span class="sxs-lookup"><span data-stu-id="0d0eb-127">DevTest Labs concepts</span></span>](devtest-lab-concepts.md)


---
title: Informazioni su Azure DevTest Labs | Microsoft Docs
description: "Informazioni su come Lab di sviluppo/test può rendere più semplice la creazione, la gestione e il monitoraggio delle macchine virtuali di Azure"
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
ms.openlocfilehash: 62e2d214d6d685c7f27c8c45cae161eb25ed1cbd
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="about-azure-devtest-labs"></a><span data-ttu-id="ed7d8-103">Informazioni su Azure DevTest Labs</span><span class="sxs-lookup"><span data-stu-id="ed7d8-103">About Azure DevTest Labs</span></span>
## <a name="overview"></a><span data-ttu-id="ed7d8-104">Panoramica</span><span class="sxs-lookup"><span data-stu-id="ed7d8-104">Overview</span></span>
<span data-ttu-id="ed7d8-105">Gli sviluppatori e i tester stanno cercando di risolvere i ritardi nella creazione e nella gestione dei propri ambienti accedendo al cloud.</span><span class="sxs-lookup"><span data-stu-id="ed7d8-105">Developers and testers are looking to solve the delays in creating and managing their environments by going to the cloud.</span></span>  <span data-ttu-id="ed7d8-106">Azure consente di risolvere il problema dei ritardi di ambiente e consente il self-service all'interno di una nuova struttura conveniente.</span><span class="sxs-lookup"><span data-stu-id="ed7d8-106">Azure solves the problem of environment delays and allows self-service within a new cost efficient structure.</span></span>  <span data-ttu-id="ed7d8-107">Tuttavia, gli sviluppatori e i tester necessitano ancora di molto tempo per la configurazione dei propri ambienti autonomi.</span><span class="sxs-lookup"><span data-stu-id="ed7d8-107">However, developers and testers still need to spend considerable time configuring their self-served environments.</span></span> <span data-ttu-id="ed7d8-108">Inoltre, i decision maker sono incerti su come sfruttare il cloud per ottimizzare i risparmi senza aggiungere una quantità eccessiva di overhead del processo.</span><span class="sxs-lookup"><span data-stu-id="ed7d8-108">Also, decision makers are uncertain about how to leverage the cloud to maximize their cost savings without adding too much process overhead.</span></span>

<span data-ttu-id="ed7d8-109">Lab di sviluppo e test di Azure è un servizio che consente agli sviluppatori e ai tester di creare rapidamente ambienti in Azure riducendo al minimo gli sprechi e i costi di controllo.</span><span class="sxs-lookup"><span data-stu-id="ed7d8-109">Azure DevTest Labs is a service that helps developers and testers quickly create environments in Azure while minimizing waste and controlling cost.</span></span> <span data-ttu-id="ed7d8-110">È possibile provare la versione più recente dell'applicazione eseguendo rapidamente il provisioning di ambienti Windows e Linux tramite modelli ed elementi riutilizzabili.</span><span class="sxs-lookup"><span data-stu-id="ed7d8-110">You can test the latest version of your application by quickly provisioning Windows and Linux environments using reusable templates and artifacts.</span></span> <span data-ttu-id="ed7d8-111">Consente di integrare facilmente la pipeline di distribuzione in lab di sviluppo e test per effettuare il provisioning di ambienti su richiesta.</span><span class="sxs-lookup"><span data-stu-id="ed7d8-111">Easily integrate your deployment pipeline with DevTest Labs to provision on-demand environments.</span></span> <span data-ttu-id="ed7d8-112">Aumentare i propri test di carico tramite il provisioning di più agenti di test e creare ambienti di pre-provisioning per training e demo.</span><span class="sxs-lookup"><span data-stu-id="ed7d8-112">Scale up your load testing by provisioning multiple test agents, and create pre-provisioned environments for training and demos.</span></span>

> [!VIDEO https://channel9.msdn.com/Blogs/Azure/What-is-Azure-DevTest-Labs/player]
> 
> 

<span data-ttu-id="ed7d8-113">Lab di sviluppo e test offre i seguenti vantaggi nella creazione, configurazione e gestione di ambienti di sviluppo e test nel cloud</span><span class="sxs-lookup"><span data-stu-id="ed7d8-113">DevTest Labs provides the following benefits in creating, configuring, and managing developer and test environments in the cloud</span></span>

## <a name="worry-free-self-service"></a><span data-ttu-id="ed7d8-114">Self-service di semplice uso</span><span class="sxs-lookup"><span data-stu-id="ed7d8-114">Worry-free self-service</span></span>
<span data-ttu-id="ed7d8-115">Lab di sviluppo e test rende più semplice controllare i costi consentendo di impostare criteri nel lab, come il numero di macchine virtuali (VM) per ogni utente e il numero di macchine virtuali per ogni lab.</span><span class="sxs-lookup"><span data-stu-id="ed7d8-115">DevTest Labs makes it easier to control costs by allowing you to set policies on your lab - such as number of virtual machines (VM) per user and number of VMs per lab.</span></span> <span data-ttu-id="ed7d8-116">Lab di sviluppo e test consente inoltre di creare criteri per arrestare e avviare le macchine virtuali automaticamente.</span><span class="sxs-lookup"><span data-stu-id="ed7d8-116">DevTest Labs also enables you to create policies to automatically shut down and start VMs.</span></span>

## <a name="quickly-get-to-ready-to-test"></a><span data-ttu-id="ed7d8-117">Ambienti di test subito pronti</span><span class="sxs-lookup"><span data-stu-id="ed7d8-117">Quickly get to ready-to-test</span></span>
<span data-ttu-id="ed7d8-118">Lab di sviluppo e test consente di creare ambienti di pre-provisioning con tutto ciò che è necessario per il team affinché possa iniziare lo sviluppo e il test delle applicazioni.</span><span class="sxs-lookup"><span data-stu-id="ed7d8-118">DevTest Labs enables you to create pre-provisioned environments with everything your team needs to start developing and testing applications.</span></span> <span data-ttu-id="ed7d8-119">È sufficiente richiedere gli ambienti in cui è stata installata l'ultima compilazione valida dell'applicazione e iniziare subito a lavorare.</span><span class="sxs-lookup"><span data-stu-id="ed7d8-119">Simply claim the environments where the last good build of your application is installed and get working right away.</span></span> <span data-ttu-id="ed7d8-120">Oppure utilizzare i contenitori per creare gli ambienti in modo ancora più veloce ed efficiente.</span><span class="sxs-lookup"><span data-stu-id="ed7d8-120">Or, use containers for even faster and leaner environment creation.</span></span>

## <a name="create-once-use-everywhere"></a><span data-ttu-id="ed7d8-121">Creazione di un'unica soluzione per scenari di diverso tipo</span><span class="sxs-lookup"><span data-stu-id="ed7d8-121">Create once, use everywhere</span></span>
<span data-ttu-id="ed7d8-122">E’ possibile acquisire e condividere elementi e modelli di ambienti all'interno del team o dell'organizzazione, il tutto nel controllo del codice sorgente, per creare in modo facile ambienti di sviluppo e test.</span><span class="sxs-lookup"><span data-stu-id="ed7d8-122">Capture and share environment templates and artifacts within your team or organization - all in source control - to create developer and test environments easily.</span></span>

## <a name="integrates-with-your-existing-toolchain"></a><span data-ttu-id="ed7d8-123">Integrazione con la toolchain esistente</span><span class="sxs-lookup"><span data-stu-id="ed7d8-123">Integrates with your existing toolchain</span></span>
<span data-ttu-id="ed7d8-124">E’ possibile sfruttare plug-in già pronti oppure l’API per effettuare il provisioning di ambienti di sviluppo/test direttamente dallo strumento di integrazione continua (CI), dall'ambiente di sviluppo integrato (IDE, Integrated Development Environment) o dalla pipeline di rilascio automatizzata.</span><span class="sxs-lookup"><span data-stu-id="ed7d8-124">Leverage pre-made plug-ins or our API to provision Dev/Test environments directly from your preferred continuous integration (CI) tool, integrated development environment (IDE), or automated release pipeline.</span></span> <span data-ttu-id="ed7d8-125">E’ anche possibile utilizzare il nostro strumento da riga di comando completo.</span><span class="sxs-lookup"><span data-stu-id="ed7d8-125">You can also use our comprehensive command-line tool.</span></span>


[!INCLUDE [devtest-lab-try-it-out](../../includes/devtest-lab-try-it-out.md)]

## <a name="next-steps"></a><span data-ttu-id="ed7d8-126">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="ed7d8-126">Next steps</span></span>
[<span data-ttu-id="ed7d8-127">Concetti di Lab di sviluppo e test</span><span class="sxs-lookup"><span data-stu-id="ed7d8-127">DevTest Labs concepts</span></span>](devtest-lab-concepts.md)


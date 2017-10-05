---
title: Proteggere le soluzioni IoT (Internet delle cose) in Azure | Documentazione Microsoft
description: " I servizi di Azure IoT (Internet delle cose) offrono una vasta gamma di funzionalità. Questo articolo illustra come proteggere le soluzioni IoT in Azure. "
services: security
documentationcenter: na
author: TomShinder
manager: MBaldwin
editor: TomSh
ms.assetid: 1473c8dd-8669-48fb-86db-b3c50e2eaf59
ms.service: security
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 01/23/2017
ms.author: terrylan
ms.openlocfilehash: 3793f5453b74b6c06d9e58b426d89099298e1288
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="internet-of-things-security-overview"></a><span data-ttu-id="ea144-104">Informazioni generali sulla sicurezza di Internet delle cose</span><span class="sxs-lookup"><span data-stu-id="ea144-104">Internet of Things security overview</span></span>
<span data-ttu-id="ea144-105">I servizi di Azure IoT (Internet delle cose) offrono una vasta gamma di funzionalità.</span><span class="sxs-lookup"><span data-stu-id="ea144-105">Azure internet of things (IoT) services offer a broad range of capabilities.</span></span> <span data-ttu-id="ea144-106">Questi servizi di livello aziendale consentono di:</span><span class="sxs-lookup"><span data-stu-id="ea144-106">These enterprise grade services enable you to:</span></span>

* <span data-ttu-id="ea144-107">Raccogliere dati dai dispositivi</span><span class="sxs-lookup"><span data-stu-id="ea144-107">Collect data from devices</span></span>
* <span data-ttu-id="ea144-108">Analizzare i flussi dei dati in movimento</span><span class="sxs-lookup"><span data-stu-id="ea144-108">Analyze data streams in-motion</span></span>
* <span data-ttu-id="ea144-109">Archiviare ed eseguire query su set di dati di grandi dimensioni</span><span class="sxs-lookup"><span data-stu-id="ea144-109">Store and query large data sets</span></span>
* <span data-ttu-id="ea144-110">Visualizzare i dati in tempo reale e cronologici</span><span class="sxs-lookup"><span data-stu-id="ea144-110">Visualize both real-time and historical data</span></span>
* <span data-ttu-id="ea144-111">Eseguire l'integrazione con i sistemi back-office</span><span class="sxs-lookup"><span data-stu-id="ea144-111">Integrate with back-office systems</span></span>

<span data-ttu-id="ea144-112">Per offrire queste funzionalità, Azure IoT Suite include più servizi di Azure con estensioni personalizzate come soluzioni preconfigurate.</span><span class="sxs-lookup"><span data-stu-id="ea144-112">To deliver these capabilities, Azure IoT Suite packages together multiple Azure services with custom extensions as preconfigured solutions.</span></span> <span data-ttu-id="ea144-113">Queste soluzioni preconfigurate sono implementazioni di base dei modelli di soluzione IoT comuni che contribuiscono a ridurre i tempi di distribuzione delle soluzioni IoT.</span><span class="sxs-lookup"><span data-stu-id="ea144-113">These preconfigured solutions are base implementations of common IoT solution patterns that help to reduce the time you take to deliver your IoT solutions.</span></span> <span data-ttu-id="ea144-114">I Software Development Kit IoT consentono di personalizzare ed estendere queste soluzioni per soddisfare le proprie esigenze.</span><span class="sxs-lookup"><span data-stu-id="ea144-114">Using the IoT software development kits, you can customize and extend these solutions to meet your own requirements.</span></span> <span data-ttu-id="ea144-115">È anche possibile usare queste soluzioni come esempi o modelli durante lo sviluppo di nuove soluzioni IoT.</span><span class="sxs-lookup"><span data-stu-id="ea144-115">You can also use these solutions as examples or templates when you are developing new IoT solutions.</span></span>

<span data-ttu-id="ea144-116">Azure IoT Suite è una potente soluzione per le esigenze di IoT.</span><span class="sxs-lookup"><span data-stu-id="ea144-116">The Azure IoT suite is a powerful solution for your IoT needs.</span></span> <span data-ttu-id="ea144-117">È tuttavia fondamentale che le soluzioni IoT siano progettate sin dall'inizio pensando alla sicurezza.</span><span class="sxs-lookup"><span data-stu-id="ea144-117">However, it’s of upmost importance that your IoT solutions are designed with security in mind from the start.</span></span> <span data-ttu-id="ea144-118">A causa del numero elevato di dispositivi IoT, qualsiasi evento imprevisto riguardante la sicurezza può diventare rapidamente un evento esteso con conseguenze significative.</span><span class="sxs-lookup"><span data-stu-id="ea144-118">Because of the sheer number of IoT devices, any security incident can quickly become a widespread event with significant consequences.</span></span>

<span data-ttu-id="ea144-119">Le informazioni seguenti sono utili per comprendere come proteggere le soluzioni IoT.</span><span class="sxs-lookup"><span data-stu-id="ea144-119">To help you understand how to secure your IoT solutions, we have the following information.</span></span>

## <a name="security-architecture"></a><span data-ttu-id="ea144-120">Architettura di sicurezza</span><span class="sxs-lookup"><span data-stu-id="ea144-120">Security architecture</span></span>
<span data-ttu-id="ea144-121">Quando si progetta un sistema, è importante comprendere le potenziali minacce e aggiungere le difese appropriate di conseguenza, perché il sistema è definito da una progettazione e un'architettura specifiche.</span><span class="sxs-lookup"><span data-stu-id="ea144-121">When designing a system, it is important to understand the potential threats to that system, and add appropriate defenses accordingly, as the system is designed and architected.</span></span> <span data-ttu-id="ea144-122">È importante progettare il prodotto tenendo conto della sicurezza, perché comprendere in che modo un utente malintenzionato potrebbe compromettere un sistema aiuta ad implementare le misure appropriate fin dall'inizio.</span><span class="sxs-lookup"><span data-stu-id="ea144-122">It is important to design the product from the start with security in mind because understanding how an attacker might be able to compromise a system helps make sure appropriate mitigations are in place from the beginning.</span></span>

<span data-ttu-id="ea144-123">Informazioni sull'architettura di sicurezza IoT sono disponibili in [Architettura di sicurezza di Internet delle cose](../iot-suite/iot-security-architecture.md).</span><span class="sxs-lookup"><span data-stu-id="ea144-123">You can learn about IoT security architecture by reading [Internet of Things Security Architecture](../iot-suite/iot-security-architecture.md).</span></span>

<span data-ttu-id="ea144-124">Questo articolo tratta gli argomenti seguenti:</span><span class="sxs-lookup"><span data-stu-id="ea144-124">This article discusses the following topics:</span></span>

* [<span data-ttu-id="ea144-125">La sicurezza inizia con un modello di rischio</span><span class="sxs-lookup"><span data-stu-id="ea144-125">Security Starts with a Threat Model</span></span>](../iot-suite/iot-security-architecture.md#security-starts-with-a-threat-model)
* [<span data-ttu-id="ea144-126">Sicurezza in IoT</span><span class="sxs-lookup"><span data-stu-id="ea144-126">Security in IoT</span></span>](../iot-suite/iot-security-architecture.md#security-in-iot)
* [<span data-ttu-id="ea144-127">Modellazione delle minacce nell'architettura di riferimento di Azure IoT</span><span class="sxs-lookup"><span data-stu-id="ea144-127">Threat Modeling the Azure IoT Reference Architecture</span></span>](../iot-suite/iot-security-architecture.md#threat-modeling-the-azure-iot-reference-architecture)

## <a name="security-from-the-ground-up"></a><span data-ttu-id="ea144-128">Sicurezza sin dall'inizio</span><span class="sxs-lookup"><span data-stu-id="ea144-128">Security from the ground up</span></span>
<span data-ttu-id="ea144-129">Internet delle cose pone numerose sfide in termini di sicurezza, privacy e conformità per le aziende di tutto il mondo.</span><span class="sxs-lookup"><span data-stu-id="ea144-129">The IoT poses unique security, privacy, and compliance challenges to businesses worldwide.</span></span> <span data-ttu-id="ea144-130">A differenza delle tecnologie informatiche tradizionali in cui questi problemi riguardano il software e la relativa implementazione, l'IoT riguarda le sfide poste dalla convergenza tra il mondo fisico e quello informatico.</span><span class="sxs-lookup"><span data-stu-id="ea144-130">Unlike traditional cyber technology where these issues revolve around software and how it is implemented, IoT concerns what happens when the cyber and the physical worlds converge.</span></span> <span data-ttu-id="ea144-131">Per proteggere le soluzioni IoT, è necessario garantire il provisioning sicuro dei dispositivi, la connettività protetta tra questi dispositivi e il cloud e la protezione dei dati nel cloud durante l'elaborazione e l'archiviazione.</span><span class="sxs-lookup"><span data-stu-id="ea144-131">Protecting IoT solutions requires ensuring secure provisioning of devices, secure connectivity between these devices and the cloud, and secure data protection in the cloud during processing and storage.</span></span> <span data-ttu-id="ea144-132">A sfavore di queste funzionalità, tuttavia, giocano fattori quali dispositivi vincolati alle risorse, la distribuzione geografica delle implementazioni e l'inclusione di numerosi dispositivi in un'unica soluzione.</span><span class="sxs-lookup"><span data-stu-id="ea144-132">Working against such functionality, however, are resource-constrained devices, geographic distribution of deployments, and many devices within a solution.</span></span>

<span data-ttu-id="ea144-133">Informazioni su come gestire la sicurezza in queste aree sono disponibili in [Sicurezza di Internet delle cose sin dall'inizio](../iot-suite/securing-iot-ground-up.md).</span><span class="sxs-lookup"><span data-stu-id="ea144-133">You can learn how to handle security in these areas by reading [Internet of Things security from the ground up](../iot-suite/securing-iot-ground-up.md).</span></span>

<span data-ttu-id="ea144-134">L'articolo tratta gli argomenti seguenti:</span><span class="sxs-lookup"><span data-stu-id="ea144-134">The article discusses the following topics:</span></span>

* [<span data-ttu-id="ea144-135">Proteggere l'infrastruttura fin dall'inizio</span><span class="sxs-lookup"><span data-stu-id="ea144-135">Secure infrastructure from the ground up</span></span>](../iot-suite/securing-iot-ground-up.md#secure-infrastructure-from-the-ground-up)
* [<span data-ttu-id="ea144-136">Microsoft Azure: protezione dell'infrastruttura IoT aziendale</span><span class="sxs-lookup"><span data-stu-id="ea144-136">Microsoft Azure – secure IoT infrastructure for your business</span></span>](../iot-suite/securing-iot-ground-up.md#microsoft-azure---secure-iot-infrastructure-for-your-business)

## <a name="best-practices"></a><span data-ttu-id="ea144-137">Procedure consigliate</span><span class="sxs-lookup"><span data-stu-id="ea144-137">Best Practices</span></span>
<span data-ttu-id="ea144-138">Proteggere un'infrastruttura IoT richiede una strategia di sicurezza rigorosa e approfondita.</span><span class="sxs-lookup"><span data-stu-id="ea144-138">Securing an IoT infrastructure requires a rigorous security-in-depth strategy.</span></span> <span data-ttu-id="ea144-139">Dalla protezione dei dati nel cloud alla protezione dell'integrità dei dati in transito sulla rete Internet pubblica e al provisioning sicuro dei dispositivi, ogni strato aumenta il livello di sicurezza dell'intera infrastruttura.</span><span class="sxs-lookup"><span data-stu-id="ea144-139">From securing data in the cloud, protecting data integrity while in transit over the public internet, to securely provisioning devices, each layer builds greater security assurance in the overall infrastructure.</span></span>

<span data-ttu-id="ea144-140">Informazioni sulle procedure consigliate per la sicurezza di Internet delle cose sono disponibili in [Procedure consigliate per la sicurezza di Internet delle cose](../iot-suite/iot-security-best-practices.md).</span><span class="sxs-lookup"><span data-stu-id="ea144-140">You can learn about Internet of Things security best practices by reading [Internet of Things security best practices](../iot-suite/iot-security-best-practices.md).</span></span>

<span data-ttu-id="ea144-141">L'articolo tratta gli argomenti seguenti:</span><span class="sxs-lookup"><span data-stu-id="ea144-141">The article discusses the following topics:</span></span>

* [<span data-ttu-id="ea144-142">Produttore/integratore di hardware IoT</span><span class="sxs-lookup"><span data-stu-id="ea144-142">IoT hardware manufacturer/integrator</span></span>](../iot-suite/iot-security-best-practices.md#iot-hardware-manufacturerintegrator)
* [<span data-ttu-id="ea144-143">Sviluppatore di soluzioni IoT</span><span class="sxs-lookup"><span data-stu-id="ea144-143">IoT solution developer</span></span>](../iot-suite/iot-security-best-practices.md#iot-solution-developer)
* [<span data-ttu-id="ea144-144">Distributore di soluzioni IoT</span><span class="sxs-lookup"><span data-stu-id="ea144-144">IoT solution deployer</span></span>](../iot-suite/iot-security-best-practices.md#iot-solution-deployer)
* [<span data-ttu-id="ea144-145">Operatore di soluzioni IoT</span><span class="sxs-lookup"><span data-stu-id="ea144-145">IoT solution operator</span></span>](../iot-suite/iot-security-best-practices.md#iot-solution-operator)

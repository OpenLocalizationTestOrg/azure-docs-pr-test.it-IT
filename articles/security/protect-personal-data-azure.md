---
title: aaaProtect dati personali in Microsoft Azure | Documenti Microsoft
description: Primo articolo in una serie di articoli toohelp utilizzare dati personali tooprotect Azure
services: security
documentationcenter: na
author: Barclayn
manager: MBaldwin
editor: TomSh
ms.assetid: 
ms.service: security
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/22/2017
ms.author: barclayn
ms.custom: 
ms.openlocfilehash: cbffd3872552cbd0f12539535898c41ecf7789e8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="protect-personal-data-in-microsoft-azure"></a><span data-ttu-id="cd8ec-103">Proteggere i dati personali in Microsoft Azure</span><span class="sxs-lookup"><span data-stu-id="cd8ec-103">Protect personal data in Microsoft Azure</span></span>

<span data-ttu-id="cd8ec-104">Questo articolo descrive una serie di articoli che consentono di utilizzare Azure sicurezza tecnologie e servizi tooprotect dati personali.</span><span class="sxs-lookup"><span data-stu-id="cd8ec-104">This article introduces a series of articles that help you use Azure security technologies and services tooprotect personal data.</span></span> <span data-ttu-id="cd8ec-105">Si tratta di un requisito fondamentale per molte aziende e iniziative di governance e conformità.</span><span class="sxs-lookup"><span data-stu-id="cd8ec-105">This is a key requirement for many corporate and industry compliance and governance initiatives.</span></span> <span data-ttu-id="cd8ec-106">scenario di Hello, gli obiettivi di istruzione e la società problema questa sezione sono inclusi.</span><span class="sxs-lookup"><span data-stu-id="cd8ec-106">hello scenario, problem statement and company goals are included here.</span></span>

## <a name="scenario-and-problem-statement"></a><span data-ttu-id="cd8ec-107">Scenario e presentazione del problema</span><span class="sxs-lookup"><span data-stu-id="cd8ec-107">Scenario and problem statement</span></span>

<span data-ttu-id="cd8ec-108">Una società crociera di grandi dimensioni, la sede centrale negli Stati Uniti hello espansione relativo itinerari toooffer operazioni Mediterraneo hello, Adriatico e mare Baltico, nonché hello isole britannico.</span><span class="sxs-lookup"><span data-stu-id="cd8ec-108">A large cruise company, headquartered in hello United States, is expanding its operations toooffer itineraries in hello Mediterranean, Adriatic, and Baltic seas, as well as hello British Isles.</span></span> <span data-ttu-id="cd8ec-109">toosupport tali attività, che è stato acquisito più righe crociera inferiori basate in Italia, Germania, Danimarca e hello Regno Unito</span><span class="sxs-lookup"><span data-stu-id="cd8ec-109">toosupport those efforts, it has acquired several smaller cruise lines based in Italy, Germany, Denmark and hello U.K.</span></span>

<span data-ttu-id="cd8ec-110">la società Hello utilizza i dati aziendali di Microsoft Azure toostore nel cloud hello.</span><span class="sxs-lookup"><span data-stu-id="cd8ec-110">hello company uses Microsoft Azure toostore corporate data in hello cloud.</span></span> <span data-ttu-id="cd8ec-111">Può trattarsi di dipendente e/o informazioni sul cliente, ad esempio:</span><span class="sxs-lookup"><span data-stu-id="cd8ec-111">This may include employee and/or customer information such as:</span></span>

- <span data-ttu-id="cd8ec-112">Indirizzi</span><span class="sxs-lookup"><span data-stu-id="cd8ec-112">addresses</span></span>
- <span data-ttu-id="cd8ec-113">Numeri di telefono</span><span class="sxs-lookup"><span data-stu-id="cd8ec-113">phone numbers</span></span>
- <span data-ttu-id="cd8ec-114">Codici fiscali</span><span class="sxs-lookup"><span data-stu-id="cd8ec-114">tax identification numbers</span></span>
- <span data-ttu-id="cd8ec-115">informazioni mediche</span><span class="sxs-lookup"><span data-stu-id="cd8ec-115">medical information</span></span>
- <span data-ttu-id="cd8ec-116">Dati delle carte di credito</span><span class="sxs-lookup"><span data-stu-id="cd8ec-116">credit card information</span></span>

<span data-ttu-id="cd8ec-117">società Hello necessario proteggere la privacy hello di dati dipendenti e clienti durante la creazione di servizi accessibili toothose dati che ne hanno necessità.</span><span class="sxs-lookup"><span data-stu-id="cd8ec-117">hello company must protect hello privacy of employee and customer data while making data accessible toothose departments that need it.</span></span> <span data-ttu-id="cd8ec-118">ad esempio quelli che si occupano di retribuzioni e prenotazioni.</span><span class="sxs-lookup"><span data-stu-id="cd8ec-118">(such as payroll and reservations departments)</span></span>

## <a name="company-goals"></a><span data-ttu-id="cd8ec-119">Obiettivi dell'azienda</span><span class="sxs-lookup"><span data-stu-id="cd8ec-119">Company goals</span></span> 

- <span data-ttu-id="cd8ec-120">Le origini dati che contengono dati personali vengono crittografate quando che risiedono nell'archiviazione cloud.</span><span class="sxs-lookup"><span data-stu-id="cd8ec-120">Data sources that contain personal data are encrypted when residing in cloud storage.</span></span>

- <span data-ttu-id="cd8ec-121">Dati personali che viene trasferiti da un'unica posizione tooanother vengono crittografati durante il transito.</span><span class="sxs-lookup"><span data-stu-id="cd8ec-121">Personal data that is transferred from one location tooanother is encrypted while in-transit.</span></span> <span data-ttu-id="cd8ec-122">Ciò è vero se hello dati vengono inviati attraverso la rete virtuale hello o hello Internet tra data center aziendale hello e hello cloud di Azure.</span><span class="sxs-lookup"><span data-stu-id="cd8ec-122">This is true if hello data is traveling across hello virtual network or across hello Internet between hello corporate datacenter and hello Azure cloud.</span></span>

- <span data-ttu-id="cd8ec-123">La riservatezza e l'integrità dei dati personali vengono protette da accessi non autorizzati grazie a tecnologie avanzate di gestione delle identità e controllo di accesso.</span><span class="sxs-lookup"><span data-stu-id="cd8ec-123">Confidentiality and integrity of personal data is protected from unauthorized access by strong identity management and access control technologies.</span></span>

- <span data-ttu-id="cd8ec-124">I dati personali vengono protetti dall'esposizione dovuta alla violazione dei dati grazie al monitoraggio di minacce e vulnerabilità.</span><span class="sxs-lookup"><span data-stu-id="cd8ec-124">Personal data is protected from exposure via data breach via monitoring for vulnerabilities and threats.</span></span>

- <span data-ttu-id="cd8ec-125">Hello lo stato di sicurezza dei servizi Azure che memorizzano o trasmettono dati personali viene valutato tooidentify opportunità toobetter proteggere i dati personali.</span><span class="sxs-lookup"><span data-stu-id="cd8ec-125">hello security state of Azure services that store or transmit personal data is assessed tooidentify opportunities toobetter protect personal data.</span></span>

## <a name="data-protection-guidance"></a><span data-ttu-id="cd8ec-126">Materiale sussidiario sulla protezione dei dati</span><span class="sxs-lookup"><span data-stu-id="cd8ec-126">Data protection guidance</span></span>

<span data-ttu-id="cd8ec-127">Hello seguenti articoli contenga come tooguidance tecniche che consentirà di raggiungere gli obiettivi di protezione dati personali hello elencati in precedenza:</span><span class="sxs-lookup"><span data-stu-id="cd8ec-127">hello following articles contain technical how-tooguidance that will help you attain hello personal data protection goals listed above:</span></span>

- [<span data-ttu-id="cd8ec-128">Tecnologie di crittografia di Azure</span><span class="sxs-lookup"><span data-stu-id="cd8ec-128">Azure encryption technologies</span></span>](protect-personal-data-at-rest.md)

- [<span data-ttu-id="cd8ec-129">Tecnologie di crittografia di Azure</span><span class="sxs-lookup"><span data-stu-id="cd8ec-129">Azure encryption technologies</span></span>](protect-personal-data-in-transit-encryption.md)

- [<span data-ttu-id="cd8ec-130">Tecnologie di gestione delle identità e degli accessi di Azure</span><span class="sxs-lookup"><span data-stu-id="cd8ec-130">Azure identity and access technologies</span></span>](protect-personal-data-identity-access-controls.md)

- [<span data-ttu-id="cd8ec-131">Tecnologie di sicurezza di rete di Azure</span><span class="sxs-lookup"><span data-stu-id="cd8ec-131">Azure network security technologies</span></span>](protect-personal-data-network-security.md)

- [<span data-ttu-id="cd8ec-132">Centro sicurezza di Azure</span><span class="sxs-lookup"><span data-stu-id="cd8ec-132">Azure Security Center</span></span>](protect-personal-data-azure-security-center.md)



## <a name="next-steps"></a><span data-ttu-id="cd8ec-133">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="cd8ec-133">Next steps</span></span>

- [<span data-ttu-id="cd8ec-134">Sito di informazioni sulla sicurezza di Azure</span><span class="sxs-lookup"><span data-stu-id="cd8ec-134">Azure Security Information Site</span></span>](https://aka.ms/AzureSecInfo)

- [<span data-ttu-id="cd8ec-135">Centro protezione Microsoft</span><span class="sxs-lookup"><span data-stu-id="cd8ec-135">Microsoft Trust Center</span></span>](https://www.microsoft.com/TrustCenter/default.aspx)

- [<span data-ttu-id="cd8ec-136">Centro sicurezza di Azure</span><span class="sxs-lookup"><span data-stu-id="cd8ec-136">Azure Security Center</span></span>](https://azure.microsoft.com/services/security-center/)

- [<span data-ttu-id="cd8ec-137">Blog del team di sicurezza di Azure</span><span class="sxs-lookup"><span data-stu-id="cd8ec-137">Azure Security Team Blog</span></span>](https://www.azuresecurityorg)

- [<span data-ttu-id="cd8ec-138">Blog di Azure.com - Sicurezza</span><span class="sxs-lookup"><span data-stu-id="cd8ec-138">Azure.com Blog - Security</span></span>](https://azure.microsoft.com/blog/topics/security/)

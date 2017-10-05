---
title: Proteggere i dati personali in Microsoft Azure | Microsoft Docs
description: Primo di una serie di articoli che illustrano come usare Azure per proteggere i dati personali
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
ms.openlocfilehash: dfb046374397c8a19672ce6b67741903fff6e178
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/29/2017
---
# <a name="protect-personal-data-in-microsoft-azure"></a><span data-ttu-id="2f362-103">Proteggere i dati personali in Microsoft Azure</span><span class="sxs-lookup"><span data-stu-id="2f362-103">Protect personal data in Microsoft Azure</span></span>

<span data-ttu-id="2f362-104">Questo articolo è il primo di una serie di articoli che illustrano come usare le tecnologie e i servizi di sicurezza di Azure per proteggere i dati personali.</span><span class="sxs-lookup"><span data-stu-id="2f362-104">This article introduces a series of articles that help you use Azure security technologies and services to protect personal data.</span></span> <span data-ttu-id="2f362-105">Si tratta di un requisito fondamentale per molte aziende e iniziative di governance e conformità.</span><span class="sxs-lookup"><span data-stu-id="2f362-105">This is a key requirement for many corporate and industry compliance and governance initiatives.</span></span> <span data-ttu-id="2f362-106">L'articolo descrive anche lo scenario, la presentazione del problema e gli obiettivi aziendali.</span><span class="sxs-lookup"><span data-stu-id="2f362-106">The scenario, problem statement and company goals are included here.</span></span>

## <a name="scenario-and-problem-statement"></a><span data-ttu-id="2f362-107">Scenario e presentazione del problema</span><span class="sxs-lookup"><span data-stu-id="2f362-107">Scenario and problem statement</span></span>

<span data-ttu-id="2f362-108">Un'importante compagnia di viaggi in crociera, con sede negli Stati Uniti, sta espandendo le proprie operazioni per offrire itinerari nel Mar Mediterraneo e nel Mar Baltico, nonché nelle isole britanniche.</span><span class="sxs-lookup"><span data-stu-id="2f362-108">A large cruise company, headquartered in the United States, is expanding its operations to offer itineraries in the Mediterranean, Adriatic, and Baltic seas, as well as the British Isles.</span></span> <span data-ttu-id="2f362-109">Per supportare tale iniziativa, ha acquistato diverse linee minori con sede in Italia, Germania, Danimarca e Regno Unito.</span><span class="sxs-lookup"><span data-stu-id="2f362-109">To support those efforts, it has acquired several smaller cruise lines based in Italy, Germany, Denmark and the U.K.</span></span>

<span data-ttu-id="2f362-110">La società usa Microsoft Azure per archiviare i dati aziendali nel cloud.</span><span class="sxs-lookup"><span data-stu-id="2f362-110">The company uses Microsoft Azure to store corporate data in the cloud.</span></span> <span data-ttu-id="2f362-111">Può trattarsi di dipendente e/o informazioni sul cliente, ad esempio:</span><span class="sxs-lookup"><span data-stu-id="2f362-111">This may include employee and/or customer information such as:</span></span>

- <span data-ttu-id="2f362-112">Indirizzi</span><span class="sxs-lookup"><span data-stu-id="2f362-112">addresses</span></span>
- <span data-ttu-id="2f362-113">Numeri di telefono</span><span class="sxs-lookup"><span data-stu-id="2f362-113">phone numbers</span></span>
- <span data-ttu-id="2f362-114">Codici fiscali</span><span class="sxs-lookup"><span data-stu-id="2f362-114">tax identification numbers</span></span>
- <span data-ttu-id="2f362-115">informazioni mediche</span><span class="sxs-lookup"><span data-stu-id="2f362-115">medical information</span></span>
- <span data-ttu-id="2f362-116">Dati delle carte di credito</span><span class="sxs-lookup"><span data-stu-id="2f362-116">credit card information</span></span>

<span data-ttu-id="2f362-117">La società è necessario proteggere la privacy dei dati dipendenti e clienti durante la creazione di dati accessibili per i reparti che ne hanno necessità.</span><span class="sxs-lookup"><span data-stu-id="2f362-117">The company must protect the privacy of employee and customer data while making data accessible to those departments that need it.</span></span> <span data-ttu-id="2f362-118">ad esempio quelli che si occupano di retribuzioni e prenotazioni.</span><span class="sxs-lookup"><span data-stu-id="2f362-118">(such as payroll and reservations departments)</span></span>

## <a name="company-goals"></a><span data-ttu-id="2f362-119">Obiettivi dell'azienda</span><span class="sxs-lookup"><span data-stu-id="2f362-119">Company goals</span></span> 

- <span data-ttu-id="2f362-120">Le origini dati che contengono dati personali vengono crittografate quando che risiedono nell'archiviazione cloud.</span><span class="sxs-lookup"><span data-stu-id="2f362-120">Data sources that contain personal data are encrypted when residing in cloud storage.</span></span>

- <span data-ttu-id="2f362-121">I dati personali che vengono trasferiti da una posizione all'altra vengono crittografati durante il transito.</span><span class="sxs-lookup"><span data-stu-id="2f362-121">Personal data that is transferred from one location to another is encrypted while in-transit.</span></span> <span data-ttu-id="2f362-122">Ciò accade se i dati vengono trasferiti attraverso la rete virtuale o in Internet tra i data center aziendali e il cloud di Azure.</span><span class="sxs-lookup"><span data-stu-id="2f362-122">This is true if the data is traveling across the virtual network or across the Internet between the corporate datacenter and the Azure cloud.</span></span>

- <span data-ttu-id="2f362-123">La riservatezza e l'integrità dei dati personali vengono protette da accessi non autorizzati grazie a tecnologie avanzate di gestione delle identità e controllo di accesso.</span><span class="sxs-lookup"><span data-stu-id="2f362-123">Confidentiality and integrity of personal data is protected from unauthorized access by strong identity management and access control technologies.</span></span>

- <span data-ttu-id="2f362-124">I dati personali vengono protetti dall'esposizione dovuta alla violazione dei dati grazie al monitoraggio di minacce e vulnerabilità.</span><span class="sxs-lookup"><span data-stu-id="2f362-124">Personal data is protected from exposure via data breach via monitoring for vulnerabilities and threats.</span></span>

- <span data-ttu-id="2f362-125">Lo stato di sicurezza dei servizi di Azure che archiviano o trasmettono dati personali viene valutato per identificare le opportunità di ottimizzazione della protezione di tali dati.</span><span class="sxs-lookup"><span data-stu-id="2f362-125">The security state of Azure services that store or transmit personal data is assessed to identify opportunities to better protect personal data.</span></span>

## <a name="data-protection-guidance"></a><span data-ttu-id="2f362-126">Materiale sussidiario sulla protezione dei dati</span><span class="sxs-lookup"><span data-stu-id="2f362-126">Data protection guidance</span></span>

<span data-ttu-id="2f362-127">Gli articoli seguenti contengono indicazioni sulle procedure tecniche che consentono di raggiungere gli obiettivi di protezione dei dati personali elencati in precedenza:</span><span class="sxs-lookup"><span data-stu-id="2f362-127">The following articles contain technical how-to guidance that will help you attain the personal data protection goals listed above:</span></span>

- [<span data-ttu-id="2f362-128">Tecnologie di crittografia di Azure</span><span class="sxs-lookup"><span data-stu-id="2f362-128">Azure encryption technologies</span></span>](protect-personal-data-at-rest.md)

- [<span data-ttu-id="2f362-129">Tecnologie di crittografia di Azure</span><span class="sxs-lookup"><span data-stu-id="2f362-129">Azure encryption technologies</span></span>](protect-personal-data-in-transit-encryption.md)

- [<span data-ttu-id="2f362-130">Tecnologie di gestione delle identità e degli accessi di Azure</span><span class="sxs-lookup"><span data-stu-id="2f362-130">Azure identity and access technologies</span></span>](protect-personal-data-identity-access-controls.md)

- [<span data-ttu-id="2f362-131">Tecnologie di sicurezza di rete di Azure</span><span class="sxs-lookup"><span data-stu-id="2f362-131">Azure network security technologies</span></span>](protect-personal-data-network-security.md)

- [<span data-ttu-id="2f362-132">Centro sicurezza di Azure</span><span class="sxs-lookup"><span data-stu-id="2f362-132">Azure Security Center</span></span>](protect-personal-data-azure-security-center.md)



## <a name="next-steps"></a><span data-ttu-id="2f362-133">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="2f362-133">Next steps</span></span>

- [<span data-ttu-id="2f362-134">Sito di informazioni sulla sicurezza di Azure</span><span class="sxs-lookup"><span data-stu-id="2f362-134">Azure Security Information Site</span></span>](https://aka.ms/AzureSecInfo)

- [<span data-ttu-id="2f362-135">Centro protezione Microsoft</span><span class="sxs-lookup"><span data-stu-id="2f362-135">Microsoft Trust Center</span></span>](https://www.microsoft.com/TrustCenter/default.aspx)

- [<span data-ttu-id="2f362-136">Centro sicurezza di Azure</span><span class="sxs-lookup"><span data-stu-id="2f362-136">Azure Security Center</span></span>](https://azure.microsoft.com/services/security-center/)

- [<span data-ttu-id="2f362-137">Blog del team di sicurezza di Azure</span><span class="sxs-lookup"><span data-stu-id="2f362-137">Azure Security Team Blog</span></span>](https://www.azuresecurityorg)

- [<span data-ttu-id="2f362-138">Blog di Azure.com - Sicurezza</span><span class="sxs-lookup"><span data-stu-id="2f362-138">Azure.com Blog - Security</span></span>](https://azure.microsoft.com/blog/topics/security/)

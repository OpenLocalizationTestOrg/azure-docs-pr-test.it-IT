---
title: domande frequenti di Active Directory Reporting su aaaAzure | Documenti Microsoft
description: Domande frequenti sulla creazione di report in Azure Active Directory.
services: active-directory
documentationcenter: 
author: MarkusVi
manager: femila
ms.assetid: 534da0b1-7858-4167-9986-7a62fbd10439
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/22/2017
ms.author: markvi
ms.reviewer: dhanyahk
ms.openlocfilehash: be65a05574ea3b5b190cd02a96b211c571ba70bc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="azure-active-directory-reporting-faq"></a><span data-ttu-id="e703b-103">Domande frequenti sulla creazione di report in Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="e703b-103">Azure Active Directory reporting FAQ</span></span>

<span data-ttu-id="e703b-104">In questo articolo vengono fornite le risposte toofrequently domande frequenti (FAQ) sulla creazione di report di Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="e703b-104">This article includes answers toofrequently asked questions (FAQs) about Azure Active Directory reporting.</span></span>  
<span data-ttu-id="e703b-105">Per altre informazioni, vedere la pagina relativa alla [creazione di report in Azure Active Directory](active-directory-reporting-azure-portal.md)</span><span class="sxs-lookup"><span data-stu-id="e703b-105">For more details, see [Azure Active Directory reporting](active-directory-reporting-azure-portal.md).</span></span> 

<span data-ttu-id="e703b-106">**D: qual è la conservazione dei dati hello per i log di attività (controllo e accessi) nel portale di Azure hello?**</span><span class="sxs-lookup"><span data-stu-id="e703b-106">**Q: What is hello data retention for activity logs (Audit and Sign-ins) in hello Azure portal?**</span></span> 

<span data-ttu-id="e703b-107">**R:** forniamo 7 giorni di dati per i clienti gratuiti e passando tooan Azure AD Premium 1 o 2 Premium licenza, è possibile accedere a dati per i giorni too30.</span><span class="sxs-lookup"><span data-stu-id="e703b-107">**A:** We provide 7 days of data for our free customers and by switching tooan Azure AD Premium 1 or Premium 2 license, you can access data for up too30 days.</span></span> <span data-ttu-id="e703b-108">Per altri dettagli sulla conservazione, vedere la pagina relativa ai [criteri di conservazione dei report di Azure Active Directory](active-directory-reporting-retention.md).</span><span class="sxs-lookup"><span data-stu-id="e703b-108">For more details on retention, see [Azure Active Directory report retention policies](active-directory-reporting-retention.md)</span></span>

--- 

<span data-ttu-id="e703b-109">**D: come tempo fino a quando non vengono visualizzati i dati di attività hello dopo aver completato le attività?**</span><span class="sxs-lookup"><span data-stu-id="e703b-109">**Q: How long does it take until I can see hello Activity data after I have completed my task?**</span></span>

<span data-ttu-id="e703b-110">**R:** log attività di controllo con una latenza compresa tra 15 minuti tooan ora.</span><span class="sxs-lookup"><span data-stu-id="e703b-110">**A:** Audit activity logs have a latency ranging from 15 mins tooan hour.</span></span> <span data-ttu-id="e703b-111">Log attività di accesso con una latenza compreso tra 15 minuti per la maggior parte dei record e le ore too2 per alcuni record.</span><span class="sxs-lookup"><span data-stu-id="e703b-111">Sign-in activity logs have a latency ranging from 15 mins for most records and up too2 hours for a few records.</span></span>

---

<span data-ttu-id="e703b-112">**D: è necessario toobe che un'attività di amministratore globale toosee hello registra nel portale di Azure hello tooget dati o tramite API hello?**</span><span class="sxs-lookup"><span data-stu-id="e703b-112">**Q: Do I need toobe a global admin toosee hello activity logs in hello Azure Portal or tooget data through hello API?**</span></span>

<span data-ttu-id="e703b-113">**R:** No.</span><span class="sxs-lookup"><span data-stu-id="e703b-113">**A:** No.</span></span> <span data-ttu-id="e703b-114">Può essere un **lettore sicurezza**, un **amministratore responsabile della sicurezza** o **amministratore globale** toosee segnalano i dati nel portale di Azure o accedendovi mediante hello API.</span><span class="sxs-lookup"><span data-stu-id="e703b-114">You can either be a **Security Reader**, a **Security Admin** or a **Global Admin** toosee reporting data in Azure Portal or by accessing it through hello API.</span></span>

---

<span data-ttu-id="e703b-115">**D: è possibile ottenere informazioni di log attività di Office 365 tramite il portale di Azure hello?**</span><span class="sxs-lookup"><span data-stu-id="e703b-115">**Q: Can I get Office 365 activity log information through hello Azure portal?**</span></span>

<span data-ttu-id="e703b-116">**R:** anche attività di Office 365 e Azure AD attività registri condividere molte delle risorse della directory hello, se si desidera una visualizzazione completa di hello log attività di Office 365, è necessario passare informazioni del log attività di Office 365 tooget toohello il centro di amministrazione di Office 365.</span><span class="sxs-lookup"><span data-stu-id="e703b-116">**A:** Even though Office 365 activity and Azure AD activity logs share a lot of hello directory resources, if you want a full view of hello Office 365 activity logs, you should go toohello Office 365 Admin Center tooget Office 365 Activity log information.</span></span>

---


<span data-ttu-id="e703b-117">**D: quali API utilizzare tooget informazioni sui log attività di Office 365?**</span><span class="sxs-lookup"><span data-stu-id="e703b-117">**Q: Which APIs do I use tooget information about Office 365 Activity logs?**</span></span>

<span data-ttu-id="e703b-118">**R:** hello tooaccess API di gestione di Office 365 di usare hello [log attività di Office 365 tramite un'API](https://msdn.microsoft.com/office-365/office-365-managment-apis-overview).</span><span class="sxs-lookup"><span data-stu-id="e703b-118">**A:** Use hello Office 365 Management APIs tooaccess hello [Office 365 Activity logs through an API](https://msdn.microsoft.com/office-365/office-365-managment-apis-overview).</span></span>

---

<span data-ttu-id="e703b-119">**D: Quanti record è possibile scaricare dal portale di Azure?**</span><span class="sxs-lookup"><span data-stu-id="e703b-119">**Q: How many records I can download from Azure portal?**</span></span>

<span data-ttu-id="e703b-120">**R:** è possibile scaricare i record too120K da hello portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="e703b-120">**A:** You can download up too120K records from hello Azure portal.</span></span> <span data-ttu-id="e703b-121">record Hello sono ordinati per *più recente* e per impostazione predefinita, si visualizza record hello K 120 più recente.</span><span class="sxs-lookup"><span data-stu-id="e703b-121">hello records are sorted by *most recent* and by default, you get hello most recent 120K records.</span></span> 

---

<span data-ttu-id="e703b-122">**D: come numero di record è query tramite le attività di hello API?**</span><span class="sxs-lookup"><span data-stu-id="e703b-122">**Q: How many records can I query through hello activities API?**</span></span>

<span data-ttu-id="e703b-123">**R:** è possibile eseguire query dei milioni record too1 (se non si utilizza l'operatore top hello, che ordina i record di hello più recente).</span><span class="sxs-lookup"><span data-stu-id="e703b-123">**A:** You can query up too1 million records (if you don’t use hello top operator, which sorts hello record by most recent).</span></span> <span data-ttu-id="e703b-124">Se si utilizza l'operatore "top" hello, è possibile eseguire query dei record too500K.</span><span class="sxs-lookup"><span data-stu-id="e703b-124">If you do use hello “top” operator, you can query up too500K records.</span></span> <span data-ttu-id="e703b-125">È possibile trovare esempi di query in modalità toouse hello API qui [qui](active-directory-reporting-api-getting-started.md).</span><span class="sxs-lookup"><span data-stu-id="e703b-125">You can find sample queries on how toouse hello API here [here](active-directory-reporting-api-getting-started.md).</span></span>

---

<span data-ttu-id="e703b-126">**D: Come ottenere una licenza Premium?**</span><span class="sxs-lookup"><span data-stu-id="e703b-126">**Q: How do I get a premium license?**</span></span>

<span data-ttu-id="e703b-127">**R:** vedere [Introduzione a Azure Active Directory Premium](active-directory-get-started-premium.md) per una domanda toothis di risposta.</span><span class="sxs-lookup"><span data-stu-id="e703b-127">**A:** See [Getting started with Azure Active Directory Premium](active-directory-get-started-premium.md) for an answer toothis question.</span></span>

---

<span data-ttu-id="e703b-128">**D: In quanto tempo è possibile visualizzare le attività dopo aver acquistato una licenza Premium?**</span><span class="sxs-lookup"><span data-stu-id="e703b-128">**Q: How soon should I see activities data after getting a premium license?**</span></span>

<span data-ttu-id="e703b-129">**R:** se si dispongono già dei dati di attività come una licenza gratuita, quindi è possibile visualizzare hello stessi dati.</span><span class="sxs-lookup"><span data-stu-id="e703b-129">**A:** If you already have activities data as a free license, then you can see hello same data.</span></span> <span data-ttu-id="e703b-130">Se non si dispone di dati, saranno necessari uno o due giorni.</span><span class="sxs-lookup"><span data-stu-id="e703b-130">If you don’t have any data, then it will take one or two days.</span></span>

---

<span data-ttu-id="e703b-131">**D: È possibile visualizzare i dati del mese precedente dopo avere acquistato una licenza Azure AD Premium?**</span><span class="sxs-lookup"><span data-stu-id="e703b-131">**Q: Do I see last month's data after getting an Azure AD premium license?**</span></span>

<span data-ttu-id="e703b-132">**R:** se di recente si è passati versione Premium tooa (inclusi una versione di valutazione), è possibile visualizzare inizialmente dati backup too7 giorni.</span><span class="sxs-lookup"><span data-stu-id="e703b-132">**A:** If you have recently switched tooa Premium version (including a trial version), you can see data up too7 days initially.</span></span> <span data-ttu-id="e703b-133">Quando i dati vengono accumulati, verranno visualizzati i giorni too30.</span><span class="sxs-lookup"><span data-stu-id="e703b-133">When data accumulates, you will see up too30 days.</span></span>

---

<span data-ttu-id="e703b-134">**Q: è un evento di rischio di protezione dell'identità, ma vengono non visualizzati Accedi corrispondente in hello tutti gli accessi. È normale?**</span><span class="sxs-lookup"><span data-stu-id="e703b-134">**Q: There is a risk event in Identity Protection but I’m not seeing corresponding sign-in in hello all sign-ins. Is this expected?**</span></span>

<span data-ttu-id="e703b-135">**R:** Sì, la protezione dell'identità valuta il rischio per tutti i flussi di autenticazione, sia interattivi che non interattivi.</span><span class="sxs-lookup"><span data-stu-id="e703b-135">**A:** Yes, Identity Protection evaluates risk for all authentication flows whether if be interactive or non-interactive.</span></span> <span data-ttu-id="e703b-136">Tuttavia, tutti i report solo accessi Mostra solo hello accessi interattivi.</span><span class="sxs-lookup"><span data-stu-id="e703b-136">However, all sign-ins only report shows only hello interactive sign-ins.</span></span>

---

<span data-ttu-id="e703b-137">**D: come è possibile scaricare report "Utenti contrassegno i rischi" hello nel portale di Azure?**</span><span class="sxs-lookup"><span data-stu-id="e703b-137">**Q: How can I download hello “Users flagged for risk” report in Azure portal?**</span></span>

<span data-ttu-id="e703b-138">**R:** toodownload opzione hello *utenti contrassegno i rischi* report verranno aggiunte presto.</span><span class="sxs-lookup"><span data-stu-id="e703b-138">**A:** hello option toodownload *Users flagged for risk* report will be added soon.</span></span>

---

<span data-ttu-id="e703b-139">**D: come si capisce perché un accesso o un utente è stato contrassegnato rischiose hello portale di Azure?**</span><span class="sxs-lookup"><span data-stu-id="e703b-139">**Q: How do I know why a sign-in or a user was flagged risky in hello Azure portal?**</span></span>

<span data-ttu-id="e703b-140">**R:** clienti edizione Premium per altre informazioni su hello sottostante gli eventi di rischio, fare clic sull'utente hello in "Utenti contrassegno i rischi" o facendo clic su "Rischiosi accessi" hello.</span><span class="sxs-lookup"><span data-stu-id="e703b-140">**A:** Premium edition customers can learn more about hello underlying risk events by clicking on hello user in “Users flagged for risk” or by clicking on hello “Risky sign-ins”.</span></span> <span data-ttu-id="e703b-141">I clienti di edizione Free e Basic ottenere toosee agli utenti di rischio hello e accessi senza hello sottostante informazioni sugli eventi di rischio.</span><span class="sxs-lookup"><span data-stu-id="e703b-141">Free and Basic edition customers get toosee hello at-risk users and sign-ins without hello underlying risk event information.</span></span>

---

<span data-ttu-id="e703b-142">**D: come vengono calcolati gli indirizzi IP in accessi hello e report accessi rischiosa??**</span><span class="sxs-lookup"><span data-stu-id="e703b-142">**Q: How are IP addresses calculated in hello sign-ins and risky sign-ins report??**</span></span>

<span data-ttu-id="e703b-143">**R:** gli indirizzi IP vengono rilasciati in modo che non sia disponibile alcuna connessione definitivo tra un indirizzo IP e in cui si trova fisicamente computer hello con tale indirizzo.</span><span class="sxs-lookup"><span data-stu-id="e703b-143">**A:** IP addresses are issued in such a way that there is no definitive connection between an IP address and where hello computer with that address is physically located.</span></span> <span data-ttu-id="e703b-144">Questo è complicato da fattori quali i provider di dispositivi mobili e VPN con il rilascio di indirizzi IP da pool centrale spesso molto distanti da dove dispositivo client hello viene effettivamente utilizzato.</span><span class="sxs-lookup"><span data-stu-id="e703b-144">This is complicated by factors such as mobile providers and VPNs issuing IP addresses from central pools often very far from where hello client device is actually used.</span></span> <span data-ttu-id="e703b-145">Dato hello precedente, la conversione di posizione fisica tooa di indirizzo IP è un lavoro migliore in base alle tracce, i dati del Registro di sistema, ricerche inverse e altre informazioni.</span><span class="sxs-lookup"><span data-stu-id="e703b-145">Given hello above, converting IP address tooa physical location is a best effort based on traces, registry data, reverse look ups and other information.</span></span> 

---

---
title: Domande frequenti sulla creazione di report in Azure Active Directory | Documentazione Microsoft
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
ms.openlocfilehash: accf292f70bf0eafdefc00c3feeaf8e346605401
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/29/2017
---
# <a name="azure-active-directory-reporting-faq"></a><span data-ttu-id="9a9d0-103">Domande frequenti sulla creazione di report in Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="9a9d0-103">Azure Active Directory reporting FAQ</span></span>

<span data-ttu-id="9a9d0-104">Questo articolo include risposte alle domande frequenti sulla creazione di report in Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="9a9d0-104">This article includes answers to frequently asked questions (FAQs) about Azure Active Directory reporting.</span></span>  
<span data-ttu-id="9a9d0-105">Per altre informazioni, vedere la pagina relativa alla [creazione di report in Azure Active Directory](active-directory-reporting-azure-portal.md)</span><span class="sxs-lookup"><span data-stu-id="9a9d0-105">For more details, see [Azure Active Directory reporting](active-directory-reporting-azure-portal.md).</span></span> 

<span data-ttu-id="9a9d0-106">**D: Qual è la conservazione dei dati per i log attività (controllo e accessi) nel portale di Azure?**</span><span class="sxs-lookup"><span data-stu-id="9a9d0-106">**Q: What is the data retention for activity logs (Audit and Sign-ins) in the Azure portal?**</span></span> 

<span data-ttu-id="9a9d0-107">**R:** Offriamo 7 giorni di dati per i clienti con sottoscrizione gratuita. Passando a una licenza AD Premium 1 o Azure AD Premium 2 è possibile accedere ai dati fino a 30 giorni.</span><span class="sxs-lookup"><span data-stu-id="9a9d0-107">**A:** We provide 7 days of data for our free customers and by switching to an Azure AD Premium 1 or Premium 2 license, you can access data for up to 30 days.</span></span> <span data-ttu-id="9a9d0-108">Per altri dettagli sulla conservazione, vedere la pagina relativa ai [criteri di conservazione dei report di Azure Active Directory](active-directory-reporting-retention.md).</span><span class="sxs-lookup"><span data-stu-id="9a9d0-108">For more details on retention, see [Azure Active Directory report retention policies](active-directory-reporting-retention.md)</span></span>

--- 

<span data-ttu-id="9a9d0-109">**D: Quanto tempo occorre per la visualizzazione dei dati sull'attività dopo il completamento della stessa?**</span><span class="sxs-lookup"><span data-stu-id="9a9d0-109">**Q: How long does it take until I can see the Activity data after I have completed my task?**</span></span>

<span data-ttu-id="9a9d0-110">**R:** I log dell'attività di controllo hanno una latenza compresa tra 15 minuti e un'ora.</span><span class="sxs-lookup"><span data-stu-id="9a9d0-110">**A:** Audit activity logs have a latency ranging from 15 mins to an hour.</span></span> <span data-ttu-id="9a9d0-111">I log dell'attività di accesso hanno una latenza compresa tra 15 minuti per la maggior parte dei record e fino a 2 ore per altri record.</span><span class="sxs-lookup"><span data-stu-id="9a9d0-111">Sign-in activity logs have a latency ranging from 15 mins for most records and up to 2 hours for a few records.</span></span>

---

<span data-ttu-id="9a9d0-112">**Q: È necessario essere amministratore globale per visualizzare i log attività nel portale di Azure o per ottenere i dati tramite l'API?**</span><span class="sxs-lookup"><span data-stu-id="9a9d0-112">**Q: Do I need to be a global admin to see the activity logs in the Azure Portal or to get data through the API?**</span></span>

<span data-ttu-id="9a9d0-113">**R:** No.</span><span class="sxs-lookup"><span data-stu-id="9a9d0-113">**A:** No.</span></span> <span data-ttu-id="9a9d0-114">L'utente può avere un **ruolo con autorizzazioni di lettura per la sicurezza**, può essere un **amministratore della protezione** o un **amministratore globale** per visualizzare i dati dei report nel portale di Azure o accedendovi tramite l'API.</span><span class="sxs-lookup"><span data-stu-id="9a9d0-114">You can either be a **Security Reader**, a **Security Admin** or a **Global Admin** to see reporting data in Azure Portal or by accessing it through the API.</span></span>

---

<span data-ttu-id="9a9d0-115">**D: È possibile ottenere informazioni sui log attività di Office 365 tramite il portale di Azure?**</span><span class="sxs-lookup"><span data-stu-id="9a9d0-115">**Q: Can I get Office 365 activity log information through the Azure portal?**</span></span>

<span data-ttu-id="9a9d0-116">**R:** Sebbene l'attività di Office 365 e i log attività di Azure AD condividano numerose risorse della directory, se si desidera una visualizzazione completa dei log attività di Office 365, è necessario usare l'interfaccia di amministrazione di Office 365 per ottenere informazioni sui log attività di Office 365.</span><span class="sxs-lookup"><span data-stu-id="9a9d0-116">**A:** Even though Office 365 activity and Azure AD activity logs share a lot of the directory resources, if you want a full view of the Office 365 activity logs, you should go to the Office 365 Admin Center to get Office 365 Activity log information.</span></span>

---


<span data-ttu-id="9a9d0-117">**D: Quali API è necessario usare per ottenere informazioni sui log attività di Office 365?**</span><span class="sxs-lookup"><span data-stu-id="9a9d0-117">**Q: Which APIs do I use to get information about Office 365 Activity logs?**</span></span>

<span data-ttu-id="9a9d0-118">**R:** Usare le API Gestione di Office 365 per accedere ai [log attività di Office 365 tramite un'API](https://msdn.microsoft.com/office-365/office-365-managment-apis-overview).</span><span class="sxs-lookup"><span data-stu-id="9a9d0-118">**A:** Use the Office 365 Management APIs to access the [Office 365 Activity logs through an API](https://msdn.microsoft.com/office-365/office-365-managment-apis-overview).</span></span>

---

<span data-ttu-id="9a9d0-119">**D: Quanti record è possibile scaricare dal portale di Azure?**</span><span class="sxs-lookup"><span data-stu-id="9a9d0-119">**Q: How many records I can download from Azure portal?**</span></span>

<span data-ttu-id="9a9d0-120">**R:** Dal portale di Azure è possibile scaricare fino a 120 KB di record.</span><span class="sxs-lookup"><span data-stu-id="9a9d0-120">**A:** You can download up to 120K records from the Azure portal.</span></span> <span data-ttu-id="9a9d0-121">I record vengono ordinati in base ai *più recenti* e, per impostazione predefinita, vengono visualizzati 120 KB dei record più recenti.</span><span class="sxs-lookup"><span data-stu-id="9a9d0-121">The records are sorted by *most recent* and by default, you get the most recent 120K records.</span></span> 

---

<span data-ttu-id="9a9d0-122">**D: Su quanti record è possibile eseguire query tramite le API delle attività?**</span><span class="sxs-lookup"><span data-stu-id="9a9d0-122">**Q: How many records can I query through the activities API?**</span></span>

<span data-ttu-id="9a9d0-123">**R:** Le query possono essere eseguite su un numero massimo di 1 milione di record (se non si usa l'operatore TOP, che ordina i record in base al più recente).</span><span class="sxs-lookup"><span data-stu-id="9a9d0-123">**A:** You can query up to 1 million records (if you don’t use the top operator, which sorts the record by most recent).</span></span> <span data-ttu-id="9a9d0-124">Se si usa l'operatore TOP, è possibile eseguire query su un massimo di 500 KB di record.</span><span class="sxs-lookup"><span data-stu-id="9a9d0-124">If you do use the “top” operator, you can query up to 500K records.</span></span> <span data-ttu-id="9a9d0-125">[Qui](active-directory-reporting-api-getting-started.md) è possibile trovare le query di esempio su come usare l'API.</span><span class="sxs-lookup"><span data-stu-id="9a9d0-125">You can find sample queries on how to use the API here [here](active-directory-reporting-api-getting-started.md).</span></span>

---

<span data-ttu-id="9a9d0-126">**D: Come ottenere una licenza Premium?**</span><span class="sxs-lookup"><span data-stu-id="9a9d0-126">**Q: How do I get a premium license?**</span></span>

<span data-ttu-id="9a9d0-127">**R:** Per la risposta a questa domanda, vedere [Introduzione ad Azure Active Directory Premium](active-directory-get-started-premium.md).</span><span class="sxs-lookup"><span data-stu-id="9a9d0-127">**A:** See [Getting started with Azure Active Directory Premium](active-directory-get-started-premium.md) for an answer to this question.</span></span>

---

<span data-ttu-id="9a9d0-128">**D: In quanto tempo è possibile visualizzare le attività dopo aver acquistato una licenza Premium?**</span><span class="sxs-lookup"><span data-stu-id="9a9d0-128">**Q: How soon should I see activities data after getting a premium license?**</span></span>

<span data-ttu-id="9a9d0-129">**R:** Se si dispone già di dati sulle attività come licenza gratuita, è possibile visualizzare questi dati.</span><span class="sxs-lookup"><span data-stu-id="9a9d0-129">**A:** If you already have activities data as a free license, then you can see the same data.</span></span> <span data-ttu-id="9a9d0-130">Se non si dispone di dati, saranno necessari uno o due giorni.</span><span class="sxs-lookup"><span data-stu-id="9a9d0-130">If you don’t have any data, then it will take one or two days.</span></span>

---

<span data-ttu-id="9a9d0-131">**D: È possibile visualizzare i dati del mese precedente dopo avere acquistato una licenza Azure AD Premium?**</span><span class="sxs-lookup"><span data-stu-id="9a9d0-131">**Q: Do I see last month's data after getting an Azure AD premium license?**</span></span>

<span data-ttu-id="9a9d0-132">**R:**: Se di recente si è passati alla versione Premium (anche di valutazione), inizialmente è possibile visualizzare i dati fino a 7 giorni.</span><span class="sxs-lookup"><span data-stu-id="9a9d0-132">**A:** If you have recently switched to a Premium version (including a trial version), you can see data up to 7 days initially.</span></span> <span data-ttu-id="9a9d0-133">Quando i dati si accumulano, verranno visualizzati fino a 30 giorni.</span><span class="sxs-lookup"><span data-stu-id="9a9d0-133">When data accumulates, you will see up to 30 days.</span></span>

---

<span data-ttu-id="9a9d0-134">**D: Esiste un evento di rischio nella protezione dell'identità, ma non vengono visualizzati accessi corrispondenti in tutti gli accessi. È normale?**</span><span class="sxs-lookup"><span data-stu-id="9a9d0-134">**Q: There is a risk event in Identity Protection but I’m not seeing corresponding sign-in in the all sign-ins. Is this expected?**</span></span>

<span data-ttu-id="9a9d0-135">**R:** Sì, la protezione dell'identità valuta il rischio per tutti i flussi di autenticazione, sia interattivi che non interattivi.</span><span class="sxs-lookup"><span data-stu-id="9a9d0-135">**A:** Yes, Identity Protection evaluates risk for all authentication flows whether if be interactive or non-interactive.</span></span> <span data-ttu-id="9a9d0-136">Tuttavia, tutti i report degli accessi mostrano solo gli accessi interattivi.</span><span class="sxs-lookup"><span data-stu-id="9a9d0-136">However, all sign-ins only report shows only the interactive sign-ins.</span></span>

---

<span data-ttu-id="9a9d0-137">**D: Come è possibile scaricare il report "Utenti contrassegnati per il rischio" nel portale di Azure?**</span><span class="sxs-lookup"><span data-stu-id="9a9d0-137">**Q: How can I download the “Users flagged for risk” report in Azure portal?**</span></span>

<span data-ttu-id="9a9d0-138">**R:**: L'opzione per scaricare il report *Utenti contrassegnati per il rischio* verrà aggiunta a breve.</span><span class="sxs-lookup"><span data-stu-id="9a9d0-138">**A:** The option to download *Users flagged for risk* report will be added soon.</span></span>

---

<span data-ttu-id="9a9d0-139">**D: Come sapere perché un accesso o un utente è stato contrassegnato come rischioso nel portale di Azure?**</span><span class="sxs-lookup"><span data-stu-id="9a9d0-139">**Q: How do I know why a sign-in or a user was flagged risky in the Azure portal?**</span></span>

<span data-ttu-id="9a9d0-140">**R:** I clienti dell'edizione Premium possono scoprire altre informazioni sugli eventi di rischio sottostanti facendo clic sull'utente in "Utenti contrassegnati per il rischio" o facendo clic su "Accessi a rischio".</span><span class="sxs-lookup"><span data-stu-id="9a9d0-140">**A:** Premium edition customers can learn more about the underlying risk events by clicking on the user in “Users flagged for risk” or by clicking on the “Risky sign-ins”.</span></span> <span data-ttu-id="9a9d0-141">I clienti della versione Basic e Free riescono a visualizzare gli utenti e gli accessi a rischio senza le informazioni sull'evento di rischio sottostante.</span><span class="sxs-lookup"><span data-stu-id="9a9d0-141">Free and Basic edition customers get to see the at-risk users and sign-ins without the underlying risk event information.</span></span>

---

<span data-ttu-id="9a9d0-142">**D: Come vengono calcolati gli indirizzi IP nel report degli accessi e degli accessi a rischio?**</span><span class="sxs-lookup"><span data-stu-id="9a9d0-142">**Q: How are IP addresses calculated in the sign-ins and risky sign-ins report??**</span></span>

<span data-ttu-id="9a9d0-143">**R:** Gli indirizzi IP vengono rilasciati in modo che non esista una connessione certa tra un IP e la posizione in cui si trova fisicamente il computer con tale indirizzo.</span><span class="sxs-lookup"><span data-stu-id="9a9d0-143">**A:** IP addresses are issued in such a way that there is no definitive connection between an IP address and where the computer with that address is physically located.</span></span> <span data-ttu-id="9a9d0-144">A ciò si aggiungono fattori come la possibilità che provider di telefonia mobile e VPN rilascino indirizzi IP da pool centrali spesso molto distanti dal luogo in cui viene effettivamente usato il dispositivo client.</span><span class="sxs-lookup"><span data-stu-id="9a9d0-144">This is complicated by factors such as mobile providers and VPNs issuing IP addresses from central pools often very far from where the client device is actually used.</span></span> <span data-ttu-id="9a9d0-145">Per questi motivi, la conversione di un indirizzo IP in una posizione fisica è un'approssimazione basata su tracce, dati del Registro di sistema, ricerche inverse e altre informazioni.</span><span class="sxs-lookup"><span data-stu-id="9a9d0-145">Given the above, converting IP address to a physical location is a best effort based on traces, registry data, reverse look ups and other information.</span></span> 

---

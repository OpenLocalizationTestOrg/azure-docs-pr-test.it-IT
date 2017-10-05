---
title: "Considerazioni di progettazione per la soluzione ibrida di gestione delle identità di Azure Active Directory: determinare i requisiti di gestione dei contenuti | Documentazione Microsoft"
description: "Fornisce importanti informazioni su come determinare i requisiti di gestione dei contenuti dell'azienda. In genere, quando un utente usa un dispositivo personale, si avvale di più credenziali diverse, in base all'applicazione a cui deve accedere. È importante quindi distinguere i contenuti creati usando credenziali personali rispetto a quelli realizzati ricorrendo a credenziali aziendali. La soluzione di identità adottata deve essere in grado di interagire con i servizi cloud, in modo da fornire un'esperienza trasparente per l'utente finale, garantirne la privacy e migliorare la protezione contro la perdita di dati."
documentationcenter: 
services: active-directory
author: billmath
manager: femila
editor: 
ms.assetid: dd1ef776-db4d-4ab8-9761-2adaa5a4f004
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 07/18/2017
ms.author: billmath
ms.openlocfilehash: 840de1e1fcba74285788d51d8f544375f0affa77
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/03/2017
---
# <a name="determine-content-management-requirements-for-your-hybrid-identity-solution"></a><span data-ttu-id="e38a8-106">Determinare i requisiti di gestione dei contenuti per una soluzione di identità ibrida</span><span class="sxs-lookup"><span data-stu-id="e38a8-106">Determine content management requirements for your hybrid identity solution</span></span>
<span data-ttu-id="e38a8-107">Comprendere i requisiti aziendali relativi alla gestione dei contenuti può incidere direttamente sulla decisione in merito alla soluzione di identità ibrida da usare.</span><span class="sxs-lookup"><span data-stu-id="e38a8-107">Understanding the content management requirements for your business may direct affect your decision on which hybrid identity solution to use.</span></span> <span data-ttu-id="e38a8-108">Con la proliferazione delle tipologie di dispositivi e la possibilità per gli utenti di usare dispositivi personali anche nelle attività lavorative (approccio[BYOD](http://aka.ms/byodcg)), è sempre più forte l'esigenza per le aziende di proteggere i dati senza compromettere la privacy degli utenti.</span><span class="sxs-lookup"><span data-stu-id="e38a8-108">With the proliferation of multiple devices and the capability of users to bring their own devices ([BYOD](http://aka.ms/byodcg)), the company must protect its own data but it also must keep user’s privacy intact.</span></span> <span data-ttu-id="e38a8-109">In genere, quando un utente usa un dispositivo personale, si avvale di più credenziali diverse, in base all'applicazione a cui deve accedere.</span><span class="sxs-lookup"><span data-stu-id="e38a8-109">Usually when a user has his own device he might have also multiple credentials that will be alternating according to the application that he uses.</span></span> <span data-ttu-id="e38a8-110">È importante quindi distinguere i contenuti creati usando credenziali personali rispetto a quelli realizzati ricorrendo a credenziali aziendali.</span><span class="sxs-lookup"><span data-stu-id="e38a8-110">It is important to differentiate what content was created using personal credentials versus the ones created using corporate credentials.</span></span> <span data-ttu-id="e38a8-111">La soluzione di identità adottata deve essere in grado di interagire con i servizi cloud, in modo da fornire un'esperienza trasparente per l'utente finale, garantirne la privacy e migliorare la protezione contro la perdita di dati.</span><span class="sxs-lookup"><span data-stu-id="e38a8-111">Your identity solution should be able to interact with cloud services to provide a seamless experience to the end user while ensure his privacy and increase the protection against data leakage.</span></span> 

<span data-ttu-id="e38a8-112">La soluzione di identità deve essere inoltre sottoposta a vari controlli tecnici per permettere la gestione dei contenuti, come illustrato nella figura seguente:</span><span class="sxs-lookup"><span data-stu-id="e38a8-112">Your identity solution will be leveraged by different technical controls in order to provide content management as shown in the figure below:</span></span>

![](./media/hybrid-id-design-considerations/securitycontrols.png)

<span data-ttu-id="e38a8-113">**Controlli di protezione che interessano il sistema di gestione delle identità**</span><span class="sxs-lookup"><span data-stu-id="e38a8-113">**Security controls that will be leveraging your identity management system**</span></span>

<span data-ttu-id="e38a8-114">In generale, i requisiti di gestione dei contenuti interessano il sistema di gestione delle identità nelle aree seguenti:</span><span class="sxs-lookup"><span data-stu-id="e38a8-114">In general, content management requirements will leverage your identity management system in the following areas:</span></span>

* <span data-ttu-id="e38a8-115">Privacy: identificare l'utente proprietario di una risorsa e applicare i controlli appropriati per garantirne l'integrità.</span><span class="sxs-lookup"><span data-stu-id="e38a8-115">Privacy: identifying the user that owns a resource and applying the appropriate controls to maintain integrity.</span></span>
* <span data-ttu-id="e38a8-116">Classificazione dei dati: identificare l'utente o il gruppo e il livello di accesso a un oggetto in base a una classificazione prestabilita.</span><span class="sxs-lookup"><span data-stu-id="e38a8-116">Data Classification: identify the user or group and level of access to an object according to its classification.</span></span> 
* <span data-ttu-id="e38a8-117">Protezione contro la perdita di dati: per poter convalidare l'identità degli utenti, il sistema di gestione delle identità deve poter interagire con i controlli di protezione adottati per evitare perdite di dati.</span><span class="sxs-lookup"><span data-stu-id="e38a8-117">Data Leakage Protection: security controls responsible for protecting data to avoid leakage will need to interact with the identity system to validate the user’s identity.</span></span> <span data-ttu-id="e38a8-118">Questo aspetto è importante anche per eventuali esigenze di auditing.</span><span class="sxs-lookup"><span data-stu-id="e38a8-118">This is also important for auditing trail purpose.</span></span>

> [!NOTE]
> <span data-ttu-id="e38a8-119">Leggere l'articolo sulla [classificazione dei dati per la conformità al cloud](http://download.microsoft.com/download/0/A/3/0A3BE969-85C5-4DD2-83B6-366AA71D1FE3/Data-Classification-for-Cloud-Readiness.pdf) per maggiori informazioni sulle linee guida e le procedure consigliate per la classificazione dei dati.</span><span class="sxs-lookup"><span data-stu-id="e38a8-119">Read [data classification for cloud readiness](http://download.microsoft.com/download/0/A/3/0A3BE969-85C5-4DD2-83B6-366AA71D1FE3/Data-Classification-for-Cloud-Readiness.pdf) for more information about best practices and guidelines for data classification.</span></span>
> 
> 

<span data-ttu-id="e38a8-120">Quando si pianifica una soluzione di identità ibrida, assicurarsi che venga fornita una risposta alle domande seguenti, in base ai requisiti aziendali:</span><span class="sxs-lookup"><span data-stu-id="e38a8-120">When planning your hybrid identity solution ensure that the following questions are answered according to your organization’s requirements:</span></span>

* <span data-ttu-id="e38a8-121">Sono presenti in azienda controlli di sicurezza per garantire la riservatezza dei dati?</span><span class="sxs-lookup"><span data-stu-id="e38a8-121">Does your company have security controls in place to enforce data privacy?</span></span>
  * <span data-ttu-id="e38a8-122">In caso affermativo, sarà possibile integrarli con la soluzione di identità ibrida che si intende adottare?</span><span class="sxs-lookup"><span data-stu-id="e38a8-122">If yes, will those security controls be able to integrate with the hybrid identity solution that you are going to adopt?</span></span>
* <span data-ttu-id="e38a8-123">È presente in azienda un sistema di classificazione dei dati?</span><span class="sxs-lookup"><span data-stu-id="e38a8-123">Does your company use data classification?</span></span>
  * <span data-ttu-id="e38a8-124">In caso affermativo, sarà possibile integrarlo con la soluzione di identità ibrida che si intende adottare?</span><span class="sxs-lookup"><span data-stu-id="e38a8-124">If yes, is the current solution able to integrate with the hybrid identity solution that you are going to adopt?</span></span>
* <span data-ttu-id="e38a8-125">È presente in azienda un sistema di protezione contro la perdita di dati?</span><span class="sxs-lookup"><span data-stu-id="e38a8-125">Does your company currently have any solution for data leakage?</span></span> 
  * <span data-ttu-id="e38a8-126">In caso affermativo, sarà possibile integrarlo con la soluzione di identità ibrida che si intende adottare?</span><span class="sxs-lookup"><span data-stu-id="e38a8-126">If yes, is the current solution able to integrate with the hybrid identity solution that you are going to adopt?</span></span>
* <span data-ttu-id="e38a8-127">L'azienda desidera controllare l'accesso alle risorse?</span><span class="sxs-lookup"><span data-stu-id="e38a8-127">Does your company need to audit access to resources?</span></span>
  * <span data-ttu-id="e38a8-128">In caso affermativo, che tipo di risorse?</span><span class="sxs-lookup"><span data-stu-id="e38a8-128">If yes, what type of resources?</span></span>
  * <span data-ttu-id="e38a8-129">Quale livello di informazioni è necessario?</span><span class="sxs-lookup"><span data-stu-id="e38a8-129">If yes, what level of information is necessary?</span></span>
  * <span data-ttu-id="e38a8-130">Dove deve trovarsi il log di controllo,</span><span class="sxs-lookup"><span data-stu-id="e38a8-130">If yes, where the audit log must reside?</span></span> <span data-ttu-id="e38a8-131">in locale o nel cloud?</span><span class="sxs-lookup"><span data-stu-id="e38a8-131">On-premises or in the cloud?</span></span>
* <span data-ttu-id="e38a8-132">L'azienda desidera crittografare i messaggi e-mail che contengono dati riservati (numeri di previdenza sociale, numeri di carta di credito e così via)?</span><span class="sxs-lookup"><span data-stu-id="e38a8-132">Does your company need to encrypt any emails that contain sensitive data (SSNs, credit card numbers, etc)?</span></span>
* <span data-ttu-id="e38a8-133">L'azienda desidera crittografare tutti i documenti e i contenuti condivisi con partner commerciali esterni?</span><span class="sxs-lookup"><span data-stu-id="e38a8-133">Does your company need to encrypt all documents/contents shared with external business partners?</span></span>
* <span data-ttu-id="e38a8-134">L'azienda intende applicare criteri specifici su determinati tipi di e-mail ("non rispondere a tutti", "non inoltrare" e così via)?</span><span class="sxs-lookup"><span data-stu-id="e38a8-134">Does your company need to enforce corporate policies on certain kinds of emails (do no reply all, do not forward)?</span></span>

> [!NOTE]
> <span data-ttu-id="e38a8-135">Accertarsi di prendere nota di ogni risposta e comprendere la logica che ne sta alla base.</span><span class="sxs-lookup"><span data-stu-id="e38a8-135">Make sure to take notes of each answer and understand the rationale behind the answer.</span></span> <span data-ttu-id="e38a8-136">[definizione della strategia di protezione dei dati](active-directory-hybrid-identity-design-considerations-data-protection-strategy.md) esamina le opzioni disponibili con i relativi vantaggi e svantaggi.</span><span class="sxs-lookup"><span data-stu-id="e38a8-136">[Define Data Protection Strategy](active-directory-hybrid-identity-design-considerations-data-protection-strategy.md) will go over the options available and advantages/disadvantages of each option.</span></span>  <span data-ttu-id="e38a8-137">Una volta fornite le risposte a queste domande, sarà possibile selezionare l'opzione più adatta in base alle esigenze aziendali.</span><span class="sxs-lookup"><span data-stu-id="e38a8-137">By having answered those questions you will select which option best suits your business needs.</span></span>
> 
> 

## <a name="next-steps"></a><span data-ttu-id="e38a8-138">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="e38a8-138">Next steps</span></span>
[<span data-ttu-id="e38a8-139">Determinare i requisiti di controllo di accesso</span><span class="sxs-lookup"><span data-stu-id="e38a8-139">Determine access control requirements</span></span>](active-directory-hybrid-identity-design-considerations-accesscontrol-requirements.md)

## <a name="see-also"></a><span data-ttu-id="e38a8-140">Vedere anche</span><span class="sxs-lookup"><span data-stu-id="e38a8-140">See Also</span></span>
[<span data-ttu-id="e38a8-141">Panoramica delle considerazioni di progettazione</span><span class="sxs-lookup"><span data-stu-id="e38a8-141">Design considerations overview</span></span>](active-directory-hybrid-identity-design-considerations-overview.md)


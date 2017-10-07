---
title: "Considerazioni sulla progettazione di aaaAzure Active Directory ibrido identità - determinare i requisiti di gestione del contenuto | Documenti Microsoft"
description: "Fornisce informazioni approfondite come toodetermine hello requisiti di gestione dei contenuti dell'azienda. In genere quando un utente ha il proprio dispositivo potrebbe essere anche più credenziali che verranno essere alternati applicazione toohello in base che utilizza. È importante toodifferentiate il contenuto è stato creato utilizzando le credenziali personali rispetto a quelli creati utilizzando le credenziali aziendale hello. La soluzione di identità deve essere in grado di toointeract con cloud services tooprovide un utente finale di esperienza toohello durante garantire la privacy e aumentare la protezione di hello da perdita di dati."
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
ms.openlocfilehash: 607d366633c37b65ec5cf8ae5c64d73ca1cc96b7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="determine-content-management-requirements-for-your-hybrid-identity-solution"></a><span data-ttu-id="83ef0-106">Determinare i requisiti di gestione dei contenuti per una soluzione di identità ibrida</span><span class="sxs-lookup"><span data-stu-id="83ef0-106">Determine content management requirements for your hybrid identity solution</span></span>
<span data-ttu-id="83ef0-107">Informazioni sui requisiti di gestione dei contenuti hello per l'azienda può indirizzare influire sulla decisione su quale toouse soluzione di identità ibride.</span><span class="sxs-lookup"><span data-stu-id="83ef0-107">Understanding hello content management requirements for your business may direct affect your decision on which hybrid identity solution toouse.</span></span> <span data-ttu-id="83ef0-108">Con hello proliferazione di più dispositivi e dalla capacità di hello di utenti toobring i propri dispositivi ([BYOD](http://aka.ms/byodcg)), società hello devono proteggere i propri dati ma anche necessario tenere privacy dell'utente intatto.</span><span class="sxs-lookup"><span data-stu-id="83ef0-108">With hello proliferation of multiple devices and hello capability of users toobring their own devices ([BYOD](http://aka.ms/byodcg)), hello company must protect its own data but it also must keep user’s privacy intact.</span></span> <span data-ttu-id="83ef0-109">In genere quando un utente ha il proprio dispositivo potrebbe essere anche più credenziali che verranno essere alternati applicazione toohello in base che utilizza.</span><span class="sxs-lookup"><span data-stu-id="83ef0-109">Usually when a user has his own device he might have also multiple credentials that will be alternating according toohello application that he uses.</span></span> <span data-ttu-id="83ef0-110">È importante toodifferentiate il contenuto è stato creato utilizzando le credenziali personali rispetto a quelli creati utilizzando le credenziali aziendale hello.</span><span class="sxs-lookup"><span data-stu-id="83ef0-110">It is important toodifferentiate what content was created using personal credentials versus hello ones created using corporate credentials.</span></span> <span data-ttu-id="83ef0-111">La soluzione di identità deve essere in grado di toointeract con cloud services tooprovide un utente finale di esperienza toohello durante garantire la privacy e aumentare la protezione di hello da perdita di dati.</span><span class="sxs-lookup"><span data-stu-id="83ef0-111">Your identity solution should be able toointeract with cloud services tooprovide a seamless experience toohello end user while ensure his privacy and increase hello protection against data leakage.</span></span> 

<span data-ttu-id="83ef0-112">La soluzione di identità verrà utilizzata dai diversi controlli tecnici nella gestione dei contenuti tooprovide ordine come illustrato nella figura hello seguente:</span><span class="sxs-lookup"><span data-stu-id="83ef0-112">Your identity solution will be leveraged by different technical controls in order tooprovide content management as shown in hello figure below:</span></span>

![](./media/hybrid-id-design-considerations/securitycontrols.png)

<span data-ttu-id="83ef0-113">**Controlli di protezione che interessano il sistema di gestione delle identità**</span><span class="sxs-lookup"><span data-stu-id="83ef0-113">**Security controls that will be leveraging your identity management system**</span></span>

<span data-ttu-id="83ef0-114">In generale, i requisiti di gestione dei contenuti verranno utilizzati il sistema di gestione di identità in hello seguenti aree:</span><span class="sxs-lookup"><span data-stu-id="83ef0-114">In general, content management requirements will leverage your identity management system in hello following areas:</span></span>

* <span data-ttu-id="83ef0-115">Privacy: identificazione utente hello che possiede una risorsa e applicare l'integrità toomaintain hello controlli appropriati.</span><span class="sxs-lookup"><span data-stu-id="83ef0-115">Privacy: identifying hello user that owns a resource and applying hello appropriate controls toomaintain integrity.</span></span>
* <span data-ttu-id="83ef0-116">Classificazione dei dati: identificare l'utente hello o gruppo e il livello di oggetto tooan accesso in base tooits classificazione.</span><span class="sxs-lookup"><span data-stu-id="83ef0-116">Data Classification: identify hello user or group and level of access tooan object according tooits classification.</span></span> 
* <span data-ttu-id="83ef0-117">Protezione di perdita di dati: i controlli di sicurezza responsabili della protezione tooavoid perdita dei dati saranno necessario toointeract con hello identità sistema toovalidate hello identità dell'utente.</span><span class="sxs-lookup"><span data-stu-id="83ef0-117">Data Leakage Protection: security controls responsible for protecting data tooavoid leakage will need toointeract with hello identity system toovalidate hello user’s identity.</span></span> <span data-ttu-id="83ef0-118">Questo aspetto è importante anche per eventuali esigenze di auditing.</span><span class="sxs-lookup"><span data-stu-id="83ef0-118">This is also important for auditing trail purpose.</span></span>

> [!NOTE]
> <span data-ttu-id="83ef0-119">Leggere l'articolo sulla [classificazione dei dati per la conformità al cloud](http://download.microsoft.com/download/0/A/3/0A3BE969-85C5-4DD2-83B6-366AA71D1FE3/Data-Classification-for-Cloud-Readiness.pdf) per maggiori informazioni sulle linee guida e le procedure consigliate per la classificazione dei dati.</span><span class="sxs-lookup"><span data-stu-id="83ef0-119">Read [data classification for cloud readiness](http://download.microsoft.com/download/0/A/3/0A3BE969-85C5-4DD2-83B6-366AA71D1FE3/Data-Classification-for-Cloud-Readiness.pdf) for more information about best practices and guidelines for data classification.</span></span>
> 
> 

<span data-ttu-id="83ef0-120">Quando pianificazione della soluzione di identità ibrida accertarsi che hello seguenti domande in base ai requisiti dell'organizzazione tooyour:</span><span class="sxs-lookup"><span data-stu-id="83ef0-120">When planning your hybrid identity solution ensure that hello following questions are answered according tooyour organization’s requirements:</span></span>

* <span data-ttu-id="83ef0-121">L'azienda prevede dei controlli di sicurezza in luogo tooenforce privacy dei dati?</span><span class="sxs-lookup"><span data-stu-id="83ef0-121">Does your company have security controls in place tooenforce data privacy?</span></span>
  * <span data-ttu-id="83ef0-122">In caso affermativo, i controlli di sicurezza sarà in grado di toointegrate con una soluzione con identità ibrida hello siano tooadopt corso?</span><span class="sxs-lookup"><span data-stu-id="83ef0-122">If yes, will those security controls be able toointegrate with hello hybrid identity solution that you are going tooadopt?</span></span>
* <span data-ttu-id="83ef0-123">È presente in azienda un sistema di classificazione dei dati?</span><span class="sxs-lookup"><span data-stu-id="83ef0-123">Does your company use data classification?</span></span>
  * <span data-ttu-id="83ef0-124">In caso affermativo, è toointegrate hello corrente soluzione in grado di soluzione con identità ibrida hello siano tooadopt corso?</span><span class="sxs-lookup"><span data-stu-id="83ef0-124">If yes, is hello current solution able toointegrate with hello hybrid identity solution that you are going tooadopt?</span></span>
* <span data-ttu-id="83ef0-125">È presente in azienda un sistema di protezione contro la perdita di dati?</span><span class="sxs-lookup"><span data-stu-id="83ef0-125">Does your company currently have any solution for data leakage?</span></span> 
  * <span data-ttu-id="83ef0-126">In caso affermativo, è toointegrate hello corrente soluzione in grado di soluzione con identità ibrida hello siano tooadopt corso?</span><span class="sxs-lookup"><span data-stu-id="83ef0-126">If yes, is hello current solution able toointegrate with hello hybrid identity solution that you are going tooadopt?</span></span>
* <span data-ttu-id="83ef0-127">L'azienda necessita di tooaudit accesso tooresources?</span><span class="sxs-lookup"><span data-stu-id="83ef0-127">Does your company need tooaudit access tooresources?</span></span>
  * <span data-ttu-id="83ef0-128">In caso affermativo, che tipo di risorse?</span><span class="sxs-lookup"><span data-stu-id="83ef0-128">If yes, what type of resources?</span></span>
  * <span data-ttu-id="83ef0-129">Quale livello di informazioni è necessario?</span><span class="sxs-lookup"><span data-stu-id="83ef0-129">If yes, what level of information is necessary?</span></span>
  * <span data-ttu-id="83ef0-130">In caso affermativo, in cui deve risiedere il log di controllo di hello?</span><span class="sxs-lookup"><span data-stu-id="83ef0-130">If yes, where hello audit log must reside?</span></span> <span data-ttu-id="83ef0-131">Locale o nel cloud hello?</span><span class="sxs-lookup"><span data-stu-id="83ef0-131">On-premises or in hello cloud?</span></span>
* <span data-ttu-id="83ef0-132">L'azienda necessita tooencrypt eventuali messaggi di posta elettronica che contengono dati riservati (SSNs, i numeri di carta di credito e così via)?</span><span class="sxs-lookup"><span data-stu-id="83ef0-132">Does your company need tooencrypt any emails that contain sensitive data (SSNs, credit card numbers, etc)?</span></span>
* <span data-ttu-id="83ef0-133">L'azienda necessita tooencrypt tutti i documenti o contenuto condiviso con i partner commerciali esterni?</span><span class="sxs-lookup"><span data-stu-id="83ef0-133">Does your company need tooencrypt all documents/contents shared with external business partners?</span></span>
* <span data-ttu-id="83ef0-134">L'azienda necessita di criteri aziendali di tooenforce su determinati tipi di messaggi di posta elettronica (non Rispondi a tutti, non inoltrare)?</span><span class="sxs-lookup"><span data-stu-id="83ef0-134">Does your company need tooenforce corporate policies on certain kinds of emails (do no reply all, do not forward)?</span></span>

> [!NOTE]
> <span data-ttu-id="83ef0-135">Annotare i tootake che ogni risposta e comprendere motivazioni hello delle risposte hello.</span><span class="sxs-lookup"><span data-stu-id="83ef0-135">Make sure tootake notes of each answer and understand hello rationale behind hello answer.</span></span> <span data-ttu-id="83ef0-136">[Definire la strategia di protezione dati](active-directory-hybrid-identity-design-considerations-data-protection-strategy.md) esaminerà le opzioni di hello disponibili e i vantaggi e svantaggi di ogni opzione.</span><span class="sxs-lookup"><span data-stu-id="83ef0-136">[Define Data Protection Strategy](active-directory-hybrid-identity-design-considerations-data-protection-strategy.md) will go over hello options available and advantages/disadvantages of each option.</span></span>  <span data-ttu-id="83ef0-137">Una volta fornite le risposte a queste domande, sarà possibile selezionare l'opzione più adatta in base alle esigenze aziendali.</span><span class="sxs-lookup"><span data-stu-id="83ef0-137">By having answered those questions you will select which option best suits your business needs.</span></span>
> 
> 

## <a name="next-steps"></a><span data-ttu-id="83ef0-138">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="83ef0-138">Next steps</span></span>
[<span data-ttu-id="83ef0-139">Determinare i requisiti di controllo di accesso</span><span class="sxs-lookup"><span data-stu-id="83ef0-139">Determine access control requirements</span></span>](active-directory-hybrid-identity-design-considerations-accesscontrol-requirements.md)

## <a name="see-also"></a><span data-ttu-id="83ef0-140">Vedere anche</span><span class="sxs-lookup"><span data-stu-id="83ef0-140">See Also</span></span>
[<span data-ttu-id="83ef0-141">Panoramica delle considerazioni di progettazione</span><span class="sxs-lookup"><span data-stu-id="83ef0-141">Design considerations overview</span></span>](active-directory-hybrid-identity-design-considerations-overview.md)


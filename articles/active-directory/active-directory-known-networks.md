---
title: Reti aaaKnown nel portale di Azure classico hello | Documenti Microsoft
description: "Quando si configurano reti note, è possibile evitare gli indirizzi IP che sono di proprietà dell'organizzazione incluso in hello accessi da più aree geografiche e accessi da indirizzi IP con attività sospetta report."
services: active-directory
documentationcenter: 
author: MarkusVi
manager: femila
editor: 
ms.assetid: f56e042a-78d5-4ea3-be33-94004f2a0fc3
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/05/2017
ms.author: markvi
ms.openlocfilehash: ec636cdda172cd3baeb1e606dd8d6e1949fbc63b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="known-networks"></a><span data-ttu-id="a9e66-103">Reti note</span><span class="sxs-lookup"><span data-stu-id="a9e66-103">Known networks</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="a9e66-104">Portale di Azure classico</span><span class="sxs-lookup"><span data-stu-id="a9e66-104">Azure classic portal</span></span>](active-directory-known-networks.md)
> * [<span data-ttu-id="a9e66-105">Portale di Azure</span><span class="sxs-lookup"><span data-stu-id="a9e66-105">Azure portal</span></span>](active-directory-known-networks-azure-portal.md)
> 
> 


<span data-ttu-id="a9e66-106">È possibile utilizzare l'accesso di Azure Active Directory e utilizzo report toogain visibilità hello integrità e sicurezza della directory dell'organizzazione.</span><span class="sxs-lookup"><span data-stu-id="a9e66-106">You can use Azure Active Directory's access and usage reports toogain visibility into hello integrity and security of your organization’s directory.</span></span> <span data-ttu-id="a9e66-107">Con queste informazioni, un amministratore di directory possa meglio stabilire l'origine di possibili rischi per la sicurezza in modo da poter adeguatamente pianificare toomitigate tali rischi.</span><span class="sxs-lookup"><span data-stu-id="a9e66-107">With this information, a directory admin can better determine where possible security risks may lie so that they can adequately plan toomitigate those risks.</span></span>

<span data-ttu-id="a9e66-108">È possibile che hello "*accessi da più aree geografiche*"e"*accessi da indirizzi IP con attività sospetta*" report flag in modo errato gli indirizzi IP che sono effettivamente di proprietà del organizzazione.</span><span class="sxs-lookup"><span data-stu-id="a9e66-108">It is possible that hello “*Sign ins from multiple geographies*” and “*Sign ins from IP addresses with suspicious activity*” reports incorrectly flag IP addresses that are actually owned by your organization.</span></span> 

<span data-ttu-id="a9e66-109">Questo può avvenire, ad esempio, nei casi seguenti:</span><span class="sxs-lookup"><span data-stu-id="a9e66-109">This can, for example, happen when:</span></span> 

* <span data-ttu-id="a9e66-110">Un utente nel proprio ufficio Boston ha effettuato l'accesso in modalità remota tooyour centro dati San Francisco trigger hello report "Accessi da più aree geografiche"</span><span class="sxs-lookup"><span data-stu-id="a9e66-110">A user in your Boston office has signed in remotely tooyour data center in San Francisco triggers hello “Sign ins from multiple geographies” report</span></span> 
* <span data-ttu-id="a9e66-111">Un utente dell'organizzazione tenta toosign su più volte con un hello trigger password non corretta per il report "Accessi da indirizzi IP con attività sospetta"</span><span class="sxs-lookup"><span data-stu-id="a9e66-111">A user of your organization tries toosign-on several times with an incorrect password triggers hello “Sign ins from IP addresses with suspicious activity” report</span></span> 

<span data-ttu-id="a9e66-112">tooprevent questi casi protezione fuorviante la generazione del report, è consigliabile aggiungere note intervalli toohello elenco di indirizzi IP dell'indirizzo IP pubblico dell'organizzazione.</span><span class="sxs-lookup"><span data-stu-id="a9e66-112">tooprevent these cases from generating misleading security reports, you should add known IP address ranges toohello list of your organization's public IP address.</span></span>    

### <a name="tooadd-your-organizations-public-ip-address-ranges-perform-hello-following-steps"></a><span data-ttu-id="a9e66-113">gli intervalli di tooadd indirizzo IP pubblico dell'organizzazione, eseguire hello alla procedura seguente:</span><span class="sxs-lookup"><span data-stu-id="a9e66-113">tooadd your organization’s public IP address ranges, perform hello following steps:</span></span>

1. <span data-ttu-id="a9e66-114">Sign-on toohello [portale di gestione di Azure](https://manage.windowsazure.com).</span><span class="sxs-lookup"><span data-stu-id="a9e66-114">Sign-on toohello [Azure management portal](https://manage.windowsazure.com).</span></span>

2. <span data-ttu-id="a9e66-115">Nel riquadro di sinistra hello, fare clic su **Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="a9e66-115">In hello left pane, click **Active Directory**.</span></span> 

    ![Reti note](./media/active-directory-known-networks/known-netwoks-01.png)

3. <span data-ttu-id="a9e66-117">In hello **Directory** scheda, selezionare la directory.</span><span class="sxs-lookup"><span data-stu-id="a9e66-117">In hello **Directory** tab, select your directory.</span></span>

4. <span data-ttu-id="a9e66-118">Scegliere dal menu hello in primo piano hello **configura**.</span><span class="sxs-lookup"><span data-stu-id="a9e66-118">In hello menu on hello top, click **Configure**.</span></span> 

    ![Reti note](./media/active-directory-known-networks/known-netwoks-02.png)

5. <span data-ttu-id="a9e66-120">Nella scheda Configura hello, andare troppo**gli intervalli di indirizzi IP pubblici organizzazioni**</span><span class="sxs-lookup"><span data-stu-id="a9e66-120">On hello Configure tab, go too**your organizations public IP address ranges**</span></span> 

    ![Reti note](./media/active-directory-known-networks/known-netwoks-03.png)

6. <span data-ttu-id="a9e66-122">Fare clic su **Aggiungi intervalli di indirizzi IP noti**.</span><span class="sxs-lookup"><span data-stu-id="a9e66-122">Click **Add Known IP Address Ranges**.</span></span>

7. <span data-ttu-id="a9e66-123">Aggiungere gli intervalli di indirizzi nella finestra di dialogo hello visualizzata e quindi fare clic su pulsante di controllo hello al termine.</span><span class="sxs-lookup"><span data-stu-id="a9e66-123">Add your address ranges in hello dialog box that appears, and then click hello check button  when you are done.</span></span> 

    ![Reti note](./media/active-directory-known-networks/known-netwoks-04.png)

<span data-ttu-id="a9e66-125">**Risorse aggiuntive:**</span><span class="sxs-lookup"><span data-stu-id="a9e66-125">**Additional resources:**</span></span>

* [<span data-ttu-id="a9e66-126">Visualizzare i report di accesso e utilizzo</span><span class="sxs-lookup"><span data-stu-id="a9e66-126">View your access and usage reports</span></span>](active-directory-view-access-usage-reports.md)
* [<span data-ttu-id="a9e66-127">Accessi da indirizzi IP con attività sospetta</span><span class="sxs-lookup"><span data-stu-id="a9e66-127">Sign ins from IP addresses with suspicious activity</span></span>](active-directory-reporting-sign-ins-from-ip-addresses-with-suspicious-activity.md)
* [<span data-ttu-id="a9e66-128">Accessi da più aree geografiche</span><span class="sxs-lookup"><span data-stu-id="a9e66-128">Sign ins from multiple geographies</span></span>](active-directory-reporting-sign-ins-from-multiple-geographies.md)


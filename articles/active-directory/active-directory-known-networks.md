---
title: Reti note nel portale di Azure classico | Documentazione Microsoft
description: "Configurando le reti note si evita che indirizzi IP di proprietà dell'organizzazione vengano inclusi nei report Accessi da più aree geografiche e Accessi da indirizzi IP con attività sospetta."
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
ms.openlocfilehash: e4d51d1d2f09fca34d749879e21d49f785eac35c
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="known-networks"></a><span data-ttu-id="c4617-103">Reti note</span><span class="sxs-lookup"><span data-stu-id="c4617-103">Known networks</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="c4617-104">Portale di Azure classico</span><span class="sxs-lookup"><span data-stu-id="c4617-104">Azure classic portal</span></span>](active-directory-known-networks.md)
> * [<span data-ttu-id="c4617-105">Portale di Azure</span><span class="sxs-lookup"><span data-stu-id="c4617-105">Azure portal</span></span>](active-directory-known-networks-azure-portal.md)
> 
> 


<span data-ttu-id="c4617-106">È possibile usare i report di utilizzo e accesso di Azure Active Directory per ottenere informazioni sull'integrità e sicurezza della directory dell'organizzazione.</span><span class="sxs-lookup"><span data-stu-id="c4617-106">You can use Azure Active Directory's access and usage reports to gain visibility into the integrity and security of your organization’s directory.</span></span> <span data-ttu-id="c4617-107">Con queste informazioni un amministratore di directory può stabilire meglio dove potrebbero esserci possibili rischi per la sicurezza in modo da poterne pianificare adeguatamente la riduzione.</span><span class="sxs-lookup"><span data-stu-id="c4617-107">With this information, a directory admin can better determine where possible security risks may lie so that they can adequately plan to mitigate those risks.</span></span>

<span data-ttu-id="c4617-108">È possibile che i report "*Accessi da più aree geografiche*" e "*Accessi da indirizzi IP con attività sospetta*" indichino erroneamente indirizzi IP che sono effettivamente di proprietà dell'organizzazione.</span><span class="sxs-lookup"><span data-stu-id="c4617-108">It is possible that the “*Sign ins from multiple geographies*” and “*Sign ins from IP addresses with suspicious activity*” reports incorrectly flag IP addresses that are actually owned by your organization.</span></span> 

<span data-ttu-id="c4617-109">Questo può avvenire, ad esempio, nei casi seguenti:</span><span class="sxs-lookup"><span data-stu-id="c4617-109">This can, for example, happen when:</span></span> 

* <span data-ttu-id="c4617-110">L'accesso di un utente dell'ufficio di Boston in modalità remota al data center di San Francisco attiva il report "Accessi da più aree geografiche"</span><span class="sxs-lookup"><span data-stu-id="c4617-110">A user in your Boston office has signed in remotely to your data center in San Francisco triggers the “Sign ins from multiple geographies” report</span></span> 
* <span data-ttu-id="c4617-111">Un utente dell'organizzazione tenta di accedere più volte con una password non corretta, attivando il report "Accessi da indirizzi IP con attività sospetta"</span><span class="sxs-lookup"><span data-stu-id="c4617-111">A user of your organization tries to sign-on several times with an incorrect password triggers the “Sign ins from IP addresses with suspicious activity” report</span></span> 

<span data-ttu-id="c4617-112">Per impedire che casi come questi generino report sulla sicurezza fuorvianti, è necessario aggiungere gli intervalli di indirizzi IP noti all'elenco di indirizzi IP pubblici dell'organizzazione.</span><span class="sxs-lookup"><span data-stu-id="c4617-112">To prevent these cases from generating misleading security reports, you should add known IP address ranges to the list of your organization's public IP address.</span></span>    

### <a name="to-add-your-organizations-public-ip-address-ranges-perform-the-following-steps"></a><span data-ttu-id="c4617-113">Per aggiungere gli intervalli di indirizzi IP pubblici dell'organizzazione, seguire questa procedura:</span><span class="sxs-lookup"><span data-stu-id="c4617-113">To add your organization’s public IP address ranges, perform the following steps:</span></span>

1. <span data-ttu-id="c4617-114">Accedere al [portale di gestione di Azure](https://manage.windowsazure.com).</span><span class="sxs-lookup"><span data-stu-id="c4617-114">Sign-on to the [Azure management portal](https://manage.windowsazure.com).</span></span>

2. <span data-ttu-id="c4617-115">Nel riquadro di sinistra fare clic su **Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="c4617-115">In the left pane, click **Active Directory**.</span></span> 

    ![Reti note](./media/active-directory-known-networks/known-netwoks-01.png)

3. <span data-ttu-id="c4617-117">Selezionare la propria directory nella scheda **Directory** .</span><span class="sxs-lookup"><span data-stu-id="c4617-117">In the **Directory** tab, select your directory.</span></span>

4. <span data-ttu-id="c4617-118">Nel menu in alto fare clic su **Configura**.</span><span class="sxs-lookup"><span data-stu-id="c4617-118">In the menu on the top, click **Configure**.</span></span> 

    ![Reti note](./media/active-directory-known-networks/known-netwoks-02.png)

5. <span data-ttu-id="c4617-120">Nella scheda Configura passare agli **intervalli di indirizzi IP pubblici dell'organizzazione**</span><span class="sxs-lookup"><span data-stu-id="c4617-120">On the Configure tab, go to **your organizations public IP address ranges**</span></span> 

    ![Reti note](./media/active-directory-known-networks/known-netwoks-03.png)

6. <span data-ttu-id="c4617-122">Fare clic su **Aggiungi intervalli di indirizzi IP noti**.</span><span class="sxs-lookup"><span data-stu-id="c4617-122">Click **Add Known IP Address Ranges**.</span></span>

7. <span data-ttu-id="c4617-123">Aggiungere gli intervalli di indirizzi nella finestra di dialogo visualizzata e quindi fare clic sul segno di spunta al termine dell'operazione.</span><span class="sxs-lookup"><span data-stu-id="c4617-123">Add your address ranges in the dialog box that appears, and then click the check button  when you are done.</span></span> 

    ![Reti note](./media/active-directory-known-networks/known-netwoks-04.png)

<span data-ttu-id="c4617-125">**Risorse aggiuntive:**</span><span class="sxs-lookup"><span data-stu-id="c4617-125">**Additional resources:**</span></span>

* [<span data-ttu-id="c4617-126">Visualizzare i report di accesso e utilizzo</span><span class="sxs-lookup"><span data-stu-id="c4617-126">View your access and usage reports</span></span>](active-directory-view-access-usage-reports.md)
* [<span data-ttu-id="c4617-127">Accessi da indirizzi IP con attività sospetta</span><span class="sxs-lookup"><span data-stu-id="c4617-127">Sign ins from IP addresses with suspicious activity</span></span>](active-directory-reporting-sign-ins-from-ip-addresses-with-suspicious-activity.md)
* [<span data-ttu-id="c4617-128">Accessi da più aree geografiche</span><span class="sxs-lookup"><span data-stu-id="c4617-128">Sign ins from multiple geographies</span></span>](active-directory-reporting-sign-ins-from-multiple-geographies.md)


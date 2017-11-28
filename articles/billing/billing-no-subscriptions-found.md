---
title: le sottoscrizioni aaaNo errore quando tenta toosign nel portale di tooAzure o centro account Azure | Documenti Microsoft
description: Fornisce una soluzione di hello per un problema in cui le sottoscrizioni non rilevato l'errore si verifica quando accede al portale tooAzure o centro account Azure.
services: 
documentationcenter: 
author: genlin
manager: jlian
editor: 
tags: billing
ms.assetid: d1545298-99db-4941-8e97-f24a06bb7cb6
ms.service: billing
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/21/2017
ms.author: genli
ms.openlocfilehash: def4d4a1f883dd948fe8132f2d85abc4c23ae624
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="no-subscriptions-found-error-in-azure-portal-or-azure-account-center"></a><span data-ttu-id="68ef2-103">Errore Non sono state trovate sottoscrizioni nel portale di Azure o nel Centro account di Azure</span><span class="sxs-lookup"><span data-stu-id="68ef2-103">No subscriptions found error in Azure portal or Azure account center</span></span>
<span data-ttu-id="68ef2-104">Si potrebbe ricevere un messaggio di errore "Non è stata trovata alcuna sottoscrizione" quando si tenta di toosign in toohello [portale di Azure](https://portal.azure.com/) o hello [centro account Azure](https://account.windowsazure.com/Subscriptions).</span><span class="sxs-lookup"><span data-stu-id="68ef2-104">You might receive a "No subscriptions found" error message when you try toosign in toohello [Azure portal](https://portal.azure.com/) or hello [Azure account center](https://account.windowsazure.com/Subscriptions).</span></span> <span data-ttu-id="68ef2-105">Questo articolo offre una soluzione al problema.</span><span class="sxs-lookup"><span data-stu-id="68ef2-105">This article provides a solution for this problem.</span></span>

## <a name="symptom"></a><span data-ttu-id="68ef2-106">Sintomo</span><span class="sxs-lookup"><span data-stu-id="68ef2-106">Symptom</span></span>

<span data-ttu-id="68ef2-107">Quando si tenta di toosign in toohello [portale di Azure](https://portal.azure.com/) o hello [centro account Azure](https://account.windowsazure.com/Subscriptions), viene visualizzato hello seguente messaggio di errore: "Non è stata trovata alcuna sottoscrizione".</span><span class="sxs-lookup"><span data-stu-id="68ef2-107">When you try toosign in toohello [Azure portal](https://portal.azure.com/) or hello [Azure account center](https://account.windowsazure.com/Subscriptions), you receive hello following error message: "No subscriptions found".</span></span>

## <a name="cause"></a><span data-ttu-id="68ef2-108">Causa</span><span class="sxs-lookup"><span data-stu-id="68ef2-108">Cause</span></span>

<span data-ttu-id="68ef2-109">Questo problema si verifica se l'account non ha autorizzazioni sufficienti.</span><span class="sxs-lookup"><span data-stu-id="68ef2-109">This problem occurs if your account doesn’t have sufficient permissions.</span></span> 

## <a name="solution"></a><span data-ttu-id="68ef2-110">Soluzione</span><span class="sxs-lookup"><span data-stu-id="68ef2-110">Solution</span></span>

<span data-ttu-id="68ef2-111">Assicurarsi di accedere come amministratore di hello corretto.</span><span class="sxs-lookup"><span data-stu-id="68ef2-111">Make sure that you log in as hello correct administrator.</span></span> <span data-ttu-id="68ef2-112">Un amministratore di Account può accedere solo hello Account Center.</span><span class="sxs-lookup"><span data-stu-id="68ef2-112">An Account Administrator can access only hello Account Center.</span></span> <span data-ttu-id="68ef2-113">Gli amministratori del servizio (SA) e coamministratore (CA) hanno toohello solo dell'autorizzazione di accesso portale di Azure o hello portale di Azure classico.</span><span class="sxs-lookup"><span data-stu-id="68ef2-113">Service Administrators (SA) and Co-Administrators (CA) have access permission only toohello Azure portal or hello Azure classic portal.</span></span>

### <a name="scenario-1-error-message-is-received-in-hello-azure-portalhttpsportalazurecom"></a><span data-ttu-id="68ef2-114">Scenario 1: Messaggio di errore viene generato in hello [portale di Azure](https://portal.azure.com)</span><span class="sxs-lookup"><span data-stu-id="68ef2-114">Scenario 1: Error message is received in hello [Azure portal](https://portal.azure.com)</span></span>

<span data-ttu-id="68ef2-115">toofix questo problema:</span><span class="sxs-lookup"><span data-stu-id="68ef2-115">toofix this issue:</span></span>

* <span data-ttu-id="68ef2-116">Verificare che tale hello directory Azure è selezionata, fare clic su account in alto a destra hello corretto.</span><span class="sxs-lookup"><span data-stu-id="68ef2-116">Make sure that hello correct Azure directory is selected by clicking your account at hello top right.</span></span>

  ![Directory selezionare hello hello in alto a destra di hello portale di Azure](./media/billing-no-subscriptions-found/directory-switch.png)

* <span data-ttu-id="68ef2-118">Se hello Azure right directory è selezionata, ma viene visualizzato il messaggio di errore hello, [l'account aggiunto come proprietario](billing-add-change-azure-subscription-administrator.md).</span><span class="sxs-lookup"><span data-stu-id="68ef2-118">If hello right Azure directory is selected but you still receive hello error message, [have your account added as an Owner](billing-add-change-azure-subscription-administrator.md).</span></span>

### <a name="scenario-2-error-message-is-received-in-hello-azure-account-centerhttpsaccountwindowsazurecomsubscriptions"></a><span data-ttu-id="68ef2-119">Scenario 2: Messaggio di errore viene generato in hello [centro account Azure](https://account.windowsazure.com/Subscriptions)</span><span class="sxs-lookup"><span data-stu-id="68ef2-119">Scenario 2: Error message is received in hello [Azure account center](https://account.windowsazure.com/Subscriptions)</span></span>

<span data-ttu-id="68ef2-120">Controllare se l'account hello utilizzato è hello amministratore dell'Account.</span><span class="sxs-lookup"><span data-stu-id="68ef2-120">Check whether hello account that you used is hello Account Administrator.</span></span> <span data-ttu-id="68ef2-121">tooverify che hello amministratore dell'Account, eseguire la procedura seguente:</span><span class="sxs-lookup"><span data-stu-id="68ef2-121">tooverify who hello Account Administrator is, follow these steps:</span></span>

1. <span data-ttu-id="68ef2-122">Accedi toohello [portale di Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="68ef2-122">Sign in toohello [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="68ef2-123">Nel menu Hub hello, selezionare **sottoscrizione**.</span><span class="sxs-lookup"><span data-stu-id="68ef2-123">On hello Hub menu, select **Subscription**.</span></span>
3. <span data-ttu-id="68ef2-124">Selezionare hello sottoscrizione che desidera toocheck e quindi selezionare **impostazioni**.</span><span class="sxs-lookup"><span data-stu-id="68ef2-124">Select hello subscription that you want toocheck, and then select **Settings**.</span></span>
4. <span data-ttu-id="68ef2-125">Selezionare **Proprietà**.</span><span class="sxs-lookup"><span data-stu-id="68ef2-125">Select **Properties**.</span></span> <span data-ttu-id="68ef2-126">amministratore dell'account di sottoscrizione hello Hello viene visualizzato in hello **amministratore dell'Account** casella.</span><span class="sxs-lookup"><span data-stu-id="68ef2-126">hello account administrator of hello subscription is displayed in hello **Account Admin** box.</span></span>

## <a name="need-help-contact-support"></a><span data-ttu-id="68ef2-127">Richiesta di assistenza</span><span class="sxs-lookup"><span data-stu-id="68ef2-127">Need help?</span></span> <span data-ttu-id="68ef2-128">Contattare il supporto tecnico.</span><span class="sxs-lookup"><span data-stu-id="68ef2-128">Contact support.</span></span>
<span data-ttu-id="68ef2-129">Se è ancora necessario della Guida, [contattare il supporto tecnico](http://go.microsoft.com/fwlink/?linkid=544831&clcid=0x409) tooget risolta il problema.</span><span class="sxs-lookup"><span data-stu-id="68ef2-129">If you still need help, [contact support](http://go.microsoft.com/fwlink/?linkid=544831&clcid=0x409) tooget your issue resolved quickly.</span></span> 

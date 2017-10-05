---
title: Errore Non sono state trovate sottoscrizioni quando si prova ad accedere al portale di Azure o al Centro account di Azure | Microsoft Docs
description: Fornisce la soluzione al problema per cui si verifica l'errore Non sono state trovate sottoscrizioni quando si accede al portale di Azure o al Centro account di Azure.
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
ms.openlocfilehash: a4ce9b219c05f8469379c2aac5241fcfffd16033
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/29/2017
---
# <a name="no-subscriptions-found-error-in-azure-portal-or-azure-account-center"></a><span data-ttu-id="0212e-103">Errore Non sono state trovate sottoscrizioni nel portale di Azure o nel Centro account di Azure</span><span class="sxs-lookup"><span data-stu-id="0212e-103">No subscriptions found error in Azure portal or Azure account center</span></span>
<span data-ttu-id="0212e-104">È possibile che venga visualizzato il messaggio di errore "Non sono state trovate sottoscrizioni" quando si prova ad accedere al [portale di Azure](https://portal.azure.com/) o al [Centro account di Azure](https://account.windowsazure.com/Subscriptions).</span><span class="sxs-lookup"><span data-stu-id="0212e-104">You might receive a "No subscriptions found" error message when you try to sign in to the [Azure portal](https://portal.azure.com/) or the [Azure account center](https://account.windowsazure.com/Subscriptions).</span></span> <span data-ttu-id="0212e-105">Questo articolo offre una soluzione al problema.</span><span class="sxs-lookup"><span data-stu-id="0212e-105">This article provides a solution for this problem.</span></span>

## <a name="symptom"></a><span data-ttu-id="0212e-106">Sintomo</span><span class="sxs-lookup"><span data-stu-id="0212e-106">Symptom</span></span>

<span data-ttu-id="0212e-107">Quando si prova ad accedere al [portale di Azure](https://portal.azure.com/) o al [Centro account di Azure](https://account.windowsazure.com/Subscriptions), viene visualizzato il messaggio di errore seguente: "Non sono state trovate sottoscrizioni".</span><span class="sxs-lookup"><span data-stu-id="0212e-107">When you try to sign in to the [Azure portal](https://portal.azure.com/) or the [Azure account center](https://account.windowsazure.com/Subscriptions), you receive the following error message: "No subscriptions found".</span></span>

## <a name="cause"></a><span data-ttu-id="0212e-108">Causa</span><span class="sxs-lookup"><span data-stu-id="0212e-108">Cause</span></span>

<span data-ttu-id="0212e-109">Questo problema si verifica se l'account non ha autorizzazioni sufficienti.</span><span class="sxs-lookup"><span data-stu-id="0212e-109">This problem occurs if your account doesn’t have sufficient permissions.</span></span> 

## <a name="solution"></a><span data-ttu-id="0212e-110">Soluzione</span><span class="sxs-lookup"><span data-stu-id="0212e-110">Solution</span></span>

<span data-ttu-id="0212e-111">Assicurarsi di accedere con l'account amministratore corretto.</span><span class="sxs-lookup"><span data-stu-id="0212e-111">Make sure that you log in as the correct administrator.</span></span> <span data-ttu-id="0212e-112">Un amministratore account può accedere solo al Centro account.</span><span class="sxs-lookup"><span data-stu-id="0212e-112">An Account Administrator can access only the Account Center.</span></span> <span data-ttu-id="0212e-113">Gli amministratori del servizio e i co-amministratori hanno l'autorizzazione di accesso solo per il portale di Azure o il portale di Azure classico.</span><span class="sxs-lookup"><span data-stu-id="0212e-113">Service Administrators (SA) and Co-Administrators (CA) have access permission only to the Azure portal or the Azure classic portal.</span></span>

### <a name="scenario-1-error-message-is-received-in-the-azure-portalhttpsportalazurecom"></a><span data-ttu-id="0212e-114">Scenario 1: Il messaggio di errore viene visualizzato nel [portale di Azure](https://portal.azure.com)</span><span class="sxs-lookup"><span data-stu-id="0212e-114">Scenario 1: Error message is received in the [Azure portal](https://portal.azure.com)</span></span>

<span data-ttu-id="0212e-115">Per risolvere il problema:</span><span class="sxs-lookup"><span data-stu-id="0212e-115">To fix this issue:</span></span>

* <span data-ttu-id="0212e-116">Verificare che sia selezionata la directory di Azure corretta facendo clic sull'account in alto a destra.</span><span class="sxs-lookup"><span data-stu-id="0212e-116">Make sure that the correct Azure directory is selected by clicking your account at the top right.</span></span>

  ![Selezionare la directory in alto a destra nel portale di Azure](./media/billing-no-subscriptions-found/directory-switch.png)

* <span data-ttu-id="0212e-118">Se è selezionata la directory di Azure corretta, ma viene comunque visualizzato il messaggio di errore, [richiedere che il proprio account venga aggiunto come proprietario](billing-add-change-azure-subscription-administrator.md).</span><span class="sxs-lookup"><span data-stu-id="0212e-118">If the right Azure directory is selected but you still receive the error message, [have your account added as an Owner](billing-add-change-azure-subscription-administrator.md).</span></span>

### <a name="scenario-2-error-message-is-received-in-the-azure-account-centerhttpsaccountwindowsazurecomsubscriptions"></a><span data-ttu-id="0212e-119">Scenario 2: Il messaggio di errore viene visualizzato nel [Centro account di Azure](https://account.windowsazure.com/Subscriptions)</span><span class="sxs-lookup"><span data-stu-id="0212e-119">Scenario 2: Error message is received in the [Azure account center](https://account.windowsazure.com/Subscriptions)</span></span>

<span data-ttu-id="0212e-120">Controllare se l'account usato è l'amministratore account.</span><span class="sxs-lookup"><span data-stu-id="0212e-120">Check whether the account that you used is the Account Administrator.</span></span> <span data-ttu-id="0212e-121">Per verificare chi è l'amministratore account, seguire questa procedura:</span><span class="sxs-lookup"><span data-stu-id="0212e-121">To verify who the Account Administrator is, follow these steps:</span></span>

1. <span data-ttu-id="0212e-122">Accedere al [portale di Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="0212e-122">Sign in to the [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="0212e-123">Nel menu Hub, selezionare **Sottoscrizione**.</span><span class="sxs-lookup"><span data-stu-id="0212e-123">On the Hub menu, select **Subscription**.</span></span>
3. <span data-ttu-id="0212e-124">Scegliere la sottoscrizione da controllare, quindi selezionare **Impostazioni**.</span><span class="sxs-lookup"><span data-stu-id="0212e-124">Select the subscription that you want to check, and then select **Settings**.</span></span>
4. <span data-ttu-id="0212e-125">Selezionare **Proprietà**.</span><span class="sxs-lookup"><span data-stu-id="0212e-125">Select **Properties**.</span></span> <span data-ttu-id="0212e-126">L'amministratore account della sottoscrizione viene visualizzato nella casella **Amministratore account** .</span><span class="sxs-lookup"><span data-stu-id="0212e-126">The account administrator of the subscription is displayed in the **Account Admin** box.</span></span>

## <a name="need-help-contact-support"></a><span data-ttu-id="0212e-127">Richiesta di assistenza</span><span class="sxs-lookup"><span data-stu-id="0212e-127">Need help?</span></span> <span data-ttu-id="0212e-128">Contattare il supporto tecnico.</span><span class="sxs-lookup"><span data-stu-id="0212e-128">Contact support.</span></span>
<span data-ttu-id="0212e-129">Se si necessita ancora di assistenza, [contattare il supporto tecnico](http://go.microsoft.com/fwlink/?linkid=544831&clcid=0x409) per ottenere una rapida risoluzione del problema.</span><span class="sxs-lookup"><span data-stu-id="0212e-129">If you still need help, [contact support](http://go.microsoft.com/fwlink/?linkid=544831&clcid=0x409) to get your issue resolved quickly.</span></span> 

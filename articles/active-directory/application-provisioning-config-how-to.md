---
title: Come configurare il provisioning degli utenti in un'applicazione della raccolta di Azure AD | Microsoft Docs
description: "Come configurare rapidamente il provisioning e il deprovisioning degli account utente per applicazioni già elencate nella raccolta di applicazioni AD Azure"
services: active-directory
documentationcenter: 
author: ajamess
manager: femila
ms.assetid: 
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/11/2017
ms.author: asteen
ms.openlocfilehash: 2e38fcb30ea7632339a3ba8815a536872cfcc69e
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/03/2017
---
# <a name="how-to-configure-user-provisioning-to-an-azure-ad-gallery-application"></a><span data-ttu-id="5b6c6-103">Come configurare il provisioning degli utenti in un'applicazione della raccolta di Azure AD</span><span class="sxs-lookup"><span data-stu-id="5b6c6-103">How to configure user provisioning to an Azure AD Gallery application</span></span>

<span data-ttu-id="5b6c6-104">Il *provisioning degli account utente* è l'atto di creazione, aggiornamento e/o la disabilitazione di record di account utente nell'archivio di profili utente locale di un'applicazione.</span><span class="sxs-lookup"><span data-stu-id="5b6c6-104">*User account provisioning* is the act of creating, updating, and/or disabling user account records in an application’s local user profile store.</span></span> <span data-ttu-id="5b6c6-105">La maggior parte delle applicazioni cloud e SaaS archiviano i ruoli e le autorizzazioni utente in un proprio archivio di profili utente locale e la presenza di tali record utente nell'archivio locale è *necessaria* per il funzionamento degli accessi e del Single Sign-on.</span><span class="sxs-lookup"><span data-stu-id="5b6c6-105">Most cloud and SaaS applications store the users role and permissions in their own local user profile store, and presence of such a user record in their local store is *required* for single sign-on and access to work.</span></span>

<span data-ttu-id="5b6c6-106">Nel portale di Azure, la scheda **Provisioning** nel riquadro di spostamento a sinistra di un'applicazione Enterprise mostra le modalità di provisioning supportate per l'applicazione.</span><span class="sxs-lookup"><span data-stu-id="5b6c6-106">In the Azure portal, the **Provisioning** tab in the left navigation pane for an Enterprise App displays what provisioning modes are supported for that app.</span></span> <span data-ttu-id="5b6c6-107">Può essere uno dei due valori:</span><span class="sxs-lookup"><span data-stu-id="5b6c6-107">This can be one of two values:</span></span>

## <a name="configuring-an-application-for-manual-provisioning"></a><span data-ttu-id="5b6c6-108">Configurazione di un'applicazione per il Provisioning manuale</span><span class="sxs-lookup"><span data-stu-id="5b6c6-108">Configuring an application for Manual Provisioning</span></span>

<span data-ttu-id="5b6c6-109">Con il provisioning *manuale* gli account utente devono essere creati manualmente usando i metodi forniti dall'applicazione.</span><span class="sxs-lookup"><span data-stu-id="5b6c6-109">*Manual* provisioning means that user accounts must be created manually using the methods provided by that app.</span></span> <span data-ttu-id="5b6c6-110">Potrebbe essere necessario accedere a un portale amministrativo dell'applicazione e aggiungere gli utenti usando un'interfaccia utente basata sul Web.</span><span class="sxs-lookup"><span data-stu-id="5b6c6-110">This could mean logging into an administrative portal for that app and adding users using a web-based user interface.</span></span> <span data-ttu-id="5b6c6-111">Oppure caricare un foglio di calcolo con i dettagli degli account utente, usando un meccanismo fornito dall'applicazione.</span><span class="sxs-lookup"><span data-stu-id="5b6c6-111">Or it could be uploading a spreadsheet with user account detail, using a mechanism provided by that application.</span></span> <span data-ttu-id="5b6c6-112">Consultare la documentazione o contattare lo sviluppatore dell'applicazione per determinare i meccanismi disponibili.</span><span class="sxs-lookup"><span data-stu-id="5b6c6-112">Consult the documentation provided by the app, or contact the app developer to determine wat mechanisms are available.</span></span>

<span data-ttu-id="5b6c6-113">Se Manuale è l'unica modalità disponibile per una determinata applicazione, significa che non è stato creato alcun connettore di provisioning automatico AD Azure per l'applicazione.</span><span class="sxs-lookup"><span data-stu-id="5b6c6-113">If Manual is the only mode shown for a given application, it means that no automatic Azure AD provisioning connector has been created for the app yet.</span></span> <span data-ttu-id="5b6c6-114">O significa che l'applicazione non supporta l'API prerequisita di gestione degli utenti in base a cui creare un connettore di provisioning automatico.</span><span class="sxs-lookup"><span data-stu-id="5b6c6-114">Or it means the app does not support the pre-requisite user management API upon which to build an automated provisioning connector.</span></span>

<span data-ttu-id="5b6c6-115">Se si intende richiedere supporto per il provisioning automatico per una determinata applicazione, è possibile inviare una richiesta all'indirizzo <http://aka.ms/aadapprequest>.</span><span class="sxs-lookup"><span data-stu-id="5b6c6-115">If you would like to request support for automatic provisioning for a given app, you can fill out a request at <http://aka.ms/aadapprequest>.</span></span>

## <a name="configuring-an-application-for-automatic-provisioning"></a><span data-ttu-id="5b6c6-116">Configurazione di un'applicazione per il Provisioning automatico</span><span class="sxs-lookup"><span data-stu-id="5b6c6-116">Configuring an application for Automatic Provisioning</span></span>

<span data-ttu-id="5b6c6-117">*Automatico* significa che è stato sviluppato un connettore di provisioning Azure AD per l'applicazione.</span><span class="sxs-lookup"><span data-stu-id="5b6c6-117">*Automatic* means that an Azure AD provisioning connector has been developed for this application.</span></span> <span data-ttu-id="5b6c6-118">Per altre informazioni sul servizio di provisioning automatico e sul relativo funzionamento, vedere [Automatizzare il provisioning e il deprovisioning utenti in applicazioni SaaS con Azure Active Directory](https://docs.microsoft.com/azure/active-directory/active-directory-saas-app-provisioning).</span><span class="sxs-lookup"><span data-stu-id="5b6c6-118">For more information on the Azure AD provisioning service and how it works, see [Automate User Provisioning and Deprovisioning to SaaS Applications with Azure Active Directory](https://docs.microsoft.com/azure/active-directory/active-directory-saas-app-provisioning).</span></span>

<span data-ttu-id="5b6c6-119">Per altre informazioni su come eseguire il provisioning di utenti e gruppi specifici per un'app, vedere [Anteprima: gestione del provisioning degli account utenti per app aziendali nel nuovo portale di Azure](https://docs.microsoft.com/azure/active-directory/active-directory-enterprise-apps-manage-provisioning).</span><span class="sxs-lookup"><span data-stu-id="5b6c6-119">For more information on how to provision specific users and groups to an application, see [Managing user account provisioning for enterprise apps](https://docs.microsoft.com/azure/active-directory/active-directory-enterprise-apps-manage-provisioning).</span></span>

<span data-ttu-id="5b6c6-120">I passaggi necessari per abilitare e configurare il provisioning automatico variano a seconda dell'applicazione.</span><span class="sxs-lookup"><span data-stu-id="5b6c6-120">The actual steps required to enable and configure automatic provisioning vary depending on the application.</span></span>

>[!NOTE]
><span data-ttu-id="5b6c6-121">È consigliabile iniziare cercando l'esercitazione per la configurazione del provisioning per l'applicazione e seguire i passaggi per configurare l'applicazione e Azure AD per creare la connessione di provisioning.</span><span class="sxs-lookup"><span data-stu-id="5b6c6-121">You should start by finding the setup tutorial specific to setting up provisioning for your application, and following those steps to configure both the app and Azure AD to create the provisioning connection.</span></span> 
>
>

<span data-ttu-id="5b6c6-122">Le esercitazioni per le applicazioni si trovano nell'[Elenco di esercitazioni sulla procedura di integrazione delle applicazioni SaaS con Azure Active Directory](https://docs.microsoft.com/azure/active-directory/active-directory-saas-tutorial-list).</span><span class="sxs-lookup"><span data-stu-id="5b6c6-122">App tutorials can be found at [List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory](https://docs.microsoft.com/azure/active-directory/active-directory-saas-tutorial-list).</span></span>

<span data-ttu-id="5b6c6-123">Un aspetto importante da considerare quando si configura il provisioning è quello di esaminare e configurare il mapping degli attributi e i flussi di lavoro che definiscono il tipo di flusso di proprietà utente (o gruppo) da Azure AD all'applicazione.</span><span class="sxs-lookup"><span data-stu-id="5b6c6-123">An important thing to consider when setting up provisioning be to review and configure the attribute mappings and workflows that define which user (or group) properties flow from Azure AD to the application.</span></span> <span data-ttu-id="5b6c6-124">Rientra in questo ambito anche l'impostazione della "proprietà di abbinamento" che può essere usata per identificare e abbinare in modo univoco utenti/gruppi tra i due sistemi.</span><span class="sxs-lookup"><span data-stu-id="5b6c6-124">This includes setting the “matching property” that be used to uniquely identify and match users/groups between the two systems.</span></span> <span data-ttu-id="5b6c6-125">Per altre informazioni su questo processo importante.</span><span class="sxs-lookup"><span data-stu-id="5b6c6-125">For more information on this important process.</span></span>

## <a name="next-steps"></a><span data-ttu-id="5b6c6-126">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="5b6c6-126">Next steps</span></span>
[<span data-ttu-id="5b6c6-127">Personalizzazione dei mapping degli attributi del provisioning degli utenti per le applicazioni SaaS in Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="5b6c6-127">Customizing User Provisioning Attribute Mappings for SaaS Applications in Azure Active Directory</span></span>](https://docs.microsoft.com/azure/active-directory/active-directory-saas-customizing-attribute-mappings)


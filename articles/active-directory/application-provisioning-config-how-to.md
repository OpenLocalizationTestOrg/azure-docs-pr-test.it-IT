---
title: applicazione raccolta tooan AD Azure il provisioning degli utenti aaaHow tooconfigure | Documenti Microsoft
description: "Come è possibile configurare rapidamente account utente di provisioning e deprovisioning tooapplications già nella raccolta di Azure Active Directory dell'applicazione hello"
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
ms.openlocfilehash: 2c28e59a3ac8f221ed93b2f6b0b1221f7604af23
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooconfigure-user-provisioning-tooan-azure-ad-gallery-application"></a><span data-ttu-id="cfa94-103">Come utente tooconfigure provisioning applicazione raccolta tooan Azure AD</span><span class="sxs-lookup"><span data-stu-id="cfa94-103">How tooconfigure user provisioning tooan Azure AD Gallery application</span></span>

<span data-ttu-id="cfa94-104">*Provisioning dell'account utente* è hello atto della creazione, aggiornamento e/o la disabilitazione di record di account utente nell'archivio profili utente locale di un'applicazione.</span><span class="sxs-lookup"><span data-stu-id="cfa94-104">*User account provisioning* is hello act of creating, updating, and/or disabling user account records in an application’s local user profile store.</span></span> <span data-ttu-id="cfa94-105">La maggior parte dei cloud e le applicazioni SaaS archiviano hello utenti ruoli e le autorizzazioni in un proprio archivio di profilo utente locale e la presenza di tale record utente nell'archivio locale è *obbligatorio* per single sign-on e accesso di toowork.</span><span class="sxs-lookup"><span data-stu-id="cfa94-105">Most cloud and SaaS applications store hello users role and permissions in their own local user profile store, and presence of such a user record in their local store is *required* for single sign-on and access toowork.</span></span>

<span data-ttu-id="cfa94-106">Nel portale di Azure hello, hello **Provisioning** scheda nel riquadro di spostamento a sinistra di hello per un'applicazione aziendale vengono visualizzate le modalità di provisioning sono supportate per l'app.</span><span class="sxs-lookup"><span data-stu-id="cfa94-106">In hello Azure portal, hello **Provisioning** tab in hello left navigation pane for an Enterprise App displays what provisioning modes are supported for that app.</span></span> <span data-ttu-id="cfa94-107">Può essere uno dei due valori:</span><span class="sxs-lookup"><span data-stu-id="cfa94-107">This can be one of two values:</span></span>

## <a name="configuring-an-application-for-manual-provisioning"></a><span data-ttu-id="cfa94-108">Configurazione di un'applicazione per il Provisioning manuale</span><span class="sxs-lookup"><span data-stu-id="cfa94-108">Configuring an application for Manual Provisioning</span></span>

<span data-ttu-id="cfa94-109">*Manuale* provisioning significa che gli account utente devono essere creati manualmente utilizzando i metodi di hello forniti da tale app.</span><span class="sxs-lookup"><span data-stu-id="cfa94-109">*Manual* provisioning means that user accounts must be created manually using hello methods provided by that app.</span></span> <span data-ttu-id="cfa94-110">Potrebbe essere necessario accedere a un portale amministrativo dell'applicazione e aggiungere gli utenti usando un'interfaccia utente basata sul Web.</span><span class="sxs-lookup"><span data-stu-id="cfa94-110">This could mean logging into an administrative portal for that app and adding users using a web-based user interface.</span></span> <span data-ttu-id="cfa94-111">Oppure caricare un foglio di calcolo con i dettagli degli account utente, usando un meccanismo fornito dall'applicazione.</span><span class="sxs-lookup"><span data-stu-id="cfa94-111">Or it could be uploading a spreadsheet with user account detail, using a mechanism provided by that application.</span></span> <span data-ttu-id="cfa94-112">Consultare la documentazione di hello fornite da app hello, o contatto hello sono disponibili meccanismi di sviluppatore toodetermine wat.</span><span class="sxs-lookup"><span data-stu-id="cfa94-112">Consult hello documentation provided by hello app, or contact hello app developer toodetermine wat mechanisms are available.</span></span>

<span data-ttu-id="cfa94-113">Se manuale è in modalità solo hello visualizzato per una determinata applicazione, significa che non automatico AD Azure provisioning connettore è ancora stata creata per l'applicazione hello.</span><span class="sxs-lookup"><span data-stu-id="cfa94-113">If Manual is hello only mode shown for a given application, it means that no automatic Azure AD provisioning connector has been created for hello app yet.</span></span> <span data-ttu-id="cfa94-114">O significa app di hello non non supporto hello utente prerequisito API di gestione al quale toobuild un connettore di provisioning automatico.</span><span class="sxs-lookup"><span data-stu-id="cfa94-114">Or it means hello app does not support hello pre-requisite user management API upon which toobuild an automated provisioning connector.</span></span>

<span data-ttu-id="cfa94-115">Se si desidera supporto toorequest per il provisioning automatico per un'applicazione specificata, è possibile compilare una richiesta di <http://aka.ms/aadapprequest>.</span><span class="sxs-lookup"><span data-stu-id="cfa94-115">If you would like toorequest support for automatic provisioning for a given app, you can fill out a request at <http://aka.ms/aadapprequest>.</span></span>

## <a name="configuring-an-application-for-automatic-provisioning"></a><span data-ttu-id="cfa94-116">Configurazione di un'applicazione per il Provisioning automatico</span><span class="sxs-lookup"><span data-stu-id="cfa94-116">Configuring an application for Automatic Provisioning</span></span>

<span data-ttu-id="cfa94-117">*Automatico* significa che è stato sviluppato un connettore di provisioning Azure AD per l'applicazione.</span><span class="sxs-lookup"><span data-stu-id="cfa94-117">*Automatic* means that an Azure AD provisioning connector has been developed for this application.</span></span> <span data-ttu-id="cfa94-118">Per ulteriori informazioni su hello Azure AD, il provisioning di servizio e il relativo funzionamento, vedere [tooSaaS automatizzare Provisioning e Deprovisioning applicazioni con Azure Active Directory](https://docs.microsoft.com/azure/active-directory/active-directory-saas-app-provisioning).</span><span class="sxs-lookup"><span data-stu-id="cfa94-118">For more information on hello Azure AD provisioning service and how it works, see [Automate User Provisioning and Deprovisioning tooSaaS Applications with Azure Active Directory](https://docs.microsoft.com/azure/active-directory/active-directory-saas-app-provisioning).</span></span>

<span data-ttu-id="cfa94-119">Per ulteriori informazioni su utenti specifici tooprovision e l'applicazione di tooan gruppi, vedere [la gestione di provisioning dell'account utente per applicazioni aziendali](https://docs.microsoft.com/azure/active-directory/active-directory-enterprise-apps-manage-provisioning).</span><span class="sxs-lookup"><span data-stu-id="cfa94-119">For more information on how tooprovision specific users and groups tooan application, see [Managing user account provisioning for enterprise apps](https://docs.microsoft.com/azure/active-directory/active-directory-enterprise-apps-manage-provisioning).</span></span>

<span data-ttu-id="cfa94-120">Hello tooenable necessari passaggi effettivi e configurare il provisioning automatico variano a seconda dell'applicazione hello.</span><span class="sxs-lookup"><span data-stu-id="cfa94-120">hello actual steps required tooenable and configure automatic provisioning vary depending on hello application.</span></span>

>[!NOTE]
><span data-ttu-id="cfa94-121">È consigliabile iniziare dalla ricerca hello toosetting specifico dell'esercitazione di programma di installazione di provisioning per l'applicazione e seguenti tooconfigure tali passaggi app hello sia Azure AD toocreate hello connessione provisioning.</span><span class="sxs-lookup"><span data-stu-id="cfa94-121">You should start by finding hello setup tutorial specific toosetting up provisioning for your application, and following those steps tooconfigure both hello app and Azure AD toocreate hello provisioning connection.</span></span> 
>
>

<span data-ttu-id="cfa94-122">Esercitazioni di App sono reperibile in [elenco di esercitazioni sulla procedura tooIntegrate App SaaS con Azure Active Directory](https://docs.microsoft.com/azure/active-directory/active-directory-saas-tutorial-list).</span><span class="sxs-lookup"><span data-stu-id="cfa94-122">App tutorials can be found at [List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory](https://docs.microsoft.com/azure/active-directory/active-directory-saas-tutorial-list).</span></span>

<span data-ttu-id="cfa94-123">Tooconsider una cosa importante quando l'impostazione di provisioning essere tooreview e configurare i mapping degli attributi hello e flussi di lavoro che definiscono quale flusso di proprietà utente (o gruppo) dall'applicazione toohello Azure AD.</span><span class="sxs-lookup"><span data-stu-id="cfa94-123">An important thing tooconsider when setting up provisioning be tooreview and configure hello attribute mappings and workflows that define which user (or group) properties flow from Azure AD toohello application.</span></span> <span data-ttu-id="cfa94-124">Ciò include l'impostazione di hello "proprietà corrispondente" che toouniquely utilizzati da identificare e corrisponde agli utenti o i gruppi tra i sistemi di hello due.</span><span class="sxs-lookup"><span data-stu-id="cfa94-124">This includes setting hello “matching property” that be used toouniquely identify and match users/groups between hello two systems.</span></span> <span data-ttu-id="cfa94-125">Per altre informazioni su questo processo importante.</span><span class="sxs-lookup"><span data-stu-id="cfa94-125">For more information on this important process.</span></span>

## <a name="next-steps"></a><span data-ttu-id="cfa94-126">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="cfa94-126">Next steps</span></span>
[<span data-ttu-id="cfa94-127">Personalizzazione dei mapping degli attributi del provisioning degli utenti per le applicazioni SaaS in Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="cfa94-127">Customizing User Provisioning Attribute Mappings for SaaS Applications in Azure Active Directory</span></span>](https://docs.microsoft.com/azure/active-directory/active-directory-saas-customizing-attribute-mappings)


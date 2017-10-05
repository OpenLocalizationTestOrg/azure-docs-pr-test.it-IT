---
title: Problema nella configurazione dell'accesso Single Sign-On federato per un'applicazione non inclusa nella raccolta di Azure AD | Microsoft Docs
description: Informazioni sui problemi comuni che si possono incontrare durante la configurazione dell'accesso Single Sign-On federato per un'applicazione SAML personalizzata non inclusa nella raccolta delle applicazioni di Azure AD
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
ms.openlocfilehash: 4eb2c04c940dd6ad15a491a331aed76c237f0387
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/03/2017
---
# <a name="problem-configuring-federated-single-sign-on-for-a-non-gallery-application"></a><span data-ttu-id="80579-103">Problema nella configurazione dell'accesso Single Sign-On federato per un'applicazione non inclusa nella raccolta di Azure AD</span><span class="sxs-lookup"><span data-stu-id="80579-103">Problem configuring federated single sign-on for a non-gallery application</span></span>

<span data-ttu-id="80579-104">Se si verifica un problema durante la configurazione di un'applicazione.</span><span class="sxs-lookup"><span data-stu-id="80579-104">If you encounter a problem when configuring an application.</span></span> <span data-ttu-id="80579-105">Verificare di avere seguito tutti i passaggi indicati nell'articolo [Configurazione del servizio Single Sign-On in applicazioni non presenti nella raccolta di applicazioni di Azure Active Directory](https://docs.microsoft.com/azure/active-directory/active-directory-saas-custom-apps).</span><span class="sxs-lookup"><span data-stu-id="80579-105">Verify you have followed all the steps in the article [Configuring single sign-on to applications that are not in the Azure Active Directory application gallery.](https://docs.microsoft.com/azure/active-directory/active-directory-saas-custom-apps)</span></span>

## <a name="cant-add-another-instance-of-the-application"></a><span data-ttu-id="80579-106">Impossibile aggiungere un'altra istanza dell'applicazione</span><span class="sxs-lookup"><span data-stu-id="80579-106">Can’t add another instance of the application</span></span>

<span data-ttu-id="80579-107">Per aggiungere una seconda istanza di un'applicazione, è necessario:</span><span class="sxs-lookup"><span data-stu-id="80579-107">To add a second instance of an application, you need to be able to:</span></span>

-   <span data-ttu-id="80579-108">Configurare un identificatore univoco per la seconda istanza.</span><span class="sxs-lookup"><span data-stu-id="80579-108">Configure a unique identifier for the second instance.</span></span> <span data-ttu-id="80579-109">Non è possibile configurare lo stesso identificatore usato per la prima istanza.</span><span class="sxs-lookup"><span data-stu-id="80579-109">You won’t be able to configure the same identifier used for the first instance.</span></span>

-   <span data-ttu-id="80579-110">Configurare un certificato diverso da quello usato per la prima istanza.</span><span class="sxs-lookup"><span data-stu-id="80579-110">Configure a different certificate than the one used for the first instance.</span></span>

<span data-ttu-id="80579-111">Se l'applicazione non supporta alcuna delle operazioni sopra indicate,</span><span class="sxs-lookup"><span data-stu-id="80579-111">If the application doesn’t support any of the above.</span></span> <span data-ttu-id="80579-112">non è possibile configurare una seconda istanza.</span><span class="sxs-lookup"><span data-stu-id="80579-112">Then, you won’t be able to configure a second instance.</span></span>

## <a name="where-do-i-set-the-entityid-user-identifier-format"></a><span data-ttu-id="80579-113">Dove impostare il formato di EntityID (Identificatore utente)</span><span class="sxs-lookup"><span data-stu-id="80579-113">Where do I set the EntityID (User Identifier) format</span></span>

<span data-ttu-id="80579-114">Non è possibile selezionare il formato di EntityID (identificatore utente) che Azure AD invia all'applicazione in risposta all'autenticazione dell'utente.</span><span class="sxs-lookup"><span data-stu-id="80579-114">You won’t be able to select the EntityID (User Identifier) format that Azure AD sends to the application in the response after user authentication.</span></span>

<span data-ttu-id="80579-115">Azure AD seleziona il formato per l'attributo NameID (identificatore utente) in base al valore selezionato o al formato richiesto dall'applicazione nell'oggetto AuthRequest SAML.</span><span class="sxs-lookup"><span data-stu-id="80579-115">Azure AD select the format for the NameID attribute (User Identifier) based on the value selected or the format requested by the application in the SAML AuthRequest.</span></span> <span data-ttu-id="80579-116">Per altre informazioni, vedere l'articolo relativo al [protocollo SAML per Single Sign-On](https://docs.microsoft.com/azure/active-directory/develop/active-directory-single-sign-on-protocol-reference#authnrequest) sotto la sezione NameIDPolicy.</span><span class="sxs-lookup"><span data-stu-id="80579-116">For more information visit the article [Single Sign-On SAML protocol](https://docs.microsoft.com/azure/active-directory/develop/active-directory-single-sign-on-protocol-reference#authnrequest) under the section NameIDPolicy,</span></span>

## <a name="where-do-i-get-the-application-metadata-or-certificate-from-azure-ad"></a><span data-ttu-id="80579-117">Dove scaricare il certificato o i metadati dell'applicazione da Azure AD</span><span class="sxs-lookup"><span data-stu-id="80579-117">Where do I get the application metadata or certificate from Azure AD</span></span>

<span data-ttu-id="80579-118">Per scaricare il certificato o i metadati dell'applicazione da Azure AD, seguire questa procedura:</span><span class="sxs-lookup"><span data-stu-id="80579-118">To download the application metadata or certificate from Azure AD, follow the steps below:</span></span>

1.  <span data-ttu-id="80579-119">Aprire il [**portale di Azure**](https://portal.azure.com/) e accedere come **Amministratore globale** o **Coamministratore**.</span><span class="sxs-lookup"><span data-stu-id="80579-119">Open the [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator** or **Co-admin.**</span></span>

2.  <span data-ttu-id="80579-120">Aprire l'**estensione Azure Active Directory** facendo clic su **Altri servizi** nella parte inferiore del menu di navigazione principale a sinistra.</span><span class="sxs-lookup"><span data-stu-id="80579-120">Open the **Azure Active Directory Extension** by clicking **More services** at the bottom of the main left hand navigation menu.</span></span>

3.  <span data-ttu-id="80579-121">Digitare "**Azure Active Directory**" nella casella di ricerca filtro e selezionare l'elemento **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="80579-121">Type in **“Azure Active Directory**” in the filter search box and select the **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="80579-122">Fare clic su **Applicazioni aziendali** nel menu di navigazione a sinistra di Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="80579-122">click **Enterprise Applications** from the Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="80579-123">Fare clic su **Tutte le applicazioni** per visualizzare un elenco di tutte le applicazioni.</span><span class="sxs-lookup"><span data-stu-id="80579-123">click **All Applications** to view a list of all your applications.</span></span>

   * <span data-ttu-id="80579-124">Se l'applicazione non è inclusa nell'elenco, usare il controllo **Filtro** all'inizio dell'elenco **Tutte le applicazioni** e impostare l'opzione **Mostra** su **Tutte le applicazioni**.</span><span class="sxs-lookup"><span data-stu-id="80579-124">If you do not see the application you want show up here, use the **Filter** control at the top of the **All Applications List** and set the **Show** option to **All Applications.**</span></span>

6.  <span data-ttu-id="80579-125">Selezionare l'applicazione per cui è stato configurato l'accesso Single Sign-On.</span><span class="sxs-lookup"><span data-stu-id="80579-125">Select the application you have configured single sign-on.</span></span>

7.  <span data-ttu-id="80579-126">Dopo il caricamento dell'applicazione, fare clic su **Single Sign-On** nel menu di navigazione a sinistra dell'applicazione.</span><span class="sxs-lookup"><span data-stu-id="80579-126">Once the application loads, click the **Single sign-on** from the application’s left hand navigation menu.</span></span>

8.  <span data-ttu-id="80579-127">Passare alla sezione **Certificato di firma SAML** e quindi fare clic sul valore della colonna **Download**.</span><span class="sxs-lookup"><span data-stu-id="80579-127">Go to **SAML Signing Certificate** section, then click **Download** column value.</span></span> <span data-ttu-id="80579-128">A seconda di quale applicazione richiede la configurazione dell'accesso Single Sign-On, è visibile l'opzione per scaricare il codice XML dei metadati o l'opzione per scaricare il certificato.</span><span class="sxs-lookup"><span data-stu-id="80579-128">Depending on what the application requires configuring single sign-on, you see either the option to download the Metadata XML or the Certificate.</span></span>

<span data-ttu-id="80579-129">Azure AD non fornisce URL per ottenere i metadati.</span><span class="sxs-lookup"><span data-stu-id="80579-129">Azure AD doesn’t provide a URL to get the metadata.</span></span> <span data-ttu-id="80579-130">I metadati possono essere recuperati solo come file XML.</span><span class="sxs-lookup"><span data-stu-id="80579-130">The metadata can only be retrieved as a XML file.</span></span>

## <a name="dont-know-how-to-customize-saml-claims-sent-to-an-application"></a><span data-ttu-id="80579-131">Informazioni sulla personalizzazione delle attestazioni SAML inviate a un'applicazione</span><span class="sxs-lookup"><span data-stu-id="80579-131">Don't know how to customize SAML claims sent to an application</span></span>

<span data-ttu-id="80579-132">Per informazioni su come personalizzare le attestazioni degli attributi SAML inviate all'applicazione, vedere [Claims mapping in Azure Active Directory](https://docs.microsoft.com/azure/active-directory/active-directory-claims-mapping) (Mapping di attestazioni in Azure Active Directory).</span><span class="sxs-lookup"><span data-stu-id="80579-132">To learn how to customize the SAML attribute claims sent to your application, see [Claims mapping in Azure Active Directory](https://docs.microsoft.com/azure/active-directory/active-directory-claims-mapping) for more information.</span></span>

## <a name="next-steps"></a><span data-ttu-id="80579-133">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="80579-133">Next steps</span></span>
[<span data-ttu-id="80579-134">Gestione di applicazioni con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="80579-134">Managing Applications with Azure Active Directory</span></span>](active-directory-enable-sso-scenario.md)

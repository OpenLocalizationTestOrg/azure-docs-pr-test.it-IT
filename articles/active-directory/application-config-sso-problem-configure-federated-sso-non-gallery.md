---
title: configurazione di single sign-on federato per un'applicazione non raccolta aaaProblem | Documenti Microsoft
description: "Risolvere alcuni dei problemi di hello comuni che riscontrabili durante la configurazione federata single sign-on tooyour personalizzata SAML dell'applicazione che non è elencato nella raccolta di applicazioni Azure AD hello"
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
ms.openlocfilehash: 8c80f0001de01cbc9930ef0441cd804082ee8578
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="problem-configuring-federated-single-sign-on-for-a-non-gallery-application"></a><span data-ttu-id="7d0df-103">Problema nella configurazione dell'accesso Single Sign-On federato per un'applicazione non inclusa nella raccolta di Azure AD</span><span class="sxs-lookup"><span data-stu-id="7d0df-103">Problem configuring federated single sign-on for a non-gallery application</span></span>

<span data-ttu-id="7d0df-104">Se si verifica un problema durante la configurazione di un'applicazione.</span><span class="sxs-lookup"><span data-stu-id="7d0df-104">If you encounter a problem when configuring an application.</span></span> <span data-ttu-id="7d0df-105">Verificare di aver seguito tutti i passaggi nell'articolo hello hello [configurazione single sign-on tooapplications non presenti nella raccolta di hello Azure Active Directory dell'applicazione.](https://docs.microsoft.com/azure/active-directory/active-directory-saas-custom-apps)</span><span class="sxs-lookup"><span data-stu-id="7d0df-105">Verify you have followed all hello steps in hello article [Configuring single sign-on tooapplications that are not in hello Azure Active Directory application gallery.](https://docs.microsoft.com/azure/active-directory/active-directory-saas-custom-apps)</span></span>

## <a name="cant-add-another-instance-of-hello-application"></a><span data-ttu-id="7d0df-106">Non è possibile aggiungere un'altra istanza di un'applicazione hello</span><span class="sxs-lookup"><span data-stu-id="7d0df-106">Can’t add another instance of hello application</span></span>

<span data-ttu-id="7d0df-107">tooadd una seconda istanza di un'applicazione, è necessario poter toobe:</span><span class="sxs-lookup"><span data-stu-id="7d0df-107">tooadd a second instance of an application, you need toobe able to:</span></span>

-   <span data-ttu-id="7d0df-108">Configurare un identificatore univoco per la seconda istanza hello.</span><span class="sxs-lookup"><span data-stu-id="7d0df-108">Configure a unique identifier for hello second instance.</span></span> <span data-ttu-id="7d0df-109">Non sarà in grado di tooconfigure hello stesso identificatore utilizzato per la prima istanza hello.</span><span class="sxs-lookup"><span data-stu-id="7d0df-109">You won’t be able tooconfigure hello same identifier used for hello first instance.</span></span>

-   <span data-ttu-id="7d0df-110">Configurare un certificato diverso da hello di hello prima istanza.</span><span class="sxs-lookup"><span data-stu-id="7d0df-110">Configure a different certificate than hello one used for hello first instance.</span></span>

<span data-ttu-id="7d0df-111">Se hello applicazione non supporta i hello precedente.</span><span class="sxs-lookup"><span data-stu-id="7d0df-111">If hello application doesn’t support any of hello above.</span></span> <span data-ttu-id="7d0df-112">Quindi, non sarà in grado di tooconfigure una seconda istanza.</span><span class="sxs-lookup"><span data-stu-id="7d0df-112">Then, you won’t be able tooconfigure a second instance.</span></span>

## <a name="where-do-i-set-hello-entityid-user-identifier-format"></a><span data-ttu-id="7d0df-113">In cui è possibile impostare il formato di EntityID (ID utente) hello</span><span class="sxs-lookup"><span data-stu-id="7d0df-113">Where do I set hello EntityID (User Identifier) format</span></span>

<span data-ttu-id="7d0df-114">Sarà formato EntityID (ID utente) di hello tooselect in grado di Azure AD invia toohello applicazione in risposta hello dopo l'autenticazione utente.</span><span class="sxs-lookup"><span data-stu-id="7d0df-114">You won’t be able tooselect hello EntityID (User Identifier) format that Azure AD sends toohello application in hello response after user authentication.</span></span>

<span data-ttu-id="7d0df-115">Azure AD selezionare hello formato attributo NameID hello (ID utente) in base al valore di hello selezionato o per hello formato richiesto da un'applicazione hello in hello AuthRequest SAML.</span><span class="sxs-lookup"><span data-stu-id="7d0df-115">Azure AD select hello format for hello NameID attribute (User Identifier) based on hello value selected or hello format requested by hello application in hello SAML AuthRequest.</span></span> <span data-ttu-id="7d0df-116">Per ulteriori informazioni visitare articolo hello [protocollo Single Sign-On SAML](https://docs.microsoft.com/azure/active-directory/develop/active-directory-single-sign-on-protocol-reference#authnrequest) nella sezione hello NameIDPolicy,</span><span class="sxs-lookup"><span data-stu-id="7d0df-116">For more information visit hello article [Single Sign-On SAML protocol](https://docs.microsoft.com/azure/active-directory/develop/active-directory-single-sign-on-protocol-reference#authnrequest) under hello section NameIDPolicy,</span></span>

## <a name="where-do-i-get-hello-application-metadata-or-certificate-from-azure-ad"></a><span data-ttu-id="7d0df-117">Dove ottenere i metadati dell'applicazione hello o un certificato da Azure AD</span><span class="sxs-lookup"><span data-stu-id="7d0df-117">Where do I get hello application metadata or certificate from Azure AD</span></span>

<span data-ttu-id="7d0df-118">i metadati dell'applicazione hello toodownload o un certificato da Azure AD, procedura hello riportata di seguito:</span><span class="sxs-lookup"><span data-stu-id="7d0df-118">toodownload hello application metadata or certificate from Azure AD, follow hello steps below:</span></span>

1.  <span data-ttu-id="7d0df-119">Aprire hello [ **portale Azure** ](https://portal.azure.com/) e accedere come un **amministratore globale** o **Co-amministratore.**</span><span class="sxs-lookup"><span data-stu-id="7d0df-119">Open hello [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator** or **Co-admin.**</span></span>

2.  <span data-ttu-id="7d0df-120">Aprire hello **estensione di Azure Active Directory** facendo **più servizi** nella parte inferiore di hello del menu di navigazione a sinistra principale hello.</span><span class="sxs-lookup"><span data-stu-id="7d0df-120">Open hello **Azure Active Directory Extension** by clicking **More services** at hello bottom of hello main left hand navigation menu.</span></span>

3.  <span data-ttu-id="7d0df-121">Digitare **"Azure Active Directory**" nella casella di ricerca di filtro hello e seleziona hello **Azure Active Directory** elemento.</span><span class="sxs-lookup"><span data-stu-id="7d0df-121">Type in **“Azure Active Directory**” in hello filter search box and select hello **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="7d0df-122">Fare clic su **applicazioni aziendali** dal menu di navigazione a sinistra di hello Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="7d0df-122">click **Enterprise Applications** from hello Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="7d0df-123">Fare clic su **tutte le applicazioni** tooview un elenco di tutte le applicazioni.</span><span class="sxs-lookup"><span data-stu-id="7d0df-123">click **All Applications** tooview a list of all your applications.</span></span>

   * <span data-ttu-id="7d0df-124">Se non viene visualizzata l'applicazione hello da visualizzare qui, utilizzare hello **filtro** controllo nella parte superiore di hello di hello **elenco di tutte le applicazioni** e set hello **Mostra** opzione troppo **Tutte le applicazioni.**</span><span class="sxs-lookup"><span data-stu-id="7d0df-124">If you do not see hello application you want show up here, use hello **Filter** control at hello top of hello **All Applications List** and set hello **Show** option too**All Applications.**</span></span>

6.  <span data-ttu-id="7d0df-125">Selezionare un'applicazione hello è stato configurato single sign-on.</span><span class="sxs-lookup"><span data-stu-id="7d0df-125">Select hello application you have configured single sign-on.</span></span>

7.  <span data-ttu-id="7d0df-126">Una volta che un'applicazione hello caricato, fare clic su hello **Single sign-on** dal menu di navigazione a sinistra dell'applicazione hello.</span><span class="sxs-lookup"><span data-stu-id="7d0df-126">Once hello application loads, click hello **Single sign-on** from hello application’s left hand navigation menu.</span></span>

8.  <span data-ttu-id="7d0df-127">Andare troppo**certificato di firma SAML** sezione, quindi fare clic su **scaricare** valore della colonna.</span><span class="sxs-lookup"><span data-stu-id="7d0df-127">Go too**SAML Signing Certificate** section, then click **Download** column value.</span></span> <span data-ttu-id="7d0df-128">A seconda di quale applicazione hello richiede la configurazione di single sign-on, vedere uno toodownload opzione hello hello Metadata XML o hello certificato.</span><span class="sxs-lookup"><span data-stu-id="7d0df-128">Depending on what hello application requires configuring single sign-on, you see either hello option toodownload hello Metadata XML or hello Certificate.</span></span>

<span data-ttu-id="7d0df-129">Azure AD non fornisce i metadati hello tooget URL.</span><span class="sxs-lookup"><span data-stu-id="7d0df-129">Azure AD doesn’t provide a URL tooget hello metadata.</span></span> <span data-ttu-id="7d0df-130">Hello metadati possono essere recuperati solo come un file XML.</span><span class="sxs-lookup"><span data-stu-id="7d0df-130">hello metadata can only be retrieved as a XML file.</span></span>

## <a name="dont-know-how-toocustomize-saml-claims-sent-tooan-application"></a><span data-ttu-id="7d0df-131">Non conosce la modalità di invio applicazione tooan attestazioni SAML toocustomize</span><span class="sxs-lookup"><span data-stu-id="7d0df-131">Don't know how toocustomize SAML claims sent tooan application</span></span>

<span data-ttu-id="7d0df-132">toolearn come le attestazioni degli attributi toocustomize hello SAML inviato tooyour applicazione, vedere [attestazioni mapping in Azure Active Directory](https://docs.microsoft.com/azure/active-directory/active-directory-claims-mapping) per ulteriori informazioni.</span><span class="sxs-lookup"><span data-stu-id="7d0df-132">toolearn how toocustomize hello SAML attribute claims sent tooyour application, see [Claims mapping in Azure Active Directory](https://docs.microsoft.com/azure/active-directory/active-directory-claims-mapping) for more information.</span></span>

## <a name="next-steps"></a><span data-ttu-id="7d0df-133">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="7d0df-133">Next steps</span></span>
[<span data-ttu-id="7d0df-134">Gestione di applicazioni con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="7d0df-134">Managing Applications with Azure Active Directory</span></span>](active-directory-enable-sso-scenario.md)

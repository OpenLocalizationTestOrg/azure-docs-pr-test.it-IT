---
title: 'Azure Active Directory B2C: attributi personalizzati | Documentazione Microsoft'
description: "La modalità di attributi personalizzati di toouse in Azure Active Directory B2C toocollect informazioni utenti"
services: active-directory-b2c
documentationcenter: 
author: swkrish
manager: mbaldwin
editor: bryanla
ms.assetid: 055ffb0a-197b-4716-8dad-1fd8a01e174f
ms.service: active-directory-b2c
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 12/06/2016
ms.author: swkrish
ms.openlocfilehash: fb1bff77ad54c246c6d2f69f39c03eafb76fe6bf
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="azure-active-directory-b2c-use-custom-attributes-toocollect-information-about-your-consumers"></a><span data-ttu-id="9e545-103">Azure Active B2C di Directory: Utilizzare attributi personalizzati toocollect informazioni utenti</span><span class="sxs-lookup"><span data-stu-id="9e545-103">Azure Active Directory B2C: Use custom attributes toocollect information about your consumers</span></span>
<span data-ttu-id="9e545-104">La directory Azure Active Directory (Azure AD) B2C viene fornita con un set predefinito di informazioni (attributi), ad esempio nome, cognome, città, codice postale e altri attributi.</span><span class="sxs-lookup"><span data-stu-id="9e545-104">Your Azure Active Directory (Azure AD) B2C directory comes with a built-in set of information (attributes): Given Name, Surname, City, Postal Code, and other attributes.</span></span> <span data-ttu-id="9e545-105">Tuttavia, ogni applicazione per consumatori presenta requisiti specifici su quali toogather attributi dal consumer.</span><span class="sxs-lookup"><span data-stu-id="9e545-105">However, every consumer-facing application has unique requirements on what attributes toogather from consumers.</span></span> <span data-ttu-id="9e545-106">Con Azure Active Directory B2C, è possibile estendere il set di hello di attributi archiviati in ogni account utente.</span><span class="sxs-lookup"><span data-stu-id="9e545-106">With Azure AD B2C, you can extend hello set of attributes stored on each consumer account.</span></span> <span data-ttu-id="9e545-107">È possibile creare attributi personalizzati in hello [portale di Azure](https://portal.azure.com/) e usare nei criteri per l'abbonamento, come illustrato di seguito.</span><span class="sxs-lookup"><span data-stu-id="9e545-107">You can create custom attributes on hello [Azure portal](https://portal.azure.com/) and use it in your sign-up policies, as shown below.</span></span> <span data-ttu-id="9e545-108">È anche possibile leggere e scrivere tali attributi tramite hello [API Azure AD Graph](active-directory-b2c-devquickstarts-graph-dotnet.md).</span><span class="sxs-lookup"><span data-stu-id="9e545-108">You can also read and write these attributes by using hello [Azure AD Graph API](active-directory-b2c-devquickstarts-graph-dotnet.md).</span></span>

> [!NOTE]
> <span data-ttu-id="9e545-109">Gli attributi personalizzati usano le [Estensioni dello schema di directory dell'API Graph di Azure AD](https://msdn.microsoft.com/library/azure/dn720459.aspx).</span><span class="sxs-lookup"><span data-stu-id="9e545-109">Custom attributes use [Azure AD Graph API Directory Schema Extensions](https://msdn.microsoft.com/library/azure/dn720459.aspx).</span></span>
> 
> 

## <a name="create-a-custom-attribute"></a><span data-ttu-id="9e545-110">Creare un attributo personalizzato</span><span class="sxs-lookup"><span data-stu-id="9e545-110">Create a custom attribute</span></span>
1. <span data-ttu-id="9e545-111">[Seguire questi blade di passaggi toonavigate toohello B2C funzionalità nel portale di Azure hello](active-directory-b2c-app-registration.md#navigate-to-b2c-settings).</span><span class="sxs-lookup"><span data-stu-id="9e545-111">[Follow these steps toonavigate toohello B2C features blade on hello Azure portal](active-directory-b2c-app-registration.md#navigate-to-b2c-settings).</span></span>
2. <span data-ttu-id="9e545-112">Fare clic su **Attributi utente**.</span><span class="sxs-lookup"><span data-stu-id="9e545-112">Click **User attributes**.</span></span>
3. <span data-ttu-id="9e545-113">Fare clic su **+ Aggiungi** nella parte superiore di hello del pannello hello.</span><span class="sxs-lookup"><span data-stu-id="9e545-113">Click **+Add** at hello top of hello blade.</span></span>
4. <span data-ttu-id="9e545-114">Fornire un **nome** per l'attributo personalizzato hello (ad esempio, "ShoeSize") e, facoltativamente, un **descrizione**.</span><span class="sxs-lookup"><span data-stu-id="9e545-114">Provide a **Name** for hello custom attribute (for example, "ShoeSize") and optionally, a **Description**.</span></span> <span data-ttu-id="9e545-115">Fare clic su **Crea**.</span><span class="sxs-lookup"><span data-stu-id="9e545-115">Click **Create**.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="9e545-116">Solo hello "Stringa" **tipo di dati** è attualmente disponibile.</span><span class="sxs-lookup"><span data-stu-id="9e545-116">Only hello "String" **Data Type** is currently available.</span></span>
   > 
   > 

<span data-ttu-id="9e545-117">attributo personalizzato Hello è ora disponibile nell'elenco di hello di **gli attributi utente**e per l'uso nei criteri per l'abbonamento.</span><span class="sxs-lookup"><span data-stu-id="9e545-117">hello custom attribute is now available in hello list of **User attributes**, and for use in your sign-up policies.</span></span>

## <a name="use-a-custom-attribute-in-your-sign-up-policy"></a><span data-ttu-id="9e545-118">Usare un attributo personalizzato nei criteri di iscrizione</span><span class="sxs-lookup"><span data-stu-id="9e545-118">Use a custom attribute in your sign-up policy</span></span>
1. <span data-ttu-id="9e545-119">[Seguire questi blade di passaggi toonavigate toohello B2C funzionalità nel portale di Azure hello](active-directory-b2c-app-registration.md#navigate-to-b2c-settings).</span><span class="sxs-lookup"><span data-stu-id="9e545-119">[Follow these steps toonavigate toohello B2C features blade on hello Azure portal](active-directory-b2c-app-registration.md#navigate-to-b2c-settings).</span></span>
2. <span data-ttu-id="9e545-120">Fare clic su **Criteri di iscrizione**.</span><span class="sxs-lookup"><span data-stu-id="9e545-120">Click **Sign-up policies**.</span></span>
3. <span data-ttu-id="9e545-121">Fare clic su tooopen i criteri di iscrizione (ad esempio, "B2C_1_SiUp") è.</span><span class="sxs-lookup"><span data-stu-id="9e545-121">Click your sign-up policy (for example, "B2C_1_SiUp") tooopen it.</span></span> <span data-ttu-id="9e545-122">Fare clic su **modifica** nella parte superiore di hello del pannello hello.</span><span class="sxs-lookup"><span data-stu-id="9e545-122">Click **Edit** at hello top of hello blade.</span></span>
4. <span data-ttu-id="9e545-123">Fare clic su **attributi iscrizione** e l'attributo personalizzato selezionare hello (ad esempio, "ShoeSize").</span><span class="sxs-lookup"><span data-stu-id="9e545-123">Click **Sign-up attributes** and select hello custom attribute (for example, "ShoeSize").</span></span> <span data-ttu-id="9e545-124">Fare clic su **OK**.</span><span class="sxs-lookup"><span data-stu-id="9e545-124">Click **OK**.</span></span>
5. <span data-ttu-id="9e545-125">Fare clic su **attestazioni applicazione** e l'attributo personalizzato hello selezionare.</span><span class="sxs-lookup"><span data-stu-id="9e545-125">Click **Application claims** and select hello custom attribute.</span></span> <span data-ttu-id="9e545-126">Fare clic su **OK**.</span><span class="sxs-lookup"><span data-stu-id="9e545-126">Click **OK**.</span></span>
6. <span data-ttu-id="9e545-127">Fare clic su **salvare** nella parte superiore di hello del pannello hello.</span><span class="sxs-lookup"><span data-stu-id="9e545-127">Click **Save** at hello top of hello blade.</span></span>

<span data-ttu-id="9e545-128">È possibile utilizzare funzionalità "Esegui" hello sull'esperienza di hello criteri tooverify hello consumer.</span><span class="sxs-lookup"><span data-stu-id="9e545-128">You can use hello "Run now" feature on hello policy tooverify hello consumer experience.</span></span> <span data-ttu-id="9e545-129">Dovrebbero ora vedere "ShoeSize" nell'elenco di hello di attributi raccolti durante l'iscrizione consumer e visualizzarlo in un'applicazione hello token tooyour indietro inviato.</span><span class="sxs-lookup"><span data-stu-id="9e545-129">You should now see "ShoeSize" in hello list of attributes collected during consumer sign-up, and see it in hello token sent back tooyour application.</span></span>

## <a name="notes"></a><span data-ttu-id="9e545-130">Note</span><span class="sxs-lookup"><span data-stu-id="9e545-130">Notes</span></span>
* <span data-ttu-id="9e545-131">Insieme ai criteri di iscrizione, gli attributi personalizzati possono essere usati anche nei criteri di iscrizione o accesso e nei criteri di modifica del profilo.</span><span class="sxs-lookup"><span data-stu-id="9e545-131">Along with sign-up policies, custom attributes can also be used in sign-up or sign-in policies and profile editing policies.</span></span>
* <span data-ttu-id="9e545-132">Esiste una limitazione nota degli attributi personalizzati.</span><span class="sxs-lookup"><span data-stu-id="9e545-132">There is a known limitation of custom attributes.</span></span> <span data-ttu-id="9e545-133">È solo creato hello prima volta che viene utilizzata in tutti i criteri e non quando si aggiungerla elenco toohello di **gli attributi utente**.</span><span class="sxs-lookup"><span data-stu-id="9e545-133">It is only created hello first time it is used in any policy, and not when you add it toohello list of **User attributes**.</span></span>


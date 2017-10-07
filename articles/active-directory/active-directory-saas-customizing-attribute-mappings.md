---
title: aaaCustomizing i mapping degli attributi di Active Directory di Azure | Documenti Microsoft
description: "Conoscere il mapping degli attributi per le applicazioni SaaS in Azure Active Directory come è possibile modificarle tooaddress l'azienda necessita."
services: active-directory
documentationcenter: 
author: MarkusVi
manager: femila
editor: 
ms.assetid: 549e0b8c-87ce-4c9b-b487-b7bf0155dc77
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/17/2017
ms.author: markvi
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 14db5303f06fc8df3b07a0a8b75713312e71bbfd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="customizing-user-provisioning-attribute-mappings-for-saas-applications-in-azure-active-directory"></a><span data-ttu-id="a48c4-103">Personalizzazione dei mapping degli attributi del provisioning degli utenti per le applicazioni SaaS in Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="a48c4-103">Customizing User Provisioning Attribute Mappings for SaaS Applications in Azure Active Directory</span></span>
<span data-ttu-id="a48c4-104">Microsoft Azure AD fornisce supporto per applicazioni SaaS di terze parti toothird come Salesforce, Google Apps e altre di provisioning dell'utente.</span><span class="sxs-lookup"><span data-stu-id="a48c4-104">Microsoft Azure AD provides support for user provisioning toothird-party SaaS applications such as Salesforce, Google Apps and others.</span></span> <span data-ttu-id="a48c4-105">Se si dispone di un'applicazione SaaS di terze parti abilitata il provisioning degli utenti, hello portale di gestione di Azure controlla i valori di attributo sotto forma di una configurazione denominata "mapping degli attributi".</span><span class="sxs-lookup"><span data-stu-id="a48c4-105">If you have user provisioning for a third-party SaaS application enabled, hello Azure Management Portal controls its attribute values in form of a configuration called “attribute mapping.”</span></span>

<span data-ttu-id="a48c4-106">Esiste un set preconfigurato di mapping degli attributi tra gli oggetti utente di Azure AD e gli oggetti utente di ogni app SaaS.</span><span class="sxs-lookup"><span data-stu-id="a48c4-106">There is a preconfigured set of attribute mappings between Azure AD user objects and each SaaS app’s user objects.</span></span> <span data-ttu-id="a48c4-107">Alcune app gestiscono altri tipi di oggetti, quali Gruppi o Contatti.</span><span class="sxs-lookup"><span data-stu-id="a48c4-107">Some apps manage other types of objects, such as Groups or Contacts.</span></span> <br> 
 <span data-ttu-id="a48c4-108">È possibile personalizzare i mapping degli attributi predefinito hello in base alle esigenze aziendali tooyour.</span><span class="sxs-lookup"><span data-stu-id="a48c4-108">You can customize hello default attribute mappings according tooyour business needs.</span></span> <span data-ttu-id="a48c4-109">È infatti possibile modificare o eliminare i mapping degli attributi esistenti oppure crearne di nuovi.</span><span class="sxs-lookup"><span data-stu-id="a48c4-109">This means, you can change or delete existing attribute mappings or create new attribute mappings.</span></span>

<span data-ttu-id="a48c4-110">Nel portale di Azure AD hello, è possibile accedere a questa funzionalità facendo clic su un **mapping** configurazione **Provisioning** in hello **Gestisci** sezione di un  **Applicazione aziendale**.</span><span class="sxs-lookup"><span data-stu-id="a48c4-110">In hello Azure AD portal, you can access this feature by clicking a **Mappings** configuration under **Provisioning** in hello **Manage** section of an **Enterprise application**.</span></span>


![Salesforce][5] 

<span data-ttu-id="a48c4-112">Fare clic su un **mapping** configurazione, verrà aperta hello correlato **attributo Mapping** blade.</span><span class="sxs-lookup"><span data-stu-id="a48c4-112">Clicking a **Mappings** configuration, opens hello related **Attribute Mapping** blade.</span></span>  
<span data-ttu-id="a48c4-113">Sono presenti i mapping degli attributi richiesti da un toofunction applicazione SaaS correttamente.</span><span class="sxs-lookup"><span data-stu-id="a48c4-113">There are attribute mappings that are required by a SaaS application toofunction correctly.</span></span> <span data-ttu-id="a48c4-114">Per gli attributi obbligatori, hello **eliminare** funzionalità non è disponibile.</span><span class="sxs-lookup"><span data-stu-id="a48c4-114">For required attributes, hello **Delete** feature is unavailable.</span></span>


![Salesforce][6]  

<span data-ttu-id="a48c4-116">Nell'esempio hello sopra, è possibile visualizzare tale hello **Username** attributo di un oggetto gestito in Salesforce è popolato con hello **userPrincipalName** valore di hello collegato l'oggetto di Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="a48c4-116">In hello example above, you can see that hello **Username** attribute of a managed object in Salesforce is populated with hello **userPrincipalName** value of hello linked Azure Active Directory Object.</span></span>

<span data-ttu-id="a48c4-117">È possibile personalizzare i **Mapping degli attributi** esistenti facendo clic su un mapping.</span><span class="sxs-lookup"><span data-stu-id="a48c4-117">You can customize existing **Attribute Mappings** by clicking a mapping.</span></span> <span data-ttu-id="a48c4-118">Verrà visualizzata hello **Modifica attributo** blade.</span><span class="sxs-lookup"><span data-stu-id="a48c4-118">This opens hello **Edit Attribute** blade.</span></span>

![Salesforce][7]  


  

## <a name="understanding-attribute-mapping-types"></a><span data-ttu-id="a48c4-120">Informazioni sui tipi di mapping degli attributi</span><span class="sxs-lookup"><span data-stu-id="a48c4-120">Understanding attribute mapping types</span></span>
<span data-ttu-id="a48c4-121">I mapping degli attributi permettono di controllare il modo in cui gli attribuiti vengono popolati in un'applicazione SaaS di terze parti.</span><span class="sxs-lookup"><span data-stu-id="a48c4-121">With attribute mappings, you control how attributes are populated in a third-party SaaS application.</span></span> <span data-ttu-id="a48c4-122">Sono supportati quattro diversi tipi di mapping:</span><span class="sxs-lookup"><span data-stu-id="a48c4-122">There are four different mapping types supported:</span></span>

* <span data-ttu-id="a48c4-123">**Diretto** : attributo di destinazione hello viene popolato con il valore di hello di un attributo dell'oggetto collegato hello in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="a48c4-123">**Direct** – hello target attribute is populated with hello value of an attribute of hello linked object in Azure AD.</span></span>
* <span data-ttu-id="a48c4-124">**Costante** : attributo di destinazione hello viene popolato con una stringa specifica è stato specificato.</span><span class="sxs-lookup"><span data-stu-id="a48c4-124">**Constant** – hello target attribute is populated with a specific string you have specified.</span></span>
* <span data-ttu-id="a48c4-125">**Espressione** -attributo di destinazione hello viene popolato in base al risultato di un'espressione analoga a uno script hello.</span><span class="sxs-lookup"><span data-stu-id="a48c4-125">**Expression** - hello target attribute is populated based on hello result of a script-like expression.</span></span> 
  <span data-ttu-id="a48c4-126">Per altre informazioni, vedere [Scrittura di espressioni per il mapping degli attributi in Azure Active Directory](active-directory-saas-writing-expressions-for-attribute-mappings.md).</span><span class="sxs-lookup"><span data-stu-id="a48c4-126">For more information, see [Writing Expressions for Attribute Mappings in Azure Active Directory](active-directory-saas-writing-expressions-for-attribute-mappings.md).</span></span>
* <span data-ttu-id="a48c4-127">**Nessuna** -attributo di destinazione hello viene lasciato invariato.</span><span class="sxs-lookup"><span data-stu-id="a48c4-127">**None** - hello target attribute is left unmodified.</span></span> <span data-ttu-id="a48c4-128">Tuttavia, se l'attributo di destinazione hello viene lasciato vuoto, viene popolata con il valore predefinito di hello specificato.</span><span class="sxs-lookup"><span data-stu-id="a48c4-128">However, if hello target attribute is ever empty, it is populated with hello Default value that you specify.</span></span>

<span data-ttu-id="a48c4-129">In tipi di mapping di addizione toothese quattro attributi di base, mapping di attributi personalizzati supportano il concetto di hello di facoltativa **predefinito** valore assegnazione.</span><span class="sxs-lookup"><span data-stu-id="a48c4-129">In addition toothese four basic attribute mapping types, custom attribute mappings support hello concept of an optional **default** value assignment.</span></span> <span data-ttu-id="a48c4-130">assegnazione di valore predefinito di Hello garantisce che un attributo di destinazione viene popolato con un valore se è presente un valore né in Azure AD, né nell'oggetto di destinazione hello.</span><span class="sxs-lookup"><span data-stu-id="a48c4-130">hello default value assignment ensures that a target attribute is populated with a value if there is neither a value in Azure AD nor on hello target object.</span></span> <span data-ttu-id="a48c4-131">la configurazione più comune di Hello è tooleave questo vuoto.</span><span class="sxs-lookup"><span data-stu-id="a48c4-131">hello most common configuration is tooleave this blank.</span></span>


## <a name="understanding-attribute-mapping-properties"></a><span data-ttu-id="a48c4-132">Informazioni sulle proprietà di mapping degli attributi</span><span class="sxs-lookup"><span data-stu-id="a48c4-132">Understanding attribute mapping properties</span></span>

<span data-ttu-id="a48c4-133">Nella sezione precedente hello, sono già state introdotte toohello attributo mapping tipo proprietà.</span><span class="sxs-lookup"><span data-stu-id="a48c4-133">In hello previous section, you have already been introduced toohello attribute mapping type property.</span></span>
<span data-ttu-id="a48c4-134">Nella proprietà toothis inoltre, i mapping degli attributi supportano anche hello gli attributi seguenti:</span><span class="sxs-lookup"><span data-stu-id="a48c4-134">In addition toothis property, attribute mappings do also support hello following attributes:</span></span>

- <span data-ttu-id="a48c4-135">**Attributo di origine** -attributo utente hello dal sistema di origine hello (ad esempio: Azure Active Directory).</span><span class="sxs-lookup"><span data-stu-id="a48c4-135">**Source attribute** - hello user attribute from hello source system (e.g.: Azure Active Directory).</span></span>
- <span data-ttu-id="a48c4-136">**Attributo di destinazione** : attributo utente hello nel sistema di destinazione hello (ad esempio: ServiceNow).</span><span class="sxs-lookup"><span data-stu-id="a48c4-136">**Target attribute** – hello user attribute in hello target system (e.g.: ServiceNow).</span></span>
- <span data-ttu-id="a48c4-137">**Associare gli oggetti utilizzando l'attributo** : questo mapping deve essere utilizzato o meno toouniquely identificare gli utenti tra i sistemi di origine e destinazione hello.</span><span class="sxs-lookup"><span data-stu-id="a48c4-137">**Match objects using this attribute** – Whether or not this mapping should be used toouniquely identify users between hello source and target systems.</span></span> <span data-ttu-id="a48c4-138">È in genere impostato su userPrincipalName hello o attributo mail in Azure AD, che è in genere eseguito il mapping di campo del nome utente tooa in un'applicazione di destinazione.</span><span class="sxs-lookup"><span data-stu-id="a48c4-138">This is typically set on hello userPrincipalName or mail attribute in Azure AD, which is typically mapped tooa username field in a target application.</span></span>
- <span data-ttu-id="a48c4-139">**Precedenza abbinamento**: è possibile impostare più attributi corrispondenti.</span><span class="sxs-lookup"><span data-stu-id="a48c4-139">**Matching precedence** – Multiple matching attributes can be set.</span></span> <span data-ttu-id="a48c4-140">Quando sono presenti più, essi vengono valutati in ordine di hello definito in questo campo.</span><span class="sxs-lookup"><span data-stu-id="a48c4-140">When there are multiple, they are evaluated in hello order defined by this field.</span></span> <span data-ttu-id="a48c4-141">Quando viene rilevata una corrispondenza la valutazione degli attributi corrispondenti termina.</span><span class="sxs-lookup"><span data-stu-id="a48c4-141">As soon as a match is found, no further matching attributes are evaluated.</span></span>
- <span data-ttu-id="a48c4-142">**Applica questo mapping**</span><span class="sxs-lookup"><span data-stu-id="a48c4-142">**Apply this mapping**</span></span>
    - <span data-ttu-id="a48c4-143">**Sempre**: applica il mapping sia all'azione di creazione che all'azione di aggiornamento dell'utente</span><span class="sxs-lookup"><span data-stu-id="a48c4-143">**Always** – Apply this mapping on both user creation and update actions</span></span>
    - <span data-ttu-id="a48c4-144">**Only during creation** (Solo durante la creazione): applica il mapping solo alle azioni di creazione dell'utente</span><span class="sxs-lookup"><span data-stu-id="a48c4-144">**Only during creation** - Apply this mapping only on user creation actions</span></span>


## <a name="what-you-should-know"></a><span data-ttu-id="a48c4-145">Informazioni utili</span><span class="sxs-lookup"><span data-stu-id="a48c4-145">What you should know</span></span>

<span data-ttu-id="a48c4-146">Microsoft Azure AD offre un'implementazione efficiente di un processo di sincronizzazione.</span><span class="sxs-lookup"><span data-stu-id="a48c4-146">Microsoft Azure AD provides an efficient implementation of a synchronization process.</span></span> <span data-ttu-id="a48c4-147">In un ambiente inizializzato, durante un ciclo di sincronizzazione vengono elaborati solo gli oggetti che richiedono aggiornamenti.</span><span class="sxs-lookup"><span data-stu-id="a48c4-147">In an initialized environment, only objects requiring updates are processed during a synchronization cycle.</span></span> <span data-ttu-id="a48c4-148">L'aggiornamento di mapping degli attributi ha un impatto sulle prestazioni di hello di un ciclo di sincronizzazione.</span><span class="sxs-lookup"><span data-stu-id="a48c4-148">Updating attribute mappings has an impact on hello performance of a synchronization cycle.</span></span> <span data-ttu-id="a48c4-149">Una configurazione di mapping di aggiornamento toohello attributo richiede rivalutate tutte toobe di oggetti gestiti.</span><span class="sxs-lookup"><span data-stu-id="a48c4-149">An update toohello attribute mapping configuration requires all managed objects toobe reevaluated.</span></span> <span data-ttu-id="a48c4-150">È un best practice tookeep hello numero consigliato di mapping degli attributi di modifiche consecutivi tooyour almeno.</span><span class="sxs-lookup"><span data-stu-id="a48c4-150">It is a recommended best practice tookeep hello number of consecutive changes tooyour attribute mappings at a minimum.</span></span>

## <a name="next-steps"></a><span data-ttu-id="a48c4-151">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="a48c4-151">Next steps</span></span>

* [<span data-ttu-id="a48c4-152">Indice di articoli per la gestione di applicazioni in Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="a48c4-152">Article Index for Application Management in Azure Active Directory</span></span>](active-directory-apps-index.md)
* [<span data-ttu-id="a48c4-153">Automatizzare tooSaaS utente Provisioning o Deprovisioning App</span><span class="sxs-lookup"><span data-stu-id="a48c4-153">Automate User Provisioning/Deprovisioning tooSaaS Apps</span></span>](active-directory-saas-app-provisioning.md)
* [<span data-ttu-id="a48c4-154">Scrittura di espressioni per i mapping degli attributi</span><span class="sxs-lookup"><span data-stu-id="a48c4-154">Writing Expressions for Attribute Mappings</span></span>](active-directory-saas-writing-expressions-for-attribute-mappings.md)
* [<span data-ttu-id="a48c4-155">Ambito dei filtri per il Provisioning utente</span><span class="sxs-lookup"><span data-stu-id="a48c4-155">Scoping Filters for User Provisioning</span></span>](active-directory-saas-scoping-filters.md)
* [<span data-ttu-id="a48c4-156">Utilizzando SCIM tooenable il provisioning automatico degli utenti e gruppi da Azure Active Directory tooapplications</span><span class="sxs-lookup"><span data-stu-id="a48c4-156">Using SCIM tooenable automatic provisioning of users and groups from Azure Active Directory tooapplications</span></span>](active-directory-scim-provisioning.md)
* [<span data-ttu-id="a48c4-157">Notifiche relative al provisioning dell'account</span><span class="sxs-lookup"><span data-stu-id="a48c4-157">Account Provisioning Notifications</span></span>](active-directory-saas-account-provisioning-notifications.md)
* [<span data-ttu-id="a48c4-158">Elenco di esercitazioni sulla tooIntegrate App SaaS</span><span class="sxs-lookup"><span data-stu-id="a48c4-158">List of Tutorials on How tooIntegrate SaaS Apps</span></span>](active-directory-saas-tutorial-list.md)

<!--Image references-->
[1]: ./media/active-directory-saas-customizing-attribute-mappings/ic765497.png
[2]: ./media/active-directory-saas-customizing-attribute-mappings/ic775419.png
[3]: ./media/active-directory-saas-customizing-attribute-mappings/ic775420.png
[4]: ./media/active-directory-saas-customizing-attribute-mappings/ic775421.png
[5]: ./media/active-directory-saas-customizing-attribute-mappings/21.png
[6]: ./media/active-directory-saas-customizing-attribute-mappings/22.png
[7]: ./media/active-directory-saas-customizing-attribute-mappings/23.png


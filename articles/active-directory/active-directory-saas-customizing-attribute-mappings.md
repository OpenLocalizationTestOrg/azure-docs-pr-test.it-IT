---
title: Personalizzazione dei mapping degli attributi di Azure AD | Documentazione Microsoft
description: "Informazioni sui mapping degli attributi per app SaaS in Azure Active Directory e su come è possibile modificarli in base alle esigenze aziendali."
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
ms.openlocfilehash: 6ca2fdc9c68ea0030d938eeaebd57aafa0e2790f
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="customizing-user-provisioning-attribute-mappings-for-saas-applications-in-azure-active-directory"></a><span data-ttu-id="089d4-103">Personalizzazione dei mapping degli attributi del provisioning degli utenti per le applicazioni SaaS in Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="089d4-103">Customizing User Provisioning Attribute Mappings for SaaS Applications in Azure Active Directory</span></span>
<span data-ttu-id="089d4-104">Microsoft Azure AD fornisce supporto per il provisioning degli utenti in applicazioni SaaS di terze parti, ad esempio Salesforce, Google Apps e altre.</span><span class="sxs-lookup"><span data-stu-id="089d4-104">Microsoft Azure AD provides support for user provisioning to third-party SaaS applications such as Salesforce, Google Apps and others.</span></span> <span data-ttu-id="089d4-105">Se è abilitato il provisioning degli utenti per un'applicazione SaaS di terze parti, il portale di gestione di Azure controlla i relativi valori di attributo tramite una configurazione denominata "mapping degli attributi".</span><span class="sxs-lookup"><span data-stu-id="089d4-105">If you have user provisioning for a third-party SaaS application enabled, the Azure Management Portal controls its attribute values in form of a configuration called “attribute mapping.”</span></span>

<span data-ttu-id="089d4-106">Esiste un set preconfigurato di mapping degli attributi tra gli oggetti utente di Azure AD e gli oggetti utente di ogni app SaaS.</span><span class="sxs-lookup"><span data-stu-id="089d4-106">There is a preconfigured set of attribute mappings between Azure AD user objects and each SaaS app’s user objects.</span></span> <span data-ttu-id="089d4-107">Alcune app gestiscono altri tipi di oggetti, quali Gruppi o Contatti.</span><span class="sxs-lookup"><span data-stu-id="089d4-107">Some apps manage other types of objects, such as Groups or Contacts.</span></span> <br> 
 <span data-ttu-id="089d4-108">È possibile personalizzare i mapping degli attributi predefiniti in base alle esigenze aziendali.</span><span class="sxs-lookup"><span data-stu-id="089d4-108">You can customize the default attribute mappings according to your business needs.</span></span> <span data-ttu-id="089d4-109">È infatti possibile modificare o eliminare i mapping degli attributi esistenti oppure crearne di nuovi.</span><span class="sxs-lookup"><span data-stu-id="089d4-109">This means, you can change or delete existing attribute mappings or create new attribute mappings.</span></span>

<span data-ttu-id="089d4-110">Nel portale di Azure AD è possibile accedere a questa funzionalità facendo clic su una configurazione **Mapping** in **Provisioning** nella sezione **Gestione** di un'**applicazione aziendale**.</span><span class="sxs-lookup"><span data-stu-id="089d4-110">In the Azure AD portal, you can access this feature by clicking a **Mappings** configuration under **Provisioning** in the **Manage** section of an **Enterprise application**.</span></span>


![Salesforce][5] 

<span data-ttu-id="089d4-112">Se si fa clic su una configurazione **Mapping** viene aperto il pannello **Mapping attributi** corrispondente.</span><span class="sxs-lookup"><span data-stu-id="089d4-112">Clicking a **Mappings** configuration, opens the related **Attribute Mapping** blade.</span></span>  
<span data-ttu-id="089d4-113">Alcuni mapping di attributi sono obbligatori per il corretto funzionamento di un'applicazione SaaS.</span><span class="sxs-lookup"><span data-stu-id="089d4-113">There are attribute mappings that are required by a SaaS application to function correctly.</span></span> <span data-ttu-id="089d4-114">Per gli attributi obbligatori la funzionalità **Elimina** non è disponibile.</span><span class="sxs-lookup"><span data-stu-id="089d4-114">For required attributes, the **Delete** feature is unavailable.</span></span>


![Salesforce][6]  

<span data-ttu-id="089d4-116">Nell'esempio riportato sopra si può notare che l'attributo **Username** di un oggetto gestito in Salesforce è popolato con il valore **userPrincipalName** dell'oggetto di Azure Active Directory collegato.</span><span class="sxs-lookup"><span data-stu-id="089d4-116">In the example above, you can see that the **Username** attribute of a managed object in Salesforce is populated with the **userPrincipalName** value of the linked Azure Active Directory Object.</span></span>

<span data-ttu-id="089d4-117">È possibile personalizzare i **Mapping degli attributi** esistenti facendo clic su un mapping.</span><span class="sxs-lookup"><span data-stu-id="089d4-117">You can customize existing **Attribute Mappings** by clicking a mapping.</span></span> <span data-ttu-id="089d4-118">Viene visualizzato il pannello **Modifica attributo**.</span><span class="sxs-lookup"><span data-stu-id="089d4-118">This opens the **Edit Attribute** blade.</span></span>

![Salesforce][7]  


  

## <a name="understanding-attribute-mapping-types"></a><span data-ttu-id="089d4-120">Informazioni sui tipi di mapping degli attributi</span><span class="sxs-lookup"><span data-stu-id="089d4-120">Understanding attribute mapping types</span></span>
<span data-ttu-id="089d4-121">I mapping degli attributi permettono di controllare il modo in cui gli attribuiti vengono popolati in un'applicazione SaaS di terze parti.</span><span class="sxs-lookup"><span data-stu-id="089d4-121">With attribute mappings, you control how attributes are populated in a third-party SaaS application.</span></span> <span data-ttu-id="089d4-122">Sono supportati quattro diversi tipi di mapping:</span><span class="sxs-lookup"><span data-stu-id="089d4-122">There are four different mapping types supported:</span></span>

* <span data-ttu-id="089d4-123">**Diretto:** l'attributo di destinazione viene popolato con il valore di un attributo dell'oggetto collegato in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="089d4-123">**Direct** – the target attribute is populated with the value of an attribute of the linked object in Azure AD.</span></span>
* <span data-ttu-id="089d4-124">**Costante:** l'attributo di destinazione viene popolato con una stringa specificata.</span><span class="sxs-lookup"><span data-stu-id="089d4-124">**Constant** – the target attribute is populated with a specific string you have specified.</span></span>
* <span data-ttu-id="089d4-125">**Espressione:** l'attributo di destinazione viene popolato in base al risultato di un'espressione simile a uno script.</span><span class="sxs-lookup"><span data-stu-id="089d4-125">**Expression** - the target attribute is populated based on the result of a script-like expression.</span></span> 
  <span data-ttu-id="089d4-126">Per altre informazioni, vedere [Scrittura di espressioni per il mapping degli attributi in Azure Active Directory](active-directory-saas-writing-expressions-for-attribute-mappings.md).</span><span class="sxs-lookup"><span data-stu-id="089d4-126">For more information, see [Writing Expressions for Attribute Mappings in Azure Active Directory](active-directory-saas-writing-expressions-for-attribute-mappings.md).</span></span>
* <span data-ttu-id="089d4-127">**Nessuno:** l'attributo di destinazione viene lasciato invariato.</span><span class="sxs-lookup"><span data-stu-id="089d4-127">**None** - the target attribute is left unmodified.</span></span> <span data-ttu-id="089d4-128">Se l'attributo di destinazione viene lasciato vuoto, viene popolato con il valore predefinito specificato.</span><span class="sxs-lookup"><span data-stu-id="089d4-128">However, if the target attribute is ever empty, it is populated with the Default value that you specify.</span></span>

<span data-ttu-id="089d4-129">Oltre a questi quattro tipi base di mapping, i mapping degli attributi personalizzati supportano il concetto di assegnazione di un valore **predefinito** facoltativo.</span><span class="sxs-lookup"><span data-stu-id="089d4-129">In addition to these four basic attribute mapping types, custom attribute mappings support the concept of an optional **default** value assignment.</span></span> <span data-ttu-id="089d4-130">L'assegnazione di un valore predefinito garantisce che un attributo di destinazione venga popolato con un valore nel caso in cui non sia presente un valore né in Azure AD, né nell'oggetto di destinazione.</span><span class="sxs-lookup"><span data-stu-id="089d4-130">The default value assignment ensures that a target attribute is populated with a value if there is neither a value in Azure AD nor on the target object.</span></span> <span data-ttu-id="089d4-131">Nella maggior parte delle configurazioni questo campo viene lasciato vuoto.</span><span class="sxs-lookup"><span data-stu-id="089d4-131">The most common configuration is to leave this blank.</span></span>


## <a name="understanding-attribute-mapping-properties"></a><span data-ttu-id="089d4-132">Informazioni sulle proprietà di mapping degli attributi</span><span class="sxs-lookup"><span data-stu-id="089d4-132">Understanding attribute mapping properties</span></span>

<span data-ttu-id="089d4-133">Nella sezione precedente è già stata presentata la proprietà del tipo di mapping degli attributi.</span><span class="sxs-lookup"><span data-stu-id="089d4-133">In the previous section, you have already been introduced to the attribute mapping type property.</span></span>
<span data-ttu-id="089d4-134">Oltre a questa proprietà i mapping degli attributi supportano i seguenti attributi:</span><span class="sxs-lookup"><span data-stu-id="089d4-134">In addition to this property, attribute mappings do also support the following attributes:</span></span>

- <span data-ttu-id="089d4-135">**Attributo di origine**: attributo utente del sistema di origine (ad esempio Azure Active Directory).</span><span class="sxs-lookup"><span data-stu-id="089d4-135">**Source attribute** - The user attribute from the source system (e.g.: Azure Active Directory).</span></span>
- <span data-ttu-id="089d4-136">**Attributo di destinazione**: attributo utente nel sistema di destinazione (ad esempio ServiceNow).</span><span class="sxs-lookup"><span data-stu-id="089d4-136">**Target attribute** – The user attribute in the target system (e.g.: ServiceNow).</span></span>
- <span data-ttu-id="089d4-137">**Abbina gli oggetti in base a questo attributo**: specifica se questo mapping va usato per l'identificazione univoca degli utenti tra il sistema di origine e il sistema di destinazione.</span><span class="sxs-lookup"><span data-stu-id="089d4-137">**Match objects using this attribute** – Whether or not this mapping should be used to uniquely identify users between the source and target systems.</span></span> <span data-ttu-id="089d4-138">Questa opzione è in genere impostata sull'attributo userPrincipalName o mail in Azure AD, che a sua volta è in genere mappato su un campo username in un'applicazione di destinazione.</span><span class="sxs-lookup"><span data-stu-id="089d4-138">This is typically set on the userPrincipalName or mail attribute in Azure AD, which is typically mapped to a username field in a target application.</span></span>
- <span data-ttu-id="089d4-139">**Precedenza abbinamento**: è possibile impostare più attributi corrispondenti.</span><span class="sxs-lookup"><span data-stu-id="089d4-139">**Matching precedence** – Multiple matching attributes can be set.</span></span> <span data-ttu-id="089d4-140">Se sono presenti più attributi, vengono valutati nell'ordine definito da questo campo.</span><span class="sxs-lookup"><span data-stu-id="089d4-140">When there are multiple, they are evaluated in the order defined by this field.</span></span> <span data-ttu-id="089d4-141">Quando viene rilevata una corrispondenza la valutazione degli attributi corrispondenti termina.</span><span class="sxs-lookup"><span data-stu-id="089d4-141">As soon as a match is found, no further matching attributes are evaluated.</span></span>
- <span data-ttu-id="089d4-142">**Applica questo mapping**</span><span class="sxs-lookup"><span data-stu-id="089d4-142">**Apply this mapping**</span></span>
    - <span data-ttu-id="089d4-143">**Sempre**: applica il mapping sia all'azione di creazione che all'azione di aggiornamento dell'utente</span><span class="sxs-lookup"><span data-stu-id="089d4-143">**Always** – Apply this mapping on both user creation and update actions</span></span>
    - <span data-ttu-id="089d4-144">**Only during creation** (Solo durante la creazione): applica il mapping solo alle azioni di creazione dell'utente</span><span class="sxs-lookup"><span data-stu-id="089d4-144">**Only during creation** - Apply this mapping only on user creation actions</span></span>


## <a name="what-you-should-know"></a><span data-ttu-id="089d4-145">Informazioni utili</span><span class="sxs-lookup"><span data-stu-id="089d4-145">What you should know</span></span>

<span data-ttu-id="089d4-146">Microsoft Azure AD offre un'implementazione efficiente di un processo di sincronizzazione.</span><span class="sxs-lookup"><span data-stu-id="089d4-146">Microsoft Azure AD provides an efficient implementation of a synchronization process.</span></span> <span data-ttu-id="089d4-147">In un ambiente inizializzato, durante un ciclo di sincronizzazione vengono elaborati solo gli oggetti che richiedono aggiornamenti.</span><span class="sxs-lookup"><span data-stu-id="089d4-147">In an initialized environment, only objects requiring updates are processed during a synchronization cycle.</span></span> <span data-ttu-id="089d4-148">L'aggiornamento dei mapping degli attributi influisce negativamente sulle prestazioni di un ciclo di sincronizzazione.</span><span class="sxs-lookup"><span data-stu-id="089d4-148">Updating attribute mappings has an impact on the performance of a synchronization cycle.</span></span> <span data-ttu-id="089d4-149">Un aggiornamento della configurazione del mapping degli attributi richiede la rivalutazione di tutti gli oggetti gestiti.</span><span class="sxs-lookup"><span data-stu-id="089d4-149">An update to the attribute mapping configuration requires all managed objects to be reevaluated.</span></span> <span data-ttu-id="089d4-150">È consigliabile ridurre al minimo il numero di modifiche consecutive ai mapping degli attributi.</span><span class="sxs-lookup"><span data-stu-id="089d4-150">It is a recommended best practice to keep the number of consecutive changes to your attribute mappings at a minimum.</span></span>

## <a name="next-steps"></a><span data-ttu-id="089d4-151">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="089d4-151">Next steps</span></span>

* [<span data-ttu-id="089d4-152">Indice di articoli per la gestione di applicazioni in Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="089d4-152">Article Index for Application Management in Azure Active Directory</span></span>](active-directory-apps-index.md)
* [<span data-ttu-id="089d4-153">Automatizzare il provisioning e il deprovisioning utenti in app SaaS</span><span class="sxs-lookup"><span data-stu-id="089d4-153">Automate User Provisioning/Deprovisioning to SaaS Apps</span></span>](active-directory-saas-app-provisioning.md)
* [<span data-ttu-id="089d4-154">Scrittura di espressioni per i mapping degli attributi</span><span class="sxs-lookup"><span data-stu-id="089d4-154">Writing Expressions for Attribute Mappings</span></span>](active-directory-saas-writing-expressions-for-attribute-mappings.md)
* [<span data-ttu-id="089d4-155">Ambito dei filtri per il Provisioning utente</span><span class="sxs-lookup"><span data-stu-id="089d4-155">Scoping Filters for User Provisioning</span></span>](active-directory-saas-scoping-filters.md)
* [<span data-ttu-id="089d4-156">Uso di SCIM per abilitare il provisioning automatico di utenti e gruppi da Azure Active Directory alle applicazioni</span><span class="sxs-lookup"><span data-stu-id="089d4-156">Using SCIM to enable automatic provisioning of users and groups from Azure Active Directory to applications</span></span>](active-directory-scim-provisioning.md)
* [<span data-ttu-id="089d4-157">Notifiche relative al provisioning dell'account</span><span class="sxs-lookup"><span data-stu-id="089d4-157">Account Provisioning Notifications</span></span>](active-directory-saas-account-provisioning-notifications.md)
* [<span data-ttu-id="089d4-158">Elenco di esercitazioni pratiche sulla procedura di integrazione delle applicazioni SaaS</span><span class="sxs-lookup"><span data-stu-id="089d4-158">List of Tutorials on How to Integrate SaaS Apps</span></span>](active-directory-saas-tutorial-list.md)

<!--Image references-->
[1]: ./media/active-directory-saas-customizing-attribute-mappings/ic765497.png
[2]: ./media/active-directory-saas-customizing-attribute-mappings/ic775419.png
[3]: ./media/active-directory-saas-customizing-attribute-mappings/ic775420.png
[4]: ./media/active-directory-saas-customizing-attribute-mappings/ic775421.png
[5]: ./media/active-directory-saas-customizing-attribute-mappings/21.png
[6]: ./media/active-directory-saas-customizing-attribute-mappings/22.png
[7]: ./media/active-directory-saas-customizing-attribute-mappings/23.png


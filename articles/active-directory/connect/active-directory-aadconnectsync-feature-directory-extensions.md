---
title: 'Servizio di sincronizzazione Azure AD Connect: estensioni della directory | Documentazione Microsoft'
description: "Questo argomento illustra la funzionalità relativa alle estensioni della directory in Azure AD Connect."
services: active-directory
documentationcenter: 
author: AndKjell
manager: femila
editor: 
ms.assetid: 995ee876-4415-4bb0-a258-cca3cbb02193
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 07/12/2017
ms.author: billmath
ms.openlocfilehash: 8ab9944437443a6d796345782f4f798aec96a0f6
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/03/2017
---
# <a name="azure-ad-connect-sync-directory-extensions"></a><span data-ttu-id="80a89-103">Servizio di sincronizzazione Azure AD Connect: estensioni della directory</span><span class="sxs-lookup"><span data-stu-id="80a89-103">Azure AD Connect sync: Directory extensions</span></span>
<span data-ttu-id="80a89-104">Le estensioni della directory consentono di estendere lo schema in Azure AD con attributi personalizzati da Active Directory in locale.</span><span class="sxs-lookup"><span data-stu-id="80a89-104">Directory extensions allows you to extend the schema in Azure AD with your own attributes from on-premises Active Directory.</span></span> <span data-ttu-id="80a89-105">Questa funzionalità consente di compilare app line-of-business che utilizzano attributi che continuano a essere gestiti in locale.</span><span class="sxs-lookup"><span data-stu-id="80a89-105">This feature allows you to build LOB apps consuming attributes you continue to manage on-premises.</span></span> <span data-ttu-id="80a89-106">Questi attributi possono essere utilizzati tramite le [estensioni della directory Azure AD Graph](https://msdn.microsoft.com/Library/Azure/Ad/Graph/howto/azure-ad-graph-api-directory-schema-extensions) o [Microsoft Graph](https://graph.microsoft.io/).</span><span class="sxs-lookup"><span data-stu-id="80a89-106">These attributes can be consumed through [Azure AD Graph directory extensions](https://msdn.microsoft.com/Library/Azure/Ad/Graph/howto/azure-ad-graph-api-directory-schema-extensions) or [Microsoft Graph](https://graph.microsoft.io/).</span></span> <span data-ttu-id="80a89-107">È possibile visualizzare gli attributi disponibili usando rispettivamente lo [strumento di esplorazione di Azure AD Graph](https://graphexplorer.cloudapp.net) e lo [strumento di esplorazione di Microsoft Graph](https://graphexplorer2.azurewebsites.net/).</span><span class="sxs-lookup"><span data-stu-id="80a89-107">You can see the attributes available using [Azure AD Graph explorer](https://graphexplorer.cloudapp.net) and [Microsoft Graph explorer](https://graphexplorer2.azurewebsites.net/) respectively.</span></span>

<span data-ttu-id="80a89-108">Attualmente nessun carico di lavoro di Office 365 utilizza questi attributi.</span><span class="sxs-lookup"><span data-stu-id="80a89-108">At present no Office 365 workload consumes these attributes.</span></span>

<span data-ttu-id="80a89-109">È possibile configurare gli attributi aggiuntivi da sincronizzare nel percorso delle impostazioni personalizzate nell'installazione guidata.</span><span class="sxs-lookup"><span data-stu-id="80a89-109">You configure which additional attributes you want to synchronize in the custom settings path in the installation wizard.</span></span>
<span data-ttu-id="80a89-110">![Procedura guidata per l'estensione dello schema](./media/active-directory-aadconnectsync-feature-directory-extensions/extension2.png)</span><span class="sxs-lookup"><span data-stu-id="80a89-110">![Schema Extension Wizard](./media/active-directory-aadconnectsync-feature-directory-extensions/extension2.png)</span></span>  
<span data-ttu-id="80a89-111">L'installazione mostra gli attributi seguenti, che sono candidati validi:</span><span class="sxs-lookup"><span data-stu-id="80a89-111">The installation shows the following attributes, which are valid candidates:</span></span>

* <span data-ttu-id="80a89-112">Tipi di oggetto utente e gruppo</span><span class="sxs-lookup"><span data-stu-id="80a89-112">User and Group object types</span></span>
* <span data-ttu-id="80a89-113">Attributi a valore singolo: String, Boolean, Integer, Binary</span><span class="sxs-lookup"><span data-stu-id="80a89-113">Single-valued attributes: String, Boolean, Integer, Binary</span></span>
* <span data-ttu-id="80a89-114">Attributi multivalore: String, Binary</span><span class="sxs-lookup"><span data-stu-id="80a89-114">Multi-valued attributes: String, Binary</span></span>

<span data-ttu-id="80a89-115">L'elenco di attributi viene letto dalla cache dello schema creata durante l'installazione di Azure AD Connect.</span><span class="sxs-lookup"><span data-stu-id="80a89-115">The list of attributes is read from the schema cache created during installation of Azure AD Connect.</span></span> <span data-ttu-id="80a89-116">Se è stato esteso lo schema di Active Directory con altri attributi, prima che questi nuovi attributi siano visibili è quindi necessario [aggiornare lo schema della directory](active-directory-aadconnectsync-installation-wizard.md#refresh-directory-schema) .</span><span class="sxs-lookup"><span data-stu-id="80a89-116">If you have extended the Active Directory schema with additional attributes, then the [schema must be refreshed](active-directory-aadconnectsync-installation-wizard.md#refresh-directory-schema) before these new attributes are visible.</span></span>

<span data-ttu-id="80a89-117">Un oggetto in Azure AD può avere al massimo 100 attributi delle estensioni della directory.</span><span class="sxs-lookup"><span data-stu-id="80a89-117">An object in Azure AD can have up to 100 directory extensions attributes.</span></span> <span data-ttu-id="80a89-118">La lunghezza massima consentita è di 250 caratteri.</span><span class="sxs-lookup"><span data-stu-id="80a89-118">The max length is 250 characters.</span></span> <span data-ttu-id="80a89-119">Se il valore di un attributo è più lungo, viene quindi troncato dal motore di sincronizzazione.</span><span class="sxs-lookup"><span data-stu-id="80a89-119">If an attribute value is longer, then it is truncated by the sync engine.</span></span>

<span data-ttu-id="80a89-120">Durante l'installazione di Azure AD Connect viene registrata un'applicazione in cui sono disponibili questi attributi.</span><span class="sxs-lookup"><span data-stu-id="80a89-120">During installation of Azure AD Connect, an application is registered where these attributes are available.</span></span> <span data-ttu-id="80a89-121">È possibile visualizzare questa applicazione nel portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="80a89-121">You can see this application in the Azure portal.</span></span>  
![App estensione dello schema](./media/active-directory-aadconnectsync-feature-directory-extensions/extension3new.png)

<span data-ttu-id="80a89-123">Questi attributi ora sono disponibili tramite Graph: </span><span class="sxs-lookup"><span data-stu-id="80a89-123">These attributes are now available through Graph:</span></span>  
![Grafico](./media/active-directory-aadconnectsync-feature-directory-extensions/extension4.png)

<span data-ttu-id="80a89-125">Gli attributi sono preceduti da extension\_{AppClientId}\_.</span><span class="sxs-lookup"><span data-stu-id="80a89-125">The attributes are prefixed with extension\_{AppClientId}\_.</span></span> <span data-ttu-id="80a89-126">AppClientId ha lo stesso valore per tutti gli attributi nel tenant di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="80a89-126">The AppClientId has the same value for all attributes in your Azure AD tenant.</span></span>

## <a name="next-steps"></a><span data-ttu-id="80a89-127">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="80a89-127">Next steps</span></span>
<span data-ttu-id="80a89-128">Ulteriori informazioni sulla configurazione della [sincronizzazione di Azure AD Connect](active-directory-aadconnectsync-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="80a89-128">Learn more about the [Azure AD Connect sync](active-directory-aadconnectsync-whatis.md) configuration.</span></span>

<span data-ttu-id="80a89-129">Ulteriori informazioni su [Integrazione delle identità locali con Azure Active Directory](active-directory-aadconnect.md).</span><span class="sxs-lookup"><span data-stu-id="80a89-129">Learn more about [Integrating your on-premises identities with Azure Active Directory](active-directory-aadconnect.md).</span></span>

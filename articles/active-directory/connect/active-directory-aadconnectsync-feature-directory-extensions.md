---
title: 'Servizio di sincronizzazione Azure AD Connect: estensioni della directory | Documentazione Microsoft'
description: "In questo argomento vengono descritte funzionalità estensioni di directory hello in Azure AD Connect."
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
ms.openlocfilehash: 31525ae914aa4d9e047ea1515b460a8311d5c815
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="azure-ad-connect-sync-directory-extensions"></a><span data-ttu-id="910a0-103">Servizio di sincronizzazione Azure AD Connect: estensioni della directory</span><span class="sxs-lookup"><span data-stu-id="910a0-103">Azure AD Connect sync: Directory extensions</span></span>
<span data-ttu-id="910a0-104">Le estensioni di directory consente di schema hello tooextend in Azure AD con gli attributi da Active Directory locale.</span><span class="sxs-lookup"><span data-stu-id="910a0-104">Directory extensions allows you tooextend hello schema in Azure AD with your own attributes from on-premises Active Directory.</span></span> <span data-ttu-id="910a0-105">Questa funzionalità permette di App LOB toobuild utilizzo di attributi continui toomanage locale.</span><span class="sxs-lookup"><span data-stu-id="910a0-105">This feature allows you toobuild LOB apps consuming attributes you continue toomanage on-premises.</span></span> <span data-ttu-id="910a0-106">Questi attributi possono essere utilizzati tramite le [estensioni della directory Azure AD Graph](https://msdn.microsoft.com/Library/Azure/Ad/Graph/howto/azure-ad-graph-api-directory-schema-extensions) o [Microsoft Graph](https://graph.microsoft.io/).</span><span class="sxs-lookup"><span data-stu-id="910a0-106">These attributes can be consumed through [Azure AD Graph directory extensions](https://msdn.microsoft.com/Library/Azure/Ad/Graph/howto/azure-ad-graph-api-directory-schema-extensions) or [Microsoft Graph](https://graph.microsoft.io/).</span></span> <span data-ttu-id="910a0-107">È possibile visualizzare gli attributi di hello disponibili tramite [Esplora Azure AD Graph](https://graphexplorer.cloudapp.net) e [Esplora Microsoft Graph](https://graphexplorer2.azurewebsites.net/) rispettivamente.</span><span class="sxs-lookup"><span data-stu-id="910a0-107">You can see hello attributes available using [Azure AD Graph explorer](https://graphexplorer.cloudapp.net) and [Microsoft Graph explorer](https://graphexplorer2.azurewebsites.net/) respectively.</span></span>

<span data-ttu-id="910a0-108">Attualmente nessun carico di lavoro di Office 365 utilizza questi attributi.</span><span class="sxs-lookup"><span data-stu-id="910a0-108">At present no Office 365 workload consumes these attributes.</span></span>

<span data-ttu-id="910a0-109">Configurare attributi aggiuntivi di cui si desidera toosynchronize nel percorso di impostazioni personalizzate hello nell'installazione guidata di hello.</span><span class="sxs-lookup"><span data-stu-id="910a0-109">You configure which additional attributes you want toosynchronize in hello custom settings path in hello installation wizard.</span></span>
<span data-ttu-id="910a0-110">![Procedura guidata per l'estensione dello schema](./media/active-directory-aadconnectsync-feature-directory-extensions/extension2.png)</span><span class="sxs-lookup"><span data-stu-id="910a0-110">![Schema Extension Wizard](./media/active-directory-aadconnectsync-feature-directory-extensions/extension2.png)</span></span>  
<span data-ttu-id="910a0-111">installazione di Hello Mostra hello gli attributi, che costituiscono candidati validi seguenti:</span><span class="sxs-lookup"><span data-stu-id="910a0-111">hello installation shows hello following attributes, which are valid candidates:</span></span>

* <span data-ttu-id="910a0-112">Tipi di oggetto utente e gruppo</span><span class="sxs-lookup"><span data-stu-id="910a0-112">User and Group object types</span></span>
* <span data-ttu-id="910a0-113">Attributi a valore singolo: String, Boolean, Integer, Binary</span><span class="sxs-lookup"><span data-stu-id="910a0-113">Single-valued attributes: String, Boolean, Integer, Binary</span></span>
* <span data-ttu-id="910a0-114">Attributi multivalore: String, Binary</span><span class="sxs-lookup"><span data-stu-id="910a0-114">Multi-valued attributes: String, Binary</span></span>

<span data-ttu-id="910a0-115">elenco di Hello di attributi viene letto dalla cache di schema hello creata durante l'installazione di Azure AD Connect.</span><span class="sxs-lookup"><span data-stu-id="910a0-115">hello list of attributes is read from hello schema cache created during installation of Azure AD Connect.</span></span> <span data-ttu-id="910a0-116">Se è stato esteso lo schema di Active Directory hello con attributi aggiuntivi, hello [schema deve essere aggiornato](active-directory-aadconnectsync-installation-wizard.md#refresh-directory-schema) prima che questi nuovi attributi sono visibili.</span><span class="sxs-lookup"><span data-stu-id="910a0-116">If you have extended hello Active Directory schema with additional attributes, then hello [schema must be refreshed](active-directory-aadconnectsync-installation-wizard.md#refresh-directory-schema) before these new attributes are visible.</span></span>

<span data-ttu-id="910a0-117">Un oggetto in Azure AD può avere gli attributi di estensioni di directory too100.</span><span class="sxs-lookup"><span data-stu-id="910a0-117">An object in Azure AD can have up too100 directory extensions attributes.</span></span> <span data-ttu-id="910a0-118">la lunghezza massima di Hello è 250 caratteri.</span><span class="sxs-lookup"><span data-stu-id="910a0-118">hello max length is 250 characters.</span></span> <span data-ttu-id="910a0-119">Se un valore di attributo è più lungo, viene troncato dal motore di sincronizzazione hello.</span><span class="sxs-lookup"><span data-stu-id="910a0-119">If an attribute value is longer, then it is truncated by hello sync engine.</span></span>

<span data-ttu-id="910a0-120">Durante l'installazione di Azure AD Connect viene registrata un'applicazione in cui sono disponibili questi attributi.</span><span class="sxs-lookup"><span data-stu-id="910a0-120">During installation of Azure AD Connect, an application is registered where these attributes are available.</span></span> <span data-ttu-id="910a0-121">È possibile visualizzare l'applicazione nel portale di Azure hello.</span><span class="sxs-lookup"><span data-stu-id="910a0-121">You can see this application in hello Azure portal.</span></span>  
![App estensione dello schema](./media/active-directory-aadconnectsync-feature-directory-extensions/extension3new.png)

<span data-ttu-id="910a0-123">Questi attributi ora sono disponibili tramite Graph: </span><span class="sxs-lookup"><span data-stu-id="910a0-123">These attributes are now available through Graph:</span></span>  
![Grafico](./media/active-directory-aadconnectsync-feature-directory-extensions/extension4.png)

<span data-ttu-id="910a0-125">gli attributi di Hello sono preceduti da estensione\_{AppClientId}\_.</span><span class="sxs-lookup"><span data-stu-id="910a0-125">hello attributes are prefixed with extension\_{AppClientId}\_.</span></span> <span data-ttu-id="910a0-126">Hello AppClientId ha hello stesso valore per tutti gli attributi nel tenant di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="910a0-126">hello AppClientId has hello same value for all attributes in your Azure AD tenant.</span></span>

## <a name="next-steps"></a><span data-ttu-id="910a0-127">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="910a0-127">Next steps</span></span>
<span data-ttu-id="910a0-128">Altre informazioni su hello [sincronizzazione di Azure AD Connect](active-directory-aadconnectsync-whatis.md) configurazione.</span><span class="sxs-lookup"><span data-stu-id="910a0-128">Learn more about hello [Azure AD Connect sync](active-directory-aadconnectsync-whatis.md) configuration.</span></span>

<span data-ttu-id="910a0-129">Altre informazioni su [Integrazione delle identità locali con Azure Active Directory](active-directory-aadconnect.md).</span><span class="sxs-lookup"><span data-stu-id="910a0-129">Learn more about [Integrating your on-premises identities with Azure Active Directory](active-directory-aadconnect.md).</span></span>

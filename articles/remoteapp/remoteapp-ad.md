---
title: aaaAzure AD + requisiti di Active Directory per Azure RemoteApp | Documenti Microsoft
description: Informazioni su come tooset backup toowork di Active Directory con Azure RemoteApp.
services: remoteapp
documentationcenter: 
author: msmbaldwin
manager: mbaldwin
ms.assetid: 66366b25-6012-45fa-a4f6-da0ddfe0b486
ms.service: remoteapp
ms.workload: compute
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/26/2017
ms.author: mbaldwin
ms.openlocfilehash: c1c4a7ad6fb96ec4d479fdc231f03d81b58b2b71
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="azure-ad--active-directory-requirements-for-azure-remoteapp"></a><span data-ttu-id="86241-103">Azure AD + requisiti di Active Directory per Azure RemoteApp</span><span class="sxs-lookup"><span data-stu-id="86241-103">Azure AD + Active Directory requirements for Azure RemoteApp</span></span>
> [!IMPORTANT]
> <span data-ttu-id="86241-104">Azure RemoteApp verrà sospeso a partire dal 31 agosto 2017.</span><span class="sxs-lookup"><span data-stu-id="86241-104">Azure RemoteApp is being discontinued on August 31, 2017.</span></span> <span data-ttu-id="86241-105">Hello lettura [annuncio](https://go.microsoft.com/fwlink/?linkid=821148) per informazioni dettagliate.</span><span class="sxs-lookup"><span data-stu-id="86241-105">Read hello [announcement](https://go.microsoft.com/fwlink/?linkid=821148) for details.</span></span>
> 
> 

<span data-ttu-id="86241-106">Per la raccolta ibrida di RemoteApp di Azure o per una raccolta di cloud che si desidera toofederate con Active Directory Connect, è necessario seguente hello toodo.</span><span class="sxs-lookup"><span data-stu-id="86241-106">For your Azure RemoteApp hybrid collection or for a cloud collection that you want toofederate using AD Connect, you need toodo hello following.</span></span>

### <a name="connect-azure-ad-and-active-directory"></a><span data-ttu-id="86241-107">Connettersi AD Azure e ad Active Directory</span><span class="sxs-lookup"><span data-stu-id="86241-107">Connect Azure AD and Active Directory</span></span>
<span data-ttu-id="86241-108">Se si desidera tooconnect tenant di Azure AD e gli ambienti di Active Directory locale, utilizzare AD Connect.</span><span class="sxs-lookup"><span data-stu-id="86241-108">If you want tooconnect your Azure AD tenant and your on-premises Active Directory environments, use AD Connect.</span></span> <span data-ttu-id="86241-109">Verranno visualizzate solo [4 clic](https://blogs.technet.microsoft.com/enterprisemobility/2014/08/04/connecting-ad-and-azure-ad-only-4-clicks-with-azure-ad-connect/) tooconnect hello due directory.</span><span class="sxs-lookup"><span data-stu-id="86241-109">It will take you only [4 clicks](https://blogs.technet.microsoft.com/enterprisemobility/2014/08/04/connecting-ad-and-azure-ad-only-4-clicks-with-azure-ad-connect/) tooconnect hello two directories.</span></span>

<span data-ttu-id="86241-110">Nota - la sincronizzazione delle Directory è necessaria per le raccolte ibride.</span><span class="sxs-lookup"><span data-stu-id="86241-110">Note - Directory synchronization is required for hybrid collections.</span></span>

### <a name="make-sure-your-domaincom-match"></a><span data-ttu-id="86241-111">Controllare la corrispondenza del valore "@domain.com"</span><span class="sxs-lookup"><span data-stu-id="86241-111">Make sure your "@domain.com" match</span></span>
<span data-ttu-id="86241-112">Prima di iniziare, verificare che tale hello UPN per il suffisso di hello corrispondenze foresta locale del dominio di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="86241-112">Before you get started, make sure that hello UPN for your on-premises forest matches hello suffix of your Azure AD domain.</span></span> 

<span data-ttu-id="86241-113">Dopo aver configurato il suffisso di dominio UPN hello in Azure AD, tutti gli utenti che accedono in Azure RemoteApp vengono registrati come "utente @<hello suffix you set up>."</span><span class="sxs-lookup"><span data-stu-id="86241-113">After you set up hello UPN domain suffix in Azure AD, all users logging into Azure RemoteApp will log in as "user@<hello suffix you set up>."</span></span> <span data-ttu-id="86241-114">Assicurarsi che gli utenti possono anche accedere con hello stesso user@suffix nel dominio locale hello.</span><span class="sxs-lookup"><span data-stu-id="86241-114">Make sure that users can also log in with hello same user@suffix into hello on-premises domain.</span></span> <span data-ttu-id="86241-115">In alcuni casi è possibile impostare un nome di dominio in Azure AD quando si specifica un suffisso di dominio diverso per hello utente in locale.</span><span class="sxs-lookup"><span data-stu-id="86241-115">In certain cases you can set up one domain name in Azure AD while specifying a different domain suffix for hello user on-prem.</span></span> <span data-ttu-id="86241-116">In questo caso, gli utenti sarà in grado di tooconnect tooany dominio computer o alle risorse tramite Azure RemoteApp.</span><span class="sxs-lookup"><span data-stu-id="86241-116">In this case, your users won't be able tooconnect tooany domain-joined computers or resources through Azure RemoteApp.</span></span>

<span data-ttu-id="86241-117">Se, ad esempio, impostare il suffisso di dominio UPN in AAD come contoso.com, ma alcuni utenti in locale o Active Directory sono configurati toolog con @contoso.uk, gli utenti non saranno hello raccolta ARA toocorrectly in grado di accedere.</span><span class="sxs-lookup"><span data-stu-id="86241-117">For example, if you set up your UPN domain suffix in AAD as contoso.com, but some users on premises/AD are configured toolog in with @contoso.uk, then those users will not be able toocorrectly log into hello ARA collection.</span></span> <span data-ttu-id="86241-118">Gli utenti che UPN in AAD e Active Directory deve essere uguale hello per le possibili toobe account di accesso di hello"</span><span class="sxs-lookup"><span data-stu-id="86241-118">Users UPN in AAD and AD must be hello same for hello login toobe possible”</span></span>

### <a name="create-objects-for-azure-remoteapp"></a><span data-ttu-id="86241-119">Creare gli oggetti per RemoteApp di Azure</span><span class="sxs-lookup"><span data-stu-id="86241-119">Create objects for Azure RemoteApp</span></span>
<span data-ttu-id="86241-120">È inoltre necessario hello toocreate seguendo gli oggetti di Active Directory locale:</span><span class="sxs-lookup"><span data-stu-id="86241-120">You also need toocreate hello following on-premises Active Directory objects:</span></span>

* <span data-ttu-id="86241-121">Un account servizio tooprovide accesso toodomain alle risorse per i programmi RemoteApp creando un join di dominio locale toohello punti finali di host sessione Desktop remoto.</span><span class="sxs-lookup"><span data-stu-id="86241-121">A service account tooprovide access toodomain resources for RemoteApp programs by joining RDSH end points toohello on-premises domain.</span></span>
* <span data-ttu-id="86241-122">Un'unità organizzativa (OU) toocontain RemoteApp gli oggetti macchina.</span><span class="sxs-lookup"><span data-stu-id="86241-122">An Organizational Unit (OU) toocontain RemoteApp machine objects.</span></span> <span data-ttu-id="86241-123">Utilizzo di hello unità Organizzativa è account hello tooisolate consigliata (ma non obbligatorio) e i criteri che verranno utilizzati con RemoteApp.</span><span class="sxs-lookup"><span data-stu-id="86241-123">Use of hello OU is recommended (but not required) tooisolate hello accounts and policies you will use with RemoteApp.</span></span>

<span data-ttu-id="86241-124">È necessario entrambi gli oggetti quando si crea la raccolta RemoteApp, pertanto è necessario che toodo questi passaggi prima.</span><span class="sxs-lookup"><span data-stu-id="86241-124">You need both of these objects when you create your RemoteApp collection, so be sure toodo these steps first.</span></span>


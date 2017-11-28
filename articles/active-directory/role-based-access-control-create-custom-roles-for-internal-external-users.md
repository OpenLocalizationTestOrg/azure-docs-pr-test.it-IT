---
title: ruoli di controllo di accesso basato sui ruoli personalizzati aaaCreate e assegnare toointernal e gli utenti esterni in Azure | Documenti Microsoft
description: Assegnare ruoli personalizzati di controllo degli accessi in base al ruolo creati con PowerShell e l'interfaccia della riga di comando per utenti interni ed esterni
services: active-directory
documentationcenter: 
author: andreicradu
manager: catadinu
editor: kgremban
ms.assetid: 
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 05/10/2017
ms.author: a-crradu
ms.openlocfilehash: 26793a66d6ca2f771338eed87d10ce2b3b431841
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
## <a name="intro-on-role-based-access-control"></a><span data-ttu-id="a08f9-103">Introduzione al controllo degli accessi in base al ruolo</span><span class="sxs-lookup"><span data-stu-id="a08f9-103">Intro on role-based access control</span></span>

<span data-ttu-id="a08f9-104">Controllo di accesso basato sui ruoli è una funzionalità di sola portale Azure consentendo ai proprietari di una sottoscrizione di hello tooassign ruoli granulari tooother gli utenti possono gestire gli ambiti di risorsa specifico nel proprio ambiente.</span><span class="sxs-lookup"><span data-stu-id="a08f9-104">Role-based access control is an Azure portal only feature allowing hello owners of a subscription tooassign granular roles tooother users who can manage specific resource scopes in their environment.</span></span>

<span data-ttu-id="a08f9-105">RBAC consente una migliore gestione della sicurezza per organizzazioni di grandi dimensioni e per piccole e medie imprese di utilizzo con collaboratori esterni, i fornitori o collaboratori esterni che devono accedere alle risorse di toospecific nell'ambiente di ma non necessariamente toohello intera infrastruttura o qualsiasi ambiti correlati alla fatturazione.</span><span class="sxs-lookup"><span data-stu-id="a08f9-105">RBAC allows better security management for large organizations and for SMBs working with external collaborators, vendors or freelancers which need access toospecific resources in your environment but not necessarily toohello entire infrastructure or any billing-related scopes.</span></span> <span data-ttu-id="a08f9-106">RBAC hello flessibilità di proprietario di una sottoscrizione di Azure gestita da account di amministratore hello (ruolo di amministratore del servizio a livello di sottoscrizione) e sono più utenti invitati toowork in hello ma senza stessa sottoscrizione qualsiasi amministrativi diritti per tale.</span><span class="sxs-lookup"><span data-stu-id="a08f9-106">RBAC allows hello flexibility of owning one Azure subscription managed by hello administrator account (service administrator role at a subscription level) and have multiple users invited toowork under hello same subscription but without any administrative rights for it.</span></span> <span data-ttu-id="a08f9-107">Da una gestione e la prospettiva di fatturazione, funzionalità RBAC hello dimostra toobe un'opzione efficiente time e della gestione per l'utilizzo di Azure in vari scenari.</span><span class="sxs-lookup"><span data-stu-id="a08f9-107">From a management and billing perspective, hello RBAC feature proves toobe a time and management efficient option for using Azure in various scenarios.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="a08f9-108">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="a08f9-108">Prerequisites</span></span>
<span data-ttu-id="a08f9-109">L'utilizzo nell'ambiente Azure hello RBAC richiede:</span><span class="sxs-lookup"><span data-stu-id="a08f9-109">Using RBAC in hello Azure environment requires:</span></span>

* <span data-ttu-id="a08f9-110">Un computer autonomo con sottoscrizione di Azure toohello utente assegnato come proprietario (ruolo di sottoscrizione)</span><span class="sxs-lookup"><span data-stu-id="a08f9-110">Having a standalone Azure subscription assigned toohello user as owner (subscription role)</span></span>
* <span data-ttu-id="a08f9-111">Ruolo di proprietario hello di hello sottoscrizione di Azure</span><span class="sxs-lookup"><span data-stu-id="a08f9-111">Have hello Owner role of hello Azure subscription</span></span>
* <span data-ttu-id="a08f9-112">Avere accesso toohello [portale di Azure](https://portal.azure.com)</span><span class="sxs-lookup"><span data-stu-id="a08f9-112">Have access toohello [Azure portal](https://portal.azure.com)</span></span>
* <span data-ttu-id="a08f9-113">Verificare che hello toohave seguendo i provider di risorse registrato per la sottoscrizione utente hello: **Microsoft**.</span><span class="sxs-lookup"><span data-stu-id="a08f9-113">Make sure toohave hello following Resource Providers registered for hello user subscription: **Microsoft.Authorization**.</span></span> <span data-ttu-id="a08f9-114">Per ulteriori informazioni su come tooregister hello i provider di risorse, vedere [i provider di gestione delle risorse, aree, le versioni dell'API e schemi](/azure-resource-manager/resource-manager-supported-services.md).</span><span class="sxs-lookup"><span data-stu-id="a08f9-114">For more information on how tooregister hello resource providers, see [Resource Manager providers, regions, API versions and schemas](/azure-resource-manager/resource-manager-supported-services.md).</span></span>

> [!NOTE]
> <span data-ttu-id="a08f9-115">Le sottoscrizioni di Office 365 o di licenze di Azure Active Directory (ad esempio: accesso tooAzure Active Directory) fornito da hello Office 365 portal non qualità usa tale controllo.</span><span class="sxs-lookup"><span data-stu-id="a08f9-115">Office 365 subscriptions or Azure Active Directory licenses (for example: Access tooAzure Active Directory) provisioned from hello O365 portal don't quality for using RBAC.</span></span>

## <a name="how-can-rbac-be-used"></a><span data-ttu-id="a08f9-116">Modalità d'uso del controllo degli accessi in base al ruolo</span><span class="sxs-lookup"><span data-stu-id="a08f9-116">How can RBAC be used</span></span>
<span data-ttu-id="a08f9-117">Il controllo degli accessi in base al ruolo può essere applicato in tre ambiti diversi in Azure.</span><span class="sxs-lookup"><span data-stu-id="a08f9-117">RBAC can be applied at three different scopes in Azure.</span></span> <span data-ttu-id="a08f9-118">Da hello massimo ambito toohello uno più basso, sono i seguenti:</span><span class="sxs-lookup"><span data-stu-id="a08f9-118">From hello highest scope toohello lowest one, they are as follows:</span></span>

* <span data-ttu-id="a08f9-119">Sottoscrizione (più alto)</span><span class="sxs-lookup"><span data-stu-id="a08f9-119">Subscription (highest)</span></span>
* <span data-ttu-id="a08f9-120">Gruppo di risorse</span><span class="sxs-lookup"><span data-stu-id="a08f9-120">Resource group</span></span>
* <span data-ttu-id="a08f9-121">Ambito di risorsa (hello più basso livello di accesso offerta autorizzazioni destinazione tooan ambito di singole risorse di Azure)</span><span class="sxs-lookup"><span data-stu-id="a08f9-121">Resource scope (hello lowest access level offering targeted permissions tooan individual Azure resource scope)</span></span>

## <a name="assign-rbac-roles-at-hello-subscription-scope"></a><span data-ttu-id="a08f9-122">Assegnare i ruoli RBAC ambito della sottoscrizione hello</span><span class="sxs-lookup"><span data-stu-id="a08f9-122">Assign RBAC roles at hello subscription scope</span></span>
<span data-ttu-id="a08f9-123">Ecco due esempi comuni di uso del controllo degli accessi in base al ruolo:</span><span class="sxs-lookup"><span data-stu-id="a08f9-123">There are two common examples when RBAC is used (but not limited to):</span></span>

* <span data-ttu-id="a08f9-124">Con utenti esterni di organizzazioni hello (non fa parte del tenant di Azure Active Directory dell'utente admin hello) invitato toomanage determinate risorse o la sottoscrizione intera hello</span><span class="sxs-lookup"><span data-stu-id="a08f9-124">Having external users from hello organizations (not part of hello admin user's Azure Active Directory tenant) invited toomanage certain resources or hello whole subscription</span></span>
* <span data-ttu-id="a08f9-125">Utilizzo con utenti all'interno dell'organizzazione hello (fanno parte del tenant di Azure Active Directory dell'utente hello) ma parte del team diversi o gruppi a cui è necessario un accesso granulare entrambi toohello intera sottoscrizione o gruppi di risorse toocertain o la risorsa gli ambiti in hello ambiente</span><span class="sxs-lookup"><span data-stu-id="a08f9-125">Working with users inside hello organization (they are part of hello user's Azure Active Directory tenant) but part of different teams or groups which need granular access either toohello whole subscription or toocertain resource groups or resource scopes in hello environment</span></span>

## <a name="grant-access-at-a-subscription-level-for-a-user-outside-of-azure-active-directory"></a><span data-ttu-id="a08f9-126">Concedere l'accesso a livello di sottoscrizione per un utente all'esterno di Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="a08f9-126">Grant access at a subscription level for a user outside of Azure Active Directory</span></span>
<span data-ttu-id="a08f9-127">Ruoli RBAC possono essere concessa solo da **proprietari** della sottoscrizione hello pertanto l'utente amministratore hello necessario accedere con un nome utente che dispone di questo ruolo pre-assegnato o ha creato hello sottoscrizione di Azure.</span><span class="sxs-lookup"><span data-stu-id="a08f9-127">RBAC roles can be granted only by **Owners** of hello subscription therefore hello admin user must be logged with a username which has this role pre-assigned or has created hello Azure subscription.</span></span>

<span data-ttu-id="a08f9-128">Dal portale di Azure hello, dopo aver Accedi come amministratore, selezionare "Sottoscrizioni" e scegliere hello desiderato uno.</span><span class="sxs-lookup"><span data-stu-id="a08f9-128">From hello Azure portal, after you sign-in as admin, select “Subscriptions” and chose hello desired one.</span></span>
<span data-ttu-id="a08f9-129">![Pannello di sottoscrizione nel portale di Azure](./media/role-based-access-control-create-custom-roles-for-internal-external-users/0.png) per impostazione predefinita, se l'utente amministratore hello ha acquistato hello sottoscrizione di Azure, utente hello viene visualizzata come **amministratore dell'Account**, questo corso ruolo sottoscrizione hello.</span><span class="sxs-lookup"><span data-stu-id="a08f9-129">![subscription blade in Azure portal](./media/role-based-access-control-create-custom-roles-for-internal-external-users/0.png) By default, if hello admin user has purchased hello Azure subscription, hello user will show up as **Account Admin**, this being hello subscription role.</span></span> <span data-ttu-id="a08f9-130">Per ulteriori informazioni sui ruoli di hello sottoscrizione di Azure, vedere [aggiungere o modificare ruoli di amministratore di Azure che gestiscono la sottoscrizione hello o servizi](/billing/billing-add-change-azure-subscription-administrator.md).</span><span class="sxs-lookup"><span data-stu-id="a08f9-130">For more details on hello Azure subscription roles, see [Add or change Azure administrator roles that manage hello subscription or services](/billing/billing-add-change-azure-subscription-administrator.md).</span></span>

<span data-ttu-id="a08f9-131">In questo esempio hello utente "alflanigan@outlook.com" è hello **proprietario** sottoscrizione in hello AAD di hello "Versione di valutazione gratuita" tenant "Default tenant di Azure".</span><span class="sxs-lookup"><span data-stu-id="a08f9-131">In this example, hello user "alflanigan@outlook.com" is hello **Owner** of hello "Free Trial" subscription in hello AAD tenant "Default tenant Azure".</span></span> <span data-ttu-id="a08f9-132">Poiché questo utente creatore hello di hello sottoscrizione di Azure con hello iniziale Account Microsoft "Outlook" (Account Microsoft = Outlook, in tempo reale e così via) nome di dominio hello predefinito per tutti gli altri utenti aggiunti in questo tenant sarà **"@alflaniganuoutlook.onmicrosoft.com"**.</span><span class="sxs-lookup"><span data-stu-id="a08f9-132">Since this user is hello creator of hello Azure subscription with hello initial Microsoft Account “Outlook” (Microsoft Account = Outlook, Live etc.) hello default domain name for all other users added in this tenant will be **"@alflaniganuoutlook.onmicrosoft.com"**.</span></span> <span data-ttu-id="a08f9-133">Per impostazione predefinita, sintassi hello del nuovo dominio hello è formata dalla combinazione di nome hello di nome utente e dominio dell'utente hello che ha creato il tenant hello e aggiunta estensione hello **". c o m"**.</span><span class="sxs-lookup"><span data-stu-id="a08f9-133">By design, hello syntax of hello new domain is formed by putting together hello username and domain name of hello user who created hello tenant and adding hello extension **".onmicrosoft.com"**.</span></span>
<span data-ttu-id="a08f9-134">Inoltre, gli utenti possono Accedi con un nome di dominio personalizzato nel tenant di hello dopo l'aggiunta e verifica per il nuovo tenant di hello.</span><span class="sxs-lookup"><span data-stu-id="a08f9-134">Furthermore, users can sign-in with a custom domain name in hello tenant after adding and verifying it for hello new tenant.</span></span> <span data-ttu-id="a08f9-135">Per ulteriori informazioni su come tooverify un nome di dominio personalizzato in un tenant di Azure Active Directory, vedere [aggiungere una directory tooyour nome di dominio personalizzato](/active-directory/active-directory-add-domain).</span><span class="sxs-lookup"><span data-stu-id="a08f9-135">For more details on how tooverify a custom domain name in an Azure Active Directory tenant, see [Add a custom domain name tooyour directory](/active-directory/active-directory-add-domain).</span></span>

<span data-ttu-id="a08f9-136">In questo esempio, la directory hello "tenant predefinito Azure" contiene solo gli utenti con il nome di dominio hello "@alflanigan.onmicrosoft.com".</span><span class="sxs-lookup"><span data-stu-id="a08f9-136">In this example, hello "Default tenant Azure" directory contains only users with hello domain name "@alflanigan.onmicrosoft.com".</span></span>

<span data-ttu-id="a08f9-137">Dopo aver selezionato la sottoscrizione hello, è necessario fare clic su utente admin hello **il controllo di accesso (IAM)** e quindi **aggiungere un nuovo ruolo**.</span><span class="sxs-lookup"><span data-stu-id="a08f9-137">After selecting hello subscription, hello admin user must click **Access Control (IAM)** and then **Add a new role**.</span></span>





![funzione IAM di controllo di accesso nel portale di Azure](./media/role-based-access-control-create-custom-roles-for-internal-external-users/1.png)





![aggiungere un nuovo utente nella funzione IAM di controllo di accesso nel portale di Azure](./media/role-based-access-control-create-custom-roles-for-internal-external-users/2.png)

<span data-ttu-id="a08f9-140">passaggio successivo Hello è tooselect hello ruolo toobe assegnato e utente hello che verrà assegnato al ruolo RBAC hello.</span><span class="sxs-lookup"><span data-stu-id="a08f9-140">hello next step is tooselect hello role toobe assigned and hello user whom hello RBAC role will be assigned to.</span></span> <span data-ttu-id="a08f9-141">In hello **ruolo** utente admin hello di menu a discesa Visualizza solo hello RBAC ruoli predefiniti che sono disponibili in Azure.</span><span class="sxs-lookup"><span data-stu-id="a08f9-141">In hello **Role** dropdown menu hello admin user sees only hello built-in RBAC roles which are available in Azure.</span></span> <span data-ttu-id="a08f9-142">Per altre descrizioni di ogni ruolo e dei relativi ambiti assegnabili, vedere [Ruoli predefiniti per il controllo degli accessi in base al ruolo di Azure](/active-directory/role-based-access-built-in-roles.md).</span><span class="sxs-lookup"><span data-stu-id="a08f9-142">For more detailed explanations of each role and their assignable scopes, see [Built-in roles for Azure Role-Based Access Control](/active-directory/role-based-access-built-in-roles.md).</span></span>

<span data-ttu-id="a08f9-143">l'utente amministratore Hello deve quindi l'indirizzo di posta elettronica hello tooadd dell'utente esterno hello.</span><span class="sxs-lookup"><span data-stu-id="a08f9-143">hello admin user then needs tooadd hello email address of hello external user.</span></span> <span data-ttu-id="a08f9-144">Hello previsto è il comportamento per hello utente esterno toonot compaiano in hello tenant esistente.</span><span class="sxs-lookup"><span data-stu-id="a08f9-144">hello expected behavior is for hello external user toonot show up in hello existing tenant.</span></span> <span data-ttu-id="a08f9-145">Dopo che è stato invitato l'utente esterno hello, saranno visibile in **sottoscrizioni > controllo di accesso (IAM)** con tutti gli utenti correnti hello che sono attualmente assegnati a un ruolo RBAC hello ambito della sottoscrizione.</span><span class="sxs-lookup"><span data-stu-id="a08f9-145">After hello external user has been invited, he will be visible under **Subscriptions > Access Control (IAM)** with all hello current users which are currently assigned an RBAC role at hello Subscription scope.</span></span>





![aggiungere le autorizzazioni toonew RBAC ruolo](./media/role-based-access-control-create-custom-roles-for-internal-external-users/3.png)





![elenco di ruoli di controllo degli accessi in base al ruolo a livello di sottoscrizione](./media/role-based-access-control-create-custom-roles-for-internal-external-users/4.png)

<span data-ttu-id="a08f9-148">utente Hello "chessercarlton@gmail.com" è stato invitato toobe un **proprietario** per hello sottoscrizione "Versione di valutazione gratuita".</span><span class="sxs-lookup"><span data-stu-id="a08f9-148">hello user "chessercarlton@gmail.com" has been invited toobe an **Owner** for hello “Free Trial” subscription.</span></span> <span data-ttu-id="a08f9-149">Dopo l'invio di invito hello utente esterno hello riceverà una conferma tramite posta elettronica con un collegamento di attivazione.</span><span class="sxs-lookup"><span data-stu-id="a08f9-149">After sending hello invitation, hello external user will receive an email confirmation with an activation link.</span></span>
<span data-ttu-id="a08f9-150">![Invito tramite posta elettronica per il ruolo di controllo degli accessi in base al ruolo](./media/role-based-access-control-create-custom-roles-for-internal-external-users/5.png)</span><span class="sxs-lookup"><span data-stu-id="a08f9-150">![email invitation for RBAC role](./media/role-based-access-control-create-custom-roles-for-internal-external-users/5.png)</span></span>

<span data-ttu-id="a08f9-151">Da organizzazione toohello esterno, hello nuovo utente non dispone gli attributi esistenti nella directory "Tenant di Azure predefinita" hello.</span><span class="sxs-lookup"><span data-stu-id="a08f9-151">Being external toohello organization, hello new user does not have any existing attributes in hello "Default tenant Azure" directory.</span></span> <span data-ttu-id="a08f9-152">Verranno creati previo consenso toobe registrate nella directory hello associata alla sottoscrizione hello che egli è stato assegnato un ruolo utente esterno hello.</span><span class="sxs-lookup"><span data-stu-id="a08f9-152">They will be created after hello external user has given consent toobe recorded in hello directory which is associated with hello subscription which he has been assigned a role to.</span></span>





![messaggio di invito tramite posta elettronica per il ruolo di controllo degli accessi in base al ruolo](./media/role-based-access-control-create-custom-roles-for-internal-external-users/6.png)

<span data-ttu-id="a08f9-154">utente esterno Hello Mostra in hello tenant di Azure Active Directory in come utente esterno e possono essere visualizzato nel portale di Azure hello e nel portale classico hello.</span><span class="sxs-lookup"><span data-stu-id="a08f9-154">hello external user shows in hello Azure Active Directory tenant from now on as external user and this can be viewed both in hello Azure portal and in hello classic portal.</span></span>





![pannello utenti azure active directory portale di Azure](./media/role-based-access-control-create-custom-roles-for-internal-external-users/7.png)





![pannello utenti azure active directory portale di Azure classico](./media/role-based-access-control-create-custom-roles-for-internal-external-users/8.png)

<span data-ttu-id="a08f9-157">In hello **utenti** vista in entrambi i portali hello perché gli utenti esterni può essere riconosciuto da:</span><span class="sxs-lookup"><span data-stu-id="a08f9-157">In hello **Users** view in both portals hello external users can be recognized by:</span></span>

* <span data-ttu-id="a08f9-158">tipo di icona diversa Hello in hello portale di Azure</span><span class="sxs-lookup"><span data-stu-id="a08f9-158">hello different icon type in hello Azure portal</span></span>
* <span data-ttu-id="a08f9-159">Hello diverso punti nel portale classico hello di determinazione dell'origine</span><span class="sxs-lookup"><span data-stu-id="a08f9-159">hello different sourcing point in hello classic portal</span></span>

<span data-ttu-id="a08f9-160">Tuttavia, la concessione **proprietario** o **collaboratore** accesso tooan esterno utente hello **sottoscrizione** ambito, non consentire hello accesso toohello amministrazione della directory dell'utente, a meno che non hello **amministratore globale** lo consente.</span><span class="sxs-lookup"><span data-stu-id="a08f9-160">However, granting **Owner** or **Contributor** access tooan external user at hello **Subscription** scope, does not allow hello access toohello admin user's directory, unless hello **Global Admin** allows it.</span></span> <span data-ttu-id="a08f9-161">In proprietà utente hello, hello **tipo utente** che presenta due parametri comuni, **membro** e **Guest** possono essere identificati.</span><span class="sxs-lookup"><span data-stu-id="a08f9-161">In hello user proprieties,  hello **User Type** which has two common parameters, **Member** and **Guest** can be identified.</span></span> <span data-ttu-id="a08f9-162">Un membro è un utente a cui viene registrato nella directory di hello mentre un utente guest è una directory toohello utente oltre agli inviti inviati da un'origine esterna.</span><span class="sxs-lookup"><span data-stu-id="a08f9-162">A member is a user which is registered in hello directory while a guest is a user invited toohello directory from an external source.</span></span> <span data-ttu-id="a08f9-163">Per altre informazioni, vedere [Procedura per aggiungere utenti di Collaborazione B2B ad Azure Active Directory da parte degli amministratori](/active-directory/active-directory-b2b-admin-add-users).</span><span class="sxs-lookup"><span data-stu-id="a08f9-163">For more information, see [How do Azure Active Directory admins add B2B collaboration users](/active-directory/active-directory-b2b-admin-add-users).</span></span>

> [!NOTE]
> <span data-ttu-id="a08f9-164">Assicurarsi che dopo aver immesso le credenziali di hello nel portale di hello, gli utenti esterni hello Seleziona directory corretta di hello toosign in.</span><span class="sxs-lookup"><span data-stu-id="a08f9-164">Make sure that after entering hello credentials in hello portal, hello external user selects hello correct directory toosign-in to.</span></span> <span data-ttu-id="a08f9-165">Hello stesso utente può dispone di accesso toomultiple directory e possono selezionare uno di essi facendo clic sul nome utente hello in hello lato superiore destro nel portale di Azure hello e quindi scegliere la directory appropriata hello dall'elenco a discesa hello.</span><span class="sxs-lookup"><span data-stu-id="a08f9-165">hello same user can have access toomultiple directories and can select either one of  them by clicking hello username in hello top right-hand side in hello Azure portal and then choose hello appropriate directory from hello dropdown list.</span></span>

<span data-ttu-id="a08f9-166">Pur essendo guest nella directory di hello, utente esterno hello possibile gestire tutte le risorse per hello sottoscrizione di Azure, ma Impossibile accedere alla directory hello.</span><span class="sxs-lookup"><span data-stu-id="a08f9-166">While being a guest in hello directory, hello external user can manage all resources for hello Azure subscription, but can't access hello directory.</span></span>





![portale di Azure active directory tooazure con restrizioni di accesso](./media/role-based-access-control-create-custom-roles-for-internal-external-users/9.png)

<span data-ttu-id="a08f9-168">Azure Active Directory e una sottoscrizione di Azure non hanno una relazione padre-figlio come quella che hanno altre risorse di Azure, ad esempio le macchine virtuali, le reti virtuali, le app Web, le risorse di archiviazione e così via, con una sottoscrizione di Azure.</span><span class="sxs-lookup"><span data-stu-id="a08f9-168">Azure Active Directory and an Azure subscription don't have a child-parent relation like other Azure resources (for example: virtual machines, virtual networks, web apps, storage etc.) have with an Azure subscription.</span></span> <span data-ttu-id="a08f9-169">Hello tutti quest'ultimo viene creato, gestiti e fatturati in una sottoscrizione di Azure, mentre una sottoscrizione di Azure viene utilizzato toomanage hello accesso tooan directory Azure.</span><span class="sxs-lookup"><span data-stu-id="a08f9-169">All hello latter is created, managed and billed under an Azure subscription while an Azure subscription is used toomanage hello access tooan Azure directory.</span></span> <span data-ttu-id="a08f9-170">Per ulteriori informazioni, vedere [sottoscrizione di Azure è tooAzure correlati AD](/active-directory/active-directory-how-subscriptions-associated-directory).</span><span class="sxs-lookup"><span data-stu-id="a08f9-170">For more details, see [How an Azure subscription is related tooAzure AD](/active-directory/active-directory-how-subscriptions-associated-directory).</span></span>

<span data-ttu-id="a08f9-171">Da tutti hello RBAC ruoli predefiniti, **proprietario** e **collaboratore** offrono l'accesso di gestione complete risorse tooall in ambiente hello, hello differenza corso che non è possibile creare un collaboratore e delete nuovo Ruoli RBAC.</span><span class="sxs-lookup"><span data-stu-id="a08f9-171">From all hello built-in RBAC roles, **Owner** and **Contributor** offer full management access tooall resources in hello environment, hello difference being that a Contributor can't create and delete new RBAC roles.</span></span> <span data-ttu-id="a08f9-172">come Hello altri ruoli predefiniti **collaboratore alla macchina virtuale** offrono l'accesso di gestione completa solo le risorse toohello indicate dal nome hello, indipendentemente dal hello **gruppo di risorse** la creazione in.</span><span class="sxs-lookup"><span data-stu-id="a08f9-172">hello other built-in roles like **Virtual Machine Contributor** offer full management access only toohello resources indicated by hello name, regardless of hello **Resource Group** they are being created into.</span></span>

<span data-ttu-id="a08f9-173">L'assegnazione hello ruolo incorporato e RBAC di **collaboratore alla macchina virtuale** a livello di sottoscrizione, significa che tale ruolo hello assegnati all'utente di hello:</span><span class="sxs-lookup"><span data-stu-id="a08f9-173">Assigning hello built-in RBAC role of **Virtual Machine Contributor** at a subscription level, means that hello user assigned hello role:</span></span>

* <span data-ttu-id="a08f9-174">Può visualizzare tutte le macchine virtuali indipendentemente dal loro distribuzione data e hello gruppi di risorse di che fanno parte</span><span class="sxs-lookup"><span data-stu-id="a08f9-174">Can view all virtual machines regardless their deployment date and hello resource groups they are part of</span></span>
* <span data-ttu-id="a08f9-175">Dispone di macchine virtuali di gestione complete accesso toohello nella sottoscrizione hello</span><span class="sxs-lookup"><span data-stu-id="a08f9-175">Has full management access toohello virtual machines in hello subscription</span></span>
* <span data-ttu-id="a08f9-176">Non è possibile visualizzare altri tipi di risorse nella sottoscrizione di hello</span><span class="sxs-lookup"><span data-stu-id="a08f9-176">Can't view any other resource types in hello subscription</span></span>
* <span data-ttu-id="a08f9-177">Non può applicare modifiche dalla prospettiva della fatturazione</span><span class="sxs-lookup"><span data-stu-id="a08f9-177">Can't operate any changes from a billing perspective</span></span>

> [!NOTE]
> <span data-ttu-id="a08f9-178">ACCESSI da un'unica funzionalità del portale Azure, non concede portale classico toohello di accesso.</span><span class="sxs-lookup"><span data-stu-id="a08f9-178">RBAC being an Azure portal only feature, it doesn't grant access toohello classic portal.</span></span>

## <a name="assign-a-built-in-rbac-role-tooan-external-user"></a><span data-ttu-id="a08f9-179">Assegnare un RBAC ruolo tooan esterno utente predefiniti</span><span class="sxs-lookup"><span data-stu-id="a08f9-179">Assign a built-in RBAC role tooan external user</span></span>
<span data-ttu-id="a08f9-180">Per uno scenario diverso in questo test, hello utente esterno "alflanigan@gmail.com" viene aggiunto come un **collaboratore alla macchina virtuale**.</span><span class="sxs-lookup"><span data-stu-id="a08f9-180">For a different scenario in this test, hello external user "alflanigan@gmail.com" is added as a **Virtual Machine Contributor**.</span></span>




![ruolo predefinito collaboratore macchina virtuale](./media/role-based-access-control-create-custom-roles-for-internal-external-users/11.png)

<span data-ttu-id="a08f9-182">un comportamento normale per questo utente esterno con questo ruolo incorporato Hello è toosee e gestire solo le macchine virtuali e i relativi adiacenti Gestione risorse solo le risorse necessarie durante la distribuzione.</span><span class="sxs-lookup"><span data-stu-id="a08f9-182">hello normal behavior for this external user with this built-in role is toosee and manage only virtual machines and their adjacent Resource Manager only resources necessary while deploying.</span></span> <span data-ttu-id="a08f9-183">Per impostazione predefinita, questi ruoli limitati consentono l'accesso solo le risorse corrispondenti tootheir create nel portale di Azure hello, indipendentemente dal fatto che alcune può ancora essere distribuito nel portale classico di hello (ad esempio: le macchine virtuali).</span><span class="sxs-lookup"><span data-stu-id="a08f9-183">By design, these limited roles offer access only tootheir correspondent resources created in hello Azure portal, regardless some can still be deployed in hello classic portal as well (for example: virtual machines).</span></span>





![Panoramica del ruolo Collaboratore macchina virtuale nel portale di Azure](./media/role-based-access-control-create-custom-roles-for-internal-external-users/12.png)

## <a name="grant-access-at-a-subscription-level-for-a-user-in-hello-same-directory"></a><span data-ttu-id="a08f9-185">Concedere accesso a livello di sottoscrizione per un utente in hello stessa directory</span><span class="sxs-lookup"><span data-stu-id="a08f9-185">Grant access at a subscription level for a user in hello same directory</span></span>
<span data-ttu-id="a08f9-186">flusso del processo Hello è identica tooadding un utente esterno, sia da hello prospettiva concessione hello RBAC ruolo di amministratore, nonché utente hello concessa ruolo toohello di accesso.</span><span class="sxs-lookup"><span data-stu-id="a08f9-186">hello process flow is identical tooadding an external user, both from hello admin perspective granting hello RBAC role as well as hello user being granted access toohello role.</span></span> <span data-ttu-id="a08f9-187">differenza Hello è che utente hello invitato non riceverà gli inviti di qualsiasi messaggio di posta elettronica come tutti gli ambiti di risorsa hello in sottoscrizione hello saranno disponibili nel dashboard di hello dopo l'accesso.</span><span class="sxs-lookup"><span data-stu-id="a08f9-187">hello difference here is that hello invited user will not receive any email invitations as all hello resource scopes within hello subscription will be available in hello dashboard after signing in.</span></span>

## <a name="assign-rbac-roles-at-hello-resource-group-scope"></a><span data-ttu-id="a08f9-188">Assegnare ruoli RBAC nell'ambito del gruppo di risorse hello</span><span class="sxs-lookup"><span data-stu-id="a08f9-188">Assign RBAC roles at hello resource group scope</span></span>
<span data-ttu-id="a08f9-189">L'assegnazione di un ruolo RBAC un **gruppo di risorse** ambito è un processo identico per l'assegnazione di ruolo hello a livello di sottoscrizione hello, per entrambi i tipi di utenti - esterni o interni (hello in parte stessa directory).</span><span class="sxs-lookup"><span data-stu-id="a08f9-189">Assigning an RBAC role at a **Resource Group** scope has an identical process for assigning hello role at hello subscription level, for both types of users - either external or internal (part of hello same directory).</span></span> <span data-ttu-id="a08f9-190">Hello gli utenti a cui vengono assegnati il ruolo di RBAC hello è toosee nel proprio ambiente solo il gruppo di risorse hello che sia stato assegnato l'accesso da hello **gruppi di risorse** icona in hello portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="a08f9-190">hello users which are assigned hello RBAC role is toosee in their environment only hello resource group they have been assigned access from hello **Resource Groups** icon in hello Azure portal.</span></span>

## <a name="assign-rbac-roles-at-hello-resource-scope"></a><span data-ttu-id="a08f9-191">Assegnare i ruoli RBAC ambito risorsa hello</span><span class="sxs-lookup"><span data-stu-id="a08f9-191">Assign RBAC roles at hello resource scope</span></span>
<span data-ttu-id="a08f9-192">L'assegnazione di un ruolo RBAC a un ambito di risorse in Azure è un processo per l'assegnazione di ruolo hello a livello di sottoscrizione hello o a livello di gruppo di risorse hello identico, seguente hello stesso flusso di lavoro per entrambi gli scenari.</span><span class="sxs-lookup"><span data-stu-id="a08f9-192">Assigning an RBAC role at a resource scope in Azure has an identical process for assigning hello role at hello subscription level or at hello resource group level, following hello same workflow for both scenarios.</span></span> <span data-ttu-id="a08f9-193">Nuovamente, gli utenti di hello che vengono assegnati hello RBAC ruolo possono visualizzare solo gli elementi hello che sono stati assegnati l'accesso a, entrambi in hello **tutte le risorse** scheda o direttamente nei loro dashboard.</span><span class="sxs-lookup"><span data-stu-id="a08f9-193">Again, hello users which are assigned hello RBAC role can see only hello items that they have been assigned access to, either in hello **All Resources** tab or directly in their dashboard.</span></span>

<span data-ttu-id="a08f9-194">Un aspetto importante per RBAC sia nell'ambito di gruppo di risorse o risorse è per directory corretta di hello utenti toomake toohello verificare toosign-in.</span><span class="sxs-lookup"><span data-stu-id="a08f9-194">An important aspect for RBAC both at resource group scope or resource scope is for hello users toomake sure toosign-in toohello correct directory.</span></span>





![accesso alla directory nel portale di Azure](./media/role-based-access-control-create-custom-roles-for-internal-external-users/13.png)

## <a name="assign-rbac-roles-for-an-azure-active-directory-group"></a><span data-ttu-id="a08f9-196">Assegnare ruoli di controllo degli accessi in base al ruolo per un gruppo di Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="a08f9-196">Assign RBAC roles for an Azure Active Directory group</span></span>
<span data-ttu-id="a08f9-197">Tutti gli scenari di hello utilizzando RBAC hello tre diversi ambiti privilegi hello Azure offerta di gestione, distribuzione e amministrazione delle varie risorse come un utente assegnato senza hello necessario della gestione di una sottoscrizione personale.</span><span class="sxs-lookup"><span data-stu-id="a08f9-197">All hello scenarios using RBAC at hello three different scopes in Azure offer hello privilege of managing, deploying and administering various resources as an assigned user without hello need of managing a personal subscription.</span></span> <span data-ttu-id="a08f9-198">Tutte le risorse di hello create più avanti dagli utenti di hello assegnato vengono fatturate in hello una sottoscrizione di Azure in cui gli utenti di hello hanno accesso al ruolo RBAC hello indipendentemente dal fatto che viene assegnato per una sottoscrizione, un gruppo di risorse o un ambito di risorsa.</span><span class="sxs-lookup"><span data-stu-id="a08f9-198">Regardless hello RBAC role is assigned for a subscription, resource group or resource scope, all hello resources created further on by hello assigned users are billed under hello one Azure subscription where hello users have access to.</span></span> <span data-ttu-id="a08f9-199">In questo modo, hello gli utenti che dispongono delle autorizzazioni di amministratore per la sottoscrizione Azure intera di fatturazione è una panoramica completa sul consumo di hello, indipendentemente dal fatto che che gestisce le risorse di hello.</span><span class="sxs-lookup"><span data-stu-id="a08f9-199">This way, hello users who have billing administrator permissions for that entire Azure subscription has a complete overview on hello consumption, regardless who is managing hello resources.</span></span>

<span data-ttu-id="a08f9-200">Per le organizzazioni più grandi, è possono applicare ruoli RBAC in hello allo stesso modo per gruppi di Azure Active Directory si considera di tale utente amministratore hello prospettiva hello vuole toogrant un accesso granulare hello per team o reparti interi, non singolarmente per ogni utente, pertanto possibilità di valutazione è molto tempo e la gestione efficiente.</span><span class="sxs-lookup"><span data-stu-id="a08f9-200">For larger organizations, RBAC roles can be applied in hello same way for Azure Active Directory groups considering hello perspective that hello admin user wants toogrant hello granular access for teams or entire departments, not individually for each user, thus considering it as an extremely time and management efficient option.</span></span> <span data-ttu-id="a08f9-201">tooillustrate questo esempio, hello **collaboratore** ruolo è stato aggiunto tooone dei gruppi di hello nel tenant di hello a livello di sottoscrizione hello.</span><span class="sxs-lookup"><span data-stu-id="a08f9-201">tooillustrate this example, hello **Contributor** role has been added tooone of hello groups in hello tenant at hello subscription level.</span></span>





![aggiungere il ruolo di controllo degli accessi in base al ruolo per i gruppi AAD](./media/role-based-access-control-create-custom-roles-for-internal-external-users/14.png)

<span data-ttu-id="a08f9-203">Questi gruppi sono gruppi di sicurezza di cui viene eseguito il provisioning e la gestione solo all'interno di Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="a08f9-203">These groups are security groups which are provisioned and managed only within Azure Active Directory.</span></span>

## <a name="create-a-custom-rbac-role-tooopen-support-requests-using-powershell"></a><span data-ttu-id="a08f9-204">Creare un supporto di tooopen ruolo RBAC personalizzato richieste tramite PowerShell</span><span class="sxs-lookup"><span data-stu-id="a08f9-204">Create a custom RBAC role tooopen support requests using PowerShell</span></span>
<span data-ttu-id="a08f9-205">ruoli RBAC incorporati Hello che sono disponibili in Azure verificare alcuni livelli di autorizzazione basate sulle risorse disponibili di hello in ambiente hello.</span><span class="sxs-lookup"><span data-stu-id="a08f9-205">hello built-in RBAC roles which are available in Azure ensure certain permission levels based on hello available resources in hello environment.</span></span> <span data-ttu-id="a08f9-206">Tuttavia, se nessuno di questi ruoli sono adatti alle esigenze dell'utente dell'amministratore di hello, è accesso toolimit di hello opzione ulteriormente creando ruoli RBAC personalizzati.</span><span class="sxs-lookup"><span data-stu-id="a08f9-206">However, if none of these roles suit hello admin user's needs, there is hello option toolimit access even more by creating custom RBAC roles.</span></span>

<span data-ttu-id="a08f9-207">Creazione di ruoli RBAC personalizzati richiede un ruolo incorporato e tootake, modificarlo e importarlo in ambiente hello.</span><span class="sxs-lookup"><span data-stu-id="a08f9-207">Creating custom RBAC roles requires tootake one built-in role, edit it and then import it back in hello environment.</span></span> <span data-ttu-id="a08f9-208">download di Hello e il caricamento del ruolo hello vengono gestiti tramite PowerShell o CLI.</span><span class="sxs-lookup"><span data-stu-id="a08f9-208">hello download and upload of hello role are managed using either PowerShell or CLI.</span></span>

<span data-ttu-id="a08f9-209">È importante toounderstand prerequisiti a hello di creazione di un ruolo personalizzato che possono concedere un accesso granulare a livello di sottoscrizione hello e consentono inoltre di hello invitato hello flessibilità di apertura di richieste di supporto.</span><span class="sxs-lookup"><span data-stu-id="a08f9-209">It is important toounderstand hello prerequisites of creating a custom role which can grant granular access at hello subscription level and also allow hello invited user hello flexibility of opening support requests.</span></span>

<span data-ttu-id="a08f9-210">Per questo ruolo predefiniti di esempio hello **lettore** che consente agli utenti accesso tooview tutte le risorse hello ambiti ma non tooedit li o crearne di nuovi è stato personalizzato tooallow hello utente hello possibile aprire le richieste di assistenza.</span><span class="sxs-lookup"><span data-stu-id="a08f9-210">For this example hello built-in role **Reader** which allows users access tooview all hello resource scopes but not tooedit them or create new ones has been customized tooallow hello user hello option of opening support requests.</span></span>

<span data-ttu-id="a08f9-211">Hello prima azione di esportazione hello **lettore** ruolo esigenze toobe completata in PowerShell è stato eseguito con autorizzazioni elevate come amministratore.</span><span class="sxs-lookup"><span data-stu-id="a08f9-211">hello first action of exporting hello **Reader** role needs toobe completed in PowerShell ran with elevated permissions as administrator.</span></span>

```
Login-AzureRMAccount

Get-AzureRMRoleDefinition -Name "Reader"

Get-AzureRMRoleDefinition -Name "Reader" | ConvertTo-Json | Out-File C:\rbacrole2.json

```





![Screenshot di PowerShell per il ruolo Lettore di controllo degli accessi in base al ruolo](./media/role-based-access-control-create-custom-roles-for-internal-external-users/15.png)

<span data-ttu-id="a08f9-213">È quindi necessario modello JSON di hello tooextract del ruolo hello.</span><span class="sxs-lookup"><span data-stu-id="a08f9-213">Then you need tooextract hello JSON template of hello role.</span></span>





![Modello JSON per il ruolo personalizzato Lettore di controllo degli accessi in base al ruolo](./media/role-based-access-control-create-custom-roles-for-internal-external-users/16.png)

<span data-ttu-id="a08f9-215">Un tipico ruolo di controllo degli accessi in base al ruolo è composto da tre sezioni principali, **Actions**, **NotActions** e **AssignableScopes**.</span><span class="sxs-lookup"><span data-stu-id="a08f9-215">A typical RBAC role is composed out of three main sections, **Actions**, **NotActions** and **AssignableScopes**.</span></span>

<span data-ttu-id="a08f9-216">In hello **azione** sezione sono elencati tutti hello operazioni consentite per questo ruolo.</span><span class="sxs-lookup"><span data-stu-id="a08f9-216">In hello **Action** section are listed all hello permitted operations for this role.</span></span> <span data-ttu-id="a08f9-217">È importante toounderstand che ogni azione viene assegnato da un provider di risorse.</span><span class="sxs-lookup"><span data-stu-id="a08f9-217">It's important toounderstand that each action is assigned from a resource provider.</span></span> <span data-ttu-id="a08f9-218">In questo caso, per la creazione di hello ticket di supporto **Microsoft. support** provider di risorse deve essere elencato.</span><span class="sxs-lookup"><span data-stu-id="a08f9-218">In this case, for creating support tickets hello **Microsoft.Support** resource provider must be listed.</span></span>

<span data-ttu-id="a08f9-219">toosee in grado di toobe tutti hello i provider di risorse disponibili e registrati nella sottoscrizione, è possibile utilizzare PowerShell.</span><span class="sxs-lookup"><span data-stu-id="a08f9-219">toobe able toosee all hello resource providers available and registered in your subscription, you can use PowerShell.</span></span>
```
Get-AzureRMResourceProvider

```
<span data-ttu-id="a08f9-220">Inoltre, è possibile controllare per hello tutti hello disponibile PowerShell cmdlet toomanage hello provider di risorse.</span><span class="sxs-lookup"><span data-stu-id="a08f9-220">Additionally, you can check for hello all hello available PowerShell cmdlets toomanage hello resource providers.</span></span>
    <span data-ttu-id="a08f9-221">![Screenshot di PowerShell per la gestione dei provider di risorse](./media/role-based-access-control-create-custom-roles-for-internal-external-users/17.png)</span><span class="sxs-lookup"><span data-stu-id="a08f9-221">![PowerShell screenshot for resource provider management](./media/role-based-access-control-create-custom-roles-for-internal-external-users/17.png)</span></span>

<span data-ttu-id="a08f9-222">toorestrict tutti hello azioni per un particolare ruolo RBAC resource provider sono elencati nella sezione hello **NotActions**.</span><span class="sxs-lookup"><span data-stu-id="a08f9-222">toorestrict all hello actions for a particular RBAC role, resource providers are listed under hello section **NotActions**.</span></span>
<span data-ttu-id="a08f9-223">Infine, è obbligatoria che tale ruolo RBAC hello contiene sottoscrizione esplicita hello ID in cui viene utilizzato.</span><span class="sxs-lookup"><span data-stu-id="a08f9-223">Last, it's mandatory that hello RBAC role contains hello explicit subscription IDs where it is used.</span></span> <span data-ttu-id="a08f9-224">Hello gli ID di sottoscrizione sono elencati sotto hello **AssignableScopes**, in caso contrario non sarà possibile ruolo hello tooimport nella sottoscrizione.</span><span class="sxs-lookup"><span data-stu-id="a08f9-224">hello subscription IDs are listed under hello **AssignableScopes**, otherwise you will not be allowed tooimport hello role in your subscription.</span></span>

<span data-ttu-id="a08f9-225">Dopo la creazione e personalizzazione hello RBAC ruolo, è necessario ambiente hello indietro importati toobe.</span><span class="sxs-lookup"><span data-stu-id="a08f9-225">After creating and customizing hello RBAC role, it needs toobe imported back hello environment.</span></span>

```
New-AzureRMRoleDefinition -InputFile "C:\rbacrole2.json"

```

<span data-ttu-id="a08f9-226">In questo esempio, nome personalizzato per questo ruolo RBAC il hello è "lettore supporto ticket livello di accesso" consentendo hello utente tooview tutti gli elementi nella sottoscrizione di hello e anche le richieste di assistenza tooopen.</span><span class="sxs-lookup"><span data-stu-id="a08f9-226">In this example, hello custom name for this RBAC role is "Reader support tickets access level" allowing hello user tooview everything in hello subscription and also tooopen support requests.</span></span>

> [!NOTE]
> <span data-ttu-id="a08f9-227">sono Hello solo due ruoli RBAC incorporati che consentono l'azione hello di apertura di richieste di supporto **proprietario** e **collaboratore**.</span><span class="sxs-lookup"><span data-stu-id="a08f9-227">hello only two built-in RBAC roles allowing hello action of opening of support requests are **Owner** and **Contributor**.</span></span> <span data-ttu-id="a08f9-228">Per un utente toobe in grado di tooopen le richieste di assistenza, egli deve essere assegnato un RBAC ruolo solo nell'ambito di sottoscrizione hello, poiché tutte le richieste di supporto vengono create in base a una sottoscrizione di Azure.</span><span class="sxs-lookup"><span data-stu-id="a08f9-228">For a user toobe able tooopen support requests, he must be assigned an RBAC role only at hello subscription scope, because all support requests are created based on an Azure subscription.</span></span>

<span data-ttu-id="a08f9-229">Questo nuovo ruolo personalizzato è stato assegnato l'utente tooan hello stessa directory.</span><span class="sxs-lookup"><span data-stu-id="a08f9-229">This new custom role has been assigned tooan user from hello same directory.</span></span>





![schermata del ruolo RBAC personalizzata importata nel portale di Azure hello](./media/role-based-access-control-create-custom-roles-for-internal-external-users/18.png)





![schermata di assegnazione personalizzato toouser ruolo RBAC importati in hello stessa directory](./media/role-based-access-control-create-custom-roles-for-internal-external-users/19.png)





![screenshot delle autorizzazioni per il ruolo personalizzato importato di controllo degli accessi in base al ruolo](./media/role-based-access-control-create-custom-roles-for-internal-external-users/20.png)

<span data-ttu-id="a08f9-233">esempio Hello è stata ulteriormente i limiti di hello tooemphasize dettagliate di questo ruolo RBAC personalizzato come indicato di seguito:</span><span class="sxs-lookup"><span data-stu-id="a08f9-233">hello example has been further detailed tooemphasize hello limits of this custom RBAC role as follows:</span></span>
* <span data-ttu-id="a08f9-234">Può creare nuove richieste di supporto</span><span class="sxs-lookup"><span data-stu-id="a08f9-234">Can create new support requests</span></span>
* <span data-ttu-id="a08f9-235">Non può creare nuovi ambiti di risorse, ad esempio la macchina virtuale</span><span class="sxs-lookup"><span data-stu-id="a08f9-235">Can't create new resource scopes (for example: virtual machine)</span></span>
* <span data-ttu-id="a08f9-236">Non può creare nuovi gruppi di risorse</span><span class="sxs-lookup"><span data-stu-id="a08f9-236">Can't create new resource groups</span></span>





![screenshot del ruolo personalizzato di controllo degli accessi in base al ruolo che crea richieste di supporto](./media/role-based-access-control-create-custom-roles-for-internal-external-users/21.png)





![schermata del ruolo RBAC personalizzato non è possibile toocreate macchine virtuali](./media/role-based-access-control-create-custom-roles-for-internal-external-users/22.png)





![schermata del ruolo RBAC personalizzato non è possibile toocreate RGs nuovo](./media/role-based-access-control-create-custom-roles-for-internal-external-users/23.png)

## <a name="create-a-custom-rbac-role-tooopen-support-requests-using-azure-cli"></a><span data-ttu-id="a08f9-240">Creare un supporto di tooopen ruolo RBAC personalizzato richieste tramite l'interfaccia CLI di Azure</span><span class="sxs-lookup"><span data-stu-id="a08f9-240">Create a custom RBAC role tooopen support requests using Azure CLI</span></span>
<span data-ttu-id="a08f9-241">In esecuzione su un Mac e senza accesso tooPowerShell, CLI di Azure è toogo modo hello.</span><span class="sxs-lookup"><span data-stu-id="a08f9-241">Running on a Mac and without having access tooPowerShell, Azure CLI is hello way toogo.</span></span>

<span data-ttu-id="a08f9-242">Hello passaggi toocreate un ruolo personalizzato sono hello stesso, con l'unica eccezione hello che usa CLI ruolo hello non è possibile scaricare un modello JSON, ma possono essere visualizzati in hello CLI.</span><span class="sxs-lookup"><span data-stu-id="a08f9-242">hello steps toocreate a custom role are hello same, with hello sole exception that using CLI hello role can't be downloaded in a JSON template, but it can be viewed in hello CLI.</span></span>

<span data-ttu-id="a08f9-243">Per questo esempio ho scelto ruolo incorporato e hello di **lettore Backup**.</span><span class="sxs-lookup"><span data-stu-id="a08f9-243">For this example I have chosen hello built-in role of **Backup Reader**.</span></span>

```

azure role show "backup reader" --json

```





![Screenshot dell'interfaccia della riga di comando del ruolo di lettore backup](./media/role-based-access-control-create-custom-roles-for-internal-external-users/24.png)

<span data-ttu-id="a08f9-245">Modifica ruolo hello in Visual Studio dopo la copia memorizzando hello in un modello JSON, hello **Microsoft. support** provider di risorse è stata aggiunta in hello **azioni** sezioni in modo che l'utente può aprire richieste di assistenza continuando toobe un lettore per gli insiemi di credenziali backup hello.</span><span class="sxs-lookup"><span data-stu-id="a08f9-245">Editing hello role in Visual Studio after copying hello proprieties in a JSON template, hello **Microsoft.Support** resource provider has been added in hello **Actions** sections so that this user can open support requests while continuing toobe a reader for hello backup vaults.</span></span> <span data-ttu-id="a08f9-246">Caso è necessario tooadd ID di sottoscrizione hello in cui verrà utilizzato questo ruolo in hello **AssignableScopes** sezione.</span><span class="sxs-lookup"><span data-stu-id="a08f9-246">Again it is necessary tooadd hello subscription ID where this role will be used in hello **AssignableScopes** section.</span></span>

```

azure role create --inputfile <path>

```





![Screenshot dell'interfaccia della riga di comando di importazione del ruolo personalizzato di controllo degli accessi in base al ruolo](./media/role-based-access-control-create-custom-roles-for-internal-external-users/25.png)

<span data-ttu-id="a08f9-248">nuovo ruolo Hello è ora disponibile nel portale di Azure hello e processo di tutte le assegnazioni di hello è hello stesso, come negli esempi precedenti hello.</span><span class="sxs-lookup"><span data-stu-id="a08f9-248">hello new role is now available in hello Azure portal and hello assignation process is hello same as in hello previous examples.</span></span>





![Screenshot del portale di Azure del ruolo personalizzato di controllo degli accessi in base al ruolo creato usando l'interfaccia della riga di comando 1.0](./media/role-based-access-control-create-custom-roles-for-internal-external-users/26.png)

<span data-ttu-id="a08f9-250">A partire da hello 2017 di compilazione più recente, hello Shell di Cloud di Azure è disponibile.</span><span class="sxs-lookup"><span data-stu-id="a08f9-250">As of hello latest Build 2017, hello Azure Cloud Shell is generally available.</span></span> <span data-ttu-id="a08f9-251">Shell Cloud Azure è un complemento tooIDE hello portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="a08f9-251">Azure Cloud Shell is a complement tooIDE and hello Azure Portal.</span></span> <span data-ttu-id="a08f9-252">Con questo servizio si ottiene una shell basata su browser autenticata e ospitata in Azure che è possibile usare al posto dell'interfaccia della riga di comando installata nel computer.</span><span class="sxs-lookup"><span data-stu-id="a08f9-252">With this service, you get a browser-based shell that is authenticated and hosted within Azure and you can use it instead of CLI installed on your machine.</span></span>





![Azure Cloud Shell](./media/role-based-access-control-create-custom-roles-for-internal-external-users/27.png)

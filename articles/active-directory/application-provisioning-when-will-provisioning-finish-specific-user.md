---
title: "Identificare se un utente specifico è in grado di accedere a un'applicazione | Microsoft Docs"
description: "Come identificare se un utente fondamentale è in grado di accedere a un'applicazione configurata per il provisioning utenti con Azure AD"
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
ms.openlocfilehash: fcefb31904cfb77022db0358e9feee6a0479db81
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/03/2017
---
# <a name="find-out-when-a-specific-user-will-be-able-to-access-an-application"></a><span data-ttu-id="07d02-103">Identificare se un utente specifico è in grado di accedere a un'applicazione</span><span class="sxs-lookup"><span data-stu-id="07d02-103">Find out when a specific user will be able to access an application</span></span>
<span data-ttu-id="07d02-104">Quando si usa il provisioning utenti automatico con un'applicazione, Azure AD esegue automaticamente il provisioning e aggiorna gli account utente in un'app in base ad alcuni elementi, ad esempio l'[assegnazione di utenti e gruppi](https://docs.microsoft.com/azure/active-directory/active-directory-coreapps-assign-user-azure-portal), a intervalli regolari pianificati, in genere ogni 10 minuti.</span><span class="sxs-lookup"><span data-stu-id="07d02-104">When using automatic user provisioning with an application, Azure AD automatically provision and update user accounts in an app based on things like [user and group assignment](https://docs.microsoft.com/azure/active-directory/active-directory-coreapps-assign-user-azure-portal) at a regularly scheduled time interval, typically every 10 minutes.</span></span>

## <a name="how-long-does-it-take"></a><span data-ttu-id="07d02-105">Quanto tempo occorre?</span><span class="sxs-lookup"><span data-stu-id="07d02-105">How long does it take?</span></span>

<span data-ttu-id="07d02-106">Il tempo necessario per eseguire il provisioning di un utente varia essenzialmente a seconda che sia stata eseguita o meno una sincronizzazione iniziale "completa".</span><span class="sxs-lookup"><span data-stu-id="07d02-106">The time it takes for a given user to be provisioned depends mainly on whether or not an initial “full” sync has already occurred.</span></span>

<span data-ttu-id="07d02-107">La prima sincronizzazione tra Azure AD e un'app può richiedere da 20 minuti a diverse ore, a seconda delle dimensioni della directory di Azure AD e del numero di utenti inclusi nell'ambito del provisioning.</span><span class="sxs-lookup"><span data-stu-id="07d02-107">The first sync between Azure AD and an app can take anywhere from 20 minutes to several hours, depending on the size of the Azure AD directory and the number of users in scope for provisioning.</span></span> 

<span data-ttu-id="07d02-108">Le sincronizzazioni successive a quella iniziale risultano più veloci (entro 10 minuti), poiché il servizio di provisioning archivia i limiti che rappresentano lo stato di entrambi i sistemi dopo la sincronizzazione iniziale, migliorando le prestazioni delle sincronizzazioni successive.</span><span class="sxs-lookup"><span data-stu-id="07d02-108">Subsequent syncs after the initial sync be faster (e.g. within 10 minutes), as the provisioning service stores watermarks that represent the state of both systems after the initial sync, improving performance of subsequent syncs.</span></span>

## <a name="how-to-check-the-status-of-a-user"></a><span data-ttu-id="07d02-109">Come controllare lo stato di un utente</span><span class="sxs-lookup"><span data-stu-id="07d02-109">How to check the status of a user</span></span>

<span data-ttu-id="07d02-110">Per visualizzare lo stato di provisioning per un utente selezionato, vedere i log di controllo in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="07d02-110">To see the provisioning status for a selected user, consult the Audit logs in Azure AD.</span></span>

<span data-ttu-id="07d02-111">I log di controllo di provisioning sono accessibili nella scheda **Azure Active Directory &gt; App aziendali &gt; \[Nome applicazione\] &gt; Log di controllo** del Portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="07d02-111">The provisioning audit logs can be accessed in the Azure portal, in the **Azure Active Directory &gt; Enterprise Apps &gt; \[Application Name\] &gt; Audit Logs** tab.</span></span> <span data-ttu-id="07d02-112">Filtrare i log nella categoria **Provisioning account** per visualizzare solo gli eventi di provisioning per l'app specifica.</span><span class="sxs-lookup"><span data-stu-id="07d02-112">Filter the logs on the **Account Provisioning** category to only see the provisioning events for that app.</span></span> <span data-ttu-id="07d02-113">È possibile cercare gli utenti in base all'ID di abbinamento configurato nel mapping degli attributi.</span><span class="sxs-lookup"><span data-stu-id="07d02-113">You can search for users based on the “matching ID” that was configured for them in the attribute mappings.</span></span> 

<span data-ttu-id="07d02-114">Ad esempio, se è stato configurato il nome dell'entità utente o l'indirizzo di posta elettronica come attributo di abbinamento sul lato Azure AD e l'utente non sottoposto a provisioning presenta un valore "audrey@contoso.com", cercare "audrey@contoso.com" nei log di controllo ed esaminare le voci restituite.</span><span class="sxs-lookup"><span data-stu-id="07d02-114">For example, if you configured the “user principal name” or “email address” as the matching attribute on the Azure AD side, and the user not being provisioning has a value of “audrey@contoso.com”, then search the audit logs for “audrey@contoso.com” and review then entries returned.</span></span>

<span data-ttu-id="07d02-115">I log di controllo di provisioning registrano tutte le operazioni eseguite dal servizio di provisioning, ad esempio:</span><span class="sxs-lookup"><span data-stu-id="07d02-115">The provisioning audit logs record all the operations performed by the provisioning service, including:</span></span>

* <span data-ttu-id="07d02-116">Esecuzione in Azure AD di query sugli utenti assegnati che rientrano nell'ambito del provisioning</span><span class="sxs-lookup"><span data-stu-id="07d02-116">Querying Azure AD for assigned users that are in scope for provisioning</span></span>
* <span data-ttu-id="07d02-117">Esecuzione nell'app di destinazione di query sull'esistenza di tali utenti</span><span class="sxs-lookup"><span data-stu-id="07d02-117">Querying the target app for the existence of those users</span></span>
* <span data-ttu-id="07d02-118">Confronto degli oggetti utente tra i sistemi</span><span class="sxs-lookup"><span data-stu-id="07d02-118">Comparing the user objects between the system</span></span>
* <span data-ttu-id="07d02-119">Aggiunta, aggiornamento o disabilitazione dell'account utente nel sistema di destinazione in base al confronto</span><span class="sxs-lookup"><span data-stu-id="07d02-119">Adding, updating, or disabling the user account in the target system based on the comparison</span></span>

## <a name="next-steps"></a><span data-ttu-id="07d02-120">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="07d02-120">Next steps</span></span>
<span data-ttu-id="07d02-121">[Automatizzare il provisioning e il deprovisioning utenti in applicazioni SaaS con Azure Active Directory](https://docs.microsoft.com/azure/active-directory/active-directory-saas-app-provisioning)''</span><span class="sxs-lookup"><span data-stu-id="07d02-121">[Automate User Provisioning and Deprovisioning to SaaS Applications with Azure Active Directory](https://docs.microsoft.com/azure/active-directory/active-directory-saas-app-provisioning)''</span></span>

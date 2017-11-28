---
title: "aaaWindows l'autenticazione e Server di autenticazione a più fattori di Azure | Documenti Microsoft"
description: Si tratta hello Azure multi-factor authentication pagina di supporto della distribuzione di autenticazione di Windows e il Server Azure multi-Factor Authentication.
services: multi-factor-authentication
documentationcenter: 
author: kgremban
manager: femila
ms.assetid: 19a4043f-c4ce-43c0-80e7-2548ee92cb74
ms.service: multi-factor-authentication
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 06/06/2017
ms.author: kgremban
ms.reviewer: yossib
ms.custom: it-pro
ms.openlocfilehash: 0fc38fd751966bf883d4eae7c48055988922af80
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="windows-authentication-and-azure-multi-factor-authentication-server"></a><span data-ttu-id="6e559-103">L'autenticazione di Windows e Azure il Server Multi-Factor Authentication</span><span class="sxs-lookup"><span data-stu-id="6e559-103">Windows Authentication and Azure Multi-Factor Authentication Server</span></span>
<span data-ttu-id="6e559-104">Utilizzare sezione autenticazione di Windows hello di hello del Server Azure multi-Factor Authentication tooenable e configurare l'autenticazione di Windows per le applicazioni.</span><span class="sxs-lookup"><span data-stu-id="6e559-104">Use hello Windows Authentication section of hello Azure Multi-Factor Authentication Server tooenable and configure Windows authentication for applications.</span></span> <span data-ttu-id="6e559-105">Prima di configurare l'autenticazione di Windows, tenere hello seguente elenco presente:</span><span class="sxs-lookup"><span data-stu-id="6e559-105">Before you set up Windows Authentication, keep hello following list in mind:</span></span>

* <span data-ttu-id="6e559-106">Dopo l'installazione, riavviare hello Azure multi-Factor Authentication per effetto di tootake di servizi Terminal.</span><span class="sxs-lookup"><span data-stu-id="6e559-106">After setup, reboot hello Azure Multi-Factor Authentication for Terminal Services tootake effect.</span></span>
* <span data-ttu-id="6e559-107">Se non sono nell'elenco di utenti hello 'Corrispondenza utente richiedono Azure multi-Factor Authentication' è selezionata, non sarà in grado di toolog macchina hello dopo il riavvio.</span><span class="sxs-lookup"><span data-stu-id="6e559-107">If ‘Require Azure Multi-Factor Authentication user match’ is checked and you are not in hello user list, you will not be able toolog into hello machine after reboot.</span></span>
* <span data-ttu-id="6e559-108">Indirizzi IP attendibili dipende se applicazione hello di fornire l'indirizzo IP con l'autenticazione di hello hello del client.</span><span class="sxs-lookup"><span data-stu-id="6e559-108">Trusted IPs is dependent on whether hello application can provide hello client IP with hello authentication.</span></span> <span data-ttu-id="6e559-109">Attualmente solo la funzione Servizi Terminal è supportata.</span><span class="sxs-lookup"><span data-stu-id="6e559-109">Currently only Terminal Services is supported.</span></span>  

> [!NOTE]
> <span data-ttu-id="6e559-110">Questa funzionalità non è supportato toosecure di servizi Terminal in Windows Server 2012 R2.</span><span class="sxs-lookup"><span data-stu-id="6e559-110">This feature is not supported toosecure Terminal Services on Windows Server 2012 R2.</span></span>

## <a name="toosecure-an-application-with-windows-authentication-use-hello-following-procedure"></a><span data-ttu-id="6e559-111">toosecure un'applicazione con l'autenticazione di Windows, utilizzare hello seguente procedura.</span><span class="sxs-lookup"><span data-stu-id="6e559-111">toosecure an application with Windows Authentication, use hello following procedure.</span></span>
1. <span data-ttu-id="6e559-112">In hello del Server Azure multi-Factor Authentication fare clic sull'icona di autenticazione di Windows hello.</span><span class="sxs-lookup"><span data-stu-id="6e559-112">In hello Azure Multi-Factor Authentication Server click hello Windows Authentication icon.</span></span>
   <span data-ttu-id="6e559-113">![Autenticazione di Windows](./media/multi-factor-authentication-get-started-server-windows/windowsauth.png)</span><span class="sxs-lookup"><span data-stu-id="6e559-113">![Windows Authentication](./media/multi-factor-authentication-get-started-server-windows/windowsauth.png)</span></span>
2. <span data-ttu-id="6e559-114">Controllare hello **abilitare l'autenticazione di Windows** casella di controllo.</span><span class="sxs-lookup"><span data-stu-id="6e559-114">Check hello **Enable Windows Authentication** checkbox.</span></span> <span data-ttu-id="6e559-115">Per impostazione predefinita, questa casella è deselezionata.</span><span class="sxs-lookup"><span data-stu-id="6e559-115">By default, this box is unchecked.</span></span>
3. <span data-ttu-id="6e559-116">scheda applicazioni Hello consente hello amministratore tooconfigure uno o più applicazioni per l'autenticazione di Windows.</span><span class="sxs-lookup"><span data-stu-id="6e559-116">hello Applications tab allows hello administrator tooconfigure one or more applications for Windows Authentication.</span></span>
4. <span data-ttu-id="6e559-117">Selezionare un server o l'applicazione: specificare se i server o l'applicazione hello è abilitata.</span><span class="sxs-lookup"><span data-stu-id="6e559-117">Select a server or application – specify whether hello server/application is enabled.</span></span> <span data-ttu-id="6e559-118">Fare clic su **OK**.</span><span class="sxs-lookup"><span data-stu-id="6e559-118">Click **OK**.</span></span>
5. <span data-ttu-id="6e559-119">Fare clic su **Aggiungi...**</span><span class="sxs-lookup"><span data-stu-id="6e559-119">Click **Add…**</span></span>
6. <span data-ttu-id="6e559-120">scheda indirizzi IP attendibili Hello consente tooskip Azure multi-Factor Authentication per le sessioni Windows provenienti da IP specifici.</span><span class="sxs-lookup"><span data-stu-id="6e559-120">hello Trusted IPs tab allows you tooskip Azure Multi-Factor Authentication for Windows sessions originating from specific IPs.</span></span> <span data-ttu-id="6e559-121">Ad esempio, se i dipendenti usano un'applicazione hello da office hello e da casa, si può decidere che non si desidera far squillare per Azure multi-Factor Authentication in ufficio hello loro telefoni.</span><span class="sxs-lookup"><span data-stu-id="6e559-121">For example, if employees use hello application from hello office and from home, you may decide you don't want their phones ringing for Azure Multi-Factor Authentication while at hello office.</span></span> <span data-ttu-id="6e559-122">A tale scopo, è necessario specificare subnet dell'ufficio hello come voce di indirizzi IP attendibili.</span><span class="sxs-lookup"><span data-stu-id="6e559-122">For this, you would specify hello office subnet as Trusted IPs entry.</span></span>
7. <span data-ttu-id="6e559-123">Fare clic su **Aggiungi...**</span><span class="sxs-lookup"><span data-stu-id="6e559-123">Click **Add…**</span></span>
8. <span data-ttu-id="6e559-124">Selezionare **IP singolo** se si desidera tooskip un singolo indirizzo IP.</span><span class="sxs-lookup"><span data-stu-id="6e559-124">Select **Single IP** if you would like tooskip a single IP address.</span></span>
9. <span data-ttu-id="6e559-125">Selezionare **intervallo IP** se si desidera tooskip un intero intervallo IP.</span><span class="sxs-lookup"><span data-stu-id="6e559-125">Select **IP Range** if you would like tooskip an entire IP range.</span></span> <span data-ttu-id="6e559-126">Esempio: 10.63.193.1-10.63.193.100.</span><span class="sxs-lookup"><span data-stu-id="6e559-126">Example 10.63.193.1-10.63.193.100.</span></span>
10. <span data-ttu-id="6e559-127">Selezionare **Subnet** se si desidera toospecify un intervallo di indirizzi IP utilizzando la notazione di subnet.</span><span class="sxs-lookup"><span data-stu-id="6e559-127">Select **Subnet** if you would like toospecify a range of IPs using subnet notation.</span></span> <span data-ttu-id="6e559-128">Immettere l'IP iniziale della subnet hello e selezionare hello netmask appropriata dall'elenco a discesa hello.</span><span class="sxs-lookup"><span data-stu-id="6e559-128">Enter hello subnet's starting IP and pick hello appropriate netmask from hello drop-down list.</span></span>
11. <span data-ttu-id="6e559-129">Fare clic su **OK**.</span><span class="sxs-lookup"><span data-stu-id="6e559-129">Click **OK**.</span></span>

## <a name="next-steps"></a><span data-ttu-id="6e559-130">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="6e559-130">Next steps</span></span>

- [<span data-ttu-id="6e559-131">Configurare dispositivi VPN di terze parti per il server Azure MFA</span><span class="sxs-lookup"><span data-stu-id="6e559-131">Configure third-party VPN appliances for Azure MFA Server</span></span>](multi-factor-authentication-advanced-vpn-configurations.md)

- [<span data-ttu-id="6e559-132">Aumentare l'infrastruttura di autenticazione esistente con hello estensione dei criteri di rete per Azure MFA</span><span class="sxs-lookup"><span data-stu-id="6e559-132">Augment your existing authentication infrastructure with hello NPS extension for Azure MFA</span></span>](multi-factor-authentication-nps-extension.md)

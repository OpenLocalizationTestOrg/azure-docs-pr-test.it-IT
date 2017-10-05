---
title: Autenticazione di Windows e server Azure MFA | Documentazione Microsoft
description: "Questa è la pagina di autenticazione a più fattori di Azure che sarà utile per distribuire l'autenticazione di Windows e Server Azure Multi-Factor Authentication."
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
ms.openlocfilehash: 7e6384ea8fea686b5cad1a3bc3007252b9cfcd65
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="windows-authentication-and-azure-multi-factor-authentication-server"></a><span data-ttu-id="9185f-103">L'autenticazione di Windows e Azure il Server Multi-Factor Authentication</span><span class="sxs-lookup"><span data-stu-id="9185f-103">Windows Authentication and Azure Multi-Factor Authentication Server</span></span>
<span data-ttu-id="9185f-104">Usare la sezione Autenticazione di Windows del server Azure Multi-Factor Authentication per abilitare e configurare l'autenticazione di Windows per le applicazioni.</span><span class="sxs-lookup"><span data-stu-id="9185f-104">Use the Windows Authentication section of the Azure Multi-Factor Authentication Server to enable and configure Windows authentication for applications.</span></span> <span data-ttu-id="9185f-105">Prima di configurare l'autenticazione di Windows, tenere presente quanto segue:</span><span class="sxs-lookup"><span data-stu-id="9185f-105">Before you set up Windows Authentication, keep the following list in mind:</span></span>

* <span data-ttu-id="9185f-106">Dopo aver eseguito la configurazione, riavviare Azure Multi-Factor Authentication per rendere effettivo Servizi terminal.</span><span class="sxs-lookup"><span data-stu-id="9185f-106">After setup, reboot the Azure Multi-Factor Authentication for Terminal Services to take effect.</span></span>
* <span data-ttu-id="9185f-107">Se "Richiedere corrispondenza utente Azure Multi-Factor Authentication" è selezionata e non si è nell'elenco degli utenti, non sarà possibile accedere alla macchina dopo il riavvio.</span><span class="sxs-lookup"><span data-stu-id="9185f-107">If ‘Require Azure Multi-Factor Authentication user match’ is checked and you are not in the user list, you will not be able to log into the machine after reboot.</span></span>
* <span data-ttu-id="9185f-108">La funzione IP attendibili dipende da se l'applicazione può fornire l'IP del client con l'autenticazione.</span><span class="sxs-lookup"><span data-stu-id="9185f-108">Trusted IPs is dependent on whether the application can provide the client IP with the authentication.</span></span> <span data-ttu-id="9185f-109">Attualmente solo la funzione Servizi Terminal è supportata.</span><span class="sxs-lookup"><span data-stu-id="9185f-109">Currently only Terminal Services is supported.</span></span>  

> [!NOTE]
> <span data-ttu-id="9185f-110">Questa funzionalità non è supportata per proteggere Servizi Terminal in Windows Server 2012 R2.</span><span class="sxs-lookup"><span data-stu-id="9185f-110">This feature is not supported to secure Terminal Services on Windows Server 2012 R2.</span></span>

## <a name="to-secure-an-application-with-windows-authentication-use-the-following-procedure"></a><span data-ttu-id="9185f-111">Per proteggere un'applicazione con l'autenticazione di Windows, utilizzare la procedura seguente.</span><span class="sxs-lookup"><span data-stu-id="9185f-111">To secure an application with Windows Authentication, use the following procedure.</span></span>
1. <span data-ttu-id="9185f-112">Nel server Microsoft Azure Multi-Factor Authentication fare clic sull'icona Autenticazione di Windows.</span><span class="sxs-lookup"><span data-stu-id="9185f-112">In the Azure Multi-Factor Authentication Server click the Windows Authentication icon.</span></span>
   <span data-ttu-id="9185f-113">![Autenticazione di Windows](./media/multi-factor-authentication-get-started-server-windows/windowsauth.png)</span><span class="sxs-lookup"><span data-stu-id="9185f-113">![Windows Authentication](./media/multi-factor-authentication-get-started-server-windows/windowsauth.png)</span></span>
2. <span data-ttu-id="9185f-114">Selezionare la casella di controllo **Abilita autenticazione di Windows**.</span><span class="sxs-lookup"><span data-stu-id="9185f-114">Check the **Enable Windows Authentication** checkbox.</span></span> <span data-ttu-id="9185f-115">Per impostazione predefinita, questa casella è deselezionata.</span><span class="sxs-lookup"><span data-stu-id="9185f-115">By default, this box is unchecked.</span></span>
3. <span data-ttu-id="9185f-116">La scheda applicazioni consente all'amministratore di configurare uno o più applicazioni per l'autenticazione di Windows.</span><span class="sxs-lookup"><span data-stu-id="9185f-116">The Applications tab allows the administrator to configure one or more applications for Windows Authentication.</span></span>
4. <span data-ttu-id="9185f-117">Selezionare un server o un'applicazione, specificare se il server/applicazione è abilitato.</span><span class="sxs-lookup"><span data-stu-id="9185f-117">Select a server or application – specify whether the server/application is enabled.</span></span> <span data-ttu-id="9185f-118">Fare clic su **OK**.</span><span class="sxs-lookup"><span data-stu-id="9185f-118">Click **OK**.</span></span>
5. <span data-ttu-id="9185f-119">Fare clic su **Aggiungi...**</span><span class="sxs-lookup"><span data-stu-id="9185f-119">Click **Add…**</span></span>
6. <span data-ttu-id="9185f-120">La scheda di ID attendibili consente di ignorare Azure Multi-Factor Authentication per le sessioni Windows provenienti da IP specifici.</span><span class="sxs-lookup"><span data-stu-id="9185f-120">The Trusted IPs tab allows you to skip Azure Multi-Factor Authentication for Windows sessions originating from specific IPs.</span></span> <span data-ttu-id="9185f-121">Ad esempio, se i dipendenti usano l'applicazione dall'ufficio e da casa, è possibile decidere di non volere che i loro telefoni squillino per Azure Multi-Factor Authentication in ufficio.</span><span class="sxs-lookup"><span data-stu-id="9185f-121">For example, if employees use the application from the office and from home, you may decide you don't want their phones ringing for Azure Multi-Factor Authentication while at the office.</span></span> <span data-ttu-id="9185f-122">A tale scopo, specificare la subnet dell'ufficio come voce di ID attendibili.</span><span class="sxs-lookup"><span data-stu-id="9185f-122">For this, you would specify the office subnet as Trusted IPs entry.</span></span>
7. <span data-ttu-id="9185f-123">Fare clic su **Aggiungi...**</span><span class="sxs-lookup"><span data-stu-id="9185f-123">Click **Add…**</span></span>
8. <span data-ttu-id="9185f-124">Selezionare **IP singolo** se si vuole ignorare un singolo indirizzo IP.</span><span class="sxs-lookup"><span data-stu-id="9185f-124">Select **Single IP** if you would like to skip a single IP address.</span></span>
9. <span data-ttu-id="9185f-125">Selezionare **Intervallo IP** se si vuole ignorare un intero intervallo di indirizzi IP.</span><span class="sxs-lookup"><span data-stu-id="9185f-125">Select **IP Range** if you would like to skip an entire IP range.</span></span> <span data-ttu-id="9185f-126">Esempio: 10.63.193.1-10.63.193.100.</span><span class="sxs-lookup"><span data-stu-id="9185f-126">Example 10.63.193.1-10.63.193.100.</span></span>
10. <span data-ttu-id="9185f-127">Selezionare **Subnet** per specificare un intervallo di indirizzi IP usando la notazione subnet.</span><span class="sxs-lookup"><span data-stu-id="9185f-127">Select **Subnet** if you would like to specify a range of IPs using subnet notation.</span></span> <span data-ttu-id="9185f-128">Immettere l’IP iniziale della subnet e scegliere la mask appropriata dall'elenco a discesa.</span><span class="sxs-lookup"><span data-stu-id="9185f-128">Enter the subnet's starting IP and pick the appropriate netmask from the drop-down list.</span></span>
11. <span data-ttu-id="9185f-129">Fare clic su **OK**.</span><span class="sxs-lookup"><span data-stu-id="9185f-129">Click **OK**.</span></span>

## <a name="next-steps"></a><span data-ttu-id="9185f-130">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="9185f-130">Next steps</span></span>

- [<span data-ttu-id="9185f-131">Configurare dispositivi VPN di terze parti per il server Azure MFA</span><span class="sxs-lookup"><span data-stu-id="9185f-131">Configure third-party VPN appliances for Azure MFA Server</span></span>](multi-factor-authentication-advanced-vpn-configurations.md)

- [<span data-ttu-id="9185f-132">Ampliare l'infrastruttura di autenticazione esistente con l'estensione NPS per Azure MFA</span><span class="sxs-lookup"><span data-stu-id="9185f-132">Augment your existing authentication infrastructure with the NPS extension for Azure MFA</span></span>](multi-factor-authentication-nps-extension.md)

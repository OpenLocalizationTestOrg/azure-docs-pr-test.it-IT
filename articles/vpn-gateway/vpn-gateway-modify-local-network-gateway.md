---
title: Modificare i prefissi di indirizzo IP gateway hello rete locale e l'indirizzo IP del Gateway VPN di hello | Azure | PowerShell | Documenti Microsoft
description: Questo articolo illustra in modo dettagliato come modificare i prefissi degli indirizzi IP per il gateway di rete locale usando PowerShell
services: vpn-gateway
documentationcenter: na
author: cherylmc
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 8c7db48f-d09a-44e7-836f-1fb6930389df
ms.service: vpn-gateway
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 06/19/2017
ms.author: cherylmc
ms.openlocfilehash: 1353598b39a97fae9bdb424505a5ae2560482654
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="modify-local-network-gateway-settings-using-powershell"></a><span data-ttu-id="c37e5-103">Modificare le impostazioni del gateway di rete locale usando PowerShell</span><span class="sxs-lookup"><span data-stu-id="c37e5-103">Modify local network gateway settings using PowerShell</span></span>

<span data-ttu-id="c37e5-104">In alcuni casi modificare le impostazioni di hello per il gateway di rete locale AddressPrefix o GatewayIPAddress.</span><span class="sxs-lookup"><span data-stu-id="c37e5-104">Sometimes hello settings for your local network gateway AddressPrefix or GatewayIPAddress change.</span></span> <span data-ttu-id="c37e5-105">In questo articolo illustra come toomodify le impostazioni del gateway di rete locale.</span><span class="sxs-lookup"><span data-stu-id="c37e5-105">This article shows you how toomodify your local network gateway settings.</span></span> <span data-ttu-id="c37e5-106">È inoltre possibile modificare queste impostazioni utilizzando un metodo diverso selezionando un'opzione diversa da hello seguente elenco:</span><span class="sxs-lookup"><span data-stu-id="c37e5-106">You can also modify these settings using a different method by selecting a different option from hello following list:</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="c37e5-107">Portale di Azure</span><span class="sxs-lookup"><span data-stu-id="c37e5-107">Azure portal</span></span>](vpn-gateway-modify-local-network-gateway-portal.md)
> * [<span data-ttu-id="c37e5-108">PowerShell</span><span class="sxs-lookup"><span data-stu-id="c37e5-108">PowerShell</span></span>](vpn-gateway-modify-local-network-gateway.md)
> * [<span data-ttu-id="c37e5-109">Interfaccia della riga di comando di Azure</span><span class="sxs-lookup"><span data-stu-id="c37e5-109">Azure CLI</span></span>](vpn-gateway-modify-local-network-gateway-cli.md)
>
>

## <span data-ttu-id="c37e5-110"><a name="before"></a>Prima di iniziare</span><span class="sxs-lookup"><span data-stu-id="c37e5-110"><a name="before"></a>Before you begin</span></span>

<span data-ttu-id="c37e5-111">Installare hello l'ultima versione di hello cmdlet PowerShell di gestione risorse di Azure.</span><span class="sxs-lookup"><span data-stu-id="c37e5-111">Install hello latest version of hello Azure Resource Manager PowerShell cmdlets.</span></span> <span data-ttu-id="c37e5-112">Vedere [come tooinstall e configurare Azure PowerShell](/powershell/azureps-cmdlets-docs) per ulteriori informazioni sull'installazione dei cmdlet di PowerShell hello.</span><span class="sxs-lookup"><span data-stu-id="c37e5-112">See [How tooinstall and configure Azure PowerShell](/powershell/azureps-cmdlets-docs) for more information about installing hello PowerShell cmdlets.</span></span>

## <span data-ttu-id="c37e5-113"><a name="ipaddprefix"></a>Modificare i prefissi degli indirizzi IP</span><span class="sxs-lookup"><span data-stu-id="c37e5-113"><a name="ipaddprefix"></a>Modify IP address prefixes</span></span>

[!INCLUDE [vpn-gateway-modify-ip-prefix-rm](../../includes/vpn-gateway-modify-ip-prefix-rm-include.md)]

## <span data-ttu-id="c37e5-114"><a name="gwip"></a>Modificare l'indirizzo IP del gateway hello</span><span class="sxs-lookup"><span data-stu-id="c37e5-114"><a name="gwip"></a>Modify hello gateway IP address</span></span>

[!INCLUDE [vpn-gateway-modify-lng-gateway-ip-rm](../../includes/vpn-gateway-modify-lng-gateway-ip-rm-include.md)]

## <a name="next-steps"></a><span data-ttu-id="c37e5-115">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="c37e5-115">Next steps</span></span>

<span data-ttu-id="c37e5-116">È possibile verificare la connessione al gateway.</span><span class="sxs-lookup"><span data-stu-id="c37e5-116">You can verify your gateway connection.</span></span> <span data-ttu-id="c37e5-117">Vedere [Verificare una connessione al gateway](vpn-gateway-verify-connection-resource-manager.md).</span><span class="sxs-lookup"><span data-stu-id="c37e5-117">See [Verify a gateway connection](vpn-gateway-verify-connection-resource-manager.md).</span></span>
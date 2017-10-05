---
title: Modificare i prefissi degli indirizzi IP per il gateway di rete locale e l'indirizzo IP del gateway VPN | Azure| PowerShell| Microsoft Docs
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
ms.openlocfilehash: 2a095b96a8c352abeca72640d37c0d629b447763
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/18/2017
---
# <a name="modify-local-network-gateway-settings-using-powershell"></a><span data-ttu-id="e53e6-103">Modificare le impostazioni del gateway di rete locale usando PowerShell</span><span class="sxs-lookup"><span data-stu-id="e53e6-103">Modify local network gateway settings using PowerShell</span></span>

<span data-ttu-id="e53e6-104">In alcuni casi le impostazioni per il valore AddressPrefix o GatewayIPAddress del gateway di rete locale subiscono modifiche.</span><span class="sxs-lookup"><span data-stu-id="e53e6-104">Sometimes the settings for your local network gateway AddressPrefix or GatewayIPAddress change.</span></span> <span data-ttu-id="e53e6-105">Questo articolo illustra come modificare le impostazioni del gateway di rete locale.</span><span class="sxs-lookup"><span data-stu-id="e53e6-105">This article shows you how to modify your local network gateway settings.</span></span> <span data-ttu-id="e53e6-106">È anche possibile modificare queste impostazioni con un altro metodo selezionando un'opzione diversa nell'elenco seguente:</span><span class="sxs-lookup"><span data-stu-id="e53e6-106">You can also modify these settings using a different method by selecting a different option from the following list:</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="e53e6-107">Portale di Azure</span><span class="sxs-lookup"><span data-stu-id="e53e6-107">Azure portal</span></span>](vpn-gateway-modify-local-network-gateway-portal.md)
> * [<span data-ttu-id="e53e6-108">PowerShell</span><span class="sxs-lookup"><span data-stu-id="e53e6-108">PowerShell</span></span>](vpn-gateway-modify-local-network-gateway.md)
> * [<span data-ttu-id="e53e6-109">Interfaccia della riga di comando di Azure</span><span class="sxs-lookup"><span data-stu-id="e53e6-109">Azure CLI</span></span>](vpn-gateway-modify-local-network-gateway-cli.md)
>
>

## <span data-ttu-id="e53e6-110"><a name="before"></a>Prima di iniziare</span><span class="sxs-lookup"><span data-stu-id="e53e6-110"><a name="before"></a>Before you begin</span></span>

<span data-ttu-id="e53e6-111">Installare la versione più recente dei cmdlet di PowerShell per Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="e53e6-111">Install the latest version of the Azure Resource Manager PowerShell cmdlets.</span></span> <span data-ttu-id="e53e6-112">Per altre informazioni sull'installazione dei cmdlet di PowerShell, vedere [Come installare e configurare Azure PowerShell](/powershell/azureps-cmdlets-docs) .</span><span class="sxs-lookup"><span data-stu-id="e53e6-112">See [How to install and configure Azure PowerShell](/powershell/azureps-cmdlets-docs) for more information about installing the PowerShell cmdlets.</span></span>

## <span data-ttu-id="e53e6-113"><a name="ipaddprefix"></a>Modificare i prefissi degli indirizzi IP</span><span class="sxs-lookup"><span data-stu-id="e53e6-113"><a name="ipaddprefix"></a>Modify IP address prefixes</span></span>

[!INCLUDE [vpn-gateway-modify-ip-prefix-rm](../../includes/vpn-gateway-modify-ip-prefix-rm-include.md)]

## <span data-ttu-id="e53e6-114"><a name="gwip"></a>Modificare l'indirizzo IP del gateway</span><span class="sxs-lookup"><span data-stu-id="e53e6-114"><a name="gwip"></a>Modify the gateway IP address</span></span>

[!INCLUDE [vpn-gateway-modify-lng-gateway-ip-rm](../../includes/vpn-gateway-modify-lng-gateway-ip-rm-include.md)]

## <a name="next-steps"></a><span data-ttu-id="e53e6-115">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="e53e6-115">Next steps</span></span>

<span data-ttu-id="e53e6-116">È possibile verificare la connessione al gateway.</span><span class="sxs-lookup"><span data-stu-id="e53e6-116">You can verify your gateway connection.</span></span> <span data-ttu-id="e53e6-117">Vedere [Verificare una connessione al gateway](vpn-gateway-verify-connection-resource-manager.md).</span><span class="sxs-lookup"><span data-stu-id="e53e6-117">See [Verify a gateway connection](vpn-gateway-verify-connection-resource-manager.md).</span></span>
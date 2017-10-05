---
title: Modificare i prefissi degli indirizzi IP per il gateway di rete locale e l'indirizzo IP del Gateway VPN | Azure| Interfaccia della riga di comando | Microsoft Docs
description: Questo articolo illustra in modo dettagliato come modificare i prefissi degli indirizzi IP per il gateway di rete locale usando l'interfaccia della riga di comando di Azure.
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
ms.openlocfilehash: 7db1ad970ebb93d46d5a861f9a9b27bf121531a3
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/18/2017
---
# <a name="modify-local-network-gateway-settings-using-the-azure-cli"></a><span data-ttu-id="40fe9-103">Modificare le impostazioni del gateway di rete locale usando l'interfaccia della riga di comando di Azure</span><span class="sxs-lookup"><span data-stu-id="40fe9-103">Modify local network gateway settings using the Azure CLI</span></span>

<span data-ttu-id="40fe9-104">In alcuni casi le impostazioni per il prefisso indirizzo o l'indirizzo IP gateway del gateway di rete locale subiscono modifiche.</span><span class="sxs-lookup"><span data-stu-id="40fe9-104">Sometimes the settings for your local network gateway Address Prefix or Gateway IP Address change.</span></span> <span data-ttu-id="40fe9-105">Questo articolo illustra come modificare le impostazioni del gateway di rete locale.</span><span class="sxs-lookup"><span data-stu-id="40fe9-105">This article shows you how to modify your local network gateway settings.</span></span> <span data-ttu-id="40fe9-106">È anche possibile modificare queste impostazioni con un altro metodo selezionando un'opzione diversa nell'elenco seguente:</span><span class="sxs-lookup"><span data-stu-id="40fe9-106">You can also modify these settings using a different method by selecting a different option from the following list:</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="40fe9-107">Portale di Azure</span><span class="sxs-lookup"><span data-stu-id="40fe9-107">Azure portal</span></span>](vpn-gateway-modify-local-network-gateway-portal.md)
> * [<span data-ttu-id="40fe9-108">PowerShell</span><span class="sxs-lookup"><span data-stu-id="40fe9-108">PowerShell</span></span>](vpn-gateway-modify-local-network-gateway.md)
> * [<span data-ttu-id="40fe9-109">Interfaccia della riga di comando di Azure</span><span class="sxs-lookup"><span data-stu-id="40fe9-109">Azure CLI</span></span>](vpn-gateway-modify-local-network-gateway-cli.md)
>
>

## <span data-ttu-id="40fe9-110"><a name="before"></a>Prima di iniziare</span><span class="sxs-lookup"><span data-stu-id="40fe9-110"><a name="before"></a>Before you begin</span></span>

<span data-ttu-id="40fe9-111">Installare la versione più recente dei comandi dell'interfaccia della riga di comando (2.0 o successiva).</span><span class="sxs-lookup"><span data-stu-id="40fe9-111">Install the latest version of the CLI commands (2.0 or later).</span></span> <span data-ttu-id="40fe9-112">Per informazioni sull'installazione dei comandi dell'interfaccia della riga di comando, vedere [Install Azure CLI 2.0](https://docs.microsoft.com/cli/azure/install-azure-cli) (Installare l'interfaccia della riga di comando di Azure 2.0).</span><span class="sxs-lookup"><span data-stu-id="40fe9-112">For information about installing the CLI commands, see [Install Azure CLI 2.0](https://docs.microsoft.com/cli/azure/install-azure-cli).</span></span>

[!INCLUDE [CLI-login](../../includes/vpn-gateway-cli-login-include.md)]

## <span data-ttu-id="40fe9-113"><a name="ipaddprefix"></a>Modificare i prefissi degli indirizzi IP</span><span class="sxs-lookup"><span data-stu-id="40fe9-113"><a name="ipaddprefix"></a>Modify IP address prefixes</span></span>

[!INCLUDE [modify-prefix](../../includes/vpn-gateway-modify-ip-prefix-cli-include.md)]

## <span data-ttu-id="40fe9-114"><a name="gwip"></a>Modificare l'indirizzo IP del gateway</span><span class="sxs-lookup"><span data-stu-id="40fe9-114"><a name="gwip"></a>Modify the gateway IP address</span></span>

[!INCLUDE [modify-gateway-IP](../../includes/vpn-gateway-modify-lng-gateway-ip-cli-include.md)]

## <a name="next-steps"></a><span data-ttu-id="40fe9-115">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="40fe9-115">Next steps</span></span>

<span data-ttu-id="40fe9-116">È possibile verificare la connessione al gateway.</span><span class="sxs-lookup"><span data-stu-id="40fe9-116">You can verify your gateway connection.</span></span> <span data-ttu-id="40fe9-117">Vedere [Verificare una connessione al gateway](vpn-gateway-verify-connection-resource-manager.md).</span><span class="sxs-lookup"><span data-stu-id="40fe9-117">See [Verify a gateway connection](vpn-gateway-verify-connection-resource-manager.md).</span></span>


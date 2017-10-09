---
title: Modificare i prefissi di indirizzo IP gateway hello rete locale e l'indirizzo IP del Gateway VPN di hello | Azure | CLI | Documenti Microsoft
description: In questo articolo illustra la modifica di prefissi di indirizzi IP per il gateway di rete locale tramite hello CLI di Azure.
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
ms.openlocfilehash: 4b8bbf3e9d3d42ac2d12f87360fa0a4134c57a21
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="modify-local-network-gateway-settings-using-hello-azure-cli"></a><span data-ttu-id="52693-103">Modificare le impostazioni di gateway di rete locale utilizzando hello CLI di Azure</span><span class="sxs-lookup"><span data-stu-id="52693-103">Modify local network gateway settings using hello Azure CLI</span></span>

<span data-ttu-id="52693-104">In alcuni casi modificare le impostazioni di hello per il prefisso dell'indirizzo di gateway di rete locale o un indirizzo IP del Gateway.</span><span class="sxs-lookup"><span data-stu-id="52693-104">Sometimes hello settings for your local network gateway Address Prefix or Gateway IP Address change.</span></span> <span data-ttu-id="52693-105">In questo articolo illustra come toomodify le impostazioni del gateway di rete locale.</span><span class="sxs-lookup"><span data-stu-id="52693-105">This article shows you how toomodify your local network gateway settings.</span></span> <span data-ttu-id="52693-106">È inoltre possibile modificare queste impostazioni utilizzando un metodo diverso selezionando un'opzione diversa da hello seguente elenco:</span><span class="sxs-lookup"><span data-stu-id="52693-106">You can also modify these settings using a different method by selecting a different option from hello following list:</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="52693-107">Portale di Azure</span><span class="sxs-lookup"><span data-stu-id="52693-107">Azure portal</span></span>](vpn-gateway-modify-local-network-gateway-portal.md)
> * [<span data-ttu-id="52693-108">PowerShell</span><span class="sxs-lookup"><span data-stu-id="52693-108">PowerShell</span></span>](vpn-gateway-modify-local-network-gateway.md)
> * [<span data-ttu-id="52693-109">Interfaccia della riga di comando di Azure</span><span class="sxs-lookup"><span data-stu-id="52693-109">Azure CLI</span></span>](vpn-gateway-modify-local-network-gateway-cli.md)
>
>

## <span data-ttu-id="52693-110"><a name="before"></a>Prima di iniziare</span><span class="sxs-lookup"><span data-stu-id="52693-110"><a name="before"></a>Before you begin</span></span>

<span data-ttu-id="52693-111">Installare hello versione i comandi CLI hello (2.0 o versione successivo).</span><span class="sxs-lookup"><span data-stu-id="52693-111">Install hello latest version of hello CLI commands (2.0 or later).</span></span> <span data-ttu-id="52693-112">Per informazioni sull'installazione di comandi CLI hello, vedere [installare Azure CLI 2.0](https://docs.microsoft.com/cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="52693-112">For information about installing hello CLI commands, see [Install Azure CLI 2.0](https://docs.microsoft.com/cli/azure/install-azure-cli).</span></span>

[!INCLUDE [CLI-login](../../includes/vpn-gateway-cli-login-include.md)]

## <span data-ttu-id="52693-113"><a name="ipaddprefix"></a>Modificare i prefissi degli indirizzi IP</span><span class="sxs-lookup"><span data-stu-id="52693-113"><a name="ipaddprefix"></a>Modify IP address prefixes</span></span>

[!INCLUDE [modify-prefix](../../includes/vpn-gateway-modify-ip-prefix-cli-include.md)]

## <span data-ttu-id="52693-114"><a name="gwip"></a>Modificare l'indirizzo IP del gateway hello</span><span class="sxs-lookup"><span data-stu-id="52693-114"><a name="gwip"></a>Modify hello gateway IP address</span></span>

[!INCLUDE [modify-gateway-IP](../../includes/vpn-gateway-modify-lng-gateway-ip-cli-include.md)]

## <a name="next-steps"></a><span data-ttu-id="52693-115">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="52693-115">Next steps</span></span>

<span data-ttu-id="52693-116">È possibile verificare la connessione al gateway.</span><span class="sxs-lookup"><span data-stu-id="52693-116">You can verify your gateway connection.</span></span> <span data-ttu-id="52693-117">Vedere [Verificare una connessione al gateway](vpn-gateway-verify-connection-resource-manager.md).</span><span class="sxs-lookup"><span data-stu-id="52693-117">See [Verify a gateway connection](vpn-gateway-verify-connection-resource-manager.md).</span></span>


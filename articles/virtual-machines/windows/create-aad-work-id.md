---
title: "aaaCreate un'identità aziendale o dell'istituto di istruzione in Azure ad per Windows | Documenti Microsoft"
description: "Informazioni su come toocreate un'identità aziendale o dell'istituto di istruzione in Azure Active Directory toouse con le macchine virtuali di Windows."
services: virtual-machines-windows
documentationcenter: 
author: squillace
manager: timlt
editor: 
tags: azure-service-management,azure-resource-manager
ms.assetid: d07dca34-618a-48aa-9971-03d9c1210f4a
ms.service: virtual-machines-windows
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: infrastructure
ms.date: 08/23/2016
ms.author: rasquill
ms.openlocfilehash: dd6e2381fd0aa503483aa786b36232e557729c4d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="creating-a-work-or-school-identity-in-azure-active-directory-toouse-with-windows-vms"></a>Creazione di un'identità aziendale o dell'istituto di istruzione in Azure Active Directory toouse con macchine virtuali di Windows
Se è stato creato un account di Azure personale o disporre di una sottoscrizione MSDN personale e creato hello account Azure tootake sfruttare crediti di Azure di MSDN hello - è stato utilizzato un *account Microsoft* toocreate identità è. Molte caratteristiche di Azure - [modelli di gruppo di risorse](../../azure-resource-manager/resource-group-overview.md) è un esempio, richiedono un account aziendale o dell'istituto di istruzione (un'identità gestita da Azure Active Directory) toowork. È possibile seguire le istruzioni di hello sotto toocreate che un nuovo lavoro o scuola account perché, per fortuna, uno degli aspetti migliori hello l'account di Azure personale che è dotato di un dominio di Azure Active Directory predefinito che è possibile utilizzare toocreate un nuovo lavoro o dell'istituto di istruzione account che è possibile utilizzare con le funzionalità di Azure che lo richiedono.

Tuttavia, le modifiche recenti rendono possibili toomanage la sottoscrizione con qualsiasi tipo di account Azure tramite hello `azure login` il metodo di accesso interattivo descritto [qui](../../xplat-cli-connect.md). È possibile utilizzare tale meccanismo oppure è possibile seguire le istruzioni hello che seguono. È anche possibile [creare un'identità aziendale o dell'istituto di istruzione in Azure Active Directory toouse con le macchine virtuali Linux](../linux/create-aad-work-id.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).

[!INCLUDE [learn-about-deployment-models](../../../includes/learn-about-deployment-models-both-include.md)]

[!INCLUDE [virtual-machines-common-create-aad-work-id](../../../includes/virtual-machines-common-create-aad-work-id.md)]


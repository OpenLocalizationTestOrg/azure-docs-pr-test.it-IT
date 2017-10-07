---
title: aaaValidate hello rete virtuale di Azure toouse con Azure RemoteApp | Documenti Microsoft
description: "Informazioni su come toomake assicurarsi che la rete virtuale di Azure è pronta toouse con Azure RemoteApp"
services: remoteapp
documentationcenter: 
author: msmbaldwin
manager: mbaldwin
ms.assetid: b573ba02-4587-4be5-9821-27bd891a73b2
ms.service: remoteapp
ms.workload: compute
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 11/23/2016
ms.author: mbaldwin
ms.openlocfilehash: 5587556c264356e6ab6039b983a38cb2b95ed268
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="validate-hello-azure-vnet-toouse-with-azure-remoteapp"></a>Convalidare hello toouse di rete virtuale di Azure con Azure RemoteApp
> [!IMPORTANT]
> Azure RemoteApp verrà sospeso a partire dal 31 agosto 2017. Hello lettura [annuncio](https://go.microsoft.com/fwlink/?linkid=821148) per informazioni dettagliate.
> 
> 

Prima di utilizzare una rete virtuale di Azure con Azure RemoteApp, è possibile toovalidate hello rete virtuale. Consente di evitare problemi con la connettività.

toovalidate rete virtuale di Azure, hello seguenti:

1. Creare una macchina virtuale di Azure all'interno di hello subnet della rete virtuale di Azure, si desidera toouse con Azure RemoteApp hello.
2. Connettersi con hello toothat VM **Connetti** opzione nel portale di gestione di hello.
3. Join hello macchina virtuale toohello stesso dominio in cui si desidera toouse con Azure RemoteApp. Se si sta creando una raccolta ibrida che si connette rete locale tooyour, dominio locale tooyour join hello macchina virtuale.

Se ha esito positivo, hello rete virtuale di Azure è pronta toouse con RemoteApp.

Per ulteriori informazioni sul flusso di lavoro Raccolta hello ibrida end-to-end, vedere hello seguenti articoli:

* [Come tooplan la rete virtuale di Azure RemoteApp](remoteapp-planvnet.md)
* [Creare una raccolta ibrida](remoteapp-create-hybrid-deployment.md)
* [Distribuire Azure RemoteApp raccolta tooyour rete virtuale di Azure (con supporto per ExpressRoute)](http://blogs.msdn.com/b/rds/archive/2015/04/23/deploy-azure-remoteapp-collection-to-your-azure-virtual-network-with-support-for-expressroute.aspx)


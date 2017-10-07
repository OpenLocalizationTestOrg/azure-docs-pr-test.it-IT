---
title: aaaEnabling fine tooend SSL nel Gateway di applicazione di Azure | Documenti Microsoft
description: Questa pagina viene fornita una panoramica di hello Gateway applicazione end tooend supporto SSL.
documentationcenter: na
services: application-gateway
author: amsriva
manager: rossort
editor: amsriva
ms.assetid: 3976399b-25ad-45eb-8eb3-fdb736a598c5
ms.service: application-gateway
ms.devlang: na
ms.topic: hero-article
ms.tgt_pltfrm: na
ms.custom: H1Hack27Feb2017
ms.workload: infrastructure-services
ms.date: 07/19/2017
ms.author: amsriva
ms.openlocfilehash: c5cb398a1e7d9a08662a3120baad98edb5575917
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="overview-of-end-tooend-ssl-with-application-gateway"></a>Panoramica di fine tooend SSL con Gateway applicazione

Gateway applicazione supporta la terminazione SSL gateway hello, dopo che il traffico passa in genere non crittografati toohello i server back-end. Questa funzionalità consente di web server toobe unburdened da sovraccarico di crittografia e decrittografia costoso. Per alcuni clienti server back-end toohello di comunicazione non crittografata non è tuttavia un'opzione accettabile. Questa comunicazione non crittografata potrebbe essere dovuto toosecurity requisiti, i requisiti di conformità, o un'applicazione hello può accettare solo una connessione sicura. Per tali applicazioni, i gateway applicazione supporta fine tooend SSL crittografia.

## <a name="overview"></a>Panoramica

Fine tooend SSL consente toosecurely trasmettere back-end toohello dati sensibili crittografati mentre vengono comunque usufruire dei vantaggi di hello della funzionalità di bilanciamento del carico di livello 7 il gateway applicazione. Alcune di queste funzionalità sono l'affinità di sessione basato su cookie, il routing basato su URL, il supporto per il routing basato su siti o possibilità tooinject - inoltrati - X * intestazioni.

Quando è configurato con la modalità di comunicazione end tooend SSL, gateway applicazione termina le sessioni SSL hello gateway hello e decrittografa il traffico utente. Viene quindi applicata hello configurata regole tooselect un back-end appropriata pool istanza tooroute del traffico. Gateway applicazione quindi avvia un nuovo server di back-end toohello connessione SSL e crittografare nuovamente i dati tramite certificato di chiave pubblica del server back-end hello prima della trasmissione hello back-end toohello di richiesta. Fine tooend che SSL è abilitato impostando l'impostazione del protocollo in tooHTTPS BackendHTTPSetting, che viene quindi applicato pool back-end tooa. Ogni server di back-end nel pool back-end di hello con SSL abilitato tooend di fine deve essere configurato con una comunicazione protetta tooallow di certificato.

![scenario di end tooend ssl][1]

In questo esempio, le richieste tramite TLS 1.2 sono server toobackend indirizzato Pool1 utilizzando tooend fine SSL.

## <a name="end-tooend-ssl-and-whitelisting-of-certificates"></a>Terminare tooend SSL e whitelist dei certificati

Gateway applicazione comunica solo con le istanze di back-end noto che hanno consentito il proprio certificato al gateway applicazione hello. whitelist tooenable dei certificati, è necessario caricare la chiave pubblica hello di gateway applicazione back-end server certificati toohello (non certificato radice hello). Solo le connessioni tooknown e consentito back-end sono quindi consentiti. Hello rimanenti back-end genera un errore di gateway. I certificati autofirmati vengono usati a scopo di test e non sono consigliati per i carichi di lavoro. Tali certificati hanno consentito di toobe con il gateway applicazione hello come descritto in hello passaggi precedenti, prima di poter essere usati.

## <a name="next-steps"></a>Passaggi successivi

Dopo avere imparare a fine tooend SSL, andare troppo[abilitare fine tooend SSL nel gateway applicazione](application-gateway-end-to-end-ssl-powershell.md) toocreate gateway un'applicazione che utilizza end tooend SSL.

<!--Image references-->

[1]: ./media/application-gateway-backend-ssl/scenario.png

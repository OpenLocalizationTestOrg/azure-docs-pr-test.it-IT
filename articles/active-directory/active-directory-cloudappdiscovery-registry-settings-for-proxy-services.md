---
title: le impostazioni del Registro di sistema di individuazione di App per servizi Proxy aaaCloud | Documenti Microsoft
description: "obiettivo Hello di questo argomento è tooprovide si con hello i passaggi necessari per necessario tooperform tooset hello necessario porta hello i computer agente Cloud App Discovery hello."
services: active-directory
documentationcenter: 
author: MarkusVi
manager: femila
ms.assetid: 8d78e925-e331-40ba-904a-e4ef14260cac
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/05/2017
ms.author: markvi
ms.reviewer: nigu
ms.openlocfilehash: bb1fe20016459160b4f67cb0125b1781a0260c4b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="cloud-app-discovery-registry-settings-for-proxy-services"></a>Impostazioni del Registro di sistema di Cloud App Discovery per i servizi proxy
Per impostazione predefinita, l'agente Cloud App Discovery hello è toouse configurato solo hello porte 80 o 443. Se prevede di installare Cloud App Discovery in un ambiente con un server proxy che utilizza una porta personalizzata (80 né 443), è necessario tooconfigure il toouse agenti questa porta. configurazione di Hello è basata su una chiave del Registro di sistema.

obiettivo Hello di questo argomento è tooprovide si con hello i passaggi necessari per necessario tooperform tooset hello necessario porta hello i computer agente Cloud App Discovery hello.

**porta hello toomodify utilizzata dal computer hello esecuzione agente Cloud App Discovery hello, eseguire hello alla procedura seguente:**

1. Avviare l'editor del Registro di sistema hello. <br> ![Esegui](./media/active-directory-cloudappdiscovery-registry-settings-for-proxy-services/proxy01.png)
2. Passare tooor creare hello seguente chiave del Registro di sistema: <br> **HKLM_LOCAL_MACHINE\Software\Microsoft\Cloud App Discovery\Endpoint** 
3. Creare un nuovo valore **multistringa** denominato **Ports**. ![Nuovo](./media/active-directory-cloudappdiscovery-registry-settings-for-proxy-services/proxy02.png)
4. hello tooopen **Modifica multistringhe** finestra di dialogo, fare doppio clic sul valore porte hello.
5. Nella casella dati valore hello digitare i seguenti valori hello e aggiungere tutte le porte personalizzate che vengono utilizzate dall'organizzazione: <br><br>
   **80** <br>
   **8080** <br>
   **8118** <br>
   **8888** <br>
   **81** <br>
   **12080** <br>
   **6999** <br>
   **30606** <br>
   **31595** <br>
   **4080** <br>
   **443** <br>
   **1110** <br><br>
   ![Modifica multistringhe](./media/active-directory-cloudappdiscovery-registry-settings-for-proxy-services/proxy03.png)
6. Fare clic su **OK** tooclose hello **Modifica multistringhe** finestra di dialogo.

**Risorse aggiuntive**

* [Come individuare app cloud non autorizzate usate nell'organizzazione](active-directory-cloudappdiscovery-whatis.md) 


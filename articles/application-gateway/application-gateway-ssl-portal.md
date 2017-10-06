---
title: -Gateway applicazione Azure - portale di Azure di offload SSL aaaConfigure | Documenti Microsoft
description: Questa pagina fornisce un gateway applicazione con SSL offload tramite il portale di hello toocreate di istruzioni
documentationcenter: na
services: application-gateway
author: georgewallace
manager: timlt
editor: tysonn
ms.assetid: 8373379a-a26a-45d2-aa62-dd282298eff3
ms.service: application-gateway
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 01/23/2017
ms.author: gwallace
ms.openlocfilehash: e87ac0bbe10ac45e307c18802741c7bc31764a20
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="configure-an-application-gateway-for-ssl-offload-by-using-hello-portal"></a>Configurare un gateway applicazione per l'offload SSL tramite il portale di hello

> [!div class="op_single_selector"]
> * [Portale di Azure](application-gateway-ssl-portal.md)
> * [PowerShell per Azure Resource Manager](application-gateway-ssl-arm.md)
> * [PowerShell per Azure classico](application-gateway-ssl.md)
> * [Interfaccia della riga di comando di Azure 2.0](application-gateway-ssl-cli.md)

Gateway applicazione Azure può essere configurato tooterminate hello Secure Sockets Layer (SSL) sessione hello gateway tooavoid costosi SSL decrittografia attività toohappen alla farm web hello. Offload SSL semplifica anche l'installazione di server front-end di hello e gestione di un'applicazione web hello.

## <a name="scenario"></a>Scenario

Hello segue scenario passa attraverso la configurazione di offload SSL su un gateway applicazione esistente. Hello scenario si presuppone che siano state già seguite passaggi hello troppo[creare un Gateway applicazione](application-gateway-create-gateway-portal.md).

## <a name="before-you-begin"></a>Prima di iniziare

offload SSL di tooconfigure con un gateway applicazione, è necessario un certificato. Questo certificato viene caricato nel gateway applicazione hello e usato tooencrypt e decrittografia il traffico hello inviato tramite SSL. certificato Hello deve toobe nel formato di scambio di informazioni personali (pfx). Questo formato di file consente di hello privata toobe chiave esportato richiesto dal hello applicazione gateway tooperform hello crittografia e decrittografia del traffico.

## <a name="add-an-https-listener"></a>Aggiungere un listener HTTPS

listener HTTPS Hello Cerca il traffico in base alla relativa configurazione e consente di pool back-end di route hello traffico toohello.

### <a name="step-1"></a>Passaggio 1

Passare toohello portale di Azure e selezionare un gateway applicazione esistente

### <a name="step-2"></a>Passaggio 2

Selezionare i listener hello Aggiungi pulsante tooadd un listener.

![Pannello di panoramica del gateway applicazione][1]

### <a name="step-3"></a>Passaggio 3

Compilare le informazioni necessarie per il listener hello hello e caricamento hello certificato PFX, al termine, fare clic su OK.

**Nome** -questo valore è un nome descrittivo del listener hello.

**Configurazione IP Frontend** -questo valore è una configurazione IP front-end del hello che viene utilizzato per il listener hello.

**Porta front-end (nome/porta)** -un nome descrittivo per la porta hello utilizzata nel front-end di hello di gateway applicazione hello e hello effettivo della porta utilizzata.

**Protocollo** -toodetermine un commutatore se viene utilizzato https o http per front-end hello.

**Certificato (Nome/Password)** : se si usa l'offload SSL, per questa impostazione sono necessari un certificato PFX, un nome descrittivo e una password.

![Pannello Aggiungi listener][2]

## <a name="create-a-rule-and-associate-it-toohello-listener"></a>Creare una regola e associarlo toohello listener

listener Hello è stata creata. È ora toocreate un traffico di hello toohandle regola dal listener hello. Le regole definiscono come il traffico è indirizzato toohello pool di back-end in base a più impostazioni di configurazione, ad esempio se viene utilizzato l'affinità di sessione basato su cookie, protocollo, porta e probe di integrità.

### <a name="step-1"></a>Passaggio 1

Fare clic su hello **regole** di gateway applicazione hello, quindi fare clic su Aggiungi.

![Pannello delle regole del gateway applicazione][3]

### <a name="step-2"></a>Passaggio 2

In hello **Aggiungi regola di base** pannello digitare hello nome descrittivo per la regola hello e scegliere listener hello creato nel passaggio precedente hello. Scegliere il pool di back-end appropriata hello e http impostazione e fare clic su **OK**

![Finestra delle impostazioni HTTP][4]

gateway applicazione toohello verranno salvate le impostazioni di Hello. Hello Salva processo per queste impostazioni potrebbe richiedere qualche minuto prima che vengano tooview disponibili tramite il portale di hello o PowerShell. Gateway applicazione hello dopo il salvataggio gestisce hello crittografia e decrittografia del traffico. Tutto il traffico tra server di hello back-end web e di gateway applicazione hello verrà gestito tramite http. Verrà restituito client toohello crittografata qualsiasi client toohello indietro comunicazione se avviata tramite https.

## <a name="next-steps"></a>Passaggi successivi

toolearn come probe tooconfigure dello stato personalizzato con Gateway applicazione Azure, vedere [per creare un probe di integrità personalizzato](application-gateway-create-gateway-portal.md).

[1]: ./media/application-gateway-ssl-portal/figure1.png
[2]: ./media/application-gateway-ssl-portal/figure2.png
[3]: ./media/application-gateway-ssl-portal/figure3.png
[4]: ./media/application-gateway-ssl-portal/figure4.png

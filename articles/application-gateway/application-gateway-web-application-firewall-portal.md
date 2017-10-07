---
title: aaaCreate o aggiornare un Gateway applicazione Azure con firewall applicazione web | Documenti Microsoft
description: Informazioni su come toocreate con firewall applicazione web tramite un Gateway di applicazione hello portale
services: application-gateway
documentationcenter: na
author: georgewallace
manager: timlt
editor: tysonn
tags: azure-resource-manager
ms.assetid: b561a210-ed99-4ab4-be06-b49215e3255a
ms.service: application-gateway
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 05/03/2017
ms.author: gwallace
ms.openlocfilehash: 68d140fef14499da654ea251d1208e6a800f55a9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="create-an-application-gateway-with-web-application-firewall-by-using-hello-portal"></a>Creare un gateway applicazione con firewall applicazione web tramite il portale di hello

> [!div class="op_single_selector"]
> * [Portale di Azure](application-gateway-web-application-firewall-portal.md)
> * [PowerShell](application-gateway-web-application-firewall-powershell.md)
> * [Interfaccia della riga di comando di Azure](application-gateway-web-application-firewall-cli.md)

Informazioni su come toocreate un firewall applicazione web abilitata gateway applicazione.

firewall applicazione web di Hello (WAF) nel Gateway di applicazione di Azure consente di proteggere le applicazioni web da attacchi basati sul web comuni quali attacchi SQL injection, attacchi di script e assume il controllo di sessione. Applicazione Web consente di proteggere molti hello OWASP top 10 web vulnerabilità comuni.

## <a name="scenarios"></a>Scenari

Questo articolo presenta due scenari:

Nel primo scenario hello, si apprenderà troppo[creare un gateway applicazione con firewall applicazione web](#create-an-application-gateway-with-web-application-firewall)

Nel secondo scenario hello, si apprenderà troppo[aggiungere web application firewall tooan esistente gateway applicazione](#add-web-application-firewall-to-an-existing-application-gateway).

![Esempio dello scenario][scenario]

> [!NOTE]
> Le ricerche di configurazione aggiuntiva di gateway applicazione hello, inclusi stato personalizzato, gli indirizzi del pool back-end e regole aggiuntive vengono configurati dopo la configurazione di gateway applicazione hello e non durante la distribuzione iniziale.

## <a name="before-you-begin"></a>Prima di iniziare

Il gateway applicazione di Azure richiede una propria subnet. Quando si crea una rete virtuale, assicurarsi di lasciare sufficiente toohave spazio di indirizzi più subnet. Dopo aver distribuito una subnet tooa di gateway applicazione, gateway di applicazione solo aggiuntive sono in grado di toobe aggiunto toohello subnet.

##<a name="add-web-application-firewall-to-an-existing-application-gateway"></a>Aggiungere web application firewall tooan esistente gateway applicazione

In questo esempio aggiorna un'applicazione gateway toosupport web application firewall esistente in modalità di prevenzione.

1. Nel portale di Azure hello **Preferiti** riquadro, fare clic su **tutte le risorse**. Fare clic su hello Gateway applicazione esistente in hello **tutte le risorse** blade. Se sottoscrizione hello selezionati sono già dispone di numerose risorse in essa contenuti, è possibile immettere il nome di hello in hello **filtrare in base al nome...** zona DNS hello accesso tooeasily casella.

   ![Creazione di un gateway applicazione][1]

1. Fare clic su **firewall applicazione Web** e aggiornare le impostazioni di gateway applicazione hello. Al termine, fare clic su **Salva**

    le impostazioni di Hello tooupdate un firewall di applicazione web esistente del toosupport gateway applicazione sono:

   | **Impostazione** | **Valore** | **Dettagli**
   |---|---|---|
   |**Aggiornamento tooWAF livello**| Selezionato | Consente di impostare il livello di hello del livello di WAF toohello gateway applicazione hello.|
   |**Stato del firewall**| Enabled | Questa impostazione abilita il firewall di hello nei hello WAF.|
   |**Modalità firewall** | Prevenzione | Questa impostazione riguarda la modalità di gestione del traffico dannoso da parte del firewall applicazione Web. **Rilevamento** modalità registra solo gli eventi di hello, in cui **prevenzione** modalità registra gli eventi di hello e arresta hello traffico dannoso.|
   |**Set di regole**|3.0|Questa impostazione determina hello [set di regole di base](application-gateway-web-application-firewall-overview.md#core-rule-sets) membri del pool che è usato tooprotect hello back-end.|
   |**Configurare regole disabilitate**|variabile|tooprevent possibili falsi positivi, questa impostazione consente toodisable determinati [regole e gruppi di regole](application-gateway-crs-rulegroups-rules.md).|

    >[!NOTE]
    > Quando si aggiorna un toohello di gateway applicazione esistente WAF SKU, hello SKU dimensioni troppo modifiche**Media**. L'impostazione può essere riconfigurata al termine della configurazione.

    ![Pannello con impostazioni di base][2-1]

    > [!NOTE]
    > log di firewall applicazione web tooview, diagnostica deve essere abilitato e ApplicationGatewayFirewallLog selezionato. A scopo di test si può scegliere 1 come numero di istanze. È importante che tutte le istanze in due istanze di contare tooknow non coperto da hello contratto di servizio e pertanto non sono consigliati. Con il firewall applicazione Web non è possibile usare gateway di piccole dimensioni.

## <a name="create-an-application-gateway-with-web-application-firewall"></a>creare un gateway applicazione con il firewall applicazione Web

Questo scenario illustrerà come:

* Creare un gateway applicazione del firewall applicazione Web Medium con due istanze.
* Creare una rete virtuale denominata AdatumAppGatewayVNET con un blocco CIDR riservato 10.0.0.0/16.
* Creare una subnet denominata Appgatewaysubnet che usa 10.0.0.0/28 come blocco CIDR.
* Configurare un certificato per l'offload SSL.

1. Accedi toohello [portale di Azure](https://portal.azure.com). Se non si dispone già di un account, è possibile iscriversi per ottenere una [versione di valutazione gratuita della durata di un mese](https://azure.microsoft.com/free)
1. Nel riquadro di Preferiti hello del portale di hello, fare clic su **New**
1. In hello **New** pannello, fare clic su **rete**. In hello **rete** pannello, fare clic su **Gateway applicazione**, come illustrato nella seguente immagine hello:
1. Passare toohello portale di Azure, fare clic su **New** > **rete** > **Gateway applicazione**

    ![Creazione di un gateway applicazione][1]

1. In hello **nozioni di base** blade che viene visualizzata, immettere i seguenti valori hello, quindi fare clic su **OK**:

   | **Impostazione** | **Valore** | **Dettagli**
   |---|---|---|
   |**Nome**|AdatumAppGateway|nome Hello del gateway applicazione hello|
   |**Livello**|WAF|I valori disponibili sono Standard e WAF. Visitare [firewall applicazione web](application-gateway-web-application-firewall-overview.md) toolearn ulteriori informazioni sulla WAF.|
   |**Dimensioni SKU**|Media|Opzioni disponibili quando si sceglie il livello Standard: Small, Medium e Large. Quando si sceglie il livello WAF, le opzioni sono solo Medium e Large.|
   |**Numero di istanze**|2|Numero di istanze del gateway applicazione hello per la disponibilità elevata. I numeri di istanze di 1 devono essere usati solo a scopo di test.|
   |**Sottoscrizione**|[Sottoscrizione]|Selezionare un gateway applicazione di sottoscrizione toocreate hello in.|
   |**Gruppo di risorse**|**Crea nuovo:** AdatumAppGatewayRG|Creare un gruppo di risorse. nome del gruppo di risorse Hello deve essere univoco all'interno di sottoscrizione hello selezionata. ulteriori informazioni sui gruppi di risorse, leggere hello toolearn [Gestione risorse](../azure-resource-manager/resource-group-overview.md?toc=%2fazure%2fapplication-gateway%2ftoc.json#resource-groups) articolo introduttivo.|
   |**Posizione**|Stati Uniti occidentali||

   ![Pannello con impostazioni di base][2-2]

1. In hello **impostazioni** pannello visualizzato sotto **rete virtuale**, fare clic su **scegliere una rete virtuale**. Questo passaggio viene visualizzata immettere hello **rete virtuale scegliere** blade.  Fare clic su **Crea nuovo** tooopen hello **crea rete virtuale** blade.

   ![scegliere una rete virtuale][2]

1. In hello **blade di rete virtuale crea** immettere i seguenti valori hello, quindi fare clic su **OK**. Questo passaggio consente di chiudere hello **crea rete virtuale** e **rete virtuale scegliere** pannelli. Questo compilerà hello **Subnet** campo hello **impostazioni** pannello con subnet hello scelto.

   |**Impostazione** | **Valore** | **Dettagli** |
   |---|---|---|
   |**Nome**|AdatumAppGatewayVNET|Nome del gateway applicazione hello|
   |**Spazio di indirizzi:**|10.0.0.0/16| Questo valore è lo spazio di indirizzo hello per la rete virtuale hello|
   |**Nome della subnet**|AppGatewaySubnet|Nome della subnet di hello per il gateway applicazione hello|
   |**Intervallo di indirizzi subnet**|10.0.0.0/28 | Questa subnet consente ulteriori altre subnet nella rete virtuale hello per i membri del pool back-end|

1. In hello **impostazioni** pannello **configurazione IP Frontend**, scegliere **pubblica** come hello **tipo di indirizzo IP**

1. In hello **impostazioni** pannello **indirizzo IP pubblico**, fare clic su **scegliere un indirizzo IP pubblico**, questo passaggio apre hello **scegliere l'indirizzo IP pubblico**pannello, fare clic su **Crea nuovo**.

   ![scegliere un indirizzo IP pubblico][3]

1. In hello **creare l'indirizzo IP pubblico** pannello, accettare il valore di predefinito hello e fare clic su **OK**. Questo passaggio consente di chiudere hello **scegliere l'indirizzo IP pubblico** blade, hello **creare l'indirizzo IP pubblico** pannello e popolare **indirizzo IP pubblico** con indirizzo IP pubblico hello scelto.

1. In hello **impostazioni** pannello **configurazione Listener**, fare clic su **HTTP** in **protocollo**. toouse **https**, è necessario un certificato. chiave privata di Hello del certificato di hello è necessario pertanto un'esportazione con estensione pfx del certificato hello deve toobe fornito e hello password per il file hello.

1. Configurare hello **WAF** impostazioni specifiche.

   |**Impostazione** | **Valore** | **Dettagli** |
   |---|---|---|
   |**Stato del firewall**| Enabled| Questa impostazione attiva o disattiva il WAF.|
   |**Modalità firewall** | Prevenzione| Questa impostazione determina le azioni di hello che WAF accetta traffico dannoso. Se viene scelta l'opzione **Rilevamento** , il traffico sarà solo registrato.  Se viene scelta l'opzione **Prevenzione**, il traffico viene registrato e interrotto con una risposta 403 di accesso non autorizzato.|


1. Esaminare la pagina Riepilogo hello e fare clic su **OK**.  Gateway applicazione hello ora viene messo in coda e creato.

1. Dopo aver creato il gateway di applicazione hello, passare in Configurazione portale toocontinue hello del gateway applicazione hello tooit.

    ![Visualizzazione della risorsa del gateway applicazione][10]

Questi passaggi creano un gateway applicazione basic con le impostazioni predefinite per il listener hello, pool back-end, le impostazioni http back-end e regole. È possibile modificare questi toosuit impostazioni la distribuzione di una volta hello provisioning ha esito positivo

> [!NOTE]
> Gateway applicazione creati con configurazione del firewall applicazione web di base hello sono configurati con CRS 3.0 per la protezione.

## <a name="next-steps"></a>Passaggi successivi

Successivamente, è possibile ottenere informazioni come un alias di dominio personalizzato per hello tooconfigure [indirizzo IP pubblico](../dns/dns-custom-domain.md#public-ip-address) tramite DNS di Azure o un altro provider DNS.

Informazioni su come la registrazione diagnostica tooconfigure, toolog hello gli eventi rilevati o prevenire firewall applicazione web, visitare il sito [diagnostica del Gateway applicazione](application-gateway-diagnostics.md)

Informazioni su come probe di integrità personalizzato toocreate visitando [per creare un probe di integrità personalizzato](application-gateway-create-probe-portal.md)

Informazioni su come tooconfigure offload SSL e la decrittografia SSL costosa di intraprendere hello off i server web, visitare il sito [configurare Offload SSL](application-gateway-ssl-portal.md)

<!--Image references-->
[1]: ./media/application-gateway-web-application-firewall-portal/figure1.png
[2]: ./media/application-gateway-web-application-firewall-portal/figure2.png
[2-1]: ./media/application-gateway-web-application-firewall-portal/figure2-1.png
[2-2]: ./media/application-gateway-web-application-firewall-portal/figure2-2.png
[3]: ./media/application-gateway-web-application-firewall-portal/figure3.png
[10]: ./media/application-gateway-web-application-firewall-portal/figure10.png
[scenario]: ./media/application-gateway-web-application-firewall-portal/scenario.png

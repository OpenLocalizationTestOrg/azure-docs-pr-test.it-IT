---
title: aaaMigrate un DNS active nome tooAzure servizio App | Documenti Microsoft
description: "Informazioni su come un nome di dominio DNS personalizzato che è già assegnato tooa toomigrate live tooAzure sito servizio App senza alcun tempo di inattività."
services: app-service
documentationcenter: 
author: cephalin
manager: erikre
editor: jimbe
tags: top-support-issue
ms.assetid: 10da5b8a-1823-41a3-a2ff-a0717c2b5c2d
ms.service: app-service
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/28/2017
ms.author: cephalin
ms.openlocfilehash: fbc4cc30dcb87efb2e867cb65c5404b667661e62
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="migrate-an-active-dns-name-tooazure-app-service"></a>Eseguire la migrazione di un active tooAzure di nome DNS del servizio App

Questo articolo viene illustrato come un DNS active toomigrate denominati troppo[Azure App Service](../app-service/app-service-value-prop-what-is.md) senza alcun tempo di inattività.

Quando si esegue la migrazione di un sito in tempo reale e il relativo tooApp nome di dominio DNS del servizio, tale nome DNS è già in uso presso il traffico in tempo reale. È possibile evitare periodi di inattività per la risoluzione DNS durante la migrazione di hello associando hello active tooyour di nome DNS del servizio App app modalità preemptive.

Se non si ritiene che la risoluzione DNS periodi di inattività, vedere [mappare un esistente personalizzato DNS nome tooAzure App Web](app-service-web-tutorial-custom-domain.md).

## <a name="prerequisites"></a>Prerequisiti

toocomplete questo procedure:

- [Verificare che l'app del servizio app non sia inclusa nel livello GRATUITO](app-service-web-tutorial-custom-domain.md#checkpricing).

## <a name="bind-hello-domain-name-preemptively"></a>Associare il nome di dominio hello modalità preemptive

Quando si associa un dominio personalizzato modalità preemptive, eseguire entrambe le operazioni seguenti hello prima di apportare modifiche ai record DNS:

- Verificare la proprietà del dominio
- Abilita hello nome di dominio per l'app

Quando si migra infine il nome DNS personalizzato hello vecchio sito toohello app del servizio App, non saranno presenti tempi di inattività nella risoluzione DNS.

[!INCLUDE [Access DNS records with domain provider](../../includes/app-service-web-access-dns-records.md)]

### <a name="create-domain-verification-record"></a>Creare un record di verifica del dominio

la proprietà dominio tooverify, Aggiungi un TXT record. esegue il mapping di Hello record TXT da _awverify.&lt; sottodominio >_ too_&lt;appname >. azurewebsites.net_. 

Hello record TXT, è necessario dipende dal record DNS che si desidera toomigrate hello. Per esempi, vedere hello nella tabella seguente (`@` in genere rappresenta hello dominio principale):  

| Esempio di record DNS | Host TXT | Valore TXT |
| - | - | - |
| @ (radice) | _awverify_ | _&lt;appname>.azurewebsites.net_ |
| www (sottodominio) | _awverify.www_ | _&lt;appname&gt;.azurewebsites.net_ |
| \* (wildcard) | _awverify.\*_ | _&lt;appname&gt;.azurewebsites.net_ |

Nella pagina di record DNS, tipo di record di hello del nome DNS desiderato toomigrate hello nota. Il servizio app supporta i mapping da record CNAME e A.

### <a name="enable-hello-domain-for-your-app"></a>Abilitare hello dominio per l'app

In hello [portale di Azure](https://portal.azure.com)in hello spostamento a sinistra della pagina app hello, selezionare **i domini personalizzati**. 

![Menu del dominio personalizzato](./media/app-service-web-tutorial-custom-domain/custom-domain-menu.png)

In hello **i domini personalizzati** pagina, seleziona hello  **+**  icona Avanti troppo**aggiungere hostname**.

![Aggiunta del nome host](./media/app-service-web-tutorial-custom-domain/add-host-name-cname.png)

Nome dominio completo del tipo hello aggiunti record TXT hello, ad esempio `www.contoso.com`. Per un dominio con caratteri jolly (ad esempio \*. contoso.com), è possibile utilizzare qualsiasi nome DNS al dominio con caratteri jolly hello. 

Selezionare **Convalida**.

Hello **aggiungere hostname** pulsante è attivato. 

Assicurarsi che **tipo di record Hostname** è di tipo di record DNS toohello desiderato toomigrate impostato.

Selezionare **Aggiungi il nome host**.

![Aggiungere app toohello di nome DNS](./media/app-service-web-tutorial-custom-domain/validate-domain-name-cname.png)

Potrebbe richiedere del tempo hello nuovo nome host toobe riportate nella finestra dell'applicazione hello **i domini personalizzati** pagina. Provare ad aggiornare dati hello tooupdate di hello del browser.

![Record CNAME aggiunto](./media/app-service-web-tutorial-custom-domain/cname-record-added.png)

Il dominio DNS personalizzato è ora abilitato nell'app Azure. 

## <a name="remap-hello-active-dns-name"></a>Modificare il nome DNS active hello mapping

Hello solo toodo a sinistra di cosa è mapping l'active tooApp di toopoint record DNS del servizio. Destra a questo punto, fa ancora riferimento tooyour vecchio sito.

<a name="info"></a>

### <a name="copy-hello-apps-ip-address-a-record-only"></a>Copiare l'indirizzo IP dell'applicazione hello (solo un record)

Se si vuole modificare il mapping di un record CNAME, ignorare questa sezione. 

tooremap un record, è necessario indirizzo IP esterno dell'applicazione di servizio App hello, come illustrato nella hello **i domini personalizzati** pagina.

Chiude hello **aggiungere hostname** selezionando **X** nell'angolo superiore destro di hello. 

In hello **i domini personalizzati** copiare l'indirizzo IP dell'applicazione hello.

![Spostamento del portale tooAzure app](./media/app-service-web-tutorial-custom-domain/mapping-information.png)

### <a name="update-hello-dns-record"></a>Aggiornamento del record DNS hello

Nella pagina di record DNS hello del provider di dominio, selezionare hello tooremap di record DNS.

Per hello `contoso.com` esempio dominio radice, modificare i record A o CNAME hello, come negli esempi di hello hello nella tabella seguente: 

| Esempio di FQDN | Tipo di record | Host | Valore |
| - | - | - | - |
| contoso.com (radice) | Una  | `@` | Indirizzo IP da [indirizzo IP dell'applicazione hello copia](#info) |
| www.contoso.com (sottodominio) | CNAME | `www` | _&lt;appname>.azurewebsites.net_ |
| \*.contoso.com (carattere jolly) | CNAME | _\*_ | _&lt;appname&gt;.azurewebsites.net_ |

Salvare le impostazioni.

Query DNS devono iniziare a risolvere tooyour app del servizio App immediatamente dopo l'operazione di propagazione DNS.

## <a name="next-steps"></a>Passaggi successivi

Informazioni su come toobind un SSL personalizzato certificato tooApp servizio.

> [!div class="nextstepaction"]
> [Associare un esistente personalizzato SSL certificato tooAzure App Web](app-service-web-tutorial-custom-ssl.md)

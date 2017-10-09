---
title: aaaMap un DNS personalizzato esistente nome app Web tooAzure | Documenti Microsoft
description: Informazioni su come tooadd un dominio DNS personalizzato esistente nome app web di tooa (dominio personale), back-end dell'app mobile o app per le API in Azure App Service.
services: app-service\web
documentationcenter: nodejs
author: cephalin
manager: erikre
editor: 
ms.assetid: dc446e0e-0958-48ea-8d99-441d2b947a7c
ms.service: app-service-web
ms.workload: web
ms.tgt_pltfrm: na
ms.devlang: nodejs
ms.topic: tutorial
ms.date: 06/23/2017
ms.author: cephalin
ms.custom: mvc
ms.openlocfilehash: 2c4eea3c56c758ca11355554321ffa52dd2c6b9d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="map-an-existing-custom-dns-name-tooazure-web-apps"></a>Eseguire il mapping di un esistente personalizzato DNS nome tooAzure App Web

Le [app Web di Azure](app-service-web-overview.md) forniscono un servizio di hosting Web ad alta scalabilità e con funzioni di auto-correzione. Questa esercitazione viene illustrato come assegnare un nome app Web tooAzure toomap un DNS personalizzato esistente.

![Spostamento del portale tooAzure app](./media/app-service-web-tutorial-custom-domain/app-with-custom-dns.png)

In questa esercitazione si apprenderà come:

> [!div class="checklist"]
> * Eseguire il mapping di un sottodominio (ad esempio, `www.contoso.com`) usando un record CNAME
> * Eseguire il mapping di un dominio radice (ad esempio, `contoso.com`) usando un record A
> * Eseguire il mapping di un dominio con caratteri jolly (ad esempio, `*.contoso.com`) usando un record CNAME
> * Automatizzare il mapping dei domini con script

È possibile utilizzare un **record CNAME** o **un record** toomap un DNS personalizzato nome tooApp servizio. 

> [!NOTE]
> È consigliabile usare un record CNAME per tutti i nomi DNS personalizzati tranne il dominio radice (ad esempio, `contoso.com`).

toomigrate un sito in tempo reale e il relativo tooApp nome di dominio DNS del servizio, vedere [eseguire la migrazione di un tooAzure di nome DNS del servizio App active](app-service-custom-domain-name-migrate.md).

## <a name="prerequisites"></a>Prerequisiti

toocomplete questa esercitazione:

* [Creare un'app del servizio app](/azure/app-service/) oppure usare un'app creata per un'altra esercitazione.
* Acquistare un nome di dominio e assicurarsi di disporre del Registro di sistema di accesso toohello DNS per il provider del dominio (ad esempio GoDaddy).

  Ad esempio, le voci DNS tooadd per `contoso.com` e `www.contoso.com`, è necessario essere in grado di tooconfigure hello impostazioni DNS hello `contoso.com` dominio radice.

  > [!NOTE]
  > Se non è un dominio esistente nome, prendere in considerazione [acquisto di un dominio utilizzando hello Azure portal](custom-dns-web-site-buydomains-web-app.md). 

## <a name="prepare-hello-app"></a>Preparare l'applicazione hello

toomap un personalizzato DNS nome tooa dell'app web, app web hello [piano di servizio App](https://azure.microsoft.com/pricing/details/app-service/) deve essere un livello a pagamento (**Shared**, **base**, **Standard**, o  **Premium**). In questo passaggio assicurarsi che il servizio App app è in hello hello supportato piano tariffario.

### <a name="sign-in-tooazure"></a>Accedi tooAzure

Aprire hello [portale di Azure](https://portal.azure.com) e accedere con l'account di Azure.

### <a name="navigate-toohello-app-in-hello-azure-portal"></a>Passare toohello app nel portale di Azure hello

Scegliere dal menu a sinistra hello **servizi App**e quindi selezionare il nome di hello di app hello.

![Spostamento del portale tooAzure app](./media/app-service-web-tutorial-custom-domain/select-app.png)

Verrà visualizzata hello pagina di gestione di app del servizio App hello.  

<a name="checkpricing"></a>

### <a name="check-hello-pricing-tier"></a>Controllo hello piano tariffario

Hello navigazione della pagina dell'app hello a sinistra, scorrere toohello **impostazioni** sezione e selezionare **scalabilità verticale (piano di servizio App)**.

![Menu di scalabilità verticale](./media/app-service-web-tutorial-custom-domain/scale-up-menu.png)

livello corrente dell'applicazione Hello è evidenziato da un bordo blu. Verificare che tale applicazione hello non hello toomake **libero** livello. DNS personalizzato non è supportato in hello **libero** livello. 

![Controllare il piano tariffario](./media/app-service-web-tutorial-custom-domain/check-pricing-tier.png)

Se hello piano di servizio App non è **libero**, chiudere hello **scegliere il piano tariffario** pagina e andare troppo[mapping di un record CNAME](#cname).

<a name="scaleup"></a>

### <a name="scale-up-hello-app-service-plan"></a>Applicare la scalabilità verticale hello piano di servizio App

Selezionare uno dei livelli di hello non disponibili (**Shared**, **base**, **Standard**, o **Premium**). 

Fare clic su **Seleziona**.

![Controllare il piano tariffario](./media/app-service-web-tutorial-custom-domain/choose-pricing-tier.png)

Quando viene visualizzata hello previa notifica, l'operazione di ridimensionamento hello è stata completata.

![Conferma operazione di scalabilità](./media/app-service-web-tutorial-custom-domain/scale-notification.png)

<a name="cname"></a>

## <a name="map-a-cname-record"></a>Esecuzione del mapping di un record CNAME

Nell'esempio di esercitazione hello, si aggiunge un record CNAME per hello `www` sottodominio (ad esempio, `www.contoso.com`).

[!INCLUDE [Access DNS records with domain provider](../../includes/app-service-web-access-dns-records.md)]

### <a name="create-hello-cname-record"></a>Creare record CNAME hello

Aggiungere un toomap record CNAME nome host predefinito dell'app un sottodominio toohello (`<app_name>.azurewebsites.net`).

Per hello `www.contoso.com` esempio dominio, aggiungere un record CNAME che esegue il mapping nome hello `www` troppo`<app_name>.azurewebsites.net`.

Dopo aver aggiunto hello CNAME, pagina record DNS di hello aspetto hello di esempio seguente:

![Spostamento del portale tooAzure app](./media/app-service-web-tutorial-custom-domain/cname-record.png)

### <a name="enable-hello-cname-record-mapping-in-azure"></a>Abilitare il mapping di record CNAME hello in Azure

Nel riquadro di spostamento della pagina app hello sinistro nel portale di Azure hello di hello, selezionare **i domini personalizzati**. 

![Menu del dominio personalizzato](./media/app-service-web-tutorial-custom-domain/custom-domain-menu.png)

In hello **i domini personalizzati** pagina dell'applicazione hello, aggiungere hello personalizzato nome DNS completo (`www.contoso.com`) toohello elenco.

Seleziona hello  **+**  icona Avanti troppo**aggiungere hostname**.

![Aggiunta del nome host](./media/app-service-web-tutorial-custom-domain/add-host-name-cname.png)

Aggiungere un record CNAME per, ad esempio nome di dominio completo di tipo hello `www.contoso.com`. 

Selezionare **Convalida**.

Hello **aggiungere hostname** pulsante è attivato. 

Assicurarsi che **tipo di record Hostname** è troppo**CNAME (www.example.com o qualsiasi sottodominio)**.

Selezionare **Aggiungi il nome host**.

![Aggiungere app toohello di nome DNS](./media/app-service-web-tutorial-custom-domain/validate-domain-name-cname.png)

Potrebbe richiedere del tempo hello nuovo nome host toobe riportate nella finestra dell'applicazione hello **i domini personalizzati** pagina. Provare ad aggiornare dati hello tooupdate di hello del browser.

![Record CNAME aggiunto](./media/app-service-web-tutorial-custom-domain/cname-record-added.png)

Se manca un passaggio o apportate a un errore di digitazione in un punto precedente, viene visualizzato un errore di verifica nella parte inferiore di hello della pagina hello.

![Errore di verifica](./media/app-service-web-tutorial-custom-domain/verification-error-cname.png)

<a name="a"></a>

## <a name="map-an-a-record"></a>Esecuzione del mapping di un record A

Nell'esempio di esercitazione hello, aggiungere un record A per il dominio radice hello (ad esempio, `contoso.com`). 

<a name="info"></a>

### <a name="copy-hello-apps-ip-address"></a>Copiare l'indirizzo IP dell'applicazione hello

toomap un record, è necessario un indirizzo IP esterno dell'applicazione hello. È possibile trovare questo indirizzo IP in app di hello **i domini personalizzati** pagina hello portale di Azure.

Nel riquadro di spostamento della pagina app hello sinistro nel portale di Azure hello di hello, selezionare **i domini personalizzati**. 

![Menu del dominio personalizzato](./media/app-service-web-tutorial-custom-domain/custom-domain-menu.png)

In hello **i domini personalizzati** copiare l'indirizzo IP dell'applicazione hello.

![Spostamento del portale tooAzure app](./media/app-service-web-tutorial-custom-domain/mapping-information.png)

[!INCLUDE [Access DNS records with domain provider](../../includes/app-service-web-access-dns-records.md)]

### <a name="create-hello-a-record"></a>Creare record hello

app tooan record toomap un servizio App richiede **due** record DNS:

- Un **A** registrare l'indirizzo IP dell'app toohello toomap.
- Oggetto **TXT** record nome host predefinito dell'app toohello toomap `<app_name>.azurewebsites.net`. Servizio App Usa questo record solo in fase di configurazione, che si è proprietari di dominio personalizzato hello tooverify. Dopo che il dominio personalizzato è stato convalidato e configurato nel servizio app, è possibile eliminare il record TXT. 

Per hello `contoso.com` esempio dominio, creare record TXT e in base toohello nella tabella seguente, hello (`@` in genere rappresenta hello dominio radice). 

| Tipo di record | Host | Valore |
| - | - | - |
| Una  | `@` | Indirizzo IP da [indirizzo IP dell'applicazione hello copia](#info) |
| TXT | `@` | `<app_name>.azurewebsites.net` |

Quando vengono aggiunti record hello, pagina record DNS hello aspetto hello di esempio seguente:

![Pagina dei record DNS](./media/app-service-web-tutorial-custom-domain/a-record.png)

<a name="enable-a"></a>

### <a name="enable-hello-a-record-mapping-in-hello-app"></a>Abilitare un mapping di record nell'app hello hello

Dell'applicazione hello **i domini personalizzati** pagina hello portale di Azure, aggiungere hello personalizzato nome DNS completo (ad esempio, `contoso.com`) toohello elenco.

Seleziona hello  **+**  icona Avanti troppo**aggiungere hostname**.

![Aggiunta del nome host](./media/app-service-web-tutorial-custom-domain/add-host-name.png)

Nome di dominio completo tipo hello è configurato il record A hello, ad esempio `contoso.com`.

Selezionare **Convalida**.

Hello **aggiungere hostname** pulsante è attivato. 

Assicurarsi che **tipo di record Hostname** è troppo**un record (example.com)**.

Selezionare **Aggiungi il nome host**.

![Aggiungere app toohello di nome DNS](./media/app-service-web-tutorial-custom-domain/validate-domain-name.png)

Potrebbe richiedere del tempo hello nuovo nome host toobe riportate nella finestra dell'applicazione hello **i domini personalizzati** pagina. Provare ad aggiornare dati hello tooupdate di hello del browser.

![Record A aggiunto](./media/app-service-web-tutorial-custom-domain/a-record-added.png)

Se manca un passaggio o apportate a un errore di digitazione in un punto precedente, viene visualizzato un errore di verifica nella parte inferiore di hello della pagina hello.

![Errore di verifica](./media/app-service-web-tutorial-custom-domain/verification-error.png)

<a name="wildcard"></a>

## <a name="map-a-wildcard-domain"></a>Esecuzione del mapping di un dominio con caratteri jolly

Nell'esempio di esercitazione hello, si esegue il mapping un [nome DNS jolly](https://en.wikipedia.org/wiki/Wildcard_DNS_record) (ad esempio, `*.contoso.com`) toohello app del servizio App aggiungendo un record CNAME. 

[!INCLUDE [Access DNS records with domain provider](../../includes/app-service-web-access-dns-records.md)]

### <a name="create-hello-cname-record"></a>Creare record CNAME hello

Aggiungere un toomap record CNAME nome host predefinito dell'applicazione di toohello nome con caratteri jolly (`<app_name>.azurewebsites.net`).

Per hello `*.contoso.com` esempio dominio hello record CNAME verrà eseguito il mapping nome hello `*` troppo`<app_name>.azurewebsites.net`.

Quando viene aggiunto hello CNAME, pagina record DNS hello aspetto hello di esempio seguente:

![Spostamento del portale tooAzure app](./media/app-service-web-tutorial-custom-domain/cname-record-wildcard.png)

### <a name="enable-hello-cname-record-mapping-in-hello-app"></a>Abilitare il mapping di record CNAME hello in app hello

È ora possibile aggiungere qualsiasi sottodominio corrispondente hello jolly nome toohello app (ad esempio, `sub1.contoso.com` e `sub2.contoso.com` corrispondono `*.contoso.com`). 

Nel riquadro di spostamento della pagina app hello sinistro nel portale di Azure hello di hello, selezionare **i domini personalizzati**. 

![Menu del dominio personalizzato](./media/app-service-web-tutorial-custom-domain/custom-domain-menu.png)

Seleziona hello  **+**  icona Avanti troppo**aggiungere hostname**.

![Aggiunta del nome host](./media/app-service-web-tutorial-custom-domain/add-host-name-cname.png)

Digitare un nome di dominio completo corrispondente hello jolly dominio (ad esempio, `sub1.contoso.com`), quindi selezionare **convalida**.

Hello **aggiungere hostname** pulsante è attivato. 

Assicurarsi che **tipo di record Hostname** è troppo**record CNAME (www.example.com o qualsiasi sottodominio)**.

Selezionare **Aggiungi il nome host**.

![Aggiungere app toohello di nome DNS](./media/app-service-web-tutorial-custom-domain/validate-domain-name-cname-wildcard.png)

Potrebbe richiedere del tempo hello nuovo nome host toobe riportate nella finestra dell'applicazione hello **i domini personalizzati** pagina. Provare ad aggiornare dati hello tooupdate di hello del browser.

Seleziona hello  **+**  icona tooadd nuovamente un altro nome host al dominio con caratteri jolly hello. Ad esempio, aggiungere `sub2.contoso.com`.

![Record CNAME aggiunto](./media/app-service-web-tutorial-custom-domain/cname-record-added-wildcard2.png)

## <a name="test-in-browser"></a>Prova nel browser

Individuare i nomi DNS toohello configurata in precedenza (ad esempio, `contoso.com`, `www.contoso.com`, `sub1.contoso.com`, e `sub2.contoso.com`).

![Spostamento del portale tooAzure app](./media/app-service-web-tutorial-custom-domain/app-with-custom-dns.png)

## <a name="automate-with-scripts"></a>Automatizzazione con gli script

È possibile automatizzare la gestione dei domini personalizzati con gli script, utilizzando hello [CLI di Azure](/cli/azure/install-azure-cli) o [Azure PowerShell](/powershell/azure/overview). 

### <a name="azure-cli"></a>Interfaccia della riga di comando di Azure 

Hello comando seguente consente di aggiungere una configurazione personalizzata DNS nome tooan app del servizio App. 

```bash 
az appservice web config hostname add \
    --webapp <app_name> \
    --resource-group <resource_group_name> \ 
    --name <fully_qualified_domain_name> 
``` 

Per ulteriori informazioni, vedere [eseguire il mapping di un'app web di dominio personalizzato tooa](scripts/app-service-cli-configure-custom-domain.md). 

### <a name="azure-powershell"></a>Azure PowerShell 

Hello comando seguente consente di aggiungere una configurazione personalizzata DNS nome tooan app del servizio App. 

```PowerShell  
Set-AzureRmWebApp `
    -Name <app_name> `
    -ResourceGroupName <resource_group_name> ` 
    -HostNames @("<fully_qualified_domain_name>","<app_name>.azurewebsites.net") 
```

Per ulteriori informazioni, vedere [assegnare un'app web di dominio personalizzato tooa](scripts/app-service-powershell-configure-custom-domain.md).

## <a name="next-steps"></a>Passaggi successivi

In questa esercitazione si è appreso come:

> [!div class="checklist"]
> * Eseguire il mapping di un sottodominio usando un record CNAME
> * Eseguire il mapping di un dominio radice usando un record A
> * Eseguire il mapping di un dominio con caratteri jolly usando un record CNAME
> * Automatizzare il mapping dei domini con script

Spostare toolearn esercitazione successiva toohello come toobind un SSL personalizzato certificato tooa web app.

> [!div class="nextstepaction"]
> [Associare un esistente personalizzato SSL certificato tooAzure App Web](app-service-web-tutorial-custom-ssl.md)

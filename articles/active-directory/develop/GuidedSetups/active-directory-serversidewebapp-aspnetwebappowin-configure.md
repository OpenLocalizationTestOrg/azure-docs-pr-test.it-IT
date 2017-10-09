---
title: aaaAzure AD v2 ASP.NET Web Server Getting Started - Config | Documenti Microsoft
description: Implementazione di accessi Microsoft in una soluzione ASP.NET con un'applicazione tradizionale basata su Web browser tramite lo standard OpenID Connect
services: active-directory
documentationcenter: dev-center-name
author: andretms
manager: mbaldwin
editor: 
ms.assetid: 820acdb7-d316-4c3b-8de9-79df48ba3b06
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 05/09/2017
ms.author: andret
ms.custom: aaddev
ms.openlocfilehash: e666be4622ad30aaa1e12e49ae56bbe1e129b2a9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
## <a name="create-an-application-express"></a>Creare un'applicazione (Rapida)
Ora è necessario tooregister l'applicazione in hello *portale di registrazione dell'applicazione Microsoft*:
1. Registrare l'applicazione tramite hello [portale di registrazione dell'applicazione di Microsoft](https://apps.dev.microsoft.com/portal/register-app?appType=serverSideWebApp&appTech=aspNetWebAppOwin&step=configure)
2.  Immettere un nome per l'applicazione e l'indirizzo di posta elettronica
3.  Verificare che sia selezionata l'opzione hello per l'installazione guidata
4.  Seguire le istruzioni di hello tooadd un'applicazione tooyour l'URL di reindirizzamento

## <a name="add-your-application-registration-information-tooyour-solution-advanced"></a>Aggiungere la soluzione di tooyour informazioni di registrazione applicazione (avanzate)
Ora è necessario tooregister l'applicazione in hello *portale di registrazione dell'applicazione Microsoft*:
1. Passare toohello [portale di registrazione dell'applicazione Microsoft](https://apps.dev.microsoft.com/portal/register-app) tooregister un'applicazione
2. Immettere un nome per l'applicazione e l'indirizzo di posta elettronica 
3.  Verificare che l'opzione hello per l'installazione guidata non è selezionata
4.  Fare clic su `Add Platform`, quindi selezionare `Web`
5.  Tornare indietro tooVisual Studio e, in Esplora soluzioni selezionare il progetto di hello e osservare hello proprietà finestra (se non viene visualizzata una finestra delle proprietà, premere F4)
6.  Modificare anche SSL abilitato`True`
7.  Copia URL SSL hello e aggiungere questo elenco toohello URL di reindirizzamento URL nell'elenco del portale di registrazione hello di URL di reindirizzamento:<br/><br/>![Proprietà del progetto](media/active-directory-serversidewebapp-aspnetwebappowin-configure/vsprojectproperties.png)<br />
8.  Aggiungere il seguente hello in `web.config` ubicato nella cartella radice hello nella sezione hello `configuration\appSettings`:

```xml
<add key="ClientId" value="Enter_the_Application_Id_here" />
<add key="redirectUri" value="Enter_the_Redirect_URL_here" />
<add key="Tenant" value="common" />
<add key="Authority" value="https://login.microsoftonline.com/{0}/v2.0" /> 
```
<!-- Workaround for Docs conversion bug -->
<ol start="9">
<li>
Sostituire `ClientId` con hello Id applicazione appena registrato
</li>
<li>
Sostituire `redirectUri` con hello URL SSL del progetto
</li>
</ol>
<!-- End Docs -->

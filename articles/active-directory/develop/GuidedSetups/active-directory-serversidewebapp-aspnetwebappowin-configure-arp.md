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
ms.openlocfilehash: badc47e131290a56a507592f944a0fc7093260a6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
## <a name="configure-your-aspnet-web-app-with-hello-applications-registration-information"></a>Configurare l'App Web ASP.NET con le informazioni di registrazione dell'applicazione hello

In questo passaggio si configurare il toouse progetto SSL e quindi utilizzare le informazioni di registrazione dell'applicazione hello URL SSL tooconfigure. Successivamente, aggiungere un'applicazione hello' soluzione tooyour informazioni di registrazione tramite *Web. config*.

1.  In Esplora soluzioni selezionare il progetto hello e analizzare hello `Properties` finestra (se non viene visualizzata una finestra delle proprietà, premere F4)
2.  Modifica `SSL Enabled` troppo`True`
3.  Copiare il valore di hello da `SSL URL` in precedenza e incollarlo in hello `Redirect URL` campo nella parte superiore di hello di questa pagina, quindi fare clic su *aggiornamento*:<br/><br/>![Proprietà del progetto](media/active-directory-serversidewebapp-aspnetwebappowin-configure/vsprojectproperties.png)<br />
4.  Aggiungere il seguente hello in `web.config` file si trova nella cartella della radice sezione `configuration\appSettings`:

```xml
<add key="ClientId" value="[Enter hello application Id here]" />
<add key="RedirectUri" value="[Enter hello Redirect URL here]" />
<add key="Tenant" value="common" />
<add key="Authority" value="https://login.microsoftonline.com/{0}/v2.0" /> 
```

---
title: aaaManage accesso toocloud App limitando - tenant di Azure | Documenti Microsoft
description: Come toouse restrizioni Tenant toomanage quali utenti possono accedere le applicazioni in base al proprio tenant di Azure AD.
services: active-directory
documentationcenter: 
author: kgremban
manager: femila
editor: yossib
ms.assetid: 
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/10/2017
ms.author: kgremban
ms.openlocfilehash: 6470fa217738b29104353ae17a2f53216f825c19
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="use-tenant-restrictions-toomanage-access-toosaas-cloud-applications"></a>Utilizzare le applicazioni cloud Tenant restrizioni toomanage accesso tooSaaS

Le organizzazioni di grandi dimensioni che evidenziano sicurezza desidera toomove toocloud servizi come Office 365, ma tooknow necessità che possono accedere solo agli utenti approvati risorse. In genere, le aziende limitano i nomi di dominio o gli indirizzi IP quando desiderano accedere toomanage. Questo approccio non è efficace in situazioni dove le app SaaS vengono ospitate in un cloud pubblico ed eseguite su nomi di dominio condivisi come outlook.office.com e login.microsoftonline.com. Questi indirizzi di blocco è consigliabile mantenere gli utenti di accedere a Outlook Web hello interamente, anziché semplicemente limitando le risorse e le identità tooapproved.

Richiesta di verifica della Azure Active Directory soluzione toothis è una funzionalità denominata restrizioni Tenant. Tenant restrizioni consente alle organizzazioni toocontrol accesso tooSaaS cloud le applicazioni, in base all'utilizzo di applicazioni hello tenant hello Azure AD per single sign-on. È ad esempio, applicazioni di Office 365 dell'organizzazione di tooallow accesso tooyour, impedendo le istanze di accesso tooother delle organizzazioni di queste stesse applicazioni.  

Consente alle organizzazioni hello possibilità toospecify hello elenco di restrizioni di tenant che gli utenti sono autorizzati tooaccess del tenant. Azure AD quindi concede solo tenant toothese consentito l'accesso.

Questo articolo è incentrato sulle restrizioni di Tenant per Office 365, ma la funzionalità hello dovrebbe funzionare con qualsiasi app di cloud SaaS che usa i protocolli di autenticazione moderna con Azure AD per single sign-on. Se si usa l'App con un annuncio di Azure diversi tenant di hello tenant usato da Office 365 SaaS, assicurarsi che tutti necessari tenant sono consentiti. Per ulteriori informazioni sulle app di SaaS cloud, vedere hello [Active Directory Marketplace](https://azure.microsoft.com/en-us/marketplace/active-directory/).

## <a name="how-it-works"></a>Funzionamento

Hello complessiva soluzione comprende hello seguenti componenti: 

1. **Azure AD** : se hello `Restrict-Access-To-Tenants: <permitted tenant list>` è presente, Azure AD rilascia token di sicurezza per hello consentito tenant. 

2. **Infrastruttura del server proxy locale** – un dispositivo proxy in grado di ispezione SSL intestazione hello tooinsert configurato contenente hello elenco di tenant è consentito in traffico di Azure AD. 

3. **Il software client** – toosupport Tenant restrizioni, il software client deve richiedere i token direttamente da Azure AD, in modo che il traffico possa essere intercettato dall'infrastruttura del proxy hello. Restrizioni dei tenant è attualmente supportata nelle applicazioni Office 365 basate su browser e nei client Office dove vengono usate tecniche di autenticazione moderne come OAuth 2.0. 

4. **L'autenticazione moderna** : servizi cloud è necessario utilizzare l'autenticazione moderna toouse Tenant restrizioni e bloccare l'accesso a tooall non autorizzata tenant. Servizi di Office 365 cloud devono essere configurato toouse protocolli di autenticazione moderna per impostazione predefinita. Per informazioni più recenti di hello sul supporto di Office 365 per l'autenticazione moderna, vedere [autenticazione moderna di Office 365 aggiornato](https://blogs.office.com/2015/11/19/updated-office-365-modern-authentication-public-preview/).

Hello seguente diagramma illustra il flusso di traffico di alto livello hello. Ispezione SSL è necessaria solo per il traffico tooAzure AD, non ai servizi cloud di toohello Office 365. Questa distinzione è importante perché il volume di traffico hello per l'autenticazione tooAzure Active Directory è in genere molto inferiore di quelle applicazioni tooSaaS volume di traffico come Exchange Online e SharePoint Online.

![Flusso di traffico di Restrizioni dei tenant, diagramma](./media/active-directory-tenant-restrictions/traffic-flow.png)

## <a name="set-up-tenant-restrictions"></a>Impostare Restrizioni dei tenant

Esistono due passaggi tooget, avviata con restrizioni di Tenant. Hello primo passaggio è assicurarsi che i client possono connettersi indirizzi destra toohello toomake. Hello in secondo luogo è tooconfigure l'infrastruttura del proxy.

### <a name="urls-and-ip-addresses"></a>URL e indirizzi IP

toouse Tenant restrizioni, i client devono essere in grado di tooconnect toohello seguenti URL di Azure AD tooauthenticate: login.microsoftonline.com login.microsoft.com e login.windows.net. Inoltre, tooaccess Office 365, i client devono essere in grado di tooconnect toohello FQDN o URL e gli indirizzi IP definito in [gli intervalli di indirizzi IP e gli URL di Office 365](https://support.office.com/article/Office-365-URLs-and-IP-address-ranges-8548a211-3fe7-47cb-abb1-355ea5aa88a2). 

### <a name="proxy-configuration-and-requirements"></a>Configurazione e requisiti del proxy

Hello seguente configurazione è necessario tooenable Tenant restrizioni tramite l'infrastruttura del proxy. Questa guida è generica, pertanto è consigliabile consultare la documentazione del fornitore di tooyour proxy per i passaggi di implementazione specifica.

#### <a name="prerequisites"></a>Prerequisiti

- proxy Hello deve essere tooperform in grado di intercettazione di SSL, l'inserimento di intestazione HTTP e le destinazioni di filtro con FQDN o URL. 

- I client devono considerare attendibile la catena di certificati hello presentata dal proxy hello per le comunicazioni SSL. Ad esempio, se si utilizzano i certificati rilasciati da un'infrastruttura PKI interna, hello interno emittente certificato certificato dell'autorità radice deve essere attendibile.

- Questa funzionalità è inclusa nelle sottoscrizioni di Office 365, ma se si desidera che le app SaaS di toouse restrizioni Tenant toocontrol accesso tooother licenze di Azure AD Premium 1 sono necessari.

#### <a name="configuration"></a>Configurazione

Per ogni toologin.microsoftonline.com richiesta in ingresso, login.microsoft.com e login.windows.net, inserire due intestazioni HTTP: *limitare l'accesso al tenant* e *contesto di limitare l'accesso*.

intestazioni Hello devono includere hello seguenti elementi: 
- Per *limitare l'accesso al tenant*, un valore di \<consentito elenco tenant\>, ovvero un elenco delimitato da virgole di tenant desiderato tooallow utenti tooaccess. Qualsiasi dominio registrato con un tenant può essere tenant hello tooidentify utilizzati in questo elenco. Ad esempio, toopermit tooboth Contoso e Fabrikam tenant di accedere, hello coppia nome/valore aspetto:`Restrict-Access-To-Tenants: contoso.onmicrosoft.com,fabrikam.onmicrosoft.com` 
- Per *contesto di limitare l'accesso*, un valore di un ID di directory singola dichiarazione tenant dall'impostazione di restrizioni di Tenant hello. Ad esempio, Contoso come tenant hello che impostare criteri di restrizione Tenant hello toodeclare, coppia nome/valore hello aspetto:`Restrict-Access-Context: 456ff232-35l2-5h23-b3b3-3236w0826f3d`  

> [!TIP]
> È possibile trovare l'ID di directory in hello [portale di Azure](https://portal.azure.com). Accedere come amministratore, selezionare **Azure Active Directory**, quindi selezionare **Proprietà**.

tooprevent agli utenti di inserire le proprie intestazione HTTP con i tenant non riconosciuta, proxy hello deve intestazione limitare l'accesso al tenant di hello tooreplace se è già presente nella richiesta in ingresso hello. 

I client devono essere forzato toouse hello proxy per tutte le richieste toologin.microsoftonline.com login.microsoft.com e login.windows.net. Ad esempio, se i file PAC toodirect utilizzato client toouse hello proxy, gli utenti finali deve non essere in grado di tooedit o disabilitare file PAC hello.

## <a name="hello-user-experience"></a>esperienza utente Hello

Questa sezione illustra l'esperienza di hello per gli utenti finali e amministratori.

### <a name="end-user-experience"></a>Esperienza utente finale

Un utente di esempio si trova in rete di Contoso hello, ma tenta tooaccess hello Fabrikam istanza un' condivisa applicazione SaaS come Outlook online. Se Contoso è un tenant non è consentito per l'istanza, l'utente hello Visualizza hello pagina seguente:

![Pagina di accesso negato per gli utenti in tenant non consentiti](./media/active-directory-tenant-restrictions/end-user-denied.png)

### <a name="admin-experience"></a>Esperienza amministratore

Mentre configurazione delle restrizioni di Tenant viene eseguita sull'infrastruttura di hello proxy aziendale, gli amministratori possono accedere direttamente i report di restrizioni Tenant hello in hello portale di Azure. i report tooview hello, toohello pagina di panoramica di Azure Active Directory e quindi cercare nella casella 'Funzionalità'.

salve per tenant hello specificato come tenant hello contesto di accesso con restrizioni, può utilizzare questo toosee report che accessi tutti bloccato a causa di hello criteri di restrizione di Tenant, tra cui identità hello utilizzata e l'ID di directory di destinazione hello.

![Utilizzare hello Azure tooview portale con restrizioni tentativi di accesso riusciti](./media/active-directory-tenant-restrictions/portal-report.png)

Come altri report di hello portale di Azure, è possibile utilizzare i filtri toospecify hello ambito del report. È possibile usare filtri per utenti, applicazioni, client o intervalli di tempo specifici.

## <a name="office-365-support"></a>Supporto di Office 365

Applicazioni di Office 365 devono soddisfare due criteri toofully supporto Tenant restrizioni:

1. client Hello utilizzato supporta l'autenticazione moderna
2. L'autenticazione moderna è abilitato come protocollo di autenticazione hello predefinito per il servizio cloud hello.

Fare riferimento troppo[autenticazione moderna di Office 365 aggiornato](https://blogs.office.com/2015/11/19/updated-office-365-modern-authentication-public-preview/) per informazioni più recenti di hello in Office client supportano attualmente l'autenticazione moderna. Questa pagina include anche collegamenti tooinstructions per abilitare l'autenticazione moderna su specifici Exchange Online e Skype for Business Online tenant. L'autenticazione moderna è già abilitata per impostazione predefinita in SharePoint Online.

Restrizioni tenant è attualmente supportato dalle applicazioni di Office 365 basati su browser (hello SharePoint del portale di Office, Yammer, siti, Outlook sul hello Web, ecc.). Per i thick client come Outlook, Skype for Business, Word, Excel, PowerPoint e così via, Restrizioni dei tenant può essere applicata solo quando si usa l'autenticazione moderna.  

Outlook e Skype per i client di Business che supportano l'autenticazione moderna sono comunque toouse protocolli legacy contro i tenant in cui non è abilitata l'autenticazione moderna, in modo efficace ignorando le restrizioni di Tenant. Per Outlook su Windows, i clienti possono scegliere restrizioni tooimplement impedire agli utenti finali di aggiungere non approvato account tootheir profili di posta elettronica. Ad esempio, vedere hello [impedisce l'aggiunta di account di Exchange non predefinito](http://gpsearch.azurewebsites.net/default.aspx?ref=1) impostazione di criteri di gruppo. Per Outlook su piattaforme non Windows e per Skype for Business su tutte le piattaforme, il supporto completo per le restrizioni del tenant non è attualmente disponibile.

## <a name="testing"></a>Test

Se si desidera tootry le restrizioni di Tenant prima di implementarlo per l'intera organizzazione, sono disponibili due opzioni: un approccio basato su host utilizzando uno strumento come Fiddler o un'implementazione per fasi delle impostazioni del proxy.

### <a name="fiddler-for-a-host-based-approach"></a>Fiddler per un approccio basato su host

Fiddler è un proxy che possono essere utilizzati toocapture e modificano il traffico HTTP/HTTPS, tra cui l'inserimento di intestazioni HTTP per debug gratuitamente dal web. tooconfigure Fiddler tootest restrizioni Tenant, eseguire hello alla procedura seguente:

1.  [Scaricare e installare Fiddler](http://www.telerik.com/fiddler).
2.  Configurare il traffico HTTPS toodecrypt Fiddler, per ogni [documentazione della Guida di Fiddler](http://docs.telerik.com/fiddler/Configure-Fiddler/Tasks/DecryptHTTPS).
3.  Configurare hello tooinsert Fiddler *limitare l'accesso al tenant* e *contesto di limitare l'accesso* intestazioni usando le regole personalizzate:
  1. Nello strumento Debugger Web Fiddler hello selezionare hello **regole** dal menu **personalizzare le regole...** file di CustomRules tooopen hello.
  2. Aggiungere hello seguenti righe all'inizio di hello di hello *OnBeforeRequest* (funzione). Sostituire il \<dominio del tenant\> con un dominio registrato con il proprio tenant, ad esempio contoso.onmicrosoft.com. Sostituire \<l'ID della directory\> con l'identificatore GUID di Azure AD del proprio tenant.

  ```
  if (oSession.HostnameIs("login.microsoftonline.com") || oSession.HostnameIs("login.microsoft.com") || oSession.HostnameIs("login.windows.net")){      oSession.oRequest["Restrict-Access-To-Tenants"] = "<tenant domain>";      oSession.oRequest["Restrict-Access-Context"] = "<directory ID>";}
  ```

  Se è necessario tooallow più tenant, usare un nome di tenant hello tooseparate valori delimitati da virgole. ad esempio:

  ```
  oSession.oRequest["Restrict-Access-To-Tenants"] = "contoso.onmicrosoft.com,fabrikam.onmicrosoft.com";
  ```

4. Salvare e chiudere file CustomRules hello.

Dopo aver configurato Fiddler, è possibile acquisire il traffico da passare toohello **File** menu e selezionando **acquisire il traffico**.

### <a name="staged-rollout-of-proxy-settings"></a>Implementazione per fasi delle impostazioni del proxy

A seconda delle funzionalità di hello dell'infrastruttura di proxy, potrebbe essere implementazione hello toostage in grado di impostazioni tooyour che gli utenti. Di seguito sono indicate due opzioni generali da tenere in considerazione:

1.  Utilizzare PAC file toopoint test utenti tooa test infrastruttura del proxy, dall'infrastruttura del proxy toouse hello produzione mentre agli utenti normali.
2.  Alcuni server proxy possono supportare configurazioni diverse usando i gruppi.

Consultare la documentazione del server proxy tooyour per informazioni dettagliate.

## <a name="next-steps"></a>Passaggi successivi

- Informazioni sull'[autenticazione moderna aggiornata di Office 365](https://blogs.office.com/2015/11/19/updated-office-365-modern-authentication-public-preview/)

- Hello revisione [gli intervalli di indirizzi IP e gli URL di Office 365](https://support.office.com/article/Office-365-URLs-and-IP-address-ranges-8548a211-3fe7-47cb-abb1-355ea5aa88a2)

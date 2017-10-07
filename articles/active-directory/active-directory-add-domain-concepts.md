---
title: Panoramica di aaaConceptual di nomi di dominio personalizzati in Azure Active Directory | Documenti Microsoft
description: Viene spiegato concettuale hello per l'utilizzo di nomi di dominio personalizzati in Azure Active directory, compresa la federazione per single sign-on
services: active-directory
documentationcenter: 
author: curtand
manager: femila
editor: 
ms.assetid: fd0c5def-0da2-43af-81bc-76f4cfe86afd
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/25/2017
ms.author: curtand
ms.openlocfilehash: 0a3454ae6b733a8a13a71925df3cc664063f388e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="conceptual-overview-of-custom-domain-names-in-azure-active-directory"></a>Panoramica concettuale dei nomi di dominio personalizzati in Azure Active Directory
Un nome di dominio può essere un identificatore importante per molte risorse della directory, come parte di:

* Un nome utente o un indirizzo di posta elettronica di un utente
* indirizzo Hello per un gruppo
* URI ID app Hello per un'applicazione

Una risorsa in Azure Active Directory (Azure AD) può includere un nome di dominio che è già verificato toobe proprietà directory hello che contiene risorse hello. Solo un amministratore globale può eseguire attività di gestione del dominio in Azure AD.

> [!IMPORTANT]
> Si consiglia di gestire Azure AD usando la hello [centro di amministrazione di Azure AD](https://aad.portal.azure.com) in hello portale di Azure anziché hello portale di Azure classico a cui fa riferimento in questo articolo. Per modalità toomanage i nomi di dominio nel centro di amministrazione di hello Azure AD, vedere [gestione dei nomi di dominio personalizzati in Azure Active Directory](active-directory-domains-manage-azure-portal.md).

I nomi di dominio in Azure AD sono univoci. Un nome di dominio personalizzato può essere usato da un solo tenant di Azure AD per volta. Se una directory di Azure AD ha verificato un nome di dominio, nessun'altra directory di Azure AD può verificare o usare lo stesso nome di dominio.

## <a name="initial-and-custom-domain-names"></a>Nomi di dominio iniziali e personalizzati
Ogni nome di dominio in Azure AD è un nome di dominio iniziale o un nome di dominio personalizzato.

Ogni AD Azure viene fornito con un nome di dominio iniziale nel hello formato contoso.onmicrosoft.com. Il nome di dominio di livello terzo, in questo esempio "contoso.onmicrosoft.com", è stato stabilito quando hello directory è stata creata, in genere dall'amministratore di hello che ha creato la directory hello. nome di dominio iniziale Hello per una directory non può essere modificato o eliminato. nome di dominio iniziale Hello, benché completamente funzionanti, è destinato principalmente toobe utilizzato come meccanismo di avvio fino a un nome di dominio personalizzato viene verificata.

Nella maggior parte degli ambienti di produzione, una directory ha almeno un dominio personalizzato verificato, ad esempio, "contoso.com", e è il dominio personalizzato che gli utenti tooend visibile. Un nome di dominio personalizzato, ad esempio "contoso.com", è un nome di dominio di proprietà dall'organizzazione che lo usa ad esempio come hosting del sito Web. Questo nome di dominio è familiare tooemployees perché è parte del nome utente di hello che utilizzano toosign nella rete aziendale toohello o toosend e recuperare la posta elettronica.

Prima di e può essere utilizzato da Azure AD, il nome di dominio personalizzato hello deve essere directory tooyour aggiunto e verificato.

## <a name="verified-and-unverified-domain-names"></a>Nomi di dominio verificati e non verificati
nome di dominio iniziale Hello per una directory viene valutato in modo implicito come risulta da Azure AD. Quando un amministratore aggiunge un tooan di nome di dominio personalizzato AD Azure, è inizialmente in uno stato non verificato. Azure AD non consentirà qualsiasi toouse risorse directory un nome di dominio non verificato. Ciò garantisce che solo una directory è possibile utilizzare un nome di dominio e che l'organizzazione di hello utilizza il nome di dominio hello effettivamente proprietario di tale nome di dominio.

Azure AD verifica la proprietà di un nome di dominio mediante la ricerca di una voce specifica nel file hello domain name service (DNS) zona per il nome di dominio di hello. proprietà tooverify di un nome di dominio, un amministratore ottiene voce DNS hello da Azure AD che avrà un aspetto Azure AD e aggiunge file di zona DNS toohello tale voce per il nome di dominio di hello. file di zona DNS Hello viene gestito dal nome di dominio di hello per quel dominio. Hello passaggi tooverify un dominio vengono visualizzati nell'articolo hello per [aggiunta di una directory di dominio personalizzato AD Azure tooyour](active-directory-add-domain.md).

Aggiunta di un file di zona toohello voce DNS per il nome di dominio di hello non influenza gli altri servizi di dominio, ad esempio posta elettronica o di hosting web.

## <a name="federated-and-managed-domain-names"></a>Nomi di dominio federati e gestiti
Un nome di dominio personalizzato in Azure AD possono essere configurato toogive utenti un accesso federato esperienza tra Active Directory locale e Azure AD. Per configurare un dominio per la federazione richiede aggiornamenti tooprivileged risorse in Azure AD e anche tooyour Windows Server Active Directory. La configurazione di un dominio federato deve essere completata da Azure AD Connect o tramite PowerShell. La federazione di un dominio personalizzato non può essere avviata dal portale di Azure classico hello. [Guardare questo video toolearn sulla configurazione di ADFS per l'accesso degli utenti con Azure AD Connect](http://channel9.msdn.com/Series/Azure-Active-Directory-Videos-Demos/Configuring-AD-FS-for-user-sign-in-with-Azure-AD-Connect).

I domini non federati sono talvolta detti domini gestiti. dominio iniziale di Hello per una directory di Azure AD viene valutata in modo implicito come un dominio gestito.

## <a name="primary-domain-names"></a>Nomi di dominio primari
nome di dominio primario per una directory Hello è hello nome di dominio che è già selezionato come valore predefinito di hello per parte dominio' hello' nome utente di hello, quando un amministratore crea un nuovo utente in hello [portale di Azure](https://portal.azure.com/), o un altro portale ad esempio il portale di amministrazione di Office 365 hello o il portale di Microsoft Intune hello. Una directory può avere un solo nome di dominio primario. Un amministratore può modificare toobe nome di dominio primario hello qualsiasi dominio personalizzato verificato che non è federato o toohello iniziale al dominio.

## <a name="domain-names-in-azure-ad-and-other-microsoft-online-services"></a>Nomi di dominio in Azure AD e altri Microsoft Online Services
Un nome di dominio deve essere verificato in Azure AD prima che possa essere usato da altri Microsoft Online Services, ad esempio Exchange Online, SharePoint Online e Intune. Questi altri servizi in genere richiedono un amministratore tooadd uno o più voci DNS presenti toohello particolare servizio.

Un'app web di Azure Usa proprietà di tooverify un proprio meccanismo di un dominio. Un dominio deve essere verificato per l'uso con Azure AD anche se è stato già verificato per l'uso con un'app Web di Azure in una sottoscrizione che si basa su Azure AD. Un'app web di Azure è possibile utilizzare un nome di dominio che è stato verificato in una directory diversa dalla directory hello che protegge hello web app.

## <a name="managing-domain-names"></a>Gestione dei nomi di dominio
È possibile completare l'attività di gestione dal portale di Azure classico hello e da PowerShell. È possibile completare molte attività tramite l'API di Azure AD Graph hello.

* [Aggiunta e verifica di un nome di dominio personalizzato](active-directory-add-domain.md)
* [Gestione dei domini nel portale di Azure classico hello](active-directory-add-manage-domain-names.md)
* [Utilizzo di PowerShell toomanage i nomi di dominio in Azure AD](https://msdn.microsoft.com/library/azure/e1ef403f-3347-4409-8f46-d72dafa116e0#BKMK_ManageDomains)
* [Utilizzando i nomi di dominio toomanage hello API Azure AD Graph di Azure AD](https://msdn.microsoft.com/Library/Azure/Ad/Graph/api/domains-operations)


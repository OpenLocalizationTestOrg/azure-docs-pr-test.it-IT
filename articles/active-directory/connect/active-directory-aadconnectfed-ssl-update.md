---
title: 'Azure AD Connect: Certificato SSL aggiornamento hello per una farm di Active Directory Federation Services (ADFS) | Documenti Microsoft'
description: Questo documento dettagli hello passaggi tooupdate hello certificato SSL di una farm di ADFS con Azure AD Connect.
services: active-directory
keywords: azure ad connect, aggiornamento ssl ad fs, aggiornamento certificato ad fs, modifica certificato ad fs, nuovo certificato ad fs, certificato ad fs, aggiornare certificato ssl ad fs, aggiornare ad fs certificato ssl, configurare certificato ssl ad fs, ad fs, ssl, certificato, certificato comunicazioni di servizio ad fs, aggiornare federazione, configurare federazione, aad connect
authors: anandyadavmsft
manager: femila
editor: billmath
ms.assetid: 7c781f61-848a-48ad-9863-eb29da78f53c
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/02/2017
ms.author: anandy
ms.openlocfilehash: bce7f75aab83b6abacb8472a6895054d137e10e0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="update-hello-ssl-certificate-for-an-active-directory-federation-services-ad-fs-farm"></a>Aggiorna il certificato SSL di hello per una farm di Active Directory Federation Services (ADFS)

## <a name="overview"></a>Panoramica
In questo articolo viene descritto come utilizzare certificato SSL di Azure AD Connect tooupdate hello per una farm di Active Directory Federation Services (ADFS). È possibile utilizzare un certificato SSL hello Azure AD Connect strumento tooeasily aggiornamento hello per farm ADFS hello AD anche se hello utente metodo di accesso selezionato non è AD FS.

È possibile eseguire l'intera operazione di hello di aggiornamento certificato SSL per la farm di hello AD FS in tutti i server Proxy applicazione Web (WAP) in tre passaggi semplici e federazione:

![Tre passaggi](./media/active-directory-aadconnectfed-ssl-update/threesteps.png)


>[!NOTE]
>toolearn ulteriori informazioni sui certificati utilizzati da ADFS, vedere [informazioni sui certificati utilizzati da ADFS](https://technet.microsoft.com/library/cc730660.aspx).

## <a name="prerequisites"></a>Prerequisiti

* **Farm AD FS**: assicurarsi che la farm AD FS sia basata su Windows Server 2012 R2 o versioni successive.
* **Azure AD Connect**: verificare che hello versione di Azure AD Connect è 1.1.443.0 o versione successiva. Si userà attività hello **certificato SSL ADFS aggiornamento AD**.

![Attività Aggiorna il certificato SSL di AD FS](./media/active-directory-aadconnectfed-ssl-update/updatessltask.png)

## <a name="step-1-provide-ad-fs-farm-information"></a>Passaggio 1: Specificare informazioni sulla farm AD FS

Azure AD Connect tenta automaticamente da tooobtain informazioni farm di hello AD FS:
1. Esecuzione di query su informazioni relative alla farm hello da ADFS (Windows Server 2016 o versione successiva).
2. Un riferimento a informazioni hello esecuzioni precedenti, che vengono archiviate localmente con Azure AD Connect.

È possibile modificare l'elenco di hello del server che vengono visualizzati aggiungendo o rimuovendo hello server tooreflect hello configurazione corrente delle farm di hello AD FS. Non appena viene forniti informazioni sul server hello, Azure AD Connect consente di visualizzare la connettività hello e stato corrente del certificato SSL.

![Informazioni sui server AD FS](./media/active-directory-aadconnectfed-ssl-update/adfsserverinfo.png)

Se l'elenco di hello contiene un server che non è più parte della farm ADFS hello Active Directory, fare clic su **rimuovere** server hello toodelete dall'elenco di hello del server nella farm ADFS.

![Server offline nell'elenco](./media/active-directory-aadconnectfed-ssl-update/offlineserverlist.png)

>[!NOTE]
> Rimozione di un server dall'elenco di hello del server per AD FS farm in Azure AD Connect è un'operazione locale e aggiornamenti hello informazioni per hello farm ADFS in locale da Azure AD Connect. Azure AD Connect non modifica la configurazione hello su ADFS tooreflect hello modifica.    

## <a name="step-2-provide-a-new-ssl-certificate"></a>Passaggio 2: Specificare un nuovo certificato SSL

Dopo aver verificato informazioni hello sui server della farm di ADFS, Azure AD Connect richiede nuovo certificato SSL di hello. Fornire un'installazione di hello di protetto da password PFX certificato toocontinue.

![Certificato SSL](./media/active-directory-aadconnectfed-ssl-update/certificate.png)

Dopo aver fornito il certificato di hello, Azure AD Connect passa attraverso una serie di prerequisiti. Verificare tooensure certificato hello che hello certificato sia corretta per la farm ADFS hello:

-   Hello nome soggetto alternativo di nome/soggetto certificato hello è hello stesso come nome del servizio federativo hello oppure è un certificato con caratteri jolly.
-   certificato di Hello è valido per più di 30 giorni.
-   catena di certificati Hello è valido.
-   certificato Hello è protetto da password.

## <a name="step-3-select-servers-for-hello-update"></a>Passaggio 3: Selezionare i server per l'aggiornamento di hello

Nel passaggio successivo hello, selezionare Server hello che richiedono i certificati SSL di hello toohave aggiornata. Impossibile selezionare i server che non sono in linea per l'aggiornamento di hello.

![Selezionare i server tooupdate](./media/active-directory-aadconnectfed-ssl-update/selectservers.png)

Dopo aver completato la configurazione hello, Azure AD Connect consente di visualizzare il messaggio hello che indica lo stato di hello dell'aggiornamento hello e fornisce un'opzione tooverify hello ADFS Accedi.

![Configurazione completata](./media/active-directory-aadconnectfed-ssl-update/configurecomplete.png)   

## <a name="faqs"></a>Domande frequenti

* **Quale deve essere hello nome del soggetto hello certificato per il certificato SSL di AD FS nuovo hello?**

    Azure AD Connect controlla se hello soggetto alternativo di nome/nome del soggetto hello certificato contiene il nome di servizio federativo hello. Ad esempio, se il nome del servizio federativo è fs.contoso.com, nome soggetto di nome/alternativo del soggetto hello deve essere fs.contoso.com.  Sono accettati anche certificati con caratteri jolly.

* **Motivo per cui viene chiesto di credenziali nuovamente nella pagina server WAP di hello?**

    Se credenziali hello specificate per la connessione server ADFS tooAD non dispongono anche di server WAP di hello privilegio toomanage hello, Azure AD Connect richiede le credenziali che dispongono di privilegi amministrativi sui server WAP hello.

* **server Hello viene visualizzato come offline. Cosa devo fare?**

    Azure AD Connect non è possibile eseguire qualsiasi operazione se hello server è offline. Se server hello fa parte di hello farm AD FS, controllare server toohello di connettività hello. Dopo avere risolto il problema di hello, premere hello aggiornamento icona tooupdate hello dello stato nella procedura guidata hello. Se il server di hello faceva parte di hello farm in precedenza, ma ora non esiste più, fare clic su **rimuovere** toodelete dall'elenco di hello del server che si connettono AD Azure gestisce. Rimozione di server hello dall'elenco di hello in Azure AD Connect non modifica hello stessa configurazione di ADFS. Se si usa ADFS in Windows Server 2016 o versione successiva, hello server rimane nelle impostazioni di configurazione hello e verrà visualizzato nuovamente hello successivo hello attività viene eseguita.

* **È possibile aggiornare un sottoinsieme di my Server farm con nuovo certificato SSL di hello?**

    Sì. È sempre possibile eseguire attività di hello **certificato SSL di aggiornamento** nuovamente i hello tooupdate server rimanenti. In hello **selezionare i server per SSL certificato aggiornamento** pagina, è possibile ordinare l'elenco di hello del server in **data di scadenza SSL** tooeasily i server di hello di accesso che non sono ancora aggiornati.

* **Rimosso server hello hello precedente esecuzione, ma ancora viene visualizzato come offline ed è elencato nella pagina di annuncio hello server ADFS. Anche dopo che è stato rimosso, perché è ancora presenti server offline hello?**

    Rimozione di server hello dall'elenco di hello in Azure AD Connect non rimuoverlo in hello configurazione di ADFS. Azure AD Connect fa riferimento AD FS (Windows Server 2016 o versioni successive) per qualsiasi informazione sulla farm hello. Se il server di hello è ancora presente nella configurazione di ADFS hello, sarà elencato in elenco hello.  

## <a name="next-steps"></a>Passaggi successivi

- [Azure AD Connect e federazione](active-directory-aadconnectfed-whatis.md)
- [Gestione e personalizzazione di Active Directory Federation Services con Azure AD Connect](active-directory-aadconnect-federation-management.md)

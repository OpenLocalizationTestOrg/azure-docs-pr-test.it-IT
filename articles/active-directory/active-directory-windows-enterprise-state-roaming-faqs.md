---
title: aaaSettings e dati in roaming domande frequenti | Documenti Microsoft
description: Fornisce le risposte toosome domande gli amministratori IT potrebbero essere sulle impostazioni e sincronizzazione dei dati di app.
services: active-directory
keywords: impostazioni di enterprise state roaming, cloud windows, domande frequenti su enterprise state roaming
documentationcenter: 
author: tanning
manager: swadhwa
editor: curtand
ms.assetid: c0824f5c-129b-4240-969f-921f6a64eae7
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/08/2017
ms.author: markvi
ms.openlocfilehash: 4d6d6619b3a5fbd1d274603808d89b73ed942cd7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="settings-and-data-roaming-faq"></a>Domande frequenti su impostazioni e dati in roaming
Questo argomento fornisce le risposte ad alcune possibili domande degli amministratori IT in merito alle impostazioni e alla sincronizzazione dei dati delle app.

## <a name="what-data-roams"></a>Quali tipi di dati sono disponibili in roaming?
**Impostazioni di Windows**: hello impostazioni PC incorporate nel sistema operativo di Windows hello. In genere, si tratta di impostazioni di personalizzare il PC e includono hello ampie categorie seguenti:

* *Tema*, che include caratteristiche come il tema del desktop e le impostazioni della barra delle applicazioni.
* *Impostazioni di Internet Explorer*, tra cui le schede e i Preferiti aperti di recente.
* *Impostazioni del browser Edge*, come i Preferiti e l'elenco di lettura.
* *Password*, tra cui le password Internet, i profili Wi-Fi e così via.
* *Preferenze della lingua*, tra cui le impostazioni di layout della tastiera, lingua del sistema, data e ora e così via.
* *Caratteristiche di accessibilità*, come i temi a contrasto elevato, l'Assistente vocale e la Lente di ingrandimento.
* *Altre impostazioni di Windows*, ad esempio le impostazioni del prompt dei comandi e l'elenco delle applicazioni.

**Dati dell'applicazione**: app universali di Windows è possibile scrivere tooa dati impostazioni roaming cartella e verranno sincronizzati automaticamente tutti i dati scritti toothis cartella. È attivo toohello singole app developer toodesign un vantaggio tootake app di questa funzionalità. Per ulteriori informazioni su come toodevelop un'app di Windows universale che usa il roaming, vedere hello [API di archiviazione appdata](https://msdn.microsoft.com/library/windows/apps/mt299098.aspx) hello e [appdata Windows 8 roaming blog per sviluppatori](http://blogs.msdn.com/b/windowsappdev/archive/2012/07/17/roaming-your-app-data.aspx).

## <a name="what-account-is-used-for-settings-sync"></a>Quale account si usa per la sincronizzazione delle impostazioni?
In Windows 8 e Windows 8.1 la sincronizzazione delle impostazione usa sempre gli account Microsoft per utenti. Gli utenti aziendali era hello possibilità tooconnect un tootheir account Microsoft toosettings sincronizzazione di Active Directory dominio account toogain accesso. In Windows 10 la funzione di questo account Microsoft connesso è stata sostituita da un framework di account principale/secondario.

account principale Hello è definito come account di hello usato toosign in tooWindows. Può essere un account Microsoft, un account Azure Active Directory (Azure AD), un account Active Directory locale oppure un account locale. In account principale toohello addizione, gli utenti di Windows 10 possono aggiungere uno o più dispositivi tootheir di account cloud secondario. Un account secondario è in genere un account Microsoft, un account Azure AD o un altro account, ad esempio Gmail o Facebook. Questi account secondari forniscono accesso tooadditional servizi, ad esempio accesso single sign-on e hello Windows Store, ma non sono in grado di sincronizzazione delle impostazioni di accensione.

In Windows 10, solo hello account principale per il dispositivo di hello può essere utilizzato per la sincronizzazione delle impostazioni (vedere [come l'aggiornamento di sincronizzazione delle impostazioni dell'account Microsoft nella sincronizzazione delle impostazioni tooAzure Active Directory di Windows 8 in Windows 10?](active-directory-windows-enterprise-state-roaming-faqs.md#how-do-i-upgrade-from-microsoft-account-settings-sync-in-windows-8-to-azure-ad-settings-sync-in-windows-10)).

Dati non sono mai mixed tra hello diversi account utente sul dispositivo hello. Esistono due regole per la sincronizzazione delle impostazioni:

* Impostazioni di Windows verranno sempre effettuato il roaming con account principale hello.
* I dati dell'App verranno contrassegnati con l'applicazione hello tooacquire di hello account utilizzato. Verranno sincronizzate solo le app contrassegnate con l'account principale hello. Tag di proprietà App viene determinato quando un'app è sideload tramite hello Windows Store o di gestione dei dispositivi mobili (MDM).

Se non è possibile identificare il proprietario di un'app, verrà effettuato il roaming con account principale hello. Se un dispositivo viene aggiornato da Windows 8 o Windows 8.1 tooWindows 10, tutte le app hello verranno contrassegnate come acquisito dall'account Microsoft hello. In questo modo la maggior parte degli utenti di acquisire le app tramite Windows Store hello e si è verificato alcun supporto di Windows Store per Azure AD account precedente tooWindows 10. Se un'applicazione viene installata tramite una licenza non in linea, hello app verrà contrassegnato utilizzando l'account principale hello sul dispositivo hello.

> [!NOTE]
> I dispositivi Windows 10 che sono proprietà dell'azienda e tooAzure connesso AD non possono più connettersi all'account di dominio tooa account Microsoft. Hello possibilità tooconnect un account di dominio tooa account Microsoft e la sincronizzazione dei dati dell'utente di hello tutti toohello Microsoft account, vale a dire hello Microsoft account roaming tramite account Microsoft hello connesso e le funzionalità di Active Directory viene rimosso da I dispositivi Windows 10 che vengono unite in join tooa connesso Active Directory o l'ambiente di Azure AD.
>
>

## <a name="how-do-i-upgrade-from-microsoft-account-settings-sync-in-windows-8-tooazure-ad-settings-sync-in-windows-10"></a>Come aggiornare dalla sincronizzazione delle impostazioni dell'account Microsoft nella sincronizzazione delle impostazioni tooAzure Active Directory di Windows 8 in Windows 10?
Se si toohello aggiunti a un dominio di Active Directory in esecuzione Windows 8 o Windows 8.1 con un account Microsoft collegato, si verranno impostazioni di sincronizzazione tramite il tuo account Microsoft. Dopo l'aggiornamento tooWindows 10, si continuerà impostazioni utente toosync tramite account Microsoft fino a quando un utente di dominio e il dominio di Active Directory hello non si connette con Azure AD.

Se hello locale collegare il dominio di Active Directory con Azure AD, il dispositivo tenterà impostazioni toosync utilizzando account di Azure AD hello connesso. Se l'amministratore hello Azure AD non abilitare Enterprise State Roaming connessa account Azure AD verrà interrotta la sincronizzazione delle impostazioni. Se un utente di Windows 10 accede con un'identità di Azure AD, potrà iniziare a sincronizzare le impostazioni di Windows non appena l'amministratore abiliterà questa funzione tramite Azure AD.

Se è stato archiviato nel dispositivo azienda dei dati personali, è necessario tenere presente che del sistema operativo Windows e i dati dell'applicazione verranno avviata la sincronizzazione di Active Directory tooAzure. Questo approccio sono hello seguenti implicazioni:

* Le impostazioni dell'account Microsoft personale verranno dello sfasamento oltre alle impostazioni di hello del lavoro o scuola account Azure AD. Infatti, account di Microsoft hello e le impostazioni di Azure AD sincronizzati utilizzano account distinti.
* I dati personali come le password Wi-Fi, le credenziali Web e i Preferiti di Internet Explorer in precedenza sincronizzati tramite un account Microsoft connesso ora saranno sincronizzati tramite Azure AD.

## <a name="how-do-microsoft-account-and-azure-ad-enterprise-state-roaming-interoperability-work"></a>Come funziona l'interoperabilità fra l'account Microsoft e l'Enterprise State Roaming di Azure AD?
In hello novembre 2015 o versioni successive di Windows 10 Enterprise State Roaming è supportato solo per un singolo account alla volta. Se si accede tooWindows tramite un lavoro o scuola account Azure Active Directory, tutti i dati verranno sincronizzati tramite Azure AD. Se si accede tooWindows utilizzando un account Microsoft personale, tutti i dati verranno sincronizzati tramite hello account Microsoft. Verrà effettuato il roaming appdata universale usando solo hello primario account di accesso nel dispositivo hello e verrà effettuato il roaming solo se la licenza dell'applicazione hello è di proprietà di account principale hello. Non verrà sincronizzato appdata universale per le app hello di proprietà di qualsiasi account secondario.

## <a name="do-settings-sync-for-azure-ad-accounts-from-multiple-tenants"></a>È possibile sincronizzare le impostazioni per gli account Azure AD da più tenant?
Quando Azure AD più account da diversi tenant di Azure AD si trovano in hello stesso dispositivo, è necessario aggiornare toocommunicate del Registro di sistema del dispositivo hello con Azure Rights Management (Azure RMS) per ogni tenant di Azure AD.  

1. Trovare hello GUID per ogni tenant di Azure AD. Aprire hello portale di Azure classico e selezionare un tenant di Azure AD. Hello GUID per il tenant hello è hello URL nella barra degli indirizzi del browser hello. Ad esempio: `https://manage.windowsazure.com/YourAccount.onmicrosoft.com#Workspaces/ActiveDirectoryExtension/Directory/Tenant GUID/directoryQuickStart`
2. Dopo aver hello GUID, sarà necessario chiave del Registro di sistema di hello tooadd **HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows\SettingSync\WinMSIPC\<ID GUID del tenant >**.
   Da hello **ID GUID del tenant** chiave, creare un nuovo valore multistringa (MULTI-REG-SZ) denominato **AllowedRMSServerUrls**. Per i propri dati, specificare hello licenze URL dei punti di distribuzione di hello altri tenant di Azure che hello gli accessi ai dispositivi.
3. È possibile trovare l'URL dei punti di distribuzione di licenze eseguendo hello hello **Get-AadrmConfiguration** cmdlet. Se i valori hello per hello **LicensingIntranetDistributionPointUrl** e **LicensingExtranetDistributionPointUrl** sono diversi, specificare entrambi i valori. Se i valori sono hello hello stesso, è possibile specificare solo una volta al valore di hello.

## <a name="what-are-hello-roaming-settings-options-for-existing-windows-desktop-applications"></a>Quali sono hello roaming le opzioni delle impostazioni per le applicazioni desktop di Windows esistente?
Il roaming è disponibile solo per le app di Windows universale. Sono disponibili due opzioni per l'abilitazione del roaming in un'applicazione desktop di Windows esistente:

* Hello [Desktop Bridge](http://aka.ms/desktopbridge) consente di introdurre il toohello di applicazioni desktop di Windows esistente Universal Windows Platform. Da qui, quantità minima di codice le modifiche saranno necessari tootake sfruttare roaming dati applicazione Azure AD. Hello Bridge Desktop fornisce le app con un'identità di applicazione, che è necessario tooenable dati delle app mobili per applicazioni desktop esistenti.
* [User Experience Virtualization (UE-V)](https://technet.microsoft.com/library/dn458947.aspx) consente di creare un modello di impostazioni personalizzate per le app desktop di Windows esistenti e di abilitare il roaming per le applicazioni Win32. Questa opzione non richiede codice toochange di hello app dello sviluppatore dell'applicazione hello. UE-V è comune per i clienti che hanno acquistato Microsoft Desktop Optimization Pack hello limitati tooon locale Active Directory.

Gli amministratori possono configurare i dati dell'app desktop Windows tooroam UE-V modificando il roaming delle impostazioni del sistema operativo Windows e dei dati di app universale tramite [criteri di gruppo UE-V](https://technet.microsoft.com/itpro/mdop/uev-v2/configuring-ue-v-2x-with-group-policy-objects-both-uevv2), tra cui:

* Eseguendo il roaming dei criteri di gruppo delle impostazioni di Windows
* Non sincronizzando i criteri di gruppo delle app Windows
* Nella sezione applicazioni hello comuni di Internet Explorer

In futuro hello, Microsoft potrebbe analizzare toomake modi CHE UE-V è perfettamente integrata in Windows ed estendere le impostazioni di tooroam UE-V tramite hello cloud di Azure AD.

## <a name="can-i-store-synced-settings-and-data-on-premises"></a>È possibile archiviare in locale le impostazioni e i dati sincronizzati?
Enterprise State Roaming archivia tutti i dati sincronizzati in hello cloud di Azure. La soluzione di roaming locale è disponibile in UE-V.

## <a name="who-owns-hello-data-thats-being-roamed"></a>Chi possiede i dati di hello che sono in corso roaming?
le aziende Hello proprie hello dati in roaming tramite Enterprise State Roaming. I dati vengono archiviati in un data center di Azure. Tutti i dati utente vengono crittografati in transito e inattivi nel cloud hello con Azure RMS. Si tratta di una miglioramento rispetto tooMicrosoft impostazioni basate su account la sincronizzazione, che crittografa solo alcuni dati sensibili quali le credenziali utente prima che il dispositivo hello.

Microsoft è impegnata toosafeguarding i dati dei clienti. I dati delle impostazioni di ogni utente aziendale vengono crittografati automaticamente tramite Azure RMS prima che lascino il dispositivo Windows 10, per impedire agli altri utenti di leggerli. Se l'organizzazione dispone di una sottoscrizione a pagamento per Azure RMS, è possibile utilizzare altre funzionalità di Azure RMS, ad esempio tenere traccia e revocare i documenti, automaticamente proteggere messaggi di posta elettronica che contengono informazioni riservate e gestire chiavi personalizzate (hello anche la soluzione "bring your own key", noto come BYOK). Per ulteriori informazioni su queste funzionalità e sul funzionamento di Azure RMS, vedere l' [articolo descrittivo su Azure Rights Management](https://technet.microsoft.com/jj585026.aspx).

## <a name="can-i-manage-sync-for-a-specific-app-or-setting"></a>È possibile gestire la sincronizzazione per un'app o un'impostazione specifica?
In Windows 10, non è presente alcun toodisable impostazione MDM o criteri di gruppo per una singola applicazione. Gli amministratori del tenant possono disabilitare la sincronizzazione dei dati di tutte le app presenti in un dispositivo gestito, ma non esiste un controllo più dettagliato a livello di singola app o all'interno di ogni app.

## <a name="how-can-i-enable-or-disable-roaming"></a>Come si fa ad abilitare o disabilitare il roaming?
In hello **impostazioni** app, andare troppo**account** > **Sincronizza le impostazioni**. In questa pagina, è possibile visualizzare quale account viene utilizzato tooroam impostazioni ed è possibile abilitare o disabilitare singoli gruppi di impostazioni toobe roaming.

## <a name="what-is-microsofts-recommendation-for-enabling-roaming-in-windows-10"></a>Che cosa consiglia Microsoft per abilitare il roaming in Windows 10?
Microsoft offre alcune soluzioni per il roaming delle impostazioni, inclusi Profili utente mobili, UE-V e Enterprise State Roaming.  Microsoft è impegnata toomaking investimenti in Enterprise State Roaming nelle future versioni di Windows. Se l'organizzazione non è pronta o si ha familiarità con lo spostamento dati toohello nel cloud, è consigliabile utilizzare UE-V come la tecnologia di roaming primaria. Se l'organizzazione richiede supporto per le applicazioni desktop di Windows esistente roaming ma toomove eager toohello cloud, è consigliabile utilizzare sia Enterprise stato Roaming e UE-V. Per quanto simili, UE-V ed Enterprise State Roaming non si escludono a vicenda. Complementari toohelp assicurarsi che l'organizzazione fornisca hello roaming servizi che servono agli utenti.  

Quando si utilizza Enterprise State Roaming e UE-V, applica hello seguenti regole:

* Enterprise State Roaming è hello agente primario di roaming sul dispositivo hello. UE-V viene utilizzato toosupplement hello "gap Win32".
* Per le impostazioni di Windows e i dati dell'app UWP moderni UE-V deve essere disabilitata quando i criteri di gruppo hello UE-V. poiché già incluso in Enterprise State Roaming.

## <a name="how-does-enterprise-state-roaming-support-virtual-desktop-infrastructure-vdi"></a>In che modo Enterprise State Roaming supporta la Virtual Desktop Infrastructure (VDI)?
Enterprise State Roaming è supportato sulle SKU dei client Windows 10, ma non su quelle dei server. Se una VM client si trova in una macchina hypervisor e si accede in remoto nella macchina virtuale toohello, verranno effettuato il roaming dei dati. Se più utenti condividono hello stesso sistema operativo e gli utenti accedono in modalità remota il server tooa per un'esperienza desktop completi, roaming potrebbe non funzionare. scenario basato sulla sessione quest'ultimo Hello non è ufficialmente supportato.

## <a name="what-happens-when-my-organization-purchases-azure-rms-after-using-roaming"></a>Cosa accade quando l'organizzazione acquista Azure RMS dopo aver utilizzato il roaming?
Se l'organizzazione sta già utilizzando il roaming in Windows 10 con hello sottoscrizione gratuita limitazioni d'uso di Azure RMS, acquistare una sottoscrizione a pagamento di Azure RMS verrà non hanno alcun impatto sulla funzionalità hello di roaming di hello e modifiche alla configurazione non saranno richiesto dall'amministratore IT.

## <a name="known-issues"></a>Problemi noti
Vedere la documentazione di hello in hello [risoluzione dei problemi](active-directory-windows-enterprise-state-roaming-troubleshooting.md) sezione per un elenco di problemi noti. 

## <a name="related-topics"></a>Argomenti correlati
* [Panoramica di Enterprise State Roaming](active-directory-windows-enterprise-state-roaming-overview.md)
* [Abilitare Enterprise State Roaming in Azure Active Directory](active-directory-windows-enterprise-state-roaming-enable.md)
* [Criteri di gruppo e impostazioni del software MDM per la sincronizzazione delle impostazioni](active-directory-windows-enterprise-state-roaming-group-policy-settings.md)
* [Riferimento alle impostazioni di roaming di Windows 10](active-directory-windows-enterprise-state-roaming-windows-settings-reference.md)
* [Risoluzione dei problemi](active-directory-windows-enterprise-state-roaming-troubleshooting.md)

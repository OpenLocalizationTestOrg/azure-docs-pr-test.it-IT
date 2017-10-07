---
title: aaaView i report di utilizzo e di accesso | Documenti Microsoft
description: "Viene illustrato come tooview accesso e utilizzo segnala toogain approfondite hello integrità e la sicurezza della directory dell'organizzazione."
services: active-directory
documentationcenter: 
author: dhanyahk
manager: femila
editor: 
ms.assetid: a074bc4e-cf3f-4ad1-8cc6-4199d2e09ce4
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/16/2017
ms.author: dhanyahk;markvi
ms.openlocfilehash: 1c18fd2a327ae8b67f62ce2754f643bdb03514a9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="view-your-access-and-usage-reports"></a>Visualizzare i report di accesso e utilizzo
*Questa documentazione fa parte di hello [Azure Active Directory Reporting Guida](active-directory-reporting-guide.md).*

È possibile utilizzare l'accesso di Azure Active Directory e utilizzo report toogain visibilità hello integrità e sicurezza della directory dell'organizzazione. Con queste informazioni, un amministratore di directory possa meglio stabilire l'origine di possibili rischi per la sicurezza in modo da poter adeguatamente pianificare toomitigate tali rischi.

Nel portale di gestione Azure hello, i report sono suddivisi in hello seguenti modi:

* Report anomalie: contiene eventi di accesso che è stato rilevato toobe anomali. L'obiettivo è toomake si è consapevoli di tale attività e consentono di toobe in grado di toomake aggettivo indicano se un evento è sospetto.
* Report applicazioni integrate: fornisce informazioni dettagliate sull'uso delle applicazioni cloud nell'organizzazione. Azure Active Directory offre l'integrazione con migliaia di applicazioni cloud.
* Report errori: indicano gli errori che possono verificarsi durante il provisioning di applicazioni tooexternal account.
* Report specifici degli utenti: visualizza i dati del dispositivo/dell'attività di accesso per un utente specifico.
* Log attività: contengono un record di tutti gli eventi controllati entro hello ultimi 24 ore, ultimi 7 giorni, o ultimi 30 giorni, nonché le modifiche delle attività di gruppo e attività di registrazione e di reimpostazione della password.

> [!NOTE]
> * Alcuni report di utilizzo di anomalie e risorse avanzati sono disponibili solo quando si abilita [Azure Active Directory Premium](active-directory-get-started-premium.md). Report avanzati consentono migliorare la sicurezza di accesso, rispondere toopotential minacce e ottenere accesso tooanalytics sull'utilizzo di accesso e l'applicazione di dispositivo.
> * Azure Active Directory Premium e le edizioni Basic sono disponibili per i clienti in Cina tramite hello istanza globale di Azure Active Directory. Azure Active Directory Premium e le edizioni Basic non sono attualmente supportate nel servizio di Microsoft Azure hello gestito da 21Vianet in Cina. Per ulteriori informazioni, contattare Microsoft in hello [Forum di Azure Active Directory](https://feedback.azure.com/forums/169401-azure-active-directory/).
> 
> 

## <a name="reports"></a>Report
| Report | Descrizione |
| --- | --- |
| **Report Anomalie dell'attività** | |
| [Accessi da origini sconosciute](active-directory-reporting-sign-ins-from-unknown-sources.md) |Può indicare un tentativo toosign in senza tracciamento. |
| [Accessi dopo più errori](active-directory-reporting-sign-ins-after-multiple-failures.md) |Può indicare un attacco di forza bruta riuscito. |
| [Accessi da più aree geografiche](active-directory-reporting-sign-ins-from-multiple-geographies.md) |Può indicare che più utenti stanno accedendo con hello stesso account. |
| [Accessi da indirizzi IP con attività sospetta](active-directory-reporting-sign-ins-from-ip-addresses-with-suspicious-activity.md) |Può indicare un accesso riuscito in seguito a un prolungato tentativo di intrusione. |
| [Accessi da dispositivi potenzialmente infetti](active-directory-reporting-sign-ins-from-possibly-infected-devices.md) |Può indicare un tentativo toosign in da dispositivi probabilmente infetti. |
| [Attività di accesso irregolare](active-directory-reporting-irregular-sign-in-activity.md) |Può indicare l'accesso degli toousers di eventi anomali nei modelli. |
| [Utenti con anomalie dell'attività di accesso](active-directory-reporting-users-with-anomalous-sign-in-activity.md) |Indica utenti i cui account sono stati compromessi. |
| Utenti con credenziali perse |Utenti con credenziali perse |
| **Log attività** | |
| Report di controllo |Eventi controllati nella directory |
| Attività di reimpostazione password |Fornisce una visualizzazione dettagliata delle reimpostazioni della password all'interno dell'organizzazione. |
| Attività di registrazione reimpostazione password |Fornisce una visualizzazione dettagliata delle registrazioni di reimpostazione della password all'interno dell'organizzazione. |
| Attività dei gruppi self-service |Fornisce un tooall log attività gruppo di attività self-service nella directory |
| **Applicazioni integrate** | |
| Utilizzo applicazioni |Fornisce un riepilogo di utilizzo per tutte le applicazioni SaaS integrate con la directory. |
| Attività di provisioning dell'account |Fornisce una cronologia dei tentativi di applicazioni di tooexternal tooprovision account. |
| Stato rollover della password |Fornisce una panoramica dettagliata dello stato di rollover automatico delle password di applicazioni SaaS. |
| Errori di provisioning dell'account |Indica le applicazioni tooexternal di accesso degli toousers un impatto. |
| **Rights Management** | |
| Utilizzo di RMS |Fornisce un riepilogo dell'utilizzo di Rights Management |
| Utenti RMS più attivi |Visualizza l'elenco dei primi 1000 utenti attivi che hanno eseguito l'accesso ai file protetti con RMS |
| Utilizzo dispositivi RMS |Visualizza l'elenco dei dispositivi usati per accedere ai file protetti con RMS |
| Utilizzo applicazioni abilitate per RMS |Fornisce l'utilizzo delle applicazioni abilitate per RMS |

## <a name="report-editions"></a>Edizioni dei report
| Report | Free | Basic | Premium |
| --- | --- | --- | --- |
| **Report Anomalie dell'attività** | | | |
| Accessi da origini sconosciute |✓ |✓  |✓ |
| Accessi dopo più errori |✓ |✓  |✓ |
| Accessi da più aree geografiche |✓ |✓  |✓ |
| Accessi da indirizzi IP con attività sospetta | | |✓ |
| Accessi da dispositivi potenzialmente infetti | | |✓ |
| Attività di accesso irregolare | | |✓ |
| Utenti con anomalie dell'attività di accesso | | |✓ |
| Utenti con credenziali perse | | |✓ |
| **Log attività** | | | |
| Report di controllo |✓ |✓  |✓ |
| Attività di reimpostazione password | | |✓ |
| Attività di registrazione reimpostazione password | | |✓ |
| Attività dei gruppi self-service | | |✓ |
| **Applicazioni integrate** | | | |
| Utilizzo applicazioni | | |✓ |
| Attività di provisioning dell'account |✓ |✓  |✓ |
| Stato rollover della password | | |✓ |
| Errori di provisioning dell'account |✓ |✓  |✓ |
| **Rights Management** | | | |
| Utilizzo di RMS | | |Solo RMS |
| Utenti RMS più attivi | | |Solo RMS |
| Utilizzo dispositivi RMS | | |Solo RMS |
| Utilizzo applicazioni abilitate per RMS | | |Solo RMS |

## <a name="anomalous-activity-reports"></a>Report Anomalie dell'attività
<p>Hello anomalo accedere nei report di attività flag sospette Accedi tooOffice365 attività, il portale di gestione di Azure, pannello di accesso AD Azure, Sharepoint Online, Dynamics CRM Online e altri Microsoft online services.</p>

<p>Tutti i report seguenti, ad eccezione del fatto hello report "Accessi dopo più errori", anche flag sospette <i>federata</i> firmare aggiuntivi toohello menzionati in precedenza i servizi, indipendentemente dal provider federativo hello. </p>

<p>Hello i report seguenti sono disponibile: </p><ul>

<li>[Accessi da origini sconosciute](active-directory-reporting-sign-ins-from-unknown-sources.md).</li>

<li>[Accessi dopo più errori](active-directory-reporting-sign-ins-after-multiple-failures.md).</li>

<li>[Accessi da più aree geografiche](active-directory-reporting-sign-ins-from-multiple-geographies.md).</li>

<li>[Accessi da indirizzi IP con attività sospetta](active-directory-reporting-sign-ins-from-ip-addresses-with-suspicious-activity.md).</li>

<li>[Attività di accesso irregolare](active-directory-reporting-irregular-sign-in-activity.md).</li>

<li>[Accessi da dispositivi potenzialmente infetti](active-directory-reporting-sign-ins-from-possibly-infected-devices.md).</li>

<li>[Utenti con anomalie dell'attività di accesso](active-directory-reporting-users-with-anomalous-sign-in-activity.md).</li>

<li>Utenti con credenziali perse</li></ul>

## <a name="activity-logs"></a>Log attività
### <a name="audit-report"></a>Report di controllo
| Descrizione | Percorso report |
|:--- |:--- |
| Viene visualizzato un record di tutti gli eventi controllati entro hello ultime 24 ore, ultimi 7 giorni o 30 giorni. <br /> Per altre informazioni, vedere [Eventi del report di controllo di Azure Active Directory](active-directory-reporting-audit-events.md) |Scheda Directory > Report |

![Report di controllo](./media/active-directory-view-access-usage-reports/auditReport.PNG)

### <a name="password-reset-activity"></a>Attività di reimpostazione password
| Descrizione | Percorso report |
|:--- |:--- |
| Vengono illustrati tutti i tentativi di reimpostazione della password che si sono verificati nell'organizzazione. |Scheda Directory > Report |

![Attività di reimpostazione password](./media/active-directory-view-access-usage-reports/passwordResetActivity.PNG)

### <a name="password-reset-registration-activity"></a>Attività di registrazione reimpostazione password
| Descrizione | Percorso report |
|:--- |:--- |
| Vengono illustrate tutte le registrazioni per la reimpostazione della password che si sono verificate nell'organizzazione |Scheda Directory > Report |

![Attività di registrazione reimpostazione password](./media/active-directory-view-access-usage-reports/passwordResetRegistrationActivity.PNG)

### <a name="self-service-groups-activity"></a>Attività dei gruppi self-service
| Descrizione | Percorso report |
|:--- |:--- |
| Mostra tutte le attività dei gruppi gestiti self-service hello nella directory. |Scheda Directory > Utenti > <i>Utente</i> > Dispositivi |

![Attività dei gruppi self-service](./media/active-directory-view-access-usage-reports/selfServiceGroupsActivity.PNG)

## <a name="integrated-applications-reports"></a>Report Applicazioni integrate
### <a name="application-usage-summary"></a>Utilizzo dell'applicazione: riepilogo
| Descrizione | Percorso report |
|:--- |:--- |
| Utilizzare questo report quando si desidera toosee utilizzo per tutte le applicazioni SaaS hello nella directory. Questo report in base hello numero di volte in cui gli utenti hanno fatto clic su un'applicazione hello in hello Pannello di accesso. |Scheda Directory > Report |

Questo report include accessi troppo*tutti* le applicazioni che la directory include l'accesso, incluse le applicazioni Microsoft preintegrate.

Applicazioni di Microsoft preintegrate includono Office 365, Sharepoint, hello portale di gestione di Azure e ad altri utenti.

![Riepilogo utilizzo applicazione](./media/active-directory-view-access-usage-reports/applicationUsage.PNG)

### <a name="application-usage-detailed"></a>Utilizzo dell'applicazione: dettagliato
| Descrizione | Percorso report |
|:--- |:--- |
| Utilizzare questo report quando si desidera toosee quanto un'applicazione SaaS specifica è in uso. Questo report in base hello numero di volte in cui gli utenti hanno fatto clic su un'applicazione hello in hello Pannello di accesso. |Scheda Directory > Report |

### <a name="application-dashboard"></a>Dashboard dell'applicazione
| Descrizione | Percorso report |
|:--- |:--- |
| Questo rapporto indica accesso cumulativo aggiuntivi toohello applicazione gli utenti dell'organizzazione, in un intervallo di tempo selezionato. grafico Hello nella pagina dashboard hello consentono di identificare le tendenze di tutti gli utilizzi dell'applicazione. |Scheda Directory > Applicazione > Dashboard |

## <a name="error-reports"></a>Report di errori
### <a name="account-provisioning-errors"></a>Errori di provisioning dell'account
| Descrizione | Percorso report |
|:--- |:--- |
| Utilizzare questo toomonitor di errori verificatisi durante la sincronizzazione degli account hello tooAzure applicazioni SaaS Active Directory. |Scheda Directory > Report |

![Errori di provisioning dell'account](./media/active-directory-view-access-usage-reports/accountProvisioningErrors.PNG)

## <a name="user-specific-reports"></a>Report specifici degli utenti
### <a name="devices"></a>Dispositivi
| Descrizione | Percorso report |
|:--- |:--- |
| Utilizzare questo report quando si desidera che l'indirizzo IP toosee hello e la posizione geografica dei dispositivi che un utente specifico ha usato tooaccess Azure Active Directory. |Scheda Directory > Utenti > <i>Utente</i> > Dispositivi |

### <a name="activity"></a>Attività
| Descrizione | Percorso report |
|:--- |:--- |
| Mostra hello sign in attività per un utente. report Hello include informazioni quali effettuato l'accesso a un'applicazione hello, dispositivo usato, l'indirizzo IP e il percorso. Microsoft non raccoglie informazioni sulla cronologia hello degli utenti che accedono con un account Microsoft. |Scheda Directory > Utenti > <i>Utente</i> > Attività |

#### <a name="sign-in-events-included-in-hello-user-activity-report"></a>Accedi a eventi inclusi in hello report attività utente
Solo determinati tipi di eventi di accesso verranno visualizzati nel report attività utente hello.

| Tipo evento | Incluso |
| --- | --- |
| Firmare aggiuntivi toohello [Pannello di accesso](http://myapps.microsoft.com/) |Sì |
| Firmare aggiuntivi toohello [il portale di gestione di Azure](https://manage.windowsazure.com/) |Sì |
| Firmare aggiuntivi toohello [portale di Microsoft Azure](https://portal.azure.com/) |Sì |
| Firmare aggiuntivi toohello [portale di Office 365](http://portal.office.com/) |Sì |
| Firmare l'applicazione di tooa nativa aggiuntivi, come Outlook (vedere l'eccezione riportata di seguito) |Sì |
| Firmare app federata provisioning tooa aggiuntivi tramite il pannello di accesso, come Salesforce hello |Sì |
| Firmare app basate su password tooa aggiuntivi tramite il pannello di accesso, ad esempio Twitter hello |Sì |
| Firmare app di business personalizzata tooa aggiuntivi che è stata aggiunta la directory toohello |No (disponibile a breve) |
| Firmare aggiuntivi tooan Proxy dell'applicazione Azure AD app che è stata aggiunta la directory toohello |No (disponibile a breve) |

> Nota: quantità di hello tooreduce di disturbo nel rapporto di accessi da hello [Microsoft Online Services Sign-In Assistant](http://community.office365.com/en-us/w/sso/534.aspx) non vengono visualizzati.
> 
> 

## <a name="things-tooconsider-if-you-suspect-security-breach"></a>Operazioni tooconsider se si sospetta violazione della sicurezza
Se si ritiene che un account utente potrebbe essere compromessa o qualsiasi tipo di attività utente sospetta che possono causare una violazione della sicurezza tooa dei dati della directory nel cloud hello, è possibile tooconsider uno o più delle seguenti azioni hello:

* Attività di hello tooverify utente hello contatto
* Reimpostare la password dell'utente hello
* [Abilitare l'autenticazione a più fattori](../multi-factor-authentication/multi-factor-authentication-get-started.md) per una maggiore sicurezza

## <a name="view-or-download-a-report"></a>Visualizzare o scaricare un report
1. Nel portale di Azure classico hello, fare clic su **Active Directory**, fare clic sul nome della directory dell'organizzazione hello e quindi fare clic su **report**.
2. Nella pagina report hello, fare clic su report hello da tooview e/o scaricare.
   
   > [!NOTE]
   > Se si tratta di hello prima volta che è stato utilizzato hello reporting funzionalità di Azure Active Directory, si noterà tooOpt un messaggio In. Se si accetta, fare clic su toocontinue icona di segno di spunta hello.
   > 
   > 
3. Fare clic su Avanti tooInterval di hello dal menu a discesa e quindi selezionare una delle seguenti intervalli di tempo che devono essere utilizzati durante la generazione di questo report hello:
   
   * Ultime 24 ore
   * Ultimi 7 giorni
   * Ultimi 30 giorni
4. Fare clic hello segno di spunta icona toorun hello report.
   * Backup too1000 eventi verranno visualizzati nel portale di Azure classico hello.
5. Se applicabile, fare clic su **scaricare** toodownload hello report tooa file compresso in formato con valori delimitati da virgole (CSV) per visualizzarlo offline o a scopi di archiviazione.
   * Backup too75, 000 eventi verranno inclusi nel file hello scaricato.
   * Per ulteriori dati, consultare hello [API Azure AD Reporting](active-directory-reporting-api-getting-started.md).

## <a name="ignore-an-event"></a>Ignorare un evento
Se si stanno visualizzando tutti i report anomalie, si noterà che è possibile ignorare vari eventi che vengono visualizzati nei report correlati. tooignore un evento, è sufficiente evidenziare evento hello in report hello e quindi fare clic su **ignora**. Hello **ignora** pulsante rimuoverà definitivamente evento evidenziato hello da report hello e può essere utilizzato solo dagli amministratori globali autorizzati.

## <a name="automatic-email-notifications"></a>Notifiche automatiche tramite posta elettronica
Per altre informazioni sulle notifiche della funzionalità di creazione di report di Azure AD, vedere [Notifiche relative alla funzionalità di creazione di report di Azure Active Directory](active-directory-reporting-notifications.md).

## <a name="whats-next"></a>Passaggi successivi
* [Introduzione ad Azure Active Directory Premium](active-directory-get-started-premium.md)
* [Aggiungere personalizzazione delle pagine di accesso e il pannello di accesso tooyour della società](active-directory-add-company-branding.md)


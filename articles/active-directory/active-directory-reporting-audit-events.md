---
title: eventi report di controllo Active Directory aaaAzure | Documenti Microsoft
description: Eventi controllati disponibili per la visualizzazione e il download dalla propria istanza di Azure Active Directory
services: active-directory
documentationcenter: 
author: dhanyahk
manager: femila
editor: 
ms.assetid: 307eedf7-05bc-448d-a84d-bead5a4c5770
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 06/16/2017
ms.author: dhanyahk;markvi
ms.openlocfilehash: 4a84cce2be56bde006164abf10ad1e72ca6e99bf
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="azure-active-directory-audit-report-events"></a>Eventi del report di controllo di Azure Active Directory
*Questa documentazione fa parte di hello [Azure Active Directory Reporting Guida](active-directory-reporting-guide.md).*

Report di controllo di Azure Active Directory Hello contribuisce ai clienti di identificare le azioni con privilegi che si sono verificati in Azure Active Directory. Le azioni con privilegi includono modifiche elevazione (ad esempio, creazione del ruolo o la reimpostazione della password), modificare le configurazioni di criteri (ad esempio criteri password) o configurazione toodirectory modifiche (ad esempio, le modifiche toodomain impostazioni di federazione). report di Hello forniscono record di controllo hello per nome dell'evento hello, attore hello che ha eseguito l'azione di hello, risorse di destinazione hello interessata dalla modifica hello e hello data e ora (UTC). I clienti sono elenco hello tooretrieve in grado di eventi di controllo per Azure Active Directory tramite hello [portale Azure](https://portal.azure.com/), come descritto in [consente di visualizzare il log di controllo](active-directory-reporting-azure-portal.md).

## <a name="list-of-audit-report-events"></a>Elenco degli eventi del report di controllo
<!--- audit event descriptions should be in hello past tense --->

| Eventi | Descrizione evento |
| --- | --- |
| **Eventi degli utenti** | |
| Aggiunta di un utente |Aggiungere una directory toohello utente. |
| Eliminazione di un utente. |Eliminare un utente dalla directory hello. |
| Impostazione delle proprietà della licenza |Impostare le proprietà di licenza hello per un utente nella directory hello. |
| Reimpostazione password utente |Reimpostare la password di hello per un utente nella directory hello. |
| Modifica password utente |Modifica password hello per un utente nella directory hello. |
| Modifica licenza utente |Modificare licenza hello tooa utente nella directory hello. le licenze sono state aggiornate, cercare nel hello toosee [utente aggiornamento](#update-user-attributes) proprietà riportata di seguito |
| Aggiornamento utente |Aggiornare un utente nella directory hello. [Vedere le informazioni seguenti](#update-user-attributes) per conoscere gli attributi che possono essere aggiornati. |
| Impostazione forzatura per la modifica delle password utente |Impostare proprietà di hello che forza una toochange utente la password dell'account di accesso. |
| Aggiornamento delle credenziali dell'utente |Password modificata hello utente |
| **Eventi del gruppo** | |
| Aggiungi gruppo |Creare un gruppo nella directory hello. |
| Aggiornare un gruppo |Aggiornare un gruppo nella directory hello. toosee sono state aggiornate le proprietà di gruppo, fare riferimento troppo[gruppo controllata la proprietà](#update-group-attributes) nella seguente sezione hello |
| Eliminare gruppo |Eliminare un gruppo dalla directory hello. |
| CreateGroupSettings |Sono state create impostazioni del gruppo. |
| UpdateGroupSettings |Sono state aggiornate impostazioni del gruppo. toosee sono state aggiornate le impostazioni di gruppo, fare riferimento troppo[gruppo controllata la proprietà](#update-group-attributes) nella seguente sezione hello |
| DeleteGroupSettings |Sono state eliminate impostazioni del gruppo. |
| SetGroupLicense |È stata configurata la licenza del gruppo. |
| SetGroupManagedBy |Impostare toobe gruppo gestito dall'utente |
| AddGroupMember |Membro aggiunto toogroup |
| RemoveGroupMember |Rimuovere un membro dal gruppo |
| AddGroupOwner |Proprietario aggiunto toogroup |
| RemoveGroupOwner |È stato rimosso il proprietario dal gruppo. |
| **Eventi dell'applicazione** | |
| Aggiunta di un'entità servizio |Aggiungere una directory toohello dell'entità servizio. |
| Rimozione di un'entità servizio |Rimuovere un'entità servizio da directory di hello. |
| Aggiunta delle credenziali dell'entità servizio |Entità di servizio tooa credenziali aggiunte. |
| Rimozione delle credenziali dell'entità servizio |Sono state rimosse le credenziali da un'entità servizio. |
| Aggiunta di una voce di delega |Creare un [OAuth2PermissionGrant](https://msdn.microsoft.com/Library/Azure/Ad/Graph/api/entity-and-complex-type-reference#oauth2permissiongrant-entity) nella directory hello. |
| Impostazione voce di delega |Aggiornare un [OAuth2PermissionGrant](https://msdn.microsoft.com/Library/Azure/Ad/Graph/api/entity-and-complex-type-reference#oauth2permissiongrant-entity) nella directory hello. |
| Rimozione voce di delega |Eliminare un [OAuth2PermissionGrant](https://msdn.microsoft.com/Library/Azure/Ad/Graph/api/entity-and-complex-type-reference#oauth2permissiongrant-entity) nella directory hello. |
| **Eventi del ruolo** | |
| Aggiungere tooRole membri ruolo |Aggiungere un ruolo della directory tooa utente. |
| Rimozione di un membro ruolo dal ruolo |È stato rimosso un utente da un ruolo della directory. |
| AddRoleDefinition |È stata aggiunta la definizione del ruolo. |
| UpdateRoleDefinition |È stata aggiornata la definizione del ruolo. toosee sono state aggiornate le impostazioni di ruolo, fare riferimento troppo[ruolo definizione proprietà controllata](#update-role-definition-attributes) nella seguente sezione hello |
| DeleteRoleDefinition |È stata eliminata la definizione del ruolo. |
| AddRoleAssignmentToRoleDefinition |Aggiungere una definizione toorole assegnazione di ruolo. |
| RemoveRoleAssignmentFromRoleDefinition |È stata rimossa l'assegnazione del ruolo dalla definizione del ruolo. |
| AddRoleFromTemplate |È stato aggiunto un ruolo dal modello. |
| UpdateRole |È stato aggiornato un ruolo. |
| AddRoleScopeMemberToRole |Aggiungere membri con ambito toorole. |
| RemoveRoleScopedMemberFromRole |È stato rimosso un membro con ambito dal ruolo. |
| **Eventi relativi al dispositivo (eventi nuovi)** | |
| AddDevice |È stato aggiunto un dispositivo. |
| UpdateDevice |È stato aggiornato un dispositivo. toosee sono state aggiornate le proprietà del dispositivo, fare riferimento troppo[delle proprietà del dispositivo Audited](#update-device-attributes) nella seguente sezione hello |
| DeleteDevice |È stato eliminato un dispositivo. |
| AddDeviceConfiguration |È stata aggiunta la configurazione del dispositivo. |
| UpdateDeviceConfiguration |È stata aggiornata la configurazione del dispositivo. toosee sono state aggiornate le proprietà di configurazione del dispositivo, fare riferimento troppo[delle proprietà di configurazione del dispositivo Audited](#update-device-configuration-attributes) nella seguente sezione hello |
| DeleteDeviceConfiguration |È stata eliminata la configurazione del dispositivo. |
| AddRegisteredOwner |Aggiunto toodevice proprietario registrato. |
| AddRegisteredUsers |Aggiunta di utenti registrati toodevice. |
| RemoveRegisteredOwner |Viene rimosso il proprietario registrato dal dispositivo. |
| RemoveRegisteredUsers |Vengono rimossi gli utenti registrati dal dispositivo. |
| RemoveDeviceCredentials |Vengono rimosse le credenziali del dispositivo. |
| **Eventi B2B** | |
| Inviti batch caricati. |Un amministratore ha caricato un file contenente toobe inviti inviati agli utenti di toopartner. |
| Inviti batch elaborati. |Un file contenente gli inviti toopartner utenti è stato elaborato. |
| Invitare gli utenti esterni. |Un utente esterno è stato invitato toohello directory. |
| Riscattare l'invito utente esterno. |Un utente esterno è riscattati directory toohello invito. |
| Aggiungere toogroup utente esterno. |Un utente esterno è stato assegnato l'appartenenza al gruppo di tooa nella directory hello. |
| Assegnare tooapplication utente esterno. |Un utente esterno è stato assegnato l'applicazione tooan accesso diretto. |
| Creazione del tenant virale. |Un nuovo tenant è stato creato in Azure AD dal riscatto invito hello. |
| Creazione dell'utente virale. |Un utente è stato creato in un tenant esistente in Azure AD da riscatto invito hello. |
| **Unità amministrative (eventi nuovi)** | |
| AddAdministrativeUnit |Viene aggiunta un'unità amministrativa. |
| UpdateAdministrativeUnit |Viene aggiornata un'unità amministrativa. toosee sono state aggiornate le proprietà dell'unità amministrativa, vedere troppo[le proprietà dell'unità amministrativa controllata](#update-administrative-unit-attributes) nella seguente sezione hello |
| DeleteAdministrativeUnit |Viene eliminata un'unità amministrativa. |
| AddMemberToAdministrativeUnit |Aggiungere unità tooadministrative membro. |
| RemoveMemberFromAdministrativeUnit |Viene rimosso un membro dall'unità amministrativa. |
| **Eventi della directory** | |
| Aggiungere partner toocompany |Aggiungere una directory toohello partner. |
| Rimozione di un partner dalla società |Rimuovere un partner da directory di hello. |
| DemotePartner |Viene abbassato di livello un partner. |
| Aggiungi dominio toocompany |Aggiungere una directory toohello di dominio. |
| Rimozione di un dominio dalla società |Rimuovere un dominio dalla directory hello. |
| Aggiornamento dominio |Aggiornare un dominio nella directory hello. toosee sono state aggiornate le proprietà di dominio, fare riferimento troppo[proprietà dominio controllati](#update-domain-attributes) nella seguente sezione hello |
| Impostazione dell'autenticazione del dominio |Modificare l'impostazione hello del dominio predefinito per la società hello. |
| Impostazione delle informazioni di contatto della società |Sono state impostate le preferenze di contatto a livello aziendale. Sono inclusi gli indirizzi di posta elettronica per le attività di marketing, oltre alle notifiche tecniche relative ai Microsoft Online Services. |
| Configurazione delle impostazioni di federazione nel dominio |Aggiornamento delle impostazioni di federazione hello per un dominio. |
| Verifica dominio |Verificare un dominio nella directory hello. |
| Verifica del dominio tramite la verifica di posta elettronica |Verificare un dominio nella directory hello utilizzando la verifica di posta elettronica. |
| Impostazione del flag DirSyncEnabled per la società |Impostare la proprietà hello che può essere una directory di Azure AD Sync. |
| Impostazione criteri password |Sono stati impostati vincoli di lunghezza e caratteri per le password utente. |
| Impostazione informazioni società |Informazioni a livello di società hello aggiornato. Vedere hello [Get-MsolCompanyInformation](https://msdn.microsoft.com/library/azure/dn194126.aspx) cmdlet di PowerShell per altri dettagli. |
| SetCompanyAllowedDataLocation |È stata configurata la posizione dei dati consentita per l'azienda. |
| SetCompanyDirSyncEnabled |È stato impostato il flag DirSyncEnabled. |
| SetCompanyDirSyncFeature |È stata configurata la funzionalità Set DirSync. |
| SetCompanyInformation |Sono state configurate le informazioni sull'azienda. |
| SetCompanyMultiNationalEnabled |È stata abilitata la funzionalità multinazionale per l'azienda. |
| SetDirectoryFeatureOnTenant |È stata configurata una funzionalità directory nel tenant. |
| SetTenantLicenseProperties |Sono state configurate le proprietà della licenza del tenant. |
| CreateCompanySettings |Vengono create le impostazioni aziendali. |
| UpdateCompanySettings |Vengono aggiornate le impostazioni aziendali. toosee sono state aggiornate le proprietà della società, fare riferimento troppo[proprietà società controllate](#update-company-attributes) nella seguente sezione hello |
| DeleteCompanySettings |Vengono eliminate le impostazioni aziendali. |
| SetAccidentalDeletionThreshold |È stata configurata la soglia di eliminazioni accidentali. |
| SetRightsManagementProperties |Sono state configurate le proprietà di Rights Management. |
| PurgeRightsManagementProperties |Vengono ripulite configurate le proprietà di Rights Management. |
| UpdateExternalSecrets |Vengono aggiornati i segreti esterni. |
| **Eventi relativi ai criteri (eventi nuovi)** | |
| AddPolicy |Vengono aggiunti criteri. |
| UpdatePolicy |Vengono aggiornati i criteri. |
| DeletePolicy |Vengono eliminati i criteri. |
| AddDefaultPolicyApplication |Aggiungere criteri tooapplication. |
| AddDefaultPolicyServicePrincipal |Aggiungere criteri tooservice entità. |
| RemoveDefaultPolicyApplication |Vengono rimossi criteri dall'applicazione. |
| RemoveDefaultPolicyServicePrincipal |Vengono rimossi criteri dall'entità servizio. |
| RemovePolicyCredentials |Vengono rimosse le credenziali dei criteri. |

## <a name="audit-report-retention"></a>Conservazione dei report di controllo

Per informazioni più recenti di hello sulla conservazione, vedere [criteri di conservazione dei report di Azure Active Directory](active-directory-reporting-retention.md).


Per i clienti che desiderano archiviare gli eventi di controllo per lunghi periodi di conservazione, hello Reporting API può essere tooregularly utilizzati gli eventi di controllo di pull in un archivio dati separato. Vedere [introduzione hello API Reporting](active-directory-reporting-api-getting-started.md) per informazioni dettagliate.

## <a name="properties-included-with-each-audit-event"></a>Proprietà incluse in ogni evento di controllo
| Proprietà | Descrizione |
| --- | --- |
| Data e ora |si è verificato Hello data e ora hello evento di controllo |
| Attore |utente Hello o entità servizio che ha eseguito hello azione |
| Azione |azione di Hello che è stata eseguita |
| Destinazione |utente Hello o entità servizio è stata eseguita l'azione hello |

## <a name="update-user-attributes"></a>Attributi "Aggiornamento utente"
evento di controllo Hello "aggiornamento utente" include informazioni aggiuntive sui quali gli attributi utente sono stati aggiornati. Per ogni attributo, entrambi hello valore precedente e nuovo valore hello è incluso.

| Attributo | Descrizione |
| --- | --- |
| AccountEnabled |Hello utente possa accedere. |
| AssignedLicense |Tutte le licenze che sono state assegnate toohello utente. |
| AssignedPlan |I piani di servizio determinate dalle licenze hello assegnato toohello utente. |
| LicenseAssignmentDetail |Dettagli sulle licenze assegnate toohello utente. Ad esempio, se è stato coinvolto in base al gruppo di licenze, ciò include gruppo hello hello concesse licenze. |
| Mobile |cellulare dell'utente Hello. |
| OtherMail |Hello indirizzo di posta elettronica alternativo dell'utente. |
| OtherMobile |Hello telefono cellulare alternativi dell'utente. |
| StrongAuthenticationMethod |Un elenco di metodi di verifica configurato dall'utente hello multi-Factor Authentication, ad esempio telefonata, SMS o verifica del codice da un'app per dispositivi mobili. |
| StrongAuthenticationRequirement |Se l'autenticazione a più fattori è imposta, abilitata o disabilitata per questo utente. |
| StrongAuthenticationUserDetails |dell'utente Hello telefonica posta elettronica e numero di telefono alternativo, numero indirizzo utilizzato per l'autenticazione a più fattori e verifica la reimpostazione della password. |
| StrongAuthenticationPhoneAppDetail |Dettagli forof phone App registrato tooperform 2FA accesso |
| TelephoneNumber |numero di telefono dell'utente Hello. |
| AlternativeSecurityId |Un ID di sicurezza alternativo per l'oggetto hello. |
| CreationType |Metodo di creazione dell'utente hello (o tramite invito virale). |
| InviteTicket |Elenco di ticket di invito per l'utente hello. |
| InviteReplyUrl |Elenco di URL tooreply all'accettazione dell'invito. |
| InviteResources |Elenco di risorse toowhich hello gli è stato inviato. |
| LastDirSyncTime |Ora dell'ultima hello oggetto è stato aggiornato a causa di sincronizzazione dal hello autorevole (cliente, in locale) directory. |
| MSExchRemoteRecipientType |Esegue il mapping di tipi di destinatari tooMSO. Fare riferimento troppo https://msdn.microsoft.com/library/microsoft.office.interop.outlook.recipient.type.aspx [tipi destinatario MSO] per tipi di destinatari |
| PreferredDataLocation |Hello percorso preferito per l'utente hello, del gruppo, del contatto, della cartella pubblica o i dati del dispositivo. |
| ProxyAddresses |indirizzo Hello mediante il quale un oggetto destinatario di Exchange Server è riconosciuto in un sistema di posta elettronica esterna. |
| StsRefreshTokensValidFrom |Fornisce informazioni sulla revoca dei token di aggiornamento. Eventuali token di aggiornamento del servizio token di sicurezza emessi prima di questa data vengono considerati scaduti. |
| UserPrincipalName |Hello UPN è un nome di accesso Internet per un utente. |
| UserState |Stato dell'utente PendingApproval/PendingAcceptance/Accepted/PendingVerification. |
| UserStateChangedOn |TimeStamp dell'ultima modifica tooUserState. Utilizzare i flussi di lavoro di tootrigger del ciclo di vita. |
| UserType |Tipo di utente. Membro (0), guest (1), virale (2). |

## <a name="update-group-attributes"></a>Attributi di "Aggiornamento gruppo"
| Attributo | Descrizione |
| --- | --- |
| Classificazione |classificazione Hello per un gruppo unificato (impatto ad alto impatto aziendale, e così via). |
| Descrizione |Leggibile frasi descrittive sull'oggetto hello. |
| DisplayName |nome visualizzato Hello per un oggetto |
| DirSyncEnabled |Indica se la sincronizzazione viene eseguita da una directory autorevole (cliente, locale). |
| GroupLicenseAssignment |Assegnazione di licenza di un gruppo. |
| GroupType |Tipo di gruppo, unificato (0). |
| IsMembershipRuleLocked |Indica che la proprietà MembershipRule hello è impostato dal servizio di gestione di gruppi self-service hello e non può essere modificato dagli utenti. Applicabile toogroups solo in GroupType include GroupType.DynamicMembership |
| IsPublic |Flag tooindicate se il gruppo di hello è pubblica/privata. |
| LastDirSyncTime |Ora dell'ultima hello oggetto è stato aggiornato in seguito la sincronizzazione da hello autorevole (in locale, cliente) directory. |
| Mail |Indirizzo di posta elettronica primario. |
| MailEnabled |Indica se il gruppo ha funzionalità di posta elettronica. |
| MailNickname |Moniker per un oggetto della Rubrica, in genere parte hello del relativo nome di posta elettronica che precede hello "@" simbolo. |
| MembershipRule |Stringa che esprime criteri hello utilizzati dal servizio gestione di hello gruppo self-service toodetermine quali membri devono appartenere toothis gruppo. Vedere anche IsMembershipRuleLocked. Applicabile solo toogroups in GroupType include GroupType.DynamicMembership. |
| MembershipRuleProcessingState |Un valore di enumerazione definito dal servizio di gestione di gruppi self-service hello definizione hello dello stato di elaborazione per questo gruppo di appartenenza. Applicabile solo toogroups in GroupType include GroupType.DynamicMembership. |
| ProxyAddresses |indirizzo Hello mediante il quale un oggetto destinatario di Exchange Server è riconosciuto in un sistema di posta elettronica esterna. |
| RenewedDateTime |Record del timestamp che indica la data più recente in cui il gruppo è stato rinnovato. |
| SecurityEnabled |Indica se l'appartenenza al gruppo hello può influenzare le decisioni di autorizzazione. |
| WellKnownObject |Applica un'etichetta a un oggetto directory, designandolo come parte di un set predefinito. |

## <a name="update-device-attributes"></a>Attributi di "Aggiornamento dispositivo"
| Attributo | Descrizione |
| --- | --- |
| AccountEnabled |Indica se un'entità di sicurezza può eseguire l'autenticazione. |
| CloudAccountEnabled |Indica se un'entità di sicurezza può eseguire l'autenticazione. Scritti da InTune quando il dispositivo hello è gestito in locale. |
| CloudDeviceOSType |Tipo di dispositivo hello in base a hello del sistema operativo, ad esempio Windows RT, iOS. Se è impostato da un servizio cloud (ad esempio Intune), questo attributo diventa autorevole nella directory hello per DeviceOSType. |
| CloudDeviceOSVersion |Versione di hello del sistema operativo. Se è impostato da un servizio cloud (ad esempio Intune), questo attributo diventa autorevole nella directory hello per DeviceOSVersion. |
| CloudDisplayName |Valore dell'attributo LDAP di hello displayName. Questo attributo se è impostato da un servizio cloud (ad esempio Intune), diventa autorevole nella directory hello displayName. |
| CloudCreated |Indica se l'oggetto hello è stata creata dai servizi cloud. |
| CompliantUntil |Scadenza della conformità del dispositivo. |
| DeviceMetadata |Metadati personalizzati per il dispositivo hello |
| DeviceObjectVersion |Questo attributo è una versione dello schema di hello tooidentify utilizzati del dispositivo hello. |
| DeviceOSType |Tipo di dispositivo hello in base a hello del sistema operativo, ad esempio Windows RT, iOS. Scritto da hello toobe previsti e servizio di registrazione aggiornata da hello servizio di gestione MDM o STS chiaro servizio di gestione. |
| DeviceOSVersion |Versione di hello del sistema operativo. Scritto da hello toobe previsti e servizio di registrazione aggiornata da hello servizio di gestione MDM o STS chiaro servizio di gestione. |
| DevicePhysicalIds |Attributo multivalore deve toostore identificatori della periferica fisica hello. Può includere l'ID BIOS, l'identificazione personale di TPM, ID specifici dell'hardware e così via. |
| DirSyncEnabled |Indica se la sincronizzazione viene eseguita da una directory autorevole (cliente, locale). |
| DisplayName |nome visualizzato Hello per un oggetto |
| IsCompliant |Questo attributo è usato toomanage hello dispositivo mobile lo stato di gestione dispositivo hello. |
| IsManaged |Questo attributo viene utilizzato il dispositivo di hello tooindicate è gestito da un cloud MDM. |
| LastDirSyncTime |Ora dell'ultima hello oggetto è stato aggiornato a causa di sincronizzazione dal hello autorevole (in locale, cliente) directory. |

## <a name="update-device-configuration-attributes"></a>Attributi di "Aggiornamento configurazione dispositivi"
| Attributo | Descrizione |
| --- | --- |
| MaximumRegistrationInactivityPeriod |numero massimo di Hello di giorni di un dispositivo può rimanere inattivo prima di essere considerato per la rimozione. |
| RegistrationQuota |Numero di hello toolimit di registrazioni dei dispositivi consentiti per un singolo utente utilizzati i criteri. |

## <a name="update-service-principal-configuration-attributes"></a>Attributi di "Aggiornamento configurazione delle entità servizio"
| Attributo | Descrizione |
| --- | --- |
| AccountEnabled |Indica se un'entità di sicurezza può eseguire l'autenticazione. |
| AppPrincipalId |Identità esterna definita dall'applicazione per un'entità di sicurezza. |
| DisplayName |nome visualizzato Hello per un oggetto |
| ServicePrincipalName |Un nome dell'entità servizio, che contiene "nome/authority" in nome specifica un valore di classe dell'applicazione e autorità contiene almeno il nome host [: porta] o "nome" che specifica un identificatore dell'entità servizio hello. |

## <a name="update-app-attributes"></a>Attributi di "Aggiornamento app"
| Attributo | Descrizione |
| --- | --- |
| AppAddress |set di Hello di indirizzo (URL di reindirizzamento) dell'entità servizio tooa assegnato. |
| AppId |ID applicazione di hello App |
| AppIdentifierUri |URI dell'applicazione, che identifica un'applicazione hello.  È in genere hello URL di accesso dell'applicazione. |
| AppLogoUrl |Hello url immagine del logo dell'applicazione hello archiviata in una rete CDN. |
| AvailableToOtherTenants |Un'applicazione hello true è l'applicazione multi-tenant (ad esempio può essere utilizzato da altri tenant). |
| DisplayName |nome visualizzato Hello per nome di un'applicazione |
| Entitlement |Elenco di diritti dell'applicazione. |
| ExternalUserAccountDelegationsAllowed |Flag che indica se l'applicazione della risorsa è attendibile e può creare voci di delega per account utente esterni. |
| GroupMembershipClaims |l'appartenenza al gruppo di Hello attestazioni criteri. |
| PublicClient |True se il client di hello non è possibile tenere segreto (ad esempio i client non riservato in OAuth 2.0) |
| RecordConsentConditions |Tipi di condizioni di consenso, come definito da hello termini del contratto: None (0), SilentConsentForPartnerManagedApp(1). Questo valore sarà esposta in schema di API Graph hello e può essere impostato/modificato da amministratori tenant. |
| RequiredResourceAccess |Contenuto XML di un valore di proprietà RequiredResourceAccess hello. |
| WebApp |Se True, indica che questa applicazione è un'app Web. |
| WwwHomepage |Hello primario della pagina Web. |

## <a name="update-role-attributes"></a>Attributi di "Aggiornamento ruolo"
| Attributo | Descrizione |
| --- | --- |
| AppAddress |set di Hello di indirizzo (URL di reindirizzamento) dell'entità servizio tooa assegnato. |
| BelongsToFirstLoginObjectSet |Se true, indica che l'oggetto appartiene toohello set di account di accesso obbligatorio tooenable gli oggetti di salve prima di un nuovo tenant. |
| Builtin |Indica se la durata hello di un oggetto è di proprietà di sistema hello. |
| Descrizione |Leggibile frasi descrittive sull'oggetto hello. |
| DisplayName |nome visualizzato Hello per un oggetto |
| MailNickname |Moniker per un oggetto della Rubrica, in genere parte hello del relativo nome di posta elettronica che precede hello "@" simbolo. |
| RoleDisabled |Indica se il ruolo di hello deve essere ignorato ai fini di controlli di accesso. |
| RoleTemplateId |Identità del modello di ruolo hello. |
| ServiceInfo |Informazioni che possono essere utilizzate da MOAC e/o altre istanze del servizio di provisioning specifico del servizio (di hello uguali o diverso tipi di servizi). |
| TaskSetScopeReference |Identifica un valore TaskSet e un set di ambiti associati a un valore Role o RoleTemplate. |
| ValidationError |Informazioni pubblicate da un servizio federativo che descrive un errore non temporaneo, specifico del servizio relativa alle proprietà hello o collegamento da tooresolve di azione amministratore un oggetto. |
| WellKnownObject |Applica un'etichetta a un oggetto directory, designandolo come parte di un set predefinito. |

## <a name="update-role-definition-attributes"></a>Attributi di "Aggiornamento definizione ruolo"
| Attributo | Descrizione |
| --- | --- |
| AssignableScopes |Raccolta di ambiti di autorizzazione che è possibile fare riferimento quando si assegna questa entità di sicurezza di RoleDefinition tooa. |
| DisplayName |nome visualizzato Hello per un oggetto |
| GrantedPermissions |Autorizzazioni concesse da questo valore RoleDefinition. |

## <a name="update-administrative-unit-attributes"></a>Attributi di "Aggiornamento unità amministrativa"
| Attributo | Descrizione |
| --- | --- |
| Descrizione |Questa proprietà viene aggiornata quando si modifica la descrizione hello di un'unità amministrativa. |
| DisplayName |Questa proprietà viene aggiornata quando si modifica il nome di hello di un'unità amministrativa. |

## <a name="update-company-attributes"></a>Attributi di "Aggiornamento azienda"
| Attributo | Descrizione |
| --- | --- |
| AllowedDataLocation |Posizione in cui hello utenti della società sono consentiti toobe il provisioning. |
| AuthorizedServiceInstance |Nomi delle istanze di servizio toowhich un piano possono essere distribuiti. |
| DirSyncEnabled |Indica se la sincronizzazione viene eseguita da una directory autorevole (cliente, locale). |
| DirSyncStatus |Indica se la sincronizzazione degli oggetti della Rubrica indirizzi in questo contesto di tenant di un autorevole (cliente, in locale) directory. un'espansione di hello DirSyncEnabled proprietà sugli oggetti della società. |
| DirSyncFeatures |Traccia di tookeep flag bit di set di funzionalità di dirsync abilitati e disabilitati per tenant hello. |
| DirectoryFeatures |Funzionalità della directory abilitate/disabilitate. |
| DirSyncConfiguration |Contiene tutti DirSync configurazione toohello specifico tenant corrente. |
| DisplayName |nome visualizzato Hello per un oggetto |
| IsMnc |Una società di hello flag booleano set troppo "true" se è abilitata per la funzionalità di società multinazionale hello. |
| ObjectSettings |Raccolta di ambito toohello applicabili le impostazioni dell'oggetto hello. |
| PartnerCommerceUrl |URL toohello commerce siti Partner. |
| PartnerHelpUrl |Sito della Guida del Partner toohello URL. |
| PartnerSupportEmail |Posta elettronica di supporto del Partner toohello URL. |
| PartnerSupportTelephone |Telefono del supporto del Partner toohello URL. |
| PartnerSupportUrl |Sito del supporto tecnico del Partner toohello URL. |
| StrongAuthenticationDetails |I dettagli correlati tooStrongAuthentication. |
| StrongAuthenticationPolicy |Criteri di autenticazione per l'azienda hello. |
| TechnicalNotificationMail |Posta elettronica indirizzo toonotify problemi tecnici relativi tooa aziendale. |
| TelephoneNumber |Numeri di telefono che rispettano hello e. 123 raccomandazione ITU. |
| TenantType |tipo di Hello di un tenant. Se questo valore viene omesso, il tenant di hello è una società. In caso contrario, i valori possibili sono MicrosoftSupport (0), SyndicatePartner (1), BreadthPartner (2) BreadthPartnerDelegatedAdmin (3) ResellerPartnerDelegatedAdmin (4) ValueAddedResellerPartnerDelegatedAdmin (5). |
| VerifiedDomain |Un set di nomi di dominio DNS associato tooa aziendale. |

## <a name="update-domain-attributes"></a>Attributi di "Aggiornamento dominio"
| Attributo | Descrizione |
| --- | --- |
| Capabilities |Flag di bit che descrive le funzionalità di hello del dominio hello, se presente. |
| Default |Indica se il dominio hello è valore predefinito di hello. ad esempio, hello UserPrincipalName suffisso predefinito quando un amministratore crea un nuovo utente in MOAC. |
| Initial |Indica se hello dominio è hello iniziale per la società hello, allocato dal OCP. dominio iniziale Hello è un sottodominio univoco di un dominio di Microsoft Online. e.g.contoso3.microsoftonline.com. |
| LiveType |Tipo di hello Windows Live spazio dei nomi corrispondente, se presente. |
| Nome |Identificatore hello endpoint. |
| PasswordNotificationWindowDays |numero di Hello di giorni prima della scadenza di una password utente hello riceve una notifica. |
| PasswordValidityPeriodDays |Hello numero di giorni che è utile per una password prima che debba essere cambiata. |

I record di controllo rappresentano un controllo obbligatorio per molte normative per la conformità. Per i clienti che usano hello Azure Active Directory Audit Report toomeet le normative di conformità, è consigliabile cliente hello inviare una copia di questo argomento della Guida con copia hello del cliente hello esportata toohelp spiegare report hello report di controllo informazioni dettagliate. Se il revisore hello desidera normative di conformità hello toounderstand conforme attualmente Azure, indirizzare hello revisore toohello [pagina conformità](https://azure.microsoft.com/support/trust-center/compliance/) di Microsoft Azure Trust Center hello.


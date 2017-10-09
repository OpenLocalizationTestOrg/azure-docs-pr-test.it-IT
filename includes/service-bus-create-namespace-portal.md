utilizzo di Service Bus toobegin le code in Azure, è innanzitutto necessario creare uno spazio dei nomi con un nome univoco in Azure. Uno spazio dei nomi fornisce un contenitore di ambito per fare riferimento alle risorse del bus di servizio all'interno dell'applicazione.

toocreate uno spazio dei nomi:

1. Accesso toohello [portale di Azure][Azure portal].
2. Nel riquadro di spostamento a sinistra di hello del portale di hello, fare clic su **New**, quindi fare clic su **Enterprise Integration**, quindi fare clic su **Bus di servizio**.
3. In hello **Crea spazio dei nomi** finestra di dialogo immettere un nome di spazio dei nomi. sistema di Hello controlla immediatamente toosee se nome hello è disponibile.
4. Dopo il nome di spazio dei nomi che hello è disponibile, scegliere hello tariffario (Basic, Standard o Premium).
5. In hello **sottoscrizione** campo, scegliere una sottoscrizione di Azure in cui lo spazio dei nomi di toocreate hello.
6. In hello **gruppo di risorse** selezionare un gruppo di risorse esistente in cui hello dello spazio dei nomi in tempo reale oppure crearne uno nuovo.      
7. In **percorso**, scegliere hello paese in cui lo spazio dei nomi deve essere ospitato.
   
    ![Crea spazio dei nomi][create-namespace]
8. Fare clic su **Crea**. sistema Hello ora crea uno spazio dei nomi e viene abilitato. Potrebbe essere toowait alcuni minuti per le risorse di hello sistema esegue il provisioning per l'account.

### <a name="obtain-hello-management-credentials"></a>Ottenere le credenziali di gestione di hello

1. Nell'elenco di hello degli spazi dei nomi, fare clic su hello appena creato il nome dello spazio dei nomi.
2. Nel Pannello di hello dello spazio dei nomi, fare clic su **criteri di accesso condiviso**.
3. In hello **criteri di accesso condiviso** pannello, fare clic su **RootManageSharedAccessKey**.
   
    ![connection-info][connection-info]
4. In hello **criteri: RootManageSharedAccessKey** pannello, fare clic su pulsante Copia hello Avanti troppo**chiave – primario di stringa di connessione**, negli Appunti toocopy hello connessione stringa tooyour per un uso successivo. Incollare questo valore nel Blocco note o in un'altra posizione temporanea.
   
    ![connection-string][connection-string]

5. Passaggio precedente hello ripetizione, copiare e incollare il valore di hello di **chiave primaria** tooa percorso temporaneo per un uso successivo.

<!--Image references-->

[create-namespace]: ./media/service-bus-create-namespace-portal/create-namespace.png
[connection-info]: ./media/service-bus-create-namespace-portal/connection-info.png
[connection-string]: ./media/service-bus-create-namespace-portal/connection-string.png
[Azure portal]: https://portal.azure.com

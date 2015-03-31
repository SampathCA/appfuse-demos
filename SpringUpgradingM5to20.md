
```
Index: src/test/resources/web-tests.xml
===================================================================
--- src/test/resources/web-tests.xml	(revision 85)
+++ src/test/resources/web-tests.xml	(working copy)
@@ -85,7 +85,7 @@
             &config;
             <steps>
                 &login;
-                <invoke description="click View Users link" url="/users.html"/>
+                <invoke description="click View Users link" url="/admin/users.html"/>
                 <verifytitle description="we should see the user list title" 
                     text=".*${userList.title}.*" regex="true"/>
             </steps>
@@ -136,7 +136,7 @@
 
                 <verifytitle description="view user list screen" text=".*${userList.title}.*" regex="true"/>
                 <verifytext description="verify success message" regex="true"
-                    text='&lt;div class="message.*&gt;.*&lt;strong&gt;Test Name&lt;/strong&gt;.*&lt;/div&gt;'/>
+                    text='&lt;div class="message.*&gt;.*Test Name.*&lt;/div&gt;'/>
                     
                 <!-- Delete user -->
                 <clickLink description="Click edit user link" label="newuser"/>
@@ -144,7 +144,7 @@
                 <clickbutton label="${button.delete}" description="Click button 'Delete'"/>
                 <verifyNoDialogResponses/>
                 <verifytext description="verify success message" regex="true"
-                    text='&lt;div class="message.*&gt;.*&lt;strong&gt;Test Name&lt;/strong&gt;.*&lt;/div&gt;'/>
+                    text='&lt;div class="message.*&gt;.*Test Name.*&lt;/div&gt;'/>
                 <verifytitle description="display user list" text=".*${userList.title}.*" regex="true"/>
             </steps>
         </webtest>
@@ -184,7 +184,7 @@
             &config;
             <steps>
                 &login;
-                <invoke description="get activeUsers URL" url="/activeUsers.html"/>
+                <invoke description="get activeUsers URL" url="/admin/activeUsers.html"/>
                 <verifytitle description="we should see the activeUsers title" 
                     text=".*${activeUsers.title}.*" regex="true"/>
             </steps>
@@ -197,7 +197,7 @@
             &config;
             <steps>
                 &login;
-                <invoke description="get flushCache URL" url="/flushCache.html"/>
+                <invoke description="get flushCache URL" url="/admin/flushCache.html"/>
                 <verifytitle description="we should see the flush cache title" 
                     text=".*${flushCache.title}.*" regex="true"/>
             </steps>
Index: src/main/resources/applicationContext-resources.xml
===================================================================
--- src/main/resources/applicationContext-resources.xml	(revision 85)
+++ src/main/resources/applicationContext-resources.xml	(working copy)
@@ -23,10 +23,8 @@
         <property name="username" value="${jdbc.username}"/>
         <property name="password" value="${jdbc.password}"/>
         <property name="maxActive" value="100"/>
-        <property name="maxIdle" value="30"/>
         <property name="maxWait" value="1000"/>
+        <property name="poolPreparedStatements" value="true"/>
         <property name="defaultAutoCommit" value="true"/>
-        <property name="removeAbandoned" value="true"/>
-        <property name="removeAbandonedTimeout" value="60"/>
     </bean>
 </beans>
Index: src/main/resources/ApplicationResources_pt_BR.properties
===================================================================
--- src/main/resources/ApplicationResources_pt_BR.properties	(revision 85)
+++ src/main/resources/ApplicationResources_pt_BR.properties	(working copy)
@@ -22,7 +22,7 @@
 # -- other errors --
 errors.cancel=OperaÁ„o cancelada.
 errors.detail={0}
-errors.general=<strong>O processo n„o completou. Os detalhes devem seguir.</strong>
+errors.general=O processo n„o completou. Os detalhes devem seguir.
 errors.token=RequisiÁ„o n„o poderia ser completada. A operaÁ„o n„o est· em ordem.
 errors.none=Nenhuma mensagem de erro foi encontrada, verifica seus registros do servidor.
 errors.password.mismatch=Nome do usu·rio ou senha inv·lido, por favor tente novamente.
@@ -31,11 +31,11 @@
 errors.existing.user=Este nome de usu·rio ({0}) ou endereÁo de e-mail ({1}) j· existe.  Por favor tente um nome de usu·rio diferente.
 
 # -- success messages --
-user.added=InformaÁ„o de Usu·rio para <strong>{0}</strong> foi adicionada com sucesso.
-user.deleted=Perfil de Usu·rio para <strong>{0}</strong> foi deletada com sucesso. 
+user.added=InformaÁ„o de Usu·rio para {0} foi adicionada com sucesso.
+user.deleted=Perfil de Usu·rio para {0} foi deletada com sucesso.
 user.registered=VocÍ registou com sucesso para o acesso a esta aplicaÁ„o.
 user.saved=Seu perfil foi atualizado com sucesso.
-user.updated.byAdmin=InformaÁ„o de Usu·rio para <strong>{0}</strong> foi atualizada com sucesso.
+user.updated.byAdmin=InformaÁ„o de Usu·rio para {0} foi atualizada com sucesso.
 newuser.email.message={0} criou uma conta AppFuse para vocÍ.  Sua informaÁ„o nome de usu·rio e senha est· logo abaixo.
 reload.succeeded=AtualizaÁ„o das opÁıes realizada com sucesso.
 
@@ -53,8 +53,8 @@
 login.rememberMe=Lembre-me
 login.signup=N„o È um membro? <a href="{0}">Registre-se</a> para uma conta.
 login.passwordHint=Esqueceu sua senha? Tenha <a href="?" onmouseover="window.status='Tenha sua dica de senha enviada a vocÍ.'; return true" onmouseout="window.status=''; return true" title="Tenha sua dica de senha enviada a vocÍ." onclick="passwordHint(); return false">sua dica de senha enviada a vocÍ</a>.
-login.passwordHint.sent=A dica de senha para <strong>{0}</strong> foi enviada para <strong>{1}</strong>.
-login.passwordHint.error=O nome de usu·rio <strong>{0}</strong> n„o foi encontrado no banco de dados.
+login.passwordHint.sent=A dica de senha para {0} foi enviada para {1}.
+login.passwordHint.error=O nome de usu·rio {0} n„o foi encontrado no banco de dados.
 
 # -- mainMenu --
 mainMenu.title=Menu Principal
Index: src/main/resources/ApplicationResources_fr.properties
===================================================================
--- src/main/resources/ApplicationResources_fr.properties	(revision 85)
+++ src/main/resources/ApplicationResources_fr.properties	(working copy)
@@ -1,41 +1,41 @@
-user.status=ConnectÈ(e) en tant que : 
+user.status=ConnectÈ(e) en tant que :
 user.logout=DÈconnexion
 
 # -- validator errors --
-errors.invalid={0} n'est pas valide.
+errors.invalid={0} n''est pas valide.
 errors.maxlength={0} ne peut pas avoir plus de {1} caractËres.
 errors.minlength={0} ne peut pas avoir moins de {1} caractËres.
-errors.range={0} n'est pas dans la plage de {1} ‡ {2}.
+errors.range={0} n''est pas dans la plage de {1} ‡ {2}.
 errors.required={0} est un champ requis.
 errors.byte={0} doit Ítre un octet.
-errors.date={0} n'est pas une date.
+errors.date={0} n''est pas une date.
 errors.double={0} doit Ítre un nombre au format "double".
 errors.float={0} doit Ítre un nombre au format "float".
 errors.integer={0} doit Ítre un nombre.
 errors.long={0} doit Ítre un entier au format "long".
 errors.short={0} doit Ítre un entier au format "short".
-errors.creditcard={0} n'est pas un numÈro de carte de crÈdit valide.
-errors.email={0} n'est pas une adresse de email valide.
-errors.phone={0} n'est pas un numÈro de tÈlÈphone valide.
-errors.zip={0} n'est pas un code postal (USA ZIP) valide.
+errors.creditcard={0} n''est pas un numÈro de carte de crÈdit valide.
+errors.email={0} n''est pas une adresse de email valide.
+errors.phone={0} n''est pas un numÈro de tÈlÈphone valide.
+errors.zip={0} n''est pas un code postal (USA ZIP) valide.
 
 # -- other errors --
 errors.cancel=OpÈration annulÈe.
 errors.detail={0}
-errors.general=<strong>Le processus ne s'est pas achevÈ. Les dÈtails devraient suivre.</strong>
-errors.token=La requÍte n'est peut-Ítre pas terminÈe. L'opÈration n'est dans en sÈquence.
-errors.none=Aucun message d'erreur n'a ÈtÈ trouvÈ. VÈrifier les logs de votre serveur.
+errors.general=Le processus ne s'est pas achevÈ. Les dÈtails devraient suivre.
+errors.token=La requÍte n''est peut-Ítre pas terminÈe. L'opÈration n''est dans en sÈquence.
+errors.none=Aucun message d'erreur n''a ÈtÈ trouvÈ. VÈrifier les logs de votre serveur.
 errors.password.mismatch=Identifiant ou mot de passe invalide(s). Veuillez rÈessayer.
 errors.conversion=Une erreur est apparue pendant la conversion des valeurs Web en valeurs typÈes.
 errors.twofields=Le champ {0} doit avoir la mÍme valeur que le champ {1}.
-errors.existing.user=L'identifiant ({0}) ou l'adresse de email ({1}) existe dÈj‡. Veuillez essayer un autre identifiant.
+errors.existing.user=L''identifiant ({0}) ou l''adresse de email ({1}) existe dÈj‡. Veuillez essayer un autre identifiant.
 
 # -- success messages --
-user.added=Les informations utilisateur pour <strong>{0}</strong> ont ÈtÈ ajoutÈes avec succËs.
-user.deleted=Le profil utilisateur pour <strong>{0}</strong> a ÈtÈ supprimÈ avec succËs. 
-user.registered=Vous vous Ítes inscrit(e) avec succËs pour accÈder ‡ cette application. 
+user.added=Les informations utilisateur pour {0} ont ÈtÈ ajoutÈes avec succËs.
+user.deleted=Le profil utilisateur pour {0} a ÈtÈ supprimÈ avec succËs.
+user.registered=Vous vous Ítes inscrit(e) avec succËs pour accÈder ‡ cette application.
 user.saved=Votre profil a ÈtÈ mis ‡ jour avec succËs.
-user.updated.byAdmin=Les informations utilisateur pour <strong>{0}</strong> ont ÈtÈ mises ‡ jour avec succËs.
+user.updated.byAdmin=Les informations utilisateur pour {0} ont ÈtÈ mises ‡ jour avec succËs.
 newuser.email.message={0} a crÈÈ un compte AppFuse pour vous. Les informations concernant vos indentifiant et mot de passe sont donnÈes ci-dessous.
 reload.succeeded=Les options de rechargement sont completees avec succes.
 
@@ -43,7 +43,7 @@
 errorPage.title=Une erreur est apparue
 errorPage.heading=Oups !
 404.title=Page non trouvÈe
-404.message=La page que vous avez demandÈe n'a pas ÈtÈ trouvÈe. Vous pouvez essayer de retourner ‡ <a href="{0}">Main Menu</a>. En attendant, pourquoi pas une belle image pour vous remonter le moral ?
+404.message=La page que vous avez demandÈe n''a pas ÈtÈ trouvÈe. Vous pouvez essayer de retourner ‡ <a href="{0}">Main Menu</a>. En attendant, pourquoi pas une belle image pour vous remonter le moral ?
 403.title=AccËs refusÈ
 403.message=Votre rÙle actuel ne vous permet pas de voir cette page. Veuillez contacter votre administrateur systËme si vous pensez en avoir les droits d'accËs. Entre temps, pourquoi pas une belle image pour vous remonter le moral ?
 
@@ -53,8 +53,8 @@
 login.rememberMe=Conserver ce mot de passe
 login.signup=Pas encore membre ? <a href="{0}">Demander</a> un compte.
 login.passwordHint=Passeport oubliÈ ? Obtenez votre <a href="?" onmouseover="window.status='Obtenez votre mot de passe provisoire chez vous.'; return true" onmouseout="window.status=''; return true" title="Obtenez votre mot de passe directement chez vous." onclick="passwordHint(); return false">mot de passe provisoire, envoyÈ par email</a>.
-login.passwordHint.sent=Le mot de passe provisoire pour <strong>{0}</strong> a ÈtÈ envoyÈ ‡ <strong>{1}</strong>.
-login.passwordHint.error=L'utilisateur <strong>{0}</strong> n'a pas ÈtÈ trouvÈ dans l'annuaire.
+login.passwordHint.sent=Le mot de passe provisoire pour {0} a ÈtÈ envoyÈ ‡ {1}.
+login.passwordHint.error=L'utilisateur {0} n''a pas ÈtÈ trouvÈ dans l''annuaire.
 
 # -- mainMenu --
 mainMenu.title=Menu principal
@@ -83,7 +83,7 @@
 button.delete=Supprimer
 button.done=Fait
 button.edit=Editer
-button.register=S'inscrire
+button.register=S''inscrire
 button.save=Sauvegarder
 button.search=Rechercher
 button.upload=Charger
@@ -101,18 +101,15 @@
 date.format=dd/MM/yyyy
 colon=&nbsp;:
 
-# -- role form -- TODO: change it? internal only?
-roleForm.name=Name
-
 # -- user profile page --
 userProfile.title=ParamËtres utilisateur
 userProfile.heading=Profil utilisateur
-userProfile.message=Veuiller mettre ‡ jour vos informations ‡ l'aide du formulaire ci-dessous.
-userProfile.admin.message=Vous pouvez mettre ‡ jour ces informations utilisateur ‡ l'aide du formulaire ci-dessous.
-userProfile.showMore=Pour plus d'info
+userProfile.message=Veuiller mettre ‡ jour vos informations ‡ l''aide du formulaire ci-dessous.
+userProfile.admin.message=Vous pouvez mettre ‡ jour ces informations utilisateur ‡ l''aide du formulaire ci-dessous.
+userProfile.showMore=Pour plus d''info
 userProfile.accountSettings=Edition du profil
 userProfile.assignRoles=Assigner des rÙles
-userProfile.cookieLogin=Vous ne pouvez changer de mot de passe en vous connectant ‡ l'aide du dispositif <strong>Conserver ce mot de passe</strong>. Veuillez vous dÈconnecter et vous reconnecter pour changer de mot de passe.
+userProfile.cookieLogin=Vous ne pouvez changer de mot de passe en vous connectant ‡ l''aide du dispositif <strong>Conserver ce mot de passe</strong>. Veuillez vous dÈconnecter et vous reconnecter pour changer de mot de passe.
 
 # -- user form --
 user.address.address=Adresse
@@ -148,7 +145,7 @@
 signup.heading=Enregistrement d'un nouvel utilisateur
 signup.message=Veuillez complÈter le formulaire ci-aprËs avec vos informations d'utilisateur.
 signup.email.subject=Information de compte AppFuse
-signup.email.message=Vous vous Ítes correctement inscrit pour avoir accËs ‡ AppFuse. Vos informations d'identifiant et de mot de passe sont ci-dessous.
+signup.email.message=Vous vous Ítes correctement inscrit pour avoir accËs ‡ AppFuse. Vos informations d''identifiant et de mot de passe sont ci-dessous.
 
 # -- upload page messages --
 maxLengthExceeded=Le fichier que vous essayez de charger est trop gros. Le maximum autorisÈ est de 2 Mo.
@@ -158,7 +155,7 @@
 uploadForm.name=Friendly Name
 uploadForm.file=Fichier ‡ charger
 
-# -- display page messages -- 
+# -- display page messages --
 display.title=Fichier chargÈ avec succËs !
 display.heading=Information sur le fichier
 
@@ -178,9 +175,9 @@
 # -- active users page --
 activeUsers.title=Utilisateurs actifs
 activeUsers.heading=Utilisateurs connectÈs
-activeUsers.message=Ci-dessous une liste des utilisateurs qui sont connectÈs et dont la session n'a pas expirÈ.
+activeUsers.message=Ci-dessous une liste des utilisateurs qui sont connectÈs et dont la session n''a pas expirÈ.
 activeUsers.fullName=Nom complet
 
 # JSF-only messages, remove if not using JSF
 javax.faces.component.UIInput.REQUIRED={0} est un champ requis.
-activeUsers.summary={0} Utilisateur(s) trouvé(s), {1} utilisateur(s) affiché(s), de {2} à {3}. Page {4} / {5}
\ No newline at end of file
+activeUsers.summary={0} Utilisateur(s) trouvÈ(s), {1} utilisateur(s) affichÈ(s), de {2} ‡ {3}. Page {4} / {5}
\ No newline at end of file
Index: src/main/resources/ApplicationResources_es.properties
===================================================================
--- src/main/resources/ApplicationResources_es.properties	(revision 85)
+++ src/main/resources/ApplicationResources_es.properties	(working copy)
@@ -22,7 +22,7 @@
 # -- other errors --
 errors.cancel=Operaci\u00F3n cancelada.
 errors.detail={0}
-errors.general=<strong>El proceso no se ha completado. Eval\u00FAe los siguiente detalles\:</strong>
+errors.general=El proceso no se ha completado. Eval\u00FAe los siguiente detalles.
 errors.token=La petici\u00F3n no pudo completarse. La operaci\u00F3n no est\u00E1 en proceso.
 errors.none=No hay mensajes de error, revise los logs del servidor.
 errors.password.mismatch=Nombre de usuario o contrase\u00F1a no v\u00E1lido, por favor, int\u00E9ntelo de nuevo.
@@ -31,11 +31,11 @@
 errors.existing.user=Este usuario ({0}) o direcci\u00F3n de e-mail ({1}) ya existe.  Por favor int\u00E9ntelo con un nombre de usuario diferente.
 
 # -- success messages --
-user.added=La informaci\u00F3n del usuario <strong>{0}</strong> has sido insertada con \u00E9xito.
-user.deleted=El perfil del usuario <strong>{0}</strong> ha sido borrado con \u00E9xito.
+user.added=La informaci\u00F3n del usuario {0} has sido insertada con \u00E9xito.
+user.deleted=El perfil del usuario {0} ha sido borrado con \u00E9xito.
 user.registered=Ha sido registrado con \u00E9xito para acceder a esta aplicaci\u00F3n.
 user.saved=Su perfil ha sido actualizado con \u00E9xito.
-user.updated.byAdmin=La informaci\u00F3n del usuario <strong>{0}</strong> ha sido actualizada con \u00E9xito.
+user.updated.byAdmin=La informaci\u00F3n del usuario {0} ha sido actualizada con \u00E9xito.
 newuser.email.message={0} ha creado una cuenta para usted. Su usuario y contrase\u00F1a son los siguientes.
 reload.succeeded=La recarga de opciones se ha completado con \u00E9xito.
 
@@ -53,8 +53,8 @@
 login.signup=\u00BFNo es miembro? <a href\="{0}">Crear</a> una cuenta.
 403.title=Acceso Denegado
 login.passwordHint=\u00BFOlvid\u00F3 su contrase\u00F1a?  Enviarme la <a href\="?" onmouseover\="window.status\='Enviarme la pista de la contrase\u00F1a.'; return true" onmouseout\="window.status\=''; return true" title\="Enviarme la pista de la contrase\u00F1a." onclick\="passwordHint(); return false">pista de la contrase\u00F1a por email</a>.
-login.passwordHint.sent=La pista de la contrase\u00F1a para <strong>{0}</strong> ha sido enviada a <strong>{1}</strong>.
-login.passwordHint.error=El usuario <strong>{0}</strong> no se encuentra en nuestra base de datos.
+login.passwordHint.sent=La pista de la contrase\u00F1a para {0} ha sido enviada a {1}.
+login.passwordHint.error=El usuario {0} no se encuentra en nuestra base de datos.
 
 # -- mainMenu --
 mainMenu.title=Men\u00FA Principal
Index: src/main/resources/ApplicationResources_nl.properties
===================================================================
--- src/main/resources/ApplicationResources_nl.properties	(revision 85)
+++ src/main/resources/ApplicationResources_nl.properties	(working copy)
@@ -22,7 +22,7 @@
 # -- other errors --
 errors.cancel=Proces gestopt.
 errors.detail={0}
-errors.general=<strong>Deze actie is niet volledig verwerkt. Details volgen.</strong>
+errors.general=Deze actie is niet volledig verwerkt. Details volgen.
 errors.token=Verzoek kon niet volledig verwerkt worden. Proces is niet synchroon.
 errors.none=Geen foutmelding gevonden, controleer je server-logs.
 errors.password.mismatch=Ongeldige gebruikersnaam en/of wachtwoord, probeer opnieuw.
@@ -31,11 +31,11 @@
 errors.existing.user=Deze gebruikersnaam ({0}) of dit e-mail adres ({1}) bestaat al. Probeer een andere gebruikersnaam.
 
 # -- success messages --
-user.added=Gebruikersgegevens van <strong>{0}</strong> zijn toegevoegd.
-user.deleted=Gebruikersprofiel van <strong>{0}</strong> is verwijderd. 
+user.added=Gebruikersgegevens van {0} zijn toegevoegd.
+user.deleted=Gebruikersprofiel van {0} is verwijderd.
 user.registered=Je bent geregistreerd als gebruiker voor deze applicatie en hebt nu toegang. 
 user.saved=Je profiel is bijgewerkt.
-user.updated.byAdmin=Gebruikersgegevens van <strong>{0}</strong> zijn bijgewerkt.
+user.updated.byAdmin=Gebruikersgegevens van {0} zijn bijgewerkt.
 newuser.email.message={0} heeft een AppFuse account voor je aangemaakt.  Je gebruikersnaam en wachtwoord staan hieronder.
 reload.succeeded=Vernieuwen van opties succesvol afgerond.
 
@@ -53,8 +53,8 @@
 login.rememberMe=Onthoud mijn gegevens
 login.signup=Nog geen lid? <a href="{0}">Registreer</a> je hier.
 login.passwordHint=Wachtwoord vergeten? Klik om je <a href="?" onmouseover="window.status='E-mail wachtwoord hint.'; return true" onmouseout="window.status=''; return true" title="E-mail wachtwoord hint." onclick="passwordHint(); return false">wachtwoord hint</a> te e-mailen.
-login.passwordHint.sent=De wachtwoord hint van <strong>{0}</strong> is verstuurd naar <strong>{1}</strong>.
-login.passwordHint.error=De gebruikersnaam <strong>{0}</strong> is niet gevonden in onze database.
+login.passwordHint.sent=De wachtwoord hint van {0} is verstuurd naar {1}.
+login.passwordHint.error=De gebruikersnaam {0} is niet gevonden in onze database.
 
 # -- mainMenu --
 mainMenu.title=Hoofdmenu
Index: src/main/resources/ApplicationResources_it.properties
===================================================================
--- src/main/resources/ApplicationResources_it.properties	(revision 85)
+++ src/main/resources/ApplicationResources_it.properties	(working copy)
@@ -22,7 +22,7 @@
 # -- other errors --
 errors.cancel=Operazione cancellata.
 errors.detail={0}
-errors.general=<strong>Il processo non \u00E8 stato completato. Seguono eventuali dettagli.</strong>
+errors.general=Il processo non \u00E8 stato completato. Seguono eventuali dettagli.
 errors.token=La richiesta non pu\u00F2 essere esaudita. Operazione fuori sequenza.
 errors.none=Errore generale, controllare i file di registro.
 errors.password.mismatch=Nome utente o password non validi, per favore riprovare.
@@ -31,11 +31,11 @@
 errors.existing.user=Questo nome utente ({0}) o questo indirizzo di e-mail ({1}) esistono gi\u00E0. Per favore riprovare con un nome utente diverso.
 
 # -- success messages --
-user.added=Dati dell'utente <strong>{0}</strong> aggiunti con successo.
-user.deleted=Cancellazione del profilo dell'utente <strong>{0}</strong> effettuata con successo.
+user.added=Dati dell'utente {0} aggiunti con successo.
+user.deleted=Cancellazione del profilo dell'utente {0} effettuata con successo.
 user.registered=La registrazione ha avuto successo.
 user.saved=Dati memorizzati con successo.
-user.updated.byAdmin=Dati dell'utente <strong>{0}</strong> aggiornati con successo.
+user.updated.byAdmin=Dati dell'utente {0} aggiornati con successo.
 newuser.email.message={0} ha creato un utente Appfuse per lei. Il suo nome utente e la sua password sono indicate appresso.
 reload.succeeded=Opzioni ricaricate con successo.
 
@@ -53,8 +53,8 @@
 login.rememberMe=Memorizza nome utente e password
 login.signup=Non \u00E8 ancora registrato? Pu\u00F2 <a href="{0}">creare un utente</a>.
 login.passwordHint=Dimenticata la password?  <a href="?" onmouseover="window.status='Manda un suggerimento per ricordarsi la password.'; return true" onmouseout="window.status=''; return true" title="Manda un suggerimento per ricordarsi la password." onclick="passwordHint(); return false">Manda per e-mail un suggerimento per ricordarsi la password</a>.
-login.passwordHint.sent=Il suggerimento password per <strong>{0}</strong> \u00E8 stato spedito a <strong>{1}</strong>.
-login.passwordHint.error=Il nome utente <strong>{0}</strong> non \u00E8 stato trovato nel nostro archivio.
+login.passwordHint.sent=Il suggerimento password per {0} \u00E8 stato spedito a {1}.
+login.passwordHint.error=Il nome utente {0} non \u00E8 stato trovato nel nostro archivio.
 
 # -- mainMenu --
 mainMenu.title=Men\u00F9 Principale
Index: src/main/resources/ApplicationResources_no.properties
===================================================================
--- src/main/resources/ApplicationResources_no.properties	(revision 85)
+++ src/main/resources/ApplicationResources_no.properties	(working copy)
@@ -1,186 +1,186 @@
-
-user.status=Logget inn som: 
-user.logout=Logg ut
-
-# -- validator errors --
-errors.invalid={0} er ugyldig.
-errors.maxlength={0} kan ikke vÊre st¯rre enn {1} tegn.
-errors.minlength={0} kan ikke vÊre mindre enn {1} tegn.
-errors.range={0} er ikke i intervallet fra {1} til {2}.
-errors.required={0} er et obligatorisk felt.
-errors.byte={0} mÂ vÊre en byte.
-errors.date={0} er ikke en dato.
-errors.double={0} mÂ vÊre en double.
-errors.float={0} mÂ vÊre en float.
-errors.integer={0} mÂ vÊre en number.
-errors.long={0} mÂ vÊre en long.
-errors.short={0} mÂ vÊre en short.
-errors.creditcard={0} er ikke et gyldig kredittkort nummer.
-errors.email={0} er en ugyldig e-post adresse.
-errors.phone={0} er et ugyldig telefonnummer.
-errors.zip={0} er et ugyldig postnummer.
-
-# -- other errors --
-errors.cancel=handling avbrutt.
-errors.detail={0}
-errors.general=<strong>Handlingen ble ikke fullf¯rt. Detaljer f¯lger.</strong>
-errors.token=Foresp¯rsel kunne ikke gjennomf¯res. Handlingen er ikke i riktig rekkef¯lge.
-errors.none=Ingen feilbeskjed ble funnet, sjekk server loggen.
-errors.password.mismatch=Ugyldig brukernavn og/eller passord, pr¯v igjen.
-errors.conversion=En feil oppstod under konvertering av web verdier til data verdier.
-errors.twofields=Feltet {0} mÂ ha samme verdi som feltet {1}.
-errors.existing.user=Brukernavnet ({0}) eller e-post adressen ({1}) finnes allerede. Vennligst pr¯v et annet brukernavn.
-
-# -- success messages --
-user.added=Brukerinformasjon for <strong>{0}</strong> har blitt lagt til.
-user.deleted=Brukerprofil for <strong>{0}</strong> har blitt slettet. 
-user.registered=Du har registrert deg for tilgang til dette programmet. 
-user.saved=Din profil har blitt oppdatert.
-user.updated.byAdmin=Brukerinformasjon for <strong>{0}</strong> har blitt oppdatert.
-newuser.email.message={0} har laget en AppFuse konto for deg. Ditt brukernavn og passord er synlig nedenfor.
-reload.succeeded=Valgene er lastet inn pÂ nytt
-
-# -- error page messages --
-errorPage.title=En feil har oppstÂtt
-errorPage.heading=Uffda!
-404.title=Siden finnes ikke
-404.message=Siden du ba om ble ikke funnet. Du kan pr¯ve Â gÂ tilbake til <a href="{0}">Hovedmeny</a>.
-403.title=Ikke tilgang
-403.message=Din rolle tillater ikke visning av denne siden. Vennligst kontakt system administrator hvis du mener at du burde ha tilgang.
-
-# -- login --
-login.title=Logg inn
-login.heading=Logg inn
-login.rememberMe=Husk meg
-login.signup=Ikke medlem? <a href="{0}">Registrer</a> deg for en konto.
-login.passwordHint=Glemt passordet?  FÂ ditt <a href="?" onmouseover="window.status='FÂ ditt passord tilsendt.'; return true" onmouseout="window.status=''; return true" title="FÂ ditt passord tilsendt." onclick="passwordHint(); return false">passord hint sendt pÂ e-post til deg</a>.
-login.passwordHint.sent=Passord hint for <strong>{0}</strong> har blitt sendt til <strong>{1}</strong>.
-login.passwordHint.error=Bruker <strong>{0}</strong> ble ikke funnet i vÂrt system.
-
-# -- mainMenu --
-mainMenu.title=Hovedmenu
-mainMenu.heading=Velkommen!
-mainMenu.message=Gratulerer, du er nÂ logget inn! Som innlogget har du disse valgene
-mainMenu.activeUsers=NÂvÊrende brukere
-
-# -- menu/link messages --
-menu.admin=Administrasjon
-menu.admin.users=Se brukere
-menu.admin.reload=Last inn valg pÂ nytt
-
-menu.user=Rediger profil
-menu.selectFile=Last opp fil
-menu.flushCache=T¯m minne
-menu.clickstream=Sidenavigering
-
-# -- form labels --
-label.username=Brukernavn
-label.password=Passord
-
-# -- button labels --
-button.add=Legg til
-button.cancel=Avbryt
-button.copy=Kopier
-button.delete=Slett
-button.done=Ferdig
-button.edit=Rediger
-button.register=Registrer
-button.save=Lagre
-button.search=S¯k
-button.upload=Last opp
-button.view=Se
-button.reset=Nullstill
-button.login=Logg inn
-
-# -- general values --
-icon.information=Informasjon
-icon.information.img=/images/iconInformation.gif
-icon.email=E-Post
-icon.email.img=/images/iconEmail.gif
-icon.warning=Advarsel
-icon.warning.img=/images/iconWarning.gif
-date.format=dd/MM/yyyy
-
-# -- role form --
-roleForm.name=Navn
-
-# -- user profile page --
-userProfile.title=Brukerinstillinger
-userProfile.heading=Brukerprofil
-userProfile.message=Vennligst oppdater din informasjon i skjemaet under.
-userProfile.admin.message=Du kan oppdatere denne brukerens informasjon i skjemaet under.
-userProfile.showMore=Se mer informasjon
-userProfile.accountSettings=Konto valg
-userProfile.assignRoles=Tildel rolle
-userProfile.cookieLogin=Du kan ikke skifte passord nÂr du har logget inn med <strong>Husk Meg</strong>.  Vennligst logg ut og logg inn igjen for Â skifte passord.
-
-# -- user form --
-user.address.address=Addresse
-user.availableRoles=Tilgjengelige roller
-user.address.city=By
-user.address.country=Land
-user.email=E-Post
-user.firstName=Fornavn
-user.id=Id
-user.lastName=Etternavn
-user.password=Passord
-user.confirmPassword=Bekreft passord
-user.phoneNumber=Telefonnummer
-user.address.postalCode=Postnummer
-user.address.province=Fylke
-user.roles=NÂvÊrende roller
-user.username=Brukernavn
-user.website=Webside
-user.visitWebsite=bes¯k
-user.passwordHint=Passord hint
-user.enabled=Aktiv
-user.accountExpired=UtgÂtt
-user.accountLocked=LÂst
-user.credentialsExpired=Passord utgÂtt
-
-# -- user list page --
-userList.title=Brukerliste
-userList.heading=NÂvÊrende brukere
-userList.nousers=<span>Ingen brukere funnet.</span>
-
-# -- user self-registration --
-signup.title=Registrer
-signup.heading=Registrer ny bruker
-signup.message=Vennligst fyll inn din brukerinformasjon i skjemaet under.
-signup.email.subject=AppFuse Konto Informasjon
-signup.email.message=Du har registrert deg for tilgang til AppFuse. Ditt brukernavn og passord er synlig under.
-
-# -- upload page messages --
-maxLengthExceeded=Filen du pr¯ver Â laste opp er for stor. St¯rste lovlige fil er 2MB.
-upload.title=Filopplasting
-upload.heading=Last opp en fil
-upload.message=Merk at filen som blir lastet opp ikke kan vÊre st¯rre enn 2MB.
-uploadForm.name=Merk filen som
-uploadForm.file=Fil Â laste opp
-
-# -- display page messages -- 
-display.title=Filen ferdig opplastet!
-display.heading=Filinformasjon
-
-# -- flushCache page --
-flushCache.title=T¯m minne
-flushCache.heading=Minne t¯mt!
-flushCache.message=Alt minne t¯mt, du vil komme tilbake til forrige side straks.
-
-# -- clickstreams page --
-clickstreams.title=All sidenavigering
-clickstreams.heading=All sidenavigering
-
-# -- viewstream page --
-viewstream.title=Sidenavigering detaljer
-viewstream.heading=Sidenavigering informasjon
-
-# -- active users page --
-activeUsers.title=Aktive brukere
-activeUsers.heading=NÂvÊrende brukere
-activeUsers.message=F¯lgende er en liste over brukere som har logget inn og der sesjonen ikke er utgÂtt.
-activeUsers.fullName=Fullt navn
-
-# JSF-only messages, remove if not using JSF
-javax.faces.component.UIInput.REQUIRED=Dette er et obligatorisk felt.
+

+user.status=Logget inn som: 

+user.logout=Logg ut

+

+# -- validator errors --

+errors.invalid={0} er ugyldig.

+errors.maxlength={0} kan ikke vÊre st¯rre enn {1} tegn.

+errors.minlength={0} kan ikke vÊre mindre enn {1} tegn.

+errors.range={0} er ikke i intervallet fra {1} til {2}.

+errors.required={0} er et obligatorisk felt.

+errors.byte={0} mÂ vÊre en byte.

+errors.date={0} er ikke en dato.

+errors.double={0} mÂ vÊre en double.

+errors.float={0} mÂ vÊre en float.

+errors.integer={0} mÂ vÊre en number.

+errors.long={0} mÂ vÊre en long.

+errors.short={0} mÂ vÊre en short.

+errors.creditcard={0} er ikke et gyldig kredittkort nummer.

+errors.email={0} er en ugyldig e-post adresse.

+errors.phone={0} er et ugyldig telefonnummer.

+errors.zip={0} er et ugyldig postnummer.

+

+# -- other errors --

+errors.cancel=handling avbrutt.

+errors.detail={0}

+errors.general=Handlingen ble ikke fullf¯rt. Detaljer f¯lger.

+errors.token=Foresp¯rsel kunne ikke gjennomf¯res. Handlingen er ikke i riktig rekkef¯lge.

+errors.none=Ingen feilbeskjed ble funnet, sjekk server loggen.

+errors.password.mismatch=Ugyldig brukernavn og/eller passord, pr¯v igjen.

+errors.conversion=En feil oppstod under konvertering av web verdier til data verdier.

+errors.twofields=Feltet {0} mÂ ha samme verdi som feltet {1}.

+errors.existing.user=Brukernavnet ({0}) eller e-post adressen ({1}) finnes allerede. Vennligst pr¯v et annet brukernavn.

+

+# -- success messages --

+user.added=Brukerinformasjon for {0} har blitt lagt til.

+user.deleted=Brukerprofil for {0} har blitt slettet.

+user.registered=Du har registrert deg for tilgang til dette programmet. 

+user.saved=Din profil har blitt oppdatert.

+user.updated.byAdmin=Brukerinformasjon for {0} har blitt oppdatert.

+newuser.email.message={0} har laget en AppFuse konto for deg. Ditt brukernavn og passord er synlig nedenfor.

+reload.succeeded=Valgene er lastet inn pÂ nytt

+

+# -- error page messages --

+errorPage.title=En feil har oppstÂtt

+errorPage.heading=Uffda!

+404.title=Siden finnes ikke

+404.message=Siden du ba om ble ikke funnet. Du kan pr¯ve Â gÂ tilbake til <a href="{0}">Hovedmeny</a>.

+403.title=Ikke tilgang

+403.message=Din rolle tillater ikke visning av denne siden. Vennligst kontakt system administrator hvis du mener at du burde ha tilgang.

+

+# -- login --

+login.title=Logg inn

+login.heading=Logg inn

+login.rememberMe=Husk meg

+login.signup=Ikke medlem? <a href="{0}">Registrer</a> deg for en konto.

+login.passwordHint=Glemt passordet?  FÂ ditt <a href="?" onmouseover="window.status='FÂ ditt passord tilsendt.'; return true" onmouseout="window.status=''; return true" title="FÂ ditt passord tilsendt." onclick="passwordHint(); return false">passord hint sendt pÂ e-post til deg</a>.

+login.passwordHint.sent=Passord hint for {0} har blitt sendt til {1}.

+login.passwordHint.error=Bruker {0} ble ikke funnet i vÂrt system.

+

+# -- mainMenu --

+mainMenu.title=Hovedmeny

+mainMenu.heading=Velkommen!

+mainMenu.message=Gratulerer, du er nÂ logget inn! Som innlogget har du disse valgene

+mainMenu.activeUsers=NÂvÊrende brukere

+

+# -- menu/link messages --

+menu.admin=Administrasjon

+menu.admin.users=Se brukere

+menu.admin.reload=Last inn valg pÂ nytt

+

+menu.user=Rediger profil

+menu.selectFile=Last opp fil

+menu.flushCache=T¯m minne

+menu.clickstream=Sidenavigering

+

+# -- form labels --

+label.username=Brukernavn

+label.password=Passord

+

+# -- button labels --

+button.add=Legg til

+button.cancel=Avbryt

+button.copy=Kopier

+button.delete=Slett

+button.done=Ferdig

+button.edit=Rediger

+button.register=Registrer

+button.save=Lagre

+button.search=S¯k

+button.upload=Last opp

+button.view=Se

+button.reset=Nullstill

+button.login=Logg inn

+

+# -- general values --

+icon.information=Informasjon

+icon.information.img=/images/iconInformation.gif

+icon.email=E-Post

+icon.email.img=/images/iconEmail.gif

+icon.warning=Advarsel

+icon.warning.img=/images/iconWarning.gif

+date.format=dd/MM/yyyy

+

+# -- role form --

+roleForm.name=Navn

+

+# -- user profile page --

+userProfile.title=Brukerinstillinger

+userProfile.heading=Brukerprofil

+userProfile.message=Vennligst oppdater din informasjon i skjemaet under.

+userProfile.admin.message=Du kan oppdatere denne brukerens informasjon i skjemaet under.

+userProfile.showMore=Se mer informasjon

+userProfile.accountSettings=Konto valg

+userProfile.assignRoles=Tildel rolle

+userProfile.cookieLogin=Du kan ikke skifte passord nÂr du har logget inn med <strong>Husk Meg</strong>.  Vennligst logg ut og logg inn igjen for Â skifte passord.

+

+# -- user form --

+user.address.address=Addresse

+user.availableRoles=Tilgjengelige roller

+user.address.city=By

+user.address.country=Land

+user.email=E-Post

+user.firstName=Fornavn

+user.id=Id

+user.lastName=Etternavn

+user.password=Passord

+user.confirmPassword=Bekreft passord

+user.phoneNumber=Telefonnummer

+user.address.postalCode=Postnummer

+user.address.province=Fylke

+user.roles=NÂvÊrende roller

+user.username=Brukernavn

+user.website=Webside

+user.visitWebsite=bes¯k

+user.passwordHint=Passord hint

+user.enabled=Aktiv

+user.accountExpired=UtgÂtt

+user.accountLocked=LÂst

+user.credentialsExpired=Passord utgÂtt

+

+# -- user list page --

+userList.title=Brukerliste

+userList.heading=NÂvÊrende brukere

+userList.nousers=<span>Ingen brukere funnet.</span>

+

+# -- user self-registration --

+signup.title=Registrer

+signup.heading=Registrer ny bruker

+signup.message=Vennligst fyll inn din brukerinformasjon i skjemaet under.

+signup.email.subject=AppFuse Konto Informasjon

+signup.email.message=Du har registrert deg for tilgang til AppFuse. Ditt brukernavn og passord er synlig under.

+

+# -- upload page messages --

+maxLengthExceeded=Filen du pr¯ver Â laste opp er for stor. St¯rste lovlige fil er 2MB.

+upload.title=Filopplasting

+upload.heading=Last opp en fil

+upload.message=Merk at filen som blir lastet opp ikke kan vÊre st¯rre enn 2MB.

+uploadForm.name=Merk filen som

+uploadForm.file=Fil Â laste opp

+

+# -- display page messages -- 

+display.title=Filen ferdig opplastet!

+display.heading=Filinformasjon

+

+# -- flushCache page --

+flushCache.title=T¯m minne

+flushCache.heading=Minne t¯mt!

+flushCache.message=Alt minne t¯mt, du vil komme tilbake til forrige side straks.

+

+# -- clickstreams page --

+clickstreams.title=All sidenavigering

+clickstreams.heading=All sidenavigering

+

+# -- viewstream page --

+viewstream.title=Sidenavigering detaljer

+viewstream.heading=Sidenavigering informasjon

+

+# -- active users page --

+activeUsers.title=Aktive brukere

+activeUsers.heading=NÂvÊrende brukere

+activeUsers.message=F¯lgende er en liste over brukere som har logget inn og der sesjonen ikke er utgÂtt.

+activeUsers.fullName=Fullt navn

+

+# JSF-only messages, remove if not using JSF

+javax.faces.component.UIInput.REQUIRED=Dette er et obligatorisk felt.

 activeUsers.summary={0} Bruker(e) funnet, viser {1} bruker(e), fra {2} til {3}. Side {4} / {5}
\ No newline at end of file
Index: src/main/resources/ApplicationResources.properties
===================================================================
--- src/main/resources/ApplicationResources.properties	(revision 85)
+++ src/main/resources/ApplicationResources.properties	(working copy)
@@ -32,7 +32,7 @@
 # -- other errors --
 errors.cancel=Operation cancelled.
 errors.detail={0}
-errors.general=<strong>The process did not complete. Details should follow.</strong>
+errors.general=The process did not complete. Details should follow.
 errors.token=Request could not be completed. Operation is not in sequence.
 errors.none=No error message was found, check your server logs.
 errors.password.mismatch=Invalid username and/or password, please try again.
@@ -41,11 +41,11 @@
 errors.existing.user=This username ({0}) or e-mail address ({1}) already exists.  Please try a different username.
 
 # -- success messages --
-user.added=User information for <strong>{0}</strong> has been added successfully.
-user.deleted=User Profile for <strong>{0}</strong> has been deleted successfully. 
+user.added=User information for {0} has been added successfully.
+user.deleted=User Profile for {0} has been deleted successfully.
 user.registered=You have successfully registered for access to this application. 
 user.saved=Your profile has been updated successfully.
-user.updated.byAdmin=User information for <strong>{0}</strong> has been successfully updated.
+user.updated.byAdmin=User information for {0} has been successfully updated.
 newuser.email.message={0} has created an AppFuse account for you.  Your username and password information is below.
 reload.succeeded=Reloading options completed successfully.
 
@@ -63,8 +63,8 @@
 login.rememberMe=Remember Me
 login.signup=Not a member? <a href="{0}">Signup</a> for an account.
 login.passwordHint=Forgot your password?  Have your <a href="?" onmouseover="window.status='Have your password hint sent to you.'; return true" onmouseout="window.status=''; return true" title="Have your password hint sent to you." onclick="passwordHint(); return false">password hint e-mailed to you</a>.
-login.passwordHint.sent=The password hint for <strong>{0}</strong> has been sent to <strong>{1}</strong>.
-login.passwordHint.error=The username <strong>{0}</strong> was not found in our database.
+login.passwordHint.sent=The password hint for {0} has been sent to {1}.
+login.passwordHint.error=The username {0} was not found in our database.
 
 # -- mainMenu --
 mainMenu.title=Main Menu
Index: src/main/resources/ApplicationResources_zh.properties
===================================================================
--- src/main/resources/ApplicationResources_zh.properties	(revision 85)
+++ src/main/resources/ApplicationResources_zh.properties	(working copy)
@@ -1,5 +1,4 @@
-Ôªø## Do NOT delete! Keep this line to avoid the native2ascii UTF-8 BOM bug. See #APF-639
-
+Ôªø
 user.status=ÂΩìÂâçÁî®Êà∑: 
 user.logout=ÈÄÄÂá∫
 
@@ -24,7 +23,7 @@
 # -- other errors --
 errors.cancel=Êìç‰ΩúË¢´ÂèñÊ∂à„ÄÇ
 errors.detail={0}
-errors.general=<strong>Êìç‰ΩúÊú™ÂÆåÊàê„ÄÇËØ¶ÁªÜÂéüÂõ†Â¶Ç‰∏ã„ÄÇ</strong>
+errors.general=Êìç‰ΩúÊú™ÂÆåÊàê„ÄÇËØ¶ÁªÜÂéüÂõ†Â¶Ç‰∏ã„ÄÇ
 errors.token=ËØ∑Ê±ÇÊú™ÂÆåÂÖ®Â§ÑÁêÜ„ÄÇÊìç‰ΩúÈ°∫Â∫èÈîôËØØ„ÄÇ
 errors.none=Êó†ÈîôËØØÊ∂àÊÅØÔºåËØ∑Ê£ÄÊü•ÊúçÂä°Âô®Êó•ÂøóÊñá‰ª∂„ÄÇ
 errors.password.mismatch=Êó†ÊïàÁî®Êà∑ÂêçÊàñÂØÜÁ†ÅÔºåËØ∑ÈáçËØï„ÄÇ
@@ -33,11 +32,11 @@
 errors.existing.user=Áî®Êà∑Âêç ({0}) Êàñe-mailÂú∞ÂùÄ ({1}) Â∑≤Â≠òÂú®„ÄÇËØ∑ÂÜçÊ¨°Â∞ùËØï‰∏çÂêåÂêçÁß∞„ÄÇ
 
 # -- success messages --
-user.added=Áî®Êà∑ <strong>{0}</strong> ÁöÑ‰ø°ÊÅØÊ∑ªÂä†ÊàêÂäü„ÄÇ
-user.deleted=Áî®Êà∑ <strong>{0}</strong> ÁöÑ‰ø°ÊÅØÂà†Èô§ÊàêÂäü„ÄÇ 
+user.added=Áî®Êà∑ {0} ÁöÑ‰ø°ÊÅØÊ∑ªÂä†ÊàêÂäü„ÄÇ
+user.deleted=Áî®Êà∑ {0} ÁöÑ‰ø°ÊÅØÂà†Èô§ÊàêÂäü„ÄÇ
 user.registered=Ê≥®ÂÜåÊàêÂäüÔºåÊÇ®ÂèØ‰ª•ÂºÄÂßã‰ΩøÁî®Á≥ªÁªü„ÄÇ
 user.saved=ÊÇ®ÁöÑ‰ø°ÊÅØÂ∑≤ÊàêÂäüÊõ¥Êñ∞„ÄÇ
-user.updated.byAdmin=Áî®Êà∑ <strong>{0}</strong> ÁöÑ‰ø°ÊÅØÂ∑≤ÊàêÂäüÊõ¥Êñ∞„ÄÇ
+user.updated.byAdmin=Áî®Êà∑ {0} ÁöÑ‰ø°ÊÅØÂ∑≤ÊàêÂäüÊõ¥Êñ∞„ÄÇ
 newuser.email.message={0} ‰∏∫ÊÇ®ÊàêÂäüÂàõÂª∫‰∫Ü‰∏Ä‰∏™AppFuseÂ∏êÂè∑„ÄÇÊÇ®ÁöÑÁî®Êà∑ÂêçÂíåÂØÜÁ†Å‰ø°ÊÅØÂ¶Ç‰∏ãÔºö
 reload.succeeded=Â∑≤ÁªèÊàêÂäüÈáçËΩΩ.
 
@@ -55,8 +54,8 @@
 login.rememberMe=ËÆ©Á≥ªÁªüËÆ∞‰ΩèÊàë
 login.signup=‰∏çÊòØÊ≥®ÂÜåÁî®Êà∑? <a href="{0}">Áî≥ËØ∑</a> ‰∏Ä‰∏™Â∏êÂè∑„ÄÇ
 login.passwordHint=ÂøòËÆ∞‰∫ÜÂØÜÁ†Å?  ËÆ©Á≥ªÁªüÂ∞Ü <a href="?" onmouseover="window.status='Á≥ªÁªüÂèëÈÄÅÂØÜÁ†ÅÊèêÁ§∫„ÄÇ'; return true" onmouseout="window.status=''; return true" title="Á≥ªÁªüÂèëÈÄÅÂØÜÁ†ÅÊèêÁ§∫„ÄÇ" onclick="passwordHint(); return false">ÂØÜÁ†ÅÊèêÁ§∫‰ø°ÊÅØÂ∑≤e-mailÂΩ¢ÂºèÂèëÈÄÅÁªôÊÇ®</a>„ÄÇ
-login.passwordHint.sent=<strong>{0}</strong> ÁöÑÂØÜÁ†ÅÊèêÁ§∫Â∑≤ÊàêÂäüÂèëÈÄÅÂà∞ <strong>{1}</strong>„ÄÇ
-login.passwordHint.error=Áî®Êà∑Âêç <strong>{0}</strong> Âú®Á≥ªÁªüÊï∞ÊçÆÂ∫ì‰∏≠Êú™ÊâæÂà∞„ÄÇ
+login.passwordHint.sent={0}</strong> ÁöÑÂØÜÁ†ÅÊèêÁ§∫Â∑≤ÊàêÂäüÂèëÈÄÅÂà∞ {1}„ÄÇ
+login.passwordHint.error=Áî®Êà∑Âêç {0} Âú®Á≥ªÁªüÊï∞ÊçÆÂ∫ì‰∏≠Êú™ÊâæÂà∞„ÄÇ
 
 # -- mainMenu --
 mainMenu.title=‰∏ªËèúÂçï
Index: src/main/resources/ApplicationResources_pt.properties
===================================================================
--- src/main/resources/ApplicationResources_pt.properties	(revision 85)
+++ src/main/resources/ApplicationResources_pt.properties	(working copy)
@@ -1,3 +1,4 @@
+Ôªø
 user.status=Registrado como: 
 user.logout=Sair
 
@@ -2,9 +3,9 @@
 # -- validator errors --
-errors.invalid={0} È inv·lido.
-errors.maxlength={0} n„o pode ser maior que {1} caracter(es).
-errors.minlength={0} n„o pode ser menos que {1} caracter(es).
-errors.range={0} n„o est· na escala {1} a {2}.
-errors.required={0} È um campo obrigatÛrio.
+errors.invalid={0} √© inv√°lido.
+errors.maxlength={0} n√£o pode ser maior que {1} caracter(es).
+errors.minlength={0} n√£o pode ser menos que {1} caracter(es).
+errors.range={0} n√£o est√° na escala {1} a {2}.
+errors.required={0} √© um campo obrigat√≥rio.
 errors.byte={0} deve ser um byte.
-errors.date={0} n„o È uma data.
+errors.date={0} n√£o √© uma data.
 errors.double={0} deve ser double.
@@ -14,76 +15,78 @@
 errors.integer={0} deve ser um number.
 errors.long={0} deve ser um long.
 errors.short={0} deve ser um short.
-errors.creditcard={0} n„o È um n˙mero de cart„o de crÈdito v·lido.
-errors.email={0} È um endereÁo de e-mail inv·lido.
-errors.phone={0} È n˙mero de telefone inv·lido.
-errors.zip={0} È um cÛdigo postal inv·lido.
+errors.creditcard={0} n√£o √© um n√∫mero de cart√£o de cr√©dito v√°lido.
+errors.email={0} √© um endere√ßo de e-mail inv√°lido.
+errors.phone={0} √© n√∫mero de telefone inv√°lido.
+errors.zip={0} √© um c√≥digo postal inv√°lido.
 
 # -- other errors --
-errors.cancel=OperaÁ„o cancelada.
+errors.cancel=Opera√ß√£o cancelada.
 errors.detail={0}
-errors.general=<strong>O processo n„o completou. Os detalhes devem seguir.</strong>
-errors.token=RequisiÁ„o n„o poderia ser completada. A operaÁ„o n„o est· em ordem.
+errors.general=O processo n√£o foi conclu√≠do com sucesso. Os detalhes devem seguir.
+errors.token=Requisi√ß√£o n√£o poderia ser completada. A opera√ß√£o n√£o est√° em ordem.
 errors.none=Nenhuma mensagem de erro foi encontrada, verifica seus registros do servidor.
-errors.password.mismatch=Nome do usu·rio ou senha inv·lido, por favor tente novamente.
-errors.conversion=Um erro ocorreu ao converter valores web para valores de dados.
+errors.password.mismatch=Nome do utilizador ou senha inv√°lido, por favor tente novamente.
+errors.conversion=Ocorreu um erro ao converter valores web para valores de dados.
 errors.twofields=O campo {0} tem que ter o mesmo valor que o campo {1}.
-errors.existing.user=Este nome de usu·rio ({0}) ou endereÁo de e-mail ({1}) j· existe.  Por favor tente um nome de usu·rio diferente.
+errors.existing.user=Este nome de utilizador ({0}) ou endere√ßo de e-mail ({1}) j√° existe.  Por favor tente um nome de utilizador diferente.
 
 # -- success messages --
-user.added=InformaÁ„o de Usu·rio para <strong>{0}</strong> foi adicionada com sucesso.
-user.deleted=Perfil de Usu·rio para <strong>{0}</strong> foi deletada com sucesso. 
-user.registered=VocÍ registou com sucesso para o acesso a esta aplicaÁ„o.
-user.saved=Seu perfil foi atualizado com sucesso.
-user.updated.byAdmin=InformaÁ„o de Usu·rio para <strong>{0}</strong> foi atualizada com sucesso.
-newuser.email.message={0} criou uma conta AppFuse para vocÍ.  Sua informaÁ„o nome de usu·rio e senha est· logo abaixo.
-reload.succeeded=AtualizaÁ„o das opÁıes realizada com sucesso.
+user.added=Informa√ß√£o de utilizador para {0} foi adicionada com sucesso.
+user.deleted=Perfil de utilizador para {0} foi apagada com sucesso.
+user.registered=Acabou de se registar com sucesso para o acesso a esta aplica√ß√£o.
+user.saved=Perfil actualizado com sucesso.
+user.updated.byAdmin=Informa√ß√£o de Utilizador para {0} foi actualizada com sucesso.
+newuser.email.message={0} criou uma conta AppFuse para voc√™.  Sua informa√ß√£o nome de utilizador e senha est√° mencionada mais abaixo.
+reload.succeeded=Actualiza√ß√£o das op√ß√µes realizada com sucesso.
 
 # -- error page messages --
 errorPage.title=Um erro ocorreu
 errorPage.heading=Yikes!
-404.title=P·gina n„o encontrada
-404.message=A p·gina que vocÍ requisitou n„o foi encontrada.  VocÍ pode tentar retornar para <a href="{0}">Main Menu</a>.Enquanto vocÍ est· aqui, que tal uma linda figura para anim·-lo?
+404.title=P√°gina n√£o encontrada
+404.message=A p√°gina que voc√™ requisitou n√£o foi encontrada.  Voc√™ pode tentar retornar para <a href="{0}">Main Menu</a>.Enquanto voc√™ est√° aqui, que tal uma linda figura para anim√°-lo?
 403.title=Acesso Negado
-403.message=Seu corrente perfil n„o permite a vocÍ a visualizaÁ„o desta p·gina. Por favor entrar em contato com seu administrador de sistemas se vocÍ acredita que deveria ter acesso.  Nesse meio tempo, que tal uma linda figura para anim·-lo?
+403.message=O seu perfil n√£o permite a visualiza√ß√£o desta p√°gina. Por favor entre em contato com seu administrador de sistemas se voc√™ acredita que deveria ter acesso.  No entretanto, que tal uma linda figura para anim√°-lo?
 
 # -- login --
-login.title=Registrar
-login.heading=Registrar
+login.title=Registar
+login.heading=Registar
 login.rememberMe=Lembre-me
-login.signup=N„o È um membro? <a href="{0}">Registre-se</a> para uma conta.
-login.passwordHint=Esqueceu sua senha? Tenha <a href="?" onmouseover="window.status='Tenha sua dica de senha enviada a vocÍ.'; return true" onmouseout="window.status=''; return true" title="Tenha sua dica de senha enviada a vocÍ." onclick="passwordHint(); return false">sua dica de senha enviada a vocÍ</a>.
-login.passwordHint.sent=A dica de senha para <strong>{0}</strong> foi enviada para <strong>{1}</strong>.
-login.passwordHint.error=O nome de usu·rio <strong>{0}</strong> n„o foi encontrado no banco de dados.
+login.signup=N√£o √© um membro? <a href="{0}">Registe-se</a> para uma conta.
+login.passwordHint=Esqueceu sua senha? Tenha <a href="?" onmouseover="window.status='Tenha sua dica de senha enviada a voc√™.'; return true" onmouseout="window.status=''; return true" title="Tenha sua dica de senha enviada a voc√™." onclick="passwordHint(); return false">sua dica de senha enviada a voc√™</a>.
+login.passwordHint.sent=A dica de senha para {0} foi enviada para {1}.
+login.passwordHint.error=O nome de utilizador {0} n√£o consta na base de dados.
 
 # -- mainMenu --
 mainMenu.title=Menu Principal
 mainMenu.heading=Bem vindo!
-mainMenu.message=Parabens, registro efetuado com sucesso!  Agora que vocÍ est· registrado, vocÍ tem as seguintes opÁıes:
-mainMenu.activeUsers=Usu·rios Registrados
+mainMenu.message=Parabens, registo efectuado com sucesso!  Agora que est√° registado, tem as seguintes op√ß√µes:
+mainMenu.activeUsers=Utilizadores Registrados
 
 # -- menu/link messages --
-menu.admin=AdministraÁ„o
-menu.admin.users=Visualizar Usu·rios
-menu.admin.reload=Atualizar OpÁıes
+menu.admin=Administra√ß√£o
+menu.admin.users=Visualizar Utilizadores
+menu.admin.reload=Actualizar Op√ß√µes
 menu.user=Editar Perfil
-menu.selectFile=Carregar um arquivo
-menu.flushCache=Liberar Cache
+menu.selectFile=Carregar um ficheiro
+menu.flushCache=Limpar Cache
 menu.clickstream=Clickstream
 
+menu.portorama=Obtenha o software aqui!
+
 # -- form labels --
-label.username=Nome de Usu·rio
+label.username=Nome de Utilizador
 label.password=Senha
 
 # -- button labels --
 button.add=Adicionar
 button.cancel=Cancelar
 button.copy=Copiar
-button.delete=Deletar
-button.done=Feito
+button.delete=Apagar
+button.done=Terminado
 button.edit=Editar
-button.register=Registre-se
-button.save=Salvar
+button.register=Registe-se
+button.save=Guardar
 button.search=Pesquisar
 button.upload=Carregar
 button.view=Visualizar
@@ -91,11 +94,11 @@
 button.login=Entrar
 
 # -- general values --
-icon.information=InformaÁ„o
+icon.information=Informa√ß√£o
 icon.information.img=/images/iconInformation.gif
 icon.email=E-Mail
 icon.email.img=/images/iconEmail.gif
-icon.warning=AtenÁ„o
+icon.warning=Aten√ß√£o
 icon.warning.img=/images/iconWarning.gif
 date.format=MM/dd/yyyy
 
@@ -103,20 +106,20 @@
 roleForm.name=Nome
 
 # -- user profile page --
-userProfile.title=ConfiguraÁıes de Usu·rio
-userProfile.heading=Perfil de Usu·rio
-userProfile.message=Por favor atualize sua imformaÁ„o usando o formul·rio abaixo.
-userProfile.admin.message=VocÍ pode atualizar a imformaÁ„o deste usu·rio no formul·rio abaixo.
-userProfile.showMore=Veja Mais Informações
-userProfile.accountSettings=Configurações da Conta
+userProfile.title=Configura√ß√µes de Utilizador
+userProfile.heading=Perfil de Utilizador
+userProfile.message=Por favor actualize sua imforma√ß√£o utilizando o formul√°rio abaixo.
+userProfile.admin.message=Pode actualizar a informa√ß√£o deste utilizador no formul√°rio abaixo.
+userProfile.showMore=Veja Mais Informa√ß√µees
+userProfile.accountSettings=Configura√ß√µes da Conta
 userProfile.assignRoles=Atribuir Perfis
-userProfile.cookieLogin=VocÍ n„o pode alter senhas quando registrado com a caracterÌstica<strong>Lembre-me</strong>. Por favor saia e registre novamente para alterar senhas.
+userProfile.cookieLogin=Voc√™ n√£o pode alter senhas quando registado com a caracter√≠stica<strong>Lembre-me</strong>. Por favor saia e registe novamente para alterar senhas.
 
 # -- user form --
-user.address.address=EndereÁo
-user.availableRoles=Perfis disponÌveis
+user.address.address=Endere√ßo
+user.availableRoles=Perfis dispon√≠veis
 user.address.city=Cidade
-user.address.country=PaÌs
+user.address.country=Pa√≠s
 user.email=E-Mail
 user.firstName=Primeiro Nome
 user.id=Id
@@ -124,10 +127,10 @@
 user.password=Senha
 user.confirmPassword=Comfirmar Senha
 user.phoneNumber=Numero Telefone
-user.address.postalCode=CÛdigo Postal
+user.address.postalCode=C√≥digo Postal
 user.address.province=Estado
 user.roles=Perfis Corrente
-user.username=Nome de Usu·rio
+user.username=Nome de Utilizador
 user.website=Website
 user.visitWebsite=visite
 user.passwordHint=Dica de Senha
@@ -136,34 +139,39 @@
 user.accountLocked=Bloqueada
 user.credentialsExpired=Senha Expirada
 
+# Portorama 
+user.snarkport=Porto Peer-to-Peer
+user.rating=Intensidade do Filtro
+
+
 # -- user list page --
-userList.title=Lista Usu·rio
-userList.heading=Usu·rios Corrente
-userList.nousers=<span>Nenhum usu·rio encontrado.</span>
+userList.title=Lista Utilizador
+userList.heading=Utilizadores Correntes
+userList.nousers=<span>Nenhum utilizador encontrado.</span>
 
 # -- user self-registration --
-signup.title=Registre-se
-signup.heading=Registro de Novo Usu·rio
-signup.message=Por favor entre com sua informaÁ„o no formul·rio abaixo.
-signup.email.subject=InformaÁ„o de Conta AppFuse
-signup.email.message=VocÍ se registrou com sucesso para acesso a AppFuse.  Sua informaÁ„o nome de usu·rio e senha est· logo abaixo.
+signup.title=Registe-se
+signup.heading=Registo de Novo Utilizador
+signup.message=Por favor insira a sua informa√ß√£o informa√ß√£o no formul√°rio abaixo.
+signup.email.subject=Informa√ß√£o de Conta AppFuse
+signup.email.message=Registou-se com sucesso para acesso a AppFuse. Sua informa√ß√£o: nome de utilizador e senha est√£o mais abaixo.
 
 # -- upload page messages --
-maxLengthExceeded=O arquivo que vocÍ esta tentando carregar È muito grande.  O m·ximo permitido È 2 MB.
+maxLengthExceeded=O arquivo que voc√™ esta a tentar carregar √© muito grande.  O m√°ximo permitido √© 2 MB.
 upload.title=Carregar Arquivo
 upload.heading=Carrega um Arquivo
-upload.message=Observe que o tamanho m·ximo permitido para um arquivo carregado para esta aplicaÁ„o È 2 MB.
-uploadForm.name=Nome Amig·vel 
+upload.message=Note que o tamanho m√°ximo permitido para um arquivo carregado para esta aplica√ß√£o √© 2 MB.
+uploadForm.name=Nome Amig√°vel 
 uploadForm.file=Arquivo a Carregar
 
 # -- display page messages -- 
 display.title=Arquivo Carregado com Sucesso!
-display.heading=InformÁ„o de Arquivo
+display.heading=Informa√ß√£o de Arquivo
 
 # -- flushCache page --
-flushCache.title=Liberar Cache
-flushCache.heading=Chache Liberado com Sucesso!
-flushCache.message=Todos Chaches Liberados com Sucesso, retorno ‡ p·gina anterior em  2 segundos.
+flushCache.title=Limpar Cache
+flushCache.heading=Cache Limpa com Sucesso!
+flushCache.message=Todas as Caches Limpas com sucesso, retornando √† p√°gina anterior em  2 segundos.
 
 # -- clickstreams page --
 clickstreams.title=Todos Clickstreams
@@ -171,14 +179,14 @@
 
 # -- viewstream page --
 viewstream.title=Stream Detalhes
-viewstream.heading=Stream InformaÁ„o
+viewstream.heading=Stream Informa√ß√£o
 
 # -- active users page --
-activeUsers.title=Usu·rios Ativos
-activeUsers.heading=Usu·rios Corrente
-activeUsers.message=O seguinte È uma lista de usu·rios que se registraram e as suas sessıes n„o expiraram.
-activeUsers.fullName=Todo Nome
+activeUsers.title=Utilizadores Activos
+activeUsers.heading=Utilizadores Correntes
+activeUsers.message=A seguinte listagem referencia os utilizadores que se registaram e as suas sess√µes n√£o expiraram.
+activeUsers.fullName=Nome Completo
 
 # JSF-only messages, remove if not using JSF
-javax.faces.component.UIInput.REQUIRED={0} È um campo obrigatÛrio.
-activeUsers.summary={0} Usuário(s) encontrado(s), exibindo {1} usuário(s), de {2} a {3}. Página {4} / {5}
\ No newline at end of file
+javax.faces.component.UIInput.REQUIRED={0} √© um campo obrigat√≥rio.
+activeUsers.summary={0} Utilizador(es) encontrado(s), exibindo {1} utilizador(es), de {2} a {3}. P√°gina {4} / {5}
Index: src/main/resources/ApplicationResources_tr.properties
===================================================================
--- src/main/resources/ApplicationResources_tr.properties	(revision 85)
+++ src/main/resources/ApplicationResources_tr.properties	(working copy)
@@ -1,186 +1,186 @@
-

-user.status=Oturum a√ßan kullanƒ±cƒ± :

-user.logout=√áƒ±kƒ±≈ü

-

-# -- validator errors --

-errors.invalid={0} ge√ßersiz.

-errors.maxlength={0}  {1} karakterden fazla olamaz.

-errors.minlength={0}  {1} karakterden az olamaz.

-errors.range={0}  {1} ve {2} aralƒ±ƒüƒ±nda deƒüil.

-errors.required={0} gerekli bir alan.

-errors.byte={0} byte tipinde olmalƒ±.

-errors.date={0} tarih tipinde deƒüil.

-errors.double={0} double tipinde olmalƒ±.

-errors.float={0} float tipinde olmalƒ±.

-errors.integer={0} bir rakam olmalƒ±.

-errors.long={0} long tipinde olmalƒ±.

-errors.short={0} short tipinde olmalƒ±.

-errors.creditcard={0} ge√ßerli bir kredi kartƒ± numarasƒ± deƒüil.

-errors.email={0} ge√ßersiz e-posta adresi.

-errors.phone={0} ge√ßersiz bir telefon numarasƒ±.

-errors.zip={0} ge√ßersiz posta kodu.

-

-# -- other errors --

-errors.cancel=ƒ∞≈ülem iptal edildi.

-errors.detail={0}

-errors.general=<strong>ƒ∞≈ülem tamamlanmadƒ±. Detaylar a≈üaƒüƒ±daki gibi olmalƒ±.</strong>

-errors.token=ƒ∞stek tamamlanamadƒ±. ƒ∞≈ülem y√ºr√ºrl√ºl√ºkte deƒüil.

-errors.none=Hata mesajƒ± bulunamadƒ±, server loglarƒ±na bakƒ±nƒ±z.

-errors.password.mismatch=Yanlƒ±≈ü kullanƒ±cƒ± adƒ± ve/veya ≈üifre, l√ºtfen tekrar deneyiniz.

-errors.conversion=Web deƒüerlerini veri deƒüerlerine √ßevirirken bir hata olu≈ütu.

-errors.twofields={0} alanƒ± {1} alanƒ± ile aynƒ± olmalƒ±.

-errors.existing.user=Bu kullanƒ±cƒ± adƒ± ({0}) veya e-posta adresi ({1}) sisteme kayƒ±tlƒ±dƒ±r.  L√ºtfen deƒüi≈üik bir kullanƒ±cƒ± adƒ± ile tekrar deneyiniz.

-

-# -- success messages --

-user.added= <strong>{0}</strong> i√ßin kullanƒ±cƒ± bilgisi ba≈üarƒ±yla eklendi.

-user.deleted=<strong>{0}</strong> i√ßin kullanƒ±cƒ± profili ba≈üarƒ±yla silindi.

-user.registered=Uygulamaya eri≈üebilmek i√ßin ba≈üarƒ±yla kayƒ±t oldunuz.

-user.saved=Profiliniz ba≈üarƒ±yla kayƒ±t edildi.

-user.updated.byAdmin=<strong>{0}</strong> i√ßin kullanƒ±cƒ± bilgisi g√ºncellendi.

-newuser.email.message={0} sizin i√ßin bir AppFuse hesabƒ± yarattƒ±.  Kullanƒ±cƒ± adƒ± ve ≈üifre bilginiz a≈üaƒüƒ±dadƒ±r.

-reload.succeeded=Se√ßeneklerin tekrar y√ºklenmesi ba≈üarƒ±yla ger√ßekle≈üti.

-

-# -- error page messages --

-errorPage.title=Bir hata olu≈ütu

-errorPage.heading=Opps!

-404.title=Sayfa bulunamadƒ±

-404.message=ƒ∞stediƒüiniz sayfa bulunamadƒ±.   <a href="{0}">Ana Sayfaya</a> d√∂nmeyi deneyebilirsiniz. Buradayken nasƒ±l bir g√ºzel resim sizi ne≈üelendirebilir ?

-403.title=Eri≈üim Engellendi

-403.message=Sahip olduƒüunuz yetki bu sayfayƒ± g√∂rmek i√ßin yeterli deƒüil.  Eri≈üebilmeniz gerektiƒüini d√º≈ü√ºn√ºyorsanƒ±z l√ºtfen ,sistem y√∂neticinizle g√∂r√º≈ü√ºn.  Bu arada , g√ºzel bir resmin sizi ne≈üelendirmesine ne dersiniz ?

-

-# -- login --

-login.title=Giri≈ü

-login.heading=Giri≈ü

-login.rememberMe=Beni hatƒ±rla

-login.signup=√úye deƒüil misiniz ? Bir kullanƒ±cƒ± hesabƒ± i√ßin <a href="{0}">Kayƒ±t Ol !</a> .

-login.passwordHint=≈ûifrenizi unuttunuz mu?   <a href="?" onmouseover="window.status='≈ûifre ipucunuzu e-posta adresinize yollayƒ±n'; return true" onmouseout="window.status=''; return true" title="\u00c5\ufffdifre ipucunuzu e-posta adresinize yollayƒ±n" onclick="passwordHint(); return false">≈ûifre ipucunuzu e-posta adresinize yollayƒ±n</a>.

-login.passwordHint.sent=<strong>{0}</strong> i√ßin ≈üifre ipucu  <strong>{1}</strong>na yollandƒ±.

-login.passwordHint.error=Kullanƒ±cƒ± adƒ± <strong>{0}</strong> veri tabanƒ±nda bulunamadƒ±.

-

-# -- mainMenu --

-mainMenu.title=Ana Men√º

-mainMenu.heading=Ho≈ü Geldiniz!

-mainMenu.message=Tebrikler, sisteme ba≈üarƒ±lƒ± bir giri≈ü yaptƒ±nƒ±z!  Sisteme giri≈ü yaptƒ±nƒ±z, ≈üu se√ßeneklere sahipsiniz:

-mainMenu.activeUsers=Mevcut Aktif Kullanƒ±cƒ±lar

-

-# -- menu/link messages --

-menu.admin=Y√∂netim

-menu.admin.users=Kullanƒ±cƒ±larƒ± G√∂r

-menu.admin.reload=Se√ßenekleri Tekrar Y√ºkle

-

-menu.user=Bilgilerini G√ºncelle

-menu.selectFile=Dosya Y√ºkle

-menu.flushCache=√ñnbellek Temizleme

-menu.clickstream=Tƒ±klama ƒ∞zi

-

-# -- form labels --

-label.username=Kullanƒ±cƒ± Adƒ±

-label.password=≈ûifre

-

-# -- button labels --

-button.add=Ekle

-button.cancel=ƒ∞ptal

-button.copy=Kopyala

-button.delete=Sil

-button.done=Bitti

-button.edit=G√ºncelle

-button.register=Kayƒ±t Ol

-button.save=Kaydet

-button.search=Ara

-button.upload=Y√ºkle

-button.view=G√∂r√ºnt√º

-button.reset=Yeniden Ba≈ülat

-button.login=Giri≈ü Yap

-

-# -- general values --

-icon.information=Bilgi

-icon.information.img=/images/iconInformation.gif

-icon.email=E-Posta

-icon.email.img=/images/iconEmail.gif

-icon.warning=Uyarƒ±

-icon.warning.img=/images/iconWarning.gif

-date.format=dd/MM/yyyy

-

-# -- role form --

-roleForm.name=ƒ∞sim

-

-# -- user profile page --

-userProfile.title=Kullanƒ±cƒ± Ayarlarƒ±

-userProfile.heading=Kullanƒ±cƒ± Profili

-userProfile.message=L√ºtfen a≈üaƒüƒ±daki formu kullanarak kullanƒ±cƒ± bilgilerinizi g√ºncelleyiniz.

-userProfile.admin.message=Bu kullanƒ±cƒ±nƒ±n bilgilerini a≈üaƒüƒ±daki formu kullanarak g√ºncelleyebilirsiniz.

-userProfile.showMore=Daha Fazla Bilgi Edinin

-userProfile.accountSettings=Kullanƒ±cƒ± Hesabƒ± Ayarlarƒ±

-userProfile.assignRoles=G√∂rev Ata

-userProfile.cookieLogin=<strong>Beni Hatƒ±rla</strong> se√ßeneƒüi se√ßiliyken ≈üifrelerinizi deƒüi≈ütiremezsiniz. ≈ûifrenizi deƒüi≈ütirmek i√ßin l√ºtfen sistemden √ßƒ±kƒ±p tekrar sisteme giri≈ü yapƒ±nƒ±z.

-

-# -- user form --

-user.address.address=Adres

-user.availableRoles=Se√ßilebilir G√∂revler

-user.address.city=≈ûehir

-user.address.country=√úlke

-user.email=E-Posta

-user.firstName=ƒ∞sim

-user.id=Id

-user.lastName=Ad

-user.password=≈ûifre

-user.confirmPassword=≈ûifrenizi Onaylayƒ±n

-user.phoneNumber=Telefon

-user.address.postalCode=Posta Kodu

-user.address.province=Eyalet

-user.roles=Mevcut G√∂revler

-user.username=Kullanƒ±cƒ± Adƒ±

-user.website=Web Sayfasƒ±

-user.visitWebsite=Ziyaret et

-user.passwordHint=≈ûifre ƒ∞pucu

-user.enabled=Aktive edildi.

-user.accountExpired=S√ºresi Doldu

-user.accountLocked=Kilitlendi

-user.credentialsExpired=≈ûifre S√ºresi Dolmu≈ü

-

-# -- user list page --

-userList.title=Kullanƒ±cƒ± Listesi

-userList.heading=Mevcut Kullanƒ±cƒ±lar

-userList.nousers=<span>Herhangi bir kullanƒ±cƒ± yok.</span>

-

-# -- user self-registration --

-signup.title=Kayƒ±t Ol

-signup.heading=Yeni Kullanƒ±cƒ± Kayƒ±tƒ±

-signup.message=L√ºtfen a≈ü≈üaƒüƒ±daki forma kullanƒ±cƒ± bilgilerinizi giriniz.

-signup.email.subject=AppFuse Kullanƒ±cƒ± Hesabƒ± Bilgisi

-signup.email.message=AppFuse eri≈üim i√ßin ba≈üarƒ±yla kayƒ±t oldunuz.  Kullanƒ±cƒ± adƒ± ve ≈üifre bilginiz a≈üaƒüƒ±dadƒ±r.

-

-# -- upload page messages --

-maxLengthExceeded=Y√ºklemeye √ßalƒ±≈ütƒ±ƒüƒ±nƒ±z dosyanƒ±n boyutu √ßok b√ºy√ºk.  Kabul edilen en b√ºy√ºk boyut 2 MB.

-upload.title=Dosya Y√ºkleme

-upload.heading=Dosya Y√ºkleyin

-upload.message=Y√ºklenebilir en b√ºy√ºk dosya boyutunun 2 MB olduƒüunu l√ºtfen hatƒ±rlayƒ±n.

-uploadForm.name=Temsili isim

-uploadForm.file=Y√ºklenecek Dosya

-

-# -- display page messages -- 

-display.title=Dosya Ba≈üarƒ±yla Y√ºklendi

-display.heading=Dosya Bilgisi

-

-# -- flushCache page --

-flushCache.title=√ñnbelleƒüi Temizle

-flushCache.heading=Temizleme Ba≈üarƒ±lƒ±!

-flushCache.message=B√ºt√ºn √∂nbellekler ba≈üarƒ±yla temizlendi, bir √∂nceki sayfanƒ±za 2 saniye i√ßinde d√∂n√ºl√ºyor.

-

-# -- clickstreams page --

-clickstreams.title=B√ºt√ºn Tƒ±klama ƒ∞zleri

-clickstreams.heading=B√ºt√ºn Tƒ±klama ƒ∞zleri

-

-# -- viewstream page --

-viewstream.title=Akƒ±≈ü Detaylarƒ±

-viewstream.heading=Akƒ±≈ü Bilgisi

-

-# -- active users page --

-activeUsers.title=Aktif Kullanƒ±cƒ±lar

-activeUsers.heading=Mevcut Kullanƒ±cƒ±lar

-activeUsers.message=A≈üaƒüƒ±daki liste sisteme giri≈ü yapmƒ±≈ü ve oturumu sonlanmamƒ±≈ü kullanƒ±cƒ±larƒ±n listesidir.

-activeUsers.fullName=Tam ƒ∞sim

-

-# JSF-only messages, remove if not using JSF

-javax.faces.component.UIInput.REQUIRED=Bu zorunlu bir alandƒ±r.

-activeUsers.summary={0} Kullanƒ±cƒ± bulundu,  {2} den {3} e , {1} kullanƒ±cƒ± g√∂steriliyor . Sayfa {4} / {5}

+Ôªø
+user.status=Oturum a√ßan kullanƒ±cƒ± :
+user.logout=√áƒ±kƒ±≈ü
+
+# -- validator errors --
+errors.invalid={0} ge√ßersiz.
+errors.maxlength={0}  {1} karakterden fazla olamaz.
+errors.minlength={0}  {1} karakterden az olamaz.
+errors.range={0}  {1} ve {2} aralƒ±ƒüƒ±nda deƒüil.
+errors.required={0} gerekli bir alan.
+errors.byte={0} byte tipinde olmalƒ±.
+errors.date={0} tarih tipinde deƒüil.
+errors.double={0} double tipinde olmalƒ±.
+errors.float={0} float tipinde olmalƒ±.
+errors.integer={0} bir rakam olmalƒ±.
+errors.long={0} long tipinde olmalƒ±.
+errors.short={0} short tipinde olmalƒ±.
+errors.creditcard={0} ge√ßerli bir kredi kartƒ± numarasƒ± deƒüil.
+errors.email={0} ge√ßersiz e-posta adresi.
+errors.phone={0} ge√ßersiz bir telefon numarasƒ±.
+errors.zip={0} ge√ßersiz posta kodu.
+
+# -- other errors --
+errors.cancel=ƒ∞≈ülem iptal edildi.
+errors.detail={0}
+errors.general=ƒ∞≈ülem tamamlanmadƒ±. Detaylar a≈üaƒüƒ±daki gibi olmalƒ±.
+errors.token=ƒ∞stek tamamlanamadƒ±. ƒ∞≈ülem y√ºr√ºrl√ºl√ºkte deƒüil.
+errors.none=Hata mesajƒ± bulunamadƒ±, server loglarƒ±na bakƒ±nƒ±z.
+errors.password.mismatch=Yanlƒ±≈ü kullanƒ±cƒ± adƒ± ve/veya ≈üifre, l√ºtfen tekrar deneyiniz.
+errors.conversion=Web deƒüerlerini veri deƒüerlerine √ßevirirken bir hata olu≈ütu.
+errors.twofields={0} alanƒ± {1} alanƒ± ile aynƒ± olmalƒ±.
+errors.existing.user=Bu kullanƒ±cƒ± adƒ± ({0}) veya e-posta adresi ({1}) sisteme kayƒ±tlƒ±dƒ±r.  L√ºtfen deƒüi≈üik bir kullanƒ±cƒ± adƒ± ile tekrar deneyiniz.
+
+# -- success messages --
+user.added= {0} i√ßin kullanƒ±cƒ± bilgisi ba≈üarƒ±yla eklendi.
+user.deleted={0}</strong> i√ßin kullanƒ±cƒ± profili ba≈üarƒ±yla silindi.
+user.registered=Uygulamaya eri≈üebilmek i√ßin ba≈üarƒ±yla kayƒ±t oldunuz.
+user.saved=Profiliniz ba≈üarƒ±yla kayƒ±t edildi.
+user.updated.byAdmin={0}</strong> i√ßin kullanƒ±cƒ± bilgisi g√ºncellendi.
+newuser.email.message={0} sizin i√ßin bir AppFuse hesabƒ± yarattƒ±.  Kullanƒ±cƒ± adƒ± ve ≈üifre bilginiz a≈üaƒüƒ±dadƒ±r.
+reload.succeeded=Se√ßeneklerin tekrar y√ºklenmesi ba≈üarƒ±yla ger√ßekle≈üti.
+
+# -- error page messages --
+errorPage.title=Bir hata olu≈ütu
+errorPage.heading=Opps!
+404.title=Sayfa bulunamadƒ±
+404.message=ƒ∞stediƒüiniz sayfa bulunamadƒ±.   <a href="{0}">Ana Sayfaya</a> d√∂nmeyi deneyebilirsiniz. Buradayken nasƒ±l bir g√ºzel resim sizi ne≈üelendirebilir ?
+403.title=Eri≈üim Engellendi
+403.message=Sahip olduƒüunuz yetki bu sayfayƒ± g√∂rmek i√ßin yeterli deƒüil.  Eri≈üebilmeniz gerektiƒüini d√º≈ü√ºn√ºyorsanƒ±z l√ºtfen ,sistem y√∂neticinizle g√∂r√º≈ü√ºn.  Bu arada , g√ºzel bir resmin sizi ne≈üelendirmesine ne dersiniz ?
+
+# -- login --
+login.title=Giri≈ü
+login.heading=Giri≈ü
+login.rememberMe=Beni hatƒ±rla
+login.signup=√úye deƒüil misiniz ? Bir kullanƒ±cƒ± hesabƒ± i√ßin <a href="{0}">Kayƒ±t Ol !</a> .
+login.passwordHint=≈ûifrenizi unuttunuz mu?   <a href="?" onmouseover="window.status='≈ûifre ipucunuzu e-posta adresinize yollayƒ±n'; return true" onmouseout="window.status=''; return true" title="\u00c5\ufffdifre ipucunuzu e-posta adresinize yollayƒ±n" onclick="passwordHint(); return false">≈ûifre ipucunuzu e-posta adresinize yollayƒ±n</a>.
+login.passwordHint.sent={0}</strong> i√ßin ≈üifre ipucu  {1}na yollandƒ±.
+login.passwordHint.error=Kullanƒ±cƒ± adƒ± {0} veri tabanƒ±nda bulunamadƒ±.
+
+# -- mainMenu --
+mainMenu.title=Ana Men√º
+mainMenu.heading=Ho≈ü Geldiniz!
+mainMenu.message=Tebrikler, sisteme ba≈üarƒ±lƒ± bir giri≈ü yaptƒ±nƒ±z!  Sisteme giri≈ü yaptƒ±nƒ±z, ≈üu se√ßeneklere sahipsiniz:
+mainMenu.activeUsers=Mevcut Aktif Kullanƒ±cƒ±lar
+
+# -- menu/link messages --
+menu.admin=Y√∂netim
+menu.admin.users=Kullanƒ±cƒ±larƒ± G√∂r
+menu.admin.reload=Se√ßenekleri Tekrar Y√ºkle
+
+menu.user=Bilgilerini G√ºncelle
+menu.selectFile=Dosya Y√ºkle
+menu.flushCache=√ñnbellek Temizleme
+menu.clickstream=Tƒ±klama ƒ∞zi
+
+# -- form labels --
+label.username=Kullanƒ±cƒ± Adƒ±
+label.password=≈ûifre
+
+# -- button labels --
+button.add=Ekle
+button.cancel=ƒ∞ptal
+button.copy=Kopyala
+button.delete=Sil
+button.done=Bitti
+button.edit=G√ºncelle
+button.register=Kayƒ±t Ol
+button.save=Kaydet
+button.search=Ara
+button.upload=Y√ºkle
+button.view=G√∂r√ºnt√º
+button.reset=Yeniden Ba≈ülat
+button.login=Giri≈ü Yap
+
+# -- general values --
+icon.information=Bilgi
+icon.information.img=/images/iconInformation.gif
+icon.email=E-Posta
+icon.email.img=/images/iconEmail.gif
+icon.warning=Uyarƒ±
+icon.warning.img=/images/iconWarning.gif
+date.format=dd/MM/yyyy
+
+# -- role form --
+roleForm.name=ƒ∞sim
+
+# -- user profile page --
+userProfile.title=Kullanƒ±cƒ± Ayarlarƒ±
+userProfile.heading=Kullanƒ±cƒ± Profili
+userProfile.message=L√ºtfen a≈üaƒüƒ±daki formu kullanarak kullanƒ±cƒ± bilgilerinizi g√ºncelleyiniz.
+userProfile.admin.message=Bu kullanƒ±cƒ±nƒ±n bilgilerini a≈üaƒüƒ±daki formu kullanarak g√ºncelleyebilirsiniz.
+userProfile.showMore=Daha Fazla Bilgi Edinin
+userProfile.accountSettings=Kullanƒ±cƒ± Hesabƒ± Ayarlarƒ±
+userProfile.assignRoles=G√∂rev Ata
+userProfile.cookieLogin=Beni Hatƒ±rla</strong> se√ßeneƒüi se√ßiliyken ≈üifrelerinizi deƒüi≈ütiremezsiniz. ≈ûifrenizi deƒüi≈ütirmek i√ßin l√ºtfen sistemden √ßƒ±kƒ±p tekrar sisteme giri≈ü yapƒ±nƒ±z.
+
+# -- user form --
+user.address.address=Adres
+user.availableRoles=Se√ßilebilir G√∂revler
+user.address.city=≈ûehir
+user.address.country=√úlke
+user.email=E-Posta
+user.firstName=ƒ∞sim
+user.id=Id
+user.lastName=Ad
+user.password=≈ûifre
+user.confirmPassword=≈ûifrenizi Onaylayƒ±n
+user.phoneNumber=Telefon
+user.address.postalCode=Posta Kodu
+user.address.province=Eyalet
+user.roles=Mevcut G√∂revler
+user.username=Kullanƒ±cƒ± Adƒ±
+user.website=Web Sayfasƒ±
+user.visitWebsite=Ziyaret et
+user.passwordHint=≈ûifre ƒ∞pucu
+user.enabled=Aktive edildi.
+user.accountExpired=S√ºresi Doldu
+user.accountLocked=Kilitlendi
+user.credentialsExpired=≈ûifre S√ºresi Dolmu≈ü
+
+# -- user list page --
+userList.title=Kullanƒ±cƒ± Listesi
+userList.heading=Mevcut Kullanƒ±cƒ±lar
+userList.nousers=<span>Herhangi bir kullanƒ±cƒ± yok.</span>
+
+# -- user self-registration --
+signup.title=Kayƒ±t Ol
+signup.heading=Yeni Kullanƒ±cƒ± Kayƒ±tƒ±
+signup.message=L√ºtfen a≈ü≈üaƒüƒ±daki forma kullanƒ±cƒ± bilgilerinizi giriniz.
+signup.email.subject=AppFuse Kullanƒ±cƒ± Hesabƒ± Bilgisi
+signup.email.message=AppFuse eri≈üim i√ßin ba≈üarƒ±yla kayƒ±t oldunuz.  Kullanƒ±cƒ± adƒ± ve ≈üifre bilginiz a≈üaƒüƒ±dadƒ±r.
+
+# -- upload page messages --
+maxLengthExceeded=Y√ºklemeye √ßalƒ±≈ütƒ±ƒüƒ±nƒ±z dosyanƒ±n boyutu √ßok b√ºy√ºk.  Kabul edilen en b√ºy√ºk boyut 2 MB.
+upload.title=Dosya Y√ºkleme
+upload.heading=Dosya Y√ºkleyin
+upload.message=Y√ºklenebilir en b√ºy√ºk dosya boyutunun 2 MB olduƒüunu l√ºtfen hatƒ±rlayƒ±n.
+uploadForm.name=Temsili isim
+uploadForm.file=Y√ºklenecek Dosya
+
+# -- display page messages -- 
+display.title=Dosya Ba≈üarƒ±yla Y√ºklendi
+display.heading=Dosya Bilgisi
+
+# -- flushCache page --
+flushCache.title=√ñnbelleƒüi Temizle
+flushCache.heading=Temizleme Ba≈üarƒ±lƒ±!
+flushCache.message=B√ºt√ºn √∂nbellekler ba≈üarƒ±yla temizlendi, bir √∂nceki sayfanƒ±za 2 saniye i√ßinde d√∂n√ºl√ºyor.
+
+# -- clickstreams page --
+clickstreams.title=B√ºt√ºn Tƒ±klama ƒ∞zleri
+clickstreams.heading=B√ºt√ºn Tƒ±klama ƒ∞zleri
+
+# -- viewstream page --
+viewstream.title=Akƒ±≈ü Detaylarƒ±
+viewstream.heading=Akƒ±≈ü Bilgisi
+
+# -- active users page --
+activeUsers.title=Aktif Kullanƒ±cƒ±lar
+activeUsers.heading=Mevcut Kullanƒ±cƒ±lar
+activeUsers.message=A≈üaƒüƒ±daki liste sisteme giri≈ü yapmƒ±≈ü ve oturumu sonlanmamƒ±≈ü kullanƒ±cƒ±larƒ±n listesidir.
+activeUsers.fullName=Tam ƒ∞sim
+
+# JSF-only messages, remove if not using JSF
+javax.faces.component.UIInput.REQUIRED=Bu zorunlu bir alandƒ±r.
+activeUsers.summary={0} Kullanƒ±cƒ± bulundu,  {2} den {3} e , {1} kullanƒ±cƒ± g√∂steriliyor . Sayfa {4} / {5}
Index: src/main/resources/ApplicationResources_de.properties
===================================================================
--- src/main/resources/ApplicationResources_de.properties	(revision 85)
+++ src/main/resources/ApplicationResources_de.properties	(working copy)
@@ -3,12 +3,12 @@
 
 # -- validator errors --
 errors.invalid={0} ist ung¸ltig.
-errors.maxlength={0} muss mindestens {1} Zeichen lang sein.
-errors.minlength={0} darf maximal {1} Zeichen lang sein.
+errors.maxlength={0} darf maximal {1} Zeichen lang sein.
+errors.minlength={0} muss mindestens {1} Zeichen lang sein.
 errors.range={0} ist nicht im Bereich zwischen {1} und {2}.
 errors.required={0} ist ein Pflichtfeld.
 errors.byte={0} muss ein Bytewert sein.
-errors.date={0} ist kein Datumswert.
+errors.date={0} ist kein g¸ltiges Datum.
 errors.double={0} muss ein Wert vom Typ 'double' sein.
 errors.float={0} muss ein Wert vom Typ 'float' sein.
 errors.integer={0} muss eine Zahl sein.
@@ -22,53 +22,53 @@
 # -- other errors --
 errors.cancel=Operation abgebrochen.
 errors.detail={0}
-errors.general=<strong>Der Prozess konnte nicht abgeschlossen werden. Detaillierte Angaben sollten nachfolgend angezeigt werden.</strong>
-errors.token=Anfrage konnte nicht abgeschlossen werden. Die Reihenfolge der Operationen ist nicht korrekt.
-errors.none=Es konnte keine Fehlermeldung gefunden werden, ¸berpr¸fen sie bitte die Log-Dateien ihres Servers.
-errors.password.mismatch=Ung¸ltiger Benutzername und/oder Passwort, bitte versuchen sie es nochmals.
-errors.browser.warning=<strong>Hinweis:</strong> Der Inhalt dieser Webpr‰senz kann von jedem Browser in allen Versionen abgerufen werden. Der von ihnen benutzte Browser unterst¸tzt jedoch mˆglicherweise grundlegende WWW-Standards nicht, so dass sie eventuell das detaillierte Design unserer Webseite nicht korrekt angezeigt bekommen. Wir unterst¸tzen die <a href="http://www.webstandards.org/upgrade/">Kampagne</a> des Web Standards Projekt, welche die Verbreitung und den Wechsel zu neueren Browserversionen zum Ziel hat.
+errors.general=Der Prozess konnte nicht abgeschlossen werden. Detaillierte Angaben sollten nachfolgend angezeigt werden.
+errors.token=Die Anfrage konnte nicht abgeschlossen werden. Die Reihenfolge der Operationen ist nicht korrekt.
+errors.none=Es konnte keine Fehlermeldung gefunden werden, ¸berpr¸fen Sie bitte die Log-Dateien Ihres Servers.
+errors.password.mismatch=Ung¸ltiger Benutzername und/oder Passwort, bitte versuchen Sie es nochmal.
+errors.browser.warning=Hinweis:</strong> Der Inhalt dieser Webpr‰senz kann von jedem Browser in allen Versionen abgerufen werden. Der von Ihnen benutzte Browser unterst¸tzt jedoch mˆglicherweise grundlegende WWW-Standards nicht, so dass Sie das detaillierte Design unserer Webseite eventuell nicht korrekt angezeigt bekommen. Wir unterst¸tzen die <a href="http://www.webstandards.org/upgrade/">Kampagne</a> des Web Standards Projekt, welche die Verbreitung und den Wechsel zu neueren Browserversionen zum Ziel hat.
 errors.conversion=Bei der Konvertierung von Webwerten zu Datenwerten ist ein Fehler aufgetreten.
 errors.twofields=Das Feld {0} muss denselben Wert wie das Feld {1} aufweisen.
-errors.existing.user=Diese Benutzername ({0}) oder diese E-Mail Adresse ({1}) existiert bereits.  Bitte versuchen sie es mit einem anderen Benutzernamen.
+errors.existing.user=Diese Benutzername ({0}) oder diese E-Mail Adresse ({1}) existiert bereits. Bitte versuchen Sie es mit einem anderen Benutzernamen.
 
 # -- success messages --
-user.added=Informationen f¸r Benutzer <strong>{0}</strong> wurden erfolgreich hinzugef¸gt.
-user.deleted=Benutzerprofil f¸r <strong>{0}</strong> wurde erfolgreich gelˆscht. 
+user.added=Die Informationen f¸r Benutzer {0} wurden erfolgreich hinzugef¸gt.
+user.deleted=Das Benutzerprofil f¸r {0} wurde erfolgreich gelˆscht. 
 user.registered=Sie haben sich erfolgreich registriert.
 user.saved=Ihr Profil wurde erfolgreich aktualisiert.
-user.updated.byAdmin=Die Informationen f¸r Benutzer <strong>{0}</strong> wurden erfolgreich aktualisiert.
-newuser.email.message={0} hat ein Konto bei AppFuse f¸r sie angelegt. Informationen zu ihrem Benutzernamen und ihrem Passwort finden sie nachfolgend.
+user.updated.byAdmin=Die Informationen f¸r Benutzer {0} wurden erfolgreich aktualisiert.
+newuser.email.message={0} hat ein Konto bei AppFuse f¸r Sie angelegt. Informationen zu ihrem Benutzernamen und Ihrem Passwort finden Sie nachfolgend.
 reload.succeeded=Das erneute Laden der Optionen wurde erfolgreich abgeschlossen.
 
 # -- error page messages --
 errorPage.title=Ein Fehler ist aufgetreten
 errorPage.heading=Sapperlott!
-404.title=Seite konnte nicht gefunden werden
-404.message=Die von ihnen angeforderte Seite konnte nicht gefunden werden. Sie kˆnnen versuchen wieder zum <a href="{0}">Hauptmen¸</a> zur¸ckzukehren. Wenn sie schon hier gelandet sind, wie w‰r's mit einem h¸bschen Bild zur Aufmunterung?
+404.title=Die Seite konnte nicht gefunden werden
+404.message=Die von Ihnen angeforderte Seite konnte nicht gefunden werden. Sie kˆnnen versuchen wieder zum <a href="{0}">Hauptmen¸</a> zur¸ckzukehren. Wenn sie schon hier gelandet sind, wie w‰r&#39;s mit einem h¸bschen Bild zur Aufmunterung?
 403.title=Zugang nicht gestattet
-403.message=Ihre derzeitiger Benutzerstatus erlaubt es nicht, diese Seite anzuzeigen.  Bitte nehmen sie Kontakt mit ihrem Systemadministrator auf falls sie glauben, dass ihnen der Zugang gestattet sein sollte. Wie w‰r's zwischenzeitlich mit einem h¸bschen Bild zur Aufmunterung?
+403.message=Ihre derzeitiger Benutzerstatus erlaubt es nicht, diese Seite anzuzeigen.  Bitte nehmen Sie Kontakt mit ihrem Systemadministrator auf falls Sie glauben, dass Ihnen der Zugang gestattet sein sollte. Wie w‰r&#39;s zwischenzeitlich mit einem h¸bschen Bild zur Aufmunterung?
 
 # -- login --
 login.title=Anmeldung
 login.heading=Anmeldung
 login.rememberMe=Daten behalten
 login.signup=Kein Mitglied? <a href="{0}">Anmeldung</a> f¸r ein Benutzerkonto.
-login.passwordHint=Haben sie ihr Passwort vergessen?  Lassen sie sich per E-Mail einen <a href="?" onmouseover="window.status='Lassen sie sich einen Hinweis auf ihr Passwort zusenden.'; return true" onmouseout="window.status=''; return true" title="Lassen sie sich einen Hinweis auf ihr Passwort zusenden." onclick="passwordHint(); return false">Hinweis auf ihr Passwort</a> zusenden.
-login.passwordHint.sent=Ein Passwordhinweis f¸r <strong>{0}</strong> wurde an <strong>{1}</strong> gesendet.
-login.passwordHint.error=Der Benutzername <strong>{0}</strong> konnte nicht in der Datenbank gefunden werden.
+login.passwordHint=Haben Sie ihr Passwort vergessen?  Lassen Sie sich per E-Mail einen <a href="?" onmouseover="window.status='Lassen Sie sich einen Hinweis auf Ihr Passwort zusenden.'; return true" onmouseout="window.status=''; return true" title="Lassen Sie sich einen Hinweis auf Ihr Passwort zusenden." onclick="passwordHint(); return false">Hinweis auf Ihr Passwort</a> zusenden.
+login.passwordHint.sent=Ein Passwordhinweis f¸r {0} wurde an {1} gesendet.
+login.passwordHint.error=Der Benutzername {0} konnte nicht in der Datenbank gefunden werden.
 
 # -- mainMenu --
 mainMenu.title=Hauptmen¸
 mainMenu.heading=Willkommen!
-mainMenu.message=Gratulation, sie haben sich erfolgreich angemeldet!  Als angemeldeter Benutzer haben sie folgende Mˆglichkeiten:
+mainMenu.message=Gratulation, Sie haben sich erfolgreich angemeldet!  Als angemeldeter Benutzer haben Sie folgende Mˆglichkeiten:
 mainMenu.activeUsers=Derzeitige Benutzer
 
 # -- menu/link messages --
 menu.admin=Administration
 menu.admin.users=Zeige Benutzer an
-menu.admin.reload=Optionen f¸r erneutes Laden
+menu.admin.reload=Optionen neu laden
 
-menu.user=Benutzerprofil bearbeiten
+menu.user=Profil
 menu.selectFile=Datei hochladen
 menu.flushCache=Cache leeren
 menu.clickstream=Clickstream
@@ -82,7 +82,7 @@
 button.cancel=Abbrechen
 button.copy=Kopieren
 button.delete=Lˆschen
-button.done=Getan
+button.done=Fertig
 button.edit=Bearbeiten
 button.register=Registrieren
 button.save=Speichern
@@ -107,11 +107,11 @@
 # -- user profile page --
 userProfile.title=Benutzereinstellungen
 userProfile.heading=Benutzerprofil
-userProfile.message=Bitte aktualisieren sie ihre Daten im nachfolgenden Formular.
-userProfile.admin.message=Sie kˆnnen die Daten dieses Benutzers im nachfolgenden Formular aktualisierenˆnnen die Daten dieses Benutzers im nachfolgenden Formular aktualisieren.
+userProfile.message=Bitte aktualisieren Sie Ihre Daten im nachfolgenden Formular.
+userProfile.admin.message=Sie kˆnnen die Daten dieses Benutzers im nachfolgenden Formular aktualisieren.
 userProfile.showMore=Weitere Informationen
 userProfile.assignRoles=Benutzerstatus zuweisen
-userProfile.cookieLogin= Sie kˆnnen ihr Passwort nicht ‰ndern, wenn sie bei der Anmeldung die Option <strong>Daten behalten</strong> ausgew‰hlt haben.  Bitte melden sie sich zun‰chst ab und dann erneut an, um ihr Passwort ‰ndern zu kˆnnen.
+userProfile.cookieLogin= Sie kˆnnen Ihr Passwort nicht ‰ndern, wenn Sie bei der Anmeldung die Option <strong>Daten behalten</strong> ausgew‰hlt haben.  Bitte melden Sie sich zun‰chst ab und dann erneut an, um ihr Passwort ‰ndern zu kˆnnen.
 
 # -- user form --
 user.addressForm.address=Adresse
@@ -131,7 +131,7 @@
 user.username=Benutzername
 user.website=Website
 user.visitWebsite=Besuchen
-user.passwordHint=Hinweis auf Passwort
+user.passwordHint=Passworthinweis
 user.enabled=Freigeschaltet
 
 # -- user list page --
@@ -142,20 +142,20 @@
 # -- user self-registration --
 signup.title=Anmeldung
 signup.heading=Registrierung als neuer Benutzer
-signup.message=Bitte geben sie ihre Benutzerdaten in das nachfolgende Formular ein.
-signup.email.subject= Details zu ihrem AppFuse Benutzerkonto
-signup.email.message=Sie wurden erfolgreich f¸r den Zugang zu AppFuse registriert. Angaben zu ihrem Benutzernamen und ihrem Passwort finden sie nachfolgend.
+signup.message=Bitte geben Sie Ihre Benutzerdaten in das nachfolgende Formular ein.
+signup.email.subject= Details zu Ihrem AppFuse Benutzerkonto
+signup.email.message=Sie wurden erfolgreich f¸r den Zugang zu AppFuse registriert. Angaben zu Ihrem Benutzernamen und Ihrem Passwort finden Sie nachfolgend.
 
 # -- upload page messages --
-maxLengthExceeded=Die Datei, welche sie hochladen mˆchten, ist zu groﬂ. Die Maximalgrˆﬂe einer Datei zum Hochladen betr‰gt 2 MB.
+maxLengthExceeded=Die Datei, welche Sie hochladen mˆchten, ist zu groﬂ. Die Maximalgrˆﬂe einer Datei zum Hochladen betr‰gt 2 MB.
 upload.title=Hochladen von Dateien
-upload.heading=Laden sie eine Datei hoch
-upload.message=Bitte beachten sie, dass Maximalgrˆﬂe einer Datei zum Hochladen innerhalb dieser Anwendung 2 MB betr‰gt.
+upload.heading=Laden Sie eine Datei hoch
+upload.message=Bitte beachten Sie, dass die Maximalgrˆﬂe einer Datei zum Hochladen innerhalb dieser Anwendung 2 MB betr‰gt.
 uploadForm.name=H¸bscher Name
 uploadForm.file=Hochzuladende Datei
 
 # -- display page messages -- 
-display.title=Datei wurde erfolgreich hochgeladen!
+display.title= Die Datei wurde erfolgreich hochgeladen!
 display.heading=Dateiinformation
 
 # -- flushCache page --
Index: src/main/resources/ApplicationResources_zh_TW.properties
===================================================================
--- src/main/resources/ApplicationResources_zh_TW.properties	(revision 85)
+++ src/main/resources/ApplicationResources_zh_TW.properties	(working copy)
@@ -1,5 +1,4 @@
-Ôªø## Do NOT delete! Keep this line to avoid the native2ascii UTF-8 BOM bug. See #APF-639

-

+Ôªø

 user.status=ÁõÆÂâçÁî®Êà∂:

 user.logout=ÁôªÂá∫

 

@@ -24,7 +23,7 @@
 # -- other errors --

 errors.cancel=Êìç‰ΩúË¢´ÂèñÊ∂à„ÄÇ

 errors.detail={0}

-errors.general=<strong>Êìç‰ΩúÊú™ÂÆåÊàê„ÄÇË©≥Á¥∞ÂéüÂõ†Â¶Ç‰∏ã„ÄÇ</strong>

+errors.general=Êìç‰ΩúÊú™ÂÆåÊàê„ÄÇË©≥Á¥∞ÂéüÂõ†Â¶Ç‰∏ã„ÄÇ

 errors.token=Ë´ãÊ±ÇÊú™ÂÆåÂÖ®ËôïÁêÜ„ÄÇÊìç‰ΩúÈ†ÜÂ∫èÈåØË™§„ÄÇ

 errors.none=ÁÑ°ÈåØË™§Ê∂àÊÅØÔºåË´ãÊ™¢Êü•‰º∫ÊúçÂô®Êó•Ë™åÊ™î„ÄÇ

 errors.password.mismatch=ÁÑ°ÊïàÁî®Êà∂ÂêçÊàñÂØÜÁ¢ºÔºåË´ãÈáçË©¶„ÄÇ

@@ -33,11 +32,11 @@
 errors.existing.user=Áî®Êà∂Âêç ({0}) Êàñe-mailÂú∞ÂùÄ ({1}) Â∑≤Â≠òÂú®„ÄÇË´ãÂÜçÊ¨°ÂòóË©¶‰∏çÂêåÂêçÁ®±„ÄÇ

 

 # -- success messages --

-user.added=Áî®Êà∂ <strong>{0}</strong> ÁöÑË≥áË®äÊñ∞Â¢ûÊàêÂäü„ÄÇ

-user.deleted=Áî®Êà∂ <strong>{0}</strong> ÁöÑË≥áË®äÂà™Èô§ÊàêÂäü„ÄÇ

+user.added=Áî®Êà∂ {0} ÁöÑË≥áË®äÊñ∞Â¢ûÊàêÂäü„ÄÇ

+user.deleted=Áî®Êà∂ {0} ÁöÑË≥áË®äÂà™Èô§ÊàêÂäü„ÄÇ

 user.registered=Ë®ªÂÜäÊàêÂäüÔºåÊÇ®ÂèØ‰ª•ÈñãÂßã‰ΩøÁî®Á≥ªÁµ±„ÄÇ

 user.saved=ÊÇ®ÁöÑË≥áË®äÂ∑≤ÊàêÂäüÊõ¥Êñ∞„ÄÇ

-user.updated.byAdmin=Áî®Êà∂ <strong>{0}</strong> ÁöÑË≥áË®äÂ∑≤ÊàêÂäüÊõ¥Êñ∞„ÄÇ

+user.updated.byAdmin=Áî®Êà∂ {0} ÁöÑË≥áË®äÂ∑≤ÊàêÂäüÊõ¥Êñ∞„ÄÇ

 newuser.email.message = {0} ÁÇ∫ÊÇ®ÊàêÂäüÂâµÂª∫‰∫Ü‰∏ÄÂÄãAppFuseÂ∏≥Ëôü„ÄÇÊÇ®ÁöÑÁî®Êà∂ÂêçÂíåÂØÜÁ¢ºË≥áË®äÂ¶Ç‰∏ãÔºö

 reload.succeeded=Â∑≤Á∂ìÊàêÂäüÈáçËºâ.

 

@@ -55,8 +54,8 @@
 login.rememberMe=ËÆìÁ≥ªÁµ±Ë®ò‰ΩèÊàë

 login.signup=‰∏çÊòØË®ªÂÜäÁî®Êà∂? <a href="{0}">Áî≥Ë´ã</a> ‰∏ÄÂÄãÂ∏≥Ëôü„ÄÇ

 login.passwordHint=ÂøòË®ò‰∫ÜÂØÜÁ¢º?  ËÆìÁ≥ªÁµ±Â∞á <a href="?" onmouseover="window.status='Á≥ªÁµ±ÁôºÈÄÅÂØÜÁ¢ºÊèêÁ§∫„ÄÇ'; return true" onmouseout="window.status=''; return true" title="Á≥ªÁµ±ÁôºÈÄÅÂØÜÁ¢ºÊèêÁ§∫„ÄÇ" onclick="passwordHint(); return false">ÂØÜÁ¢ºÊèêÁ§∫Ë≥áË®äÂ∑≤e-mailÂΩ¢ÂºèÁôºÈÄÅÁµ¶ÊÇ®</a>„ÄÇ

-login.passwordHint.sent=<strong>{0}</strong> ÁöÑÂØÜÁ¢ºÊèêÁ§∫Â∑≤ÊàêÂäüÁôºÈÄÅÂà∞ <strong>{1}</strong>„ÄÇ

-login.passwordHint.error=Áî®Êà∂Âêç <strong>{0}</strong> Âú®Á≥ªÁµ±Ë≥áÊñôÂ∫´‰∏≠Êú™ÊâæÂà∞„ÄÇ

+login.passwordHint.sent={0}</strong> ÁöÑÂØÜÁ¢ºÊèêÁ§∫Â∑≤ÊàêÂäüÁôºÈÄÅÂà∞ {1}„ÄÇ

+login.passwordHint.error=Áî®Êà∂Âêç {0} Âú®Á≥ªÁµ±Ë≥áÊñôÂ∫´‰∏≠Êú™ÊâæÂà∞„ÄÇ

 

 # -- mainMenu --

 mainMenu.title=‰∏ªÈÅ∏ÂñÆ

Index: src/main/resources/ApplicationResources_zh_CN.properties
===================================================================
--- src/main/resources/ApplicationResources_zh_CN.properties	(revision 85)
+++ src/main/resources/ApplicationResources_zh_CN.properties	(working copy)
@@ -1,5 +1,4 @@
-Ôªø## Do NOT delete! Keep this line to avoid the native2ascii UTF-8 BOM bug. See #APF-639
-
+Ôªø
 user.status=ÂΩìÂâçÁî®Êà∑: 
 user.logout=ÈÄÄÂá∫
 
@@ -24,7 +23,7 @@
 # -- other errors --
 errors.cancel=Êìç‰ΩúË¢´ÂèñÊ∂à„ÄÇ
 errors.detail={0}
-errors.general=<strong>Êìç‰ΩúÊú™ÂÆåÊàê„ÄÇËØ¶ÁªÜÂéüÂõ†Â¶Ç‰∏ã„ÄÇ</strong>
+errors.general=Êìç‰ΩúÊú™ÂÆåÊàê„ÄÇËØ¶ÁªÜÂéüÂõ†Â¶Ç‰∏ã„ÄÇ
 errors.token=ËØ∑Ê±ÇÊú™ÂÆåÂÖ®Â§ÑÁêÜ„ÄÇÊìç‰ΩúÈ°∫Â∫èÈîôËØØ„ÄÇ
 errors.none=Êó†ÈîôËØØÊ∂àÊÅØÔºåËØ∑Ê£ÄÊü•ÊúçÂä°Âô®Êó•ÂøóÊñá‰ª∂„ÄÇ
 errors.password.mismatch=Êó†ÊïàÁî®Êà∑ÂêçÊàñÂØÜÁ†ÅÔºåËØ∑ÈáçËØï„ÄÇ
@@ -33,11 +32,11 @@
 errors.existing.user=Áî®Êà∑Âêç ({0}) Êàñe-mailÂú∞ÂùÄ ({1}) Â∑≤Â≠òÂú®„ÄÇËØ∑ÂÜçÊ¨°Â∞ùËØï‰∏çÂêåÂêçÁß∞„ÄÇ
 
 # -- success messages --
-user.added=Áî®Êà∑ <strong>{0}</strong> ÁöÑ‰ø°ÊÅØÊ∑ªÂä†ÊàêÂäü„ÄÇ
-user.deleted=Áî®Êà∑ <strong>{0}</strong> ÁöÑ‰ø°ÊÅØÂà†Èô§ÊàêÂäü„ÄÇ 
+user.added=Áî®Êà∑ {0} ÁöÑ‰ø°ÊÅØÊ∑ªÂä†ÊàêÂäü„ÄÇ
+user.deleted=Áî®Êà∑ {0} ÁöÑ‰ø°ÊÅØÂà†Èô§ÊàêÂäü„ÄÇ
 user.registered=Ê≥®ÂÜåÊàêÂäüÔºåÊÇ®ÂèØ‰ª•ÂºÄÂßã‰ΩøÁî®Á≥ªÁªü„ÄÇ
 user.saved=ÊÇ®ÁöÑ‰ø°ÊÅØÂ∑≤ÊàêÂäüÊõ¥Êñ∞„ÄÇ
-user.updated.byAdmin=Áî®Êà∑ <strong>{0}</strong> ÁöÑ‰ø°ÊÅØÂ∑≤ÊàêÂäüÊõ¥Êñ∞„ÄÇ
+user.updated.byAdmin=Áî®Êà∑ {0} ÁöÑ‰ø°ÊÅØÂ∑≤ÊàêÂäüÊõ¥Êñ∞„ÄÇ
 newuser.email.message={0} ‰∏∫ÊÇ®ÊàêÂäüÂàõÂª∫‰∫Ü‰∏Ä‰∏™AppFuseÂ∏êÂè∑„ÄÇÊÇ®ÁöÑÁî®Êà∑ÂêçÂíåÂØÜÁ†Å‰ø°ÊÅØÂ¶Ç‰∏ãÔºö
 reload.succeeded=Â∑≤ÁªèÊàêÂäüÈáçËΩΩ.
 
@@ -55,8 +54,8 @@
 login.rememberMe=ËÆ©Á≥ªÁªüËÆ∞‰ΩèÊàë
 login.signup=‰∏çÊòØÊ≥®ÂÜåÁî®Êà∑? <a href="{0}">Áî≥ËØ∑</a> ‰∏Ä‰∏™Â∏êÂè∑„ÄÇ
 login.passwordHint=ÂøòËÆ∞‰∫ÜÂØÜÁ†Å?  ËÆ©Á≥ªÁªüÂ∞Ü <a href="?" onmouseover="window.status='Á≥ªÁªüÂèëÈÄÅÂØÜÁ†ÅÊèêÁ§∫„ÄÇ'; return true" onmouseout="window.status=''; return true" title="Á≥ªÁªüÂèëÈÄÅÂØÜÁ†ÅÊèêÁ§∫„ÄÇ" onclick="passwordHint(); return false">ÂØÜÁ†ÅÊèêÁ§∫‰ø°ÊÅØÂ∑≤e-mailÂΩ¢ÂºèÂèëÈÄÅÁªôÊÇ®</a>„ÄÇ
-login.passwordHint.sent=<strong>{0}</strong> ÁöÑÂØÜÁ†ÅÊèêÁ§∫Â∑≤ÊàêÂäüÂèëÈÄÅÂà∞ <strong>{1}</strong>„ÄÇ
-login.passwordHint.error=Áî®Êà∑Âêç <strong>{0}</strong> Âú®Á≥ªÁªüÊï∞ÊçÆÂ∫ì‰∏≠Êú™ÊâæÂà∞„ÄÇ
+login.passwordHint.sent={0}</strong> ÁöÑÂØÜÁ†ÅÊèêÁ§∫Â∑≤ÊàêÂäüÂèëÈÄÅÂà∞ {1}„ÄÇ
+login.passwordHint.error=Áî®Êà∑Âêç {0} Âú®Á≥ªÁªüÊï∞ÊçÆÂ∫ì‰∏≠Êú™ÊâæÂà∞„ÄÇ
 
 # -- mainMenu --
 mainMenu.title=‰∏ªËèúÂçï
Index: src/main/webapp/WEB-INF/urlrewrite.xml
===================================================================
--- src/main/webapp/WEB-INF/urlrewrite.xml	(revision 85)
+++ src/main/webapp/WEB-INF/urlrewrite.xml	(working copy)
@@ -1,9 +1,11 @@
-<?xml version="1.0" encoding="utf-8"?>
+<?xml version="1.0" encoding="UTF-8"?>
+<!DOCTYPE urlrewrite PUBLIC "-//tuckey.org//DTD UrlRewrite 3.0//EN"
+    "http://tuckey.org/res/dtds/urlrewrite3.0.dtd">
 
 <urlrewrite>
     <rule>
-        <from>^/user/(.*)\.html$</from>
-        <to type="forward">/userform.html?username=$1</to>
+        <from>^/admin/user/(.*)\.html$</from>
+        <to type="forward">/admin/userform.html?id=$1&amp;from=list</to>
     </rule>
 </urlrewrite>
 
Index: src/main/webapp/WEB-INF/menu-config.xml
===================================================================
--- src/main/webapp/WEB-INF/menu-config.xml	(revision 85)
+++ src/main/webapp/WEB-INF/menu-config.xml	(working copy)
@@ -8,12 +8,12 @@
         <Menu name="UserMenu" title="menu.user" description="User Menu" page="/userform.html" roles="ROLE_ADMIN,ROLE_USER"/>
         <Menu name="PeopleMenu" title="menu.viewPeople" page="/persons.html"/>
         <Menu name="AdminMenu" title="menu.admin" description="Admin Menu" roles="ROLE_ADMIN" width="120" page="/users.html">
-            <Item name="ViewUsers" title="menu.admin.users" page="/users.html"/>
-            <Item name="ActiveUsers" title="mainMenu.activeUsers" page="/activeUsers.html"/>
-            <Item name="ReloadContext" title="menu.admin.reload" page="/reload.html"/>
+            <Item name="ViewUsers" title="menu.admin.users" page="/admin/users.html"/>
+            <Item name="ActiveUsers" title="mainMenu.activeUsers" page="/admin/activeUsers.html"/>
+            <Item name="ReloadContext" title="menu.admin.reload" page="/admin/reload.html"/>
             <Item name="FileUpload" title="menu.selectFile" page="/fileupload.html"/>
-            <Item name="FlushCache" title="menu.flushCache" page="/flushCache.html"/>
-            <Item name="Clickstream" title="menu.clickstream" page="/clickstreams.jsp"/>
+            <Item name="FlushCache" title="menu.flushCache" page="/admin/flushCache.html"/>
+            <Item name="Clickstream" title="menu.clickstream" page="/admin/clickstreams.jsp"/>
         </Menu>
         <Menu name="Logout" title="user.logout" page="/logout.jsp" roles="ROLE_ADMIN,ROLE_USER"/>
     </Menus>
Index: src/main/webapp/WEB-INF/dispatcher-servlet.xml
===================================================================
--- src/main/webapp/WEB-INF/dispatcher-servlet.xml	(revision 85)
+++ src/main/webapp/WEB-INF/dispatcher-servlet.xml	(working copy)
@@ -80,17 +80,19 @@
     <bean id="urlMapping" class="org.springframework.web.servlet.handler.SimpleUrlHandlerMapping">

         <property name="mappings">

             <value>

-                /activeUsers.html=filenameController

-                /flushCache.html=filenameController

+                /admin/activeUsers.html=filenameController

+                /admin/flushCache.html=filenameController

+                /admin/reload.html=reloadController

+                /admin/users.html=userController

                 /mainMenu.html=filenameController

                 /passwordHint.html=passwordHintController

             </value>

         </property>

-        <property name="order" value="1"/>

+        <property name="order" value="0"/>

     </bean>

 

     <bean class="org.springframework.web.servlet.mvc.support.ControllerClassNameHandlerMapping">

-        <property name="order" value="0"/>

+        <property name="order" value="1"/>

     </bean>

 

     <!-- View Resolver for JSPs -->

Index: src/main/webapp/WEB-INF/validation.xml
===================================================================
--- src/main/webapp/WEB-INF/validation.xml	(revision 85)
+++ src/main/webapp/WEB-INF/validation.xml	(working copy)
@@ -1,24 +1,22 @@
 <?xml version="1.0" encoding="UTF-8" ?>
-<!DOCTYPE form-validation PUBLIC
-    "-//Apache Software Foundation//DTD Commons Validator Rules Configuration 1.1//EN"
-    "http://jakarta.apache.org/commons/dtds/validator_1_1.dtd">
+<!DOCTYPE form-validation PUBLIC "-//Apache Software Foundation//DTD Commons Validator Rules Configuration 1.1//EN" "http://jakarta.apache.org/commons/dtds/validator_1_1.dtd">
 
 <form-validation>
-    <global>
-        <constant>
-            <constant-name>phone</constant-name>
-            <constant-value>^\(?(\d{3})\)?[-| ]?(\d{3})[-| ]?(\d{4})$</constant-value>
-        </constant>
-        <constant>
-            <constant-name>zip</constant-name>
-            <constant-value>^\d{5}\d*$</constant-value>
-        </constant>
-        <constant>
-            <constant-name>currency</constant-name>
-            <constant-value>^\d{1,3}(,?\d{1,3})*\.?(\d{1,2})?$</constant-value>
-        </constant>
-    </global>
-    <formset>
+     <global>
+      <constant>
+        <constant-name>phone</constant-name>
+        <constant-value>^\(?(\d{3})\)?[-| ]?(\d{3})[-| ]?(\d{4})$</constant-value>
+      </constant>
+      <constant>
+        <constant-name>zip</constant-name>
+        <constant-value>^\d{5}\d*$</constant-value>
+      </constant>
+      <constant>
+        <constant-name>currency</constant-name>
+        <constant-value>^\d{1,3}(,?\d{1,3})*\.?(\d{1,2})?$</constant-value>
+      </constant> 
+   </global>
+   <formset>
         <form name="fileUpload">
             <field property="name" depends="required">
                 <arg0 key="uploadForm.name"/>
@@ -30,126 +28,126 @@
         </form>
     </formset>
 
-    <formset>
-        <!--
-          Define form validation config in validation-forms.xml
-        -->
+  <formset>
+  <!--
+    Define form validation config in validation-forms.xml
+  -->
 
-        <form name="address">
-            <field property="city"
-                   depends="required">
+      <form name="address">
+              <field property="city"
+                     depends="required">
 
-                <arg0 key="address.city"/>
-            </field>
-            <field property="country"
-                   depends="required">
+                  <arg0 key="address.city"/>
+              </field>
+              <field property="country"
+                     depends="required">
 
-                <arg0 key="address.country"/>
-            </field>
-            <field property="postalCode"
-                   depends="required,mask">
-                <msg
-                        name="mask"
-                        key="errors.zip"/>
+                  <arg0 key="address.country"/>
+              </field>
+              <field property="postalCode"
+                     depends="required,mask">
+                  <msg
+                    name="mask"
+                    key="errors.zip"/>
 
-                <arg0 key="address.postalCode"/>
-                <var>
+                  <arg0 key="address.postalCode"/>
+                  <var>
                     <var-name>mask</var-name>
                     <var-value>${zip}</var-value>
-                </var>
-            </field>
-            <field property="province"
-                   depends="required">
+                  </var>
+              </field>
+              <field property="province"
+                     depends="required">
 
-                <arg0 key="address.province"/>
-            </field>
-        </form>
-        <form name="user">
-            <field property="username"
-                   depends="required">
+                  <arg0 key="address.province"/>
+              </field>
+      </form>
+      <form name="user">
+              <field property="username"
+                     depends="required">
 
-                <arg0 key="user.username"/>
-            </field>
-            <field property="password"
-                   depends="required,twofields">
-                <msg
-                        name="twofields"
-                        key="errors.twofields"/>
+                  <arg0 key="user.username"/>
+              </field>
+              <field property="password"
+                     depends="required,twofields">
+                  <msg
+                    name="twofields"
+                    key="errors.twofields"/>
 
-                <arg0 key="user.password"/>
-                <arg1
-                        key="user.confirmPassword"
-                        />
-                <var>
+                  <arg0 key="user.password"/>
+                  <arg1
+                    key="user.confirmPassword"
+                  />
+                  <var>
                     <var-name>secondProperty</var-name>
                     <var-value>confirmPassword</var-value>
-                </var>
-            </field>
-            <field property="confirmPassword"
-                   depends="required">
+                  </var>
+              </field>
+              <field property="confirmPassword"
+                     depends="required">
 
-                <arg0 key="user.confirmPassword"/>
-            </field>
-            <field property="firstName"
-                   depends="required">
+                  <arg0 key="user.confirmPassword"/>
+              </field>
+              <field property="firstName"
+                     depends="required">
 
-                <arg0 key="user.firstName"/>
-            </field>
-            <field property="lastName"
-                   depends="required">
+                  <arg0 key="user.firstName"/>
+              </field>
+              <field property="lastName"
+                     depends="required">
 
-                <arg0 key="user.lastName"/>
-            </field>
-            <field property="address.city"
-                   depends="required">
+                  <arg0 key="user.lastName"/>
+              </field>
+              <field property="address.city"
+                     depends="required">
 
-                <arg0 key="user.address.city"/>
-            </field>
-            <field property="address.country"
-                   depends="required">
+                  <arg0 key="user.address.city"/>
+              </field>
+              <field property="address.country"
+                     depends="required">
 
-                <arg0 key="user.address.country"/>
-            </field>
-            <field property="address.postalCode"
-                   depends="required,mask">
-                <msg
-                        name="mask"
-                        key="errors.zip"/>
+                  <arg0 key="user.address.country"/>
+              </field>
+              <field property="address.postalCode"
+                     depends="required,mask">
+                  <msg
+                    name="mask"
+                    key="errors.zip"/>
 
-                <arg0 key="user.address.postalCode"/>
-                <var>
+                  <arg0 key="user.address.postalCode"/>
+                  <var>
                     <var-name>mask</var-name>
                     <var-value>${zip}</var-value>
-                </var>
-            </field>
-            <field property="address.province"
-                   depends="required">
+                  </var>
+              </field>
+              <field property="address.province"
+                     depends="required">
 
-                <arg0 key="user.address.province"/>
-            </field>
-            <field property="email"
-                   depends="required,email">
+                  <arg0 key="user.address.province"/>
+              </field>
+              <field property="email"
+                     depends="required,email">
 
-                <arg0 key="user.email"/>
-            </field>
-            <field property="phoneNumber"
-                   depends="mask">
-                <msg
-                        name="mask"
-                        key="errors.phone"/>
+                  <arg0 key="user.email"/>
+              </field>
+              <field property="phoneNumber"
+                     depends="mask">
+                  <msg
+                    name="mask"
+                    key="errors.phone"/>
 
-                <arg0 key="user.phoneNumber"/>
-                <var>
+                  <arg0 key="user.phoneNumber"/>
+                  <var>
                     <var-name>mask</var-name>
                     <var-value>${phone}</var-value>
-                </var>
-            </field>
-            <field property="passwordHint"
-                   depends="required">
+                  </var>
+              </field>
+              <field property="passwordHint"
+                     depends="required">
 
-                <arg0 key="user.passwordHint"/>
-            </field>
-        </form>
+                  <arg0 key="user.passwordHint"/>
+              </field>
+      </form>
 
         <form name="person">
             <field property="firstName" depends="required">
@@ -159,5 +157,5 @@
                 <arg0 key="person.lastName"/>
             </field>
         </form>
-    </formset>
+  </formset>
 </form-validation>
Index: src/main/webapp/WEB-INF/web.xml
===================================================================
--- src/main/webapp/WEB-INF/web.xml	(revision 85)
+++ src/main/webapp/WEB-INF/web.xml	(working copy)
@@ -27,11 +27,10 @@
     <context-param>
         <param-name>contextConfigLocation</param-name>
         <param-value>
-            classpath*:/applicationContext-resources.xml
-            classpath*:/applicationContext-dao.xml
-            classpath*:/applicationContext-service.xml
+            classpath:/applicationContext-dao.xml
+            classpath:/applicationContext-service.xml
             classpath*:/applicationContext.xml
-            /WEB-INF/applicationContext*.xml
+            /WEB-INF/**/applicationContext*.xml
             /WEB-INF/xfire-servlet.xml
             /WEB-INF/security.xml
         </param-value>
@@ -99,7 +98,7 @@
         <filter-class>org.appfuse.webapp.filter.StaticFilter</filter-class>
         <init-param>
             <param-name>includes</param-name>
-            <param-value>/scripts/dojo/*</param-value>
+            <param-value>/scripts/dojo/*,/dwr/*</param-value>
         </init-param>
         <init-param>
             <param-name>servletName</param-name>
@@ -196,18 +195,28 @@
             <param-value>true</param-value>
         </init-param>
     </servlet>
+    
+    <servlet>
+        <servlet-name>xfire</servlet-name>
+        <servlet-class>org.codehaus.xfire.spring.XFireSpringServlet</servlet-class>
+    </servlet>
 
+    <servlet-mapping>
+        <servlet-name>dwr-invoker</servlet-name>
+        <url-pattern>/dwr/*</url-pattern>
+    </servlet-mapping>
+    
+    <servlet-mapping>
+        <servlet-name>xfire</servlet-name>
+        <url-pattern>/services/*</url-pattern>
+    </servlet-mapping>
+    
     <!-- Dispatching handled by StaticFilter -->
     <!--<servlet-mapping>
         <servlet-name>dispatcher</servlet-name>
         <url-pattern>*.html</url-pattern>
     </servlet-mapping>-->
 
-    <servlet-mapping>
-        <servlet-name>dwr-invoker</servlet-name>
-        <url-pattern>/dwr/*</url-pattern>
-    </servlet-mapping>
-
     <session-config>
         <session-timeout>10</session-timeout>
     </session-config>
Index: src/main/webapp/common/menu.jsp
===================================================================
--- src/main/webapp/common/menu.jsp	(revision 85)
+++ src/main/webapp/common/menu.jsp	(working copy)
@@ -3,10 +3,7 @@
 <menu:useMenuDisplayer name="Velocity" config="cssHorizontalMenu.vm" permissions="rolesAdapter">

 <ul id="primary-nav" class="menuList">

     <li class="pad">&nbsp;</li>

-    <c:if test="${empty pageContext.request.remoteUser}">

-    <li><a href="<c:url value="/login.jsp"/>" class="current">

-        <fmt:message key="login.title"/></a></li>

-    </c:if>

+    <c:if test="${empty pageContext.request.remoteUser}"><li><a href="<c:url value="/login.jsp"/>" class="current"><fmt:message key="login.title"/></a></li></c:if>

     <menu:displayMenu name="MainMenu"/>

     <menu:displayMenu name="UserMenu"/>

     <menu:displayMenu name="PeopleMenu"/>

Index: pom.xml
===================================================================
--- pom.xml	(revision 85)
+++ pom.xml	(working copy)
@@ -6,12 +6,12 @@
     <groupId>org.appfuse.tutorial</groupId>
     <artifactId>tutorial-spring</artifactId>
     <packaging>war</packaging>
-    <version>1.0-m5</version>
+    <version>1.0</version>
     <name>AppFuse Spring MVC Application</name>
     <url>http://www.mycompany.com</url>
 
     <prerequisites>
-        <maven>2.0.4</maven>
+        <maven>2.0.6</maven>
     </prerequisites>
 
     <licenses>
@@ -45,6 +45,48 @@
         <defaultGoal>install</defaultGoal>
         <plugins>
             <plugin>
+                <groupId>org.codehaus.mojo</groupId>
+                <artifactId>appfuse-maven-plugin</artifactId>
+                <version>${appfuse.version}</version>
+                <configuration>
+                    <genericCore>${amp.genericCore}</genericCore>
+                    <fullSource>${amp.fullSource}</fullSource>
+                </configuration>
+                <!-- Dependency needed by appfuse:gen-model to connect to database. -->
+                <!-- See http://issues.appfuse.org/browse/APF-868 to learn more.    -->
+                <dependencies>
+                    <dependency>
+                        <groupId>${jdbc.groupId}</groupId>
+                        <artifactId>${jdbc.artifactId}</artifactId>
+                        <version>${jdbc.version}</version>
+                    </dependency>
+                </dependencies>
+            </plugin>
+            <plugin>
+                <groupId>org.codehaus.mojo</groupId>
+                <artifactId>aspectj-maven-plugin</artifactId>
+                <version>1.0-beta-2</version>
+                <configuration>
+                    <source>1.5</source>
+                    <verbose>true</verbose>
+                    <complianceLevel>1.5</complianceLevel>
+                    <showWeaveInfo>true</showWeaveInfo>
+                    <aspectLibraries>
+                        <aspectLibrary>
+                            <groupId>org.springframework</groupId>
+                            <artifactId>spring-aspects</artifactId>
+                        </aspectLibrary>
+                    </aspectLibraries>
+                </configuration>
+                <executions>
+                    <execution>
+                        <goals>
+                            <goal>compile</goal>
+                        </goals>
+                    </execution>
+                </executions>
+            </plugin>
+            <plugin>
                 <artifactId>maven-compiler-plugin</artifactId>
                 <version>2.0.2</version>
                 <configuration>
@@ -54,7 +96,7 @@
             </plugin>
             <plugin>
                 <artifactId>maven-eclipse-plugin</artifactId>
-                <version>2.3</version>
+                <version>2.4</version>
                 <configuration>
                     <additionalProjectnatures>
                         <projectnature>org.springframework.ide.eclipse.core.springnature</projectnature>
@@ -69,7 +111,7 @@
             </plugin>
             <plugin>
                 <artifactId>maven-idea-plugin</artifactId>
-                <version>2.0</version>
+                <version>2.1</version>
                 <configuration>
                     <downloadSources>true</downloadSources>
                     <downloadJavadocs>true</downloadJavadocs>
@@ -80,7 +122,7 @@
             <plugin>
                 <groupId>org.codehaus.mojo</groupId>
                 <artifactId>hibernate3-maven-plugin</artifactId>
-                <version>2.0-alpha-1</version>
+                <version>2.0-alpha-2</version>
                 <configuration>
                     <components>
                         <component>
@@ -154,13 +196,22 @@
             <plugin>
                 <groupId>org.mortbay.jetty</groupId>
                 <artifactId>maven-jetty-plugin</artifactId>
-                <version>6.0.0</version>
+                <version>6.1.5</version>
                 <configuration>
                     <contextPath>/</contextPath>
                     <scanIntervalSeconds>3</scanIntervalSeconds>
-                    <scanTargets>
-                        <scanTarget>src/main/webapp/WEB-INF</scanTarget>
-                    </scanTargets>
+                    <scanTargetPatterns>
+                        <scanTargetPattern>
+                            <directory>src/main/webapp/WEB-INF</directory>
+                            <excludes>
+                                <exclude>**/*.jsp</exclude>
+                            </excludes>
+                            <includes>
+                                <include>**/*.properties</include>
+                                <include>**/*.xml</include>
+                            </includes>
+                        </scanTargetPattern>
+                    </scanTargetPatterns>
                 </configuration>
             </plugin>
             <plugin>
@@ -175,7 +226,7 @@
             <plugin>
                 <groupId>org.appfuse</groupId>
                 <artifactId>maven-warpath-plugin</artifactId>
-                <version>1.0-m5</version>
+                <version>1.0-SNAPSHOT</version>
                 <extensions>true</extensions>
                 <executions>
                     <execution>
@@ -194,15 +245,6 @@
             </plugin>
             <plugin>
                 <groupId>org.codehaus.mojo</groupId>
-                <artifactId>appfuse-maven-plugin</artifactId>
-                <version>${appfuse.version}</version>
-                <configuration>
-                    <genericCore>${amp.genericCore}</genericCore>
-                    <fullSource>${amp.fullSource}</fullSource>
-                </configuration>
-            </plugin>
-            <plugin>
-                <groupId>org.codehaus.mojo</groupId>
                 <artifactId>native2ascii-maven-plugin</artifactId>
                 <version>1.0-alpha-1</version>
                 <configuration>
@@ -218,6 +260,7 @@
                         <configuration>
                             <encoding>UTF8</encoding>
                             <includes>
+                                ApplicationResources_ko.properties,
                                 ApplicationResources_no.properties,
                                 ApplicationResources_tr.properties,
                                 ApplicationResources_zh*.properties
@@ -246,16 +289,25 @@
             <resource>
                 <directory>src/main/resources</directory>
                 <excludes>
-                    <exclude>ApplicationResources_zh*.properties</exclude>
                     <exclude>ApplicationResources_de.properties</exclude>
                     <exclude>ApplicationResources_fr.properties</exclude>
+                    <exclude>ApplicationResources_ko.properties</exclude>
                     <exclude>ApplicationResources_nl.properties</exclude>
                     <exclude>ApplicationResources_no.properties</exclude>
                     <exclude>ApplicationResources_pt*.properties</exclude>
                     <exclude>ApplicationResources_tr.properties</exclude>
+                    <exclude>ApplicationResources_zh*.properties</exclude>
+                    <exclude>applicationContext-resources.xml</exclude>
                 </excludes>
                 <filtering>true</filtering>
             </resource>
+            <resource>
+                <directory>src/main/resources</directory>
+                <includes>
+                    <include>applicationContext-resources.xml</include>
+                </includes>
+                <filtering>false</filtering>
+            </resource>
         </resources>
         <testResources>
             <testResource>
@@ -474,31 +526,18 @@
                         </executions>
                         <dependencies>
                             <dependency>
-                                <groupId>com.canoo</groupId>
+                                <groupId>com.canoo.webtest</groupId>
                                 <artifactId>webtest</artifactId>
                                 <version>${webtest.version}</version>
+                                <!-- groovy-all doesn't have a pom in central repo -->
+                                <!-- exclude groovy to prevent trying to fetch pom -->
                                 <exclusions>
                                     <exclusion>
-                                        <groupId>javax.xml</groupId>
-                                        <artifactId>jsr173</artifactId>
+                                        <groupId>groovy</groupId>
+                                        <artifactId>groovy-all</artifactId>
                                     </exclusion>
                                 </exclusions>
                             </dependency>
-                            <dependency>
-                                <groupId>javax.mail</groupId>
-                                <artifactId>mail</artifactId>
-                                <version>${javamail.version}</version>
-                            </dependency>
-                            <dependency>
-                                <groupId>log4j</groupId>
-                                <artifactId>log4j</artifactId>
-                                <version>${log4j.version}</version>
-                            </dependency>
-                            <dependency>
-                                <groupId>oro</groupId>
-                                <artifactId>oro</artifactId>
-                                <version>${oro.version}</version>
-                            </dependency>
                         </dependencies>
                     </plugin>
                 </plugins>
@@ -514,7 +553,7 @@
                 <jdbc.artifactId>derbyclient</jdbc.artifactId>
                 <jdbc.version>10.2.2.0</jdbc.version>
                 <jdbc.driverClassName>org.apache.derby.jdbc.ClientDriver</jdbc.driverClassName>
-                <jdbc.url><![CDATA[jdbc:derby://localhost/appfuse;create=true]]></jdbc.url>
+                <jdbc.url><![CDATA[jdbc:derby://localhost/tutorial_spring;create=true]]></jdbc.url>
                 <jdbc.username>any</jdbc.username>
                 <jdbc.password>value</jdbc.password>
             </properties>
@@ -528,7 +567,7 @@
                 <jdbc.artifactId>h2</jdbc.artifactId>
                 <jdbc.version>1.0.20061217</jdbc.version>
                 <jdbc.driverClassName>org.h2.Driver</jdbc.driverClassName>
-                <jdbc.url><![CDATA[jdbc:h2:tutorial-spring]]></jdbc.url>
+                <jdbc.url><![CDATA[jdbc:h2:tutorial_spring]]></jdbc.url>
                 <jdbc.username>sa</jdbc.username>
                 <jdbc.password></jdbc.password>
             </properties>
@@ -542,7 +581,7 @@
                 <jdbc.artifactId>hsqldb</jdbc.artifactId>
                 <jdbc.version>1.8.0.7</jdbc.version>
                 <jdbc.driverClassName>org.hsqldb.jdbcDriver</jdbc.driverClassName>
-                <jdbc.url><![CDATA[jdbc:hsqldb:tutorial-spring;shutdown=true]]></jdbc.url>
+                <jdbc.url><![CDATA[jdbc:hsqldb:tutorial_spring;shutdown=true]]></jdbc.url>
                 <jdbc.username>sa</jdbc.username>
                 <jdbc.password></jdbc.password>
             </properties>
@@ -570,7 +609,7 @@
                 <jdbc.artifactId>postgresql</jdbc.artifactId>
                 <jdbc.version>8.1-407.jdbc3</jdbc.version>
                 <jdbc.driverClassName>org.postgresql.Driver</jdbc.driverClassName>
-                <jdbc.url><![CDATA[jdbc:postgresql://localhost/tutorial-spring]]></jdbc.url>
+                <jdbc.url><![CDATA[jdbc:postgresql://localhost/tutorial_spring]]></jdbc.url>
                 <jdbc.username>postgres</jdbc.username>
                 <jdbc.password>postgres</jdbc.password>
             </properties>
@@ -587,7 +626,7 @@
                 <jdbc.artifactId>jtds</jdbc.artifactId>
                 <jdbc.version>1.2</jdbc.version>
                 <jdbc.driverClassName>net.sourceforge.jtds.jdbc.Driver</jdbc.driverClassName>
-                <jdbc.url><![CDATA[jdbc:jtds:sqlserver://localhost:3683/tutorial-spring]]></jdbc.url>
+                <jdbc.url><![CDATA[jdbc:jtds:sqlserver://localhost:3683/tutorial_spring]]></jdbc.url>
                 <jdbc.username>sa</jdbc.username>
                 <jdbc.password>appfuse</jdbc.password>
             </properties>
@@ -612,26 +651,23 @@
         <amp.fullSource>false</amp.fullSource>
         
         <!-- Framework dependency versions -->
-        <appfuse.version>2.0-m5</appfuse.version>
-        <spring.version>2.0.5</spring.version>
+        <appfuse.version>2.0-SNAPSHOT</appfuse.version>
+        <spring.version>2.0.6</spring.version>
 
         <!-- Testing dependency versions -->
         <jmock.version>1.1.0</jmock.version>
         <jsp.version>2.0</jsp.version>
-        <junit.version>3.8.2</junit.version>
+        <junit.version>4.4</junit.version>
         <servlet.version>2.4</servlet.version>
-        <wiser.version>1.0.3</wiser.version>
+        <wiser.version>1.2</wiser.version>
 
         <!-- WebTest dependency versions  -->
-        <javamail.version>1.4</javamail.version>
-        <log4j.version>1.2.13</log4j.version>
-        <oro.version>2.0.8</oro.version>
-        <webtest.version>1454</webtest.version>
+        <webtest.version>R_1600</webtest.version>
 
         <!-- Cargo settings -->
         <cargo.container>tomcat5x</cargo.container>
         <cargo.container.home>${env.CATALINA_HOME}</cargo.container.home>
-        <cargo.container.url>http://archive.apache.org/dist/tomcat/tomcat-5/v5.5.23/bin/apache-tomcat-5.5.23.zip</cargo.container.url>
+        <cargo.container.url>http://archive.apache.org/dist/tomcat/tomcat-6/v6.0.14/bin/apache-tomcat-6.0.14.zip</cargo.container.url>
         <cargo.host>localhost</cargo.host>
         <cargo.port>8081</cargo.port>
         <cargo.wait>false</cargo.wait>
@@ -644,7 +680,7 @@
         <jdbc.artifactId>mysql-connector-java</jdbc.artifactId>
         <jdbc.version>5.0.5</jdbc.version>
         <jdbc.driverClassName>com.mysql.jdbc.Driver</jdbc.driverClassName>
-        <jdbc.url><![CDATA[jdbc:mysql://localhost/tutorial?createDatabaseIfNotExist=true&amp;useUnicode=true&amp;characterEncoding=utf-8]]></jdbc.url>
+        <jdbc.url><![CDATA[jdbc:mysql://localhost/tutorial_spring?createDatabaseIfNotExist=true&amp;useUnicode=true&amp;characterEncoding=utf-8]]></jdbc.url>
         <jdbc.username>root</jdbc.username>
         <jdbc.password></jdbc.password>
     </properties>

```



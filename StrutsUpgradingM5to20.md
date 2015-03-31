
```
Index: src/test/resources/web-tests.xml
===================================================================
--- src/test/resources/web-tests.xml	(revision 85)
+++ src/test/resources/web-tests.xml	(working copy)
@@ -84,7 +84,7 @@
             &config;
             <steps>
                 &login;
-                <invoke description="click View Users link" url="/users.html"/>
+                <invoke description="click View Users link" url="/admin/users.html"/>
                 <verifytitle description="we should see the user list title" 
                     text=".*${userList.title}.*" regex="true"/>
             </steps>
@@ -114,7 +114,7 @@
             &config;
             <steps>
                 &login;
-                <invoke description="click Add Button" url="/editUser.html?method=Add&amp;from=list"/>
+                <invoke description="click Add Button" url="/editUser.html?from=list"/>
                 <verifytitle description="we should see the user profile title"
                     text=".*${userProfile.title}.*" regex="true"/>
                     
@@ -135,7 +135,7 @@
                 
                 <verifytitle description="view user list screen" text=".*${userList.title}.*" regex="true"/>
                 <verifytext description="verify success message" regex="true"
-                    text='&lt;div class="message.*&gt;.*&lt;strong&gt;Test Name&lt;/strong&gt;.*&lt;/div&gt;'/>
+                    text='&lt;div class="message.*&gt;.*Test Name.*&lt;/div&gt;'/>
                     
                 <!-- Delete user -->
                 <clicklink description="Click edit user link" label="newuser"/>
@@ -144,7 +144,7 @@
                 <clickbutton label="${button.delete}" description="Click button 'Delete'"/>
                 <!--verifyNoDialogResponses/-->
                 <verifytext description="verify success message" regex="true"
-                    text='&lt;div class="message.*&gt;.*&lt;strong&gt;Test Name&lt;/strong&gt;.*&lt;/div&gt;'/>
+                    text='&lt;div class="message.*&gt;.*Test Name.*&lt;/div&gt;'/>
                 <verifytitle description="display user list" text=".*${userList.title}.*" regex="true"/>
             </steps>
         </webtest>
@@ -172,7 +172,7 @@
                 <setinputfield description="set passwordHint" name="user.passwordHint" value="test"/>
                 
                 <enableJavaScript enable="false"/> <!-- HtmlUnit doesn't understand table.rows.length -->
-                <clickbutton label="${button.register}" description="Click button 'Signup'"/>
+                <clickbutton name="button.register" description="Click button 'Signup'"/>
                 
                 <verifytitle description="view main menu" text=".*${mainMenu.title}.*" regex="true"/>
                 <verifytext description="verify success message" text="${user.registered}"/>
@@ -186,7 +186,7 @@
             &config;
             <steps>
                 &login;
-                <invoke description="get activeUsers URL" url="/activeUsers.html"/>
+                <invoke description="get activeUsers URL" url="/admin/activeUsers.html"/>
                 <verifytitle description="we should see the activeUsers title" 
                     text=".*${activeUsers.title}.*" regex="true"/>
             </steps>
@@ -199,7 +199,7 @@
             &config;
             <steps>
                 &login;
-                <invoke description="get flushCache URL" url="/flushCache.html"/>
+                <invoke description="get flushCache URL" url="/admin/flushCache.html"/>
                 <verifytitle description="we should see the flush cache title"
                     text=".*${flushCache.title}.*" regex="true"/>
             </steps>
@@ -212,7 +212,7 @@
             &config;
             <steps>
                 &login;
-                <invoke description="click Upload a File link" url="/uploadFile!start.html"/>
+                <invoke description="click Upload a File link" url="/uploadFile.html"/>
                 <verifytitle description="we should see file upload form" text=".*${upload.title}.*" regex="true"/>
                 <setinputfield description="set name" name="name" value="Canoo Test File"/>
                 <setFileField description="set file" name="file" fileName="pom.xml"/>
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
@@ -1,186 +1,186 @@
-user.status=Iniciado como \:

-user.logout=Salir

-

-# -- validator errors --

-errors.invalid={0} no es v\u00E1lido.

-errors.maxlength={0} no puede ser m\u00E1s grande de {1} caracteres.

-errors.minlength={0} no puede ser menor que {1} caracteres.

-errors.range={0} no est\u00E1 en el rango entre {1} y {2}.

-errors.required={0} es un campo requerido.

-errors.byte={0} debe ser un byte.

-errors.date={0} no es una fecha.

-errors.double={0} debe ser un valor flotante doble.

-errors.float={0} deber ser un valor flotante.

-errors.integer={0} debe ser un entero.

-errors.long={0} debe ser un entero largo.

-errors.short={0} debe ser un entero corto.

-errors.creditcard={0} no es un n\u00FAmero v\u00E1lido de tarjeta de cr\u00E9dito.

-errors.email={0} no es una direcci\u00F3n de e-mail v\u00E1lida.

-errors.phone={0} no es un n\u00FAmero de tel\u00E9fono v\u00E1lido.

-errors.zip={0} no es un c\u00F3digo postal v\u00E1lido.

-

-# -- other errors --

-errors.cancel=Operaci\u00F3n cancelada.

-errors.detail={0}

-errors.general=<strong>El proceso no se ha completado. Eval\u00FAe los siguiente detalles\:</strong>

-errors.token=La petici\u00F3n no pudo completarse. La operaci\u00F3n no est\u00E1 en proceso.

-errors.none=No hay mensajes de error, revise los logs del servidor.

-errors.password.mismatch=Nombre de usuario o contrase\u00F1a no v\u00E1lido, por favor, int\u00E9ntelo de nuevo.

-errors.conversion=Se ha producido un error mientras se convert\u00EDan valores de la web a valores de datos.

-errors.twofields=El campo {0} debe tener el mismo valor que el campo {1}.

-errors.existing.user=Este usuario ({0}) o direcci\u00F3n de e-mail ({1}) ya existe.  Por favor int\u00E9ntelo con un nombre de usuario diferente.

-

-# -- success messages --

-user.added=La informaci\u00F3n del usuario <strong>{0}</strong> has sido insertada con \u00E9xito.

-user.deleted=El perfil del usuario <strong>{0}</strong> ha sido borrado con \u00E9xito.

-user.registered=Ha sido registrado con \u00E9xito para acceder a esta aplicaci\u00F3n.

-user.saved=Su perfil ha sido actualizado con \u00E9xito.

-user.updated.byAdmin=La informaci\u00F3n del usuario <strong>{0}</strong> ha sido actualizada con \u00E9xito.

-newuser.email.message={0} ha creado una cuenta para usted. Su usuario y contrase\u00F1a son los siguientes.

-reload.succeeded=La recarga de opciones se ha completado con \u00E9xito.

-

-# -- error page messages --

-errorPage.title=Ha ocurrido un error

-errorPage.heading=\u00A1Error\!

-404.title=P\u00E1gina No Encontrada

-404.message=La p\u00E1gina solicitada no existe. Deber\u00EDa intentar volver al <a href\="{0}">Men\u00FA Principal</a>. Mientras usted est\u00E1 aqu\u00ED, \u00BFLe gustar\u00EDa ver una foto para animarle?

-403.message=Su rol no le permite ver esta p\u00E1gina. Por favor contacte con el administrador si cree que usted deber\u00EDa tener acceso. Mientras tanto, una bonita foto para animarle.

-

-# -- login --

-login.title=Usuario

-login.heading=Control de acceso

-login.rememberMe=Recordarme

-login.signup=\u00BFNo es miembro? <a href\="{0}">Crear</a> una cuenta.

-403.title=Acceso Denegado

-login.passwordHint=\u00BFOlvid\u00F3 su contrase\u00F1a?  Enviarme la <a href\="?" onmouseover\="window.status\='Enviarme la pista de la contrase\u00F1a.'; return true" onmouseout\="window.status\=''; return true" title\="Enviarme la pista de la contrase\u00F1a." onclick\="passwordHint(); return false">pista de la contrase\u00F1a por email</a>.

-login.passwordHint.sent=La pista de la contrase\u00F1a para <strong>{0}</strong> ha sido enviada a <strong>{1}</strong>.

-login.passwordHint.error=El usuario <strong>{0}</strong> no se encuentra en nuestra base de datos.

-

-# -- mainMenu --

-mainMenu.title=Men\u00FA Principal

-mainMenu.heading=\u00A1Bienvenido\!

-mainMenu.message=\u00A1Felicidades, usted ha entrado en la aplicaci\u00F3n\!  Ahora que ha entrado correctamente, puede utilizar las siguientes opciones\:

-mainMenu.activeUsers=Usuarios conectados

-

-# -- menu/link messages --

-menu.admin=Administraci\u00F3n

-menu.admin.users=Ver lista de usuarios

-menu.admin.reload=Recargar Opciones

-

-menu.user=Editar Perfil

-menu.selectFile=Subir Un Fichero

-menu.flushCache=Recargar Cach\u00E9

-menu.clickstream=Clickstream

-

-# -- form labels --

-label.username=Usuario

-label.password=Contrase\u00F1a

-

-# -- button labels --

-button.add=A\u00F1adir

-button.cancel=Cancelar

-button.copy=Copiar

-button.delete=Borrar

-button.done=Hecho

-button.edit=Editar

-button.register=Registrar

-button.save=Guardar

-button.search=Buscar

-button.upload=Subir

-button.view=Ver

-button.reset=Reiniciar

-button.login=Entrar

-

-# -- general values --

-icon.information=Informaci\u00F3n

-icon.information.img=/images/iconInformation.gif

-icon.email=E-Mail

-icon.email.img=/images/iconEmail.gif

-icon.warning=Peligro

-icon.warning.img=/images/iconWarning.gif

-date.format=dd/MM/yyyy

-

-# -- role form --

-roleForm.name=Nombre

-

-# -- user profile page --

-userProfile.title=Propiedades del Usuario

-userProfile.heading=Perfil de Usuario

-userProfile.message=Por favor actualice su informci\u00F3n mediante el siguiente formulario.

-userProfile.admin.message=Usted puede actualizar la informaci\u00F3n del usuario mediante el siguiente formulario.

-userProfile.showMore=Ver más información

-userProfile.accountSettings=Configuraci\u00F3n de la cuenta

-userProfile.assignRoles=Asignar Roles

-userProfile.cookieLogin=Usted no puede cambiar su contrase\u00F1a si ha entrado mediante la caracter\u00EDstica <strong>Recordarme</strong>. Por favor, salga de la aplicaci\u00F3n y vuelva entrar para cambiar contrase\u00F1a.

-

-# -- user form --

-user.address.address=Direcci\u00F3n

-user.availableRoles=Roles Permitidos

-user.address.city=Ciudad

-user.address.country=Pais

-user.firstName=Nombre

-user.email=E-Mail

-user.lastName=Apellidos

-user.id=Id

-user.confirmPassword=Confirme Contrase\u00F1a

-user.phoneNumber=N\u00FAmero de tel\u00E9fono

-user.address.postalCode=C\u00F3digo Postal

-user.address.province=Provincia

-user.roles=Roles Activos

-user.username=Usuario

-user.website=Web

-user.visitWebsite=visitar

-user.password=Contrase\u00F1a

-user.passwordHint=Olvid\u00F3 su Contrase\u00F1a

-user.enabled=Habilitada

-user.accountExpired=Caducada

-user.accountLocked=Bloqueada

-user.credentialsExpired=Contrase\u00F1a Caducada

-

-# -- user list page --

-userList.title=Listado de Usuarios

-userList.heading=Usuarios Activos

-userList.nousers=<span>No se han encontrado Usuarios.</span>

-

-# -- user self-registration --

-signup.title=Registro

-signup.heading=Registro de Nuevo Usuario

-signup.message=Por favor introduzca sus datos mediante el siguiente formulario.

-signup.email.subject=Datos Cuenta Registrada (AppFuse)

-signup.email.message=Usted ha sido registrado con \u00E9xito en nuestra aplicaci\u00F3n. Su usuario y contrase\u00F1a son los siguientes\:

-

-# -- upload page messages --

-maxLengthExceeded=El fichero que usted ha intentado subir es demasiado grande. El tama\u00F1o m\u00E1ximo habilitado es de 2 MB.

-upload.title=S\u00FAbida de Ficheros al Servidor

-upload.heading=Subir un fichero

-upload.message=\u00A1Ojo\u0021 el m\u00E1ximo tama\u00F1o habilitado para subir ficheros a esta aplicaci\u00F3n es de 2 MB.

-uploadForm.name=Nombre

-uploadForm.file=Fichero a Subir

-

-# -- display page messages --

-display.title=\u00A1Fichero Subido con \u00C9xito\!

-display.heading=Informaci\u00F3n del Fichero

-

-# -- flushCache page --

-flushCache.title=Actualizar la Cach\u00E9

-flushCache.heading=\u00A1Actualizaci\u00F3n realizada con \u00C9xito\!

-flushCache.message=Todas las cach\u00E9s se han actualizado con \u00E9xito, volviendo a la p\u00E1gina anterior en 2 segundos.

-

-# -- clickstreams page --

-clickstreams.title=Eventos sobre enlace

-clickstreams.heading=Todos los eventos

-

-# -- viewstream page --

-viewstream.title=Detalles de las visitas

-viewstream.heading=Stream Information

-

-# -- active users page --

-activeUsers.title=Usuarios Activos

-activeUsers.heading=Usuarios Conectados

-activeUsers.message=La siguiente lista muestra los usuarios que han entrado y cuyas sesiones no han caducado.

-activeUsers.fullName=Nombre Completo

-

-# JSF-only messages, remove if not using JSF

-javax.faces.component.UIInput.REQUIRED={0} es un campo requerido.

-activeUsers.summary={0} Usuario(s) encontrado(s), muestra {1} usuario(s), del {2} al {3}. Página {4} / {5}

-

+user.status=Iniciado como \:
+user.logout=Salir
+
+# -- validator errors --
+errors.invalid={0} no es v\u00E1lido.
+errors.maxlength={0} no puede ser m\u00E1s grande de {1} caracteres.
+errors.minlength={0} no puede ser menor que {1} caracteres.
+errors.range={0} no est\u00E1 en el rango entre {1} y {2}.
+errors.required={0} es un campo requerido.
+errors.byte={0} debe ser un byte.
+errors.date={0} no es una fecha.
+errors.double={0} debe ser un valor flotante doble.
+errors.float={0} deber ser un valor flotante.
+errors.integer={0} debe ser un entero.
+errors.long={0} debe ser un entero largo.
+errors.short={0} debe ser un entero corto.
+errors.creditcard={0} no es un n\u00FAmero v\u00E1lido de tarjeta de cr\u00E9dito.
+errors.email={0} no es una direcci\u00F3n de e-mail v\u00E1lida.
+errors.phone={0} no es un n\u00FAmero de tel\u00E9fono v\u00E1lido.
+errors.zip={0} no es un c\u00F3digo postal v\u00E1lido.
+
+# -- other errors --
+errors.cancel=Operaci\u00F3n cancelada.
+errors.detail={0}
+errors.general=El proceso no se ha completado. Eval\u00FAe los siguiente detalles.
+errors.token=La petici\u00F3n no pudo completarse. La operaci\u00F3n no est\u00E1 en proceso.
+errors.none=No hay mensajes de error, revise los logs del servidor.
+errors.password.mismatch=Nombre de usuario o contrase\u00F1a no v\u00E1lido, por favor, int\u00E9ntelo de nuevo.
+errors.conversion=Se ha producido un error mientras se convert\u00EDan valores de la web a valores de datos.
+errors.twofields=El campo {0} debe tener el mismo valor que el campo {1}.
+errors.existing.user=Este usuario ({0}) o direcci\u00F3n de e-mail ({1}) ya existe.  Por favor int\u00E9ntelo con un nombre de usuario diferente.
+
+# -- success messages --
+user.added=La informaci\u00F3n del usuario {0} has sido insertada con \u00E9xito.
+user.deleted=El perfil del usuario {0} ha sido borrado con \u00E9xito.
+user.registered=Ha sido registrado con \u00E9xito para acceder a esta aplicaci\u00F3n.
+user.saved=Su perfil ha sido actualizado con \u00E9xito.
+user.updated.byAdmin=La informaci\u00F3n del usuario {0} ha sido actualizada con \u00E9xito.
+newuser.email.message={0} ha creado una cuenta para usted. Su usuario y contrase\u00F1a son los siguientes.
+reload.succeeded=La recarga de opciones se ha completado con \u00E9xito.
+
+# -- error page messages --
+errorPage.title=Ha ocurrido un error
+errorPage.heading=\u00A1Error\!
+404.title=P\u00E1gina No Encontrada
+404.message=La p\u00E1gina solicitada no existe. Deber\u00EDa intentar volver al <a href\="{0}">Men\u00FA Principal</a>. Mientras usted est\u00E1 aqu\u00ED, \u00BFLe gustar\u00EDa ver una foto para animarle?
+403.message=Su rol no le permite ver esta p\u00E1gina. Por favor contacte con el administrador si cree que usted deber\u00EDa tener acceso. Mientras tanto, una bonita foto para animarle.
+
+# -- login --
+login.title=Usuario
+login.heading=Control de acceso
+login.rememberMe=Recordarme
+login.signup=\u00BFNo es miembro? <a href\="{0}">Crear</a> una cuenta.
+403.title=Acceso Denegado
+login.passwordHint=\u00BFOlvid\u00F3 su contrase\u00F1a?  Enviarme la <a href\="?" onmouseover\="window.status\='Enviarme la pista de la contrase\u00F1a.'; return true" onmouseout\="window.status\=''; return true" title\="Enviarme la pista de la contrase\u00F1a." onclick\="passwordHint(); return false">pista de la contrase\u00F1a por email</a>.
+login.passwordHint.sent=La pista de la contrase\u00F1a para {0} ha sido enviada a {1}.
+login.passwordHint.error=El usuario {0} no se encuentra en nuestra base de datos.
+
+# -- mainMenu --
+mainMenu.title=Men\u00FA Principal
+mainMenu.heading=\u00A1Bienvenido\!
+mainMenu.message=\u00A1Felicidades, usted ha entrado en la aplicaci\u00F3n\!  Ahora que ha entrado correctamente, puede utilizar las siguientes opciones\:
+mainMenu.activeUsers=Usuarios conectados
+
+# -- menu/link messages --
+menu.admin=Administraci\u00F3n
+menu.admin.users=Ver lista de usuarios
+menu.admin.reload=Recargar Opciones
+
+menu.user=Editar Perfil
+menu.selectFile=Subir Un Fichero
+menu.flushCache=Recargar Cach\u00E9
+menu.clickstream=Clickstream
+
+# -- form labels --
+label.username=Usuario
+label.password=Contrase\u00F1a
+
+# -- button labels --
+button.add=A\u00F1adir
+button.cancel=Cancelar
+button.copy=Copiar
+button.delete=Borrar
+button.done=Hecho
+button.edit=Editar
+button.register=Registrar
+button.save=Guardar
+button.search=Buscar
+button.upload=Subir
+button.view=Ver
+button.reset=Reiniciar
+button.login=Entrar
+
+# -- general values --
+icon.information=Informaci\u00F3n
+icon.information.img=/images/iconInformation.gif
+icon.email=E-Mail
+icon.email.img=/images/iconEmail.gif
+icon.warning=Peligro
+icon.warning.img=/images/iconWarning.gif
+date.format=dd/MM/yyyy
+
+# -- role form --
+roleForm.name=Nombre
+
+# -- user profile page --
+userProfile.title=Propiedades del Usuario
+userProfile.heading=Perfil de Usuario
+userProfile.message=Por favor actualice su informci\u00F3n mediante el siguiente formulario.
+userProfile.admin.message=Usted puede actualizar la informaci\u00F3n del usuario mediante el siguiente formulario.
+userProfile.showMore=Ver más información
+userProfile.accountSettings=Configuraci\u00F3n de la cuenta
+userProfile.assignRoles=Asignar Roles
+userProfile.cookieLogin=Usted no puede cambiar su contrase\u00F1a si ha entrado mediante la caracter\u00EDstica <strong>Recordarme</strong>. Por favor, salga de la aplicaci\u00F3n y vuelva entrar para cambiar contrase\u00F1a.
+
+# -- user form --
+user.address.address=Direcci\u00F3n
+user.availableRoles=Roles Permitidos
+user.address.city=Ciudad
+user.address.country=Pais
+user.firstName=Nombre
+user.email=E-Mail
+user.lastName=Apellidos
+user.id=Id
+user.confirmPassword=Confirme Contrase\u00F1a
+user.phoneNumber=N\u00FAmero de tel\u00E9fono
+user.address.postalCode=C\u00F3digo Postal
+user.address.province=Provincia
+user.roles=Roles Activos
+user.username=Usuario
+user.website=Web
+user.visitWebsite=visitar
+user.password=Contrase\u00F1a
+user.passwordHint=Olvid\u00F3 su Contrase\u00F1a
+user.enabled=Habilitada
+user.accountExpired=Caducada
+user.accountLocked=Bloqueada
+user.credentialsExpired=Contrase\u00F1a Caducada
+
+# -- user list page --
+userList.title=Listado de Usuarios
+userList.heading=Usuarios Activos
+userList.nousers=<span>No se han encontrado Usuarios.</span>
+
+# -- user self-registration --
+signup.title=Registro
+signup.heading=Registro de Nuevo Usuario
+signup.message=Por favor introduzca sus datos mediante el siguiente formulario.
+signup.email.subject=Datos Cuenta Registrada (AppFuse)
+signup.email.message=Usted ha sido registrado con \u00E9xito en nuestra aplicaci\u00F3n. Su usuario y contrase\u00F1a son los siguientes\:
+
+# -- upload page messages --
+maxLengthExceeded=El fichero que usted ha intentado subir es demasiado grande. El tama\u00F1o m\u00E1ximo habilitado es de 2 MB.
+upload.title=S\u00FAbida de Ficheros al Servidor
+upload.heading=Subir un fichero
+upload.message=\u00A1Ojo\u0021 el m\u00E1ximo tama\u00F1o habilitado para subir ficheros a esta aplicaci\u00F3n es de 2 MB.
+uploadForm.name=Nombre
+uploadForm.file=Fichero a Subir
+
+# -- display page messages --
+display.title=\u00A1Fichero Subido con \u00C9xito\!
+display.heading=Informaci\u00F3n del Fichero
+
+# -- flushCache page --
+flushCache.title=Actualizar la Cach\u00E9
+flushCache.heading=\u00A1Actualizaci\u00F3n realizada con \u00C9xito\!
+flushCache.message=Todas las cach\u00E9s se han actualizado con \u00E9xito, volviendo a la p\u00E1gina anterior en 2 segundos.
+
+# -- clickstreams page --
+clickstreams.title=Eventos sobre enlace
+clickstreams.heading=Todos los eventos
+
+# -- viewstream page --
+viewstream.title=Detalles de las visitas
+viewstream.heading=Stream Information
+
+# -- active users page --
+activeUsers.title=Usuarios Activos
+activeUsers.heading=Usuarios Conectados
+activeUsers.message=La siguiente lista muestra los usuarios que han entrado y cuyas sesiones no han caducado.
+activeUsers.fullName=Nombre Completo
+
+# JSF-only messages, remove if not using JSF
+javax.faces.component.UIInput.REQUIRED={0} es un campo requerido.
+activeUsers.summary={0} Usuario(s) encontrado(s), muestra {1} usuario(s), del {2} al {3}. Página {4} / {5}
+
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
Index: src/main/resources/ApplicationResources_zh.properties
===================================================================
--- src/main/resources/ApplicationResources_zh.properties	(revision 85)
+++ src/main/resources/ApplicationResources_zh.properties	(working copy)
@@ -1,187 +1,186 @@
-Ôªø## Do NOT delete! Keep this line to avoid the native2ascii UTF-8 BOM bug. See #APF-639

-

-user.status=ÂΩìÂâçÁî®Êà∑: 

-user.logout=ÈÄÄÂá∫

-

-# -- validator errors --

-errors.invalid={0} Êó†Êïà„ÄÇ

-errors.maxlength={0} ‰∏çËÉΩÂ§ß‰∫é {1} ‰∏™Â≠óÁ¨¶„ÄÇ

-errors.minlength={0} ‰∏çËÉΩÂ∞ë‰∫é {1} ‰∏™Â≠óÁ¨¶„ÄÇ

-errors.range={0} Êú™Âú® {1} ‰∏é {2} ËåÉÂõ¥ÂÜÖ„ÄÇ

-errors.required={0} ‰∏∫ÂøÖÂ°´È°π„ÄÇ

-errors.byte={0} ÂøÖÈ°ª‰∏∫byteÁ±ªÂûã„ÄÇ

-errors.date={0} ‰∏çÊòØÊúâÊïàÊó•ÊúüÊ†ºÂºè„ÄÇ

-errors.double={0} ÂøÖÈ°ª‰∏∫doubleÁ±ªÂûã„ÄÇ

-errors.float={0} ÂøÖÈ°ª‰∏∫floatÁ±ªÂûã„ÄÇ

-errors.integer={0} ÂøÖÈ°ª‰∏∫‰∏ÄÊï∞ÂÄº„ÄÇ

-errors.long={0} ÂøÖÈ°ª‰∏∫longÁ±ªÂûã„ÄÇ

-errors.short={0} ÂøÖÈ°ª‰∏∫shortÁ±ªÂûã„ÄÇ

-errors.creditcard={0} ‰∏∫Êó†Êïà‰ø°Áî®Âç°Âè∑„ÄÇ

-errors.email={0} ‰∏∫Êó†ÊïàÈÇÆ‰ª∂Âú∞ÂùÄ„ÄÇ

-errors.phone={0} ‰∏∫Êó†ÊïàÁîµËØùÂè∑Á†Å„ÄÇ

-errors.zip={0} ‰∏∫Êó†ÊïàÈÇÆÊîøÁºñÁ†Å„ÄÇ

-

-# -- other errors --

-errors.cancel=Êìç‰ΩúË¢´ÂèñÊ∂à„ÄÇ

-errors.detail={0}

-errors.general=<strong>Êìç‰ΩúÊú™ÂÆåÊàê„ÄÇËØ¶ÁªÜÂéüÂõ†Â¶Ç‰∏ã„ÄÇ</strong>

-errors.token=ËØ∑Ê±ÇÊú™ÂÆåÂÖ®Â§ÑÁêÜ„ÄÇÊìç‰ΩúÈ°∫Â∫èÈîôËØØ„ÄÇ

-errors.none=Êó†ÈîôËØØÊ∂àÊÅØÔºåËØ∑Ê£ÄÊü•ÊúçÂä°Âô®Êó•ÂøóÊñá‰ª∂„ÄÇ

-errors.password.mismatch=Êó†ÊïàÁî®Êà∑ÂêçÊàñÂØÜÁ†ÅÔºåËØ∑ÈáçËØï„ÄÇ

-errors.conversion=Âú®webÂ±ÇÊï∞ÊçÆÂà∞‰∏öÂä°Â±ÇÊï∞ÊçÆÁöÑËΩ¨Êç¢ËøáÁ®ã‰∏≠ÔºåÂèëÁîü‰∫Ü‰∏Ä‰∏™ÈîôËØØ„ÄÇ

-errors.twofields={0} Â≠óÊÆµ‰∏é {1} Â≠óÊÆµÁöÑÂÄºÂøÖÈ°ª‰∏ÄËá¥„ÄÇ

-errors.existing.user=Áî®Êà∑Âêç ({0}) Êàñe-mailÂú∞ÂùÄ ({1}) Â∑≤Â≠òÂú®„ÄÇËØ∑ÂÜçÊ¨°Â∞ùËØï‰∏çÂêåÂêçÁß∞„ÄÇ

-

-# -- success messages --

-user.added=Áî®Êà∑ <strong>{0}</strong> ÁöÑ‰ø°ÊÅØÊ∑ªÂä†ÊàêÂäü„ÄÇ

-user.deleted=Áî®Êà∑ <strong>{0}</strong> ÁöÑ‰ø°ÊÅØÂà†Èô§ÊàêÂäü„ÄÇ 

-user.registered=Ê≥®ÂÜåÊàêÂäüÔºåÊÇ®ÂèØ‰ª•ÂºÄÂßã‰ΩøÁî®Á≥ªÁªü„ÄÇ

-user.saved=ÊÇ®ÁöÑ‰ø°ÊÅØÂ∑≤ÊàêÂäüÊõ¥Êñ∞„ÄÇ

-user.updated.byAdmin=Áî®Êà∑ <strong>{0}</strong> ÁöÑ‰ø°ÊÅØÂ∑≤ÊàêÂäüÊõ¥Êñ∞„ÄÇ

-newuser.email.message={0} ‰∏∫ÊÇ®ÊàêÂäüÂàõÂª∫‰∫Ü‰∏Ä‰∏™AppFuseÂ∏êÂè∑„ÄÇÊÇ®ÁöÑÁî®Êà∑ÂêçÂíåÂØÜÁ†Å‰ø°ÊÅØÂ¶Ç‰∏ãÔºö

-reload.succeeded=Â∑≤ÁªèÊàêÂäüÈáçËΩΩ.

-

-# -- error page messages --

-errorPage.title=Á≥ªÁªüÈîôËØØ

-errorPage.heading=Âì¶ÔºÅ

-404.title=È°µÈù¢Êú™ÊâæÂà∞

-404.message=ËØ∑Ê±ÇÁöÑÈ°µÈù¢Êú™ÊâæÂà∞„ÄÇÊÇ®ÂèØ‰ª•ÈÄâÊã©ËøîÂõûÂà∞ <a href="{0}">‰∏ªËèúÂçï</a>„ÄÇÊàñËÄÖÈÄâÊã©Âú®Ê≠§‰ºëÊÅØ‰∏Ä‰∏ãÔºåÂøòÊéâÂàöÊâçÁöÑÊ≤Æ‰∏ßÔºåÊ¨£Ëµè‰∏Ä‰∏™Áæé‰∏ΩÁöÑÂõæÁâáÔºü

-403.title=ËÆøÈóÆË¢´ÊãíÁªù

-403.message=ÊÇ®ÂΩìÂâçËßíËâ≤Êó†ÊùÉÈôêÊü•ÁúãÊ≠§È°µÈù¢„ÄÇËØ∑ËÅîÁ≥ªÁ≥ªÁªüÁÆ°ÁêÜÂëòÔºåËé∑ÂæóÁõ∏Â∫îÁöÑÊùÉÈôê„ÄÇÊ≠§ÂàªÔºåËÆ©Êàë‰ª¨Ê¨£Ëµè‰∏Ä‰∏™ÂõæÁâáÔºåÊîæÊùæ‰∏Ä‰∏ãÂ•ΩÂêßÔºü

-

-# -- login --

-login.title=ÁôªÂΩï

-login.heading=ÁôªÂΩï

-login.rememberMe=ËÆ©Á≥ªÁªüËÆ∞‰ΩèÊàë

-login.signup=‰∏çÊòØÊ≥®ÂÜåÁî®Êà∑? <a href="{0}">Áî≥ËØ∑</a> ‰∏Ä‰∏™Â∏êÂè∑„ÄÇ

-login.passwordHint=ÂøòËÆ∞‰∫ÜÂØÜÁ†Å?  ËÆ©Á≥ªÁªüÂ∞Ü <a href="?" onmouseover="window.status='Á≥ªÁªüÂèëÈÄÅÂØÜÁ†ÅÊèêÁ§∫„ÄÇ'; return true" onmouseout="window.status=''; return true" title="Á≥ªÁªüÂèëÈÄÅÂØÜÁ†ÅÊèêÁ§∫„ÄÇ" onclick="passwordHint(); return false">ÂØÜÁ†ÅÊèêÁ§∫‰ø°ÊÅØÂ∑≤e-mailÂΩ¢ÂºèÂèëÈÄÅÁªôÊÇ®</a>„ÄÇ

-login.passwordHint.sent=<strong>{0}</strong> ÁöÑÂØÜÁ†ÅÊèêÁ§∫Â∑≤ÊàêÂäüÂèëÈÄÅÂà∞ <strong>{1}</strong>„ÄÇ

-login.passwordHint.error=Áî®Êà∑Âêç <strong>{0}</strong> Âú®Á≥ªÁªüÊï∞ÊçÆÂ∫ì‰∏≠Êú™ÊâæÂà∞„ÄÇ

-

-# -- mainMenu --

-mainMenu.title=‰∏ªËèúÂçï

-mainMenu.heading=Ê¨¢ËøéÔºÅ

-mainMenu.message=ÊÅ≠ÂñúÔºåÊÇ®ÁôªÂΩïÊàêÂäüÔºÅÊÇ®ÂèØ‰ª•ÈÄâÊã©ÊâßË°å‰ª•‰∏ãÊìç‰ΩúÔºö

-mainMenu.activeUsers=Âú®Á∫øÁî®Êà∑

-

-# -- menu/link messages --

-menu.admin=Á≥ªÁªüÁÆ°ÁêÜ

-menu.admin.users=Êü•ÁúãÁî®Êà∑

-menu.admin.reload=ÈáçËΩΩÈÄâÈ°π

-

-menu.user=ÁºñËæë‰ø°ÊÅØ

-menu.selectFile=‰∏ä‰º†Êñá‰ª∂

-menu.flushCache=Âà∑Êñ∞ÁºìÂ≠ò

-menu.clickstream=ËÆøÈóÆËÆ∞ÂΩï

-

-# -- form labels --

-label.username=Áî®Êà∑Âêç

-label.password=ÂØÜÁ†Å

-

-# -- button labels --

-button.add=Ê∑ªÂä†

-button.cancel=ÂèñÊ∂à

-button.copy=Â§çÂà∂

-button.delete=Âà†Èô§

-button.done=ÂÅö

-button.edit=ÁºñËæë

-button.register=Ê≥®ÂÜå

-button.save=‰øùÂ≠ò

-button.search=ÊêúÁ¥¢

-button.upload=‰∏ä‰º†

-button.view=Êü•Áúã

-button.reset=Â§ç‰Ωç

-button.login=ÁôªÂΩï

-

-# -- general values --

-icon.information=‰ø°ÊÅØ

-icon.information.img=/images/iconInformation.gif

-icon.email=E-Mail

-icon.email.img=/images/iconEmail.gif

-icon.warning=Ë≠¶Âëä

-icon.warning.img=/images/iconWarning.gif

-date.format=MM/dd/yyyy

-

-# -- role form --

-roleForm.name=ÂêçÁß∞

-

-# -- user profile page --

-userProfile.title=Áî®Êà∑ËÆæÁΩÆ

-userProfile.heading=Áî®Êà∑ÁÆÄË¶Å‰ø°ÊÅØ

-userProfile.message=ËØ∑ÊåâÂ¶Ç‰∏ãË°®Ê†ºÊõ¥Êñ∞ÊÇ®ÁöÑ‰ø°ÊÅØ„ÄÇ

-userProfile.admin.message=ÊÇ®ÂèØ‰ª•ÊåâÂ¶Ç‰∏ãË°®Ê†ºÔºåÊõ¥Êñ∞Áî®Êà∑ÁöÑ‰ø°ÊÅØ„ÄÇ

-userProfile.showMore=Êü•ÁúãÊõ¥Â§ö‰ø°ÊÅØ

-userProfile.accountSettings=Â∏êÊà∑ËÆæÁΩÆ

-userProfile.assignRoles=ÂàÜÈÖçËßíËâ≤

-userProfile.cookieLogin=ÊÇ®Êó†Ê≥ïÊõ¥ÊîπÂØÜÁ†ÅÔºåÂõ†‰∏∫ÊÇ®ÈÄâÊã©‰∫Ü <strong>ËÆ©Á≥ªÁªüËÆ∞‰ΩèÊàë</strong> ÈÄâÈ°π„ÄÇËØ∑ÈÄÄÂá∫Á≥ªÁªüÔºåÂÜçÊ¨°ÁôªÂΩïÂ∞ùËØïÊõ¥ÊîπÂØÜÁ†Å„ÄÇ

-

-# -- user form --

-user.address.address=Âú∞ÂùÄ

-user.availableRoles=ÂèØÁî®ËßíËâ≤

-user.address.city=ÂüéÂ∏Ç

-user.address.country=ÂõΩÂÆ∂

-user.email=E-Mail

-user.firstName=Âêç

-user.id=Id

-user.lastName=Âßì

-user.password=ÂØÜÁ†Å

-user.confirmPassword=Á°ÆËÆ§ÂØÜÁ†Å

-user.phoneNumber=ÁîµËØù

-user.address.postalCode=ÈÇÆÁºñ

-user.address.province=Â∑ûÁúÅ

-user.roles=ÂΩìÂâçËßíËâ≤

-user.username=Áî®Êà∑Âêç

-user.website=ÁΩëÂùÄ

-user.visitWebsite=ÊâìÂºÄ

-user.passwordHint=ÂØÜÁ†ÅÊèêÁ§∫

-user.enabled=‰ΩøËÉΩ

-user.accountExpired=Âà∞Êúü

-user.accountLocked=ÈîÅÁùÄ

-user.credentialsExpired=ÂØÜÁ†ÅÂà∞Êúü‰∫Ü

-

-# -- user list page --

-userList.title=Áî®Êà∑ÂàóË°®

-userList.heading=Âú®Á∫øÁî®Êà∑

-userList.nousers=<span>Ê≤°ÊâæÂà∞Áî®Êà∑„ÄÇ</span>

-

-# -- user self-registration --

-signup.title=Ê≥®ÂÜå

-signup.heading=Êñ∞Áî®Êà∑Ê≥®ÂÜå

-signup.message=ËØ∑ËæìÂÖ•Áî®Êà∑‰ø°ÊÅØ„ÄÇ

-signup.email.subject=AppFuse Â∏êÊà∑‰ø°ÊÅØ

-signup.email.message=ÊÇ®Â∑≤ÊàêÂäüÊ≥®ÂÜåÂà∞ AppFuse„ÄÇÊÇ®ÁöÑÁî®Êà∑ÂêçÂíåÂØÜÁ†Å‰ø°ÊÅØÂ¶Ç‰∏ãÔºö

-

-# -- upload page messages --

-maxLengthExceeded=ÈÄâÊã©‰∏ä‰º†ÁöÑÊñá‰ª∂ËøáÂ§ß„ÄÇÊúÄÂ§ßÂÖÅËÆ∏ÂÄº‰∏∫ 2 MB„ÄÇ

-upload.title=Êñá‰ª∂‰∏ä‰º†

-upload.heading=‰∏ä‰º†‰∏ÄÊñá‰ª∂

-upload.message=‰∏ªË¶ÅÁ≥ªÁªüÂÖÅËÆ∏‰∏ä‰º†Êñá‰ª∂ÁöÑÊúÄÂ§ßÂÄº‰∏∫ 2 MB„ÄÇ

-uploadForm.name=ÈáçÂëΩÂêçÊñá‰ª∂

-uploadForm.file=ÈÄâÊã©Êñá‰ª∂

-

-# -- display page messages -- 

-display.title=Êñá‰ª∂‰∏ä‰º†ÊàêÂäüÔºÅ

-display.heading=Êñá‰ª∂‰ø°ÊÅØ

-

-# -- flushCache page --

-flushCache.title=Âà∑Êñ∞ÁºìÂ≠ò

-flushCache.heading=Âà∑Êñ∞ÊàêÂäüÔºÅ

-flushCache.message=ÊâÄÊúâÁºìÂ≠òÊàêÂäüÂà∑Êñ∞Ôºå2 Áßí‰πãÂêéÔºåÁ≥ªÁªüËá™Âä®ËøîÂõûÂà∞ÂâçÈù¢ÁöÑÈ°µÈù¢„ÄÇ

-

-# -- clickstreams page --

-clickstreams.title=ÊâÄÊúâËÆøÈóÆËÆ∞ÂΩï

-clickstreams.heading=ÊâÄÊúâËÆøÈóÆËÆ∞ÂΩï

-

-# -- viewstream page --

-viewstream.title=ËÆøÈóÆËÆ∞ÂΩïËØ¶ÁªÜ

-viewstream.heading=ËÆøÈóÆËÆ∞ÂΩï‰ø°ÊÅØ

-

-# -- active users page --

-activeUsers.title=Ê¥ªÂä®Áî®Êà∑ÂàóË°®

-activeUsers.heading=Âú®Á∫øÁî®Êà∑

-activeUsers.message=ÂàóË°®‰∏∫Â∑≤ÊàêÂäüÁôªÂΩïÁöÑ„ÄÅsession‰∏∫ËøáÊúüÁöÑÁî®Êà∑„ÄÇ

-activeUsers.fullName=ÂÖ®Âêç

-

-# JSF-only messages, remove if not using JSF

-javax.faces.component.UIInput.REQUIRED={0} ‰∏∫ÂøÖÂ°´È°π„ÄÇ

+Ôªø
+user.status=ÂΩìÂâçÁî®Êà∑: 
+user.logout=ÈÄÄÂá∫
+
+# -- validator errors --
+errors.invalid={0} Êó†Êïà„ÄÇ
+errors.maxlength={0} ‰∏çËÉΩÂ§ß‰∫é {1} ‰∏™Â≠óÁ¨¶„ÄÇ
+errors.minlength={0} ‰∏çËÉΩÂ∞ë‰∫é {1} ‰∏™Â≠óÁ¨¶„ÄÇ
+errors.range={0} Êú™Âú® {1} ‰∏é {2} ËåÉÂõ¥ÂÜÖ„ÄÇ
+errors.required={0} ‰∏∫ÂøÖÂ°´È°π„ÄÇ
+errors.byte={0} ÂøÖÈ°ª‰∏∫byteÁ±ªÂûã„ÄÇ
+errors.date={0} ‰∏çÊòØÊúâÊïàÊó•ÊúüÊ†ºÂºè„ÄÇ
+errors.double={0} ÂøÖÈ°ª‰∏∫doubleÁ±ªÂûã„ÄÇ
+errors.float={0} ÂøÖÈ°ª‰∏∫floatÁ±ªÂûã„ÄÇ
+errors.integer={0} ÂøÖÈ°ª‰∏∫‰∏ÄÊï∞ÂÄº„ÄÇ
+errors.long={0} ÂøÖÈ°ª‰∏∫longÁ±ªÂûã„ÄÇ
+errors.short={0} ÂøÖÈ°ª‰∏∫shortÁ±ªÂûã„ÄÇ
+errors.creditcard={0} ‰∏∫Êó†Êïà‰ø°Áî®Âç°Âè∑„ÄÇ
+errors.email={0} ‰∏∫Êó†ÊïàÈÇÆ‰ª∂Âú∞ÂùÄ„ÄÇ
+errors.phone={0} ‰∏∫Êó†ÊïàÁîµËØùÂè∑Á†Å„ÄÇ
+errors.zip={0} ‰∏∫Êó†ÊïàÈÇÆÊîøÁºñÁ†Å„ÄÇ
+
+# -- other errors --
+errors.cancel=Êìç‰ΩúË¢´ÂèñÊ∂à„ÄÇ
+errors.detail={0}
+errors.general=Êìç‰ΩúÊú™ÂÆåÊàê„ÄÇËØ¶ÁªÜÂéüÂõ†Â¶Ç‰∏ã„ÄÇ
+errors.token=ËØ∑Ê±ÇÊú™ÂÆåÂÖ®Â§ÑÁêÜ„ÄÇÊìç‰ΩúÈ°∫Â∫èÈîôËØØ„ÄÇ
+errors.none=Êó†ÈîôËØØÊ∂àÊÅØÔºåËØ∑Ê£ÄÊü•ÊúçÂä°Âô®Êó•ÂøóÊñá‰ª∂„ÄÇ
+errors.password.mismatch=Êó†ÊïàÁî®Êà∑ÂêçÊàñÂØÜÁ†ÅÔºåËØ∑ÈáçËØï„ÄÇ
+errors.conversion=Âú®webÂ±ÇÊï∞ÊçÆÂà∞‰∏öÂä°Â±ÇÊï∞ÊçÆÁöÑËΩ¨Êç¢ËøáÁ®ã‰∏≠ÔºåÂèëÁîü‰∫Ü‰∏Ä‰∏™ÈîôËØØ„ÄÇ
+errors.twofields={0} Â≠óÊÆµ‰∏é {1} Â≠óÊÆµÁöÑÂÄºÂøÖÈ°ª‰∏ÄËá¥„ÄÇ
+errors.existing.user=Áî®Êà∑Âêç ({0}) Êàñe-mailÂú∞ÂùÄ ({1}) Â∑≤Â≠òÂú®„ÄÇËØ∑ÂÜçÊ¨°Â∞ùËØï‰∏çÂêåÂêçÁß∞„ÄÇ
+
+# -- success messages --
+user.added=Áî®Êà∑ {0} ÁöÑ‰ø°ÊÅØÊ∑ªÂä†ÊàêÂäü„ÄÇ
+user.deleted=Áî®Êà∑ {0} ÁöÑ‰ø°ÊÅØÂà†Èô§ÊàêÂäü„ÄÇ
+user.registered=Ê≥®ÂÜåÊàêÂäüÔºåÊÇ®ÂèØ‰ª•ÂºÄÂßã‰ΩøÁî®Á≥ªÁªü„ÄÇ
+user.saved=ÊÇ®ÁöÑ‰ø°ÊÅØÂ∑≤ÊàêÂäüÊõ¥Êñ∞„ÄÇ
+user.updated.byAdmin=Áî®Êà∑ {0} ÁöÑ‰ø°ÊÅØÂ∑≤ÊàêÂäüÊõ¥Êñ∞„ÄÇ
+newuser.email.message={0} ‰∏∫ÊÇ®ÊàêÂäüÂàõÂª∫‰∫Ü‰∏Ä‰∏™AppFuseÂ∏êÂè∑„ÄÇÊÇ®ÁöÑÁî®Êà∑ÂêçÂíåÂØÜÁ†Å‰ø°ÊÅØÂ¶Ç‰∏ãÔºö
+reload.succeeded=Â∑≤ÁªèÊàêÂäüÈáçËΩΩ.
+
+# -- error page messages --
+errorPage.title=Á≥ªÁªüÈîôËØØ
+errorPage.heading=Âì¶ÔºÅ
+404.title=È°µÈù¢Êú™ÊâæÂà∞
+404.message=ËØ∑Ê±ÇÁöÑÈ°µÈù¢Êú™ÊâæÂà∞„ÄÇÊÇ®ÂèØ‰ª•ÈÄâÊã©ËøîÂõûÂà∞ <a href="{0}">‰∏ªËèúÂçï</a>„ÄÇÊàñËÄÖÈÄâÊã©Âú®Ê≠§‰ºëÊÅØ‰∏Ä‰∏ãÔºåÂøòÊéâÂàöÊâçÁöÑÊ≤Æ‰∏ßÔºåÊ¨£Ëµè‰∏Ä‰∏™Áæé‰∏ΩÁöÑÂõæÁâáÔºü
+403.title=ËÆøÈóÆË¢´ÊãíÁªù
+403.message=ÊÇ®ÂΩìÂâçËßíËâ≤Êó†ÊùÉÈôêÊü•ÁúãÊ≠§È°µÈù¢„ÄÇËØ∑ËÅîÁ≥ªÁ≥ªÁªüÁÆ°ÁêÜÂëòÔºåËé∑ÂæóÁõ∏Â∫îÁöÑÊùÉÈôê„ÄÇÊ≠§ÂàªÔºåËÆ©Êàë‰ª¨Ê¨£Ëµè‰∏Ä‰∏™ÂõæÁâáÔºåÊîæÊùæ‰∏Ä‰∏ãÂ•ΩÂêßÔºü
+
+# -- login --
+login.title=ÁôªÂΩï
+login.heading=ÁôªÂΩï
+login.rememberMe=ËÆ©Á≥ªÁªüËÆ∞‰ΩèÊàë
+login.signup=‰∏çÊòØÊ≥®ÂÜåÁî®Êà∑? <a href="{0}">Áî≥ËØ∑</a> ‰∏Ä‰∏™Â∏êÂè∑„ÄÇ
+login.passwordHint=ÂøòËÆ∞‰∫ÜÂØÜÁ†Å?  ËÆ©Á≥ªÁªüÂ∞Ü <a href="?" onmouseover="window.status='Á≥ªÁªüÂèëÈÄÅÂØÜÁ†ÅÊèêÁ§∫„ÄÇ'; return true" onmouseout="window.status=''; return true" title="Á≥ªÁªüÂèëÈÄÅÂØÜÁ†ÅÊèêÁ§∫„ÄÇ" onclick="passwordHint(); return false">ÂØÜÁ†ÅÊèêÁ§∫‰ø°ÊÅØÂ∑≤e-mailÂΩ¢ÂºèÂèëÈÄÅÁªôÊÇ®</a>„ÄÇ
+login.passwordHint.sent={0}</strong> ÁöÑÂØÜÁ†ÅÊèêÁ§∫Â∑≤ÊàêÂäüÂèëÈÄÅÂà∞ {1}„ÄÇ
+login.passwordHint.error=Áî®Êà∑Âêç {0} Âú®Á≥ªÁªüÊï∞ÊçÆÂ∫ì‰∏≠Êú™ÊâæÂà∞„ÄÇ
+
+# -- mainMenu --
+mainMenu.title=‰∏ªËèúÂçï
+mainMenu.heading=Ê¨¢ËøéÔºÅ
+mainMenu.message=ÊÅ≠ÂñúÔºåÊÇ®ÁôªÂΩïÊàêÂäüÔºÅÊÇ®ÂèØ‰ª•ÈÄâÊã©ÊâßË°å‰ª•‰∏ãÊìç‰ΩúÔºö
+mainMenu.activeUsers=Âú®Á∫øÁî®Êà∑
+
+# -- menu/link messages --
+menu.admin=Á≥ªÁªüÁÆ°ÁêÜ
+menu.admin.users=Êü•ÁúãÁî®Êà∑
+menu.admin.reload=ÈáçËΩΩÈÄâÈ°π
+
+menu.user=ÁºñËæë‰ø°ÊÅØ
+menu.selectFile=‰∏ä‰º†Êñá‰ª∂
+menu.flushCache=Âà∑Êñ∞ÁºìÂ≠ò
+menu.clickstream=ËÆøÈóÆËÆ∞ÂΩï
+
+# -- form labels --
+label.username=Áî®Êà∑Âêç
+label.password=ÂØÜÁ†Å
+
+# -- button labels --
+button.add=Ê∑ªÂä†
+button.cancel=ÂèñÊ∂à
+button.copy=Â§çÂà∂
+button.delete=Âà†Èô§
+button.done=ÂÅö
+button.edit=ÁºñËæë
+button.register=Ê≥®ÂÜå
+button.save=‰øùÂ≠ò
+button.search=ÊêúÁ¥¢
+button.upload=‰∏ä‰º†
+button.view=Êü•Áúã
+button.reset=Â§ç‰Ωç
+button.login=ÁôªÂΩï
+
+# -- general values --
+icon.information=‰ø°ÊÅØ
+icon.information.img=/images/iconInformation.gif
+icon.email=E-Mail
+icon.email.img=/images/iconEmail.gif
+icon.warning=Ë≠¶Âëä
+icon.warning.img=/images/iconWarning.gif
+date.format=MM/dd/yyyy
+
+# -- role form --
+roleForm.name=ÂêçÁß∞
+
+# -- user profile page --
+userProfile.title=Áî®Êà∑ËÆæÁΩÆ
+userProfile.heading=Áî®Êà∑ÁÆÄË¶Å‰ø°ÊÅØ
+userProfile.message=ËØ∑ÊåâÂ¶Ç‰∏ãË°®Ê†ºÊõ¥Êñ∞ÊÇ®ÁöÑ‰ø°ÊÅØ„ÄÇ
+userProfile.admin.message=ÊÇ®ÂèØ‰ª•ÊåâÂ¶Ç‰∏ãË°®Ê†ºÔºåÊõ¥Êñ∞Áî®Êà∑ÁöÑ‰ø°ÊÅØ„ÄÇ
+userProfile.showMore=Êü•ÁúãÊõ¥Â§ö‰ø°ÊÅØ
+userProfile.accountSettings=Â∏êÊà∑ËÆæÁΩÆ
+userProfile.assignRoles=ÂàÜÈÖçËßíËâ≤
+userProfile.cookieLogin=ÊÇ®Êó†Ê≥ïÊõ¥ÊîπÂØÜÁ†ÅÔºåÂõ†‰∏∫ÊÇ®ÈÄâÊã©‰∫Ü <strong>ËÆ©Á≥ªÁªüËÆ∞‰ΩèÊàë</strong> ÈÄâÈ°π„ÄÇËØ∑ÈÄÄÂá∫Á≥ªÁªüÔºåÂÜçÊ¨°ÁôªÂΩïÂ∞ùËØïÊõ¥ÊîπÂØÜÁ†Å„ÄÇ
+
+# -- user form --
+user.address.address=Âú∞ÂùÄ
+user.availableRoles=ÂèØÁî®ËßíËâ≤
+user.address.city=ÂüéÂ∏Ç
+user.address.country=ÂõΩÂÆ∂
+user.email=E-Mail
+user.firstName=Âêç
+user.id=Id
+user.lastName=Âßì
+user.password=ÂØÜÁ†Å
+user.confirmPassword=Á°ÆËÆ§ÂØÜÁ†Å
+user.phoneNumber=ÁîµËØù
+user.address.postalCode=ÈÇÆÁºñ
+user.address.province=Â∑ûÁúÅ
+user.roles=ÂΩìÂâçËßíËâ≤
+user.username=Áî®Êà∑Âêç
+user.website=ÁΩëÂùÄ
+user.visitWebsite=ÊâìÂºÄ
+user.passwordHint=ÂØÜÁ†ÅÊèêÁ§∫
+user.enabled=‰ΩøËÉΩ
+user.accountExpired=Âà∞Êúü
+user.accountLocked=ÈîÅÁùÄ
+user.credentialsExpired=ÂØÜÁ†ÅÂà∞Êúü‰∫Ü
+
+# -- user list page --
+userList.title=Áî®Êà∑ÂàóË°®
+userList.heading=Âú®Á∫øÁî®Êà∑
+userList.nousers=<span>Ê≤°ÊâæÂà∞Áî®Êà∑„ÄÇ</span>
+
+# -- user self-registration --
+signup.title=Ê≥®ÂÜå
+signup.heading=Êñ∞Áî®Êà∑Ê≥®ÂÜå
+signup.message=ËØ∑ËæìÂÖ•Áî®Êà∑‰ø°ÊÅØ„ÄÇ
+signup.email.subject=AppFuse Â∏êÊà∑‰ø°ÊÅØ
+signup.email.message=ÊÇ®Â∑≤ÊàêÂäüÊ≥®ÂÜåÂà∞ AppFuse„ÄÇÊÇ®ÁöÑÁî®Êà∑ÂêçÂíåÂØÜÁ†Å‰ø°ÊÅØÂ¶Ç‰∏ãÔºö
+
+# -- upload page messages --
+maxLengthExceeded=ÈÄâÊã©‰∏ä‰º†ÁöÑÊñá‰ª∂ËøáÂ§ß„ÄÇÊúÄÂ§ßÂÖÅËÆ∏ÂÄº‰∏∫ 2 MB„ÄÇ
+upload.title=Êñá‰ª∂‰∏ä‰º†
+upload.heading=‰∏ä‰º†‰∏ÄÊñá‰ª∂
+upload.message=‰∏ªË¶ÅÁ≥ªÁªüÂÖÅËÆ∏‰∏ä‰º†Êñá‰ª∂ÁöÑÊúÄÂ§ßÂÄº‰∏∫ 2 MB„ÄÇ
+uploadForm.name=ÈáçÂëΩÂêçÊñá‰ª∂
+uploadForm.file=ÈÄâÊã©Êñá‰ª∂
+
+# -- display page messages -- 
+display.title=Êñá‰ª∂‰∏ä‰º†ÊàêÂäüÔºÅ
+display.heading=Êñá‰ª∂‰ø°ÊÅØ
+
+# -- flushCache page --
+flushCache.title=Âà∑Êñ∞ÁºìÂ≠ò
+flushCache.heading=Âà∑Êñ∞ÊàêÂäüÔºÅ
+flushCache.message=ÊâÄÊúâÁºìÂ≠òÊàêÂäüÂà∑Êñ∞Ôºå2 Áßí‰πãÂêéÔºåÁ≥ªÁªüËá™Âä®ËøîÂõûÂà∞ÂâçÈù¢ÁöÑÈ°µÈù¢„ÄÇ
+
+# -- clickstreams page --
+clickstreams.title=ÊâÄÊúâËÆøÈóÆËÆ∞ÂΩï
+clickstreams.heading=ÊâÄÊúâËÆøÈóÆËÆ∞ÂΩï
+
+# -- viewstream page --
+viewstream.title=ËÆøÈóÆËÆ∞ÂΩïËØ¶ÁªÜ
+viewstream.heading=ËÆøÈóÆËÆ∞ÂΩï‰ø°ÊÅØ
+
+# -- active users page --
+activeUsers.title=Ê¥ªÂä®Áî®Êà∑ÂàóË°®
+activeUsers.heading=Âú®Á∫øÁî®Êà∑
+activeUsers.message=ÂàóË°®‰∏∫Â∑≤ÊàêÂäüÁôªÂΩïÁöÑ„ÄÅsession‰∏∫ËøáÊúüÁöÑÁî®Êà∑„ÄÇ
+activeUsers.fullName=ÂÖ®Âêç
+
+# JSF-only messages, remove if not using JSF
+javax.faces.component.UIInput.REQUIRED={0} ‰∏∫ÂøÖÂ°´È°π„ÄÇ
 activeUsers.summary=ÊâæÂà∞ {0} ‰∏™Áî®Êà∑ÔºåÊòæÁ§∫ {1} ‰∏™Áî®Êà∑Ôºå‰ªé {2} Âà∞ {3}„ÄÇ {4} / {5} È°µ
\ No newline at end of file
Index: src/main/resources/ApplicationResources_pt.properties
===================================================================
--- src/main/resources/ApplicationResources_pt.properties	(revision 85)
+++ src/main/resources/ApplicationResources_pt.properties	(working copy)
@@ -1,184 +1,192 @@
-user.status=Registrado como: 

-user.logout=Sair

-

-# -- validator errors --

-errors.invalid={0} È inv·lido.

-errors.maxlength={0} n„o pode ser maior que {1} caracter(es).

-errors.minlength={0} n„o pode ser menos que {1} caracter(es).

-errors.range={0} n„o est· na escala {1} a {2}.

-errors.required={0} È um campo obrigatÛrio.

-errors.byte={0} deve ser um byte.

-errors.date={0} n„o È uma data.

-errors.double={0} deve ser double.

-errors.float={0} deve ser um float.

-errors.integer={0} deve ser um number.

-errors.long={0} deve ser um long.

-errors.short={0} deve ser um short.

-errors.creditcard={0} n„o È um n˙mero de cart„o de crÈdito v·lido.

-errors.email={0} È um endereÁo de e-mail inv·lido.

-errors.phone={0} È n˙mero de telefone inv·lido.

-errors.zip={0} È um cÛdigo postal inv·lido.

-

-# -- other errors --

-errors.cancel=OperaÁ„o cancelada.

-errors.detail={0}

-errors.general=<strong>O processo n„o completou. Os detalhes devem seguir.</strong>

-errors.token=RequisiÁ„o n„o poderia ser completada. A operaÁ„o n„o est· em ordem.

-errors.none=Nenhuma mensagem de erro foi encontrada, verifica seus registros do servidor.

-errors.password.mismatch=Nome do usu·rio ou senha inv·lido, por favor tente novamente.

-errors.conversion=Um erro ocorreu ao converter valores web para valores de dados.

-errors.twofields=O campo {0} tem que ter o mesmo valor que o campo {1}.

-errors.existing.user=Este nome de usu·rio ({0}) ou endereÁo de e-mail ({1}) j· existe.  Por favor tente um nome de usu·rio diferente.

-

-# -- success messages --

-user.added=InformaÁ„o de Usu·rio para <strong>{0}</strong> foi adicionada com sucesso.

-user.deleted=Perfil de Usu·rio para <strong>{0}</strong> foi deletada com sucesso. 

-user.registered=VocÍ registou com sucesso para o acesso a esta aplicaÁ„o.

-user.saved=Seu perfil foi atualizado com sucesso.

-user.updated.byAdmin=InformaÁ„o de Usu·rio para <strong>{0}</strong> foi atualizada com sucesso.

-newuser.email.message={0} criou uma conta AppFuse para vocÍ.  Sua informaÁ„o nome de usu·rio e senha est· logo abaixo.

-reload.succeeded=AtualizaÁ„o das opÁıes realizada com sucesso.

-

-# -- error page messages --

-errorPage.title=Um erro ocorreu

-errorPage.heading=Yikes!

-404.title=P·gina n„o encontrada

-404.message=A p·gina que vocÍ requisitou n„o foi encontrada.  VocÍ pode tentar retornar para <a href="{0}">Main Menu</a>.Enquanto vocÍ est· aqui, que tal uma linda figura para anim·-lo?

-403.title=Acesso Negado

-403.message=Seu corrente perfil n„o permite a vocÍ a visualizaÁ„o desta p·gina. Por favor entrar em contato com seu administrador de sistemas se vocÍ acredita que deveria ter acesso.  Nesse meio tempo, que tal uma linda figura para anim·-lo?

-

-# -- login --

-login.title=Registrar

-login.heading=Registrar

-login.rememberMe=Lembre-me

-login.signup=N„o È um membro? <a href="{0}">Registre-se</a> para uma conta.

-login.passwordHint=Esqueceu sua senha? Tenha <a href="?" onmouseover="window.status='Tenha sua dica de senha enviada a vocÍ.'; return true" onmouseout="window.status=''; return true" title="Tenha sua dica de senha enviada a vocÍ." onclick="passwordHint(); return false">sua dica de senha enviada a vocÍ</a>.

-login.passwordHint.sent=A dica de senha para <strong>{0}</strong> foi enviada para <strong>{1}</strong>.

-login.passwordHint.error=O nome de usu·rio <strong>{0}</strong> n„o foi encontrado no banco de dados.

-

-# -- mainMenu --

-mainMenu.title=Menu Principal

-mainMenu.heading=Bem vindo!

-mainMenu.message=Parabens, registro efetuado com sucesso!  Agora que vocÍ est· registrado, vocÍ tem as seguintes opÁıes:

-mainMenu.activeUsers=Usu·rios Registrados

-

-# -- menu/link messages --

-menu.admin=AdministraÁ„o

-menu.admin.users=Visualizar Usu·rios

-menu.admin.reload=Atualizar OpÁıes

-menu.user=Editar Perfil

-menu.selectFile=Carregar um arquivo

-menu.flushCache=Liberar Cache

-menu.clickstream=Clickstream

-

-# -- form labels --

-label.username=Nome de Usu·rio

-label.password=Senha

-

-# -- button labels --

-button.add=Adicionar

-button.cancel=Cancelar

-button.copy=Copiar

-button.delete=Deletar

-button.done=Feito

-button.edit=Editar

-button.register=Registre-se

-button.save=Salvar

-button.search=Pesquisar

-button.upload=Carregar

-button.view=Visualizar

-button.reset=Limpar

-button.login=Entrar

-

-# -- general values --

-icon.information=InformaÁ„o

-icon.information.img=/images/iconInformation.gif

-icon.email=E-Mail

-icon.email.img=/images/iconEmail.gif

-icon.warning=AtenÁ„o

-icon.warning.img=/images/iconWarning.gif

-date.format=MM/dd/yyyy

-

-# -- role form --

-roleForm.name=Nome

-

-# -- user profile page --

-userProfile.title=ConfiguraÁıes de Usu·rio

-userProfile.heading=Perfil de Usu·rio

-userProfile.message=Por favor atualize sua imformaÁ„o usando o formul·rio abaixo.

-userProfile.admin.message=VocÍ pode atualizar a imformaÁ„o deste usu·rio no formul·rio abaixo.

-userProfile.showMore=Veja Mais Informações

-userProfile.accountSettings=Configurações da Conta

-userProfile.assignRoles=Atribuir Perfis

-userProfile.cookieLogin=VocÍ n„o pode alter senhas quando registrado com a caracterÌstica<strong>Lembre-me</strong>. Por favor saia e registre novamente para alterar senhas.

-

-# -- user form --

-user.address.address=EndereÁo

-user.availableRoles=Perfis disponÌveis

-user.address.city=Cidade

-user.address.country=PaÌs

-user.email=E-Mail

-user.firstName=Primeiro Nome

-user.id=Id

-user.lastName=Ultimo Nome

-user.password=Senha

-user.confirmPassword=Comfirmar Senha

-user.phoneNumber=Numero Telefone

-user.address.postalCode=CÛdigo Postal

-user.address.province=Estado

-user.roles=Perfis Corrente

-user.username=Nome de Usu·rio

-user.website=Website

-user.visitWebsite=visite

-user.passwordHint=Dica de Senha

-user.enabled=Habilitada

-user.accountExpired=Expirada

-user.accountLocked=Bloqueada

-user.credentialsExpired=Senha Expirada

-

-# -- user list page --

-userList.title=Lista Usu·rio

-userList.heading=Usu·rios Corrente

-userList.nousers=<span>Nenhum usu·rio encontrado.</span>

-

-# -- user self-registration --

-signup.title=Registre-se

-signup.heading=Registro de Novo Usu·rio

-signup.message=Por favor entre com sua informaÁ„o no formul·rio abaixo.

-signup.email.subject=InformaÁ„o de Conta AppFuse

-signup.email.message=VocÍ se registrou com sucesso para acesso a AppFuse.  Sua informaÁ„o nome de usu·rio e senha est· logo abaixo.

-

-# -- upload page messages --

-maxLengthExceeded=O arquivo que vocÍ esta tentando carregar È muito grande.  O m·ximo permitido È 2 MB.

-upload.title=Carregar Arquivo

-upload.heading=Carrega um Arquivo

-upload.message=Observe que o tamanho m·ximo permitido para um arquivo carregado para esta aplicaÁ„o È 2 MB.

-uploadForm.name=Nome Amig·vel 

-uploadForm.file=Arquivo a Carregar

-

-# -- display page messages -- 

-display.title=Arquivo Carregado com Sucesso!

-display.heading=InformÁ„o de Arquivo

-

-# -- flushCache page --

-flushCache.title=Liberar Cache

-flushCache.heading=Chache Liberado com Sucesso!

-flushCache.message=Todos Chaches Liberados com Sucesso, retorno ‡ p·gina anterior em  2 segundos.

-

-# -- clickstreams page --

-clickstreams.title=Todos Clickstreams

-clickstreams.heading=Todos Clickstreams

-

-# -- viewstream page --

-viewstream.title=Stream Detalhes

-viewstream.heading=Stream InformaÁ„o

-

-# -- active users page --

-activeUsers.title=Usu·rios Ativos

-activeUsers.heading=Usu·rios Corrente

-activeUsers.message=O seguinte È uma lista de usu·rios que se registraram e as suas sessıes n„o expiraram.

-activeUsers.fullName=Todo Nome

-

-# JSF-only messages, remove if not using JSF

-javax.faces.component.UIInput.REQUIRED={0} È um campo obrigatÛrio.

-activeUsers.summary={0} Usuário(s) encontrado(s), exibindo {1} usuário(s), de {2} a {3}. Página {4} / {5}
\ No newline at end of file
+Ôªø
+user.status=Registrado como: 
+user.logout=Sair
+
+# -- validator errors --
+errors.invalid={0} √© inv√°lido.
+errors.maxlength={0} n√£o pode ser maior que {1} caracter(es).
+errors.minlength={0} n√£o pode ser menos que {1} caracter(es).
+errors.range={0} n√£o est√° na escala {1} a {2}.
+errors.required={0} √© um campo obrigat√≥rio.
+errors.byte={0} deve ser um byte.
+errors.date={0} n√£o √© uma data.
+errors.double={0} deve ser double.
+errors.float={0} deve ser um float.
+errors.integer={0} deve ser um number.
+errors.long={0} deve ser um long.
+errors.short={0} deve ser um short.
+errors.creditcard={0} n√£o √© um n√∫mero de cart√£o de cr√©dito v√°lido.
+errors.email={0} √© um endere√ßo de e-mail inv√°lido.
+errors.phone={0} √© n√∫mero de telefone inv√°lido.
+errors.zip={0} √© um c√≥digo postal inv√°lido.
+
+# -- other errors --
+errors.cancel=Opera√ß√£o cancelada.
+errors.detail={0}
+errors.general=O processo n√£o foi conclu√≠do com sucesso. Os detalhes devem seguir.
+errors.token=Requisi√ß√£o n√£o poderia ser completada. A opera√ß√£o n√£o est√° em ordem.
+errors.none=Nenhuma mensagem de erro foi encontrada, verifica seus registros do servidor.
+errors.password.mismatch=Nome do utilizador ou senha inv√°lido, por favor tente novamente.
+errors.conversion=Ocorreu um erro ao converter valores web para valores de dados.
+errors.twofields=O campo {0} tem que ter o mesmo valor que o campo {1}.
+errors.existing.user=Este nome de utilizador ({0}) ou endere√ßo de e-mail ({1}) j√° existe.  Por favor tente um nome de utilizador diferente.
+
+# -- success messages --
+user.added=Informa√ß√£o de utilizador para {0} foi adicionada com sucesso.
+user.deleted=Perfil de utilizador para {0} foi apagada com sucesso.
+user.registered=Acabou de se registar com sucesso para o acesso a esta aplica√ß√£o.
+user.saved=Perfil actualizado com sucesso.
+user.updated.byAdmin=Informa√ß√£o de Utilizador para {0} foi actualizada com sucesso.
+newuser.email.message={0} criou uma conta AppFuse para voc√™.  Sua informa√ß√£o nome de utilizador e senha est√° mencionada mais abaixo.
+reload.succeeded=Actualiza√ß√£o das op√ß√µes realizada com sucesso.
+
+# -- error page messages --
+errorPage.title=Um erro ocorreu
+errorPage.heading=Yikes!
+404.title=P√°gina n√£o encontrada
+404.message=A p√°gina que voc√™ requisitou n√£o foi encontrada.  Voc√™ pode tentar retornar para <a href="{0}">Main Menu</a>.Enquanto voc√™ est√° aqui, que tal uma linda figura para anim√°-lo?
+403.title=Acesso Negado
+403.message=O seu perfil n√£o permite a visualiza√ß√£o desta p√°gina. Por favor entre em contato com seu administrador de sistemas se voc√™ acredita que deveria ter acesso.  No entretanto, que tal uma linda figura para anim√°-lo?
+
+# -- login --
+login.title=Registar
+login.heading=Registar
+login.rememberMe=Lembre-me
+login.signup=N√£o √© um membro? <a href="{0}">Registe-se</a> para uma conta.
+login.passwordHint=Esqueceu sua senha? Tenha <a href="?" onmouseover="window.status='Tenha sua dica de senha enviada a voc√™.'; return true" onmouseout="window.status=''; return true" title="Tenha sua dica de senha enviada a voc√™." onclick="passwordHint(); return false">sua dica de senha enviada a voc√™</a>.
+login.passwordHint.sent=A dica de senha para {0} foi enviada para {1}.
+login.passwordHint.error=O nome de utilizador {0} n√£o consta na base de dados.
+
+# -- mainMenu --
+mainMenu.title=Menu Principal
+mainMenu.heading=Bem vindo!
+mainMenu.message=Parabens, registo efectuado com sucesso!  Agora que est√° registado, tem as seguintes op√ß√µes:
+mainMenu.activeUsers=Utilizadores Registrados
+
+# -- menu/link messages --
+menu.admin=Administra√ß√£o
+menu.admin.users=Visualizar Utilizadores
+menu.admin.reload=Actualizar Op√ß√µes
+menu.user=Editar Perfil
+menu.selectFile=Carregar um ficheiro
+menu.flushCache=Limpar Cache
+menu.clickstream=Clickstream
+
+menu.portorama=Obtenha o software aqui!
+
+# -- form labels --
+label.username=Nome de Utilizador
+label.password=Senha
+
+# -- button labels --
+button.add=Adicionar
+button.cancel=Cancelar
+button.copy=Copiar
+button.delete=Apagar
+button.done=Terminado
+button.edit=Editar
+button.register=Registe-se
+button.save=Guardar
+button.search=Pesquisar
+button.upload=Carregar
+button.view=Visualizar
+button.reset=Limpar
+button.login=Entrar
+
+# -- general values --
+icon.information=Informa√ß√£o
+icon.information.img=/images/iconInformation.gif
+icon.email=E-Mail
+icon.email.img=/images/iconEmail.gif
+icon.warning=Aten√ß√£o
+icon.warning.img=/images/iconWarning.gif
+date.format=MM/dd/yyyy
+
+# -- role form --
+roleForm.name=Nome
+
+# -- user profile page --
+userProfile.title=Configura√ß√µes de Utilizador
+userProfile.heading=Perfil de Utilizador
+userProfile.message=Por favor actualize sua imforma√ß√£o utilizando o formul√°rio abaixo.
+userProfile.admin.message=Pode actualizar a informa√ß√£o deste utilizador no formul√°rio abaixo.
+userProfile.showMore=Veja Mais Informa√ß√µees
+userProfile.accountSettings=Configura√ß√µes da Conta
+userProfile.assignRoles=Atribuir Perfis
+userProfile.cookieLogin=Voc√™ n√£o pode alter senhas quando registado com a caracter√≠stica<strong>Lembre-me</strong>. Por favor saia e registe novamente para alterar senhas.
+
+# -- user form --
+user.address.address=Endere√ßo
+user.availableRoles=Perfis dispon√≠veis
+user.address.city=Cidade
+user.address.country=Pa√≠s
+user.email=E-Mail
+user.firstName=Primeiro Nome
+user.id=Id
+user.lastName=Ultimo Nome
+user.password=Senha
+user.confirmPassword=Comfirmar Senha
+user.phoneNumber=Numero Telefone
+user.address.postalCode=C√≥digo Postal
+user.address.province=Estado
+user.roles=Perfis Corrente
+user.username=Nome de Utilizador
+user.website=Website
+user.visitWebsite=visite
+user.passwordHint=Dica de Senha
+user.enabled=Habilitada
+user.accountExpired=Expirada
+user.accountLocked=Bloqueada
+user.credentialsExpired=Senha Expirada
+
+# Portorama 
+user.snarkport=Porto Peer-to-Peer
+user.rating=Intensidade do Filtro
+
+
+# -- user list page --
+userList.title=Lista Utilizador
+userList.heading=Utilizadores Correntes
+userList.nousers=<span>Nenhum utilizador encontrado.</span>
+
+# -- user self-registration --
+signup.title=Registe-se
+signup.heading=Registo de Novo Utilizador
+signup.message=Por favor insira a sua informa√ß√£o informa√ß√£o no formul√°rio abaixo.
+signup.email.subject=Informa√ß√£o de Conta AppFuse
+signup.email.message=Registou-se com sucesso para acesso a AppFuse. Sua informa√ß√£o: nome de utilizador e senha est√£o mais abaixo.
+
+# -- upload page messages --
+maxLengthExceeded=O arquivo que voc√™ esta a tentar carregar √© muito grande.  O m√°ximo permitido √© 2 MB.
+upload.title=Carregar Arquivo
+upload.heading=Carrega um Arquivo
+upload.message=Note que o tamanho m√°ximo permitido para um arquivo carregado para esta aplica√ß√£o √© 2 MB.
+uploadForm.name=Nome Amig√°vel 
+uploadForm.file=Arquivo a Carregar
+
+# -- display page messages -- 
+display.title=Arquivo Carregado com Sucesso!
+display.heading=Informa√ß√£o de Arquivo
+
+# -- flushCache page --
+flushCache.title=Limpar Cache
+flushCache.heading=Cache Limpa com Sucesso!
+flushCache.message=Todas as Caches Limpas com sucesso, retornando √† p√°gina anterior em  2 segundos.
+
+# -- clickstreams page --
+clickstreams.title=Todos Clickstreams
+clickstreams.heading=Todos Clickstreams
+
+# -- viewstream page --
+viewstream.title=Stream Detalhes
+viewstream.heading=Stream Informa√ß√£o
+
+# -- active users page --
+activeUsers.title=Utilizadores Activos
+activeUsers.heading=Utilizadores Correntes
+activeUsers.message=A seguinte listagem referencia os utilizadores que se registaram e as suas sess√µes n√£o expiraram.
+activeUsers.fullName=Nome Completo
+
+# JSF-only messages, remove if not using JSF
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
@@ -1,182 +1,182 @@
-user.status=Angemeldet als: 

-user.logout=Abmelden

-

-# -- validator errors --

-errors.invalid={0} ist ungültig.

-errors.maxlength={0} muss mindestens {1} Zeichen lang sein.

-errors.minlength={0} darf maximal {1} Zeichen lang sein.

-errors.range={0} ist nicht im Bereich zwischen {1} und {2}.

-errors.required={0} ist ein Pflichtfeld.

-errors.byte={0} muss ein Bytewert sein.

-errors.date={0} ist kein Datumswert.

-errors.double={0} muss ein Wert vom Typ 'double' sein.

-errors.float={0} muss ein Wert vom Typ 'float' sein.

-errors.integer={0} muss eine Zahl sein.

-errors.long={0} muss ein Wert vom Typ 'long' sein.

-errors.short={0} muss ein Wert vom Typ 'short' sein.

-errors.creditcard={0} ist keine gültige Kreditkartennummer.

-errors.email={0} ist eine ungültige E-Mail Adresse.

-errors.phone={0} ist eine ungültige Telefonnummer.

-errors.zip={0} ist eine ungültige Postleitzahl.

-

-# -- other errors --

-errors.cancel=Operation abgebrochen.

-errors.detail={0}

-errors.general=<strong>Der Prozess konnte nicht abgeschlossen werden. Detaillierte Angaben sollten nachfolgend angezeigt werden.</strong>

-errors.token=Anfrage konnte nicht abgeschlossen werden. Die Reihenfolge der Operationen ist nicht korrekt.

-errors.none=Es konnte keine Fehlermeldung gefunden werden, überprüfen sie bitte die Log-Dateien ihres Servers.

-errors.password.mismatch=Ungültiger Benutzername und/oder Passwort, bitte versuchen sie es nochmals.

-errors.browser.warning=<strong>Hinweis:</strong> Der Inhalt dieser Webpräsenz kann von jedem Browser in allen Versionen abgerufen werden. Der von ihnen benutzte Browser unterstützt jedoch möglicherweise grundlegende WWW-Standards nicht, so dass sie eventuell das detaillierte Design unserer Webseite nicht korrekt angezeigt bekommen. Wir unterstützen die <a href="http://www.webstandards.org/upgrade/">Kampagne</a> des Web Standards Projekt, welche die Verbreitung und den Wechsel zu neueren Browserversionen zum Ziel hat.

-errors.conversion=Bei der Konvertierung von Webwerten zu Datenwerten ist ein Fehler aufgetreten.

-errors.twofields=Das Feld {0} muss denselben Wert wie das Feld {1} aufweisen.

-errors.existing.user=Diese Benutzername ({0}) oder diese E-Mail Adresse ({1}) existiert bereits.  Bitte versuchen sie es mit einem anderen Benutzernamen.

-

-# -- success messages --

-user.added=Informationen für Benutzer <strong>{0}</strong> wurden erfolgreich hinzugefügt.

-user.deleted=Benutzerprofil für <strong>{0}</strong> wurde erfolgreich gelöscht. 

-user.registered=Sie haben sich erfolgreich registriert.

-user.saved=Ihr Profil wurde erfolgreich aktualisiert.

-user.updated.byAdmin=Die Informationen für Benutzer <strong>{0}</strong> wurden erfolgreich aktualisiert.

-newuser.email.message={0} hat ein Konto bei AppFuse für sie angelegt. Informationen zu ihrem Benutzernamen und ihrem Passwort finden sie nachfolgend.

-reload.succeeded=Das erneute Laden der Optionen wurde erfolgreich abgeschlossen.

-

-# -- error page messages --

-errorPage.title=Ein Fehler ist aufgetreten

-errorPage.heading=Sapperlott!

-404.title=Seite konnte nicht gefunden werden

-404.message=Die von ihnen angeforderte Seite konnte nicht gefunden werden. Sie können versuchen wieder zum <a href="{0}">Hauptmenü</a> zurückzukehren. Wenn sie schon hier gelandet sind, wie wär&#39;s mit einem hübschen Bild zur Aufmunterung?

-403.title=Zugang nicht gestattet

-403.message=Ihre derzeitiger Benutzerstatus erlaubt es nicht, diese Seite anzuzeigen.  Bitte nehmen sie Kontakt mit ihrem Systemadministrator auf falls sie glauben, dass ihnen der Zugang gestattet sein sollte. Wie wär&#39;s zwischenzeitlich mit einem hübschen Bild zur Aufmunterung?

-

-# -- login --

-login.title=Anmeldung

-login.heading=Anmeldung

-login.rememberMe=Daten behalten

-login.signup=Kein Mitglied? <a href="{0}">Anmeldung</a> für ein Benutzerkonto.

-login.passwordHint=Haben sie ihr Passwort vergessen?  Lassen sie sich per E-Mail einen <a href="?" onmouseover="window.status='Lassen sie sich einen Hinweis auf ihr Passwort zusenden.'; return true" onmouseout="window.status=''; return true" title="Lassen sie sich einen Hinweis auf ihr Passwort zusenden." onclick="passwordHint(); return false">Hinweis auf ihr Passwort</a> zusenden.

-login.passwordHint.sent=Ein Passwordhinweis für <strong>{0}</strong> wurde an <strong>{1}</strong> gesendet.

-login.passwordHint.error=Der Benutzername <strong>{0}</strong> konnte nicht in der Datenbank gefunden werden.

-

-# -- mainMenu --

-mainMenu.title=Hauptmenü

-mainMenu.heading=Willkommen!

-mainMenu.message=Gratulation, sie haben sich erfolgreich angemeldet!  Als angemeldeter Benutzer haben sie folgende Möglichkeiten:

-mainMenu.activeUsers=Derzeitige Benutzer

-

-# -- menu/link messages --

-menu.admin=Administration

-menu.admin.users=Zeige Benutzer an

-menu.admin.reload=Optionen neu laden

-

-menu.user=Benutzerprofil bearbeiten

-menu.selectFile=Datei hochladen

-menu.flushCache=Cache leeren

-menu.clickstream=Clickstream

-

-# -- form labels --

-label.username=Benutzer

-label.password=Passwort

-

-# -- button labels --

-button.add=Hinzufügen

-button.cancel=Abbrechen

-button.copy=Kopieren

-button.delete=Löschen

-button.done=Getan

-button.edit=Bearbeiten

-button.register=Registrieren

-button.save=Speichern

-button.search=Suchen

-button.upload=Hochladen

-button.view=Anzeigen

-button.reset=Zurücksetzen

-button.login=Anmelden

-

-# -- general values --

-icon.information=Information

-icon.information.img=/images/iconInformation.gif

-icon.email=E-Mail

-icon.email.img=/images/iconEmail.gif

-icon.warning=Warnung

-icon.warning.img=/images/iconWarning.gif

-date.format=dd.MM.yyyy

-

-# -- role form --

-roleForm.name=Name

-

-# -- user profile page --

-userProfile.title=Benutzereinstellungen

-userProfile.heading=Benutzerprofil

-userProfile.message=Bitte aktualisieren sie ihre Daten im nachfolgenden Formular.

-userProfile.admin.message=Sie können die Daten dieses Benutzers im nachfolgenden Formular aktualisierenönnen die Daten dieses Benutzers im nachfolgenden Formular aktualisieren.

-userProfile.showMore=Weitere Informationen

-userProfile.assignRoles=Benutzerstatus zuweisen

-userProfile.cookieLogin= Sie können ihr Passwort nicht ändern, wenn sie bei der Anmeldung die Option <strong>Daten behalten</strong> ausgewählt haben.  Bitte melden sie sich zunächst ab und dann erneut an, um ihr Passwort ändern zu können.

-

-# -- user form --

-user.addressForm.address=Adresse

-user.availableRoles=Verfügbare Benutzerrollen

-user.addressForm.city=Stadt

-user.addressForm.country=Land

-user.email=E-Mail

-user.firstName=Vorname

-user.id=ID

-user.lastName=Nachname

-user.password=Passwort

-user.confirmPassword=Passwort bestätigen

-user.phoneNumber=Telefon

-user.addressForm.postalCode=Postleitzahl

-user.addressForm.province=Bundesland

-user.roles=Derzeitige Benutzerrollen

-user.username=Benutzername

-user.website=Website

-user.visitWebsite=Besuchen

-user.passwordHint=Hinweis auf Passwort

-user.enabled=Freigeschaltet

-

-# -- user list page --

-userList.title=Benutzerliste

-userList.heading=Derzeitige Benutzer

-userList.nousers=<span>Keine Benutzer gefunden.</span>

-

-# -- user self-registration --

-signup.title=Anmeldung

-signup.heading=Registrierung als neuer Benutzer

-signup.message=Bitte geben sie ihre Benutzerdaten in das nachfolgende Formular ein.

-signup.email.subject= Details zu ihrem AppFuse Benutzerkonto

-signup.email.message=Sie wurden erfolgreich für den Zugang zu AppFuse registriert. Angaben zu ihrem Benutzernamen und ihrem Passwort finden sie nachfolgend.

-

-# -- upload page messages --

-maxLengthExceeded=Die Datei, welche sie hochladen möchten, ist zu groß. Die Maximalgröße einer Datei zum Hochladen beträgt 2 MB.

-upload.title=Hochladen von Dateien

-upload.heading=Laden sie eine Datei hoch

-upload.message=Bitte beachten sie, dass Maximalgröße einer Datei zum Hochladen innerhalb dieser Anwendung 2 MB beträgt.

-uploadForm.name=Hübscher Name

-uploadForm.file=Hochzuladende Datei

-

-# -- display page messages -- 

-display.title=Datei wurde erfolgreich hochgeladen!

-display.heading=Dateiinformation

-

-# -- flushCache page --

-flushCache.title=Cache leeren

-flushCache.heading=Cache wurde erfolgreich geleert!

-flushCache.message=Alle Caches wurden erfolgreich geleert, kehre nach 2 Sekunden zur vorherigen Seite zurück.

-

-# -- clickstreams page --

-clickstreams.title=Alle Clickstreams

-clickstreams.heading=Alle Clickstreams

-

-# -- viewstream page --

-viewstream.title=Stream Details

-viewstream.heading=Stream Informationen

-

-# -- active users page --

-activeUsers.title=Aktive Benutzer

-activeUsers.heading=Derzeitige Benutzer

-activeUsers.message=Nachfolgend eine Liste aller angemeldeten Benutzer, deren Sizung nicht abgelaufen ist.

-activeUsers.fullName=Name

-

-# JSF-only messages, remove if not using JSF

-javax.faces.component.UIInput.REQUIRED=Dies ist ein Pflichtfeld.

+user.status=Angemeldet als: 
+user.logout=Abmelden
+
+# -- validator errors --
+errors.invalid={0} ist ung¸ltig.
+errors.maxlength={0} darf maximal {1} Zeichen lang sein.
+errors.minlength={0} muss mindestens {1} Zeichen lang sein.
+errors.range={0} ist nicht im Bereich zwischen {1} und {2}.
+errors.required={0} ist ein Pflichtfeld.
+errors.byte={0} muss ein Bytewert sein.
+errors.date={0} ist kein g¸ltiges Datum.
+errors.double={0} muss ein Wert vom Typ 'double' sein.
+errors.float={0} muss ein Wert vom Typ 'float' sein.
+errors.integer={0} muss eine Zahl sein.
+errors.long={0} muss ein Wert vom Typ 'long' sein.
+errors.short={0} muss ein Wert vom Typ 'short' sein.
+errors.creditcard={0} ist keine g¸ltige Kreditkartennummer.
+errors.email={0} ist eine ung¸ltige E-Mail Adresse.
+errors.phone={0} ist eine ung¸ltige Telefonnummer.
+errors.zip={0} ist eine ung¸ltige Postleitzahl.
+
+# -- other errors --
+errors.cancel=Operation abgebrochen.
+errors.detail={0}
+errors.general=Der Prozess konnte nicht abgeschlossen werden. Detaillierte Angaben sollten nachfolgend angezeigt werden.
+errors.token=Die Anfrage konnte nicht abgeschlossen werden. Die Reihenfolge der Operationen ist nicht korrekt.
+errors.none=Es konnte keine Fehlermeldung gefunden werden, ¸berpr¸fen Sie bitte die Log-Dateien Ihres Servers.
+errors.password.mismatch=Ung¸ltiger Benutzername und/oder Passwort, bitte versuchen Sie es nochmal.
+errors.browser.warning=Hinweis:</strong> Der Inhalt dieser Webpr‰senz kann von jedem Browser in allen Versionen abgerufen werden. Der von Ihnen benutzte Browser unterst¸tzt jedoch mˆglicherweise grundlegende WWW-Standards nicht, so dass Sie das detaillierte Design unserer Webseite eventuell nicht korrekt angezeigt bekommen. Wir unterst¸tzen die <a href="http://www.webstandards.org/upgrade/">Kampagne</a> des Web Standards Projekt, welche die Verbreitung und den Wechsel zu neueren Browserversionen zum Ziel hat.
+errors.conversion=Bei der Konvertierung von Webwerten zu Datenwerten ist ein Fehler aufgetreten.
+errors.twofields=Das Feld {0} muss denselben Wert wie das Feld {1} aufweisen.
+errors.existing.user=Diese Benutzername ({0}) oder diese E-Mail Adresse ({1}) existiert bereits. Bitte versuchen Sie es mit einem anderen Benutzernamen.
+
+# -- success messages --
+user.added=Die Informationen f¸r Benutzer {0} wurden erfolgreich hinzugef¸gt.
+user.deleted=Das Benutzerprofil f¸r {0} wurde erfolgreich gelˆscht.
+user.registered=Sie haben sich erfolgreich registriert.
+user.saved=Ihr Profil wurde erfolgreich aktualisiert.
+user.updated.byAdmin=Die Informationen f¸r Benutzer {0} wurden erfolgreich aktualisiert.
+newuser.email.message={0} hat ein Konto bei AppFuse f¸r Sie angelegt. Informationen zu ihrem Benutzernamen und Ihrem Passwort finden Sie nachfolgend.
+reload.succeeded=Das erneute Laden der Optionen wurde erfolgreich abgeschlossen.
+
+# -- error page messages --
+errorPage.title=Ein Fehler ist aufgetreten
+errorPage.heading=Sapperlott!
+404.title=Die Seite konnte nicht gefunden werden
+404.message=Die von Ihnen angeforderte Seite konnte nicht gefunden werden. Sie kˆnnen versuchen wieder zum <a href="{0}">Hauptmen¸</a> zur¸ckzukehren. Wenn sie schon hier gelandet sind, wie w‰r&#39;s mit einem h¸bschen Bild zur Aufmunterung?
+403.title=Zugang nicht gestattet
+403.message=Ihre derzeitiger Benutzerstatus erlaubt es nicht, diese Seite anzuzeigen.  Bitte nehmen Sie Kontakt mit ihrem Systemadministrator auf falls Sie glauben, dass Ihnen der Zugang gestattet sein sollte. Wie w‰r&#39;s zwischenzeitlich mit einem h¸bschen Bild zur Aufmunterung?
+
+# -- login --
+login.title=Anmeldung
+login.heading=Anmeldung
+login.rememberMe=Daten behalten
+login.signup=Kein Mitglied? <a href="{0}">Anmeldung</a> f¸r ein Benutzerkonto.
+login.passwordHint=Haben Sie ihr Passwort vergessen?  Lassen Sie sich per E-Mail einen <a href="?" onmouseover="window.status='Lassen Sie sich einen Hinweis auf Ihr Passwort zusenden.'; return true" onmouseout="window.status=''; return true" title="Lassen Sie sich einen Hinweis auf Ihr Passwort zusenden." onclick="passwordHint(); return false">Hinweis auf Ihr Passwort</a> zusenden.
+login.passwordHint.sent=Ein Passwordhinweis f¸r {0} wurde an {1} gesendet.
+login.passwordHint.error=Der Benutzername {0} konnte nicht in der Datenbank gefunden werden.
+
+# -- mainMenu --
+mainMenu.title=Hauptmen¸
+mainMenu.heading=Willkommen!
+mainMenu.message=Gratulation, Sie haben sich erfolgreich angemeldet!  Als angemeldeter Benutzer haben Sie folgende Mˆglichkeiten:
+mainMenu.activeUsers=Derzeitige Benutzer
+
+# -- menu/link messages --
+menu.admin=Administration
+menu.admin.users=Zeige Benutzer an
+menu.admin.reload=Optionen neu laden
+
+menu.user=Profil
+menu.selectFile=Datei hochladen
+menu.flushCache=Cache leeren
+menu.clickstream=Clickstream
+
+# -- form labels --
+label.username=Benutzer
+label.password=Passwort
+
+# -- button labels --
+button.add=Hinzuf¸gen
+button.cancel=Abbrechen
+button.copy=Kopieren
+button.delete=Lˆschen
+button.done=Fertig
+button.edit=Bearbeiten
+button.register=Registrieren
+button.save=Speichern
+button.search=Suchen
+button.upload=Hochladen
+button.view=Anzeigen
+button.reset=Zur¸cksetzen
+button.login=Anmelden
+
+# -- general values --
+icon.information=Information
+icon.information.img=/images/iconInformation.gif
+icon.email=E-Mail
+icon.email.img=/images/iconEmail.gif
+icon.warning=Warnung
+icon.warning.img=/images/iconWarning.gif
+date.format=dd.MM.yyyy
+
+# -- role form --
+roleForm.name=Name
+
+# -- user profile page --
+userProfile.title=Benutzereinstellungen
+userProfile.heading=Benutzerprofil
+userProfile.message=Bitte aktualisieren Sie Ihre Daten im nachfolgenden Formular.
+userProfile.admin.message=Sie kˆnnen die Daten dieses Benutzers im nachfolgenden Formular aktualisieren.
+userProfile.showMore=Weitere Informationen
+userProfile.assignRoles=Benutzerstatus zuweisen
+userProfile.cookieLogin= Sie kˆnnen Ihr Passwort nicht ‰ndern, wenn Sie bei der Anmeldung die Option <strong>Daten behalten</strong> ausgew‰hlt haben.  Bitte melden Sie sich zun‰chst ab und dann erneut an, um ihr Passwort ‰ndern zu kˆnnen.
+
+# -- user form --
+user.addressForm.address=Adresse
+user.availableRoles=Verf¸gbare Benutzerrollen
+user.addressForm.city=Stadt
+user.addressForm.country=Land
+user.email=E-Mail
+user.firstName=Vorname
+user.id=ID
+user.lastName=Nachname
+user.password=Passwort
+user.confirmPassword=Passwort best‰tigen
+user.phoneNumber=Telefon
+user.addressForm.postalCode=Postleitzahl
+user.addressForm.province=Bundesland
+user.roles=Derzeitige Benutzerrollen
+user.username=Benutzername
+user.website=Website
+user.visitWebsite=Besuchen
+user.passwordHint=Passworthinweis
+user.enabled=Freigeschaltet
+
+# -- user list page --
+userList.title=Benutzerliste
+userList.heading=Derzeitige Benutzer
+userList.nousers=<span>Keine Benutzer gefunden.</span>
+
+# -- user self-registration --
+signup.title=Anmeldung
+signup.heading=Registrierung als neuer Benutzer
+signup.message=Bitte geben Sie Ihre Benutzerdaten in das nachfolgende Formular ein.
+signup.email.subject= Details zu Ihrem AppFuse Benutzerkonto
+signup.email.message=Sie wurden erfolgreich f¸r den Zugang zu AppFuse registriert. Angaben zu Ihrem Benutzernamen und Ihrem Passwort finden Sie nachfolgend.
+
+# -- upload page messages --
+maxLengthExceeded=Die Datei, welche Sie hochladen mˆchten, ist zu groﬂ. Die Maximalgrˆﬂe einer Datei zum Hochladen betr‰gt 2 MB.
+upload.title=Hochladen von Dateien
+upload.heading=Laden Sie eine Datei hoch
+upload.message=Bitte beachten Sie, dass die Maximalgrˆﬂe einer Datei zum Hochladen innerhalb dieser Anwendung 2 MB betr‰gt.
+uploadForm.name=H¸bscher Name
+uploadForm.file=Hochzuladende Datei
+
+# -- display page messages -- 
+display.title= Die Datei wurde erfolgreich hochgeladen!
+display.heading=Dateiinformation
+
+# -- flushCache page --
+flushCache.title=Cache leeren
+flushCache.heading=Cache wurde erfolgreich geleert!
+flushCache.message=Alle Caches wurden erfolgreich geleert, kehre nach 2 Sekunden zur vorherigen Seite zur¸ck.
+
+# -- clickstreams page --
+clickstreams.title=Alle Clickstreams
+clickstreams.heading=Alle Clickstreams
+
+# -- viewstream page --
+viewstream.title=Stream Details
+viewstream.heading=Stream Informationen
+
+# -- active users page --
+activeUsers.title=Aktive Benutzer
+activeUsers.heading=Derzeitige Benutzer
+activeUsers.message=Nachfolgend eine Liste aller angemeldeten Benutzer, deren Sizung nicht abgelaufen ist.
+activeUsers.fullName=Name
+
+# JSF-only messages, remove if not using JSF
+javax.faces.component.UIInput.REQUIRED=Dies ist ein Pflichtfeld.
 activeUsers.summary={0} Benutzer gefunden, {1} Benutzer angezeigt von Position {2} bis {3}. Seite {4} / {5}
\ No newline at end of file
Index: src/main/resources/struts.xml
===================================================================
--- src/main/resources/struts.xml	(revision 85)
+++ src/main/resources/struts.xml	(working copy)
@@ -12,10 +12,8 @@
     <constant name="struts.multipart.maxSize" value="2097152"/>

     <constant name="struts.ui.theme" value="css_xhtml"/>

     <constant name="struts.codebehind.pathPrefix" value="/WEB-INF/pages/"/>

+    <constant name="struts.enable.SlashesInActionNames" value="true"/>

 

-    <!-- Include Struts defaults -->

-    <include file="struts-default.xml"/>

-

     <!-- Configuration for the default package. -->

     <package name="default" extends="struts-default">

         <interceptors>

@@ -37,11 +35,11 @@
                 <interceptor-ref name="checkbox"/>

                 <interceptor-ref name="static-params"/>

                 <interceptor-ref name="params">

-                	<param name="excludeParams">dojo\..*</param>

+                    <param name="excludeParams">dojo\..*</param>

                 </interceptor-ref>

                 <interceptor-ref name="conversionError"/>

                 <interceptor-ref name="validation">

-                    <param name="excludeMethods">cancel,execute,delete,edit,list,start</param>

+                    <param name="excludeMethods">cancel,execute,delete,edit,list</param>

                 </interceptor-ref>

                 <interceptor-ref name="workflow">

                     <param name="excludeMethods">input,back,cancel,browse</param>

@@ -65,12 +63,8 @@
         <global-exception-mappings>

             <exception-mapping exception="org.springframework.dao.DataAccessException" result="dataAccessFailure"/>

         </global-exception-mappings> 

-        

-        <action name="activeUsers" class="com.opensymphony.xwork2.ActionSupport"> 

-            <result name="success">/WEB-INF/pages/activeUsers.jsp</result> 

-        </action> 

-        

-        <action name="mainMenu" class="com.opensymphony.xwork2.ActionSupport">

+

+        <action name="mainMenu">

             <result name="success">/WEB-INF/pages/mainMenu.jsp</result> 

         </action> 

 

@@ -85,50 +79,35 @@
             <result name="success" type="redirect">/mainMenu.html</result>

         </action> 

 

-        <action name="users" class="userAction" method="list"> 

-            <interceptor-ref name="adminCheck"/>

-            <result name="success">/WEB-INF/pages/userList.jsp</result> 

-        </action>

-        

         <action name="editUser" class="userAction" method="edit">

             <interceptor-ref name="adminCheck"/>

             <result name="success">/WEB-INF/pages/userForm.jsp</result>

-            <result name="input">/WEB-INF/pages/userList.jsp</result>

+            <result name="input">/WEB-INF/pages/admin/userList.jsp</result>

         </action>

 

         <action name="editProfile" class="userAction" method="edit"> 

             <result name="success">/WEB-INF/pages/userForm.jsp</result>

             <result name="error">/WEB-INF/pages/mainMenu.jsp</result>

         </action>

-        

+

         <action name="saveUser" class="userAction" method="save">

-            <result name="cancel" type="redirect">users.html</result>

+            <result name="cancel" type="redirect">admin/users.html</result>

             <result name="input">/WEB-INF/pages/userForm.jsp</result>

-            <result name="success" type="redirect">users.html</result>

+            <result name="success" type="redirect">admin/users.html</result>

         </action>

-        

+

         <action name="uploadFile" class="org.appfuse.webapp.action.FileUploadAction">

             <interceptor-ref name="fileUploadStack"/>

             <result name="input">/WEB-INF/pages/uploadForm.jsp</result>

             <result name="success">/WEB-INF/pages/uploadDisplay.jsp</result>

             <result name="cancel" type="redirect">mainMenu.html</result>

         </action>

-        

-        <action name="flushCache" class="com.opensymphony.xwork2.ActionSupport">

-            <interceptor-ref name="adminCheck"/>

-            <result name="success">/WEB-INF/pages/flushCache.jsp</result> 

-        </action> 

 

         <action name="passwordHint" class="passwordHintAction"> 

-            <result name="success">/</result> 

-        </action> 

-        

-        <action name="reload" class="org.appfuse.webapp.action.ReloadAction">

-            <interceptor-ref name="adminCheck"/>

-            <!-- this should never be used, it's here to prevent warnings -->

-            <result name="success">/WEB-INF/pages/mainMenu.jsp</result>

+            <result name="input">/</result>

+            <result name="success">/</result>

         </action>

-        

+

         <!-- Add additional actions here -->

         <action name="persons" class="org.appfuse.tutorial.webapp.action.PersonAction" method="list">

             <result>/WEB-INF/pages/personList.jsp</result>

@@ -146,4 +125,27 @@
             <result name="success" type="redirect">persons.html</result>

         </action>

     </package>

+

+    <!-- Actions in this package will be prefixed with /admin/ -->

+    <package name="admin" extends="default" namespace="/admin">

+        <action name="activeUsers" class="com.opensymphony.xwork2.ActionSupport">

+            <result name="success">/WEB-INF/pages/admin/activeUsers.jsp</result>

+        </action>

+

+        <action name="flushCache" class="com.opensymphony.xwork2.ActionSupport">

+            <interceptor-ref name="adminCheck"/>

+            <result name="success">/WEB-INF/pages/admin/flushCache.jsp</result>

+        </action>

+

+        <action name="reload" class="org.appfuse.webapp.action.ReloadAction">

+            <interceptor-ref name="adminCheck"/>

+            <!-- this should never be used, it's here to prevent warnings -->

+            <result name="success">/WEB-INF/pages/mainMenu.jsp</result>

+        </action>

+

+        <action name="users" class="userAction" method="list">

+            <interceptor-ref name="adminCheck"/>

+            <result name="success">/WEB-INF/pages/admin/userList.jsp</result>

+        </action>

+    </package>

 </struts>

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
@@ -1,187 +1,186 @@
-Ôªø## Do NOT delete! Keep this line to avoid the native2ascii UTF-8 BOM bug. See #APF-639

-

-user.status=ÂΩìÂâçÁî®Êà∑: 

-user.logout=ÈÄÄÂá∫

-

-# -- validator errors --

-errors.invalid={0} Êó†Êïà„ÄÇ

-errors.maxlength={0} ‰∏çËÉΩÂ§ß‰∫é {1} ‰∏™Â≠óÁ¨¶„ÄÇ

-errors.minlength={0} ‰∏çËÉΩÂ∞ë‰∫é {1} ‰∏™Â≠óÁ¨¶„ÄÇ

-errors.range={0} Êú™Âú® {1} ‰∏é {2} ËåÉÂõ¥ÂÜÖ„ÄÇ

-errors.required={0} ‰∏∫ÂøÖÂ°´È°π„ÄÇ

-errors.byte={0} ÂøÖÈ°ª‰∏∫byteÁ±ªÂûã„ÄÇ

-errors.date={0} ‰∏çÊòØÊúâÊïàÊó•ÊúüÊ†ºÂºè„ÄÇ

-errors.double={0} ÂøÖÈ°ª‰∏∫doubleÁ±ªÂûã„ÄÇ

-errors.float={0} ÂøÖÈ°ª‰∏∫floatÁ±ªÂûã„ÄÇ

-errors.integer={0} ÂøÖÈ°ª‰∏∫‰∏ÄÊï∞ÂÄº„ÄÇ

-errors.long={0} ÂøÖÈ°ª‰∏∫longÁ±ªÂûã„ÄÇ

-errors.short={0} ÂøÖÈ°ª‰∏∫shortÁ±ªÂûã„ÄÇ

-errors.creditcard={0} ‰∏∫Êó†Êïà‰ø°Áî®Âç°Âè∑„ÄÇ

-errors.email={0} ‰∏∫Êó†ÊïàÈÇÆ‰ª∂Âú∞ÂùÄ„ÄÇ

-errors.phone={0} ‰∏∫Êó†ÊïàÁîµËØùÂè∑Á†Å„ÄÇ

-errors.zip={0} ‰∏∫Êó†ÊïàÈÇÆÊîøÁºñÁ†Å„ÄÇ

-

-# -- other errors --

-errors.cancel=Êìç‰ΩúË¢´ÂèñÊ∂à„ÄÇ

-errors.detail={0}

-errors.general=<strong>Êìç‰ΩúÊú™ÂÆåÊàê„ÄÇËØ¶ÁªÜÂéüÂõ†Â¶Ç‰∏ã„ÄÇ</strong>

-errors.token=ËØ∑Ê±ÇÊú™ÂÆåÂÖ®Â§ÑÁêÜ„ÄÇÊìç‰ΩúÈ°∫Â∫èÈîôËØØ„ÄÇ

-errors.none=Êó†ÈîôËØØÊ∂àÊÅØÔºåËØ∑Ê£ÄÊü•ÊúçÂä°Âô®Êó•ÂøóÊñá‰ª∂„ÄÇ

-errors.password.mismatch=Êó†ÊïàÁî®Êà∑ÂêçÊàñÂØÜÁ†ÅÔºåËØ∑ÈáçËØï„ÄÇ

-errors.conversion=Âú®webÂ±ÇÊï∞ÊçÆÂà∞‰∏öÂä°Â±ÇÊï∞ÊçÆÁöÑËΩ¨Êç¢ËøáÁ®ã‰∏≠ÔºåÂèëÁîü‰∫Ü‰∏Ä‰∏™ÈîôËØØ„ÄÇ

-errors.twofields={0} Â≠óÊÆµ‰∏é {1} Â≠óÊÆµÁöÑÂÄºÂøÖÈ°ª‰∏ÄËá¥„ÄÇ

-errors.existing.user=Áî®Êà∑Âêç ({0}) Êàñe-mailÂú∞ÂùÄ ({1}) Â∑≤Â≠òÂú®„ÄÇËØ∑ÂÜçÊ¨°Â∞ùËØï‰∏çÂêåÂêçÁß∞„ÄÇ

-

-# -- success messages --

-user.added=Áî®Êà∑ <strong>{0}</strong> ÁöÑ‰ø°ÊÅØÊ∑ªÂä†ÊàêÂäü„ÄÇ

-user.deleted=Áî®Êà∑ <strong>{0}</strong> ÁöÑ‰ø°ÊÅØÂà†Èô§ÊàêÂäü„ÄÇ 

-user.registered=Ê≥®ÂÜåÊàêÂäüÔºåÊÇ®ÂèØ‰ª•ÂºÄÂßã‰ΩøÁî®Á≥ªÁªü„ÄÇ

-user.saved=ÊÇ®ÁöÑ‰ø°ÊÅØÂ∑≤ÊàêÂäüÊõ¥Êñ∞„ÄÇ

-user.updated.byAdmin=Áî®Êà∑ <strong>{0}</strong> ÁöÑ‰ø°ÊÅØÂ∑≤ÊàêÂäüÊõ¥Êñ∞„ÄÇ

-newuser.email.message={0} ‰∏∫ÊÇ®ÊàêÂäüÂàõÂª∫‰∫Ü‰∏Ä‰∏™AppFuseÂ∏êÂè∑„ÄÇÊÇ®ÁöÑÁî®Êà∑ÂêçÂíåÂØÜÁ†Å‰ø°ÊÅØÂ¶Ç‰∏ãÔºö

-reload.succeeded=Â∑≤ÁªèÊàêÂäüÈáçËΩΩ.

-

-# -- error page messages --

-errorPage.title=Á≥ªÁªüÈîôËØØ

-errorPage.heading=Âì¶ÔºÅ

-404.title=È°µÈù¢Êú™ÊâæÂà∞

-404.message=ËØ∑Ê±ÇÁöÑÈ°µÈù¢Êú™ÊâæÂà∞„ÄÇÊÇ®ÂèØ‰ª•ÈÄâÊã©ËøîÂõûÂà∞ <a href="{0}">‰∏ªËèúÂçï</a>„ÄÇÊàñËÄÖÈÄâÊã©Âú®Ê≠§‰ºëÊÅØ‰∏Ä‰∏ãÔºåÂøòÊéâÂàöÊâçÁöÑÊ≤Æ‰∏ßÔºåÊ¨£Ëµè‰∏Ä‰∏™Áæé‰∏ΩÁöÑÂõæÁâáÔºü

-403.title=ËÆøÈóÆË¢´ÊãíÁªù

-403.message=ÊÇ®ÂΩìÂâçËßíËâ≤Êó†ÊùÉÈôêÊü•ÁúãÊ≠§È°µÈù¢„ÄÇËØ∑ËÅîÁ≥ªÁ≥ªÁªüÁÆ°ÁêÜÂëòÔºåËé∑ÂæóÁõ∏Â∫îÁöÑÊùÉÈôê„ÄÇÊ≠§ÂàªÔºåËÆ©Êàë‰ª¨Ê¨£Ëµè‰∏Ä‰∏™ÂõæÁâáÔºåÊîæÊùæ‰∏Ä‰∏ãÂ•ΩÂêßÔºü

-

-# -- login --

-login.title=ÁôªÂΩï

-login.heading=ÁôªÂΩï

-login.rememberMe=ËÆ©Á≥ªÁªüËÆ∞‰ΩèÊàë

-login.signup=‰∏çÊòØÊ≥®ÂÜåÁî®Êà∑? <a href="{0}">Áî≥ËØ∑</a> ‰∏Ä‰∏™Â∏êÂè∑„ÄÇ

-login.passwordHint=ÂøòËÆ∞‰∫ÜÂØÜÁ†Å?  ËÆ©Á≥ªÁªüÂ∞Ü <a href="?" onmouseover="window.status='Á≥ªÁªüÂèëÈÄÅÂØÜÁ†ÅÊèêÁ§∫„ÄÇ'; return true" onmouseout="window.status=''; return true" title="Á≥ªÁªüÂèëÈÄÅÂØÜÁ†ÅÊèêÁ§∫„ÄÇ" onclick="passwordHint(); return false">ÂØÜÁ†ÅÊèêÁ§∫‰ø°ÊÅØÂ∑≤e-mailÂΩ¢ÂºèÂèëÈÄÅÁªôÊÇ®</a>„ÄÇ

-login.passwordHint.sent=<strong>{0}</strong> ÁöÑÂØÜÁ†ÅÊèêÁ§∫Â∑≤ÊàêÂäüÂèëÈÄÅÂà∞ <strong>{1}</strong>„ÄÇ

-login.passwordHint.error=Áî®Êà∑Âêç <strong>{0}</strong> Âú®Á≥ªÁªüÊï∞ÊçÆÂ∫ì‰∏≠Êú™ÊâæÂà∞„ÄÇ

-

-# -- mainMenu --

-mainMenu.title=‰∏ªËèúÂçï

-mainMenu.heading=Ê¨¢ËøéÔºÅ

-mainMenu.message=ÊÅ≠ÂñúÔºåÊÇ®ÁôªÂΩïÊàêÂäüÔºÅÊÇ®ÂèØ‰ª•ÈÄâÊã©ÊâßË°å‰ª•‰∏ãÊìç‰ΩúÔºö

-mainMenu.activeUsers=Âú®Á∫øÁî®Êà∑

-

-# -- menu/link messages --

-menu.admin=Á≥ªÁªüÁÆ°ÁêÜ

-menu.admin.users=Êü•ÁúãÁî®Êà∑

-menu.admin.reload=ÈáçËΩΩÈÄâÈ°π

-

-menu.user=ÁºñËæë‰ø°ÊÅØ

-menu.selectFile=‰∏ä‰º†Êñá‰ª∂

-menu.flushCache=Âà∑Êñ∞ÁºìÂ≠ò

-menu.clickstream=ËÆøÈóÆËÆ∞ÂΩï

-

-# -- form labels --

-label.username=Áî®Êà∑Âêç

-label.password=ÂØÜÁ†Å

-

-# -- button labels --

-button.add=Ê∑ªÂä†

-button.cancel=ÂèñÊ∂à

-button.copy=Â§çÂà∂

-button.delete=Âà†Èô§

-button.done=ÂÅö

-button.edit=ÁºñËæë

-button.register=Ê≥®ÂÜå

-button.save=‰øùÂ≠ò

-button.search=ÊêúÁ¥¢

-button.upload=‰∏ä‰º†

-button.view=Êü•Áúã

-button.reset=Â§ç‰Ωç

-button.login=ÁôªÂΩï

-

-# -- general values --

-icon.information=‰ø°ÊÅØ

-icon.information.img=/images/iconInformation.gif

-icon.email=E-Mail

-icon.email.img=/images/iconEmail.gif

-icon.warning=Ë≠¶Âëä

-icon.warning.img=/images/iconWarning.gif

-date.format=MM/dd/yyyy

-

-# -- role form --

-roleForm.name=ÂêçÁß∞

-

-# -- user profile page --

-userProfile.title=Áî®Êà∑ËÆæÁΩÆ

-userProfile.heading=Áî®Êà∑ÁÆÄË¶Å‰ø°ÊÅØ

-userProfile.message=ËØ∑ÊåâÂ¶Ç‰∏ãË°®Ê†ºÊõ¥Êñ∞ÊÇ®ÁöÑ‰ø°ÊÅØ„ÄÇ

-userProfile.admin.message=ÊÇ®ÂèØ‰ª•ÊåâÂ¶Ç‰∏ãË°®Ê†ºÔºåÊõ¥Êñ∞Áî®Êà∑ÁöÑ‰ø°ÊÅØ„ÄÇ

-userProfile.showMore=Êü•ÁúãÊõ¥Â§ö‰ø°ÊÅØ

-userProfile.accountSettings=Â∏êÊà∑ËÆæÁΩÆ

-userProfile.assignRoles=ÂàÜÈÖçËßíËâ≤

-userProfile.cookieLogin=ÊÇ®Êó†Ê≥ïÊõ¥ÊîπÂØÜÁ†ÅÔºåÂõ†‰∏∫ÊÇ®ÈÄâÊã©‰∫Ü <strong>ËÆ©Á≥ªÁªüËÆ∞‰ΩèÊàë</strong> ÈÄâÈ°π„ÄÇËØ∑ÈÄÄÂá∫Á≥ªÁªüÔºåÂÜçÊ¨°ÁôªÂΩïÂ∞ùËØïÊõ¥ÊîπÂØÜÁ†Å„ÄÇ

-

-# -- user form --

-user.address.address=Âú∞ÂùÄ

-user.availableRoles=ÂèØÁî®ËßíËâ≤

-user.address.city=ÂüéÂ∏Ç

-user.address.country=ÂõΩÂÆ∂

-user.email=E-Mail

-user.firstName=Âêç

-user.id=Id

-user.lastName=Âßì

-user.password=ÂØÜÁ†Å

-user.confirmPassword=Á°ÆËÆ§ÂØÜÁ†Å

-user.phoneNumber=ÁîµËØù

-user.address.postalCode=ÈÇÆÁºñ

-user.address.province=Â∑ûÁúÅ

-user.roles=ÂΩìÂâçËßíËâ≤

-user.username=Áî®Êà∑Âêç

-user.website=ÁΩëÂùÄ

-user.visitWebsite=ÊâìÂºÄ

-user.passwordHint=ÂØÜÁ†ÅÊèêÁ§∫

-user.enabled=‰ΩøËÉΩ

-user.accountExpired=Âà∞Êúü

-user.accountLocked=ÈîÅÁùÄ

-user.credentialsExpired=ÂØÜÁ†ÅÂà∞Êúü‰∫Ü

-

-# -- user list page --

-userList.title=Áî®Êà∑ÂàóË°®

-userList.heading=Âú®Á∫øÁî®Êà∑

-userList.nousers=<span>Ê≤°ÊâæÂà∞Áî®Êà∑„ÄÇ</span>

-

-# -- user self-registration --

-signup.title=Ê≥®ÂÜå

-signup.heading=Êñ∞Áî®Êà∑Ê≥®ÂÜå

-signup.message=ËØ∑ËæìÂÖ•Áî®Êà∑‰ø°ÊÅØ„ÄÇ

-signup.email.subject=AppFuse Â∏êÊà∑‰ø°ÊÅØ

-signup.email.message=ÊÇ®Â∑≤ÊàêÂäüÊ≥®ÂÜåÂà∞ AppFuse„ÄÇÊÇ®ÁöÑÁî®Êà∑ÂêçÂíåÂØÜÁ†Å‰ø°ÊÅØÂ¶Ç‰∏ãÔºö

-

-# -- upload page messages --

-maxLengthExceeded=ÈÄâÊã©‰∏ä‰º†ÁöÑÊñá‰ª∂ËøáÂ§ß„ÄÇÊúÄÂ§ßÂÖÅËÆ∏ÂÄº‰∏∫ 2 MB„ÄÇ

-upload.title=Êñá‰ª∂‰∏ä‰º†

-upload.heading=‰∏ä‰º†‰∏ÄÊñá‰ª∂

-upload.message=‰∏ªË¶ÅÁ≥ªÁªüÂÖÅËÆ∏‰∏ä‰º†Êñá‰ª∂ÁöÑÊúÄÂ§ßÂÄº‰∏∫ 2 MB„ÄÇ

-uploadForm.name=ÈáçÂëΩÂêçÊñá‰ª∂

-uploadForm.file=ÈÄâÊã©Êñá‰ª∂

-

-# -- display page messages -- 

-display.title=Êñá‰ª∂‰∏ä‰º†ÊàêÂäüÔºÅ

-display.heading=Êñá‰ª∂‰ø°ÊÅØ

-

-# -- flushCache page --

-flushCache.title=Âà∑Êñ∞ÁºìÂ≠ò

-flushCache.heading=Âà∑Êñ∞ÊàêÂäüÔºÅ

-flushCache.message=ÊâÄÊúâÁºìÂ≠òÊàêÂäüÂà∑Êñ∞Ôºå2 Áßí‰πãÂêéÔºåÁ≥ªÁªüËá™Âä®ËøîÂõûÂà∞ÂâçÈù¢ÁöÑÈ°µÈù¢„ÄÇ

-

-# -- clickstreams page --

-clickstreams.title=ÊâÄÊúâËÆøÈóÆËÆ∞ÂΩï

-clickstreams.heading=ÊâÄÊúâËÆøÈóÆËÆ∞ÂΩï

-

-# -- viewstream page --

-viewstream.title=ËÆøÈóÆËÆ∞ÂΩïËØ¶ÁªÜ

-viewstream.heading=ËÆøÈóÆËÆ∞ÂΩï‰ø°ÊÅØ

-

-# -- active users page --

-activeUsers.title=Ê¥ªÂä®Áî®Êà∑ÂàóË°®

-activeUsers.heading=Âú®Á∫øÁî®Êà∑

-activeUsers.message=ÂàóË°®‰∏∫Â∑≤ÊàêÂäüÁôªÂΩïÁöÑ„ÄÅsession‰∏∫ËøáÊúüÁöÑÁî®Êà∑„ÄÇ

-activeUsers.fullName=ÂÖ®Âêç

-

-# JSF-only messages, remove if not using JSF

-javax.faces.component.UIInput.REQUIRED={0} ‰∏∫ÂøÖÂ°´È°π„ÄÇ

+Ôªø
+user.status=ÂΩìÂâçÁî®Êà∑: 
+user.logout=ÈÄÄÂá∫
+
+# -- validator errors --
+errors.invalid={0} Êó†Êïà„ÄÇ
+errors.maxlength={0} ‰∏çËÉΩÂ§ß‰∫é {1} ‰∏™Â≠óÁ¨¶„ÄÇ
+errors.minlength={0} ‰∏çËÉΩÂ∞ë‰∫é {1} ‰∏™Â≠óÁ¨¶„ÄÇ
+errors.range={0} Êú™Âú® {1} ‰∏é {2} ËåÉÂõ¥ÂÜÖ„ÄÇ
+errors.required={0} ‰∏∫ÂøÖÂ°´È°π„ÄÇ
+errors.byte={0} ÂøÖÈ°ª‰∏∫byteÁ±ªÂûã„ÄÇ
+errors.date={0} ‰∏çÊòØÊúâÊïàÊó•ÊúüÊ†ºÂºè„ÄÇ
+errors.double={0} ÂøÖÈ°ª‰∏∫doubleÁ±ªÂûã„ÄÇ
+errors.float={0} ÂøÖÈ°ª‰∏∫floatÁ±ªÂûã„ÄÇ
+errors.integer={0} ÂøÖÈ°ª‰∏∫‰∏ÄÊï∞ÂÄº„ÄÇ
+errors.long={0} ÂøÖÈ°ª‰∏∫longÁ±ªÂûã„ÄÇ
+errors.short={0} ÂøÖÈ°ª‰∏∫shortÁ±ªÂûã„ÄÇ
+errors.creditcard={0} ‰∏∫Êó†Êïà‰ø°Áî®Âç°Âè∑„ÄÇ
+errors.email={0} ‰∏∫Êó†ÊïàÈÇÆ‰ª∂Âú∞ÂùÄ„ÄÇ
+errors.phone={0} ‰∏∫Êó†ÊïàÁîµËØùÂè∑Á†Å„ÄÇ
+errors.zip={0} ‰∏∫Êó†ÊïàÈÇÆÊîøÁºñÁ†Å„ÄÇ
+
+# -- other errors --
+errors.cancel=Êìç‰ΩúË¢´ÂèñÊ∂à„ÄÇ
+errors.detail={0}
+errors.general=Êìç‰ΩúÊú™ÂÆåÊàê„ÄÇËØ¶ÁªÜÂéüÂõ†Â¶Ç‰∏ã„ÄÇ
+errors.token=ËØ∑Ê±ÇÊú™ÂÆåÂÖ®Â§ÑÁêÜ„ÄÇÊìç‰ΩúÈ°∫Â∫èÈîôËØØ„ÄÇ
+errors.none=Êó†ÈîôËØØÊ∂àÊÅØÔºåËØ∑Ê£ÄÊü•ÊúçÂä°Âô®Êó•ÂøóÊñá‰ª∂„ÄÇ
+errors.password.mismatch=Êó†ÊïàÁî®Êà∑ÂêçÊàñÂØÜÁ†ÅÔºåËØ∑ÈáçËØï„ÄÇ
+errors.conversion=Âú®webÂ±ÇÊï∞ÊçÆÂà∞‰∏öÂä°Â±ÇÊï∞ÊçÆÁöÑËΩ¨Êç¢ËøáÁ®ã‰∏≠ÔºåÂèëÁîü‰∫Ü‰∏Ä‰∏™ÈîôËØØ„ÄÇ
+errors.twofields={0} Â≠óÊÆµ‰∏é {1} Â≠óÊÆµÁöÑÂÄºÂøÖÈ°ª‰∏ÄËá¥„ÄÇ
+errors.existing.user=Áî®Êà∑Âêç ({0}) Êàñe-mailÂú∞ÂùÄ ({1}) Â∑≤Â≠òÂú®„ÄÇËØ∑ÂÜçÊ¨°Â∞ùËØï‰∏çÂêåÂêçÁß∞„ÄÇ
+
+# -- success messages --
+user.added=Áî®Êà∑ {0} ÁöÑ‰ø°ÊÅØÊ∑ªÂä†ÊàêÂäü„ÄÇ
+user.deleted=Áî®Êà∑ {0} ÁöÑ‰ø°ÊÅØÂà†Èô§ÊàêÂäü„ÄÇ
+user.registered=Ê≥®ÂÜåÊàêÂäüÔºåÊÇ®ÂèØ‰ª•ÂºÄÂßã‰ΩøÁî®Á≥ªÁªü„ÄÇ
+user.saved=ÊÇ®ÁöÑ‰ø°ÊÅØÂ∑≤ÊàêÂäüÊõ¥Êñ∞„ÄÇ
+user.updated.byAdmin=Áî®Êà∑ {0} ÁöÑ‰ø°ÊÅØÂ∑≤ÊàêÂäüÊõ¥Êñ∞„ÄÇ
+newuser.email.message={0} ‰∏∫ÊÇ®ÊàêÂäüÂàõÂª∫‰∫Ü‰∏Ä‰∏™AppFuseÂ∏êÂè∑„ÄÇÊÇ®ÁöÑÁî®Êà∑ÂêçÂíåÂØÜÁ†Å‰ø°ÊÅØÂ¶Ç‰∏ãÔºö
+reload.succeeded=Â∑≤ÁªèÊàêÂäüÈáçËΩΩ.
+
+# -- error page messages --
+errorPage.title=Á≥ªÁªüÈîôËØØ
+errorPage.heading=Âì¶ÔºÅ
+404.title=È°µÈù¢Êú™ÊâæÂà∞
+404.message=ËØ∑Ê±ÇÁöÑÈ°µÈù¢Êú™ÊâæÂà∞„ÄÇÊÇ®ÂèØ‰ª•ÈÄâÊã©ËøîÂõûÂà∞ <a href="{0}">‰∏ªËèúÂçï</a>„ÄÇÊàñËÄÖÈÄâÊã©Âú®Ê≠§‰ºëÊÅØ‰∏Ä‰∏ãÔºåÂøòÊéâÂàöÊâçÁöÑÊ≤Æ‰∏ßÔºåÊ¨£Ëµè‰∏Ä‰∏™Áæé‰∏ΩÁöÑÂõæÁâáÔºü
+403.title=ËÆøÈóÆË¢´ÊãíÁªù
+403.message=ÊÇ®ÂΩìÂâçËßíËâ≤Êó†ÊùÉÈôêÊü•ÁúãÊ≠§È°µÈù¢„ÄÇËØ∑ËÅîÁ≥ªÁ≥ªÁªüÁÆ°ÁêÜÂëòÔºåËé∑ÂæóÁõ∏Â∫îÁöÑÊùÉÈôê„ÄÇÊ≠§ÂàªÔºåËÆ©Êàë‰ª¨Ê¨£Ëµè‰∏Ä‰∏™ÂõæÁâáÔºåÊîæÊùæ‰∏Ä‰∏ãÂ•ΩÂêßÔºü
+
+# -- login --
+login.title=ÁôªÂΩï
+login.heading=ÁôªÂΩï
+login.rememberMe=ËÆ©Á≥ªÁªüËÆ∞‰ΩèÊàë
+login.signup=‰∏çÊòØÊ≥®ÂÜåÁî®Êà∑? <a href="{0}">Áî≥ËØ∑</a> ‰∏Ä‰∏™Â∏êÂè∑„ÄÇ
+login.passwordHint=ÂøòËÆ∞‰∫ÜÂØÜÁ†Å?  ËÆ©Á≥ªÁªüÂ∞Ü <a href="?" onmouseover="window.status='Á≥ªÁªüÂèëÈÄÅÂØÜÁ†ÅÊèêÁ§∫„ÄÇ'; return true" onmouseout="window.status=''; return true" title="Á≥ªÁªüÂèëÈÄÅÂØÜÁ†ÅÊèêÁ§∫„ÄÇ" onclick="passwordHint(); return false">ÂØÜÁ†ÅÊèêÁ§∫‰ø°ÊÅØÂ∑≤e-mailÂΩ¢ÂºèÂèëÈÄÅÁªôÊÇ®</a>„ÄÇ
+login.passwordHint.sent={0}</strong> ÁöÑÂØÜÁ†ÅÊèêÁ§∫Â∑≤ÊàêÂäüÂèëÈÄÅÂà∞ {1}„ÄÇ
+login.passwordHint.error=Áî®Êà∑Âêç {0} Âú®Á≥ªÁªüÊï∞ÊçÆÂ∫ì‰∏≠Êú™ÊâæÂà∞„ÄÇ
+
+# -- mainMenu --
+mainMenu.title=‰∏ªËèúÂçï
+mainMenu.heading=Ê¨¢ËøéÔºÅ
+mainMenu.message=ÊÅ≠ÂñúÔºåÊÇ®ÁôªÂΩïÊàêÂäüÔºÅÊÇ®ÂèØ‰ª•ÈÄâÊã©ÊâßË°å‰ª•‰∏ãÊìç‰ΩúÔºö
+mainMenu.activeUsers=Âú®Á∫øÁî®Êà∑
+
+# -- menu/link messages --
+menu.admin=Á≥ªÁªüÁÆ°ÁêÜ
+menu.admin.users=Êü•ÁúãÁî®Êà∑
+menu.admin.reload=ÈáçËΩΩÈÄâÈ°π
+
+menu.user=ÁºñËæë‰ø°ÊÅØ
+menu.selectFile=‰∏ä‰º†Êñá‰ª∂
+menu.flushCache=Âà∑Êñ∞ÁºìÂ≠ò
+menu.clickstream=ËÆøÈóÆËÆ∞ÂΩï
+
+# -- form labels --
+label.username=Áî®Êà∑Âêç
+label.password=ÂØÜÁ†Å
+
+# -- button labels --
+button.add=Ê∑ªÂä†
+button.cancel=ÂèñÊ∂à
+button.copy=Â§çÂà∂
+button.delete=Âà†Èô§
+button.done=ÂÅö
+button.edit=ÁºñËæë
+button.register=Ê≥®ÂÜå
+button.save=‰øùÂ≠ò
+button.search=ÊêúÁ¥¢
+button.upload=‰∏ä‰º†
+button.view=Êü•Áúã
+button.reset=Â§ç‰Ωç
+button.login=ÁôªÂΩï
+
+# -- general values --
+icon.information=‰ø°ÊÅØ
+icon.information.img=/images/iconInformation.gif
+icon.email=E-Mail
+icon.email.img=/images/iconEmail.gif
+icon.warning=Ë≠¶Âëä
+icon.warning.img=/images/iconWarning.gif
+date.format=MM/dd/yyyy
+
+# -- role form --
+roleForm.name=ÂêçÁß∞
+
+# -- user profile page --
+userProfile.title=Áî®Êà∑ËÆæÁΩÆ
+userProfile.heading=Áî®Êà∑ÁÆÄË¶Å‰ø°ÊÅØ
+userProfile.message=ËØ∑ÊåâÂ¶Ç‰∏ãË°®Ê†ºÊõ¥Êñ∞ÊÇ®ÁöÑ‰ø°ÊÅØ„ÄÇ
+userProfile.admin.message=ÊÇ®ÂèØ‰ª•ÊåâÂ¶Ç‰∏ãË°®Ê†ºÔºåÊõ¥Êñ∞Áî®Êà∑ÁöÑ‰ø°ÊÅØ„ÄÇ
+userProfile.showMore=Êü•ÁúãÊõ¥Â§ö‰ø°ÊÅØ
+userProfile.accountSettings=Â∏êÊà∑ËÆæÁΩÆ
+userProfile.assignRoles=ÂàÜÈÖçËßíËâ≤
+userProfile.cookieLogin=ÊÇ®Êó†Ê≥ïÊõ¥ÊîπÂØÜÁ†ÅÔºåÂõ†‰∏∫ÊÇ®ÈÄâÊã©‰∫Ü <strong>ËÆ©Á≥ªÁªüËÆ∞‰ΩèÊàë</strong> ÈÄâÈ°π„ÄÇËØ∑ÈÄÄÂá∫Á≥ªÁªüÔºåÂÜçÊ¨°ÁôªÂΩïÂ∞ùËØïÊõ¥ÊîπÂØÜÁ†Å„ÄÇ
+
+# -- user form --
+user.address.address=Âú∞ÂùÄ
+user.availableRoles=ÂèØÁî®ËßíËâ≤
+user.address.city=ÂüéÂ∏Ç
+user.address.country=ÂõΩÂÆ∂
+user.email=E-Mail
+user.firstName=Âêç
+user.id=Id
+user.lastName=Âßì
+user.password=ÂØÜÁ†Å
+user.confirmPassword=Á°ÆËÆ§ÂØÜÁ†Å
+user.phoneNumber=ÁîµËØù
+user.address.postalCode=ÈÇÆÁºñ
+user.address.province=Â∑ûÁúÅ
+user.roles=ÂΩìÂâçËßíËâ≤
+user.username=Áî®Êà∑Âêç
+user.website=ÁΩëÂùÄ
+user.visitWebsite=ÊâìÂºÄ
+user.passwordHint=ÂØÜÁ†ÅÊèêÁ§∫
+user.enabled=‰ΩøËÉΩ
+user.accountExpired=Âà∞Êúü
+user.accountLocked=ÈîÅÁùÄ
+user.credentialsExpired=ÂØÜÁ†ÅÂà∞Êúü‰∫Ü
+
+# -- user list page --
+userList.title=Áî®Êà∑ÂàóË°®
+userList.heading=Âú®Á∫øÁî®Êà∑
+userList.nousers=<span>Ê≤°ÊâæÂà∞Áî®Êà∑„ÄÇ</span>
+
+# -- user self-registration --
+signup.title=Ê≥®ÂÜå
+signup.heading=Êñ∞Áî®Êà∑Ê≥®ÂÜå
+signup.message=ËØ∑ËæìÂÖ•Áî®Êà∑‰ø°ÊÅØ„ÄÇ
+signup.email.subject=AppFuse Â∏êÊà∑‰ø°ÊÅØ
+signup.email.message=ÊÇ®Â∑≤ÊàêÂäüÊ≥®ÂÜåÂà∞ AppFuse„ÄÇÊÇ®ÁöÑÁî®Êà∑ÂêçÂíåÂØÜÁ†Å‰ø°ÊÅØÂ¶Ç‰∏ãÔºö
+
+# -- upload page messages --
+maxLengthExceeded=ÈÄâÊã©‰∏ä‰º†ÁöÑÊñá‰ª∂ËøáÂ§ß„ÄÇÊúÄÂ§ßÂÖÅËÆ∏ÂÄº‰∏∫ 2 MB„ÄÇ
+upload.title=Êñá‰ª∂‰∏ä‰º†
+upload.heading=‰∏ä‰º†‰∏ÄÊñá‰ª∂
+upload.message=‰∏ªË¶ÅÁ≥ªÁªüÂÖÅËÆ∏‰∏ä‰º†Êñá‰ª∂ÁöÑÊúÄÂ§ßÂÄº‰∏∫ 2 MB„ÄÇ
+uploadForm.name=ÈáçÂëΩÂêçÊñá‰ª∂
+uploadForm.file=ÈÄâÊã©Êñá‰ª∂
+
+# -- display page messages -- 
+display.title=Êñá‰ª∂‰∏ä‰º†ÊàêÂäüÔºÅ
+display.heading=Êñá‰ª∂‰ø°ÊÅØ
+
+# -- flushCache page --
+flushCache.title=Âà∑Êñ∞ÁºìÂ≠ò
+flushCache.heading=Âà∑Êñ∞ÊàêÂäüÔºÅ
+flushCache.message=ÊâÄÊúâÁºìÂ≠òÊàêÂäüÂà∑Êñ∞Ôºå2 Áßí‰πãÂêéÔºåÁ≥ªÁªüËá™Âä®ËøîÂõûÂà∞ÂâçÈù¢ÁöÑÈ°µÈù¢„ÄÇ
+
+# -- clickstreams page --
+clickstreams.title=ÊâÄÊúâËÆøÈóÆËÆ∞ÂΩï
+clickstreams.heading=ÊâÄÊúâËÆøÈóÆËÆ∞ÂΩï
+
+# -- viewstream page --
+viewstream.title=ËÆøÈóÆËÆ∞ÂΩïËØ¶ÁªÜ
+viewstream.heading=ËÆøÈóÆËÆ∞ÂΩï‰ø°ÊÅØ
+
+# -- active users page --
+activeUsers.title=Ê¥ªÂä®Áî®Êà∑ÂàóË°®
+activeUsers.heading=Âú®Á∫øÁî®Êà∑
+activeUsers.message=ÂàóË°®‰∏∫Â∑≤ÊàêÂäüÁôªÂΩïÁöÑ„ÄÅsession‰∏∫ËøáÊúüÁöÑÁî®Êà∑„ÄÇ
+activeUsers.fullName=ÂÖ®Âêç
+
+# JSF-only messages, remove if not using JSF
+javax.faces.component.UIInput.REQUIRED={0} ‰∏∫ÂøÖÂ°´È°π„ÄÇ
 activeUsers.summary=ÊâæÂà∞ {0} ‰∏™Áî®Êà∑ÔºåÊòæÁ§∫ {1} ‰∏™Áî®Êà∑Ôºå‰ªé {2} Âà∞ {3}„ÄÇ {4} / {5} È°µ
\ No newline at end of file
Index: src/main/resources/log4j.xml
===================================================================
--- src/main/resources/log4j.xml	(revision 85)
+++ src/main/resources/log4j.xml	(working copy)
@@ -1,51 +1,61 @@
-<?xml version="1.0" encoding="UTF-8" ?>
-<!DOCTYPE log4j:configuration SYSTEM "log4j.dtd">
-
-<log4j:configuration xmlns:log4j="http://jakarta.apache.org/log4j/">
-
-    <appender name="CONSOLE" class="org.apache.log4j.ConsoleAppender">
-        <layout class="org.apache.log4j.PatternLayout">
-            <param name="ConversionPattern"
-                value="[tutorial-struts2] %p [%t] %c{1}.%M(%L) | %m%n"/>
-        </layout>
-    </appender>
-
-    <logger name="net.sf.ehcache">
-        <level value="ERROR"/>
-    </logger>
-
-    <!-- Suppress success logging from InteractiveAuthenticationSuccessEvent -->
-    <logger name="org.acegisecurity">
-        <level value="ERROR"/>
-    </logger>
-
-    <logger name="org.apache">
-        <level value="WARN"/>
-    </logger>
-
-    <logger name="org.hibernate">
-        <level value="WARN"/>
-    </logger>
-  
-    <!--logger name="org.hibernate.SQL">
-        <level value="DEBUG"/>
-    </logger-->
-
-    <logger name="org.springframework">
-        <level value="WARN"/>
-    </logger>
-   
-    <logger name="org.appfuse">
-        <level value="INFO"/>
-    </logger>
-    
-    <logger name="org.appfuse.tutorial">
-        <level value="DEBUG"/>
-    </logger>
-
-    <root>
-        <level value="WARN"/>
-        <appender-ref ref="CONSOLE"/>
-    </root>
-
-</log4j:configuration>
+<?xml version="1.0" encoding="UTF-8" ?>

+<!DOCTYPE log4j:configuration SYSTEM "log4j.dtd">

+

+<log4j:configuration xmlns:log4j="http://jakarta.apache.org/log4j/">

+

+    <appender name="CONSOLE" class="org.apache.log4j.ConsoleAppender">

+        <layout class="org.apache.log4j.PatternLayout">

+            <param name="ConversionPattern"

+                value="[tutorial-struts2] %p [%t] %c{1}.%M(%L) | %m%n"/>

+        </layout>

+    </appender>

+

+    <logger name="net.sf.ehcache">

+        <level value="ERROR"/>

+    </logger>

+

+    <!-- Suppress success logging from InteractiveAuthenticationSuccessEvent -->

+    <logger name="org.acegisecurity">

+        <level value="ERROR"/>

+    </logger>

+

+    <logger name="org.apache">

+        <level value="WARN"/>

+    </logger>

+

+    <logger name="org.hibernate">

+        <level value="WARN"/>

+    </logger>

+  

+    <!--logger name="org.hibernate.SQL">

+        <level value="DEBUG"/>

+    </logger-->

+

+    <logger name="org.springframework">

+        <level value="WARN"/>

+    </logger>

+

+    <!-- http://issues.appfuse.org/browse/APF-736#action_11786 -->

+    <logger name="com.opensymphony.xwork2.util.XWorkConverter">

+        <level value="FATAL"/>

+    </logger>

+

+    <!-- http://issues.appfuse.org/browse/APF-852 -->

+    <logger name="com.opensymphony.xwork2.util.OgnlUtil">

+        <level value="ERROR"/>

+    </logger>

+   

+    <logger name="org.appfuse">

+        <level value="INFO"/>

+    </logger>

+    

+    <logger name="org.appfuse.tutorial">

+        <level value="DEBUG"/>

+    </logger>

+

+    <root>

+        <level value="WARN"/>

+        <appender-ref ref="CONSOLE"/>

+    </root>

+

+</log4j:configuration>
\ No newline at end of file
Index: src/main/webapp/WEB-INF/urlrewrite.xml
===================================================================
--- src/main/webapp/WEB-INF/urlrewrite.xml	(revision 85)
+++ src/main/webapp/WEB-INF/urlrewrite.xml	(working copy)
@@ -1,9 +1,11 @@
 <?xml version="1.0" encoding="utf-8"?>
+<!DOCTYPE urlrewrite PUBLIC "-//tuckey.org//DTD UrlRewrite 3.0//EN"
+    "http://tuckey.org/res/dtds/urlrewrite3.0.dtd">
 
 <urlrewrite>
     <rule>
-        <from>^/user/(.*).html$</from>
-        <to type="forward">/editUser.html\?id=$1&amp;from=list</to>
+        <from>^/admin/user/(.*).html$</from>
+        <to type="forward">/admin/editUser.html\?id=$1&amp;from=list</to>
     </rule>
 
     <!-- Override default validation.js from WebWork -->
Index: src/main/webapp/WEB-INF/menu-config.xml
===================================================================
--- src/main/webapp/WEB-INF/menu-config.xml	(revision 85)
+++ src/main/webapp/WEB-INF/menu-config.xml	(working copy)
@@ -6,13 +6,13 @@
     <Menus>
         <Menu name="MainMenu" title="mainMenu.title" page="/mainMenu.html" roles="ROLE_ADMIN,ROLE_USER"/>
         <Menu name="UserMenu" title="menu.user" description="User Menu" page="/editProfile.html" roles="ROLE_ADMIN,ROLE_USER"/>
-        <Menu name="AdminMenu" title="menu.admin" description="Admin Menu" roles="ROLE_ADMIN" width="120" page="/users.html">
-            <Item name="ViewUsers" title="menu.admin.users" page="/users.html"/>
-            <Item name="ActiveUsers" title="mainMenu.activeUsers" page="/activeUsers.html"/>
-            <Item name="ReloadContext" title="menu.admin.reload" page="/reload.html"/>
-            <Item name="FileUpload" title="menu.selectFile" page="/uploadFile!start.html"/>
-            <Item name="FlushCache" title="menu.flushCache" page="/flushCache.html"/>
-            <Item name="Clickstream" title="menu.clickstream" page="/clickstreams.jsp"/>
+        <Menu name="AdminMenu" title="menu.admin" description="Admin Menu" roles="ROLE_ADMIN" width="120" page="/admin/users.html">
+            <Item name="ViewUsers" title="menu.admin.users" page="/admin/users.html"/>
+            <Item name="ActiveUsers" title="mainMenu.activeUsers" page="/admin/activeUsers.html"/>
+            <Item name="ReloadContext" title="menu.admin.reload" page="/admin/reload.html"/>
+            <Item name="FileUpload" title="menu.selectFile" page="/uploadFile.html"/>
+            <Item name="FlushCache" title="menu.flushCache" page="/admin/flushCache.html"/>
+            <Item name="Clickstream" title="menu.clickstream" page="/admin/clickstreams.jsp"/>
         </Menu>
         <Menu name="Logout" title="user.logout" page="/logout.jsp" roles="ROLE_ADMIN,ROLE_USER"/>
         <Menu name="PeopleMenu" title="menu.viewPeople" page="/persons.html"/>
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
     </filter>
     <filter>
@@ -166,6 +165,7 @@
         <url-pattern>/*</url-pattern>
         <dispatcher>REQUEST</dispatcher>
         <dispatcher>FORWARD</dispatcher>
+        <dispatcher>INCLUDE</dispatcher>
     </filter-mapping>
     <filter-mapping>
         <filter-name>staticFilter</filter-name>
Index: pom.xml
===================================================================
--- pom.xml	(revision 85)
+++ pom.xml	(working copy)
@@ -6,12 +6,12 @@
     <groupId>org.appfuse.tutorial</groupId>

     <artifactId>tutorial-struts2</artifactId>

     <packaging>war</packaging>

-    <version>1.0-m5</version>

+    <version>1.0</version>

     <name>AppFuse Struts 2 Application</name>

     <url>http://www.mycompany.com</url>

 

     <prerequisites>

-        <maven>2.0.4</maven>

+        <maven>2.0.6</maven>

     </prerequisites>

 

     <licenses>

@@ -22,9 +22,9 @@
     </licenses>

 

     <scm>

-        <connection>scm:svn:http://appfuse-demos.googlecode.com/svn/trunk/tutorial-struts2</connection>

-        <developerConnection>scm:svn:https://appfuse-demos.googlecode.com/svn/trunk/tutorial-struts2</developerConnection>

-        <url>http://code.google.com/p/appfuse-demos/source</url>

+        <connection></connection>

+        <developerConnection></developerConnection>

+        <url></url>

     </scm>

 

     <issueManagement>

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

@@ -80,13 +122,13 @@
             <plugin>

                 <groupId>org.codehaus.mojo</groupId>

                 <artifactId>hibernate3-maven-plugin</artifactId>

-                <version>2.0-alpha-1</version>

+                <version>2.0-alpha-2</version>

                 <configuration>

                     <components>

                         <component>

                             <name>hbm2ddl</name>

                             <implementation>annotationconfiguration</implementation>

-                            <!-- Use 'jpaconfiguration' if your going the -Ddao.framework=jpa-hibernate route. -->

+                            <!-- Use 'jpaconfiguration' if you're using JPA. -->

                             <!--<implementation>jpaconfiguration</implementation>-->

                         </component>

                     </components>

@@ -156,13 +198,22 @@
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

@@ -177,7 +228,7 @@
             <plugin>

                 <groupId>org.appfuse</groupId>

                 <artifactId>maven-warpath-plugin</artifactId>

-                <version>1.0-m5</version>

+                <version>1.0-SNAPSHOT</version>

                 <extensions>true</extensions>

                 <executions>

                     <execution>

@@ -190,21 +241,12 @@
                     <warpathExcludes>

                         applicationContext-resources.xml,ApplicationResources*.properties,ehcache.xml,

                         hibernate.cfg.xml,jdbc.properties,log4j.xml,mail.properties,**/persistence.xml,

-                        sql-map-config.xml

+                        sql-map-config.xml,struts.xml

                     </warpathExcludes>

                 </configuration>

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

@@ -220,6 +262,7 @@
                         <configuration>

                             <encoding>UTF8</encoding>

                             <includes>

+                                ApplicationResources_ko.properties,

                                 ApplicationResources_no.properties,

                                 ApplicationResources_tr.properties,

                                 ApplicationResources_zh*.properties

@@ -248,16 +291,27 @@
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

+                    <exclude>struts.xml</exclude>

                 </excludes>

                 <filtering>true</filtering>

             </resource>

+            <resource>

+                <directory>src/main/resources</directory>

+                <includes>

+                    <include>applicationContext-resources.xml</include>

+                    <include>struts.xml</include>

+                </includes>

+                <filtering>false</filtering>

+            </resource>

         </resources>

         <testResources>

             <testResource>

@@ -476,31 +530,18 @@
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

@@ -516,7 +557,7 @@
                 <jdbc.artifactId>derbyclient</jdbc.artifactId>

                 <jdbc.version>10.2.2.0</jdbc.version>

                 <jdbc.driverClassName>org.apache.derby.jdbc.ClientDriver</jdbc.driverClassName>

-                <jdbc.url><![CDATA[jdbc:derby://localhost/appfuse;create=true]]></jdbc.url>

+                <jdbc.url><![CDATA[jdbc:derby://localhost/tutorial_struts2;create=true]]></jdbc.url>

                 <jdbc.username>any</jdbc.username>

                 <jdbc.password>value</jdbc.password>

             </properties>

@@ -530,7 +571,7 @@
                 <jdbc.artifactId>h2</jdbc.artifactId>

                 <jdbc.version>1.0.20061217</jdbc.version>

                 <jdbc.driverClassName>org.h2.Driver</jdbc.driverClassName>

-                <jdbc.url><![CDATA[jdbc:h2:tutorial-struts2]]></jdbc.url>

+                <jdbc.url><![CDATA[jdbc:h2:tutorial_struts2]]></jdbc.url>

                 <jdbc.username>sa</jdbc.username>

                 <jdbc.password></jdbc.password>

             </properties>

@@ -544,7 +585,7 @@
                 <jdbc.artifactId>hsqldb</jdbc.artifactId>

                 <jdbc.version>1.8.0.7</jdbc.version>

                 <jdbc.driverClassName>org.hsqldb.jdbcDriver</jdbc.driverClassName>

-                <jdbc.url><![CDATA[jdbc:hsqldb:tutorial-struts2;shutdown=true]]></jdbc.url>

+                <jdbc.url><![CDATA[jdbc:hsqldb:tutorial_struts2;shutdown=true]]></jdbc.url>

                 <jdbc.username>sa</jdbc.username>

                 <jdbc.password></jdbc.password>

             </properties>

@@ -572,7 +613,7 @@
                 <jdbc.artifactId>postgresql</jdbc.artifactId>

                 <jdbc.version>8.1-407.jdbc3</jdbc.version>

                 <jdbc.driverClassName>org.postgresql.Driver</jdbc.driverClassName>

-                <jdbc.url><![CDATA[jdbc:postgresql://localhost/tutorial-struts2]]></jdbc.url>

+                <jdbc.url><![CDATA[jdbc:postgresql://localhost/tutorial_struts2]]></jdbc.url>

                 <jdbc.username>postgres</jdbc.username>

                 <jdbc.password>postgres</jdbc.password>

             </properties>

@@ -589,7 +630,7 @@
                 <jdbc.artifactId>jtds</jdbc.artifactId>

                 <jdbc.version>1.2</jdbc.version>

                 <jdbc.driverClassName>net.sourceforge.jtds.jdbc.Driver</jdbc.driverClassName>

-                <jdbc.url><![CDATA[jdbc:jtds:sqlserver://localhost:3683/tutorial-struts2]]></jdbc.url>

+                <jdbc.url><![CDATA[jdbc:jtds:sqlserver://localhost:3683/tutorial_struts2]]></jdbc.url>

                 <jdbc.username>sa</jdbc.username>

                 <jdbc.password>appfuse</jdbc.password>

             </properties>

@@ -615,26 +656,23 @@
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

@@ -647,7 +685,7 @@
         <jdbc.artifactId>mysql-connector-java</jdbc.artifactId>

         <jdbc.version>5.0.5</jdbc.version>

         <jdbc.driverClassName>com.mysql.jdbc.Driver</jdbc.driverClassName>

-        <jdbc.url><![CDATA[jdbc:mysql://localhost/tutorial?createDatabaseIfNotExist=true&amp;useUnicode=true&amp;characterEncoding=utf-8]]></jdbc.url>

+        <jdbc.url><![CDATA[jdbc:mysql://localhost/tutorial_struts2?createDatabaseIfNotExist=true&amp;useUnicode=true&amp;characterEncoding=utf-8]]></jdbc.url>

         <jdbc.username>root</jdbc.username>

         <jdbc.password></jdbc.password>

     </properties>
```
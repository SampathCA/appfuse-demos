
```
Index: src/test/java/org/appfuse/tutorial/webapp/action/PersonListTest.java
===================================================================
--- src/test/java/org/appfuse/tutorial/webapp/action/PersonListTest.java	(revision 85)
+++ src/test/java/org/appfuse/tutorial/webapp/action/PersonListTest.java	(working copy)
@@ -6,13 +6,18 @@
 
 public class PersonListTest extends BasePageTestCase {
     private PersonList bean;
+    private GenericManager<Person, Long> personManager;
 
-    protected void setUp() throws Exception {
-        super.setUp();
-        bean = (PersonList) getManagedBean("personList");
-        GenericManager<Person, Long> personManager =
-                (GenericManager<Person, Long>) applicationContext.getBean("personManager");
+    public void setPersonManager(GenericManager<Person, Long> personManager) {
+        this.personManager = personManager;
+    }
 
+    @Override @SuppressWarnings("unchecked")
+    protected void onSetUp() throws Exception {
+        super.onSetUp();
+        bean = new PersonList();
+        bean.setPersonManager(personManager);
+
         // add a test person to the database
         Person person = new Person();
         person.setFirstName("Abbie Loo");
@@ -20,8 +25,9 @@
         personManager.save(person);
     }
 
-    protected void tearDown() throws Exception {
-        super.tearDown();
+    @Override
+    protected void onTearDown() throws Exception {
+        super.onTearDown();
         bean = null;
     }
 
Index: src/test/java/org/appfuse/tutorial/webapp/action/PersonFormTest.java
===================================================================
--- src/test/java/org/appfuse/tutorial/webapp/action/PersonFormTest.java	(revision 85)
+++ src/test/java/org/appfuse/tutorial/webapp/action/PersonFormTest.java	(working copy)
@@ -2,18 +2,26 @@
 
 import org.appfuse.tutorial.model.Person;
 import org.appfuse.webapp.action.BasePageTestCase;
+import org.appfuse.service.GenericManager;
 
 public class PersonFormTest extends BasePageTestCase {
     private PersonForm bean;
+    private GenericManager<Person, Long> personManager;
 
-    protected void setUp() throws Exception {
-        super.setUp();
-        bean = (PersonForm) getManagedBean("personForm");
-        
+    public void setPersonManager(GenericManager<Person, Long> personManager) {
+        this.personManager = personManager;
     }
 
-    protected void tearDown() throws Exception {
-        super.tearDown();
+    @Override
+    protected void onSetUp() throws Exception {
+        super.onSetUp();
+        bean = new PersonForm();
+        bean.setPersonManager(personManager);
+    }
+
+    @Override
+    protected void onTearDown() throws Exception {
+        super.onTearDown();
         bean = null;
     }
 
Index: src/test/resources/web-tests.xml
===================================================================
--- src/test/resources/web-tests.xml	(revision 85)
+++ src/test/resources/web-tests.xml	(working copy)
@@ -73,7 +73,7 @@
             &config;
             <steps>
                 &login;
-                <invoke description="click View Users link" url="/users.html"/>
+                <invoke description="click View Users link" url="/admin/users.html"/>
                 <verifytitle description="we should see the user list title" 
                     text=".*${userList.title}.*" regex="true"/>
             </steps>
@@ -104,7 +104,7 @@
             &config;
             <steps>
                 &login;
-                <invoke description="View User List" url="/users.html"/>
+                <invoke description="View User List" url="/admin/users.html"/>
                 <clickbutton description="Click 'Add' button'" label="${button.add}"/>
                 
                 <verifytitle description="view user profile title" text=".*${userProfile.title}.*" regex="true"/>
@@ -125,15 +125,16 @@
                 
                 <verifytitle description="view user list screen" text=".*${userList.title}.*" regex="true"/>
                 <verifytext description="verify success message" regex="true"
-                    text='&lt;div class="message.*&gt;.*&lt;strong&gt;Test Name&lt;/strong&gt;.*&lt;/div&gt;'/>
+                    text='&lt;div class="message.*&gt;.*Test Name.*&lt;/div&gt;'/>
                     
                 <!-- Delete user -->
                 <clicklink description="Click edit user link" label="newuser"/>
+                <verifytitle text=".*${userProfile.title}.*" regex="true"/>
                 <prepareDialogResponse description="Confirm delete" dialogType="confirm" response="true"/>
                 <clickbutton label="${button.delete}" description="Click button 'Delete'"/>
                 <verifyNoDialogResponses/>
                 <verifytext description="verify success message" regex="true"
-                    text='&lt;div class="message.*&gt;.*&lt;strong&gt;Test Name&lt;/strong&gt;.*&lt;/div&gt;'/>
+                    text='&lt;div class="message.*&gt;.*Test Name.*&lt;/div&gt;'/>
                 <verifytitle description="display user list" text=".*${userList.title}.*" regex="true"/>
             </steps>
         </webtest>
@@ -173,7 +174,7 @@
             &config;
             <steps>
                 &login;
-                <invoke description="get activeUsers URL" url="/activeUsers.html"/>
+                <invoke description="get activeUsers URL" url="/admin/activeUsers.html"/>
                 <verifytitle description="we should see the activeUsers title" 
                     text=".*${activeUsers.title}.*" regex="true"/>
             </steps>
@@ -186,7 +187,7 @@
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
Index: src/main/resources/log4j.xml
===================================================================
--- src/main/resources/log4j.xml	(revision 85)
+++ src/main/resources/log4j.xml	(working copy)
@@ -34,7 +34,17 @@
     <logger name="org.springframework">
         <level value="WARN"/>
     </logger>
-   
+
+    <!-- Suppress warnings from Commons Validator -->
+    <logger name="org.apache.commons.validator.ValidatorResources">
+        <level value="ERROR"/>
+    </logger>
+
+    <!-- Suppress invalid warning messages from JSF -->
+    <logger name="org.apache.myfaces.shared_impl.renderkit.html">
+        <level value="ERROR"/>
+    </logger>
+
     <logger name="org.appfuse">
         <level value="INFO"/>
     </logger>
Index: src/main/webapp/WEB-INF/urlrewrite.xml
===================================================================
--- src/main/webapp/WEB-INF/urlrewrite.xml	(revision 85)
+++ src/main/webapp/WEB-INF/urlrewrite.xml	(working copy)
@@ -1,4 +1,6 @@
 <?xml version="1.0" encoding="UTF-8"?>
+<!DOCTYPE urlrewrite PUBLIC "-//tuckey.org//DTD UrlRewrite 3.0//EN"
+    "http://tuckey.org/res/dtds/urlrewrite3.0.dtd">
 
 <urlrewrite>
     <rule>
@@ -6,8 +8,8 @@
         <to type="forward">/login.jsp</to>
     </rule>
     <rule>
-        <from>^/flushCache.html$</from>
-        <to type="forward">/flushCache.jsp</to>
+        <from>^/admin/flushCache.html$</from>
+        <to type="forward">/admin/flushCache.jsp</to>
     </rule>
 </urlrewrite>
 
Index: src/main/webapp/WEB-INF/faces-config.xml
===================================================================
--- src/main/webapp/WEB-INF/faces-config.xml	(revision 85)
+++ src/main/webapp/WEB-INF/faces-config.xml	(working copy)
@@ -11,6 +11,8 @@
             <supported-locale>es</supported-locale>
             <supported-locale>de</supported-locale>
             <supported-locale>fr</supported-locale>
+            <supported-locale>it</supported-locale>
+            <supported-locale>ko</supported-locale>
             <supported-locale>nl</supported-locale>
             <supported-locale>no</supported-locale>
             <supported-locale>pt</supported-locale>
@@ -54,12 +56,12 @@
         <from-view-id>/userForm.xhtml</from-view-id>
         <navigation-case>
             <from-outcome>cancel</from-outcome>
-            <to-view-id>/users.xhtml</to-view-id>
+            <to-view-id>/admin/users.xhtml</to-view-id>
             <redirect/>
         </navigation-case>
         <navigation-case>
             <from-outcome>list</from-outcome>
-            <to-view-id>/users.xhtml</to-view-id>
+            <to-view-id>/admin/users.xhtml</to-view-id>
             <redirect/>
         </navigation-case>
     </navigation-rule>
Index: src/main/webapp/WEB-INF/menu-config.xml
===================================================================
--- src/main/webapp/WEB-INF/menu-config.xml	(revision 85)
+++ src/main/webapp/WEB-INF/menu-config.xml	(working copy)
@@ -7,13 +7,13 @@
         <Menu name="MainMenu" title="mainMenu.title" page="/mainMenu.html" roles="ROLE_ADMIN,ROLE_USER"/>
         <Menu name="UserMenu" title="menu.user" description="User Menu" page="/editProfile.html" roles="ROLE_ADMIN,ROLE_USER"/>
         <Menu name="PeopleMenu" title="menu.viewPeople" page="/persons.html"/>
-        <Menu name="AdminMenu" title="menu.admin" description="Admin Menu" roles="ROLE_ADMIN" width="120" page="/users.html">
-            <Item name="ViewUsers" title="menu.admin.users" page="/users.html"/>
-            <Item name="ActiveUsers" title="mainMenu.activeUsers" page="/activeUsers.html"/>
-            <Item name="ReloadContext" title="menu.admin.reload" page="/reload.html"/>
+        <Menu name="AdminMenu" title="menu.admin" description="Admin Menu" roles="ROLE_ADMIN" width="120" page="/admin/users.html">
+            <Item name="ViewUsers" title="menu.admin.users" page="/admin/users.html"/>
+            <Item name="ActiveUsers" title="mainMenu.activeUsers" page="/admin/activeUsers.html"/>
+            <Item name="ReloadContext" title="menu.admin.reload" page="/admin/reload.html"/>
             <Item name="FileUpload" title="menu.selectFile" page="/selectFile.html"/>
-            <Item name="FlushCache" title="menu.flushCache" page="/flushCache.html"/>
-            <Item name="Clickstream" title="menu.clickstream" page="/clickstreams.jsp"/>
+            <Item name="FlushCache" title="menu.flushCache" page="/admin/flushCache.html"/>
+            <Item name="Clickstream" title="menu.clickstream" page="/admin/clickstreams.jsp"/>
         </Menu>
         <Menu name="Logout" title="user.logout" page="/logout.jsp" roles="ROLE_ADMIN,ROLE_USER"/>
     </Menus>
Index: src/main/webapp/WEB-INF/web.xml
===================================================================
--- src/main/webapp/WEB-INF/web.xml	(revision 85)
+++ src/main/webapp/WEB-INF/web.xml	(working copy)
@@ -28,11 +28,10 @@
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
@@ -56,6 +55,7 @@
     <context-param>
         <param-name>facelets.LIBRARIES</param-name>
         <param-value>
+            /WEB-INF/taglibs/acegijsf.taglib.xml;
             /WEB-INF/taglibs/corejsf-validator.taglib.xml;
             /WEB-INF/taglibs/tomahawk.taglib.xml
         </param-value>
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
     <artifactId>tutorial-jsf</artifactId>
     <packaging>war</packaging>
-    <version>1.0-m5</version>
+    <version>1.0</version>
     <name>AppFuse JSF Application</name>
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
@@ -79,23 +121,14 @@
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
@@ -165,26 +198,24 @@
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
+                                <exclude>**/*.xhtml</exclude>
+                            </excludes>
+                            <includes>
+                                <include>**/*.properties</include>
+                                <include>**/*.xml</include>
+                            </includes>
+                        </scanTargetPattern>
+                    </scanTargetPatterns>
                 </configuration>
-                <dependencies>
-                    <dependency>
-                        <groupId>org.apache.myfaces.core</groupId>
-                        <artifactId>myfaces-impl</artifactId>
-                        <version>1.1.5</version>
-                    </dependency>
-                    <dependency>
-                        <groupId>log4j</groupId>
-                        <artifactId>log4j</artifactId>
-                        <version>1.2.13</version>
-                    </dependency>
-                </dependencies>
             </plugin>
             <plugin>
                 <artifactId>maven-war-plugin</artifactId>
@@ -198,7 +229,7 @@
             <plugin>
                 <groupId>org.appfuse</groupId>
                 <artifactId>maven-warpath-plugin</artifactId>
-                <version>1.0-m5</version>
+                <version>1.0-SNAPSHOT</version>
                 <extensions>true</extensions>
                 <executions>
                     <execution>
@@ -232,6 +263,7 @@
                         <configuration>
                             <encoding>UTF8</encoding>
                             <includes>
+                                ApplicationResources_ko.properties,
                                 ApplicationResources_no.properties,
                                 ApplicationResources_tr.properties,
                                 ApplicationResources_zh*.properties
@@ -260,16 +292,25 @@
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
@@ -338,7 +379,7 @@
         </dependency>
         <!-- Dependencies with scope=provided aren't picked up from dependent JARs -->
         <dependency>
-            <groupId>javax.servlet</groupId>
+            <groupId>javax.servlet.jsp</groupId>
             <artifactId>jsp-api</artifactId>
             <version>${jsp.version}</version>
             <scope>provided</scope>
@@ -362,6 +403,12 @@
             <scope>test</scope>
         </dependency>
         <dependency>
+            <groupId>org.apache.shale</groupId>
+            <artifactId>shale-test</artifactId>
+            <version>${shale.version}</version>
+            <scope>test</scope>
+        </dependency>
+        <dependency>
             <groupId>org.springframework</groupId>
             <artifactId>spring-mock</artifactId>
             <version>${spring.version}</version>
@@ -488,36 +535,39 @@
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
             </build>
         </profile>
+
+        <!-- ================= Production Profile ================ -->
+        <profile>
+            <id>prod</id>
+            <build>
+                <plugins>
+                    <!-- Override location of data file for DbUnit to load (doesn't have negative keys) -->
+                    <plugin>
+                        <artifactId>dbunit-maven-plugin</artifactId>
+                        <configuration>
+                            <src>src/main/resources/default-data.xml</src>
+                        </configuration>
+                    </plugin>
+                </plugins>
+            </build>
+        </profile>
         
         <!-- ================= Database Profiles ================= -->
         <profile>
@@ -528,7 +578,7 @@
                 <jdbc.artifactId>derbyclient</jdbc.artifactId>
                 <jdbc.version>10.2.2.0</jdbc.version>
                 <jdbc.driverClassName>org.apache.derby.jdbc.ClientDriver</jdbc.driverClassName>
-                <jdbc.url><![CDATA[jdbc:derby://localhost/appfuse;create=true]]></jdbc.url>
+                <jdbc.url><![CDATA[jdbc:derby://localhost/tutorial_jsf;create=true]]></jdbc.url>
                 <jdbc.username>any</jdbc.username>
                 <jdbc.password>value</jdbc.password>
             </properties>
@@ -542,7 +592,7 @@
                 <jdbc.artifactId>h2</jdbc.artifactId>
                 <jdbc.version>1.0.20061217</jdbc.version>
                 <jdbc.driverClassName>org.h2.Driver</jdbc.driverClassName>
-                <jdbc.url><![CDATA[jdbc:h2:tutorial-jsf]]></jdbc.url>
+                <jdbc.url><![CDATA[jdbc:h2:tutorial_jsf]]></jdbc.url>
                 <jdbc.username>sa</jdbc.username>
                 <jdbc.password></jdbc.password>
             </properties>
@@ -556,7 +606,7 @@
                 <jdbc.artifactId>hsqldb</jdbc.artifactId>
                 <jdbc.version>1.8.0.7</jdbc.version>
                 <jdbc.driverClassName>org.hsqldb.jdbcDriver</jdbc.driverClassName>
-                <jdbc.url><![CDATA[jdbc:hsqldb:tutorial-jsf;shutdown=true]]></jdbc.url>
+                <jdbc.url><![CDATA[jdbc:hsqldb:tutorial_jsf;shutdown=true]]></jdbc.url>
                 <jdbc.username>sa</jdbc.username>
                 <jdbc.password></jdbc.password>
             </properties>
@@ -584,7 +634,7 @@
                 <jdbc.artifactId>postgresql</jdbc.artifactId>
                 <jdbc.version>8.1-407.jdbc3</jdbc.version>
                 <jdbc.driverClassName>org.postgresql.Driver</jdbc.driverClassName>
-                <jdbc.url><![CDATA[jdbc:postgresql://localhost/tutorial-jsf]]></jdbc.url>
+                <jdbc.url><![CDATA[jdbc:postgresql://localhost/tutorial_jsf]]></jdbc.url>
                 <jdbc.username>postgres</jdbc.username>
                 <jdbc.password>postgres</jdbc.password>
             </properties>
@@ -601,7 +651,7 @@
                 <jdbc.artifactId>jtds</jdbc.artifactId>
                 <jdbc.version>1.2</jdbc.version>
                 <jdbc.driverClassName>net.sourceforge.jtds.jdbc.Driver</jdbc.driverClassName>
-                <jdbc.url><![CDATA[jdbc:jtds:sqlserver://localhost:3683/tutorial-jsf]]></jdbc.url>
+                <jdbc.url><![CDATA[jdbc:jtds:sqlserver://localhost:3683/tutorial_jsf]]></jdbc.url>
                 <jdbc.username>sa</jdbc.username>
                 <jdbc.password>appfuse</jdbc.password>
             </properties>
@@ -610,6 +660,14 @@
         <!-- ================= Container Profiles ================= -->
         <profile>
             <id>jboss</id>
+            <!-- Add el-api dependency since JBoss 4.0.5 uses Tomcat 5.5.x and JBoss 4.2.0 doesn't work with Cargo -->
+            <dependencies>
+                <dependency>
+                    <groupId>javax.el</groupId>
+                    <artifactId>el-api</artifactId>
+                    <version>${el.version}</version>
+                </dependency>
+            </dependencies>
             <properties>
                 <cargo.container>jboss4x</cargo.container>
                 <cargo.container.home>${env.JBOSS_HOME}</cargo.container.home>
@@ -619,33 +677,32 @@
     </profiles>
     
     <properties>
+        <!-- Application settings -->
         <copyright.year>2007</copyright.year>
         <dao.framework>hibernate</dao.framework>
         <web.framework>jsf</web.framework>
         <amp.genericCore>true</amp.genericCore>
         <amp.fullSource>false</amp.fullSource>
         
-		<!-- Framework dependency versions -->
-        <appfuse.version>2.0-m5</appfuse.version>
-        <spring.version>2.0.5</spring.version>
+        <!-- Framework dependency versions -->
+        <appfuse.version>2.0-SNAPSHOT</appfuse.version>
+        <spring.version>2.0.6</spring.version>
 
         <!-- Testing dependency versions -->
         <jmock.version>1.1.0</jmock.version>
-        <jsp.version>2.0</jsp.version>
-        <junit.version>3.8.2</junit.version>
+        <jsp.version>2.1</jsp.version>
+        <junit.version>4.4</junit.version>
         <servlet.version>2.4</servlet.version>
-        <wiser.version>1.0.3</wiser.version>
+        <shale.version>1.0.4</shale.version>
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
@@ -658,7 +715,7 @@
         <jdbc.artifactId>mysql-connector-java</jdbc.artifactId>
         <jdbc.version>5.0.5</jdbc.version>
         <jdbc.driverClassName>com.mysql.jdbc.Driver</jdbc.driverClassName>
-        <jdbc.url><![CDATA[jdbc:mysql://localhost/tutorial?createDatabaseIfNotExist=true&amp;useUnicode=true&amp;characterEncoding=utf-8]]></jdbc.url>
+        <jdbc.url><![CDATA[jdbc:mysql://localhost/tutorial_jsf?createDatabaseIfNotExist=true&amp;useUnicode=true&amp;characterEncoding=utf-8]]></jdbc.url>
         <jdbc.username>root</jdbc.username>
         <jdbc.password></jdbc.password>
     </properties>

```

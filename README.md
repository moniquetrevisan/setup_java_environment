# Configurações Gerais 

------------------------------------
Setup da Maquina
------------------------------------
0. Organização dos arquivos
  - c:\dev\codes -> todos os códigos dos projetos (lugar onde daremos os git clones)
  - c:\dev\soft -> Instaladores e programas
  
1. Configurar o java
  - variaveis de ambiente
    JAVA_HOME = c:\dev\soft\Java\jdk1.8.0_171
    JAVA_TOOL_OPTIONS = -Dfile.encoding=UTF8
    JRE_HOME = c:\dev\soft\Java\jre1.8.0_171
2. Configurar o maven
  - variaveis de ambiente
    - M2_HOME = c:\dev\soft\apache-maven-3.5.2
    - M2_REPO = c:\dev\soft\.m2\repository
    - ir na pasta conf do maven e editar o settings para usar as configurações da bolsa e apontar o localRepository para onde vc configurou a variavel M2_REPO
      ex: <localRepository>c:\dev\soft\.m2\repository</localRepository>
      
3. Configurar o eclipse
  - acertar a instalação do java e apontar sempre para a JDK
    Preferences > Java > Installed JREs > Add... > caminho da sua JAVA_HOME
  - acertar a configuração do maven para ele não usar o padrão dele
    Preferences > Maven > Installations > Add... > caminho da sua M2_HOME
    Preferences > Maven > User Settings > User Settings > Browse... > caminho M2_HOME\conf\settings.xml 
    Preferences > Maven > User Settings > User Settings > Browse... > Update Settings 
    Preferences > Maven > User Settings > User Settings > Browse... > Local Repository > Reindex 

4. Baixar os projetos do git
  - Abrir o GitBash e ir na pasta c > dev > codes 
  - Pegar a URL do clone no BitBucket  
    $ git clone <url_copiada>
  - Executar o comando (tanto faz se for no cmd ou no próprio GitBash)
    $ mvn clean install
    $ mvn eclipse:clean (apaga os .project etc...limpa as referencias dos objetos etc)
    $ mvn eclipse:eclipse (ele recria as referencias e ponteiros)
    
5. Configurar workspace no Eclipse
  - criar uma pasta workspace separada do codigo do projeto para evitar erros bizarros
  - criar um workpace por contexto de projeto (um workpace para nemo/crr juntos...etc)
  - Configurar o proxy
    Preferences > General > Network Connections > Active Provider: Manual
  - baixo os plugins que eu já sei que eu gosto e baixo do Eclipse Marketplace - Recomendação
    Eclipse Web Developer Tools
    Eclipse XML Editors and Tools
    STS - Spring Tools (para aquele search rapidao)
	JAD ou algum decompilador
  - Viadagens da cor - Opcional
    Preferences > General > Editors > Text Editors > Line number foreground (cor dos numeros da linha)
    Preferences > General > Editors > Text Editors > Current line highlight (cor da linha atual - gosto de (160,0,181))
    Preferences > General > Editors > Text Editors > Annotations > Occurrences (140,240,120)
    Preferences > General > Editors > Text Editors > Annotations > Search Results (160,240,180)
    Preferences > General > Editors > Text Editors > Selecionar displayed tab width 4, highlight current line, show line numbers
  - Importar os projetos
    File > Import > Maven > Existing Maven Projects
  - Arrumar a ordem dos pacotes (durante o comando mvn eclipse:eclipse ele coloca a pasta de testes pra cima da de java)
    Botao Direito no Projeto > Properties > Java Build Path > Order and Export > padrão geralmente usado:
      src/main/java
      src/main/resources
      src/test/java
      src/test/resources
  - Conferir que o projeto está marcado como maven - Botão Direito no projeto - se nao aparecer a opção Maven logo de cara...
    Botão Direito > Configure > Convert to Maven Project
    
------------------------------------------
Conectar ao JConsole
------------------------------------------
para conexao remota:
executar no cmd
C:\Development\Softwares\Java\jdk1.8.0_74\bin\jconsole.exe -J-Djava.class.path=%JAVA_HOME%\lib\jconsole.jar;%JAVA_HOME%\lib\tools.jar;C:\Development\jmxremote_optional-repackaged-4.1.1.jar

remote process
service:jmx:jmxmp://localhost:9987 (substituir o localhost pelo servidor e porta que quer ver remoto)
  
------------------------------------------
Comandos linux
------------------------------------------
-------------
greps
-------------
grep --color 'SLOW database activity' NemoSushi_0*.log.0|awk '{ print $12}'|sort -nr|more
grep 'stats' NemoSushi_0*.log.0|awk '{ print $5}'|grep -v 'time'|grep -v 'initLog'>NemoSushi_Stats.csv
-Fazer grep de uma string e alterar para string2
grep -rl MobyTOB /apps/puma/MobyMBP/ | xargs sed -i 's/MobyTOB/MobyMBP/g'
-apenas para ver a ocorrencia
grep -rl MobyTOB /apps/puma/MobyMBP/

-------------
VI Comandos
-------------
- find and replace
:%s/NemoFalcon/MobyMBO/g

- ver a memoria da maquina de forma detalhada
head -1 /proc/meminfo

- descobrir hostname a partir de IP
nslookup -A "ipdesejado" 

-ver as interfaces de rede da maquina
netstat -g

-looping infinito para rodar o seeAll
while true; do ./seeAll; sleep 2; done

- link simbolico
ln -sf <origem> <destino>


### JVM ARGS ###
-Dcatalina.home=C:\dev\epuma\jws-3.0\share\apache-tomcat-8.0.18 -Dcatalina.base=C:\dev\epuma\jws-3.0\share\apache-tomcat-8.0.18 -Dcatalina.config=file:C:\epumacfg\catalina.properties -Djava.util.logging.manager=org.apache.juli.ClassLoaderLogManager -Djava.util.logging.config.file=C:\epumacfg\logging.properties -Dlog4j.configuration=file:C:\epumacfg\log4j.xml -Dorg.owasp.esapi.resources=C:\epumacfg -DEPUMA_HOME=C:\dev\epuma -DServerConfigDir=C:\epumacfg -DenvironmentFilePath=C:\epumacfg\environment.properties -DldapCertificateFilePath=C:\epumacfg\bvmfldapcacerts -DldapPropertiesFilePath=C:\epumacfg\ldapBVMF.properties -DldapCertificateCORPFilePath=C:\epumacfg\bvmfldapcacerts -DldapPropertiesCORPFilePath=C:\epumacfg\ldapBVMFCORP.properties -DwebServicesURLFilePath=C:\epumacfg\webServicesURL.properties -DuseLDAPCorporate=false -Dlogfile.location=C:\dev\epuma\log\epuma-web.log -DlogfileAPILDAP.location=log/epuma-security.log 

-Dcatalina.base="C:\workspace\pcopuma_workspace\.metadata\.plugins\org.eclipse.wst.server.core\tmp0" -Dcatalina.home="C:\dev\jws-3.0\share\apache-tomcat-8.0.18" -Dwtp.deploy="C:\workspace\pcopuma_workspace\.metadata\.plugins\org.eclipse.wst.server.core\tmp0\wtpwebapps" -Djava.endorsed.dirs="C:\dev\jws-3.0\share\apache-tomcat-8.0.18\endorsed" -Dspring.config.location="C:\dev\pcopuma\cfg\application.properties"   -Denvironment=DEV

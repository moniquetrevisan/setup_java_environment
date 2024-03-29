# Configurações Gerais 

## Setup da Máquina

### Organização dos arquivos
- c:\dev\codes -> todos os códigos dos projetos (lugar onde daremos os git clones)
- c:\dev\soft  -> Instaladores e programas
  
### Java
Fazer download dos pacotes do java, e para desenvolver, precisamos ter o runtime do Java (conhecido como jre) e também os pacotes de desenvolvedor que estão dentro da jdk (Java Development Kit) 

Quando fazemos o download da jdk, os pacotes de runtime (jre) estão incluídos. 
Download: https://www.oracle.com/technetwork/java/javase/downloads/jdk8-downloads-2133151.html
Faça o download da versão x64

IMPORTANTE: Caso você já tenha alguma versão de Java instalado, eu aconselho desinstalar e deixar somente a mais atual, pois as vezes acontece alguns problemas de ambiente que são relacionados a diferentes versões de Java na máquina. 
O melhor jeito de você instalar o Java, na verdade é apenas pegar os zips que serão obtidos no download, e fazer os apontamentos de onde está o Java através de variáveis de ambiente. Isso vale, inclusive, para o linux. 

As variáveis de ambiente necessárias são:
- JAVA_HOME = c:\dev\soft\Java\jdk1.8.0_171
- JAVA_TOOL_OPTIONS = -Dfile.encoding=UTF8
- JRE_HOME = c:\dev\soft\Java\jre1.8.0_171

Após criar as variáveis de ambiente, abra um cmd e digite o comando "java -version"
A saída será alguma coisa parecida com isso:
C:\Users\mvolpe>java -version
Picked up JAVA_TOOL_OPTIONS: -Dfile.encoding=UTF8
java version "1.8.0_171"
Java(TM) SE Runtime Environment (build 1.8.0_171-b11)
Java HotSpot(TM) 64-Bit Server VM (build 25.171-b11, mixed mode)


### Maven
A próxima tecnologia que vamos utilizar é o Maven.
O maven é basicamente uma ferramenta que organiza as dependências (imports) do seu projeto, compila o código e gera os diferentes tipos de binários que temos em Java (war, jar, etc).
Para saber mais sobre isso, acesse o link deles: https://maven.apache.org/what-is-maven.html 

Para instalar ele, precisamos apenas fazer o download dele, e apontarmos sua localização via variáveis de ambiente.
Para isso, vamos precisar da variável que indica seu caminho (M2_HOME) e da variável que vai indicar onde ele vai organizar o repositório local (M2_REPO).

variáveis de ambiente
- M2_HOME = c:\dev\soft\apache-maven-3.5.2
- M2_REPO = c:\dev\soft\.m2\repository

### GIT
Para conseguirmos organizar os códigos, e fazer controle de versão vamos utilizar o git como ferramenta de controle de versão. Se você não sabe nada sobre isso, ou precisa de ajudar para configurar o git, eu aconselho muito que você assista esse curso do udacity: https://www.udacity.com/course/how-to-use-git-and-github--ud775 
- Comando para atualizar o password armazenado: git config credential.helper store

### Clonar Projetos / Compilar código
Abrir o GitBash e ir na pasta "c>dev>codes"
Pegar a URL do clone no GitHub  
- $ git clone <url_copiada>
Executar os seguintes comandos para compilar o código (algum terminal: cmd, powershell, gitbash...)
- $ mvn clean install
- $ mvn eclipse:clean (apaga os .project etc...limpa as referências dos objetos etc)
- $ mvn eclipse:eclipse (ele recria as referências e ponteiros para navegação no código)
    
-----------------------------------------------------------------------------------------------------------------------------------
## Comandos/Dicas Úteis 

### Conectar ao JConsole
para conexão remota executar no cmd
- C:\Development\Softwares\Java\jdk1.8.0_74\bin\jconsole.exe -J-Djava.class.path=%JAVA_HOME%\lib\jconsole.jar;%JAVA_HOME%\lib\tools.jar;C:\Development\jmxremote_optional-repackaged-4.1.1.jar

remote process
service:jmx:jmxmp://localhost:9987 (substituir o localhost pelo servidor e porta que quer ver remoto)
  
### Greps
- grep --color 'SLOW database activity' Log_0*.log.0|awk '{ print $12}'|sort -nr|more
- grep 'stats' Log_0*.log.0|awk '{ print $5}'|grep -v 'time'|grep -v 'initLog'>Log_Stats.csv
Fazer grep de uma string1 e alterar para string2
- grep -rl string1 <dir> | xargs sed -i 's/string1/string2/g'
Apenas para ver a ocorrência
- grep -rl string1 <dir>


### VI / Linux Comandos
find and replace
- :%s/string1/string2/g

ver a memória da máquina de forma detalhada
- head -1 /proc/meminfo

descobrir hostname a partir de IP
- nslookup -A "ipdesejado" 

ver as interfaces de rede da máquina
- netstat -g

looping infinito para rodar algum script para sempre
- while true; do ./seeAll; sleep 2; done

link simbólico
- ln -sf _origem _destino

### JVM ARGS Exemplos
-Dcatalina.base="C:\workspace\proj_workspace\.metadata\.plugins\org.eclipse.wst.server.core\tmp0" -Dcatalina.home="C:\dev\jws-3.0\share\apache-tomcat-8.0.18" -Dwtp.deploy="C:\workspace\proj_workspace\.metadata\.plugins\org.eclipse.wst.server.core\tmp0\wtpwebapps" -Djava.endorsed.dirs="C:\dev\jws-3.0\share\apache-tomcat-8.0.18\endorsed" -Dspring.config.location="C:\dev\proj\cfg\application.properties"   -Denvironment=DEV

### Agile Coach Atlassian
Link para um entendimento completo sobre scrum e agile
https://br.atlassian.com/agile/scrum 

Outras referências:
https://www.scrumguides.org/scrum-guide.html 

### idle.vbs
Dim objResult

Set objShell = WScript.CreateObject("WScript.Shell")

Do While True
  objResult = objShell.sendkeys("{NUMLOCK}{NUMLOCK}")
  Wscript.Sleep(6000)
Loop

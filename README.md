maven2-repository
=================

To update the contents of this repository
-----------------------------------------

The following profile has to be defined in `~/.m2/settings.xml` or `pom.xml`

    	<profile>
    		<id>local-deploy</id>
    		<activation>
    			<property>
    				<name>repo.path</name>
    			</property>
    		</activation>
    		<repositories>
    			<repository>
    				<id>internal.repo</id>
    				<name>Repository in local machine</name>
    				<url>file://${repo.path}</url>
    			</repository>
    		</repositories>
    	</profile>

Example. For:

    File: util-lib.jar
    GroupId: com.utils
    ArtifactId: util-lib
    Version: 1.0
    Path to this repository: c:\maven2-repository    
    
Call:

    mvn deploy:deploy-file -DgroupId=com.utils -DartifactId=util-lib -Dversion=1.0 -Dfile=util-lib.jar -Drepo.path=c:/maven2-repository -DrepositoryId=internal.repo -Durl=file://c:/maven2repository

The file deploy-file-to-github.launch can be imported in the Eclipse IDE launch configurations to help with this procedure.

To deploy the current project, call:

    mvn deploy -Drepo.path=c:/maven2-repository -DrepositoryId=internal.repo

To use  this repository
-----------------------

If the contents have been pushed to GitHub, it will be available configuring the following repositories in a profile in
 `settings.xml`:
 
    <profile>
      <id>maven-vfs-plugin-repo</id>
		<repositories>
			<repository>
				<id>maven-vfs-plugin-github</id>
				<url>https://comundus.github.io/maven2-repository</url>
			</repository>
		</repositories>
		<pluginRepositories>
			<pluginRepository>
				<id>maven-vfs-plugin-github</id>
				<url>https://comundus.github.io/maven2-repository</url>
				<snapshots>
					<enabled>false</enabled>
				</snapshots>
			</pluginRepository>
		</pluginRepositories>
    </profile>


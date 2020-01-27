# Portshift Jenkins CI Plugin #
Enables scanning of docker images for vulnerabilities and report to Portshift server.

## Prerequisites for the plugin to be operational ##

1. Docker must be installed on the same machine Jenkins is installed. If your job is configured to use a node other than Master node, then Docker is required only on the build Jenkins node (slave). 
2. The *jenkins* user must be added to the *docker* group so it has permission to run Docker:

     ```
     sudo usermod -aG docker jenkins
     ```
## Install and configure the plugin
 1. In Jenkins, select **Manage Jenkins** and then select **Manage Plugins** from the list. Make sure that the list of available plugins is up to date. 
2. Select the **Available** tab, search for Portshift Vulnerability Scanner, and select it.  Click on **Download the Plugin**. This will install the plugin.

![](images/Jenkins-plugin-installed.png)

3. In Jenkins, select **Manage Jenkins**, then select **Configure System**. Enter the token value.

![](images/Jenkins-configure-plugin.png)


## Use the plugin
You can use the plugin in the build process in Freestyle and Pipelines jobs. You can configure the job to scan the image during the build process.

### Freestyle jobs

In Freestyle jobs add a build step to scan the image with Portshift, as part of the job configuration. 
1. In Jenkins, in the **Configure** page for a job, click **Add Build Step**.
2. Select Portshift Vulnerability Scanner.

![](images/Jenkins-build-freestyle.png)

3. Enter the image name.

### Pipeline jobs
In Pipeline jobs, the build step to scan the image with Portshift is included in a pipeline script, as part of the job configuration.

1. In Jenkins, in the **Configure **page for a job, scroll to the **Pipeline **section.
1. Add the a snippet such as the following to the pipeline script, to include a step to scan the image. 

![](images/Jenkins-build-pipeline.png)
3. Alternatively, you can use the Snippet Generator to create the snippet.

![](images/Jenkins-build-pipeline-script-generator.png)

## Plugin Output

You can see the results of the scan in the Console Output.

![](images/Jenkins-console-output.png)

You can also see results of the scan as an HTML page. An artifact named "scanResults.html" will be created in the project's workspace. In the Jenkins build menu, select Portshift Vulnerability Scanner, and then select the job whose results you wish to see.

![](images/Jenkins-html-output.png)


## Build the plugin (instructions for Ubuntu)

* If JDK 7 is not installed, install it
```
     sudo apt-get update
     sudo apt-get install openjdk-8-jdk
```

* Install Maven3 (must be 3)

*  Build

   When in the root directory, where *pom.xml* resides:
```
     mvn package
```
   **Note**: the first time this command is invoked, many downloads will occur and it will take quite some time.


## Publicly release a new version to jenkins-ci.org ##
See https://wiki.jenkins-ci.org/display/JENKINS/Hosting+Plugins#HostingPlugins-Releasingtojenkinsci.org. It describes several alternatives; use the following:

1. If not already done, create a *settings.xml* file with your credentials as described
2. Execute and accept defaults for prompts :
```
    mvn release:prepare release:perform
````

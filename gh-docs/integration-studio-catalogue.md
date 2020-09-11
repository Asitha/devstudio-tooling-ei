# WSO2 Integration Studio Catalogue

## High Level Architecture
![](https://i.imgur.com/dpc4WLw.png)


* **A->** GMF uses the EMF model to generate graphical elements, tool palette, etc.
* **B->** GEF (a lightweight graphical framework, based on MVC architecture) creates the Controller Classes for graphical objects of GMF.
* **C->** Integration Studio uses the GMF generated Graphical objects to create synapse mediation on a drag and drop interface.
* **D->** EEF framework uses the EMF model to generate the properties’ view for mediators, proxies, and other synapse artifacts.
* **E->** The Integration Studio uses an EEF generated Properties view as the view to configure the properties of synapse components.


### Eclipse EMF Framework
Eclipse EMF is a modeling framework, and it provides a code generation facility for building tools and other applications based on a structured data model. From a model specification described in XMI, EMF provides tools and runtime support to produce a set of Java classes for the model along with a set of adapter classes that enables viewing and command-based editing of the model, and a basic editor.

### Eclipse GMF Framework
The GMF Runtime is an application framework for creating graphical editors using EMF and GEF. GMF generates reusable components for graphical editors(ESB editor) such as drag and drop actions and toolbars(Mediator Palette), and much more. It is a standardized model to describe diagram elements which separates between the semantic (domain) and notation (diagram) elements. A command infrastructure that bridges the different command frameworks is used by EMF and GEF.
### Eclipse GEF Framework
The Eclipse Graphical Editing Framework (GEF) provides Eclipse-integrated end-user tools in terms of Graph visualization (The graphical components of the Integration Studio follow a graph style representation)
### Eclipse EEF Framework
EEF is a presentation framework for the Eclipse Modeling Framework (EMF). It allows users to create rich user interfaces (Properties view of ESB components like mediators, proxies, API resources, Inbound Endpoints, etc.) to edit EMF models.

### How is the Integration Studio designed with Eclipse Frameworks?
The Integration Studio IDE is an Eclipse Oxygen based Rich Client Platform(RCP). All the synapse level constructs (including mediators, proxies, inbound endpoints, etc), are first described as an XMI model using the Eclipse Modeling Framework(EMF). The EMF XMI model is in the devstudio-tooling-esb repository: https://github.com/wso2/devstudio-tooling-esb/blob/master/plugins/org.wso2.developerstudio.eclipse.gmf.esb/model/esb.ecore
Then, the EMF framework generates the model classes for the MVC architecture. 
The EMF generated classes include Mediators(Interface of the model), and MediatorImpl(model).

GMF “provides a generative component and runtime infrastructure for developing graphical editors based on EMF and GEF”, that is, it acts as a bridge between EMF (that allows the model definition) and GEF (a lightweight graphical framework, based on MVC architecture), generating the complete infrastructure needed to coordinate the model objects’ lifecycle (EMF EObject) and their corresponding graphical representation (GEF EditPart).
All the GMF related model files can be found at https://github.com/wso2/devstudio-tooling-esb/tree/master/plugins/org.wso2.developerstudio.eclipse.gmf.esb/model

Finally, using the EEF framework, the Classes related to the Properties view are generated. The EEF model is deduced from the EMF model(.ecore file). The EEF model is hosted at https://github.com/rosensilva/devstudio-tooling-esb/blob/ec4f86d2a46bb23a6a1933b65bcf3e4603375253/plugins/org.wso2.developerstudio.eclipse.gmf.esb.edit/model/esb.components

# Introduction to the repos

## Integration Studio Kernel(https://github.com/wso2/developer-studio)


WSO2 Developer Studio Kernel provides a set of common plugins, which can be used to develop Eclipse plugins for WSO2 products that are based on WSO2 Carbon platform. All the product specific plugins will use the Developer Studio Kernel as the base for their respective tooling implementation.

#### Integration Studio kernel has following key capabilities

* A UI toolkit that will generate UIs using XML instead of visually designing
* A platform and a framework to use web technologies for plugin development
* Large number of reusable built-in UI Component for plugin development (SWT Composites)
* Built-in template support for rapid development
* Provide Maven utilities to add maven support for developed plugins
* Built in support for CApp and Carbon servers
* Seamless integration with Eclipse, Developer Studio kernel and other plugin features using extension points

## Integration Studio Platform(https://github.com/wso2/devstudio-tooling-platform)
WSO2 Developer Studio Platform acts as a middle layer from Devleoper Studio Kernel to Developer Studio product Tooling by bridging the gap for carbon specific requirement implementation on top of Eclipse.

#### WSO2 Developer Studio Platform has following key capabilities

* Provide Maven utilities to add maven support for developed plugins
* Built in support for CApp and Carbon servers
* Seamless integration with Eclipse, Developer Studio kernel and other plugin features using extension points
* Connectivity to Carbon Servers and WSO2 cloud
* Developer Studio Platform will provide comprehensive support for developing tools and speedup the development process by providing generic Carbon based implementations and requirements.

## ESB Tooling(https://github.com/wso2/devstudio-tooling-esb)
WSO2 ESB tooling provides capabilities of a complete eclipse-based development environment for the ESB. You can develop services, features and artifacts as well as manage their links and dependencies through a simplified graphical editor via WSO2 ESB tooling. 
#### WSO2 ESB Tooling has the following key capabilities
* Develop ESB configurations (Proxy, API, Sequence, etc.) for the runtime
* Debug ESB configurations using the mediation debugger
* Mapping data across different formats using data mapper
* Deploying ESB configurations directly to local and remote ESB instances
* Provides a graphical editor to build ESB configurations in a drag and drop manner

## DSS Tooling(https://github.com/wso2/devstudio-tooling-dss)
WSO2 DSS tooling provides capabilities of a complete eclipse-based development environment for the DSS. You can develop dss artifacts through a simplified graphical editor via WSO2 DSS tooling.
#### WSO2 DSS Tooling has following key capabilities
Develop Data Services for the runtime Develop Data Source configurations Deploy DSS configurations directly to local and remote DSS instances Provides a graphical editor to develop Data Services configurations

## BPS Tooling(https://github.com/wso2/devstudio-tooling-bps)
BPS Tooling repo is maintained for the Business Process development of WSO2 Enterprise Integrator. Devstudio Tooling for BPS project contains two main components,
* BPEL Editor
* Human Task Editor

## Integration Studio EI(https://github.com/wso2/devstudio-tooling-ei)
Integration Studio EI contains the source code to create Eclipse RCP(Rich Client Application) for WSO2 Enterprise Integrator. This will package all the WSO2 Enterprise Integrator tooling plugins into one WSO2 branded eclipse based RCP application. Also, this will contain the packaging of third-party components such as Adopt OpenJDK, Maven, WSO2 Micro-integrator, WSO2 Monitoring dashbord, HTTP4e client, etc.



## Setting up Integration Studio for Developers
1. Download [Eclipse IDE Oxygen IDE](https://www.eclipse.org/downloads/packages/release/oxygen/3a) based on the OS [Eclipse IDE for Java EE Developers]
2. Use [JDK 8u202](https://www.oracle.com/java/technologies/javase/javase8-archive-downloads.html) for development(Other java versions might not work).
3. Import the Kernel source to eclipse. 
    * Clone Integration Studio kernal repository https://github.com/wso2/developer-studio.
    * Switch to **developer-studio-kernel-4.3.0_update** branch
    * Build the branch using maven
    * Import the **plugins directory** to the eclipse workspace by  selecting **File -> Import -> General -> Existing Projects into workspace** 
    * Untick the **plugins** project and select the rest plugins when importing the plugins folder

4. Import the Platform source to eclipse. 
    * Clone Integration Studio platform repository https://github.com/wso2/devstudio-tooling-platform.
    * Import the **plugins directory** to the eclipse workspace by  selecting **File -> Import -> General -> Existing Projects into workspace** 
    * Untick the **plugins** project and select the rest plugins when importing the plugins folder

5. Import the ESB source to eclipse. 
    * Clone Integration Studio platform repository https://github.com/wso2/devstudio-tooling-esb.
    * Import the **plugins directory** to the eclipse workspace by  selecting **File -> Import -> General -> Existing Projects into workspace** 
    * Untick the **plugins** project and select the rest plugins when importing the plugins folder

6. Import the EI source to eclipse. 
    * Clone Integration Studio platform repository https://github.com/wso2/devstudio-tooling-ei.
    * Import the **plugins directory** to the eclipse workspace by  selecting **File -> Import -> General -> Existing Projects into workspace** 
    * Untick the **plugins** project and select the rest plugins when importing the plugins folder

7. Install Modeling features(EMF) to eclipse
    * Click on Help -> Install New Software
    * Select **Oxygen - http://download.eclipse.org/releases/oxygen/** from work with drop down list 
    * Click on **Modeling** checkbox in the install window
    * Then untick **Contact all updates sites during install to find required software** and Click on **Next**
    * Then you will get Install details page, again click on **Next**
    * Then in the Review Licenses page (Select one licence form the list), click on **I accept the terms of the license agreements** and click on **Finish**
    * It will take sometime to install the software, during the process you will get a security warning pop-up, click on **Install anyway**.
    * Then it will ask to restart the server, click on **Yes**.

8. Install GMF related tooling runtime for oxygen, using the p2. (some features might not be able to install but install what is allowed)
    * Click on **Help** -> Install New Software
    * Click on **Add** -> Add the url http://download.eclipse.org/modeling/gmp/gmf-tooling/updates/releases/ into **Location**, and click OK.
    * Select only **GMF Tooling** from the dropdown list.
    * Then untick **Contact all updates sites during install to find required software** and Click on **Next**
    * Then, you will get the Install details page, again click on **Next**.
    * In the next page, accept the licence (Select **I accept the terms of the license agreements** and click on **Finish**)
    * It will take sometime to install the selected software.
    * Finally, it will ask to restart the eclipse, click on **Yes**.

9. Copy micro-integrator runtime eclipse 
    * Create a directory under the eclipse directory (macOS: /Applications/Eclipse.app/Contents/Eclipse/, Linux/Windows /eclipse directory) as **/runtime/microesb/** 
    * Download and copy the contents of micro integrator runtime to the folder created in the above step


10. [Optional - add only if you need to work on DSS] Import DSS and BPS Source to eclpise.
    * Clone Integration Studio DSS repository https://github.com/wso2/devstudio-tooling-dss.
    * Import the **plugins directory** to the eclipse workspace by  selecting **File -> Import -> General -> Existing Projects into workspace** 
    * Untick the **plugins** project and select the rest plugins when importing the plugins folder

11. [Optional - add only if you need to work on BPS] Import BPS and BPS Source to eclpise.
    * Clone Integration Studio DSS repository https://github.com/wso2/devstudio-tooling-bps.
    * Import the **plugins directory** to the eclipse workspace by  selecting **File -> Import -> General -> Existing Projects into workspace** 
    * Untick the **plugins** project and select the rest plugins when importing the plugins folder

## Running Integration Studio in Developer Mode

* Running the tool from the source
    1. Right click on an imported plugin
    2. Click on Run As -> Run Configurations
    3. Create a new Eclipse Application
    4. Click on Run
    
    This will open an eclipse instance which contains tooling plugins

* Debugging the source
    1. Right click on an imported plugin
    2. Click on Debug As -> Debug Configurations
    3. Create a new Eclipse Application
    4. Click on Debug

* **[Important]** For macOS 
Go to **Run -> Run configuration -> Select eclipse run configuration -> Select Arguments tab** and add **-nosplash** as an argument

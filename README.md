# Ingress - Red Hat OpenShift <img width="26" src="https://github.com/emeloibmco/Red-Hat-Open-Shift-Ingress/blob/main/Images/logo_oc.png">
<br />

## Índice  📰
1. [Pre-Requisitos](#Pre-Requisitos-pencil)
2. [Acceder al clúster](#Acceder-al-clúster-round_pushpin)
3. [Crear Proyectos](#Crear-proyectos-computer)
    * [Desplegar aplicación listas](#Desplegar-aplicación-listas)
    * [Desplegar aplicación de ejemplo NET](#Desplegar-aplicación-de-ejemplo-NET)
4. [Exponer aplicaciones mediante Ingress](#Exponer-aplicaciones-mediante-Ingress-outbox_tray)
    * [Subdominio proporcionado por IBM](#Subdominio-proporcionado-por-IBM)
    * [Nombre de dominio personalizado](#Nombre-de-dominio-personalizado)
5. [Referencias](#Referencias-mag)
6. [Autores](#Autores-black_nib)
<br />

## Pre-Requisitos :pencil:
* Cuenta en IBM Cloud.
* Clúster OpenShift en VPC.
<br />

## Acceder al clúster :round_pushpin:
Para acceder al clúster de OpenShift, complete los siguientes pasos:
<br />

1. Dentro de su cuenta de *IBM Cloud* acceda al ```IBM Cloud Shell``` dando click en la pestaña <a href="https://cloud.ibm.com/shell"> <img width="25" src="https://github.com/emeloibmco/Red-Hat-Open-Shift-Ingress/blob/main/Images/Cluster/boton_shell.png"></a>, que se ubica en la parte superior derecha del portal. 
<br />

<p align="center"><img src="https://github.com/emeloibmco/Red-Hat-Open-Shift-Ingress/blob/main/Images/Cluster/Shell_IBM.PNG"></p>

<br />

2. Ingrese a la consola web de OpenShift presionando el botón ```OpenShift web console```. 
<br />

<p align="center"><img src="https://github.com/emeloibmco/Red-Hat-Open-Shift-Ingress/blob/main/Images/Cluster/ConsolaOC.PNG"></p>

<br />


3. Posteriormente de click sobre su correo (parte superior derecha) y luego en la opción ```Copy Login Command```. Una vez cargue la nueva ventana, de click en la opción ```Display Token```. Copie el comando que sale en la opción ```Log in with this token``` y colóquelo en el IBM Cloud Shell para iniciar sesión y acceder a su clúster de OpenShift.
<br />

<p align="center"><img src="https://github.com/emeloibmco/Red-Hat-Open-Shift-Ingress/blob/main/Images/Cluster/TokenFinal.gif"></p>

<br />

<p align="center"><img src="https://github.com/emeloibmco/Red-Hat-Open-Shift-Ingress/blob/main/Images/Cluster/TokenAccesoShell.png"></p>

<br />

## Crear Proyectos :computer:

### Desplegar aplicación listas
Debe crear un proyecto en el cúal desplegará la aplicación de la listas. Complete los siguientes pasos:
<br />

1. En la consola de OpenShift cree un nuevo proyecto. Para ello, asegúrese de estar en el rol de ```Developer```, de click en la pestaña ```Project``` y luego ```Create Project```. Allí, asígne un nombre y de click en el botón ```Create```.
<br />

<p align="center"><img src="https://github.com/emeloibmco/Red-Hat-Open-Shift-Ingress/blob/main/Images/Listas/Crear-proyecto-Listas-OC.gif"></p>

<br />

2. Acceda al proyecto creado en IBM Cloud Shell. Para ello utilice el comando:

   ```powershell
   oc project <nombre_proyecto>
   ```

   Ejemplo:

   ```powershell
   oc project angular-web-list
   ```
   <br />

   <p align="center"><img src="https://github.com/emeloibmco/Red-Hat-Open-Shift-Ingress/blob/main/Images/Listas/oc_proyect.png"></p>

   <br />

Luego de tener el proyecto listo, el paso siguiente consiste en desplegar la aplicación <a href="https://github.com/emeloibmco/AngularWebList"> Angular Web List</a> en el clúster de OpenShift. Los pasos que debe realizar son los siguientes:
<br />

1. En el IBM Cloud Shell, clone el repositorio que contiene los archivos de la aplicación. Utilice el comando:
   
   ```powershell
   git clone https://github.com/emeloibmco/AngularWebList
   ```
   <br />

   <p align="center"><img src="https://github.com/emeloibmco/Red-Hat-Open-Shift-Ingress/blob/main/Images/Listas/ClonarRepoListas.png"></p>

   <br />

2. Acceda a la carpeta *AngularWebList* con el comando:
   
   ```powershell
   cd AngularWebList
   ```
   <br />

   <p align="center"><img src="https://github.com/emeloibmco/Red-Hat-Open-Shift-Ingress/blob/main/Images/Listas/cd_carpeta_listas.png"></p>

   <br />

3. Despliegue la aplicación en el clúster con el comando:

   ```powershell
   npx nodeshift --strictSSL=false --dockerImage=nodeshift/ubi8-s2i-web-app --imageTag=10.x --build.env OUTPUT_DIR=dist/angular-web-app --expose
   ```
   <br />
   
   > NOTA: Si tiene alguna inquietud sobre el despliegue de la aplicación puede consultar <a href="https://github.com/emeloibmco/ROKS-Angular-HandsOn-4.4#despliegue-aplicaci%C3%B3n-listas-en-angular-%F0%9F%85%B0%EF%B8%8F"> Despliegue Aplicación Listas en Angular</a>.
   
   <br />

4. Verifique que la aplicación se ha desplegado correctamente dentro del proyecto creado.
   
   <br />

   <p align="center"><img src="https://github.com/emeloibmco/Red-Hat-Open-Shift-Ingress/blob/main/Images/Listas/App_ok.gif"></p>

   <br />
<br />

### Desplegar aplicación de ejemplo NET
<br />

## Exponer aplicaciones mediante Ingress :outbox_tray:

### Subdominio proporcionado por IBM
Para exponer aplicaciones a través del ingress es posible usar el *Ingress subdomain* del clúster OpenShift. Para este caso de ejemplo, se va a exponer la aplicación desplegada *Angular Web List*. Complete los siguientes pasos para exponer su aplicación:
<br />

1. Obtenga el *Ingress subdomain* de su clúster y guárdelo para utilizarlo en las configuraciones posteriores. Utilice el comando:

   ```powershell
   ibmcloud oc cluster get -c <cluster_name_or_ID> | grep 'Ingress Subdomain'
   ```
   
   <p align="center"><img src="https://github.com/emeloibmco/Red-Hat-Open-Shift-Ingress/blob/main/Images/Listas/IngressSubdomain.PNG"></p>

   <br />   
   
2. Clone el presente repositorio, ya que este contiene el archivo .yaml necesario para la implementación del ingress. Coloque el comando:


   ```powershell
   git clone https://github.com/emeloibmco/Red-Hat-Open-Shift-Ingress
   ```
   
   <p align="center"><img src="https://github.com/emeloibmco/Red-Hat-Open-Shift-Ingress/blob/main/Images/Listas/ClonarRepoIngress.PNG"></p>

   <br />   
   
3. Cambie su ubicación a la carpeta que contiene el archivo .yaml del ingress. Para ello coloque:


   ```powershell
   cd Red-Hat-Open-Shift-Ingress
   ```
   
   ```powershell
   cd Files
   ```
   
   <p align="center"><img src="https://github.com/emeloibmco/Red-Hat-Open-Shift-Ingress/blob/main/Images/Listas/cdIngressFiles.PNG"></p>

   <br />   
   
4. Visualice el contenido del archivo .yaml con el comando:

   ```powershell
   cat myingressresource.yaml
   ```
        
   <p align="center"><img src="https://github.com/emeloibmco/Red-Hat-Open-Shift-Ingress/blob/main/Images/Listas/catInicial.PNG"></p>  
   
   <br />
  
5. Edite el archivo .yaml con los datos de su aplicación y clúster. Para ello coloque el comando:

   ```
   nano myingressresource.yaml
   ```
   
   Una vez se encuentre dentro del editor modifique lo siguiente:
      * ```apiVersion```: si su clúster es de versión 4.6 o posterior coloque ```networking.k8s.io/v1```. Si su clúster es de versión 4.5 o menor coloque ```networking.k8s.io/v1beta1```.
      * ```host: <ingress_subdomain>```: en el valor de ```<ingress_subdomain>>``` coloque el *Ingress subdomain* de su clúster, obtenido en el paso 1.
      * ```path: /<app_path>```: reemplace ```<app_path>``` con la ruta en la que escucha su aplicación. Si su aplicación no escucha en una ruta específica, defina la ruta raíz solo con ```/```. 
      * ```name: <service_name>```: reemplce ```<service_name>``` con el nombre del servicio de la aplicación. Por ejemplo: ```name: listas```.
      * ```number: <service_port>```: indique el puerto de escucha del servicio en ```<service_port>```. 
   
   <br />
   
   <p align="center"><img src="https://github.com/emeloibmco/Red-Hat-Open-Shift-Ingress/blob/main/Images/Listas/nanoFinal.PNG"></p>

   <br />    
   
   Presione ```Ctrl s``` para guardar el archivo y luego ```Ctrl x``` para salir.
   
   <br />

6. Visualice nuevamente el archivo con el comando ```cat myingressresource.yaml``` e identifique los cambios realizados en base a su información.
   <br />
   
   <p align="center"><img src="https://github.com/emeloibmco/Red-Hat-Open-Shift-Ingress/blob/main/Images/Listas/catFinal.PNG"></p>

   <br />    
   
7. Cree el recurso ingress en el proyecto donde se encuentra su aplicación. Use el comando:

   ```powershell
   oc apply -f myingressresource.yaml -n <project>
   ```
   
   Ejemplo:
   
   ```powershell
   oc apply -f myingressresource.yaml -n angular-web-list
   ```

   <br />
   
   <p align="center"><img src="https://github.com/emeloibmco/Red-Hat-Open-Shift-Ingress/blob/main/Images/Listas/createIngress.PNG"></p>

   <br />   

8. 

<br />

### Nombre de dominio personalizado
<br />

## Referencias :mag:
<br />

## Autores :black_nib:
Equipo *IBM Cloud Tech Sales Colombia*.

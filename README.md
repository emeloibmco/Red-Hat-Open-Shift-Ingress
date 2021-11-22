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
* Tener una cuenta en <a href="https://cloud.ibm.com/"> IBM Cloud</a> <img width="25" src="https://github.com/emeloibmco/IBM-Cloud-Kubernetes-Angular-Web-List/blob/main/Images/ibm-cloud-logo.png">.
* Tener un clúster OpenShift en VPC.
* Contar con una VPC.
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


3. Cuando ya se encuentre en la consola web de OpenShift, de click sobre su correo (parte superior derecha) y luego en la opción ```Copy Login Command```. Una vez cargue la nueva ventana, de click en la opción ```Display Token```. Copie el comando que sale en la opción ```Log in with this token``` y colóquelo en el IBM Cloud Shell para iniciar sesión y acceder a su clúster de OpenShift.
<br />

<p align="center"><img src="https://github.com/emeloibmco/Red-Hat-Open-Shift-Ingress/blob/main/Images/Cluster/TokenFinal.gif"></p>

<br />

<p align="center"><img src="https://github.com/emeloibmco/Red-Hat-Open-Shift-Ingress/blob/main/Images/Cluster/TokenAccesoShell.png"></p>

<br />

## Crear Proyectos :computer:

### Desplegar aplicación listas
Debe crear un proyecto en el cúal desplegará la aplicación de la listas. Complete los siguientes pasos:
<br />

1. En la consola de OpenShift cree un nuevo proyecto. Para ello, asegúrese de estar en el rol de ```Developer```, de click en la pestaña ```Project``` y luego ```Create Project```. Allí asígne un nombre y de click en el botón ```Create```.
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
Para desplegar una aplicación de ejemplo .NET 5.0 realice lo siguiente:
<br />

1. En la consola web de OpenShift, despliegue la pestaña ```Project``` y de click en la opción ```Create Project```.
<br />

2. Asigne un nombre para el proyecto y luego de click en la pestaña ```Create```.
<br />

3. Seleccione la pestaña ```+ Add``` y allí de click en la opción ```Samples```.
<br />

4. De click en la opción de ejemplos ```.NET```. Asígne un nombre y para finalizar presione el botón ```Create```.
<br />

5. Espere unos minutos mientras se completa el despliegue de la aplicación. Luego de click en ```Open URL``` y visualice la aplicación de ejemplo funcionando.

   <br />
   
   <p align="center"><img src="https://github.com/emeloibmco/Red-Hat-Open-Shift-Ingress/blob/main/Images/NetApp/AppNETSample.gif"></p>

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
   
2. Clone el presente repositorio ya que este contiene el archivo .yaml necesario para la implementación del ingress. Coloque el comando:


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
      * ```host: <ingress_subdomain>```: en el valor de ```<ingress_subdomain>``` coloque el *Ingress subdomain* de su clúster, obtenido en el paso 1.
      * ```path: /<app_path>```: reemplace ```<app_path>``` con la ruta en la que escucha su aplicación. Si su aplicación no escucha en una ruta específica, defina la ruta raíz solo con ```/```. 
      * ```name: <service_name>```: reemplace ```<service_name>``` con el nombre del servicio de la aplicación. Por ejemplo: ```name: listas```.
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


8. Para probar el funcionamiento de la aplicación a través del ingress, en la consola web de OpenShift cambie al rol de ```Administrator```. Luego de click en la sección ```Networking``` ➡ ```Ingresses``` y observe que aparezca el ingress creado. Luego, de click en la pestaña ```Routes``` y allí identifique 2 rutas para la aplicación:

   * La ruta obtenida en el despliegue de la aplicación.
   * La ruta generada con el ingress (observe que la URL es el mismo Ingress Sundomain del clúster).

   Para continuar, de click sobre ambas rutas. Como resultado debe obtener la aplicación funcionando con las 2 URL.

   <br />
   
   <p align="center"><img src="https://github.com/emeloibmco/Red-Hat-Open-Shift-Ingress/blob/main/Images/Listas/IngressListas.gif"></p>

   <br />  

<br />


### Nombre de dominio personalizado
Para exponer aplicaciones a través del ingress es posible personalizar un nombre de dominio y usarlo junto con el *Ingress subdomain* del clúster OpenShift. Para este caso, es necesario hacer uso de un servicio DNS para registrar el nombre de dominio. Para este ejercicio se utilizará la aplicación de ejemplo .NET.
<br />

### Crear Servicio DNS
Para crear un servicio DNS realice lo siguiente:
<br />

1. Acceda al catálogo en el portal de IBM Cloud y allí coloque DNS para encontrar el servicio.
<br />

2. Seleccione el servicio ```DNS Services```. Posteriormente complete los campos solicitados de la siguiente manera:

   * Seleccione el plan de precios ```Standard DNS```.
   * Asígne un nombre exclusivo para el servicio.
   * Seleccione el grupo de recursos (coloque el mismo grupo de recursos correspondiente al clúster).
   
   Para finalizar acepte haber leído los acuerdos de licencia y de click en el botón ```Create```.
   
   <br />

   <p align="center"><img src="https://github.com/emeloibmco/Red-Hat-Open-Shift-Ingress/blob/main/Images/NetApp/ServicioDNS.gif"></p>

   <br />

### Registrar nombre de dominio
Luego de desplegar el servicio DNS, debe registrar un nombre de dominio personalizado para exponer la aplicación a través del ingress. Para ello, realice lo siguiente:
<br />

1. En la pestaña ```DNS Zones``` de click en el botón ```Create Zone```. Asigne un dominio en el campo ```Name``` (por ejemplo: ```dns-ibmcloud-net.com```) y para finalizar de click en el botón ```Create zone```.
<br />

2. Seleccione la Zona DNS creada.
<br />

3. En un principio, el estado de la Zona DNS debe ser ```pending```. Para actualizarlo, de click la pestaña ```Permitted Networks``` y allí presione el botón ```Add network```. Luego, seleccione la región y VPC en donde se encuentra su clúster y de click en ```Add network```. Después de agregar la VPC el estado de la Zona DNS deberá cambiar a ```Active```.
<br />

4. De click en la pestaña ```DNS records``` y presione el botón ```Add record```. Luego, complete los campos solicitados de la siguiente maneras:

   * ```Type```: CNAME.
   * ```TTL```: 15 min.
   * ```Name```: www.
   * ```Type```: Asígne un nombre canónico, por ejemplo: ```dns-ibmcloud-net.com```.
<br />

5. Para finalizar, de click en el botón ```Save record```.
   
<br />

<p align="center"><img src="https://github.com/emeloibmco/Red-Hat-Open-Shift-Ingress/blob/main/Images/NetApp/CrearDNS.gif"></p>

<br />

### Exponer aplicación a través del Ingress
Complete los siguientes pasos para exponer la aplicación .NET a través de ingress con un nombre de dominio personalizadp:
<br />

1. En la misma ventana de IBM Cloud Shell, seleccione el proyecto .NET desplegado. Para ello utilice el comando:

   ```powershell
   oc project <nombre_proyecto>
   ```
   
   Ejemplo:
   
   ```powershell
   oc project net-app-test
   ```
   
   <br />
   
2. Teniendo en cuenta que previamente clon+o el repositorio que contiene el archivo ```myingressresource.yaml```, asegúrese de estar en la ubicación de la carpeta que lo contiene (```Red-Hat-Open-Shift-Ingress/Files```) y edite el archivo con los nuevos datos de la aplicación. Utilice el comando:

   ```powershel
   nano myingressresource.yaml
   ```
   <br />
   
   Luego, edite los campos de la siguiente manera:
   
   * ```apiVersion```: si su clúster es de versión 4.6 o posterior coloque ```networking.k8s.io/v1```. Si su clúster es de versión 4.5 o menor coloque ```networking.k8s.io/v1beta1```.
   * ```host: <ingress_subdomain>```: en el valor de ```<ingress_subdomain>``` coloque: ```<dns_personalizado>.<ingress_subdomain>```. Donde ```<dns_personalizado>``` corresponde al nombre de dominio generado en el servicio DNS y el ```<ingress_subdomain>``` corresponde al valor del *Ingress Subdomain* del clúster.
   * ```path: /<app_path>```: reemplace ```<app_path>``` con la ruta en la que escucha su aplicación. Si su aplicación no escucha en una ruta específica, defina la ruta raíz solo con ```/```. 
   * ```name: <service_name>```: reemplace ```<service_name>``` con el nombre del servicio de la aplicación. Por ejemplo: ```name: net-sample-app```.
   * ```number: <service_port>```: indique el puerto de escucha del servicio en ```<service_port>```. 
   
   <br />
   
   <p align="center"><img src="https://github.com/emeloibmco/Red-Hat-Open-Shift-Ingress/blob/main/Images/NetApp/nano.PNG"></p>

   <br />    
   
   Presione ```Ctrl s``` para guardar el archivo y luego ```Ctrl x``` para salir.
   
   <br />

6. Visualice el archivo con el comando ```cat myingressresource.yaml``` e identifique los cambios realizados en base a su información.
   <br />
   
   <p align="center"><img src="https://github.com/emeloibmco/Red-Hat-Open-Shift-Ingress/blob/main/Images/NetApp/cat.PNG"></p>

   <br />    
   
7. Cree el recurso ingress en el proyecto donde se encuentra su aplicación. Use el comando:

   ```powershell
   oc apply -f myingressresource.yaml -n <project>
   ```
   
   Ejemplo:
   
   ```powershell
   oc apply -f myingressresource.yaml -n net-app-test
   ```

   <br />
   
   <p align="center"><img src="https://github.com/emeloibmco/Red-Hat-Open-Shift-Ingress/blob/main/Images/NetApp/oc_apply.PNG"></p>

   <br />   


8. Para probar el funcionamiento de la aplicación a través del ingress, en la consola web de OpenShift cambie al rol de ```Administrator```. Luego de click en la sección ```Networking``` ➡ ```Ingresses``` y observe que aparezca el ingress creado. Luego, de click en la pestaña ```Routes``` y allí identifique 2 rutas para la aplicación:

   * La ruta obtenida en el despliegue de la aplicación.
   * La ruta generada con el ingress (observe que la URL se compone del nombre de dominio personalizado, el cual contiene el DNS registrado junto con el Ingress Sundomain del clúster).

   Para continuar, de click sobre ambas rutas. Como resultado debe obtener la aplicación funcionando con las 2 URL.

   <br />
   
   <p align="center"><img src="https://github.com/emeloibmco/Red-Hat-Open-Shift-Ingress/blob/main/Images/NetApp/IngressNet.gif"></p>

   <br />  

<br />



## Referencias :mag:
* <a href="https://cloud.ibm.com/docs/openshift?topic=openshift-ingress-qs-roks4">Quick start for Ingress</a>.
<br />

## Autores :black_nib:
Equipo *IBM Cloud Tech Sales Colombia*.

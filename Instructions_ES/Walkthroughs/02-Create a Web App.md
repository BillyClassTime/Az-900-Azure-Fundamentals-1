---
wts:
    title: '02 - Crear una aplicación web (10 minutos)'
    module: 'Módulo 02: Servicios principales de Azure (Cargas de trabajo)'
---
# 02 - Crear una aplic. web

En este tutorial, crearemos una nueva aplic. web que ejecute un contenedor Docker. El contenedor muestra un mensaje de bienvenida. 

# Tarea 1: Crear una aplicación web (10 minutos)

Azure App Service es en realidad una colección de cuatro servicios, los cuales están diseñados para hospedar y ejecutar aplicaciones web. Los cuatro servicios (Web Apps, Mobile Apps, API Apps y Logic Apps) se ven diferentes, pero, al final, todos funcionan de manera muy similar. De los cuatro servicios, las Web Apps son las que se usan con mayor frecuencia y es el servicio que utilizaremos en este laboratorio.

En esta tarea, creará una aplicación web de Azure App Service. 

1. Inicie sesión en [Azure Portal](http://portal.azure.com/). 

2. Desde la hoja **Todos los servicios**, busque y seleccione **App Services** y haga clic en **+ Agregar**.

3. En la pestaña **Datos básicos** de la hoja **Aplicación web**, especifique la siguiente configuración (reemplace **xxxx** en el nombre de la aplicación web con letras y dígitos para que el nombre sea único a nivel mundial). Deje los valores predeterminados para todo lo demás, incluido el plan de App Service. 

    | Configuración | Valor |
    | -- | -- |
    | Suscripción | **Elija su suscripción** |
    | Grupo de recursos | **myRGWebApp1** (crear nuevo) |
    | Nombre | **myDockerWebAppxxxx** |
    | Publicar | **Contenedor de Docker** |
    | Sistema operativo | **Linux** |
    | Región | **Este de EE. UU.** (ignore cualquier advertencia de disponibilidad del plan de servicio) |
    | | |	
    
    **Nota** - : Recuerde cambiar **xxxx** de modo que sea un **nombre** único

4. Haga clic en **Siguiente > Docker** y configure la información del contenedor. El comando de inicio es opcional y no es necesario en este ejercicio. 

    **Nota:** Este es el mismo contenedor que se utilizó en el tutorial de Container Instances para mostrar un mensaje de Hola mundo. 

    | Configuración | Valor |
    | -- | -- |
    | Opciones | **Contenedor individual** |
    | Origen de imagen | **Docker Hub** |
    | Tipo de acceso | **Pública** |
    | Imagen y etiqueta | **microsoft/aci-helloworld** |
    | | |	


5. Haga clic en **Revisar y crear**, y luego haga clic en **Crear**. 

# Tarea 2: Probar la aplicación web

En esta tarea probaremos la aplicación web.

1. Espere a que se implemente la aplicación web.

2. Desde **Notificaciones**, haga clic en **Ir al recurso**. 

3. En la hoja **Información general**, ubique la entrada **URL**. 

    ![Captura de pantalla de la hoja de propiedades de la aplicación web. La URL está resaltada.](../images/0801.png)

4. Haga clic en la **URL** para abrir la nueva pestaña del explorador y mostrar la página Le damos la bienvenida a Azure Container Instances.

    ![Captura de pantalla de la página Le damos la bienvenida a Azure Container Instance.](../images/0802.png)

5. Vuelva a la hoja de **Información general** de su aplicación web y tenga en cuenta que incluye varios gráficos. Si repite el paso 4 varias veces, debería poder ver la telemetría correspondiente en los gráficos. Esto incluye el número de solicitudes y el tiempo de respuesta promedio. 

**Nota**: Para evitar costes adicionales, puede quitar este grupo de recursos. Busque grupos de recursos, haga clic en su grupo de recursos y, a continuación, haga clic en **Eliminar grupo de recursos**. Compruebe el nombre del grupo de recursos y luego haga clic en **Eliminar**. Supervise las **Notificaciones** para ver cómo se realiza la eliminación.


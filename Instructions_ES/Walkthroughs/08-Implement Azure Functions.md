---
wts:
    title: '08 - Implementar Azure Functions (5 minutos)'
    module: 'Módulo 03: Describir las soluciones principales y las herramientas de administración'
---
# 08 - Implementar Azure Functions

En este tutorial, crearemos una aplicación de funciones para mostrar un mensaje de saludo cuando haya una solicitud HTTP. 

# Tarea 1: Crear una aplicación Functions (5 minutos)

En esta tarea, crearemos un aplicación de funciones.

1. Inicie sesión en [Azure Portal](https://portal.azure.com).

1. En el cuadro de texto **Buscar recursos, servicios y documentos**, en la parte superior del portal, busque y seleccione **Aplicación de funciones** y luego, desde la hoja **Aplicación de funciones**, haga clic en **Agregar**.

1. En la pestaña **Básico** de la hoja **Aplicación de funciones**, especifique la siguiente configuración (reemplace **xxxx** en el nombre de la función por letras y dígitos, de modo que el nombre sea globalmente único, y deje todas las demás configuraciones con sus valores predeterminados): 

    | Configuración | Valor |
    | -- | --|
    | Suscripción | el nombre de su suscripción de Azure |
    | Grupo de recursos | el nombre de un nuevo grupo de recursos **myRGFunction** |
    | Nombre de la aplicación de funciones | **función-xxxx** |
    | Publicar | **Código** |
    | Pila de tiempo de ejecución | **NET Core** |
    | Versión | **3.1** |
    | Región | **Este de EE. UU.** |
    | | |

    **Nota** - Recuerde cambiar **xxxx** de modo que sea un **nombre de aplicación de Functions** único

1. Haga clic en **Revisar y crear** y, después de una correcta validación, haga clic en **Crear** para empezar a aprovisionar e implementar su nueva aplicación de funciones de Azure.

1. Espere la notificación de que el recurso ha sido creado.

1. Vuelva a la hoja de **Aplicación de funciones**, haga clic en **Actualizar** y compruebe que la aplicación de función recién creada tenga el estado **Ejecutando**. 

    ![Captura de pantalla de la página Aplicación de funciones con la nueva aplicación de funciones.](../images/0701.png)

# Tarea 2: Crear una función activada por HTTP y probar

En esta tarea, usaremos la función API de Webhook para mostrar un mensaje cuando haya una solicitud HTTP. 

1. Sobre la hoja **Aplicación de funciones**, haga clic en la aplicación de funciones recién creada. 

1. En la hoja de la aplicación de funciones, en la sección **Funciones**, haga clic en **Funciones** y luego en **+ Agregar**.

    ![Captura de pantalla del paso elegir un entorno de desarrollo en Azure Function para el panel de inicio dot net dentro de Azure Portal. Se resaltan los elementos de visualización para crear una nueva función en el portal. Los elementos resaltados son expandir la aplicación de funciones, agregar nuevas funciones, en el portal y el botón continuar.](../images/0702.png)

1. En la pestaña **Plantillas** de la hoja **Nueva función**, haga clic en **Desencadenador HTTP**. 

    ![Captura de pantalla del paso Crear una función en Azure Functions para el panel de inicio dot net dentro de Azure Portal. La tarjeta de desencadenador HTTP se resalta para ilustrar los elementos de visualización utilizados para agregar un nuevo webhook a una función de Azure.](../images/0702a.png)

1. En la pestaña **Detalles** de la hoja **Nueva función**, acepte el nombre predeterminado **Nueva función** y el **Nivel de autorización** y luego haga clic en **Crear función**. 

    ![Captura de pantalla del paso Crear una función en Azure Functions para el panel de inicio dot net dentro de Azure Portal. El botón webhook + API y el botón Crear se resaltan para ilustrar los elementos de visualización que se usan para agregar un nuevo webhook a una función de Azure.](../images/0703.png)

1. En la hoja **HttpTrigger1**, en la sección **Desarrollador**, haga clic en **Código + Prueba**. 

1. En la hoja **HttpTrigger1 \|** En la hoja **Código + prueba**, revise el código generado automáticamente y tenga en cuenta que el código está diseñado para ejecutar una solicitud HTTP y registrar información. Además, observe que la función devuelve un mensaje de saludo con un nombre. 

    ![Captura de pantalla del código de función. El mensaje de saludo está resaltado.](../images/0704.png)

1. Haga clic en **Obtener URL de función** desde la sección superior del editor de funciones. 

1. Asegúrese de que el valor en la lista desplegable **Clave** se establece en **predeterminado** y haga clic en **Copiar** para copiar la función URL. 

    ![Captura de pantalla del panel URL de obtención de funciones dentro del editor de funciones en Azure Portal. Los elementos de visualización obtienen el botón URL de la función, establecen el menú desplegable de teclas y el botón Copiar URL se resaltan para indicar cómo obtener y copiar la URL de la función desde el editor de funciones.](../images/0705.png)

1. Abra una nueva pestaña del explorador y pegue la URL de la función copiada en la barra de direcciones del explorador web. Cuando se solicite la página, la función se ejecutará. Observe el mensaje devuelto que indica que la función requiere un nombre en el cuerpo de la solicitud.

    ![Captura de pantalla del mensaje para proporcionar un nombre.](../images/0706.png)

1. Agregue **&name=*yourname*** al final de la URL.

    **Nota**: Reemplace ***yourname*** con su nombre. Por ejemplo, si su nombre es Cindy, la URL final se parecerá a la siguiente `https://azfuncxxx.azurewebsites.net/api/HttpTrigger1?code=X9xx9999xXXXXX9x9xxxXX==&name=cindy`

    ![Captura de pantalla de una URL de función resaltada y un nombre de usuario de ejemplo adjunto en la barra de direcciones de un explorador web. El mensaje de saludo y el nombre de usuario también se resaltan para ilustrar el resultado de la función en la ventana principal del explorador.](../images/0707.png)

1. Cuando se ejecuta su función, se rastrea cada invocación. Para ver el seguimiento en Azure Portal, vuelva a **HttpTrigger1 \|** Hoja **Código + Prueba** y haga clic en **Supervisar**.

    ![Captura de pantalla de un registro de información de seguimiento resultante de ejecutar la función dentro del editor de funciones en Azure Portal.](../images/0709.png) 

¡Enhorabuena! Ha creado una aplicación de funciones para mostrar un mensaje de saludo cuando hay una solicitud HTTP. 

**Nota**: Para evitar costes adicionales, puede quitar este grupo de recursos. Busque grupos de recursos, haga clic en su grupo de recursos y, a continuación, haga clic en **Eliminar grupo de recursos**. Compruebe el nombre del grupo de recursos y luego haga clic en **Eliminar**. Supervise las **Notificaciones** para ver cómo se realiza la eliminación.

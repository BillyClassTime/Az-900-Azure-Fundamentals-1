---
wts:
    title: '07 - Implementar un Azure IoT Hub (10 minutos)'
    module: 'Módulo 03: Describir las soluciones principales y las herramientas de administración'
---
# 07 - Implementar un Azure IoT Hub

En este tutorial, configuraremos un nuevo Azure IoT Hub en Azure Portal, y luego autenticaremos una conexión a un dispositivo IoT usando el simulador de dispositivo Raspberry Pi en línea. Los datos y los mensajes del sensor se pasan del simulador de Raspberry Pi a su Azure IoT Hub, y puede ver las métricas para la actividad de mensajería en Azure Portal.

# Tarea 1: Crear un centro de IoT (10 minutos)

En esta tarea, crearemos un centro de IoT. 

1. Inicie sesión en [Azure Portal](https://portal.azure.com).

2. Desde la hoja **Todos los servicios**, busque y seleccione **Centro de IoT** y luego haga clic en **+ Agregar**.

3. En la pestaña **Datos básicos** de la hoja **centro de IoT**, complete los campos con los siguientes detalles (reemplace **xxxx** en el nombre de la cuenta de almacenamiento con letras y dígitos de modo que el nombre sea globalmente único):

    | Configuración | Valor |
    |--|--|
    | Suscripción | **Elija su suscripción** |
    | Grupo de recursos |  **myRGIoT** (crear nuevo)|
    | Región | **Este de EE. UU.** |
    | Nombre del centro de IoT | **my-hub-groupxxxx** |
    | | |

    **Nota** - Recuerde cambiar **xxxx** de modo que sea un **nombre de centro de IoT** único

4. Vaya a la pestaña **Administración**, use la lista desplegable para configurar **Precios y nivel de escala** en **S1:**

5. Haga clic en el botón **Revisar y crear**.

6. Haga clic en el botón **Crear** para comenzar a crear su nueva instancia de Azure IoT Hub.

7. Espere hasta que se implemente la instancia de Azure IoT Hub. 

# Tarea 2: Agregar un dispositivo de IoT

En esta tarea, agregaremos un dispositivo IoT al centro de IoT. 

1. Cuando la implementación se haya completado, haga clic en **Ir al recurso** desde la hoja de implementación. Si no, desde la hoja **Todos los servicios**, busque y seleccione **Centro de IoT** y ubique su nueva instancia de centro de IoT.

	![Captura de pantalla de la implementación en curso y notificaciones de implementación exitosa en Azure Portal.](../images/0601.png)

2. Para agregar un nuevo dispositivo IoT, desplácese hacia abajo hasta la sección **Exploradores** y haga clic en **Dispositivos IoT**. Luego, haga clic en **+ Nuevo**.

	![Captura de pantalla del panel de dispositivos IoT, resaltado dentro de la hoja de navegación del centro IoT, en Azure Portal. El botón Nuevo se resalta para ilustrar cómo agregar una nueva identidad del dispositivo IoT al centro de IoT.](../images/0602.png)

3. Proporcione un nombre para su nuevo dispositivo IoT, **myRaspberryPi**, y haga clic en el botón **Guardar**. Esto creará una nueva identidad del dispositivo IoT en su Azure IoT Hub.

4. Si no ve su nuevo dispositivo, **actualice** la página de dispositivos IoT. 

5. Seleccione **myRaspberryPi** y copie el valor **Cadena de conexión primaria**. Utilizará esta clave en la siguiente tarea para autenticar una conexión al simulador de Raspberry Pi.

	![Captura de pantalla de la página Cadena de conexión primaria con el icono de copia resaltado.](../images/0603.png)

# Tarea 3: Probar el dispositivo con el simulador de Raspberry Pi

En esta tarea probaremos nuestro dispositivo usando el simulador de Raspberry Pi. 

1. Abra una nueva pestaña en el explorador web y navegue hasta el [simulador en línea de Raspberry Pi](https://azure-samples.github.io/raspberry-pi-web-simulator/#Getstarted). 

2. Lea sobre el simulador de Raspberry Pi. Si hay una ventana emergente de información general, seleccione "**X**" para cerrar la ventana.

3. En el área de código, al lado derecho, ubique la línea con 'const connectionString ='. Reemplácelo con la cadena de conexión que copió de Azure Portal. Tenga en cuenta que la cadena de conexión incluye las entradas DeviceId (**myRaspberryPi**) y SharedAccessKey.

	![Captura de pantalla del área de codificación dentro del simulador de Raspberry Pi.](../images/0604.png)

4. Haga clic en **Ejecutar** (debajo del área de código) para ejecutar la aplicación. La salida de la consola debe mostrar los datos y mensajes del sensor que se envían desde el simulador de Raspberry Pi a su Azure IoT Hub. Los datos y mensajes se envían cada vez que parpadea el LED del simulador Raspberry Pi. 

	![Captura de pantalla de la consola del simulador Raspberry Pi.  La salida de la consola muestra los datos y mensajes del sensor enviados desde el simulador de Raspberry Pi a Azure IoT Hub.](../images/0605.png)

5. Haga clic en **Detener** para dejar de enviar datos.

6. Regrese al Azure Portal y a su centro de IoT.

7. Cambie la hoja de **Información general** del centro de IoT y desplácese hacia abajo hasta la información de **Utilización del centro de IoT**.

	![Captura de pantalla de las métricas dentro del área de utilización del centro de IoT de Azure Portal.](../images/0606.png)


¡Enhorabuena! Ha configurado Azure IoT Hub para recopilar datos del sensor de un dispositivo IoT.

**Nota**: Para evitar costes adicionales, puede quitar este grupo de recursos. Busque grupos de recursos, haga clic en su grupo de recursos y, a continuación, haga clic en **Eliminar grupo de recursos**. Compruebe el nombre del grupo de recursos y luego haga clic en **Eliminar**. Supervise las **Notificaciones** para ver cómo se realiza la eliminación.

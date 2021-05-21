---
wts:
    title: '01 - Crear una máquina virtual en el portal (10 minutos)'
    module: 'Módulo 2: Servicios principales de Azure (Cargas de trabajo)'
---
# 01 - Crear una máquina virtual en el portal

En este tutorial crearemos una máquina virtual en Azure Portal, nos conectaremos a dicha máquina virtual, instalaremos la función del servidor web y la probaremos. 

**Nota**: Tómese el tiempo durante este tutorial para hacer clic y leer los iconos informativos. 

# Tarea 1: Crear una máquina virtual (10 minutos)

En esta tarea, crearemos una máquina virtual Windows Server 2019 Datacenter - Gen1. 

1. Inicie sesión en [Azure Portal (https://portal.azure.com)](https://portal.azure.com?azure-portal=true).

2. Desde la hoja **Todos los servicios**, busque y seleccione **Máquinas virtuales** y luego haga clic en **+ Agregar** y seleccione **+ Maquinas virtuales**.

3. En la pestaña **Datos básicos**, complete la siguiente información (deje los valores predeterminados para todo lo demás):

    | Configuración | Valores |
    |  -- | -- |
    | Suscripción | **Elija su suscripción**|
    | Grupo de recursos | **myRGVM** (crear nueva) |
    | Nombre de la máquina virtual | **myVm** |
    | Ubicación | **Este de EE. UU.**|
    | Imagen | **Windows Server 2019 Datacenter - Gen 1**|
    | Tamaño | Estándar D2s, v3|
    | Nombre de usuario de la cuenta de administrador | **azureuser** |
    | Contraseña de cuenta de administrador | **Pa$$w0rd1234**|
    | Reglas del puerto de entrada: Permitir puertos seleccionados | **RDP (3389)** y **HTTP (80)**|
    | | |

4. Cambie a la pestaña Redes y busque **Seleccionar puertos de entrada:**

    | Configuración | Valores |
    | -- | -- |
    | Seleccionar puertos de entrada | **HTTP (80), RDP (3389)**|
    | | |

    **Nota** - Compruebe que tanto el puerto 80 como el puerto 3389 están seleccionados

5. Vaya a la pestaña Administración y, en la sección **Supervisión**, seleccione la siguiente configuración:

    | Configuración | Valores |
    | -- | -- |
    | Diagnóstico de arranque | **Deshabilitar**|
    | | |

6. Deje los valores predeterminados restantes y luego haga clic en el botón **Revisar y crear**, en la parte inferior de la página.

7. Una vez que se supere la validación, haga clic en el botón **Crear**. La implementación de la máquina virtual puede demorar entre cinco y siete minutos.

8. Recibirá actualizaciones en la página de implementación y a través del área **Notificaciones** (el icono de la campana en el menú superior).

* **Compruebe que los puertos 80 y 3389 están abiertos**

# Tarea 2: Conectarse a la máquina virtual

En esta tarea nos conectaremos a nuestra nueva máquina virtual usando el RDP. 

1. Busque **myVM** y seleccione su nueva máquina virtual.

    **Nota**: También puede usar el vínculo **Ir al recurso** en la página de implementación o el vínculo para acceder al recurso en el área de **Notificaciones**.

2. En la hoja de **Información general** de la máquina virtual, haga clic en el botón **Conectar** y seleccione **RDP**.

    ![Captura de pantalla de las propiedades de la máquina virtual con el botón Conectar resaltado.](../images/0101.png)

    **Nota**: Las siguientes instrucciones le indican cómo conectarse a su VM desde un equipo con Windows. En un equipo Mac, necesita un cliente RDP, como este cliente de escritorio remoto de Mac App Store, y en un equipo Linux, puede usar un cliente RDP de código abierto.

2. En la página **Conectarse a la máquina virtual**, mantenga las opciones predeterminadas para conectarse con la dirección IP pública a través del puerto 3389 y haga clic en **Descargar archivo RDP**.

3. **Abra** el archivo RDP descargado y haga clic en **Conectar** cuando se le solicite. 

    ![Captura de pantalla de las propiedades de la máquina virtual con el botón Conectar resaltado. ](../images/0102.png)

4. En la ventana **Seguridad de Windows**, seleccione **Más opciones** y luego **Usar una cuenta diferente**. Proporcione el nombre de usuario (.\azureuser) y la contraseña (Pa$$w0rd1234). Haga clic en **Aceptar** para conectarse.

    ![Captura de pantalla del cuadro de diálogo de seguridad de Windows con la opción Usar una cuenta diferente seleccionada, y el nombre de usuario Azure y una contraseña ingresados.](../images/0103.png)

5. Es posible que reciba una advertencia de certificado durante el proceso de inicio de sesión. Haga clic en **Sí** o cree la conexión y conéctese a su VM implementada. Debería conectarse correctamente.

    ![Captura de pantalla del cuadro de diálogo de advertencia de certificado que informa al usuario de un certificado no confiable, con el botón Sí resaltado. ](../images/0104.png)

¡Enhorabuena! Ha implementado una máquina virtual de Windows Server en Azure y se ha conectado a ella

# Tarea 3: Instalar la función del servidor web y probarla

En esta tarea, instale el rol Servidor web en el servidor y asegúrese de que se pueda mostrar la página principal predeterminada de IIS.

1. Abra un símbolo del sistema de PowerShell en la máquina virtual. Para ello, haga clic en el botón **Inicio**, escriba **PowerShell**, haga clic con el botón derecho en **Windows PowerShell** y seleccione **Ejecutar como administrador** en el menú contextual.

    ![Captura de pantalla del escritorio de la máquina virtual con el botón de inicio presionado y PowerShell seleccionado, con la opción Ejecutar como administrador resaltada.](../images/0105.png)

2. Instale la característica **Servidor web** en la máquina virtual al ejecutar el siguiente comando en el símbolo del sistema de PowerShell. Puede copiar y pegar este comando.

    ```PowerShell
    Install-WindowsFeature -name Web-Server -IncludeManagementTools
    ```
  
3. Cuando complete este paso, aparecerá un aviso que indicará **Correcto** con un valor **Verdadero**. No es necesario que reinicie la máquina virtual para completar la instalación. Cierre la conexión RDP a la VM.

    ![Captura de pantalla del símbolo del sistema de Windows PowerShell con el comando Install-WindowsFeature -name Web-Server -IncludeManagementTools completado correctamente y la salida que indica que fue exitoso.](../images/0106.png)

4. De vuelta en el portal, navegue hasta la hoja **Información general** de myVM y use el botón **Clic para copiar al Portapapeles** para copiar la dirección IP pública de myVM. Abra una nueva pestaña del explorador, pegue la dirección IP pública en el cuadro de texto de URL y presione la tecla **Entrar** para acceder a ella.

    ![Captura de pantalla del panel de propiedades de la máquina virtual de Azure Portal con la dirección IP copiada.](../images/0107.png)

5. Se abrirá la página principal predeterminada del servidor web IIS.

    ![Captura de pantalla de la página principal predeterminada del servidor web IIS a la que se accede a través de la dirección IP pública en un explorador web.](../images/0108.png)

¡Enhorabuena! Creó un servidor web al que se puede acceder a través de su dirección IP pública. Si tuviera una aplicación web para hospedar, podría implementar archivos de aplicación en la máquina virtual y hospedarlos para acceso público en la máquina virtual implementada.


**Nota**: Para evitar costes adicionales, puede quitar este grupo de recursos. Busque grupos de recursos, haga clic en su grupo de recursos y, a continuación, haga clic en **Eliminar grupo de recursos**. Compruebe el nombre del grupo de recursos y luego haga clic en **Eliminar**. Supervise las **Notificaciones** para comprobar que la eliminación se haya completado correctamente. 

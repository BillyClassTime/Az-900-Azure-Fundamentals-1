---
wts:
    title: '13 - Tráfico de red segura (10 min)'
    module: 'Módulo 04: Descripción de las características de seguridad general y de seguridad de red'
---
# 13 - Tráfico de red segura

En este tutorial, configuraremos un grupo de seguridad de red.

# Tarea 1: Crear una máquina virtual (10 min)

En esta tarea, crearemos una máquina virtual de Windows Server 2019 Datacenter. 

1. Inicie sesión en [Azure Portal](https://portal.azure.com).

2. Desde la hoja **Todos los servicios**, busque y seleccione **Máquinas virtuales** y luego haga clic en **+ Agregar**.

3. En la pestaña **Datos básicos**, complete la siguiente información (deje los valores predeterminados para todo lo demás):

    | Configuración | Valores |
    |  -- | -- |
    | Suscripción | **Elija su suscripción**|
    | Grupo de recursos | **myRGSecure** (crear nuevo) |
    | Nombre de la máquina virtual | **SimpleWinVM** |
    | Ubicación | **Este de EE. UU.**|
    | Imagen | **Windows Server 2019 Datacenter**|
    | Tamaño | **Estándar D2s v3**|
    | Nombre de usuario de la cuenta de administrador | **azureuser** |
    | Contraseña de cuenta de administrador | **Pa$$w0rd1234**|
    | Reglas de puerto de entrada | **Ninguna**|
    | | |

4. Cambie a la pestaña **Redes** y configure la siguiente configuración:

    | Configuración | Valores |
    | -- | -- |
    | Grupo de seguridad de red NIC | **Ninguna**|
    | | |

5. Vaya a la pestaña **Administración** y, en la sección **Supervisión**, seleccione la siguiente configuración:

    | Configuración | Valores |
    | -- | -- |
    | Diagnóstico de arranque | **Deshabilitar**|
    | | |

6. Deje los valores predeterminados restantes y luego haga clic en el botón **Revisar y crear**, en la parte inferior de la página.

7. Una vez que se supere la validación, haga clic en el botón **Crear**. La implementación de la máquina virtual puede tardar unos cinco minutos.

8. Supervisar la implementación. La creación del grupo de recursos y la máquina virtual puede tomar varios minutos. 

9. Desde la hoja de implementación o desde el área Notificación, haga clic en **Ir al recurso**. 

10. Sobre la hoja de la máquina virtual **SimpleWinVM**, haga clic en **Redes**, revise la pestaña de **Reglas de puerto de entrada** y tenga en cuenta que no hay un grupo de seguridad de red asociado con la interfaz de red de la máquina virtual o la subred a la que está conectada la interfaz de red.

    **Nota**: Identifique el nombre de la interfaz de red. Lo necesitará en la próxima tarea.

# Tarea 2: Crear un grupo de seguridad de red

En esta tarea, crearemos un grupo de seguridad de red y lo asociaremos con la interfaz de red.

1. Desde la hoja **Todos los servicios**, busque y seleccione **Grupos de seguridad de red** y luego haga clic en **+ Agregar**

2. Sobre la pestaña **Datos básicos** de la hoja **Crear grupo de seguridad de red**, especifique la siguiente configuración.

    | Configuración | Valor |
    | -- | -- |
    | Suscripción | **Elija su suscripción** |
    | Grupo de recursos | **myRGSecure** |
    | Nombre | **myNSGSecure** |
    | Región | **(EE. UU.) Este de EE. UU.**  |
    | | |

3. Haga clic en **Revisar y crear** y luego, después de la validación, haga clic en  **Crear**.

4. Después de crear el NSG, haga clic en **Ir al recurso**.

5. Debajo de **Configuración**, haga clic en **Interfaces de red** y luego en **+ Asociar**.

6. Seleccione la interfaz de red que identificó en la tarea anterior. 

# Tarea 3: Configurar una regla de puerto de seguridad entrante para permitir RDP

En esta tarea, permitiremos el tráfico RDP a la máquina virtual configurando una regla de puerto de seguridad entrante. 

1. En Azure Portal, navegue hasta la hoja de la máquina virtual **SimpleWinVM**. 

2. Sobre el panel de **Visión general**, haga clic en **Conectar**.

3. Intente conectarse a la máquina virtual mediante RDP. Por defecto, el grupo de seguridad de red no permite RDP. Cierre la ventana de error. 

    ![Captura de pantalla del mensaje de error de que la conexión de la máquina virtual ha fallado.](../images/1201.png)

4. En la hoja de la máquina virtual, desplácese hacia abajo hasta la sección **Configuración**, haga clic en **Redes** y observe las reglas de entrada para el grupo de seguridad de red **myNSGSecure (conectado a la interfaz de red: myVMNic)** niega todo el tráfico entrante, excepto el tráfico dentro de la red virtual y las sondas de equilibrador de carga.

5. Sobre la pestaña **Reglas de puerto de entrada**, haga clic en **Agregar regla de puerto de entrada** . Haga clic en **Agregar** cuando haya terminado. 

    | Configuración | Valor |
    | -- | -- |
    | Origen | **Cualquiera**|
    | Rangos de puertos de origen | **\*** |
    | Destino | **Cualquiera** |
    | Rangos de puertos de destino | **3389** |
    | Protocolo | **TCP** |
    | Acción | **Permitir** |
    | Prioridad | **300** |
    | Nombre | **AllowRDP** |
    | | |

6. Espere a que se aprovisione la regla y vuelva a intentar el RDP en la máquina virtual. Esta vez debería tener éxito. Recuerde que el usuario es **azureuser** y la contraseña es **Pa$$w0rd1234**.

# Tarea 4: Configurar una regla de puerto de seguridad saliente para denegar el acceso a Internet

En esta tarea, crearemos una regla de puerto saliente NSG que denegará el acceso a Internet y luego la probaremos para asegurarnos de que la regla funciona.

1. Continúe en su sesión de máquina virtual RDP. 

2. Después de que la máquina arranque, abra el explorador de **Internet Explorer**. 

3. Compruebe que puede acceder **https://www.bing.com** y luego cierre Internet Explorer. Deberá trabajar a través de las ventanas emergentes de seguridad mejorada de IE. 

    **Nota**: Ahora configuraremos una regla para denegar el acceso saliente a Internet. 

4. En Azure Portal, vuelva a la hoja de la máquina virtual **SimpleWinVM**. 

5. En **Configuración**, haga clic en **Redes** y, a continuación, en **Reglas de puerto de salida**.

6. Verá que hay una regla, **AllowInternetOutbound**. Esta es una regla predeterminada y no se puede eliminar. 

7. Haga clic en **Agregar regla de puerto de salida**, a la derecha del grupo de seguridad de red **myNSGSecure (conectado a la interfaz de red: myVMNic)** y configure una nueva regla de seguridad saliente con una prioridad más alta que denegará el tráfico de Internet. Seleccione **Agregar** cuando haya acabado. 

    | Configuración | Valor |
    | -- | -- |
    | Origen | **Cualquiera**|
    | Rangos de puertos de origen | **\*** |
    | Destino | **Etiqueta de servicio** |
    | Etiqueta de servicio de destino | **Internet** |
    | Rangos de puertos de destino | **\*** |
    | Protocolo | **TCP** |
    | Acción | **Deny** |
    | Prioridad | **4000** |
    | Nombre | **DenyInternet** |
    | | |

8. Vuelva a su sesión RDP. 

9. Visite **https://www.microsoft.com**. La página no debe mostrarse. Es posible que deba trabajar a través de ventanas emergentes de seguridad mejoradas de IE adicionales.  

**Nota**: Para evitar costes adicionales, puede quitar este grupo de recursos. Busque grupos de recursos, haga clic en su grupo de recursos y, a continuación, haga clic en **Eliminar grupo de recursos**. Compruebe el nombre del grupo de recursos y luego haga clic en **Eliminar**. Supervise las **Notificaciones** para ver cómo se realiza la eliminación.

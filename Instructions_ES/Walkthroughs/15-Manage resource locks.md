---
wts:
    title: '15 - Administrar bloqueos de recursos (5 min)'
    module: 'Módulo 05: Descripción de las características de identidad, gobernanza, privacidad y cumplimiento'
---
# 15 - Administrar bloqueos de recursos

En este tutorial, crearemos un grupo de recursos, agregaremos un bloqueo al grupo de recursos y probaremos su eliminación, probaremos la eliminación de un recurso en el grupo de recursos y quitaremos el bloqueo de recursos. 

# Tarea 1: Crear un grupo de recursos (5 min)

En esta tarea, crearemos un grupo de recursos para este ejercicio. 

1. Inicie sesión en [Azure Portal](https://portal.azure.com).

2. Desde la hoja **Todos los servicios**, busque y seleccione **Grupos de recursos**, luego seleccione **+ Agregar**.

3. Cree un grupo de recursos nuevo. Cuando haya terminado, haga clic en **Revisar + crear** y luego en **Crear**. 

    | Configuración | Valor |
    | -- | -- |
    | Suscripción | **Use su suscripción** |
    | Nombre | **myRGLocks** |
    | Región | **(EE. UU.) Este de EE. UU.** |
    | | |

# Tarea 2:  Agregar un bloqueo al grupo de recursos y probar su eliminación

En esta tarea, agregaremos un bloqueo de recursos al grupo de recursos y probaremos la eliminación del grupo de recursos. 

1. En Azure Portal, navegue hasta el grupo de recursos recién creado **myRGLocks**.

2. Puede aplicar un bloqueo a una suscripción, un grupo de recursos o un recurso individual para evitar la eliminación o modificación accidental de recursos críticos. 

3. En la sección **Configuración**, haga clic en **Bloqueos** y luego en **+ Agregar**. 

    ![Captura de pantalla del grupo de recursos myRGLocks que muestra el panel Bloqueos.](../images/1601.png)

4. Configure el nuevo bloqueo. Al finalizar, haga clic en **Aceptar**. 

    | Configuración | Valor |
    | -- | -- |
    | Nombre del bloqueo | **RGLock** |
    | Tipo de bloqueo | **Eliminar** |
    | | |

5. Haga clic en **Información general** y en **Eliminar grupo de recursos**. Escriba el nombre del grupo de recursos y haga clic en **Aceptar**. Recibirá un mensaje de error que indica que el grupo de recursos está bloqueado y que no se puede eliminar.

    ![Captura de pantalla del error sobre el bloqueo contra la eliminación.](../images/1602.png)

# Tarea 3: Probar a eliminar un miembro del grupo de recursos

En esta tarea, probaremos si el bloqueo de recursos protege una cuenta de almacenamiento en el grupo de recursos. 

1. Desde la hoja **Todos los servicios**, busque y seleccione **Cuentas de almacenamiento** y luego haga clic en **+ Agregar**. 

2. En la pestaña **Datos básicos** de la hoja **Crear cuenta de almacenamiento**, complete la siguiente información (reemplace **xxxx** en el nombre de la cuenta de almacenamiento con letras y dígitos de modo que el nombre sea globalmente único). Deje los valores predeterminados para todo lo demás.

    | Configuración | Valor | 
    | --- | --- |
    | Suscripción | **Seleccione su suscripción** |
    | Grupo de recursos | **myRGLocks** |
    | Nombre de la cuenta de almacenamiento | **storageaccountxxxx** |
    | Ubicación | **(EE. UU.) Este de EE. UU.**  |
    | Rendimiento | **Estándar** |
    | Tipo de cuenta | **Almacenamiento V2 (uso general v2)** |
    | Replicación | **Almacenamiento con redundancia local (LRS)** |
    | Nivel de acceso (predeterminado) | **Frecuente** |
    | | |

3. Haga clic en **Revisar y crear** para revisar la configuración de su cuenta de almacenamiento y permitir que Azure valide la configuración. 

4. Una vez validada, haga clic en **Crear**. Espere la notificación de que la cuenta se creó correctamente. 

5.  Espere la notificación de que la cuenta de almacenamiento se creó correctamente. 

6. Acceda a su nueva cuenta de almacenamiento y, desde el panel **Información general**, haga clic en **Eliminar**. Recibirá un mensaje de error que indica que el recurso o su primario tiene un bloqueo de eliminación. 

    ![Captura de pantalla del error al eliminar la cuenta de almacenamiento.](../images/1603.png)

    **Nota**: Aunque no hayamos creado específicamente un bloqueo para la cuenta de almacenamiento, hemos creado un bloqueo en el nivel del grupo de recursos que contiene la cuenta de almacenamiento. Como tal, este bloqueo de nivel *primario* nos impide eliminar el recurso y la cuenta de almacenamiento hereda el bloqueo del nivel primario.

# Tarea 4: Quitar el bloqueo de recurso

En esta tarea quitaremos el bloqueo del recurso y lo probaremos. 

1. Vuelva a la hoja del grupo de recursos **miRGLocks** y, en la sección **Configuración**, haga clic en **Bloqueos**.
    
2. Haga clic en el vínculo **Eliminar** a la derecha de la entrada **RGLock**.

    ![Captura de pantalla del bloqueo con el vínculo Eliminar resaltado](../images/1604.png)

3. Vuelva a la hoja de la cuenta de almacenamiento y confirme que ahora puede eliminar el recurso.

¡Enhorabuena! Creó un grupo de recursos, agregó un bloqueo al grupo de recursos y probó su eliminación, probó la eliminación de un recurso en el grupo de recursos y quitó el bloqueo de un recurso. 

**Nota**: Para evitar costes adicionales, puede quitar este grupo de recursos. Busque grupos de recursos, haga clic en su grupo de recursos y, a continuación, haga clic en **Eliminar grupo de recursos**. Compruebe el nombre del grupo de recursos y luego haga clic en **Eliminar**. Supervise las **Notificaciones** para ver cómo se realiza la eliminación.
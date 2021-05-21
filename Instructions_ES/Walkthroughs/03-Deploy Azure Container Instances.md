---
wts:
    title: '03 - Implementar Azure Container Instances (10 minutos)'
    module: 'Módulo 02: Servicios principales de Azure (Cargas de trabajo)'
---

# 03 - Implementación de Azure Container Instances

En este tutorial creamos, configuramos e implementamos un contenedor Docker mediante Azure Container Instances (ACI) en Azure Portal. El contenedor es una aplicación web Bienvenido a ACI que muestra una página HTML estática. 

# Tarea 1: Crear una instancia de contenedor (10 minutos)

En esta tarea, crearemos una nueva instancia de contenedor para la aplicación web. 

1. Inicie sesión en [Azure Portal](https://portal.azure.com).

2. Desde la hoja **Todos los servicios**, busque y seleccione **Container instances** y luego haga clic en **Agregar**. 

3. Proporcione los siguientes detalles básicos para la nueva instancia de contenedor (deje los valores predeterminados para todo lo demás): 

	| Configuración| Valor|
	|----|----|
	| Suscripción | **Elija su suscripción** |
	| Grupo de recursos | **myRGContainer** (crear nuevo) |
	| Nombre del contenedor| **mycontainer**|
	| Región | **(EE. UU.) Este de EE. UU.** |
	| Origen de imagen| **Docker Hub u otro registro**|
	| Tipo de imagen| **Público**|
	| Imagen| **microsoft / aci-helloworld**|
	| Tipo de sistema operativo| **Linux** |
	| Tamaño| ***Dejar en el valor predeterminado***|
	|||

4. Configure la pestaña Redes (reemplace **xxxx** con letras y dígitos para que el nombre sea globalmente único). Deje todas las demás configuraciones en sus valores predeterminados.

	| Configuración| Valor|
	|--|--|
	| Etiqueta de nombre DNS| **mycontainerdnsxxxx** |
	|||
	
	**Nota**: Su contenedor será accesible públicamente en dns-name-label.region.azurecontainer.io. Si recibe un mensaje de error que dice **Etiqueta de nombre DNS no disponible** después de la implementación, especifique una etiqueta de nombre DNS diferente (no use xxxx) y vuelva a implementar. 


	![Captura de pantalla del panel de configuración de la hoja Crear instancias de contenedor en Azure Portal, con la etiqueta de nombre DNS especificada. ](../images/0201.png)

5. Haga clic en **Revisar y crear** para iniciar el proceso de validación automática.

6. Haga clic en **Crear** para crear la instancia de contenedor. 

7. Supervise la página de implementación y la de **Notificaciones**. 

8. Mientras espera puede que esté interesado en ver el [código de muestra detrás de esta sencilla aplicación](https://github.com/Azure-Samples/aci-helloworld). Examine la carpeta \app. 

# Tarea 2: Compruebe la implementación de la instancia del contenedor

En esta tarea, comprobamos que la instancia del contenedor se está ejecutando asegurándonos de que se muestre la página principal.

1. Una vez completada la implementación, haga clic en el vínculo **Ir al recurso** en la hoja de implementación o el vínculo al recurso en el área de notificación.

2. En la hoja **Visión general** de **mycontainer**, asegúrese de que el **Estado** de su contenedor esté **ejecutándose**. 

3. Localice el nombre de dominio completo (FQDN).

	![Captura de pantalla del panel de información general para el contenedor recién creado en Azure Portal, con el FQDN resaltado. ](../images/0202.png)

2. Copie el FQDN del contenedor en el explorador web del cuadro de texto URL y presione **Entrar**. La página principal debería aparecer. 

	![Captura de pantalla del mensaje de bienvenida de ACI que se muestra en un explorador web.](../images/0203.png)

**Nota**: También puede usar la dirección IP del contenedor en su explorador. 

¡Enhorabuena! Ha usado Azure Portal para implementar con éxito una aplicación en un contenedor en instancia de contenedor Azure.

**Nota**: Para evitar costes adicionales, puede quitar este grupo de recursos. Busque grupos de recursos, haga clic en su grupo de recursos y, a continuación, haga clic en **Eliminar grupo de recursos**. Compruebe el nombre del grupo de recursos y luego haga clic en **Eliminar**. Supervise las **Notificaciones** para ver cómo se realiza la eliminación.

author: Pedro Luis Borrego Vargas
summary: Protección del arranque de Linux
id: arranquegrub2
categories: codelab,markdown
environments: Web
status: Published

# Protección del arranque de Linux (Grub2)

## Introducción.

En esta practica vamos a realizar un bastionado del arranque de linux (grub2).

Para ello, lo primero que tenemos que hacer es realizar un instalado común de un sistema linux, en nuestro caso debian.

## Ocultación del arranque.
Vamos a ocultar el arranque del menu de GRUB2 para que los usuarios que intenten acceder no puedan seleccionar ninguna opción.

Para ello abrimos el terminal, ingresamos como usuario root utilizando su - root y realizaremos los siguientes pasos:

Abrimos /etc/default/grub: nano /etc/default/grub. Para abrir el archivo de configuración de grub.

![Primer Paso](img/Captura5.png)

 Cambiamos GRUB_TIMEOUT=5 a GRUB_TIMEOUT=0 lo que realmente hacemos es que el usuario no tenga tiempo de seleccionar la opción.

![Segundo Paso](img/Captura6.png)

 Guardamos el archivo y salimos del editor de texto.

 Y hacemos un update-grub para actualizar la configuración.

![Tercer Paso](img/Captura7.png)

## Contraseña de arranque.

Vamos a colocar una contraseña para que el arranque solo lo pueda realizar un superusuario.

Modificaremos el archivo /etc/grub.d/40_custom en el cual tendremos que añadir al final las siguientes lineas:

set superusers=“root” y password root (CONTRASEÑA)

![Lineas en archivo](img/Captura8.png)

Realizaremos un update-grub para que se actualice en la configuración del arranque.

Vamos a cifrar tambien la contraseña que hemos seleccionado antes.

![Cifrado de contraseña](img/Captura9.png)

Tambien podemos editar los permisos del archivo para que solo root pueda ser editado por root.

![Permisos del archivo](img/Captura10.png)

## Copia de seguridad de configuración del arranque.

Este paso es bastante sencillo, solo tendremos que realizar un tar sobre los archivos de configuración del arranque(/etc/grub.d/40_custom y /etc/default/grub).

![tar en archivos](img/Captura11.png)


## Otras opciones de seguridad.

Para realizar esta opción deberiamos de haberlo empezado cuando estabamos instalando el sistema operativo, la coloco alfinal ya que es una opción secundaria.

Iniciaremos una configuración de la instalación manual.

En el particionamiento de discos seleccionaremos nuestro discos y crearemos una nueva tabla de particiones:

![particionado de discos](img/Captura1.png)

Una vez creada la tabla de particiones seleccionaremos el espacio libre que hemos creado:

![como crear una partición nueva](img/Captura2.png)

Realizare una de prueba con la raiz /boot para hacer una partición con todo lo necesario para el arranque del sistema, con 250MB serán suficientes:

![seleccionar espacio de partición](img/Captura3.png)

Al pulsar continuar, nos pedira seleccionar si queremos que sea una partición primaria o logica, la dejaremos en primaria y seleccionaremos que este al principio del espacio disponible.

Realizaremos lo mismo con cada raiz que consideremos oportuno particionar en mi caso swap, / , home, /var:

![particiones restantes](img/Captura4.png)

Una vez realizada las particiones, vamos a cifrarlas, para ello hacemos click en configurar los volúmenes cifrados y seguimos la guia, cuando acabemos, habremos terminado.







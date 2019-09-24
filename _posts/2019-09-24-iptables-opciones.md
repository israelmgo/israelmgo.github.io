---
layout: post
title: IPtables opciones
---

En esta segunda parte explicare una forma sencilla las opciones que dispone iptables para modificar la tabla filter, como comente el la anterior entrada conociendo iptables, solo tratare la tabla filter.

Lo primero que debemos hacer es abrir una terminal como superusuario, una vez echos esto y para poder ver la ayuda de iptables, debemos escribir lo siguinete:

#iptables -h

Como podéis ver al introducir* iptables -h* lo que hace es mostrarnos la ayuda de iptables, en la que se detalla todas las opciones de que disponemos, lo primero que haremos sera listar las cadenas de la tabla filter:

#iptables -L

Chain INPUT (policy ACCEPT)

target prot opt source destination

Chain FORWARD (policy ACCEPT)

target prot opt source destination

Chain OUTPUT (policy ACCEPT)

target prot opt source destination

Y como mostré en la anterior entrada nos indica las cadenas y reglas para la tabla filter, también se puede especificar la cadena por el nombre por ejemplo:

#iptables -L INPUT

Chain INPUT (policy ACCEPT)

target prot opt source       destination

Ahora ya podemos continuar con la creación y eliminación de cadenas con las siguientes opciones, para ello crearemos la cadena prueba y la eliminaremos.

#iptables -N prueba

Chain prueba (0 references)
*target     prot opt source       destination *

Y para eliminarla:

#iptables -X prueba

Ya hemos visto como listar, crear y eliminar cadenas, pero tenemos mas opciones:

#iptables -A  Añade una regla al final de la cadena indicada.

#iptables -D Borra una regla pero indicando el numero de regla.

#iptables -E  Renombrar una cadena.

#iptables -F  Limpia la cadena indicada de las reglas, si no especificas la cadena borra todas las reglas de todas las cadenas.

#iptables -I  Añade una regla pero indicando en que lugar dentro de la cadena.

#iptables -P  Cambia la política de una cadena indicada.

#iptables -R  Remplaza una regla en una cadena indicada.

#iptables -Z  Pone a cero los contadores de bytes y paquetes de todas las cadenas de la tabla.

Como podemos ver tenemos varias opciones que todavía se deben de ampliar mas, ademas con alguna de las opciones debemos fijarnos en especificar bien la cadena o podemos borrar las reglas de todas las cadenas, también podéis ver que todas las opciones se indican con letra mayúscula.

Si os habéis fijado cuando hemos creado la cadena y la listamos aparecía lo siguiente :

Chain prueba (0 references)
*target     prot opt source       destination *

Esto se debe que al crear cadena no la hemos indicado las reglas o políticas a seguir, ahora avanzaremos un poco mas haciendo un cambio en la cadena y ademas indicándole el puerto protocolo y que hacer con los paquetes, os recuerdo que las cadenas existentes son INPUT, OUTPUT y FORWARD.

#iptables -A INPUT  -p tcp –dport 21 -i DROP

Aquí ya empezamos con mas opciones, explicaremos un poco que es lo que estamos haciendo.

#iptables -A INPUT  Aqui estamos indicando que queremos añadir con -A al final del la cadena INPUT las siguiente regla.

*-p tcp * Con -p configuramos el protocolo y con tcp le indicamos cual (icmp, tcp, udp, all)

–dport 21  Con — dport le indicamos el puerto en este caso el 21 FTP

-i DROP  Con -i  podríamos especificar alguna interfaz ( eth0, wlan1..) o como en este caso, si no le indicamos la interfaz se lo aplica a todas.

Y finalmente con DROP, descartamos el paquete , por lo que en definitiva lo que hemos conseguido es cerrar el puerto 21, como es lógico podemos cambiar el protocolo, numero de puerto y regla, y así ajustar iptables a nuestra necesidad.

Otro ejemplo, pero en este caso añadimos otra opción :

#iptables -A INPUT -s 87.34.57.8 -p tcp –dport 22 -i ACCEPT

Ahora con -A añadimos esta regla al final de la cadena y con -s  especificamos una ip entrante, si ademas al final del la dirección IP le añadimos /20 , le indicamos un rango de puertos entre el 8 y el 20 que pueden acceder por el puerto 22 de nuestro sistema.

Explico alguna opción mas :

-p Configuramos el protocolo.

-s Indicamos la dirección de origen , también puede ser el nombre de un host, o una dirección de red.* *

-d Indicamos el destino puede ser igual que en -s un host, dirección de red o IP.

-i  Especificamos la interfaz de entrada.

-o Especificamos la interfaz de salida.

*-f: Aplica la regla solo a paquetes fragmentos. *

-j Especificamos el destino del paquete.

Y como guardo los cambios que haga?

Ya que cada vez que reiniciemos el sistema o apaguemos, los cambios se perderán es necesario poder guardar los cambios , siguiendo estos pasos podrás hacerlo :

*#iptables-save >  ruta/nombre del fichero
*

Si añadimos -c  también guardara los contadores y para recupera la configuración al inicio:

#iptables restore < ruta/nombre del fichero

Para poder cargar automáticamente la configuración de iptables podemos guardar el archivo el directorio etc/ y editar el archivo interfaces en etc/network con las siguientes lineas :

auto eth0

* iface eth0*

* inet dhcp*

* pre-up iptables-restore < /etc/nombre de archivo*

Como podemos ver podríamos extender esta entrada mucho mas, pero creo que para tener unos conocimientos básicos de funcionamiento y configuración de iptables es suficientes, si de todas maneras quieres profundizar mas a continuación de dejo unos enlaces:

Tutoriales y manuales en Netfilter

Iptables en la wikipedia

Espero que os sea de ayuda como lo fue para mi,  si ves que hay algo equivocado o quieres añadir algo sobre lo explicado o alguna configuración de iptables ,puedes hacerlo comentando esta entrada.

---
layout: post
title: You're up and running!
---

Iptables es seguramente la herramienta mas conocido del Framework Netfilter, que se encuentra incluido en el núcleo de Linux desde marzo de 2000, es el predecesor de Ipcahins , aquí podéis encontrar algunas de las diferencias entre ambos, también podemos decir sin duda alguna que es una de las herramientas por excelencia para la gestión de servidores.

Con iptables nos podremos encargar de la administración de las cadenas y reglas de las tablas que por defecto crea iptables, estas 3 tablas predeterminadas son la tabla FILTER, tabla NAT y tabla MANGLE.

Para gestionar la tabla filter nos bastara el comando* iptables* junto a sus diferentes opciones y especificaciones [Basic Syntax], en esta serie de entradas solo veremos como gestionar la tabla filters.



Empecemos por lo básico, como es la jerarquía de una tabla en Iptables, para ver nuestra tabla, abriremos un terminal y ejecutaremos el siguiente comando** iptables -L , y a continuación nos arrojara como resultado algo como esto:
**

Chain INPUT (policy ACCEPT)

target prot opt source destination

Chain FORWARD (policy ACCEPT)

target prot opt source destination

Chain OUTPUT (policy ACCEPT)

target prot opt source destination

Como podéis ver tenemos la TABLA que esta compuesta por las CADENAS (chain) que a su vez definen las REGLAS, que por defecto acepta todo.

CADENAS INPUT, OUTPUT Y FORWARD
Estas 3 cadenas  las podemos modificar para administra el comportamiento de los paquetes, ademas de estas cadenas podemos crear mas dentro de las tablas, de estas cadenas la primera de ellas input sera la encargada de decidir que hacer con los paquetes que entran, la cadena output se encargara de los paquetes que salen y la cadena forward se encarga de los paquetes que no van dirigidos a nosotros ni hemos creado localmente.

INPUT Paquetes entrantes.

OUTPUT Paquetes salientes.

FORWARD Paquetes  no generados localmente.

REGLAS
Con las reglas indicamos a la cadena que hacer con el paquete, compara las propiedades del destino, si es aceptado(ACCEPT), descartado(DROP), lo deja en cola(QUEUE) o lo retorna(RETURN), si coincide con la regla de destino de la cadena aborta el proceso en el resto de cadenas y el paquete es destinado, si por el contrario no coincide con una cadena pasa a la siguiente.

**ACCEPT: Acepta el paquete
**

**DROP: Descarta el paquete
**

**QUEUE: Deja en la cola el paquete
**

****RETURN: Retorna el paquete



Este proceso se genera con todos los paquetes, ya sean generados localmente o procedentes del exterior, por lo que con iptables tendremos un control mas especifico de todo el trafico de red y aplicando diferentes reglas a las diferentes cadenas podremos conseguir una mayor seguridad de nuestro sistema, incluso dejarnos incomunicados totalmente, a si que cuidado.

Esta primera entrada esta destinada a conocer Iptables y algo de su funcionamiento, y así en el siguiente poder desarrollar y aplicar las configuraciones con mayor conocimiento de lo que hacemos.

Espero vuestro comentarios, tanto para ampliar un poco mas su funcionamiento o simplemente para dar vuestra opinión.

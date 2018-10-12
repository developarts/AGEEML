# cat_localidad

Base de Datos del INEGI que contiene todos los estados, municipios y localidades de México trasladado a una Base de Datos MySQL

El archivo contiene 3 tablas: `estados`, `municipios` y `localidades`. El diseño de la base de datos se muestra en la siguiente imagen:

![DB Design](http://developarts.com/bl-content/uploads/db.png)

Los campos `clave` son una referencia numérica usado por el [INEGI](http://www.inegi.org.mx/) y están relacionados a su padre exceptuando estados. 

También agregué los campos `latitud`, `longitud` y `altitud` en la tabla `localidades`. Y para usar un sistema de mapas tipo *Google Maps* hago la conversión de latitud y longitud en los campos `lat` y `lng` 

La base de datos MySQL se puede descargar desde el siguiente enlace:

[Descargar](https://github.com/developarts/cat_localidad/releases/latest)


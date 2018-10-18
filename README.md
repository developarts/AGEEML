# Estados, Municipios y Localidades de México

![Diseño de Base de Datos](http://developarts.com/bl-content/uploads/inegibanner.png)
[![Github All Releases](https://img.shields.io/badge/Download-GitHub-orange.svg?style=flat-square)](https://github.com/developarts/cat_localidad/releases/latest) 
[![Packagist](https://img.shields.io/packagist/l/doctrine/orm.svg?style=flat-square)](https://opensource.org/licenses/MIT)

El [INEGI](http://www.inegi.org.mx/) cuenta con una base de datos de todos los Estados, Municipios y Localidades de la república mexicana. Específicamente en la sección [Catálogos Predefinidos](http://www.inegi.org.mx/geo/contenidos/geoestadistica/catalogoclaves.aspx).

En este proyecto, extraigo toda la información de ese archivo y la convierto a una base de datos MySQL.

* **32** Estados
* **2,463** Municipios
* **304,495** Localidades

<!-- pagebreak -->

El archivo contiene 3 tablas: `estados`, `municipios` y `localidades`. El diseño de la base de datos se muestra en la siguiente imagen:

![Diseño de Base de Datos](http://developarts.com/bl-content/uploads/inegidbdesign.png)

Los campos `clave` son una referencia numérica usado por el [INEGI](http://www.inegi.org.mx/) y están relacionados a su padre exceptuando estados. 

También agregué los campos `latitud`, `longitud` y `altitud` en la tabla `localidades`. Y para usar un sistema de mapas tipo *Google Maps* hago la conversión de latitud y longitud en los campos `lat` y `lng` 

**La base de datos MySQL se puede descargar desde el siguiente enlace:**

[![Descargar aquí](http://developarts.com/bl-content/uploads/github.png)](https://github.com/developarts/cat_localidad/releases/latest)

Espero que sea de utilidad para tu proyecto.

### Diccionario de Datos
#### estados
| Columna | tipo | Comentarios |
| --- | --- | --- |
| id | int(11) | ![Llave Primaria](http://developarts.com/bl-content/uploads/iconkey.png) |
| clave | varchar(2) | **CVE_ENT** - Clave de la entidad |
| nombre | varchar(40) | **NOM_ENT** - Nombre de la entidad |
| abrev | varchar(10) | **NOM_ABR** - Nombre abreviado de la entidad |
| activo | tinyint(1) |  |

#### municipios
| Columna | tipo | Comentarios |
| --- | --- | --- |
| id | int(11) | ![Llave Primaria](http://developarts.com/bl-content/uploads/iconkey.png) |
| estado_id | int(11) | Relación: _estados -> id_ |
| clave | varchar(3) | **CVE_MUN** - Clave del municipio |
| nombre | varchar(100) | **NOM_MUN** - Nombre del municipio |
| activo | tinyint(1) |  |

#### localidades
| Columna | tipo | Comentarios |
| --- | --- | --- |
| id | int(11) | ![Llave Primaria](http://developarts.com/bl-content/uploads/iconkey.png) |
| municipio_id | int(11) | Relación: _municipios -> id_ |
| clave | varchar(4) | **CVE_LOC** – Clave de la localidad |
| nombre | varchar(100) | **NOM_LOC** - Nombre de la localidad |
| latitud | varchar(15) | **LATITUD** - Latitud (en DMS) |
| longitud | varchar(15) | **LONGITUD** - Longitud (en DMS) |
| altitud | varchar(15) | **ALTITUD** - Altitud |
| carta | varchar(10) | **CVE_CARTA** |
| ambito | varchar(1) | **AMBITO** |
| poblacion | int(11) | **PTOT** - Población Total |
| masculino | int(11) | **PMAS** - Población Masculina |
| femenino | int(11) | **PFEM** - Población Femenina |
| viviendas | int(11) | **VTOT** - Número total de viviendas |
| lat | decimal(10,7) | Latitud en decimal |
| lng | decimal(10,7) | Longitud en decimal |
| activo | tinyint(1) |  |

-----

> ### Actualizaciones:
> 
> `[2018-10-18]` Se actualiza la información del INEGI a **SEP2018**.
> 
> `[2018-10-11]` Se creó el proyecto en GitHub para la distribución de los releases.
> 
> `[2016-02-01]`La base de datos del INEGI se encuentra actualizada a **ENE2016**.

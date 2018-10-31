# Estados, Municipios y Localidades de México
Base de Datos del INEGI en MySQL

![INEGI](http://developarts.com/bl-content/uploads/pages/0816cd7b202010d18c4740d5a698faa9/inegibanner.png)
[![Github All Releases](https://img.shields.io/badge/Download-GitHub-orange.svg?style=flat-square)](https://github.com/developarts/cat_inegi/releases/latest) 
[![Packagist](https://img.shields.io/packagist/l/doctrine/orm.svg?style=flat-square)](https://opensource.org/licenses/MIT)

El [INEGI](http://www.inegi.org.mx/) cuenta con una base de datos de todos los Estados, Municipios y Localidades de la república mexicana que actualiza cada mes. El archivo fuente se encuentra en formato _DBF_ y se puede descargar desde la sección [Catálogos Predefinidos](http://www.inegi.org.mx/geo/contenidos/geoestadistica/catalogoclaves.aspx) y consultar la [descripción](https://blog.openalfa.com/recursos-para-la-obtencion-de-datos-geograficos-de-mexico#Catalogos_de_Entidades_Estados_Municipios_y_Localidades) de los campos.

En este proyecto, extraigo toda la información de ese archivo y la convierto a una base de datos MySQL.

<!-- pagebreak -->

## Índice
-----
1. [Diseño](#link1)
2. [Coordenadas Geográficas](#link2)
3. [Descarga](#link3)
4. [Diccionario de Datos](#link4)
5. [Actualizaciones](#link5)

<!-- toc -->

## Diseño <a name="link1"></a>
-----

El archivo contiene 3 tablas: `estados`, `municipios` y `localidades`. El diseño de la base de datos se muestra en la siguiente imagen:


![Diseño de Base de Datos](http://developarts.com/bl-content/uploads/inegidbdesign.png)


He importado todos los campos que vienen en la base de datos del [INEGI](http://www.inegi.org.mx/), se pueden consultar en la sección _"Diccionario de Datos"_. Los campos importados están marcados en **negrita**.

Este es el conteo de registros:

* **32** Estados
* **2,463** Municipios
* **304,495** Localidades

## Coordenadas Geográficas <a name="link2"></a>
------

Los campos `latitud` y `longitud` vienen originalmente en un sistema de coordenadas **DMS** (Grados/Minutos/Segundos) y hago la conversión a un sistema de coordenadas **DD** (Grados Decimales) en los campos `lat` y `lng` para ser ocupados en sistemas de mapas tipo _Google Maps_


## Descarga <a name="link3"></a>
------

La base de datos MySQL se puede descargar desde el proyecto de GitHub dándo click en el siguiente enlace:

[![Descarga aquí](http://developarts.com/bl-content/uploads/github.png)](https://github.com/developarts/cat_inegi/releases/latest)



## Diccionario de Datos <a name="link4"></a>
------

Descripción de los campos de cada tabla del proyecto

### estados
| Columna | tipo | Comentarios |
| --- | --- | --- |
| `id` | _int(11)_ | ![Llave Primaria](http://developarts.com/bl-content/uploads/iconkey.png) |
| `clave` | _varchar(2)_ | **CVE_ENT** - Clave de la entidad |
| `nombre` | _varchar(40)_ | **NOM_ENT** - Nombre de la entidad |
| `abrev` | _varchar(10)_ | **NOM_ABR** - Nombre abreviado de la entidad |
| `activo` | _tinyint(1)_ |  |

### municipios
| Columna | tipo | Comentarios |
| --- | --- | --- |
| `id` | _int(11)_ | ![Llave Primaria](http://developarts.com/bl-content/uploads/iconkey.png) |
| `estado_id` | _int(11)_ | Relación: _`estados -> id`_ |
| `clave` | _varchar(3)_ | **CVE_MUN** - Clave del municipio |
| `nombre` | _varchar(100)_ | **NOM_MUN** - Nombre del municipio |
| `activo` | _tinyint(1)_ |  |

### localidades
| Columna | tipo | Comentarios |
| --- | --- | --- |
| `id` | _int(11)_ | ![Llave Primaria](http://developarts.com/bl-content/uploads/iconkey.png) |
| `municipio_id` | _int(11)_ | Relación: _`municipios -> id`_ |
| `clave` | _varchar(4)_ | **CVE_LOC** – Clave de la localidad |
| `nombre` | _varchar(100)_ | **NOM_LOC** - Nombre de la localidad |
| `latitud` | _varchar(15)_ | **LATITUD** - Latitud (en DMS) |
| `longitud` | _varchar(15)_ | **LONGITUD** - Longitud (en DMS) |
| `altitud` | _varchar(15)_ | **ALTITUD** - Altitud |
| `carta` | _varchar(10)_ | **CVE_CARTA** |
| `ambito` | _varchar(1)_ | **AMBITO** |
| `poblacion` | _int(11)_ | **PTOT** - Población Total |
| `masculino` | _int(11)_ | **PMAS** - Población Masculina |
| `femenino` | _int(11)_ | **PFEM** - Población Femenina |
| `viviendas` | _int(11)_ | **VTOT** - Número total de viviendas |
| `lat` | _decimal(10,7)_ | Latitud en DD |
| `lng` | _decimal(10,7)_ | Longitud en DD |
| `activo` | tinyint(1) |  |



## Actualizaciones <a name="link5"></a>
------

* `[2018-10-18]` Se actualizó la información del INEGI a **SEP2018**.
* `[2018-10-11]` Se creó el proyecto en GitHub para la distribución de los releases.
* `[2016-02-01]` Se actualizó la información del INEGI a **ENE2016**.

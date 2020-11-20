# Áreas Geoestadísticas Estatales, Municipales y Localidades

Base de Datos del INEGI en MySQL

![INEGI](http://developarts.com/bl-content/uploads/pages/0816cd7b202010d18c4740d5a698faa9/inegibanner.png)
![GitHub tag (latest by date)](https://img.shields.io/github/v/release/developarts/AGEEML?style=for-the-badge)
[![Packagist](https://img.shields.io/packagist/l/doctrine/orm.svg?style=for-the-badge)](https://opensource.org/licenses/MIT)
![GitHub all releases](https://img.shields.io/github/downloads/developarts/AGEEML/total?style=for-the-badge)
[![Donate with PayPal](https://img.shields.io/badge/PayPal-Donate-yellow.svg?style=for-the-badge)](https://www.paypal.me/developarts)

El [INEGI](http://www.inegi.org.mx/) cuenta con **“Catálogo Único de Claves de Áreas Geoestadísticas Estatales, Municipales y Localidades”**  de la república mexicana que actualiza cada mes. El archivo fuente se encuentra en varios formatos y se puede descargar desde la sección [Catálogos Predefinidos](https://www.inegi.org.mx/app/ageeml/) y consultar el documento de [descripción](https://www.inegi.org.mx/contenidos/app/ageeml/Ayuda/Ayuda_Gral_Cat_Unico.pdf) de los campos.

En este proyecto, extraigo toda la información de un archivo _CSV_ versión _UTF-8_ y lo convierto a una base de datos MySQL.

<!-- pagebreak -->

## Índice

1. [Diseño](#link1)
2. [Coordenadas Geográficas](#link2)
3. [Descarga](#link3)
4. [Diccionario de Datos](#link4)
5. [Actualizaciones](#link5)

<!-- toc -->

## Diseño <a name="link1"></a>

El archivo contiene 3 tablas: `estados`, `municipios` y `localidades`. El diseño de la base de datos se muestra en la siguiente imagen:


![Diseño de Base de Datos](http://developarts.com/bl-content/uploads/mysql_inegi.png)


He importado todos los campos que vienen en la base de datos del [INEGI](http://www.inegi.org.mx/), se pueden consultar en la sección _"Diccionario de Datos"_. Los campos importados están marcados en **negrita**.

Este es el conteo de registros:

* **32** Estados
* **2,469** Municipios
* **300,690** Localidades

El peso de la base de datos es de **37.3 MB**

La fecha de corte corresponde a **OCT 2020**


## Coordenadas Geográficas <a name="link2"></a>

Los campos `latitud` y `longitud` vienen originalmente en un sistema de coordenadas **DMS** (Grados/Minutos/Segundos) . Actualmente el archivo también cuenta con dos campos con un sistema de coordenadas **DD** (Grados Decimales) en los campos `lat` y `lng` para ser ocupados en sistemas de mapas tipo _Google Maps_


## Descarga <a name="link3"></a>

La base de datos MySQL se puede descargar desde el proyecto de GitHub dándo click en el siguiente enlace:

[![Descarga aquí](http://developarts.com/bl-content/uploads/github.png)](https://github.com/developarts/AGEEML/releases/latest)



## Diccionario de Datos <a name="link4"></a>

Descripción de los campos de cada tabla del proyecto


### estados
| Columna | tipo | Comentarios |
| --- | --- | --- |
| `id` | _int(11)_ | ![Llave Primaria](http://developarts.com/bl-content/uploads/iconkey.png) |
| `clave` | _varchar(2)_ | **Cve_Ent** - Clave de la entidad |
| `nombre` | _varchar(40)_ | **Nom_Ent** - Nombre de la entidad |
| `abrev` | _varchar(10)_ | **Nom_Abr** - Nombre abreviado de la entidad |
| `activo` | _tinyint(1)_ |  |


### municipios
| Columna | tipo | Comentarios |
| --- | --- | --- |
| `id` | _int(11)_ | ![Llave Primaria](http://developarts.com/bl-content/uploads/iconkey.png) |
| `estado_id` | _int(11)_ | Relación: _`estados -> id`_ |
| `clave` | _varchar(3)_ | **Cve_Mun** - Clave del municipio |
| `nombre` | _varchar(100)_ | **Nom_Mun** - Nombre del municipio |
| `activo` | _tinyint(1)_ |  |


### localidades
| Columna | tipo | Comentarios |
| --- | --- | --- |
| `id` | _int(11)_ | ![Llave Primaria](http://developarts.com/bl-content/uploads/iconkey.png) |
| `municipio_id` | _int(11)_ | Relación: _`municipios -> id`_ |
| `clave` | _varchar(4)_ | **Cve_Loc** – Clave de la localidad |
| `nombre` | _varchar(100)_ | **Nom_Loc** - Nombre de la localidad |
| `mapa` | _int(10)_ | **Mapa** - Identificador del INEGI |
| `ambito` | _varchar(1)_ | **Ámbito** - Clasificación |
| `latitud` | _varchar(15)_ | **Latitud** - Latitud en formato DMS |
| `longitud` | _varchar(15)_ | **Longitud** - Longitud en formato DMS |
| `lat` | _decimal(10,7)_ | **Lat_Decimal** Latitud en formato DD |
| `lng` | _decimal(10,7)_ | **Lon_Decimal** Longitud en formato DD |
| `altitud` | _varchar(15)_ | **Altitud** - Altitud |
| `carta` | _varchar(10)_ | **Cve_Carta** - Clave de carta topográfica |
| `poblacion` | _int(11)_ | **Pob_Total** - Población Total |
| `masculino` | _int(11)_ | **Pob_Masculina** - Población Masculina |
| `femenino` | _int(11)_ | **Pob_Femenina** - Población Femenina |
| `viviendas` | _int(11)_ | **Total De Viviendas Habitadas** - Total De Viviendas Habitadas |
| `activo` | tinyint(1) |  |


## Actualizaciones <a name="link5"></a>


* `[2020-11-20]` Se actualizó la información del INEGI a **OCT2020**.
* `[2018-10-18]` Se actualizó la información del INEGI a **SEP2018**.
* `[2018-10-11]` Se creó el proyecto en GitHub para la distribución de los releases.
* `[2016-02-01]` Se actualizó la información del INEGI a **ENE2016**.

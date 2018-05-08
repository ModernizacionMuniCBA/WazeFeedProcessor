# Waze Feed Processor
Procesador y administrador del Feed de datos que Waze entrega a las ciudades.

# Datos de Waze
Waze entrega un feed json/xml con datos minuto a minuto a las ciudades que forman pare del [programa CCP (Connected Citizens Program)](https://www.waze.com/es/ccp)

[Aquí](sample-data-test-modified.json) hay una version reducida de los datos que recibimos.

# Opción planificada
Nois parece interesante el camino que eligió Medellín (COL). Está contado en [este video](https://www.youtube.com/watch?v=eXK4F-Plz-k&feature=youtu.be&t=5h14m10s).

En resumen queremos usar: 
 - **Logstash** para conectarse a los datos y grabarlos
 - **Elasticsearch** para almacenar los datos
 - **Kibana** para analizar y visualizar los datos

# Otras opciones
La ciudad de Luisville en USA enfrento este problema y [dejo liberada una descripción de la infraestructura en GitHub](https://github.com/LouisvilleMetro/WazeCCPProcessor/). Al parecer ya hay decenas de Gobiernos usándola


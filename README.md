# Waze Feed Processor
Procesador y administrador del Feed de datos que Waze entrega a las ciudades.

# Datos de Waze
Waze entrega un feed json/xml con datos minuto a minuto a las ciudades que forman pare del [programa CCP (Connected Citizens Program)](https://www.waze.com/es/ccp)

# Opción planificada
Usar: 
 - **Logstash** para conectarse a los datos y grabarlos
 - **Elasticsearch** para almacenar los datos
 - **Kibana** para analizar y visualizar los datos

# Otras opciones
La ciudad de Luisville en USA enfrento este problema y [dejo liberada una descripción de la infraestructura en GitHub](https://github.com/LouisvilleMetro/WazeCCPProcessor/). Al parecer ya hay decenas de Gobiernos usándola


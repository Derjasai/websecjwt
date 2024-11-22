# websecjwt
Proyecto web el cual permite que el usuario cree una cuenta y pueda hacer login para poder pedirle a un unicornio que lo reoja en una ubicación determinada en el mapa

# Arquitectura
![img_14.png](img_14.png)

La arquitectura del aplicativo está descrita en la anterior imagen, como se puede apreciar primero se tiene un cliente
JS el cual permite renderizar una página web la cual nos permite hacer tanto el registro como el logeo de una cuenta, este
proceso se válida mediante Cognito el cual nos genera un JWT, el proceso de despliegue se hace de manera automatica mediante
Amplify, el cual tambien es el responsable de sostener el frontend.

Cuando el cliente JS hace una petición se realiza mediante el API Gateway el cual válida con Cognito que el token generado 
sea correcto, este API Gateway esá conectado de manera directa con una lambda la cual tiene como objetivo realizar la creación
de entidades una tabla, la cual esta hosteado en DynamoDB.

## Flujo del aplicativo

1. El navegador web carga la aplicación frontend desde AWS Amplify.
2. Los usuarios se autentican utilizando Amazon Cognito, que valida su identidad y emite tokens.
3. Las solicitudes autenticadas del frontend viajan a través del Amazon API Gateway.
4. El API Gateway pasa las solicitudes a AWS Lambda, que ejecuta la lógica necesaria.
5. AWS Lambda interactúa con Amazon DynamoDB para manejar los datos requeridos por la aplicación.

# Paso a paso creacion recursos / evidencias
## Modulo 1

Creación del amplify conectado con el repositorio de github
![img.png](img.png)
![img_1.png](img_1.png)

Página web desplegada
![img_2.png](img_2.png)

Despliegues realizados al cambiar el titulo de la página web y hacer un commit
![img_3.png](img_3.png)

## Modulo 2

Creación del Cognito para la autenticación
![img_4.png](img_4.png)
![img_5.png](img_5.png)

configuracion realizada de manera local para el cognito:
```
window._config = {
    cognito: {
        userPoolId: 'us-east-1_RM2RTbayN', // e.g. us-east-2_uXboG5pAb
        userPoolClientId: '5uofcghhngbrto53vcn40kr39g', // e.g. 25ddkmj4v6hfsfvruhpfi7n4hv
        region: 'us-east-1' // e.g. us-east-2
    },
    api: {
        invokeUrl: '' // e.g. https://rc7nyt4tql.execute-api.us-west-2.amazonaws.com/prod',
    }
};
```

Prueba de logeo con el usuario creado icnluyendo el código de verificación
![img_6.png](img_6.png)

Token JWT generado

![img_7.png](img_7.png)

## Modulo 3

Creación de la tabla Rides en DynamoDB
![img_8.png](img_8.png)

Creación de la lambda para crear recursos en la DB
![img_13.png](img_13.png)

Test funcional ejecutado en la lambda
![img_9.png](img_9.png)

## Modulo 4

Creación del authorizer dentro del api gateway
![img_10.png](img_10.png)

Configuración del método POST
![img_11.png](img_11.png)

Prueba de funcionamiento
![img_12.png](img_12.png)

# Version
1.0

# Author
Daniel Esteban Ramos Jimenez
### Crear función Handler en Lambda

1) Dentro de Lambda, creamos la función que tendrá la lógica para responder a solicitudes a Alexa (runtime Python 3.8):

![](images/LambdaHandler_ES/2020-11-24T21-01-20.png)

Seleccionamos VPC y subnet donde se encuentre instancia SAP, además de grupo de seguridad con acceso a puertos 33(nro de instancia):

![](images/LambdaHandler_ES/2020-11-24T21-03-22.png)

![](images/LambdaHandler_ES/2020-11-24T21-03-54.png)


2) Luego de crear la función, seleccionar el Layer creado en pasos anteriores:

![](images/LambdaHandler_ES/2020-11-24T21-05-22.png)

3) Copiar y pegar el siguiente código:

```Python
{
Poner Python Lambda aquí.
    }]
}
```

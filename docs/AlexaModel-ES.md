### Crear Skill para Alexa

1) Ingresar a Alexa Developer Console (https://developer.amazon.com/alexa/console/ask) con cuenta de desarrollador. Si no tiene, crear una nueva.

2) En la consola presionar "Create Skill":

![](images/AlexaModel/2020-11-24T21-49-51.png)

3) Indicar un nombre para Skill y el lenguaje por defecto (NOTA: Este leguaje debe ser el mismo que esté configfurado en el dispositivo a probar).

![](images/AlexaModel/2020-11-24T21-51-37.png)

Seleccionar modelo Custom:
![](images/AlexaModel/2020-11-24T21-53-20.png)

Y en método de host seleccionar "Provision your own"
![](images/AlexaModel/2020-11-24T21-53-00.png)

Luego "Create Skill"

4) En el Template, seleccionar "Start from scratch":
![](images/AlexaModel/2020-11-24T21-54-09.png)

5) En la siguiente pantalla, seleccionar "Interaction Model->JSON Editor":
![](images/AlexaModel/2020-11-24T21-56-24.png)

6) Copiar y pegar el siguiente código:

```JSON
{
    "interactionModel": {
        "languageModel": {
            "invocationName": "bandeja sap",
            "intents": [
                {
                    "name": "AMAZON.FallbackIntent",
                    "samples": []
                },
                {
                    "name": "AMAZON.CancelIntent",
                    "samples": []
                },
                {
                    "name": "AMAZON.HelpIntent",
                    "samples": []
                },
                {
                    "name": "AMAZON.StopIntent",
                    "samples": [
                        "salir de bandeja",
                        "salir de bandeja sap"
                    ]
                },
                {
                    "name": "AMAZON.NavigateHomeIntent",
                    "samples": []
                },
                {
                    "name": "ContarItems",
                    "slots": [],
                    "samples": [
                        "cuantos pedidos tengo pendientes por aprobar",
                        "cantidad de documentos",
                        "cuantos documentos tengo",
                        "cuantos documentos tengo en la bandeja",
                        "cuantos documentos tengo pendientes",
                        "cuanto documentos tengo por aprobar"
                    ]
                },
                {
                    "name": "DocumentoAntiguo",
                    "slots": [],
                    "samples": [
                        "documento mas viejo",
                        "documento mas atrasado",
                        "cual es el documento mas antiguo",
                        "documento mas antiguo"
                    ]
                },
                {
                    "name": "AMAZON.YesIntent",
                    "samples": []
                },
                {
                    "name": "AMAZON.NoIntent",
                    "samples": []
                },
                {
                    "name": "AprobarPedido",
                    "slots": [],
                    "samples": [
                        "aprueba pedido",
                        "aprobar pedido"
                    ]
                },
                {
                    "name": "BuscarPedido",
                    "slots": [
                        {
                            "name": "nro_pedido",
                            "type": "AMAZON.NUMBER"
                        }
                    ],
                    "samples": [
                        "busca el pedido {nro_pedido}"
                    ]
                },
                {
                    "name": "BuscarPedidoPorNumero",
                    "slots": [
                        {
                            "name": "fin_nro_pedido",
                            "type": "AMAZON.FOUR_DIGIT_NUMBER"
                        }
                    ],
                    "samples": [
                        "busca el pedido que termina con {fin_nro_pedido}"
                    ]
                }
            ],
            "types": []
        }
    }
}
````

7) Presionar "Save Model" y luego "Build Model". El módelo será construido en unos segundos.

8) En la consola de Alexa seleccionamos "Endpoint" y copiamos el Skill ID:
![](images/AlexaModel/2020-11-24T22-02-21.png)


8) Volvemos a nuestra función en Lambda y seleccionamos "Add Trigger". Para el tipo de trigger seleccionamos Alexa Skills Kit e indicamos el Skill ID previamente copiado:

![](images/AlexaModel/2020-11-24T22-04-37.png)

amzn1.ask.skill.cb0c71de-1df1-481e-8657-ed0d042998af

Luego copiamos el ARN de la función Lambda:
![](images/AlexaModel/2020-11-24T22-00-40.png)

9) Volvemos a la consola de Alexa y en default region pegamos el ARN de la función lambda previamente copiado:

![](images/AlexaModel/2020-11-24T22-07-33.png)

Luego "Save endpoints"

10) Para probar vamos al menu superior "Test" e indicamos  "Abre bandeja SAP". Alexa debería responder con el mensaje de bienvenida del Skill:

![](images/AlexaModel/2020-11-24T22-16-14.png)

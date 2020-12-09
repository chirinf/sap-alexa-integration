### Criar função Handler no Lambda

1) Faça login no Alexa Developer Console (https://developer.amazon.com/alexa/console/ask) com conta de desenvolvedor. Se você não tiver, crie um novo.

2) No console pressione “Criar habilidade”:

![](images/AlexaModel/2020-11-24T21-49-51.png)

3) Digite um nome para Habilidade e o idioma padrão (NOTA: Este idioma deve ser o mesmo que configurado no dispositivo a ser testado).

![](images/AlexaModel/2020-11-24T21-51-37.png)

Selecione o modelo personalizado:
![](images/AlexaModel/2020-11-24T21-53-20.png)

E no método host selecione “Provisionar seu próprio”
![](images/AlexaModel/2020-11-24T21-53-00.png)

Então “Criar Habilidade”

4) No Modelo, selecione “Começar do zero”:
![](images/AlexaModel/2020-11-24T21-54-09.png)

5) Na próxima tela, selecione “Modelo de interação->Editor JSON”:
![](images/AlexaModel/2020-11-24T21-56-24.png)

6) Copie e cole o seguinte código:

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

7) Pressione “Salvar modelo” e, em seguida, “Build Model”. O modelo será construído em poucos segundos.

8) No console Alexa selecione “Endpoint” e copie o ID da habilidade:
![](images/AlexaModel/2020-11-24T22-02-21.png)


Retornamos à nossa função no Lambda e selecionamos “Add Trigger”. Para o tipo de gatilho, selecione Alexa Skills Kit e indique o ID de habilidade copiado anteriormente:

![](images/AlexaModel/2020-11-24T22-04-37.png)


Em seguida, copiamos o ARN da função Lambda:
![](images/AlexaModel/2020-11-24T22-00-40.png)

9) Retornamos ao console Alexa e, na região padrão, colamos o ARN da função lambda anteriormente copiada:

![](images/AlexaModel/2020-11-24T22-07-33.png)

Em seguida, “Salvar endpoints”

10) Para testar vá para o menu superior “Teste” e indique “Abrir bandeja SAP”. Alexa deve responder com a mensagem de boas-vindas da habilidade:

![](images/AlexaModel/2020-11-24T22-16-14.png)

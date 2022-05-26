#### Actualizar indice transacciones_rest en elasticsearch, para corregir el campo fechapago con valor null
``` json
{
    "script": {
        "lang": "painless",
        "source": "ctx._source.fechapago = ZonedDateTime.parse(ctx._source.fechapago_real).toInstant().toEpochMilli()"
    },
    "indice": "transacciones_rest",
    "query": {
        "bool": {
            "must": [
                {
                    "terms": {
                        "id": [
                            
                        ]
                    }
                }
            ]
        }
    }
}
```

#### Actualizar indice recaudo_facturas en elasticsearch, para corregir el campo fechapagoreal con valor null
``` json
{
    "script": {
        "lang": "painless",
        "source": "for(pago in ctx._source.pagos) { pago.fechapagoreal = pago.fechapago }"
    },
    "indice": "recaudo_facturas",
    "query": {
        "bool": {
            "must": [
                {
                    "terms": {
                        "pagos.referencia_epayco": [
                            
                        ]
                    }
                }
            ]
        }
    }
}
```
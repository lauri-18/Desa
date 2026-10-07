{
    "name": "Integration Telegram Bot",
    "flow": [
        {
            "id": 1,
            "module": "telegram:WatchUpdates",
            "version": 1,
            "parameters": {
                "__IMTHOOK__": 2901256
            },
            "mapper": {},
            "metadata": {
                "designer": {
                    "x": -1182,
                    "y": 5
                },
                "setupValidation": {
                    "result": {
                        "valid": true,
                        "fields": []
                    },
                    "version": 1,
                    "configuration": "eac956a0dbd90bb"
                },
                "restore": {
                    "parameters": {
                        "__IMTHOOK__": {
                            "data": {
                                "editable": "false"
                            },
                            "label": "biodiversidad"
                        }
                    }
                },
                "parameters": [
                    {
                        "name": "__IMTHOOK__",
                        "type": "hook:telegramapi",
                        "label": "Webhook",
                        "required": true
                    }
                ]
            }
        },
        {
            "id": 2,
            "module": "builtin:BasicRouter",
            "version": 1,
            "mapper": null,
            "metadata": {
                "designer": {
                    "x": -751,
                    "y": -392
                }
            },
            "routes": [
                {
                    "flow": [
                        {
                            "id": 3,
                            "module": "telegram:SendReplyMessage",
                            "version": 1,
                            "parameters": {
                                "__IMTCONN__": 10783886
                            },
                            "filter": {
                                "name": "no tiene foto",
                                "conditions": [
                                    [
                                        {
                                            "a": "{{1.message.photo}}",
                                            "o": "notexist"
                                        }
                                    ]
                                ]
                            },
                            "mapper": {
                                "text": "Eres un bot botánico empático, amigable y muy práctico. Tu objetivo es ayudar a los usuarios a rescatar o cuidar sus plantas respondiendo siempre de manera concisa y clara.Debes decirle riesgos cuidados y la salud de la planta.",
                                "chatId": "{{1.message.chat.id}}",
                                "parseMode": "",
                                "replyMarkup": "",
                                "messageThreadId": "",
                                "replyToMessageId": "",
                                "replyMarkupAssembleType": "reply_markup_enter"
                            },
                            "metadata": {
                                "designer": {
                                    "x": -742,
                                    "y": 57
                                },
                                "setupValidation": {
                                    "result": {
                                        "valid": true,
                                        "fields": []
                                    },
                                    "version": 1,
                                    "configuration": "4f918c105eb9bf6f"
                                },
                                "restore": {
                                    "expect": {
                                        "parseMode": {
                                            "label": "Empty"
                                        },
                                        "disableNotification": {
                                            "mode": "chose"
                                        },
                                        "replyMarkupAssembleType": {
                                            "label": "Enter the Reply Markup"
                                        }
                                    },
                                    "parameters": {
                                        "__IMTCONN__": {
                                            "data": {
                                                "scoped": "true",
                                                "connection": "telegram"
                                            },
                                            "label": "economia bot"
                                        }
                                    }
                                },
                                "parameters": [
                                    {
                                        "name": "__IMTCONN__",
                                        "type": "account:telegram",
                                        "label": "Connection",
                                        "required": true
                                    }
                                ],
                                "expect": [
                                    {
                                        "name": "chatId",
                                        "type": "text",
                                        "label": "Chat ID",
                                        "required": true
                                    },
                                    {
                                        "name": "text",
                                        "type": "text",
                                        "label": "Text",
                                        "required": true
                                    },
                                    {
                                        "name": "messageThreadId",
                                        "type": "number",
                                        "label": "Message Thread ID"
                                    },
                                    {
                                        "name": "parseMode",
                                        "type": "select",
                                        "label": "Parse Mode",
                                        "validate": {
                                            "enum": [
                                                "Markdown",
                                                "HTML"
                                            ]
                                        }
                                    },
                                    {
                                        "name": "disableNotification",
                                        "type": "boolean",
                                        "label": "Disable Notifications"
                                    },
                                    {
                                        "name": "disableWebPagePreview",
                                        "type": "boolean",
                                        "label": "Disable Link Previews"
                                    },
                                    {
                                        "name": "replyToMessageId",
                                        "type": "number",
                                        "label": "Original Message ID"
                                    },
                                    {
                                        "name": "replyMarkupAssembleType",
                                        "type": "select",
                                        "label": "Enter/Assemble the Reply Markup Field",
                                        "validate": {
                                            "enum": [
                                                "reply_markup_enter",
                                                "reply_markup_assemble"
                                            ]
                                        }
                                    },
                                    {
                                        "name": "replyMarkup",
                                        "type": "text",
                                        "label": "Reply Markup"
                                    }
                                ]
                            }
                        }
                    ]
                },
                {
                    "flow": [
                        {
                            "id": 4,
                            "module": "telegram:DownloadFile",
                            "version": 1,
                            "parameters": {
                                "__IMTCONN__": 11533117
                            },
                            "filter": {
                                "name": "tiene foto",
                                "conditions": [
                                    [
                                        {
                                            "a": "{{1.message.photo}}",
                                            "o": "exist"
                                        }
                                    ]
                                ]
                            },
                            "mapper": {
                                "fileId": "{{1.message.photo[].file_id}}"
                            },
                            "metadata": {
                                "designer": {
                                    "x": -305,
                                    "y": 52
                                },
                                "setupValidation": {
                                    "result": {
                                        "valid": true,
                                        "fields": []
                                    },
                                    "version": 1,
                                    "configuration": "a7ec7919247151b9"
                                },
                                "restore": {
                                    "parameters": {
                                        "__IMTCONN__": {
                                            "data": {
                                                "scoped": "true",
                                                "connection": "telegram"
                                            },
                                            "label": "Laura's Telegram Bot connection"
                                        }
                                    }
                                },
                                "parameters": [
                                    {
                                        "name": "__IMTCONN__",
                                        "type": "account:telegram",
                                        "label": "Connection",
                                        "required": true
                                    }
                                ],
                                "expect": [
                                    {
                                        "name": "fileId",
                                        "type": "text",
                                        "label": "File ID",
                                        "required": true
                                    }
                                ]
                            }
                        },
                        {
                            "id": 5,
                            "module": "ai-local-agent:RunLocalAIAgent",
                            "version": 0,
                            "parameters": {
                                "makeConnectionId": 11544541
                            },
                            "mapper": {
                                "files": [
                                    {
                                        "data": "{{4.data}}",
                                        "fileName": "foto.jpg"
                                    }
                                ],
                                "message": "Analiza la imagen adjunta siguiendo tus instrucciones",
                                "threadId": "",
                                "outputType": "text",
                                "tokenLimit": "50",
                                "modelConfig": {
                                    "timeout": "",
                                    "recursionLimit": "300",
                                    "aiCompactionEnabled": true,
                                    "iterationsFromHistoryCount": "10"
                                },
                                "defaultModel": "medium",
                                "systemPrompt": "Actúa como un bot botánico empático, amigable y muy práctico. Genera un diagnóstico para la siguiente planta siguiendo estrictamente estas reglas:\r\n\r\n[DATOS DE LA PLANTA]\r\n- Planta: {{1.nombre_planta}}\r\n- Síntomas observados: {{1.sintomas}}\r\n- Frecuencia de riego actual: {{1.frecuencia_riego}}\r\n- Ubicación / Luz: {{1.ubicacion_luz}}\r\n\r\n[INSTRUCCIONES DE FORMATO Y CONTENIDO]\r\nGenera una respuesta amigable organizada exactamente en las siguientes 3 secciones con emoticonos:\r\n\r\n1. 🩺 DIAGNÓSTICO DE SALUD\r\n- Identifica el problema principal según los síntomas y la luz (ej. exceso de agua, falta de luz, plaga o deshidratación).\r\n- Da un mensaje de tranquilidad de 1 a 2 oraciones.\r\n\r\n2. 💧 PLAN DE RIEGO\r\n- Frecuencia sugerida exacta (ej. \"Cada 8-10 días\" o \"Solo cuando el sustrato esté seco\").\r\n- Técnica de riego recomendada (ej. riego por inmersión, drenaje completo o pulverizado).\r\n- Prueba del palito o sustrato para comprobar la humedad.\r\n\r\n3. ☀️ CUIDADOS ESENCIALES\r\n- Nivel de luz ideal (luz indirecta, sol directo, sombra).\r\n- Tipo de maceta o drenaje recomendado.\r\n- Un consejo adicional o truco clave (ej. limpiar hojas, rotar la maceta).\r\n\r\nREGLAS ADICIONALES:\r\n- Usa un tono cercano, entusiasta y sencillo.\r\n- Usa listas con viñetas para facilitar la lectura.\r\n- Longitud máxima: 200 palabras.",
                                "promptCaching": "none",
                                "fallbackEnabled": false
                            },
                            "metadata": {
                                "designer": {
                                    "x": -139,
                                    "y": -371
                                },
                                "setupValidation": {
                                    "result": {
                                        "valid": true,
                                        "fields": []
                                    },
                                    "version": 1,
                                    "configuration": "41669b33fa51bf1d"
                                },
                                "restore": {
                                    "expect": {
                                        "files": {
                                            "mode": "chose",
                                            "items": [
                                                null
                                            ]
                                        },
                                        "outputType": {
                                            "label": "Text"
                                        },
                                        "defaultModel": {
                                            "mode": "chose",
                                            "label": "MediumModel: gpt-5-nano. Reasoning: low. A balanced, quick choice for clearly defined tasks needing reliable answers rather than deep analysis"
                                        },
                                        "promptCaching": {
                                            "label": "Automatic (always on)"
                                        }
                                    },
                                    "parameters": {
                                        "makeConnectionId": {
                                            "data": {
                                                "scoped": "true",
                                                "connection": "ai-provider"
                                            },
                                            "label": "Laura's Make's AI Provider connection"
                                        }
                                    }
                                },
                                "parameters": [
                                    {
                                        "name": "makeConnectionId",
                                        "type": "account:ai-provider,openai-gpt-3,anthropic-claude,gemini-ai-q9zyjp,ai-agent-foundry-openai,ai-agent-foundry-non-openai,mistral-ai,cohere,groq,ai-agent-xai,amazon-bedrock,ai-agent-openai-compatible",
                                        "label": "Connection",
                                        "required": true
                                    }
                                ],
                                "expect": [
                                    {
                                        "name": "defaultModel",
                                        "type": "select",
                                        "label": "Model",
                                        "required": true
                                    },
                                    {
                                        "name": "tokenLimit",
                                        "type": "number",
                                        "label": "Maximum output length (%)",
                                        "validate": {
                                            "max": 100,
                                            "min": 20
                                        }
                                    },
                                    {
                                        "name": "promptCaching",
                                        "type": "select",
                                        "label": "Prompt caching",
                                        "validate": {
                                            "enum": [
                                                "none"
                                            ]
                                        }
                                    },
                                    {
                                        "name": "fallbackEnabled",
                                        "type": "boolean",
                                        "label": "Enable fallback connection",
                                        "required": true
                                    },
                                    {
                                        "name": "systemPrompt",
                                        "type": "text",
                                        "label": "Instructions"
                                    },
                                    {
                                        "name": "message",
                                        "type": "text",
                                        "label": "Input",
                                        "required": true
                                    },
                                    {
                                        "name": "files",
                                        "spec": [
                                            {
                                                "name": "fileName",
                                                "type": "filename",
                                                "label": "File name",
                                                "semantic": "file:name"
                                            },
                                            {
                                                "name": "data",
                                                "type": "buffer",
                                                "label": "Data",
                                                "semantic": "file:data"
                                            }
                                        ],
                                        "type": "array",
                                        "label": "Input files"
                                    },
                                    {
                                        "name": "threadId",
                                        "type": "text",
                                        "label": "Conversation ID",
                                        "validate": {
                                            "max": 256
                                        }
                                    },
                                    {
                                        "name": "modelConfig",
                                        "spec": [
                                            {
                                                "name": "recursionLimit",
                                                "type": "number",
                                                "label": "Steps per agent call"
                                            },
                                            {
                                                "name": "iterationsFromHistoryCount",
                                                "type": "number",
                                                "label": "Maximum conversation history"
                                            },
                                            {
                                                "name": "timeout",
                                                "type": "number",
                                                "label": "Step timeout",
                                                "validate": {
                                                    "max": 600,
                                                    "min": 120
                                                }
                                            },
                                            {
                                                "name": "aiCompactionEnabled",
                                                "type": "boolean",
                                                "label": "Enable compaction",
                                                "required": true
                                            }
                                        ],
                                        "type": "collection",
                                        "label": "Model configuration"
                                    },
                                    {
                                        "name": "outputType",
                                        "type": "select",
                                        "label": "Response format",
                                        "required": true,
                                        "validate": {
                                            "enum": [
                                                "text",
                                                "make-schema",
                                                "udt-schema"
                                            ]
                                        }
                                    }
                                ]
                            },
                            "tools": []
                        },
                        {
                            "id": 6,
                            "module": "telegram:SendReplyMessage",
                            "version": 1,
                            "parameters": {
                                "__IMTCONN__": 11537654
                            },
                            "mapper": {
                                "text": "{{{5.response}}}(respuesta del AI Agent)",
                                "chatId": "{{1.message.chat.id}}",
                                "parseMode": "",
                                "replyMarkup": "",
                                "messageThreadId": "",
                                "replyToMessageId": "",
                                "replyMarkupAssembleType": "reply_markup_enter"
                            },
                            "metadata": {
                                "designer": {
                                    "x": 89,
                                    "y": 110
                                },
                                "setupValidation": {
                                    "result": {
                                        "valid": true,
                                        "fields": []
                                    },
                                    "version": 1,
                                    "configuration": "6b0bb2704a920955"
                                },
                                "restore": {
                                    "expect": {
                                        "parseMode": {
                                            "label": "Empty"
                                        },
                                        "disableNotification": {
                                            "mode": "chose"
                                        },
                                        "replyMarkupAssembleType": {
                                            "label": "Enter the Reply Markup"
                                        }
                                    },
                                    "parameters": {
                                        "__IMTCONN__": {
                                            "data": {
                                                "scoped": "true",
                                                "connection": "telegram"
                                            },
                                            "label": "Laura's Telegram Bot connection"
                                        }
                                    }
                                },
                                "parameters": [
                                    {
                                        "name": "__IMTCONN__",
                                        "type": "account:telegram",
                                        "label": "Connection",
                                        "required": true
                                    }
                                ],
                                "expect": [
                                    {
                                        "name": "chatId",
                                        "type": "text",
                                        "label": "Chat ID",
                                        "required": true
                                    },
                                    {
                                        "name": "text",
                                        "type": "text",
                                        "label": "Text",
                                        "required": true
                                    },
                                    {
                                        "name": "messageThreadId",
                                        "type": "number",
                                        "label": "Message Thread ID"
                                    },
                                    {
                                        "name": "parseMode",
                                        "type": "select",
                                        "label": "Parse Mode",
                                        "validate": {
                                            "enum": [
                                                "Markdown",
                                                "HTML"
                                            ]
                                        }
                                    },
                                    {
                                        "name": "disableNotification",
                                        "type": "boolean",
                                        "label": "Disable Notifications"
                                    },
                                    {
                                        "name": "disableWebPagePreview",
                                        "type": "boolean",
                                        "label": "Disable Link Previews"
                                    },
                                    {
                                        "name": "replyToMessageId",
                                        "type": "number",
                                        "label": "Original Message ID"
                                    },
                                    {
                                        "name": "replyMarkupAssembleType",
                                        "type": "select",
                                        "label": "Enter/Assemble the Reply Markup Field",
                                        "validate": {
                                            "enum": [
                                                "reply_markup_enter",
                                                "reply_markup_assemble"
                                            ]
                                        }
                                    },
                                    {
                                        "name": "replyMarkup",
                                        "type": "text",
                                        "label": "Reply Markup"
                                    }
                                ]
                            }
                        }
                    ]
                }
            ]
        }
    ],
    "metadata": {
        "instant": true,
        "version": 1,
        "scenario": {
            "roundtrips": 1,
            "maxErrors": 3,
            "autoCommit": true,
            "autoCommitTriggerLast": true,
            "sequential": false,
            "slots": null,
            "confidential": false,
            "dataloss": false,
            "dlq": false,
            "freshVariables": false
        },
        "designer": {
            "orphans": []
        },
        "zone": "us2.make.com",
        "notes": []
    }
}

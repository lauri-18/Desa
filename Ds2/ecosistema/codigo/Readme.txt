
{
    "name": "Integration Telegram Bot",
    "flow": [
        {
            "id": 1,
            "module": "telegram:WatchUpdates",
            "version": 1,
            "parameters": {
                "__IMTHOOK__": 2832280
            },
            "mapper": {},
            "metadata": {
                "designer": {
                    "x": -116,
                    "y": 76
                },
                "setupValidation": {
                    "version": 1,
                    "configuration": "87067616365b7a48",
                    "result": {
                        "valid": true,
                        "fields": []
                    }
                },
                "restore": {
                    "parameters": {
                        "__IMTHOOK__": {
                            "label": "My Telegram Bot Updates webhook",
                            "data": {
                                "editable": "false"
                            }
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
                    "x": 257,
                    "y": -150
                }
            },
            "routes": [
                {
                    "flow": [
                        {
                            "id": 3,
                            "module": "telegram:DownloadFile",
                            "version": 1,
                            "parameters": {
                                "__IMTCONN__": 11185122
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
                                "fileId": "{{1.message.photo[3].file_id}}"
                            },
                            "metadata": {
                                "designer": {
                                    "x": 598,
                                    "y": 316
                                },
                                "setupValidation": {
                                    "version": 1,
                                    "configuration": "f3d3d816f3ccedb0",
                                    "result": {
                                        "valid": true,
                                        "fields": []
                                    }
                                },
                                "restore": {
                                    "parameters": {
                                        "__IMTCONN__": {
                                            "label": "Laura's Telegram Bot connection",
                                            "data": {
                                                "scoped": "true",
                                                "connection": "telegram"
                                            }
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
                                "makeConnectionId": 11185169
                            },
                            "mapper": {
                                "defaultModel": "medium",
                                "tokenLimit": "50",
                                "promptCaching": "none",
                                "fallbackEnabled": false,
                                "systemPrompt": "Eres un asistente educativo que identifica organismos en fotos tomadas \r\npor estudiantes en el jardín del Tecnológico, para la materia de \r\nDesarrollo Sustentable, tema \"El Ecosistema\". \r\nCuando recibas una imagen, responde SIEMPRE en este formato, sin texto \r\nadicional antes o después:\r\n� [nombre probable del organismo] \r\n�� [Productor / Consumidor / Descomponedor] \r\n♻️ [rol en el ecosistema en máximo 15 palabras] \r\nSi la imagen no muestra un organismo vivo, responde únicamente: \r\n\"❌ No identifico un organismo. Intenta con una planta, insecto u otro \r\nser vivo.\" \r\nReglas estrictas: \r\n- Máximo 35 palabras en total. \r\n- Sin introducciones, sin despedidas, sin explicaciones extra. \r\n- Responde siempre en español\r\n",
                                "message": "Analiza la imagen adjunta siguiendo tus instrucciones",
                                "files": [
                                    {
                                        "fileName": "{{3.fileName}}",
                                        "data": "{{3.fileOutput}}"
                                    }
                                ],
                                "threadId": "",
                                "modelConfig": {
                                    "recursionLimit": "300",
                                    "iterationsFromHistoryCount": "10",
                                    "timeout": ""
                                },
                                "outputType": "text"
                            },
                            "metadata": {
                                "designer": {
                                    "x": 782,
                                    "y": -148
                                },
                                "setupValidation": {
                                    "version": 1,
                                    "configuration": "972d858e6ae25254",
                                    "result": {
                                        "valid": true,
                                        "fields": []
                                    }
                                },
                                "restore": {
                                    "parameters": {
                                        "makeConnectionId": {
                                            "label": "Laura's Make's AI Provider connection",
                                            "data": {
                                                "scoped": "true",
                                                "connection": "ai-provider"
                                            }
                                        }
                                    },
                                    "expect": {
                                        "defaultModel": {
                                            "mode": "chose",
                                            "label": "MediumModel: gpt-5-nano. Reasoning: low. A balanced, quick choice for clearly defined tasks needing reliable answers rather than deep analysis"
                                        },
                                        "promptCaching": {
                                            "label": "Automatic (always on)"
                                        },
                                        "files": {
                                            "mode": "chose",
                                            "items": [
                                                null
                                            ]
                                        },
                                        "outputType": {
                                            "label": "Text"
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
                                            "min": 20,
                                            "max": 100
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
                                        "type": "array",
                                        "label": "Input files",
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
                                        ]
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
                                        "type": "collection",
                                        "label": "Model configuration",
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
                                                    "min": 120,
                                                    "max": 600
                                                }
                                            }
                                        ]
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
                            "id": 7,
                            "module": "telegram:SendReplyMessage",
                            "version": 1,
                            "parameters": {
                                "__IMTCONN__": 11185237
                            },
                            "mapper": {
                                "chatId": "{{1.message.chat.id}}",
                                "text": "{{{5.response}}} (respuesta del AI Agent)",
                                "messageThreadId": "",
                                "parseMode": "",
                                "replyToMessageId": "",
                                "replyMarkupAssembleType": "reply_markup_enter",
                                "replyMarkup": ""
                            },
                            "metadata": {
                                "designer": {
                                    "x": 1041,
                                    "y": 299
                                },
                                "setupValidation": {
                                    "version": 1,
                                    "configuration": "66f83e2cf3d6a606",
                                    "result": {
                                        "valid": true,
                                        "fields": []
                                    }
                                },
                                "restore": {
                                    "parameters": {
                                        "__IMTCONN__": {
                                            "label": "Laura's Telegram Bot connection",
                                            "data": {
                                                "scoped": "true",
                                                "connection": "telegram"
                                            }
                                        }
                                    },
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
                            "module": "telegram:SendReplyMessage",
                            "version": 1,
                            "parameters": {
                                "__IMTCONN__": 10629386
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
                                "chatId": "{{1.message.chat.id}}",
                                "text": "Envíame una foto del organismo (planta, insecto, hongo, etc.) para poder identificarlo.",
                                "messageThreadId": "",
                                "parseMode": "",
                                "replyToMessageId": "",
                                "replyMarkupAssembleType": "reply_markup_enter",
                                "replyMarkup": ""
                            },
                            "metadata": {
                                "designer": {
                                    "x": 204,
                                    "y": 346
                                },
                                "setupValidation": {
                                    "version": 1,
                                    "configuration": "9670e8eca4b8dafd",
                                    "result": {
                                        "valid": true,
                                        "fields": []
                                    }
                                },
                                "restore": {
                                    "parameters": {
                                        "__IMTCONN__": {
                                            "label": "Laura's Telegram Bot connection",
                                            "data": {
                                                "scoped": "true",
                                                "connection": "telegram"
                                            }
                                        }
                                    },
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

{
    "name": "noticias climaticas del dia#",
    "flow": [
        {
            "id": 1,
            "module": "gateway:CustomWebHook",
            "version": 1,
            "parameters": {
                "hook": 3004547,
                "maxResults": 1
            },
            "mapper": {},
            "metadata": {
                "designer": {
                    "x": 0,
                    "y": 0
                },
                "setupValidation": {
                    "version": 1,
                    "configuration": "bb20054e52c726d8",
                    "result": {
                        "valid": true,
                        "fields": []
                    }
                },
                "restore": {
                    "parameters": {
                        "hook": {
                            "label": "noticias",
                            "data": {
                                "editable": "true"
                            }
                        }
                    }
                },
                "parameters": [
                    {
                        "name": "hook",
                        "type": "hook:gateway-webhook",
                        "label": "Webhook",
                        "required": true
                    },
                    {
                        "name": "maxResults",
                        "type": "number",
                        "label": "Maximum number of results"
                    }
                ]
            }
        },
        {
            "id": 2,
            "module": "rss:ActionReadArticles",
            "version": 4,
            "parameters": {
                "include": []
            },
            "mapper": {
                "url": "https://news.google.com/rss/search?q={{{{encodeURL(\"1.tema\")}}}}&hl=es-419&gl=MX&ceid=MX:es-419",
                "username": "",
                "password": "",
                "filterDateFrom": "",
                "filterDateTo": "",
                "maxResults": "5",
                "gzip": true
            },
            "metadata": {
                "designer": {
                    "x": 300,
                    "y": 0
                },
                "setupValidation": {
                    "version": 1,
                    "configuration": "b70b6cfe3ff04349",
                    "result": {
                        "valid": true,
                        "fields": []
                    }
                },
                "restore": {},
                "parameters": [
                    {
                        "name": "include",
                        "type": "select",
                        "label": "Process RSS fields",
                        "multiple": true,
                        "validate": {
                            "enum": [
                                "google-merchant-center",
                                "itunes"
                            ]
                        }
                    }
                ],
                "expect": [
                    {
                        "name": "url",
                        "type": "url",
                        "label": "URL",
                        "required": true
                    },
                    {
                        "name": "username",
                        "type": "text",
                        "label": "User name"
                    },
                    {
                        "name": "password",
                        "type": "password",
                        "label": "Password"
                    },
                    {
                        "name": "filterDateFrom",
                        "type": "date",
                        "label": "Date from"
                    },
                    {
                        "name": "filterDateTo",
                        "type": "date",
                        "label": "Date to "
                    },
                    {
                        "name": "maxResults",
                        "type": "number",
                        "label": "Maximum number of returned items",
                        "required": true
                    },
                    {
                        "name": "gzip",
                        "type": "boolean",
                        "label": "Request compressed content",
                        "required": true
                    }
                ],
                "interface": [
                    {
                        "name": "title",
                        "type": "text",
                        "label": "Title"
                    },
                    {
                        "name": "description",
                        "type": "text",
                        "label": "Description"
                    },
                    {
                        "name": "summary",
                        "type": "text",
                        "label": "Summary"
                    },
                    {
                        "name": "author",
                        "type": "text",
                        "label": "Author"
                    },
                    {
                        "name": "url",
                        "type": "url",
                        "label": "URL"
                    },
                    {
                        "name": "dateUpdated",
                        "type": "date",
                        "label": "Date updated"
                    },
                    {
                        "name": "dateCreated",
                        "type": "date",
                        "label": "Date created"
                    },
                    {
                        "name": "comments",
                        "type": "url",
                        "label": "Comments"
                    },
                    {
                        "name": "image",
                        "type": "collection",
                        "label": "Image",
                        "spec": [
                            {
                                "name": "title",
                                "label": "Name",
                                "type": "text"
                            },
                            {
                                "name": "url",
                                "label": "URL",
                                "type": "url"
                            }
                        ]
                    },
                    {
                        "name": "categories",
                        "type": "array",
                        "label": "Categories",
                        "spec": {
                            "type": "text"
                        }
                    },
                    {
                        "name": "source",
                        "type": "collection",
                        "label": "Source",
                        "spec": [
                            {
                                "name": "title",
                                "label": "Name",
                                "type": "text"
                            },
                            {
                                "name": "url",
                                "label": "URL",
                                "type": "url"
                            }
                        ]
                    },
                    {
                        "name": "enclosures",
                        "type": "array",
                        "label": "Enclosures",
                        "spec": [
                            {
                                "name": "url",
                                "label": "URL",
                                "type": "url"
                            },
                            {
                                "name": "type",
                                "label": "Type",
                                "type": "text"
                            },
                            {
                                "name": "length",
                                "label": "Length",
                                "type": "number"
                            }
                        ]
                    },
                    {
                        "name": "rssFields",
                        "label": "RSS fields",
                        "help": "Other RSS fields. All values are in text format.",
                        "type": "collection",
                        "spec": [
                            {
                                "name": "title",
                                "label": "title",
                                "type": "text"
                            },
                            {
                                "name": "link",
                                "label": "link",
                                "type": "text"
                            },
                            {
                                "name": "guid",
                                "label": "guid",
                                "type": "text"
                            },
                            {
                                "name": "pubdate",
                                "label": "pubdate",
                                "type": "text"
                            },
                            {
                                "name": "description",
                                "label": "description",
                                "type": "text"
                            },
                            {
                                "name": "source",
                                "label": "source",
                                "type": "text"
                            }
                        ]
                    }
                ]
            }
        },
        {
            "id": 3,
            "module": "util:TextAggregator",
            "version": 1,
            "parameters": {
                "rowSeparator": "",
                "feeder": 2
            },
            "mapper": {
                "value": "Título: {{2.title}}\r\nFecha: {{2.dateCreated}}\r\nEnlace: {{2.url}}"
            },
            "metadata": {
                "designer": {
                    "x": 600,
                    "y": 0
                },
                "setupValidation": {
                    "version": 1,
                    "configuration": "d405130050a9a630",
                    "result": {
                        "valid": true,
                        "fields": []
                    }
                },
                "restore": {
                    "parameters": {
                        "rowSeparator": {
                            "label": "Empty"
                        }
                    },
                    "extra": {
                        "feeder": {
                            "label": "RSS - Retrieve RSS feed items [2]"
                        }
                    }
                },
                "parameters": [
                    {
                        "name": "rowSeparator",
                        "type": "select",
                        "label": "Row separator",
                        "validate": {
                            "enum": [
                                "\n",
                                "\t",
                                "other"
                            ]
                        }
                    }
                ],
                "expect": [
                    {
                        "name": "value",
                        "type": "text",
                        "label": "Text"
                    }
                ]
            }
        },
        {
            "id": 4,
            "module": "ai-local-agent:RunLocalAIAgent",
            "version": 0,
            "parameters": {
                "makeConnectionId": 10593897
            },
            "mapper": {
                "defaultModel": "medium",
                "tokenLimit": "50",
                "promptCaching": "none",
                "fallbackEnabled": false,
                "systemPrompt": "Eres un divulgador ambiental para alumnos de Desarrollo Sustentable del TecNM.\r\nRecibirás un tema y una lista de noticias recientes (título, fecha y enlace).\r\nUsa ÚNICAMENTE la información de esas noticias; no inventes datos ni agregues\r\nnoticias que no estén en la lista.\r\nResponde en texto plano (sin asteriscos, sin markdown), en español, con este formato:\r\nRESUMEN DEL DÍA\r\n[3 a 4 líneas explicando de qué tratan las noticias en conjunto]\r\nNOTICIAS\r\n1. [título] - [1 línea explicando por qué importa]\r\n[enlace]\r\n(repite para cada noticia)\r\n¿QUÉ PUEDO HACER YO?\r\n[1 acción concreta que un estudiante puede hacer relacionada con el tema]\r\nSi la lista de noticias viene vacía, responde: &quot;No se encontraron noticias recientes\r\nsobre este tema.&quot;",
                "message": "Tema: {{1.tema}}\r\nNoticias:\r\n{{3.text}}",
                "files": [],
                "threadId": "",
                "modelConfig": {
                    "recursionLimit": "300",
                    "iterationsFromHistoryCount": "10",
                    "timeout": "",
                    "aiCompactionEnabled": true
                },
                "outputType": "text"
            },
            "metadata": {
                "designer": {
                    "x": 900,
                    "y": 0
                },
                "setupValidation": {
                    "version": 1,
                    "configuration": "a7ea652c50536729",
                    "result": {
                        "valid": true,
                        "fields": []
                    }
                },
                "restore": {
                    "parameters": {
                        "makeConnectionId": {
                            "label": "Make's AI Provider (default)",
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
                            "mode": "chose"
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
                            },
                            {
                                "name": "aiCompactionEnabled",
                                "type": "boolean",
                                "label": "Enable compaction",
                                "required": true
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
            "id": 5,
            "module": "gateway:WebhookRespond",
            "version": 1,
            "parameters": {},
            "mapper": {
                "status": "200",
                "body": "{{4.response}}",
                "headers": [
                    {
                        "key": "Content-Type = text/plain; charset=utf-8",
                        "value": "Access-Control-Allow-Origin = *"
                    }
                ]
            },
            "metadata": {
                "designer": {
                    "x": 1200,
                    "y": 0
                },
                "setupValidation": {
                    "version": 1,
                    "configuration": "340c302c76c6f9f6",
                    "result": {
                        "valid": true,
                        "fields": []
                    }
                },
                "restore": {
                    "expect": {
                        "headers": {
                            "mode": "chose",
                            "items": [
                                null
                            ]
                        }
                    }
                },
                "expect": [
                    {
                        "name": "status",
                        "type": "uinteger",
                        "label": "Status",
                        "validate": {
                            "min": 100
                        },
                        "required": true
                    },
                    {
                        "name": "body",
                        "type": "any",
                        "label": "Body"
                    },
                    {
                        "name": "headers",
                        "type": "array",
                        "label": "Custom headers",
                        "validate": {
                            "maxItems": 16
                        },
                        "spec": [
                            {
                                "name": "key",
                                "label": "Key",
                                "type": "text",
                                "required": true,
                                "validate": {
                                    "max": 256
                                }
                            },
                            {
                                "name": "value",
                                "label": "Value",
                                "type": "text",
                                "required": true,
                                "validate": {
                                    "max": 4096
                                }
                            }
                        ]
                    }
                ],
                "advanced": true
            }
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

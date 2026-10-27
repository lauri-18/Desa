{
    "name": "IDH_Estados_Equipo",
    "flow": [
        {
            "id": 1,
            "module": "gateway:CustomWebHook",
            "version": 1,
            "parameters": {
                "hook": 2985728,
                "maxResults": 1
            },
            "mapper": {},
            "metadata": {
                "designer": {
                    "x": 0,
                    "y": 0
                },
                "setupValidation": {
                    "result": {
                        "valid": true,
                        "fields": []
                    },
                    "version": 1,
                    "configuration": "4c203ace97a47b53"
                },
                "restore": {
                    "parameters": {
                        "hook": {
                            "data": {
                                "editable": "true"
                            },
                            "label": "IDH_webhook"
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
            "id": 3,
            "module": "ai-local-agent:RunLocalAIAgent",
            "version": 0,
            "parameters": {
                "makeConnectionId": 10593897
            },
            "mapper": {
                "files": [],
                "message": "Entidad: {{1.entidad}} (mapear el campo desde el panel)",
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
                "systemPrompt": "Eres un analista de desarrollo humano para alumnos de Desarrollo Sustentable del\r\nTecNM.\r\nResponde ÚNICAMENTE con los datos del archivo de conocimiento sobre el IDH por\r\nentidad federativa de México. No inventes cifras.\r\nCuando recibas el nombre de una entidad, responde en texto plano (sin asteriscos, sin\r\nmarkdown) con este formato:\r\n\r\nIDH: [valor] - Nivel [muy alto/alto/medio]\r\nSalud: [valor]\r\nEducación: [valor]\r\nIngreso: [valor]\r\nLugar nacional: [posición] de 32\r\nAño de los datos: [año]\r\nInterpretación: [3 líneas máximo: en qué destaca, dónde tiene rezago y qué implica\r\npara su desarrollo sustentable]\r\nSi la entidad no aparece en el archivo, responde: &quot;No encontré datos de esa entidad\r\nen el documento.&quot;",
                "promptCaching": "none",
                "fallbackEnabled": false
            },
            "metadata": {
                "designer": {
                    "x": 303,
                    "y": -12
                },
                "setupValidation": {
                    "result": {
                        "valid": true,
                        "fields": []
                    },
                    "version": 1,
                    "configuration": "ff6f528f6d5e38cc"
                },
                "restore": {
                    "expect": {
                        "files": {
                            "mode": "chose"
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
                            "label": "Make's AI Provider (default)"
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
            "tools": [
                {
                    "name": "Agent knowledge",
                    "description": "Search uploaded files using semantic similarity to retrieve relevant facts and context needed to answer the user’s question. Use this tool when the answer depends on information contained in the uploaded documents.",
                    "flow": [
                        {
                            "id": 5,
                            "module": "knowledge:KnowledgeStandAlone",
                            "version": 1,
                            "parameters": {},
                            "mapper": {
                                "limit": "50",
                                "query": "{{3.query}}",
                                "fileIds": [],
                                "filestorage": [
                                    "976ed8a6-f576-4a67-a724-a12e1919df61"
                                ]
                            },
                            "metadata": {
                                "designer": {
                                    "x": 603,
                                    "y": 238
                                },
                                "setupValidation": {
                                    "result": {
                                        "valid": true,
                                        "fields": []
                                    },
                                    "version": 1,
                                    "configuration": "2ea54801fdb4962c"
                                },
                                "restore": {
                                    "expect": {
                                        "query": {
                                            "extra": {
                                                "aiHelp": "A concise natural-language description of the information to look for. The query is embedded and matched by semantic similarity (cosine distance), so it should express intent and meaning, not exact phrasing, keywords, or technical instructions."
                                            }
                                        }
                                    }
                                },
                                "expect": [
                                    {
                                        "name": "filestorage",
                                        "type": "filestorage",
                                        "label": "Knowledge files"
                                    },
                                    {
                                        "name": "query",
                                        "type": "text",
                                        "label": "Search query",
                                        "required": true
                                    },
                                    {
                                        "name": "fileIds",
                                        "type": "hidden",
                                        "required": true
                                    },
                                    {
                                        "name": "limit",
                                        "type": "number",
                                        "label": "Limit",
                                        "required": true,
                                        "validate": {
                                            "max": 100,
                                            "min": 1
                                        }
                                    }
                                ]
                            }
                        }
                    ]
                }
            ]
        },
        {
            "id": 6,
            "module": "gateway:WebhookRespond",
            "version": 1,
            "parameters": {},
            "mapper": {
                "body": "{{3.response}}",
                "status": "200",
                "headers": []
            },
            "metadata": {
                "designer": {
                    "x": 603,
                    "y": -12
                },
                "setupValidation": {
                    "result": {
                        "valid": true,
                        "fields": []
                    },
                    "version": 1,
                    "configuration": "be2e680b0aa2684f"
                },
                "restore": {
                    "expect": {
                        "headers": {
                            "mode": "chose"
                        }
                    }
                },
                "expect": [
                    {
                        "name": "status",
                        "type": "uinteger",
                        "label": "Status",
                        "required": true,
                        "validate": {
                            "min": 100
                        }
                    },
                    {
                        "name": "body",
                        "type": "any",
                        "label": "Body"
                    },
                    {
                        "name": "headers",
                        "spec": [
                            {
                                "name": "key",
                                "type": "text",
                                "label": "Key",
                                "required": true,
                                "validate": {
                                    "max": 256
                                }
                            },
                            {
                                "name": "value",
                                "type": "text",
                                "label": "Value",
                                "required": true,
                                "validate": {
                                    "max": 4096
                                }
                            }
                        ],
                        "type": "array",
                        "label": "Custom headers",
                        "validate": {
                            "maxItems": 16
                        }
                    }
                ]
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

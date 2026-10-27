{
    "name": "buzon_ciudadano_equipo#",
    "flow": [
        {
            "id": 1,
            "module": "telegram:WatchUpdates",
            "version": 1,
            "parameters": {
                "__IMTHOOK__": 2984837
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
                    "configuration": "b897979e778f389d"
                },
                "restore": {
                    "parameters": {
                        "__IMTHOOK__": {
                            "data": {
                                "editable": "false"
                            },
                            "label": "My Telegram Bot Updates webhook"
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
            "id": 3,
            "module": "util:SetVariable2",
            "version": 1,
            "parameters": {},
            "mapper": {
                "name": "folio",
                "value": "AMB-{{formatDate(now; \"YYMMDD-HHmmss\")}}"
            },
            "metadata": {
                "designer": {
                    "x": 300,
                    "y": 0
                },
                "setupValidation": {
                    "result": {
                        "valid": true,
                        "fields": []
                    },
                    "version": 1,
                    "configuration": "94de4c46a268e272"
                },
                "restore": {},
                "expect": [
                    {
                        "name": "name",
                        "type": "text",
                        "label": "Variable name",
                        "required": true
                    },
                    {
                        "name": "value",
                        "type": "any",
                        "label": "Variable value"
                    }
                ],
                "interface": [
                    {
                        "name": "folio",
                        "type": "any",
                        "label": "folio"
                    }
                ]
            }
        },
        {
            "id": 4,
            "module": "google-sheets:addRow",
            "version": 2,
            "parameters": {
                "__IMTCONN__": 11961949
            },
            "mapper": {
                "from": "drive",
                "mode": "select",
                "values": {
                    "Fecha": "{{formatDate(now; quot; DD / MM / YYYY + HH:mm & quot; )}}",
                    "Folio": "{{3.folio}}",
                    "Nombre": "{{1.message.from.first_name}}",
                    "Estatus": "Recibido",
                    "Reporte": "{{1.message.text}}",
                    "Usuario": "{{1.message.from.username}}"
                },
                "sheetId": "Reportes",
                "spreadsheetId": "/19pGR73AAdz5pTl3wpqW1pCFQ2_gZtDoOzP0yHh1g8WU",
                "includesHeaders": true,
                "insertDataOption": "INSERT_ROWS",
                "useColumnHeaders": true,
                "valueInputOption": "USER_ENTERED",
                "insertUnformatted": false
            },
            "metadata": {
                "designer": {
                    "x": 600,
                    "y": 0
                },
                "setupValidation": {
                    "result": {
                        "valid": true,
                        "fields": []
                    },
                    "version": 1,
                    "configuration": "d8cf2a9df614c631"
                },
                "restore": {
                    "expect": {
                        "from": {
                            "label": "My Drive"
                        },
                        "mode": {
                            "label": "Search by path"
                        },
                        "sheetId": {
                            "label": "Reportes"
                        },
                        "spreadsheetId": {
                            "path": [
                                "buzon_ciudadano_equipo#"
                            ]
                        },
                        "includesHeaders": {
                            "label": "Yes"
                        },
                        "insertDataOption": {
                            "mode": "chose",
                            "label": "Insert rows"
                        },
                        "useColumnHeaders": {
                            "label": "Yes"
                        },
                        "valueInputOption": {
                            "mode": "chose",
                            "label": "User entered"
                        },
                        "insertUnformatted": {
                            "mode": "chose"
                        }
                    },
                    "parameters": {
                        "__IMTCONN__": {
                            "data": {
                                "scoped": "true",
                                "connection": "google"
                            },
                            "label": "Laura's Google connection (laurapatriciavazquezvilla@gmail.com)"
                        }
                    }
                },
                "parameters": [
                    {
                        "name": "__IMTCONN__",
                        "type": "account:google",
                        "label": "Connection",
                        "required": true
                    }
                ],
                "expect": [
                    {
                        "name": "mode",
                        "type": "select",
                        "label": "Search Method",
                        "required": true,
                        "validate": {
                            "enum": [
                                "select",
                                "fromAll",
                                "map"
                            ]
                        }
                    },
                    {
                        "name": "insertUnformatted",
                        "type": "boolean",
                        "label": "Unformatted",
                        "required": true
                    },
                    {
                        "name": "valueInputOption",
                        "type": "select",
                        "label": "Value input option",
                        "required": true,
                        "validate": {
                            "enum": [
                                "USER_ENTERED",
                                "RAW"
                            ]
                        }
                    },
                    {
                        "name": "insertDataOption",
                        "type": "select",
                        "label": "Insert data option",
                        "validate": {
                            "enum": [
                                "INSERT_ROWS",
                                "OVERWRITE"
                            ]
                        }
                    },
                    {
                        "name": "from",
                        "type": "select",
                        "label": "Drive",
                        "required": true,
                        "validate": {
                            "enum": [
                                "drive",
                                "share",
                                "team"
                            ]
                        }
                    },
                    {
                        "name": "spreadsheetId",
                        "type": "file",
                        "label": "Spreadsheet Name",
                        "required": true
                    },
                    {
                        "name": "sheetId",
                        "type": "select",
                        "label": "Sheet Name",
                        "required": true
                    },
                    {
                        "name": "includesHeaders",
                        "type": "select",
                        "label": "Table contains headers",
                        "required": true,
                        "validate": {
                            "enum": [
                                true,
                                false
                            ]
                        }
                    },
                    {
                        "name": "useColumnHeaders",
                        "type": "select",
                        "label": "Use column headers as IDs of the columns",
                        "required": true,
                        "validate": {
                            "enum": [
                                true,
                                false
                            ]
                        }
                    },
                    {
                        "name": "values",
                        "spec": [
                            {
                                "name": "Folio",
                                "type": "text",
                                "label": "Folio (A)"
                            },
                            {
                                "name": "Fecha",
                                "type": "text",
                                "label": "Fecha (B)"
                            },
                            {
                                "name": "Usuario",
                                "type": "text",
                                "label": "Usuario (C)"
                            },
                            {
                                "name": "Nombre",
                                "type": "text",
                                "label": "Nombre (D)"
                            },
                            {
                                "name": "Reporte",
                                "type": "text",
                                "label": "Reporte (E)"
                            },
                            {
                                "name": "Estatus",
                                "type": "text",
                                "label": "Estatus (F)"
                            }
                        ],
                        "type": "collection",
                        "label": "Values in columns",
                        "metadata": [
                            [
                                [
                                    "Folio",
                                    "Fecha",
                                    "Usuario",
                                    "Nombre",
                                    "Reporte",
                                    "Estatus"
                                ]
                            ]
                        ]
                    }
                ]
            }
        },
        {
            "id": 5,
            "module": "telegram:SendReplyMessage",
            "version": 1,
            "parameters": {
                "__IMTCONN__": 11962958
            },
            "mapper": {
                "text": "Reporte recibido.\r\nTu folio es: {{3.folio}}\r\nEstatus: Recibido\r\nGuarda este número para dar seguimiento a tu reporte.",
                "chatId": "{{1.message.chat.id}}",
                "parseMode": "",
                "replyMarkup": "",
                "messageThreadId": "",
                "replyToMessageId": "",
                "replyMarkupAssembleType": "reply_markup_enter"
            },
            "metadata": {
                "designer": {
                    "x": 900,
                    "y": 0
                },
                "setupValidation": {
                    "result": {
                        "valid": true,
                        "fields": []
                    },
                    "version": 1,
                    "configuration": "657e66cb4849637a"
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

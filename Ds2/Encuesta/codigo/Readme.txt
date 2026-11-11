{
    "name": "Encuesta_equipo#",
    "flow": [
        {
            "id": 1,
            "module": "gateway:CustomWebHook",
            "version": 1,
            "parameters": {
                "hook": 3047698,
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
                    "configuration": "5700946564011c4a"
                },
                "restore": {
                    "parameters": {
                        "hook": {
                            "data": {
                                "editable": "true"
                            },
                            "label": "encuesta"
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
            "module": "builtin:BasicRouter",
            "version": 1,
            "mapper": null,
            "metadata": {
                "designer": {
                    "x": 300,
                    "y": 0
                }
            },
            "routes": [
                {
                    "flow": [
                        {
                            "id": 3,
                            "module": "google-sheets:addRow",
                            "version": 2,
                            "parameters": {
                                "__IMTCONN__": 12258905
                            },
                            "filter": {
                                "name": "guardar respuesta",
                                "conditions": [
                                    [
                                        {
                                            "a": "{{1.accion}}",
                                            "b": "respuesta",
                                            "o": "text:equal"
                                        }
                                    ]
                                ]
                            },
                            "mapper": {
                                "from": "drive",
                                "mode": "select",
                                "values": {
                                    "0": "{{formatDate(now; \"DD/MM/YYYY HH:mm\")}}",
                                    "1": "{{1.comida}}",
                                    "2": "{{1.ropa}}",
                                    "3": "{{1.apps}}",
                                    "4": "{{1.criterio}}",
                                    "5": "{{1.origen}}",
                                    "6": "{{1.edad}}"
                                },
                                "sheetId": "Respuestas",
                                "spreadsheetId": "/1GAnWDOJRZTvP-GzqkWQBfxW9jlYPaZ9Ilz3n0dThDUw",
                                "includesHeaders": true,
                                "insertDataOption": "INSERT_ROWS",
                                "useColumnHeaders": false,
                                "valueInputOption": "USER_ENTERED",
                                "insertUnformatted": false
                            },
                            "metadata": {
                                "designer": {
                                    "x": 600,
                                    "y": -150
                                },
                                "setupValidation": {
                                    "result": {
                                        "valid": true,
                                        "fields": []
                                    },
                                    "version": 1,
                                    "configuration": "ab2206bac9916524"
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
                                            "label": "Respuestas"
                                        },
                                        "spreadsheetId": {
                                            "path": [
                                                "Encuesta_Equipo#"
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
                                            "label": "No"
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
                                            "label": "Laura's Google connection"
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
                                                "name": "0",
                                                "type": "text",
                                                "label": "fecha (A)"
                                            },
                                            {
                                                "name": "1",
                                                "type": "text",
                                                "label": "comida (B)"
                                            },
                                            {
                                                "name": "2",
                                                "type": "text",
                                                "label": "ropa (C)"
                                            },
                                            {
                                                "name": "3",
                                                "type": "text",
                                                "label": "apps (D)"
                                            },
                                            {
                                                "name": "4",
                                                "type": "text",
                                                "label": "criterios (E)"
                                            },
                                            {
                                                "name": "5",
                                                "type": "text",
                                                "label": "origen  (F)"
                                            },
                                            {
                                                "name": "6",
                                                "type": "text",
                                                "label": "edad (G)"
                                            },
                                            {
                                                "name": "7",
                                                "type": "text",
                                                "label": "(H)"
                                            },
                                            {
                                                "name": "8",
                                                "type": "text",
                                                "label": "(I)"
                                            },
                                            {
                                                "name": "9",
                                                "type": "text",
                                                "label": "(J)"
                                            },
                                            {
                                                "name": "10",
                                                "type": "text",
                                                "label": "(K)"
                                            },
                                            {
                                                "name": "11",
                                                "type": "text",
                                                "label": "(L)"
                                            },
                                            {
                                                "name": "12",
                                                "type": "text",
                                                "label": "(M)"
                                            },
                                            {
                                                "name": "13",
                                                "type": "text",
                                                "label": "(N)"
                                            },
                                            {
                                                "name": "14",
                                                "type": "text",
                                                "label": "(O)"
                                            },
                                            {
                                                "name": "15",
                                                "type": "text",
                                                "label": "(P)"
                                            },
                                            {
                                                "name": "16",
                                                "type": "text",
                                                "label": "(Q)"
                                            },
                                            {
                                                "name": "17",
                                                "type": "text",
                                                "label": "(R)"
                                            },
                                            {
                                                "name": "18",
                                                "type": "text",
                                                "label": "(S)"
                                            },
                                            {
                                                "name": "19",
                                                "type": "text",
                                                "label": "(T)"
                                            },
                                            {
                                                "name": "20",
                                                "type": "text",
                                                "label": "(U)"
                                            },
                                            {
                                                "name": "21",
                                                "type": "text",
                                                "label": "(V)"
                                            },
                                            {
                                                "name": "22",
                                                "type": "text",
                                                "label": "(W)"
                                            },
                                            {
                                                "name": "23",
                                                "type": "text",
                                                "label": "(X)"
                                            },
                                            {
                                                "name": "24",
                                                "type": "text",
                                                "label": "(Y)"
                                            },
                                            {
                                                "name": "25",
                                                "type": "text",
                                                "label": "(Z)"
                                            }
                                        ],
                                        "type": "collection",
                                        "label": "Values in columns",
                                        "metadata": [
                                            [
                                                [
                                                    "fecha",
                                                    "comida",
                                                    "ropa",
                                                    "apps",
                                                    "criterios",
                                                    "origen ",
                                                    "edad"
                                                ]
                                            ]
                                        ]
                                    }
                                ]
                            }
                        },
                        {
                            "id": 5,
                            "module": "gateway:WebhookRespond",
                            "version": 1,
                            "parameters": {},
                            "mapper": {
                                "body": "respuesta registrada",
                                "status": "200",
                                "headers": [
                                    {
                                        "key": "Content-Type",
                                        "value": "text/plain; charset=utf-8"
                                    },
                                    {
                                        "key": "Access-Control-Allow-Origin",
                                        "value": "*"
                                    }
                                ]
                            },
                            "metadata": {
                                "designer": {
                                    "x": 900,
                                    "y": -150
                                },
                                "setupValidation": {
                                    "result": {
                                        "valid": true,
                                        "fields": []
                                    },
                                    "version": 1,
                                    "configuration": "793ccb261a1b761c"
                                },
                                "restore": {
                                    "expect": {
                                        "headers": {
                                            "mode": "chose",
                                            "items": [
                                                null,
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
                                ],
                                "advanced": true
                            }
                        }
                    ]
                },
                {
                    "flow": [
                        {
                            "id": 4,
                            "module": "google-sheets:filterRows",
                            "version": 2,
                            "parameters": {
                                "__IMTCONN__": 12259016
                            },
                            "filter": {
                                "name": "generar reporte",
                                "conditions": [
                                    [
                                        {
                                            "a": "{{1.accion}}",
                                            "b": "reporte",
                                            "o": "text:equal"
                                        }
                                    ]
                                ]
                            },
                            "mapper": {
                                "from": "drive",
                                "sheetId": "Respuestas",
                                "sortOrder": "asc",
                                "spreadsheetId": "1GAnWDOJRZTvP-GzqkWQBfxW9jlYPaZ9Ilz3n0dThDUw",
                                "tableFirstRow": "A1:CZ1",
                                "includesHeaders": true,
                                "valueRenderOption": "FORMATTED_VALUE",
                                "dateTimeRenderOption": "FORMATTED_STRING"
                            },
                            "metadata": {
                                "designer": {
                                    "x": 600,
                                    "y": 150
                                },
                                "setupValidation": {
                                    "result": {
                                        "valid": true,
                                        "fields": []
                                    },
                                    "version": 1,
                                    "configuration": "ccc606583da68ab3"
                                },
                                "restore": {
                                    "expect": {
                                        "from": {
                                            "label": "Select from My Drive"
                                        },
                                        "orderBy": {
                                            "mode": "chose"
                                        },
                                        "sheetId": {
                                            "mode": "chose",
                                            "label": "Respuestas"
                                        },
                                        "sortOrder": {
                                            "mode": "chose",
                                            "label": "Ascending"
                                        },
                                        "spreadsheetId": {
                                            "mode": "chose",
                                            "label": "Encuesta_Equipo#"
                                        },
                                        "tableFirstRow": {
                                            "label": "A-CZ"
                                        },
                                        "includesHeaders": {
                                            "mode": "chose",
                                            "label": "Yes"
                                        },
                                        "valueRenderOption": {
                                            "mode": "chose",
                                            "label": "Formatted value"
                                        },
                                        "dateTimeRenderOption": {
                                            "mode": "chose",
                                            "label": "Formatted string"
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
                                        "name": "from",
                                        "type": "select",
                                        "label": "Search Method",
                                        "required": true,
                                        "validate": {
                                            "enum": [
                                                "drive",
                                                "share"
                                            ]
                                        }
                                    },
                                    {
                                        "name": "valueRenderOption",
                                        "type": "select",
                                        "label": "Value render option",
                                        "validate": {
                                            "enum": [
                                                "FORMATTED_VALUE",
                                                "UNFORMATTED_VALUE",
                                                "FORMULA"
                                            ]
                                        }
                                    },
                                    {
                                        "name": "dateTimeRenderOption",
                                        "type": "select",
                                        "label": "Date and time render option",
                                        "validate": {
                                            "enum": [
                                                "SERIAL_NUMBER",
                                                "FORMATTED_STRING"
                                            ]
                                        }
                                    },
                                    {
                                        "name": "limit",
                                        "type": "uinteger",
                                        "label": "Limit"
                                    },
                                    {
                                        "name": "spreadsheetId",
                                        "type": "select",
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
                                        "name": "tableFirstRow",
                                        "type": "select",
                                        "label": "Column range",
                                        "required": true,
                                        "validate": {
                                            "enum": [
                                                "A1:Z1",
                                                "A1:BZ1",
                                                "A1:CZ1",
                                                "A1:DZ1",
                                                "A1:MZ1",
                                                "A1:ZZ1",
                                                "A1:AZZ1",
                                                "A1:BZZ1",
                                                "A1:CZZ1",
                                                "A1:DZZ1",
                                                "A1:MZZ1",
                                                "A1:ZZZ1"
                                            ]
                                        }
                                    },
                                    {
                                        "name": "filter",
                                        "type": "filter",
                                        "label": "Filter",
                                        "options": "rpc://google-sheets/2/rpcGetFilterKeys?includesHeaders=true"
                                    },
                                    {
                                        "name": "orderBy",
                                        "type": "select",
                                        "label": "Order by"
                                    },
                                    {
                                        "name": "sortOrder",
                                        "type": "select",
                                        "label": "Sort order",
                                        "validate": {
                                            "enum": [
                                                "asc",
                                                "desc"
                                            ]
                                        }
                                    }
                                ],
                                "interface": [
                                    {
                                        "name": "__IMTLENGTH__",
                                        "type": "uinteger",
                                        "label": "Total number of bundles"
                                    },
                                    {
                                        "name": "__IMTINDEX__",
                                        "type": "uinteger",
                                        "label": "Bundle order position"
                                    },
                                    {
                                        "name": "__ROW_NUMBER__",
                                        "type": "number",
                                        "label": "Row number"
                                    },
                                    {
                                        "name": "__SPREADSHEET_ID__",
                                        "type": "text",
                                        "label": "Spreadsheet ID"
                                    },
                                    {
                                        "name": "__SHEET__",
                                        "type": "text",
                                        "label": "Sheet"
                                    },
                                    {
                                        "name": "0",
                                        "type": "text",
                                        "label": "fecha (A)"
                                    },
                                    {
                                        "name": "1",
                                        "type": "text",
                                        "label": "comida (B)"
                                    },
                                    {
                                        "name": "2",
                                        "type": "text",
                                        "label": "ropa (C)"
                                    },
                                    {
                                        "name": "3",
                                        "type": "text",
                                        "label": "apps (D)"
                                    },
                                    {
                                        "name": "4",
                                        "type": "text",
                                        "label": "criterios (E)"
                                    },
                                    {
                                        "name": "5",
                                        "type": "text",
                                        "label": "origen  (F)"
                                    },
                                    {
                                        "name": "6",
                                        "type": "text",
                                        "label": "edad (G)"
                                    },
                                    {
                                        "name": "7",
                                        "type": "text",
                                        "label": "(H)"
                                    },
                                    {
                                        "name": "8",
                                        "type": "text",
                                        "label": "(I)"
                                    },
                                    {
                                        "name": "9",
                                        "type": "text",
                                        "label": "(J)"
                                    },
                                    {
                                        "name": "10",
                                        "type": "text",
                                        "label": "(K)"
                                    },
                                    {
                                        "name": "11",
                                        "type": "text",
                                        "label": "(L)"
                                    },
                                    {
                                        "name": "12",
                                        "type": "text",
                                        "label": "(M)"
                                    },
                                    {
                                        "name": "13",
                                        "type": "text",
                                        "label": "(N)"
                                    },
                                    {
                                        "name": "14",
                                        "type": "text",
                                        "label": "(O)"
                                    },
                                    {
                                        "name": "15",
                                        "type": "text",
                                        "label": "(P)"
                                    },
                                    {
                                        "name": "16",
                                        "type": "text",
                                        "label": "(Q)"
                                    },
                                    {
                                        "name": "17",
                                        "type": "text",
                                        "label": "(R)"
                                    },
                                    {
                                        "name": "18",
                                        "type": "text",
                                        "label": "(S)"
                                    },
                                    {
                                        "name": "19",
                                        "type": "text",
                                        "label": "(T)"
                                    },
                                    {
                                        "name": "20",
                                        "type": "text",
                                        "label": "(U)"
                                    },
                                    {
                                        "name": "21",
                                        "type": "text",
                                        "label": "(V)"
                                    },
                                    {
                                        "name": "22",
                                        "type": "text",
                                        "label": "(W)"
                                    },
                                    {
                                        "name": "23",
                                        "type": "text",
                                        "label": "(X)"
                                    },
                                    {
                                        "name": "24",
                                        "type": "text",
                                        "label": "(Y)"
                                    },
                                    {
                                        "name": "25",
                                        "type": "text",
                                        "label": "(Z)"
                                    },
                                    {
                                        "name": "26",
                                        "type": "text",
                                        "label": "(AA)"
                                    },
                                    {
                                        "name": "27",
                                        "type": "text",
                                        "label": "(AB)"
                                    },
                                    {
                                        "name": "28",
                                        "type": "text",
                                        "label": "(AC)"
                                    },
                                    {
                                        "name": "29",
                                        "type": "text",
                                        "label": "(AD)"
                                    },
                                    {
                                        "name": "30",
                                        "type": "text",
                                        "label": "(AE)"
                                    },
                                    {
                                        "name": "31",
                                        "type": "text",
                                        "label": "(AF)"
                                    },
                                    {
                                        "name": "32",
                                        "type": "text",
                                        "label": "(AG)"
                                    },
                                    {
                                        "name": "33",
                                        "type": "text",
                                        "label": "(AH)"
                                    },
                                    {
                                        "name": "34",
                                        "type": "text",
                                        "label": "(AI)"
                                    },
                                    {
                                        "name": "35",
                                        "type": "text",
                                        "label": "(AJ)"
                                    },
                                    {
                                        "name": "36",
                                        "type": "text",
                                        "label": "(AK)"
                                    },
                                    {
                                        "name": "37",
                                        "type": "text",
                                        "label": "(AL)"
                                    },
                                    {
                                        "name": "38",
                                        "type": "text",
                                        "label": "(AM)"
                                    },
                                    {
                                        "name": "39",
                                        "type": "text",
                                        "label": "(AN)"
                                    },
                                    {
                                        "name": "40",
                                        "type": "text",
                                        "label": "(AO)"
                                    },
                                    {
                                        "name": "41",
                                        "type": "text",
                                        "label": "(AP)"
                                    },
                                    {
                                        "name": "42",
                                        "type": "text",
                                        "label": "(AQ)"
                                    },
                                    {
                                        "name": "43",
                                        "type": "text",
                                        "label": "(AR)"
                                    },
                                    {
                                        "name": "44",
                                        "type": "text",
                                        "label": "(AS)"
                                    },
                                    {
                                        "name": "45",
                                        "type": "text",
                                        "label": "(AT)"
                                    },
                                    {
                                        "name": "46",
                                        "type": "text",
                                        "label": "(AU)"
                                    },
                                    {
                                        "name": "47",
                                        "type": "text",
                                        "label": "(AV)"
                                    },
                                    {
                                        "name": "48",
                                        "type": "text",
                                        "label": "(AW)"
                                    },
                                    {
                                        "name": "49",
                                        "type": "text",
                                        "label": "(AX)"
                                    },
                                    {
                                        "name": "50",
                                        "type": "text",
                                        "label": "(AY)"
                                    },
                                    {
                                        "name": "51",
                                        "type": "text",
                                        "label": "(AZ)"
                                    },
                                    {
                                        "name": "52",
                                        "type": "text",
                                        "label": "(BA)"
                                    },
                                    {
                                        "name": "53",
                                        "type": "text",
                                        "label": "(BB)"
                                    },
                                    {
                                        "name": "54",
                                        "type": "text",
                                        "label": "(BC)"
                                    },
                                    {
                                        "name": "55",
                                        "type": "text",
                                        "label": "(BD)"
                                    },
                                    {
                                        "name": "56",
                                        "type": "text",
                                        "label": "(BE)"
                                    },
                                    {
                                        "name": "57",
                                        "type": "text",
                                        "label": "(BF)"
                                    },
                                    {
                                        "name": "58",
                                        "type": "text",
                                        "label": "(BG)"
                                    },
                                    {
                                        "name": "59",
                                        "type": "text",
                                        "label": "(BH)"
                                    },
                                    {
                                        "name": "60",
                                        "type": "text",
                                        "label": "(BI)"
                                    },
                                    {
                                        "name": "61",
                                        "type": "text",
                                        "label": "(BJ)"
                                    },
                                    {
                                        "name": "62",
                                        "type": "text",
                                        "label": "(BK)"
                                    },
                                    {
                                        "name": "63",
                                        "type": "text",
                                        "label": "(BL)"
                                    },
                                    {
                                        "name": "64",
                                        "type": "text",
                                        "label": "(BM)"
                                    },
                                    {
                                        "name": "65",
                                        "type": "text",
                                        "label": "(BN)"
                                    },
                                    {
                                        "name": "66",
                                        "type": "text",
                                        "label": "(BO)"
                                    },
                                    {
                                        "name": "67",
                                        "type": "text",
                                        "label": "(BP)"
                                    },
                                    {
                                        "name": "68",
                                        "type": "text",
                                        "label": "(BQ)"
                                    },
                                    {
                                        "name": "69",
                                        "type": "text",
                                        "label": "(BR)"
                                    },
                                    {
                                        "name": "70",
                                        "type": "text",
                                        "label": "(BS)"
                                    },
                                    {
                                        "name": "71",
                                        "type": "text",
                                        "label": "(BT)"
                                    },
                                    {
                                        "name": "72",
                                        "type": "text",
                                        "label": "(BU)"
                                    },
                                    {
                                        "name": "73",
                                        "type": "text",
                                        "label": "(BV)"
                                    },
                                    {
                                        "name": "74",
                                        "type": "text",
                                        "label": "(BW)"
                                    },
                                    {
                                        "name": "75",
                                        "type": "text",
                                        "label": "(BX)"
                                    },
                                    {
                                        "name": "76",
                                        "type": "text",
                                        "label": "(BY)"
                                    },
                                    {
                                        "name": "77",
                                        "type": "text",
                                        "label": "(BZ)"
                                    },
                                    {
                                        "name": "78",
                                        "type": "text",
                                        "label": "(CA)"
                                    },
                                    {
                                        "name": "79",
                                        "type": "text",
                                        "label": "(CB)"
                                    },
                                    {
                                        "name": "80",
                                        "type": "text",
                                        "label": "(CC)"
                                    },
                                    {
                                        "name": "81",
                                        "type": "text",
                                        "label": "(CD)"
                                    },
                                    {
                                        "name": "82",
                                        "type": "text",
                                        "label": "(CE)"
                                    },
                                    {
                                        "name": "83",
                                        "type": "text",
                                        "label": "(CF)"
                                    },
                                    {
                                        "name": "84",
                                        "type": "text",
                                        "label": "(CG)"
                                    },
                                    {
                                        "name": "85",
                                        "type": "text",
                                        "label": "(CH)"
                                    },
                                    {
                                        "name": "86",
                                        "type": "text",
                                        "label": "(CI)"
                                    },
                                    {
                                        "name": "87",
                                        "type": "text",
                                        "label": "(CJ)"
                                    },
                                    {
                                        "name": "88",
                                        "type": "text",
                                        "label": "(CK)"
                                    },
                                    {
                                        "name": "89",
                                        "type": "text",
                                        "label": "(CL)"
                                    },
                                    {
                                        "name": "90",
                                        "type": "text",
                                        "label": "(CM)"
                                    },
                                    {
                                        "name": "91",
                                        "type": "text",
                                        "label": "(CN)"
                                    },
                                    {
                                        "name": "92",
                                        "type": "text",
                                        "label": "(CO)"
                                    },
                                    {
                                        "name": "93",
                                        "type": "text",
                                        "label": "(CP)"
                                    },
                                    {
                                        "name": "94",
                                        "type": "text",
                                        "label": "(CQ)"
                                    },
                                    {
                                        "name": "95",
                                        "type": "text",
                                        "label": "(CR)"
                                    },
                                    {
                                        "name": "96",
                                        "type": "text",
                                        "label": "(CS)"
                                    },
                                    {
                                        "name": "97",
                                        "type": "text",
                                        "label": "(CT)"
                                    },
                                    {
                                        "name": "98",
                                        "type": "text",
                                        "label": "(CU)"
                                    },
                                    {
                                        "name": "99",
                                        "type": "text",
                                        "label": "(CV)"
                                    },
                                    {
                                        "name": "100",
                                        "type": "text",
                                        "label": "(CW)"
                                    },
                                    {
                                        "name": "101",
                                        "type": "text",
                                        "label": "(CX)"
                                    },
                                    {
                                        "name": "102",
                                        "type": "text",
                                        "label": "(CY)"
                                    },
                                    {
                                        "name": "103",
                                        "type": "text",
                                        "label": "(CZ)"
                                    }
                                ]
                            }
                        },
                        {
                            "id": 6,
                            "module": "util:TextAggregator",
                            "version": 1,
                            "parameters": {
                                "feeder": 4,
                                "rowSeparator": ""
                            },
                            "mapper": {
                                "value": "{{Comida}} | {{Ropa}} | {{Apps}} | {{Criterio}} | {{Origen}} | {{Edad}}"
                            },
                            "metadata": {
                                "designer": {
                                    "x": 900,
                                    "y": 150
                                },
                                "setupValidation": {
                                    "result": {
                                        "valid": true,
                                        "fields": []
                                    },
                                    "version": 1,
                                    "configuration": "d4f7c06317bb5255"
                                },
                                "restore": {
                                    "extra": {
                                        "feeder": {
                                            "label": "Google Sheets - Search Rows [4]"
                                        }
                                    },
                                    "parameters": {
                                        "rowSeparator": {
                                            "label": "Empty"
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
                            "id": 8,
                            "module": "ai-local-agent:RunLocalAIAgent",
                            "version": 0,
                            "parameters": {
                                "makeConnectionId": 10593897
                            },
                            "mapper": {
                                "files": [],
                                "message": "Respuestas de la encuesta (comida | ropa | apps | criterio | origen | edad):",
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
                                "systemPrompt": "Eres un analista de economia local para alumnos de Desarrollo Sustentable del TecNM en Mazatlan,\r\nSinaloa.\r\nRecibiras las respuestas de una encuesta, una por linea, con el formato: comida | ropa | apps |\r\ncriterio | origen | edad.\r\nUsa UNICAMENTE esas respuestas; no inventes datos.\r\nResponde en texto plano (sin asteriscos, sin markdown), en espanol, con este formato:\r\nTOTAL DE RESPUESTAS: [numero]\r\nRESULTADOS\r\nComida: [cada opcion con su porcentaje]\r\nRopa: [...]\r\nApps internacionales: [...]\r\nCriterio de compra: [...]\r\nConoce el origen: [...]\r\nANALISIS\r\n[4 lineas maximo: que tan local o global es el consumo de esta comunidad y que diferencias hay\r\npor edad]\r\nCONCLUSIONES\r\n1. [efecto en la economia local]\r\n2. [efecto ambiental por transporte y empaques]\r\n3. [una accion concreta para impulsar el consumo local]",
                                "promptCaching": "none",
                                "fallbackEnabled": false
                            },
                            "metadata": {
                                "designer": {
                                    "x": 1200,
                                    "y": 150
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
                            "tools": []
                        },
                        {
                            "id": 9,
                            "module": "gateway:WebhookRespond",
                            "version": 1,
                            "parameters": {},
                            "mapper": {
                                "body": "{{8.response}}",
                                "status": "200",
                                "headers": []
                            },
                            "metadata": {
                                "designer": {
                                    "x": 1500,
                                    "y": 150
                                },
                                "setupValidation": {
                                    "result": {
                                        "valid": true,
                                        "fields": []
                                    },
                                    "version": 1,
                                    "configuration": "b49d925869f05b32"
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

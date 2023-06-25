## newPage vs pageList

```json
{
    "_id": "63567eb3d1e1de1000000004",
    "applicationId": "jetsondashboard",
    "slug": "ResetPassword",
    "createdAt": "2022-10-24T12:01:55.988Z",
    "updatedAt": "2022-10-24T09:41:39.201Z",
    "deleted": false,
    "policies": [
        {
            "permission": "read:pages",
            "groups": [],
            "users": [
                null
            ]
        },
        {
            "permission": "manage:pages",
            "groups": [],
            "users": [
                null
            ]
        }
    ],
    "Page": {
        "name": "ResetPassword",
        "layouts": [
            {
                "_id": "63565dd3d1e1de1000000002",
                "viewMode": false,
                "dsl": {
                    "widgetName": "MainContainer",
                    "backgroundColor": "none",
                    "rightColumn": 1224,
                    "snapColumns": 64,
                    "widgetId": "0",
                    "topRow": 0,
                    "bottomRow": 750,
                    "parentRowSpace": 1,
                    "type": "CANVAS_WIDGET",
                    "detachFromLayout": true,
                    "minHeight": 760,
                    "dynamicBindingPathList": [],
                    "parentColumnSpace": 1,
                    "leftColumn": 0,
                    "children": [
					....
                    ],
                    "snapRows": 75,
                    "containerStyle": "none",
                    "canExtend": true,
                    "version": 57
                },
                "widgetNames": [
                    "MainContainer",
                    "GridLayout1",
                    "GridLayoutCanvas1",
                    "RowContainer1",
                    "RowLayoutCanvas1",
                    "Container1",
                    "Canvas12",
                    "Text1Copy",
                    "InputConfirmPassword",
                    "Image2",
                    "InputPassword",
                    "Text1",
                    "Button1"
                ],
                "deleted": false,
                "policies": [],
                "layoutOnLoadActions": [
                    []
                ],
                "layoutOnCloseActions": [
                    []
                ]
            }
        ],
        "isHidden": false
    }
},
```



```json
{
    "unpublishedPage": {
        "name": "Dashboard",
        "slug": "dashboard",
        "layouts": [
            {
                "viewMode": false,
                "dsl": {
                    "widgetName": "MainContainer",
                    "backgroundColor": "none",
                    "rightColumn": 1224.0,
                    "snapColumns": 64.0,
                    "detachFromLayout": true,
                    "widgetId": "0",
                    "topRow": 0.0,
                    "bottomRow": 1220.0,
                    "containerStyle": "none",
                    "snapRows": 95.0,
                    "parentRowSpace": 1.0,
                    "type": "CANVAS_WIDGET",
                    "canExtend": true,
                    "version": 79.0,
                    "minHeight": 970.0,
                    "parentColumnSpace": 1.0,
                    "dynamicBindingPathList": [],
                    "leftColumn": 0.0,
                    "children": [
                    ...
                    ]
                },
                "layoutOnLoadActions": [
                    [
                        ...
                ],
                "layoutOnLoadActionErrors": [],
                "validOnPageLoadActions": true,
                "id": "Dashboard",
                "deleted": false,
                "policies": [],
                "userPermissions": []
            }
        ],
        "userPermissions": [],
        "policies": [],
        "isHidden": true
    },                                
```



## newAction

pluginType

pluginId

```json
[
{
    "_id": "6356a851d1e1de1000000008",
    "applicationId": "jetsondashboard",
    "organizationId": "Org",
    "pluginType": "API",
    "pluginId": "API",
    "createdAt": "2022-10-24T14:59:29.274Z",
    "updatedAt": "2023-05-19T11:35:40.573Z",
    "deleted": false,
    "policies": [
        {
            "permission": "read:actions",
            "groups": [],
            "users": []
        },
        {
            "permission": "manage:actions",
            "groups": [],
            "users": []
        },
        {
            "permission": "execute:actions",
            "groups": [],
            "users": []
        }
    ],
    "Action": {
        "name": "sendEmailForResetPassword",
        "datasource": {
            "invalids": [],
            "datasourceConfiguration": {
                "url": "{{main.env.nodeUrl}}/sendEmailForResetPassword"
            },
            "isValid": true,
            "name": "DEFAULT_REST_DATASOURCE",
            "new": true,
            "organizationId": "Org",
            "pluginId": "API",
            "userPermissions": []
        },
        "executeOnLoad": false,
        "pageId": "queryToResetPassword",
        "actionConfiguration": {
            "timeoutInMillisecond": 10000,
            "encodeParamsToggle": true,
            "httpMethod": "POST",
            "headers": [
                {
                    "key": "content-type",
                    "value": "application/json"
                }
            ],
            "queryParameters": [],
            "bodyFormData": [],
            "formData": {
                "apiContentType": "none"
            },
            "pluginSpecifiedTemplates": [
                {
                    "value": true
                }
            ],
            "path": "",
            "body": "{\n\t\"email\": \"{{InputEmail.text}}\"\n}"
        },
        "dynamicBindingPathList": [
            {
                "key": "body"
            },
            {
                "key": "datasourceUrl"
            }
        ],
        "isValid": true,
        "invalids": [],
        "jsonPathKeys": [
            "main.env.nodeUrl",
            "InputEmail.text"
        ],
        "userSetOnLoad": false,
        "confirmBeforeExecute": false
    }
},
]
```



## newCollection

```json
[
{
    "_id": "6364e18e65d44c1100000006",
    "name": "JSObject1",
    "pageId": "UserManagement",
    "organizationId": "Org",
    "body": "export default {\n\teditUserRole: ...\n}",
    "variables": [],
    "actions": [
        {
            "_id": "6364e18ec2e17400119dc7f1",
            "name": "editUserRole",
            "pageId": "User Management",
            "organizationId": "Org",
            "executeOnLoad": false,
            "actionConfiguration": {
                "body": "async ..}",
                "isAsync": true,
                "timeoutInMillisecond": 10000,
                "jsArguments": [],
                "paginationType": "NONE",
                "encodeParamsToggle": true
            },
            "clientSideExecution": true,
            "collectionId": "6364e18e65d44c1100000006",
            "applicationId": "jetsondashboard",
            "datasource": {
                "isValid": true,
                "messages": [],
                "name": "UNUSED_DATASOURCE",
                "new": true,
                "organizationId": "Org",
                "pluginId": "",
                "userPermissions": []
            },
            "dynamicBindingPathList": [
                {
                    "key": "body"
                }
            ],
            "fullyQualifiedName": "JSObject1.myFun2",
            "isValid": true,
            "jsonPathKeys": [
                "async () => {\n\t\t//use async-await or promises\n\t}"
            ],
            "pluginType": "JS",
            "id": "6364e18ec2e17400119dc7f1"
        },
        {
            "name": "createUser",
            "collectionId": "6364e18e65d44c1100000006",
            "executeOnLoad": false,
            "pageId": "User Management",
            "organizationId": "Org",
            "actionConfiguration": {
                "body": "async () => {\n\t\tawait ;\n\t}",
                "isAsync": true,
                "timeoutInMillisecond": 0,
                "jsArguments": []
            }
        }
    ],
    "applicationId": "jetsondashboard",
    "pluginType": "JS",
    "id": "6364e18e65d44c1100000006",
    "actionIds": [],
    "archivedActionIds": [],
    "archivedActions": [],
    "pluginId": "JS",
    "workspaceId": "Org"
}
],
```



## organization

```json
{
    "_id": "6400a9c121a064c14ad6d8a4",
    "name": "Org",
    "organizationSettings": [],
    "plugins": [
        {
            "pluginId": "API",
            "status": "FREE",
            "deleted": false,
            "policies": []
        },
        {
            "pluginId": "JS",
            "status": "FREE",
            "deleted": false,
            "policies": []
        }
    ],
    "slug": "Org",
    "userRoles": [],
    "createdAt": "2023-03-02T13:50:57.853Z",
    "deleted": false,
    "policies": []
},
```



## application vs exportedApplication

application  ubos v2

```json
"application": {
    "_id": "62b41da7022a791200000002",
    "name": "Authorization",
    "slug": "jetsondashboard",
    "organizationId": "Org",
    "isPublic": true,
    "createdAt": "2023-03-02T13:50:57.853Z",
    "updatedAt": "2023-05-19T14:54:13.221Z",
    "deleted": false,
    "pages": [
        {
            "_id": "Login",
            "isDefault": true
        },
    ],
    "policies": [
        {
            "permission": "makePublic:applications",
            "groups": [],
            "users": []
        },
        {
            "permission": "read:applications",
            "groups": [],
            "users": []
        },
        {
            "permission": "publish:applications",
            "groups": [],
            "users": []
        },
        {
            "permission": "manage:applications",
            "groups": [],
            "users": []
        }
    ],
    "function_dsl": [],
    "version": "V1"
}               
```

exportedApplication Appsmith

```json
{
    "name": "Inventory Management Dashboard",
    "isPublic": false,
    "pages": [
        {
            "id": "Dashboard",
            "isDefault": true
        },
        {
            "id": "Products",
            "isDefault": false
        },
        {
            "id": "Purchase Orders",
            "isDefault": false
        },
        {
            "id": "Suppliers",
            "isDefault": false
        },
        {
            "id": "Warehouses",
            "isDefault": false
        }
    ],
    "publishedPages": [
        {
            "id": "Dashboard",
            "isDefault": true
        },
        {
            "id": "Products",
            "isDefault": false
        },
        {
            "id": "Purchase Orders",
            "isDefault": false
        },
        {
            "id": "Suppliers",
            "isDefault": false
        },
        {
            "id": "Warehouses",
            "isDefault": false
        }
    ],
    "viewMode": false,
    "appIsExample": false,
    "unreadCommentThreads": 0.0,
    "color": "#EAEDFB",
    "icon": "cloud",
    "slug": "inventory-management-dashboard",
    "unpublishedAppLayout": {
        "type": "DESKTOP"
    },
    "publishedAppLayout": {
        "type": "DESKTOP"
    },
    "unpublishedCustomJSLibs": [],
    "publishedCustomJSLibs": [],
    "evaluationVersion": 2.0,
    "applicationVersion": 2.0,
    "embedSetting": {
        "height": "720px",
        "width": "1024px",
        "showNavigationBar": false
    },
    "collapseInvisibleWidgets": true,
    "forkingEnabled": true,
    "isManualUpdate": false,
    "deleted": false
}
```



## version

```json
{
    "_id": "63565dd3d1e1de1000000001",
    "applicationId": "jetsondashboard",
    "slug": "queryToResetPassword",
    "createdAt": "2022-10-24T09:41:39.201Z",
    "updatedAt": "2022-10-24T09:41:39.201Z",
    "deleted": false,
    "policies": [
    ],
    "Page": {
        "name": "queryToResetPassword",
        "layouts": [
        ],
        "isHidden": false
    }
    }
```


<!-- AUTO GENERATED CODE. DO NOT EDIT MANUALLY. -->
# cdap_application


# Example

Note, `jsonencode` is used for the purpose of explicit example.
In most real use cases you would just use.
`spec = file("${path.module}/realtive/path/to/pipeline_spec.json")`
```
resource "cdap_application" "pipeline" {
    name = "example_pipeline"
    spec = jsonencode({
        "name": "example_pipeline",
        "description": "Example",
        "artifact": {
            "name": "cdap-data-streams",
            "version": "6.1.1",
            "scope": "SYSTEM"
        },
        "config": {
            "resources": {
                "memoryMB": 2048,
                "virtualCores": 1
            },
            "driverResources": {
                "memoryMB": 2048,
                "virtualCores": 1
            },
            "connections": [
                {
                    "from": "gcs_input",
                    "to": "gcs_output"
                }
            ],
            "processTimingEnabled": true,
            "stageLoggingEnabled": true,
            "stages": [
                {
                    "name": "gcs_input",
                    "plugin": {
                        "name": "GCSFile",
                        "type": "batchsource",
                        "label": "GCS Input",
                        "artifact": {
                            "name": "google-cloud",
                            "version": "0.13.2",
                            "scope": "SYSTEM"
                        },
                        "properties": {
                            "project": "auto-detect",
                            "format": "text",
                            "serviceFilePath": "auto-detect",
                            "filenameOnly": "false",
                            "recursive": "false",
                            "copyHeader": "false",
                            "schema": "{\"type\":\"record\",\"name\":\"etlSchemaBody\",\"fields\":[{\"name\":\"body\",\"type\":\"string\"}]}",
                            "path": "TODO",
                            "referenceName": "input"
                        }
                    },
                    "outputSchema": "{\"type\":\"record\",\"name\":\"etlSchemaBody\",\"fields\":[{\"name\":\"body\",\"type\":\"string\"}]}",
                    "type": "batchsource",
                    "label": "gcs_input",
                    "icon": "fa-plug",
                    "$$hashKey": "object:2909",
                    "_uiPosition": {
                        "left": "880px",
                        "top": "550px"
                    }
                },
                {
                    "name": "gcs_output",
                    "plugin": {
                        "name": "GCS",
                        "type": "batchsink",
                        "label": "GCS Output",
                        "artifact": {
                            "name": "google-cloud",
                            "version": "0.13.2",
                            "scope": "SYSTEM"
                        },
                        "properties": {
                            "project": "auto-detect",
                            "suffix": "yyyy-MM-dd-HH-mm",
                            "format": "json",
                            "serviceFilePath": "auto-detect",
                            "location": "us",
                            "schema": "{\"type\":\"record\",\"name\":\"etlSchemaBody\",\"fields\":[{\"name\":\"body\",\"type\":\"string\"}]}",
                            "referenceName": "gcs_output",
                            "path": "TODO"
                        }
                    },
                    "outputSchema": "{\"type\":\"record\",\"name\":\"etlSchemaBody\",\"fields\":[{\"name\":\"body\",\"type\":\"string\"}]}",
                    "inputSchema": [
                        {
                            "name": "gcs_input",
                            "schema": "{\"type\":\"record\",\"name\":\"etlSchemaBody\",\"fields\":[{\"name\":\"body\",\"type\":\"string\"}]}"
                        }
                    ],
                    "type": "batchsink",
                    "label": "gcs_output",
                    "icon": "fa-plug",
                    "$$hashKey": "object:2911",
                    "_uiPosition": {
                        "left": "1180px",
                        "top": "550px"
                    }
                }
            ],
            "schedule": "0 * * * *",
            "engine": "spark",
            "numOfRecordsPreview": 100,
            "maxConcurrentRuns": 1
        }
    })
}
```

## Argument Reference

The following fields are supported:

* name
  (Required):
  The name of the application. This will be used as the unique identifier in the CDAP API.

* namespace
  (Optional):
  The name of the namespace in which this resource belongs. If not provided, the default namespace is used.

* spec
  (Required):
  The full contents of the exported pipeline JSON spec.



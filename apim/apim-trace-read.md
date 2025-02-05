# API Trace Read

This document describes how to use the `api-trace.http` script to trace API calls in Azure API Management.

## Prerequisites

1. **Entra App Registration**: Some of the variable values required by the script need an Entra app registration. Ensure you have registered an application in Entra and have the following details:
   - Client ID
   - Client Secret
   - Tenant ID
The app registration can be made using the following command, be sure to record the results which will contain the above values:
```bash
az ad sp create-for-rbac
```
## Usage

1. **Set Environment Variables**: Open the `api-trace.http` script and set the following variables with your Entra app registration details and other required values:
   - `@client_id`: Your Entra app's Client ID
   - `@client_secret`: Your Entra app's Client Secret
   - `@tenant_id`: Your Entra app's Tenant ID
   - `@subscription_id`: Your Azure Subscription ID
   - `@resource_group`: Your Azure Resource Group name
   - `@service_name`: Your API Management service name
   - `@trace_id`: The trace ID you want to read

2. **Run the Script**: Use a tool like Visual Studio Code with the REST Client extension to run the requests in `api-trace.http` script.  Run the requests in order, it will authenticate using the provided Entra app registration details and retrieve the API trace information.  The output trace response can be saved to disk using the save response icon which will appear above the response pane.

## Example

```http
# Set variables
@client_id = <your-client-id>
@client_secret = <your-client-secret>
@tenant_id = <your-tenant-id>
@subscription_id = <your-subscription-id>
@resource_group = <your-resource-group>
@service_name = <your-service-name>
@trace_id = <your-trace-id>

# Request to get the API trace
GET https://management.azure.com/subscriptions/{{subscription_id}}/resourceGroups/{{resource_group}}/providers/Microsoft.ApiManagement/service/{{service_name}}/traces/{{trace_id}}?api-version=2021-04-01-preview
Authorization: Bearer {{access_token}}
```

Ensure you replace the placeholder values with your actual details before running the script.

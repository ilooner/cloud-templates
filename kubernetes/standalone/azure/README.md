## Prereqs For Script

 1. Create a resource group. `az group create --name myResourceGroup --location centralus`
 2. Create a log workspace. `Log Analytics -> Add`
 3. Create a servicePrincipal `az ad sp create-for-rbac --skip-assignment`
 4. Record service principal id
 5. Create a vnet `az network vnet create --name myVirtualNetwork --resource-group myResourceGroup --subnet-name default`
 6. Save subnet id

## TODO

 - Make it work with azure networking and custom vnet.
 - Add operation management, currently not working
 ```
    {
      "apiVersion": "2015-11-01-preview",
      "type": "Microsoft.OperationsManagement/solutions",
      "location": "[parameters('workspaceLocation')]",
      "name": "[concat('ContainerInsights', '(', parameters('deploymentId'), ')')]",
      "dependsOn": ["[concat('Microsoft.OperationalInsights/workspaces/', variables('omswsName'))]"],
      "properties": {
        "workspaceResourceId": "[resourceId('Microsoft.OperationalInsights/workspaces', variables('omswsName'))]"
      },
      "plan": {
        "name": "[concat('ContainerInsights', '(', variables('omswsName'), ')')]",
        "product": "[concat('OMSGallery/', 'ContainerInsights')]",
        "promotionCode": "",
        "publisher": "Microsoft"
      }
    },
```

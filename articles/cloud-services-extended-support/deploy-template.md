---
title: Wdrażanie usługi w chmurze platformy Azure (obsługa rozszerzona) — szablony
description: Wdrażanie usługi w chmurze platformy Azure (obsługa rozszerzona) przy użyciu szablonów ARM
ms.topic: tutorial
ms.service: cloud-services-extended-support
author: gachandw
ms.author: gachandw
ms.reviewer: mimckitt
ms.date: 10/13/2020
ms.custom: ''
ms.openlocfilehash: a606956483ddb7c7f3a4f3cef8728ade508ab461
ms.sourcegitcommit: 87a6587e1a0e242c2cfbbc51103e19ec47b49910
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 03/16/2021
ms.locfileid: "103574275"
---
# <a name="deploy-a-cloud-service-extended-support-using-arm-templates"></a>Wdrażanie usługi w chmurze (obsługa rozszerzona) przy użyciu szablonów usługi ARM

W tym samouczku wyjaśniono, jak utworzyć wdrożenie usługi w chmurze (obsługa rozszerzona) przy użyciu [szablonów ARM](../azure-resource-manager/templates/overview.md). 

> [!IMPORTANT]
> Cloud Services (obsługa rozszerzona) jest obecnie dostępna w publicznej wersji zapoznawczej.
> Ta wersja zapoznawcza nie jest objęta umową dotyczącą poziomu usług i nie zalecamy korzystania z niej w przypadku obciążeń produkcyjnych. Niektóre funkcje mogą być nieobsługiwane lub ograniczone.
> Aby uzyskać więcej informacji, zobacz [Uzupełniające warunki korzystania z wersji zapoznawczych platformy Microsoft Azure](https://azure.microsoft.com/support/legal/preview-supplemental-terms/).


## <a name="before-you-begin"></a>Zanim rozpoczniesz

1. Zapoznaj się z [wymaganiami wstępnymi](deploy-prerequisite.md) dotyczącymi wdrażania Cloud Services (obsługa rozszerzona) i Utwórz skojarzone zasoby.

2. Utwórz nową grupę zasobów przy użyciu [Azure Portal](/azure/azure-resource-manager/management/manage-resource-groups-portal) lub [programu PowerShell](/azure/azure-resource-manager/management/manage-resource-groups-powershell). Ten krok jest opcjonalny, jeśli używasz istniejącej grupy zasobów.
 
3. Utwórz nowe konto magazynu przy użyciu [Azure Portal](/azure/storage/common/storage-account-create?tabs=azure-portal) lub [programu PowerShell](/azure/storage/common/storage-account-create?tabs=azure-powershell). Ten krok jest opcjonalny, jeśli używasz istniejącego konta magazynu.

4. Przekaż pliki definicji usługi (. csdef) i konfiguracji usługi (. cscfg) do konta magazynu przy użyciu [Azure Portal](/azure/storage/blobs/storage-quickstart-blobs-portal#upload-a-block-blob), [AzCopy](/azure/storage/common/storage-use-azcopy-blobs-upload?toc=/azure/storage/blobs/toc.json) lub [PowerShell](/azure/storage/blobs/storage-quickstart-blobs-powershell#upload-blobs-to-the-container). Uzyskaj identyfikatory URI sygnatury dostępu współdzielonego dla obu plików, które mają zostać dodane do szablonu ARM w dalszej części tego samouczka.

5. Obowiązkowe Utwórz magazyn kluczy i przekaż certyfikaty.

    -  Certyfikaty mogą być dołączane do usług w chmurze w celu zapewnienia bezpiecznej komunikacji z usługą i z niej. Aby można było korzystać z certyfikatów, ich odciski palców muszą być określone w pliku konfiguracji usługi (. cscfg) i przekazywane do magazynu kluczy. Magazyn kluczy można utworzyć za pomocą [Azure Portal](/azure/key-vault/general/quick-create-portal) lub [programu PowerShell](/azure/key-vault/general/quick-create-powershell).
    - Skojarzony Magazyn kluczy musi znajdować się w tym samym regionie i w ramach subskrypcji co usługa w chmurze.
    - Skojarzony Magazyn kluczy dla programu musi mieć włączone odpowiednie uprawnienia, aby zasób Cloud Services (obsługa rozszerzona) mógł pobrać certyfikaty z Key Vault. Aby uzyskać więcej informacji, zobacz [Certyfikaty i Key Vault](certificates-and-key-vault.md)
    - Magazyn kluczy musi być przywoływany w sekcji OsProfile szablonu ARM przedstawionym w poniższych krokach.

## <a name="deploy-a-cloud-service-extended-support"></a>Wdrażanie usługi w chmurze (obsługa rozszerzona)

> [!NOTE]
> Alternatywny sposób wdrożenia usługi w chmurze (obsługa rozszerzona) odbywa się za pośrednictwem [Azure Portal](https://portal.azure.com). Możesz pobrać wygenerowany szablon ARM za pośrednictwem portalu dla przyszłych wdrożeń
 
1. Utwórz sieć wirtualną. Nazwa sieci wirtualnej musi być zgodna z odwołaniami w pliku konfiguracji usługi (. cscfg). Jeśli używasz istniejącej sieci wirtualnej, Pomiń tę sekcję z szablonu ARM.

    ```json
    "resources": [ 
        { 
          "apiVersion": "2019-08-01", 
          "type": "Microsoft.Network/virtualNetworks", 
          "name": "[parameters('vnetName')]", 
          "location": "[parameters('location')]", 
          "properties": { 
            "addressSpace": { 
              "addressPrefixes": [ 
                "10.0.0.0/16" 
              ] 
            }, 
            "subnets": [ 
              { 
                "name": "WebTier", 
                "properties": { 
                  "addressPrefix": "10.0.0.0/24" 
                } 
              } 
            ] 
          } 
        } 
    ] 
    ```
    
     W przypadku tworzenia nowej sieci wirtualnej Dodaj następujące elementy do sekcji, `dependsOn` Aby upewnić się, że platforma tworzy sieć wirtualną przed utworzeniem usługi w chmurze.

    ```json
    "dependsOn": [ 
            "[concat('Microsoft.Network/virtualNetworks/', parameters('vnetName'))]" 
     ] 
    ```
 
2. Utwórz publiczny adres IP i (opcjonalnie) ustaw właściwość etykieta DNS publicznego adresu IP. Jeśli używasz statycznego adresu IP, musisz odwołać się do niego jako Zastrzeżony adres IP w pliku konfiguracji usługi (. cscfg). Jeśli używany jest istniejący adres IP, Pomiń ten krok i Dodaj informacje o adresie IP bezpośrednio do ustawień konfiguracji usługi równoważenia obciążenia dla szablonu ARM.
 
    ```json
    "resources": [ 
        { 
          "apiVersion": "2019-08-01", 
          "type": "Microsoft.Network/publicIPAddresses", 
          "name": "[parameters('publicIPName')]", 
          "location": "[parameters('location')]", 
          "properties": { 
            "publicIPAllocationMethod": "Dynamic", 
            "idleTimeoutInMinutes": 10, 
            "publicIPAddressVersion": "IPv4", 
            "dnsSettings": { 
              "domainNameLabel": "[variables('dnsName')]" 
            } 
          }, 
          "sku": { 
            "name": "Basic" 
          } 
        } 
    ] 
    ```
     
     Jeśli tworzysz nowy adres IP, Dodaj następujący element do sekcji, `dependsOn` Aby upewnić się, że platforma tworzy adres IP przed utworzeniem usługi w chmurze.
    
    ```json
    "dependsOn": [ 
            "[concat('Microsoft.Network/publicIPAddresses/', parameters('publicIPName'))]" 
          ] 
    ```
 
3. Utwórz obiekt profilu sieciowego i skojarz publiczny adres IP z frontonem modułu równoważenia obciążenia. Moduł równoważenia obciążenia jest automatycznie tworzony przez platformę.

    ```json
    "networkProfile": { 
        "loadBalancerConfigurations": [ 
          { 
            "id": "[concat(variables('resourcePrefix'), 'Microsoft.Network/loadBalancers/', variables('lbName'))]", 
            "name": "[variables('lbName')]", 
            "properties": { 
              "frontendIPConfigurations": [ 
                { 
                  "name": "[variables('lbFEName')]", 
                  "properties": { 
                    "publicIPAddress": { 
                      "id": "[concat(variables('resourcePrefix'), 'Microsoft.Network/publicIPAddresses/', parameters('publicIPName'))]" 
                    } 
                  } 
                } 
              ] 
            } 
          } 
        ] 
      } 
    ```
 

4. Dodaj odwołanie do magazynu kluczy w  `OsProfile`   sekcji szablonu ARM. Key Vault jest używany do przechowywania certyfikatów skojarzonych z Cloud Services (obsługa rozszerzona). Dodaj certyfikaty do Key Vault, a następnie odwołując się do odcisków palców certyfikatu w pliku konfiguracji usługi (cscfg). Należy również włączyć Key Vault dla odpowiednich uprawnień, aby zasób Cloud Services (obsługa rozszerzona) mógł pobrać certyfikat zapisany jako wpisy tajne z Key Vault. Magazyn kluczy musi znajdować się w tym samym regionie i w ramach subskrypcji co usługa w chmurze i mieć unikatową nazwę. Aby uzyskać więcej informacji, zobacz [Korzystanie z certyfikatów z Cloud Services (obsługa rozszerzona)](certificates-and-key-vault.md).
     
    ```json
    "osProfile": { 
          "secrets": [ 
            { 
              "sourceVault": { 
                "id": "/subscriptions/{subscription-id}/resourceGroups/{resource-group}/providers/Microsoft.KeyVault/vaults/{keyvault-name}" 
              }, 
              "vaultCertificates": [ 
                { 
                  "certificateUrl": "https://{keyvault-name}.vault.azure.net:443/secrets/ContosoCertificate/{secret-id}" 
                } 
              ] 
            } 
          ] 
        } 
    ```
  
    > [!NOTE]
    > SourceVault to identyfikator zasobu ARM do magazynu kluczy. Te informacje można znaleźć, lokalizowanie identyfikatora zasobu w sekcji właściwości magazynu kluczy.
    > - certificateUrl można znaleźć, przechodząc do certyfikatu w magazynie kluczy oznaczonym jako **Identyfikator tajny**.  
   >  - certificateUrl powinna mieć postać https://{endpoin}/Secret/{tajnname}/{Secret-ID}

5. Utwórz profil roli. Upewnij się, że liczba ról, nazw ról, liczby wystąpień w każdej roli i rozmiarze jest taka sama w sekcji Konfiguracja usługi (cscfg), definicja usługi (. csdef) i profil roli w szablonie ARM.
    
    ```json
    "roleProfile": {
      "roles": {
        "value": [
          {
            "name": "WebRole1",
            "sku": {
              "name": "Standard_D1_v2",
              "capacity": "1"
            }
          },
          {
            "name": "WorkerRole1",
            "sku": {
              "name": "Standard_D1_v2",
              "capacity": "1"
            } 
          } 
        ]
      }
    }   
    ```

6. Obowiązkowe Utwórz profil rozszerzenia, aby dodać rozszerzenia do usługi w chmurze. Na potrzeby tego przykładu dodajemy rozszerzenie diagnostyki usług pulpitu zdalnego i platformy Microsoft Azure.
    
    ```json
        "extensionProfile": {
          "extensions": [
            {
              "name": "RDPExtension",
              "properties": {
                "autoUpgradeMinorVersion": true,
                "publisher": "Microsoft.Windows.Azure.Extensions",
                "type": "RDP",
                "typeHandlerVersion": "1.2.1",
                "settings": "<PublicConfig>\r\n <UserName>[Insert Username]</UserName>\r\n <Expiration>1/21/2022 12:00:00 AM</Expiration>\r\n</PublicConfig>",
                "protectedSettings": "<PrivateConfig>\r\n <Password>[Insert Password]</Password>\r\n</PrivateConfig>"
              }
            },
            {
              "name": "Microsoft.Insights.VMDiagnosticsSettings_WebRole1",
              "properties": {
                "autoUpgradeMinorVersion": true,
                "publisher": "Microsoft.Azure.Diagnostics",
                "type": "PaaSDiagnostics",
                "typeHandlerVersion": "1.5",
                "settings": "[parameters('wadPublicConfig_WebRole1')]",
                "protectedSettings": "[parameters('wadPrivateConfig_WebRole1')]",
                "rolesAppliedTo": [
                  "WebRole1"
                ]
              }
            }
          ]
        }
    ```

7. Zapoznaj się z pełnym szablonem.

    ```json
    {
      "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
      "contentVersion": "1.0.0.0",
      "parameters": {
        "cloudServiceName": {
          "type": "string",
          "metadata": {
            "description": "Name of the cloud service"
          }
        },
        "location": {
          "type": "string",
          "metadata": {
            "description": "Location of the cloud service"
          }
        },
        "deploymentLabel": {
          "type": "string",
          "metadata": {
            "description": "Label of the deployment"
          }
        },
        "packageSasUri": {
          "type": "securestring",
          "metadata": {
            "description": "SAS Uri of the CSPKG file to deploy"
          }
        },
        "configurationSasUri": {
          "type": "securestring",
          "metadata": {
            "description": "SAS Uri of the service configuration (.cscfg)"
          }
        },
        "roles": {
          "type": "array",
          "metadata": {
            "description": "Roles created in the cloud service application"
          }
        },
        "wadPublicConfig_WebRole1": {
          "type": "string",
          "metadata": {
             "description": "Public configuration of Windows Azure Diagnostics extension"
          }
        },
        "wadPrivateConfig_WebRole1": {
          "type": "securestring",
          "metadata": {
            "description": "Private configuration of Windows Azure Diagnostics extension"
          }
        },
        "vnetName": {
          "type": "string",
          "defaultValue": "[concat(parameters('cloudServiceName'), 'VNet')]",
          "metadata": {
            "description": "Name of vitual network"
          }
        },
        "publicIPName": {
          "type": "string",
          "defaultValue": "contosocsIP",
          "metadata": {
            "description": "Name of public IP address"
          }
        },
        "upgradeMode": {
          "type": "string",
          "defaultValue": "Auto",
          "metadata": {
            "UpgradeMode": "UpgradeMode of the CloudService"
          }
        }
      },
      "variables": {
        "cloudServiceName": "[parameters('cloudServiceName')]",
        "subscriptionID": "[subscription().subscriptionId]",
        "dnsName": "[variables('cloudServiceName')]",
        "lbName": "[concat(variables('cloudServiceName'), 'LB')]",
        "lbFEName": "[concat(variables('cloudServiceName'), 'LBFE')]",
        "resourcePrefix": "[concat('/subscriptions/', variables('subscriptionID'), '/resourceGroups/', resourceGroup().name, '/providers/')]"
      },
      "resources": [
        {
          "apiVersion": "2019-08-01",
          "type": "Microsoft.Network/virtualNetworks",
          "name": "[parameters('vnetName')]",
          "location": "[parameters('location')]",
          "properties": {
            "addressSpace": {
              "addressPrefixes": [
                "10.0.0.0/16"
              ]
            },
            "subnets": [
              {
                "name": "WebTier",
                "properties": {
                  "addressPrefix": "10.0.0.0/24"
                }
              }
            ]
          }
        },
        {
          "apiVersion": "2019-08-01",
          "type": "Microsoft.Network/publicIPAddresses",
          "name": "[parameters('publicIPName')]",
          "location": "[parameters('location')]",
          "properties": {
            "publicIPAllocationMethod": "Dynamic",
            "idleTimeoutInMinutes": 10,
            "publicIPAddressVersion": "IPv4",
            "dnsSettings": {
              "domainNameLabel": "[variables('dnsName')]"
            }
          },
          "sku": {
            "name": "Basic"
          }
        },
        {
          "apiVersion": "2020-10-01-preview",
          "type": "Microsoft.Compute/cloudServices",
          "name": "[variables('cloudServiceName')]",
          "location": "[parameters('location')]",
          "tags": {
            "DeploymentLabel": "[parameters('deploymentLabel')]",
            "DeployFromVisualStudio": "true"
          },
          "dependsOn": [
            "[concat('Microsoft.Network/virtualNetworks/', parameters('vnetName'))]",
            "[concat('Microsoft.Network/publicIPAddresses/', parameters('publicIPName'))]"
          ],
          "properties": {
            "packageUrl": "[parameters('packageSasUri')]",
            "configurationUrl": "[parameters('configurationSasUri')]",
            "upgradeMode": "[parameters('upgradeMode')]",
            "roleProfile": {
              "roles": [
                {
                  "name": "WebRole1",
                  "sku": {
                    "name": "Standard_D1_v2",
                    "capacity": "1"
                  }
                },
                {
                  "name": "WorkerRole1",
                  "sku": {
                    "name": "Standard_D1_v2",
                    "capacity": "1"
                  }
                }
              ]
            },
            "networkProfile": {
              "loadBalancerConfigurations": [
                {
                  "id": "[concat(variables('resourcePrefix'), 'Microsoft.Network/loadBalancers/', variables('lbName'))]",
                  "name": "[variables('lbName')]",
                  "properties": {
                    "frontendIPConfigurations": [
                      {
                        "name": "[variables('lbFEName')]",
                        "properties": {
                          "publicIPAddress": {
                            "id": "[concat(variables('resourcePrefix'), 'Microsoft.Network/publicIPAddresses/', parameters('publicIPName'))]"
                          }
                        }
                      }
                    ]
                  }
                }
              ]
            },
            "osProfile": {
              "secrets": [
                {
                  "sourceVault": {
                    "id": "/subscriptions/{subscription-id}/resourceGroups/{resource-group}/providers/Microsoft.KeyVault/vaults/{keyvault-name}"
                  },
                  "vaultCertificates": [
                    {
                      "certificateUrl": "https://{keyvault-name}.vault.azure.net:443/secrets/ContosoCertificate/{secret-id}"
                    }
                  ]
                }
              ]
            },
            "extensionProfile": {
              "extensions": [
                {
                  "name": "RDPExtension",
                  "properties": {
                    "autoUpgradeMinorVersion": true,
                    "publisher": "Microsoft.Windows.Azure.Extensions",
                    "type": "RDP",
                    "typeHandlerVersion": "1.2.1",
                    "settings": "<PublicConfig>\r\n <UserName>[Insert Username]</UserName>\r\n <Expiration>1/21/2022 12:00:00 AM</Expiration>\r\n</PublicConfig>",
                    "protectedSettings": "<PrivateConfig>\r\n <Password>[Insert Password]</Password>\r\n</PrivateConfig>"
                  }
                },
                {
                  "name": "Microsoft.Insights.VMDiagnosticsSettings_WebRole1",
                  "properties": {
                    "autoUpgradeMinorVersion": true,
                    "publisher": "Microsoft.Azure.Diagnostics",
                    "type": "PaaSDiagnostics",
                    "typeHandlerVersion": "1.5",
                    "settings": "[parameters('wadPublicConfig_WebRole1')]",
                    "protectedSettings": "[parameters('wadPrivateConfig_WebRole1')]",
                    "rolesAppliedTo": [
                      "WebRole1"
                  ]
                }
              }
            ]
          }
        }
       }
      ]
    }
    ```

8. Wdróż szablon i plik parametrów (Definiowanie parametrów w pliku szablonu), aby utworzyć wdrożenie usługi w chmurze (obsługa rozszerzona). Zapoznaj się z tymi [przykładowymi szablonami](https://github.com/Azure-Samples/cloud-services-extended-support) zgodnie z potrzebami.

    ```powershell
    New-AzResourceGroupDeployment -ResourceGroupName "ContosOrg" -TemplateFile "file path to your template file" -TemplateParameterFile "file path to your parameter file"
    ```

## <a name="next-steps"></a>Następne kroki 

- Zapoznaj się z [często zadawanymi pytaniami](faq.md) dotyczącymi Cloud Services (obsługa rozszerzona).
- Wdróż usługę w chmurze (obsługę rozszerzoną) przy użyciu [Azure Portal](deploy-portal.md), [programu PowerShell](deploy-powershell.md), [szablonu](deploy-template.md) lub [programu Visual Studio](deploy-visual-studio.md).
- Odwiedź [repozytorium przykładów Cloud Services (obsługa rozszerzona)](https://github.com/Azure-Samples/cloud-services-extended-support)

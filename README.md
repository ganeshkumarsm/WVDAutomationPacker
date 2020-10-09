# WVDAutomationPacker
Automated WVD via both Build and Release Pipelines

1. Refer: https://xenithit.blogspot.com/2020/03/how-to-deploy-windows-virtual-dekstop.html

2. Modify ARM template (Removed Add to workspace (seems there is a bug with ADO).

3. Dont forget to save variables (Build Pipeline) and load variables into Release Pipeline.

4. Release Pipeline: Override template parameters with the line below
-nestedTemplatesLocation "https://catalogartifact.azureedge.net/publicartifacts/Microsoft.Hostpool-ARM-1.0.15-preview/" -artifactsLocation "https://wvdportalstorageblob.blob.core.windows.net/galleryartifacts/Configuration_9-11-2020.zip" -hostpoolName "WVDPool2" -hostpoolFriendlyName "" -hostpoolDescription "Created through the WVD extension" -location "eastus2" -workSpaceName "" -workspaceLocation "" -workspaceResourceGroup "" -allApplicationGroupReferences "" -addToWorkspace false -administratorAccountUsername "azureuser@wvdlab.in" -administratorAccountPassword ChangeMe123456 -createAvailabilitySet true -vmResourceGroup "" -vmLocation "eastus2" -vmSize "Standard_B2ms" -vmNumberOfInstances 1 -vmNamePrefix "VM-WVD-$(Release.ReleaseName)" -vmImageType "CustomImage" -vmGalleryImageOffer "" -vmGalleryImagePublisher "" -vmGalleryImageSKU "" -vmImageVhdUri "" -vmCustomImageSourceId "/subscriptions/52357355-aaab-4d65-a9c0-aa285d794ff4/resourceGroups/myPackerGroup/providers/Microsoft.Compute/images/$(BuildImage)" -vmDiskType "StandardSSD_LRS" -vmUseManagedDisks true -storageAccountResourceGroupName "" -existingVnetName "VNet-Azureeastus2" -existingSubnetName "Subnet-WVD" -virtualNetworkResourceGroupName "ADonAzureVMss" -usePublicIP false -publicIpAddressSku "Basic" -publicIpAddressType "Dynamic" -createNetworkSecurityGroup false -networkSecurityGroupId "" -networkSecurityGroupRules [] -hostpoolType "Pooled" -personalDesktopAssignmentType "" -maxSessionLimit 99999 -loadBalancerType "BreadthFirst" -customRdpProperty "" -vmTemplate "{\"domain\":\"wvdlab.in\",\"galleryImageOffer\":null,\"galleryImagePublisher\":null,\"galleryImageSKU\":null,\"imageType\":\"CustomImage\",\"imageUri\":null,\"customImageId\":\"/subscriptions/52357355-aaab-4d65-a9c0-aa285d794ff4/resourceGroups/aibwinsig/providers/Microsoft.Compute/galleries/myIBSIG/images/winSvrimage\",\"namePrefix\":\"WVDHost\",\"osDiskType\":\"StandardSSD_LRS\",\"useManagedDisks\":true,\"vmSize\":{\"id\":\"Standard_D2s_v3\",\"cores\":2,\"ram\":8},\"galleryItemId\":null}" -tokenExpirationTime "2020-10-11T18:49:32.605Z" -hostpoolTags {} -applicationGroupTags {} -availabilitySetTags {} -networkInterfaceTags {} -networkSecurityGroupTags {} -publicIPAddressTags {} -virtualMachineTags {} -imageTags {} -apiVersion "2019-12-10-preview" -deploymentId "c23fd5df-7f66-40bf-8819-0040acf5f028" -validationEnvironment false -preferredAppGroupType "Desktop" -ouPath "OU=WVD,DC=wvdlab,DC=in" -domain "wvdlab.in"

5. Dont forget to change the Token expiry time in the override parameters

6. Check the Resource Group for Deployments for the release pipeline

7. Monitor the time spent for each time
  a. For Build - It took around 15 minutes
  b. For Release - It took around 8 minutes

8. Add the Application Group to WVD Workspace manuallly

9. Assign the Appication Group to Users manually

10. Change the Application Group to any identifiable name (to identify the release pipeline) if required.

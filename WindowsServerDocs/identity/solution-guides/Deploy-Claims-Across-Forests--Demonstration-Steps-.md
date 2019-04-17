---
ms.assetid: 846c3680-b321-47da-8302-18472be42421
title: Deploy Claims Across Forests (Demonstration Steps)
description: 
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adds
ms.openlocfilehash: 3bab7a396061ecae8a187cc6986d6d026a9e4b32
ms.sourcegitcommit: db290fa07e9d50686667bfba3969e20377548504
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 12/12/2017
---
# <a name="deploy-claims-across-forests-demonstration-steps"></a>Deploy Claims Across Forests (Demonstration Steps)

>Область применения: Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

In this topic, we'll cover a basic scenario that explains how to configure claims transformations between trusting and trusted forests. You will learn how claims transformation policy objects can be created and linked to the trust on the trusting forest and the trusted forest. You will then validate the scenario.  
  
## <a name="scenario-overview"></a>Scenario overview  
Предоставляет корпорации adatum финансовых услуг Contoso, Ltd. Каждый квартал бухгалтеры Adatum скопируйте их электронные таблицы учетной записи в папку на файловом сервере, находящегося по адресу Contoso, Ltd. Существует двустороннее доверие настроить из Contoso для Adatum. Contoso, Ltd. хочет Защита общей папки, чтобы только Adatum сотрудники получают доступ к удаленной общей папке.  
  
In this scenario:  
  
1.  [Set up the prerequisites and the test environment](Deploy-Claims-Across-Forests--Demonstration-Steps-.md#BKMK_1.1)  
  
2.  [Set up claims transformation on trusted forest (Adatum)](Deploy-Claims-Across-Forests--Demonstration-Steps-.md#BKMK_3)  
  
3.  [Set up claims transformation in the trusting forest (Contoso)](Deploy-Claims-Across-Forests--Demonstration-Steps-.md#BKMK_4)  
  
4.  [Validate the scenario](Deploy-Claims-Across-Forests--Demonstration-Steps-.md#BKMK_5)  
  
## <a name="BKMK_1.1"></a>Set up the prerequisites and the test environment  
The test configuration involves setting up two forests: Adatum Corporation and Contoso, Ltd, and having a two-way trust between Contoso and Adatum. "adatum.com" is the trusted forest and "contoso.com" is the trusting forest.  
  
The claims transformation scenario demonstrates transformation of a claim in the trusted forest to a claim in the trusting forest. To do this, you need to set up a new forest called adatum.com and populate the forest with a test user with a company value of 'Adatum'. You then have to set up a two-way trust between contoso.com and adatum.com.  
  
> [!IMPORTANT]  
> When setting up the Contoso and Adatum forests, you must ensure that both the root domains are at the Windows Server 2012 Domain Functional Level for claims transformation to work.  
  
You need to set up the following for the lab. These procedures are explained in detail in [Appendix B: Setting Up the Test Environment](Appendix-B--Setting-Up-the-Test-Environment.md)  
  
You need to implement the following procedures to set up the lab for this scenario:  
  
1.  [Set Adatum as trusted forest to Contoso](Appendix-B--Setting-Up-the-Test-Environment.md)  
  
2.  [Create the 'Company' claim type on Contoso](Appendix-B--Setting-Up-the-Test-Environment.md#BKMK_2.8)  
  
3.  [Enable the 'Company' resource property on Contoso](Appendix-B--Setting-Up-the-Test-Environment.md#BKMK_2.55)  
  
4.  [Create the central access rule](Appendix-B--Setting-Up-the-Test-Environment.md#BKMK_2.9)  
  
5.  [Create the central access policy](Appendix-B--Setting-Up-the-Test-Environment.md#BKMK_2.10)  
  
6.  [Publish the new policy through Group Policy](Appendix-B--Setting-Up-the-Test-Environment.md#BKMK_2.11)  
  
7.  [Create the Earnings folder on the file server](Appendix-B--Setting-Up-the-Test-Environment.md#BKMK_2.12)  
  
8.  [Set classification and apply the central access policy on the new folder](Appendix-B--Setting-Up-the-Test-Environment.md#BKMK_2.13)  
  
Use the following information to complete this scenario:  
  
|Objects|Сведения о|  
|-----------|-----------|  
|Пользователи|Jeff Low, Contoso|  
|User claims on Adatum and Contoso|ID: ad://ext/Company:ContosoAdatum,<br /><br />Source attribute: company<br /><br />Suggested values: Contoso, Adatum **Important:** You must set the ID on the 'Company' claim type on both Contoso and Adatum to be the same for the claims transformation to work.|  
|Central access rule on Contoso|AdatumEmployeeAccessRule|  
|Central access policy on Contoso|Adatum Only Access Policy|  
|Claims Transformation policies on Adatum and Contoso|DenyAllExcept Company|  
|File folder on Contoso|D:\EARNINGS|  
  
## <a name="BKMK_3"></a>Set up claims transformation on trusted forest (Adatum)  
In this step you create a transformation policy in Adatum to deny all claims except 'Company' to pass to Contoso.  
  
The Active Directory module for Windows PowerShell provides the **DenyAllExcept** argument, which drops everything except the specified claims in the transformation policy.  
  
To set up a claims transformation, you need to create a claims transformation policy and link it between the trusted and trusting forests.  
  
### <a name="BKMK_2.2"></a>Create a claims transformation policy in Adatum  
  
##### <a name="to-create-a-transformation-policy-adatum-to-deny-all-claims-except-company"></a>To create a transformation policy Adatum to deny all claims except 'Company'  
  
1.  Sign in to the domain controller, adatum.com as Administrator with the password **pass@word1**.  
  
2.  Open an elevated command prompt in Windows PowerShell, and type the following:  
  
    ```  
    New-ADClaimTransformPolicy `  
    -Description:"Claims transformation policy to deny all claims except Company"`  
    -Name:"DenyAllClaimsExceptCompanyPolicy" `  
    -DenyAllExcept:company `  
    -Server:"adatum.com" `  
  
    ```  
  
### <a name="BKMK_2.3"></a>Set a claims transformation link on Adatum's trust domain object  
In this step, you apply the newly created claims transformation policy on Adatum's trust domain object for Contoso.  
  
##### <a name="to-apply-the-claims-transformation-policy"></a>To apply the claims transformation policy  
  
1.  Sign in to the domain controller, adatum.com as Administrator with the password  **pass@word1**.  
  
2.  Open an elevated command prompt in Windows PowerShell, and type the following:  
  
    ```  
  
      Set-ADClaimTransformLink `  
    -Identity:"contoso.com" `  
    -Policy:"DenyAllClaimsExceptCompanyPolicy" `  
    '"TrustRole:Trusted `  
  
    ```  
  
## <a name="BKMK_4"></a>Set up claims transformation in the trusting forest (Contoso)  
In this step you create a claims transformation policy in Contoso (the trusting forest) to deny all claims except 'Company.' You need to create a claims transformation policy and link it to the forest trust.  
  
### <a name="BKMK_4.1"></a>Create a claims transformation policy in Contoso  
  
##### <a name="to-create-a-transformation-policy-adatum-to-deny-all-except-company"></a>To create a transformation policy Adatum to deny all except 'Company'  
  
1.  Sign in to the domain controller, contoso.com as Administrator with the password **pass@word1**.  
  
2.  Open an elevated command prompt in Windows PowerShell and type the following:  
  
    ```  
    New-ADClaimTransformPolicy `  
    -Description:"Claims transformation policy to deny all claims except company" `  
    -Name:"DenyAllClaimsExceptCompanyPolicy" `  
    -DenyAllExcept:company `  
    -Server:"contoso.com" `  
  
    ```  
  
### <a name="BKMK_4.2"></a>Set a claims transformation link on Contoso's trust domain object  
На этом шаге вы примените только что созданный политики преобразования утверждений на объекте contoso.com доверия домена для Adatum разрешить «Компания» передаваться contoso.com. Объект доверия домена называется adatum.com.  
  
##### <a name="to-set-the-claims-transformation-policy"></a>To set the claims transformation policy  
  
1.  Sign in to the domain controller, contoso.com as Administrator with the password **pass@word1**.  
  
2.  Open an elevated command prompt in Windows PowerShell and type the following:  
  
    ```  
  
      Set-ADClaimTransformLink   
    -Identity:"adatum.com" `  
    -Policy:"DenyAllClaimsExceptCompanyPolicy" `  
    -TrustRole:Trusting `  
  
    ```  
  
## <a name="BKMK_5"></a>Validate the scenario  
In this step you try to access the D:\EARNINGS folder that was set up on the file server FILE1 to validate that the user has access to the shared folder.  
  
#### <a name="to-ensure-that-the-adatum-user-can-access-the-shared-folder"></a>To ensure that the Adatum user can access the shared folder  
  
1.  Sign in to the Client machine, CLIENT1 as Jeff Low with the password **pass@word1**.  
  
2.  Browse to the folder \\\FILE1.contoso.com\Earnings.  
  
3.  Jeff Low should be able to access the folder.  
  
## <a name="additional-scenarios-for-claims-transformation-policies"></a>Additional scenarios for claims transformation policies  
Following is a list of additional common cases in claims transformation.  
  
|Сценарий|Политики|  
|------------|----------|  
|Allow all claims that come from Adatum to go through to Contoso Adatum|Кода. <br />New-ADClaimTransformPolicy \`<br /> -Description:"Claims transformation policy to allow all claims" \`<br />-Name:"AllowAllClaimsPolicy" \`<br />-AllowAll \`<br />-Server:"contoso.com" \`<br />Set-ADClaimTransformLink \`<br />-Identity:"adatum.com" \`<br />-Policy:"AllowAllClaimsPolicy" \`<br />-TrustRole:Trusting \`<br />-Server:"contoso.com" `|  
|Deny all claims that come from Adatum to go through to Contoso Adatum|Кода. <br />New-ADClaimTransformPolicy \`<br />-Description:"Claims transformation policy to deny all claims" \`<br />-Name:"DenyAllClaimsPolicy" \`<br /> -DenyAll \`<br />-Server:"contoso.com" \`<br />Set-ADClaimTransformLink \`<br />-Identity:"adatum.com" \`<br />-Policy:"DenyAllClaimsPolicy" \`<br />-TrustRole:Trusting \`<br />-Server:"contoso.com"`|  
|Allow all claims that come from Adatum except "Company" and "Department" to go through to Contoso Adatum|Код <br />- New-ADClaimTransformationPolicy \`<br />-Description:"Claims transformation policy to allow all claims except company and department" \`<br /> -Name:"AllowAllClaimsExceptCompanyAndDepartmentPolicy" \`<br />-AllowAllExcept:company,department \`<br />-Server:"contoso.com" \`<br />Set-ADClaimTransformLink \`<br /> -Identity:"adatum.com" \`<br />-Policy:"AllowAllClaimsExceptCompanyAndDepartmentPolicy" \`<br /> -TrustRole:Trusting \`<br />-Server:"contoso.com" `|  
  
## <a name="BKMK_Links"></a>См. также:  
  
-   For a list of all Windows PowerShell cmdlets that are available for claims transformation, see [Active Directory PowerShell Cmdlet Reference](https://go.microsoft.com/fwlink/?LinkId=243150).  
  
-   For advanced tasks that involve export and import of DAC configuration information between two forests, use the [Dynamic Access Control PowerShell Reference](https://go.microsoft.com/fwlink/?LinkId=243150)  
  
-   [Развертывание утверждений между лесами](Deploy-Claims-Across-Forests.md)  
  
-   [Язык правил преобразования утверждений](Claims-Transformation-Rules-Language.md)  
  
-   [Динамического контроля доступа: Обзор сценария](Dynamic-Access-Control--Scenario-Overview.md)  
  

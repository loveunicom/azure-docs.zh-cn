---
title: 教程：Azure Active Directory 与 OpsGenie 集成 | Microsoft 文档
description: 了解如何在 Azure Active Directory 和 OpsGenie 之间配置单一登录。
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 41b59b22-a61d-4fe6-ab0d-6c3991d1375f
ms.service: active-directory
ms.component: saas-app-tutorial
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/16/2018
ms.author: jeedes
ms.openlocfilehash: 715035072ddc2ceb087d003dd5da5bc47572e9b9
ms.sourcegitcommit: 1d850f6cae47261eacdb7604a9f17edc6626ae4b
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/02/2018
ms.locfileid: "39444345"
---
# <a name="tutorial-azure-active-directory-integration-with-opsgenie"></a>教程：Azure Active Directory 与 OpsGenie 的集成

本教程介绍如何将 OpsGenie 与 Azure Active Directory (Azure AD) 集成。

将 OpsGenie 与 Azure AD 集成具有以下优势：

- 可在 Azure AD 中控制谁有权访问 OpsGenie
- 可以让用户通过其 Azure AD 帐户自动登录到 OpsGenie（单一登录）
- 可以在一个中心位置（即 Azure 门户）管理帐户

如需了解有关 SaaS 应用与 Azure AD 集成的详细信息，请参阅 [Azure Active Directory 的应用程序访问与单一登录是什么](../manage-apps/what-is-single-sign-on.md)。

## <a name="prerequisites"></a>先决条件

若要配置 Azure AD 与 OpsGenie 的集成，需备齐以下项目：

- Azure AD 订阅
- 启用了 OpsGenie 单一登录的订阅

> [!NOTE]
> 为了测试本教程中的步骤，我们不建议使用生产环境。

测试本教程中的步骤应遵循以下建议：

- 除非必要，请勿使用生产环境。
- 如果没有 Azure AD 试用环境，可以在[此处](https://azure.microsoft.com/pricing/free-trial/)获取一个月的试用版。

## <a name="scenario-description"></a>方案描述
在本教程中，将在测试环境中测试 Azure AD 单一登录。 本教程中概述的方案包括两个主要构建基块：

1. 从库中添加 OpsGenie
1. 配置和测试 Azure AD 单一登录

## <a name="adding-opsgenie-from-the-gallery"></a>从库中添加 OpsGenie
要通过配置将 OpsGenie 集成到 Azure AD 中，需从库将 OpsGenie 添加到托管式 SaaS 应用的列表中。

**若要从库添加 OpsGenie，请执行以下步骤：**

1. 在 **[Azure 门户](https://portal.azure.com)** 的左侧导航面板中，单击“Azure Active Directory”图标。 

    ![Active Directory][1]

1. 导航到“企业应用程序”。 然后转到“所有应用程序”。

    ![应用程序][2]
    
1. 若要添加新应用程序，请单击对话框顶部的“新建应用程序”按钮。

    ![应用程序][3]

1. 在搜索框中，键入“OpsGenie”。

    ![创建 Azure AD 测试用户](./media/opsgenie-tutorial/tutorial_opsgenie_search.png)

1. 在结果面板中，选择“OpsGenie”，然后单击“添加”按钮添加该应用程序。

    ![创建 Azure AD 测试用户](./media/opsgenie-tutorial/tutorial_opsgenie_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a>配置和测试 Azure AD 单一登录
在本部分中，基于一个名为“Britta Simon”的测试用户使用 OpsGenie 配置和测试 Azure AD 单一登录。

若要运行单一登录，Azure AD 需要知道与 Azure AD 用户相对应的 OpsGenie 用户。 换句话说，需要建立 Azure AD 用户与 OpsGenie 中相关用户之间的关联关系。

可通过将 Azure AD 中“用户名”的值指定为 OpsGenie 中“用户名”的值来建立此链接关系。

若要使用 OpsGenie 配置和测试 Azure AD 单一登录，需完成以下构建基块：

1. **[配置 Azure AD 单一登录](#configuring-azure-ad-single-sign-on)** - 让用户使用此功能。
1. **[创建 Azure AD 测试用户](#creating-an-azure-ad-test-user)** - 使用 Britta Simon 测试 Azure AD 单一登录。
1. [创建 OpsGenie 测试用户](#creating-a-opsgenie-test-user) - 在 OpsGenie 中创建 Britta Simon 的对应用户，将其链接到用户的 Azure AD 表示形式。
1. **[分配 Azure AD 测试用户](#assigning-the-azure-ad-test-user)** - 让 Britta Simon 使用 Azure AD 单一登录。
1. **[测试单一登录](#testing-single-sign-on)** - 验证配置是否正常工作。

### <a name="configuring-azure-ad-single-sign-on"></a>配置 Azure AD 单一登录

在本部分中，将在 Azure 门户中启用 Azure AD 单一登录并在 OpsGenie 应用程序中配置单一登录。

**若要通过 OpsGenie 配置 Azure AD 单一登录，请执行以下步骤：**

1. 在 Azure 门户中的 OpsGenie 应用程序集成页上，单击“单一登录”。

    ![配置单一登录][4]

1. 在“单一登录”对话框中，选择“基于 SAML 的单一登录”作为“模式”以启用单一登录。
 
    ![配置单一登录](./media/opsgenie-tutorial/tutorial_opsgenie_samlbase.png)

1. 在“OpsGenie 域和 URL”部分，执行以下步骤：

    ![配置单一登录](./media/opsgenie-tutorial/tutorial_opsgenie_url.png)

    在“登录 URL”文本框中，键入 URL：`https://app.opsgenie.com/auth/login`

1. 在“SAML 签名证书”部分上，单击”复制”按钮来复制**应用联合元数据 URL**，并将其粘贴到记事本。

    ![证书下载链接](./media/opsgenie-tutorial/tutorial_opsgenie_certificate.png)

1. 单击“保存”按钮。

    ![配置单一登录](./media/opsgenie-tutorial/tutorial_general_400.png)

1. 在“OpsGenie 配置”部分，单击“配置 OpsGenie”打开“配置登录”窗口。 从“快速参考”部分中复制“SAML 单一登录服务 URL”。

    ![配置单一登录](./media/opsgenie-tutorial/tutorial_opsgenie_configure.png)

1. 打开另一个浏览器实例，并以管理员身份登录到 OpsGenie。

1. 单击“设置”，并单击“单一登录”选项卡。
   
    ![OpsGenie 单一登录](./media/opsgenie-tutorial/tutorial_opsgenie_06.png)

1. 若要启用 SSO，请选择“启用”。 
   
    ![OpsGenie 设置](./media/opsgenie-tutorial/tutorial_opsgenie_07.png) 

1. 在“提供程序”部分，单击“Azure Active Directory”选项卡。
   
    ![OpsGenie 设置](./media/opsgenie-tutorial/tutorial_opsgenie_08.png) 

1. 在“Azure Active Directory”对话框页上，执行以下步骤：
   
    ![OpsGenie 设置](./media/opsgenie-tutorial/tutorial_opsgenie_09.png)
    
    a. 在“SAML 2.0 终结点”文本框中，粘贴从 Azure 门户复制的“单一登录服务 URL”值。
    
    b. 在“元数据 URL:”文本框中，粘贴从 Azure 门户复制的**应用联合元数据 URL**值。
    
    c. 单击“保存更改”。

### <a name="creating-an-azure-ad-test-user"></a>创建 Azure AD 测试用户
本部分的目的是在 Azure 门户中创建名为 Britta Simon 的测试用户。

![创建 Azure AD 用户][100]

**若要在 Azure AD 中创建测试用户，请执行以下步骤：**

1. 在 **Azure 门户**的左侧导航窗格中，单击“Azure Active Directory”图标。

    ![创建 Azure AD 测试用户](./media/opsgenie-tutorial/create_aaduser_01.png) 

1. 若要显示用户列表，请转到“用户和组”，单击“所有用户”。
    
    ![创建 Azure AD 测试用户](./media/opsgenie-tutorial/create_aaduser_02.png) 

1. 若要打开“用户”对话框，请在对话框顶部单击“添加”。
 
    ![创建 Azure AD 测试用户](./media/opsgenie-tutorial/create_aaduser_03.png) 

1. 在“用户”对话框页上，执行以下步骤：
 
    ![创建 Azure AD 测试用户](./media/opsgenie-tutorial/create_aaduser_04.png) 

    a. 在“名称”文本框中，键入 **BrittaSimon**。

    b. 在“用户名”文本框中，键入 BrittaSimon 的“电子邮件地址”。

    c. 选择“显示密码”并记下“密码”的值。

    d. 单击“创建”。
 
### <a name="creating-a-opsgenie-test-user"></a>创建 OpsGenie 测试用户

本部分的目的是在 OpsGenie 中创建名为“Britta Simon”的用户。 

1. 在 Web 浏览器窗口中，以管理员身份登录到 OpsGenie 租户。

1. 单击左侧面板中的“用户”，导航到“用户”列表。
   
   ![OpsGenie 设置](./media/opsgenie-tutorial/tutorial_opsgenie_10.png) 

1. 单击“添加用户”。

1. 在“添加用户”对话框中，执行以下步骤：
   
   ![OpsGenie 设置](./media/opsgenie-tutorial/tutorial_opsgenie_11.png)
   
   a. 在“电子邮件”文本框中，键入 Britta Simon 在 Azure Active Directory 中填写的电子邮件地址。
   
   b. 在“完整名称”文本框中，键入“Britta Simon”。
   
   c. 单击“ **保存**”。 

>[!NOTE]
>Britta 会收到一封电子邮件，其中包含配置文件设置说明。

### <a name="assigning-the-azure-ad-test-user"></a>分配 Azure AD 测试用户

在本部分中，通过授予 Britta Simon 访问 OpsGenie 的权限，允许她使用 Azure 单一登录。

![分配用户][200] 

**要将 Britta Simon 分配到 OpsGenie，请执行以下步骤：**

1. 在 Azure 门户中打开应用程序视图，导航到目录视图，接着转到“企业应用程序”，并单击“所有应用程序”。

    ![分配用户][201] 

1. 在应用程序列表中，选择“OpsGenie”。

    ![配置单一登录](./media/opsgenie-tutorial/tutorial_opsgenie_app.png) 

1. 在左侧菜单中，单击“用户和组”。

    ![分配用户][202] 

1. 单击“添加”按钮。 然后在“添加分配”对话框中选择“用户和组”。

    ![分配用户][203]

1. 在“用户和组”对话框的“用户”列表中，选择“Britta Simon”。

1. 在“用户和组”对话框中单击“选择”按钮。

1. 在“添加分配”对话框中单击“分配”按钮。
    
### <a name="testing-single-sign-on"></a>测试单一登录

本部分旨在使用“访问面板”测试 Azure AD SSO 配置。

单击访问面板中的“OpsGenie”磁贴时，用户就会自动登录到 OpsGenie 应用程序。

## <a name="additional-resources"></a>其他资源

* [有关如何将 SaaS 应用与 Azure Active Directory 集成的教程列表](tutorial-list.md)
* [什么是使用 Azure Active Directory 的应用程序访问和单一登录？](../manage-apps/what-is-single-sign-on.md)

<!--Image references-->

[1]: ./media/opsgenie-tutorial/tutorial_general_01.png
[2]: ./media/opsgenie-tutorial/tutorial_general_02.png
[3]: ./media/opsgenie-tutorial/tutorial_general_03.png
[4]: ./media/opsgenie-tutorial/tutorial_general_04.png

[100]: ./media/opsgenie-tutorial/tutorial_general_100.png

[200]: ./media/opsgenie-tutorial/tutorial_general_200.png
[201]: ./media/opsgenie-tutorial/tutorial_general_201.png
[202]: ./media/opsgenie-tutorial/tutorial_general_202.png
[203]: ./media/opsgenie-tutorial/tutorial_general_203.png


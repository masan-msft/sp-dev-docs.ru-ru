---
title: How to Programmatically Add an Excel Web Access Web Part to a Page
ms.date: 09/25/2017
keywords: how to,howdoi,howto,webpart
f1_keywords: how to,howdoi,howto,webpart
ms.prod: sharepoint
ms.assetid: 858bb0f6-654a-4f12-ba0b-4776bda5ff6d
ms.openlocfilehash: 85020bb527853d4b1b51910cf61d452f4e9ab5c6
ms.sourcegitcommit: 1cae27d85ee691d976e2c085986466de088f526c
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/13/2017
---
# <a name="how-to-programmatically-add-an-excel-web-access-web-part-to-a-page"></a><span data-ttu-id="b338c-103">How to: Programmatically Add an Excel Web Access Web Part to a Page</span><span class="sxs-lookup"><span data-stu-id="b338c-103">How to: Programmatically Add an Excel Web Access Web Part to a Page</span></span>

<span data-ttu-id="b338c-p101">This example shows how to programmatically add an Веб-клиент Excel Web Part to a SharePoint page. It also shows you how to display an Excel workbook programmatically in an Веб-клиент Excel Web Part.</span><span class="sxs-lookup"><span data-stu-id="b338c-p101">This example shows how to programmatically add an Excel Web Access Web Part to a SharePoint page. It also shows you how to display an Excel workbook programmatically in an Excel Web Access Web Part.</span></span> 
  
    
    

<span data-ttu-id="b338c-106">The following project uses Microsoft Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="b338c-106">The following project uses Microsoft Visual Studio.</span></span>
> <span data-ttu-id="b338c-107">**Примечание:** В зависимости от версии Visual Studio и среды разработки Visual Studio (IDE) параметры, которые вы используете, процесса и действия, для создания проекта Visual Studio может немного отличаться от процедуры, приведенные в этом разделе.</span><span class="sxs-lookup"><span data-stu-id="b338c-107">**Note:** Depending on the Visual Studio version and the Visual Studio integrated development environment (IDE) settings that you are using, the process and steps to create a Visual Studio project could be slightly different from the procedures shown in this topic.</span></span> 
  
    
    


> <span data-ttu-id="b338c-108">**Примечание:** Предполагается, что уже создан в библиотеке документов SharePoint и был очень надежного расположения.</span><span class="sxs-lookup"><span data-stu-id="b338c-108">**Note:** It is assumed that you have already created a SharePoint document library and made it a trusted location.</span></span> <span data-ttu-id="b338c-109">Дополнительные сведения можно [как: надежного расположения](how-to-trust-a-location.md).</span><span class="sxs-lookup"><span data-stu-id="b338c-109">For more information, see  [How to: Trust a Location](how-to-trust-a-location.md).</span></span> 
  
    
    


## <a name="adding-a-reference"></a><span data-ttu-id="b338c-110">Adding a Reference</span><span class="sxs-lookup"><span data-stu-id="b338c-110">Adding a Reference</span></span>

<span data-ttu-id="b338c-p103">The following steps show how to locate Microsoft.Office.Excel.WebUI.dll and how to add a reference to it. Repeat for Microsoft.Office.Excel.WebUI.Internal.dll and Microsoft.SharePoint.dll.</span><span class="sxs-lookup"><span data-stu-id="b338c-p103">The following steps show how to locate Microsoft.Office.Excel.WebUI.dll and how to add a reference to it. Repeat for Microsoft.Office.Excel.WebUI.Internal.dll and Microsoft.SharePoint.dll.</span></span>
  
    
    

> <span data-ttu-id="b338c-113">**Примечание:** Предполагается, что уже копирования Microsoft.Office.Excel.WebUI.dll и Microsoft.Office.Excel.WebUI.Internal.dll из глобального кэша сборок в папке по выбору.</span><span class="sxs-lookup"><span data-stu-id="b338c-113">**Note:** It is assumed that you have already copied Microsoft.Office.Excel.WebUI.dll and Microsoft.Office.Excel.WebUI.Internal.dll from the global assembly cache to a folder of your choice.</span></span> <span data-ttu-id="b338c-114">Дополнительные сведения о том, как найти и копирование Microsoft.Office.Excel.WebUI.dll и Microsoft.Office.Excel.WebUI.Internal.dll можно [как: найдите и копии Microsoft.Office.Excel.WebUI.dll и Microsoft.Office.Excel.WebUI.Internal.dll](how-to-locate-and-copy-microsoft-office-excel-webui-dll-and-microsoft-office-exc.md) .</span><span class="sxs-lookup"><span data-stu-id="b338c-114">For more information about how to locate and copy Microsoft.Office.Excel.WebUI.dll and Microsoft.Office.Excel.WebUI.Internal.dll, see  [How to: Locate and Copy Microsoft.Office.Excel.WebUI.dll and Microsoft.Office.Excel.WebUI.Internal.dll](how-to-locate-and-copy-microsoft-office-excel-webui-dll-and-microsoft-office-exc.md).</span></span> 
  
    
    


### <a name="to-add-a-reference-to-microsoftofficeexcelwebuidll"></a><span data-ttu-id="b338c-115">To add a reference to Microsoft.Office.Excel.WebUI.dll</span><span class="sxs-lookup"><span data-stu-id="b338c-115">To add a reference to Microsoft.Office.Excel.WebUI.dll</span></span>


1. <span data-ttu-id="b338c-116">On the **Project** menu, click **Add Reference**.</span><span class="sxs-lookup"><span data-stu-id="b338c-116">On the **Project** menu, click **Add Reference**.</span></span>
    
  
2. <span data-ttu-id="b338c-117">In the **Add Reference** dialog box, click **Browse**.</span><span class="sxs-lookup"><span data-stu-id="b338c-117">In the **Add Reference** dialog box, click **Browse**.</span></span>
    
    > <span data-ttu-id="b338c-118">**Примечание:** Можно также открыть диалоговое окно **Добавить ссылку** в области **Обозреватель решений** , щелкнув правой кнопкой мыши **ссылки** и выберите команду **Добавить ссылку**.</span><span class="sxs-lookup"><span data-stu-id="b338c-118">**Note:** You can also open the **Add Reference** dialog box in the **Solution Explorer** pane by right-clicking **References** and selecting **Add Reference**.</span></span> 
3. <span data-ttu-id="b338c-119">Browse to the location of Microsoft.Office.Excel.WebUI.dll.</span><span class="sxs-lookup"><span data-stu-id="b338c-119">Browse to the location of Microsoft.Office.Excel.WebUI.dll.</span></span>
    
  
4. <span data-ttu-id="b338c-120">Select Microsoft.Office.Excel.WebUI.dll, and then click **OK**.</span><span class="sxs-lookup"><span data-stu-id="b338c-120">Select Microsoft.Office.Excel.WebUI.dll, and then click **OK**.</span></span>
    
  
5. <span data-ttu-id="b338c-p105">Click **Add Reference**. A reference to Microsoft.Office.Excel.WebUI.dll is added to your project.</span><span class="sxs-lookup"><span data-stu-id="b338c-p105">Click **Add Reference**. A reference to Microsoft.Office.Excel.WebUI.dll is added to your project.</span></span>
    
  

## <a name="instantiating-a-web-part"></a><span data-ttu-id="b338c-123">Instantiating a Web Part</span><span class="sxs-lookup"><span data-stu-id="b338c-123">Instantiating a Web Part</span></span>


### <a name="to-instantiate-the-excel-web-access-web-part"></a><span data-ttu-id="b338c-124">To instantiate the Excel Web Access Web Part</span><span class="sxs-lookup"><span data-stu-id="b338c-124">To instantiate the Excel Web Access Web Part</span></span>


1. <span data-ttu-id="b338c-125">Add the Microsoft.Office.Excel.WebUI namespace as a directive to your code, so that when you use the types in this namespace, you do not need to fully qualify them:</span><span class="sxs-lookup"><span data-stu-id="b338c-125">Add the Microsoft.Office.Excel.WebUI namespace as a directive to your code, so that when you use the types in this namespace, you do not need to fully qualify them:</span></span>
    
```cs
  
using Microsoft.Office.Excel.WebUI;
```


```VB.net
  Imports Microsoft.Office.Excel.WebUI
```

2. <span data-ttu-id="b338c-126">Instantiate and initialize the Веб-клиент Excel Web Part, as follows:</span><span class="sxs-lookup"><span data-stu-id="b338c-126">Instantiate and initialize the Excel Web Access Web Part, as follows:</span></span>
    
```cs
  
 ExcelWebRenderer ewaWebPart = new ExcelWebRenderer();
```


```VB.net
  
Dim ewaWebPart As New ExcelWebRenderer()
```


### <a name="to-display-a-workbook-programmatically"></a><span data-ttu-id="b338c-127">To display a workbook programmatically</span><span class="sxs-lookup"><span data-stu-id="b338c-127">To display a workbook programmatically</span></span>


1. <span data-ttu-id="b338c-p106">In this example, the **AddWebPart** method takes in the path to an Excel workbook location as an argument. The user provides the path by typing in a Windows Forms text box and clicking a button.</span><span class="sxs-lookup"><span data-stu-id="b338c-p106">In this example, the **AddWebPart** method takes in the path to an Excel workbook location as an argument. The user provides the path by typing in a Windows Forms text box and clicking a button.</span></span>
    
    <span data-ttu-id="b338c-130">**Sample code provided by:** Daniel Mullowney, Microsoft Corporation</span><span class="sxs-lookup"><span data-stu-id="b338c-130">**Sample code provided by:** Daniel Mullowney, Microsoft Corporation</span></span>
    


```cs
  
public bool AddWebPart(string sitename, string book)
{
...
}
            private void AddEWAButton_Click(object sender, 
                EventArgs e)
            {
                siteurl = textBox1.Text;
                bookuri = textBox2.Text;
                succeeded = AddWebPart(siteurl, bookuri);
                if (succeeded)
                {
                    MessageBox.Show(
                        success,
                        appname,
                        MessageBoxButtons.OK,
                        MessageBoxIcon.Information);
                    progressBar1.Value = 1;
                }
            }
```




```VB.net
  
Public Function AddWebPart(ByVal sitename As String, ByVal book As String) As Boolean
...
End Function
Private Sub AddEWAButton_Click(ByVal sender As Object, ByVal e As EventArgs)
        siteurl = textBox1.Text
        bookuri = textBox2.Text
        succeeded = AddWebPart(siteurl, bookuri)
        If succeeded Then
            MessageBox.Show(success, appname, MessageBoxButtons.OK, MessageBoxIcon.Information)
            progressBar1.Value = 1
        End If
End Sub
```


    > **Important:**
      > Ensure that the location where the workbook is saved is a trusted location. 
2. <span data-ttu-id="b338c-131">You can display an Excel workbook programmatically by using the following code.</span><span class="sxs-lookup"><span data-stu-id="b338c-131">You can display an Excel workbook programmatically by using the following code.</span></span>
    
    <span data-ttu-id="b338c-132">**Sample code provided by:** Daniel Mullowney, Microsoft Corporation</span><span class="sxs-lookup"><span data-stu-id="b338c-132">**Sample code provided by:** Daniel Mullowney, Microsoft Corporation</span></span>
    


```cs
  
...
// Instantiate Excel Web Access Web Part.
// Add an Excel Web Access Web Part in a shared view.
ExcelWebRenderer ewaWebPart = new ExcelWebRenderer();
ewaWebPart.WorkbookUri = book;
progressBar1.PerformStep();

try
{
    webPartManager.AddWebPart(ewaWebPart, "Left", 0);
}
catch (Exception exc)
{
    MessageBox.Show(
        addWebPartError + "\\n" + exc.Message,
        appName,
        MessageBoxButtons.OK,
        MessageBoxIcon.Asterisk);
    progressBar1.Value = 1;
    return b;

```




```VB.net
  
'Instantiate Excel Web Access Web Part.
'Add an Excel Web Access Web Part in a shared view.
Dim ewaWebPart As New ExcelWebRenderer()
ewaWebPart.WorkbookUri = book
progressBar1.PerformStep()

Try
    webPartManager.AddWebPart(ewaWebPart, "Left", 0)
Catch exc As Exception
    MessageBox.Show(addWebPartError &amp; vbLf &amp; exc.Message, appName, 
        MessageBoxButtons.OK, MessageBoxIcon.Asterisk)
    progressBar1.Value = 1
    Return b
End Try
```


## <a name="example"></a><span data-ttu-id="b338c-133">Пример</span><span class="sxs-lookup"><span data-stu-id="b338c-133">Example</span></span>

<span data-ttu-id="b338c-p107">The following example is a Windows Forms application that enables a user to enter information on a SharePoint site and display an Excel workbook saved in a trusted location programmatically. It programmatically creates an Веб-клиент Excel Web Part on the default.aspx page of the specified site and displays the specified Excel workbook.</span><span class="sxs-lookup"><span data-stu-id="b338c-p107">The following example is a Windows Forms application that enables a user to enter information on a SharePoint site and display an Excel workbook saved in a trusted location programmatically. It programmatically creates an Excel Web Access Web Part on the default.aspx page of the specified site and displays the specified Excel workbook.</span></span>
  
    
    
<span data-ttu-id="b338c-p108">The code sample is the code from the Form1.cs and Form1.vb example files described in the previous procedures. The code sample uses two text boxes, a progress bar, and a button. The code is only a portion of the Windows Forms project. For example, the code involving the layout of the form is not shown.</span><span class="sxs-lookup"><span data-stu-id="b338c-p108">The code sample is the code from the Form1.cs and Form1.vb example files described in the previous procedures. The code sample uses two text boxes, a progress bar, and a button. The code is only a portion of the Windows Forms project. For example, the code involving the layout of the form is not shown.</span></span> 
  
    
    
 <span data-ttu-id="b338c-140">**Sample code provided by:** Daniel Mullowney, Microsoft Corporation</span><span class="sxs-lookup"><span data-stu-id="b338c-140">**Sample code provided by:** Daniel Mullowney, Microsoft Corporation</span></span>
  
    
    



```cs

namespace AddEWATool
{
    using System;
    using System.Windows.Forms;
    using Microsoft.Office.Excel.WebUI;
    using Microsoft.SharePoint;
    using Microsoft.SharePoint.WebPartPages;

    /// <summary>
    /// Form1 class derived from System.Windows.Forms.
    /// </summary>
    public partial class Form1 : Form
    {
        private string appName = "AddEWATool";
        private string specifyInputError = "Please add a site URL, for example: http://myserver/site/";
        private string openSiteError = "There was a problem with the site name. Please check that the site exists.";
        private string addWebPartError = "There was a problem adding the Web Part.";
        private string successMessage = "Web Part successfully added.";

        /// <summary>
        /// Add the Excel Web Access Web Part to the Default.aspx page of the specified site.
        /// </summary>
        /// <param name="siteName">URL of the SharePoint site</param>
        /// <param name="book">URI to the workbook</param>
        /// <returns>Returns true if the WebPart was successfully added; otherwise, false.</returns>
        public bool AddWebPart(string siteName, string book)
        {
            SPSite site = null;
            SPWeb targetWeb = null;
            SPLimitedWebPartManager webPartManager = null;

            bool b = false;
            progressBar1.Visible = true;
            progressBar1.Minimum = 1;
            progressBar1.Maximum = 4;
            progressBar1.Value = 1;
            progressBar1.Step = 1;

            if (String.IsNullOrEmpty(siteName))
            {
                MessageBox.Show(
                    specifyInputError,
                    appName,
                    MessageBoxButtons.OK,
                    MessageBoxIcon.Asterisk);
                return b;
            }

            try
            {
                try
                {
                    site = new SPSite(siteName);
                    targetWeb = site.OpenWeb();
                }
                catch (Exception exc)
                {
                    MessageBox.Show(
                        openSiteError + "\\n" + exc.Message,
                        appName,
                        MessageBoxButtons.OK,
                        MessageBoxIcon.Asterisk);
                    progressBar1.Value = 1;
                    return b;
                }

                progressBar1.PerformStep();

                try
                {
                    // Get the shared Web Part manager on the Default.aspx page.
                    webPartManager = targetWeb.GetLimitedWebPartManager(
                        "Default.aspx",
                        System.Web.UI.WebControls.WebParts.PersonalizationScope.Shared);
                }
                catch (Exception exc)
                {
                    MessageBox.Show(
                        openSiteError + "\\n" + exc.Message,
                        appName,
                        MessageBoxButtons.OK,
                        MessageBoxIcon.Asterisk);
                    progressBar1.Value = 1;
                    return b;
                }

                progressBar1.PerformStep();

                // Instantiate Excel Web Access Web Part.
                // Add an Excel Web Access Web Part in a shared view.
                ExcelWebRenderer ewaWebPart = new ExcelWebRenderer();
                ewaWebPart.WorkbookUri = book;
                progressBar1.PerformStep();

                try
                {
                    webPartManager.AddWebPart(ewaWebPart, "Left", 0);
                }
                catch (Exception exc)
                {
                    MessageBox.Show(
                        addWebPartError + "\\n" + exc.Message,
                        appName,
                        MessageBoxButtons.OK,
                        MessageBoxIcon.Asterisk);
                    progressBar1.Value = 1;
                    return b;
                }
            }
            finally
            {
                if (site != null)
                {
                    site.Dispose();
                }

                if (targetWeb != null)
                {
                    targetWeb.Dispose();
                }

                if (webPartManager != null)
                {
                    webPartManager.Dispose();
                }
            }

            progressBar1.PerformStep();
            b = true;
            return b;
        }

        /// <summary>
        /// AddEWAButton click handler.
        /// </summary>
        /// <param name="sender">caller</param>
        /// <param name="e">event</param>
        private void AddEWAButton_Click(object sender, EventArgs e)
        {
            string siteUrl = textBox1.Text;
            string bookUri = textBox2.Text;
            bool succeeded = AddWebPart(siteUrl, bookUri);
            if (succeeded)
            {
                MessageBox.Show(
                    successMessage,
                    appName,
                    MessageBoxButtons.OK,
                    MessageBoxIcon.Information);
                progressBar1.Value = 1;
            }
        }
    }
}

```




```VB.net

Imports System
Imports System.Windows.Forms
Imports Microsoft.Office.Excel.WebUI
Imports Microsoft.SharePoint
Imports Microsoft.SharePoint.WebPartPages

Namespace AddEWATool
    ''' <summary>
    ''' Form1 class derived from System.Windows.Forms.
    ''' </summary>
    Partial Public Class Form1
        Inherits Form

        Private appName As String = "AddEWATool"
        Private specifyInputError As String = "Please add a site URL, for example, http://myserver/site/"
        Private openSiteError As String = "There was a problem with the site name. Please check that the site exists."
        Private addWebPartError As String = "There was a problem adding the Web Part."
        Private successMessage As String = "Web Part successfully added."

        ''' <summary>
        ''' Add the Excel Web Access Web Part to the Default.aspx page of the specified site.
        ''' </summary>
        ''' <param name="siteName">URL of the SharePoint site</param>
        ''' <param name="book">URI to the workbook</param>
        ''' <returns>Returns true if the WebPart was successfully added; otherwise, false.</returns>
        Public Function AddWebPart(ByVal siteName As String, ByVal book As String) As Boolean
            Dim site As SPSite = Nothing
            Dim targetWeb As SPWeb = Nothing
            Dim webPartManager As SPLimitedWebPartManager = Nothing

            Dim b As Boolean = False
            progressBar1.Visible = True
            progressBar1.Minimum = 1
            progressBar1.Maximum = 4
            progressBar1.Value = 1
            progressBar1.Step = 1

            If String.IsNullOrEmpty(siteName) Then
                MessageBox.Show(specifyInputError, appName, MessageBoxButtons.OK, MessageBoxIcon.Asterisk)
                Return b
            End If

            Try
                Try
                    site = New SPSite(siteName)
                    targetWeb = site.OpenWeb()
                Catch exc As Exception
                    MessageBox.Show(openSiteError &amp; vbLf &amp; exc.Message, appName, MessageBoxButtons.OK, MessageBoxIcon.Asterisk)
                    progressBar1.Value = 1
                    Return b
                End Try

                progressBar1.PerformStep()

                Try
                    ' Get the shared Web Part manager on the Default.aspx page.
                    webPartManager = targetWeb.GetLimitedWebPartManager( _
                            "Default.aspx", _
                            System.Web.UI.WebControls.WebParts.PersonalizationScope.Shared)
                Catch exc As Exception
                    MessageBox.Show(openSiteError &amp; vbLf &amp; exc.Message, appName, MessageBoxButtons.OK, MessageBoxIcon.Asterisk)
                    progressBar1.Value = 1
                    Return b
                End Try

                progressBar1.PerformStep()

                'Instantiate Excel Web Access Web Part.
                'Add an Excel Web Access Web Part in a shared view.
                Dim ewaWebPart As New ExcelWebRenderer()
                ewaWebPart.WorkbookUri = book
                progressBar1.PerformStep()

                Try
                    webPartManager.AddWebPart(ewaWebPart, "Left", 0)
                Catch exc As Exception
                    MessageBox.Show(addWebPartError &amp; vbLf &amp; exc.Message, appName, MessageBoxButtons.OK, MessageBoxIcon.Asterisk)
                    progressBar1.Value = 1
                    Return b
                End Try
            Finally
                If Not IsNothing(site) Then
                    site.Dispose()
                End If

                If Not IsNothing(targetWeb) Then
                    targetWeb.Dispose()
                End If

                If Not IsNothing(webPartManager) Then
                    webPartManager.Dispose()
                End If
            End Try

            progressBar1.PerformStep()
            b = True
            Return b
        End Function

        ''' <summary>
        ''' AddEWAButton click handler.
        ''' </summary>
        ''' <param name="sender">caller</param>
        ''' <param name="e">event</param>
        Private Sub AddEWAButton_Click(ByVal sender As Object, ByVal e As EventArgs)
            Dim siteUrl As String = textBox1.Text
            Dim bookUri As String = textBox2.Text
            Dim succeeded As Boolean = AddWebPart(siteUrl, bookUri)
            If succeeded Then
                MessageBox.Show(successMessage, appName, MessageBoxButtons.OK, MessageBoxIcon.Information)
                progressBar1.Value = 1
            End If
        End Sub
    End Class
End Namespace



```


## <a name="robust-programming"></a><span data-ttu-id="b338c-141">Надежное программирование</span><span class="sxs-lookup"><span data-stu-id="b338c-141">Robust programming</span></span>

<span data-ttu-id="b338c-142">The Excel workbook that you are using must be in a trusted location.</span><span class="sxs-lookup"><span data-stu-id="b338c-142">The Excel workbook that you are using must be in a trusted location.</span></span>
  
    
    

## <a name="see-also"></a><span data-ttu-id="b338c-143">См. также</span><span class="sxs-lookup"><span data-stu-id="b338c-143">See also</span></span>


#### <a name="tasks"></a><span data-ttu-id="b338c-144">Задачи</span><span class="sxs-lookup"><span data-stu-id="b338c-144">Tasks</span></span>


  
    
    
 [<span data-ttu-id="b338c-145">How to: Locate and Copy Microsoft.Office.Excel.WebUI.dll and Microsoft.Office.Excel.WebUI.Internal.dll</span><span class="sxs-lookup"><span data-stu-id="b338c-145">How to: Locate and Copy Microsoft.Office.Excel.WebUI.dll and Microsoft.Office.Excel.WebUI.Internal.dll</span></span>](how-to-locate-and-copy-microsoft-office-excel-webui-dll-and-microsoft-office-exc.md)
#### <a name="concepts"></a><span data-ttu-id="b338c-146">Основные понятия</span><span class="sxs-lookup"><span data-stu-id="b338c-146">Concepts</span></span>


  
    
    
 [<span data-ttu-id="b338c-147">Excel Services Alerts</span><span class="sxs-lookup"><span data-stu-id="b338c-147">Excel Services Alerts</span></span>](excel-services-alerts.md)
  
    
    
 [<span data-ttu-id="b338c-148">Excel Services Known Issues and Tips</span><span class="sxs-lookup"><span data-stu-id="b338c-148">Excel Services Known Issues and Tips</span></span>](excel-services-known-issues-and-tips.md)
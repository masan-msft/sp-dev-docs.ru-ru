---
title: "Доступ к внешнему источнику данных из пользовательской функции"
ms.date: 09/25/2017
keywords: how to,howdoi,howto,UDF
f1_keywords: how to,howdoi,howto,UDF
ms.prod: sharepoint
ms.assetid: 7a1876da-aeb5-4017-8eb6-3fed47912f70
ms.openlocfilehash: d1357dedf74ec344ef0f58fb4b0afe34a566508a
ms.sourcegitcommit: f6ea922341c38e700d0697961f8df9a454a03cba
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 11/15/2017
---
# <a name="access-an-external-data-source-from-a-udf"></a><span data-ttu-id="efc99-103">Доступ к внешнему источнику данных из пользовательской функции</span><span class="sxs-lookup"><span data-stu-id="efc99-103">Access an external data source from a UDF</span></span>

<span data-ttu-id="efc99-104">This example shows how to access an external database from a user-defined function (UDF).</span><span class="sxs-lookup"><span data-stu-id="efc99-104">This example shows how to access an external database from a user-defined function (UDF).</span></span> 
  
    
    


## <a name="example"></a><span data-ttu-id="efc99-105">Пример</span><span class="sxs-lookup"><span data-stu-id="efc99-105">Example</span></span>


```cs

using System;
using System.Collections.Generic;
using System.Text;
using Microsoft.Office.Excel.Server.Udf;
using System.Data.SqlClient;
using System.Web;
using System.Security.Principal;

namespace DatabaseAccessUdfTest1
{
    [UdfClass]
    public class
    {
        [UdfMethod(IsVolatile=true)]
        public string GetRowCount()
        {
            try
            {
                SqlConnection sqlConnection = new SqlConnection
                   ("Data Source=myDatabaseServer002;Initial 
                   Catalog=northwind;Integrated Security=SSPI;");
                SqlCommand sqlCommand = new SqlCommand("SELECT COUNT(*) 
                    FROM Customers", sqlConnection);
                sqlConnection.Open();
                string rowCount = (string)sqlCommand.ExecuteScalar();
                sqlConnection.Close();
                return (rowCount);
            }
            catch (Exception e)
            {
                return (e.ToString());
            }
        }

        [UdfMethod(IsVolatile=true)]
        public string GetSqlUserName()
        {
            try
            {
                SqlConnection sqlConnection = new SqlConnection("Data 
                    Source= myDatabaseServer003;Initial 
                    Catalog=northwind;Integrated Security=SSPI;");
                SqlCommand sqlCommand = new SqlCommand("SELECT 
                    CURRENT_USER", sqlConnection);

                sqlConnection.Open();
                string userName = (string)sqlCommand.ExecuteScalar();
                sqlConnection.Close();
                return (userName);
            }
            catch (Exception e)
            {
                return (e.ToString());
            }
        }

        [UdfMethod(ReturnsPersonalInformation=true)]
        public string GetUserName()
        {
            return 
              (System.Threading.Thread.CurrentPrincipal.Identity.Name);
        }

        [UdfMethod(ReturnsPersonalInformation=true)]
        public string GetUserAuthenticationType()
        {
            return 
(System.Threading.Thread.CurrentPrincipal.Identity.AuthenticationType);
        }
    }
}
```


```VB.net

Imports System
Imports System.Collections.Generic
Imports System.Text
Imports Microsoft.Office.Excel.Server.Udf
Imports System.Data.SqlClient
Imports System.Web
Imports System.Security.Principal

Namespace DatabaseAccessUdfTest1
    <UdfClass> _
    Public Class
        <UdfMethod(IsVolatile:=True)> _
        Public Function GetRowCount() As String
            Try
                Dim sqlConnection As New SqlConnection("Data Source=myDatabaseServer002;Initial Catalog=northwind;Integrated Security=SSPI;")
                Dim sqlCommand As New SqlCommand("SELECT COUNT(*) FROM Customers", sqlConnection)
                sqlConnection.Open()
                Dim rowCount As String = CStr(sqlCommand.ExecuteScalar())
                sqlConnection.Close()
                Return (rowCount)
            Catch e As Exception
                Return (e.ToString())
            End Try
        End Function

        <UdfMethod(IsVolatile:=True)> _
        Public Function GetSqlUserName() As String
            Try
                Dim sqlConnection As New SqlConnection("Data Source= myDatabaseServer003;Initial Catalog=northwind;Integrated Security=SSPI;")
                Dim sqlCommand As New SqlCommand("SELECT CURRENT_USER", sqlConnection)

                sqlConnection.Open()
                Dim userName As String = CStr(sqlCommand.ExecuteScalar())
                sqlConnection.Close()
                Return (userName)
            Catch e As Exception
                Return (e.ToString())
            End Try
        End Function

        <UdfMethod(ReturnsPersonalInformation:=True)> _
        Public Function GetUserName() As String
            Return (System.Threading.Thread.CurrentPrincipal.Identity.Name)
        End Function

        <UdfMethod(ReturnsPersonalInformation:=True)> _
        Public Function GetUserAuthenticationType() As String
            Return (System.Threading.Thread.CurrentPrincipal.Identity.AuthenticationType)
        End Function
    End Class
End Namespace
```


## <a name="see-also"></a><span data-ttu-id="efc99-106">См. также</span><span class="sxs-lookup"><span data-stu-id="efc99-106">See also</span></span>


#### <a name="tasks"></a><span data-ttu-id="efc99-107">Задачи</span><span class="sxs-lookup"><span data-stu-id="efc99-107">Tasks</span></span>


  
    
    
 [<span data-ttu-id="efc99-108">How to: Create a UDF That Calls a Web Service</span><span class="sxs-lookup"><span data-stu-id="efc99-108">How to: Create a UDF That Calls a Web Service</span></span>](how-to-create-a-udf-that-calls-a-web-service.md)
  
    
    
 [<span data-ttu-id="efc99-109">How to: Trust a Location</span><span class="sxs-lookup"><span data-stu-id="efc99-109">How to: Trust a Location</span></span>](how-to-trust-a-location.md)
  
    
    
 [<span data-ttu-id="efc99-110">How to: Catch Exceptions</span><span class="sxs-lookup"><span data-stu-id="efc99-110">How to: Catch Exceptions</span></span>](how-to-catch-exceptions.md)
  
    
    
 [<span data-ttu-id="efc99-111">How to: Enable UDFs</span><span class="sxs-lookup"><span data-stu-id="efc99-111">How to: Enable UDFs</span></span>](how-to-enable-udfs.md)
#### <a name="concepts"></a><span data-ttu-id="efc99-112">Понятия</span><span class="sxs-lookup"><span data-stu-id="efc99-112">Concepts</span></span>


  
    
    
 [<span data-ttu-id="efc99-113">Walkthrough: Developing a Managed-Code UDF</span><span class="sxs-lookup"><span data-stu-id="efc99-113">Walkthrough: Developing a Managed-Code UDF</span></span>](walkthrough-developing-a-managed-code-udf.md)
  
    
    
 [<span data-ttu-id="efc99-114">Frequently Asked Questions About Excel Services UDFs</span><span class="sxs-lookup"><span data-stu-id="efc99-114">Frequently Asked Questions About Excel Services UDFs</span></span>](frequently-asked-questions-about-excel-services-udfs.md)
  
    
    
 [<span data-ttu-id="efc99-115">Архитектура служб Excel</span><span class="sxs-lookup"><span data-stu-id="efc99-115">Excel Services Architecture</span></span>](excel-services-architecture.md)
  
    
    
 [<span data-ttu-id="efc99-116">Excel Services Alerts</span><span class="sxs-lookup"><span data-stu-id="efc99-116">Excel Services Alerts</span></span>](excel-services-alerts.md)
  
    
    
 [<span data-ttu-id="efc99-117">Excel Services Known Issues and Tips</span><span class="sxs-lookup"><span data-stu-id="efc99-117">Excel Services Known Issues and Tips</span></span>](excel-services-known-issues-and-tips.md)
  
    
    
 [<span data-ttu-id="efc99-118">Excel Services Best Practices</span><span class="sxs-lookup"><span data-stu-id="efc99-118">Excel Services Best Practices</span></span>](excel-services-best-practices.md)

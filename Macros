1) Send Mails using Macro 

First, you will need to have Microsoft Excel and have some basic knowledge of VBA (Visual Basic for Applications) to create a macro.
Here is an example of a macro that can accomplish what you described:
Sub Send_Workbook_By_Email()

Dim OutApp As Object
Dim OutMail As Object
Dim wb As Workbook
Dim ws As Worksheet

Set wb = ThisWorkbook
Set ws = wb.Sheets("Sheet1")

With Application
    .EnableEvents = False
    .ScreenUpdating = False
End With

Set OutApp = CreateObject("Outlook.Application")
Set OutMail = OutApp.CreateItem(0)

With OutMail
    .to = wb.Sheets("Sheet2").Range("A2").Value
    .Subject = wb.Sheets("Sheet2").Range("B2").Value
    .Attachments.Add wb.FullName
    .Send
End With

With Application
    .EnableEvents = True
    .ScreenUpdating = True
End With

Set OutMail = Nothing
Set OutApp = Nothing

End Sub


This macro will use the Outlook application to send the current workbook (ThisWorkbook) as an attachment to the email address in cell A2 of Sheet2. The subject of the email will be the text in cell B2 of Sheet2.
Note that this is a basic example and you can customize it further to suit your needs, such as adding CC and BCC, adding body message or adding more attachments.


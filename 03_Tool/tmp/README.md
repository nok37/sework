
```vb
Sub test()
    Dim x As Long
    Dim y As Long
    Dim path As String
    Dim kaku As String
    Dim file As String
    Dim buf As String
    Dim new2 As String
    Dim wb1 As Workbook
    
    '初期化
    Range("B8:C130").Select
    Selection.ClearContents
    
    x = 2
    y = 7
    path = Range("C3").Value
    kaku = Range("C5").Value
    old = Range("E8").Value
    news = Range("E10").Value
    new2 = Range("F10").Value
    buf = Dir(path & "\*." & kaku)

    Do While buf <> ""
        y = y + 1
        file = path & "\" & buf
        Cells(y, x) = y - 7
        Cells(y, x + 1) = file
        
        Workbooks.Open filename:=file, UpdateLinks:=0
        Set wb1 = ActiveWorkbook
        Application.DisplayAlerts = False
        nfile = Replace(file, old, news)
        wb1.SaveAs nfile, FileFormat:=new2
        wb1.Close
        Application.DisplayAlerts = True
        buf = Dir()
    Loop
    
    Range("A1").Select
End Sub
```

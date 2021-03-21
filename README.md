# VBA-challenge
VBA homework 
Sub StockMarket():

    'Loop through everywork sheet
    For Each ws In Worksheets
    
    'All Variables
    Dim Ticker As String
    Dim Yearly_Change As Double
    Dim Percentage_Change As Double
    Dim Total_Volume As Long
    Dim Summary_Table As Integer
    Dim Open_Value As Double
    Dim Close_Value As Double
    Dim Vol As Integer
    Dim Lastrow As Double
    
    'Summary variable for the first row in the Summary Table

     Summary_TableRow = 2
    
    
    'Setting Headers
    
    ws.Cells(1, 9).Value = "Ticker"
    ws.Cells(1, 10).Value = "Yearly Change"
    ws.Cells(1, 11).Value = "Percent Chnage"
    ws.Cells(1, 12).Value = "Total Stock Volume"
    
    'Returning Percent change
    
    ws.Columns("J").NumberFormat = "0.00"
    ws.Columns("K").NumberFormat = "0.00%"
    
    
    'Opening Values
    Open_Value = ws.Cells(2, 3).Value
    Yearly_Close = 0
    Yearly_Change = 0
    
    'Last row variables
    
    Lastrow = ws.Cells(Rows.Count, 1).End(xlUp).Row
    
    
    
    'looping through all the ticker symbols
    'list all tickers in a column
    'Go through all the ticker symbols
    'Find the Total Volume and the Precent change each year
    
    For i = 2 To Lastrow
    
    If ws.Cells(i + 1, 1).Value <> ws.Cells(i, 1).Value Then
        
        'Find the ticker name
        Ticker = ws.Cells(i, 1).Value
        
        'Retrive Stock Volume
        Volume = ws.Cells(i, 7).Value
        
        'Combine Stock volumes to get total for year
        Total_Volume = Total_Volume + Volume
        
        ws.Range("I" & Summary_TableRow).Value = Ticker
        
        ws.Range("L" & Summary_TableRow).Value = Total_Volume
        
        'Find yearly closing price and calculate the precent changes
        
        Yearly_Close = ws.Cells(i, 6).Value
        
        Yearly_Change = Yearly_Close - Yearly_Open
        
        ws.Range("J" & Summary_TableRow).Value = Yearly_Change
        
        'Percent Change
        
        If Yearly_Open <> 0 Then
            
            Percent_Change = (Yearly_Change / Yearly_Open)
            ws.Range("K" & Summary_TableRow).Value = Percent_Change
        
        Else
            ws.Range("K" & Summary_TableRow).Value = 0
        
        End If
        
        'Formatting of Yearly_Change Cell
        
            If Yearly_Change > 0 Then
            
                ws.Range("J" & Summary_TableRow).Interior.ColorIndex = 4
            
            Else
            
                ws.Range("J" & Summary_TableRow).Interior.ColorIndex = 3
                
            End If
            
        'Update Yearly_Open for next ticker
        Yearly_Open = ws.Cells(i + 1, 3).Value
        
        
        'Go to next row for data table
        
        Summary_TableRow = Summary_TableRow + 1
        
        'Rest Volume
        Total_Volume = 0
        
        'If ticker is the same
        Else
        
            Volume = ws.Cells(1, 7).Value
            
            Total_Volume = Total_Volume
            
        End If
        
    Next i
    
    Next ws
            
        
     
     End Sub


---
layout: post
title: DataGridView ColorPicker using a DataGridViewButtonColumn
date: 2007-12-13 20:41
author: chrispelatari
comments: true
categories: [DataGridView,winforms,csharp]
---
It's not often that I get the opportunity to blog about something neat that I learned to do in [winforms](http://windowsclient.net/) so you know I gotta, even tho it's not totally complete yet. Here's how I got a DataGridViewButtonColumn to act as a color picker.

After a little bit of webernettin', I found a post by [Ward Bekker](http://dotnetjunkies.com/WebLog/wardb/archive/2006/10/12/150262.aspx) that describes how to handle the button click event of a DataGridViewButtonColumn. Sweet. We'll get back to that code in a second.

I want to have a special button that will display a rectangle of the selected color, so I created a class that derives from DataGridViewButtonCell. I want to be able to set the Color of the rectangle, and of course we have to paint the rectangle so we'll add a Color property of type Color (imagine that:) and override the Paint method.

```csharp
public ColorPickerCell : DataGridViewButtonCell{
  const float phi = 1.618f;
  private Color colorValue;
  public Color Color {
    get { return colorValue; }
    set {  
      colorValue = value; 
      this.Value = value.ToArgb().ToString();
    }
  }

  protected override void Paint(Graphics graphics, 
    Rectangle clipBounds,
    Rectangle cellBounds, 
    int rowIndex, 
    DataGridViewElementStates cellState,
    object value, 
    object formattedValue, 
    string errorText, 
    DataGridViewCellStyle cellStyle, 
    DataGridViewAdvancedBorderStyle advancedBorderStyle, 
    DataGridViewPaintParts paintParts){
      //CDF: draw the button
      base.Paint(graphics, clipBounds, cellBounds, rowIndex, cellState, value,     formattedValue, errorText, cellStyle, advancedBorderStyle, paintParts);
      //CDF: draw a purty rectangle over the button
      using(Pen darkPen = new Pen(SystemColors.ControlDark){
        Rectangle rc = new Rectangle(cellBounds.X + 8, cellBounds.Y + 3, 
        cellBounds.Width - (int)(cellBounds.Width * phi / 8), 
        cellBounds.Height - (int)(cellBounds.Height * phi / 4));

        graphics.FillRectangle(new SolidBrush(Color.FromArgb(int.Parse(formattedValue.ToString()))), rc);
        graphics.DrawRectangle(darkPen, rc);
      }
    }
  }
```

I also derived a class from DataGridViewButtonColumn (ColorPickerColumn), but I didn't really override anything. Anyway, now that we've got a button that will display a colored rectangle, we can add a ColorPickerColumn to a DataGridView on a Form. The next step is to handle the CellContentClick event as Ward indicated.

```csharp
private void dataGridView1_CellContentClick(object sender, DataGridViewCellEventArgs e) {
  //CDF: make sure we're on the right column. I used the name for this test.
  if(dataGridView1.Columns[e.ColumnIndex].Name == "ColorColumn"){
    ColorDialog dlg = new ColorDialog();
    ColorPickerCell currentCell = dataGridView1[e.ColumnIndex, e.RowIndex] as ColorPickerCell;

    if(dlg.ShowDialog() == DialogResult.OK){
      if(currentCell != null){
        currentCell.Color = dlg.Color;
        this.Invalidate();
      }
    }
  }
```

Seems to do exactly what I want for now. Nice XD

---
title: Aspose.Slides for Android via Java 20.11 Release Notes
type: docs
weight: 20
url: /java/aspose-slides-for-android-via-java-20-11-release-notes/
---

{{% alert color="primary" %}} 

This page contains release notes for Aspose.Slides for Android via Java 20.11

{{% /alert %}} 

|**Key**|**Summary**|**Category**|
| :- | :- | :- |
|SLIDESANDROID-245|Use Aspose.Slides for Java 20.11 features|Enhancement|


## **Public API Changes**
### 3D Support Added
A new own cross-platform 3D engine was implemented in Slides 20.11. This new engine will now enable functionality to export and rasterize shapes and text with 3D effects. If in the previous versions of Slides shapes that have the 3D effect applied on them were rendered flat, now it is possible to render shapes with a full-fledged 3D.

In addition to that now it is possible to create shapes with 3D effects via Slides public API:
```java
Presentation pres = new Presentation();
try {
    IAutoShape shape = pres.getSlides().get_Item(0).getShapes().addAutoShape(ShapeType.Rectangle, 200, 150, 200, 200);
    shape.getTextFrame().setText("3D");
    shape.getTextFrame().getParagraphs().get_Item(0).getParagraphFormat().getDefaultPortionFormat().setFontHeight(64);

    shape.getThreeDFormat().getCamera().setCameraType(CameraPresetType.OrthographicFront);
    shape.getThreeDFormat().getCamera().setRotation(20, 30, 40);
    shape.getThreeDFormat().getLightRig().setLightType(LightRigPresetType.Flat);
    shape.getThreeDFormat().getLightRig().setDirection(LightingDirection.Top);
    shape.getThreeDFormat().setMaterial(MaterialPresetType.Flat);
    shape.getThreeDFormat().setExtrusionHeight(100);
    shape.getThreeDFormat().getExtrusionColor().setColor(Color.BLUE);

    FileOutputStream fos = null;
    try {
        fos = new FileOutputStream("sample_3d.png");
        pres.getSlides().get_Item(0).getThumbnail(2, 2).compress(android.graphics.Bitmap.CompressFormat.PNG, 100, fos);
    } finally {
        if(fos != null) {
            fos.close();
        }
    }
    pres.save("sandbox_3d.pptx", SaveFormat.Pptx);
} finally {
    if (pres != null) pres.dispose();
}
```

The rendered thumbnail will look like that:

![todo:image_alt_text](img_01_01.png)

### Checking password to open via IPresentationInfo interface
**[checkPassword()](https://apireference.aspose.com/slides/androidjava/com.aspose.slides/IPresentationInfo#checkPassword-java.lang.String-)** 
method has been added to **[IPresentationInfo](https://apireference.aspose.com/slides/androidjava/com.aspose.slides/IPresentationInfo)** 
interface and **[PresentationInfo](https://apireference.aspose.com/slides/androidjava/com.aspose.slides/PresentationInfo)** class. 
This method allows checking whether a presentation is protected by a password to open.

Method declaration:
```java
/**
 * Checks whether a password is correct for a presentation protected with open password.
 *
 * IPresentationInfo info = PresentationFactory.getInstance().getPresentationInfo("pres.pptx");
 * boolean isPasswordCorrect = info.checkPassword("my_password");
 * 
 * @return True if the presentation is protected with open password and the password is correct and false otherwise.
 * @param password The password to check.
 * 
 * When the password is null or empty, this method returns false.
 */
public boolean checkPassword(String password);
```

The example below demonstrates how to check a password to open a presentation:
```java
IPresentationInfo info = PresentationFactory.getInstance().getPresentationInfo("pres.pptx");
boolean isPasswordCorrect = info.checkPassword("my_password");
```

### getKeepTextFlat() and setKeepTextFlat() methods have been added to ITextFrameFormat
New methods **[getKeepTextFlat()](https://apireference.aspose.com/slides/androidjava/com.aspose.slides/ITextFrameFormat#getKeepTextFlat--)** 
and **[setKeepTextFlat()](https://apireference.aspose.com/slides/androidjava/com.aspose.slides/ITextFrameFormat#setKeepTextFlat-boolean-)** 
have been added to **[ITextFrameFormat](https://apireference.aspose.com/slides/androidjava/com.aspose.slides/ITextFrameFormat)** interface.

Using these methods allows to keep text out of 3D scene entirely.

Properties declaration:

```java
/**
 * <p>
 * Returns or set keeping text out of 3D scene entirely.
 * Read/write {@code boolean}.
 * </p>
 */
public boolean getKeepTextFlat();
/**
 * <p>
 * Returns or set keeping text out of 3D scene entirely.
 * Read/write {@code boolean}.
 * </p>
 */
public void setKeepTextFlat(boolean value);
```

The code snippet below demonstrates setting keep text out of 3D scene:

```java
Presentation pres = new Presentation("Presentation.pptx");
try {
    IAutoShape shape = (AutoShape)pres.getSlides().get_Item(0).getShapes().get_Item(0);
    shape.getTextFrame().getTextFrameFormat().setKeepTextFlat(true);
} finally {
    if (pres != null) pres.dispose();
}
```

### Partial support of Map charts has been added
Partial support of Map charts has been added. It means that you can create, edit, and save charts. Rendering options are limited since Microsoft Office uses Bing data provider for generating chart image. 
So any changes related to the Map charts made within Aspose.Slides won't affect the rendering results. 
If the chart was loaded from an input file, the cached image from the PPTX package will be used for rendering purposes. 

Following enum values have been added:

- **[CombinableSeriesTypesGroup.MapChart](https://apireference.aspose.com/slides/androidjava/com.aspose.slides/CombinableSeriesTypesGroup#MapChart)**

- **[ChartType.Map](https://apireference.aspose.com/slides/androidjava/com.aspose.slides/ChartType#Map)**

Methods:

- **[IChartDataPointCollection.addDataPointForMapSeries(IChartDataCell)](https://apireference.aspose.com/slides/androidjava/com.aspose.slides/IChartDataPointCollection#addDataPointForMapSeries-com.aspose.slides.IChartDataCell-)**

- **[IChartDataPoint.getColorValue()](https://apireference.aspose.com/slides/androidjava/com.aspose.slides/IChartDataPoint#getColorValue--)**

Following **example** shows how to create a map chart from scratch:
```java
Presentation presentation = new Presentation();
try {
    //create empty chart
    IChart chart = presentation.getSlides().get_Item(0).getShapes().addChart(ChartType.Map, 50, 50, 500, 400, false);

    IChartDataWorkbook wb = chart.getChartData().getChartDataWorkbook();

    //Add series and few data points
    IChartSeries series = chart.getChartData().getSeries().add(ChartType.Map);
    series.getDataPoints().addDataPointForMapSeries(wb.getCell(0, "B2", 5));
    series.getDataPoints().addDataPointForMapSeries(wb.getCell(0, "B3", 1));
    series.getDataPoints().addDataPointForMapSeries(wb.getCell(0, "B4", 10));

    //add categories
    chart.getChartData().getCategories().add(wb.getCell(0, "A2", "United States"));
    chart.getChartData().getCategories().add(wb.getCell(0, "A3", "Mexico"));
    chart.getChartData().getCategories().add(wb.getCell(0, "A4", "Brazil"));

    //change data point value    
    IChartDataPoint dataPoint = series.getDataPoints().get_Item(1);
    dataPoint.getColorValue().getAsCell().setValue("15");

    //set data point appearance    
    dataPoint.getFormat().getFill().setFillType(FillType.Solid);
    dataPoint.getFormat().getFill().getSolidFillColor().setColor(Color.GREEN);

    presentation.save("output.pptx", SaveFormat.Pptx);
} finally {
    if (presentation != null) presentation.dispose();
}
```


* *When you first open a presentation in PP it may take a few seconds to upload an image of the chart from the Bing service since we don't provide the cached image.*

![todo:image_alt_text](MapChart.png)

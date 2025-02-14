---
title: Install Aspose.Slides for Android via Java
type: docs
weight: 10
url: /java/install-aspose-slides-for-android-via-java/
---




## **Installation**
Previously, Aspose.Slides for Android via Java was distributed as a single ZIP file which contained the JAR file, demos and documentation of Aspose.Slides for Android via Java.

1. If you want to use any version before Aspose.Words for Android via Java 18.9, you just need to unzip any version of Aspose.Slides.Android.zip into a directory of your choice.
1. Include the extracted Jar file in your application using the Build Path configuration for its application.
### **Adding reference to Aspose.Slides for Android via Java Jar**
1. Download the newest version of [Aspose.Slides for Android via Java](https://downloads.aspose.com/slides/androidjava)
1. Copy aspose-slides-18.9-android.via.java.jar into your project’s *libs/*folder

![todo:image_alt_text](install-aspose-slides-for-android-via-java_1.png)

![todo:image_alt_text](install-aspose-slides-for-android-via-java_2.png)
### **Install Aspose.Slides for Android via Java from Maven Repository**
1. Add maven repository into your build.gradle 
1. Add '[Aspose.Slides for Android via Java](https://repository.aspose.com/webapp/#/artifacts/browse/tree/General/repo/com/aspose/aspose-slides/)' JAR as a dependency

``` java

 // 1. Add maven repository into your build.gradle 

repositories {

    mavenCentral()

    maven { url "https://repository.aspose.com/repo/" }

}

// 2. Add 'Aspose.Slides for Android via Java' JAR as a dependency

dependencies {

    ...

    ...

    compile (group: 'com.aspose', name: 'aspose-slides', version: 'XX.XX', classifier: 'android.via.java')

}

```
## **Your First Application Using Aspose.Slides for Android via Java**
This article gives you an idea of getting started with Aspose.Slides for Android via Java. It will demonstrate how to setup a new Android project from scratch, add a reference to the Aspose.Slides JAR and create a new PowerPoint presentation which is saved to disk in PPTX format. This example uses [Android Studio](https://developer.android.com/studio/index.html) for development and the application is run on the Android Emulator. To get started with Aspose.Slides for Android via Java, please follow this step-by-step tutorial to create an app which uses Aspose.Slides for Android via Java:

1. Download and the [Android Studio](https://developer.android.com/studio/index.html) and install to any location.
1. Run the Android Studio.
1. Create a new Android Application Project.

![todo:image_alt_text](install-aspose-slides-for-android-via-java_3.png)

![todo:image_alt_text](install-aspose-slides-for-android-via-java_4.png)

![todo:image_alt_text](install-aspose-slides-for-android-via-java_5.png)

![todo:image_alt_text](install-aspose-slides-for-android-via-java_6.png)

![todo:image_alt_text](install-aspose-slides-for-android-via-java_7.png)





1. Copy aspose-slides-XX.XX-android.via.java.jar into your project’s libs/folder

![todo:image_alt_text](install-aspose-slides-for-android-via-java_1.png)

![todo:image_alt_text](install-aspose-slides-for-android-via-java_2.png)




1. Select Project Section (from file menu and click on Dependencies tab.
   1. Click on "+" button, select file dependency option.
   1. Select Aspose.Slides library from libs folder and click on OK.

![todo:image_alt_text](install-aspose-slides-for-android-via-java_10.png)




1. Sync the project with gradle files if needed

![todo:image_alt_text](install-aspose-slides-for-android-via-java_11.png)





1. In order to access the SDcard special permissions must be added. Click on the AndroidManifest.xml file and choose XML view. Add the following line to the file <uses-permission android:name="android.permission.WRITE_EXTERNAL_STORAGE" />



![todo:image_alt_text](install-aspose-slides-for-android-via-java_12.png)




1. Navigate back to the code section of the app and add the following imports: 

``` java

 import java.io.File;

import com.aspose.slides.IAutoShape;

import com.aspose.slides.IParagraph;

import com.aspose.slides.IPortion;

import com.aspose.slides.ISlide;

import com.aspose.slides.ITextFrame;

import com.aspose.slides.Presentation;

import com.aspose.slides.SaveFormat;

import com.aspose.slides.ShapeType;

import android.os.Environment; 

```

And then insert the following code in the body of the onCreate method to create a new Presentation from scratch using Aspose.Slides and save it to the SDCard in PPTX format.

``` java

 try

{

    // Instantiate Presentation class that represents PPTX

    Presentation pres = new Presentation();



    // Access first slide

    ISlide sld = pres.getSlides().get_Item(0);



    // Add an AutoShape of Rectangle type

    IAutoShape ashp = sld.getShapes().addAutoShape(ShapeType.Rectangle, 150, 75, 150, 50);



    // Add TextFrame to the Rectangle

    ashp.addTextFrame(" ");



    // Accessing the text frame

    ITextFrame txtFrame = ashp.getTextFrame();



    // Create the Paragraph object for text frame

    IParagraph para = txtFrame.getParagraphs().get_Item(0);



    // Create Portion object for paragraph

    IPortion portion = para.getPortions().get_Item(0);



    // Set Text

    portion.setText("Aspose TextBox");



    // Save the PPTX to card

    String sdCardPath = Environment.getExternalStorageDirectory().getPath() + File.separator;

    pres.save(sdCardPath + "Textbox.pptx",SaveFormat.Pptx);

}

catch (Exception e)

{

   e.printStackTrace();

}

```

The full code should look like this:

![todo:image_alt_text](install-aspose-slides-for-android-via-java_13.png)



1. Now run the application again. This time the Aspose.Slides code will run in the background and generate a document which is saved to the SDcard.

![todo:image_alt_text](install-aspose-slides-for-android-via-java_14.png)

![todo:image_alt_text](install-aspose-slides-for-android-via-java_15.jpg)

1. To view the created document navigate to the Tools menu then choose Android and choose Android Device Monitor

![todo:image_alt_text](install-aspose-slides-for-android-via-java_16.jpg)




![todo:image_alt_text](install-aspose-slides-for-android-via-java_17.jpg)
## **Versioning**
Since 2018 the versioning of Aspose.Slides for Android via Java complies with Aspose.Slides for Java. 



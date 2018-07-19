---
title: Custom PDF Viewer
book: userguide
chapter: pdf
slug: custom-viewer
weight: 60
---
By default, the submission PDF's that are generated use a hosted Form viewer application to render the submissions. This is great for many use cases, but there may be other situations where you would like to introduce your own **viewer** application to render the submissions for PDF generation. This is very helpful if you wish to provide your own PDF templates, or maybe even create submission pdf's that introduce your own custom elements into the pdf generation. To achieve, this, the first thing you will need to do is fork the Form Viewer found @

[https://github.com/formio/formio-viewer](https://github.com/formio/formio-viewer)

Once you download this Viewer application, you will want to make sure you install dependencies with the following command.

```
npm install
```

You can make any changes you would like to the application. For example, we could use the [Paper Theme](https://bootswatch.com/3/paper/) from Bootswatch by making the following change to the ```src/index.html```

**src/index.html**
```html
document.write('<link rel="stylesheet" href="lib/bootswatch/paper/bootstrap.min.css" />');
```

You can now compile this application using the following command.

```html
gulp build
```

This will create a **dist** folder, which you can then launch to your own hosting service. Once you have this hosted, you can then edit your form settings, and then introduce a new **Custom Property** called **viewer** and then set the value to the URL of your custom viewer application like so.

![](/assets/img/userguide/pdf/custom-viewer.png)

Once you save, and then go back to a submission and download that submission, you will notice that the PDF download now uses your own custom viewer application to render the submission PDF.

![](/assets/img/userguide/pdf/custom-viewer-download.png)

### Hosted Viewer
The current viewer is currently hosted @ https://formio.github.io/formio-viewer/dist. If you wish to make changes to the theme based on [Bootswatch Themes](https://bootswatch.com/3/), then you can use the following format

```
https://formio.github.io/formio-viewer/dist?theme=paper
```

Like so...

![](/assets/img/userguide/pdf/custom-viewer-hosted.png)

### Viewer Parameters
There are also some parameters that you can pass to the Hosted viewer if you wish to alter the output of the generated PDF. These parameters can be provided a GET query parameters to the viewer. For example, to not show the header for the viewer, you can provide the following.

```
https://formio.github.io/formio-viewer/dist?theme=paper&header=0
```

The following viewer parameters are supported.

{: .table .table-bordered .table-striped}
| Setting | Description | Example |
|---------|-------------|---------|
| theme | The Bootswatch 3 theme to provide to the pdf. | theme=yeti |
| header | If you wish to hide the header | header=0 |

### PDF Generation Parmameters
In addition to there being viewer parameters, there are also parameters that you can provide to the end of the PDF generation API. For example, if you wish to alter the margins of the generated PDF document, you can provide the following to the PDF generation url.

```
https://yourproject.form.io/yourform/submission/[SUBMISSION_ID]/download?token=TOKEN&margin=20,20,20,20
```

The accepted PDF parameters are as follows.

{: .table .table-bordered .table-striped}
| Setting | Description | Example |
|---------|-------------|---------|
| margin | The margin as provided like a CSS margin (top,left,bottom,right) | margin=20,20,20,20 |
| scale | The scale to provide to the generated PDF | scale=0.6 |
| width | The width of the viewport when generating the PDF | width=800 |
| height | The height of the viewport when generating the PDF | height=1100 |
| view | To show the submission in "viewAsHtml" mode | view=1 |
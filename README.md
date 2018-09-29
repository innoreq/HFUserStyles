# HFUserStyles

This repository provides a guidance how you as a user of the [HappyFreelancer App](https://happyfreelancer.net) can create your own custom style and use it within the app.

The HappyFreelancer App enables you to create high-quality proposals for any specialization you offer within a few minutes, and to maintain all of your experiences continuously in one place.


# Prerequisites

* You are able to create CSS styles for a given HTML output.

# The Procedure

* The app generates an HTML file from your given data. 
* That HTML references a **style.css**, where you put all your stylings in. 
* Your custom style is provided as package with a defined structure to the app. 
* You provide your custom style through **iCloud Drive** and load it from within the app.
* Alternatively, you provide your custom style in any way to your iOS device and open it with the app.

# The Package Structure

![The Package Structure Definition](Documentation/PackageStructure.png)

* The package must have a top-level folder with a **unique name** and an extension **.hfstyle**. (*01-CleanGreen-left.hfstyle*)

That folder must contain:

* A file **description.txt** which contains a brief description of the style (1 to 2 lines of text).
* A file **sample.html** which contains an app-generated sample content used to create the previews for the style selection. We strongly recommend you to use the sample.html from this repository.
* A file **version.txt** which just contains a number indicating the version of the package. This allows you to create update packages with the same name and have the app handling it accordingly.
* A file **style.css** with the stylings. This is what you must adopt to your needs.

That folder contains one required sub-folder:

* A folder **images** with required images.

That sub-folder **images** contains:

* A file **body-background.png** which is used as background image for the front page of your proposal. This file must be adopted to your needs as well.
* A file **CompanyPlaceholder.png** which is used as dummy placeholder for the style selection’s preview. You may or may not adopt this.
* A file **PersonPlaceholder.png** which is used as dummy placeholder for the style selection’s preview, too. You may or may not adopt this.

Those two placeholder images will be replaced with the images that you provide for your person and your own company during proposal generation.

# The CSS Sources

The sub-folder **origin** in this repository contains an SCSS file **style.scss** which you may want to use to generate the **style.css** in a more convenient way. 

It also contains a **_settings.scss** file where many design parameters are defined.

It additionally provides multiple other **_xxx.scss** files that are included by that **style.scss** file and required for the toolchain to work. 

# Adoption Strategies

## Scenario 1: Just modify colors and frontpage background

In this scenario, you should:

* Modify the colors and color assignments in the **_settings.scss**
* Modify the **body-background.png**
* Add and/or modify colors and color assignments to **style.scss**

## Scenario 2: Modify the basic structure of the presentation

In this case you should:

* Rework the full set of SCSS files according to your wishes.

# The Toolchain

We are using SASS to process the **style.scss** file and to create the  **style.css** required for the package. 

For performance reasons, you should use the most compact variant of the generated CSS.

# 




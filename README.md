# HFUserStyles

This repository provides a guidance how you as a user of the [HappyFreelancer App](https://happyfreelancer.net) can create your own custom style and use it within the app.

The HappyFreelancer App enables you to create high-quality proposals for any specialization you offer within a few minutes, and to maintain all of your experiences continuously in one place.

The app is available currently only in the German iOS AppStore. Other regions will follow soon, so we provide the information here in English language.

If you want to act as a professional style provider for HappyFreelancer, [please contact us](mailto:service@happyfreelancer.net). 

Please let us know when you're missing something here.


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

# The Inner Structure of the HTML

How is the HTML defined? We tried to create it in a way that leaves you all options to adopt its presentation for your needs.

Therefore, we’re using **div** elements with appropriate **class** assignments throughout the HTML.

The basic idea behind that - and this is how all the provided styles are implemented - is to have two table structures:

* An outer table, that is used for the main structure (e.g., labels and values for the *Personal Data* section, or date range and descriptions for the *Work* sections).

* An inner table, that is used for sub-structures (e.g., electronic addresses within the *Personal Data* section, or work details within the *Work* section.

Let’s have a look on the frontpage in the **sample.html**:

	<div class="frontpage">
		<div class="table">
	    	<div class="row">
	        	<div class="column left"><img class="companylogo" src="images/CompanyPlaceholder.png"></div>
	
	            	<div class="column right">
	               		<div class="maintitle">
	                        Mustermann IT
	                    </div>
	
	                    <div class="subtitle">
	                        Web+Apps
	                    </div>
	
	                    <div class="houseaddress list">
	                        <div class="headline">
	                            House Addresses
	                        </div>
	
	                        <div class="houseaddress">
	                            <div class="street">
	                                Paulinenstrasse 14
	                            </div>
	
	                            <div class="housenumber"></div>
	
	                            <div class="zipcode"></div>
	
	                            <div class="location">
	                                90200 Nürnberg
	                            </div>
	
	                            <div class="country"></div>
	                        </div>
	                    </div>
	
	                    <div class="proposaltitle label">
	                        Proposal
	                    </div>
	
	                    <div class="proposaltitle value">
	                        Experte für Web-Design und UX
	                    </div>
	                </div>
	            </div>
	        </div>
	    </div>
	

Now, let’s check the corresponding part in the **style.scss**:

	/*	
	===============================================
	Frontpage
	===============================================
	*/
	
	body {
	@extend %body-common;
	}
	
	div {
	
	&.frontpage {
		@extend %frontpage-structure-common;
	
	    .maintitle {
			@extend %frontpage-title-common;
	    }
	
	    .subtitle {
			@extend %frontpage-subtitle-common;
	    }
	
		.companylogo {
			@extend %frontpage-logo-common;
		}
	
		.houseaddress.list {
			padding-bottom: 20px;
	
			&.houseaddress {
				.street, 
				.housenumber, 
				.zipcode, 
				.location, 
				.country {
					@extend %frontpage-address-entry-common;
					color: $defensiv-color;
				}
			}
		}
		
		.postaddress.list {
			padding-bottom: 20px;
	
			&.postaddress {
				.postbox, 
				.zipcode, 
				.location, 
				.country {
					@extend %frontpage-address-entry-common;
					color: #666;
				}
			}
		}
		
		.table {
			width: 100%;
			display: table;
			clear: both;
			border-collapse: separate;
			border-spacing: 0px;
			
			 .row {
				 width: 100%;
				 display: table-row;
				 line-height: 1.35;
				 
				 .column {
				    display: table-cell;
				    vertical-align: top;
				    padding-bottom: 1px;
	
					&.left {
						width: $embedded-column-left-width;
						padding-right: 20px;
						float: left;
						white-space: nowrap;
					}
					&.right {
						width: $embedded-column-right-width;
						padding-left: 20px;
						white-space: word-wrap;
					}
				}
			}
	
			&.electronicaddress {
				@extend %eaddress-table-common;
				
				& .row {
					@extend %eaddress-row-common;
	
					&.electronicaddress {				
						& .column {
							&.left {
								@extend %eaddress-label-common;
							
							    text-transform: uppercase;
							    text-align: right;
							    letter-spacing: 0.05em;
							    font-weight: 500;
							    font-size: .7rem;
							    color: $base-color !important;
							    padding-top: 0px;
							    padding-left: 3px;
							    padding-right: 20px;
								padding-bottom: 0px;
							}
								 
							&.right {
								@extend %eaddress-value-common;
								
								color: $defensiv-color;
								text-align: left;
								font-weight: 300;
								font-size: 1rem;
								padding-bottom: 0px;
								padding-top: 0px;
							}
						}	
					}
				} 
			} 
		}
		
	    .proposaltitle {
			@extend %frontpage-proposal-title-common;
	    }
		
		.headline {
			@extend %frontpage-headline-common;
		}
	}
	}
	
You can easily see how this relates. All the other content is handled pretty much the same way.

This way, you may want to change the overall structure, i.e., by hiding certain parts at all, by changing alignments, by displaying key visuals, using sequences instead of tables, and more.


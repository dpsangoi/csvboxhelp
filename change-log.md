---
description: A record of all notable changes made to the application.
---

# Change Log

## 26 July 2021

### Added

* In addition to the Column Name, you can now add Display Label for any sheet column. Display Labels will replace the Column Names in the header row that the user will see while doing an import.

### Changed

* Fixed Date validation bug.

## 20 July 2021

### Added

* Angular Integration

## 13 July 2021

### Added

* React Integration

## 07 July 2021

### Added

* A new **`Data`** variable is returned via the **`callback`** function of the integration code. This variable contains the details of the completed import. More information [here](https://help.csvbox.io/getting-started#callback-function). This change is backward compatible with the old integration code.

## 30 June 2021

### Changed

* Fixed UI bugs.
* Optimized importer for faster speed.

## 11 June 2021

### Added

* New column type 'List'. You can now specify a list of allowed values for a column. The importer will validate the column data with the list of values configured.
* Min, Max values validation for Number type columns.
* Min, Max character length validation option for Text type columns.

## 09 June 2021

### Added

* Multiple custom user attributes to reference the users and identify them in your platform. More info here - [https://help.csvbox.io/getting-started\#referencing-the-user](https://help.csvbox.io/getting-started#referencing-the-user)

## 28 May 2021

### Added

* A sheet copy button to quickly make duplicate sheets.

## 24 May 2021

### Added

* A new optional method **setUser\(\)** to the sheet integration code. With the **setUser\(\)** method you can reference the user by providing the value to the **user\_id** option. This helps you identify and match imports to their respective users from within your system.

### Changed

* Updated pricing plans.

![New Pricing Plans](.gitbook/assets/pricing.png)

## 21 May 2021

### Added

* Support for adding custom headers for all webhooks.

## 18 May 2021

### Changed

* Fixed a few edge case data input scenarios for CSV files.
* Improved the speed of import.

## 29 April 2021

### Added

* Boolean, Regex, IP, URL, Credit Card type validations for sheet columns.

### Removed

* csvbox.io branding for paid plans. 

## 20 April 2021

### Added

* Amazon S3 destination type. You can now push the user uploaded files directly to your S3 bucket

## 12 April 2021

### Added

* Encryption for the user-uploaded files.
* Validation check for restricting files more than 15MB in size.

### Changed

* Enhancements for faster uploads

## 19 Mar 2021

### Added

* Settings page under the top right menu

![Settings Page](.gitbook/assets/settings.png)

* Delete Files Policy to provide an option to get all the user files deleted as soon as the upload is complete.

![File Delete Policy](.gitbook/assets/delete.png)

### Changed

* Filter UI on the Import Page

## 03 Mar 2021

### Added

* Date type validation for the sheet columns

### Fixed

* UI bugs on the importer widget

## 18 Feb 2021

### Added

* You can now subscribe to a webhook that will be triggered each time an import event is completed.

### Fixed

* CDN file caching problem.

## 10 Feb 2021

### Added

* Added a callback function to the sheet integration code. This function will be invoked client side each time an import event is completed.

## 20 Dec 2020

### Fixed

* UI errors on the Imports page.

### Changed

* Location of the plans page. Moved it under the User menu.

## 14 Dec 2020

### Added

* Introduced csvbox.io to the world




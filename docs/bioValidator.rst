.. bioValidator

.. _`Download latest release`: https://github.com/biocodellc/bioValidatorDeploy
.. _`Biocode Template`: http://biocode.berkeley.edu/excel/BiocodeTemplate.xls'
.. _`instructions for entering data`: http://biocode.berkeley.edu/batch_upload_help.html

bioValidator:  A desktop validation tool (legacy)
========================

About
------------------------
bioValidator is a desktop appliction that is "maintenance" only mode and is included here since it is closely related to other FIMS projects and some projects still use bioValidator.  Included in bioValidator is a photo-matcher, which is a visual method for matching photos with spreadsheet elements and renames photos according to Collector's Specimen Numbers.

Getting Started
------------------------
`Download latest release`_.  bioValidator installs and runs in a single file.  It is reccomended, however, that you create its own directory when downloading it.  If you have Java 1.6 or later installed on your computer, everything will run fine.  Otherwise, you will need to download and install Java 1.6

Entering Data For Biocode by using the `Biocode Template`_ and view `instructions for entering data`_

Building rules for data validation
------------------------

Data validation is based on a set of rules that are defined in an XML file.  Each rule can be set to a level of "Error", which means that no  downstream processing or PhotoMatching can occur, or "Warning" which means that this is an issue that can be fixed later and not critical for fixing immediately.    Tools for building validation XML files are forthcoming in later releases.  Meanwhile, it is important to know that all XML rules files themselves are validated against an <a href="http://biocode.berkeley.edu/bioValidator">XSD schema document</a>

Validating Data
------------------------
You must first download the appropriate Excel Template file to begin entering data.  The excel template and instructions for filling it out are available on the <a href="http://biocode.berkeley.edu/batch_upload_help.html">Biocode Website</a>.  Once you have entered some data, you can validate it by opening bioValidator and clicking on "Load Spreadsheet".  You can use the tools on the screen to view errors and/or warnings.  Once you fix any errors or warning, save your spreadsheet and re-load it by clicking on "Load Spreadsheet" again.

PhotoMatching
------------------------
In order to photomatch, you must first have a spreadsheet that has passed validation with no errors (though you may proceed with warnings).   Click on the "Input Directory" to choose a directory that contains your photos.  bioValidator will not modify photos in this directory, but it will create a subdirectory called ".bvthumbs" which the application uses to display thumbnails.  Once you have loaded a directory, choose an output directory by clicking on "Output Directory".  This directory will store photos that have been renamed during the matching processes.  Create matches of photos to specimens by scrolling through each and pressing Control & the mouse click button at the same time.  You will see photos copied to each specimen.

Note that if you have an output directory with appropriately named photos  that have already gone through the photomatching processing, they will appear under the specimen information.

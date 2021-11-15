# SelectPdf Online REST API - Perl Client

## HTML To PDF API - Perl Client

SelectPdf HTML To PDF Online REST API is a professional solution that lets you create PDF from web pages and raw HTML code in your applications. The API is easy to use and the integration takes only a few lines of code.

## Features

* Create PDF from any web page or html string.
* Full html5/css3/javascript support.
* Set PDF options such as page size and orientation, margins, security, web page settings.
* Set PDF viewer options and PDF document information.
* Create custom headers and footers for the pdf document.
* Hide web page elements during the conversion.
* Automatically generate bookmarks during the html to pdf conversion.
* Support for partial page conversion.
* Easy integration, no third party libraries needed.
* Works in all programming languages.
* No installation required.

Sign up for for free to get instant API access to SelectPdf [HTML to PDF API](https://selectpdf.com/html-to-pdf-api/).

## Pdf Merge API

SelectPdf offers a REST API that can be used to merge PDF documents from local disk or remote url.

## Pdf To Text API

SelectPdf offers a REST API that can be used to extract text from local or remote PDF documents and search in existing PDF documents.


## Installation

Download [selectpdf-api-perl-client-1.4.0.zip](https://github.com/selectpdf/selectpdf-api-perl-client/releases/download/1.4.0/selectpdf-api-perl-client-1.4.0.zip), unzip it and run:

```
cd selectpdf-api-perl-client-1.4.0
perl Makefile.PL
make
make test
make install
```

OR

Install SelectPdf Perl Client for Online API via CPAN: [SelectPdf on CPAN](https://metacpan.org/dist/SelectPdf).

```
cpanm SelectPdf
```

OR

Clone [selectpdf-api-perl-client](https://github.com/selectpdf/selectpdf-api-perl-client) from Github and install the library.

```
git clone https://github.com/selectpdf/selectpdf-api-perl-client
cd selectpdf-api-perl-client
perl Makefile.PL
make
make test
make install
```

## Sample Code

```
local $| = 1;

use strict;
use JSON;
use SelectPdf;

print "This is SelectPdf-$SelectPdf::VERSION.\n";

my $url = "https://selectpdf.com/";
my $local_file = "Test.pdf";
my $apiKey = "Your API key here";

eval {
    my $client = new SelectPdf::HtmlToPdfClient($apiKey);
    
    # set parameters - see full list at https://selectpdf.com/html-to-pdf-api/
    $client
        # main properties
        
        ->setPageSize("A4") # PDF page size
        ->setPageOrientation("Portrait") # PDF page orientation
        ->setMargins(0) # PDF page margins
        ->setRenderingEngine('WebKit') # rendering engine
        ->setConversionDelay(1) # conversion delay
        ->setNavigationTimeout(30) # navigation timeout
        ->setShowPageNumbers('False') # page numbers
        ->setPageBreaksEnhancedAlgorithm('True') # enhanced page break algorithm

        # additional properties

        #->setUseCssPrint('True') # enable CSS media print
        #->setDisableJavascript('True') # disable javascript
        #->setDisableInternalLinks('True') # disable internal links
        #->setDisableExternalLinks('True') # disable external links
        #->setKeepImagesTogether('True') # keep images together
        #->setScaleImages('True') # scale images to create smaller pdfs
        #->setSinglePagePdf('True') # generate a single page PDF
        #->setUserPassword('password') # secure the PDF with a password

        # generate automatic bookmarks
        
        #->setPdfBookmarksSelectors("H1, H2") # create outlines (bookmarks) for the specified elements
        #->setViewerPageMode(1) # 1 (Use Outlines) - display outlines (bookmarks) in viewer
    ;

    print "Starting conversion ...\n";

    # convert url to file
    $client->convertUrlToFile($url, $local_file);

    # convert url to memory
    # my $pdf = $client->convertUrl($url);

    # convert html string to file
    # $client->convertHtmlStringToFile("This is some <b>html</b>.", $local_file);

    # convert html string to memory
    # my $pdf = $client->convertHtmlString("This is some <b>html</b>.");

    print "Finished! Number of pages: " . $client->getNumberOfPages() . ".\n";

    # get API usage
    my $usageClient = new SelectPdf::UsageClient($apiKey);
    my $usage = $usageClient->getUsage();
    print("Usage: " . encode_json($usage) . "\n");
    print("Conversions remained this month: ". $usage->{"available"});
};

if ($@) {
    print "An error occurred: $@\n";  
}

```
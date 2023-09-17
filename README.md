# APITemplateio

# Introduction


Welcome to the [APITemplate.io](https://apitemplate.io) API v2! This is the official APITemplate.io library for PHP. For more details, see our [REST API Reference](https://apitemplate.io/apiv2/).

APITemplate.io provides PDF generation services including [Template-based PDF generation](https://apitemplate.io/pdf-generation-api/), [HTML to PDF](https://apitemplate.io/html-to-pdf-api/), and [URL to PDF conversions](https://apitemplate.io/create-pdf-from-url/), as well as an [image generation API](https://apitemplate.io/image-generation-api/).

This page contains the documentation on how to use APITemplate.io through API calls. With the APITemplate.io API, you can create PDF documents and images, as well as manage your templates.

Our API is built on RESTful HTTP, so you can utilize any HTTP/REST library of your choice in your preferred programming language to interact with APITemplate.io's API.

**Steps to produce PDFs/Images**
1. Design your template(s) using our intuitive drag-and-drop template editor or the HTML editor and save it.
2. Integrate your workflow, either with platforms like Zapier, Make.com/Integromat, Bubble.io, or any programming languages that support REST API, to send us the JSON data along with the template ID/URL/or HTML content.
3. Our REST API will then return a download URL for the images (in PNG and JPEG formats) or PDFs.

# Authentication
Upon signing up for an account, an API key will be generated for you. If needed, you can reset this API key via the web console (under the \"API Integration\" section).

To integrate with our services, you need to authenticate with the APITemplate.io API. Provide your secret key in the request header using the X-API-KEY field.


# Content Type and CORS

**Request Content-Type**
The Content-Type for POST and GET requests is set to application/json.

**Cross-Origin Resource Sharing**
This API features Cross-Origin Resource Sharing (CORS) implemented in compliance with  [W3C spec](https://www.w3.org/TR/cors/).
And that allows cross-domain communication from the browser.
All responses have a wildcard same-origin which makes them completely public and accessible to everyone, including any code on any site.



# Regional API endpoint(s)
A regional API endpoint is intended for customers in the same region. The data for the request and generated PDFs/images are processed and stored within the region.

The regions are:

| Region               | Endpoint                            | Max Timeout (Seconds) | Max Payload Size(MB)** |
|----------------------|-------------------------------------|-----------------------|-------------------------|
| Default (Singapore)  | https://rest.apitemplate.io         | 100                   | 1                       |
| Europe (Frankfurt)   | https://rest-de.apitemplate.io      | 100                   | 1                       |
| US East (N. Virginia)| https://rest-us.apitemplate.io      | 100                   | 1                       |
| Australia (Sydney)   | https://rest-au.apitemplate.io      | 30                    | 6                       |


Alternative Regions:
| Region               | Endpoint                            | Max Timeout (Seconds) | Max Payload Size(MB)** |
|----------------------|-------------------------------------|-----------------------|-------------------------|
| Default (Singapore)  | https://rest-alt.apitemplate.io     | 30                    | 6                       |
| Europe (Frankfurt)   | https://rest-alt-de.apitemplate.io  | 30                    | 6                       |
| US East (N. Virginia)| https://rest-alt-us.apitemplate.io  | 30                    | 6                       |

** Note:
- Payload size applies to request and response
- If \"export_type\" is set to `json` which output file that on AWS S3 doesn't have the limitation
- If the \"export_type\" is set to `file` which returns binary data of the generated PDF, the file size of the generated PDF is limited to either 6MB or 1MB based on the region



Other regions are available on request, contact us at hello@apitemplate.io for more information

# Rate limiting
Our API endpoints use IP-based rate limiting to ensure fair usage and prevent abuse. Users are allowed to make up to **100 requests per 10 seconds**. This rate limit is designed to accommodate a reasonable volume of requests while maintaining optimal performance for all users.

However, if you exceed this limit and make additional requests, you will receive a response with HTTP code 429. This status code indicates that you have reached the rate limit and need to wait before making further requests.


For more information, please visit [https://apitemplate.io](https://apitemplate.io).

## Installation & Usage

### Requirements

PHP 7.4 and later.
Should also work with PHP 8.0.

### Composer

To install the bindings via [Composer](https://getcomposer.org/), add the following to `composer.json`:

```json
{
  "repositories": [
    {
      "type": "vcs",
      "url": "https://github.com/GIT_USER_ID/GIT_REPO_ID.git"
    }
  ],
  "require": {
    "GIT_USER_ID/GIT_REPO_ID": "*@dev"
  }
}
```

Then run `composer install`

### Manual Installation

Download the files and include `autoload.php`:

```php
<?php
require_once('/path/to/APITemplateio/vendor/autoload.php');
```

## Getting Started

Please follow the [installation procedure](#installation--usage) and then run the following:

```php
<?php
require_once(__DIR__ . '/vendor/autoload.php');



// Configure API key authorization: ApiKeyAuth
$config = OpenAPI\Client\Configuration::getDefaultConfiguration()->setApiKey('X-API-KEY', 'YOUR_API_KEY');
// Uncomment below to setup prefix (e.g. Bearer) for API key, if needed
// $config = OpenAPI\Client\Configuration::getDefaultConfiguration()->setApiKeyPrefix('X-API-KEY', 'Bearer');


$apiInstance = new OpenAPI\Client\Api\APIIntegrationApi(
    // If you want use custom http client, pass your client which implements `GuzzleHttp\ClientInterface`.
    // This is optional, `GuzzleHttp\Client` will be used as default.
    new GuzzleHttp\Client(),
    $config
);
$template_id = 00377b2b1e0ee394; // string | Your template id, it can be obtained in the web console
$body = array('key' => new \stdClass); // object
$output_image_type = 1; // string | - Output image type(JPEG or PNG format), default to `all`. Options are `all`, `jpegOnly`,`pngOnly`.
$expiration = 5; // int | - Expiration of the generated PDF in minutes(default to `0`, store permanently)   - Use `0` to store on cdn permanently   - Or use the range between `1` minute and `10080` minutes(7 days) to specify the expiration of the generated PDF
$cloud_storage = 1; // int | - Upload the generated PDFs/images to our storage CDN, default to `1`. If you have configured `Post Action` to upload the PDFs/Images to your own S3, please set it to `0`.
$postaction_s3_filekey = 'postaction_s3_filekey_example'; // string | - This is to specify the file name for `Post Action(S3 Storage)`. - Please do not specify the file extension - Please make sure the file name is unique - You might use slash (/) as the folder delimiter
$postaction_s3_bucket = 'postaction_s3_bucket_example'; // string | - This is to overwrite the AWS Bucket for `Post Action(S3 Storage)`.
$meta = inv-iwj343jospig; // string | - Specify an external reference ID for your own reference. It appears in the `list-objects` API.

try {
    $result = $apiInstance->createImage($template_id, $body, $output_image_type, $expiration, $cloud_storage, $postaction_s3_filekey, $postaction_s3_bucket, $meta);
    print_r($result);
} catch (Exception $e) {
    echo 'Exception when calling APIIntegrationApi->createImage: ', $e->getMessage(), PHP_EOL;
}

```

## API Endpoints

All URIs are relative to *https://rest.apitemplate.io*

Class | Method | HTTP request | Description
------------|---------------|---------------|---------------
*APIIntegrationApi* | [**createImage**](docs/Api/APIIntegrationApi.md#createimage) | **POST** /v2/create-image | Create an Image
*APIIntegrationApi* | [**createPdf**](docs/Api/APIIntegrationApi.md#createpdf) | **POST** /v2/create-pdf | Create a PDF
*APIIntegrationApi* | [**createPdfFromHtml**](docs/Api/APIIntegrationApi.md#createpdffromhtml) | **POST** /v2/create-pdf-from-html | Create a PDF from HTML
*APIIntegrationApi* | [**createPdfFromUrl**](docs/Api/APIIntegrationApi.md#createpdffromurl) | **POST** /v2/create-pdf-from-url | Create a PDF from URL
*APIIntegrationApi* | [**deleteObject**](docs/Api/APIIntegrationApi.md#deleteobject) | **GET** /v2/delete-object | Delete an Object
*APIIntegrationApi* | [**listObjects**](docs/Api/APIIntegrationApi.md#listobjects) | **GET** /v2/list-objects | List Generated Objects
*PDFManipulationAPIApi* | [**mergePdfs**](docs/Api/PDFManipulationAPIApi.md#mergepdfs) | **POST** /v2/merge-pdfs | Join/Merge multiple PDFs
*TemplateManagementApi* | [**getTemplate**](docs/Api/TemplateManagementApi.md#gettemplate) | **GET** /v2/get-template | Get PDF template
*TemplateManagementApi* | [**listTemplates**](docs/Api/TemplateManagementApi.md#listtemplates) | **GET** /v2/list-templates | List Templates
*TemplateManagementApi* | [**updateTemplate**](docs/Api/TemplateManagementApi.md#updatetemplate) | **POST** /v2/update-template | Update PDF Template

## Models

- [CreatePdfFromHtmlRequest](docs/Model/CreatePdfFromHtmlRequest.md)
- [CreatePdfFromUrlRequest](docs/Model/CreatePdfFromUrlRequest.md)
- [Error](docs/Model/Error.md)
- [MergePdfsRequest](docs/Model/MergePdfsRequest.md)
- [PDFGenerationSettingsObject](docs/Model/PDFGenerationSettingsObject.md)
- [ResponseSuccess](docs/Model/ResponseSuccess.md)
- [ResponseSuccessDeleteObject](docs/Model/ResponseSuccessDeleteObject.md)
- [ResponseSuccessImageFile](docs/Model/ResponseSuccessImageFile.md)
- [ResponseSuccessListObjects](docs/Model/ResponseSuccessListObjects.md)
- [ResponseSuccessListTemplates](docs/Model/ResponseSuccessListTemplates.md)
- [ResponseSuccessListTemplatesTemplatesInner](docs/Model/ResponseSuccessListTemplatesTemplatesInner.md)
- [ResponseSuccessPDFFile](docs/Model/ResponseSuccessPDFFile.md)
- [ResponseSuccessPDFFilePostActionsInner](docs/Model/ResponseSuccessPDFFilePostActionsInner.md)
- [ResponseSuccessQueryImageTemplate](docs/Model/ResponseSuccessQueryImageTemplate.md)
- [ResponseSuccessSingleFile](docs/Model/ResponseSuccessSingleFile.md)
- [ResponseSuccessTemplate](docs/Model/ResponseSuccessTemplate.md)
- [UpdateTemplateRequest](docs/Model/UpdateTemplateRequest.md)

## Authorization

Authentication schemes defined for the API:
### ApiKeyAuth

- **Type**: API key
- **API key parameter name**: X-API-KEY
- **Location**: HTTP header


## Tests

To run the tests, use:

```bash
composer install
vendor/bin/phpunit
```

## Author

hello@apitemplate.io

## About this package

This PHP package is automatically generated by the [OpenAPI Generator](https://openapi-generator.tech) project:

- API version: `Version 2.0`
- Build package: `org.openapitools.codegen.languages.PhpClientCodegen`

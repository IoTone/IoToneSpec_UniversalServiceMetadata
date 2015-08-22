Universal Service Metadata (USM) Specification draft v0.9.1
========================================================

This document is released under the terms of the [Apache 2.0 License](https://raw.githubusercontent.com/IoTone/IoToneSpec_UniversalServiceMetadata/master/LICENSE)

Copyright 2014-2015 IoTone, Inc.

# Abstract

Universal Service Metadata(USM) Specification is a microformat intended to describe any kind of service and its characteristics.  It isn't intended as a programatic interface description to low level software interfaces, but as a high level reference to a service definition exposed.

# Conformance

 The key words "MUST", "MUST NOT", "REQUIRED", "SHALL", "SHALL NOT", "SHOULD", "SHOULD NOT", "RECOMMENDED", "MAY", and "OPTIONAL" in this document are to be interpreted as described in RFC 2119 [RFC2119].

 The terms "JSON", "JSON text", "JSON value", "member", "element", "object", "array", "number", "string", "boolean", "true", "false", and "null" in this document are to be interpreted as defined in RFC 4627 [RFC4627]. 

# Terminology

## JSON Primitives

The following primitves are:

*    array
>        A JSON array. 
*   boolean
>        A JSON boolean. 
*    integer
>        A JSON number without a fraction or exponent part. 
*    number
>        Any JSON number. Number includes integer. 
*    null
>        The JSON null value. 
*    object
>        A JSON object. 
*    string
>        A JSON string. 

# Overview

There are numerous standards of formal and ad-hoc approaches to defining remote service interfaces with varying levels of granularity.  Some standards are defined by Standards bodies, with large amounts of work going into spages and pages of specification.  As well, the format of the data varies (IDL, xml, soap, xml schemas).  Because of these differences, there isn't a good universal approach on the market, making it possible to get stuck in committee based standards, stove pipe proprietary approaches, compute intensive approaches, or incompatible approaches.

# Requirements 

-   Simple
-   Low-Compute overhead
-   Human Readable
-   Machine Readable
-   Supports Nested Definitions
-   Defines the key attributes of any device, essentially, a generic product datasheet definition
-   NoSQL DB Friendly (i.e. JSON)
-   Supports linking
-   No Standards Body necessary
-   Doesn't duplicate an existing solution that is clearly already good enough
-   Future proof through extensibility
-   Secure as required

# Implementation

Within a "usm_services" defintion, one devices a "usm_service".  Each "usm_service" is defined by a "usm_service_spec", which can be:

   * an Object representing an API specification
   * an Array of API specifications
   * a String that is a path to a JSON file

Each "usm_service" is defined by a single resource, params, and callback in a JSON array, where arg[0] is the resource, arg[1] is the params, and arg[2] is the callback.
get: [resource, params, callback ]
GET an API resource, with optional params object for the request, and an optional callback that looks like: function (err, response, body) { ... }.
post: [resource, params, callback]
Same usage as .get(), but sends a POST request.
patch: [resource, params, callback ]
Same usage as .get(), but sends a PATCH request.
put: [resource, params, callback]
Same usage as .get(), but sends a PUT request.
delete: [resource, params, callback]

Same usage as .get(), but sends a DELETE request.

Users of USM are free to define custom attributes to meet needs not yet forseen.  Universal Device Metadata(UDM) Specification is defined as a microfotmat for defining devices.  It references USM.  A device may only choose to expose services and no device details, though it is recommended that for every service, it optionally include a link to the device hosting the service using UDM.

## Alternative Implementation 1: HASH-SETS

It is possible to break down JSON into simple HASH-SET encodings.  The USM schema's notion of JSON objects with key attribute value sets is very easily represented in HASH-SET form.  One could implement a network protocol to transmit such sets simply and compactly over any number of transports.  JSON isn't neccessary as much as a structure to the data is necessary, in order to encapsulate heirarchy and relationships between data.  For constrained environments this iplementation will make more sense.  It is then possible to compact the data into a serialized format for wire transfer, such as in a TLV8 packet encoding, and transmit with fragmentation if needed.  This will be a requirement for transports with limits on packet size.  As such, if JSON isn't a requirement in alternative implementations, then HTTP is not a strict requirement.  More complex nested JSON structures would need flattening, but one could compensate for the complexity by packing more data into the key, and requiring more key prefixes per child object node to represent.

# USM Schema

It is recommended to follow the JSON-Schema format to provide conforming schema definitions for the initial specification. However, JSON-Schema isn't strictly necessary to implement this specification.
The draft schema follows below. It was generated using a sample input into http://www.jsonschema.net/

```
{
   "type":"object",
   "$schema":"http://json-schema.org/draft-03/schema",
   "id":"http://iotone.org/specs/2/schema",
   "required":false,
   "properties":{
      "usm_schema_name":{
         "type":"string",
         "id":"http://iotone.org/specs/2/schema/usm_schema_name",
         "required":false
      },
      "usm_serviceset_name":{
         "type":"string",
         "id":"http://iotone.org/specs/2/schema/usm_serviceset_name",
         "required":false
      },
      "usm_version":{
         "type":"string",
         "id":"http://iotone.org/specs/s/schema/usm_version",
         "required":false
      },
      "usm_services":{
         "type":"array",
         "id":"http://iotone.org/specs/2/schema/usm_services",
         "required":true,
         "items":{
            "type":"object",
            "id":"http://iotone.org/specs/2/schema/usm_services/0",
            "required":false,
            "properties":{
               "usm_key":{
                  "type":"string",
                  "id":"http://iotone.org/specs/2/schema/usm_services/0/usm_key",
                  "required":false
               },
               "usm_uuid":{
                  "type":"string",
                  "id":"http://iotone.org/specs/2/schema/usm_services/0/usm_uuid",
                  "required":false
               },
               "usm_schema_name":{
                  "type":"string",
                  "id":"http://iotone.org/specs/2/schema/usm_services/0/usm_schema_name",
                  "required":false
               },
               "usm_service_version":{
                  "type":"string",
                  "id":"http://iotone.org/specs/2/schema/usm_services/0/usm_service_version",
                  "required":false
               },
               "usm_class":{
                  "type":"string",
                  "id":"http://iotone.org/specs/2/schema/usm_services/0/usm_class",
                  "required":false
               },
               "usm_type":{
                  "type":"string",
                  "id":"http://iotone.org/specs/2/schema/usm_services/0/usm_type",
                  "required":false
               },
               "usm_service_endpoint":{
                  "type":"string",
                       "id":"http://iotone.org/specs/2/schema/usm_services/0/usm_service_endpoint",
                  "required":false
               },
               "usm_capabilities":{
                  "type":"string",
                  "id":"http://iotone.org/specs/2/schema/usm_services/0/usm_capabilities",
                  "required":false
               },
               "usm_service_name":{
                  "type":"string",
                  "id":"http://iotone.org/specs/2/schema/usm_services/0/usm_service_name",
                  "required":false
               },
               "usm_copyright":{
                  "type":"string",
                  "id":"http://iotone.org/specs/2/schema/usm_services/0/usm_copyright",
                  "required":false
               },
               "usm_license":{
                  "type":"string",
                  "id":"http://iotone.org/specs/2/schema/usm_services/0/usm_license",
                  "required":false
               },
               "usm_author":{
                  "type":"string",
                  "id":"http://iotone.org/specs/2/schema/usm_services/0/usm_author",
                  "required":false
               },
               "usm_tags":{
                  "type":"string",
                  "id":"http://iotone.org/specs/2/schema/usm_services/0/usm_tags",
                  "required":false
               },
               "usm_vendor":{
                  "type":"string",
                  "id":"http://iotone.org/specs/2/schema/usm_services/0/usm_vendor",
                  "required":false
               },
               "usm_build_origin":{
                  "type":"string",
                  "id":"http://iotone.org/specs/2/schema/usm_services/0/usm_build_origin",
                  "required":false
               },
               "usm_build_date":{
                  "type":"string",
                  "id":"http://iotone.org/specs/2/schema/usm_services/0/usm_build_date",
                  "required":false
               }
            }
         }
      }
   }
}

```

# Example Use

*Sample Webserver*

```
{
   "usm_version":"0.9",
   "usm_serviceset_name": "mypersonalcloud"
   "usm_sevices": [
      {
         "usm_key": "lighttpd-001",
         "usm_service_name": "storage-cloud",
         "usm_version_number": "1.0.0",
         "usm_vendor": "Big Company, Inc",
         "usm_uuid": "1a8748bd-9c13-46ab-a762-e463376a1f16",
         "usm_author": "rockstardev@abigcompany.com",
         "usm_type": "webserver",
         "usm_class":["object-storage"],
         "usm_service_endpoint": {
      "create_block": {
         "put": [":id", {
            "id":containername,
            "restype":"container"
         }, callback]
      },
      "get_block": {
         "get": [":id", {
            "id":containername,
            "restype":"container"
         }, callback]
      }
         },
         "usm_copyright":"2014 Big Company Inc.",
         "usm_license":"2014 Big Company Proprietary License",
         "usm_tags":["webserver","storage","public"],
         "usm_build_origin":"Canada",
         "usm_build_date":"12/01/2013",
         "usm_capabilities": {
            "max_file_size": "10gb",
            "cost_per_gb": "0" 
         }
      }
   ]
}

```


# Alternatives 

In survey of the possible existing alternatives, there are hints of solutions that come close to what we are looking for.  In most cases, where XML is utilized, the "API Surface" for the definitions becomes vast. 

 

## JSON-P


In survey of the possible existing alternatives, there are other very good solutions.  In most cases, where XML is utilized, the "API Surface" for the definitions becomes vast.  The compute requirements for XML support may exceed the capabilities of certain devices in terms of processing and memory.  For these reasons, XML is discarded as the first choice for the USM solution.

JSON-P offers a very interesting option of RPC via string passing on top of HTTP. It is often used to get around same domain restrictions in web applications.  
Pro: 
   - It has been used for years
   - A lot of developers are familiar with it
   - It can be defined within JSON or as HTTP payload in a request
Con:
   - It has serious security considerations
   - It lacks a formal definition

## DNODE

DNODE is a fascinating approach to RPC, that enables remote function execution. 
Pro:
   • Very formal approach, any valid javascript function can be executed remotely
Con:
   • It assumes full Javascript support, as formal function definitions are needed

It also has serious security considerations

# Conclusion 

The USM solution provides flexibility and some options for a variety of implementation options, by providing guidelines for developers to follow without a heavyweight api or learning curve.  It doesn't force a particular implementation.  And it is NoSQL friendly and should be easily implemented.

# Normative References 

* JSON Spec - http://json.org/ 
* http://json-schema.org/latest/json-schema-core.html
* https://github.com/IoTone/IoToneSpec_UniversalDeviceMetadata/blob/master/IOTONE_SPEC_1.md
* http://tools.ietf.org/html/rfc4122
* 
# Non-Normative References 

*  DNODE https://github.com/substack/dnode (DNODE), 
*  JSON-P: https://github.com/jaubourg/jquery-jsonp/blob/master/doc/API.md and
*  (UNIO): https://github.com/IoTone/unio
*  Metadata Standards: https://en.wikipedia.org/wiki/Metadata_standards

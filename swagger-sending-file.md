# Sending file using swagger

tl;dr: If you want to send file with html, you should use 'multipart/form-data'. You can skip to [swagger section](#swagger) now.

## Intro
How to send file with html request

HTML forms provide three methods of encoding:
 - application/x-www-form-urlencoded (the default)
 - multipart/form-data
 - text/plain

Base64 encodes each set of three bytes into four bytes. In addition the output is padded to always be a multiple of four.
So it makes file sizes roughly 33% larger than their original binary representations.
From HTML 5 spec:
'Payloads using the text/plain format are intended to be human readable. They are not reliably interpretable by computer.'
From HTML 4.01 spec:
'The content type "application/x-www-form-urlencoded" is inefficient for sending large quantities of binary data or text containing non-ASCII characters. The content type "multipart/form-data" should be used for submitting forms that contain files, non-ASCII data, and binary data.'

-

## Swagger

How to send file with swagger 2.0 by multipart/form-data

* You don't need extra modules, just plain swagger.
* You can send header and query, but you can not send body parameter with form data.
* If you need to send some data with file, do it in text fields of form. You can of course send json objects using this 'workaround'.
* In parameters of swagger request, set 'in: formData' for stuff being send with multipart/form-data.
* Set 'type: file', if you want to send file or 'type: string' for additional text data.

Yaml example for sending image with array of receivers id, some optional message and token in header:

```yaml
paths:
  /images:
    post:
      tags: [Images]
      summary: Add image
      description: |
        Adds new image with array of receivers and optional message.
      parameters:
        - name: authorization
          description: JWT authorization token
          in: header
          required: true
          type: string
        - name: image
          in: formData
          description: File you want to send with swagger
          required: true
          type: file
        - name: receivers
          in: formData
          description: JSON stringified array of receivers ids
          required: true
          type: string
        - name: message
          in: formData
          description: Optional message added to photo
          required: false
          type: string
```
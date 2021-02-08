# Request signature

You must sign all API requests to ensure security. Alibaba Cloud uses the request signature to verify the identity of the API caller. When you send an HTTP or HTTPS API request, the request must contain the signature information.

## Overview

For an RPC API, you must add the signature to the API request in the following format:

```
https://Endpoint/?SignatureVersion=1.0&SignatureMethod=HMAC-SHA1&Signature=CT9X0VtwR86fNWSnsc6v8YGOjuE%3D&SignatureNonce=3ee8c1b8-83d3-44af-a94f-4e0ad82fd6cf
```

where:

-   SignatureMethod: the encryption algorithm used to calculate the signature. Set the value to HMAC-SHA1.
-   SignatureVersion: the version of the signature encryption algorithm. Set the value to 1.0.
-   SignatureNonce: a unique random number used to prevent replay attacks. You must use different random numbers for different requests. We recommend that you use universally unique identifiers \(UUIDs\).
-   Signature: the signature. The signature is calculated by using a symmetric encryption algorithm. The AccessKey secret is the key of the algorithm.

## Procedure

The signature algorithm complies with the HMAC-SHA1 specifications in RFC 2104. It uses an AccessKey secret to calculate the Hash-based Message Authentication Code \(HMAC\) of an encoded and formatted query string and use the HMAC value as the signature. Request signatures include operation-specific parameters. Therefore, the signature of a request varies depending on the request parameters.

```
Signature = Base64( HMAC-SHA1( AccessSecret, UTF-8-Encoding-Of(
StringToSign)) )
```

To calculate a signature, follow these steps:

1.  Construct a string-to-sign.
    1.  Use the request parameters to construct a canonicalized query string:
        1.  Sort all request parameters \(including all the common request parameters and operation-specific parameters except Signature\) in alphabetical order.

            When you use the GET method to send a request, the request parameters are placed after the question mark \(?\) in the URI and are separated with ampersands \(&\).

        2.  Encode in UTF-8 the parameters and their values in the request URL. The following table describes the encoding rules.

            |Character|Encoding rule|
            |---------|-------------|
            |A to Z, a to z, 0 to 9, hyphens \(-\), underscores \(\_\), periods \(.\), and tildes \(~\)|These characters do not need to be encoded.|
            |Other characters|These characters are percent encoded in the `%XY` format. `XY` represents the ASCII code of the characters in hexadecimal notation. For example, double quotation marks \("\) are encoded as `%22`.|
            |Extended UTF-8 characters|These characters are encoded in the `%XY%ZA...` format.|
            |Spaces|Spaces must be encoded as `%20`. Do not encode spaces as plus signs \(+\). These encoding methods are different from the `application/x-www-form-urlencoded` MIME encoding algorithm \(such as the `java.net.URLEncoder` class provided by the Java standard library\). However, you can apply the encoding algorithm and then replace the plus sign \(+\) in the encoded string with `%20`, the asterisk \(\*\) with `%2A`, and `%7E` with the tilde \(~\). To do this, you can use the following `percentEncode` method:

            ```
private static final String ENCODING = "UTF-8";
private static String percentEncode(String value) throws UnsupportedEncodingException 
{
return value ! = null ? URLEncoder.encode(value, ENCODING).replace("+", "%20").replace("*", "%2A").replace("%7E", "~") : null;
}
            ``` |

        3.  Associate the encoded parameter names with their encoded values separately by using equal signs \(=\).
        4.  Sort the parameter name and value pairs in the order specified in step i and associate the pairs with ampersands \(&\) to produce the canonicalized query string.
    2.  Create a string-to-sign from the encoded canonicalized query string as follows:

        ```
        StringToSign=
              HTTPMethod + “&” +
              percentEncode(“/”) + ”&” +
               percentEncode(CanonicalizedQueryString)
        ```

        where:

        -   HTTPMethod indicates the HTTP method used to send the request, for example, GET.
        -   percentEncode\("/"\) is the encoded backslashes \(/\), namely %2F, according to the URL encoding rule described in step i.
        -   percentEncode\(CanonicalizedQueryString\) encodes the canonicalized query string based on the URL encoding rule described in step ii.
2.  Obtain the signature.
    1.  Calculate the RFC 2104-compliant HMAC value of the string-to-sign.

        **Note:** The HMAC algorithm is HMAC-SHA1. The key of the HMAC algorithm is the combination of your AccessKey secret and an ampersand \(&\) \(ASCII code 38\) that follows the secret.

    2.  Encode the HMAC value in Base64 to obtain the signature string.
    3.  Add the signature string to the request as the Signature parameter.

        **Note:** When you add the signature string to the request, you must encode the parameter in the same way as other parameters by following the [RFC3986](https://tools.ietf.org/html/rfc3986) specifications.


## Example

This example shows how to sign an API request for calling the DescribeRegions operation. If the value of the `AccessKeyId` parameter is `testid`, the `AccessKeySecret` parameter is `testsecret`. the unsigned request URL is as follows:

```
http://ecs.aliyuncs.com/?Timestamp=2016-02-23T12:46:24Z&Format=XML&AccessKeyId=testid&Action=DescribeRegions&SignatureMethod=HMAC-SHA1&SignatureNonce=3ee8c1b8-83d3-44af-a94f-4e0ad82fd6cf&Version=2014-05-26&SignatureVersion=1.0
```

The signature string calculated by using `testsecret&` is as follows:

```
OLeaidS1JvxuMvnyHOwuJ+uX5qY=
```

Add the Signature parameter to the request and set the value to the signature string. Then the URL of the signed request is as follows:

```
http://ecs.aliyuncs.com/?SignatureVersion=1.0&Action=DescribeRegions&Format=XML&SignatureNonce=3ee8c1b8-83d3-44af-a94f-4e0ad82fd6cf&Version=2014-05-26&AccessKeyId=testid&Signature=OLeaidS1JvxuMvnyHOwuJ+uX5qY=&SignatureMethod=HMAC-SHA1&Timestamp=2016-02-23T12%3A46%3A24Z
```


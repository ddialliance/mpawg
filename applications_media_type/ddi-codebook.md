__How to read:__ 
- The following text is based on the form available at https://www.iana.org/form/media-types. When rendered on GitHub, the suggested entries are displayed in a light grey highlighted box with a copy icon on the right. In the Markdown source, these sections are enclosed in triple backticks (` ``` `) and indicate the exact text to be entered into the form; any placeholders should be replaced as appropriate. 
- All other text reproduces the structure of the original form and serves explanatory purposes only. 
- Where a selection from predefined options is required, the full list of available options - along with brief descriptions - is provided below.
- After submission, the application will be reviewed and discussed on the media-types mailing list: https://mailarchive.ietf.org/arch/browse/media-types/

# Application for a Media Type

We recommend that you read the following RFCs before proceeding with this application. It is important that you understand the application process and requirements completely. These documents are the standards for media types:

 - [RFC 2045](https://www.iana.org/go/rfc2045) - MIME formats and encodings 
 - [RFC 2046](https://www.iana.org/go/rfc2046) - Definition of media types 
 - [RFC 2077](https://www.iana.org/go/rfc2077) - Model top-level media type 
 - [RFC 6657](https://www.iana.org/go/rfc6657) - Update to MIME regarding "charset" parameter handling in textual media types 
 - [RFC 7303](https://www.iana.org/go/rfc7303) - XML media types 
 - [RFC 8081](https://www.iana.org/go/rfc8081) - Font top-level media type 
 - [RFC 9695](https://www.iana.org/go/rfc9695) - Haptics top-level media type 
 - [RFC 9694](https://www.iana.org/go/rfc9694) - Guidelines for the definition of new top-level media types 
 - [RFC 6838](https://www.iana.org/go/rfc6838) - Media type specifications and registration procedures 

#### Your Full Name [1]
```
Name of person submitting this form
```

#### Your E-mail [2]

```
E-mail
```

Please read the following questions carefully and provide complete answers. Write "N/A" for fields that are not applicable.

When referring to specifications, please provide URLs (if applicable).

#### Type Name [3]

What is the media type name?

```
application
```

Options:
 - application (RFC 2046)
 - audio (RFC 2046)
 - font (RFC 8081)
 - haptics (RFC 9695)
 - image (RFC 2046)
 - message (RFC 2046)
 - model (RFC 2077)
 - multipart (RFC 2046)
 - text (RFC 2046)
 - video (RFC 2046)

See the [Top-Level Media Types](https://www.iana.org/assignments/top-level-media-types) registry.

#### Subtype Name

What is the media subtype name? 

_The prefix, if any, will be taken from the drop-down menu and should be omitted from the text field._ **[4]**

```
Standards Tree (no prefix)
```

Options:
- Vendor Tree (vnd. prefix)
- Standards Tree (no prefix)
- Personal Tree (prs. prefix)

_Name:_ **[5]**

```
ddi-codebook+xml
```

Review the [existing subtype names](https://www.iana.org/assignments/media-types). See also [RFC 2046](https://www.iana.org/go/rfc2046) and [RFC 6838](https://www.iana.org/go/rfc6838) (sections 3 and 4.2).

Registrations in the standards tree must be approved by the IESG or correspond to a formal publication by a recognized standards body. See [RFC 6838](https://www.iana.org/go/rfc6838) (section 3.1).

If the name includes a suffix (text that follows a "+" at the end of the subtype name), that suffix must be listed in the [Structured Syntax Suffixes](https://www.iana.org/assignments/media-type-structured-suffix) registry.

The appearance of a dot (".") in a standards-tree subtype name would require registration of a new facet, which may not be what is intended.

#### Required Parameters [6]

Describe the required parameters. (If none, enter "N/A.")

```
N/A.
```

See [RFC 2046](https://www.iana.org/go/rfc2046), section 1, and [RFC 6838](https://www.iana.org/go/rfc6838), section 4.3.

Text types should pay attention to the discussion of the charset parameter in [RFC 6838](https://www.iana.org/go/rfc6838), section 4.2.1.

#### Optional Parameters [7]

Describe the optional parameters. (If none, enter "N/A.")

```
version: The version of the DDI-Codebook specification (e.g., "2.5").
charset: Same as for application/xml as specified in RFC 7303.
```

See [RFC 2046](https://www.iana.org/go/rfc2046), section 1, and [RFC 6838](https://www.iana.org/go/rfc6838), section 4.3.

#### Encoding Considerations [8]

```
binary (this media type may require encoding on transports not capable of handling binary)
```

Options:
- 7-bit text
- 8-bit text (this media type may require encoding on transports not capable of handling 8-bit text)
- binary (this media type may require encoding on transports not capable of handling binary)
- framed (transport must provide framing information)

_Additional notes (optional):_ **[9]**

```
Note
```

See [RFC 2045](https://www.iana.org/go/rfc2045), section 6, and [RFC 6838](https://www.iana.org/go/rfc6838), section 4.8.

8-bit data consists of lines no longer than 998 octets, separated by CRLF.

The following questions should help determine whether to select "8-bit" or "binary":

1. Can NUL octet appear in the format? If yes, then encoding is "binary."
2. Can CR and/or LF octets appear outside of CRLF sequence? If yes, then encoding is "binary."
3. Does the format allow for lines longer than 998 octets? If yes, then encoding is "binary."
4. Otherwise the encoding is "8-bit."

If the format is based on JSON or XML, "binary" should generally be selected due to the possibility that lines could be longer than 998 octets.

If the format is encoded using UTF-16, the encoding is always "binary."

#### Security Considerations [10]

Provide a discussion of the security considerations.

```
As a format using the +xml structured syntax suffix, it is subject to the 
security risks associated with XML, such as XML External Entity (XXE) attacks
and "Billion Laughs" denial-of-service attacks. The format does not contain
"active content" (executable scripts), but it provides metadata for research 
processes that must be interpreted carefully by receiving applications to avoid
resource exhaustion or unauthorized information disclosure.
```

All media type registrations must describe their security considerations; simply saying there are none or leaving the section blank is unacceptable.

In discussing the security considerations for a media type, it is necessary to cover at least these points:

1. State whether or not the media type contains active or executable content. If the media type does contain executable content, explain what measures have been taken to insure that it can be executed safely, e.g. a sandbox, safe operation set, signed content, etc.
2. State whether or not the information contained in the media type needs privacy or integrity services.
3. If the answer to (2) is yes, elaborate on any privacy or integrity services the media type itself provides. If it doesn't provide such services, explain how they should be provided externally, e.g., through the use of SSL/TLS.
4. If the media type uses an existing format, e.g. XML or JSON, the security considerations for that format must be referenced and any issues specific to the usage of that format, e.g., XML extensibility, must be described.
   - (4a) If the media type employs compression, the security considerations associated with that usage must be covered.
   - (4b) If the media type employs a container format, e.g., ZIP, any issues associated with that usage need to be described.
5. If the media type incorporates links that must be referenced in order to properly interpret the type, this should be noted.

Finally, although it is discouraged, it is acceptable to simply say that the security considerations of the media type have not been assessed.

See [RFC 6838](https://www.iana.org/go/rfc6838), section 4.6.

#### Interoperability Considerations [11]

Provide a discussion of the interoperability considerations.

```
DDI-Codebook is a lightweight representation of the DDI standard 
(ISO/PAS 25955:2026, also described as DDI Common Core 1.0, 
https://doi.org/10.5281/zenodo.17297309) intended primarily for documenting
simple survey data. Interoperability is ensured through the use of a single,
canonical data format defined by a publicly available XML Schema. Users 
should validate instances against the specific schema version referenced. 
While the XML Schema ensures structural consistency, independent 
implementations must account for potential schema changes between major or
minor versions. Furthermore, interoperability considerations for the 
underlying XML syntax are handled in accordance with RFC 7303.

The canonical expression of DDI 1.* through 2.1 is a Document Type Definition 
(DTD), although XML Schema versions have been created. The DTD can be 
converted to a schema using XML software, but the DTD should be used as the 
authoritative source for instance creation and validation.

The DDI-Codebook development line is backward compatible meaning that instances 
compliant with DDI versions 1 – 2.5 will also be compliant with version 2.6.
```

See [RFC 6838](https://www.iana.org/go/rfc6838), section 4.5.

#### Published specification [12]

Provide references to the published specification.

```
- DDI-Codebook 2.6 (current version): 
  https://ddialliance.org/ddi-codebook_v2.6.
- XML Schema Entry Point:
  https://ddialliance.org/Specification/DDI-Codebook/2.6/XMLSchema/codebook.xsd
```

See [RFC 6838](https://www.iana.org/go/rfc6838), section 4.10.

#### Application Usage [13]

Describe applications which use/will use this media type.

```
Metadata management tools used in data repositories, social science archives,
statistical software packages, within research and academia.
```

See [RFC 6838](https://www.iana.org/go/rfc6838), section 4.5.

#### Fragment Identifier Considerations [14]

```
Identical to the rules for application/xml as defined in RFC 7303.
```

See [RFC 6838](https://www.iana.org/go/rfc6838), section 4.11.

#### Restrictions on Usage [15]

```
N/A.
```

See [RFC 6838](https://www.iana.org/go/rfc6838), section 4.9.

#### Provisional Registrations [16]

Is this a request for provisional registration only? (Vendor-tree and personal-tree requests must select "No.")

```
No
```

Options:
- Yes. This is a request for provisional standards-tree registration only. A request for permanent registration will be submitted at a later date.
- No. This is a request for vendor-tree, personal-tree, or permanent standards-tree registration.

See [RFC 6838](https://www.iana.org/go/rfc6838), section 5.2.1 and the [provisional standards-tree media type registry](https://www.iana.org/assignments/provisional-standard-media-types).

#### Additional Information

See [RFC 6838](https://www.iana.org/go/rfc6838), section 4.12.

_Deprecated alias names for this type_ **[17]**

```
N/A.
```

_Magic number(s)_ **[18]**

```
N/A.
```

_File extension(s)_ **[19]**

```
.xml
```

_Macintosh File Type Code(s)_ **[20]**

```
N/A.
```

_Object Identifier(s) or OID(s) — See [RFC 1494](https://www.iana.org/go/rfc1494)._ **[21]**

```
N/A.
```

#### Intended Usage [22]

```
COMMON
```

Options:
- COMMON
- LIMITED USE
- OBSOLETE

_Additional information (if necessary):_ **[23]**

```
N/A.
```

"LIMITED USE" can be appropriate when the media type is restricted in its usage, such as when it is used only in a particular protocol (e.g. HTTP, but not email) or application, and its use is not recommended in other contexts.

#### Other Information & Comments [24]

```
N/A.
```

#### Contact Person

See [RFC 6838](https://www.iana.org/go/rfc6838), section 5.5.

_Contact Name_ **[25]**

```
Name
```

_Contact Email Address_ **[26]**

```
dditcmgr@gmail.com
```

_Author/Change Controller (for standards-tree registrations, this is typically the standards body)_ **[27]**

```
DDI Alliance, https://ddialliance.org/
```

By submitting my personal data, I agree that my personal data will be processed in accordance with our [Privacy Policy](https://www.icann.org/privacy/policy) and agree to abide by the website [Terms of Service](https://www.icann.org/privacy/tos).

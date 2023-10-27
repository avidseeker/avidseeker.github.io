---
title: Guidelines for extended attributes
date: 2023-08-29
---

## Draft
* A standardized tag for marking files as "favorite" (E.g: featured by Nautilus but without using xattrs).
* Attribute for binding files with each other. See [here](https://bbs.archlinux.org/viewtopic.php?pid=2114455#p2114455).
* [Dolphin ASCII xattrs](https://discuss.kde.org/t/4392)


The following is an update of the [original XDG proposal](https://www.freedesktop.org/wiki/CommonExtendedAttributes/) since 2013.

---

Extended attributes (xattrs) can be set in different namespaces. Linux uses
"security", "system", "trusted", and "user". This document only describes and
proposes attributes in the "user" namespace.

To avoid future conflicts between attributes, application-specific attributes
must be namespaced using reverse-DNS naming style. Standard DNS mapping places a
subdomain (**WWW**) before a domain (**EXAMPLE**) before the top-level
(**COM**), all separated by periods. In Common Extended Attributes, this is done
backwards, in which the top level (**user**) appears first, followed
(optionally) by one or more application-specific namespaces, followed by the
attribute name, all separated by periods.

For example, information about a document might include: number of words, number
of characters, number of chapters, and so on. These attributes might be added by
your word processor or manually inserted using an attribute editor. Since they
would change every time you edited the document, you wouldn't want to include
them as a part of your document unless the information was specifically marked
as being information about the document ("metadata") in which case either it's
kept in the document as a special marked internal value (e.g. an attribute) or
is stored outside the document as an attribute. The difference being, at least
in theory, one could examine the attribute data about a file without changing
the last access date/time of that file. Thus information not directly related to
the file itself could be stored externally to the file, such as comments, lists
of contributors, and so on.

To prevent one program from misreading attributes written by another - and
becoming confused or crashing if what it expects for an attribute is not the
same as what was written by the other program - it is recommended that at least
one application-specific namespace be used before the attribute, to avoid
conflicting use of attributes, unless the attribute is such that it is unique to
the file, is unambiguous, and would not be used for any other purpose, e.g. an
attribute like "creation-date" or "last-modified-date" might be acceptable as an
attribute without a name space, but an attribute such as "Status" might not be
as what status represents is probably ambiguous. On the other hand, an attribute
such as "document-status" or "document.status" would be a better choice (it
would also allow other forms of a "status" value to be associated with the
file.)

Then there is the issue of the value for the attribute, if it is not in an
application-specific namespace like *user.mywordprocessor.lasteditdate* as
opposed to *user.lasteditdate*, which value for "lasteditdate" is going to be
used? There are probably a half-dozen ways to store dates on computers, many
conflicting with each other. For example, is the date 04/05/06 the value April
4, 2006, May 4, 2006, or May 6, 2004? (All three of these interpretations have
been validly used for ambiguous date values). And does the date include the
time? And is it local time or UTC?

Any attribute for a specific application using the file must be in an
application-specific namespace in order to prevent conflicts such as the one
given above. The application-specific namespace should probably either be the
name of the company producing the application, a general identifier which
indicates the application, or both. So, as in the example above, the company
making the product "mywordprocessor" would put all of the extended attributes in
the form user.mywordprocessor.*attribute* where "attribute" is whatever extended
attribute used by that program. This would prevent some other program
accidentally changing or contaminating an attribute it is using.

This recommendation also applies on Mac OS X, where for example the resource
fork is stored as an extended attribute with the key
"com.apple.[?](https://secure.freedesktop.org/write/www/ikiwiki.cgi?do=create&from=CommonExtendedAttributes&page=ResourceFork)ResourceFork".
Attributes specified by freedesktop.org are prefixed with "xdg".

Attribute strings should be in UTF-8 encoding.

## General attributes in current use

- `user.mime_type`: Sets the MIME type of a file explicitly. This attribute is
documented by the "Shared MIME-info Database
Specification"(https://specifications.freedesktop.org/shared-mime-info-spec). It
says:   * "An implementation MAY also get a file's MIME type from the
user.mime_type extended attribute. The type given here should normally be used
in preference to any guessed type, since the user is able to set it explicitly.
Applications MAY choose to set the type when saving files. Since many
applications and filesystems do not support extended attributes, implementations
MUST NOT rely on this method being available."
- `user.charset`: The character encoding of a file. This attribute can be useful
if the encoding is different than the platform default. It is used by the Apache
httpd module mod_mime_xattr
(http://0pointer.de/lennart/projects/mod_mime_xattr).
- `user.creator`: The name of the application that created the file. The ROX
Contact Manager "Contact" sets this value to "Contact"
(http://roxos.sunsite.dk/dev-contrib/guido/Contacts/). This meaning of the
creator string is different from the meaning in Dublin core

## Proposed metadata attributes

Extended attributes are especially useful when they add information that is not
present in the in the actual file. Depending on the file origin, an application
can add metadata that is not present and/or can not be specified by the file or
its format. For example file downloaded from a web server can be tagged with the
URL, which can be convenient if its source has to be determined in the future.
Likewise, an email attachment can when saved be tagged with the message-id of
the email. This will make it possible to trace the original message.

These attributes are currently proposed:

- `user.xdg.comment`: A comment specified by the user. This comment could be
displayed by file managers
- `user.xdg.language`: Language of the intellectual content of the resource. The
value should follow the syntax described in RFC 3066 in conjunction with ISO 639
language codes. When a file is downloaded using HTTP, the value of the
Content-Language HTTP header can if present be copied into this attribute. See
also the Language element in Dublin core.
- `user.xdg.creator`: Reserved but not yet defined. The string "user" has a
different meaning in ROX Contact Manager (creating application) compared with
Dublin core (creating person/entity).
- `user.xdg.publisher`: Name of the creating application. See also the Publisher
element in Dublin core.
- `user.xdg.tags`: comma-delimited string of file tags. A proposed tag is to use
`favorite` to list bookmarked files in file managers.
- `user.xdg.currentpage`: used by document viewers to retrieve last read page.
This way all document viewers agree on what page to retrieve.

### Network-related attributes

- `user.xdg.origin.url`: Set on a file downloaded from a URL. Its value should
equal the URL it was downloaded from.
- `user.xdg.origin.referrer`: Set on a file downloaded from a URL. Its value
should equal the page that redirected to the download link. This is used as a
fallback for `user.xdg.origin.url` in case the direct download link expires or
was of CDN, in which case the user might be more interested in knowing the
referrer page.
- `user.xdg.origin.email.subject`: Set on an email attachment when saved to
disk. It should get its value from the originating message's "Subject" header
- `user.xdg.origin.email.from`: Set on an email attachment when saved to disk.
It should get its value from the originating messsage's "From" header. For
example '"John Doe" <[jdoe@example.com](mailto:jdoe@example.com)>', or
'[jdoe@example.com](mailto:jdoe@example.com)'
- `user.xdg.origin.email.message-id`: Set on an email attachment when saved to
disk. It should get its value from the originating message's "Message-Id"
header.

### Control attributes

Extended attributes could also act as flags for backup programs, indexing
programs and similar, to control their behavior. Below is an initial proposal
for start of discussion, to alter the default behavior. They are inspired by
html attributes to control web crawling.

- `user.xdg.robots.index`: On a file: "true" to index, "false" to not index. On
a directory: "true" to traverse the into the directory for indexing, "false" for
not traversing into it.
- `user.xdg.robots.backup`: On a file: "true" to index, "false" to not backup.
On a directory: "true" to traverse the into the directory for backup, "false"
for not traversing into it.

## Relation to Dublin Core

Dublin Core is a standard for cross-domain information resource description. The
Simple Dublin Core Metadata Element Set defines 15 elements. Applications that
have knowledge of Dublin Core metadata may choose to set this metadata as
extended attributes on a file when it saves it. Some of these elements have
counterparts in the xdg name space, but then with more strict or detailed syntax
or meaning. Attributes in the Dublin core namespace are currently not further
specified.

- `user.dublincore.title `
- `user.dublincore.creator` See also user.xdg.creator
- `user.dublincore.subject`
- `user.dublincore.description`
- `user.dublincore.publisher`
- `user.dublincore.contributor`
- `user.dublincore.date`
- `user.dublincore.type`
- `user.dublincore.format`
- `user.dublincore.identifier`
- `user.dublincore.source`
- `user.dublincore.language` See also user.xdg.language
- `user.dublincore.relation`
- `user.dublincore.coverage`
- `user.dublincore.rights`

## Application-specific attributes in current use

- `user.mime_encoding`: This attribute defines the MIME encoding to use when
serving a file with Apache httpd. It is used by mod_mime_xattr.
- `user.apache_handler`: This attribute is used by mod_mime_xattr to define the
Apache handler for a file.

Used by Beagle:

- `user.Beagle.[?](https://secure.freedesktop.org/write/www/ikiwiki.cgi?do=create&from=CommonExtendedAttributes&page=AttrTime)AttrTime
- `user.Beagle.Fingerprint`
- `user.Beagle.MTime`
- `user.Beagle.Uid`

Used by KDE Dolphin and Baloo:

* `user.baloo.rating`: how many stars

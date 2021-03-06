Cloudhopper by Twitter
============================

cloudhopper-commons-charset
---------------------------

## 3.0.1 - 2012-11-06
 - Added T-Mobile NL charset to CharsetUtils and updated tests, also to Readme
 - Changed byte constant in T-Mobile NL charset to uppercase for readability

## 3.0.0 - 2012-10-30
 - No major code changes, mostly project layout changes in prep of release to
   Maven Central Repository
 - Maven artifact group changed from cloudhopper to com.cloudhopper
 - Readme and changelog switched to markdown
 - Log4J dependency switched to SLF4J
 - Updated underlying maven license plugin - every java file had its
   license positioned after package declaration.

## 2.3.2 - 2012-10-29
 - Added custom charset for T-Mobile NL, TMobileNlGSMCharset

## 2.3.1 - 2012-02-17
 - Removed Turkish "dotless i" safe unicode replacements in MobileTextUtil.
    At recommendation of locals in Turkey, these replacements changed the 
    meaning of of a message too much.

## 2.3.0 - 2011-10-26
 - Upgrade parent POM dependency from 1.5 to 1.6
 - Added support for OSGI in final jar
 - UTF8Charset.calculateByteLength() is deprecated.  The algorithm  only
    calculates the byte length for a "modified UTF-8" string and is wrong on
    higher range characters.  Will be removed in a future release since it
    now calls ModifiedUTF8Charset.calculateByteLength() for backwards compatability.
 - GSMCharset.canRepresent is now ~10X faster by switching from a lookup table
    to a switch statement.  See test "PrintGSMMain.class" for automated class
    for re-generating the switch statement if needed.
 - Added "Modified UTF-8" charset for improved performance on encoding/decoding
    vs. Java's native UTF-8 charset.  Decoding is generally ~35% faster and 
    encoding is generally between 0 and 25% faster than Java's UTF-8 impl. 
    Encoding performance will be higher assuming you already had a byte buffer
    you planned on copying the bytes into anyway (very useful for serialization).
 - Much better performance on CharsetUtil.decode() into a String.  Each 
    charset can now optimize this usage vs. the previous method of creating
    an underlying StringBuilder.  Performance is ~25% better on most charsets.
 - Some behavior of encode() and decode() with NULL parameters was changed
    to always either do a NOOP or return a NULL.  Unit tests now check every
    registered charset for similar behavior.

## 2.2.1 - 2011-08-18
 - Fixed a performance bug with GSMCharset.canRepresent() where an inner loop
    was not broken as soon as a char was found and the search continued.
    Thanks to Yury Korolev (https://github.com/yury) for finding.
 - Fixed a correctness bug with GSMCharset.canRepresent() where the '`' (0x60)
    character was included as part of the GSM charset. This character was not
    included on encodes or decodes, but was included in this specific method
    as part of an optimization.
    Thanks to Yury Korolev (https://github.com/yury) for finding.
 - Removed any external dependency on log4j.
 - Cleaned up documentation

## 2.2.0 - 2011-07-26
 - Upgrade parent POM dependency from 1.1 to 1.5
 - Switched to new version format.
 - Added Version class to compile build info into jar

## 2.1 - 2011-05-27
 - Dotless i (used mainly in Turkic language) is now replaced with the char "1"
    (digit one) in MobileTextUtil. Please see wiki page for common SMS usage:
      http://en.wikipedia.org/wiki/Dotted_and_dotless_I
 - U+201B and U+201F unicode chars are now replaced with ascii equivalents of
    ' and "" respectively.

## 2.0 - 2011-03-14
 - Migrated build system from Ant to Maven
 - Deleted all legacy Ant build files (build.xml, Dependency.txt)
 - Added Apache license to top of all source files
 - Moved demo source code from src/demo/java into src/test/java directory and
    placed in separate "demo" package.
 - Added "Makefile" with targets that match previous demo ant tasks.

## 1.8 - 2011-02-14
 - Added MobileTextUtil.replaceAccentedChars to downgrade accented chars with
    their ascii equivalent.  For example, an accented e to a non-accented e.
 - Added additional ascii equivalents for unicode chars that MS-Word typically
    uses for text.

## 1.7 - 2011-01-08
 - Added UTF8Charset.calculateByteLength method to calculate the byte length
    required to convert a Java String into an array of UTF-8 bytes. Highly
    efficient method since it doesn't require any byte array allocation.

## 1.6 - 2010-12-16
 - Added normalize() feature: filters a source Java string into a new Java
    string with any unsupported characters converted into ?'s.
 - Added MobileTextUtil utility class: helps replace unicode characters with
    their ascii equivalents (e.g. smart quotes into dumb quotes)
 - Fixed extra E on name of charset for AIRWIDE.
 - Modified log4j.properties to ouput UTF-8 to console during demos.
 - Fixed unit tests with encoding issue on linux vs. mac os x due to encoding
    of unicode chars in the source files.

## 1.5 - 2010-08-23
 - Added support for ISO-8859-15 charset
 - Added support for VFTR-GSM charset which is a custom charset specifically
    for the Vodafone Turkey SMSC.

## 1.4 - 2010-06-08
 - Added aliases for GSM -> GSM8, PACKED-GSM -> GSM7, AIRWIDE-IA5 -> AIRWIDE-GSM
 - Added support for "VFD2-GSM" which is a custom charset Vodafone D2 uses to
    interpret the @ and some German letters from the standard GSM charset.
 - Fixed bug with some charsets modifying the byte array parameter values in
    the decoding process.  Wrote a unit test to validate common byte values
    commonly replaced does not actually change the byte array.
 - Added extra unit tests to check for null parameters against every charset

## 1.3 - 2010-05-16
 - Added support for verfiying a Java String can be represented by the
    GSMCharset.  Provides a way of automatically figuring out the correct
    data coding scheme to use when forwarding an SMS to an operator.
 - Fixed deprecated methods used in ch-commons-util

## 1.2 - 2010-02-28
 - Added support for Airwide-IA5 charset

## 1.1 - 2010-02-21
 - Added support for charset conversions including GSM, PackedGSM, etc.

## 1.0 - 2010-02-11
 - Initial release

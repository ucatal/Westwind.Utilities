﻿# Westwind.Utilities Changelog

### 3.0.28
*June 23rd, 2019*

* **Update: ShellUtils.ExecuteProcess with Output Capture**  
Add overload for `ShellUtils.ExecuteProcess()` that allows passing in a string that is filled with the output generated from execution of a command line tool.

* **New: DataUtils.IndexOfByteArray()**  
Small helper that finds a array of bytes or a string in an buffer of bytes and returns an index. Similar to `Span.IndexOf` but works in environments where not available, and also supports searching for decoded strings.

* **Fix: HtmlUtils.HtmlEncode()**  
Handle encoding of single quotes `'` as well as double quotes. Also marked this method as obsolete (despite the PR fix :-)) since this is handled by `System.Net.WebUtility` class now (since .NET 4.0).

* **Fix: ReflectionUtils.CallMethodExCom()**  
Fix bug when traversing object hierarchy.

* **Add .NET 4.8 to WindowsUtilities.GetDotnetVersion()**  
Add support for .NET 4.8 and also fix an errant `Debug.Writeline()` in this method.

### 3.0.24
*February 28th, 2019*

* **Fix: HtmlUtils.SanitizeHtml() for multi-line**  
Fix SanitizeHtml() function to work across line breaks for a tag.

* **XmlUtils.XmlString()**  
Create an XML encode string for elements or attributes.

* **FileUtils.DeleteFiles()**  
Added routine that deletes files in a folder based on a path spec, optionally recursively.

* **DebugUtils.GetCodeWithLineNumbers()**  
Add method that creates lines with line numbers appended. Useful for displaying source code.

* **StringUtils.Truncate()**  
Added method that truncates a string if it exceeds a certain number of characters.

### 3.0.20
*September 6th, 2018*

* **HtmlUtils.SanitizeHtml()**  
RegEx based HTML sanitation that handles the most common script injection scenarios for `<script>`,`<iframe>`,`<form>` etc. tags, `javascript:` script embeds and `onXXX` DOM element event handlers.

* **StringUtils.IndexOfNth() and .LastIndexOfNth()**  
Helper that returns an index for the nTh occurrance of a matched character in string.

* **ShellUtils.OpenInExplorer()**  
Allows opening an Explorer Window for for a folder or file in a folder. (full framework only)

* **ShellUtils.ExecuteProcess()**  
Wrapper around Process.Start() that captures exceptions and handles a few common scenarios simply including execution with timeout and presetting the Window. (full framework only)

* **ShellUtils.OpenTerminal()**  
Opens a shell window using Powershell or Command Prompt in a given pre-selected folder. (full framework only)

* **WindowsUtils.GetWindowsVersion() and GetDotnetVerision()**  
Helpers that retrieve a display version string that can be used by an application to display the Windows and .NET version in a meaningful way.

* **HttpClient.HttpVerb Property**  
Added HttpVerb property directly to the HttpClient object. This replaces the previous approach that required `CreateHttpWebRequest()` followed by setting  `client.WebRequest.Method` explicit.

* **LanguageUtils.IgnoreErrors()**   
Helper functions that allows you to execute a block of code explicitly with a wrapped around try/catch block. Two version - one that returns true or false, one that allows the operation to return a result.

* **ImageUtils.AdjustAspectRatio**   
Image helper routine that crops an image according to a new aspect ratio from the center outward. Useful for creating uniform images in uploaded files for previews. Also optionally resizes the adjusted image to a fixed width or height.

### 3.0.10
*January 9th, 2018*

* **FileUtils.AddTrailingSlash()**  
Adds a trailing OS specific slash to the end of a path if there isn't one.

* **FileUtils.ExpandPathEnvironmentVariables()**  
Method that checks for %envVar% embedded in the path and tries to evaluate the value from environment vars.

* **Fix: FileUtils.GetRelativePath()**   
Fix Uri usage with local file paths.

### 3.0.4
*November 12th, 2017*

* **DataUtils.GetSqlProviderFactory()**  
Add helper function to allow retrieving a SQL Provider factory without having to take a dependency on the assembly that contains the provider. This is provided for .NET Standard 2.0 which doesn't have `DbProviderFactories.GetFactory()` support that provides this functionality.

* **FileUtils.NormalizePath() and NormalizeDirectory()**  
Added function to normalize a path for the given platform it runs on - forward backward slashes. Mainly useful for legacy code that explicitly formatted paths to Windows formatting. NormalizeDirectory ensures a trailing path slash on a path.

* **FileUtils.GetCompactPath()**  
Added to return a filename that is trimmed in the middle with elipsis for long file names. You specify a max string length the and the method truncates accordingly.

* **FileUtils.SafeFileName() Updates**  
`SafeFileName()` now has options for the replacement character for invalid characters replaced as well (blank by default) as well as for spaces (which by default are not stripped).


### 3.0.1
*August 5th, 2017*

* **Support for .NET Core 2.0**  
Version 3.0 adds support for .NET Core 2.0. Most features of the toolkit have been carried forward, but some features like configuration using standard .NET Configuration files is not available in .NET Core. There are a few other features that are not available.

* **StringUtils.TokenizeString() and DetokenizeString()**  
Added a function that looks for a string pattern based on start and end characters, and replaces the text with numbered tokens. DetokenizeString() then can reinsert the tokens back into the string. Useful for parsing out parts of string for manipulation and then re-adding the values edited out.

* **StringUtils.GetLines() optional maxLines Parameter**  
Added an optional parameter to `GetLines()` to allow specifying the number of lines returned. Internally still all strings are parsed first, but the result retrieves only the max number of lines.

* **StringUtils.GenerateUniqueId() additional characters**
You can now add additional character to be included in the unique ID in addition to numbers and digits. This makes the string more resilient to avoid dupe values.

* **Add support for HMAC hashing in Encryption.ComputeHash()**  
HMAC provides a standardized way to introduces salted values into hashes that results in fixed length hashes are not vulnerable to length attacks. ComputeHash now exposes HMAC versions of the standard hash algorithms.

* **Add Encryption.EncryptBytes() and Encryption.DecryptBytes()**  
Added additional overloads that allow passing byte buffer for the encryption key to make it easier to work with OS data API.

* **Add SecureString Overloads to Encrypt/Decrypt Functions**   
The various implementations of Encrypt/DecryptString/Bytes now work with SecureString values for the encryption key to minimize holding unencrypted keys in memory as string for all but the immediate encrypt/decrypt operations.

* **DataUtils.DataTableToObjectList<T>**   
You can now convert a data table to a strongly typed list with this new function.

* **XmlUtils.GetXmlEnum()/GetXmlBool() and XmlUtils.GetAttributeXmlBool()**   
Added additional conversion methods to the XML helpers to facilitate retrieving values from XML documents more easily.

* **LinqUtils.FlattenTree**   
Flattens a tree type list into a flat enumarable by letting your provide the property for the children to flatten. `var topics = topicTree.FlattenTree(t=> t.Topics);`.

* **FileUtils.CopyDirectory()**  
Copies an entire directory tree to another directory. If the target exists files and folders are merged.

* **Fix: HMAC Processing in Encryption.ComputeHash()**  
HMAC hash computation was broken as salt was added to the data rather than just passed to the hash generator. Fixed.

> ### Breaking Changes for 3.0
> ##### .NET Core 2.0 Version
> * ConfigurationFileProvider for Configuration is not supported
> * We recommend you switch to JsonConfiguration
> * SqlDataAccess ctor requires that you pass in a **full** connection string or SqlProvider Factory. 
> * SqlDataAccess connection string names and provider names are no longer supported. (this may get fixed as additional .NET Core APIs are made available by Microsoft to support providers)
> * Encrypt.Encrypt()/Decrypt() use 24 bit keys where the old version for full framework uses 16 bit keys  
> The result is that encrypted values can't be duplicated currently with .NET Core implementation. This may get fixed in later updates of .NET Core as 16 bit TripleDES keys are possibly reintroduced.
> * Encryption DataProtection API methods don't work with .NET 2.0 since those are based on Windows APIs


### 2.70
*December 15th, 2016*

* **Fix binary encoding for extended characters in Encryption class**  
Binary encoding now uses UTF encoding to encrypt/decrypt strings in order to support extended characters.

* **Encryption adds support for returning binary string data as BinHex**  
You can now return binary values in BinHex format in addition to the default base64 encoded string values.

* **FileUtils.GetPhsysicalPath()**  
This function returns a given pathname with the proper casing for the file that exists on disk. If the file doesn't exist it

* **Fix Encoding in HttpUtils**  
Fix encoding bug that didn't properly manage UTF-8 encoding in uploaded JSON content.
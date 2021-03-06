# POSTGRESQL TEXT - CSV Dialect / Format

Note: See POSTGRESQL for an alternative CSV Dialect / Format using comma (`,`) as as separator.

- sep         = \t
- quote       = ?
- escape      = \\
- doublequote = false
- blanks (ignore empty lines) = false
- trim (leading and trailing spaces) = false


PostgreSQL docu:

> When the text format is used, the data read or written is a text file with one line per table row. 
> Columns in a row are separated by the delimiter character.
> The column values themselves are strings generated by the output function, or acceptable to the input function, 
> of each attribute's data type. The specified null string is used in place of columns that are null. 
> COPY FROM will raise an error if any line of the input file contains more or fewer columns than are expected. 
>
> End of data can be represented by a single line containing just backslash-period (\.).
> An end-of-data marker is not necessary when reading from a file, since the end of file serves perfectly well; 
> it is needed only when copying data to or from client applications using pre-3.0 client protocol.
>
> Backslash characters (\) can be used in the COPY data to quote data characters that might otherwise be taken as 
> row or column delimiters. In particular, the following characters must be preceded by a backslash 
> if they appear as part of a column value: backslash itself, newline, carriage return, and the current delimiter character.
>
> The specified null string is sent by COPY TO without adding any backslashes; conversely, 
> COPY FROM matches the input against the null string before removing backslashes. 
> Therefore, a null string such as \N cannot be confused with the actual data value \N (which would be represented as \\N).
>
> The following special backslash sequences are recognized by COPY FROM:
>
> Sequence	Represents
> - \b	Backspace (ASCII 8)
> - \f	Form feed (ASCII 12)
> - \n	Newline (ASCII 10)
> - \r	Carriage return (ASCII 13)
> - \t	Tab (ASCII 9)
> - \v	Vertical tab (ASCII 11)
> - \digits	Backslash followed by one to three octal digits specifies the character with that numeric code
> - \xdigits	Backslash x followed by one or two hex digits specifies the character with that numeric codePresently, COPY TO will never emit an octal or hex-digits backslash sequence, but it does use the other sequences listed above for those control characters.
>
> Any other backslashed character that is not mentioned in the above table will be taken to represent itself.
> However, beware of adding backslashes unnecessarily, 
> since that might accidentally produce a string matching the end-of-data marker (\.) 
> or the null string (\N by default). These strings will be recognized before any other backslash processing is done.


Edge Cases / Open Questions:

- Can values get quoted e.g. enclosed in (`"..."`)?

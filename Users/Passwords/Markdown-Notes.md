It is possible to use Markdown syntax to add some styling and formatting to password notes.
This page shows and explains the markdown syntax available for the notes.

> :star: Some apps don't support markdown styling for notes and will show plain text instead

## Bold
Text can be formatted as bold by adding two `**` before and after the text.
If more than one line should be bold, every line needs to marked separately.

#### Example
```markdown
**BOLD**

**
This
doesn't
work
**
```

#### Result
**BOLD**

**
This
doesn't
work
**


## Italic
Text can be formatted as italic by adding underscores (`_`) before and after the text.
If more than one line should be bold, every line needs to marked separately.

#### Example
```markdown
_ITALIC_

_
This
doesn't
work
_
```

#### Result
_ITALIC_

_
This
doesn't
work
_



## Headlines
It is possible to add six different levels of headlines by adding `#` at the beginning of the line.
The more `#`, the smaller the resulting headline.

#### Example
```markdown
# H1
## H2
### H3
#### H4
##### H5
###### H6
```

#### Result
# H1
## H2
### H3
#### H4
##### H5
###### H6



## Quotes
Text can be formatted as quote or blockquote by adding a `>` at the beginning of the line.
You need to have at least ony empty line after a quote, otherwise the following text will still be formatted as quote.

#### Example
```markdown
> First line of quoted text
Second line of quoted text

Not quoted text
```

#### Result
> First line of quoted text
Second line of quoted text

Not quoted text
# Regular Expression Cheat Sheet - PCRE 

|Anchor|Description|Example|Valid match|Invalid|
:---|:---|:---|:---|---
^|start of string or line|^foam|foam|bath foam|
\A|start of string in any match mode|\Afoam|foam|bath foam|
$|end of string or line|finish$|finish|finnish|
\Z|end of string, or char before last new line in any match mode|finish\Z|finish|finnish|
\z|end of string, in any match mode.|
\G|end of the previous match or the start of the string for the first match|\^(get\|set)\|\G\w+$|setValue|seValue
\b|word boundary; position between a word character (\w), and a nonword character (\W)|\bis\b|This island is beautiful|This island isn't beautiful
\B|not-word-boundary.|\Bland|island|peninsula

|Assertion|Description|Example|Valid match|Invalid|
:---|:---|:---|:---|---
(?=...)|positive lookahead|question(?=s)|questions|question
(?!...)|negative lookahead|answer(?!s)|answer| answers
(?<=...)|positive look-behind|(?<=appl)e|apple|application
(?<!...)|negative look-behind|(?<!goo)d|mood|good

|Char class|Description|Example|Valid match|Invalid|
:---|:---|:---|:---|---
[ ]|class definition|[axf]|a, x, f|b
[ - ]|class definition range|[a-c]|a, b, c|d
[ \ ]|escape inside class|[a-f\.]|a, b, .| g
[^ ]|Not in class|[^abc]|d, e| a
[:class:]|POSIX class|[:alpha:]|string|0101
.|match any chars except new line|b.ttle|battle, bottle| bttle
\s|white space, [\n\r\f\t ]|good\smorning|good morning|good.morning
\S|no-white space, [^\n\r\f\t]|good\Smorning|good.morning|good morning
\d| digit|\d{2}|23|1a
\D| non-digit|\D{3}|foo, bar|fo1
\w| word, [a-z-A-Z0-9_]|\w{4}|v411|v4.1
\W|non word, [^a-z-A-Z0-9_]|.$%?|.$%?|.ab?

|Special character|Description
:---|:---
\\|general escape|
\n|new line|
\r|carriage return|
\t|tab|
\v|vertical tab|
\f|form feed|
\a|alarm|
[\b]|backspace|
\e|escape|
\cchar|Ctrl + char(ie:\cc is Ctrl+c)
\ooo|three digit octal (ie: \123)
\xhh|one or two digit hexadecimal (ie: \x10)
\x{hex}|any hexadecimal code (ie: \x{1234})
\p{xx}|char with unicode property (ie: \p{Arabic}
\P{xx}|char without unicode property

|Sequence|Description|Example|Valid match|Invalid|
:---|:---|:---|:---|---
\||alternation|apple\|orange|apple, orange|melon
( )| subpattern |foot(er\|ball)|footer or football|footpath
(?P\<*name*>...)|subpattern, and capture submatch into *name*|`(?P<greeting>hello)`|hello|hallo
(?:...)|subpattern, but does not capture submatch|(?:hello)|hello|hallo
+| one or more quantifier|ye+ah|yeah, yeeeah|yah  
*| zero or more quantifier|ye*ah|yeeah, yeeeah, yah|yeh 
?| zero or one quantifier|yes?|yes, ye|yess  
??| zero or one, as few times as possible (lazy)|yea??h|yeah|yeaah|
+?| one or more  lazy |`/<.+?>/g`|`<P>foo</P>` matches only `<P>` and `</P>`|  
*?| zero or more, lazy|`/<.*?>/g`|`<html>`|
{n}|n times exactly|fo{2}|foo|fooo
{n,m}|from n to m times|go{2,3}d|good,goood|gooood
{n,}|at least n times|go{2,}|goo, gooo|go
(?(condition)...)|if-then pattern|`(<)?[p](?(1)>)`|`<p>`, p|<p
(?(condition)...\|...)|if-then-else pattern|`^(?(?=q)que|ans)`|question, answer|quote

|Pattern modifier|Description|
:---|:---
g| global match
i| case-insensitiv, match both uppercase and lowercase
m| multiple lines
s| single line (by default)
x| ingore whitespace allows comments
A| anchored, the pattern is forced to ^
D| dollar end only, a dollar metacharacter matches only at the end 
S| extra analysis performed, useful for non-anchored patterns
U| ungreedy, greedy patterns becomes lazy by default
X| additional functionality of PCRE (PCRE extra)
J| allow duplicate names for subpatterns
u| unicode, pattern and subject strings are treated as UTF-8

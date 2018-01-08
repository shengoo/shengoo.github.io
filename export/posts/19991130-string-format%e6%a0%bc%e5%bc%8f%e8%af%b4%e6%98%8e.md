title: String.Format格式说明
link: http://www.sheng00.com/68.html
author: admin
description: 
post_id: 68
created: 1999/11/30 08:00:00
created_gmt: 1999/11/30 00:00:00
comment_status: open
post_name: string-format%e6%a0%bc%e5%bc%8f%e8%af%b4%e6%98%8e
status: publish
post_type: post

# String.Format格式说明

## C#格式化数值结果表

字符 说明 示例 输出

C
货币
`string.Format("{0:C3}", 2)`
＄2.000

D
十进制
`string.Format("{0:D3}", 2)`
002

E
科学计数法
`1.20E+001`
1.20E+001

G
常规
`string.Format("{0:G}", 2)`
2

N
用分号隔开的数字
`string.Format("{0:N}", 250000)`
250,000.00

X
十六进制
`string.Format("{0:X000}", 12)`
C

`string.Format("{0:000.000}", 12.2)`
012.200

### Strings

There really isn't any formatting within a strong, beyond it's alignment. Alignment works for any argument being printed in a String.Format call. 

Sample Generates

`String.Format("->{1,10}<-", "Hello");`
-> Hello<-

`String.Format("->{1,-10}<-", "Hello");`
->Hello <-

### Numbers

Basic number formatting specifiers: 

Specifier
Type
Format
Output (Passed Double 1.42)
Output (Passed Int -12400)

c
Currency
{0:c}
＄1.42
-＄12,400

d
Decimal (Whole number)
{0:d}
System.FormatException
-12400

e
Scientific
{0:e}
1.420000e+000
-1.240000e+004

f
Fixed point
{0:f}
1.42
-12400.00

g
General
{0:g}
1.42
-12400

n
Number with commas for thousands
{0:n}
1.42
-12,400

r
Round trippable
{0:r}
1.42
System.FormatException

x
Hexadecimal
{0:x4}
System.FormatException
cf90

Custom number formatting: 

Specifier Type Example  Output (Passed Double 1500.42) Note

0
Zero placeholder
{0:00.0000}
1500.4200
Pads with zeroes.

#
Digit placeholder
{0:(#).##}
(1500).42

.
Decimal point
{0:0.0}
1500.4

,
Thousand separator
{0:0,0}
1,500
Must be between two zeroes.

,.
Number scaling
{0:0,.} 
2
Comma adjacent to Period scales by 1000.

%
Percent
{0:0%}
150042%
Multiplies by 100, adds % sign.

e
Exponent placeholder
{0:00e+0}
15e+2
Many exponent formats available.

;
Group separator
see below
 

The group separator is especially useful for formatting currency values which require that negative values be enclosed in parentheses. This currency formatting example at the bottom of this document makes it obvious: 

### Dates

Note that date formatting is especially dependant on the system's regional settings; the example strings here are from my local locale. 

**Specifier**
**Type**
**Example (Passed System.DateTime.Now)**

d
Short date
10/12/2002

D
Long date
December 10, 2002

t
Short time
10:11 PM

T
Long time
10:11:29 PM

f
Full date & time 
December 10, 2002 10:11 PM

F
Full date & time (long)
December 10, 2002 10:11:29 PM

g
Default date & time
10/12/2002 10:11 PM

G
Default date & time (long)
10/12/2002 10:11:29 PM

M
Month day pattern
December 10

r
RFC1123 date string
Tue, 10 Dec 2002 22:11:29 GMT

s
Sortable date string
2002-12-10T22:11:29

u
Universal sortable, local time
2002-12-10 22:13:50Z

U
Universal sortable, GMT
December 11, 2002 3:13:50 AM

Y
Year month pattern
December, 2002
The 'U' specifier seems broken; that string certainly isn't sortable. **Custom date formatting:**  

**Specifier**
**Type**
**Example **
**Example Output**

dd
Day
{0:dd}
10

ddd
Day name
{0:ddd}
Tue

dddd
Full day name
{0:dddd}
Tuesday

f, ff, ...
Second fractions
{0:fff}
932

gg, ...
Era
{0:gg}
A.D.

hh
2 digit hour
{0:hh}
10

HH
2 digit hour, 24hr format
{0:HH}
22

mm
Minute 00-59
{0:mm}
38

MM
Month 01-12
{0:MM}
12

MMM
Month abbreviation
{0:MMM}
Dec

MMMM
Full month name
{0:MMMM}
December

ss
Seconds 00-59
{0:ss}
46

tt
AM or PM
{0:tt}
PM

yy
Year, 2 digits
{0:yy}
02

yyyy
Year
{0:yyyy}
2002

zz
Timezone offset, 2 digits
{0:zz}
-05

zzz
Full timezone offset
{0:zzz}
-05:00

:
Separator
{0:hh:mm:ss}
10:43:20

/
Separator
{0:dd/MM/yyyy}
10/12/2002

### Enumerations

 

**Specifier**
**Type**

g
Default (Flag names if available, otherwise decimal)

f
Flags always

d
Integer always

x
Eight digit hex.

### Some Useful Examples

String.Format("{0:＄#,##0.00;(＄#,##0.00);Zero}", value); This will output "＄1,240.00" if passed 1243.50. It will output the same format but in parentheses if the number is negative, and will output the string "Zero" if the number is zero. String.Format("{0:(###) ###-####}", 18005551212); This will output "(800) 555-1212".   **变量.ToString()** 字符型转换 转为字符串 
    
    
    12345.ToString("n"); //生成 12,345.00 
    12345.ToString("C"); //生成 ￥12,345.00 
    12345.ToString("e"); //生成 1.234500e+004 
    12345.ToString("f4"); //生成 12345.0000 
    12345.ToString("x"); //生成 3039 (16进制)
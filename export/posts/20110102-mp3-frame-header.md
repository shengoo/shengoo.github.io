title: mp3 frame header
link: http://www.sheng00.com/19.html
author: admin
description: 
post_id: 19
created: 2011/01/02 08:00:00
created_gmt: 2011/01/02 00:00:00
comment_status: open
post_name: mp3-frame-header
status: publish
post_type: post

# mp3 frame header

** AAAAAAAA AAABBCCD EEEEFFGH IIJJKLMM**

**Sign**
**Length  
(bits)**
**Position  
(bits)**
**Description**

A
11
(31-21)
Frame sync (all bits must be set)

B
2
(20,19)
MPEG Audio version ID  
00 - MPEG Version 2.5 (later extension of MPEG 2)  
01 - reserved  
10 - MPEG Version 2 (ISO/IEC 13818-3)  
11 - MPEG Version 1 (ISO/IEC 11172-3) 

Note: MPEG Version 2.5 was added lately to the MPEG 2 standard. It is an extension used for very low bitrate files, allowing the use of lower sampling frequencies. If your decoder does not support this extension, it is recommended for you to use 12 bits for synchronization instead of 11 bits. 

C
2
(18,17)
Layer description  
00 - reserved  
01 - Layer III  
10 - Layer II  
11 - Layer I

D
1
(16)
Protection bit  
0 - Protected by CRC (16bit CRC follows header)  
1 - Not protected

E
4
(15,12)
Bitrate index  


bits
V1,L1
V1,L2
V1,L3
V2,L1
V2, L2 & L3

0000
free
free
free
free
free

0001
32
32
32
32
8

0010
64
48
40
48
16

0011
96
56
48
56
24

0100
128
64
56
64
32

0101
160
80
64
80
40

0110
192
96
80
96
48

0111
224
112
96
112
56

1000
256
128
112
128
64

1001
288
160
128
144
80

1010
320
192
160
160
96

1011
352
224
192
176
112

1100
384
256
224
192
128

1101
416
320
256
224
144

1110
448
384
320
256
160

1111
bad
bad
bad
bad
bad

NOTES: All values are in kbps  
V1 - MPEG Version 1  
V2 - MPEG Version 2 and Version 2.5  
L1 - Layer I  
L2 - Layer II  
L3 - Layer III  
  
"free" means free format. The free bitrate must remain constant, an must be lower than the maximum allowed bitrate. Decoders are not required to support decoding of free bitrate streams.  
"bad" means that the value is unallowed. 

MPEG files may feature variable bitrate (VBR). Each frame may then be created with a different bitrate. It may be used in all layers. Layer III decoders must support this method. Layer I & II decoders may support it. 

For Layer II there are some combinations of bitrate and mode which are not allowed. Here is a list of allowed combinations. 

bitrate

single channel

stereo

intensity stereo

dual channel

free

yes

yes

yes

yes

32

yes

no

no

no

48

yes

no

no

no

56

yes

no

no

no

64

yes

yes

yes

yes

80

yes

no

no

no

96

yes

yes

yes

yes

112

yes

yes

yes

yes

128

yes

yes

yes

yes

160

yes

yes

yes

yes

192

yes

yes

yes

yes

224

no

yes

yes

yes

256

no

yes

yes

yes

320

no

yes

yes

yes

384

no

yes

yes

yes

F
2
(11,10)
Sampling rate frequency index 

bits
MPEG1
MPEG2
MPEG2.5

00
44100 Hz
22050 Hz
11025 Hz

01
48000 Hz
24000 Hz
12000 Hz

10
32000 Hz
16000 Hz
8000 Hz

11
reserv.
reserv.
reserv.

G
1
(9)
Padding bit
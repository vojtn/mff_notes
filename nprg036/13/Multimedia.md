# Multimedia formats

## Graphic formats
vector / raster

### Vector graphics
2D graphic
- points
- paths - lines, curves, polygons | stroke, fill, color
- text - font, color


#### SVG (Scalable Vector Graphics)
Web standard for vector graphics
- W3C recommendation 2011
- XML-based format
- supported by all major web browsers
- quite complex specification
- can be embedded directly in html
- can be styled by css
media type: image/svg+xml
file extention: .svg

```
<svg height="210" width="500">
  <polygon points="200,10 250,190 160,210" style="fill:lime;stroke:purple;stroke-width:1" />
</svg>

```

Correct usage for:
- Diagrams
- Slide graphics
- Plot charts
- Engineering plans

D3.js
- interactivity visualization of data

Tools:
- Inkscape - Free, open-source
- Adobe illustrator
- CorelDraw
- google drawings (svg export)
- diagramns.net (svg export)

#### Universal 3D (U3D)
- ECMA-363 2005
- can be embedded in PDf
- Vertex based 3D graphics format

### Raster (bitmap) graphics
Pixel/dot = square of color
Image = pixel/dot matrix

Resolution
- number of columns and rows: 3840x2160
- total number of pixels 

Dot/pixel density
- 1200 dots per inch (DPI)
- 550 pixels per inch (PPI)

Editors:
- GIMP - Free, Opensource
- Adobe Photoshop
- Corel Painter

#### Color
- monochrome: just 2 colors, black and white
- grayscale: whole scale between black and white 
- paletized: limited set of colors, fixed for each image
- full color

#### Color model
Abstract mathematical representation of a color 

##### RGB (additive)
3 main light sources - red, blue, green
- mainly for displays
"how strongly should each light source shine"

##### CMYK (subtractive)
- Cyan, Magenta, Yellow, Black
- used for printers
"how much ink of each color should be applied"

#### Color space
Diagram of space of visable light forhuman eye - lightwaves

Color model - has to be mapped to specific color space

- sRGB - used on the internet, standard Red, Green, Blue
- Adobe RGB - mapped to CMYK colors, printers

##### Gamut
All colors achiavable by a display device  
Predefined  
Devices with a larger gamut can represent more colors

##### Bit depth
How many bits are to represent one pixel
- 24bits nowadays used the most

##### Transparency
RGBA  
A = aplha chnanel  
adds transparency control through the alpha channel   
Each RGB channel ranges from 0 to 255  
alpha ranges from 0 (completely transparent) to 1 (completely opaque)

##### Dithering
Technique of achieving color combinations from available primary colors

Reduces effective resolution
- more output pixels/dots are used to represent one input pixel
- e.g. 1 pixel of input image represented by 4 dots of different color and intensity on paper
- e.g. 4800 DPI 4-color printer effectively prints 1200 DPI images

###### Temporal dithering 
Fast switching between neighboring colors of a single pixel in time

#### BMP (Device-Independent Bitmap)

### Lossless Compression
compression good for images with large areas of same color
- screenshots
- drawings (if vector representation not possible)  
Formats:
- PNG (historical)
- WebP lossless
- AVIF lossless


#### Run length coding
1. run types and lengths
2. type, end position
3. when row length is known, runs can span rows - see 4A

#### Blockwise coding
Run length extension to 2D

#### Quadtree coding
Split into quadrants, until the blocks have the same color

#### Huffman coding
- most common values coded with the shortest bit sequences
- requires frequence analysis

#### L277
- doesnt require frequency analysis
- when a reapated value is found, it is replaced with reference to its first occurence

#### Raster formats:
##### GIF (Graphics Interchange Format) 
CompuServe, 1987
- 8 bits per pixel
    - palette of 256 colors
    - each color chosen from 24-bit RGB model
- lossless LZW compression
- supports animation
Media type: image/gif
File extension: .gif

##### PNG (Portable Network Graphics)
RFC 2083 1997, ISO/IEC 15948:2004
- replacement for GIF
- 8bpc
    - palette
    - full color RGB
- lossless DEFLATE compression
- does not support animation
- supports transparency: 8-bit alpha channel
Media type: image/png
File extension: .png

### Lossy Compression
good for photographs  
Formats:
- JPEG (historical)
- WebP
- AVIF

#### Discrete cosine transformation (DCT)
Transformation of image from raster representation to frequency representation
x = spatial dimension
y = pixel color

image represented as a sum of cosine function series
difference from Fourier’s series, which uses sinus and cosinus

Compression does not happen here, this is just change of representation.e
Compression comes next ~ quantization.


#### Quantization
Humans more sensitive to lower frequencies, less sensitive to higher frequencies  
Variable amount of discarded frequencies ~ compression level

#### Chroma subsampling
reducing resolution of the chroma components  
human eye more sensitive to luma changes than to chroma changes

#### YCbCr
different representation of color from RGB
different color model
Y′ - luma, luminance ~ brightness
Cb - chroma, chrominance, blue component
Cr - chroma, chrominance, red component

#### Raster formats: 
##### JPEG (Joint Photographic Experts group)
1992, ISO/IEC 10918-1:1994
- Most common format for photographic images on the Web
- Support for progressive compression
Media type: image/jpeg
File extension: .jpg, .jpeg



## Video formats

### R210
by Blackmagic Design
- uncompressed
10bpc RGB bitmap
each pixel padded to 32 bits (XX)
Pixel bit representation:
XXrrrrrr rrrrgggg ggggggbb bbbbbbbb

### MJPEG (Motion JPEG)
JPEG, 1992
- Video is sequence of individual JPEG images
- Typically 20:1 compression ratio
- uncompressed

### Video compression - inter-picture prediction
Macroblock
- 16x16 pixel block with 4:2:0 chroma subsampling used for DCT - as in JPEG

Motion vectors
- specifies position of a macroblock in one picture based on its position in another picture
- reduces temporal redundancy

### H.261
1988 ITU-T
2 video frame sizes
- 352x288 4:2:0
- 176x144 4:2:0
Designed for 40 kbps to 2 Mbps videos
- uses DCT and quantization
- motion-compensated inter-picture prediction
- deblocking filter smoothes macroblock edges
Usage:
- videoconferencing
- first usable video coding standard. Preceded only by unusable H.120.

### MPEG-4 

### H.265 HEVC
TU-T 2013, v10.0 2024
- 25% to 50% better compression than AVC
Up to 8K video
- Used by 43% video developers in September 2019
- Heavily patented, licensed

### VP8
On2 Technologies 2008
- bought by Google in 2010 and released as open format, RFC 6386, 2011
- Used in HTML5 video, replacement for GIF for short animations

### VP9
Google, 2013
- Direct successor to VP8, competes with HEVC
- Used by YouTube

### AV1 (AOMedia Video 1)
Alliance for Open Media, 2018
- Open, royalty-free format, based on VP9
Compression, tested by Facebook in 2018
- 34% better than VP9
- 46.2% better than H.264 high profile
- competes with HEVC
Used by YouTube, Netfli
- AV2 to be released in 2026

### H.266 VVC
ITU-T 2020, v3 2023
- Successor to H.265 HEVC
4K to 16K resolution, 10-16 bpc, YCbCr 4:4:4, 4:2:2 and 4:2:0, 360° video, variable and fractional frame rates 0 - 120 fps
- Expected 30% to 50% better compression rate compared to HEVC.
- Licensed


## Raster Graphics formats based on video formats

### WebP
- Google 2010
- successor to GIF, PNG and JPEG
- open format
- based on VP8 I-frame encoding
- lossless - 26% smaller than PNG
- lossy - 25% - 34% smaller than JPEG

Media type: image/webp
File extension: .webp

### HEIF
High Efficiency Image File Format (HEIF)  
container, MPEG 2015  
*HEIC* based on H.265 HEVC I-frames  
Media type: image/heif image/heic  
File extension: .heif .heic  
### AVIF
*AVIF* - based on AV1 encoding  
Media type: image/avif  
File extension: .avif  
Both about 50% smaller than JPEG  

## Digital audio formats

### Pulse-code modulation (PCM)
1. analog signal amplitude is sampled at regular intervals - sampling rate, frequency
2. quantized to the nearest value within a range of digital steps - bit depth, sample size

### Linear pulse-code modulation (LPCM)
- quantization steps linearly uniform

### Audio formats

#### WAV
Waveform Audio File Format
- IBM & Microsoft 1991
- Typical format for uncompressed audio
File extension: .wav

#### CD Audio
Compact Disc Digital Audio
- Red Book format
- LPCM, 44 kHz, 16bit, 2 channels

### FLAC (Free Lossless Audio Codec)
Xiph.Org Foundation 2001
- lossless compression
- 50%-70% compression rate
File extension: .flac

Compression techniques:
- linear prediction compression - predictor + error coding
- run length encoding - for silent passages
- inter-channel correlation for multi-channel audio

### MP3 (MPEG Part 3)
- lossy compression
- Fraunhofer Society, 1993
Discards parts of sound considered beyond hearing capabilities of most humans
- based on DCT
- based on psychoacoustic analysis
- 128 kbps file approx. 9% size of CD audio
Joint-stereo encoding
- main channel - sum or avg L+R
- side channel - difference L-R

### AAC (MPEG Part 7, Advanced Audio Coding)
- lossy compression
- designed as successor to MP3
- more flexible, more compression techniques -> more efficient
- patented, licensed

### OPUS
- Open format
- Ranked higher quality than any other standard audio format at any bitrate
by blind listening tests
- Used, e.g. by WhatsApp and Signal for audio messages
Media type: audio/opus
File extension: .opus



## Multimedia container formats
Encapsulation of 
- different data types (e.g. audio and video for streaming)
- multiple streams
    - audio in various languages
    - video from multiple angles
    - subtitles
    - chapter information

Contains metadata for synchronized playing of multiple data types

### Simple containers
- JPEG, PNG, WAV
- TIFF - images and metadata

### Flexible containers - patented, licensed
- AVI - Audio Video Interleave - .avi
- MPEG program stream - .ps, .mpg, .mpeg
- MPEG-2 transport stream - .ts, .m2t
- MP4 - .mp4

### Flexible containers - open, royalty free
- Matroska - .mkv and its ssubset WebM - .webm
- Ogg - .ogg

### Matroska
Matroska 2002
- open format 
file extension: .mkv

### WebM
Google 2010
- subset of Matroska
- limits usable formats to the open ones  

Video: VP8, VP9, AV1  
Audio: Vorbis, Opus  

file extension: .webm

## Print formats

### PostScript (PS)
printer programming language
- first version in 1984
- reverse polish natation
- arguments first, function last
- contains global state, instructions on one page may affect all the following pages

media type: application/postscript  
File extension: .ps

```
%!PS
/Courier             % name the desired font
20 selectfont        % choose the size in points and establish 
                    % the font as the current one
72 500 moveto        % position the current point at 
                    % coordinates 72, 500 (the origin is at the 
                    % lower-left corner of the page)
(Hello world!) show  % stroke the text in parentheses
showpage             % print all on the page
```

### Encapuslated PostScript (EPS)
PostScript + encapsulated bitmap preview  
- developed by Adobe - 1987

### Portable Document Format (PDF)
- Adobe Inc. 1993

Based on PostScript
- but no global state, each PDF page independent

Represents complete description of a document
- texts
- fonts
- vector graphics
- raster graphics
- metadata
- form fields
- 3D graphics
- videos
- file attachment
- ESMAScript
- support for encryption


#### PDF/A
Specialized PDF for archiving and long-term preservation

Prohibits some features like
- font linking
- audio
- video
- encryption
- ESMASscript

Convertor: [PDF online](https://pdf.online/pdf-to-pdfaa)

Validator: [veraPDF](https://verapdf.org/)

- PDF/A-1 (2005)
- PDF/A-2 (2011) - attached files either plan text of PDF/A
- PDF/A-3 (2012) - permits arbitrary attachments 
- PDF/A-4 (2020)

#### PDF/X
- reliable print data eXchange
- ISO 15930 2001

#### PDF/UA
- universal accessibility
- ensures accessibility on screen readres and other assistive technologies
- ISO 14289 2012

#### PDF/VT
- based on PDF/X
- variable data and transactional printing
- invoices, marketing documents
(where text needs to be changed in places)
- ISO 16612-2 2010

#### PDF/E
- Engineering documents
- rotating and folding 3D objects in U3D
- ISO 24517 2008

### Adobe Illustrator Artwork (ai)
- from Adobe
- proprietary file format
- stores vector graphics using EPS and PDF
# Bitmap Images
## Bitmap Image Format
- There are numerous variations on the format
- For the purpose of our application, the bitmap will have the following properties
	- 24 bits per pixel (so in paint, `Save as...` -> Other Formats -> 24-bit Bitmap)
	- No alpha channel (No transparency)
	- No compression

## Bitmap File Header
- Block of bytes at the start of the file used to identify the file
- Typical application reads this block first to ensure the file is actually a BMP and not damaged
- First two bytes are `'B'` and `'M'` in ASCII
- All integer values stored in little-endian format
- **header size is 14 bytes**

| Offset (in bytes) | Size (in bytes) | Description                                                                                                                           |
| ----------------- | --------------- | ------------------------------------------------------------------------------------------------------------------------------------- |
| 0                 | 2               | Header field used to identify the BMP and DIB is `0x42` `0x4D` in hex, same as `"BM"` in ASCII. BM used in Windows 3.1x, 95, NT, etc. |
| 2                 | 4               | The size of the BMP in bytes                                                                                                          |
| 6                 | 2               | Reserved; actual value depends on the app that created the image                                                                      |
| 8                 | 2               | Reserved; actual value depends on the app that created the image                                                                      |
| 10                | 4               | Offset (starting location of the byte where the image data (pixel array) can be found)                                                |

## Device Independent Bitmap (DIB) Header
- Bitmap information header
- Tells the application detailed information about the image, which will be used to display the image on the screen
- Block also matches the header used internally by Windows and OS/2 and has several variations
- All of them contain a `DWORD` (32 bit) field specifying their size, so that an application can determine which header is used in the image
- For the purpose of our application, we will use the 40 byte **`BITMAPINFOHEADER`** for Windows NT, 3.1x or later

### `BITMAPINFOHEADER` Format
- All values are stored as **unsigned integers** unless explicitly noted

| Offset (in bytes) | Size (in bytes) | Description                                                                       |
| ----------------- | --------------- | --------------------------------------------------------------------------------- |
| 14                | 4               | Size of this header in bytes (40)                                                 |
| 18                | 4               | Bitmap width in pixels (signed int)                                               |
| 22                | 4               | Bitmap height in pixels (signed int)                                              |
| 26                | 2               | Number of color planes (must be 1)                                                |
| 28                | 2               | Number of bits per pixel, which is color epth.                                    |
| 30                | 4               | Compression method used                                                           |
| 34                | 4               | The T size of the image (size of the raw bitmap data pixel array)                 |
| 38                | 4               | Horizontal resolution of the image (pixels per meter, signed int)                 |
| 42                | 4               | Vertical resolution                                                               |
| 46                | 4               | Number of colors in the color palette, or 0 to default to $2^n$                   |
| 50                | 4               | Number of important colors, or 0 when every color is important, generally ignored |

### Pixel Array
- Following the DIB header is the pixel array
- For this application, it's assumed that the pixel stores a red, green and blue component and each component is 1 byte in size (3 bytes or 24 bits per pixel)
- Note that some images could store 4 bytes per pixel (32 bits) if they have an alpha channel (for transparency)

#### Example

| Pixel 3 | Pixel 4 |
| ------- | ------- |
| Pixel 1 | Pixel 2 |

- What would this image data look like in the file?
- At the end of each row, there might be padding
- Bitmap standard requires that each row ends on a 4-byte boundary
- ![](Pasted%20image%2020250328101459.png)
- How big is this padding? How do we calculate it?
- `Padding (bytes) = image width (pixels) % 4`
- Must consider padding when reading in the image AND when looping through the array of pixels

# Options

Note: The *stack* and *wpc* converters supports the options of its containing converters. Writing this on every option would be tedious, so I have not.

### `autofilter`
```
Type:         boolean
Default:      false
Supported by: cwebp, vips and imagickbinary
```
Turns auto-filter on. This algorithm will spend additional time optimizing the filtering strength to reach a well-balanced quality. Unfortunately, it is extremely expensive in terms of computation. It takes about 5-10 times longer to do a conversion. A 1MB picture which perhaps typically takes about 2 seconds to convert, will takes about 15 seconds to convert with auto-filter. So in most cases, you will want to leave this at its default, which is off.


### `converters`
```
Type:         array
Default:      ['cwebp', 'vips', 'wpc', 'imagickbinary', 'ewww', 'imagick', 'gmagick', 'gmagickbinary', 'gd']
Supported by: stack
```
Converters to try. Each item can be:

- An id (ie "cwebp")
- A fully qualified class name (in case you have programmed your own custom converter)
- An array with two keys: "converter" and "options".

Example:
```php
$options = [
    'quality' => 71,
    'converters' => [
        'cwebp',        
        [
            'converter' => 'vips',
            'options' => [
                'quality' => 72                
            ]
        ],
        [
            'converter' => 'ewww',
            'options' => [
                'quality' => 73               
            ]
        ],
        'wpc',
        'imagickbinary',
        '\\MyNameSpace\\WonderConverter'
    ],
];
```
Alternatively, converter options can be set using the *converter-options* option.

Read more about the stack converter in the [introduction](https://github.com/rosell-dk/webp-convert/blob/master/docs/converting/introduction-for-converting.md#the-stack-converter).


### `converter-options`
```
Type:         array
Default:      []
Supported by: stack
```
Extra options for specific converters. Example for setting quality to 72 for vips:

```php
$options = [
    'quality' => 71,    // will apply to all converters, except vips.
    'converter-options' => [
        'vips' => [
            'quality' => 72
        ],
    ]    
]
```

Alternatively, you can simply do this: (not implemented yet)

```php
$options = [
    'quality' => 71,
    'vips-quality' => 72,
]
```

### `cwebp-command-line-options`
```
Type:         string
Default:      ''
Supported by: cwebp
```
This allows you to set any parameter available for cwebp in the same way as you would do when executing *cwebp*. You could ie set it to "-sharpness 5 -mt -crop 10 10 40 40". Read more about all the available parameters in [the docs](https://developers.google.com/speed/webp/docs/cwebp)


### `default-quality`
```
Type:          integer (0-100)
Default:       75 for jpegs and 85 for pngs
Supported by:  all (cwebp, ewww, gd, gmagick, gmagickbinary, imagick, imagickbinary, vips)
```
Read about this option in the ["auto quality" section in the introduction](https://github.com/rosell-dk/webp-convert/blob/master/docs/converting/introduction-for-converting.md#auto-quality).


### `ewww-api-key`
```
Type:         string
Default:      ''
Supported by: ewww
```
Api key for the ewww converter. PS: This option can alternatively be set through the *EWWW_API_KEY* environment variable.


### `jpeg`
```
Type:          array
Default:       []
Supported by:  all
```
Override selected options when the source is a jpeg. The options provided here are simply merged into the other options when the source is a jpeg.
Read about this option in the [introduction](https://github.com/rosell-dk/webp-convert/blob/master/docs/converting/introduction-for-converting.md#png-og-jpeg-specific-options).


### `lossless`
```
Type:          boolean | "auto"
Default:       "auto" for jpegs and false for pngs
Supported by:  cwebp, imagickbinary, vips  (the other converters always uses lossy encoding)
```
Read about this option in the ["lossy/lossless" section in the introduction](https://github.com/rosell-dk/webp-convert/blob/master/docs/converting/introduction-for-converting.md#auto-selecting-between-losslesslossy-encoding).


### `low-memory`
```
Type:          false
Default:       ''
Supported by:  cwebp, imagickbinary
```
Reduce memory usage of lossy encoding at the cost of ~30% longer encoding time and marginally larger output size. Read more in [the docs](https://developers.google.com/speed/webp/docs/cwebp).


### `max-quality`
```
Type:          integer (0-100)
Default:       85
Supported by:  all (cwebp, ewww, gd, gmagick, gmagickbinary, imagick, imagickbinary, vips)
```
Read about this option in the ["auto quality" section in the introduction](https://github.com/rosell-dk/webp-convert/blob/master/docs/converting/introduction-for-converting.md#auto-quality).


### `metadata`
```
Type:          string ("all" | "none" | "exif" | "icc" | "xmp")
Default:       'none'
Supported by:  'none' is supported by all. 'all' is supported by all, except *gd*. The rest is only supported by *cwebp*
```

Only *cwebp* supports all values. *gd* will always remove all metadata. *ewww*, *imagick* and *gmagick* can either strip all or keep all (they will keep all, unless the option is set to *none*)


### `method`
```
Type:          integer (0-6)
Default:       6
Supported by:  cwebp, imagickbinary
```
This parameter controls the trade off between encoding speed and the compressed file size and quality. Possible values range from 0 to 6. 0 is fastest. 6 results in best quality.


### `near-lossless`
```
Type:          integer (0-100)
Default:       60
Supported by:  cwebp, imagickbinary
```
Specify the level of near-lossless image preprocessing. This option adjusts pixel values to help compressibility, but has minimal impact on the visual quality. It triggers lossless compression mode automatically. The range is 0 (maximum preprocessing) to 100 (no preprocessing). The typical value is around 60. Read more [here](https://groups.google.com/a/webmproject.org/forum/#!topic/webp-discuss/0GmxDmlexek)


### `png`
```
Type:          array
Default:       []
Supported by:  all
```
Override selected options when the source is a png. The options provided here are simply merged into the other options when the source is a png.
Read about this option in the [introduction](https://github.com/rosell-dk/webp-convert/blob/master/docs/converting/introduction-for-converting.md#png-og-jpeg-specific-options).


### `quality`
```
Type:          integer (0-100) | "auto"
Default:       "auto" for jpegs and 85 for pngs
Supported by:  all (cwebp, ewww, gd, gmagick, gmagickbinary, imagick, imagickbinary, vips)
```
Quality for lossy encoding. Read about the "auto" option in the [introduction](https://github.com/rosell-dk/webp-convert/blob/master/docs/converting/introduction-for-converting.md#auto-quality).


### `size-in-percentage`
```
Type:          integer (0-100) | null
Default:       null
Supported by:  cwebp
```
This option sets the file size, *cwebp* should aim for, in percentage of the original. If you for example set it to *45*, and the source file is 100 kb, *cwebp* will try to create a file with size 45 kb (we use the `-size` option). This is an excellent alternative to the "quality:auto" option. If the quality detection isn't working on your system (and you do not have the rights to install imagick or gmagick), you should consider using this options instead. *Cwebp* is generally able to create webp files with the same quality at about 45% the size. So *45* would be a good choice. The option overrides the quality option. And note that it slows down the conversion - it takes about 2.5 times longer to do a conversion this way, than when quality is specified. Default is *off* (null)


### `wpc-api-key`
```
Type:          string
Default:       ''
Supported by:  wpc
```
Note: You can alternatively set the api key through the *WPC_API_KEY* environment variable.


### `wpc-api-version`
```
Type:          integer (0 - 1)
Default:       0
Supported by:  wpc
```

### `wpc-api-url`
```
Type:          string
Default:       ''
Supported by:  wpc
```
Note: You can alternatively set the api url through the *WPC_API_URL* environment variable.


### `wpc-crypt-api-key-in-transfer`
```
Type:          boolean
Default:       false
Supported by:  wpc
```

### `wpc-secret`
```
Type:          string
Default:       ''
Supported by:  wpc
```
Note: This option is only relevant for api version 0.
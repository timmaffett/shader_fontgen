Generates Shadertoy Signed Distance Field (SDF) Image for a specified font.

generate_sdf.html is my wrapper around @otaviogood 's codepage_gen.html which allows you to choose any font from your system for to choose any Google font from a specified category ('monospace' works best probably)

A [live](https://timmaffett.github.io/shadertoy_fontgen/generate_sdf.html) version can be found here : [https://timmaffett.github.io/shadertoy_fontgen/generate_sdf.html](https://timmaffett.github.io/shadertoy_fontgen/generate_sdf.html).


This is the logic for the quality settings
```
      if(quality=='low') {
        sourceSize = 64 | 0;
        divisions = 1.0;
        downSamples = 0;
        gradPrecision = 1 | 0;

        cellSize = 64 | 0;
        targetSize = 1024 | 0;

        tileCount = (targetSize / cellSize) | 0;
      } else if(quality=='medium') { // i made this up
        sourceSize = 64*2 | 0;
        divisions = 2.0;
        downSamples = 1;
        gradPrecision = 2 | 0;

        cellSize = 64 | 0;
        targetSize = 1024 | 0;

        tileCount = (targetSize / cellSize) | 0;
      } else if(quality=='mediumhigh') {  // i made this up
        sourceSize = 64*2*2*2 | 0; // one *2 for every down sample and additional one for cellsize 64->128
        divisions = 3.0;
        downSamples = 2;
        gradPrecision = 4 | 0;

        cellSize = 128 | 0;
        targetSize = 2048 | 0;

        tileCount = (targetSize / cellSize) | 0;
      } else if(quality=='high1024') {  // i made this up
        // otaviogood's settings for high when he generated sdf font for shadertoy:
        //  shadertoy texture is 1024x1024
        // 2048, div 4.0, 3 downsamples, gradPrecision 8
        sourceSize = 64*2*2*2 | 0; // one *2 for every down sample
        divisions = 4.0;
        downSamples = 3;
        gradPrecision = 8 | 0;

        cellSize = 64 | 0;
        targetSize = 1024 | 0;

        tileCount = (targetSize / cellSize) | 0;
      } else {
        // otaviogood's settings for high when he generated sdf font for shadertoy:
        //  (BUT not exaclty this because shadertoy texture is 1024x1024)
        // 2048, div 4.0, 3 downsamples, gradPrecision 8
        sourceSize = 64*2*2*2*2 | 0; // one *2 for every down sample and additional one for cellsize 64->128
        divisions = 4.0;
        downSamples = 3;
        gradPrecision = 8 | 0;

        cellSize = 128 | 0;
        targetSize = 2048 | 0;

        tileCount = (targetSize / cellSize) | 0;
      }
    ```
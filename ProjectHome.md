# Homepage Switch #
**Improvements in the maintenance of this project had leaded in a merger of this project into a multipurpose innovative, creative exciting and amusing multiple purpose c open engine project: openxl http://code.google.com/p/openxl. Consider taking any valuable update or syndication action.**

ml: media library based on opengl and openal

<table width='100%'>
<blockquote><tr>
<blockquote><td align='center'>
<blockquote><wiki:gadget url="http://goo.gl/Uql18" width="728" height="90" border="1" up_ad_client="1499394790009918" up_ad_slot="0061131168" up_ad_width="728" up_ad_height="90" /><br>
</blockquote></td>
</blockquote></tr>
</table></blockquote>


---


# Introduction #

Media Library is a library that displays media streams such as video with sound using accelerated hardware and true tridimensional capabilities (ffmpeg implementation).


---


# Details #

It can be as clean and simple as:
```
...

mlStreamLoadDefault(filepath);
mlStreamConvert(alformat, alfreq, glwidth, glheight, glformat, glsize);

for(i = 0; i< NUM_AUDIO_BUFFERS && !mlStreamAudioEnd(); i++)
        mlStreamConvertBufferChunk(size, bfrs[i]);
alSourceQueueBuffers(src, i, bfrs);
mlStreamReadFrame();
mlStreamSync();
if(mlStreamFrameCheck())
        mlStreamConvertTexSubImage2D(target, level, xoffset, yoffset);
alSourcePlay(src);

while(!mlStreamEnd())
{
        alGetSourcei(src, AL_BUFFERS_PROCESSED, prc);
        alSourceUnqueueBuffers(src, prc, prcs);
        for(i = 0; i < prc && !mlStreamAudioEnd(); i++)
                mlStreamConvertBufferChunk(size, prcs[i]);
        alSourceQueueBuffers(src, i, prcs);
        if(!mlStreamVideoEnd())
        {
                mlStreamReadFrame();
                if(mlStreamFrameCheck())
                        mlStreamConvertTexSubImage2D(target, level, xoffset, yoffset);
        }
}

mlStreamUnload();

...
```

and as powerful as to use the direct stream input formats or convert the stream to the targets, use pixelbuffer objects or texture rectangles, and seek:

```
mlStreamLoadDefault(filepath);
mlStreamInform(&alformat, &alfreq,& glwidth, &glheight, &glformat, &glsize);
mlStreamConvertt(alformat, alfreq, glwidth, glheight, glformat, glsize);

mlStreamBufferChunk(size, bfr);
mlStreamConvertBufferChunk(size, bfr);

mlStreamTexSubImage2D(target, level, xoffset, yoffset);
mlStreamConvertTexSubImage2D(target, level, xoffset, yoffset);

mlStreamBufferTexSubImage2D(target, level, xoffset, yoffset);
mlStreamConvertBufferTexSubImage2D(target, level, xoffset, yoffset);

mlStreamBestTexSubImage2D(target, level, xoffset, yoffset);
mlStreamConvertBestTexSubImage2D(target, level, xoffset, yoffset);

mlStreamSeek(ms);
```


---


<table width='50%' align='center'>
<blockquote><tr>
<blockquote><td align='center'>
<a href='http://www.youtube.com/watch?feature=player_embedded&v=BHPzjpojlz0' target='_blank'><img src='http://img.youtube.com/vi/BHPzjpojlz0/0.jpg' width='425' height=344 /></a><br>
</td>
</blockquote></tr>
<tr>
<blockquote><td align='center'>
<img src='http://openmedialibrary.googlecode.com/files/ml-simple.png' />
</td>
</blockquote></tr>
<tr>
<blockquote><td align='center'>
<img src='http://openmedialibrary.googlecode.com/files/ml-cube.png' />
</td>
</blockquote></tr>
<tr>
<blockquote><td align='center'>
<img src='http://openmedialibrary.googlecode.com/files/ml-player.png' />
</td>
</blockquote></tr>
</table></blockquote>


---


# About #

ml (Media Library) uses and contributes to mkproject technologies:
  * ml (Media Library) was generated with [mkproject (Make Project)](http://code.google.com/p/makeproject) technology


---


# License #

This program is free software: you can redistribute it and/or modify it under the terms of the GNU General Public License as published by the Free Software Foundation, version 3 of the License.

This program is distributed in the hope that it will be useful, but WITHOUT ANY WARRANTY; without even the implied warranty of MERCHANTABILITY or FITNESS FOR A PARTICULAR PURPOSE.  See the GNU General Public License for more details.

You should have received a copy of the GNU General Public License along with this program.  If not, see < http://www.gnu.org/licenses />.


---


<table width='100%'>
<blockquote><tr>
<blockquote><td align='center'>
<blockquote><wiki:gadget url="http://goo.gl/Uql18" width="728" height="90" border="1" up_ad_client="1499394790009918" up_ad_slot="0061131168" up_ad_width="728" up_ad_height="90" /><br>
</blockquote></td>
</blockquote></tr>
</table>
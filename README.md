# What is it?
ImgWizard is a small server written in Go as faster alternative for [thumbor][thumbor]

[thumbor]: https://github.com/thumbor/thumbor

# What it can do?

  - Fetch image from local file system or remote media
  - Resize it
  - Crop it
  - Change quality 
  - Cache resized image to file system and get it on next request
  - Return WebP images if browser supports it

# How to use?

http://{server}/images/{storage}/{size}/{path_to_file}

  - <b>server</b> - imgwizard server addr
  - <b>mark</b> - mark for url (can be used for nginx proxying)
  - <b>storage</b> - "loc" (local file system) or "rem" (remote media)
  - <b>size</b> - "320x240" or "320x" or "x240"
  - <b>path_to_file</b> - path to original file (without "http://")

##### Example: #####

http://<b>192.168.0.1:4444</b>/images/<b>rem</b>/<b>462x</b>/<b>media.google.com/uploads/images/1/test.jpg</b>

# How to install? #

### Installing libvips ###

VIPS is a free image processing system. Compared to similar libraries, VIPS is fast and does not need much memory, see the [Speed and Memory Use][speed] page. As well as JPEG, TIFF, PNG and WebP images, it also supports scientific formats like FITS, OpenEXR, Matlab, Analyze, PFM, Radiance, OpenSlide and DICOM (via libMagick). (&copy; [vips wiki][libvips])

##### Mac OS #####
```$ brew install vips```

##### Debian based #####
```$ sudo apt-get install libvips-dev```

##### RedHat #####
Check [this][centos]

### Installing imgwizard ###
  - ```go get github.com/shifr/imgwizard```
  - ```export PATH=$PATH:$GOPATH/bin``` if you haven't done it before
  
### Running imgwizard ###
  - ```imgwizard``` - run server without restrictions

You will see "<b>ImgWizard started...</b>" 

Check [imgwizard] work after server start 

[imgwizard]: http://localhost:8070/images/rem/320x240/thumbs.dreamstime.com/z/cartoon-wizard-man-23333089.jpg
[centos]: http://astonj.com/tech/how-to-install-vips-on-centos-libvips/
[libvips]: http://www.vips.ecs.soton.ac.uk/index.php?title=VIPS
[speed]: http://www.vips.ecs.soton.ac.uk/index.php?title=Speed_and_Memory_Use

# Parameters on start? #
```imgwizard -l localhost:9000 -c /tmp/my_cache_dir -m media1.com,media2.com -s 100x100,480x,x200 -q 80 -mark imgw -thumb /path_to_404_image.jpg```

  - <b>-l</b>: Address to listen on (default - "localhost:8070")
  - <b>-c</b>: directory for cached files (default - "/tmp/imgwizard")
  - <b>-m</b>: comma separated list of allowed media (default - all enabled)
  - <b>-s</b>: comma separated list of allowed sizes (default - all enabled)
  - <b>-q</b>: resized image quality (default - 80)
  - <b>-mark</b>: mark (default - images)
  - <b>-thumb</b>: default image if requested doesn't exists (default - /tmp/404.jpg)


# Plans? #
Yes, a lot.

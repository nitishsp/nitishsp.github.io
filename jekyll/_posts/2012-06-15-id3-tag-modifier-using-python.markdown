---
layout: post
title: "ID3 Tag Modifier using Python"
---

I was organizing my mp3 library & I noticed that a lot of meta-information was not in proper case. As I am learning python, I decided to test whether mp3 metadata could be modified using python program. After an hour spent googling and coding, finally I have a simple program that changes title, artist and album information of mp3 files in 'Title' case. The program uses [eyeD3](http://eyed3.nicfit.net/) library to acess ID3 metadata.

{% highlight python %}
import eyeD3
import os
import fnmatch
#---------------------------------------------
def modifyEyeD3Tags(path):
    tag = eyeD3.Tag()
    tag.link(path)

    song_artist = tag.getArtist()
    song_album = tag.getAlbum()
    song_title = tag.getTitle()
    """
    print song_artist
    print song_album
    print song_title
    """
    song_artist=song_artist.title()
    song_album=song_album.title()
    song_title=song_title.title()

    tag.setArtist(song_artist)
    tag.setAlbum(song_album)
    tag.setTitle(song_title)
    tag.update()
    """
    print song_artist
    print song_album
    print song_title
    """

directory = os.path.dirname(os.path.realpath(__file__))
print "Directory => ",directory
files_list = os.listdir(directory)
print "Starting Tag Modification"
for x in files_list:
    if fnmatch.fnmatch(x, '*.mp3'):
        print "File:",x
        modifyEyeD3Tags(x)
print "Finished Tag Modification"
{% endhighlight %}

The program first obtains the path of the directory in which the python source file resides. Then it fetches names of all the files in that directory into a list. Then it traverses the list and passes mp3 filenames to modifyEyeD3Tags() function. The modifyEyeD3Tags() function performs the actual case change operation.

The programs performs very trivial task and perhaps has no practical use (apart from aesthetically enhancing ID3 tags :p ) but I learned a few things in python and that's all that matters!

References:

+ [http://stackoverflow.com/questions/8948/accessing-mp3-meta-data-with-python](http://stackoverflow.com/questions/8948/accessing-mp3-meta-data-with-python)
+ [http://www.blog.pythonlibrary.org/2010/04/22/parsing-id3-tags-from-mp3s-using-python/](http://www.blog.pythonlibrary.org/2010/04/22/parsing-id3-tags-from-mp3s-using-python/)
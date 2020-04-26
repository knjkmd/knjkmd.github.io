# Build from source
Followed the instruction here.

http://htmlpreview.github.io/?https://raw.github.com/qgis/QGIS/master/doc/INSTALL.html

## What is `ccache`?
>Ccache (or “ccache”) is a compiler cache. It speeds up recompilation by caching previous compilations and detecting when the same compilation is being done again. Ccache is free software, released under the GNU General Public License version 3 or later. See also the license page.

https://ccache.dev/

The instruction page recommends to do this.
```
cd /usr/local/bin
sudo ln -s /usr/bin/ccache gcc
sudo ln -s /usr/bin/ccache g++
```

From `ccache` documentation.
> There are two ways to use ccache. You can either prefix your compilation commands with ccache or you can let ccache masquerade as the compiler by creating a symbolic link (named as the compiler) to ccache. The first method is most convenient if you just want to try out ccache or wish to use it for some specific projects. The second method is most useful for when you wish to use ccache for all your compilations.

So it's the second way.


## What is `LD_LIBRARY_PATH`?
> LD_LIBRARY_PATH is the search path environment variable for the linux shared library. In Linux, the environment variable LD_LIBRARY_PATH is a colon-separated (:) set of directories where libraries are searched for first before the standard set of directories.
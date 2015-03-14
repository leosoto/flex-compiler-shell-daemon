# Fast Flex Compiler, without the interactive (and blocking!) shell. #

## Usage ##

```
$ fcshd.py "mxmlc /path/to/foo.mxml -o /path/to/foo.swf"
 Loading configuration file [...]
[...]
/path/to/foo.swf (349854 bytes)
(fcsh)

$ fcshd.py "mxmlc /path/to/foo.mxml -o /path/to/foo.swf"
 Loading configuration file [...]
Nothing has changed since the last compile. Skip...
/path/to/foo.swf (349854 bytes)
(fcsh)
```

## Why? ##

If you do flex development outside Flex Builder (very likely if you use Linux, as the official Flex Builder is quite buggy there), using the command line mxmlc is a painfully sloooooow.

Fortunately, Adobe released a tool called the [Flex Compiler Shell](http://labs.adobe.com/wiki/index.php/Flex_Compiler_Shell), abbreviated as fcsh, which speeds up the compilation time considerably.

Unfortunately, fcsh doesn't work well when you want to integrate fcsh with the common build toolchains, where the compiler is expected to compile the source _and exit_ (with at least a non-zero exit code if the compilation failed, of course).

Here is a simple solution to the problem: "The Flex Compiler Shell Daemon", or fcshd for short. It basically wraps the fcsh in a daemonized process, and calls that server process when you invoke it from the command line. The daemon is automatically started the first time you use fcshd, of course.

Bottom line: You get _fast_ compilation and _familiar interface_, easy to integrate to build tools like rake, or text editor plugins such as Emacs/Flymake.

## Installation ##

Just copy [fcshd.py](http://flex-compiler-shell-daemon.googlecode.com/svn/trunk/fcshd.py) into a directory which is in on your `PATH`
# Debugging

## General <a href="#trace-options" id="trace-options"></a>

If you use the packaged version of tvheadend, make sure that you use the debug version of tvheadend (with the debugging symbols). For debian/ubuntu these packages have **-dbg** suffix, for rpm packages, these symbols are in **debuginfo** rpm files.

If you're going to be regularly trying development versions of Tvheadend or need to report a crash or deadlock then you should really read this page!

If you are investigating problems within Tvheadend then its worth being familiar with tools such as gdb and valgrind or clang, although these are not covered here.

However one thing that can be useful in investigating crashes within Tvheadend is to ensure that coredumps are generated, this will allow post analysis in gdb without having to actual run Tvheadend within gdb.

You can enable temporarily by running:

```
ulimit -c unlimited
```

To make this permanent put this somewhere in your shell environment setup (.bashrc, .profile, etc...)\
Firstly I'd recommend that if you're specifically trying to investigate an issue then you should consider running Tvheadend manually, rather than as a service, as documented below.

## Logging

I'd strongly recommend that if you're specifically trying to investigate a crash or other problem in Tvheadend that you enable debugging:

* **-s** will output debug info to syslog
* **--debug** allows you to specify which subsystem to debug&#x20;
* **--trace** allows you to enable trace (more in-depth) logging on specific subsystems

You can also get Tvheadend to log to it's own file using:

```
-l FILE
```

You may also modify the debug settings using WEB GUI as admin - Configuration/Debugging. Note that the information is not saved,\
it is just set for run-time (current task).

* Debug log path - filename to store log
* Debug trace - enable traces
* Debug subsystems - comma separated list of subsystems
* Trace subsystems - comma separated list of subsystems

The traces must be compiled to the tvheadend binary (see below).

### Trace Options <a href="#trace-options" id="trace-options"></a>

The following options can be passed to tvheadend to provide detailed debugging information while the application is running. Trace debugging has to be enabled at build time with`--enable-debugging` and can be specified in a CLI command, e.g. `tvheadend -u hts -g video --trace <module>` or in the web interface (_Configuration -> Debugging_).

Multiple options can be used, e.g. `–-trace cwc,dvr,linuxdvb`

```
START
STOP
CRASH
main
tprof
qprof
CPU
thread
tvhpoll
time
spawn
fsmonitor
lock
uuid
idnode
url
tcp
rtsp
upnp
settings
config
access
cron
dbus
avahi
bonjour
api
http
httpc
htsp
htsp-sub
htsp-req
htsp-ans
imagecache
tbl
tbl-base
tbl-csa
tbl-eit
tbl-time
tbl-atsc
tbl-pass
tbl-satip
fastscan
pcr
parser
TS
globalheaders
tsfix
hevc
muxer
pass
audioes
mkv
service
channel
subscription
service-mapper
bouquet
esfilter
profile
descrambler
descrambler-emm
caclient
csa
capmt
cwc
cccam
dvbcam
dvr
dvr-inotify
epg
epgdb
epggrab
charset
dvb
mpegts
muxsched
libav
transcode
iptv
iptv-pcr
iptv-sub
linuxdvb
diseqc
en50221
en50494
satip
satips
tvhdhomerun
psip
opentv
pyepg
xmltv
webui
timeshift
scanfile
tsfile
tsdebug
codec
vaapi
ddci
udp
ratinglabels
```

## Crash reports

### Incorrect (not useable) crash reports

```
Jun  6 15:01:08 srv tvheadend[10808]: CRASH: Signal: 11 in PRG: /usr/bin/tvheadend (4.3-193~ga4ff519) [15a15a895adaf9c5760b80707f582c2d60cfab01] CWD: /
Jun  6 15:01:08 srv tvheadend[10808]: CRASH: Fault address 0x90 (Address not mapped)
Jun  6 15:01:08 srv tvheadend[10808]: CRASH: STACKTRACE
Jun  6 15:01:08 srv tvheadend[10808]: CRASH: ??:0 0x555558549eba 0x555558350000
Jun  6 15:01:08 srv tvheadend[10808]: CRASH: ??:0 0x7f3d97c0c0c0 0x7f3d97bfb000
Jun  6 15:01:08 srv tvheadend[10808]: CRASH: ??:0 0x555558525620 0x555558350000
Jun  6 15:01:08 srv tvheadend[10808]: CRASH: ??:0 0x5555585257a8 0x555558350000
Jun  6 15:01:08 srv tvheadend[10808]: CRASH: ??:? 0x5555585db371 0x555558350000
Jun  6 15:01:08 srv tvheadend[10808]: CRASH: ??:? 0x5555585dc1f2 0x555558350000
Jun  6 15:01:08 srv tvheadend[10808]: CRASH: ??:? 0x5555585c3212 0x555558350000
Jun  6 15:01:08 srv tvheadend[10808]: CRASH: ??:? 0x5555585bb71d 0x555558350000
Jun  6 15:01:08 srv tvheadend[10808]: CRASH: ??:? 0x5555585bb8d1 0x555558350000
Jun  6 15:01:08 srv tvheadend[10808]: CRASH: ??:0 0x5555585b4589 0x555558350000
Jun  6 15:01:08 srv tvheadend[10808]: CRASH: ??:0 0x5555585b4796 0x555558350000
Jun  6 15:01:09 srv tvheadend[10808]: CRASH: ??:0 0x555558511e44 0x555558350000
Jun  6 15:01:09 srv tvheadend[10808]: CRASH: ??:0 0x7f3d97c02494 0x7f3d97bfb000
Jun  6 15:01:09 srv kernel: [2320412.837462] tvh:mi-table[11208]: segfault at 90 ip 0000555558525620 sp 00007f3d85ff0b98 error 4 in tvheadend[555558350000+10d1000]
```

In this case, the debug symbols are missing (look to the top of this page). Install the debug version of the tvheadend package.

### Correct crash reports

```
2017-06-06 17:36:53.626 [  ALERT] CRASH: Signal: 6 in PRG: ./build.linux/tvheadend (4.3-195~gf476b37-dirty) [d761557cdfcd10940d79f8758376fadda7e49e8c] CWD: /home/tvheadend/git/tvheadend  
2017-06-06 17:36:53.626 [  ALERT] CRASH: Fault address 0x311100002adf (N/A)
2017-06-06 17:36:53.626 [  ALERT] CRASH: STACKTRACE
2017-06-06 17:36:53.626 [  ALERT] CRASH: backtrace+0x41  (./build.linux/tvheadend)
2017-06-06 17:36:53.643 [  ALERT] CRASH: /home/tvheadend/git/tvheadend/src/trap.c:148 0x5584f45ad4ef 0x5584f3d72000
2017-06-06 17:36:53.666 [  ALERT] CRASH: ??:0 0x7f1afde155c0 0x7f1afde04000
2017-06-06 17:36:53.666 [  ALERT] CRASH: gsignal+0x9f  (/lib64/libc.so.6)
2017-06-06 17:36:53.666 [  ALERT] CRASH: abort+0x16a  (/lib64/libc.so.6)
2017-06-06 17:36:53.690 [  ALERT] CRASH: /home/tvheadend/git/tvheadend/src/main.c:1267 0x5584f4462996 0x5584f3d72000
2017-06-06 17:36:53.690 [  ALERT] CRASH: __libc_start_main+0xf1  (/lib64/libc.so.6)
```

### Basic crash debug

You may run tvh in gdb directly using command:

```
gdb --args /the standard tvh command line/

(gdb) run
```

Or attach gdb to the running process:

```
gdb tvheadend pid

(gdb) continue
```

The 'continue' command will continue the execution of the program. If you need to _break_ the execution and return to gdb, just use 'Ctrl-C'.

You may need to replace _tvheadend_ with the full path to the binary and you will need to replace _pid_ with the PID of the running process. To find that run:

```
ps -C tvheadend
```

Once you have gdb attached grab a stack trace from every thread using the following command:

```
(gdb) set logging on
(gdb) set pagination off
(gdb) bt full
```

Note: "set logging on" will cause GDB to write its output to a file, by default this will be gdb.txt in the current directory.

### Enabling coredumps

If you need to investigate some running problem you can always attach (see below) later and if you need to trap crashes, then you can configure your system to generate a core file and then retrospectively analyse this with gdb.

If you're running manually you should enable coredumps in your environment:

```
ulimit -c unlimited
```

I'd recommend you enable this permanently by putting this command in your shell initialisation scripts (.bashrc etc..).

If you're running as a daemon then you should use the -D command line option, this will enable coredumps from the daemon. If you start using sysvinit, upstart etc... then you will need to put this in the configuration file, e.g.:

```
TVH_ARGS="-D" 
```

Finally it's probably worth changing the coredump file format, personally I use the following configuration:

```
echo core.%h.%e.%t | sudo tee /proc/sys/kernel/core_pattern
echo 0 | sudo tee /proc/sys/kernel/core_uses_pid
```

Or put the following in /etc/sysctl.conf:

```
kernel.core_pattern = core.%h.%e.%t
kernel.core_uses_pid = 0
```

If you're using a system like Ubuntu that uses apport (and cripples the ability to change the core format) just set core\_uses\_pid=1 instead.

Note: coredumps are (by default) stored in the current working directory, to make it possible for the daemon to write files the current working directory is set to /tmp when using -D, so check there for core files.

To verify that you have everything configured properly you can use the -A option to force a crash on startup. Do this from the command line or add to /etc/default/tvheadend:

```
TVH_ARGS="-D -A" 
```

Note: remember to remove the option after you've tested it!

### Processing core file.

Once you have a core file you can start up gdb with that coredump, just as if you'd caught the crash while running under gdb:

```
gdb tvheadend core
```

You may need to replace _tvheadend_ and _core_ above with the proper paths.

For most crashes the most useful information is the back trace, this will provide a stack trace showing where the code crashed and the stack information at the time of the crash:

```
(gdb) set logging on
(gdb) set pagination off
(gdb) bt full
#0  0x00007f5b10cc1425 in __GI_raise (sig=<optimised out>)
    at ../nptl/sysdeps/unix/sysv/linux/raise.c:64
        resultvar = 0
        pid = <optimised out>
        selftid = 7517
#1  0x00007f5b10cc4b10 in __GI_abort () at abort.c:120
        act = {__sigaction_handler = {sa_handler = 0, sa_sigaction = 0}, 
          sa_mask = {__val = {18446744073709551615 <repeats 16 times>}}, 
          sa_flags = 0, sa_restorer = 0}
        sigs = {__val = {32, 0 <repeats 15 times>}}
#2  0x000000000040744e in main (argc=<optimised out>, argv=<optimised out>)
    at src/main.c:810
        i = <optimised out>
        set = {__val = {16386, 0 <repeats 15 times>}}
        adapter_mask = <optimised out>
        log_level = <optimised out>
        log_options = <optimised out>
        log_debug = <optimised out>
        log_trace = <optimised out>
        buf = "/tmp\000\000\000\000\360\350\364\023[\177\000\000\000\320\365\023[\177\000\000t\n\327\023[\177\000\000\370\271\311\020[\177\000\000\017\000\000\000\000\000\000\000:\000\000\000\000\000\000\000h\344\364\023[\177\000\000.N=\366\000\000\000\000\236\022\327\023[\177\000\000\300\304S\205\377\177\000\000.\000\000\000\000\000\000\000 \305S\205\377\177\000\000\377\377\377\377\000\000\000\000\264\352\310\020[\177\000\000\250\354\310\020[\177\000\000\360\304S\205\377\177\000\000\360\350\364\023[\177\000\000@\256\311\020[\177", '\000' <repeats 18 times>"\340, \346\364\023[\177\000\000\000\320\365\023[\177\000\000\231,@\000\000\000\000\000\370\271\311\020[\177\000\000\340\033@\000\000\000\000\000\000\000\000\000\001\000\000\000\021\b\000\000\001", '\000' <repeats 11 times>, " \266\370\023[\177\000\000`\305S\205\377\177\000\000.N=\366\000\000\000\000\340\346\364\023[\177\000\000\200\305S\205\377\177\000\000"...
        opt_help = 0
        opt_version = 0
        opt_fork = 1
        opt_firstrun = 0
        opt_stderr = 0
        opt_syslog = 0
        opt_uidebug = 0
```

Note: "set logging on" will cause GDB to write its output to a file, by default this will be gdb.txt in the current directory.

However I'd strongly recommend that you keep a copy of tvheadend binary and core file in case further analysis is required.

## Dead or Live Lock

If Tvheadend appears to die but the process is still running, then its quite possible that the process is deadlocked (or possibly live locked).

### Buildin deadlock mutex checker (since latest 4.3 version)

Use '--thrdebug 1' as the command line option. The deadlock will be printed to the tvheadend's configuration directory to file **mutex-deadlock.txt** and to the standard task error output (so you can see it through the systemctl service log for example).

### GDB

The best way to help investigate such a problem is to get a full stack trace from every thread in the system.

First attach gdb to the running process:

```
gdb tvheadend pid

(gdb) continue
```

The 'continue' command will continue the execution of the program. If you need to _break_ the execution and return to gdb, just use 'Ctrl-C'.

You may need to replace _tvheadend_ with the full path to the binary and you will need to replace _pid_ with the PID of the running process. To find that run:

```
ps -C tvheadend
```

Once you have gdb attached grab a stack trace from every thread using the following command:

```
(gdb) set logging on
(gdb) set pagination off
(gdb) thread apply all bt full
```

Note: "set logging on" will cause GDB to write its output to a file, by default this will be gdb.txt in the current directory.

It might also be useful to generate a core file for good measure:

```
(gdb) generate-core-file
```

This information may give an indication as to why things are locked, often 2 threads are stuck trying to lock a mutex (probably each holds the opposite lock).

## Reporting crash (or lock)

If you're going to report a crash (or lockup) then please try to provide the above information, including a debug log (or whatever logging you have), a core file and the tvheadend binary and basic information about the platform (distribution, version and architecture) you're running on.

## Memory leaks or corruption

It may be really difficult to track these problems. There are basically two tools which may help to discover the memory leaks or memory corruptions.

### Valgrind

It is very slow, but it may be useable for things which are triggered everytime:

```
valgrind --suppressions=support/valgrind.supp --leak-check=full --show-reachable=yes /tvh_command_line/
```

### clang

There is address and leak sanitizer in the clang toolkit.

The clang / llvm tools are usually split to multiple packages, here is list of required packages for Fedora 26:

```
llvm
clang
libasan
liblsan
```

The binary must be rebuild using the clang compiler and libraries:

```
ARGS="/your_configure_arguments/" 
SANITIZER=leak # or address
export CFLAGS="-fsanitize=$SANITIZER" 
export LDFLAGS="-fsanitize=$SANITIZER" 
./configure $ARGS --disable-pie --enable-ccdebug python=python3 cc=clang ld=clang nowerror
make -j4
```

Example build script (build\_with\_clang.sh):

```
#!/bin/sh
make distclean
ARGS="--enable-libffmpeg_static --disable-hdhomerun_static" 
SANITIZER=leak # or address
export CFLAGS="-fsanitize=$SANITIZER" 
export LDFLAGS="-fsanitize=$SANITIZER" 
./configure $ARGS --disable-pie --enable-ccdebug python=python3 cc=clang ld=clang nowerror
make -j4
```

Make sure to make your script executable.

If you do not see resolved the function names like:

```
==16673==WARNING: Trying to symbolize code, but external symbolizer is not initialized!
    #0 0x7fcda9407680 (/home/tvh/src/tvheadend/build.linux/tvheadend+0x65b680)
    #1 0x7fcda943b115 (/home/tvh/src/tvheadend/build.linux/tvheadend+0x68f115)
```

get the correct path for the llvm-symbolizer, i.e. with\


```
whereis llvm-symbolizer
```

then make sure that you set the external symbolizer like:

```
ASAN_OPTIONS=symbolize=1 ASAN_SYMBOLIZER_PATH=/usr/bin/llvm-symbolizer /home/ts/workspace/tvheadend/build.linux/tvheadend -l thv.log
```

The error log should be like:

```
==27911==ERROR: AddressSanitizer: heap-use-after-free on address 0x60700000d928 at pc 0x56409f916af4 bp 0x7ffc463d6670 sp 0x7ffc463d6668
READ of size 8 at 0x60700000d928 thread T0
    #0 0x56409f916af3 in idnode_unlink /home/tvh/git/tvheadend/src/idnode.c:164:94
    #1 0x56409f9c9f8a in memoryinfo_unregister /home/tvh/git/tvheadend/src/memoryinfo.h:52:3
    #2 0x56409f9c9de2 in streaming_done /home/tvh/git/tvheadend/src/streaming.c:597:3
```

## Mutex profiling

The code blocks are protected using mutexes. Tvheadend has the debug interface to show locks which took too much time now (latest 4.3 code). Use '--thrdebug 10020' where 20 means 20 millisecond threshold to show the problematic mutexes. The output is printed to standard error file descriptor (stderr) by default. If you run tvheadend using systemctl or initd, you may send those messages to a UDP port. Set the TVHEADEND\_RTLOG\_UDP\_PORT environment variable like:

```
... console 1
$ export TVHEADEND_RTLOG_UDP_PORT=7777
$ ./build.linux/tvheadend --thrdebug 10020 <more-options>
... console 2
$ nc -lu -p 7777
```

The result should look like:

```
thread: mutex 0x5562f9f859e0 at src/api/api_idnode.c:134 took 43ms
thread: mutex 0x5562f9f859e0 at src/api/api_idnode.c:134 took 31ms
```


# Notes on systems

### Resources
- [The GNU C Library](https://www.gnu.org/software/libc/manual/html_node/index.html)
- [Advanced C++ (Can Skip this for now)](http://aszt.inf.elte.hu/~gsd/halado_cpp/index.html)
- [C++ FAQ](http://yosefk.com/c++fqa/index.html)
- [C FAQ](http://c-faq.com)
- [UNIX System Calls and Subroutines using C](http://users.cs.cf.ac.uk/Dave.Marshall/C/)
- [Linux Kernel Module Cheatsheet](https://github.com/cirosantilli/linux-kernel-module-cheat) (Don't know what this is, will be useful someday)
- [Unix Signal Resources](https://gist.github.com/geekodour/93552b2f382e99b3d14ddc5c464f6c50)
- [Code Samples (Skip for now i'd say)](https://gist.github.com/geekodour/93552b2f382e99b3d14ddc5c464f6c50)
- [Actual and good kernel dev guide](http://www.osdever.net/bkerndev/Docs/intro.htm)
- [Linux Insides Book](https://0xax.gitbooks.io/linux-insides/content/)
- [Graphviz Intro](https://www.worthe-it.co.za/programming/2017/09/19/quick-introduction-to-graphviz.html)
- [Things every hacker knew](http://www.catb.org/esr/faqs/things-every-hacker-once-knew/)
- [Computer Science Triva Latency Numbers](https://keon.io/computer-scientists-trivia/)
- [writing c libraries](https://www.cs.swarthmore.edu/~newhall/unixhelp/howto_C_libraries.html)
- [Structure Packaging](http://www.catb.org/esr/structure-packing/)

### Tools
- [Function pointers](http://fuckingfunctionpointers.com)
- [CDECL](https://cdecl.org)

### Level 0
- This is a refresher of C
    - [ ] Do relevant worksheets
    - [ ] [How to C](https://matt.sh/howto-c)
    - [ ] [Refresher Notes](https://www.cs.uic.edu/~jbell/CourseNotes/C_Programming/index.html)
    - [ ] [Function Pointer example](http://sites.harvard.edu/~lib215/reference/programming/color_test.c)
    - [ ] [Style Notes on Programming in C](http://sites.harvard.edu/~lib215/reference/programming/pikestyle.html)
    - [ ] [Some Philosophy](http://sites.harvard.edu/~lib215/reference/programming/unix-esr.html)
    - [ ] [C Puzzles](http://www.gowrikumar.com/c/index.php)
    - [ ] [K splice Challenge](https://blogs.oracle.com/linux/the-ksplice-pointer-challenge-v2)
    - [ ] [Writing C Programs](http://seenaburns.com/building-c-programs/)
    - [ ] [Building C Programs](http://nethack4.org/blog/building-c.html)
    - [ ] [Assert in hands of bad coders](https://blog.erratasec.com/2017/03/assert-in-hands-of-bad-coders.html)
- Makefile
    - [ ] [Tutorial I](http://makefiletutorial.com)
    - [ ] [Tutorial II](http://gromnitsky.users.sourceforge.net/articles/notes-for-new-make-users/)
- GDB Tutorials
    - [GDB Tutorial](http://www.unknownroad.com/rtfm/gdbtut/gdbtoc.html)
    - [GDB tricks](https://blogs.oracle.com/ksplice/8-gdb-tricks-you-should-know)
    - [Learning C with GDB](https://www.recurse.com/blog/5-learning-c-with-gdb)
    - [Valgrind and GDB](https://fau.re/blog/20140330_vgdb.html)
    - [Practical GDB using ncurses](http://www.brendangregg.com/blog/2016-08-09/gdb-example-ncurses.html)
    - [gdb and coredump](https://jvns.ca/blog/2018/04/28/debugging-a-segfault-on-linux/)
- MOOCs (Just do the assignments and you're done)
    - [ ] [Practical Programming in C]( https://ocw.mit.edu/courses/electrical-engineering-and-computer-science/6-087-practical-programming-in-c-january-iap-2010/index.htm)
    - [ ] [Intro to memory management in C (only do memory management extercise)]( https://ocw.mit.edu/courses/electrical-engineering-and-computer-science/6-088-introduction-to-c-memory-management-and-c-object-oriented-programming-january-iap-2010/index.htm)

### Level 1
- MOOC
    - [ ] [Intro to Computer Systems 213 Homepage](https://www.cs.cmu.edu/~213/schedule.html)
    - [ ] [Intro to Computer Systems 213 YT](https://www.youtube.com/playlist?list=PLpIxOj-HnDsPZIJYO4U9f-xRI8bBadaso)
    - Book for this mooc is CSAPP
    - [Binary Bomb Solution P1](https://archive.is/DDdeT)
    - [Binary Bomb Solution P2]( https://web.archive.org/web/20160314033730/http://blog.carlosgaldino.com/2015/11/19/defusing-a-binary-bomb-with-gdb-part-2.html)
    - [Binary Bomb Solution P3]( https://web.archive.org/web/20160314033758/http://blog.carlosgaldino.com:80/2015/12/03/defusing-a-binary-bomb-with-gdb-part-3.html)
- Blogposts
    - [ ] [How does a segfault occur](https://unix.stackexchange.com/questions/257598/how-does-a-segmentation-fault-work-under-the-hood)
    - [ ] [Memory](http://marek.vavrusa.com/memory/)

### Level 2
- Tutorials
    - [ ] [Learning C by learning assembly](https://www.recurse.com/blog/7-understanding-c-by-learning-assembly)
    - [ ] [Green Threads Tutorial](http://c9x.me/articles/gthreads/intro.html)
    - [ ] [Beej guide to IPC](http://beej.us/guide/bgipc/html/multi/index.html)
    - [ ] [What is the dbus](https://techbase.kde.org/Development/Tutorials/D-Bus/Introduction)
    - Tracing
        - [ ] [Primer to Linux Tracing](https://jvns.ca/blog/2017/07/05/linux-tracing-systems/)
        - [ ] [Choosing a tracer](http://www.brendangregg.com/blog/2015-07-08/choosing-a-linux-tracer.html)
        - [ ] [Linux Tracing Workshop](https://github.com/goldshtn/linux-tracing-workshop)
        - [ ] [Notes on bpf and ebpf](https://jvns.ca/blog/2017/06/28/notes-on-bpf---ebpf/)
        - [ ] [Linux Performance Tracing](http://www.brendangregg.com/linuxperf.html)
        - [ ] [Introduction to strace](https://jorge.fbarr.net/2014/01/19/introduction-to-strace/)
        - [ ] [How does strace work](https://blog.packagecloud.io/eng/2016/02/29/how-does-strace-work/)
    - Profiling
        - [ ] [What is profiling](http://www.pixelbeat.org/programming/profiling/)
    - Concurrency
        - [ ] [Introduction to concurrency](http://cs.lmu.edu/~ray/notes/introconcurrency/)
        - [ ] [Concurrency primer](https://drive.google.com/open?id=1msGTeCIV0ZfHefb_MpHZDZqv8qcGnhEU)
        - [ ] [Concurrency VS Parallel](http://yosefk.com/blog/parallelism-and-concurrency-need-different-tools.html)

### Level 3
- Tutorials
    - [ ] [Using select(2) in Linux](http://aivarsk.github.io/2017/04/06/select/)
    - [ ] [Understanding linux load average](http://www.brendangregg.com/blog/2017-08-08/linux-load-averages.html)


- Rabbitholes
    - [ ] [MOTD Art](https://tylercipriani.com/blog/2014/05/22/creating-baller-useful-motd-ascii-art/)
    - [ ] [Programming the Framebuffer](https://cmcenroe.me/2018/01/30/fbclock.html)
    - [ ] [Writing to framebuffer](http://seenaburns.com/2018/04/04/writing-to-the-framebuffer/)
    - [ ] [Low level graphics](http://betteros.org/tut/graphics1.php)
    - [ ] [Project Ideas I](http://sites.harvard.edu/~lib215/hw/)
    - [ ] [Fork can fail](http://rachelbythebay.com/w/2014/08/19/fork/)

### Level 4
- Contributing to the kernel
    - [ ] Read Rober Love's book
    - [ ] [Eudyotula Challenge](http://eudyptula-challenge.org/)
    - [ ] [Kernel Newbies](https://kernelnewbies.org)
    - [ ] [Ops Class](https://www.ops-class.org/)
    - [ ] [Quickly Writing a Kernel(Not really a kernel)](https://arjunsreedharan.org/post/82710718100/kernel-101-lets-write-a-kernel)
    - [ ] [Writing Kernels](https://www.cs.vu.nl/~herbertb/misc/writingkernels.txt)
    - [ ] [Starting Kernel dev](https://brennan.io/2016/10/13/kernel-dev-ep1/)

- System Calls
    - [ ] [Write a system call](https://brennan.io/2016/11/14/kernel-dev-ep3/)
    - [ ] [Linux system calls](https://blog.packagecloud.io/eng/2016/04/05/the-definitive-guide-to-linux-system-calls/)
- All about systemd
    - [ ] [Escape from systemd](https://davmac.wordpress.com/2017/06/14/escape-from-system-d/)
    - [ ] [Why i dislike systemd](https://lobste.rs/s/vzjalp/why_i_dislike_systemd)

### Level 5
- Tutorials
    - [C/C++ Memory Model](https://davmac.wordpress.com/2018/01/28/understanding-the-c-c-memory-model/)
    - [Shared libs Internals](https://amir.rachum.com/blog/2016/09/17/shared-libraries/)
- Assembly
    - [Nice short guide to x86](https://www.nayuki.io/page/a-fundamental-introduction-to-x86-assembly-programming)
    - [Learning to read assembly](http://patshaughnessy.net/2016/11/26/learning-to-read-x86-assembly-language)
    - [x86 Guide](http://www.cs.virginia.edu/~evans/cs216/guides/x86.html)
- Reverse engg
    - [Exercises](https://github.com/wapiflapi/exrs)

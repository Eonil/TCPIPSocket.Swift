**WARNING** [According to Apple's guideline](https://github.com/Eonil/TCPIPSocket.Swift/issues/1), accessing network socket using `NSFileSHandle` may cause some unknown failures. You still can do that, but I don't recommend it. Instead, use `NSStream` and `CFStream` or [`CFStreamCreatePairWithSocket`](http://stackoverflow.com/questions/9902707/ios-getting-cfreadstream-cfwritestream-from-a-socket). You still can use my library to make an established socket connection for those features. I will update my library as soon as possible if I can make some time.

Eonil/TCPIPSocket.Swift
=======================
2015/01/19
Hoon H.


Provides simple, regular, thin, synchronous, asynchronous and minimal TCP/IP socket wrapper on Swift.

This just wraps BSD socket as is, and does not try to add any extra abstraction.
I believe this can serve any applications, but I intended this for quicky apps. 








How To Use
----------
This is a single file library.
`TCPIPSocket.swift` file into your project.
Here's an example that performs an HTTP request.

````swift
	let	s	=	TCPIPSocket()
	let	f	=	NSFileHandle(fileDescriptor: s.socketDescriptor)

	s.connect(TCPIPSocketAddress(173, 194, 127, 231), 80)
	f.writeData(("GET / HTTP/1.0\n\n" as NSString).dataUsingEncoding(NSUTF8StringEncoding)!)
	let	d	=	f.readDataToEndOfFile()

	println(NSString(data: d, encoding: NSUTF8StringEncoding)!)
````

The `TCPIPSocket` class is the core. And it does not provide any I/O methods. 
Instead create and use `NSFileHandle` class to perform actual I/O.

Though this library is originally intended to provide synchronous interface, 
but also provides asynchronous I/O through `NSFileHandle`'s asynchronous interface.
See `main.swift` for example.



Requirements
------------
-	Swift 1.2.





"No"s
---------
-	No I/O functions. Unix can use same I/O functions for sockets and files. And there's
	no reason to add duplicated functions. Instead, use `NSFileHandle` class to perform I/O.
	If you have some existing codebase with `NSFileHandle` class, it will become available 
	for free.

-	No DNS resolution. Do it yourself if you need it.

-	No any other socket mode. Strictly only for TCP/IP. No UDP, no raw, and no any other 
	protocol I never have heard of its name in recent 10 years...







Missings
--------
-	IPv6 support is a desired feature, but I have no time to work on it. It will be added 
	when I feel need for it.

-	Some fundamental socket functions such as `select`. This also will be added when I 
	feel need for it.

-	DNS resolution service. As a separated feature rather than a part of API.






License
-------
Licensed under MIT license.
This library is written by Hoon H., and hosted on [Github](https://github.com/Eonil/TCPIPSocket.Swift).

Copyright(c) Hoon H.. All rights reserved.






---
type: mina
title: News
---

# News

## MINA 2.1.4 released _posted on August, 24, 2020_

The MINA project is pleased to announce a new release, MINA 2.1.4. This is a bug fix release. Here are the fixed issues :

Bugs

* DIRMINA-966    NIO Datagram messages can get duplicated when unable to be sent by the underlying DatagramChannel
* DIRMINA-1014   SocketAcceptor doesn't unbind correctly
* DIRMINA-1115   Filter ProfilerTimerFilter ArithmeticException
* DIRMINA-1123   Receive buffer size is never set for NIO acceptor
* DIRMINA-1126   filterWrite in ProtocolCodecFilter can send corrupted writeRequest message to the next filter
* DIRMINA-1064   Implement cipher suites preference flag introduced in JDK 8
* DIRMINA-1105   SSLHandler buffer handling

For any information about the API modifications and the impact on existing application, please read the [2.1 vs 2.0 page](2.1-vs-2.0.html).

## MINA 2.1.3 released _posted on June, 2, 2019_

The MINA project is pleased to announce a new release, MINA 2.1.3. This is a bug fix release: it fixes a 100% CPU usage in some corner case. Here are the fixed issues :

* DIRMINA-1095    Seems like the management f UDP sessions is really unneficient
* DIRMINA-1107    SslHandler flushScheduledEvents race condition, redux
* DIRMINA-1111    100% CPU (epoll bug) on 2.1.x, Linux only
* DIRMINA-1104    IoBufferHexDumper.getHexdump(IoBuffer in, int lengthLimit) does not truncate the output

For any information about the API modifications and the impact on existing application, please read the [2.1 vs 2.0 page](2.1-vs-2.0.html).

## MINA 2.1.2 released _posted on April, 20, 2019_

The MINA project is pleased to announce a new release, MINA 2.1.2. This is a bug fix release: it fixes an issue for applications using *SSL/TLS*, which will stall waiting on a *WriteFuture* because it does not get signaled when the message has been fully sent.

For any information about the API modifications and the impact on existing application, please read the [2.1 vs 2.0 page](2.1-vs-2.0.html).

## MINA 2.1.1 & MINA 2.0.21 released _posted on April, 14, 2019_

The MINA project is pleased to announce two new releases, MINA 2.1.1 and MINA 2.0.21. 

**These are fixing a critical issue, CVE-2019-0231**

CVE-2019-0231: 'Handling of the close_notify SSL/TLS message does not lead to a connection closure, leading the server to retain the socket opened and to have the client potentially receive clear-text messages which were supposed to be encrypted.'

MINA 2.1.1 also fixes the _CompressionFilter_ usage, by simplifying the way we proceed with writes. A side effect is that it should be slightly faster to write data from an application. (This fix is not included in 2.0.21)

**We urge anyone using any previous MINA version to migrate to one of those two new versions**

## MINA 2.1.0 released _posted on March, 14, 2019_

The MINA project is pleased to announce a new release, MINA 2.1.0. This is a evolution over the
2.0.x branch, with some API modifications that makes it incompatible.

That means some effort will be required from applications to be able to use Apache MINA
2.1.0 as a replacement for Apache MINA 2.0.20.

Otherwise, every fix applied in Apache MINA 2.0.20 has been ported to this version, so one can still keep going with Apache MINA 2.0.20 which will be maintained for the coming months.

For any information about the API modifications and the impact on existing application, please read the [2.1 vs 2.0 page](2.1-vs-2.0.html).

## MINA 2.0.20 released _posted on February, 24, 2019_

The MINA project is pleased to announce a new release, MINA 2.0.20, fixing some API issues:

* DIRMINA-1092: Removed a spurious printstacktrace
* DIRMINA-1098: handshakeStatus variable has been wrongly made global
* DIRMINA-1088: the OrderedThreadPool implementation has been made Java 10 compatible


We urge you to switch to this version if you were using MINA 2.0.19 or any older version.


## MINA 2.0.19 released _posted on June, 11, 2018_

The MINA project is pleased to announce a new release, MINA 2.0.19, fixing some API regression:

* the 'event' message has been removed from the IoHandler interface
* the SESSION_SECURED/SESSION_UNSECURED message are back

Those changes have been introduced in MINA 2.0.18 by mistake, and break applications that were 
working with MINA 2.0.17.

They will be reintroduced in MINA 2.1.0

We urge you to switch to this version if you were using MINA 2.0.17 or any older version.

## MINA 2.0.18 released _posted on June, 1, 2018_

The MINA project is pleased to announce a new bug fix release, MINA 2.0.18. 

There is some important addition in this version, the IoHandler interface now exposes a
new method :

    void event(IoSession session, FilterEvent event) throws Exception;


This can be used by any filter to generate a specific event (which will
be handled on demand by the application).

Currently, the only added event is defined in SslEvent, and it tells if
the session has been secured (ie the Handshake has completed) or isn't
anymore.

It changes one thing in your application: if you were implementing
IoHandler, you have to add this method. You may also extends
IoHandlerAdapter which has a void implementation of this event() method.

The few fixes bugs/added features are:

* Added a flag to tell the Handshake to start immediately or not
* The IoBufferHexDumper implementation now does not modify the IoBuffer
position
* Some missing synchronization have been added in teh SslFilter
* The suspendRead call is handled for Datagrams, instead of throwing an
exception

We urge you to switch to this version if you were using MINA 2.0.17 or any older version.


## MINA 2.0.17 released _posted on March, 15, 2018_

The MINA project is pleased to announce a new bug fix release, MINA 2.0.17. It fixes many issues, and adds the missing Javadoc.

Here are the fixed issues :

Bugs :
------

* [DIRMINA-844](https://issues.apache.org/jira/browse/DIRMINA-844) - Http Proxy Authentication failed to complete (see description for exact point of failure)
* [DIRMINA-1002](https://issues.apache.org/jira/browse/DIRMINA-1002) - Mina IoHandlerEvents missing inputClosed enum item.
* [DIRMINA-1051](https://issues.apache.org/jira/browse/DIRMINA-1051) - The MD5withRSA cipher is not anymore supported by Java 8, and our tests certificates have been generated with it.
* [DIRMINA-1052](https://issues.apache.org/jira/browse/DIRMINA-1052) - Fix the mvn-site command
* [DIRMINA-1056](https://issues.apache.org/jira/browse/DIRMINA-1056) - IllegalArgumentException when setting max and minReadBufferSize > 65536 (default)
* [DIRMINA-1057](https://issues.apache.org/jira/browse/DIRMINA-1057) - AbstractIoSession getScheduledWriteMessages always -negative?
* [DIRMINA-1059](https://issues.apache.org/jira/browse/DIRMINA-1059) - NioProcessor's selector is synchronized but accessed outside
* [DIRMINA-1060](https://issues.apache.org/jira/browse/DIRMINA-1060) - Handle the spinning selectors in Socket/Datagram Acceptor and Connector
* [DIRMINA-1072](https://issues.apache.org/jira/browse/DIRMINA-1072) - SslFilter does not account for SSLEngine runtime exceptions
* [DIRMINA-1073](https://issues.apache.org/jira/browse/DIRMINA-1073) - NioSocketSession#isSecured does not comply with interface contract
* [DIRMINA-1076](https://issues.apache.org/jira/browse/DIRMINA-1076) - Leaking NioProcessors/NioSocketConnectors hanging in call to dispose
* [DIRMINA-1077](https://issues.apache.org/jira/browse/DIRMINA-1077) - Threads hanging in dispose() on SSLHandshakeException

Improvement :
-------------

* [DIRMINA-1061](https://issues.apache.org/jira/browse/DIRMINA-1061) - When AbstractPollingIoProcessor read nothing, free the temporary buffer should be better

Task :
------

* [DIRMINA-1058](https://issues.apache.org/jira/browse/DIRMINA-1058) - Add the missing Javadoc

We urge you to switch to this version if you were using MINA 2.0.16 or any older version.


## MINA 2.0.16 released _posted on October, 31, 2016_

The MINA project is pleased to announce a new bug fix release, MINA 2.0.16. It fixes a critical SSL issue, and a regression introduced in 2.0.14.

Here are the fixed issues :

Bugs :
------
* [DIRMINA-1043](https://issues.apache.org/jira/browse/DIRMINA-1043) NullPointerException after upgrade to mina 2.0.14
* [DIRMINA-1044](https://issues.apache.org/jira/browse/DIRMINA-1044) Non-Secure (no TLS/SSL) based client could successfully send message to secure Mina endpoint after second attempt

We urge you to switch to this version if you were using MINA 2.0.15 or any older version.



## MINA 2.0.15 released _posted on September, 27, 2016_

The MINA project is pleased to announce a new bug fix release, MINA 2.0.15. It fixes a hang, a NPE and a few other minor issues.

Here are the fixed issues :

Bugs :
------
* [DIRMINA-1041](<https://issues.apache.org/jira/browse/DIRMINA-1041>) WriteFuture.await() hangs when the connection is closed remotely before await is invoked
* [DIRMINA-1047](<https://issues.apache.org/jira/browse/DIRMINA-1047>) NullPointerException in AbstractIoSession.destroy()
* [DIRMINA-1049](<https://issues.apache.org/jira/browse/DIRMINA-1049>) Error in mina-statemachine manifest prevents using it in Apache Karaf

We urge you to switch to this version if you were using MINA 2.0.14 or any older version.


## MINA 2.0.14 released _posted on August, 30, 2016_

The MINA project is pleased to announce a new bug fix release, MINA 2.0.14. It fixes many issues, some of them being a real burden for SSHD DIRMINA-1021). Some patches were also applied (thanks to Maria Petridan).

Here are the fixed issues :

Bugs :
------
* [DIRMINA-760](https://issues.apache.org/jira/browse/DIRMINA-760)   Client fails to detect disconnection
* [DIRMINA-976](https://issues.apache.org/jira/browse/DIRMINA-976)   ScheduledWriteBytes Increases after Exception on Writing
* [DIRMINA-1021](https://issues.apache.org/jira/browse/DIRMINA-1021) MINA-CORE does not remove sessions if exceptions occur while closing
* [DIRMINA-1025](https://issues.apache.org/jira/browse/DIRMINA-1025) A call to session.closed(true) may still flush messages.
* [DIRMINA-1028](https://issues.apache.org/jira/browse/DIRMINA-1028) The supported ciphers configuration might not be used
* [DIRMINA-1029](https://issues.apache.org/jira/browse/DIRMINA-1029) The sent buffer is reset to its original position when using the SSL Filter after a session.write()
* [DIRMINA-1037](https://issues.apache.org/jira/browse/DIRMINA-1037) Throw exception in NioProcessor.write if the session is closing
* [DIRMINA-1039](https://issues.apache.org/jira/browse/DIRMINA-1039) Response messages queue up on the server side waiting to be written to socket, while the server continues to read more request messages, causing out of heap memory
* [DIRMINA-1042](https://issues.apache.org/jira/browse/DIRMINA-1042) Epoll spinning causes memory leak


Task :
------
* [DIRMINA-986](https://issues.apache.org/jira/browse/DIRMINA-986) Update the web site to reflect the switch to git for the release process
1027) SSLHandler writes corrupt messages under heavy load

A security issue has also been fixed in this version.

We urge you to switch to this version if you were using MINA 2.0.13.


## MINA 2.0.13 released _posted on February, 16, 2016_

Another release to fix a critical SSL bug ( a race condition which could lead to a deadlock in some corner cases).

We urge you to switch to this version if you were using MINA 2.0.12.



Bugs :
------
* [DIRMINA-1019](https://issues.apache.org/jira/browse/DIRMINA-1019) SslHandler flushScheduledEvents race condition
* [DIRMINA-1027](https://issues.apache.org/jira/browse/DIRMINA-1027) SSLHandler writes corrupt messages under heavy load


## MINA 2.0.12 released _posted on February, 07, 2016_

This new release of MINA is a bug fix release. There are a few new bugs that were wound in the way we handle closure, leading to some infinite loop consuming 100% CPU, and a bad counter update forbidding the main loop to be exited.


We urge you to switch to this version if you were using MINA 2.0.11.



Bugs :
------

* [DIRMINA-1001](https://issues.apache.org/jira/browse/DIRMINA-1001) mina2.0.9 session.close cpu100%
* [DIRMINA-1006](https://issues.apache.org/jira/browse/DIRMINA-1006) mina2.0.9 NioProcessor thread make cpu 100%
* [DIRMINA-1024](https://issues.apache.org/jira/browse/DIRMINA-1024) There is no way to start a SslHandshake when the autoStart flag is set to false
* [DIRMINA-1026](https://issues.apache.org/jira/browse/DIRMINA-1026) Session may be removed twice from the removedSession queue


## MINA 2.0.11 released _posted on January, 26, 2016_

This new release of MINA is a bug fix release. We have found a critical bug in the SSL Handler, that may cause a loop when dealing with big messages being transmitted over an SSL connection. 

Otherwise, thee Javadoc has been cleaned.

We urge you to switch to this version if you were using MINA 2.0.10.



Bugs :
------

* [DIRMINA-1023](https://issues.apache.org/jira/browse/DIRMINA-1023) - Infinite loop in SslHandler when the AppBuffer is too small
* [DIRMINA-1022](https://issues.apache.org/jira/browse/DIRMINA-0122) - The IoBuffer.fill(byte, int) method does not work when byte > 0x7F

Improvements :
--------------
* [DIRMINA-985](https://issues.apache.org/jira/browse/DIRMINA-985) - Fix the various Javadoc issues


## MINA 2.0.10 released _posted on December, 16, 2015_

This new release of MINA is a bug fix release. Among important fixes, we have removed a bottleneck in the way we were using Codecs, removed a deadlock in SSL when using the proxy, a race condition, and a few other things :


Bugs :
------

* [DIRMINA-992](https://issues.apache.org/jira/browse/DIRMINA-992) - NioSocketConnector.newHandle throws the wrong exception 
* [DIRMINA-994](https://issues.apache.org/jira/browse/DIRMINA-994) - The ConnectionRequest.cancel() method is inconsistent wrt concurrent access
* [DIRMINA-995](https://issues.apache.org/jira/browse/DIRMINA-995) - Deadlock when using SSL and proxy
* [DIRMINA-1013](https://issues.apache.org/jira/browse/DIRMINA-1013) - Threading model is suppressed by ProtocolCodecFilter
* [DIRMINA-1016](https://issues.apache.org/jira/browse/DIRMINA-1016) - Regression with 2.0.9: Missing javax.net.ssl import in manifest
* [DIRMINA-1017](https://issues.apache.org/jira/browse/DIRMINA-1017) - SSLEngine BUFFER_OVERFLOW (unwrap)
* [DIRMINA-1019](https://issues.apache.org/jira/browse/DIRMINA-1019) - SslHandler flushScheduledEvents race condition

Improvements :
--------------
* [DIRMINA-1018](https://issues.apache.org/jira/browse/DIRMINA-1018) - fetchAppBuffer shrink
* [DIRMINA-1020](https://issues.apache.org/jira/browse/DIRMINA-1020) - Change minimum version for slf4j in MANIFEST


## MINA 2.0.9 released _posted on October, 25, 2014_

This new release of MINA is just a bug fix release. A few issues have been fixed, one critical, inducing a 100% CPU, and one was annoying as it was generating stack traces for nothing.

You can check the list of fixes for this version there :

[Release note](https://issues.apache.org/jira/issues/?jql=project%20%3D%20DIRMINA%20AND%20fixVersion%20%3D%202.0.9%20AND%20status%20%3D%20Resolved%20ORDER%20BY%20priority%20DESC)

* [DIRMINA-921](https://issues.apache.org/jira/browse/DIRMINA-921) - Maven build fails if test phase is given
* [DIRMINA-988](https://issues.apache.org/jira/browse/DIRMINA-988) - 100% CPU when using IoBuffer.shrink() method in some cases
* [DIRMINA-989](https://issues.apache.org/jira/browse/DIRMINA-989) - Frequent CancelledKeyException
* [DIRMINA-990](https://issues.apache.org/jira/browse/DIRMINA-990) - Control flow over exceptional path in AbstractIoBuffer
* [DIRMINA-991](https://issues.apache.org/jira/browse/DIRMINA-991) - Possible faster deserialization in AbstractIoBuffer object deserialization.

## MINA 2.0.8 released _posted on September, 22, 2014_

It's 2 years we haven't had a release of MINA 2.0, it's about time.

We have tried to fix as much issues as we could in the last 3 weeks. As a result, we have closed around 90 JIRAs (fixed, postponed or simply discarded).

There is one change that might break the build for those switching from MINA 2.0.7 to MINA 2.0.8 : the _IoHandler_ interface now has a method called _inputClosed()_, so either you have to implement this method if you are directly implementing the _IoHandler_ interface, or better, you can extends _IoHandlerAdapter_, which implements a placeholder for this method.

You can check the list of fixes for this version there :

[Release note](https://issues.apache.org/jira/issues/?jql=project%20%3D%20DIRMINA%20AND%20fixVersion%20%3D%202.0.8%20AND%20status%20%3D%20Resolved%20ORDER%20BY%20priority%20DESC)

### Bug

* [DIRMINA-539](https://issues.apache.org/jira/browse/DIRMINA-539) - NioDatagramConnector doesn't takes the TrafficClass value set to his DatagramSessionConfig
* [DIRMINA-574](https://issues.apache.org/jira/browse/DIRMINA-574) - ClassCastException when a message is written on a closed session.
* [DIRMINA-604](https://issues.apache.org/jira/browse/DIRMINA-604) - Deadlock occurs when implementing two mina StateMachine
* [DIRMINA-639](https://issues.apache.org/jira/browse/DIRMINA-639) - WriteFuture are updated long after a session.write() is done
* [DIRMINA-738](https://issues.apache.org/jira/browse/DIRMINA-738) - Using IoEventQueueThrottler with a WriteRequestFilter can lead to hangs
* [DIRMINA-760](https://issues.apache.org/jira/browse/DIRMINA-760) - Client fails to detect disconnection
* [DIRMINA-764](https://issues.apache.org/jira/browse/DIRMINA-764) - DDOS possible in only a few seconds...
* [DIRMINA-777](https://issues.apache.org/jira/browse/DIRMINA-777) - IoSessionConfig.setUseReadOperation(true) doesn't seem to work
* [DIRMINA-779](https://issues.apache.org/jira/browse/DIRMINA-779) - SSLHandler can re-order data that it reads
* [DIRMINA-782](https://issues.apache.org/jira/browse/DIRMINA-782) - Combination of SslFilter & FileRegionWriteFilter causes messageSent events to be lost
* [DIRMINA-785](https://issues.apache.org/jira/browse/DIRMINA-785) - Half-duplex close of TCP channel
* [DIRMINA-789](https://issues.apache.org/jira/browse/DIRMINA-789) - Possible Deadlock/Out of memory when sending large amounts of data using Nio
* [DIRMINA-792](https://issues.apache.org/jira/browse/DIRMINA-792) - await() forever
* [DIRMINA-804](https://issues.apache.org/jira/browse/DIRMINA-804) - NioDatagramAcceptor.unbind does not unbind cleanly
* [DIRMINA-805](https://issues.apache.org/jira/browse/DIRMINA-805) - No cipher suites and protocols in SslFilter
* [DIRMINA-813](https://issues.apache.org/jira/browse/DIRMINA-813) - Starvation occurs sometimes in SerialSession#close()
* [DIRMINA-818](https://issues.apache.org/jira/browse/DIRMINA-818) - Loosing connects on NioSocketConnector
* [DIRMINA-833](https://issues.apache.org/jira/browse/DIRMINA-833) - LoggingFilter does not log SENT bytes when used with a ProtocolCodecFilter
* [DIRMINA-843](https://issues.apache.org/jira/browse/DIRMINA-843) - NioSocketAcceptor does not provide an interface to input connectiontimeout parameter.
* [DIRMINA-844](https://issues.apache.org/jira/browse/DIRMINA-844) - Http Proxy Authentication failed to complete (see description for exact point of failure)
* [DIRMINA-845](https://issues.apache.org/jira/browse/DIRMINA-845) - ProtocolEncoderOutputImpl isn't thread-safe
* [DIRMINA-891](https://issues.apache.org/jira/browse/DIRMINA-891) - SSLHandler throws SSLException during handshake that sequence number triggers
* [DIRMINA-899](https://issues.apache.org/jira/browse/DIRMINA-899) - IoSession.getAttribute() doesn't store default value
* [DIRMINA-902](https://issues.apache.org/jira/browse/DIRMINA-902) - Buffer read incorrectly when reading after a NEED_DATA trigger.
* [DIRMINA-905](https://issues.apache.org/jira/browse/DIRMINA-905) - mina serial close
* [DIRMINA-911](https://issues.apache.org/jira/browse/DIRMINA-911) - Surprising behaviour with ConnectFuture
* [DIRMINA-912](https://issues.apache.org/jira/browse/DIRMINA-912) - Different instances of OrderedThreadPoolExecutor may use same task queue
* [DIRMINA-920](https://issues.apache.org/jira/browse/DIRMINA-920) - HTTP server decoding is broken
* [DIRMINA-926](https://issues.apache.org/jira/browse/DIRMINA-926) - IoSession IP Error when Socket Server Communicate With Microcomputer In LAN and Internet.
* [DIRMINA-928](https://issues.apache.org/jira/browse/DIRMINA-928) - when client want to connect to server by binding wrong ip address,there is a bug.
* [DIRMINA-931](https://issues.apache.org/jira/browse/DIRMINA-931) - HTTP header decoding is broken
* [DIRMINA-932](https://issues.apache.org/jira/browse/DIRMINA-932) - HTTP Request decoding is broken if request headers are received in several messages
* [DIRMINA-933](https://issues.apache.org/jira/browse/DIRMINA-933) - subtle HttpServerDecoder problems
* [DIRMINA-937](https://issues.apache.org/jira/browse/DIRMINA-937) - sslfilter hangs with openjdk works with oracle?
* [DIRMINA-940](https://issues.apache.org/jira/browse/DIRMINA-940) - HTTP Client decoder does not support responses without Content-Length header
* [DIRMINA-942](https://issues.apache.org/jira/browse/DIRMINA-942) - Infinite loop flushing to broken pipe
* [DIRMINA-948](https://issues.apache.org/jira/browse/DIRMINA-948) - Performance recession when invoke session.write concurrent
* [DIRMINA-956](https://issues.apache.org/jira/browse/DIRMINA-956) - Status code match bug in AbstractHttpLogicHandler
* [DIRMINA-957](https://issues.apache.org/jira/browse/DIRMINA-957) - MINA build in BlacklistFilter does not support IPV6 address
* [DIRMINA-962](https://issues.apache.org/jira/browse/DIRMINA-962) - Immediate session close with a SSL filter
* [DIRMINA-963](https://issues.apache.org/jira/browse/DIRMINA-963) - Socks5 and ProxyConnector don't work with InetSocketAddress.createUnresolved
* [DIRMINA-965](https://issues.apache.org/jira/browse/DIRMINA-965) - HttpServerDecoder is broken in certain condition
* [DIRMINA-966](https://issues.apache.org/jira/browse/DIRMINA-966) - NIO Datagram messages can get duplicated when unable to be sent by the underlying DatagramChannel
* [DIRMINA-967](https://issues.apache.org/jira/browse/DIRMINA-967) - IoSession updateThroughput not automatically called
* [DIRMINA-968](https://issues.apache.org/jira/browse/DIRMINA-968) - Memory leak in SSL Handshake errors
* [DIRMINA-970](https://issues.apache.org/jira/browse/DIRMINA-970) - ProtocolEncoderOutputImpl.flush() occur a IllegalArgumentException
* [DIRMINA-972](https://issues.apache.org/jira/browse/DIRMINA-972) - NPE during handshake on Android using SSLFilter
* [DIRMINA-973](https://issues.apache.org/jira/browse/DIRMINA-973) - IllegalArgumentException thrown on ProtocolCodecFilter.flush
* [DIRMINA-976](https://issues.apache.org/jira/browse/DIRMINA-976) - ScheduledWriteBytes Increases after Exception on Writing
* [DIRMINA-977](https://issues.apache.org/jira/browse/DIRMINA-977) - DefaultIoFilterChain.replace does not call register/deregister
* [DIRMINA-978](https://issues.apache.org/jira/browse/DIRMINA-978) - ClosedSelectorException handling in AbstractPollingIoProcessor
* [DIRMINA-980](https://issues.apache.org/jira/browse/DIRMINA-980) - Missing implementation of write() method in SerialSessionImpl.SerialIoProcessor
* [DIRMINA-981](https://issues.apache.org/jira/browse/DIRMINA-981) - IoBuffer GetSlice throw an IllegalArgumentException
* [DIRMINA-982](https://issues.apache.org/jira/browse/DIRMINA-982) - ProtocolEncoderOutputImpl.flush() throws an IllegalArgumentException if buffers queue is empty
* [DIRMINA-983](https://issues.apache.org/jira/browse/DIRMINA-983) - Problems with TextLineDecoder and special characters

### Improvement

* [DIRMINA-210](https://issues.apache.org/jira/browse/DIRMINA-210) - Investigate removal of static methods in ByteBuffer
* [DIRMINA-237](https://issues.apache.org/jira/browse/DIRMINA-237) - Improve Spring integration
* [DIRMINA-572](https://issues.apache.org/jira/browse/DIRMINA-572) - Add Spring support for Mina statemachine
* [DIRMINA-586](https://issues.apache.org/jira/browse/DIRMINA-586) - Dynamic delimiter support for TextLineCodecFactory
* [DIRMINA-593](https://issues.apache.org/jira/browse/DIRMINA-593) - Javadoc & documentation for org/apache/mina/filter/reqres
* [DIRMINA-629](https://issues.apache.org/jira/browse/DIRMINA-629) - The IoServiceStatistics methods are called for every new session creation
* [DIRMINA-631](https://issues.apache.org/jira/browse/DIRMINA-631) - AbstractIoFilter: increment written- and receivedMessages statistics on application end of filter chain
* [DIRMINA-668](https://issues.apache.org/jira/browse/DIRMINA-668) - Modify the way we use IoProcessors
* [DIRMINA-682](https://issues.apache.org/jira/browse/DIRMINA-682) - We need a better documentation for the ExecutorFilter [was :Writing more than one message will block until the MessageReceived as been fully proceced]
* [DIRMINA-723](https://issues.apache.org/jira/browse/DIRMINA-723) - OrderedThreadPoolExecutor behavior: configurable queue size, corePoolSize, maximumPoolSize
* [DIRMINA-752](https://issues.apache.org/jira/browse/DIRMINA-752) - maybe move SerialAddressEditor.class to the mina beans project
* [DIRMINA-761](https://issues.apache.org/jira/browse/DIRMINA-761) - how to shutdown a mina application
* [DIRMINA-766](https://issues.apache.org/jira/browse/DIRMINA-766) - Read does not exploit buffer optimally
* [DIRMINA-767](https://issues.apache.org/jira/browse/DIRMINA-767) - Move encoder/decoder out of the session Attributes
* [DIRMINA-773](https://issues.apache.org/jira/browse/DIRMINA-773) - org.apache.mina.filter.firewall.Subnet should consider 0.0.0.0/0 as a subnet that contains 'all the ipv4 addresses'
* [DIRMINA-780](https://issues.apache.org/jira/browse/DIRMINA-780) - Writing null objects to the Session should raise an Exception
* [DIRMINA-825](https://issues.apache.org/jira/browse/DIRMINA-825) - Add host and port info to BindException thrown by NioSocketAcceptor#open
* [DIRMINA-838](https://issues.apache.org/jira/browse/DIRMINA-838) - Redundant AttributeKey allocation resulting in high garbage collector activity
* [DIRMINA-913](https://issues.apache.org/jira/browse/DIRMINA-913) - Add a method IoSession.isSecured() to tell the user if the SSL filter has been started or not
* [DIRMINA-921](https://issues.apache.org/jira/browse/DIRMINA-921) - Maven build fails if test phase is given
* [DIRMINA-929](https://issues.apache.org/jira/browse/DIRMINA-929) - AbstractPollingIoProcessor patch to mark buffer as free
* [DIRMINA-934](https://issues.apache.org/jira/browse/DIRMINA-934) - Replace synchronized with a Semaphore for better performance
* [DIRMINA-941](https://issues.apache.org/jira/browse/DIRMINA-941) - DefaultIoFilterChain (or any other class) should not catch Throwable without re-throwing
* [DIRMINA-945](https://issues.apache.org/jira/browse/DIRMINA-945) - DefaultVmPipeSessionConfig is empty

### New Feature

* [DIRMINA-23](https://issues.apache.org/jira/browse/DIRMINA-23) - New transport type: non-NIO sockets
* [DIRMINA-68](https://issues.apache.org/jira/browse/DIRMINA-68) - Automatic reconnect configuration for client channels.
* [DIRMINA-389](https://issues.apache.org/jira/browse/DIRMINA-389) - Create a Connection Throttle Filter
* [DIRMINA-453](https://issues.apache.org/jira/browse/DIRMINA-453) - Multiple IoServices for one java.nio.Selector
* [DIRMINA-485](https://issues.apache.org/jira/browse/DIRMINA-485) - SCTP Transport based on APR (Apache Portable Runtime)
* [DIRMINA-489](https://issues.apache.org/jira/browse/DIRMINA-489) - Composite IoBuffer
* [DIRMINA-507](https://issues.apache.org/jira/browse/DIRMINA-507) - IoBuffer: Support prepending data
* [DIRMINA-554](https://issues.apache.org/jira/browse/DIRMINA-554) - A hook between bind() and accept()
* [DIRMINA-655](https://issues.apache.org/jira/browse/DIRMINA-655) - Add a more general purpose text based decoder
* [DIRMINA-816](https://issues.apache.org/jira/browse/DIRMINA-816) - NioSocketConnector missing defaultLocalAddress
* [DIRMINA-964](https://issues.apache.org/jira/browse/DIRMINA-964) - Custom NIO SelectorProvider for NioSocketAcceptor

### Task

* [DIRMINA-56](https://issues.apache.org/jira/browse/DIRMINA-56) - Create a Benchmark Suite That Generates HTML Reports.
* [DIRMINA-188](https://issues.apache.org/jira/browse/DIRMINA-188) - All-in-one JAR
* [DIRMINA-477](https://issues.apache.org/jira/browse/DIRMINA-477) - Update page about differences between 1.x and 2.x
* [DIRMINA-721](https://issues.apache.org/jira/browse/DIRMINA-721) - Get rid of multiton iohandler and netty2 codec as proposed on ML

### Test

* [DIRMINA-922](https://issues.apache.org/jira/browse/DIRMINA-922) - Add a benchmark project to compare with other IO frameworks

### Wish

* [DIRMINA-250](https://issues.apache.org/jira/browse/DIRMINA-250) - Provide a test suite for a transport implementor.
* [DIRMINA-916](https://issues.apache.org/jira/browse/DIRMINA-916) - Adding Http Status code 101 "101 Switching Protocols" in org.apache.mina.http.api.HttpStatus


## MINA 2.0.7 released _posted on October, 12, 2012_

The Apache MINA project is pleased to announce MINA 2.0.7 ! This version is a bug fix release.

It fixes a regression introduced in MINA 2.0.5, and some performance improvements for the UDP server.

We recommend all users to upgrade to this release. We consider this a stable and production ready release.

[Release note1](https://issues.apache.org/jira/secure/ReleaseNote.jspa?projectId=10670&version=12323341)
[Release note2](https://issues.apache.org/jira/secure/ReleaseNote.jspa?projectId=10670&version=12316652)

## MINA 2.0.5 released _posted on August, 26, 2012_

The Apache MINA project is pleased to announce MINA 2.0.5 ! This version is a bug fix release.

We recommend all users to upgrade to this release. We consider this a stable and production ready release.

[Release note](http://issues.apache.org/jira/secure/ReleaseNote.jspa?projectId=10670&version=12316474)

## MINA 2.0.4 released _posted on August, 26, 2012_

The Apache MINA project is pleased to announce MINA 2.0.4 ! This version is a bug fix release.

We recommend all users to upgrade to this release. We consider this a stable and production ready release.

[Release note](https://issues.apache.org/jira/secure/ReleaseNote.jspa?projectId=10670&version=12316009)

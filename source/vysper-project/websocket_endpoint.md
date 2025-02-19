---
type: vysper
title: Vysper Websocket endpoint
---

# Websocket endpoint

<div class="info" markdown="1">
    Available since version 0.7.
</div>

While websockets are still being specified, a draft specification for XMPP over websockets has been published at <http://tools.ietf.org/html/draft-moffitt-xmpp-over-websocket-00>. Websockets enables web browsers to establish duplex communications with servers with very little overhead.

Vysper provides a websocket endpoint. The easiest way to use the endpoint is to simply add it as a regular endpoint:

```java
XMPPServer server = new XMPPServer("vysper.org");

server.addEndpoint(new TCPEndpoint());

server.addEndpoint(new WebSocketEndpoint());

server.start();
```

That’s it. The default configuration will start a web server on port 8080 and supply websockets on <http://vysper.org:8080/>.

The port and context path can be configured:

```java
WebSocketEndpoint wsEndpoint = new WebSocketEndpoint();
wsEndpoint.setContextPath("/xmpp");
wsEndpoint.setPort(9000);
server.addEndpoint(wsEndpoint);
```

## Embedded

Commonly, there’s a need to use websockets within the context of a web application. For that purpose, there is a servlet available that can be configured in web.xml inside your regular application.

Vysper currently supports this for Jetty and Apache Tomcat 7.0.27 or later.

For Jetty, add the following to your web.xml:

```java
WebSocketEndpoint wsEndpoint = new WebSocketEndpoint();
wsEndpoint.setSSLEnabled(true);
wsEndpoint.setSSLCertificateKeystore("keystore.jks", "sekrit");
server.addEndpoint(wsEndpoint);
```

For Tomcat, add the following to your web.xml:

```xml
<servlet>
  <servlet-name>WebSocket Servlet</servlet-name>
  <servlet-class>org.apache.vysper.xmpp.extension.websockets.TomcatXmppWebSocketServlet</servlet-class>
  <load-on-startup>1</load-on-startup>
</servlet>
<servlet-mapping>
  <servlet-name>WebSocket Servlet</servlet-name>
  <url-pattern>/ws</url-pattern>
</servlet-mapping>
```

Also, when using the servlet, the main Vysper XMPP server needs to be started by some other mean, typically via a context listener. The ServerRuntimeContext of the Vysper server needs to be made available within the servlet context under the key “org.apache.vysper.xmpp.server.ServerRuntimeContext”. There’s an example application included in the Vysper distribution which does this. The source code is available here: <http://svn.apache.org/repos/asf/mina/vysper/trunk/examples/embedded-war/>

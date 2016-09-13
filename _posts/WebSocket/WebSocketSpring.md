#WebSocket
http://docs.spring.io/spring/docs/current/spring-framework-reference/html/websocket.html#websocket-intro

##1 Introduction
使用websocket优点以及设计考虑,移植挑战等.

RFC 6455:全双工(full-duplex,two-way communication)

初始的握手使用HTTP,后面使用TCP,这其中要求协议切换(protocol upgrade,protocol switch)(需要回复http状态101),之后连接保持打开

###1.1 WebScoket Fallback Options
在不同浏览器中对websocket的支持不同,有些时候连接会被关闭,因此spring框架使用sockJS协议
###1.2 A Messaging Architecture
REST框架使用许多URL,与此同时WebSocket应用程序则可能只使用最初用于http握手的那个url

spring-websocket,spring-messaging
###1.3 Sub-Protocol Support in WebSocket
Websocket是TCP层上非常薄的一层,它并不使用任何特殊的消息协议,将信息解析出来的工作交由应用执行,它将bit流转为信息流,由于websocket本身太过低级,大部分的webapplication使用web框架而不是仅仅使用websocket本身

因此,websocket定义了sub-protocols这个概念,在握手时,client和server都能使用header选项`Sec-WebSocket-Protocol`来同意一个子协议,这个子协议通常是应用层协议.子协议不是强制要求的,而且有时候尽管使用了子协议,客户端和服务器还是需要一个数据格式的约定.

spring框架使用的子协议是STOMP,一个简单的消息框架,主要面向脚本语言.

###Should I use WebSocket?
如果客户端和服务器需要以高频率和低延时交换信息,那么websocket是个不错的选择

Spring框架允许@Controlle和@RestController都支持Websocket和普通的http

##2. WebSocket API
 Tomcat 7.0.47+, Jetty 9.1+, GlassFish 4.1+, WebLogic 12.1.3+, and Undertow 1.0+ (and WildFly 8.0+). 
###Create and Configure a WebSocketHandler
创建WebSocket server

1. 创建handler很简单,只需要实现WebSocketHandler接口或者继承TextWebSocketHandler或者BinaryWebSocketHandler即可

		import org.springframework.web.socket.WebSocketHandler;
		import org.springframework.web.socket.WebSocketSession;
		import org.springframework.web.socket.TextMessage;
		
		public class MyHandler extends TextWebSocketHandler {
		
		    @Override
		    public void handleTextMessage(WebSocketSession session, TextMessage message) {
		        // ...
		    }
		
		}
2. 专用的WebSocket JavaConfig 或者XML配置以将handler与特定的URL联系

		import org.springframework.web.socket.config.annotation.EnableWebSocket;
		import org.springframework.web.socket.config.annotation.WebSocketConfigurer;
		import org.springframework.web.socket.config.annotation.WebSocketHandlerRegistry;
		
		@Configuration
		@EnableWebSocket
		public class WebSocketConfig implements WebSocketConfigurer {
		
		    @Override
		    public void registerWebSocketHandlers(WebSocketHandlerRegistry registry) {
		        registry.addHandler(myHandler(), "/myHandler");
		    }
		
		    @Bean
		    public WebSocketHandler myHandler() {
		        return new MyHandler();
		    }
		
		}

	或者

		<beans xmlns="http://www.springframework.org/schema/beans"
		    xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
		    xmlns:websocket="http://www.springframework.org/schema/websocket"
		    xsi:schemaLocation="
		        http://www.springframework.org/schema/beans
		        http://www.springframework.org/schema/beans/spring-beans.xsd
		        http://www.springframework.org/schema/websocket
		        http://www.springframework.org/schema/websocket/spring-websocket.xsd">
		
		    <websocket:handlers>
		        <websocket:mapping path="/myHandler" handler="myHandler"/>
		    </websocket:handlers>
		
		    <bean id="myHandler" class="org.springframework.samples.MyHandler"/>
		
		</beans>

3. 通过WebSocketHttpRequestHandler的帮助下,可以将WebSocketHandler与其它Http环境集成,不需要仅仅使用SpringMVC

###2.2 自定义WebSocket Handshake
最简单的方式是通过HandshakeInterceptor.这样的interceptor能够被用在handshake之前或者配置WebSocketSession的属性上,例如,这个内置的拦截器可以将httpsession的属性传给websocket session

		@Configuration
		@EnableWebSocket
		public class WebSocketConfig implements WebSocketConfigurer {
		
		    @Override
		    public void registerWebSocketHandlers(WebSocketHandlerRegistry registry) {
		        registry.addHandler(new MyHandler(), "/myHandler")
		            .addInterceptors(new HttpSessionHandshakeInterceptor());
		    }
		
		}

XML

		<beans xmlns="http://www.springframework.org/schema/beans"
		    xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
		    xmlns:websocket="http://www.springframework.org/schema/websocket"
		    xsi:schemaLocation="
		        http://www.springframework.org/schema/beans
		        http://www.springframework.org/schema/beans/spring-beans.xsd
		        http://www.springframework.org/schema/websocket
		        http://www.springframework.org/schema/websocket/spring-websocket.xsd">
		
		    <websocket:handlers>
		        <websocket:mapping path="/myHandler" handler="myHandler"/>
		        <websocket:handshake-interceptors>
		            <bean class="org.springframework.web.socket.server.support.HttpSessionHandshakeInterceptor"/>
		        </websocket:handshake-interceptors>
		    </websocket:handlers>
		
		    <bean id="myHandler" class="org.springframework.samples.MyHandler"/>
		
		</beans>

一种更加先进的选择是继承DefaultHandshakeHandler,它执行力额WebSocket的握手,比如检测客户,商议子协议等等

如果WebSocket需要自定义RequestUpgradeStrategy来适应一个Wengine和version现在还不支持的websocket服务器,那么需要设置一个自定义的HandshakeHandler

###2.3 WebSocketHandler Decoration
Spring提供了基础类WebSocketHandlerDecorator以用于修饰WebSocketHandler并使其做额外的事

当使用WebSocket 的JavaConfig或者XML设置时,logging和异常处理被默认添加.ExceptionWebSocketHandlerDecorator把所有在WebSocketHandler中丢出的错误接住后,关闭webSocket会话
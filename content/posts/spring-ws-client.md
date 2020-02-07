+++
title = "Using Spring-WS for creating a client"
date = 2010-06-01T08:18:23+08:00
draft = false
slug = "spring-ws-client"
tags = ["spring mvc"]
categories = ["development", "java", "spring mvc"]
series = []
+++

Sample config for WebServiceTemplate
```
<bean id="saajMessageFactory" class="org.springframework.ws.soap.saaj.SaajSoapMessageFactory">
    <property name="soapVersion">
      <util:constant static-field="org.springframework.ws.soap.SoapVersion.SOAP_12"/>
    </property>
  </bean>

  <bean id="marshaller" class="org.springframework.oxm.jaxb.Jaxb2Marshaller"
        p:contextPath="com.whatever:com.another.package"/>

  <bean id="wsTemplate" class="org.springframework.ws.client.core.WebServiceTemplate"
        p:messageFactory-ref="saajMessageFactory"
        p:defaultUri="http://whatever"
        p:marshaller-ref="marshaller"
        p:unmarshaller-ref="marshaller"/>
```

To specify more than 1 path for the marshaller, just use colons to separate the packages.
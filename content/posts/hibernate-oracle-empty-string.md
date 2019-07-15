+++ 
title = "Hibernate, Oracle and the empty string"
draft = true
date = 2010-08-12T11:18:05+08:00
description = ""
slug = "hibernate-oracle-empty-string" 
tags = ["spring mvc"]
categories = ["development", "java", "spring mvc"]
externalLink = ""
series = []
+++

We had a model that contained an annotation specifying that it shouldn't be null. It works with Postgres when we were inserting empty strings. But with Oracle, it's throwing an exception. Apparently, Oracle converts empty strings to null. Just one of those quirks. As a workaround, we just allowed null entries.
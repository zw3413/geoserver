.. _introduction:

简介
============

欢迎来到GeoServer开发。本项目使用了如下资源：

* https://github.com/geoserver/geoserver.github.io/wiki Wiki used for Proposals
* https://github.com/geoserver/geoserver Github source code
* https://osgeo-org.atlassian.net/projects/GEOS Jira issue tracker
* `GeoServer User Manual <http://docs.geoserver.org/latest/en/user/>`_
* `GeoServer Developer Manual <http://docs.geoserver.org/latest/en/developer/>`_

沟通方式：

* http://blog.geoserver.org/
* `geoserver-devel <http://lists.sourceforge.net/mailman/listinfo/geoserver-devel>`_ email list
* `geoserver-users <http://lists.sourceforge.net/mailman/listinfo/geoserver-users>`_ email list
* https://gitter.im/geoserver/geoserver

我们有几台构建服务器，用来进行日常构建：

* https://build.geoserver.org/view/geoserver/ (main build server)
* http://office.geo-solutions.it/jenkins/ (windows build server)

通知邮件列表：

* https://groups.google.com/forum/#!forum/geoserver-commits
* https://groups.google.com/forum/#!forum/geoserver-extra-builds

常见问题：

* http://gis.stackexchange.com/questions/tagged/geoserver
* http://stackoverflow.com/questions/tagged/geoserver

授权协议
---------

完整的Licene信息请参考 :download:`LICENSE.txt </../../../../LICENSE.txt>`。

* GeoServer是一个免费软件，使用 :download:`GNU General Public License </../../../../src/release/GPL.txt>` 授权::

    GeoServer, open geospatial information server
    Copyright (C) 2014 - Open Source Geospatial Foundation
    Copyright (C) 2001 - 2014 OpenPlans

    This program is free software; you can redistribute it and/or modify
    it under the terms of the GNU General Public License as published by
    the Free Software Foundation; either version 2 of the License, or
    (at your option) any later version (collectively, "GPL").

    As an exception to the terms of the GPL, you may copy, modify,
    propagate, and distribute a work formed by combining GeoServer with the
    Eclipse Libraries, or a work derivative of such a combination, even if
    such copying, modification, propagation, or distribution would otherwise
    violate the terms of the GPL. Nothing in this exception exempts you from
    complying with the GPL in all respects for all of the code used other
    than the Eclipse Libraries. You may include this exception and its grant
    of permissions when you distribute GeoServer.  Inclusion of this notice
    with such a distribution constitutes a grant of such permissions.  If
    you do not wish to grant these permissions, remove this paragraph from
    your distribution. "GeoServer" means the GeoServer software licensed
    under version 2 or any later version of the GPL, or a work based on such
    software and licensed under the GPL. "Eclipse Libraries" means Eclipse
    Modeling Framework Project and XML Schema Definition software
    distributed by the Eclipse Foundation and licensed under the Eclipse
    Public License Version 1.0 ("EPL"), or a work based on such software and
    licensed under the EPL.

    This program is distributed in the hope that it will be useful,
    but WITHOUT ANY WARRANTY; without even the implied warranty of
    MERCHANTABILITY or FITNESS FOR A PARTICULAR PURPOSE.  See the
    GNU General Public License for more details.

    You should have received a copy of the GNU General Public License
    along with this program; if not, write to the Free Software
    Foundation, Inc., 51 Franklin Street, Suite 500, Boston, MA 02110-1335  USA

另外：

* 用来支持GZIP压缩的几个文件（GZIPFilter, GZIPResponseStream, GZIPResponseWrapper）使用的授权信息如下::

    /*
     * Copyright 2003 Jayson Falkner (jayson@jspinsider.com)
     * This code is from "Servlets and JavaServer pages; the J2EE Web Tier",
     * http://www.jspbook.com. You may freely use the code both commercially
     * and non-commercially. If you like the code, please pick up a copy of
     * the book and help support the authors, development of more free code,
     * and the JSP/Servlet/J2EE community.
     *
     * Modified by David Winslow <dwinslow@openplans.org>
     */


* SetCharacterEncodingFilter 和 RewindableInputStream使用 :download:`Apache License Version 2.0 </../../../../src/release/apache-2.0.txt>` 授权。

* UCSReader使用 :download:`Apache License Version 1.1 </../../../../src/release/apache-1.1.txt>` 授权。

* Prototype library (www.prototypejs.org)的一些代码使用MIT授权.

* 构建过程中会从JAI ImageIO (BSD), Jetty (Jetty License), EMF (EPL), XSD (EPL)下载jar包. Spring, Apache Commons, Log4j, Batik, Xerces几个项目使用Apache License 2.0。

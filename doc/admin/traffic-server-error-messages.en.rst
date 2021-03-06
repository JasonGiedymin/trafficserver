Error Messages
**************

.. Licensed to the Apache Software Foundation (ASF) under one
   or more contributor license agreements.  See the NOTICE file
  distributed with this work for additional information
  regarding copyright ownership.  The ASF licenses this file
  to you under the Apache License, Version 2.0 (the
  "License"); you may not use this file except in compliance
  with the License.  You may obtain a copy of the License at
 
   http://www.apache.org/licenses/LICENSE-2.0
 
  Unless required by applicable law or agreed to in writing,
  software distributed under the License is distributed on an
  "AS IS" BASIS, WITHOUT WARRANTIES OR CONDITIONS OF ANY
  KIND, either express or implied.  See the License for the
  specific language governing permissions and limitations
  under the License.

This section contains the following sections:

-  `Traffic Server Error Messages <#TSErrorMessages>`_: describes the
   warning messages Traffic Server sends to the system log file.
-  `Traffic Server Alarm Messages <#TSAlarmMessages>`_: describes the
   alarm messages that may appear on Traffic Manager Monitor pages.
-  `HTML Messages Sent to Clients <#HTMLMessagesSentClients>`_:
   describes the HTML error messages Traffic Server sends to browser
   clients.
-  `Standard HTTP Response Messages <#StandardHTTPResponseMessages>`_:
   describes the standard HTTP response codes origin servers send to
   browser clients.

Traffic Server Error Messages
=============================

The following table lists messages that can appear in system log files.
This list is not exhaustive; it simply describes common warning messages
that can occur and which might require your attention.

Traffic Server Process Fatal
============================

``Accept port is not between 1 and 65535. Please check configuration``
    The port specified in the :file:`records.config` file that accepts
    incoming HTTP requests is not valid.

``Self loop is detected in parent proxy configuration``
    The name and port of the parent proxy match that of Traffic Server.
    This creates a loop when Traffic Server attempts to send the request
    to the parent proxy.

Traffic Server Warnings
-----------------------

*``Logfile``* ``error:`` *``error_number``*
    Generic logging error.

``Bad cluster major version range`` *``version1-version2``* ``for node``
*``IP address``* ``connect failed``
    Incompatible software versions causing a problem.

``Connect by disallowed client`` *``IP address``*\ ``, closing``
    The specified client is not allowed to connect to Traffic Server;
    the client IP address is not listed in the ``ip_allow.config`` file.

``Could not rename log`` *``filename``* to *``rolled filename``*
    System error when renaming log file during roll.

``Did`` *``this_amount``* ``of backup; still to do``
*``remaining_amount``*
    Congestion is approaching.

``Different clustering minor versions`` *``version1, version2``*
``for node`` *``IP address``* ``continuing``
    Incompatible software versions are causing a problem.

``Log format symbol`` *``symbol_name``* ``not found``
    Custom log format references a field symbol that does not exist.
    Refer to `Event Logging Formats <logfmts.htm>`_.

``Missing field for field marker``
    Error reading a log buffer.

``Unable to open log file``
*``filename``*\ ``, errno=``\ *``error_number``*
    Cannot open the log file.

``Error accessing disk`` *``disk_name``*
    Traffic Server might have a cache read problem. You might need to
    replace the disk.

``Too many errors accessing disk`` *``disk_name``*
``: declaring disk bad``
    Traffic Server is not using the cache disk because it encountered
    too many errors. The disk might be corrupt and might have to be
    replaced.

``No cache disks specified in storage.config file: cache disabled``
    The Traffic Server ``storage.config`` file does not list any cache
    disks; Traffic Server is running in proxy-only mode. You must add
    the disks you want to use for the cache to the
    `storage.config <../configuration-files/storage.config>`_ file.

Traffic Server Alarm Messages
=============================

``[Rollback::Rollback] Config file is read-only:`` *``filename``*
    Go to the Traffic Server ``config`` directory and check the
    indicated file permissions; change if necessary.

``[Rollback::Rollback] Unable to read or write config file``
*``filename``*
    Go to the Traffic Server ``config`` directory and make sure the
    indicated file exists. Check permissions and modify if necessary.

``[Traffic Manager] Configuration File Update Failed:``
*``error_number``*
    Go to the Traffic Server ``config`` directory and check the
    indicated file permissions; change if necessary.

``[Traffic Manager] Mgmt <==>Proxy conn. closed``
    An informational message to inform you that the :program:`traffic_server`
    process is down.

``Access logging suspended - configured space allocation exhausted.``
    The space allocated to the event log files is full; you must either
    increase the space or delete some log files so that access logging
    to continue. To prevent this error, consider rolling log files more
    frequently and enabling the autodelete feature.

``Access logging suspended - no more space on the logging partition.``
    The entire partition containing the event logs is full; you must
    delete or move some log files to enable access logging to continue.
    To prevent this error, consider rolling log files more frequently
    and enabling the autodelete feature.

``Created zero length place holder for config file`` *``filename``*
    Go to the Traffic Server ``config`` directory and check the
    indicated file. If it is indeed zero in length, then use a backup
    copy of the configuration file.

``Traffic Server could not open logfile`` *``filename``*
    Check permissions for the indicated file and the logging directory.

``Traffic Server failed to parse line`` *``line_number``*
``of the logging config file`` *``filename``*
    Check your custom log configuration file; there could be syntax
    errors. Refer to `Custom Logging Fields <logfmts.htm#66912>`_ for
    correct custom log format fields.

``vip_config binary is not setuid root, manager will be unable to enable virtual ip addresses``
    The :program:`traffic_manager` process is not able to set virtual IP
    addresses. You must ``setuid root``\ for the ``vip_config`` file in
    the Traffic Server ``bin`` directory.

HTML Messages Sent to Clients
=============================

Traffic Server returns detailed error messages to browser clients when
there are problems with the HTTP transactions requested by the browser.
These Traffic Server response messages correspond to standard HTTP
response codes, but provide more information. A list of the more
frequently-encountered HTTP response codes is provided in `Standard HTTP
Response Messages <#StandardHTTPResponseMessages>`_. You can customize
the Traffic Server response messages, if desired.

The following table lists the hard-coded Traffic Server HTTP messages,
with corresponding HTTP response codes and customizable files.

``Access Denied``
    ``403``
    You are not allowed to access the document at location *``URL``* .
    ``access#denied``

``Cache Read Error``
    ``500``
    Error reading from cache; please retry request.
    ``cache#read_error``

``Connection Timed Out``
    ``504``
    Too much time has elapsed since the server has sent data.
    ``timeout#inactivity``

``Content Length Required``
    ``400``
    Could not process this request because ``Content-Length`` was not
    specified.
    ``request#no_content_length``

``Cycle Detected``
    ``400``
    Your request is prohibited because it would cause an HTTP proxy
    cycle.
    ``request#cycle_detected``

``Forbidden``
    ``403``
    *``port_number``* is not an allowed port for SSL connections (you
    have made a request for a secure SSL connection to a forbidden port
    number).
    ``access#ssl_forbidden``

``Host Header Required``
    ``400``
    An attempt was made to transparently proxy your request, but this
    attempt failed because your browser did not send an HTTP ``Host``
    header. Manually configure your browser to use
    ``http://``\ *``proxy_name``*\ ``:``\ *``proxy_port``* as the HTTP
    proxy. Alternatively, end users can upgrade to a browser that
    supports the HTTP ``Host`` header field.
    ``interception#no_host``

``Host Header Required``
    ``400``
    Because your browser did not send a ``Host`` HTTP header field, the
    virtual host being requested could not be determined. To access the
    website correctly, you must upgrade to a browser that supports the
    HTTP ``Host`` header field.
    ``request#no_host``

``HTTP Version Not Supported``
    ``505``
    The origin server *``server_name``* is using an unsupported version
    of the HTTP protocol.
    ``response#bad_version``

``Invalid HTTP Request``
    ``400``
    Could not process this *``client_request``* HTTP method request for
    *``URL``*.
    ``request#syntax_error``

``Invalid HTTP Response``
    ``502``
    The host *``server_name``* did not return the document *``URL``*
    correctly.
    ``response#bad_response``

``Malformed Server Response``
    ``502``
    The host *``server_name``* did not return the document *``URL``*
    correctly.
    ``response#bad_response``

``Malformed Server Response Status``
    ``502``
    The host *``server_name``* did not return the document *``URL``*
    correctly.
    ``response#bad_response``

``Maximum Transaction Time exceeded``
    ``504``
    Too much time has elapsed while transmitting document *``URL``* .
    ``timeout#activity``

``No Response Header From Server``
    ``502``
    The host *``server_name``* did not return the document *``URL``*
    correctly.
    ``response#bad_response``

``Not Cached``
    ``504``
    This document was not available in the cache, and you (the client)
    only accept cached copies.
    ``cache#not_in_cache``

``Not Found on Accelerator``
    ``404``
    The request for *``URL``* on host *``server_name``* was not found.
    Check the location and try again.
    ``urlrouting#no_mapping``

``NULL``
    ``502``
    The host *``hostname``* did not return the document *``URL``*
    correctly.
    ``response#bad_response``

``Proxy Authentication Required``
    ``407``
    Please log in with username and password.
    ``access#proxy_auth_required``

``Server Hangup``
    ``502``
    The server *``hostname``* closed the connection before the
    transaction was completed.
    ``connect#hangup``

``Temporarily Moved``
    ``302``
    The document you requested, *``URL``*, has moved to a new location.
    The new location is *``new_URL``*.
    ``redirect#moved_temporarily``

``Transcoding Not Available``
    ``406``
    Unable to provide the document *``URL``* in the format requested by
    your browser.
    ``transcoding#unsupported``

``Tunnel Connection Failed``
    ``502``
    Could not connect to the server *``hostname``*.
    ``connect#failed_connect``

``Unknown Error``
    ``502``
    The host *``hostname``* did not return the document *``URL``*
    correctly.
    ``response#bad_response``

``Unknown Host``
    ``500``
    Unable to locate the server named *``hostname``*; the server does
    not have a DNS entry. Perhaps there is a misspelling in the server
    name or the server no longer exists; double-check the name and try
    again.
    ``connect#dns_failed``

``Unsupported URL Scheme``
    ``400``
    Cannot perform your request for the document *``URL``* because the
    protocol scheme is unknown.
    ``request#scheme_unsupported``

Standard HTTP Response Messages
-------------------------------

The following standard HTTP response messages are provided for your
information.

**``200``**
    OK

**``202``**
    Accepted

**``204``**
    No Content

**``206``**
    Partial Content

**``300``**
    Multiple Choices

**``301``**
    Moved Permanently

**``302``**
    Found

**``303``**
    See Other

**``304``**
    Not Modified

**``400``**
    Bad Request

**``401``**
    Unauthorized; retry

**``403``**
    Forbidden

**``404``**
    Not Found

**``405``**
    Method Not Allowed

**``406``**
    Not acceptable

**``408``**
    Request Timeout

**``500``**
    Internal server error

**``501``**
    Not Implemented

**``502``**
    Bad Gateway

**``504``**
    Gateway Timeout



---
layout: post
title: "How to write a client side tool for Monupco"
date: 2012-02-11 00:32
comments: true
categories: ["Monupco", "Tips", "Open Source"]
---

[Monupco](http://monupco.com) is aiming to support a broad range of PaaS and
cloud vendors but that takes time. If your favorite PaaS platform is not
already supported here's how you can help.

The client side tool is very simple and serves only a single purpose -
to build a list of installed software and send it to the server.

Some general considerations first:

* Your code should be open source! Preferably licensed under the MIT or BSD license;

* Whenever possible use the native programming language for the platform - if writing
a client tool for PHP PaaS use PHP, if writing for Node.JS use JavaScript, etc;

* All client side tools are bundled as packages so that they can install natively
on the platform. For Python it is a package from PyPI, for PHP it will be a PEAR package,
etc. Develop your client as a package;

* Naming convention for client side tools is **monupco-\<vendor\>-\<language\>**. For example
`monupco-openshift-express-python`, `monupco-dotcloud-nodejs`. If you have common code,
for example the package management part, it can be split into separate module named
**common-\<language\>-monupco**.

* Client side tools are specific to vendor and programming language. This is because
different PaaS vendors provide the information in a different way. This makes code easier
to maintain and easier for end-users to find the proper client side tool later;

* Vendor ID and package type ID numbers are unique. It is important to use the correct IDs.
They allow proper identification of applications and packages stored in the database.
Different types of data also require different processing. Tell us for which vendor/language
you would like to contribute a client side tool and we will reserve the IDs for you;

* We will also setup a development server so you can safely test the application
registration/update process. Just let us know you need one.


Once you have the ID allocation and development server you can start writing some code.


* Your code should create the following data structure:

        {
            'user_id'    : integer,
            'app_name'   : string,
            'app_uuid'   : string,
            'app_type'   : string,
            'app_url'    : string,
            'app_vendor' : integer,
            'pkg_type'   : integer,
            'installed'  : list of {'n' : string, 'v' : string, 't' : integer}
        }

Fields are defined as follow:

* user_id - integer - the ID of the user at Monupco website. All applications registered under
the same user_id will be visible only to that user. You can view your UserID
[here](https://monupco-otb.rhcloud.com/profiles/mine/). It is important that this value is not
hard-coded but read from ENV variable or a text file. The user will configure the proper
value when installing the client side tool into their application;

* app_name - string - the name of the application. This is used to identify the application in the
web interface. The value is usually available from ENV variable;

* app_uuid - string - a unique identifier of the application on the cloud platform. Some platforms
do not provide a real UUID. In such case you may use any unique string, for example $username-$appname;

* app_type - string - type of the application, e.g. Python, Ruby, etc. Used for visualization in the
web interface. Some cloud vendors store this in ENV variable;

* app_url - string - the URL at which the application can be accessed including the protocol part (http://).
Should be available from ENV;

* app_vendor - integer - the vendor ID reserved by Monupco. This is used for proper identification
of applications in the web console and for processing purposes;

* pkg_type - integer - the package type ID reserved by Monupco. This is used to properly process
package information and find new versions and updates. If the cloud platform allows only a single
type of packages to be installed into the application then use this variable. If you can install
multiple package types (e.g. Python and Ruby) then you can set this on a per-package basis;

* installed - a list of {'n' : string, 'v' : string, 't' : integer} elements, where:
    * n - string - package name as identified by a native package management tool (e.g. gem, pip, etc);

    * v - string - package version;

    * t - integer (optional) - package type ID reserved by Monupco. Define it here is multiple
    package types are allowed and the current package is different from `pkg_type`.


* In some cloud platforms your application will be considered as a package and listed in the database
as well. You may use an ENV variable to ignore this name and not include it in the list;


* The defined structure is converted into JSON format and URL escaped;

* Assign the escaped JSON string to the `json_data` POST variable;

* Send a POST request to https://$devel-server-url/application/register/;

* When sending the request make sure to include a `User-agent` header. The `User-agent`
string must follow the format:

        monupco-<vendor>-<language>/<version>

* If using common packages include them in the `User-agent` string as follows:

        monupco-<vendor>-<language>/<version> common-<language>-monupco/<version>
For more information about `User-aget` string format click
[here](http://en.wikipedia.org/wiki/User_agent#Format).

* If everything went fine you will receive a 200 status code and response in JSON format:
        {
            'message' : string,
            'exit_code' : integer
        }

    * message - holds any pass/fail messages;

    * exit_code - non 0 in case of failure.


* Add a README file with instructions how to install. Pay attention to end-user configuration
settings and proper execution of the tool. The best place to place a call to
the client side tool is a post_deploy/post_install hook. Some cloud platforms do not offer
hooks. In this case you may want to ping us for some help.



Congratulations! You have just written a client side tool for your favorite PaaS and
programming language. Sent us the code for review and we will add it to our GitHub channel.



For more details you may take a look at <https://github.com/monupco/monupco-openshift-express-python>.


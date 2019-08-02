## Skiptracer - OSINT scraping framework
![python](https://img.shields.io/badge/python-3.6-green.svg) ![version](https://img.shields.io/badge/version-3.0.0-brightgreen.svg) ![licence](https://img.shields.io/badge/license-GPLv3-lightgrey.svg)

![screen](https://i.imgur.com/gG0KZ0F.png)

Initial attack vectors for recon usually involve utilizing pay-for-data/API (Recon-NG), or paying to utilize transforms (Maltego) to get data mining results. Skiptracer utilizes some basic python webscraping (BeautifulSoup) of PII paywall sites to compile passive information on a target on a ramen noodle budget.


Background:
-----------
The following recording from DEFCON 26 Recon Village provides background on Skiptracer:
[DEFCON 26 Recon Village Skiptracer Talk](https://www.youtube.com/watch?v=3mEOkwrxfsU)


Installation
-------------
There are a number of ways to install/access Skiptracer. These are as follows.

### From source

```
$ git clone https://github.com/xillwillx/skiptracer.git skiptracer
```
__Install source__
```
$ pip3 install -e skiptracer
```
__Run__
```
$ python3 -m skiptracer
```

### From requirements

```
$ git clone https://github.com/xillwillx/skiptracer.git skiptracer
cd skiptracer
```

__Install requirements__
```
$ pip3 install -r requirements.txt
```

__Run__
```
$ python3 -m skiptracer
```


### From Buscador

Skiptracer is included in the Buscador OS.

You can obtain a copy from the IntelTechniques website:

[Buscador - Intel Techniques](https://inteltechniques.com/buscador/)



Usage
----

Once Skiptarcer is launched, the menu system can be used to navigate between plugins and
execute them, passing in parameters from the command line.

Currently supported features include:

* Phone
* Email
* Screen names
* Real names
* Addresses
* IP
* Hostname
* Breach Credentials

The plugin framework will allow contributors to submit new modules for different websites to help collect as much data as possible with minimal work. This makes Skiptracer your one-stop-shop to help you collect relevant information about a target to help expand your attack surface.



Extending and configuring Skiptracer
------------------------------------

The following section describes how to configure and extend
Skiptracer's functionality using plugins and .cfg files.

### Plugins


Skiptracer uses a plugin architecture.

Plugins are added to the following dir:

```
src/skiptracer/plugins/
```

Plugins should be added in a folder under here with their plugin name and
should contain a __main__.py and __init__.py

Once added, to register them, please add them to the setup.py under the
skiptracer.plugins section under entry_points.

For example:

```
'skiptracer.plugins': [
    'myplugin = skiptracer.plugins.myplugin:MyNewSiteGrabber',
    ...
    ]
```


If your plugin requires parameters, please add these to the setup.cfg. For
example:

```
[plugin.myplugin]
homepageurl = https://www.example.com
loginurl = https://www.example.com/uas/login-submit
logouturl = https://www.example.com/m/logout
viewbyemail = https://example.com/sales/gmail/profile/viewByEmail/
sessionkey = ""
sessionpassword = ""
```


### Plugin Menu Configuration

The menus in Skiptracer are configurable and handled by the setup.cfg file
located in the package/source code.

When adding a new plugin, you will need to update the setup.cfg to config
which menus the plugin will be displayed under. A plugin can appear under 1:n
menus.

For example if your plugin supports both email and phone based scraping features
then it can be added to both menus.

To do this, simply edit the setup.cfg and add the plugin name, title and description to
the menu you wish it to appear under, for example:

```
[menu.email]
myplugin = ["My Plugin","Check if user exposes information through some site"]
```

### Dockerize Environment

You may run this application in a dockerized environment using the command:

```bash
docker-compose run --rm skiptracer
```

Note: the `--rm` flag will remove the container after execution.

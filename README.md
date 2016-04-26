apache-nginx-referral-spam-blacklist [![Build Status](https://travis-ci.org/Stevie-Ray/apache-nginx-referral-spam-blacklist.svg)](https://travis-ci.org/Stevie-Ray/apache-nginx-referral-spam-blacklist)
====================================

Generator to create Apache and Nginx files plus a Google Analytics segment to prevent (old) referral spam traffic.

- - - -

## Apache: .htaccess usage

.htaccess is a configuration file for use on web servers running Apache. This file is usually found in the root “public_html” folder of your website. The .htaccess file uses two modules to prevent referral spam, mod_rewrite and mod_setenvif. Decide which method is most suitable with your Apache server configuration. This file is **Apache 2.4** ready, where mod_authz_host got deprecated.


## Nginx: referral-spam.conf usage

With `referral-spam.conf` in `/etc/nginx`, include it globally from within `/etc/nginx/nginx.conf`:

```conf
http {
	include referral-spam.conf;
}
```

Add the following to each `/etc/nginx/site-available/your-site.conf` that needs protection:

```conf
server {
	if ($bad_referer) {
		return 444;
	}
}
```


## Options for old Google Analytics 'ghost' spam

**UPDATE:**
The problem with future Google Analytics spam seems to be [fixed](http://www.thesempost.com/google-analytics-referral-spam-removed/). 

The above methods don't stop the Google Analytics **ghost** referral spam (because they are hitting Analytics directly and don't touching your website). You should use filters in Analytics to prevent **ghost** referral spam. 


Navigate to your Google Analytics Admin panel and add a Segment:

Filter | Session | **Include**
------------ | ------------- | -------------
Hostname | matches regex | ```your-website\.com|www\.your-website\.com```

Filter | Session | **Exclude**
------------ | ------------- | -------------
Source | matches regex |Copy all the domains from [google-exclude.txt](https://raw.githubusercontent.com/Stevie-Ray/apache-nginx-referral-spam-blacklist/master/google-exclude.txt) to this field

You can also prevent **ghost** referral spam by:

  * [Adding a filter](https://support.google.com/analytics/answer/1033162)
  * [Enabeling bot and Spider Filtering](https://plus.google.com/+GoogleAnalytics/posts/2tJ79CkfnZk) 


## Like it?

- [Buy me a beer](https://www.paypal.com/cgi-bin/webscr?cmd=_s-xclick&hosted_button_id=4XC7KX75K6636) 🍺
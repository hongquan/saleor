Saleor
======

Avast ye landlubbers! Saleor be a Satchless store ye can fork.

[![Build Status](https://travis-ci.org/mirumee/saleor.png?branch=master)](https://travis-ci.org/mirumee/saleor)


Usage
-----

1. Use `django-admin.py` to start a new project using Saleor as template:

   ```
   $ django-admin.py startproject \
   --template=https://github.com/mirumee/saleor/archive/master.zip myproject
   ```
2. Enter the directory:

   ```
   $ cd myproject/
   ```
3. Install it in development mode:

   ```
   $ python setup.py develop
   ```
   (For production use `python setup.py install` instead.)
4. Prepare the database:

   ```
   $ saleor syncdb
   ```

   `saleor` is a shortcut for running `python manage.py` so you can use it to execute all management commands.

5. Install frontend dependencies:

   ```
   $ npm install
   $ ./node_modules/.bin/bower install 
   ```
   
6. Prepare assets:

  ```
  $ ./node_modules/.bin/grunt
  ```
 

## Deploy to Heroku

### First steps

    $ heroku create --buildpack https://github.com/ddollar/heroku-buildpack-multi.git
    $ heroku addons:add heroku-postgresql
    $ heroku config:set SECRET_KEY='<your secret key here>'
    $ heroku config:set ALLOWED_HOSTS='<your hosts here>'

### Amazon S3

Configure S3 for serving media files:

    $ heroku config:set AWS_ACCESS_KEY_ID='<your key id>'
    $ heroku config:set AWS_SECRET_ACCESS_KEY='<your access key>'
    $ heroku config:set AWS_MEDIA_BUCKET_NAME='<your bucket name>'

`saleor` supports serving static files through [WhiteNoise](https://warehouse.python.org/project/whitenoise/) by default. 
If you intend to use S3 for your static files as well, set the following config variable:
    
    $ heroku config:set AWS_STATIC_BUCKET_NAME='<your bucket name>'


### Deploy

    $ git push heroku master
    
### Prepare the database
    
    $ heroku run python manage.py migrate
  
    

Google Analytics
----------------

Because of EU law regulations, Saleor will not use any tracking cookies by default. We do support server-side Google Analytics out of the box using [Google Analytics Measurement Protocol](https://developers.google.com/analytics/devguides/collection/protocol/v1/). This is implemented using [google-measurement-protocol](https://pypi.python.org/pypi/google-measurement-protocol) and does not use cookies at the cost of not reporting things like geolocation and screen resolution.

To get it working you will need to set the `GOOGLE_ANALYTICS_TRACKING_ID` in your settings file:

```python
# settings.py
GOOGLE_ANALYTICS_TRACKING_ID = 'UA-123456-78'
```


Testing changes
---------------

Run the tests to make sure everything works:

```
$ python setup.py test
```


Commercial support
------------------

Disclaimer: everything you see here is open and free to use as long as you comply with the [license](LICENSE). It is not a bait to force you to pay us later and we promise to do our bests to fix bugs and improve the code.

Some situations however call for extra code being written. Whether you need us to cover an exotic use case or build you a custom e-commerce appliance, our team can help.

> Mirumee Software  
> http://mirumee.com/  
> hello@mirumee.com

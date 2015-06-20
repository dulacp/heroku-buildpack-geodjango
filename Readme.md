#Heroku buildpack: GeoDjango

This is a [Heroku buildpack](http://devcenter.heroku.com/articles/buildpacks) for GeoDjango apps.
It extends the original Python buildpack by adding GEOS, Proj.4 and GDAL, per the [GeoDjango installation
instructions](https://docs.djangoproject.com/en/dev/ref/contrib/gis/install/).

---

This is a [Heroku buildpack](http://devcenter.heroku.com/articles/buildpacks) for Python apps.

##Usage

Example usage:

    $ heroku create --buildpack git://github.com/dulaccc/heroku-buildpack-geodjango.git

    $ git push heroku master
    ...
    -----> Python app detected
    -----> Installing runtime (python-2.7.8)
    -----> Checking for GDAL
           Fetching and installing GEOS 3.3.2
           Caching ...
           GEOS installed
    -----> Checking for Proj.4
           Fetching and installing Proj.4 4.7.0
           Installing ...
           Proj.4 installed
    -----> Checking for GDAL
           Fetching and installing GDAL 1.8.1
           Installing ...
           GDAL installed
    -----> Installing dependencies using pip
           Downloading/unpacking requests (from -r requirements.txt (line 1))
           Installing collected packages: requests
           Successfully installed requests
           Cleaning up...
    -----> Discovering process types
           Procfile declares types -> (none)

You can also add it to upcoming builds of an existing application:

    $ heroku config:add BUILDPACK_URL=git://github.com/dulaccc/heroku-buildpack-geodjango.git

The buildpack will detect your app as Python if it has the file requirements.txt in the root.

It will use Pip to install your dependencies, vendoring a copy of the Python runtime into your slug.

##Configuration

Then you need to set two Django settings in order for `GEOS` and `GDAL` to work properly.

**settings.py**

```python
from os import environ

GEOS_LIBRARY_PATH = environ.get('GEOS_LIBRARY_PATH')
GDAL_LIBRARY_PATH = environ.get('GDAL_LIBRARY_PATH')
```

## Notes

All libraries are stored in the directory `/app/.geodjango`.

## Specify a Runtime

You can also provide arbitrary releases Python with a `runtime.txt` file.

    $ cat runtime.txt
    python-3.4.2

Runtime options include:

- python-2.7.8
- python-3.4.2
- pypy-2.4.0 (unsupported, experimental)
- pypy3-2.4.0 (unsupported, experimental)

Other [unsupported runtimes](https://github.com/kennethreitz/python-versions/tree/master/formula) are available as well.

## Contact

[Pierre Dulac](http://github.com/dulaccc)
[@dulaccc](https://twitter.com/dulaccc)

==============
djangocms-blog
==============

.. image:: https://badge.fury.io/py/djangocms-blog.png
        :target: http://badge.fury.io/py/djangocms-blog

.. image:: https://travis-ci.org/nephila/djangocms-blog.svg?branch=develop
    :target: https://travis-ci.org/nephila/djangocms-blog

.. image:: https://pypip.in/d/djangocms-blog/badge.png
        :target: https://pypi.python.org/pypi/djangocms-blog

.. image:: https://coveralls.io/repos/nephila/djangocms-blog/badge.png?branch=develop
        :target: https://coveralls.io/r/nephila/djangocms-blog?branch=develop


A djangoCMS 3 blog application.

Still experimental and untested. You are welcome if you want to try it; if
you encounter any issue, please open an issue.

Supported Django versions:

* Django 1.5
* Django 1.6

Supported django CMS versions:

* django CMS 3.0

Documentation
-------------

No doc at the moment, sorry

Quickstart
----------

Install djangocms-blog::

    pip install djangocms-blog==0.2b5

Add ``djangocms_blog`` and its dependencies to INSTALLED_APPS::

    INSTALLED_APPS = [
        ...
        'filer',
        'parler',
        'taggit',
        'django_select2',
        'taggit_autosuggest',
        'meta',
        'meta_mixin',
        'djangocms_blog',
        'cmsplugin_filer_image'
        'easy_thumbnail'
        'admin_enhancer'
        ...
    ]

Then sync and migrate::

    $ python manage.py syncdb
    $ python manage.py migrate

External applications configuration
+++++++++++++++++++++++++++++++++++

Dependency applications may need configuration to work properly.

Please, refer to each application documentation on details.

* django-filer: http://django-filer.readthedocs.org
* django-meta: https://github.com/nephila/django-meta#installation
* django-taggit-autosuggest: https://bitbucket.org/fabian/django-taggit-autosuggest

Quick hint
++++++++++

The following are minimal defaults to get the blog running; they may not be
suited for your deployment.

* Add the following settings to your project::    

    SOUTH_MIGRATION_MODULES = {
        'easy_thumbnails': 'easy_thumbnails.south_migrations',
        'taggit': 'taggit.south_migrations',
    }
    THUMBNAIL_PROCESSORS = (
        'easy_thumbnails.processors.colorspace',
        'easy_thumbnails.processors.autocrop',
        'filer.thumbnail_processors.scale_and_crop_with_subject_location',
        'easy_thumbnails.processors.filters',
    )
    META_SITE_PROTOCOL = 'http'
    META_USE_SITES = True

* Add the following to your ``urls.py``::

    url(r'^taggit_autosuggest/', include('taggit_autosuggest.urls')),

* To start your blog, you need to create a new page from the CMS and hook it to the blog application. Then, go to Advanced setting and select Blog from the Application selector.

Features
--------

* Placeholder content editing
* Frontend editing using django CMS 3.0 frontend editor
* Multilingual support using django-parler
* Support for Twitter cards, Open Graph and Google+ snippets meta tags
* Optional support for simpler TextField-based content editing

Import from Wordpress
+++++++++++++++++++++

If you want to import content from existing wordpress blog, check
https://pypi.python.org/pypi/the-real-django-wordpress and
this gist https://gist.github.com/yakky/11336204 as a base.


Settings
--------
* BLOG_ENABLE_COMMENTS: Whether to enable comments by default on posts;
  while `djangocms_blog` does not ship any comment system, this flag can be used
  to control the chosen comments framework; (default: True)
* BLOG_USE_PLACEHOLDER: Post content is managed via placeholder; if `False` a
  simple HTMLField is used; (default: True)
* BLOG_IMAGE_THUMBNAIL_SIZE: Size of the main image when shown on the post lists;
  it's a dictionary with `size`, `crop` and `upscale` keys;
  (default: `{'size': '120x120', 'crop': True,'upscale': False}`)
* BLOG_IMAGE_FULL_SIZE: Size of the main image when shown on the post detail;
  it's a dictionary with `size`, `crop` and `upscale` keys;
  (default: `{'size': '640x120', 'crop': True,'upscale': False}`)
* BLOG_PAGINATION: Number of post per page; (defaul: 10)
* BLOG_LATEST_POSTS: Default number of post in the **Latest post** plugin; (defaul: 5)
* BLOG_POSTS_LIST_TRUNCWORDS_COUNT: Default number of words shown for abstract in the post list; (default: 100)

Social media tags settings
++++++++++++++++++++++++++
* BLOG_TYPE: Generic type for the post object; (default: Article)
* BLOG_FB_TYPE: Open Graph type for the post object; (default: Article)
* BLOG_FB_APPID: Facebook Application ID
* BLOG_FB_PROFILE_ID: Facebook profile ID of the post author
* BLOG_FB_PUBLISHER: Facebook URL of the blog publisher
* BLOG_FB_AUTHOR_URL: Facebook profile URL of the post author
* BLOG_FB_AUTHOR: Facebook profile URL of the post author
* BLOG_TWITTER_TYPE: Twitter Card type for the post object; (default: Summary)
* BLOG_TWITTER_SITE: Twitter account of the site
* BLOG_TWITTER_AUTHOR: Twitter account of the post author
* BLOG_GPLUS_TYPE: Google+ Snippet type for the post object; (default: Blog)
* BLOG_GPLUS_AUTHOR: Google+ account of the post author

.. image:: https://d2weczhvl823v0.cloudfront.net/nephila/djangocms-blog/trend.png
   :alt: Bitdeli badge
   :target: https://bitdeli.com/free


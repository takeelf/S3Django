# S3Django with seoul region

Seoul region have to set host "s3.ap-northeast-2.amazonaws.com"
Otherwise boto library return 400 bad request error.


### Install libs

 - boto [http://docs.pythonboto.org/en/latest/]
 - django storage [https://django-storages.readthedocs.io/en/latest/]

### Edit settings.py
```sh
AWS_HEADERS = {  # see http://developer.yahoo.com/performance/rules.html#expires
    'Expires': 'Thu, 31 Dec 2099 20:00:00 GMT',
    'Cache-Control': 'max-age=3600',
}
AWS_QUERYSTRING_AUTH = False
STATICFILES_STORAGE = 'storages.backends.s3boto.S3BotoStorage'
DEFAULT_FILE_STORAGE = 'storages.backends.s3boto.S3BotoStorage'
AWS_S3_HOST = 's3.ap-northeast-2.amazonaws.com'  # Seoul region needs this host
AWS_ACCESS_KEY_ID = 'access key id'
AWS_SECRET_ACCESS_KEY = 'secret access key'
AWS_STORAGE_BUCKET_NAME = 'bucket name'
AWS_S3_CUSTOM_DOMAIN = '%s.s3.ap-northeast-2.amazonaws.com' % AWS_STORAGE_BUCKET_NAME  # Seoul region needs this host
STATIC_URL = "http://%s/" % AWS_S3_CUSTOM_DOMAIN
MEDIA_URL = "http://%s/user_static/" % AWS_S3_CUSTOM_DOMAIN
MEDIA_ROOT = os.path.join(AWS_S3_CUSTOM_DOMAIN, 'user_static')
```

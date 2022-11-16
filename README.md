# recipe-app-api
Recipe API training project

## WARNING

### django-admin startproject app .

Running startproject fails with following message
```
PermissionError: [Errno 13] Permission denied: '/app/manage.py'
```

Reason is the file permissions and running non-root docker-compose.

I fixed it by changing the file permissions on the ./app directory.
Unless generating stuff will be used we should change back the permissions afterwards

```
❯ chmod 777 app 
❯ docker-compose run --rm app sh -c "django-admin startproject app ."
Creating recipe-app-api_app_run ... done
❯ sudo chown user:user -R app
❯ chmod 755 app 
```

### docker-compose up

Also for `docker-compose up`the permissions on the app directory need to be write for all otherwise we will see the following error message

```
app_1  | django.db.utils.OperationalError: unable to open database file
```

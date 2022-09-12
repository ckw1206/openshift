# User management
### Retrieve the HTPasswd file from the htpass-secret Secret object and save the file as users.htpasswd
```
oc get secret htpass-secret -ojsonpath={.data.htpasswd} -n openshift-config | base64 --decode > users.htpasswd
```

### See current user and secret in users.htpasswd.
```
cat users.htpasswd 
<user01>:$2a$10$VQielMSsR7RXdM8VCtskMeO.5moVdknasdjWjkllMRpAVa79Abo.W
<user02>:$2a$10$207sFj.wmwdl5XXVOREl4Oave7tInasdjWjkKpdQPqr87MoqWhPfm
...
```

### To add an new user
```
htpasswd -bB users.htpasswd <username> <password>
```

### To remove an existing user
```
htpasswd -D users.htpasswd <user>
```

### Replace the htpass-secret Secret object with the updated users in the users.htpasswd file.
```
oc create secret generic htpass-secret --from-file=htpasswd=users.htpasswd --dry-run=client -o yaml -n openshift-config | oc replace -f -
```

### Remove existing resources if you remove one or more users. 
- ### Check current User and Identity.
```
oc get users
NAME           UID                                    FULL NAME   IDENTITIES
user01         c1c1c709-8818-382s-9901-ewkj3bf745c8               identity:user01
user01         b92a8e00-774e-20ks-966c-d6717c47a5e5               identity:user02
...
```

- ### Delete User and Identity 
```
oc delete <user> developer ; oc delete identity <identity:user>
```

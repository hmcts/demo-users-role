# Techie General info:

This app generates a .htpasswd file.

It uses json as an internal database to keep track of users.  
When new users are added, the htpasswd file is updated.  
If the htpasswd file is used by nginx, then nginx does not need to be restarted for new users to be picked up.  
The web app runs on port 5001 in order to provide an easy way to add users.


### Testing
For the normal tests do:  
```
molecule test
```

To test locally and see the webapp:  
edit molecule.yml and uncomment the port bindings, then just run:
```
molecule converge
```
It will then be available on localhost:5001


# User Documentation

A webapp is provided to manage demo users on https://my.demo.proxy.example.com/ to allow the addition of new users  
In order to log into this system, a user must be in the -REDACTED-GROUP- group in LDAP  
Once logged in to the webapp, a demo user can be added by submitting the form, no details need to be provided  
Usernames are generated sequentially e.g. user1, user2, etc  
The new users details will then be provided on screen  
It is not possible to retrieve these in future, if a user loses their details it is best to just make a new user  
User details are set to expire after 7 days currently (7*24 hours not working/week days)  
Again, just make a new user if someones details expire

The system then runs NGINX as a proxy. User details are held in a htpasswd file and basic auth is used to authenticate users

Systems are to be directed through the demo proxy in order to use this authentication mechanism  

When a user first visits a system using the demo proxy, they will be prompted by a basic authentication popup box asking for their username and password  
A user should only have to enter these details once per hostname using the proxy  
After this step, everything should work normally as if they were not going through the demo proxy

The webapp is currently available on port 80/443, it may be needed to move this to another port if the demo proxy is going to be made available to the public internet.  
It is already listening on port 5001 so I could remove the vhost for the webapp on port 443 if needed.

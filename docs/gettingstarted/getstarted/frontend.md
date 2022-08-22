---
sidebar_position: 1
sidebar_label: Accesing dev api
---
## Instead of running the backend api locally you can access the api by using the public url. 

Make sure you authentication to the request when acessing the api, it is a basic auth username:password. 

Check your passit to see the auth information for all client.

But first you need to secure you localhost with ssl 

> Intructions Below

- Install  [mkcert](https://github.com/FiloSottile/mkcert#installation)

Browse to your root directory and run 

```bash
     mkcert -install
```
- Accept the popup mkcert is now ready to generate keys for you.

- create a folder called cert in the project directory

```bash
    mkdir cert
```

-  create certificate for the project using mkcert

```bash
     mkcert -key-file ./cert/key.pem -cert-file ./cert/cert.pem "localhost"
```

you can now start the app by running npm start and it should run on https
the environment variables are already setup for you in [env](.env.development) file
if you need to add or customize this variables create a new `env.local` file and copy the content of `env.development`
you can now modify the variables to your liking

> Make sure you do not commit `env.local`
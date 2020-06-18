## Requires
- self-certificate by [mkcert](https://github.com/FiloSottile/mkcert)

## create self-certificate
- before starting development, we need to create self-cert into cert directory first, please following below steps
```bash
mkdir cert # create cert directory
mkcert -install # install root CA
mkcert -key-file key.pem -cert-file cert.pem localhost ::1 # gen certificate for `localhost`
```

## run all micro-frontend on local development
```bash
# clone recursive submodule
git clone --recursive git@github.com:wornut/mk-series.git

# install workspace deps
yarn install

# open new pane for running root-config
cd mk-root
yarn start

# open new pane for running auth app
cd mk-auth
yarn dev

# open new pane for running any app
```

## also you can run individual micro-frontend 
sometime we starting develop individual project on the localhost but another are running on the runtest server or hosting
```bash
cd someapp
yarn dev
```
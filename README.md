## require
- [mkcert](https://github.com/FiloSottile/mkcert)

## create self-certificate
- after install mkcert
```bash
mkdir cert # create cert directory
mkcert -install # install root CA
mkcert -key-file key.pem -cert-file cert.pem localhost ::1 # gen certificate for `localhost`
```

## run micro frontend
```bash
# clone recursive submodule
git clone --recursive git@github.com:wornut/mk-series.git

# install workspace deps
yarn install

# start pane 1 for root config
cd mk-root
yarn start

# start pane 2 for auth application
cd mk-auth
yarn dev
```
## Issue Tracker
-   [x] layout controller
    -   [x] layout controller should belong to ? `root-config` or a new `layout` application
        -   **pick** `root-config` to handle layout
    -   [x] load app condition, for example should render `auth` module before any modules
        -   **solution** use more than 1 script tag before `root-config` loaded
-   [x] vue over single-spa
    -   [x] async component `Foo: () => import('~/components/Foo')`
    -   [x] webpack resolve alias
        -   **solution** add webpack resolve alias block, resolve `src` path
    -   [ ] root dependecies control
        -   should not import latest cdn
-   [x] `assets` and `resource` configuration
    -   [x] cannot resolve assets from _single-spa/application_
        -   **solution** check `set_public_path` should import on the top of main file
-   [ ] development
    -   [x] local dev server need CORS support
    -   [x] use self-certificate on local dev server
        -   **solution** use [mkcert](https://github.com/FiloSottile/mkcert)
        -   **webpack dev server** set `key` and `cert` on [https](https://webpack.js.org/configuration/dev-server/#devserverhttps)
    -   [x] infer vue type
        -   **solution** declare vue module in `*.shim.d.ts` and add to tsconfig.json
    -   [ ] create custom `single-spa` boilerplate both `root-config`, `application | parcel` and `share module`
        -   **solution** we build [cli-tools]() to help initialize project
    -   [x] hot reload problem
        -   **solution** depends on `publicPath` webpack config
        -   if https required, _recheck self-certificate ip address_
    -   [x] support code splitting
        -   **solution** use [dynamic import](https://webpack.js.org/guides/code-splitting/#dynamic-imports)
    -   [x] support `vue composition api`
    -   [ ] support `vue 3`
    -   [ ] implement universal UI
    -   [x] mantainance problem, when we have many projects, which waty is the best option to handle its
        -   **solution** we use both `git submodule` and `yarn workspace`
            -   `yarn workspace` will control workspace dependencies. we can update/upgrade dependencies at the same time.
            -   `git submodule` will seperate project that will help us control project sizing and CI/CD 
-   [ ] security
    -   [x] should not import `package.json` directly, hide library infomation
        -   **solution-vue** pass environment variable through [_process.env.VUE_APP\_\*_](https://cli.vuejs.org/guide/mode-and-env.html#example-staging-mode)
    -   [ ] better CSP config

----

## Development
before starting development, we need to create self-cert into cert directory first, 
please following below steps

### 0. requires
- self-certificate by [mkcert](https://github.com/FiloSottile/mkcert)

### 1. create self-certificate
```bash
mkdir cert # create cert directory
mkcert -install # install root CA
mkcert -key-file key.pem -cert-file cert.pem localhost ::1 # gen certificate for `localhost`
```

### 2.1 run all micro-frontend on local development
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

### 2.2 also you can run individual micro-frontend 
sometime we starting develop individual project on the localhost but another are running on the runtest server or hosting
```bash
cd someapp
yarn dev
```
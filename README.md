nginx-upload-module-build
=========================

Build NGINX Upload module as installable packages for dynamic module.

Current Nginx version: 1.21.0

EL 9
----

* Install NGINX from EL9 AppStream with e.g. `dnf install nginx`

* Download [the pkg-oss script](https://github.com/natefoo/pkg-oss/blob/el9/build_module.sh) from [the `el9` branch](https://github.com/natefoo/pkg-oss/tree/el9) of [my pkg-oss fork](https://github.com/natefoo/pkg-oss/). These pkg-oss modifications are necessary since pkg-oss is made for upstream nginx.org repo versions of NGINX, not the OS-packaged version:

  ```
  wget https://github.com/natefoo/pkg-oss/raw/refs/heads/el9/build_module.sh
  ```

  and give it the right permissions:

  ```
  chmod a+x build_module.sh
  ```

* Build the module:

  ```
  ./build_module.sh -b openssl3 -v 1.20.1 https://github.com/natefoo/nginx-upload-module.git
  ```

  the rpm will be located in the ``build-module-artifacts`` directory:

  ```
  $ ls build-module-artifacts/
  nginx-module-upload-1.20.1+1.0-1.el9.ngx.x86_64.rpm  nginx-module-upload-debuginfo-1.20.1+1.0-1.el9.ngx.x86_64.rpm
  ```

* Install it using rpm:

  ```
  sudo rpm -i nginx-module-upload-1.20.1+1.0-1.el9.ngx.x86_64.rpm
  ```

* Finally, load the upload module, by editing the nginx configuration by adding, with your favourite text editor:

  ```
  load_module /usr/lib64/nginx/modules/ngx_http_upload_module.so;

  ```
  in NGINX configuration file.

CentOS 7
--------

* Install NGINX using the official NGINX CentOS7 repository, following the [documentation](http://nginx.org/en/linux_packages.html#RHEL-CentOS)

* Download the pkg-oss script to build the module

  ```
  wget https://hg.nginx.org/pkg-oss/raw-file/default/build_module.sh
  ```

  and give it the right permissions:

  ```
  chmod a+x build_module.sh
  ```

* Build the module:

  ```
  ./build_module.sh -v 1.21.0 https://github.com/fdintino/nginx-upload-module.git
  ```

  the rpm will be located in the ``build-module-artifacts`` directory:

  ```
  $ ls build-module-artifacts/
  nginx-module-upload-1.21.0+1.0-1.el7.ngx.x86_64.rpm  nginx-module-upload-debuginfo-1.21.0+1.0-1.el7.ngx.x86_64.rpm
  ```

* Install it using rpm:

  ```
  sudo rpm -i nginx-module-upload-1.21.0+1.0-1.el7.ngx.x86_64.rpm
  ```

* Finally, load the upload module, by editing the nginx configuration by adding, with your favourite text editor:

  ```
  load_module modules/ngx_http_upload_module.so;
  ```
  in NGINX configuration file.

References
----------

* https://gorails.com/blog/how-to-compile-dynamic-nginx-modules

* https://www.nginx.com/blog/creating-installable-packages-dynamic-modules/

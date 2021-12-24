# Description

Attempt rebuilding legacy docker image on alpine linux for more lean image size

docker build --rm -t local/alpine-rails:alpha-1 . 2>&1 | tee ../build.log

docker exec -it api bash

libressl-dev
curl -L https://get.rvm.io | rvm_tar_command=tar bash -s stable
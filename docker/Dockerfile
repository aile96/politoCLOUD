FROM ubuntu:latest AS ubuntu
ENV FILES=/fileDaGit
WORKDIR ${FILES}
RUN apt-get -qq update -y && apt-get install -qq hugo -y && apt-get -qq install git -y \
&& hugo new site $FILES && sed -i 's|baseURL = "http://example.org/"|baseURL = "/"|' $FILES/config.toml \
&& sed -i 's|title = "My New Hugo Site"|title = "My New Elia Site"|' $FILES/config.toml \
&& git init && git submodule add https://github.com/nanxiaobei/hugo-paper.git themes/hugo-paper \
&& echo theme = \"hugo-paper\" >> $FILES/config.toml && sed -i 's/draft: true/draft: false/' $FILES/archetypes/default.md \
&& hugo new _index.md && hugo new basic/_index.md && hugo new basic/first.md && hugo new basic/second.md \
&& hugo new advanced/_index.md && hugo new advanced/first.md && hugo new advanced/second.md && hugo -v

FROM nginx:latest
ENV FILES=/fileDaGit
COPY --from=ubuntu $FILES/public /usr/share/nginx/html

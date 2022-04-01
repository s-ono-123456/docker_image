# docker_image
1. 以下の手順通りにDocker Desktop for Windowsをインストールする。

    https://qiita.com/techpit-jp/items/f4a1319a909dd508f372

    ※2022/02に実施して同じ手順で問題なく動作しました。


1. コマンドプロンプトで以下のコマンドが叩けるか確認する。

    ```cmd
    > docker version

    Client:
     Cloud integration: v1.0.22
     Version:           20.10.12
     API version:       1.41
     Go version:        go1.16.12
     Git commit:        e91ed57
     Built:             Mon Dec 13 11:44:07 2021
     OS/Arch:           windows/amd64
     Context:           default
     Experimental:      true

    Server: Docker Desktop 4.5.1 (74721)
     Engine:
      Version:          20.10.12
      API version:      1.41 (minimum version 1.12)
      Go version:       go1.16.12
      Git commit:       459d0df
      Built:            Mon Dec 13 11:43:56 2021
      OS/Arch:          linux/amd64
      Experimental:     false
     containerd:
      Version:          1.4.12
      GitCommit:        7b11cfaabd73bb80907dd23182b9347b4245eb5d
     runc:
      Version:          1.0.2
      GitCommit:        v1.0.2-0-g52b36a2
     docker-init:
      Version:          0.19.0
      GitCommit:        de40ad0
    
    > docker-compose version
    docker-compose version 1.29.2, build 5becea4c
    docker-py version: 5.0.0
    CPython version: 3.9.0
    OpenSSL version: OpenSSL 1.1.1g  21 Apr 2020
    ```

1. 問題なければ以下のGitからソースコードをダウンロードする。

    https://github.com/s-ono-123456/docker_image

    以下のファイルにpythonの必要ライブラリを指定している。

    もし、追加したいライブラリがあれば、以下ファイルに記載するとよい。

    https://github.com/s-ono-123456/docker_image/blob/main/jupyter/py3/requirements.txt

1. 任意のフォルダに配置して、jupyter/up-down.cmdをダブルクリックする

    以下のような画面が立ち上がり、DockerImageのビルドが行われる。

    なお、初回起動の場合は20分くらいかかるので、気長に待つ。

    2回目以降はキャッシュされているので、すぐに起動する。（はず）

    ```
    Launch...
    Building py3
    [+] Building 1032.3s (9/9) FINISHED
    => [internal] load build definition from Dockerfile                                                               1.4s
    => => transferring dockerfile: 746B                                                                               0.0s
    => [internal] load .dockerignore                                                                                  1.8s
    => => transferring context: 2B                                                                                    0.0s
    => [internal] load metadata for docker.io/library/python:3.9.7-buster                                             4.0s
    => [internal] load build context                                                                                  0.7s
    => => transferring context: 1.06kB                                                                                0.0s
    => CACHED [1/4] FROM docker.io/library/python:3.9.7-buster@sha256:2ea1c4a9d762bb318f11cc6c7d9ce3fc71b928f5c70bbb  0.0s
    => [2/4] COPY ./requirements.txt requirements.txt                                                                 1.3s
    => [3/4] RUN apt-get update && apt-get install -y tzdata &&  ln -sf /usr/share/zoneinfo/Asia/Tokyo /etc/localt  139.8s
    => [4/4] RUN python3 -m pip install --upgrade pip &&  pip install --no-cache-dir -r requirements.txt            865.0s
    => exporting to image                                                                                            18.8s
    => => exporting layers                                                                                           18.1s
    => => writing image sha256:7c59ad62dedec679327c9171c6df5495139455e9e2d8f0dca0715a748a2c6d6b                       0.1s
    => => naming to docker.io/library/jupyter_py3                                                                     0.1s
    Creating network "jupyter_default" with the default driver
    Creating jupyter_py3_1 ... done
    Attaching to jupyter_py3_1
    py3_1  | [I 2022-04-01 21:32:00.534 ServerApp] jupyter_server_mathjax | extension was successfully linked.
    py3_1  | [W 2022-04-01 21:32:00.540 LabApp] 'token' has moved from NotebookApp to ServerApp. This config will be passed to ServerApp. Be sure to update your config before our next release.
    py3_1  | [I 2022-04-01 21:32:00.549 ServerApp] jupyterlab | extension was successfully linked.
    py3_1  | [I 2022-04-01 21:32:00.550 ServerApp] jupyterlab_code_formatter | extension was successfully linked.
    py3_1  | [I 2022-04-01 21:32:00.550 ServerApp] jupyterlab_git | extension was successfully linked.
    py3_1  | [I 2022-04-01 21:32:00.562 ServerApp] nbclassic | extension was successfully linked.
    py3_1  | [I 2022-04-01 21:32:00.562 ServerApp] nbdime | extension was successfully linked.
    py3_1  | [I 2022-04-01 21:32:00.564 ServerApp] Writing Jupyter server cookie secret to /root/.local/share/jupyter/runtime/jupyter_cookie_secret
    py3_1  | [I 2022-04-01 21:32:00.866 ServerApp] notebook_shim | extension was successfully linked.
    py3_1  | [W 2022-04-01 21:32:00.888 ServerApp] All authentication is disabled.  Anyone who can connect to this server will be able to run code.
    py3_1  | [I 2022-04-01 21:32:00.890 ServerApp] notebook_shim | extension was successfully loaded.
    py3_1  | [I 2022-04-01 21:32:00.891 ServerApp] jupyter_server_mathjax | extension was successfully loaded.
    py3_1  | [I 2022-04-01 21:32:00.892 LabApp] JupyterLab extension loaded from /usr/local/lib/python3.9/site-packages/jupyterlab
    py3_1  | [I 2022-04-01 21:32:00.893 LabApp] JupyterLab application directory is /usr/local/share/jupyter/lab
    py3_1  | [I 2022-04-01 21:32:00.897 ServerApp] jupyterlab | extension was successfully loaded.
    py3_1  | [I 2022-04-01 21:32:00.898 ServerApp] jupyterlab_code_formatter | extension was successfully loaded.
    py3_1  | [I 2022-04-01 21:32:00.904 ServerApp] jupyterlab_git | extension was successfully loaded.
    py3_1  | [I 2022-04-01 21:32:00.908 ServerApp] nbclassic | extension was successfully loaded.
    py3_1  | [I 2022-04-01 21:32:01.040 ServerApp] nbdime | extension was successfully loaded.
    py3_1  | [I 2022-04-01 21:32:01.041 ServerApp] Serving notebooks from local directory: /workspace
    py3_1  | [I 2022-04-01 21:32:01.041 ServerApp] Jupyter Server 1.16.0 is running at:
    py3_1  | [I 2022-04-01 21:32:01.041 ServerApp] http://e4dbf7d966a2:8888/lab
    py3_1  | [I 2022-04-01 21:32:01.041 ServerApp]  or http://127.0.0.1:8888/lab
    py3_1  | [I 2022-04-01 21:32:01.041 ServerApp] Use Control-C to stop this server and shut down all kernels (twice to skip confirmation).
    py3_1  | [I 2022-04-01 21:32:04.628 ServerApp] 302 GET / (172.18.0.1) 0.62ms
    py3_1  | [W 2022-04-01 21:32:07.520 LabApp] Could not determine jupyterlab build status without nodejs
    py3_1  | Generating grammar tables from /usr/local/lib/python3.9/site-packages/blib2to3/Grammar.txt
    py3_1  | Writing grammar tables to /root/.cache/black/22.3.0/Grammar3.9.7.final.0.pickle
    py3_1  | Writing failed: [Errno 2] No such file or directory: '/root/.cache/black/22.3.0/tmpz9m1_f3e'
    py3_1  | Generating grammar tables from /usr/local/lib/python3.9/site-packages/blib2to3/PatternGrammar.txt
    py3_1  | Writing grammar tables to /root/.cache/black/22.3.0/PatternGrammar3.9.7.final.0.pickle
    py3_1  | Writing failed: [Errno 2] No such file or directory: '/root/.cache/black/22.3.0/tmpjxvmdnpi'
    py3_1  | [W 2022-04-01 21:46:40.047 LabApp] Could not determine jupyterlab build status without nodejs

    ```

1. localhost:8888にjupyterがホストされ、自動でlocalhost:8888がブラウザで開く
    
    また、ノートブックはWindowsの jupyter/workspace フォルダに配置することで、Dockerコンテナと同期される。
    Dockerコンテナ上で保存したものもWindows上に自動保存されるため、コンテナを落としても、保持される。

    
1. なお、本GitHub Actionで自動ビルド及びDockerHubへの自動プッシュを行っているため、各端末でDockerイメージをPullしても良いが、サイズが1.5GBと大きいため、ローカルでビルドしたほうが良いと思われる。（通信制限とかを気にしないのであれば、以下からpullしても良いです。）

    ```
    docker pull sono123456/jupyter:latest
    ```
    
    https://hub.docker.com/repository/docker/sono123456/jupyter/general

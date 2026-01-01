
pyenv lets you easily switch between multiple versions of Python. It's simple, unobtrusive, and follows the UNIX tradition of single-purpose tools that do one thing well.

```shell

sudo apt update && sudo apt install -y \
    build-essential \
    libbz2-dev \
    libreadline-dev \
    libssl-dev \
    libsqlite3-dev \
    zlib1g-dev \
    libncursesw5-dev \
    libffi-dev \
    liblzma-dev \
    uuid-dev \
    tk-dev \
    libgdbm-dev \
    libnss3-dev \
    libgdbm-compat-dev \
    libdb-dev \
    libexpat1-dev \
    wget \
    curl \
    llvm


curl -fsSL https://pyenv.run | bash


export PATH="$HOME/.pyenv/bin:$PATH"
eval "$(pyenv init -)"
eval "$(pyenv virtualenv-init -)"



pyenv install 3.8.10

pyenv virtualenv 3.8.10 uncompyle-env
pyenv activate uncompyle-env
pip install uncompyle6




```
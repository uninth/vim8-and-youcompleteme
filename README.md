

# How to install YouCompleteMe and vim version 8 on Debian 10 (proxmox), Ubuntu 14, 16 and 18 using vim-plug

YouCompleteMe is a fast, as-you-type, fuzzy-search code completion engine for
Vim available from [vimawesome.com](http://vimawesome.com/plugin/youcompleteme)

There is - for the moment - no Ubuntu package compiled with python which is
required by the plugin. The following is a short description on how to install
everything.

First, install

    sudo apt-get install build-essential cmake python-dev python3-dev libncurses5-dev libncursesw5-dev

Then install vim from source:

`````bash
cd /usr/local/src
git clone https://github.com/vim/vim.git
cd vim
./configure --enable-pythoninterp=yes --enable-python3interp=yes  --enable-rubyinterp=yes
make install
`````

On Debian (buster) / proxmox the `configure` arguments should be

`````bash
./configure --enable-pythoninterp=yes --enable-python3interp=yes  --enable-rubyinterp=yes --enable-pythoninterp=yes --enable-python3interp=yes --with-python3-config-dir=/usr/lib/python3.7/config-3.7m-x86_64-linux-gnu/
`````

Now you have a vim version with the required components compled in.

Next install the minimalist Vim plugin manager [vim-plug](https://github.com/junegunn/vim-plug)

    curl -fLo ~/.vim/autoload/plug.vim --create-dirs \
    https://raw.githubusercontent.com/junegunn/vim-plug/master/plug.vim

Add all tree sections _Example_ and _On-demand loading of plugins_ and the _Post-update hooks_
from [vim-plug](https://github.com/junegunn/vim-plug) for _Valloric/YouCompleteMe_ to your `~/.vimrc`.

Start `/usr/local/bin/vim` and type

    :PlugInstall

The package manager will fetch everything and compile it. Your `.vim` will grow
to 450Mb.

If this is a true multiuser system you may want to move `~/.vim/autoload` and
`~/.vim/plugged` to ` /usr/local/share/vim/vim80/` and create links back to
your `.vim` directory.

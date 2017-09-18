padagraph.io meets HackFoldr
========

## <i class="fa fa-github"></i> foldr

#### padagraph fork of hackfoldr
https://github.com/padagraph/hackfoldr-2.0-forkme

## <i class="fa fa-github"></i> botapad
https://github.com/padagraph/botapad


### Dumpfoldr

#### <i class="fa fa-download"></i> backup your foldr

This program allow to dump the urls from a foldr configuration calc stored as an ethercalc.org document. 
 
    $ python foldr.py dump http://foldr.padagraph.io/pdgio  ./foldr-pdgio
    
#### <i class="fa fa-github"></i> Commit your files to github


* create a repository on github
https://github.com/new

* download and commit your files
```bash
cd ./foldr-pdgio
git init
git remote add origin git@github.com:ynnk/foldr-pdgio.git
git add *
git commit -am "first commit"
git push
```


### Botapad

Import tool to convert pad & calc to graphs.

#### Install

    $ pip install -r requirements.txt

#### Usage

    # see help :
    $ python botapad.py --help

    # exemple with framapad
    # edge graph
    $ python botapad.py fillon https://mensuel.framapad.org/p/qzpH0qxHkM/export/txt  --key `cat ../../key.txt` --separator ';'

    # projected graph
    $ python botapad.py uspol https://mensuel.framapad.org/p/uspol/export/txt  --key `cat ../../key.txt` --separator ','
    

### flask app / Botapadapp

Accessible Flask service for botapad  
#### Export host

    # routes: external server to compute layouts/clustering given
    $ export ENGINES_HOST=http://www.padagraph.io

#### copy your token

:::success
Tokens are required to store graphs to padagraph.io
:::

- get a token (http://padagraph.io/account/me/generate_auth_token)  
- copy this token to ```secret/key.txt``` 

#### Run  

    $ python botapadapp.py

#### Paths

    /
    /readme
    /stats
    /import
    /import/igraph    form
    /import/padagraph form
    /static/*.js css  



[DEPRECATED] requires ../../screenshot/screenshot.py in `$PYTHONPATH`
    
## TODO

* [star] starred projected node  

* [materials]nodetype materials (shape, color, size) ??   

* [import]circular import @[Nodetype]#id  
* [import]url expansion with some providers  
      [+] navigation for humans between pad, git, cloud ...  
      [-] url might be unaccurate with some providers  
      ex : 
        & https://mensuel.framapad.org/p/uspol  
        ! is converted during import to  https://mensuel.framapad.org/p/uspol/export/txt  



<a href="http://botapad.padagraph.io/import/igraph.html?s=framapad&gid=game_of_thrones&live=1&nofoot=1" target="iframe">voir ce graphe</a>

<iframe src="https://botapad.padagraph.io/import/igraph.html?s=framapad&gid=game_of_thrones&nofoot=1" style="width:100%; height:600px"/>


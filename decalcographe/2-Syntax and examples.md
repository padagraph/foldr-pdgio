
[toc]

# Syntax

We are using a csv like file format for data.  
One header is required to describe the content of the data.  
Some special characters are used at a begin line:  

*[Comments]*  
* '!' is used to comment a line, useful for discussion and help, it will be ignored by the program

*[Separator]*  
* is defined in the first line "!," a commented comma  can also use "!;"

*[Headers]*  
* '@' Header for nodes :  
* '_' Header for edges :  

*[Properties]*  
* '*' marker for starred nodes :  
* '+' marker for multiple values in column  
* '%' marker for projection :  
* '=' used with '%' create a clique with all cell elements :  
* '&' is an import directive to load external data  


`Headers` refers to `nodetypes` or `edgetypes` in the padagraph database.   
syntax is ```char name: prop; other``` with `char` in ( `@`,`_` )   
`:` after  Nodetype name and `;` between properties  
Properties are defined with a `Text` definition.  

## Graph data

We need to define  `nodetypes`, an `edgetypes` for graph data.
`nodetype`, an `edgetype` are described with properties.  

### @ Nodes

#### Add a nodetype  

    @ Person:  label ; image 

We just defined a `Person` nodetype with `properties`.

`label` is required and is the property used by padagraph to render in graphs and find nodes in the searchbox.  
`image` is used by padagraph to render nodes in graph.  

Indexed columns can be specified with an extra '#'.  

    @ Person: #num; label; image ; +roles

you will next use `num` values  to create `Relations` for shorthand and pad maintenance and uniqness.  

#### Add nodes data
Next row is expecting data from this table.  
Beginning and ending space will be removed in each cell.    

    *0; François Fillon; https://infographics.mediapart.fr/2017/nodes-fillon/img/nodes/0.png; candidat, premier ministre
    3; Myriam Lévy; https://infographics.mediapart.fr/2017/nodes-fillon/img/nodes/3.png
    4; Delphine Burgaud; https://infographics.mediapart.fr/2017/nodes-fillon/img/nodes/4.png
    5; Delphine Peyrat-Stricker; https://infographics.mediapart.fr/2017/nodes-fillon/img/nodes/5.png
    15; Anne Méaux; https://infographics.mediapart.fr/2017/nodes-fillon/img/nodes/15.png

Mind the node 0 , starting with `*` is `starred` .  


### _ Edge


`_` is the marker used to start a set of relation of a certain type.

    _ Knows: 

and the data we use the indexed column `num` to identify the nodes and create links.

    0 -- 5
    0 -- 4
    15 -- 4
    15 -- 3
    
:::warning
You have to keep your uniq ids for the whole data !!!!   
:::


### Using special properties

#### @ Nodes
* `label` displayed node text label 
* `image` url image 
* `shape` node shape in `circle`,`square`,`triangle`,`diamond`,`square`
* `size`   bigger or smaller node default is `1`


#### _ Relations
* `label` 
* `weight` 

## Reifications

Sometimes you want to use a property of the row as a Node with a link to the row node id  
Considere a list of politicians  

    @ Politic: %Chamber; #FirstName; #LastName; %Party; %State; %Stance; Statement;

    Senator,Lisa,Murkowski,R,AK,Neutral,"All weekend long my staff and I have been monitoring ..."
    Senator,Dan,Sullivan,R,AK,Support,"Excerpt -  The temporary restrictions, which I support,  ..."

we ll get a graph with 7 nodes from 5 types  
2 'Politics', 1 'Chamber' (Senator), 1 'State' (AK) , 1 'Party' (R) , 2 'Stance' ...  
and 8 edges.  

    Politic -- Chamber  (2) 
    Politic -- State   (2)
    Politic -- Party   (2)
    Politic -- Stance  (2)
        
## Imports 

As the data can be collected from  tiers,
they can also be used in a different datasets. 

    ! one set of data describe states ( code, name, image . )
    & https://mensuel.framapad.org/p/usstates/export/txt
    
    ! one to describe senators
    & https://mensuel.framapad.org/p/uspol/export/txt

    ! then add some nodes and links ..
    @ ...
    or
    _ ...


## Advanced :

###   mixing '%' and '+' in a prop will project row on each value of the cell  

     @ Test: #id ; %+ prop ; another
     1; a, b, c ; another
     ! this will create 3 links
     1 -- a
     1 -- b
     1 -- c
     
### mixing '%', '+' and '=' :

'=' create a clique of the nodes means create a link between each values  

     @ Test: #id ; %+= prop ; another
     1; a, b, c ; another
     ! this will create 3 links like row -- prop
     1 -- a
     1 -- b
     1 -- c

and also 3 links  

     a -- b
     a -- c
     b -- c
 



# Exemples


## Solar system

### data
<iframe src="https://docs.google.com/document/d/1pctuIXU4ioIjZ3v9P6vT8bpMMOVW_BUv1rYTFNctil8/edit" style="width:100%; height:600px"/>

### Graph 


<iframe src="https://botapad.padagraph.io/import/igraph.html?s=https://docs.google.com/document/d/1pctuIXU4ioIjZ3v9P6vT8bpMMOVW_BUv1rYTFNctil8/edit&gid=solar&nofoot=1" style="width:100%; height:400px"/>

:::success
Use the `refresh` button after edition to see your changes.
:::


### direct links
<a target="iframe" href="https://docs.google.com/document/d/1pctuIXU4ioIjZ3v9P6vT8bpMMOVW_BUv1rYTFNctil8/edit">[edit google doc]</a> <a target="iframe" href="http://botapad.padagraph.io/import/igraph.html?s=google&gid=1pctuIXU4ioIjZ3v9P6vT8bpMMOVW_BUv1rYTFNctil8&nofoot=1"> [import graph]</a> <a target="iframe" href="http://botapad.padagraph.io/googledoc/1pctuIXU4ioIjZ3v9P6vT8bpMMOVW_BUv1rYTFNctil8"> [Edit & visualise]</a>

## More examples

#### Réseau ferroviaire
`data` https://docs.google.com/document/d/1QiWDBtjxx6b_jnvvYrqFykiTSZzYn_F84hY7V_GsEQ8/edit
`graph` http://botapad.padagraph.io/import/igraph.html?s=google&gid=1QiWDBtjxx6b_jnvvYrqFykiTSZzYn_F84hY7V_GsEQ8&nofoot=1	

#### boat family tree
`data` https://docs.google.com/document/d/13YQ30xZHM-lTAifMBkUAcHagSOBo2Puy1PzZ_t1riPg/edit	
`graph` http://botapad.padagraph.io/import/igraph.html?s=google&gid=13YQ30xZHM-lTAifMBkUAcHagSOBo2Puy1PzZ_t1riPg&nofoot=1

#### Us Pol
`data` https://ethercalc.org/uspol	
`graph` http://botapad.padagraph.io/import/igraph.html?s=https://ethercalc.org/uspol&nofoot=1&gid=uspol






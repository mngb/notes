+++
title = "*rdf system"
author = ["PENG Kui"]
draft = false
+++

## Rdf System Structure {#rdf-system-structure}


## Rake Command {#rake-command}

-   rake set:wdir/pdir/fdir/sdir/gdir[abs_dir]
-   rake clean:wdir/pdir/fdir/sdir/nvm
-   rake install:ep/op/sip[ep-list/op-list/sip/rdf]
-   rake uninstall:ep/op/sip[ep-list/op-list/sip/rdf]
-   rake update:ep/op/sip[ep-list/op-list/rdf] # TODO
-   rake list:epc/opc/ep/op/sip/pr/wr
-   rake server[gem/git/web]
    -   **gem:** -   **cache:** cache ext gem from remote source, default all needed
        -   **push:** push own gem to local, default all ops
        -   **install:** install from cache, default all needed
        -   **pstart:** start push(own gem) server
        -   **cstart:** start cache(ext gem) server
-   rake migrate[all/op-list/ep-list]
-   rake emacs[...]
-   rake ruby[...]

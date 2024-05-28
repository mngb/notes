+++
title = "*electron"
author = ["PENG Kevin"]
draft = false
+++

## electron {#electron}


### node.js overview {#node-dot-js-overview}

-   refer <https://www.liaoxuefeng.com/wiki/1022910821149312/1023025732384672>
-   -   **v8:** javascript engine by GOOGLE
    -   **libev:** node.js uses libev for the event loop
        which in turn uses internal C++ thread pool to
        provide asynchronous I/O.
-   -   node -v
    -   npm 包管理工具
    -   node
    -   module.exports = &lt;module-name&gt;
-   基本模块
    -   global
    -   process
    -   fs,path,util,http,url,querystring,stream,crypto
-   <http://nodejs.cn/api/>


### electron overview {#electron-overview}

用web技术开发桌面应用, a module of node.js.

setup api-demo
: -   git clone <https://github.com/electron/electron-api-demos>
    -   npm i -g mirror-config-china --registry=<https://registry.npm.taobao.org>
    -   npm install
    -   -   **api:**

debug
: -   console.log
    -   win.webContents.openDevTools()

indium
: -   **configure file like this for nodejs program use electron:** ```javascript
        {
            "configurations": [
        	{
        	    "name": "demo",
        	    "type": "node",
        	    "program": "electron",
        	    "args": " ."
        	}
            ]
        }
        ```
    -   use 'indium-list-script-sources' list all known files by indium
    -   step run and breakpoint set has some issue, don't know how to solve
        refer <https://github.com/NicolasPetton/Indium/issues/232> this is a known issue
        can insert 'debugger' to passthrough this.


### electron detail {#electron-detail}

console
: nodejs
    -   can write to any stream

menu and menuItem
: -   **application menu:** Menu.setApplicationMenu(menu)
    -   **popup:** menu.popup

shortkey
: <https://www.electronjs.org/docs/api/accelerator>
    -   **global key:** (Ctrl, Alt, Shift, 0-9, a-z, Plus, Space, Tab, Backspace,...)
    -   **local key:** -   **menu:** accelerator 属性
    -   **browser key:** -   **BrowserWindow:** addEventListener OR use 'Mousetrap' library

start process
: nodejs api <http://nodejs.cn/api/child_process.html>
    -   exec('xxx')
    -   ruby server
    -   start ruby script

dialog
: <https://www.electronjs.org/docs/api/dialog>
    -   showOpenDialog
    -   showSaveDialog
    -   showMessageBox
    -   showErrorBox

html ui
: -   window.loadFile('index.html')
    -   layout
    -   button
    -   input
    -   form
    -   ...

package and release
: -

    -


### fiddle to study electron {#fiddle-to-study-electron}

-   <https://www.electronjs.org/fiddle>
-

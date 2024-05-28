+++
title = "svg"
author = ["PENG Kui"]
tags = ["html", "svg"]
draft = false
+++

## 文字 {#文字}

text
: ```html
    <svg>
      <text>Text</text>
    </svg>
    ```


## 形状 {#形状}

-   line
    ```html
    <svg>
      <line x1="0" y1="0" x2="100" y2="100"></line>
    </svg>
    ```

-   rect
    ```html
    <svg>
      <rect x="0" y="0" width="100" height="100" rx="5" yr="5"></rect>
    </svg>
    ```

-   circle
    ```html
    <svg>
      <circle cx="50" cy="50" r="50"></circle>
    </svg>
    ```

-   ellipse
    ```html
    <svg>
      <ellipse cx="50" cy="50" rx="50" ry="100"></ellipse>
    </svg>
    ```

-   polygon
    ```html
    <svg>
      <polygon points="0 0 100 100 200 300"></polygon>
    </svg>
    ```

-   polyline
    ```html
    <svg>
      <polyline points="0 0 100 100 200 300"></polyline>
    </svg>
    ```

-   path M/L/C/Q/S/T/A
    ```html
    <svg>
      <path d="M0,0 L100,100 "></path>
    </svg>
    ```


## 变换 (transform) {#变换--transform}

-   translate
    ```html
    <svg>
      <polygon points="0 0 100 100 200 300" transform="translate(100,100)"></polygon>
    </svg>
    ```

-   scale
    ```html
    <svg>
      <polygon points="0 0 100 100 200 300" transform="scale(2,2)"></polygon>
    </svg>
    ```

-   rotate
    ```html
    <svg>
      <polygon points="0 0 100 100 200 300" transform="rotate(90)"></polygon>
    </svg>
    ```


## 裁剪 (clip-path) {#裁剪--clip-path}

-   clipPath
    ```html
    <svg>
      <defs>
        <clipPath id="cut-off-bottom">
          <rect x="0" y="0" width="200" height="100" />
        </clipPath>
      </defs>

      <circle cx="100" cy="100" r="100" clip-path="url(#cut-off-bottom)" />
    </svg>

    ```


## 参考链接 {#参考链接}

Firefox SVG 教程 <https://developer.mozilla.org/zh-CN/docs/Web/SVG/Tutorial>

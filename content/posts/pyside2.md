+++
title = "pyside2"
author = ["PENG Kevin"]
draft = false
+++

## 基本内容 {#基本内容}


### 库 {#库}


#### Core {#core}

提供 Signal slot, 基类等基本核心功能


#### Gui {#gui}

提供窗口、事件、opengl, 2d 图形化功能等


#### Widget {#widget}

提供基本控件功能，如常用图形元素 Label,
布局，Button 等。


### 常用事件及绑定 {#常用事件及绑定}


#### 按键事件 {#按键事件}

-   `keyPressed(self, event)` 其中 event 可以是 QtCore.Qt.Key_a 等


#### 鼠标事件 {#鼠标事件}


#### 绘制事件 {#绘制事件}

`paintEvent(self, event)`


### 常用控件 {#常用控件}


#### QApplication {#qapplication}

1.  `app = QApplication(sys.argv)`
2.  = app.exec_() =


#### QMainWindow {#qmainwindow}

-   setCentralWidget(widget)
-   setFixedSize(QSize(width, height))
-   setWindowTitle(title)
-   show()


#### QLabel {#qlabel}

api
: -   `QLabel("Context")`
    -   setText(text)


#### QLineEdit {#qlineedit}

api
: -   setMaxLength(len)
    -   setPlaceholderText(text)

bind
: -   returnPressed(self)
    -   selectionChanged(self)
    -   textChanged(self,text)
    -   textEdited(self,text)


#### QCheckBox {#qcheckbox}

api
: -   setCheckState(Qt.Checked)

binding
: -   stateChanged(self, checked)


#### QPushButton {#qpushbutton}

api
: -   `QPushButton(text)`
    -   setCheckable(Bool)
    -   setChecked(Bool)
    -   setText(text)
    -   setEnabled(Bool)

binding
: -   clicked()
    -   released()


#### QDialog {#qdialog}

<!--list-separator-->

-  QMessageBox

    -   about(parent, title, message)
        返回值是 `QMessageBox.Ok`
    -   critical(parent, title, message)
    -   information(parent, title, message)
    -   question(parent, title, message)
        返回值是 `QMessageBox.Yes`
        或者 `QMessageBox.No`
    -   warning(parent, title, message)


#### QGLWidget {#qglwidget}


### 常用布局 {#常用布局}


#### 垂直布局 QVBoxLayout {#垂直布局-qvboxlayout}

-   addWidget(widget)
-   addLayout(layout)


#### 水平布局 QHBoxLayout {#水平布局-qhboxlayout}

-   addWidget(widget)
-   addLayout(layout)


#### 网格布局 QGridLayout {#网格布局-qgridlayout}

-   addWidget(widget, x, y)


#### 层叠布局 QStackedLayout {#层叠布局-qstackedlayout}

-   addWidget(widget)
-   setCurrentIndex(z)


### 常用代码片断 {#常用代码片断}


#### 启动应用程序 {#启动应用程序}

```python
from PySide2.QtWidgets import QApplication, QMainWindow
from PySide2.QtCore import QSize
import sys
app = QApplication(sys.argv)
main_win = QMainWindow()
main_win.setWindowTitle("MainWindow")
main_win.setFixedSize(QSize(800, 600))
main_win.show()
app.exec_()
```


#### 简单表单程序 {#简单表单程序}

```python
from PySide2.QtWidgets import (
    QApplication,
    QMainWindow,
    QWidget,
    QLabel,
    QLineEdit,
    QPushButton,
    QVBoxLayout,
    QMessageBox
)
from PySide2.QtCore import QSize
import sys

class MainWindow(QMainWindow):
    def __init__(self, parent=None):
        super(MainWindow, self).__init__(parent)
        self.label_name = QLabel("Name:")
        self.input_name = QLineEdit("")
        self.label_age = QLabel("Age:")
        self.input_age = QLineEdit("")
        self.submit = QPushButton("Submit")
        self.layout = QVBoxLayout()
        self.layout.addWidget(self.label_name)
        self.layout.addWidget(self.input_name)
        self.layout.addWidget(self.label_age)
        self.layout.addWidget(self.input_age)
        self.layout.addWidget(self.submit)
        self.center = QWidget()
        self.center.setLayout(self.layout)
        self.setCentralWidget(self.center)
        self.submit.clicked.connect(self.submit_form)

    def submit_form(self):
        QMessageBox.information(self, "FormSubmit", "Submit success!")

app = QApplication(sys.argv)
main_win = MainWindow()
main_win.setWindowTitle("FormDemo")
main_win.setFixedSize(QSize(800, 600))
main_win.show()
app.exec_()
```


#### 简单布局和事件交互程序 {#简单布局和事件交互程序}

```python
from PySide2.QtWidgets import (
    QApplication,
    QMainWindow,
    QMessageBox,
    QWidget
)
from PySide2.QtCore import (
    QSize,
    Qt
)
import sys
from PySide2.QtGui import QPainter

class Canvas(QWidget):
    def __init__(self):
        super(Canvas, self).__init__()
        self.draw_rect = True

    def paintEvent(self, event):
        qp = QPainter()
        qp.begin(self)
        qp.setPen(Qt.red)
        qp.drawPoint(10, 10)
        qp.drawLine(0, 0, 100, 100)
        if self.draw_rect:
            qp.drawRect(0, 0, 100, 100)
        qp.end()

    def toggle_rect(self):
        self.draw_rect = not self.draw_rect

class MainWindow(QMainWindow):
    def __init__(self, parent=None):
        super(MainWindow, self).__init__(parent)
        self.canvas = Canvas()
        self.setCentralWidget(self.canvas)
    def keyPressEvent(self, event):
        self.canvas.toggle_rect()
        self.canvas.update()

app = QApplication(sys.argv)
main_win = MainWindow()
main_win.setWindowTitle("GameDemo")
main_win.setFixedSize(QSize(800, 600))
main_win.show()
app.exec_()
```


#### OpenGL Widget 程序 {#opengl-widget-程序}


## 参考链接 {#参考链接}

官方网站 <https://doc.qt.io/qtforpython-5/contents.html>
API 列表 <https://doc.qt.io/qtforpython-5/modules.html>
总结性的教程 <https://www.pythonguis.com/pyside2/>

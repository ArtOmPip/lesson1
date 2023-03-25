from PyQt5.QtWidgets import QApplication, QWidget, QLabel, QLineEdit, QHBoxLayout, QVBoxLayout, QPushButton
from PyQt5.QtCore import Qt

#инициализация глобальных переменных
name = ''
age = 7
p1, p2, p3 = 0, 0, 0

win_x, win_y = 200, 100
win_w, win_h = 1000, 600

txt_title = 'Тест Руфье'

#первый экран(Имя)
class InstrScr(QWidget):
    def __init__(self):
        super().__init__()
        self.initUi()
        self.connect()
        self.set_appear()
        self.show()

    def initUi(self):
        #создание чего-то основного
        self.lbl_instr = QLabel('Надо вот так.')
        self.lbl_name = QLabel('Введите имя:')
        self.inp_name = QLineEdit()
        self.lbl_age = QLabel('Введите возраст:')
        self.inp_age = QLineEdit('7')
        self.btn = QPushButton('Начать')
        
        #создание линий
        self.line = QVBoxLayout()
        self.h_line_name = QHBoxLayout()
        self.h_line_age = QHBoxLayout()
        
        #размещение виджетов по линиям
        self.h_line_name.addWidget(self.lbl_name)
        self.h_line_name.addWidget(self.inp_name)
        self.h_line_age.addWidget(self.lbl_age)
        self.h_line_age.addWidget(self.inp_age)
        self.line.addWidget(self.lbl_instr, alignment= Qt.AlignCenter)
        self.line.addLayout(self.h_line_name)
        self.line.addLayout(self.h_line_age)
        self.line.addWidget(self.btn, alignment= Qt.AlignCenter)
        self.setLayout(self.line)

    def connect(self):
        self.btn.clicked.connect(self.next_click)
    
    def next_click(self):
        self.ps = PulsScr()
        self.hide()

    def set_appear(self):
        self.setWindowTitle(txt_title)
        self.resize(win_w, win_h)
        self.move(win_x, win_y)

#второй экран(Состояние покоя)
class PulsScr(QWidget):
    def __init__(self):
        super().__init__()
        self.set_appear()
        self.show()
        
    def set_appear(self):
        self.setWindowTitle(txt_title)
        self.resize(win_w, win_h)
        self.move(win_x, win_y)

#третий экран
class ChekSits(QWidget):
    def __init__(self):
        super().__init__()
        self.set_appear()
        self.show()

    def set_appear(self):
        self.setWindowTitle(txt_title)
        self.resize(win_w, win_h)
        self.move(win_x, win_y)

#четвёртый экран
class PulsScr2(QWidget):
    def __init__(self):
        super().__init__()
        self.set_appear()
        self.show()

    def set_appear(self):
        self.setWindowTitle(txt_title)
        self.resize(win_w, win_h)
        self.move(win_x, win_y)

#пятый экран
class Result(QWidget):
    def __init__(self):
        super().__init__()
        self.set_appear()
        self.show()

    def set_appear(self):
        self.setWindowTitle(txt_title)
        self.resize(win_w, win_h)
        self.move(win_x, win_y)

app =  QApplication([])
mw = InstrScr()
app.exec_()


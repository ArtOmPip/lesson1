from PyQt5.QtWidgets import QApplication, QWidget, QLabel, QLineEdit, QHBoxLayout, QVBoxLayout, QPushButton
from PyQt5.QtCore import Qt
from innstr import *
#инициализация глобальных переменных
name = ''
age = 7
p1, p2, p3 = 0, 0, 0


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
        self.lbl_instr = QLabel(txt_instruction)
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
        self.mw = PulsScr()
        self.hide()

    def set_appear(self):
        self.setWindowTitle(txt_title)
        self.resize(win_w, win_h)
        self.move(win_x, win_y)

#второй экран(Состояние покоя)
class PulsScr(QWidget):
    def __init__(self):
        super().__init__()
        self.initUi()
        self.connect()
        self.set_appear()
        self.show()
        
    def set_appear(self):
        self.setWindowTitle(txt_title)
        self.resize(win_w, win_h)
        self.move(win_x, win_y)

    def initUi(self):
        self.instr = QLabel(txt_starttest1)
        self.text_p1 = QLabel('Введите результат:')
        self.line_p1 = QLineEdit('0')
        self.btn_next = QPushButton(txt_next, self)
        self.h_line = QHBoxLayout()
        self.h_line.addWidget(self.text_p1)
        self.h_line.addWidget(self.line_p1)
        self.line = QVBoxLayout()
        self.line.addWidget(self.instr, alignment = Qt.AlignCenter)
        self.line.addLayout(self.h_line)
        self.line.addWidget(self.btn_next, alignment = Qt.AlignCenter)
        self.setLayout(self.line)
    
        self.layout_line = QVBoxLayout()

    def connect(self):
        self.btn_next.clicked.connect(self.next_click)
    
    def next_click(self):
        self.mw = ChekSits()
        self.hide()

    def set_appear(self):
        self.setWindowTitle(txt_title)
        self.resize(win_w, win_h)
        self.move(win_x, win_y) 



#третий экран
class ChekSits(QWidget):
    def __init__(self):
        super().__init__()
        self.initUi()
        self.connect()
        self.set_appear()
        self.show()

    def set_appear(self):
        self.setWindowTitle(txt_title)
        self.resize(win_w, win_h)
        self.move(win_x, win_y)

    def initUi(self):
        self.instr = QLabel(txt_starttest2)
        self.btn_next = QPushButton(txt_next, self)
        self.line = QVBoxLayout()
        self.line.addWidget(self.instr, alignment = Qt.AlignCenter)
        self.line.addWidget(self.btn_next, alignment = Qt.AlignCenter)
        self.setLayout(self.line)

    def connect(self):
        self.btn_next.clicked.connect(self.next_click)
    
    def next_click(self):
        self.Ps = PulsScr2()
        self.hide()

    def set_appear(self):
        self.setWindowTitle(txt_title)
        self.resize(win_w, win_h)
        self.move(win_x, win_y) 


#четвёртый экран
class PulsScr2(QWidget):
    def __init__(self):
        super().__init__()
        self.initUi()
        self.connect()
        self.set_appear()
        self.show()

    def set_appear(self):
        self.setWindowTitle(txt_title)
        self.resize(win_w, win_h)
        self.move(win_x, win_y)

    def initUi(self):
        #создание чего-то основного
        self.lbl_instr = QLabel(txt_test3)
        self.lbl_p1 = QLabel('Введите результат:')
        self.inp_p1 = QLineEdit('0')
        self.lbl_p2 = QLabel('Введите результат после отдыха:')
        self.inp_p2 = QLineEdit('0')
        
        #создание линий
        self.line1= QHBoxLayout()
        self.line2 = QHBoxLayout()
        
        self.line1.addWidget(self.lbl_p1)
        self.line1.addWidget(self.inp_p1)
        self.line2.addWidget(self.lbl_p2)
        self.line2.addWidget(self.inp_p2)
        self.btn_next = QPushButton(txt_next)
        self.line = QVBoxLayout()  
        self.line.addWidget(self.lbl_instr, alignment= Qt.AlignCenter)
        self.line.addLayout(self.line1)
        self.line.addLayout(self.line2)
        self.line.addWidget(self.btn_next, alignment= Qt.AlignCenter)
        self.setLayout(self.line)       

    def connect(self):
        self.btn_next.clicked.connect(self.next_click)
    
    def next_click(self):
        self.mw = Result()
        self.hide()

    def set_appear(self):
        self.setWindowTitle(txt_title)
        self.resize(win_w, win_h)
        self.move(win_x, win_y)


#пятый экран
class Result(QWidget):
    def __init__(self):
        super().__init__()        
        self.initUi()
        self.set_appear()
        self.show()

    def initUi(self):
        self.w_text = QLabel(txt_workheart)
        self.i_text = QLabel(txt_index)

        self.line = QVBoxLayout()
        self.line.addWidget(self.i_text, alignment= Qt.AlignCenter)
        self.line.addWidget(self.w_text, alignment= Qt.AlignCenter)
        self.setLayout(self.line)

    def set_appear(self):
        self.setWindowTitle(txt_title)
        self.resize(win_w, win_h)
        self.move(win_x, win_y)

app =  QApplication([])
mw = InstrScr()
app.exec_()


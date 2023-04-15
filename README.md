from PyQt5.QtWidgets import QApplication, QWidget, QLabel, QLineEdit, QHBoxLayout, QVBoxLayout, QPushButton, QMessageBox
from PyQt5.QtCore import Qt
from innstr import *
from PyQt5.QtGui import QFont
#инициализация глобальных переменных
name = ''
age = 7
p1, p2, p3 = 1, 1, 1


def error_init(intg):
    try:
        return int(intg)
    
    except:
        return False

#класс важный
class Person():
    def __init__(self, name, age):
        self.name = name()
        self.age = age()

class Experiment():
    def __init__(self, person, test1, test2, test3):
        self.person = person()
        self.test1 = test1()
        self.test2 = test2()
        self.test3 = test3()

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
        self.lbl_instr.setFont(QFont(None, 15))
        self.lbl_name = QLabel('Введите имя:')
        self.inp_name = QLineEdit()
        self.lbl_age = QLabel('Введите возраст:')
        self.inp_age = QLineEdit('7')
        self.btn = QPushButton('Начать')
        self.btn.setStyleSheet('background: rgb(73, 89, 94)')

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
        global name, age
        name = self.inp_name.text()
        age = error_init(self.inp_age.text())
        if age == False or age < 7:
            msg = QMessageBox()
            msg.setWindowTitle("Ошибка возраста")
            msg.setText("Возраст должен быть больше 7 лет и состоять из цифр!")
            msg.setIcon(msg.Warning)
            msg.exec_()
            age = 7
            self.inp_age.setText(str(age))
        else:
            self.tw = PulsScr()
            self.hide()


    def set_appear(self):
        self.setWindowTitle(txt_title)
        self.resize(win_w, win_h)
        self.move(win_x, win_y)
        self.setStyleSheet('background-color: rgb(61, 58, 96)')

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
        self.setStyleSheet('background-color: rgb(61, 58, 96)')

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
        self.btn_next.setStyleSheet('background: rgb(73, 89, 94)')   
        self.layout_line = QVBoxLayout()
        self.instr.setFont(QFont(None, 15))

    def connect(self):
        self.btn_next.clicked.connect(self.next_click)
    
    def next_click(self):
        global p1
        p1 = error_init(self.line_p1.text())
        if p1 == False or p1 <= 0:
            msg = QMessageBox()
            msg.setWindowTitle("Ошибка пульса")
            msg.setText("Пульс должен быть больше 0 и соостоять из цифр!")
            msg.setIcon(msg.Warning)
            msg.exec_()
            p1 = 0
            self.line_p1.setText(str(p1))
        else:
            self.tw = ChekSits()
            self.hide()


    def set_appear(self):
        self.setWindowTitle(txt_title)
        self.resize(win_w, win_h)
        self.move(win_x, win_y) 
        self.setStyleSheet('background-color: rgb(61, 58, 96)')


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
        self.btn_next.setStyleSheet('background: rgb(73, 89, 94)')   
        self.instr.setFont(QFont(None, 15))

    def connect(self):
        self.btn_next.clicked.connect(self.next_click)
    
    def next_click(self):
        self.Ps = PulsScr2()
        self.hide()

    def set_appear(self):
        self.setWindowTitle(txt_title)
        self.resize(win_w, win_h)
        self.move(win_x, win_y) 
        self.setStyleSheet('background-color: rgb(61, 58, 96)')

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
        self.lbl_p2 = QLabel('Введите результат:')
        self.inp_p2 = QLineEdit('0')
        self.lbl_p3 = QLabel('Введите результат после отдыха:')
        self.inp_p3 = QLineEdit('0')
        
        #создание линий
        self.line1 = QHBoxLayout()
        self.line1.addStretch(5)
        self.line2 = QHBoxLayout()
        
        self.line1.addWidget(self.lbl_p2)
        self.line1.addWidget(self.inp_p2)
        self.line2.addWidget(self.lbl_p3)
        self.line2.addWidget(self.inp_p3)
        self.btn_next = QPushButton(txt_next)
        self.line = QVBoxLayout()  
        self.line.addWidget(self.lbl_instr, alignment= Qt.AlignCenter)
        self.line.addLayout(self.line1)
        self.line.addLayout(self.line2)
        self.line.addWidget(self.btn_next, alignment= Qt.AlignCenter)
        self.setLayout(self.line)       
        self.btn_next.setStyleSheet('background: rgb(73, 89, 94)')   

    def connect(self):
        self.btn_next.clicked.connect(self.next_click)
    
    def next_click(self):
        global p2, p3
        p2 = error_init(self.inp_p2.text())
        p3 = error_init(self.inp_p3.text())
        if p2 == False or p2 <= 0:
            msg = QMessageBox()
            msg.setWindowTitle("Ошибка пульсв")
            msg.setText("Пульс должен быть больше 0 и соостоять из цифр!")
            msg.setIcon(msg.Warning)
            msg.exec_()
            p2 = 0
            self.inp_p2.setText(str(p2))
        elif p3 == False or p3 <= 0:
            msg = QMessageBox()
            msg.setWindowTitle("Ошибка пульсв")
            msg.setText("Пульс после отдыха должен быть больше 0 и соостоять из цифр!")
            msg.setIcon(msg.Warning)
            msg.exec_()
            p3 = 0
            self.inp_p3.setText(str(p3))
        else:
            self.tw = Result()
            self.hide()

    def set_appear(self):
        self.setWindowTitle(txt_title)
        self.resize(win_w, win_h)
        self.move(win_x, win_y)
        self.setStyleSheet('background-color: rgb(61, 58, 96)')

#пятый экран
class Result(QWidget):
    def __init__(self):
        super().__init__()        
        self.initUi()
        self.set_appear()
        self.show()
        #self exp = exp

    def results(self):
        if age < 7:
            self.index = 0
            return 'нет данных для такого возраста'
        self.index = (4 *(int(p1) + int(p2) + int(p3)) - 200) / 10
        if age == 7 or age == 8:
            if self.index >= 21:
                return txt_res1
            elif self.index < 21 and self.index >= 17:
                return txt_res2
            elif self.index <17 and self.index >= 12:
                return txt_res3
            elif self.index < 12 and self.index >= 6.5:
                return txt_res4
            return txt_res5

        if age == 9 or age == 10:
            if self.index >= 19.5:
                return txt_res1
            elif self.index < 19.4 and self.index >= 15.5:
                return txt_res2
            elif self.index < 15.4 and self.index >= 10.5:
                return txt_res3
            elif self.index < 10.4 and self.index >= 5:
                return txt_res4
            return txt_res5

        if age == 11 or age == 12:
            if self.index >= 18:
                return txt_res1
            elif self.index < 18 and self.index >= 14:
                return txt_res2
            elif self.index < 14 and self.index >= 9:
                return txt_res3
            elif self.index < 9 and self.index >= 3.5:
                return txt_res4
            return txt_res5

        if age == 13 or age == 14:
            if self.index >= 16.5:
                return txt_res1
            elif self.index < 16.5 and self.index >= 12.5:
                return txt_res2
            elif self.index < 12.5 and self.index >= 7.5:
                return txt_res3
            elif self.index < 7.5 and self.index >= 2:
                
                return txt_res4
            return txt_res5

        if age > 15:
            if self.index >= 15:
                return txt_res1
            elif self.index < 15 and self.index >= 11:
                return txt_res2
            elif self.index < 11 and self.index >= 6:
                return txt_res3
            elif self.index < 6 and self.index >= 0.4:
                return txt_res4
            return txt_res5

    def initUi(self):
        self.w_text = QLabel(txt_workheart + self.results())
        self.i_text = QLabel(name + '\n\n\n\n'+txt_index + str(self.index))

        self.line = QVBoxLayout()
        self.line.addWidget(self.i_text, alignment= Qt.AlignCenter)
        self.line.addWidget(self.w_text, alignment= Qt.AlignCenter)
        self.setLayout(self.line)

    def set_appear(self):
        self.setWindowTitle(txt_title)
        self.resize(win_w, win_h)
        self.move(win_x, win_y)
        self.setStyleSheet('background-color: rgb(62, 72, 105)')
app =  QApplication([])
mw = InstrScr()
app.exec_()


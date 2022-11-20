from pprint import pprint




class Mentor:

    def __init__(self, name, surname):
        self.name = name
        self.surname = surname
        self.courses_attached = []
    def add_cour_attached(self, course):
        self.courses_attached.append(course)

class Student:

    def __init__(self, name, surname, gender):
        self.name = name
        self.surname = surname
        self.gender = gender
        self.finished_courses = []
        self.courses_in_progress = []
        self.grades = {}
        self.grades_list = []
        self.ave_grade = float

    def __str__(self):
        text = (f"Имя:{self.name}",
                f" Фамилия:{self.surname}",
                f" Средняя оценка за домашние задания :{float(sum(self.grades.values())/len(self.grades.keys()))}",
                f" Изучаемые курсы:{self.courses_in_progress}",
                f" Изученные курсы:{self.finished_courses}")
        return text



    def add_fin_course(self, course):
        self.finished_courses.append(course)

    def add_progress_courses(self, course):
        self.courses_in_progress.append(course)



    def rate_lect(self, lecturer, course, digit):

        if isinstance(lecturer, Lecturer):
            if course in self.courses_in_progress and course in lecturer.course_lect:
                lecturer.rate.append(digit)

            else:
                raise ('Ошибка')
        else:
            raise ('Это не лектор')


    def average_grade(self):
        self.ave_grade = sum(self.grades.values())/len(self.grades.keys())
        return self.ave_grade

    def __eq__(self, other):
        return self.ave_grade == other.ave_grade

class Reviewer(Mentor):

    def rate_hw(self, student, course, grade):
        if isinstance(student, Student) and course in self.courses_attached and course in student.finished_courses:
            if course in student.grades:
                student.grades[course] = int(grade)
                student.grades_list.append(int(grade))
            else:
                return "Ошибка"
        else:

            return 'Ошибка'

    def __str__(self):
        text_rev = (f"Имя:{self.name}",
                    f"Фамилия:{self.surname}"
        )
        return text_rev

class Lecturer(Mentor):

    def __init__ (self, name, surname):
        self.name = name
        self.surname = surname
        self.rate = []
        self.course_lect = []
        self.ave_rate = float
    def __str__(self):
        text_lec = (f"Имя:{self.name}",
                  f" Фамилия:{self.surname}",
                  f"Средняя оценка за лекции :{float(sum(self.rate))/len(self.rate)}")
        return text_lec


    def add_cour_lect(self, course):
        self.course_lect.append(course)

    def add_ave_rate(self):
        self.ave_rate = (sum(self.rate)) / len(self.rate)
        return self.ave_rate

    def __eq__(self, other):
        return self.ave_rate == other.ave_rate


student_list = []

student1 = Student('Пётр', 'Максимов', 'мужской')

student1.add_fin_course('Базы данных')

student1.add_fin_course('Управление проектами')

student1.grades['Базы данных'] = None

student1.grades['Управление проектами'] = None

student1.add_progress_courses("Алгоритмизация и программирование")

student1.add_progress_courses("Архитектура компьютера")


student_list.append(student1)


student_list.append(student1)

student2 = Student('Дмитрий', 'Коваль', 'мужской')

student2.add_fin_course('Базы данных')

student2.add_fin_course('Управление проектами')

student2.add_progress_courses("Архитектура компьютера")

student2.add_progress_courses("Алгоритмизация и программирование")

student2.grades['Базы данных'] = None

student2.grades['Управление проектами'] = None

student_list.append(student2)




lecturer1 = Lecturer('Дмитрий','Зубарев')

lecturer1.add_cour_lect('Архитектура компьютера')

lecturer2 = Lecturer('Максим', 'Косов')

lecturer2.add_cour_lect("Алгоритмизация и программирование")

lecturer_list = []

lecturer_list.append(lecturer1)

lecturer_list.append(lecturer2)



student1.rate_lect(lecturer1, "Архитектура компьютера", 8)

student1.rate_lect(lecturer2, "Алгоритмизация и программирование", 9)

student2.rate_lect(lecturer1, "Архитектура компьютера", 9)

student2.rate_lect(lecturer2, "Алгоритмизация и программирование", 10)


lecturer1.__eq__(lecturer2)

lecturer2.__eq__(lecturer1)

reviewer1 = Reviewer('Андрей', 'Кобылкин')

reviewer2 = Reviewer('Виталия', 'Арсенина')

reviewer2.add_cour_attached('Базы данных')

reviewer1.add_cour_attached('Управление проектами')

reviewer1.rate_hw(student1, "Управление проектами", 10)

reviewer1.rate_hw(student2, "Управление проектами", 9)

reviewer2.rate_hw( student1, "Базы данных", 8)

reviewer2.rate_hw( student2, "Базы данных", 10)

student1.__eq__(student2)

student2.__eq__(student1)


pprint(reviewer1.__str__())

pprint(lecturer1.__str__())

pprint(lecturer2.__str__())

pprint(student1.__str__())
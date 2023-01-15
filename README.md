# oop-Mentors-and-students
class Mentor:
    def __init__(self, name, surname):
        self.name = name
        self.surname = surname
        self.courses_attached = []
        self.grades = {}

    def rate_hw(self, student, course, grade):
        if isinstance(student, Student) and course in self.courses_attached and course in student.courses_in_progress:
            if course in student.grades:
                student.grades[course] += [grade]
            else:
                student.grades[course] = [grade]
        else:
            return 'Ошибка'

    def mid_grade(self):
        for grade in self.grades:
            mid = sum(self.grades[grade]) / len(self.grades[grade])
            return mid


class Lecturer(Mentor):
    def __init__(self, name, surname, courses_attached):
        super().__init__(name, surname)
        self.courses_attached = courses_attached

    def __str__(self):
        return f"ЛЕКТОР:\n{self.name}\n{self.surname}\nСредняя оценка за лекции:{self.mid_grade()}"


class Student:
    def __init__(self, name, surname, gender):
        self.name = name
        self.surname = surname
        self.gender = gender
        self.finished_courses = ["Введение в программирование"]
        self.courses_in_progress = ["Python", "Git"]
        self.grades = {}
        self.dict = []

    def __str__(self):
        return f"СТУДЕНТ:\n{self.name}\n{self.surname}\nСредняя оценка за домашние задания: {self.mid_grade()}\n" \
               f"Курсы в процессе изучения:{self.courses_in_progress}\nЗавершенные курсы:{self.finished_courses}"

    def rate_hw(self, lecturer, course, grade):
        if isinstance(lecturer,
                      Lecturer) and course in self.courses_in_progress and course in lecturer.courses_attached:
            if course in lecturer.grades:
                lecturer.grades[course] += [grade]
            else:
                lecturer.grades[course] = [grade]
        else:
            return 'Ошибка'

    def mid_grade(self):
        for grade in self.grades:
            mid = sum(self.grades[grade]) / len(self.grades[grade])
            return mid

    def function(self, other):
        if not isinstance(other, Student):
            return 'Ошибка'

        if self.mid_grade() < other.mid_grade():
            return f'Средняя оценка студента {self.name} меньше, чем у студента {other.name}'
        elif self.mid_grade() > other.mid_grade():
            return f'Средняя оценка студента {self.name} больше, чем у студента {other.name}'
        else:
            return f'Средняя оценки студентов {self.name} и {other.name} равны'


class Reviewer(Mentor):
    def __init__(self, name, surname):
        super().__init__(name, surname)

    def __str__(self):
        return f"Проверяющий:\n{self.name}\n{self.surname}"


# Индексация, доступ к элементу (словаря, списка) по индексу
# students = [best_student, best_student_one, best_student_two]
def mid_grades(student_list, course, class_name):
    summ = 0
    quantity = 0
    for student in student_list:
        summ += sum(student.__dict__['grades'][course])
        quantity += len(student.__dict__['grades'][course])
  # lecturers = [lecturer, lecturer_one, lecturer_two]
def mid_grades(student_list, course, class_name):
    summ = 0
    quantity = 0
    for student in student_list:
        summ += sum(student.__dict__['grades'][course])
        quantity += len(student.__dict__['grades'][course])

    return f"Средняя оценка за курс {course} у всех {class_name}: {round(summ / quantity, 2)}"
    def __eq__(self, other):
        return self.mid_grade() == other.mid_grade()

    # !=
    def __ne__(self, other):
        return self.mid_grade() != other.mid_grade()

    # <
    def __lt__(self, other):
        return self.mid_grade() < other.mid_grade()

    # >
    def __gt__(self, other):
        return self.mid_grade() > other.mid_grade()


# lecturer 1
lecturer = Lecturer("Some", "Buddy", "Python")
lecturer.courses_attached = ["Python"]

# lecturer 2
lecturer_one = Lecturer("Lesha", "Corepanoff", "Python")
lecturer_one.courses_attached = ["Python"]

# lecturer 3
lecturer_two = Lecturer("Masha", "Tinkoffa", "Python")
lecturer_two.courses_attached = ["Python"]

# student 1
best_student = Student('Ruoy', 'Eman', 'your_gender')
best_student.courses_in_progress += ["Python"]
best_student.rate_hw(lecturer, 'Python', 10)
best_student.rate_hw(lecturer, 'Python', 8)
best_student.rate_hw(lecturer, 'Python', 10)

# student 2
best_student_one = Student('Elizaveta', 'Comoffa', 'your_gender')
best_student_one.courses_in_progress += ["Python"]
best_student_one.rate_hw(lecturer_one, 'Python', 10)
best_student_one.rate_hw(lecturer_one, 'Python', 4)
best_student_one.rate_hw(lecturer_one, 'Python', 4)

# student 3
best_student_two = Student('Natasha', 'Comoffa-Vulgata', 'fem')
best_student_two.courses_in_progress += ["Python"]
best_student_two.rate_hw(lecturer_two, 'Python', 1)
best_student_two.rate_hw(lecturer_two, 'Python', 1)
best_student_two.rate_hw(lecturer_two, 'Python', 7)

# original student
best_student = Student('Ruoy', 'Eman', 'your_gender')
best_student.courses_in_progress += ['Python']

# reviewer 1
reviewer = Reviewer('Don', 'Jon')
reviewer.courses_attached += ['Python']
reviewer.rate_hw(best_student, 'Python', 10)
reviewer.rate_hw(best_student, 'Python', 5)
reviewer.rate_hw(best_student, 'Python', 10)

# reviewer 2
reviewer_one = Reviewer("Jack", "London")
reviewer_one.courses_attached += ['Python']
reviewer_one.rate_hw(best_student_one, 'Python', 4)
reviewer_one.rate_hw(best_student_one, 'Python', 5)
reviewer_one.rate_hw(best_student_one, 'Python', 6)

# reviewer 3
reviewer_two = Reviewer("Jane", "Londoness")
reviewer_two.courses_attached += ['Python']
reviewer_one.rate_hw(best_student_two, 'Python', 7)
reviewer_one.rate_hw(best_student_two, 'Python', 8)
reviewer_one.rate_hw(best_student_two, 'Python', 7)

students = [best_student, best_student_one, best_student_two]
lecturers = [lecturer, lecturer_one, lecturer_two]

# print(mid_grades(students, 'Python', 'студентов'))
# print(mid_grades(lecturers, 'Python', 'лекторов'))

print(best_student_one.function(best_student_two))
print(best_student>lecturer_two)
print(best_student<lecturer_two)
print(best_student.mid_grade())
print(lecturer_two.mid_grade())

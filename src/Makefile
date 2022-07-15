FLAGS = -Wall -Wextra -Werror

all: test gcov_report

re: clean all

test: s21_decimal.a build_s21_decimal
	gcc $(FLAGS) -lcheck s21_decimal_test.c s21_decimal.a -o s21_tests
	./s21_tests

gcov_report: s21_decimal.c s21_decimal_test.c
	gcc $(FLAGS) --coverage -lcheck s21_decimal.c s21_decimal_test.c -o gcov_report
	./gcov_report
	lcov -t "./gcov_report" -o gcov_report.info --no-external -c -d .
	genhtml -o report gcov_report.info
	open ./report/index.html

s21_decimal.a: build_s21_decimal

build_s21_decimal:
	gcc $(FLAGS) -c s21_decimal.c
	ar rc s21_decimal.a s21_decimal.o
	ranlib s21_decimal.a

check:
	
	cppcheck *.c
	python3 ../materials/linters/cpplint.py --extensions=c *.c *.h
	make test

clean_obj:
	rm -rf *.o

clean_lib: 
	rm -rf *.a

clean_test:
	rm -rf *.gcda
	rm -rf *.gcno
	rm -rf *.info
	rm -rf gcov_report
	rm -rf report
	rm -rf s21_tests

clean: clean_lib clean_test clean_obj
	rm -rf s21_decimal

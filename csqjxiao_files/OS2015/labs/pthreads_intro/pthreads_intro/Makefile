# Defined constants for command base name and arguments for simple test
#
STUDENT_ID=XXXXXXX
PTC=ptcount
LOOP=1000000
INC=1

all:
	gcc -g  -o $(PTC) $(PTC).c -lpthread 

test:
	./$(PTC) $(LOOP) $(INC)

clean:
	rm -f $(PTC) 

tar:
	make clean
	mkdir $(STUDENT_ID)-pthreads_intro-lab
	cp ptcount.c Makefile $(STUDENT_ID)-pthreads_intro-lab/
	tar cvzf $(STUDENT_ID)-pthreads_intro-lab.tar.gz $(STUDENT_ID)-pthreads_intro-lab
	rm -rf $(STUDENT_ID)-pthreads_intro-lab


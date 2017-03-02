## Eclipse Makefile Project

Go to menu project -> properties, select Tool Chain Editor then select in Current Builder Gnu Make Builder.   
   
makefile script
```sh
all: hello.exe

clean:
    rm main.o hello.exe

hello.exe: main.o
    g++ -g -o hello main.o

main.o:
    g++ -c -g main.cpp
```

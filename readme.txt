FXCV is the JavaFX program
	1) Add jna reference. I've used jna-5.12.1.jar
	2) Program.java is JavaFX Application
	3) ImageCV.java is the peer class for the structure defined in Program.h of LibTessCV
	4) TessCV.java is the wrapper for the functions defined in Program.cpp of LibTessCV
	5) Change the location of your native library and tessData path in public void init() of Program.java
-----------------------------------------------

LibTessCV contains the code for c++ shared library
	1) It uses opencv and tesseract-ocr.
	2) To compile the native library you've to have libopencv4-devel and tesseract-ocr-devel installed. Those ..-devel are the names in void linux repo
-----------------------------------------------

It just converts image color and extracts text from image. Not bad, looks like the chickens are hatching well in the incubator.
===============================================

CallbackFX is JavaFX Application and LibCallback is the C shared library. Change the location of nativeLib in public void init() of CallbackFX. 

1) when you click the button of CallbackFX, C calls a Java function three times and Java calls a C function 3 times
2) void keepCallingJavaFunction(int times) of Program C calls an anonymous Java function
3) private Function sumInteger of App.java points to int sumInteger(int x, int y) function of Program.c
4) pass Java function to C using Callback interface, see CallbackWrapper.java
    interface ICallback extends Callback {
        void call(Person person);
    }
5) obtain C function pointer with Function.getFunction("nativeLibraryLocation", "functionName");

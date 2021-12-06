# SHDLab_Fortran
Quick guide for Fortran with Intel Fortran compiler and Visual Studio.
This guide is originally targeted to the graduate students, who are first to Fortran, of Surface Hydrology Lab - Korea University.
The document will explain how to build Fortran code in VS (with ifort) step-by-step. 

Previously, our lab has Intel Visual Fortran Compiler for Window lincense. In 2020, Intel launched OneAPI Base and HPC Toolkit to replace the Intel Visual Fortran Compiler. The Toolkits are free for all developers so that we can use all the Fortran features such as parallel computing assistance at no coast ([Link](https://www.intel.com/content/www/us/en/developer/articles/news/free-intel-software-developer-tools.html)).

You can compile Fortran code with Intel Fortran compiler in command-line mode. However, we prefer develope and debug code in a user-friendly environment like Matlab. Microsoft Visual Studio provide strong integrated development environment and Intel Fortran compiler can be synced with it in Windows. For free use, community version is recommended (comparing the commercial version, there is no difference in features). 

I hope following contents will be helpful for you even though you have elementary coding experiences with Fortran. 

## Contents
1. [Installation and settings](#Installation-and-Settings)
2. [Learn Fortran](#Learn-Fortran)
3. [Practice with sample codes](#Practice-with-sample-codes)
4. [Useful links](#Useful-links)

## Installation and Settings
Here, we are going to set a Fortran development environment with Microsoft Visual Studio 2019 community and Intel Fortran Compiler. Until now (Dec. 2021), the latest versions of the products working perfectly are Visual Studio Community 2019 Release 16.11 and Intel Fortran Compiler Classic and Intel Fortran Compiler(Beta) for Windows Release 2021.3.0. The latest version could not ensure the perfect work. __This section is based on VS 2019 community 16.11 and Intel Fortran Compiler 2021.3.0 .__  

Visual Studio 2019 : <https://docs.microsoft.com/ko-kr/visualstudio/releases/2019/release-notes>

Intel Fortran Compiler : <https://www.intel.com/content/www/us/en/developer/articles/tool/oneapi-standalone-components.html#fortran>

(Sometimes, downloading offilne installer was failed. Online installer is recommended.)

### Visual Studio


### Intel Fortran compiler

## Learn Fortran


## Practice with sample codes

### Edit and build in VS

### Hello world!

```
PROGRAM HelloWorld
IMPLICIT NONE

! Comment line is start with '!'
print *, 'Hello World!'

END PROGRAM HelloWorld
```

### Sort algorithm
  1. Quick sort
  2. Heap sort
  3. Quick sort

### Water head calculation
  1. Problem
  2. Source code

## Useful links

- Fortran-lang : <https://fortran-lang.org/>
- Learn Fortran in Y minutes : <https://learnxinyminutes.com/docs/fortran95/>
- Cheat sheet by B. Evans : <http://fm137.ugr.es/imnf/descargas/archivos/fortran_quick_reference_cheat_crib_sheet.pdf>
- Mistakes in Fortran 90 programs that might you surprise : <http://www.cs.rpi.edu/~szymansk/OOF90/bugs.html>
- Analysis with Fortran by KMA (in Korean) : <https://bd.kma.go.kr/kma2020/dta/edu/KBP57200_Fortran.do?menuCd=F040304000>

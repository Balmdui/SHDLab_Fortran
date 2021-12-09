# A quick guide for Fortran with Intel Fortran compiler and Visual Studio.
This guide is originally targeted to the graduate students, who are first to Fortran, of Surface Hydrology Lab - Korea University.
The document will explain how to build Fortran code in VS (with ifort) step-by-step. 

Previously, our lab has Intel Visual Fortran Compiler for Window lincense. In 2020, Intel launched OneAPI Base and HPC Toolkit to replace the Intel Visual Fortran Compiler. The Toolkits are free for all developers so that we can use all the Fortran features such as parallel computing assistance at no coast ([Link](https://www.intel.com/content/www/us/en/developer/articles/news/free-intel-software-developer-tools.html)).

You can compile Fortran code with Intel Fortran compiler in command-line mode. However, we prefer develope and debug code in a user-friendly environment like Matlab. Microsoft Visual Studio provide strong integrated development environment and Intel Fortran compiler can be synced with it in Windows. For free use, community version is recommended (comparing the commercial version, there is no difference in features). 

I hope following contents will be helpful for you even though you have elementary coding experiences with Fortran. 

## Contents
1. [Installation and settings](#Installation-and-Settings)
2. [Learin Fortran with sample codes](#Learn-Fortran-with-sample-codes)
3. [Useful links](#Useful-links)

## Installation and Settings
Here, we are going to set a Fortran development environment with Microsoft Visual Studio 2019 community and Intel Fortran Compiler. Until now (Dec. 2021), the latest versions of the products working perfectly are Visual Studio Community 2019 Release 16.11 and Intel Fortran Compiler Classic and Intel Fortran Compiler(Beta) for Windows Release 2021.3.0. The latest version could not ensure the perfect work. __This section is based on VS 2019 community 16.11 and Intel Fortran Compiler 2021.3.0 .__  

__Visual Studio 2019 download__ : <https://docs.microsoft.com/ko-kr/visualstudio/releases/2019/release-notes>
![image](https://user-images.githubusercontent.com/95595540/145339945-8bf4b9c3-afb0-4901-bd45-e5fba5b9d410.png)


__Intel Fortran Compiler download__ : <https://www.intel.com/content/www/us/en/developer/articles/tool/oneapi-standalone-components.html#fortran>

![image](https://user-images.githubusercontent.com/95595540/145339971-a1fd71f4-eab9-453c-af4b-d2a83609c579.png)

(Sometimes, downloading offilne installer was failed. Online installer is recommended.)

### Visual Studio

You should install Visual Studio before Intel Fortran compiler so that the compiler install wizard can automatically integrate with Visual Studio.
Only option you should add in the installation wizard is __Desktop development with C++"__.
If you finish VS installation without the C++ option, you can add it from the menu (도구 -> 도구 및 기능 가져오기 -> C++를 사용한 데스크톱 개발).

#### Frequently used shortcuts in VS
- Start without debugg : ctrl+F5
- Go to a subroutine or user-defined function : ctrl+click or F12
- Find all the strings : ctrl+shift+F
- Change the function of the same name : ctrl+R+R 
- multiple cursor : alt+(mouse drag)
- automatic align : ctrl+K+F
- code to comment / comment to code : ctrl+K+C / ctrl+K+U


#### Recommended Font
D2Coding : Korean & Alphabet fixed-width font. Released by Naver and free to use and re-distribute. 

After install the font, you can apply it from the VS option (도구 -> 옵션 -> 환경 -> 글꼴 및 색 -> 글꼴에서 D2Coding 선택)

download : <https://github.com/naver/d2codingfont>

![image](https://user-images.githubusercontent.com/95595540/144979269-548cf82c-94c8-46b4-8b2d-237453a63959.png)


### Intel Fortran compiler

Just launch the Intel Fortran compiler intall wizard! It will automatically integrate with VS.
If there is error during installation, quit the install wizard and launch it in repair mode once or twice agiain.
It will find omitted components and complete installation.

## Learn Fortran with sample codes

In this section, you will practice the elementary Fortran syntax.

### Edit and build in VS

1. File -> New -> New Project (ctrl+shift+N)
2. Select "Empty Project" in Fortran language
3. Write the code in the editor
4. Debug-Start without Debug (ctrl+F5)

### Hello world!

```
PROGRAM HelloWorld
IMPLICIT NONE

! Comment line is start with '!'
print *, 'Hello World!'

END PROGRAM HelloWorld
```

### Variables

There are 5 built-in varialbe types in Fortran: Integer, Real, Complex, Character, Logical

> Syntax:
> 
> <Variable_Type> :: <Variable_name>
> 
> <Variable_Type> :: <Variable_name1>, <Variable_name2>

- complex number a+bi is saved in form of (a, b)
- string is embraced by single('') or double quote ("")
- Logical expression True False : .true. .false.

```
PROGRAM variables
IMPLICIT NONE

INTEGER :: population
REAL :: pi
COMPLEX :: showmaker
CHARACTER :: monkey
LOGICAL :: aristotles

population = 11000000
pi = 3.14
showmaker = (7, 22)
monkey = 'luffy'
aristotles = .false.

END PROGRAM variables
```

### Arrays

```
PROGRAM arrays
IMPLICIT NONE

integer, dimension(10) :: array_1
integer :: array_2(10)
! array_1 and array_2 is identical as 10-elements vector
! You can declare array with either expression

! 10x10 matrix declaration
real, dimension(10, 10) :: array_3

real :: array_4(0:9)
real :: array_5(-5:5)

! customized index vectors
! array 4 : C-type index from 0 to 9
! array 5 : symmetric index from -5 to 5

END PROGRAM arrays
```

### Array and memory allocation

In Fortran, array is column-wise so that it is more efficient to move step like (1, 1) -> (2, 1).
It is inefficient to move step like (1, 1) -> (1, 2) in C or Matlab customs.

![image](https://user-images.githubusercontent.com/95595540/145341497-b348d63c-6671-4ed7-b760-bd40525e5ad2.png)


### Array slicing

Array slicing in Fortran is quite similar with the customs in Matlab. (Originally Matlab follows a lot of customs in Fortran)
You can practice array slicing following the snippet below.

```
PROGRAM array_slicing
IMPLICIT NONE

integer :: i
integer :: array_1(10)
integer :: array_2(10, 10)

array_1 = [1, 2, 3, 4, 5, 6, 7, 8, 9, 10]
array_2 = [(i, i = 1, 10)]

array_1(:) = 0

array_1(1:5) = 2
array_1(6:) = 3

! print the element of odd index (i.e., 1, 3, 5, 7, 9)
print *, array_1(1:10:2)

! print all the element inversely
print *, array_1(10:1:-1)

! print the first column in a 2-d array
print *, array_2(:,1)

END PROGRAM array_slicing

```

### Allocatable arrays

Previous array declaration was static: we already knew their length of the arrays.
If we need to declare an array without identifying its size, we use __allocatable(dynamic) array__.

It is useful for declaring an array that we don't know its size when we copy form the data size.


``` 
PROGRAM array_allocatable
IMPLICIT NONE

! allocatable vecotor
integer, allocatable :: array_1(:)

! allocatable 2-d matrix
integer, allocatable :: array_2(:, :)


! deallcoate
deallocate(array_1)
deallocate(array_2)

END PROGRAM array_allocatable
```

### Logical operation
(on working)
  
### Conditional
(on working)
  
### Loop (iterations)
(on working)
  
### File read and write
(on working)
  
### Sort algorithm
  1. Quick sort
  2. Heap sort
  3. Quick sort
(on working)
  
### Water head calculation
1. Problem
    > __Calculate iso-water head line from the given condition__
    > 
    > ![image](https://user-images.githubusercontent.com/95595540/145343096-b2557ddd-c4fa-4970-9bd9-93f0ca3d78ca.png)


    > __Expected result__
    > 
    > ![image](https://user-images.githubusercontent.com/95595540/145343178-f215e558-f0a7-406e-bddf-e1f2ccfad104.png)
 
2. Source code

```
program co_calculate
implicit none

integer :: i,j,k,count,m,n
real ::h(0:480,0:160,0:3),sum
real ::error,errmax,tol,prev,err(0:480,0:160)

open (unit=10,file="condition.txt",status="old")
open (unit=11,file="condition_t.txt",status="old")
open (unit=50,file="output.txt",status="unknown")
open (unit=51,file="output_t.txt",status="unknown")
open (unit=70,file="error.txt",status="unknown")
open (unit=71,file="error_t.txt",status="unknown")
open (unit=60,file="results.txt",status="unknown")
open (unit=61,file="results_t.txt",status="unknown")

!size of condition
m=480
n=160

!calculating none-tunnel, tunnel conditions
do k=0,1
  
!reading condition file
do j=0,n
    read(10+k,*) (h(i,j,0),i=0,480)
    do i=0,m
	h(i,j,1)=h(i,j,0)
    end do
end do
  
!setting errors
do j=0,n
  do i=0,m
    err(i,j)=0
  end do
end do
  
!setting vlaues
count=0
sum=0
tol=0.000001
error=1
errmax=error+0.1

!iteration
99 if(error>tol) then
count=count+1

do i=1,m-1    
  do j=1,n-1
    
!Calcultating hydrauric head
	if(int(h(i,j,0)).NE.0) then
!X-axis      
		if (int(h(i-1,j,0)*h(i+1,j,0)).ne.0) then
  			sum=h(i-1,j,1)+h(i+1,j,1)
		else if (int(h(i-1,j,0)).ne.0.and.int(h(i+1,j,0))==0) then
  			sum=2*h(i-1,j,1)
		else if (int(h(i+1,j,0)).ne.0.and.int(h(i-1,j,0))==0) then
  			sum=2*h(i+1,j,1)
		else if (int(h(i-1,j,0))==0 .and. int(h(i+1,j,0))==0) then
  			sum=0
		end if
!Y-axis
		if (int(h(i,j-1,0)*h(i,j+1,0)).ne.0) then
  			if(j.ne.40) then
    			sum=sum+h(i,j-1,1)+h(i,j+1,1)
  			else if(j==40) then
   				sum=sum+1.714286*h(i,j-1,1)+0.285714*h(i,j+1,1)
			end if
		else if (int(h(i,j-1,0)).ne.0.and.int(h(i,j+1,0))==0) then
  			sum=sum+2*h(i,j-1,1)
		else if (int(h(i,j+1,0)).ne.0.and.int(h(i,j-1,0))==0) then
  			sum=sum+2*h(i,j+1,1)
		else if (int(h(i-1,j,0))==0.and.int(h(i+1,j,0))==0) then
  			sum=sum+0
		end if

	prev=h(i,j,1)
	h(i,j,1)=sum/4	
	end if 

  		error=abs(h(i,j,1)-prev)
    if(int(h(i,j,0))==0) then
      	error=0
    end if
		err(i,j)=error    

	if(error>errmax) then
    errmax=error
    end if

    error=errmax    

	end do
end do

    print *,"count :", count
    print *,"err   :", errmax
    print *,"head  :", h(210,80,1)

    errmax=0

goto 99
end if

	do j=0,n
    	write (50+k,77) (h(i,j,1),i=0,m)
    	write (70+k,77) (err(i,j),i=0,m)
	end do

write (60+k,*) "# of iteration : ",count,", max error : ",errmax,", head of A : ",h(210,80,1)
end do

77 format(f4.1,1x,480(f6.3,1x))

end program
```
## Useful links

- Fortran-lang : <https://fortran-lang.org/>
- Learn Fortran in Y minutes : <https://learnxinyminutes.com/docs/fortran95/>
- Cheat sheet by B. Evans : <http://fm137.ugr.es/imnf/descargas/archivos/fortran_quick_reference_cheat_crib_sheet.pdf>
- Mistakes in Fortran 90 programs that might you surprise : <http://www.cs.rpi.edu/~szymansk/OOF90/bugs.html>
- Analysis with Fortran by KMA (in Korean) : <https://bd.kma.go.kr/kma2020/dta/edu/KBP57200_Fortran.do?menuCd=F040304000>

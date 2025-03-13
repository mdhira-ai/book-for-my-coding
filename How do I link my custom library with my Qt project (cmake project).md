# **`How do I link my custom library with my Qt project (cmake project)`**

**First way :**

1) create a cmake project in Qt creator.

![][image1]

2) Create a cmake custom lib in Qt creator.

3) Make a function and declare into .h file in custom lib.  
   

![][image2]

4) Build the lib and check Release folder there is “.so” file. Copy that “.so” file and make a lib folder in your main project and paste it.

5) Add “ link\_directories(${CMAKE\_SOURCE\_DIR}/lib) “ into main project cmake file.  
6) And add lib header file/folder path ”include\_directories("/home/kali/Desktop/gui c/myqtlib/")  
7) Add target\_link\_libraries(projectname PRIVATE myqtlib)

![][image3]

8) Import your custom lib .h file in main.cpp in your main project and run it.

![][image4]

**Second way :** 

1) Create project using cmake in Qt creator.

![][image5]

2) Add new c++ header/source file.(two files).

![][image6]

3) Put your custom lib name. It like lib main.cpp.

![][image7]

4) Put the header file (.h) name.

![][image8]

5) Declare function in .h file of your custom header.

![][image9]

6) Make the function in your lib .cpp file (source file).

![][image10]

7) Import into main project main.cpp file. And build it.

![][image11]

# 

# 

# 

# 

# 

# To install lib with vcpkg and integrate with Qt creator

\#\#\# 1\. \*\*Ensure \`vcpkg\` is Set Up Correctly\*\*  
Make sure \`vcpkg\` is installed and the \`fmt\` library is installed using:  
\`\`\`bash  
vcpkg install fmt  
\`\`\`

\#\#\# 2\. \*\*Configure CMake in Qt Creator to Use \`vcpkg\`\*\*  
You need to tell CMake where to find the \`vcpkg\` toolchain file. This file is typically located in the root of your \`vcpkg\` installation directory and is named \`vcpkg.cmake\`.

\- Open your Qt Creator project.  
\- Go to the \*\*Projects\*\* mode (left sidebar).  
\- Under \*\*Build & Run\*\*, select your kit (e.g., Desktop Qt).  
\- Scroll down to the \*\*CMake Configuration\*\* section.  
\- Add the following line to the \*\*Initial Configuration\*\* or \*\*CMake Arguments\*\*:  
  \`\`\`cmake  
  **\-DCMAKE\_TOOLCHAIN\_FILE=\<path-to-vcpkg\>/scripts/buildsystems/vcpkg.cmake**  
  \`\`\`  
  Replace \`\<path-to-vcpkg\>\` with the full path to your \`vcpkg\` installation directory.

\---

\#\#\# 3\. \*\*Update Your \`CMakeLists.txt\`\*\*  
In your \`CMakeLists.txt\` file, add the following to find and link the \`fmt\` library:

\`\`\`cmake  
cmake\_minimum\_required(VERSION 3.14)  
project(MyProject)

\# Find the fmt library  
find\_package(fmt REQUIRED)

\# Add your executable or library  
add\_executable(MyApp main.cpp)

\# Link the fmt library to your target  
target\_link\_libraries(MyApp PRIVATE fmt::fmt)  
\`\`\`

\#\#\# 4\. \*\*Include \`fmt\` in Your Code\*\*  
In your source files (e.g., \`main.cpp\`), include the \`fmt\` header and use it:

\`\`\`cpp  
\#include \<fmt/core.h\>

int main() {  
    fmt::print("Hello, {}\!\\n", "world");  
    return 0;  
}  
\`\`\`

\---

\#\#\# 5\. \*\*Build and Run\*\*  
\- Save all changes.  
\- Build your project in Qt Creator.  
\- Run the application to verify that \`fmt\` is working correctly.

\---

\#\#\# Troubleshooting  
\- If CMake cannot find \`fmt\`, double-check that the \`vcpkg\` toolchain file path is correct.  
\- Ensure that the \`vcpkg\` triplet (e.g., \`x64-windows\`, \`x86-windows\`) matches your Qt Creator kit.  
\- If you encounter linker errors, ensure that \`fmt\` is installed for the correct architecture (e.g., 32-bit vs 64-bit).

![Image 1](data:image/png;base64,iVBORw0KGgoAAAANSUhEUgAAAnAAAAFTCAIAAAA2oabxAABsX0lEQVR4XuzdCVQb2Z0/+nnzP+edeXPenPOfzMx/zv/NZOmkt0y6pZIAsWMBEtgG2yzeV8DGNnhf8M7ijcWYfZexjcFgwGxm3zcBArSU3G2Ynkym05[...])
![Image 2](data:image/png;base64,iVBORw0KGgoAAAANSUhEUgAAAnIAAAFkCAIAAAArK0HZAACAAElEQVR4Xuy9eVQb2YHw+/31zjvvnDnnTb45Z76vk+50Z+ss3Uhi3xFa2G2zGANmB9ts3vGGbTAYg9kROwjbYMy+7/sqEBJIqiq7G09mkpdOJpPM9O[...])
![Image 3](data:image/png;base64,iVBORw0KGgoAAAANSUhEUgAAAnAAAAExCAIAAABznQigAACAAElEQVR4Xuy9iV8byZ3wvf/Afj7Pk919nk32TSaTTTa7mYzUkhD3oZP7kA0YbIxt8IFtwPeJweYy5jD3jY0N5jIYY+4bSQiEACF1e2w5u5Nsks01mZ[...])
![Image 4](data:image/png;base64,iVBORw0KGgoAAAANSUhEUgAAAY4AAAEeCAIAAAASAGVoAABedklEQVR4XuydCXwT1534Id1mu91su0277abbXN22SZMgjSTfp3zfxvjANgaDL8D3fVuSbXxwGYxtwJjLgLkxN/jC921ZR0Jg02u33bb/bbtpk90em5[...])
![Image 5](data:image/png;base64,iVBORw0KGgoAAAANSUhEUgAAAnAAAAFHCAIAAACu5uZ8AACAAElEQVR4Xuy9d3Qb152wvef7f8/53n13v/fd7MYlWZckNhp7R2cXOymJRexVlERRVKdEihR776TYey8SSbH3AhJlRpaoONWx1846Tjax17HjGn13Zg[...])
![Image 6](data:image/png;base64,iVBORw0KGgoAAAANSUhEUgAAAnAAAAFXCAIAAACtMOTnAAB4xElEQVR4Xuy9eVQb2Z3oP+f3x++88ztnznuTZN68dMbdnaQ73Z10awHEvgghAQa8sIPNvtiAwTu28Y7ZDGbfDcZg9n23zQ5CIIG2KsdtdybpdM+bTH[...])
![Image 7](data:image/png;base64,iVBORw0KGgoAAAANSUhEUgAAAjgAAAF2CAIAAADSrXUgAAA+CElEQVR4Xu3deVcTe+Ln8X4GM79e5nb3TC+/7ut1zwIBRBREVFCRNRB2FQEBAXEHlUUREGRRUEREQERkF1DZ9y1krTrz1yz/zHLmzJlz5sxjmG9VJa[...])
![Image 8](data:image/png;base64,iVBORw0KGgoAAAANSUhEUgAAAjEAAAFyCAIAAACLKRz8AAA78ElEQVR4Xu3diV/T+KL38ecfuM89Z+45d845996zjjOOM9OWXVQQFcUNBLqyKggKCu4bCKIiKFAWQRER2dzYZVH2HUrpluQPeV73b3h+SdoSmoIoKD[...])
![Image 9](data:image/png;base64,iVBORw0KGgoAAAANSUhEUgAAAnAAAAFlCAIAAADkgkJBAACAAElEQVR4Xuy9d3Ab2Z2o63p/vHr1qrbqvvXu23vt9QSv99njmSEARpGiKCIxk2LOOQeJilQmRTEnMQcQJEWKOeccEUgEAuhuzUi64zu+6x2P7ZmxvQ[...])
![Image 10](data:image/png;base64,iVBORw0KGgoAAAANSUhEUgAAAnAAAAFdCAIAAAAMq8eBAAB4M0lEQVR4Xuy9eVQb2Z3423+98847Z855v2RmMsmkl2SSdHpDQuxm04IAs9hgFmMDNqsNeMH7jm3Axuz7vu/7voOQQBJCAklV6na705N1kky2ybwsk[...])
![Image 11](data:image/png;base64,iVBORw0KGgoAAAANSUhEUgAAAnAAAAGVCAIAAADxEFtYAACAAElEQVR4Xuy9eVQbR76wPef74zvv+c6557x33vPee2dNJplksoIk9l0rO5jVYBswuwHbYBtvgMEYMLtZBWa12ffdgFkFEptAS7djk8mdm2WSmUziS[...])

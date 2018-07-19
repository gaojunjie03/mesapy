------------------------------------
How to Build/Execute the Sample Code
------------------------------------
1. Install Intel(R) SGX SDK for Linux* OS.
2. Install pypy and libffi for your machine.
3. Download pypy package provided by us.
4. Build project as the detail instruction we provide in the following:
	1) Build libpypy-c.a by using the pypy source code we provide. 
		a. Go into pypy/pypy/goal directory
                b. Run command "../../rpython/bin/rpython --opt=2 targetstandaloned.py --no-allworkingmodules"
                   The libpypy-c.a will be generated and put in tmp directory showing in the terminal or you can set path for it.

        2) Build Python functions' C interfaces using CFFI.
		a. The example code is under /Enclave/pypy_embedding, there are files, implementation.py, embed.py, api.h
		   Wirte python function you want to run in implementation.py.
		b. create a CFFI interface for it, define the C interface function definition for it.
		c. run pypy ./embed.py for generating the corresponed object file.

        3) Write ecall in SGX which could call the Python function.

	4) Link libpypy-c.a, the object generated at step 2) in enclave.so.

	5) Generate sgx binary.

NOTICE: While running pypy embed.py, make sure the typedefine.h and include directory are in the same directory as the command running, and import the cffi module from the lib_pypy we provide.


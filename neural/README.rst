Theano - Windows 10 installation notes
======================================

0) install CUDA 7.5 
1) install microsoft visual studio 2013 with no extras
2) install windows 10 SDK (for include and lib files)
3) use the custom nvcc.profile and .theano files in this directory (critical!)
4) pip install mingw libpython numpy
5) download pycuda from http://www.lfd.uci.edu/~gohlke/pythonlibs/#pycuda
pip install ~/Downloads/"pycuda-2016.1.2+cuda7518-cp35-cp35m-win_amd64.whl"

4) make temp directory (not sure this step is needed):
copy python35.dll and do the following
> gendef python35.dll
> dlltool --as-flags=--64 -m i386:x86-64 -k --output-lib libpython35.a --input-def python35.def
copy libpython35 and python35 to Anaconda/libs

5) run python -m theanotest
this will build the cuda code and then run theanotest
and then check pycuda with :
> python -m pycudatest

6) at python REPL import theano. Should get: 
Using gpu device 0: GeForce GTX 970 (CNMeM is enabled with initial size: 75.0% of memory, cuDNN not available)



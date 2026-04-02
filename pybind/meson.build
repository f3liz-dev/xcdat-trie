pymod = import('python')
py_installation = pymod.find_installation('python3', required : false)

if py_installation.found()
  py_dep = py_installation.dependency(embed : true)
  pybind11_dep = dependency('pybind11', required : false)
  
  if pybind11_dep.found()
    pyext_module = pymod.extension_module('xcdat',
      'xcdat_pybind.cpp',
      include_directories : incdir,
      dependencies : [py_dep, pybind11_dep],
      install : true)
    
    message('Python bindings will be built')
  else
    warning('pybind11 not found: Python bindings will not be built')
  endif
else
  warning('Python3 not found: Python bindings will not be built')
endif

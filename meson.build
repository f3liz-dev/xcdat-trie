project('xcdat', 'cpp',
  version : '0.2.0',
  default_options : [
    'cpp_std=c++17',
    'buildtype=release',
    'warning_level=3',
  ])

# Compiler identification and C++17 check
cc = meson.get_compiler('cpp')

if cc.get_id() == 'gcc'
  if cc.version().version_compare('< 7.0')
    error('GCC 7.0 or greater is required for C++17 support')
  endif
elif cc.get_id() in ['clang', 'clang-cl']
  if cc.version().version_compare('< 4.0')
    error('Clang 4.0 or greater is required for C++17 support')
  endif
endif

message('Compiler: @0@ @1@'.format(cc.get_id(), cc.version()))

# Set up compiler flags
common_flags = ['-pthread']
release_flags = ['-DNDEBUG']
debug_flags = ['-fno-omit-frame-pointer', '-g', '-DDEBUG']

# Add platform-specific flags for macOS
if host_machine.system() == 'darwin'
  common_flags += ['-stdlib=libc++']
endif

# Apply flags based on build type
if get_option('buildtype') == 'release'
  add_project_arguments(common_flags + release_flags, language : 'cpp')
else
  add_project_arguments(common_flags + debug_flags, language : 'cpp')
endif

# Include directories
incdir = include_directories('include')

# Subdirectories
subdir('sample')
subdir('tools')
subdir('tests')
subdir('pybind')

# Install headers
install_headers('include/xcdat.hpp')
install_headers(
  'include/xcdat/bc_vector_15.hpp',
  'include/xcdat/bc_vector_16.hpp',
  'include/xcdat/bc_vector_7.hpp',
  'include/xcdat/bc_vector_8.hpp',
  'include/xcdat/bit_tools.hpp',
  'include/xcdat/bit_vector.hpp',
  'include/xcdat/code_table.hpp',
  'include/xcdat/compact_vector.hpp',
  'include/xcdat/exception.hpp',
  'include/xcdat/immutable_vector.hpp',
  'include/xcdat/load_visitor.hpp',
  'include/xcdat/mmap_visitor.hpp',
  'include/xcdat/save_visitor.hpp',
  'include/xcdat/size_visitor.hpp',
  'include/xcdat/tail_vector.hpp',
  'include/xcdat/trie_builder.hpp',
  'include/xcdat/trie.hpp',
  subdir : 'xcdat'
)

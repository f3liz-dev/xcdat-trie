# Copy test data file to build directory
run_command('cp', join_paths(meson.current_source_dir(), 'keys.txt'),
  meson.current_build_dir(), check : false)

# Define the test configurations
test_sources = {
  'test_bit_vector': 'test_bit_vector.cpp',
  'test_compact_vector': 'test_compact_vector.cpp',
  'test_tail_vector': 'test_tail_vector.cpp',
}

# Add the base tests
foreach test_name, test_src : test_sources
  exe = executable(test_name, test_src, include_directories : incdir)
  test(test_name, exe)
endforeach

# BC Vector tests with compile-time definitions
bc_options = ['7', '8', '15', '16']

foreach bc_option : bc_options
  test_name = 'test_bc_vector_@0@'.format(bc_option)
  exe = executable(test_name,
    'test_bc_vector.cpp',
    include_directories : incdir,
    cpp_args : ['-DBC_VECTOR_@0@'.format(bc_option)])
  test(test_name, exe)
endforeach

# Trie tests with compile-time definitions
foreach bc_option : bc_options
  test_name = 'test_trie_@0@'.format(bc_option)
  exe = executable(test_name,
    'test_trie.cpp',
    include_directories : incdir,
    cpp_args : ['-DTRIE_@0@'.format(bc_option)])
    
  # 2. Force the test to run in the source folder where keys.txt lives!
  test(test_name, exe, 
    args: ['--no-breaks'],
    workdir: meson.current_source_dir() 
  )
endforeach
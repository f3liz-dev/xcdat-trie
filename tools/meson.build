xcdat_tools = [
  'xcdat_build',
  'xcdat_lookup',
  'xcdat_decode',
  'xcdat_prefix_search',
  'xcdat_predictive_search',
  'xcdat_enumerate',
  'xcdat_benchmark',
]

foreach tool : xcdat_tools
  executable(tool,
    tool + '.cpp',
    include_directories : incdir,
    cpp_args : ['-Wno-pedantic'],
    install : true,
    install_dir : get_option('bindir'))
endforeach

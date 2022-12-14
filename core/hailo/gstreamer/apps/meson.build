apps_install_dir = get_option('apps_install_dir')
target_platform = get_option('target_platform')
if apps_install_dir == ''
  # By default install for x86 workspace
  apps_install_dir = tappas_workspace + '/apps/gstreamer/libs/apps/'
endif

thread_deps = [dependency('threads')]

################################################
# CV Singleton
################################################
cv_singleton_src = '../../general/hailo_cv_singleton.cpp'

cv_singleton_lib = shared_library('hailo_cv_singleton',
  cv_singleton_src,
  cpp_args : hailo_lib_args,
  include_directories: [hailo_general_inc],
  dependencies : [opencv_dep],
  gnu_symbol_visibility : 'default',
  version: meson.project_version(),
  install: true,
  install_dir: get_option('libdir'),
)

cv_singleton_dep = declare_dependency(
  include_directories: [include_directories('../../general')],
  link_with : cv_singleton_lib)

################################################
# GST Image Handling
################################################
image_src = '../plugins/common/image.cpp'

image_lib = shared_library('hailo_gst_image',
  image_src,
  cpp_args : hailo_lib_args,
  include_directories: [hailo_general_inc, include_directories('../plugins')],
  dependencies : plugin_deps + [opencv_dep],
  gnu_symbol_visibility : 'default',
  version: meson.project_version(),
  install: true,
  install_dir: get_option('libdir'),
)

image_dep = declare_dependency(
  include_directories: [include_directories('../plugins/common')],
  link_with : image_lib)

# App Subdirectories
if target_platform == 'x86'
    subdir('x86')
elif target_platform == 'imx'
    subdir('imx')
endif

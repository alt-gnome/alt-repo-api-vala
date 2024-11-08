project(
  'libalt-repo',
  ['c', 'vala'],
  version: '0.1.0',
  meson_version: '>= 1.0.0',
  license: 'GPL-3.0-or-later',
)

api_version = '0.1'
glib_min_version = '2.76'

project_name = meson.project_name()
gir_name = 'AltRepo'

versioned_name = meson.project_name() + '-' + api_version
versioned_gir_name = gir_name + '-' + api_version

libalt_repo_deps = versioned_name + '.deps'
libalt_repo_header = project_name + '.h'
libalt_repo_vapi = versioned_name + '.vapi'
libalt_repo_gir = versioned_gir_name + '.gir'
libalt_repo_typelib = versioned_gir_name + '.typelib'

pkgconfig = import('pkgconfig')
gnome = import('gnome')

deps_pkgs = [
  'libapi-base-0.1',
  'gee-0.8',
  'gio-2.0',
]

libalt_repo_dependencies = []

foreach deps_pkg : deps_pkgs 
  libalt_repo_dependencies += dependency(deps_pkg)
endforeach

gee = dependency('gee-0.8')
gee_girdir = gee.get_variable('datadir') / 'gir-1.0'
gee_vapidir = gee.get_variable('datadir') / 'vala' / 'vapi'

add_project_arguments(
  # GCC14 COMPILE ERROR
  '-Wno-int-conversion',
  language: ['c'],
)

add_project_arguments(
  '--abi-stability',
  '--hide-internal',
  '--target-glib', glib_min_version,
  '--vapidir', meson.current_source_dir(),
  language: ['vala'],
)

subdir('lib')
subdir('tests')

if get_option('documentation')
  subdir('doc')
endif

gnome.post_install()

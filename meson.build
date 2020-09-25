project(
  'gnome-session-ctl', 'c',
  version: '3.38.0', # same as gnome-session
  license: 'GPL2+',
  default_options: 'buildtype=debugoptimized',
  meson_version: '>= 0.53.0'
)

version = meson.project_version()
version_array = version.split('.')
major_version = version_array[0].to_int()
api_version = '@0@.0'.format(major_version)
api_name = '@0@-@1@'.format(meson.project_name(), api_version)

prefix = get_option('prefix')
localedir = prefix / get_option('localedir')
libexecdir = prefix / get_option('libexecdir')

glib_req_version = '>= 2.46.0'

gio_dep = dependency('gio-2.0', version: glib_req_version)
glib_dep = dependency('glib-2.0', version: glib_req_version)
libsystemd_dep = dependency('libsystemd', version: '>= 209', required: false)

deps = [
  gio_dep,
  glib_dep,
  libsystemd_dep,
]

cflags = ['-DLOCALE_DIR="@0@"'.format(localedir)]

config_h = configuration_data()

# defines
set_defines = [
  # package
  ['PACKAGE', meson.project_name()],
  ['PACKAGE_VERSION', version],
  ['VERSION', version],
  # i18n
  ['GETTEXT_PACKAGE', api_name]
]

foreach define: set_defines
  config_h.set_quoted(define[0], define[1])
endforeach

configure_file(
  output: 'config.h',
  configuration: config_h
)

executable(
  'gnome-session-ctl',
  'gnome-session-ctl.c',
  include_directories: include_directories('.'),
  dependencies: deps,
  c_args: cflags,
  install: true,
  install_dir: libexecdir,
)
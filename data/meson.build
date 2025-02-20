icons_dir = join_paths(get_option('datadir'), 'icons', 'hicolor')
scalable_dir = join_paths(icons_dir, 'scalable', 'apps')
symbolic_dir = join_paths(icons_dir, 'symbolic', 'apps')

install_data(
    join_paths('icons', 'color.svg'),
    install_dir: scalable_dir,
    rename: meson.project_name() + '.svg',
)
install_data(
    join_paths('icons', 'symbolic.svg'),
    install_dir: symbolic_dir,
    rename: meson.project_name() + '-symbolic.svg',
)

install_data(
    meson.project_name() + '.gschema.xml',
    install_dir: join_paths(
        get_option('prefix'),
        get_option('datadir'),
        'glib-2.0',
        'schemas',
    ),
)

desktop_file = i18n.merge_file(
    input: meson.project_name() + '.desktop.in',
    output: meson.project_name() + '.desktop',
    po_dir: join_paths(meson.project_source_root(), 'po'),
    type: 'desktop',
    install: true,
    install_dir: join_paths(get_option('datadir'), 'applications'),
)

desktop_utils = find_program('desktop-file-validate', required: false)
if desktop_utils.found()
    test('Validate desktop file', desktop_utils, args: [desktop_file])
endif

appstream_file = i18n.merge_file(
    input: meson.project_name() + '.appdata.xml.in',
    output: meson.project_name() + '.appdata.xml',
    po_dir: join_paths(meson.project_source_root(), 'po'),
    install: true,
    install_dir: join_paths(get_option('datadir'), 'metainfo'),
)

appstream_util = find_program('appstream-util', required: false)
if appstream_util.found()
    test(
        'Validate appstream file',
        appstream_util,
        args: ['validate', appstream_file],
    )
endif

#
# SPDX-FileCopyrightText: 2020 George Florea Bănuș <georgefb899@gmail.com>
#
# SPDX-License-Identifier: GPL-3.0-or-later
#

qt5_add_dbus_interface(haruna_screensaver_inhibit_SRCS ../org.freedesktop.ScreenSaver.xml screensaverdbusinterface)
add_executable(haruna
    application.cpp
    player.cpp
    haction.cpp
    lockmanager.cpp
    main.cpp
    mpvobject.cpp
    qthelper.h
    playlist/playlistitem.cpp
    playlist/playlistmodel.cpp
    Settings/audiosettings.cpp
    Settings/generalsettings.cpp
    Settings/mousesettings.cpp
    Settings/playbacksettings.cpp
    Settings/playlistsettings.cpp
    Settings/settings.cpp
    Settings/subtitlessettings.cpp
    Settings/videosettings.cpp
    subtitlesfoldersmodel.cpp
    track.cpp
    tracksmodel.cpp
    worker.cpp
    qml.qrc
    ../help/help.qrc
    ${haruna_screensaver_inhibit_SRCS})
target_compile_definitions(haruna PRIVATE $<$<OR:$<CONFIG:Debug>,$<CONFIG:RelWithDebInfo>>:QT_QML_DEBUG>)
target_link_libraries(haruna PRIVATE
    Qt5::Core
    Qt5::Quick
    Qt5::QuickControls2
    Qt5::DBus
    KF5::ConfigGui
    KF5::CoreAddons
    KF5::FileMetaData
    KF5::I18n
    KF5::XmlGui
    KF5::WindowSystem
    mpv
)

install(TARGETS haruna DESTINATION ${KDE_INSTALL_TARGETS_DEFAULT_ARGS})
install(FILES org.kde.haruna.qtdbus.playvideo.service DESTINATION /usr/share/dbus-1/services/)
 
feature_summary(WHAT ALL FATAL_ON_MISSING_REQUIRED_PACKAGES)

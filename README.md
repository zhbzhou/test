Thread 1 "cobalt_launcher" hit Breakpoint 1, 0xb60e50ba in g_variant_new () from /lib/libglib-2.0.so.0
(gdb) bt
#0  0xb60e50ba in g_variant_new () from /lib/libglib-2.0.so.0
#1  0xb5958c7e in ?? () from /lib/libbuxton2.so.1
#2  0xb5953396 in ?? () from /lib/libbuxton2.so.1
#3  0xb59537a4 in ?? () from /lib/libbuxton2.so.1
#4  0xb5956062 in buxton_register_notification_sync () from /lib/libbuxton2.so.1
#5  0xb6f1538c in ?? () from /lib/libvconf.so.0
#6  0x004db31c in starboard::tizen::product::ApplicationTizen::CreateWindow(SbWindowOptions const*) ()
#7  0xaf106628 in ?? ()
Backtrace stopped: previous frame identical to this frame (corrupt stack?)
(gdb) c
Continuing.

Thread 1 "cobalt_launcher" hit Breakpoint 1, 0xb60e50ba in g_variant_new () from /lib/libglib-2.0.so.0
(gdb) bt
#0  0xb60e50ba in g_variant_new () from /lib/libglib-2.0.so.0
#1  0xb5958c92 in ?? () from /lib/libbuxton2.so.1
#2  0xb5953396 in ?? () from /lib/libbuxton2.so.1
#3  0xb59537a4 in ?? () from /lib/libbuxton2.so.1
#4  0xb5956062 in buxton_register_notification_sync () from /lib/libbuxton2.so.1
#5  0xb6f1538c in ?? () from /lib/libvconf.so.0
#6  0x004db31c in starboard::tizen::product::ApplicationTizen::CreateWindow(SbWindowOptions const*) ()
#7  0xaf106628 in ?? ()
Backtrace stopped: previous frame identical to this frame (corrupt stack?)
(gdb) c
Continuing.
[New LWP 23918]

Thread 1 "cobalt_launcher" hit Breakpoint 1, 0xb60e50ba in g_variant_new () from /lib/libglib-2.0.so.0
(gdb) bt
#0  0xb60e50ba in g_variant_new () from /lib/libglib-2.0.so.0
#1  0xb5958c7e in ?? () from /lib/libbuxton2.so.1
#2  0xb5953396 in ?? () from /lib/libbuxton2.so.1
#3  0xb59537a4 in ?? () from /lib/libbuxton2.so.1
#4  0xb5956062 in buxton_register_notification_sync () from /lib/libbuxton2.so.1
#5  0xb6f1538c in ?? () from /lib/libvconf.so.0
#6  0x004db33c in starboard::tizen::product::ApplicationTizen::CreateWindow(SbWindowOptions const*) ()
#7  0xaf106628 in ?? ()
Backtrace stopped: previous frame identical to this frame (corrupt stack?)
(gdb) c
Continuing.

Thread 1 "cobalt_launcher" hit Breakpoint 1, 0xb60e50ba in g_variant_new () from /lib/libglib-2.0.so.0
(gdb) c
Continuing.

Thread 1 "cobalt_launcher" hit Breakpoint 1, 0xb60e50ba in g_variant_new () from /lib/libglib-2.0.so.0
(gdb) c
Continuing.

(process:23593): GLib-CRITICAL **: 10:18:41.684: '(iislu)' is not a valid GVariant format string

(process:23593): GLib-CRITICAL **: 10:18:41.685: g_variant_new: assertion 'valid_format_string (format_string, TRUE, NULL) && format_string[0] != '?' && format_string[0] != '@' && format_string[0] != '*' && format_string[0] != 'r'' failed
[New LWP 23948]
[New LWP 23949]
[Switching to LWP 23619]

Thread 12 "Updater" hit Breakpoint 1, 0xb60e50ba in g_variant_new () from /lib/libglib-2.0.so.0
(gdb) bt
#0  0xb60e50ba in g_variant_new () from /lib/libglib-2.0.so.0
#1  0xb5958c7e in ?? () from /lib/libbuxton2.so.1
#2  0xb5953396 in ?? () from /lib/libbuxton2.so.1
#3  0xb5953544 in ?? () from /lib/libbuxton2.so.1
#4  0xb5955acc in buxton_set_value_sync () from /lib/libbuxton2.so.1
#5  0xb6f1574a in ?? () from /lib/libvconf.so.0
#6  0xb6f1678c in vconf_set_str () from /lib/libvconf.so.0
#7  0x004c2008 in SetVconfInfoStr(char const*, std::__cxx11::basic_string<char, std::char_traits<char>, std::allocator<char> >) ()
#8  0x004f2618 in starboard::tizen::evergreen::cobaltUpdateFailedHandler(char const*) ()
#9  0x004ef5b8 in starboard::tizen::evergreen::UpdaterState(CobaltExtensionUpdaterNotificationState, char const*) ()
#10 0xaf1ea5dc in ?? ()
Backtrace stopped: previous frame identical to this frame (corrupt stack?)
(gdb) c
Continuing.
[New LWP 24061]

Thread 12 "Updater" hit Breakpoint 1, 0xb60e50ba in g_variant_new () from /lib/libglib-2.0.so.0
(gdb) bt
#0  0xb60e50ba in g_variant_new () from /lib/libglib-2.0.so.0
#1  0xb5958c92 in ?? () from /lib/libbuxton2.so.1
#2  0xb5953396 in ?? () from /lib/libbuxton2.so.1
#3  0xb5953544 in ?? () from /lib/libbuxton2.so.1
#4  0xb5955acc in buxton_set_value_sync () from /lib/libbuxton2.so.1
#5  0xb6f1574a in ?? () from /lib/libvconf.so.0
#6  0xb6f1678c in vconf_set_str () from /lib/libvconf.so.0
#7  0x004c2008 in SetVconfInfoStr(char const*, std::__cxx11::basic_string<char, std::char_traits<char>, std::allocator<char> >) ()
#8  0x004f2618 in starboard::tizen::evergreen::cobaltUpdateFailedHandler(char const*) ()
#9  0x004ef5b8 in starboard::tizen::evergreen::UpdaterState(CobaltExtensionUpdaterNotificationState, char const*) ()
#10 0xaf1ea5dc in ?? ()
Backtrace stopped: previous frame identical to this frame (corrupt stack?)
(gdb) c
Continuing.
[Switching to LWP 23593]

Thread 1 "cobalt_launcher" hit Breakpoint 1, 0xb60e50ba in g_variant_new () from /lib/libglib-2.0.so.0
(gdb) bt
#0  0xb60e50ba in g_variant_new () from /lib/libglib-2.0.so.0
#1  0xb5a9b088 in ?? () from /lib/libgio-2.0.so.0
#2  0xb5a9fe60 in g_dbus_connection_signal_subscribe () from /lib/libgio-2.0.so.0
#3  0xb35e67e8 in ?? () from /lib/libnetwork.so.0
#4  0xb35ebb10 in ?? () from /lib/libnetwork.so.0
#5  0xb35deb82 in net_register_client () from /lib/libnetwork.so.0
#6  0xb6cbdcac in ?? () from /lib/libcapi-network-connection.so.1
#7  0xb6cb456c in connection_create () from /lib/libcapi-network-connection.so.1
#8  0x004db42c in starboard::tizen::product::ApplicationTizen::CreateWindow(SbWindowOptions const*) ()
#9  0xaf106628 in ?? ()
Backtrace stopped: previous frame identical to this frame (corrupt stack?)

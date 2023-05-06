# pyportal-openwrt
Show OpenWrt Stats on PyPortal (SAMD51 M4)

## Enable ubus access on OpenWrt

Allow ubus access over uhttpd.

```shell
# opkg update
# opkg install rpcd-mod-file uhttpd-mod-ubus
```

And create on your OpenWrt device a read-only user to be used by setting up the ACL file `/usr/share/rpcd/acl.d/user.json`.

```json
{
  "user": {
    "description": "Read only user access role",
    "read": {
      "ubus": {
        "*": [ "*" ]
      },
      "uci": [ "*" ]
    },
    "write": {}
  }
}
```

Restart the services. This ACL file needs to be recreated after updating/upgrading your OpenWrt firmware.

```shell
# service rpcd restart && service uhttpd restart
```

Check if the file namespaces is registered with the RPC server.

```
# ubus list | grep file
file
```

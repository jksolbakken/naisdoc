# device command

!!! info "MVP"
    The `device` command is very fresh, and only has a small subset of functions compared to [naisdevice](../../../device).

The device command can be used to connect to, disconnect from, and view the connection status of [naisdevice](../../../device).
Currently, the command requires the processes `naisdevice-agent` and `naisdevice-helper` to run, both of which can be run by starting naisdevice.

## connect

Requests a connection and waits for success.
The expected result is "Connected".

```bash
nais device connect
```

## disconnect

Requests a disconnection and waits for success.
The expected result is "Disconnected".

```bash
nais device disconnect
```

## status

Prints the current connection status of `naisdevice-agent`. 
This includes connection status, as well as gateways and their current statuses.


```bash
nais device status
```

| Flag     | Required | Short |Default |Description                            |
|----------|----------|--- ---|--------|---------------------------------------|
| quiet    | No       | -q    | false  | Only print connection status.         |
| output   | No       | -o    | ''     | Specify output format. (yaml|json)    |


!!! note "output format"
    If the output format and quiet flags are specified, output takes precedence.

## jita

Starts the *just-in-time access* flow for a named gateway.
This should redirect you to a browser to submit a request for just-in-time access.

```bash
nais device jita my-privileged-access-gateway
```

| Argument | Required |Description                                        |
|----------|----------|---------------------------------------------------|
| gateway  | Yes      | The desired gateway to establish a connection to. |

!!! tip "Which gateways require just-in-time access?"
    You can view gateways and their JITA requirement with `nais device status`.

    This snippet explicitly shows the names of gateways with that requirement.
    ```bash
    nais device status -ojson | jq -r '.Gateways[] | select(.requiresPrivilegedAccess == true) | .name'
    ```
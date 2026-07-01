# otp.RemoteTS

### ``class RemoteTS(host, port=None, protocol=None, resource=None, cep=False)``

Bases: ``object``

Class representing remote tick-server.
Can be ``used``
in ``Session`` as well as the local databases.

* **Parameters:**
  * **host** (str, ``LoadBalancing``, ``FaultTolerance``) – 

    In case of string: string with this format: `[proto://]hostname:port[/resource]`.
    Parameters in square brackets are optional.

    Otherwise, configuration of LoadBalancing and/or FaultTolerance (please, check corresponding classes)
  * **port** (*int* *,* *str* *,* *optional*) – The port number of the remote tick-server.
    If not specified here, can be specified in the `host` parameter.
  * **protocol** (*str* *,* *optional*) – The protocol to connect with.
    If not specified here, can be specified in the `host` parameter.
  * **resource** (*str* *,* *optional*) – The resource of the host.
    If not specified here, can be specified in the `host` parameter.
  * **cep** (*bool*) – Specifies if the remote server is the CEP-mode tick-server.

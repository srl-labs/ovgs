# OVGS

## URL Endpoint

```
ov-sztp-qa.ext.net.nokia.com
```

## GRPC Interface
For these examples, we will use grpcurl to demonstrate the usage. 

### Login with username/password

``` bash
docker run --network=host -v`pwd`:/mnt -w /mnt --rm -ti \
grpc2sasitest grpcurl -insecure -proto login.proto \
-d '{"username": "user1", "password":"pass1223", "org_id":"org1"}' \
$ADDR:443 login.v1.LoginService/Login
```

This will return a token such as:
``` bash
eyJhbGciOiJSUzI1NiIsInR5cCI6IkpXVCJ9.eyJ1c2VyIjoidXNlcjEiLCJvcmciOns \
ib3JnIjoib3JnMSIsInJvbGUiOiJBRE1JTiJ9fQ. \
bEfftl4SGeuzmJ7na9PytYqs_f1WwGrIwN0V0I7Gd68k2FwwVPahPNc73unAb1sLeOcy \
tID4MyVwGQQ3t9pF_MghB_dCw-iTy52Vs6cYbyR0yeOqidib1M7C4ytw6JRkqJC4cFAS \
ymVLTOrPfrDcE7V30U0tGsZcCiOx5IYoQWrkwsX6lLZDi6PHxfre7V0WaVFSJ5iMZc7P \
r-bo6L8zUqT-ScU-Nh3F2rjwGxZwMjyRCxZbiz15D7you0KxImHwh7nAh2a-UYxIu-i4 \
_CiY3yt4oEa51QaIKxtpNe0NNr7atfRKjO55VMzSHLeuDFxn-trYCqAfFSRfAM7TUTXn \
0WU1qxvv6YrNGjuylb-tcnSgjdQBsrl9Dum1AjFJClSH8zETPetY5afFbdc2Ls78S7_8 \
tzPimDt8l0_IsqPY2L4WBJFswpcFA1VoPqHTT71bMQPbjmbThjxJOlFL-eUO90UD0KqT \
J0zRh58u7ruEsPqGyNjKky63JfqkQ8oe7_wX-xFWH6xtClBwL-Vf6w75oJ3Uo43926PO \
s_iYGbzlQIYL9ecKWydHsY6DTgfxa0bTedF6smlCqkqJopSu-f9xGEDCwOuzFqT-nxij \
FfEFq8PQG6tw0zN6yKNK8t23CUYT6u2bd0_uUmerqgE-cwv32qr9Z8c2KZSAepyEzg0y \
vRg
```
The token can then be used for the next calls
``` bash
docker run --network=host -v`pwd`:/mnt -w /mnt --rm -ti \
grpc2sasitest grpcurl -insecure -H "authorization:  $TOKEN" \
-proto ovgs.proto -d '{"parent": "org-acmeco", "description": "default"}' \
$ADDR:443 ovgs.v1.OwnershipVoucherService/CreateGroup
```

### Create groups, Assign roles to group/users, Create certs, Assign serials

Please see documentation at [https://github.com/openconfig/ovgs](https://github.com/openconfig/ovgs)
